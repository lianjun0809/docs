> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

`LiveAudienceStore` 是 `AtomicXCore` 中专门负责管理直播间观众信息的模块。通过 `LiveAudienceStore`，您可以为您的直播应用构建一套完整的观众列表及管理系统。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027182498/96da98a0ab3711f09b75525400bf7822.png)


## 核心功能
- **实时观众列表**：获取并展示当前在直播间内的所有观众信息。

- **观众人数统计**：实时获取当前直播间的准确观众总数。

- **观众动态监听**：通过事件订阅，实时感知观众的加入和离开。

- **管理员权限**：主播可以将普通观众设为管理员，或撤销其管理员身份。

- **房间管理**：主播或管理员可以将任意普通观众请出（踢出）直播间。


## 核心概念

在开始集成之前，我们先通过下表了解一下 LiveAudienceStore 相关的几个核心概念：
<table>
<tr>
<td rowspan="1" colSpan="1" >**核心概念**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**核心职责与描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`LiveUserInfo`</td>

<td rowspan="1" colSpan="1" >struct</td>

<td rowspan="1" colSpan="1" >代表一个观众（用户）的基础信息模型。它包含了用户的唯一标识 (`userID`)、昵称 (`userName`) 和头像地址 (`avatarURL`)。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`LiveAudienceState`</td>

<td rowspan="1" colSpan="1" >struct</td>

<td rowspan="1" colSpan="1" >代表观众模块的当前状态。其核心属性 `audienceList` 是一个 `[LiveUserInfo] `数组，存储了观众列表的快照；`audienceCount` 则代表当前观众总数。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`LiveAudienceEvent`</td>

<td rowspan="1" colSpan="1" >enum</td>

<td rowspan="1" colSpan="1" >代表观众动态的实时事件。分为 `.onAudienceJoined`（观众加入） 和 `.onAudienceLeft`（观众离开）两种，用于实现对观众列表的增量更新。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`LiveAudienceStore`</td>

<td rowspan="1" colSpan="1" >class</td>

<td rowspan="1" colSpan="1" >这是与观众列表功能交互的核心管理类。通过它，您可以获取观众列表快照、执行管理操作，并通过订阅其 `liveAudienceEventPublisher` 来接收实时动态。</td>
</tr>
</table>


## 实现步骤

### 步骤1：组件集成

