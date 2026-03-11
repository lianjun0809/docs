> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

# 腾讯云直播SDK V2TXLivePusher 推流接口文档

## 概述

`V2TXLivePusher` 是腾讯云 TRTC 直播 SDK 的核心推流器接口类，负责将本地的音频和视频画面进行编码，并推送到指定的推流地址，支持任意的推流服务端。

### 🎯 主要能力
- ✅ **多采集源支持**: 摄像头、麦克风、屏幕、图片、自定义采集
- ✅ **画面控制**: 旋转、填充模式、镜像、水印
- ✅ **推流控制**: 开始/停止、暂停/恢复、音视频分离
- ✅ **特效处理**: 美颜、滤镜、贴纸、音效处理
- ✅ **云端混流**: 多路音视频流混合转码
- ✅ **本地录制**: 音视频流本地录制功能
- ✅ **自定义采集**: 支持外部设备和特殊格式采集

### 🔧 技术特性
- **低延迟**: 优化的编码策略和网络自适应
- **高兼容**: 支持多种视频编码格式和分辨率
- **易集成**: 简洁的API设计和完整的回调机制
- **高性能**: 硬件加速编码和高效的采集管线

### 推流器实例创建
```dart
// 创建 RTC 协议推流实例，startPush 必须传入 RTC 协议地址
V2TXLivePusher pusher = await V2TXLivePusher.create(V2TXLiveMode.V2TXLiveModeRTC);
```

**协议选择建议**:
- **RTMP协议**: 适合CDN直播分发场景，延迟较高（2-3秒）
- **RTC协议**: 适合实时互动场景，延迟较低（400ms以内）

## 文件信息

- **文件路径**: `v2_tx_live_pusher.dart`
- **依赖文件**: 
  - `v2_tx_live_code.dart` - 错误码定义
  - `v2_tx_live_def.dart` - 类型定义
  - `v2_tx_live_pusher_observer.dart` - 观察者回调接口
  - `tx_audio_effect_manager.dart` - 音效管理
  - `tx_device_manager.dart` - 设备管理

## 类定义

```dart
abstract class V2TXLivePusher {
  V2TXLivePusher() {}
}
```

## 静态方法

### create
**功能**: 创建推流器实例
```dart
static Future<V2TXLivePusher> create(V2TXLiveMode liveMode) async
```

**参数**:
- `liveMode`: 推流模式 [V2TXLiveMode]

**返回值**:
- `Future<V2TXLivePusher>`: 推流器实例

**使用示例**:
```dart
V2TXLivePusher pusher = await V2TXLivePusher.create(V2TXLiveMode.V2TXLiveModeRTC);
```

## 观察者管理

### addListener
**功能**: 设置推流器回调观察者
```dart
void addListener(V2TXLivePusherObserver observer)
```

**参数**:
- `observer`: 推流器回调观察者对象，需实现 `V2TXLivePusherObserver` 协议

**使用时机**: 推流器初始化后立即设置

**说明**: 通过设置回调，可以监听推流器状态、音量回调、统计数据、警告和错误信息等

**示例**:
```dart
pusher.addListener(V2TXLivePusherObserver(
  onPushStatusUpdate: (status, msg, extraInfo) {
    // 处理推流状态变化
  },
  onStatisticsUpdate: (statistics) {
    // 处理统计信息
  },
  onError: (code, msg, extraInfo) {
    // 处理错误信息
  }
));
```

### removeListener
**功能**: 移除推流器回调观察者
```dart
void removeListener(V2TXLivePusherObserver observer)
```

**参数**:
- `observer`: 推流器回调观察者对象 [V2TXLivePusherObserver]

### destroy
**功能**: 销毁推流器实例
```dart
void destroy()
```

## 视频渲染控制

### setRenderViewID
**功能**: 设置本地摄像头预览视图 ID
```dart
Future<V2TXLiveCode> setRenderViewID(int viewID)
```

**参数**:
- `viewID`: 本地摄像头预览视图 ID

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功

**使用时机**: 必须在开始推流前设置预览视图

**说明**: 本地摄像头采集到的画面，经过美颜、脸型调整、滤镜等多种效果叠加之后，最终会显示在指定的视图上

**示例**:
```dart
await pusher.setRenderViewID(yourTextureViewID);
```

