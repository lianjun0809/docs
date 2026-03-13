> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

# Tencent Cloud Live Streaming SDK V2TXLivePlayer Playback API Documentation

## Feature Overview

`V2TXLivePlayer` is the primary interface for the Tencent Cloud Live Streaming (CSS) player. It handles pulling audio and video streams from a specified live stream URL, performs decoding, and renders playback on the local device.

**File Path**: `v2_tx_live_player.dart`  
**Platform Support**: Flutter

## Core Features

### 🎯 Main Capabilities
- ✅ **Multi-Protocol Support**: HTTP-FLV, WebRTC, TRTC, HLS, RTMP
- ✅ **Video Controls**: Rotation, Fill Mode, Mirroring
- ✅ **Playback Controls**: Play/Stop, Pause/Resume, Volume Adjustment
- ✅ **Cache Optimization**: Automatic cache strategy adjustment
- ✅ **Seamless Switching**: Switch between streams of different resolutions without interruption
- ✅ **Custom Processing**: Monitor audio/video data and implement custom rendering
- ✅ **Advanced Features**: Snapshot, SEI message handling, Picture-in-picture, Local recording

### 🔧 Technical Highlights
- **Low Latency**: Optimized cache management and adaptive networking
- **High Compatibility**: Supports a wide range of video encoding formats and resolutions
- **Easy Integration**: Simple API design with comprehensive callback support
- **High Performance**: Hardware Decoding acceleration and efficient rendering pipeline

### Create Player Instance
```dart
V2TXLivePlayer player = await V2TXLivePlayer.create();
```

## API Details

### Basic Setup APIs

#### Add Listener
```dart
void addListener(V2TXLivePlayerObserver observer)
```

**Parameters**:
- `observer`: Callback target, must implement the `V2TXLivePlayerObserver` interface

**When to Use**: Set immediately after initializing the player

**Description**: Register callbacks to monitor player state, playback volume, first frame events for audio/video, statistics, warnings, and errors.

**Example**:
```dart
player.addListener(V2TXLivePlayerObserver(
  onConnected: (player) {
    print('Player connected');
  },
  onVideoPlaying: (player, isFirstPlay) {
    print('Video started playing');
  },
));
```

#### Set Render View
```dart
Future<V2TXLiveCode> setRenderViewID(int viewID)
```

**Parameters**:
- `viewID`: ID of the rendering view

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**When to Use**: Set before starting playback

**Example**:
```dart
await player.setRenderViewID(viewId);
```

#### Set Render Rotation
```dart
Future<V2TXLiveCode> setRenderRotation(V2TXLiveRotation rotation)
```

**Parameters**:
- `rotation`: Rotation angle (`V2TXLiveRotation`)
  - `v2TXLiveRotation0` [Default]: 0°, no rotation
  - `v2TXLiveRotation90`: 90° clockwise
  - `v2TXLiveRotation180`: 180° clockwise
  - `v2TXLiveRotation270`: 270° clockwise

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**When to Use**: Any time

**Example**:
```dart
await player.setRenderRotation(V2TXLiveRotation.v2TXLiveRotation0);
await player.setRenderRotation(V2TXLiveRotation.v2TXLiveRotation90);
await player.setRenderRotation(V2TXLiveRotation.v2TXLiveRotation180);
await player.setRenderRotation(V2TXLiveRotation.v2TXLiveRotation270);
```

#### Set Render Fill Mode
```dart
Future<V2TXLiveCode> setRenderFillMode(V2TXLiveFillMode mode)
```

**Parameters**:
- `mode`: Fill mode (`V2TXLiveFillMode`)
  - `v2TXLiveFillModeFill` [Default]: Fills the screen, crops if aspect ratio differs
  - `v2TXLiveFillModeFit`: Fits the entire image, may show black borders
  - `v2TXLiveFillModeScaleFill`: Stretches image to fill screen, may distort aspect ratio

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**When to Use**: Any time

**Example**:
```dart
await player.setRenderFillMode(V2TXLiveFillMode.v2TXLiveFillModeFill);
await player.setRenderFillMode(V2TXLiveFillMode.v2TXLiveFillModeFit);
await player.setRenderFillMode(V2TXLiveFillMode.v2TXLiveFillModeScaleFill);
```

### Playback Control APIs

#### Start Live Playback
```dart
Future<V2TXLiveCode> startLivePlay(String url)
```

**Parameters**:
- `url`: Stream playback URL (supports HTTP-FLV, WebRTC, TRTC, HLS, RTMP)

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success, starts connecting and playback
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: Invalid URL
- `V2TXLIVE_ERROR_REFUSED`: RTC does not support pushing and pulling the same StreamId on the same device simultaneously
- `V2TXLIVE_ERROR_INVALID_LICENSE`: Invalid license, playback failed

