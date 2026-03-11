> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

# 腾讯云直播SDK V2TXLivePusher 推流接口文档

## 概述

`V2TXLivePusher` 是腾讯云直播 SDK 的核心推流器接口类，负责将本地的音频和视频画面进行编码，并推送到指定的推流地址，支持任意的推流服务端。

**平台支持**: iOS, macOS  
**功能范围**: 推流控制、音视频采集、特效处理、云端混流、本地录制

## 📋 目录结构

### 1. [核心功能特性](#核心功能特性)
### 2. [推流器初始化](#推流器初始化)
### 3. [视频预览与渲染](#视频预览与渲染)
### 4. [音视频采集控制](#音视频采集控制)
### 5. [推流控制接口](#推流控制接口)
### 6. [音视频质量控制](#音视频质量控制)
### 7. [特效与设备管理](#特效与设备管理)
### 8. [高级功能接口](#高级功能接口)
### 9. [云端混流与录制](#云端混流与录制)
### 10. [使用示例](#使用示例)

## 1. 核心功能特性

### 🎯 主要能力

- **自定义视频采集**: 支持定制音视频数据源
- **美颜滤镜贴纸**: 多套美颜算法和色彩空间滤镜
- **QoS流量控制**: 上行网络自适应能力
- **AI人脸特效**: 基于优图AI技术的大眼、瘦脸、隆鼻等效果
- **云端混流转码**: 多路音视频流混合为一路标准直播流
- **本地录制**: 支持音视频流本地录制

### 🔧 技术规格

- **支持协议**: RTMP, RTC
- **平台适配**: iOS 11.0+, macOS
- **编码格式**: H.264/H.265视频, AAC音频
- **分辨率支持**: 最高4K超高清
- **帧率范围**: 15-60fps自适应

## 2. 推流器初始化

### initWithLiveMode() - 初始化推流器

**参数**:
- `liveMode`: 推流协议类型
  - `V2TXLiveModeRTMP`: RTMP协议（默认）
  - `V2TXLiveModeRTC`: ROOM协议

**使用时机**: 应用启动时调用

**示例**:
```objc
// 创建 RTMP 协议推流实例，startPush 必须传入 RTMP 协议地址
V2TXLivePusher *pusher = [[V2TXLivePusher alloc] initWithLiveMode:V2TXLiveModeRTMP];

// 创建 RTC 协议推流实例，startPush 必须传入 RTC 协议地址
V2TXLivePusher *pusher = [[V2TXLivePusher alloc] initWithLiveMode:V2TXLiveModeRTC];
```

### setObserver() - 设置推流器回调

```objc
- (void)setObserver:(id<V2TXLivePusherObserver>)observer;
```

**参数**:
- `observer`: 实现V2TXLivePusherObserver协议的对象

**使用时机**: 推流器初始化后立即设置

**注意事项**:
- 观察者对象需要在整个推流生命周期内保持有效
- 用于接收推流状态、统计数据、警告和错误信息

## 3. 视频预览与渲染

### setRenderView() - 设置本地摄像头预览视图

```objc
- (V2TXLiveCode)setRenderView:(TXView *)view;
```

**参数**:
- `view`: 本地摄像头预览视图

**使用时机**: 必须在开始推流前设置预览视图

**说明**: 本地摄像头采集到的画面，经过美颜、脸型调整、滤镜等多种效果叠加之后，最终会显示在View上

### 🔄 setRenderMirror - 设置预览镜像

```objc
- (V2TXLiveCode)setRenderMirror:(V2TXLiveMirrorType)mirrorType;
```

**功能**: 设置本地摄像头预览镜像模式

**参数说明**:
- `mirrorType`: 镜像类型
  - `V2TXLiveMirrorTypeAuto`: 默认镜像类型（前置镜像，后置不镜像）
  - `V2TXLiveMirrorTypeEnable`: 前后置摄像头都镜像
  - `V2TXLiveMirrorTypeDisable`: 前后置摄像头都不镜像

### 📺 setEncoderMirror - 设置编码镜像

