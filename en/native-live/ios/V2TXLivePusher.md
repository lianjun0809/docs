> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

Tencent Cloud Live Streaming SDK V2TXLivePusher Streaming API Documentation

## Overview

`V2TXLivePusher` is the primary streaming interface in the Tencent Cloud Live Streaming SDK. It handles encoding of local audio and video frames and pushes them to a specified streaming URL. Compatible with any streaming server.

**Supported Platforms**: iOS, macOS  
**Features**: Stream control, audio/video capture, effects processing, cloud stream mixing, local recording

## 📋 Table of Contents

### 1. Core Feature Highlights
### 2. Pusher Initialization
### 3. Video Preview & Rendering
### 4. Audio/Video Capture Control
### 5. Streaming Control APIs
### 6. Audio/Video Quality Control
### 7. Effects & Device Management
### 8. Advanced Feature APIs
### 9. Cloud Stream Mixing & Recording
### 10. Usage Examples

## 1. Core Feature Highlights

### 🎯 Main Capabilities

- **Custom Video Capture**: Supports custom audio and video input sources
- **Beauty Filters & Stickers**: Includes multiple beauty algorithms and color filters
- **QoS Traffic Control**: Adapts to upstream network conditions
- **AI Face Effects**: Features like eye enlargement, face slimming, and nose enhancement powered by Youtu AI
- **Cloud Stream Mixing (MixTranscoding)**: Combines multiple audio/video streams into a single live stream
- **Local Recording**: Records audio and video streams locally

### 🔧 Technical Specifications

- **Supported Protocols**: RTMP, RTC
- **Platform Compatibility**: iOS 11.0+, macOS
- **Encoding Formats**: H.264/H.265 for video, AAC for audio
- **Resolution**: Up to 4K Ultra HD
- **Frame Rate**: Adaptive, 15–60 fps

## 2. Pusher Initialization

### initWithLiveMode – Initialize Pusher

**Parameters**:
- `liveMode`: Streaming protocol
  - `V2TXLiveModeRTMP`: RTMP protocol (default)
  - `V2TXLiveModeRTC`: RTC protocol

**Usage**: Call during app initialization

**Example**:
```objc
// Create RTMP streaming instance; startPush must use an RTMP URL
V2TXLivePusher *pusher = [[V2TXLivePusher alloc] initWithLiveMode:V2TXLiveModeRTMP];

// Create RTC streaming instance; startPush must use an RTC URL
V2TXLivePusher *pusher = [[V2TXLivePusher alloc] initWithLiveMode:V2TXLiveModeRTC];
```

### setObserver – Set Pusher Observer

```objc
- (void)setObserver:(id<V2TXLivePusherObserver>)observer;
```

**Parameters**:
- `observer`: Object conforming to V2TXLivePusherObserver protocol

**Usage**: Set immediately after initializing the pusher

**Notes**:
- The observer must remain valid for the duration of the streaming session
- Receives streaming status, statistics, warnings, and error notifications

## 3. Video Preview & Rendering

### setRenderView – Configure Local Camera Preview

```objc
- (V2TXLiveCode)setRenderView:(TXView *)view;
```

**Parameters**:
- `view`: View for local camera preview

**Usage**: Set before starting the stream

**Description**: Displays the local camera feed with applied beauty, face shaping, filters, and other effects

### setRenderMirror – Configure Preview Mirroring

```objc
- (V2TXLiveCode)setRenderMirror:(V2TXLiveMirrorType)mirrorType;
```

**Function**: Sets mirroring for the local camera preview

**Parameters**:
- `mirrorType`:
  - `V2TXLiveMirrorTypeAuto`: Default (front camera mirrored, rear camera not mirrored)
  - `V2TXLiveMirrorTypeEnable`: Both cameras mirrored
  - `V2TXLiveMirrorTypeDisable`: No mirroring

### setEncoderMirror – Configure Encoding Mirroring

```objc
- (V2TXLiveCode)setEncoderMirror:(BOOL)mirror;
```

**Function**: Sets mirroring for the encoded video, affecting what the audience sees

**Parameters**:
- `mirror`: 
  - `NO`: Audience sees non-mirrored video (default)
  - `YES`: Audience sees mirrored video

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**Difference**:
- `setRenderMirror`: Affects only local preview
- `setEncoderMirror`: Affects the audience view

