> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

# Tencent Cloud Live Streaming SDK V2TXLiveDef Type Definition Documentation

## Feature Overview

`V2TXLiveDef.h` is the primary type definition file for the Tencent Cloud Live Streaming SDK on iOS and macOS. It provides all enumerations, constants, and data structures required for live stream publishing and playback.

**Platform Support**: iOS, macOS  
**Type Coverage**: Includes video, audio, statistics, configuration, and more

## 📋 Table of Contents

### 1. [Supported Protocols](#supported-protocols)
### 2. [Video Types](#video-types)
### 3. [Audio Types](#audio-types)
### 4. [Statistics Data](#statistics-data)
### 5. [Connection Status](#connection-status)
### 6. [Cloud Stream Mixing Configuration](#cloud-stream-mixing-configuration)
### 7. [Local Recording Configuration](#local-recording-configuration)
### 8. [Log Configuration](#log-configuration)
### 9. [Other Configuration](#other-configuration)

## 1. Supported Protocols

### V2TXLiveMode - Supported Protocols for Stream Publishing
```objc
typedef NS_ENUM(NSUInteger, V2TXLiveMode) {
    /// Supported protocol: RTMP
    V2TXLiveMode_RTMP,
    
    /// Supported protocol: RTC
    V2TXLiveMode_RTC
};
```

**Protocol Details**:
- RTMP: Standard protocol for live streaming
- RTC: Real-Time Communication (TRTC) protocol

## 2. Video Types

### V2TXLiveVideoResolution - Video Resolution Enumeration
```objc
typedef NS_ENUM(NSInteger, V2TXLiveVideoResolution) {
    /// 160x160, bitrate: 100Kbps–150Kbps, frame rate: 15fps
    V2TXLiveVideoResolution160x160,
    
    /// 270x270, bitrate: 200Kbps–300Kbps, frame rate: 15fps
    V2TXLiveVideoResolution270x270,

    /// 480x480, bitrate: 350Kbps–525Kbps, frame rate: 15fps
    V2TXLiveVideoResolution480x480,

    /// 320x240, bitrate: 250Kbps–375Kbps, frame rate: 15fps
    V2TXLiveVideoResolution320x240,

    /// 480x360, bitrate: 400Kbps–600Kbps, frame rate: 15fps
    V2TXLiveVideoResolution480x360,

    /// 640x480, bitrate: 600Kbps–900Kbps, frame rate: 15fps
    V2TXLiveVideoResolution640x480,

    /// 320x180, bitrate: 250Kbps–400Kbps, frame rate: 15fps
    V2TXLiveVideoResolution320x180,

    /// 480x270, bitrate: 350Kbps–550Kbps, frame rate: 15fps
    V2TXLiveVideoResolution480x270,

    /// 640x360, bitrate: 500Kbps–900Kbps, frame rate: 15fps
    V2TXLiveVideoResolution640x360,

    /// 960x540, bitrate: 800Kbps–1500Kbps, frame rate: 15fps
    V2TXLiveVideoResolution960x540,

    /// 1280x720, bitrate: 1000Kbps–1800Kbps, frame rate: 15fps
    V2TXLiveVideoResolution1280x720,

    /// 1920x1080, bitrate: 2500Kbps–3000Kbps, frame rate: 15fps
    V2TXLiveVideoResolution1920x1080
};
```

### V2TXLiveVideoResolutionMode - Video Resolution Mode
```objc
typedef NS_ENUM(NSInteger, V2TXLiveVideoResolutionMode) {
    /// Landscape mode
    V2TXLiveVideoResolutionModeLandscape,
    
    /// Portrait mode
    V2TXLiveVideoResolutionModePortrait
};
```

**Resolution Options**:
- Supports a range of resolutions from 160×160 up to 1920×1080
- Landscape and portrait orientation available

### V2TXLiveMirrorType - Camera Mirroring Mode
```objc
typedef NS_ENUM(NSInteger, V2TXLiveMirrorType) {
    /// System default: front camera mirrored, rear camera not mirrored
    V2TXLiveMirrorTypeAuto,
    
    /// Mirror mode enabled for both front and rear cameras
    V2TXLiveMirrorTypeEnable,
    
    /// Mirror mode disabled for both front and rear cameras
    V2TXLiveMirrorTypeDisable
};
```

