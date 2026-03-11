> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/en/llms.txt
> Use this file to discover all available pages before exploring further.

# Tencent Cloud Live Streaming SDK V2TXLivePusherObserver Live Stream Pusher Callback Interface

## Feature Overview

`V2TXLivePusherObserver` provides callback methods for the stream pusher in the Tencent Cloud Live Streaming SDK. Implement this interface to receive real-time status updates and event notifications from the stream pusher. With these callbacks, you can monitor streaming health, handle events, collect statistics, and manage advanced features.

**File Path**: `com/tencent/live2/V2TXLivePusherObserver.java`

**Core Features**:
- Stream pusher status monitoring (errors, warnings, connection updates)
- Audio and video capture event notifications
- Streaming statistics and performance metrics
- Custom audio and video processing
- Local recording management
- Screen sharing status monitoring
- Cloud stream mixing (MixTranscoding) event handling

## Callback Method Details

### 1. Error and Warning Callbacks

#### onError() - Stream Pusher Error Notification
```java
public void onError(int code, String msg, Bundle extraInfo)
```

**Purpose**: Notifies when the stream pusher encounters an error.

**Parameters**:
- `code`: Error code. See `V2TXLiveCode` enum.
- `msg`: Error description.
- `extraInfo`: Additional details about the error.

**Typical Scenarios**:
- Network connection failure
- Invalid stream URL
- Encoder errors
- Streaming permission issues

**Example**:
```java
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onError(int code, String msg, Bundle extraInfo) {
        switch (code) {
            case V2TXLIVE_ERROR_REQUEST_TIMEOUT:
                Log.e(TAG, "Stream connection timed out");
                break;
            case V2TXLIVE_ERROR_SERVER_PROCESS_FAILED:
                Log.e(TAG, "Stream server processing failed");
                break;
            default:
                Log.e(TAG, "Other error: " + msg);
                break;
        }
    }
});
```

#### onWarning() - Stream Pusher Warning Notification
```java
public void onWarning(int code, String msg, Bundle extraInfo)
```

**Purpose**: Notifies when the stream pusher encounters a warning.

**Parameters**:
- `code`: Warning code. See `V2TXLiveCode` enum.
- `msg`: Warning description.
- `extraInfo`: Additional details.

**Typical Scenarios**:
- Network quality degradation
- Encoding delays
- Buffer underruns

**Example**:
```java
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onWarning(int code, String msg, Bundle extraInfo) {
        switch (code) {
            case V2TXLiveCode.V2TXLIVE_WARNING_CURRENT_ENCODE_TYPE_CHANGED:
                int codec_type = extraInfo.getInt("codec_type");
                if (codec_type == 0) {
                    Log.w(TAG, "Encoder switched to h.264, " + msg);
                } else if (codec_type == 1) {
                    Log.w(TAG, "Encoder switched to h.265, " + msg);
                }
                break;
            case V2TXLiveCode.V2TXLIVE_WARNING_NETWORK_BUSY:
                Log.w(TAG, "Network busy, " + msg);
                break;
            case V2TXLiveCode.V2TXLIVE_WARNING_CAMERA_START_FAILED:
                Log.w(TAG, "Camera failed to start, " + msg);
                break;
            case V2TXLiveCode.V2TXLIVE_WARNING_CAMERA_NO_PERMISSION:
                Log.w(TAG, "Camera permission denied, " + msg);
                break;
            case V2TXLiveCode.V2TXLIVE_WARNING_CAMERA_OCCUPIED:
                Log.w(TAG, "Camera is occupied, " + msg);
                break;
            case V2TXLIVE_WARNING_SCREEN_CAPTURE_START_FAILED:
                Log.w(TAG, "Screen capture failed to start, " + msg);
                break;
            case V2TXLIVE_WARNING_SCREEN_CAPTURE_NOT_SUPPORTED:
                Log.w(TAG, "Screen capture not supported, " + msg);
                break;
            case V2TXLIVE_WARNING_SCREEN_CAPTURE_INTERRUPTED:
                Log.w(TAG, "Screen capture interrupted, " + msg);
                break;
            case V2TXLIVE_WARNING_MICROPHONE_START_FAILED:
                Log.w(TAG, "Microphone failed to start, " + msg);
                break;
            case V2TXLIVE_WARNING_MICROPHONE_NO_PERMISSION:
                Log.w(TAG, "Microphone permission denied, " + msg);
                break;
            case V2TXLIVE_WARNING_MICROPHONE_OCCUPIED:
                Log.w(TAG, "Microphone is occupied, " + msg);
                break;
            default:
                Log.w(TAG, "Other warning: " + msg);
                break;
        }
    }
});
```

