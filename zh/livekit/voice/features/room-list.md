> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

## Platform: Android

`LiveListStore` 是 `AtomicXCore` 中负责管理直播房间列表、创建、加入以及维护房间状态的核心模块。通过`LiveListStore`，您可以为您的应用构建完整的直播生命周期管理。

## 核心功能
- **直播列表拉取**：获取当前所有公开的直播间列表，支持分页加载。

- **直播生命周期管理**：提供从创建、开播、加入、离开到结束直播的全套流程接口。

- **直播信息更新**：主播可以随时更新直播间的公开信息，例如封面、公告等。

- **实时事件监听**：监听直播结束、用户被踢出等关键事件。

- **自定义业务数据**：强大的自定义元数据（`MetaData`）能力，允许您在房间内存储和同步任何业务相关的信息，例如直播状态、音乐信息、自定义角色等 。

## 核心概念

在开始集成之前，我们先通过下表了解一下 `LiveListStore` 相关的几个核心概念：
| **核心概念** | **类型** | **核心职责与描述** |
| --- | --- | --- |
| `LiveInfo` | `data class` | 代表一个直播间的所有信息模型。包含了直播ID (`liveID`)、名称 (`liveName`)、房主信息 (`liveOwner`) 以及自定义元数据 (`metaData`) 等。 |
| `LiveListState` | `data class` | 代表直播列表模块的当前状态。其核心属性 liveList 是一个 `StateFlow`，存储了拉取到的直播列表；`currentLive` 则代表用户当前所在的直播间信息。 |
| `LiveListListener` | `abstract class` | 代表直播房间的全局事件。分为 `onLiveEnded` (直播结束) 和 `onKickedOutOfLive` (被踢出直播) 两种，用于处理关键的房间状态变更。 |
| `LiveListStore` | `abstract class` | 代表直播房间的全局事件。分为 `.onLiveEnded` (直播结束) 和 `.onKickedOutOfLive` (被踢出直播) 两种，用于处理关键的房间状态变更。 |

## 实现步骤

### 步骤1：组件集成

请参考 开始直播 集成 **AtomicXCore**，并完成 主播开播 和 观众观看 的功能实现。

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
| **参数名** | **类型** | **描述** |
| --- | --- | --- |
| `liveID` | `String` | 直播间的唯一标识符 |
| `liveName` | `String` | 直播间的标题 |
| `coverURL` | `String` | 直播间的封面图片地址 |
| `liveOwner` | [LiveUserInfo](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-live-user-info/index.html) | 房主的个人信息 |
| `totalViewerCount` | `Int` | 直播间的总观看人数 |
| `categoryList` | `List<Int>` | 直播间的分类标签列表 |
| `notice` | `String` | 直播间的公告信息 |
| `metaData` | `Map<String: String>` | 开发者自定义的元数据，用于实现复杂的业务场景 |

## 功能进阶

### 场景一：实现直播列表的分类展示

在 App 的直播广场页，顶部设有"热门"、"音乐"、"游戏"等分类标签。用户点击不同的标签后，下方的直播列表会动态筛选，只展示对应分类的直播间，从而帮助用户快速发现感兴趣的内容。

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
| **Store/Component** | **功能描述** | **API 文档** |
| --- | --- | --- |
| **LiveListStore** | 直播间全生命周期管理：创建 / 加入 / 离开 / 销毁房间，查询房间列表，修改直播信息（名称、公告等），监听直播状态（例如被踢出、结束）。 | [API 文档](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-live-list-store/index.html) |

## 常见问题

### 语聊房的列表和视频直播的列表数据是同一份吗？

它们的数据是同一份，您不需要分开拉取。`LiveListStore` 是一个全局单例，它负责统一管理应用中所有“直播”房间的生命周期，无论是视频直播还是语聊房。

### **直播列表中如何区分语聊房和视频直播**

`LiveListStore` 本身不区分房间的业务类型。您需要在获取列表后，在客户端的应用层（业务逻辑或 `UI` 层）进行筛选和分类。

我们推荐采用以下两种方式进行区分：

**方式一（推荐）**：**使用 seatLayoutTemplateID 区分**。这是一个用于定义房间布局的模板 `ID`，关于目前已支持的模板 `ID` 和效果，请参阅文档 开始直播 > 运行效果。您要在创建房间时指定 `ID`，然后在获取列表时根据 `ID` 范围来识别业务场景。
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

---

## Platform: iOS

`LiveListStore` 是 `AtomicXCore` 中负责管理直播房间列表、创建、加入以及维护房间状态的核心模块。通过`LiveListStore`，您可以为您的应用构建完整的直播生命周期管理。

## 核心功能
- **直播列表拉取**：获取当前所有公开的直播间列表，支持分页加载。

- **直播生命周期管理**：提供从创建、开播、加入、离开到结束直播的全套流程接口。

- **直播信息更新**：主播可以随时更新直播间的公开信息，例如封面、公告等。

- **实时事件监听**：监听直播结束、用户被踢出等关键事件。

- **自定义业务数据**：强大的自定义元数据（`MetaData`）能力，允许您在房间内存储和同步任何业务相关的信息，例如直播状态、音乐信息、自定义角色等 。

## 核心概念

在开始集成之前，我们先通过下表了解一下 `LiveListStore` 相关的几个核心概念：
| **核心概念** | **类型** | **核心职责与描述** |
| --- | --- | --- |
| `LiveInfo` | `struct` | 代表一个直播间的所有信息模型。包含了直播ID (`liveID`)、名称 (`liveName`)、房主信息 (`liveOwner`) 以及自定义元数据 (`metaData`) 等。 |
| `LiveListState` | `struct` | 代表直播列表模块的当前状态。其核心属性 liveList 是一个 `[LiveInfo] `数组，存储了拉取到的直播列表；`currentLive` 则代表用户当前所在的直播间信息。 |
| `LiveListEvent` | `enum` | 代表直播房间的全局事件。分为 `.onLiveEnded` (直播结束) 和 `.onKickedOutOfLive` (被踢出直播) 两种，用于处理关键的房间状态变更。 |
| `LiveListStore` | `class` | 这是与直播列表和房间生命周期交互的核心管理类。它是一个全局单例 (shared)，负责所有直播房间的创建、加入、信息更新等操作。 |

## 实现步骤

### 步骤1：组件集成

请参考 快速接入 集成 **AtomicXCore**，并完成 搭建基础语聊房的功能实现。

### 步骤2：实现观众从直播列表进入直播间

#### 实现方式：
1. 创建一个展示直播列表的页面，该页面使用 `UICollectionView` 来布局直播间卡片。

