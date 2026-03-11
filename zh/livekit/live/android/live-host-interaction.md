> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

**AtomicXCore** 提供了 [CoHostStore](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-co-host-store/index.html) 和 [BattleStore](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-battle-store/index.html) 两个核心模块，分别用于处理**跨房连线和 PK 对战**。本文档将指导您如何组合使用这两个工具，来完成直播场景下连线到 PK 的完整流程。

## 核心场景

一次完整的“主播连线 PK”通常包含三个核心阶段，其整体流程如下：

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032603567/596fcf27afc011f09c7d525400454e06.png)


## 实现步骤

### 步骤1：组件集成

请参考 [开始直播](https://write.woa.com/document/191126372105478144) 集成 **AtomicXCore**，并完成 **LiveCoreView** 的接入。

### 步骤2：实现跨房连线

此步骤的目标是让两个主播的画面出现在同一个视图中，我们将使用 [CoHostStore](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-co-host-store/index.html) 来完成。

#### 邀请方（主播 A）实现
1. **发起连线邀请**


   当主播A在界面上选择目标主播B并发起连线时，调用 `requestHostConnection` 方法。

   ``` kotlin
   import androidx.appcompat.app.AppCompatActivity
   import io.trtc.tuikit.atomicxcore.api.CompletionHandler
   import io.trtc.tuikit.atomicxcore.api.live.CoHostLayoutTemplate
   import io.trtc.tuikit.atomicxcore.api.live.CoHostStore
   
   // 主播A的Activity
   class AnchorAActivity : AppCompatActivity() {
       private val liveId = "主播A的房间ID"
       private val coHostStore = CoHostStore.create(liveId)
   
       // 用户点击"连线"按钮，并选择了主播B
       fun inviteHostB(targetHostLiveId: String) {
           val layout = CoHostLayoutTemplate.HOST_DYNAMIC_GRID // 选择一个布局模板
           val timeout = 30 // 邀请超时时间（秒）
   
           coHostStore.requestHostConnection(
               targetHostLiveID = targetHostLiveId,
               layoutTemplate = layout,
               timeout = timeout,
               extraInfo = null,
               completion = object : CompletionHandler {
                   override fun onSuccess() { 
                       println("连线邀请已发送，等待对方处理...")
                   }
   
                   override fun onFailure(code: Int, desc: String) { 
                       println("邀请发送失败: $desc")
                   }
               }
           )
       }
   }
   ```
2. **监听邀请结果**


   通过 `CoHostListener` 的回调方法，您可以接收到主播 B 的处理结果。

   ``` java
   import android.os.Bundle
   import androidx.appcompat.app.AppCompatActivity
   import io.trtc.tuikit.atomicxcore.api.live.CoHostListener
   import io.trtc.tuikit.atomicxcore.api.live.CoHostStore
   import io.trtc.tuikit.atomicxcore.api.live.SeatUserInfo
   
   class AnchorAActivity : AppCompatActivity() {
       private val liveId = "主播A的房间ID"
       private val coHostStore = CoHostStore.create(liveId)
       private val coHostListener = object : CoHostListener() {
           override fun onCoHostRequestAccepted(invitee: SeatUserInfo) {
               println("主播 ${invitee.userName} 同意了你的连线邀请")
           }
   
           override fun onCoHostRequestRejected(invitee: SeatUserInfo) {
               println("主播 ${invitee.userName} 拒绝了你的邀请")
           }
   
           override fun onCoHostRequestTimeout(inviter: SeatUserInfo, invitee: SeatUserInfo) { 
               println("邀请超时，对方未回应")
           }
       }
   
       override fun onCreate(savedInstanceState: Bundle?) {
           super.onCreate(savedInstanceState)
           setContentView(R.layout.activity_anchor_a)
           
           // 初始化CoHostStore
           coHostStore.addCoHostListener(coHostListener)
       }
   }
   ```

#### 受邀方（主播 B）实现
1. **接收连线邀请**


   通过 `CoHostListener`，主播B可以监听到来自主播A的邀请。

   ``` kotlin
   import androidx.appcompat.app.AppCompatActivity
   import io.trtc.tuikit.atomicxcore.api.live.CoHostListener
   import io.trtc.tuikit.atomicxcore.api.live.CoHostStore
   import io.trtc.tuikit.atomicxcore.api.live.SeatUserInfo
   
   // 主播B的Activity
   class AnchorBActivity : AppCompatActivity() {
       private val liveId = "主播B的房间ID"
       private val coHostStore = CoHostStore.create(liveId)
       
       private val coHostListener = object : CoHostListener() {
           override fun onCoHostRequestReceived(inviter: SeatUserInfo, extensionInfo: String) {
               println("收到主播 ${inviter.userName} 的连线邀请")
               // 显示邀请对话框,响应联线邀请
               // showInvitationDialog(inviter)
           }
       }
   }
   ```
2. **响应连线邀请**


   当主播B在弹出的对话框中做出选择后，调用相应的方法。

   ``` kotlin
   // AnchorBActivity 的一部分
   fun acceptInvitation(fromHostLiveId: String) {
       coHostStore.acceptHostConnection(fromHostLiveID = fromHostLiveId, completion = null)
   }
   
   fun rejectInvitation(fromHostLiveId: String) {
       coHostStore.rejectHostConnection(fromHostLiveID = fromHostLiveId, completion = null)
   }
   ```

### 步骤3：实现主播 PK

连线成功后，任意一方都可以发起 PK，此步骤我们将使用 [BattleStore](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-battle-store/index.html) 来实现主播 PK。

#### 挑战方（例如主播 A）实现
1. **发起 PK 挑战**


   当主播 A 点击** PK** 按钮时，调用 `requestBattle` 方法。

   ``` kotlin
   // AnchorAActivity 的一部分
   class AnchorAActivity : AppCompatActivity() {
       private val liveId = "主播A的房间ID"
       private val battleStore = BattleStore.create(liveId)
   
       fun startPK(opponentUserId: String) {
           val config = BattleConfig(duration = 300) // PK持续5分钟
           battleStore.requestBattle(
               config = config,
               userIDList = listOf(opponentUserId),
               timeout = 30,
               completion = null
           )
       }
   }
   ```
2. **监听 PK 状态**


   通过 `BattleListener` 监听 PK 的开始、结束等关键事件。

   ``` java
    // AnchorAActivity 的一部分
   class AnchorAActivity : AppCompatActivity() {
       private val liveId = "主播A的房间ID"
       private val battleStore = BattleStore.create(liveId)
       
       private val battleListener = object : BattleListener() {
           override fun onBattleStarted(
               battleInfo: BattleInfo,
               inviter: SeatUserInfo,
               invitees: List<SeatUserInfo>
           ) {
               println("PK 开始")
           }
   
           override fun onBattleEnded(battleInfo: BattleInfo, reason: BattleEndedReason?) {
               println("PK 结束")
           }
       }
   
       override fun onCreate(savedInstanceState: Bundle?) {
           super.onCreate(savedInstanceState)
           // ... 其他初始化代码 ...
           battleStore.addBattleListener(battleListener)
       }
   }
   ```

#### 应战方（主播 B）实现
1. **接收 PK 挑战**


   通过 `BattleListener` 监听到 PK 邀请。

   ``` kotlin
   // 在 AnchorBActivity 中添加
   class AnchorBActivity : AppCompatActivity() {
       private val liveId = "主播B的房间ID"
       private val battleStore = BattleStore.create(liveId)
   
       private val battleListener = object : BattleListener() {
           override fun onBattleRequestReceived(battleID: String, inviter: SeatUserInfo, invitee: SeatUserInfo) {
               println("收到主播 ${inviter.userName} 的PK挑战")
               // 弹出对话框，让主播B选择"接受"或"拒绝"
               // showPKChallengeDialog(battleID, inviter)
               }
           }
       
           override fun onCreate(savedInstanceState: Bundle?) {
               super.onCreate(savedInstanceState)
               // ... 其他初始化代码 ...
               battleStore.addBattleListener(battleListener)
           }
   }
   ```
2. **响应 PK 挑战**


   当主播 B 做出选择后，调用相应的方法。

   ``` kotlin
   // AnchorBActivity 的一部分
   // 用户点击"接受挑战"
   fun acceptPK(battleId: String) {
       battleStore.acceptBattle(battleID = battleId, completion = null)
   }
   
   // 用户点击"拒绝挑战"
   fun rejectPK(battleId: String) {
       battleStore.rejectBattle(battleID = battleId, completion = null)
   }
   ```

### 运行效果

当您集成以上功能实现后，请分别使用主播 A 和主播 B 进行对应操作，运行效果如下，您可以参考下一章节 [完善 UI 细节](https://write.woa.com/#.E5.AE.8C.E5.96.84-ui-.E7.BB.86.E8.8A.82) 来定制您想要的 UI 逻辑。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032603567/838a83afafcd11f0b28a5254005ef0f7.png)


## 完善 UI 细节

您可以通过 `VideoViewAdapter` 接口提供的"插槽"能力，在视频流画面上添加自定义视图，用于显示昵称、头像、PK 进度条等信息，或在他们关闭摄像头时提供占位图，以优化视觉体验。

### 实现视频流画面的昵称显示

#### 实现效果

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032603567/8bc12d19afcd11f0943c5254007c27c5.png)


#### 实现方式
- **步骤1**：创建前景视图 (**CustomSeatView**)，该视图用于在视频流上方显示用户信息。
   

   > **提示：**
   > 

   > 您也可以参考 TUILiveKit 开源项目中的 [widgets](https://github.com/Tencent-RTC/TUIKit_Android/tree/main/live/tuilivekit/src/main/java/com/trtc/uikit/livekit/features/anchorboardcast/view/cohost/widgets) 目录下文件来了解完整的实现逻辑。
   > 

   ``` kotlin
   import android.content.Context
   import android.graphics.Color
   import android.view.Gravity
   import android.widget.LinearLayout
   import android.widget.TextView
   
   // 自定义的用户信息悬浮视图（前景）
   class CustomSeatView(context: Context) : LinearLayout(context) {
       private val nameLabel: TextView
   
       init {
           orientation = VERTICAL
           setBackgroundColor(Color.parseColor("#80000000")) // 半透明黑色背景
   
           nameLabel = TextView(context).apply {
               setTextColor(Color.WHITE)
               textSize = 14f
               gravity = Gravity.CENTER
           }
   
           addView(nameLabel)
           val layoutParams = nameLabel.layoutParams as LayoutParams
           layoutParams.setMargins(5, 0, 5, 5)
       }
   
       fun setUserName(userName: String) {
           nameLabel.text = userName
       }
   }
   ```
- **步骤2**：创建背景视图 (**CustomAvatarView**)，该视图用于在用户无视频流时作为占位图显示。

   ``` kotlin
   import android.content.Context
   import android.graphics.Color
   import android.view.Gravity
   import android.widget.ImageView
   import android.widget.LinearLayout
   
   // 自定义的头像占位视图（背景）
   class CustomAvatarView(context: Context) : LinearLayout(context) {
       private val avatarImageView: ImageView
   
       init {
           orientation = VERTICAL
           gravity = Gravity.CENTER
           setBackgroundColor(Color.TRANSPARENT)
   
           avatarImageView = ImageView(context).apply {
               setColorFilter(Color.GRAY)
               scaleType = ImageView.ScaleType.CENTER_CROP
           }
   
           addView(avatarImageView)
           val layoutParams = avatarImageView.layoutParams as LayoutParams
           layoutParams.width = 120 // 60dp
           layoutParams.height = 120 // 60dp
       }
   }
   ```
- **步骤3**：实现 `VideoViewAdapter.createCoHostView` 协议，根据 `viewLayer` 的值返回对应的视图。

   ``` kotlin
   import com.tencent.cloud.tuikit.engine.room.TUIRoomDefine
   import android.view.View
   import androidx.appcompat.app.AppCompatActivity
   import io.trtc.tuikit.atomicxcore.api.view.VideoViewAdapter
   import io.trtc.tuikit.atomicxcore.api.view.ViewLayer
   
   // 1. 在您的Activity中，实现 VideoViewAdapter 接口
   class YourActivity : AppCompatActivity(), VideoViewAdapter {
   
       // ... 其他代码 ...
   
       // 2. 完整实现接口方法，处理两种 viewLayer
       override fun createCoHostView(coHostUser: TUIRoomDefine.SeatFullInfo?, viewLayer: ViewLayer?): View? {
           val seatInfo = coHostUser ?: return null
           val userId = seatInfo.userId
           if (userId.isNullOrEmpty()) {
               return null
           }
   
           return when (viewLayer) {
               ViewLayer.FOREGROUND -> {
                   val seatView = CustomSeatView(this)
                   seatView.setUserName(seatInfo.userName ?: "")
                   seatView
               }
               ViewLayer.BACKGROUND -> {
                   val avatarView = CustomAvatarView(this)
                   // 您可以在这里通过 seatInfo.userAvatar 加载用户真实头像
                   avatarView
               }
               null -> null
           }
       }
   }
   ```

#### **参数说明**：
<table>
<tr>
<td rowspan="1" colSpan="1" >**参数**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**说明**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`seatInfo`</td>

<td rowspan="1" colSpan="1" >`SeatFullInfo?`</td>

<td rowspan="1" colSpan="1" >麦位信息对象，包含麦上用户的详细信息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`seatInfo.userId`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >麦上用户的 ID</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`seatInfo.userName`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >麦上用户的昵称</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`seatInfo.userAvatar`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >麦上用户的头像 URL</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`seatInfo.userMicrophoneStatus`</td>

<td rowspan="1" colSpan="1" >`DeviceStatus`</td>

<td rowspan="1" colSpan="1" >麦上用户的麦克风状态</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`seatInfo.userCameraStatus `</td>

<td rowspan="1" colSpan="1" >`DeviceStatus`</td>

<td rowspan="1" colSpan="1" >麦上用户的摄像头状态</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`viewLayer`</td>

<td rowspan="1" colSpan="1" >`ViewLayer`</td>

<td rowspan="1" colSpan="1" >视图层级枚举<br>- `FOREGROUND` 表示前景挂件视图，始终显示在视频画面的最上层<br>- `BACKGROUND` 表示背景挂件视图，位于前景视图下层，仅在对应用户没有视频流（例如未开摄像头）的情况下显示，通常用于展示用户的默认头像或占位图</td>
</tr>
</table>


### 实现 PK 用户视图的分数展示

当主播开始 PK 后，可以在对方主播的视频画面上挂载自定义视图，通常用于展示该主播收到的礼物价值或其它 PK 相关信息。

#### **实现效果**

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032603567/a9a9233aafd911f0943c5254007c27c5.png)


#### 实现方式
- **步骤1**：创建自定义 PK 用户视图，您可以参考 TUILiveKit 开源项目中的 [BattleMemberInfoView.kt](https://github.com/Tencent-RTC/TUIKit_Android/blob/main/live/tuilivekit/src/main/java/com/trtc/uikit/livekit/features/anchorboardcast/view/battle/widgets/BattleMemberInfoView.kt) 文件来了解完整的实现逻辑。

   ``` kotlin
   import android.content.Context
   import android.graphics.Color
   import android.view.Gravity
   import android.widget.LinearLayout
   import android.widget.TextView
   import com.tencent.cloud.tuikit.engine.extension.TUILiveBattleManager.BattleUser
   import io.trtc.tuikit.atomicxcore.api.live.BattleStore
   import kotlinx.coroutines.CoroutineScope
   import kotlinx.coroutines.Dispatchers
   import kotlinx.coroutines.launch
   
   // 自定义PK 用户视图
   class CustomBattleUserView(
       context: Context,
       private val liveId: String,
       private val battleUser: BattleUser
   ) : LinearLayout(context) {
   
       private lateinit var scoreView: LinearLayout
       private lateinit var scoreLabel: TextView
       private val battleStore: BattleStore
   
       init {
           orientation = VERTICAL
           gravity = Gravity.BOTTOM or Gravity.END
           setBackgroundColor(Color.TRANSPARENT)
           isClickable = false
   
           battleStore = BattleStore.create(liveId)
   
           // UI 布局
           setupUI()
           // 订阅分数变化
           subscribeBattleState()
       }
   
       private fun setupUI() {
           scoreView = LinearLayout(context).apply {
               setBackgroundColor(Color.parseColor("#66000000"))
               orientation = VERTICAL
               gravity = Gravity.CENTER
           }
   
           scoreLabel = TextView(context).apply {
               setTextColor(Color.WHITE)
               textSize = 14f
               gravity = Gravity.CENTER
           }
   
           scoreView.addView(scoreLabel)
           addView(scoreView)
   
           val layoutParams = scoreView.layoutParams as LayoutParams
           layoutParams.width = LayoutParams.WRAP_CONTENT
           layoutParams.height = 48 // 24dp
           layoutParams.setMargins(0, 0, 10, 10)
       }
   
       // 订阅 PK 分数变化
       private fun subscribeBattleState() {
           CoroutineScope(Dispatchers.Main).launch {
               battleStore.battleState.battleScore.collect { battleScore ->
                   val score = battleScore[battleUser.userId] ?: 0
                   // 更新 UI
                   scoreLabel.text = score.toString()
               }
           }
       }
   }
   ```
- **步骤2**：实现 `VideoViewAdapter.createBattleView` 协议

   ``` kotlin
     // 1. 让您的Activity实现 VideoViewAdapter 接口
   class YourActivity : AppCompatActivity(), VideoViewAdapter {
   
       override fun createBattleView(battleUser: BattleUser?): View? {
           battleUser ?: return null
           // CustomBattleUserView 是您自定义的PK用户信息视图
           return CustomBattleUserView(this, liveId, battleUser)
       }
   
   }
   ```

#### **参数说明**：
<table>
<tr>
<td rowspan="1" colSpan="1" >**参数**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**说明**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`battleUser`</td>

<td rowspan="1" colSpan="1" >`BattleUser?`</td>

<td rowspan="1" colSpan="1" >PK 用户信息对象</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`battleUser.roomId`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >PK 的房间 ID</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`battleUser.userId`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >PK 用户 ID</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`battleUser.userName`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >PK 用户昵称</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`battleUser.avatarUrl`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >PK 用户头像地址</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`battleUser.score`</td>

<td rowspan="1" colSpan="1" >`int`</td>

<td rowspan="1" colSpan="1" >PK 分数</td>
</tr>
</table>


### 实现视频流画面上的 PK 状态显示

#### **实现效果**

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032603567/2fb544d5afda11f082b4525400e889b2.png)


#### **实现方式**
- **步骤1：**创建自定义 PK 全局视图 **CustomBattleContainerView**，您可以参考 TUILiveKit 开源项目中的 [BattleInfoView.kt](https://github.com/Tencent-RTC/TUIKit_Android/blob/main/live/tuilivekit/src/main/java/com/trtc/uikit/livekit/features/anchorboardcast/view/battle/widgets/BattleInfoView.kt) 文件来实现，即可实现同样的效果。

- **步骤2**：实现 `VideoViewAdapter.createBattleContainerView` 协议。

   ``` kotlin
   // 让您的Activity实现 VideoViewAdapter 接口并设置适配器
   class YourActivity : AppCompatActivity(), VideoViewAdapter {
       override fun createBattleContainerView(): View? {
           return CustomBattleContainerView(this)
       }
   }
   ```

## 功能进阶

### 通过 REST API 实现 PK 分数更新

通常在**直播主播 PK 场景**下，会将主播收到的礼物价值与 PK 数值挂钩（例如：观众送 "火箭" 礼物，主播 PK 分数增加 500 分），您可以通过我们的 REST API，轻松实现直播 PK 场景下的分数实时更新。

> **重要说明：**
> 

> LiveKit 后台的 PK 分数系统采用纯数值计算和累加机制，所以您需要根据自身的运营策略和业务需求，在调用更新接口前完成 PK 分数的计算，您可以参考如下的 PK 分数计算示例：
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

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032603567/7cc3e8afafda11f0b28a5254005ef0f7.png)


#### 关键流程说明
1. ​**获取 PK 状态​**：

  - 回调配置​：您可以通过配置 [PK 状态回调](https://write.woa.com/document/170122621675196416)，由 LiveKit 后台在 PK 开始、结束时，主动通知您的系统 PK 状态。

  - 主动查询​：您的后台服务可主动调用 [PK 状态查询](https://write.woa.com/document/169572228815638528) 接口，随时查询当前 PK 状态。

2. **PK分数计算**​：您的后台服务根据业务规则（如上述示例），计算 PK 分数增量。

3. **PK分数更新​**：您的后台服务调用 [修改 PK 分数](https://write.woa.com/document/169571965752266752) 接口，向 LiveKit 后台更新 PK 分数。

4. **LiveKit后台 同步客户端**​：LiveKit 后台自动将更新后的 PK 分数同步到所有客户端。


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


## API 文档

关于 [CoHostStore](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-co-host-store/index.html) 及其相关类的所有公开接口、属性和方法的详细信息，请参阅随 [AtomicXCore](https://tencent-rtc.github.io/TUIKit_Android/index.html) 框架的官方 API 文档。本指南使用到的相关 Store 如下：
<table>
<tr>
<td rowspan="1" colSpan="1" >Store/Component</td>

<td rowspan="1" colSpan="1" >功能描述</td>

<td rowspan="1" colSpan="1" >API 文档</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >LiveCoreView</td>

<td rowspan="1" colSpan="1" >直播视频流展示与交互的核心视图组件：负责视频流渲染和视图挂件处理，支持主播直播、观众连麦、主播连线等场景。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.view/-live-core-view/index.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >DeviceStore</td>

<td rowspan="1" colSpan="1" >音视频设备控制：麦克风（开关 / 音量）、摄像头（开关 / 切换 / 画质）、屏幕共享，设备状态实时监听。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.device/-device-store/index.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >CoHostStore</td>

<td rowspan="1" colSpan="1" >主播跨房连线：支持多布局模板（动态网格等），发起 / 接受 / 拒绝连线，连麦主播互动管理。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-co-host-store/index.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >BattleStore</td>

<td rowspan="1" colSpan="1" >主播 PK 对战：发起 PK（配置时长 / 对手），管理 PK 状态（开始 / 结束），同步分数，监听对战结果。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-battle-store/index.html)</td>
</tr>
</table>


## 常见问题

### **为什么发起了连线邀请，对方却没收到？**
- 请检查 **targetHostLiveId** 是否正确，并且对方直播间处于正常开播状态。

- 检查网络连接是否通畅，邀请信令有30秒的默认超时时间。


### 连线或PK过程中，一方主播网络断开或App崩溃了怎么办？

**CoHostStore** 和 **BattleStore** 内部都有心跳和超时检测机制。如果一方异常退出，另一方会通过 **onCoHostUserLeft** 或 **onUserExitBattle** 等事件收到通知，您可以根据这些事件来处理UI，例如提示"对方已掉线"并结束互动。

### 为什么 PK 分数只能通过 REST API 更新？

因为 REST API  能同时满足 PK 分数的**安全性、实时性、扩展性**需求：
- **防篡改保公平**：需鉴权 + 数据校验，每笔更新可追溯来源（例如礼物行为），杜绝手动改分、刷分，保障竞技公平；

- **多端实时同步**：用标准化格式（例如 JSON）快速对接礼物、PK、展示系统，确保主播 / 观众 / 后台分数实时一致，无延迟；

- **灵活适配规则**：后端改配置（例如调整礼物对应分数、加成分数）即可适配业务变化，无需改前端，降低迭代成本。


### 如何管理通过 `VideoViewAdapter` 添加的自定义视图的生命周期和事件？

**LiveCoreView** 会自动管理您通过适配器方法返回视图的添加和移除，您无需手动处理。如果需要在自定义视图中处理用户交互（例如点击事件），请在创建视图时为其添加相应的事件即可。

