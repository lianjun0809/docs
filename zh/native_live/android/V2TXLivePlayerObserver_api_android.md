> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

# 腾讯云直播SDK V2TXLivePlayerObserver 直播播放器回调接口

## 概述

`V2TXLivePlayerObserver` 是腾讯云直播SDK的播放器回调接口，用于接收播放器的各种状态通知和事件回调。通过实现该接口的回调方法，开发者可以监控播放器的运行状态、处理播放事件、获取统计数据等。

**文件路径**: `com/tencent/live2/V2TXLivePlayerObserver.java`

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
```java
public void onError(V2TXLivePlayer player, int code, String msg, Bundle extraInfo)
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
```java
player.setObserver(new V2TXLivePlayerObserver() {
    @Override
    public void onError(V2TXLivePlayer player, int code, String msg, Bundle extraInfo) {
        switch (code) {
            case V2TXLIVE_ERROR_INVALID_PARAMETER:
                Log.e(TAG, "rtc拉流参数不合法，" + msg);
                break;
            case V2TXLIVE_ERROR_REQUEST_TIMEOUT:
                Log.e(TAG, "rtc拉流超时，" + msg);
                break;
            case V2TXLIVE_ERROR_SERVER_PROCESS_FAILED:
                Log.e(TAG, "rtc拉流服务器处理失败，请检查拉流参数，" + msg);
                break;
            case V2TXLIVE_ERROR_DISCONNECTED:
                Log.e(TAG, "拉流断开，" + msg);
                break;
            case V2TXLIVE_ERROR_NO_AVAILABLE_HEVC_DECODERS:
                Log.e(TAG, "找不到hevc解码器，可以切换到avc流进行播放，" + msg);
                break;
            default:
                Log.e(TAG, "其它错误，" + msg);
                break;
        }
    }
});
```

#### onWarning() - 播放器警告通知
```java
public void onWarning(V2TXLivePlayer player, int code, String msg, Bundle extraInfo)
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
```java
player.setObserver(new V2TXLivePlayerObserver() {
    @Override
    public void onWarning(V2TXLivePlayer player, int code, String msg, Bundle extraInfo) {
        switch (code) {
            case V2TXLIVE_WARNING_VIDEO_BLOCK:
                Log.w(TAG, "视频渲染发生卡顿");
                break;
            case V2TXLIVE_WARNING_CURRENT_DECODE_TYPE_CHANGED:
                int codec_type = extraInfo.getInt("codec_type");
                if (codec_type == 0) {
                    Log.w(TAG, "解码器类型变更，h.264，" + msg);
                } else if (codec_type == 1) {
                    Log.w(TAG, "解码器类型变更，h.265，" + msg);
                }
                break;
            default:
                Log.w(TAG, "其它警告，" + msg);
                break;
        }
    }
});
```

### 2. 连接和状态回调

#### onConnected() - 网络连接成功回调
```java
public void onConnected(V2TXLivePlayer player, Bundle extraInfo)
```

**功能**: 播放器成功连接到服务器时回调

**参数**:
- `player`: 触发回调的播放器实例
- `extraInfo`: 连接相关信息

**使用场景**:
- 监控播放器网络连接状态

**示例**:
```java
player.setObserver(new V2TXLivePlayerObserver() {
    @Override
    public void onConnected(V2TXLivePlayer player, Bundle extraInfo) {
        Log.i(TAG, "服务器连接成功");
    }
});
```


#### onVideoResolutionChanged() - 视频分辨率变化回调
```java
public void onVideoResolutionChanged(V2TXLivePlayer player, int width, int height)
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
```java
player.setObserver(new V2TXLivePlayerObserver() {
    @Override
    public void onVideoResolutionChanged(V2TXLivePlayer player, int width, int height) {
        Log.i(TAG, "视频流分辨率发生变化: width-" + width + ", height-" + height);
    }
});
```

### 3. 播放事件回调

#### onVideoPlaying() - 视频开始播放事件
```java
public void onVideoPlaying(V2TXLivePlayer player, boolean firstPlay, Bundle extraInfo)
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
```java
player.setObserver(new V2TXLivePlayerObserver() {
    @Override
    public void onVideoPlaying(V2TXLivePlayer player, boolean firstPlay, Bundle extraInfo) {
        if (firstPlay) {
            // 视频首次开始播放
            Log.i(TAG, "首次开始播放");
        } else {
            // 视频非首次开始播放，可以隐藏加载 UI
            Log.i(TAG, "开始播放");
        }
    }
});
```