2. 当用户点击某个卡片时，获取该直播间的 `liveID`，并跳转到观众观看页面。

   ``` swift
   class LiveListViewController: UIViewController, UICollectionViewDataSource, UICollectionViewDelegate, UICollectionViewDelegateFlowLayout {
   
       private let liveListStore = LiveListStore.shared
       private var cancellables = Set<AnyCancellable>()
       private var liveList: [LiveInfo] = []
       
       private var collectionView: UICollectionView!
   
       override func viewDidLoad() {
           super.viewDidLoad()
           setupUI()
           bindStore()
           fetchLiveList()
       }
       
       private func bindStore() {
           // 订阅 state，自动接收列表更新
           liveListStore.state
               .subscribe(StatePublisherSelector(keyPath: \LiveListState.liveList))           
               .removeDuplicates()
               .receive(on: DispatchQueue.main)
               .sink { [weak self] fetchedList in
                   self?.liveList = fetchedList
                   self?.collectionView.reloadData()
               }
               .store(in: &cancellables)
       }
   
       private func fetchLiveList() {
           liveListStore.fetchLiveList(cursor: "", count: 20) { result in
               if case .failure(let error) = result {
                   print("直播列表拉取失败: \(error.localizedDescription)")
               }
           }
       }
       
       // 当用户点击列表中的某个Cell时
       func collectionView(_ collectionView: UICollectionView, didSelectItemAt indexPath: IndexPath) {
           let selectedLiveInfo = liveList[indexPath.item]
           
           // 创建观众观看页面，并将 liveID 传入
           let audienceVC = YourAudienceViewController(liveID: selectedLiveInfo.liveID)
           audienceVC.modalPresentationStyle = .fullScreen
           present(audienceVC, animated: true)
       }
       
       // --- UICollectionViewDataSource, Delegate, and UI setup methods ---
       private func setupUI() {
           let layout = UICollectionViewFlowLayout()
           // ... (可以自定义您的布局)
           collectionView = UICollectionView(frame: view.bounds, collectionViewLayout: layout)
           collectionView.dataSource = self
           collectionView.delegate = self
           collectionView.register(UICollectionViewCell.self, forCellWithReuseIdentifier: "LiveCell")
           view.addSubview(collectionView)
       }
   
       func collectionView(_ collectionView: UICollectionView, numberOfItemsInSection section: Int) -> Int {
           return liveList.count
       }
       
       func collectionView(_ collectionView: UICollectionView, cellForItemAt indexPath: IndexPath) -> UICollectionViewCell {
           let cell = collectionView.dequeueReusableCell(withReuseIdentifier: "LiveCell", for: indexPath)
           cell.backgroundColor = .lightGray // 自定义您的Cell样式
           // let liveInfo = liveList[indexPath.item]
           // ... (例如: cell.titleLabel.text = liveInfo.liveName)
           return cell
       }
       
       func collectionView(_ collectionView: UICollectionView, layout collectionViewLayout: UICollectionViewLayout, sizeForItemAt indexPath: IndexPath) -> CGSize {
           // 单列、双列布局可通过自定义您的Cell大小来实现
           let width = (view.bounds.width - 30) / 2
           return CGSize(width: width, height: width * 1.2)
       }
   }
   ```

   **LiveInfo 参数说明**

| **参数名** | **类型** | **描述** |
| --- | --- | --- |
| `liveID` | `String` | 直播间的唯一标识符 |
| `liveName` | `String` | 直播间的标题 |
| `coverURL` | `String` | 直播间的封面图片地址 |
| `liveOwner` | [LiveUserInfo](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/liveuserinfo) | 房主的个人信息 |
| `totalViewerCount` | `Int` | 直播间的总观看人数 |
| `categoryList` | `[NSNumber]` | 直播间的分类标签列表 |
| `notice` | `String` | 直播间的公告信息 |
| `metaData` | `[String: String]` | 开发者自定义的元数据，用于实现复杂的业务场景 |

## 功能进阶

### 场景一：实现直播列表的分类展示

在 App 的直播广场页，顶部设有“热门”、“音乐”、“游戏”等分类标签。用户点击不同的标签后，下方的直播列表会动态筛选，只展示对应分类的直播间，从而帮助用户快速发现感兴趣的内容。

#### 实现方式：

核心是利用 `LiveInfo` 模型中的 `categoryList` 属性。
1. 当主播开播设置分类后，`fetchLiveList` 返回的 `LiveInfo` 对象中就会包含这些分类信息。

2. 您的 App 在获取到完整的直播列表后，只需在客户端根据用户选择的分类，对这个列表进行一次简单的筛选，然后刷新 UI 即可。

#### 代码示例：

以下示例展示了如何在 `LiveListViewController` 中扩展一个 `LiveListManager` 来处理数据和筛选逻辑。
``` swift
import AtomicXCore
import Combine

// 1. 创建一个数据管理器来封装数据获取和筛选逻辑
class LiveListManager {
    private let liveListStore = LiveListStore.shared
    private var cancellables = Set<AnyCancellable>()
    private var fullLiveList: [LiveInfo] = []

    // 对外暴露最终的直播列表
    let filteredLiveListPublisher = CurrentValueSubject<[LiveInfo], Never>([])

    init() {
        liveListStore.state
            .subscribe(StatePublisherSelector(keyPath: \LiveListState.liveList))
            .receive(on: DispatchQueue.main)
            .sink { [weak self] fetchedList in
                self?.fullLiveList = fetchedList
                // 默认将完整列表发布出去
                self?.filteredLiveListPublisher.send(fetchedList)
            }
            .store(in: &cancellables)
    }

    func fetchFirstPage() {
        liveListStore.fetchLiveList(cursor: "", count: 20) { _ in }
    }

    /// 根据分类筛选直播列表
    func filterLiveList(by categoryId: NSNumber?) {
        guard let categoryId = categoryId else {
            // 如果 categoryId 为 nil，则显示完整列表
            filteredLiveListPublisher.send(fullLiveList)
            return
        }

        let filteredList = fullLiveList.filter { liveInfo in
            liveInfo.categoryList.contains(categoryId)
        }
        filteredLiveListPublisher.send(filteredList)
    }
}
```
``` swift
// 2. 在您的 LiveListViewController 中使用 Manager
class LiveListViewController: UIViewController {
    private let manager = LiveListManager()
    private var cancellables = Set<AnyCancellable>()
    private var liveList: [LiveInfo] = []
    private var collectionView: UICollectionView!

    override func viewDidLoad() {
        super.viewDidLoad()
        // ... setupUI ...

        // 绑定数据
        manager.filteredLiveListPublisher
            .receive(on: DispatchQueue.main)
            .sink { [weak self] filteredList in
                self?.liveList = filteredList
                self?.collectionView.reloadData()
            }
            .store(in: &cancellables)

        // 首次拉取
        manager.fetchFirstPage()
    }

    // 当用户点击顶部分类标签 (UISegmentedControl) 时
    @objc func categorySegmentDidChange(_ sender: UISegmentedControl) {
        let selectedCategoryId: NSNumber? = 1 // 假设 "音乐" 分类的ID是 1
        manager.filterLiveList(by: selectedCategoryId)
    }

    // ... (UICollectionView 相关代码)
}

```

### 场景二：实现语聊房内的自定义状态同步

在语聊房中，主播可能需要向所有观众同步一些自定义信息，例如“当前房间话题”、“背景音乐信息”等。`LiveListStore` 的 `MetaData` 功能可以实现这一点。

#### 实现方式：
1. 主播端将自定义信息（建议使用 JSON 格式）通过 `updateLiveMetaData` 接口设置到一个或多个 key 中。`AtomicXCore` 会将这个变更实时同步给所有观众。

2. 观众端只需订阅` LiveListState.currentLive`，监听 `metaData` 的变化，一旦发现关心的 key 更新，就解析其 value 并刷新业务状态。

