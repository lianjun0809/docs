> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/en/llms.txt
> Use this file to discover all available pages before exploring further.

# Tencent Cloud Live Streaming SDK V2TXLivePusherObserver Live Stream Pusher Callback Interface

## Feature Overview

`V2TXLivePusherObserver` defines the observer callback interface for the Tencent Cloud TRTC Live Streaming SDK pusher. This interface provides callbacks for status updates, error handling, data statistics, and custom processing during live streaming.

## File Information

- **File Path**: `v2_tx_live_pusher_observer.dart`
- **Dependencies**:
  - `v2_tx_live_code.dart` - Error code definitions
  - `v2_tx_live_def.dart` - Type definitions

## Callback Type Enumeration

### V2TXLivePusherListenerType

Lists all callback types available for the stream pusher observer:

```dart
enum V2TXLivePusherListenerType {
  // Detailed callback definitions...
}
```

## Callback Function Definition

```dart
typedef V2TXLivePusherObserver<P> = void Function(V2TXLivePusherListenerType type, P? params);
```

## Callback Type Details

### Error and Warning Callbacks

#### onError
**Purpose**: Triggered when the SDK encounters an unrecoverable error.
```dart
onError,
```
**Parameters**:
- `code`: Error code ([V2TXLiveCode])
- `msg`: Error message (String)
- `extraInfo`: Additional details (Map)

**Note**: Always handle this callback and provide appropriate UI feedback to users.

#### onWarning
**Purpose**: Triggered for non-critical issues.
```dart
onWarning,
```
**Parameters**:
- `code`: Warning code ([V2TXLiveCode])
- `msg`: Warning message (String)
- `extraInfo`: Additional details (Map)

**Note**: Used for events such as stuttering or recoverable decoding failures.

### Capture Status Callbacks

#### onCaptureFirstAudioFrame
**Purpose**: Invoked when the first audio frame is captured.
```dart
onCaptureFirstAudioFrame,
```
**Parameters**: None

#### onCaptureFirstVideoFrame
**Purpose**: Invoked when the first video frame is captured.
```dart
onCaptureFirstVideoFrame,
```
**Parameters**: None

#### onMicrophoneVolumeUpdate
**Purpose**: Reports microphone capture volume.
```dart
onMicrophoneVolumeUpdate,
```
**Parameters**:
- `volume`: Volume value (int)

### Stream Status Callbacks

#### onPushStatusUpdate
**Purpose**: Notifies about the pusher connection status.
```dart
onPushStatusUpdate,
```
**Parameters**:
- `status`: Current status (String)
- `errMsg`: Connection status message (String)
- `extraInfo`: Additional details (Map)

### Statistics Data Callback

#### onStatisticsUpdate
**Purpose**: Reports live stream pusher statistics.
```dart
onStatisticsUpdate,
```
**Parameters**:
- `appCpu`: App CPU usage (%) (int)
- `systemCpu`: System CPU usage (%) (int)
- `width`: Video width (int)
- `height`: Video height (int)
- `fps`: Frame rate (int)
- `videoBitrate`: Video bitrate (Kbps) (int)
- `audioBitrate`: Audio bitrate (Kbps) (int)

### Snapshot Callback

#### onSnapshotComplete
**Purpose**: Invoked when a snapshot is completed.
```dart
onSnapshotComplete,
```
**Parameters**:
- `image`: Captured video frame (Uint8List)

### OpenGL Environment Callbacks

#### onGLContextCreated
**Purpose**: Notifies when the SDK's internal OpenGL environment is created.
```dart
onGLContextCreated,
```
**Parameters**: None

#### onGLContextDestroyed
**Purpose**: Notifies when the SDK's internal OpenGL environment is destroyed.
```dart
onGLContextDestroyed,
```
**Parameters**: None

### Custom Processing Callback

#### onProcessVideoFrame
**Purpose**: Handles custom video frame processing.
```dart
onProcessVideoFrame,
```
**Parameters**: Video frame processing parameters

### Cloud MixTranscoding Callback

#### onSetMixTranscodingConfig
**Purpose**: Reports the result of setting cloud stream mixing MixTranscoding parameters.
```dart
onSetMixTranscodingConfig,
```
**Parameters**:
- `errCode`: Error code ([V2TXLiveCode])
- `errMsg`: Error message (String)

### Screen Sharing Callbacks

#### onScreenCaptureStarted
**Purpose**: Notifies when screen sharing starts.
```dart
onScreenCaptureStarted,
```
**Parameters**: None

#### onScreenCaptureStopped
**Purpose**: Notifies when screen sharing stops.
```dart
onScreenCaptureStopped,
```
**Parameters**: None

## Code Examples

### Basic Callback Setup

