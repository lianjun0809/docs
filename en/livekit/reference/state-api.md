> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

The atomicx-core SDK is a brand-new first-generation responsive API launched by Tencent Cloud for Chat, Audio/Video Calls, live streaming, voice chat room and other scenarios. You can quickly build your own UI page based on this set of APIs. It supports room management, screen sharing, member management, microphone position control, basic beauty filter and other rich features. Based on the TRTC SDK, it can provide ultra-low latency and high-quality audio/video experience. This page contains ALL API interfaces of the atomicx-core SDK, displayed by feature module.

## LoginState

User Identity Authentication and Logon Management Module
-Core features: Provide basic identity authentication including user login, logout, and personal information management, forming the user identity basis of the entire system.

- Technical features: Support various log-in methods, user information cache, login status persistence and other features to underwrite user identity security and reliability.

- Business value: Provides unified user identity authentication service for all business modules, forming the foundation of system security and user experience assurance.

- Application scenarios: Core identity authentication scenarios such as user login, identity verification, personal information management, and permission control.

   responsive data

| **Data List** | **Description** |
| --- | --- |
| [loginUserInfo](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#loginUserInfo) | Current login user information. |

   API Function

| **Function list** | **Description** |
| --- | --- |
| [login](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#login) | User login. |
| [setSelfInfo](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setSelfInfo) | Set user personal information. |
| [logout](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#logout) | User logout function. |

## DeviceState

Device Status Management Module
-Core feature: Manage control of cameras, microphones and other audio/video devices, providing device status monitoring, permission check and other basic equipment services.

- Technical feature: Supports advanced functions such as multi-device management, real-time status monitoring, dynamic permission check, and automatic failure recovery.

- Business value: Provide stability to the live streaming system, underwriting the reliability of audio and video capture and user experience.

- Use cases: Basic technical scenarios such as device management, permission control, audio and video capture, and fault handling.

   responsive data

| **Data List** | **Description** |
| --- | --- |
| [microphoneStatus](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#microphoneStatus) | Microphone Status. |
| [microphoneList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#microphoneList) | Microphone Device List. |
| [currentMicrophone](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#currentMicrophone) | Selected microphone device. |
| [microphoneLastError](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#microphoneLastError) | Last microphone error information. |
| [captureVolume](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#captureVolume) | Mic capture volume. |
| [currentMicVolume](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#currentMicVolume) | Current microphone volume. |
| [isMicrophoneTesting](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isMicrophoneTesting) | Mic testing status. |
| [testingMicVolume](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#testingMicVolume) | Microphone volume during testing. |
| [cameraStatus](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#cameraStatus) | Camera status. |
| [cameraList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#cameraList) | Camera list. |
| [currentCamera](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#currentCamera) | Selected camera. |
| [cameraLastError](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#cameraLastError) | Last camera error information. |
| [isCameraTesting](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isCameraTesting) | Camera test status. |
| [isCameraTestLoading](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isCameraTestLoading) | Camera test loading status. |
| [isFrontCamera](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isFrontCamera) | Whether the camera is front-facing. |
| [localMirrorType](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#localMirrorType) | Local video image type. |
| [localVideoQuality](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#localVideoQuality) | Local video quality. |
| [speakerList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#speakerList) | Speaker Device List. |
| [currentSpeaker](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#currentSpeaker) | Selected speaker device. |
| [outputVolume](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#outputVolume) | Speaker output volume. |
| [currentAudioRoute](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#currentAudioRoute) | Current audio routing. |
| [isSpeakerTesting](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isSpeakerTesting) | Speaker testing status. |
| [screenStatus](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#screenStatus) | Screen sharing status. |
| [networkInfo](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#networkInfo) | Network information. |

   API Function

| **Function list** | **Description** |
| --- | --- |
| [openLocalMicrophone](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#openLocalMicrophone) | Open local microphone. |
| [closeLocalMicrophone](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#closeLocalMicrophone) | Close local microphone. |
| [muteLocalAudio](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#muteLocalAudio) | Mute local audio. |
| [unmuteLocalAudio](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#unmuteLocalAudio) | Unmute local audio. |
| [getMicrophoneList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getMicrophoneList) | Get microphone device list. |
| [setCurrentMicrophone](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setCurrentMicrophone) | Set current microphone device. |
| [startMicrophoneTest](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#startMicrophoneTest) | Start mic testing. |
| [setCaptureVolume](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setCaptureVolume) | Set audio capture volume. |
| [setOutputVolume](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setOutputVolume) | Set audio playback volume. |
| [stopMicrophoneTest](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#stopMicrophoneTest) | Stop mic testing. |
| [getSpeakerList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getSpeakerList) | Search speaker device list. |
| [setCurrentSpeaker](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setCurrentSpeaker) | Set current speaker device. |
| [setAudioRoute](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setAudioRoute) | Set audio routing. |
| [startSpeakerTest](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#startSpeakerTest) | Start speaker testing. |
| [stopSpeakerTest](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#stopSpeakerTest) | Stop speaker test. |
| [openLocalCamera](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#openLocalCamera) | Turn on local camera. |
| [closeLocalCamera](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#closeLocalCamera) | Turn off local camera. |
| [getCameraList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getCameraList) | Get camera list. |
| [setCurrentCamera](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setCurrentCamera) | Set current camera. |
| [switchCamera](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#switchCamera) | Switch between front and rear cameras. |
| [switchMirror](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#switchMirror) | Toggle video mirroring mode. |
| [updateVideoQuality](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#updateVideoQuality) | Refresh video quality. |
| [startCameraDeviceTest](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#startCameraDeviceTest) | Start camera test. |
| [startScreenShare](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#startScreenShare) | Start screen sharing. |
| [stopScreenShare](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#stopScreenShare) | Stop screen sharing. |
| [stopCameraDeviceTest](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#stopCameraDeviceTest) | Stop camera test. |
| [screenCaptureStopped](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#screenCaptureStopped) | Screen sharing stop callback. |

## LiveListState

Live List Management Module
-Core features: Manage the complete lifecycle of live streaming rooms, including creation, join, leave, and end core business processes, support pagination fetch and real-time update of live lists.

- Technical features: Support load by page, real-time state synchronization, dynamic data updates of live information, implement responsive data management to ensure real-time synchronization between UI and data status. Newly-added liveList and liveListCursor responsive data, provide fetchLiveList API function.

- Business value: Provide core live room management capabilities for the live streaming platform, support large-scale concurrency in live-streaming scenarios, and serve as the infrastructure for the live streaming business.

- Application scenario: Core business scenarios such as live list display, live room creation, live stream status management, and live broadcast data statistics.

   responsive data

| **Data List** | **Description** |
| --- | --- |
| [currentLive](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#currentLive) | Switch TUILiveInfo to LiveInfo format. |
| [liveList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#liveList) | Live list data, including info of all live streaming rooms. |
| [liveListCursor](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#liveListCursor) | Live list pagination cursor, used to obtain next page data. |

   API Function

| **Function list** | **Description** |
| --- | --- |
| [createLive](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#createLive) | Create a live streaming room. |
| [joinLive](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#joinLive) | Join live room. |
| [leaveLive](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#leaveLive) | Leave the live streaming room. |
| [endLive](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#endLive) | End live stream. |
| [updateLiveInfo](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#updateLiveInfo) | Refresh live room information. |
| [queryMetaData](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#queryMetaData) | Query metadata. |
| [updateLiveMetaData](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#updateLiveMetaData) | Update live room metadata. |
| [fetchLiveList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#fetchLiveList) | Get live list. |

## LiveSeatState

Live Room Seat Management Module
-Core features: Implement seat control in microphone-connected scenarios, support complex seat status management and audio/video device control, including joining, leaving, seat lock and all features.

-Technical features: Based on WebRTC technology, it supports multiple media stream management and offers advanced functions like seat locking, device control, and permission management. Newly-added responsive data includes seatList, canvas, speakingUsers, and networkQualities, as well as a complete operation API for seats.

- Business value: Provide core technology support for multi-person interactive live streaming, supporting various interactive scenarios like PK, microphone connection, and multiplayer games.

- Application scenarios: Scenarios requiring multi-person audio and video interaction, such as co-anchoring, PK battles, interactive games, online education, and live conference streaming.

   responsive data

| **Data List** | **Description** |
| --- | --- |
| [seatList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#seatList) | Microphone position list, including ALL seat states and user information. |
| [canvas](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#canvas) | Canvas configuration for video rendering and layout management. |
| [speakingUsers](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#speakingUsers) | List of users speaking. |
| [networkQualities](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#networkQualities) | Network quality information, including user's network status. |

   API Function

| **Function list** | **Description** |
| --- | --- |
| [takeSeat](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#takeSeat) | User joins the stage. |
| [leaveSeat](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#leaveSeat) | User Microphone Dequeuing. |
| [lockSeat](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#lockSeat) | Seat locking. |
| [unLockSeat](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#unLockSeat) | Unlock microphone position. |
| [kickUserOutOfSeat](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#kickUserOutOfSeat) | Remove users from speaking. |
| [moveUserToSeat](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#moveUserToSeat) | Move user to designated seat. |
| [openRemoteCamera](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#openRemoteCamera) | Enable remote camera. |
| [closeRemoteCamera](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#closeRemoteCamera) | Turn off remote camera. |
| [openRemoteMicrophone](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#openRemoteMicrophone) | Enable remote microphone. |
| [closeRemoteMicrophone](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#closeRemoteMicrophone) | Turn off remote microphone. |
| [muteMicrophone](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#muteMicrophone) | Mute microphone. |
| [unmuteMicrophone](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#unmuteMicrophone) | Unmute microphone. |
| [startPlayStream](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#startPlayStream) | Start playback. |
| [stopPlayStream](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#stopPlayStream) | Stop playback. |

## LiveAudienceState

Live Room Audience Management Module
- Core features: Manage the audience list of live streaming rooms, provide permission control, admin settings and other maintenance features for live room order, support real-time audience statistics.

- Technical features: Support advanced functions such as real-time audience list update, permission hierarchy management, and batch operation to underwrite live room order and user experience. Newly-added responsive data: audienceList and audienceCount.

- Business value: Offer a complete audience management solution for the live streaming platform, supporting order maintenance in large-scale audience scenarios.

- Application scenario: Core business scenarios such as audience management, permission control, live streaming room order maintenance, and audience interaction management.

   responsive data

| **Data List** | **Description** |
| --- | --- |
| [audienceList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#audienceList) | Audience list, including info of all audience in the live streaming room. |
| [audienceCount](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#audienceCount) | Total number statistics of audience. |

   API Function

| **Function list** | **Description** |
| --- | --- |
| [fetchAudienceList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#fetchAudienceList) | Retrieve audience list. |
| [setAdministrator](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setAdministrator) | Set administrator. |
| [revokeAdministrator](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#revokeAdministrator) | Revoke admin. |
| [kickUserOutOfRoom](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#kickUserOutOfRoom) | Kick out of room. |
| [disableSendMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#disableSendMessage) | Mute users. |

## LiveMonitorState

Live Stream Monitoring Management Module
- Core features: Provide real-time monitoring for live streaming rooms, including live status monitoring, data statistics, anomaly detection and other core monitoring capabilities, support multi-room monitoring.

- Technical features: Support real-time data collection, multidimensional monitoring metrics, intelligent alarm mechanism to underwrite service stability and reliability. Newly-added monitorLiveInfoList responsive data, optimized monitoring interface.

- Business value: Offer comprehensive monitoring assurance for the live streaming platform, enabling timely detection and handling of anomalies to improve service quality.

- Application scenario: Operation management scenarios such as live stream quality monitoring, performance analysis, abnormal alarm, and data statistics.

   responsive data

| **Data List** | **Description** |
| --- | --- |
| [monitorLiveInfoList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#monitorLiveInfoList) | Live room monitoring list. |

   API Function

| **Function list** | **Description** |
| --- | --- |
| [init](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#init) | Initialize monitoring. |
| [getLiveList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getLiveList) | Get live list. |
| [closeRoom](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#closeRoom) | Close the room. |
| [sendMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#sendMessage) | Send message. |
| [startPlay](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#startPlay) | Start playback. |
| [stopPlay](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#stopPlay) | Stop playback. |
| [muteLiveAudio](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#muteLiveAudio) | Mute live audio. |

## CoGuestState

Guest management module
- Core features: Handle mic-connect interaction between audience and host, manage join microphone application, invitation, acceptance, rejection and other complete process, support status management.

- Technical features: Based on real-time audio and video technology, support advanced functions like real-time synchronization of mic-connect status, adaptive adjustment of audio/video quality, and network condition monitoring. Newly-added connected, invitees, applicants, candidates responsive data and applyForSeat API.

- Business value: Provide core audience interaction capabilities for the live streaming platform, enhance user stickiness and live stream fun.

- Application scenarios: Interactive scenarios requiring audience participation, such as audience mic connection, interactive Q&A, online karaoke, and game live streaming.

   responsive data

| **Data List** | **Description** |
| --- | --- |
| [candidates](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#candidates) | Unsubscription of co-streaming event. |
| [connected](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#connected) | Co-streaming Connection Status. |
| [invitees](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#invitees) | List of invited users. |
| [applicants](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#applicants) | List of users applying for mic connection. |

   API Function

| **Function list** | **Description** |
| --- | --- |
| [cancelApplication](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#cancelApplication) | Cancel application. |
| [acceptApplication](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#acceptApplication) | Accept application. |
| [rejectApplication](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#rejectApplication) | Reject application. |
| [cancelInvitation](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#cancelInvitation) | Cancel invitation. |
| [acceptInvitation](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#acceptInvitation) | Accept invitation. |
| [rejectInvitation](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#rejectInvitation) | Reject invitation. |
| [disConnect](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#disConnect) | Disconnect. |
| [applyForSeat](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#applyForSeat) | Request to speak. |

## CoHostState

Anchor management module
- Core features: Implement the co-anchoring function between hosts, support host invitations, join microphone applications, status management, and other interaction features, providing a complete co-anchoring process.

- Technical features: Support advanced technologies like multi-anchor audio-video synchronization, Picture-in-Picture display, and audio/video quality optimization to ensure smooth co-anchoring experience. Newly-added coHostStatus, connected, applicant, invitees, candidates responsive data and a complete co-anchoring control API.

- Business value: Provide core collaboration capabilities for hosts on live streaming platforms, supporting advanced business scenarios like PK and co-streaming.

- Application scenarios: Advanced live-streaming scenarios such as host PK battles, co-streaming, cross-platform voice chats, and host interactions.

   responsive data

| **Data List** | **Description** |
| --- | --- |
| [coHostStatus](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#coHostStatus) | Co-streaming Host Status. |
| [connected](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#connected) | Co-streaming Connection Status. |
| [applicant](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#applicant) | Host information applying for mic connection. |
| [invitees](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#invitees) | List of invited users. |
| [candidates](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#candidates) | List of candidate users. |

   API Function

| **Function list** | **Description** |
| --- | --- |
| [requestHostConnection](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#requestHostConnection) | Request host mic connection. |
| [cancelHostConnection](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#cancelHostConnection) | Cancel host mic connection. |
| [acceptHostConnection](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#acceptHostConnection) | Accept host mic connection. |
| [rejectHostConnection](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#rejectHostConnection) | Reject host mic connection. |
| [exitHostConnection](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#exitHostConnection) | Exit host mic connection. |

## BattleState

PK Battle Management Module
- Core features: Manage PK battles between hosts, including battle invitations, acceptance, rejection, and completion, supporting live score statistics.

- Technical features: Support real-time battle state synchronization, score calculation, results statistics and other features. Newly-added battleScore responsive data provides a complete PK battle experience.

- Business value: The platform offers competitive gaming interaction features to enhance live stream fun and user engagement.

- Application scenarios: Entertainment scenarios such as host PK battles, talent competitions, game battles, and interactive competitions.

   responsive data

| **Data List** | **Description** |
| --- | --- |
| [currentBattleInfo](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#currentBattleInfo) | Current PK info. |
| [battleUsers](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#battleUsers) | List of PK participants. |
| [battleScore](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#battleScore) | Live score of PK battle. |

   API Function

| **Function list** | **Description** |
| --- | --- |
| [requestBattle](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#requestBattle) | Request PK. |
| [cancelBattleRequest](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#cancelBattleRequest) | Cancel battle request. |
| [acceptBattle](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#acceptBattle) | Accept PK. |
| [rejectBattle](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#rejectBattle) | Reject PK. |
| [exitBattle](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#exitBattle) | Exit PK. |

## BarrageState

Bullet screen message management module
- Core features: Process text messages and custom messages in the live streaming room, support barrage sending, message status synchronization and complete danmaku system, provide local notification.

- Technical features: Support advanced functions like high-concurrency message processing, real-time message synchronization, message filtering, and emoji pack support. Newly-added API functions: sendTextMessage, sendCustomMessage, appendLocalTip.

- Business value: Provide core interactive capabilities for the live streaming platform, enhance user engagement and communication environment.

- Application scenarios: bullet screen interaction, message management, emoji pack, chat room, and other social interactive scenarios.

   responsive data

| **Data List** | **Description** |
| --- | --- |
| [messageList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#messageList) | Barrage message list. |

   API Function

| **Function list** | **Description** |
| --- | --- |
| [sendTextMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#sendTextMessage) | Send text message. |
| [sendCustomMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#sendCustomMessage) | Send custom messages. |
| [appendLocalTip](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#appendLocalTip) | Add local prompt. |

## MessageListState

Message List Management Module
- Core features: Manage chat message list, support message loading, scroll control, read receipt, and highlight for complete display functionality.

- Technical features: Support high-performance message processing like virtual scrolling, message optimization, and real-time update. Newly-added responsive data: activeConversationID, messageList, hasMoreOlderMessage.

- Business value: Provide core message display capacity for Chat to underwrite a good chat experience.

- Application scenarios: Chat, group chat, private chat, and message management in communication scenarios.

   responsive data

| **Data List** | **Description** |
| --- | --- |
| [activeConversationID](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#activeConversationID) | Current active session ID. |
| [messageList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#messageList) | Message list data. |
| [hasMoreOlderMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#hasMoreOlderMessage) | Whether there are more old messages. |
| [hasMoreNewerMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#hasMoreNewerMessage) | Whether there are more new messages. |
| [enableReadReceipt](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#enableReadReceipt) | Whether to enable read receipt. |
| [isDisableScroll](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isDisableScroll) | Whether to disable scrolling. |
| [recalledMessageIDSet](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#recalledMessageIDSet) | ID set of recalled messages. |
| [highlightMessageIDSet](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#highlightMessageIDSet) | ID set of highlight messages. |

   API Function

| **Function list** | **Description** |
| --- | --- |
| [setEnableReadReceipt](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setEnableReadReceipt) | Set read receipt. |
| [setIsDisableScroll](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setIsDisableScroll) | Disable scrolling. |
| [highlightMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#highlightMessage) | Highlight message. |

## MessageInputState

Message Input Management Module
- Core features: Manage the state and behavior of the message input box, support text input, emoji pack, @feature, input state notification, and complete input experience.

- Technical features: Support rich text editing, input state synchronization, draft saving, and other features. Newly-added responsive data: inputRawValue, isPeerTyping.

- Business value: Provide users with a convenient message input experience to enhance communication efficiency.

- Application scenarios: Message editing, emoji input, file sending, and voice input in input scenarios.

   responsive data

| **Data List** | **Description** |
| --- | --- |
| [inputRawValue](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#inputRawValue) | Original text content of the input box. |
| [isPeerTyping](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isPeerTyping) | Whether the other party is typing. |

   API Function

| **Function list** | **Description** |
| --- | --- |
| [updateRawValue](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#updateRawValue) | Refresh original value. |
| [setEditorInstance](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setEditorInstance) | Set the editor instance. |
| [setContent](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setContent) | Set Content. |
| [insertContent](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#insertContent) | Insert content. |
| [focusEditor](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#focusEditor) | Focus editor. |
| [blurEditor](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#blurEditor) | Blur editor. |
| [sendMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#sendMessage) | Send message. |

## MessageActionState

Message Operation Management Module
- Core features: Manage various operations of messages, including forward, refer, copy, delete, and revoke for complete message operation functionality.

- Technical features: Support batch operations, status management, permission control, and other features. Newly-added responsive data: forwardMessageIDList, isForwardMessageSelectionDone.

- Business value: Provide users with various message operation capabilities to enhance user experience.

- Application scenarios: Message forwarding, message quotation, message management, batch operation, and other scenarios.

   responsive data

| **Data List** | **Description** |
| --- | --- |
| [forwardMessageIDList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#forwardMessageIDList) | ID list of messages to forward. |
| [isForwardMessageSelectionDone](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isForwardMessageSelectionDone) | Whether message forwarding is completed. |
| [forwardConversationIDList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#forwardConversationIDList) | ID list of forwarding target sessions. |
| [quotedMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#quotedMessage) | Referenced message info. |

   API Function

| **Function list** | **Description** |
| --- | --- |
| [forwardMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#forwardMessage) | Forward message. |
| [setForwardMessageIDList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setForwardMessageIDList) | Set forwarding message list. |
| [setIsForwardMessageSelectionDone](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setIsForwardMessageSelectionDone) | Forward selection is completed. |
| [setForwardConversationIDList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setForwardConversationIDList) | Set forwarding session list. |
| [quoteMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#quoteMessage) | Quoted message. |
| [clearQuotedMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#clearQuotedMessage) | Clear quoted message. |
| [copyTextMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#copyTextMessage) | Copy text message. |
| [deleteMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#deleteMessage) | Delete message. |
| [recallMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#recallMessage) | Recall message. |
| [resetMessageActionState](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#resetMessageActionState) | Reset message operation status. |

## ConversationListState

Session List Management Module
- Core features: Manage user session list, support session sorting, unread statistics, and conversation action for complete session management functionality.

- Technical features: Support real-time session update, intelligent sorting, network status monitoring and other features. Newly-added responsive data: conversationList, activeConversation, totalUnRead, netStatus.

- Business value: Provide users with a clear session management interface to enhance communication efficiency.

- Application scenarios: Session management, contact list, group management, message center, and other scenarios.

   responsive data

| **Data List** | **Description** |
| --- | --- |
| [conversationList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#conversationList) | Conversation list data. |
| [activeConversation](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#activeConversation) | Current active session. |
| [totalUnRead](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#totalUnRead) | Total unread count. |
| [netStatus](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#netStatus) | Network connection status. |

   API Function

| **Function list** | **Description** |
| --- | --- |
| [markConversationUnread](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#markConversationUnread) | Mark conversation as unread. |
| [setActiveConversation](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setActiveConversation) | Set active session. |
| [pinConversation](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#pinConversation) | Pin conversation to top. |
| [deleteConversation](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#deleteConversation) | Delete conversation. |
| [muteConversation](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#muteConversation) | Mute session. |
| [setConversationDraft](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setConversationDraft) | Set session draft. |
| [createC2CConversation](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#createC2CConversation) | Create one-on-one chat session. |
| [createGroupConversation](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#createGroupConversation) | Create group chat session. |

## ContactListState

Contact Management Module
- Core features: Manage user contact list, including friend management, chat group management, and blocklist management for complete contact feature.

- Technical features: Support contact group, Friend request processing, group application management and other features. Newly-added responsive data: friendList, groupList, blackList, and complete contact operation API.

- Business value: Provides users with complete social relationship management capability to build a social network.

- Application scenarios: Friend management, group management, contact search, social network, and other scenarios.

   responsive data

| **Data List** | **Description** |
| --- | --- |
| [friendList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#friendList) | Friend list. |
| [groupList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#groupList) | Group list. |
| [blackList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#blackList) | Blocklist. |
| [friendApplicationUnreadCount](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#friendApplicationUnreadCount) | Friend request unread. |
| [friendGroupList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#friendGroupList) | Friend group list. |
| [friendApplicationList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#friendApplicationList) | Friend request list. |
| [groupApplicationList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#groupApplicationList) | Group join request list. |

   API Function

| **Function list** | **Description** |
| --- | --- |
| [setGroupApplicationList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setGroupApplicationList) | Set group join request list. |
| [setFriendList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setFriendList) | Set friend list. |
| [setGroupList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setGroupList) | Set group list. |
| [setBlackList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setBlackList) | Set blocklist. |
| [setFriendApplicationUnreadCount](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setFriendApplicationUnreadCount) | Set friend request unread. |
| [setFriendGroupList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setFriendGroupList) | Set friend group list. |
| [setFriendApplicationList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setFriendApplicationList) | Set friend request list. |
| [initContactListWatcher](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#initContactListWatcher) | Initialize contact person listener. |
| [addFriend](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#addFriend) | Add friend. |
| [markFriendApplicationAsRead](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#markFriendApplicationAsRead) | Tag friend request as read. |
| [acceptFriendApplication](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#acceptFriendApplication) | Accept friend request. |
| [refuseFriendApplication](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#refuseFriendApplication) | Refuse friend application. |
| [addToBlacklist](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#addToBlacklist) | Add to blocklist. |
| [removeFromBlacklist](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#removeFromBlacklist) | Remove from blocklist. |
| [deleteFriend](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#deleteFriend) | Delete friend. |
| [setFriendRemark](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setFriendRemark) | Set friend remark. |
| [createFriendGroup](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#createFriendGroup) | Create friend group. |
| [deleteFriendGroup](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#deleteFriendGroup) | Delete friend group. |
| [addToFriendGroup](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#addToFriendGroup) | Add to friend group. |
| [removeFromFriendGroup](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#removeFromFriendGroup) | Remove from friend group. |
| [renameFriendGroup](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#renameFriendGroup) | Rename friend group. |
| [joinGroup](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#joinGroup) | Join group. |
| [acceptGroupApplication](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#acceptGroupApplication) | Accept group request. |
| [refuseGroupApplication](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#refuseGroupApplication) | Reject group request. |

## C2CSettingState

C2C Chat Settings Management Module
- Core features: Manage various settings for C2C Chat, including user information, chat settings, and permission control.

- Technical features: Support real-time set synchronization, permission management, personalized configuration, and other features. Update responsive data to standardized fields such as userID, avatar, and signature.

- Business value: Provide users with a personalized C2C Chat experience to enhance communication quality.

- Application scenarios: C2C chat settings, user information management, and permission control in chat scenarios.

   responsive data

| **Data List** | **Description** |
| --- | --- |
| [currentConversationRef](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#currentConversationRef) | Current session reference. |
| [userIDRef](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#userIDRef) | User ID. |
| [nickRef](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#nickRef) | User nickname. |
| [avatarRef](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#avatarRef) | User profile photo. |
| [signatureRef](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#signatureRef) | User personal signature. |
| [remarkRef](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#remarkRef) | Friend remark name. |
| [isMutedRef](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isMutedRef) | Session mute status. |
| [isPinnedRef](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isPinnedRef) | Session pinning status. |
| [isContactRef](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isContactRef) | Friend relationship status. |
| [userID](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#userID) | User ID. |
| [avatar](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#avatar) | User avatar URL. |
| [signature](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#signature) | User personal signature. |
| [remark](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#remark) | User remark name. |
| [isMuted](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isMuted) | Whether muted. |
| [isPinned](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isPinned) | Whether pinned to top. |
| [isContact](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isContact) | Whether it is the contact person. |

   API Function

| **Function list** | **Description** |
| --- | --- |
| [setChatPinned](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setChatPinned) | Pin chat to top. |
| [setChatMuted](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setChatMuted) | Enable Do Not Disturb for chat. |
| [setUserRemark](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setUserRemark) | Set user remark. |

## GroupSettingState

Group chat settings management module
-Core features: Manage various group chat settings and operations, including information management, member management, permission control, and complete group management capabilities.

- Technical features: Support group permission management, member operations, group set sync and other features. Newly-added responsive data: groupID, groupType, groupName, and complete group information response and management API.

- Business value: Provides group owners and admins with complete group management capability to maintain order.

- Application scenarios: Group management, member management, permission control, group settings, and other scenarios.

   responsive data

| **Data List** | **Description** |
| --- | --- |
| [groupID](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#groupID) | Group ID. |
| [groupType](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#groupType) | Group type. |
| [groupName](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#groupName) | Group name. |
| [avatar](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#avatar) | User avatar URL. |
| [introduction](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#introduction) | Group introduction. |
| [notification](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#notification) | Group notice. |
| [isMuted](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isMuted) | Whether muted. |
| [isPinned](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isPinned) | Whether pinned to top. |
| [groupOwner](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#groupOwner) | Group owner info. |
| [adminMembers](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#adminMembers) | Administrator list. |
| [allMembers](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#allMembers) | All member list. |
| [memberCount](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#memberCount) | Total number of members. |
| [maxMemberCount](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#maxMemberCount) | Maximum number of members. |
| [currentUserID](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#currentUserID) | Current user ID. |
| [currentUserRole](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#currentUserRole) | Current user role. |
| [nameCard](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#nameCard) | Name card. |
| [isMuteAllMembers](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isMuteAllMembers) | Whether to mute all members. |
| [isInGroup](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isInGroup) | Whether in the group. |
| [inviteOption](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#inviteOption) | InviteOption. |

   API Function

| **Function list** | **Description** |
| --- | --- |
| [getGroupMemberList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getGroupMemberList) | Get Group Member list. |
| [updateGroupProfile](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#updateGroupProfile) | Refresh group information. |
| [addGroupMember](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#addGroupMember) | Add Group Member. |
| [deleteGroupMember](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#deleteGroupMember) | Delete group member. |
| [changeGroupOwner](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#changeGroupOwner) | Transfer Group Ownership. |
| [setGroupMemberRole](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setGroupMemberRole) | Set group member role. |
| [setGroupMemberNameCard](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setGroupMemberNameCard) | Set group member name card. |
| [setChatPinned](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setChatPinned) | Pin chat to top. |
| [setChatMuted](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setChatMuted) | Enable Do Not Disturb for chat. |
| [setGroupMemberMuteTime](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setGroupMemberMuteTime) | Mute group member. |
| [setMuteAllMember](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setMuteAllMember) | Enable room-wide mute. |
| [dismissGroup](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#dismissGroup) | Disband group. |
| [quitGroup](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#quitGroup) | Leave Group. |
| [hasPermission](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#hasPermission) | Check permission. |
| [canOperateOnMember](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#canOperateOnMember) | Check member operation permissions. |
| [getAvailablePermissions](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getAvailablePermissions) | Get available permissions. |
| [initWatcher](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#initWatcher) | Initialize listener. |

## VideoMixerState

Video stream mixing management module
-Core feature: Manage video stream mixing functionality, support advanced video processing such as multiple streams video compositing, layout management, and media source control.

- Technical features: Support real-time video stream mixing, dynamic layout adjustment, media source management and other features. Newly-added isVideoMixerEnabled, mediaSourceList, activeMediaSource responsive data and complete control interface.

- Business value: The platform offers professional video production capabilities to enhance live streaming quality.

- Application scenarios: Scenarios such as multi-person live streaming, Picture-in-Picture, video compositing, and professional production.

   responsive data

| **Data List** | **Description** |
| --- | --- |
| [publishVideoQuality](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#publishVideoQuality) | Get size based on resolution. |
| [isVideoMixerEnabled](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isVideoMixerEnabled) | Whether video stream mixing is enabled. |
| [mediaSourceList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#mediaSourceList) | Media source list. |
| [activeMediaSource](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#activeMediaSource) | Currently active media source. |

   API Function

| **Function list** | **Description** |
| --- | --- |
| [getVideoDataByQuality](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getVideoDataByQuality) | Get video data based on quality. |
| [getSizeByQuality](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getSizeByQuality) | Get size based on quality. |
| [getSizeByResolution](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getSizeByResolution) | Get size based on resolution. |
| [transformTUIVideoQualityToTRTCVideoResolution](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#transformTUIVideoQualityToTRTCVideoResolution) | Switch video quality to TRTC resolution. |
| [transformTRTCVideoResolutionToTUIVideoQuality](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#transformTRTCVideoResolutionToTUIVideoQuality) | Switch TRTC resolution to video quality. |
| [transformTRTCVideoResModeToTUIVideoResMode](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#transformTRTCVideoResModeToTUIVideoResMode) | Switch TRTC resolution mode. |
| [changeActiveMediaSource](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#changeActiveMediaSource) | Switch active media source. |
| [updateVideoQuality](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#updateVideoQuality) | Refresh video quality. |
| [getDefaultLayoutByMediaSource](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getDefaultLayoutByMediaSource) | Get default layout based on media source. |
| [addMediaSource](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#addMediaSource) | Add media source. |
| [updateMediaSource](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#updateMediaSource) | Refresh media source. |
| [removeMediaSource](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#removeMediaSource) | Remove media source. |
| [enableLocalVideoMixer](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#enableLocalVideoMixer) | Enable local video stream mixing. |
| [clearMediaSource](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#clearMediaSource) | Clear ALL media sources. |
| [initMediaSourceManager](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#initMediaSourceManager) | Initialize media source manager. |
| [initVideoMixerState](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#initVideoMixerState) | Initialize video mixing status. |

## VirtualBackgroundState

Virtual Background Management Module
-Core features: Manage the virtual background feature, supporting background replacement, background blurring, and custom background for video beautification.

- Technical features: Real-time background segmentation and replacement based on AI technology. Newly-added virtualBackgroundConfig responsive data and isSupported, setVirtualBackground API functions.

- Business value: Provides users with privacy protection and video beautification features to enhance the video call experience.

- Application scenarios: Video call, online meeting, live stream beautification, privacy protection, and other scenarios.

   responsive data

| **Data List** | **Description** |
| --- | --- |
| [virtualBackgroundConfig](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#virtualBackgroundConfig) | Virtual background configuration. |

   API Function

| **Function list** | **Description** |
| --- | --- |
| [initVirtualBackground](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#initVirtualBackground) | Initialize virtual background. |
| [saveVirtualBackground](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#saveVirtualBackground) | Save virtual background. |
| [isSupported](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isSupported) | Check whether it is supported. |
| [setVirtualBackground](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setVirtualBackground) | Set virtual background. |

## ASRState

Automatic Speech Recognition (ASR) management module
- Core features: Manage Automatic Speech Recognition (ASR), support real-time voice-to-text, history management, export and other features.

- Technical features: Based on advanced ASR technology, support language recognition, real-time transcription, history and other features. Newly-added responsive data: recentTranscripts, transcriptHistory and API: exportTranscripts.

- Business value: Provide users with speech-to-text service to enhance communication efficiency and accessibility.

- Application scenarios: Meeting minutes, speech transcription, barrier-free communication, content recording, and other scenarios.

   responsive data

| **Data List** | **Description** |
| --- | --- |
| [recentTranscripts](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#recentTranscripts) | Latest speech transcription records. |
| [transcriptHistory](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#transcriptHistory) | Speech transcription history. |

   API Function

| **Function list** | **Description** |
| --- | --- |
| [setRecentTranscriptsDuration](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setRecentTranscriptsDuration) | Set the most recent transcription duration. |
| [clearHistory](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#clearHistory) | Clear transcription history. |
| [exportTranscripts](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#exportTranscripts) | Export transcribed content. |

## SearchState

Search functionality management module
-Core feature: Manage global search functionality, supporting message search, user search, group search, and other multidimensional search capabilities.

- Technical feature: Support advanced search, search history, search suggestions, and other features. Reconstruct responsive data into standardized fields like keyword, results, isLoading, and provide a complete search interface.

- Business value: Provide users with quick search ability to enhance usage efficiency.

- Application scenarios: Message search, contact search, content search, history records, and other scenarios.

   responsive data

| **Data List** | **Description** |
| --- | --- |
| [keyword](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#keyword) | Search keywords. |
| [results](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#results) | Search result. |
| [isLoading](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isLoading) | Whether loading. |
| [error](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#error) | Error Message. |
| [searchAdvancedParams](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#searchAdvancedParams) | Advanced search parameter. |
| [selectedSearchType](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#selectedSearchType) | Selected search type. |

   API Function

| **Function list** | **Description** |
| --- | --- |
| [search](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#search) | Search. |
| [setKeyword](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setKeyword) | Set keyword. |
| [setSelectedType](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setSelectedType) | Set selected type. |
| [setSearchMessageAdvancedParams](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setSearchMessageAdvancedParams) | Set advanced message search parameters. |
| [setSearchUserAdvancedParams](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setSearchUserAdvancedParams) | Set advanced user search parameters. |
| [setSearchGroupAdvancedParams](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setSearchGroupAdvancedParams) | Set advanced group search parameters. |
| [loadMore](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#loadMore) | Load more. |

## SeatStore

Seat Storage Management Module
-Core features: Provide underlying storage and management for seat status, support core features such as seat information cache, user information map, and device request handling.

- Technical features: Use responsive storage design, support real-time status synchronization, event-driven updates, and other features. Add newly-added responsive data such as liveOwnerUserId, localUserId, seatList, and APIs like getUserInfo and convertUserInfoToAudienceInfo.

- Business value: Provide a reliable data foundation for seat management and ensure seat status consistency.

- Application scenarios: Seat status management, user information storage, device status tracking, and other underlying scenarios.

   responsive data

| **Data List** | **Description** |
| --- | --- |
| [liveOwnerUserId](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#liveOwnerUserId) | Anchor user ID in the live streaming room. |
| [localUserId](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#localUserId) | Local User ID. |
| [seatList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#seatList) | Microphone position list, including ALL seat states and user information. |
| [coHostUserList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#coHostUserList) | Anchor list for mic connection. |
| [sentDeviceRequestMap](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#sentDeviceRequestMap) | Request mapping sent to the device. |
| [receivedDeviceRequestMap](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#receivedDeviceRequestMap) | Request mapping received from the device. |
| [userInfoMap](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#userInfoMap) | User information mapping table. |

   API Function

| Function list | Description |
| --- | --- |
| [getUserInfo](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getUserInfo) | Retrieve user information. |
| [convertUserInfoToAudienceInfo](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#convertUserInfoToAudienceInfo) | Switch user information to audience information. |
