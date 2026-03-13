> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

# Tencent Cloud Live Streaming SDK V2TXLivePlayerObserver Player Callback Interface Documentation

## Feature Overview

`V2TXLivePlayerObserver` is the callback interface for the Tencent Cloud Live Streaming SDK. It provides notifications and event callbacks from the player, allowing you to monitor playback status, handle events, collect statistics, and more.

**File Path**: `v2_tx_live_player_observer.dart`  
**Platform Support**: Flutter

**Core Features**:
- Monitor player status (errors, warnings, connection state)
- Receive audio/video playback event callbacks
- Access playback statistics and performance metrics
- Enable custom video rendering and audio processing
- Manage local recording tasks
- Receive and handle SEI messages

## Callback Methods

### Error and Warning Callbacks

#### onError - Playback Error Callback
```dart
void onError(V2TXLivePlayer player, int code, String msg, Map<String, dynamic> extraInfo)
```

**Description**: Invoked when the player encounters an error.

**Parameters**:
- `player`: The player instance that triggered the callback
- `code`: Error code (see `V2TXLiveCode`)
- `msg`: Error description
- `extraInfo`: Additional error details

**Typical Scenarios**:
- Invalid RTC stream pull parameters
- RTC stream pull timeout
- RTC stream pull server processing failure
- HEVC decoder not found

**Example**:
```dart
player.addListener(V2TXLivePlayerObserver(
  onError: (player, code, msg, extraInfo) {
    switch (code) {
      case V2TXLiveCode.V2TXLIVE_ERROR_INVALID_PARAMETER:
        print('Invalid RTC stream pull parameters, $msg');
        break;
      case V2TXLiveCode.V2TXLIVE_ERROR_REQUEST_TIMEOUT:
        print('RTC stream pull timeout, $msg');
        break;
      case V2TXLiveCode.V2TXLIVE_ERROR_SERVER_PROCESS_FAILED:
        print('RTC stream pull server processing failed, please check the stream pull parameters, $msg');
        break;
      case V2TXLiveCode.V2TXLIVE_ERROR_DISCONNECTED:
        print('Stream pull disconnected, $msg');
        break;
      case V2TXLiveCode.V2TXLIVE_ERROR_NO_AVAILABLE_HEVC_DECODERS:
        print('HEVC decoder not found, you can switch to AVC stream for playback, $msg');
        break;
      default:
        print('Other error, $msg');
        break;
    }
  }
));
```

#### onWarning - Playback Warning Callback
```dart
void onWarning(V2TXLivePlayer player, int code, String msg, Map<String, dynamic> extraInfo)
```

**Description**: Invoked when the player encounters a warning.

**Parameters**:
- `player`: The player instance that triggered the callback
- `code`: Warning code (see `V2TXLiveCode`)
- `msg`: Warning description
- `extraInfo`: Additional warning details

**Typical Scenarios**:
- Video rendering stutter
- Decoder type change

**Example**:
```dart
player.addListener(V2TXLivePlayerObserver(
  onWarning: (player, code, msg, extraInfo) {
    switch (code) {
      case V2TXLiveCode.V2TXLIVE_WARNING_VIDEO_BLOCK:
        print('Video rendering stutter detected');
        break;
      case V2TXLiveCode.V2TXLIVE_WARNING_CURRENT_DECODE_TYPE_CHANGED:
        int codecType = extraInfo['codec_type'];
        if (codecType == 0) {
          print('Decoder type changed to h.264, $msg');
        } else if (codecType == 1) {
          print('Decoder type changed to h.265, $msg');
        }
        break;
      default:
        print('Other warning, $msg');
        break;
    }
  }
));
```

## Callback Type Enumeration

### V2TXLivePlayerListenerType

Enumeration of all available player callback event types:

