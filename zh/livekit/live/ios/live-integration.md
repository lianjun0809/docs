> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

本文档将帮助您使用 **AtomicXCore SDK **的核心组件 [LiveCoreView](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/livecoreview)，快速构建一个包含主播开播和观众观看功能的基础直播 App。

## **核心功能**

**LiveCoreView** 是一个专为直播场景设计的轻量级 `UIView` 组件，是您构建直播场景的核心，它封装了所有复杂的底层直播技术（例如推拉流、连麦、音视频渲染）。您可以将 LiveCoreView 作为直播画面的“画布”，专注于上层 UI 与交互的开发。

通过下方的视图层级示意图，您可以直观了解 **LiveCoreView** 在直播界面中的位置和作用：

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027182498/415b5505a5b011f0a90152540099c741.png)


## 准备工作

### 步骤1：开通服务

请参见 [开通服务](https://write.woa.com/document/141302177829593088)，获取体验版或付费版 SDK。

### 步骤2：在当前项目中导入 AtomicXCore
1. **安装组件**：请在您的 **Podfile** 文件中添加 `pod 'AtomicXCore'` 依赖，然后执行`pod install`。

   ``` ruby
   target 'xxxx' do
     pod 'AtomicXCore'
   end
   ```
2. **配置工程权限:  **请在应用的 `Info.plist` 文件中添加相机和麦克风的使用权限说明。

   ``` ruby
   <key>NSCameraUsageDescription</key>
   <string>TUILiveKit需要访问你的相机权限，开启后录制的视频才会有画面</string>
   <key>NSMicrophoneUsageDescription</key>
   <string>TUILiveKit需要访问您的麦克风权限，开启后录制的视频才会有声音</string>
   ```
   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027182498/5f6d26e7a5b011f09936525400e889b2.png)


### 步骤3：实现登录逻辑

在您的项目中调用 `LoginStore.shared.login` 完成登录，**这是使用 **`AtomicXCore`** 所有功能的关键前提**。

> **重要：**
> 

> 推荐在您 App 自身的用户账户登录成功后，再调用 LoginStore.shared.login，以确保登录业务逻辑的清晰和一致。
> 

``` swift
import AtomicXCore

//  AppDelegate.swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    LoginStore.shared.login(sdkAppID: 1400000001,                  // 替换为您的 SDKAppID
                            userID: "test_001",                    // 替换为您的 UserID
                            userSig: "xxxxxxxxxxx") { result in    // 替换为您的 UserSig
      switch result {
        case .success(let info):
        debugPrint("login success")
        case .failure(let error):
        debugPrint("login failed code:\(error.code), message:\(error.message)")
      }
    }
    return true
}
```

**登录接口参数说明：**
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >说明</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >sdkAppId</td>

<td rowspan="1" colSpan="1" >Int32</td>

<td rowspan="1" colSpan="1" >从 [控制台](https://console.cloud.tencent.com/trtc) 获取，通常是以 `140` 或 `160` 开头的 10 位整数。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userID</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >当前用户的唯一 ID，仅包含英文字母、数字、连字符和下划线。为避免多端登录冲突，**请勿使用**`1`、`123`**等简单 ID**。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userSig</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >用于腾讯云鉴权的票据。请注意：<br>- 开发环境：您可以采用本地 `GenerateTestUserSig.genTestSig` 函数生成 userSig 或者通过 [UserSig 辅助工具](https://console.cloud.tencent.com/im/tool-usersig) 生成临时的 UserSig。<br>- 生产环境：为了防止密钥泄露，请务必采用服务端生成 UserSig 的方式。详细信息请参考 [服务端生成 UserSig](https://cloud.tencent.com/document/product/647/17275)。<br>更多信息请参见 [如何计算及使用 UserSig](https://cloud.tencent.com/document/product/647/17275)。</td>
</tr>
</table>


## 搭建基础直播间

### 步骤1：实现主播视频开播

主播开播流程如下，您只需执行以下几步操作，即可快速搭建主播视频直播。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027182498/8dd049b0a66e11f0bf2352540044a08e.png)


