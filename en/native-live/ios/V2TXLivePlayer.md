> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

# Tencent Cloud Live Streaming SDK V2TXLivePlayer Playback API Documentation

## Feature Overview

`V2TXLivePlayer` is the primary interface for the Tencent Cloud Live Streaming (CSS) player. It pulls audio and video from a specified live stream URL, decodes the content, and renders playback on the local device.

**Platform Support**: iOS, macOS

## Core Features

### 🎯 Main Capabilities
- ✅ **Multi-Protocol Support**: HTTP-FLV, WebRTC, TRTC, HLS, RTMP
- ✅ **Video Control**: Rotation, Fill Mode, Mirroring
- ✅ **Playback Control**: Play/Stop, Pause/Resume, Volume Adjustment
- ✅ **Cache Optimization**: Automatic cache strategy adjustment
- ✅ **Seamless Switching**: Multi-resolution stream switching without interruption
- ✅ **Custom Processing**: Monitor audio/video data and implement custom rendering
- ✅ **Advanced Features**: Snapshot, SEI message handling, Picture-in-Picture, Local Recording

### 🔧 Technical Highlights
- **Low Latency**: Optimized caching and adaptive network handling
- **High Compatibility**: Supports a wide range of video encoding formats and resolutions
- **Easy Integration**: Streamlined API design and robust callback system
- **High Performance**: Hardware Decoding and efficient rendering pipeline

### Player Instance Creation
```objc
V2TXLivePlayer *player = [[V2TXLivePlayer alloc] init];
```

## API Details

### Basic Setup APIs

#### setObserver – Configure Player Callback
```objc
- (void)setObserver:(id<V2TXLivePlayerObserver>)observer;
```

**Parameters**:
- `observer`: Object that receives player callbacks; must implement the `V2TXLivePlayerObserver` protocol

**Recommended Usage**: Set immediately after initializing the player.

**Description**: Assign a callback to monitor player status, playback volume changes, first audio/video frame events, statistics, warnings, and error notifications.

**Example**:
```objc
[player setObserver:self];
```

#### setRenderView – Assign Video Rendering View
```objc
- (V2TXLiveCode)setRenderView:(TXView *)view;
```

**Parameters**:
- `view`: The view for video rendering; use UIView on iOS or NSView on macOS

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**Recommended Usage**: Set the rendering view before starting playback.

**Example**:
```objc
[player setRenderView:videoView];
```

#### setRenderRotation – Set Video Rotation
```objc
- (V2TXLiveCode)setRenderRotation:(V2TXLiveRotation)rotation;
```

**Parameters**:
- `rotation`: Rotation angle, see `V2TXLiveDef#V2TXLiveRotation`
  - `V2TXLiveRotation0` (Default): 0°, no rotation
  - `V2TXLiveRotation90`: 90° clockwise
  - `V2TXLiveRotation180`: 180° clockwise
  - `V2TXLiveRotation270`: 270° clockwise

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**Recommended Usage**: No restrictions.

**Example**:
```objc
[player setRenderRotation:V2TXLiveRotation0];    // No rotation
[player setRenderRotation:V2TXLiveRotation90];   // 90° clockwise
[player setRenderRotation:V2TXLiveRotation180];  // 180° clockwise
[player setRenderRotation:V2TXLiveRotation270];  // 270° clockwise
```

#### setRenderFillMode – Set Video Fill Mode
```objc
- (V2TXLiveCode)setRenderFillMode:(V2TXLiveFillMode)mode;
```

**Parameters**:
- `mode`: Fill mode, see `V2TXLiveDef#V2TXLiveFillMode`
  - `V2TXLiveFillModeFill` (Default): Fills the view, cropping content if aspect ratios differ
  - `V2TXLiveFillModeFit`: Fits the entire image, adding black borders if needed
  - `V2TXLiveFillModeScaleFill`: Stretches image to fill the view, may distort aspect ratio

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**Recommended Usage**: No restrictions.