请参考 [开始直播](https://write.woa.com/document/191126382767431680) 集成 **AtomicXCore**，完成接入。

### 步骤2：初始化并获取观众列表

获取一个与当前直播间 liveId 绑定的 `LiveAudienceStore` 实例，并主动拉取一次当前的观众列表，用于首次展示。
``` swift
import Foundation
import AtomicXCore 
import Combine     

class AudienceManager {
    private let liveId: String
    private let audienceStore: LiveAudienceStore
    private var cancellables = Set<AnyCancellable>()
    
    // 对外暴露【全量】观众列表的发布者，方便UI层订阅
    let audienceListPublisher = CurrentValueSubject<[LiveUserInfo], Never>([])
    // 对外暴露观众总数的发布者
    let audienceCountPublisher = PassthroughSubject<UInt, Never>()

    init(liveId: String) {
        self.liveId = liveId
        // 1. 通过 liveId 获取 LiveAudienceStore 的实例
        self.audienceStore = LiveAudienceStore.create(liveID: liveId)
        
        // 2. 订阅状态和事件
        subscribeToAudienceState()
        subscribeToAudienceEvents()
        
        // 3. 主动拉取首屏数据
        fetchInitialAudienceList()
    }

    /// 主动获取一次观众列表快照
    func fetchInitialAudienceList() {
        audienceStore.fetchAudienceList { [weak self] result in
            switch result {
            case .success:
                print("首次拉取观众列表成功")
                // 成功后，数据会通过下面的 state 订阅通道自动更新
            case .failure(let error):
                print("首次拉取观众列表失败: \(error.localizedDescription)")
            }
        }
    }
    
    // ... 后续代码
}
```

### 步骤3：监听观众列表状态与实时动态

订阅 `audienceStore` 的 `state` 和 `event`，以接收全量列表快照和实时的观众进出事件，从而驱动 UI 更新。
``` swift
extension AudienceManager {
    /// 订阅 state，用于获取观众总数和列表快照
    private func subscribeToAudienceState() {
        audienceStore.state
            .subscribe()
            .receive(on: DispatchQueue.main)
            .sink { [weak self] state in
                // state.audienceList 是一个全量快照
                self?.audienceListPublisher.send(state.audienceList)
                // state.audienceCount 是实时总数
                self?.audienceCountPublisher.send(state.audienceCount)
            }
            .store(in: &cancellables)
    }

    /// 订阅 event，用于处理观众的实时进出
    private func subscribeToAudienceEvents() {
        audienceStore.liveAudienceEventPublisher
            .receive(on: DispatchQueue.main)
            .sink { [weak self] event in
                guard let self = self else { return }
                
                var currentList = self.audienceListPublisher.value
                
                switch event {
                case .onAudienceJoined(let newAudience):
                    print("观众 \(newAudience.userName) 加入了直播间")
                    // 增量更新：在当前列表末尾添加新观众
                    if !currentList.contains(where: { $0.userID == newAudience.userID }) {
                        currentList.append(newAudience)
                        self.audienceListPublisher.send(currentList)
                    }
                    
                case .onAudienceLeft(let departedAudience):
                    print("观众 \(departedAudience.userName) 离开了直播间")
                    // 增量更新：从当前列表中移除离开的观众
                    currentList.removeAll { $0.userID == departedAudience.userID }
                    self.audienceListPublisher.send(currentList)
                }
            }
            .store(in: &cancellables)
    }
}
```

### 步骤4：管理观众（踢人与设置管理员）

作为主播或管理员，对直播间内的观众进行管理操作。

#### 4.1 将观众踢出直播间

调用 `kickUserOutOfRoom` 接口可以将指定用户请出直播间。
``` swift
extension AudienceManager {
    func kick(userId: String) {
        audienceStore.kickUserOutOfRoom(userID: userId) { result in
            switch result {
            case .success:
                print("成功将用户 \(userId) 踢出房间")
                // 踢出成功后，您会收到 onAudienceLeft 事件
            case .failure(let error):
                print("踢出用户 \(userId) 失败: \(error.localizedDescription)")
            }
        }
    }
}
```

#### 4.2 设置/撤销管理员

通过 `setAdministrator` 和 `revokeAdministrator` 接口可以管理用户的管理员身份。
``` swift
extension AudienceManager {
    /// 将用户设为管理员
    func promoteToAdmin(userId: String) {
        audienceStore.setAdministrator(userID: userId) { result in
            if case .success = result {
                print("成功将用户 \(userId) 设为管理员")
            }
        }
    }

    /// 撤销用户的管理员身份
    func revokeAdmin(userId: String) {
        audienceStore.revokeAdministrator(userID: userId) { result in
            if case .success = result {
                print("成功撤销用户 \(userId) 的管理员身份")
            }
        }
    }
}
```

## 功能进阶

### 在弹幕区展示观众入场欢迎语

当有新观众进入直播间时，弹幕/聊天区域会在本地自动显示一条欢迎消息，例如：“欢迎 [用户昵称] 进入直播间”。

#### 实现方式

我们通过订阅 `LiveAudienceStore` 的观众加入事件（`LiveAudienceEvent.onAudienceJoined`）来获取新观众加入的实时通知。一旦事件触发，我们便提取出新观众的昵称信息，然后立即调用 `BarrageStore` 的本地插入接口 `appendLocalTip`。
``` swift
import Foundation
import AtomicXCore 
import Combine

class LiveRoomManager {
    private let liveId: String
    private let audienceManager: AudienceManager
    private let barrageManager: BarrageManager // 假设您已实现了弹幕文档中的BarrageManager
    private var cancellables = Set<AnyCancellable>()

    init(liveId: String) {
        self.liveId = liveId
        // 初始化两个核心管理器
        self.audienceManager = AudienceManager(liveId: liveId)
        self.barrageManager = BarrageManager(liveId: liveId)

        // 设置联动
        setupWelcomeMessageFlow()
    }

    private func setupWelcomeMessageFlow() {
        // 1. 获取 LiveAudienceStore 的实例
        let audienceStore = LiveAudienceStore.create(liveID: self.liveId)

        // 2. 获取 BarrageStore 的实例 (得益于内部机制，这会是同一个实例)
        let barrageStore = BarrageStore.create(liveID: self.liveId)

        // 3. 订阅观众事件
        audienceStore.liveAudienceEventPublisher
            .receive(on: DispatchQueue.main)
            .sink { event in
                // 4. 只处理观众加入事件
                guard case .onAudienceJoined(let newAudience) = event else {
                    return
                }

                // 5. 创建一条本地提示消息
                var welcomeTip = Barrage()
                welcomeTip.messageType = .text 
                welcomeTip.textContent = "欢迎 \(newAudience.userName) 进入直播间！"

                // 6. 调用 BarrageStore 的接口将其插入弹幕列表
                barrageStore.appendLocalTip(message: welcomeTip)
            }
            .store(in: &cancellables)
    }
}
```

## API 文档

关于 [LiveAudienceStore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/liveaudiencestore) 及其相关类的所有公开接口、属性和方法的详细信息，请参阅随 [AtomicXCore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore) 框架的官方 API 文档。本文档使用到的相关 Store 如下：
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
<td rowspan="1" colSpan="1" >LiveAudienceStore</td>

<td rowspan="1" colSpan="1" >观众管理：获取实时观众列表（ID / 名称 / 头像），统计观众数量，监听观众进出事件。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/liveaudiencestore)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >BarrageStore</td>

<td rowspan="1" colSpan="1" >弹幕功能：发送文本 / 自定义弹幕，维护弹幕列表，实时监听弹幕状态。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/barragestore)</td>
</tr>
</table>


## 常见问题

### `LiveAudienceState` 中的在线人数（`audienceCount`）是如何更新的？时机和频率是怎样的？

`audienceCount` 的更新并非总是实时的，其机制如下：
- **主动进出房间**：当用户主动加入或正常退出直播间时，在线人数的变更通知会即时触发。您会很快在 `LiveAudienceState` 中观察到 `audienceCount` 的变化。

- **异常掉线**：当用户因网络问题、应用崩溃等原因异常掉线时，系统需要通过心跳机制来判断其真实状态。只有当该用户连续 90 秒没有心跳后，系统才会判定其为离线，并触发人数变更通知。

- **更新机制与频率控制：**

  - 无论是即时触发还是延迟触发，所有的人数变更通知都是以消息的形式在房间内广播的。

  - 房间内每秒的消息总量有上限，单房间消息频控是**每秒 40 条消息**。

  - **关键点：**在“弹幕风暴”或礼物刷屏等消息流量极高的场景下，如果房间内的消息速率超过了 40条/秒 的阈值，为了保证核心消息（例如弹幕）的送达，**人数变更的消息可能会被频控策略丢弃**。


      **这对开发者意味着什么？**


      `audienceCount` 是一个非常接近实时的**高精度估算值**，但在极端高并发场景下，它可能存在短暂的延迟或数据丢失。因此，我们建议您将其用于 **UI 展示**，而不应作为计费、统计等需要绝对精准场景的唯一依据。


