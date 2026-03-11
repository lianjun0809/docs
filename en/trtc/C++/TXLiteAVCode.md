> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

# TRTC Real-Time Communication (TRTC SDK) Documentation
## Overview
`TXLiteAVCode.h` provides status code definitions for TRTC Real-Time Communication (TRTC SDK) on C++. This file is used to notify developers of warnings and errors that occur while using TRTC.


## Enumeration Types
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



#### Error Code
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

<td rowspan="1" colSpan="1" >The current API does not support calls</td>
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

<td rowspan="1" colSpan="1" >Disconnect</td>
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

<td rowspan="1" colSpan="1" >No permission to send auxiliary stream</td>
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

<td rowspan="1" colSpan="1" >Custom video capture: Unsupported pixel format</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_BUFFER_TYPE_UNSUPPORTED</td>

<td rowspan="1" colSpan="1" >-1328</td>

<td rowspan="1" colSpan="1" >Custom video capture: Unsupported buffer type</td>
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
<td rowspan="1" colSpan="1" >ERR_MIC_SET_PARAM_FAIL</td>

<td rowspan="1" colSpan="1" >-1318</td>

<td rowspan="1" colSpan="1" >Failed to set microphone parameters.</td>
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

<td rowspan="1" colSpan="1" >Failed to enable system sound recording; for example, the audio driver plugin was unavailable</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_AUDIO_PLUGIN_INSTALL_NOT_AUTHORIZED</td>

<td rowspan="1" colSpan="1" >-1331</td>

<td rowspan="1" colSpan="1" >Unauthorized audio driver plugin installation</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_AUDIO_PLUGIN_INSTALL_FAILED</td>

<td rowspan="1" colSpan="1" >-1332</td>

<td rowspan="1" colSpan="1" >Failed to install audio driver plugin</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_AUDIO_PLUGIN_INSTALLED_BUT_NEED_RESTART</td>

<td rowspan="1" colSpan="1" >-1333</td>

<td rowspan="1" colSpan="1" >Successfully installed virtual sound card plugin, but features are temporarily unavailable after the first installation due to macOS system restrictions. Please advise the user to restart the current app upon receiving this error code</td>
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

<td rowspan="1" colSpan="1" >System mixing startup error. Common causes and solutions: 1. The current system version is unsupported. Specific process exclusion feature requires Windows System to be 10.0.19042 (20H2) or higher. Path mixing feature x64 version requires Windows System to be 10.0.19042 (20H2) or higher. Please check the current system version. 2. Invalid input parameters (including empty parameters, nonexistent path, nonexistent process ID, nonexistent device name). Please check the validity of input parameters. 3. No available speaker device, please check availability</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_SYSTEM_LOOPBACK_THIRD_PARTY_APP_EXIT</td>

<td rowspan="1" colSpan="1" >-1324</td>

<td rowspan="1" colSpan="1" >Third party application mixing and acquisition error. This error may occur after the third party application mixing starts successfully. During the sound acquisition process, the specified process or application may exit unexpectedly. Please check the state of the specified process or application, and try again by re-entering the process ID</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_ENTER_ROOM_FAILED</td>

<td rowspan="1" colSpan="1" >-3301</td>

<td rowspan="1" colSpan="1" >Failed to enter the room. Please view -3301 in onError to confirm the message for the reason of the failure.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_REQUEST_IP_TIMEOUT</td>

<td rowspan="1" colSpan="1" >-3307</td>

<td rowspan="1" colSpan="1" >Request for IP and Sig timed out. Please check whether your network is functioning properly and whether UDP is unblocked in your network firewall.<br>You can try accessing the following IPs: 162.14.22.165:8000, 162.14.6.105:8000 and domain name: default-query.trtc.tencent-cloud.com:8000</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_CONNECT_SERVER_TIMEOUT</td>

<td rowspan="1" colSpan="1" >-3308</td>

<td rowspan="1" colSpan="1" >Request for room entry timed out. Please check your network connection or whether you are on a VPN. You can also try switching to 4G for confirmation.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_ROOM_PARAM_NULL</td>

<td rowspan="1" colSpan="1" >-3316</td>

<td rowspan="1" colSpan="1" >Join Room Parameters are empty. Please check if the enterRoom:appScene: interface call has a valid param</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_INVALID_SDK_APPID</td>