**Example**:
```objc
[player setRenderFillMode:V2TXLiveFillModeFill];       // Fill view, crop if needed
[player setRenderFillMode:V2TXLiveFillModeFit];        // Fit image, add black borders
[player setRenderFillMode:V2TXLiveFillModeScaleFill];  // Stretch to fill
```

#### setRenderMirrorMode – Toggle Video Mirroring
```objc
- (V2TXLiveCode)setRenderMirrorMode:(BOOL)enable;
```

**Parameters**:
- `enable`: Enable horizontal mirroring during playback (Default: NO)

**Description**: When enabled, the video is flipped horizontally. You can toggle mirroring at any time.

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**Recommended Usage**: No restrictions.

**Example**:
```objc
[player setRenderMirrorMode:YES];  // Enable mirroring
[player setRenderMirrorMode:NO];   // Disable mirroring
```

### Playback Control APIs

#### startLivePlay – Start Stream Playback
```objc
- (V2TXLiveCode)startLivePlay:(NSString *)url;
```

**Parameters**:
- `url`: Stream playback URL; supports HTTP-FLV, WebRTC, TRTC, HLS, RTMP

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Playback started successfully
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: Invalid URL
- `V2TXLIVE_ERROR_REFUSED`: RTC does not support pushing and pulling the same StreamId on the same device simultaneously
- `V2TXLIVE_ERROR_INVALID_LICENSE`: Invalid license, playback failed

**Important Note**:  
- From version 10.7 onward, you must set the License using `V2TXLivePremier#setLicence` before playback; otherwise, playback will fail (black screen). Only set once globally.
- Supports Cloud Live Streaming License, Short Video License, and Video Playback License.

**Recommended Usage**: No restrictions.

**Example**:
```objc
V2TXLiveCode result = [player startLivePlay:@"http://example.com/live/stream_1080p.flv"];
if (result == V2TXLIVE_OK) {
    NSLog(@"Playback started successfully");
} else if (result == V2TXLIVE_ERROR_INVALID_PARAMETER) {
    NSLog(@"Invalid playback address");
} else if (result == V2TXLIVE_ERROR_REFUSED) {
    NSLog(@"Operation refused");
} else if (result == V2TXLIVE_ERROR_INVALID_LICENSE) {
    NSLog(@"Invalid License, please check your License");
}
```

#### stopPlay – Stop Stream Playback
```objc
- (V2TXLiveCode)stopPlay;
```

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**Recommended Usage**: Call after playback has started.

**Example**:
```objc
[player stopPlay];
```

#### isPlaying – Query Playback Status
```objc
- (int)isPlaying;
```

**Return Value**:
- `1`: Currently playing
- `0`: Playback stopped

**Recommended Usage**: No restrictions.

**Example**:
```objc
int isPlaying = [player isPlaying];
if (isPlaying == 1) {
    NSLog(@"Playing");
} else {
    NSLog(@"Playback stopped");
}
```

### Audio/Video Control APIs

#### pauseAudio – Pause Audio Playback
```objc
- (V2TXLiveCode)pauseAudio;
```

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**Recommended Usage**: No restrictions. If called before playback starts, only video will play (no audio).

**Example**:
```objc
[player pauseAudio];
```

#### resumeAudio – Resume Audio Playback
```objc
- (V2TXLiveCode)resumeAudio;
```

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**Recommended Usage**: No restrictions.

**Example**:
```objc
[player resumeAudio];
```

#### pauseVideo – Pause Video Playback
```objc
- (V2TXLiveCode)pauseVideo;
```

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**Recommended Usage**: No restrictions. If called before playback starts, only audio will play (no video).

**Example**:
```objc
[player pauseVideo];
```

#### resumeVideo – Resume Video Playback
```objc
- (V2TXLiveCode)resumeVideo;
```

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**Recommended Usage**: No restrictions.

