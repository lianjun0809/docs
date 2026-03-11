> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

# Tencent Cloud Live Streaming SDK V2TXLivePlayerObserver Live Player Callback Interface

## Feature Overview

`V2TXLivePlayerObserver` is the callback interface for the Tencent Cloud Live Streaming SDK player. Implement this interface to receive real-time status updates and event notifications from the player. By handling these callbacks, you can monitor player status, respond to playback events, collect statistics, and more.

**File Path**: `com/tencent/live2/V2TXLivePlayerObserver.java`

**Core Features**:
- Player status monitoring (errors, warnings, connection events)
- Audio and video playback event callbacks
- Playback statistics and performance metrics
- Custom video rendering and audio processing
- Local recording management
- SEI message reception and handling

## Callback Method Details

### 1. Error and Warning Callbacks

#### onError() - Player Error Callback
```java
public void onError(V2TXLivePlayer player, int code, String msg, Bundle extraInfo)
```

**Description**: Triggered when a player error occurs.

**Parameters**:
- `player`: The player instance reporting the error
- `code`: Error code (see `V2TXLiveCode` enum)
- `msg`: Error message
- `extraInfo`: Additional error details

**Common Scenarios**:
- Invalid RTC stream pull parameters
- RTC stream pull timeout
- RTC stream pull server processing failure
- No available HEVC decoder

**Example**:
```java
player.setObserver(new V2TXLivePlayerObserver() {
    @Override
    public void onError(V2TXLivePlayer player, int code, String msg, Bundle extraInfo) {
        switch (code) {
            case V2TXLIVE_ERROR_INVALID_PARAMETER:
                Log.e(TAG, "Invalid RTC stream pull parameters, " + msg);
                break;
            case V2TXLIVE_ERROR_REQUEST_TIMEOUT:
                Log.e(TAG, "RTC stream pull timeout, " + msg);
                break;
            case V2TXLIVE_ERROR_SERVER_PROCESS_FAILED:
                Log.e(TAG, "RTC stream pull server processing failed, please check stream pull parameters, " + msg);
                break;
            case V2TXLIVE_ERROR_DISCONNECTED:
                Log.e(TAG, "Stream pull disconnected, " + msg);
                break;
            case V2TXLIVE_ERROR_NO_AVAILABLE_HEVC_DECODERS:
                Log.e(TAG, "No available HEVC decoder, you can switch to AVC stream for playback, " + msg);
                break;
            default:
                Log.e(TAG, "Other error, " + msg);
                break;
        }
    }
});
```

#### onWarning() - Player Warning Callback
```java
public void onWarning(V2TXLivePlayer player, int code, String msg, Bundle extraInfo)
```

**Description**: Triggered when a player warning occurs.

**Parameters**:
- `player`: The player instance reporting the warning
- `code`: Warning code (see `V2TXLiveCode` enum)
- `msg`: Warning message
- `extraInfo`: Additional warning details

**Common Scenarios**:
- Video rendering stutter
- Decoder type change

**Example**:
```java
player.setObserver(new V2TXLivePlayerObserver() {
    @Override
    public void onWarning(V2TXLivePlayer player, int code, String msg, Bundle extraInfo) {
        switch (code) {
            case V2TXLIVE_WARNING_VIDEO_BLOCK:
                Log.w(TAG, "Video rendering stutter detected");
                break;
            case V2TXLIVE_WARNING_CURRENT_DECODE_TYPE_CHANGED:
                int codec_type = extraInfo.getInt("codec_type");
                if (codec_type == 0) {
                    Log.w(TAG, "Decoder type changed to h.264, " + msg);
                } else if (codec_type == 1) {
                    Log.w(TAG, "Decoder type changed to h.265, " + msg);
                }
                break;
            default:
                Log.w(TAG, "Other warning, " + msg);
                break;
        }
    }
});
```

### 2. Connection and Status Callbacks

#### onConnected() - Connection Success Callback
```java
public void onConnected(V2TXLivePlayer player, Bundle extraInfo)
```

**Description**: Triggered when the player successfully connects to the server.

**Parameters**:
- `player`: The player instance that connected
- `extraInfo`: Connection details

**Use Cases**:
- Monitor network connection status

**Example**:
```java
player.setObserver(new V2TXLivePlayerObserver() {
    @Override
    public void onConnected(V2TXLivePlayer player, Bundle extraInfo) {
        Log.i(TAG, "Successfully connected to server");
    }
});
```

#### onVideoResolutionChanged() - Video Resolution Change Callback
```java
public void onVideoResolutionChanged(V2TXLivePlayer player, int width, int height)
```