| Enum Value | Description | Parameter Details |
|--------|------|----------|
| `onError` | **Error Callback** – Unrecoverable SDK error | `code`: Error code<br>`msg`: Error message<br>`extraInfo`: Additional info |
| `onWarning` | **Warning Callback** – Non-critical issues (e.g., stutter, recoverable decoding failure) | `code`: Warning code<br>`msg`: Warning message<br>`extraInfo`: Additional info |
| `onVideoResolutionChanged` | **Video Resolution Change** | `width`: Video width<br>`height`: Video height |
| `onConnected` | **Connection Success** | `extraInfo`: Additional info |
| `onVideoPlaying` | **Video Playback Event** | `firstPlay`: First play flag<br>`extraInfo`: Additional info |
| `onAudioPlaying` | **Audio Playback Event** | `firstPlay`: First play flag<br>`extraInfo`: Additional info |
| `onVideoLoading` | **Video Loading Event** | `extraInfo`: Additional info |
| `onAudioLoading` | **Audio Loading Event** | `extraInfo`: Additional info |
| `onPlayoutVolumeUpdate` | **Playback Volume Update** | `volume`: Volume (0-100) |
| `onStatisticsUpdate` | **Playback Statistics** | `appCpu`: App CPU usage (%)<br>`systemCpu`: System CPU usage (%)<br>`width`: Video width<br>`height`: Video height<br>`fps`: Frame rate<br>`videoBitrate`: Video bitrate (Kbps)<br>`audioBitrate`: Audio bitrate (Kbps) |
| `onSnapshotComplete` | **Snapshot Complete** | `image`: Captured video frame (Uint8List) |
| `onRenderVideoFrame` | **Custom Video Rendering** | `videoFrame`: Video frame data (Map) |
| `onReceiveSeiMessage` | **SEI Message Reception** | `payloadType`: Message type<br>`data`: Message content (Uint8List) |
| `onPictureInPictureStateUpdate` | **Picture-in-Picture State Change** | `state`: State code<br>`message`: State message<br>`extraInfo`: Additional info |
| `onStreamSwitched` | **Stream Switch** | Parameters not detailed |

## Callback Function Definition

### V2TXLivePlayerObserver

Player observer callback function type:

```dart
typedef V2TXLivePlayerObserver<P> = void Function(
    V2TXLivePlayerListenerType type, 
    P? params
);
```

**Parameters:**
- `type`: Callback event type (`V2TXLivePlayerListenerType`)
- `params`: Callback parameters (type P), varies by callback type

## Callback Categories

### Error and Warning Callbacks

#### onError
- **Importance**: High
- **Trigger**: When the SDK encounters an unrecoverable error
- **Recommendation**: Always listen for this callback and provide appropriate UI feedback based on the error code

#### onWarning
- **Importance**: Medium
- **Trigger**: When non-critical issues occur, such as stutter or recoverable decoding failures
- **Recommendation**: Optional to listen; useful for monitoring playback quality

### Connection and Status Callbacks

#### onConnected - Connection Success Callback
```dart
void onConnected(V2TXLivePlayer player, Map<String, dynamic> extraInfo)
```

**Description**: Called when the player successfully connects to the server.

**Parameters**:
- `player`: The player instance
- `extraInfo`: Connection details

**Typical Scenarios**:
- Monitor network connection status
- Confirm player connection

**Example**:
```dart
player.addListener(V2TXLivePlayerObserver(
  onConnected: (player, extraInfo) {
    print('Successfully connected to the server');
  }
));
```

#### onVideoResolutionChanged - Video Resolution Change Callback
```dart
void onVideoResolutionChanged(V2TXLivePlayer player, int width, int height)
```

**Description**: Called when the video resolution changes.

**Parameters**:
- `player`: The player instance
- `width`: New video width
- `height`: New video height

**Typical Scenarios**:
- Adaptive video rendering
- Dynamic player layout adjustment

**Example**:
```dart
player.addListener(V2TXLivePlayerObserver(
  onVideoResolutionChanged: (player, width, height) {
    print('Video stream resolution changed: width-$width, height-$height');
  }
));
```

### Playback Event Callbacks

#### onVideoPlaying - Video Playback Started
```dart
void onVideoPlaying(V2TXLivePlayer player, bool firstPlay, Map<String, dynamic> extraInfo)
```

**Description**: Called when video playback starts. For non-initial playback, this is paired with onVideoLoading.

**Parameters**:
- `player`: The player instance
- `firstPlay`: Whether this is the first playback
- `extraInfo`: Playback details

**Typical Scenarios**:
- Show playback status UI
- Start playback timer
- Log playback events
- Measure time to first frame

**Example**:
```dart
player.addListener(V2TXLivePlayerObserver(
  onVideoPlaying: (player, firstPlay, extraInfo) {
    if (firstPlay) {
      print('First playback started');
    } else {
      print('Playback started');
    }
  }
));
```

#### onVideoLoading - Video Loading Started
```dart
void onVideoLoading(V2TXLivePlayer player, Map<String, dynamic> extraInfo)
```

**Description**: Called when video data begins loading.

