> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

# 腾讯云直播SDK V2TXLivePusherObserver 直播推流器回调接口

## 概述

`V2TXLivePusherObserver.h` 是腾讯云直播SDK iOS/macOS平台的推流器回调接口定义文件，用于接收推流过程中的各种状态通知、统计数据、错误信息和事件回调。

**平台支持**: iOS, macOS  
**协议类型**: Objective-C Protocol  
**回调总数**: 15个核心回调方法

## 📋 目录结构

### 1. [核心功能特性](#核心功能特性)
### 2. [错误与警告回调](#错误与警告回调)
### 3. [首帧采集回调](#首帧采集回调)
### 4. [推流状态回调](#推流状态回调)
### 5. [统计数据回调](#统计数据回调)
### 6. [音视频处理回调](#音视频处理回调)
### 7. [屏幕分享回调](#屏幕分享回调)
### 8. [本地录制回调](#本地录制回调)
### 9. [高级功能回调](#高级功能回调)
### 10. [使用示例](#使用示例)

## 1. 核心功能特性

### 🎯 回调分类

| 类别 | 回调数量 | 主要功能 |
|------|----------|----------|
| 错误警告 | 2个 | 推流器错误和警告通知 |
| 首帧采集 | 2个 | 音视频首帧采集完成通知 |
| 推流状态 | 1个 | 连接状态变化通知 |
| 统计数据 | 1个 | 实时推流数据统计 |
| 音视频处理 | 3个 | 自定义音视频处理回调 |
| 屏幕分享 | 2个 | 屏幕采集开始/停止通知 |
| 本地录制 | 3个 | 录制任务状态回调 |
| 高级功能 | 1个 | 人声检测状态更新 |

### 🔧 技术特点

- **实时性**: 所有回调均在主线程执行
- **完整性**: 覆盖推流全生命周期的关键事件
- **可扩展性**: 支持自定义音视频处理
- **调试友好**: 提供详细的错误信息和统计数据

## 2. 错误与警告回调

### ⚠️ onError - 错误通知回调

```objc
- (void)onError:(V2TXLiveCode)code message:(NSString *)msg extraInfo:(NSDictionary *)extraInfo;
```

**功能**: 推流器出现错误时的回调通知

**参数说明**:
- `code`: 错误码，参考 `V2TXLiveCode` 枚举
- `msg`: 错误描述信息
- `extraInfo`: 扩展信息字典

**触发时机**:
- 网络连接失败
- 推流地址无效
- 硬件设备异常
- 编码器初始化失败

**处理建议**:
```objc
- (void)onError:(V2TXLiveCode)code message:(NSString *)msg extraInfo:(NSDictionary *)extraInfo {
    NSLog(@"推流错误: %ld - %@", (long)code, msg);
    
    switch (code) {
        case V2TXLIVE_ERROR_NET_DISCONNECT:
            // 网络断开，尝试重连
            [self reconnect];
            break;
        case V2TXLIVE_ERROR_INVALID_LICENSE:
            // License无效，检查配置
            [self checkLicense];
            break;
        default:
            // 其他错误处理
            [self handleError:code];
            break;
    }
}
```

### ⚠️ onWarning - 警告通知回调

```objc
- (void)onWarning:(V2TXLiveCode)code message:(NSString *)msg extraInfo:(NSDictionary *)extraInfo;
```

**功能**: 推流器出现警告时的回调通知

**参数说明**:
- `code`: 警告码，参考 `V2TXLiveCode` 枚举
- `msg`: 警告描述信息
- `extraInfo`: 扩展信息字典

**常见警告场景**:
- 网络状况不佳
- 编码参数不匹配
- 设备资源紧张
- 音视频采集异常

**处理建议**:
```objc
- (void)onWarning:(V2TXLiveCode)code message:(NSString *)msg extraInfo:(NSDictionary *)extraInfo {
    NSLog(@"推流警告: %ld - %@", (long)code, msg);
    
    // 根据警告码进行相应处理
    if (code == V2TXLIVE_WARNING_NETWORK_BUSY) {
        // 网络繁忙，提示用户或降低码率
        [self adjustBitrate];
    }
}
```

