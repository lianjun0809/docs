> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

# 腾讯云直播SDK V2TXLiveDef 类型定义文档

## 概述

`V2TXLiveDef.h` 是腾讯云直播SDK iOS/macOS平台的核心类型定义文件，包含了直播推流和播放相关的所有枚举、常量和数据结构定义。

**平台支持**: iOS, macOS  
**类型总数**: 包含视频、音频、统计、配置等各类定义

## 📋 目录结构

### 1. [支持协议](#支持协议)
### 2. [视频相关类型](#视频相关类型)
### 3. [音频相关类型](#音频相关类型)
### 4. [统计指标数据](#统计指标数据)
### 5. [连接状态相关](#连接状态相关)
### 6. [云端混流配置](#云端混流配置)
### 7. [本地录制配置](#本地录制配置)
### 8. [日志配置](#日志配置)
### 9. [其他配置](#其他配置)

## 1. 支持协议

### V2TXLiveMode - 直播 SDK 推流支持的协议类型
```objc
typedef NS_ENUM(NSUInteger, V2TXLiveMode) {
    /// 支持协议: RTMP
    V2TXLiveMode_RTMP,
    
    /// 支持协议: RTC
    V2TXLiveMode_RTC
};
```

**协议说明**:
- RTMP: 标准直播协议
- RTC: 实时音视频协议

## 2. 视频相关类型

### V2TXLiveVideoResolution - 视频分辨率枚举，定义了各种标准分辨率
```objc
typedef NS_ENUM(NSInteger, V2TXLiveVideoResolution) {
    /// 分辨率 160*160，码率范围：100Kbps ~ 150Kbps，帧率：15fps。
    V2TXLiveVideoResolution160x160,
    
    /// 分辨率 270*270，码率范围：200Kbps ~ 300Kbps，帧率：15fps。
    V2TXLiveVideoResolution270x270,

    /// 分辨率 480*480，码率范围：350Kbps ~ 525Kbps，帧率：15fps。
    V2TXLiveVideoResolution480x480,

    /// 分辨率 320*240，码率范围：250Kbps ~ 375Kbps，帧率：15fps。
    V2TXLiveVideoResolution320x240,

    /// 分辨率 480*360，码率范围：400Kbps ~ 600Kbps，帧率：15fps。
    V2TXLiveVideoResolution480x360,

    /// 分辨率 640*480，码率范围：600Kbps ~ 900Kbps，帧率：15fps。
    V2TXLiveVideoResolution640x480,

    /// 分辨率 320*180，码率范围：250Kbps ~ 400Kbps，帧率：15fps。
    V2TXLiveVideoResolution320x180,

    /// 分辨率 480*270，码率范围：350Kbps ~ 550Kbps，帧率：15fps。
    V2TXLiveVideoResolution480x270,

    /// 分辨率 640*360，码率范围：500Kbps ~ 900Kbps，帧率：15fps。
    V2TXLiveVideoResolution640x360,

    /// 分辨率 960*540，码率范围：800Kbps ~ 1500Kbps，帧率：15fps。
    V2TXLiveVideoResolution960x540,

    /// 分辨率 1280*720，码率范围：1000Kbps ~ 1800Kbps，帧率：15fps。
    V2TXLiveVideoResolution1280x720,

    /// 分辨率 1920*1080，码率范围：2500Kbps ~ 3000Kbps，帧率：15fps。
    V2TXLiveVideoResolution1920x1080
};
```

### V2TXLiveVideoResolutionMode - 视频分辨率模式
```objc
typedef NS_ENUM(NSInteger, V2TXLiveVideoResolutionMode) {
    /// 横屏模式
    V2TXLiveVideoResolutionModeLandscape,
    
    /// 竖屏模式
    V2TXLiveVideoResolutionModePortrait
};
```

**分辨率说明**:
- 支持从160×160到1920×1080的多种分辨率
- 支持横屏和竖屏两种模式

### V2TXLiveMirrorType - 本地摄像头镜像类型
```objc
typedef NS_ENUM(NSInteger, V2TXLiveMirrorType) {
    /// 系统默认镜像类型，前置摄像头镜像，后置摄像头不镜像
    V2TXLiveMirrorTypeAuto,
    
    /// 前置摄像头和后置摄像头都切换为镜像模式
    V2TXLiveMirrorTypeEnable,
    
    /// 前置摄像头和后置摄像头都切换为非镜像模式
    V2TXLiveMirrorTypeDisable
};
```

