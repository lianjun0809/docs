> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

# Tencent Cloud Live Streaming SDK V2TXLiveCode Error Code Documentation

## Overview

`V2TXLiveCode.h` defines the error and warning codes for the Tencent Cloud Live Streaming (CSS) SDK on iOS and macOS. This file covers error code categories and detailed descriptions for modules such as host, player, stream mixing, and recording.

**Platform Support**: iOS, macOS  
**Total Error Codes**: 20 core error and warning codes

## 📋 Table of Contents

### 1. [Error Code Categories](#错误码分类)
### 2. [General Error Codes](#通用错误码)
### 3. [Network-Related Warning Codes](#网络相关警告码)
### 4. [Camera-Related Warning Codes](#摄像头相关警告码)
### 5. [Microphone-Related Warning Codes](#麦克风相关警告码)
### 6. [Screen Sharing Warning Codes](#屏幕分享相关警告码)
### 7. [Codec Warning Codes](#编解码相关警告码)
### 8. [Error Code Usage Guide](#错误码使用指南)

## 1. Error Code Categories

### 🎯 Error Code Statistics

| Category                        | Number of Codes | Main Functions                        |
|----------------------------------|----------------|---------------------------------------|
| General Error Codes              | 9              | API calls, parameter validation, permission checks |
| Network-Related Warning Codes    | 2              | Network status, video stutter monitoring |
| Camera-Related Warning Codes     | 3              | Camera device status monitoring       |
| Microphone-Related Warning Codes | 3              | Microphone device status monitoring   |
| Screen Sharing Warning Codes     | 3              | Screen sharing feature status monitoring |
| Codec Warning Codes              | 2              | Audio/video codec status monitoring   |

### 🔧 Technical Features

- **Hierarchical Categorization**: Error codes are organized by functional module.
- **Detailed Descriptions**: Each error code includes a clear explanation and usage scenario.
- **Platform-Specific**: Error codes are tailored for iOS and macOS.
- **Debug-Friendly**: Each code provides detailed explanations and troubleshooting suggestions.

## 2. General Error Codes

### ✅ V2TXLIVE_OK - Operation Successful

```objc
V2TXLIVE_OK = 0
```

**Description**: No error occurred; the operation completed successfully.

**Typical Scenarios**:
- API call succeeded
- Operation executed and confirmed
- Status check returned normal

### ❌ V2TXLIVE_ERROR_FAILED - General Error

```objc
V2TXLIVE_ERROR_FAILED = -1
```

**Description**: A general error occurred that does not fit into a specific category.

**Possible Causes**:
- Internal processing exception
- Unclassified error

### ❌ V2TXLIVE_ERROR_INVALID_PARAMETER - Invalid Parameter

```objc
V2TXLIVE_ERROR_INVALID_PARAMETER = -2
```

**Description**: An invalid parameter was passed to the API.

**Common Causes**:
- Incorrect stream URL format
- Unsupported parameter value

### ❌ V2TXLIVE_ERROR_REFUSED - API Call Refused

```objc
V2TXLIVE_ERROR_REFUSED = -3
```

**Description**: The API call was refused.

**Possible Causes**:
- Incorrect call timing

### ❌ V2TXLIVE_ERROR_NOT_SUPPORTED - API Not Supported

```objc
V2TXLIVE_ERROR_NOT_SUPPORTED = -4
```

**Description**: The current API is not supported.

**Common Causes**:
- Feature not supported on this platform
- SDK version is outdated
- Hardware does not support the feature

### ❌ V2TXLIVE_ERROR_INVALID_LICENSE - Invalid License

```objc
V2TXLIVE_ERROR_INVALID_LICENSE = -5
```

**Description**: The license is invalid; the call failed.

**Possible Causes**:
- License file not set
- License expired
- License does not match the bundle identifier

### ❌ V2TXLIVE_ERROR_REQUEST_TIMEOUT - Request Timeout

```objc
V2TXLIVE_ERROR_REQUEST_TIMEOUT = -6
```

**Description**: The request to the server timed out.

**Common Causes**:
- Unstable network connection
- Slow server response

### ❌ V2TXLIVE_ERROR_SERVER_PROCESS_FAILED - Server Processing Failed

```objc
V2TXLIVE_ERROR_SERVER_PROCESS_FAILED = -7
```

**Description**: The server failed to process the request.

**Possible Causes**:
- Internal server error
- Incorrect request format
- Insufficient server resources

### ❌ V2TXLIVE_ERROR_DISCONNECTED - Disconnected

```objc
V2TXLIVE_ERROR_DISCONNECTED = -8
```

**Description**: Network connection was lost.

**Common Causes**:
- Stream push network disconnected
- Stream pull network disconnected

### ❌ V2TXLIVE_ERROR_NO_AVAILABLE_HEVC_DECODERS - No Available HEVC Decoders

```objc
V2TXLIVE_ERROR_NO_AVAILABLE_HEVC_DECODERS = -2304
```

**Description**: No available HEVC decoder found.

**Possible Causes**:
- Device does not support HEVC Hardware Decoding
- Failed to initialize HEVC decoder
- System version is too low

## 3. Network-Related Warning Codes