**Description**: Triggered when the video resolution changes.

**Parameters**:
- `player`: The player instance
- `width`: New video width
- `height`: New video height

**Use Cases**:
- Adapt video rendering view
- Dynamically adjust player layout

**Example**:
```java
player.setObserver(new V2TXLivePlayerObserver() {
    @Override
    public void onVideoResolutionChanged(V2TXLivePlayer player, int width, int height) {
        Log.i(TAG, "Video stream resolution changed: width-" + width + ", height-" + height);
    }
});
```

### 3. Playback Event Callbacks

#### onVideoPlaying() - Video Playback Start Callback
```java
public void onVideoPlaying(V2TXLivePlayer player, boolean firstPlay, Bundle extraInfo)
```

**Description**: Triggered when video playback starts. For subsequent plays, this callback is paired with `onVideoLoading`.

**Parameters**:
- `player`: The player instance
- `firstPlay`: `true` if this is the first playback, otherwise `false`
- `extraInfo`: Playback details

**Use Cases**:
- Update playback status UI
- Start playback timer
- Log playback events
- Calculate time-to-first-frame

**Example**:
```java
player.setObserver(new V2TXLivePlayerObserver() {
    @Override
    public void onVideoPlaying(V2TXLivePlayer player, boolean firstPlay, Bundle extraInfo) {
        if (firstPlay) {
            // First time video starts playing
            Log.i(TAG, "First playback started");
        } else {
            // Subsequent playback, hide loading UI
            Log.i(TAG, "Playback started");
        }
    }
});
```

#### onVideoLoading() - Video Loading Callback
```java
public void onVideoLoading(V2TXLivePlayer player, Bundle extraInfo)
```

**Description**: Triggered when video data is loading.

**Parameters**:
- `player`: The player instance
- `extraInfo`: Loading status details

**Use Cases**:
- Show loading animation
- Display buffering status

**Example**:
```java
player.setObserver(new V2TXLivePlayerObserver() {
    @Override
    public void onVideoLoading(V2TXLivePlayer player, Bundle extraInfo) {
        // Video playback is loading, show loading UI
        Log.i(TAG, "Video playback loading started");
    }
});
```

#### onAudioPlaying() - Audio Playback Start Callback
```java
public void onAudioPlaying(V2TXLivePlayer player, boolean firstPlay, Bundle extraInfo)
```

**Description**: Triggered when audio playback starts.

**Parameters**:
- `player`: The player instance
- `firstPlay`: `true` if this is the first playback, otherwise `false`
- `extraInfo`: Playback details

**Use Cases**:
- Monitor audio playback status
- Handle pure audio stream playback

**Example**:
```java
player.setObserver(new V2TXLivePlayerObserver() {
    @Override
    public void onAudioPlaying(V2TXLivePlayer player, boolean firstPlay, Bundle extraInfo) {
        if (firstPlay) {
            Log.i(TAG, "First audio playback started");
        } else {
            Log.i(TAG, "Audio playback started");
        }
    }
});
```

#### onAudioLoading() - Audio Loading Callback
```java
public void onAudioLoading(V2TXLivePlayer player, Bundle extraInfo)
```

**Description**: Triggered when audio data is loading.

**Parameters**:
- `player`: The player instance
- `extraInfo`: Loading status details

**Use Cases**:
- Show loading animation
- Display buffering status

**Example**:
```java
player.setObserver(new V2TXLivePlayerObserver() {
    @Override
    public void onAudioLoading(V2TXLivePlayer player, Bundle extraInfo) {
        // Audio playback is loading
        Log.i(TAG, "Audio playback loading started");
    }
});
```

### 4. Audio/Video Data Processing Callbacks

#### onPlayoutVolumeUpdate() - Volume Update Callback
```java
public void onPlayoutVolumeUpdate(V2TXLivePlayer player, int volume)
```

**Description**: Provides real-time updates on playback volume.

**Parameters**:
- `player`: The player instance
- `volume`: Current playback volume (0-100)

**Prerequisite**: Call `enableVolumeEvaluation()` to enable volume evaluation.

**Use Cases**:
- Display real-time volume levels
- Animate audio waveform
- Detect mute status

**Example**:
```java
player.setObserver(new V2TXLivePlayerObserver() {
    @Override
    public void onPlayoutVolumeUpdate(V2TXLivePlayer player, int volume) {
        // Update audio playback volume UI
        Log.i(TAG, "Audio playback volume: " + volume);
    }
});
player.enableVolumeEvaluation(300);
```

