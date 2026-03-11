> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

# 腾讯云直播SDK V2TXLiveDef 类型定义文档

## 概述

`V2TXLiveDef` 是腾讯云直播SDK的核心类型定义文件，包含了直播推流和播放相关的所有枚举、常量和数据结构定义。

**文件路径**: `v2_tx_live_def.dart`

**主要功能**:
- 定义视频、音频相关的枚举类型和常量
- 提供统计数据和配置参数的数据结构
- 支持云端混流和本地录制的配置定义

## 一、支持协议

### V2TXLiveMode - 直播 SDK 推流支持的协议类型
```dart
enum V2TXLiveMode {
  /// 支持协议: RTMP
  v2TXLiveModeRTMP,
  
  /// 支持协议: RTC
  v2TXLiveModeRTC,
}
```

## 渲染视图定义

### V2TXLiveRenderView

渲染视图类，用于定义视频渲染视图的类型。

```dart
class V2TXLiveRenderView {
  static const String renderViewType = 'v2_live_view_factory';
}
```

## 协议支持

### V2TXLiveMode

支持的直播协议类型枚举：

| 枚举值 | 描述 |
|--------|------|
| `v2TXLiveModeRTMP` | RTMP 协议 |
| `v2TXLiveModeRTC` | TRTC 协议 |

## 二、视频相关类型定义

### V2TXLiveVideoResolution - 视频分辨率枚举，定义了各种标准分辨率
```dart
enum V2TXLiveVideoResolution {
  /// 分辨率 160*160，码率范围：100Kbps ~ 150Kbps，帧率：15fps。
  v2TXLiveVideoResolution160x160,
  
  /// 分辨率 270*270，码率范围：200Kbps ~ 300Kbps，帧率：15fps。
  v2TXLiveVideoResolution270x270,

  /// 分辨率 480*480，码率范围：350Kbps ~ 525Kbps，帧率：15fps。
  v2TXLiveVideoResolution480x480,

  /// 分辨率 320*240，码率范围：250Kbps ~ 375Kbps，帧率：15fps。
  v2TXLiveVideoResolution320x240,

  ///  分辨率 480*360，码率范围：400Kbps ~ 600Kbps，帧率：15fps。
  v2TXLiveVideoResolution480x360,

  ///  分辨率 640*480，码率范围：600Kbps ~ 900Kbps，帧率：15fps。
  v2TXLiveVideoResolution640x480,

  /// 分辨率 320*180，码率范围：250Kbps ~ 400Kbps，帧率：15fps。
  v2TXLiveVideoResolution320x180,

  ///  分辨率 480*270，码率范围：350Kbps ~ 550Kbps，帧率：15fps。
  v2TXLiveVideoResolution480x270,

  /// 分辨率 640*360，码率范围：500Kbps ~ 900Kbps，帧率：15fps。
  v2TXLiveVideoResolution640x360,

  ///  分辨率 960*540，码率范围：800Kbps ~ 1500Kbps，帧率：15fps。
  v2TXLiveVideoResolution960x540,

  ///  分辨率 1280*720，码率范围：1000Kbps ~ 1800Kbps，帧率：15fps。
  v2TXLiveVideoResolution1280x720,

  ///  分辨率 1920*1080，码率范围：2500Kbps ~ 3000Kbps，帧率：15fps。
  v2TXLiveVideoResolution1920x1080,
}
```

| 分辨率 | 码率范围 | 帧率 | 说明 |
|--------|----------|------|------|
| 160×160 | 100-150Kbps | 15fps | 超低分辨率，适合语音通话 |
| 270×270 | 200-300Kbps | 15fps | 低分辨率 |
| 480×480 | 350-525Kbps | 15fps | 标准方形分辨率 |
| 320×240 | 250-375Kbps | 15fps | 4:3比例标准分辨率 |
| 480×360 | 400-600Kbps | 15fps | 4:3比例中等分辨率 |
| 640×480 | 600-900Kbps | 15fps | 标清分辨率 |
| 320×180 | 250-400Kbps | 15fps | 16:9比例低分辨率 |
| 480×270 | 350-550Kbps | 15fps | 16:9比例标准分辨率 |
| 640×360 | 500-900Kbps | 15fps | 16:9比例中等分辨率 |
| 960×540 | 800-1500Kbps | 15fps | 高清分辨率 |
| 1280×720 | 1000-1800Kbps | 15fps | 720p高清 |
| 1920×1080 | 2500-3000Kbps | 15fps | 1080p全高清 |

