> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

本篇文档将详细指导您如何使用 Atomicx 的 [useRoomState](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#module-RoomState) 管理房间的完整生命周期，包括创建、加入、离开以及结束房间，以及处理关键的房间状态通知。以下时序图演示了房间从创建到销毁的主要流程。

## 功能介绍

[useRoomState](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#module-RoomState) 是 Atomicx 方案中负责房间管理的核心 Hook。它封装了复杂的底层信令流程，开发者可以通过简单的响应式数据和方法调用来驱动房间状态。
- **创建与加入：**通过 [createAndJoinRoom](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#createAndJoinRoom) 方法创建并加入房间，或通过 [joinRoom](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#joinRoom) 方法加入已有房间。

- **状态实时同步：**`useRoomState`Hook 内部维护 [currentRoom](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#currentRoom) 响应式数据，自动同步房间名称、模式及成员数等信息。

- **权限分明的退出机制：**针对不同角色提供了清晰的操作边界。普通成员可以使用 [leaveRoom](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#leaveRoom) 退出；而房主（主持人）则拥有 [endRoom](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#endRoom) 权限，可以一键结束房间并销毁房间资源。

## **前提条件**

用户已经通过 [useLoginState](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#module-LoginState) 完成登录鉴权，请参考 接入概览。

## 实现房间管理

### 步骤1：导入 useRoomState
``` typescript
import { useRoomState } from 'tuikit-atomicx-vue3/room';

const { 
  createAndJoinRoom, 
  joinRoom, 
  leaveRoom, 
  endRoom,
  currentRoom 
} = useRoomState();
```

### 步骤2：创建房间

创建房间（房主）：使用 [createAndJoinRoom](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#createAndJoinRoom)，调用成功后该用户将自动获得房主权限。

> **注意：**
> 

> 创建房间时指定的 roomId 建议由业务后台生成并下发，以确保房间 Id 在全局应用中的唯一性与稳定性。
> 

- **示例一：用户创建房间**

   ``` typescript
   import { useRoomState } from 'tuikit-atomicx-vue3/room';
   const { createAndJoinRoom } = useRoomState();
   
   await createAndJoinRoom({
     roomId: 'YOUR_ROOM_ID',    // 指定房间 Id，由业务后台生成
   })
   ```
- **示例二：用户创建房间并指定房间名称**

   ``` typescript
   import { useRoomState } from 'tuikit-atomicx-vue3/room';
   const { createAndJoinRoom } = useRoomState();
   
   await createAndJoinRoom({
     roomId: 'YOUR_ROOM_ID',    // 指定房间 Id，由业务后台生成
     options: {
       roomName: '我的临时房间'
     }
   })
   ```
- **示例三：用户创建密码房间**

   ``` typescript
   import { useRoomState } from 'tuikit-atomicx-vue3/room';
   const { createAndJoinRoom } = useRoomState();
   
   await createAndJoinRoom({
     roomId: 'YOUR_ROOM_ID',    // 指定房间 Id，由业务后台生成
     options: {
       roomName: '我的临时房间',
       password: '123456',
     }
   })
   ```   

   > **说明：**
   > 

   > 创建者在调用 [createAndJoinRoom](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#createAndJoinRoom) 时会自动加入房间，无需输入密码。
   > 

- **示例四：用户创建房间并配置成员管理信息**

   ``` typescript
   import { useRoomState } from 'tuikit-atomicx-vue3/room';
   const { createAndJoinRoom } = useRoomState();
   
   await createAndJoinRoom({
     roomId: 'YOUR_ROOM_ID',    // 指定房间 Id，由业务后台生成
     options: {
       roomName: '我的临时房间',
       password: '123456',
       isAllMicrophoneDisabled: true,   // 开启全员静音
       isAllCameraDisabled: true,       // 开启全员静画
       isAllScreenShareDisabled: true,  // 开启全员禁止屏幕共享
       isAllMessageDisabled: true,      // 开启全员禁止发会中消息
     }
   })
   ```   

   > **说明：**
   > 

   > 成员管理配置信息仅对普通成员生效，房主和管理员不受限制。如需在房间创建后修改成员管理配置或单独管理成员权限，请参考 成员管理。
   > 

### 步骤3：用户加入已有房间

登录用户可以调用 [joinRoom](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#joinRoom) 加入已有房间。Atomicx 仅支持用户同时加入一个房间。
- **示例一：用户加入房间**

   ``` typescript
   import { useRoomState } from 'tuikit-atomicx-vue3/room';
   const { joinRoom } = useRoomState();
   
   await joinRoom({
     roomId: 'YOUR_ROOM_ID',    // 指定房间 Id，由业务后台生成
   })
   ```
- **示例二：用户加入密码房间**

   ``` typescript
   import { useRoomState } from 'tuikit-atomicx-vue3/room';
   const { joinRoom } = useRoomState();
   
   await joinRoom({
     roomId: 'YOUR_ROOM_ID',    // 指定房间 Id，由业务后台生成
     password: '123456',
   })
   ```

### 步骤4：更新房间信息

房主可以在创建房间后使用 [updateRoomInfo](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#updateRoomInfo) 更新房间名称和密码。
``` typescript
import { useRoomState } from 'tuikit-atomicx-vue3/room';
const { updateRoomInfo } = useRoomState();

await updateRoomInfo({
  roomId: 'YOUR_ROOM_ID',    // 指定房间 Id，由业务后台生成
  options: {
     roomName: '新的房间名称',
     password: '234567',
  },
})
```

> **说明：**
> 

> 房主必须在房间内才能调用 [updateRoomInfo](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#updateRoomInfo)。如果房主已离开房间，需要重新加入后才能更新房间信息。
> 

### 步骤5：离开房间

房主及普通用户均可调用 [leaveRoom](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#leaveRoom) 接口离开房间，使用该接口的前提是用户已经通过 [createAndJoinRoom](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#createAndJoinRoom) 或者 [joinRoom](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#joinRoom) 接口加入房间。
``` typescript
import { useRoomState } from 'tuikit-atomicx-vue3/room';
const { leaveRoom } = useRoomState();

await leaveRoom();
```

### 步骤6：销毁房间

仅房主可调用 [endRoom](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#endRoom) 接口销毁房间，使用该接口的前提是用户已经通过 [createAndJoinRoom](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#createAndJoinRoom) 创建房间或者已经获取房主身份。
``` typescript
import { useRoomState } from 'tuikit-atomicx-vue3/room';
const { endRoom } = useRoomState();

await endRoom();
```

> **说明：**
> 
> - 如果房主离开房间但未调用 [endRoom](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#endRoom)，房间将继续存在，直到满足自动回收条件（连续 6 小时无用户）。
> - 房主可以通过 [transferOwner](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#transferOwner) 接口将房主身份转移给其他用户。

### 步骤7：异常退出处理

#### 处理房间被销毁事件

普通用户可通过监听 `RoomEvent.onRoomEnded` 事件处理房间被销毁的业务交互。
``` typescript
import { useRoomState, RoomEvent } from 'tuikit-atomicx-vue3/room';
import { TUIMessageBox } from '@tencentcloud/uikit-base-component-vue3';
const { subscribeEvent, unsubscribeEvent } = useRoomState();

function onRoomEnded() {
  TUIMessageBox.alert({
    title: '通知',
    content: '房主已解散房间',
  });
}

// 在组件加载时监听 RoomEvent
subscribeEvent(RoomEvent.onRoomEnded, onRoomEnded);
// 在组件销毁时取消监听 RoomEvent
unsubscribeEvent(RoomEvent.onRoomEnded, onRoomEnded);
```

#### 处理用户被踢退房事件

普通用户可通过监听 `RoomParticipantEvent.onKickedFromRoom` 事件处理用户被踢出房间的业务交互。
``` typescript
import { useRoomParticipantState, RoomParticipantEvent, KickedOutOfRoomReason } from 'tuikit-atomicx-vue3/room';
import { TUIMessageBox } from '@tencentcloud/uikit-base-component-vue3';

const { subscribeEvent, unsubscribeEvent } = useRoomParticipantState();

function onKickedFromRoom({ reason }: { reason: KickedOutOfRoomReason; message: string }) {
    let notice = '';
    switch (reason) {
      case KickedOutOfRoomReason.KickedByAdmin:
        notice = '您已被房主移出房间';
        break;
      case KickedOutOfRoomReason.ReplacedByAnotherDevice:
        notice = '您的账号已在其他设备登录';
        break;
      case KickedOutOfRoomReason.KickedByServer:
        notice = '您已被服务器移出房间';
        break;
      case KickedOutOfRoomReason.ConnectionTimeout:
        notice = '网络连接超时，正在退出房间';
        break;
      case KickedOutOfRoomReason.InvalidStatusOnReconnect:
        notice = '房间已解散或您在离线期间已被移出';
        break;
      case KickedOutOfRoomReason.RoomLimitExceeded:
        notice = '房间人数已达上限，无法加入';
        break;
      default:
        notice = '您已被移出房间';
        break;
    }
    TUIMessageBox.alert({
      title: '通知',
      content: notice,
    });
  }

// 在组件加载时监听 RoomParticipantEvent
subscribeEvent(RoomParticipantEvent.onKickedFromRoom, onKickedFromRoom);
// 在组件销毁时取消监听 RoomParticipantEvent
unsubscribeEvent(RoomParticipantEvent.onKickedFromRoom, onKickedFromRoom);
```

## 进阶实现

当前文档介绍的是快速创建并立即加入一个房间，适用于即时多人音视频互通场景。

但在现实商业场景中，我们往往需要提前规划：设置房间的主题、预定特定的开始与结束时间、并邀请参与者。参与者可以在多人音视频房间开始前收到提醒，并准时接入。

Atomicx 提供了完整的预约房间能力，包括：
- **预定房间：**提前设定多人房间时间与参与人名单。

- **预约列表**：查看并管理自己名下的所有待开始的多人房间。

- **入会提醒：**支持开始前的自动提醒逻辑。

   如果您需要实现上述更复杂的商业多人音视频房间管理逻辑，请参考：预定房间。

## 常见问题

### 房间内已经没有用户但房间未被解散，房间是否会一直存在？

房间内连续 6 小时无用户进入时，后台将尝试回收房间。

### 房间内已经没有用户但房间未被解散，是否会产生费用消耗？

没有用户但是未被解散的房间仅占用套餐群组数，不产生分钟数消耗和额外费用消耗。

### 一个用户可以同时加入多个房间吗？

Atomicx 提供的 `useRoomState` 为单例接口，仅支持用户同时加入一个房间。若您需要支持一个用户同时加入多个房间，欢迎 [联系我们](https://cloud.tencent.com/document/product/647/19906) 提交反馈。

### 最多支持多少人同时加入房间？

房间内用户数量上限和您的套餐包相关，具体请查看 [TUIRoomKit 套餐包说明](https://cloud.tencent.com/document/product/647/104842#function)。
