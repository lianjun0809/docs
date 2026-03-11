> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/en/llms.txt
> Use this file to discover all available pages before exploring further.

# Tencent Cloud Live Streaming SDK V2TXLiveDef Type Definition Documentation

## Feature Overview

`V2TXLiveDef` is the primary type definition file for the Tencent Cloud Live Streaming SDK. It includes all enumerations, constants, and data structures required for live stream publishing and playback.

**File Path**: `v2_tx_live_def.dart`

**Core Features**:
- Defines video and audio enumerations and constants
- Provides data structures for statistics and configuration parameters
- Supports configuration for cloud stream mixing and local recording

## 1. Supported Protocols

### V2TXLiveMode - Supported Protocols for Live Stream Publishing
```dart
enum V2TXLiveMode {
  /// Supported protocol: RTMP
  v2TXLiveModeRTMP,
  
  /// Supported protocol: RTC
  v2TXLiveModeRTC,
}
```

## Render View Definition

### V2TXLiveRenderView

Defines the video rendering view type.

```dart
class V2TXLiveRenderView {
  static const String renderViewType = 'v2_live_view_factory';
}
```

## Protocol Support

### V2TXLiveMode

Enumerates the supported live streaming protocols:

| Enum Value | Description |
|------------|-------------|
| `v2TXLiveModeRTMP` | RTMP protocol |
| `v2TXLiveModeRTC` | TRTC protocol |

## 2. Video Type Definitions

### V2TXLiveVideoResolution - Video Resolution Enumeration
```dart
enum V2TXLiveVideoResolution {
  /// 160x160, bitrate: 100Kbps ~ 150Kbps, frame rate: 15fps.
  v2TXLiveVideoResolution160x160,
  
  /// 270x270, bitrate: 200Kbps ~ 300Kbps, frame rate: 15fps.
  v2TXLiveVideoResolution270x270,

  /// 480x480, bitrate: 350Kbps ~ 525Kbps, frame rate: 15fps.
  v2TXLiveVideoResolution480x480,

  /// 320x240, bitrate: 250Kbps ~ 375Kbps, frame rate: 15fps.
  v2TXLiveVideoResolution320x240,

  /// 480x360, bitrate: 400Kbps ~ 600Kbps, frame rate: 15fps.
  v2TXLiveVideoResolution480x360,

  /// 640x480, bitrate: 600Kbps ~ 900Kbps, frame rate: 15fps.
  v2TXLiveVideoResolution640x480,

  /// 320x180, bitrate: 250Kbps ~ 400Kbps, frame rate: 15fps.
  v2TXLiveVideoResolution320x180,

  /// 480x270, bitrate: 350Kbps ~ 550Kbps, frame rate: 15fps.
  v2TXLiveVideoResolution480x270,

  /// 640x360, bitrate: 500Kbps ~ 900Kbps, frame rate: 15fps.
  v2TXLiveVideoResolution640x360,

  /// 960x540, bitrate: 800Kbps ~ 1500Kbps, frame rate: 15fps.
  v2TXLiveVideoResolution960x540,

  /// 1280x720, bitrate: 1000Kbps ~ 1800Kbps, frame rate: 15fps.
  v2TXLiveVideoResolution1280x720,

  /// 1920x1080, bitrate: 2500Kbps ~ 3000Kbps, frame rate: 15fps.
  v2TXLiveVideoResolution1920x1080,
}
```

| Resolution | Bitrate Range | Frame Rate | Description |
|------------|--------------|------------|-------------|
| 160×160 | 100-150Kbps | 15fps | Ultra-low resolution, ideal for voice calls |
| 270×270 | 200-300Kbps | 15fps | Low resolution |
| 480×480 | 350-525Kbps | 15fps | Standard square resolution |
| 320×240 | 250-375Kbps | 15fps | Standard 4:3 aspect ratio |
| 480×360 | 400-600Kbps | 15fps | Medium 4:3 aspect ratio |
| 640×480 | 600-900Kbps | 15fps | SD resolution |
| 320×180 | 250-400Kbps | 15fps | Low 16:9 aspect ratio |
| 480×270 | 350-550Kbps | 15fps | Standard 16:9 aspect ratio |
| 640×360 | 500-900Kbps | 15fps | Medium 16:9 aspect ratio |
| 960×540 | 800-1500Kbps | 15fps | HD resolution |
| 1280×720 | 1000-1800Kbps | 15fps | 720p HD |
| 1920×1080 | 2500-3000Kbps | 15fps | 1080p Full HD |

