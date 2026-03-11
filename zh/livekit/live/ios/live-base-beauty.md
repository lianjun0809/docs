> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

`BaseBeautyStore` 是 `AtomicXCore` 中负责管理人像基础美颜效果的模块。通过它，您可以轻松为您的直播或通话应用添加自然的美颜效果。

## 核心功能
- **磨皮效果调节**：设置磨皮强度 (0-9)。

- **美白效果调节**：设置美白强度 (0-9)。

- **红润效果调节**：设置红润强度 (0-9)。

- **效果重置**：一键恢复所有美颜参数至默认值。

- **状态监听**：实时获取当前生效的美颜参数。


## 核心概念

在开始集成之前，我们先通过下表了解一下 BaseBeautyStore 相关的核心概念：
<table>
<tr>
<td rowspan="1" colSpan="1" >**核心概念**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**核心职责与描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`BaseBeautyState`</td>

<td rowspan="1" colSpan="1" >`struct`</td>

<td rowspan="1" colSpan="1" >代表基础美颜模块的当前状态。包含了当前生效的磨皮 (`smoothLevel`)、美白 (`whitenessLevel`) 和红润 (`ruddyLevel`) 的强度值。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`BaseBeautyStore`</td>

<td rowspan="1" colSpan="1" >`class`</td>

<td rowspan="1" colSpan="1" >这是与基础美颜功能交互的核心管理类。它是一个全局单例 (`shared`)，负责所有基础美颜参数的设置、重置和状态同步。</td>
</tr>
</table>


## 实现步骤

### 步骤1：组件集成

