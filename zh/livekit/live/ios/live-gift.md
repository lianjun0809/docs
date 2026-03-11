> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

`GiftStore` 是 `AtomicXCore` 中专门负责管理直播间礼物功能的模块。通过它，您可以为您的直播应用构建一套完整的礼物系统，实现丰富的营收和互动场景。
<table>
<tr>
<td rowspan="1" colSpan="1" >礼物面板</td>

<td rowspan="1" colSpan="1" >弹幕礼物</td>

<td rowspan="1" colSpan="1" >全屏礼物</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027182498/b480dc47ae6f11f096c2525400454e06.jpeg)</td>

<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027182498/1363112bae7011f096c2525400454e06.png)</td>

<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027182498/b5caaab8ae6f11f0b08552540044a08e.gif)</td>
</tr>
</table>


## 核心功能
- **礼物列表获取**：从服务端拉取礼物面板所需的数据，包括礼物分类和礼物详情。

- **发送礼物**：观众可以向主播发送选定的礼物，并附带数量。

- **礼物事件广播**：实时接收房间内发生的礼物赠送事件，用于展示礼物动画和弹幕通知。


## 核心概念

在开始集成之前，我们先通过下表了解一下 `GiftStore` 相关的几个核心概念：
<table>
<tr>
<td rowspan="1" colSpan="1" >**核心概念**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**核心职责与描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`Gift`</td>

<td rowspan="1" colSpan="1" >`struct`</td>

<td rowspan="1" colSpan="1" >代表一个具体的礼物数据模型。包含了礼物的 ID、名称、图标地址、动画资源地址 (resourceURL) 和价格 (coins) 等。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`GiftCategory`</td>

<td rowspan="1" colSpan="1" >`struct`</td>

<td rowspan="1" colSpan="1" >代表一个礼物分类，例如“热门”、“豪华”等。它包含了分类的名称以及该分类下的 **Gift **列表。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`GiftState`</td>

<td rowspan="1" colSpan="1" >`struct`</td>

<td rowspan="1" colSpan="1" >代表礼物模块的当前状态。其核心属性 usableGifts 是一个 [GiftCategory] 数组，存储了从服务端拉取到的完整礼物列表。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`GiftEvent`</td>

<td rowspan="1" colSpan="1" >`enum`</td>

<td rowspan="1" colSpan="1" >代表直播间内发生的礼物事件。目前只有 .onReceiveGift，当有任何人（包括自己）发送礼物时，房间内所有人都会收到此事件。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`GiftStore`</td>

<td rowspan="1" colSpan="1" >`class`</td>

<td rowspan="1" colSpan="1" >这是与礼物功能交互的核心管理类。通过它，您可以拉取礼物列表、发送礼物，并通过订阅其 giftEventPublisher 来接收礼物事件。</td>
</tr>
</table>


## 实现步骤

### 步骤1：组件集成

> **说明：**
> 