### V2TXLiveFillMode - Video Fill Mode
```objc
typedef NS_ENUM(NSInteger, V2TXLiveFillMode) {
    /// Fill screen by cropping excess, may lose content
    V2TXLiveFillModeFill,
    
    /// Fit long edge to screen, black bars on short edge, content remains intact
    V2TXLiveFillModeFit,
    
    /// Stretch to fill screen, aspect ratio may not be preserved
    V2TXLiveFillModeScaleFill
};
```

### V2TXLiveRotation - Video Rotation Angle
```objc
typedef NS_ENUM(NSInteger, V2TXLiveRotation) {
    /// No rotation
    V2TXLiveRotation0,
    
    /// 90° clockwise
    V2TXLiveRotation90,
    
    /// 180° clockwise
    V2TXLiveRotation180,
    
    /// 270° clockwise
    V2TXLiveRotation270
};
```

### V2TXLiveVideoEncoderParam - Video Encoder Parameter Configuration
```objc
@interface V2TXLiveVideoEncoderParam : NSObject

@property(nonatomic, assign) V2TXLiveVideoResolution videoResolution;      // Video resolution
@property(nonatomic, assign) V2TXLiveVideoResolutionMode videoResolutionMode; // Resolution mode
@property(nonatomic, assign) int videoFps;                                // Capture Frame Rate (fps)
@property(nonatomic, assign) int videoBitrate;                             // Target video bitrate (kbps)
@property(nonatomic, assign) int minVideoBitrate;                          // Minimum video bitrate (kbps)

- (instancetype)initWith:(V2TXLiveVideoResolution)resolution;          // Initialization method

@end
```

**Recommended Settings**:
- **Frame Rate**: Set to 15fps or 20fps. Frame rates below 5fps cause noticeable Playback Stuttering; rates above 20fps may waste bandwidth.
- **Adaptive Bitrate**: Specify both videoBitrate and minVideoBitrate to define the bitrate adjustment range.

### V2TXLivePixelFormat - Video Frame Pixel Format
```objc
typedef NS_ENUM(NSInteger, V2TXLivePixelFormat) {
    /// Unknown pixel format
    V2TXLivePixelFormatUnknown,
    
    /// I420 (YUV420P)
    V2TXLivePixelFormatI420,
    
    /// NV12
    V2TXLivePixelFormatNV12,
    
    /// BGRA32
    V2TXLivePixelFormatBGRA32,
    
    /// OpenGL 2D texture
    V2TXLivePixelFormatTexture2D
};
```

### V2TXLiveBufferType - Video Data Buffer Type
```objc
typedef NS_ENUM(NSInteger, V2TXLiveBufferType) {
    /// Unknown buffer type
    V2TXLiveBufferTypeUnknown,
    
    /// PixelBuffer (native iOS video format)
    V2TXLiveBufferTypePixelBuffer,
    
    /// NSData (used for I420 and other buffer types)
    V2TXLiveBufferTypeNSData,
    
    /// OpenGL texture (highest performance, minimal quality loss)
    V2TXLiveBufferTypeTexture
};
```

### V2TXLiveVideoFrame - Video Frame Data Structure
```objc
@interface V2TXLiveVideoFrame : NSObject

@property(nonatomic, assign) V2TXLivePixelFormat pixelFormat;  // Pixel format
@property(nonatomic, assign) V2TXLiveBufferType bufferType;   // Buffer type
@property(nonatomic, strong) NSData *data;                    // Video data
@property(nonatomic, assign) CVPixelBufferRef pixelBuffer;    // PixelBuffer data
@property(nonatomic, assign) NSUInteger width;                // Video width
@property(nonatomic, assign) NSUInteger height;               // Video height
@property(nonatomic, assign) V2TXLiveRotation rotation;       // Rotation angle
@property(nonatomic, assign) GLuint textureId;                // Texture ID

@end
```

### Picture-in-Picture State