请参考 [开始直播](https://write.woa.com/document/191126382767431680) 集成 **AtomicXCore**，并完成 **LiveCoreView** 的接入。

### 步骤2：获取实例并监听状态

获取 `BaseBeautyStore` 的全局单例，并设置订阅者以实时获取当前的美颜参数状态。

#### 实现方式
1. **获取单例**：直接使用 `BaseBeautyStore.shared` 获取全局唯一的 `BaseBeautyStore` 实例。

2. **订阅状态**：订阅 `baseBeautyStore.state` 以实时获取 `BaseBeautyState` 的更新。


#### 代码示例
``` swift
import Foundation
import AtomicXCore 
import Combine     

class BeautyManager {
    // 1. 获取单例
    private let baseBeautyStore = BaseBeautyStore.shared //
    private var cancellables = Set<AnyCancellable>()
    
    // 对外暴露美颜状态
    let beautyStatePublisher = CurrentValueSubject<BaseBeautyState, Never>(BaseBeautyState())

    init() {
        // 2. 订阅状态
        subscribeToBeautyState()
    }
    
    private func subscribeToBeautyState() {
        baseBeautyStore.state //
            .subscribe()
            .receive(on: DispatchQueue.main)
            .assign(to: \.value, on: beautyStatePublisher)
            .store(in: &cancellables)
    }
    
    // ... 后续方法
}
```

### 步骤3：设置美颜参数

当用户拖动美颜滑块或点击预设按钮时，调用相应的接口设置美颜强度。

#### 实现方式
1. **获取强度值**：从 UI 控件（如 `UISlider`）获取用户设定的强度值。请注意，SDK 接口接收的参数范围是 `[0, 9]`，其中 `0` 表示关闭效果，`9` 表示效果最明显。您需要将 UI 控件的值（例如 UISlider 的 `0.0 - 1.0`）映射到 `0 - 9` 的范围。

2. **调用接口**：分别调用 `setSmoothLevel(smoothLevel:)`、`setWhitenessLevel(whitenessLevel:)`、`setRuddyLevel(ruddyLevel:) `来设置磨皮、美白、红润的强度。


#### 代码示例
``` swift
extension BeautyManager {
    /// 设置磨皮等级 (输入范围 0.0 ~ 1.0, 内部转换为 0 ~ 9)
    func updateSmoothLevel(uiLevel: Float) {
        // 将 UI 的 0.0 ~ 1.0 映射到 SDK 的 0 ~ 9
        let sdkLevel = uiLevel * 9.0
        baseBeautyStore.setSmoothLevel(smoothLevel: sdkLevel) //
    }

    /// 设置美白等级 (输入范围 0.0 ~ 1.0, 内部转换为 0 ~ 9)
    func updateWhitenessLevel(uiLevel: Float) {
        let sdkLevel = uiLevel * 9.0
        baseBeautyStore.setWhitenessLevel(whitenessLevel: sdkLevel) //
    }

    /// 设置红润等级 (输入范围 0.0 ~ 1.0, 内部转换为 0 ~ 9)
    func updateRuddyLevel(uiLevel: Float) {
        let sdkLevel = uiLevel * 9.0
        baseBeautyStore.setRuddyLevel(ruddyLevel: sdkLevel) //
    }
}
```

### 步骤4：重置美颜效果

当用户点击“重置”或“关闭美颜”按钮时，将所有美颜参数恢复到默认值（通常是0）。

#### 实现方式

**调用接口**：直接调用 baseBeautyStore.reset() 方法。

#### 代码示例
``` swift
extension BeautyManager {
    /// 重置所有基础美颜效果
    func resetBeautyEffects() {
        baseBeautyStore.reset() //
    }
}
```

## 功能进阶

### 基础美颜与高级美颜对比

AtomicXCore 也提供了高级美颜支持，以满足不同场景的需求
<table>
<tr>
<td rowspan="1" colSpan="1" >**对比项**</td>

<td rowspan="1" colSpan="1" >**基础美颜 (BaseBeautyStore)**</td>

<td rowspan="1" colSpan="1" >**高级美颜 (TEBeautyKit 需额外集成)**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >核心功能</td>

<td rowspan="1" colSpan="1" >磨皮、美白、红润</td>

<td rowspan="1" colSpan="1" >包含基础美颜，并增加 V 脸、眼距、瘦鼻、3D 贴纸、滤镜、美妆等丰富效果</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >计费</td>

<td rowspan="1" colSpan="1" >免费 (包含在 AtomicXCore 授权内)</td>

<td rowspan="1" colSpan="1" >付费（需要额外购买腾讯特效 SDK License） </td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >集成方式</td>

<td rowspan="1" colSpan="1" >默认内置，直接使用 `BaseBeautyStore.shared`</td>

<td rowspan="1" colSpan="1" >需要额外集成 `TEBeautyKit` 组件并进行鉴权</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >推荐场景</td>

<td rowspan="1" colSpan="1" >对美颜要求不高，需要快速实现基础美颜功能的场景</td>

<td rowspan="1" colSpan="1" >对美颜效果有较高要求，需要丰富的美型、贴纸、滤镜等高级功能的场景</td>
</tr>
</table>


### 集成高级美颜

如果您需要使用高级美颜功能，请参考 [高级美颜](https://cloud.tencent.com/document/product/616/103697) 文档进行集成。集成并成功鉴权 `TEBeautyKit` 后，您可以通过 `TEBeautyKit` 提供的接口来控制所有美颜效果。

## API 文档

关于 [BaseBeautyStore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/basebeautystore) 及其相关类的所有公开接口、属性和方法的详细信息，请参阅随 [AtomicXCore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore) 框架的官方 API 文档。本指南使用到的相关 Store 如下：
<table>
<tr>
<td rowspan="1" colSpan="1" >Store/Component</td>

<td rowspan="1" colSpan="1" >功能描述</td>

<td rowspan="1" colSpan="1" >API 文档</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >BaseBeautyStore</td>

<td rowspan="1" colSpan="1" >基础美颜：调节磨皮 / 美白 / 红润（0-9 级），重置美颜状态，同步效果参数。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/basebeautystore)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >DeviceStore</td>

<td rowspan="1" colSpan="1" >音视频设备控制：麦克风（开关 / 音量）、摄像头（开关 / 切换 / 画质）、屏幕共享，设备状态实时监听。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/devicestore)</td>
</tr>
</table>


## 常见问题

### 我设置了美颜参数，为什么没有效果？

请检查以下几点：
1. **摄像头是否开启**：必须先成功打开摄像头（例如通过 `DeviceStore.shared.openLocalCamera`），美颜效果才能应用到视频流上。

2. **是否使用了高级美颜**：如果您集成了 `TEBeautyKit` (高级美颜)，请确保您使用的是 `TEBeautyKit` 提供的接口来调节美颜。

3. **参数范围**：如果您使用的基础美颜，请确认您传入的强度值在有效的范围内 (`0` 到 `9` 之间的 Float 值)。


