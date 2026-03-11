> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

# 腾讯云直播SDK V2TXLivePusherObserver 直播推流器回调接口

## 概述

`V2TXLivePusherObserver` 是腾讯云直播SDK的推流器回调接口，用于接收推流器的各种状态通知和事件回调。通过实现该接口的回调方法，开发者可以监控推流器的运行状态、处理推流事件、获取统计数据等。

**文件路径**: `com/tencent/live2/V2TXLivePusherObserver.java`

**主要功能**:
- 推流器状态监控（错误、警告、连接状态）
- 音视频采集事件回调
- 推流统计数据和性能指标
- 自定义音视频处理
- 本地录制任务管理
- 屏幕分享状态监控
- 云端混流转码回调

## 回调方法详解

### 1. 错误和警告回调

#### onError() - 推流器错误通知
```java
public void onError(int code, String msg, Bundle extraInfo)
```

**功能**: 推流器出现错误时回调

**参数**:
- `code`: 错误码，参考 `V2TXLiveCode` 枚举
- `msg`: 错误描述信息
- `extraInfo`: 扩展信息，包含详细的错误上下文

**使用场景**:
- 网络连接失败
- 推流地址无效
- 编码器错误
- 推流权限问题

**示例**:
```java
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onError(int code, String msg, Bundle extraInfo) {
        switch (code) {
            case V2TXLIVE_ERROR_REQUEST_TIMEOUT:
                Log.e(TAG, "推流连接超时");
                break;
            case V2TXLIVE_ERROR_SERVER_PROCESS_FAILED:
                Log.e(TAG, "推流服务器处理失败");
                break;
            default:
                Log.e(TAG, "其它错误: " + msg);
                break;
        }
    }
});
```

#### onWarning() - 推流器警告通知
```java
public void onWarning(int code, String msg, Bundle extraInfo)
```

**功能**: 推流器出现警告时回调

**参数**:
- `code`: 警告码，参考 `V2TXLiveCode` 枚举
- `msg`: 警告描述信息
- `extraInfo`: 扩展信息

**使用场景**:
- 网络质量下降
- 编码延迟
- 缓冲区不足

**示例**:
```java
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onWarning(int code, String msg, Bundle extraInfo) {
        switch (code) {
            case V2TXLiveCode.V2TXLIVE_WARNING_CURRENT_ENCODE_TYPE_CHANGED:
                int codec_type = extraInfo.getInt("codec_type");
                if (codec_type == 0) {
                    Log.w(TAG, "编码器类型变更，h.264, " + msg);
                } else if (codec_type == 1) {
                    Log.w(TAG, "编码器类型变更，h.265, " + msg);
                }
                break;
            case V2TXLiveCode.V2TXLIVE_WARNING_NETWORK_BUSY:
                Log.w(TAG, "网络繁忙，" + msg);
                break;
            case V2TXLiveCode.V2TXLIVE_WARNING_CAMERA_START_FAILED:
                Log.w(TAG, "摄像头启动失败，" + msg);
                break;
            case V2TXLiveCode.V2TXLIVE_WARNING_CAMERA_NO_PERMISSION:
                Log.w(TAG, "摄像头设备未授权，" + msg);
                break;
            case V2TXLiveCode.V2TXLIVE_WARNING_CAMERA_OCCUPIED:
                Log.w(TAG, "摄像头设备被占用，" + msg);
                break;
            case V2TXLIVE_WARNING_SCREEN_CAPTURE_START_FAILED:
                Log.w(TAG, "屏幕采集启动失败，" + msg);
                break;
            case V2TXLIVE_WARNING_SCREEN_CAPTURE_NOT_SUPPORTED:
                Log.w(TAG, "屏幕采集不支持，" + msg);
                break;
            case V2TXLIVE_WARNING_SCREEN_CAPTURE_INTERRUPTED:
                Log.w(TAG, "屏幕采集中断，" + msg);
                break;
            case V2TXLIVE_WARNING_MICROPHONE_START_FAILED:
                Log.w(TAG, "麦克风启动失败，" + msg);
                break;
            case V2TXLIVE_WARNING_MICROPHONE_NO_PERMISSION:
                Log.w(TAG, "麦克风未授权，" + msg);
                break;
            case V2TXLIVE_WARNING_MICROPHONE_OCCUPIED:
                Log.w(TAG, "麦克风被占用，" + msg);
                break;
            default:
                Log.w(TAG, "其他警告，" + msg);
                break;
        }
    }
});
```

