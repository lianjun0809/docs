> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/en/llms.txt
> Use this file to discover all available pages before exploring further.

# Tencent Cloud Live Streaming SDK V2TXLivePusher Streaming API Documentation

## Feature Overview

`V2TXLivePusher` is the primary streaming interface in the Tencent Cloud Live Streaming SDK. It handles encoding local audio and video and pushes the stream to a specified URL, supporting any streaming server.

**File Path**: `com/tencent/live2/V2TXLivePusher.java`  
**Platform Support**: Android

## Core Features

### 🎯 Main Capabilities
- ✅ **Capture Sources**: Camera, microphone, screen, image, custom capture
- ✅ **Video Controls**: Rotation, fill mode, mirroring, watermark
- ✅ **Streaming Controls**: Start/stop, pause/resume, audio/video separation
- ✅ **Effects**: Beauty, filters, stickers, audio effects
- ✅ **Cloud Stream Mixing**: Multi-channel audio/video stream mix transcoding
- ✅ **Local Recording**: Record audio/video streams locally
- ✅ **Custom Capture**: Support for external devices and special formats

### 🔧 Technical Highlights
- **Low Latency**: Optimized encoding and adaptive networking
- **High Compatibility**: Supports multiple video encoding formats and resolutions
- **Easy Integration**: Simple APIs and robust callback system
- **High Performance**: Hardware encoding acceleration and efficient capture pipeline

### Creating a Pusher Instance
```java
// Create an RTMP protocol pusher instance; startPush must use an RTMP URL
V2TXLivePusher pusher = new V2TXLivePusherImpl(context, V2TXLiveDef.V2TXLiveMode.TXLiveMode_RTMP);

// Create an RTC protocol pusher instance; startPush must use an RTC URL
V2TXLivePusher pusher = new V2TXLivePusherImpl(context, V2TXLiveDef.V2TXLiveMode.TXLiveMode_RTC);
```

**Protocol Selection Guidelines**:
- **RTMP Protocol**: Best for CDN live streaming; latency is typically 2–3 seconds.
- **RTC Protocol**: Ideal for real-time interactive scenarios; latency is typically under 400ms.

## API Details

### 1. Basic Setup Interfaces

#### setObserver() - Set Pusher Callback
```java
public abstract void setObserver(V2TXLivePusherObserver observer);
```

**Parameters**:
- `observer`: Callback object implementing `V2TXLivePusherObserver`

**When to Use**: Set immediately after initializing the pusher.

**Description**: Register a callback to receive pusher status updates, volume changes, statistics, warnings, and errors.

**Example**:
```java
pusher.setObserver(new V2TXLivePusherObserver(){
  // ...
});
```

#### setRenderView() - Set Local Camera Preview View
```java
public abstract int setRenderView(TXCloudVideoView view);
public abstract int setRenderView(TextureView view);
public abstract int setRenderView(SurfaceView view);
```

**Parameters**:
- `view`: Preview view; supports three types

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**When to Use**: Set the preview view before starting the stream.

**Description**: The camera feed, after applying beauty, face shape adjustment, filters, and other effects, will display on the specified view.

**Example**:
```java
pusher.setRenderView(videoView);
```

#### setRenderMirror() - Set Local Camera Preview Mirroring
```java
public abstract int setRenderMirror(V2TXLiveMirrorType mirrorType);
```

**Parameters**:
- `mirrorType`: Camera mirror type (`V2TXLiveDef#V2TXLiveMirrorType`)
  - `V2TXLiveMirrorTypeAuto` [default]: Front camera mirrored, rear camera not mirrored
  - `V2TXLiveMirrorTypeEnable`: Both front and rear cameras mirrored
  - `V2TXLiveMirrorTypeDisable`: Both front and rear cameras not mirrored

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**When to Use**: No restrictions

**Example**:
```java
// Front camera mirrored, rear camera not mirrored
pusher.setRenderMirror(V2TXLiveDef.V2TXLiveMirrorType.V2TXLiveMirrorTypeAuto);
// All cameras mirrored
pusher.setRenderMirror(V2TXLiveDef.V2TXLiveMirrorType.V2TXLiveMirrorTypeEnable);
// All cameras not mirrored
pusher.setRenderMirror(V2TXLiveDef.V2TXLiveMirrorType.V2TXLiveMirrorTypeDisable);
```

