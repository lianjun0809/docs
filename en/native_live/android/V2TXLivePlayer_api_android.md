> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

Tencent Cloud Live Streaming SDK V2TXLivePlayer Playback API Documentation

## Feature Overview

`V2TXLivePlayer` is the primary interface class for the Tencent Cloud Live Streaming (CSS) player. It handles pulling audio and video data from a specified live stream URL, decoding, and rendering the stream for local playback.

**File Path**: `com/tencent/live2/V2TXLivePlayer.java`  
**Platform Support**: Android

## Core Features

### 🎯 Main Capabilities
- ✅ **Multi-Protocol Support**: HTTP-FLV, WebRTC, TRTC, HLS, RTMP
- ✅ **Video Control**: Rotation, fill mode, mirroring
- ✅ **Playback Control**: Play/stop, pause/resume, volume adjustment
- ✅ **Cache Optimization**: Automatic cache strategy adjustment
- ✅ **Seamless Switching**: Seamless multi-resolution stream switching
- ✅ **Custom Processing**: Audio/video data monitoring and custom rendering
- ✅ **Advanced Features**: Snapshot, SEI message, Picture-in-Picture, local recording

### 🔧 Technical Highlights
- **Low Latency**: Optimized caching and adaptive network handling
- **High Compatibility**: Supports multiple video encoding formats and resolutions
- **Easy Integration**: Simple API design with comprehensive callback support
- **High Performance**: Hardware Decoding acceleration and efficient rendering pipeline

### Player Instance Creation
```java
V2TXLivePlayer player = new V2TXLivePlayerImpl(context);
```

## API Details

### 1. Basic Setup Interfaces

#### setObserver() - Set Player Callback
```java
public abstract void setObserver(V2TXLivePlayerObserver observer)
```

**Parameters**:
- `observer`: The callback object for the player. Must implement the `V2TXLivePlayerObserver` interface.

**When to Call**: Set immediately after initializing the player.

**Description**: Assign a callback to monitor player status, playback volume updates, first audio/video frame events, statistics, warnings, and error notifications.

**Example**:
```java
player.setObserver(new V2TXLivePlayerObserver() {
  // ...
});
```

### setRenderView() - Set Video Rendering View
```java
public abstract int setRenderView(TXCloudVideoView view)
public abstract int setRenderView(TextureView view)
public abstract int setRenderView(SurfaceView view)
```

**Parameters**:
- `view`: The video rendering view. Supports TXCloudVideoView, TextureView, and SurfaceView (HDR playback requires SurfaceView).

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**When to Call**: Set the rendering view before starting playback.

**Example**:
```java
player.setRenderView(videoView);
```

### setRenderRotation() - Set Video Rotation Angle
```java
public abstract int setRenderRotation(V2TXLiveRotation rotation)
```

**Parameters**:
- `rotation`: Rotation angle. See `V2TXLiveDef#V2TXLiveRotation`.
  - `V2TXLiveRotation0` [Default]: 0 degrees (no rotation)
  - `V2TXLiveRotation90`: 90 degrees clockwise
  - `V2TXLiveRotation180`: 180 degrees clockwise
  - `V2TXLiveRotation270`: 270 degrees clockwise

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**When to Call**: No restrictions.

**Example**:
```java
// Set video rotation to 0 degrees
player.setRenderRotation(V2TXLiveDef.V2TXLiveRotation.V2TXLiveRotation0);
// Set video rotation to 90 degrees
player.setRenderRotation(V2TXLiveDef.V2TXLiveRotation.V2TXLiveRotation90);
// Set video rotation to 180 degrees
player.setRenderRotation(V2TXLiveDef.V2TXLiveRotation.V2TXLiveRotation180);
// Set video rotation to 270 degrees
player.setRenderRotation(V2TXLiveDef.V2TXLiveRotation.V2TXLiveRotation270);
```

### setRenderFillMode() - Set Video Fill Mode
```java
public abstract int setRenderFillMode(V2TXLiveFillMode mode)
```

