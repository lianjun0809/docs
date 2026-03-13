> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

# Tencent Cloud Live Streaming SDK V2TXLivePusher Streaming Interface Documentation

## Feature Overview

`V2TXLivePusher` is the primary streaming interface in the Tencent Cloud TRTC Live Streaming SDK. It handles encoding of local audio and video and pushes the stream to a specified streaming URL, compatible with any streaming server.

### 🎯 Core Features
- ✅ **Multiple Capture Sources**: Camera, microphone, screen, image, custom capture
- ✅ **Video Controls**: Rotation, fill mode, mirroring, watermark
- ✅ **Streaming Controls**: Start/stop, pause/resume, separate audio/video
- ✅ **Effects Processing**: Beauty, filters, stickers, audio effects
- ✅ **Cloud Stream Mixing**: Multi-channel audio/video stream mix transcoding
- ✅ **Local Recording**: Record local audio/video streams
- ✅ **Custom Capture**: Support for external devices and custom formats

### 🔧 Technical Highlights
- **Low Latency**: Optimized encoding and adaptive network strategies
- **High Compatibility**: Supports various video encoding formats and resolutions
- **Easy Integration**: Simple API design with robust callback support
- **High Performance**: Accelerated hardware encoding and efficient capture pipeline

### Creating a Pusher Instance
```dart
// Create a streaming instance using the RTC protocol. startPush requires an RTC protocol URL.
V2TXLivePusher pusher = await V2TXLivePusher.create(V2TXLiveMode.V2TXLiveModeRTC);
```

**Protocol Selection Guidelines**:
- **RTMP Protocol**: Best for CDN live distribution; latency is typically 2–3 seconds.
- **RTC Protocol**: Ideal for real-time interactive scenarios; latency is typically under 400ms.

## File Information

- **File Path**: `v2_tx_live_pusher.dart`
- **Dependencies**:
  - `v2_tx_live_code.dart` – Error code definitions
  - `v2_tx_live_def.dart` – Type definitions
  - `v2_tx_live_pusher_observer.dart` – Observer callback interface
  - `tx_audio_effect_manager.dart` – Audio effect management
  - `tx_device_manager.dart` – Device management

## Class Definition

```dart
abstract class V2TXLivePusher {
  V2TXLivePusher() {}
}
```

## Static Methods

### create
**Purpose**: Create a pusher instance
```dart
static Future<V2TXLivePusher> create(V2TXLiveMode liveMode) async
```

**Parameters**:
- `liveMode`: Streaming mode [V2TXLiveMode]

**Returns**:
- `Future<V2TXLivePusher>`: The created pusher instance

**Usage Example**:
```dart
V2TXLivePusher pusher = await V2TXLivePusher.create(V2TXLiveMode.V2TXLiveModeRTC);
```

## Observer Management

### addListener
**Purpose**: Register a pusher callback observer
```dart
void addListener(V2TXLivePusherObserver observer)
```

**Parameters**:
- `observer`: Observer object implementing the `V2TXLivePusherObserver` protocol

**When to Call**: Immediately after initializing the pusher

**Description**: Use callbacks to monitor pusher status, volume changes, statistics, warnings, and errors.

**Example**:
```dart
pusher.addListener(V2TXLivePusherObserver(
  onPushStatusUpdate: (status, msg, extraInfo) {
    // Handle streaming status changes
  },
  onStatisticsUpdate: (statistics) {
    // Handle statistics
  },
  onError: (code, msg, extraInfo) {
    // Handle error information
  }
));
```

### removeListener
**Purpose**: Unregister a pusher callback observer
```dart
void removeListener(V2TXLivePusherObserver observer)
```

**Parameters**:
- `observer`: Observer object [V2TXLivePusherObserver]

### destroy
**Purpose**: Destroy the pusher instance and release resources
```dart
void destroy()
```

## Video Rendering Controls

### setRenderViewID
**Purpose**: Set the view ID for local camera preview
```dart
Future<V2TXLiveCode> setRenderViewID(int viewID)
```

**Parameters**:
- `viewID`: ID of the view for local camera preview

**Returns**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**When to Call**: Set the preview view before starting the stream