> **提示：**
> 

> 主播开播推流的业务代码，您也可以参考 TUILiveKit 开源项目中的 [TUILiveRoomAnchorViewController.swift](https://github.com/Tencent-RTC/TUIKit_iOS/blob/main/live/Sources/LiveStream/TUILiveRoomAnchorViewController.swift) 文件来了解完整的实现逻辑。
> 

1. **初始化主播推流的视图**


   在您的主播视图控制器中，创建一个 `LiveCoreView` 实例，并将 `viewType` 指定为 `.pushView`（推流视图）。

   ``` swift
   import AtomicXCore
   
   // YourAnchorViewController 代表您的主播开播视图控制器
   class YourAnchorViewController: UIViewController {
   
       private let liveId: String
       // 1. 将 LiveCoreView 作为您视图控制器的一个属性
       private let coreView = LiveCoreView(viewType:.pushView, frame: UIScreen.main.bounds)
      
       // 2. 新增便利构造函数完成实例初始化
       //    - liveId: 您需要开播的直播房间 id
       public init(liveId: String) {
           self.liveId = liveId
           super.init(nibName: nil, bundle: nil)
           self.coreView.setLiveID(liveId)
       }
       
       required init?(coder: NSCoder) {
           fatalError("init(coder:) has not been implemented")
       }
       
       public override func viewDidLoad() {
           super.viewDidLoad()
           // 3. 将主播推流页面加载到您的视图上
           view.addSubview(coreView)
       }
   }  
   ```
2. **打开摄像头和麦克风**


   通过调用 **DeviceStore** 的 `openLocalCamera、openLocalMicrophone` 接口打开摄像头和麦克风，**您无需做额外操作，LiveCoreView 会自动预览当前摄像头的视频流**，示例代码如下：

   ``` swift
   import AtomicXCore
   
   // YourAnchorViewController 代表您的主播开播视图控制器
   class YourAnchorViewController: UIViewController {
       // ... 其他代码 ...
       public override func viewDidLoad() {
           super.viewDidLoad()
           // 打开设备
           openDevices()
       }
       
       private func openDevices() {
           // 1. 打开前置摄像头 
           DeviceStore.shared.openLocalCamera(isFront: true, completion: nil)
           // 2. 打开麦克风
           DeviceStore.shared.openLocalMicrophone(completion: nil)
       }
   }
   ```
3. **开始直播**


   通过调用 **LiveListStore** 的 `createLive` 接口开始视频直播，完整示例代码如下：

   ``` swift
   import AtomicXCore
   
   // YourAnchorViewController 代表您的主播开播视图控制器
   class YourAnchorViewController: UIViewController {
   
       // ... 其他代码 ...
   
       // 调用开播接口开始直播
       private func startLive() {
           var liveInfo = LiveInfo()
           // 1. 设置直播的房间 id
           liveInfo.liveID = self.liveId
           // 2. 设置直播的房间名称
           liveInfo.liveName = "test 直播"
           // 3. 配置布局模板，默认：600 动态宫格布局
           liveInfo.seatLayoutTemplateID = 600
           // 4. 配置主播始终在麦位上
           liveInfo.keepOwnerOnSeat = true
           // 5. 调用 LiveListStore.shared.createLive 开始直播
           LiveListStore.shared.createLive(liveInfo) { [weak self] result in
               guard let self = self else { return }
               switch result {
               case .success(let info):
                   debugPrint("startLive success")
               case .failure(let error):
                   debugPrint("startLive error:\(error.message)")
               }
           }
       }
   }  
   ```

   `LiveInfo`**参数说明:**

<table>
<tr>
<td rowspan="1" colSpan="1" >**参数名**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**属性**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`liveID`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >必填</td>

<td rowspan="1" colSpan="1" >直播间的唯一标识符。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`liveName`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >直播间的标题。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`notice`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >直播间的公告信息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`isMessageDisable`</td>

<td rowspan="1" colSpan="1" >`Bool`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >是否禁言（`true`：是，`false`：否）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`isPublicVisible`</td>

<td rowspan="1" colSpan="1" >`Bool`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >是否公开可见（`true`：是，`false`：否）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`isSeatEnabled`</td>

<td rowspan="1" colSpan="1" >`Bool`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >是否启用麦位功能（`true`：是，`false`：否）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`keepOwnerOnSeat`</td>

<td rowspan="1" colSpan="1" >`Bool`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >是否保持房主在麦位上。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`maxSeatCount`</td>

<td rowspan="1" colSpan="1" >`Int`</td>

<td rowspan="1" colSpan="1" >必填</td>

<td rowspan="1" colSpan="1" >最大麦位数量。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`seatMode`</td>

<td rowspan="1" colSpan="1" >`TakeSeatMode`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >上麦模式（`.free`：自由上麦，`.apply`：申请上麦）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`seatLayoutTemplateID`</td>

<td rowspan="1" colSpan="1" >`UInt`</td>

<td rowspan="1" colSpan="1" >必填</td>

<td rowspan="1" colSpan="1" >麦位布局模板 `ID。`</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`coverURL`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >直播间的封面图片地址。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`backgroundURL`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >直播间的背景图片地址。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`categoryList`</td>

<td rowspan="1" colSpan="1" >`[NSNumber]`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >直播间的分类标签列表。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`activityStatus`</td>

<td rowspan="1" colSpan="1" >`Int`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >直播活动状态。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`isGiftEnabled`</td>

<td rowspan="1" colSpan="1" >`Bool`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >是否启用礼物功能（`true`：是，`false`：否）。</td>
</tr>
</table>

4. **结束直播**


   直播结束后，主播可以调用 **LiveListStore** 的 `endLive` 接口结束直播。SDK 会处理停止推流和销毁房间的逻辑。

   ``` swift
   import AtomicXCore
   
   // YourAnchorViewController 代表您的主播开播视图控制器
   class YourAnchorViewController: UIViewController {
   
       // ... 其他代码 ...
   
       // 结束直播
       private func stopLive() {
           LiveListStore.shared.endLive { [weak self] result in
               guard let self = self else { return }
               switch result {
               case .success(let data):
                   debugPrint("endLive success")
               case .failure(let error):
                   debugPrint("endLive error: \(error.message)")
               }
           }
       }
   }
   ```

### 步骤2：实现观众进房观看

观众观看流程如下，通过简单几步操作，即可实现观众观看直播。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027182498/9ceb345ca66e11f0bf2352540044a08e.png)


