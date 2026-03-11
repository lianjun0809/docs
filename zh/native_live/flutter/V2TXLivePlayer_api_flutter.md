> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

# 腾讯云直播SDK V2TXLivePlayer 播放接口文档

## 概述

`V2TXLivePlayer` 是腾讯云直播播放器的核心接口类，负责从指定的直播流地址拉取音视频数据，并进行解码和本地渲染播放。

**文件路径**: `v2_tx_live_player.dart`
**平台支持**: Flutter

## 核心功能

### 🎯 主要能力
- ✅ **多协议支持**: HTTP-FLV、WebRTC、TRTC、HLS、RTMP
- ✅ **画面控制**: 旋转、填充模式、镜像
- ✅ **播放控制**: 播放/停止、暂停/恢复、音量调节
- ✅ **缓存优化**: 自动调整缓存策略
- ✅ **无缝切换**: 直播流多分辨率无缝切换
- ✅ **自定义处理**: 音视频数据监听和自定义渲染
- ✅ **高级功能**: 截图、SEI消息、画中画、本地录制

### 🔧 技术特性
- **低延迟**: 优化的缓存策略和网络自适应
- **高兼容**: 支持多种视频编码格式和分辨率
- **易集成**: 简洁的API设计和完整的回调机制
- **高性能**: 硬件加速解码和高效的渲染管线

### 播放器实例创建
```dart
V2TXLivePlayer player = await V2TXLivePlayer.create();
```

## 接口详解

### 1. 基础设置接口

#### addListener() - 设置播放器回调
```dart
void addListener(V2TXLivePlayerObserver observer)
```

**参数**:
- `observer`: 播放器回调目标对象，需实现 `V2TXLivePlayerObserver` 协议

**使用时机**: 播放器初始化后立即设置

**说明**: 通过设置回调，可以监听播放器状态、播放音量回调、音视频首帧回调、统计数据、警告和错误信息等

**示例**:
```dart
player.addListener(V2TXLivePlayerObserver(
  onConnected: (player) {
    print('播放器已连接');
  },
  onVideoPlaying: (player, isFirstPlay) {
    print('视频开始播放');
  },
));
```

#### setRenderViewID() - 设置视频渲染视图
```dart
Future<V2TXLiveCode> setRenderViewID(int viewID)
```

**参数**:
- `viewID`: 播放器渲染视图ID

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功

**使用时机**: 必须在开始播放前设置渲染视图

**示例**:
```dart
await player.setRenderViewID(viewId);
```

#### setRenderRotation() - 设置播放器画面的旋转角度
```dart
Future<V2TXLiveCode> setRenderRotation(V2TXLiveRotation rotation)
```

**参数**:
- `rotation`: 旋转角度 `V2TXLiveRotation`
  - `v2TXLiveRotation0`【默认值】: 0度, 不旋转
  - `v2TXLiveRotation90`: 顺时针旋转90度
  - `v2TXLiveRotation180`: 顺时针旋转180度
  - `v2TXLiveRotation270`: 顺时针旋转270度

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功

**使用时机**: 无限制

**示例**:
```dart
// 设置视频画面旋转0度
await player.setRenderRotation(V2TXLiveRotation.v2TXLiveRotation0);
// 设置视频画面旋转90度
await player.setRenderRotation(V2TXLiveRotation.v2TXLiveRotation90);
// 设置视频画面旋转180度
await player.setRenderRotation(V2TXLiveRotation.v2TXLiveRotation180);
// 设置视频画面旋转270度
await player.setRenderRotation(V2TXLiveRotation.v2TXLiveRotation270);
```

#### setRenderFillMode() - 设置播放器画面的填充模式
```dart
Future<V2TXLiveCode> setRenderFillMode(V2TXLiveFillMode mode)
```

**参数**:
- `mode`: 填充模式 `V2TXLiveFillMode`
  - `v2TXLiveFillModeFill`:【默认值】: 图像铺满屏幕，不留黑边，如果图像宽高比不同于屏幕宽高比，部分画面内容会被裁剪掉
  - `v2TXLiveFillModeFit`: 图像适应屏幕，保持画面完整，但如果图像宽高比不同于屏幕宽高比，会有黑边的存在
  - `v2TXLiveFillModeScaleFill`: 图像拉伸铺满，因此长度和宽度可能不会按比例变化

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功

