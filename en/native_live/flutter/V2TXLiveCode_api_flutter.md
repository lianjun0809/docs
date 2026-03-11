> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/en/llms.txt
> Use this file to discover all available pages before exploring further.

# Tencent Cloud Live Streaming SDK V2TXLiveCode Error Code Documentation

## Overview

`V2TXLiveCode` defines error and warning codes for the Tencent Cloud Live Streaming (CSS) SDK on Flutter. This file organizes error codes and provides detailed descriptions for features such as stream publishing, playback, stream mixing, and recording.

**File Path**: `v2_tx_live_code.dart`  
**Platform Support**: Flutter  
**Total Error Codes**: 20 core error and warning codes

## 📋 Table of Contents

### 1. [Error Code Categories](#错误码分类)
### 2. [General Error Codes](#通用错误码)
### 3. [Network-Related Warning Codes](#网络相关警告码)
### 4. [Camera-Related Warning Codes](#摄像头相关警告码)
### 5. [Microphone-Related Warning Codes](#麦克风相关警告码)
### 6. [Screen Sharing Warning Codes](#屏幕分享相关警告码)
### 7. [Codec Warning Codes](#编解码相关警告码)

## 1. Error Code Categories

### 🎯 Error Code Statistics

| Category                      | Number of Codes | Main Functionality                        |
|-------------------------------|----------------|-------------------------------------------|
| General Error Codes           | 9              | API calls, parameter validation, permission checks |
| Network-Related Warning Codes | 2              | Network status, playback stuttering monitoring     |
| Camera-Related Warning Codes  | 3              | Camera device status monitoring                   |
| Microphone-Related Warning Codes | 3           | Microphone device status monitoring               |
| Screen Sharing Warning Codes  | 3              | Screen sharing feature status monitoring          |
| Codec Warning Codes           | 2              | Audio/video codec status monitoring               |

### 🔧 Technical Highlights

- **Hierarchical Categorization**: Error codes are grouped by functional module.
- **Detailed Descriptions**: Each error code includes clear explanations and usage scenarios.
- **Platform Adaptation**: Error codes are tailored for the Flutter platform.
- **Debug-Friendly**: Each code provides actionable explanations and troubleshooting tips.

## Type Definition

```dart
typedef V2TXLiveCode = int;
```

`V2TXLiveCode` is an alias for the `int` type, representing all error and warning codes.

## Success Code

| Code              | Value | Description          |
|-------------------|-------|----------------------|
| `V2TXLIVE_OK`     | 0     | Operation succeeded  |

## 2. General Error Codes

### ✅ V2TXLIVE_OK - Operation Succeeded

```dart
static const int V2TXLIVE_OK = 0;
```

**Meaning**: No error occurred; the operation completed successfully.

**Typical Scenarios**:
- API call returns successfully.
- Operation completes as expected.
- Status check passes.

### ❌ V2TXLIVE_ERROR_FAILED - General Error

```dart
static const int V2TXLIVE_ERROR_FAILED = -1;
```

**Meaning**: Unclassified general error.

**Possible Causes**:
- Internal processing exception.

### ❌ V2TXLIVE_ERROR_INVALID_PARAMETER - Invalid Parameter

```dart
static const int V2TXLIVE_ERROR_INVALID_PARAMETER = -2;
```

**Meaning**: Invalid parameters were provided in the API call.

**Common Causes**:
- Incorrect stream publishing URL format.
- Unsupported parameter values.

### ❌ V2TXLIVE_ERROR_REFUSED - API Call Refused

```dart
static const int V2TXLIVE_ERROR_REFUSED = -3;
```

**Meaning**: The API call was refused.

**Possible Causes**:
- Incorrect call timing.

### ❌ V2TXLIVE_ERROR_NOT_SUPPORTED - API Not Supported

```dart
static const int V2TXLIVE_ERROR_NOT_SUPPORTED = -4;
```

**Meaning**: The API is not supported.

**Common Causes**:
- Feature unsupported on the current platform.
- SDK version is outdated.
- Hardware does not support the feature.

### ❌ V2TXLIVE_ERROR_INVALID_LICENSE - Invalid License

```dart
static const int V2TXLIVE_ERROR_INVALID_LICENSE = -5;
```

**Meaning**: License is invalid; operation failed.

**Possible Causes**:
- License file not set.
- License expired.
- License does not match the package name.

### ❌ V2TXLIVE_ERROR_REQUEST_TIMEOUT - Request Timeout

```dart
static const int V2TXLIVE_ERROR_REQUEST_TIMEOUT = -6;
```

**Meaning**: Server request timed out.

**Common Causes**:
- Unstable network connection.
- Slow server response.

### ❌ V2TXLIVE_ERROR_SERVER_PROCESS_FAILED - Server Processing Failed

```dart
static const int V2TXLIVE_ERROR_SERVER_PROCESS_FAILED = -7;
```