## 3. 首帧采集回调

### 🎵 onCaptureFirstAudioFrame - 音频首帧采集

```objc
- (void)onCaptureFirstAudioFrame;
```

**功能**: 首帧音频采集完成的回调通知

**触发时机**: 麦克风成功采集到第一帧音频数据

**使用场景**:
- 音频采集状态监控
- 推流启动时间统计
- 音频设备检测

**示例代码**:
```objc
- (void)onCaptureFirstAudioFrame {
    NSLog(@"音频首帧采集完成");
    [self updateUIWithAudioStatus:YES];
}
```

### 🎥 onCaptureFirstVideoFrame - 视频首帧采集

```objc
- (void)onCaptureFirstVideoFrame;
```

**功能**: 首帧视频采集完成的回调通知

**触发时机**: 摄像头成功采集到第一帧视频数据

**使用场景**:
- 视频采集状态监控
- 预览画面显示时机
- 摄像头设备检测

**示例代码**:
```objc
- (void)onCaptureFirstVideoFrame {
    NSLog(@"视频首帧采集完成");
    [self updateUIWithVideoStatus:YES];
    
    // 可以开始显示预览画面
    [self showPreviewAnimation];
}
```

## 4. 推流状态回调

### 🔄 onPushStatusUpdate - 推流状态更新

```objc
- (void)onPushStatusUpdate:(V2TXLivePushStatus)status message:(NSString *)msg extraInfo:(NSDictionary *)extraInfo;
```

**功能**: 推流器连接状态变化的回调通知

**参数说明**:
- `status`: 推流状态，参考 `V2TXLivePushStatus` 枚举
- `msg`: 状态描述信息
- `extraInfo`: 扩展信息字典

**状态枚举说明**:
```objc
typedef NS_ENUM(NSInteger, V2TXLivePushStatus) {
    V2TXLivePushStatusDisconnected = 0,    // 断开连接
    V2TXLivePushStatusConnecting,         // 正在连接
    V2TXLivePushStatusConnectSuccess,     // 连接成功
    V2TXLivePushStatusReconnecting,        // 重连中
};
```

**状态流转示例**:
```objc
- (void)onPushStatusUpdate:(V2TXLivePushStatus)status message:(NSString *)msg extraInfo:(NSDictionary *)extraInfo {
    switch (status) {
        case V2TXLivePushStatusConnecting:
            NSLog(@"正在连接推流服务器...");
            [self updateStatus:@"连接中"];
            break;
            
        case V2TXLivePushStatusConnectSuccess:
            NSLog(@"推流连接成功");
            [self updateStatus:@"推流中"];
            [self startPushTimer];
            break;
            
        case V2TXLivePushStatusReconnecting:
            NSLog(@"网络异常，正在重连...");
            [self updateStatus:@"重连中"];
            break;
            
        case V2TXLivePushStatusDisconnected:
            NSLog(@"推流连接断开");
            [self updateStatus:@"已断开"];
            [self stopPushTimer];
            break;
    }
}
```

## 5. 统计数据回调

### 📊 onStatisticsUpdate - 统计数据更新

```objc
- (void)onStatisticsUpdate:(V2TXLivePusherStatistics *)statistics;
```

**功能**: 推流器实时统计数据的回调通知

**参数说明**:
- `statistics`: 推流统计数据对象，包含详细的性能指标

**统计数据结构**:
```objc
@interface V2TXLivePusherStatistics : NSObject

/** 当前 App 的 CPU 使用率 (%) */
@property (nonatomic, assign) int appCpu;

/** 当前系统的 CPU 使用率 (%) */
@property (nonatomic, assign) int systemCpu;

/** 视频宽度 */
@property (nonatomic, assign) int width;

/** 视频高度 */
@property (nonatomic, assign) int height;

/** 帧率 (fps) */
@property (nonatomic, assign) int fps;

/** 视频码率 (kbps) */
@property (nonatomic, assign) int videoBitrate;

/** 音频码率 (kbps) */
@property (nonatomic, assign) int audioBitrate;

/** 网络延迟 (ms) */
@property (nonatomic, assign) int delay;

/** 网络抖动 (ms) */
@property (nonatomic, assign) int jitter;

/** 音频采样率 (Hz) */
@property (nonatomic, assign) int audioSampleRate;

/** 音频声道数 */
@property (nonatomic, assign) int audioChannels;

@end
```