```objc
- (V2TXLiveCode)setEncoderMirror:(BOOL)mirror;
```

**功能**: 设置视频编码镜像，影响观众端看到的画面

**参数说明**:
- `mirror`: 是否镜像
  - `NO`: 观众看到非镜像画面（默认）
  - `YES`: 观众看到镜像画面

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功

**重要区别**:
- `setRenderMirror`: 只影响本地预览
- `setEncoderMirror`: 影响观众端观看效果

**使用时机**: 无限制

**示例**:
```objc
// 观众端看到镜像画面
[pusher setEncoderMirror:YES];
// 观众端看到非镜像画面
[pusher setEncoderMirror:NO];
```

### 🎛️ setRenderRotation - 设置预览旋转

```objc
- (V2TXLiveCode)setRenderRotation:(V2TXLiveRotation)rotation;
```

**功能**: 设置本地摄像头预览画面的旋转角度

**参数说明**:
- `rotation`: 旋转角度
  - `V2TXLiveRotation0`: 0度不旋转（默认）
  - `V2TXLiveRotation90`: 顺时针旋转90度
  - `V2TXLiveRotation180`: 顺时针旋转180度
  - `V2TXLiveRotation270`: 顺时针旋转270度

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功

**说明**: 只旋转本地预览画面，不影响推流出去的画面

**使用时机**: 无限制

**示例**:
```objc
// 设置预览画面旋转0度
[pusher setRenderRotation:V2TXLiveRotation0];
// 设置预览画面旋转90度
[pusher setRenderRotation:V2TXLiveRotation90];
// 设置预览画面旋转180度
[pusher setRenderRotation:V2TXLiveRotation180];
// 设置预览画面旋转270度
[pusher setRenderRotation:V2TXLiveRotation270];
```

### 🖼️ setRenderFillMode - 设置填充模式

```objc
- (V2TXLiveCode)setRenderFillMode:(V2TXLiveFillMode)mode;
```

**功能**: 设置本地摄像头预览画面的填充模式

**参数说明**:
- `mode`: 填充模式
  - `V2TXLiveFillModeFill`: 图像铺满屏幕，可能裁剪（默认）
  - `V2TXLiveFillModeFit`: 图像适应屏幕，保持完整，可能有黑边
  - `V2TXLiveFillModeScaleFill`: 图像拉伸铺满，可能变形

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功

**说明**: 只影响本地预览画面，不影响推流出去的画面

**使用时机**: 无限制

**示例**:
```objc
// 图像铺满屏幕，不留黑边，部分画面可能被裁剪
[pusher setRenderFillMode:V2TXLiveFillModeFill];
// 图像适应屏幕，保持画面完整，可能有黑边
[pusher setRenderFillMode:V2TXLiveFillModeFit];
// 图像拉伸铺满，长度和宽度可能不会按比例变化
[pusher setRenderFillMode:V2TXLiveFillModeScaleFill];
```
### startCamera() - 打开本地摄像头

```objc
// iOS版本
- (V2TXLiveCode)startCamera:(BOOL)frontCamera;

// macOS版本
- (V2TXLiveCode)startCamera:(NSString *)cameraId;
```

**参数**:
- **iOS**: `frontCamera` - 是否为前置摄像头
- **macOS**: `cameraId` - 摄像头标识

**重要说明**:
- **推流前必须开启至少一个采集源**，否则推流将失败
- `startVirtualCamera`, `startCamera`, `startScreenCapture`在同一Pusher实例下，仅有一个采集源可以上行
- 不同采集源之间切换，请先关闭前一采集源，再开启后一采集源

**使用时机**: 必须推流前调用

### startMicrophone() - 打开麦克风

```objc
- (V2TXLiveCode)startMicrophone;
```

**使用场景**:
- **音视频直播**: 配合摄像头采集提供音频
- **纯音频直播**: 单独使用麦克风进行音频推流
- **屏幕分享**: 配合屏幕采集提供系统声音和麦克风声音

**注意事项**:
- **推流前必须调用此方法开启麦克风采集**，否则推流将只有视频没有音频
- 纯音频推流场景下，可以单独使用麦克风采集
- 推流过程中可以动态开启/关闭麦克风采集

