> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/en/llms.txt
> Use this file to discover all available pages before exploring further.

# Tencent Cloud Live Streaming SDK V2TXLivePlayerObserver Callback Interface

## Feature Overview

`V2TXLivePlayerObserver.h` defines the callback interface for the Tencent Cloud Live Streaming SDK on iOS and macOS. This file includes all callback methods related to player status, audio/video events, statistics, error handling, local recording, and more.

**Platform Support**: iOS, macOS  
**Feature Scope**: Player status monitoring, audio/video events, statistics, error handling, local recording, and more.

## 📋 Table of Contents

### 1. [Error and Warning Callbacks](#错误和警告回调)
### 2. [Connection Status Callbacks](#连接状态回调)
### 3. [Audio/Video Playback Events](#音视频播放事件)
### 4. [Statistics Callbacks](#统计数据回调)
### 5. [Advanced Feature Callbacks](#高级功能回调)
### 6. [Local Recording Callbacks](#本地录制回调)
### 7. [Picture-in-Picture Status Callbacks](#画中画状态回调)
### 8. [Usage Examples](#使用示例)

## 1. Error and Warning Callbacks

### 🔴 onError - Player Error Callback

```objc
- (void)onError:(id<V2TXLivePlayer>)player 
          code:(V2TXLiveCode)code 
       message:(NSString *)msg 
     extraInfo:(NSDictionary *)extraInfo;
```

**Description**: Invoked when the player encounters an error.

**Parameters**:
- `player`: The player instance reporting the error
- `code`: Error code, see the `V2TXLiveCode` enum
- `msg`: Detailed error message
- `extraInfo`: Additional error context

**Common Scenarios**:
- Network connection failures
- Invalid stream URL
- Decoder errors
- Internal player errors

### ⚠️ onWarning - Player Warning Callback

```objc
- (void)onWarning:(id<V2TXLivePlayer>)player 
            code:(V2TXLiveCode)code 
         message:(NSString *)msg 
       extraInfo:(NSDictionary *)extraInfo;
```

**Description**: Invoked when the player encounters a warning.

**Parameters**:
- `player`: The player instance reporting the warning
- `code`: Warning code, see the `V2TXLiveCode` enum
- `msg`: Warning message
- `extraInfo`: Additional warning context

**Common Scenarios**:
- Poor network conditions
- Decoding performance issues
- Playback buffering warnings

## 2. Connection Status Callbacks

### 🔗 onConnected - Connection Success Callback

```objc
- (void)onConnected:(id<V2TXLivePlayer>)player 
         extraInfo:(NSDictionary *)extraInfo;
```

**Description**: Invoked when the player successfully connects to the server.

**Parameters**:
- `player`: The player instance that connected
- `extraInfo`: Additional connection information

**Triggered When**:
- `startPlay` is called and connection is established
- Network reconnection succeeds

### 📺 onVideoResolutionChanged - Video Resolution Change Callback

```objc
- (void)onVideoResolutionChanged:(id<V2TXLivePlayer>)player 
                           width:(NSInteger)width 
                          height:(NSInteger)height;
```

**Description**: Invoked when the video resolution changes.

**Parameters**:
- `player`: The player instance
- `width`: New video width
- `height`: New video height

**Common Scenarios**:
- Resolution changes during stream switching
- Resolution changes due to cloud stream mixing output
- Adaptive bitrate adjustments

## 3. Audio/Video Playback Events

### 🎬 onVideoPlaying - Video Playback Started

```objc
- (void)onVideoPlaying:(id<V2TXLivePlayer>)player 
            firstPlay:(BOOL)firstPlay 
            extraInfo:(NSDictionary *)extraInfo;
```

**Description**: Invoked when video playback starts.

**Parameters**:
- `player`: The player instance
- `firstPlay`: Indicates if this is the first playback
- `extraInfo`: Additional playback information

**Triggered When**:
- First successful video playback
- Playback resumes

### 🔊 onAudioPlaying - Audio Playback Started

