> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

**AtomicXCore** 提供了 [CoGuestStore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/cogueststore) 和 [LiveSeatStore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/liveseatstore) 模块，用于管理观众连麦的完整业务流程。您无需关心复杂的状态同步和信令交互，只需调用几个简单的方法，即可为您的直播添加强大的观众与主播音视频互动功能。本文档将指导您如何使用 `CoGuestStore `和 `LiveSeatStore`在 iOS 应用中快速实现语音连麦功能。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032603567/02ca5724b64111f0a5e052540099c741.png)


## 核心场景

`CoGuestStore`和`LiveSeatStore`支持以下几个主流的场景：
- **观众申请上麦**：观众主动发起连麦请求，主播在收到请求后进行同意或拒绝。

- **主播邀请上麦**：主播可以主动向直播间内的任意一位观众发起连麦邀请。

- **主播管理麦位**：主播可以对麦位上的用户进行踢人、闭麦、锁麦等操作。


## 实现步骤

### 步骤1：组件集成

请参考 [快速接入](https://write.woa.com/document/192834898445422592) 集成 **AtomicXCore**。

### 步骤2：实现观众申请上麦

#### 观众端实现

作为观众，您的核心任务是**发起申请、接收结果**和**主动下麦**。
1. **发起连麦申请**


   当用户点击界面上的“申请连麦”按钮时，调用 `applyForSeat` 方法。

   ``` swift
   import AtomicXCore
   
   let liveId = "房间ID"
   var guestStore: CoGuestStore {
       CoGuestStore.create(liveID: liveID)
   }
   
   // 用户点击“申请连麦”
   func requestToConnect() {
       // timeout: 请求超时时间，例如 30 秒
       guestStore.applyForSeat(timeout: 30.0, extraInfo: nil) { result in
         switch result {
         case .success():
             print("连麦申请已发送，等待主播处理...")
         case .failure(let error):
             print("申请发送失败: \(error.message)")
         }
       }
   }
   ```
2. **监听主播的处理结果**


   通过订阅 `guestEventPublisher`，您可以接收到主播的处理结果。

   ``` swift
   // 在您的视图控制器初始化时订阅事件
   func subscribeGuestEvents() {
       guestStore.guestEventPublisher
         .sink { [weak self] event in
             if case let .onGuestApplicationResponded(isAccept, hostUser) = event {
                 if isAccept {
                     print("主播 \(hostUser.userName) 同意了你的申请，准备上麦")
                     // 1. 打开麦克风 
                     DeviceStore.shared.openLocalMicrophone(completion: nil)
                     // 2. 在此更新 UI，例如关闭申请按钮，显示连麦中的状态
                 } else {
                     print("主播 \(hostUser.userName) 拒绝了你的申请")
                     // 弹窗提示用户申请被拒绝
                 }
             }
         }
         .store(in: &cancellables) // 管理订阅生命周期
   }
   ```
3. **主动下麦**


   当连麦观众想结束互动时，调用 `disConnect` 方法即可返回普通观众状态。

   ``` swift
   // 用户点击“下麦”按钮
   func leaveSeat() {
       guestStore.disConnect { result in
         switch result {
         case .success():
             print("已成功下麦")
         case .failure(let error):
             print("下麦失败: \(error.message)")
         }
       }
   }
   ```
4. **(可选) 取消申请**


   如果观众在主播处理前想撤回申请，可以调用 `cancelApplication`。

   ``` swift
   // 用户在等待时，点击“取消申请”
   func cancelRequest() {
       guestStore.cancelApplication { result in
         switch result {
         case .success():
             print("申请已取消")
         case .failure(let error):
             print("申请取消失败: \(error.message)")
         }
       }
   }
   ```

#### 主播端实现

作为主播，您的核心任务是**接收申请、展示申请列表**和**处理申请**。
1. **监听新的连麦申请**


   通过订阅 `hostEventPublisher`，您可以在有新观众申请时立即收到通知，并给出提示。

   ``` swift
   import AtomicXCore
   
   let liveId = "房间ID"
   var guestStore: CoGuestStore {
       CoGuestStore.create(liveID: liveID)
   }
   
   // 订阅主播事件
   guestStore.hostEventPublisher
       .sink { [weak self] event in
           if case let .onGuestApplicationReceived(guestUser) = event {
               print("收到观众 \(guestUser.userName) 的连麦申请")
               // 在此更新 UI，例如在“申请列表”按钮上显示红点
           }
       }
       .store(in: &cancellables)
   ```
2. **展示申请列表**


   `CoGuestStore` 的 state 会实时维护当前的申请者列表，您可以订阅它来刷新您的 UI。

   ``` swift
   // 订阅状态变更
   guestStore.state
       .subscribe(StatePublisherSelector(keyPath: \CoGuestState.applicants)) // 只关心申请者列表的变化
       .removeDuplicates()
       .sink { applicants in
           print("当前申请人数: \(applicants.count)")
           // 在此刷新您的“申请者列表”UI
           // self.applicantListView.update(with: applicants)
       }
       .store(in: &cancellables)
   ```
3. **处理连麦申请**


   当您在列表中选择一位观众并点击“同意”或“拒绝”时，调用相应的方法。

   ``` perl
   // 主播点击“同意”按钮，传入申请者的 userID
   func accept(userId: String) {
       guestStore.acceptApplication(userID: userId) { result in
           if case .success = result {
               print("已同意 \(userId) 的申请，对方正在上麦")
           }
       }
   }
   
   // 主播点击“拒绝”按钮
   func reject(userId: String) {
       guestStore.rejectApplication(userID: userId) { result in
           if case .success = result {
               print("已拒绝 \(userId) 的申请")
           }
       }
   }
   ```

### 步骤3：实现主播邀请上麦

#### 主播端实现
1. **向观众发起邀请**


   当主播在观众列表中选择某人并点击“邀请连麦”时，调用 `inviteToSeat` 方法。

   ``` swift
    // 主播选择观众并发起邀请
   func invite(userId: String) {
       // timeout: 邀请超时时间
       guestStore.inviteToSeat(userID: userId, timeout: 30.0, extraInfo: nil) { result in
           if case .success = result {
               print("已向 \(userId) 发出邀请，等待对方回应...")
           }
       }
   }
   ```
2. **监听观众的回应**


   通过 `hostEventPublisher` 监听 `onHostInvitationResponded` 事件。

   ``` swift
   // 在 hostEventPublisher 的订阅中添加
   if case let .onHostInvitationResponded(isAccept, guestUser) = event {
       if isAccept {
           print("观众 \(guestUser.userName) 接受了你的邀请")
       } else {
           print("观众 \(guestUser.userName) 拒绝了你的邀请")
       }
   }
   ```

#### 观众端实现
1. **接收主播的邀请**


   通过 `guestEventPublisher` 监听 `onHostInvitationReceived` 事件。

   ``` swift
   // 在 guestEventPublisher 的订阅中添加
   if case let .onHostInvitationReceived(hostUser) = event {
       print("收到主播 \(hostUser.userName) 的连麦邀请")
       // 在此弹出一个对话框，让用户选择“接受”或“拒绝”
       // self.showInvitationDialog(from: hostUser)
   }
   ```
2. **响应邀请**


   当用户在弹出的对话框中做出选择后，调用相应的方法。

   ``` swift
   let inviterId = "发起邀请的主播ID" // 从 onHostInvitationReceived 事件中获取
   
   // 用户点击“接受”
   func accept() {
       guestStore.acceptInvitation(inviterID: inviterId) { result in
           if case .success = result {
               // 2. 打开麦克风
               DeviceStore.shared.openLocalMicrophone(completion: nil)
           }
       }
   }
   
   // 用户点击“拒绝”
   func reject() {
       guestStore.rejectInvitation(inviterID: inviterId) { result in
           // ...
       }
   }
   ```

## 功能进阶

当用户上麦后，主播可能需要对麦位进行管理。以下功能主要由 `LiveSeatStore` 提供，它可以与 `CoGuestStore` 协同工作。

### 麦上用户自行开/关麦

麦上用户（包括主播自己）可以通过 `LiveSeatStore` 提供的接口来控制自己的麦克风静音状态。

#### 实现方式：
1. **静音：**调用 `muteMicrophone()` 方法。这是一个无回调的单向请求。

2. **解除静音**：调用 `unmuteMicrophone(completion:)` 方法。


#### 示例代码：
``` swift
let seatStore = LiveSeatStore.create(liveID: liveId)

seatStore.muteMicrophone() //静音

seatStore.unmuteMicrophone(completion: nil) //解除静音
```

#### unmuteMicrophone 接口参数：
<table>
<tr>
<td rowspan="1" colSpan="1" >**参数**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`completion`</td>

<td rowspan="1" colSpan="1" >`CompletionClosure?`</td>

<td rowspan="1" colSpan="1" >操作完成后的回调。</td>
</tr>
</table>


### 主播远程控制麦上用户开麦或关麦

主播可以对其他麦上用户进行“强制静音”或“邀请开麦”的操作。

#### 实现方式：
1. **强制静音（锁定）**：主播调用 `closeRemoteMicrophone` 会强制关闭对方的麦克风，并锁定对方的麦克风权限，被静音的用户会收到 `liveSeatEventPublisher` 中的 `onLocalMicrophoneClosedByAdmin` 事件，此时其本地的“打开麦克风”按钮应变为不可点击状态。

2. **邀请开麦（解锁）**：主播调用 `openRemoteMicrophone` 并非强制打开对方麦克风，而是解除对方的“锁定状态”，允许对方自行开麦。此时，被操作的用户会收到 `onLocalMicrophoneOpenedByAdmin` 事件，其本地的“打开麦克风”按钮应恢复为可点击状态，但用户仍处于静音中。

3. **用户自行开麦**：用户在收到“解除锁定”的通知后，必须主动调用 `LiveSeatStore` 的 `unmuteMicrophone()`方法解除静音，才能让房间内其他人听到自己的声音。


#### 示例代码：

##### 主播端：
``` swift
let targetUserId = "userD"

// 1. 强制静音 userD 并锁定
seatStore.closeRemoteMicrophone(userID: targetUserId) { result in
    if case .success = result {
        print("已将 \(targetUserId) 静音并锁定")
    }
}

// 2. 解锁 userD 的麦克风权限（此时 userD 依然是静音状态）
seatStore.openRemoteMicrophone(userID: targetUserId, policy: .unlockOnly) { result in
     if case .success = result {
        print("已邀请 \(targetUserId) 打开麦克风（已解锁）")
    }
}
```

##### 观众端：
``` swift
// userD监听主播的操作
seatStore.liveSeatEventPublisher
    .sink { event in
        switch event {
        case .onLocalMicrophoneClosedByAdmin:
            print("被主播静音了")
            // self.muteButton.isEnabled = false
        case .onLocalMicrophoneOpenedByAdmin(policy: _):
             print("主播已解除静音锁定")
            // self.muteButton.isEnabled = true
            // self.muteButton.setTitle("打开麦克风")
        default:
            break
        }
    }
    .store(in: &cancellables)
```

#### closeRemoteMicrophone 接口参数：
<table>
<tr>
<td rowspan="1" colSpan="1" >**参数**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`userID`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >被操作的用户`userID`。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`completion`</td>

<td rowspan="1" colSpan="1" >`CompletionClosure?`</td>

<td rowspan="1" colSpan="1" >请求完成后的回调。</td>
</tr>
</table>


#### openRemoteMicrophone 接口参数：
<table>
<tr>
<td rowspan="1" colSpan="1" >**参数**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`userID`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >被操作的用户`userID`。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`completion`</td>

<td rowspan="1" colSpan="1" >`CompletionClosure?`</td>

<td rowspan="1" colSpan="1" >请求完成后的回调。</td>
</tr>
</table>


### 主播将麦上用户踢下麦位

#### 实现方式：
1. **踢人下麦**：主播可以调用 `kickUserOutOfSeat` 方法，强制将指定用户踢下麦位。

2. **监听事件通知**：被踢下麦的用户会收到 `CoGuestStore.guestEventPublisher `中的 `onKickedOffSeat` 事件通知。


#### 示例代码：
``` swift
// 假设要踢走 "userB"
let targetUserId = "userB"
seatStore.kickUserOutOfSeat(userID: targetUserId) { result in
    switch result {
    case .success:
        print("已将 \(targetUserId) 踢下麦位")
    case .failure(let error):
        print("踢人失败: \(error.message)")
    }
}

// "userB"收到被踢下麦事件
guestStore
    .guestEventPublisher
    .receive(on: RunLoop.main)
    .sink { [weak self] event in
        guard let self = self else { return }
        switch event {
        case .onKickedOffSeat(seatIndex: _, hostUser: _):
            // 弹toast提示
        default:
            break
        }
    }
    .store(in: &cancellables)

```

#### kickUserOutOfSeat 接口参数：
<table>
<tr>
<td rowspan="1" colSpan="1" >**参数**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`userID`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >被踢下麦的用户`userID`。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`completion`</td>

<td rowspan="1" colSpan="1" >`CompletionClosure?`</td>

<td rowspan="1" colSpan="1" >请求完成后的回调。</td>
</tr>
</table>


### 主播锁定和解锁麦位

主播可以锁定或解锁某个麦位。

#### 实现方式：
1. **锁定麦位**：主播可调用 `lockSeat` 方法锁定指定索引的麦位，麦位被锁定后，观众无法通过 `applyForSeat` 或`takeSeat` 占用该麦位。

2. **解锁麦位**：调用 `unlockSeat` 可以解锁麦位，解锁后该麦位可以再次被占用。


#### 示例代码：
``` swift
// 锁定2号麦位
seatStore.lockSeat(seatIndex: 2) { result in
    if case .success = result {
        print("2号麦位已锁定")
    }
}

// 解锁2号麦位
seatStore.unlockSeat(seatIndex: 2) { result in
    if case .success = result {
        print("2号麦位已解锁")
    }
}
```

#### lockSeat 接口参数：
<table>
<tr>
<td rowspan="1" colSpan="1" >**参数**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`seatIndex`</td>

<td rowspan="1" colSpan="1" >`Int`</td>

<td rowspan="1" colSpan="1" >需要锁定的麦位索引。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`completion`</td>

<td rowspan="1" colSpan="1" >`CompletionClosure?`</td>

<td rowspan="1" colSpan="1" >请求完成后的回调。</td>
</tr>
</table>


#### unlockSeat 接口参数：
<table>
<tr>
<td rowspan="1" colSpan="1" >**参数**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`seatIndex`</td>

<td rowspan="1" colSpan="1" >`Int`</td>

<td rowspan="1" colSpan="1" >需要解锁的麦位索引。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`completion`</td>

<td rowspan="1" colSpan="1" >`CompletionClosure?`</td>

<td rowspan="1" colSpan="1" >请求完成后的回调。</td>
</tr>
</table>


### 移动麦位

主播和普通上麦用户可以调用`moveUserToSeat(userID:targetIndex:policy:completion:)`移动麦位。

#### 实现方式：
1. **主播移动麦位**：主播可以调用此接口将任意用户移动到指定麦位。此时 `userID` 传入目标用户的 ID，`targetIndex`是目标麦位索引，`policy` 参数来指定如果目标麦位有人时的移动策略，详细参见 [接口参数](https://write.woa.com/#227e92a5-7552-41ae-b57c-2dab5b7de234) 说明。

2. **普通上麦用户移动自己麦位**：普通上麦用户也可以调用此接口来移动自己。此时 `userID` 必须传入用户自己的 ID，`targetIndex` 传入想去的新麦位索引，此时`policy` 参数无效，如果目标麦位有人时会报错并停止移动。


#### 示例代码：
``` swift
seatStore.moveUserToSeat(userID: "userC", 
                         targetIndex: newSeatIndex, 
                         policy: .abortWhenOccupied) { result in
    if case .success = result {
        print("已成功移动到 \(newSeatIndex) 号麦位")
    } else {
        print("换座失败，可能位置有人了")
    }
}
```

#### moveUserToSeat 接口参数：
<table>
<tr>
<td rowspan="1" colSpan="1" >**参数**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`userID`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >需要移麦的用户`userID`。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`targetIndex`</td>

<td rowspan="1" colSpan="1" >`Int`</td>

<td rowspan="1" colSpan="1" >目标麦位索引。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`policy`</td>

<td rowspan="1" colSpan="1" >`MoveSeatPolicy?`</td>

<td rowspan="1" colSpan="1" >目标麦位有人时的移动策略枚举：<br>- `abortWhenOccupied`：目标麦位有人时放弃移动（默认策略）​​<br>- `forceReplace`：强制替换目标麦位上的用户​​，被替换的用户将会被踢下麦<br>- `swapPosition`：与目标麦位用户交换位置​​。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`completion`</td>

<td rowspan="1" colSpan="1" >`CompletionClosure?`</td>

<td rowspan="1" colSpan="1" >请求完成后的回调。</td>
</tr>
</table>


## API 文档

关于 [CoGuestStore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/cogueststore) 和 [LiveSeatStore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/liveseatstore) 及其相关类的所有公开接口、属性和方法的详细信息，请参阅 [AtomicXCore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore) 框架的官方 API 文档。本指南使用到的相关 Store 如下：
<table>
<tr>
<td rowspan="1" colSpan="1" >**Store/Component**</td>

<td rowspan="1" colSpan="1" >**功能描述**</td>

<td rowspan="1" colSpan="1" >**API 文档**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >CoGuestStore</td>

<td rowspan="1" colSpan="1" >观众连麦管理：连麦申请 / 邀请 / 同意 / 拒绝，连麦成员权限控制（麦克风 / 摄像头），状态同步。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/cogueststore)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >LiveSeatStore</td>

<td rowspan="1" colSpan="1" >麦位管理：静音/解除静音，锁定/解锁麦位，踢人下麦、远程控制麦上用户麦克风，麦列表状态监听</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/liveseatstore)</td>
</tr>
</table>


