> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

# 腾讯云直播SDK V2TXLivePlayerObserver 直播播放器回调接口

## 概述

`V2TXLivePlayerObserver.h` 是腾讯云直播SDK iOS/macOS平台的播放器回调接口定义文件，包含了播放器状态、音视频事件、统计数据、错误处理等所有回调方法的定义。

**平台支持**: iOS, macOS  
**功能范围**: 播放器状态监控、音视频事件、统计数据、错误处理、本地录制等

## 📋 目录结构

### 1. [错误和警告回调](#错误和警告回调)
### 2. [连接状态回调](#连接状态回调)
### 3. [音视频播放事件](#音视频播放事件)
### 4. [统计数据回调](#统计数据回调)
### 5. [高级功能回调](#高级功能回调)
### 6. [本地录制回调](#本地录制回调)
### 7. [画中画状态回调](#画中画状态回调)
### 8. [使用示例](#使用示例)

## 1. 错误和警告回调

### 🔴 onError - 播放器错误通知

```objc
- (void)onError:(id<V2TXLivePlayer>)player 
          code:(V2TXLiveCode)code 
       message:(NSString *)msg 
     extraInfo:(NSDictionary *)extraInfo;
```

**功能**: 播放器出现错误时回调

**参数说明**:
- `player`: 触发回调的播放器对象
- `code`: 错误码，参考 `V2TXLiveCode` 枚举
- `msg`: 详细的错误信息描述
- `extraInfo`: 扩展信息字典，包含额外错误上下文

**使用场景**:
- 网络连接失败
- 流地址无效
- 解码器错误
- 播放器内部错误

### ⚠️ onWarning - 播放器警告通知

```objc
- (void)onWarning:(id<V2TXLivePlayer>)player 
            code:(V2TXLiveCode)code 
         message:(NSString *)msg 
       extraInfo:(NSDictionary *)extraInfo;
```

**功能**: 播放器出现警告时回调

**参数说明**:
- `player`: 触发回调的播放器对象
- `code`: 警告码，参考 `V2TXLiveCode` 枚举
- `msg`: 警告信息描述
- `extraInfo`: 扩展信息字典

**使用场景**:
- 网络状况不佳
- 解码性能问题
- 播放缓冲警告

## 2. 连接状态回调

### 🔗 onConnected - 连接成功回调

```objc
- (void)onConnected:(id<V2TXLivePlayer>)player 
         extraInfo:(NSDictionary *)extraInfo;
```

**功能**: 播放器成功连接到服务器时回调

**参数说明**:
- `player`: 触发回调的播放器对象
- `extraInfo`: 连接相关的扩展信息

**触发时机**:
- 调用 `startPlay` 后成功建立连接
- 网络重连成功后

### 📺 onVideoResolutionChanged - 分辨率变化回调

```objc
- (void)onVideoResolutionChanged:(id<V2TXLivePlayer>)player 
                           width:(NSInteger)width 
                          height:(NSInteger)height;
```

**功能**: 视频分辨率发生变化时回调

**参数说明**:
- `player`: 触发回调的播放器对象
- `width`: 新的视频宽度
- `height`: 新的视频高度

**使用场景**:
- 流切换时分辨率变化
- 云端混流输出分辨率变化
- 自适应码率调整分辨率

## 3. 音视频播放事件

### 🎬 onVideoPlaying - 视频播放事件

```objc
- (void)onVideoPlaying:(id<V2TXLivePlayer>)player 
            firstPlay:(BOOL)firstPlay 
            extraInfo:(NSDictionary *)extraInfo;
```

**功能**: 视频开始播放时回调

**参数说明**:
- `player`: 触发回调的播放器对象
- `firstPlay`: 是否为首次播放标志
- `extraInfo`: 播放相关的扩展信息

**触发时机**:
- 首次成功播放视频
- 恢复播放后

### 🔊 onAudioPlaying - 音频播放事件

