> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

`GiftStore` 是 `AtomicXCore` 中专门负责管理直播间礼物功能的模块。通过它，您可以为您的直播应用构建一套完整的礼物系统，实现丰富的营收和互动场景。
| 礼物面板 | 弹幕礼物 | 全屏礼物 |
| --- | --- | --- |
|  |  |  |

## 核心功能
- **礼物列表获取**：从服务端拉取礼物面板所需的数据，包括礼物分类和礼物详情。

- **发送礼物**：观众可以向主播发送选定的礼物，并附带数量。

- **礼物事件广播**：实时接收房间内发生的礼物赠送事件，用于展示礼物动画和弹幕通知。

## 核心概念

在开始集成之前，我们先通过下表了解一下 `GiftStore` 相关的几个核心概念：
| **核心概念** | **类型** | **核心职责与描述** |
| --- | --- | --- |
| `Gift` | `data class` | 代表一个具体的礼物数据模型。包含了礼物的 ID、名称、图标地址、动画资源地址 (resourceURL) 和价格 (coins) 等。 |
| `GiftCategory` | `data class` | 代表一个礼物分类，例如“热门”、“豪华”等。它包含了分类的名称以及该分类下的 **Gift** 列表。 |
| `GiftState` | `data class` | 代表礼物模块的当前状态。其核心属性 usableGifts 是一个 `StateFlow`，存储了从服务端拉取到的完整礼物列表。 |
| `GiftEvent` | `abstract class` | 代表直播间内发生的礼物事件监听器。目前只有 onReceiveGift，当有任何人（包括自己）发送礼物时，房间内所有人都会收到此事件。 |
| `GiftStore` | `abstract class` | 这是与礼物功能交互的核心管理类。通过它，您可以拉取礼物列表、发送礼物，并通过添加监听器来接收礼物事件。 |

## 实现步骤

### 步骤1：组件集成

> **说明：**
> 

> 使用**礼物系统**要求开通TUILiveKit **多人连麦版**、**大规模直播版**，不同套餐中可配置的礼物数量有所不同，详细参见 功能与计费说明 中的**礼物系统**说明。
> 

- **视频直播**：请参考 快速接入 集成 **AtomicXCore**，完成接入。

- **语聊房**：请参考 快速接入 集成 **AtomicXCore**，完成接入。

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

| **参数** | **类型** | **描述** |
| --- | --- | --- |
| `categoryID` | `String` | 礼物分类的唯一 ID。 |
| `name` | `String` | 礼物分类的显示名称。 |
| `desc` | `String` | 礼物分类的描述信息。 |
| `extensionInfo` | `Map<String, String>` | 扩展信息字段。 |
| `giftList` | `List` | 该分类下包含的 Gift 礼物对象数组。 |

- `Gift`** 参数说明**

| **参数** | **类型** | **描述** |
| --- | --- | --- |
| `giftID` | `String` | 礼物的唯一 ID。 |
| `name` | `String` | 礼物的显示名称。 |
| `desc` | `String` | 礼物的描述信息。 |
| `iconURL` | `String` | 礼物图标 URL。 |
| `resourceURL` | `String` | 礼物动画资源 URL。 |
| `level` | `Long` | 礼物等级。 |
| `coins` | `Long` | 礼物价格。 |
| `extensionInfo` | `Map<String, String>` | 扩展信息字段。 |

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
| **参数名** | **类型** | **描述** |
| --- | --- | --- |
| `giftID` | `String` | 要发送的礼物的唯一 ID。 |
| `count` | `Int` | 发送的数量。 |
| `completion` | `CompletionHandler?` | 发送完成后的回调。 |

## 功能进阶

`GiftStore` 的功能高度依赖于您的业务后台服务。本章将指导您如何通过服务端配置和客户端实现，构建功能丰富、体验卓越的礼物互动系统。

### **礼物素材配置**

您需要自定义直播间可用的礼物种类、分类、名称、图标、价格以及动画效果，以满足运营需求和品牌特色。

