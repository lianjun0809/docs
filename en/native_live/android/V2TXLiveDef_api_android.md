> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

# Tencent Cloud Live Streaming SDK V2TXLiveDef Type Definitions

## Feature Overview

`V2TXLiveDef` is the primary type definition file for the Tencent Cloud Live Streaming SDK. It includes all enumerations, constants, and data structures required for live streaming push and playback.

**File Path**: `com/tencent/live2/V2TXLiveDef.java`

**Core Features**:
- Defines video and audio enumerations and constants
- Provides data structures for statistics and configuration parameters
- Supports configuration for cloud stream mixing and local recording

## 1. Supported Protocols

### V2TXLiveMode - Supported Protocols for Live Streaming Push
```java
public enum V2TXLiveMode {
    /// Supported protocol: RTMP
    TXLiveMode_RTMP,
    
    /// Supported protocol: RTC
    TXLiveMode_RTC;
}
```

## 2. Video Type Definitions

### V2TXLiveVideoResolution - Video Resolution Enumeration
```java
public enum V2TXLiveVideoResolution {
    /// 160x160, bitrate: 100–150 Kbps, frame rate: 15 fps
    V2TXLiveVideoResolution160x160,
    
    /// 270x270, bitrate: 200–300 Kbps, frame rate: 15 fps
    V2TXLiveVideoResolution270x270,

    /// 480x480, bitrate: 350–525 Kbps, frame rate: 15 fps
    V2TXLiveVideoResolution480x480,

    /// 320x240, bitrate: 250–375 Kbps, frame rate: 15 fps
    V2TXLiveVideoResolution320x240,

    /// 480x360, bitrate: 400–600 Kbps, frame rate: 15 fps
    V2TXLiveVideoResolution480x360,

    /// 640x480, bitrate: 600–900 Kbps, frame rate: 15 fps
    V2TXLiveVideoResolution640x480,

    /// 320x180, bitrate: 250–400 Kbps, frame rate: 15 fps
    V2TXLiveVideoResolution320x180,

    /// 480x270, bitrate: 350–550 Kbps, frame rate: 15 fps
    V2TXLiveVideoResolution480x270,

    /// 640x360, bitrate: 500–900 Kbps, frame rate: 15 fps
    V2TXLiveVideoResolution640x360,

    /// 960x540, bitrate: 800–1500 Kbps, frame rate: 15 fps
    V2TXLiveVideoResolution960x540,

    /// 1280x720, bitrate: 1000–1800 Kbps, frame rate: 15 fps
    V2TXLiveVideoResolution1280x720,

    /// 1920x1080, bitrate: 2500–3000 Kbps, frame rate: 15 fps
    V2TXLiveVideoResolution1920x1080,
}
```

| Resolution   | Bitrate Range | Frame Rate | Description                                 |
|--------------|--------------|------------|---------------------------------------------|
| 160×160      | 100–150 Kbps | 15 fps     | Ultra-low resolution, ideal for voice calls |
| 270×270      | 200–300 Kbps | 15 fps     | Low resolution                              |
| 480×480      | 350–525 Kbps | 15 fps     | Standard square resolution                  |
| 320×240      | 250–375 Kbps | 15 fps     | 4:3 aspect ratio, standard resolution       |
| 480×360      | 400–600 Kbps | 15 fps     | 4:3 aspect ratio, medium resolution         |
| 640×480      | 600–900 Kbps | 15 fps     | SD resolution                               |
| 320×180      | 250–400 Kbps | 15 fps     | 16:9 aspect ratio, low resolution           |
| 480×270      | 350–550 Kbps | 15 fps     | 16:9 aspect ratio, standard resolution      |
| 640×360      | 500–900 Kbps | 15 fps     | 16:9 aspect ratio, medium resolution        |
| 960×540      | 800–1500 Kbps| 15 fps     | HD resolution                               |
| 1280×720     | 1000–1800 Kbps| 15 fps    | 720p HD                                     |
| 1920×1080    | 2500–3000 Kbps| 15 fps    | 1080p Full HD                               |