### V2TXLiveFillMode - 视频画面填充模式
```objc
typedef NS_ENUM(NSInteger, V2TXLiveFillMode) {
    /// 图像铺满屏幕，超出部分将被裁剪，画面可能不完整
    V2TXLiveFillModeFill,
    
    /// 图像长边填满屏幕，短边区域填充黑色，画面内容完整
    V2TXLiveFillModeFit,
    
    /// 图像拉伸铺满，长度和宽度可能不会按比例变化
    V2TXLiveFillModeScaleFill
};
```

### V2TXLiveRotation - 视频画面旋转角度
```objc
typedef NS_ENUM(NSInteger, V2TXLiveRotation) {
    /// 不旋转
    V2TXLiveRotation0,
    
    /// 顺时针旋转90度
    V2TXLiveRotation90,
    
    /// 顺时针旋转180度
    V2TXLiveRotation180,
    
    /// 顺时针旋转270度
    V2TXLiveRotation270
};
```

### V2TXLiveVideoEncoderParam - 视频编码参数配置类
```objc
@interface V2TXLiveVideoEncoderParam : NSObject

@property(nonatomic, assign) V2TXLiveVideoResolution videoResolution;      // 视频分辨率
@property(nonatomic, assign) V2TXLiveVideoResolutionMode videoResolutionMode; // 分辨率模式
@property(nonatomic, assign) int videoFps;                                // 视频采集帧率（fps）
@property(nonatomic, assign) int videoBitrate;                             // 目标视频码率（kbps）
@property(nonatomic, assign) int minVideoBitrate;                          // 最低视频码率（kbps）

- (instancetype)initWith:(V2TXLiveVideoResolution)resolution;          // 初始化方法

@end
```

**推荐配置**:
- **帧率**: 15fps或20fps（5fps以下卡顿明显，20fps以上浪费带宽）
- **码率自适应**: 通过同时设置videoBitrate和minVideoBitrate来约束码率调整范围

### V2TXLivePixelFormat - 视频帧像素格式
```objc
typedef NS_ENUM(NSInteger, V2TXLivePixelFormat) {
    /// 未知像素格式
    V2TXLivePixelFormatUnknown,
    
    /// I420格式（YUV420P）
    V2TXLivePixelFormatI420,
    
    /// NV12格式
    V2TXLivePixelFormatNV12,
    
    /// BGRA32格式
    V2TXLivePixelFormatBGRA32,
    
    /// OpenGL 2D纹理格式
    V2TXLivePixelFormatTexture2D
};
```

### V2TXLiveBufferType - 视频数据包装格式
```objc
typedef NS_ENUM(NSInteger, V2TXLiveBufferType) {
    /// 未知数据包装格式
    V2TXLiveBufferTypeUnknown,
    
    /// PixelBuffer格式，iOS平台原生视频数据格式
    V2TXLiveBufferTypePixelBuffer,
    
    /// NSData格式，装载I420等buffer数据
    V2TXLiveBufferTypeNSData,
    
    /// OpenGL纹理格式，性能最好，画质损失最少
    V2TXLiveBufferTypeTexture
};
```

### V2TXLiveVideoFrame - 视频帧信息类
```objc
@interface V2TXLiveVideoFrame : NSObject

@property(nonatomic, assign) V2TXLivePixelFormat pixelFormat;  // 视频帧像素格式
@property(nonatomic, assign) V2TXLiveBufferType bufferType;   // 视频数据包装格式
@property(nonatomic, strong) NSData *data;                    // 视频数据
@property(nonatomic, assign) CVPixelBufferRef pixelBuffer;    // 视频数据PixelBuffer
@property(nonatomic, assign) NSUInteger width;                // 视频宽度
@property(nonatomic, assign) NSUInteger height;               // 视频高度
@property(nonatomic, assign) V2TXLiveRotation rotation;       // 视频帧旋转角度
@property(nonatomic, assign) GLuint textureId;                // 视频纹理ID

@end
```
### 🖼️ 画中画状态