#### 实现方式 
1. **服务端配置**：使用 LiveKit 服务端 REST API 管理礼物信息、分类、多语言等。请参考 [礼物配置指引文档](https://cloud.tencent.com/document/product/647/121321)。

2. **客户端拉取**：在客户端调用 `refreshUsableGifts` 获取配置数据。

3. **UI 展示**：使用拉取到的 `List<GiftCategory>` 数据填充礼物面板。

#### **配置时序图**

#### **涉及 REST API 接口一览**
| 接口分类 | 接口 | 请求示例 |
| --- | --- | --- |
| ​礼物管理​ | 添加礼物信息 | 请求示例 |
| 删除礼物信息 | 请求示例 |  |
| 查询礼物信息 | 请求示例 |  |
| 礼物​分类管理​ | 添加礼物分类信息 | 请求示例 |
| 删除指定礼物分类信息 | 请求示例 |  |
| 获取指定礼物分类信息 | 请求示例 |  |
| ​礼物关系管理​ | 添加指定礼物分类和礼物间的关系 | 请求示例 |
| 删除指定礼物分类和礼物间的关系 | 请求示例 |  |
| 获取指定礼物分类下的礼物关系 | 请求示例 |  |
| ​礼物多语言​管理 | 添加礼物多语言信息 | 请求示例 |
| 删除指定礼物多语言信息 | 请求示例 |  |
| 获取礼物多语言信息 | 请求示例 |  |
| 添加礼物分类多语言信息 | 请求示例 |  |
| 删除指定礼物分类多语言信息 | 请求示例 |  |
| 获取礼物分类多语言信息 | 请求示例 |  |

### 计费与送礼扣费流程

当观众赠送礼物时，需要确保其账户余额充足，并完成实际的扣费操作，然后才能触发礼物特效的播放和广播。

#### 实现方式
1. **后台配置回调**：在 LiveKit 后台配置您的自建计费系统的回调 URL。参考 回调配置文档。

2. **客户端发送**：客户端调用 `sendGift`。

3. **后台交互**：LiveKit 后台调用您的回调 URL，您的计费系统执行扣费并返回结果。

4. **结果同步**：扣费成功，AtomicXCore 广播 `onReceiveGift` 事件；扣费失败，`sendGift` 的 `completion` 收到错误。

#### 调用流程图

#### 涉及 REST API 接口一览
| 接口 | 说明 | 请求示例 |
| --- | --- | --- |
| 回调配置 - 发送礼物之前回调 | 客户后台可以通过该回调决定是否通过送礼前校验等场景 | 调用示例 |

### 实现全屏礼物动画播放

当直播间有用户（包括自己）发送了"火箭"、"嘉年华"等豪华礼物时，全屏播放一个酷炫的礼物动画（例如 SVGA 动画），营造热烈的氛围。

#### 实现方式

`AtomicXCore` 本身不包含礼物动画播放器，您需要根据业务需求选择并集成第三方库。以下是两种方案的对比：
| **对比项** | **基础方案 (SVGAPlayer-Android)** | **高级方案 (TCEffectPlayerKit)** |
| --- | --- | --- |
| 计费 | 免费 (开源库) | 付费 (需购买 License)，请参见 [付费指引](https://cloud.tencent.com/document/product/616/116461) |
| 集成方式 | 需手动集成 SVGAPlayer 库 (例如通过 Gradle) | 需额外集成 TCEffectPlayerKit 并进行鉴权 |
| 动画格式支持 | 仅支持 SVGA | SVGA、PAG、WebP、Lottie、MP4 等多种格式 |
| 性能 | 建议 SVGA 文件 ≤ 10MB | 支持更大的动画文件，复杂特效/多动画并发/低端机表现更优 |
| 推荐场景 | 礼物动画格式统一为 SVGA，且文件大小可控 | 需要支持多种动画格式，或对动画性能/设备兼容性有更高要求 |

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
| Store/Component | 功能描述 | API 文档 |
| --- | --- | --- |
| GiftStore | 礼物互动：获取礼物列表，发送 / 接收礼物，监听礼物事件（含发送者、礼物详情）。 | [API 文档](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.gift/-gift-store/index.html) |
| BarrageStore | 弹幕功能：发送文本 / 自定义弹幕，维护弹幕列表，实时监听弹幕状态。 | [API 文档](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.barrage/-barrage-store/index.html) |

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

---

`GiftStore` 是 `AtomicXCore` 中专门负责管理直播间礼物功能的模块。通过它，您可以为您的直播应用构建一套完整的礼物系统，实现丰富的营收和互动场景。
| 礼物面板 | 弹幕礼物 | 全屏礼物 |
| --- | --- | --- |
|  |  |  |

## 核心功能
- **礼物列表获取**：从服务端拉取礼物面板所需的数据，包括礼物分类和礼物详情。

- **发送礼物**：观众可以向主播发送选定的礼物，并附带数量。

- **礼物事件广播**：实时接收房间内发生的礼物赠送事件，用于展示礼物动画和弹幕通知。

## 核心概念

在开始集成之前，我们先通过下表了解一下 `GiftStore` 相关的几个核心概念：
| **核心概念** | **类型** | **核心职责与描述** |
| --- | --- | --- |
| `Gift` | `struct` | 代表一个具体的礼物数据模型。包含了礼物的 ID、名称、图标地址、动画资源地址 (resourceURL) 和价格 (coins) 等。 |
| `GiftCategory` | `struct` | 代表一个礼物分类，例如“热门”、“豪华”等。它包含了分类的名称以及该分类下的 **Gift **列表。 |
| `GiftState` | `struct` | 代表礼物模块的当前状态。其核心属性 usableGifts 是一个 [GiftCategory] 数组，存储了从服务端拉取到的完整礼物列表。 |
| `GiftEvent` | `enum` | 代表直播间内发生的礼物事件。目前只有 .onReceiveGift，当有任何人（包括自己）发送礼物时，房间内所有人都会收到此事件。 |
| `GiftStore` | `class` | 这是与礼物功能交互的核心管理类。通过它，您可以拉取礼物列表、发送礼物，并通过订阅其 giftEventPublisher 来接收礼物事件。 |

## 实现步骤

### 步骤1：组件集成

> **说明：**
> 

> 使用**礼物系统**要求开通TUILiveKit **多人连麦版**、**大规模直播版**，不同套餐中可配置的礼物数量有所不同，详细参见 功能与计费说明 中的**礼物系统**说明。
> 

- **视频直播**：请参考 快速接入 集成 **AtomicXCore**，完成接入。

- **语聊房**：请参考 快速接入 集成 **AtomicXCore**，完成接入。

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

| **参数** | **类型** | **描述** |
| --- | --- | --- |
| `categoryID` | `String` | 礼物分类的唯一 ID。 |
| `name` | `String` | 礼物分类的显示名称。 |
| `desc` | `String` | 礼物分类的描述信息。 |
| `extensionInfo` | `[String: String]` | 扩展信息字段。 |
| `giftList` | `[`[`Gift`](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/gift)`]` | 该分类下包含的 Gift 礼物对象数组。 |

- `Gift`** 参数说明**

| **参数** | **类型** | **描述** |
| --- | --- | --- |
| `giftID` | `String` | 礼物的唯一 ID。 |
| `name` | `String` | 礼物的显示名称。 |
| `desc` | `String` | 礼物的描述信息。 |
| `iconURL` | `String` | 礼物图标 URL。 |
| `resourceURL` | `String` | 礼物动画资源 URL。 |
| `level` | `UInt` | 礼物等级。 |
| `coins` | `UInt` | 礼物价格。 |
| `extensionInfo` | `[String: String]` | 扩展信息字段。 |

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
| **参数名** | **类型** | **描述** |
| --- | --- | --- |
| `giftID` | `String` | 要发送的礼物的唯一 ID。 |
| `count` | `UInt` | 发送的数量。 |
| `completion` | `CompletionClosure?` | 发送完成后的回调。 |

## 功能进阶

`GiftStore` 的功能高度依赖于您的业务后台服务。本章将指导您如何通过服务端配置和客户端实现，构建功能丰富、体验卓越的礼物互动系统。

### **礼物素材配置**

您需要自定义直播间可用的礼物种类、分类、名称、图标、价格以及动画效果，以满足运营需求和品牌特色。

#### **实现方式 **
1. **服务端配置**：使用 LiveKit 服务端 REST API 管理礼物信息、分类、多语言等。请参考 [礼物配置指引文档](https://cloud.tencent.com/document/product/647/121321)。

2. **客户端拉取**：在客户端调用 `refreshUsableGifts` 获取配置数据。

3. **UI 展示**：使用拉取到的 `[GiftCategory]` 数据填充礼物面板。

#### **配置时序图**

#### **涉及 REST API 接口一览**
| 接口分类 | 接口 | 请求示例 |
| --- | --- | --- |
| ​礼物管理​ | 添加礼物信息 | 请求示例 |
| 删除礼物信息 | 请求示例 |  |
| 查询礼物信息 | 请求示例 |  |
| 礼物​分类管理​ | 添加礼物分类信息 | 请求示例 |
| 删除指定礼物分类信息 | 请求示例 |  |
| 获取指定礼物分类信息 | 请求示例 |  |
| ​礼物关系管理​ | 添加指定礼物分类和礼物间的关系 | 请求示例 |
| 删除指定礼物分类和礼物间的关系 | 请求示例 |  |
| 获取指定礼物分类下的礼物关系 | 请求示例 |  |
| ​礼物多语言​管理 | 添加礼物多语言信息 | 请求示例 |
| 删除指定礼物多语言信息 | 请求示例 |  |
| 获取礼物多语言信息 | 请求示例 |  |
| 添加礼物分类多语言信息 | 请求示例 |  |
| 删除指定礼物分类多语言信息 | 请求示例 |  |
| 获取礼物分类多语言信息 | 请求示例 |  |

### 计费与送礼扣费流程

当观众赠送礼物时，需要确保其账户余额充足，并完成实际的扣费操作，然后才能触发礼物特效的播放和广播。

#### 实现方式
1. **后台配置回调**：在 LiveKit 后台配置您的自建计费系统的回调 URL。参考 回调配置文档。

2. **客户端发送**：客户端调用 `sendGift`。

3. **后台交互**：LiveKit 后台调用您的回调 URL，您的计费系统执行扣费并返回结果。

4. **结果同步**：扣费成功，AtomicXCore 广播 `.onReceiveGift` 事件。扣费失败，`sendGift` 的 `completion` 收到错误。

#### 调用流程图

#### 涉及 REST API 接口一览
| 接口 | 说明 | 请求示例 |
| --- | --- | --- |
| 回调配置 - 发送礼物之前回调 | 客户后台可以通过该回调决定是否通过送礼前校验等场景 | 调用示例 |

### 实现全屏礼物动画播放

当直播间有用户（包括自己）发送了“火箭”、“嘉年华”等豪华礼物时，全屏播放一个酷炫的礼物动画（例如 SVGA 动画），营造热烈的氛围。

#### 实现方式

`AtomicXCore` 本身不包含礼物动画播放器，您需要根据业务需求选择并集成第三方库。以下是两种方案的对比：
| **对比项** | **基础方案 (SVGAPlayer-iOS)** | **高级方案 (TCEffectPlayerKit)** |
| --- | --- | --- |
| 计费 | 免费 (开源库) | 付费 (需购买 License)，请参见 [付费指引](https://cloud.tencent.com/document/product/616/116461) |
| 集成方式 | 需手动集成 SVGAPlayer 库 (例如通过 CocoaPods) | 需额外集成 TCEffectPlayerKit 并进行鉴权 |
| 动画格式支持 | 仅支持 SVGA | SVGA、PAG、WebP、Lottie、MP4 等多种格式 |
| 性能 | 建议 SVGA 文件 ≤ 10MB | 支持更大的动画文件，复杂特效/多动画并发/低端机表现更优 |
| 推荐场景 | 礼物动画格式统一为 SVGA，且文件大小可控 | 需要支持多种动画格式，或对动画性能/设备兼容性有更高要求 |

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
| Store/Component | 功能描述 | API 文档 |
| --- | --- | --- |
| GiftStore | 礼物互动：获取礼物列表，发送 / 接收礼物，监听礼物事件（含发送者、礼物详情）。 | [API 文档](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/giftstore) |
| BarrageStore | 弹幕功能：发送文本 / 自定义弹幕，维护弹幕列表，实时监听弹幕状态。 | [API 文档](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/barragestore) |

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

---

`GiftStore` 是 `AtomicXCore` 中专门负责管理直播间礼物功能的模块。通过它，您可以为您的直播应用构建一套完整的礼物系统，实现丰富的营收和互动场景。
| **礼物面板** | **弹幕礼物** | **全屏礼物** |
| --- | --- | --- |
|  |  |  |

## 核心功能
- **礼物列表获取**：从服务端拉取礼物面板所需的数据，包括礼物分类和礼物详情。

- **发送礼物**：观众可以向主播发送选定的礼物，并附带数量。

- **礼物事件广播**：实时接收房间内发生的礼物赠送事件，用于展示礼物动画和弹幕通知。

## 核心概念

在开始集成之前，我们先通过下表了解一下 `GiftStore` 相关的几个核心概念：
| **核心概念** | **类型** | **核心职责与描述** |
| --- | --- | --- |
| [Gift](https://tencent-rtc.github.io/TUIKit_Flutter/api_gift_gift_store/Gift-class.html) | `class` | 代表一个具体的礼物数据模型。包含了礼物的 ID、名称、图标地址、动画资源地址 (resourceURL) 和价格 (coins) 等。 |
| [GiftCategory](https://tencent-rtc.github.io/TUIKit_Flutter/api_gift_gift_store/GiftCategory-class.html) | `class` | 代表一个礼物分类，例如"热门"、"豪华"等。它包含了分类的名称以及该分类下的 **Gift** 列表。 |
| [GiftState](https://tencent-rtc.github.io/TUIKit_Flutter/api_gift_gift_store/GiftState-class.html) | `class` | 代表礼物模块的当前状态。其核心属性 `usableGifts` 是一个 `ValueListenable<List<GiftCategory>>`，存储了从服务端拉取到的完整礼物列表。 |
| [GiftListener](https://tencent-rtc.github.io/TUIKit_Flutter/api_gift_gift_store/GiftListener-class.html) | `class` | 礼物事件监听器，通过 `onReceiveGift` 回调接收礼物赠送事件，当有任何人（包括自己）发送礼物时，房间内所有人都会收到此事件。 |
| [GiftStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_gift_gift_store/GiftStore-class.html) | `class` | 这是与礼物功能交互的核心管理类。通过它，您可以拉取礼物列表、发送礼物，并通过 `addGiftListener` 来接收礼物事件。 |

## 实现步骤

### 步骤1：组件集成

请参考 开始直播 集成 **AtomicXCore**，完成接入。

### 步骤2：初始化并监听礼物事件

获取 `GiftStore` 实例，并设置监听器以接收礼物事件和礼物列表更新。

#### 实现方式:
1. **获取实例**：使用 `GiftStore.create(liveId)` 获取与当前直播间绑定的 `GiftStore` 实例。

2. **订阅事件**：通过 `giftStore.addGiftListener(listener)` 添加礼物事件监听器。

3. **订阅状态**：监听 `giftStore.giftState.usableGifts` 获取礼物列表更新。

#### 代码示例:
``` java
import 'package:flutter/foundation.dart';
import 'package:atomic_x_core/atomicxcore.dart';

class GiftManager {
  final String liveId;
  late final GiftStore giftStore;
  late final GiftListener _giftListener;
  late final VoidCallback _giftListChangedListener = _onGiftListChanged;

  // 对外暴露礼物事件回调
  void Function(String liveID, Gift gift, int count, LiveUserInfo sender)? onReceiveGift;

  // 对外暴露礼物列表
  ValueNotifier<List<GiftCategory>> giftListNotifier = ValueNotifier([]);

  GiftManager({required this.liveId}) {
    // 1. 通过 liveId 获取 GiftStore 的实例
    giftStore = GiftStore.create(liveId);

    _subscribeToGiftState();
    _subscribeToGiftEvents();
  }

  /// 2. 订阅礼物事件
  void _subscribeToGiftEvents() {
    _giftListener = GiftListener(
      onReceiveGift: (liveID, gift, count, sender) {
        // 收到事件后，将其转发给外部处理
        onReceiveGift?.call(liveID, gift, count, sender);
      },
    );
    giftStore.addGiftListener(_giftListener);
  }

  /// 3. 订阅礼物列表状态
  void _subscribeToGiftState() {
    giftStore.giftState.usableGifts.addListener(_giftListChangedListener);
  }

  void _onGiftListChanged() {
    giftListNotifier.value = giftStore.giftState.usableGifts.value;
  }

  // 在退出直播间时可调用 dispose 方法回收资源
  void dispose() {
    giftStore.removeGiftListener(_giftListener);
    giftStore.giftState.usableGifts.removeListener(_giftListChangedListener);
    giftListNotifier.dispose();
  }
}
```

#### 礼物列表结构体参数
- `GiftCategory`**参数说明**

| **参数** | **类型** | **描述** |
| --- | --- | --- |
| `categoryID` | `String` | 礼物分类的唯一 ID。 |
| `name` | `String` | 礼物分类的显示名称。 |
| `desc` | `String` | 礼物分类的描述信息。 |
| `extensionInfo` | `Map<String, String>` | 扩展信息字段。 |
| `giftList` | `List<Gift>` | 该分类下包含的 Gift 礼物对象数组。 |

- `Gift`**参数说明**

| **参数** | **类型** | **描述** |
| --- | --- | --- |
| `giftID` | `String` | 礼物的唯一 ID。 |
| `name` | `String` | 礼物的显示名称。 |
| `desc` | `String` | 礼物的描述信息。 |
| `iconURL` | `String` | 礼物图标 URL。 |
| `resourceURL` | `String` | 礼物动画资源 URL。 |
| `level` | `int` | 礼物等级。 |
| `coins` | `int` | 礼物价格。 |
| `extensionInfo` | `Map<String, String>` | 扩展信息字段。 |

### 步骤3：获取礼物列表

调用 `refreshUsableGifts` 方法，从服务端拉取礼物数据。

#### 实现方式:
1. **调用接口**：在合适的时机（例如进入直播间后）调用 `giftStore.refreshUsableGifts()`。

2. **处理结果**：可选地处理返回结果以获知拉取结果。

3. **接收数据**：拉取成功后，通过步骤2中对 `giftStore.giftState.usableGifts` 的监听，自动接收到更新后的礼物列表。

#### 代码示例:
``` java
extension GiftManagerFetch on GiftManager {
  /// 从服务端刷新礼物列表
  Future<void> fetchGiftList() async {
    final result = await giftStore.refreshUsableGifts();
    if (result.isSuccess) {
      debugPrint("礼物列表拉取成功");
      // 成功后，数据会通过 usableGifts 监听自动更新
    } else {
      debugPrint("礼物列表拉取失败: ${result.errorMessage}");
    }
  }
}
```

### 步骤4：发送礼物

当用户在礼物面板选择一个礼物并点击发送时，调用 `sendGift` 接口将礼物发送出去。

#### 实现方式:
1. **获取参数**：从 UI 获取用户选择的 giftID 和发送数量 count。

2. **调用接口**：调用 `giftStore.sendGift(giftID:, count:)`。

3. **处理结果**：在返回结果中处理发送失败的情况（例如余额不足提示）；发送成功后的 UI 更新（动画、弹幕）应由 `onReceiveGift` 事件驱动。

#### 代码示例:
``` java
extension GiftManagerSend on GiftManager {
  /// 用户发送一个礼物
  Future<void> sendGift(String giftID, int count) async {
    final result = await giftStore.sendGift(giftID: giftID, count: count);
    if (result.isSuccess) {
      debugPrint("礼物 $giftID 发送成功");
      // 发送成功后，包括发送者在内的所有人都会收到 onReceiveGift 事件
    } else {
      debugPrint("礼物发送失败: ${result.errorMessage}");
      // 可以在此提示用户，例如"余额不足"或"网络错误"
    }
  }
}
```

#### `sendGift` 接口参数
| **参数名** | **类型** | **描述** |
| --- | --- | --- |
| `giftID` | `String` | 要发送的礼物的唯一 ID。 |
| `count` | `int` | 发送的数量。 |

## 功能进阶

`GiftStore` 的功能高度依赖于您的业务后台服务。本章将指导您如何通过服务端配置和客户端实现，构建功能丰富、体验卓越的礼物互动系统。

### **礼物素材配置**

您需要自定义直播间可用的礼物种类、分类、名称、图标、价格以及动画效果，以满足运营需求和品牌特色。

#### **实现方式**
1. **服务端配置**：使用 LiveKit 服务端 REST API 管理礼物信息、分类、多语言等。请参考 礼物配置指引文档。

2. **客户端拉取**：在客户端调用 `refreshUsableGifts` 获取配置数据。

3. **UI 展示**：使用拉取到的 `List<GiftCategory>` 数据填充礼物面板。

#### **配置时序图**

#### **涉及 REST API 接口一览**
| **接口分类** | **接口** | **请求示例** |
| --- | --- | --- |
| 礼物管理 | 添加礼物信息 | 请求示例 |
| 礼物管理 | 删除礼物信息 | 请求示例 |
| 礼物管理 | 查询礼物信息 | 请求示例 |
| 礼物分类管理 | 添加礼物分类信息 | 请求示例 |
| 礼物分类管理 | 删除指定礼物分类信息 | 请求示例 |
| 礼物分类管理 | 获取指定礼物分类信息 | 请求示例 |
| 礼物关系管理 | 添加指定礼物分类和礼物间的关系 | 请求示例 |
| 礼物关系管理 | 删除指定礼物分类和礼物间的关系 | 请求示例 |
| 礼物关系管理 | 获取指定礼物分类下的礼物关系 | 请求示例 |
| 礼物多语言管理 | 添加礼物多语言信息 | 请求示例 |
| 礼物多语言管理 | 删除指定礼物多语言信息 | 请求示例 |
| 礼物多语言管理 | 获取礼物多语言信息 | 请求示例 |
| 礼物多语言管理 | 添加礼物分类多语言信息 | 请求示例 |
| 礼物多语言管理 | 删除指定礼物分类多语言信息 | 请求示例 |
| 礼物多语言管理 | 获取礼物分类多语言信息 | 请求示例 |

### 计费与送礼扣费流程

当观众赠送礼物时，需要确保其账户余额充足，并完成实际的扣费操作，然后才能触发礼物特效的播放和广播。

#### 实现方式
1. **后台配置回调**：在 LiveKit 后台配置您的自建计费系统的回调 URL。参考 回调配置文档。

2. **客户端发送**：客户端调用 `sendGift`。

3. **后台交互**：LiveKit 后台调用您的回调 URL，您的计费系统执行扣费并返回结果。

4. **结果同步**：扣费成功，AtomicXCore 广播 `onReceiveGift` 事件。扣费失败，`sendGift` 返回错误。

#### 调用流程图

#### 涉及 REST API 接口一览
| **接口** | **说明** | **请求示例** |
| --- | --- | --- |
| 回调配置 - 发送礼物之前回调 | 客户后台可以通过该回调决定是否通过送礼前校验等场景 | 调用示例 |

### 播放全屏礼物动画

当直播间有用户（包括自己）发送了"火箭"、"嘉年华"等豪华礼物时，全屏播放一个酷炫的礼物动画（例如 SVGA 动画），营造热烈的氛围。

#### 实现方式

`AtomicXCore` 本身不包含礼物动画播放器，您需要根据业务需求选择并集成第三方库。以下是两种方案的对比：
| **对比项** | **基础方案 (svgaplayer_flutter)** | **高级方案 (TCEffectPlayerKit)** |
| --- | --- | --- |
| 计费 | 免费 (开源库) | 付费 (需购买 License)，请参见 [付费指引](https://cloud.tencent.com/document/product/616/116461) |
| 集成方式 | 需手动集成 [svgaplayer_flutter](https://pub.dev/packages/svgaplayer_flutter) 库 | 需额外集成 [flutter_effect_player](https://github.com/Tencent-RTC/EffectPlayer_Flutter)库并进行鉴权 |
| 动画格式支持 | 仅支持 SVGA | SVGA、PAG、WebP、Lottie、MP4 等多种格式 |
| 性能 | 建议 SVGA 文件 ≤ 10MB | 支持更大的动画文件，复杂特效/多动画并发/低端机表现更优 |
| 推荐场景 | 礼物动画格式统一为 SVGA，且文件大小可控 | 需要支持多种动画格式，或对动画性能/设备兼容性有更高要求 |

本章节主要演示基础方案的集成。如果您选择高级方案，请参考 [EffectPlayer Flutter 集成指引](https://cloud.tencent.com/document/product/616/123945)。

#### 基础方案实现：使用 svgaplayer_flutter
1. **集成 svgaplayer_flutter**：在您的 `pubspec.yaml` 文件中，添加依赖并运行 `flutter pub get`。

   ``` yaml
   dependencies:
     svgaplayer_flutter: ^2.0.0
   ```
2. **监听礼物事件**：通过 `GiftStore` 的 `addGiftListener` 添加监听器。

3. **解析并播放**：当收到 `onReceiveGift` 事件时，检查 `gift.resourceURL` 是否有效且指向一个 SVGA 文件。如果是，则使用 `SVGAAnimationController` 播放动画。

#### 代码示例
``` java
import 'package:flutter/material.dart';
import 'package:atomic_x_core/atomicxcore.dart';
import 'package:svgaplayer_flutter/svgaplayer_flutter.dart';

class LiveRoomWidget extends StatefulWidget {
  final String liveId;
  const LiveRoomWidget({Key? key, required this.liveId}) : super(key: key);

  @override
  State<LiveRoomWidget> createState() => _LiveRoomWidgetState();
}

class _LiveRoomWidgetState extends State<LiveRoomWidget> with SingleTickerProviderStateMixin {
  late GiftManager giftManager;

  // SVGA 播放器
  late SVGAAnimationController _svgaController;
  bool _showAnimation = false;

  @override
  void initState() {
    super.initState();
    _svgaController = SVGAAnimationController(vsync: this);
    _setupGiftSubscription();
  }

  void _setupGiftSubscription() {
    giftManager = GiftManager(liveId: widget.liveId);

    giftManager.onReceiveGift = (liveID, gift, count, sender) {
      if (gift.resourceURL.isNotEmpty) {
        _playAnimation(gift.resourceURL);
      }
    };
  }

  Future<void> _playAnimation(String url) async {
    try {
      final videoItem = await SVGAParser.shared.decodeFromURL(url);
      _svgaController.videoItem = videoItem;
      setState(() {
        _showAnimation = true;
      });
      _svgaController.forward().whenComplete(() {
        setState(() {
          _showAnimation = false;
        });
      });
    } catch (e) {
      debugPrint("SVGA 动画解析失败: $e");
    }
  }

  @override
  void dispose() {
    _svgaController.dispose();
    giftManager.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Stack(
      children: [
        // 直播画面
        // ...

        // 全屏礼物动画
        if (_showAnimation)
          Positioned.fill(
            child: SVGAImage(_svgaController),
          ),
      ],
    );
  }
}
```

### 在弹幕区展示礼物赠送消息

当有用户发送礼物时，不仅播放动画，同时在公屏弹幕区域显示一条系统消息，例如："【观众昵称】送出了【礼物名称】x【数量】"，让所有观众都能看到。

#### 实现方式
1. **监听事件**：通过 `giftStore.addGiftListener` 添加监听器。

2. **获取信息**：收到 `onReceiveGift` 事件后，提取发送者 sender、礼物 gift 和数量 count。

3. **获取弹幕 Store**：使用 `BarrageStore.create(liveId)` 获取与当前房间绑定的实例。

4. **拼接消息**：创建一条 `Barrage` 对象，设置 `messageType = BarrageType.text`，`textContent` 为拼接好的字符串（例如 “[`sender.userName`] 送出了 [`gift.name`] x [`count`]”）。

5. **本地插入**：调用 `barrageStore.appendLocalTip(giftTip)` 将消息插入本地列表。

#### 代码示例
``` java
// 在 LiveRoomManager 或类似的顶层管理器中
void _setupGiftToBarrageFlow() {
  final giftStore = GiftStore.create(liveId);
  final barrageStore = BarrageStore.create(liveId);

  final giftListener = GiftListener(
    onReceiveGift: (liveID, gift, count, sender) {
      // 拼接消息
      final tipText = "${sender.userName} 送出了 ${gift.name} x $count";
      final giftTip = Barrage(
        messageType: BarrageType.text,
        textContent: tipText,
      );
      // 可选：设置一个特殊的sender

      // 本地插入
      barrageStore.appendLocalTip(giftTip);
    },
  );

  giftStore.addGiftListener(giftListener);
}
```

## API 文档

关于 [GiftStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_gift_gift_store/GiftStore-class.html) 及其相关类的所有公开接口、属性和方法的详细信息，请参阅随 [AtomicXCore](https://tencent-rtc.github.io/TUIKit_Flutter/index.html) 框架的官方 API 文档。本指南使用到的相关 Store 如下：
| **Store/Component** | **功能描述** | **API 文档** |
| --- | --- | --- |
| **GiftStore** | 礼物互动：获取礼物列表，发送 / 接收礼物，监听礼物事件（含发送者、礼物详情）。 | [API 文档](https://tencent-rtc.github.io/TUIKit_Flutter/api_gift_gift_store/GiftStore-class.html) |
| **BarrageStore** | 弹幕功能：发送文本 / 自定义弹幕，维护弹幕列表，实时监听弹幕状态。 | [API 文档](https://tencent-rtc.github.io/TUIKit_Flutter/api_barrage_barrage_store/BarrageStore-class.html) |

## 常见问题

### `GiftStore` 的礼物列表是空的，我该怎么办？

您必须主动调用 `refreshUsableGifts()` 来从您的业务后台拉取礼物数据。这些礼物数据需要在您的业务后台通过服务端 REST API 进行配置。

### 如何实现礼物的多语言展示（例如中文、英文）？

`GiftStore` 提供了 `setLanguage(String language)` 接口。您可以在 `refreshUsableGifts` 之前调用此方法，传入目标语言代码（例如 "en" 或 "zh-CN"）。服务端会根据此语言代码，返回对应语言的礼物名称和描述。

### 我调用 sendGift 发送了礼物，礼物动画为什么重复播放了两次？

`onReceiveGift` 事件是对房间内所有成员的广播（包括发送者自己）。如果您在 `sendGift` 的成功回调里执行了一次 UI 操作，同时又在 `onReceiveGift` 回调中执行了相同的 UI 操作，就会造成重复。
- **最佳实践**：UI 的更新（例如播放动画、弹幕提示）只在 `onReceiveGift` 事件的回调中处理。`sendGift` 的返回结果仅用于处理发送失败的逻辑（例如提示用户"发送失败"或"余额不足"）。

### 礼物扣费逻辑在哪里实现？

礼物扣费逻辑完全由您的自建计费系统负责。`AtomicXCore` 通过后台回调机制与您的计费系统对接。客户端调用 `sendGift` 触发回调，您的后台服务完成扣费后，将结果返回给 `AtomicXCore` 后台，从而决定礼物事件是否广播。

### 送礼通知会被禁言或频控拦截吗？

不会。送礼通知（`onReceiveGift` 事件）不受禁言或消息频控影响，确保可靠投递。

### 礼物动画播放卡顿怎么办？

请检查您的 SVGA 文件大小，基础播放器建议不要超过 10MB。如果文件过大或动画复杂，您可以考虑集成 TUILiveKit 提供的高级特效播放器，以获得更优的性能表现。
