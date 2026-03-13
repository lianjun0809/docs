> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

# TRTC Real-Time Communication (TRTC SDK) Documentation
## Overview
`TRTCTypeDef.h` provides type definitions for TRTC Real-Time Communication (TRTC SDK) on C++.

## Struct Type
| Function List | Description |
| --- | --- |
| TRTCParams | Room entry parameters |
| TRTCVideoEncParam | Video encoding parameters |
| TRTCNetworkQosParam | Network flow control (Qos) parameter set |
| TRTCRenderParams | Rendering parameters for video footage |
| TRTCQualityInfo | Network quality |
| TRTCVolumeInfo | Volume level |
| TRTCSpeedTestParams | Speed test parameters |
| TRTCSpeedTestResult | Network speed test results |
| TRTCTexture | Video texture data |
| TRTCVideoFrame | Video frame information |
| TRTCAudioFrame | Audio frame data |
| TRTCMixUser | Description information of each screen in Cloud Mixed Streaming |
| TRTCTranscodingConfig | Layout and Transcoding Parameters of Cloud Mixed Streaming |
| TRTCPublishCDNParam | The relay parameters to be set when publishing audio and video streams to non-Tencent Cloud CDN |
| TRTCAudioRecordingParams | Local audio file recording parameters |
| TRTCLocalRecordingParams | Local media file recording parameters |
| TRTCAudioEffectParam | Audio Effect Parameters (Deprecated) |
| TRTCSwitchRoomConfig | Room switching parameters |
| TRTCAudioFrameCallbackFormat | Audio self Definition callback format parameters |
| TRTCImageBuffer | TRTC screen sharing icon information and mute image spacer |
| TRTCScreenCaptureSourceInfo | Target information for screen sharing (only applicable to desktop systems) |
| TRTCScreenCaptureProperty | Advanced control parameters for screen sharing |
| TRTCAudioParallelParams | Parameters of the intelligent concurrent playback strategy for remote audio streams |
| TRTCUser | User information related to media stream publishing settings |
| TRTCPublishCdnUrl | URL configuration required when publishing audio and video streams to Tencent or third-party CDNs |
| TRTCPublishTarget | Target Streaming Configuration |
| TRTCVideoLayout | Transcoding Video Layout |
| TRTCWatermark | Watermark Layout |
| TRTCStreamEncoderParam | Media Stream Encoding Output Parameters |
| TRTCStreamMixingConfig | Media Stream Transcoding Configuration Parameters |
| TRTCPayloadPrivateEncryptionConfig | Private media stream encryption configuration |
| TRTCAudioVolumeEvaluateParams | Volume assessment and related parameter settings |

## Enumeration Types
| Enumeration Types | Description |
| --- | --- |
| TRTCVideoResolution | Video Resolution |
| TRTCVideoResolutionMode | Video aspect ratio mode |
| TRTCVideoStreamType | Video stream type |
| TRTCVideoFillMode | Video fill mode |
| TRTCVideoRotation | Video rotation direction |
| TRTCBeautyStyle | Beauty Filter (Skin Smoothing) algorithm |
| TRTCVideoPixelFormat | Video pixel format |
| TRTCVideoBufferType | Video data transfer method |
| TRTCVideoMirrorType | Video mirroring type |
| TRTCSnapshotSourceType | Data source for local video screenshot |
| TRTCAppScene | Use Cases |
| TRTCRoleType | Roles |
| TRTCQosControlMode | Traffic control mode (deprecated) |
| TRTCVideoQosPreference | Image quality preference |
| TRTCQuality | Network quality |
| TRTCAVStatusType | Audio/Video status type |
| TRTCAVStatusChangeReason | Audio/Video status change reason type |
| TRTCAudioQuality | Sound quality |
| TRTCAudioFrameFormat | Content format of audio frame |
| TRTCAudioFrameOperationMode | Audio Callback Data Read/Write Mode |
| TRTCLogLevel | Log Level |
| TRTCScreenCaptureSourceType | Target Type for Screen Sharing (Only applicable to desktop devices) |
| TRTCTranscodingConfigMode | Layout Mode for Cloud Mixed Streaming |
| TRTCLocalRecordType | Media Recording Type |
| TRTCMixInputType | Mixed Streaming Input Type |
| TRTCWaterMarkSrcType | Watermark image source type |
| TRTCAudioRecordingContent | Audio Recording Content Type |
| TRTCPublishMode | Media Stream Publication Mode |
| TRTCEncryptionAlgorithm | Encryption Algorithm |
| TRTCSpeedTestScene | Speed Test Scenario |
| TRTCGravitySensorAdaptiveMode | Set Adaptation Mode for Gravity Sensor (Only applicable to mobile devices) |

## TRTCVideoResolution

#### Video Resolution

Only Definition is in landscape resolution (e.g., 640 × 360). To use portrait resolution (e.g., 360 × 640), you also need to set TRTCVideoResolutionMode to Portrait.
| Enumeration | Value | Description |
| --- | --- | --- |
| TRTCVideoResolution_120_120 | 1 | Aspect Ratio 1:1; Resolution 120x120; Suggested Bitrate (VideoCall) 80kbps; Suggested Bitrate (LIVE) 120kbps. |
| TRTCVideoResolution_160_160 | 3 | Aspect Ratio 1:1; Resolution 160x160; Suggested Bitrate (VideoCall) 100kbps; Suggested Bitrate (LIVE) 150kbps. |
| TRTCVideoResolution_270_270 | 5 | Aspect Ratio 1:1; Resolution 270x270; Suggested Bitrate (VideoCall) 200kbps; Suggested Bitrate (LIVE) 300kbps. |
| TRTCVideoResolution_480_480 | 7 | Aspect Ratio 1:1; Resolution 480x480; Suggested Bitrate (VideoCall) 350kbps; Suggested Bitrate (LIVE) 500kbps. |
| TRTCVideoResolution_160_120 | 50 | Aspect Ratio 4:3; Resolution 160x120; Suggested Bitrate (VideoCall) 100kbps; Suggested Bitrate (LIVE) 150kbps. |
| TRTCVideoResolution_240_180 | 52 | Aspect Ratio 4:3; Resolution 240x180; Suggested Bitrate (VideoCall) 150kbps; Suggested Bitrate (LIVE) 250kbps. |
| TRTCVideoResolution_280_210 | 54 | Aspect Ratio 4:3; Resolution 280x210; Suggested Bitrate (VideoCall) 200kbps; Suggested Bitrate (LIVE) 300kbps. |
| TRTCVideoResolution_320_240 | 56 | Aspect Ratio 4:3; Resolution 320x240; Suggested Bitrate (VideoCall) 250kbps; Suggested Bitrate (LIVE) 375kbps. |
| TRTCVideoResolution_400_300 | 58 | Aspect Ratio 4:3; Resolution 400x300; Suggested Bitrate (VideoCall) 300kbps; Suggested Bitrate (LIVE) 450kbps. |
| TRTCVideoResolution_480_360 | 60 | Aspect Ratio 4:3; Resolution 480x360; Suggested Bitrate (VideoCall) 400kbps; Suggested Bitrate (LIVE) 600kbps. |
| TRTCVideoResolution_640_480 | 62 | Aspect Ratio 4:3; Resolution 640x480; Suggested Bitrate (VideoCall) 600kbps; Suggested Bitrate (LIVE) 900kbps. |
| TRTCVideoResolution_960_720 | 64 | Aspect Ratio 4:3; Resolution 960x720; Suggested Bitrate (VideoCall) 1000kbps; Suggested Bitrate (LIVE) 1500kbps. |
| TRTCVideoResolution_160_90 | 100 | Aspect Ratio 16:9; Resolution 160x90; Suggested Bitrate (VideoCall) 150kbps; Suggested Bitrate (LIVE) 250kbps. |
| TRTCVideoResolution_256_144 | 102 | Aspect Ratio 16:9; Resolution 256x144; Suggested Bitrate (VideoCall) 200kbps; Suggested Bitrate (LIVE) 300kbps. |
| TRTCVideoResolution_320_180 | 104 | Aspect Ratio 16:9; Resolution 320x180; Suggested Bitrate (VideoCall) 250kbps; Suggested Bitrate (LIVE) 400kbps. |
| TRTCVideoResolution_480_270 | 106 | Aspect Ratio 16:9; Resolution 480x270; Suggested Bitrate (VideoCall) 350kbps; Suggested Bitrate (LIVE) 550kbps. |
| TRTCVideoResolution_640_360 | 108 | Aspect Ratio 16:9; Resolution 640x360; Suggested Bitrate (VideoCall) 500kbps; Suggested Bitrate (LIVE) 900kbps. |
| TRTCVideoResolution_960_540 | 110 | Aspect Ratio 16:9; Resolution 960x540; Suggested Bitrate (VideoCall) 850kbps; Suggested Bitrate (LIVE) 1300kbps. |
| TRTCVideoResolution_1280_720 | 112 | Aspect Ratio 16:9; Resolution 1280x720; Suggested Bitrate (VideoCall) 1200kbps; Suggested Bitrate (LIVE) 1800kbps. |
| TRTCVideoResolution_1920_1080 | 114 | Aspect Ratio 16:9; Resolution 1920x1080; Suggested Bitrate (VideoCall) 2000kbps; Suggested Bitrate (LIVE) 3000kbps. |

## TRTCVideoResolutionMode

#### Video aspect ratio mode

In TRTCVideoResolution, only landscape resolution (e.g., 640 × 360) is defined. To use portrait resolution (e.g., 360 × 640), you also need to set TRTCVideoResolutionMode to Portrait.
| Enumeration | Value | Description |
| --- | --- | --- |
| TRTCVideoResolutionModeLandscape | 0 | Landscape resolution, e.g., TRTCVideoResolution_640_360 + TRTCVideoResolutionModeLandscape = 640 × 360. |
| TRTCVideoResolutionModePortrait | 1 | Portrait resolution, e.g., TRTCVideoResolution_640_360 + TRTCVideoResolutionModePortrait = 360 × 640. |

## TRTCVideoStreamType

#### Video stream type

There are three different video streams in TRTC:
-  HD large screen: Generally used for transmitting video data from the camera.

-  Low-definition small picture: The content of the small picture is the same as the large picture, but the resolution and bitrate are lower than those of the large picture, resulting in lower clarity.

-  Auxiliary stream picture: Generally used for screen sharing. Only one user can publish auxiliary stream video in the same room at the same time. Other users must wait until the current user stops before they can publish their own auxiliary stream.

> **Note**
> 

> Low-definition small picture cannot be enabled independently. The small picture must rely on the large picture, and the SDK will automatically set the resolution and bitrate of the low-definition small picture.
> 

| Enumeration | Value | Description |
| --- | --- | --- |
| TRTCVideoStreamTypeBig | 0 | HD large screen: Generally used for transmitting video data from the camera. |
| TRTCVideoStreamTypeSmall | 1 | Low-definition small picture: The content of the small picture is the same as the large picture, but the resolution and bitrate are lower than those of the large picture, resulting in lower clarity. |
| TRTCVideoStreamTypeSub | 2 | Auxiliary stream picture: Generally used for screen sharing. Only one user can publish auxiliary stream video in the same room at the same time. Other users must wait until the current user stops before they can publish their own auxiliary stream. |

