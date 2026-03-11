> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

`AtomicXCore` 提供了 `CoHostStore` 和 `BattleStore` 两个模块，分别用于处理**跨房连线**和 **PK 对战**。本文将指导您如何组合使用这两个工具，完成语聊房场景下的连线和 PK 功能的开发。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100038646063/9a1b8a61cc3111f084a45254005ef0f7.jpeg)


## 核心概念

在开始集成之前，我们先通过下表了解一下跨房连线与 PK 相关的几个核心概念。
<table>
<tr>
<td rowspan="1" colSpan="1" >**核心概念**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**核心职责与描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**CoHostStore**</td>

<td rowspan="1" colSpan="1" >抽象类</td>

<td rowspan="1" colSpan="1" >管理主播间的连线生命周期，提供连线功能 API（requestHostConnection、acceptHostConnection）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**BattleStore**</td>

<td rowspan="1" colSpan="1" >抽象类</td>

<td rowspan="1" colSpan="1" >管理跨房 PK 对战的信令与数据，包括 PK 状态。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**LiveListStore**</td>

<td rowspan="1" colSpan="1" >单例</td>

<td rowspan="1" colSpan="1" >提供直播房间列表的拉取功能 (`fetchLiveList`)，用于获取可连线的其他房间信息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**LiveSeatStore**</td>

<td rowspan="1" colSpan="1" >抽象类</td>

<td rowspan="1" colSpan="1" >管理房间内所有麦位状态（包括连线状态下的跨房间麦位），用于监听用户上下麦、麦克风等状态。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**CoHostLayoutTemplate**</td>

<td rowspan="1" colSpan="1" >枚举</td>

<td rowspan="1" colSpan="1" >连线时，用于指定房间麦位布局模板，例如 `HOST_STATIC_VOICE_6V6`。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**BattleConfig**</td>

<td rowspan="1" colSpan="1" >数据模型</td>

<td rowspan="1" colSpan="1" >配置 PK 的详细信息，例如 PK 时长 (`duration`) 和是否需要二次响应 (`needResponse`)。</td>
</tr>
</table>


## 前提条件

