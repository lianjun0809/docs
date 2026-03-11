> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

`LiveListStore` 是 `AtomicXCore` 中负责管理直播房间列表、创建、加入以及维护房间状态的核心模块。通过`LiveListStore`，您可以为您的应用构建完整的直播生命周期管理。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032603567/a3e16b96b00111f0bb7b525400bf7822.png)


## 核心功能
- **直播列表拉取**：获取当前所有公开的直播间列表，支持分页加载。

- **直播生命周期管理**：提供从创建、开播、加入、离开到结束直播的全套流程接口。

- **直播信息更新**：主播可以随时更新直播间的公开信息，例如封面、公告等。

- **实时事件监听**：监听直播结束、用户被踢出等关键事件。

- **自定义业务数据**：强大的自定义元数据（`MetaData`）能力，允许您在房间内存储和同步任何业务相关的信息，例如直播状态、音乐信息、自定义角色等 。


## 核心概念

在开始集成之前，我们先通过下表了解一下 `LiveListStore` 相关的几个核心概念：
<table>
<tr>
<td rowspan="1" colSpan="1" >**核心概念**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**核心职责与描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`LiveInfo`</td>

<td rowspan="1" colSpan="1" >`data class`</td>

<td rowspan="1" colSpan="1" >代表一个直播间的所有信息模型。包含了直播ID (`liveID`)、名称 (`liveName`)、房主信息 (`liveOwner`) 以及自定义元数据 (`metaData`) 等。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`LiveListState`</td>

<td rowspan="1" colSpan="1" >`data class`</td>

<td rowspan="1" colSpan="1" >代表直播列表模块的当前状态。其核心属性 liveList 是一个 `StateFlow`，存储了拉取到的直播列表；`currentLive` 则代表用户当前所在的直播间信息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`LiveListListener`</td>

<td rowspan="1" colSpan="1" >`abstract class`</td>

<td rowspan="1" colSpan="1" >代表直播房间的全局事件。分为 `onLiveEnded` (直播结束) 和 `onKickedOutOfLive` (被踢出直播) 两种，用于处理关键的房间状态变更。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`LiveListStore`</td>

<td rowspan="1" colSpan="1" >`abstract class`</td>

<td rowspan="1" colSpan="1" >代表直播房间的全局事件。分为 `.onLiveEnded` (直播结束) 和 `.onKickedOutOfLive` (被踢出直播) 两种，用于处理关键的房间状态变更。</td>
</tr>
</table>


## 实现步骤

### 步骤1：组件集成