#### onVideoLoading() - 视频开始加载事件
```java
public void onVideoLoading(V2TXLivePlayer player, Bundle extraInfo)
```

**功能**: 视频数据加载时回调

**参数**:
- `player`: 触发回调的播放器实例
- `extraInfo`: 加载状态信息

**使用场景**:
- 显示加载动画
- 缓冲状态提示

**示例**:
```java
player.setObserver(new V2TXLivePlayerObserver() {
    @Override
    public void onVideoLoading(V2TXLivePlayer player, Bundle extraInfo) {
        // 视频播放开始加载，可以显示加载 UI
        Log.i(TAG, "视频播放开始加载");
    }
});
```

#### onAudioPlaying() - 音频开始播放事件
```java
public void onAudioPlaying(V2TXLivePlayer player, boolean firstPlay, Bundle extraInfo)
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
```java
player.setObserver(new V2TXLivePlayerObserver() {
    @Override
    public void onAudioPlaying(V2TXLivePlayer player, boolean firstPlay, Bundle extraInfo) {
        if (firstPlay) {
            Log.i(TAG, "音频首次开始播放");
        } else {
            Log.i(TAG, "音频开始播放");
        }
    }
});
```

#### onAudioLoading() - 音频开始加载事件
```java
public void onAudioLoading(V2TXLivePlayer player, Bundle extraInfo)
```

**功能**: 音频数据加载时回调

**参数**:
- `player`: 触发回调的播放器实例
- `extraInfo`: 加载状态信息

**使用场景**:
- 显示加载动画
- 缓冲状态提示

**示例**:
```java
player.setObserver(new V2TXLivePlayerObserver() {
    @Override
    public void onAudioLoading(V2TXLivePlayer player, Bundle extraInfo) {
        // 音频播放开始加载
        Log.i(TAG, "音频播放开始加载");
    }
});
```


### 4. 音视频数据处理回调

#### onPlayoutVolumeUpdate() - 音量更新回调
```java
public void onPlayoutVolumeUpdate(V2TXLivePlayer player, int volume)
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
```java
player.setObserver(new V2TXLivePlayerObserver() {
    @Override
    public void onPlayoutVolumeUpdate(V2TXLivePlayer player, int volume) {
        // 音频播放音量回调，可以更新音量大小
        Log.i(TAG, "音频播放音量，音量：" + volume);
    }
});
player.enableVolumeEvaluation(300);
```


#### onRenderVideoFrame() - 自定义视频渲染回调
```java
public void onRenderVideoFrame(V2TXLivePlayer player, V2TXLiveVideoFrame videoFrame)
```

**功能**: 自定义视频帧渲染回调

**参数**:
- `player`: 触发回调的播放器实例
- `videoFrame`: 视频帧数据 `V2TXLiveVideoFrame`

**前提条件**: 需要调用 `enableObserveVideoFrame()` 开启视频帧回调

**使用场景**:
- 自定义视频渲染

**示例**:
```java
// 开启自定义渲染
player.enableObserveVideoFrame(true, V2TXLiveDef.V2TXLivePixelFormat.V2TXLivePixelFormatTexture2D, V2TXLiveDef.V2TXLiveBufferType.V2TXLiveBufferTypeTexture);
player.setObserver(new V2TXLivePlayerObserver() {
    @Override
    public void onRenderVideoFrame(V2TXLivePlayer player, V2TXLiveVideoFrame videoFrame) {
        // 自定义渲染
    }
});
```


#### onPlayoutAudioFrame() - 音频数据回调
```java
public void onPlayoutAudioFrame(V2TXLivePlayer player, V2TXLiveAudioFrame audioFrame)
```

**功能**: 音频数据播放回调

**参数**:
- `player`: 触发回调的播放器实例
- `audioFrame`: 音频帧数据 `V2TXLiveAudioFrame`

**前提条件**: 需要调用 `enableObserveAudioFrame()` 开启音频帧回调

**使用场景**:
- 自定义音频处理

