> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

# 腾讯云直播SDK V2TXLivePlayerObserver 播放器回调接口文档

## 概述

`V2TXLivePlayerObserver` 是腾讯云直播SDK的播放器回调接口，用于接收播放器的各种状态通知和事件回调。通过实现该接口的回调方法，开发者可以监控播放器的运行状态、处理播放事件、获取统计数据等。

**文件路径**: `v2_tx_live_player_observer.dart`
**平台支持**: Flutter

**主要功能**:
- 播放器状态监控（错误、警告、连接状态）
- 音视频播放事件回调
- 播放统计数据和性能指标
- 自定义渲染和音频处理
- 本地录制任务管理
- SEI消息接收和处理

## 回调方法详解

### 1. 错误和警告回调

#### onError() - 播放器错误通知
```dart
void onError(V2TXLivePlayer player, int code, String msg, Map<String, dynamic> extraInfo)
```

**功能**: 播放器出现错误时回调

**参数**:
- `player`: 触发回调的播放器实例
- `code`: 错误码，参考 `V2TXLiveCode` 枚举
- `msg`: 错误描述信息
- `extraInfo`: 扩展信息，包含详细的错误上下文

**使用场景**:
- rtc拉流参数不合法
- rtc拉流超时
- rtc拉流服务器处理失败
- 找不到hevc解码器

**示例**:
```dart
player.addListener(V2TXLivePlayerObserver(
  onError: (player, code, msg, extraInfo) {
    switch (code) {
      case V2TXLiveCode.V2TXLIVE_ERROR_INVALID_PARAMETER:
        print('rtc拉流参数不合法，$msg');
        break;
      case V2TXLiveCode.V2TXLIVE_ERROR_REQUEST_TIMEOUT:
        print('rtc拉流超时，$msg');
        break;
      case V2TXLiveCode.V2TXLIVE_ERROR_SERVER_PROCESS_FAILED:
        print('rtc拉流服务器处理失败，请检查拉流参数，$msg');
        break;
      case V2TXLiveCode.V2TXLIVE_ERROR_DISCONNECTED:
        print('拉流断开，$msg');
        break;
      case V2TXLiveCode.V2TXLIVE_ERROR_NO_AVAILABLE_HEVC_DECODERS:
        print('找不到hevc解码器，可以切换到avc流进行播放，$msg');
        break;
      default:
        print('其它错误，$msg');
        break;
    }
  }
));
```

#### onWarning() - 播放器警告通知
```dart
void onWarning(V2TXLivePlayer player, int code, String msg, Map<String, dynamic> extraInfo)
```

**功能**: 播放器出现警告时回调

**参数**:
- `player`: 触发回调的播放器实例
- `code`: 警告码，参考 `V2TXLiveCode` 枚举
- `msg`: 警告描述信息
- `extraInfo`: 扩展信息

**使用场景**:
- 视频渲染发生卡顿
- 解码器类型变更

**示例**:
```dart
player.addListener(V2TXLivePlayerObserver(
  onWarning: (player, code, msg, extraInfo) {
    switch (code) {
      case V2TXLiveCode.V2TXLIVE_WARNING_VIDEO_BLOCK:
        print('视频渲染发生卡顿');
        break;
      case V2TXLiveCode.V2TXLIVE_WARNING_CURRENT_DECODE_TYPE_CHANGED:
        int codecType = extraInfo['codec_type'];
        if (codecType == 0) {
          print('解码器类型变更，h.264，$msg');
        } else if (codecType == 1) {
          print('解码器类型变更，h.265，$msg');
        }
        break;
      default:
        print('其它警告，$msg');
        break;
    }
  }
));
```

## 回调类型枚举

### V2TXLivePlayerListenerType

播放器监听器类型枚举，定义了所有可用的回调事件类型：