**Usage**: No restrictions

**Example**:
```objc
// Audience sees mirrored video
[pusher setEncoderMirror:YES];
// Audience sees non-mirrored video
[pusher setEncoderMirror:NO];
```

### setRenderRotation – Configure Preview Rotation

```objc
- (V2TXLiveCode)setRenderRotation:(V2TXLiveRotation)rotation;
```

**Function**: Sets the rotation angle for the local camera preview

**Parameters**:
- `rotation`:
  - `V2TXLiveRotation0`: No rotation (default)
  - `V2TXLiveRotation90`: 90° clockwise
  - `V2TXLiveRotation180`: 180° clockwise
  - `V2TXLiveRotation270`: 270° clockwise

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**Description**: Rotates only the local preview, does not affect the streamed video

**Usage**: No restrictions

**Example**:
```objc
[pusher setRenderRotation:V2TXLiveRotation0];
[pusher setRenderRotation:V2TXLiveRotation90];
[pusher setRenderRotation:V2TXLiveRotation180];
[pusher setRenderRotation:V2TXLiveRotation270];
```

### setRenderFillMode – Configure Preview Fill Mode

```objc
- (V2TXLiveCode)setRenderFillMode:(V2TXLiveFillMode)mode;
```

**Function**: Sets how the local camera preview fits the view

**Parameters**:
- `mode`:
  - `V2TXLiveFillModeFill`: Fills screen, may crop (default)
  - `V2TXLiveFillModeFit`: Fits screen, preserves full image, may show black bars
  - `V2TXLiveFillModeScaleFill`: Stretches to fill, may distort

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**Description**: Affects only local preview, not the streamed video

**Usage**: No restrictions

**Example**:
```objc
[pusher setRenderFillMode:V2TXLiveFillModeFill];
[pusher setRenderFillMode:V2TXLiveFillModeFit];
[pusher setRenderFillMode:V2TXLiveFillModeScaleFill];
```

### startCamera – Enable Local Camera

```objc
// iOS
- (V2TXLiveCode)startCamera:(BOOL)frontCamera;

// macOS
- (V2TXLiveCode)startCamera:(NSString *)cameraId;
```

**Parameters**:
- **iOS**: `frontCamera` – Use front camera
- **macOS**: `cameraId` – Camera identifier

**Important**:
- Enable at least one capture source before streaming, or streaming will fail
- Only one capture source can be active per pusher instance: `startVirtualCamera`, `startCamera`, or `startScreenCapture`
- To switch sources, stop the current one before starting another

**Usage**: Call before streaming

### startMicrophone – Enable Microphone

```objc
- (V2TXLiveCode)startMicrophone;
```

**Use Cases**:
- Audio/video streaming: Use with camera capture
- Audio-only streaming: Use microphone alone
- Screen sharing: Use with screen capture for system and mic audio

**Notes**:
- Must call before streaming to enable microphone capture, or only video will be streamed
- Microphone capture can be enabled/disabled dynamically during streaming

**Usage**: Call before streaming

### startVirtualCamera – Enable Image Streaming

```objc
- (V2TXLiveCode)startVirtualCamera:(TXImage *)image;
```

**Parameters**:
- `image`: Image to stream

**Use Cases**:
- Stream a static image as video source
- Display maintenance page during downtime
- Show advertisement images

**Notes**:
- Must call before streaming to enable image streaming, or streaming will fail
- Image is encoded as video and uses bandwidth
- Typically used with microphone capture for audio
- Cannot enable image streaming and camera capture at the same time

**Usage**: Call before streaming

### startScreenCapture – Enable Screen Capture

```objc
- (V2TXLiveCode)startScreenCapture:(NSString *)appGroup;
```

**Parameters**:
- `appGroup`: App Group Identifier shared between main app and broadcast extension

**Use Cases**:
- Share device screen via live streaming
- Online teaching: share teacher’s screen
- Game streaming: share gameplay
- App demo: show app workflows

**Notes**:
- Must call before streaming to enable screen capture, or streaming will fail
- iOS requires screen recording permission
- Can be used with `startSystemAudioLoopback()` to capture system audio
- Cannot enable screen capture and camera capture simultaneously