**使用时机**: 无限制

**示例**:
```dart
// 图像铺满屏幕
await player.setRenderFillMode(V2TXLiveFillMode.v2TXLiveFillModeFill);
// 图像适应屏幕
await player.setRenderFillMode(V2TXLiveFillMode.v2TXLiveFillModeFit);
// 图像拉伸铺满
await player.setRenderFillMode(V2TXLiveFillMode.v2TXLiveFillModeScaleFill);
```

### 2. 播放控制接口

#### startLivePlay() - 开始播放音视频流
```dart
Future<V2TXLiveCode> startLivePlay(String url)
```

**参数**:
- `url`: 音视频流的播放地址，支持 HTTP-FLV、WebRTC、TRTC、HLS、RTMP

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 操作成功，开始连接并播放
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: 操作失败，url 不合法
- `V2TXLIVE_ERROR_REFUSED`: RTC 不支持同一设备上同时推拉同一个 StreamId
- `V2TXLIVE_ERROR_INVALID_LICENSE`: licence 不合法，播放失败

**重要说明**: 
- 10.7 版本开始，需要通过 `V2TXLivePremier.setLicence` 设置 Licence 后方可成功播放，否则将播放失败（黑屏），全局仅设置一次即可
- 直播 Licence、短视频 Licence 和视频播放 Licence 均可使用

**使用时机**: 无限制

**示例**:
```dart
V2TXLiveCode result = await player.startLivePlay("http://example.com/live/stream_1080p.flv");
if (result == V2TXLiveCode.V2TXLIVE_OK) {
    print("开始播放成功");
} else if (result == V2TXLiveCode.V2TXLIVE_ERROR_INVALID_PARAMETER) {
    print("播放地址不合法");
} else if (result == V2TXLiveCode.V2TXLIVE_ERROR_REFUSED) {
    print("调用被拒绝");
} else if (result == V2TXLiveCode.V2TXLIVE_ERROR_INVALID_LICENSE) {
    print("Licence 不合法，请检查 Licence");
}
```

#### stopPlay() - 停止播放音视频流
```dart
Future<V2TXLiveCode> stopPlay()
```

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功

**使用时机**: 开始播放后

**示例**:
```dart
await player.stopPlay();
```

#### isPlaying() - 播放器是否正在播放中
```dart
Future<int> isPlaying()
```

**返回值**:
- `1`: 正在播放中
- `0`: 已经停止播放

**使用时机**: 无限制

**示例**:
```dart
int isPlaying = await player.isPlaying();
if (isPlaying == 1) {
    print("正在播放中");
} else {
    print("播放停止");
}


### 4. 缓存控制接口

#### setCacheParams() - 设置播放器缓存自动调整的最小和最大时间
```dart
Future<V2TXLiveCode> setCacheParams(double minTime, double maxTime)
```

**参数**:
- `minTime`: 缓存自动调整的最小时间，取值需要大于0【默认值】：1
- `maxTime`: 缓存自动调整的最大时间，取值需要大于0【默认值】：5

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: 操作失败，minTime 和 maxTime 需要大于0

**优化建议**:
- **网络稳定**: 设置较小缓存（1-3秒）
- **网络波动**: 设置较大缓存（3-5秒）
- **无特殊要求**: 建议使用默认值

**使用时机**: 无限制

**示例**:
```dart
await player.setCacheParams(1, 5);
```

### 5. 高级功能接口

#### switchStream() - 直播流多分辨率无缝切换，支持 FLV 和 LEB
```dart
Future<V2TXLiveCode> switchStream(String newUrl)
```

**参数**:
- `newUrl`: 新分辨率拉流地址

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功

**使用时机**: 开始播放后

**示例**:
```dart
await player.startLivePlay("http://example.com/live/stream_1080p.flv");