请参考 [快速接入](https://write.woa.com/document/192834878686547968) 集成 **AtomicXCore SDK**，并完成 **主播开播** 和 **观众观看** 的功能实现。

## 主播发起一场连线

### 步骤1：查看正在开播中的主播列表

主播需要拉取当前的直播间列表，从中选择一个目标房间的主播发起连线或 PK。

**实现方式： **调用 `LiveListStore.shared().fetchLiveList`。

> **注意：**
> 
> - 如果接口返回的列表中没有找到您想要的直播间，您需要检查开播时设置的 `TUILiveInfo` 的 `isPublicVisible` 字段是否为 `true`；
> - 该接口支持分页继续拉取，您可以使用接口 `onSuccess` 回调中 `cursor` 作为下一次续拉的游标，如果返回的 `cursor` 为空，则表示直播间列表已全部拉取完；
> - 为了性能考虑，建议您将pageCount设置为 20。

``` java
import io.trtc.tuikit.atomicxcore.api.live.LiveListStore
import io.trtc.tuikit.atomicxcore.api.CompletionHandler

fun fetchLiveListForCoHost() {
    val cursor = "" // 首次拉取，游标为空
    val pageCount = 20  // 每次拉取 20 条数据

    LiveListStore.shared().fetchLiveList(cursor, pageCount, object : CompletionHandler {
        override fun onSuccess() {
            println("直播间列表拉取成功")
            // 拉取到的直播列表会更新到 LiveListStore.liveState.liveList 中，在拉取成功之后，更新连线邀请面板推荐的用户。
            // inviteAdapter.submitList(LiveListStore.liveState.liveList))
        }
        override fun onFailure(code: Int, desc: String) {
            println("邀请发送失败: $code")
        }
    })
}
```

### 步骤2：主播发起连线邀请

您可以在主播选中指定的主播连线时，调用 `CoHostStore` 的 `requestHostConnection` 接口发起连线邀请。

> **说明：**
> 
> 1. AtomicXCore最大支持 **9** 个房间互相连线，每个房间支持 **50 **路用户。
> 2. 该接口支持批量发起邀请，您可以按需使用；单个直播间是否邀请成功，您需要监听 `onSuccess` 回调并解析 `code` 枚举值是否为 `0`；
> 3. 该接口支持扩展字段，邀请发送成功后，该字段会随着 `CoHostListener` 的 `onCoHostRequestReceived` 回调通知给对端主播，您可以在这个字段中携带 “**是否立即开始 PK 对战**” 等信息，来实现自己的特殊业务。

``` java
import io.trtc.tuikit.atomicxcore.api.live.CoHostLayoutTemplate
import io.trtc.tuikit.atomicxcore.api.CompletionHandler

// 从 LiveListStore 中获取的目标房间 ID
val targetHostLiveID = "target_host_room_id" 
// 使用 6v6 语聊房静态布局为例
val layoutTemplate = CoHostLayoutTemplate.HOST_STATIC_VOICE_6V6 
val timeout = 10 // 邀请超时时间（秒）
val extraInfo = "" // 额外的业务信息，用于“直连 PK”时携带标识

coHostStore.requestHostConnection(
    targetHostLiveID,
    layoutTemplate,
    timeout,
    extraInfo,
    object : CompletionHandler {
        override fun onSuccess() {
            println("连线请求发送成功，等待对方处理...")
        }
        override fun onFailure(code: Int, desc: String) {
            println("邀请发送失败: $desc")
        }
    }
)
```

### 步骤3：对端主播收到连线邀请

当跨房连线邀请发送成功后，对端主播会收到 `CoHostListener` 的 `onCoHostRequestReceived` 回调，对端主播可以监听这个回调并在 UI 上提醒 “主播邀请您参与连线互动”。
``` java
private val coHostListener = object : CoHostListener() {
        override fun onCoHostRequestReceived(
            inviter: SeatUserInfo, extensionInfo: String
        ){
            // 您可以在这里 UI 弹框提醒用户
        }
    }
```

### 步骤4：对端主播处理连线邀请

对端主播在步骤 3 的 UI 面板中可以点击同意或者拒绝按钮时，您可以调用 `CoHostStore` 的 `acceptHostConnection` 和 `rejectHostConnection` 接口分别同意或拒绝连线邀请。
``` java
private val coHostStore = CoHostStore.create(liveID)


private val coHostListener = object : CoHostListener() {
        override fun onCoHostRequestReceived(
            inviter: SeatUserInfo, extensionInfo: String
        ){
            // 接受连线
            coHostStore.acceptHostConnection(fromHostLiveID, null)
            //拒绝连线
            // coHostStore.rejectHostConnection(fromHostLiveID, null)


        }    
}

```

### 步骤5：建立连线后，渲染 UI 布局

连线成功后，UI 应当监听 `CoHostStore.coHostState.coHostStatus` 状态流，以及 `LiveSeatStore.liveSeatState.seatList` 状态流，以动态切换和刷新麦位布局。
``` java
import io.trtc.tuikit.atomicxcore.api.live.CoHostStatus
import io.trtc.tuikit.atomicxcore.api.live.LiveSeatStore
import io.trtc.tuikit.atomicxcore.api.live.SeatInfo
import kotlinx.coroutines.flow.collect

// 1. 获取 LiveSeatStore 实例 (通常在房间初始化时获取)
private val liveSeatStore = LiveSeatStore.create(liveID)

// 2. 监听连线状态
coHostStore.coHostState.coHostStatus.collect { status ->
    if (status == CoHostStatus.CONNECTED) {
        // 连线成功，开始渲染连线布局（例如 6v6）
    }
}

// 3. 监听麦位信息，用于刷新连线布局中所有用户的头像、静音状态等
liveSeatStore.liveSeatState.seatList.collect { seatList: List<SeatInfo> ->
    // 布局刷新逻辑：
    // 根据 seatInfo.userInfo.liveID 区分本房间用户和对方房间用户。
    // 根据 seatInfo.userInfo.microphoneStatus 刷新麦克风静音图标。
}
```

### 步骤6：连线过程中继续邀请其他主播参与连线

AtomicXCore 支持您在已经连线的过程中，还可以继续邀请其他主播参与连线，您可以继续调用`requestHostConnection`邀请新的主播参与连线。
``` java
import io.trtc.tuikit.atomicxcore.api.live.CoHostLayoutTemplate
import io.trtc.tuikit.atomicxcore.api.CompletionHandler

// 从 LiveListStore 中获取的目标房间 ID
val targetHostLiveID = "target_host_room_id" 
// 使用 6v6 语聊房静态布局为例
val layoutTemplate = CoHostLayoutTemplate.HOST_STATIC_VOICE_6V6 
val timeout = 10 // 邀请超时时间（秒）
val extraInfo = "" // 额外的业务信息，用于“直连 PK”时携带标识

coHostStore.requestHostConnection(
    targetHostLiveID,
    layoutTemplate,
    timeout,
    extraInfo,
    object : CompletionHandler {
        override fun onSuccess() {
            println("连线请求发送成功，等待对方处理...")
        }
        override fun onFailure(code: Int, desc: String) {
            println("邀请发送失败: $desc")
        }
    }
)
```

### 步骤7：退出连线

当您想退出连线，您可以调用 `CoHostStore` 的 `exitHostConnection` 接口退出；当您退出连线后，还处于连线状态的其他主播的 `LiveSeatStore` 的 `seatList` 会更新。其他还处于连线状态的主播重新根据麦位渲染 UI 即可。
``` java
public void onExitButtonClicked() {
    val coHostStore = CoHostStore.create(liveInfo.liveID)
    coHostStore.exitHostConnection(object : CompletionHandler{
        override fun onSuccess(){

        }
        override fun onFailure(code: Int, desc: String){

        }
    })
}
```

## 主播发起 PK

主播发起 PK 支持两种主要业务流程，以满足不同直播互动需求。核心区别在于 PK 发起前房间的状态。
<table>
<tr>
<td rowspan="1" colSpan="1" >**PK 模式**</td>

<td rowspan="1" colSpan="1" >**房间状态（PK 前）**</td>

<td rowspan="1" colSpan="1" >**房间状态（PK 后）**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**场景一：主播在连线后再发起 PK**</td>

<td rowspan="1" colSpan="1" >双方**已连线**</td>

<td rowspan="1" colSpan="1" >恢复连线状态</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**场景二：主播发起带 PK 模式的连线**</td>

<td rowspan="1" colSpan="1" >双方**未连线**</td>

<td rowspan="1" colSpan="1" >恢复连线状态</td>
</tr>
</table>


### 场景一：主播在连线后再发起 PK

AtomicXCore 支持您在这些主播中发起限时的对战 PK。交互如下图，主要包含以下 UI 交互：
1. 发起连线邀请，对端被邀请的主播接受连线邀请。

2. 参与连线的主播，点击 PK 按钮发起一场限时的对战，可以通过主播收到的礼物数来判定对战的胜负。

3. 对端主播可以弹框提醒，并提示是否加入PK，当被邀请的主播同意后对战即刻开始。

4. PK 开始后，UI 进入对战状态，显示 PK 进度条；该进度条可以是主播收到的礼物数，也可以是收到的点赞数等业务数据。

5. PK 到时间后会自动停止，并且展示胜方和败方，并进入惩罚时间。

6. 当 PK 完全结束后又恢复到连线状态。

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100038646063/9ee5406bcc3111f08e74525400bf7822.png)

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100038646063/9b49a9bacc3111f093295254001c06ec.png)