```objc
- (void)onAudioPlaying:(id<V2TXLivePlayer>)player 
            firstPlay:(BOOL)firstPlay 
            extraInfo:(NSDictionary *)extraInfo;
```

**Description**: Invoked when audio playback starts.

**Parameters**:
- `player`: The player instance
- `firstPlay`: Indicates if this is the first playback
- `extraInfo`: Additional playback information

### ⏳ onVideoLoading - Video Buffering Started

```objc
- (void)onVideoLoading:(id<V2TXLivePlayer>)player 
             extraInfo:(NSDictionary *)extraInfo;
```

**Description**: Invoked when the video is buffering or loading.

**Parameters**:
- `player`: The player instance
- `extraInfo`: Additional buffering information

**Triggered When**:
- Network buffering begins
- Player is preparing data

### ⏳ onAudioLoading - Audio Buffering Started

```objc
- (void)onAudioLoading:(id<V2TXLivePlayer>)player 
             extraInfo:(NSDictionary *)extraInfo;
```

**Description**: Invoked when the audio is buffering or loading.

## 4. Statistics Callbacks

### 📊 onStatisticsUpdate - Player Statistics Callback

```objc
- (void)onStatisticsUpdate:(id<V2TXLivePlayer>)player 
               statistics:(V2TXLivePlayerStatistics *)statistics;
```

**Description**: Periodically provides player statistics.

**Parameters**:
- `player`: The player instance
- `statistics`: Player statistics object

**Statistics Include**:
- Video width, height, frame rate, bitrate
- Audio bitrate, packet loss rate
- Stutter duration, stutter rate
- Network Round-Trip Time (RTT), download speed

**Frequency**: Every 2 seconds by default

### 🔊 onPlayoutVolumeUpdate - Playback Volume Callback

```objc
- (void)onPlayoutVolumeUpdate:(id<V2TXLivePlayer>)player 
                      volume:(NSInteger)volume;
```

**Description**: Provides real-time playback volume updates.

**Parameters**:
- `player`: The player instance
- `volume`: Current playback volume (0-100)

**Enablement**: Requires `enableVolumeEvaluation` to be called

**Frequency**: Every 100ms

## 5. Advanced Feature Callbacks

### 📸 onSnapshotComplete - Snapshot Completion Callback

```objc
- (void)onSnapshotComplete:(id<V2TXLivePlayer>)player 
                   image:(nullable TXImage *)image;
```

**Description**: Invoked when a snapshot operation completes.

**Parameters**:
- `player`: The player instance
- `image`: Captured video frame image, or nil if failed

**Triggered When**: After calling the `snapshot` method

### 🎨 onRenderVideoFrame - Custom Video Rendering Callback

```objc
- (void)onRenderVideoFrame:(id<V2TXLivePlayer>)player 
                    frame:(V2TXLiveVideoFrame *)videoFrame;
```

**Description**: Provides access to decoded video frames for custom rendering.

**Parameters**:
- `player`: The player instance
- `videoFrame`: Video frame data object

**Enablement**: Requires `enableObserveVideoFrame` to be called

**Use Cases**:
- Custom video processing
- Applying video filters
- Video analysis

### 🎵 onPlayoutAudioFrame - Audio Frame Callback

```objc
- (void)onPlayoutAudioFrame:(id<V2TXLivePlayer>)player 
                    frame:(V2TXLiveAudioFrame *)audioFrame;
```

**Description**: Provides access to playback audio frames.

**Parameters**:
- `player`: The player instance
- `audioFrame`: Audio frame data object

**Enablement**: Requires `enableObserveAudioFrame` to be called

**Use Cases**:
- Real-time audio processing
- Audio analysis
- Applying audio effects

### 📨 onReceiveSeiMessage - SEI Message Callback

```objc
- (void)onReceiveSeiMessage:(id<V2TXLivePlayer>)player 
               payloadType:(int)payloadType 
                      data:(NSData *)data;
```

