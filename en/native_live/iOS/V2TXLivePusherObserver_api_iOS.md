> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

Tencent Cloud Live Streaming SDK V2TXLivePusherObserver Callback Reference

## Overview

`V2TXLivePusherObserver.h` defines the callback protocol for Tencent Cloud Live Streaming SDK on iOS and macOS. Use this interface to receive real-time status updates, streaming statistics, error notifications, and event callbacks during the live broadcast lifecycle.

**Supported Platforms**: iOS, macOS  
**Protocol Type**: Objective-C Protocol  
**Callback Methods**: 15 core callbacks

## 📋 Table of Contents

### 1. [Core Feature Highlights](#核心功能特性)
### 2. [Error and Warning Callbacks](#错误与警告回调)
### 3. [First Frame Capture Callbacks](#首帧采集回调)
### 4. [Push Status Callbacks](#推流状态回调)
### 5. [Statistics Callbacks](#统计数据回调)
### 6. [Audio & Video Processing Callbacks](#音视频处理回调)
### 7. [Screen Sharing Callbacks](#屏幕分享回调)
### 8. [Local Recording Callbacks](#本地录制回调)
### 9. [Advanced Feature Callbacks](#高级功能回调)
### 10. [Usage Examples](#使用示例)

## 1. Core Feature Highlights

### 🎯 Callback Categories

| Category        | Callback Count | Description                                   |
|-----------------|---------------|-----------------------------------------------|
| Error & Warning | 2             | Error and warning notifications for live push |
| First Frame     | 2             | First audio/video frame capture notifications |
| Push Status     | 1             | Connection status updates                     |
| Statistics      | 1             | Real-time streaming statistics                |
| Audio/Video Proc| 3             | Custom audio/video processing                 |
| Screen Sharing  | 2             | Screen capture start/stop notifications       |
| Local Recording | 3             | Local recording status updates                |
| Advanced        | 1             | Voice activity detection status               |

### 🔧 Technical Highlights

- **Real-time**: All callbacks are dispatched on the main thread
- **Comprehensive**: Covers all major live stream events
- **Extensible**: Supports custom audio and video processing
- **Debug-Friendly**: Provides detailed error and statistics reporting

## 2. Error and Warning Callbacks

### ⚠️ onError - Error Notification

```objc
- (void)onError:(V2TXLiveCode)code message:(NSString *)msg extraInfo:(NSDictionary *)extraInfo;
```

**Description**: Notifies when the live pusher encounters an error.

**Parameters**:
- `code`: Error code, see `V2TXLiveCode`
- `msg`: Error message
- `extraInfo`: Additional details

**Typical Scenarios**:
- Network connection failure
- Invalid stream URL
- Hardware device error
- Encoder initialization failure

**Recommended Handling**:
```objc
- (void)onError:(V2TXLiveCode)code message:(NSString *)msg extraInfo:(NSDictionary *)extraInfo {
    NSLog(@"Live push error: %ld - %@", (long)code, msg);

    switch (code) {
        case V2TXLIVE_ERROR_NET_DISCONNECT:
            // Network disconnected, attempt reconnection
            [self reconnect];
            break;
        case V2TXLIVE_ERROR_INVALID_LICENSE:
            // Invalid license, verify configuration
            [self checkLicense];
            break;
        default:
            // Handle other errors
            [self handleError:code];
            break;
    }
}
```

### ⚠️ onWarning - Warning Notification

```objc
- (void)onWarning:(V2TXLiveCode)code message:(NSString *)msg extraInfo:(NSDictionary *)extraInfo;
```

**Description**: Notifies when the live pusher encounters a warning.

**Parameters**:
- `code`: Warning code, see `V2TXLiveCode`
- `msg`: Warning message
- `extraInfo`: Additional details

**Common Scenarios**:
- Poor network conditions
- Encoding parameter mismatch
- Device resource constraints
- Audio/video capture issues