### V2TXLivePictureInPictureState - Picture-in-Picture State Enumeration
```objc
typedef NS_ENUM(NSInteger, V2TXLivePictureInPictureState) {
    /// Undefined state
    V2TXLivePictureInPictureStateUndefined,
    
    /// Error occurred
    V2TXLivePictureInPictureStateOccurError,
    
    /// Will start
    V2TXLivePictureInPictureStateWillStart,
    
    /// Started
    V2TXLivePictureInPictureStateDidStart,
    
    /// Will stop
    V2TXLivePictureInPictureStateWillStop,
    
    /// Stopped
    V2TXLivePictureInPictureStateDidStop,
    
    /// Restore UI from picture-in-picture
    V2TXLivePictureInPictureStateRestoreUI
};
```

## 3. Audio Types

### V2TXLiveAudioQuality - Audio Quality Options
```objc
typedef NS_ENUM(NSInteger, V2TXLiveAudioQuality) {
    /// Speech: 16k sample rate, mono, 16kbps; suitable for voice calls
    V2TXLiveAudioQualitySpeech,
    
    /// Default: 48k sample rate, mono, 50kbps; SDK default
    V2TXLiveAudioQualityDefault,
    
    /// Music: 48k sample rate, stereo, full band, 128kbps; suitable for high-fidelity music
    V2TXLiveAudioQualityMusic
};
```

### V2TXLiveAudioFrame - Audio Frame Data Structure
```objc
@interface V2TXLiveAudioFrame : NSObject

@property(nonatomic, strong) NSData *data;        // Audio data
@property(nonatomic, assign) int sampleRate;      // Sample rate (default: 48000Hz)
@property(nonatomic, assign) int channel;         // Audio Channel count (default: 1, mono)
@property(nonatomic, assign) uint64_t timestamp;  // Timestamp (ms)

@end
```

### V2TXLiveAudioFrameOperationMode - Audio Callback Data Mode
```objc
typedef NS_ENUM(NSInteger, V2TXLiveAudioFrameOperationMode) {
    /// Read/Write: get and modify callback audio data (default)
    V2TXLiveAudioFrameOperationModeReadWrite,
    
    /// Read-only: only get audio data from callback
    V2TXLiveAudioFrameOperationModeReadOnly
};
```

### V2TXLiveAudioFrameObserverFormat - Audio Frame Callback Format
```objc
@interface V2TXLiveAudioFrameObserverFormat : NSObject

@property(nonatomic, assign) int sampleRate;                      // Sample rate (default: 48000Hz)
@property(nonatomic, assign) int channel;                        // Audio Channel count (default: 1)
@property(nonatomic, assign) int samplesPerCall;                 // Samples per callback
@property(nonatomic, assign) V2TXLiveAudioFrameOperationMode mode; // Callback data mode

@end
```

**Parameter Notes**:
- **samplesPerCall**: Must be an integer multiple of sampleRate/100

## 4. Statistics Data

### V2TXLivePusherStatistics - Stream Publisher Statistics
```objc
@interface V2TXLivePusherStatistics : NSObject

@property(nonatomic, assign) NSUInteger appCpu;              // App CPU usage (%)
@property(nonatomic, assign) NSUInteger systemCpu;           // System CPU usage (%)
@property(nonatomic, assign) NSUInteger width;              // Video width
@property(nonatomic, assign) NSUInteger height;             // Video height
@property(nonatomic, assign) NSUInteger fps;                // Frame rate (fps)
@property(nonatomic, assign) NSUInteger videoBitrate;       // Video bitrate (Kbps)
@property(nonatomic, assign) NSUInteger audioBitrate;       // Audio bitrate (Kbps)
@property(nonatomic, assign) NSUInteger rtt;                // Round-Trip Time (RTT) (ms)
@property(nonatomic, assign) NSUInteger netSpeed;           // Upload speed (kbps)

@end
```

