> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

# 腾讯云直播SDK V2TXLiveDef 类型定义文档

## 概述

`V2TXLiveDef` 是腾讯云直播SDK的核心类型定义文件，包含了直播推流和播放相关的所有枚举、常量和数据结构定义。

**文件路径**: `com/tencent/live2/V2TXLiveDef.java`

**主要功能**:
- 定义视频、音频相关的枚举类型和常量
- 提供统计数据和配置参数的数据结构
- 支持云端混流和本地录制的配置定义

## 一、支持协议

### V2TXLiveMode - 直播 SDK 推流支持的协议类型
```java
public enum V2TXLiveMode {
    /// 支持协议: RTMP
    TXLiveMode_RTMP,
    
    /// 支持协议: RTC
    TXLiveMode_RTC;
}
```

## 二、视频相关类型定义

### V2TXLiveVideoResolution - 视频分辨率枚举，定义了各种标准分辨率
```java
public enum V2TXLiveVideoResolution {
    /// 分辨率 160*160，码率范围：100Kbps ~ 150Kbps，帧率：15fps。
    V2TXLiveVideoResolution160x160,
    
    /// 分辨率 270*270，码率范围：200Kbps ~ 300Kbps，帧率：15fps。
    V2TXLiveVideoResolution270x270,

    /// 分辨率 480*480，码率范围：350Kbps ~ 525Kbps，帧率：15fps。
    V2TXLiveVideoResolution480x480,

    /// 分辨率 320*240，码率范围：250Kbps ~ 375Kbps，帧率：15fps。
    V2TXLiveVideoResolution320x240,

    ///  分辨率 480*360，码率范围：400Kbps ~ 600Kbps，帧率：15fps。
    V2TXLiveVideoResolution480x360,

    ///  分辨率 640*480，码率范围：600Kbps ~ 900Kbps，帧率：15fps。
    V2TXLiveVideoResolution640x480,

    /// 分辨率 320*180，码率范围：250Kbps ~ 400Kbps，帧率：15fps。
    V2TXLiveVideoResolution320x180,

    ///  分辨率 480*270，码率范围：350Kbps ~ 550Kbps，帧率：15fps。
    V2TXLiveVideoResolution480x270,

    /// 分辨率 640*360，码率范围：500Kbps ~ 900Kbps，帧率：15fps。
    V2TXLiveVideoResolution640x360,

    ///  分辨率 960*540，码率范围：800Kbps ~ 1500Kbps，帧率：15fps。
    V2TXLiveVideoResolution960x540,

    ///  分辨率 1280*720，码率范围：1000Kbps ~ 1800Kbps，帧率：15fps。
    V2TXLiveVideoResolution1280x720,

    ///  分辨率 1920*1080，码率范围：2500Kbps ~ 3000Kbps，帧率：15fps。
    V2TXLiveVideoResolution1920x1080,
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

### V2TXLiveVideoResolutionMode - 视频横竖屏模式
```java
public enum V2TXLiveVideoResolutionMode {
    /// 横屏模式
    V2TXLiveVideoResolutionModeLandscape,
    
    /// 竖屏模式
    V2TXLiveVideoResolutionModePortrait,
}
```


### V2TXLiveVideoEncoderParam - 视频编码参数配置类
```java
public final static class V2TXLiveVideoEncoderParam {
    public V2TXLiveVideoResolution videoResolution;      // 视频分辨率
    public V2TXLiveVideoResolutionMode videoResolutionMode; // 分辨率模式
    public int videoFps;                                 // 视频采集帧率
    public int videoBitrate;                             // 目标视频码率
    public int minVideoBitrate;                          // 最低视频码率
}
```

**推荐配置**:
- **帧率**: 15fps或20fps（5fps以下卡顿明显，20fps以上浪费带宽）
- **码率自适应**: 通过同时设置videoBitrate和minVideoBitrate来约束码率调整范围

### V2TXLiveMirrorType - 本地摄像头镜像类型
```java
public enum V2TXLiveMirrorType {
    /// 系统默认镜像类型，前置摄像头镜像，后置摄像头不镜像
    V2TXLiveMirrorTypeAuto,
    
