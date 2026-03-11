> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

`LiveListStore` 是 `AtomicXCore` 中负责管理直播房间列表、创建、加入以及维护房间状态的核心模块。通过`LiveListStore`，您可以为您的应用构建完整的直播生命周期管理。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027182498/6fd3c4f2ab6011f0b5345254005ef0f7.png)


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

<td rowspan="1" colSpan="1" >`struct`</td>

<td rowspan="1" colSpan="1" >代表一个直播间的所有信息模型。包含了直播ID (`liveID`)、名称 (`liveName`)、房主信息 (`liveOwner`) 以及自定义元数据 (`metaData`) 等。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`LiveListState`</td>

<td rowspan="1" colSpan="1" >`struct`</td>

<td rowspan="1" colSpan="1" >代表直播列表模块的当前状态。其核心属性 liveList 是一个 `[LiveInfo] `数组，存储了拉取到的直播列表；`currentLive` 则代表用户当前所在的直播间信息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`LiveListEvent`</td>

<td rowspan="1" colSpan="1" >`enum`</td>

<td rowspan="1" colSpan="1" >代表直播房间的全局事件。分为 `.onLiveEnded` (直播结束) 和 `.onKickedOutOfLive` (被踢出直播) 两种，用于处理关键的房间状态变更。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`LiveListStore`</td>

<td rowspan="1" colSpan="1" >`class`</td>

<td rowspan="1" colSpan="1" >这是与直播列表和房间生命周期交互的核心管理类。它是一个全局单例 (shared)，负责所有直播房间的创建、加入、信息更新等操作。</td>
</tr>
</table>


## 实现步骤

### 步骤1：组件集成

