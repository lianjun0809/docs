> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

# 腾讯云直播SDK V2TXLivePusher 推流接口文档

## 概述

`V2TXLivePusher` 是腾讯云直播SDK的核心推流器接口类，负责将本地的音频和视频画面进行编码，并推送到指定的推流地址，支持任意的推流服务端。

**文件路径**: `com/tencent/live2/V2TXLivePusher.java`
**平台支持**: Android

## 核心功能

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
```java
// 创建 RTMP 协议推流实例，startPush 必须传入 RTMP 协议地址
V2TXLivePusher pusher = new V2TXLivePusherImpl(context, V2TXLiveDef.V2TXLiveMode.TXLiveMode_RTMP);

// 创建 RTC 协议推流实例，startPush 必须传入 RTC 协议地址
V2TXLivePusher pusher = new V2TXLivePusherImpl(context, V2TXLiveDef.V2TXLiveMode.TXLiveMode_RTC);
```

**协议选择建议**:
- **RTMP协议**: 适合CDN直播分发场景，延迟较高（2-3秒）
- **RTC协议**: 适合实时互动场景，延迟较低（400ms以内）

## 接口详解

### 1. 基础设置接口

#### setObserver() - 设置推流器回调
```java
public abstract void setObserver(V2TXLivePusherObserver observer);
```

**参数**:
- `observer`: 推流器回调目标对象，需实现 `V2TXLivePusherObserver` 协议

**使用时机**: 推流器初始化后立即设置

**说明**: 通过设置回调，可以监听推流器状态、音量回调、统计数据、警告和错误信息等

**示例**:
```java
pusher.setObserver(new V2TXLivePusherObserver(){
  // ...
});
```

#### setRenderView() - 设置本地摄像头预览View
```java
public abstract int setRenderView(TXCloudVideoView view);
public abstract int setRenderView(TextureView view);
public abstract int setRenderView(SurfaceView view);
```

**参数**:
- `view`: 本地摄像头预览View，支持三种类型

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功

**使用时机**: 必须在开始推流前设置预览视图

**说明**: 本地摄像头采集到的画面，经过美颜、脸型调整、滤镜等多种效果叠加之后，最终会显示View上

**示例**:
```java
pusher.setRenderView(videoView);
```

#### setRenderMirror() - 设置本地摄像头预览镜像
```java
public abstract int setRenderMirror(V2TXLiveMirrorType mirrorType);
```

**参数**:
- `mirrorType`: 摄像头镜像类型 `V2TXLiveDef#V2TXLiveMirrorType`
  - `V2TXLiveMirrorTypeAuto`【默认值】: 前置摄像头镜像，后置摄像头不镜像
  - `V2TXLiveMirrorTypeEnable`: 前置和后置摄像头都镜像
  - `V2TXLiveMirrorTypeDisable`: 前置和后置摄像头都不镜像

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功

**使用时机**: 无限制

**示例**:
```java
// 前置摄像头镜像，后置摄像头不镜像
pusher.setRenderMirror(V2TXLiveDef.V2TXLiveMirrorType.V2TXLiveMirrorTypeAuto);
// 所有摄像头都镜像
pusher.setRenderMirror(V2TXLiveDef.V2TXLiveMirrorType.V2TXLiveMirrorTypeEnable);
// 所有摄像头都不镜像
pusher.setRenderMirror(V2TXLiveDef.V2TXLiveMirrorType.V2TXLiveMirrorTypeDisable);
```

#### setEncoderMirror() - 设置视频编码镜像
```java
public abstract int setEncoderMirror(boolean mirror);
```

**参数**:
- `mirror`: 是否镜像【默认值】：false

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功

**说明**: 编码镜像只影响观众端看到的视频效果

**使用时机**: 无限制

**示例**:
```java
// 观众端看到镜像画面
pusher.setEncoderMirror(true);
// 观众端看到非镜像画面
pusher.setEncoderMirror(false);
```