### 2. 连接和状态回调

#### onPushStatusUpdate() - 推流器连接状态回调
```java
public void onPushStatusUpdate(V2TXLivePushStatus status, String msg, Bundle extraInfo)
```

**功能**: 推流器连接状态回调通知

**参数**:
- `status`: 推流器连接状态 `V2TXLivePushStatus`
- `msg`: 连接状态信息
- `extraInfo`: 扩展信息

**状态枚举**:
- `V2TXLivePushStatus.V2TXLivePushStatusDisconnected`: 断开连接
- `V2TXLivePushStatus.V2TXLivePushStatusConnecting`: 连接中
- `V2TXLivePushStatus.V2TXLivePushStatusConnectSuccess`: 连接成功
- `V2TXLivePushStatus.V2TXLivePushStatusReconnecting`: 重连中

**使用场景**:
- 推流状态实时监控
- 连接失败重试机制
- 用户界面状态更新

**示例**:
```java
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onPushStatusUpdate(V2TXLivePushStatus status, String msg, Bundle extraInfo) {
        switch (status) {
            case V2TXLivePushStatusConnectSuccess:
                Log.i(TAG, "推流连接成功");
                break;
            case V2TXLivePushStatusConnecting:
                Log.i(TAG, "推流连接中...");
                break;
            case V2TXLivePushStatusReconnecting:
                Log.w(TAG, "推流重连中...");
                break;
            case V2TXLivePushStatusDisconnected:
                Log.e(TAG, "推流连接断开");
                break;
        }
    }
});
```

### 3. 采集事件回调

#### onCaptureFirstAudioFrame() - 首帧音频采集完成
```java
public void onCaptureFirstAudioFrame()
```

**功能**: 首帧音频采集完成的回调通知

**使用场景**:
- 确认音频采集已开始
- 音频相关UI状态更新
- 音频处理初始化

**示例**:
```java
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onCaptureFirstAudioFrame() {
        Log.i(TAG, "音频采集开始，首帧音频已采集");
        // 更新UI状态，显示音频采集中
    }
});
```

#### onCaptureFirstVideoFrame() - 首帧视频采集完成
```java
public void onCaptureFirstVideoFrame()
```

**功能**: 首帧视频采集完成的回调通知

**使用场景**:
- 确认视频采集已开始
- 视频相关UI状态更新
- 视频处理初始化

**示例**:
```java
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onCaptureFirstVideoFrame() {
        Log.i(TAG, "视频采集开始，首帧视频已采集");
        // 更新UI状态，显示视频采集中
    }
});
```

#### onMicrophoneVolumeUpdate() - 麦克风采集音量回调
```java
public void onMicrophoneVolumeUpdate(int volume)
```

**功能**: 麦克风采集音量值回调

**参数**:
- `volume`: 音量大小（0-100）

**前提条件**: 需要调用 `enableVolumeEvaluation()` 开启采集音量大小提示

**使用场景**:
- 实时音量显示
- 音频波形动画
- 静音检测

**示例**:
```java
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onMicrophoneVolumeUpdate(int volume) {
        // 实时更新音量显示
        
        // 静音检测
        if (volume < 5) {
            Log.d(TAG, "检测到静音状态");
        }
    }
});
// 开启音量评估
pusher.enableVolumeEvaluation(300);
```

### 4. 音视频数据处理回调

#### onProcessAudioFrame() - 音频数据处理回调
```java
public void onProcessAudioFrame(V2TXLiveDef.V2TXLiveAudioFrame frame)
```