#### onRenderVideoFrame() - Custom Video Rendering Callback
```java
public void onRenderVideoFrame(V2TXLivePlayer player, V2TXLiveVideoFrame videoFrame)
```

**Description**: Delivers video frame data for custom rendering.

**Parameters**:
- `player`: The player instance
- `videoFrame`: Video frame data (`V2TXLiveVideoFrame`)

**Prerequisite**: Call `enableObserveVideoFrame()` to enable video frame callbacks.

**Use Cases**:
- Implement custom video rendering

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

#### onPlayoutAudioFrame() - Audio Frame Callback
```java
public void onPlayoutAudioFrame(V2TXLivePlayer player, V2TXLiveAudioFrame audioFrame)
```

**Description**: Delivers audio frame data for custom processing.

**Parameters**:
- `player`: The player instance
- `audioFrame`: Audio frame data (`V2TXLiveAudioFrame`)

**Prerequisite**: Call `enableObserveAudioFrame()` to enable audio frame callbacks.

**Use Cases**:
- Implement custom audio processing

**Example**:
```java
// Enable audio frame monitoring
player.enableObserveAudioFrame(true);
player.setObserver(new V2TXLivePlayerObserver() {
    @Override
    public void onPlayoutAudioFrame(V2TXLivePlayer player, V2TXLiveAudioFrame audioFrame) {
        // Custom audio processing
    }
});
```

### 5. Statistics and Monitoring Callbacks

#### onStatisticsUpdate() - Playback Statistics Callback
```java
public void onStatisticsUpdate(V2TXLivePlayer player, V2TXLivePlayerStatistics statistics)
```

**Description**: Provides real-time playback statistics every 2 seconds.

**Parameters**:
- `player`: The player instance
- `statistics`: Playback statistics (`V2TXLivePlayerStatistics`)

**Statistics Include**:
- Video width and height
- Frame rate and bitrate
- Network status
- Buffer size
- Playback latency

**Use Cases**:
- Monitor playback quality
- Analyze performance
- Collect user experience metrics

**Example**:
```java
player.setObserver(new V2TXLivePlayerObserver() {
    @Override
    public void onStatisticsUpdate(V2TXLivePlayer player, V2TXLivePlayerStatistics statistics) {
        // Handle playback statistics
    }
});
```

### 6. Advanced Feature Callbacks

#### onSnapshotComplete() - Snapshot Completion Callback
```java
public void onSnapshotComplete(V2TXLivePlayer player, Bitmap image)
```

**Description**: Triggered when a snapshot operation completes.

**Parameters**:
- `player`: The player instance
- `image`: Captured video frame as a Bitmap

**Use Cases**:
- Save video snapshots
- Implement frame sharing

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

#### onReceiveSeiMessage() - SEI Message Callback
```java
public void onReceiveSeiMessage(V2TXLivePlayer player, int payloadType, byte[] data)
```

**Description**: Receives SEI (Supplemental Enhancement Information) messages.

**Parameters**:
- `player`: The player instance
- `payloadType`: SEI message type
- `data`: SEI message data

**Prerequisite**: Call `enableReceiveSeiMessage()` to enable SEI message reception.

**Use Cases**:
- Transmit scene information
- Deliver interactive messages