```objc
- (void)onAudioPlaying:(id<V2TXLivePlayer>)player 
            firstPlay:(BOOL)firstPlay 
            extraInfo:(NSDictionary *)extraInfo;
```

**功能**: 音频开始播放时回调

**参数说明**:
- `player`: 触发回调的播放器对象
- `firstPlay`: 是否为首次播放标志
- `extraInfo`: 播放相关的扩展信息

### ⏳ onVideoLoading - 视频加载事件

```objc
- (void)onVideoLoading:(id<V2TXLivePlayer>)player 
             extraInfo:(NSDictionary *)extraInfo;
```

**功能**: 视频加载缓冲时回调

**参数说明**:
- `player`: 触发回调的播放器对象
- `extraInfo`: 加载相关的扩展信息

**触发时机**:
- 网络缓冲开始
- 播放器准备数据

### ⏳ onAudioLoading - 音频加载事件

```objc
- (void)onAudioLoading:(id<V2TXLivePlayer>)player 
             extraInfo:(NSDictionary *)extraInfo;
```

**功能**: 音频加载缓冲时回调

## 4. 统计数据回调

### 📊 onStatisticsUpdate - 统计数据回调

```objc
- (void)onStatisticsUpdate:(id<V2TXLivePlayer>)player 
               statistics:(V2TXLivePlayerStatistics *)statistics;
```

**功能**: 播放器统计数据定期回调

**参数说明**:
- `player`: 触发回调的播放器对象
- `statistics`: 播放器统计数据对象

**统计信息包含**:
- 视频宽度、高度、帧率、码率
- 音频码率、丢包率
- 卡顿时长、卡顿率
- 网络往返延时、下载速度

**回调频率**: 默认2秒一次

### 🔊 onPlayoutVolumeUpdate - 音量大小回调

```objc
- (void)onPlayoutVolumeUpdate:(id<V2TXLivePlayer>)player 
                      volume:(NSInteger)volume;
```

**功能**: 播放音量大小实时回调

**参数说明**:
- `player`: 触发回调的播放器对象
- `volume`: 当前播放音量大小（0-100）

**启用条件**: 需要调用 `enableVolumeEvaluation` 开启音量评估

**回调频率**: 100ms一次

## 5. 高级功能回调

### 📸 onSnapshotComplete - 截图完成回调

```objc
- (void)onSnapshotComplete:(id<V2TXLivePlayer>)player 
                   image:(nullable TXImage *)image;
```

**功能**: 截图操作完成时回调

**参数说明**:
- `player`: 触发回调的播放器对象
- `image`: 截取的视频画面图像，失败时为nil

**触发时机**: 调用 `snapshot` 方法后

### 🎨 onRenderVideoFrame - 自定义视频渲染回调

```objc
- (void)onRenderVideoFrame:(id<V2TXLivePlayer>)player 
                    frame:(V2TXLiveVideoFrame *)videoFrame;
```

**功能**: 自定义视频渲染回调，获取解码后的视频帧

**参数说明**:
- `player`: 触发回调的播放器对象
- `videoFrame`: 视频帧数据对象

**启用条件**: 需要调用 `enableObserveVideoFrame` 开启回调

**使用场景**:
- 自定义视频处理
- 视频滤镜应用
- 视频分析处理

### 🎵 onPlayoutAudioFrame - 音频数据回调

```objc
- (void)onPlayoutAudioFrame:(id<V2TXLivePlayer>)player 
                    frame:(V2TXLiveAudioFrame *)audioFrame;
```

**功能**: 音频数据回调，获取播放的音频帧

**参数说明**:
- `player`: 触发回调的播放器对象
- `audioFrame`: 音频帧数据对象

**启用条件**: 需要调用 `enableObserveAudioFrame` 开启回调

**使用场景**:
- 音频实时处理
- 音频分析
- 音频特效应用

### 📨 onReceiveSeiMessage - SEI消息接收回调

```objc
- (void)onReceiveSeiMessage:(id<V2TXLivePlayer>)player 
               payloadType:(int)payloadType 
                      data:(NSData *)data;
```