### V2TXLivePlayerStatistics - Player Statistics
```objc
@interface V2TXLivePlayerStatistics : NSObject

@property(nonatomic, assign) NSUInteger appCpu;              // App CPU usage (%)
@property(nonatomic, assign) NSUInteger systemCpu;           // System CPU usage (%)
@property(nonatomic, assign) NSUInteger width;              // Video width
@property(nonatomic, assign) NSUInteger height;             // Video height
@property(nonatomic, assign) NSUInteger fps;                // Frame rate (fps)
@property(nonatomic, assign) NSUInteger videoBitrate;       // Video bitrate (Kbps)
@property(nonatomic, assign) NSUInteger audioBitrate;       // Audio bitrate (Kbps)
@property(nonatomic, assign) NSUInteger audioPacketLoss;    // Audio packet loss rate (%)
@property(nonatomic, assign) NSUInteger videoPacketLoss;    // Video Packet Loss Rate (%)
@property(nonatomic, assign) NSUInteger jitterBufferDelay;   // Playback delay (ms)
@property(nonatomic, assign) NSUInteger audioTotalBlockTime; // Total audio Playback Stuttering duration (ms)
@property(nonatomic, assign) NSUInteger audioBlockRate;      // Audio Playback Stuttering rate (%)
@property(nonatomic, assign) NSUInteger videoTotalBlockTime; // Total video Playback Stuttering duration (ms)
@property(nonatomic, assign) NSUInteger videoBlockRate;      // Video Playback Stuttering rate (%)
@property(nonatomic, assign) NSUInteger rtt;                // Round-Trip Time (RTT) (ms)
@property(nonatomic, assign) NSUInteger netSpeed;           // Download speed (kbps)

@end
```

## 5. Connection Status

### V2TXLivePushStatus - Stream Publishing Connection Status
```objc
typedef NS_ENUM(NSInteger, V2TXLivePushStatus) {
    /// Disconnected from server
    V2TXLivePushStatusDisconnected,
    
    /// Connecting to server
    V2TXLivePushStatusConnecting,
    
    /// Connected to server
    V2TXLivePushStatusConnectSuccess,
    
    /// Reconnecting to server
    V2TXLivePushStatusReconnecting
};
```

### V2TXAudioRoute - Audio Output Mode
```objc
typedef NS_ENUM(NSInteger, V2TXAudioRoute) {
    /// Play via the speaker (device speaker)
    V2TXAudioRouteSpeakerphone,
    
    /// Play via the receiver (device earpiece)
    V2TXAudioRouteEarpiece
};
```

## 6. Cloud Stream Mixing Configuration

### V2TXLiveMixInputType - Stream Mixing Input Type
```objc
typedef NS_ENUM(NSInteger, V2TXLiveMixInputType) {
    /// Mix audio and video
    V2TXLiveMixInputTypeAudioVideo,
    
    /// Mix video only
    V2TXLiveMixInputTypePureVideo,
    
    /// Mix audio only
    V2TXLiveMixInputTypePureAudio
};
```

### V2TXLiveMixStream - Cloud Stream Mixing Sub-Screen Layout
```objc
@interface V2TXLiveMixStream : NSObject

@property(nonatomic, copy) NSString *userId;          // userId participating in Cloud stream mixing
@property(nonatomic, copy) NSString *streamId;        // streamId for publishing
@property(nonatomic, assign) NSInteger x;             // Layer X position (pixels)
@property(nonatomic, assign) NSInteger y;             // Layer Y position (pixels)
@property(nonatomic, assign) NSInteger width;         // Layer width (pixels)
@property(nonatomic, assign) NSInteger height;        // Layer height (pixels)
@property(nonatomic, assign) NSUInteger zOrder;       // Layer z-order (1–15, must be unique)
@property(nonatomic, assign) V2TXLiveMixInputType inputType; // Stream input type

@end
```