#### 步骤 1. 连线主播发起 PK 邀请

当主播已经处于跨房连线时，可以在参与连线的主播之间发起一场限时 PK，`AtomicXCore` 支持您设置 PK 的时长、是否需要对端主播同意才开始 PK 以及发起 PK 时携带扩展信息。您可以调用 `BattleStore` 的 `requestBattle` 接口发起 PK 邀请。

> **说明：**
> 
> 1. 当您不设置 `BattleConfig` 的 `duration` 字段时， PK 默认时长为 5 分钟；
> 2. 当您不需要对端主播同意时，您可以设置 `TUIBattleConfig` 的 `needResponse` 字段为 `false`，当邀请发出后 PK 会立即开始；
> 3. 当 `BattleConfig` 的 `needResponse` 字段为 `false` 时，`requestBattle` 接口的 `timeout` 字段必须设置为 0；
> 4. 当设置了超时时间后，如果对端主播在 timeout 时间内还未同意，当次的 PK 邀请会超时，主播和对端主播都会收到 `BattleListener` 的 `onBattleRequestTimeout` 回调；参与连线的所有主播依然可以继续发起下一场 PK。

``` java
// 对方主播的 User ID
val targetUserID = "target_host_user_id" 

val config = BattleConfig(
    duration = 30, // PK 持续 30 秒
    needResponse = true, // 需要对方响应
    extensionInfo = ""
)

battleStore.requestBattle(
    config,
    listOf(targetUserID),
    timeout = 10, // 10 秒内等待响应
    completion = null
)
```