**使用时机**: 推流前必须调用

### startVirtualCamera() - 开启图片推流

```objc
- (V2TXLiveCode)startVirtualCamera:(TXImage *)image;
```

**参数**:
- `image`: 推流使用的图片

**使用场景**:
- **图片直播**: 将静态图片作为视频源进行推流
- **维护页面**: 系统维护时显示维护页面
- **广告展示**: 展示广告图片

**注意事项**:
- **推流前必须调用此方法开启图片推流**，否则推流将失败
- 图片会被编码为视频流进行推送，消耗带宽
- 通常需要配合麦克风采集提供音频
- 图片推流和摄像头采集不能同时开启

**使用时机**: 推流前必须调用

### startScreenCapture() - 开始屏幕采集

```objc
- (V2TXLiveCode)startScreenCapture:(NSString *)appGroup;
```

**参数**:
- `appGroup`: 主App与Broadcast共享的Application Group Identifier

**使用场景**:
- **屏幕分享**: 分享设备屏幕内容进行直播
- **远程教学**: 教师分享屏幕进行在线教学
- **游戏直播**: 分享游戏画面进行游戏直播
- **应用演示**: 演示App操作流程

**注意事项**:
- **推流前必须调用此方法开启屏幕采集**，否则推流将失败
- iOS系统需要申请屏幕录制权限
- 可以配合`startSystemAudioLoopback()`采集系统声音
- 屏幕采集和摄像头采集不能同时开启

**使用时机**: 推流前必须调用

### ⏸️ 停止采集接口

```objc
// 停止摄像头
- (V2TXLiveCode)stopCamera;

// 停止麦克风
- (V2TXLiveCode)stopMicrophone;

// 停止图片推流
- (V2TXLiveCode)stopVirtualCamera;

// 停止屏幕采集
- (V2TXLiveCode)stopScreenCapture;
```

## 5. 推流控制接口

### startPush() - 开始音视频数据推流

```objc
- (V2TXLiveCode)startPush:(NSString *)url;
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

### 🛑 stopPush - 停止推流

```objc
- (V2TXLiveCode)stopPush;
```

**功能**: 停止推送音视频数据

**返回值**:
- `V2TXLIVE_OK`: 成功

### 📊 isPushing - 推流状态检查

```objc
- (int)isPushing;
```

**功能**: 检查当前推流器是否正在推流中

**返回值**:
- `1`: 正在推流中
- `0`: 已经停止推流

## 6. 音视频质量控制

### setAudioQuality() - 设置推流音频质量

```objc
- (V2TXLiveCode)setAudioQuality:(V2TXLiveAudioQuality)quality;
```

**参数**:
- `quality`: 音频质量
  - `V2TXLiveAudioQualityDefault`: 通用音质（默认）
  - `V2TXLiveAudioQualitySpeech`: 语音音质
  - `V2TXLiveAudioQualityMusic`: 音乐音质

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功
- `V2TXLIVE_ERROR_REFUSED`: 推流过程中，不允许调整音质

**使用时机**: 推流开始前

**示例**:
```objc
// 设置通用音质
[pusher setAudioQuality:V2TXLiveAudioQualityDefault];

// 设置语音音质（适合语音通话场景）
[pusher setAudioQuality:V2TXLiveAudioQualitySpeech];

// 设置音乐音质（适合音乐直播场景）
[pusher setAudioQuality:V2TXLiveAudioQualityMusic];
```
**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功
- `V2TXLIVE_ERROR_REFUSED`: 推流过程中，不允许调整音质

**使用时机**: 推流开始前

### setVideoQuality() - 设置推流视频编码参数

```objc
- (V2TXLiveCode)setVideoQuality:(V2TXLiveVideoEncoderParam *)param;
```

**参数**:
- `param`: 视频编码参数对象

**可配置参数**:
- 分辨率、码率、帧率
- 编码模式（软编/硬编）
- 编码复杂度

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功
- `V2TXLIVE_ERROR_REFUSED`: 推流过程中，不允许调整视频质量

**使用时机**: 推流开始前

**示例**:
```objc
V2TXLiveVideoEncoderParam *param = [[V2TXLiveVideoEncoderParam alloc] init];
param.videoResolution = V2TXLiveVideoResolution1280x720;
param.videoFps = 15;
param.videoBitrate = 1200;
param.minVideoBitrate = 800;
param.enableAdjustRes = YES;
param.videoEncoderMode = V2TXLiveVideoEncoderModeHardware;

