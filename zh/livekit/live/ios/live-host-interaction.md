> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

**AtomicXCore** 提供了 [CoHostStore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/cohoststore) 和 [BattleStore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/battlestore) 两个核心模块，分别用于处理**跨房连线和 PK 对战**。本文档将指导您如何组合使用这两个工具，来完成直播场景下连线到 PK 的完整流程。

## 核心场景

一次完整的“主播连线 PK”通常包含三个核心阶段，其整体流程如下：

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027182498/0a02a43ea68411f0b8b9525400454e06.png)


## 实现步骤

### 步骤1：组件集成

请参考 [开始直播](https://write.woa.com/document/191126382767431680) 集成 **AtomicXCore**，并完成 **LiveCoreView** 的接入。

### 步骤2：实现跨房连线

此步骤的目标是让两个主播的画面出现在同一个视图中，我们将使用 [CoHostStore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/cohoststore) 来完成。

#### 邀请方（主播 A）实现
1. **发起连线邀请**


   当主播A在界面上选择目标主播 B 并发起连线时，调用 `requestHostConnection` 方法。

   ``` swift
   import AtomicXCore
   import Combine
   
   // 主播A的视图控制器
   class AnchorAViewController {
       private let liveId = "主播A的房间ID"
       private var cancellables: Set<AnyCancellable> = []
       private lazy var coHostStore: CoHostStore = {
           return CoHostStore.create(liveID: self.liveId)
       }()
   
       // 用户点击“连线”按钮，并选择了主播B
       func inviteHostB(targetHostLiveId: String) {
           let layout: CoHostLayoutTemplate = .hostDynamicGrid // 选择一个布局模板
           let timeout: TimeInterval = 30.0 // 邀请超时时间
   
           coHostStore.requestHostConnection(targetHost: targetHostLiveId,
                                             layoutTemplate: layout,
                                             timeout: timeout) { result in
               switch result {
               case .success():
                   print("连线邀请已发送，等待对方处理...")
               case .failure(let error):
                   print("邀请发送失败: \(error.message)")
               }
           }
       }
   }
   ```
2. **监听邀请结果**


   通过订阅 `coHostEventPublisher`，您可以接收到主播 B 的处理结果。

   ``` swift
   // 在 AnchorAViewController 初始化时设置监听
   func setupListeners() {
       coHostStore.coHostEventPublisher
           .sink { [weak self] event in
               switch event {
               case .onCoHostRequestAccepted(let invitee): //
                   print("主播 \(invitee.userName) 同意了你的连线邀请")
               case .onCoHostRequestRejected(let invitee): //
                   print("主播 \(invitee.userName) 拒绝了你的邀请")
               case .onCoHostRequestTimeout: //
                   print("邀请超时，对方未回应")
               default:
                   break
               }
           }
           .store(in: &cancellables)
   }
   ```

#### 受邀方（主播 B）实现
1. **接收连线邀请**


   通过 `coHostEventPublisher`，主播B可以监听到来自主播 A 的邀请。

   ``` swift
   import AtomicXCore
   import Combine
   
   // 主播B的视图控制器
   class AnchorBViewController {
       // ... coHostStore 和 cancellables 初始化 ...
   
       // 在初始化时设置监听
       func setupListeners() {
           coHostStore.coHostEventPublisher
               .sink { [weak self] event in
                   if case let .onCoHostRequestReceived(inviter, _) = event { //
                       print("收到主播 \(inviter.userName) 的连线邀请")
                       // self?.showInvitationDialog(from: inviter)
                   }
               }
               .store(in: &cancellables)
       }
   }
   ```
2. **响应连线邀请**


   当主播 B 在弹出的对话框中做出选择后，调用相应的方法。

   ``` swift
   // AnchorBViewController 的一部分
   func acceptInvitation(fromHostLiveId: String) {
       coHostStore.acceptHostConnection(fromHostLiveID: fromHostLiveId, completion: nil) //
   }
   
   func rejectInvitation(fromHostLiveId: String) {
       coHostStore.rejectHostConnection(fromHostLiveID: fromHostLiveId, completion: nil) //
   }
   ```

### 步骤3：实现主播 PK

连线成功后，任意一方都可以发起 PK，此步骤我们将使用 [BattleStore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/battlestore) 来实现主播 PK。

#### 挑战方（例如主播 A）实现
1. **发起 PK 挑战**


   当主播 A 点击“PK”按钮时，调用 `requestBattle` 方法。

   ``` swift
     
   // AnchorAViewController 的一部分
   private lazy var battleStore: BattleStore = BattleStore.create(liveID: self.liveId)
   
   func startPK(with opponentUserId: String) {
       var config = BattleConfig(duration: 300) // PK持续5分钟
       battleStore.requestBattle(config: config, userIDList: [opponentUserId], timeout: 30.0, completion: nil)
   }
   ```
2. **监听 PK 状态**


   通过 `battleEventPublisher` 监听 PK 的开始、结束等关键事件。

   ``` swift
   // 在 AnchorAViewController 的 setupListeners 方法中添加
   battleStore.battleEventPublisher
       .sink { [weak self] event in
           switch event {
           case .onBattleStarted: //
               print("PK 开始")
           case .onBattleEnded: //
               print("PK 结束")
           default:
               break
           }
       }
       .store(in: &cancellables)
   ```

#### 应战方（主播 B）实现
1. **接收 PK 挑战**


   通过 `battleEventPublisher` 监听到 PK 邀请。

   ``` swift
   // 在 AnchorBViewController 的 setupListeners 方法中添加
   battleStore.battleEventPublisher
       .sink { [weak self] event in
           if case let .onBattleRequestReceived(battleId, inviter, _) = event {
               print("收到主播 \(inviter.userName) 的PK挑战")
               // 弹出对话框，让主播B选择“接受”或“拒绝”
               // self?.showPKChallengeDialog(battleId: battleId)
           }
       }
       .store(in: &cancellables)
   ```
2. **响应 PK 挑战**


   当主播 B 做出选择后，调用相应的方法。

   ``` swift
   // AnchorBViewController 的一部分
   // 用户点击“接受挑战”
   func acceptPK(battleId: String) {
       battleStore.acceptBattle(battleID: battleId) { result in
           // ...
       }
   }
   
   // 用户点击“拒绝挑战”
   func rejectPK(battleId: String) {
       battleStore.rejectBattle(battleID: battleId) { result in
           // ...
       }
   }
   ```

### 运行效果

当您集成以上功能实现后，请分别使用主播 A 和主播 B 进行对应操作，运行效果如下，您可以参考下一章节 [完善 UI 细节](https://write.woa.com/#6fe270da-d3b3-4785-bdc2-53b59d6d9cc0) 来定制您想要的 UI 逻辑。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027182498/8496bbe6a68611f0930a5254007c27c5.png)


## 完善 UI 细节

您可以通过 `LiveCoreView.VideoViewDelegate` 协议提供的“插槽”能力，在视频流画面上添加自定义视图，用于显示昵称、头像、PK 进度条等信息，或在他们关闭摄像头时提供占位图，以优化视觉体验。

### 实现视频流画面的昵称显示

#### 实现效果

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027182498/4411f8b7a69411f09936525400e889b2.png)


#### 实现方式
- **步骤1**：创建前景视图 (**CustomSeatView**)，该视图用于在视频流上方显示用户信息。
   

   > **提示：**
   > 

   > 您也可以参考 TUILiveKit 开源项目中的 [AnchorCoHostView.swift](https://github.com/Tencent-RTC/TUIKit_iOS/blob/main/live/Sources/Features/AnchorBoardcast/View/LivingView/Video/AnchorCoHostView.swift) 和 [AnchorEmptySeatView.swift](https://github.com/Tencent-RTC/TUIKit_iOS/blob/main/live/Sources/Features/AnchorBoardcast/View/LivingView/Video/AnchorEmptySeatView.swift) 文件来了解完整的实现逻辑。
   > 

   ``` swift
   import UIKit
   import SnapKit
   
   // 自定义的用户信息悬浮视图（前景）
   class CustomSeatView: UIView {
      lazy var nameLabel: UILabel = {
           let label = UILabel()
           label.textColor = .white
           label.font = .systemFont(ofSize: 14)
           return label
       }()
   
       override init(frame: CGRect) {
           super.init(frame: frame)
           backgroundColor = UIColor.black.withAlphaComponent(0.5)
           addSubview(nameLabel)
           nameLabel.snp.makeConstraints { make in
               make.bottom.equalToSuperview().offset(-5)
               make.leading.equalToSuperview().offset(5)
           }
       }
   }
   ```
- **步骤2**：创建背景视图 (**CustomAvatarView**)，该视图用于在用户无视频流时作为占位图显示。

   ``` swift
   import UIKit
   import SnapKit
   
   // 自定义的头像占位视图（背景）
   class CustomAvatarView: UIView {
       lazy var avatarImageView: UIImageView = {
           let imageView = UIImageView()
           imageView.tintColor = .gray
           return imageView
       }()
   
       override init(frame: CGRect) {
           super.init(frame: frame)
           backgroundColor = .clear
           layer.cornerRadius = 30
           addSubview(avatarImageView)
           avatarImageView.snp.makeConstraints { make in
               make.center.equalToSuperview()
               make.width.height.equalTo(60)
           }
       }
   }
   ```
- **步骤3**：实现 `VideoViewDelegate.createCoHostView` 协议，根据 `viewLayer` 的值返回对应的视图。

   ``` swift
   import AtomicXCore
   import RTCRoomEngine
   
   // 1. 在您的视图控制器中，遵守 VideoViewDelegate 协议
   class YourViewController: UIViewController, VideoViewDelegate {
   
       // ... 其他代码 ...
       
       // 2. 完整实现协议方法，处理两种 viewLayer
       func createCoHostView(seatInfo: TUISeatFullInfo, viewLayer: ViewLayer) -> UIView? {
           guard let userId = seatInfo.userId, !userId.isEmpty else {
               return nil
           }
           if viewLayer == .foreground {
               let seatView = CustomSeatView()
               seatView.nameLabel.text = seatInfo.userName
               return seatView
           } else { // viewLayer == .background
               let avatarView = CustomAvatarView()
               // 您可以在这里通过 seatInfo.userAvatar 加载用户真实头像
               return avatarView
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

<td rowspan="1" colSpan="1" >`TUISeatFullInfo`</td>

<td rowspan="1" colSpan="1" >麦位信息对象，包含麦上用户的详细信息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`seatInfo.userId`</td>

<td rowspan="1" colSpan="1" >`String?`</td>

<td rowspan="1" colSpan="1" >麦上用户的 ID</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`seatInfo.userName`</td>

<td rowspan="1" colSpan="1" >`String? `</td>

<td rowspan="1" colSpan="1" >麦上用户的昵称</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`seatInfo.userAvatar`</td>

<td rowspan="1" colSpan="1" >`String?`</td>

<td rowspan="1" colSpan="1" >麦上用户的头像 URL</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`seatInfo.userMicrophoneStatus`</td>

<td rowspan="1" colSpan="1" >`TUIDeviceStatus`</td>

<td rowspan="1" colSpan="1" >麦上用户的麦克风状态</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`seatInfo.userCameraStatus `</td>

<td rowspan="1" colSpan="1" >`TUIDeviceStatus`</td>

<td rowspan="1" colSpan="1" >麦上用户的摄像头状态</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`viewLayer`</td>

<td rowspan="1" colSpan="1" >`ViewLayer`</td>

<td rowspan="1" colSpan="1" >视图层级枚举<br>`.foreground` 表示前景挂件视图，始终显示在视频画面的最上层<br>`.background` 表示背景挂件视图，位于前景视图下层，仅在对应用户没有视频流（例如未开摄像头）的情况下显示，通常用于展示用户的默认头像或占位图</td>
</tr>
</table>


### 实现 PK 用户视图的分数展示

当主播开始 PK 后，可以在对方主播的视频画面上挂载自定义视图，通常用于展示该主播收到的礼物价值或其它 PK 相关信息。

#### **实现效果**

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027182498/c8cbd5eda69311f091df5254005ef0f7.png)


#### 实现方式
- **步骤1**：创建自定义 PK 用户视图，您可以参考 TUILiveKit 开源项目中的 [AnchorBattleMemberInfoView.swift](https://github.com/Tencent-RTC/TUIKit_iOS/blob/main/live/Sources/Features/AnchorBoardcast/View/HostBattle/View/AnchorBattleMemberInfoView.swift) 文件来了解完整的实现逻辑。

   ``` swift
   import AtomicXCore
   import RTCRoomEngine
   import SnapKit
   
   // 自定义PK 用户视图
   class CustomBattleUserView: UIView {
       private let scoreView: UIView = {
           let view = UIView()
           view.backgroundColor = .black.withAlphaComponent(0.4)
           view.layer.cornerRadius = 12
           return view
       }()
   
       private lazy var scoreLabel: UILabel = {
           let label = UILabel()
           label.textColor = .white
           label.font = .systemFont(ofSize: 14, weight: .bold)
           return label
       }()
       
       private var userId: String
       private let battleStore: BattleStore
       private var cancellableSet: Set<AnyCancellable> = []
       
       init(liveId: String, battleUser: TUIBattleUser) {
           self.userId = battleUser.userId
           self.battleStore = BattleStore.create(liveID: liveId)
           super.init(frame: .zero)
           backgroundColor = .clear
           isUserInteractionEnabled = false
           // UI 布局
           setupUI()
           // 订阅分数变化
           subscribeBattleState()
       }
       
       private func setupUI() {
           addSubView(scoreView)       
           scoreView.addSubview(scoreLabel)
           scoreLabel.snp.makeConstraints { make in
               make.leading.trailing.equalToSuperview().inset(5)
           }
           scoreView.snp.makeConstraints { make in
               make.height.equalTo(24)
               make.bottom.equalToSuperview().offset(-5)
               make.trailing.equalToSuperview().offset(-5)
           }
       }
       
       // 订阅 PK 分数变化
       private func subscribeBattleState() {
           battleStore.state
               .subscribe(StatePublisherSelector(keyPath: \BattleState.battleScore))
               .removeDuplicates()
               .receive(on: RunLoop.main)
               .sink { battleUsers in
                   guard let self = self else { return }
                   guard let score = battleScore[self.userId] else { return }
                   // 更新 UI 
                   self.scoreLabel.text = "\(battleUser.score)"
               }
               .store(in: &cancellableSet)
       }
   }
   ```
- **步骤2**：实现 `VideoViewDelegate.createBattleView` 协议

   ``` swift
     // 1. 让您的视图控制器遵守 VideoViewDelegate 协议
   extension YourViewController: VideoViewDelegate {
   
       public func createBattleView(battleUser: TUIBattleUser) -> UIView? {
           // CustomBattleUserView 是您自定义的PK用户信息视图
           let customView = CustomBattleUserView(liveId:liveId, battleUser:battleUser)
           return customView
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

<td rowspan="1" colSpan="1" >`TUIBattleUser`</td>

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

<td rowspan="1" colSpan="1" >`UInt`</td>

<td rowspan="1" colSpan="1" >PK 分数</td>
</tr>
</table>


### 实现视频流画面上的 PK 状态显示

#### **实现效果**

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027182498/b41a8b8ba69311f091df5254005ef0f7.png)


#### **实现方式**
- **步骤1：**创建自定义 PK 全局视图 **CustomBattleContainerView**，您可以参考 TUILiveKit 开源项目中的 [AnchorBattleInfoView.swift](https://github.com/Tencent-RTC/TUIKit_iOS/blob/main/live/Sources/Features/AnchorBoardcast/View/HostBattle/View/AnchorBattleInfoView.swift) 文件来实现，即可实现同样的效果。

- **步骤2**：实现 `VideoViewDelegate.createBattleContainerView` 协议。

   ``` swift
   // 让您的视图控制器遵守 VideoViewDelegate 协议并设置代理
   extension YourViewController: VideoViewDelegate {
       func createBattleContainerView() -> UIView? {
           return CustomBattleContainerView()
       }
   }
   ```

## 功能进阶

### 通过 REST API 实现 PK 分数更新

通常在**直播主播 PK 场景**下，会将主播收到的礼物价值与 PK 数值挂钩（例如：观众送 “火箭” 礼物，主播 PK 分数增加 500 分），您可以通过我们的 REST API，轻松实现直播 PK 场景下的分数实时更新。

> 重要说明：
> 

> LiveKit 后台的 PK 分数系统采用纯数值计算和累加机制，所以您需要根据自身的运营策略和业务需求，调用更新接口前完成 PK 分数的计算，您可以参考如下的 PK 分数计算示例：
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

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027182498/4329dd7fa69511f0a90152540099c741.png)


#### 关键流程说明
1. ​**获取 PK 状态​**：

  - 回调配置​：您可以通过配置 [PK 状态回调](https://write.woa.com/document/170122621675196416)，由 LiveKit 后台在 PK 开始、结束时，主动通知您的系统 PK 状态。

  - 主动查询​：您的后台服务可主动调用 [PK 状态查询](https://write.woa.com/document/169572228815638528) 接口，随时查询当前 PK 状态。

2. **PK分数计算**​：您的后台服务根据业务规则（如上述示例），计算 PK 分数增量。

3. **PK分数更新​**：您的后台服务调用 [修改 PK 分数](https://write.woa.com/document/169571965752266752) 接口，向 LiveKit 后台更新 PK 分数。

4. **LiveKit****后台 同步客户端**​：LiveKit 后台自动将更新后的 PK 分数同步到所有客户端。


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

关于 [CoHostStore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/cohoststore) 及其相关类的所有公开接口、属性和方法的详细信息，请参阅随 [AtomicXCore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore) 框架的官方 API 文档。本指南使用到的相关 Store 如下：
<table>
<tr>
<td rowspan="1" colSpan="1" >Store/Component</td>

<td rowspan="1" colSpan="1" >功能描述</td>

<td rowspan="1" colSpan="1" >API 文档</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >LiveCoreView</td>

<td rowspan="1" colSpan="1" >直播视频流展示与交互的核心视图组件：负责视频流渲染和视图挂件处理，支持主播直播、观众连麦、主播连线等场景。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/livecoreview)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >DeviceStore</td>

<td rowspan="1" colSpan="1" >音视频设备控制：麦克风（开关 / 音量）、摄像头（开关 / 切换 / 画质）、屏幕共享，设备状态实时监听。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/devicestore)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >CoHostStore</td>

<td rowspan="1" colSpan="1" >主播跨房连线：支持多布局模板（动态网格等），发起 / 接受 / 拒绝连线，连麦主播互动管理。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/cohoststore)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >BattleStore</td>

<td rowspan="1" colSpan="1" >主播 PK 对战：发起 PK（配置时长 / 对手），管理 PK 状态（开始 / 结束），同步分数，监听对战结果。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/battlestore)</td>
</tr>
</table>


## 常见问题

### **为什么发起了连线邀请，对方却没收到？**
- 请检查 `targetHostLiveId` 是否正确，并且对方直播间处于正常开播状态。

- 检查网络连接是否通畅，邀请信令有30秒的默认超时时间。


### 连线或 PK 过程中，一方主播网络断开或 App 崩溃了怎么办？

**CoHostStore** 和 **BattleStore** 内部都有心跳和超时检测机制。如果一方异常退出，另一方会通过 **onCoHostUserLeft** 或 **onUserExitBattle** 等事件收到通知，您可以根据这些事件来处理UI，例如提示“对方已掉线”并结束互动。

### 为什么 PK 分数只能通过 REST API 更新？

因为 REST API  能同时满足 PK 分数的**安全性、实时性、扩展性**需求：
- **防篡改保公平**：需鉴权 + 数据校验，每笔更新可追溯来源（例如礼物行为），杜绝手动改分、刷分，保障竞技公平；

- **多端实时同步**：用标准化格式（例如 JSON）快速对接礼物、PK、展示系统，确保主播 / 观众 / 后台分数实时一致，无延迟；

- **灵活适配规则**：后端改配置（例如调整礼物对应分数、加成分数）即可适配业务变化，无需改前端，降低迭代成本。


### 如何管理通过 `VideoViewDelegate` 添加的自定义视图的生命周期和事件？

**LiveCoreView** 会自动管理您通过代理方法返回视图的添加和移除，您无需手动处理。如果需要在自定义视图中处理用户交互（例如点击事件），请在创建视图时为其添加相应的事件即可。