#### setRenderRotation() - 设置本地摄像头预览画面的旋转角度
```java
public abstract int setRenderRotation(V2TXLiveRotation rotation);
```

**参数**:
- `rotation`: 预览画面的旋转角度 `V2TXLiveDef#V2TXLiveRotation`
  - `V2TXLiveRotation0`【默认值】: 0度，不旋转
  - `V2TXLiveRotation90`: 顺时针旋转90度
  - `V2TXLiveRotation180`: 顺时针旋转180度
  - `V2TXLiveRotation270`: 顺时针旋转270度

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功

**说明**: 只旋转本地预览画面，不影响推流出去的画面

**使用时机**: 无限制

**示例**:
```java
// 设置预览画面旋转0度
pusher.setRenderRotation(V2TXLiveDef.V2TXLiveRotation.V2TXLiveRotation0);
// 设置预览画面旋转90度
pusher.setRenderRotation(V2TXLiveDef.V2TXLiveRotation.V2TXLiveRotation90);
// 设置预览画面旋转180度
pusher.setRenderRotation(V2TXLiveDef.V2TXLiveRotation.V2TXLiveRotation180);
// 设置预览画面旋转270度
pusher.setRenderRotation(V2TXLiveDef.V2TXLiveRotation.V2TXLiveRotation270);
```

#### setRenderFillMode() - 设置本地摄像头预览画面的填充模式
```java
public abstract int setRenderFillMode(V2TXLiveFillMode mode);
```

**参数**:
- `mode`: 画面填充模式 `V2TXLiveDef#V2TXLiveFillMode`
  - `V2TXLiveFillModeFill`【默认值】: 图像铺满屏幕，不留黑边，部分画面内容可能被裁剪
  - `V2TXLiveFillModeFit`: 图像适应屏幕，保持画面完整，可能有黑边
  - `V2TXLiveFillModeScaleFill`: 图像拉伸铺满，长度和宽度可能不会按比例变化

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功

**使用时机**: 无限制

**示例**:
```java
// 图像铺满屏幕
pusher.setRenderFillMode(V2TXLiveDef.V2TXLiveFillMode.V2TXLiveFillModeFill);
// 图像适应屏幕
pusher.setRenderFillMode(V2TXLiveDef.V2TXLiveFillMode.V2TXLiveFillModeFit);
// 图像拉伸铺满
pusher.setRenderFillMode(V2TXLiveDef.V2TXLiveFillMode.V2TXLiveFillModeScaleFill);
```

### 2. 采集控制接口

#### startCamera() / stopCamera() - 打开/关闭本地摄像头
```java
public abstract int startCamera(boolean frontCamera);
public abstract int stopCamera();
```

**参数**:
- `frontCamera`: 指定摄像头方向是否为前置【默认值】：true

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功

**重要说明**: 
- **推流前必须开启至少一个采集源**，否则推流将失败
- `startVirtualCamera`, `startCamera`, `startScreenCapture`在同一Pusher实例下，仅有一个采集源可以上行
- 不同采集源之间切换，请先关闭前一采集源，再开启后一采集源

**使用时机**: 必须推流前调用

**示例**:
```java
// 开启前置摄像头
pusher.startCamera(true);
// 开启后置摄像头
pusher.startCamera(false);
// 停止摄像头采集
pusher.stopCamera();
```