### setRenderMirror
**功能**: 设置摄像头镜像类型
```dart
Future<V2TXLiveCode> setRenderMirror(V2TXLiveMirrorType mirrorType)
```

**参数**:
- `mirrorType`: 镜像类型 [V2TXLiveMirrorType]
  - `V2TXLiveMirrorType.v2TXLiveMirrorTypeAuto`: 默认值，前置摄像头镜像，后置摄像头不镜像
  - `V2TXLiveMirrorType.v2TXLiveMirrorTypeEnable`: 前后置摄像头都镜像
  - `V2TXLiveMirrorType.v2TXLiveMirrorTypeDisable`: 前后置摄像头都不镜像

### setEncoderMirror
**功能**: 设置视频编码镜像（仅影响观众看到的视频效果）
```dart
Future<V2TXLiveCode> setEncoderMirror(bool mirror)
```

**参数**:
- `mirror`: 是否镜像
  - `false`: 默认值，观众看到非镜像图像
  - `true`: 观众看到镜像图像

### setRenderRotation
**功能**: 设置本地摄像头预览画面旋转角度（仅影响本地预览）
```dart
Future<V2TXLiveCode> setRenderRotation(V2TXLiveRotation rotation)
```

**参数**:
- `rotation`: 旋转角度 [V2TXLiveRotation]
  - `V2TXLiveRotation.v2TXLiveRotation0`: 0度，不旋转（默认）
  - `V2TXLiveRotation.v2TXLiveRotation90`: 顺时针旋转90度
  - `V2TXLiveRotation.v2TXLiveRotation180`: 顺时针旋转180度
  - `V2TXLiveRotation.v2TXLiveRotation270`: 顺时针旋转270度

### setRenderFillMode
**功能**: 设置画面填充模式
```dart
Future<V2TXLiveCode> setRenderFillMode(V2TXLiveFillMode mode)
```

**参数**:
- `mode`: 画面填充模式 [V2TXLiveFillMode]
  - `V2TXLiveFillMode.v2TXLiveFillModeFill`: 默认值，图像铺满屏幕，无黑边
  - `V2TXLiveFillMode.v2TXLiveFillModeFit`: 图像适应屏幕，保持画面完整

## 采集控制

### startCamera
**功能**: 开启本地摄像头
```dart
Future<V2TXLiveCode> startCamera(bool frontCamera)
```

**参数**:
- `frontCamera`: 指定摄像头方向是否为前置【默认值】：true

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功

**重要说明**: 
- **推流前必须开启至少一个采集源**，否则推流将失败
- `startVirtualCamera`, `startCamera`, `startScreenCapture` 在同一Pusher实例下，仅有一个采集源可以上行
- 不同采集源之间切换，请先关闭前一采集源，再开启后一采集源

**使用时机**: 必须推流前调用

**示例**:
```dart
// 开启前置摄像头
await pusher.startCamera(true);
// 开启后置摄像头
await pusher.startCamera(false);
```

### stopCamera
**功能**: 关闭本地摄像头
```dart
Future<void> stopCamera()
```

### startMicrophone
**功能**: 开启麦克风
```dart
Future<V2TXLiveCode> startMicrophone()
```

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功

**使用场景**:
- **音视频直播**: 配合摄像头采集提供音频
- **纯音频直播**: 单独使用麦克风进行音频推流
- **屏幕分享**: 配合屏幕采集提供系统声音和麦克风声音

**注意事项**:
- **推流前必须调用此方法开启麦克风采集**，否则推流将只有视频没有音频
- 纯音频推流场景下，可以单独使用麦克风采集
- 推流过程中可以动态开启/关闭麦克风采集

**使用时机**: 推流前必须调用

**示例**:
```dart
// 开启麦克风采集
await pusher.startMicrophone();
// 停止麦克风采集
await pusher.stopMicrophone();
```

### stopMicrophone
**功能**: 关闭麦克风
```dart
Future<V2TXLiveCode> stopMicrophone()
```

### startScreenCapture
**功能**: 开启屏幕共享
```dart
Future<V2TXLiveCode> startScreenCapture(String appGroup)
```

**参数**:
- `appGroup`: iOS专用参数，Android可忽略，主应用与广播进程共享的 Application Group Identifier