**Recommended Handling**:
```objc
- (void)onWarning:(V2TXLiveCode)code message:(NSString *)msg extraInfo:(NSDictionary *)extraInfo {
    NSLog(@"Live push warning: %ld - %@", (long)code, msg);

    // Respond to specific warnings
    if (code == V2TXLIVE_WARNING_NETWORK_BUSY) {
        // Network congestion, notify user or reduce bitrate
        [self adjustBitrate];
    }
}
```

## 3. First Frame Capture Callbacks

### 🎵 onCaptureFirstAudioFrame - First Audio Frame

```objc
- (void)onCaptureFirstAudioFrame;
```

**Description**: Triggered when the microphone captures the first audio frame.

**Typical Use Cases**:
- Monitor audio capture status
- Measure stream startup latency
- Detect audio device readiness

**Sample Implementation**:
```objc
- (void)onCaptureFirstAudioFrame {
    NSLog(@"First audio frame captured");
    [self updateUIWithAudioStatus:YES];
}
```

### 🎥 onCaptureFirstVideoFrame - First Video Frame

```objc
- (void)onCaptureFirstVideoFrame;
```

**Description**: Triggered when the camera captures the first video frame.

**Typical Use Cases**:
- Monitor video capture status
- Control preview display timing
- Detect camera device readiness

**Sample Implementation**:
```objc
- (void)onCaptureFirstVideoFrame {
    NSLog(@"First video frame captured");
    [self updateUIWithVideoStatus:YES];

    // Start preview animation
    [self showPreviewAnimation];
}
```

## 4. Push Status Callbacks

### 🔄 onPushStatusUpdate - Connection Status Update

```objc
- (void)onPushStatusUpdate:(V2TXLivePushStatus)status message:(NSString *)msg extraInfo:(NSDictionary *)extraInfo;
```

**Description**: Notifies when the live pusher connection status changes.

**Parameters**:
- `status`: Push status, see `V2TXLivePushStatus`
- `msg`: Status message
- `extraInfo`: Additional details

**Status Enum Reference**:
```objc
typedef NS_ENUM(NSInteger, V2TXLivePushStatus) {
    V2TXLivePushStatusDisconnected = 0,    // Disconnected
    V2TXLivePushStatusConnecting,          // Connecting
    V2TXLivePushStatusConnectSuccess,      // Connected
    V2TXLivePushStatusReconnecting,        // Reconnecting
};
```

**Status Transition Example**:
```objc
- (void)onPushStatusUpdate:(V2TXLivePushStatus)status message:(NSString *)msg extraInfo:(NSDictionary *)extraInfo {
    switch (status) {
        case V2TXLivePushStatusConnecting:
            NSLog(@"Connecting to live streaming server...");
            [self updateStatus:@"Connecting"];
            break;

        case V2TXLivePushStatusConnectSuccess:
            NSLog(@"Live stream connected successfully");
            [self updateStatus:@"Streaming"];
            [self startPushTimer];
            break;

        case V2TXLivePushStatusReconnecting:
            NSLog(@"Network issue, reconnecting...");
            [self updateStatus:@"Reconnecting"];
            break;

        case V2TXLivePushStatusDisconnected:
            NSLog(@"Live stream connection disconnected");
            [self updateStatus:@"Disconnected"];
            [self stopPushTimer];
            break;
    }
}
```

## 5. Statistics Callback

### 📊 onStatisticsUpdate - Streaming Statistics

```objc
- (void)onStatisticsUpdate:(V2TXLivePusherStatistics *)statistics;
```

**Description**: Provides real-time streaming performance metrics.

**Parameters**:
- `statistics`: Streaming statistics object with detailed metrics