#### 示例代码：
``` swift
import AtomicXCore
import Combine

// 1. 定义一个背景音乐模型 (可选，建议使用 Codable)
struct MusicModel: Codable {
    let musicId: String
    let musicName: String
}

// 2. 主播端：在您的主播业务逻辑中，添加推送背景音乐的方法
func updateBackgroundMusic(music: MusicModel) {
    guard let jsonData = try? JSONEncoder().encode(music),
            let jsonString = String(data: jsonData, encoding: .utf8) else { return }

    // 将要更新的元数据
    let metaData = ["music_info": jsonString]

    // 使用全局单例的 liveListStore 来更新 metaData
    LiveListStore.shared.updateLiveMetaData(metaData) { result in
        if case .success = result {
            print("背景音乐 \(music.musicName) 推送成功")
        } else if case .failure(let error) = result {
            print("背景音乐推送失败: \(error.message)")
        }
    }
}

// 3. 观众端：在您的观众业务逻辑中，订阅并响应
private func subscribeToDataUpdates() {
        LiveListStore.shared.state
            // 监听当前房间的 metaData
            .subscribe(StatePublisherSelector(keyPath: \LiveListState.currentLive))
            .map { $0.metaData["music_info"]}
            .removeDuplicates()
            .receive(on: DispatchQueue.main)
            .sink { jsonString in
                guard let jsonString = jsonString,
                      let data = jsonString.data(using: .utf8),
                      let music = try? JSONDecoder().decode(MusicModel.self, from: data) else {
                    // 刷新业务状态，播放新的音乐
                  // ... (例如: playMusic(music))
                    return
                }
               
            }
            .store(in: &cancellables)
    }

```

关于 [LiveListStore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/liveliststore) 及其相关类的所有公开接口、属性和方法的详细信息，请参阅随 [AtomicXCore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore) 框架的官方 API 文档。本文档使用到的相关 Store 如下：
| **Store/Component** | **功能描述** | **API 文档** |
| --- | --- | --- |
| LiveListStore | 直播间全生命周期管理：创建 / 加入 / 离开 / 销毁房间，查询房间列表，修改直播信息（名称、公告等），监听直播状态（例如被踢出、结束）。 | [API 文档](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/liveliststore) |

## 常见问题

### 语聊房的列表和视频直播的列表数据是同一份吗？

它们的数据是同一份，您不需要分开拉取。`LiveListStore` 是一个全局单例，它负责统一管理应用中所有“直播”房间的生命周期，无论是视频直播还是语聊房。

### **直播列表中如何区分语聊房和视频直播**

`LiveListStore` 本身不区分房间的业务类型。您需要在获取列表后，在客户端的应用层（业务逻辑或 UI 层）进行筛选和分类。

我们推荐采用以下两种方式进行区分：

**方式一（推荐）：使用 seatLayoutTemplateID 区分**。这是一个用于定义房间布局的模板 ID，关于目前已支持的模板 ID 和效果，请参阅文档开始直播-运行效果。您要在创建房间时指定 ID，然后在获取列表时根据 ID 范围来识别业务场景。
- **步骤1：创建房间时指定 ID **调用 LiveListStore.shared.createLive 时，您需要根据业务场景为 LiveInfo 的 seatLayoutTemplateID 属性传入指定范围的 ID：

  - 语聊房场景：传入 1 - 199 范围内的模板 ID。

  - 视频直播场景：传入 200 - 999 范围内的模板 ID。

- **步骤2：获取列表时筛选 **客户端在 `LiveListStore.state.liveList`中收到列表数据后，通过判断这个 ID 值所属的范围来区分，从而在进入直播间的时候区分两种业务场景。
   

   > **重要提示：**
   > 

   > 创建房间时，如果传入的 seatLayoutTemplateID 范围与您的业务场景（语聊房、视频直播）不匹配，可能会导致麦位布局出现功能异常。
   > 

   **方式二**：**为 **`liveID`** 添加业务前缀。**这是一种可选的、纯粹的应用层约定，用于辅助您在客户端快速筛选。

  - **步骤1：创建房间时添加前缀 **在您生成 liveID 并调用 createLive 时，为不同业务类型的 liveID 赋予不同的前缀。例如：视频直播的 ID 以 “Live_” 开头 (例如：Live_12345)，语聊房的 ID 以 “voice_” 开头 (例如：voice_67890)。

  - **步骤2：获取列表时检查前缀 **客户端在拉取到列表后，通过检查 liveID 字符串的前缀来进行区分。

### 使用 `updateLiveMetaData` 时有哪些需要注意的限制和规则？

为了保证系统的稳定和高效，`metaData` 的使用遵循以下规则：
- **权限**：只有房主和管理员可以调用 `updateLiveMetaData`。普通观众没有权限。

- **数量与大小限制：**

  - 单个房间最多支持 **10** 个 key。

  - 每个 key 的长度不超过 **50 字节**，每个 value 的长度不超过 **2KB**。

  - 单个房间所有 value 的总大小不超过 **16KB**。

- **冲突解决**： `metaData` 的更新机制是“后来者覆盖”。如果多个管理员在短时间内修改同一个 key，最后一次的修改会生效。建议在业务设计上避免多人同时修改同一个关键信息。

---

## Platform: Flutter

`LiveListStore` 是 `AtomicXCore` 中负责管理直播房间列表、创建、加入以及维护房间状态的核心模块。通过`LiveListStore`，开发者可以为应用构建完整的直播生命周期管理。

## 核心功能
- **直播列表拉取**：获取当前所有公开的直播间列表，支持分页加载。

- **直播生命周期管理**：提供从创建、开播、加入、离开到结束直播的全套流程接口。

- **直播信息更新**：主播可以随时更新直播间的公开信息，例如封面、公告等。

- **实时事件监听**：监听直播结束、用户被踢出等关键事件。

- **自定义业务数据**：强大的自定义元数据（`MetaData`）能力，允许您在房间内存储和同步任何业务相关的信息，例如直播状态、音乐信息、自定义角色等。

## 核心概念

在开始集成之前，下表介绍了 `LiveListStore` 相关的核心概念：
| **核心概念** | **类型** | **核心职责与描述** |
| --- | --- | --- |
| [LiveInfo](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_live_list_store/LiveInfo-class.html) | `class` | 代表一个直播间的所有信息模型。包含了直播 ID (`liveID`)、名称 (`liveName`)、房主信息 (`liveOwner`) 以及自定义元数据 (`metaData`) 等。 |
| [LiveListState](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_live_list_store/LiveListState-class.html) | `class` | 代表直播列表模块的当前状态。其核心属性 `liveList` 是一个 `ValueListenable<List<LiveInfo>>` 类型，存储了拉取到的直播列表；`currentLive` 则代表用户当前所在的直播间信息。 |
| [LiveListListener](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_live_list_store/LiveListListener-class.html) | `class` | 代表直播房间的全局事件监听器。包含 `onLiveEnded` (直播结束) 和 `onKickedOutOfLive` (被踢出直播) 两种回调，用于处理关键的房间状态变更。 |
| [LiveListStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_live_list_store/LiveListStore-class.html) | `class` | 这是与直播列表和房间生命周期交互的核心管理类。它是一个全局单例 (`shared`)，负责所有直播房间的创建、加入、信息更新等操作。 |