#### setEncoderMirror() - Set Video Encoding Mirroring
```java
public abstract int setEncoderMirror(boolean mirror);
```

**Parameters**:
- `mirror`: Whether to mirror [default: false]

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**Description**: Encoding mirroring only affects the video displayed to the audience.

**When to Use**: No restrictions

**Example**:
```java
// Audience sees mirrored video
pusher.setEncoderMirror(true);
// Audience sees non-mirrored video
pusher.setEncoderMirror(false);
```

#### setRenderRotation() - Set Local Camera Preview Rotation
```java
public abstract int setRenderRotation(V2TXLiveRotation rotation);
```

**Parameters**:
- `rotation`: Preview rotation angle (`V2TXLiveDef#V2TXLiveRotation`)
  - `V2TXLiveRotation0` [default]: 0°, no rotation
  - `V2TXLiveRotation90`: 90° clockwise
  - `V2TXLiveRotation180`: 180° clockwise
  - `V2TXLiveRotation270`: 270° clockwise

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**Description**: Rotates only the local preview; does not affect the streamed video.

**When to Use**: No restrictions

**Example**:
```java
// Set preview rotation to 0°
pusher.setRenderRotation(V2TXLiveDef.V2TXLiveRotation.V2TXLiveRotation0);
// Set preview rotation to 90°
pusher.setRenderRotation(V2TXLiveDef.V2TXLiveRotation.V2TXLiveRotation90);
// Set preview rotation to 180°
pusher.setRenderRotation(V2TXLiveDef.V2TXLiveRotation.V2TXLiveRotation180);
// Set preview rotation to 270°
pusher.setRenderRotation(V2TXLiveDef.V2TXLiveRotation.V2TXLiveRotation270);
```

#### setRenderFillMode() - Set Local Camera Preview Fill Mode
```java
public abstract int setRenderFillMode(V2TXLiveFillMode mode);
```

**Parameters**:
- `mode`: Fill mode (`V2TXLiveDef#V2TXLiveFillMode`)
  - `V2TXLiveFillModeFill` [default]: Image fills the screen, no black borders, some cropping
  - `V2TXLiveFillModeFit`: Image fits the screen, no cropping, may have black borders
  - `V2TXLiveFillModeScaleFill`: Image stretched to fill; aspect ratio may not be preserved

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**When to Use**: No restrictions

**Example**:
```java
// Image fills the screen
pusher.setRenderFillMode(V2TXLiveDef.V2TXLiveFillMode.V2TXLiveFillModeFill);
// Image fits the screen
pusher.setRenderFillMode(V2TXLiveDef.V2TXLiveFillMode.V2TXLiveFillModeFit);
// Image stretched to fill
pusher.setRenderFillMode(V2TXLiveDef.V2TXLiveFillMode.V2TXLiveFillModeScaleFill);
```

### 2. Capture Control Interfaces

#### startCamera() / stopCamera() - Enable/Disable Camera Capture
```java
public abstract int startCamera(boolean frontCamera);
public abstract int stopCamera();
```

**Parameters**:
- `frontCamera`: true for front camera [default: true]

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**Important**:  
- **Enable at least one capture source before streaming**; otherwise, streaming will fail.
- Only one capture source can be active per pusher instance: `startVirtualCamera`, `startCamera`, or `startScreenCapture`.
- To switch sources, stop the current source before starting another.

**When to Use**: Call before starting the stream.

**Example**:
```java
// Enable front camera
pusher.startCamera(true);
// Enable rear camera
pusher.startCamera(false);
// Stop camera capture
pusher.stopCamera();
```

#### startMicrophone() / stopMicrophone() - Enable/Disable Microphone Capture
```java
public abstract int startMicrophone();
public abstract int stopMicrophone();
```

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**Use Cases**:
- **Audio/Video Streaming**: Capture audio with camera
- **Audio-only Streaming**: Use microphone alone
- **Screen Sharing**: Combine with screen capture for system and microphone audio

**Notes**:
- **Enable microphone capture before streaming**; otherwise, only video will be streamed.
- For audio-only streaming, use microphone capture alone.
- Microphone capture can be toggled during streaming.

**When to Use**: Call before starting the stream.

**Example**:
```java
// Enable microphone capture
pusher.startMicrophone();
// Stop microphone capture
pusher.stopMicrophone();
```

#### startVirtualCamera() / stopVirtualCamera() - Enable/Disable Image Streaming
```java
public abstract int startVirtualCamera(Bitmap image);
public abstract int stopVirtualCamera();
```