**Example**:
```objc
[player resumeVideo];
```

#### setPlayoutVolume – Adjust Playback Volume
```objc
- (V2TXLiveCode)setPlayoutVolume:(NSUInteger)volume;
```

**Parameters**:
- `volume`: Volume level, range 0–100 (Default: 100)

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**Recommended Usage**: No restrictions.

**Example**:
```objc
[player setPlayoutVolume:50];
```

### Advanced Feature APIs

#### setCacheParams – Configure Cache Duration
```objc
- (V2TXLiveCode)setCacheParams:(CGFloat)minTime maxTime:(CGFloat)maxTime;
```

**Parameters**:
- `minTime`: Minimum cache duration (seconds), must be > 0 (Default: 1)
- `maxTime`: Maximum cache duration (seconds), must be > 0 (Default: 5)

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: minTime and maxTime must be greater than 0

**Optimization Tips**:
- Stable network: Use a smaller cache (1–3 seconds)
- Unstable network: Use a larger cache (3–5 seconds)
- No special requirements: Use default values

**Recommended Usage**: No restrictions.

**Example**:
```objc
[player setCacheParams:1.0 maxTime:5.0];
```

#### switchStream – Switch Stream Resolution Seamlessly (FLV and LEB Supported)
```objc
- (V2TXLiveCode)switchStream:(NSString *)newUrl;
```

**Parameters**:
- `newUrl`: URL of the stream with the desired resolution

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**Recommended Usage**: Call after playback has started.

**Example**:
```objc
[player setObserver:self];
[player startLivePlay:@"http://example.com/live/stream_1080p.flv"];
[player switchStream:@"http://example.com/live/stream_720p.flv"];

#pragma mark - V2TXLivePlayerObserver
- (void)onStreamSwitched:(V2TXLivePlayer *)player url:(NSString *)url code:(V2TXLiveCode)code {
    if (code == V2TXLIVE_OK) {
        NSLog(@"Stream switched successfully, current playback address: %@", url);
    } else if (code == V2TXLIVE_ERROR_STREAM_SWITCH_FAIL) {
        NSLog(@"Stream switch failed, timeout");
    } else if (code == V2TXLIVE_ERROR_STREAM_SWITCH_SERVER_ERROR) {
        NSLog(@"Stream switch failed, server error");
    } else if (code == V2TXLIVE_ERROR_STREAM_SWITCH_CLIENT_ERROR) {
        NSLog(@"Stream switch failed, client error");
    }
}
```

#### getStreamList – Retrieve Available Stream Qualities (HLS Supported)
```objc
- (NSArray<V2TXLiveStreamInfo *> *)getStreamList;
```

**Return Value**: Array of stream info objects, representing available qualities

**Recommended Usage**: Call after playback has started.

**Example**:
```objc
[player startLivePlay:@"http://example.com/live/stream_1080p.m3u8"];
NSArray<V2TXLiveStreamInfo *> *streamList = [player getStreamList];
```

#### enableVolumeEvaluation – Enable Playback Volume Level Callback
```objc
- (V2TXLiveCode)enableVolumeEvaluation:(NSUInteger)intervalMs;
```

**Parameters**:
- `intervalMs`: Interval (ms) for `onPlayoutVolumeUpdate` callback. Minimum: 100ms. Set ≤0 to disable. Recommended: 300ms (Default: 0, disabled)

**Description**: When enabled, you receive periodic volume level updates via `V2TXLivePlayerObserver`.

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**Recommended Usage**: No restrictions.

**Example**:
```objc
[player setObserver:self];
[player enableVolumeEvaluation:300];

#pragma mark - V2TXLivePlayerObserver
- (void)onPlayoutVolumeUpdate:(int)volume {
    // Handle volume update
}
```

#### snapshot – Capture Video Frame During Playback
```objc
- (V2TXLiveCode)snapshot;
```

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success
- `V2TXLIVE_ERROR_REFUSED`: Snapshot not allowed when player is stopped