### V2TXLiveVideoResolutionMode - Video Orientation Mode
```java
public enum V2TXLiveVideoResolutionMode {
    /// Landscape orientation
    V2TXLiveVideoResolutionModeLandscape,
    
    /// Portrait orientation
    V2TXLiveVideoResolutionModePortrait,
}
```

### V2TXLiveVideoEncoderParam - Video Encoder Parameter Configuration
```java
public final static class V2TXLiveVideoEncoderParam {
    public V2TXLiveVideoResolution videoResolution;         // Video resolution
    public V2TXLiveVideoResolutionMode videoResolutionMode; // Orientation mode
    public int videoFps;                                   // Capture frame rate
    public int videoBitrate;                               // Target video bitrate
    public int minVideoBitrate;                            // Minimum video bitrate
}
```

**Recommended Settings**:
- **Frame Rate**: Use 15 fps or 20 fps. Frame rates below 5 fps will result in noticeable stuttering, while rates above 20 fps may waste bandwidth.
- **Adaptive Bitrate**: Set both `videoBitrate` and `minVideoBitrate` to define the bitrate adjustment range.

### V2TXLiveMirrorType - Local Camera Mirror Mode
```java
public enum V2TXLiveMirrorType {
    /// System default: front camera mirrored, rear camera not mirrored
    V2TXLiveMirrorTypeAuto,
    
    /// Both front and rear cameras mirrored
    V2TXLiveMirrorTypeEnable,
    
    /// Both front and rear cameras not mirrored
    V2TXLiveMirrorTypeDisable,
}
```

### V2TXLiveFillMode - Video Fill Mode
```java
public enum V2TXLiveFillMode {
    /// Image fills the view, cropping excess; some content may be lost
    V2TXLiveFillModeFill,
    
    /// Image's longer side fits the view, shorter side padded with black; full content retained
    V2TXLiveFillModeFit,
    
    /// Image stretched to fill view; aspect ratio may not be preserved
    V2TXLiveFillModeScaleFill
}
```

### V2TXLiveRotation - Video Rotation Angle
```java
public enum V2TXLiveRotation {
    /// No rotation
    V2TXLiveRotation0,
    
    /// 90° clockwise rotation
    V2TXLiveRotation90,
    
    /// 180° clockwise rotation
    V2TXLiveRotation180,
    
    /// 270° clockwise rotation
    V2TXLiveRotation270,
}
```

### V2TXLivePixelFormat - Video Frame Pixel Format
```java
public enum V2TXLivePixelFormat {
    /// Unknown format
    V2TXLivePixelFormatUnknown,
    
    /// YUV420P I420 format
    V2TXLivePixelFormatI420,
    
    /// OpenGL 2D texture format
    V2TXLivePixelFormatTexture2D,
}
```

### V2TXLiveBufferType - Video Data Buffer Type
```java
public enum V2TXLiveBufferType {
    /// Unknown type
    V2TXLiveBufferTypeUnknown,
    
    /// DirectBuffer, stores I420 and other buffers, used at the native layer
    V2TXLiveBufferTypeByteBuffer,
    
    /// byte[], stores I420 and other buffers, used at the Java layer
    V2TXLiveBufferTypeByteArray,
    
    /// Operates directly on texture ID for optimal performance and minimal quality loss
    V2TXLiveBufferTypeTexture,
}
```

### V2TXLiveTexture - Video Texture Wrapper
```java
public final static class V2TXLiveTexture {
    public int textureId;                                   // Video texture ID
    public javax.microedition.khronos.egl.EGLContext eglContext10; // OpenGL EGLContext (v1.0)
    public android.opengl.EGLContext eglContext14;          // Android EGLContext (v1.4)
}
```

### V2TXLiveVideoFrame - Video Frame Information
```java
public final static class V2TXLiveVideoFrame {
    public V2TXLivePixelFormat pixelFormat;                 // Pixel format
    public V2TXLiveBufferType bufferType;                   // Buffer type
    public V2TXLiveTexture texture;                         // Texture wrapper
    public byte[] data;                                     // Video data
    public ByteBuffer buffer;                               // Video data buffer
    public int width;                                       // Frame width
    public int height;                                      // Frame height
    public int rotation;                                    // Rotation angle
}
```

## 3. Audio Type Definitions