**Usage**: Call before streaming

### Stop Capture APIs

```objc
- (V2TXLiveCode)stopCamera;
- (V2TXLiveCode)stopMicrophone;
- (V2TXLiveCode)stopVirtualCamera;
- (V2TXLiveCode)stopScreenCapture;
```

## 5. Streaming Control APIs

### startPush – Start Streaming

```objc
- (V2TXLiveCode)startPush:(NSString *)url;
```

**Parameters**:
- `url`: Streaming URL (supports any streaming server)

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success, starts connecting to the streaming URL
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: Invalid URL
- `V2TXLIVE_ERROR_INVALID_LICENSE`: Invalid license, authentication failed
- `V2TXLIVE_ERROR_REFUSED`: RTC does not support simultaneous push/pull of the same StreamId on one device

**Important**:
- Enable at least one capture source before calling `startPush()`, or streaming will fail
- Supported sources: camera, microphone, screen, image streaming, custom capture
- You can switch capture sources during streaming, but must stop the current source before starting a new one

**Usage**: After enabling a capture source

### stopPush – Stop Streaming

```objc
- (V2TXLiveCode)stopPush;
```

**Function**: Stops pushing audio/video data

**Return Value**:
- `V2TXLIVE_OK`: Success

### isPushing – Check Streaming Status

```objc
- (int)isPushing;
```

**Function**: Checks if streaming is active

**Return Value**:
- `1`: Streaming in progress
- `0`: Streaming stopped

## 6. Audio/Video Quality Control

### setAudioQuality – Configure Audio Quality

```objc
- (V2TXLiveCode)setAudioQuality:(V2TXLiveAudioQuality)quality;
```

**Parameters**:
- `quality`:
  - `V2TXLiveAudioQualityDefault`: General audio quality (default)
  - `V2TXLiveAudioQualitySpeech`: Optimized for speech
  - `V2TXLiveAudioQualityMusic`: Optimized for music

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success
- `V2TXLIVE_ERROR_REFUSED`: Cannot change audio quality during streaming

**Usage**: Set before starting streaming

**Example**:
```objc
[pusher setAudioQuality:V2TXLiveAudioQualityDefault];   // General quality
[pusher setAudioQuality:V2TXLiveAudioQualitySpeech];    // For voice chat
[pusher setAudioQuality:V2TXLiveAudioQualityMusic];     // For music streaming
```

### setVideoQuality – Configure Video Encoding Parameters

```objc
- (V2TXLiveCode)setVideoQuality:(V2TXLiveVideoEncoderParam *)param;
```

**Parameters**:
- `param`: Video encoding parameters

**Configurable Options**:
- Resolution, bitrate, frame rate
- Encoding mode (Software Encoding/Hardware Encoding)
- Encoding complexity

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success
- `V2TXLIVE_ERROR_REFUSED`: Cannot change video quality during streaming

**Usage**: Set before starting streaming

**Example**:
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

### pauseAudio / resumeAudio – Pause/Resume Audio Stream

```objc
- (V2TXLiveCode)pauseAudio;
- (V2TXLiveCode)resumeAudio;
```

**Use Cases**:
- Temporarily mute the host
- Maintain audio continuity for MP4 recording
- Switch from microphone to background music

**Notes**:
- Unlike `stopMicrophone()`, this does not interrupt the audio stream; silent packets are sent at low bitrate
- Audio stream remains, but content is silent during pause
- Useful for scenarios requiring uninterrupted audio during recording

**Usage**: During streaming

### pauseVideo / resumeVideo – Pause/Resume Video Stream

```objc
- (V2TXLiveCode)pauseVideo;
- (V2TXLiveCode)resumeVideo;
```

**Use Cases**:
- Temporarily black out the video feed
- Switch from camera to image streaming
- Hide video for privacy

**Notes**:
- Video stream remains, but content is black screen or last frame during pause
- Useful for scenarios requiring uninterrupted video stream

**Usage**: During streaming

## 7. Effects & Device Management

### getAudioEffectManager – Audio Effects Manager

```objc
- (TXAudioEffectManager *)getAudioEffectManager;
```

**Function**: Returns the audio effects manager

**Features**:
- Adjust microphone volume
- Set reverb and voice changer effects
- Enable ear monitoring and adjust monitor volume
- Add background music and control playback effects