[pusher setVideoQuality:param];
```

### pauseAudio() / resumeAudio() - 暂停/恢复推流器的音频流

```objc
- (V2TXLiveCode)pauseAudio;
- (V2TXLiveCode)resumeAudio;
```

**使用场景**:
- **临时静音**: 主播需要临时静音时使用
- **录制场景**: 需要保持音频流连续性的MP4录制场景
- **音频切换**: 从麦克风采集切换到背景音乐播放时

**注意事项**:
- 与`stopMicrophone()`的区别：不会中断音频流，而是发送极低码率的静音包
- 暂停期间音频流仍然存在，只是内容为静音
- 适合需要保持音频连续性的录制场景

**使用时机**: 推流过程中

### pauseVideo() / resumeVideo() - 暂停/恢复推流器的视频流

```objc
- (V2TXLiveCode)pauseVideo;
- (V2TXLiveCode)resumeVideo;
```

**使用场景**:
- **临时黑屏**: 主播需要临时关闭摄像头画面时
- **画面切换**: 从摄像头采集切换到图片推流时
- **隐私保护**: 需要临时隐藏画面保护隐私时

**注意事项**:
- 暂停期间视频流仍然存在，只是内容为黑屏或最后一帧
- 适合需要保持视频流连续性的场景

**使用时机**: 推流过程中

## 7. 特效与设备管理

### 🎵 getAudioEffectManager - 音效管理

```objc
- (TXAudioEffectManager *)getAudioEffectManager;
```

**功能**: 获取音效管理对象

**支持功能**:
- 调整麦克风音量
- 设置混响和变声效果
- 开启耳返，设置耳返音量
- 添加背景音乐，调整播放效果

### 💄 getBeautyManager - 美颜管理

```objc
- (TXBeautyManager *)getBeautyManager;
```

**功能**: 获取美颜管理对象

**支持功能**:
- **基础美颜**: 美颜风格、美白、红润
- **美型调整**: 大眼、瘦脸、V脸、下巴、短脸
- **细节优化**: 小鼻、亮眼、白牙、祛眼袋、祛皱纹
- **人脸特效**: 人脸挂件、美妆、手势识别

### 🔧 getDeviceManager - 设备管理

```objc
- (TXDeviceManager *)getDeviceManager;
```

**功能**: 获取设备管理对象

**支持功能**:
- 切换前后摄像头
- 设置自动聚焦
- 设置摄像头缩放倍数
- 打开/关闭闪光灯
- 切换耳机/扬声器
- 修改音量类型

## 8. 高级功能接口

### snapshot() - 截取推流过程中的本地画面

```objc
- (V2TXLiveCode)snapshot;
```

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功
- `V2TXLIVE_ERROR_REFUSED`: 已经停止推流，不允许调用截图操作

**使用时机**: 开始推流后

### 💧 setWatermark - 设置水印

```objc
- (V2TXLiveCode)setWatermark:(TXImage *)image x:(float)x y:(float)y scale:(float)scale;
```

**功能**: 设置推流器水印

**参数说明**:
- `image`: 水印图片（nil表示禁用水印）
- `x`: 水印横坐标（0-1）
- `y`: 水印纵坐标（0-1）
- `scale`: 水印缩放比例（0-1）

### 🔊 enableVolumeEvaluation - 音量评估

```objc
- (V2TXLiveCode)enableVolumeEvaluation:(NSUInteger)intervalMs;
```

**功能**: 启用采集音量大小提示

**参数说明**:
- `intervalMs`: 回调触发间隔（最小100ms，建议300ms）

**使用场景**: 在`onMicrophoneVolumeUpdate`回调中获取音量评估值

### 📡 sendSeiMessage - 发送SEI消息

```objc
- (V2TXLiveCode)sendSeiMessage:(int)payloadType data:(NSData *)data;
```

**功能**: 发送SEI（Supplemental Enhancement Information）消息

**参数说明**:
- `payloadType`: 数据类型（支持5、242，推荐242）
- `data`: 待发送的数据

**接收端**: 播放器通过`onReceiveSeiMessage`回调接收

### 🔍 showDebugView - 显示调试视图

```objc
- (void)showDebugView:(BOOL)isShow;
```

**功能**: 显示/隐藏仪表盘调试视图

**参数说明**:
- `isShow`: 是否显示（默认NO）

## 9. 自定义采集接口

### enableCustomVideoCapture() - 开启/关闭自定义视频采集

```objc
- (V2TXLiveCode)enableCustomVideoCapture:(BOOL)enable;
```

**参数**:
- `enable`: true开启自定义采集，false关闭【默认值: false】

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功

**使用场景**:
- **外部设备采集**: 连接外部摄像头、采集卡等设备
- **视频处理**: 对视频进行特殊处理后再推流
- **多路合成**: 将多路视频源合成为一路推流
- **特殊格式**: 支持特殊视频格式的推流

**注意事项**:
- **推流前必须调用此方法开启自定义采集**，否则推流将失败
- 必须在`startPush`之前调用才会生效
- 自定义采集模式下，SDK只负责编码和发送，不进行实际采集

**使用时机**: 推流开始前

**示例**:
```objc
// 开启自定义视频采集
[pusher enableCustomVideoCapture:YES];