### V2TXLiveVideoResolutionMode

视频分辨率模式：

| 枚举值 | 描述 |
|--------|------|
| `v2TXLiveVideoResolutionModeLandscape` | 横屏模式 |
| `v2TXLiveVideoResolutionModePortrait` | 竖屏模式 |

**注意**：分辨率模式会影响实际分辨率尺寸，例如：
- 横屏模式：640×360 = 640×360
- 竖屏模式：640×360 = 360×640

## 视频编码参数

### V2TXLiveVideoResolutionMode - 视频横竖屏模式
```dart
enum V2TXLiveVideoResolutionMode {
  /// 横屏模式
  v2TXLiveVideoResolutionModeLandscape,
  
  /// 竖屏模式
  v2TXLiveVideoResolutionModePortrait,
}
```

### V2TXLiveVideoEncoderParam - 视频编码参数配置类
```dart
class V2TXLiveVideoEncoderParam {
  V2TXLiveVideoResolution videoResolution;      // 视频分辨率
  V2TXLiveVideoResolutionMode videoResolutionMode; // 分辨率模式
  int videoFps;                                 // 视频采集帧率
  int videoBitrate;                             // 目标视频码率
  int minVideoBitrate;                          // 最低视频码率
}
```

**推荐配置**:
- **帧率**: 15fps或20fps（5fps以下卡顿明显，20fps以上浪费带宽）
- **码率自适应**: 通过同时设置videoBitrate和minVideoBitrate来约束码率调整范围

## 视频预览和填充模式

### V2TXLiveMirrorType - 本地摄像头镜像类型
```dart
enum V2TXLiveMirrorType {
  /// 系统默认镜像类型，前置摄像头镜像，后置摄像头不镜像
  v2TXLiveMirrorTypeAuto,
  
  /// 前置摄像头和后置摄像头都切换为镜像模式
  v2TXLiveMirrorTypeEnable,
  
  /// 前置摄像头和后置摄像头都切换为非镜像模式
  v2TXLiveMirrorTypeDisable,
}
```

### V2TXLiveFillMode - 视频画面填充模式
```dart
enum V2TXLiveFillMode {
  /// 图像铺满屏幕，超出部分将被裁剪，画面可能不完整
  v2TXLiveFillModeFill,
  
  /// 图像长边填满屏幕，短边填充黑色，画面内容完整
  v2TXLiveFillModeFit,
  
  /// 图像拉伸铺满，长度和宽度可能不会按比例变化
  v2TXLiveFillModeScaleFill
}
```

### V2TXLiveRotation - 视频画面旋转角度
```dart
enum V2TXLiveRotation {
  /// 不旋转
  v2TXLiveRotation0,
  
  /// 顺时针旋转90度
  v2TXLiveRotation90,
  
  /// 顺时针旋转180度
  v2TXLiveRotation180,
  
  /// 顺时针旋转270度
  v2TXLiveRotation270,
}
```

### V2TXLivePixelFormat - 视频帧像素格式
```dart
enum V2TXLivePixelFormat {
  /// 未知
  v2TXLivePixelFormatUnknown,
  
  /// YUV420P I420格式
  v2TXLivePixelFormatI420,
  
  /// YUV420SP NV12格式
  v2TXLivePixelFormatNV12,
  
  /// BGRA8888格式
  v2TXLivePixelFormatBGRA32,
  
  /// OpenGL 2D纹理格式
  v2TXLivePixelFormatTexture2D,
}
```
### V2TXLiveBufferType - 视频数据包装格式
```dart
enum V2TXLiveBufferType {
  /// 未知
  v2TXLiveBufferTypeUnknown,
  
  /// DirectBuffer，装载I420等buffer，在native层使用
  v2TXLiveBufferTypeByteBuffer,
  
  /// byte[]，装载I420等buffer，在Java层使用
  v2TXLiveBufferTypeByteArray,
  
  /// 直接操作纹理ID，性能最好，画质损失最少
  v2TXLiveBufferTypeTexture,
}
```