| 枚举值 | 描述 | 参数说明 |
|--------|------|----------|
| `onError` | **错误回调** - SDK 不可恢复的错误通知 | `code`: 错误码（V2TXLiveCode）<br>`msg`: 错误消息<br>`extraInfo`: 扩展信息 |
| `onWarning` | **警告回调** - 非关键问题通知（如卡顿、可恢复的解码失败） | `code`: 警告码（V2TXLiveCode）<br>`msg`: 警告消息<br>`extraInfo`: 扩展信息 |
| `onVideoResolutionChanged` | **视频分辨率变化通知** | `width`: 视频宽度<br>`height`: 视频高度 |
| `onConnected` | **连接成功通知** | `extraInfo`: 扩展信息 |
| `onVideoPlaying` | **视频播放事件** | `firstPlay`: 首次播放标志<br>`extraInfo`: 扩展信息 |
| `onAudioPlaying` | **音频播放事件** | `firstPlay`: 首次播放标志<br>`extraInfo`: 扩展信息 |
| `onVideoLoading` | **视频加载事件** | `extraInfo`: 扩展信息 |
| `onAudioLoading` | **音频加载事件** | `extraInfo`: 扩展信息 |
| `onPlayoutVolumeUpdate` | **播放音量更新** | `volume`: 音量值（0-100） |
| `onStatisticsUpdate` | **播放器统计信息回调** | `appCpu`: 应用 CPU 使用率（%）<br>`systemCpu`: 系统 CPU 使用率（%）<br>`width`: 视频宽度<br>`height`: 视频高度<br>`fps`: 帧率<br>`videoBitrate`: 视频码率（Kbps）<br>`audioBitrate`: 音频码率（Kbps） |
| `onSnapshotComplete` | **截图完成回调** | `image`: 截取的视频画面（Uint8List） |
| `onRenderVideoFrame` | **自定义视频渲染回调** | `videoFrame`: 视频帧数据（Map） |
| `onReceiveSeiMessage` | **SEI 消息接收回调** | `payloadType`: 消息类型<br>`data`: 消息内容（Uint8List） |
| `onPictureInPictureStateUpdate` | **画中画状态变化回调** | `state`: 状态码<br>`message`: 状态消息<br>`extraInfo`: 扩展信息 |
| `onStreamSwitched` | **流切换回调** | 参数未详细说明 |

## 回调函数定义

### V2TXLivePlayerObserver

播放器观察者回调函数类型定义：

```dart
typedef V2TXLivePlayerObserver<P> = void Function(
    V2TXLivePlayerListenerType type, 
    P? params
);
```

**参数说明：**
- `type`: 回调事件类型（V2TXLivePlayerListenerType）
- `params`: 回调参数，类型为泛型 P，根据不同的回调类型传递不同的参数结构

## 回调分类说明

### 1. 错误和警告回调

#### onError
- **重要性**: 高
- **触发时机**: SDK 发生不可恢复的错误时
- **处理建议**: 必须监听此回调，并根据错误码给用户适当的 UI 提示

#### onWarning  
- **重要性**: 中
- **触发时机**: 发生非关键问题，如卡顿、可恢复的解码失败等
- **处理建议**: 可选择性监听，用于监控播放质量

### 2. 连接和状态回调

#### onConnected() - 网络连接成功回调
```dart
void onConnected(V2TXLivePlayer player, Map<String, dynamic> extraInfo)
```

**功能**: 播放器成功连接到服务器时回调

**参数**:
- `player`: 触发回调的播放器实例
- `extraInfo`: 连接相关信息

**使用场景**:
- 监控播放器网络连接状态
- 确认播放器已建立连接

**示例**:
```dart
player.addListener(V2TXLivePlayerObserver(
  onConnected: (player, extraInfo) {
    print('服务器连接成功');
  }
));
```

#### onVideoResolutionChanged() - 视频分辨率变化回调
```dart
void onVideoResolutionChanged(V2TXLivePlayer player, int width, int height)
```

**功能**: 视频分辨率发生变化时回调

**参数**:
- `player`: 触发回调的播放器实例
- `width`: 新的视频宽度
- `height`: 新的视频高度

**使用场景**:
- 自适应视频渲染视图
- 动态调整播放器布局