<td rowspan="1" colSpan="1" >-3317</td>

<td rowspan="1" colSpan="1" >Join Room Parameter sdkAppId is incorrect. Please check if TRTCParams.sdkAppId is empty</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_INVALID_ROOM_ID</td>

<td rowspan="1" colSpan="1" >-3318</td>

<td rowspan="1" colSpan="1" >Join Room Parameter roomId is incorrect. Please check if TRTCParams.roomId or TRTCParams.strRoomId is empty. Note that roomId and strRoomId cannot be used interchangeably</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_INVALID_USER_ID</td>

<td rowspan="1" colSpan="1" >-3319</td>

<td rowspan="1" colSpan="1" >Join Room Parameter userId is incorrect. Please check if TRTCParams.userId is empty</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_INVALID_USER_SIG</td>

<td rowspan="1" colSpan="1" >-3320</td>

<td rowspan="1" colSpan="1" >Join Room Parameter userSig is incorrect. Please check if TRTCParams.userSig is empty</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_ENTER_ROOM_REFUSED</td>

<td rowspan="1" colSpan="1" >-3340</td>

<td rowspan="1" colSpan="1" >Join Room Request was rejected. Please check if you are continuously calling enterRoom to enter the room with the same Id</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_INVALID_PRIVATE_MAPKEY</td>

<td rowspan="1" colSpan="1" >-100006</td>