#### startMicrophone() / stopMicrophone() - 打开/关闭麦克风
```java
public abstract int startMicrophone();
public abstract int stopMicrophone();
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
```java
// 开启麦克风采集
pusher.startMicrophone();
// 停止麦克风采集
pusher.stopMicrophone();
```

#### startVirtualCamera() / stopVirtualCamera() - 开启/关闭图片推流
```java
public abstract int startVirtualCamera(Bitmap image);
public abstract int stopVirtualCamera();
```

**参数**:
- `image`: 推流的图片

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功

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

**示例**:
```java
// 开启图片推流
Bitmap image = BitmapFactory.decodeResource(getResources(), R.drawable.live_image);
pusher.startVirtualCamera(image);
// 停止图片推流
pusher.stopVirtualCamera();
```

#### startScreenCapture() / stopScreenCapture() - 开启/关闭屏幕采集
```java
public abstract int startScreenCapture();
public abstract int stopScreenCapture();
```

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功

**使用场景**:
- **屏幕分享**: 分享设备屏幕内容进行直播
- **远程教学**: 教师分享屏幕进行在线教学
- **游戏直播**: 分享游戏画面进行游戏直播
- **应用演示**: 演示App操作流程

**注意事项**:
- **推流前必须调用此方法开启屏幕采集**，否则推流将失败
- Android系统需要申请屏幕录制权限
- 可以配合`startSystemAudioLoopback()`采集系统声音
- 屏幕采集和摄像头采集不能同时开启

**使用时机**: 推流前必须调用

**示例**:
```java
// 开启屏幕采集
pusher.startScreenCapture();
// 停止屏幕采集
pusher.stopScreenCapture();
```

### 3. 推流控制接口

#### startPush() - 开始音视频数据推流
```java
public abstract int startPush(String url);
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
```java
int result = pusher.startPush("rtmp://example.com/live/stream");
if (result == V2TXLiveCode.V2TXLIVE_OK) {
    Log.i(TAG, "开始推流成功");
} else if (result == V2TXLiveCode.V2TXLIVE_ERROR_INVALID_PARAMETER) {
    Log.w(TAG, "推流地址不合法");
} else if (result == V2TXLiveCode.V2TXLIVE_ERROR_INVALID_LICENSE) {
    Log.w(TAG, "Licence不合法，请检查Licence");
} else if (result == V2TXLiveCode.V2TXLIVE_ERROR_REFUSED) {
    Log.w(TAG, "调用被拒绝");
}
```

#### stopPush() - 停止音视频数据推流
```java
public abstract int stopPush();
```

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功

**使用时机**: 开始推流后

**示例**:
```java
pusher.stopPush();
```

#### isPushing() - 检查当前推流器是否正在推流中
```java
public abstract int isPushing();
```

**返回值**:
- `1`: 正在推流中
- `0`: 已经停止推流

**使用时机**: 无限制

**示例**:
```java
int isPushing = pusher.isPushing();
if (isPushing == 1) {
    Log.i(TAG, "正在推流中");
} else {
    Log.i(TAG, "推流停止");
}
```

### 4. 音视频控制接口

#### pauseAudio() / resumeAudio() - 暂停/恢复推流器的音频流
```java
public abstract int pauseAudio();
public abstract int resumeAudio();
```

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功

**使用时机**: 无限制

**示例**:
```java
// 暂停音频流
pusher.pauseAudio();
// 恢复音频流
pusher.resumeAudio();
```

#### pauseVideo() / resumeVideo() - 暂停/恢复推流器的视频流
```java
public abstract int pauseVideo();
public abstract int resumeVideo();
```

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功

**使用时机**: 无限制

**示例**:
```java
// 暂停视频流
pusher.pauseVideo();
// 恢复视频流
pusher.resumeVideo();
```

#### setAudioQuality() - 设置推流音频质量
```java
public abstract int setAudioQuality(V2TXLiveAudioQuality quality);
```

**参数**:
- `quality`: 音频质量 `V2TXLiveDef#V2TXLiveAudioQuality`
  - `V2TXLiveAudioQualityDefault`【默认值】: 通用音质
  - `V2TXLiveAudioQualitySpeech`: 语音音质
  - `V2TXLiveAudioQualityMusic`: 音乐音质

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功
- `V2TXLIVE_ERROR_REFUSED`: 推流过程中，不允许调整音质

**使用时机**: 推流开始前