**示例**:
```java
// 开启音频数据监听
player.enableObserveAudioFrame(true);
player.setObserver(new V2TXLivePlayerObserver() {
    @Override
    public void onPlayoutAudioFrame(V2TXLivePlayer player, V2TXLiveAudioFrame audioFrame) {
        // doSomething
    }
});
```

### 5. 统计和监控回调

#### onStatisticsUpdate() - 统计数据回调
```java
public void onStatisticsUpdate(V2TXLivePlayer player, V2TXLivePlayerStatistics statistics)
```

**功能**: 播放器统计数据实时回调，2s回调一次

**参数**:
- `player`: 触发回调的播放器实例
- `statistics`: 播放统计信息 `V2TXLivePlayerStatistics`

**包含数据**:
- 视频宽度/高度
- 帧率/码率
- 网络状况
- 缓存大小
- 播放延迟

**使用场景**:
- 播放质量监控
- 性能优化分析
- 用户体验统计

**示例**:
```java
player.setObserver(new V2TXLivePlayerObserver() {
    @Override
    public void onStatisticsUpdate(V2TXLivePlayer player, V2TXLivePlayerStatistics statistics) {
        // doSomething
    }
});
```

### 6. 高级功能回调

#### onSnapshotComplete() - 截图完成回调
```java
public void onSnapshotComplete(V2TXLivePlayer player, Bitmap image)
```

**功能**: 截图操作完成回调

**参数**:
- `player`: 触发回调的播放器实例
- `image`: 截取的视频画面Bitmap

**使用场景**:
- 视频截图保存
- 画面分享功能

**示例**:
```java
player.setObserver(new V2TXLivePlayerObserver() {
    @Override
    public void onSnapshotComplete(V2TXLivePlayer player, Bitmap image) {
        // doSomething
    }
});
player.snapshot();
```

#### onReceiveSeiMessage() - SEI消息接收回调
```java
public void onReceiveSeiMessage(V2TXLivePlayer player, int payloadType, byte[] data)
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

**示例**:
```java
// 开启音频数据监听
player.enableReceiveSeiMessage(true, 5);
player.enableReceiveSeiMessage(true, 242);
player.enableReceiveSeiMessage(true, 243);
player.setObserver(new V2TXLivePlayerObserver() {
    @Override
    public void onReceiveSeiMessage(V2TXLivePlayer player, int payloadType, byte[] data) {
        // doSomething
    }
});
```

#### onStreamSwitched() - 流切换回调
```java
public void onStreamSwitched(V2TXLivePlayer player, String url, int code)
```

**功能**: 分辨率切换操作完成回调，调用 `switchStream()` 时回调

**参数**:
- `player`: 触发回调的播放器实例
- `url`: 切换后的播放地址
- `code`: 切换状态码（0:成功，-1:超时，-2:服务端错误，-3:客户端错误）

**使用场景**:
- 清晰度切换监控

**示例**:
```java
player.startLivePlayer("http://example.com/live/stream_1080p.flv");