### V2TXLiveVideoResolutionMode

Video resolution orientation:

| Enum Value | Description |
|------------|-------------|
| `v2TXLiveVideoResolutionModeLandscape` | Landscape orientation |
| `v2TXLiveVideoResolutionModePortrait` | Portrait orientation |

**Note**: The orientation affects the actual resolution dimensions. For example:
- Landscape: 640×360 = 640×360
- Portrait: 640×360 = 360×640

## Video Encoder Parameters

### V2TXLiveVideoResolutionMode - Video Orientation Mode
```dart
enum V2TXLiveVideoResolutionMode {
  /// Landscape orientation
  v2TXLiveVideoResolutionModeLandscape,
  
  /// Portrait orientation
  v2TXLiveVideoResolutionModePortrait,
}
```

### V2TXLiveVideoEncoderParam - Video Encoder Parameter Configuration
```dart
class V2TXLiveVideoEncoderParam {
  V2TXLiveVideoResolution videoResolution;      // Video resolution
  V2TXLiveVideoResolutionMode videoResolutionMode; // Resolution orientation
  int videoFps;                                 // Capture frame rate
  int videoBitrate;                             // Target video bitrate
  int minVideoBitrate;                          // Minimum video bitrate
}
```

**Recommended Settings**:
- **Frame Rate**: 15fps or 20fps. Using less than 5fps can cause severe playback stuttering; above 20fps may result in unnecessary bandwidth usage.
- **Adaptive Bitrate**: Set both `videoBitrate` and `minVideoBitrate` to define the range for bitrate adaptation.

## Video Preview and Fill Modes

### V2TXLiveMirrorType - Camera Mirror Mode
```dart
enum V2TXLiveMirrorType {
  /// System default: front camera mirrored, rear camera not mirrored
  v2TXLiveMirrorTypeAuto,
  
  /// Mirror mode for both front and rear cameras
  v2TXLiveMirrorTypeEnable,
  
  /// No mirror mode for either camera
  v2TXLiveMirrorTypeDisable,
}
```

### V2TXLiveFillMode - Video Fill Mode
```dart
enum V2TXLiveFillMode {
  /// Image fills the screen; excess is cropped, some content may be lost
  v2TXLiveFillModeFill,
  
  /// Long edge fills the screen; short edge is padded with black, full content retained
  v2TXLiveFillModeFit,
  
  /// Image is stretched to fill; aspect ratio may not be preserved
  v2TXLiveFillModeScaleFill
}
```

### V2TXLiveRotation - Video Rotation Angle
```dart
enum V2TXLiveRotation {
  /// No rotation
  v2TXLiveRotation0,
  
  /// Rotate 90 degrees clockwise
  v2TXLiveRotation90,
  
  /// Rotate 180 degrees clockwise
  v2TXLiveRotation180,
  
  /// Rotate 270 degrees clockwise
  v2TXLiveRotation270,
}
```

### V2TXLivePixelFormat - Video Frame Pixel Format
```dart
enum V2TXLivePixelFormat {
  /// Unknown
  v2TXLivePixelFormatUnknown,
  
  /// YUV420P I420 format
  v2TXLivePixelFormatI420,
  
  /// YUV420SP NV12 format
  v2TXLivePixelFormatNV12,
  
  /// BGRA8888 format
  v2TXLivePixelFormatBGRA32,
  
  /// OpenGL 2D texture format
  v2TXLivePixelFormatTexture2D,
}
```
### V2TXLiveBufferType - Video Data Buffer Format
```dart
enum V2TXLiveBufferType {
  /// Unknown
  v2TXLiveBufferTypeUnknown,
  
  /// DirectBuffer for I420 and similar buffers, used in native layer
  v2TXLiveBufferTypeByteBuffer,
  
  /// byte[] for I420 and similar buffers, used in Java layer
  v2TXLiveBufferTypeByteArray,
  
  /// Operates directly on texture ID, optimal performance, minimal quality loss
  v2TXLiveBufferTypeTexture,
}
```

