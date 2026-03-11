> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

`GiftStore` 是 `AtomicXCore` 中专门负责管理直播间礼物功能的模块。通过它，您可以为您的直播应用构建一套完整的礼物系统，实现丰富的营收和互动场景。
<table>
<tr>
<td rowspan="1" colSpan="1" >礼物面板</td>

<td rowspan="1" colSpan="1" >弹幕礼物</td>

<td rowspan="1" colSpan="1" >全屏礼物</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027182232/bd3a817eb63f11f0a808525400bf7822.png)</td>

<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027182232/c1a5bdebb63f11f0b4c35254001c06ec.png)</td>

<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027182232/c68b79e4b63f11f0a6c652540044a08e.png)</td>
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

<td rowspan="1" colSpan="1" >`data class`</td>

<td rowspan="1" colSpan="1" >代表一个具体的礼物数据模型。包含了礼物的 ID、名称、图标地址、动画资源地址 (resourceURL) 和价格 (coins) 等。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`GiftCategory`</td>

<td rowspan="1" colSpan="1" >`data class`</td>

<td rowspan="1" colSpan="1" >代表一个礼物分类，例如“热门”、“豪华”等。它包含了分类的名称以及该分类下的 **Gift** 列表。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`GiftState`</td>

<td rowspan="1" colSpan="1" >`data class`</td>

<td rowspan="1" colSpan="1" >代表礼物模块的当前状态。其核心属性 usableGifts 是一个 `StateFlow`，存储了从服务端拉取到的完整礼物列表。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`GiftEvent`</td>

<td rowspan="1" colSpan="1" >`abstract class`</td>

<td rowspan="1" colSpan="1" >代表直播间内发生的礼物事件监听器。目前只有 onReceiveGift，当有任何人（包括自己）发送礼物时，房间内所有人都会收到此事件。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`GiftStore`</td>

<td rowspan="1" colSpan="1" >`abstract class`</td>

<td rowspan="1" colSpan="1" >这是与礼物功能交互的核心管理类。通过它，您可以拉取礼物列表、发送礼物，并通过添加监听器来接收礼物事件。</td>
</tr>
</table>


## 实现步骤

### 步骤1：组件集成

> **说明：**
> 