**Parameters**:
- `image`: Image to stream

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**Use Cases**:
- **Image Streaming**: Use a static image as the video source
- **Maintenance Page**: Display maintenance info during downtime
- **Ad Display**: Show advertisement images

**Notes**:
- **Enable image streaming before streaming**; otherwise, streaming will fail.
- The image is encoded as video, consuming bandwidth.
- Typically used with microphone capture for audio.
- Image streaming and camera capture cannot be enabled simultaneously.

**When to Use**: Call before starting the stream.

**Example**:
```java
// Enable image streaming
Bitmap image = BitmapFactory.decodeResource(getResources(), R.drawable.live_image);
pusher.startVirtualCamera(image);
// Stop image streaming
pusher.stopVirtualCamera();
```

#### startScreenCapture() / stopScreenCapture() - Enable/Disable Screen Capture
```java
public abstract int startScreenCapture();
public abstract int stopScreenCapture();
```

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**Use Cases**:
- **Screen Sharing**: Share device screen for live streaming
- **Remote Teaching**: Share screens for online classes
- **Game Streaming**: Stream gameplay
- **App Demo**: Demonstrate app workflows

**Notes**:
- **Enable screen capture before streaming**; otherwise, streaming will fail.
- Android requires screen recording permissions.
- Can be combined with `startSystemAudioLoopback()` to capture system audio.
- Screen capture and camera capture cannot be enabled simultaneously.

**When to Use**: Call before starting the stream.

**Example**:
```java
// Enable screen capture
pusher.startScreenCapture();
// Stop screen capture
pusher.stopScreenCapture();
```

### 3. Streaming Control Interfaces

#### startPush() - Start Streaming
```java
public abstract int startPush(String url);
```

**Parameters**:
- `url`: Target streaming address; supports any streaming server

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Operation successful, connecting to target
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: Invalid URL
- `V2TXLIVE_ERROR_INVALID_LICENSE`: Invalid license, authentication failed
- `V2TXLIVE_ERROR_REFUSED`: RTC does not support simultaneous push/pull of the same StreamId on one device

**Important**:
- **Enable at least one capture source before calling startPush()**; otherwise, streaming will fail.
- Supported sources: camera, microphone, screen, image streaming, custom capture.
- You can switch sources during streaming, but must stop the current source before starting another.

**When to Use**: After enabling a capture source.

**Example**:
```java
int result = pusher.startPush("rtmp://example.com/live/stream");
if (result == V2TXLiveCode.V2TXLIVE_OK) {
    Log.i(TAG, "Streaming started successfully");
} else if (result == V2TXLiveCode.V2TXLIVE_ERROR_INVALID_PARAMETER) {
    Log.w(TAG, "Invalid streaming URL");
} else if (result == V2TXLiveCode.V2TXLIVE_ERROR_INVALID_LICENSE) {
    Log.w(TAG, "Invalid license, please check your license");
} else if (result == V2TXLiveCode.V2TXLIVE_ERROR_REFUSED) {
    Log.w(TAG, "Operation refused");
}
```

#### stopPush() - Stop Streaming
```java
public abstract int stopPush();
```

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**When to Use**: After streaming has started.

**Example**:
```java
pusher.stopPush();
```

#### isPushing() - Check Streaming Status
```java
public abstract int isPushing();
```

**Return Value**:
- `1`: Currently streaming
- `0`: Streaming stopped

**When to Use**: No restrictions

**Example**:
```java
int isPushing = pusher.isPushing();
if (isPushing == 1) {
    Log.i(TAG, "Streaming in progress");
} else {
    Log.i(TAG, "Streaming stopped");
}
```

### 4. Audio/Video Control Interfaces

#### pauseAudio() / resumeAudio() - Pause/Resume Audio
```java
public abstract int pauseAudio();
public abstract int resumeAudio();
```

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**When to Use**: No restrictions

**Example**:
```java
// Pause audio
pusher.pauseAudio();
// Resume audio
pusher.resumeAudio();
```

#### pauseVideo() / resumeVideo() - Pause/Resume Video
```java
public abstract int pauseVideo();
public abstract int resumeVideo();
```

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**When to Use**: No restrictions

**Example**:
```java
// Pause video
pusher.pauseVideo();
// Resume video
pusher.resumeVideo();
```