**Description**: Invoked when an SEI (Supplemental Enhancement Information) message is received.

**Parameters**:
- `player`: The player instance
- `payloadType`: SEI message payload type
- `data`: SEI message data

**Enablement**: Requires `enableReceiveSeiMessage` to be called

**Use Cases**:
- Time synchronization
- Scene description
- Custom business data

### 🔄 onStreamSwitched - Stream Switch Callback

```objc
- (void)onStreamSwitched:(id<V2TXLivePlayer>)player 
                    url:(NSString *)url 
                   code:(NSInteger)code;
```

**Description**: Reports the result of seamless stream switching.

**Parameters**:
- `player`: The player instance
- `url`: Playback URL after switching
- `code`: Switch status code
  - `0`: Success
  - `-1`: Switch timeout
  - `-2`: Server error
  - `-3`: Client error

**Triggered When**: After calling `switchStream`

## 6. Local Recording Callbacks

### 🎬 onLocalRecordBegin - Recording Start Callback

```objc
- (void)onLocalRecordBegin:(id<V2TXLivePlayer>)player 
                  errCode:(NSInteger)errCode 
              storagePath:(NSString *)storagePath;
```

**Description**: Invoked when a local recording task starts.

**Parameters**:
- `player`: The player instance
- `errCode`: Recording start status code
  - `0`: Started successfully
  - `-1`: Internal error
  - `-2`: Unsupported file format
  - `-6`: Recording already started
  - `-7`: File already exists
  - `-8`: No write permission for directory
- `storagePath`: Path to the recording file

**Triggered When**: After calling `startLocalRecording`

### ⏱️ onLocalRecording - Recording Progress Callback

```objc
- (void)onLocalRecording:(id<V2TXLivePlayer>)player 
             durationMs:(NSInteger)durationMs 
            storagePath:(NSString *)storagePath;
```

**Description**: Reports progress during a recording task.

**Parameters**:
- `player`: The player instance
- `durationMs`: Current recording duration in milliseconds
- `storagePath`: Path to the recording file

**Enablement**: Set the callback interval when calling `startLocalRecording`  
**Default**: No callback if not set

### ✅ onLocalRecordComplete - Recording Completion Callback

```objc
- (void)onLocalRecordComplete:(id<V2TXLivePlayer>)player 
                     errCode:(NSInteger)errCode 
                 storagePath:(NSString *)storagePath;
```

**Description**: Invoked when a recording task completes.

**Parameters**:
- `player`: The player instance
- `errCode`: Recording completion status code
  - `0`: Completed successfully
  - `-1`: Recording failed
  - `-2`: Ended due to resolution/orientation change
  - `-3`: Recording too short or no data
- `storagePath`: Path to the recording file

**Triggered When**: After calling `stopLocalRecording`

## 7. Picture-in-Picture Status Callbacks

### 🖼️ onPictureInPictureStateUpdate - Picture-in-Picture State Callback

```objc
- (void)onPictureInPictureStateUpdate:(id<V2TXLivePlayer>)player 
                               state:(V2TXLivePictureInPictureState)state 
                             message:(NSString *)msg 
                           extraInfo:(NSDictionary *)extraInfo;
```

**Description**: Invoked when the picture-in-picture state changes.

**Parameters**:
- `player`: The player instance
- `state`: Picture-in-picture state, see `V2TXLivePictureInPictureState`
- `msg`: State description
- `extraInfo`: Additional information

**Supported States**:
- `V2TXLivePictureInPictureStateWillStart`: About to start
- `V2TXLivePictureInPictureStateDidStart`: Started
- `V2TXLivePictureInPictureStateWillStop`: About to stop
- `V2TXLivePictureInPictureStateDidStop`: Stopped
- `V2TXLivePictureInPictureStateRestoreUI`: Restore UI

**Enablement**: Requires `enablePictureInPicture` to be called

## 8. Usage Examples

### 🔧 Basic Player Observer Implementation