// 关闭自定义视频采集
[pusher enableCustomVideoCapture:NO];
```

### enableCustomAudioCapture() - 开启/关闭自定义音频采集

```objc
- (V2TXLiveCode)enableCustomAudioCapture:(BOOL)enable;
```

**参数**:
- `enable`: true开启自定义采集，false关闭【默认值: false】

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功

**使用场景**:
- **外部音频设备**: 连接外部麦克风、音频接口等设备
- **音频处理**: 对音频进行特殊处理后再推流
- **多路音频**: 将多路音频源合成为一路推流
- **特殊格式**: 支持特殊音频格式的推流

**注意事项**:
- **推流前必须调用此方法开启自定义采集**，否则推流将失败
- 必须在`startPush`之前调用才会生效
- 自定义采集模式下，SDK只负责编码和发送，不进行实际采集

**使用时机**: 推流开始前

**示例**:
```objc
// 开启自定义音频采集
[pusher enableCustomAudioCapture:YES];

// 关闭自定义音频采集
[pusher enableCustomAudioCapture:NO];
```

### 📦 sendCustomVideoFrame - 发送自定义视频帧

```objc
- (V2TXLiveCode)sendCustomVideoFrame:(V2TXLiveVideoFrame *)videoFrame;
```

**功能**: 在自定义采集模式下发送视频数据到SDK

**前提条件**: 必须先调用`enableCustomVideoCapture`开启自定义采集

### 🔊 sendCustomAudioFrame - 发送自定义音频帧

```objc
- (V2TXLiveCode)sendCustomAudioFrame:(V2TXLiveAudioFrame *)audioFrame;
```

**功能**: 在自定义采集模式下发送音频数据到SDK

### 🔄 enableCustomVideoProcess - 自定义视频处理

```objc
- (V2TXLiveCode)enableCustomVideoProcess:(BOOL)enable 
                            pixelFormat:(V2TXLivePixelFormat)pixelFormat 
                            bufferType:(V2TXLiveBufferType)bufferType;
```

**功能**: 开启/关闭自定义视频处理

**支持格式组合**:
- `V2TXLivePixelFormatTexture2D` + `V2TXLiveBufferTypeTexture`
- `V2TXLivePixelFormatNV12` + `V2TXLiveBufferTypePixelBuffer`
- `V2TXLivePixelFormatBGRA32` + `V2TXLiveBufferTypePixelBuffer`

### 🎧 enableAudioProcessObserver - 音频处理监听

```objc
- (V2TXLiveCode)enableAudioProcessObserver:(BOOL)enable 
                                  format:(V2TXLiveAudioFrameObserverFormat *)format;
