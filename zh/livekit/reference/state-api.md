> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

atomicx-core SDK 是腾讯云最新推出的面向即时通信、音视频通话、视频直播、语聊房等场景的全新一代基于响应式的 API，您可以非常快速的基于这组 API 构建自己的 UI 页面，它支持房间管理、屏幕分享、成员管理、麦位控制、基础美颜等丰富功能，同时基于 TRTC SDK，能够提供超低延时、高品质的音视频体验，本页面包含 atomicx-core SDK 的所有 API 接口，按功能模块分类展示。

## LoginState

用户身份认证与登录管理模块
- 核心功能：提供用户登录、登出、个人信息管理等基础身份认证功能，是整个系统的用户身份基础。

- 技术特点：支持多种登录方式、用户信息缓存、登录状态持久化等功能，确保用户身份的安全性和可靠性。

- 业务价值：为所有业务模块提供统一的用户身份认证服务，是系统安全和用户体验的基础保障。

- 应用场景：用户登录、身份验证、个人信息管理、权限控制等核心身份认证场景。

   **响应式数据**

| **数据列表** | **描述** |
| --- | --- |
| [loginUserInfo](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#loginUserInfo) | 当前登录用户信息。 |

   **接口函数**

| **函数列表** | **描述** |
| --- | --- |
| [login](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#login) | 用户登录。 |
| [setSelfInfo](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setSelfInfo) | 设置用户个人信息。 |
| [logout](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#logout) | 用户登出函数。 |

## DeviceState

设备状态管理模块
- 核心功能：管理摄像头、麦克风等音视频设备的控制，提供设备状态监控、权限检查等基础设备服务。

- 技术特点：支持多设备管理、设备状态实时监控、权限动态检查、设备故障自动恢复等高级功能。

- 业务价值：为直播系统提供稳定的设备基础，确保音视频采集的可靠性和用户体验。

- 应用场景：设备管理、权限控制、音视频采集、设备故障处理等基础技术场景。

   **响应式数据**

| **数据列表** | **描述** |
| --- | --- |
| [microphoneStatus](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#microphoneStatus) | 麦克风状态。 |
| [microphoneList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#microphoneList) | 麦克风设备列表。 |
| [currentMicrophone](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#currentMicrophone) | 当前选中的麦克风设备。 |
| [microphoneLastError](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#microphoneLastError) | 麦克风最后一次错误信息。 |
| [captureVolume](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#captureVolume) | 麦克风采集音量。 |
| [currentMicVolume](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#currentMicVolume) | 当前麦克风音量。 |
| [isMicrophoneTesting](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isMicrophoneTesting) | 麦克风测试状态。 |
| [testingMicVolume](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#testingMicVolume) | 测试时的麦克风音量。 |
| [cameraStatus](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#cameraStatus) | 摄像头状态。 |
| [cameraList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#cameraList) | 摄像头设备列表。 |
| [currentCamera](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#currentCamera) | 当前选中的摄像头设备。 |
| [cameraLastError](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#cameraLastError) | 摄像头最后一次错误信息。 |
| [isCameraTesting](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isCameraTesting) | 摄像头测试状态。 |
| [isCameraTestLoading](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isCameraTestLoading) | 摄像头测试加载状态。 |
| [isFrontCamera](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isFrontCamera) | 是否为前置摄像头。 |
| [localMirrorType](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#localMirrorType) | 本地视频镜像类型。 |
| [localVideoQuality](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#localVideoQuality) | 本地视频质量。 |
| [speakerList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#speakerList) | 扬声器设备列表。 |
| [currentSpeaker](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#currentSpeaker) | 当前选中的扬声器设备。 |
| [outputVolume](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#outputVolume) | 扬声器输出音量。 |
| [currentAudioRoute](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#currentAudioRoute) | 当前音频路由。 |
| [isSpeakerTesting](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isSpeakerTesting) | 扬声器测试状态。 |
| [screenStatus](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#screenStatus) | 屏幕分享状态。 |
| [networkInfo](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#networkInfo) | 网络信息。 |

   **接口函数**

| **函数列表** | **描述** |
| --- | --- |
| [openLocalMicrophone](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#openLocalMicrophone) | 开启本地麦克风。 |
| [closeLocalMicrophone](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#closeLocalMicrophone) | 关闭本地麦克风。 |
| [muteLocalAudio](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#muteLocalAudio) | 静音本地音频。 |
| [unmuteLocalAudio](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#unmuteLocalAudio) | 取消静音本地音频。 |
| [getMicrophoneList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getMicrophoneList) | 获取麦克风设备列表。 |
| [setCurrentMicrophone](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setCurrentMicrophone) | 设置当前麦克风设备。 |
| [startMicrophoneTest](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#startMicrophoneTest) | 开始麦克风测试。 |
| [setCaptureVolume](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setCaptureVolume) | 设置音频采集音量。 |
| [setOutputVolume](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setOutputVolume) | 设置音频播放音量。 |
| [stopMicrophoneTest](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#stopMicrophoneTest) | 停止麦克风测试。 |
| [getSpeakerList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getSpeakerList) | 获取扬声器设备列表。 |
| [setCurrentSpeaker](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setCurrentSpeaker) | 设置当前扬声器设备。 |
| [setAudioRoute](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setAudioRoute) | 设置音频路由。 |
| [startSpeakerTest](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#startSpeakerTest) | 开始扬声器测试。 |
| [stopSpeakerTest](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#stopSpeakerTest) | 停止扬声器测试。 |
| [openLocalCamera](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#openLocalCamera) | 开启本地摄像头。 |
| [closeLocalCamera](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#closeLocalCamera) | 关闭本地摄像头。 |
| [getCameraList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getCameraList) | 获取摄像头设备列表。 |
| [setCurrentCamera](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setCurrentCamera) | 设置当前摄像头设备。 |
| [switchCamera](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#switchCamera) | 切换前后摄像头。 |
| [switchMirror](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#switchMirror) | 切换视频镜像模式。 |
| [updateVideoQuality](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#updateVideoQuality) | 更新视频质量。 |
| [startCameraDeviceTest](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#startCameraDeviceTest) | 开始摄像头设备测试。 |
| [startScreenShare](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#startScreenShare) | 开始屏幕分享。 |
| [stopScreenShare](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#stopScreenShare) | 停止屏幕分享。 |
| [stopCameraDeviceTest](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#stopCameraDeviceTest) | 停止摄像头设备测试。 |
| [screenCaptureStopped](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#screenCaptureStopped) | 屏幕分享停止回调。 |

## LiveListState

直播列表管理模块
- 核心功能：管理直播间的完整生命周期，包括创建、加入、离开、结束等核心业务流程，支持直播列表的分页获取和实时更新。

- 技术特点：支持分页加载、实时状态同步、直播信息动态更新，采用响应式数据管理，确保 UI 与数据状态实时同步。新增 liveList 和 liveListCursor 响应式数据，提供 fetchLiveList 接口函数。

- 业务价值：为直播平台提供核心的直播间管理能力，支持大规模并发直播场景，是直播业务的基础设施。

- 应用场景：直播列表展示、直播间创建、直播状态管理、直播数据统计等核心业务场景。

   **响应式数据**

| **数据列表** | **描述** |
| --- | --- |
| [currentLive](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#currentLive) | 转换TUILiveInfo为LiveInfo格式。 |
| [liveList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#liveList) | 直播列表数据，包含所有直播间的信息。 |
| [liveListCursor](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#liveListCursor) | 直播列表分页游标，用于获取下一页数据。 |

   **接口函数**

| **函数列表** | **描述** |
| --- | --- |
| [createLive](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#createLive) | 创建直播间。 |
| [joinLive](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#joinLive) | 加入直播间。 |
| [leaveLive](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#leaveLive) | 离开直播间。 |
| [endLive](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#endLive) | 结束直播。 |
| [updateLiveInfo](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#updateLiveInfo) | 更新直播间信息。 |
| [queryMetaData](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#queryMetaData) | 查询元数据。 |
| [updateLiveMetaData](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#updateLiveMetaData) | 更新直播间元数据。 |
| [fetchLiveList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#fetchLiveList) | 获取直播列表。 |

## LiveSeatState

直播间座位管理模块
- 核心功能：实现多人连麦场景下的座位控制，支持复杂的座位状态管理和音视频设备控制，包括上麦、下麦、座位锁定等完整功能。

- 技术特点：基于 WebRTC 技术，支持多路音视频流管理，提供座位锁定、设备控制、权限管理等高级功能。新增 seatList、canvas、speakingUsers、networkQualities 响应式数据，以及完整的座位操作接口。

- 业务价值：为多人互动直播提供核心技术支撑，支持 PK、连麦、多人游戏等丰富的互动场景。

- 应用场景：多人连麦、主播 PK、互动游戏、在线教育、会议直播等需要多人音视频互动的场景。

   **响应式数据**

| **数据列表** | **描述** |
| --- | --- |
| [seatList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#seatList) | 麦位列表，包含所有麦位的状态和用户信息。 |
| [canvas](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#canvas) | 画布配置，用于视频渲染和布局管理。 |
| [speakingUsers](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#speakingUsers) | 正在发言的用户列表。 |
| [networkQualities](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#networkQualities) | 网络质量信息，包含各用户的网络状态。 |

   **接口函数**

| **函数列表** | **描述** |
| --- | --- |
| [takeSeat](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#takeSeat) | 用户上麦。 |
| [leaveSeat](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#leaveSeat) | 用户下麦。 |
| [lockSeat](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#lockSeat) | 锁定麦位。 |
| [unLockSeat](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#unLockSeat) | 解锁麦位。 |
| [kickUserOutOfSeat](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#kickUserOutOfSeat) | 踢用户下麦。 |
| [moveUserToSeat](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#moveUserToSeat) | 移动用户到指定麦位。 |
| [openRemoteCamera](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#openRemoteCamera) | 开启远端摄像头。 |
| [closeRemoteCamera](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#closeRemoteCamera) | 关闭远端摄像头。 |
| [openRemoteMicrophone](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#openRemoteMicrophone) | 开启远端麦克风。 |
| [closeRemoteMicrophone](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#closeRemoteMicrophone) | 关闭远端麦克风。 |
| [muteMicrophone](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#muteMicrophone) | 静音麦克风。 |
| [unmuteMicrophone](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#unmuteMicrophone) | 取消静音麦克风。 |
| [startPlayStream](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#startPlayStream) | 开始播放流。 |
| [stopPlayStream](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#stopPlayStream) | 停止播放流。 |

## LiveAudienceState

直播间观众管理模块
- 核心功能：管理直播间观众列表，提供观众权限控制、管理员设置等直播间秩序维护功能，支持实时观众统计。

- 技术特点：支持实时观众列表更新、权限分级管理、批量操作等高级功能，确保直播间秩序和用户体验。新增 audienceList 和 audienceCount 响应式数据。

- 业务价值：为直播平台提供完整的观众管理解决方案，支持大规模观众场景下的秩序维护。

- 应用场景：观众管理、权限控制、直播间秩序维护、观众互动管理等核心业务场景。

   **响应式数据**

| **数据列表** | **描述** |
| --- | --- |
| [audienceList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#audienceList) | 观众列表，包含直播间所有观众的信息。 |
| [audienceCount](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#audienceCount) | 观众总数统计。 |

   **接口函数**

| **函数列表** | **描述** |
| --- | --- |
| [fetchAudienceList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#fetchAudienceList) | 获取观众列表。 |
| [setAdministrator](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setAdministrator) | 设置管理员。 |
| [revokeAdministrator](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#revokeAdministrator) | 撤销管理员。 |
| [kickUserOutOfRoom](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#kickUserOutOfRoom) | 踢出房间。 |
| [disableSendMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#disableSendMessage) | 禁言用户。 |

## LiveMonitorState

直播监控管理模块
- 核心功能：提供直播间实时监控功能，包括直播状态监控、数据统计、异常检测等核心监控能力，支持多直播间监控。

- 技术特点：支持实时数据采集、多维度监控指标、智能告警机制，确保直播服务的稳定性和可靠性。新增 monitorLiveInfoList 响应式数据，优化监控接口。

- 业务价值：为直播平台提供全方位的监控保障，及时发现和处理异常情况，提升服务质量。

- 应用场景：直播质量监控、性能分析、异常告警、数据统计等运营管理场景。

   **响应式数据**

| **数据列表** | **描述** |
| --- | --- |
| [monitorLiveInfoList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#monitorLiveInfoList) | 监控的直播间信息列表。 |

   **接口函数**

| **函数列表** | **描述** |
| --- | --- |
| [init](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#init) | 初始化监控。 |
| [getLiveList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getLiveList) | 获取直播列表。 |
| [closeRoom](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#closeRoom) | 关闭房间。 |
| [sendMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#sendMessage) | 发送消息。 |
| [startPlay](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#startPlay) | 开始播放。 |
| [stopPlay](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#stopPlay) | 停止播放。 |
| [muteLiveAudio](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#muteLiveAudio) | 静音直播音频。 |

## CoGuestState

连麦嘉宾管理模块
- 核心功能：处理观众与主播之间的连麦互动，管理连麦申请、邀请、接受、拒绝等完整的连麦流程，支持连麦状态管理。

- 技术特点：基于实时音视频技术，支持连麦状态实时同步、音视频质量自适应、网络状况监控等高级功能。新增 connected、invitees、applicants、candidates 响应式数据和 applyForSeat 接口。

- 业务价值：为直播平台提供观众参与互动的核心能力，增强用户粘性和直播趣味性。

- 应用场景：观众连麦、互动问答、在线K歌、游戏直播等需要观众参与的互动场景。

   **响应式数据**

| **数据列表** | **描述** |
| --- | --- |
| [candidates](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#candidates) | 取消订阅连麦事件。 |
| [connected](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#connected) | 连麦连接状态。 |
| [invitees](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#invitees) | 被邀请的用户列表。 |
| [applicants](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#applicants) | 申请连麦的用户列表。 |

   **接口函数**

| **函数列表** | **描述** |
| --- | --- |
| [cancelApplication](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#cancelApplication) | 取消申请。 |
| [acceptApplication](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#acceptApplication) | 接受申请。 |
| [rejectApplication](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#rejectApplication) | 拒绝申请。 |
| [cancelInvitation](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#cancelInvitation) | 取消邀请。 |
| [acceptInvitation](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#acceptInvitation) | 接受邀请。 |
| [rejectInvitation](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#rejectInvitation) | 拒绝邀请。 |
| [disConnect](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#disConnect) | 断开连接。 |
| [applyForSeat](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#applyForSeat) | 申请上麦。 |

## CoHostState

连麦主播管理模块
- 核心功能：实现主播间的连麦功能，支持主播邀请、连麦申请、连麦状态管理等主播间互动功能，提供完整的主播连麦流程。

- 技术特点：支持多主播音视频同步、画中画显示、音视频质量优化等高级技术，确保连麦体验的流畅性。新增 coHostStatus、connected、applicant、invitees、candidates 响应式数据和完整的连麦控制接口。

- 业务价值：为直播平台提供主播间协作的核心能力，支持 PK、合作直播等高级业务场景。

- 应用场景：主播 PK、合作直播、跨平台连麦、主播互动等高级直播场景。

   **响应式数据**

| **数据列表** | **描述** |
| --- | --- |
| [coHostStatus](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#coHostStatus) | 连麦主播状态。 |
| [connected](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#connected) | 连麦连接状态。 |
| [applicant](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#applicant) | 申请连麦的主播信息。 |
| [invitees](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#invitees) | 被邀请的用户列表。 |
| [candidates](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#candidates) | 候选用户列表。 |

   **接口函数**

| **函数列表** | **描述** |
| --- | --- |
| [requestHostConnection](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#requestHostConnection) | 请求主播连麦。 |
| [cancelHostConnection](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#cancelHostConnection) | 取消主播连麦。 |
| [acceptHostConnection](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#acceptHostConnection) | 接受主播连麦。 |
| [rejectHostConnection](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#rejectHostConnection) | 拒绝主播连麦。 |
| [exitHostConnection](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#exitHostConnection) | 退出主播连麦。 |

## BattleState

PK 对战管理模块
- 核心功能：管理主播间的 PK 对战功能，包括对战邀请、接受、拒绝、结束等完整的 PK 流程，支持实时比分统计。

- 技术特点：支持实时对战状态同步、比分计算、对战结果统计等功能。新增 battleScore 响应式数据，提供完整的 PK 对战体验。

- 业务价值：为直播平台提供竞技互动功能，增强直播趣味性和用户参与度。

- 应用场景：主播 PK、才艺比拼、游戏对战、互动竞技等娱乐场景。

   **响应式数据**

| **数据列表** | **描述** |
| --- | --- |
| [currentBattleInfo](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#currentBattleInfo) | 当前PK信息。 |
| [battleUsers](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#battleUsers) | PK参与用户列表。 |
| [battleScore](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#battleScore) | PK对战的实时比分。 |

   **接口函数**

| **函数列表** | **描述** |
| --- | --- |
| [requestBattle](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#requestBattle) | 请求 PK。 |
| [cancelBattleRequest](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#cancelBattleRequest) | 取消 PK 请求。 |
| [acceptBattle](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#acceptBattle) | 接受 PK。 |
| [rejectBattle](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#rejectBattle) | 拒绝 PK。 |
| [exitBattle](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#exitBattle) | 退出 PK。 |

## BarrageState

弹幕消息管理模块
- 核心功能：处理直播间内的文本消息、自定义消息等弹幕功能，支持弹幕发送、消息状态同步等完整弹幕系统，提供本地提示功能。

- 技术特点：支持高并发消息处理、实时消息同步、消息过滤、表情包支持等高级功能。新增 sendTextMessage、sendCustomMessage、appendLocalTip 接口函数。

- 业务价值：为直播平台提供核心的互动能力，增强用户参与度和直播氛围。

- 应用场景：弹幕互动、消息管理、表情包、聊天室等社交互动场景。

   **响应式数据**

| **数据列表** | **描述** |
| --- | --- |
| [messageList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#messageList) | 弹幕消息列表。 |

   **接口函数**

| **函数列表** | **描述** |
| --- | --- |
| [sendTextMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#sendTextMessage) | 发送文本消息。 |
| [sendCustomMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#sendCustomMessage) | 发送自定义消息。 |
| [appendLocalTip](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#appendLocalTip) | 添加本地提示。 |

## MessageListState

消息列表管理模块
- 核心功能：管理聊天消息列表，支持消息加载、滚动控制、已读回执、消息高亮等完整的消息展示功能。

- 技术特点：支持虚拟滚动、消息优化、实时更新等高性能消息处理。新增 activeConversationID、messageList、hasMoreOlderMessage 等响应式数据。

- 业务价值：为即时通信提供核心的消息展示能力，确保良好的聊天体验。

- 应用场景：即时通信、群聊、私聊、消息管理等通信场景。

   **响应式数据**

| **数据列表** | **描述** |
| --- | --- |
| [activeConversationID](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#activeConversationID) | 当前活跃的会话 ID。 |
| [messageList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#messageList) | 消息列表数据。 |
| [hasMoreOlderMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#hasMoreOlderMessage) | 是否有更多旧消息。 |
| [hasMoreNewerMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#hasMoreNewerMessage) | 是否有更多新消息。 |
| [enableReadReceipt](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#enableReadReceipt) | 是否启用已读回执。 |
| [isDisableScroll](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isDisableScroll) | 是否禁用滚动。 |
| [recalledMessageIDSet](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#recalledMessageIDSet) | 已撤回消息的 ID 集合。 |
| [highlightMessageIDSet](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#highlightMessageIDSet) | 高亮消息的 ID 集合。 |

   **接口函数**

| **函数列表** | **描述** |
| --- | --- |
| [setEnableReadReceipt](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setEnableReadReceipt) | 设置已读回执。 |
| [setIsDisableScroll](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setIsDisableScroll) | 设置滚动禁用。 |
| [highlightMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#highlightMessage) | 高亮消息。 |

## MessageInputState

消息输入管理模块
- 核心功能：管理消息输入框的状态和行为，支持文本输入、表情包、@功能、输入状态提示等完整的输入体验。

- 技术特点：支持富文本编辑、输入状态同步、草稿保存等功能。新增 inputRawValue、isPeerTyping 响应式数据。

- 业务价值：为用户提供便捷的消息输入体验，提升沟通效率。

- 应用场景：消息编辑、表情输入、文件发送、语音输入等输入场景。

   **响应式数据**

| **数据列表** | **描述** |
| --- | --- |
| [inputRawValue](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#inputRawValue) | 输入框的原始文本内容。 |
| [isPeerTyping](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isPeerTyping) | 对方是否正在输入。 |

   **接口函数**

| **函数列表** | **描述** |
| --- | --- |
| [updateRawValue](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#updateRawValue) | 更新原始值。 |
| [setEditorInstance](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setEditorInstance) | 设置编辑器实例。 |
| [setContent](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setContent) | 设置内容。 |
| [insertContent](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#insertContent) | 插入内容。 |
| [focusEditor](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#focusEditor) | 聚焦编辑器。 |
| [blurEditor](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#blurEditor) | 失焦编辑器。 |
| [sendMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#sendMessage) | 发送消息。 |

## MessageActionState

消息操作管理模块
- 核心功能：管理消息的各种操作，包括转发、引用、复制、删除、撤回等完整的消息操作功能。

- 技术特点：支持批量操作、操作状态管理、权限控制等功能。新增 forwardMessageIDList、isForwardMessageSelectionDone 等响应式数据。

- 业务价值：为用户提供丰富的消息操作能力，提升使用体验。

- 应用场景：消息转发、消息引用、消息管理、批量操作等场景。

   **响应式数据**

| **数据列表** | **描述** |
| --- | --- |
| [forwardMessageIDList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#forwardMessageIDList) | 要转发的消息 ID 列表。 |
| [isForwardMessageSelectionDone](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isForwardMessageSelectionDone) | 消息转发选择是否完成。 |
| [forwardConversationIDList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#forwardConversationIDList) | 转发目标会话 ID 列表。 |
| [quotedMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#quotedMessage) | 被引用的消息信息。 |

   **接口函数**

| **函数列表** | **描述** |
| --- | --- |
| [forwardMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#forwardMessage) | 转发消息。 |
| [setForwardMessageIDList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setForwardMessageIDList) | 设置转发消息列表。 |
| [setIsForwardMessageSelectionDone](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setIsForwardMessageSelectionDone) | 设置转发选择完成。 |
| [setForwardConversationIDList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setForwardConversationIDList) | 设置转发会话列表。 |
| [quoteMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#quoteMessage) | 引用消息。 |
| [clearQuotedMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#clearQuotedMessage) | 清除引用消息。 |
| [copyTextMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#copyTextMessage) | 复制文本消息。 |
| [deleteMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#deleteMessage) | 删除消息。 |
| [recallMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#recallMessage) | 撤回消息。 |
| [resetMessageActionState](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#resetMessageActionState) | 重置消息操作状态。 |

## ConversationListState

会话列表管理模块
- 核心功能：管理用户的会话列表，支持会话排序、未读统计、会话操作等完整的会话管理功能。

- 技术特点：支持实时会话更新、智能排序、网络状态监控等功能。新增 conversationList、activeConversation、totalUnRead、netStatus 响应式数据。

- 业务价值：为用户提供清晰的会话管理界面，提升沟通效率。

- 应用场景：会话管理、联系人列表、群组管理、消息中心等场景。

   **响应式数据**

| **数据列表** | **描述** |
| --- | --- |
| [conversationList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#conversationList) | 会话列表数据。 |
| [activeConversation](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#activeConversation) | 当前活跃的会话。 |
| [totalUnRead](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#totalUnRead) | 未读消息总数。 |
| [netStatus](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#netStatus) | 网络连接状态。 |

   **接口函数**

| **函数列表** | **描述** |
| --- | --- |
| [markConversationUnread](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#markConversationUnread) | 标记会话未读。 |
| [setActiveConversation](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setActiveConversation) | 设置活跃会话。 |
| [pinConversation](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#pinConversation) | 置顶会话。 |
| [deleteConversation](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#deleteConversation) | 删除会话。 |
| [muteConversation](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#muteConversation) | 静音会话。 |
| [setConversationDraft](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setConversationDraft) | 设置会话草稿。 |
| [createC2CConversation](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#createC2CConversation) | 创建单聊会话。 |
| [createGroupConversation](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#createGroupConversation) | 创建群聊会话。 |

## ContactListState

联系人管理模块
- 核心功能：管理用户的联系人列表，包括好友管理、群组管理、黑名单管理等完整的联系人功能。

- 技术特点：支持联系人分组、好友申请处理、群组申请管理等功能。新增 friendList、groupList、blackList 等响应式数据和完整的联系人操作接口。

- 业务价值：为用户提供完整的社交关系管理能力，构建社交网络。

- 应用场景：好友管理、群组管理、联系人搜索、社交网络等场景。

   **响应式数据**

| **数据列表** | **描述** |
| --- | --- |
| [friendList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#friendList) | 好友列表。 |
| [groupList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#groupList) | 群组列表。 |
| [blackList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#blackList) | 黑名单列表。 |
| [friendApplicationUnreadCount](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#friendApplicationUnreadCount) | 好友申请未读数。 |
| [friendGroupList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#friendGroupList) | 好友分组列表。 |
| [friendApplicationList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#friendApplicationList) | 好友申请列表。 |
| [groupApplicationList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#groupApplicationList) | 群申请列表。 |

   **接口函数**

| **函数列表** | **描述** |
| --- | --- |
| [setGroupApplicationList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setGroupApplicationList) | 设置群组申请列表。 |
| [setFriendList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setFriendList) | 设置好友列表。 |
| [setGroupList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setGroupList) | 设置群组列表。 |
| [setBlackList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setBlackList) | 设置黑名单列表。 |
| [setFriendApplicationUnreadCount](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setFriendApplicationUnreadCount) | 设置好友申请未读数。 |
| [setFriendGroupList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setFriendGroupList) | 设置好友分组列表。 |
| [setFriendApplicationList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setFriendApplicationList) | 设置好友申请列表。 |
| [initContactListWatcher](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#initContactListWatcher) | 初始化联系人监听器。 |
| [addFriend](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#addFriend) | 添加好友。 |
| [markFriendApplicationAsRead](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#markFriendApplicationAsRead) | 标记好友申请为已读。 |
| [acceptFriendApplication](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#acceptFriendApplication) | 接受好友申请。 |
| [refuseFriendApplication](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#refuseFriendApplication) | 拒绝好友申请。 |
| [addToBlacklist](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#addToBlacklist) | 添加到黑名单。 |
| [removeFromBlacklist](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#removeFromBlacklist) | 从黑名单移除。 |
| [deleteFriend](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#deleteFriend) | 删除好友。 |
| [setFriendRemark](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setFriendRemark) | 设置好友备注。 |
| [createFriendGroup](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#createFriendGroup) | 创建好友分组。 |
| [deleteFriendGroup](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#deleteFriendGroup) | 删除好友分组。 |
| [addToFriendGroup](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#addToFriendGroup) | 添加到好友分组。 |
| [removeFromFriendGroup](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#removeFromFriendGroup) | 从好友分组移除。 |
| [renameFriendGroup](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#renameFriendGroup) | 重命名好友分组。 |
| [joinGroup](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#joinGroup) | 加入群组。 |
| [acceptGroupApplication](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#acceptGroupApplication) | 接受群组申请。 |
| [refuseGroupApplication](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#refuseGroupApplication) | 拒绝群组申请。 |

## C2CSettingState

单聊设置管理模块
- 核心功能：管理单聊会话的各种设置，包括用户信息、聊天设置、权限控制等功能。

- 技术特点：支持实时设置同步、权限管理、个性化配置等功能。更新响应式数据为 userID、avatar、signature 等标准化字段。

- 业务价值：为用户提供个性化的单聊体验，提升沟通质量。

- 应用场景：单聊设置、用户信息管理、聊天权限控制等场景。

   **响应式数据**

| **数据列表** | **描述** |
| --- | --- |
| [currentConversationRef](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#currentConversationRef) | 当前会话引用。 |
| [userIDRef](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#userIDRef) | 用户 ID。 |
| [nickRef](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#nickRef) | 用户昵称。 |
| [avatarRef](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#avatarRef) | 用户头像。 |
| [signatureRef](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#signatureRef) | 用户个性签名。 |
| [remarkRef](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#remarkRef) | 好友备注名。 |
| [isMutedRef](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isMutedRef) | 会话静音状态。 |
| [isPinnedRef](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isPinnedRef) | 会话置顶状态。 |
| [isContactRef](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isContactRef) | 好友关系状态。 |
| [userID](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#userID) | 用户 ID。 |
| [avatar](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#avatar) | 用户头像 URL。 |
| [signature](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#signature) | 用户个性签名。 |
| [remark](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#remark) | 用户备注名。 |
| [isMuted](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isMuted) | 是否已静音。 |
| [isPinned](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isPinned) | 是否已置顶。 |
| [isContact](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isContact) | 是否为联系人。 |

   **接口函数**

| **函数列表** | **描述** |
| --- | --- |
| [setChatPinned](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setChatPinned) | 设置聊天置顶。 |
| [setChatMuted](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setChatMuted) | 设置聊天免打扰。 |
| [setUserRemark](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setUserRemark) | 设置用户备注。 |

## GroupSettingState

群聊设置管理模块
- 核心功能：管理群聊的各种设置和操作，包括群信息管理、成员管理、权限控制等完整的群管理功能。

- 技术特点：支持群权限管理、成员操作、群设置同步等功能。新增 groupID、groupType、groupName 等完整的群信息响应式数据和管理接口。

- 业务价值：为群主和管理员提供完整的群管理能力，维护群秩序。

- 应用场景：群管理、成员管理、权限控制、群设置等场景。

   **响应式数据**

| **数据列表** | **描述** |
| --- | --- |
| [groupID](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#groupID) | 群组 ID。 |
| [groupType](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#groupType) | 群组类型。 |
| [groupName](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#groupName) | 群组名称。 |
| [avatar](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#avatar) | 用户头像 URL。 |
| [introduction](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#introduction) | 群组介绍。 |
| [notification](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#notification) | 群组公告。 |
| [isMuted](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isMuted) | 是否已静音。 |
| [isPinned](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isPinned) | 是否已置顶。 |
| [groupOwner](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#groupOwner) | 群主信息。 |
| [adminMembers](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#adminMembers) | 管理员列表。 |
| [allMembers](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#allMembers) | 所有成员列表。 |
| [memberCount](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#memberCount) | 成员总数。 |
| [maxMemberCount](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#maxMemberCount) | 最大成员数。 |
| [currentUserID](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#currentUserID) | 当前用户 ID。 |
| [currentUserRole](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#currentUserRole) | 当前用户角色。 |
| [nameCard](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#nameCard) | 用户名片。 |
| [isMuteAllMembers](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isMuteAllMembers) | 是否禁言所有成员。 |
| [isInGroup](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isInGroup) | 是否在群组中。 |
| [inviteOption](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#inviteOption) | 邀请选项。 |

   **接口函数**

| **函数列表** | **描述** |
| --- | --- |
| [getGroupMemberList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getGroupMemberList) | 获取群成员列表。 |
| [updateGroupProfile](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#updateGroupProfile) | 更新群资料。 |
| [addGroupMember](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#addGroupMember) | 添加群成员。 |
| [deleteGroupMember](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#deleteGroupMember) | 删除群成员。 |
| [changeGroupOwner](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#changeGroupOwner) | 转让群主。 |
| [setGroupMemberRole](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setGroupMemberRole) | 设置群成员角色。 |
| [setGroupMemberNameCard](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setGroupMemberNameCard) | 设置群成员名片。 |
| [setChatPinned](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setChatPinned) | 设置聊天置顶。 |
| [setChatMuted](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setChatMuted) | 设置聊天免打扰。 |
| [setGroupMemberMuteTime](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setGroupMemberMuteTime) | 设置群成员禁言。 |
| [setMuteAllMember](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setMuteAllMember) | 设置全员禁言。 |
| [dismissGroup](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#dismissGroup) | 解散群组。 |
| [quitGroup](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#quitGroup) | 退出群组。 |
| [hasPermission](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#hasPermission) | 检查权限。 |
| [canOperateOnMember](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#canOperateOnMember) | 检查成员操作权限。 |
| [getAvailablePermissions](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getAvailablePermissions) | 获取可用权限。 |
| [initWatcher](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#initWatcher) | 初始化监听器。 |

## VideoMixerState

视频混流管理模块
- 核心功能：管理视频混流功能，支持多路视频合成、布局管理、媒体源控制等高级视频处理功能。

- 技术特点：支持实时视频混流、动态布局调整、媒体源管理等功能。新增 isVideoMixerEnabled、mediaSourceList、activeMediaSource 响应式数据和完整的混流控制接口。

- 业务价值：为直播平台提供专业的视频制作能力，提升直播质量。

- 应用场景：多人直播、画中画、视频合成、专业制作等场景。

   **响应式数据**

| **数据列表** | **描述** |
| --- | --- |
| [publishVideoQuality](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#publishVideoQuality) | 根据分辨率获取尺寸。 |
| [isVideoMixerEnabled](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isVideoMixerEnabled) | 视频混流是否启用。 |
| [mediaSourceList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#mediaSourceList) | 媒体源列表。 |
| [activeMediaSource](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#activeMediaSource) | 当前活跃的媒体源。 |

   **接口函数**

| **函数列表** | **描述** |
| --- | --- |
| [getVideoDataByQuality](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getVideoDataByQuality) | 根据质量获取视频数据。 |
| [getSizeByQuality](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getSizeByQuality) | 根据质量获取尺寸。 |
| [getSizeByResolution](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getSizeByResolution) | 根据分辨率获取尺寸。 |
| [transformTUIVideoQualityToTRTCVideoResolution](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#transformTUIVideoQualityToTRTCVideoResolution) | 转换视频质量到 TRTC 分辨率。 |
| [transformTRTCVideoResolutionToTUIVideoQuality](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#transformTRTCVideoResolutionToTUIVideoQuality) | 转换 TRTC 分辨率到视频质量。 |
| [transformTRTCVideoResModeToTUIVideoResMode](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#transformTRTCVideoResModeToTUIVideoResMode) | 转换 TRTC 分辨率模式。 |
| [changeActiveMediaSource](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#changeActiveMediaSource) | 切换活跃媒体源。 |
| [updateVideoQuality](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#updateVideoQuality) | 更新视频质量。 |
| [getDefaultLayoutByMediaSource](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getDefaultLayoutByMediaSource) | 根据媒体源获取默认布局。 |
| [addMediaSource](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#addMediaSource) | 添加媒体源。 |
| [updateMediaSource](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#updateMediaSource) | 更新媒体源。 |
| [removeMediaSource](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#removeMediaSource) | 移除媒体源。 |
| [enableLocalVideoMixer](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#enableLocalVideoMixer) | 启用本地视频混流。 |
| [clearMediaSource](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#clearMediaSource) | 清空所有媒体源。 |
| [initMediaSourceManager](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#initMediaSourceManager) | 初始化媒体源管理器。 |
| [initVideoMixerState](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#initVideoMixerState) | 初始化视频混流状态。 |

## VirtualBackgroundState

虚拟背景管理模块
- 核心功能：管理虚拟背景功能，支持背景替换、背景模糊、自定义背景等视频美化功能。

- 技术特点：基于 AI 技术实现实时背景分割和替换。新增 virtualBackgroundConfig 响应式数据和 isSupported、setVirtualBackground 接口函数。

- 业务价值：为用户提供隐私保护和视频美化功能，提升视频通话体验。

- 应用场景：视频通话、在线会议、直播美化、隐私保护等场景。

   **响应式数据**

| **数据列表** | **描述** |
| --- | --- |
| [virtualBackgroundConfig](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#virtualBackgroundConfig) | 虚拟背景配置。 |

   **接口函数**

| **函数列表** | **描述** |
| --- | --- |
| [initVirtualBackground](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#initVirtualBackground) | 初始化虚拟背景。 |
| [saveVirtualBackground](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#saveVirtualBackground) | 保存虚拟背景。 |
| [isSupported](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isSupported) | 检查是否支持。 |
| [setVirtualBackground](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setVirtualBackground) | 设置虚拟背景。 |

## ASRState

语音识别管理模块
- 核心功能：管理语音识别功能，支持实时语音转文字、转录历史管理、转录导出等功能。

- 技术特点：基于先进的 ASR 技术，支持多语言识别、实时转录、历史记录等功能。新增 recentTranscripts、transcriptHistory 响应式数据和 exportTranscripts 接口。

- 业务价值：为用户提供语音转文字服务，提升沟通效率和可访问性。

- 应用场景：会议记录、语音转录、无障碍通信、内容记录等场景。

   **响应式数据**

| **数据列表** | **描述** |
| --- | --- |
| [recentTranscripts](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#recentTranscripts) | 最近的语音转录记录。 |
| [transcriptHistory](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#transcriptHistory) | 语音转录历史记录。 |

   **接口函数**

| **函数列表** | **描述** |
| --- | --- |
| [setRecentTranscriptsDuration](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setRecentTranscriptsDuration) | 设置最近转录时长。 |
| [clearHistory](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#clearHistory) | 清空转录历史记录。 |
| [exportTranscripts](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#exportTranscripts) | 导出转录内容。 |

## SearchState

搜索功能管理模块
- 核心功能：管理全局搜索功能，支持消息搜索、用户搜索、群组搜索等多维度搜索能力。

- 技术特点：支持高级搜索、搜索历史、搜索建议等功能。重构响应式数据为 keyword、results、isLoading 等标准化字段，提供完整的搜索接口。

- 业务价值：为用户提供快速查找信息的能力，提升使用效率。

- 应用场景：消息搜索、联系人搜索、内容查找、历史记录等场景。

   **响应式数据**

| **数据列表** | **描述** |
| --- | --- |
| [keyword](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#keyword) | 搜索关键词。 |
| [results](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#results) | 搜索结果。 |
| [isLoading](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isLoading) | 是否正在加载。 |
| [error](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#error) | 错误信息。 |
| [searchAdvancedParams](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#searchAdvancedParams) | 高级搜索参数。 |
| [selectedSearchType](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#selectedSearchType) | 选中的搜索类型。 |

   **接口函数**

| **函数列表** | **描述** |
| --- | --- |
| [search](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#search) | 搜索。 |
| [setKeyword](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setKeyword) | 设置关键词。 |
| [setSelectedType](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setSelectedType) | 设置选中类型。 |
| [setSearchMessageAdvancedParams](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setSearchMessageAdvancedParams) | 设置消息搜索高级参数。 |
| [setSearchUserAdvancedParams](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setSearchUserAdvancedParams) | 设置用户搜索高级参数。 |
| [setSearchGroupAdvancedParams](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setSearchGroupAdvancedParams) | 设置群组搜索高级参数。 |
| [loadMore](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#loadMore) | 加载更多。 |

## SeatStore

座位存储管理模块
- 核心功能：提供座位状态的底层存储和管理，支持座位信息缓存、用户信息映射、设备请求处理等核心功能。

- 技术特点：采用响应式存储设计，支持实时状态同步、事件驱动更新等功能。新增 liveOwnerUserId、localUserId、seatList 等响应式数据和 getUserInfo、convertUserInfoToAudienceInfo 接口。

- 业务价值：为座位管理提供可靠的数据基础，确保座位状态的一致性。

- 应用场景：座位状态管理、用户信息存储、设备状态跟踪等底层场景。

   **响应式数据**

| **数据列表** | **描述** |
| --- | --- |
| [liveOwnerUserId](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#liveOwnerUserId) | 直播间主播用户 ID。 |
| [localUserId](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#localUserId) | 本地用户 ID。 |
| [seatList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#seatList) | 麦位列表，包含所有麦位的状态和用户信息。 |
| [coHostUserList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#coHostUserList) | 连麦主播列表。 |
| [sentDeviceRequestMap](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#sentDeviceRequestMap) | 已发送的设备请求映射。 |
| [receivedDeviceRequestMap](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#receivedDeviceRequestMap) | 已接收的设备请求映射。 |
| [userInfoMap](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#userInfoMap) | 用户信息映射表。 |

   **接口函数**

| 函数列表 | 描述 |
| --- | --- |
| [getUserInfo](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getUserInfo) | 获取用户信息。 |
| [convertUserInfoToAudienceInfo](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#convertUserInfoToAudienceInfo) | 转换用户信息为观众信息。 |