### 2. Connection and Status Callbacks

#### onPushStatusUpdate() - Stream Pusher Connection Status
```java
public void onPushStatusUpdate(V2TXLivePushStatus status, String msg, Bundle extraInfo)
```

**Purpose**: Reports changes in the stream pusher's connection status.

**Parameters**:
- `status`: Connection status (`V2TXLivePushStatus`)
- `msg`: Status details
- `extraInfo`: Additional information

**Status Values**:
- `V2TXLivePushStatus.V2TXLivePushStatusDisconnected`: Disconnected
- `V2TXLivePushStatus.V2TXLivePushStatusConnecting`: Connecting
- `V2TXLivePushStatus.V2TXLivePushStatusConnectSuccess`: Connected
- `V2TXLivePushStatus.V2TXLivePushStatusReconnecting`: Reconnecting

**Typical Scenarios**:
- Real-time streaming status monitoring
- Connection retry logic
- UI status updates

**Example**:
```java
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onPushStatusUpdate(V2TXLivePushStatus status, String msg, Bundle extraInfo) {
        switch (status) {
            case V2TXLivePushStatusConnectSuccess:
                Log.i(TAG, "Stream connected successfully");
                break;
            case V2TXLivePushStatusConnecting:
                Log.i(TAG, "Connecting to stream...");
                break;
            case V2TXLivePushStatusReconnecting:
                Log.w(TAG, "Reconnecting to stream...");
                break;
            case V2TXLivePushStatusDisconnected:
                Log.e(TAG, "Stream disconnected");
                break;
        }
    }
});
```

### 3. Capture Event Callbacks

#### onCaptureFirstAudioFrame() - First Audio Frame Notification
```java
public void onCaptureFirstAudioFrame()
```

**Purpose**: Notifies when the first audio frame is captured.

**Typical Scenarios**:
- Confirm audio capture started
- Update audio UI status
- Initialize audio processing

**Example**:
```java
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onCaptureFirstAudioFrame() {
        Log.i(TAG, "Audio capture started. First audio frame received.");
        // Update UI to indicate audio capture
    }
});
```

#### onCaptureFirstVideoFrame() - First Video Frame Notification
```java
public void onCaptureFirstVideoFrame()
```

**Purpose**: Notifies when the first video frame is captured.

**Typical Scenarios**:
- Confirm video capture started
- Update video UI status
- Initialize video processing

**Example**:
```java
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onCaptureFirstVideoFrame() {
        Log.i(TAG, "Video capture started. First video frame received.");
        // Update UI to indicate video capture
    }
});
```

#### onMicrophoneVolumeUpdate() - Microphone Capture Volume
```java
public void onMicrophoneVolumeUpdate(int volume)
```

**Purpose**: Reports real-time microphone capture volume.

**Parameters**:
- `volume`: Volume level (0-100)

**Prerequisite**: Call `enableVolumeEvaluation()` to receive volume updates.

**Typical Scenarios**:
- Display live volume levels
- Animate audio waveform
- Detect mute state

**Example**:
```java
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onMicrophoneVolumeUpdate(int volume) {
        // Update volume indicator
        
        // Detect mute state
        if (volume < 5) {
            Log.d(TAG, "Mute detected");
        }
    }
});
// Enable volume evaluation
pusher.enableVolumeEvaluation(300);
```

### 4. Audio/Video Data Processing Callbacks