## TRTCVideoFillMode

#### Video fill mode

When the aspect ratio of the video display area is not equal to the aspect ratio of the video content, you need to specify the fill mode.
| Enumeration | Value | Description |
| --- | --- | --- |
| TRTCVideoFillMode_Fill | 0 | Fill mode: The content is scaled to fill the entire display area while maintaining the aspect ratio. The parts that exceed the display area will be cropped, so the image may be incomplete. |
| TRTCVideoFillMode_Fit | 1 | Adaptive mode: The image is scaled according to the long side to fit the display area. The short sides will be filled with black bars, so the image will be complete but may have black bars. |

## TRTCVideoRotation

#### Video rotation direction

TRTC provides APIs for setting the rotation angle of local and remote video. The angles listed below are in a clockwise direction.
| Enumeration | Value | Description |
| --- | --- | --- |
| TRTCVideoRotation0 | 0 | No rotation. |
| TRTCVideoRotation90 | 1 | Rotate clockwise by 90 degrees. |
| TRTCVideoRotation180 | 2 | Rotate clockwise by 180 degrees. |
| TRTCVideoRotation270 | 3 | Rotate clockwise by 270 degrees. |

## TRTCBeautyStyle

#### Beauty Filter (Skin Smoothing) algorithm

TRTC offers various skin smoothing algorithms. You can choose the one that best fits your product positioning.
| Enumeration | Value | Description |
| --- | --- | --- |
| TRTCBeautyStyleSmooth | 0 | Smooth: This aggressive algorithm results in a more pronounced skin smoothing effect, suitable for show live streaming. |
| TRTCBeautyStyleNature | 1 | Natural: This algorithm retains more facial details, resulting in a more natural smoothing effect, suitable for most live streaming scenarios. |

## TRTCVideoPixelFormat

#### Video pixel format

TRTC provides custom data collection and custom rendering features for video:
-  In the custom data collection feature, you can use the following enumeration values to describe the pixel format of your captured video.

-  In the custom rendering feature, you can specify the pixel format you expect the SDK to call back.

| Enumeration | Value | Description |
| --- | --- | --- |
| TRTCVideoPixelFormat_Unknown | 0 | Undefined format. |
| TRTCVideoPixelFormat_I420 | 1 | YUV420P (I420) format. |
| TRTCVideoPixelFormat_Texture_2D | 2 | OpenGL 2D texture format. |
| TRTCVideoPixelFormat_BGRA32 | 3 | BGRA format |
| TRTCVideoPixelFormat_NV21 | 4 | NV21 format. |
| TRTCVideoPixelFormat_RGBA32 | 5 | RGBA format. |

## TRTCVideoBufferType

#### Video data transfer method

In custom data collection and custom rendering features, you need to use the following enumerated values to specify how you want to transmit video data:
-  Option 1: Transmit video data using Memory Buffer. This method is efficient on iOS, but less efficient on Android, and Windows currently only supports Memory Buffer transmission.

-  Option 2: Transmit video data using Texture. This method is highly efficient on both iOS and Android, but not supported on Windows. A certain level of OpenGL programming knowledge is required.

| Enumeration | Value | Description |
| --- | --- | --- |
| TRTCVideoBufferType_Unknown | 0 | Undefined transmission method. |
| TRTCVideoBufferType_Buffer | 1 | Transmit video data using Memory Buffer, iOS: PixelBuffer; Android: Direct Buffer for JNI layer; Win: Memory Data Block. |
| TRTCVideoBufferType_Texture | 3 | Transmit video data using OpenGL texture. |
| TRTCVideoBufferType_TextureD3D11 | 4 | Transmit video data using D3D11 texture. |

## TRTCVideoMirrorType

#### Video mirroring type

Video mirroring refers to flipping the video content horizontally, especially for the local camera preview video. Enabling mirroring can provide the host with a familiar "mirror" experience.
| Enumeration | Value | Description |
| --- | --- | --- |
| TRTCVideoMirrorType_Auto | 0 | Automatic Mode: If using the front-facing camera, enable mirroring; if using the rear-facing camera, disable mirroring (only applicable to mobile devices). |
| TRTCVideoMirrorType_Enable | 1 | Force On mirroring, regardless of whether the current camera is front-facing or rear-facing. |
| TRTCVideoMirrorType_Disable | 2 | Force Off mirroring, regardless of whether the current camera is front-facing or rear-facing. |

## TRTCSnapshotSourceType

#### Data source for local video screenshot

The SDK supports capturing images from the following two data sources and saving them as local files:
-  Video Stream: Capture native video content from the video stream. The captured content is not controlled by the rendering controls.

-  Rendering Layer: Capture the displayed video content from the rendering controls, achieving a What You See Is What You Get (WYSIWYG) effect. However, if the display area is too small, the captured image will also be small.

-  Capture Layer: Capture the video content collected by the capture controls, allowing for the extraction of high-definition screenshots.

| Enumeration | Value | Description |
| --- | --- | --- |
| TRTCSnapshotSourceTypeStream | 0 | Capture native video content from the video stream. The captured content is not controlled by the rendering controls. |
| TRTCSnapshotSourceTypeView | 1 | Capture the displayed video content from the rendering controls, achieving a What You See Is What You Get (WYSIWYG) effect. However, if the display area is too small, the captured image will also be small. |
| TRTCSnapshotSourceTypeCapture | 2 | Capture the video content collected by the capture controls, allowing for the extraction of high-definition screenshots. |

## TRTCAppScene

#### Use Cases

TRTC has optimized for common audio and video application scenarios to meet the differentiated requirements of various vertical scenarios. The main scenarios can be categorized into two types:
-  Live Streaming (LIVE) Scenario: Includes LIVE and VoiceChatRoom. The former is audio + video, while the latter is audio only.

In the live streaming scenario, users are divided into two roles: "Anchors" and "Audience." A single room can support up to 100,000 people online simultaneously, making it suitable for live streaming scenarios with a large audience.
-  Real-Time (RTC) Scenario: Includes VideoCall and AudioCall. The former is audio + video, while the latter is audio only.

In the real-time scenario, there is no role differentiation among users, but a single room can support up to 300 people online simultaneously, making it suitable for small-scale real-time communication.
| Enumeration | Value | Description |
| --- | --- | --- |
| TRTCAppSceneVideoCall | 0 | Video call scenario, supports 720p and 1080p HD quality, each room can have up to 300 concurrent users, with a maximum of 50 users speaking simultaneously. Applicable to [One-to-one video call], [300-person video conference], [Online consultation], [Educational small class], [Remote interview], and other business scenarios. |
| TRTCAppSceneLIVE | 1 | Video interactive live streaming, supports smooth mic switching without waiting, anchor delay less than 300 ms; supports up to 100,000 concurrent viewers, with playback latency as low as 1,000 ms. Applicable to [Low-latency interactive live streaming], [Large class], [Host PK], [Video blind dating], [Online interactive classroom], [Remote training], [Large-scale conferences], and other business scenarios. **Note** In this scenario, you must specify the current user's role through the role field in TRTCParams. |
| TRTCAppSceneAudioCall | 2 | Voice call scenario, default uses SPEECH quality, each room can have up to 300 concurrent users, with a maximum of 50 users speaking simultaneously. Applicable to [One-to-one voice call], [300-person voice conference], [Voice chat], [Voice conference], [Online Werewolf Game], and other business scenarios. |
| TRTCAppSceneVoiceChatRoom | 3 | Voice interactive live streaming, supports smooth mic switching without waiting, anchor delay less than 300 ms; supports up to 100,000 concurrent viewers, with playback latency as low as 1,000 ms. Applicable to [Voice club], [Online KTV room], [Music live broadcast room], [FM radio station], and other business scenarios. **Note** In this scenario, you must specify the current user's role through the role field in TRTCParams. |

## TRTCRoleType

#### Roles

Only applicable to live streaming scenarios (i.e., TRTCAppSceneLIVE and TRTCAppSceneVoiceChatRoom), distinguishing users into two different identities:
-  Anchors: Can publish their own audio and video streams at any time, but the number of anchors is limited. A maximum of 50 anchors can publish their audio and video streams simultaneously in the same room.

-  Audience: Can only watch other users' audio and video streams. To publish audio and video streams, they need to switch their role to anchor using switchRole. A single room can accommodate up to 100,000 audience members.

| Enumeration | Value | Description |
| --- | --- | --- |
| TRTCRoleAnchor | 20 | Anchors: Can publish their own audio and video streams at any time, but the number of anchors is limited. A maximum of 50 anchors can publish their audio and video streams simultaneously in the same room. |
| TRTCRoleAudience | 21 | Audience: Can only watch other users' audio and video streams. To publish audio and video streams, they need to switch their role to anchor using switchRole. A single room can accommodate up to 100,000 audience members. |

## TRTCQosControlMode(Deprecated)

#### Traffic control mode (deprecated)
| Enumeration | Value | Description |
| --- | --- | --- |
| TRTCQosControlModeClient | 0 | Local Control, used for SDK development internal debugging, please do not use for customers. |
| TRTCQosControlModeServer | 1 | Cloud Control, the default mode, is recommended. |

## TRTCVideoQosPreference

#### Image quality preference

TRTC offers two adjustment modes under a weak network environment: "Prioritize Clear Picture" or "Prioritize Smooth Picture". Both modes will primarily ensure audio data transmission.
| Enumeration | Value | Description |
| --- | --- | --- |
| TRTCVideoQosPreferenceSmooth | 1 | Smooth Priority: When the current network is insufficient to transmit both clear and smooth images, it prioritizes the smoothness of the picture, which results in a blurrier image with more mosaics. |
| TRTCVideoQosPreferenceClear | 2 | Clarity Priority (default): When the current network is insufficient to transmit both clear and smooth images, it prioritizes the clarity of the picture, which results in more stuttering. |

## TRTCQuality

#### Network quality

TRTC evaluates the current network quality every two seconds, with six evaluation levels: Excellent indicating the best, and Down indicating the worst.
| Enumeration | Value | Description |
| --- | --- | --- |
| TRTCQuality_Unknown | 0 | Undefined. |
| TRTCQuality_Excellent | 1 | The current network is excellent. |
| TRTCQuality_Good | 2 | The current network is good. |
| TRTCQuality_Poor | 3 | The current network is average. |
| TRTCQuality_Bad | 4 | The current network is poor. |
| TRTCQuality_Vbad | 5 | The current network is very poor. |
| TRTCQuality_Down | 6 | The current network does not meet the minimum requirements of TRTC. |

## TRTCAVStatusType

#### Audio/Video status type

This enumeration type is used for audio status change callback interfaces (onRemoteAudioStatusUpdated) and video status change callback interfaces (onRemoteVideoStatusUpdated) to specify the current audio or video status.
| Enumeration | Value | Description |
| --- | --- | --- |
| TRTCAVStatusStopped | 0 | Stops playback. |
| TRTCAVStatusPlaying | 1 | Playing. |
| TRTCAVStatusLoading | 2 | Loading. |

## TRTCAVStatusChangeReason