**示例**:
```dart
player.addListener(V2TXLivePlayerObserver(
  onVideoResolutionChanged: (player, width, height) {
    print('视频流分辨率发生变化: width-$width, height-$height');
  }
));
```

### 3. 播放事件回调

#### onVideoPlaying() - 视频开始播放事件
```dart
void onVideoPlaying(V2TXLivePlayer player, bool firstPlay, Map<String, dynamic> extraInfo)
```

**功能**: 视频开始播放时回调，除首次播放外，与onVideoLoading配对使用

**参数**:
- `player`: 触发回调的播放器实例
- `firstPlay`: 是否为首次播放标志
- `extraInfo`: 播放相关信息

**使用场景**:
- 显示播放状态UI
- 开始播放计时
- 记录播放日志
- 计算秒开耗时

**示例**:
```dart
player.addListener(V2TXLivePlayerObserver(
  onVideoPlaying: (player, firstPlay, extraInfo) {
    if (firstPlay) {
      // 视频首次开始播放
      print('首次开始播放');
    } else {
      // 视频非首次开始播放，可以隐藏加载 UI
      print('开始播放');
    }
  }
));
```

#### onVideoLoading() - 视频开始加载事件
```dart
void onVideoLoading(V2TXLivePlayer player, Map<String, dynamic> extraInfo)
```

**功能**: 视频数据加载时回调

**参数**:
- `player`: 触发回调的播放器实例
- `extraInfo`: 加载状态信息

**使用场景**:
- 显示加载动画
- 缓冲状态提示

**示例**:
```dart
player.addListener(V2TXLivePlayerObserver(
  onVideoLoading: (player, extraInfo) {
    // 视频播放开始加载，可以显示加载 UI
    print('视频播放开始加载');
  }
));
```

#### onAudioPlaying() - 音频开始播放事件
```dart
void onAudioPlaying(V2TXLivePlayer player, bool firstPlay, Map<String, dynamic> extraInfo)
```

**功能**: 音频开始播放时回调

**参数**:
- `player`: 触发回调的播放器实例
- `firstPlay`: 是否为首次播放标志
- `extraInfo`: 播放相关信息

**使用场景**:
- 音频播放状态监控
- 纯音频流播放场景

**示例**:
```dart
player.addListener(V2TXLivePlayerObserver(
  onAudioPlaying: (player, firstPlay, extraInfo) {
    if (firstPlay) {
      print('音频首次开始播放');
    } else {
      print('音频开始播放');
    }
  }
));
```

#### onAudioLoading() - 音频开始加载事件
```dart
void onAudioLoading(V2TXLivePlayer player, Map<String, dynamic> extraInfo)
```

**功能**: 音频数据加载时回调

**参数**:
- `player`: 触发回调的播放器实例
- `extraInfo`: 加载状态信息

**使用场景**:
- 显示加载动画
- 缓冲状态提示

**示例**:
```dart
player.addListener(V2TXLivePlayerObserver(
  onAudioLoading: (player, extraInfo) {
    // 音频播放开始加载
    print('音频播放开始加载');
  }
));
```

### 3. 音视频质量监控回调

#### onVideoResolutionChanged
- **触发时机**: 直播流分辨率发生变化时
### 4. 音视频数据处理回调

#### onPlayoutVolumeUpdate() - 音量更新回调
```dart
void onPlayoutVolumeUpdate(V2TXLivePlayer player, int volume)
```

**功能**: 播放音量大小实时回调

**参数**:
- `player`: 触发回调的播放器实例
- `volume`: 当前播放音量值（0-100）

**前提条件**: 需要调用 `enableVolumeEvaluation()` 开启音量评估

**使用场景**:
- 实时音量显示
- 音频波形动画
- 静音检测

**示例**:
```dart
player.addListener(V2TXLivePlayerObserver(
  onPlayoutVolumeUpdate: (player, volume) {
    // 音频播放音量回调，可以更新音量大小
    print('音频播放音量，音量：$volume');
  }
));
player.enableVolumeEvaluation(300);
```