**Recommended Usage**: Call after playback has started.

**Example**:
```objc
[player setObserver:self];
[player snapshot];

#pragma mark - V2TXLivePlayerObserver
- (void)onSnapshotComplete:(UIImage *)image {
    // Handle snapshot result
}
```

#### enableObserveVideoFrame – Enable Custom Video Rendering
```objc
- (V2TXLiveCode)enableObserveVideoFrame:(BOOL)enable 
                          pixelFormat:(V2TXLivePixelFormat)pixelFormat 
                           bufferType:(V2TXLiveBufferType)bufferType;
```

**Parameters**:
- `enable`: Enable custom rendering (Default: NO)
- `pixelFormat`: Pixel format for callback, see `V2TXLiveDef#V2TXLivePixelFormat`
- `bufferType`: Data format for callback, see `V2TXLiveDef#V2TXLiveBufferType`

**Description**:  
- When enabled, the SDK stops rendering video frames internally. You receive frames via `V2TXLivePlayerObserver` for custom rendering.
- Supported combinations:
  - V2TXLivePixelFormatTexture2D + V2TXLiveBufferTypeTexture (Recommended)
  - V2TXLivePixelFormatI420 + V2TXLiveBufferTypeByteArray
  - V2TXLivePixelFormatI420 + V2TXLiveBufferTypeByteBuffer

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success
- `V2TXLIVE_ERROR_NOT_SUPPORTED`: Unsupported pixel/data format

**Recommended Usage**: Set before playback starts.

**Example**:
```objc
[player enableObserveVideoFrame:YES 
                     pixelFormat:V2TXLivePixelFormatTexture2D 
                      bufferType:V2TXLiveBufferTypeTexture];
[player setObserver:self];

#pragma mark - V2TXLivePlayerObserver
- (void)onRenderVideoFrame:(V2TXLiveVideoFrame *)videoFrame {
    // Custom rendering
}
```

#### enableObserveAudioFrame – Enable Audio Data Callback
```objc
- (V2TXLiveCode)enableObserveAudioFrame:(BOOL)enable;
```

**Parameters**:
- `enable`: Enable audio data callback (Default: NO)

**Description**: When enabled, you receive audio data via `V2TXLivePlayerObserver` for custom processing.

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**Recommended Usage**: Set before playback starts.

**Example**:
```objc
[player enableObserveAudioFrame:YES];
[player setObserver:self];

#pragma mark - V2TXLivePlayerObserver
- (void)onPlayoutAudioFrame:(V2TXLiveAudioFrame *)audioFrame {
    // Handle audio data
}
```

#### enableReceiveSeiMessage – Enable SEI Message Reception
```objc
- (V2TXLiveCode)enableReceiveSeiMessage:(BOOL)enable payloadType:(int)payloadType;
```

**Parameters**:
- `enable`: YES to enable, NO to disable (Default: NO)
- `payloadType`: SEI payload type; supported values: 5, 242, 243. Must match sender's payloadType.

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**Recommended Usage**: Set before playback starts.

**Example**:
```objc
[player enableReceiveSeiMessage:YES payloadType:5];
[player enableReceiveSeiMessage:YES payloadType:242];
[player enableReceiveSeiMessage:YES payloadType:243];
[player setObserver:self];

#pragma mark - V2TXLivePlayerObserver
- (void)onReceiveSeiMessage:(int)payloadType data:(NSData *)data {
    // Handle SEI message
}
```

#### enablePictureInPicture – Enable Picture-in-Picture (iOS Only)
```objc
- (V2TXLiveCode)enablePictureInPicture:(BOOL)enable;
```

**Parameters**:
- `enable`: YES to enable, NO to disable (Default: NO)

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**Recommended Usage**: No restrictions.

**Description**: Available only on iOS. Not supported on macOS.