### V2TXLiveVideoFrame - 视频帧信息类
```dart
class V2TXLiveVideoFrame {
  V2TXLivePixelFormat pixelFormat;              // 视频帧像素格式
  V2TXLiveBufferType bufferType;                // 视频数据包装格式
  Uint8List? data;                             // 视频数据
  int width;                                   // 视频宽度
  int height;                                  // 视频高度
  V2TXLiveRotation rotation;                   // 视频帧旋转角度
  int? textureId;                              // 视频纹理ID
}
```

## 三、音频相关类型定义

### V2TXLiveAudioQuality - 声音音质配置
```dart
enum V2TXLiveAudioQuality {
  /// 语音音质：16k采样率，单声道，16kbps码率，适合语音通话
  v2TXLiveAudioQualitySpeech,
  
  /// 默认音质：48k采样率，单声道，50kbps码率，SDK默认配置
  v2TXLiveAudioQualityDefault,
  
  /// 音乐音质：48k采样率，双声道+全频带，128kbps码率，适合高保真音乐场景
  v2TXLiveAudioQualityMusic,
}
```

### V2TXLiveAudioFrame - 音频帧数据类
```dart
class V2TXLiveAudioFrame {
  Uint8List data;          // 音频数据
  int sampleRate;         // 采样率（默认48000Hz）
  int channel;            // 声道数（默认1，单声道）
  int timestamp;          // 时间戳，单位ms
}
```

## 四、统计指标数据定义

### V2TXLivePusherStatistics - 推流器统计数据类
```dart
class V2TXLivePusherStatistics {
  int appCpu;           // 当前App的CPU使用率（%）
  int systemCpu;        // 当前系统的CPU使用率（%）
  int width;            // 视频宽度
  int height;           // 视频高度
  int fps;              // 帧率（fps）
  int videoBitrate;     // 视频码率（Kbps）
  int audioBitrate;     // 音频码率（Kbps）
  int rtt;              // SDK到云端的往返延时（ms）
  int netSpeed;         // 上行速度（kbps）
}
```

### V2TXLivePlayerStatistics - 播放器统计数据类
```dart
class V2TXLivePlayerStatistics {
  int appCpu;                   // 当前App的CPU使用率（%）
  int systemCpu;                // 当前系统的CPU使用率（%）
  int width;                    // 视频宽度
  int height;                   // 视频高度
  int fps;                      // 帧率（fps）
  int videoBitrate;             // 视频码率（Kbps）
  int audioBitrate;             // 音频码率（Kbps）
  int audioPacketLoss;          // 网络音频丢包率（%）
  int videoPacketLoss;          // 网络视频丢包率（%）
  int jitterBufferDelay;        // 播放延迟（ms）
  int audioTotalBlockTime;      // 音频播放累计卡顿时长（ms）
  int audioBlockRate;           // 音频播放卡顿率（%）
  int videoTotalBlockTime;      // 视频播放累计卡顿时长（ms）
  int videoBlockRate;           // 视频播放卡顿率（%）
  int rtt;                      // 往返延时（ms）
  int netSpeed;                 // 下载速度（kbps）
}
```

## 五、连接状态相关枚举

### V2TXLivePushStatus - 直播流连接状态
```dart
enum V2TXLivePushStatus {
  /// 与服务器断开连接
  v2TXLivePushStatusDisconnected,
  
  /// 正在连接服务器
  v2TXLivePushStatusConnecting,
  
  /// 连接服务器成功
  v2TXLivePushStatusConnectSuccess,
  
  /// 重连服务器中
  v2TXLivePushStatusReconnecting,
}
```

## 六、云端混流配置

### V2TXLiveMixInputType - 混流输入类型
```dart
enum V2TXLiveMixInputType {
  /// 混入音视频
  v2TXLiveMixInputTypeAudioVideo,
  
  /// 只混入视频
  v2TXLiveMixInputTypePureVideo,
  
  /// 只混入音频
  v2TXLiveMixInputTypePureAudio,
}
```