```dart
import 'v2_tx_live_pusher_observer.dart';
import 'v2_tx_live_pusher.dart';
import 'v2_tx_live_code.dart';

// Create pusher instance
V2TXLivePusher pusher = V2TXLivePusher(V2TXLiveMode.V2TXLiveModeRTC);

// Set observer callback
pusher.setObserver((type, params) {
  switch (type) {
    case V2TXLivePusherListenerType.onError:
      print('Stream error: code=${params.code}, msg=${params.msg}');
      // Display error prompt to user
      break;
      
    case V2TXLivePusherListenerType.onWarning:
      print('Stream warning: code=${params.code}, msg=${params.msg}');
      break;
      
    case V2TXLivePusherListenerType.onCaptureFirstAudioFrame:
      print('First audio frame captured');
      break;
      
    case V2TXLivePusherListenerType.onCaptureFirstVideoFrame:
      print('First video frame captured');
      break;
      
    case V2TXLivePusherListenerType.onMicrophoneVolumeUpdate:
      print('Microphone volume: ${params.volume}');
      break;
      
    case V2TXLivePusherListenerType.onPushStatusUpdate:
      print('Stream status update: status=${params.status}, errMsg=${params.errMsg}');
      break;
      
    case V2TXLivePusherListenerType.onStatisticsUpdate:
      print('Statistics: appCpu=${params.appCpu}%, systemCpu=${params.systemCpu}%, '
            'width=${params.width}, height=${params.height}, fps=${params.fps}, '
            'videoBitrate=${params.videoBitrate}Kbps, audioBitrate=${params.audioBitrate}Kbps');
      break;
      
    case V2TXLivePusherListenerType.onSnapshotComplete:
      print('Snapshot complete, image data size: ${params.image.length} bytes');
      break;
      
    case V2TXLivePusherListenerType.onScreenCaptureStarted:
      print('Screen sharing started');
      break;
      
    case V2TXLivePusherListenerType.onScreenCaptureStopped:
      print('Screen sharing stopped');
      break;
      
    default:
      break;
  }
});
```

### Advanced Callback Usage

```dart
// OpenGL environment callback handling
pusher.setObserver((type, params) {
  switch (type) {
    case V2TXLivePusherListenerType.onGLContextCreated:
      print('OpenGL environment created, you can set up custom rendering');
      break;
      
    case V2TXLivePusherListenerType.onGLContextDestroyed:
      print('OpenGL environment destroyed, clean up related resources');
      break;
      
    case V2TXLivePusherListenerType.onProcessVideoFrame:
      // Custom video processing logic
      // params contains video frame data, you can apply beauty filters, effects, etc.
      break;
      
    case V2TXLivePusherListenerType.onSetMixTranscodingConfig:
      if (params.errCode == V2TXLiveCode.V2TXLIVE_OK) {
        print('Cloud stream mixing MixTranscoding configuration succeeded');
      } else {
        print('Cloud stream mixing MixTranscoding configuration failed: ${params.errMsg}');
      }
      break;
      
    default:
      break;
  }
});
```

## Best Practices for Callback Handling

### Error Handling

```dart
case V2TXLivePusherListenerType.onError:
  // Handle different errors based on error code
  switch (params.code) {
    case V2TXLiveCode.V2TXLIVE_ERROR_NET_DISCONNECT:
      // Network disconnected, prompt user to check network
      showNetworkErrorDialog();
      break;
    case V2TXLiveCode.V2TXLIVE_ERROR_CAMERA_START_FAILED:
      // Camera failed to start, check permissions
      checkCameraPermission();
      break;
    default:
      // Other error handling
      showGenericError(params.msg);
      break;
  }
  break;
```

### Performance Monitoring

```dart
case V2TXLivePusherListenerType.onStatisticsUpdate:
  // Monitor performance metrics
  if (params.appCpu > 80) {
    print('App CPU usage is too high, optimization recommended');
  }
  if (params.fps < 15) {
    print('Frame rate is too low, may affect live stream quality');
  }
  break;
```

### Status Management

```dart
case V2TXLivePusherListenerType.onPushStatusUpdate:
  // Update UI based on stream status
  switch (params.status) {
    case 'CONNECTING':
      updateUIState('Connecting...');
      break;
    case 'CONNECTED':
      updateUIState('Streaming');
      break;
    case 'DISCONNECTED':
      updateUIState('Connection lost');
      break;
  }
  break;
```

## Notes

1. **Always handle error callbacks**: The `onError` callback reports unrecoverable errors. Provide clear feedback to users.
2. **Threading**: All callbacks run on non-UI threads. Switch to the UI thread before updating the interface.
3. **Performance**: Avoid heavy operations in callbacks to prevent streaming performance issues.
4. **Resource management**: Manage OpenGL-related resources carefully throughout their lifecycle.
5. **Snapshot data**: The image data from `onSnapshotComplete` can be large. Release it promptly after use.
6. **Custom processing**: When processing video frames in `onProcessVideoFrame`, monitor performance impact.