> **提示：**
> 

> 观众进房拉流的业务代码，您也可以参考 TUILiveKit 开源项目中的 [TUILiveRoomAudienceViewController.swift](https://github.com/Tencent-RTC/TUIKit_iOS/blob/main/live/Sources/LiveStream/TUILiveRoomAudienceViewController.swift) 文件来了解完整的实现逻辑。
> 

1. **实现观众拉流页面**


   在您的观众视图控制器中，创建 `LiveCoreView` 实例，并将 `viewType` 指定为 `.playView`（拉流视图）。

   ``` swift
   import AtomicXCore
   
   // YourAudienceViewController 代表您的观众观看视图控制器
   class YourAudienceViewController: UIViewController {
      
       // 1. 初始化观众拉流页面
       private let coreView = LiveCoreView(viewType:.playView, frame: UIScreen.main.bounds)
       private let liveId: String
       
       public init(liveId: String) {
           self.liveId = liveId
           super.init(nibName: nil, bundle: nil)
           // 2. 绑定直播 id
           self.coreView.setLiveID(liveId)
       }
       
       required init?(coder: NSCoder) {
           fatalError("init(coder:) has not been implemented")
       }
       
       public override func viewDidLoad() {
           super.viewDidLoad()
           // 3. 将主播推流页面加载到您的视图上
           view.addSubview(coreView)
       }
   }  
   ```
2. **进入直播间观看**


   通过调用 **LiveListStore** 的 `joinLive` 接口加入直播，**您无需做额外操作，LiveCoreView 会自动播放当前房间的视频流**，完整示例代码如下：

   ``` swift
   import AtomicXCore
   
   // YourAudienceViewController 代表您的观众观看视图控制器
   class YourAudienceViewController: UIViewController {
       // ... 其他代码 ...
   
       public override func viewDidLoad() {
           super.viewDidLoad()
           // 3. 将主播推流页面加载到您的视图上
           view.addSubview(coreView)
   
           // 4. 进入直播间
           joinLive()
       }
   
       private func joinLive() {
            // 调用 LiveListStore.shared.joinLive 进入直播间
           // - liveId: 与主播开播同样的 liveId
           LiveListStore.shared.joinLive(liveID: liveId) { [weak self] result in
               guard let self = self else { return }
               switch result {
               case .success(let info):
                   debugPrint("joinLive success")
               case .failure(let error):
                   debugPrint("joinLive error \(error.message)")
                   // 进房失败，也需要退出页面
                   // self.dismiss(animated: true)
               }
           }
       }
   }
   ```
3. **退出直播**


   观众退出直播间时，需要调用 **LiveListStore** 的 `leaveLive` 接口退出直播。SDK 会自动停止拉流并退出房间。

   ``` swift
   import AtomicXCore
   
   // YourAudienceViewController 代表您的观众观看视图控制器
   class YourAudienceViewController: UIViewController {
   
       // ... 其他代码 ...
   
       // 退出直播
       private func leaveLive() {
           LiveListStore.shared.leaveLive { [weak self] result in
               guard let self = self else { return }
               switch result {
               case .success:
                   debugPrint("leaveLive success")
               case .failure(let error):
                   debugPrint("leaveLive error \(error.message)")
               }
           }
       }
   }
   ```

### 步骤3：监听直播事件

在观众加入直播间后，您还需要处理一些房间内的“被动”事件。例如，主播主动结束了直播，或者观众因为违规等原因被踢出房间。如果不监听这些事件，观众端 UI 可能会停留在黑屏页面，影响用户体验。

您可以通过订阅 `LiveListStore` 提供的 `liveListEventPublisher` 来实现事件监听。
``` swift
import AtomicXCore
import Combine // 1. 导入 Combine 框架

// YourAudienceViewController 代表您的观众观看视图控制器
class YourAudienceViewController: UIViewController {
   
    // ... 其他代码 (coreView, liveId, init, deinit, joinLive, leaveLive等) ...

    // 2. 定义 cancellableSet 来管理订阅生命周期
    private var cancellableSet: Set<AnyCancellable> = []
    
    public override func viewDidLoad() {
        super.viewDidLoad()
        view.addSubview(coreView)
        // 3. 监听直播事件
        setupLiveEventListener()
        // 4. 进入直播间
        joinLive()
    }

    // 5. 新增一个方法来设置事件监听
    private func setupLiveEventListener() {
        LiveListStore.shared.liveListEventPublisher
            .receive(on: RunLoop.main) // 确保在主线程处理 UI 更新
            .sink { [weak self] event in
                guard let self = self else { return }
                switch event {
                case .onLiveEnded(let liveID, let reason, let message):
                    // 监听到直播结束
                    debugPrint("Live ended. liveID: \(liveID), reason: \(reason.rawValue), message: \(message)")
                    // 在此处处理退出直播间的逻辑，例如关闭当前页面
                    // self.dismiss(animated: true)
                case .onKickedOutOfLive(let liveID, let reason, let message):
                    // 监听到被踢出直播
                    debugPrint("Kicked out of live. liveID: \(liveID), reason: \(reason.rawValue), message: \(message)")
                    // 在此处处理退出直播间的逻辑
                    // self.dismiss(animated: true)
                }
            }
            .store(in: &cancellableSet) // 管理订阅
    }
    
    // ... joinLive() 和 leaveLive() 方法 ...
}
```

### 运行效果

集成 **LiveCoreView** 后，您将得到一个纯净的视频渲染视图，它已具备完整的直播业务能力，但没有任何交互 UI。您可以参考下一章节 [丰富直播场景](https://write.woa.com/#82dbc44c-8a8e-40e2-89b9-66070f4beb72) 来完善直播场景。
<table>
<tr>
<td rowspan="1" colSpan="1" ></td>

<td rowspan="1" colSpan="1" >**动态宫格布局**</td>

<td rowspan="1" colSpan="1" >**浮动小窗布局**</td>

<td rowspan="1" colSpan="1" >**固定宫格布局**</td>

<td rowspan="1" colSpan="1" >**固定小窗布局**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**模板 ID**</td>

<td rowspan="1" colSpan="1" >600</td>

<td rowspan="1" colSpan="1" >601</td>

<td rowspan="1" colSpan="1" >800</td>

<td rowspan="1" colSpan="1" >801</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**描述**</td>

<td rowspan="1" colSpan="1" >默认布局，可根据连麦人数动态调整宫格大小。</td>

<td rowspan="1" colSpan="1" >连麦嘉宾以浮动小窗形式显示。</td>

<td rowspan="1" colSpan="1" >连麦人数固定，每个嘉宾占据一个固定宫格。</td>

<td rowspan="1" colSpan="1" >连麦人数固定，嘉宾以固定小窗形式显示。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**运行效果**</td>

<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027182498/394f3851a5b511f09936525400e889b2.png)</td>

<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027182498/395e0e3da5b511f0930a5254007c27c5.png)</td>