**功能**: 本地采集并经过音频模块前处理、音效处理和混BGM后的音频数据回调

**参数**:
- `frame`: PCM格式的音频数据帧

**技术规格**:
- 音频时间帧长固定为0.02s
- 格式为PCM格式
- 字节帧长计算公式：`采样率 × 时间帧长 × 声道数 × 采样点位宽`
- 默认格式（48000采样率、单声道、16采样点位宽）：1920字节

**重要注意事项**:
1. 不要在此回调函数中做任何耗时操作
2. SDK每隔20ms处理一帧音频数据，处理时间超过20ms会导致声音异常
3. 音频数据可读写，可同步修改但需保证处理耗时

**使用场景**:
- 自定义音频处理
- 音频特效应用
- 音频分析统计

**示例**:
```java
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onProcessAudioFrame(V2TXLiveDef.V2TXLiveAudioFrame frame) {
        // 自定义音频处理，如添加混响效果
        
        // 音频数据统计
        audioFrameCount++;
        if (audioFrameCount % 50 == 0) {
            Log.d(TAG, "已处理音频帧数: " + audioFrameCount);
        }
    }
});
```

#### onProcessVideoFrame() - 自定义视频处理回调
```java
public int onProcessVideoFrame(V2TXLiveVideoFrame srcFrame, V2TXLiveVideoFrame dstFrame)
```

**功能**: 自定义视频处理回调

**参数**:
- `srcFrame`: 用于承载未处理的视频画面
- `dstFrame`: 用于承载处理过的视频画面

**返回值**: 处理结果（0表示成功）

**前提条件**: 需要调用 `enableCustomVideoProcess()` 开启自定义视频处理

**使用场景示例**:

**情况一：美颜组件产生新纹理**
```java
@Override
public void onGLContextCreated() {
    mFURenderer.onSurfaceCreated();
    mFURenderer.setUseTexAsync(true);
}

@Override
public int onProcessVideoFrame(V2TXLiveVideoFrame srcFrame, V2TXLiveVideoFrame dstFrame) {
    dstFrame.texture.textureId = mFURenderer.onDrawFrameSingleInput(
                        srcFrame.texture.textureId, srcFrame.width, srcFrame.height);
    return 0;
}

@Override
public void onGLContextDestroyed() {
    mFURenderer.onSurfaceDestroyed();
}
```

**情况二：美颜组件不产生新纹理**
```java
int onProcessVideoFrame(V2TXLiveVideoFrame srcFrame, V2TXLiveVideoFrame dstFrame) {
    thirdparty_process(srcFrame.texture.textureId, srcFrame.width, srcFrame.height, dstFrame.texture.textureId);
    return 0;
}
```

### 5. OpenGL环境回调

#### onGLContextCreated() - OpenGL环境创建通知
```java
public void onGLContextCreated()
```

**功能**: SDK内部的OpenGL环境的创建通知

**使用场景**:
- 美颜组件初始化
- 视频处理模块初始化
- OpenGL资源创建

**示例**:
```java
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onGLContextCreated() {
        Log.i(TAG, "OpenGL环境已创建");
        // 初始化美颜组件
        if (mBeautyProcessor != null) {
            mBeautyProcessor.initGL();
        }
    }
});
```

#### onGLContextDestroyed() - OpenGL环境销毁通知
```java
public void onGLContextDestroyed()
```

**功能**: SDK内部的OpenGL环境的销毁通知

**使用场景**:
- 美颜组件清理
- 视频处理模块清理
- OpenGL资源释放

**示例**:
```java
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onGLContextDestroyed() {
        Log.i(TAG, "OpenGL环境已销毁");
        // 清理美颜组件资源
        if (mBeautyProcessor != null) {
            mBeautyProcessor.releaseGL();
        }
    }
});
```

### 6. 统计和监控回调

#### onStatisticsUpdate() - 统计数据回调
```java
public void onStatisticsUpdate(V2TXLivePusherStatistics statistics)
```