**功能**: 接收SEI（补充增强信息）消息回调

**参数说明**:
- `player`: 触发回调的播放器对象
- `payloadType`: SEI消息的payload类型
- `data`: SEI消息数据

**启用条件**: 需要调用 `enableReceiveSeiMessage` 开启接收

**使用场景**:
- 时间同步信息
- 场景描述信息
- 自定义业务数据

### 🔄 onStreamSwitched - 流切换回调

```objc
- (void)onStreamSwitched:(id<V2TXLivePlayer>)player 
                    url:(NSString *)url 
                   code:(NSInteger)code;
```

**功能**: 分辨率无缝切换结果回调

**参数说明**:
- `player`: 触发回调的播放器对象
- `url`: 切换后的播放地址
- `code`: 切换状态码
  - `0`: 成功
  - `-1`: 切换超时
  - `-2`: 服务端错误
  - `-3`: 客户端错误

**触发时机**: 调用 `switchStream` 方法后

## 6. 本地录制回调

### 🎬 onLocalRecordBegin - 录制开始回调

```objc
- (void)onLocalRecordBegin:(id<V2TXLivePlayer>)player 
                  errCode:(NSInteger)errCode 
              storagePath:(NSString *)storagePath;
```

**功能**: 本地录制任务开始事件回调

**参数说明**:
- `player`: 触发回调的播放器对象
- `errCode`: 录制开始状态码
  - `0`: 启动成功
  - `-1`: 内部错误
  - `-2`: 文件格式不支持
  - `-6`: 录制已启动
  - `-7`: 文件已存在
  - `-8`: 目录无写入权限
- `storagePath`: 录制文件存储路径

**触发时机**: 调用 `startLocalRecording` 后

### ⏱️ onLocalRecording - 录制进行中回调

```objc
- (void)onLocalRecording:(id<V2TXLivePlayer>)player 
             durationMs:(NSInteger)durationMs 
            storagePath:(NSString *)storagePath;
```

**功能**: 录制任务进行中的进展回调

**参数说明**:
- `player`: 触发回调的播放器对象
- `durationMs`: 当前录制时长（毫秒）
- `storagePath`: 录制文件存储路径

**启用条件**: 需要在 `startLocalRecording` 时设置回调间隔
**默认状态**: 不回调

### ✅ onLocalRecordComplete - 录制完成回调

```objc
- (void)onLocalRecordComplete:(id<V2TXLivePlayer>)player 
                     errCode:(NSInteger)errCode 
                 storagePath:(NSString *)storagePath;
```

**功能**: 录制任务结束事件回调

**参数说明**:
- `player`: 触发回调的播放器对象
- `errCode`: 录制结束状态码
  - `0`: 结束成功
  - `-1`: 录制失败
  - `-2`: 分辨率/横竖屏切换导致结束
  - `-3`: 录制时间太短或无数据
- `storagePath`: 录制文件存储路径

**触发时机**: 调用 `stopLocalRecording` 后

## 7. 画中画状态回调

### 🖼️ onPictureInPictureStateUpdate - 画中画状态变更回调

```objc
- (void)onPictureInPictureStateUpdate:(id<V2TXLivePlayer>)player 
                               state:(V2TXLivePictureInPictureState)state 
                             message:(NSString *)msg 
                           extraInfo:(NSDictionary *)extraInfo;
```

**功能**: 画中画状态变化时回调

**参数说明**:
- `player`: 触发回调的播放器对象
- `state`: 画中画状态，参考 `V2TXLivePictureInPictureState`
- `msg`: 状态描述信息
- `extraInfo`: 扩展信息

**支持状态**:
- `V2TXLivePictureInPictureStateWillStart`: 将要开始
- `V2TXLivePictureInPictureStateDidStart`: 已经开始
- `V2TXLivePictureInPictureStateWillStop`: 将要停止
- `V2TXLivePictureInPictureStateDidStop`: 已经停止
- `V2TXLivePictureInPictureStateRestoreUI`: 恢复用户界面

