> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

本篇文档将指导您如何管理房间内的参会者。Atomicx 提供了开箱即用的列表组件 `RoomParticipantList` 用于快速集成，并暴露了 [useRoomParticipantState](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#module-RoomParticipantState) Hook，方便您实现自定义的成员控制逻辑。

## 功能介绍

成员管理模块涵盖了房间内用户信息展示以及权限处理的全套能力：
- **实时列表展示：**动态呈现房间内所有成员的昵称、角色、音视频状态及音量波动。

- **权限控制：**支持房主或管理员执行踢人、全员禁言、转让房主等管理操作。

- **分级管理：**支持对房主、管理员及普通成员实现差异化的权限策略。

## 前提条件
- 用户已经通过 [useLoginState](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#module-LoginState) 完成登录鉴权，请参考 接入概览。

- 用户已经通过 [useRoomState](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#module-RoomState) 进入房间，请参考 房间管理。

## 集成成员管理组件

如果您需要快速构建成员列表界面，推荐直接使用 `RoomParticipantList` 组件。`RoomParticipantList` 是一个开箱即用的参会者列表组件，内置了完整的成员管理 UI 和交互。

集成 `RoomParticipantList` 组件示例代码：
``` typescript
<template>
  <div class="room-page">
    <!-- 参会者列表侧边栏 -->
    <aside class="sidebar">
      <div class="sidebar-header">
        <span>参会者 ({{ currentRoom.participantCount }})</span>
        <IconClose />
      </div>

      <!-- 参会者列表组件 -->
      <RoomParticipantList />
    </aside>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { IconClose } from '@tencentcloud/uikit-base-component-vue3';
import { 
  RoomView,
  RoomParticipantList,
  useRoomState,
  useRoomParticipantState 
} from 'tuikit-atomicx-vue3/room';

const { currentRoom } = useRoomState();
const { participantList } = useRoomParticipantState();
</script>

<style scope>
.room-page {
  width: 100vw;
  height: 100vh;
  min-width: 1150px;
  display: flex;
  flex-direction: row;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  position: relative;
  overflow: hidden;
}

.sidebar {
  position: absolute;
  top: 0;
  right: 0;
  width: 400px;
  height: 100%;
  box-sizing: border-box;
}

.sidebar-header {
  display: flex;
  height: 60px;
  justify-content: space-between;
  align-items: center;
  padding: 0px 20px;
}
</style>
```

> **说明：**
> 
> - `RoomParticipantList` 会自动占满父容器的高度和宽度，请确保其父容器具备明确的尺寸。
> - 使用 `RoomParticipantList` 组件请确保在 `App.vue` 中配置全局 `UIKitProvider`，具体请参考 [配置 App.vue](https://cloud.tencent.com/document/product/647/81962#ce98ee15-b0cb-43af-81da-70f51231430e)。

## 实现成员管理功能

如果您需要自定义成员列表 UI 或在特定业务中触发管理行为，请使用 [useRoomParticipantState](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#module-RoomParticipantState)。

### 步骤1：获取成员列表

通过 [getParticipantList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getParticipantList) 获取响应式的成员数据 [participantList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#participantList)。
``` typescript
import { useRoomState, useRoomParticipantState } from 'tuikit-atomicx-vue3/room';

const { currentRoom } = useRoomState();
const { participantList, participantListCursor, getParticipantList } = useRoomParticipantState();

// 在进房成功之后获取房间内用户列表
watch(() => currentRoom.value?.roomId, async () => {
 await getParticipantList();
})

// 当列表滚动到底部时，加载更多用户
const handleLoadMore = async () => {
  if (participantListCursor.value) {
    await getParticipantList({ cursor: participantListCursor.value });
  }
};
```

> **说明：**
> 

> `getParticipantList` 接口拉取成功的数据会自动维护在 `participantList` 中，UI 只需要渲染 `participantList` 的数据即可。
> 

### 步骤2：渲染参会者信息

开发者可以使用  [participantList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#participantList) 数据自定义渲染用户信息列表。
``` typescript
<template>
  <div class="participant-list">
    <div class="list-header">
      <h3>参会者 ({{ participantList.length }})</h3>
      <button @click="handleRefresh">
        <IconRefresh />
      </button>
    </div>
    <div class="list-content">
      <div 
        v-for="participant in participantList" 
        :key="participant.userId"
        class="participant-item"
      >
        <!-- 头像 -->
        <Avatar 
          :user-id="participant.userId" 
          :avatar-url="participant.avatarUrl" 
        />

        <!-- 用户信息 -->
        <div class="user-info">
          <div class="user-name">
            <span>{{ participant.userName }}</span>
            <span v-if="participant.userId === localParticipant.userId" class="badge">我</span>
            <span 
              v-if="participant.role === RoomParticipantRole.Owner" 
              class="role-badge owner"
            >
              房主
            </span>
            <span 
              v-else-if="participant.role === RoomParticipantRole.Admin" 
              class="role-badge admin"
            >
              管理员
            </span>
          </div>
        </div>

        <!-- 设备状态 -->
        <div class="device-status">
          <IconMicOn 
            size="20"
            v-if="participant.microphoneStatus === DeviceStatus.On" 
            class="icon-on"
          />
          <IconMicOff size="20" v-else class="icon-off" />
          <IconCameraOn
            size="20"
            v-if="participant.cameraStatus === DeviceStatus.On" 
            class="icon-on"
          />
          <IconCameraOff size="20" v-else class="icon-off" />
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue';
import { IconRefresh, IconMicOn, IconMicOff, IconCameraOn, IconCameraOff } from '@tencentcloud/uikit-base-component-vue3';
import { 
  useRoomParticipantState,
  Avatar,
  RoomParticipantRole,
  DeviceStatus
} from 'tuikit-atomicx-vue3/room';

const { 
  localParticipant, 
  participantList,
  getParticipantList,
  transferOwner
} = useRoomParticipantState();

const handleRefresh = async () => {
  await getParticipantList({ cursor: '' });
};
</script>

<style scoped>
.participant-list {  display: flex;  flex-direction: column;  width: 400px;  height: 100%;  background-color: white;}.list-header {  display: flex;  align-items: center;  justify-content: space-between;  padding: 16px;  border-bottom: 1px solid #e0e0e0;}.list-header h3 {  margin: 0;  font-size: 16px;  font-weight: 600;}.list-content {  flex: 1;  overflow-y: auto;  padding: 8px;}.participant-item {  display: flex;  align-items: center;  gap: 12px;  padding: 12px;  border-radius: 8px;  transition: background-color 0.2s;}.participant-item:hover {  background-color: #f5f5f5;}.participant-item.is-local {  background-color: #e3f2fd;}.user-info {  flex: 1;  min-width: 0;}.user-name {  display: flex;  align-items: center;  gap: 6px;  font-size: 14px;  font-weight: 500;}.badge {  padding: 2px 6px;  background-color: #4caf50;  color: white;  border-radius: 3px;  font-size: 12px;}.role-badge {  padding: 2px 6px;  border-radius: 3px;  font-size: 12px;}.role-badge.owner {  background-color: #ff9800;  color: white;}.role-badge.admin {  background-color: #2196f3;  color: white;}.device-status {  display: flex;  gap: 8px;}.icon-on {  color: #4caf50;}.icon-off {  color: #999;}.action-button {  padding: 4px 8px;  background: transparent;  border: none;  cursor: pointer;  border-radius: 4px;  color: #666;}.action-button:hover {  background-color: #f0f0f0;}
</style>
```

### 步骤3：设置用户自定义信息

开发者可以使用 [updateParticipantMetaData](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#updateParticipantMetaData) 接口设置用户的自定义数据，用于**实现职务**、**购买状态**等能力。更新之后 `metaData` 信息将被维护在 `participantList` 对应用户的响应式数据中。
``` typescript
<template>
  <div v-for="participant in participantList" :key="participant.userId">
    <span>{{ participant.userName }}</span>
    <span v-if="participant.metaData">
      {{ JSON.parse(participant.metaData).level }}
    </span>
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue';
import { IconRefresh, IconMicOn, IconMicOff, IconCameraOn, IconCameraOff } from '@tencentcloud/uikit-base-component-vue3';
import { 
  useRoomParticipantState,
} from 'tuikit-atomicx-vue3/room';

const { 
  updateParticipantMetaData,
} = useRoomParticipantState();

await updateParticipantMetaData({
 userId: '', // 指定用户 id
 metaData: JSON.stringify({ level: 1 }),   // 业务自定义信息
})
</script>
```

### 步骤4：管理成员身份

房主可以通过 [setAdmin](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setAdmin) 接口变更用户角色为管理员, 通过 [revokeAdmin](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#revokeAdmin) 方法撤销用户管理员身份。
``` typescript
const { setAdmin, revokeAdmin } = useRoomParticipantState();

// 将普通用户设置为管理员
await setAdmin({ userId });

// 将管理员设置为普通用户
await revokeAdmin({ userId });
```

### 步骤5：管理成员媒体设备

房主及管理员可以通过 [closeParticipantDevice](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#closeParticipantDevice) 接口远程控制其他成员的媒体设备，以维持会议环境的安静及有序。
``` typescript
import { useRoomParticipantState, DeviceType } from 'tuikit-atomicx-vue3/room';
const { closeParticipantDevice } = useRoomParticipantState();

// 强制关闭指定成员的麦克风
async function handleCloseUserMicrophone(userId: string) {
  await closeParticipantDevice({
    userId,
    deviceType: DeviceType.Microphone,
  });
}

// 强制关闭指定成员的摄像头
async function handleCloseUserCamera(userId: string) {
  await closeParticipantDevice({
    userId,
    deviceType: DeviceType.Camera,
  });
}
```

### 步骤6：开启全局状态管理

房主及管理员可通过 [disableAllDevices](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#disableAllDevices) 及 [disableAllMessages](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#disableAllMessages) 接口开启房间全局状态管理。

#### **禁用房间内所有普通用户的媒体设备**
``` typescript
import { useRoomParticipantState, DeviceType } from 'tuikit-atomicx-vue3/room';
const { closeParticipantDevice } = useRoomParticipantState();

// 强制关闭所有普通成员的麦克风
async function handleDisableAllMicrophone() {
  await disableAllDevices({
    deviceType: DeviceType.Microphone,
    disable: true,
  });
}

// 解除全员麦克风禁用
async function handleEnableAllMicrophone() {
  await disableAllDevices({
    deviceType: DeviceType.Microphone,
    disable: false,
  });
}

// 强制关闭所有普通成员的摄像头
async function handleDisableAllCamera() {
  await disableAllDevices({
    deviceType: DeviceType.Camera,
    disable: true,
  });
}

// 解除全员摄像头禁用
async function handleEnableAllCamera() {
  await disableAllDevices({
    deviceType: DeviceType.Camera,
    disable: false,
  });
}
```

#### **禁用房间内所有普通用户的会中聊天**
``` typescript
import { useRoomParticipantState, DeviceType } from 'tuikit-atomicx-vue3/room';
const { disableAllMessages } = useRoomParticipantState();

// 强制禁用所有普通成员的聊天能力
async function handleDisableAllMessage() {
  await disableAllMessages({
    disable: true,
  });
}
```

### **步骤7：**监控成员发言状态

通过 [speakingUsers](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#speakingUsers) 可以实时获取房间内正在说话的用户及其音量大小。
``` typescript
const { speakingUsers } = useRoomParticipantState();

// 判断用户是否正在说话
const isSpeaking = (userId: string) => speakingUsers.value.has(userId);
// 获取用户实时音量 (0-100)
const getVolume = (userId: string) => speakingUsers.value.get(userId) || 0;
```

### 步骤8：踢出房间内成员

房主及管理员可以通过 [kickParticipant](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#kickParticipant) 接口将用户移出房间。
``` typescript
const { kickParticipant } = useRoomParticipantState();

// 将用户踢出房间
await kickParticipant({ userId });
```

### 步骤9：邀请其他人加入房间

实际业务中，您可能需要向未进房的用户发起呼叫邀请。Atomicx 提供了完整的呼叫系统支持，请查看 会中呼叫。

## API 文档
| **State/Component** | **功能描述** | **API 文档** |
| --- | --- | --- |
| **useRoomParticipantState** | 包含房间内用户数据，用户管理接口。 | [API 文档](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#module-RoomParticipantState) |

## 开发建议

**权限校验：**在 UI 层建议通过 `participant.role` 判断当前用户的操作权限，对不具备管理权限的用户隐藏**踢人**或**禁言**按钮。
``` typescript
<script setup>
import { RoomParticipantRole } from 'tuikit-atomicx-vue3/room';

const { localParticipant } = useRoomParticipantState();

// 判断当前用户是否有管理权限
const hasAdminPermission = computed(() => {
  return localParticipant.value.role === RoomParticipantRole.Owner ||
         localParticipant.value.role === RoomParticipantRole.Admin;
});
</script>

// 在模板中使用
<template>
<button v-if="hasAdminPermission" @click="handleKick">踢出</button>
<template>
```
