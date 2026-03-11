> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/en/llms.txt
> Use this file to discover all available pages before exploring further.

# TRTC Real-Time Communication (TRTC SDK) Documentation
## Overview
`TXLiteAVCode.h` provides status code definitions for TRTC Real-Time Communication (TRTC SDK) on iOS. This file is used to notify developers of warnings and errors that occur while using TRTC.


## 枚举类型
<table>
<tr>
<td rowspan="1" colSpan="1" >Enumeration Types</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[TXLiteAVError](https://write.woa.com/document/86735809798561792)</td>

<td rowspan="1" colSpan="1" >Error Code</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[TXLiteAVWarning](https://write.woa.com/document/86735809798561792)</td>

<td rowspan="1" colSpan="1" >Warning Codes</td>
</tr>
</table>


## TXLiteAVError


#### 错误码。
<table>
<tr>
<td rowspan="1" colSpan="1" >Enumeration</td>

<td rowspan="1" colSpan="1" >Value</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_NULL</td>

<td rowspan="1" colSpan="1" >0</td>

<td rowspan="1" colSpan="1" >No error</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_FAILED</td>

<td rowspan="1" colSpan="1" >-1</td>

<td rowspan="1" colSpan="1" >A common error not yet classified</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_INVALID_PARAMETER</td>

<td rowspan="1" colSpan="1" >-2</td>

<td rowspan="1" colSpan="1" >An invalid parameter was passed in during API calling</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_REFUSED</td>

<td rowspan="1" colSpan="1" >-3</td>

<td rowspan="1" colSpan="1" >The API call was rejected</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_NOT_SUPPORTED</td>

<td rowspan="1" colSpan="1" >-4</td>

<td rowspan="1" colSpan="1" >Does not support API call currently</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_INVALID_LICENSE</td>

<td rowspan="1" colSpan="1" >-5</td>

<td rowspan="1" colSpan="1" >Failed to call the API due to invalid license</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_REQUEST_SERVER_TIMEOUT</td>

<td rowspan="1" colSpan="1" >-6</td>

<td rowspan="1" colSpan="1" >The server request timed out</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_SERVER_PROCESS_FAILED</td>

<td rowspan="1" colSpan="1" >-7</td>

<td rowspan="1" colSpan="1" >The server could not handle your request</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_DISCONNECTED</td>

<td rowspan="1" colSpan="1" >-8</td>

<td rowspan="1" colSpan="1" >Disconnect from user</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_CAMERA_START_FAIL</td>

<td rowspan="1" colSpan="1" >-1301</td>

<td rowspan="1" colSpan="1" >Failed to enable the camera; for example, the configuration program (driver) of the camera on Windows or macOS was exceptional. In this case, please try to disable and then enable the camera again, restart the device, or update the configuration program</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_CAMERA_NOT_AUTHORIZED</td>

<td rowspan="1" colSpan="1" >-1314</td>

<td rowspan="1" colSpan="1" >The camera is not authorized. This error usually occurs on mobile devices and may be caused by permission denial by user</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_CAMERA_SET_PARAM_FAIL</td>

<td rowspan="1" colSpan="1" >-1315</td>

<td rowspan="1" colSpan="1" >Incorrect camera parameter settings (unsupported value or other causes)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_CAMERA_OCCUPY</td>

<td rowspan="1" colSpan="1" >-1316</td>

<td rowspan="1" colSpan="1" >The camera is being used. Please try to enable another camera</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_SCREEN_CAPTURE_START_FAIL</td>

<td rowspan="1" colSpan="1" >-1308</td>

<td rowspan="1" colSpan="1" >Failed to start screen sharing. If this error occurs on a mobile device, it may be caused by permission denial by user; if on Windows or macOS, please check whether parameters of the screen sharing API meet the requirements</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_SCREEN_CAPTURE_UNSURPORT</td>

<td rowspan="1" colSpan="1" >-1309</td>

<td rowspan="1" colSpan="1" >Screen sharing failed. Please use Android 5.0 or above if the device is on Android or use iOS 11.0 or above if the device is on iOS</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_SCREEN_CAPTURE_STOPPED</td>

<td rowspan="1" colSpan="1" >-7001</td>

<td rowspan="1" colSpan="1" >Screencapturing was stopped by the system</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_SCREEN_SHARE_NOT_AUTHORIZED</td>

<td rowspan="1" colSpan="1" >-102015</td>

<td rowspan="1" colSpan="1" >No permission for uplink auxiliary route</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_SCREEN_SHRAE_OCCUPIED_BY_OTHER</td>

<td rowspan="1" colSpan="1" >-102016</td>

<td rowspan="1" colSpan="1" >Other users are upstreaming substream</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_VIDEO_ENCODE_FAIL</td>

<td rowspan="1" colSpan="1" >-1303</td>

<td rowspan="1" colSpan="1" >Failed to encode video frames; for example, when a user switches from an iOS device to another device, the hardware encoder may be released by the system; and after the user switches back, this error may be thrown before the hardware encoder is restarted</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_UNSUPPORTED_RESOLUTION</td>

<td rowspan="1" colSpan="1" >-1305</td>

<td rowspan="1" colSpan="1" >Unsupported video resolution</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_PIXEL_FORMAT_UNSUPPORTED</td>

<td rowspan="1" colSpan="1" >-1327</td>

<td rowspan="1" colSpan="1" >Custom Video Capture: Unsupported pixel format</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_BUFFER_TYPE_UNSUPPORTED</td>

<td rowspan="1" colSpan="1" >-1328</td>

<td rowspan="1" colSpan="1" >Custom Video Capture: Unsupported buffer type</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_NO_AVAILABLE_HEVC_DECODERS</td>

<td rowspan="1" colSpan="1" >-2304</td>

<td rowspan="1" colSpan="1" >No available HEVC decoder found</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_MIC_START_FAIL</td>

<td rowspan="1" colSpan="1" >-1302</td>

<td rowspan="1" colSpan="1" >Failed to enable the mic; for example, the configuration program (driver) of the mic on Windows or macOS was exceptional. In this case, please try to disable and then enable the mic again, restart the device, or update the configuration program</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_MIC_NOT_AUTHORIZED</td>

<td rowspan="1" colSpan="1" >-1317</td>

<td rowspan="1" colSpan="1" >No access to the microphone. This usually occurs on mobile devices and may be because the user denied the access.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_MIC_OCCUPY</td>

<td rowspan="1" colSpan="1" >-1319</td>

<td rowspan="1" colSpan="1" >The microphone is occupied. This occurs when, for example, the user is currently having a call on the mobile device.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_MIC_STOP_FAIL</td>

<td rowspan="1" colSpan="1" >-1320</td>

<td rowspan="1" colSpan="1" >Failed to stop the microphone.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_SPEAKER_START_FAIL</td>

<td rowspan="1" colSpan="1" >-1321</td>

<td rowspan="1" colSpan="1" >Failed to enable the speaker; for example, the configuration program (driver) of the speaker on Windows or macOS was exceptional. In this case, please try to disable and then enable the speaker again, restart the device, or update the configuration program</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_SPEAKER_SET_PARAM_FAIL</td>

<td rowspan="1" colSpan="1" >-1322</td>

<td rowspan="1" colSpan="1" >Failed to set speaker parameters.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_SPEAKER_STOP_FAIL</td>

<td rowspan="1" colSpan="1" >-1323</td>

<td rowspan="1" colSpan="1" >Failed to stop the speaker.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_AUDIO_PLUGIN_START_FAIL</td>

<td rowspan="1" colSpan="1" >-1330</td>

<td rowspan="1" colSpan="1" >console.log('Failed to enable system sound recording; for example, the audio driver plugin was unavailable');</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_AUDIO_PLUGIN_INSTALL_NOT_AUTHORIZED</td>

<td rowspan="1" colSpan="1" >-1331</td>

<td rowspan="1" colSpan="1" >Installation of the audio driver plugin was unauthorized</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_AUDIO_PLUGIN_INSTALL_FAILED</td>

<td rowspan="1" colSpan="1" >-1332</td>

<td rowspan="1" colSpan="1" >Failed to install the audio driver plugin</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_AUDIO_PLUGIN_INSTALLED_BUT_NEED_RESTART</td>

<td rowspan="1" colSpan="1" >-1333</td>

<td rowspan="1" colSpan="1" >Successfully installed the virtual sound card plugin, but the feature is temporarily unavailable after the first installation. This is a macOS system limitation. Please prompt the user to restart the current app upon receiving this error code</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_AUDIO_ENCODE_FAIL</td>

<td rowspan="1" colSpan="1" >-1304</td>

<td rowspan="1" colSpan="1" >Failed to encode audio frames; for example, the SDK could not process the custom audio data passed in</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_UNSUPPORTED_SAMPLERATE</td>

<td rowspan="1" colSpan="1" >-1306</td>

<td rowspan="1" colSpan="1" >Unsupported audio sample rate</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_SYSTEM_LOOPBACK_START_FAILED</td>

<td rowspan="1" colSpan="1" >-1307</td>

<td rowspan="1" colSpan="1" >System mixing startup error. Common causes and solutions: 1. The current system version is incompatible. Specifying or excluding specific processes for mixing requires Windows version 10.0.19042 (20H2) or higher. Specifying a path for mixing (x64 version) also requires Windows version 10.0.19042 (20H2) or higher. Please check your current system version. 2. Invalid input parameters (including empty parameters, non-existent paths, non-existent process IDs, and non-existent device names). Please check if the input parameters are valid. 3. No available speaker devices. Please check if any are available.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_SYSTEM_LOOPBACK_THIRD_PARTY_APP_EXIT</td>

<td rowspan="1" colSpan="1" >-1324</td>

<td rowspan="1" colSpan="1" >An error occurred during the mixing and acquisition process of the third-party application. This error may occur after the third-party application's mixing process starts successfully, but the specified process or application unexpectedly exits during the sound acquisition process. Please check the status of the specified process or application. You can try retrying by re-entering the process ID.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_ENTER_ROOM_FAILED</td>

<td rowspan="1" colSpan="1" >-3301</td>

<td rowspan="1" colSpan="1" >Failed to enter the room. Please view -3301 in onError to confirm the message for the reason of the failure.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_REQUEST_IP_TIMEOUT</td>

<td rowspan="1" colSpan="1" >-3307</td>

<td rowspan="1" colSpan="1" >Request for IP and Sig timed out. Please check whether your network is functioning properly and whether UDP is unblocked in your network firewall.<br>You can try to access the following IPs: 162.14.22.165:8000, 162.14.6.105:8000 and the domain: default-query.trtc.tencent-cloud.com:8000</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_CONNECT_SERVER_TIMEOUT</td>

<td rowspan="1" colSpan="1" >-3308</td>

<td rowspan="1" colSpan="1" >Request for room entry timed out. Please check your network connection or whether you are on a VPN. You can also try switching to 4G for confirmation.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_ROOM_PARAM_NULL</td>

<td rowspan="1" colSpan="1" >-3316</td>

<td rowspan="1" colSpan="1" >Join Room Parameters are empty. Please check: enterRoom:appScene: whether the valid parameters were passed during the interface call</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_INVALID_SDK_APPID</td>

<td rowspan="1" colSpan="1" >-3317</td>

<td rowspan="1" colSpan="1" >Join Room Parameters sdkAppId is incorrect. Please check whether TRTCParams.sdkAppId is empty</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_INVALID_ROOM_ID</td>

<td rowspan="1" colSpan="1" >-3318</td>

<td rowspan="1" colSpan="1" >Join Room Parameters roomId is incorrect. Please check whether TRTCParams.roomId or TRTCParams.strRoomId is empty. Note that roomId and strRoomId cannot be used interchangeably</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_INVALID_USER_ID</td>

<td rowspan="1" colSpan="1" >-3319</td>

<td rowspan="1" colSpan="1" >Join Room Parameters userId is incorrect. Please check whether TRTCParams.userId is empty</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_INVALID_USER_SIG</td>

<td rowspan="1" colSpan="1" >-3320</td>

<td rowspan="1" colSpan="1" >Join Room Parameters userSig is incorrect. Please check whether TRTCParams.userSig is empty</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_ENTER_ROOM_REFUSED</td>

<td rowspan="1" colSpan="1" >-3340</td>

<td rowspan="1" colSpan="1" >Join Room request was denied. Please check whether you continuously invoked enterRoom for the same ID room</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_INVALID_PRIVATE_MAPKEY</td>

<td rowspan="1" colSpan="1" >-100006</td>

<td rowspan="1" colSpan="1" >You have enabled Advanced Permission Control, but the parameter TRTCParams.privateMapKey failed to verify<br>You can refer to [Advanced Permission Control](https://cloud.tencent.com/document/product/647/32240) for checks</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_SERVICE_SUSPENDED</td>

<td rowspan="1" colSpan="1" >-100013</td>

<td rowspan="1" colSpan="1" >Unavailable service. Please check whether the remaining validity period in minutes in the package is greater than 0 and whether the Tencent Cloud account is in arrears.<br>You can refer to [Package management](https://cloud.tencent.com/document/product/647/50492) for viewing and configuration</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_USER_SIG_CHECK_FAILED</td>

<td rowspan="1" colSpan="1" >-100018</td>

<td rowspan="1" colSpan="1" >UserSig verification failed. Please check whether the parameters TRTCParams.userSig are filled correctly or have expired.<br>You can refer to [UserSig Generation and Verification](https://cloud.tencent.com/document/product/647/50686) for verification</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_PUSH_THIRD_PARTY_CLOUD_TIMEOUT</td>

<td rowspan="1" colSpan="1" >-3321</td>

<td rowspan="1" colSpan="1" >The relayed push request timed out</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_MIX_TRANSCODING_TIMEOUT</td>

<td rowspan="1" colSpan="1" >-3322</td>

<td rowspan="1" colSpan="1" >The On-Cloud MixTranscoding request timed out</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_PUSH_THIRD_PARTY_CLOUD_FAILED</td>

<td rowspan="1" colSpan="1" >-3323</td>

<td rowspan="1" colSpan="1" >Exception in Relay to CDN Callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_MIX_TRANSCODING_FAILED</td>

<td rowspan="1" colSpan="1" >-3324</td>

<td rowspan="1" colSpan="1" >Exception in Cloud Mixed Streaming Callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_START_PUBLISHING_TIMEOUT</td>

<td rowspan="1" colSpan="1" >-3333</td>

<td rowspan="1" colSpan="1" >Signaling timed out when starting pushing to Tencent Cloud LVB CDN</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_START_PUBLISHING_FAILED</td>

<td rowspan="1" colSpan="1" >-3334</td>

<td rowspan="1" colSpan="1" >Signaling was exceptional when starting pushing to Tencent Cloud LVB CDN</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_STOP_PUBLISHING_TIMEOUT</td>

<td rowspan="1" colSpan="1" >-3335</td>

<td rowspan="1" colSpan="1" >Signaling timed out when stopping pushing to Tencent Cloud LVB CDN</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_STOP_PUBLISHING_FAILED</td>

<td rowspan="1" colSpan="1" >-3336</td>

<td rowspan="1" colSpan="1" >Signaling was exceptional when stopping pushing to Tencent Cloud LVB CDN</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_CONNECT_OTHER_ROOM_TIMEOUT</td>

<td rowspan="1" colSpan="1" >-3326</td>

<td rowspan="1" colSpan="1" >Request for mic connection timed out</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_DISCONNECT_OTHER_ROOM_TIMEOUT</td>

<td rowspan="1" colSpan="1" >-3327</td>

<td rowspan="1" colSpan="1" >Request to exit mic connection timed out</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_CONNECT_OTHER_ROOM_INVALID_PARAMETER</td>

<td rowspan="1" colSpan="1" >-3328</td>

<td rowspan="1" colSpan="1" >Invalid parameter</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_CONNECT_OTHER_ROOM_AS_AUDIENCE</td>

<td rowspan="1" colSpan="1" >-3330</td>

<td rowspan="1" colSpan="1" >Currently in audience role. Cannot request or disconnect cross-room mic connection. Please first ` switchRole ` to anchor</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_BGM_OPEN_FAILED</td>

<td rowspan="1" colSpan="1" >-4001</td>

<td rowspan="1" colSpan="1" >Failed to open file, such as invalid audio data, FFMPEG protocol not found, etc</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_BGM_DECODE_FAILED</td>

<td rowspan="1" colSpan="1" >-4002</td>

<td rowspan="1" colSpan="1" >Audio file decoding failed</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_BGM_OVER_LIMIT</td>

<td rowspan="1" colSpan="1" >-4003</td>

<td rowspan="1" colSpan="1" >Quantity exceeds the limit, such as preloading two background music tracks simultaneously</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_BGM_INVALID_OPERATION</td>

<td rowspan="1" colSpan="1" >-4004</td>

<td rowspan="1" colSpan="1" >Invalid operation, such as calling preload operation after starting playback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_BGM_INVALID_PATH</td>

<td rowspan="1" colSpan="1" >-4005</td>

<td rowspan="1" colSpan="1" >Invalid path causing file opening failure. Please check if the path parameter points to a valid music file</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_BGM_INVALID_URL</td>

<td rowspan="1" colSpan="1" >-4006</td>

<td rowspan="1" colSpan="1" >Invalid URL causing file opening failure. Please check in the browser if the provided URL address can download the intended music file</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_BGM_NO_AUDIO_STREAM</td>

<td rowspan="1" colSpan="1" >-4007</td>

<td rowspan="1" colSpan="1" >No audio stream causing file opening failure. Please confirm the file is a valid audio file and is not corrupted</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_BGM_FORMAT_NOT_SUPPORTED</td>

<td rowspan="1" colSpan="1" >-4008</td>

<td rowspan="1" colSpan="1" >Unsupported format causing file opening failure. Please confirm if the file format is supported. Mobile supports [mp3, aac, m4a, wav, ogg, mp4, mkv], and desktop supports [mp3, aac, m4a, wav, mp4, mkv]</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_CONCURRENT_BGM_OVER_LIMIT</td>

<td rowspan="1" colSpan="1" >-4009</td>

<td rowspan="1" colSpan="1" >The number of background music tracks (BGMs) playing simultaneously has exceeded the limit. If this error message appears after the number of BGMs playing simultaneously exceeds 10, please check the number of concurrently playing BGMs.</td>
</tr>
</table>


## TXLiteAVWarning



#### 警告码。
<table>
<tr>
<td rowspan="1" colSpan="1" >Enumeration</td>

<td rowspan="1" colSpan="1" >Value</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_HW_ENCODER_START_FAIL</td>

<td rowspan="1" colSpan="1" >1103</td>

<td rowspan="1" colSpan="1" >Issue with starting hardware encoding, automatically switched to software encoding</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_CURRENT_ENCODE_TYPE_CHANGED</td>

<td rowspan="1" colSpan="1" >1104</td>

<td rowspan="1" colSpan="1" >Indicates a change in the encoder. You can get the current encoding format and type through the relevant fields in the extended information of the onWarning function.<br>A value of 0 in the 'type' field represents H.264 encoding, and 1 represents H.265 encoding<br>A value of 0 in the 'hardware' field represents software encoding, and 1 represents hardware encoding<br>A value of 0 in the 'stream' field represents a large stream, 1 represents a small stream, and 2 represents an auxiliary stream</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_VIDEO_ENCODER_SW_TO_HW</td>

<td rowspan="1" colSpan="1" >1107</td>

<td rowspan="1" colSpan="1" >The current CPU utilization is too high to meet software encoding needs, and the hardware encoder was automatically switch to</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_INSUFFICIENT_CAPTURE_FPS</td>

<td rowspan="1" colSpan="1" >1108</td>

<td rowspan="1" colSpan="1" >Insufficient frame rate for video capturing through camera. This error may occur in Android mobile devices with an in-built beauty filter algorithm</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_SW_ENCODER_START_FAIL</td>

<td rowspan="1" colSpan="1" >1109</td>

<td rowspan="1" colSpan="1" >Failed to enable the software encoder</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_REDUCE_CAPTURE_RESOLUTION</td>

<td rowspan="1" colSpan="1" >1110</td>

<td rowspan="1" colSpan="1" >Camera resolution reduced for balance between frame rate and performance.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_CAMERA_DEVICE_EMPTY</td>

<td rowspan="1" colSpan="1" >1111</td>

<td rowspan="1" colSpan="1" >No available camera device detected</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_CAMERA_NOT_AUTHORIZED</td>

<td rowspan="1" colSpan="1" >1112</td>

<td rowspan="1" colSpan="1" >The current application is not authorized to use the camera</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_OUT_OF_MEMORY</td>

<td rowspan="1" colSpan="1" >1113</td>

<td rowspan="1" colSpan="1" >Insufficient memory, some features may not function properly.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_CAMERA_IS_OCCUPIED</td>

<td rowspan="1" colSpan="1" >1114</td>

<td rowspan="1" colSpan="1" >The camera is being used.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_CAMERA_DEVICE_ERROR</td>

<td rowspan="1" colSpan="1" >1115</td>

<td rowspan="1" colSpan="1" >Device anomaly with the camera.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_CAMERA_DISCONNECTED</td>

<td rowspan="1" colSpan="1" >1116</td>

<td rowspan="1" colSpan="1" >Unable to connect to the camera.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_CAMERA_START_FAILED</td>

<td rowspan="1" colSpan="1" >1117</td>

<td rowspan="1" colSpan="1" >Failed to start the camera.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_CAMERA_SERVER_DIED</td>

<td rowspan="1" colSpan="1" >1118</td>

<td rowspan="1" colSpan="1" >System anomaly.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_SCREEN_CAPTURE_NOT_AUTHORIZED</td>

<td rowspan="1" colSpan="1" >1206</td>

<td rowspan="1" colSpan="1" >The current application is not authorized to use screen recording</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_CURRENT_DECODE_TYPE_CHANGED</td>

<td rowspan="1" colSpan="1" >2008</td>

<td rowspan="1" colSpan="1" >Indicates a change in the decoder. You can get the current decoding format through the 'type' field in the extended information of the onWarning function.<br>Among them, 1 represents 265 decoding, and 0 represents 264 decoding. Note that this error code's extended information is not supported on Windows.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_VIDEO_FRAME_DECODE_FAIL</td>

<td rowspan="1" colSpan="1" >2101</td>

<td rowspan="1" colSpan="1" >Failed to decode the current video frame</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_HW_DECODER_START_FAIL</td>

<td rowspan="1" colSpan="1" >2106</td>

<td rowspan="1" colSpan="1" >Failed to enable the hardware decoder, and the software decoder was used</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_VIDEO_DECODER_HW_TO_SW</td>

<td rowspan="1" colSpan="1" >2108</td>

<td rowspan="1" colSpan="1" >The hardware decoder failed to decode the first I frame of the current stream, and the SDK automatically switched to the software decoder</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_SW_DECODER_START_FAIL</td>

<td rowspan="1" colSpan="1" >2109</td>

<td rowspan="1" colSpan="1" >Failed to enable the software decoder</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_VIDEO_RENDER_FAIL</td>

<td rowspan="1" colSpan="1" >2110</td>

<td rowspan="1" colSpan="1" >Failed to render video</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_VIRTUAL_BACKGROUND_DEVICE_UNSURPORTED</td>

<td rowspan="1" colSpan="1" >8001</td>

<td rowspan="1" colSpan="1" >Virtual background device not supported</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_VIRTUAL_BACKGROUND_NOT_AUTHORIZED</td>

<td rowspan="1" colSpan="1" >8002</td>

<td rowspan="1" colSpan="1" >Virtual background not authorized</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_VIRTUAL_BACKGROUND_INVALID_PARAMETER</td>

<td rowspan="1" colSpan="1" >8003</td>

<td rowspan="1" colSpan="1" >Virtual background parameter exception</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_VIRTUAL_BACKGROUND_PERFORMANCE_INSUFFICIENT</td>

<td rowspan="1" colSpan="1" >8004</td>

<td rowspan="1" colSpan="1" >Insufficient virtual background performance</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_MICROPHONE_DEVICE_EMPTY</td>

<td rowspan="1" colSpan="1" >1201</td>

<td rowspan="1" colSpan="1" >No available mic device detected</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_SPEAKER_DEVICE_EMPTY</td>

<td rowspan="1" colSpan="1" >1202</td>

<td rowspan="1" colSpan="1" >No available speaker device detected</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_MICROPHONE_NOT_AUTHORIZED</td>

<td rowspan="1" colSpan="1" >1203</td>

<td rowspan="1" colSpan="1" >The current application is not authorized to use the mic</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_MICROPHONE_DEVICE_ABNORMAL</td>

<td rowspan="1" colSpan="1" >1204</td>

<td rowspan="1" colSpan="1" >The audio capture device is unavailable (for example, it is in use or the PC determines it as an invalid device)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_SPEAKER_DEVICE_ABNORMAL</td>

<td rowspan="1" colSpan="1" >1205</td>

<td rowspan="1" colSpan="1" >The audio playback device is unavailable (for example, it is in use or the PC determines it as an invalid device)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_BLUETOOTH_DEVICE_CONNECT_FAIL</td>

<td rowspan="1" colSpan="1" >1207</td>

<td rowspan="1" colSpan="1" >Bluetooth device connection failed (for example, other applications occupying the audio channel through setting the call volume)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_MICROPHONE_IS_OCCUPIED</td>

<td rowspan="1" colSpan="1" >1208</td>

<td rowspan="1" colSpan="1" >Audio capture device is occupied</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_AUDIO_FRAME_DECODE_FAIL</td>

<td rowspan="1" colSpan="1" >2102</td>

<td rowspan="1" colSpan="1" >Failed to decode the current audio frame</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_AUDIO_RECORDING_WRITE_FAIL</td>

<td rowspan="1" colSpan="1" >7001</td>

<td rowspan="1" colSpan="1" >Failed to write the recorded audio to a file</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_MICROPHONE_HOWLING_DETECTED</td>

<td rowspan="1" colSpan="1" >7002</td>

<td rowspan="1" colSpan="1" >Howling detected while recording audio</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_IGNORE_UPSTREAM_FOR_AUDIENCE</td>

<td rowspan="1" colSpan="1" >6001</td>

<td rowspan="1" colSpan="1" >Currently in audience role, publishing audio and video is not supported. Please switch to the anchor role first</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_UPSTREAM_AUDIO_AND_VIDEO_OUT_OF_SYNC</td>

<td rowspan="1" colSpan="1" >6006</td>

<td rowspan="1" colSpan="1" >Abnormal timestamp of audio and video transmission, which may cause audio and video out of sync issues</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_RECONNECT_ON_SERVER_STATUS_ABNORMAL</td>

<td rowspan="1" colSpan="1" >6007</td>

<td rowspan="1" colSpan="1" >The server is experiencing an error and is reconnecting</td>
</tr>
</table>