### ⚠️ V2TXLIVE_WARNING_NETWORK_BUSY - Network Busy

```objc
V2TXLIVE_WARNING_NETWORK_BUSY = 1101
```

**Description**: Network conditions are poor. Uplink bandwidth is insufficient, causing data upload to be blocked.

**Monitoring Indicators**:
- Uplink bandwidth limitation
- Increased network latency
- High packet loss rate

### ⚠️ V2TXLIVE_WARNING_VIDEO_BLOCK - Video Stutter

```objc
V2TXLIVE_WARNING_VIDEO_BLOCK = 2105
```

**Description**: Video playback is currently stuttering.

**Possible Causes**:
- Insufficient network bandwidth
- Decoding performance bottleneck
- Rendering performance issues

## 4. Camera-Related Warning Codes

### ⚠️ V2TXLIVE_WARNING_CAMERA_START_FAILED - Camera Start Failed

```objc
V2TXLIVE_WARNING_CAMERA_START_FAILED = -1301
```

**Description**: Failed to start the camera.

**Possible Causes**:
- Hardware malfunction
- Driver issues
- Resource conflict

### ⚠️ V2TXLIVE_WARNING_CAMERA_OCCUPIED - Camera Occupied

```objc
V2TXLIVE_WARNING_CAMERA_OCCUPIED = -1316
```

**Description**: The camera is currently in use. Try switching to another camera.

**Possible Scenarios**:
- Another app is using the camera
- System camera app is running
- Video call in progress

### ⚠️ V2TXLIVE_WARNING_CAMERA_NO_PERMISSION - Camera Not Authorized

```objc
V2TXLIVE_WARNING_CAMERA_NO_PERMISSION = -1314
```

**Description**: The camera is not authorized. This usually occurs when the user denies camera permission on a mobile device.

## 5. Microphone-Related Warning Codes

### ⚠️ V2TXLIVE_WARNING_MICROPHONE_START_FAILED - Microphone Start Failed

```objc
V2TXLIVE_WARNING_MICROPHONE_START_FAILED = -1302
```

**Description**: Failed to start the microphone.

**Possible Causes**:
- Hardware connection issues
- Abnormal system audio settings
- Failed to initialize audio session

### ⚠️ V2TXLIVE_WARNING_MICROPHONE_OCCUPIED - Microphone Occupied

```objc
V2TXLIVE_WARNING_MICROPHONE_OCCUPIED = -1319
```

**Description**: The microphone is currently in use. For example, opening the microphone fails when the device is in a call.

**Possible Scenarios**:
- Device is in a call
- Another audio app is using the microphone
- Audio session conflict

### ⚠️ V2TXLIVE_WARNING_MICROPHONE_NO_PERMISSION - Microphone Not Authorized

```objc
V2TXLIVE_WARNING_MICROPHONE_NO_PERMISSION = -1317
```

**Description**: The microphone is not authorized. This usually occurs when the user denies microphone permission on a mobile device.

## 6. Screen Sharing Warning Codes

### ⚠️ V2TXLIVE_WARNING_SCREEN_CAPTURE_NOT_SUPPORTED - Screen Sharing Not Supported by System

```objc
V2TXLIVE_WARNING_SCREEN_CAPTURE_NOT_SUPPORTED = -1309
```

**Description**: The current system does not support screen sharing.

**Compatibility Requirements**:
- iOS 11.0 or later supports ReplayKit screen recording
- ReplayKit feature must be available

### ⚠️ V2TXLIVE_WARNING_SCREEN_CAPTURE_START_FAILED - Failed to Start Screen Recording

```objc
V2TXLIVE_WARNING_SCREEN_CAPTURE_START_FAILED = -1308
```

**Description**: Failed to start screen recording. On mobile devices, this may occur if the user denies permission.

**Possible Causes**:
- User denied screen recording permission
- Screen recording feature unavailable
- System restrictions

### ⚠️ V2TXLIVE_WARNING_SCREEN_CAPTURE_INTERRUPTED - Screen Recording Interrupted by System

```objc
V2TXLIVE_WARNING_SCREEN_CAPTURE_INTERRUPTED = -7001
```

**Description**: Screen recording was interrupted by the system.

**Possible Causes**:
- System events (such as incoming calls or screen lock)
- User manually stopped screen recording
- System resource limitations

## 7. Codec Warning Codes

### ⚠️ V2TXLIVE_WARNING_CURRENT_ENCODE_TYPE_CHANGED - Encoder Changed

```objc
V2TXLIVE_WARNING_CURRENT_ENCODE_TYPE_CHANGED = 1104
```

**Description**: The encoder type has changed. You can retrieve the current codec format from the `codec_type` field in the extended info of the `onWarning` callback.

**Note**: Extended info for this warning code is not supported on Windows.

### ⚠️ V2TXLIVE_WARNING_CURRENT_DECODE_TYPE_CHANGED - Decoder Changed

```objc
V2TXLIVE_WARNING_CURRENT_DECODE_TYPE_CHANGED = 2008
```

**Description**: The decoder type has changed. You can retrieve the current decoding format from the `codec_type` field in the extended info of the `onWarning` callback.

**Note**: Extended info for this warning code is not supported on Windows.