### V2TXLiveTranscodingConfig - Cloud Stream Mixing MixTranscoding Configuration
```objc
@interface V2TXLiveTranscodingConfig : NSObject

@property(nonatomic, assign) NSUInteger videoWidth;      // Output video width
@property(nonatomic, assign) NSUInteger videoHeight;     // Output video height
@property(nonatomic, assign) NSUInteger videoBitrate;    // Output video bitrate (kbps)
@property(nonatomic, assign) NSUInteger videoFramerate;  // Output video frame rate (FPS)
@property(nonatomic, assign) NSUInteger videoGOP;        // Keyframe interval (seconds)
@property(nonatomic, assign) NSUInteger backgroundColor; // Background color
@property(nonatomic, copy) NSString *backgroundImage;    // Background image
@property(nonatomic, assign) NSUInteger audioSampleRate; // Output audio sample rate
@property(nonatomic, assign) NSUInteger audioBitrate;    // Output audio bitrate (kbps)
@property(nonatomic, assign) NSUInteger audioChannels;   // Output audio channel count
@property(nonatomic, copy) NSArray<V2TXLiveMixStream *> *mixStreams; // Sub-screen layout info
@property(nonatomic, copy) NSString *outputStreamId;     // Output stream ID for CDN

@end
```

## 7. Local Recording Configuration

### V2TXLiveRecordMode - Local Recording Mode
```objc
typedef NS_ENUM(NSUInteger, V2TXLiveRecordMode) {
    /// Record both audio and video
    V2TXLiveRecordModeBoth
};
```

### V2TXLiveLocalRecordingParams - Local Recording Parameters
```objc
@interface V2TXLiveLocalRecordingParams : NSObject

@property(nonatomic, copy) NSString *filePath;      // Path for recording file (required, must include filename and extension)
@property(nonatomic, assign) V2TXLiveRecordMode recordMode; // Recording mode
@property(nonatomic, assign) int interval;          // Recording info update interval (ms)

@end
```

**Parameter Notes**:
- **filePath**: Must include filename and extension (currently supports MP4 only)
- **interval**: Valid range is 1000–10000ms; set to -1 to disable recording info callback

## 8. Log Configuration

### V2TXLiveLogLevel - Log Level
```objc
typedef NS_ENUM(NSInteger, V2TXLiveLogLevel) {
    V2TXLiveLogLevelAll,        // Output all levels
    V2TXLiveLogLevelDebug,      // Output DEBUG and above
    V2TXLiveLogLevelInfo,       // Output INFO and above
    V2TXLiveLogLevelWarning,    // Output WARNING and above
    V2TXLiveLogLevelError,      // Output ERROR and above
    V2TXLiveLogLevelFatal,      // Output FATAL only
    V2TXLiveLogLevelNULL        // No log output
};
```

### V2TXLiveLogConfig - Log Configuration
```objc
@interface V2TXLiveLogConfig : NSObject

@property(nonatomic, assign) V2TXLiveLogLevel logLevel;      // Log level
@property(nonatomic, assign) BOOL enableObserver;            // Receive log info via Observer
@property(nonatomic, assign) BOOL enableConsole;             // Print log info to console
@property(nonatomic, assign) BOOL enableLogFile;             // Enable local log file
@property(nonatomic, copy) NSString *logPath;                // Log storage directory

@end
```

**Default Storage Path**: On iOS/macOS, logs are stored in the Documents/log directory by default.

**Field Descriptions**:
- **logLevel**: Controls the verbosity of SDK log output
- **enableObserver**: Receive log info via Observer for custom handling
- **enableConsole**: Print log info to the editor console for debugging
- **enableLogFile**: Enable local log file for troubleshooting
- **logPath**: Directory for storing logs; uses default path if not specified

## 9. Other Configuration

### V2TXLiveSocks5ProxyConfig - SOCKS5 Proxy Configuration
```objc
@interface V2TXLiveSocks5ProxyConfig : NSObject

@property(nonatomic, assign) BOOL supportHttps;    // Enable HTTPS support
@property(nonatomic, assign) BOOL supportTcp;      // Enable TCP support
@property(nonatomic, assign) BOOL supportUdp;      // Enable UDP support

@end
```

### V2TXLiveStreamInfo - Adaptive Bitrate Stream Info
```objc
@interface V2TXLiveStreamInfo : NSObject

@property(nonatomic, assign) int width;             // Video width
@property(nonatomic, assign) int height;            // Video height
@property(nonatomic, assign) int bitrate;           // Bitrate (bps)
@property(nonatomic, assign) float framerate;       // Frame rate
@property(nonatomic, copy) NSString *url;           // Stream URL

@end
```