**Example**:
```java
// Enable SEI message reception
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

#### onStreamSwitched() - Stream Switch Callback
```java
public void onStreamSwitched(V2TXLivePlayer player, String url, int code)
```

**Description**: Triggered after a stream resolution switch completes via `switchStream()`.

**Parameters**:
- `player`: The player instance
- `url`: Playback URL after switching
- `code`: Switch status code (`0`: success, `-1`: timeout, `-2`: server error, `-3`: client error)

**Use Cases**:
- Monitor stream quality switching

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

### 7. Local Recording Callbacks

#### onLocalRecordBegin() - Recording Start Callback
```java
public void onLocalRecordBegin(V2TXLivePlayer player, int code, String storagePath)
```

**Description**: Triggered when a local recording task starts, after calling `startLocalRecording()`.

**Parameters**:
- `player`: The player instance
- `code`: Recording status code
- `storagePath`: Path to the recording file

**Status Codes**:
- `0`: Recording started successfully
- `-1`: Internal error
- `-2`: Invalid file extension
- `-6`: Recording already started
- `-7`: Recording file already exists
- `-8`: No write permission in recording directory

#### onLocalRecording() - Recording Progress Callback
```java
public void onLocalRecording(V2TXLivePlayer player, long durationMs, String storagePath)
```

**Description**: Reports recording progress at intervals specified by `V2TXLiveDef.V2TXLiveLocalRecordingParams.interval` in `startLocalRecording`.

**Parameters**:
- `player`: The player instance
- `durationMs`: Recorded duration in milliseconds
- `storagePath`: Path to the recording file

**Use Cases**:
- Display recording progress
- Enforce recording duration limits
- Monitor recording status

#### onLocalRecordComplete() - Recording Completion Callback
```java
public void onLocalRecordComplete(V2TXLivePlayer player, int code, String storagePath)
```

**Description**: Triggered when a recording task ends, after calling `stopLocalRecording()`.

**Parameters**:
- `player`: The player instance
- `code`: Completion status code
- `storagePath`: Path to the recording file

**Status Codes**:
- `0`: Recording completed successfully
- `-1`: Recording failed
- `-2`: Recording ended due to resolution or orientation change
- `-3`: Recording duration too short or no data captured

**Example**:
```java
player.setObserver(new V2TXLivePlayerObserver() {
    @Override
    public void onLocalRecordBegin(V2TXLivePlayer player, int code, String storagePath) {
        Log.i(TAG, "Recording started");
    }

    @Override
    public void onLocalRecording(V2TXLivePlayer player, long durationMs, String storagePath) {
        Log.i(TAG, "Recording in progress..., durationMs: " + durationMs);
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
    Log.i(TAG, "Recording request refused");
}
```

### Basic Player Callback Implementation
```java
public class MyPlayerObserver extends V2TXLivePlayerObserver {
    @Override
    public void onError(V2TXLivePlayer player, int code, String msg, Bundle extraInfo) {
        // Handle playback error
        Log.e("PlayerError", "Error code: " + code + ", Error message: " + msg);
    }
    
    @Override
    public void onConnected(V2TXLivePlayer player, Bundle extraInfo) {
        // Handle connection success
        Log.i("Player", "Successfully connected to server");
    }
    
    @Override
    public void onVideoPlaying(V2TXLivePlayer player, boolean firstPlay, Bundle extraInfo) {
        // Video playback started
        if (firstPlay) {
            Log.i("Player", "First playback started");
        }
    }
    
    @Override
    public void onStatisticsUpdate(V2TXLivePlayer player, V2TXLivePlayerStatistics statistics) {
        // Update playback statistics
        Log.d("PlayerStats", "Frame rate: " + statistics.fps + ", Bitrate: " + statistics.bitrate);
    }
}

// Set the observer
V2TXLivePlayer player = new V2TXLivePlayerImpl(context);
player.setObserver(new MyPlayerObserver());
```

### Custom Video Processing Example
```java
public class VideoProcessorObserver extends V2TXLivePlayerObserver {
    @Override
    public void onRenderVideoFrame(V2TXLivePlayer player, V2TXLiveVideoFrame videoFrame) {
        // Custom video frame processing
        // Add filters, watermarks, etc.
        processVideoFrame(videoFrame);
    }
    
    private void processVideoFrame(V2TXLiveVideoFrame frame) {
        // Video frame processing logic
    }
}

// Enable custom video frame callback
player.enableObserveVideoFrame(true);
player.setObserver(new VideoProcessorObserver());
```

### Local Recording Monitoring Example
```java
public class RecordingObserver extends V2TXLivePlayerObserver {
    @Override
    public void onLocalRecordBegin(V2TXLivePlayer player, int code, String storagePath) {
        if (code == 0) {
            Log.i("Recording", "Recording started, file path: " + storagePath);
        } else {
            Log.e("Recording", "Recording failed, error code: " + code);
        }
    }
    
    @Override
    public void onLocalRecording(V2TXLivePlayer player, long durationMs, String storagePath) {
        // Update recording progress
        updateRecordingProgress(durationMs);
    }
    
    @Override
    public void onLocalRecordComplete(V2TXLivePlayer player, int code, String storagePath) {
        if (code == 0) {
            Log.i("Recording", "Recording completed, file path: " + storagePath);
        } else {
            Log.w("Recording", "Recording ended abnormally, status code: " + code);
        }
    }
}
```

## Notes

1. **Callback Thread**: All callbacks except custom rendering are executed on the UI main thread.
2. **Performance Impact**: Custom rendering and audio processing callbacks may impact playback performance.
3. **Memory Management**: Release unused observer objects promptly to prevent memory leaks.
4. **Error Handling**: Handle error codes appropriately and provide user-friendly messages.
5. **Permission Check**: Local recording requires storage permissions and sufficient available space.