**功能**: 推流器统计数据实时回调，2s回调一次

**参数**:
- `statistics`: 推流统计信息 `V2TXLivePusherStatistics`

**包含数据**:
- 视频宽度/高度
- 帧率/码率
- 网络状况
- 缓存大小
- 推流延迟

**使用场景**:
- 推流质量监控
- 性能优化分析
- 用户体验统计

**示例**:
```java
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onStatisticsUpdate(V2TXLivePusherStatistics statistics) {
        Log.d(TAG, "推流统计 - 帧率: " + statistics.fps + 
                  ", 码率: " + statistics.videoBitrate + 
                  ", 分辨率: " + statistics.width + "x" + statistics.height);
        
        // 更新推流质量显示
    }
});
```

### 7. 高级功能回调

#### onSnapshotComplete() - 截图完成回调
```java
public void onSnapshotComplete(Bitmap image)
```

**功能**: 截图操作完成回调

**参数**:
- `image`: 截取的视频画面Bitmap

**使用场景**:
- 视频截图保存
- 画面分享功能
- 证据保存

**示例**:
```java
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onSnapshotComplete(Bitmap image) {
        Log.i(TAG, "截图完成，图片尺寸: " + image.getWidth() + "x" + image.getHeight());
        
        // 保存截图到相册
        
        // 显示截图预览
    }
});

// 触发截图
pusher.snapshot();
```

#### onSetMixTranscodingConfig() - 云端混流转码回调
```java
public void onSetMixTranscodingConfig(int code, String msg)
```

**功能**: 设置云端的混流转码参数的回调，仅RTC协议支持

**参数**:
- `code`: 0表示成功，其余值表示失败
- `msg`: 具体错误原因

**对应接口**: `setMixTranscodingConfig()`

**使用场景**:
- 混流转码状态监控
- 转码失败处理
- 多路流合成状态跟踪

**示例**:
```java
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onSetMixTranscodingConfig(int code, String msg) {
        if (code == 0) {
            Log.i(TAG, "云端混流转码配置成功");
        } else {
            Log.e(TAG, "云端混流转码配置失败: " + msg);
        }
    }
});

// 配置云端混流
V2TXLiveDef.V2TXLiveTranscodingConfig config = new V2TXLiveDef.V2TXLiveTranscodingConfig();
// ... 配置混流参数
pusher.setMixTranscodingConfig(config);
```

#### onVoiceActivityDetectionUpdate() - 人声检测回调
```java
public void onVoiceActivityDetectionUpdate(boolean active)
```

**功能**: 人声检测状态更新回调

**参数**:
- `active`: 人声开始或停止

**前提条件**: 调用 `enableVoiceActivityDetection()` 开启人声检测

**使用场景**:
- 语音活动检测
- 智能静音处理
- 语音识别应用

**示例**:
```java
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onVoiceActivityDetectionUpdate(boolean active) {
        if (active) {
            Log.i(TAG, "检测到人声活动开始");
            // 显示说话状态指示器
            showSpeakingIndicator(true);
        } else {
            Log.i(TAG, "检测到人声活动停止");
            // 隐藏说话状态指示器
            showSpeakingIndicator(false);
        }
    }
});

// 开启人声检测
pusher.enableVoiceActivityDetection(true);
```

### 8. 屏幕分享回调

#### onScreenCaptureStarted() - 屏幕分享开始回调
```java
public void onScreenCaptureStarted()
```

**功能**: 当屏幕分享开始时，SDK会通过此回调通知

**使用场景**:
- 屏幕分享状态监控
- UI状态更新
- 权限检查确认

**示例**:
```java
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onScreenCaptureStarted() {
        Log.i(TAG, "屏幕分享已开始");
        // 更新UI显示屏幕分享状态
        updateScreenShareStatus(true);
    }
});
```

#### onScreenCaptureStopped() - 屏幕分享停止回调
```java
public void onScreenCaptureStopped(int reason)
```