**Description**: The video captured by the local camera, after applying beauty, face shape adjustment, filters, and other effects, is displayed in the specified view.

**Example**:
```dart
await pusher.setRenderViewID(yourTextureViewID);
```

### setRenderMirror
**Purpose**: Set camera mirroring mode for preview
```dart
Future<V2TXLiveCode> setRenderMirror(V2TXLiveMirrorType mirrorType)
```

**Parameters**:
- `mirrorType`: Mirroring mode [V2TXLiveMirrorType]
  - `V2TXLiveMirrorType.v2TXLiveMirrorTypeAuto`: Default; front camera mirrored, rear camera not mirrored
  - `V2TXLiveMirrorType.v2TXLiveMirrorTypeEnable`: Both front and rear cameras mirrored
  - `V2TXLiveMirrorType.v2TXLiveMirrorTypeDisable`: Neither camera mirrored

### setEncoderMirror
**Purpose**: Set video encoding mirroring (affects only what the audience sees)
```dart
Future<V2TXLiveCode> setEncoderMirror(bool mirror)
```

**Parameters**:
- `mirror`: Whether to mirror the encoded video
  - `false`: Default; audience sees non-mirrored video
  - `true`: Audience sees mirrored video

### setRenderRotation
**Purpose**: Set rotation angle for local camera preview (local preview only)
```dart
Future<V2TXLiveCode> setRenderRotation(V2TXLiveRotation rotation)
```

**Parameters**:
- `rotation`: Rotation angle [V2TXLiveRotation]
  - `V2TXLiveRotation.v2TXLiveRotation0`: 0°, no rotation (default)
  - `V2TXLiveRotation.v2TXLiveRotation90`: 90° clockwise
  - `V2TXLiveRotation.v2TXLiveRotation180`: 180° clockwise
  - `V2TXLiveRotation.v2TXLiveRotation270`: 270° clockwise

### setRenderFillMode
**Purpose**: Set video fill mode for preview
```dart
Future<V2TXLiveCode> setRenderFillMode(V2TXLiveFillMode mode)
```

**Parameters**:
- `mode`: Video fill mode [V2TXLiveFillMode]
  - `V2TXLiveFillMode.v2TXLiveFillModeFill`: Default; fills the screen, no black borders
  - `V2TXLiveFillMode.v2TXLiveFillModeFit`: Fits the screen, preserves full image

## Capture Controls

### startCamera
**Purpose**: Start the local camera
```dart
Future<V2TXLiveCode> startCamera(bool frontCamera)
```

**Parameters**:
- `frontCamera`: Whether to use the front camera (default: true)

**Returns**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**Key Points**:
- **You must start at least one capture source before streaming; otherwise, streaming will fail.**
- Only one capture source (camera, virtual camera, or screen capture) can be active per pusher instance.
- To switch sources, stop the current source before starting a new one.

**When to Call**: Before starting the stream

**Example**:
```dart
// Start front camera
await pusher.startCamera(true);
// Start rear camera
await pusher.startCamera(false);
```

### stopCamera
**Purpose**: Stop the local camera
```dart
Future<void> stopCamera()
```

### startMicrophone
**Purpose**: Start microphone capture
```dart
Future<V2TXLiveCode> startMicrophone()
```

**Returns**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**Use Cases**:
- **Audio/video streaming**: Use with camera capture for audio
- **Audio-only streaming**: Use microphone alone
- **Screen sharing**: Use with screen capture for system and microphone audio

**Notes**:
- **Call this method before streaming to capture audio; otherwise, only video will be streamed.**
- For audio-only streaming, use microphone capture alone.
- Microphone capture can be enabled or disabled dynamically during streaming.

**When to Call**: Before starting the stream

**Example**:
```dart
// Start microphone capture
await pusher.startMicrophone();
// Stop microphone capture
await pusher.stopMicrophone();
```

### stopMicrophone
**Purpose**: Stop microphone capture
```dart
Future<V2TXLiveCode> stopMicrophone()
```

### startScreenCapture
**Purpose**: Start screen sharing
```dart
Future<V2TXLiveCode> startScreenCapture(String appGroup)
```