> 使用**礼物系统**要求开通TUILiveKit **多人连麦版**、**大规模直播版**，不同套餐中可配置的礼物数量有所不同，详细参见 [功能与计费说明](https://write.woa.com/document/141302177829593088) 中的**礼物系统**说明。
> 

- **视频直播**：请参考 [快速接入](https://write.woa.com/document/191126372105478144) 集成 **AtomicXCore**，完成接入。

- **语聊房**：请参考 [快速接入](https://write.woa.com/document/192834878686547968) 集成 **AtomicXCore**，完成接入。


### 步骤2：初始化并监听礼物事件

获取 GiftStore 实例，并设置监听器以接收礼物事件和礼物列表更新。

#### 实现方式:
1. **获取实例**：使用 `GiftStore.create(liveID)` 获取与当前直播间绑定的 `GiftStore` 实例。

2. **添加监听器**：添加 `GiftListener` 以接收 `onReceiveGift` 事件。

3. **订阅状态**：订阅 `giftStore.giftState.usableGifts` 以获取礼物列表。


#### 代码示例:
``` kotlin
import io.trtc.tuikit.atomicxcore.api.gift.Gift
import io.trtc.tuikit.atomicxcore.api.gift.GiftCategory
import io.trtc.tuikit.atomicxcore.api.gift.GiftListener
import io.trtc.tuikit.atomicxcore.api.gift.GiftStore
import io.trtc.tuikit.atomicxcore.api.live.LiveUserInfo
import kotlinx.coroutines.flow.StateFlow
import kotlinx.coroutines.flow.MutableStateFlow
import kotlinx.coroutines.flow.asStateFlow
import kotlinx.coroutines.CoroutineScope
import kotlinx.coroutines.Dispatchers
import kotlinx.coroutines.launch

class GiftManager(
    private val liveId: String
) {
    private val giftStore: GiftStore = GiftStore.create(liveId)
    private val coroutineScope = CoroutineScope(Dispatchers.Main)
    // 对外暴露礼物列表
    private val _giftList = MutableStateFlow<List<GiftCategory>>(emptyList())
    val giftList: StateFlow<List<GiftCategory>> = _giftList.asStateFlow()

    init {
        setupGiftListener()
        subscribeToGiftState()
    }

    /// 2. 订阅礼物事件
    private fun setupGiftListener() {
        giftStore.addGiftListener(object : GiftListener() {
            override fun onReceiveGift(liveID: String, gift: Gift, count: Int, sender: LiveUserInfo) {
                // 收到事件后，将其转发给UI层处理
            }
        })
    }

    /// 3. 订阅礼物列表状态
    private fun subscribeToGiftState() {
        coroutineScope.launch(Dispatchers.Main) {
            giftStore.giftState.usableGifts.collect { giftList ->
                // 仅在列表内容变化时才更新
                _giftList.value = giftList
            }
        }
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

<td rowspan="1" colSpan="1" >`Map<String, String>`</td>

<td rowspan="1" colSpan="1" >扩展信息字段。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`giftList`</td>

<td rowspan="1" colSpan="1" >`List`</td>

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

<td rowspan="1" colSpan="1" >`Long`</td>

<td rowspan="1" colSpan="1" >  礼物等级。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`coins`</td>

<td rowspan="1" colSpan="1" >`Long`</td>

<td rowspan="1" colSpan="1" >  礼物价格。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`extensionInfo`</td>

<td rowspan="1" colSpan="1" >`Map<String, String>`</td>

<td rowspan="1" colSpan="1" >  扩展信息字段。</td>
</tr>
</table>


### 步骤3：获取礼物列表

调用 `refreshUsableGifts` 方法，从服务端拉取礼物数据。

#### 实现方式:
1. **调用接口**：在合适的时机（如进入直播间后）调用 `giftStore.refreshUsableGifts()`。

2. **处理回调**：可选地处理 completion 回调以获知拉取结果。

3. **接收数据**：拉取成功后，通过步骤2中对 giftStore.giftState.usableGifts 的订阅，自动接收到更新后的 usableGifts 列表。


#### 代码示例:
``` kotlin
class GiftManager(
    private val liveId: String
) {
    private val giftStore: GiftStore = GiftStore.create(liveId)

    /// 从服务端刷新礼物列表
    fun fetchGiftList() {
        giftStore.refreshUsableGifts(object : CompletionHandler {
            override fun onSuccess() {
                println("礼物列表拉取成功")
                // 成功后，数据会通过 giftState 订阅通道自动更新
            }

            override fun onFailure(code: Int, desc: String) {
                println("礼物列表拉取失败: $desc")
            }
        })
    }
}
```

### 步骤4：发送礼物

当用户在礼物面板选择一个礼物并点击发送时，调用 `sendGift` 接口将礼物发送出去。

#### 实现方式:
1. **获取参数**：从UI获取用户选择的 giftID 和发送数量 count。

2. **调用接口**：调用 `giftStore.sendGift(giftID, count, completion)`。

3. **处理回调**：在 `completion` 回调中处理发送失败的情况（例如余额不足提示）；发送成功后的 UI 更新（动画、弹幕）应由 `onReceiveGift` 事件驱动。


#### 代码示例:
``` kotlin
class GiftManager(
    private val liveId: String
) {
    private val giftStore: GiftStore = GiftStore.create(liveId)

    /// 用户发送一个礼物
    fun sendGift(giftID: String, count: Int) {
        giftStore.sendGift(giftID, count, object : CompletionHandler {
            override fun onSuccess() {
                println("礼物 $giftID 发送成功")
                // 发送成功后，包括发送者在内的所有人都会收到 onReceiveGift 事件
            }

            override fun onFailure(code: Int, desc: String) {
                println("礼物发送失败: $desc")
                // 可以在此提示用户，例如"余额不足"或"网络错误"
            }
        })
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

<td rowspan="1" colSpan="1" >`Int`</td>

<td rowspan="1" colSpan="1" >发送的数量。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`completion`</td>

<td rowspan="1" colSpan="1" >`CompletionHandler?`</td>

<td rowspan="1" colSpan="1" >发送完成后的回调。</td>
</tr>
</table>


## 功能进阶

`GiftStore` 的功能高度依赖于您的业务后台服务。本章将指导您如何通过服务端配置和客户端实现，构建功能丰富、体验卓越的礼物互动系统。

### **礼物素材配置**

您需要自定义直播间可用的礼物种类、分类、名称、图标、价格以及动画效果，以满足运营需求和品牌特色。

#### 实现方式 
1. **服务端配置**：使用 LiveKit 服务端 REST API 管理礼物信息、分类、多语言等。请参考 [礼物配置指引文档](https://cloud.tencent.com/document/product/647/121321)。

2. **客户端拉取**：在客户端调用 `refreshUsableGifts` 获取配置数据。

3. **UI 展示**：使用拉取到的 `List<GiftCategory>` 数据填充礼物面板。


#### **配置时序图**

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032603567/374c3d5dafec11f0b28a5254005ef0f7.png)


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

4. **结果同步**：扣费成功，AtomicXCore 广播 `onReceiveGift` 事件；扣费失败，`sendGift` 的 `completion` 收到错误。


#### 调用流程图

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032603567/62699205afec11f0b707525400bf7822.png)


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

当直播间有用户（包括自己）发送了"火箭"、"嘉年华"等豪华礼物时，全屏播放一个酷炫的礼物动画（例如 SVGA 动画），营造热烈的氛围。

#### 实现方式

`AtomicXCore` 本身不包含礼物动画播放器，您需要根据业务需求选择并集成第三方库。以下是两种方案的对比：
<table>
<tr>
<td rowspan="1" colSpan="1" >**对比项**</td>

<td rowspan="1" colSpan="1" >**基础方案 (SVGAPlayer-Android)**</td>

<td rowspan="1" colSpan="1" >**高级方案 (TCEffectPlayerKit)**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >计费</td>

<td rowspan="1" colSpan="1" >免费 (开源库)</td>

<td rowspan="1" colSpan="1" >付费 (需购买 License)，请参见 [付费指引](https://cloud.tencent.com/document/product/616/116461)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >集成方式</td>

<td rowspan="1" colSpan="1" >需手动集成 SVGAPlayer 库 (例如通过 Gradle)</td>

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


本章节主要演示基础方案的集成。如果您选择高级方案，请参见 [TCEffectPlayer 集成指引](https://cloud.tencent.com/document/product/616/116472)。

#### 基础方案实现：使用 SVGAPlayer
1. **集成 SVGAPlayer**: 在您的 `build.gradle` 文件中，添加 `SVGAPlayer` 的依赖并同步项目。

   ``` gradle
   dependencies {
       // ... other dependencies
       implementation 'com.github.yyued:SVGAPlayer-Android:2.6.1'
   }
   ```
2. **监听礼物事件**: 订阅 `GiftStore` 的 `GiftListener`。

3. **解析并播放**: 当收到 `onReceiveGift` 事件时，检查 `gift.resourceURL` 是否有效且指向一个 SVGA 文件。如果是，则使用 `SVGAParser` 解析 URL，并将解析后的 `SVGAVideoEntity` 交给 `SVGAPlayer` 实例播放。


#### 代码示例
``` kotlin
import android.os.Bundle
import androidx.appcompat.app.AppCompatActivity
import com.opensource.svgaplayer.SVGACallback
import com.opensource.svgaplayer.SVGAParser
import com.opensource.svgaplayer.SVGAVideoEntity
import com.opensource.svgaplayer.SVGAImageView
import io.trtc.tuikit.atomicxcore.api.gift.Gift
import io.trtc.tuikit.atomicxcore.api.gift.GiftListener
import io.trtc.tuikit.atomicxcore.api.gift.GiftStore
import io.trtc.tuikit.atomicxcore.api.live.LiveUserInfo
import java.net.URL

class LiveRoomActivity : AppCompatActivity() {
    private lateinit var giftStore: GiftStore
    private lateinit var svgaImageView: SVGAImageView
    private lateinit var svgaParser: SVGAParser

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_live_room)
        setupSVGAPlayer()
    }

    private fun setupSVGAPlayer() {
        svgaImageView = findViewById(R.id.svga_player)
        svgaParser = SVGAParser(this)
        svgaImageView.visibility = android.view.View.GONE
        
        // 设置礼物播放次数为一次
        svgaImageView.loops = 1
        
        // 设置播放完成回调，用于隐藏和清理
        svgaImageView.callback = object : SVGACallback {
            override fun onFinished() {
                svgaImageView.visibility = android.view.View.GONE
                svgaImageView.clear()
            }
            override fun onPause() {}
            override fun onRepeat() {}
            override fun onStep(frame: Int, percentage: Double) {}
        }
    }

    fun setupGiftSubscription(liveId: String) {
        giftStore = GiftStore.create(liveId)

        giftStore.addGiftListener(object : GiftListener() {
            override fun onReceiveGift(liveID: String, gift: Gift, count: Int, sender: LiveUserInfo) {
                if (gift.resourceURL.isNotEmpty()) {
                    try {
                        val url = URL(gift.resourceURL)
                        playAnimation(url)
                    } catch (e: Exception) {
                        println("无效的动画URL: ${gift.resourceURL}")
                    }
                }
            }
        })
    }
    
    private fun playAnimation(url: URL) {
        // 4. 解析播放
        svgaParser.decodeFromURL(url, object : SVGAParser.ParseCompletion {
            override fun onComplete(videoItem: SVGAVideoEntity) {
                runOnUiThread {
                    svgaImageView.setVideoItem(videoItem)
                    svgaImageView.visibility = android.view.View.VISIBLE
                    svgaImageView.startAnimation()
                }
            }
            
            override fun onError() {
                println("SVGA 动画解析失败")
                // 可以在此添加失败重试或上报逻辑
            }
        })
    }
}
```

### 在弹幕区展示礼物赠送消息

当有用户发送礼物时，不仅播放动画，同时在公屏弹幕区域显示一条系统消息，例如：“【观众昵称】送出了【礼物名称】x【数量】”，让所有观众都能看到。

#### 实现方式
1. **监听事件**：订阅 `giftStore` 的 `GiftListener`。

2. **获取信息**：收到 `onReceiveGift` 事件后，提取发送者 sender、礼物 gift 和数量 count。

3. **获取弹幕 Store**：使用 `BarrageStore.create(liveID)` 获取与当前房间绑定的实例。

4. **拼接消息**：创建一条 `Barrage` 结构体，设置 `messageType = BarrageType.TEXT`，textContent 为拼接好的字符串（例如 “[`sender.userName`] 送出了 [`gift.name`] x [`count`]”）。

5. **本地插入**：调用 `barrageStore.appendLocalTip(message: giftTip)` 将消息插入本地列表。


#### 代码示例
``` kotlin
import io.trtc.tuikit.atomicxcore.api.barrage.Barrage
import io.trtc.tuikit.atomicxcore.api.barrage.BarrageStore
import io.trtc.tuikit.atomicxcore.api.barrage.BarrageType
import io.trtc.tuikit.atomicxcore.api.gift.Gift
import io.trtc.tuikit.atomicxcore.api.gift.GiftListener
import io.trtc.tuikit.atomicxcore.api.gift.GiftStore
import io.trtc.tuikit.atomicxcore.api.live.LiveUserInfo

// 在 LiveRoomManager 或类似的顶层管理器中
class LiveRoomManager(
    private val liveId: String
) {
    private val giftStore: GiftStore = GiftStore.create(liveId)
    private val barrageStore: BarrageStore = BarrageStore.create(liveId)

    private fun setupGiftToBarrageFlow() {
        giftStore.addGiftListener(object : GiftListener() {
            override fun onReceiveGift(liveID: String, gift: Gift, count: Int, sender: LiveUserInfo) {
                // 1. 监听事件 2. 获取信息

                // 4. 拼接消息
                val tipText = "送出了 ${gift.name} x $count"
                val giftTip = Barrage(
                    liveID = liveID,
                    messageType = BarrageType.TEXT,
                    textContent = tipText
                    sender = sender
                )

                // 5. 本地插入
                barrageStore.appendLocalTip(giftTip)
            }
        })
    }
}
```

## API 文档

关于 [GiftStore](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.gift/-gift-store/index.html) 及其相关类的所有公开接口、属性和方法的详细信息，请参阅随 [AtomicXCore](https://tencent-rtc.github.io/TUIKit_Android/index.html) 框架的官方 API 文档。本指南使用到的相关 Store 如下：
<table>
<tr>
<td rowspan="1" colSpan="1" >Store/Component</td>

<td rowspan="1" colSpan="1" >功能描述</td>

<td rowspan="1" colSpan="1" >API 文档</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GiftStore</td>

<td rowspan="1" colSpan="1" >礼物互动：获取礼物列表，发送 / 接收礼物，监听礼物事件（含发送者、礼物详情）。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.gift/-gift-store/index.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >BarrageStore</td>

<td rowspan="1" colSpan="1" >弹幕功能：发送文本 / 自定义弹幕，维护弹幕列表，实时监听弹幕状态。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.barrage/-barrage-store/index.html)</td>
</tr>
</table>


## 常见问题

### `GiftStore` 的礼物列表是空的，我该怎么办？

您必须主动调用 `refreshUsableGifts(completion)`来从您的业务后台拉取礼物数据。这些礼物数据需要在您的业务后台通过服务端 REST API 进行配置。

### 如何实现礼物的多语言展示（例如中文、英文）？

`GiftStore` 提供了 `setLanguage(language: String)`接口。您可以在 `refreshUsableGifts` 之前调用此方法，传入目标语言代码（例如 "en" 或 "zh-CN"）。服务端会根据此语言代码，返回对应语言的礼物名称和描述。

### 我调用 sendGift 发送了礼物，礼物动画为什么重复播放了两次？

`onReceiveGift` 事件是对房间内所有成员的广播（包括发送者自己）。如果您在 `sendGift` 的 `completion` 成功回调里执行了一次UI操作，同时又在 `onReceiveGift` 订阅中执行了相同的UI操作，就会造成重复。
- **实践教程**：UI 的更新（例如播放动画、弹幕提示）只在 `onReceiveGift` 事件的订阅中处理。`sendGift` 的 `completion`回调仅用于处理发送失败的逻辑（例如提示用户"发送失败"或"余额不足"）。


### 礼物扣费逻辑在哪里实现？

礼物扣费逻辑完全由您的自建计费系统负责。`AtomicXCore` 通过后台回调机制与您的计费系统对接。客户端调用 `sendGift` 触发回调，您的后台服务完成扣费后，将结果返回给 `AtomicXCore` 后台，从而决定礼物事件是否广播。

### 送礼通知会被禁言或频控拦截吗？

不会。送礼通知（`onReceiveGift` 事件）不受禁言或消息频控影响，确保可靠投递。

### 礼物动画播放卡顿怎么办？

请检查您的 SVGA 文件大小，基础播放器建议不要超过 10MB。如果文件过大或动画复杂，您可以考虑集成 TUILiveKit 提供的高级特效播放器，以获得更优的性能表现。