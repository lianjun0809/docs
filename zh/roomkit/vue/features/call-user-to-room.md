> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

会中呼叫功能允许会议内的用户（邀请者）向房间外的其他用户（被邀请者）发送实时入会邀请。该功能基于 `Atomicx State Hooks` 实现，能够帮助开发者快速构建具有主动邀约能力的互动场景。

## 适用场景
- **协同办公：**在进行远程会议时，若涉及跨部门决策，可一键呼叫外部专家快速入会，缩短沟通链路。

- **直播教学：**老师在授课过程中，若发现部分学生缺席，可直接邀请其加入课堂。

- **互联网医疗会诊：**首诊医生在病历分析过程中，通过呼叫功能邀请上级医生进入虚拟诊室进行多方会诊，或者医生呼叫在等候室的患者进行问诊。


## 前提条件

在接入功能前，请确保满足以下条件：
- **邀请者 (User A)：**用户已经通过 `useLoginState` 完成登录鉴权，参考 [接入概览](https://write.woa.com/document/197379797539790848)，并已作为一个房间的房主或成员在房间内，参考 [房间周期](https://write.woa.com/document/197379861957083136)。

- **被邀请者 (User B)：**用户已经通过 `useLoginState` 完成登录鉴权，参考 [接入概览](https://write.woa.com/document/197379797539790848)，以便接收信令事件。

- **环境依赖：**项目已正确安装并引入 `tuikit-atomicx-vue3`。


## 实现会中呼叫功能

实现会中呼叫的核心流程如下：

![会中呼叫时序图](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027160512/82ba8603dee611f0a4f35254007c27c5.png)

会中呼叫时序图


### 步骤1：发起呼叫（邀请者）

邀请者调用 [callUserToRoom](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#callUserToRoom) 接口发起邀请。请确保邀请者当前已在房间内（即 [currentRoom](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#currentRoom) 不为空），否则无法发起呼叫。
``` typescript
import { useRoomState } from 'tuikit-atomicx-vue3/room';

const { currentRoom, callUserToRoom } = useRoomState();

const inviteUser = async () => {
  // 会中呼叫必须关联一个已存在的 roomId，因此需先校验当前用户的进房状态
  if (!currentRoom.value) {
    console.warn('请先进入房间再发起邀请');
    return;
  }

  try {
    const resultMap = await callUserToRoom({
      roomId: currentRoom.value.roomId, // 被邀请者将要加入的房间 ID
      userIdList: ['user1', 'user2'],    // 目标用户 ID 数组，支持单人或多人
      timeout: 60,                        // 邀请有效时长（秒），超时后双方会触发 onCallTimeout
      // extensionInfo 可用于传递业务自定义数据，例如邀请类型、附加消息等
      extensionInfo: JSON.stringify({ type: 'emergency', priority: 'high' }) 
    });
    
    // resultMap 返回每个 userId 对应的状态，例如 Success、AlreadyInRoom (已在房) 或 AlreadyInCalling (通话中)
    console.log('邀请发送完成，详情状态映射:', resultMap);
  } catch (error) {
    console.error('呼叫请求发送失败，请检查网络或登录状态:', error);
  }
};
```

### 步骤2：监听呼叫事件（被邀请者）

被邀请者需要监听 `onCallReceived` 事件。建议在例如 `App.vue`等长驻组件中实现，以确保无论用户在哪个页面都能响应。
``` typescript
import { ref, onMounted, onUnmounted } from 'vue';
import { useRoomState, RoomEvent } from 'tuikit-atomicx-vue3/room';

const { 
  subscribeEvent, 
  unsubscribeEvent, 
  acceptCall, 
  rejectCall, 
  joinRoom, 
  currentRoom 
} = useRoomState();

const showInviteDialog = ref(false); // 控制 UI 弹窗显隐
const currentCallInfo = ref(null);   // 缓存收到的邀请上下文

const handleCallReceived = async ({ roomInfo, call, extensionInfo }) => {
  // 冲突处理：如果用户当前已经在会议中，根据业务策略通常应直接拒绝新邀请，防止干扰
  if (currentRoom.value?.roomId) {
    await rejectCall({ roomId: roomInfo.roomId });
    return;
  }

  // 记录邀请详情，用于在 UI 上展示邀请者名称或业务透传数据
  currentCallInfo.value = { roomInfo, call };
  showInviteDialog.value = true;
};

// 接受邀请逻辑
const onUserAccept = async () => {
  if (!currentCallInfo.value) return;
  const { roomId } = currentCallInfo.value.roomInfo;

  try {
    // 关键流程 A：响应信令。告知邀请者已接受，使其能更新 UI（例如显示“对方已接听”）
    await acceptCall({ roomId });
    
    // 关键流程 B：执行进房。只有调用 joinRoom 才会真正开启音视频推拉流链路
    await joinRoom({ roomId }); 
  } catch (error) {
    console.error('接受呼叫后的进房操作失败:', error);
  } finally {
    closeDialog();
  }
};

// 拒绝邀请逻辑
const onUserReject = async () => {
  if (currentCallInfo.value) {
    // 告知邀请者已拒绝，邀请者会收到 onCallRejected 事件
    await rejectCall({ roomId: currentCallInfo.value.roomInfo.roomId });
  }
  closeDialog();
};

const closeDialog = () => {
  showInviteDialog.value = false;
  currentCallInfo.value = null;
};

// 事件全生命周期管理：确保在组件挂载时监听，销毁时移除，防止事件溢出
onMounted(() => {
  subscribeEvent(RoomEvent.onCallReceived, handleCallReceived);
  
  // 监听导致邀请结束的各种异常/同步事件，确保 UI 弹窗能及时闭合
  subscribeEvent(RoomEvent.onCallCancelled, closeDialog); // 邀请者取消了呼叫
  subscribeEvent(RoomEvent.onCallTimeout, closeDialog);   // 呼叫超时未响应
  subscribeEvent(RoomEvent.onCallHandledByOtherDevice, closeDialog); // 用户在其他设备已处理该呼叫
});

onUnmounted(() => {
  // 移除所有监听器，避免在组件销毁后继续执行 handleCallReceived 导致内存泄漏或报错
  unsubscribeEvent(RoomEvent.onCallReceived, handleCallReceived);
  unsubscribeEvent(RoomEvent.onCallCancelled, closeDialog);
  unsubscribeEvent(RoomEvent.onCallTimeout, closeDialog);
  unsubscribeEvent(RoomEvent.onCallHandledByOtherDevice, closeDialog);
});
```

## 实践教程：提升呼叫接通率

为了在业务中获得更高的呼叫接通率，除了基础功能的实现外，建议参考以下策略优化用户体验：

### 1. 增强呼叫感知（避免用户遗漏）

由于 Web 端特性，浏览器静音或页面处于后台运行状态可能导致用户遗漏呼叫。
- **视觉提醒**：利用 [Page Visibility API](https://developer.mozilla.org/en-US/docs/Web/API/Page_Visibility_API) 检测页面可见性状态。若页面处于后台，可通过循环修改 `document.title` 实现标题栏闪烁提示（例如：“【新邀请】UserA 邀请您入会...”），以吸引用户注意。

- **听觉提醒**：在 `onCallReceived` 事件触发时播放高优先级的提示铃声。注意：需遵循浏览器的 [自动播放策略](https://developer.mozilla.org/zh-CN/docs/Web/Media/Guides/Autoplay)，大部分浏览器在缺乏用户交互（例如点击、触摸或按键）的情况下会限制音频自动播放。


### 2. 丰富邀请上下文（提升接听意愿）

缺乏明确意图的邀请容易被用户拒绝。建议充分利用 `extensionInfo` 字段传递关键业务信息，以提升用户的接听意愿。
- **传递业务上下文**：利用 `extensionInfo` 透传如 `reason`（例如：“项目紧急评审”）、`level`（例如：“P0故障排查”）等业务字段，告知用户呼叫的紧迫性和重要性。


### 3. 多通道触达兜底（确保消息可达）

受限于 Web 端机制，浏览器进程结束将无法接收实时信令。建议采取以下替代方案以确保触达：
- **浏览器系统通知**：引导用户授权 [Web Notification API](https://developer.mozilla.org/en-US/docs/Web/API/Notification)。只要浏览器进程未关闭（包括最小化或在后台标签页），即可触发操作系统级别的弹窗通知，有效提醒用户。

- **多通道触达**：建议结合业务后端逻辑，在检测到用户不在线或超时未响应时，通过**短信**、**邮件**或**企业微信**等外部渠道发送入会链接，实现全方位触达。


### 4. 智能重试机制（解决“接受邀请后进房失败”）

在弱网或其他不稳定环境下，用户点击接受邀请后调用 `joinRoom` 可能会出现偶发性失败。
- **自动重试**：建议在 `onUserAccept` 的异常处理逻辑（`catch`）中引入 2-3 次自动重试机制（推荐结合指数退避策略），以最大程度确保用户点击“接受”后能成功加入会议。


## 开发注意事项
1. **接受邀请不等于进房**


   `acceptCall` 仅仅是信令层面的回复（告知对方已接听）。用户必须在调用 `acceptCall` 后紧接着手动调用 `await joinRoom({ roomId })` 才能真正进入音视频房间。

2. **生命周期管理**


   请务必在组件销毁周期（`onUnmounted`）调用 `unsubscribeEvent`。如果不清理监听器，当用户切换页面时，旧页面的监听器会残留在内存中，导致一次邀请弹出多个窗口或逻辑重复执行。

3. **超时设置**


   如果不设置 `timeout` 参数，在某些网络异常或程序崩溃情况下，邀请可能长期处于挂起状态，导致无法再次对该用户发起呼叫。建议设置为 30-60 秒。


## 常见问题
1. **如何在呼叫时带上自定义参数（如“来自XX的紧急会议”）？**


   使用 `callUserToRoom` 的 `extensionInfo` 参数传递 JSON 字符串。被邀请者可以在 `onCallReceived` 事件的 `extensionInfo` 字段中解析该字符串获取业务信息。

2. **被邀请者如果不在线，上线后能收到邀请吗？**


   不可以。邀请事件是一个瞬时信令动作，SDK 目前不会补发离线期间收到的呼叫通知。

3. **可以取消已发出的邀请吗？**


   可以。调用 `cancelCall({ roomId, userIdList })` 即可撤销。此时被邀请者会收到 `onCallCancelled` 事件，您需要监听此事件来关闭被邀请端的 UI 弹窗。

4. **接受后进房失败怎么办？**


   检查是否已登录 `TUIRoomEngine`，重试 `joinRoom({ roomId })` 并捕获错误提示用户；必要时在 UI 上提供“重试”按钮。

5. **对方忙线或已在其他房间如何提示？**


   `callUserToRoom` 的返回值 `resultMap` 中若出现 `AlreadyInRoom` / `AlreadyInCalling`，应在邀请者 UI 提示“对方忙线/已在会中”，并决定是否稍后重试。

6. **超时/取消后弹窗不关闭？**


   确保监听 `onCallTimeout`、`onCallCancelled`、`onCallHandledByOtherDevice`，统一在回调里关闭弹窗、清理当前邀请数据。

7. **多设备同时响铃如何处理？**


   在任意设备接受/拒绝后，其余设备会收到 `onCallHandledByOtherDevice`，需关闭其他端弹窗避免重复处理。

8. **extensionInfo 该怎么约定？**


   建议使用 JSON 字符串并约定字段（例如 `type`、`priority`、`from`），在 `handleCallReceived` 时解析后展示友好文案（例如“来自XX的紧急会议”）。


## **示例项目**

腾讯云在 GitHub 上提供了示例项目 [atomicx-vite-vue3-ts](https://github.com/Tencent-RTC/TUIRoomKit/tree/main/Web/example/atomicx-vite-vue3-ts) ，您可以参考以实现完整的 RoomKit 功能。

## API 文档
<table>
<tr>
<td rowspan="1" colSpan="1" >**State/Component**</td>

<td rowspan="1" colSpan="1" >**功能描述**</td>

<td rowspan="1" colSpan="1" >**API 文档**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**useRoomState**</td>

<td rowspan="1" colSpan="1" >房间状态管理（创建、加入、预约等）</td>

<td rowspan="1" colSpan="1" >[API 文档](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#module-RoomState)</td>
</tr>
</table>