<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027182498/39427c02a5b511f0b1565254001c06ec.png)</td>

<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027182498/3942f453a5b511f091df5254005ef0f7.png)</td>
</tr>
</table>


## 丰富直播场景

当您完成了基础的直播功能后，您可以参考以下功能指南来为直播添加丰富的互动玩法。
<table>
<tr>
<td rowspan="1" colSpan="1" >**直播功能**</td>

<td rowspan="1" colSpan="1" >**功能介绍**</td>

<td rowspan="1" colSpan="1" >**功能 Stores**</td>

<td rowspan="1" colSpan="1" >**实现指南**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**实现观众音视频连线**</td>

<td rowspan="1" colSpan="1" >观众申请上麦，与主播进行实时视频互动。</td>

<td rowspan="1" colSpan="1" >[CoGuestStore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/cogueststore)</td>

<td rowspan="1" colSpan="1" >[实现观众连线](https://write.woa.com/document/191126698271952896)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**实现主播跨房连线 PK**</td>

<td rowspan="1" colSpan="1" >两个不同房间的主播进行连线，实现互动或 PK。</td>

<td rowspan="1" colSpan="1" >[CoHostStore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/cohoststore)<br>[BattleStore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/battlestore)</td>

<td rowspan="1" colSpan="1" >[实现主播连线 PK](https://write.woa.com/document/191126550284738560)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**添加弹幕聊天功能**</td>

<td rowspan="1" colSpan="1" >观众可以在直播间发送和接收实时文字消息。</td>

<td rowspan="1" colSpan="1" >[BarrageStore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/barragestore)</td>

<td rowspan="1" colSpan="1" >[实现弹幕功能](https://write.woa.com/document/191126786270978048)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**构建礼物赠送系统**</td>

<td rowspan="1" colSpan="1" >观众可以向主播赠送虚拟礼物，增加互动和趣味性。</td>

<td rowspan="1" colSpan="1" >[GiftStore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/giftstore)</td>

<td rowspan="1" colSpan="1" >[实现礼物功能](https://write.woa.com/document/191127003187093504)</td>
</tr>
</table>


## API 文档
<table>
<tr>
<td rowspan="1" colSpan="1" >**Store/Component**</td>

<td rowspan="1" colSpan="1" >**功能描述**</td>

<td rowspan="1" colSpan="1" >**API 文档**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**LiveCoreView**</td>

<td rowspan="1" colSpan="1" >直播视频流展示与交互的核心视图组件：负责视频流渲染和视图挂件处理，支持主播直播、观众连麦、主播连线等场景。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/livecoreview)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**LiveListStore**</td>

<td rowspan="1" colSpan="1" >直播间全生命周期管理：创建 / 加入 / 离开 / 销毁房间，查询房间列表，修改直播信息（名称、公告等），监听直播状态（如被踢出、结束）。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/liveliststore)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**DeviceStore**</td>

<td rowspan="1" colSpan="1" >音视频设备控制：麦克风（开关 / 音量）、摄像头（开关 / 切换 / 画质）、屏幕共享，设备状态实时监听。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/devicestore)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**CoGuestStore**</td>

<td rowspan="1" colSpan="1" >观众连麦管理：连麦申请 / 邀请 / 同意 / 拒绝，连麦成员权限控制（麦克风 / 摄像头），状态同步。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/cogueststore)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**CoHostStore**</td>