### V2TXLiveVideoFrame - Video Frame Information
```dart
class V2TXLiveVideoFrame {
  V2TXLivePixelFormat pixelFormat;              // Video frame pixel format
  V2TXLiveBufferType bufferType;                // Video data buffer format
  Uint8List? data;                             // Video data
  int width;                                   // Video width
  int height;                                  // Video height
  V2TXLiveRotation rotation;                   // Video frame rotation angle
  int? textureId;                              // Video texture ID
}
```

## 3. Audio Type Definitions

### V2TXLiveAudioQuality - Audio Quality Settings
```dart
enum V2TXLiveAudioQuality {
  /// Speech quality: 16k sample rate, mono, 16kbps bitrate, ideal for voice calls
  v2TXLiveAudioQualitySpeech,
  
  /// Default quality: 48k sample rate, mono, 50kbps bitrate (SDK default)
  v2TXLiveAudioQualityDefault,
  
  /// Music quality: 48k sample rate, stereo/full band, 128kbps bitrate, suitable for high-fidelity music
  v2TXLiveAudioQualityMusic,
}
```

### V2TXLiveAudioFrame - Audio Frame Data
```dart
class V2TXLiveAudioFrame {
  Uint8List data;          // Audio data
  int sampleRate;         // Sample rate (default 48000Hz)
  int channel;            // Audio channel count (default 1, mono)
  int timestamp;          // Timestamp in ms
}
```

## 4. Statistics Data Definitions

### V2TXLivePusherStatistics - Stream Publisher Statistics
```dart
class V2TXLivePusherStatistics {
  int appCpu;           // App CPU usage (%)
  int systemCpu;        // System CPU usage (%)
  int width;            // Video width
  int height;           // Video height
  int fps;              // Frame rate (fps)
  int videoBitrate;     // Video bitrate (Kbps)
  int audioBitrate;     // Audio bitrate (Kbps)
  int rtt;              // SDK to cloud Round-Trip Time (RTT) (ms)
  int netSpeed;         // Upload speed (kbps)
}
```

### V2TXLivePlayerStatistics - Player Statistics
```dart
class V2TXLivePlayerStatistics {
  int appCpu;                   // App CPU usage (%)
  int systemCpu;                // System CPU usage (%)
  int width;                    // Video width
  int height;                   // Video height
  int fps;                      // Frame rate (fps)
  int videoBitrate;             // Video bitrate (Kbps)
  int audioBitrate;             // Audio bitrate (Kbps)
  int audioPacketLoss;          // Audio packet loss rate (%)
  int videoPacketLoss;          // Video packet loss rate (%)
  int jitterBufferDelay;        // Playback delay (ms)
  int audioTotalBlockTime;      // Total audio playback stuttering duration (ms)
  int audioBlockRate;           // Audio playback stuttering rate (%)
  int videoTotalBlockTime;      // Total video playback stuttering duration (ms)
  int videoBlockRate;           // Video playback stuttering rate (%)
  int rtt;                      // Round-Trip Time (RTT) (ms)
  int netSpeed;                 // Download speed (kbps)
}
```

## 5. Connection Status Enumerations

### V2TXLivePushStatus - Live Stream Connection Status
```dart
enum V2TXLivePushStatus {
  /// Disconnected from server
  v2TXLivePushStatusDisconnected,
  
  /// Connecting to server
  v2TXLivePushStatusConnecting,
  
  /// Connected to server
  v2TXLivePushStatusConnectSuccess,
  
  /// Reconnecting to server
  v2TXLivePushStatusReconnecting,
}
```

## 6. Cloud Stream Mixing Configuration

### V2TXLiveMixInputType - Cloud Stream Mixing Input Type
```dart
enum V2TXLiveMixInputType {
  /// Mix audio and video
  v2TXLiveMixInputTypeAudioVideo,
  
  /// Mix video only
  v2TXLiveMixInputTypePureVideo,
  
  /// Mix audio only
  v2TXLiveMixInputTypePureAudio,
}
```