**Parameters**:
- `appGroup`: iOS only; ignored on Android. The Application Group Identifier shared between the main app and broadcast process.

**Note**: Screen capture and camera capture are mutually exclusive.

### stopScreenCapture
**Purpose**: Stop screen sharing
```dart
Future<V2TXLiveCode> stopScreenCapture()
```

## Streaming Controls

### startPush
**Purpose**: Start audio/video streaming
```dart
Future<V2TXLiveCode> startPush(String url)
```

**Parameters**:
- `url`: Streaming URL; supports any streaming server

**Returns**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success; connecting to streaming target
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: Failed; invalid URL
- `V2TXLIVE_ERROR_INVALID_LICENSE`: Failed; invalid license or authentication
- `V2TXLIVE_ERROR_REFUSED`: Failed; RTC does not support pushing and pulling the same StreamId on the same device

**Key Points**:
- **Start at least one capture source before calling startPush(); otherwise, streaming will fail.**
- Supported sources: camera, microphone, screen, image, custom capture
- You can switch capture sources during streaming, but must stop the current source before starting a new one.

**When to Call**: After starting a capture source

**Example**:
```dart
V2TXLiveCode result = await pusher.startPush("rtmp://example.com/live/stream");
if (result == V2TXLiveCode.V2TXLIVE_OK) {
    print('Streaming started successfully');
} else if (result == V2TXLiveCode.V2TXLIVE_ERROR_INVALID_PARAMETER) {
    print('Invalid streaming address');
} else if (result == V2TXLiveCode.V2TXLIVE_ERROR_INVALID_LICENSE) {
    print('Invalid Licence, please check your Licence');
} else if (result == V2TXLiveCode.V2TXLIVE_ERROR_REFUSED) {
    print('Call refused');
}
```

### stopPush
**Purpose**: Stop streaming
```dart
Future<V2TXLiveCode> stopPush()
```

### isPushing
**Purpose**: Check if streaming is active
```dart
Future<V2TXLiveCode> isPushing()
```

**Returns**:
- `1`: Streaming is active
- `0`: Streaming is stopped

## Audio/Video Controls

### pauseAudio
**Purpose**: Pause audio stream
```dart
Future<V2TXLiveCode> pauseAudio()
```

### resumeAudio
**Purpose**: Resume audio stream
```dart
Future<V2TXLiveCode> resumeAudio()
```

### pauseVideo
**Purpose**: Pause video stream
```dart
Future<V2TXLiveCode> pauseVideo()
```

### resumeVideo
**Purpose**: Resume video stream
```dart
Future<V2TXLiveCode> resumeVideo()
```

## Audio/Video Quality Settings

### setAudioQuality
**Purpose**: Set audio quality for streaming
```dart
Future<V2TXLiveCode> setAudioQuality(V2TXLiveAudioQuality quality)
```

**Parameters**:
- `quality`: Audio quality [V2TXLiveAudioQuality]
  - `V2TXLiveAudioQuality.v2TXLiveAudioQualityDefault`: Default, general
  - `V2TXLiveAudioQuality.v2TXLiveAudioQualitySpeech`: Speech
  - `V2TXLiveAudioQuality.v2TXLiveAudioQualityMusic`: Music

**Returns**:
- `V2TXLIVE_OK`: Success
- `V2TXLIVE_ERROR_REFUSED`: Cannot change audio quality during streaming

### setVideoQuality
**Purpose**: Set video encoding parameters for streaming
```dart
Future<V2TXLiveCode> setVideoQuality(V2TXLiveVideoEncoderParam param)
```

**Parameters**:
- `param`: Video encoding parameters [V2TXLiveVideoEncoderParam]

## Audio Effects and Device Management

### getAudioEffectManager
**Purpose**: Access the audio effect manager
```dart
TXAudioEffectManager getAudioEffectManager()
```

**Features**:
- **Background Music**: Supports online/local playback, speed/pitch adjustment, original/accompaniment, looping, etc.
- **Monitor (Earback)**: Real-time playback of microphone audio in headphones; commonly used for music streaming
- **Reverb Effects**: KTV, small room, auditorium, deep, bright, etc.
- **Voice Changer Effects**: Child, uncle, heavy metal, etc.
- **Short Sound Effects**: Supports short audio files (e.g., applause, laughter). For files under 10 seconds, set `isShortFile` to `true`.