#### setAudioQuality() - Set Audio Quality
```java
public abstract int setAudioQuality(V2TXLiveAudioQuality quality);
```

**Parameters**:
- `quality`: Audio quality (`V2TXLiveDef#V2TXLiveAudioQuality`)
  - `V2TXLiveAudioQualityDefault` [default]: General quality
  - `V2TXLiveAudioQualitySpeech`: Speech quality
  - `V2TXLiveAudioQualityMusic`: Music quality

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success
- `V2TXLIVE_ERROR_REFUSED`: Cannot change audio quality during streaming

**When to Use**: Before streaming starts

**Example**:
```java
// Set general audio quality
pusher.setAudioQuality(V2TXLiveDef.V2TXLiveAudioQuality.V2TXLiveAudioQualityDefault);
// Set speech quality
pusher.setAudioQuality(V2TXLiveDef.V2TXLiveAudioQuality.V2TXLiveAudioQualitySpeech);
// Set music quality
pusher.setAudioQuality(V2TXLiveDef.V2TXLiveAudioQuality.V2TXLiveAudioQualityMusic);
```

#### setVideoQuality() - Set Video Encoding Parameters
```java
public abstract int setVideoQuality(V2TXLiveVideoEncoderParam param);
```

**Parameters**:
- `param`: Video encoding parameters

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**When to Use**: Before streaming starts

**Example**:
```java
V2TXLiveVideoEncoderParam param = new V2TXLiveVideoEncoderParam();
param.videoResolution = V2TXLiveVideoResolution.V2TXLiveVideoResolution1280x720;
param.videoFps = 15;
param.videoBitrate = 1200;
pusher.setVideoQuality(param);
```

### 5. Effects Management Interfaces

#### getAudioEffectManager() - Get Audio Effect Manager
```java
public abstract TXAudioEffectManager getAudioEffectManager();
```

**Description**:
- Adjust microphone volume
- Set reverb and voice effects
- Enable ear monitoring and adjust ear monitor volume
- Add background music and control playback

**Return Value**: `TXAudioEffectManager` object

**When to Use**: No restrictions

**Example**:
```java
TXAudioEffectManager audioEffectManager = pusher.getAudioEffectManager();
// Set voice volume
audioEffectManager.setVoiceVolume(100);
// Set background music volume
audioEffectManager.setAllMusicVolume(50);
```

#### getBeautyManager() - Get Beauty Manager
```java
public abstract TXBeautyManager getBeautyManager();
```

**Description**:
- Set beauty style, whitening, ruddy, big eyes, face slimming, and other beauty effects
- Adjust hairline, eye spacing, eye corners, mouth shape, and other facial features
- Add facial accessories and dynamic effects
- Apply makeup effects
- Perform gesture recognition

**Return Value**: `TXBeautyManager` object

**When to Use**: No restrictions

**Example**:
```java
TXBeautyManager beautyManager = pusher.getBeautyManager();
// Set beauty style
beautyManager.setBeautyStyle(TXBeautyManager.TXBeautyStyleNature);
// Set whitening level
beautyManager.setWhitenessLevel(5);
// Set ruddy level
beautyManager.setRuddyLevel(5);
```

#### getDeviceManager() - Get Device Manager
```java
public abstract TXDeviceManager getDeviceManager();
```

**Description**:
- Switch between front and rear cameras
- Enable auto focus
- Set camera zoom
- Toggle flashlight
- Switch between headset and speaker
- Change volume type (media or call)

**Return Value**: `TXDeviceManager` object

**When to Use**: No restrictions

**Example**:
```java
TXDeviceManager deviceManager = pusher.getDeviceManager();
// Switch camera
deviceManager.switchCamera(true);
// Enable auto focus
deviceManager.setAutoFocusEnabled(true);
// Enable flashlight
deviceManager.enableTorch(true);
```

### 6. Advanced Feature Interfaces

#### snapshot() - Capture Local Frame
```java
public abstract int snapshot();
```

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success
- `V2TXLIVE_ERROR_REFUSED`: Streaming stopped; cannot snapshot

**When to Use**: After streaming has started

**Example**:
```java
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onSnapshotComplete(Bitmap image) {
        // Handle snapshot result
    }
});
pusher.snapshot();
```

#### setWatermark() - Set Watermark
```java
public abstract int setWatermark(Bitmap image, float x, float y, float scale);
```