<td rowspan="1" colSpan="1" >主播跨房连线：支持多布局模板（动态网格等），发起 / 接受 / 拒绝连线，连麦主播互动管理。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/cohoststore)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**BattleStore**</td>

<td rowspan="1" colSpan="1" >主播 PK 对战：发起 PK（配置时长 / 对手），管理 PK 状态（开始 / 结束），同步分数，监听对战结果。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/battlestore)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**GiftStore**</td>

<td rowspan="1" colSpan="1" >礼物互动：获取礼物列表，发送 / 接收礼物，监听礼物事件（含发送者、礼物详情）。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/giftstore)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**BarrageStore**</td>

<td rowspan="1" colSpan="1" >弹幕功能：发送文本 / 自定义弹幕，维护弹幕列表，实时监听弹幕状态。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/barragestore)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**LikeStore**</td>

<td rowspan="1" colSpan="1" >点赞互动：发送点赞，监听点赞事件，同步总点赞数。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/likestore)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**LiveAudienceStore**</td>

<td rowspan="1" colSpan="1" >观众管理：获取实时观众列表（ID / 名称 / 头像），统计观众数量，监听观众进出事件。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/liveaudiencestore)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**AudioEffectStore**</td>

<td rowspan="1" colSpan="1" >音频特效：变声（童声 / 男声）、混响（KTV 等）、耳返调节，实时切换特效。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/audioeffectstore)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**BaseBeautyStore**</td>