#### onRenderVideoFrame() - 自定义视频渲染回调
```dart
void onRenderVideoFrame(V2TXLivePlayer player, Map<String, dynamic> videoFrame)
```

**功能**: 自定义视频帧渲染回调

**参数**:
- `player`: 触发回调的播放器实例
- `videoFrame`: 视频帧数据，包含像素格式、缓冲区类型等信息

**前提条件**: 需要调用 `enableObserveVideoFrame()` 开启视频帧回调

**使用场景**:
- 自定义视频渲染
- 添加滤镜效果
- 视频水印处理

**示例**:
```dart
// 开启自定义渲染
await player.enableObserveVideoFrame(true, 
    V2TXLivePixelFormat.v2TXLivePixelFormatTexture2D, 
    V2TXLiveBufferType.v2TXLiveBufferTypeTexture);

player.addListener(V2TXLivePlayerObserver(
  onRenderVideoFrame: (player, videoFrame) {
    // 自定义渲染逻辑
    print('收到视频帧数据: ${videoFrame['width']}x${videoFrame['height']}');
  }
));
```

#### onPlayoutAudioFrame() - 音频数据回调
```dart
void onPlayoutAudioFrame(V2TXLivePlayer player, Map<String, dynamic> audioFrame)
```

**功能**: 音频数据播放回调

**参数**:
- `player`: 触发回调的播放器实例
- `audioFrame`: 音频帧数据，包含采样率、声道数等信息

**前提条件**: 需要调用 `enableObserveAudioFrame()` 开启音频帧回调

**使用场景**:
- 自定义音频处理
- 音频分析
- 实时音频效果

**示例**:
```dart
// 开启音频数据监听
await player.enableObserveAudioFrame(true);

player.addListener(V2TXLivePlayerObserver(
  onPlayoutAudioFrame: (player, audioFrame) {
    // 自定义音频处理逻辑
    print('收到音频帧数据，采样率: ${audioFrame['sampleRate']}');
  }
));
```

### 5. 统计和监控回调

#### onStatisticsUpdate() - 统计数据回调
```dart
void onStatisticsUpdate(V2TXLivePlayer player, Map<String, dynamic> statistics)
```

**功能**: 播放器统计数据实时回调，约2秒回调一次

**参数**:
- `player`: 触发回调的播放器实例
- `statistics`: 播放统计信息，包含以下字段：
  - `appCpu`: 应用CPU使用率（%）
  - `systemCpu`: 系统CPU使用率（%）
  - `width`: 视频宽度
  - `height`: 视频高度
  - `fps`: 帧率
  - `videoBitrate`: 视频码率（Kbps）
  - `audioBitrate`: 音频码率（Kbps）
  - `audioSampleRate`: 音频采样率
  - `audioChannels`: 音频声道数

**使用场景**:
- 播放质量监控
- 性能优化分析
- 用户体验统计

**示例**:
```dart
player.addListener(V2TXLivePlayerObserver(
  onStatisticsUpdate: (player, statistics) {
    print('播放统计信息:');
    print('  - 应用CPU: ${statistics['appCpu']}%');
    print('  - 系统CPU: ${statistics['systemCpu']}%');
    print('  - 分辨率: ${statistics['width']}x${statistics['height']}');
    print('  - 帧率: ${statistics['fps']}fps');
    print('  - 视频码率: ${statistics['videoBitrate']}Kbps');
    print('  - 音频码率: ${statistics['audioBitrate']}Kbps');
  }
));
```

### 6. 高级功能回调

#### onSnapshotComplete() - 截图完成回调
```dart
void onSnapshotComplete(V2TXLivePlayer player, Uint8List image)
```

**功能**: 截图操作完成回调

**参数**:
- `player`: 触发回调的播放器实例
- `image`: 截取的视频画面数据（Uint8List）

**使用场景**:
- 视频截图保存
- 画面分享功能

**示例**:
```dart
player.addListener(V2TXLivePlayerObserver(
  onSnapshotComplete: (player, image) {
    // 处理截图数据
    print('截图完成，图片大小: ${image.length} bytes');
    // 可以保存到文件或分享
  }
));
player.snapshot();
```