**Parameters**:
- `image`: Watermark image; null disables watermark
- `x`: Horizontal position (0–1)
- `y`: Vertical position (0–1)
- `scale`: Scale (0–1)

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**When to Use**: No restrictions

**Example**:
```java
Bitmap watermark = BitmapFactory.decodeResource(getResources(), R.drawable.watermark);
pusher.setWatermark(watermark, 0.1f, 0.1f, 0.2f);
// Disable watermark
pusher.setWatermark(null, 0, 0, 0);
```

#### enableVolumeEvaluation() - Enable Capture Volume Evaluation
```java
public abstract int enableVolumeEvaluation(int intervalMs);
```

**Parameters**:
- `intervalMs`: Callback interval in ms; minimum 100ms. Set <=0 to disable [default: 0]

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**Description**: When enabled, the SDK reports volume via the `onMicrophoneVolumeUpdate` callback.

**When to Use**: No restrictions

**Example**:
```java
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onMicrophoneVolumeUpdate(int volume) {
        // Handle volume update
    }
});
pusher.enableVolumeEvaluation(300);
```

#### enableCustomVideoProcess() - Enable/Disable Custom Video Processing
```java
public abstract int enableCustomVideoProcess(boolean enable, V2TXLivePixelFormat pixelFormat, V2TXLiveBufferType bufferType);
```

**Parameters**:
- `enable`: true to enable, false to disable [default: false]
- `pixelFormat`: Pixel format (`V2TXLiveDef#V2TXLivePixelFormat`)
- `bufferType`: Buffer type (`V2TXLiveDef#V2TXLiveBufferType`)

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success
- `V2TXLIVE_ERROR_NOT_SUPPORTED`: Unsupported format

**Supported Format Combinations**:
- `V2TXLivePixelFormatTexture2D + V2TXLiveBufferTypeTexture`
- `V2TXLivePixelFormatI420 + V2TXLiveBufferTypeByteBuffer`

**When to Use**: Before streaming starts

**Example**:
```java
pusher.enableCustomVideoProcess(true, 
    V2TXLiveDef.V2TXLivePixelFormat.V2TXLivePixelFormatTexture2D,
    V2TXLiveDef.V2TXLiveBufferType.V2TXLiveBufferTypeTexture);
```

#### enableCustomVideoCapture() - Enable/Disable Custom Video Capture
```java
public abstract int enableCustomVideoCapture(boolean enable);
```

**Parameters**:
- `enable`: true to enable, false to disable [default: false]

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**Use Cases**:
- **External Device Capture**: Use external cameras, capture cards, etc.
- **Video Processing**: Pre-process video before streaming
- **Multi-source Composition**: Combine multiple video sources
- **Special Formats**: Stream special video formats

**Notes**:
- **Enable custom capture before streaming**; otherwise, streaming will fail.
- Must be called before `startPush` to take effect.
- In custom capture mode, the SDK only encodes and sends; it does not capture.

**When to Use**: Before streaming starts

**Example**:
```java
// Enable custom video capture
pusher.enableCustomVideoCapture(true);
pusher.startPush(url);

// Send custom video frame
V2TXLiveVideoFrame videoFrame = new V2TXLiveVideoFrame();
videoFrame.width = 1920;
videoFrame.height = 1080;
videoFrame.pixelFormat = V2TXLivePixelFormat.V2TXLivePixelFormatI420;
videoFrame.bufferType = V2TXLiveBufferType.V2TXLiveBufferTypeByteBuffer;
pusher.sendCustomVideoFrame(videoFrame);
```

#### enableCustomAudioCapture() - Enable/Disable Custom Audio Capture
```java
public abstract int enableCustomAudioCapture(boolean enable);
```

**Parameters**:
- `enable`: true to enable, false to disable [default: false]

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**Use Cases**:
- **External Audio Devices**: Use external microphones, audio interfaces, etc.
- **Audio Processing**: Pre-process audio before streaming
- **Multi-channel Audio**: Combine multiple audio sources

**Notes**:
- **Enable custom capture before streaming**; otherwise, streaming will fail.
- Must be called before `startPush` to take effect.
- In custom capture mode, the SDK only encodes and sends; it does not capture.

**When to Use**: Before streaming starts