**Parameters**:
- `player`: The player instance
- `extraInfo`: Loading status

**Typical Scenarios**:
- Show loading animation
- Indicate buffering status

**Example**:
```dart
player.addListener(V2TXLivePlayerObserver(
  onVideoLoading: (player, extraInfo) {
    print('Video playback loading started');
  }
));
```

#### onAudioPlaying - Audio Playback Started
```dart
void onAudioPlaying(V2TXLivePlayer player, bool firstPlay, Map<String, dynamic> extraInfo)
```

**Description**: Called when audio playback starts.

**Parameters**:
- `player`: The player instance
- `firstPlay`: Whether this is the first playback
- `extraInfo`: Playback details

**Typical Scenarios**:
- Monitor audio playback status
- Pure audio stream playback

**Example**:
```dart
player.addListener(V2TXLivePlayerObserver(
  onAudioPlaying: (player, firstPlay, extraInfo) {
    if (firstPlay) {
      print('Audio playback started for the first time');
    } else {
      print('Audio playback started');
    }
  }
));
```

#### onAudioLoading - Audio Loading Started
```dart
void onAudioLoading(V2TXLivePlayer player, Map<String, dynamic> extraInfo)
```

**Description**: Called when audio data begins loading.

**Parameters**:
- `player`: The player instance
- `extraInfo`: Loading status

**Typical Scenarios**:
- Show loading animation
- Indicate buffering status

**Example**:
```dart
player.addListener(V2TXLivePlayerObserver(
  onAudioLoading: (player, extraInfo) {
    print('Audio playback loading started');
  }
));
```

### Audio/Video Quality Monitoring Callback

#### onVideoResolutionChanged
- **Trigger**: When the live stream resolution changes

### Audio/Video Data Processing Callbacks

#### onPlayoutVolumeUpdate - Playback Volume Callback
```dart
void onPlayoutVolumeUpdate(V2TXLivePlayer player, int volume)
```

**Description**: Real-time callback for playback volume.

**Parameters**:
- `player`: The player instance
- `volume`: Current playback volume (0-100)

**Prerequisite**: Call `enableVolumeEvaluation()` to enable volume evaluation.

**Typical Scenarios**:
- Display real-time volume
- Show audio waveform animation
- Detect mute status

**Example**:
```dart
player.addListener(V2TXLivePlayerObserver(
  onPlayoutVolumeUpdate: (player, volume) {
    print('Audio playback volume: $volume');
  }
));
player.enableVolumeEvaluation(300);
```

#### onRenderVideoFrame - Custom Video Rendering Callback
```dart
void onRenderVideoFrame(V2TXLivePlayer player, Map<String, dynamic> videoFrame)
```

**Description**: Callback for custom video frame rendering.

**Parameters**:
- `player`: The player instance
- `videoFrame`: Video frame data (pixel format, buffer type, etc.)

**Prerequisite**: Call `enableObserveVideoFrame()` to enable video frame callbacks.

**Typical Scenarios**:
- Custom video rendering
- Add filter effects
- Process video watermarks

**Example**:
```dart
await player.enableObserveVideoFrame(true, 
    V2TXLivePixelFormat.v2TXLivePixelFormatTexture2D, 
    V2TXLiveBufferType.v2TXLiveBufferTypeTexture);

player.addListener(V2TXLivePlayerObserver(
  onRenderVideoFrame: (player, videoFrame) {
    print('Received video frame: ${videoFrame['width']}x${videoFrame['height']}');
  }
));
```

#### onPlayoutAudioFrame - Audio Data Callback
```dart
void onPlayoutAudioFrame(V2TXLivePlayer player, Map<String, dynamic> audioFrame)
```

**Description**: Callback for audio frame data during playback.

**Parameters**:
- `player`: The player instance
- `audioFrame`: Audio frame data (sample rate, audio channels, etc.)

**Prerequisite**: Call `enableObserveAudioFrame()` to enable audio frame callbacks.

**Typical Scenarios**:
- Custom audio processing
- Audio analysis
- Real-time audio effects

**Example**:
```dart
await player.enableObserveAudioFrame(true);

player.addListener(V2TXLivePlayerObserver(
  onPlayoutAudioFrame: (player, audioFrame) {
    print('Received audio frame, sample rate: ${audioFrame['sampleRate']}');
  }
));
```

### Statistics and Monitoring Callback

#### onStatisticsUpdate - Playback Statistics Callback
```dart
void onStatisticsUpdate(V2TXLivePlayer player, Map<String, dynamic> statistics)
```

