> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

本篇文档旨在指导 Android 开发者如何使用 `AtomicXCore` 框架中的 `BarrageStore` 模块，为您的直播应用快速集成功能丰富、性能卓越的弹幕系统。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032603567/9dd47237afde11f082b4525400e889b2.png)


## 核心功能

`BarrageStore` 为您的直播应用提供了一套完整的弹幕解决方案，核心功能包括：
- 接收并展示直播间弹幕消息。

- 发送文本弹幕与观众互动。

- 发送自定义业务弹幕，以支持礼物、点赞等复杂场景。

- 在本地消息列表中插入系统提示（例如，"欢迎 XX 进入直播间"）。


## 核心概念解析

在开始集成之前，我们先通过下表了解一下 BarrageStore 相关的几个核心概念：
<table>
<tr>
<td rowspan="1" colSpan="1" >**核心概念**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**核心职责与描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[Barrage](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.barrage/-barrage/index.html)</td>

<td rowspan="1" colSpan="1" >`data class`</td>

<td rowspan="1" colSpan="1" >代表一条弹幕消息的数据模型。它包含了发送者信息 (`sender`)、消息内容 (`textContent` 或 `data`)、消息类型 (`messageType`) 等所有关键信息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[BarrageState](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.barrage/-barrage-state/index.html)</td>

<td rowspan="1" colSpan="1" >`data class`</td>

<td rowspan="1" colSpan="1" >代表弹幕模块的当前状态。其核心属性 `messageList` 是一个`StateFlow`，按时间顺序存储了当前直播间的所有弹幕消息，是UI渲染的数据源。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[BarrageStore](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.barrage/-barrage-store/index.html)</td>

<td rowspan="1" colSpan="1" >`abstract class`</td>

<td rowspan="1" colSpan="1" >这是与弹幕功能交互的核心管理类。通过它，您可以发送消息 (`sendTextMessage`, `sendCustomMessage`)，并通过订阅其 `state` 属性来接收和监听所有弹幕消息的更新。</td>
</tr>
</table>


## 实现步骤

### 步骤1：组件集成