    /// 前置摄像头和后置摄像头都切换为镜像模式
    V2TXLiveMirrorTypeEnable,
    
    /// 前置摄像头和后置摄像头都切换为非镜像模式
    V2TXLiveMirrorTypeDisable,
}
```

### V2TXLiveFillMode - 视频画面填充模式
```java
public enum V2TXLiveFillMode {
    /// 图像铺满屏幕，超出部分将被裁剪，画面可能不完整
    V2TXLiveFillModeFill,
    
    /// 图像长边填满屏幕，短边填充黑色，画面内容完整
    V2TXLiveFillModeFit,
    
    /// 图像拉伸铺满，长度和宽度可能不会按比例变化
    V2TXLiveFillModeScaleFill
}
```

### V2TXLiveRotation - 视频画面旋转角度
```java
public enum V2TXLiveRotation {
    /// 不旋转
    V2TXLiveRotation0,
    
    /// 顺时针旋转90度
    V2TXLiveRotation90,
    
    /// 顺时针旋转180度
    V2TXLiveRotation180,
    
    /// 顺时针旋转270度
    V2TXLiveRotation270,
}
```

### V2TXLivePixelFormat - 视频帧像素格式
```java
public enum V2TXLivePixelFormat {
    /// 未知
    V2TXLivePixelFormatUnknown,
    
    /// YUV420P I420格式
    V2TXLivePixelFormatI420,
    
    /// OpenGL 2D纹理格式
    V2TXLivePixelFormatTexture2D,
}
```

### V2TXLiveBufferType - 视频数据包装格式
```java
public enum V2TXLiveBufferType {
    /// 未知
    V2TXLiveBufferTypeUnknown,
    
    /// DirectBuffer，装载I420等buffer，在native层使用
    V2TXLiveBufferTypeByteBuffer,
    
    /// byte[]，装载I420等buffer，在Java层使用
    V2TXLiveBufferTypeByteArray,
    
    /// 直接操作纹理ID，性能最好，画质损失最少
    V2TXLiveBufferTypeTexture,
}
```

### V2TXLiveTexture - 视频纹理包装类

```java
public final static class V2TXLiveTexture {
    public int textureId;                                // 视频纹理ID
    public javax.microedition.khronos.egl.EGLContext eglContext10; // OpenGL接口定义
    public android.opengl.EGLContext eglContext14;        // Android OpenGL接口定义
}
```

### V2TXLiveVideoFrame - 视频帧信息类

```java
public final static class V2TXLiveVideoFrame {
    public V2TXLivePixelFormat pixelFormat;              // 视频帧像素格式
    public V2TXLiveBufferType bufferType;                // 视频数据包装格式
    public V2TXLiveTexture texture;                       // 视频纹理包装类
    public byte[] data;                                  // 视频数据
    public ByteBuffer buffer;                            // 视频数据Buffer
    public int width;                                    // 视频宽度
    public int height;                                   // 视频高度
    public int rotation;                                 // 视频帧旋转角度
}
```

## 三、音频相关类型定义

### V2TXLiveAudioQuality - 声音音质配置
```java
public enum V2TXLiveAudioQuality {
    /// 语音音质：16k采样率，单声道，16kbps码率，适合语音通话
    V2TXLiveAudioQualitySpeech,
    
    /// 默认音质：48k采样率，单声道，50kbps码率，SDK默认配置
    V2TXLiveAudioQualityDefault,
    