### V2TXLiveMixStream - 云端混流子画面位置信息
```dart
class V2TXLiveMixStream {
  String userId;                // 参与混流的userId
  String? streamId;            // 推流streamId
  int x;                        // 图层位置x坐标（绝对像素值）
  int y;                        // 图层位置y坐标（绝对像素值）
  int width;                    // 图层宽度（绝对像素值）
  int height;                   // 图层高度（绝对像素值）
  int zOrder;                   // 图层层次（1-15，不可重复）
  V2TXLiveMixInputType inputType; // 直播流输入类型
}
```

### V2TXLiveTranscodingConfig - 云端混流转码配置
```dart
class V2TXLiveTranscodingConfig {
  int videoWidth;               // 最终转码后的视频宽度
  int videoHeight;              // 最终转码后的视频高度
  int videoBitrate;             // 最终转码后的视频码率（kbps）
  int videoFramerate;           // 最终转码后的视频帧率（FPS）
  int videoGOP;                 // 关键帧间隔（秒）
  int backgroundColor;          // 混合后画面的底色颜色
  String? backgroundImage;      // 混合后画面的背景图
  int audioSampleRate;          // 最终转码后的音频采样率
  int audioBitrate;             // 最终转码后的音频码率（kbps）
  int audioChannels;            // 最终转码后的音频声道数
  List<V2TXLiveMixStream> mixStreams; // 子画面位置信息
  String? outputStreamId;        // 输出到CDN的直播流ID
}
```

## 七、本地录制配置

### V2TXLiveRecordMode - 本地音视频录制模式
```dart
enum V2TXLiveRecordMode {
  /// 录制音频和视频
  v2TXLiveRecordModeBoth,
}
```

### V2TXLiveLocalRecordingParams - 本地录制配置参数
```dart
class V2TXLiveLocalRecordingParams {
  String filePath;              // 录制的文件地址（必填）
  V2TXLiveRecordMode recordMode; // 媒体录制模式
  int interval;                 // 录制信息更新频率（毫秒）
}
```

## 混流配置

### V2TXLiveMixInputType

混流输入类型：

| 枚举值 | 描述 |
|--------|------|
| `v2TXLiveMixInputTypeAudioVideo` | 混入音视频 |
| `v2TXLiveMixInputTypePureVideo` | 仅混入视频 |
| `v2TXLiveMixInputTypePureAudio` | 仅混入音频 |

### V2TXLiveMixStream

混流画面位置配置：

```dart
class V2TXLiveMixStream {
  String userId;
  String? streamId;
  int x;
  int y;
  int width;
  int height;
  int zOrder;
  V2TXLiveMixInputType inputType;
}
```

### V2TXLiveTranscodingConfig

云端混流（转码）配置：

```dart
class V2TXLiveTranscodingConfig {
  int videoWidth;
  int videoHeight;
  int videoBitrate;
  int videoFramerate;
  int videoGOP;
  int backgroundColor;
  String? backgroundImage;
  int audioSampleRate;
  int audioBitrate;
  int audioChannels;
  List<V2TXLiveMixStream> mixStreams;
  String? outputStreamId;
}
```

**重要参数说明**：

- **纯音频推流**：设置 `videoWidth × videoHeight = 0px × 0px`
- **背景图片**：需要先在腾讯云控制台上传图片获取 Image ID
- **输出流 ID**：不设置时默认混流到 API 调用者的视频流

## 八、日志配置

### V2TXLiveLogLevel - 日志级别枚举
```dart
class V2TXLiveLogLevel {
  static const int v2TXLiveLogLevelAll = 0;      // 输出所有级别的log
  static const int v2TXLiveLogLevelDebug = 1;   // 输出DEBUG及以上级别
  static const int v2TXLiveLogLevelInfo = 2;    // 输出INFO及以上级别
  static const int v2TXLiveLogLevelWarning = 3; // 输出WARNING及以上级别
  static const int v2TXLiveLogLevelError = 4;   // 输出ERROR及以上级别
  static const int v2TXLiveLogLevelFatal = 5;   // 只输出FATAL级别
  static const int v2TXLiveLogLevelNULL = 6;    // 不输出任何SDK log
}
```