### V2TXLiveAudioQuality - Audio Quality Settings
```java
public enum V2TXLiveAudioQuality {
    /// Speech: 16kHz sample rate, mono, 16 Kbps, suitable for voice calls
    V2TXLiveAudioQualitySpeech,
    
    /// Default: 48kHz sample rate, mono, 50 Kbps, SDK default
    V2TXLiveAudioQualityDefault,
    
    /// Music: 48kHz sample rate, stereo, full band, 128 Kbps, for high-fidelity music
    V2TXLiveAudioQualityMusic,
}
```

### V2TXLiveAudioFrame - Audio Frame Data
```java
public final static class V2TXLiveAudioFrame {
    public byte[] data;          // Audio data
    public int sampleRate;       // Sample rate (default: 48000 Hz)
    public int channel;          // Audio channel count (default: 1, mono)
    public long timestamp;       // Timestamp (ms)
}
```

### V2TXLiveAudioFrameOperationMode - Audio Callback Data Access Mode
```java
public enum V2TXLiveAudioFrameOperationMode {
    /// Read/write mode: access and modify callback audio data (default)
    V2TXLiveAudioFrameOperationModeReadWrite,
    
    /// Read-only mode: access callback audio data only
    V2TXLiveAudioFrameOperationModeReadOnly,
}
```

### V2TXLiveAudioFrameObserverFormat - Audio Frame Callback Format
```java
public final static class V2TXLiveAudioFrameObserverFormat {
    public int sampleRate;                               // Sample rate (default: 48000 Hz)
    public int channel;                                  // Audio channel count (default: 1)
    public int samplesPerCall;                           // Samples per callback
    public V2TXLiveAudioFrameOperationMode mode;         // Data access mode
}
```

## 4. Statistics Data Definitions

### V2TXLivePusherStatistics - Pusher Statistics
```java
public final static class V2TXLivePusherStatistics {
    public int appCpu;           // App CPU usage (%)
    public int systemCpu;        // System CPU usage (%)
    public int width;            // Video width
    public int height;           // Video height
    public int fps;              // Frame rate (fps)
    public int videoBitrate;     // Video bitrate (Kbps)
    public int audioBitrate;     // Audio bitrate (Kbps)
    public int rtt;              // SDK to cloud Round-Trip Time (RTT) (ms)
    public int netSpeed;         // Uplink speed (Kbps)
}
```

### V2TXLivePlayerStatistics - Player Statistics
```java
public final static class V2TXLivePlayerStatistics {
    public int appCpu;                   // App CPU usage (%)
    public int systemCpu;                // System CPU usage (%)
    public int width;                    // Video width
    public int height;                   // Video height
    public int fps;                      // Frame rate (fps)
    public int videoBitrate;             // Video bitrate (Kbps)
    public int audioBitrate;             // Audio bitrate (Kbps)
    public int audioPacketLoss;          // Audio packet loss rate (%)
    public int videoPacketLoss;          // Video packet loss rate (%)
    public int jitterBufferDelay;        // Playback delay (ms)
    public int audioTotalBlockTime;      // Total audio playback stuttering time (ms)
    public int audioBlockRate;           // Audio playback stuttering rate (%)
    public int videoTotalBlockTime;      // Total video playback stuttering time (ms)
    public int videoBlockRate;           // Video playback stuttering rate (%)
    public int rtt;                      // Round-Trip Time (RTT) (ms)
    public int netSpeed;                 // Download speed (Kbps)
}
```

## 5. Connection Status Enumerations

### V2TXLivePushStatus - Live Stream Connection Status
```java
public enum V2TXLivePushStatus {
    /// Disconnected from server
    V2TXLivePushStatusDisconnected,
    
    /// Connecting to server
    V2TXLivePushStatusConnecting,
    
    /// Connected to server
    V2TXLivePushStatusConnectSuccess,
    
    /// Reconnecting to server
    V2TXLivePushStatusReconnecting,
}
```

## 6. Cloud Stream Mixing Configuration

### V2TXLiveMixInputType - Stream Mixing Input Type
```java
public enum V2TXLiveMixInputType {
    /// Mix audio and video
    V2TXLiveMixInputTypeAudioVideo,
    
    /// Mix video only
    V2TXLiveMixInputTypePureVideo,
    
    /// Mix audio only
    V2TXLiveMixInputTypePureAudio,
}
```