#### onReceiveSeiMessage() - SEI消息接收回调
```dart
void onReceiveSeiMessage(V2TXLivePlayer player, int payloadType, Uint8List data)
```

**功能**: 接收SEI（Supplemental Enhancement Information）消息回调

**参数**:
- `player`: 触发回调的播放器实例
- `payloadType`: SEI消息类型
- `data`: SEI消息数据

**前提条件**: 需要调用 `enableReceiveSeiMessage()` 开启SEI消息接收

**使用场景**:
- 场景信息传递
- 互动消息传输
- 时间戳同步

**示例**:
```dart
// 开启SEI消息接收
await player.enableReceiveSeiMessage(true, 5);

player.addListener(V2TXLivePlayerObserver(
  onReceiveSeiMessage: (player, payloadType, data) {
    // 处理SEI消息
    print('收到SEI消息，类型: $payloadType，数据大小: ${data.length} bytes');
  }
));
```

#### onStreamSwitched() - 流切换回调
```dart
void onStreamSwitched(V2TXLivePlayer player, String url, int code)
```

**功能**: 分辨率切换操作完成回调，调用 `switchStream()` 时回调

**参数**:
- `player`: 触发回调的播放器实例
- `url`: 切换后的播放地址
- `code`: 切换状态码（0:成功，-1:超时，-2:服务端错误，-3:客户端错误）

**使用场景**:
- 清晰度切换监控
- 流切换状态反馈

**示例**:
```dart
player.startLivePlay("http://example.com/live/stream_1080p.flv");

player.addListener(V2TXLivePlayerObserver(
  onStreamSwitched: (player, url, code) {
    if (code == 0) {
      print('切换成功');
    } else if (code == -1) {
      print('切换超时');
    } else if (code == -2) {
      print('切换失败，服务端错误');
    } else if (code == -3) {
      print('切换失败，客户端错误');
    }
  }
));

await player.switchStream("http://example.com/live/stream_720p.flv");
```
### 7. 本地录制回调

#### onLocalRecordBegin() - 录制开始回调
```dart
void onLocalRecordBegin(V2TXLivePlayer player, int code, String storagePath)
```

**功能**: 本地录制任务开始回调，调用 `startLocalRecording()` 时回调

**参数**:
- `player`: 触发回调的播放器实例
- `code`: 录制状态码
- `storagePath`: 录制文件存储路径

**状态码说明**:
- `0`: 录制任务启动成功
- `-1`: 内部错误导致录制失败
- `-2`: 文件后缀名有误
- `-6`: 录制已经启动
- `-7`: 录制文件已存在
- `-8`: 录制目录无写入权限

#### onLocalRecording() - 录制进度回调
```dart
void onLocalRecording(V2TXLivePlayer player, int durationMs, String storagePath)
```

**功能**: 录制任务进行中进度回调，频率与 `startLocalRecording()` 传入的 `interval` 参数一致

**参数**:
- `player`: 触发回调的播放器实例
- `durationMs`: 已录制时长（毫秒）
- `storagePath`: 录制文件存储路径

**使用场景**:
- 录制进度显示
- 录制时长限制
- 录制状态监控

#### onLocalRecordComplete() - 录制完成回调
```dart
void onLocalRecordComplete(V2TXLivePlayer player, int code, String storagePath)
```

**功能**: 录制任务完成回调，调用 `stopLocalRecording()` 时回调

**参数**:
- `player`: 触发回调的播放器实例
- `code`: 录制完成状态码
- `storagePath`: 录制文件存储路径

**状态码说明**:
- `0`: 结束录制任务成功
- `-1`: 录制失败
- `-2`: 切换分辨率或横竖屏导致录制结束
- `-3`: 录制时间太短或未采集到数据

