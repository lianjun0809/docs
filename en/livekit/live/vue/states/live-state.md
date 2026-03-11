> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/en/llms.txt
> Use this file to discover all available pages before exploring further.

The atomicx-core SDK is a brand-new first-generation responsive API launched by Tencent Cloud for Chat, Audio/Video Calls, live streaming, voice chat room and other scenarios. You can quickly build your own UI page based on this set of APIs. It supports room management, screen sharing, member management, microphone position control, basic beauty filter and other rich features. Based on the TRTC SDK, it can provide ultra-low latency and high-quality audio/video experience. This page contains ALL API interfaces of the atomicx-core SDK, displayed by feature module.


## LoginState


User Identity Authentication and Logon Management Module
-Core features: Provide basic identity authentication including user login, logout, and personal information management, forming the user identity basis of the entire system.


- Technical features: Support various log-in methods, user information cache, login status persistence and other features to underwrite user identity security and reliability.


- Business value: Provides unified user identity authentication service for all business modules, forming the foundation of system security and user experience assurance.


- Application scenarios: Core identity authentication scenarios such as user login, identity verification, personal information management, and permission control.




   responsive data


<table>
<tr>
<td rowspan="1" colSpan="1" >**Data List**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[loginUserInfo](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#loginUserInfo)</td>


<td rowspan="1" colSpan="1" >Current login user information.</td>
</tr>
</table>




   API Function


<table>
<tr>
<td rowspan="1" colSpan="1" >**Function list**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[login](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#login)</td>


<td rowspan="1" colSpan="1" >User login.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[setSelfInfo](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setSelfInfo)</td>


<td rowspan="1" colSpan="1" >Set user personal information.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[logout](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#logout)</td>


<td rowspan="1" colSpan="1" >User logout function.</td>
</tr>
</table>




## DeviceState


Device Status Management Module
-Core feature: Manage control of cameras, microphones and other audio/video devices, providing device status monitoring, permission check and other basic equipment services.


- Technical feature: Supports advanced functions such as multi-device management, real-time status monitoring, dynamic permission check, and automatic failure recovery.


- Business value: Provide stability to the live streaming system, underwriting the reliability of audio and video capture and user experience.


- Use cases: Basic technical scenarios such as device management, permission control, audio and video capture, and fault handling.




   responsive data


<table>
<tr>
<td rowspan="1" colSpan="1" >**Data List**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[microphoneStatus](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#microphoneStatus)</td>


<td rowspan="1" colSpan="1" >Microphone Status.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[microphoneList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#microphoneList)</td>


<td rowspan="1" colSpan="1" >Microphone Device List.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[currentMicrophone](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#currentMicrophone)</td>


<td rowspan="1" colSpan="1" >Selected microphone device.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[microphoneLastError](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#microphoneLastError)</td>


<td rowspan="1" colSpan="1" >Last microphone error information.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[captureVolume](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#captureVolume)</td>


<td rowspan="1" colSpan="1" >Mic capture volume.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[currentMicVolume](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#currentMicVolume)</td>


<td rowspan="1" colSpan="1" >Current microphone volume.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[isMicrophoneTesting](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isMicrophoneTesting)</td>


<td rowspan="1" colSpan="1" >Mic testing status.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[testingMicVolume](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#testingMicVolume)</td>


<td rowspan="1" colSpan="1" >Microphone volume during testing.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[cameraStatus](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#cameraStatus)</td>


<td rowspan="1" colSpan="1" >Camera status.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[cameraList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#cameraList)</td>


<td rowspan="1" colSpan="1" >Camera list.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[currentCamera](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#currentCamera)</td>


<td rowspan="1" colSpan="1" >Selected camera.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[cameraLastError](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#cameraLastError)</td>


<td rowspan="1" colSpan="1" >Last camera error information.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[isCameraTesting](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isCameraTesting)</td>


<td rowspan="1" colSpan="1" >Camera test status.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[isCameraTestLoading](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isCameraTestLoading)</td>


<td rowspan="1" colSpan="1" >Camera test loading status.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[isFrontCamera](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isFrontCamera)</td>


<td rowspan="1" colSpan="1" >Whether the camera is front-facing.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[localMirrorType](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#localMirrorType)</td>


<td rowspan="1" colSpan="1" >Local video image type.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[localVideoQuality](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#localVideoQuality)</td>


<td rowspan="1" colSpan="1" >Local video quality.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[speakerList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#speakerList)</td>


<td rowspan="1" colSpan="1" >Speaker Device List.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[currentSpeaker](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#currentSpeaker)</td>


<td rowspan="1" colSpan="1" >Selected speaker device.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[outputVolume](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#outputVolume)</td>


<td rowspan="1" colSpan="1" >Speaker output volume.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[currentAudioRoute](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#currentAudioRoute)</td>


<td rowspan="1" colSpan="1" >Current audio routing.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[isSpeakerTesting](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isSpeakerTesting)</td>


<td rowspan="1" colSpan="1" >Speaker testing status.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[screenStatus](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#screenStatus)</td>


<td rowspan="1" colSpan="1" >Screen sharing status.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[networkInfo](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#networkInfo)</td>


<td rowspan="1" colSpan="1" >Network information.</td>
</tr>
</table>




   API Function


<table>
<tr>
<td rowspan="1" colSpan="1" >**Function list**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[openLocalMicrophone](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#openLocalMicrophone)</td>


<td rowspan="1" colSpan="1" >Open local microphone.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[closeLocalMicrophone](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#closeLocalMicrophone)</td>


<td rowspan="1" colSpan="1" >Close local microphone.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[muteLocalAudio](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#muteLocalAudio)</td>


<td rowspan="1" colSpan="1" >Mute local audio.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[unmuteLocalAudio](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#unmuteLocalAudio)</td>


<td rowspan="1" colSpan="1" >Unmute local audio.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[getMicrophoneList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getMicrophoneList)</td>


<td rowspan="1" colSpan="1" >Get microphone device list.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[setCurrentMicrophone](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setCurrentMicrophone)</td>


<td rowspan="1" colSpan="1" >Set current microphone device.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[startMicrophoneTest](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#startMicrophoneTest)</td>


<td rowspan="1" colSpan="1" >Start mic testing.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[setCaptureVolume](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setCaptureVolume)</td>


<td rowspan="1" colSpan="1" >Set audio capture volume.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[setOutputVolume](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setOutputVolume)</td>


<td rowspan="1" colSpan="1" >Set audio playback volume.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[stopMicrophoneTest](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#stopMicrophoneTest)</td>


<td rowspan="1" colSpan="1" >Stop mic testing.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[getSpeakerList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getSpeakerList)</td>


<td rowspan="1" colSpan="1" >Search speaker device list.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[setCurrentSpeaker](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setCurrentSpeaker)</td>


<td rowspan="1" colSpan="1" >Set current speaker device.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[setAudioRoute](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setAudioRoute)</td>


<td rowspan="1" colSpan="1" >Set audio routing.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[startSpeakerTest](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#startSpeakerTest)</td>


<td rowspan="1" colSpan="1" >Start speaker testing.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[stopSpeakerTest](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#stopSpeakerTest)</td>


<td rowspan="1" colSpan="1" >Stop speaker test.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[openLocalCamera](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#openLocalCamera)</td>


<td rowspan="1" colSpan="1" >Turn on local camera.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[closeLocalCamera](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#closeLocalCamera)</td>


<td rowspan="1" colSpan="1" >Turn off local camera.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[getCameraList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getCameraList)</td>


<td rowspan="1" colSpan="1" >Get camera list.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[setCurrentCamera](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setCurrentCamera)</td>


<td rowspan="1" colSpan="1" >Set current camera.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[switchCamera](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#switchCamera)</td>


<td rowspan="1" colSpan="1" >Switch between front and rear cameras.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[switchMirror](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#switchMirror)</td>


<td rowspan="1" colSpan="1" >Toggle video mirroring mode.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[updateVideoQuality](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#updateVideoQuality)</td>


<td rowspan="1" colSpan="1" >Refresh video quality.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[startCameraDeviceTest](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#startCameraDeviceTest)</td>


<td rowspan="1" colSpan="1" >Start camera test.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[startScreenShare](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#startScreenShare)</td>


<td rowspan="1" colSpan="1" >Start screen sharing.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[stopScreenShare](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#stopScreenShare)</td>


<td rowspan="1" colSpan="1" >Stop screen sharing.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[stopCameraDeviceTest](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#stopCameraDeviceTest)</td>


<td rowspan="1" colSpan="1" >Stop camera test.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[screenCaptureStopped](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#screenCaptureStopped)</td>


<td rowspan="1" colSpan="1" >Screen sharing stop callback.</td>
</tr>
</table>




## LiveListState


Live List Management Module
-Core features: Manage the complete lifecycle of live streaming rooms, including creation, join, leave, and end core business processes, support pagination fetch and real-time update of live lists.


- Technical features: Support load by page, real-time state synchronization, dynamic data updates of live information, implement responsive data management to ensure real-time synchronization between UI and data status. Newly-added liveList and liveListCursor responsive data, provide fetchLiveList API function.


- Business value: Provide core live room management capabilities for the live streaming platform, support large-scale concurrency in live-streaming scenarios, and serve as the infrastructure for the live streaming business.


- Application scenario: Core business scenarios such as live list display, live room creation, live stream status management, and live broadcast data statistics.




   responsive data


<table>
<tr>
<td rowspan="1" colSpan="1" >**Data List**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[currentLive](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#currentLive)</td>


<td rowspan="1" colSpan="1" >Switch TUILiveInfo to LiveInfo format.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[liveList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#liveList)</td>


<td rowspan="1" colSpan="1" >Live list data, including info of all live streaming rooms.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[liveListCursor](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#liveListCursor)</td>


<td rowspan="1" colSpan="1" >Live list pagination cursor, used to obtain next page data.</td>
</tr>
</table>




   API Function


<table>
<tr>
<td rowspan="1" colSpan="1" >**Function list**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[createLive](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#createLive)</td>


<td rowspan="1" colSpan="1" >Create a live streaming room.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[joinLive](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#joinLive)</td>


<td rowspan="1" colSpan="1" >Join live room.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[leaveLive](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#leaveLive)</td>


<td rowspan="1" colSpan="1" >Leave the live streaming room.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[endLive](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#endLive)</td>


<td rowspan="1" colSpan="1" >End live stream.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[updateLiveInfo](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#updateLiveInfo)</td>


<td rowspan="1" colSpan="1" >Refresh live room information.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[queryMetaData](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#queryMetaData)</td>


<td rowspan="1" colSpan="1" >Query metadata.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[updateLiveMetaData](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#updateLiveMetaData)</td>


<td rowspan="1" colSpan="1" >Update live room metadata.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[fetchLiveList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#fetchLiveList)</td>


<td rowspan="1" colSpan="1" >Get live list.</td>
</tr>
</table>




## LiveSeatState


Live Room Seat Management Module
-Core features: Implement seat control in microphone-connected scenarios, support complex seat status management and audio/video device control, including joining, leaving, seat lock and all features.


-Technical features: Based on WebRTC technology, it supports multiple media stream management and offers advanced functions like seat locking, device control, and permission management. Newly-added responsive data includes seatList, canvas, speakingUsers, and networkQualities, as well as a complete operation API for seats.


- Business value: Provide core technology support for multi-person interactive live streaming, supporting various interactive scenarios like PK, microphone connection, and multiplayer games.


- Application scenarios: Scenarios requiring multi-person audio and video interaction, such as co-anchoring, PK battles, interactive games, online education, and live conference streaming.




   responsive data


<table>
<tr>
<td rowspan="1" colSpan="1" >**Data List**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[seatList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#seatList)</td>


<td rowspan="1" colSpan="1" >Microphone position list, including ALL seat states and user information.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[canvas](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#canvas)</td>


<td rowspan="1" colSpan="1" >Canvas configuration for video rendering and layout management.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[speakingUsers](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#speakingUsers)</td>


<td rowspan="1" colSpan="1" >List of users speaking.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[networkQualities](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#networkQualities)</td>


<td rowspan="1" colSpan="1" >Network quality information, including user's network status.</td>
</tr>
</table>




   API Function


<table>
<tr>
<td rowspan="1" colSpan="1" >**Function list**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[takeSeat](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#takeSeat)</td>


<td rowspan="1" colSpan="1" >User joins the stage.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[leaveSeat](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#leaveSeat)</td>


<td rowspan="1" colSpan="1" >User Microphone Dequeuing.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[lockSeat](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#lockSeat)</td>


<td rowspan="1" colSpan="1" >Seat locking.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[unLockSeat](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#unLockSeat)</td>


<td rowspan="1" colSpan="1" >Unlock microphone position.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[kickUserOutOfSeat](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#kickUserOutOfSeat)</td>


<td rowspan="1" colSpan="1" >Remove users from speaking.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[moveUserToSeat](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#moveUserToSeat)</td>


<td rowspan="1" colSpan="1" >Move user to designated seat.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[openRemoteCamera](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#openRemoteCamera)</td>


<td rowspan="1" colSpan="1" >Enable remote camera.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[closeRemoteCamera](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#closeRemoteCamera)</td>


<td rowspan="1" colSpan="1" >Turn off remote camera.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[openRemoteMicrophone](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#openRemoteMicrophone)</td>


<td rowspan="1" colSpan="1" >Enable remote microphone.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[closeRemoteMicrophone](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#closeRemoteMicrophone)</td>


<td rowspan="1" colSpan="1" >Turn off remote microphone.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[muteMicrophone](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#muteMicrophone)</td>


<td rowspan="1" colSpan="1" >Mute microphone.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[unmuteMicrophone](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#unmuteMicrophone)</td>


<td rowspan="1" colSpan="1" >Unmute microphone.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[startPlayStream](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#startPlayStream)</td>


<td rowspan="1" colSpan="1" >Start playback.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[stopPlayStream](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#stopPlayStream)</td>


<td rowspan="1" colSpan="1" >Stop playback.</td>
</tr>
</table>




## LiveAudienceState


Live Room Audience Management Module
- Core features: Manage the audience list of live streaming rooms, provide permission control, admin settings and other maintenance features for live room order, support real-time audience statistics.


- Technical features: Support advanced functions such as real-time audience list update, permission hierarchy management, and batch operation to underwrite live room order and user experience. Newly-added responsive data: audienceList and audienceCount.


- Business value: Offer a complete audience management solution for the live streaming platform, supporting order maintenance in large-scale audience scenarios.


- Application scenario: Core business scenarios such as audience management, permission control, live streaming room order maintenance, and audience interaction management.




   responsive data


<table>
<tr>
<td rowspan="1" colSpan="1" >**Data List**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[audienceList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#audienceList)</td>


<td rowspan="1" colSpan="1" >Audience list, including info of all audience in the live streaming room.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[audienceCount](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#audienceCount)</td>


<td rowspan="1" colSpan="1" >Total number statistics of audience.</td>
</tr>
</table>




   API Function


<table>
<tr>
<td rowspan="1" colSpan="1" >**Function list**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[fetchAudienceList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#fetchAudienceList)</td>


<td rowspan="1" colSpan="1" >Retrieve audience list.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[setAdministrator](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setAdministrator)</td>


<td rowspan="1" colSpan="1" >Set administrator.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[revokeAdministrator](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#revokeAdministrator)</td>


<td rowspan="1" colSpan="1" >Revoke admin.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[kickUserOutOfRoom](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#kickUserOutOfRoom)</td>


<td rowspan="1" colSpan="1" >Kick out of room.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[disableSendMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#disableSendMessage)</td>


<td rowspan="1" colSpan="1" >Mute users.</td>
</tr>
</table>




## LiveMonitorState


Live Stream Monitoring Management Module
- Core features: Provide real-time monitoring for live streaming rooms, including live status monitoring, data statistics, anomaly detection and other core monitoring capabilities, support multi-room monitoring.


- Technical features: Support real-time data collection, multidimensional monitoring metrics, intelligent alarm mechanism to underwrite service stability and reliability. Newly-added monitorLiveInfoList responsive data, optimized monitoring interface.


- Business value: Offer comprehensive monitoring assurance for the live streaming platform, enabling timely detection and handling of anomalies to improve service quality.


- Application scenario: Operation management scenarios such as live stream quality monitoring, performance analysis, abnormal alarm, and data statistics.




   responsive data


<table>
<tr>
<td rowspan="1" colSpan="1" >**Data List**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[monitorLiveInfoList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#monitorLiveInfoList)</td>


<td rowspan="1" colSpan="1" >Live room monitoring list.</td>
</tr>
</table>




   API Function


<table>
<tr>
<td rowspan="1" colSpan="1" >**Function list**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[init](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#init)</td>


<td rowspan="1" colSpan="1" >Initialize monitoring.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[getLiveList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getLiveList)</td>


<td rowspan="1" colSpan="1" >Get live list.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[closeRoom](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#closeRoom)</td>


<td rowspan="1" colSpan="1" >Close the room.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[sendMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#sendMessage)</td>


<td rowspan="1" colSpan="1" >Send message.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[startPlay](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#startPlay)</td>


<td rowspan="1" colSpan="1" >Start playback.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[stopPlay](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#stopPlay)</td>


<td rowspan="1" colSpan="1" >Stop playback.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[muteLiveAudio](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#muteLiveAudio)</td>


<td rowspan="1" colSpan="1" >Mute live audio.</td>
</tr>
</table>




## CoGuestState


Guest management module
- Core features: Handle mic-connect interaction between audience and host, manage join microphone application, invitation, acceptance, rejection and other complete process, support status management.


- Technical features: Based on real-time audio and video technology, support advanced functions like real-time synchronization of mic-connect status, adaptive adjustment of audio/video quality, and network condition monitoring. Newly-added connected, invitees, applicants, candidates responsive data and applyForSeat API.


- Business value: Provide core audience interaction capabilities for the live streaming platform, enhance user stickiness and live stream fun.


- Application scenarios: Interactive scenarios requiring audience participation, such as audience mic connection, interactive Q&A, online karaoke, and game live streaming.




   responsive data


<table>
<tr>
<td rowspan="1" colSpan="1" >**Data List**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[candidates](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#candidates)</td>


<td rowspan="1" colSpan="1" >Unsubscription of co-streaming event.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[connected](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#connected)</td>


<td rowspan="1" colSpan="1" >Co-streaming Connection Status.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[invitees](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#invitees)</td>


<td rowspan="1" colSpan="1" >List of invited users.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[applicants](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#applicants)</td>


<td rowspan="1" colSpan="1" >List of users applying for mic connection.</td>
</tr>
</table>




   API Function


<table>
<tr>
<td rowspan="1" colSpan="1" >**Function list**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[cancelApplication](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#cancelApplication)</td>


<td rowspan="1" colSpan="1" >Cancel application.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[acceptApplication](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#acceptApplication)</td>


<td rowspan="1" colSpan="1" >Accept application.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[rejectApplication](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#rejectApplication)</td>


<td rowspan="1" colSpan="1" >Reject application.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[cancelInvitation](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#cancelInvitation)</td>


<td rowspan="1" colSpan="1" >Cancel invitation.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[acceptInvitation](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#acceptInvitation)</td>


<td rowspan="1" colSpan="1" >Accept invitation.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[rejectInvitation](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#rejectInvitation)</td>


<td rowspan="1" colSpan="1" >Reject invitation.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[disConnect](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#disConnect)</td>


<td rowspan="1" colSpan="1" >Disconnect.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[applyForSeat](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#applyForSeat)</td>


<td rowspan="1" colSpan="1" >Request to speak.</td>
</tr>
</table>




## CoHostState


Anchor management module
- Core features: Implement the co-anchoring function between hosts, support host invitations, join microphone applications, status management, and other interaction features, providing a complete co-anchoring process.


- Technical features: Support advanced technologies like multi-anchor audio-video synchronization, Picture-in-Picture display, and audio/video quality optimization to ensure smooth co-anchoring experience. Newly-added coHostStatus, connected, applicant, invitees, candidates responsive data and a complete co-anchoring control API.


- Business value: Provide core collaboration capabilities for hosts on live streaming platforms, supporting advanced business scenarios like PK and co-streaming.


- Application scenarios: Advanced live-streaming scenarios such as host PK battles, co-streaming, cross-platform voice chats, and host interactions.




   responsive data


<table>
<tr>
<td rowspan="1" colSpan="1" >**Data List**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[coHostStatus](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#coHostStatus)</td>


<td rowspan="1" colSpan="1" >Co-streaming Host Status.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[connected](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#connected)</td>


<td rowspan="1" colSpan="1" >Co-streaming Connection Status.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[applicant](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#applicant)</td>


<td rowspan="1" colSpan="1" >Host information applying for mic connection.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[invitees](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#invitees)</td>


<td rowspan="1" colSpan="1" >List of invited users.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[candidates](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#candidates)</td>


<td rowspan="1" colSpan="1" >List of candidate users.</td>
</tr>
</table>




   API Function


<table>
<tr>
<td rowspan="1" colSpan="1" >**Function list**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[requestHostConnection](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#requestHostConnection)</td>


<td rowspan="1" colSpan="1" >Request host mic connection.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[cancelHostConnection](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#cancelHostConnection)</td>


<td rowspan="1" colSpan="1" >Cancel host mic connection.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[acceptHostConnection](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#acceptHostConnection)</td>


<td rowspan="1" colSpan="1" >Accept host mic connection.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[rejectHostConnection](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#rejectHostConnection)</td>


<td rowspan="1" colSpan="1" >Reject host mic connection.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[exitHostConnection](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#exitHostConnection)</td>


<td rowspan="1" colSpan="1" >Exit host mic connection.</td>
</tr>
</table>




## BattleState


PK Battle Management Module
- Core features: Manage PK battles between hosts, including battle invitations, acceptance, rejection, and completion, supporting live score statistics.


- Technical features: Support real-time battle state synchronization, score calculation, results statistics and other features. Newly-added battleScore responsive data provides a complete PK battle experience.


- Business value: The platform offers competitive gaming interaction features to enhance live stream fun and user engagement.


- Application scenarios: Entertainment scenarios such as host PK battles, talent competitions, game battles, and interactive competitions.




   responsive data


<table>
<tr>
<td rowspan="1" colSpan="1" >**Data List**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[currentBattleInfo](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#currentBattleInfo)</td>


<td rowspan="1" colSpan="1" >Current PK info.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[battleUsers](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#battleUsers)</td>


<td rowspan="1" colSpan="1" >List of PK participants.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[battleScore](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#battleScore)</td>


<td rowspan="1" colSpan="1" >Live score of PK battle.</td>
</tr>
</table>




   API Function


<table>
<tr>
<td rowspan="1" colSpan="1" >**Function list**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[requestBattle](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#requestBattle)</td>


<td rowspan="1" colSpan="1" >Request PK.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[cancelBattleRequest](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#cancelBattleRequest)</td>


<td rowspan="1" colSpan="1" >Cancel battle request.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[acceptBattle](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#acceptBattle)</td>


<td rowspan="1" colSpan="1" >Accept PK.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[rejectBattle](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#rejectBattle)</td>


<td rowspan="1" colSpan="1" >Reject PK.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[exitBattle](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#exitBattle)</td>


<td rowspan="1" colSpan="1" >Exit PK.</td>
</tr>
</table>




## BarrageState


Bullet screen message management module
- Core features: Process text messages and custom messages in the live streaming room, support barrage sending, message status synchronization and complete danmaku system, provide local notification.


- Technical features: Support advanced functions like high-concurrency message processing, real-time message synchronization, message filtering, and emoji pack support. Newly-added API functions: sendTextMessage, sendCustomMessage, appendLocalTip.


- Business value: Provide core interactive capabilities for the live streaming platform, enhance user engagement and communication environment.


- Application scenarios: bullet screen interaction, message management, emoji pack, chat room, and other social interactive scenarios.




   responsive data


<table>
<tr>
<td rowspan="1" colSpan="1" >**Data List**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[messageList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#messageList)</td>


<td rowspan="1" colSpan="1" >Barrage message list.</td>
</tr>
</table>




   API Function


<table>
<tr>
<td rowspan="1" colSpan="1" >**Function list**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[sendTextMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#sendTextMessage)</td>


<td rowspan="1" colSpan="1" >Send text message.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[sendCustomMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#sendCustomMessage)</td>


<td rowspan="1" colSpan="1" >Send custom messages.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[appendLocalTip](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#appendLocalTip)</td>


<td rowspan="1" colSpan="1" >Add local prompt.</td>
</tr>
</table>




## MessageListState


Message List Management Module
- Core features: Manage chat message list, support message loading, scroll control, read receipt, and highlight for complete display functionality.


- Technical features: Support high-performance message processing like virtual scrolling, message optimization, and real-time update. Newly-added responsive data: activeConversationID, messageList, hasMoreOlderMessage.


- Business value: Provide core message display capacity for Chat to underwrite a good chat experience.


- Application scenarios: Chat, group chat, private chat, and message management in communication scenarios.




   responsive data


<table>
<tr>
<td rowspan="1" colSpan="1" >**Data List**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[activeConversationID](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#activeConversationID)</td>


<td rowspan="1" colSpan="1" >Current active session ID.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[messageList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#messageList)</td>


<td rowspan="1" colSpan="1" >Message list data.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[hasMoreOlderMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#hasMoreOlderMessage)</td>


<td rowspan="1" colSpan="1" >Whether there are more old messages.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[hasMoreNewerMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#hasMoreNewerMessage)</td>


<td rowspan="1" colSpan="1" >Whether there are more new messages.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[enableReadReceipt](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#enableReadReceipt)</td>


<td rowspan="1" colSpan="1" >Whether to enable read receipt.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[isDisableScroll](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isDisableScroll)</td>


<td rowspan="1" colSpan="1" >Whether to disable scrolling.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[recalledMessageIDSet](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#recalledMessageIDSet)</td>


<td rowspan="1" colSpan="1" >ID set of recalled messages.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[highlightMessageIDSet](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#highlightMessageIDSet)</td>


<td rowspan="1" colSpan="1" >ID set of highlight messages.</td>
</tr>
</table>




   API Function


<table>
<tr>
<td rowspan="1" colSpan="1" >**Function list**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[setEnableReadReceipt](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setEnableReadReceipt)</td>


<td rowspan="1" colSpan="1" >Set read receipt.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[setIsDisableScroll](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setIsDisableScroll)</td>


<td rowspan="1" colSpan="1" >Disable scrolling.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[highlightMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#highlightMessage)</td>


<td rowspan="1" colSpan="1" >Highlight message.</td>
</tr>
</table>




## MessageInputState


Message Input Management Module
- Core features: Manage the state and behavior of the message input box, support text input, emoji pack, @feature, input state notification, and complete input experience.


- Technical features: Support rich text editing, input state synchronization, draft saving, and other features. Newly-added responsive data: inputRawValue, isPeerTyping.


- Business value: Provide users with a convenient message input experience to enhance communication efficiency.


- Application scenarios: Message editing, emoji input, file sending, and voice input in input scenarios.




   responsive data


<table>
<tr>
<td rowspan="1" colSpan="1" >**Data List**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[inputRawValue](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#inputRawValue)</td>


<td rowspan="1" colSpan="1" >Original text content of the input box.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[isPeerTyping](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isPeerTyping)</td>


<td rowspan="1" colSpan="1" >Whether the other party is typing.</td>
</tr>
</table>




   API Function


<table>
<tr>
<td rowspan="1" colSpan="1" >**Function list**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[updateRawValue](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#updateRawValue)</td>


<td rowspan="1" colSpan="1" >Refresh original value.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[setEditorInstance](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setEditorInstance)</td>


<td rowspan="1" colSpan="1" >Set the editor instance.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[setContent](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setContent)</td>


<td rowspan="1" colSpan="1" >Set Content.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[insertContent](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#insertContent)</td>


<td rowspan="1" colSpan="1" >Insert content.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[focusEditor](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#focusEditor)</td>


<td rowspan="1" colSpan="1" >Focus editor.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[blurEditor](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#blurEditor)</td>


<td rowspan="1" colSpan="1" >Blur editor.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[sendMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#sendMessage)</td>


<td rowspan="1" colSpan="1" >Send message.</td>
</tr>
</table>




## MessageActionState


Message Operation Management Module
- Core features: Manage various operations of messages, including forward, refer, copy, delete, and revoke for complete message operation functionality.


- Technical features: Support batch operations, status management, permission control, and other features. Newly-added responsive data: forwardMessageIDList, isForwardMessageSelectionDone.


- Business value: Provide users with various message operation capabilities to enhance user experience.


- Application scenarios: Message forwarding, message quotation, message management, batch operation, and other scenarios.




   responsive data


<table>
<tr>
<td rowspan="1" colSpan="1" >**Data List**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[forwardMessageIDList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#forwardMessageIDList)</td>


<td rowspan="1" colSpan="1" >ID list of messages to forward.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[isForwardMessageSelectionDone](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isForwardMessageSelectionDone)</td>


<td rowspan="1" colSpan="1" >Whether message forwarding is completed.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[forwardConversationIDList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#forwardConversationIDList)</td>


<td rowspan="1" colSpan="1" >ID list of forwarding target sessions.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[quotedMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#quotedMessage)</td>


<td rowspan="1" colSpan="1" >Referenced message info.</td>
</tr>
</table>




   API Function


<table>
<tr>
<td rowspan="1" colSpan="1" >**Function list**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[forwardMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#forwardMessage)</td>


<td rowspan="1" colSpan="1" >Forward message.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[setForwardMessageIDList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setForwardMessageIDList)</td>


<td rowspan="1" colSpan="1" >Set forwarding message list.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[setIsForwardMessageSelectionDone](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setIsForwardMessageSelectionDone)</td>


<td rowspan="1" colSpan="1" >Forward selection is completed.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[setForwardConversationIDList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setForwardConversationIDList)</td>


<td rowspan="1" colSpan="1" >Set forwarding session list.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[quoteMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#quoteMessage)</td>


<td rowspan="1" colSpan="1" >Quoted message.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[clearQuotedMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#clearQuotedMessage)</td>


<td rowspan="1" colSpan="1" >Clear quoted message.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[copyTextMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#copyTextMessage)</td>


<td rowspan="1" colSpan="1" >Copy text message.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[deleteMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#deleteMessage)</td>


<td rowspan="1" colSpan="1" >Delete message.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[recallMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#recallMessage)</td>


<td rowspan="1" colSpan="1" >Recall message.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[resetMessageActionState](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#resetMessageActionState)</td>


<td rowspan="1" colSpan="1" >Reset message operation status.</td>
</tr>
</table>




## ConversationListState


Session List Management Module
- Core features: Manage user session list, support session sorting, unread statistics, and conversation action for complete session management functionality.


- Technical features: Support real-time session update, intelligent sorting, network status monitoring and other features. Newly-added responsive data: conversationList, activeConversation, totalUnRead, netStatus.


- Business value: Provide users with a clear session management interface to enhance communication efficiency.


- Application scenarios: Session management, contact list, group management, message center, and other scenarios.




   responsive data


<table>
<tr>
<td rowspan="1" colSpan="1" >**Data List**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[conversationList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#conversationList)</td>


<td rowspan="1" colSpan="1" >Conversation list data.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[activeConversation](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#activeConversation)</td>


<td rowspan="1" colSpan="1" >Current active session.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[totalUnRead](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#totalUnRead)</td>


<td rowspan="1" colSpan="1" >Total unread count.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[netStatus](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#netStatus)</td>


<td rowspan="1" colSpan="1" >Network connection status.</td>
</tr>
</table>




   API Function


<table>
<tr>
<td rowspan="1" colSpan="1" >**Function list**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[markConversationUnread](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#markConversationUnread)</td>


<td rowspan="1" colSpan="1" >Mark conversation as unread.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[setActiveConversation](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setActiveConversation)</td>


<td rowspan="1" colSpan="1" >Set active session.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[pinConversation](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#pinConversation)</td>


<td rowspan="1" colSpan="1" >Pin conversation to top.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[deleteConversation](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#deleteConversation)</td>


<td rowspan="1" colSpan="1" >Delete conversation.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[muteConversation](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#muteConversation)</td>


<td rowspan="1" colSpan="1" >Mute session.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[setConversationDraft](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setConversationDraft)</td>


<td rowspan="1" colSpan="1" >Set session draft.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[createC2CConversation](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#createC2CConversation)</td>


<td rowspan="1" colSpan="1" >Create one-on-one chat session.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[createGroupConversation](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#createGroupConversation)</td>


<td rowspan="1" colSpan="1" >Create group chat session.</td>
</tr>
</table>




## ContactListState


Contact Management Module
- Core features: Manage user contact list, including friend management, chat group management, and blocklist management for complete contact feature.


- Technical features: Support contact group, Friend request processing, group application management and other features. Newly-added responsive data: friendList, groupList, blackList, and complete contact operation API.


- Business value: Provides users with complete social relationship management capability to build a social network.


- Application scenarios: Friend management, group management, contact search, social network, and other scenarios.




   responsive data


<table>
<tr>
<td rowspan="1" colSpan="1" >**Data List**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[friendList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#friendList)</td>


<td rowspan="1" colSpan="1" >Friend list.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[groupList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#groupList)</td>


<td rowspan="1" colSpan="1" >Group list.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[blackList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#blackList)</td>


<td rowspan="1" colSpan="1" >Blocklist.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[friendApplicationUnreadCount](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#friendApplicationUnreadCount)</td>


<td rowspan="1" colSpan="1" >Friend request unread.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[friendGroupList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#friendGroupList)</td>


<td rowspan="1" colSpan="1" >Friend group list.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[friendApplicationList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#friendApplicationList)</td>


<td rowspan="1" colSpan="1" >Friend request list.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[groupApplicationList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#groupApplicationList)</td>


<td rowspan="1" colSpan="1" >Group join request list.</td>
</tr>
</table>




   API Function


<table>
<tr>
<td rowspan="1" colSpan="1" >**Function list**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[setGroupApplicationList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setGroupApplicationList)</td>


<td rowspan="1" colSpan="1" >Set group join request list.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[setFriendList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setFriendList)</td>


<td rowspan="1" colSpan="1" >Set friend list.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[setGroupList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setGroupList)</td>


<td rowspan="1" colSpan="1" >Set group list.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[setBlackList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setBlackList)</td>


<td rowspan="1" colSpan="1" >Set blocklist.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[setFriendApplicationUnreadCount](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setFriendApplicationUnreadCount)</td>


<td rowspan="1" colSpan="1" >Set friend request unread.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[setFriendGroupList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setFriendGroupList)</td>


<td rowspan="1" colSpan="1" >Set friend group list.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[setFriendApplicationList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setFriendApplicationList)</td>


<td rowspan="1" colSpan="1" >Set friend request list.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[initContactListWatcher](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#initContactListWatcher)</td>


<td rowspan="1" colSpan="1" >Initialize contact person listener.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[addFriend](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#addFriend)</td>


<td rowspan="1" colSpan="1" >Add friend.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[markFriendApplicationAsRead](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#markFriendApplicationAsRead)</td>


<td rowspan="1" colSpan="1" >Tag friend request as read.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[acceptFriendApplication](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#acceptFriendApplication)</td>


<td rowspan="1" colSpan="1" >Accept friend request.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[refuseFriendApplication](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#refuseFriendApplication)</td>


<td rowspan="1" colSpan="1" >Refuse friend application.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[addToBlacklist](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#addToBlacklist)</td>


<td rowspan="1" colSpan="1" >Add to blocklist.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[removeFromBlacklist](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#removeFromBlacklist)</td>


<td rowspan="1" colSpan="1" >Remove from blocklist.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[deleteFriend](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#deleteFriend)</td>


<td rowspan="1" colSpan="1" >Delete friend.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[setFriendRemark](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setFriendRemark)</td>


<td rowspan="1" colSpan="1" >Set friend remark.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[createFriendGroup](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#createFriendGroup)</td>


<td rowspan="1" colSpan="1" >Create friend group.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[deleteFriendGroup](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#deleteFriendGroup)</td>


<td rowspan="1" colSpan="1" >Delete friend group.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[addToFriendGroup](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#addToFriendGroup)</td>


<td rowspan="1" colSpan="1" >Add to friend group.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[removeFromFriendGroup](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#removeFromFriendGroup)</td>


<td rowspan="1" colSpan="1" >Remove from friend group.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[renameFriendGroup](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#renameFriendGroup)</td>


<td rowspan="1" colSpan="1" >Rename friend group.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[joinGroup](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#joinGroup)</td>


<td rowspan="1" colSpan="1" >Join group.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[acceptGroupApplication](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#acceptGroupApplication)</td>


<td rowspan="1" colSpan="1" >Accept group request.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[refuseGroupApplication](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#refuseGroupApplication)</td>


<td rowspan="1" colSpan="1" >Reject group request.</td>
</tr>
</table>




## C2CSettingState


C2C Chat Settings Management Module
- Core features: Manage various settings for C2C Chat, including user information, chat settings, and permission control.


- Technical features: Support real-time set synchronization, permission management, personalized configuration, and other features. Update responsive data to standardized fields such as userID, avatar, and signature.


- Business value: Provide users with a personalized C2C Chat experience to enhance communication quality.


- Application scenarios: C2C chat settings, user information management, and permission control in chat scenarios.




   responsive data


<table>
<tr>
<td rowspan="1" colSpan="1" >**Data List**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[currentConversationRef](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#currentConversationRef)</td>


<td rowspan="1" colSpan="1" >Current session reference.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[userIDRef](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#userIDRef)</td>


<td rowspan="1" colSpan="1" >User ID.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[nickRef](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#nickRef)</td>


<td rowspan="1" colSpan="1" >User nickname.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[avatarRef](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#avatarRef)</td>


<td rowspan="1" colSpan="1" >User profile photo.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[signatureRef](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#signatureRef)</td>


<td rowspan="1" colSpan="1" >User personal signature.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[remarkRef](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#remarkRef)</td>


<td rowspan="1" colSpan="1" >Friend remark name.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[isMutedRef](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isMutedRef)</td>


<td rowspan="1" colSpan="1" >Session mute status.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[isPinnedRef](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isPinnedRef)</td>


<td rowspan="1" colSpan="1" >Session pinning status.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[isContactRef](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isContactRef)</td>


<td rowspan="1" colSpan="1" >Friend relationship status.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[userID](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#userID)</td>


<td rowspan="1" colSpan="1" >User ID.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[avatar](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#avatar)</td>


<td rowspan="1" colSpan="1" >User avatar URL.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[signature](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#signature)</td>


<td rowspan="1" colSpan="1" >User personal signature.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[remark](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#remark)</td>


<td rowspan="1" colSpan="1" >User remark name.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[isMuted](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isMuted)</td>


<td rowspan="1" colSpan="1" >Whether muted.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[isPinned](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isPinned)</td>


<td rowspan="1" colSpan="1" >Whether pinned to top.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[isContact](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isContact)</td>


<td rowspan="1" colSpan="1" >Whether it is the contact person.</td>
</tr>
</table>




   API Function


<table>
<tr>
<td rowspan="1" colSpan="1" >**Function list**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[setChatPinned](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setChatPinned)</td>


<td rowspan="1" colSpan="1" >Pin chat to top.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[setChatMuted](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setChatMuted)</td>


<td rowspan="1" colSpan="1" >Enable Do Not Disturb for chat.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[setUserRemark](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setUserRemark)</td>


<td rowspan="1" colSpan="1" >Set user remark.</td>
</tr>
</table>




## GroupSettingState


Group chat settings management module
-Core features: Manage various group chat settings and operations, including information management, member management, permission control, and complete group management capabilities.


- Technical features: Support group permission management, member operations, group set sync and other features. Newly-added responsive data: groupID, groupType, groupName, and complete group information response and management API.


- Business value: Provides group owners and admins with complete group management capability to maintain order.


- Application scenarios: Group management, member management, permission control, group settings, and other scenarios.




   responsive data


<table>
<tr>
<td rowspan="1" colSpan="1" >**Data List**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[groupID](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#groupID)</td>


<td rowspan="1" colSpan="1" >Group ID.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[groupType](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#groupType)</td>


<td rowspan="1" colSpan="1" >Group type.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[groupName](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#groupName)</td>


<td rowspan="1" colSpan="1" >Group name.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[avatar](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#avatar)</td>


<td rowspan="1" colSpan="1" >User avatar URL.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[introduction](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#introduction)</td>


<td rowspan="1" colSpan="1" >Group introduction.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[notification](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#notification)</td>


<td rowspan="1" colSpan="1" >Group notice.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[isMuted](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isMuted)</td>


<td rowspan="1" colSpan="1" >Whether muted.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[isPinned](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isPinned)</td>


<td rowspan="1" colSpan="1" >Whether pinned to top.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[groupOwner](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#groupOwner)</td>


<td rowspan="1" colSpan="1" >Group owner info.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[adminMembers](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#adminMembers)</td>


<td rowspan="1" colSpan="1" >Administrator list.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[allMembers](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#allMembers)</td>


<td rowspan="1" colSpan="1" >All member list.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[memberCount](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#memberCount)</td>


<td rowspan="1" colSpan="1" >Total number of members.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[maxMemberCount](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#maxMemberCount)</td>


<td rowspan="1" colSpan="1" >Maximum number of members.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[currentUserID](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#currentUserID)</td>


<td rowspan="1" colSpan="1" >Current user ID.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[currentUserRole](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#currentUserRole)</td>


<td rowspan="1" colSpan="1" >Current user role.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[nameCard](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#nameCard)</td>


<td rowspan="1" colSpan="1" >Name card.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[isMuteAllMembers](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isMuteAllMembers)</td>


<td rowspan="1" colSpan="1" >Whether to mute all members.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[isInGroup](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isInGroup)</td>


<td rowspan="1" colSpan="1" >Whether in the group.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[inviteOption](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#inviteOption)</td>


<td rowspan="1" colSpan="1" >InviteOption.</td>
</tr>
</table>




   API Function


<table>
<tr>
<td rowspan="1" colSpan="1" >**Function list**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[getGroupMemberList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getGroupMemberList)</td>


<td rowspan="1" colSpan="1" >Get Group Member list.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[updateGroupProfile](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#updateGroupProfile)</td>


<td rowspan="1" colSpan="1" >Refresh group information.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[addGroupMember](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#addGroupMember)</td>


<td rowspan="1" colSpan="1" >Add Group Member.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[deleteGroupMember](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#deleteGroupMember)</td>


<td rowspan="1" colSpan="1" >Delete group member.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[changeGroupOwner](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#changeGroupOwner)</td>


<td rowspan="1" colSpan="1" >Transfer Group Ownership.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[setGroupMemberRole](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setGroupMemberRole)</td>


<td rowspan="1" colSpan="1" >Set group member role.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[setGroupMemberNameCard](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setGroupMemberNameCard)</td>


<td rowspan="1" colSpan="1" >Set group member name card.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[setChatPinned](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setChatPinned)</td>


<td rowspan="1" colSpan="1" >Pin chat to top.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[setChatMuted](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setChatMuted)</td>


<td rowspan="1" colSpan="1" >Enable Do Not Disturb for chat.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[setGroupMemberMuteTime](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setGroupMemberMuteTime)</td>


<td rowspan="1" colSpan="1" >Mute group member.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[setMuteAllMember](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setMuteAllMember)</td>


<td rowspan="1" colSpan="1" >Enable room-wide mute.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[dismissGroup](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#dismissGroup)</td>


<td rowspan="1" colSpan="1" >Disband group.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[quitGroup](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#quitGroup)</td>


<td rowspan="1" colSpan="1" >Leave Group.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[hasPermission](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#hasPermission)</td>


<td rowspan="1" colSpan="1" >Check permission.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[canOperateOnMember](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#canOperateOnMember)</td>


<td rowspan="1" colSpan="1" >Check member operation permissions.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[getAvailablePermissions](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getAvailablePermissions)</td>


<td rowspan="1" colSpan="1" >Get available permissions.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[initWatcher](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#initWatcher)</td>


<td rowspan="1" colSpan="1" >Initialize listener.</td>
</tr>
</table>




## VideoMixerState


Video stream mixing management module
-Core feature: Manage video stream mixing functionality, support advanced video processing such as multiple streams video compositing, layout management, and media source control.


- Technical features: Support real-time video stream mixing, dynamic layout adjustment, media source management and other features. Newly-added isVideoMixerEnabled, mediaSourceList, activeMediaSource responsive data and complete control interface.


- Business value: The platform offers professional video production capabilities to enhance live streaming quality.


- Application scenarios: Scenarios such as multi-person live streaming, Picture-in-Picture, video compositing, and professional production.




   responsive data


<table>
<tr>
<td rowspan="1" colSpan="1" >**Data List**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[publishVideoQuality](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#publishVideoQuality)</td>


<td rowspan="1" colSpan="1" >Get size based on resolution.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[isVideoMixerEnabled](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isVideoMixerEnabled)</td>


<td rowspan="1" colSpan="1" >Whether video stream mixing is enabled.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[mediaSourceList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#mediaSourceList)</td>


<td rowspan="1" colSpan="1" >Media source list.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[activeMediaSource](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#activeMediaSource)</td>


<td rowspan="1" colSpan="1" >Currently active media source.</td>
</tr>
</table>




   API Function


<table>
<tr>
<td rowspan="1" colSpan="1" >**Function list**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[getVideoDataByQuality](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getVideoDataByQuality)</td>


<td rowspan="1" colSpan="1" >Get video data based on quality.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[getSizeByQuality](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getSizeByQuality)</td>


<td rowspan="1" colSpan="1" >Get size based on quality.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[getSizeByResolution](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getSizeByResolution)</td>


<td rowspan="1" colSpan="1" >Get size based on resolution.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[transformTUIVideoQualityToTRTCVideoResolution](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#transformTUIVideoQualityToTRTCVideoResolution)</td>


<td rowspan="1" colSpan="1" >Switch video quality to TRTC resolution.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[transformTRTCVideoResolutionToTUIVideoQuality](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#transformTRTCVideoResolutionToTUIVideoQuality)</td>


<td rowspan="1" colSpan="1" >Switch TRTC resolution to video quality.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[transformTRTCVideoResModeToTUIVideoResMode](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#transformTRTCVideoResModeToTUIVideoResMode)</td>


<td rowspan="1" colSpan="1" >Switch TRTC resolution mode.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[changeActiveMediaSource](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#changeActiveMediaSource)</td>


<td rowspan="1" colSpan="1" >Switch active media source.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[updateVideoQuality](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#updateVideoQuality)</td>


<td rowspan="1" colSpan="1" >Refresh video quality.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[getDefaultLayoutByMediaSource](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getDefaultLayoutByMediaSource)</td>


<td rowspan="1" colSpan="1" >Get default layout based on media source.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[addMediaSource](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#addMediaSource)</td>


<td rowspan="1" colSpan="1" >Add media source.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[updateMediaSource](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#updateMediaSource)</td>


<td rowspan="1" colSpan="1" >Refresh media source.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[removeMediaSource](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#removeMediaSource)</td>


<td rowspan="1" colSpan="1" >Remove media source.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[enableLocalVideoMixer](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#enableLocalVideoMixer)</td>


<td rowspan="1" colSpan="1" >Enable local video stream mixing.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[clearMediaSource](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#clearMediaSource)</td>


<td rowspan="1" colSpan="1" >Clear ALL media sources.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[initMediaSourceManager](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#initMediaSourceManager)</td>


<td rowspan="1" colSpan="1" >Initialize media source manager.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[initVideoMixerState](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#initVideoMixerState)</td>


<td rowspan="1" colSpan="1" >Initialize video mixing status.</td>
</tr>
</table>




## VirtualBackgroundState


Virtual Background Management Module
-Core features: Manage the virtual background feature, supporting background replacement, background blurring, and custom background for video beautification.


- Technical features: Real-time background segmentation and replacement based on AI technology. Newly-added virtualBackgroundConfig responsive data and isSupported, setVirtualBackground API functions.


- Business value: Provides users with privacy protection and video beautification features to enhance the video call experience.


- Application scenarios: Video call, online meeting, live stream beautification, privacy protection, and other scenarios.




   responsive data


<table>
<tr>
<td rowspan="1" colSpan="1" >**Data List**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[virtualBackgroundConfig](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#virtualBackgroundConfig)</td>


<td rowspan="1" colSpan="1" >Virtual background configuration.</td>
</tr>
</table>




   API Function


<table>
<tr>
<td rowspan="1" colSpan="1" >**Function list**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[initVirtualBackground](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#initVirtualBackground)</td>


<td rowspan="1" colSpan="1" >Initialize virtual background.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[saveVirtualBackground](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#saveVirtualBackground)</td>


<td rowspan="1" colSpan="1" >Save virtual background.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[isSupported](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isSupported)</td>


<td rowspan="1" colSpan="1" >Check whether it is supported.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[setVirtualBackground](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setVirtualBackground)</td>


<td rowspan="1" colSpan="1" >Set virtual background.</td>
</tr>
</table>




## ASRState


Automatic Speech Recognition (ASR) management module
- Core features: Manage Automatic Speech Recognition (ASR), support real-time voice-to-text, history management, export and other features.


- Technical features: Based on advanced ASR technology, support language recognition, real-time transcription, history and other features. Newly-added responsive data: recentTranscripts, transcriptHistory and API: exportTranscripts.


- Business value: Provide users with speech-to-text service to enhance communication efficiency and accessibility.


- Application scenarios: Meeting minutes, speech transcription, barrier-free communication, content recording, and other scenarios.




   responsive data


<table>
<tr>
<td rowspan="1" colSpan="1" >**Data List**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[recentTranscripts](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#recentTranscripts)</td>


<td rowspan="1" colSpan="1" >Latest speech transcription records.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[transcriptHistory](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#transcriptHistory)</td>


<td rowspan="1" colSpan="1" >Speech transcription history.</td>
</tr>
</table>




   API Function


<table>
<tr>
<td rowspan="1" colSpan="1" >**Function list**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[setRecentTranscriptsDuration](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setRecentTranscriptsDuration)</td>


<td rowspan="1" colSpan="1" >Set the most recent transcription duration.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[clearHistory](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#clearHistory)</td>


<td rowspan="1" colSpan="1" >Clear transcription history.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[exportTranscripts](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#exportTranscripts)</td>


<td rowspan="1" colSpan="1" >Export transcribed content.</td>
</tr>
</table>




## SearchState


Search functionality management module
-Core feature: Manage global search functionality, supporting message search, user search, group search, and other multidimensional search capabilities.


- Technical feature: Support advanced search, search history, search suggestions, and other features. Reconstruct responsive data into standardized fields like keyword, results, isLoading, and provide a complete search interface.


- Business value: Provide users with quick search ability to enhance usage efficiency.


- Application scenarios: Message search, contact search, content search, history records, and other scenarios.




   responsive data


<table>
<tr>
<td rowspan="1" colSpan="1" >**Data List**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[keyword](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#keyword)</td>


<td rowspan="1" colSpan="1" >Search keywords.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[results](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#results)</td>


<td rowspan="1" colSpan="1" >Search result.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[isLoading](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isLoading)</td>


<td rowspan="1" colSpan="1" >Whether loading.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[error](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#error)</td>


<td rowspan="1" colSpan="1" >Error Message.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[searchAdvancedParams](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#searchAdvancedParams)</td>


<td rowspan="1" colSpan="1" >Advanced search parameter.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[selectedSearchType](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#selectedSearchType)</td>


<td rowspan="1" colSpan="1" >Selected search type.</td>
</tr>
</table>




   API Function


<table>
<tr>
<td rowspan="1" colSpan="1" >**Function list**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[search](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#search)</td>


<td rowspan="1" colSpan="1" >Search.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[setKeyword](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setKeyword)</td>


<td rowspan="1" colSpan="1" >Set keyword.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[setSelectedType](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setSelectedType)</td>


<td rowspan="1" colSpan="1" >Set selected type.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[setSearchMessageAdvancedParams](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setSearchMessageAdvancedParams)</td>


<td rowspan="1" colSpan="1" >Set advanced message search parameters.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[setSearchUserAdvancedParams](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setSearchUserAdvancedParams)</td>


<td rowspan="1" colSpan="1" >Set advanced user search parameters.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[setSearchGroupAdvancedParams](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setSearchGroupAdvancedParams)</td>


<td rowspan="1" colSpan="1" >Set advanced group search parameters.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[loadMore](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#loadMore)</td>


<td rowspan="1" colSpan="1" >Load more.</td>
</tr>
</table>




## SeatStore


Seat Storage Management Module
-Core features: Provide underlying storage and management for seat status, support core features such as seat information cache, user information map, and device request handling.


- Technical features: Use responsive storage design, support real-time status synchronization, event-driven updates, and other features. Add newly-added responsive data such as liveOwnerUserId, localUserId, seatList, and APIs like getUserInfo and convertUserInfoToAudienceInfo.


- Business value: Provide a reliable data foundation for seat management and ensure seat status consistency.


- Application scenarios: Seat status management, user information storage, device status tracking, and other underlying scenarios.




   responsive data


<table>
<tr>
<td rowspan="1" colSpan="1" >**Data List**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[liveOwnerUserId](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#liveOwnerUserId)</td>


<td rowspan="1" colSpan="1" >Anchor user ID in the live streaming room.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[localUserId](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#localUserId)</td>


<td rowspan="1" colSpan="1" >Local User ID.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[seatList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#seatList)</td>


<td rowspan="1" colSpan="1" >Microphone position list, including ALL seat states and user information.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[coHostUserList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#coHostUserList)</td>


<td rowspan="1" colSpan="1" >Anchor list for mic connection.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[sentDeviceRequestMap](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#sentDeviceRequestMap)</td>


<td rowspan="1" colSpan="1" >Request mapping sent to the device.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[receivedDeviceRequestMap](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#receivedDeviceRequestMap)</td>


<td rowspan="1" colSpan="1" >Request mapping received from the device.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[userInfoMap](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#userInfoMap)</td>


<td rowspan="1" colSpan="1" >User information mapping table.</td>
</tr>
</table>




   API Function


<table>
<tr>
<td rowspan="1" colSpan="1" >Function list</td>


<td rowspan="1" colSpan="1" >Description</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[getUserInfo](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getUserInfo)</td>


<td rowspan="1" colSpan="1" >Retrieve user information.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[convertUserInfoToAudienceInfo](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#convertUserInfoToAudienceInfo)</td>


<td rowspan="1" colSpan="1" >Switch user information to audience information.</td>
</tr>
</table>