**Example**:
```java
// Enable custom audio capture
pusher.enableCustomAudioCapture(true);
pusher.startPush(url);

// Send custom audio frame
V2TXLiveAudioFrame audioFrame = new V2TXLiveAudioFrame();
audioFrame.data = audioData; // PCM audio data
audioFrame.sampleRate = 44100; // Sample rate
audioFrame.channel = 1; // Audio channel count
pusher.sendCustomAudioFrame(audioFrame);
```

#### sendSeiMessage() - Send SEI Message
```java
public abstract int sendSeiMessage(int payloadType, byte[] data);
```

**Parameters**:
- `payloadType`: Data type; supports 5 and 242 (recommend 242)
- `data`: Data to send

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**Description**: The player receives this message via the `onReceiveSeiMessage` callback.

**When to Use**: During streaming

**Example**:
```java
byte[] seiData = "Hello SEI".getBytes();
pusher.sendSeiMessage(242, seiData);
```

#### startSystemAudioLoopback() / stopSystemAudioLoopback() - Enable/Disable System Audio Capture
```java
public abstract int startSystemAudioLoopback();
public abstract int stopSystemAudioLoopback();
```

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**Description**:
- Captures all system audio playback and mixes with microphone audio for cloud streaming
- Only available on Android API 29+
- Must enable before starting screen sharing
- Requires a foreground service to avoid silent capture

**When to Use**: Before streaming starts

**Example**:
```java
// Enable system audio capture
pusher.startSystemAudioLoopback();
// Disable system audio capture
pusher.stopSystemAudioLoopback();
```

#### setMixTranscodingConfig() - Set Cloud Stream Mixing Parameters
```java
public abstract int setMixTranscodingConfig(V2TXLiveTranscodingConfig config);
```

**Parameters**:
- `config`: MixTranscoding configuration; pass null to cancel cloud stream mixing

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success
- `V2TXLIVE_ERROR_REFUSED`: Not allowed if streaming hasn't started

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

**Notes**:
- **RTC Protocol Only**: This API is only supported for RTC protocol; not available for RTMP or other protocols.
- Cloud transcoding adds 1–2 seconds of CDN viewing latency.
- Cancel mixing configuration promptly to avoid unnecessary charges.

**When to Use**: During streaming

**Example**:
```java
V2TXLiveTranscodingConfig config = new V2TXLiveTranscodingConfig();
config.videoWidth = 1280;
config.videoHeight = 720;
config.videoBitrate = 1500;
config.videoFps = 15;
pusher.setMixTranscodingConfig(config);

// Cancel mixing
pusher.setMixTranscodingConfig(null);
```

#### startLocalRecording() / stopLocalRecording() - Start/Stop Local Recording
```java
public abstract int startLocalRecording(V2TXLiveLocalRecordingParams params);
public abstract void stopLocalRecording();
```

**Parameters**:
- `params`: Local recording parameters

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: Invalid parameters
- `V2TXLIVE_ERROR_REFUSED`: API refused; streaming not started

**Description**: Recording can only start after streaming is enabled; recording is invalid when not streaming.

**When to Use**: During streaming

**Example**:
```java
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onLocalRecordBegin(int code, String storagePath) {
        Log.i(TAG, "Recording started");
    }

    @Override
    public void onLocalRecording(long durationMs, String storagePath) {
        Log.i(TAG, "Recording..., durationMs: " + durationMs);
    }

    @Override
    public void onLocalRecordComplete(int code, String storagePath) {
        Log.i(TAG, "Recording completed");
    }
});

V2TXLiveLocalRecordingParams params = new V2TXLiveLocalRecordingParams();
params.filePath = "filepath";
params.interval = 2000;
int code = pusher.startLocalRecording(params);
if (code == V2TXLIVE_OK) {
    Log.i(TAG, "Recording started successfully");
} else if (code == V2TXLIVE_ERROR_INVALID_PARAMETER) {
    Log.i(TAG, "Invalid recording parameters");
} else if (code == V2TXLIVE_ERROR_REFUSED) {
    Log.i(TAG, "Recording call refused");
}
```

#### showDebugView() - Show Debug Dashboard
```java
public abstract void showDebugView(boolean isShow);
```

**Parameters**:
- `isShow`: true to show, false to hide [default: false]

**When to Use**: No restrictions

**Example**:
```java
// Show debug view
pusher.showDebugView(true);
// Hide debug view
pusher.showDebugView(false);
```

#### setProperty() - Call Advanced V2TXLivePusher API
```java
public abstract int setProperty(String key, Object value);
```