### V2TXLiveLogConfig - 日志配置类
```dart
class V2TXLiveLogConfig {
  int logLevel;                  // 设置Log级别
  bool enableObserver;           // 是否通过Observer接收Log信息
  bool enableConsole;            // 是否在编辑器控制台打印Log
  bool enableLogFile;            // 是否启用本地Log文件
  String? logPath;               // 本地Log存储目录
}
```

**默认日志存储位置**：
- iOS & Mac：沙盒 Documents/log
- Android 6.7 及以下：/sdcard/log/liteav
- Android 6.8 及以上：/sdcard/Android/data/包名/files/log/liteav/

## 九、其他配置

### V2TXLiveSocks5ProxyConfig - Socks5代理协议配置
```dart
class V2TXLiveSocks5ProxyConfig {
  bool supportHttps = true;  // 是否支持HTTPS
  bool supportTcp = true;     // 是否支持TCP
  bool supportUdp = true;     // 是否支持UDP
}
```

### V2TXLiveStreamInfo - 自适应切换的码流信息
```dart
class V2TXLiveStreamInfo {
  int width;                    // 视频宽度
  int height;                   // 视频高度
  int bitrate;                  // 码率（bps）
  double framerate;             // 帧率
  String url;                   // 流地址
}
```

### TXSystemVolumeType - 系统音量控制类型
```dart
class TXSystemVolumeType {
  static const int TXSystemVolumeTypeAuto = 0;  // 自动模式切换
  static const int TXSystemVolumeTypeMedia = 1;  // 全媒体音量
  static const int TXSystemVolumeTypeVOIP = 2;   // 通话音量
}
```

### TXAudioRoute - 音频路由类型
```dart
class TXAudioRoute {
  static const int TXAudioRouteSpeakerphone = 0; // 扬声器播放
  static const int TXAudioRouteEarpiece = 1;     // 听筒播放
}
```

## 十、音效处理

### TXVoiceReverbType - 混响效果类型
```dart
class TXVoiceReverbType {
  static const int TXVoiceReverbTypeOff = 0;      // 关闭混响
  static const int TXVoiceReverbTypeKTV = 1;      // KTV
  static const int TXVoiceReverbTypeSmallRoom = 2; // 小房间
  static const int TXVoiceReverbTypeGreatHall = 3; // 大会堂
  static const int TXVoiceReverbTypeDeep = 4;     // 深沉
  static const int TXVoiceReverbTypeLoud = 5;     // 洪亮
  static const int TXVoiceReverbTypeMetallic = 6; // 金属声
  static const int TXVoiceReverbTypeMagnetic = 7; // 磁性
  static const int TXVoiceReverbTypeEthereal = 8; // 空灵
  static const int TXVoiceReverbTypeStudio = 9;    // 录音棚
  static const int TXVoiceReverbTypeMelodious = 10; // 悠扬
  static const int TXVoiceReverbTypeStudio2 = 11;  // 录音棚2
}
```

### TXVoiceChangerType - 变声效果类型
```dart
class TXVoiceChangerType {
  static const int TXVoiceChangerTypeOff = 0;      // 关闭变声
  static const int TXVoiceChangerTypeChild = 1;   // 顽皮男孩
  static const int TXVoiceChangerTypeLittleGirl = 2; // 少女
  static const int TXVoiceChangerTypeUncle = 3;    // 中年大叔
  static const int TXVoiceChangerTypeHeavyMetal = 4; // 重金属
  static const int TXVoiceChangerTypeCold = 5;     // 感冒
  static const int TXVoiceChangerTypePunk = 6;    // 朋克
  static const int TXVoiceChangerTypeBeast = 7;    // 狂暴动物
  static const int TXVoiceChangerTypeFatty = 8;    // 肥仔
  static const int TXVoiceChangerTypeStrongCurrent = 9; // 强电流
  static const int TXVoiceChangerTypeRobot = 10;   // 机器人
  static const int TXVoiceChangerTypeEthereal = 11; // 空灵
}
```