**使用示例**:
```objc
- (void)onStatisticsUpdate:(V2TXLivePusherStatistics *)statistics {
    // 更新UI显示
    self.statsLabel.text = [NSString stringWithFormat:@"帧率:%dfps 码率:%dkbps 延迟:%dms", 
                           statistics.fps, statistics.videoBitrate, statistics.delay];
    
    // 性能监控
    if (statistics.appCpu > 80) {
        [self adjustPerformance];
    }
    
    // 网络质量监控
    if (statistics.delay > 1000) {
        [self adjustBitrateForNetwork];
    }
}
```

## 6. 音视频处理回调

### 🔊 onMicrophoneVolumeUpdate - 麦克风音量更新

```objc
- (void)onMicrophoneVolumeUpdate:(NSInteger)volume;
```

**功能**: 麦克风采集音量值的回调通知

**前提条件**: 需要调用 `enableVolumeEvaluation` 开启音量评估

**参数说明**:
- `volume`: 音量大小，范围通常为0-100

**使用场景**:
- 实时音量显示
- 静音检测
- 音频质量监控

**示例代码**:
```objc
- (void)onMicrophoneVolumeUpdate:(NSInteger)volume {
    // 更新音量条显示
    [self.volumeView setVolume:volume];
    
    // 静音检测
    if (volume < 5) {
        [self showMuteIndicator];
    } else {
        [self hideMuteIndicator];
    }
}
```

### 🎵 onProcessAudioFrame - 音频处理回调

```objc
- (void)onProcessAudioFrame:(V2TXLiveAudioFrame *)frame;
```

**功能**: 本地采集并经过音频模块前处理、音效处理和混BGM后的音频数据回调

**技术规格**:
- **时间帧长**: 固定0.02秒
- **数据格式**: PCM格式
- **字节计算**: `采样率 × 时间帧长 × 声道数 × 采样点位宽`

**默认配置示例**:
```
48000Hz × 0.02s × 1声道 × 16bit = 15360bit = 1920字节
```

**重要注意事项**:
1. **禁止耗时操作**: 回调函数中不要做任何耗时操作
2. **处理时间限制**: 处理时间必须小于20ms
3. **数据可读写**: 可以同步修改音频数据

**使用示例**:
```objc
- (void)onProcessAudioFrame:(V2TXLiveAudioFrame *)frame {
    // 实时音频处理示例
    
    // 1. 简单的音量增强
    [self enhanceAudioVolume:frame];
    
    // 2. 实时音频分析
    [self analyzeAudioSpectrum:frame];
    
    // 3. 自定义音效处理
    [self applyCustomAudioEffect:frame];
}

- (void)enhanceAudioVolume:(V2TXLiveAudioFrame *)frame {
    // 简单的音量增强算法
    int16_t *audioData = (int16_t *)frame.data;
    NSUInteger sampleCount = frame.data.length / sizeof(int16_t);
    
    for (NSUInteger i = 0; i < sampleCount; i++) {
        audioData[i] = (int16_t)(audioData[i] * 1.2); // 增加20%音量
    }
}
```

### 🎥 onProcessVideoFrame - 视频处理回调

```objc
- (void)onProcessVideoFrame:(V2TXLiveVideoFrame *_Nonnull)srcFrame dstFrame:(V2TXLiveVideoFrame *_Nonnull)dstFrame;
```

**功能**: 自定义视频处理回调，支持美颜、滤镜等视频特效

**前提条件**: 需要调用 `enableCustomVideoProcess` 开启自定义视频处理

**参数说明**:
- `srcFrame`: 原始视频帧（只读）
- `dstFrame`: 处理后的视频帧（可写）

**使用场景**:

