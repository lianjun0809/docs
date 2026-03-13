> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

# Tencent Cloud Live Streaming SDK V2TXLiveCode Error Code Documentation

## Overview

`V2TXLiveCode.java` defines the error and warning codes for the Tencent Cloud Live Streaming (CSS) SDK on Android. This file categorizes error codes and provides detailed descriptions for features such as host (push), player (playback), stream mixing, and recording.

**File Path**: `com/tencent/live2/V2TXLiveCode.java`  
**Platform Support**: Android  
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
### 9. [Error Handling Best Practices](#错误处理最佳实践)

## 1. Error Code Categories

### 🎯 Error Code Breakdown

| Category                        | Number of Codes | Main Functionality                        |
|----------------------------------|----------------|-------------------------------------------|
| General Error Codes              | 9              | API calls, parameter validation, permission checks |
| Network-Related Warning Codes    | 2              | Network status, video stutter monitoring  |
| Camera-Related Warning Codes     | 3              | Camera device status monitoring           |
| Microphone-Related Warning Codes | 3              | Microphone device status monitoring       |
| Screen Sharing Warning Codes     | 3              | Screen sharing status monitoring          |
| Codec Warning Codes              | 2              | Audio/video codec status monitoring       |

### 🔧 Technical Highlights

- **Hierarchical Categorization**: Error codes are organized by functional module.
- **Detailed Descriptions**: Each error code includes a clear explanation and usage scenario.
- **Platform-Specific**: Android-only error codes.
- **Debug-Friendly**: Comprehensive explanations and handling recommendations for each error code.

## 2. General Error Codes

### ✅ V2TXLIVE_OK - Operation Successful

```java
public static final int V2TXLIVE_OK = 0;
```

**Description**: Operation completed successfully; no error occurred.

**Typical Use Cases**:
- API call succeeded
- Operation executed and confirmed
- Status check returned normal

### ❌ V2TXLIVE_ERROR_FAILED - General Error

```java
public static final int V2TXLIVE_ERROR_FAILED = -1;
```

**Description**: Unclassified general error.

**Possible Causes**:
- Internal processing exception

### ❌ V2TXLIVE_ERROR_INVALID_PARAMETER - Invalid Parameter

```java
public static final int V2TXLIVE_ERROR_INVALID_PARAMETER = -2;
```

**Description**: Invalid parameters were provided in the API call.

**Common Scenarios**:
- Incorrect stream push URL format
- Unsupported parameter value

### ❌ V2TXLIVE_ERROR_REFUSED - API Call Refused

```java
public static final int V2TXLIVE_ERROR_REFUSED = -3;
```

**Description**: API call was refused.

**Possible Causes**:
- Incorrect call timing

### ❌ V2TXLIVE_ERROR_NOT_SUPPORTED - API Not Supported

```java
public static final int V2TXLIVE_ERROR_NOT_SUPPORTED = -4;
```

**Description**: This API is not supported.

**Common Scenarios**:
- Feature not supported on the current platform
- SDK version is too low
- Hardware does not support the feature

### ❌ V2TXLIVE_ERROR_INVALID_LICENSE - Invalid License

```java
public static final int V2TXLIVE_ERROR_INVALID_LICENSE = -5;
```

**Description**: License is invalid; the call failed.

**Possible Causes**:
- License file not set
- License expired
- License does not match the package name

### ❌ V2TXLIVE_ERROR_REQUEST_TIMEOUT - Request Timeout

```java
public static final int V2TXLIVE_ERROR_REQUEST_TIMEOUT = -6;
```

**Description**: Request to the server timed out.

**Common Scenarios**:
- Unstable network connection
- Slow server response

### ❌ V2TXLIVE_ERROR_SERVER_PROCESS_FAILED - Server Processing Failed

```java
public static final int V2TXLIVE_ERROR_SERVER_PROCESS_FAILED = -7;
```

**Description**: The server was unable to process your request.

**Possible Causes**:
- Internal server error
- Incorrect request format
- Insufficient server resources

### ❌ V2TXLIVE_ERROR_DISCONNECTED - Disconnected

```java
public static final int V2TXLIVE_ERROR_DISCONNECTED = -8;
```

**Description**: Network connection was lost.

**Common Scenarios**:
- Push stream network disconnected
- Playback network disconnected

### ❌ V2TXLIVE_ERROR_NO_AVAILABLE_HEVC_DECODERS - No Available HEVC Decoders

```java
public static final int V2TXLIVE_ERROR_NO_AVAILABLE_HEVC_DECODERS = -2304;
```

**Description**: No available HEVC decoders found.

**Possible Causes**:
- Device does not support HEVC Hardware Decoding
- HEVC decoder initialization failed
- System version is too low

## 3. Network-Related Warning Codes

### ⚠️ V2TXLIVE_WARNING_NETWORK_BUSY - Network Busy