player.addListener(V2TXLivePlayerObserver(
  onStreamSwitched: (player, url, code) {
    if (code == 0) {
      print("切换成功");
    } else if (code == -1) {
      print("切换超时");
    } else if (code == -2) {
      print("切换失败，服务端错误");
    } else if (code == -3) {
      print("切换失败，客户端错误");
    }
  }
));
await player.switchStream("http://example.com/live/stream_720p.flv");
```
### 6. 缓存控制

#### setCacheParams()
**功能**: 设置播放器缓存自动调整的最小和最大时间
```dart
Future<V2TXLiveCode> setCacheParams(double minTime, double maxTime)
```
**参数**: 
- `minTime`: 缓存自动调整的最小时间（秒），必须大于0，默认值: 1
- `maxTime`: 缓存自动调整的最大时间（秒），必须大于0，默认值: 5

**错误码**:
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: minTime 和 maxTime 需要大于0
- `V2TXLIVE_ERROR_REFUSED`: 播放器处于播放状态，无法修改缓存策略

#### enableVolumeEvaluation() - 启用播放音量大小提示
```dart
Future<V2TXLiveCode> enableVolumeEvaluation(int intervalMs)
```

**参数**:
- `intervalMs`: 决定了 `onPlayoutVolumeUpdate` 回调的触发间隔，单位为ms，最小间隔为100ms，如果小于等于0则会关闭回调，建议设置为300ms【默认值】：0，不开启

**说明**: 开启后可以在 `V2TXLivePlayerObserver` 回调中获取到 SDK 对音量大小值的评估

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功

**使用时机**: 无限制

**示例**:
```dart
player.addListener(V2TXLivePlayerObserver(
  onPlayoutVolumeUpdate: (player, volume) {
    // 音频播放音量回调，可以更新音量大小
    print("音频播放音量，音量：$volume");
  }
));
await player.enableVolumeEvaluation(300);
```

#### snapshot() - 截取播放过程中的视频画面
```dart
Future<V2TXLiveCode> snapshot()
```

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功
- `V2TXLIVE_ERROR_REFUSED`: 播放器处于停止状态，不允许调用截图操作

**使用时机**: 开始播放后

**示例**:
```dart
player.addListener(V2TXLivePlayerObserver(
  onSnapshotComplete: (player, image) {
    // doSomething
  }
));
await player.snapshot();
```

#### enableObserveVideoFrame() - 开启/关闭自定义视频渲染
```dart
Future<V2TXLiveCode> enableObserveVideoFrame(bool enable, int pixelFormat, int bufferType)
```

**参数**:
- `enable`: 是否开启自定义渲染【默认值】：false
- `pixelFormat`: 自定义渲染回调的视频像素格式 `V2TXLivePixelFormat`
- `bufferType`: 自定义渲染回调的视频数据格式 `V2TXLiveBufferType`

**说明**: 
- SDK 在您开启此开关后将不再渲染视频画面，您可以通过 `V2TXLivePlayerObserver` 获得视频帧，并执行自定义的渲染逻辑
- 支持的类型组合：
  `V2TXLivePixelFormat.v2TXLivePixelFormatTexture2D`, `V2TXLiveBufferType.v2TXLiveBufferTypeTexture`（推荐）
  `V2TXLivePixelFormat.v2TXLivePixelFormatI420`, `V2TXLiveBufferType.v2TXLiveBufferTypeByteArray`
  `V2TXLivePixelFormat.v2TXLivePixelFormatI420`, `V2TXLiveBufferType.v2TXLiveBufferTypeByteBuffer`

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功
- `V2TXLIVE_ERROR_NOT_SUPPORTED`: 像素格式或者数据格式不支持

**使用时机**: 开始播放前

**示例**:
```dart
// 开启自定义渲染
await player.enableObserveVideoFrame(true, 
    V2TXLivePixelFormat.v2TXLivePixelFormatTexture2D, 
    V2TXLiveBufferType.v2TXLiveBufferTypeTexture);