#### 情况一：美颜组件产生新纹理
```objc
- (void)onProcessVideoFrame:(V2TXLiveVideoFrame *)srcFrame dstFrame:(V2TXLiveVideoFrame *)dstFrame {
    // 美颜处理，生成新纹理
    GLuint dstTextureId = [self.beautyProcessor processTexture:srcFrame.textureId 
                                                          width:srcFrame.width 
                                                         height:srcFrame.height];
    
    // 设置处理后的纹理
    dstFrame.textureId = dstTextureId;
}
```

#### 情况二：美颜组件不产生新纹理
```objc
- (void)onProcessVideoFrame:(V2TXLiveVideoFrame *)srcFrame dstFrame:(V2TXLiveVideoFrame *)dstFrame {
    // 第三方美颜处理，使用现有纹理
    [self.thirdPartyBeauty processInputTexture:srcFrame.textureId 
                                outputTexture:dstFrame.textureId 
                                        width:srcFrame.width 
                                       height:srcFrame.height];
}
```

### 🔧 onGLContextDestroyed - OpenGL环境销毁

```objc
- (void)onGLContextDestroyed;
```

**功能**: SDK内部OpenGL环境销毁的通知

**触发时机**:
- 应用进入后台
- 推流器被释放
- OpenGL上下文丢失

**处理建议**:
```objc
- (void)onGLContextDestroyed {
    NSLog(@"OpenGL环境已销毁");
    
    // 清理自定义的OpenGL资源
    [self cleanupGLResources];
    
    // 重新初始化OpenGL相关组件
    [self reinitializeGLComponents];
}
```

## 7. 屏幕分享回调

### 🖥️ onScreenCaptureStarted - 屏幕分享开始

```objc
- (void)onScreenCaptureStarted;
```

**功能**: 屏幕分享开始时的回调通知

**触发时机**: 屏幕分享成功启动

**使用场景**:
```objc
- (void)onScreenCaptureStarted {
    NSLog(@"屏幕分享已开始");
    
    // 更新UI状态
    [self updateScreenShareStatus:YES];
    
    // 显示屏幕分享提示
    [self showScreenShareIndicator];
}
```

### 🖥️ onScreenCaptureStopped - 屏幕分享停止

```objc
- (void)onScreenCaptureStopped:(int)reason;
```

**功能**: 屏幕分享停止时的回调通知

**参数说明**:
- `reason`: 停止原因
  - `0`: 用户主动停止
  - `1`: iOS-录屏被系统中断；Mac/Windows-屏幕分享窗口被关闭
  - `2`: Windows-显示屏状态变更；其他平台不抛出

**处理示例**:
```objc
- (void)onScreenCaptureStopped:(int)reason {
    NSLog(@"屏幕分享已停止，原因: %d", reason);
    
    switch (reason) {
        case 0: // 用户主动停止
            [self showToast:@"屏幕分享已结束"];
            break;
            
        case 1: // 系统中断
            [self showToast:@"屏幕分享被系统中断"];
            break;
            
        case 2: // 设备状态变更（仅Windows）
            [self showToast:@"显示设备状态变更"];
            break;
    }
    
    [self updateScreenShareStatus:NO];
}
```

## 8. 本地录制回调

### 📹 onLocalRecordBegin - 录制开始

```objc
- (void)onLocalRecordBegin:(NSInteger)errCode storagePath:(NSString *)storagePath;
```

**功能**: 录制任务开始的事件回调

**参数说明**:
- `errCode`: 状态码
  - `0`: 录制任务启动成功
  - `-1`: 内部错误导致录制失败
  - `-2`: 文件后缀名有误（不支持的录制格式）
  - `-6`: 录制已经启动，需要先停止录制
  - `-7`: 录制文件已存在，需要先删除文件
  - `-8`: 录制目录无写入权限
- `storagePath`: 录制的文件地址

**使用示例**:
```objc
- (void)onLocalRecordBegin:(NSInteger)errCode storagePath:(NSString *)storagePath {
    if (errCode == 0) {
        NSLog(@"本地录制开始成功，文件路径: %@", storagePath);
        [self updateRecordStatus:YES];
    } else {
        NSLog(@"本地录制开始失败，错误码: %ld", (long)errCode);
        [self handleRecordError:errCode];
    }
}
```

