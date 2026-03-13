> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

预定房间功能允许用户提前规划会议时间、主题和入会密码。通过该功能，用户可以创建未来的会议计划，生成专属的会议号和入会链接，方便提前通知参会人员。

## 适用场景
- **企业定期会议：** 提前安排周会、月会，确保参会者提前收到通知。

- **在线课堂排课：** 老师可以提前设置好一周的课程表。

- **远程面试预约：** HR 为面试者和面试官预约特定的时间段。

## 前提条件
- **用户状态：** 用户已经通过 useLoginState 完成登录鉴权，参考 接入概览，处于**已登录**状态才能发起预定或查看预定列表。

- **环境依赖：** 项目已引入 `tuikit-atomicx-vue3`。

## 实现预定房间功能

本功能提供两种集成方案，您可以根据业务需求选择最适合的一种：
- **方案一（推荐）：** 使用 UI 组件快速集成。直接引入 `tuikit-atomicx-vue3` 提供的预定房间面板（[ScheduleRoomPanel](https://github.com/Tencent-RTC/TUIKit_Vue3/blob/main/packages/tuikit-atomicx-vue3/src/components/ScheduleRoomPanel/ScheduleRoomPanel.vue)）和预定房间列表组件（[ScheduledRoomList](https://github.com/Tencent-RTC/TUIKit_Vue3/blob/main/packages/tuikit-atomicx-vue3/src/components/ScheduleRoomPanel/ScheduledRoomList.vue)），开发成本最低。

- **方案二（高级）：** 使用底层 API 自定义集成。基于 atomicx-core SDK API `useRoomState` 状态钩子自行实现 UI 和交互逻辑，灵活度最高。

   

## 方案一：使用 UI 组件快速集成

`tuikit-atomicx-vue3` 提供了两个核心组件：
- [**ScheduleRoomPanel**](https://github.com/Tencent-RTC/TUIKit_Vue3/blob/main/packages/tuikit-atomicx-vue3/src/components/ScheduleRoomPanel/ScheduleRoomPanel.vue)**：**预定会议的配置面板，包含时间选择、成员邀请等功能。

- [**ScheduledRoomList**](https://github.com/Tencent-RTC/TUIKit_Vue3/blob/main/packages/tuikit-atomicx-vue3/src/components/ScheduleRoomPanel/ScheduledRoomList.vue)**：**展示当前用户的预定会议列表，支持点击入会、修改和取消预定。

### 步骤1：引入组件
``` typescript
import { ScheduleRoomPanel, ScheduledRoomList } from 'tuikit-atomicx-vue3/room';
```

### 步骤2：使用组件

在您的页面中，可以直接组合使用这两个组件。
``` typescript
<template>
  <UIKitProvider theme="light" language="zh-CN">
    <div class="schedule-container">
      <!-- 预定按钮，点击后显示预定弹窗 -->
      <button @click="showSchedulePanel = true">
        预定会议
      </button>

      <!-- 预定列表组件 -->
      <div class="list-container">
        <!-- 监听 join-room 事件处理入会逻辑 -->
        <ScheduledRoomList @join-room="handleJoinRoom" />
      </div>

      <!-- 预定面板弹窗 -->
      <!-- 建议将其包裹在 Dialog 或 Modal 组件中 -->
      <div v-if="showSchedulePanel" class="modal-mask">
        <div class="modal-content">
          <ScheduleRoomPanel
            @confirm="handleScheduleConfirm"
            @cancel="showSchedulePanel = false"
          />
        </div>
      </div>
    </div>
  </UIKitProvider>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { UIKitProvider } from '@tencentcloud/uikit-base-component-vue3';
import { ScheduleRoomPanel, ScheduledRoomList, useRoomState } from 'tuikit-atomicx-vue3/room';

const { joinRoom } = useRoomState();

const showSchedulePanel = ref(false);

const handleScheduleConfirm = (roomId: string, options: Record<string, any>) => {
  console.log('预定成功', roomId, options);
  showSchedulePanel.value = false;
  // 可选：显示邀请弹窗或复制链接
};

const handleJoinRoom = async (roomInfo: { roomId: string }) => {
  console.log('点击入会', roomInfo.roomId);
  await joinRoom(roomInfo.roomId); 
};
</script>

<style scoped>
.schedule-container{padding:24px;max-width:1000px;margin:0 auto;font-family:-apple-system,BlinkMacSystemFont,'Segoe UI',Roboto,'Helvetica Neue',Arial,sans-serif}button{background-color:#006eff;color:#fff;border:none;padding:10px 20px;border-radius:4px;cursor:pointer;font-size:14px;font-weight:500;transition:background-color .2s;margin-bottom:24px}button:hover{background-color:#0056cc}.list-container{background:#fff;border-radius:8px;box-shadow:0 2px 8px rgba(0,0,0,.05);padding:16px}.modal-mask{position:fixed;top:0;left:0;right:0;bottom:0;background-color:rgba(0,0,0,.4);backdrop-filter:blur(4px);display:flex;align-items:center;justify-content:center;z-index:1000}.modal-content{background-color:#fff;border-radius:8px;box-shadow:0 4px 16px rgba(0,0,0,.1);padding:24px;width:100%;max-width:480px}
</style>
```

## 方案二：使用底层 API 自定义集成

本节主要介绍如何通过 atomicx-core SDK API [useRoomState](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#module-RoomState) 接口来实现预定房间的核心逻辑。

预定房间时序图

### 步骤1：发起预定

使用 [scheduleRoom](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#scheduleRoom) 方法创建一个新的预定会议。您需要指定会议的开始时间、结束时间以及房间名称等信息。
``` typescript
import { useRoomState } from 'tuikit-atomicx-vue3/room';

const { scheduleRoom } = useRoomState();

const createSchedule = async () => {
  try {
    // roomId 限制：字符串类型，必传参数，建议随机生成
    const roomId = '123456'; 
    
    // 注意：时间戳单位必须为 **秒** (Date.getTime() 获取的是毫秒，需除以 1000)
    const startTime = Math.floor(new Date().getTime() / 1000) + 3600; // 1小时后开始
    const duration = 1800; // 30分钟

    const options = {
      roomName: '产品需求评审会',
      scheduleStartTime: startTime, // 单位：秒
      scheduleEndTime: startTime + duration, // 单位：秒
      scheduleAttendees: ['userA', 'userB'], // 邀请参会成员ID列表
      password: '123', // 可选：设置入会密码
      isAllMicrophoneDisabled: false, // 可选：是否全体禁麦
      isAllCameraDisabled: false,     // 可选：是否全体禁画
    };

    await scheduleRoom({ roomId, options });
    console.log('预定成功', roomId);
  } catch (error) {
    console.error('预定失败', error);
  }
};
```

### 步骤2：获取预定列表

使用 [getScheduledRoomList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getScheduledRoomList) 方法拉取当前用户的预定会议列表。列表数据会响应式更新到 [scheduledRoomList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#scheduledRoomList) 状态中。
``` typescript
import { onMounted, watch } from 'vue';
import { useRoomState } from 'tuikit-atomicx-vue3/room';

const { 
  scheduledRoomList,      // 响应式数据：预定会议列表
  getScheduledRoomList    // 方法：拉取列表
} = useRoomState();

// 初始化加载列表
onMounted(async () => {
  // cursor 表示从哪里开始拉取数据，空字符串表示从头开始
  // getScheduledRoomList 返回值包含新的 cursor
  const { cursor } = await getScheduledRoomList({ cursor: '' }); 
  // 如果 cursor 不为空，表示还有更多数据，可继续调用拉取
});

// 监听列表变化，实时更新 UI
watch(scheduledRoomList, (list) => {
  console.log('当前预定列表：', list);
});
```

### 步骤3：修改预定

如果需要调整已预定会议的时间或主题，可以使用 [updateScheduledRoom](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#updateScheduledRoom) 方法。
``` typescript
import { useRoomState } from 'tuikit-atomicx-vue3/room';

const { updateScheduledRoom } = useRoomState();

const updateRoom = async (roomId: string) => {
  try {
    const newStartTime = Math.floor(new Date().getTime() / 1000) + 7200; // 延后2小时
    const options = {
      roomName: '产品需求评审会（改期）',
      scheduleStartTime: newStartTime,
      scheduleEndTime: newStartTime + 1800,
    };

    await updateScheduledRoom({ roomId, options });
    console.log('修改成功');
  } catch (error) {
    console.error('修改失败', error);
  }
};
```

### 步骤4：取消预定

如果需要取消某个已预定的会议，可以调用 [cancelScheduledRoom](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#cancelScheduledRoom) 方法。
``` typescript
import { useRoomState } from 'tuikit-atomicx-vue3/room';

const { cancelScheduledRoom } = useRoomState();

const cancelRoom = async (roomId: string) => {
  try {
    await cancelScheduledRoom({ roomId });
    console.log('取消成功');
    // 取消成功后，scheduledRoomList 会自动更新，无需手动重新拉取
  } catch (error) {
    console.error('取消失败', error);
  }
};
```

### 步骤5：处理入会密码

对于设置了密码的预定会议，在调用 [joinRoom](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#joinRoom) 接口入会时，需要捕获鉴权失败的错误，并引导用户输入密码。
``` typescript
import { useRoomState, TUIErrorCode } from 'tuikit-atomicx-vue3/room';

const { joinRoom } = useRoomState();

const enterRoom = async (roomId: string, password?: string) => {
  try {
    await joinRoom({ roomId, password });
  } catch (error: any) {
    // 捕获特定错误码，TUIErrorCode.ERR_NEED_PASSWORD (-2010)
    if (error.code === TUIErrorCode.ERR_NEED_PASSWORD) {
      console.log('该房间需要密码，请引导用户输入');
      // 1. 弹出密码输入框
      // 2. 获取用户输入的密码 inputPassword
      // 3. 重新调用 enterRoom(roomId, inputPassword)
    } else if (error.code === TUIErrorCode.ERR_WRONG_PASSWORD) {
      console.error('密码错误，请重新输入');
    } else {
      console.error('入会失败', error);
    }
  }
};
```

### 步骤6：监听预定事件

除了被动响应数据变化，您还可以监听特定的预定事件来处理业务逻辑，例如在会议即将开始时弹出提醒。
``` typescript
import { onMounted, onUnmounted } from 'vue';
import { useRoomState, RoomEvent } from 'tuikit-atomicx-vue3/room';

const { subscribeEvent, unsubscribeEvent } = useRoomState();

// 会议即将开始通知（默认为开始前5分钟）
const handleRoomStartingSoon = (info: { roomInfo: any }) => {
  console.log('会议即将开始：', info.roomInfo.roomName);
  // 可在此处实现 Toast 提醒或系统通知
};

// 会议被取消通知
const handleRoomCancelled = (info: { roomInfo: any; operateUser: any }) => {
  console.log(`会议 ${info.roomInfo.roomName} 已被 ${info.operateUser.userName} 取消`);
};

// 收到新的会议邀请通知
const handleRoomAdded = (info: { roomInfo: any }) => {
  console.log('收到新的会议邀请：', info.roomInfo.roomName);
};

// 被移出会议通知
const handleRemovedFromRoom = (info: { roomInfo: any; operateUser: any }) => {
  console.log(`您已被 ${info.operateUser.userName} 移出会议 ${info.roomInfo.roomName}`);
};

onMounted(() => {
  // 注册事件监听
  subscribeEvent(RoomEvent.onScheduledRoomStartingSoon, handleRoomStartingSoon);
  subscribeEvent(RoomEvent.onScheduledRoomCancelled, handleRoomCancelled);
  subscribeEvent(RoomEvent.onAddedToScheduledRoom, handleRoomAdded);
  subscribeEvent(RoomEvent.onRemovedFromScheduledRoom, handleRemovedFromRoom);
});

onUnmounted(() => {
  // 移除事件监听
  unsubscribeEvent(RoomEvent.onScheduledRoomStartingSoon, handleRoomStartingSoon);
  unsubscribeEvent(RoomEvent.onScheduledRoomCancelled, handleRoomCancelled);
  unsubscribeEvent(RoomEvent.onAddedToScheduledRoom, handleRoomAdded);
  unsubscribeEvent(RoomEvent.onRemovedFromScheduledRoom, handleRemovedFromRoom);
});
```

## 开发注意事项
1. **时间戳单位**：SDK 中涉及的所有时间参数（例如 `scheduleStartTime`、`scheduleEndTime`）单位均为 **秒**，而非 JavaScript 中 `Date` 对象默认的毫秒。在传参前请务必执行 `/ 1000` 操作。

2. **样式引入**：使用 UI 组件时，务必引入 `UIKitProvider`，否则组件样式将无法正常渲染。

3. **RoomID 建议**：虽然 `scheduleRoom` 允许前端传入 `roomId`，但为了避免 ID 冲突，建议该 ID 由业务后端生成并保证全局唯一。

4. **分页处理**：预定列表可能会很长，`getScheduledRoomList` 接口支持分页拉取。请关注返回值中的 `cursor` 字段，若不为空，则说明还有更多数据。

## 常见问题
1. **预定成功但列表不更新？**

   请确认已登录且首屏调用过 `getScheduledRoomList`（例如 `cursor: ''`）。返回的 `cursor` 不为空需继续拉取；列表是响应式的，更新后 UI 会同步。

2. `joinRoom`** 参数怎么传？**

   推荐统一使用对象入参：`joinRoom({ roomId, password })`，避免直接传字符串导致类型不匹配或后续扩展受限。

3. **时间戳用毫秒导致预约失败？**

   所有时间相关参数必须是秒，`Date.now()` 需 `/ 1000`，否则会返回时间冲突错误。

4. **房间设置了密码如何处理？**

   捕获 `TUIErrorCode.ERR_NEED_PASSWORD` / `ERR_WRONG_PASSWORD`，弹出密码输入框，重新 `joinRoom({ roomId, password })`；错误多次后可提示联系房主重置。

5. **roomId 冲突或重复？**

   建议由后端生成全局唯一 roomId；如果前端生成，请在调度前检查冲突并做好重试策略。

6. **分页怎么继续拉取？**

   `getScheduledRoomList` 返回的 `cursor` 不为空时继续传入；为空表示已拉完。

## **示例项目**

腾讯云在 GitHub 上提供了示例项目 [atomicx-vite-vue3-ts](https://github.com/Tencent-RTC/TUIRoomKit/tree/main/Web/example/atomicx-vite-vue3-ts) ，您可以参考以实现完整的 RoomKit 功能。

## API 文档
| **State/Component** | **功能描述** | **API 文档** |
| --- | --- | --- |
| **useRoomState** | 房间状态管理（创建、加入、预约等） | [API 文档](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#module-RoomState) |