### V2TXLiveMixStream - Cloud Stream Mixing Sub-Screen Position
```dart
class V2TXLiveMixStream {
  String userId;                // User ID for stream mixing
  String? streamId;            // Stream publishing streamId
  int x;                        // Layer X coordinate (pixels)
  int y;                        // Layer Y coordinate (pixels)
  int width;                    // Layer width (pixels)
  int height;                   // Layer height (pixels)
  int zOrder;                   // Layer z-order (1-15, unique)
  V2TXLiveMixInputType inputType; // Stream input type
}
```

### V2TXLiveTranscodingConfig - Cloud Stream Mixing MixTranscoding Configuration
```dart
class V2TXLiveTranscodingConfig {
  int videoWidth;               // Output video width after transcoding
  int videoHeight;              // Output video height after transcoding
  int videoBitrate;             // Output video bitrate after transcoding (kbps)
  int videoFramerate;           // Output video frame rate after transcoding (FPS)
  int videoGOP;                 // Keyframe interval (seconds)
  int backgroundColor;          // Mixed output background color
  String? backgroundImage;      // Mixed output background image
  int audioSampleRate;          // Output audio sample rate after transcoding
  int audioBitrate;             // Output audio bitrate after transcoding (kbps)
  int audioChannels;            // Output audio channel count after transcoding
  List<V2TXLiveMixStream> mixStreams; // Sub-screen position info
  String? outputStreamId;        // Output stream ID for CDN
}
```

## 7. Local Recording Configuration

### V2TXLiveRecordMode - Local Recording Mode
```dart
enum V2TXLiveRecordMode {
  /// Record both audio and video
  v2TXLiveRecordModeBoth,
}
```

### V2TXLiveLocalRecordingParams - Local Recording Configuration
```dart
class V2TXLiveLocalRecordingParams {
  String filePath;              // Recording file path (required)
  V2TXLiveRecordMode recordMode; // Recording mode
  int interval;                 // Recording info update interval (ms)
}
```

## Stream Mixing Configuration

### V2TXLiveMixInputType

Cloud stream mixing input type:

| Enum Value | Description |
|------------|-------------|
| `v2TXLiveMixInputTypeAudioVideo` | Mix audio and video |
| `v2TXLiveMixInputTypePureVideo` | Mix video only |
| `v2TXLiveMixInputTypePureAudio` | Mix audio only |

### V2TXLiveMixStream

Cloud stream mixing screen position configuration:

```dart
class V2TXLiveMixStream {
  String userId;
  String? streamId;
  int x;
  int y;
  int width;
  int height;
  int zOrder;
  V2TXLiveMixInputType inputType;
}
```

### V2TXLiveTranscodingConfig

Cloud stream mixing (MixTranscoding) configuration:

```dart
class V2TXLiveTranscodingConfig {
  int videoWidth;
  int videoHeight;
  int videoBitrate;
  int videoFramerate;
  int videoGOP;
  int backgroundColor;
  String? backgroundImage;
  int audioSampleRate;
  int audioBitrate;
  int audioChannels;
  List<V2TXLiveMixStream> mixStreams;
  String? outputStreamId;
}
```

**Parameter Notes**:

- **Audio-only streaming**: Set `videoWidth × videoHeight = 0px × 0px`
- **Background image**: Upload the image in the Tencent Cloud Console to obtain the Image ID
- **Output stream ID**: If not set, the mixed stream defaults to the API caller's video stream

## 8. Log Configuration

### V2TXLiveLogLevel - Log Level Enumeration
```dart
class V2TXLiveLogLevel {
  static const int v2TXLiveLogLevelAll = 0;      // Output all log levels
  static const int v2TXLiveLogLevelDebug = 1;   // Output DEBUG and above
  static const int v2TXLiveLogLevelInfo = 2;    // Output INFO and above
  static const int v2TXLiveLogLevelWarning = 3; // Output WARNING and above
  static const int v2TXLiveLogLevelError = 4;   // Output ERROR and above
  static const int v2TXLiveLogLevelFatal = 5;   // Output FATAL only
  static const int v2TXLiveLogLevelNULL = 6;    // Disable all SDK logs
}
```