## 实现步骤

### 步骤1：组件集成

参考 快速接入 集成 **AtomicXCore**，并完成 构建基础语聊房应用 的功能实现。

### 步骤2：实现观众从直播列表进入直播间

#### 实现方式
1. 创建一个展示直播列表的页面，该页面使用 `GridView` 来布局直播间卡片。

2. 当用户点击某个卡片时，获取该直播间的 `liveID`，并跳转到观众观看页面。

#### 代码示例
``` java
import 'package:flutter/material.dart';
import 'package:atomic_x_core/atomicxcore.dart';

/// 直播列表页面
class LiveListPage extends StatefulWidget {
  const LiveListPage({super.key});

  @override
  State<LiveListPage> createState() => _LiveListPageState();
}

class _LiveListPageState extends State<LiveListPage> {
  final _liveListStore = LiveListStore.shared;
  final ScrollController _scrollController = ScrollController();
  bool _isLoading = false;
  late final VoidCallback _liveListListener = _onLiveListChanged;

  @override
  void initState() {
    super.initState();
    _liveListStore.liveState.liveList.addListener(_liveListListener);
    _scrollController.addListener(_onScroll);
    _fetchLiveList();
  }

  void _onLiveListChanged() {
    setState(() {});
  }

  void _onScroll() {
    // 滚动到底部时加载更多
    if (_scrollController.position.pixels >=
        _scrollController.position.maxScrollExtent - 200) {
      _loadMore();
    }
  }

  Future<void> _fetchLiveList() async {
    if (_isLoading) return;
    setState(() => _isLoading = true);

    final result = await _liveListStore.fetchLiveList(cursor: '', count: 20);
    if (!result.isSuccess) {
      debugPrint('直播列表拉取失败: ${result.message}');
    }

    setState(() => _isLoading = false);
  }

  Future<void> _loadMore() async {
    if (_isLoading) return;

    final cursor = _liveListStore.liveState.liveListCursor.value;
    if (cursor.isEmpty) return; // 没有更多数据

    setState(() => _isLoading = true);
    await _liveListStore.fetchLiveList(cursor: cursor, count: 20);
    setState(() => _isLoading = false);
  }

  Future<void> _refresh() async {
    _liveListStore.reset();
    await _fetchLiveList();
  }

  // 当用户点击列表中的某个卡片时
  void _onLiveCardTap(LiveInfo liveInfo) {
    // 创建观众观看页面，并将 liveID 传入
    Navigator.push(
      context,
      MaterialPageRoute(
        builder: (context) => YourAudiencePage(liveID: liveInfo.liveID),
      ),
    );
  }

  @override
  void dispose() {
    _liveListStore.liveState.liveList.removeListener(_liveListListener);
    _scrollController.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    final liveList = _liveListStore.liveState.liveList.value;

    return Scaffold(
      appBar: AppBar(title: const Text('直播列表')),
      body: RefreshIndicator(
        onRefresh: _refresh,
        child: liveList.isEmpty
            ? Center(
                child: _isLoading
                    ? const CircularProgressIndicator()
                    : const Text('暂无直播'),
              )
            : GridView.builder(
                controller: _scrollController,
                padding: const EdgeInsets.all(8),
                gridDelegate: const SliverGridDelegateWithFixedCrossAxisCount(
                  crossAxisCount: 2,
                  childAspectRatio: 0.75,
                  crossAxisSpacing: 8,
                  mainAxisSpacing: 8,
                ),
                itemCount: liveList.length + (_isLoading ? 1 : 0),
                itemBuilder: (context, index) {
                  if (index >= liveList.length) {
                    return const Center(child: CircularProgressIndicator());
                  }
                  return _buildLiveCard(liveList[index]);
                },
              ),
      ),
    );
  }

  Widget _buildLiveCard(LiveInfo liveInfo) {
    return GestureDetector(
      onTap: () => _onLiveCardTap(liveInfo),
      child: Card(
        clipBehavior: Clip.antiAlias,
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            // 封面图
            Expanded(
              child: Stack(
                fit: StackFit.expand,
                children: [
                  Image.network(
                    liveInfo.coverURL,
                    fit: BoxFit.cover,
                    errorBuilder: (context, error, stackTrace) {
                      return Container(color: Colors.grey[300]);
                    },
                  ),
                  // 直播中标签
                  Positioned(
                    top: 8,
                    left: 8,
                    child: Container(
                      padding: const EdgeInsets.symmetric(
                        horizontal: 6,
                        vertical: 2,
                      ),
                      decoration: BoxDecoration(
                        color: Colors.red,
                        borderRadius: BorderRadius.circular(4),
                      ),
                      child: const Text(
                        '直播中',
                        style: TextStyle(color: Colors.white, fontSize: 10),
                      ),
                    ),
                  ),
                  // 观看人数
                  Positioned(
                    bottom: 8,
                    right: 8,
                    child: Container(
                      padding: const EdgeInsets.symmetric(
                        horizontal: 6,
                        vertical: 2,
                      ),
                      decoration: BoxDecoration(
                        color: Colors.black54,
                        borderRadius: BorderRadius.circular(4),
                      ),
                      child: Row(
                        mainAxisSize: MainAxisSize.min,
                        children: [
                          const Icon(
                            Icons.visibility,
                            color: Colors.white,
                            size: 12,
                          ),
                          const SizedBox(width: 4),
                          Text(
                            '${liveInfo.totalViewerCount}',
                            style: const TextStyle(
                              color: Colors.white,
                              fontSize: 10,
                            ),
                          ),
                        ],
                      ),
                    ),
                  ),
                ],
              ),
            ),
            // 直播信息
            Padding(
              padding: const EdgeInsets.all(8),
              child: Column(
                crossAxisAlignment: CrossAxisAlignment.start,
                children: [
                  Text(
                    liveInfo.liveName,
                    maxLines: 1,
                    overflow: TextOverflow.ellipsis,
                    style: const TextStyle(fontWeight: FontWeight.bold),
                  ),
                  const SizedBox(height: 4),
                  Row(
                    children: [
                      CircleAvatar(
                        radius: 10,
                        backgroundImage: NetworkImage(
                          liveInfo.liveOwner.avatarURL,
                        ),
                      ),
                      const SizedBox(width: 4),
                      Expanded(
                        child: Text(
                          liveInfo.liveOwner.userName,
                          maxLines: 1,
                          overflow: TextOverflow.ellipsis,
                          style: TextStyle(
                            fontSize: 12,
                            color: Colors.grey[600],
                          ),
                        ),
                      ),
                    ],
                  ),
                ],
              ),
            ),
          ],
        ),
      ),
    );
  }
}

/// 观众观看页面（占位）
class YourAudiencePage extends StatelessWidget {
  final String liveID;

  const YourAudiencePage({super.key, required this.liveID});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('直播间')),
      body: Center(child: Text('直播间: $liveID')),
    );
  }
}
```

