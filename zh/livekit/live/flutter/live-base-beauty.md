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

在开始集成之前，我们先通过下表了解一下 `BaseBeautyStore` 相关的核心概念：
<table>
<tr>
<td rowspan="1" colSpan="1" >**核心概念**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**核心职责与描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[BaseBeautyState](https://tencent-rtc.github.io/TUIKit_Flutter/api_device_base_beauty_store/BaseBeautyState-class.html)</td>

<td rowspan="1" colSpan="1" >`class`</td>

<td rowspan="1" colSpan="1" >代表基础美颜模块的当前状态。包含了当前生效的磨皮 (`smoothLevel`)、美白 (`whitenessLevel`) 和红润 (`ruddyLevel`) 的强度值。所有属性均为 `ValueListenable<double>` 类型，支持订阅监听。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[BaseBeautyStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_device_base_beauty_store/BaseBeautyStore-class.html)</td>

<td rowspan="1" colSpan="1" >`class`</td>

<td rowspan="1" colSpan="1" >这是与基础美颜功能交互的核心管理类。它是一个全局单例 (`shared`)，负责所有基础美颜参数的设置、重置和状态同步。</td>
</tr>
</table>


## 实现步骤

### 步骤1：组件集成

请参考 [开始直播](https://write.woa.com/document/191126413785100288) 集成 **AtomicXCore**，完成接入。

### 步骤2：获取实例并监听状态

获取 `BaseBeautyStore` 的全局单例，并设置监听器以实时获取当前的美颜参数状态。

#### 实现方式
1. **获取单例**：直接使用 `BaseBeautyStore.shared` 获取全局唯一的 `BaseBeautyStore` 实例。

2. **订阅状态**：通过 `addListener` 监听 `baseBeautyState` 中各属性的变化，实时获取美颜参数更新。


#### 代码示例
``` java
import 'package:flutter/material.dart';
import 'package:atomic_x_core/atomicxcore.dart';

class BeautyManager {
  // 1. 获取单例
  final _baseBeautyStore = BaseBeautyStore.shared;
  late final VoidCallback _smoothLevelChangedListener = _onSmoothLevelChanged;
  late final VoidCallback _whitenessLevelChangedListener = _onWhitenessLevelChanged;
  late final VoidCallback _ruddyLevelChangedListener = _onRuddyLevelChanged;

  // 2. 订阅状态
  void subscribeToBeautyState() {
    _baseBeautyStore.baseBeautyState.smoothLevel.addListener(_smoothLevelChangedListener);
    _baseBeautyStore.baseBeautyState.whitenessLevel.addListener(_whitenessLevelChangedListener);
    _baseBeautyStore.baseBeautyState.ruddyLevel.addListener(_ruddyLevelChangedListener);
  }

  void _onSmoothLevelChanged() {
    final level = _baseBeautyStore.baseBeautyState.smoothLevel.value;
    debugPrint('磨皮强度变化: $level');
  }

  void _onWhitenessLevelChanged() {
    final level = _baseBeautyStore.baseBeautyState.whitenessLevel.value;
    debugPrint('美白强度变化: $level');
  }

  void _onRuddyLevelChanged() {
    final level = _baseBeautyStore.baseBeautyState.ruddyLevel.value;
    debugPrint('红润强度变化: $level');
  }

  // 退出 App 应用前执行 dispose 操作
  void dispose() {
    _baseBeautyStore.baseBeautyState.smoothLevel.removeListener(_smoothLevelChangedListener);
    _baseBeautyStore.baseBeautyState.whitenessLevel.removeListener(_whitenessLevelChangedListener);
    _baseBeautyStore.baseBeautyState.ruddyLevel.removeListener(_ruddyLevelChangedListener);
  }
}
```

### 步骤3：设置美颜参数

当用户拖动美颜滑块或点击预设按钮时，调用相应的接口设置美颜强度。

#### 实现方式
1. **获取强度值**：从 UI 控件（如 `Slider`）获取用户设定的强度值。SDK 接口接收的参数范围是 `0-9`，其中 `0` 表示关闭效果，`9` 表示效果最明显。您需要将 UI 控件的值（例如 Slider 的 `0.0 - 1.0`）映射到 `0 - 9` 的范围。

2. **调用接口**：分别调用 `setSmoothLevel()`、`setWhitenessLevel()`、`setRuddyLevel()` 来设置磨皮、美白、红润的强度。


#### 代码示例
``` java
extension BeautyManagerExtension on BeautyManager {
  /// 设置磨皮强度 (输入范围 0.0 ~ 1.0, 内部转换为 0 ~ 9)
  void updateSmoothLevel(double uiLevel) {
    // 将 UI 的 0.0 ~ 1.0 映射到 SDK 的 0 ~ 9
    final sdkLevel = uiLevel * 9.0;
    _baseBeautyStore.setSmoothLevel(sdkLevel);
  }

  /// 设置美白强度 (输入范围 0.0 ~ 1.0, 内部转换为 0 ~ 9)
  void updateWhitenessLevel(double uiLevel) {
    final sdkLevel = uiLevel * 9.0;
    _baseBeautyStore.setWhitenessLevel(sdkLevel);
  }

  /// 设置红润强度 (输入范围 0.0 ~ 1.0, 内部转换为 0 ~ 9)
  void updateRuddyLevel(double uiLevel) {
    final sdkLevel = uiLevel * 9.0;
    _baseBeautyStore.setRuddyLevel(sdkLevel);
  }
}
```

### 步骤4：重置美颜效果

当用户点击"重置"或"关闭美颜"按钮时，将所有美颜参数恢复到默认值（通常是0）。

#### 实现方式

**调用接口**：直接调用 `baseBeautyStore.reset()` 方法。

#### 代码示例
``` java
extension BeautyManagerReset on BeautyManager {
  /// 重置所有基础美颜效果
  void resetBeautyEffects() {
    _baseBeautyStore.reset();
  }
}
```

## 构建美颜 UI 界面

Flutter 推荐使用 `ValueListenableBuilder` 来构建响应式 UI，当美颜参数变化时自动更新界面：
``` java
class BeautySliderWidget extends StatelessWidget {
  final beautyStore = BaseBeautyStore.shared;

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        // 磨皮滑块
        ValueListenableBuilder<double>(
          valueListenable: beautyStore.baseBeautyState.smoothLevel,
          builder: (context, smoothLevel, child) {
            return Row(
              children: [
                Text('磨皮'),
                Expanded(
                  child: Slider(
                    value: smoothLevel,
                    min: 0,
                    max: 9,
                    divisions: 9,
                    onChanged: (value) {
                      beautyStore.setSmoothLevel(value);
                    },
                  ),
                ),
                Text('${smoothLevel.toInt()}'),
              ],
            );
          },
        ),
        // 美白滑块
        ValueListenableBuilder<double>(
          valueListenable: beautyStore.baseBeautyState.whitenessLevel,
          builder: (context, whitenessLevel, child) {
            return Row(
              children: [
                Text('美白'),
                Expanded(
                  child: Slider(
                    value: whitenessLevel,
                    min: 0,
                    max: 9,
                    divisions: 9,
                    onChanged: (value) {
                      beautyStore.setWhitenessLevel(value);
                    },
                  ),
                ),
                Text('${whitenessLevel.toInt()}'),
              ],
            );
          },
        ),
        // 红润滑块
        ValueListenableBuilder<double>(
          valueListenable: beautyStore.baseBeautyState.ruddyLevel,
          builder: (context, ruddyLevel, child) {
            return Row(
              children: [
                Text('红润'),
                Expanded(
                  child: Slider(
                    value: ruddyLevel,
                    min: 0,
                    max: 9,
                    divisions: 9,
                    onChanged: (value) {
                      beautyStore.setRuddyLevel(value);
                    },
                  ),
                ),
                Text('${ruddyLevel.toInt()}'),
              ],
            );
          },
        ),
      ],
    );
  }
}
```

## 完整示例
``` java
import 'package:flutter/material.dart';
import 'package:atomic_x_core/atomicxcore.dart';

class BeautySettingsPage extends StatelessWidget {
  final beautyStore = BaseBeautyStore.shared;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('美颜设置')),
      body: Padding(
        padding: EdgeInsets.all(16),
        child: Column(
          children: [
            // 磨皮
            _buildBeautySlider(
              title: '磨皮',
              valueListenable: beautyStore.baseBeautyState.smoothLevel,
              onChanged: (value) => beautyStore.setSmoothLevel(value),
            ),
            SizedBox(height: 20),
            // 美白
            _buildBeautySlider(
              title: '美白',
              valueListenable: beautyStore.baseBeautyState.whitenessLevel,
              onChanged: (value) => beautyStore.setWhitenessLevel(value),
            ),
            SizedBox(height: 20),
            // 红润
            _buildBeautySlider(
              title: '红润',
              valueListenable: beautyStore.baseBeautyState.ruddyLevel,
              onChanged: (value) => beautyStore.setRuddyLevel(value),
            ),
            SizedBox(height: 40),
            // 重置按钮
            ElevatedButton(
              onPressed: () {
                beautyStore.reset();
              },
              child: Text('重置美颜'),
            ),
          ],
        ),
      ),
    );
  }

  Widget _buildBeautySlider({
    required String title,
    required ValueListenable<double> valueListenable,
    required ValueChanged<double> onChanged,
  }) {
    return ValueListenableBuilder<double>(
      valueListenable: valueListenable,
      builder: (context, value, child) {
        return Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Row(
              mainAxisAlignment: MainAxisAlignment.spaceBetween,
              children: [
                Text(title, style: TextStyle(fontSize: 16)),
                Text('${value.toInt()}', style: TextStyle(fontSize: 16)),
              ],
            ),
            Slider(
              value: value,
              min: 0,
              max: 9,
              divisions: 9,
              onChanged: onChanged,
            ),
          ],
        );
      },
    );
  }
}
```

## 功能进阶

### 基础美颜与高级美颜对比

AtomicXCore 也提供了高级美颜支持，以满足不同场景的需求：
<table>
<tr>
<td rowspan="1" colSpan="1" >**对比项**</td>

<td rowspan="1" colSpan="1" >**基础美颜 (BaseBeautyStore)**</td>

<td rowspan="1" colSpan="1" >**高级美颜 (TencentEffect 需额外集成)**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >核心功能</td>

<td rowspan="1" colSpan="1" >磨皮、美白、红润</td>

<td rowspan="1" colSpan="1" >包含基础美颜，并增加 V 脸、眼距、瘦鼻、3D 贴纸、滤镜、美妆等丰富效果</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >计费</td>

<td rowspan="1" colSpan="1" >免费 (包含在 AtomicXCore 授权内)</td>

<td rowspan="1" colSpan="1" >付费（需要额外购买腾讯特效 SDK License）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >集成方式</td>

<td rowspan="1" colSpan="1" >默认内置，直接使用 `BaseBeautyStore.shared`</td>

<td rowspan="1" colSpan="1" >需要额外集成 `TencentEffect` 组件并进行鉴权</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >推荐场景</td>

<td rowspan="1" colSpan="1" >对美颜要求不高，需要快速实现基础美颜功能的场景</td>

<td rowspan="1" colSpan="1" >对美颜效果有较高要求，需要丰富的美型、贴纸、滤镜等高级功能的场景</td>
</tr>
</table>


### 集成高级美颜

如果您需要使用高级美颜功能，请参考 [高级美颜](https://cloud.tencent.com/document/product/616/81197) 文档进行集成。集成并成功鉴权 `TencentEffect` 后，您可以通过 `TencentEffect` 提供的接口来控制所有美颜效果。

## API 参考

### BaseBeautyStore
<table>
<tr>
<td rowspan="1" colSpan="1" >**属性/方法**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**说明**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`shared`</td>

<td rowspan="1" colSpan="1" >`BaseBeautyStore`</td>

<td rowspan="1" colSpan="1" >单例实例</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`baseBeautyState`</td>

<td rowspan="1" colSpan="1" >`BaseBeautyState`</td>

<td rowspan="1" colSpan="1" >美颜状态</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`setSmoothLevel`</td>

<td rowspan="1" colSpan="1" >`void`</td>

<td rowspan="1" colSpan="1" >设置磨皮强度（0-9）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`setWhitenessLevel`</td>

<td rowspan="1" colSpan="1" >`void`</td>

<td rowspan="1" colSpan="1" >设置美白强度（0-9）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`setRuddyLevel`</td>

<td rowspan="1" colSpan="1" >`void`</td>

<td rowspan="1" colSpan="1" >设置红润强度（0-9）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`reset`</td>

<td rowspan="1" colSpan="1" >`void`</td>

<td rowspan="1" colSpan="1" >重置所有美颜参数至默认值（0）</td>
</tr>
</table>


### BaseBeautyState
<table>
<tr>
<td rowspan="1" colSpan="1" >**属性**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**说明**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`smoothLevel`</td>

<td rowspan="1" colSpan="1" >`ValueListenable<double>`</td>

<td rowspan="1" colSpan="1" >磨皮强度（0-9）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`whitenessLevel`</td>

<td rowspan="1" colSpan="1" >`ValueListenable<double>`</td>

<td rowspan="1" colSpan="1" >美白强度（0-9）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`ruddyLevel`</td>

<td rowspan="1" colSpan="1" >`ValueListenable<double>`</td>

<td rowspan="1" colSpan="1" >红润强度（0-9）</td>
</tr>
</table>


## 常见问题

### 我设置了美颜参数，为什么没有效果？

请检查以下几点：
1. **摄像头是否开启**：必须先成功打开摄像头（例如通过 `DeviceStore.shared.openLocalCamera()`），美颜效果才能应用到视频流上。

2. **是否使用了高级美颜**：如果您集成了 `TencentEffect` (高级美颜)，请确保您使用的是 `TencentEffect` 提供的接口来调节美颜。

3. **参数范围**：如果您使用基础美颜，请确认您传入的强度值在有效的范围内（`0` 到 `9` 之间的 double 值）。