### V2TXLiveLogConfig - Log Configuration
```dart
class V2TXLiveLogConfig {
  int logLevel;                  // Log level
  bool enableObserver;           // Receive logs via Observer
  bool enableConsole;            // Print logs to editor console
  bool enableLogFile;            // Enable local log file
  String? logPath;               // Local log storage directory
}
```

**Default Log Storage Paths**:
- iOS & Mac: Sandbox Documents/log
- Android 6.7 and below: /sdcard/log/liteav
- Android 6.8 and above: /sdcard/Android/data/package_name/files/log/liteav/

## 9. Other Configurations

### V2TXLiveSocks5ProxyConfig - SOCKS5 Proxy Configuration
```dart
class V2TXLiveSocks5ProxyConfig {
  bool supportHttps = true;  // Enable HTTPS
  bool supportTcp = true;    // Enable TCP
  bool supportUdp = true;    // Enable UDP
}
```

### V2TXLiveStreamInfo - Adaptive Bitrate Stream Information
```dart
class V2TXLiveStreamInfo {
  int width;                    // Video width
  int height;                   // Video height
  int bitrate;                  // Bitrate (bps)
  double framerate;             // Frame rate
  String url;                   // Stream URL
}
```

### TXSystemVolumeType - System Volume Control Type
```dart
class TXSystemVolumeType {
  static const int TXSystemVolumeTypeAuto = 0;   // Auto mode switching
  static const int TXSystemVolumeTypeMedia = 1;  // Media volume
  static const int TXSystemVolumeTypeVOIP = 2;   // Call volume
}
```

### TXAudioRoute - Audio Routing Type
```dart
class TXAudioRoute {
  static const int TXAudioRouteSpeakerphone = 0; // Play via the speaker
  static const int TXAudioRouteEarpiece = 1;     // Play via the receiver
}
```

## 10. Audio Effects Processing

### TXVoiceReverbType - Reverb Effect Types
```dart
class TXVoiceReverbType {
  static const int TXVoiceReverbTypeOff = 0;       // Disable reverb
  static const int TXVoiceReverbTypeKTV = 1;       // KTV
  static const int TXVoiceReverbTypeSmallRoom = 2; // Small room
  static const int TXVoiceReverbTypeGreatHall = 3; // Great hall
  static const int TXVoiceReverbTypeDeep = 4;      // Deep
  static const int TXVoiceReverbTypeLoud = 5;      // Loud
  static const int TXVoiceReverbTypeMetallic = 6;  // Metallic
  static const int TXVoiceReverbTypeMagnetic = 7;  // Magnetic
  static const int TXVoiceReverbTypeEthereal = 8;  // Ethereal
  static const int TXVoiceReverbTypeStudio = 9;    // Studio
  static const int TXVoiceReverbTypeMelodious = 10;// Melodious
  static const int TXVoiceReverbTypeStudio2 = 11;  // Studio 2
}
```

### TXVoiceChangerType - Voice Changer Effect Types
```dart
class TXVoiceChangerType {
  static const int TXVoiceChangerTypeOff = 0;        // Disable voice changer
  static const int TXVoiceChangerTypeChild = 1;      // Naughty boy
  static const int TXVoiceChangerTypeLittleGirl = 2; // Girl
  static const int TXVoiceChangerTypeUncle = 3;      // Middle-aged man
  static const int TXVoiceChangerTypeHeavyMetal = 4; // Heavy metal
  static const int TXVoiceChangerTypeCold = 5;       // Cold
  static const int TXVoiceChangerTypePunk = 6;       // Punk
  static const int TXVoiceChangerTypeBeast = 7;      // Beast
  static const int TXVoiceChangerTypeFatty = 8;      // Fatty
  static const int TXVoiceChangerTypeStrongCurrent = 9; // Strong current
  static const int TXVoiceChangerTypeRobot = 10;     // Robot
  static const int TXVoiceChangerTypeEthereal = 11;  // Ethereal
}
```