#### onProcessAudioFrame() - Audio Frame Processing
```java
public void onProcessAudioFrame(V2TXLiveDef.V2TXLiveAudioFrame frame)
```

**Purpose**: Provides locally captured audio data after pre-processing, audio effects, and background music mixing.

**Parameters**:
- `frame`: PCM audio data frame

**Technical Details**:
- Frame duration: 0.02s (20ms)
- Format: PCM
- Byte length: `Sample rate × frame duration × Audio Channel count × sample bit width`
- Default: 48000 sample rate, mono, 16-bit = 1920 bytes

**Important Notes**:
1. Avoid time-consuming operations in this callback.
2. The SDK processes one audio frame every 20ms; exceeding this time may cause audio issues.
3. Audio data is readable and writable; you can modify it synchronously but must keep processing time under control.

**Typical Scenarios**:
- Custom audio processing
- Applying audio effects
- Audio analysis and statistics

**Example**:
```java
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onProcessAudioFrame(V2TXLiveDef.V2TXLiveAudioFrame frame) {
        // Apply custom audio processing (e.g., reverb)
        
        // Track processed frames
        audioFrameCount++;
        if (audioFrameCount % 50 == 0) {
            Log.d(TAG, "Processed audio frames: " + audioFrameCount);
        }
    }
});
```

#### onProcessVideoFrame() - Custom Video Frame Processing
```java
public int onProcessVideoFrame(V2TXLiveVideoFrame srcFrame, V2TXLiveVideoFrame dstFrame)
```

**Purpose**: Enables custom video frame processing.

**Parameters**:
- `srcFrame`: Original video frame
- `dstFrame`: Processed video frame

**Return Value**: 0 for success

**Prerequisite**: Call `enableCustomVideoProcess()` to enable custom video processing.

**Usage Examples**:

**Case 1: Beauty component generates a new texture**
```java
@Override
public void onGLContextCreated() {
    mFURenderer.onSurfaceCreated();
    mFURenderer.setUseTexAsync(true);
}

@Override
public int onProcessVideoFrame(V2TXLiveVideoFrame srcFrame, V2TXLiveVideoFrame dstFrame) {
    dstFrame.texture.textureId = mFURenderer.onDrawFrameSingleInput(
                        srcFrame.texture.textureId, srcFrame.width, srcFrame.height);
    return 0;
}

@Override
public void onGLContextDestroyed() {
    mFURenderer.onSurfaceDestroyed();
}
```

**Case 2: Beauty component does not generate a new texture**
```java
int onProcessVideoFrame(V2TXLiveVideoFrame srcFrame, V2TXLiveVideoFrame dstFrame) {
    thirdparty_process(srcFrame.texture.textureId, srcFrame.width, srcFrame.height, dstFrame.texture.textureId);
    return 0;
}
```

### 5. OpenGL Environment Callbacks

#### onGLContextCreated() - OpenGL Environment Created
```java
public void onGLContextCreated()
```

**Purpose**: Notifies when the SDK's internal OpenGL environment is created.

**Typical Scenarios**:
- Initialize beauty components
- Set up video processing modules
- Create OpenGL resources

**Example**:
```java
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onGLContextCreated() {
        Log.i(TAG, "OpenGL environment created");
        // Initialize beauty component
        if (mBeautyProcessor != null) {
            mBeautyProcessor.initGL();
        }
    }
});
```

#### onGLContextDestroyed() - OpenGL Environment Destroyed
```java
public void onGLContextDestroyed()
```

**Purpose**: Notifies when the SDK's internal OpenGL environment is destroyed.

**Typical Scenarios**:
- Clean up beauty components
- Release video processing modules
- Free OpenGL resources

**Example**:
```java
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onGLContextDestroyed() {
        Log.i(TAG, "OpenGL environment destroyed");
        // Release beauty component resources
        if (mBeautyProcessor != null) {
            mBeautyProcessor.releaseGL();
        }
    }
});
```

### 6. Statistics and Monitoring Callbacks