**Important**:
- From version 10.7, you must set the License using `V2TXLivePremier.setLicence` before playback. Otherwise, playback will fail (black screen). Only set once globally.
- Supports Live Streaming License, Short Video License, and Video Playback License.

**When to Use**: Any time

**Example**:
```dart
V2TXLiveCode result = await player.startLivePlay("http://example.com/live/stream_1080p.flv");
if (result == V2TXLiveCode.V2TXLIVE_OK) {
    print("Playback started successfully");
} else if (result == V2TXLiveCode.V2TXLIVE_ERROR_INVALID_PARAMETER) {
    print("Invalid playback URL");
} else if (result == V2TXLiveCode.V2TXLIVE_ERROR_REFUSED) {
    print("Operation refused");
} else if (result == V2TXLiveCode.V2TXLIVE_ERROR_INVALID_LICENSE) {
    print("Invalid License, please check your License");
}
```

#### Stop Playback
```dart
Future<V2TXLiveCode> stopPlay()
```

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**When to Use**: After playback has started

**Example**:
```dart
await player.stopPlay();
```

#### Check Playback Status
```dart
Future<int> isPlaying()
```

**Return Value**:
- `1`: Currently playing
- `0`: Playback stopped

**When to Use**: Any time

**Example**:
```dart
int isPlaying = await player.isPlaying();
if (isPlaying == 1) {
    print("Playing");
} else {
    print("Playback stopped");
}
```

### Cache Control APIs

#### Set Cache Parameters
```dart
Future<V2TXLiveCode> setCacheParams(double minTime, double maxTime)
```

**Parameters**:
- `minTime`: Minimum cache time (seconds), must be > 0 [Default: 1]
- `maxTime`: Maximum cache time (seconds), must be > 0 [Default: 5]

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: minTime and maxTime must be greater than 0

**Optimization Tips**:
- **Stable Network**: Use a smaller cache (1–3 seconds)
- **Unstable Network**: Use a larger cache (3–5 seconds)
- **No Special Requirements**: Use default values

**When to Use**: Any time

**Example**:
```dart
await player.setCacheParams(1, 5);
```

### Advanced Feature APIs

#### Switch Stream
```dart
Future<V2TXLiveCode> switchStream(String newUrl)
```

**Parameters**:
- `newUrl`: URL of the new stream with different resolution

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**When to Use**: After playback has started

**Example**:
```dart
await player.startLivePlay("http://example.com/live/stream_1080p.flv");

player.addListener(V2TXLivePlayerObserver(
  onStreamSwitched: (player, url, code) {
    if (code == 0) {
      print("Switch successful");
    } else if (code == -1) {
      print("Switch timeout");
    } else if (code == -2) {
      print("Switch failed, server error");
    } else if (code == -3) {
      print("Switch failed, client error");
    }
  }
));
await player.switchStream("http://example.com/live/stream_720p.flv");
```

### Cache Control

#### Set Cache Parameters
**Feature**: Configure minimum and maximum cache times for automatic adjustment
```dart
Future<V2TXLiveCode> setCacheParams(double minTime, double maxTime)
```
**Parameters**:
- `minTime`: Minimum cache time (seconds), must be > 0, default: 1
- `maxTime`: Maximum cache time (seconds), must be > 0, default: 5

**Error Codes**:
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: minTime and maxTime must be greater than 0
- `V2TXLIVE_ERROR_REFUSED`: Cannot modify cache strategy while player is playing

#### Enable Volume Evaluation
```dart
Future<V2TXLiveCode> enableVolumeEvaluation(int intervalMs)
```

**Parameters**:
- `intervalMs`: Interval for `onPlayoutVolumeUpdate` callback in ms. Minimum is 100ms. Set to 0 or less to disable. Recommended: 300ms [Default: 0, disabled]

**Description**: Enables SDK volume level evaluation via the `V2TXLivePlayerObserver` callback.

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**When to Use**: Any time

**Example**:
```dart
player.addListener(V2TXLivePlayerObserver(
  onPlayoutVolumeUpdate: (player, volume) {
    print("Audio playback volume: $volume");
  }
));
await player.enableVolumeEvaluation(300);
```

#### Snapshot
```dart
Future<V2TXLiveCode> snapshot()
```

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success
- `V2TXLIVE_ERROR_REFUSED`: Cannot capture snapshot when player is stopped

**When to Use**: After playback has started

**Example**:
```dart
player.addListener(V2TXLivePlayerObserver(
  onSnapshotComplete: (player, image) {
    // Handle snapshot
  }
));
await player.snapshot();
```

#### Enable Custom Video Rendering
```dart
Future<V2TXLiveCode> enableObserveVideoFrame(bool enable, int pixelFormat, int bufferType)
```

**Parameters**:
- `enable`: Enable custom rendering [Default: false]
- `pixelFormat`: Pixel format for rendering callback (`V2TXLivePixelFormat`)
- `bufferType`: Data format for rendering callback (`V2TXLiveBufferType`)