#### Audio/Video status change reason type

This enumeration type is used for audio status change callback interfaces (onRemoteAudioStatusUpdated) and video status change callback interfaces (onRemoteVideoStatusUpdated) to specify the reason for the current audio or video status change.
| Enumeration | Value | Description |
| --- | --- | --- |
| TRTCAVStatusChangeReasonInternal | 0 | Default value. |
| TRTCAVStatusChangeReasonBufferingBegin | 1 | Network buffering. |
| TRTCAVStatusChangeReasonBufferingEnd | 2 | End buffering. |
| TRTCAVStatusChangeReasonLocalStarted | 3 | Locally starts playing the audio or video stream. |
| TRTCAVStatusChangeReasonLocalStopped | 4 | Locally stops playing the audio or video stream. |
| TRTCAVStatusChangeReasonRemoteStarted | 5 | Starts (or resumes) the remote audio or video stream. |
| TRTCAVStatusChangeReasonRemoteStopped | 6 | Stops (or interrupts) the remote audio or video stream. |

## TRTCAudioQuality

#### Sound quality

TRTC provides three carefully calibrated modes to meet the diverse pursuit of audio quality in various vertical scenarios:
-  Vocal Mode (Speech): Suitable for applications focused on voice communication. This mode offers strong audio transmission resistance, ensuring optimal smoothness in weak network environments through various voice processing techniques.

-  Music Mode (Music): Suitable for scenarios with high vocal demands. This mode transmits a large amount of audio data, ensuring high-fidelity detail reproduction of music signals across all frequency bands through various technologies.

-  Default Mode (Default): Positioned between Speech and Music, this mode offers better music reproduction than the Vocal Mode but transmits much less data than the Music Mode. It is well-suited for various scenarios.

| Enumeration | Value | Description |
| --- | --- | --- |
| TRTCAudioQualitySpeech | 1 | Vocal Mode: Sampling Rate: 16k; Mono; Encoding Bitrate: 16kbps; Offers the strongest network resistance among the modes, suitable for voice-focused scenarios such as online meetings and voice calls. |
| TRTCAudioQualityDefault | 2 | Default Mode: Sampling Rate: 48k; Mono; Encoding Bitrate: 50kbps; A tier between Speech and Music, the default level of the SDK, recommended. |
| TRTCAudioQualityMusic | 3 | Music Mode: Sampling Rate: 48k; Full-band Stereo; Encoding Bitrate: 128kbps; Suitable for scenarios requiring high-fidelity music transmission, such as online karaoke and music live streaming. |

## TRTCAudioFrameFormat

#### Content format of audio frame
| Enumeration | Value | Description |
| --- | --- | --- |
| TRTCAudioFrameFormatNone | 0 | None |
| TRTCAudioFrameFormatPCM | Not Defined | Audio data in PCM format. |

## TRTCAudioFrameOperationMode

#### Audio Callback Data Read/Write Mode

TRTC provides two operation modes for audio callback data.
-  Read-Write Mode: You can retrieve and modify the callback audio data. This is the default mode.

-  Read-Only Mode: You can only retrieve the audio data from the callback.

| Enumeration | Value | Description |
| --- | --- | --- |
| TRTCAudioFrameOperationModeReadWrite | 0 | Read-Write Mode: You can retrieve and modify the callback audio data. |
| TRTCAudioFrameOperationModeReadOnly | 1 | Read-Only Mode: You can only retrieve the audio data from the callback. |

## TRTCLogLevel

#### Log Level

Different log levels define different levels of detail and log quantities. It is recommended to set the log level to TRTCLogLevelInfo under normal circumstances.
| Enumeration | Value | Description |
| --- | --- | --- |
| TRTCLogLevelVerbose | 0 | Output all levels of logs. |
| TRTCLogLevelDebug | 1 | Output DEBUG, INFO, WARNING, ERROR, and FATAL levels of logs. |
| TRTCLogLevelInfo | 2 | Output INFO, WARNING, ERROR, and FATAL levels of logs. |
| TRTCLogLevelWarn | 3 | Output WARNING, ERROR, and FATAL levels of logs. |
| TRTCLogLevelError | 4 | Output ERROR and FATAL levels of logs. |
| TRTCLogLevelFatal | 5 | Output only FATAL level logs. |
| TRTCLogLevelNone | 6 | Do not output any SDK logs. |

## TRTCScreenCaptureSourceType

#### Target Type for Screen Sharing (Only applicable to desktop devices)
| Enumeration | Value | Description |
| --- | --- | --- |
| TRTCScreenCaptureSourceTypeUnknown | -1 | Undefined. |
| TRTCScreenCaptureSourceTypeWindow | 0 | The share target is a window of an application. |
| TRTCScreenCaptureSourceTypeScreen | 1 | The share target is the screen of a monitor. |
| TRTCScreenCaptureSourceTypeCustom | 2 | This sharing target is a user-defined data source. |

## TRTCTranscodingConfigMode

#### Layout Mode for Cloud Mixed Streaming

TRTC's cloud mixed streaming service can combine multiple audio and video streams in a room into one stream. Therefore, you need to specify a layout plan for the screen. We offer the following layout modes.
| Enumeration | Value | Description |
| --- | --- | --- |
| TRTCTranscodingConfigMode_Unknown | 0 | Undefined. |
| TRTCTranscodingConfigMode_Manual | 1 | Fully Manual Layout Mode. In this mode, you need to specify the exact layout position for each screen. This mode offers the highest degree of freedom but is the least user-friendly: -  You need to fill in all parameters in TRTCTranscodingConfig, including the position coordinates for each screen (TRTCMixUser). -  You need to monitor the onUserVideoAvailable() and onUserAudioAvailable() event callbacks in ITRTCCloudCallback, and continuously adjust the mixUsers parameters based on the audio and video status of users on each mic in the current room. |
| TRTCTranscodingConfigMode_Template_PureAudio | 2 | Pure Audio Mode. This mode is suitable for voice call (AudioCall) and voice chat room (VoiceChatRoom) audio-only applications. -  After entering the room, you only need to set up the mixing configuration once through the setMixTranscodingConfig interface. The SDK will then automatically mix the audio of all on-mic users in the room into the current user's live stream. -  You don't need to set the mixUsers parameters in TRTCTranscodingConfig. Just set the audioSampleRate, audioBitrate, and audioChannels parameters. |
| TRTCTranscodingConfigMode_Template_PresetLayout | 3 | Pre-layout Mode. The most popular layout mode because it supports pre-setting the positions of each screen using placeholders, and then the SDK will automatically adapt and adjust based on the number of screens in the room. In this mode, you still need to set the mixUsers parameters, but you can set the userId to "Placeholder". The available placeholders are: -  "$PLACE_HOLDER_REMOTE$"     :  Represents the remote user's screen. Multiple instances can be set. -  "$PLACE_HOLDER_LOCAL_MAIN$" : Represents the local camera screen. Only one instance is allowed. -  "$PLACE_HOLDER_LOCAL_SUB$"  :  Represents the local screen sharing. Only one instance is allowed. In this mode, you do not need to monitor the onUserVideoAvailable and onUserAudioAvailable callbacks in ITRTCCloudCallback for real-time adjustment. You just need to call setMixTranscodingConfig once after successfully entering the room; thereafter, the SDK will automatically fill the real userId into the placeholders you set. |
| TRTCTranscodingConfigMode_Template_ScreenSharing | 4 | Screen Sharing Mode. Suitable for online education scenarios and other screen sharing-centric applications, this mode is only supported on Windows and Mac SDKs. In this mode, the SDK will first build a canvas based on the target resolution you set via the videoWidth and videoHeight parameters, -  If the teacher does not activate the screen sharing, the SDK will proportionally stretch and draw the teacher's camera feed onto the canvas; -  When the teacher activates screen sharing, the SDK will draw the screen sharing feed onto the same canvas. The purpose of this layout is to ensure that the output resolution of the stream mixing module is consistent, avoiding screen tearing issues during course playback and web viewing (web players do not support variable resolutions). Additionally, the students' audio will be mixed into the teacher's audio and video stream by default. Since video content in teaching mode is primarily screen sharing, simultaneously transmitting the camera feed and the screen sharing feed is very bandwidth-intensive. The recommended approach is to directly render the camera feed onto the current screen via the setLocalVideoRenderCallback interface. In this mode, you don't need to set the mixUsers parameters in TRTCTranscodingConfig. The SDK will not mix the students' screens to prevent interference with the screen sharing effect. You can set the width x height in TRTCTranscodingConfig to 0px × 0px. The SDK will automatically calculate a suitable resolution based on the user's current screen aspect ratio -  If the teacher's current screen width is <= 1920px, the SDK will use the actual resolution of the teacher's current screen. -  If the teacher's current screen width is > 1920px, the SDK will choose one of the three resolutions based on the current screen aspect ratio: 1920x1080 (16:9), 1920x1200 (16:10), or 1920x1440 (4:3). |

## TRTCRecordType

#### Media Recording Type

This enumeration type is used for the local media recording interface startLocalRecording to specify whether to record audio and video files or pure audio files.
| Enumeration | Value | Description |
| --- | --- | --- |
| TRTCLocalRecordType_Audio | 0 | Audio recording only. |
| TRTCLocalRecordType_Video | 1 | Video recording only. |
| TRTCLocalRecordType_Both | 2 | Record both audio and video. |

## TRTCMixInputType

#### Mixed Streaming Input Type
| Enumeration | Value | Description |
| --- | --- | --- |
| TRTCMixInputTypeUndefined | 0 | Default value. Considering compatibility with older versions, if you specify the inputType as Undefined, the SDK will determine the mixed input type based on the value of another parameter, pureAudio. |
| TRTCMixInputTypeAudioVideo | 1 | Mix both audio and video. |
| TRTCMixInputTypePureVideo | 2 | Mix video only. |
| TRTCMixInputTypePureAudio | 3 | Mix audio only. |
| TRTCMixInputTypeWatermark | 4 | Mix watermarks. In this case, you do not need to specify the userId field but need to specify the image field. Using png format images is recommended. |

## TRTCWaterMarkSrcType

#### Watermark image source type
| Enumeration | Value | Description |
| --- | --- | --- |
| TRTCWaterMarkSrcTypeFile | 0 | Image file path, supports BMP, GIF, JPEG, PNG, TIFF, Exif, WMF, and EMF file formats. |
| TRTCWaterMarkSrcTypeBGRA32 | 1 | BGRA32 format memory block |
| TRTCWaterMarkSrcTypeRGBA32 | 2 | RGBA32 format memory block. |

## TRTCAudioRecordingContent

#### Audio Recording Content Type

This enumeration type is used for the audio recording interface startAudioRecording to specify the content of the audio to be recorded.
| Enumeration | Value | Description |
| --- | --- | --- |
| TRTCAudioRecordingContentAll | 0 | Record all local and remote audio. |
| TRTCAudioRecordingContentLocal | 1 | Record local audio only. |
| TRTCAudioRecordingContentRemote | 2 | Record remote audio only. |

## TRTCPublishMode

#### Media Stream Publication Mode