#### onStatisticsUpdate() - Streaming Statistics
```java
public void onStatisticsUpdate(V2TXLivePusherStatistics statistics)
```

**Purpose**: Provides real-time streaming statistics every 2 seconds.

**Parameters**:
- `statistics`: Streaming statistics (`V2TXLivePusherStatistics`)

**Included Metrics**:
- Video resolution (width/height)
- Frame rate and bitrate
- Network status
- Buffer size
- Streaming latency

**Typical Scenarios**:
- Monitor streaming quality
- Analyze performance
- Collect user experience metrics

**Example**:
```java
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onStatisticsUpdate(V2TXLivePusherStatistics statistics) {
        Log.d(TAG, "Streaming stats - FPS: " + statistics.fps + 
                  ", Bitrate: " + statistics.videoBitrate + 
                  ", Resolution: " + statistics.width + "x" + statistics.height);
        
        // Update streaming quality display
    }
});
```

### 7. Advanced Feature Callbacks

#### onSnapshotComplete() - Snapshot Completion
```java
public void onSnapshotComplete(Bitmap image)
```

**Purpose**: Notifies when a video snapshot is captured.

**Parameters**:
- `image`: Bitmap of the captured frame

**Typical Scenarios**:
- Save video snapshots
- Share frames
- Preserve evidence

**Example**:
```java
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onSnapshotComplete(Bitmap image) {
        Log.i(TAG, "Snapshot complete, image size: " + image.getWidth() + "x" + image.getHeight());
        
        // Save to album
        
        // Show snapshot preview
    }
});

// Trigger snapshot
pusher.snapshot();
```

#### onSetMixTranscodingConfig() - Cloud Stream Mixing (MixTranscoding)
```java
public void onSetMixTranscodingConfig(int code, String msg)
```

**Purpose**: Reports the result of setting cloud stream mixing (MixTranscoding) parameters. Supported only by RTC protocol.

**Parameters**:
- `code`: 0 for success, other values indicate failure
- `msg`: Error details

**Related API**: `setMixTranscodingConfig()`

**Typical Scenarios**:
- Monitor MixTranscoding status
- Handle MixTranscoding failures
- Track multi-stream composition

**Example**:
```java
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onSetMixTranscodingConfig(int code, String msg) {
        if (code == 0) {
            Log.i(TAG, "Cloud stream mixing (MixTranscoding) configuration succeeded");
        } else {
            Log.e(TAG, "Cloud stream mixing (MixTranscoding) configuration failed: " + msg);
        }
    }
});

// Configure cloud stream mixing
V2TXLiveDef.V2TXLiveTranscodingConfig config = new V2TXLiveDef.V2TXLiveTranscodingConfig();
// ... configure mixing parameters
pusher.setMixTranscodingConfig(config);
```

#### onVoiceActivityDetectionUpdate() - Voice Activity Detection
```java
public void onVoiceActivityDetectionUpdate(boolean active)
```

**Purpose**: Reports voice activity detection status.

**Parameters**:
- `active`: True if voice activity is detected, false otherwise

**Prerequisite**: Call `enableVoiceActivityDetection()` to enable this feature.

**Typical Scenarios**:
- Voice activity detection
- Smart mute handling
- Voice recognition

**Example**:
```java
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onVoiceActivityDetectionUpdate(boolean active) {
        if (active) {
            Log.i(TAG, "Voice activity detected");
            // Show speaking indicator
            showSpeakingIndicator(true);
        } else {
            Log.i(TAG, "Voice activity stopped");
            // Hide speaking indicator
            showSpeakingIndicator(false);
        }
    }
});

// Enable voice activity detection
pusher.enableVoiceActivityDetection(true);
```

### 8. Screen Sharing Callbacks

#### onScreenCaptureStarted() - Screen Sharing Started
```java
public void onScreenCaptureStarted()
```

**Purpose**: Notifies when screen sharing starts.

**Typical Scenarios**:
- Monitor screen sharing status
- Update UI
- Confirm permissions