请参考 [开始直播](https://write.woa.com/document/191126382767431680) 集成 **AtomicXCore**，并完成 [主播开播](https://write.woa.com/document/191126382767431680) 和 [观众观看](https://write.woa.com/document/191126382767431680) 的功能实现。

### 步骤2：实现观众从直播列表进入直播间

创建一个展示直播列表的页面，该页面使用 `UICollectionView` 来布局直播间卡片。当用户点击某个卡片时，获取该直播间的 `liveId`，并跳转到观众观看页面。
``` swift
import AtomicXCore
import SnapKit
import RTCRoomEngine
import Combine

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
        
        // 创建观众观看页面，并将 liveId 传入
        let audienceVC = YourAudienceViewController(liveId: selectedLiveInfo.liveID)
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

<td rowspan="1" colSpan="1" >[LiveUserInfo](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/liveuserinfo)</td>

<td rowspan="1" colSpan="1" >房主的个人信息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`totalViewerCount`</td>

<td rowspan="1" colSpan="1" >`Int`</td>

<td rowspan="1" colSpan="1" >直播间的总观看人数</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`categoryList`</td>

<td rowspan="1" colSpan="1" >`[NSNumber]`</td>

<td rowspan="1" colSpan="1" >直播间的分类标签列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`notice`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >直播间的公告信息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`metaData`</td>

<td rowspan="1" colSpan="1" >`[String: String]`</td>

<td rowspan="1" colSpan="1" >开发者自定义的元数据，用于实现复杂的业务场景</td>
</tr>
</table>


## 功能进阶

### 场景一：实现直播列表的分类展示

在 App 的直播广场页，顶部设有“热门”、“音乐”、“游戏”等分类标签。用户点击不同的标签后，下方的直播列表会动态筛选，只展示对应分类的直播间，从而帮助用户快速发现感兴趣的内容。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027182498/7dcde616ab4b11f0a68e5254001c06ec.png)


#### 实现方式

核心是利用 `LiveInfo` 模型中的 `categoryList` 属性。当主播开播设置分类后，`fetchLiveList` 返回的 `LiveInfo` 对象中就会包含这些分类信息。您的 App 在获取到完整的直播列表后，只需在客户端根据用户选择的分类，对这个列表进行一次简单的筛选，然后刷新 UI 即可。

#### 代码示例

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

// 2. 在您的 LiveListViewController 中使用 Manager
class LiveListViewController: UIViewController, UICollectionViewDataSource, UICollectionViewDelegate {

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

### 场景二：实现直播列表的滑动播放

用户可以通过上下滑动来切换直播间，当一个新的直播间滑动到屏幕中央时，视频会自动开始播放预览；当它滑出屏幕时，视频则会自动停止，以节省带宽和设备性能。

#### 交互流程图

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027182498/904c1b1dab5c11f08bcc5254007c27c5.webp)


#### 实现方式

`LiveCoreView` 支持多实例使用，我们为每一个 `UICollectionViewCell` 都创建一个独立的 `LiveCoreView` 实例。通过监听 `UICollectionView` 的滚动代理方法，我们可以精确地控制即将出现和已经离开屏幕的 Cell 中的 `LiveCoreView` 何时开始和停止拉流，从而实现“即滑即播、即走即停”的效果。

#### 代码示例

我们创建一个自定义的 `LiveFeedCell`，它内部持有一个 `LiveCoreView`。然后在 UIViewController 中管理这些 Cell 的播放状态。
``` swift
import UIKit
import AtomicXCore

// 1. 自定义 UICollectionViewCell，内部包含一个 LiveCoreView
class LiveFeedCell: UICollectionViewCell {
    private var liveCoreView: LiveCoreView?

    func setLiveInfo(_ liveInfo: LiveInfo) {
        // 为新的直播信息创建一个新的 LiveCoreView
        liveCoreView = LiveCoreView(viewType: .playView)
        guard let liveCoreView = liveCoreView else { return }
        contentView.addSubview(liveCoreView)
        liveCoreView.frame = contentView.bounds
    }

    func startPlay(roomId: String) {
        liveCoreView?.startPreviewLiveStream(roomId: roomId, isMuteAudio: false)
    }

    func stopPlay(roomId: String) {
        liveCoreView?.stopPreviewLiveStream(roomId: roomId)
    }
}

// 2. 在 ViewController 中管理播放逻辑
class LiveFeedViewController: UIViewController, UICollectionViewDataSource, UICollectionViewDelegate {

    private var collectionView: UICollectionView!
    private var liveList: [LiveInfo] = []
    private var currentPlayingIndexPath: IndexPath?

    // 当滑动完全停止后，此代理方法会被调用
    func scrollViewDidEndDecelerating(_ scrollView: UIScrollView) {
        let page = Int(scrollView.contentOffset.y / view.frame.height)
        let indexPath = IndexPath(item: page, section: 0)

        // 只有当居中的 Cell 变化时才切换播放
        if currentPlayingIndexPath != indexPath {
            playVideo(at: indexPath)
        }
    }

    // 当 Cell 即将离开屏幕时调用
    func collectionView(_ collectionView: UICollectionView, didEndDisplaying cell: UICollectionViewCell, forItemAt indexPath: IndexPath) {
        if let liveCell = cell as? LiveFeedCell {
            let liveInfo = liveList[indexPath.item]
            liveCell.stopPlay(roomId: liveInfo.liveID)
        }
    }

    private func playVideo(at indexPath: IndexPath) {
        if let cell = collectionView.cellForItem(at: indexPath) as? LiveFeedCell {
            let liveInfo = liveList[indexPath.item]
            cell.startPlay(roomId: liveInfo.liveID)
            currentPlayingIndexPath = indexPath
        }
    }

    // ... (UICollectionViewDataSource 的其他方法)
    func collectionView(_ collectionView: UICollectionView, cellForItemAt indexPath: IndexPath) -> UICollectionViewCell {
        let cell = collectionView.dequeueReusableCell(withReuseIdentifier: "LiveFeedCell", for: indexPath) as! LiveFeedCell
        cell.setLiveInfo(liveList[indexPath.item])
        return cell
    }
}
```

### 场景三：实现电商直播的商品信息展示

在电商直播中，主播正在讲解一款商品。此时，所有观众的直播画面下方都会弹出一张商品卡片，实时展示该商品的图片、名称和价格。当主播切换讲解下一件商品时，所有观众端的卡片都会自动、同步更新。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027182498/2ba67778ac9611f0a0a052540099c741.png)


#### 实现方式

主播端将当前商品的结构化信息（建议使用 **JSON **格式）通过 `updateLiveMetaData` 接口设置到一个自定义的 key（例如 "`product_info`"）中。**AtomicXCore** 会将这个变更实时同步给所有观众。观众端只需订阅 `LiveListStore.state`，监听 `metaData` 的变化，一旦发现 `product_info` 的值更新，就解析其中的 JSON 数据并刷新商品卡片 UI。

#### 代码示例
``` swift
import AtomicXCore
import Combine

// 1. 定义一个商品信息模型，遵循 Codable 以便与JSON互转
struct Product: Codable {
    let id: String
    let name: String
    let price: String
    let imageUrl: String
}

// 2. 主播端：在 YourAnchorViewController 中添加推送商品的方法
extension YourAnchorViewController {
    func pushProductInfo(_ product: Product) {
        guard let jsonData = try? JSONEncoder().encode(product),
              let jsonString = String(data: jsonData, encoding: .utf8) else { return }

        let metaData = ["product_info": jsonString]

        // 使用全局单例的 liveListStore 来更新 metaData
        LiveListStore.shared.updateLiveMetaData(metaData) { result in
            if case .success = result {
                print("商品 \(product.name) 信息推送成功")
            }
        }
    }
}

// 3. 观众端：在 YourAudienceViewController 中订阅并响应
class YourAudienceViewController: UIViewController {

    // ... (已有代码)
    private var cancellables = Set<AnyCancellable>()
    // 假设您有一个自定义的商品卡片视图
    // private let productCardView = ProductCardView()

    override func viewDidLoad() {
        super.viewDidLoad()
        view.backgroundColor = .black
        // ... (setupUI, 布局 productCardView)
        joinLive()
        subscribeToProductUpdates()
    }

    private func subscribeToProductUpdates() {
        LiveListStore.shared.state
            // 监听当前房间的 metaDatass
            .subscribe(StatePublisherSelector(keyPath: \LiveListState.currentLive.metaData))
            .removeDuplicates()
            .receive(on: DispatchQueue.main)
            .sink { metaData in
                guard let jsonString = metaData["product_info"],
                      let data = jsonString.data(using: .utf8),
                      let product = try? JSONDecoder().decode(Product.self, from: data) else {
                    // self.productCardView.hide() // 如果没有商品信息，则隐藏卡片
                    return
                }
                // self.productCardView.update(with: product) // 使用新数据更新商品卡片UI
                // self.productCardView.show()
            }
            .store(in: &cancellables)
    }

    // ... (joinLive 和 leaveLive 方法)
}
```

## API 文档

关于 [LiveListStore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/liveliststore) 及其相关类的所有公开接口、属性和方法的详细信息，请参阅随 [AtomicXCore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore) 框架的官方 API 文档。本文档使用到的相关 Store 如下：
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
<td rowspan="1" colSpan="1" >LiveListStore</td>

<td rowspan="1" colSpan="1" >直播间全生命周期管理：创建 / 加入 / 离开 / 销毁房间，查询房间列表，修改直播信息（名称、公告等），监听直播状态（例如被踢出、结束）。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/liveliststore)</td>
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

- **冲突解决**： `metaData` 的更新机制是“后来者覆盖”。如果多个管理员在短时间内修改同一个 key，最后一次的修改会生效。建议在业务设计上避免多人同时修改同一个关键信息。