请参考 [开始直播](https://write.woa.com/document/191126372105478144) 集成 **AtomicXCore**，并完成 [主播开播](https://write.woa.com/document/191126372105478144) 和 [观众观看](https://write.woa.com/document/191126372105478144) 的功能实现。

### 步骤2：实现观众从直播列表进入直播间

创建一个展示直播列表的页面，该页面使用 `RecyclerView` 来布局直播间卡片。当用户点击某个卡片时，获取该直播间的 `liveId`，并跳转到观众观看页面。
``` kotlin
import android.content.Intent
import android.os.Bundle
import android.view.LayoutInflater
import android.view.View
import android.view.ViewGroup
import androidx.appcompat.app.AppCompatActivity
import androidx.recyclerview.widget.GridLayoutManager
import androidx.recyclerview.widget.RecyclerView
import io.trtc.tuikit.atomicxcore.api.CompletionHandler
import io.trtc.tuikit.atomicxcore.api.live.LiveInfo
import io.trtc.tuikit.atomicxcore.api.live.LiveListStore
import kotlinx.coroutines.*
import kotlinx.coroutines.flow.*

class LiveListActivity : AppCompatActivity() {
    private val liveListStore = LiveListStore.shared()
    private var liveList: List<LiveInfo> = emptyList()
    private val coroutineScope = CoroutineScope(Dispatchers.Main)

    private lateinit var recyclerView: RecyclerView
    private lateinit var adapter: LiveListAdapter

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_live_list)
        setupUI()
        bindStore()
        fetchLiveList()
    }

    private fun bindStore() {
        // 订阅 state，自动接收列表更新
        coroutineScope.launch {
            liveListStore.liveState.liveList.collect { fetchedList ->
                liveList = fetchedList
                adapter.notifyDataSetChanged()
            }
        }
    }

    private fun fetchLiveList() {
        liveListStore.fetchLiveList(
            cursor = "",
            count = 20,
            completion = object : CompletionHandler {
                override fun onSuccess() {
                    println("直播列表拉取成功")
                }

                override fun onFailure(code: Int, desc: String) {
                    println("直播列表拉取失败: $desc")
                }
            }
        )
    }

    // 当用户点击列表中的某个Item时
    private fun onLiveItemClick(liveInfo: LiveInfo) {
        // 创建观众观看页面，并将 liveId 传入
        val intent = Intent(this, YourAudienceActivity::class.java)
        intent.putExtra("liveId", liveInfo.liveID)
        startActivity(intent)
    }


    // --- RecyclerView 相关方法 ---
    private fun setupUI() {
        recyclerView = findViewById(R.id.recyclerView)
        adapter = LiveListAdapter(liveList) { liveInfo ->
            onLiveItemClick(liveInfo)
        }
        recyclerView.layoutManager = GridLayoutManager(this, 2)
        recyclerView.adapter = adapter
    }

    override fun onDestroy() {
        super.onDestroy()
        coroutineScope.cancel()
    }
}

// RecyclerView Adapter
class LiveListAdapter(
    private var liveList: List<LiveInfo>,
    private val onItemClick: (LiveInfo) -> Unit
) : RecyclerView.Adapter<LiveListAdapter.LiveViewHolder>() {

    class LiveViewHolder(itemView: View) : RecyclerView.ViewHolder(itemView) {
        // 定义您的ViewHolder视图组件
        // val titleTextView: TextView = itemView.findViewById(R.id.titleTextView)
        // val coverImageView: ImageView = itemView.findViewById(R.id.coverImageView)
    }

    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): LiveViewHolder {
        val view = LayoutInflater.from(parent.context)
            .inflate(R.layout.item_live_card, parent, false)
        return LiveViewHolder(view)
    }

    override fun onBindViewHolder(holder: LiveViewHolder, position: Int) {
        val liveInfo = liveList[position]
        // 设置数据到ViewHolder
        // holder.titleTextView.text = liveInfo.liveName
        // 加载封面图片等

        holder.itemView.setOnClickListener {
            onItemClick(liveInfo)
        }
    }

    override fun getItemCount(): Int = liveList.size
}

```

**LiveInfo 参数说明**
<table>
<tr>
<td rowspan="1" colSpan="1" >**参数名**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`liveID`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >直播间的唯一标识符</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`liveName`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >直播间的标题</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`coverURL`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >直播间的封面图片地址</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`liveOwner`</td>

<td rowspan="1" colSpan="1" >[LiveUserInfo](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-live-user-info/index.html)</td>

<td rowspan="1" colSpan="1" >房主的个人信息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`totalViewerCount`</td>

<td rowspan="1" colSpan="1" >`Int`</td>

<td rowspan="1" colSpan="1" >直播间的总观看人数</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`categoryList`</td>

<td rowspan="1" colSpan="1" >`List<Int>`</td>

<td rowspan="1" colSpan="1" >直播间的分类标签列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`notice`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >直播间的公告信息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`metaData`</td>

<td rowspan="1" colSpan="1" >`Map<String: String>`</td>

<td rowspan="1" colSpan="1" >开发者自定义的元数据，用于实现复杂的业务场景</td>
</tr>
</table>


## 功能进阶

### 场景一：实现直播列表的分类展示

在 App 的直播广场页，顶部设有"热门"、"音乐"、"游戏"等分类标签。用户点击不同的标签后，下方的直播列表会动态筛选，只展示对应分类的直播间，从而帮助用户快速发现感兴趣的内容。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032603567/ecdcbe1db00311f09e195254007c27c5.png)


#### 实现方式

核心是利用 `LiveInfo` 模型中的 `categoryList` 属性。当主播开播设置分类后，`fetchLiveList` 返回的 `LiveInfo` 对象中就会包含这些分类信息。您的 App 在获取到完整的直播列表后，只需在客户端根据用户选择的分类，对这个列表进行一次简单的筛选，然后刷新 UI 即可。

#### 代码示例

