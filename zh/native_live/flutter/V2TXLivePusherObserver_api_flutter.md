> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

# 腾讯云直播SDK V2TXLivePusherObserver 直播推流器回调接口

## 概述

`V2TXLivePusherObserver` 是腾讯云 TRTC 直播 SDK 推流器的观察者回调接口定义文件，提供了推流过程中的各种状态通知、错误处理、数据统计和自定义处理等回调功能。

## 文件信息

- **文件路径**: `v2_tx_live_pusher_observer.dart`
- **依赖文件**: 
  - `v2_tx_live_code.dart` - 错误码定义
  - `v2_tx_live_def.dart` - 类型定义

## 回调类型枚举

### V2TXLivePusherListenerType

定义了推流器观察者的所有回调类型：

```dart
enum V2TXLivePusherListenerType {
  // 详细回调定义...
}
```

## 回调函数定义

```dart
typedef V2TXLivePusherObserver<P> = void Function(V2TXLivePusherListenerType type, P? params);
```

## 回调类型详解

### 1. 错误和警告回调

#### onError
**功能**: 错误回调，表示 SDK 遇到不可恢复的错误
```dart
onError,
```
**参数**:
- `code`: 错误码（[V2TXLiveCode]）
- `msg`: 错误消息（String）
- `extraInfo`: 扩展信息（Map）

**说明**: 必须监听此回调并根据情况给用户适当的 UI 提示

#### onWarning
**功能**: 警告回调，通知非关键问题
```dart
onWarning,
```
**参数**:
- `code`: 警告码（[V2TXLiveCode]）
- `msg`: 警告消息（String）
- `extraInfo`: 扩展信息（Map）

**说明**: 如卡顿或可恢复的解码失败等问题

### 2. 采集状态回调

#### onCaptureFirstAudioFrame
**功能**: 音频采集第一帧完成回调
```dart
onCaptureFirstAudioFrame,
```
**参数**: 无

#### onCaptureFirstVideoFrame
**功能**: 视频采集第一帧完成回调
```dart
onCaptureFirstVideoFrame,
```
**参数**: 无

#### onMicrophoneVolumeUpdate
**功能**: 麦克风采集音量值回调
```dart
onMicrophoneVolumeUpdate,
```
**参数**:
- `volume`: 音量值（int）

### 3. 推流状态回调

#### onPushStatusUpdate
**功能**: 推流器连接状态回调通知
```dart
onPushStatusUpdate,
```
**参数**:
- `status`: 状态（String）
- `errMsg`: 连接状态信息（String）
- `extraInfo`: 扩展信息（Map）

### 4. 统计数据回调

#### onStatisticsUpdate
**功能**: 推流器直播数据统计回调
```dart
onStatisticsUpdate,
```
**参数**:
- `appCpu`: 当前应用 CPU 使用率（%）（int）
- `systemCpu`: 当前系统 CPU 使用率（%）（int）
- `width`: 视频宽度（int）
- `height`: 视频高度（int）
- `fps`: 帧率（int）
- `videoBitrate`: 视频码率（Kbps）（int）
- `audioBitrate`: 音频码率（Kbps）（int）

### 5. 截图回调

#### onSnapshotComplete
**功能**: 截图完成回调
```dart
onSnapshotComplete,
```
**参数**:
- `image`: 截取的视频画面（Uint8List）

### 6. OpenGL 环境回调

#### onGLContextCreated
**功能**: SDK 内部 OpenGL 环境创建通知
```dart
onGLContextCreated,
```
**参数**: 无

#### onGLContextDestroyed
**功能**: SDK 内部 OpenGL 环境销毁通知
```dart
onGLContextDestroyed,
```
**参数**: 无

### 7. 自定义处理回调

#### onProcessVideoFrame
**功能**: 自定义视频处理回调
```dart
onProcessVideoFrame,
```
**参数**: 视频帧处理相关参数

### 8. 云端混流转码回调

#### onSetMixTranscodingConfig
**功能**: 设置云端混流转码参数回调
```dart
onSetMixTranscodingConfig,
```
**参数**:
- `errCode`: 错误码（[V2TXLiveCode]）
- `errMsg`: 错误消息（String）

### 9. 屏幕共享回调

#### onScreenCaptureStarted
**功能**: 屏幕共享开始通知回调
```dart
onScreenCaptureStarted,
```
**参数**: 无

#### onScreenCaptureStopped
**功能**: 屏幕共享停止通知回调
```dart
onScreenCaptureStopped,
```
**参数**: 无

## 使用示例

### 基础回调设置示例