#### 步骤 2. 对端主播收到 PK 邀请

当 PK 请求成功发出后，对端主播会收到 `BattleListener` 的 `onBattleRequestReceived` 回调，您可以在这个回调中给对端主播的UI 提醒 “有人邀请您 PK”，您也可以通过该回调的 battleInfo 参数的 config 字段中的 needResponse 信息确认是否需要 UI 提醒，例如：
- 当 needResponse 为 false 时，您无需提醒，直接进入 PK 状态（详见步骤 3）。

- 当 needResponse 为 true 时，您可以弹框提醒 “有人邀请您 PK”，当对端主播点击同意后进入 PK 状态（详见步骤 3）。

   ``` java
   private val mBattleListener: BattleListener = object : BattleListener() {
           override fun onBattleRequestReceived(
               battleId: String,
               inviter: SeatUserInfo,
               invitee: SeatUserInfo,
           ) {
               super.onBattleRequestReceived(battleInfo, inviter, invitee)
               // 邀请者的信息
               val userId = inviter.userId
               val userName = inviter.userName
               // 是否需要响应
               val needResponse = battleInfo.config.needResponse
           }
       }
   ```

#### 步骤 3. 进入 PK 状态

如下图，当主播监听到 `BattleListener` 的 `onBattleStarted` 回调之后，**可以在 UI 上渲染 PK 进度条**。
- 当 `needResponse` 设置为 `false`, 则当邀请成功发出后，会自动进入 PK 状态。

- 当 `needResponse` 设置为 `true`，则当被邀请的所有对端主播都调用 `BattleStore` 的 `acceptBattle` 接口同意后进入 PK 状态。

- 当 `needResponse` 设置为 `true`，若对端主播同意 PK，则已加入 PK 的主播会收到 `BattleListener` 的 `onUserJoinBattle` 回调。

- 进入 PK 状态之后，参与 PK 的所有主播均会收到 `BattleListener` 的 `onBattleStarted` 回调。

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100036572332/177ffe23bb2311f0a808525400bf7822.png)


#### 步骤 4. 结束 PK 状态

有以下两种方式可以结束 PK 状态。

##### 1. PK 时间结束

当发起 PK 时设置的 `BattleConfig` 中的 `duration` 到时间后，PK 会自动结束，所有参与 PK 的主播均会收到 `BattleListener` 的 `onBattleEnded` 回调；

##### 2. 主动调用 exitBattle 结束 PK

在 PK 过程中，参与 PK 的任一主播均可以调用 `BattleStore` 的 `exitBattle` 退出 PK，其他主播依然处于 PK 中不受影响，且会收到 `BattleListener` 的 `onUserExitBattle` 回调，您可以在这个回调中提醒 “有人退出 PK”；如果在 PK 的 `duration` 还未结束之前，其余人都主动调用 `BattleStore` 的 `exitBattle` 结束 PK 后，整个 PK 同样也会提前结束，最后一个 PK 主播也会收到`BattleListener` 的 `onUserExitBattle` 回调。
``` java
val battleStore:BattleStore = BattleStore.create(liveID)
battleID = battleStore.battleState.currentBattleInfo.value?.battleID
battleStore.exitBattle(battleID, null)
```

当 PK 结束之后 （也即 `BattleListener` 的 `onBattleEnded` 回调触发时），您可以通过该回调在 UI 上展示 PK 结束，并区分出胜负（详见区分胜负章节）

> **说明：**
> 
> - 在连线过程中发起的 PK，当 PK 结束后会自动恢复到跨房连线状态。
> - 如果您想在 PK 结束之后同步结束跨房连线，可以调用 `CoHostStore` 的 `exitHostConnection` 结束连线。


### 场景二：主播发起带 PK 模式的连线

