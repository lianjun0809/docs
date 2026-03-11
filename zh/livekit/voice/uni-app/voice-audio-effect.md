> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

本篇文档旨在指导您如何使用 `AtomicXCore` 框架中的  `AudioEffectState` 和 `DeviceState` 模块，为您的直播应用快速集成音效控制功能，包括麦克风音量、耳返监听，并添加多种趣味变声效果和混响效果。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100028028022/46976106baed11f0b0cf525400e889b2.png)


## 核心功能

通过组合 `AudioEffectState` 和 `DeviceState`，您将能实现以下核心功能：
- **人声音量调节**：控制本地音频上行的采集音量大小，即观众听到的您的声音大小。

- **耳返功能**：允许主播或连麦用户通过耳机实时听到自己的声音，用于监听和矫正发音。

- **变声效果**：提供多种趣味变声选项，例如萝莉、大叔、熊孩子等。

- **混响效果**：模拟不同环境的声场效果，例如 KTV、金属声、低沉、洪亮等。


## 实现步骤

### 步骤1：组件集成

请参考 [快速接入](https://write.woa.com/document/191656297444069376) 集成 **AtomicXCore。**

### 步骤2：获取 State 实例

`AudioEffectState` 和 `DeviceState`是单例对象，您可以在项目的任何位置获取实例。
``` typescript
import { useAudioEffectState } from '@/uni_modules/tuikit-atomic-x/state/AudioEffectState'
import { useDeviceState } from "@/uni_modules/tuikit-atomic-x/state/DeviceState";

// liveID 是语聊房的唯一标识
const liveID = 'your_live_id'; // 替换为实际的语聊房 liveID

// 通过 liveID 获取对应实例
useAudioEffectState(liveID)
useDeviceState(liveID)
```

### 步骤3：实现耳返功能

耳返功能允许用户实时监听自己的麦克风声音，可以通过调用本节介绍的接口管理耳返功能。

> **注意：**
> 

> 耳返功能通常需要连接耳机才能正常工作。
> 


#### 实现方式:
1. **开关耳返**：您可以在 `UI` 上自行实现开关耳返功能。

2. **设置耳返音量值**：您可以自行实现左右拖动滑块来调节音量的功能，并将您 `UI` 上的值映射成音量值，调用 `setVoiceEarMonitorVolume(volume:)。`请注意，该接口接收的参数范围是 `[0, 150]`，所以您需要将 UI 控件的值映射到 `0 - 150` 的范围。

3. **监听状态更新 UI**：您可以订阅实时的耳返状态值更新 UI。


#### 代码示例:
``` typescript
import { watch } from 'vue'
import { useAudioEffectState } from '@/uni_modules/tuikit-atomic-x/state/AudioEffectState'

// liveID 是语聊房的唯一标识
const liveID = 'your_live_id'; // 替换为实际的语聊房 liveID


// 通过 liveID 获取对应实例
const { setVoiceEarMonitorEnable, setVoiceEarMonitorVolume, earMonitorVolume } = useAudioEffectState(liveID)

// 1. 开启/关闭耳返
const toggleEarMonitor = () => {
    setVoiceEarMonitorEnable({
      enable: true // true 为开启， false 为关闭
     })
}

// 2. 调节耳返音量
const adjustEarMonitorVolume = () => {
    setVoiceEarMonitorVolume({
      volume: 80
     })
}

// 3.监听耳返音量变化
watch(earMonitorVolume, (newVolume) => {
  console.log('耳返音量:', newVolume);
});
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

<td rowspan="1" colSpan="1" >`boolean`</td>

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

<td rowspan="1" colSpan="1" >`number`</td>

<td rowspan="1" colSpan="1" >耳返音量大小。<br>- 取值范围： [0, 150]<br>- 默认值：100</td>
</tr>
</table>


### 步骤4：实现人声音量调节

当主播希望调节自己的上行采集音量大小时，调用`DeviceState`的`setCaptureVolume(volume: )`方法传入音量值即可。

#### 实现方式:
1. **设置采集音量值**：您可自行实现调节音量的功能，并将 `UI `上的值映射成音量值后调用`setCaptureVolume(volume: 80)。`请注意，该接口接收的参数范围是 `[0, 150]`，所以您需要将 UI 控件的值映射到 `0 - 150` 的范围。

2. **监听状态更新 UI**：您可以订阅实时的音量状态值更新 UI。


#### 示例代码：
``` typescript
import { watch } from 'vue'
import { useDeviceState } from "@/uni_modules/tuikit-atomic-x/state/DeviceState";

// liveID 是语聊房的唯一标识
const liveID = 'your_live_id'; // 替换为实际的语聊房 liveID

/ 通过 liveID 获取对应实例
const { setCaptureVolume, captureVolume } = useDeviceState(liveID)

// 1. 调节音量
const adjustCaptureVolume = () => {
    setCaptureVolume({
      volume: 80
    })
}

// 2. 监听状态
watch(captureVolume, (newVolume) => {
  console.log('采集音量:', newVolume);
});
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

<td rowspan="1" colSpan="1" >`number`</td>

<td rowspan="1" colSpan="1" >采集音量大小。<br>- 取值范围： [0, 150]<br>- 默认值：100</td>
</tr>
</table>


### 步骤5：实现变声效果

当主播希望改变自己的声音时，您可以调用 `setAudioChangerType({type:})`方法，传入相应的枚举值即可切换效果。

#### 示例代码：
``` typescript
import { useAudioEffectState } from '@/uni_modules/tuikit-atomic-x/state/AudioEffectState'

// liveID 是语聊房的唯一标识
const liveID = 'your_live_id'; // 替换为实际的语聊房 liveID
// 通过 liveID 获取对应实例
const { setAudioChangerType } = useAudioEffectState(liveID)

// 示例：将变声效果设置为"小孩"
const applyVoiceChanger = () => {
    setAudioChangerType({
      changerType: 'CHILD'
    })
}
```

#### setAudioChangerType 接口参数
<table>
<tr>
<td rowspan="1" colSpan="1" >**参数名**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`changerType`</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >[变声效果枚举](https://liteav.sdk.qcloud.com/doc/product/tuikit/atomic-x/uni-app/zh/v1.0/api/interface.html#AudioReverbTypeParam)。</td>
</tr>
</table>


### 步骤6：实现混响效果

当主播希望给自己的声音添加混响效果时，您可以调用`setAudioReverbType({type:})` 方法，传入相应的枚举值即可切换效果。
``` typescript
import { useAudioEffectState } from '@/uni_modules/tuikit-atomic-x/state/AudioEffectState'

// liveID 是语聊房的唯一标识
const liveID = 'your_live_id'; // 替换为实际的语聊房 liveID

// 通过 liveID 获取对应实例
const { setAudioReverbType } = useAudioEffectState(liveID)

// 示例：设置为"KTV"混响效果
const applyReverbEffect = () => {
    setAudioReverbType({
      reverbType: 'KTV'
    })
}
```

#### setAudioReverbType 接口参数
<table>
<tr>
<td rowspan="1" colSpan="1" >**参数名**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`reverbType`</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >[混响效果枚举](https://liteav.sdk.qcloud.com/doc/product/tuikit/atomic-x/uni-app/zh/v1.0/api/interface.html#AudioReverbTypeParam)。</td>
</tr>
</table>


## API 文档

关于 [AudioEffectState](https://liteav.sdk.qcloud.com/doc/product/tuikit/atomic-x/uni-app/zh/v1.0/api/index.html#module-AudioEffectState) 和 [DeviceState](https://liteav.sdk.qcloud.com/doc/product/tuikit/atomic-x/uni-app/zh/v1.0/api/index.html#module-DeviceState) 及其相关类的所有公开接口、属性的详细信息，请参阅随 [AtomicXCore](https://write.woa.com/document/192223419814899712) 框架的官方 API 文档。
<table>
<tr>
<td rowspan="1" colSpan="1" >**State**</td>

<td rowspan="1" colSpan="1" >**功能描述**</td>

<td rowspan="1" colSpan="1" >**API 文档**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >AudioEffectState</td>

<td rowspan="1" colSpan="1" >音效管理：进行音效设置，并获取实时音效状态。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://liteav.sdk.qcloud.com/doc/product/tuikit/atomic-x/uni-app/zh/v1.0/api/index.html#module-AudioEffectState)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >DeviceState</td>

<td rowspan="1" colSpan="1" >设备管理：进行摄像头、麦克风操作，并获取实时设备状态。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://liteav.sdk.qcloud.com/doc/product/tuikit/atomic-x/uni-app/zh/v1.0/api/index.html#module-DeviceState)</td>
</tr>
</table>


## 常见问题

### 音效和设备接口的调用时机有没有要求？

没有限制。`AudioEffectState`和`DeviceState` 的设置是全局生效的，您可以在进入直播间之前或之后随时调用相关接口（例如设置变声、混响或耳返），设置会立即生效并被保留。

### **“人声音量” 和“耳返音量” 有什么区别？**

这是一个非常重要且易混淆的概念，区别如下：
- **人声音量 (CaptureVolume)：**通过 `setCaptureVolume()` 设置**。它决定了观众**能听到的您的声音大小。

- **耳返音量 (EarMonitorVolume)：**通过 `setVoiceEarMonitorVolume()`** 设置。它只**决定了**您自己**在耳机里听到的监听声音大小，**不会**影响观众。


### **新创建的直播间为什么直接就有音效、或者出现音量很大、很小等问题？**

`AudioEffectState`和`DeviceState`是单例，这意味着音效和设备设置是全局生效的，出现这种情况很可能是因为您之前设置过音效但是没有重置，需要在合适的地方将数据重置。

### **为什么我开启了“耳返”，但是听不到自己的声音？**

请您按照以下步骤检查：
1. **是否插入耳机**：耳返功能绝大多数情况下依赖耳机才能生效，请确保已连接有线或蓝牙耳机。

2. **音量是否为0**：检查“耳返音量”是否被设置为 0。

3. **麦克风是否开启**：确认 `DeviceState` 中的麦克风是开启状态（即已调用 `openLocalMicrophone`）。


### **变声效果 和混响效果 可以同时生效吗？**

可以。`AudioChangerType` 和 `AudioReverbType` 是可以叠加生效的。例如，您可以同时设置 `'LITTLEGIRL'` 变声和 `'KTV'`混响。