**Meaning**: The server failed to process the request.

**Possible Causes**:
- Internal server error.
- Malformed request.
- Insufficient server resources.

### ❌ V2TXLIVE_ERROR_DISCONNECTED - Connection Disconnected

```dart
static const int V2TXLIVE_ERROR_DISCONNECTED = -8;
```

**Meaning**: Network connection lost.

**Common Causes**:
- Network disconnected during stream publishing.
- Network disconnected during playback.

### ❌ V2TXLIVE_ERROR_NO_AVAILABLE_HEVC_DECODERS - No Available HEVC Decoders

```dart
static const int V2TXLIVE_ERROR_NO_AVAILABLE_HEVC_DECODERS = -2304;
```

**Meaning**: No available HEVC decoder found.

**Possible Causes**:
- Device does not support HEVC Hardware Decoding.
- HEVC decoder initialization failed.
- System version is too low.

## 3. Network-Related Warning Codes

### ⚠️ V2TXLIVE_WARNING_NETWORK_BUSY - Poor Network Condition

```dart
static const int V2TXLIVE_WARNING_NETWORK_BUSY = 1101;
```

**Meaning**: Network is congested; upstream bandwidth is too low and upload data is blocked.

**Possible Causes**:
- Insufficient upstream bandwidth.
- Severe network jitter.
- Data packet transmission blocked.

**Troubleshooting Tips**:
- Check network connection status.
- Lower video bitrate or resolution.
- Switch to a more stable network.

### ⚠️ V2TXLIVE_WARNING_VIDEO_BLOCK - Video Playback Stuttering

```dart
static const int V2TXLIVE_WARNING_VIDEO_BLOCK = 2105;
```

**Meaning**: Video playback is stuttering.

**Possible Causes**:
- Insufficient downstream bandwidth.
- Poor video decoder performance.
- Device CPU overload.

**Troubleshooting Tips**:
- Check network quality.
- Lower video resolution or frame rate.
- Optimize player decoding performance.

## 4. Camera-Related Warning Codes

### ⚠️ V2TXLIVE_WARNING_CAMERA_START_FAILED - Camera Start Failed

```dart
static const int V2TXLIVE_WARNING_CAMERA_START_FAILED = -1301;
```

**Meaning**: Camera failed to start.

**Possible Causes**:
- Camera hardware malfunction.
- Camera driver error.
- Insufficient system resources.

**Troubleshooting Tips**:
- Check camera hardware status.
- Restart the app or device.
- Verify system permissions.

### ⚠️ V2TXLIVE_WARNING_CAMERA_OCCUPIED - Camera Occupied

```dart
static const int V2TXLIVE_WARNING_CAMERA_OCCUPIED = -1316;
```

**Meaning**: Camera is currently in use; try switching to another camera.

**Possible Causes**:
- Another app is using the camera.
- System camera app is active.
- Video call app is occupying the camera.

**Troubleshooting Tips**:
- Close other apps using the camera.
- Switch to a different available camera.
- Wait for camera resources to be released.

### ⚠️ V2TXLIVE_WARNING_CAMERA_NO_PERMISSION - Camera Permission Not Granted

```dart
static const int V2TXLIVE_WARNING_CAMERA_NO_PERMISSION = -1314;
```

**Meaning**: Camera access not authorized, typically on mobile devices due to denied permission.

**Possible Causes**:
- User denied camera permission.
- App did not request camera permission.
- Permission revoked by system or user.

**Troubleshooting Tips**:
- Check and request camera permission.
- Guide users to enable camera permissions.
- Provide instructions for requesting permissions.

## 5. Microphone-Related Warning Codes

### ⚠️ V2TXLIVE_WARNING_MICROPHONE_START_FAILED - Microphone Start Failed

```dart
static const int V2TXLIVE_WARNING_MICROPHONE_START_FAILED = -1302;
```

**Meaning**: Microphone failed to start.

**Possible Causes**:
- Microphone hardware malfunction.
- Audio driver error.
- System audio service failure.

**Troubleshooting Tips**:
- Check microphone hardware status.
- Restart audio service or device.
- Verify audio permissions.

### ⚠️ V2TXLIVE_WARNING_MICROPHONE_OCCUPIED - Microphone Occupied

```dart
static const int V2TXLIVE_WARNING_MICROPHONE_OCCUPIED = -1319;
```

**Meaning**: Microphone is currently in use, for example, starting the microphone fails during an active phone call.

**Possible Causes**:
- Ongoing phone call.
- Another app is using the microphone.
- Voice assistant is active.

**Troubleshooting Tips**:
- End the current call or voice app.
- Wait for microphone resources to be released.
- Switch to another audio input device.

### ⚠️ V2TXLIVE_WARNING_MICROPHONE_NO_PERMISSION - Microphone Permission Not Granted