AtomicXCore 支持您在房间内直播时，直接发起 PK （中间不经历连线的交互过程），当 PK 结束后自动恢复到房间内直播状态。如下图所示：
1. 主播在个人直播过程中，点击 PK 按钮，打开 UI 面板展示当前正在开播的主播列表（详见[《主播发起一场连线》的步骤 1](https://write.woa.com/#1ce7ad55-e199-4098-a9bb-554c204fdd97)）。

2. 主播选中其中一个主播，发起 PK 邀请。

3. 对端主播收到邀请后，会在 UI 上提示 “有人向您发来 PK”；选择同意或拒绝连线邀请。

4. 当对端主播同意后，自动进入 PK 状态，PK 过程中可以通过送礼或者点赞来计分。

5. 当 PK 结束之后，根据 PK 过程中的积分来区分胜负。

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100036572332/a095fb06bb2911f0b0cf525400e889b2.png)

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100036572332/844f538fbb2411f0a808525400bf7822.png)
   

   > **说明：**
   > 

   > 该功能需要同时使用 CoHostStore 和 BattleStore，并且借助 BattleConfig 的 needResponse 为 false 完成。
   > 


#### 步骤 1. 主播发起连线请求

此处的步骤与 《主播发起一场连线》中的步骤 1 和步骤 2 相似。唯一的区别在于：主播发起连线请求时，通过`CoHostStore` 的 `requestConnection` 接口设置 `extensionInfo` 字段来标识当前的连线发起后需要同步发起 PK，用于对端主播 UI 提示信息的区分。

例如：
- 当 `extensionInfo` 设置为 {"withPK:true"} 时，对端主播收到连线请求后 UI 提示 “主播向您发起 PK”。

- 当 `extensionInfo` 设置为 {"withPK:false"} 时，对端主播收到连线请求后 UI 提示 “主播邀请您参与跨房连线”。

   ``` java
   import io.trtc.tuikit.atomicxcore.api.live.CoHostLayoutTemplate
   import io.trtc.tuikit.atomicxcore.api.CompletionHandler
   
   
   // 从 LiveListStore 中获取的目标房间 ID
   val targetHostLiveID = "target_host_room_id" 
   // 使用 6v6 语聊房静态布局为例
   val layoutTemplate = CoHostLayoutTemplate.HOST_STATIC_VOICE_6V6 
   val timeout = 10 // 邀请超时时间（秒）
   val extraInfo = "withPK:true" // 对端主播收到连线请求后 UI 提示 “主播向您发起 PK”
   
   coHostStore.requestHostConnection(
       targetHostLiveID,
       layoutTemplate,
       timeout,
       extraInfo,
       object : CompletionHandler {
           override fun onSuccess() {
               println("连线请求发送成功，等待对方处理...")
           }
           override fun onFailure(code: Int, desc: String) {
               println("邀请发送失败: $desc")
           }
       }
   )
   
   ```

#### 步骤 2. 对端主播收到连线请求后，确认加入

当跨房连线邀请发送成功后，对端主播会收到 `CoHostListener` 的 `onCoHostRequestReceived` 回调，对端主播可以监听这个回调并在 UI 上提醒 “主播邀请您参与连线互动”。
``` java
private val coHostListener = object : CoHostListener() {
        override fun onCoHostRequestReceived(
            inviter: SeatUserInfo, extensionInfo: String
        ){
            // 您可以在这里 UI 弹框提醒用户
        }
    }
```

对端主播在步骤 3 的 UI 面板中可以点击同意或者拒绝按钮时，您可以调用 `CoHostStore` 的 `acceptHostConnection` 和 `rejectHostConnection` 接口分别同意或拒绝连线邀请。
``` java
private val coHostStore = CoHostStore.create(liveID)

private val coHostListener = object : CoHostListener() {
        override fun onCoHostRequestReceived(
            inviter: SeatUserInfo, extensionInfo: String
        ){
            // 接受连线
            coHostStore.acceptHostConnection(fromHostLiveID, null)
            //拒绝连线
            // coHostStore.rejectHostConnection(fromHostLiveID, null)

        }
    }
```

#### 步骤 3. 主播监听到对端主播同意加入后，无感知发起 PK

当主播监听到对端主播同意加入连线的通知后，会收到 `CoHostListener` 的 `onCoHostRequestReceived` 回调，此时可以在当前回调中立即调用 `BattleStore` 的 `requestBattle` 接口发起一场无需对端主播同意（也即 `TUIBattleConfig` 的 `needResponse` 为 `false`）的 PK。
``` java
// 在接收方 CoHostListener 中处理：
override fun onCoHostRequestReceived(inviter: SeatUserInfo, extensionInfo: String) {
        coHostStore.acceptHostConnection(inviter.liveID, null)

        val directPKConfig = BattleConfig(
            duration = 30, 
            needResponse = false, // 关键：无需对方二次同意
            extensionInfo = ""
        )
        // 立即向连线发起方发起 PK
        battleStore.requestBattle(
            directPKConfig,
            listOf(inviter.userID), 
            timeout = 0, // 无需等待响应
            completion = null 
        )
    
}
```