**示例**:
```java
// 设置通用音质
pusher.setAudioQuality(V2TXLiveDef.V2TXLiveAudioQuality.V2TXLiveAudioQualityDefault);
// 设置语音音质
pusher.setAudioQuality(V2TXLiveDef.V2TXLiveAudioQuality.V2TXLiveAudioQualitySpeech);
// 设置音乐音质
pusher.setAudioQuality(V2TXLiveDef.V2TXLiveAudioQuality.V2TXLiveAudioQualityMusic);
```

#### setVideoQuality() - 设置推流视频编码参数
```java
public abstract int setVideoQuality(V2TXLiveVideoEncoderParam param);
```

**参数**:
- `param`: 视频编码参数

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功

**使用时机**: 推流开始前

**示例**:
```java
V2TXLiveVideoEncoderParam param = new V2TXLiveVideoEncoderParam();
param.videoResolution = V2TXLiveVideoResolution.V2TXLiveVideoResolution1280x720;
param.videoFps = 15;
param.videoBitrate = 1200;
pusher.setVideoQuality(param);
```

### 5. 特效管理接口

#### getAudioEffectManager() - 获取音效管理对象
```java
public abstract TXAudioEffectManager getAudioEffectManager();
```

**功能说明**:
- 调整麦克风收集的人声音量
- 设置混响和变声效果
- 开启耳返，设置耳返音量
- 添加背景音乐，调整背景音乐的播放效果

**返回值**: `TXAudioEffectManager` 音效管理对象

**使用时机**: 无限制

**示例**:
```java
TXAudioEffectManager audioEffectManager = pusher.getAudioEffectManager();
// 设置人声音量
audioEffectManager.setVoiceVolume(100);
// 设置背景音乐音量
audioEffectManager.setAllMusicVolume(50);
```

#### getBeautyManager() - 获取美颜管理对象
```java
public abstract TXBeautyManager getBeautyManager();
```

**功能说明**:
- 设置"美颜风格"、美白、红润、大眼、瘦脸等美容效果
- 调整发际线、眼间距、眼角、嘴形等面部特征
- 设置人脸挂件等动态效果
- 添加美妆
- 进行手势识别

**返回值**: `TXBeautyManager` 美颜管理对象

**使用时机**: 无限制

**示例**:
```java
TXBeautyManager beautyManager = pusher.getBeautyManager();
// 设置美颜风格
beautyManager.setBeautyStyle(TXBeautyManager.TXBeautyStyleNature);
// 设置美白级别
beautyManager.setWhitenessLevel(5);
// 设置红润级别
beautyManager.setRuddyLevel(5);
```

#### getDeviceManager() - 获取设备管理对象
```java
public abstract TXDeviceManager getDeviceManager();
```

**功能说明**:
- 切换前后摄像头
- 设置自动聚焦
- 设置摄像头缩放倍数
- 打开或关闭闪光灯
- 切换耳机或者扬声器
- 修改音量类型(媒体音量或者通话音量)

**返回值**: `TXDeviceManager` 设备管理对象

**使用时机**: 无限制

**示例**:
```java
TXDeviceManager deviceManager = pusher.getDeviceManager();
// 切换摄像头
deviceManager.switchCamera(true);
// 设置自动聚焦
deviceManager.setAutoFocusEnabled(true);
// 设置闪光灯
deviceManager.enableTorch(true);
```

### 6. 高级功能接口

#### snapshot() - 截取推流过程中的本地画面
```java
public abstract int snapshot();
```

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功
- `V2TXLIVE_ERROR_REFUSED`: 已经停止推流，不允许调用截图操作

**使用时机**: 开始推流后

**示例**:
```java
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onSnapshotComplete(Bitmap image) {
        // 处理截图结果
    }
});
pusher.snapshot();
```

#### setWatermark() - 设置推流器水印
```java
public abstract int setWatermark(Bitmap image, float x, float y, float scale);
```