    /// 音乐音质：48k采样率，双声道+全频带，128kbps码率，适合高保真音乐场景
    V2TXLiveAudioQualityMusic,
}
```

### V2TXLiveAudioFrame - 音频帧数据类
```java
public final static class V2TXLiveAudioFrame {
    public byte[] data;          // 音频数据
    public int sampleRate;       // 采样率（默认48000Hz）
    public int channel;          // 声道数（默认1，单声道）
    public long timestamp;      // 时间戳，单位ms
}
```

### V2TXLiveAudioFrameOperationMode - 音频回调数据读写模式
```java
public enum V2TXLiveAudioFrameOperationMode {
    /// 读写模式：可以获取并修改回调的音频数据（默认模式）
    V2TXLiveAudioFrameOperationModeReadWrite,
    
    /// 只读模式：仅从回调中获取音频数据
    V2TXLiveAudioFrameOperationModeReadOnly,
}
```

### V2TXLiveAudioFrameObserverFormat - 音频帧回调格式配置
```java
public final static class V2TXLiveAudioFrameObserverFormat {
    public int sampleRate;                               // 采样率（默认48000Hz）
    public int channel;                                  // 声道数（默认1）
    public int samplesPerCall;                           // 采样点数
    public V2TXLiveAudioFrameOperationMode mode;         // 回调数据读写模式
}
```

## 四、统计指标数据定义

### V2TXLivePusherStatistics - 推流器统计数据类
```java
public final static class V2TXLivePusherStatistics {
    public int appCpu;           // 当前App的CPU使用率（%）
    public int systemCpu;        // 当前系统的CPU使用率（%）
    public int width;            // 视频宽度
    public int height;           // 视频高度
    public int fps;              // 帧率（fps）
    public int videoBitrate;      // 视频码率（Kbps）
    public int audioBitrate;      // 音频码率（Kbps）
    public int rtt;              // SDK到云端的往返延时（ms）
    public int netSpeed;          // 上行速度（kbps）
}
```

### V2TXLivePlayerStatistics - 播放器统计数据类
```java
public final static class V2TXLivePlayerStatistics {
    public int appCpu;                   // 当前App的CPU使用率（%）
    public int systemCpu;                // 当前系统的CPU使用率（%）
    public int width;                    // 视频宽度
    public int height;                   // 视频高度
    public int fps;                      // 帧率（fps）
    public int videoBitrate;              // 视频码率（Kbps）
    public int audioBitrate;              // 音频码率（Kbps）
    public int audioPacketLoss;           // 网络音频丢包率（%）
    public int videoPacketLoss;           // 网络视频丢包率（%）
    public int jitterBufferDelay;        // 播放延迟（ms）
    public int audioTotalBlockTime;      // 音频播放累计卡顿时长（ms）
    public int audioBlockRate;           // 音频播放卡顿率（%）
    public int videoTotalBlockTime;      // 视频播放累计卡顿时长（ms）
    public int videoBlockRate;            // 视频播放卡顿率（%）
    public int rtt;                      // 往返延时（ms）
    public int netSpeed;                  // 下载速度（kbps）
}
```

## 五、连接状态相关枚举

### V2TXLivePushStatus - 直播流连接状态
```java
public enum V2TXLivePushStatus {
    /// 与服务器断开连接
    V2TXLivePushStatusDisconnected,
    
    /// 正在连接服务器
    V2TXLivePushStatusConnecting,
    
    /// 连接服务器成功
    V2TXLivePushStatusConnectSuccess,
    
    /// 重连服务器中
    V2TXLivePushStatusReconnecting,
}
```

## 六、云端混流配置

### V2TXLiveMixInputType - 混流输入类型
```java
public enum V2TXLiveMixInputType {
    /// 混入音视频
    V2TXLiveMixInputTypeAudioVideo,
    
    /// 只混入视频
    V2TXLiveMixInputTypePureVideo,
    