### V2TXLivePictureInPictureState - 画中画状态枚举
```objc
typedef NS_ENUM(NSInteger, V2TXLivePictureInPictureState) {
    /// 画中画状态未定义
    V2TXLivePictureInPictureStateUndefined,
    
    /// 画中画发生错误
    V2TXLivePictureInPictureStateOccurError,
    
    /// 画中画将要开始
    V2TXLivePictureInPictureStateWillStart,
    
    /// 画中画已经开始
    V2TXLivePictureInPictureStateDidStart,
    
    /// 画中画将要停止
    V2TXLivePictureInPictureStateWillStop,
    
    /// 画中画已经停止
    V2TXLivePictureInPictureStateDidStop,
    
    /// 画中画恢复用户界面
    V2TXLivePictureInPictureStateRestoreUI
};
```
## 3. 音频相关类型

### V2TXLiveAudioQuality - 声音音质配置
```objc
typedef NS_ENUM(NSInteger, V2TXLiveAudioQuality) {
    /// 语音音质：16k采样率，单声道，16kbps码率，适合语音通话
    V2TXLiveAudioQualitySpeech,
    
    /// 默认音质：48k采样率，单声道，50kbps码率，SDK默认配置
    V2TXLiveAudioQualityDefault,
    
    /// 音乐音质：48k采样率，双声道+全频带，128kbps码率，适合高保真音乐场景
    V2TXLiveAudioQualityMusic
};
```

### V2TXLiveAudioFrame - 音频帧数据类
```objc
@interface V2TXLiveAudioFrame : NSObject

@property(nonatomic, strong) NSData *data;        // 音频数据
@property(nonatomic, assign) int sampleRate;      // 采样率（默认48000Hz）
@property(nonatomic, assign) int channel;         // 声道数（默认1，单声道）
@property(nonatomic, assign) uint64_t timestamp;  // 时间戳，单位ms

@end
```

### V2TXLiveAudioFrameOperationMode - 音频回调数据读写模式
```objc
typedef NS_ENUM(NSInteger, V2TXLiveAudioFrameOperationMode) {
    /// 读写模式：可以获取并修改回调的音频数据（默认模式）
    V2TXLiveAudioFrameOperationModeReadWrite,
    
    /// 只读模式：仅从回调中获取音频数据
    V2TXLiveAudioFrameOperationModeReadOnly
};
```

### V2TXLiveAudioFrameObserverFormat - 音频帧回调格式配置
```objc
@interface V2TXLiveAudioFrameObserverFormat : NSObject

@property(nonatomic, assign) int sampleRate;                      // 采样率（默认48000Hz）
@property(nonatomic, assign) int channel;                        // 声道数（默认1）
@property(nonatomic, assign) int samplesPerCall;                 // 采样点数
@property(nonatomic, assign) V2TXLiveAudioFrameOperationMode mode; // 回调数据读写模式

@end
```

**参数说明**:
- **samplesPerCall**: 必须是sampleRate/100的整数倍

## 4. 统计指标数据

### V2TXLivePusherStatistics - 推流器统计数据类
```objc
@interface V2TXLivePusherStatistics : NSObject

@property(nonatomic, assign) NSUInteger appCpu;              // 当前App的CPU使用率（%）
@property(nonatomic, assign) NSUInteger systemCpu;           // 当前系统的CPU使用率（%）
@property(nonatomic, assign) NSUInteger width;              // 视频宽度
@property(nonatomic, assign) NSUInteger height;             // 视频高度
@property(nonatomic, assign) NSUInteger fps;                // 帧率（fps）
@property(nonatomic, assign) NSUInteger videoBitrate;       // 视频码率（Kbps）
@property(nonatomic, assign) NSUInteger audioBitrate;       // 音频码率（Kbps）
@property(nonatomic, assign) NSUInteger rtt;                // 往返延时（ms）
@property(nonatomic, assign) NSUInteger netSpeed;          // 上行速度（kbps）

@end
```