**Description**: Real-time callback for playback statistics, triggered about every 2 seconds.

**Parameters**:
- `player`: The player instance
- `statistics`: Playback statistics:
  - `appCpu`: App CPU usage (%)
  - `systemCpu`: System CPU usage (%)
  - `width`: Video width
  - `height`: Video height
  - `fps`: Frame rate
  - `videoBitrate`: Video bitrate (Kbps)
  - `audioBitrate`: Audio bitrate (Kbps)
  - `audioSampleRate`: Audio sample rate
  - `audioChannels`: Audio channel count

**Typical Scenarios**:
- Monitor playback quality
- Analyze performance
- Collect user experience metrics

**Example**:
```dart
player.addListener(V2TXLivePlayerObserver(
  onStatisticsUpdate: (player, statistics) {
    print('Playback statistics:');
    print('  - App CPU: ${statistics['appCpu']}%');
    print('  - System CPU: ${statistics['systemCpu']}%');
    print('  - Resolution: ${statistics['width']}x${statistics['height']}');
    print('  - Frame rate: ${statistics['fps']}fps');
    print('  - Video bitrate: ${statistics['videoBitrate']}Kbps');
    print('  - Audio bitrate: ${statistics['audioBitrate']}Kbps');
  }
));
```

### Advanced Feature Callbacks

#### onSnapshotComplete - Snapshot Callback
```dart
void onSnapshotComplete(V2TXLivePlayer player, Uint8List image)
```

**Description**: Called when a snapshot operation completes.

**Parameters**:
- `player`: The player instance
- `image`: Captured video frame data (Uint8List)

**Typical Scenarios**:
- Save video snapshots
- Frame sharing

**Example**:
```dart
player.addListener(V2TXLivePlayerObserver(
  onSnapshotComplete: (player, image) {
    print('Snapshot complete, image size: ${image.length} bytes');
    // Save or share the image
  }
));
player.snapshot();
```

#### onReceiveSeiMessage - SEI Message Callback
```dart
void onReceiveSeiMessage(V2TXLivePlayer player, int payloadType, Uint8List data)
```

**Description**: Called when an SEI (Supplemental Enhancement Information) message is received.

**Parameters**:
- `player`: The player instance
- `payloadType`: SEI message type
- `data`: SEI message data

**Prerequisite**: Call `enableReceiveSeiMessage()` to enable SEI message reception.

**Typical Scenarios**:
- Transmit scene information
- Send interactive messages
- Synchronize timestamps

**Example**:
```dart
await player.enableReceiveSeiMessage(true, 5);

player.addListener(V2TXLivePlayerObserver(
  onReceiveSeiMessage: (player, payloadType, data) {
    print('Received SEI message, type: $payloadType, data size: ${data.length} bytes');
  }
));
```

#### onStreamSwitched - Stream Switch Callback
```dart
void onStreamSwitched(V2TXLivePlayer player, String url, int code)
```

**Description**: Called after a stream resolution switch completes, triggered by `switchStream()`.

**Parameters**:
- `player`: The player instance
- `url`: Playback URL after switching
- `code`: Switch status code (0: success, -1: timeout, -2: server error, -3: client error)

**Typical Scenarios**:
- Monitor stream quality switching
- Provide switch status feedback

**Example**:
```dart
player.startLivePlay("http://example.com/live/stream_1080p.flv");

player.addListener(V2TXLivePlayerObserver(
  onStreamSwitched: (player, url, code) {
    if (code == 0) {
      print('Switch successful');
    } else if (code == -1) {
      print('Switch timeout');
    } else if (code == -2) {
      print('Switch failed, server error');
    } else if (code == -3) {
      print('Switch failed, client error');
    }
  }
));

await player.switchStream("http://example.com/live/stream_720p.flv");
```

### Local Recording Callbacks

#### onLocalRecordBegin - Recording Start Callback
```dart
void onLocalRecordBegin(V2TXLivePlayer player, int code, String storagePath)
```

**Description**: Called when a local recording task starts (triggered by `startLocalRecording()`).

**Parameters**:
- `player`: The player instance
- `code`: Recording status code
- `storagePath`: Recording file path

**Status Codes**:
- `0`: Recording started successfully
- `-1`: Internal error
- `-2`: Invalid file extension
- `-6`: Recording already started
- `-7`: Recording file already exists
- `-8`: No write permission for recording directory