This enumeration type is used for the media stream publishing interface startPublishMediaStream. TRTC's media stream publishing service can mix multiple audio and video streams in the room into one stream and publish it to a CDN or push it back to the room. You can also publish your current audio and video stream to Tencent or a third-party CDN. Therefore, you need to specify the publishing mode of the corresponding media stream. We provide the following modes.
| Enumeration | Value | Description |
| --- | --- | --- |
| TRTCPublishModeUnknown | 0 | Undefined. |
| TRTCPublishBigStreamToCdn | 1 | You can set this parameter to publish the main stream (TRTCVideoStreamTypeBig) in your room to Tencent or third-party live streaming CDN services (only supports standard RTMP protocol). |
| TRTCPublishSubStreamToCdn | 2 | You can set this parameter to publish the substream (TRTCVideoStreamTypeSub) in your room to Tencent or third-party live streaming CDN services (only supports standard RTMP protocol). |
| TRTCPublishMixStreamToCdn | 3 | You can set this parameter, together with encoding output parameters (TRTCStreamEncoderParam) and mix stream transcoding parameters (TRTCStreamMixingConfig), to transcode and publish your specified multiple audio and video streams to Tencent or third-party live streaming CDN services (only supports standard RTMP protocol). |
| TRTCPublishMixStreamToRoom | 4 | You can set this parameter, together with media stream encoding output parameters (TRTCStreamEncoderParam) and mix stream transcoding parameters (TRTCStreamMixingConfig), to transcode and publish your specified multiple audio and video streams into your specified room. -  Specify the robot information for the pushback room through TRTCPublishTarget TRTCUser. |

## TRTCEncryptionAlgorithm

#### Encryption Algorithm

This enumeration type is used for the selection of the private encryption algorithm for media streams.
| Enumeration | Value | Description |
| --- | --- | --- |
| TRTCEncryptionAlgorithmAes128Gcm | 0 | AES GCM 128. |
| TRTCEncryptionAlgorithmAes256Gcm | 1 | AES GCM 256. |

## TRTCSpeedTestScene

#### Speed Test Scenario

This enumeration type is used for selecting the speed test scenario.
| Enumeration | Value | Description |
| --- | --- | --- |
| TRTCSpeedTestScene_DelayTesting | 1 | Latency test. |
| TRTCSpeedTestScene_DelayAndBandwidthTesting | 2 | Latency and bandwidth test. |
| TRTCSpeedTestScene_OnlineChorusTesting | 3 | Online chorus test. |

## TRTCGravitySensorAdaptiveMode

#### Set Adaptation Mode for Gravity Sensor (Only applicable to mobile devices)
| Enumeration | Value | Description |
| --- | --- | --- |
| TRTCGravitySensorAdaptiveMode_Disable | 0 | Turn off gravity sensing. Based on the current captured resolution and the set encoding resolution, if they are inconsistent, rotate by 90 degrees to ensure the maximum frame size. |
| TRTCGravitySensorAdaptiveMode_FillByCenterCrop | 1 | Enable gravity sensing. Always ensure the remote screen image is correct. When there is a resolution inconsistency, use the centered cropping mode. |
| TRTCGravitySensorAdaptiveMode_FitWithBlackBorder | 2 | Enable gravity sensing. Always ensure the remote screen image is correct. When there is a resolution inconsistency, use the black border overlay mode. |

## TRTCParams

#### Room entry parameters

As an entry parameter for the TRTC SDK, only if this parameter is filled in correctly can you successfully enter the audio and video room specified by roomId or strRoomId.

Due to historical reasons, TRTC supports two types of room numbers, numeric and string, which are roomId and strRoomId respectively.