### V2TXLivePlayerStatistics - 播放器统计数据类
```objc
@interface V2TXLivePlayerStatistics : NSObject

@property(nonatomic, assign) NSUInteger appCpu;              // 当前App的CPU使用率（%）
@property(nonatomic, assign) NSUInteger systemCpu;           // 当前系统的CPU使用率（%）
@property(nonatomic, assign) NSUInteger width;              // 视频宽度
@property(nonatomic, assign) NSUInteger height;             // 视频高度
@property(nonatomic, assign) NSUInteger fps;                // 帧率（fps）
@property(nonatomic, assign) NSUInteger videoBitrate;       // 视频码率（Kbps）
@property(nonatomic, assign) NSUInteger audioBitrate;       // 音频码率（Kbps）
@property(nonatomic, assign) NSUInteger audioPacketLoss;   // 网络音频丢包率（%）
@property(nonatomic, assign) NSUInteger videoPacketLoss;   // 网络视频丢包率（%）
@property(nonatomic, assign) NSUInteger jitterBufferDelay;  // 播放延迟（ms）
@property(nonatomic, assign) NSUInteger audioTotalBlockTime; // 音频播放累计卡顿时长（ms）
@property(nonatomic, assign) NSUInteger audioBlockRate;     // 音频播放卡顿率（%）
@property(nonatomic, assign) NSUInteger videoTotalBlockTime; // 视频播放累计卡顿时长（ms）
@property(nonatomic, assign) NSUInteger videoBlockRate;     // 视频播放卡顿率（%）
@property(nonatomic, assign) NSUInteger rtt;                // 往返延时（ms）
@property(nonatomic, assign) NSUInteger netSpeed;          // 下载速度（kbps）

@end
```

## 5. 连接状态相关

### V2TXLivePushStatus - 推流连接状态
```objc
typedef NS_ENUM(NSInteger, V2TXLivePushStatus) {
    /// 与服务器断开连接
    V2TXLivePushStatusDisconnected,
    
    /// 正在连接服务器
    V2TXLivePushStatusConnecting,
    
    /// 连接服务器成功
    V2TXLivePushStatusConnectSuccess,
    
    /// 重连服务器中
    V2TXLivePushStatusReconnecting
};
```

### V2TXAudioRoute - 音频路由模式
```objc
typedef NS_ENUM(NSInteger, V2TXAudioRoute) {
    /// 扬声器模式，声音从手机扬声器播放
    V2TXAudioRouteSpeakerphone,
    
    /// 听筒模式，声音从手机听筒播放
    V2TXAudioRouteEarpiece
};
```

## 6. 云端混流配置

### V2TXLiveMixInputType - 混流输入类型
```objc
typedef NS_ENUM(NSInteger, V2TXLiveMixInputType) {
    /// 混入音视频
    V2TXLiveMixInputTypeAudioVideo,
    
    /// 只混入视频
    V2TXLiveMixInputTypePureVideo,
    
    /// 只混入音频
    V2TXLiveMixInputTypePureAudio
};
```

### V2TXLiveMixStream - 云端混流子画面位置信息
```objc
@interface V2TXLiveMixStream : NSObject

@property(nonatomic, copy) NSString *userId;          // 参与混流的userId
@property(nonatomic, copy) NSString *streamId;        // 推流streamId
@property(nonatomic, assign) NSInteger x;             // 图层位置x坐标（绝对像素值）
@property(nonatomic, assign) NSInteger y;             // 图层位置y坐标（绝对像素值）
@property(nonatomic, assign) NSInteger width;         // 图层宽度（绝对像素值）
@property(nonatomic, assign) NSInteger height;        // 图层高度（绝对像素值）
@property(nonatomic, assign) NSUInteger zOrder;       // 图层层次（1-15，不可重复）
@property(nonatomic, assign) V2TXLiveMixInputType inputType; // 直播流输入类型

@end
```

### V2TXLiveTranscodingConfig - 云端混流转码配置
```objc
@interface V2TXLiveTranscodingConfig : NSObject

@property(nonatomic, assign) NSUInteger videoWidth;      // 最终转码后的视频宽度
@property(nonatomic, assign) NSUInteger videoHeight;     // 最终转码后的视频高度
@property(nonatomic, assign) NSUInteger videoBitrate;   // 最终转码后的视频码率（kbps）
@property(nonatomic, assign) NSUInteger videoFramerate;  // 最终转码后的视频帧率（FPS）
@property(nonatomic, assign) NSUInteger videoGOP;        // 关键帧间隔（秒）
@property(nonatomic, assign) NSUInteger backgroundColor; // 混合后画面的底色颜色
@property(nonatomic, copy) NSString *backgroundImage;    // 混合后画面的背景图
@property(nonatomic, assign) NSUInteger audioSampleRate; // 最终转码后的音频采样率
@property(nonatomic, assign) NSUInteger audioBitrate;   // 最终转码后的音频码率（kbps）
@property(nonatomic, assign) NSUInteger audioChannels;   // 最终转码后的音频声道数
@property(nonatomic, copy) NSArray<V2TXLiveMixStream *> *mixStreams; // 子画面位置信息
@property(nonatomic, copy) NSString *outputStreamId;     // 输出到CDN的直播流ID

@end
```