以下示例展示了如何在 `LiveListActivity` 中扩展一个 `LiveListManager` 来处理数据和筛选逻辑。
``` kotlin
import android.os.Bundle
import androidx.appcompat.app.AppCompatActivity
import androidx.recyclerview.widget.RecyclerView
import io.trtc.tuikit.atomicxcore.api.live.LiveInfo
import io.trtc.tuikit.atomicxcore.api.live.LiveListStore
import kotlinx.coroutines.*
import kotlinx.coroutines.flow.*

// 1. 创建一个数据管理器来封装数据获取和筛选逻辑
class LiveListManager {
    private val liveListStore = LiveListStore.shared()
    private var fullLiveList: List<LiveInfo> = emptyList()

    // 对外暴露最终的直播列表
    private val _filteredLiveList = MutableStateFlow<List<LiveInfo>>(emptyList())
    val filteredLiveList: StateFlow<List<LiveInfo>> = _filteredLiveList

    init {
        // 监听完整列表变化
        CoroutineScope(Dispatchers.Main).launch {
            liveListStore.liveState.liveList.collect { fetchedList ->
                fullLiveList = fetchedList
                // 默认将完整列表发布出去
                _filteredLiveList.value = fetchedList
            }
        }
    }

    fun fetchFirstPage() {
        liveListStore.fetchLiveList(cursor = "", count = 20, completion = null)
    }

    /// 根据分类筛选直播列表
    fun filterLiveList(categoryId: Int?) {
        if (categoryId == null) {
            // 如果 categoryId 为 null，则显示完整列表
            _filteredLiveList.value = fullLiveList
            return
        }

        val filteredList = fullLiveList.filter { liveInfo ->
            liveInfo.categoryList.contains(categoryId)
        }
        _filteredLiveList.value = filteredList
    }
}

// 2. 在您的 LiveListActivity 中使用 Manager
class LiveListActivity : AppCompatActivity() {
    private val manager = LiveListManager()
    private lateinit var recyclerView: RecyclerView

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_live_list)
        // setupUI()

        // 绑定数据
        CoroutineScope(Dispatchers.Main).launch {
            manager.filteredLiveList.collect { filteredList ->
                // 刷新UI
               // adapter.updateList(filteredList)
            }
        }

        // 首次拉取
        manager.fetchFirstPage()
    }

    // 当用户点击顶部分类标签时
    fun onCategorySelected(categoryId: Int) {
        manager.filterLiveList(categoryId)
    }

    // ... (RecyclerView 相关代码)
}
```

### 场景二：实现直播列表的滑动播放

用户可以通过上下滑动来切换直播间，当一个新的直播间滑动到屏幕中央时，视频会自动开始播放预览；当它滑出屏幕时，视频则会自动停止，以节省带宽和设备性能。

#### 交互流程图

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032603567/81f42bdcb00411f0a6a2525400e889b2.webp)


#### 实现方式

`LiveCoreView` 支持多实例使用，我们为每一个 `RecyclerView.ViewHolder` 都创建一个独立的 `LiveCoreView` 实例。通过监听 `RecyclerView` 的滚动状态，我们可以精确地控制即将出现和已经离开屏幕的 ViewHolder 中的 `LiveCoreView` 何时开始和停止拉流，从而实现“即滑即播、即走即停”的效果。

#### 代码示例