player.setObserver(new V2TXLivePlayerObserver() {
    @Override
    public void onStreamSwitched(V2TXLivePlayer player, String url, int code) {
        if (code == 0) {
            Log.i(TAG, "切换成功");
        } else if (code == -1) {
            Log.i(TAG, "切换超时");
        } else if (code == -2) {
            Log.i(TAG, "切换失败，服务端错误");
        } else if (code == -3) {
            Log.i(TAG, "切换失败，客户端错误");
        }
    }
});
player.switchStream("http://example.com/live/stream_720p.flv";
```

### 7. 本地录制回调

#### onLocalRecordBegin() - 录制开始回调
```java
public void onLocalRecordBegin(V2TXLivePlayer player, int code, String storagePath)
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
```java
public void onLocalRecording(V2TXLivePlayer player, long durationMs, String storagePath)
```

**功能**: 录制任务进行中进度回调，频率与 startLocalRecording 传入的 V2TXLiveDef.V2TXLiveLocalRecordingParams.interval 一致

**参数**:
- `player`: 触发回调的播放器实例
- `durationMs`: 已录制时长（毫秒）
- `storagePath`: 录制文件存储路径

**使用场景**:
- 录制进度显示
- 录制时长限制
- 录制状态监控

#### onLocalRecordComplete() - 录制完成回调
```java
public void onLocalRecordComplete(V2TXLivePlayer player, int code, String storagePath)
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
```java
player.setObserver(new V2TXLivePlayerObserver() {
    @Override
    public void onLocalRecordBegin(V2TXLivePlayer player, int code, String storagePath) {
        Log.i(TAG, "开始录制");
    }

    @Override
    public void onLocalRecording(V2TXLivePlayer player, long durationMs, String storagePath) {
        Log.i(TAG, "录制中..., durationMs: " + durationMs);
    }

    @Override
    public void onLocalRecordComplete(V2TXLivePlayer player, int code, String storagePath) {
        Log.i(TAG, "录制完成");
    }
});

V2TXLiveDef.V2TXLiveLocalRecordingParams params = new V2TXLiveDef.V2TXLiveLocalRecordingParams();
params.filePath = "filepath";
params.interval = 2000;
int code = player.startLocalRecording(params);
if (code == V2TXLIVE_OK) {
    Log.i(TAG, "录制开启成功");
} else if (code == V2TXLIVE_ERROR_INVALID_PARAMETER) {
    Log.i(TAG, "录制参数不合法");
} else if (code == V2TXLIVE_ERROR_REFUSED) {
    Log.i(TAG, "录制调用被拒绝");
}
```


### 基础播放器回调实现
```java
public class MyPlayerObserver extends V2TXLivePlayerObserver {
    @Override
    public void onError(V2TXLivePlayer player, int code, String msg, Bundle extraInfo) {
        // 处理播放错误
        Log.e("PlayerError", "错误码: " + code + ", 错误信息: " + msg);
    }
    
    @Override
    public void onConnected(V2TXLivePlayer player, Bundle extraInfo) {
        // 连接成功处理
        Log.i("Player", "成功连接到服务器");
    }
    
    @Override
    public void onVideoPlaying(V2TXLivePlayer player, boolean firstPlay, Bundle extraInfo) {
        // 视频开始播放
        if (firstPlay) {
            Log.i("Player", "首次播放开始");
        }
    }
    
    @Override
    public void onStatisticsUpdate(V2TXLivePlayer player, V2TXLivePlayerStatistics statistics) {
        // 更新播放统计信息
        Log.d("PlayerStats", "帧率: " + statistics.fps + ", 码率: " + statistics.bitrate);
    }
}

// 设置回调观察者
V2TXLivePlayer player = new V2TXLivePlayerImpl(context);
player.setObserver(new MyPlayerObserver());
```

### 自定义视频处理示例
```java
public class VideoProcessorObserver extends V2TXLivePlayerObserver {
    @Override
    public void onRenderVideoFrame(V2TXLivePlayer player, V2TXLiveVideoFrame videoFrame) {
        // 自定义视频帧处理
        // 可以添加滤镜、水印等效果
        processVideoFrame(videoFrame);
    }
    
    private void processVideoFrame(V2TXLiveVideoFrame frame) {
        // 视频帧处理逻辑
    }
}

// 开启自定义视频帧回调
player.enableObserveVideoFrame(true);
player.setObserver(new VideoProcessorObserver());
```

### 本地录制监控示例
```java
public class RecordingObserver extends V2TXLivePlayerObserver {
    @Override
    public void onLocalRecordBegin(V2TXLivePlayer player, int code, String storagePath) {
        if (code == 0) {
            Log.i("Recording", "录制开始，文件路径: " + storagePath);
        } else {
            Log.e("Recording", "录制失败，错误码: " + code);
        }
    }
    
    @Override
    public void onLocalRecording(V2TXLivePlayer player, long durationMs, String storagePath) {
        // 更新录制进度
        updateRecordingProgress(durationMs);
    }
    
    @Override
    public void onLocalRecordComplete(V2TXLivePlayer player, int code, String storagePath) {
        if (code == 0) {
            Log.i("Recording", "录制完成，文件路径: " + storagePath);
        } else {
            Log.w("Recording", "录制异常结束，状态码: " + code);
        }
    }
}
```

## 注意事项

1. **回调线程**: 除自定义渲染回调，其它所有回调方法都在UI主线程执行
2. **性能影响**: 自定义渲染和音频处理回调可能影响播放性能
3. **内存管理**: 及时释放不再使用的观察者对象，避免内存泄漏
4. **错误处理**: 合理处理各种错误码，提供友好的用户提示
5. **权限检查**: 本地录制需要确保有存储权限和足够的存储空间