<td rowspan="1" colSpan="1" >You have enabled Advanced Permission Control, but the parameter TRTCParams.privateMapKey failed verification<br>You can refer to [Advanced Permission Control](https://cloud.tencent.com/document/product/647/32240) for inspection</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_SERVICE_SUSPENDED</td>

<td rowspan="1" colSpan="1" >-100013</td>

<td rowspan="1" colSpan="1" >Unavailable service. Please check whether the remained validity period in minutes in the package is greater than 0 and whether the Tencent Cloud account is in arrears.<br>You can refer to [Package Management](https://cloud.tencent.com/document/product/647/50492) for viewing and configuration</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_USER_SIG_CHECK_FAILED</td>

<td rowspan="1" colSpan="1" >-100018</td>

<td rowspan="1" colSpan="1" >UserSig verification failed. Please check if the parameter TRTCParams.userSig is filled correctly or if it has expired.<br>You can refer to [UserSig Generation and Verification](https://cloud.tencent.com/document/product/647/50686) for validation</td>
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

<td rowspan="1" colSpan="1" >Relay to CDN callback exception</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_MIX_TRANSCODING_FAILED</td>

<td rowspan="1" colSpan="1" >-3324</td>

<td rowspan="1" colSpan="1" >The On-Cloud MixTranscoding callback exception</td>
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

<td rowspan="1" colSpan="1" >Request for cross-room mic connection timed out</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_DISCONNECT_OTHER_ROOM_TIMEOUT</td>

<td rowspan="1" colSpan="1" >-3327</td>

<td rowspan="1" colSpan="1" >Request to exit cross-room mic connection timed out</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_CONNECT_OTHER_ROOM_INVALID_PARAMETER</td>

<td rowspan="1" colSpan="1" >-3328</td>

<td rowspan="1" colSpan="1" >Invalid parameter</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_CONNECT_OTHER_ROOM_AS_AUDIENCE</td>

<td rowspan="1" colSpan="1" >-3330</td>

<td rowspan="1" colSpan="1" >You are currently in Audience Role and cannot request or disconnect cross-room mic connection. You need to `switchRole` to an anchor</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_BGM_OPEN_FAILED</td>

<td rowspan="1" colSpan="1" >-4001</td>

<td rowspan="1" colSpan="1" >Failed to open file due to reasons like invalid audio data or FFMPEG Protocol not found</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_BGM_DECODE_FAILED</td>

<td rowspan="1" colSpan="1" >-4002</td>

<td rowspan="1" colSpan="1" >Failed to decode audio file</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_BGM_OVER_LIMIT</td>

<td rowspan="1" colSpan="1" >-4003</td>

<td rowspan="1" colSpan="1" >Quantity exceeds the limit, such as preloading two background music tracks simultaneously</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_BGM_INVALID_OPERATION</td>

<td rowspan="1" colSpan="1" >-4004</td>

<td rowspan="1" colSpan="1" >Invalid operation, such as calling preloading after starting playback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_BGM_INVALID_PATH</td>

<td rowspan="1" colSpan="1" >-4005</td>

<td rowspan="1" colSpan="1" >Failed to open file due to illegal path. Please check if the provided path parameter points to a valid music file</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_BGM_INVALID_URL</td>

<td rowspan="1" colSpan="1" >-4006</td>

<td rowspan="1" colSpan="1" >Failed to open file due to illegal URL. Please check with a browser if the provided URL can download the expected music file</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_BGM_NO_AUDIO_STREAM</td>

<td rowspan="1" colSpan="1" >-4007</td>

<td rowspan="1" colSpan="1" >Failed to open file due to no audio stream. Please ensure the provided file is a valid audio file and is not corrupted</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_BGM_FORMAT_NOT_SUPPORTED</td>

<td rowspan="1" colSpan="1" >-4008</td>

<td rowspan="1" colSpan="1" >Failed to open file due to unsupported format. Please check if the provided file format is supported. Mobile supports [mp3, aac, m4a, wav, ogg, mp4, mkv], desktop supports [mp3, aac, m4a, wav, mp4, mkv]</td>
</tr>
</table>


## TXLiteAVWarning



#### Warning Codes
<table>
<tr>
<td rowspan="1" colSpan="1" >Enumeration</td>

<td rowspan="1" colSpan="1" >Value</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_HW_ENCODER_START_FAIL</td>

<td rowspan="1" colSpan="1" >1103</td>

<td rowspan="1" colSpan="1" >Problem with enabling hardware encoding, switched to software encoding automatically</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_CURRENT_ENCODE_TYPE_CHANGED</td>

<td rowspan="1" colSpan="1" >1104</td>

<td rowspan="1" colSpan="1" >Indicates encoder change; detailed encoding format and type can be retrieved from relevant fields in the onWarning function's extended information.<br>Field 'type' value 0 represents H.264 encoding, 1 represents H.265 encoding<br>Field 'hardware' value 0 represents software encoding, 1 represents hardware encoding<br>Field 'stream' value 0 represents large stream, 1 represents small stream, 2 represents auxiliary stream</td>
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

<td rowspan="1" colSpan="1" >Camera device abnormal.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_CAMERA_DISCONNECTED</td>

<td rowspan="1" colSpan="1" >1116</td>

<td rowspan="1" colSpan="1" >Camera connection failed.</td>
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

<td rowspan="1" colSpan="1" >Indicates decoder change; the current decoding format can be retrieved from the type field in the onWarning function's extended information.<br>Here, 1 represents 265 decoding, and 0 represents 264 decoding. Note that this error code's extended information is not supported on Windows.</td>
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

<td rowspan="1" colSpan="1" >Virtual background parameter abnormal</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_VIRTUAL_BACKGROUND_PERFORMANCE_INSUFFICIENT</td>

<td rowspan="1" colSpan="1" >8004</td>

<td rowspan="1" colSpan="1" >Virtual background performance insufficient</td>
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

<td rowspan="1" colSpan="1" >Audio capture device is unavailable (e.g., in use or deemed invalid by PC)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_SPEAKER_DEVICE_ABNORMAL</td>

<td rowspan="1" colSpan="1" >1205</td>

<td rowspan="1" colSpan="1" >Audio playback device is unavailable (e.g., in use or deemed invalid by PC)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_BLUETOOTH_DEVICE_CONNECT_FAIL</td>

<td rowspan="1" colSpan="1" >1207</td>

<td rowspan="1" colSpan="1" >Bluetooth device connection failed (e.g., audio channel occupied by another app setting call volume)</td>
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

<td rowspan="1" colSpan="1" >Howling detected during audio recording</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_IGNORE_UPSTREAM_FOR_AUDIENCE</td>

<td rowspan="1" colSpan="1" >6001</td>

<td rowspan="1" colSpan="1" >You are currently in Audience Role and cannot publish audio or video. You need to switch to an anchor role</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_UPSTREAM_AUDIO_AND_VIDEO_OUT_OF_SYNC</td>

<td rowspan="1" colSpan="1" >6006</td>

<td rowspan="1" colSpan="1" >Audio and video sending timestamp abnormal, may cause audio and video out of sync issues</td>
</tr>
</table>