**Example**:
```java
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onScreenCaptureStarted() {
        Log.i(TAG, "Screen sharing started");
        // Update UI to show screen sharing status
        updateScreenShareStatus(true);
    }
});
```

#### onScreenCaptureStopped() - Screen Sharing Stopped
```java
public void onScreenCaptureStopped(int reason)
```

**Purpose**: Notifies when screen sharing stops.

**Parameters**:
- `reason`: Reason code
  - `0`: User stopped manually
  - `1`: Interrupted by system (iOS), window closed (Mac/Windows)
  - `2`: Display status changed (Windows only)

**Typical Scenarios**:
- Handle screen sharing exceptions
- Restore UI status
- Handle permission loss

**Example**:
```java
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onScreenCaptureStopped(int reason) {
        Log.i(TAG, "Screen sharing stopped, reason: " + reason);
        
        switch (reason) {
            case 0:
                Log.i(TAG, "User manually stopped screen sharing");
                break;
            case 1:
                Log.w(TAG, "Screen sharing interrupted by system");
                break;
            case 2:
                Log.w(TAG, "Display status change caused screen sharing to stop");
                break;
        }
        
        // Update UI to show screen sharing status
        updateScreenShareStatus(false);
    }
});
```

### 9. Local Recording Callbacks

#### onLocalRecordBegin() - Local Recording Started
```java
public void onLocalRecordBegin(int code, String storagePath)
```

**Purpose**: Notifies when a local recording task starts.

**Parameters**:
- `code`: Status code
  - `0`: Recording started successfully
  - `-1`: Internal error
  - `-2`: Invalid file extension
  - `-6`: Recording already started; stop first
  - `-7`: File already exists; delete first
  - `-8`: No write permission for directory
- `storagePath`: Recording file path

**Related API**: `startLocalRecording()`

**Example**:
```java
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onLocalRecordBegin(int code, String storagePath) {
        if (code == 0) {
            Log.i(TAG, "Local recording started, file path: " + storagePath);
            // Show recording status
            showRecordingStatus(true);
        } else {
            Log.e(TAG, "Failed to start local recording, error code: " + code);
            // Handle recording start failure
            handleRecordingError(code);
        }
    }
});
```

#### onLocalRecording() - Local Recording Progress
```java
public void onLocalRecording(long durationMs, String storagePath)
```

**Purpose**: Reports recording progress during an active recording task.

**Parameters**:
- `durationMs`: Recording duration (milliseconds)
- `storagePath`: Recording file path

**Default Behavior**: This event only triggers if a callback interval is set when calling `startLocalRecording()`.

**Typical Scenarios**:
- Display recording progress
- Enforce recording duration limits
- Monitor recording status

**Example**:
```java
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onLocalRecording(long durationMs, String storagePath) {
        // Update recording progress display
        updateRecordingProgress(durationMs);
        
        // Stop recording if duration limit reached (e.g., 1 hour)
        if (durationMs >= 3600000) {
            Log.w(TAG, "Recording duration limit reached, stopping recording automatically");
            pusher.stopLocalRecording();
        }
    }
});
```

#### onLocalRecordComplete() - Local Recording Completed
```java
public void onLocalRecordComplete(int code, String storagePath)
```

**Purpose**: Notifies when a recording task ends.

**Parameters**:
- `code`: Status code
  - `0`: Recording ended successfully
  - `-1`: Recording failed
  - `-2`: Ended due to resolution/orientation change
  - `-3`: Duration too short or no video/audio captured
- `storagePath`: Recording file path

**Related API**: `stopLocalRecording()`

**Example**:
```java
pusher.setObserver(new V2TXLivePusherObserver() {
    @Override
    public void onLocalRecordComplete(int code, String storagePath) {
        if (code == 0) {
            Log.i(TAG, "Local recording completed, file path: " + storagePath);
            // Show recording completion status
            showRecordingComplete(storagePath);
        } else {
            Log.w(TAG, "Local recording ended abnormally, status code: " + code);
            // Handle abnormal recording end
            handleRecordingAbnormalEnd(code);
        }
    }
});
```

## Code Examples