**Parameters**:
- `key`: Advanced API key; see `V2TXLiveProperty` for details
- `value`: Parameter for the corresponding advanced API

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: Key cannot be empty

**Description**: For advanced features. For special requirements, contact your business or solution architect.

**When to Use**: No restrictions

**Example**:
```java
pusher.setProperty("key", "value");
```

## Code Examples

### Basic Streaming (Camera + Microphone)
```java
// Create pusher instance
V2TXLivePusher pusher = new V2TXLivePusherImpl(context);

// Set callback
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onPushStatusUpdate(V2TXLiveDef.V2TXLivePushStatus status, String msg, Bundle extraInfo) {
        // Handle streaming status changes
    }
});

// Set preview view
pusher.setRenderView(textureView);

// Important: Enable at least one capture source before streaming
// 1. Enable camera capture (front camera)
pusher.startCamera(true);

// 2. Enable microphone capture
pusher.startMicrophone();

// 3. Start streaming (after enabling a capture source)
pusher.startPush("rtmp://your-stream-url");
```

### Screen Sharing Streaming
```java
// Create pusher instance
V2TXLivePusher pusher = new V2TXLivePusherImpl(context);

// Set callback
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onPushStatusUpdate(V2TXLiveDef.V2TXLivePushStatus status, String msg, Bundle extraInfo) {
        // Handle streaming status changes
    }
});

// Important: Enable at least one capture source before streaming
// 1. Enable screen capture
pusher.startScreenCapture();

// 2. Enable microphone capture (optional, if audio is needed)
pusher.startMicrophone();

// 3. Start streaming
pusher.startPush("rtmp://your-stream-url");
```

### Custom Capture
```java
// Create pusher instance
V2TXLivePusher pusher = new V2TXLivePusherImpl(context);

// Set callback
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onPushStatusUpdate(V2TXLiveDef.V2TXLivePushStatus status, String msg, Bundle extraInfo) {
        // Handle streaming status changes
    }
});

// Important: Enable at least one capture source before streaming
// 1. Enable custom video capture (call before startPush)
pusher.enableCustomVideoCapture(true);

// 2. Enable custom audio capture (optional, if audio is needed)
pusher.enableCustomAudioCapture(true);

// 3. Start streaming
pusher.startPush("rtmp://your-stream-url");

// 4. Send video frames in custom capture mode
V2TXLiveVideoFrame videoFrame = new V2TXLiveVideoFrame();
videoFrame.width = 1920;
videoFrame.height = 1080;
videoFrame.pixelFormat = V2TXLivePixelFormat.V2TXLivePixelFormatI420;
videoFrame.bufferType = V2TXLiveBufferType.V2TXLiveBufferTypeByteBuffer;
pusher.sendCustomVideoFrame(videoFrame);
```

## Notes

### 1. Capture Source Requirements
**Enable at least one capture source before streaming**, or streaming will fail:
- **Camera Capture**: `startCamera()` + `startMicrophone()`
- **Screen Capture**: `startScreenCapture()` + `startMicrophone()`
- **Image Streaming**: `startVirtualCamera()` + `startMicrophone()`
- **Custom Capture**: `enableCustomVideoCapture()` + `enableCustomAudioCapture()`
- **Audio-only Streaming**: `startMicrophone()`

### 2. Capture Source Switching
- Only one capture source can be active per pusher instance.
- To switch sources, always stop the current source before starting another.

### 3. Required Call Sequence
1. Create pusher instance
2. Set callback and preview view
3. Enable at least one capture source
4. Call `startPush()` to begin streaming

### 4. Custom Capture
- Call custom capture APIs before `startPush` to take effect.
- In custom capture mode, the SDK only encodes and sends; it does not capture.

### 5. Cloud Stream Mixing
- **Protocol Limitation**: Cloud stream mixing is only supported for RTC protocol, not RTMP or other protocols.
- Cancel mixing configuration promptly to avoid unnecessary charges.
- Cloud transcoding adds 1–2 seconds of CDN viewing latency.

### 6. Local Recording
- Recording can only start after streaming is enabled.
- Do not change resolution or switch hardware/software encoding during recording.

### 7. System Audio Capture
- Requires Android API 29 or above.
- Requires a foreground service to avoid silent capture.
- Only works during screen sharing.

### 8. Performance Optimization
- Select appropriate audio/video quality settings for your scenario.
- Release unused pusher instances promptly.
- Use pause/resume functions to save bandwidth.