**Statistics Structure**:
```objc
@interface V2TXLivePusherStatistics : NSObject

/** App CPU usage (%) */
@property (nonatomic, assign) int appCpu;

/** System CPU usage (%) */
@property (nonatomic, assign) int systemCpu;

/** Video width */
@property (nonatomic, assign) int width;

/** Video height */
@property (nonatomic, assign) int height;

/** Frame rate (fps) */
@property (nonatomic, assign) int fps;

/** Video bitrate (kbps) */
@property (nonatomic, assign) int videoBitrate;

/** Audio bitrate (kbps) */
@property (nonatomic, assign) int audioBitrate;

/** Network latency (ms) */
@property (nonatomic, assign) int delay;

/** Network jitter (ms) */
@property (nonatomic, assign) int jitter;

/** Audio sample rate (Hz) */
@property (nonatomic, assign) int audioSampleRate;

/** Number of audio channels */
@property (nonatomic, assign) int audioChannels;

@end
```

**Sample Implementation**:
```objc
- (void)onStatisticsUpdate:(V2TXLivePusherStatistics *)statistics {
    // Update UI with latest stats
    self.statsLabel.text = [NSString stringWithFormat:@"FPS:%dfps Bitrate:%dkbps Latency:%dms",
                           statistics.fps, statistics.videoBitrate, statistics.delay];

    // Monitor performance
    if (statistics.appCpu > 80) {
        [self adjustPerformance];
    }

    // Monitor network quality
    if (statistics.delay > 1000) {
        [self adjustBitrateForNetwork];
    }
}
```

## 6. Audio & Video Processing Callbacks

### 🔊 onMicrophoneVolumeUpdate - Capture Volume Update

```objc
- (void)onMicrophoneVolumeUpdate:(NSInteger)volume;
```

**Description**: Reports microphone capture volume.

**Prerequisite**: Enable volume evaluation via `enableVolumeEvaluation`.

**Parameters**:
- `volume`: Volume level (0-100)

**Typical Use Cases**:
- Display real-time volume
- Detect mute state
- Monitor audio quality

**Sample Implementation**:
```objc
- (void)onMicrophoneVolumeUpdate:(NSInteger)volume {
    // Update volume bar
    [self.volumeView setVolume:volume];

    // Mute detection
    if (volume < 5) {
        [self showMuteIndicator];
    } else {
        [self hideMuteIndicator];
    }
}
```

### 🎵 onProcessAudioFrame - Custom Audio Processing

```objc
- (void)onProcessAudioFrame:(V2TXLiveAudioFrame *)frame;
```

**Description**: Provides locally captured audio frames after preprocessing, effects, and BGM mixing.

**Technical Details**:
- **Frame Duration**: 0.02 seconds
- **Format**: PCM
- **Byte Calculation**: `Sample rate × Frame duration × Channel count × Sample bit width`

**Default Example**:
```
48000Hz × 0.02s × 1 channel × 16bit = 15360bit = 1920 bytes
```

**Notes**:
1. Avoid time-consuming operations in this callback
2. Processing must complete within 20ms
3. Audio data is readable and writable for synchronous modification

**Sample Implementation**:
```objc
- (void)onProcessAudioFrame:(V2TXLiveAudioFrame *)frame {
    // Real-time audio processing

    // 1. Simple volume boost
    [self enhanceAudioVolume:frame];

    // 2. Audio spectrum analysis
    [self analyzeAudioSpectrum:frame];

    // 3. Apply custom effects
    [self applyCustomAudioEffect:frame];
}

- (void)enhanceAudioVolume:(V2TXLiveAudioFrame *)frame {
    // Volume boost algorithm
    int16_t *audioData = (int16_t *)frame.data;
    NSUInteger sampleCount = frame.data.length / sizeof(int16_t);

    for (NSUInteger i = 0; i < sampleCount; i++) {
        audioData[i] = (int16_t)(audioData[i] * 1.2); // Boost volume by 20%
    }
}
```

### 🎥 onProcessVideoFrame - Custom Video Processing

```objc
- (void)onProcessVideoFrame:(V2TXLiveVideoFrame *_Nonnull)srcFrame dstFrame:(V2TXLiveVideoFrame *_Nonnull)dstFrame;
```

**Description**: Enables custom video processing, including beauty filters and effects.