#### 步骤 4. 自动进入 PK 状态

此步骤同[《主播在连线后再发起 PK》的步骤 3](https://write.woa.com/#b775b648-c9e2-480c-8678-f7e419e32bfa)相同，此处不再赘述。

## PK 分数更新与胜负判断

### 通过 REST API 实现 PK 分数更新

通常在**直播主播 PK 场景**下，会将主播收到的礼物价值与 PK 数值挂钩（例如：观众送 "火箭" 礼物，主播 PK 分数增加 500 分），您可以通过我们的 REST API，轻松实现直播 PK 场景下的分数实时更新。

> **重要说明：**
> 

> LiveKit 后台的 PK 分数系统采用纯数值计算和累加机制，所以您需要根据自身的运营策略和业务需求，调用更新接口前完成 PK 分数的计算，您可以参考以下的 PK 分数计算示例：
> 
<table>
<tr>
<td rowspan="1" colSpan="1" >礼物类型</td>

<td rowspan="1" colSpan="1" >分数计算规则</td>

<td rowspan="1" colSpan="1" >示例</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >​基础礼物​</td>

<td rowspan="1" colSpan="1" >礼物价值 × 5</td>

<td rowspan="1" colSpan="1" >10元礼物 → 50分</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >​中级礼物​</td>

<td rowspan="1" colSpan="1" >礼物价值 × 8</td>

<td rowspan="1" colSpan="1" >50元礼物 → 400分</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >​高级礼物​</td>

<td rowspan="1" colSpan="1" >礼物价值 × 12</td>

<td rowspan="1" colSpan="1" >100元礼物 → 1200分</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >​特效礼物​</td>

<td rowspan="1" colSpan="1" >固定高分数</td>

<td rowspan="1" colSpan="1" >520元礼物 → 1314分<br></td>
</tr>
</table>



#### REST API 调用流程

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100036572332/b14327dbbabe11f0b9945254005ef0f7.png)