**Parameters**:
- `mode`: Fill mode. See `V2TXLiveDef#V2TXLiveFillMode`.
  - `V2TXLiveFillModeFill` [Default]: Fills the screen, no black bars. If the aspect ratio differs, part of the image may be cropped.
  - `V2TXLiveFillModeFit`: Fits the image to the screen, preserves the entire image, but may show black bars if aspect ratios differ.
  - `V2TXLiveFillModeScaleFill`: Stretches the image to fill the screen. Width and height may not scale proportionally.

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**When to Call**: No restrictions.

**Example**:
```java
// Fill image to screen
player.setRenderFillMode(V2TXLiveDef.V2TXLiveFillMode.V2TXLiveFillModeFill);
// Fit image to screen
player.setRenderFillMode(V2TXLiveDef.V2TXLiveFillMode.V2TXLiveFillModeFit);
// Stretch image to fill
player.setRenderFillMode(V2TXLiveDef.V2TXLiveFillMode.V2TXLiveFillModeScaleFill);
```

### setRenderMirrorMode() - Set Video Mirroring Mode
```java
public abstract int setRenderMirrorMode(boolean enable)
```

**Parameters**:
- `enable`: Enable mirroring mode during playback. [Default]: false

**Description**: When enabled, the video is flipped horizontally. You can toggle this effect at any time.

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**When to Call**: No restrictions.

**Example**:
```java
// Enable mirroring mode
player.setRenderMirrorMode(true);
// Disable mirroring mode
player.setRenderMirrorMode(false);
```

### 2. Playback Control Interfaces

### startLivePlay() - Start Audio/Video Playback
```java
public abstract int startLivePlay(String url)
```

**Parameters**:
- `url`: Stream playback URL. Supports HTTP-FLV, WebRTC, TRTC, HLS, RTMP.

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Playback started successfully
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: Invalid URL
- `V2TXLIVE_ERROR_REFUSED`: RTC does not support pushing and pulling the same StreamId on the same device simultaneously
- `V2TXLIVE_ERROR_INVALID_LICENSE`: Invalid Licence, playback failed

**Important Note**:
- Starting from version 10.7, you must set the Licence using `V2TXLivePremier#setLicence` before playback. Otherwise, playback will fail (black screen). Only needs to be set once globally.
- Supports live streaming Licence, short video Licence, and video playback Licence.

**When to Call**: No restrictions.

**Example**:
```java
int result = player.startLivePlayer("http://example.com/live/stream_1080p.flv");
if (result == V2TXLiveCode.V2TXLIVE_OK) {
    Log.i(TAG, "Playback started successfully");
} else if (result == V2TXLiveCode.V2TXLIVE_ERROR_INVALID_PARAMETER) {
    Log.w(TAG, "Invalid playback address");
} else if (result == V2TXLiveCode.V2TXLIVE_ERROR_REFUSED) {
    Log.w(TAG, "Call refused");
} else if (result == V2TXLiveCode.V2TXLIVE_ERROR_INVALID_LICENSE) {
    Log.w(TAG, "Invalid Licence, please check your Licence");
}
```

### stopPlay() - Stop Audio/Video Playback
```java
public abstract int stopPlay()
```

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**When to Call**: After playback has started.

**Example**:
```java
player.stopPlay();
```

### isPlaying() - Check Playback Status
```java
public abstract int isPlaying()
```

**Return Value**:
- `1`: Currently playing
- `0`: Playback stopped

**When to Call**: No restrictions.

**Example**:
```java
int isPlaying = player.isPlaying();
if (isPlaying == 1) {
    Log.i(TAG, "Currently playing");
} else {
    Log.i(TAG, "Playback stopped");
}
```

### 3. Audio/Video Control Interfaces

### pauseAudio() - Pause Audio Playback
```java
public abstract int pauseAudio()
```

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**When to Call**: No restrictions. If called before playback starts, only video will play (no audio).