```objc
@interface MyPlayerObserver : NSObject <V2TXLivePlayerObserver>
@end

@implementation MyPlayerObserver

#pragma mark - Error Handling
- (void)onError:(id<V2TXLivePlayer>)player code:(V2TXLiveCode)code message:(NSString *)msg extraInfo:(NSDictionary *)extraInfo {
    NSLog(@"Player error: %@, error code: %ld", msg, (long)code);
    // Handle playback error
}

#pragma mark - Connection Status
- (void)onConnected:(id<V2TXLivePlayer>)player extraInfo:(NSDictionary *)extraInfo {
    NSLog(@"Player connected successfully");
}

#pragma mark - Playback Events
- (void)onVideoPlaying:(id<V2TXLivePlayer>)player firstPlay:(BOOL)firstPlay extraInfo:(NSDictionary *)extraInfo {
    if (firstPlay) {
        NSLog(@"Video played successfully for the first time");
    }
}

#pragma mark - Statistics
- (void)onStatisticsUpdate:(id<V2TXLivePlayer>)player statistics:(V2TXLivePlayerStatistics *)statistics {
    NSLog(@"Video FPS: %ld, Bitrate: %ld Kbps", statistics.fps, statistics.videoBitrate);
}

@end
```

### 📊 Volume Monitoring Example

```objc
// Enable volume evaluation
[player enableVolumeEvaluation:100]; // Callback every 100ms

// Volume callback implementation
- (void)onPlayoutVolumeUpdate:(id<V2TXLivePlayer>)player volume:(NSInteger)volume {
    // Update UI volume indicator
    [self updateVolumeIndicator:volume];
}
```

### 🎬 Local Recording Example

```objc
// Start recording
V2TXLiveLocalRecordingParams *params = [[V2TXLiveLocalRecordingParams alloc] init];
params.filePath = @"/path/to/record.mp4";
params.recordMode = V2TXLiveRecordModeBoth;
params.interval = 1000; // Callback recording progress every 1 second

[player startLocalRecording:params];

// Recording callback implementation
- (void)onLocalRecording:(id<V2TXLivePlayer>)player durationMs:(NSInteger)durationMs storagePath:(NSString *)storagePath {
    NSLog(@"Recording progress: %.1f seconds", durationMs / 1000.0);
}

- (void)onLocalRecordComplete:(id<V2TXLivePlayer>)player errCode:(NSInteger)errCode storagePath:(NSString *)storagePath {
    if (errCode == 0) {
        NSLog(@"Recording completed, file path: %@", storagePath);
    } else {
        NSLog(@"Recording failed, error code: %ld", (long)errCode);
    }
}
```

### 🎨 Custom Video Frame Processing

```objc
// Enable video frame callback
[player enableObserveVideoFrame:YES pixelFormat:V2TXLivePixelFormatNV12];

// Video frame processing callback
- (void)onRenderVideoFrame:(id<V2TXLivePlayer>)player frame:(V2TXLiveVideoFrame *)videoFrame {
    // Custom video processing logic
    [self processVideoFrame:videoFrame];
}
```

## 📋 Best Practices

### 🔧 Callback Handling Recommendations

1. **Error Handling**: Implement robust error recovery in `onError`.
2. **Performance Monitoring**: Use `onStatisticsUpdate` to monitor playback quality.
3. **User Experience**: Improve UI feedback by leveraging playback event callbacks.
4. **Resource Management**: Release resources used in callbacks promptly.

### ⚡ Performance Optimization

1. **Callback Frequency**: Set appropriate frequencies for statistics and volume callbacks.
2. **Thread Safety**: Ensure all UI updates in callbacks are performed on the main thread.
3. **Memory Management**: Avoid creating unnecessary temporary objects in callbacks.

### 🔒 Exception Handling

1. **Network Exceptions**: Implement auto-reconnect and fallback strategies.
2. **Decoding Exceptions**: Prepare backup decoding solutions.
3. **Recording Exceptions**: Handle file permissions and storage space issues.