**启用条件**: 需要调用 `enablePictureInPicture` 开启画中画

## 8. 使用示例

### 🔧 基础播放器实现

```objc
@interface MyPlayerObserver : NSObject <V2TXLivePlayerObserver>
@end

@implementation MyPlayerObserver

#pragma mark - 错误处理
- (void)onError:(id<V2TXLivePlayer>)player code:(V2TXLiveCode)code message:(NSString *)msg extraInfo:(NSDictionary *)extraInfo {
    NSLog(@"播放器错误: %@, 错误码: %ld", msg, (long)code);
    // 处理播放错误
}

#pragma mark - 连接状态
- (void)onConnected:(id<V2TXLivePlayer>)player extraInfo:(NSDictionary *)extraInfo {
    NSLog(@"播放器连接成功");
}

#pragma mark - 播放事件
- (void)onVideoPlaying:(id<V2TXLivePlayer>)player firstPlay:(BOOL)firstPlay extraInfo:(NSDictionary *)extraInfo {
    if (firstPlay) {
        NSLog(@"视频首次播放成功");
    }
}

#pragma mark - 统计数据
- (void)onStatisticsUpdate:(id<V2TXLivePlayer>)player statistics:(V2TXLivePlayerStatistics *)statistics {
    NSLog(@"视频帧率: %ld, 码率: %ld Kbps", statistics.fps, statistics.videoBitrate);
}

@end
```

### 📊 音量监控实现

```objc
// 开启音量评估
[player enableVolumeEvaluation:100]; // 100ms回调一次

// 音量回调实现
- (void)onPlayoutVolumeUpdate:(id<V2TXLivePlayer>)player volume:(NSInteger)volume {
    // 更新UI音量指示器
    [self updateVolumeIndicator:volume];
}
```

### 🎬 本地录制实现

```objc
// 开始录制
V2TXLiveLocalRecordingParams *params = [[V2TXLiveLocalRecordingParams alloc] init];
params.filePath = @"/path/to/record.mp4";
params.recordMode = V2TXLiveRecordModeBoth;
params.interval = 1000; // 1秒回调一次录制进度

[player startLocalRecording:params];

// 录制回调实现
- (void)onLocalRecording:(id<V2TXLivePlayer>)player durationMs:(NSInteger)durationMs storagePath:(NSString *)storagePath {
    NSLog(@"录制进度: %.1f秒", durationMs / 1000.0);
}

- (void)onLocalRecordComplete:(id<V2TXLivePlayer>)player errCode:(NSInteger)errCode storagePath:(NSString *)storagePath {
    if (errCode == 0) {
        NSLog(@"录制完成，文件路径: %@", storagePath);
    } else {
        NSLog(@"录制失败，错误码: %ld", (long)errCode);
    }
}
```

### 🎨 自定义视频处理

```objc
// 开启视频帧回调
[player enableObserveVideoFrame:YES pixelFormat:V2TXLivePixelFormatNV12];

// 视频帧处理回调
- (void)onRenderVideoFrame:(id<V2TXLivePlayer>)player frame:(V2TXLiveVideoFrame *)videoFrame {
    // 自定义视频处理逻辑
    [self processVideoFrame:videoFrame];
}
```

## 📋 最佳实践

### 🔧 回调处理建议

1. **错误处理**: 在 `onError` 中实现完善的错误恢复机制
2. **性能监控**: 利用 `onStatisticsUpdate` 监控播放质量
3. **用户体验**: 通过播放事件回调优化用户界面反馈
4. **资源管理**: 及时释放回调中使用的资源

### ⚡ 性能优化

1. **回调频率**: 合理设置统计数据和音量回调频率
2. **线程安全**: 确保回调方法中的UI操作在主线程执行
3. **内存管理**: 避免在回调中创建大量临时对象

### 🔒 异常处理

1. **网络异常**: 实现自动重连和降级策略
2. **解码异常**: 准备备用解码方案
3. **录制异常**: 处理文件权限和存储空间问题