**Prerequisite**: Enable via `enableCustomVideoProcess`.

**Parameters**:
- `srcFrame`: Original video frame (read-only)
- `dstFrame`: Processed video frame (writable)

**Use Cases**:

#### Beauty Component Generates New Texture
```objc
- (void)onProcessVideoFrame:(V2TXLiveVideoFrame *)srcFrame dstFrame:(V2TXLiveVideoFrame *)dstFrame {
    // Beauty filter generates new texture
    GLuint dstTextureId = [self.beautyProcessor processTexture:srcFrame.textureId
                                                        width:srcFrame.width
                                                       height:srcFrame.height];

    // Assign processed texture
    dstFrame.textureId = dstTextureId;
}
```

#### Beauty Component Uses Existing Texture
```objc
- (void)onProcessVideoFrame:(V2TXLiveVideoFrame *)srcFrame dstFrame:(V2TXLiveVideoFrame *)dstFrame {
    // Third-party beauty filter uses input/output textures
    [self.thirdPartyBeauty processInputTexture:srcFrame.textureId
                                 outputTexture:dstFrame.textureId
                                         width:srcFrame.width
                                        height:srcFrame.height];
}
```

### 🔧 onGLContextDestroyed - OpenGL Context Cleanup

```objc
- (void)onGLContextDestroyed;
```

**Description**: Notifies when the SDK's internal OpenGL context is destroyed.

**Trigger Scenarios**:
- App enters background
- Live pusher is released
- OpenGL context lost

**Recommended Handling**:
```objc
- (void)onGLContextDestroyed {
    NSLog(@"OpenGL context destroyed");

    // Release custom OpenGL resources
    [self cleanupGLResources];

    // Reinitialize OpenGL components as needed
    [self reinitializeGLComponents];
}
```

## 7. Screen Sharing Callbacks

### 🖥️ onScreenCaptureStarted - Screen Sharing Started

```objc
- (void)onScreenCaptureStarted;
```

**Description**: Indicates that screen sharing has started successfully.

**Sample Implementation**:
```objc
- (void)onScreenCaptureStarted {
    NSLog(@"Screen sharing started");

    // Update UI state
    [self updateScreenShareStatus:YES];

    // Show screen sharing indicator
    [self showScreenShareIndicator];
}
```

### 🖥️ onScreenCaptureStopped - Screen Sharing Stopped

```objc
- (void)onScreenCaptureStopped:(int)reason;
```

**Description**: Indicates that screen sharing has stopped.

**Parameters**:
- `reason`: Stop reason
  - `0`: Stopped manually by user
  - `1`: iOS - interrupted by system; Mac/Windows - window closed
  - `2`: Windows - display device status changed (not triggered on other platforms)

**Sample Implementation**:
```objc
- (void)onScreenCaptureStopped:(int)reason {
    NSLog(@"Screen sharing stopped, reason: %d", reason);

    switch (reason) {
        case 0: // User stopped manually
            [self showToast:@"Screen sharing ended"];
            break;

        case 1: // Interrupted by system
            [self showToast:@"Screen sharing interrupted by system"];
            break;

        case 2: // Device status changed (Windows only)
            [self showToast:@"Display device status changed"];
            break;
    }

    [self updateScreenShareStatus:NO];
}
```

## 8. Local Recording Callbacks

### 📹 onLocalRecordBegin - Recording Started

```objc
- (void)onLocalRecordBegin:(NSInteger)errCode storagePath:(NSString *)storagePath;
```

**Description**: Notifies when local recording starts.

**Parameters**:
- `errCode`: Status code
  - `0`: Recording started successfully
  - `-1`: Internal error
  - `-2`: Invalid file extension (unsupported format)
  - `-6`: Recording already started, must stop first
  - `-7`: File exists, must delete first
  - `-8`: No write permission
- `storagePath`: Recording file path

