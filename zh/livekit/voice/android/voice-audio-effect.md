> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

本篇文档旨在指导您如何使用 `AtomicXCore` 框架中的  `AudioEffectStore` 和 `DeviceStore` 模块，为您的直播应用快速集成音效控制功能，包括麦克风音量、耳返监听，并添加多种趣味变声效果和混响效果。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027182232/21a3b5cdb63011f09a6b525400454e06.png)


## 核心功能

通过组合 `AudioEffectStore` 和 `DeviceStore`，您将能实现以下核心功能：
- **人声音量调节**：控制本地音频上行的采集音量大小，即观众听到的您的声音大小。

- **耳返功能**：允许主播或连麦用户通过耳机实时听到自己的声音，用于监听和矫正发音。

- **变声效果**：提供多种趣味变声选项，如萝莉、大叔、熊孩子等。

- **混响效果**：模拟不同环境的声场效果，如 KTV、金属声、低沉、洪亮等。


## 概念说明
<table>
<tr>
<td rowspan="1" colSpan="1" >**核心概念**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**核心职责与描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`AudioChangerType`</td>

<td rowspan="1" colSpan="1" >`enum class`</td>

<td rowspan="1" colSpan="1" >变声效果枚举，例如，“小孩”，“男人”等。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" ><br>`AudioReverbType`<br></td>

<td rowspan="1" colSpan="1" >`enum class`</td>

<td rowspan="1" colSpan="1" >混响效果枚举，例如，“ktv”，“礼堂”等。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`AudioEffectState`</td>

<td rowspan="1" colSpan="1" >`data class`</td>

<td rowspan="1" colSpan="1" >代表音效模块的当前状态，通常用于UI渲染。包括变声状态、混响状态、耳返开启状态、耳返音量。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`AudioEffectStore`</td>

<td rowspan="1" colSpan="1" >`abstract class`</td>

<td rowspan="1" colSpan="1" >代表音效模块**单例数据管理类**。通过它您可以调用修改音效接口，当您调用接口后，相应的`state`属性会自动更新，可以通过订阅这个state响应式数据来接收和监听状态更新。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`DeviceState`</td>

<td rowspan="1" colSpan="1" >`data class`</td>

<td rowspan="1" colSpan="1" >代表设备模块的当前状态，通常用于UI渲染。核心属性包括摄像头、麦克风的设备状态。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`DeviceStore`</td>

<td rowspan="1" colSpan="1" >`abstract class`</td>

<td rowspan="1" colSpan="1" >代表设备模块**单例数据管理类**。通过它您可以调用操作摄像头、麦克风接口，当您调用接口后，相应的`state`属性会自动更新，可以通过订阅这个state响应式数据来接收和监听状态更新。</td>
</tr>
</table>


## 实现步骤

### 步骤1：组件集成