我们创建一个自定义的 `LiveFeedViewHolder`，它内部持有一个 `LiveCoreView`。然后在 Activity 中管理这些 ViewHolder 的播放状态。
``` kotlin
import android.os.Bundle
import android.view.LayoutInflater
import android.view.View
import android.view.ViewGroup
import androidx.appcompat.app.AppCompatActivity
import androidx.recyclerview.widget.LinearLayoutManager
import androidx.recyclerview.widget.RecyclerView
import io.trtc.tuikit.atomicxcore.api.live.LiveInfo
import io.trtc.tuikit.atomicxcore.api.view.CoreViewType
import io.trtc.tuikit.atomicxcore.api.view.LiveCoreView

// 1. 自定义 RecyclerView.ViewHolder，内部包含一个 LiveCoreView
class LiveFeedViewHolder(itemView: View) : RecyclerView.ViewHolder(itemView) {
    private var liveCoreView: LiveCoreView? = null
    
    fun setLiveInfo(liveInfo: LiveInfo) {
        // 为新的直播信息创建一个新的 LiveCoreView
        liveCoreView = LiveCoreView(itemView.context, viewType = CoreViewType.PLAY_VIEW)
        liveCoreView?.let { view ->
            (itemView as ViewGroup).addView(view)
            view.layoutParams = ViewGroup.LayoutParams(
                ViewGroup.LayoutParams.MATCH_PARENT,
                ViewGroup.LayoutParams.MATCH_PARENT
            )
        }
    }

    fun startPlay(roomId: String) {
        liveCoreView?.startPreviewLiveStream(roomId, false, callback = null)
    }
    
    fun stopPlay(roomId: String) {
        liveCoreView?.stopPreviewLiveStream(roomId)
    }
}

// 2. 在 Activity 中管理播放逻辑
class LiveFeedActivity : AppCompatActivity() {
    
    private lateinit var recyclerView: RecyclerView
    private var liveList: List<LiveInfo> = emptyList()
    private var currentPlayingPosition: Int = -1

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_live_feed)
        setupRecyclerView()
    }

    private fun setupRecyclerView() {
        recyclerView = findViewById(R.id.recyclerView)
        recyclerView.layoutManager = LinearLayoutManager(this, LinearLayoutManager.VERTICAL, false)
        recyclerView.adapter = LiveFeedAdapter(liveList) { position ->
            playVideoAtPosition(position)
        }

        // 监听滚动状态
        recyclerView.addOnScrollListener(object : RecyclerView.OnScrollListener() {
            override fun onScrollStateChanged(recyclerView: RecyclerView, newState: Int) {
                super.onScrollStateChanged(recyclerView, newState)
                if (newState == RecyclerView.SCROLL_STATE_IDLE) {
                    val layoutManager = recyclerView.layoutManager as LinearLayoutManager
                    val firstVisiblePosition = layoutManager.findFirstCompletelyVisibleItemPosition()
                    if (firstVisiblePosition != RecyclerView.NO_POSITION) {
                        playVideoAtPosition(firstVisiblePosition)
                    }
                }
            }
        })
    }

    private fun playVideoAtPosition(position: Int) {
        // 只有当居中的位置变化时才切换播放
        if (currentPlayingPosition != position) {
            // 停止当前播放
            if (currentPlayingPosition != -1) {
                val currentViewHolder = recyclerView.findViewHolderForAdapterPosition(currentPlayingPosition)
                if (currentViewHolder is LiveFeedViewHolder) {
                    val liveInfo = liveList[currentPlayingPosition]
                    currentViewHolder.stopPlay(liveInfo.liveID)
                }
            }
            
            // 开始新的播放
            val newViewHolder = recyclerView.findViewHolderForAdapterPosition(position)
            if (newViewHolder is LiveFeedViewHolder) {
                val liveInfo = liveList[position]
                newViewHolder.startPlay(liveInfo.liveID)
                currentPlayingPosition = position
            }
        }
    }
    
    // RecyclerView Adapter
    inner class LiveFeedAdapter(
        private var liveList: List<LiveInfo>,
        private val onItemClick: (Int) -> Unit
    ) : RecyclerView.Adapter<LiveFeedViewHolder>() {
        
        override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): LiveFeedViewHolder {
            val view = LayoutInflater.from(parent.context)
                .inflate(R.layout.item_live_feed, parent, false)
            return LiveFeedViewHolder(view)
        }

        override fun onBindViewHolder(holder: LiveFeedViewHolder, position: Int) {
            val liveInfo = liveList[position]
            holder.setLiveInfo(liveInfo)
            holder.itemView.setOnClickListener {
                onItemClick(position)
            }
        }

        override fun getItemCount(): Int = liveList.size
    }
}
```

### 场景三：实现电商直播的商品信息展示

在电商直播中，主播正在讲解一款商品。此时，所有观众的直播画面下方都会弹出一张商品卡片，实时展示该商品的图片、名称和价格。当主播切换讲解下一件商品时，所有观众端的卡片都会自动、同步更新。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032603567/5b85e0b5b00611f0995e525400454e06.png)


#### 实现方式

主播端将当前商品的结构化信息（建议使用 **JSON **格式）通过 `updateLiveMetaData` 接口设置到一个自定义的 key（例如 "`product_info`"）中。**AtomicXCore** 会将这个变更实时同步给所有观众。观众端只需订阅 `LiveListStore.liveState.currentLive`，监听 `metaData` 的变化，一旦发现 `product_info` 的值更新，就解析其中的 JSON 数据并刷新商品卡片 UI。