**Description**:  
- When enabled, SDK stops default video rendering. You can access video frames via `V2TXLivePlayerObserver` and implement your own rendering logic.
- Supported combinations:
  - `V2TXLivePixelFormat.v2TXLivePixelFormatTexture2D`, `V2TXLiveBufferType.v2TXLiveBufferTypeTexture` (recommended)
  - `V2TXLivePixelFormat.v2TXLivePixelFormatI420`, `V2TXLiveBufferType.v2TXLiveBufferTypeByteArray`
  - `V2TXLivePixelFormat.v2TXLivePixelFormatI420`, `V2TXLiveBufferType.v2TXLiveBufferTypeByteBuffer`

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success
- `V2TXLIVE_ERROR_NOT_SUPPORTED`: Unsupported pixel or data format

**When to Use**: Before playback starts

**Example**:
```dart
await player.enableObserveVideoFrame(true, 
    V2TXLivePixelFormat.v2TXLivePixelFormatTexture2D, 
    V2TXLiveBufferType.v2TXLiveBufferTypeTexture);
player.addListener(V2TXLivePlayerObserver(
  onRenderVideoFrame: (player, videoFrame) {
    // Custom rendering logic
  }
));
```

#### Enable Audio Data Callback
```dart
Future<V2TXLiveCode> enableObserveAudioFrame(bool enable)
```

**Parameters**:
- `enable`: Enable audio data callback [Default: false]

**Description**: When enabled, access audio data via `V2TXLivePlayerObserver` for custom processing.

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**When to Use**: Before playback starts

**Example**:
```dart
await player.enableObserveAudioFrame(true);
player.addListener(V2TXLivePlayerObserver(
  onPlayoutAudioFrame: (player, audioFrame) {
    // Custom audio processing
  }
));
```

#### Enable SEI Message Reception
```dart
Future<V2TXLiveCode> enableReceiveSeiMessage(bool enable, int payloadType)
```

**Parameters**:
- `enable`: true to enable, false to disable [Default: false]
- `payloadType`: Supported values: 5, 242, 243. Must match sender's payloadType.

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success

**When to Use**: Before playback starts

**Example**:
```dart
await player.enableReceiveSeiMessage(true, 5);
await player.enableReceiveSeiMessage(true, 242);
await player.enableReceiveSeiMessage(true, 243);
player.addListener(V2TXLivePlayerObserver(
  onReceiveSeiMessage: (player, payloadType, data) {
    // Handle SEI message
  }
));
```

### Local Recording APIs

#### Start Local Recording
```dart
Future<V2TXLiveCode> startLocalRecording(V2TXLiveLocalRecordingParams params)
```

**Parameters**:
- `params`: See `V2TXLiveDef.dart` for details

**Important**:
- Start recording only after stream playback has begun; starting before pulling is invalid
- Do not switch between software and hardware decoding during recording, as this may corrupt video files

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: Invalid parameter, e.g., empty filePath
- `V2TXLIVE_ERROR_REFUSED`: API refused, stream not started

**When to Use**: After playback has started

**Example**:
```dart
player.addListener(V2TXLivePlayerObserver(
  onLocalRecordBegin: (player, code, storagePath) {
    print("Recording started");
  },
  onLocalRecording: (player, durationMs, storagePath) {
    print("Recording..., durationMs: $durationMs");
  },
  onLocalRecordComplete: (player, code, storagePath) {
    print("Recording completed");
  }
));

V2TXLiveLocalRecordingParams params = V2TXLiveLocalRecordingParams(
  filePath: "filepath",
  interval: 2000
);
V2TXLiveCode code = await player.startLocalRecording(params);
if (code == V2TXLiveCode.V2TXLIVE_OK) {
    print("Recording started successfully");
} else if (code == V2TXLiveCode.V2TXLIVE_ERROR_INVALID_PARAMETER) {
    print("Invalid recording parameters");
} else if (code == V2TXLiveCode.V2TXLIVE_ERROR_REFUSED) {
    print("Recording operation refused");
}
```

#### Stop Local Recording
```dart
Future<void> stopLocalRecording()
```

**Description**: If playback stops during recording, the SDK will automatically end the recording.

**When to Use**: After playback and recording have started

**Example**:
```dart
await player.stopLocalRecording();
```

### Debugging and Advanced Configuration APIs

#### Show Debug View
```dart
Future<void> showDebugView(bool isShow)
```

**Parameters**:
- `isShow`: true to show debug overlay [Default: false]

**When to Use**: Any time

**Example**:
```dart
await player.showDebugView(true);
```

#### Set Advanced Property
```dart
Future<V2TXLiveCode> setProperty(String key, Object value)
```

**Parameters**:
- `key`: Advanced API key
- `value`: Value for the advanced API