**LiveInfo 参数说明**
| **参数名** | **类型** | **描述** |
| --- | --- | --- |
| `liveID` | `String` | 直播间的唯一标识符 |
| `liveName` | `String` | 直播间的标题 |
| `coverURL` | `String` | 直播间的封面图片地址 |
| `liveOwner` | `LiveUserInfo` | 房主的个人信息 |
| `totalViewerCount` | `int` | 直播间的总观看人数 |
| `categoryList` | `List<int>` | 直播间的分类标签列表 |
| `notice` | `String` | 直播间的公告信息 |
| `metaData` | `Map<String, String>` | 开发者自定义的元数据，用于实现复杂的业务场景 |

## 功能进阶

### 场景一：分类展示直播列表

在 App 的直播广场页，顶部设有“热门”、“音乐”、“游戏”等分类标签。用户点击不同的标签后，下方的直播列表会动态筛选，只展示对应分类的直播间，从而帮助用户快速发现感兴趣的内容。

#### 实现方式

核心是利用 `LiveInfo` 模型中的 `categoryList` 属性。
1. 当主播开播设置分类后，`fetchLiveList` 返回的 `LiveInfo` 对象中就会包含这些分类信息。

2. 您的 App 在获取到完整的直播列表后，只需在客户端根据用户选择的分类，对这个列表进行一次简单的筛选，然后刷新 UI 即可。

#### 代码示例

以下示例展示了如何创建一个 `LiveListManager` 来处理数据和筛选逻辑。
``` java
import 'package:flutter/material.dart';
import 'package:atomic_x_core/atomicxcore.dart';

/// 直播列表数据管理器
class LiveListManager extends ChangeNotifier {
  final _liveListStore = LiveListStore.shared;
  List<LiveInfo> _fullLiveList = [];
  List<LiveInfo> _filteredLiveList = [];
  int? _selectedCategoryId;

  List<LiveInfo> get filteredLiveList => _filteredLiveList;
  int? get selectedCategoryId => _selectedCategoryId;
  
  late final VoidCallback _liveListListener = _onLiveListChanged;

  LiveListManager() {
    _liveListStore.liveState.liveList.addListener(_liveListListener);
  }

  void _onLiveListChanged() {
    _fullLiveList = _liveListStore.liveState.liveList.value;
    _applyFilter();
  }

  Future<void> fetchFirstPage() async {
    _liveListStore.reset();
    await _liveListStore.fetchLiveList(cursor: '', count: 20);
  }

  /// 根据分类筛选直播列表
  void filterLiveList({int? categoryId}) {
    _selectedCategoryId = categoryId;
    _applyFilter();
  }

  void _applyFilter() {
    if (_selectedCategoryId == null) {
      // 如果 categoryId 为 null，则显示完整列表
      _filteredLiveList = List.from(_fullLiveList);
    } else {
      // 筛选包含指定分类的直播间
      _filteredLiveList = _fullLiveList.where((liveInfo) {
        return liveInfo.categoryList.contains(_selectedCategoryId);
      }).toList();
    }
    notifyListeners();
  }

  @override
  void dispose() {
    _liveListStore.liveState.liveList.removeListener(_liveListListener);
    super.dispose();
  }
}
```
``` java
/// 带分类筛选的直播列表页面
class CategoryLiveListPage extends StatefulWidget {
  const CategoryLiveListPage({super.key});

  @override
  State<CategoryLiveListPage> createState() => _CategoryLiveListPageState();
}

class _CategoryLiveListPageState extends State<CategoryLiveListPage> {
  final _manager = LiveListManager();
  late final VoidCallback _managerChangedListener = _onManagerChanged;

  // 分类列表（示例）
  final List<Map<String, dynamic>> _categories = [
    {'id': null, 'name': '全部'},
    {'id': 1, 'name': '音乐'},
    {'id': 2, 'name': '游戏'},
    {'id': 3, 'name': '聊天'},
  ];

  @override
  void initState() {
    super.initState();
    _manager.addListener(_managerChangedListener);
    _manager.fetchFirstPage();
  }

  void _onManagerChanged() {
    setState(() {});
  }

  // 当用户点击顶部分类标签时
  void _onCategoryTap(int? categoryId) {
    _manager.filterLiveList(categoryId: categoryId);
  }

  @override
  void dispose() {
    _manager.removeListener(_managerChangedListener);
    _manager.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('直播广场')),
      body: Column(
        children: [
          // 分类标签栏
          SizedBox(
            height: 50,
            child: ListView.builder(
              scrollDirection: Axis.horizontal,
              padding: const EdgeInsets.symmetric(horizontal: 8),
              itemCount: _categories.length,
              itemBuilder: (context, index) {
                final category = _categories[index];
                final isSelected = _manager.selectedCategoryId == category['id'];
                return Padding(
                  padding: const EdgeInsets.symmetric(horizontal: 4),
                  child: ChoiceChip(
                    label: Text(category['name']),
                    selected: isSelected,
                    onSelected: (_) => _onCategoryTap(category['id']),
                  ),
                );
              },
            ),
          ),
          // 直播列表
          Expanded(
            child: _manager.filteredLiveList.isEmpty
                ? const Center(child: Text('暂无直播'))
                : GridView.builder(
                    padding: const EdgeInsets.all(8),
                    gridDelegate:
                        const SliverGridDelegateWithFixedCrossAxisCount(
                      crossAxisCount: 2,
                      childAspectRatio: 0.75,
                      crossAxisSpacing: 8,
                      mainAxisSpacing: 8,
                    ),
                    itemCount: _manager.filteredLiveList.length,
                    itemBuilder: (context, index) {
                      final liveInfo = _manager.filteredLiveList[index];
                      return _buildLiveCard(liveInfo);
                    },
                  ),
          ),
        ],
      ),
    );
  }

  Widget _buildLiveCard(LiveInfo liveInfo) {
    return Card(
      clipBehavior: Clip.antiAlias,
      child: Column(
        crossAxisAlignment: CrossAxisAlignment.start,
        children: [
          Expanded(
            child: Image.network(
              liveInfo.coverURL,
              fit: BoxFit.cover,
              width: double.infinity,
              errorBuilder: (context, error, stackTrace) {
                return Container(color: Colors.grey[300]);
              },
            ),
          ),
          Padding(
            padding: const EdgeInsets.all(8),
            child: Text(
              liveInfo.liveName,
              maxLines: 1,
              overflow: TextOverflow.ellipsis,
            ),
          ),
        ],
      ),
    );
  }
}
```

### 场景二：同步语聊房内自定义状态

在语聊房中，主播可能需要向所有观众同步一些自定义信息，例如“当前房间话题”、“背景音乐信息”等。`LiveListStore` 的 `MetaData` 功能可以实现这一点。

#### 实现方式
1. 主播端将自定义信息（建议使用 JSON 格式）通过 `updateLiveMetaData` 接口设置到一个或多个 key 中。`AtomicXCore` 会将这个变更实时同步给所有观众。

2. 观众端只需订阅 `LiveListState.currentLive`，监听 `metaData` 的变化，一旦发现关心的 key 更新，就解析其 value 并刷新业务状态。