### getBeautyManager – Beauty Manager

```objc
- (TXBeautyManager *)getBeautyManager;
```

**Function**: Returns the beauty manager

**Features**:
- Basic beauty: style, whitening, rosy skin
- Face shaping: eye enlargement, face slimming, V-face, chin, short face
- Detail optimization: nose slimming, bright eyes, white teeth, remove eye bags, remove wrinkles
- Face effects: accessories, makeup, gesture recognition

### getDeviceManager – Device Manager

```objc
- (TXDeviceManager *)getDeviceManager;
```

**Function**: Returns the device manager

**Features**:
- Switch front/rear camera
- Set autofocus
- Adjust camera zoom
- Toggle flashlight
- Switch between headset and speaker
- Change volume type

## 8. Advanced Feature APIs

### snapshot – Capture Local Frame

```objc
- (V2TXLiveCode)snapshot;
```

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success
- `V2TXLIVE_ERROR_REFUSED`: Streaming stopped, cannot capture snapshot

**Usage**: After streaming starts

### setWatermark – Configure Watermark

```objc
- (V2TXLiveCode)setWatermark:(TXImage *)image x:(float)x y:(float)y scale:(float)scale;
```

**Function**: Adds a watermark to the stream

**Parameters**:
- `image`: Watermark image (nil to disable)
- `x`: Horizontal position (0–1)
- `y`: Vertical position (0–1)
- `scale`: Scale (0–1)

### enableVolumeEvaluation – Enable Volume Level Notifications

```objc
- (V2TXLiveCode)enableVolumeEvaluation:(NSUInteger)intervalMs;
```

**Function**: Enables microphone volume level notifications

**Parameters**:
- `intervalMs`: Callback interval (min 100ms, recommended 300ms)

**Usage**: Get volume updates via `onMicrophoneVolumeUpdate` callback

### sendSeiMessage – Send SEI Message

```objc
- (V2TXLiveCode)sendSeiMessage:(int)payloadType data:(NSData *)data;
```

**Function**: Sends SEI (Supplemental Enhancement Information) messages

**Parameters**:
- `payloadType`: Data type (supports 5, 242; 242 recommended)
- `data`: Data to send

**Receiver**: Player receives via `onReceiveSeiMessage` callback

### showDebugView – Show Debug Dashboard

```objc
- (void)showDebugView:(BOOL)isShow;
```

**Function**: Shows or hides the debug dashboard

**Parameters**:
- `isShow`: Show dashboard (default NO)

## 9. Custom Capture APIs

### enableCustomVideoCapture – Enable/Disable Custom Video Capture

```objc
- (V2TXLiveCode)enableCustomVideoCapture:(BOOL)enable;
```

**Parameters**:
- `enable`: Enable (true) or disable (false) custom capture [default: false]

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**Use Cases**:
- Capture from external cameras or capture cards
- Pre-process video before streaming
- Compose multiple video sources into one stream
- Stream special video formats

**Notes**:
- Call before streaming to enable custom capture, or streaming will fail
- Must be called before `startPush`
- In custom capture mode, the SDK only encodes and transmits; it does not capture

**Usage**: Before starting streaming

**Example**:
```objc
[pusher enableCustomVideoCapture:YES];  // Enable
[pusher enableCustomVideoCapture:NO];   // Disable
```

### enableCustomAudioCapture – Enable/Disable Custom Audio Capture

```objc
- (V2TXLiveCode)enableCustomAudioCapture:(BOOL)enable;
```

**Parameters**:
- `enable`: Enable (true) or disable (false) custom capture [default: false]

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**Use Cases**:
- Capture from external microphones or audio interfaces
- Pre-process audio before streaming
- Combine multiple audio sources
- Stream special audio formats

**Notes**:
- Call before streaming to enable custom capture, or streaming will fail
- Must be called before `startPush`
- In custom capture mode, the SDK only encodes and transmits; it does not capture

**Usage**: Before starting streaming

**Example**:
```objc
[pusher enableCustomAudioCapture:YES];  // Enable
[pusher enableCustomAudioCapture:NO];   // Disable
```

### sendCustomVideoFrame – Send Custom Video Frame

```objc
- (V2TXLiveCode)sendCustomVideoFrame:(V2TXLiveVideoFrame *)videoFrame;
```