player.addListener(V2TXLivePlayerObserver(
  onRenderVideoFrame: (player, videoFrame) {
    // 自定义渲染
  }
));
```

#### enableObserveAudioFrame() - 开启/关闭对音频数据的监听回调
```dart
Future<V2TXLiveCode> enableObserveAudioFrame(bool enable)
```

**参数**:
- `enable`: 是否开启音频数据回调【默认值】：false

**说明**: 如果您开启此开关，您可以通过 `V2TXLivePlayerObserver` 获得音频数据，并执行自定义的逻辑

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功

**使用时机**: 开始播放前

**示例**:
```dart
// 开启音频数据监听
await player.enableObserveAudioFrame(true);
player.addListener(V2TXLivePlayerObserver(
  onPlayoutAudioFrame: (player, audioFrame) {
    // doSomething
  }
));
```

#### enableReceiveSeiMessage() - 开启/关闭接收 SEI 消息
```dart
Future<V2TXLiveCode> enableReceiveSeiMessage(bool enable, int payloadType)
```

**参数**:
- `enable`: true: 开启接收 SEI 消息; false: 关闭接收 SEI 消息【默认值】: false
- `payloadType`: 指定接收 SEI 消息的 payloadType，支持 5、242、243，请与发送端的 payloadType 保持一致

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功

**使用时机**: 开始播放前

**示例**:
```dart
// 开启音频数据监听
await player.enableReceiveSeiMessage(true, 5);
await player.enableReceiveSeiMessage(true, 242);
await player.enableReceiveSeiMessage(true, 243);
player.addListener(V2TXLivePlayerObserver(
  onReceiveSeiMessage: (player, payloadType, data) {
    // doSomething
  }
));
```

### 6. 本地录制接口

#### startLocalRecording() - 开始录制音视频流
```dart
Future<V2TXLiveCode> startLocalRecording(V2TXLiveLocalRecordingParams params)
```

**参数**:
- `params`: 请参考 `V2TXLiveDef.dart` 中关于 `V2TXLiveLocalRecordingParams` 的介绍

**重要说明**:
- 拉流开启后才能开始录制，非拉流状态下开启录制无效
- 录制过程中不要动态切换软/硬解，生成的视频极有可能出现异常

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: 参数不合法，例如 filePath 为空
- `V2TXLIVE_ERROR_REFUSED`: API被拒绝，拉流尚未开始

**使用时机**: 开始播放后

**示例**:
```dart
player.addListener(V2TXLivePlayerObserver(
  onLocalRecordBegin: (player, code, storagePath) {
    print("开始录制");
  },
  onLocalRecording: (player, durationMs, storagePath) {
    print("录制中..., durationMs: $durationMs");
  },
  onLocalRecordComplete: (player, code, storagePath) {
    print("录制完成");
  }
));

V2TXLiveLocalRecordingParams params = V2TXLiveLocalRecordingParams(
  filePath: "filepath",
  interval: 2000
);
V2TXLiveCode code = await player.startLocalRecording(params);
if (code == V2TXLiveCode.V2TXLIVE_OK) {
    print("录制开启成功");
} else if (code == V2TXLiveCode.V2TXLIVE_ERROR_INVALID_PARAMETER) {
    print("录制参数不合法");
} else if (code == V2TXLiveCode.V2TXLIVE_ERROR_REFUSED) {
    print("录制调用被拒绝");
}
```

#### stopLocalRecording() - 停止录制音视频流
```dart
Future<void> stopLocalRecording()
```

**说明**: 当停止拉流后，如果视频还在录制中，SDK 内部会自动结束录制

**使用时机**: 开始播放并且开启录制后

**示例**:
```dart
await player.stopLocalRecording();
```

### 7. 调试和高级配置接口

#### showDebugView() - 是否显示播放器状态信息的调试浮层
```dart
Future<void> showDebugView(bool isShow)
```

**参数**:
- `isShow`: 是否显示【默认值】：false

**使用时机**: 无限制

**示例**:
```dart
await player.showDebugView(true);
```

#### setProperty() - 调用 V2TXLivePlayer 的高级 API 接口
```dart
Future<V2TXLiveCode> setProperty(String key, Object value)
```

**参数**:
- `key`: 高级 API 对应的 key
- `value`: 调用 key 所对应的高级 API 时，需要的参数

**说明**: 该接口用于调用一些高级功能，有特殊需求，请于商务或架构师联系

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: 操作失败，key 不允许为 null

**示例**:
```dart
await player.setProperty("key", "value");
```

## 使用示例

```dart
import 'package:tencent_trtc/v2_tx_live_player.dart';
import 'package:tencent_trtc/v2_tx_live_player_observer.dart';
import 'package:tencent_trtc/v2_tx_live_def.dart';

class LivePlayerExample {
  late V2TXLivePlayer player;
  