**注意**: 与摄像头采集互斥

### stopScreenCapture
**功能**: 关闭屏幕共享
```dart
Future<V2TXLiveCode> stopScreenCapture()
```

## 推流控制

### startPush
**功能**: 开始音视频数据推流
```dart
Future<V2TXLiveCode> startPush(String url)
```

**参数**:
- `url`: 推流的目标地址，支持任意推流服务端

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 操作成功，开始连接推流目标地址
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: 操作失败，url不合法
- `V2TXLIVE_ERROR_INVALID_LICENSE`: 操作失败，license不合法，鉴权失败
- `V2TXLIVE_ERROR_REFUSED`: 操作失败，RTC不支持同一设备上同时推拉同一个StreamId

**重要注意事项**:
- **必须在调用startPush()之前开启至少一个采集源**，否则推流将失败
- 支持的采集源类型：摄像头采集、麦克风采集、屏幕采集、图片推流、自定义采集
- 推流过程中可以切换采集源，但需要先关闭当前采集源再开启新采集源

**使用时机**: 采集源开启后

**示例**:
```dart
V2TXLiveCode result = await pusher.startPush("rtmp://example.com/live/stream");
if (result == V2TXLiveCode.V2TXLIVE_OK) {
    print('开始推流成功');
} else if (result == V2TXLiveCode.V2TXLIVE_ERROR_INVALID_PARAMETER) {
    print('推流地址不合法');
} else if (result == V2TXLiveCode.V2TXLIVE_ERROR_INVALID_LICENSE) {
    print('Licence不合法，请检查Licence');
} else if (result == V2TXLiveCode.V2TXLIVE_ERROR_REFUSED) {
    print('调用被拒绝');
}
```

### stopPush
**功能**: 停止推流
```dart
Future<V2TXLiveCode> stopPush()
```

### isPushing
**功能**: 检查是否正在推流
```dart
Future<V2TXLiveCode> isPushing()
```

**返回值**:
- `1`: 正在推流
- `0`: 推流已停止

## 音视频控制

### pauseAudio
**功能**: 暂停音频流
```dart
Future<V2TXLiveCode> pauseAudio()
```

### resumeAudio
**功能**: 恢复音频流
```dart
Future<V2TXLiveCode> resumeAudio()
```

### pauseVideo
**功能**: 暂停视频流
```dart
Future<V2TXLiveCode> pauseVideo()
```

### resumeVideo
**功能**: 恢复视频流
```dart
Future<V2TXLiveCode> resumeVideo()
```

## 音视频质量设置

### setAudioQuality
**功能**: 设置推流音频质量
```dart
Future<V2TXLiveCode> setAudioQuality(V2TXLiveAudioQuality quality)
```

**参数**:
- `quality`: 音频质量 [V2TXLiveAudioQuality]
  - `V2TXLiveAudioQuality.v2TXLiveAudioQualityDefault`: 默认值，通用
  - `V2TXLiveAudioQuality.v2TXLiveAudioQualitySpeech`: 语音
  - `V2TXLiveAudioQuality.v2TXLiveAudioQualityMusic`: 音乐

**返回值**:
- `V2TXLIVE_OK`: 成功
- `V2TXLIVE_ERROR_REFUSED`: 推流过程中无法调整音质

### setVideoQuality
**功能**: 设置推流视频编码参数
```dart
Future<V2TXLiveCode> setVideoQuality(V2TXLiveVideoEncoderParam param)
```

**参数**:
- `param`: 视频编码参数 [V2TXLiveVideoEncoderParam]

## 音效和设备管理

### getAudioEffectManager
**功能**: 获取音效管理类
```dart
TXAudioEffectManager getAudioEffectManager()
```

**功能说明**:
- **背景音乐**: 支持在线音乐和本地音乐播放，支持变速、变调、原声、伴奏、循环等功能
- **耳返**: 麦克风采集的声音实时在耳机中播放，一般用于音乐直播
- **混响效果**: KTV、小房间、大会堂、深邃、洪亮等效果
- **变声效果**: 萝莉、大叔、重金属等效果
- **短音效**: 支持掌声、笑声等短音效文件（小于10秒的文件请设置`isShortFile`参数为`true`）