**Sample Implementation**:
```objc
- (void)onLocalRecordBegin:(NSInteger)errCode storagePath:(NSString *)storagePath {
    if (errCode == 0) {
        NSLog(@"Local recording started successfully, file path: %@", storagePath);
        [self updateRecordStatus:YES];
    } else {
        NSLog(@"Local recording failed to start, error code: %ld", (long)errCode);
        [self handleRecordError:errCode];
    }
}
```

### 📹 onLocalRecording - Recording Progress

```objc
- (void)onLocalRecording:(NSInteger)durationMs storagePath:(NSString *)storagePath;
```

**Description**: Reports recording progress.

**Parameters**:
- `durationMs`: Duration in milliseconds
- `storagePath`: Recording file path

**Notes**:
- This callback is disabled by default
- Set the interval parameter when calling `startLocalRecording`

**Sample Implementation**:
```objc
- (void)onLocalRecording:(NSInteger)durationMs storagePath:(NSString *)storagePath {
    // Update recording duration display
    NSInteger seconds = durationMs / 1000;
    self.recordTimeLabel.text = [NSString stringWithFormat:@"Recording: %02ld:%02ld",
                                seconds / 60, seconds % 60];

    // Monitor long recording sessions
    if (seconds > 3600) { // Over 1 hour
        [self showLongRecordingWarning];
    }
}
```

### 📹 onLocalRecordComplete - Recording Completed

```objc
- (void)onLocalRecordComplete:(NSInteger)errCode storagePath:(NSString *)storagePath;
```

**Description**: Notifies when local recording ends.

**Parameters**:
- `errCode`: Status code
  - `0`: Recording ended successfully
  - `-1`: Recording failed
  - `-2`: Resolution/orientation change ended recording
  - `-3`: Duration too short or no audio/video captured
- `storagePath`: Recording file path

**Sample Implementation**:
```objc
- (void)onLocalRecordComplete:(NSInteger)errCode storagePath:(NSString *)storagePath {
    if (errCode == 0) {
        NSLog(@"Local recording completed, file path: %@", storagePath);
        [self showRecordSuccessAlert:storagePath];
    } else {
        NSLog(@"Local recording failed, error code: %ld", (long)errCode);
        [self handleRecordCompleteError:errCode];
    }

    [self updateRecordStatus:NO];
}
```

## 9. Advanced Feature Callbacks

### 🌐 onSetMixTranscodingConfig - Cloud Stream Mixing Status

```objc
- (void)onSetMixTranscodingConfig:(V2TXLiveCode)code message:(NSString *)msg;
```

**Description**: Reports the result of setting cloud stream mixing transcoding parameters.

**Parameters**:
- `code`: Result code
- `msg`: Error message (if any)

**Sample Implementation**:
```objc
- (void)onSetMixTranscodingConfig:(V2TXLiveCode)code message:(NSString *)msg {
    if (code == V2TXLIVE_OK) {
        NSLog(@"Cloud stream mixing configuration succeeded");
    } else {
        NSLog(@"Cloud stream mixing configuration failed: %@", msg);
        [self retryMixTranscodingConfig];
    }
}
```

### 📸 onSnapshotComplete - Snapshot Result

```objc
- (void)onSnapshotComplete:(nullable TXImage *)image;
```

**Description**: Notifies when a snapshot operation completes.

**Prerequisite**: Triggered after calling `snapshot`.

**Parameters**:
- `image`: Captured video frame (may be nil)

**Sample Implementation**:
```objc
- (void)onSnapshotComplete:(TXImage *)image {
    if (image) {
        // Save snapshot to photo album
        UIImageWriteToSavedPhotosAlbum(image, nil, nil, nil);

        // Display snapshot preview
        [self showSnapshotPreview:image];
    } else {
        NSLog(@"Snapshot failed");
    }
}
```

### 🎙️ onVoiceActivityDetectionUpdate - Voice Activity Detection

```objc
- (void)onVoiceActivityDetectionUpdate:(BOOL)active;
```

**Description**: Reports voice activity detection status.

**Prerequisite**: Enable via `enableVoiceActivityDetection`.