**Example**:
```objc
[player enablePictureInPicture:YES];
```

#### startLocalRecording – Record Audio/Video Stream Locally
```objc
- (V2TXLiveCode)startLocalRecording:(V2TXLiveLocalRecordingParams *)params;
```

**Parameters**:
- `params`: See `V2TXLiveDef.h` for details

**Important Notes**:
- Recording can only begin after stream playback has started; starting recording before playback is invalid.
- Do not switch between software and hardware decoding during recording, or the output file may be corrupted.

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: Invalid parameter (e.g., empty filePath)
- `V2TXLIVE_ERROR_REFUSED`: Stream not playing, operation refused

**Recommended Usage**: Call after playback has started.

**Example**:
```objc
[player setObserver:self];

#pragma mark - V2TXLivePlayerObserver
- (void)onLocalRecordBegin:(int)code storagePath:(NSString *)storagePath {
    NSLog(@"Recording started");
}

- (void)onLocalRecording:(long)durationMs storagePath:(NSString *)storagePath {
    NSLog(@"Recording..., durationMs: %ld", durationMs);
}

- (void)onLocalRecordComplete:(int)code storagePath:(NSString *)storagePath {
    NSLog(@"Recording completed");
}

V2TXLiveLocalRecordingParams *params = [[V2TXLiveLocalRecordingParams alloc] init];
params.filePath = @"filepath";
params.interval = 2000;
V2TXLiveCode code = [player startLocalRecording:params];
if (code == V2TXLIVE_OK) {
    NSLog(@"Recording started successfully");
} else if (code == V2TXLIVE_ERROR_INVALID_PARAMETER) {
    NSLog(@"Invalid recording parameters");
} else if (code == V2TXLIVE_ERROR_REFUSED) {
    NSLog(@"Recording operation refused");
}
```

#### stopLocalRecording – Stop Local Recording
```objc
- (void)stopLocalRecording;
```

**Description**: If playback stops while recording is active, the SDK will automatically stop recording.

**Recommended Usage**: Call after playback and recording have started.

**Example**:
```objc
[player stopLocalRecording];
```

#### showDebugView – Display Player Debug Overlay
```objc
- (void)showDebugView:(BOOL)isShow;
```

**Parameters**:
- `isShow`: Show debug overlay (Default: NO)

**Recommended Usage**: No restrictions.

**Example**:
```objc
[player showDebugView:YES];
```

#### setProperty – Access Advanced Player Features
```objc
- (V2TXLiveCode)setProperty:(NSString *)key value:(NSObject *)value;
```

**Parameters**:
- `key`: Advanced feature key
- `value`: Value for the advanced feature

**Description**: For advanced usage. Contact your business or solution architect for details.

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: Key cannot be nil

## Code Example

```objc
// Create player instance
V2TXLivePlayer *player = [[V2TXLivePlayer alloc] init];

// Set callback
[player setObserver:self];

// Set rendering view
[player setRenderView:videoView];

// Start playback
V2TXLiveCode result = [player startLivePlay:@"rtmp://example.com/live/stream"];
if (result == V2TXLIVE_OK) {
    // Playback successful
}

// Pause video
[player pauseVideo];

// Resume video
[player resumeVideo];

// Stop playback
[player stopPlay];
```

## Notes

1. **License Requirement**: From version 10.7, you must set a valid License for playback to work.
2. **Permission Requirement**: Network and audio playback permissions are required.
3. **Thread Safety**: All API calls must be made on the main thread.
4. **Memory Management**: Release player resources promptly to prevent memory leaks.
5. **Platform Differences**: Picture-in-Picture is supported only on iOS, not on macOS.

## Related Interfaces

- `V2TXLivePlayerObserver`: Player callback interface
- `V2TXLiveCode`: Error and status code definitions
- `V2TXLiveDef`: Data structure and enum definitions
- `V2TXLivePremier`: SDK global management interface