#### 关键流程说明
1. ​**获取 PK 状态​**：

  - 回调配置​：您可以通过配置 [PK 状态回调](https://write.woa.com/document/170122136263680000)，由 LiveKit 后台在 PK 开始、结束时，主动通知您的系统 PK 状态。

  - 主动查询​：您的后台服务可主动调用 [PK 状态查询](https://write.woa.com/document/169572228815638528) 接口，随时查询当前 PK 状态。

2. **PK 分数计算**​：您的后台服务根据业务规则（例如上述示例），计算 PK 分数增量。

3. **PK 分数更新​**：您的后台服务调用 [修改 PK 分数](https://write.woa.com/document/169571965752266752) 接口，向 LiveKit 后台更新 PK 分数。

4. **LiveKit 后台 同步客户端**​：LiveKit 后台自动将更新后的 PK 分数同步到所有客户端。


#### 涉及的 REST API 接口
<table>
<tr>
<td rowspan="1" colSpan="1" >接口</td>

<td rowspan="1" colSpan="1" >功能描述</td>

<td rowspan="1" colSpan="1" >请求示例</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >主动接口 - 查询 PK 状态</td>

<td rowspan="1" colSpan="1" >可根据此接口查询当前房间是否在 PK</td>

<td rowspan="1" colSpan="1" >[请求示例](https://write.woa.com/document/169572228815638528)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >主动接口 - 修改 PK 分数</td>

<td rowspan="1" colSpan="1" >将计算后的 PK 数值通过此接口更新</td>

<td rowspan="1" colSpan="1" >[请求示例](https://write.woa.com/document/169571965752266752)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >回调配置 - PK 开始时回调</td>

<td rowspan="1" colSpan="1" >客户后台可以通过该回调及时知晓 PK 开启</td>

<td rowspan="1" colSpan="1" >[回调示例](https://write.woa.com/document/170122621675196416)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >回调配置 - PK 结束时回调</td>

<td rowspan="1" colSpan="1" >客户后台可以通过该回调及时知晓 PK 结束</td>

<td rowspan="1" colSpan="1" >[回调示例](https://write.woa.com/document/170123212271988736)</td>
</tr>
</table>


### 区分 PK 胜负

通常在**主播 PK 场景**下，需将主播收到的礼物价值与 PK 分值挂钩（例如：观众送 “火箭” 礼物，主播 PK 分值增加 500 分），通过礼物互动提升 PK 竞技性与直播氛围。RoomEngine 的 PK 模块提供了 PK 分值的更新与广播系统，您只需要将观众送礼与之相关联即可。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100036572332/c9639dedba5411f085a55254007c27c5.png)


如上图所示，当您的计费系统检测到有观众送礼并且计费成功后，您可以调用 [修改 PK 分数的 REST API](https://write.woa.com/document/169571965752266752) 更新当前主播的 PK 分值。当主播的 PK 分值发生变化后，参与 PK 的直播间中的所有用户（包含主播和观众）的 `BattleState` 的 `battleScore` 均会发生改变。您可以在 `battleScore` 发生改变的时候，更新 PK 进度条中的分值。
``` java
    private fun observeBattleScore() {
        val job = lifecycleScope.launch {
            battleStore?.battleState?.battleScore?.collect { battleScore ->
                // 您可以在此处更新 PK 进度条中的分值。
            }
        }
        collectJobs.add(job)
    }
```

## API 文档

关于 `CoHostStore`、`BattleStore`、`LiveListStore` 和 `LiveSeatStore` 及其相关类的所有公开接口、属性和方法的详细信息，请参阅随 [**AtomicXCore**](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore) 框架的官方 API 文档。
<table>
<tr>
<td rowspan="1" colSpan="1" >**Store/Component**</td>

<td rowspan="1" colSpan="1" >**功能描述**</td>

<td rowspan="1" colSpan="1" >**API 文档**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**CoHostStore**</td>

<td rowspan="1" colSpan="1" >直播视频流展示与交互的核心视图组件：负责视频流渲染和视图挂件处理，支持主播直播、观众连麦、主播连线等场景。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-co-host-store/index.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**BattleStore**</td>

<td rowspan="1" colSpan="1" >直播间全生命周期管理：创建 / 加入 / 离开 / 销毁房间，查询房间列表，修改直播信息（名称、公告等），监听直播状态（例如被踢出、结束）。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-battle-store/index.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**LiveListStore**</td>

<td rowspan="1" colSpan="1" >直播间全生命周期管理：查询房间列表，修改直播信息等。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-live-list-store/index.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**LiveSeatStore**</td>

<td rowspan="1" colSpan="1" >麦位状态管理： 管理房间内所有麦位状态（包括连线状态下的跨房间麦位），用于监听用户上下麦、麦克风、麦位状态等信息。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-live-seat-store/index.html)</td>
</tr>
</table>


## 常见问题

#### 连线或 PK 时，最大支持的连线房间数量和用户数量限制是多少？

按用户维度计算，最大支持9 个房间互相连线，每个房间支持 50 路用户。

#### 如何实现 PK 失败后的惩罚时间？

您可以在收到 `BattleListener` 的 `onBattleEnded` 回调后，根据 `BattleState` 的 `battleScore` 来判别胜负。虽然此时 PK 业务结束，但连线依然处于进行中，您可以自定义 30 秒的时间用于惩罚环节，待 30 秒倒计时结束之后断开连线。

#### **为什么发起了连线邀请，对方却没收到？**
- 请检查 **targetHostLiveId** 是否正确，并且对方直播间处于正常开播状态。

- 检查网络连接是否通畅，邀请信令有30秒的默认超时时间。


#### 连线或 PK 过程中，一方主播网络断开或App崩溃了怎么办？

**CoHostStore** 和 **BattleStore** 内部都有心跳和超时检测机制。如果一方异常退出，另一方会通过 `onCoHostUserLeft` 或 `onUserExitBattle` 等事件收到通知，您可以根据这些事件来处理UI，例如提示"对方已掉线"并结束互动。

#### 为什么 PK 分数只能通过 REST API 更新？

因为 REST API能同时满足 PK 分数的**安全性、实时性、扩展性**需求：
- **防篡改保公平**：需鉴权 + 数据校验，每笔更新可追溯来源（例如礼物行为），杜绝手动改分、刷分，保障竞技公平。

- **多端实时同步**：用标准化格式（例如 JSON）快速对接礼物、PK、展示系统，确保主播 / 观众 / 后台分数实时一致，无延迟。

- **灵活适配规则**：后端改配置（例如调整礼物对应分数、加成分数）即可适配业务变化，无需改前端，降低迭代成本。