### getDeviceManager
**Purpose**: Access the device manager
```dart
TXDeviceManager getDeviceManager()
```

## Advanced Features

### snapshot
**Purpose**: Capture a snapshot of local video during streaming
```dart
Future<V2TXLiveCode> snapshot()
```

**Returns**:
- `V2TXLIVE_OK`: Success
- `V2TXLIVE_ERROR_REFUSED`: Streaming stopped; cannot capture snapshot

### enableVolumeEvaluation
**Purpose**: Enable capture volume indication
```dart
Future<V2TXLiveCode> enableVolumeEvaluation(int intervalMs)
```

**Parameters**:
- `intervalMs`: Volume callback interval (ms); minimum 100ms. Set ≤0 to disable. Recommended: 300ms.

### enableCustomVideoProcess
**Purpose**: Enable or disable custom video processing
```dart
Future<V2TXLiveCode> enableCustomVideoProcess(bool enable, V2TXLivePixelFormat pixelFormat, V2TXLiveBufferType bufferType)
```

**Parameters**:
- `enable`: Enable (true) or disable (false); default is false
- `pixelFormat`: Pixel format for custom pre-processing callback [V2TXLivePixelFormat]
- `bufferType`: Data format for custom pre-processing callback [V2TXLiveBufferType]

**Supported Combinations**:
- `V2TXLivePixelFormatTexture2D` + `V2TXLiveBufferTypeTexture`
- `V2TXLivePixelFormatI420` + `V2TXLiveBufferTypeByteBuffer`

### enableCustomVideoCapture
**Purpose**: Enable or disable custom video capture
```dart
Future<V2TXLiveCode> enableCustomVideoCapture(bool enable)
```

**Parameters**:
- `enable`: Enable custom capture (true) or disable (false); default is false

**Note**: When enabled, the SDK does not capture images from the camera, only encodes and sends. Call before [startPush] to take effect.

### enableCustomAudioCapture
**Purpose**: Enable or disable custom audio capture
```dart
Future<V2TXLiveCode> enableCustomAudioCapture(bool enable)
```

**Parameters**:
- `enable`: Enable custom capture (true) or disable (false); default is false

**Note**: When enabled, the SDK does not capture audio from the microphone, only encodes and sends. Call before [startPush] to take effect.

### sendCustomVideoFrame
**Purpose**: Send custom video frame data to the SDK in custom video capture mode
```dart
Future<V2TXLiveCode> sendCustomVideoFrame(V2TXLiveVideoFrame videoFrame)
```

**Parameters**:
- `videoFrame`: Video frame data [V2TXLiveVideoFrame]

**Returns**:
- `V2TXLIVE_OK`: Success
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: Failed; invalid video frame data
- `V2TXLIVE_ERROR_REFUSED`: Failed; must enable custom video capture first

### sendCustomAudioFrame
**Purpose**: Send custom audio frame data to the SDK in custom audio capture mode
```dart
Future<V2TXLiveCode> sendCustomAudioFrame(V2TXLiveAudioFrame audioFrame)
```

**Parameters**:
- `audioFrame`: Audio frame data [V2TXLiveAudioFrame]

**Returns**:
- `V2TXLIVE_OK`: Success
- `V2TXLIVE_ERROR_REFUSED`: Failed; must enable custom audio capture first

### sendSeiMessage
**Purpose**: Send SEI message
```dart
Future<V2TXLiveCode> sendSeiMessage(int payloadType, Uint8List data)
```

**Parameters**:
- `payloadType`: Data type; supports 5 and 242 (recommended)
- `data`: Data to send

**Description**: The player receives the message via the [V2TXLivePlayerListenerType.onReceiveSeiMessage] callback.

### showDebugView
**Purpose**: Show or hide the debug panel
```dart
Future<V2TXLiveCode> showDebugView(bool isShow)
```

**Parameters**:
- `isShow`: Show (true) or hide (false); default is false

### setProperty
**Purpose**: Call advanced API methods on V2TXLivePusher
```dart
Future<V2TXLiveCode> setProperty(String key, Object value)
```