#### onLocalRecording - Recording Progress Callback
```dart
void onLocalRecording(V2TXLivePlayer player, int durationMs, String storagePath)
```

**Description**: Called to report ongoing recording progress. Frequency matches the `interval` parameter in `startLocalRecording()`.

**Parameters**:
- `player`: The player instance
- `durationMs`: Recorded duration (milliseconds)
- `storagePath`: Recording file path

**Typical Scenarios**:
- Display recording progress
- Enforce recording duration limits
- Monitor recording status

#### onLocalRecordComplete - Recording Complete Callback
```dart
void onLocalRecordComplete(V2TXLivePlayer player, int code, String storagePath)
```

**Description**: Called when a recording task completes (triggered by `stopLocalRecording()`).

**Parameters**:
- `player`: The player instance
- `code`: Recording completion status code
- `storagePath`: Recording file path

**Status Codes**:
- `0`: Recording ended successfully
- `-1`: Recording failed
- `-2`: Ended due to resolution or orientation change
- `-3`: Duration too short or no data collected

**Example**:
```dart
player.addListener(V2TXLivePlayerObserver(
  onLocalRecordBegin: (player, code, storagePath) {
    print('Recording started');
  },
  onLocalRecording: (player, durationMs, storagePath) {
    print('Recording in progress..., durationMs: $durationMs');
  },
  onLocalRecordComplete: (player, code, storagePath) {
    print('Recording completed');
  }
));

V2TXLiveLocalRecordingParams params = V2TXLiveLocalRecordingParams(
  filePath: "filepath",
  interval: 2000
);
V2TXLiveCode code = await player.startLocalRecording(params);
if (code == V2TXLiveCode.V2TXLIVE_OK) {
    print('Recording started successfully');
} else if (code == V2TXLiveCode.V2TXLIVE_ERROR_INVALID_PARAMETER) {
    print('Invalid recording parameters');
} else if (code == V2TXLiveCode.V2TXLIVE_ERROR_REFUSED) {
    print('Recording call refused');
}
```

### Usage Examples

#### Basic Player Callback Implementation
```dart
class MyPlayerObserver extends V2TXLivePlayerObserver {
  @override
  void onError(V2TXLivePlayer player, int code, String msg, Map<String, dynamic> extraInfo) {
    // Handle playback error
    print('PlayerError: Error code: $code, Error message: $msg');
  }
  
  @override
  void onConnected(V2TXLivePlayer player, Map<String, dynamic> extraInfo) {
    // Handle successful connection
    print('Player: Successfully connected to server');
  }
  
  @override
  void onVideoPlaying(V2TXLivePlayer player, bool firstPlay, Map<String, dynamic> extraInfo) {
    // Video playback started
    if (firstPlay) {
      print('Player: First playback started');
    }
  }
  
  @override
  void onStatisticsUpdate(V2TXLivePlayer player, Map<String, dynamic> statistics) {
    // Update playback statistics
    print('PlayerStats: FPS: ${statistics['fps']}, Bitrate: ${statistics['videoBitrate']}');
  }
}

// Set callback observer
V2TXLivePlayer player = await V2TXLivePlayer.create();
player.addListener(MyPlayerObserver());
```

#### Custom Video Processing Example
```dart
class VideoProcessorObserver extends V2TXLivePlayerObserver {
  @override
  void onRenderVideoFrame(V2TXLivePlayer player, Map<String, dynamic> videoFrame) {
    // Custom video frame processing
    // Add filters, watermarks, etc.
    processVideoFrame(videoFrame);
  }
  
  void processVideoFrame(Map<String, dynamic> frame) {
    print('Processing video frame: ${frame['width']}x${frame['height']}');
  }
}

// Enable custom video frame callback
await player.enableObserveVideoFrame(true);
player.addListener(VideoProcessorObserver());
```

#### Local Recording Monitoring Example
```dart
class RecordingObserver extends V2TXLivePlayerObserver {
  @override
  void onLocalRecordBegin(V2TXLivePlayer player, int code, String storagePath) {
    if (code == 0) {
      print('Recording: Started, file path: $storagePath');
    } else {
      print('Recording: Failed, error code: $code');
    }
  }
  
  @override
  void onLocalRecording(V2TXLivePlayer player, int durationMs, String storagePath) {
    updateRecordingProgress(durationMs);
  }
  
  @override
  void onLocalRecordComplete(V2TXLivePlayer player, int code, String storagePath) {
    if (code == 0) {
      print('Recording: Completed, file path: $storagePath');
    } else {
      print('Recording: Abnormally ended, status code: $code');
    }
  }
  
  void updateRecordingProgress(int durationMs) {
    print('Recording progress: ${durationMs}ms');
  }
}

player.addListener(RecordingObserver());
```