## 常见问题

### 语音房连麦和视频直播连麦的实现有何不同？

两者的主要区别在于业务形态与 UI 展现：
- 视频直播：核心是视频画面。您会使用 `LiveCoreView` 作为核心组件来渲染主播和连麦观众的视频流。UI 的重点是处理视频画面的布局、大小，以及通过 `VideoViewDelegate` 在视频流上添加挂件（如昵称、占位图）。您可以同时打开摄像头，麦克风。

- 语音房（语聊房）：核心是麦位网格。您不会使用 `LiveCoreView`，而是会基于 `LiveSeatStore` 的 `state`（特别是 `seatList`）来构建一个网格 UI（例如 `UICollectionView`）。UI 的重点是实时显示每个麦位 `SeatInfo` 的状态：是否有人、是否静音、是否被锁定 ，以及是否正在说话。您只需要打开麦克风。


### 如何在 UI 上实时刷新麦位信息（如是否有人、是否静音）？

您应该订阅 `LiveSeatState` 中的 `seatList` 属性，它是一个`[SeatInfo]` 数组类型的响应式数据，每当数组变化时都会通知您重新渲染麦位列表。遍历此数组，您可以：
- 通过 `seatInfo.userInfo` 来获取麦位上的用户信息。

- 通过 `seatInfo.isLocked `判断麦位是否被锁定。