**参数**:
- `image`: 水印图片，如果为null则禁用水印
- `x`: 水印的横坐标，取值范围为0-1的浮点数
- `y`: 水印的纵坐标，取值范围为0-1的浮点数
- `scale`: 水印图片的缩放比例，取值范围为0-1的浮点数

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功

**使用时机**: 无限制

**示例**:
```java
Bitmap watermark = BitmapFactory.decodeResource(getResources(), R.drawable.watermark);
pusher.setWatermark(watermark, 0.1f, 0.1f, 0.2f);
// 禁用水印
pusher.setWatermark(null, 0, 0, 0);
```

#### enableVolumeEvaluation() - 启用采集音量大小提示
```java
public abstract int enableVolumeEvaluation(int intervalMs);
```

**参数**:
- `intervalMs`: 回调触发间隔，单位为ms，最小间隔为100ms，如果小于等于0则关闭回调【默认值】：0

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功

**说明**: 开启后可以在`onMicrophoneVolumeUpdate`回调中获取到SDK对音量大小值的评估

**使用时机**: 无限制

**示例**:
```java
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onMicrophoneVolumeUpdate(int volume) {
        // 处理音量更新
    }
});
pusher.enableVolumeEvaluation(300);
```

#### enableCustomVideoProcess() - 开启/关闭自定义视频处理
```java
public abstract int enableCustomVideoProcess(boolean enable, V2TXLivePixelFormat pixelFormat, V2TXLiveBufferType bufferType);
```

**参数**:
- `enable`: true开启，false关闭【默认值: false】
- `pixelFormat`: 像素格式 `V2TXLiveDef#V2TXLivePixelFormat`
- `bufferType`: 缓冲区类型 `V2TXLiveDef#V2TXLiveBufferType`

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功
- `V2TXLIVE_ERROR_NOT_SUPPORTED`: 不支持的格式

**支持的格式组合**:
- `V2TXLivePixelFormatTexture2D + V2TXLiveBufferTypeTexture`
- `V2TXLivePixelFormatI420 + V2TXLiveBufferTypeByteBuffer`

**使用时机**: 推流开始前

**示例**:
```java
pusher.enableCustomVideoProcess(true, 
    V2TXLiveDef.V2TXLivePixelFormat.V2TXLivePixelFormatTexture2D,
    V2TXLiveDef.V2TXLiveBufferType.V2TXLiveBufferTypeTexture);
```

#### enableCustomVideoCapture() - 开启/关闭自定义视频采集
```java
public abstract int enableCustomVideoCapture(boolean enable);
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
```java
// 开启自定义视频采集
pusher.enableCustomVideoCapture(true);
pusher.startPush(url);

// 发送自定义视频帧
V2TXLiveVideoFrame videoFrame = new V2TXLiveVideoFrame();
videoFrame.width = 1920;
videoFrame.height = 1080;
videoFrame.pixelFormat = V2TXLivePixelFormat.V2TXLivePixelFormatI420;
videoFrame.bufferType = V2TXLiveBufferType.V2TXLiveBufferTypeByteBuffer;
pusher.sendCustomVideoFrame(videoFrame);
```

#### enableCustomAudioCapture() - 开启/关闭自定义音频采集
```java
public abstract int enableCustomAudioCapture(boolean enable);
```

**参数**:
- `enable`: true开启自定义采集，false关闭【默认值: false】

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功

**使用场景**:
- **外部音频设备**: 连接外部麦克风、音频接口等设备
- **音频处理**: 对音频进行特殊处理后再推流
- **多路音频**: 将多路音频源合成为一路推流

**注意事项**:
- **推流前必须调用此方法开启自定义采集**，否则推流将失败
- 必须在`startPush`之前调用才会生效
- 自定义采集模式下，SDK只负责编码和发送，不进行实际采集

**使用时机**: 推流开始前

**示例**:
```java
// 开启自定义音频采集
pusher.enableCustomAudioCapture(true);
pusher.startPush(url);