```dart
import 'v2_tx_live_pusher_observer.dart';
import 'v2_tx_live_pusher.dart';
import 'v2_tx_live_code.dart';

// 创建推流器实例
V2TXLivePusher pusher = V2TXLivePusher(V2TXLiveMode.V2TXLiveModeRTC);

// 设置观察者回调
pusher.setObserver((type, params) {
  switch (type) {
    case V2TXLivePusherListenerType.onError:
      print('推流错误: code=${params.code}, msg=${params.msg}');
      // 显示错误提示给用户
      break;
      
    case V2TXLivePusherListenerType.onWarning:
      print('推流警告: code=${params.code}, msg=${params.msg}');
      break;
      
    case V2TXLivePusherListenerType.onCaptureFirstAudioFrame:
      print('音频采集第一帧完成');
      break;
      
    case V2TXLivePusherListenerType.onCaptureFirstVideoFrame:
      print('视频采集第一帧完成');
      break;
      
    case V2TXLivePusherListenerType.onMicrophoneVolumeUpdate:
      print('麦克风音量: ${params.volume}');
      break;
      
    case V2TXLivePusherListenerType.onPushStatusUpdate:
      print('推流状态更新: status=${params.status}, errMsg=${params.errMsg}');
      break;
      
    case V2TXLivePusherListenerType.onStatisticsUpdate:
      print('统计数据: appCpu=${params.appCpu}%, systemCpu=${params.systemCpu}%, '
            'width=${params.width}, height=${params.height}, fps=${params.fps}, '
            'videoBitrate=${params.videoBitrate}Kbps, audioBitrate=${params.audioBitrate}Kbps');
      break;
      
    case V2TXLivePusherListenerType.onSnapshotComplete:
      print('截图完成，图像数据大小: ${params.image.length} bytes');
      break;
      
    case V2TXLivePusherListenerType.onScreenCaptureStarted:
      print('屏幕共享开始');
      break;
      
    case V2TXLivePusherListenerType.onScreenCaptureStopped:
      print('屏幕共享停止');
      break;
      
    default:
      break;
  }
});
```

### 高级功能示例

```dart
// OpenGL 环境回调处理
pusher.setObserver((type, params) {
  switch (type) {
    case V2TXLivePusherListenerType.onGLContextCreated:
      print('OpenGL 环境已创建，可以进行自定义渲染设置');
      break;
      
    case V2TXLivePusherListenerType.onGLContextDestroyed:
      print('OpenGL 环境已销毁，清理相关资源');
      break;
      
    case V2TXLivePusherListenerType.onProcessVideoFrame:
      // 自定义视频处理逻辑
      // params 包含视频帧数据，可以进行美颜、滤镜等处理
      break;
      
    case V2TXLivePusherListenerType.onSetMixTranscodingConfig:
      if (params.errCode == V2TXLiveCode.V2TXLIVE_OK) {
        print('云端混流转码配置成功');
      } else {
        print('云端混流转码配置失败: ${params.errMsg}');
      }
      break;
      
    default:
      break;
  }
});
```

## 回调处理最佳实践

### 1. 错误处理策略
```dart
case V2TXLivePusherListenerType.onError:
  // 根据错误码进行不同的处理
  switch (params.code) {
    case V2TXLiveCode.V2TXLIVE_ERROR_NET_DISCONNECT:
      // 网络断开，提示用户检查网络
      showNetworkErrorDialog();
      break;
    case V2TXLiveCode.V2TXLIVE_ERROR_CAMERA_START_FAILED:
      // 摄像头启动失败，检查权限
      checkCameraPermission();
      break;
    default:
      // 其他错误处理
      showGenericError(params.msg);
      break;
  }
  break;
```

### 2. 性能监控
```dart
case V2TXLivePusherListenerType.onStatisticsUpdate:
  // 监控性能指标
  if (params.appCpu > 80) {
    print('应用 CPU 使用率过高，建议优化');
  }
  if (params.fps < 15) {
    print('帧率过低，可能影响直播质量');
  }
  break;
```

### 3. 状态管理
```dart
case V2TXLivePusherListenerType.onPushStatusUpdate:
  // 根据推流状态更新 UI
  switch (params.status) {
    case 'CONNECTING':
      updateUIState('连接中...');
      break;
    case 'CONNECTED':
      updateUIState('推流中');
      break;
    case 'DISCONNECTED':
      updateUIState('连接断开');
      break;
  }
  break;
```

## 注意事项

1. **错误回调必须处理**: `onError` 回调表示不可恢复的错误，必须给用户适当的提示
2. **回调线程**: 所有回调都在非 UI 线程执行，需要切换到 UI 线程更新界面
3. **性能考虑**: 在回调中避免执行耗时操作，以免影响推流性能
4. **资源管理**: OpenGL 相关回调需要正确管理资源生命周期
5. **截图数据**: `onSnapshotComplete` 返回的图像数据较大，使用后及时释放
6. **自定义处理**: `onProcessVideoFrame` 回调中处理视频帧时要注意性能影响