- 通过 `seatInfo.userInfo.microphoneStatus` 判断麦上用户的麦克风状态。


### LiveSeatStore 和 DeviceStore 都有麦克风接口，它们有何区别？

这是一个非常重要的问题。`DeviceStore` 管理的是物理设备，而 `LiveSeatStore` 管理的是麦位业务（即音频流）。

`DeviceStore`：
- `openLocalMicrophone`：向系统请求权限并启动麦克风设备进行音频采集。这是一个“重”操作。

- `closeLocalMicrophone`：停止音频采集并释放麦克风设备。


   `LiveSeatStore`：

- `muteMicrophone`：静音。停止向远端发送本地的音频流，但麦克风设备本身仍在运行。

- `unmuteMicrophone`：解除静音。恢复向远端发送音频流。


   推荐的工作流程：您应该遵循“设备只开一次，麦上只用静音切换”的原则

1. **上麦时**：当观众成功上麦，调用一次 `openLocalMicrophone`来启动设备。

2. **在麦上时**：用户在麦位上所有的“开麦”和“闭麦”操作，都应该调用 `unmuteMicrophone`和 `muteMicrophone`来控制上行音频流的通断。

3. **下麦时**：当用户下麦（例如调用 `disconnect`），调用`closeLocalMicrophone`来释放设备。