## Notes

### Callback Thread Safety
- **Main Thread Execution**: All callbacks except custom rendering run on the UI main thread.
- **Thread Switching**: Custom rendering callbacks may run on non-UI threads; ensure thread safety.

### Performance Impact
- **Custom Rendering**: Enabling custom video rendering can impact playback performance. Use only when necessary.
- **Audio Processing**: Audio data callbacks may increase CPU usage. Control processing frequency.
- **Statistics Frequency**: Statistics callbacks are triggered about every 2 seconds. Avoid heavy operations in these callbacks.

### Memory Management
- **Release Observers**: Remove unused observer objects promptly to prevent memory leaks.
- **Callback References**: Avoid strong references to the player in callbacks to prevent reference cycles.
- **Resource Cleanup**: Remove all observers before destroying the player.

### Error Handling
- **Error Code Handling**: Parse error codes and provide user-friendly feedback.
- **Exception Handling**: Add try/catch in callbacks to prevent crashes.
- **State Recovery**: Implement recovery logic based on error types.

### Permissions and Configuration
- **Storage Permission**: Local recording requires storage permission and enough free space.
- **Network Permission**: The player needs network permission for stream pulling.
- **Audio Permission**: Audio playback requires audio permission.

### Best Practices

#### Error Handling Best Practice
```dart
player.addListener(V2TXLivePlayerObserver(
  onError: (player, code, msg, extraInfo) {
    try {
      // Show user-friendly error messages
      switch (code) {
        case V2TXLiveCode.V2TXLIVE_ERROR_INVALID_PARAMETER:
          showToast('Invalid playback URL, please check and try again');
          break;
        case V2TXLiveCode.V2TXLIVE_ERROR_REQUEST_TIMEOUT:
          showToast('Network connection timeout, please check your network and try again');
          break;
        default:
          showToast('Playback failed, please try again later');
          break;
      }
    } catch (e) {
      print('Error handling exception: $e');
    }
  }
));
```

#### Performance Monitoring Best Practice
```dart
player.addListener(V2TXLivePlayerObserver(
  onStatisticsUpdate: (player, statistics) {
    double fps = statistics['fps'];
    double bitrate = statistics['videoBitrate'];
    
    if (fps < 15) {
      print('Warning: Low frame rate ($fps fps)');
    }
    
    if (bitrate < 500) {
      print('Warning: Low video bitrate ($bitrate Kbps)');
    }
  }
));
```

#### Memory Management Best Practice
```dart
class PlayerManager {
  V2TXLivePlayer? player;
  V2TXLivePlayerObserver? observer;
  
  Future<void> initPlayer() async {
    player = await V2TXLivePlayer.create();
    observer = V2TXLivePlayerObserver(
      onConnected: (player, extraInfo) {
        print('Connection successful');
      }
    );
    player!.addListener(observer!);
  }
  
  void dispose() {
    // Remove observer first
    if (player != null && observer != null) {
      player!.removeListener(observer!);
    }
    // Then destroy player
    player?.destroy();
    player = null;
    observer = null;
  }
}
```

## FAQs

### Q: Why am I not receiving callbacks?
A: Check the following:
1. Is the observer correctly set using `player.addListener(observer)`?
2. Has the player been created and initialized successfully?
3. Are callbacks registered at the correct time?

### Q: What should I do if custom rendering callbacks have poor performance?
A: Recommendations:
1. Optimize rendering logic and avoid heavy computations.
2. Use asynchronous processing to minimize main thread blocking.
3. Enable custom rendering only when necessary.

### Q: How do I resolve local recording failures?
A: Check:
1. Is storage permission granted?
2. Is the storage path valid and writable?
3. Is there enough free storage space?

### Q: Why am I not receiving SEI messages?
A: Confirm:
1. Has `enableReceiveSeiMessage()` been called?
2. Does payloadType match the sender?
3. Does the stream contain SEI messages?

## File Information

- **File Path**: `/Users/borryzhang/Work/Project/liteav_flutter/sdk/trtc/v3/lib/v2_tx_live_player_observer.dart`
- **File Size**: 3.26 KB
- **Total Lines**: 140
- **Platform Support**: Flutter
- **SDK Version**: v3