```

**功能**: 开启/关闭对前处理后的本地音频帧的监听

**使用时机**: 必须在`startPush`之前调用

## 10. 云端混流与录制

### setMixTranscodingConfig() - 设置云端的混流转码参数

```objc
- (V2TXLiveCode)setMixTranscodingConfig:(V2TXLiveTranscodingConfig *)config;
```

**参数**:
- `config`: 混流转码配置，传入nil则取消云端混流转码

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

**重要注意事项**:
- **仅支持RTC协议混流**：该接口只能在RTC协议下使用，不支持RTMP等其他推流协议
- 云端转码会引入1-2秒的CDN观看延时
- 及时传入nil取消混流，避免不必要的计费损失

**使用时机**: 推流过程中

**示例**:
```objc
// 配置云端混流参数
V2TXLiveTranscodingConfig *config = [[V2TXLiveTranscodingConfig alloc] init];
config.videoWidth = 720;
config.videoHeight = 1280;
config.videoBitrate = 1500;
config.videoFps = 15;
config.videoGOP = 3;
config.backgroundColor = 0x000000;
config.backgroundImage = nil;

// 设置混流用户
V2TXLiveMixUser *user1 = [[V2TXLiveMixUser alloc] init];
user1.userId = @"user1";
user1.x = 0;
user1.y = 0;
user1.width = 0.5;
user1.height = 1.0;
user1.zOrder = 0;

config.mixUsers = @[user1];

// 应用混流配置
V2TXLiveCode result = [pusher setMixTranscodingConfig:config];
if (result == V2TXLIVE_OK) {
    NSLog(@"混流配置设置成功");
}

// 取消混流
result = [pusher setMixTranscodingConfig:nil];
if (result == V2TXLIVE_OK) {
    NSLog(@"混流配置取消成功");
}
```

### startLocalRecording() - 开始录制音视频流

```objc
- (V2TXLiveCode)startLocalRecording:(V2TXLiveLocalRecordingParams *)params;
```

**参数**:
- `params`: 本地录制参数

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: 参数不合法
- `V2TXLIVE_ERROR_REFUSED`: 推流尚未开始，不允许录制

**使用时机**: 推流开启后

**注意事项**:
- 推流开启后才能开始录制，非推流状态下开启录制无效
- 录制过程中不要动态切换分辨率和软/硬编码
- 停止推流后，如果还在录制中，SDK会自动结束录制

**示例**:
```objc
// 设置录制回调
[pusher setObserver:self];

// 配置录制参数
V2TXLiveLocalRecordingParams *params = [[V2TXLiveLocalRecordingParams alloc] init];
params.filePath = @"/path/to/record/file.mp4";
params.recordType = V2TXLiveRecordTypeBoth;
params.interval = 2000;

// 开始本地录制
V2TXLiveCode result = [pusher startLocalRecording:params];
if (result == V2TXLIVE_OK) {
    NSLog(@"本地录制开始成功");
} else if (result == V2TXLIVE_ERROR_INVALID_PARAMETER) {
    NSLog(@"录制参数不合法");
} else if (result == V2TXLIVE_ERROR_REFUSED) {
    NSLog(@"录制调用被拒绝，请先开始推流");
}

// 在回调中处理录制状态
- (void)onLocalRecordBegin:(int)code storagePath:(NSString *)storagePath {
    if (code == V2TXLIVE_OK) {
        NSLog(@"录制开始，存储路径: %@", storagePath);
    }
}

- (void)onLocalRecording:(long)durationMs storagePath:(NSString *)storagePath {
    NSLog(@"录制中，时长: %ldms", durationMs);
}