**功能**: 当屏幕分享停止时，SDK会通过此回调通知

**参数**:
- `reason`: 停止原因
  - `0`: 用户主动停止
  - `1`: iOS表示录屏被系统中断；Mac、Windows表示屏幕分享窗口被关闭
  - `2`: Windows表示屏幕分享的显示屏状态变更；其他平台不抛出

**使用场景**:
- 屏幕分享异常处理
- 用户界面状态恢复
- 权限丢失处理

**示例**:
```java
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onScreenCaptureStopped(int reason) {
        Log.i(TAG, "屏幕分享已停止，原因: " + reason);
        
        switch (reason) {
            case 0:
                Log.i(TAG, "用户主动停止屏幕分享");
                break;
            case 1:
                Log.w(TAG, "屏幕分享被系统中断");
                break;
            case 2:
                Log.w(TAG, "显示屏状态变更导致屏幕分享停止");
                break;
        }
        
        // 更新UI显示屏幕分享状态
        updateScreenShareStatus(false);
    }
});
```

### 9. 本地录制回调

#### onLocalRecordBegin() - 录制开始回调
```java
public void onLocalRecordBegin(int code, String storagePath)
```

**功能**: 录制任务开始的事件回调

**参数**:
- `code`: 状态码
  - `0`: 录制任务启动成功
  - `-1`: 内部错误导致录制任务启动失败
  - `-2`: 文件后缀名有误
  - `-6`: 录制已经启动，需要先停止录制
  - `-7`: 录制文件已存在，需要先删除文件
  - `-8`: 录制目录无写入权限
- `storagePath`: 录制的文件地址

**对应接口**: `startLocalRecording()`

**示例**:
```java
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onLocalRecordBegin(int code, String storagePath) {
        if (code == 0) {
            Log.i(TAG, "本地录制开始，文件路径: " + storagePath);
            // 显示录制状态
            showRecordingStatus(true);
        } else {
            Log.e(TAG, "本地录制开始失败，错误码: " + code);
            // 处理录制失败情况
            handleRecordingError(code);
        }
    }
});
```

#### onLocalRecording() - 录制进度回调
```java
public void onLocalRecording(long durationMs, String storagePath)
```

**功能**: 录制任务正在进行中的进展事件回调

**参数**:
- `durationMs`: 录制时长
- `storagePath`: 录制的文件地址

**默认行为**: 不抛出本事件回调，需要在 `startLocalRecording()` 时设定回调间隔参数

**使用场景**:
- 录制进度显示
- 录制时长限制
- 录制状态监控

**示例**:
```java
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onLocalRecording(long durationMs, String storagePath) {
        // 更新录制进度显示
        updateRecordingProgress(durationMs);
        
        // 录制时长限制检查（例如限制录制1小时）
        if (durationMs >= 3600000) {
            Log.w(TAG, "录制时长已达限制，自动停止录制");
            pusher.stopLocalRecording();
        }
    }
});
```

#### onLocalRecordComplete() - 录制完成回调
```java
public void onLocalRecordComplete(int code, String storagePath)
```

**功能**: 录制任务已经结束的事件回调

**参数**:
- `code`: 状态码
  - `0`: 结束录制任务成功
  - `-1`: 录制失败
  - `-2`: 切换分辨率或横竖屏导致录制结束
  - `-3`: 录制时间太短，或未采集到任何视频或音频数据
- `storagePath`: 录制的文件地址

**对应接口**: `stopLocalRecording()`

**示例**:
```java
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onLocalRecordComplete(int code, String storagePath) {
        if (code == 0) {
            Log.i(TAG, "本地录制完成，文件路径: " + storagePath);
            // 显示录制完成状态
            showRecordingComplete(storagePath);
        } else {
            Log.w(TAG, "本地录制异常结束，状态码: " + code);
            // 处理录制异常结束
            handleRecordingAbnormalEnd(code);
        }
    }
});
```

## 使用示例