**示例**:
```dart
player.addListener(V2TXLivePlayerObserver(
  onLocalRecordBegin: (player, code, storagePath) {
    print('开始录制');
  },
  onLocalRecording: (player, durationMs, storagePath) {
    print('录制中..., durationMs: $durationMs');
  },
  onLocalRecordComplete: (player, code, storagePath) {
    print('录制完成');
  }
));

V2TXLiveLocalRecordingParams params = V2TXLiveLocalRecordingParams(
  filePath: "filepath",
  interval: 2000
);
V2TXLiveCode code = await player.startLocalRecording(params);
if (code == V2TXLiveCode.V2TXLIVE_OK) {
    print('录制开启成功');
} else if (code == V2TXLiveCode.V2TXLIVE_ERROR_INVALID_PARAMETER) {
    print('录制参数不合法');
} else if (code == V2TXLiveCode.V2TXLIVE_ERROR_REFUSED) {
    print('录制调用被拒绝');
}
```

### 8. 使用示例

#### 基础播放器回调实现
```dart
class MyPlayerObserver extends V2TXLivePlayerObserver {
  @override
  void onError(V2TXLivePlayer player, int code, String msg, Map<String, dynamic> extraInfo) {
    // 处理播放错误
    print('PlayerError: 错误码: $code, 错误信息: $msg');
  }
  
  @override
  void onConnected(V2TXLivePlayer player, Map<String, dynamic> extraInfo) {
    // 连接成功处理
    print('Player: 成功连接到服务器');
  }
  
  @override
  void onVideoPlaying(V2TXLivePlayer player, bool firstPlay, Map<String, dynamic> extraInfo) {
    // 视频开始播放
    if (firstPlay) {
      print('Player: 首次播放开始');
    }
  }
  
  @override
  void onStatisticsUpdate(V2TXLivePlayer player, Map<String, dynamic> statistics) {
    // 更新播放统计信息
    print('PlayerStats: 帧率: ${statistics['fps']}, 码率: ${statistics['videoBitrate']}');
  }
}

// 设置回调观察者
V2TXLivePlayer player = await V2TXLivePlayer.create();
player.addListener(MyPlayerObserver());
```

#### 自定义视频处理示例
```dart
class VideoProcessorObserver extends V2TXLivePlayerObserver {
  @override
  void onRenderVideoFrame(V2TXLivePlayer player, Map<String, dynamic> videoFrame) {
    // 自定义视频帧处理
    // 可以添加滤镜、水印等效果
    processVideoFrame(videoFrame);
  }
  
  void processVideoFrame(Map<String, dynamic> frame) {
    // 视频帧处理逻辑
    print('处理视频帧: ${frame['width']}x${frame['height']}');
  }
}

// 开启自定义视频帧回调
await player.enableObserveVideoFrame(true);
player.addListener(VideoProcessorObserver());
```

#### 本地录制监控示例
```dart
class RecordingObserver extends V2TXLivePlayerObserver {
  @override
  void onLocalRecordBegin(V2TXLivePlayer player, int code, String storagePath) {
    if (code == 0) {
      print('Recording: 录制开始，文件路径: $storagePath');
    } else {
      print('Recording: 录制失败，错误码: $code');
    }
  }
  
  @override
  void onLocalRecording(V2TXLivePlayer player, int durationMs, String storagePath) {
    // 更新录制进度
    updateRecordingProgress(durationMs);
  }
  
  @override
  void onLocalRecordComplete(V2TXLivePlayer player, int code, String storagePath) {
    if (code == 0) {
      print('Recording: 录制完成，文件路径: $storagePath');
    } else {
      print('Recording: 录制异常结束，状态码: $code');
    }
  }
  
  void updateRecordingProgress(int durationMs) {
    print('录制进度: ${durationMs}ms');
  }
}

player.addListener(RecordingObserver());
```
## 注意事项

### 1. 回调线程安全
- **主线程回调**: 除自定义渲染回调外，其它所有回调方法都在UI主线程执行
- **线程切换**: 自定义渲染回调可能在非UI线程执行，需要进行线程安全处理

