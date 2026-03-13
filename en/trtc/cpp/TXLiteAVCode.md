> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

# TRTC Real-Time Communication (TRTC SDK) Documentation
## Overview
`TXLiteAVCode.h` provides status code definitions for TRTC Real-Time Communication (TRTC SDK) on C++. This file is used to notify developers of warnings and errors that occur while using TRTC.

## Enumeration Types
| Enumeration Types | Description |
| --- | --- |
| TXLiteAVError | Error Code |
| TXLiteAVWarning | Warning Codes |

## TXLiteAVError

#### Error Code
| Enumeration | Value | Description |
| --- | --- | --- |
| ERR_NULL | 0 | No error |
| ERR_FAILED | -1 | A common error not yet classified |
| ERR_INVALID_PARAMETER | -2 | An invalid parameter was passed in during API calling |
| ERR_REFUSED | -3 | The API call was rejected |
| ERR_NOT_SUPPORTED | -4 | The current API does not support calls |
| ERR_INVALID_LICENSE | -5 | Failed to call the API due to invalid license |
| ERR_REQUEST_SERVER_TIMEOUT | -6 | The server request timed out |
| ERR_SERVER_PROCESS_FAILED | -7 | The server could not handle your request |
| ERR_DISCONNECTED | -8 | Disconnect |
| ERR_CAMERA_START_FAIL | -1301 | Failed to enable the camera; for example, the configuration program (driver) of the camera on Windows or macOS was exceptional. In this case, please try to disable and then enable the camera again, restart the device, or update the configuration program |
| ERR_CAMERA_NOT_AUTHORIZED | -1314 | The camera is not authorized. This error usually occurs on mobile devices and may be caused by permission denial by user |
| ERR_CAMERA_SET_PARAM_FAIL | -1315 | Incorrect camera parameter settings (unsupported value or other causes) |
| ERR_CAMERA_OCCUPY | -1316 | The camera is being used. Please try to enable another camera |
| ERR_SCREEN_CAPTURE_START_FAIL | -1308 | Failed to start screen sharing. If this error occurs on a mobile device, it may be caused by permission denial by user; if on Windows or macOS, please check whether parameters of the screen sharing API meet the requirements |
| ERR_SCREEN_CAPTURE_UNSURPORT | -1309 | Screen sharing failed. Please use Android 5.0 or above if the device is on Android or use iOS 11.0 or above if the device is on iOS |
| ERR_SCREEN_CAPTURE_STOPPED | -7001 | Screencapturing was stopped by the system |
| ERR_SCREEN_SHARE_NOT_AUTHORIZED | -102015 | No permission to send auxiliary stream |
| ERR_SCREEN_SHRAE_OCCUPIED_BY_OTHER | -102016 | Other users are upstreaming substream |
| ERR_VIDEO_ENCODE_FAIL | -1303 | Failed to encode video frames; for example, when a user switches from an iOS device to another device, the hardware encoder may be released by the system; and after the user switches back, this error may be thrown before the hardware encoder is restarted |
| ERR_UNSUPPORTED_RESOLUTION | -1305 | Unsupported video resolution |
| ERR_PIXEL_FORMAT_UNSUPPORTED | -1327 | Custom video capture: Unsupported pixel format |
| ERR_BUFFER_TYPE_UNSUPPORTED | -1328 | Custom video capture: Unsupported buffer type |
| ERR_NO_AVAILABLE_HEVC_DECODERS | -2304 | No available HEVC decoder found |
| ERR_MIC_START_FAIL | -1302 | Failed to enable the mic; for example, the configuration program (driver) of the mic on Windows or macOS was exceptional. In this case, please try to disable and then enable the mic again, restart the device, or update the configuration program |
| ERR_MIC_NOT_AUTHORIZED | -1317 | No access to the microphone. This usually occurs on mobile devices and may be because the user denied the access. |
| ERR_MIC_SET_PARAM_FAIL | -1318 | Failed to set microphone parameters. |
| ERR_MIC_OCCUPY | -1319 | The microphone is occupied. This occurs when, for example, the user is currently having a call on the mobile device. |
| ERR_MIC_STOP_FAIL | -1320 | Failed to stop the microphone. |
| ERR_SPEAKER_START_FAIL | -1321 | Failed to enable the speaker; for example, the configuration program (driver) of the speaker on Windows or macOS was exceptional. In this case, please try to disable and then enable the speaker again, restart the device, or update the configuration program |
| ERR_SPEAKER_SET_PARAM_FAIL | -1322 | Failed to set speaker parameters. |
| ERR_SPEAKER_STOP_FAIL | -1323 | Failed to stop the speaker. |
| ERR_AUDIO_PLUGIN_START_FAIL | -1330 | Failed to enable system sound recording; for example, the audio driver plugin was unavailable |
| ERR_AUDIO_PLUGIN_INSTALL_NOT_AUTHORIZED | -1331 | Unauthorized audio driver plugin installation |
| ERR_AUDIO_PLUGIN_INSTALL_FAILED | -1332 | Failed to install audio driver plugin |
| ERR_AUDIO_PLUGIN_INSTALLED_BUT_NEED_RESTART | -1333 | Successfully installed virtual sound card plugin, but features are temporarily unavailable after the first installation due to macOS system restrictions. Please advise the user to restart the current app upon receiving this error code |
| ERR_AUDIO_ENCODE_FAIL | -1304 | Failed to encode audio frames; for example, the SDK could not process the custom audio data passed in |
| ERR_UNSUPPORTED_SAMPLERATE | -1306 | Unsupported audio sample rate |
| ERR_SYSTEM_LOOPBACK_START_FAILED | -1307 | System mixing startup error. Common causes and solutions: 1. The current system version is unsupported. Specific process exclusion feature requires Windows System to be 10.0.19042 (20H2) or higher. Path mixing feature x64 version requires Windows System to be 10.0.19042 (20H2) or higher. Please check the current system version. 2. Invalid input parameters (including empty parameters, nonexistent path, nonexistent process ID, nonexistent device name). Please check the validity of input parameters. 3. No available speaker device, please check availability |
| ERR_SYSTEM_LOOPBACK_THIRD_PARTY_APP_EXIT | -1324 | Third party application mixing and acquisition error. This error may occur after the third party application mixing starts successfully. During the sound acquisition process, the specified process or application may exit unexpectedly. Please check the state of the specified process or application, and try again by re-entering the process ID |
| ERR_TRTC_ENTER_ROOM_FAILED | -3301 | Failed to enter the room. Please view -3301 in onError to confirm the message for the reason of the failure. |
| ERR_TRTC_REQUEST_IP_TIMEOUT | -3307 | Request for IP and Sig timed out. Please check whether your network is functioning properly and whether UDP is unblocked in your network firewall. You can try accessing the following IPs: 162.14.22.165:8000, 162.14.6.105:8000 and domain name: default-query.trtc.tencent-cloud.com:8000 |
| ERR_TRTC_CONNECT_SERVER_TIMEOUT | -3308 | Request for room entry timed out. Please check your network connection or whether you are on a VPN. You can also try switching to 4G for confirmation. |
| ERR_TRTC_ROOM_PARAM_NULL | -3316 | Join Room Parameters are empty. Please check if the enterRoom:appScene: interface call has a valid param |
| ERR_TRTC_INVALID_SDK_APPID | -3317 | Join Room Parameter sdkAppId is incorrect. Please check if TRTCParams.sdkAppId is empty |
| ERR_TRTC_INVALID_ROOM_ID | -3318 | Join Room Parameter roomId is incorrect. Please check if TRTCParams.roomId or TRTCParams.strRoomId is empty. Note that roomId and strRoomId cannot be used interchangeably |
| ERR_TRTC_INVALID_USER_ID | -3319 | Join Room Parameter userId is incorrect. Please check if TRTCParams.userId is empty |
| ERR_TRTC_INVALID_USER_SIG | -3320 | Join Room Parameter userSig is incorrect. Please check if TRTCParams.userSig is empty |
| ERR_TRTC_ENTER_ROOM_REFUSED | -3340 | Join Room Request was rejected. Please check if you are continuously calling enterRoom to enter the room with the same Id |
| ERR_TRTC_INVALID_PRIVATE_MAPKEY | -100006 | You have enabled Advanced Permission Control, but the parameter TRTCParams.privateMapKey failed verification You can refer to [Advanced Permission Control](https://cloud.tencent.com/document/product/647/32240) for inspection |
| ERR_TRTC_SERVICE_SUSPENDED | -100013 | Unavailable service. Please check whether the remained validity period in minutes in the package is greater than 0 and whether the Tencent Cloud account is in arrears. You can refer to [Package Management](https://cloud.tencent.com/document/product/647/50492) for viewing and configuration |
| ERR_TRTC_USER_SIG_CHECK_FAILED | -100018 | UserSig verification failed. Please check if the parameter TRTCParams.userSig is filled correctly or if it has expired. You can refer to [UserSig Generation and Verification](https://cloud.tencent.com/document/product/647/50686) for validation |
| ERR_TRTC_PUSH_THIRD_PARTY_CLOUD_TIMEOUT | -3321 | The relayed push request timed out |
| ERR_TRTC_MIX_TRANSCODING_TIMEOUT | -3322 | The On-Cloud MixTranscoding request timed out |
| ERR_TRTC_PUSH_THIRD_PARTY_CLOUD_FAILED | -3323 | Relay to CDN callback exception |
| ERR_TRTC_MIX_TRANSCODING_FAILED | -3324 | The On-Cloud MixTranscoding callback exception |
| ERR_TRTC_START_PUBLISHING_TIMEOUT | -3333 | Signaling timed out when starting pushing to Tencent Cloud LVB CDN |
| ERR_TRTC_START_PUBLISHING_FAILED | -3334 | Signaling was exceptional when starting pushing to Tencent Cloud LVB CDN |
| ERR_TRTC_STOP_PUBLISHING_TIMEOUT | -3335 | Signaling timed out when stopping pushing to Tencent Cloud LVB CDN |
| ERR_TRTC_STOP_PUBLISHING_FAILED | -3336 | Signaling was exceptional when stopping pushing to Tencent Cloud LVB CDN |
| ERR_TRTC_CONNECT_OTHER_ROOM_TIMEOUT | -3326 | Request for cross-room mic connection timed out |
| ERR_TRTC_DISCONNECT_OTHER_ROOM_TIMEOUT | -3327 | Request to exit cross-room mic connection timed out |
| ERR_TRTC_CONNECT_OTHER_ROOM_INVALID_PARAMETER | -3328 | Invalid parameter |
| ERR_TRTC_CONNECT_OTHER_ROOM_AS_AUDIENCE | -3330 | You are currently in Audience Role and cannot request or disconnect cross-room mic connection. You need to `switchRole` to an anchor |
| ERR_BGM_OPEN_FAILED | -4001 | Failed to open file due to reasons like invalid audio data or FFMPEG Protocol not found |
| ERR_BGM_DECODE_FAILED | -4002 | Failed to decode audio file |
| ERR_BGM_OVER_LIMIT | -4003 | Quantity exceeds the limit, such as preloading two background music tracks simultaneously |
| ERR_BGM_INVALID_OPERATION | -4004 | Invalid operation, such as calling preloading after starting playback |
| ERR_BGM_INVALID_PATH | -4005 | Failed to open file due to illegal path. Please check if the provided path parameter points to a valid music file |
| ERR_BGM_INVALID_URL | -4006 | Failed to open file due to illegal URL. Please check with a browser if the provided URL can download the expected music file |
| ERR_BGM_NO_AUDIO_STREAM | -4007 | Failed to open file due to no audio stream. Please ensure the provided file is a valid audio file and is not corrupted |
| ERR_BGM_FORMAT_NOT_SUPPORTED | -4008 | Failed to open file due to unsupported format. Please check if the provided file format is supported. Mobile supports [mp3, aac, m4a, wav, ogg, mp4, mkv], desktop supports [mp3, aac, m4a, wav, mp4, mkv] |

## TXLiteAVWarning

#### Warning Codes
| Enumeration | Value | Description |
| --- | --- | --- |
| WARNING_HW_ENCODER_START_FAIL | 1103 | Problem with enabling hardware encoding, switched to software encoding automatically |
| WARNING_CURRENT_ENCODE_TYPE_CHANGED | 1104 | Indicates encoder change; detailed encoding format and type can be retrieved from relevant fields in the onWarning function's extended information. Field 'type' value 0 represents H.264 encoding, 1 represents H.265 encoding Field 'hardware' value 0 represents software encoding, 1 represents hardware encoding Field 'stream' value 0 represents large stream, 1 represents small stream, 2 represents auxiliary stream |
| WARNING_VIDEO_ENCODER_SW_TO_HW | 1107 | The current CPU utilization is too high to meet software encoding needs, and the hardware encoder was automatically switch to |
| WARNING_INSUFFICIENT_CAPTURE_FPS | 1108 | Insufficient frame rate for video capturing through camera. This error may occur in Android mobile devices with an in-built beauty filter algorithm |
| WARNING_SW_ENCODER_START_FAIL | 1109 | Failed to enable the software encoder |
| WARNING_REDUCE_CAPTURE_RESOLUTION | 1110 | Camera resolution reduced for balance between frame rate and performance. |
| WARNING_CAMERA_DEVICE_EMPTY | 1111 | No available camera device detected |
| WARNING_CAMERA_NOT_AUTHORIZED | 1112 | The current application is not authorized to use the camera |
| WARNING_OUT_OF_MEMORY | 1113 | Insufficient memory, some features may not function properly. |
| WARNING_CAMERA_IS_OCCUPIED | 1114 | The camera is being used. |
| WARNING_CAMERA_DEVICE_ERROR | 1115 | Camera device abnormal. |
| WARNING_CAMERA_DISCONNECTED | 1116 | Camera connection failed. |
| WARNING_CAMERA_START_FAILED | 1117 | Failed to start the camera. |
| WARNING_CAMERA_SERVER_DIED | 1118 | System anomaly. |
| WARNING_SCREEN_CAPTURE_NOT_AUTHORIZED | 1206 | The current application is not authorized to use screen recording |
| WARNING_CURRENT_DECODE_TYPE_CHANGED | 2008 | Indicates decoder change; the current decoding format can be retrieved from the type field in the onWarning function's extended information. Here, 1 represents 265 decoding, and 0 represents 264 decoding. Note that this error code's extended information is not supported on Windows. |
| WARNING_VIDEO_FRAME_DECODE_FAIL | 2101 | Failed to decode the current video frame |
| WARNING_HW_DECODER_START_FAIL | 2106 | Failed to enable the hardware decoder, and the software decoder was used |
| WARNING_VIDEO_DECODER_HW_TO_SW | 2108 | The hardware decoder failed to decode the first I frame of the current stream, and the SDK automatically switched to the software decoder |
| WARNING_SW_DECODER_START_FAIL | 2109 | Failed to enable the software decoder |
| WARNING_VIDEO_RENDER_FAIL | 2110 | Failed to render video |
| WARNING_VIRTUAL_BACKGROUND_DEVICE_UNSURPORTED | 8001 | Virtual background device not supported |
| WARNING_VIRTUAL_BACKGROUND_NOT_AUTHORIZED | 8002 | Virtual background not authorized |
| WARNING_VIRTUAL_BACKGROUND_INVALID_PARAMETER | 8003 | Virtual background parameter abnormal |
| WARNING_VIRTUAL_BACKGROUND_PERFORMANCE_INSUFFICIENT | 8004 | Virtual background performance insufficient |
| WARNING_MICROPHONE_DEVICE_EMPTY | 1201 | No available mic device detected |
| WARNING_SPEAKER_DEVICE_EMPTY | 1202 | No available speaker device detected |
| WARNING_MICROPHONE_NOT_AUTHORIZED | 1203 | The current application is not authorized to use the mic |
| WARNING_MICROPHONE_DEVICE_ABNORMAL | 1204 | Audio capture device is unavailable (e.g., in use or deemed invalid by PC) |
| WARNING_SPEAKER_DEVICE_ABNORMAL | 1205 | Audio playback device is unavailable (e.g., in use or deemed invalid by PC) |
| WARNING_BLUETOOTH_DEVICE_CONNECT_FAIL | 1207 | Bluetooth device connection failed (e.g., audio channel occupied by another app setting call volume) |
| WARNING_MICROPHONE_IS_OCCUPIED | 1208 | Audio capture device is occupied |
| WARNING_AUDIO_FRAME_DECODE_FAIL | 2102 | Failed to decode the current audio frame |
| WARNING_AUDIO_RECORDING_WRITE_FAIL | 7001 | Failed to write the recorded audio to a file |
| WARNING_MICROPHONE_HOWLING_DETECTED | 7002 | Howling detected during audio recording |
| WARNING_IGNORE_UPSTREAM_FOR_AUDIENCE | 6001 | You are currently in Audience Role and cannot publish audio or video. You need to switch to an anchor role |
| WARNING_UPSTREAM_AUDIO_AND_VIDEO_OUT_OF_SYNC | 6006 | Audio and video sending timestamp abnormal, may cause audio and video out of sync issues |