### getDeviceManager
**功能**: 获取设备管理类
```dart
TXDeviceManager getDeviceManager()
```

## 高级功能

### snapshot
**功能**: 推流过程中截取本地画面
```dart
Future<V2TXLiveCode> snapshot()
```

**返回值**:
- `V2TXLIVE_OK`: 成功
- `V2TXLIVE_ERROR_REFUSED`: 推流已停止，不允许截图操作

### enableVolumeEvaluation
**功能**: 开启采集音量提示
```dart
Future<V2TXLiveCode> enableVolumeEvaluation(int intervalMs)
```

**参数**:
- `intervalMs`: 音量回调触发间隔（毫秒），最小间隔100ms，小于等于0则禁用回调，建议设置为300ms

### enableCustomVideoProcess
**功能**: 启用/禁用自定义视频处理
```dart
Future<V2TXLiveCode> enableCustomVideoProcess(bool enable, V2TXLivePixelFormat pixelFormat, V2TXLiveBufferType bufferType)
```

**参数**:
- `enable`: true启用，false禁用（默认false）
- `pixelFormat`: 自定义预处理回调视频的像素格式 [V2TXLivePixelFormat]
- `bufferType`: 自定义预处理回调视频的数据格式 [V2TXLiveBufferType]

**支持的格式组合**:
- `V2TXLivePixelFormatTexture2D` + `V2TXLiveBufferTypeTexture`
- `V2TXLivePixelFormatI420` + `V2TXLiveBufferTypeByteBuffer`

### enableCustomVideoCapture
**功能**: 开启/关闭自定义视频采集
```dart
Future<V2TXLiveCode> enableCustomVideoCapture(bool enable)
```

**参数**:
- `enable`: true启用自定义采集，false禁用自定义采集（默认false）

**注意**: 此模式下SDK不再从摄像头采集图像，只保留编码和发送能力，需要在[startPush]之前调用才能生效

### enableCustomAudioCapture
**功能**: 开启/关闭自定义音频采集
```dart
Future<V2TXLiveCode> enableCustomAudioCapture(bool enable)
```

**参数**:
- `enable`: true启用自定义采集，false禁用自定义采集（默认false）

**注意**: 此模式下SDK不再从麦克风采集声音，只保留编码和发送能力，需要在[startPush]之前调用才能生效

### sendCustomVideoFrame
**功能**: 自定义视频采集模式下，将采集的视频数据发送给SDK
```dart
Future<V2TXLiveCode> sendCustomVideoFrame(V2TXLiveVideoFrame videoFrame)
```

**参数**:
- `videoFrame`: 发送给SDK的视频帧数据 [V2TXLiveVideoFrame]

**返回值**:
- `V2TXLIVE_OK`: 成功
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: 发送失败，视频帧数据无效
- `V2TXLIVE_ERROR_REFUSED`: 发送失败，必须先调用[enableCustomVideoCapture]启用自定义视频采集

### sendCustomAudioFrame
**功能**: 自定义音频采集模式下，将采集的音频数据发送给SDK
```dart
Future<V2TXLiveCode> sendCustomAudioFrame(V2TXLiveAudioFrame audioFrame)
```

**参数**:
- `audioFrame`: 发送给SDK的音频帧数据 [V2TXLiveAudioFrame]

**返回值**:
- `V2TXLIVE_OK`: 成功
- `V2TXLIVE_ERROR_REFUSED`: 发送失败，必须先调用[enableCustomAudioCapture]启用自定义音频采集

### sendSeiMessage
**功能**: 发送SEI消息
```dart
Future<V2TXLiveCode> sendSeiMessage(int payloadType, Uint8List data)
```

**参数**:
- `payloadType`: 数据类型，支持5、242，推荐使用242
- `data`: 要发送的数据

**说明**: 播放器通过[V2TXLivePlayerListenerType.onReceiveSeiMessage]回调接收消息

### showDebugView
**功能**: 显示调试面板
```dart
Future<V2TXLiveCode> showDebugView(bool isShow)
```

**参数**:
- `isShow`: 是否显示（默认false）

### setProperty
**功能**: 调用V2TXLivePusher的高级API接口
```dart
Future<V2TXLiveCode> setProperty(String key, Object value)
```