请参考 [开始直播](https://write.woa.com/document/191126372105478144) 集成 **AtomicXCore**，完成接入。

### 步骤2：初始化并监听弹幕

获取一个与当前直播间 `liveId` 绑定的 `BarrageStore` 实例，并设置一个订阅者来实时接收最新的**全量**弹幕消息列表。
``` kotlin
import kotlinx.coroutines.*
import kotlinx.coroutines.flow.*
import io.trtc.tuikit.atomicxcore.api.barrage.Barrage
import io.trtc.tuikit.atomicxcore.api.barrage.BarrageStore

class BarrageManager(
    private val liveId: String
) {
    private val barrageStore: BarrageStore = BarrageStore.create(liveId)
    private val scope = CoroutineScope(Dispatchers.Main)
    
    // 对外暴露【全量】消息列表的Flow，方便UI层订阅
    private val _messagesFlow = MutableStateFlow<List<Barrage>>(emptyList())
    val messagesFlow: StateFlow<List<Barrage>> = _messagesFlow.asStateFlow()
    
    init {
        // 初始化后立即开始监听弹幕消息
        subscribeToBarrageUpdates()
    }

    private fun subscribeToBarrageUpdates() {
        scope.launch {
            barrageStore.barrageState.messageList
                .collect { messageList ->
                    // 当 messageList 更新时，通过 Flow 将新列表传递给UI层
                    // 关键点：这里接收到的是包含所有历史消息的【完整列表】
                    _messagesFlow.value = messageList
                }
        }
    }
}
```

### 步骤3：发送文本弹幕

调用 `sendTextMessage` 方法向直播间内的所有用户广播一条纯文本消息。
``` kotlin
import io.trtc.tuikit.atomicxcore.api.CompletionHandler
import io.trtc.tuikit.atomicxcore.api.barrage.BarrageStore

class BarrageManager(
    private val liveId: String
) {
    private val barrageStore: BarrageStore = BarrageStore.create(liveId)

    // 发送一条文本弹幕
    fun sendTextMessage(text: String) {
        // 建议：增加非空校验，避免发送无效消息
        if (text.isEmpty()) {
            return
        }
        
        // 调用核心API发送消息
        barrageStore.sendTextMessage(
            text,
            mapOf(
                "custom key" to "custom value",
            ),
            object : CompletionHandler {
                override fun onSuccess() {
                    println("文本弹幕 '$text' 发送成功")
                }

                override fun onFailure(code: Int, desc: String) {
                    println("文本弹幕发送失败: $desc")
                }
            }
        )
    }
}

```

#### **接口参数**
<table>
<tr>
<td rowspan="1" colSpan="1" >**参数**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`text`</td>

<td rowspan="1" colSpan="1" >`String?`</td>

<td rowspan="1" colSpan="1" >要发送的文本内容。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`extensionInfo`</td>

<td rowspan="1" colSpan="1" >`Map<String, String>?`</td>

<td rowspan="1" colSpan="1" >附加的扩展信息，可用于业务自定义。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`completion`</td>

<td rowspan="1" colSpan="1" >`CompletionHandler?`</td>

<td rowspan="1" colSpan="1" >发送完成后的回调，包含成功或失败的结果。</td>
</tr>
</table>


### 步骤4：发送自定义弹幕

发送一条包含自定义业务逻辑的消息，例如礼物、点赞或游戏化互动指令。这条消息对其他客户端来说是透明的，需要业务层自行解析。
``` kotlin
class BarrageManager(
    private val liveId: String
) {
    // 发送一条自定义弹幕，例如用于发送礼物
    fun sendGiftMessage(giftId: String, giftCount: Int) {
        // 1. 定义一个能识别业务的ID
        val businessId = "live_gift"

        // 2. 将业务数据编码为 JSON 字符串
        val giftData = mapOf(
            "gift_id" to giftId,
            "gift_count" to giftCount
        )

        val jsonString = try {
            // 使用 Gson 或其他 JSON 库进行序列化
            // 这里假设使用 Gson
            Gson().toJson(giftData)
        } catch (e: Exception) {
            return
        }

        // 3. 调用核心API发送自定义消息
        barrageStore.sendCustomMessage(
            businessId,
            jsonString,
            object : CompletionHandler {
                override fun onSuccess() {
                    println("礼物消息（自定义弹幕）发送成功")
                }
                
                override fun onFailure(code: Int, desc: String) {
                    println("礼物消息发送失败: $desc")
                }
            }
        )
    }
}
```

#### **接口参数**
<table>
<tr>
<td rowspan="1" colSpan="1" >**参数**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`businessId`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >业务唯一标识符，例如 "live_gift"，用于接收端区分不同的自定义消息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`data`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >业务数据，通常为 JSON 格式的字符串。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`completion`</td>

<td rowspan="1" colSpan="1" >`CompletionHandler?`</td>

<td rowspan="1" colSpan="1" >发送完成后的回调。</td>
</tr>
</table>


### 步骤5：在本地插入提示消息

在当前用户的消息列表中插入一条本地消息，这条消息不会被发送到直播间的其他用户。这非常适合用来显示系统欢迎、警告或操作提示等信息。
``` kotlin
class BarrageManager(
    private val liveId: String
) {
    // 在本地消息列表中插入一条欢迎提示
    fun showWelcomeMessage(user: LiveUserInfo) {
        // 1. 创建一条 Barrage 消息
        val welcomeTip = Barrage(
            liveID = liveId,
            messageType = BarrageType.TEXT, // 可以复用 text 类型来显示
            textContent = "欢迎 ${user.userName} 进入直播间！",
            sender = LiveUserInfo() // sender 可以留空或设置为一个系统用户的标识
        )

        // 2. 调用API将其插入本地列表
        barrageStore.appendLocalTip(welcomeTip)
    }
}
```

#### **接口参数**
<table>
<tr>
<td rowspan="1" colSpan="1" >**参数**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`message`</td>

<td rowspan="1" colSpan="1" >`Barrage`</td>

<td rowspan="1" colSpan="1" >要在本地插入的消息对象。SDK 会将此消息对象追加到 BarrageState 的 messageList 中。</td>
</tr>
</table>


### 步骤6：管理用户发言（禁言与解禁）

作为主播或管理员，您可以对直播间内的用户发言权限进行管理，维护健康的社区氛围。

#### 禁止/解禁单个用户发言

通过 `LiveAudienceStore` 中的 `disableSendMessage` 接口来实现对指定用户的禁言或解禁。此状态会被持久化，即使用户重新进入直播间，禁言状态依然有效。
``` kotlin
import io.trtc.tuikit.atomicxcore.api.*
import io.trtc.tuikit.atomicxcore.api.live.LiveAudienceStore

// 1. 获取与当前直播间绑定的 LiveAudienceStore 实例
val audienceStore = LiveAudienceStore.create(liveId)

// 2. 定义要操作的用户ID和禁言状态
val userIdToMute = "user_id_to_be_muted"
val shouldDisable = true // true为禁言, false为解禁

// 3. 调用接口执行操作
audienceStore.disableSendMessage(
    userIdToMute,
    shouldDisable,
    object : CompletionHandler {
        override fun onSuccess() {
            println("${if (shouldDisable) "禁言" else "解禁"}用户 $userIdToMute 成功")
        }

        override fun onFailure(code: Int, desc: String) {
            println("操作失败: $desc")
        }
    }
)
```

#### 开启/关闭全体禁言

要对直播间内所有用户（通常不包括主播自己）进行禁言，您需要通过 LiveListStore 更新直播间信息来实现。
``` kotlin
import io.trtc.tuikit.atomicxcore.api.CompletionHandler
import io.trtc.tuikit.atomicxcore.api.live.LiveInfo
import io.trtc.tuikit.atomicxcore.api.live.LiveListStore

// 1. 获取 LiveListStore 单例
val liveListStore = LiveListStore.shared()

// 2. 获取当前直播间信息，并修改全体禁言状态
val currentLiveInfo = liveListStore.liveState.currentLive.value.copy(
    isMessageDisable = true // true为全体禁言, false为关闭
)

// 3. 调用更新接口，并指定修改的标志位
liveListStore.updateLiveInfo(
    currentLiveInfo,
    listOf(LiveInfo.ModifyFlag.IS_MESSAGE_DISABLE),
    object : CompletionHandler {
        override fun onSuccess() {
            println("全体禁言状态更新成功")
        }

        override fun onFailure(code: Int, desc: String) {
            println("操作失败: $desc")
        }
    }
)
```

## 功能进阶：高并发场景下的性能优化

当您使用 `BarrageStore` 构建弹幕功能后，本章将指导您如何处理更复杂的业务场景，确保它能在真实、复杂的高并发直播场景下，依然为用户提供流畅、稳定的体验。本章将围绕三个核心业务场景，为您提供明确的优化方案和代码示例。

### 场景一：应对热门直播间的"弹幕风暴"

#### 场景描述

在一场热门活动中，直播间涌入大量观众，弹幕以每秒数十条的频率刷新。

#### 技术挑战

SDK会以极高频率返回完整的弹幕列表。如果每次都调用 `adapter.notifyDataSetChanged()`，主线程会被密集的 UI 布局和渲染操作阻塞，导致界面卡顿。

#### 优化方案：批处理与流量削峰 (Batch Processing & Debouncing)

不必响应每一次的数据更新，而是设定一个时间阈值（例如300毫秒）。只在距离上次UI刷新超过这个阈值后，才执行下一次刷新操作。这能将每秒数十次的 `notifyDataSetChanged()` 调用，降低到每秒3-4次，极大提升流畅度。

#### 代码示例

创建一个 `BarrageUIManager` 类，它内置一个缓冲区和一个定时器，专门负责将数据批量更新到 `RecyclerView`。
``` kotlin
import android.os.Handler
import androidx.recyclerview.widget.RecyclerView
import io.trtc.tuikit.atomicxcore.api.barrage.Barrage

private const val UPDATE_DURATION_MS = 300L

class BarrageUIManager() {
    private var timestampOnLastUpdate = 0L

    private var dataSource: ArrayList<Barrage> = ArrayList()
    private val updateViewTask = Runnable { notifyDataSetChanged() }
    private val handler = Handler()
    private val adapter = BarrageAdapter(dataSource)

    // 外部高频调用此方法，传入最新的全量列表
    fun update(newList: List<Barrage>) {
        handler.removeCallbacks(updateViewTask)
        dataSource.clear()
        dataSource.addAll(newList)
        // 刷新频率小于 0.3 秒，不做刷新
        if (System.currentTimeMillis() - timestampOnLastUpdate < UPDATE_DURATION_MS) {
            handler.postDelayed(updateViewTask, UPDATE_DURATION_MS)
            return
        }
    }

    private fun notifyDataSetChanged() {
        adapter.notifyDataSetChanged()
        timestampOnLastUpdate = System.currentTimeMillis()
    }
}

class BarrageAdapter(dataSource: ArrayList<Barrage>): RecyclerView.Adapter<RecyclerView.ViewHolder>() {
    //这里实现adapter能力
}
```

### 场景二：保障长时间直播的内存稳定性

#### 场景描述

您的应用需要支持数小时乃至全天候的"不间断直播"，例如游戏直播或慢直播。在此期间，App 必须保持稳定运行，不能因为长时间运行而意外退出。

#### 技术挑战

SDK 返回的全量 `messageList` 会在长时间直播中无限增长，即使 UI 层做了节流，数据层持有的这个巨大数组也会持续侵占内存，最终导致应用闪退。

#### 优化方案：固定容量的循环数组 (Circular Buffer)

**只让您自己的数据源（DataSource）持有有限数量的消息**。无论 SDK 返回的全量列表有多大，您的应用只截取其中最新的部分用于显示。

#### **代码示例**

在接收到 SDK 的全量列表后，只取最新的500条（或您定义的其他数量）来更新 UI。
``` kotlin
class BarrageUIManager(
    private val recyclerView: RecyclerView
) {
    private val capacity: Int = 500 // 客户端只保留最新的500条消息
    // ...（其他代码同上）...

    private fun refreshUIIfNeeded() {
        val fullList = this.latestMessageList ?: return
        val adapter = recyclerView.adapter ?: return
        this.latestMessageList = null 

        // 关键点：截取最新的N条消息
        val cappedList = fullList.takeLast(capacity)
        
        dataSource.clear()
        dataSource.addAll(cappedList)
        adapter.notifyDataSetChanged()
    }
}
```

### 场景三：渲染包含用户等级、徽章的复杂弹幕样式

#### 场景描述

为了增强直播氛围和付费用户荣誉感，弹幕需要展示丰富的视觉元素，例如混排用户名、用户等级图标、粉丝徽章和消息内容。

#### 技术挑战

渲染包含多图文、自定义字体或复杂布局的视图，比渲染纯文本耗时更长。在列表中高频渲染这些复杂视图，会加重主线程的计算压力，导致列表滚动时出现卡顿。

#### 优化方案：异步绘制 (Asynchronous Drawing)

将视图内容的绘制过程从主线程剥离，放到后台线程去完成。主线程只负责最终的"贴图"操作，即显示已经绘制好的位图。这极大地减轻了主线程的计算压力。

#### 代码示例

在您的自定义 `RecyclerView.ViewHolder` 中，通过使用 `AsyncLayoutInflater` 或预加载机制，来指示系统尽可能地在后台线程完成绘制任务。
``` kotlin
import android.view.LayoutInflater
import androidx.asynclayoutinflater.view.AsyncLayoutInflater
import androidx.recyclerview.widget.RecyclerView

// 在你的自定义弹幕ViewHolder中
class BarrageViewHolder(
    itemView: View
) : RecyclerView.ViewHolder(itemView) {

    // ... (TextView, ImageView等子视图的声明)

    companion object {
        fun create(parent: ViewGroup): BarrageViewHolder {
            // 使用异步布局加载器来减少主线程阻塞
            val inflater = AsyncLayoutInflater(parent.context)
            val view = LayoutInflater.from(parent.context)
                .inflate(R.layout.item_barrage, parent, false)
            return BarrageViewHolder(view)
        }
    }

    fun bind(viewModel: BarrageViewModel) {
        // 在这里设置你的TextView文本、ImageView图片等
        // 由于使用了异步布局加载，这些内容的最终渲染会尽量在后台完成
    }

    // 追求极致性能的进阶方案：完全手动绘制
    // 如果需要更精细的控制，可以使用Canvas手动绘制文本和图片
    // 结合后台线程生成Bitmap，然后在主线程的onDraw方法中绘制它，可以实现完全的异步渲染
}
```

## API 文档

关于 [BarrageStore](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.barrage/-barrage-store/index.html) 及其相关类的所有公开接口、属性和方法的详细信息，请参阅随 [AtomicXCore](https://tencent-rtc.github.io/TUIKit_Android/index.html) 框架的官方 API 文档。

## 常见问题

### 除了基础的文本弹幕，我们还希望实现"彩色弹幕"、"礼物弹幕"等更丰富的样式，该如何实现？

这是通过自定义消息 `sendCustomMessage` 来实现的。`BarrageStore` 不会限制您的业务想象力。

**实现思路**
1. **定义数据结构:** 与您的客户端和服务器团队共同定义好自定义消息的 JSON 结构。例如，一条彩色弹幕可以这样定义：

   ``` json
   {  "type": "colored_text",  "text": "这是一条彩色弹幕!",  "color": "#FF5733" }
   ```
2. **发送端:** 在发送时，将这个 JSON 结构转换为字符串，并通过 `sendCustomMessage` 的 `data` 参数发送出去。`businessID` 可以设置为一个能代表您业务的唯一标识，例如 "`barrage_style_v1`"。

3. **接收端**: 在接收到弹幕消息后，检查其 `messageType` 是否为 `BarrageType.CUSTOM` 以及 `businessID` 是否匹配。如果匹配，则解析 `data` 字符串（通常是解析 JSON），根据解析出的数据（例如 `color、text`）来渲染您的自定义UI样式。


### 我在不同的类、不同的文件中都调用了 `BarrageStore.create(liveID = "some_id")`，这会创建出多个实例导致混乱吗？

完全不会。`AtomicXCore` 内部机制会确保只要您传入的 `liveID` 相同，获取到的永远是同一个与该直播间绑定的 `BarrageStore` 实例。您可以在需要的地方随用随取，无需手动管理单例。

### 为什么我调用了 sendTextMessage，但是在消息列表中看不到我发送的消息？

**请按以下步骤排查：**
1. **检查 completion 回调**：sendTextMessage 方法有一个完成回调。请检查回调返回的结果是成功还是失败。如果失败，错误信息会明确指出问题所在（例如"您已被禁言"、"网络错误"等）。

2. **确认订阅时机**：确保您对 barrageStore.barrageState.messageList 的订阅发生在该 liveID 对应的直播开始之后。如果在加入直播房间之前就开始监听，可能会错过部分消息。

3. **检查 liveID**：确认您在创建 BarrageStore 实例、加入直播房间、以及发送消息时使用的 liveID 完全一致，包括大小写。

4. **网络问题**：检查设备当前的网络连接是否正常。消息发送依赖于网络。


### 新观众进入直播间时，如何让他们看到加入前的历史弹幕消息？

`AtomicXCore` 支持拉取历史弹幕消息，但这需要您在**服务端控制台**进行一项简单的配置。配置完成后，SDK会自动处理后续的一切，您无需编写额外的代码。

**步骤1：在 IM 控制台进行配置**
1. 登录您的 [即时通讯 IM 控制台](https://cloud.tencent.com/login?s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fim)。

2. 在左侧导航栏，按照路径**消息服务 Chat** >** 功能配置 **> **群组配置** >** 群功能配置** > **直播群新成员查看入群前消息量配置**进行导航。

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032603567/6cf938c8afe311f0b28a5254005ef0f7.png)

3. 修改"新成员可查看最近消息数"，最大支持 **50** 条。


   **步骤2：客户端无感获取**


   完成上述配置后，您的客户端代码**无需做任何改动**。 


   当新用户加入直播间时，`AtomicXCore` 的底层会自动拉取您配置的历史消息数量。这些历史消息会和实时消息一样，通过您已实现的 `BarrageStore.barrageState.messageList` 订阅通道推送给您的 UI 层。您的应用会像接收实时弹幕一样，自然地接收并展示这些历史弹幕。