- (void)onLocalRecordComplete:(int)code storagePath:(NSString *)storagePath {
    if (code == V2TXLIVE_OK) {
        NSLog(@"录制完成，存储路径: %@", storagePath);
    }
}
```

### ⏹️ stopLocalRecording - 停止录制

```objc
- (void)stopLocalRecording;
```

**功能**: 停止录制音视频流

**自动处理**: 停止推流后，如果还在录制中，SDK会自动结束录制

### 🎙️ enableVoiceActivityDetection - 人声检测

```objc
- (void)enableVoiceActivityDetection:(BOOL)enable;
```

**功能**: 启用人声检测

**回调**: 在`OnVoiceActivityDetectionUpdate`回调中获取语音活动状态

## 11. 高级API接口

### 🔧 setProperty/getProperty - 高级属性设置

```objc
- (V2TXLiveCode)setProperty:(NSString *)key value:(NSObject *)value;
- (NSString *)getProperty:(NSString *)key;
```

**功能**: 调用高级API接口

**使用场景**: 调用一些实验性功能或高级配置

**参考文档**: `V2TXLiveProperty.h`中的定义

## 12. 使用示例

### 🔧 基础推流示例

```objc
// 1. 初始化推流器
V2TXLivePusher *pusher = [[V2TXLivePusher alloc] initWithLiveMode:V2TXLiveModeRTMP];

// 2. 设置回调观察者
[pusher setObserver:self];

// 3. 设置预览视图
[pusher setRenderView:self.previewView];

// 4. 开启摄像头和麦克风
[pusher startCamera:YES];  // iOS前置摄像头
[pusher startMicrophone];

// 5. 开始推流
NSString *pushUrl = @"rtmp://your-push-url/live/stream";
V2TXLiveCode result = [pusher startPush:pushUrl];

if (result == V2TXLIVE_OK) {
    NSLog(@"推流开始成功");
} else {
    NSLog(@"推流开始失败，错误码: %ld", (long)result);
}
```

### 🎨 美颜特效配置示例

```objc
// 获取美颜管理器
TXBeautyManager *beautyManager = [pusher getBeautyManager];

// 设置基础美颜
[beautyManager setBeautyStyle:TXBeautyStyleNature];
[beautyManager setBeautyLevel:6.0];
[beautyManager setWhitenessLevel:3.0];
[beautyManager setRuddyLevel:2.0];

// 设置美型效果
[beautyManager setEyeScaleLevel:3.0];      // 大眼
[beautyManager setFaceSlimLevel:4.0];      // 瘦脸
[beautyManager setFaceVLevel:2.0];        // V脸
```

### 🌐 云端混流配置示例

```objc
// 配置云端混流参数
V2TXLiveTranscodingConfig *config = [[V2TXLiveTranscodingConfig alloc] init];
config.videoWidth = 720;
config.videoHeight = 1280;
config.videoBitrate = 1500;
config.videoFramerate = 15;
config.videoGOP = 3;
config.backgroundColor = 0x000000;
config.backgroundImage = nil;

// 设置混流用户
V2TXLiveMixUser *user1 = [[V2TXLiveMixUser alloc] init];
user1.userId = @"user1";
user1.x = 0;
user1.y = 0;
user1.width = 0.5;
user1.height = 1.0;
user1.zOrder = 0;

config.mixUsers = @[user1];

// 应用混流配置
[pusher setMixTranscodingConfig:config];
```

### 🎥 自定义采集示例

```objc
// 开启自定义视频采集
[pusher enableCustomVideoCapture:YES];

// 在自定义采集源中发送视频帧
V2TXLiveVideoFrame *videoFrame = [[V2TXLiveVideoFrame alloc] init];
videoFrame.pixelFormat = V2TXLivePixelFormatNV12;
videoFrame.bufferType = V2TXLiveBufferTypePixelBuffer;
videoFrame.data = pixelBufferData;
videoFrame.width = 720;
videoFrame.height = 1280;
videoFrame.rotation = V2TXLiveRotation0;

// 发送自定义视频帧
[pusher sendCustomVideoFrame:videoFrame];
```

## 13. 使用示例

### 🔧 基础推流示例（摄像头+麦克风）
```objc
// 1. 创建推流器实例
V2TXLivePusher *pusher = [[V2TXLivePusher alloc] initWithLiveMode:V2TXLiveModeRTMP];