<td rowspan="1" colSpan="1" >基础美颜：调节磨皮 / 美白 / 红润（0-100 级），重置美颜状态，同步效果参数。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/basebeautystore)</td>
</tr>
</table>


## 常见问题

### 主播调用 createLive 或 观众调用 joinLive 后为什么画面是黑的，没有视频画面？
- **检查 setLiveID**：请确保在调用开播或观看接口前，已经为 LiveCoreView 实例设置了正确的 liveID。

- **检查设备权限**：请确保 App 已获得摄像头和麦克风的系统使用权限。

- **检查主播端**：主播端是否正常调用 `DeviceStore.shared.openLocalCamera(isFront: true)` 打开了摄像头。

- **检查网络**：请检查设备网络连接是否正常。


### 主播端打开摄像头后，开播后可以看到本地视频预览画面，开播前视频预览是黑屏？
- **检查主播端**：请检查主播推流视图`LiveCoreView` 的 `viewType`是否配置为`.pushView`。

- **检查观众端**：请检查观众拉流视图`LiveCoreView` 的 `viewType`是否配置为 `.playView`。


### rsync 因权限不足导致依赖三方库资源拷贝失败

例如在使用 Xcode 集成 SnapKit 框架进行开发时，可能会遇到如下编译报错：
``` plaintext
rsync(xxxx):1:1: SnapKit.framework/SnapKit_Privacy.bundle/: mkpathat: Operation not permitted
```

#### 问题原因

Xcode 的用户**脚本沙盒机制**限制了构建过程中 `rsync` 脚本对 `SnapKit.framework` 资源文件的写入权限，导致框架内的 `SnapKit_Privacy.bundle` 无法正常拷贝。

#### 解决步骤
1. 关闭用户脚本沙盒后，打开 Xcode 项目，进入项目的 **Build Settings**，搜索 `User Script Sandboxing`（或标识 `ENABLE_USER_SCRIPT_SANDBOXING`），将其值从 `YES` 修改为 `NO`。

2. 清理并重新构建项目执行 **Product → Clean Build Folder** 清理项目缓存，然后重新编译运行即可。