#### 代码示例
``` java
import 'dart:convert';
import 'package:flutter/material.dart';
import 'package:atomic_x_core/atomicxcore.dart';

/// 背景音乐模型
class MusicModel {
  final String musicId;
  final String musicName;

  MusicModel({required this.musicId, required this.musicName});

  factory MusicModel.fromJson(Map<String, dynamic> json) {
    return MusicModel(
      musicId: json['musicId'] ?? '',
      musicName: json['musicName'] ?? '',
    );
  }

  Map<String, dynamic> toJson() {
    return {
      'musicId': musicId,
      'musicName': musicName,
    };
  }
}

/// 主播端：推送背景音乐
class HostMusicController {
  final _liveListStore = LiveListStore.shared;

  Future<void> updateBackgroundMusic(MusicModel music) async {
    final jsonString = jsonEncode(music.toJson());

    // 将要更新的元数据
    final metaData = {'music_info': jsonString};

    // 使用全局单例的 liveListStore 来更新 metaData
    final result = await _liveListStore.updateLiveMetaData(metaData);
    if (result.isSuccess) {
      debugPrint('背景音乐 ${music.musicName} 推送成功');
    } else {
      debugPrint('背景音乐推送失败: ${result.message}');
    }
  }
}

/// 观众端：订阅并响应背景音乐变化
class AudienceMusicWidget extends StatefulWidget {
  const AudienceMusicWidget({super.key});

  @override
  State<AudienceMusicWidget> createState() => _AudienceMusicWidgetState();
}

class _AudienceMusicWidgetState extends State<AudienceMusicWidget> {
  final _liveListStore = LiveListStore.shared;
  MusicModel? _currentMusic;
  String? _lastMusicInfo;
  late final VoidCallback _currentLiveChangedListener = _onCurrentLiveChanged;

  @override
  void initState() {
    super.initState();
    _liveListStore.liveState.currentLive.addListener(_currentLiveChangedListener);
  }

  void _onCurrentLiveChanged() {
    final currentLive = _liveListStore.liveState.currentLive.value;
    final musicInfo = currentLive.metaData['music_info'];

    // 检查是否有变化
    if (musicInfo != _lastMusicInfo) {
      _lastMusicInfo = musicInfo;
      _parseMusicInfo(musicInfo);
    }
  }

  void _parseMusicInfo(String? jsonString) {
    if (jsonString == null || jsonString.isEmpty) {
      setState(() => _currentMusic = null);
      return;
    }

    try {
      final json = jsonDecode(jsonString) as Map<String, dynamic>;
      final music = MusicModel.fromJson(json);
      setState(() => _currentMusic = music);
      // 刷新业务状态，播放新的音乐
      _playMusic(music);
    } catch (e) {
      debugPrint('解析音乐信息失败: $e');
    }
  }

  void _playMusic(MusicModel music) {
    // 实现播放音乐的逻辑
    debugPrint('正在播放: ${music.musicName}');
  }

  @override
  void dispose() {
    _liveListStore.liveState.currentLive.removeListener(_currentLiveChangedListener);
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Container(
      padding: const EdgeInsets.all(8),
      decoration: BoxDecoration(
        color: Colors.black54,
        borderRadius: BorderRadius.circular(8),
      ),
      child: Row(
        mainAxisSize: MainAxisSize.min,
        children: [
          const Icon(Icons.music_note, color: Colors.white, size: 16),
          const SizedBox(width: 4),
          Text(
            _currentMusic?.musicName ?? '暂无音乐',
            style: const TextStyle(color: Colors.white, fontSize: 12),
          ),
        ],
      ),
    );
  }
}
```

## API 文档