### V2TXLiveMixStream - Cloud Stream Mixing Sub-Screen Layout
```java
public static class V2TXLiveMixStream {
    public String userId;                // userId participating in cloud stream mixing
    public String streamId;              // Push streamId
    public int x;                        // X coordinate (absolute pixels)
    public int y;                        // Y coordinate (absolute pixels)
    public int width;                    // Layer width (absolute pixels)
    public int height;                   // Layer height (absolute pixels)
    public int zOrder;                   // Layer z-order (1–15, must be unique)
    public V2TXLiveMixInputType inputType; // Input type
}
```

### V2TXLiveTranscodingConfig - Cloud Stream Mixing MixTranscoding Configuration
```java
public final static class V2TXLiveTranscodingConfig {
    public int videoWidth;               // Output video width after transcoding
    public int videoHeight;              // Output video height after transcoding
    public int videoBitrate;             // Output video bitrate after transcoding (Kbps)
    public int videoFramerate;           // Output video frame rate after transcoding (fps)
    public int videoGOP;                 // Keyframe interval (seconds)
    public int backgroundColor;          // Mixed screen background color
    public String backgroundImage;       // Mixed screen background image
    public int audioSampleRate;          // Output audio sample rate after transcoding
    public int audioBitrate;             // Output audio bitrate after transcoding (Kbps)
    public int audioChannels;            // Output audio channel count after transcoding
    public ArrayList<V2TXLiveMixStream> mixStreams; // Sub-screen layout information
    public String outputStreamId;        // Output stream ID for CDN
}
```

## 7. Local Recording Configuration

### V2TXLiveRecordMode - Local Recording Mode
```java
public enum V2TXLiveRecordMode {
    /// Record both audio and video
    V2TXLiveRecordModeBoth,
}
```

### V2TXLiveLocalRecordingParams - Local Recording Parameters
```java
public final static class V2TXLiveLocalRecordingParams {
    public String filePath;              // Recording file path (required)
    public V2TXLiveRecordMode recordMode; // Recording mode
    public int interval;                 // Update interval for recording info (ms)
}
```

## 8. Log Configuration

### V2TXLiveLogLevel - Log Level Enumeration
```java
public static final class V2TXLiveLogLevel {
    public static final int V2TXLiveLogLevelAll = 0;      // Output all log levels
    public static final int V2TXLiveLogLevelDebug = 1;   // Output DEBUG and above
    public static final int V2TXLiveLogLevelInfo = 2;    // Output INFO and above
    public static final int V2TXLiveLogLevelWarning = 3; // Output WARNING and above
    public static final int V2TXLiveLogLevelError = 4;   // Output ERROR and above
    public static final int V2TXLiveLogLevelFatal = 5;   // Output only FATAL
    public static final int V2TXLiveLogLevelNULL = 6;    // Disable all SDK logs
}
```

### V2TXLiveLogConfig - Log Configuration
```java
public final static class V2TXLiveLogConfig {
    public int logLevel;                  // Log level
    public boolean enableObserver;        // Enable log observer callback
    public boolean enableConsole;         // Print logs to console
    public boolean enableLogFile;         // Enable local log files
    public String logPath;                // Local log directory
}
```

## 9. Additional Configurations

### V2TXLiveSocks5ProxyConfig - SOCKS5 Proxy Configuration
```java
public final static class V2TXLiveSocks5ProxyConfig {
    public boolean supportHttps = true;  // Enable HTTPS support
    public boolean supportTcp = true;    // Enable TCP support
    public boolean supportUdp = true;    // Enable UDP support
}
```

### V2TXLiveStreamInfo - Adaptive Stream Switching Info
```java
public final static class V2TXLiveStreamInfo {
    public int width;                    // Video width
    public int height;                   // Video height
    public int bitrate;                  // Bitrate (bps)
    public float framerate;              // Frame rate
    public String url;                   // Stream URL
}
```

This document details all type definitions in `V2TXLiveDef.java` and serves as a comprehensive API reference for developing with Tencent Cloud Live Streaming.