## 7. 本地录制配置

### V2TXLiveRecordMode - 本地音视频录制模式
```objc
typedef NS_ENUM(NSUInteger, V2TXLiveRecordMode) {
    /// 录制音频和视频
    V2TXLiveRecordModeBoth
};
```

### V2TXLiveLocalRecordingParams - 本地录制配置参数
```objc
@interface V2TXLiveLocalRecordingParams : NSObject

@property(nonatomic, copy) NSString *filePath;      // 录制文件路径（必填，需包含文件名和格式后缀）
@property(nonatomic, assign) V2TXLiveRecordMode recordMode; // 媒体录制模式
@property(nonatomic, assign) int interval;          // 录制信息更新频率（毫秒）

@end
```

**参数说明**:
- **filePath**: 必须精确到文件名和格式后缀（目前只支持MP4）
- **interval**: 范围1000-10000ms，-1表示不回调录制信息

## 8. 日志配置

### V2TXLiveLogLevel - 日志级别
```objc
typedef NS_ENUM(NSInteger, V2TXLiveLogLevel) {
    V2TXLiveLogLevelAll,        // 输出所有级别
    V2TXLiveLogLevelDebug,      // 输出DEBUG及以上
    V2TXLiveLogLevelInfo,       // 输出INFO及以上
    V2TXLiveLogLevelWarning,    // 输出WARNING及以上
    V2TXLiveLogLevelError,      // 输出ERROR及以上
    V2TXLiveLogLevelFatal,      // 只输出FATAL
    V2TXLiveLogLevelNULL        // 不输出任何log
};
```

### V2TXLiveLogConfig - 日志配置类
```objc
@interface V2TXLiveLogConfig : NSObject

@property(nonatomic, assign) V2TXLiveLogLevel logLevel;      // 设置Log级别
@property(nonatomic, assign) BOOL enableObserver;           // 是否通过Observer接收Log信息
@property(nonatomic, assign) BOOL enableConsole;            // 是否在编辑器控制台打印Log
@property(nonatomic, assign) BOOL enableLogFile;            // 是否启用本地Log文件
@property(nonatomic, copy) NSString *logPath;               // 本地Log存储目录

@end
```

**默认存储位置**: iOS/macOS默认存储在Documents/log目录

**字段说明**:
- **logLevel**: 设置Log级别，控制SDK输出日志的详细程度
- **enableObserver**: 是否通过Observer接收Log信息，用于自定义日志处理
- **enableConsole**: 是否在编辑器控制台打印Log，便于调试
- **enableLogFile**: 是否启用本地Log文件，用于问题排查
- **logPath**: 本地Log存储目录，如不设置则使用默认路径

## 9. 其他配置

### V2TXLiveSocks5ProxyConfig - Socks5代理协议配置
```objc
@interface V2TXLiveSocks5ProxyConfig : NSObject

@property(nonatomic, assign) BOOL supportHttps;    // 是否支持HTTPS
@property(nonatomic, assign) BOOL supportTcp;      // 是否支持TCP
@property(nonatomic, assign) BOOL supportUdp;      // 是否支持UDP

@end
```

### V2TXLiveStreamInfo - 自适应切换的码流信息
```objc
@interface V2TXLiveStreamInfo : NSObject

@property(nonatomic, assign) int width;             // 视频宽度
@property(nonatomic, assign) int height;           // 视频高度
@property(nonatomic, assign) int bitrate;          // 码率（bps）
@property(nonatomic, assign) float framerate;      // 帧率
@property(nonatomic, copy) NSString *url;          // 流地址

@end
```