**参数**:
- `key`: 高级API对应的key
- `value`: 调用高级API时需要的参数，为基础类型或jsonString

**返回值**:
- `V2TXLIVE_OK`: 成功
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: 操作失败，key不允许为空

### setMixTranscodingConfig
**功能**: 设置云端的混流转码参数
```dart
Future<V2TXLiveCode> setMixTranscodingConfig(V2TXLiveTranscodingConfig? config)
```

**参数**:
- `config`: 混流转码配置 [V2TXLiveTranscodingConfig]，传入null则取消云端混流转码

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功
- `V2TXLIVE_ERROR_REFUSED`: 未开启推流时，不允许设置混流转码参数

**混流原理**:
```
【画面1】=> 解码 ====> \
                        \
【画面2】=> 解码 =>  画面混合 => 编码 => 【混合后的画面】
                        /
【画面3】=> 解码 ====> /

【声音1】=> 解码 ====> \
                        \
【声音2】=> 解码 =>  声音混合 => 编码 => 【混合后的声音】
                        /
【声音3】=> 解码 ====> /
```

**注意事项**:
- **仅支持RTC协议混流**：该接口只能在RTC协议下使用，不支持RTMP等其他推流协议
- 云端转码会引入1-2秒的CDN观看延迟
- 及时传入null取消混流，避免不必要的计费损失
- 退房时会自动取消混流状态

**使用时机**: 推流过程中

**示例**:
```dart
V2TXLiveTranscodingConfig config = V2TXLiveTranscodingConfig(
  videoWidth: 1280,
  videoHeight: 720,
  videoBitrate: 1500,
  videoFps: 15
);
await pusher.setMixTranscodingConfig(config);

// 取消混流
await pusher.setMixTranscodingConfig(null);
```

## 使用示例

### 基础推流示例（摄像头+麦克风）
```dart
import 'package:tencent_trtc/v2_tx_live_pusher.dart';
import 'package:tencent_trtc/v2_tx_live_pusher_observer.dart';
import 'package:tencent_trtc/v2_tx_live_def.dart';
import 'package:tencent_trtc/v2_tx_live_code.dart';

class BasicPushExample {
  late V2TXLivePusher pusher;
  
  Future<void> setupBasicPush() async {
    // 1. 创建推流器实例
    pusher = await V2TXLivePusher.create(V2TXLiveMode.V2TXLiveModeRTC);
    
    // 2. 设置回调观察者
    pusher.addListener(V2TXLivePusherObserver(
      onPushStatusUpdate: (status, msg, extraInfo) {
        // 处理推流状态变化
        switch (status) {
          case V2TXLivePushStatus.V2TXLivePushStatusDisconnected:
            print('推流连接断开');
            break;
          case V2TXLivePushStatus.V2TXLivePushStatusConnecting:
            print('正在连接推流服务器');
            break;
          case V2TXLivePushStatus.V2TXLivePushStatusConnectSuccess:
            print('推流连接成功');
            break;
          case V2TXLivePushStatus.V2TXLivePushStatusReconnecting:
            print('推流正在重连');
            break;
        }
      },
      onStatisticsUpdate: (statistics) {
        // 处理统计信息
        print('App CPU: ${statistics.appCpu}%, System CPU: ${statistics.systemCpu}%');
        print('Width: ${statistics.width}, Height: ${statistics.height}');
        print('FPS: ${statistics.fps}, Video Bitrate: ${statistics.videoBitrate}');
        print('Audio Bitrate: ${statistics.audioBitrate}');
      },
      onError: (code, msg, extraInfo) {
        // 处理错误信息
        print('推流错误: code=$code, msg=$msg');
      }
    ));
    
    // 3. 设置预览视图
    await pusher.setRenderViewID(yourTextureViewID);
    
    // 4. 重要：推流前必须开启至少一个采集源
    // 开启摄像头采集（前置摄像头）
    await pusher.startCamera(true);
    
    // 开启麦克风采集
    await pusher.startMicrophone();
    
    // 5. 开始推流
    String pushUrl = "rtmp://your-push-server/live/streamid";
    V2TXLiveCode result = await pusher.startPush(pushUrl);
    
    if (result == V2TXLiveCode.V2TXLIVE_OK) {
      print('✅ 开始推流成功');
    } else if (result == V2TXLiveCode.V2TXLIVE_ERROR_INVALID_PARAMETER) {
      print('❌ 推流地址不合法');
    } else if (result == V2TXLiveCode.V2TXLIVE_ERROR_INVALID_LICENSE) {
      print('❌ Licence不合法，请检查Licence');
    } else if (result == V2TXLiveCode.V2TXLIVE_ERROR_REFUSED) {
      print('❌ 调用被拒绝');
    }
  }
  
  Future<void> stopPush() async {
    // 停止推流
    await pusher.stopPush();
    // 停止采集源
    await pusher.stopCamera();
    await pusher.stopMicrophone();
    // 销毁实例
    pusher.destroy();
  }
}
```