**Example**:
```java
player.pauseAudio();
```

### resumeAudio() - Resume Audio Playback
```java
public abstract int resumeAudio()
```

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**When to Call**: No restrictions.

**Example**:
```java
player.resumeAudio();
```

### pauseVideo() - Pause Video Playback
```java
public abstract int pauseVideo()
```

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**When to Call**: No restrictions. If called before playback starts, only audio will play (no video).

**Example**:
```java
player.pauseVideo();
```

### resumeVideo() - Resume Video Playback
```java
public abstract int resumeVideo()
```

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**When to Call**: No restrictions.

**Example**:
```java
player.resumeVideo();
```

### setPlayoutVolume() - Adjust Playback Volume
```java
public abstract int setPlayoutVolume(int volume)
```

**Parameters**:
- `volume`: Volume level, range 0–100. [Default]: 100

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**When to Call**: No restrictions.

**Example**:
```java
player.setPlayoutVolume(50);
```

### 4. Advanced Feature Interfaces

### setCacheParams() - Configure Cache Time Range
```java
public abstract int setCacheParams(float minTime, float maxTime)
```

**Parameters**:
- `minTime`: Minimum cache time for automatic adjustment. Must be > 0. [Default]: 1
- `maxTime`: Maximum cache time for automatic adjustment. Must be > 0. [Default]: 5

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: minTime and maxTime must be greater than 0

**Optimization Tips**:
- Stable network: Use a smaller cache (1–3 seconds)
- Unstable network: Use a larger cache (3–5 seconds)
- If unsure, use default values

**When to Call**: No restrictions.

**Example**:
```java
player.setCacheParams(1, 5);
```

### switchStream() - Switch Stream Resolution Seamlessly (FLV, LEB)
```java
public abstract int switchStream(String newUrl)
```

**Parameters**:
- `newUrl`: URL for the new stream resolution

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**When to Call**: After playback has started.

**Example**:
```java
player.startLivePlayer("http://example.com/live/stream_1080p.flv");

player.setObserver(new V2TXLivePlayerObserver() {
    @Override
    public void onStreamSwitched(V2TXLivePlayer player, String url, int code) {
        if (code == 0) {
            Log.i(TAG, "Switch successful");
        } else if (code == -1) {
            Log.i(TAG, "Switch timeout");
        } else if (code == -2) {
            Log.i(TAG, "Switch failed, server error");
        } else if (code == -3) {
            Log.i(TAG, "Switch failed, client error");
        }
    }
});
player.switchStream("http://example.com/live/stream_720p.flv");
```

### getStreamList() - Retrieve Stream Information (HLS Supported)
```java
public abstract ArrayList<V2TXLiveDef.V2TXLiveStreamInfo> getStreamList()
```

**Return Value**: Array of stream information, including available resolutions

**When to Call**: After playback has started.

**Example**:
```java
player.startLivePlayer("http://example.com/live/stream_1080p.m3u8");

ArrayList<V2TXLiveStreamInfo> streamList = player.getStreamList();
```

### enableVolumeEvaluation() - Enable Playback Volume Level Callback
```java
public abstract int enableVolumeEvaluation(int intervalMs)
```

**Parameters**:
- `intervalMs`: Callback interval for `onPlayoutVolumeUpdate` (ms). Minimum: 100ms. If ≤ 0, disables callback. Recommended: 300ms. [Default]: 0 (disabled)

**Description**: When enabled, the SDK reports playback volume levels via the `V2TXLivePlayerObserver` callback.

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**When to Call**: No restrictions.

**Example**:
```java
player.setObserver(new V2TXLivePlayerObserver() {
    @Override
    public void onPlayoutVolumeUpdate(V2TXLivePlayer player, int volume) {
        // Audio playback volume callback
        Log.i(TAG, "Audio playback volume, volume: " + volume);
    }
});
player.enableVolumeEvaluation(300);
```

### snapshot() - Capture Video Frame
```java
public abstract int snapshot()
```

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success
- `V2TXLIVE_ERROR_REFUSED`: Snapshot not allowed when player is stopped