请参考 [快速接入](https://write.woa.com/document/192834878686547968) 集成 **AtomicXCore。**

### 步骤2：获取 Store 实例

`AudioEffectStore` 和 `DeviceStore`是单例对象，您可以直接通过 shared 属性在项目的任何位置获取实例。您也可以参考 TUILiveKit 开源UI demo项目中的 [AudioEffectPanel.kt](https://github.com/Tencent-RTC/TUIKit_Android/blob/main/live/tuilivekit/src/main/java/com/trtc/uikit/livekit/component/audioeffect/AudioEffectPanel.kt) 文件来了解完整的实现逻辑。
``` java
import io.trtc.tuikit.atomicxcore.api.device.AudioEffectStore
import io.trtc.tuikit.atomicxcore.api.device.DeviceStore

val audioEffectStore = AudioEffectStore.shared()
val deviceStore = DeviceStore.shared()
```

### 步骤3：实现耳返功能

耳返功能允许用户实时监听自己的麦克风声音，可以通过调用本节介绍的接口管理耳返功能。

> **注意：**
> 

> 耳返功能通常需要连接耳机才能正常工作。
> 


#### 实现方式:
1. **开关耳返**：您可以使用`Switch`控件实现开关耳返功能。

2. **设置耳返音量值**：您可以使用 `SeekBar` 控件实现左右拖动滑块来调节音量的功能，并将 `SeekBar` 的值映射成音量值，调用`setOutputVolume(volume)。`请注意，该接口接收的参数范围是 `[0, 150]，`所以您需要将 UI 控件的值（例如 UISlider 的 `0 - 1.0`）映射到 `0 - 150` 的范围。

3. **监听状态更新UI**：您可以订阅实时的耳返状态值更新 `UI`。


#### 代码示例:
``` java
import io.trtc.tuikit.atomicxcore.api.device.AudioEffectStore
import kotlinx.coroutines.CoroutineScope
import kotlinx.coroutines.Dispatchers
import kotlinx.coroutines.launch

// 1. 开启耳返（建议提示用户插入耳机）
audioEffectStore.setVoiceEarMonitorEnable(true)

// 2. 调节耳返音量
audioEffectStore.setVoiceEarMonitorVolume(80)

// 3. 关闭耳返
audioEffectStore.setVoiceEarMonitorEnable(false)

// 4. 监听状态
CoroutineScope(Dispatchers.Main).launch {
  audioEffectStore.audioEffectState.earMonitorVolume.collect {
    print("耳返音量: $it")
    //更新UI 显示数值
   }
}
```

#### setVoiceEarMonitorEnable 接口参数
<table>
<tr>
<td rowspan="1" colSpan="1" >**参数名**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`enable`</td>

<td rowspan="1" colSpan="1" >`Boolean`</td>

<td rowspan="1" colSpan="1" >是否开启耳返。<br>- true：开启<br>- false：关闭</td>
</tr>
</table>


#### setVoiceEarMonitorVolume 接口参数
<table>
<tr>
<td rowspan="1" colSpan="1" >**参数名**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`volume`</td>

<td rowspan="1" colSpan="1" >`Int`</td>

<td rowspan="1" colSpan="1" >耳返音量大小。<br>- 取值范围： [0, 150]<br>- 默认值：100</td>
</tr>
</table>


### 步骤4：实现人声音量调节

当主播希望调节自己的上行采集音量大小时，调用`DeviceStore`的`setCaptureVolume(volume)`方法传入音量值即可。

#### 实现方式:
1. **设置采集音量值**：您可以使用 `SeekBar` 控件实现左右拖动滑块来调节音量的功能，并将 `SeekBar` 的值映射成音量值后调用`setCaptureVolume(80)。`请注意，该接口接收的参数范围是 `[0, 150]，`所以您需要将 `UI` 控件的值（例如 `SeekBar` 的 `0 - 150`）映射到 `0 - 150` 的范围。

2. **监听状态更新 UI**：您可以订阅实时的音量状态值更新 UI。


#### 示例代码：
``` java
import kotlinx.coroutines.CoroutineScope
import kotlinx.coroutines.Dispatchers
import kotlinx.coroutines.launch
import io.trtc.tuikit.atomicxcore.api.device.AudioEffectStore
import io.trtc.tuikit.atomicxcore.api.device.DeviceStore

// 1. 调节音量
deviceStore.setCaptureVolume(80)

// 2. 监听数据变化
CoroutineScope(Dispatchers.Main).launch {
   deviceStore.deviceState.captureVolume.collect {
     //更新显示数值
     print("采集音量: $it")
   }
}
```

#### setCaptureVolume 接口参数
<table>
<tr>
<td rowspan="1" colSpan="1" >**参数名**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`volume`</td>

<td rowspan="1" colSpan="1" >`Int`</td>

<td rowspan="1" colSpan="1" >采集音量大小。<br>- 取值范围： [0, 150]<br>- 默认值：100</td>
</tr>
</table>


### 步骤5：实现变声效果

当主播希望改变自己的声音时，您可以调用 `setAudioChangerType(type)`方法，传入相应的Type 枚举值即可切换效果。

#### 示例代码：
``` java
import io.trtc.tuikit.atomicxcore.api.device.AudioEffectStore
import io.trtc.tuikit.atomicxcore.api.device.AudioChangerType

// 示例：设置变声为“萝莉”
audioEffectStore.setAudioChangerType(AudioChangerType.LITTLE_GIRL)

// 示例：关闭变声
audioEffectStore.setAudioChangerType(AudioChangerType.NONE)
```

#### setAudioChangerType 接口参数
<table>
<tr>
<td rowspan="1" colSpan="1" >**参数名**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`type`</td>

<td rowspan="1" colSpan="1" >`AudioChangerType`</td>

<td rowspan="1" colSpan="1" >变声效果枚举。</td>
</tr>
</table>


### 步骤6：实现混响效果

当主播希望给自己的声音添加混响效果时，您可以调用`setAudioReverbType(type)` 方法，传入相应的Type 枚举值即可切换效果。
``` java
import io.trtc.tuikit.atomicxcore.api.device.AudioEffectStore
import io.trtc.tuikit.atomicxcore.api.device.AudioReverbType

// 示例：设置混响为“KTV”
audioEffectStore.setAudioReverbType(AudioReverbType.KTV)

// 示例：关闭混响
audioEffectStore.setAudioReverbType(AudioReverbType.NONE)
```

#### setAudioReverbType 接口参数
<table>
<tr>
<td rowspan="1" colSpan="1" >**参数名**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`type`</td>

<td rowspan="1" colSpan="1" >`AudioReverbType`</td>

<td rowspan="1" colSpan="1" >混响效果枚举。</td>
</tr>
</table>


### 步骤7：重置音效设置

> **重要：**
> 

> `AudioEffectStore` 和 `DeviceStore` 是单例，这意味着音效和设备设置是全局生效的，如果您在当前直播间的设置不想影响到您创建的其他直播间，就需要在当前直播间结束的时候重置音效和设备设置。
> 


以下两种情况您可能需要重置音效设置：
1. 当前直播间结束时，需要重置音效设置。

2. 您需要提供“一键恢复”的功能，可以通过调用 `store` 的`reset()` 方法实现。

   ``` java
   import io.trtc.tuikit.atomicxcore.api.device.AudioEffectStore
   import io.trtc.tuikit.atomicxcore.api.device.DeviceStore
   
   // 一键重置所有变声和混响效果
   AudioEffectStore.shared().reset()
   DeviceStore.shared().reset()
   
   ```

## API 文档

关于 [AudioEffectStore](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.device/-audio-effect-store/index.html) 和 [DeviceStore](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.device/-device-store/index.html) 及其相关类的所有公开接口、属性的详细信息，请参阅随 [AtomicXCore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore) 框架的官方 API 文档。
<table>
<tr>
<td rowspan="1" colSpan="1" >**Store/Component**</td>

<td rowspan="1" colSpan="1" >**功能描述**</td>

<td rowspan="1" colSpan="1" >**API 文档**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**AudioEffectStore**</td>

<td rowspan="1" colSpan="1" >音效管理：进行音效设置，并获取实时音效状态。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.device/-audio-effect-store/index.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**DeviceStore **</td>

<td rowspan="1" colSpan="1" >设备管理：进行摄像头、麦克风操作，并获取实时设备状态。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.device/-device-store/index.html)</td>
</tr>
</table>


## 常见问题

### 音效和设备接口的调用时机有没有要求？

没有限制。`AudioEffectStore`和`DeviceStore` 的设置是全局生效的，您可以在进入直播间之前或之后随时调用相关接口（如设置变声、混响或耳返），设置会立即生效并被保留。

### **“人声音量” 和“耳返音量” 有什么区别？**

这是一个非常重要且易混淆的概念，区别如下：
- **人声音量 (CaptureVolume)：**通过 `DeviceStore.setCaptureVolume()` 设置**。它决定了观众**能听到的您的声音大小。

- **耳返音量 (EarMonitorVolume)：**通过 `AudioEffectStore.setVoiceEarMonitorVolume()`** 设置。它只**决定了**您自己**在耳机里听到的监听声音大小，**不会**影响观众。


### **新创建的直播间为什么直接就有音效、或者出现音量很大、很小等问题？**

`AudioEffectStore`和`DeviceStore`是单例，这意味着音效和设备设置是全局生效的，出现这种情况很可能是因为您之前设置过音效但是没有重置，需要在合适的地方调用`reset()`方法重置。

### **为什么我开启了“耳返”，但是听不到自己的声音？**

请您按照以下步骤检查：
1. **是否插入耳机**：耳返功能绝大多数情况下依赖耳机才能生效，请确保已连接有线或蓝牙耳机。

2. **音量是否为0**：检查“耳返音量”是否被设置为了 0。

3. **麦克风是否开启**：确认 `DeviceStore` 中的麦克风是开启状态（即已调用 `openLocalMicrophone`）。


### **变声效果 和混响效果 可以同时生效吗？**

可以。`AudioChangerType` 和 `AudioReverbType` 是可以叠加生效的。例如，您可以同时设置 `AudioChangerType.LITTLE_GIRL` 变声和 `AudioReverbType.KTV` 混响。