### 高级配置示例

```dart
// 设置视频编码参数
V2TXLiveVideoEncoderParam videoParam = V2TXLiveVideoEncoderParam(
  videoResolution: V2TXLiveVideoResolution.v2TXLiveVideoResolution1280x720,
  videoResolutionMode: V2TXLiveVideoResolutionMode.v2TXLiveVideoResolutionModeLandscape,
  videoFps: 15,
  videoBitrate: 1200,
  minVideoBitrate: 800,
);
await pusher.setVideoQuality(videoParam);

// 设置音频质量
await pusher.setAudioQuality(V2TXLiveAudioQuality.v2TXLiveAudioQualityMusic);

// 开启音量评估
await pusher.enableVolumeEvaluation(300);

// 显示调试面板
await pusher.showDebugView(true);
```

### 自定义采集示例

```dart
// 启用自定义视频采集
await pusher.enableCustomVideoCapture(true);

// 自定义视频帧处理
V2TXLiveVideoFrame videoFrame = V2TXLiveVideoFrame(
  pixelFormat: V2TXLivePixelFormat.v2TXLivePixelFormatI420,
  bufferType: V2TXLiveBufferType.v2TXLiveBufferTypeByteBuffer,
  data: yourVideoData,
  width: 640,
  height: 480,
  rotation: V2TXLiveRotation.v2TXLiveRotation0,
);

// 发送自定义视频帧
await pusher.sendCustomVideoFrame(videoFrame);
```

## 注意事项

### 1. 采集源要求（重要）
**推流前必须开启至少一个采集源**，否则推流将失败：
- **摄像头采集**: `startCamera()` + `startMicrophone()`
- **屏幕采集**: `startScreenCapture()` + `startMicrophone()`
- **图片推流**: `startVirtualCamera()` + `startMicrophone()`
- **自定义采集**: `enableCustomVideoCapture()` + `enableCustomAudioCapture()`
- **纯音频推流**: `startMicrophone()`

### 2. 采集源切换规则
- 同一Pusher实例下，仅有一个采集源可以上行
- 不同采集源之间切换需要成对调用：先关闭当前采集源，再开启新采集源

### 3. 调用顺序要求
1. 创建推流器实例
2. 设置回调和预览视图
3. 开启至少一个采集源
4. 调用`startPush()`开始推流

### 4. 自定义采集注意事项
- 需要在`startPush`之前调用自定义采集相关接口才会生效
- 自定义采集模式下，SDK只负责编码和发送，不进行实际采集

### 5. 云端混流注意事项
- **协议限制**: 云端混流功能仅支持RTC协议，不支持RTMP等其他推流协议
- 及时取消混流配置，避免不必要的计费损失
- 云端转码会引入1-2秒的CDN观看延时

### 6. 本地录制注意事项
- 推流开启后才能开始录制
- 录制过程中不要动态切换分辨率和软/硬编

### 7. 系统声音采集要求
- 需要Android API 29及以上版本
- 需要添加前台服务确保采集不被静默
- 只在屏幕分享时真正生效

### 8. 性能优化建议
- 根据场景选择合适的音视频质量参数
- 及时释放不使用的推流器实例
- 合理使用暂停/恢复功能节省带宽

### 9. 错误处理建议
- 必须处理`onError`回调，给用户适当的提示
- 网络异常时自动重连，无需手动处理
- Licence失效时及时更新Licence配置

### 10. 权限和资源管理
- 确保应用有摄像头和麦克风使用权限
- 及时调用`destroy`释放资源
- 避免内存泄漏，及时移除观察者