**When to Call**: After playback has started.

**Example**:
```java
player.setObserver(new V2TXLivePlayerObserver() {
    @Override
    public void onSnapshotComplete(V2TXLivePlayer player, Bitmap image) {
        // Handle snapshot result
    }
});
player.snapshot();
```

### enableObserveVideoFrame() - Enable Custom Video Rendering
```java
public abstract int enableObserveVideoFrame(boolean enable, V2TXLivePixelFormat pixelFormat, V2TXLiveBufferType bufferType)
```

**Parameters**:
- `enable`: Enable custom rendering. [Default]: false
- `pixelFormat`: Pixel format for custom rendering callback. See `V2TXLiveDef#V2TXLivePixelFormat`.
- `bufferType`: Video data format for custom rendering callback. See `V2TXLiveDef#V2TXLiveBufferType`.

**Description**:
- When enabled, the SDK stops rendering video frames internally. You can access video frames via `V2TXLivePlayerObserver` for custom rendering.
- Supported combinations:
  - V2TXLiveDef.V2TXLivePixelFormat.V2TXLivePixelFormatTexture2D + V2TXLiveDef.V2TXLiveBufferType.V2TXLiveBufferTypeTexture (recommended)
  - V2TXLiveDef.V2TXLivePixelFormat.V2TXLivePixelFormatI420 + V2TXLiveDef.V2TXLiveBufferType.V2TXLiveBufferTypeByteArray
  - V2TXLiveDef.V2TXLivePixelFormat.V2TXLivePixelFormatI420 + V2TXLiveDef.V2TXLiveBufferType.V2TXLiveBufferTypeByteBuffer

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success
- `V2TXLIVE_ERROR_NOT_SUPPORTED`: Unsupported pixel or data format

**When to Call**: Before starting playback.

**Example**:
```java
// Enable custom rendering
player.enableObserveVideoFrame(true, V2TXLiveDef.V2TXLivePixelFormat.V2TXLivePixelFormatTexture2D, V2TXLiveDef.V2TXLiveBufferType.V2TXLiveBufferTypeTexture);
player.setObserver(new V2TXLivePlayerObserver() {
    @Override
    public void onRenderVideoFrame(V2TXLivePlayer player, V2TXLiveVideoFrame videoFrame) {
        // Custom rendering logic
    }
});
```

### enableObserveAudioFrame() - Enable Audio Data Callback
```java
public abstract int enableObserveAudioFrame(boolean enable)
```

**Parameters**:
- `enable`: Enable audio data callback. [Default]: false

**Description**: When enabled, you can access audio data via `V2TXLivePlayerObserver` for custom processing.

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**When to Call**: Before starting playback.

**Example**:
```java
// Enable audio data monitoring
player.enableObserveAudioFrame(true);
player.setObserver(new V2TXLivePlayerObserver() {
    @Override
    public void onPlayoutAudioFrame(V2TXLivePlayer player, V2TXLiveAudioFrame audioFrame) {
        // Handle audio frame
    }
});
```

### enableReceiveSeiMessage() - Enable SEI Message Reception
```java
public abstract int enableReceiveSeiMessage(boolean enable, int payloadType)
```

**Parameters**:
- `enable`: true to enable, false to disable SEI message reception. [Default]: false
- `payloadType`: Payload type for SEI messages. Supports 5, 242, 243. Must match sender's payloadType.

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**When to Call**: Before starting playback.

**Example**:
```java
player.enableReceiveSeiMessage(true, 5);
player.enableReceiveSeiMessage(true, 242);
player.enableReceiveSeiMessage(true, 243);
player.setObserver(new V2TXLivePlayerObserver() {
    @Override
    public void onReceiveSeiMessage(V2TXLivePlayer player, int payloadType, byte[] data) {
        // Handle SEI message
    }
});
```