// 发送自定义音频帧
V2TXLiveAudioFrame audioFrame = new V2TXLiveAudioFrame();
audioFrame.data = audioData; // PCM音频数据
audioFrame.sampleRate = 44100; // 采样率
audioFrame.channel = 1; // 声道数
pusher.sendCustomAudioFrame(audioFrame);
```

#### sendSeiMessage() - 发送SEI消息
```java
public abstract int sendSeiMessage(int payloadType, byte[] data);
```

**参数**:
- `payloadType`: 数据类型，支持5、242，推荐填242
- `data`: 待发送的数据

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功

**说明**: 播放端通过`onReceiveSeiMessage`回调来接收该消息

**使用时机**: 推流过程中

**示例**:
```java
byte[] seiData = "Hello SEI".getBytes();
pusher.sendSeiMessage(242, seiData);
```

#### startSystemAudioLoopback() / stopSystemAudioLoopback() - 打开/关闭系统声音采集
```java
public abstract int startSystemAudioLoopback();
public abstract int stopSystemAudioLoopback();
```

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功

**说明**:
- 开启后可以采集整个操作系统的播放声音，并将其混入到当前麦克风采集的声音中一起发送到云端
- 只在Android API 29及以上的版本生效
- 需要先使用该接口来开启系统声音采集，当使用屏幕分享接口开启屏幕分享时才会真正生效
- 需要添加前台服务确保系统声音采集不被静默

**使用时机**: 推流开始前

**示例**:
```java
// 开启系统声音采集
pusher.startSystemAudioLoopback();
// 停止系统声音采集
pusher.stopSystemAudioLoopback();
```

#### setMixTranscodingConfig() - 设置云端的混流转码参数
```java
public abstract int setMixTranscodingConfig(V2TXLiveTranscodingConfig config);
```

**参数**:
- `config`: 混流转码配置，传入null则取消云端混流转码

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
- 云端转码会引入1-2秒的CDN观看延时
- 及时传入null取消混流，避免不必要的计费损失

**使用时机**: 推流过程中

**示例**:
```java
V2TXLiveTranscodingConfig config = new V2TXLiveTranscodingConfig();
config.videoWidth = 1280;
config.videoHeight = 720;
config.videoBitrate = 1500;
config.videoFps = 15;
pusher.setMixTranscodingConfig(config);

// 取消混流
pusher.setMixTranscodingConfig(null);
```

#### startLocalRecording() / stopLocalRecording() - 开始/停止录制音视频流
```java
public abstract int startLocalRecording(V2TXLiveLocalRecordingParams params);
public abstract void stopLocalRecording();
```

**参数**:
- `params`: 本地录制参数

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: 参数不合法
- `V2TXLIVE_ERROR_REFUSED`: API被拒绝，推流尚未开始

**说明**: 推流开启后才能开始录制，非推流状态下开启录制无效

**使用时机**: 推流过程中

**示例**:
```java
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onLocalRecordBegin(int code, String storagePath) {
        Log.i(TAG, "开始录制");
    }

    @Override
    public void onLocalRecording(long durationMs, String storagePath) {
        Log.i(TAG, "录制中..., durationMs: " + durationMs);
    }

    @Override
    public void onLocalRecordComplete(int code, String storagePath) {
        Log.i(TAG, "录制完成");
    }
});