```java
public static final int V2TXLIVE_WARNING_NETWORK_BUSY = 1101;
```

**Description**: Poor network conditions detected; insufficient upstream bandwidth is causing data upload to be blocked.

**Monitoring Indicators**:
- Upstream bandwidth limitations
- Increased network latency
- High packet loss rate

### ⚠️ V2TXLIVE_WARNING_VIDEO_BLOCK - Video Stutter

```java
public static final int V2TXLIVE_WARNING_VIDEO_BLOCK = 2105;
```

**Description**: Video playback is experiencing stutter.

**Possible Causes**:
- Insufficient network bandwidth
- Decoding performance bottleneck
- Rendering performance issues

## 4. Camera-Related Warning Codes

### ⚠️ V2TXLIVE_WARNING_CAMERA_START_FAILED - Camera Start Failed

```java
public static final int V2TXLIVE_WARNING_CAMERA_START_FAILED = -1301;
```

**Description**: Failed to start the camera.

**Possible Causes**:
- Hardware malfunction
- Driver issues
- Resource conflicts

### ⚠️ V2TXLIVE_WARNING_CAMERA_OCCUPIED - Camera Occupied

```java
public static final int V2TXLIVE_WARNING_CAMERA_OCCUPIED = -1316;
```

**Description**: Camera is currently in use.

**Possible Scenarios**:
- Another app is using the camera
- System camera app is running
- Video call is in progress

### ⚠️ V2TXLIVE_WARNING_CAMERA_NO_PERMISSION - Camera Not Authorized

```java
public static final int V2TXLIVE_WARNING_CAMERA_NO_PERMISSION = -1314;
```

**Description**: Camera access not authorized. This typically occurs on mobile devices when the user denies permission.

## 5. Microphone-Related Warning Codes

### ⚠️ V2TXLIVE_WARNING_MICROPHONE_START_FAILED - Microphone Start Failed

```java
public static final int V2TXLIVE_WARNING_MICROPHONE_START_FAILED = -1302;
```

**Description**: Failed to start the microphone.

**Possible Causes**:
- Hardware connection issues
- Abnormal system audio settings
- Audio session initialization failed

### ⚠️ V2TXLIVE_WARNING_MICROPHONE_OCCUPIED - Microphone Occupied

```java
public static final int V2TXLIVE_WARNING_MICROPHONE_OCCUPIED = -1319;
```

**Description**: Microphone is currently in use. For example, opening the microphone will fail if the device is in a call.

**Possible Scenarios**:
- Device is in a call
- Another audio app is using the microphone
- Audio session conflict

### ⚠️ V2TXLIVE_WARNING_MICROPHONE_NO_PERMISSION - Microphone Not Authorized

```java
public static final int V2TXLIVE_WARNING_MICROPHONE_NO_PERMISSION = -1317;
```

**Description**: Microphone access not authorized. This typically occurs on mobile devices when the user denies permission.

## 6. Screen Sharing Warning Codes

### ⚠️ V2TXLIVE_WARNING_SCREEN_CAPTURE_NOT_SUPPORTED - Screen Sharing Not Supported by System

```java
public static final int V2TXLIVE_WARNING_SCREEN_CAPTURE_NOT_SUPPORTED = -1309;
```

**Description**: The current system does not support screen sharing.

### ⚠️ V2TXLIVE_WARNING_SCREEN_CAPTURE_START_FAILED - Failed to Start Screen Capture

```java
public static final int V2TXLIVE_WARNING_SCREEN_CAPTURE_START_FAILED = -1308;
```

**Description**: Failed to start screen capture. On mobile devices, this may be due to the user denying permission.

### ⚠️ V2TXLIVE_WARNING_SCREEN_CAPTURE_INTERRUPTED - Screen Capture Interrupted by System

```java
public static final int V2TXLIVE_WARNING_SCREEN_CAPTURE_INTERRUPTED = -7001;
```

**Description**: Screen capture was interrupted by the system.

## 7. Codec Warning Codes

### ⚠️ V2TXLIVE_WARNING_CURRENT_ENCODE_TYPE_CHANGED - Encoder Changed

```java
public static final int V2TXLIVE_WARNING_CURRENT_ENCODE_TYPE_CHANGED = 1104;
```

**Description**: The encoder has changed. You can get the current codec format from the `codec_type` field in the extension info of the `onWarning` callback.

### ⚠️ V2TXLIVE_WARNING_CURRENT_DECODE_TYPE_CHANGED - Decoder Changed

```java
public static final int V2TXLIVE_WARNING_CURRENT_DECODE_TYPE_CHANGED = 2008;
```

**Description**: The decoder has changed. You can get the current decoding format from the `codec_type` field in the extension info of the `onWarning` callback.

**Note**: The extension info for this warning code is not supported on Windows.