**Parameters**:
- `key`: Advanced API key
- `value`: Parameter for the advanced API; basic type or jsonString

**Returns**:
- `V2TXLIVE_OK`: Success
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: Failed; key cannot be empty

### setMixTranscodingConfig
**Purpose**: Configure cloud stream mixing transcoding parameters
```dart
Future<V2TXLiveCode> setMixTranscodingConfig(V2TXLiveTranscodingConfig? config)
```

**Parameters**:
- `config`: MixTranscoding configuration [V2TXLiveTranscodingConfig]; pass null to cancel cloud stream mixing

**Returns**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success
- `V2TXLIVE_ERROR_REFUSED`: Not allowed if streaming is not active

**Mixing Workflow**:
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
- **RTC protocol required for stream mixing**: This feature is only available with RTC protocol; not supported for RTMP or other protocols.
- Cloud transcoding adds 1–2 seconds of CDN viewing latency.
- Cancel mixing promptly by passing null to avoid unnecessary charges.
- Mixing is automatically cancelled when you Exit Room.

**When to Call**: During streaming

**Example**:
```dart
V2TXLiveTranscodingConfig config = V2TXLiveTranscodingConfig(
  videoWidth: 1280,
  videoHeight: 720,
  videoBitrate: 1500,
  videoFps: 15
);
await pusher.setMixTranscodingConfig(config);

// Cancel mixing
await pusher.setMixTranscodingConfig(null);
```

## Code Examples

### Basic Streaming Example (Camera + Microphone)
```dart
import 'package:tencent_trtc/v2_tx_live_pusher.dart';
import 'package:tencent_trtc/v2_tx_live_pusher_observer.dart';
import 'package:tencent_trtc/v2_tx_live_def.dart';
import 'package:tencent_trtc/v2_tx_live_code.dart';

class BasicPushExample {
  late V2TXLivePusher pusher;
  
  Future<void> setupBasicPush() async {
    // 1. Create pusher instance
    pusher = await V2TXLivePusher.create(V2TXLiveMode.V2TXLiveModeRTC);
    
    // 2. Register callback observer
    pusher.addListener(V2TXLivePusherObserver(
      onPushStatusUpdate: (status, msg, extraInfo) {
        // Handle streaming status changes
        switch (status) {
          case V2TXLivePushStatus.V2TXLivePushStatusDisconnected:
            print('Streaming connection disconnected');
            break;
          case V2TXLivePushStatus.V2TXLivePushStatusConnecting:
            print('Connecting to streaming server');
            break;
          case V2TXLivePushStatus.V2TXLivePushStatusConnectSuccess:
            print('Streaming connection successful');
            break;
          case V2TXLivePushStatus.V2TXLivePushStatusReconnecting:
            print('Reconnecting streaming');
            break;
        }
      },
      onStatisticsUpdate: (statistics) {
        // Handle statistics
        print('App CPU: ${statistics.appCpu}%, System CPU: ${statistics.systemCpu}%');
        print('Width: ${statistics.width}, Height: ${statistics.height}');
        print('FPS: ${statistics.fps}, Video Bitrate: ${statistics.videoBitrate}');
        print('Audio Bitrate: ${statistics.audioBitrate}');
      },
      onError: (code, msg, extraInfo) {
        // Handle error information
        print('Streaming error: code=$code, msg=$msg');
      }
    ));
    
    // 3. Set preview view
    await pusher.setRenderViewID(yourTextureViewID);
    
    // 4. Start at least one capture source before streaming
    // Start camera capture (front camera)
    await pusher.startCamera(true);
    
    // Start microphone capture
    await pusher.startMicrophone();
    
    // 5. Start streaming
    String pushUrl = "rtmp://your-push-server/live/streamid";
    V2TXLiveCode result = await pusher.startPush(pushUrl);
    
    if (result == V2TXLiveCode.V2TXLIVE_OK) {
      print('✅ Streaming started successfully');
    } else if (result == V2TXLiveCode.V2TXLIVE_ERROR_INVALID_PARAMETER) {
      print('❌ Invalid streaming address');
    } else if (result == V2TXLiveCode.V2TXLIVE_ERROR_INVALID_LICENSE) {
      print('❌ Invalid Licence, please check your Licence');
    } else if (result == V2TXLiveCode.V2TXLIVE_ERROR_REFUSED) {
      print('❌ Call refused');
    }
  }
  
  Future<void> stopPush() async {
    // Stop streaming
    await pusher.stopPush();
    // Stop capture sources
    await pusher.stopCamera();
    await pusher.stopMicrophone();
    // Destroy instance
    pusher.destroy();
  }
}
```