**Function**: Sends video data to the SDK in custom capture mode

**Prerequisite**: Enable custom video capture first

### sendCustomAudioFrame – Send Custom Audio Frame

```objc
- (V2TXLiveCode)sendCustomAudioFrame:(V2TXLiveAudioFrame *)audioFrame;
```

**Function**: Sends audio data to the SDK in custom capture mode

### enableCustomVideoProcess – Enable Custom Video Processing

```objc
- (V2TXLiveCode)enableCustomVideoProcess:(BOOL)enable 
                            pixelFormat:(V2TXLivePixelFormat)pixelFormat 
                            bufferType:(V2TXLiveBufferType)bufferType;
```

**Function**: Enables or disables custom video processing

**Supported Format Combinations**:
- `V2TXLivePixelFormatTexture2D` + `V2TXLiveBufferTypeTexture`
- `V2TXLivePixelFormatNV12` + `V2TXLiveBufferTypePixelBuffer`
- `V2TXLivePixelFormatBGRA32` + `V2TXLiveBufferTypePixelBuffer`

### enableAudioProcessObserver – Enable Audio Frame Observer

```objc
- (V2TXLiveCode)enableAudioProcessObserver:(BOOL)enable 
                                  format:(V2TXLiveAudioFrameObserverFormat *)format;
```

**Function**: Enables or disables observer for preprocessed local audio frames

**Usage**: Call before `startPush`

## 10. Cloud Stream Mixing & Recording

### setMixTranscodingConfig – Configure Cloud Stream Mixing

```objc
- (V2TXLiveCode)setMixTranscodingConfig:(V2TXLiveTranscodingConfig *)config;
```

**Parameters**:
- `config`: MixTranscoding configuration; pass nil to cancel cloud stream mixing

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success
- `V2TXLIVE_ERROR_REFUSED`: Cannot set MixTranscoding parameters if streaming hasn't started

**Mixing Principle**:
```
[Video 1] => Decoding ====> \
                             \
[Video 2] => Decoding =>  Video Mixing => Encoding => [Mixed Video]
                             /
[Video 3] => Decoding ====> /

[Audio 1] => Decoding ====> \
                             \
[Audio 2] => Decoding =>  Audio Mixing => Encoding => [Mixed Audio]
                             /
[Audio 3] => Decoding ====> /
```

**Important**:
- Only RTC protocol supports stream mixing; not available for RTMP or other protocols
- Cloud stream mixing adds 1–2 seconds CDN latency
- Pass nil promptly to cancel mixing and avoid extra charges

**Usage**: During streaming

**Example**:
```objc
V2TXLiveTranscodingConfig *config = [[V2TXLiveTranscodingConfig alloc] init];
config.videoWidth = 720;
config.videoHeight = 1280;
config.videoBitrate = 1500;
config.videoFps = 15;
config.videoGOP = 3;
config.backgroundColor = 0x000000;
config.backgroundImage = nil;

V2TXLiveMixUser *user1 = [[V2TXLiveMixUser alloc] init];
user1.userId = @"user1";
user1.x = 0;
user1.y = 0;
user1.width = 0.5;
user1.height = 1.0;
user1.zOrder = 0;

config.mixUsers = @[user1];

V2TXLiveCode result = [pusher setMixTranscodingConfig:config];
if (result == V2TXLIVE_OK) {
    NSLog(@"MixTranscoding configuration set successfully");
}

result = [pusher setMixTranscodingConfig:nil];
if (result == V2TXLIVE_OK) {
    NSLog(@"MixTranscoding configuration cancelled successfully");
}
```

### startLocalRecording – Start Local Recording

```objc
- (V2TXLiveCode)startLocalRecording:(V2TXLiveLocalRecordingParams *)params;
```

**Parameters**:
- `params`: Local recording settings

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: Invalid parameters
- `V2TXLIVE_ERROR_REFUSED`: Cannot record before streaming starts

**Usage**: After streaming starts

**Notes**:
- Recording only starts when streaming is active; starting recording when not streaming has no effect
- Do not change resolution or encoding mode (Software/Hardware Encoding) during recording
- If streaming stops during recording, the SDK automatically ends recording

