> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

本篇文档旨在指导 uniapp 开发者如何使用 `AtomicXCore` 框架中的 `BarrageState` 模块，为您的直播应用快速集成功能丰富、性能卓越的弹幕系统。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100028028022/51f80cd8bbbc11f0b4c35254001c06ec.png)


## 核心功能

`BarrageState` 为您的直播应用提供了一套完整的弹幕解决方案，核心功能包括：
- 接收并展示直播间弹幕消息。

- 发送文本弹幕与观众互动。

- 发送自定义业务弹幕，以支持礼物、点赞等复杂场景。

- 在本地消息列表中插入系统提示（例如，“欢迎 XX 进入直播间”）。


## 实现步骤

### 步骤1：组件集成

请参考 [开始直播](https://write.woa.com/document/191127271985012736) 集成 **AtomicXCore**，完成接入。

### 步骤2：初始化并监听弹幕

获取一个与当前直播间 `liveID` 绑定的 `BarrageState` 实例，并且监听 `messageList` 来接收最新的**全量**弹幕消息列表。
``` typescript
import { useBarrageState } from "@/uni_modules/tuikit-atomic-x/state/BarrageState";
import { watch } from 'vue';

// liveID 是语聊房的唯一标识
const liveID = 'your_live_id'; // 替换为实际的语聊房 liveID

//通过 liveID 获取 BarrageState 的实例
const { messageList } = useBarrageState(liveID);

// 监听 messageList 的实时变更，用于驱动 UI 更新
watch(messageList, (newVal, oldVal) => {
    console.log(newVal)
})
```

### 步骤3：发送文本弹幕

调用 `sendTextMessage` 方法向直播间内的所有用户广播一条纯文本消息。
``` typescript
import { useBarrageState } from "@/uni_modules/tuikit-atomic-x/state/BarrageState";

// liveID 是语聊房的唯一标识
const liveID = 'your_live_id'; // 替换为实际的语聊房 liveID

//通过 liveID 获取 BarrageState 的实例
const { sendTextMessage } = useBarrageState(liveID);

const sendMessage = () => {
    sendTextMessage({
      liveID: 'xxx', // 当前直播间的 liveID
      text: 'xxx', // 您想要发送的弹幕     
      success: () => {
        console.log("弹幕发送成功")
      },
      fail: (error) => {
        console.log("弹幕发送失败", error)
      } 
    })
}
```

#### **接口参数**
<table>
<tr>
<td rowspan="1" colSpan="1" >**参数**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`liveID`</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >当前直播间的`liveID`。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`text`</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >要发送的文本内容。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`success`</td>

<td rowspan="1" colSpan="1" >`Function`</td>

<td rowspan="1" colSpan="1" >发送成功的回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`fail`</td>

<td rowspan="1" colSpan="1" >`Function`</td>

<td rowspan="1" colSpan="1" >发送失败的回调。</td>
</tr>
</table>


### 步骤4：发送自定义弹幕

发送一条包含自定义业务逻辑的消息，例如礼物、点赞或游戏化互动指令。这条消息对其他客户端来说是透明的，需要业务层自行解析。
``` typescript
import { useBarrageState } from "@/uni_modules/tuikit-atomic-x/state/BarrageState";

// liveID 是语聊房的唯一标识
const liveID = 'your_live_id'; // 替换为实际的语聊房 liveID

//通过 liveID 获取 BarrageState 的实例
const { sendCustomMessage } = useBarrageState(liveID);

/// 发送一条自定义弹幕，例如用于发送礼物
const sendGiftMessage = ( giftID: string, giftCount: number ) => {
    // 1. 定义一个能识别业务的ID 
    const businessID = "live_gift"
    // 2. 将业务数据编码为 JSON 字符串
    const giftData = { "gift_id": giftId, "gift_count": giftCount }
    // 3. 调用核心API发送自定义消息
    sendCustomMessage({
      liveID: 'xxx', // 当前直播间的 liveID
      businessID,
      data: JSON.stringify(giftData),     
      success: () => {
        console.log("礼物消息发送成功")
      },
      fail: (error) => {
        console.log("礼物消息发送失败", error)
      }
    })
}
```

#### **接口参数**
<table>
<tr>
<td rowspan="1" colSpan="1" >**参数**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`liveID`</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >当前直播间的`liveID`。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`businessId`</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >业务唯一标识符，例如 "live_gift"，用于接收端区分不同的自定义消息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`data`</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >业务数据，通常为 JSON 格式的字符串。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`success`</td>

<td rowspan="1" colSpan="1" >`Function`</td>

<td rowspan="1" colSpan="1" >发送成功的回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`fail`</td>

<td rowspan="1" colSpan="1" >`Function`</td>

<td rowspan="1" colSpan="1" >发送失败的回调。</td>
</tr>
</table>


### 步骤5：在本地插入提示消息

在当前用户的消息列表中插入一条本地消息，这条消息不会被发送到直播间的其他用户。这非常适合用来显示系统欢迎、警告或操作提示等信息。
``` typescript
import { useBarrageState } from "@/uni_modules/tuikit-atomic-x/state/BarrageState";

// liveID 是语聊房的唯一标识
const liveID = 'your_live_id'; // 替换为实际的语聊房 liveID

//通过 liveID 获取 BarrageState 的实例
const { appendLocalTip } = useBarrageState(liveID);
const showWelcomeMessage = (user: LiveUserInfo) => {
    // 创建一条本地提示消息
    let welcomeTip = {}
    welcomeTip.liveID = liveID;
    welcomeTip.sender = { userID: 'xxx' };
    welcomeTip.sequence = Date.now();
    welcomeTip.timestampInSecond = Date.now();
    welcomeTip.messageType = 'TEXT';
    welcomeTip.textContent = "欢迎 ${user.userName} 进入直播间！";
    // 调用 BarrageStore 的接口将其插入弹幕列表
    appendLocalTip(welcomeTip)
}
```

#### **接口参数**
<table>
<tr>
<td rowspan="1" colSpan="1" >**参数**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`message`</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >要在本地插入的消息对象。SDK 会将此消息对象追加到 `BarrageState` 的 `messageList` 中。</td>
</tr>
</table>


### 步骤6：管理用户发言（禁言与解禁）

作为主播或管理员，您可以对直播间内的用户发言权限进行管理，维护健康的社区氛围。

#### 禁止/解禁单个用户发言

通过 `LiveAudienceState` 中的 `disableSendMessage` 接口来实现对指定用户的禁言或解禁。此状态会被持久化，即使用户重新进入直播间，禁言状态依然有效。
``` typescript
import { useLiveAudienceState } from '@/uni_modules/tuikit-atomic-x/state/LiveAudienceState';

// liveID 是语聊房的唯一标识
const liveID = 'your_live_id'; // 替换为实际的语聊房 liveID

// 1. 通过 liveID 获取 LiveAudienceState 的实例
const { disableSendMessage } = useLiveAudienceState(liveID)

// 2. 定义要操作的用户 ID 和禁言状态
const userIdToMute = "user_id_to_be_muted"
const shouldDisable = true // true为禁言, false为解禁

// 3. 调用接口执行操作
const handleDisableSendMessage = () => {
    disableSendMessage({
      liveID: 'xxx', // 当前直播间 liveID
      userID: userIdToMute,
      isDisable: shouldDisable,
      success: () => {
        console.log(`${shouldDisable ? "禁言" : "解禁"}用户 ${userIdToMute}成功`)
      },
      fail: (error) => {
        console.log("操作失败", error)
      }
    })
}
```

#### 开启/关闭全体禁言

要对直播间内所有用户（通常不包括主播自己）进行禁言，您需要通过 `LiveListState` 的 `updateLiveInfo` 更新直播间信息来实现。
``` typescript
// 1. 获取 LiveListState 的实例
const { updateLiveInfo, currentLive } = useLiveListState();

// 2. 获取当前直播间信息，并修改全体禁言状态
currentLive.value.isMessageDisable = true // true 为全体禁言, false 为关闭

// 3. 调用更新接口，并指定修改的标志位
const handleUpdateLiveInfo = () => {
    updateLiveInfo({
      liveInfo: currentLive.value,
      modifyFlagList: ['IS_MESSAGE_DISABLE'],
      success: () => {
        console.log("全体禁言成功")
      },
      fail: (error) => {
        console.log("操作失败", error)
      }
    })
}

```

## 功能进阶：高并发场景下的性能优化

当您使用 `BarrageState` 构建弹幕功能后，本章将指导您如何处理更复杂的业务场景，确保它能在真实、复杂的高并发直播场景下，依然为用户提供流畅、稳定的体验。本章将围绕两个核心业务场景，为您提供明确的优化方案和代码示例。

### 场景一：应对热门直播间的“弹幕风暴”

#### 场景描述

在一场热门活动中，直播间涌入大量观众，弹幕以每秒数十条的频率刷新。

#### 技术挑战

SDK 会以极高频率返回完整的弹幕列表。如果每次都更新完整的消息列表，主线程会被密集的UI布局和渲染操作阻塞，导致界面卡顿。

#### 优化方案：批处理与流量削峰 (Batch Processing & Debouncing)

不必响应每一次的数据更新，而是设定一个时间阈值（例如300毫秒）。只在距离上次 UI 刷新超过这个阈值后，才执行下一次刷新操作。极大提升流畅度。

#### 代码示例
``` typescript
  import { watch } from 'vue';
  // UI 展示数据
  const mixMessageList = ref()
  // ===== 防抖配置 =====
  const DEBOUNCE_THRESHOLD = 300; // 300毫秒防抖阈值
  let lastUpdateTime = 0;
  let pendingMessages: any[] = []; // 待处理的消息队列
  let debounceTimer: ReturnType<typeof setTimeout> | null = null;

  /**
   * 执行 UI 刷新操作
   */
  const flushMessages = () => {
    if (pendingMessages.length > 0) {
      mixMessageList.value = [...mixMessageList.value, ...pendingMessages]; // 用于 UI 展示的数据
      lastUpdateTime = Date.now(); // 更新最后刷新时间
      pendingMessages = []; // 清空待处理消息
    }
  };

  /**
   * 防抖处理：累积消息直到达到时间阈值
   */
  const debouncedUpdate = (newMessages: any[]) => {
    // 将新消息添加到待处理队列
    pendingMessages.push(...newMessages);

    // 清除之前的定时器
    if (debounceTimer) {
      clearTimeout(debounceTimer);
    }

    const now = Date.now();
    const timeSinceLastUpdate = now - lastUpdateTime;

    // 如果距离上次更新已经超过阈值，立即执行更新
    if (timeSinceLastUpdate >= DEBOUNCE_THRESHOLD) {
      flushMessages();
    } else {
      // 否则设置定时器在阈值时间后执行更新
      const remainingTime = DEBOUNCE_THRESHOLD - timeSinceLastUpdate;
      debounceTimer = setTimeout(() => {
        flushMessages();
        debounceTimer = null;
      }, remainingTime);
    }
  };

  watch(messageList, (newVal, oldVal) => {
    if (!newVal) return;
    const value = newVal.slice((oldVal || []).length, (newVal || []).length);
    if (value.length > 0) {
      debouncedUpdate(value);
    }
  });
```

### 场景二：保障长时间直播的内存稳定性

#### 场景描述

您的应用需要支持数小时乃至全天候的“不间断直播”，例如游戏直播或慢直播。在此期间，App 必须保持稳定运行，不能因为长时间运行而意外退出。

#### 技术挑战

SDK 返回的全量 `messageList` 会在长时间直播中无限增长，即使 `UI` 层做了节流，数据层持有的这个巨大数组也会持续侵占内存，最终导致应用闪退。

#### 优化方案：固定容量的循环数组 (Circular Buffer) 

**只让您自己的数据源（DataSource）持有有限数量的消息**。无论 `SDK` 返回的全量列表有多大，您的应用只截取其中最新的部分用于显示。

#### **代码示例**

在接收到 `SDK` 的全量列表后，只取最新的500条（或您定义的其他数量）来更新 `UI`。
``` typescript
  // ===== 消息窗口配置（只保留最新N条消息）=====
  const MAX_MESSAGES_COUNT = 500;  // 最大消息数，超过则删除最早的消息

  /**
   * 裁剪消息列表：只保留最新的 N 条消息
   * @param messages 待裁剪的消息数组
   * @returns 裁剪后的消息数组
   */
  const trimMessageList = (messages: any[]): any[] => {
    if (messages.length > MAX_MESSAGES_COUNT) {
      // 删除最早的消息，只保留最新的 MAX_MESSAGES_COUNT 条
      const trimmed = messages.slice(messages.length - MAX_MESSAGES_COUNT);
      console.warn(
        `[BarrageList] 消息数量超过限制 ${MAX_MESSAGES_COUNT}，已删除 ${messages.length - MAX_MESSAGES_COUNT} 条最早消息`
      );
      return trimmed;
    }
    return messages;
  };

  // 初始化时应用消息窗口限制
  const mixMessageList = ref<any[]>(trimMessageList(messageList.value || []));
```

## API 文档

关于 [BarrageState](https://liteav.sdk.qcloud.com/doc/product/tuikit/atomic-x/uni-app/zh/v1.0/api/index.html#module-BarrageState) 及其相关类的所有公开接口、属性和方法的详细信息，请参阅随 [AtomicXCore](https://write.woa.com/document/192223419814899712) 框架的官方 API 文档。

## 常见问题

### 除了基础的文本弹幕，我们还希望实现“彩色弹幕”、“礼物弹幕”等更丰富的样式，该如何实现？

这是通过自定义消息 `sendCustomMessage` 来实现的。`BarrageState` 不会限制您的业务想象力。

**实现思路**
1. **定义数据结构:** 与您的客户端和服务器团队共同定义好自定义消息的 JSON 结构。例如，一条彩色弹幕可以这样定义：

   ``` json
   {  "type": "colored_text",  "text": "这是一条彩色弹幕!",  "color": "#FF5733" }
   ```
2. **发送端:** 在发送时，将这个 JSON 结构转换为字符串，并通过 `sendCustomMessage` 的 `data` 参数发送出去。`businessID` 可以设置为一个能代表您业务的唯一标识，例如 "`barrage_style_v1`"。

3. **接收端**: 在接收到弹幕消息后，检查其 `messageType` 是否为 `'CUSTOM'` 以及 `businessID` 是否匹配。如果匹配，则解析 `data` 字符串（通常是解析JSON），根据解析出的数据（例如 `color、text`）来渲染您的自定义UI样式。


### 为什么我调用了 sendTextMessage，但是在消息列表中看不到我发送的消息？

**请按以下步骤排查：**
1. **检查 success，fail 回调**：`sendTextMessage` 方法有成功和失败回调。请检查回调返回的结果是成功还是失败。如果失败，错误信息会明确指出问题所在（例如“您已被禁言”、“网络错误”等）。

2. **确认订阅时机**：确保您对 `barrageState` 的订阅发生在该 `liveID` 对应的直播开始之后。如果在加入直播房间之前就开始监听，可能会错过部分消息。

3. **检查 liveID**：确认您在创建 `BarrageState` 实例、加入直播房间、以及发送消息时使用的 `liveID` 完全一致，包括大小写。

4. **网络问题**：检查设备当前的网络连接是否正常。消息发送依赖于网络。


### 新观众进入直播间时，如何让他们看到加入前的历史弹幕消息？

`AtomicXCore` 支持拉取历史弹幕消息，但这需要您在**服务端控制台**进行一项简单的配置。配置完成后，SDK 会自动处理后续的一切，您无需编写额外的代码。

**步骤1：在 IM 控制台进行配置**
1. 登录您的 [即时通信 IM 控制台](https://cloud.tencent.com/login?s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fim)。

2. 在左侧导航栏按照路径：**消息服务 Chat** >** 功能配置 **>** 群组配置 **> **群功能配置** >** 直播群新成员查看入群前消息量配置**进行导航。

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100028028022/67592599bbbc11f0a808525400bf7822.png)

3. 修改“新成员可查看最近消息数”，最大支持 **50** 条。


   **步骤2：客户端无感获取 **


   完成上述配置后，您的客户端代码**无需做任何改动**。 


   当新用户加入直播间时，`AtomicXCore` 的底层 会自动拉取您配置的历史消息数量。这些历史消息会和实时消息一样，通过您已实现的 `BarrageState` 订阅通道推送给您的 UI 层。您的应用会像接收实时弹幕一样，自然地接收并展示这些历史弹幕。


### 为什么我的弹幕区域没有消息时，遮盖住了其底层区域的点击事件。

在 `nvue` 下，如果您给组件提供默认的宽高，即使该组件没有渲染，它还是会挂载在 `UI` 上。这里建议不要给组件提供默认的宽高，而是根据有没有内容渲染来进行宽高的动态计算。