### 📹 onLocalRecording - 录制进行中

```objc
- (void)onLocalRecording:(NSInteger)durationMs storagePath:(NSString *)storagePath;
```

**功能**: 录制任务进行中的进展事件回调

**参数说明**:
- `durationMs`: 录制时长（毫秒）
- `storagePath`: 录制的文件地址

**配置说明**:
- 默认不抛出此回调
- 需要在 `startLocalRecording` 时设置回调间隔参数

**使用示例**:
```objc
- (void)onLocalRecording:(NSInteger)durationMs storagePath:(NSString *)storagePath {
    // 更新录制时长显示
    NSInteger seconds = durationMs / 1000;
    self.recordTimeLabel.text = [NSString stringWithFormat:@"录制中: %02ld:%02ld", 
                                seconds / 60, seconds % 60];
    
    // 录制进度监控
    if (seconds > 3600) { // 超过1小时
        [self showLongRecordingWarning];
    }
}
```

### 📹 onLocalRecordComplete - 录制完成

```objc
- (void)onLocalRecordComplete:(NSInteger)errCode storagePath:(NSString *)storagePath;
```

**功能**: 录制任务结束的事件回调

**参数说明**:
- `errCode`: 状态码
  - `0`: 结束录制任务成功
  - `-1`: 录制失败
  - `-2`: 切换分辨率或横竖屏导致录制结束
  - `-3`: 录制时间太短，或未采集到音视频数据
- `storagePath`: 录制的文件地址

**处理示例**:
```objc
- (void)onLocalRecordComplete:(NSInteger)errCode storagePath:(NSString *)storagePath {
    if (errCode == 0) {
        NSLog(@"本地录制完成，文件路径: %@", storagePath);
        [self showRecordSuccessAlert:storagePath];
    } else {
        NSLog(@"本地录制失败，错误码: %ld", (long)errCode);
        [self handleRecordCompleteError:errCode];
    }
    
    [self updateRecordStatus:NO];
}
```

## 9. 高级功能回调

### 🌐 onSetMixTranscodingConfig - 云端混流配置

```objc
- (void)onSetMixTranscodingConfig:(V2TXLiveCode)code message:(NSString *)msg;
```

**功能**: 设置云端混流转码参数的回调

**参数说明**:
- `code`: 操作结果码
- `msg`: 具体错误原因

**使用示例**:
```objc
- (void)onSetMixTranscodingConfig:(V2TXLiveCode)code message:(NSString *)msg {
    if (code == V2TXLIVE_OK) {
        NSLog(@"云端混流配置成功");
    } else {
        NSLog(@"云端混流配置失败: %@", msg);
        [self retryMixTranscodingConfig];
    }
}
```

### 📸 onSnapshotComplete - 截图完成

```objc
- (void)onSnapshotComplete:(nullable TXImage *)image;
```

**功能**: 截图操作完成后的回调通知

**前提条件**: 调用 `snapshot` 方法后触发

**参数说明**:
- `image`: 截取的视频画面图片（可能为nil）

**使用示例**:
```objc
- (void)onSnapshotComplete:(TXImage *)image {
    if (image) {
        // 保存截图到相册
        UIImageWriteToSavedPhotosAlbum(image, nil, nil, nil);
        
        // 显示截图预览
        [self showSnapshotPreview:image];
    } else {
        NSLog(@"截图失败");
    }
}
```

### 🎙️ onVoiceActivityDetectionUpdate - 人声检测更新

```objc
- (void)onVoiceActivityDetectionUpdate:(BOOL)active;
```

**功能**: 人声检测状态更新的回调通知

**前提条件**: 调用 `enableVoiceActivityDetection` 开启人声检测

**参数说明**:
- `active`: 人声活动状态（YES-开始说话，NO-停止说话）

**使用场景**:
```objc
- (void)onVoiceActivityDetectionUpdate:(BOOL)active {
    if (active) {
        NSLog(@"检测到主播开始说话");
        [self showSpeakingIndicator];
    } else {
        NSLog(@"检测到主播停止说话");
        [self hideSpeakingIndicator];
    }
}
```

## 10. 使用示例

