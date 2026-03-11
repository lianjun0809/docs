> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

atomicx-core SDK 是腾讯云最新推出的面向即时通信、音视频通话、视频直播、语聊房等场景的全新一代基于响应式的 API，您可以非常快速的基于这组 API 构建自己的 UI 页面，它支持房间管理、屏幕分享、成员管理、麦位控制、基础美颜等丰富功能，同时基于 TRTC SDK，能够提供超低延时、高品质的音视频体验，本页面包含 atomicx-core SDK 的所有 API 接口，按功能模块分类展示。

## LoginState

用户身份认证与登录管理模块
- 核心功能：提供用户登录、登出、个人信息管理等基础身份认证功能，是整个系统的用户身份基础。

- 技术特点：支持多种登录方式、用户信息缓存、登录状态持久化等功能，确保用户身份的安全性和可靠性。

- 业务价值：为所有业务模块提供统一的用户身份认证服务，是系统安全和用户体验的基础保障。

- 应用场景：用户登录、身份验证、个人信息管理、权限控制等核心身份认证场景。


   **响应式数据**

<table>
<tr>
<td rowspan="1" colSpan="1" >**数据列表**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[loginUserInfo](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#loginUserInfo)</td>

<td rowspan="1" colSpan="1" >当前登录用户信息。</td>
</tr>
</table>


   **接口函数**

<table>
<tr>
<td rowspan="1" colSpan="1" >**函数列表**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[login](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#login)</td>

<td rowspan="1" colSpan="1" >用户登录。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setSelfInfo](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setSelfInfo)</td>

<td rowspan="1" colSpan="1" >设置用户个人信息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[logout](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#logout)</td>

<td rowspan="1" colSpan="1" >用户登出函数。</td>
</tr>
</table>


## DeviceState

设备状态管理模块
- 核心功能：管理摄像头、麦克风等音视频设备的控制，提供设备状态监控、权限检查等基础设备服务。

- 技术特点：支持多设备管理、设备状态实时监控、权限动态检查、设备故障自动恢复等高级功能。

- 业务价值：为直播系统提供稳定的设备基础，确保音视频采集的可靠性和用户体验。

- 应用场景：设备管理、权限控制、音视频采集、设备故障处理等基础技术场景。


   **响应式数据**

<table>
<tr>
<td rowspan="1" colSpan="1" >**数据列表**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[microphoneStatus](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#microphoneStatus)</td>

<td rowspan="1" colSpan="1" >麦克风状态。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[microphoneList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#microphoneList)</td>

<td rowspan="1" colSpan="1" >麦克风设备列表。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[currentMicrophone](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#currentMicrophone)</td>

<td rowspan="1" colSpan="1" >当前选中的麦克风设备。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[microphoneLastError](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#microphoneLastError)</td>

<td rowspan="1" colSpan="1" >麦克风最后一次错误信息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[captureVolume](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#captureVolume)</td>

<td rowspan="1" colSpan="1" >麦克风采集音量。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[currentMicVolume](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#currentMicVolume)</td>

<td rowspan="1" colSpan="1" >当前麦克风音量。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[isMicrophoneTesting](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isMicrophoneTesting)</td>

<td rowspan="1" colSpan="1" >麦克风测试状态。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[testingMicVolume](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#testingMicVolume)</td>

<td rowspan="1" colSpan="1" >测试时的麦克风音量。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[cameraStatus](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#cameraStatus)</td>

<td rowspan="1" colSpan="1" >摄像头状态。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[cameraList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#cameraList)</td>

<td rowspan="1" colSpan="1" >摄像头设备列表。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[currentCamera](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#currentCamera)</td>

<td rowspan="1" colSpan="1" >当前选中的摄像头设备。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[cameraLastError](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#cameraLastError)</td>

<td rowspan="1" colSpan="1" >摄像头最后一次错误信息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[isCameraTesting](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isCameraTesting)</td>

<td rowspan="1" colSpan="1" >摄像头测试状态。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[isCameraTestLoading](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isCameraTestLoading)</td>

<td rowspan="1" colSpan="1" >摄像头测试加载状态。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[isFrontCamera](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isFrontCamera)</td>

<td rowspan="1" colSpan="1" >是否为前置摄像头。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[localMirrorType](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#localMirrorType)</td>

<td rowspan="1" colSpan="1" >本地视频镜像类型。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[localVideoQuality](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#localVideoQuality)</td>

<td rowspan="1" colSpan="1" >本地视频质量。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[speakerList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#speakerList)</td>

<td rowspan="1" colSpan="1" >扬声器设备列表。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[currentSpeaker](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#currentSpeaker)</td>

<td rowspan="1" colSpan="1" >当前选中的扬声器设备。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[outputVolume](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#outputVolume)</td>

<td rowspan="1" colSpan="1" >扬声器输出音量。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[currentAudioRoute](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#currentAudioRoute)</td>

<td rowspan="1" colSpan="1" >当前音频路由。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[isSpeakerTesting](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isSpeakerTesting)</td>

<td rowspan="1" colSpan="1" >扬声器测试状态。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[screenStatus](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#screenStatus)</td>

<td rowspan="1" colSpan="1" >屏幕分享状态。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[networkInfo](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#networkInfo)</td>

<td rowspan="1" colSpan="1" >网络信息。</td>
</tr>
</table>


   **接口函数**

<table>
<tr>
<td rowspan="1" colSpan="1" >**函数列表**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[openLocalMicrophone](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#openLocalMicrophone)</td>

<td rowspan="1" colSpan="1" >开启本地麦克风。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[closeLocalMicrophone](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#closeLocalMicrophone)</td>

<td rowspan="1" colSpan="1" >关闭本地麦克风。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[muteLocalAudio](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#muteLocalAudio)</td>

<td rowspan="1" colSpan="1" >静音本地音频。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[unmuteLocalAudio](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#unmuteLocalAudio)</td>

<td rowspan="1" colSpan="1" >取消静音本地音频。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getMicrophoneList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getMicrophoneList)</td>

<td rowspan="1" colSpan="1" >获取麦克风设备列表。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setCurrentMicrophone](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setCurrentMicrophone)</td>

<td rowspan="1" colSpan="1" >设置当前麦克风设备。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[startMicrophoneTest](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#startMicrophoneTest)</td>

<td rowspan="1" colSpan="1" >开始麦克风测试。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setCaptureVolume](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setCaptureVolume)</td>

<td rowspan="1" colSpan="1" >设置音频采集音量。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setOutputVolume](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setOutputVolume)</td>

<td rowspan="1" colSpan="1" >设置音频播放音量。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[stopMicrophoneTest](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#stopMicrophoneTest)</td>

<td rowspan="1" colSpan="1" >停止麦克风测试。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getSpeakerList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getSpeakerList)</td>

<td rowspan="1" colSpan="1" >获取扬声器设备列表。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setCurrentSpeaker](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setCurrentSpeaker)</td>

<td rowspan="1" colSpan="1" >设置当前扬声器设备。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setAudioRoute](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setAudioRoute)</td>

<td rowspan="1" colSpan="1" >设置音频路由。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[startSpeakerTest](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#startSpeakerTest)</td>

<td rowspan="1" colSpan="1" >开始扬声器测试。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[stopSpeakerTest](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#stopSpeakerTest)</td>

<td rowspan="1" colSpan="1" >停止扬声器测试。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[openLocalCamera](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#openLocalCamera)</td>

<td rowspan="1" colSpan="1" >开启本地摄像头。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[closeLocalCamera](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#closeLocalCamera)</td>

<td rowspan="1" colSpan="1" >关闭本地摄像头。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getCameraList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getCameraList)</td>

<td rowspan="1" colSpan="1" >获取摄像头设备列表。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setCurrentCamera](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setCurrentCamera)</td>

<td rowspan="1" colSpan="1" >设置当前摄像头设备。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[switchCamera](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#switchCamera)</td>

<td rowspan="1" colSpan="1" >切换前后摄像头。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[switchMirror](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#switchMirror)</td>

<td rowspan="1" colSpan="1" >切换视频镜像模式。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[updateVideoQuality](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#updateVideoQuality)</td>

<td rowspan="1" colSpan="1" >更新视频质量。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[startCameraDeviceTest](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#startCameraDeviceTest)</td>

<td rowspan="1" colSpan="1" >开始摄像头设备测试。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[startScreenShare](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#startScreenShare)</td>

<td rowspan="1" colSpan="1" >开始屏幕分享。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[stopScreenShare](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#stopScreenShare)</td>

<td rowspan="1" colSpan="1" >停止屏幕分享。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[stopCameraDeviceTest](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#stopCameraDeviceTest)</td>

<td rowspan="1" colSpan="1" >停止摄像头设备测试。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[screenCaptureStopped](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#screenCaptureStopped)</td>

<td rowspan="1" colSpan="1" >屏幕分享停止回调。</td>
</tr>
</table>


## LiveListState

直播列表管理模块
- 核心功能：管理直播间的完整生命周期，包括创建、加入、离开、结束等核心业务流程，支持直播列表的分页获取和实时更新。

- 技术特点：支持分页加载、实时状态同步、直播信息动态更新，采用响应式数据管理，确保 UI 与数据状态实时同步。新增 liveList 和 liveListCursor 响应式数据，提供 fetchLiveList 接口函数。

- 业务价值：为直播平台提供核心的直播间管理能力，支持大规模并发直播场景，是直播业务的基础设施。

- 应用场景：直播列表展示、直播间创建、直播状态管理、直播数据统计等核心业务场景。


   **响应式数据**

<table>
<tr>
<td rowspan="1" colSpan="1" >**数据列表**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[currentLive](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#currentLive)</td>

<td rowspan="1" colSpan="1" >转换TUILiveInfo为LiveInfo格式。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[liveList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#liveList)</td>

<td rowspan="1" colSpan="1" >直播列表数据，包含所有直播间的信息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[liveListCursor](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#liveListCursor)</td>

<td rowspan="1" colSpan="1" >直播列表分页游标，用于获取下一页数据。</td>
</tr>
</table>


   **接口函数**

<table>
<tr>
<td rowspan="1" colSpan="1" >**函数列表**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createLive](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#createLive)</td>

<td rowspan="1" colSpan="1" >创建直播间。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[joinLive](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#joinLive)</td>

<td rowspan="1" colSpan="1" >加入直播间。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[leaveLive](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#leaveLive)</td>

<td rowspan="1" colSpan="1" >离开直播间。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[endLive](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#endLive)</td>

<td rowspan="1" colSpan="1" >结束直播。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[updateLiveInfo](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#updateLiveInfo)</td>

<td rowspan="1" colSpan="1" >更新直播间信息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[queryMetaData](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#queryMetaData)</td>

<td rowspan="1" colSpan="1" >查询元数据。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[updateLiveMetaData](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#updateLiveMetaData)</td>

<td rowspan="1" colSpan="1" >更新直播间元数据。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[fetchLiveList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#fetchLiveList)</td>

<td rowspan="1" colSpan="1" >获取直播列表。</td>
</tr>
</table>


## LiveSeatState

直播间座位管理模块
- 核心功能：实现多人连麦场景下的座位控制，支持复杂的座位状态管理和音视频设备控制，包括上麦、下麦、座位锁定等完整功能。

- 技术特点：基于 WebRTC 技术，支持多路音视频流管理，提供座位锁定、设备控制、权限管理等高级功能。新增 seatList、canvas、speakingUsers、networkQualities 响应式数据，以及完整的座位操作接口。

- 业务价值：为多人互动直播提供核心技术支撑，支持 PK、连麦、多人游戏等丰富的互动场景。

- 应用场景：多人连麦、主播 PK、互动游戏、在线教育、会议直播等需要多人音视频互动的场景。


   **响应式数据**

<table>
<tr>
<td rowspan="1" colSpan="1" >**数据列表**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[seatList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#seatList)</td>

<td rowspan="1" colSpan="1" >麦位列表，包含所有麦位的状态和用户信息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[canvas](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#canvas)</td>

<td rowspan="1" colSpan="1" >画布配置，用于视频渲染和布局管理。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[speakingUsers](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#speakingUsers)</td>

<td rowspan="1" colSpan="1" >正在发言的用户列表。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[networkQualities](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#networkQualities)</td>

<td rowspan="1" colSpan="1" >网络质量信息，包含各用户的网络状态。</td>
</tr>
</table>


   **接口函数**

<table>
<tr>
<td rowspan="1" colSpan="1" >**函数列表**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[takeSeat](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#takeSeat)</td>

<td rowspan="1" colSpan="1" >用户上麦。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[leaveSeat](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#leaveSeat)</td>

<td rowspan="1" colSpan="1" >用户下麦。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[lockSeat](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#lockSeat)</td>

<td rowspan="1" colSpan="1" >锁定麦位。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[unLockSeat](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#unLockSeat)</td>

<td rowspan="1" colSpan="1" >解锁麦位。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[kickUserOutOfSeat](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#kickUserOutOfSeat)</td>

<td rowspan="1" colSpan="1" >踢用户下麦。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[moveUserToSeat](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#moveUserToSeat)</td>

<td rowspan="1" colSpan="1" >移动用户到指定麦位。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[openRemoteCamera](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#openRemoteCamera)</td>

<td rowspan="1" colSpan="1" >开启远端摄像头。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[closeRemoteCamera](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#closeRemoteCamera)</td>

<td rowspan="1" colSpan="1" >关闭远端摄像头。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[openRemoteMicrophone](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#openRemoteMicrophone)</td>

<td rowspan="1" colSpan="1" >开启远端麦克风。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[closeRemoteMicrophone](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#closeRemoteMicrophone)</td>

<td rowspan="1" colSpan="1" >关闭远端麦克风。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[muteMicrophone](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#muteMicrophone)</td>

<td rowspan="1" colSpan="1" >静音麦克风。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[unmuteMicrophone](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#unmuteMicrophone)</td>

<td rowspan="1" colSpan="1" >取消静音麦克风。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[startPlayStream](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#startPlayStream)</td>

<td rowspan="1" colSpan="1" >开始播放流。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[stopPlayStream](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#stopPlayStream)</td>

<td rowspan="1" colSpan="1" >停止播放流。</td>
</tr>
</table>


## LiveAudienceState

直播间观众管理模块
- 核心功能：管理直播间观众列表，提供观众权限控制、管理员设置等直播间秩序维护功能，支持实时观众统计。

- 技术特点：支持实时观众列表更新、权限分级管理、批量操作等高级功能，确保直播间秩序和用户体验。新增 audienceList 和 audienceCount 响应式数据。

- 业务价值：为直播平台提供完整的观众管理解决方案，支持大规模观众场景下的秩序维护。

- 应用场景：观众管理、权限控制、直播间秩序维护、观众互动管理等核心业务场景。


   **响应式数据**

<table>
<tr>
<td rowspan="1" colSpan="1" >**数据列表**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[audienceList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#audienceList)</td>

<td rowspan="1" colSpan="1" >观众列表，包含直播间所有观众的信息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[audienceCount](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#audienceCount)</td>

<td rowspan="1" colSpan="1" >观众总数统计。</td>
</tr>
</table>


   **接口函数**

<table>
<tr>
<td rowspan="1" colSpan="1" >**函数列表**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[fetchAudienceList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#fetchAudienceList)</td>

<td rowspan="1" colSpan="1" >获取观众列表。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setAdministrator](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setAdministrator)</td>

<td rowspan="1" colSpan="1" >设置管理员。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[revokeAdministrator](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#revokeAdministrator)</td>

<td rowspan="1" colSpan="1" >撤销管理员。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[kickUserOutOfRoom](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#kickUserOutOfRoom)</td>

<td rowspan="1" colSpan="1" >踢出房间。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[disableSendMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#disableSendMessage)</td>

<td rowspan="1" colSpan="1" >禁言用户。</td>
</tr>
</table>


## LiveMonitorState

直播监控管理模块
- 核心功能：提供直播间实时监控功能，包括直播状态监控、数据统计、异常检测等核心监控能力，支持多直播间监控。

- 技术特点：支持实时数据采集、多维度监控指标、智能告警机制，确保直播服务的稳定性和可靠性。新增 monitorLiveInfoList 响应式数据，优化监控接口。

- 业务价值：为直播平台提供全方位的监控保障，及时发现和处理异常情况，提升服务质量。

- 应用场景：直播质量监控、性能分析、异常告警、数据统计等运营管理场景。


   **响应式数据**

<table>
<tr>
<td rowspan="1" colSpan="1" >**数据列表**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[monitorLiveInfoList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#monitorLiveInfoList)</td>

<td rowspan="1" colSpan="1" >监控的直播间信息列表。</td>
</tr>
</table>


   **接口函数**

<table>
<tr>
<td rowspan="1" colSpan="1" >**函数列表**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[init](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#init)</td>

<td rowspan="1" colSpan="1" >初始化监控。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getLiveList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getLiveList)</td>

<td rowspan="1" colSpan="1" >获取直播列表。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[closeRoom](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#closeRoom)</td>

<td rowspan="1" colSpan="1" >关闭房间。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[sendMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#sendMessage)</td>

<td rowspan="1" colSpan="1" >发送消息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[startPlay](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#startPlay)</td>

<td rowspan="1" colSpan="1" >开始播放。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[stopPlay](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#stopPlay)</td>

<td rowspan="1" colSpan="1" >停止播放。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[muteLiveAudio](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#muteLiveAudio)</td>

<td rowspan="1" colSpan="1" >静音直播音频。</td>
</tr>
</table>


## CoGuestState

连麦嘉宾管理模块
- 核心功能：处理观众与主播之间的连麦互动，管理连麦申请、邀请、接受、拒绝等完整的连麦流程，支持连麦状态管理。

- 技术特点：基于实时音视频技术，支持连麦状态实时同步、音视频质量自适应、网络状况监控等高级功能。新增 connected、invitees、applicants、candidates 响应式数据和 applyForSeat 接口。

- 业务价值：为直播平台提供观众参与互动的核心能力，增强用户粘性和直播趣味性。

- 应用场景：观众连麦、互动问答、在线K歌、游戏直播等需要观众参与的互动场景。


   **响应式数据**

<table>
<tr>
<td rowspan="1" colSpan="1" >**数据列表**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[candidates](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#candidates)</td>

<td rowspan="1" colSpan="1" >取消订阅连麦事件。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[connected](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#connected)</td>

<td rowspan="1" colSpan="1" >连麦连接状态。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[invitees](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#invitees)</td>

<td rowspan="1" colSpan="1" >被邀请的用户列表。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[applicants](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#applicants)</td>

<td rowspan="1" colSpan="1" >申请连麦的用户列表。</td>
</tr>
</table>


   **接口函数**

<table>
<tr>
<td rowspan="1" colSpan="1" >**函数列表**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[cancelApplication](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#cancelApplication)</td>

<td rowspan="1" colSpan="1" >取消申请。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[acceptApplication](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#acceptApplication)</td>

<td rowspan="1" colSpan="1" >接受申请。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[rejectApplication](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#rejectApplication)</td>

<td rowspan="1" colSpan="1" >拒绝申请。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[cancelInvitation](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#cancelInvitation)</td>

<td rowspan="1" colSpan="1" >取消邀请。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[acceptInvitation](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#acceptInvitation)</td>

<td rowspan="1" colSpan="1" >接受邀请。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[rejectInvitation](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#rejectInvitation)</td>

<td rowspan="1" colSpan="1" >拒绝邀请。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[disConnect](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#disConnect)</td>

<td rowspan="1" colSpan="1" >断开连接。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[applyForSeat](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#applyForSeat)</td>

<td rowspan="1" colSpan="1" >申请上麦。</td>
</tr>
</table>


## CoHostState

连麦主播管理模块
- 核心功能：实现主播间的连麦功能，支持主播邀请、连麦申请、连麦状态管理等主播间互动功能，提供完整的主播连麦流程。

- 技术特点：支持多主播音视频同步、画中画显示、音视频质量优化等高级技术，确保连麦体验的流畅性。新增 coHostStatus、connected、applicant、invitees、candidates 响应式数据和完整的连麦控制接口。

- 业务价值：为直播平台提供主播间协作的核心能力，支持 PK、合作直播等高级业务场景。

- 应用场景：主播 PK、合作直播、跨平台连麦、主播互动等高级直播场景。


   **响应式数据**

<table>
<tr>
<td rowspan="1" colSpan="1" >**数据列表**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[coHostStatus](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#coHostStatus)</td>

<td rowspan="1" colSpan="1" >连麦主播状态。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[connected](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#connected)</td>

<td rowspan="1" colSpan="1" >连麦连接状态。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[applicant](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#applicant)</td>

<td rowspan="1" colSpan="1" >申请连麦的主播信息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[invitees](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#invitees)</td>

<td rowspan="1" colSpan="1" >被邀请的用户列表。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[candidates](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#candidates)</td>

<td rowspan="1" colSpan="1" >候选用户列表。</td>
</tr>
</table>


   **接口函数**

<table>
<tr>
<td rowspan="1" colSpan="1" >**函数列表**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[requestHostConnection](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#requestHostConnection)</td>

<td rowspan="1" colSpan="1" >请求主播连麦。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[cancelHostConnection](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#cancelHostConnection)</td>

<td rowspan="1" colSpan="1" >取消主播连麦。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[acceptHostConnection](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#acceptHostConnection)</td>

<td rowspan="1" colSpan="1" >接受主播连麦。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[rejectHostConnection](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#rejectHostConnection)</td>

<td rowspan="1" colSpan="1" >拒绝主播连麦。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[exitHostConnection](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#exitHostConnection)</td>

<td rowspan="1" colSpan="1" >退出主播连麦。</td>
</tr>
</table>


## BattleState

PK 对战管理模块
- 核心功能：管理主播间的 PK 对战功能，包括对战邀请、接受、拒绝、结束等完整的 PK 流程，支持实时比分统计。

- 技术特点：支持实时对战状态同步、比分计算、对战结果统计等功能。新增 battleScore 响应式数据，提供完整的 PK 对战体验。

- 业务价值：为直播平台提供竞技互动功能，增强直播趣味性和用户参与度。

- 应用场景：主播 PK、才艺比拼、游戏对战、互动竞技等娱乐场景。


   **响应式数据**

<table>
<tr>
<td rowspan="1" colSpan="1" >**数据列表**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[currentBattleInfo](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#currentBattleInfo)</td>

<td rowspan="1" colSpan="1" >当前PK信息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[battleUsers](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#battleUsers)</td>

<td rowspan="1" colSpan="1" >PK参与用户列表。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[battleScore](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#battleScore)</td>

<td rowspan="1" colSpan="1" >PK对战的实时比分。</td>
</tr>
</table>


   **接口函数**

<table>
<tr>
<td rowspan="1" colSpan="1" >**函数列表**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[requestBattle](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#requestBattle)</td>

<td rowspan="1" colSpan="1" >请求 PK。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[cancelBattleRequest](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#cancelBattleRequest)</td>

<td rowspan="1" colSpan="1" >取消 PK 请求。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[acceptBattle](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#acceptBattle)</td>

<td rowspan="1" colSpan="1" >接受 PK。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[rejectBattle](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#rejectBattle)</td>

<td rowspan="1" colSpan="1" >拒绝 PK。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[exitBattle](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#exitBattle)</td>

<td rowspan="1" colSpan="1" >退出 PK。</td>
</tr>
</table>


## BarrageState

弹幕消息管理模块
- 核心功能：处理直播间内的文本消息、自定义消息等弹幕功能，支持弹幕发送、消息状态同步等完整弹幕系统，提供本地提示功能。

- 技术特点：支持高并发消息处理、实时消息同步、消息过滤、表情包支持等高级功能。新增 sendTextMessage、sendCustomMessage、appendLocalTip 接口函数。

- 业务价值：为直播平台提供核心的互动能力，增强用户参与度和直播氛围。

- 应用场景：弹幕互动、消息管理、表情包、聊天室等社交互动场景。


   **响应式数据**

<table>
<tr>
<td rowspan="1" colSpan="1" >**数据列表**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[messageList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#messageList)</td>

<td rowspan="1" colSpan="1" >弹幕消息列表。</td>
</tr>
</table>


   **接口函数**

<table>
<tr>
<td rowspan="1" colSpan="1" >**函数列表**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[sendTextMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#sendTextMessage)</td>

<td rowspan="1" colSpan="1" >发送文本消息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[sendCustomMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#sendCustomMessage)</td>

<td rowspan="1" colSpan="1" >发送自定义消息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[appendLocalTip](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#appendLocalTip)</td>

<td rowspan="1" colSpan="1" >添加本地提示。</td>
</tr>
</table>


## MessageListState

消息列表管理模块
- 核心功能：管理聊天消息列表，支持消息加载、滚动控制、已读回执、消息高亮等完整的消息展示功能。

- 技术特点：支持虚拟滚动、消息优化、实时更新等高性能消息处理。新增 activeConversationID、messageList、hasMoreOlderMessage 等响应式数据。

- 业务价值：为即时通信提供核心的消息展示能力，确保良好的聊天体验。

- 应用场景：即时通信、群聊、私聊、消息管理等通信场景。


   **响应式数据**

<table>
<tr>
<td rowspan="1" colSpan="1" >**数据列表**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[activeConversationID](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#activeConversationID)</td>

<td rowspan="1" colSpan="1" >当前活跃的会话 ID。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[messageList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#messageList)</td>

<td rowspan="1" colSpan="1" >消息列表数据。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[hasMoreOlderMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#hasMoreOlderMessage)</td>

<td rowspan="1" colSpan="1" >是否有更多旧消息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[hasMoreNewerMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#hasMoreNewerMessage)</td>

<td rowspan="1" colSpan="1" >是否有更多新消息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[enableReadReceipt](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#enableReadReceipt)</td>

<td rowspan="1" colSpan="1" >是否启用已读回执。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[isDisableScroll](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isDisableScroll)</td>

<td rowspan="1" colSpan="1" >是否禁用滚动。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[recalledMessageIDSet](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#recalledMessageIDSet)</td>

<td rowspan="1" colSpan="1" >已撤回消息的 ID 集合。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[highlightMessageIDSet](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#highlightMessageIDSet)</td>

<td rowspan="1" colSpan="1" >高亮消息的 ID 集合。</td>
</tr>
</table>


   **接口函数**

<table>
<tr>
<td rowspan="1" colSpan="1" >**函数列表**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setEnableReadReceipt](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setEnableReadReceipt)</td>

<td rowspan="1" colSpan="1" >设置已读回执。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setIsDisableScroll](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setIsDisableScroll)</td>

<td rowspan="1" colSpan="1" >设置滚动禁用。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[highlightMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#highlightMessage)</td>

<td rowspan="1" colSpan="1" >高亮消息。</td>
</tr>
</table>


## MessageInputState

消息输入管理模块
- 核心功能：管理消息输入框的状态和行为，支持文本输入、表情包、@功能、输入状态提示等完整的输入体验。

- 技术特点：支持富文本编辑、输入状态同步、草稿保存等功能。新增 inputRawValue、isPeerTyping 响应式数据。

- 业务价值：为用户提供便捷的消息输入体验，提升沟通效率。

- 应用场景：消息编辑、表情输入、文件发送、语音输入等输入场景。


   **响应式数据**

<table>
<tr>
<td rowspan="1" colSpan="1" >**数据列表**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[inputRawValue](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#inputRawValue)</td>

<td rowspan="1" colSpan="1" >输入框的原始文本内容。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[isPeerTyping](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isPeerTyping)</td>

<td rowspan="1" colSpan="1" >对方是否正在输入。</td>
</tr>
</table>


   **接口函数**

<table>
<tr>
<td rowspan="1" colSpan="1" >**函数列表**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[updateRawValue](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#updateRawValue)</td>

<td rowspan="1" colSpan="1" >更新原始值。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setEditorInstance](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setEditorInstance)</td>

<td rowspan="1" colSpan="1" >设置编辑器实例。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setContent](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setContent)</td>

<td rowspan="1" colSpan="1" >设置内容。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[insertContent](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#insertContent)</td>

<td rowspan="1" colSpan="1" >插入内容。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[focusEditor](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#focusEditor)</td>

<td rowspan="1" colSpan="1" >聚焦编辑器。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[blurEditor](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#blurEditor)</td>

<td rowspan="1" colSpan="1" >失焦编辑器。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[sendMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#sendMessage)</td>

<td rowspan="1" colSpan="1" >发送消息。</td>
</tr>
</table>


## MessageActionState

消息操作管理模块
- 核心功能：管理消息的各种操作，包括转发、引用、复制、删除、撤回等完整的消息操作功能。

- 技术特点：支持批量操作、操作状态管理、权限控制等功能。新增 forwardMessageIDList、isForwardMessageSelectionDone 等响应式数据。

- 业务价值：为用户提供丰富的消息操作能力，提升使用体验。

- 应用场景：消息转发、消息引用、消息管理、批量操作等场景。


   **响应式数据**

<table>
<tr>
<td rowspan="1" colSpan="1" >**数据列表**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[forwardMessageIDList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#forwardMessageIDList)</td>

<td rowspan="1" colSpan="1" >要转发的消息 ID 列表。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[isForwardMessageSelectionDone](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isForwardMessageSelectionDone)</td>

<td rowspan="1" colSpan="1" >消息转发选择是否完成。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[forwardConversationIDList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#forwardConversationIDList)</td>

<td rowspan="1" colSpan="1" >转发目标会话 ID 列表。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[quotedMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#quotedMessage)</td>

<td rowspan="1" colSpan="1" >被引用的消息信息。</td>
</tr>
</table>


   **接口函数**

<table>
<tr>
<td rowspan="1" colSpan="1" >**函数列表**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[forwardMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#forwardMessage)</td>

<td rowspan="1" colSpan="1" >转发消息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setForwardMessageIDList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setForwardMessageIDList)</td>

<td rowspan="1" colSpan="1" >设置转发消息列表。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setIsForwardMessageSelectionDone](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setIsForwardMessageSelectionDone)</td>

<td rowspan="1" colSpan="1" >设置转发选择完成。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setForwardConversationIDList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setForwardConversationIDList)</td>

<td rowspan="1" colSpan="1" >设置转发会话列表。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[quoteMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#quoteMessage)</td>

<td rowspan="1" colSpan="1" >引用消息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[clearQuotedMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#clearQuotedMessage)</td>

<td rowspan="1" colSpan="1" >清除引用消息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[copyTextMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#copyTextMessage)</td>

<td rowspan="1" colSpan="1" >复制文本消息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#deleteMessage)</td>

<td rowspan="1" colSpan="1" >删除消息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[recallMessage](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#recallMessage)</td>

<td rowspan="1" colSpan="1" >撤回消息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[resetMessageActionState](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#resetMessageActionState)</td>

<td rowspan="1" colSpan="1" >重置消息操作状态。</td>
</tr>
</table>


## ConversationListState

会话列表管理模块
- 核心功能：管理用户的会话列表，支持会话排序、未读统计、会话操作等完整的会话管理功能。

- 技术特点：支持实时会话更新、智能排序、网络状态监控等功能。新增 conversationList、activeConversation、totalUnRead、netStatus 响应式数据。

- 业务价值：为用户提供清晰的会话管理界面，提升沟通效率。

- 应用场景：会话管理、联系人列表、群组管理、消息中心等场景。


   **响应式数据**

<table>
<tr>
<td rowspan="1" colSpan="1" >**数据列表**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[conversationList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#conversationList)</td>

<td rowspan="1" colSpan="1" >会话列表数据。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[activeConversation](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#activeConversation)</td>

<td rowspan="1" colSpan="1" >当前活跃的会话。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[totalUnRead](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#totalUnRead)</td>

<td rowspan="1" colSpan="1" >未读消息总数。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[netStatus](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#netStatus)</td>

<td rowspan="1" colSpan="1" >网络连接状态。</td>
</tr>
</table>


   **接口函数**

<table>
<tr>
<td rowspan="1" colSpan="1" >**函数列表**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[markConversationUnread](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#markConversationUnread)</td>

<td rowspan="1" colSpan="1" >标记会话未读。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setActiveConversation](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setActiveConversation)</td>

<td rowspan="1" colSpan="1" >设置活跃会话。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[pinConversation](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#pinConversation)</td>

<td rowspan="1" colSpan="1" >置顶会话。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteConversation](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#deleteConversation)</td>

<td rowspan="1" colSpan="1" >删除会话。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[muteConversation](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#muteConversation)</td>

<td rowspan="1" colSpan="1" >静音会话。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setConversationDraft](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setConversationDraft)</td>

<td rowspan="1" colSpan="1" >设置会话草稿。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createC2CConversation](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#createC2CConversation)</td>

<td rowspan="1" colSpan="1" >创建单聊会话。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createGroupConversation](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#createGroupConversation)</td>

<td rowspan="1" colSpan="1" >创建群聊会话。</td>
</tr>
</table>


## ContactListState

联系人管理模块
- 核心功能：管理用户的联系人列表，包括好友管理、群组管理、黑名单管理等完整的联系人功能。

- 技术特点：支持联系人分组、好友申请处理、群组申请管理等功能。新增 friendList、groupList、blackList 等响应式数据和完整的联系人操作接口。

- 业务价值：为用户提供完整的社交关系管理能力，构建社交网络。

- 应用场景：好友管理、群组管理、联系人搜索、社交网络等场景。


   **响应式数据**

<table>
<tr>
<td rowspan="1" colSpan="1" >**数据列表**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[friendList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#friendList)</td>

<td rowspan="1" colSpan="1" >好友列表。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[groupList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#groupList)</td>

<td rowspan="1" colSpan="1" >群组列表。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[blackList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#blackList)</td>

<td rowspan="1" colSpan="1" >黑名单列表。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[friendApplicationUnreadCount](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#friendApplicationUnreadCount)</td>

<td rowspan="1" colSpan="1" >好友申请未读数。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[friendGroupList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#friendGroupList)</td>

<td rowspan="1" colSpan="1" >好友分组列表。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[friendApplicationList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#friendApplicationList)</td>

<td rowspan="1" colSpan="1" >好友申请列表。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[groupApplicationList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#groupApplicationList)</td>

<td rowspan="1" colSpan="1" >群申请列表。</td>
</tr>
</table>


   **接口函数**

<table>
<tr>
<td rowspan="1" colSpan="1" >**函数列表**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGroupApplicationList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setGroupApplicationList)</td>

<td rowspan="1" colSpan="1" >设置群组申请列表。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setFriendList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setFriendList)</td>

<td rowspan="1" colSpan="1" >设置好友列表。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGroupList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setGroupList)</td>

<td rowspan="1" colSpan="1" >设置群组列表。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setBlackList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setBlackList)</td>

<td rowspan="1" colSpan="1" >设置黑名单列表。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setFriendApplicationUnreadCount](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setFriendApplicationUnreadCount)</td>

<td rowspan="1" colSpan="1" >设置好友申请未读数。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setFriendGroupList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setFriendGroupList)</td>

<td rowspan="1" colSpan="1" >设置好友分组列表。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setFriendApplicationList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setFriendApplicationList)</td>

<td rowspan="1" colSpan="1" >设置好友申请列表。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[initContactListWatcher](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#initContactListWatcher)</td>

<td rowspan="1" colSpan="1" >初始化联系人监听器。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addFriend](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#addFriend)</td>

<td rowspan="1" colSpan="1" >添加好友。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[markFriendApplicationAsRead](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#markFriendApplicationAsRead)</td>

<td rowspan="1" colSpan="1" >标记好友申请为已读。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[acceptFriendApplication](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#acceptFriendApplication)</td>

<td rowspan="1" colSpan="1" >接受好友申请。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[refuseFriendApplication](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#refuseFriendApplication)</td>

<td rowspan="1" colSpan="1" >拒绝好友申请。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addToBlacklist](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#addToBlacklist)</td>

<td rowspan="1" colSpan="1" >添加到黑名单。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeFromBlacklist](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#removeFromBlacklist)</td>

<td rowspan="1" colSpan="1" >从黑名单移除。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteFriend](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#deleteFriend)</td>

<td rowspan="1" colSpan="1" >删除好友。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setFriendRemark](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setFriendRemark)</td>

<td rowspan="1" colSpan="1" >设置好友备注。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createFriendGroup](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#createFriendGroup)</td>

<td rowspan="1" colSpan="1" >创建好友分组。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteFriendGroup](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#deleteFriendGroup)</td>

<td rowspan="1" colSpan="1" >删除好友分组。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addToFriendGroup](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#addToFriendGroup)</td>

<td rowspan="1" colSpan="1" >添加到好友分组。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeFromFriendGroup](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#removeFromFriendGroup)</td>

<td rowspan="1" colSpan="1" >从好友分组移除。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[renameFriendGroup](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#renameFriendGroup)</td>

<td rowspan="1" colSpan="1" >重命名好友分组。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[joinGroup](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#joinGroup)</td>

<td rowspan="1" colSpan="1" >加入群组。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[acceptGroupApplication](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#acceptGroupApplication)</td>

<td rowspan="1" colSpan="1" >接受群组申请。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[refuseGroupApplication](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#refuseGroupApplication)</td>

<td rowspan="1" colSpan="1" >拒绝群组申请。</td>
</tr>
</table>


## C2CSettingState

单聊设置管理模块
- 核心功能：管理单聊会话的各种设置，包括用户信息、聊天设置、权限控制等功能。

- 技术特点：支持实时设置同步、权限管理、个性化配置等功能。更新响应式数据为 userID、avatar、signature 等标准化字段。

- 业务价值：为用户提供个性化的单聊体验，提升沟通质量。

- 应用场景：单聊设置、用户信息管理、聊天权限控制等场景。


   **响应式数据**

<table>
<tr>
<td rowspan="1" colSpan="1" >**数据列表**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[currentConversationRef](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#currentConversationRef)</td>

<td rowspan="1" colSpan="1" >当前会话引用。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[userIDRef](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#userIDRef)</td>

<td rowspan="1" colSpan="1" >用户 ID。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[nickRef](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#nickRef)</td>

<td rowspan="1" colSpan="1" >用户昵称。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[avatarRef](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#avatarRef)</td>

<td rowspan="1" colSpan="1" >用户头像。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[signatureRef](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#signatureRef)</td>

<td rowspan="1" colSpan="1" >用户个性签名。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[remarkRef](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#remarkRef)</td>

<td rowspan="1" colSpan="1" >好友备注名。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[isMutedRef](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isMutedRef)</td>

<td rowspan="1" colSpan="1" >会话静音状态。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[isPinnedRef](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isPinnedRef)</td>

<td rowspan="1" colSpan="1" >会话置顶状态。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[isContactRef](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isContactRef)</td>

<td rowspan="1" colSpan="1" >好友关系状态。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[userID](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#userID)</td>

<td rowspan="1" colSpan="1" >用户 ID。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[avatar](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#avatar)</td>

<td rowspan="1" colSpan="1" >用户头像 URL。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[signature](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#signature)</td>

<td rowspan="1" colSpan="1" >用户个性签名。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[remark](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#remark)</td>

<td rowspan="1" colSpan="1" >用户备注名。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[isMuted](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isMuted)</td>

<td rowspan="1" colSpan="1" >是否已静音。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[isPinned](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isPinned)</td>

<td rowspan="1" colSpan="1" >是否已置顶。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[isContact](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isContact)</td>

<td rowspan="1" colSpan="1" >是否为联系人。</td>
</tr>
</table>


   **接口函数**

<table>
<tr>
<td rowspan="1" colSpan="1" >**函数列表**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setChatPinned](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setChatPinned)</td>

<td rowspan="1" colSpan="1" >设置聊天置顶。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setChatMuted](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setChatMuted)</td>

<td rowspan="1" colSpan="1" >设置聊天免打扰。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setUserRemark](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setUserRemark)</td>

<td rowspan="1" colSpan="1" >设置用户备注。</td>
</tr>
</table>


## GroupSettingState

群聊设置管理模块
- 核心功能：管理群聊的各种设置和操作，包括群信息管理、成员管理、权限控制等完整的群管理功能。

- 技术特点：支持群权限管理、成员操作、群设置同步等功能。新增 groupID、groupType、groupName 等完整的群信息响应式数据和管理接口。

- 业务价值：为群主和管理员提供完整的群管理能力，维护群秩序。

- 应用场景：群管理、成员管理、权限控制、群设置等场景。


   **响应式数据**

<table>
<tr>
<td rowspan="1" colSpan="1" >**数据列表**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[groupID](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#groupID)</td>

<td rowspan="1" colSpan="1" >群组 ID。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[groupType](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#groupType)</td>

<td rowspan="1" colSpan="1" >群组类型。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[groupName](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#groupName)</td>

<td rowspan="1" colSpan="1" >群组名称。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[avatar](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#avatar)</td>

<td rowspan="1" colSpan="1" >用户头像 URL。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[introduction](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#introduction)</td>

<td rowspan="1" colSpan="1" >群组介绍。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[notification](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#notification)</td>

<td rowspan="1" colSpan="1" >群组公告。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[isMuted](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isMuted)</td>

<td rowspan="1" colSpan="1" >是否已静音。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[isPinned](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isPinned)</td>

<td rowspan="1" colSpan="1" >是否已置顶。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[groupOwner](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#groupOwner)</td>

<td rowspan="1" colSpan="1" >群主信息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[adminMembers](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#adminMembers)</td>

<td rowspan="1" colSpan="1" >管理员列表。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[allMembers](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#allMembers)</td>

<td rowspan="1" colSpan="1" >所有成员列表。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[memberCount](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#memberCount)</td>

<td rowspan="1" colSpan="1" >成员总数。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[maxMemberCount](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#maxMemberCount)</td>

<td rowspan="1" colSpan="1" >最大成员数。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[currentUserID](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#currentUserID)</td>

<td rowspan="1" colSpan="1" >当前用户 ID。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[currentUserRole](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#currentUserRole)</td>

<td rowspan="1" colSpan="1" >当前用户角色。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[nameCard](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#nameCard)</td>

<td rowspan="1" colSpan="1" >用户名片。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[isMuteAllMembers](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isMuteAllMembers)</td>

<td rowspan="1" colSpan="1" >是否禁言所有成员。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[isInGroup](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isInGroup)</td>

<td rowspan="1" colSpan="1" >是否在群组中。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[inviteOption](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#inviteOption)</td>

<td rowspan="1" colSpan="1" >邀请选项。</td>
</tr>
</table>


   **接口函数**

<table>
<tr>
<td rowspan="1" colSpan="1" >**函数列表**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupMemberList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getGroupMemberList)</td>

<td rowspan="1" colSpan="1" >获取群成员列表。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[updateGroupProfile](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#updateGroupProfile)</td>

<td rowspan="1" colSpan="1" >更新群资料。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addGroupMember](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#addGroupMember)</td>

<td rowspan="1" colSpan="1" >添加群成员。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteGroupMember](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#deleteGroupMember)</td>

<td rowspan="1" colSpan="1" >删除群成员。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[changeGroupOwner](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#changeGroupOwner)</td>

<td rowspan="1" colSpan="1" >转让群主。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGroupMemberRole](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setGroupMemberRole)</td>

<td rowspan="1" colSpan="1" >设置群成员角色。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGroupMemberNameCard](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setGroupMemberNameCard)</td>

<td rowspan="1" colSpan="1" >设置群成员名片。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setChatPinned](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setChatPinned)</td>

<td rowspan="1" colSpan="1" >设置聊天置顶。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setChatMuted](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setChatMuted)</td>

<td rowspan="1" colSpan="1" >设置聊天免打扰。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGroupMemberMuteTime](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setGroupMemberMuteTime)</td>

<td rowspan="1" colSpan="1" >设置群成员禁言。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setMuteAllMember](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setMuteAllMember)</td>

<td rowspan="1" colSpan="1" >设置全员禁言。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[dismissGroup](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#dismissGroup)</td>

<td rowspan="1" colSpan="1" >解散群组。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[quitGroup](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#quitGroup)</td>

<td rowspan="1" colSpan="1" >退出群组。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[hasPermission](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#hasPermission)</td>

<td rowspan="1" colSpan="1" >检查权限。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[canOperateOnMember](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#canOperateOnMember)</td>

<td rowspan="1" colSpan="1" >检查成员操作权限。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getAvailablePermissions](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getAvailablePermissions)</td>

<td rowspan="1" colSpan="1" >获取可用权限。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[initWatcher](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#initWatcher)</td>

<td rowspan="1" colSpan="1" >初始化监听器。</td>
</tr>
</table>


## VideoMixerState

视频混流管理模块
- 核心功能：管理视频混流功能，支持多路视频合成、布局管理、媒体源控制等高级视频处理功能。

- 技术特点：支持实时视频混流、动态布局调整、媒体源管理等功能。新增 isVideoMixerEnabled、mediaSourceList、activeMediaSource 响应式数据和完整的混流控制接口。

- 业务价值：为直播平台提供专业的视频制作能力，提升直播质量。

- 应用场景：多人直播、画中画、视频合成、专业制作等场景。


   **响应式数据**

<table>
<tr>
<td rowspan="1" colSpan="1" >**数据列表**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[publishVideoQuality](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#publishVideoQuality)</td>

<td rowspan="1" colSpan="1" >根据分辨率获取尺寸。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[isVideoMixerEnabled](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isVideoMixerEnabled)</td>

<td rowspan="1" colSpan="1" >视频混流是否启用。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[mediaSourceList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#mediaSourceList)</td>

<td rowspan="1" colSpan="1" >媒体源列表。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[activeMediaSource](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#activeMediaSource)</td>

<td rowspan="1" colSpan="1" >当前活跃的媒体源。</td>
</tr>
</table>


   **接口函数**

<table>
<tr>
<td rowspan="1" colSpan="1" >**函数列表**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getVideoDataByQuality](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getVideoDataByQuality)</td>

<td rowspan="1" colSpan="1" >根据质量获取视频数据。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getSizeByQuality](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getSizeByQuality)</td>

<td rowspan="1" colSpan="1" >根据质量获取尺寸。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getSizeByResolution](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getSizeByResolution)</td>

<td rowspan="1" colSpan="1" >根据分辨率获取尺寸。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[transformTUIVideoQualityToTRTCVideoResolution](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#transformTUIVideoQualityToTRTCVideoResolution)</td>

<td rowspan="1" colSpan="1" >转换视频质量到 TRTC 分辨率。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[transformTRTCVideoResolutionToTUIVideoQuality](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#transformTRTCVideoResolutionToTUIVideoQuality)</td>

<td rowspan="1" colSpan="1" >转换 TRTC 分辨率到视频质量。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[transformTRTCVideoResModeToTUIVideoResMode](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#transformTRTCVideoResModeToTUIVideoResMode)</td>

<td rowspan="1" colSpan="1" >转换 TRTC 分辨率模式。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[changeActiveMediaSource](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#changeActiveMediaSource)</td>

<td rowspan="1" colSpan="1" >切换活跃媒体源。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[updateVideoQuality](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#updateVideoQuality)</td>

<td rowspan="1" colSpan="1" >更新视频质量。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getDefaultLayoutByMediaSource](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getDefaultLayoutByMediaSource)</td>

<td rowspan="1" colSpan="1" >根据媒体源获取默认布局。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addMediaSource](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#addMediaSource)</td>

<td rowspan="1" colSpan="1" >添加媒体源。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[updateMediaSource](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#updateMediaSource)</td>

<td rowspan="1" colSpan="1" >更新媒体源。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeMediaSource](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#removeMediaSource)</td>

<td rowspan="1" colSpan="1" >移除媒体源。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[enableLocalVideoMixer](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#enableLocalVideoMixer)</td>

<td rowspan="1" colSpan="1" >启用本地视频混流。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[clearMediaSource](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#clearMediaSource)</td>

<td rowspan="1" colSpan="1" >清空所有媒体源。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[initMediaSourceManager](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#initMediaSourceManager)</td>

<td rowspan="1" colSpan="1" >初始化媒体源管理器。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[initVideoMixerState](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#initVideoMixerState)</td>

<td rowspan="1" colSpan="1" >初始化视频混流状态。</td>
</tr>
</table>


## VirtualBackgroundState

虚拟背景管理模块
- 核心功能：管理虚拟背景功能，支持背景替换、背景模糊、自定义背景等视频美化功能。

- 技术特点：基于 AI 技术实现实时背景分割和替换。新增 virtualBackgroundConfig 响应式数据和 isSupported、setVirtualBackground 接口函数。

- 业务价值：为用户提供隐私保护和视频美化功能，提升视频通话体验。

- 应用场景：视频通话、在线会议、直播美化、隐私保护等场景。


   **响应式数据**

<table>
<tr>
<td rowspan="1" colSpan="1" >**数据列表**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[virtualBackgroundConfig](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#virtualBackgroundConfig)</td>

<td rowspan="1" colSpan="1" >虚拟背景配置。</td>
</tr>
</table>


   **接口函数**

<table>
<tr>
<td rowspan="1" colSpan="1" >**函数列表**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[initVirtualBackground](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#initVirtualBackground)</td>

<td rowspan="1" colSpan="1" >初始化虚拟背景。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[saveVirtualBackground](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#saveVirtualBackground)</td>

<td rowspan="1" colSpan="1" >保存虚拟背景。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[isSupported](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isSupported)</td>

<td rowspan="1" colSpan="1" >检查是否支持。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setVirtualBackground](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setVirtualBackground)</td>

<td rowspan="1" colSpan="1" >设置虚拟背景。</td>
</tr>
</table>


## ASRState

语音识别管理模块
- 核心功能：管理语音识别功能，支持实时语音转文字、转录历史管理、转录导出等功能。

- 技术特点：基于先进的 ASR 技术，支持多语言识别、实时转录、历史记录等功能。新增 recentTranscripts、transcriptHistory 响应式数据和 exportTranscripts 接口。

- 业务价值：为用户提供语音转文字服务，提升沟通效率和可访问性。

- 应用场景：会议记录、语音转录、无障碍通信、内容记录等场景。


   **响应式数据**

<table>
<tr>
<td rowspan="1" colSpan="1" >**数据列表**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[recentTranscripts](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#recentTranscripts)</td>

<td rowspan="1" colSpan="1" >最近的语音转录记录。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[transcriptHistory](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#transcriptHistory)</td>

<td rowspan="1" colSpan="1" >语音转录历史记录。</td>
</tr>
</table>


   **接口函数**

<table>
<tr>
<td rowspan="1" colSpan="1" >**函数列表**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setRecentTranscriptsDuration](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setRecentTranscriptsDuration)</td>

<td rowspan="1" colSpan="1" >设置最近转录时长。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[clearHistory](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#clearHistory)</td>

<td rowspan="1" colSpan="1" >清空转录历史记录。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[exportTranscripts](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#exportTranscripts)</td>

<td rowspan="1" colSpan="1" >导出转录内容。</td>
</tr>
</table>


## SearchState

搜索功能管理模块
- 核心功能：管理全局搜索功能，支持消息搜索、用户搜索、群组搜索等多维度搜索能力。

- 技术特点：支持高级搜索、搜索历史、搜索建议等功能。重构响应式数据为 keyword、results、isLoading 等标准化字段，提供完整的搜索接口。

- 业务价值：为用户提供快速查找信息的能力，提升使用效率。

- 应用场景：消息搜索、联系人搜索、内容查找、历史记录等场景。


   **响应式数据**

<table>
<tr>
<td rowspan="1" colSpan="1" >**数据列表**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[keyword](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#keyword)</td>

<td rowspan="1" colSpan="1" >搜索关键词。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[results](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#results)</td>

<td rowspan="1" colSpan="1" >搜索结果。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[isLoading](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#isLoading)</td>

<td rowspan="1" colSpan="1" >是否正在加载。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[error](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#error)</td>

<td rowspan="1" colSpan="1" >错误信息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[searchAdvancedParams](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#searchAdvancedParams)</td>

<td rowspan="1" colSpan="1" >高级搜索参数。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[selectedSearchType](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#selectedSearchType)</td>

<td rowspan="1" colSpan="1" >选中的搜索类型。</td>
</tr>
</table>


   **接口函数**

<table>
<tr>
<td rowspan="1" colSpan="1" >**函数列表**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[search](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#search)</td>

<td rowspan="1" colSpan="1" >搜索。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setKeyword](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setKeyword)</td>

<td rowspan="1" colSpan="1" >设置关键词。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setSelectedType](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setSelectedType)</td>

<td rowspan="1" colSpan="1" >设置选中类型。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setSearchMessageAdvancedParams](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setSearchMessageAdvancedParams)</td>

<td rowspan="1" colSpan="1" >设置消息搜索高级参数。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setSearchUserAdvancedParams](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setSearchUserAdvancedParams)</td>

<td rowspan="1" colSpan="1" >设置用户搜索高级参数。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setSearchGroupAdvancedParams](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setSearchGroupAdvancedParams)</td>

<td rowspan="1" colSpan="1" >设置群组搜索高级参数。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[loadMore](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#loadMore)</td>

<td rowspan="1" colSpan="1" >加载更多。</td>
</tr>
</table>


## SeatStore

座位存储管理模块
- 核心功能：提供座位状态的底层存储和管理，支持座位信息缓存、用户信息映射、设备请求处理等核心功能。

- 技术特点：采用响应式存储设计，支持实时状态同步、事件驱动更新等功能。新增 liveOwnerUserId、localUserId、seatList 等响应式数据和 getUserInfo、convertUserInfoToAudienceInfo 接口。

- 业务价值：为座位管理提供可靠的数据基础，确保座位状态的一致性。

- 应用场景：座位状态管理、用户信息存储、设备状态跟踪等底层场景。


   **响应式数据**

<table>
<tr>
<td rowspan="1" colSpan="1" >**数据列表**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[liveOwnerUserId](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#liveOwnerUserId)</td>

<td rowspan="1" colSpan="1" >直播间主播用户 ID。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[localUserId](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#localUserId)</td>

<td rowspan="1" colSpan="1" >本地用户 ID。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[seatList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#seatList)</td>

<td rowspan="1" colSpan="1" >麦位列表，包含所有麦位的状态和用户信息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[coHostUserList](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#coHostUserList)</td>

<td rowspan="1" colSpan="1" >连麦主播列表。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[sentDeviceRequestMap](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#sentDeviceRequestMap)</td>

<td rowspan="1" colSpan="1" >已发送的设备请求映射。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[receivedDeviceRequestMap](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#receivedDeviceRequestMap)</td>

<td rowspan="1" colSpan="1" >已接收的设备请求映射。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[userInfoMap](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#userInfoMap)</td>

<td rowspan="1" colSpan="1" >用户信息映射表。</td>
</tr>
</table>


   **接口函数**

<table>
<tr>
<td rowspan="1" colSpan="1" >函数列表</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getUserInfo](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#getUserInfo)</td>

<td rowspan="1" colSpan="1" >获取用户信息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[convertUserInfoToAudienceInfo](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#convertUserInfoToAudienceInfo)</td>

<td rowspan="1" colSpan="1" >转换用户信息为观众信息。</td>
</tr>
</table>