### startLocalRecording() - Start Local Recording
```java
public abstract int startLocalRecording(V2TXLiveLocalRecordingParams params)
```

**Parameters**:
- `params`: See `V2TXLiveDef.java` for details on `V2TXLiveLocalRecordingParams`

**Important Notes**:
- Recording can only start after stream pulling is enabled. Starting recording before pulling a stream is invalid.
- Do not switch between software and hardware decoding during recording; this may cause abnormal video output.

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: Invalid parameters (e.g., empty filePath)
- `V2TXLIVE_ERROR_REFUSED`: API refused, stream not started

**When to Call**: After playback has started.

**Example**:
```java
player.setObserver(new V2TXLivePlayerObserver() {
    @Override
    public void onLocalRecordBegin(V2TXLivePlayer player, int code, String storagePath) {
        Log.i(TAG, "Recording started");
    }

    @Override
    public void onLocalRecording(V2TXLivePlayer player, long durationMs, String storagePath) {
        Log.i(TAG, "Recording..., durationMs: " + durationMs);
    }

    @Override
    public void onLocalRecordComplete(V2TXLivePlayer player, int code, String storagePath) {
        Log.i(TAG, "Recording completed");
    }
});

V2TXLiveDef.V2TXLiveLocalRecordingParams params = new V2TXLiveDef.V2TXLiveLocalRecordingParams();
params.filePath = "filepath";
params.interval = 2000;
int code = player.startLocalRecording(params);
if (code == V2TXLIVE_OK) {
    Log.i(TAG, "Recording started successfully");
} else if (code == V2TXLIVE_ERROR_INVALID_PARAMETER) {
    Log.i(TAG, "Invalid recording parameters");
} else if (code == V2TXLIVE_ERROR_REFUSED) {
    Log.i(TAG, "Recording call refused");
}
```

### stopLocalRecording() - Stop Local Recording
```java
public abstract void stopLocalRecording()
```

**Description**: If the stream stops while recording is in progress, the SDK will automatically end the recording.

**When to Call**: After playback has started and recording is active.

**Example**:
```java
player.stopLocalRecording();
```

### showDebugView() - Show/Hide Debug Overlay
```java
public abstract void showDebugView(boolean isShow)
```

**Parameters**:
- `isShow`: true to show, false to hide. [Default]: false

**When to Call**: No restrictions.

**Example**:
```java
player.showDebugView(true);
```

### setProperty() - Advanced API Access
```java
public abstract int setProperty(String key, Object value)
```

**Parameters**:
- `key`: Advanced API key
- `value`: Parameter for the specified advanced API

**Description**: Use this method to access advanced features. For special requirements, contact your business or solution architect.

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: Key must not be null

#### enablePictureInPicture() - Enable Picture-in-Picture Mode (iOS Only)
```dart
Future<V2TXLiveCode> enablePictureInPicture(bool enable)
```
**Parameters**: 
- `enable`: Enable Picture-in-Picture mode. Default: false

#### getTextureId() - Retrieve Texture ID
```dart
Future<int> getTextureId(int width, int height)
```
**Parameters**: 
- `width`: Texture width
- `height`: Texture height

## Code Examples

```java
// Create player instance
V2TXLivePlayer player = V2TXLivePlayerImpl(context);

// Set callback
player.setObserver(new V2TXLivePlayerObserver() {
    @Override
    public void onConnected() {
        // Connection successful callback
    }
    
    @Override
    public void onVideoResolutionChanged(int width, int height) {
        // Video resolution changed callback
    }
});

// Set rendering view
player.setRenderView(videoView);

// Start playback
int result = player.startLivePlay("rtmp://example.com/live/stream");
if (result == V2TXLIVE_OK) {
    // Playback successful
}

// Pause video
player.pauseVideo();

// Resume video
player.resumeVideo();

// Stop playback
player.stopPlay();
```

## Notes

1. **Licence Requirement**: Starting from version 10.7, you must set a valid Licence for playback.
2. **Permission Requirement**: Requires network and audio playback permissions.