**Description**: For advanced features. For specific requirements, contact your business representative or solution architect.

**Return Value**: `V2TXLiveCode`
- `V2TXLIVE_OK`: Success
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: Key cannot be null

**Example**:
```dart
await player.setProperty("key", "value");
```

## Usage Example

```dart
import 'package:tencent_trtc/v2_tx_live_player.dart';
import 'package:tencent_trtc/v2_tx_live_player_observer.dart';
import 'package:tencent_trtc/v2_tx_live_def.dart';

class LivePlayerExample {
  late V2TXLivePlayer player;
  
  // Initialize player
  Future<void> initPlayer() async {
    // Create player instance
    player = await V2TXLivePlayer.create();
    
    // Register player callbacks
    player.addListener(V2TXLivePlayerObserver(
      onConnected: (player) {
        print('Player connected');
      },
      onVideoPlaying: (player, isFirstPlay) {
        print('Video started playing');
      },
      onAudioPlaying: (player, isFirstPlay) {
        print('Audio started playing');
      },
      onPlayoutVolumeUpdate: (player, volume) {
        print('Playback volume updated: $volume');
      },
      onError: (player, code, msg, extraInfo) {
        print('Player error: $code, $msg');
      }
    ));
    
    // Set rendering view
    await player.setRenderViewID(viewId);
    
    // Set rotation angle
    await player.setRenderRotation(V2TXLiveRotation.v2TXLiveRotation0);
    
    // Set fill mode
    await player.setRenderFillMode(V2TXLiveFillMode.v2TXLiveFillModeFit);
    
    // Set cache parameters
    await player.setCacheParams(1.0, 5.0);
    
    // Enable volume evaluation
    await player.enableVolumeEvaluation(300);
  }
  
  // Start playback
  Future<void> startPlay(String url) async {
    V2TXLiveCode result = await player.startLivePlay(url);
    if (result == V2TXLiveCode.V2TXLIVE_OK) {
      print('Playback started successfully');
    } else {
      print('Playback failed: $result');
    }
  }
  
  // Pause/Resume video
  Future<void> toggleVideo() async {
    int isPlaying = await player.isPlaying();
    if (isPlaying == 1) {
      await player.pauseVideo();
      print('Video paused');
    } else {
      await player.resumeVideo();
      print('Video resumed');
    }
  }
  
  // Pause/Resume audio
  Future<void> toggleAudio() async {
    int isPlaying = await player.isPlaying();
    if (isPlaying == 1) {
      await player.pauseAudio();
      print('Audio paused');
    } else {
      await player.resumeAudio();
      print('Audio resumed');
    }
  }
  
  // Set volume
  Future<void> setVolume(int volume) async {
    await player.setPlayoutVolume(volume);
    print('Volume set to: $volume');
  }
  
  // Switch stream
  Future<void> switchStream(String newUrl) async {
    await player.switchStream(newUrl);
    print('Switching stream...');
  }
  
  // Take snapshot
  Future<void> takeSnapshot() async {
    await player.snapshot();
    print('Snapshot triggered');
  }
  
  // Stop playback
  Future<void> stopPlay() async {
    await player.stopPlay();
    print('Playback stopped');
  }
  
  // Destroy player
  void destroyPlayer() {
    player.destroy();
    print('Player destroyed');
  }
}

// Usage example
void main() async {
  LivePlayerExample example = LivePlayerExample();
  await example.initPlayer();
  await example.startPlay('http://example.com/live/stream.flv');
  await Future.delayed(Duration(seconds: 10));
  await example.takeSnapshot();
  await example.stopPlay();
  example.destroyPlayer();
}
```

## Notes

1. **License Requirement**: Starting with version 10.7, you must set a valid License for playback to work.
2. **Permission Requirement**: Requires network and audio playback permissions.
3. **Lifecycle Management**: After creating an instance with `create()`, call `destroy()` to release resources.
4. **Observer Registration**: Register observers before playback to receive status callbacks.
5. **Error Handling**: All async methods return `V2TXLiveCode`; handle errors accordingly.
6. **Thread Safety**: Invoke API calls on the main thread.
7. **Resource Release**: Release resources promptly after playback ends to prevent memory leaks.
8. **Cache Strategy**: Adjust cache parameters based on network conditions for optimal playback.

## FAQs

### Q: Why does the player show a black screen with no video?
A: Verify that a valid License is set, the playback URL is correct, and the rendering view is properly configured.

### Q: Why is playback latency high?
A: Adjust cache parameters. For stable networks, use a smaller cache time (1–3 seconds).

### Q: How can I switch resolutions seamlessly?
A: Call the `switchStream()` method with a stream URL of a different resolution.

### Q: How do I get playback statistics?
A: Use the `onStatisticsUpdate` callback in `V2TXLivePlayerObserver`.