  // 初始化播放器
  Future<void> initPlayer() async {
    // 创建播放器实例
    player = await V2TXLivePlayer.create();
    
    // 设置播放器回调
    player.addListener(V2TXLivePlayerObserver(
      onConnected: (player) {
        print('播放器已连接');
      },
      onVideoPlaying: (player, isFirstPlay) {
        print('视频开始播放');
      },
      onAudioPlaying: (player, isFirstPlay) {
        print('音频开始播放');
      },
      onPlayoutVolumeUpdate: (player, volume) {
        print('播放音量更新: $volume');
      },
      onError: (player, code, msg, extraInfo) {
        print('播放器错误: $code, $msg');
      }
    ));
    
    // 设置渲染视图
    await player.setRenderViewID(viewId);
    
    // 设置画面旋转角度
    await player.setRenderRotation(V2TXLiveRotation.v2TXLiveRotation0);
    
    // 设置画面填充模式
    await player.setRenderFillMode(V2TXLiveFillMode.v2TXLiveFillModeFit);
    
    // 设置缓存参数
    await player.setCacheParams(1.0, 5.0);
    
    // 启用音量评估
    await player.enableVolumeEvaluation(300);
  }
  
  // 开始播放
  Future<void> startPlay(String url) async {
    V2TXLiveCode result = await player.startLivePlay(url);
    if (result == V2TXLiveCode.V2TXLIVE_OK) {
      print('开始播放成功');
    } else {
      print('开始播放失败: $result');
    }
  }
  
  // 暂停/恢复视频
  Future<void> toggleVideo() async {
    int isPlaying = await player.isPlaying();
    if (isPlaying == 1) {
      await player.pauseVideo();
      print('视频已暂停');
    } else {
      await player.resumeVideo();
      print('视频已恢复');
    }
  }
  
  // 暂停/恢复音频
  Future<void> toggleAudio() async {
    int isPlaying = await player.isPlaying();
    if (isPlaying == 1) {
      await player.pauseAudio();
      print('音频已暂停');
    } else {
      await player.resumeAudio();
      print('音频已恢复');
    }
  }
  
  // 设置音量
  Future<void> setVolume(int volume) async {
    await player.setPlayoutVolume(volume);
    print('音量设置为: $volume');
  }
  
  // 切换流
  Future<void> switchStream(String newUrl) async {
    await player.switchStream(newUrl);
    print('正在切换流...');
  }
  
  // 截图
  Future<void> takeSnapshot() async {
    await player.snapshot();
    print('截图已触发');
  }
  
  // 停止播放
  Future<void> stopPlay() async {
    await player.stopPlay();
    print('播放已停止');
  }
  
  // 销毁播放器
  void destroyPlayer() {
    player.destroy();
    print('播放器已销毁');
  }
}

// 使用示例
void main() async {
  LivePlayerExample example = LivePlayerExample();
  await example.initPlayer();
  await example.startPlay('http://example.com/live/stream.flv');
  await Future.delayed(Duration(seconds: 10));
  await example.takeSnapshot();
  await example.stopPlay();
  example.destroyPlayer();
}
```

## 注意事项

1. **Licence 要求**: 10.7 版本开始必须设置有效的 Licence 才能正常播放
2. **权限要求**: 需要网络权限和音频播放权限
3. **生命周期管理**: 使用 `create()` 创建实例后，必须调用 `destroy()` 销毁
4. **观察者注册**: 播放前需要注册观察者以接收状态回调
5. **错误处理**: 所有异步方法都返回 `V2TXLiveCode`，需要进行错误处理
6. **线程安全**: 接口调用需要在主线程执行
7. **资源释放**: 播放结束后及时释放资源避免内存泄漏
8. **缓存策略**: 根据网络状况调整缓存参数以获得最佳播放体验

## 常见问题

### Q: 播放器黑屏无画面？
A: 检查是否设置了有效的 Licence，播放地址是否正确，渲染视图是否设置正确

### Q: 播放延迟较高？
A: 调整缓存参数，网络稳定时可设置较小的缓存时间（1-3秒）

### Q: 如何实现无缝切换分辨率？
A: 使用 `switchStream()` 方法切换不同分辨率的流地址

### Q: 如何获取播放统计信息？
A: 通过 `V2TXLivePlayerObserver` 的 `onStatisticsUpdate` 回调获取