### 2. 性能影响
- **自定义渲染**: 开启自定义视频渲染可能影响播放性能，建议仅在必要时使用
- **音频处理**: 音频数据回调可能增加CPU开销，合理控制处理频率
- **统计频率**: 统计数据回调约2秒一次，避免在回调中进行耗时操作

### 3. 内存管理
- **观察者释放**: 及时释放不再使用的观察者对象，避免内存泄漏
- **回调引用**: 避免在回调中持有对播放器的强引用，防止循环引用
- **资源清理**: 播放器销毁前确保移除所有观察者

### 4. 错误处理
- **错误码解析**: 合理处理各种错误码，提供友好的用户提示
- **异常捕获**: 在回调方法中添加异常捕获，防止崩溃
- **状态恢复**: 根据错误类型实现相应的状态恢复逻辑

### 5. 权限和配置
- **存储权限**: 本地录制需要确保有存储权限和足够的存储空间
- **网络权限**: 播放器需要网络权限才能正常拉流
- **音频权限**: 音频播放需要音频权限支持

### 6. 最佳实践

#### 错误处理最佳实践
```dart
player.addListener(V2TXLivePlayerObserver(
  onError: (player, code, msg, extraInfo) {
    try {
      // 根据错误码提供用户友好的提示
      switch (code) {
        case V2TXLiveCode.V2TXLIVE_ERROR_INVALID_PARAMETER:
          showToast('播放地址无效，请检查后重试');
          break;
        case V2TXLiveCode.V2TXLIVE_ERROR_REQUEST_TIMEOUT:
          showToast('网络连接超时，请检查网络后重试');
          break;
        default:
          showToast('播放失败，请稍后重试');
          break;
      }
    } catch (e) {
      print('错误处理异常: $e');
    }
  }
));
```

#### 性能监控最佳实践
```dart
player.addListener(V2TXLivePlayerObserver(
  onStatisticsUpdate: (player, statistics) {
    // 监控播放质量
    double fps = statistics['fps'];
    double bitrate = statistics['videoBitrate'];
    
    if (fps < 15) {
      // 帧率过低，可能卡顿
      print('警告：帧率过低 ($fps fps)');
    }
    
    if (bitrate < 500) {
      // 码率过低，可能画质差
      print('警告：视频码率过低 ($bitrate Kbps)');
    }
  }
));
```

#### 内存管理最佳实践
```dart
class PlayerManager {
  V2TXLivePlayer? player;
  V2TXLivePlayerObserver? observer;
  
  Future<void> initPlayer() async {
    player = await V2TXLivePlayer.create();
    observer = V2TXLivePlayerObserver(
      onConnected: (player, extraInfo) {
        print('连接成功');
      }
    );
    player!.addListener(observer!);
  }
  
  void dispose() {
    // 先移除观察者
    if (player != null && observer != null) {
      player!.removeListener(observer!);
    }
    // 再销毁播放器
    player?.destroy();
    player = null;
    observer = null;
  }
}
```

## 常见问题解答

### Q: 为什么没有收到回调？
A: 请检查：
1. 是否正确设置了观察者 `player.addListener(observer)`
2. 播放器是否已成功创建和初始化
3. 是否在正确的时机注册回调

### Q: 自定义渲染回调性能差怎么办？
A: 建议：
1. 优化渲染逻辑，避免复杂计算
2. 使用异步处理减少主线程阻塞
3. 仅在必要时开启自定义渲染

### Q: 本地录制失败如何处理？
A: 检查：
1. 存储权限是否授予
2. 存储路径是否有效且有写入权限
3. 存储空间是否充足

### Q: SEI消息接收不到？
A: 确认：
1. 是否调用了 `enableReceiveSeiMessage()` 开启接收
2. payloadType 是否与发送端一致
3. 流媒体是否包含SEI消息

## 文件信息

- **文件路径**: `/Users/borryzhang/Work/Project/liteav_flutter/sdk/trtc/v3/lib/v2_tx_live_player_observer.dart`
- **文件大小**: 3.26 KB
- **总行数**: 140 行
- **平台支持**: Flutter
- **SDK版本**: v3
