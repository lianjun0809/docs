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
import io.trtc.tuikit.atomicxcore.api.*
import io.trtc.tuikit.atomicxcore.api.CompletionHandler
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
import io.trtc.tuikit.atomicxcore.api.*
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
    private lateinit var adapter: LiveListAdapter

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

### 场景二：实现语聊房内的自定义状态同步

在语聊房中，主播可能需要向所有观众同步一些自定义信息，例如“当前房间话题”、“背景音乐信息”等。`LiveListStore` 的 `MetaData` 功能可以实现这一点。

#### 实现方式：

主播端将自定义信息通过 `updateLiveMetaData` 接口设置到一个或多个 `key` 中。`AtomicXCore` 会将这个变更实时同步给所有观众。观众端只需订阅` LiveListState.currentLive`，监听 `metaData` 的变化，一旦发现关心的 `key` 更新，就解析其 `value` 并刷新业务状态。

#### 示例代码：
``` java
import io.trtc.tuikit.atomicxcore.api.LiveListStore
import io.trtc.tuikit.atomicxcore.api.CompletionHandler
import com.google.gson.Gson
import io.trtc.tuikit.atomicxcore.api.MetaDataCompletionHandler

// 1. 定义一个背景音乐模型 (使用 data class)
data class MusicModel(
    val musicId: String,
    val musicName: String
)

// 2. 主播端：在您的主播业务逻辑中，添加推送背景音乐的方法
fun updateBackgroundMusic(music: MusicModel) {
    val gson = Gson()
    val jsonString = gson.toJson(music) ?: ""

    // 将要更新的 metaData
    val metaData = hashMapOf("music_info" to jsonString)

    // 更新 metaData
    LiveListStore.shared()
        .updateLiveMetaData(
            metaData,
            object : CompletionHandler {
                override fun onSuccess() {
                    print("背景音乐 ${music.musicName} 推送成功")
                }

                override fun onFailure(code: Int, desc: String) {
                    print("背景音乐推送失败: $desc")
                }
            }
        )
}

// 3. 观众端：在您的观众业务逻辑中 ，添加监听背景音乐变化的方法
private fun subscribeToDataUpdates() {
    CoroutineScope(Dispatchers.Main).launch {
        LiveListStore.shared()
            .liveState
            .currentLive
            .map { it.metaData }
            .collect {
                val musicInfo = it["music_info"]
                // 刷新业务状态，例如播放新的背景音乐
            }
    }
}

```

## API 文档

关于 [LiveListStore](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-live-list-store/index.html) 及其相关类的所有公开接口、属性和方法的详细信息，请参阅随 [AtomicXCore](https://tencent-rtc.github.io/TUIKit_Android/index.html) 框架的官方 API 文档。本文档使用到的相关 `Store` 如下：
<table>
<tr>
<td rowspan="2" colSpan="1" >**Store/Component**</td>

<td rowspan="2" colSpan="1" >**功能描述**</td>

<td rowspan="2" colSpan="1" >**API 文档**</td>
</tr>

<tr></tr>

<tr>
<td rowspan="1" colSpan="1" >**LiveListStore**</td>

<td rowspan="1" colSpan="1" >直播间全生命周期管理：创建 / 加入 / 离开 / 销毁房间，查询房间列表，修改直播信息（名称、公告等），监听直播状态（例如被踢出、结束）。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-live-list-store/index.html)</td>
</tr>
</table>


## 常见问题

### 语聊房的列表和视频直播的列表数据是同一份吗？

它们的数据是同一份，您不需要分开拉取。`LiveListStore` 是一个全局单例，它负责统一管理应用中所有“直播”房间的生命周期，无论是视频直播还是语聊房。

### **直播列表中如何区分语聊房和视频直播**

`LiveListStore` 本身不区分房间的业务类型。您需要在获取列表后，在客户端的应用层（业务逻辑或 `UI` 层）进行筛选和分类。

我们推荐采用以下两种方式进行区分：

**方式一（推荐）**：**使用 seatLayoutTemplateID 区分**。这是一个用于定义房间布局的模板 `ID`，关于目前已支持的模板 `ID` 和效果，请参阅文档 [开始直播 > 运行效果](https://write.woa.com/document/192834878686547968)。您要在创建房间时指定 `ID`，然后在获取列表时根据 `ID` 范围来识别业务场景。
- **步骤1**：**创建房间时指定 ID **调用 `LiveListStore.shared.createLive` 时，您需要根据业务场景为 `LiveInfo` 的 `seatLayoutTemplateID` 属性传入指定范围的 `ID`：

  - 语聊房场景：传入 1 - 199 范围内的模板 `ID`。

  - 视频直播场景：传入 200 - 999 范围内的模板 `ID`。

- **步骤2**：**获取列表时筛选 **客户端在 `LiveListStore.state.liveList` 中收到列表数据后，通过判断这个 `ID` 值所属的范围判断，从而在进入直播间的时候区分两种业务场景。
   

   > **重要提示：**
   > 

   > 创建房间时，如果传入的 `seatLayoutTemplateID` 范围与您的业务场景（语聊房、视频直播）不匹配，可能会导致麦位布局出现功能异常。
   > 


   **方式二**：**为 **`liveID`** 添加业务前缀。**这是一种可选的、纯粹的应用层约定，用于辅助您在客户端快速筛选。

  - 步**骤1：创建房间时添加前缀 **在您生成 `liveID` 并调用 `createLive` 时，为不同业务类型的 `liveID` 赋予不同的前缀。例如：视频直播的 `ID` 以 “`Live_`” 开头 (例如：`Live_12345`)，语聊房的 `ID` 以 “`voice_`” 开头 (例如：`voice_67890`)。

  - **步骤2：获取列表时检查前缀 **客户端在拉取到列表后，通过检查 `liveID` 字符串的前缀来进行区分。


### 使用 `updateLiveMetaData` 时有哪些需要注意的限制和规则？

为了保证系统的稳定和高效，`metaData` 的使用遵循以下规则：
- **权限**: 只有房主和管理员可以调用 `updateLiveMetaData`。普通观众没有权限。

- **数量与大小限制**：

  - 单个房间最多支持 **10** 个 `key`。

  - 每个 `key` 的长度不超过 **50 字节**，每个 `value` 的长度不超过 **2KB**。

  - 单个房间所有 `value` 的总大小不超过 **16KB**。

- **冲突解决**： `metaData` 的更新机制是“后来者覆盖”。如果多个管理员在短时间内修改同一个 `key`，最后一次的修改会生效。建议在业务设计上避免多人同时修改同一个关键信息。