关于 [LiveListStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_live_list_store/LiveListStore-class.html) 及其相关类的所有公开接口、属性和方法的详细信息，请参考 [AtomicXCore](https://tencent-rtc.github.io/TUIKit_Flutter) 框架的官方 API 文档。本文档使用到的相关 Store 如下：
| **Store/Component** | **功能描述** | **API 文档** |
| --- | --- | --- |
| LiveListStore | 直播间全生命周期管理：创建 / 加入 / 离开 / 销毁房间，查询房间列表，修改直播信息（名称、公告等），监听直播状态（例如被踢出、结束）。 | [API 文档](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_live_list_store/LiveListStore-class.html) |

## 常见问题

### 语聊房的列表和视频直播的列表数据是同一份吗？

它们的数据是同一份，您不需要分开拉取。`LiveListStore` 是一个全局单例，它负责统一管理应用中所有“直播”房间的生命周期，无论是视频直播还是语聊房。

### 直播列表中如何区分语聊房和视频直播？

`LiveListStore` 本身不区分房间的业务类型。您需要在获取列表后，在客户端的应用层（业务逻辑或 UI 层）进行筛选和分类。

我们推荐采用以下两种方式进行区分：

**方式一（推荐）：使用 seatLayoutTemplateID 区分**

这是一个用于定义房间布局的模板 ID，关于目前已支持的模板 ID 和效果，请参考文档 开始直播-运行效果。您要在创建房间时指定 ID，然后在获取列表时根据 ID 范围来识别业务场景。
- **步骤1：创建房间时指定 ID**

   调用 `LiveListStore.shared.createLive` 时，您需要根据业务场景为 `LiveInfo` 的 `seatLayoutTemplateID` 属性传入指定范围的 ID：

  - 语聊房场景：传入 1-199 范围内的模板 ID。

  - 视频直播场景：传入 200-999 范围内的模板 ID。

- **步骤2：获取列表时筛选**

   客户端在 `liveState.liveList` 中收到列表数据后，通过判断这个 ID 值所属的范围来区分，从而在进入直播间的时候区分两种业务场景。
   

   > **重要提示：**
   > 

   > 创建房间时，如果传入的 `seatLayoutTemplateID` 范围与您的业务场景（语聊房、视频直播）不匹配，可能会导致麦位布局出现功能异常。
   > 

   **方式二：为 **`liveID`** 添加业务前缀**

   这是一种可选的、纯粹的应用层约定，用于辅助您在客户端快速筛选。

- **步骤1：创建房间时添加前缀**

   在您生成 `liveID` 并调用 `createLive` 时，为不同业务类型的 `liveID` 赋予不同的前缀。例如：视频直播的 ID 以 “Live_” 开头 (例如：Live_12345)，语聊房的 ID 以 “voice_” 开头 (例如：voice_67890)。

- **步骤2：获取列表时检查前缀**

   客户端在拉取到列表后，通过检查 `liveID` 字符串的前缀来进行区分。

### 使用 `updateLiveMetaData` 注意事项

为了保证系统的稳定和高效，`metaData` 的使用遵循以下规则：
- **权限**：只有房主和管理员可以调用 `updateLiveMetaData`。普通观众没有权限。

- **数量与大小限制：**

  - 单个房间最多支持 **10** 个 key。

  - 每个 key 的长度不超过 **50 字节**，每个 value 的长度不超过 **2KB**。

  - 单个房间所有 value 的总大小不超过 **16KB**。

- **冲突解决**：`metaData` 的更新机制是“后来者覆盖”。如果多个管理员在短时间内修改同一个 key，最后一次的修改会生效。建议在业务设计上避免多人同时修改同一个关键信息。

---

## Platform: uni-app

`LiveListState` 是 `AtomicXCore` 中负责管理直播房间列表、创建、加入以及维护房间状态的核心模块。通过`LiveListState`，您可以为您的应用构建完整的直播生命周期管理。

## 核心功能
- **直播列表拉取**：获取当前所有公开的直播间列表，支持分页加载。

- **直播生命周期管理**：提供从创建、开播、加入、离开到结束直播的全套流程接口。

- **直播信息更新**：主播可以随时更新直播间的公开信息，例如封面、公告等。

- **实时事件监听**：监听直播结束、用户被踢出等关键事件。

- **自定义业务数据**：强大的自定义元数据（`MetaData`）能力，允许您在房间内存储和同步任何业务相关的信息，例如直播状态、音乐信息、自定义角色等 。

## 实现步骤

### 步骤1：组件集成

请参考 快速接入 集成 **AtomicXCore**，并完成搭建基础语聊房的功能实现。

### 步骤2：实现观众从直播列表进入直播间

创建一个展示直播列表的页面。当用户点击某个卡片时，获取该直播间的 `liveID`，并跳转到观众观看页面。
``` typescript
<template>
  <view class="live-list">
    <!-- 直播列表 -->
    <list class="list" :show-scrollbar="false">
      <!-- 行循环 -->
      <cell v-for="(row, idx) in groupedList" :key="`row-${idx}`">
        <view class="row">
          <!-- 卡片循环 -->
          <view 
            v-for="live in row" 
            :key="live.liveID"
            class="card"
            @tap="handleJoinLive(live)"
          >
            <image :src="live.coverURL || defaultCover" class="cover" />
            <view class="info">
              <text class="title">{{ live.liveName }}</text>
              <text class="owner">{{ live.liveOwner?.userName }}</text>
              <text class="count">{{ live.totalViewerCount }}人看过</text>
            </view>
          </view>
        </view>
      </cell>
    </list>
  </view>
</template>

<script setup lang="ts">
import { computed, onMounted } from 'vue';
import { useLiveListState } from "@/uni_modules/tuikit-atomic-x/state/LiveListState";

// 状态管理
const { liveList, liveListCursor, fetchLiveList } = useLiveListState();

// 计算属性：分组列表（每行2个）您可以在这里进行每行展示个数的设置。
const groupedList = computed(() => {
  const list = liveList.value || [];
  const groups = [];
  for (let i = 0; i < list.length; i += 2) {
    groups.push(list.slice(i, i + 2));
  }
  return groups;
});

// 初始化
onMounted(() => {
  fetchLiveList({ cursor: "", count: 20 });
});

// 加入直播
const handleJoinLive = (live: any) => {
  uni.redirectTo({ url: `/pages/audience/index?liveID=${live.liveID}` }); // 跳转至您的目标页面
};

</script>

<style scoped>
.live-list {
  flex: 1;
  background: #fff;
}

.list {
  width: 100%;
}

.row {
  flex-direction: row;
  padding: 0 32rpx 16rpx;
  justify-content: space-between;
}

.card {
  width: 48%;
  height: 320rpx;
  background: #f5f5f5;
  border-radius: 12rpx;
  overflow: hidden;
}

.cover {
  width: 100%;
  height: 220rpx;
}

.info {
  flex: 1;
  padding: 12rpx;
  flex-direction: column;
}

.title {
  font-size: 26rpx;
  font-weight: 600;
  color: #000;
  lines: 1;
  text-overflow: ellipsis;
  overflow: hidden;
}

.owner {
  font-size: 22rpx;
  color: #666;
  margin-top: 4rpx;
  lines: 1;
  text-overflow: ellipsis;
  overflow: hidden;
}

.count {
  font-size: 20rpx;
  color: #999;
  margin-top: 4rpx;
  lines: 1;
  text-overflow: ellipsis;
  overflow: hidden;
}
</style>
```

**LiveInfo 参数说明**
| **参数名** | **类型** | **描述** |
| --- | --- | --- |
| `liveID` | `string` | 直播间的唯一标识符 |
| `liveName` | `string` | 直播间的标题 |
| `coverURL` | `string` | 直播间的封面图片地址 |
| `liveOwner` | [LiveUserInfo](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/liveuserinfo) | 房主的个人信息 |
| `totalViewerCount` | `number` | 直播间的总观看人数 |
| `categoryList` | `[number]` | 直播间的分类标签列表 |
| `notice` | `string` | 直播间的公告信息 |
| `metaData` | `[string: string]` | 开发者自定义的元数据，用于实现复杂的业务场景 |

## 功能进阶

### 场景一：实现直播列表的分类展示

在 App 的直播广场页，顶部设有“热门”、“音乐”、“游戏”等分类标签。用户点击不同的标签后，下方的直播列表会动态筛选，只展示对应分类的直播间，从而帮助用户快速发现感兴趣的内容。

#### 实现方式

核心是利用 `LiveInfo` 模型中的 `categoryList` 属性。当主播开播设置分类后，`fetchLiveList` 返回的 `LiveInfo` 对象中就会包含这些分类信息。您的 App 在获取到完整的直播列表后，只需在客户端根据用户选择的分类，对这个列表进行一次简单的筛选，然后刷新 UI 即可。

#### 代码示例

以下示例展示了如何在直播列表页中增加根据一个`categoryList`来处理数据和筛选逻辑的 `UI`。
``` typescript
<template>
  <view class="live-list">
    <!-- 分类标签栏 -->
    <view class="category-tabs">
      <view 
        v-for="cat in categories"
        :key="cat.id"
        class="tab"
        :class="{ active: selectedCategory === cat.id }"
        @tap="selectedCategory = cat.id"
      >
        {{ cat.name }}
      </view>
    </view>

    <!-- 直播列表 -->
    <list class="list" @loadmore="loadMore" :show-scrollbar="false">
      <!-- 行循环 -->
      <cell v-for="(row, idx) in groupedList" :key="`row-${idx}`">
        <view class="row">
          <!-- 卡片循环 -->
          <view 
            v-for="live in row" 
            :key="live.liveID"
            class="card"
            @tap="handleJoinLive(live)"
          >
            <image :src="live.coverURL" class="cover" />
            
            <!-- 分类标签 -->
            <view v-if="live.liveInfo?.categoryList?.length" class="category-badge">
              <text class="badge-text">{{ getCategoryName(live.liveInfo.categoryList[0]) }}</text>
            </view>
            
            <view class="info">
              <text class="title">{{ live.liveName }}</text>
              <text class="owner">{{ live.liveOwner?.userName }}</text>
              <text class="count">{{ live.totalViewerCount }}人看过</text>
            </view>
          </view>
        </view>
      </cell>
    </list>
  </view>
</template>

<script setup lang="ts">
import { computed, onMounted, ref } from 'vue';
import { useLiveListState } from "@/uni_modules/tuikit-atomic-x/state/LiveListState";

// 状态管理
const { liveList, liveListCursor, fetchLiveList } = useLiveListState();

// 本地状态
const selectedCategory = ref(0); // 0 代表全部

// 分类列表
const categories = [
  { id: 0, name: '全部' },
  { id: 1, name: '游戏' },
  { id: 2, name: '音乐' },
  { id: 3, name: '聊天' },
  { id: 4, name: '体育' },
  { id: 5, name: '娱乐' },
];

// 分类名称映射
const categoryMap: Record<number, string> = {
  1: '游戏',
  2: '音乐',
  3: '聊天',
  4: '体育',
  5: '娱乐',
};

// 获取分类名称
const getCategoryName = (categoryId: number) => {
  return categoryMap[categoryId] || '其他';
};

// 计算属性：过滤分类后的列表
const filteredList = computed(() => {
  const list = liveList.value || [];
  
  // 如果选择"全部"，直接返回全部列表
  if (selectedCategory.value === 0) {
    return list;
  }
  
  // 根据选中的分类过滤
  return list.filter(live => {
    const categoryList = live.liveInfo?.categoryList || [];
    return categoryList.includes(selectedCategory.value);
  });
});

// 计算属性：分组列表（每行2个）
const groupedList = computed(() => {
  const list = filteredList.value;
  const groups = [];
  for (let i = 0; i < list.length; i += 2) {
    groups.push(list.slice(i, i + 2));
  }
  return groups;
});

// 初始化
onMounted(() => {
  fetchLiveList({ cursor: "", count: 20 });
});

// 加入直播
const handleJoinLive = (live: any) => {
  uni.redirectTo({ url: `/pages/audience/index?liveID=${live.liveID}` }); // 跳转至您的目标页面
};
</script>

<style scoped>
.live-list {
  flex: 1;
  background: #fff;
}

/* 分类标签栏 */
.category-tabs {
  flex-direction: row;
  padding: 16rpx 32rpx;
  background: #f9f9f9;
  border-bottom: 1rpx solid #e8e8e8;
  overflow-x: auto;
}

.tab {
  padding: 8rpx 20rpx;
  margin-right: 12rpx;
  background: #fff;
  border: 1rpx solid #e0e0e0;
  border-radius: 20rpx;
  font-size: 24rpx;
  color: #666;
  white-space: nowrap;
}

.tab.active {
  background: #0468FC;
  border-color: #0468FC;
  color: #fff;
}

.list {
  width: 100%;
}

.row {
  flex-direction: row;
  padding: 0 32rpx 16rpx;
  justify-content: space-between;
}

.card {
  width: 48%;
  height: 320rpx;
  background: #f5f5f5;
  border-radius: 12rpx;
  overflow: hidden;
  position: relative;
}

.cover {
  width: 100%;
  height: 220rpx;
}

/* 分类徽章 */
.category-badge {
  position: absolute;
  top: 8rpx;
  left: 8rpx;
  background: rgba(4, 104, 252, 0.9);
  border-radius: 4rpx;
  padding: 4rpx 8rpx;
}

.badge-text {
  font-size: 18rpx;
  color: #fff;
  font-weight: 600;
}

.info {
  flex: 1;
  padding: 12rpx;
  flex-direction: column;
}

.title {
  font-size: 26rpx;
  font-weight: 600;
  color: #000;
  lines: 1;
  text-overflow: ellipsis;
  overflow: hidden;
}

.owner {
  font-size: 22rpx;
  color: #666;
  margin-top: 4rpx;
  lines: 1;
  text-overflow: ellipsis;
  overflow: hidden;
}

.count {
  font-size: 20rpx;
  color: #999;
  margin-top: 4rpx;
  lines: 1;
  text-overflow: ellipsis;
  overflow: hidden;
}
</style>
```

### 场景二：实现语聊房内的自定义状态同步

在语聊房中，主播可能需要向所有观众同步一些自定义信息，例如“当前房间话题”、“背景音乐信息”等。`LiveListState` 的 `MetaData` 功能可以实现这一点。

#### 实现方式
1.  主播端将自定义信息（建议使用 JSON 格式）通过 `updateLiveMetaData` 接口设置到一个或多个 key 中。`AtomicXCore` 会将这个变更实时同步给所有观众。

2. 观众端只需监听`currentLive 中 metaData` 的变化，一旦发现关心的 key 更新，就解析其 value 并刷新业务状态。

#### 代码示例
``` typescript
import { useLiveListState } from "@/uni_modules/tuikit-atomic-x/state/LiveListState";

// 状态管理
const { updateLiveMetaData, currentLive } = useLiveListState();
// 1. 定义一个背景音乐模型
const musicModel = ref({ musicId: '', musicName: '', })

// 2. 主播端：在您的主播业务逻辑中，添加推送背景音乐的方法
const updateBackgroundMusic
 = () => {
    updateLiveMetaData({
      metaData: JSON.stringify(["music_info": musicModel.value]),
      success: () => {
        console.log('背景音乐 ${musicModel.value.musicName} 推送成功')
      },
      fail: (error) => {
        console.log('背景音乐推送失败', error)
      }
    })
}

// 3. 观众端：在观众端监听 currentLive
watch( currentLive, (newVal, oldVal) => {
    const newMusic = JSON.parse(newVal).metaData
    // 在此播放音乐
})
```

## API 文档

关于 [LiveListState](https://liteav.sdk.qcloud.com/doc/product/tuikit/atomic-x/uni-app/zh/v1.0/api/index.html#module-LiveListState) 及其相关类的所有公开接口、属性和方法的详细信息，请参阅随 AtomicXCore 框架的官方 API 文档。本文档使用到的相关 Store 如下：
| **State** | **功能描述** | **API 文档** |
| --- | --- | --- |
| LiveListState | 直播间全生命周期管理：创建 / 加入 / 离开 / 销毁房间，查询房间列表，修改直播信息（名称、公告等），监听直播状态（例如被踢出、结束）。 | [API 文档](https://liteav.sdk.qcloud.com/doc/product/tuikit/atomic-x/uni-app/zh/v1.0/api/index.html#module-LiveListState) |

## 常见问题

### 语聊房的列表和视频直播的列表数据是同一份吗？

它们的数据是同一份，您不需要分开拉取。`LiveListState` 是一个全局单例，它负责统一管理应用中所有“直播”房间的生命周期，无论是视频直播还是语聊房。

### **直播列表中如何区分语聊房和视频直播**

`LiveListState` 本身不区分房间的业务类型。您需要在获取列表后，在客户端的应用层（业务逻辑或 UI 层）进行筛选和分类。

我们推荐采用以下方式进行区分：

**为 **`liveID`** 添加业务前缀。**这是一种可选的、纯粹的应用层约定，用于辅助您在客户端快速筛选。
  - **步骤1：创建房间时添加前缀 **在您生成 liveID 并调用 createLive 时，为不同业务类型的 liveID 赋予不同的前缀。例如：视频直播的 ID 以 “Live_” 开头 (例如: Live_12345)，语聊房的 ID 以 “voice_” 开头 (例如: voice_67890)。

  - **步骤2：获取列表时检查前缀 **客户端在拉取到列表后，通过检查 liveID 字符串的前缀来进行区分。

### 使用 `updateLiveMetaData` 时有哪些需要注意的限制和规则？

为了保证系统的稳定和高效，`metaData` 的使用遵循以下规则：
- **权限**: 只有房主和管理员可以调用 `updateLiveMetaData`。普通观众没有权限。

- **数量与大小限制**：

  - 单个房间最多支持 **10** 个 key。

  - 每个 key 的长度不超过 **50 字节**，每个 value 的长度不超过 **2KB**。

  - 单个房间所有 value 的总大小不超过 **16KB**。

- **冲突解决**： `metaData` 的更新机制是“后来者覆盖”。如果多个管理员在短时间内修改同一个 key，最后一次的修改会生效。建议在业务设计上避免多人同时修改同一个关键信息。