**Example**:
```objc
[pusher setObserver:self];

V2TXLiveLocalRecordingParams *params = [[V2TXLiveLocalRecordingParams alloc] init];
params.filePath = @"/path/to/record/file.mp4";
params.recordType = V2TXLiveRecordTypeBoth;
params.interval = 2000;

V2TXLiveCode result = [pusher startLocalRecording:params];
if (result == V2TXLIVE_OK) {
    NSLog(@"Local recording started successfully");
} else if (result == V2TXLIVE_ERROR_INVALID_PARAMETER) {
    NSLog(@"Invalid recording parameters");
} else if (result == V2TXLIVE_ERROR_REFUSED) {
    NSLog(@"Recording request denied, please start streaming first");
}

// Recording status callbacks
- (void)onLocalRecordBegin:(int)code storagePath:(NSString *)storagePath {
    if (code == V2TXLIVE_OK) {
        NSLog(@"Recording started, storage path: %@", storagePath);
    }
}

- (void)onLocalRecording:(long)durationMs storagePath:(NSString *)storagePath {
    NSLog(@"Recording in progress, duration: %ldms", durationMs);
}

- (void)onLocalRecordComplete:(int)code storagePath:(NSString *)storagePath {
    if (code == V2TXLIVE_OK) {
        NSLog(@"Recording completed, storage path: %@", storagePath);
    }
}
```

### stopLocalRecording – Stop Recording

```objc
- (void)stopLocalRecording;
```

**Function**: Stops recording the audio/video stream

**Automatic Handling**: If streaming stops during recording, the SDK ends recording automatically

### enableVoiceActivityDetection – Enable Voice Activity Detection

```objc
- (void)enableVoiceActivityDetection:(BOOL)enable;
```

**Function**: Enables voice activity detection

**Callback**: Voice activity status is reported via `OnVoiceActivityDetectionUpdate` callback

## 11. Advanced API Interfaces

### setProperty / getProperty – Advanced Property Configuration

```objc
- (V2TXLiveCode)setProperty:(NSString *)key value:(NSObject *)value;
- (NSString *)getProperty:(NSString *)key;
```

**Function**: Set or get advanced/exploratory SDK properties

**Usage**: Access experimental features or advanced settings

**Reference**: See definitions in `V2TXLiveProperty.h`

## 12. Usage Examples

### Basic Streaming Example

```objc
// 1. Initialize pusher
V2TXLivePusher *pusher = [[V2TXLivePusher alloc] initWithLiveMode:V2TXLiveModeRTMP];

// 2. Set observer
[pusher setObserver:self];

// 3. Set preview view
[pusher setRenderView:self.previewView];

// 4. Enable camera and microphone
[pusher startCamera:YES];  // iOS front camera
[pusher startMicrophone];

// 5. Start streaming
NSString *pushUrl = @"rtmp://your-push-url/live/stream";
V2TXLiveCode result = [pusher startPush:pushUrl];

if (result == V2TXLIVE_OK) {
    NSLog(@"Streaming started successfully");
} else {
    NSLog(@"Streaming failed to start, error code: %ld", (long)result);
}
```

### Beauty Effects Configuration Example

```objc
TXBeautyManager *beautyManager = [pusher getBeautyManager];

[beautyManager setBeautyStyle:TXBeautyStyleNature];
[beautyManager setBeautyLevel:6.0];
[beautyManager setWhitenessLevel:3.0];
[beautyManager setRuddyLevel:2.0];

[beautyManager setEyeScaleLevel:3.0];      // Eye enlargement
[beautyManager setFaceSlimLevel:4.0];      // Face slimming
[beautyManager setFaceVLevel:2.0];         // V-face
```

### Cloud Stream Mixing Configuration Example

```objc
V2TXLiveTranscodingConfig *config = [[V2TXLiveTranscodingConfig alloc] init];
config.videoWidth = 720;
config.videoHeight = 1280;
config.videoBitrate = 1500;
config.videoFramerate = 15;
config.videoGOP = 3;
config.backgroundColor = 0x000000;
config.backgroundImage = nil;

V2TXLiveMixUser *user1 = [[V2TXLiveMixUser alloc] init];
user1.userId = @"user1";
user1.x = 0;
user1.y = 0;
user1.width = 0.5;
user1.height = 1.0;
user1.zOrder = 0;

config.mixUsers = @[user1];

[pusher setMixTranscodingConfig:config];
```