### 🔧 完整的推流器回调实现

```objc
#import "V2TXLivePusherObserver.h"

@interface MyPusherObserver () <V2TXLivePusherObserver>
@end

@implementation MyPusherObserver

#pragma mark - 错误和警告处理

- (void)onError:(V2TXLiveCode)code message:(NSString *)msg extraInfo:(NSDictionary *)extraInfo {
    NSLog(@"推流错误: %ld - %@", (long)code, msg);
    
    // 根据错误码进行相应处理
    [self handlePushError:code message:msg];
}

- (void)onWarning:(V2TXLiveCode)code message:(NSString *)msg extraInfo:(NSDictionary *)extraInfo {
    NSLog(@"推流警告: %ld - %@", (long)code, msg);
    
    // 警告信息提示用户
    [self showWarningToast:msg];
}

#pragma mark - 推流状态监控

- (void)onPushStatusUpdate:(V2TXLivePushStatus)status message:(NSString *)msg extraInfo:(NSDictionary *)extraInfo {
    // 更新UI状态
    [self updatePushStatus:status];
    
    // 记录推流日志
    [self logPushStatus:status message:msg];
}

- (void)onStatisticsUpdate:(V2TXLivePusherStatistics *)statistics {
    // 实时更新统计数据
    [self updateStatsDisplay:statistics];
    
    // 性能监控和自动调整
    [self autoAdjustBasedOnStats:statistics];
}

#pragma mark - 音视频处理

- (void)onProcessAudioFrame:(V2TXLiveAudioFrame *)frame {
    // 实时音频处理
    [self.audioProcessor processFrame:frame];
}

- (void)onProcessVideoFrame:(V2TXLiveVideoFrame *)srcFrame dstFrame:(V2TXLiveVideoFrame *)dstFrame {
    // 实时视频美颜处理
    [self.beautyProcessor processFrame:srcFrame to:dstFrame];
}

#pragma mark - 录制功能

- (void)onLocalRecordBegin:(NSInteger)errCode storagePath:(NSString *)storagePath {
    if (errCode == 0) {
        self.currentRecordPath = storagePath;
        [self startRecordTimer];
    }
}

- (void)onLocalRecording:(NSInteger)durationMs storagePath:(NSString *)storagePath {
    [self updateRecordTime:durationMs];
}

- (void)onLocalRecordComplete:(NSInteger)errCode storagePath:(NSString *)storagePath {
    [self stopRecordTimer];
    [self handleRecordCompletion:errCode path:storagePath];
}

@end
```

### 🎯 最佳实践建议

**1. 线程安全处理**
```objc
- (void)onStatisticsUpdate:(V2TXLivePusherStatistics *)statistics {
    // 确保UI更新在主线程执行
    dispatch_async(dispatch_get_main_queue(), ^{
        [self updateStatsUI:statistics];
    });
}
```

**2. 性能优化**
```objc
- (void)onProcessAudioFrame:(V2TXLiveAudioFrame *)frame {
    // 避免在回调中进行复杂计算
    @autoreleasepool {
        [self.lightweightProcessor process:frame];
    }
}
```

**3. 错误恢复机制**
```objc
- (void)onError:(V2TXLiveCode)code message:(NSString *)msg extraInfo:(NSDictionary *)extraInfo {
    if ([self isRecoverableError:code]) {
        [self scheduleReconnect];
    }
}
```

## 11. 回调时序图

### 📊 推流生命周期回调时序

```
开始推流流程:
1. onPushStatusUpdate(V2TXLivePushStatusConnecting)
2. onCaptureFirstVideoFrame (如果开启视频)
3. onCaptureFirstAudioFrame (如果开启音频)
4. onPushStatusUpdate(V2TXLivePushStatusConnectSuccess)
5. onStatisticsUpdate (周期性回调)

停止推流流程:
1. onPushStatusUpdate(V2TXLivePushStatusDisconnected)
2. onGLContextDestroyed (如果使用OpenGL)
```

### 🔄 状态流转图

```
初始化 → 连接中 → 连接成功 → 推流中
                ↓
            重连中 → 连接成功
                ↓
            断开连接
```