> 使用**礼物系统**要求开通TUILiveKit **多人连麦版**、**大规模直播版**，不同套餐中可配置的礼物数量有所不同，详细参见 [功能与计费说明](https://write.woa.com/document/141302177829593088) 中的**礼物系统**说明。
> 

- **视频直播**：请参考 [快速接入](https://write.woa.com/document/191126382767431680) 集成 **AtomicXCore**，完成接入。

- **语聊房**：请参考 [快速接入](https://write.woa.com/document/192834898445422592) 集成 **AtomicXCore**，完成接入。


### 步骤2：初始化并监听礼物事件

获取 GiftStore 实例，并设置订阅者以接收礼物事件和礼物列表更新。

#### 实现方式:
1. **获取实例**：使用 `GiftStore.create(liveID:)` 获取与当前直播间绑定的 `GiftStore` 实例。

2. **订阅事件**：订阅 `giftStore.giftEventPublisher` 以接收 `.onReceiveGift `事件。

3. **订阅状态**：订阅 `giftStore.state` 以获取 `usableGifts `礼物列表。


#### 代码示例:
``` swift
import Foundation
import AtomicXCore 
import Combine     

class GiftManager {
    private let liveId: String
    private let giftStore: GiftStore
    private var cancellables = Set<AnyCancellable>()
    
    // 对外暴露礼物事件，方便UI层订阅以播放动画
    let giftEventPublisher = PassthroughSubject<GiftEvent, Never>()
    // 对外暴露礼物列表
    let giftListPublisher = CurrentValueSubject<[GiftCategory], Never>([])

    init(liveId: String) {
        self.liveId = liveId
        // 1. 通过 liveId 获取 GiftStore 的实例
        self.giftStore = GiftStore.create(liveID: liveId)
        
        subscribeToGiftState()
        subscribeToGiftEvents()
    }

    /// 2. 订阅礼物事件
    private func subscribeToGiftEvents() {
        giftStore.giftEventPublisher
            .receive(on: DispatchQueue.main)
            .sink { [weak self] event in
                // 收到事件后，将其转发给UI层处理
                self?.giftEventPublisher.send(event)
            }
            .store(in: &cancellables)
    }
    
    /// 3. 订阅礼物列表状态
    private func subscribeToGiftState() {
        giftStore.state
            .subscribe(StatePublisherSelector(keyPath: \GiftState.usableGifts))
            .receive(on: DispatchQueue.main)
            .assign(to: \.value, on: giftListPublisher)
            .store(in: &cancellables)
    }
}
```

#### 礼物列表结构体参数
- `GiftCategory`**参数说明**

<table>
<tr>
<td rowspan="1" colSpan="1" >**参数**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`categoryID`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >礼物分类的唯一 ID。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`name`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >礼物分类的显示名称。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`desc`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >礼物分类的描述信息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`extensionInfo`</td>

<td rowspan="1" colSpan="1" >`[String: String]`</td>

<td rowspan="1" colSpan="1" >扩展信息字段。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`giftList`</td>

<td rowspan="1" colSpan="1" >`[`[`Gift`](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/gift)`]`</td>

<td rowspan="1" colSpan="1" >该分类下包含的 Gift 礼物对象数组。</td>
</tr>
</table>

- `Gift`** 参数说明**

<table>
<tr>
<td rowspan="1" colSpan="1" >**参数**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`giftID`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >  礼物的唯一 ID。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`name`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >  礼物的显示名称。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`desc`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >  礼物的描述信息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`iconURL`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >  礼物图标 URL。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`resourceURL`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >  礼物动画资源 URL。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`level`</td>

<td rowspan="1" colSpan="1" >`UInt`</td>

<td rowspan="1" colSpan="1" >  礼物等级。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`coins`</td>

<td rowspan="1" colSpan="1" >`UInt`</td>

<td rowspan="1" colSpan="1" >  礼物价格。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`extensionInfo`</td>

<td rowspan="1" colSpan="1" >`[String: String]`</td>

<td rowspan="1" colSpan="1" >  扩展信息字段。</td>
</tr>
</table>


### 步骤3：获取礼物列表

调用 `refreshUsableGifts` 方法，从服务端拉取礼物数据。

#### 实现方式:
1. **调用接口**：在合适的时机（例如进入直播间后）调用 `giftStore.refreshUsableGifts(completion:)`。

2. **处理回调**：可选地处理 completion 回调以获知拉取结果。

3. **接收数据**：拉取成功后，通过步骤2中对 giftStore.state 的订阅，自动接收到更新后的 usableGifts 列表。


#### 代码示例:
``` swift
extension GiftManager {
    /// 从服务端刷新礼物列表
    func fetchGiftList() {
        giftStore.refreshUsableGifts { result in
            switch result {
            case .success:
                print("礼物列表拉取成功")
                // 成功后，数据会通过 state 订阅通道自动更新
            case .failure(let error):
                print("礼物列表拉取失败: \(error.localizedDescription)")
            }
        }
    }
}
```

### 步骤4：发送礼物

当用户在礼物面板选择一个礼物并点击发送时，调用 `sendGift` 接口将礼物发送出去。

#### 实现方式:
1. **获取参数**：从 UI 获取用户选择的 giftID 和发送数量 count。

2. **调用接口**：调用 `giftStore.sendGift(giftID:count:completion:)`。

3. **处理回调**：在 `completion` 回调中处理发送失败的情况（例如余额不足提示）；发送成功后的 UI 更新（动画、弹幕）应由 `.onReceiveGift` 事件驱动。


#### 代码示例:
``` swift
extension GiftManager {
    /// 用户发送一个礼物
    func sendGift(giftID: String, count: UInt) {
        giftStore.sendGift(giftID: giftID, count: count) { result in
            switch result {
            case .success:
                print("礼物 \(giftID) 发送成功")
                // 发送成功后，包括发送者在内的所有人都会收到 onReceiveGift 事件
            case .failure(let error):
                print("礼物发送失败: \(error.localizedDescription)")
                // 可以在此提示用户，例如“余额不足”或“网络错误”
            }
        }
    }
}
```

#### `sendGift`接口参数
<table>
<tr>
<td rowspan="1" colSpan="1" >**参数名**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`giftID`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >要发送的礼物的唯一 ID。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`count`</td>

<td rowspan="1" colSpan="1" >`UInt`</td>

<td rowspan="1" colSpan="1" >发送的数量。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`completion`</td>

<td rowspan="1" colSpan="1" >`CompletionClosure?`</td>

<td rowspan="1" colSpan="1" >发送完成后的回调。</td>
</tr>
</table>


## 功能进阶

`GiftStore` 的功能高度依赖于您的业务后台服务。本章将指导您如何通过服务端配置和客户端实现，构建功能丰富、体验卓越的礼物互动系统。

### **礼物素材配置**

您需要自定义直播间可用的礼物种类、分类、名称、图标、价格以及动画效果，以满足运营需求和品牌特色。

#### **实现方式 **
1. **服务端配置**：使用 LiveKit 服务端 REST API 管理礼物信息、分类、多语言等。请参考 [礼物配置指引文档](https://cloud.tencent.com/document/product/647/121321)。

2. **客户端拉取**：在客户端调用 `refreshUsableGifts` 获取配置数据。

3. **UI 展示**：使用拉取到的 `[GiftCategory]` 数据填充礼物面板。


#### **配置时序图**

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027182498/1a7376a1ae6e11f09b75525400bf7822.png)


#### **涉及 REST API 接口一览**
<table>
<tr>
<td rowspan="1" colSpan="1" >接口分类</td>

<td rowspan="1" colSpan="1" >接口</td>

<td rowspan="1" colSpan="1" >请求示例</td>
</tr>

<tr>
<td rowspan="3" colSpan="1" >​礼物管理​</td>

<td rowspan="1" colSpan="1" >添加礼物信息</td>

<td rowspan="1" colSpan="1" >[请求示例](https://write.woa.com/document/180341527570997248)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >删除礼物信息</td>

<td rowspan="1" colSpan="1" >[请求示例](https://write.woa.com/document/180341544133693440)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >查询礼物信息</td>

<td rowspan="1" colSpan="1" >[请求示例](https://write.woa.com/document/180341539054186496)</td>
</tr>

<tr>
<td rowspan="3" colSpan="1" >礼物​分类管理​</td>

<td rowspan="1" colSpan="1" >添加礼物分类信息</td>

<td rowspan="1" colSpan="1" >[请求示例](https://write.woa.com/document/180807825764642816)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >删除指定礼物分类信息</td>

<td rowspan="1" colSpan="1" >[请求示例](https://write.woa.com/document/180807830209925120)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >获取指定礼物分类信息</td>

<td rowspan="1" colSpan="1" >[请求示例](https://write.woa.com/document/180807827909746688)</td>
</tr>

<tr>
<td rowspan="3" colSpan="1" >​礼物关系管理​</td>

<td rowspan="1" colSpan="1" >添加指定礼物分类和礼物间的关系</td>

<td rowspan="1" colSpan="1" >[请求示例](https://write.woa.com/document/180341551420928000)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >删除指定礼物分类和礼物间的关系</td>

<td rowspan="1" colSpan="1" >[请求示例](https://write.woa.com/document/180341562381627392)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >获取指定礼物分类下的礼物关系</td>

<td rowspan="1" colSpan="1" >[请求示例](https://write.woa.com/document/180341571868094464)</td>
</tr>

<tr>
<td rowspan="6" colSpan="1" >​礼物多语言​管理</td>

<td rowspan="1" colSpan="1" >添加礼物多语言信息</td>

<td rowspan="1" colSpan="1" >[请求示例](https://write.woa.com/document/180341579611611136)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >删除指定礼物多语言信息</td>

<td rowspan="1" colSpan="1" >[请求示例](https://write.woa.com/document/180341598501920768)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >获取礼物多语言信息</td>

<td rowspan="1" colSpan="1" >[请求示例](https://write.woa.com/document/180341588810166272)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >添加礼物分类多语言信息</td>

<td rowspan="1" colSpan="1" >[请求示例](https://write.woa.com/document/180341603609534464)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >删除指定礼物分类多语言信息</td>

<td rowspan="1" colSpan="1" >[请求示例](https://write.woa.com/document/180341624911425536)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >获取礼物分类多语言信息</td>

<td rowspan="1" colSpan="1" >[请求示例](https://write.woa.com/document/180341612525645824)</td>
</tr>
</table>


### 计费与送礼扣费流程

当观众赠送礼物时，需要确保其账户余额充足，并完成实际的扣费操作，然后才能触发礼物特效的播放和广播。

#### 实现方式
1. **后台配置回调**：在 LiveKit 后台配置您的自建计费系统的回调 URL。参考 [回调配置文档](https://write.woa.com/document/183772947196690432)。

2. **客户端发送**：客户端调用 `sendGift`。

3. **后台交互**：LiveKit 后台调用您的回调 URL，您的计费系统执行扣费并返回结果。

4. **结果同步**：扣费成功，AtomicXCore 广播 `.onReceiveGift` 事件。扣费失败，`sendGift` 的 `completion` 收到错误。


#### 调用流程图

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027182498/8266a8afae6e11f0a68e5254001c06ec.png)


#### 涉及 REST API 接口一览
<table>
<tr>
<td rowspan="1" colSpan="1" >接口</td>

<td rowspan="1" colSpan="1" >说明</td>

<td rowspan="1" colSpan="1" >请求示例</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >回调配置 - 发送礼物之前回调</td>

<td rowspan="1" colSpan="1" >客户后台可以通过该回调决定是否通过送礼前校验等场景</td>

<td rowspan="1" colSpan="1" >[调用示例](https://write.woa.com/document/183772947196690432)</td>
</tr>
</table>


### 实现全屏礼物动画播放

当直播间有用户（包括自己）发送了“火箭”、“嘉年华”等豪华礼物时，全屏播放一个酷炫的礼物动画（例如 SVGA 动画），营造热烈的氛围。

#### 实现方式

`AtomicXCore` 本身不包含礼物动画播放器，您需要根据业务需求选择并集成第三方库。以下是两种方案的对比：
<table>
<tr>
<td rowspan="1" colSpan="1" >**对比项**</td>

<td rowspan="1" colSpan="1" >**基础方案 (SVGAPlayer-iOS)**</td>

<td rowspan="1" colSpan="1" >**高级方案 (TCEffectPlayerKit)**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >计费</td>

<td rowspan="1" colSpan="1" >免费 (开源库)</td>

<td rowspan="1" colSpan="1" >付费 (需购买 License)，请参见 [付费指引](https://cloud.tencent.com/document/product/616/116461)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >集成方式</td>

<td rowspan="1" colSpan="1" >需手动集成 SVGAPlayer 库 (例如通过 CocoaPods)</td>

<td rowspan="1" colSpan="1" >需额外集成 TCEffectPlayerKit 并进行鉴权</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >动画格式支持</td>

<td rowspan="1" colSpan="1" >仅支持 SVGA</td>

<td rowspan="1" colSpan="1" >SVGA、PAG、WebP、Lottie、MP4 等多种格式</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >性能</td>

<td rowspan="1" colSpan="1" >建议 SVGA 文件 ≤ 10MB</td>

<td rowspan="1" colSpan="1" >支持更大的动画文件，复杂特效/多动画并发/低端机表现更优</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >推荐场景</td>

<td rowspan="1" colSpan="1" >礼物动画格式统一为 SVGA，且文件大小可控</td>

<td rowspan="1" colSpan="1" >需要支持多种动画格式，或对动画性能/设备兼容性有更高要求</td>
</tr>
</table>


本章节主要演示基础方案的集成。如果您选择高级方案，请参考 [TCEffectPlayer 集成指引](https://cloud.tencent.com/document/product/616/116474)。

#### 基础方案实现：使用 SVGAPlayer
1. **集成 SVGAPlayer**：在您的 `Podfile` 文件中，添加 `SVGAPlayer` 的依赖并在终端中运行`pod install`。

   ``` ruby
   target 'YourApp' do
     # ... other pods
     pod 'SVGAPlayer'
   end
   ```
2. **监听礼物事件**：订阅 `GiftStore` 的 `giftEventPublisher`。

3. **解析并播放**：当收到 `.onReceiveGift `事件时，检查 `gift.resourceURL `是否有效且指向一个 SVGA 文件。如果是，则使用 `SVGAParser` 解析 URL，并将解析后的 `SVGAVideoEntity` 交给 `SVGAPlayer` 实例播放。


#### 代码示例
``` swift
import UIKit
import AtomicXCore 
import Combine
import SVGAPlayer // 1. 导入

class LiveRoomViewController: UIViewController, SVGAPlayerDelegate {
    private var giftManager: GiftManager!
    private var cancellables = Set<AnyCancellable>()
    private let svgaPlayer = SVGAPlayer() // 2. 准备实例
    private let svgaParser = SVGAParser()

    override func viewDidLoad() {
        super.viewDidLoad()
        setupSVGAPlayer()
    }

    private func setupSVGAPlayer() {
        svgaPlayer.delegate = self
        svgaPlayer.loops = 1 // 默认播放1次
        svgaPlayer.clearsAfterStop = true // 播放完毕后自动清除
        view.addSubview(svgaPlayer)
        svgaPlayer.frame = view.bounds // 默认全屏
        svgaPlayer.isHidden = true
    }

    func setupGiftSubscription(liveId: String) {
        self.giftManager = GiftManager(liveId: liveId)

        giftManager.giftEventPublisher
            .sink { [weak self] event in // 3. 监听事件
                guard case .onReceiveGift(_, let gift, _, _) = event else { return }

                if !gift.resourceURL.isEmpty, let url = URL(string: gift.resourceURL) { // 4. 解析播放
                    self?.playAnimation(from: url)
                }
            }
            .store(in: &cancellables)
    }

    private func playAnimation(from url: URL) {
        svgaParser.parse(with: url, completionBlock: { [weak self] videoItem in
            guard let self = self, let videoItem = videoItem else { return }
            DispatchQueue.main.async {
                self.svgaPlayer.videoItem = videoItem
                self.svgaPlayer.isHidden = false
                self.svgaPlayer.startAnimation()
            }
        }, failureBlock: { error in
            print("SVGA 动画解析失败: \(error?.localizedDescription ?? "unknown error")")
            // 可以在此添加失败重试或上报逻辑
        })
    }

    func svgaPlayerDidFinishedAnimation(_ player: SVGAPlayer!) { /* ... 播放结束处理 ... */ }
}
```

### 在弹幕区展示礼物赠送消息

当有用户发送礼物时，不仅播放动画，同时在公屏弹幕区域显示一条系统消息，例如：“【观众昵称】送出了【礼物名称】x【数量】”，让所有观众都能看到。

#### 实现方式
1. **监听事件**：订阅 `giftStore.giftEventPublisher`。

2. **获取信息**：收到 `.onReceiveGift` 事件后，提取发送者 sender、礼物 gift 和数量 count。

3. **获取弹幕 Store**：使用 `BarrageStore.create(liveID:) `获取与当前房间绑定的实例。

4. **拼接消息**：创建一条 `Barrage` 结构体，设置 `messageType = .text`，textContent 为拼接好的字符串（例如 “[`sender.userName`] 送出了 [`gift.name`] x [`count`]”）。

5. **本地插入**：调用 `barrageStore.appendLocalTip(message: giftTip) `将消息插入本地列表。


#### 代码示例
``` swift
// 在 LiveRoomManager 或类似的顶层管理器中
private func setupGiftToBarrageFlow() {
    giftStore.giftEventPublisher
        .receive(on: DispatchQueue.main)
        .sink { [weak self] event in // 1. 监听事件
            guard case .onReceiveGift(_, let gift, let count, let sender) = event else { return } // 2. 获取信息

            guard let self = self else { return }
            // 3. 获取弹幕Store (假设 barrageStore 已初始化)

            // 4. 拼接消息
            let tipText = "\(sender.userName) 送出了 \(gift.name) x \(count)"
            var giftTip = Barrage()
            giftTip.messageType = .text 
            giftTip.textContent = tipText
            // 可选：设置一个特殊的sender

            // 5. 本地插入
            self.barrageStore.appendLocalTip(message: giftTip)
        }
        .store(in: &cancellables)
}
```

## API 文档

关于 [GiftStore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/cohoststore) 及其相关类的所有公开接口、属性和方法的详细信息，请参阅随 [AtomicXCore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore) 框架的官方 API 文档。本指南使用到的相关 Store 如下：
<table>
<tr>
<td rowspan="1" colSpan="1" >Store/Component</td>

<td rowspan="1" colSpan="1" >功能描述</td>

<td rowspan="1" colSpan="1" >API 文档</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GiftStore</td>

<td rowspan="1" colSpan="1" >礼物互动：获取礼物列表，发送 / 接收礼物，监听礼物事件（含发送者、礼物详情）。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/giftstore)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >BarrageStore</td>

<td rowspan="1" colSpan="1" >弹幕功能：发送文本 / 自定义弹幕，维护弹幕列表，实时监听弹幕状态。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/barragestore)</td>
</tr>
</table>


## 常见问题

### `GiftStore` 的礼物列表是空的，我该怎么办？

您必须主动调用 `refreshUsableGifts(completion:)`来从您的业务后台拉取礼物数据。这些礼物数据需要在您的业务后台通过服务端 REST API 进行配置。

### 如何实现礼物的多语言展示（例如中文、英文）？

`GiftStore` 提供了 `setLanguage(_ language: String)`接口。您可以在 `refreshUsableGifts` 之前调用此方法，传入目标语言代码（例如 "en" 或 "zh-CN"）。服务端会根据此语言代码，返回对应语言的礼物名称和描述。

### 我调用 sendGift 发送了礼物，礼物动画为什么重复播放了两次？

`onReceiveGift` 事件是对房间内所有成员的广播（包括发送者自己）。如果您在 `sendGift` 的 `completion` 成功回调里执行了一次UI操作，同时又在 `onReceiveGift` 订阅中执行了相同的 UI 操作，就会造成重复。
- **实践教程**：UI 的更新（例如播放动画、弹幕提示）只在 `onReceiveGift` 事件的订阅中处理。`sendGift` 的 `completion`回调仅用于处理发送失败的逻辑（例如提示用户“发送失败”或“余额不足”）。


### 礼物扣费逻辑在哪里实现？

礼物扣费逻辑完全由您的自建计费系统负责。`AtomicXCore` 通过后台回调机制与您的计费系统对接。客户端调用 `sendGift` 触发回调，您的后台服务完成扣费后，将结果返回给 `AtomicXCore` 后台，从而决定礼物事件是否广播。

### 送礼通知会被禁言或频控拦截吗？

不会。送礼通知（`.onReceiveGift` 事件）不受禁言或消息频控影响，确保可靠投递。

### 礼物动画播放卡顿怎么办？

请检查您的 SVGA 文件大小，基础播放器建议不要超过 10MB。如果文件过大或动画复杂，您可以考虑集成 TUILiveKit 提供的高级特效播放器，以获得更优的性能表现。