#### 代码示例
``` kotlin
import android.os.Bundle
import androidx.appcompat.app.AppCompatActivity
import io.trtc.tuikit.atomicxcore.api.CompletionHandler
import io.trtc.tuikit.atomicxcore.api.live.LiveListStore
import org.json.JSONObject
import org.json.JSONException
import kotlinx.coroutines.*
import kotlinx.coroutines.flow.*

// 1. 定义一个商品信息数据类
data class Product(
    val id: String,
    val name: String,
    val price: String,
    val imageUrl: String
)

// 2. 主播端：在 YourAnchorActivity 中添加推送商品的方法
class YourAnchorActivity : AppCompatActivity() {
    fun pushProductInfo(product: Product) {
        try {
            val jsonObject = JSONObject().apply {
                put("id", product.id)
                put("name", product.name)
                put("price", product.price)
                put("imageUrl", product.imageUrl)
            }
            val jsonString = jsonObject.toString()


            val metaData = hashMapOf("product_info" to jsonString)


            // 使用全局单例的 liveListStore 来更新 metaData
            LiveListStore.shared().updateLiveMetaData(
                metaData,
                object : CompletionHandler {
                    override fun onSuccess() {
                        println("商品 ${product.name} 信息推送成功")
                    }

                    override fun onFailure(code: Int, desc: String) {
                        println("商品信息推送失败: $desc")
                    }
                }
            )
        } catch (e: JSONException) {
            println("JSON序列化失败: ${e.message}")
        }
    }
}

// 3. 观众端：在 YourAudienceActivity 中订阅并响应
class YourAudienceActivity : AppCompatActivity() {

    private val liveListStore = LiveListStore.shared()
    private val coroutineScope = CoroutineScope(Dispatchers.Main)
    // 假设您有一个自定义的商品卡片视图
    // private lateinit var productCardView: ProductCardView

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_audience)
        // ... (setupUI, 布局 productCardView)
        joinLive()
        subscribeToProductUpdates()
    }

    private fun subscribeToProductUpdates() {
        coroutineScope.launch {
            liveListStore.liveState.currentLive.collect { currentLive ->
                val productInfoJson = currentLive.metaData["product_info"]
                if (productInfoJson != null) {
                    try {
                        val jsonObject = JSONObject(productInfoJson)
                        val product = Product(
                            id = jsonObject.getString("id"),
                            name = jsonObject.getString("name"),
                            price = jsonObject.getString("price"),
                            imageUrl = jsonObject.getString("imageUrl")
                        )
                        // productCardView.updateProduct(product)
                        // productCardView.show()
                    } catch (e: JSONException) {
                        println("商品信息解析失败: ${e.message}")
                        // productCardView.hide()
                    }
                } else {
                    // productCardView.hide() // 如果没有商品信息，则隐藏卡片
                }
            }
        }
    }

    override fun onDestroy() {
        super.onDestroy()
        coroutineScope.cancel()
    }

    // ... (joinLive 和 leaveLive 方法)
}

```

## API 文档

关于 [LiveListStore](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-live-list-store/index.html) 及其相关类的所有公开接口、属性和方法的详细信息，请参阅随 [AtomicXCore](https://tencent-rtc.github.io/TUIKit_Android/index.html) 框架的官方 API 文档。本文档使用到的相关 Store 如下：
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
<td rowspan="1" colSpan="1" >LiveListStore</td>

<td rowspan="1" colSpan="1" >直播间全生命周期管理：创建 / 加入 / 离开 / 销毁房间，查询房间列表，修改直播信息（名称、公告等），监听直播状态（例如被踢出、结束）。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-live-list-store/index.html)</td>
</tr>
</table>


## 常见问题

### 使用 `updateLiveMetaData` 时有哪些需要注意的限制和规则？

为了保证系统的稳定和高效，`metaData` 的使用遵循以下规则：
- **权限**: 只有房主和管理员可以调用 `updateLiveMetaData`。普通观众没有权限。

- **数量与大小限制**：

  - 单个房间最多支持 **10** 个 key。

  - 每个 key 的长度不超过 **50 字节**，每个 value 的长度不超过 **2KB**。

  - 单个房间所有 value 的总大小不超过 **16KB**。

- **冲突解决**： `metaData` 的更新机制是"后来者覆盖"。如果多个管理员在短时间内修改同一个 key，最后一次的修改会生效。建议在业务设计上避免多人同时修改同一个关键信息。