V2TXLiveLocalRecordingParams params = new V2TXLiveLocalRecordingParams();
params.filePath = "filepath";
params.interval = 2000;
int code = pusher.startLocalRecording(params);
if (code == V2TXLIVE_OK) {
    Log.i(TAG, "录制开启成功");
} else if (code == V2TXLIVE_ERROR_INVALID_PARAMETER) {
    Log.i(TAG, "录制参数不合法");
} else if (code == V2TXLIVE_ERROR_REFUSED) {
    Log.i(TAG, "录制调用被拒绝");
}
```

#### showDebugView() - 显示仪表盘
```java
public abstract void showDebugView(boolean isShow);
```

**参数**:
- `isShow`: 是否显示【默认值: false】

**使用时机**: 无限制

**示例**:
```java
// 显示调试视图
pusher.showDebugView(true);
// 隐藏调试视图
pusher.showDebugView(false);
```

#### setProperty() - 调用V2TXLivePusher的高级API接口
```java
public abstract int setProperty(String key, Object value);
```

**参数**:
- `key`: 高级API对应的key，详情参考`V2TXLiveProperty`定义
- `value`: 调用key所对应的高级API时需要的参数

**返回值**: `V2TXLiveCode`
- `V2TXLIVE_OK`: 成功
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: 操作失败，key不允许为空

**说明**: 该接口用于调用一些高级功能，有特殊需求，请于商务或架构师联系

**使用时机**: 无限制

**示例**:
```java
pusher.setProperty("key", "value");
```

## 使用示例

### 基础推流示例（摄像头+麦克风）
```java
// 创建推流器实例
V2TXLivePusher pusher = new V2TXLivePusherImpl(context);

// 设置回调
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onPushStatusUpdate(V2TXLiveDef.V2TXLivePushStatus status, String msg, Bundle extraInfo) {
        // 处理推流状态变化
    }
});

// 设置预览视图
pusher.setRenderView(textureView);

// 重要：推流前必须开启至少一个采集源
// 1. 开启摄像头采集（前置摄像头）
pusher.startCamera(true);

// 2. 开启麦克风采集
pusher.startMicrophone();

// 3. 开始推流（必须在采集源开启后调用）
pusher.startPush("rtmp://your-stream-url");
```

### 屏幕分享推流示例
```java
// 创建推流器实例
V2TXLivePusher pusher = new V2TXLivePusherImpl(context);

// 设置回调
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onPushStatusUpdate(V2TXLiveDef.V2TXLivePushStatus status, String msg, Bundle extraInfo) {
        // 处理推流状态变化
    }
});

// 重要：推流前必须开启至少一个采集源
// 1. 开启屏幕采集
pusher.startScreenCapture();

// 2. 开启麦克风采集（可选，如果需要声音）
pusher.startMicrophone();

// 3. 开始推流
pusher.startPush("rtmp://your-stream-url");
```

### 自定义采集示例
```java
// 创建推流器实例
V2TXLivePusher pusher = new V2TXLivePusherImpl(context);

// 设置回调
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onPushStatusUpdate(V2TXLiveDef.V2TXLivePushStatus status, String msg, Bundle extraInfo) {
        // 处理推流状态变化
    }
});

// 重要：推流前必须开启至少一个采集源
// 1. 开启自定义视频采集（必须在startPush之前调用）
pusher.enableCustomVideoCapture(true);

// 2. 开启自定义音频采集（可选，如果需要音频）
pusher.enableCustomAudioCapture(true);

// 3. 开始推流
pusher.startPush("rtmp://your-stream-url");

// 4. 在自定义采集模式下发送视频帧
V2TXLiveVideoFrame videoFrame = new V2TXLiveVideoFrame();
videoFrame.width = 1920;
videoFrame.height = 1080;
videoFrame.pixelFormat = V2TXLivePixelFormat.V2TXLivePixelFormatI420;
videoFrame.bufferType = V2TXLiveBufferType.V2TXLiveBufferTypeByteBuffer;
pusher.sendCustomVideoFrame(videoFrame);
```

## 注意事项

### 1. 采集源要求（重要）
**推流前必须开启至少一个采集源**，否则推流将失败：
- **摄像头采集**：`startCamera()` + `startMicrophone()`
- **屏幕采集**：`startScreenCapture()` + `startMicrophone()`
- **图片推流**：`startVirtualCamera()` + `startMicrophone()`
- **自定义采集**：`enableCustomVideoCapture()` + `enableCustomAudioCapture()`
- **纯音频推流**：`startMicrophone()`

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
- **协议限制**：云端混流功能仅支持RTC协议，不支持RTMP等其他推流协议
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