### Basic Stream Pusher Callback Implementation
```java
public class MyPusherObserver extends V2TXLivePusherObserver {
    @Override
    public void onError(int code, String msg, Bundle extraInfo) {
        // Handle streaming errors
        Log.e("PusherError", "Error code: " + code + ", Error message: " + msg);
    }
    
    @Override
    public void onPushStatusUpdate(V2TXLivePushStatus status, String msg, Bundle extraInfo) {
        // Monitor streaming status
        switch (status) {
            case CONNECT_SUCCESS:
                Log.i("Pusher", "Stream connected successfully");
                break;
            case DISCONNECTED:
                Log.w("Pusher", "Stream disconnected");
                break;
        }
    }
    
    @Override
    public void onCaptureFirstVideoFrame() {
        // Video capture started
        Log.i("Pusher", "Video capture started");
    }
    
    @Override
    public void onStatisticsUpdate(V2TXLivePusherStatistics statistics) {
        // Update streaming statistics
        Log.d("PusherStats", "FPS: " + statistics.fps + ", Bitrate: " + statistics.bitrate);
    }
}

// Set callback observer
V2TXLivePusher pusher = new V2TXLivePusherImpl(context);
pusher.setObserver(new MyPusherObserver());
```

### Custom Video Processing Example
```java
public class VideoProcessorObserver extends V2TXLivePusherObserver {
    private BeautyProcessor mBeautyProcessor;
    
    @Override
    public void onGLContextCreated() {
        // Initialize beauty component when OpenGL environment is created
        mBeautyProcessor = new BeautyProcessor();
        mBeautyProcessor.init();
    }
    
    @Override
    public int onProcessVideoFrame(V2TXLiveVideoFrame srcFrame, V2TXLiveVideoFrame dstFrame) {
        // Custom video frame processing (beauty, filters, etc.)
        if (mBeautyProcessor != null) {
            return mBeautyProcessor.processFrame(srcFrame, dstFrame);
        }
        return 0;
    }
    
    @Override
    public void onGLContextDestroyed() {
        // Clean up resources when OpenGL environment is destroyed
        if (mBeautyProcessor != null) {
            mBeautyProcessor.release();
            mBeautyProcessor = null;
        }
    }
}

// Enable custom video processing
pusher.enableCustomVideoProcess(true);
pusher.setObserver(new VideoProcessorObserver());
```

### Local Recording Monitoring Example
```java
public class RecordingObserver extends V2TXLivePusherObserver {
    @Override
    public void onLocalRecordBegin(int code, String storagePath) {
        if (code == 0) {
            Log.i("Recording", "Recording started, file path: " + storagePath);
        } else {
            Log.e("Recording", "Recording failed, error code: " + code);
        }
    }
    
    @Override
    public void onLocalRecording(long durationMs, String storagePath) {
        // Update recording progress
        updateRecordingProgress(durationMs);
    }
    
    @Override
    public void onLocalRecordComplete(int code, String storagePath) {
        if (code == 0) {
            Log.i("Recording", "Recording completed, file path: " + storagePath);
        } else {
            Log.w("Recording", "Recording ended abnormally, status code: " + code);
        }
    }
}
```

## Notes

1. **Callback Threading**: Except for custom pre-processing callbacks, all other callback methods run on non-UI threads. Ensure thread safety.
2. **Performance Considerations**: Custom audio/video processing callbacks may impact streaming performance. Keep processing time minimal.
3. **Memory Management**: Release observer objects promptly when no longer needed to prevent memory leaks.
4. **Error Handling**: Handle all error codes appropriately and provide user-friendly feedback.
5. **Permission Checks**: Ensure proper permissions for screen sharing and local recording.
6. **OpenGL Resource Management**: Manage OpenGL resource creation and destruction carefully when using custom video processing.

## Related APIs

- `V2TXLivePusher`: Main stream pusher interface
- `V2TXLiveCode`: Error and status code definitions
- `V2TXLiveDef`: Data structures and enums
- `V2TXLivePremier`: SDK global management interface