    /// 只混入音频
    V2TXLiveMixInputTypePureAudio,
}
```

### V2TXLiveMixStream - 云端混流子画面位置信息
```java
public static class V2TXLiveMixStream {
    public String userId;                // 参与混流的userId
    public String streamId;              // 推流streamId
    public int x;                        // 图层位置x坐标（绝对像素值）
    public int y;                        // 图层位置y坐标（绝对像素值）
    public int width;                    // 图层宽度（绝对像素值）
    public int height;                   // 图层高度（绝对像素值）
    public int zOrder;                   // 图层层次（1-15，不可重复）
    public V2TXLiveMixInputType inputType; // 直播流输入类型
}
```

### V2TXLiveTranscodingConfig - 云端混流转码配置
```java
public final static class V2TXLiveTranscodingConfig {
    public int videoWidth;               // 最终转码后的视频宽度
    public int videoHeight;              // 最终转码后的视频高度
    public int videoBitrate;              // 最终转码后的视频码率（kbps）
    public int videoFramerate;           // 最终转码后的视频帧率（FPS）
    public int videoGOP;                 // 关键帧间隔（秒）
    public int backgroundColor;          // 混合后画面的底色颜色
    public String backgroundImage;       // 混合后画面的背景图
    public int audioSampleRate;          // 最终转码后的音频采样率
    public int audioBitrate;              // 最终转码后的音频码率（kbps）
    public int audioChannels;            // 最终转码后的音频声道数
    public ArrayList<V2TXLiveMixStream> mixStreams; // 子画面位置信息
    public String outputStreamId;        // 输出到CDN的直播流ID
}
```

## 七、本地录制配置

### V2TXLiveRecordMode - 本地音视频录制模式
```java
public enum V2TXLiveRecordMode {
    /// 录制音频和视频
    V2TXLiveRecordModeBoth,
}
```

### V2TXLiveLocalRecordingParams - 本地录制配置参数
```java
public final static class V2TXLiveLocalRecordingParams {
    public String filePath;              // 录制的文件地址（必填）
    public V2TXLiveRecordMode recordMode; // 媒体录制模式
    public int interval;                  // 录制信息更新频率（毫秒）
}
```

## 八、日志配置

### V2TXLiveLogLevel - 日志级别枚举
```java
public static final class V2TXLiveLogLevel {
    public static final int V2TXLiveLogLevelAll = 0;      // 输出所有级别的log
    public static final int V2TXLiveLogLevelDebug = 1;   // 输出DEBUG及以上级别
    public static final int V2TXLiveLogLevelInfo = 2;    // 输出INFO及以上级别
    public static final int V2TXLiveLogLevelWarning = 3; // 输出WARNING及以上级别
    public static final int V2TXLiveLogLevelError = 4;   // 输出ERROR及以上级别
    public static final int V2TXLiveLogLevelFatal = 5;   // 只输出FATAL级别
    public static final int V2TXLiveLogLevelNULL = 6;    // 不输出任何SDK log
}
```

### V2TXLiveLogConfig - 日志配置类
```java
public final static class V2TXLiveLogConfig {
    public int logLevel;                  // 设置Log级别
    public boolean enableObserver;        // 是否通过Observer接收Log信息
    public boolean enableConsole;         // 是否在编辑器控制台打印Log
    public boolean enableLogFile;         // 是否启用本地Log文件
    public String logPath;               // 本地Log存储目录
}
```

## 九、其他配置

### V2TXLiveSocks5ProxyConfig - Socks5代理协议配置

```java
public final static class V2TXLiveSocks5ProxyConfig {
    public boolean supportHttps = true;  // 是否支持HTTPS
    public boolean supportTcp = true;     // 是否支持TCP
    public boolean supportUdp = true;     // 是否支持UDP
}
```

### V2TXLiveStreamInfo - 自适应切换的码流信息
```java
public final static class V2TXLiveStreamInfo {
    public int width;                    // 视频宽度
    public int height;                   // 视频高度
    public int bitrate;                  // 码率（bps）
    public float framerate;              // 帧率
    public String url;                   // 流地址
}
```

该文档涵盖了V2TXLiveDef.java中的所有类型定义，为开发腾讯云直播功能提供了完整的API参考。