```dart
static const int V2TXLIVE_WARNING_MICROPHONE_NO_PERMISSION = -1317;
```

**Meaning**: Microphone access not authorized, typically on mobile devices due to denied permission.

**Possible Causes**:
- User denied microphone permission.
- App did not request microphone permission.
- Permission revoked by system or user.

**Troubleshooting Tips**:
- Check and request microphone permission.
- Guide users to enable microphone permissions.
- Provide instructions for requesting permissions.

## 6. Screen Sharing Warning Codes

### ⚠️ V2TXLIVE_WARNING_SCREEN_CAPTURE_NOT_SUPPORTED - Screen Sharing Not Supported by System

```dart
static const int V2TXLIVE_WARNING_SCREEN_CAPTURE_NOT_SUPPORTED = -1309;
```

**Meaning**: The current system does not support screen sharing.

**Possible Causes**:
- Operating system version is too low.
- Device hardware does not support screen sharing.
- Platform restrictions (e.g., certain mobile devices).

**Troubleshooting Tips**:
- Check system version requirements.
- Confirm device supports screen recording.
- Consider alternative sharing methods.

### ⚠️ V2TXLIVE_WARNING_SCREEN_CAPTURE_START_FAILED - Screen Recording Start Failed

```dart
static const int V2TXLIVE_WARNING_SCREEN_CAPTURE_START_FAILED = -1308;
```

**Meaning**: Failed to start screen recording; on mobile devices, this may be due to denied permission.

**Possible Causes**:
- User denied screen recording permission.
- System security policy restrictions.
- Another app is using screen recording.

**Troubleshooting Tips**:
- Check and request screen recording permission.
- Guide users to enable screen recording permissions.
- Close other screen recording apps.

### ⚠️ V2TXLIVE_WARNING_SCREEN_CAPTURE_INTERRUPTED - Screen Recording Interrupted

```dart
static const int V2TXLIVE_WARNING_SCREEN_CAPTURE_INTERRUPTED = -7001;
```

**Meaning**: Screen recording was interrupted by the system.

**Possible Causes**:
- System dialog or notification appeared.
- User switched to another app.
- System resources are low and recording was forcibly stopped.

**Troubleshooting Tips**:
- Restart screen recording.
- Avoid other operations during recording.
- Check system resource usage.

## 7. Codec Warning Codes

### ⚠️ V2TXLIVE_WARNING_ENCODER_START_FAILED - Video Encoder Start Failed

```dart
static const int V2TXLIVE_WARNING_ENCODER_START_FAILED = -1303;
```

**Meaning**: Failed to start the video encoder.

**Possible Causes**:
- Insufficient encoder hardware resources.
- Incorrect encoder parameter settings.
- System codec error.

**Troubleshooting Tips**:
- Check encoder parameter settings.
- Lower video resolution or bitrate.
- Restart encoder or app.

### ⚠️ V2TXLIVE_WARNING_DECODER_START_FAILED - Video Decoder Start Failed

```dart
static const int V2TXLIVE_WARNING_DECODER_START_FAILED = -1304;
```

**Meaning**: Failed to start the video decoder.

**Possible Causes**:
- Insufficient decoder hardware resources.
- Unsupported video format.
- System decoder error.

**Troubleshooting Tips**:
- Check video format compatibility.
- Lower video resolution or frame rate.
- Restart decoder or app.

### ⚠️ V2TXLIVE_WARNING_CURRENT_ENCODE_TYPE_CHANGED - Encoder Type Changed

```dart
static const int V2TXLIVE_WARNING_CURRENT_ENCODE_TYPE_CHANGED = 1104;
```

**Meaning**: The encoder type has changed. You can get the current encoding format from the codec_type field in the extended information of the onWarning callback.

**Possible Causes**:
- Encoder automatically switches (e.g., hardware encoding to software encoding).
- Encoding parameters are dynamically adjusted.
- System resource changes trigger encoder switch.

**Troubleshooting Tips**:
- Listen for encoder change events and update encoding strategy promptly.
- Adjust video quality settings based on encoder type.
- Log encoder changes for performance analysis.

### ⚠️ V2TXLIVE_WARNING_CURRENT_DECODE_TYPE_CHANGED - Decoder Type Changed

```dart
static const int V2TXLIVE_WARNING_CURRENT_DECODE_TYPE_CHANGED = 2008;
```

**Meaning**: The decoder type has changed. You can get the current decoding format from the codec_type field in the extended information of the onWarning callback.

**Possible Causes**:
- Decoder automatically switches (e.g., hardware decoding to software decoding).
- Video format changes trigger decoder switch.
- System resource changes trigger decoder switch.

**Troubleshooting Tips**:
- Listen for decoder change events and update decoding strategy promptly.
- Optimize playback performance based on decoder type.
- Log decoder changes for performance analysis.

**Note**: The Flutter platform supports extended information for this error code. You can get detailed codec type information via the callback parameters.