### Advanced Configuration Example

```dart
// Set video encoding parameters
V2TXLiveVideoEncoderParam videoParam = V2TXLiveVideoEncoderParam(
  videoResolution: V2TXLiveVideoResolution.v2TXLiveVideoResolution1280x720,
  videoResolutionMode: V2TXLiveVideoResolutionMode.v2TXLiveVideoResolutionModeLandscape,
  videoFps: 15,
  videoBitrate: 1200,
  minVideoBitrate: 800,
);
await pusher.setVideoQuality(videoParam);

// Set audio quality
await pusher.setAudioQuality(V2TXLiveAudioQuality.v2TXLiveAudioQualityMusic);

// Enable volume evaluation
await pusher.enableVolumeEvaluation(300);

// Show debug panel
await pusher.showDebugView(true);
```

### Custom Capture Example

```dart
// Enable custom video capture
await pusher.enableCustomVideoCapture(true);

// Custom video frame processing
V2TXLiveVideoFrame videoFrame = V2TXLiveVideoFrame(
  pixelFormat: V2TXLivePixelFormat.v2TXLivePixelFormatI420,
  bufferType: V2TXLiveBufferType.v2TXLiveBufferTypeByteBuffer,
  data: yourVideoData,
  width: 640,
  height: 480,
  rotation: V2TXLiveRotation.v2TXLiveRotation0,
);

// Send custom video frame
await pusher.sendCustomVideoFrame(videoFrame);
```

## Notes

### 1. Capture Source Requirements
**You must start at least one capture source before streaming; otherwise, streaming will fail:**
- **Camera capture**: `startCamera()` + `startMicrophone()`
- **Screen capture**: `startScreenCapture()` + `startMicrophone()`
- **Image streaming**: `startVirtualCamera()` + `startMicrophone()`
- **Custom capture**: `enableCustomVideoCapture()` + `enableCustomAudioCapture()`
- **Audio-only streaming**: `startMicrophone()`

### 2. Capture Source Switching Rules
- Only one capture source can be active per pusher instance.
- To switch sources, stop the current source before starting a new one.

### 3. Call Sequence Requirements
1. Create pusher instance
2. Register callbacks and set preview view
3. Start at least one capture source
4. Call `startPush()` to begin streaming

### 4. Custom Capture Guidelines
- Call custom capture-related methods before `startPush` to take effect.
- In custom capture mode, the SDK only encodes and sends data; it does not perform actual capture.

### 5. Cloud Stream Mixing Guidelines
- **Protocol restriction**: Cloud stream mixing is only supported with RTC protocol; not available for RTMP or other protocols.
- Cancel mixing promptly to avoid unnecessary charges.
- Cloud transcoding adds 1–2 seconds of CDN viewing latency.

### 6. Local Recording Guidelines
- Recording can only start after streaming begins.
- Do not change resolution or switch between hardware/software encoding during recording.

### 7. System Audio Capture Requirements
- Requires Android API 29 or higher.
- Must use a foreground service to prevent capture from being silenced.
- Only effective during screen sharing.

### 8. Performance Optimization Tips
- Choose audio/video quality settings appropriate for your scenario.
- Release unused pusher instances promptly.
- Use pause/resume features to conserve bandwidth.

### 9. Error Handling Recommendations
- Handle the `onError` callback and notify users appropriately.
- The SDK automatically reconnects on network exceptions; no manual intervention required.
- Update Licence configuration promptly when it expires.

### 10. Permissions and Resource Management
- Ensure your app has camera and microphone permissions.
- Call `destroy` promptly to release resources.
- Prevent memory leaks by removing observers in a timely manner.