### Custom Capture Example

```objc
[pusher enableCustomVideoCapture:YES];

V2TXLiveVideoFrame *videoFrame = [[V2TXLiveVideoFrame alloc] init];
videoFrame.pixelFormat = V2TXLivePixelFormatNV12;
videoFrame.bufferType = V2TXLiveBufferTypePixelBuffer;
videoFrame.data = pixelBufferData;
videoFrame.width = 720;
videoFrame.height = 1280;
videoFrame.rotation = V2TXLiveRotation0;

[pusher sendCustomVideoFrame:videoFrame];
```

## 13. Usage Examples

### Basic Streaming Example (Camera + Microphone)
```objc
V2TXLivePusher *pusher = [[V2TXLivePusher alloc] initWithLiveMode:V2TXLiveModeRTMP];

[pusher setObserver:self];
[pusher setRenderView:self.previewView];

// At least one capture source must be enabled before streaming
[pusher startCamera:YES];
[pusher startMicrophone];

NSString *pushUrl = @"rtmp://your-stream-url";
V2TXLiveCode result = [pusher startPush:pushUrl];

if (result == V2TXLIVE_OK) {
    NSLog(@"Streaming started successfully");
} else {
    NSLog(@"Streaming failed to start, error code: %ld", (long)result);
}
```

### Screen Sharing Streaming Example
```objc
V2TXLivePusher *pusher = [[V2TXLivePusher alloc] initWithLiveMode:V2TXLiveModeRTMP];

[pusher setObserver:self];

// At least one capture source must be enabled before streaming
[pusher startScreenCapture:@"group.com.your.app"];

// Enable microphone if audio is needed
[pusher startMicrophone];

NSString *pushUrl = @"rtmp://your-stream-url";
V2TXLiveCode result = [pusher startPush:pushUrl];

if (result == V2TXLIVE_OK) {
    NSLog(@"Screen sharing streaming started successfully");
} else {
    NSLog(@"Screen sharing streaming failed to start, error code: %ld", (long)result);
}
```

### Custom Capture Example
```objc
V2TXLivePusher *pusher = [[V2TXLivePusher alloc] initWithLiveMode:V2TXLiveModeRTMP];

[pusher setObserver:self];

// At least one capture source must be enabled before streaming
[pusher enableCustomVideoCapture:YES];  // Enable before startPush
[pusher enableCustomAudioCapture:YES];  // Optional for audio

NSString *pushUrl = @"rtmp://your-stream-url";
V2TXLiveCode result = [pusher startPush:pushUrl];

if (result == V2TXLIVE_OK) {
    NSLog(@"Custom capture streaming started successfully");
} else {
    NSLog(@"Custom capture streaming failed to start, error code: %ld", (long)result);
}

// Send video frame in custom capture mode
V2TXLiveVideoFrame *videoFrame = [[V2TXLiveVideoFrame alloc] init];
videoFrame.pixelFormat = V2TXLivePixelFormatNV12;
videoFrame.bufferType = V2TXLiveBufferTypePixelBuffer;
videoFrame.width = 1920;
videoFrame.height = 1080;
videoFrame.rotation = V2TXLiveRotation0;

[pusher sendCustomVideoFrame:videoFrame];
```

## 14. Best Practices

### Capture Source Management

**Principle**: Only one capture source can be active per pusher instance

**Switching Sequence**:
```objc
// Switch from camera to image streaming
[pusher startCamera:YES];
// ... streaming with camera ...
[pusher stopCamera];           // Stop current source first
[pusher startVirtualCamera:image];  // Start new source
```

### Performance Optimization

**Audio Processing**:
- Use `pauseAudio` instead of `stopMicrophone` to keep audio stream active
- Set audio quality based on scenario; use `V2TXLiveAudioQualitySpeech` for voice

**Video Encoding**:
- Adjust bitrate dynamically according to network conditions
- Set GOP (Group of Pictures) size to 2–3 seconds for live streaming
- Prefer Hardware Encoding on mobile for better performance

**Resource Management**:
- Release unused capture sources promptly
- Call `stopPush` when streaming ends to free resources
- Set preview fill mode appropriately