**Parameters**:
- `active`: YES if speaking detected, NO otherwise

**Sample Implementation**:
```objc
- (void)onVoiceActivityDetectionUpdate:(BOOL)active {
    if (active) {
        NSLog(@"Host started speaking detected");
        [self showSpeakingIndicator];
    } else {
        NSLog(@"Host stopped speaking detected");
        [self hideSpeakingIndicator];
    }
}
```

## 10. Usage Examples

### 🔧 Complete Live Pusher Callback Implementation

```objc
#import "V2TXLivePusherObserver.h"

@interface MyPusherObserver () <V2TXLivePusherObserver>
@end

@implementation MyPusherObserver

#pragma mark - Error and Warning Handling

- (void)onError:(V2TXLiveCode)code message:(NSString *)msg extraInfo:(NSDictionary *)extraInfo {
    NSLog(@"Live push error: %ld - %@", (long)code, msg);

    // Handle error based on code
    [self handlePushError:code message:msg];
}

- (void)onWarning:(V2TXLiveCode)code message:(NSString *)msg extraInfo:(NSDictionary *)extraInfo {
    NSLog(@"Live push warning: %ld - %@", (long)code, msg);

    // Display warning toast
    [self showWarningToast:msg];
}

#pragma mark - Push Status Monitoring

- (void)onPushStatusUpdate:(V2TXLivePushStatus)status message:(NSString *)msg extraInfo:(NSDictionary *)extraInfo {
    // Update UI status
    [self updatePushStatus:status];

    // Log status change
    [self logPushStatus:status message:msg];
}

- (void)onStatisticsUpdate:(V2TXLivePusherStatistics *)statistics {
    // Update statistics in UI
    [self updateStatsDisplay:statistics];

    // Auto-adjust performance
    [self autoAdjustBasedOnStats:statistics];
}

#pragma mark - Audio & Video Processing

- (void)onProcessAudioFrame:(V2TXLiveAudioFrame *)frame {
    // Real-time audio processing
    [self.audioProcessor processFrame:frame];
}

- (void)onProcessVideoFrame:(V2TXLiveVideoFrame *)srcFrame dstFrame:(V2TXLiveVideoFrame *)dstFrame {
    // Real-time beauty processing
    [self.beautyProcessor processFrame:srcFrame to:dstFrame];
}

#pragma mark - Recording Features

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

### 🎯 Best Practice Recommendations

**Thread Safety**
```objc
- (void)onStatisticsUpdate:(V2TXLivePusherStatistics *)statistics {
    // Always update UI on the main thread
    dispatch_async(dispatch_get_main_queue(), ^{
        [self updateStatsUI:statistics];
    });
}
```

**Performance Optimization**
```objc
- (void)onProcessAudioFrame:(V2TXLiveAudioFrame *)frame {
    // Keep callback logic lightweight
    @autoreleasepool {
        [self.lightweightProcessor process:frame];
    }
}
```

**Error Recovery**
```objc
- (void)onError:(V2TXLiveCode)code message:(NSString *)msg extraInfo:(NSDictionary *)extraInfo {
    if ([self isRecoverableError:code]) {
        [self scheduleReconnect];
    }
}
```

## 11. Callback Sequence Diagram

### 📊 Live Stream Lifecycle Callback Sequence

```
Live stream start:
1. onPushStatusUpdate(V2TXLivePushStatusConnecting)
2. onCaptureFirstVideoFrame (if video enabled)
3. onCaptureFirstAudioFrame (if audio enabled)
4. onPushStatusUpdate(V2TXLivePushStatusConnectSuccess)
5. onStatisticsUpdate (periodic)

Live stream stop:
1. onPushStatusUpdate(V2TXLivePushStatusDisconnected)
2. onGLContextDestroyed (if using OpenGL)
```

### 🔄 Status Transition Diagram

```
Initialize → Connecting → Connected → Streaming
                ↓
            Reconnecting → Connected
                ↓
            Disconnected
```