Please note: Do not mix roomId and strRoomId, as they are not interchangeable. For example, the number 123 and the string "123" are considered two completely different rooms in TRTC.
| Enumeration Types | Description |
| --- | --- |
| businessInfo | [Field Meaning] Business data field (optional). This field is required for some advanced features. [Recommended Value] Please do not set this field yourself. |
| privateMapKey | [Field Meaning] Permission ticket used for permission control (optional). If you want only specific userIds to enter a room, you need to use privateMapKey for permission protection. [Recommended Value] Only recommended for customers with high-level security requirements. For more details, please refer to [Room Entry Permission Protection](https://cloud.tencent.com/document/product/647/32240). |
| role | [Field Meaning] Role in live streaming scenarios, only applicable to live streaming scenarios (TRTCAppSceneLIVE and TRTCAppSceneVoiceChatRoom). Specifying this parameter in a calling scenario is ineffective. [Recommended Value] Default value: Anchor (TRTCRoleAnchor). |
| roomId | [Field Meaning] Numeric room number, where users (userId) in the same room can see each other and make audio and video calls. [Recommended Value] Value range: 1 - 4294967294. [Special Explanation] roomId and strRoomId are mutually exclusive. If you choose strRoomId, roomId must be set to 0. If both are filled, the SDK will prioritize roomId. [Please note] Do not mix roomId and strRoomId as they are not interchangeable. For example, the number 123 and the string `123` are considered two entirely different rooms in TRTC. |
| sdkAppId | [Field Meaning] Application Identifier (Required). Tencent Cloud uses sdkAppId for billing statistics. [Recommended Value] This ID can be obtained from the account information page after creating an application in the [TRTC Console](https://console.cloud.tencent.com/rav/). |
| strRoomId | [Field Meaning] String room number, where users (userId) in the same room can see each other and make audio and video calls. [Special Explanation] roomId and strRoomId are mutually exclusive. If you choose strRoomId, roomId must be set to 0. If both are filled, the SDK will prioritize roomId. [Please note] Do not mix roomId and strRoomId as they are not interchangeable. For example, the number 123 and the string `123` are considered two entirely different rooms in TRTC. [Recommended Value] Length limit is 64 bytes. The following character set range is supported (a total of 89 characters): -  Upper and lowercase English letters (a-zA-Z); -  Numbers (0-9); -  Space,` ! `,` # `,` $ `,` % `,` & `,` ( `,` ) `,` + `,` - `,` : `,` ; `,` < `,` = `,` . `,` > `,` ? `,` @ `,` [ `,` ] `,` ^ `,` _ `,` { `,` } `,` \\| `,` ~ `,` , `. |
| streamId | [Field Meaning] Used to specify the streamId on the Tencent CSS platform (optional). Once set, you can play the user's audio and video streams on the Tencent CSS CDN through the standard pull streaming scheme (FLV or HLS). [Recommended Value] Length limit is 64 bytes and can be left blank. A recommended scheme is to use ` sdkappid_roomid_userid_main ` as the streamId. This naming convention is easy to identify and will not conflict with your multiple applications. [Special Note] To use Tencent CSS CDN, you need to first enable the "Automatic Bypass Live Streaming" switch on the feature configuration page in the [console](https://console.cloud.tencent.com/trtc/). [Reference Document][CDN Bypass Live Streaming](https://cloud.tencent.com/document/product/647/16826). |
| userDefineRecordId | [Field Meaning] Cloud recording switch (optional). Used to specify whether to record this user's audio and video streams in the cloud. [Reference Document][Cloud Recording](https://cloud.tencent.com/document/product/647/16823). [Recommended Value] Length limit is 64 bytes. Only uppercase and lowercase English letters (a-zA-Z), numbers (0-9), underscores, and hyphens are allowed. Scheme 1: Manual Recording Scheme: 1. Enable Cloud Recording in the [Console](https://console.cloud.tencent.com/trtc)>Application Management>Cloud Recording Configuration. 2. Set the ` recording mode ` to ` manual recording `. 3. After setting manual recording, only users who set the userDefineRecordId parameter in a TRTC room will have recorded video files on the cloud. Users who do not specify this parameter will not be recorded. 4. The cloud will name the recorded files in the format "userDefineRecordId_start time_end time". Scheme 2: Automatic Recording Scheme: 1. Enable Cloud Recording in the [Console](https://console.cloud.tencent.com/trtc)>Application Management>Cloud Recording Configuration. 2. Set the ` recording mode ` to ` automatic recording `. 3. After setting automatic recording, any user with audio/video uplink in a TRTC room will have recorded video files on the cloud. 4. The files will be named in the format ` userDefineRecordId_start time_end time `. If userDefineRecordId is not specified, the files will be named in the format ` streamId_start time_end time `. |
| userId | [Field Meaning] User Identification (Required). The current user's userId, equivalent to username, using UTF-8 encoding. [Recommended Value] If a user's ID in your account system is "mike", then userId can be set to "mike". |
| userSig | [Field Meaning] User Signature (Required). The verification signature corresponding to the current userId, equivalent to using the cloud service's login password. [Recommended Value] For the specific calculation method, please see [How to Calculate UserSig](https://cloud.tencent.com/document/product/647/17275). |

## TRTCVideoEncParam

#### Video encoding parameters

This setting determines the picture quality seen by remote users and also the picture quality of the video files recorded on the cloud.
| Enumeration Types | Description |
| --- | --- |
| enableAdjustRes | [Field Meaning] Whether to allow dynamic resolution adjustment (enabling this will impact cloud recording). [Recommended Value] This feature is suitable for scenarios where cloud recording is not needed. When enabled, the SDK will intelligently select an appropriate resolution based on the current network conditions to avoid inefficient encoding modes like "high resolution + low bitrate". [Special Note] Default value: Disabled. If you need cloud recording, do not enable this feature because if the video resolution changes, the recorded MP4 on the cloud cannot be played properly on regular players. |
| minVideoBitrate | [Field Meaning] Minimum video bitrate. The SDK will actively lower the video bitrate when the network is poor to maintain smoothness, with the minimum lowered to the value set by minVideoBitrate. [Special Note] Default value: 0, in which case the minimum bitrate will be automatically calculated by the SDK based on the resolution you specified. [Recommended Value] You can set both videoBitrate and minVideoBitrate parameters simultaneously to constrain the SDK's video bitrate adjustment range: -  If you pursue ` allowing stuttering under weak networks but maintaining clarity `, you can set minVideoBitrate to 60% of videoBitrate. -  If you pursue ` allowing blurriness under weak networks but maintaining smoothness `, you can set minVideoBitrate to a lower value (e.g., 100kbps). -  If you set videoBitrate and minVideoBitrate to the same value, it is equivalent to disabling the SDK's adaptive video bitrate adjustment capability. |
| resMode | [Field Meaning] Resolution Mode (horizontal resolution or vertical resolution). [Recommended Value] For mobile platforms (iOS, Android), it is recommended to choose Portrait. For desktop platforms (Windows, Mac), it is recommended to choose Landscape. [Special Note] If you need to use vertical resolution, specify resMode as Portrait, e.g., 640 × 360 + Portrait = 360 × 640. |
| videoBitrate | [Field Meaning] Target video bitrate. The SDK will encode according to the target bitrate and will only actively lower the video bitrate in weak network environments. [Recommended Value] Please refer to the optimal bitrate annotations for each level in TRTCVideoResolution, which can also be appropriately increased. For example, TRTCVideoResolution_1280_720 corresponds to a target bitrate of 1200kbps, but you can set it to 1500kbps for better visual clarity. [Special Note] You can set both videoBitrate and minVideoBitrate parameters simultaneously to constrain the SDK's video bitrate adjustment range: -  If you prefer "allowing stuttering under weak network conditions but maintaining clarity," you can set minVideoBitrate to 60% of videoBitrate. -  If you prefer "allowing blurring under weak network conditions but maintaining smoothness," you can set minVideoBitrate to a lower value (e.g., 100kbps). -  If you set videoBitrate and minVideoBitrate to the same value, it is equivalent to disabling the SDK's adaptive video bitrate adjustment capability. |
| videoFps | [Field Meaning] Video capture frame rate. [Recommended Value] 15fps or 20fps. Below 5fps, lag sensation is noticeable. Below 10fps, there will be slight lag. Above 20fps, it will waste bandwidth (the frame rate of movies is 24fps). [Special Note] Some Android phones' front-facing cameras do not support a capture frame rate above 15fps. The capture frame rate of the front-facing camera of some Android phones with a beauty feature may be below 10fps. |
| videoResolution | [Field Meaning] Video resolution. [Special Note] If you need to use vertical resolution, specify resMode as Portrait, e.g., 640 × 360 + Portrait = 360 × 640. [Recommended Values] -  Mobile video call: It is recommended to choose 360 × 640 or lower resolution, with resMode set to Portrait (vertical resolution). -  Mobile online live streaming: It is recommended to choose 540 × 960, with resMode set to Portrait (vertical resolution). -  Desktop platform (Win + Mac): It is recommended to choose 640 × 360 or higher resolution, with resMode set to Landscape (horizontal resolution). |

## TRTCNetworkQosParam

#### Network flow control (Qos) parameter set

Network traffic control parameters, this setting determines the SDK's adjustment strategy in poor network conditions (for example: "Clarity Priority" or "Smoothness Priority").
| Enumeration Types | Description |
| --- | --- |
| controlMode | [Field Meaning] Flow control mode (deprecated). [Recommended Values] Cloud Control. [Special Note] Please set it to Cloud Control mode (TRTCQosControlModeServer). |
| preference | [Field Meaning] Clarity Priority or Smooth Priority. [Recommended Values] Clarity Priority. [Special Note] This parameter mainly affects TRTC's audio and video performance in poor network environments: -  Smooth Priority: When the current network is insufficient to transmit both clear and smooth images, it prioritizes the smoothness of the picture, which results in a blurrier image with more mosaics. See TRTCVideoQosPreferenceSmooth -  Clarity Priority (default): When the current network is insufficient to transmit both clear and smooth images, it prioritizes the clarity of the picture, which results in more stuttering. See TRTCVideoQosPreferenceClear |

## TRTCRenderParams

#### Rendering parameters for video footage

You can control the screen's rotation angle, fill mode, and left-right mirror mode by setting this parameter.
| Enumeration Types | Description |
| --- | --- |
| fillMode | [Field Meaning] Screen Fill Mode. [Recommended Values] Fill (the screen may be stretched or cropped) or Fit (the screen may have black edges), Default: TRTCVideoFillMode_Fill. |
| mirrorType | [Field Meaning] Screen Mirror Mode. [Recommended Value] Default value: TRTCVideoMirrorType_Auto. |
| rotation | [Field Meaning] Clockwise rotation angle of the image. [Recommended Value] Supports 90, 180, and 270 rotation angles. Default value: TRTCVideoRotation0. |

## TRTCQualityInfo

#### Network quality

Represents the quality of the network. This value can be used to display each user's network quality on the user interface.
| Enumeration Types | Description |
| --- | --- |
| quality | Network quality |
| userId | User ID |

## TRTCVolumeInfo

#### Volume level

Represents the evaluation value of voice volume. This value can be used to display each user's volume on the user interface.
| Enumeration Types | Description |
| --- | --- |
| pitch | The voice frequency of the local user (in Hz), range [0 - 4000]. For remote users, this value is always 0. |
| spectrumData | Audio spectrum data represents the distribution of audio data in the frequency domain, divided into 256 frequency bands. The spectrumData records the energy value of each frequency band, each energy value ranges from [-300, 0], in dBFS. **Note** Local spectrum is calculated using the audio data before encoding, affected by local collection volume and BGM, etc. Remote spectrum is calculated using received audio data, and local adjustments to remote playback volume will not affect it. |
| spectrumDataLength | spectrumDataLength records the length of the audio spectrum data, which is 256. |
| userId | The userId of the speaker. If the userId is empty, it represents the current user. |
| vad | Detect vocals or not, 0: Non-vocals, 1: Vocals. |
| volume | The speaker's volume. Value range: [0-100]. |

## TRTCSpeedTestParams

#### Speed test parameters

You can test the network speed before the user enters the room through the startSpeedTest interface (Note: Do not call during a call).
| Enumeration Types | Description |
| --- | --- |
| expectedDownBandwidth | Expected downstream bandwidth (kbps, value range: 10–5000, 0 means not to test). **Note** When the parameter scene is set to TRTCSpeedTestScene_OnlineChorusTesting, to obtain more accurate RTT/jitter information, the value range is limited to 10–1000. |
| expectedUpBandwidth | Expected upstream bandwidth (kbps, value range: 10–5000, 0 means not to test). **Note** When the parameter scene is set to TRTCSpeedTestScene_OnlineChorusTesting, to obtain more accurate RTT/jitter information, the value range is limited to 10–1000. |
| scene | Speed Testing Scenario. |
| sdkAppId | Application identifier, please refer to the relevant instructions in TRTCParams. |
| userId | User identifier, please refer to the relevant instructions in TRTCParams. |
| userSig | User signature, please refer to the relevant instructions in TRTCParams. |

## TRTCSpeedTestResult

#### Network speed test results

You can test the network speed before the user enters the room through the startSpeedTest interface (Note: Do not call during a call).
| Enumeration Types | Description |
| --- | --- |
| availableDownBandwidth | Downstream bandwidth (kbps, -1: invalid value). |
| availableUpBandwidth | Uplink bandwidth (kbps, -1: invalid value). |
| downJitter | Downlink packet jitter (ms), indicating the stability of data communication in the user's current network environment. The smaller the value, the better. The normal value range is 0ms to 100ms. -1 means that the speed test did not obtain a valid value. Generally, WiFi networks have slightly higher jitter than 4G/5G environments. |
| downLostRate | Downlink packet loss rate, the value range is [0 - 1.0]. For example, 0.2 means that out of every 10 packets received from the server, 2 might be lost mid-transmission. |
| errMsg | Bandwidth test error information. |
| ip | Server IP address. |
| quality | Internal evaluation algorithm calculates the network quality. For more information, please refer to TRTCQuality. |
| rtt | Latency (ms), representing the round-trip network time between the current device and the TRTC server. The smaller the value, the better. The normal value range is 10ms to 100ms. |
| success | Test success or failure. |
| upJitter | Uplink packet jitter (ms), indicating the stability of data communication in the user's current network environment. The smaller the value, the better. The normal value range is 0ms to 100ms. -1 means that the speed test did not obtain a valid value. Generally, WiFi networks have slightly higher jitter than 4G/5G environments. |
| upLostRate | Uplink packet loss rate, the value range is [0 - 1.0]. For example, 0.3 means that out of every 10 packets sent to the server, 3 might be lost mid-transmission. |

## TRTCTexture

#### Video texture data
| Enumeration Types | Description |
| --- | --- |
| glContext | [Field meaning] The OpenGL context environment where the texture resides, valid on Windows and Android platforms |
| glTextureId | [Field meaning] Video texture ID. |
| } | [Field meaning] D3D11 texture, i.e., ID3D11Texture2D pointer, valid only on Windows platform. |

## TRTCVideoFrame

#### Video frame information

TRTCVideoFrame describes the raw data of a video frame, which is the video frame data before encoding or after decoding.
| Enumeration Types | Description |
| --- | --- |
| bufferType | [Field meaning] Video data structure type. |
| data | [Field meaning] Video data when bufferType is TRTCVideoBufferType_Buffer, carrying memory blocks for the C++ layer. |
| height | [Field meaning] Video height. |
| length | [Field meaning] Length of video data, unit is bytes. For i420: length = width * height * 3 / 2; For BGRA32: length = width * height * 4. |
| rotation | [Field meaning] Clockwise rotation angle of video pixels. |
| texture | [Field meaning] Video data when bufferType is TRTCVideoBufferType_Texture, containing texture data for OpenGL rendering. |
| timestamp | [Field meaning] Timestamp of the video frame, in milliseconds. [Recommended values] Can be set to 0 when capturing Definition video. If this parameter is 0, the SDK will automatically populate the timestamp field, but please control the intervals of sendCustomVideoData calls "evenly". |
| videoFormat | [Field meaning] Pixel format of the video. |
| width | [Field meaning] Video width. |

## TRTCAudioFrame

#### Audio frame data
| Enumeration Types | Description |
| --- | --- |
| audioFormat | [Field meaning] Audio frame format. |
| channel | [Field meaning] Number of channels. |
| data | [Field meaning] Audio data. |
| extraData | [Field meaning] Extra audio data. The data written by the remote user through ` onLocalProcessedAudioFrame ` will be callbacked via this field. |
| extraDataLength | [Field meaning] Length of audio message data. |
| length | [Field meaning] Length of audio data. |
| sampleRate | [Field meaning] Sample rate. |
| timestamp | [Field meaning] Timestamp, in milliseconds. |

## TRTCMixUser

#### Description information of each stream in Cloud Mixed Streaming

TRTCMixUser is used to specify the position, size, layer, stream type, etc., of each video screen in Cloud Mixed Streaming.
| Enumeration Types | Description |
| --- | --- |
| image | [Field meaning] Placeholder Image or Watermark Image -  A placeholder image refers to an image displayed in the mixed screen when the corresponding userId's mixed content is pure audio. -  A watermark image refers to a semi-transparent image pasted on the mixed screen, always covering the mixed screen. -  When you specify inputType as TRTCMixInputTypePureAudio, the image is a placeholder image, and you need to specify the userId. -  When you specify inputType as TRTCMixInputTypeWatermark, the image is a watermark image, and you do not need to specify the userId. [Recommended Values] Default: empty, which means no placeholder image or watermark image is set. [Special Note] -  You can set the image to an asset ID found in the console. This requires you to click the [Add Image] button to upload it beforehand in "[Console](https://console.cloud.tencent.com/trtc) => Application Management => Feature Configuration => Asset Management". -  Upon successful upload, you will receive a corresponding "image ID". Convert the "image ID" into a string and set it to the image field accordingly (e.g., if the "image ID" is 63, you can set image to @"63"). -  You can also set the image to a URL address, and Tencent Cloud's backend server will mix the image specified by the URL into the final screen. -  The URL length is limited to 512 bytes. The size of the image must not exceed 2MB. -  Supported image formats include png, jpg, jpeg, and bmp. It is recommended to use semi-transparent png images as watermarks. -  The image is only effective when inputType is set to TRTCMixInputTypePureAudio or TRTCMixInputTypeWatermark. |
| inputType | [Field meaning] Specifies the mixed content of the stream (only audio, only video, mixed audio and video, watermarking). [Default Value] Default: TRTCMixInputTypeUndefined. [Special Note] -  When inputType is set to TRTCMixInputTypeUndefined and pureAudio is set to YES, it is equivalent to setting inputType to TRTCMixInputTypePureAudio. -  When inputType is set to TRTCMixInputTypeUndefined and pureAudio is set to NO, it is equivalent to setting inputType to TRTCMixInputTypeAudioVideo. -  When inputType is set to TRTCMixInputTypeWatermark, you do not need to specify the userId field but must specify the image field. |
| pureAudio | [Field meaning] Specifies whether the stream is audio-only. [Recommended Values] Default: false. [Special Note] Deprecated. It is recommended to use the newly introduced field inputType starting from version 8.5. |
| rect | [Field meaning] Specifies the coordinate area of the screen (unit: pixels). |
| renderMode | [Field meaning] The display mode of the screen during output. [Recommended Values] Default: for video streams, 0.0 for cropping, 1 for scaling, and 2 for scaling with a black background. [Special Note] The watermark image and placeholder image currently do not support setting renderMode. Default forced stretching is applied. |
| roomId | [Field meaning] The room number of the audio and video stream (setting it to an empty value represents the room number of the current user). |
| soundLevel | [Field meaning] The volume level of the audio participating in the mix (range: 0 - 100). [Default Value] Default: 100. |
| streamType | [Field Meaning] Specifies whether this video stream is a main stream (TRTCVideoStreamTypeBig) or a sub-stream (TRTCVideoStreamTypeSub). |
| userId | [Field Meaning] User ID |
| zOrder | [Field Meaning] Specifies the level of the screen (Range: 1 - 15, unique). |

## TRTCTranscodingConfig

#### Layout and transcoding parameters for Cloud Mixed Streaming

For specifying the layout position and encoding parameters of each screen during mix streaming and on-cloud transcoding.
| Enumeration Types | Description |
| --- | --- |
| appId | [Field Meaning] AppID of Tencent CSS service. [Recommended Value] Please click in sequence in the [TRTC console](https://console.cloud.tencent.com/trtc) [Application Management]=>[Application Information], and obtain the appid from [CDN Live Streaming Info]. |
| audioBitrate | [Field Meaning] Specifies the target audio bitrate for cloud transcoding. [Recommended Value] Default: 64kbps, range: [32,192]. |
| audioChannels | [Field Meaning] Specifies the number of audio channels for cloud transcoding. [Recommended Value] Default: 1, representing mono. The allowable values are: 1 - mono, 2 - stereo. |
| audioCodec | [Field Meaning] Specifies the output stream audio encoding type for cloud transcoding. [Recommended Value] Default: 0, representing LC-AAC. The allowable values are: 0 - LC-AAC, 1 - HE-AAC, 2 - HE-AACv2. [Special Explanation] HE-AAC and HE-AACv2 support output stream audio sample rates of [48000, 44100, 32000, 24000, 16000]. [Special Explanation] When audio encoding is set to HE-AACv2, only stereo output is supported. [Special Note] HE-AAC and HE-AACv2 values only take effect when the output stream is the additional streamId you set. |
| audioSampleRate | [Field Meaning] Specifies the target audio sampling rate for cloud transcoding. [Recommended Values] Default: 48000Hz. Supports 12000Hz, 16000Hz, 22050Hz, 24000Hz, 32000Hz, 44100Hz, 48000Hz. |
| backgroundColor | [Field Meaning] Specifies the background color of the mixed-screen. [Recommended Values] Default: 0x000000 represents black. The format is a hexadecimal number, e.g., "0x61B9F1" represents RGB values as (97,158,241). |
| backgroundImage | [Field Meaning] Specifies the background image of the mixed-screen. [Recommended Values] Default: empty, meaning no background image is set. [Special Note] -  You can set the image to an asset ID found in the console. This requires you to click the [Add Image] button to upload it beforehand in "[Console](https://console.cloud.tencent.com/trtc) => Application Management => Feature Configuration => Asset Management". -  Upon successful upload, you will receive a corresponding "image ID". Convert the "image ID" into a string and set it to the image field accordingly (e.g., if the "image ID" is 63, you can set image to @"63"). -  You can also set the image to a URL address, and Tencent Cloud's backend server will mix the image specified by the URL into the final screen. -  The URL length is limited to 512 bytes. The size of the image must not exceed 2MB. -  Supported image formats include png, jpg, jpeg, and bmp. |
| bizId | [Field Meaning] bizid of Tencent CSS service. [Recommended Value] Please click in sequence in the [ TRTC Console](https://console.cloud.tencent.com/trtc) [Application Management] => [Application Information], and obtain the bizid from [CDN Live Streaming Info]. |
| mixUsersArray | [Field Meaning] Specifies the position, size, layer, and stream type information for each video screen in the cloud mix. [Recommended Values] This field is an array of TRTCMixUser type. Each element in the array represents the information for each screen. |
| mixUsersArraySize | [Field meaning] Number of elements in the mixUsersArray. |
| mode | [Field Meaning] Layout mode. [Recommended Values] Please choose according to your business scenario requirements. Pre-layout mode is a well-suited option. |
| streamId | [Field Meaning] Live stream ID for output to CDN. [Recommended Value] Default: Null Value, meaning that the multiple audio and video streams in the room will ultimately be mixed into the interface caller's audio and video stream. -  If this parameter is not set, the SDK will execute the default logic, meaning the multiple audio and video streams in the room will be mixed into the interface caller's audio and video stream, i.e., A + B => A. -  If you set this parameter, the SDK will mix the multiple audio and video streams in the room into the live stream you specified, i.e., A + B => C (C represents the streamId you specified). |
| videoBitrate | [Field Meaning] Specifies the target video bitrate (kbps) for cloud transcoding. [Recommended Value] If set to 0, TRTC will estimate a reasonable bitrate based on videoWidth and videoHeight. You can also refer to the bitrate value recommended in the video resolution enum Definition (see the comment section). |
| videoFramerate | [Field Meaning] Specifies the target video frame rate (FPS) for cloud transcoding. [Recommended Value] Default: 15fps, range: (0,30]. |
| videoGOP | [Field Meaning] Specifies the target video keyframe interval (GOP) for cloud transcoding. [Recommended Value] Default: 2 seconds, range: [1,8]. |
| videoHeight | [Field Meaning] Specifies the target resolution (height) for cloud transcoding. [Recommended Value] Unit: Pixel Value. Recommended value: 640. If you are only mixing audio streams, set both width and height to 0, otherwise, the mixed transcoding live stream will have a black background. |
| videoSeiParams | [Field Meaning] Stream Mixing SEI Parameters. Not specified by default. [Special Note] Parameters are passed in as a JSON String. Example: `{` `  "payLoadContent":"xxx",` `  "payloadType":5,` `  "payloadUuid":"1234567890abcdef1234567890abcdef",` `  "interval":1000,` `  "followIdr":false` `}` Supported fields and their meanings: -  payloadContent: Required. The payload content of the transparent SEI; cannot be empty -  payloadType: Required. The type of SEI message, with a range of values: 5, or integers within [100, 254] (excluding 244, which is an internal self-definition timestamp SEI); -  payloadUuid: Required when payloadType is 5, otherwise this value is ignored. This value must be a 32-character hexadecimal number; -  interval: Optional, default is 1000. The sending interval of SEI, in milliseconds; -  followIdr: Optional, default is false. When set to true, SEI will be ensured with keyframes, otherwise, it will not be ensured. |
| videoWidth | [Field Meaning] Specifies the target resolution (width) for cloud transcoding. [Recommended Value] Unit: Pixel Value. Recommended value: 360. If you are only mixing audio streams, set both width and height to 0, otherwise, the mixed transcoding live stream will have a black background. |

## TRTCPublishCDNParam

#### Retweet parameters when publishing audio and video streams to non-Tencent Cloud CDN

The TRTC backend service supports publishing audio and video streams to third-party live streaming CDN service providers using the standard RTMP protocol.

If you are using Tencent CSS CDN Service, you can disregard this parameter and use the startPublish interface directly.
| Enumeration Types | Description |
| --- | --- |
| appId | [Field Meaning] AppID of Tencent CSS service. [Recommended Value] Please click in sequence in the [TRTC console](https://console.cloud.tencent.com/trtc) [Application Management]=>[Application Information], and obtain the appid from [CDN Live Streaming Info]. |
| bizId | [Field Meaning] bizid of Tencent CSS service. [Recommended Value] Please click in sequence in the [ TRTC Console](https://console.cloud.tencent.com/trtc) [Application Management] => [Application Information], and obtain the bizid from [CDN Live Streaming Info]. |
| streamId | [Field Meaning] The streamId that needs to be relayed. [Recommended Value] Default value: empty. If not filled, the default relay is the bidder's bypass stream. |
| url | [Field Meaning] Specifies the streaming address (RTMP format) of the audio and video stream on the third-party live streaming service provider. [Recommended Value] The rules for the streaming address vary greatly between service providers. Please fill in a valid streaming URL according to the requirements of the target service provider. The TRTC backend server will publish the standard format audio and video streams to the third-party provider according to the URL you filled in. [Special Instructions] The streaming URL must be in RTMP format and comply with your target live streaming service provider's specifications, otherwise, the target service provider will reject push-stream requests from the TRTC backend services. |

## TRTCAudioRecordingParams

#### Recording parameters for local audio files

This parameter is used to specify recording parameters in the audio recording interface startAudioRecording.
| Enumeration Types | Description |
| --- | --- |
| filePath | [Field meaning] The save path of the recording file (required). [Special Instructions] This path must include the file name and format suffix, as the suffix determines the format of the recording file. The currently supported formats are PCM, WAV, and AAC. For example: If you specify the path as "mypath/record/audio.aac", it means you want the SDK to generate an AAC format audio recording file. Please specify a legal path with read and write permissions, otherwise the recording file cannot be generated. |
| maxDurationPerFile | [Field meaning] maxDurationPerFile recording file split duration, unit: milliseconds, minimum value: 10000. The default value is 0, which means no splitting. |
| recordingContent | [Field meaning] Audio recording content type. [Special Instructions] By default, all local and remote audio is recorded. |

## TRTCLocalRecordingParams

#### Recording parameters for local media files

This parameter is used to specify recording-related parameters in the local media file recording interface startLocalRecording.

The interface startLocalRecording is an enhanced version of the interface startAudioRecording. The former can record video files, while the latter can only record audio files.
| Enumeration Types | Description |
| --- | --- |
| filePath | [Field meaning] The address of the recording file (required). Please ensure the path has read and write permissions and is legal, otherwise the recording file cannot be generated. [Special Instructions] This path must be precise to the file name and format suffix. The suffix determines the format of the recorded file. Currently, the only supported format is MP4. For example: If you specify the path as "mypath/record/test.mp4", it means you want the SDK to generate a local video file in MP4 format. Please specify a legal path with read and write permissions, otherwise the recording file cannot be generated. |
| interval | [Field meaning] interval recording information update frequency, unit: milliseconds, valid range: 1000-10000. Default value is -1, meaning no callback. |
| maxDurationPerFile | [Field meaning] maxDurationPerFile recording file split duration, unit: milliseconds, minimum value: 10000. The default value is 0, which means no splitting. |
| recordType | [Field meaning] Media recording type, default value: TRTCRecordTypeBoth, meaning to record both audio and video simultaneously. |

## TRTCSwitchRoomConfig

#### Room Switching Parameters

This parameter is used for the room switching interface switchRoom, allowing users to quickly switch from one room to another.
| Enumeration Types | Description |
| --- | --- |
| privateMapKey | [Field Meaning] Permission ticket used for permission control (optional). If you want only specific userIds to enter a room, you need to use privateMapKey for permission protection. [Recommended Value] Only recommended for customers with high-level security requirements. For more details, please refer to [Room Entry Permission Protection](https://cloud.tencent.com/document/product/647/32240). |
| roomId | [Field meaning] Numeric room number [optional], users in the same room can see each other and have audio and video calls. [Recommended Value] Value range: 1 - 4294967294. [Special Note] roomId and strRoomId must and can only fill one. If both are filled, roomId is preferred. |
| strRoomId | [Field meaning] String room number [optional], users in the same room can see each other and have audio and video calls. [Special Note] roomId and strRoomId must and can only fill one. If both are filled, roomId is preferred. |
| userSig | [Field meaning] User signature [optional], the verification signature corresponding to the current userId, equivalent to a log-in password. If you do not specify a newly calculated userSig when switching rooms, the SDK will continue using the userSig specified when you entered the room (enterRoom). You must ensure the old userSig is within its valid period when switching rooms; otherwise, the room switch will fail. [Recommended Value] For the specific calculation method, please see [How to Calculate UserSig](https://cloud.tencent.com/document/product/647/17275). |

## TRTCAudioFrameDelegateFormat

#### Format parameters for audio custom callback

This parameter is used in the audio self Definition callback related interfaces to set the format of the audio data retrieved by the SDK callback (including sampling rate, number of channels, etc.).
| Enumeration Types | Description |
| --- | --- |
| channel | [Field meaning] Number of channels. [Recommended Value] Default: 1, representing mono. The allowable values are: 1 - mono, 2 - stereo. |
| mode | [Field meaning] Callback data read/write mode [Recommended Values] TRTCAudioFrameOperationModeReadOnly: only retrieve audio data from the callback. The available modes are TRTCAudioFrameOperationModeReadOnly and TRTCAudioFrameOperationModeReadWrite. |
| sampleRate | [Field meaning] Sample rate. [Recommended Values] Default: 48000Hz. Supports 16000, 32000, 44100, 48000. |
| samplesPerCall | [Field meaning] Number of sampling points. [Recommended Values] The value must be an integer multiple of sampleRate/100. |

## TRTCImageBuffer

#### TRTC screen sharing icon information and mute image spacer
| Enumeration Types | Description |
| --- | --- |
| buffer | Contents of image storage, generally in BGRA structure. |
| height | Height of the image. |
| length | Size of the image data. |
| width | Width of the image. |

## TRTCScreenCaptureSourceInfo

#### Target information for screen sharing (only applicable to desktop systems)

When users are sharing a screen, they can choose to capture the entire desktop or just a specific program window.

TRTCScreenCaptureSourceInfo describes the target information to be shared, including ID, name, thumbnail, etc. The field information in this structure is read-only.
| Enumeration Types | Description |
| --- | --- |
| height | [Field meaning] Screen/Window height, in pixels. |
| iconBGRA | [Field meaning] Icon of the shared window. |
| isMainScreen | [Field meaning] Whether it is the main display screen (applies to the multi-monitor setup). |
| isMinimizeWindow | [Field meaning] Whether the window is minimized. |
| sourceId | [Field meaning] The ID of the capture source: for a window, this field represents the window ID; for a screen, this field represents the monitor ID. |
| sourceName | [Field meaning] Capturing source name (encoded in UTF8). |
| thumbBGRA | [Field meaning] Thumbnail of the shared window. |
| type | [Field meaning] Collection source type (Is it sharing the entire screen or a specific window?). |
| width | [Field meaning] Screen/Window width, in pixels. |
| x | [Field meaning] Screen/Window x coordinate, in pixels. |
| y | [Field meaning] Screen/Window y coordinate, in pixels. |

## TRTCScreenCaptureProperty

#### Advanced control parameters for screen sharing

This parameter is used for the screen sharing related interface selectScreenCaptureTarget, for setting a series of advanced control parameters when specifying the sharing target.

For example: whether to capture the mouse, whether to capture sub-windows, whether to draw a border around the shared target, etc.
| Enumeration Types | Description |
| --- | --- |
| enableCaptureChildWindow | [Field meaning] Whether to capture sub-windows during window capture (the sub-window needs to have the Owner or Popup attribute), default is false. |
| enableCaptureMouse | [Field meaning] Whether to capture the mouse along with the target content, default is true. |
| enableHighLight | [Field Meaning] Whether to highlight the window being shared (draw a border around the shared target), default is true. |
| enableHighPerformance | [Field Meaning] Whether to enable High-Performance Mode (only effective when sharing the screen), default is true. [Special Instruction] Performance is optimal when enabled, but it will lose anti-occlusion capability. If you enable both enableHighLight and enableHighPerformance, the remote user can see the highlighted border. |
| highLightColor | [Field Meaning] Specifies the color of the highlight border in RGB format. If 0 is passed, the default color is used, which is #FFE640. |
| highLightWidth | [Field Meaning] Specifies the width of the highlight border. If 0 is passed, the default stroke width is used. The default width is 5px, and the maximum value you can set is 50. |

## TRTCAudioParallelParams

#### Parameters for Intelligent Concurrent Playback Strategy of Remote Audio Stream

This parameter is used to set the intelligent concurrent playback strategy for remote audio streams.
| Enumeration Types | Description |
| --- | --- |
| includeUsersCount | [Field meaning] Designated users who will definitely be able to play concurrently. [Special note] List of user IDs for guaranteed concurrent playback. These users are not part of the intelligent selection. The number of includeUsers must be less than maxCount, otherwise, the concurrent playback setting is invalid. includeUsers is only effective when maxCount > 0. When includeUsers is effective, the maximum number of concurrent intelligent selections = maxCount - the number of effective includeUsers. |
| maxCount | [Field meaning] Maximum number of concurrent playbacks. Default value: 0. -  If maxCount > 0 and the actual number of users > maxCount, SDK will intelligently select maxCount streams for playback in real-time, significantly reducing performance consumption. -  If maxCount = 0, SDK will not limit the number of concurrent playbacks, which might cause performance issues in rooms with a high number of participants. |

## TRTCUser

#### User information on media stream publishing configuration

You can set this parameter, along with media stream target publishing parameters (TRTCPublishTarget) and stream mixing transcoding parameters (TRTCStreamMixingConfig), to transcode multiple audio and video streams you specify and publish them to the target publishing address you provide
| Enumeration Types | Description |
| --- | --- |
| intRoomId | [Field meaning] Numeric room number, which needs to match the room number type in your join room parameters (TRTCParams). [Recommended Value] Value range: 1 - 4294967294. [Special Note] intRoomId and strRoomId are mutually exclusive. If you choose strRoomId in your room entry parameters, then intRoomId needs to be set to 0. If both are filled, the SDK will prioritize intRoomId. |
| strRoomId | [Field meaning] String room number, which needs to match the room number type in your join room parameters (TRTCParams). [Special Note] intRoomId and strRoomId are mutually exclusive. If you choose roomId in your room entry parameters, then strRoomId does not need to be filled. If both are filled, the SDK will prioritize intRoomId. [Recommended Value] Length limit is 64 bytes. The following character set range is supported (a total of 89 characters): -  Upper and lowercase English letters (a-zA-Z); -  Numbers (0-9); -  Space,` ! `,` # `,` $ `,` % `,` & `,` ( `,` ) `,` + `,` - `,` : `,` ; `,` < `,` = `,` . `,` > `,` ? `,` @ `,` [ `,` ] `,` ^ `,` _ `,` { `,` } `,` \\| `,` ~ `,` , `. |
| userId | [Field meaning] User identifier, the current user's userId, equivalent to username, using UTF-8 encoding. [Recommended Value] If a user's ID in your account system is "mike", then userId can be set to "mike". |

## TRTCPublishCdnUrl

#### URL configuration for publishing audio and video streams to Tencent or third-party CDN

This configuration is for the target streaming configuration (TRTCPublishTarget) in the media stream publishing interface startPublishMediaStream
| Enumeration Types | Description |
| --- | --- |
| isInternalLine | [Field Meaning] Specifies whether the audio and video stream is published to Tencent Cloud. [Recommended Values] Default: true. [Special Instructions] If your target live streaming service provider is Tencent, set this parameter to true. The backend billing system will not charge for the retweet service fee in this case. |
| rtmpUrl | [Field Meaning] Specifies the streaming address (RTMP format) of the audio and video stream on Tencent or third-party live streaming service providers. [Recommended Value] The rules for the streaming address vary greatly between service providers. Please fill in a valid streaming URL according to the requirements of the target service provider. The TRTC backend server will publish the standard format audio and video streams to the third-party provider according to the URL you filled in. [Special Instructions] The streaming URL must be in RTMP format and comply with your target live streaming service provider's specifications, otherwise, the target service provider will reject push-stream requests from the TRTC backend services. |

## TRTCPublishTarget

#### Target Push Configuration

This configuration is for the media stream publishing interface startPublishMediaStream.
| Enumeration Types | Description |
| --- | --- |
| cdnUrlList | [Field Meaning] The streaming address (RTMP format) for publishing to Tencent or third-party live streaming service providers. [Special Instructions] If your mode is set to TRTCPublishMixStreamToRoom, you do not need to set this parameter. |
| cdnUrlListSize | [Field Meaning] Number of elements in the cdnUrlList array. [Special Instructions] If your mode is set to TRTCPublishMixStreamToRoom, you do not need to set this parameter. |
| mixStreamIdentity | [Field Meaning] Push-back Room Robot Information. [Special Instructions] You need to set this parameter only if your mode is set to TRTCPublishMixStreamToRoom. [Special Instructions] After setting, the transcoded audio and video data will be pushed back to your specified room. It is recommended to set a special userId to avoid confusion between the push-back robot and the host using the TRTC SDK to join the room. [Special Instructions] Users involved in stream mixing cannot subscribe to the transcoded stream. [Special Note] When the subscription mode you set before entering the room (setDefaultStreamRecvMode) is set to manual, you will need to manage the audio and video streams you wish to pull yourself (typically, when you pull the transcoding stream of the room, you should unsubscribe from the corresponding audio and video single streams involved in transcoding). [Special Explanation] If the subscription mode you set before entering the room (setDefaultStreamRecvMode) is automatic, users not participating in transcoding will automatically receive the transcoded stream sent by the backend and will no longer receive the audio and video single streams involved in transcoding. Unless you explicitly unsubscribe (muteRemoteVideoStream and muteRemoteAudio), the transcoded stream data will continue to be sent. |
| mode | [Field Meaning] Media Stream Publishing Mode. [Recommended Values] Please choose according to your business scenario requirements. TRTC supports relay, transcoding, and rollback to RTC room modes. [Special Explanation] If your business scenario requires multiple publishing modes, you can call the media stream publishing interface (startPublishMediaStream) multiple times and set different TRTCPublishTargets separately. [Special Explanation] For the same mode, please correspond to a media stream publishing interface (startPublishMediaStream), and use updatePublishCDNStream for updates when adjustments are needed later. |

## TRTCVideoLayout

#### Transcode Video Layout

This configuration is for the transcoding settings (TRTCStreamMixingConfig) in the media stream publishing interface (startPublishMediaStream).

For specifying the position, size, layer, and stream type of each video screen in the transcoded stream.
| Enumeration Types | Description |
| --- | --- |
| backgroundColor | [Field Meaning] Specifies the background color of the mixed-screen. [Recommended Values] Default: 0x000000 represents black. The format is a hexadecimal number, e.g., "0x61B9F1" represents RGB values as (97,158,241). |
| fillMode | [Field Meaning] Screen Fill Mode. [Recommended Values] Fill (the screen may be stretched or cropped) or Fit (the screen may have black edges), Default: TRTCVideoFillMode_Fill. |
| fixedVideoStreamType | [Field Meaning] Specifies whether this video stream is a main stream (TRTCVideoStreamTypeBig) or a sub-stream (TRTCVideoStreamTypeSub). |
| fixedVideoUser | [Field Meaning] User Information Participating in Transcoding. [Special Note] User information (TRTCUser) can be left unfilled (i.e., userId, intRoomId, and strRoomId are all left blank). In this case, when there is an anchor streaming audio and video data in the room initiating the stream mix, the TRTC back-end server will automatically populate the corresponding anchor's audio and video into your specified layout. |
| placeHolderImage | [Field Meaning] Placeholder image URL, i.e., when the specified user is temporarily only sending audio, Tencent Cloud's back-end server will mix the image specified by this URL into the final screen. [Recommended Values] Default: empty, which means no placeholder image is set. [Special Note] At this time, you need to specify the user information for fixedVideoUser's userId. [Special Note] -  The URL length is limited to 512 bytes. The size of the image must not exceed 2MB. -  Supported image formats include png, jpg, jpeg, and bmp. It is recommended to use semi-transparent png images as placeholders. |
| rect | [Field meaning] Specifies the coordinate area of the screen (unit: pixels). |
| zOrder | [Field Meaning] Specifies the level of the screen (Range: 0 - 15, unique). |

## TRTCWatermark

#### Watermark Layout

This configuration is used in the Transcoding Configuration (TRTCStreamMixingConfig) of the Media Stream Publishing Interface (startPublishMediaStream)
| Enumeration Types | Description |
| --- | --- |
| rect | [Field Meaning] Specifies the coordinate area of the watermark screen (unit: pixels). |
| watermarkUrl | [Field Meaning] Watermark URL, Tencent Cloud's back-end server will mix the image specified by this URL into the final screen. [Special Note] -  The URL length is limited to 512 bytes. The size of the image must not exceed 2MB. -  Supported image formats include png, jpg, jpeg, and bmp. It is recommended to use semi-transparent png images as watermarks. |
| zOrder | [Field Meaning] Specifies the level of the watermark screen (Range: 0 - 15, unique). |

## TRTCStreamEncoderParam

#### Media Stream Encoding Output Parameters

[Field Meaning] This configuration is used in the Media Stream Publishing Interface (startPublishMediaStream).

[Special Note] When the mode configuration in your publishing target (TRTCPublishTarget) is set to TRTCPublish_MixStream_ToCdn or TRTCPublish_MixStream_ToRoom, this parameter is required.

[Special Explanation] When you use the retweet service (mode is TRTCPublish_BigStream_ToCdn or TRTCPublish_SubStream_ToCdn), to ensure better stability and CDN play compatibility, it is also recommended that you fill in the specific parameters of this configuration.
| Enumeration Types | Description |
| --- | --- |
| audioEncodedChannelNum | [Field Meaning] Specifies the target audio channel count for the media publish stream. [Recommended Value] Default: 1, representing mono. The allowable values are: 1 - mono, 2 - stereo. |
| audioEncodedCodecType | [Field Meaning] Specifies the target audio encoding type for the media publish stream. [Recommended Value] Default: 0, representing LC-AAC. The allowable values are: 0 - LC-AAC, 1 - HE-AAC, 2 - HE-AACv2. [Special Explanation] HE-AAC and HE-AACv2 support output stream audio sample rates of [48000, 44100, 32000, 24000, 16000]. [Special Explanation] When audio encoding is set to HE-AACv2, only stereo output is supported. |
| audioEncodedKbps | [Field Meaning] Specifies the target audio bitrate (kbps) for the media publish stream. [Recommended Value] Default: 50kbps, range: [32,192]. |
| audioEncodedSampleRate | [Field Meaning] Specifies the target audio sampling rate for the media publish stream. [Recommended Value] Default: 48000Hz. Values are [48000, 44100, 32000, 24000, 16000, 8000], unit is Hz. |
| videoEncodedCodecType | [Field Meaning] Specifies the target video encoding type for the media publish stream. [Recommended Value] Default: 0, representing H264. The allowable values are: 0 - H264, 1 - H265. |
| videoEncodedFPS | [Field Meaning] Specifies the target video frame rate (FPS) for the media publish stream. [Recommended Value] Recommended value: 20fps, range: (0,30]. |
| videoEncodedGOP | [Field Meaning] Specifies the target video keyframe interval (GOP) for the media publish stream. [Recommended Value] Recommended value: 3 seconds, range: [1,5]. |
| videoEncodedHeight | [Field Meaning] Specifies the target resolution (height) for the media publish stream. [Recommended Value] Unit: Pixel Value. Recommended value: 640. If you are only mixing audio streams, set both width and height to 0, otherwise, the mixed transcoding live stream will have a black background. |
| videoEncodedKbps | [Field Meaning] Specifies the target video bitrate (kbps) for the media publish stream. [Recommended Values] If set to 0, TRTC will estimate a reasonable bitrate based on videoEncodedWidth and videoEncodedHeight. You can also refer to the bitrate value recommended in the video resolution enum Definition (see the comment section). |
| videoEncodedWidth | [Field Meaning] Specifies the target resolution (width) for the media publish stream. [Recommended Values] Unit: Pixel Value. Recommended value: 368. If you are only mixing audio streams, set both width and height to 0, otherwise, the mixed transcoding live stream will have a black background. |
| videoSeiParams | [Field Meaning] Stream Mixing SEI Parameters. Not specified by default. [Special Note] Parameters are passed in as a JSON String. Example: `{` `  "payLoadContent":"xxx",` `  "payloadType":5,` `  "payloadUuid":"1234567890abcdef1234567890abcdef",` `  "interval":1000,` `  "followIdr":false` `}` Supported fields and their meanings: -  payloadContent: Required. The payload content of the transparent SEI; cannot be empty -  payloadType: Required. The type of SEI message, with a range of values: 5, or integers within [100, 254] (excluding 244, which is an internal self-definition timestamp SEI); -  payloadUuid: Required when payloadType is 5, otherwise this value is ignored. This value must be a 32-character hexadecimal number; -  interval: Optional, default is 1000. The sending interval of SEI, in milliseconds; -  followIdr: Optional, default is false. When set to true, SEI will be ensured with keyframes, otherwise, it will not be ensured. |

## TRTCStreamMixingConfig

#### Media Stream Transcoding Configuration Parameters

This configuration is used for the media stream publish interface (startPublishMediaStream).

For specifying the layout position information of each screen and the input audio information during transcoding.
| Enumeration Types | Description |
| --- | --- |
| audioMixUserList | [Field Meaning] Specifies the information of each input audio stream in the transcoding stream. [Recommended Values] This field is an array of TRTCUser type. Each element in the array represents information for each input audio stream. [Special Note] User information can be left blank (i.e., audioMixUserList is empty). In this case, if the audio-related encoding output parameters in TRTCStreamEncoderParam are set, the TRTC backend server will automatically mix the audio of all hosts (currently supports up to 16 audio and video inputs). |
| audioMixUserListSize | [Field Meaning] Number of elements in the audioMixUserList array. |
| backgroundColor | [Field Meaning] Specifies the background color of the mixed-screen. [Recommended Values] Default: 0x000000 represents black. The format is a hexadecimal number, e.g., "0x61B9F1" represents RGB values as (97,158,241). |
| backgroundImage | [Field Meaning] Specifies the background image URL for the mixed screen. Tencent Cloud's backend server will mix the image specified by the URL into the final screen. [Recommended Values] Default: empty, meaning no background image is set. [Special Note] -  The URL length is limited to 512 bytes. The size of the image must not exceed 2MB. -  Supported image formats include png, jpg, jpeg, and bmp. It is recommended to use semi-transparent png images as background images. |
| videoLayoutList | [Field Meaning] Specifies the position, size, layer, and stream type information for each video screen in the mixed picture. [Recommended Values] This field is an array of TRTCVideoLayout type. Each element in the array represents the information for each screen. |
| videoLayoutListSize | [Field Meaning] Number of elements in the videoLayoutList array. |
| watermarkList | [Field Meaning] Specifies the position, size, layer, etc., information for each watermarked screen in the mixed picture. [Recommended Values] This field is an array of TRTCWatermark type. Each element in the array represents the information for each watermark. |
| watermarkListSize | [Field Meaning] Number of elements in the watermarkList array. |

## TRTCPayloadPrivateEncryptionConfig

#### Media Stream Private Encryption Configuration

This configuration is used to set the algorithm and key for private media stream encryption.
| Enumeration Types | Description |
| --- | --- |
| encryptionAlgorithm | [Field Meaning] Encryption algorithm, default is TRTCEncryptionAlgorithmAes128Gcm. |
| encryptionKey | [Field Meaning] Encryption key, string type. [Recommended Values] If the encryption algorithm is TRTCEncryptionAlgorithmAes128Gcm, the key length needs to be 16 bytes; if the encryption algorithm is TRTCEncryptionAlgorithmAes256Gcm, the key length needs to be 32 bytes. |
| encryptionSalt[32] | [Field Meaning] Salt, initial vector for encryption. [Recommended Values] Ensure that the array filled in for this parameter is not empty, not all zeros, and the data length is 32 bytes. |

## TRTCAudioVolumeEvaluateParams

#### Volume Assessment and related parameter settings

This setting is used to enable voice detection and sound spectrum calculation.
| Enumeration Types | Description |
| --- | --- |
| enablePitchCalculation | [Field Meaning] Whether to enable local voice frequency calculation |
| enableSpectrumCalculation | [Field Meaning] Whether to enable sound spectrum calculation. |
| enableVadDetection | [Field Meaning] Whether to enable local voice detection. [Please Note] It takes effect only when called before startLocalAudio. |
| interval | [Field Meaning] Sets the trigger interval for the onUserVoiceVolume callback, in milliseconds. The minimum interval is 100ms. If the value is less than or equal to 0, the callback will be disabled. [Recommended Value] Recommended value: 300 milliseconds. [Special Instruction] When the interval is greater than 0, the volume prompt will be enabled by default without additional settings. |