// 2. 设置回调
[pusher setObserver:self];

// 3. 设置预览视图
[pusher setRenderView:self.previewView];

// 重要：推流前必须开启至少一个采集源
// 4. 开启摄像头采集（前置摄像头）
[pusher startCamera:YES];

// 5. 开启麦克风采集
[pusher startMicrophone];

// 6. 开始推流（必须在采集源开启后调用）
NSString *pushUrl = @"rtmp://your-stream-url";
V2TXLiveCode result = [pusher startPush:pushUrl];

if (result == V2TXLIVE_OK) {
    NSLog(@"推流开始成功");
} else {
    NSLog(@"推流开始失败，错误码: %ld", (long)result);
}
```

### 🖥️ 屏幕分享推流示例
```objc
// 1. 创建推流器实例
V2TXLivePusher *pusher = [[V2TXLivePusher alloc] initWithLiveMode:V2TXLiveModeRTMP];

// 2. 设置回调
[pusher setObserver:self];

// 重要：推流前必须开启至少一个采集源
// 3. 开启屏幕采集
[pusher startScreenCapture:@"group.com.your.app"];

// 4. 开启麦克风采集（可选，如果需要声音）
[pusher startMicrophone];

// 5. 开始推流
NSString *pushUrl = @"rtmp://your-stream-url";
V2TXLiveCode result = [pusher startPush:pushUrl];

if (result == V2TXLIVE_OK) {
    NSLog(@"屏幕分享推流开始成功");
} else {
    NSLog(@"屏幕分享推流开始失败，错误码: %ld", (long)result);
}
```

### 🎬 自定义采集示例
```objc
// 1. 创建推流器实例
V2TXLivePusher *pusher = [[V2TXLivePusher alloc] initWithLiveMode:V2TXLiveModeRTMP];

// 2. 设置回调
[pusher setObserver:self];

// 重要：推流前必须开启至少一个采集源
// 3. 开启自定义视频采集（必须在startPush之前调用）
[pusher enableCustomVideoCapture:YES];

// 4. 开启自定义音频采集（可选，如果需要音频）
[pusher enableCustomAudioCapture:YES];

// 5. 开始推流
NSString *pushUrl = @"rtmp://your-stream-url";
V2TXLiveCode result = [pusher startPush:pushUrl];

if (result == V2TXLIVE_OK) {
    NSLog(@"自定义采集推流开始成功");
} else {
    NSLog(@"自定义采集推流开始失败，错误码: %ld", (long)result);
}

// 6. 在自定义采集模式下发送视频帧
V2TXLiveVideoFrame *videoFrame = [[V2TXLiveVideoFrame alloc] init];
videoFrame.pixelFormat = V2TXLivePixelFormatNV12;
videoFrame.bufferType = V2TXLiveBufferTypePixelBuffer;
videoFrame.width = 1920;
videoFrame.height = 1080;
videoFrame.rotation = V2TXLiveRotation0;

// 发送自定义视频帧
[pusher sendCustomVideoFrame:videoFrame];
```

## 14. 最佳实践

### 🔧 采集源管理规则

**重要原则**: 同一推流器实例下，只能有一个采集源上行

**正确切换顺序**:
```objc
// 从摄像头切换到图片推流
[pusher startCamera:YES];
// ... 使用摄像头推流 ...
[pusher stopCamera];           // 先停止当前采集源
[pusher startVirtualCamera:image];  // 再开启新采集源
```

### ⚡ 性能优化建议

**音频处理**:
- 使用`pauseAudio`而不是`stopMicrophone`来保持音频连续性
- 合理设置音频质量，语音场景使用`V2TXLiveAudioQualitySpeech`

**视频编码**:
- 根据网络状况动态调整视频码率
- 合理设置GOP大小，直播场景建议2-3秒
- 移动端推荐使用硬编码以获得更好性能

**资源管理**:
- 及时释放不再使用的采集源
- 推流结束后调用`stopPush`释放资源
- 合理设置预览视图的填充模式