### 基础推流器回调实现
```java
public class MyPusherObserver extends V2TXLivePusherObserver {
    @Override
    public void onError(int code, String msg, Bundle extraInfo) {
        // 处理推流错误
        Log.e("PusherError", "错误码: " + code + ", 错误信息: " + msg);
    }
    
    @Override
    public void onPushStatusUpdate(V2TXLivePushStatus status, String msg, Bundle extraInfo) {
        // 推流状态监控
        switch (status) {
            case CONNECT_SUCCESS:
                Log.i("Pusher", "推流连接成功");
                break;
            case DISCONNECTED:
                Log.w("Pusher", "推流连接断开");
                break;
        }
    }
    
    @Override
    public void onCaptureFirstVideoFrame() {
        // 视频采集开始
        Log.i("Pusher", "视频采集开始");
    }
    
    @Override
    public void onStatisticsUpdate(V2TXLivePusherStatistics statistics) {
        // 更新推流统计信息
        Log.d("PusherStats", "帧率: " + statistics.fps + ", 码率: " + statistics.bitrate);
    }
}

// 设置回调观察者
V2TXLivePusher pusher = new V2TXLivePusherImpl(context);
pusher.setObserver(new MyPusherObserver());
```

### 自定义视频处理示例
```java
public class VideoProcessorObserver extends V2TXLivePusherObserver {
    private BeautyProcessor mBeautyProcessor;
    
    @Override
    public void onGLContextCreated() {
        // OpenGL环境创建时初始化美颜组件
        mBeautyProcessor = new BeautyProcessor();
        mBeautyProcessor.init();
    }
    
    @Override
    public int onProcessVideoFrame(V2TXLiveVideoFrame srcFrame, V2TXLiveVideoFrame dstFrame) {
        // 自定义视频帧处理（美颜、滤镜等）
        if (mBeautyProcessor != null) {
            return mBeautyProcessor.processFrame(srcFrame, dstFrame);
        }
        return 0;
    }
    
    @Override
    public void onGLContextDestroyed() {
        // OpenGL环境销毁时清理资源
        if (mBeautyProcessor != null) {
            mBeautyProcessor.release();
            mBeautyProcessor = null;
        }
    }
}

// 开启自定义视频处理
pusher.enableCustomVideoProcess(true);
pusher.setObserver(new VideoProcessorObserver());
```

### 本地录制监控示例
```java
public class RecordingObserver extends V2TXLivePusherObserver {
    @Override
    public void onLocalRecordBegin(int code, String storagePath) {
        if (code == 0) {
            Log.i("Recording", "录制开始，文件路径: " + storagePath);
        } else {
            Log.e("Recording", "录制失败，错误码: " + code);
        }
    }
    
    @Override
    public void onLocalRecording(long durationMs, String storagePath) {
        // 更新录制进度
        updateRecordingProgress(durationMs);
    }
    
    @Override
    public void onLocalRecordComplete(int code, String storagePath) {
        if (code == 0) {
            Log.i("Recording", "录制完成，文件路径: " + storagePath);
        } else {
            Log.w("Recording", "录制异常结束，状态码: " + code);
        }
    }
}
```

## 注意事项

1. **回调线程**: 除自定义预处理回调，其它所有回调方法都在非UI线程执行，需要进行线程安全处理
2. **性能影响**: 自定义音视频处理回调可能影响推流性能，需控制处理耗时
3. **内存管理**: 及时释放不再使用的观察者对象，避免内存泄漏
4. **错误处理**: 合理处理各种错误码，提供友好的用户提示
5. **权限检查**: 屏幕分享和本地录制需要确保有相应权限
6. **OpenGL资源**: 自定义视频处理时注意OpenGL资源的创建和销毁时机

## 相关接口

- `V2TXLivePusher`: 推流器主接口
- `V2TXLiveCode`: 错误码和状态码定义
- `V2TXLiveDef`: 数据结构和枚举定义
- `V2TXLivePremier`: SDK全局管理接口