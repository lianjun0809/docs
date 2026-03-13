> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

# 腾讯云实时音视频(TRTC SDK )文档

## 概述
`TRTCCloudDef.java` 是腾讯云实时音视频(TRTC SDK ) Android 平台的类型定义文档。

## 结构体类型
| 函数列表 | 描述 |
| --- | --- |
| TRTCParams | 进房参数。 |
| TRTCVideoEncParam | 视频编码参数。 |
| TRTCNetworkQosParam | 网络流控（Qos）参数集。 |
| TRTCRenderParams | 视频画面的渲染参数。 |
| TRTCQuality | 网络质量。 |
| TRTCVolumeInfo | 音量大小。 |
| TRTCSpeedTestParams | 测速参数。 |
| TRTCSpeedTestResult | 网络测速结果。 |
| TRTCTexture | 视频纹理数据。 |
| TRTCVideoFrame | 视频帧信息。 |
| TRTCAudioFrame | 音频帧数据。 |
| TRTCMixUser | 云端混流中各路画面的描述信息。 |
| TRTCTranscodingConfig | 云端混流的排版布局和转码参数。 |
| TRTCPublishCDNParam | 向非腾讯云 CDN 上发布音视频流时需设置的转推参数。 |
| TRTCAudioRecordingParams | 本地音频文件的录制参数。 |
| TRTCLocalRecordingParams | 本地媒体文件的录制参数。 |
| TRTCAudioEffectParam | 音效参数（已废弃）。 |
| TRTCSwitchRoomConfig | 房间切换参数。 |
| TRTCAudioFrameCallbackFormat | 音频自定义回调的格式参数。 |
| TRTCScreenShareParams | 屏幕分享参数（仅适用于 Android 平台）。 |
| TRTCAudioParallelParams | 远端音频流智能并发播放策略的参数。 |
| TRTCUser | 媒体流发布相关配置的用户信息。 |
| TRTCPublishCdnUrl | 向腾讯或者第三方 CDN 上发布音视频流时需设置的 url 配置。 |
| TRTCPublishTarget | 目标推流配置。 |
| TRTCVideoLayout | 转码视频布局。 |
| TRTCWatermark | 水印布局。 |
| TRTCStreamEncoderParam | 媒体流编码输出参数。 |
| TRTCStreamMixingConfig | 媒体流转码配置参数。 |
| TRTCPayloadPrivateEncryptionConfig | 媒体流私有加密配置。 |
| TRTCAudioVolumeEvaluateParams | 音量评估等相关参数设置。 |

## 枚举类型
| 枚举类型 | 描述 |
| --- | --- |
| TRTCVideoResolution | 视频分辨率。 |
| TRTCVideoResolutionMode | 视频宽高比模式。 |
| TRTCVideoStreamType | 视频流类型。 |
| TRTCVideoFillMode | 视频画面填充模式。 |
| TRTCVideoRotation | 视频画面旋转方向。 |
| TRTCBeautyStyle | 美颜（磨皮）算法。 |
| TRTCVideoPixelFormat | 视频像素格式。 |
| TRTCVideoBufferType | 视频数据传递方式。 |
| TRTCVideoMirrorType | 视频的镜像类型。 |
| TRTCSnapshotSourceType | 本地视频截图的数据源。 |
| TRTCAppScene | 应用场景。 |
| TRTCRoleType | 角色。 |
| TRTCQosControlMode(Deprecated) | 流控模式（已废弃）。 |
| TRTCVideoQosPreference | 画质偏好。 |
| TRTCQuality | 网络质量。 |
| TRTCAVStatusType | 音视频状态类型。 |
| TRTCAVStatusChangeReason | 音视频状态变化原因类型。 |
| TRTCAudioSampleRate | 音频采样率。 |
| TRTCAudioQuality | 声音音质。 |
| TRTCAudioRoute | 音频路由（即声音的播放模式）。 |
| TRTCReverbType | 声音混响模式。 |
| TRTCVoiceChangerType | 变声类型。 |
| TRTCSystemVolumeType | 系统音量类型（仅适用于移动设备）。 |
| TRTCAudioFrameFormat | 音频帧的内容格式。 |
| TRTCAudioCapabilityType | 系统支持的音频能力类型（仅适用于Android设备）。 |
| TRTCAudioFrameOperationMode | 音频回调数据读写模式。 |
| TRTCLogLevel | Log 级别。 |
| TRTCGSensorMode | 重力感应开关（仅适用于移动端）。 |
| TRTCTranscodingConfigMode | 云端混流的排版模式。 |
| TRTCRecordType | 媒体录制类型。 |
| TRTCMixInputType | 混流输入类型。 |
| TRTCDebugViewLevel | 用于渲染控件上展示的调试信息。 |
| TRTCAudioRecordingContent | 音频录制内容类型。 |
| TRTCPublishMode | 媒体流发布模式。 |
| TRTCEncryptionAlgorithm | 加密算法。 |
| TRTCSpeedTestScene | 测速场景。 |
| TRTCGravitySensorAdaptiveMode | 设置重力感应的适配模式（仅适用于移动端）。 |

## TRTCVideoResolution

#### 视频分辨率。

此处仅定义横屏分辨率（如 640 × 360），如需使用竖屏分辨率（如360 × 640），需要同时指定 TRTCVideoResolutionMode 为 Portrait。
| 枚举 | 取值 | 描述 |
| --- | --- | --- |
| TRTC_VIDEO_RESOLUTION_120_120 | 1 | 宽高比 1:1；分辨率 120x120；建议码率（VideoCall）80kbps; 建议码率（LIVE）120kbps。 |
| TRTC_VIDEO_RESOLUTION_160_160 | 3 | 宽高比 1:1 分辨率 160x160；建议码率（VideoCall）100kbps; 建议码率（LIVE）150kbps。 |
| TRTC_VIDEO_RESOLUTION_270_270 | 5 | 宽高比 1:1；分辨率 270x270；建议码率（VideoCall）200kbps; 建议码率（LIVE）300kbps。 |
| TRTC_VIDEO_RESOLUTION_480_480 | 7 | 宽高比 1:1；分辨率 480x480；建议码率（VideoCall）350kbps; 建议码率（LIVE）500kbps。 |
| TRTC_VIDEO_RESOLUTION_160_120 | 50 | 宽高比4:3；分辨率 160x120；建议码率（VideoCall）100kbps; 建议码率（LIVE）150kbps。 |
| TRTC_VIDEO_RESOLUTION_240_180 | 52 | 宽高比 4:3；分辨率 240x180；建议码率（VideoCall）150kbps; 建议码率（LIVE）250kbps。 |
| TRTC_VIDEO_RESOLUTION_280_210 | 54 | 宽高比 4:3；分辨率 280x210；建议码率（VideoCall）200kbps; 建议码率（LIVE）300kbps。 |
| TRTC_VIDEO_RESOLUTION_320_240 | 56 | 宽高比 4:3；分辨率 320x240；建议码率（VideoCall）250kbps; 建议码率（LIVE）375kbps。 |
| TRTC_VIDEO_RESOLUTION_400_300 | 58 | 宽高比 4:3；分辨率 400x300；建议码率（VideoCall）300kbps; 建议码率（LIVE）450kbps。 |
| TRTC_VIDEO_RESOLUTION_480_360 | 60 | 宽高比 4:3；分辨率 480x360；建议码率（VideoCall）400kbps; 建议码率（LIVE）600kbps。 |
| TRTC_VIDEO_RESOLUTION_640_480 | 62 | 宽高比 4:3；分辨率 640x480；建议码率（VideoCall）600kbps; 建议码率（LIVE）900kbps。 |
| TRTC_VIDEO_RESOLUTION_960_720 | 64 | 宽高比 4:3；分辨率 960x720；建议码率（VideoCall）1000kbps; 建议码率（LIVE）1500kbps。 |
| TRTC_VIDEO_RESOLUTION_160_90 | 100 | 宽高比 16:9；分辨率 160x90；建议码率（VideoCall）150kbps; 建议码率（LIVE）250kbps。 |
| TRTC_VIDEO_RESOLUTION_256_144 | 102 | 宽高比 16:9；分辨率 256x144；建议码率（VideoCall）200kbps; 建议码率（LIVE）300kbps。 |
| TRTC_VIDEO_RESOLUTION_320_180 | 104 | 宽高比 16:9；分辨率 320x180；建议码率（VideoCall）250kbps; 建议码率（LIVE）400kbps。 |
| TRTC_VIDEO_RESOLUTION_480_270 | 106 | 宽高比 16:9；分辨率 480x270；建议码率（VideoCall）350kbps; 建议码率（LIVE）550kbps。 |
| TRTC_VIDEO_RESOLUTION_640_360 | 108 | 宽高比 16:9；分辨率 640x360；建议码率（VideoCall）500kbps; 建议码率（LIVE）900kbps。 |
| TRTC_VIDEO_RESOLUTION_960_540 | 110 | 宽高比 16:9；分辨率 960x540；建议码率（VideoCall）850kbps; 建议码率（LIVE）1300kbps。 |
| TRTC_VIDEO_RESOLUTION_1280_720 | 112 | 宽高比 16:9；分辨率 1280x720；建议码率（VideoCall）1200kbps; 建议码率（LIVE）1800kbps。 |
| TRTC_VIDEO_RESOLUTION_1920_1080 | 114 | 宽高比 16:9；分辨率 1920x1080；建议码率（VideoCall）2000kbps; 建议码率（LIVE）3000kbps。 |

## TRTCVideoResolutionMode

#### 视频宽高比模式。

TRTCVideoResolution 中仅定义了横屏分辨率（如 640 × 360），如需使用竖屏分辨率（如360 × 640），需要同时指定 ` TRTCVideoResolutionMode ` 为 Portrait。
| 枚举 | 取值 | 描述 |
| --- | --- | --- |
| TRTC_VIDEO_RESOLUTION_MODE_LANDSCAPE | 0 | 横屏分辨率，例如：` TRTCVideoResolution_640_360 + TRTCVideoResolutionModeLandscape = 640 × 360 `。 |
| TRTC_VIDEO_RESOLUTION_MODE_PORTRAIT | 1 | 竖屏分辨率，例如：` TRTCVideoResolution_640_360 + TRTCVideoResolutionModePortrait  = 360 × 640 `。 |

## TRTCVideoStreamType

#### 视频流类型。

TRTC 内部有三种不同的视频流，分别是：
-  高清大画面：一般用来传输摄像头的视频数据。

-  低清小画面：小画面和大画面的内容相互，但是分辨率和码率都比大画面低，因此清晰度也更低。

-  辅流画面：一般用于屏幕分享，同一时间在同一个房间中只允许一个用户发布辅流视频，其他用户必须要等该用户关闭之后才能发布自己的辅流。

> **注意**
> 

> 不支持单独开启低清小画面，小画面必须依附于大画面而存在，SDK 会自动设定低清小画面的分辨率和码率。
> 

| 枚举 | 取值 | 描述 |
| --- | --- | --- |
| TRTC_VIDEO_STREAM_TYPE_BIG | 0 | 高清大画面，一般用来传输摄像头的视频数据。 |
| TRTC_VIDEO_STREAM_TYPE_SMALL | 1 | 低清小画面：小画面和大画面的内容相互，但是分辨率和码率都比大画面低，因此清晰度也更低。 |
| TRTC_VIDEO_STREAM_TYPE_SUB | 2 | 辅流画面：一般用于屏幕分享，同一时间在同一个房间中只允许一个用户发布辅流视频，其他用户必须要等该用户关闭之后才能发布自己的辅流。 |

## TRTCVideoFillMode

#### 视频画面填充模式。

如果视频显示区域的宽高比不等于视频内容的宽高比时，需要指定画面的填充模式。
| 枚举 | 取值 | 描述 |
| --- | --- | --- |
| TRTC_VIDEO_RENDER_MODE_FILL | 0 | 填充模式：即将画面内容居中等比缩放以充满整个显示区域，超出显示区域的部分将会被裁剪掉，此模式下画面可能不完整。 |
| TRTC_VIDEO_RENDER_MODE_FIT | 1 | 适应模式：即按画面长边进行缩放以适应显示区域，短边部分会被填充为黑色，此模式下图像完整但可能留有黑边。 |
| TRTC_VIDEO_RENDER_MODE_SCALE_FILL | 2 | 缩放填充模式：即无论画面的宽高比，都会被拉伸或压缩以完全填充显示区域，此模式下画面宽高比可能会被改变，导致渲染画面变形 |

## TRTCVideoRotation

#### 视频画面旋转方向。

TRTC 提供了对本地和远程画面的旋转角度设置 API，下列的旋转角度都是指顺时针方向的。
| 枚举 | 取值 | 描述 |
| --- | --- | --- |
| TRTC_VIDEO_ROTATION_0 | 0 | 不旋转。 |
| TRTC_VIDEO_ROTATION_90 | 1 | 顺时针旋转90度。 |
| TRTC_VIDEO_ROTATION_180 | 2 | 顺时针旋转180度。 |
| TRTC_VIDEO_ROTATION_270 | 3 | 顺时针旋转270度。 |

## TRTCBeautyStyle

#### 美颜（磨皮）算法。

TRTC 内置多种不同的磨皮算法，您可以选择最适合您产品定位的方案。
| 枚举 | 取值 | 描述 |
| --- | --- | --- |
| TRTC_BEAUTY_STYLE_SMOOTH | 0 | 光滑，算法比较激进，磨皮效果比较明显，适用于秀场直播。 |
| TRTC_BEAUTY_STYLE_NATURE | 1 | 自然，算法更多地保留了面部细节，磨皮效果更加自然，适用于绝大多数直播场景。 |
| TRTC_BEAUTY_STYLE_PITU | 2 | 优图，由优图实验室提供，磨皮效果介于光滑和自然之间，比光滑保留更多皮肤细节，比自然磨皮程度更高。 |

## TRTCVideoPixelFormat

#### 视频像素格式。

TRTC 提供针对视频的自定义采集和自定义渲染功能：
-  在自定义采集功能中，您可以用下列枚举值描述您采集的视频像素格式。

-  在自定义渲染功能中，您可以指定您期望 SDK 回调出的视频像素格式。

| 枚举 | 取值 | 描述 |
| --- | --- | --- |
| TRTC_VIDEO_PIXEL_FORMAT_UNKNOWN | 0 | 未定义的格式。 |
| TRTC_VIDEO_PIXEL_FORMAT_I420 | 1 | YUV420P(I420) 格式。 |
| TRTC_VIDEO_PIXEL_FORMAT_Texture_2D | 2 | OpenGL 2D 纹理格式。 |
| TRTC_VIDEO_PIXEL_FORMAT_TEXTURE_EXTERNAL_OES | 3 | OES 外部纹理格式（适用于 Android 平台）。 |
| TRTC_VIDEO_PIXEL_FORMAT_NV21 | 4 | NV21 格式。 |
| TRTC_VIDEO_PIXEL_FORMAT_RGBA | 5 | RGBA 格式。 |

## TRTCVideoBufferType

#### 视频数据传递方式。

在自定义采集和自定义渲染功能，您需要用到下列枚举值来指定您希望以什么方式传递视频数据：
-  方案一：使用内存 Buffer 传递视频数据，该方案在 iOS 效率尚可，但在 Android 系统上效率较差，Windows 暂时仅支持内存 Buffer 的传递方式。

-  方案二：使用 Texture 纹理传递视频数据，该方案在 iOS 和 Android 系统下均有较高的效率，Windows 暂不支持，需要您有一定的 OpenGL 编程基础。

| 枚举 | 取值 | 描述 |
| --- | --- | --- |
| TRTC_VIDEO_BUFFER_TYPE_UNKNOWN | 0 | 未定义的传递方式。 |
| TRTC_VIDEO_BUFFER_TYPE_BYTE_BUFFER | 1 | 使用内存 Buffer 传递视频数据，iOS：PixelBuffer；Android：用于 JNI 层的 Direct Buffer；Win：内存数据块。 |
| TRTC_VIDEO_BUFFER_TYPE_BYTE_ARRAY | 2 | 使用内存 Buffer 传递视频数据，iOS：经过一次额外整理后更加紧凑的 NSData 类型的内存块；Android：用于 JAVA 层的 byte[]。 该传递的方式的性能是几种方案中效率较差的一种。 |
| TRTC_VIDEO_BUFFER_TYPE_TEXTURE | 3 | 使用 OpengGL 纹理传递视频数据。 |

## TRTCVideoMirrorType

#### 视频的镜像类型。

视频的镜像是指对视频内容进行左右翻转，尤其是对本地的摄像头预览视频，开启镜像后能给主播带来熟悉的“照镜子”体验。
| 枚举 | 取值 | 描述 |
| --- | --- | --- |
| TRTC_VIDEO_MIRROR_TYPE_AUTO | 0 | 自动模式：如果正使用前置摄像头则开启镜像，如果是后置摄像头则不开启镜像（仅适用于移动设备）。 |
| TRTC_VIDEO_MIRROR_TYPE_ENABLE | 1 | 强制开启镜像，不论当前使用的是前置摄像头还是后置摄像头。 |
| TRTC_VIDEO_MIRROR_TYPE_DISABLE | 2 | 强制关闭镜像，不论当前使用的是前置摄像头还是后置摄像头。 |

## TRTCSnapshotSourceType

#### 本地视频截图的数据源。

SDK 支持从如下两种数据源中截取图片并保存成本地文件：
-  视频流：从视频流中截取原生的视频内容，截取的内容不受渲染控件的显示控制。

-  渲染层：从渲染控件中截取显示的视频内容，可以做到用户所见即所得的效果，但如果显示区域过小，截取出的图片也会很小。

-  采集层：从采集控件中截取采集到的视频内容，可以截取采集出来的高清截图。

| 枚举 | 取值 | 描述 |
| --- | --- | --- |
| TRTC_SNAPSHOT_SOURCE_TYPE_STREAM | 0 | 从视频流中截取原生的视频内容，截取的内容不受渲染控件的显示控制。 |
| TRTC_SNAPSHOT_SOURCE_TYPE_VIEW | 1 | 从渲染控件中截取显示的视频内容，可以做到用户所见即所得的效果，但如果显示区域过小，截取出的图片也会很小。 |
| TRTC_SNAPSHOT_SOURCE_TYPE_CAPTURE | 2 | 从采集控件中截取采集到的视频内容，可以截取采集出来的高清截图。 |

## TRTCAppScene

#### 应用场景。

TRTC 针对常见的音视频应用场景都进行了定向优化，以满足各种垂直场景下的差异化要求，主要场景可以分为如下两类：
-  直播（LIVE）场景：包括 LIVE 和 VoiceChatRoom，前者是音频+视频，后者是纯音频。

直播场景下，用户被分成“主播”和“观众”两种角色，单个房间中同时最多支持10万人在线，适合于观众人数众多的直播场景。
-  实时（RTC）场景：包括 VideoCall 和 AudioCall，前者是音频+视频，后者是纯音频。

实时场景下，用户没有角色的差异，但单个房间中同时最多支持 300 人在线，适合于小范围实时通信的场景。
| 枚举 | 取值 | 描述 |
| --- | --- | --- |
| TRTC_APP_SCENE_VIDEOCALL | 0 | 视频通话场景，支持720P、1080P高清画质，单个房间最多支持300人同时在线，最高支持50人同时发言。 适用于[1对1视频通话]、[300人视频会议]、[在线问诊]、[教育小班课]、[远程面试]等业务场景。 |
| TRTC_APP_SCENE_LIVE | 1 | 视频互动直播，支持平滑上下麦，切换过程无需等待，主播延时小于300ms；支持十万级别观众同时播放，播放延时低至1000ms。 适用于[低延时互动直播]、[大班课]、[主播PK]、[视频相亲]、[在线互动课堂]、[远程培训]、[超大型会议]等业务场景。 **注意** 此场景下，您必须通过 TRTCParams 中的 role 字段指定当前用户的角色。 |
| TRTC_APP_SCENE_AUDIOCALL | 2 | 语音通话场景，默认采用 SPEECH 音质，单个房间最多支持300人同时在线，最高支持50人同时发言。 适用于 [1对1语音通话]、[300人语音会议]、[语音聊天]、[语音会议]、[在线狼人杀] 等业务场景。 |
| TRTC_APP_SCENE_VOICE_CHATROOM | 3 | 语音互动直播，支持平滑上下麦，切换过程无需等待，主播延时小于 300ms；支持十万级别观众同时播放，播放延时低至 1000ms。 适用于 [语音俱乐部]、[在线K歌房]、[音乐直播间]、[FM电台] 等业务场景。 **注意** 此场景下，您必须通过 TRTCParams 中的 role 字段指定当前用户的角色。 |

## TRTCRoleType

#### 角色。

仅适用于直播类场景（即 TRTC_APP_SCENE_LIVE 和 TRTC_APP_SCENE_VOICE_CHATROOM），把用户区分成两种不同的身份：
-  主播：可以随时发布自己的音视频流，但人数有限制，同一个房间中最多只允许 50 个主播同时发布自己的音视频流。

-  观众：只能观看其他用户的音视频流，要发布音视频流，需要先通过 switchRole 切换成主播，同一个房间中最多能容纳10万观众。

| 枚举 | 取值 | 描述 |
| --- | --- | --- |
| TRTCRoleAnchor | 20 | 主播：可以随时发布自己的音视频流，但人数有限制，同一个房间中最多只允许 50 个主播同时发布自己的音视频流。 |
| TRTCRoleAudience | 21 | 观众：只能观看其他用户的音视频流，要发布音视频流，需要先通过 switchRole 切换成主播，同一个房间中最多能容纳10万观众。 |

## TRTCQosControlMode(Deprecated)

#### 流控模式（已废弃）。
| 枚举 | 取值 | 描述 |
| --- | --- | --- |
| VIDEO_QOS_CONTROL_CLIENT | 0 | 本地控制，用于 SDK 开发内部调试，客户请勿使用。 |
| VIDEO_QOS_CONTROL_SERVER | 1 | 云端控制，默认模式，推荐选择。 |

## TRTCVideoQosPreference

#### 画质偏好。

TRTC 在弱网络环境下有两种调控模式：“优先保证画面清晰”或“优先保证画面流畅”，两种模式均会优先保障声音数据的传输。
| 枚举 | 取值 | 描述 |
| --- | --- | --- |
| TRTC_VIDEO_QOS_PREFERENCE_SMOOTH | 1 | 流畅优先：即当前网络不足以传输既清晰又流畅的画面时，优先保证画面的流畅性，代价就是画面会比较模糊且伴随有较多的马赛克。 |
| TRTC_VIDEO_QOS_PREFERENCE_CLEAR | 2 | 清晰优先（默认值）：即当前网络不足以传输既清晰又流畅的画面时，优先保证画面的清晰度，代价就是画面会比较卡顿。 |

## TRTCQuality

#### 网络质量。

TRTC 会每隔两秒对当前的网络质量进行评估，评估结果为六个等级：Excellent 表示最好，Down 表示最差。
| 枚举 | 取值 | 描述 |
| --- | --- | --- |
| TRTC_QUALITY_UNKNOWN | 0 | 未定义。 |
| TRTC_QUALITY_Excellent | 1 | 当前网络非常好。 |
| TRTC_QUALITY_Good | 2 | 当前网络比较好。 |
| TRTC_QUALITY_Poor | 3 | 当前网络一般。 |
| TRTC_QUALITY_Bad | 4 | 当前网络较差。 |
| TRTC_QUALITY_Vbad | 5 | 当前网络很差。 |
| TRTC_QUALITY_Down | 6 | 当前网络不满足 TRTC 的最低要求。 |

## TRTCAVStatusType

#### 音视频状态类型。

该枚举类型用于音频状态变化回调接口（onRemoteAudioStatusUpdated）与视频状态变化回调接口（onRemoteVideoStatusUpdated），用于指定当前的音频或视频状态。
| 枚举 | 取值 | 描述 |
| --- | --- | --- |
| TRTCAVStatusStopped | 0 | 停止播放。 |
| TRTCAVStatusPlaying | 1 | 正在播放。 |
| TRTCAVStatusLoading | 2 | 正在加载。 |

## TRTCAVStatusChangeReason

#### 音视频状态变化原因类型。

该枚举类型用于音频状态变化回调接口（onRemoteAudioStatusUpdated）与视频状态变化回调接口（onRemoteVideoStatusUpdated），用于指定当前的音频或视频状态变化原因。
| 枚举 | 取值 | 描述 |
| --- | --- | --- |
| TRTCAVStatusChangeReasonInternal | 0 | 缺省值。 |
| TRTCAVStatusChangeReasonBufferingBegin | 1 | 网络缓冲。 |
| TRTCAVStatusChangeReasonBufferingEnd | 2 | 结束缓冲。 |
| TRTCAVStatusChangeReasonLocalStarted | 3 | 本地启动音频或视频流播放。 |
| TRTCAVStatusChangeReasonLocalStopped | 4 | 本地停止音频或视频流播放。 |
| TRTCAVStatusChangeReasonRemoteStarted | 5 | 远端音频或视频流开始（或继续）。 |
| TRTCAVStatusChangeReasonRemoteStopped | 6 | 远端音频或视频流停止（或中断）。 |

## TRTCAudioSampleRate

#### 音频采样率。

音频采样率用来衡量声音的保真程度，采样率越高保真程度越好，如果您的应用场景有音乐的存在，推荐使用 ` TRTCAudioSampleRate48000 `。
| 枚举 | 取值 | 描述 |
| --- | --- | --- |
| TRTCAudioSampleRate16000 | 16000 | 16k 采样率。 |
| TRTCAudioSampleRate32000 | 32000 | 32k 采样率。 |
| TRTCAudioSampleRate44100 | 44100 | 44.1k 采样率。 |
| TRTCAudioSampleRate48000 | 48000 | 48k采样率 |

## TRTCAudioQuality

#### 声音音质。

TRTC 提供了三种精心校调好的模式，用来满足各种垂直场景下对音质的差异化追求：
-  人声模式（Speech）：适用于以人声沟通为主的应用场景，该模式下音频传输的抗性较强，TRTC 会通过各种人声处理技术保障在弱网络环境下的流畅度最佳。

-  音乐模式（Music）：适用于对声乐要求很苛刻的场景，该模式下音频传输的数据量很大，TRTC 会通过各项技术确保音乐信号在各频段均能获得高保真的细节还原度。

-  默认模式（Default）：介于 Speech 和 Music 之间的档位，对音乐的还原度比人声模式要好，但传输数据量比音乐模式要低很多，对各种场景均有不错的适应性。

| 枚举 | 取值 | 描述 |
| --- | --- | --- |
| TRTC_AUDIO_QUALITY_SPEECH | 1 | 人声模式：单声道；编码码率：18kbps；具备几个模式中最强的网络抗性，适合语音通话为主的场景，例如在线会议，语音通话等。 |
| TRTC_AUDIO_QUALITY_DEFAULT | 2 | 默认模式：单声道；编码码率：50kbps；介于 Speech 和 Music 之间的档位，SDK 默认档位，推荐选择。 |
| TRTC_AUDIO_QUALITY_MUSIC | 3 | 音乐模式：全频带立体声；编码码率：128kbps；适合需要高保真传输音乐的场景，例如在线K歌、音乐直播等。 |

## TRTCAudioRoute

#### 音频路由（即声音的播放模式）。

音频路由，即声音是从手机的扬声器还是从听筒中播放出来，因此该接口仅适用于手机等移动端设备。

手机有两个扬声器：一个是位于手机顶部的听筒，一个是位于手机底部的立体声扬声器。
-  设置音频路由为听筒时，声音比较小，只有将耳朵凑近才能听清楚，隐私性较好，适合用于接听电话。

-  设置音频路由为扬声器时，声音比较大，不用将手机贴脸也能听清，因此可以实现“免提”的功能。

-  音频路由为有线耳机。

-  音频路由为蓝牙耳机。

-  音频路由为USB专业声卡设备。

| 枚举 | 取值 | 描述 |
| --- | --- | --- |
| TRTC_AUDIO_ROUTE_UNKNOWN | -1 | Unknown：默认的路由设备。 |
| TRTC_AUDIO_ROUTE_SPEAKER | 0 | Speakerphone：使用扬声器播放（即“免提”），扬声器位于手机底部，声音偏大，适合外放音乐。 |
| TRTC_AUDIO_ROUTE_EARPIECE | 1 | Earpiece：使用听筒播放，听筒位于手机顶部，声音偏小，适合需要保护隐私的通话场景。 |
| TRTC_AUDIO_ROUTE_WIRED_HEADSET | 2 | WiredHeadset：使用有线耳机播放。 |
| TRTC_AUDIO_ROUTE_BLUETOOTH_HEADSET | 3 | BluetoothHeadset：使用蓝牙耳机播放。 |
| TRTC_AUDIO_ROUTE_SOUND_CARD | 4 | SoundCard：使用 USB 声卡播放。 |

## TRTCReverbType

#### 声音混响模式。

该枚举值应用于设定直播场景中的混响模式，常用于秀场直播中。
| 枚举 | 取值 | 描述 |
| --- | --- | --- |
| TRTC_REVERB_TYPE_0 | 0 | 关闭混响。 |
| TRTC_REVERB_TYPE_1 | 1 | KTV。 |
| TRTC_REVERB_TYPE_2 | 2 | 小房间。 |
| TRTC_REVERB_TYPE_3 | 3 | 大会堂。 |
| TRTC_REVERB_TYPE_4 | 4 | 低沉。 |
| TRTC_REVERB_TYPE_5 | 5 | 洪亮。 |
| TRTC_REVERB_TYPE_6 | 6 | 金属声。 |
| TRTC_REVERB_TYPE_7 | 7 | 磁性。 |

## TRTCVoiceChangerType

#### 变声类型。

该枚举值应用于设定直播场景中的变声模式，常用于秀场直播中。
| 枚举 | 取值 | 描述 |
| --- | --- | --- |
| TRTC_VOICE_CHANGER_TYPE_0 | 0 | 关闭变声。 |
| TRTC_VOICE_CHANGER_TYPE_1 | 1 | 熊孩子。 |
| TRTC_VOICE_CHANGER_TYPE_2 | 2 | 萝莉。 |
| TRTC_VOICE_CHANGER_TYPE_3 | 3 | 大叔。 |
| TRTC_VOICE_CHANGER_TYPE_4 | 4 | 重金属。 |
| TRTC_VOICE_CHANGER_TYPE_5 | 5 | 感冒。 |
| TRTC_VOICE_CHANGER_TYPE_6 | 6 | 外国人。 |
| TRTC_VOICE_CHANGER_TYPE_7 | 7 | 困兽。 |
| TRTC_VOICE_CHANGER_TYPE_8 | 8 | 死肥仔。 |
| TRTC_VOICE_CHANGER_TYPE_9 | 9 | 强电流。 |
| TRTC_VOICE_CHANGER_TYPE_10 | 10 | 重机械。 |
| TRTC_VOICE_CHANGER_TYPE_11 | 11 | 空灵。 |

## TRTCSystemVolumeType

#### 系统音量类型（仅适用于移动设备）。

现代智能手机中一般都具备两套系统音量类型，即“通话音量”和“媒体音量”。
-  通话音量：手机专门为接打电话所设计的音量类型，自带回声抵消（AEC）功能，并且支持通过蓝牙耳机上的麦克风进行拾音，缺点是音质比较一般。当您通过手机侧面的音量按键下调手机音量时，如果无法将其调至零（也就是无法彻底静音），说明您的手机当前处于通话音量。

-  媒体音量：手机专门为音乐场景所设计的音量类型，无法使用系统的 AEC 功能，并且不支持通过蓝牙耳机的麦克风进行拾音，但具备更好的音乐播放效果。当您通过手机侧面的音量按键下调手机音量时，如果能够将手机音量调至彻底静音，说明您的手机当前处于媒体音量。

SDK 目前提供了三种系统音量类型的控制模式：自动切换模式、全程通话音量模式、全程媒体音量模式。
| 枚举 | 取值 | 描述 |
| --- | --- | --- |
| TRTCSystemVolumeTypeAuto | 0 | 自动切换模式： 也被称为“麦上通话，麦下媒体”，即主播上麦时使用通话音量，观众不上麦则使用媒体音量，适合在线直播场景。 如果您在 enterRoom 时选择的场景为 TRTC_APP_SCENE_LIVE 或 TRTC_APP_SCENE_VOICE_CHATROOM，SDK 会自动使用该模式。 |
| TRTCSystemVolumeTypeMedia | 1 | 全程媒体音量： 通话全程使用媒体音量，并不是非常常用的音量类型，适用于对音质要求比较苛刻的音乐场景中。 如果您的用户大都使用外接设备（例如外接声卡）为主，可以使用该模式，否则请慎用。 |
| TRTCSystemVolumeTypeVOIP | 2 | 全程通话音量： 该方案的优势在于用户在上下麦时音频模块无需切换工作模式，可以做到无缝上下麦，适合于用户需要频繁上下麦的应用场景。 如果您在 enterRoom 时选择的场景为 TRTCAppSceneVideoCall 或 TRTCAppSceneAudioCall，SDK 会自动使用该模式。 |

## TRTCAudioFrameFormat

#### 音频帧的内容格式。
| 枚举 | 取值 | 描述 |
| --- | --- | --- |
| TRTC_AUDIO_FRAME_FORMAT_PCM | 1 | PCM 格式的音频数据。 |

## TRTCAudioCapabilityType

#### 系统支持的音频能力类型（仅适用于Android设备）。

SDK 目前提供了两种系统音频能力类型是否支持的查询：低延时合唱能力、低延时耳返能力。
| 枚举 | 取值 | 描述 |
| --- | --- | --- |
| TRTCAudioCapabilityLowLatencyChorus | 1 | 低延时合唱能力。 |
| TRTCAudioCapabilityLowLatencyEarMonitor | 2 | 低延时耳返能力。 |

## TRTCAudioFrameOperationMode

#### 音频回调数据读写模式。

TRTC 提供了两种音频回调数据的操作模式。
-  读写模式（ReadWrite）：可以获取并修改回调的音频数据，默认模式。

-  只读模式（ReadOnly）：仅从回调中获取音频数据。

| 枚举 | 取值 | 描述 |
| --- | --- | --- |
| TRTC_AUDIO_FRAME_OPERATION_MODE_READWRITE | 0 | 读写模式：可以获取并修改回调的音频数据。 |
| TRTC_AUDIO_FRAME_OPERATION_MODE_READONLY | 1 | 只读模式：仅从回调中获取音频数据。 |

## TRTCLogLevel

#### Log 级别。

不同的日志等级定义了不同的详实程度和日志数量，推荐一般情况下将日志等级设置为：TRTCLogLevelInfo。
| 枚举 | 取值 | 描述 |
| --- | --- | --- |
| TRTC_LOG_LEVEL_VERBOSE | 0 | 输出所有级别的 Log。 |
| TRTC_LOG_LEVEL_DEBUG | 1 | 输出 DEBUG，INFO，WARNING，ERROR 和 FATAL 级别的 Log。 |
| TRTC_LOG_LEVEL_INFO | 2 | 输出 INFO，WARNING，ERROR 和 FATAL 级别的 Log。 |
| TRTC_LOG_LEVEL_WARN | 3 | 输出WARNING，ERROR 和 FATAL 级别的 Log。 |
| TRTC_LOG_LEVEL_ERROR | 4 | 输出ERROR 和 FATAL 级别的 Log。 |
| TRTC_LOG_LEVEL_FATAL | 5 | 仅输出 FATAL 级别的 Log。 |
| TRTC_LOG_LEVEL_NULL | 6 | 不输出任何 SDK Log。 |

## TRTCGSensorMode

#### 重力感应开关（仅适用于移动端）。

@deprecated 从v11.7版本开始，推荐使用新重力感应枚举 TRTCGravitySensorAdaptiveMode。
| 枚举 | 取值 | 描述 |
| --- | --- | --- |
| TRTC_GSENSOR_MODE_DISABLE | 0 | 不适配重力感应，该模式是桌面平台上的默认值，该模式下，当前用户发布出去的视频画面不受重力感应方向变化的影响。 |
| TRTC_GSENSOR_MODE_UIAUTOLAYOUT | 1 | 适配重力感应，该模式是移动平台上的默认值，该模式下，当前用户发布出去的视频画面会跟随设备的重力感应方向进行相应的调整，同时本地预览画面保持方向不变。 SDK 目前支持的一种适配模式是：当手机或 Pad 上下颠倒时，为了保证远端用户看到的画面方向正常，SDK 会自动将发布出去的画面上下旋转180度。如果您的 APP 的界面层开启了重力感应自适应，推荐使用 UIFixLayout 模式。 |
| TRTC_GSENSOR_MODE_UIFIXLAYOUT | 2 | 适配重力感应 该模式下，当前用户发布出去的视频画面会跟随设备的重力感应方向进行相应的调整，同时本地预览画面也会进行相应的旋转适配。 目前支持的一种特性是：当手机或 Pad 上下颠倒时，为了保证远端用户看到的画面方向正常，SDK 会自动将发布出去的画面上下旋转180度。 如果您的 APP 的界面层不支持重力感应自适应，并且希望 SDK 的视频画面能够适配重力感应方向，推荐使用 UIFixLayout 模式。 @deprecated 从v11.5版本开始，不再支持 TRTCGSensorMode_UIFixLayout，只支持上面两种模式。 |

## TRTCTranscodingConfigMode

#### 云端混流的排版模式。

TRTC 的云端混流服务能够将房间中的多路音视频流混合成一路，因此您需要指定画面的排版方案，我们提供了如下几种排版模式。
| 枚举 | 取值 | 描述 |
| --- | --- | --- |
| TRTC_TranscodingConfigMode_Unknown | 0 | 未定义。 |
| TRTC_TranscodingConfigMode_Manual | 1 | 全手动排版模式。 该模式下，您需要指定每一路画面的精确排版位置。该模式的自由度最高，但易用性也最差： -  您需要填写 TRTCTranscodingConfig 中的所有参数，包括每一路画面（TRTCMixUser）的位置坐标。 -  您需要监听 TRTCCloudListener 中的 onUserVideoAvailable 和 onUserAudioAvailable 事件回调，并根据当前房间中各个麦上用户的音视频状态不断地调整 ` mixUsers ` 参数。 |
| TRTC_TranscodingConfigMode_Template_PureAudio | 2 | 纯音频模式。 该模式适用于语音通话（AudioCall）和语音聊天室（VoiceChatRoom）等纯音频的应用场景。 -  您只需要在进入房间后，通过 setMixTranscodingConfig 接口设置一次，之后 SDK 就会自动把房间内所有上麦用户的声音混流到当前用户的直播流上。 -  您无需设置 TRTCTranscodingConfig 中的 ` mixUsers ` 参数，只需设置 ` audioSampleRate `、` audioBitrate ` 和 ` audioChannels ` 等参数即可。 |
| TRTC_TranscodingConfigMode_Template_PresetLayout | 3 | 预排版模式。 最受欢迎的排版模式，因为该模式支持您通过占位符提前对各路画面的位置进行设定，之后 SDK 会自动根据房间中画面的路数动态进行适配调整。 此模式下，您依然需要设置 mixUsers 参数，但可以将 userId 设置为“占位符”，可选的占位符有： -  "$PLACE_HOLDER_REMOTE$"     :  指代远程用户的画面，可以设置多个。 -  "$PLACE_HOLDER_LOCAL_MAIN$" ： 指代本地摄像头画面，只允许设置一个。 -  "$PLACE_HOLDER_LOCAL_SUB$"  :  指代本地屏幕分享画面，只允许设置一个。 此模式下，您不需要监听 TRTCCloudListener 中的 onUserVideoAvailable 和 onUserAudioAvailable 回调进行实时调整，只需要在进房成功后调用一次 setMixTranscodingConfig 即可，之后 SDK 会自动将真实的 userId 补位到您设置的占位符上。 |
| TRTC_TranscodingConfigMode_Template_ScreenSharing | 4 | 屏幕分享模式。 适用于在线教育场景等以屏幕分享为主的应用场景，仅支持 Windows 和 Mac 两个平台的 SDK。 该模式下，SDK 会先根据您通过 videoWidth 和 videoHeight 参数设置的目标分辨率构建一张画布， -  当老师未开启屏幕分享时，SDK 会将老师的摄像头画面等比例拉伸绘制到该画布上； -  当老师开启屏幕分享之后，SDK 会将屏幕分享画面绘制到同样的画布上。 此种排版模式的目的是为了确保混流模块的输出分辨率一致，避免课程回放和网页观看的花屏问题（网页播放器不支持可变分辨率）。 同时，连麦学生的声音也会被默认混合到老师的音视频流中。 由于教学模式下的视频内容以屏幕分享为主，因此同时传输摄像头画面和屏幕分享画面是非常浪费带宽的。 推荐的做法是直接将摄像头画面通过 setLocalVideoRenderCallback 接口自定义绘制到当前屏幕上。 在该模式下，您无需设置 TRTCTranscodingConfig 中的 ` mixUsers ` 参数，SDK 不会混合学生的画面，以免干扰屏幕分享的效果。 您可以将 TRTCTranscodingConfig 中的 width x height 设为 0px × 0px，SDK 会自动根据用户当前屏幕的宽高比计算出一个合适的分辨率： -  如果老师当前屏幕宽度 <= 1920px，SDK 会使用老师当前屏幕的实际分辨率。 -  如果老师当前屏幕宽度 >  1920px，SDK 会根据当前屏幕宽高比，选择 1920x1080(16:9)、1920x1200(16:10)、1920x1440(4:3) 三种分辨率中的一种。 |

## TRTCRecordType

#### 媒体录制类型。

该枚举类型用于本地媒体录制接口 startLocalRecording，用于指定是录制音视频文件还是纯音频文件。
| 枚举 | 取值 | 描述 |
| --- | --- | --- |
| TRTC_RECORD_TYPE_AUDIO | 0 | 仅录制音频。 |
| TRTC_RECORD_TYPE_VIDEO | 1 | 仅录制视频。 |
| TRTC_RECORD_TYPE_BOTH | 2 | 同时录制音频和视频。 |

## TRTCMixInputType

#### 混流输入类型。
| 枚举 | 取值 | 描述 |
| --- | --- | --- |
| TRTC_MixInputType_Undefined | 0 | 默认值，考虑到针对老版本的兼容性，如果您指定了 inputType 为 Undefined，SDK 会根据另一个参数 pureAudio 的数值决定混流输入类型。 |
| TRTC_MixInputType_AudioVideo | 1 | 混入音频和视频。 |
| TRTC_MixInputType_PureVideo | 2 | 只混入视频。 |
| TRTC_MixInputType_PureAudio | 3 | 只混入音频。 |
| TRTC_MixInputType_Watermark | 4 | 混入水印，此时您无需指定 userId 字段，但需要指定 image 字段，推荐使用 png 格式的图片。 |

## TRTCDebugViewLevel

#### 用于渲染控件上展示的调试信息。
| 枚举 | 取值 | 描述 |
| --- | --- | --- |
| TRTC_DEBUG_VIEW_LEVEL_GONE | 0 | 不在渲染控件上展示调试信息。 |
| TRTC_DEBUG_VIEW_LEVEL_STATUS | 1 | 在渲染控件上展示音视频统计信息。 |
| TRTC_DEBUG_VIEW_LEVEL_ALL | 2 | 在渲染控件上展示音视频统计信息和关键历史事件。 |

## TRTCAudioRecordingContent

#### 音频录制内容类型。

该枚举类型用于音频录制接口 startAudioRecording，用于指定录制音频的内容。
| 枚举 | 取值 | 描述 |
| --- | --- | --- |
| TRTC_AudioRecordingContent_All | 0 | 录制本地和远端所有音频。 |
| TRTC_AudioRecordingContent_Local | 1 | 仅录制本地音频。 |
| TRTC_AudioRecordingContent_Remote | 2 | 仅录制远端音频。 |

## TRTCPublishMode

#### 媒体流发布模式。

该枚举类型用于媒体流发布接口 startPublishMediaStream TRTC 的媒体流发布服务能够将房间中的多路音视频流混合成一路发布至 CDN 或者回推到房间内，也可以将您当前的这路音视频发布到腾讯或者第三方 CDN 因此您需要指定对应媒体流的发布模式，我们提供了如下几种模式。
| 枚举 | 取值 | 描述 |
| --- | --- | --- |
| TRTC_PublishMode_Unknown | 0 | 未定义。 |
| TRTC_PublishBigStream_ToCdn | 1 | 您可以通过设置该参数将您房间内的主路流（TRTC_VIDEO_STREAM_TYPE_BIG）发布到腾讯或者第三方直播 CDN 服务商（仅支持标准 RTMP 协议）。 |
| TRTC_PublishSubStream_ToCdn | 2 | 您可以通过设置该参数将您房间内的辅路流（TRTC_VIDEO_STREAM_TYPE_SUB）发布到腾讯或者第三方直播 CDN 服务商（仅支持标准 RTMP 协议）。 |
| TRTC_PublishMixStream_ToCdn | 3 | 您可以通过设置该参数，配合编码输出参数 (TRTCStreamEncoderParam) 和混流转码参数 (TRTCStreamMixingConfig)，将您指定的多路音视频流进行转码并发布到腾讯或者第三方直播 CDN 服务商（仅支持标准 RTMP 协议）。 |
| TRTC_PublishMixStream_ToRoom | 4 | 您可以通过设置该参数，配合媒体流编码输出参数 (TRTCStreamEncoderParam) 和混流转码参数 (TRTCStreamMixingConfig)，将您指定的多路音视频流进行转码并发布到您指定的房间中。 -  通过 TRTCPublishTarget 中的 TRTCUser 进行指定回推房间的机器人信息。 |

## TRTCEncryptionAlgorithm

#### 加密算法。

该枚举类型用于媒体流私有加密算法选择。
| 枚举 | 取值 | 描述 |
| --- | --- | --- |
| TRTC_EncryptionAlgorithm_Aes_128_Gcm | 0 | AES GCM 128。 |
| TRTC_EncryptionAlgorithm_Aes_256_Gcm | 1 | AES GCM 256。 |

## TRTCSpeedTestScene

#### 测速场景。

该枚举类型用于测速场景选择。
| 枚举 | 取值 | 描述 |
| --- | --- | --- |
| TRTC_SpeedTestScene_Delay_Testing | 1 | 延迟测试。 |
| TRTC_SpeedTestScene_Delay_Bandwidth_Testing | 2 | 延迟与带宽测试。 |
| TRTC_SpeedTestScene_Online_Chorus_Testing | 3 | 在线合唱测试。 |

## TRTCGravitySensorAdaptiveMode

#### 设置重力感应的适配模式（仅适用于移动端）。

v11.7版本开始支持，只在sdk内部摄像头采集场景生效
| 枚举 | 取值 | 描述 |
| --- | --- | --- |
| TRTC_GRAVITY_SENSOR_ADAPTIVE_MODE_DISABLE | 0 | 关闭重力感应，根据当前采集分辨率与设置的编码分辨率决策，如果两者不一致，则通过旋转90度，保证最大画幅。 |
| TRTC_GRAVITY_SENSOR_ADAPTIVE_MODE_FILL_BY_CENTER_CROP | 1 | 开启重力感应，始终保证远端画面图像为正，中间过程需要处理分辨率不一致时，采用居中裁剪模式。 |
| TRTC_GRAVITY_SENSOR_ADAPTIVE_MODE_FIT_WITH_BLACK_BORDER | 2 | 开启重力感应，始终保证远端画面图像为正，中间过程需要处理分辨率不一致时，采用叠加黑边模式。 |

## TRTCParams

#### 进房参数。

作为 TRTC SDK 的进房参数，只有该参数填写正确，才能顺利进入 roomId 或者 strRoomId 所指定的音视频房间。

由于历史原因，TRTC 支持数字和字符串两种类型的房间号，分别是 roomId 和 strRoomId。

请注意：不要混用 roomId 和 strRoomId，因为它们之间是不互通的，例如数字 123 和字符串 “123” 在 TRTC 看来是两个完全不同的房间。
| 枚举类型 | 描述 |
| --- | --- |
| businessInfo | 【字段含义】业务数据字段（选填），部分高级特性才需要用到此字段。 【推荐取值】请不要自行设置该字段。 |
| privateMapKey | 【字段含义】用于权限控制的权限票据（选填），当您希望某个房间只能让特定的 userId 进入时，需要使用 privateMapKey 进行权限保护。 【推荐取值】仅建议有高级别安全需求的客户使用，更多详情请参见 [进房权限保护](https://cloud.tencent.com/document/product/647/32240)。 |
| role | 【字段含义】直播场景下的角色，仅适用于直播场景（TRTC_APP_SCENE_LIVE 和 TRTC_APP_SCENE_VOICE_CHATROOM），通话场景下指定该参数是无效的。 【推荐取值】默认值：主播（TRTCRoleAnchor）。 |
| roomId | 【字段含义】数字房间号，在同一个房间里的用户（userId）可以彼此看到对方并进行音视频通话。 【推荐取值】取值范围：1 - 4294967294。 【特别说明】1. roomId 与 strRoomId 是互斥的，若您选用 strRoomId，则 roomId 需要填写为 0。若两者都填，SDK 将优先选用 roomId。 2. 不要混用 roomId 和 strRoomId，因为它们之间是不互通的，例如数字 123 和字符串 ` 123 ` 在 TRTC 看来是两个完全不同的房间。 |
| sdkAppId | 【字段含义】应用标识（必填），腾讯云基于 sdkAppId 完成计费统计。 【推荐取值】在 [实时音视频控制台](https://console.cloud.tencent.com/rav/) 创建应用后可以在账号信息页面中得到该 ID。 |
| strRoomId | 【字段含义】字符串房间号，在同一个房间里的用户（userId）可以彼此看到对方并进行音视频通话。 【推荐取值】限制长度为 64 字节。以下为支持的字符集范围（共 89 个字符）: -  大小写英文字母（a-zA-Z）； -  数字（0-9）； -  空格、` ! `、` # `、` $ `、` % `、` & `、` ( `、` ) `、` + `、` - `、` : `、` ; `、` < `、` = `、` . `、` > `、` ? `、` @ `、` [ `、` ] `、` ^ `、` _ `、` { `、` } `、` \\| `、` ~ `、` , `。 【特别说明】1. roomId 与 strRoomId 是互斥的，若您选用 strRoomId，则 roomId 需要填写为0。若两者都填，SDK 将优先选用 roomId。 2. 不要混用 roomId 和 strRoomId，因为它们之间是不互通的，例如数字 123 和字符串 ` 123 ` 在 TRTC 看来是两个完全不同的房间。 |
| streamId | 【字段含义】用于指定在腾讯云直播平台上的 streamId（选填），设置之后，您可以在腾讯云直播 CDN 上通过标准拉流方案（FLV 或 HLS）播放该用户的音视频流。 【推荐取值】限制长度为64字节，可以不填写，一种推荐的方案是使用 ` sdkappid_roomid_userid_main ` 作为 streamid，这种命名方式容易辨认且不会在您的多个应用中发生冲突。 【特殊说明】要使用腾讯云直播 CDN，您需要先在 [控制台](https://console.cloud.tencent.com/trtc/) 中的功能配置页开启“启动自动旁路直播”开关。 【参考文档】[发布音视频流到直播 CDN](https://cloud.tencent.com/document/product/647/84721)。 |
| userDefineRecordId | 【字段含义】云端录制开关（选填），用于指定是否要在云端将该用户的音视频流录制下来。 【参考文档】[云端录制](https://cloud.tencent.com/document/product/647/76497)。 【推荐取值】限制长度为64字节，只允许包含大小写英文字母（a-zA-Z）、数字（0-9）及下划线和连词符。 方案一：手动录制方案： 1. 在 [控制台](https://console.cloud.tencent.com/trtc)>应用管理>云端录制配置 中开启云端录制。 2. 设置 ` 录制形式 ` 为 ` 手动录制 `。 3. 设置手动录制后，在一个 TRTC 房间中只有设置了 userDefineRecordId 参数的用户才会在云端录制出视频文件，不指定该参数的用户不会产生录制行为。 4. 云端会以 “userDefineRecordId_起始时间_结束时间” 的格式命名录制下来的文件。 方案二：自动录制方案： 1. 需要在 [控制台](https://console.cloud.tencent.com/trtc)>应用管理>云端录制配置 中开启云端录制。 2. 设置` 录制形式 `为` 自动录制 `。 3. 设置自动录制后，在一个 TRTC 房间中的任何一个有音视频上行的用户，均会在云端录制出视频文件。 4. 文件会以 ` userDefineRecordId_起始时间_结束时间 ` 的格式命名，如果不指定 userDefineRecordId，则文件会以 ` streamId_起始时间_结束时间 ` 命名。 |
| userId | 【字段含义】用户标识（必填），当前用户的 userId，相当于用户名，使用 UTF-8 编码。 【推荐取值】如果一个用户在您的账号系统中的 ID 为 “mike”，则 userId 即可设置为 “mike”。 |
| userSig | 【字段含义】用户签名（必填），当前 userId 对应的验证签名，相当于使用云服务的登录密码。 【推荐取值】具体计算方法请参见 [如何计算UserSig](https://cloud.tencent.com/document/product/647/17275)。 |

## TRTCVideoEncParam

#### 视频编码参数。

该设置决定远端用户看到的画面质量，同时也决定了云端录制出的视频文件的画面质量。
| 枚举类型 | 描述 |
| --- | --- |
| enableAdjustRes | 【字段含义】是否允许动态调整分辨率（开启后会对云端录制产生影响）。 【推荐取值】该功能适用于不需要云端录制的场景，开启后 SDK 会根据当前网络情况，智能选择出一个合适的分辨率，避免出现“大分辨率+小码率”的低效编码模式。 【特别说明】默认值：关闭。如有云端录制的需求，请不要开启此功能，因为如果视频分辨率发生变化后，云端录制出的 MP4 在普通的播放器上无法正常播放。 |
| minVideoBitrate | 【字段含义】最低视频码率，SDK 会在网络不佳的情况下主动降低视频码率以保持流畅度，最低会降至 minVideoBitrate 所设定的数值。 【特别说明】 默认值：0，此时最低码率由 SDK 会根据您指定的分辨率，自动计算出合适的数值。 【推荐取值】您可以通过同时设置 videoBitrate 和 minVideoBitrate 两个参数，用于约束 SDK 对视频码率的调整范围： -  如果您追求` 弱网络下允许卡顿但要保持清晰 `的效果，可以设置 minVideoBitrate 为 videoBitrate 的 60%。 -  如果您追求` 弱网络下允许模糊但要保持流畅 `的效果，可以设置 minVideoBitrate 为一个较低的数值（例如 100kbps）。 -  如果您将 videoBitrate 和 minVideoBitrate 设置为同一个值，等价于关闭 SDK 对视频码率的自适应调节能力。 |
| videoBitrate | 【字段含义】目标视频码率，SDK 会按照目标码率进行编码，只有在弱网络环境下才会主动降低视频码率。 【推荐取值】请参见本 TRTCVideoResolution 在各档位注释的最佳码率，也可以在此基础上适当调高。例如：TRTCVideoResolution_1280_720 对应 1200kbps 的目标码率，您也可以设置为 1500kbps 用来获得更好的观感清晰度。 【特别说明】您可以通过同时设置 videoBitrate 和 minVideoBitrate 两个参数，用于约束 SDK 对视频码率的调整范围： -  如果您追求“弱网络下允许卡顿但要保持清晰”的效果，可以设置 minVideoBitrate 为 videoBitrate 的 60%。 -  如果您追求“弱网络下允许模糊但要保持流畅”的效果，可以设置 minVideoBitrate 为一个较低的数值（例如 100kbps）。 -  如果您将 videoBitrate 和 minVideoBitrate 设置为同一个值，等价于关闭 SDK 对视频码率的自适应调节能力。 |
| videoFps | 【字段含义】视频采集帧率。 【推荐取值】15fps或20fps。5fps以下，卡顿感明显。10fps以下，会有轻微卡顿感。20fps以上，会浪费带宽（电影的帧率为24fps）。 【特别说明】部分 Android 手机的前置摄像头并不支持15fps以上的采集帧率，部分主打美颜功能的 Android 手机的前置摄像头的采集帧率可能低于10fps。 |
| videoResolution | 【字段含义】视频分辨率。 【特别说明】如需使用竖屏分辨率，请指定 resMode 为 Portrait，例如： ` 640 × 360 + Portrait = 360 × 640 `。 【推荐取值】 -  手机视频通话：建议选择 360 × 640 及以下分辨率，resMode 选择 Portrait，即竖屏分辨率。 -  手机在线直播：建议选择 540 × 960，resMode 选择 Portrait，即竖屏分辨率。 -  桌面平台（Win + Mac）：建议选择 640 × 360 及以上分辨率，resMode 选择 Landscape，即横屏分辨率。 |
| videoResolutionMode | 【字段含义】分辨率模式（横屏分辨率 or 竖屏分辨率）。 【推荐取值】手机平台（iOS、Android）建议选择 Portrait，桌面平台（Windows、Mac）建议选择 Landscape。 【特别说明】如需使用竖屏分辨率，请指定 resMode 为 Portrait，例如： ` 640 × 360 + Portrait = 360 × 640 `。 |

## TRTCNetworkQosParam

#### 网络流控（Qos）参数集。

网络流控相关参数，该设置决定 SDK 在弱网络环境下的调控策略（例如：“清晰优先”或“流畅优先”）。
| 枚举类型 | 描述 |
| --- | --- |
| controlMode | 【字段含义】流控模式（已废弃）。 【推荐取值】云端控制。 【特别说明】请设置为云端控制模式（TRTCQosControlModeServer）。 |
| preference | 【字段含义】清晰优先还是流畅优先。 【推荐取值】清晰优先。 【特别说明】该参数主要影响 TRTC 在较差网络环境下的音视频表现： -  流畅优先：即当前网络不足以传输既清晰又流畅的画面时，优先保证画面的流畅性，代价就是画面会比较模糊且伴随有较多的马赛克。参见 TRTC_VIDEO_QOS_PREFERENCE_SMOOTH -  清晰优先（默认值）：即当前网络不足以传输既清晰又流畅的画面时，优先保证画面的清晰度，代价就是画面会比较卡顿。参见 TRTC_VIDEO_QOS_PREFERENCE_CLEAR |

## TRTCRenderParams

#### 视频画面的渲染参数。

您可以通过设置此参数来控制画面的旋转角度、填充模式和左右镜像模式。
| 枚举类型 | 描述 |
| --- | --- |
| fillMode | 【字段含义】画面填充模式。 【推荐取值】填充（画面可能会被拉伸裁剪）或适应（画面可能会有黑边），默认值：TRTC_VIDEO_RENDER_MODE_FILL。 |
| mirrorType | 【字段含义】画面镜像模式。 【推荐取值】默认值：TRTC_VIDEO_MIRROR_TYPE_AUTO。 |
| rotation | 【字段含义】图像的顺时针旋转角度。 【推荐取值】支持 90、180 以及 270 旋转角度，默认值：TRTC_VIDEO_ROTATION_0。 |

## TRTCQualityInfo

#### 网络质量。

表征网络质量的好坏，您可以通过该数值在用户界面上展示每个用户的网络质量。
| 枚举类型 | 描述 |
| --- | --- |
| quality | 网络质量 |
| userId | 用户 ID |

## TRTCVolumeInfo

#### 音量大小。

表征语音音量的评估值，您可以通过该数值在用户界面上展示每个用户的音量大小。
| 枚举类型 | 描述 |
| --- | --- |
| pitch | 本地用户的人声频率（单位：Hz），取值范围[0 - 4000]，对于远端用户，该值始终为0。 |
| spectrumData | 音频频谱数据是将音频数据在频率域中的分布，划分为 256 个频率段，使用 spectrumData 记录各个频率段的能量值，每个能量值的取值范围为 [-300, 0]，单位为 dBFS。 **注意** 本地频谱使用编码前的音频数据计算，会受到本地采集音量、BGM等影响；远端频谱使用接收到的音频数据计算，本地调整远端播放音量等操作不会对其产生影响。 |
| userId | 说话者的 userId, 如果 userId 为空则代表是当前用户自己。 |
| vad | 是否检测到人声，0：非人声 1：人声。 |
| volume | 说话者的音量大小, 取值范围[0 - 100]。 |

## TRTCSpeedTestParams

#### 测速参数。

您可以在用户进入房间前通过 startSpeedTest 接口测试网速（注意：请不要在通话中调用）。
| 枚举类型 | 描述 |
| --- | --- |
| expectedDownBandwidth | 预期的下行带宽（kbps，取值范围：[10, 5000]，为 0 时不测试）。 **注意** 当参数 scene 设置为 TRTC_SpeedTestScene_Online_Chorus_Testing 时，为了获取更准确的 ` rtt / jitter ` 等信息，取值范围限制为 [10, 1000]。 |
| expectedUpBandwidth | 预期的上行带宽（kbps，取值范围： [10, 5000]，为 0 时不测试）。 **注意** 当参数 scene 设置为 TRTC_SpeedTestScene_Online_Chorus_Testing 时，为了获取更准确的 ` rtt / jitter ` 等信息，取值范围限制为 [10, 1000]。 |
| scene | 测速场景。 |
| sdkAppId | 应用标识，请参见 TRTCParams 中的相关说明。 |
| userId | 用户标识，请参见 TRTCParams 中的相关说明。 |
| userSig | 用户签名，请参见 TRTCParams 中的相关说明。 |

## TRTCSpeedTestResult

#### 网络测速结果。

您可以在用户进入房间前通过 startSpeedTest 接口进行测速（注意：请不要在通话中调用）。
| 枚举类型 | 描述 |
| --- | --- |
| availableDownBandwidth | 下行带宽（kbps，-1：无效值）。 |
| availableUpBandwidth | 上行带宽（kbps，-1：无效值）。 |
| downJitter | 下行数据包抖动（ms)，指用户当前网络环境下数据通信的稳定性，该值越小越好，正常数值范围是 [0, 100]，-1 代表此次测速没有成功测得有效值，一般情况下 Wi-Fi 网络的 Jitter 会比 4G/5G 环境稍大。 |
| downLostRate | 下行丢包率，取值范围是 [0 - 1.0]，例如 0.2 表示每从服务器收取 10 个数据包可能会在中途丢失 2 个。 |
| errMsg | 带宽测试错误信息。 |
| ip | 服务器 IP 地址。 |
| quality | 内部通过评估算法测算出的网络质量，更多信息请参见 TRTCQuality。 |
| rtt | 延迟（毫秒），指当前设备到 TRTC 服务器的一次网络往返时间，该值越小越好，正常数值范围是10ms - 100ms。 |
| success | 测试是否成功。 |
| upJitter | 上行数据包抖动（ms)，指用户当前网络环境下数据通信的稳定性，该值越小越好，正常数值范围是 [0, 100]，-1 代表此次测速没有成功测得有效值，一般情况下 Wi-Fi 网络的 Jitter 会比 4G/5G 环境稍大。 |
| upLostRate | 上行丢包率，取值范围是 [0 - 1.0]，例如 0.3 表示每向服务器发送 10 个数据包可能会在中途丢失 3 个。 |

## TRTCTexture

#### 视频纹理数据。
| 枚举类型 | 描述 |
| --- | --- |
| eglContext10 | 【字段含义】使用 (javax.microedition.khronos.egl.*) 定义的 OpenGL 上下文环境。 |
| eglContext14 | 【字段含义】使用 (android.opengl.*) 定义的 OpenGL 上下文环境。 |
| textureId | 【字段含义】视频纹理 ID。 |

## TRTCVideoFrame

#### 视频帧信息。

TRTCVideoFrame 用来描述一帧视频画面的裸数据，也就是编码前或者解码后的视频画面数据。
| 枚举类型 | 描述 |
| --- | --- |
| buffer | 【字段含义】bufferType 为 TRTCCloudDef#TRTC_VIDEO_BUFFER_TYPE_BYTE_BUFFER 时的视频数据，承载用于 JNI 层的 Direct Buffer。 |
| bufferType | 【字段含义】视频数据结构类型。 |
| data | 【字段含义】bufferType 为 TRTCCloudDef#TRTC_VIDEO_BUFFER_TYPE_BYTE_ARRAY 时的视频数据，承载用于 java 层的字节数组。 |
| height | 【字段含义】视频高度。 |
| pixelFormat | 【字段含义】视频的像素格式。 |
| rotation | 【字段含义】视频像素的顺时针旋转角度。 |
| texture | 【字段含义】bufferType 为 TRTCCloudDef#TRTC_VIDEO_BUFFER_TYPE_TEXTURE 时的视频数据，承载用于 OpenGL 渲染的纹理数据。 |
| timestamp | 【字段含义】视频帧的时间戳，单位毫秒。 【推荐取值】自定义视频采集时可以设置为0。若该参数为0，SDK 会自定填充 timestamp 字段，但请“均匀”地控制 sendCustomVideoData 的调用间隔。 |
| width | 【字段含义】视频宽度。 |

## TRTCAudioFrame

#### 音频帧数据。
| 枚举类型 | 描述 |
| --- | --- |
| channel | 【字段含义】声道数。 |
| data | 【字段含义】音频数据。 |
| extraData | 【字段含义】音频额外数据，远端用户通过 onLocalProcessedAudioFrame 写入的数据会通过该字段回调。 |
| sampleRate | 【字段含义】采样率。 |
| timestamp | 【字段含义】时间戳，单位ms。 |

## TRTCMixUser

#### 云端混流中各路画面的描述信息。

TRTCMixUser 用于指定云端混流中每一路视频画面的位置、大小、图层以及流类型等信息。
| 枚举类型 | 描述 |
| --- | --- |
| height | 【字段含义】指定该路画面的高度（单位：像素）。 |
| image | 【字段含义】占位图或水印图 -  占位图是指当对应 userId 混流内容为纯音频时，混合后的画面中显示的是占位图片。 -  水印图是指一张贴在混合后画面中的半透明图片，这张图片会一直覆盖于混合后的画面上。 -  当指定 inputType 为 TRTC_MixInputType_PureAudio 时，image 为占位图，此时需要您指定 userId。 -  当指定 inputType 为 TRTCCloudDef.TRTC_MixInputType_Watermark 时，image 为水印图，此时不需要您指定 userId。 【推荐取值】默认值：空值，即不设置占位图或者水印图。 【特别说明】 -  您可以将 image 设置为控制台中的某一个素材 ID，这需要您事先在 “[控制台](https://console.cloud.tencent.com/trtc) => 应用管理 => 功能配置 => 素材管理” 中单击 [新增图片] 按钮进行上传。 -  上传成功后可以获得对应的“图片ID”，然后将“图片ID”转换成字符串类型并设置给 image 字段即可（例如假设“图片ID” 为 63，可以设置 image = @"63"）。 -  您也可以将 image 设置为图片的 URL 地址，腾讯云的后台服务器会将该 URL 地址指定的图片混合到最终的画面中。 -  URL 链接长度限制为 512 字节。图片大小限制不超过 2MB。 -  图片格式支持 png、jpg、jpeg、bmp 格式，推荐使用 png 格式的半透明图片作为水印。 -  image 仅在 inputType 为 TRTC_MixInputType_PureAudio 或者 TRTCCloudDef.TRTC_MixInputType_Watermark 时才生效。 |
| inputType | 【字段含义】指定该路流的混合内容（只混音频、只混视频、混合音视频、混入水印）。 【默认取值】默认值：TRTC_MixInputType_Undefined。 【特别说明】 -  当指定 inputType 为 TRTC_MixInputType_Undefined 并设置 pureAudio 为 YES 时，等效于设置 inputType 为 TRTC_MixInputType_PureAudio。 -  当指定 inputType 为 TRTC_MixInputType_Undefined 并设置 pureAudio 为 NO 时，等效于设置 inputType 为 TRTC_MixInputType_AudioVideo。 -  当指定 inputType 为 TRTCCloudDef.TRTC_MixInputType_Watermark 时，您可以不指定 userId 字段，但需要指定 image 字段。 |
| pureAudio | 【字段含义】指定该路流是不是只混合声音。 【推荐取值】默认值：false。 【特别说明】已废弃，推荐使用8.5版本开始新引入的字段：inputType。 |
| renderMode | 【字段含义】该画面在输出时的显示模式。 【推荐取值】默认值：视频流默认为0。0为裁剪，1为缩放，2为缩放并显示黑底。 【特别说明】水印图和占位图暂时不支持设置 renderMode，默认强制拉伸处理。 |
| roomId | 【字段含义】该路音视频流所在的房间号（设置为空值代表当前用户所在的房间号）。 |
| soundLevel | 【字段含义】该路音频参与混音时的音量等级（取值范围：[0, 100]）。 【默认取值】默认值：100。 |
| streamType | 【字段含义】指定该路画面是主路画面（TRTC_VIDEO_STREAM_TYPE_BIG）还是辅路画面（TRTC_VIDEO_STREAM_TYPE_SUB）。 |
| userId | 【字段含义】用户 ID |
| width | 【字段含义】指定该路画面的宽度（单位：像素）。 |
| x | 【字段含义】指定该路画面的 x 坐标（单位：像素）。 |
| y | 【字段含义】指定该路画面的 y 坐标（单位：像素）。 |
| zOrder | 【字段含义】指定该路画面的层级（取值范围：[1, 15]，不可重复）。 |

## TRTCTranscodingConfig

#### 云端混流的排版布局和转码参数。

用于指定混流时各路画面的排版位置信息和云端转码的编码参数。
| 枚举类型 | 描述 |
| --- | --- |
| appId | 【字段含义】腾讯云直播服务的 AppID。 【推荐取值】请在 [实时音视频控制台](https://console.cloud.tencent.com/trtc) 依次单击【应用管理】=>【应用信息】，并在【旁路直播信息】中获取 appid。 【特别说明】2020年01月09日及此后新建的应用无需再填写该字段。 |
| audioBitrate | 【字段含义】指定云端转码的目标音频码率。 【推荐取值】默认值：64kbps，取值范围是 [32，192]。 |
| audioChannels | 【字段含义】指定云端转码的音频声道数。 【推荐取值】默认值：1，代表单声道。可设定的数值只有两个数字：1-单声道，2-双声道。 |
| audioCodec | 【字段含义】指定云端转码的输出流音频编码类型。 【推荐取值】默认值：0，代表LC-AAC。可设定的数值只有三个数字：0 - LC-AAC，1 - HE-AAC，2 - HE-AACv2。 【特别说明】HE-AAC 和 HE-AACv2 支持的输出流音频采样率范围为[48000, 44100, 32000, 24000, 16000]。 【特别说明】当音频编码设置为 HE-AACv2 时，只支持输出流音频声道数为双声道。 【特别说明】HE-AAC 和 HE-AACv2 取值仅在输出流为您额外设置的 streamId 上时才生效。 |
| audioSampleRate | 【字段含义】指定云端转码的目标音频采样率。 【推荐取值】默认值：48000Hz。支持12000Hz、16000Hz、22050Hz、24000Hz、32000Hz、44100Hz、48000Hz。 |
| backgroundColor | 【字段含义】指定混合画面的底色颜色。 【推荐取值】默认值：0x000000 代表黑色。格式为十六进制数字，例如：“0x61B9F1” 代表 RGB 分别为(97,158,241)。 |
| backgroundImage | 【字段含义】指定混合画面的背景图片。 【推荐取值】默认值：空值，即不设置背景图片。 【特别说明】 -  您可以将 image 设置为控制台中的某一个素材 ID，这需要您事先在 “[控制台](https://console.cloud.tencent.com/trtc) => 应用管理 => 功能配置 => 素材管理” 中单击 [新增图片] 按钮进行上传。 -  上传成功后可以获得对应的“图片ID”，然后将“图片ID”转换成字符串类型并设置给 image 字段即可（例如假设“图片ID” 为 63，可以设置 image = @"63"）。 -  您也可以将 image 设置为图片的 URL 地址，腾讯云的后台服务器会将该 URL 地址指定的图片混合到最终的画面中。 -  URL 链接长度限制为 512 字节。图片大小限制不超过 2MB。 -  图片格式支持 png、jpg、jpeg、bmp 格式。 |
| bizId | 【字段含义】腾讯云直播服务的 bizid。 【推荐取值】请在 [实时音视频控制台](https://console.cloud.tencent.com/trtc) 依次单击【应用管理】=>【应用信息】，并在【旁路直播信息】中获取 bizid。 【特别说明】2020年01月09日及此后新建的应用无需再填写该字段。 |
| mixUsers | 【字段含义】指定云端混流中每一路视频画面的位置、大小、图层以及流类型等信息。 【推荐取值】该字段是一个 TRTCMixUser 类型的数组，数组中的每一个元素都用来代表每一路画面的信息。 |
| mode | 【字段含义】排版模式。 【推荐取值】请根据您的业务场景要求自行选择，预排版模式是适用性较好的一种模式。 |
| streamId | 【字段含义】输出到 CDN 上的直播流 ID。 【推荐取值】默认值：空值，即房间里的多路音视频流最终会混合到接口调用者的那一路音视频流上。 -  如不设置该参数，SDK 会执行默认逻辑，即房间里的多路音视频流会混合到该接口调用者的那一路音视频流上，也就是 A + B => A。 -  如您设置该参数，SDK 会将房间里的多路音视频流混合到您指定的直播流上，也就是 A + B => C（C 代表您指定的 streamId）。 |
| videoBitrate | 【字段含义】指定云端转码的目标视频码率（kbps）。 【推荐取值】如果填0，TRTC 会根据 videoWidth 和 videoHeight 估算出一个合理的码率值，您也可以参考视频分辨率枚举定义中所推荐的码率值（见注释部分）。 |
| videoFramerate | 【字段含义】指定云端转码的目标视频帧率（FPS）。 【推荐取值】默认值：15fps，取值范围是 (0,30]。 |
| videoGOP | 【字段含义】指定云端转码的目标视频关键帧间隔（GOP）。 【推荐取值】默认值：2，单位为秒，取值范围是 [1,8]。 |
| videoHeight | 【字段含义】指定云端转码的目标分辨率（高度）。 【推荐取值】单位：像素值，推荐值：640，如果您只混合音频流，请将 width 和 height 均设置为 0，否则混流转码后的直播流中会有黑色背景。 |
| videoSeiParams | 【字段含义】混流 SEI 参数，默认不填写。 【特别说明】参数以 json 字符串形式传入，示例如下： `{` `  "payLoadContent":"xxx",` `  "payloadType":5,` `  "payloadUuid":"1234567890abcdef1234567890abcdef",` `  "interval":1000,` `  "followIdr":false` `}` 当前支持的字段及含义： -  payloadContent: 必填。透传 sei 的 payload 内容，不能为空； -  payloadType: 必填。sei 消息的类型，取值范围: 5 或 [100, 254] 范围内的整数（244 除外，244 是内部自定义的时间戳 sei）； -  payloadUuid: 当 payloadType 为 5 时必须填写，其他情况下该值会被忽略。该值必须是长度为 32 的十六进制数字； -  interval: 选填，默认 1000。sei 的发送间隔，单位毫秒； -  followIdr: 选填，默认 false。该值为 true 时，发送关键帧时会确保带 sei，否则不确保。 |
| videoWidth | 【字段含义】指定云端转码的目标分辨率（宽度）。 【推荐取值】单位：像素值，推荐值：360，如果您只混合音频流，请将 width 和 height 均设置为 0，否则混流转码后的直播流中会有黑色背景。 |

## TRTCPublishCDNParam

#### 向非腾讯云 CDN 上发布音视频流时需设置的转推参数。

TRTC 的后台服务支持通过标准 RTMP 协议，将其中的音视频流发布到第三方直播 CDN 服务商。

如果您使用腾讯云直播 CDN 服务，可无需关注此参数，直接使用 startPublish 接口即可。
| 枚举类型 | 描述 |
| --- | --- |
| appId | 【字段含义】腾讯云直播服务的 AppID。 【推荐取值】请在 [实时音视频控制台](https://console.cloud.tencent.com/trtc) 依次单击【应用管理】=>【应用信息】，并在【旁路直播信息】中获取 appid。 |
| bizId | 【字段含义】腾讯云直播服务的 bizid。 【推荐取值】请在 [实时音视频控制台](https://console.cloud.tencent.com/trtc) 依次单击【应用管理】=>【应用信息】，并在【旁路直播信息】中获取 bizid。 |
| streamId | 【字段含义】需要转推的 streamId。 【推荐取值】默认值：空值。如果不填写，则默认转推调用者的旁路流。 |
| url | 【字段含义】指定该路音视频流在第三方直播服务商的推流地址（RTMP 格式）。 【推荐取值】各家服务商的推流地址规则差异较大，请根据目标服务商的要求填写合法的推流 URL，TRTC 的后台服务器会按照您填写的 URL 向第三方服务商推送标准格式音视频流。 【特别说明】推流 URL 必须为 RTMP 格式，必须符合您的目标直播服务商的规范要求，否则目标服务商会拒绝来自 TRTC 后台服务的推流请求。 |

## TRTCAudioRecordingParams

#### 本地音频文件的录制参数。

该参数用于在音频录制接口 startAudioRecording 中指定录制参数。
| 枚举类型 | 描述 |
| --- | --- |
| filePath | 【字段含义】录音文件的保存路径（必填）。 【特别说明】该路径需精确到文件名及格式后缀，格式后缀用于决定录音文件的格式，目前支持的格式有 PCM、WAV 和 AAC。 例如：假如您指定路径为 "mypath/record/audio.aac"，代表您希望 SDK 生成一个 AAC 格式的音频录制文件。 请您指定一个有读写权限的合法路径，否则录音文件无法生成。 |
| maxDurationPerFile | 【字段含义】maxDurationPerFile 录制文件分片时长，单位毫秒，最小值10000。默认值为0，表示不分片。 |
| recordingContent | 【字段含义】音频录制内容类型。 【特别说明】默认录制所有本地和远端音频。 |

## TRTCLocalRecordingParams

#### 本地媒体文件的录制参数。

该参数用于在本地媒体文件的录制接口 startLocalRecording 中指定录制相关参数。

接口 startLocalRecording 是接口 startAudioRecording 的能力加强版本，前者可以录制视频文件，后者只能录制音频文件。
| 枚举类型 | 描述 |
| --- | --- |
| filePath | 【字段含义】录制的文件地址（必填），请确保路径有读写权限且合法，否则录制文件无法生成。 【特别说明】该路径需精确到文件名及格式后缀，格式后缀用于决定录制出的文件格式，目前支持的格式暂时只有 MP4。 例如：假如您指定路径为 "mypath/record/test.mp4"，代表您希望 SDK 生成一个 MP4 格式的本地视频文件。 请您指定一个有读写权限的合法路径，否则录制文件无法生成。 |
| interval | 【字段含义】interval 录制信息更新频率，单位毫秒，有效范围：[1000, 10000]。默认值为-1，表示不回调。 |
| maxDurationPerFile | 【字段含义】maxDurationPerFile 录制文件分片时长，单位毫秒，最小值10000。默认值为0，表示不分片。 |
| recordType | 【字段含义】媒体录制类型，默认值：TRTC_RECORD_TYPE_BOTH，即同时录制音频和视频。 |

## TRTCAudioEffectParam(Deprecated)

#### 音效参数（已废弃）。

TRTC 中的“音效”特指一些短暂的音频文件，通常仅有几秒钟的播放时间，例如“鼓掌声”、“欢笑声”等。

该参数用于在早期版本的音效播放接口 playAudioEffect 中指定音效文件（即短音频文件）的路径和播放次数等。

在 7.3 版本以后，音效接口已被新的接口 startPlayMusic 所取代。

您在指定 startPlayMusic 的参数 TXAudioMusicParam 时，如果将 ` isShortFile ` 设置为 true，即为“音效”文件。
| 枚举类型 | 描述 |
| --- | --- |
| effectId | 【字段含义】音效 ID 【特别说明】SDK 允许播放多路音效，因此需要音效 ID 进行标记，用于控制音效的开始、停止、音量等。 |
| loopCount | 【字段含义】循环播放次数。 【推荐取值】取值范围为0 - 任意正整数，默认值：0，表示播放音效一次；1表示播放音效两次；以此类推。 |
| path | 【字段含义】音效文件路径，支持的文件格式：aac、mp3、m4a。 |
| publish | 【字段含义】音效是否上行。 【推荐取值】true：音效在本地播放的同时，会上行至云端，因此远端用户也能听到该音效；false：音效不会上行至云端，因此只能在本地听到该音效。默认值：false。 |
| volume | 【字段含义】音效音量。 【推荐取值】取值范围为0 - 100；默认值：100。 |

## TRTCSwitchRoomConfig

#### 房间切换参数。

该参数用于切换房间接口switchRoom，可以让用户从一个房间快速切换到另一个房间。
| 枚举类型 | 描述 |
| --- | --- |
| privateMapKey | 【字段含义】用于权限控制的权限票据（选填），当您希望某个房间只能让特定的 userId 进入时，需要使用 privateMapKey 进行权限保护。 【推荐取值】仅建议有高级别安全需求的客户使用，更多详情请参见 [进房权限保护](https://cloud.tencent.com/document/product/647/32240)。 |
| roomId | 【字段含义】数字房间号码 [选填]，在同一个房间内的用户可以看到彼此并能够进行音视频通话。 【推荐取值】取值范围：1 - 4294967294。 【特别说明】roomId 和 strRoomId 必须并且只能填一个。若两者都填，则优先选择 roomId。 |
| strRoomId | 【字段含义】字符串房间号码 [选填]，在同一个房间内的用户可以看到彼此并能够进行音视频通话。 【特别说明】roomId 和 strRoomId 必须并且只能填一个。若两者都填，则优先选择 roomId。 |
| userSig | 【字段含义】用户签名 [选填]，当前 userId 对应的验证签名，相当于登录密码。 如果您在切换房间时不指定新计算出的 userSig，SDK 会继续使用您在进入房间时（enterRoom）时所指定的 userSig。 这就需要您必须保证旧的 userSig 在切换房间的那一刻仍在签名允许的效期内，否则会导致房间切换失败。 【推荐取值】具体计算方法请参见 [如何计算UserSig](https://cloud.tencent.com/document/product/647/17275)。 |

## TRTCAudioFrameDelegateFormat

#### 音频自定义回调的格式参数。

该参数用于在音频自定义回调相关的接口中，设置 SDK 回调出来的音频数据的相关格式（包括采样率、声道数等）。
| 枚举类型 | 描述 |
| --- | --- |
| channel | 【字段含义】声道数。 【推荐取值】默认值：1，代表单声道。可设定的数值只有两个数字：1-单声道，2-双声道。 |
| mode | 【字段含义】回调数据读写模式 【推荐取值】TRTC_AUDIO_FRAME_OPERATION_MODE_READONLY：仅从回调中获取音频数据。可设定的模式有 TRTC_AUDIO_FRAME_OPERATION_MODE_READONLY，TRTC_AUDIO_FRAME_OPERATION_MODE_READWRITE。 |
| sampleRate | 【字段含义】采样率。 【推荐取值】默认值：48000Hz。支持 16000, 32000, 44100, 48000。 |
| samplesPerCall | 【字段含义】采样点数。 【推荐取值】取值必须是 ` sampleRate/100 ` 的整数倍。 |

## TRTCScreenShareParams

#### 屏幕分享参数（仅适用于 Android 平台）。

该参数用于在屏幕分享接口 startScreenCapture 中指定屏幕分享时的悬浮窗等相关信息。
| 枚举类型 | 描述 |
| --- | --- |
| enableForegroundService | @deprecated 从 v11.8 版本开始，为了适配 targetSdkVersion 34 及以上版本，屏幕分享会默认启动内置前台服务。该值设置无效 |
| floatingView | 【字段含义】可以通过此参数设置一个悬浮view。 【推荐取值】从 Android 7.0 系统开始，对于没有做过任何保活措施的后台应用，Android 系统会很快将其杀掉以减少系统能耗。 但当您的 App 处于屏幕分享状态时，不可避免地要被切到系统后台运行，此时如果能弹出悬浮窗可以避免被系统强杀掉。 同时，在手机屏幕上显示悬浮窗，也有利于告知用户当前正在做屏幕分享，以便提醒用户避免泄漏个人隐私。 【特殊说明】您也可以使用 Android 系统的 WindowsManager 接口达到同样的效果。 |
| mediaProjection | 【字段含义】可以通过此参数将您自己创建的 MediaProjection 传入给 SDK 使用。 【推荐取值】正常情况下，该参数保持为 null 即可。 |

## TRTCAudioParallelParams

#### 远端音频流智能并发播放策略的参数。

该参数用于设置远端音频流智能并发播放策略。
| 枚举类型 | 描述 |
| --- | --- |
| includeUsers | 【字段含义】指定用户必定能并发播放。 【特殊说明】指定必定并发播放的用户 ID 列表。这些用户不参与智能选择。 includeUsers 的数量必须小于 maxCount，否则本次并发播放设置失效。 includeUsers 仅在 maxCount > 0 时有效。当 includeUsers 生效时，参与智能并发选择的最大播放数 = maxCount - 有效 includeUsers 的数量。 |
| maxCount | 【字段含义】最大并发播放数。默认值：0。 -  如果 maxCount > 0，且实际人数 > maxCount，会实时智能选出 maxCount 路数据进行播放，这会极大的降低性能消耗。 -  如果 maxCount = 0，SDK 不限制并发播放数，在上麦人数比较多的房间可能会引发性能问题。 |

## TRTCUser

#### 媒体流发布相关配置的用户信息。

您可以通过设置该参数，配合媒体流目标发布参数 (TRTCPublishTarget) 和混流转码参数 (TRTCStreamMixingConfig)，将您指定的多路音视频流进行转码并发布到您填写的目标发布地址中
| 枚举类型 | 描述 |
| --- | --- |
| intRoomId | 【字段含义】数字房间号，需要和您的进房参数 (TRTCParams) 中的房间号类型相匹配。 【推荐取值】取值范围：1 - 4294967294。 【特别说明】intRoomId 与 strRoomId 是互斥的，若您进房参数中选用 strRoomId，则 intRoomId 需要填写为0。若两者都填，SDK 将优先选用 intRoomId。 |
| strRoomId | 【字段含义】字符串房间号，需要和您的进房参数 (TRTCParams) 中的房间号类型相匹配。 【特别说明】intRoomId 与 strRoomId 是互斥的，若您进房参数中选用 roomId，则 strRoomId 无需填写。若两者都填，SDK 将优先选用 intRoomId。 【推荐取值】限制长度为 64 字节。以下为支持的字符集范围（共 89 个字符）: -  大小写英文字母（a-zA-Z）； -  数字（0-9）； -  空格、` ! `、` # `、` $ `、` % `、` & `、` ( `、` ) `、` + `、` - `、` : `、` ; `、` < `、` = `、` . `、` > `、` ? `、` @ `、` [ `、` ] `、` ^ `、` _ `、` { `、` } `、` \\| `、` ~ `、` , `。 |
| userId | 【字段含义】用户标识，当前用户的 userId，相当于用户名，使用 UTF-8 编码。 【推荐取值】如果一个用户在您的账号系统中的 ID 为“mike”，则 userId 即可设置为“mike”。 |

## TRTCPublishCdnUrl

#### 向腾讯或者第三方 CDN 上发布音视频流时需设置的 url 配置。

该配置用于媒体流发布接口 startPublishMediaStream 中的目标推流配置 (TRTCPublishTarget)
| 枚举类型 | 描述 |
| --- | --- |
| isInternalLine | 【字段含义】指定该路音视频流是否发布至腾讯云。 【推荐取值】默认值：true。 【特别说明】若您的目标直播服务商为腾讯，请将此参数设置为 true，此时后台计费系统不会对此计算转推服务费。 |
| rtmpUrl | 【字段含义】指定该路音视频流在腾讯或者第三方直播服务商的推流地址（RTMP 格式）。 【推荐取值】各家服务商的推流地址规则差异较大，请根据目标服务商的要求填写合法的推流 URL，TRTC 的后台服务器会按照您填写的 URL 向第三方服务商推送标准格式音视频流。 【特别说明】推流 URL 必须为 RTMP 格式，必须符合您的目标直播服务商的规范要求，否则目标服务商会拒绝来自 TRTC 后台服务的推流请求。 |

## TRTCPublishTarget

#### 目标推流配置。

该配置用于媒体流发布接口 startPublishMediaStream。
| 枚举类型 | 描述 |
| --- | --- |
| cdnUrlList | 【字段含义】发布至腾讯或者第三方直播服务商的推流地址（RTMP 格式）。 【特别说明】若您的 mode 选择为 TRTC_PublishMixStream_ToRoom，此时您不需要设置该参数。 |
| mixStreamIdentity | 【字段含义】回推房间机器人信息。 【特别说明】仅当您的 mode 选择为 TRTC_PublishMixStream_ToRoom 时，您需要设置该参数。 【特别说明】设置后，该路转码音视频数据将回推到您指定的房间中。建议设置为特殊的 userId，以避免难以区分回推机器人和您通过 TRTC SDK 进房的主播。 【特别说明】参与混流的用户不支持订阅该转码流。 【特别说明】当您进房前设置的订阅模式(setDefaultStreamRecvMode) 均为手动时，您需要自行管理您想要拉取的音视频流（通常当您拉取回推房间的转码流时，您应该取消订阅参与转码的对应音视频单流）。 【特别说明】当您进房前设置的订阅模式(setDefaultStreamRecvMode) 均为自动时，不参与转码的用户将自动收到后台下发的转码流并不再继续接收参与转码的音视频单流。除非您明确进行取消订阅（muteRemoteVideoStream 和 muteRemoteAudio），否则转码流数据将持续下发。 |
| mode | 【字段含义】媒体流发布模式。 【推荐取值】请根据您的业务场景要求自行选择，TRTC 支持转推、转码和回推到 RTC 房间的模式。 【特别说明】若您的业务场景需要多个发布模式，您可以通过多次调用媒体流发布接口 (startPublishMediaStream) 并分别设置不同的 TRTCPublishTarget。 【特别说明】同一个 mode 请对应一个媒体流发布接口 (startPublishMediaStream)，并在后续需要调整时，使用 updatePublishCDNStream 进行更新。 |

## TRTCVideoLayout

#### 转码视频布局。

该配置用于媒体流发布接口（startPublishMediaStream）中的转码配置（TRTCStreamMixingConfig）。

用于指定转码流中每一路视频画面的位置、大小、图层以及流类型等信息。
| 枚举类型 | 描述 |
| --- | --- |
| backgroundColor | 【字段含义】指定混合画面的底色颜色。 【推荐取值】默认值：0x000000 代表黑色。格式为十六进制数字，例如：“0x61B9F1” 代表 RGB 分别为 (97,158,241)。 |
| fillMode | 【字段含义】画面填充模式。 【推荐取值】填充（画面可能会被拉伸裁剪）或适应（画面可能会有黑边），默认值：TRTC_VIDEO_RENDER_MODE_FILL。 |
| fixedVideoStreamType | 【字段含义】指定该路画面是主路画面（TRTC_VIDEO_STREAM_TYPE_BIG）还是辅路画面（TRTC_VIDEO_STREAM_TYPE_SUB）。 |
| fixedVideoUser | 【字段含义】参与转码的用户信息。 【特别说明】用户信息 (TRTCUser) 支持不填写（即 userId、intRoomId 和 strRoomId 均不填写）。此时当发起混流的房间中有主播上行音视频数据时，TRTC 后台服务器将自动将对应主播音视频填充到您指定的布局中。 |
| height | 【字段含义】指定该路画面的高度（单位：像素）。 |
| placeHolderImage | 【字段含义】占位图 URL，即当指定用户暂时仅上行音频时，腾讯云的后台服务器会将该 URL 地址指定的图片混合到最终的画面中。 【推荐取值】默认值：空值，即不设置占位图。 【特别说明】此时需要您指定用户信息 fixedVideoUser 中的 userId。 【特别说明】 -  URL 链接长度限制为 512 字节。图片大小限制不超过 2MB。 -  图片格式支持 png、jpg、jpeg、bmp 格式，推荐使用 png 格式的半透明图片作为占位图。 |
| width | 【字段含义】指定该路画面的宽度（单位：像素）。 |
| x | 【字段含义】指定该路画面的 x 坐标（单位：像素）。 |
| y | 【字段含义】指定该路画面的 y 坐标（单位：像素）。 |
| zOrder | 【字段含义】指定该路画面的层级（取值范围：0 - 15，不可重复）。 |

## TRTCWatermark

#### 水印布局。

该配置用于媒体流发布接口 (startPublishMediaStream) 中的转码配置 (TRTCStreamMixingConfig)
| 枚举类型 | 描述 |
| --- | --- |
| height | 【字段含义】指定该路水印画面的高度（单位：像素）。 |
| watermarkUrl | 【字段含义】水印 URL，腾讯云的后台服务器会将该 URL 地址指定的图片混合到最终的画面中。 【特别说明】 -  URL 链接长度限制为 512 字节。图片大小限制不超过 2MB。 -  图片格式支持 png、jpg、jpeg、bmp 格式，推荐使用 png 格式的半透明图片作为水印。 |
| width | 【字段含义】指定该路水印画面的宽度（单位：像素）。 |
| x | 【字段含义】指定该路水印画面的 x 坐标（单位：像素）。 |
| y | 【字段含义】指定该路水印画面的 y 坐标（单位：像素）。 |
| zOrder | 【字段含义】指定该路水印画面的层级（取值范围：0 - 15，不可重复）。 |

## TRTCStreamEncoderParam

#### 媒体流编码输出参数。

【字段含义】该配置用于媒体流发布接口（startPublishMediaStream）。

【特别说明】当您的发布目标（TRTCPublishTarget）中的 mode 配置为 TRTC_PublishMixStream_ToCdn 或者 TRTCPublishMixStreamToRoom 时，该参数为必填。

【特别说明】当您使用转推服务（mode 为 TRTC_PublishBigStream_ToCdn 或者 TRTC_PublishSubStream_ToCdn）时，为了更好的转推稳定性以及更好的 CDN 播放兼容性，也建议您填写该配置的具体参数。
| 枚举类型 | 描述 |
| --- | --- |
| audioEncodedChannelNum | 【字段含义】指定媒体发布流的目标音频声道数。 【推荐取值】默认值：1，代表单声道。可设定的数值只有两个数字：1-单声道，2-双声道。 |
| audioEncodedCodecType | 【字段含义】指定媒体发布流的目标音频编码类型。 【推荐取值】默认值：0，代表 LC-AAC。可设定的数值只有三个数字：0 - LC-AAC，1 - HE-AAC，2 - HE-AACv2。 【特别说明】HE-AAC 和 HE-AACv2 支持的输出流音频采样率范围为[48000, 44100, 32000, 24000, 16000]。 【特别说明】当音频编码设置为 HE-AACv2 时，只支持输出流音频声道数为双声道。 |
| audioEncodedKbps | 【字段含义】指定媒体发布流的目标音频码率（kbps）。 【推荐取值】默认值：50kbps，取值范围是 [32，192]。 |
| audioEncodedSampleRate | 【字段含义】指定媒体发布流的目标音频采样率。 【推荐取值】默认值：48000Hz。取值为 [48000, 44100, 32000, 24000, 16000, 8000]，单位是 Hz。 |
| videoEncodedCodecType | 【字段含义】指定媒体发布流的目标视频编码类型。 【推荐取值】默认值：0，代表 H264。可设定的数值只有两个数字：0 - H264，1 - H265。 |
| videoEncodedFPS | 【字段含义】指定媒体发布流的目标视频帧率（FPS）。 【推荐取值】推荐值：20fps，取值范围是 (0,30]。 |
| videoEncodedGOP | 【字段含义】指定媒体发布流的目标视频关键帧间隔（GOP）。 【推荐取值】推荐值：3，单位为秒，取值范围是 [1,5]。 |
| videoEncodedHeight | 【字段含义】指定媒体发布流的目标分辨率（高度）。 【推荐取值】单位：像素值，推荐值：640，如果您只混合音频流，请将 width 和 height 均设置为 0，否则混流转码后的直播流中会有黑色背景。 |
| videoEncodedKbps | 【字段含义】指定媒体发布流的目标视频码率（kbps）。 【推荐取值】如果填 0，TRTC 会根据 videoEncodedWidth 和 videoEncodedHeight 估算出一个合理的码率值，您也可以参考视频分辨率枚举定义中所推荐的码率值（见注释部分）。 |
| videoEncodedWidth | 【字段含义】指定媒体发布流的目标分辨率（宽度）。 【推荐取值】单位：像素值，推荐值：368，如果您只混合音频流，请将 width 和 height 均设置为 0，否则混流转码后的直播流中会有黑色背景。 |
| videoSeiParams | 【字段含义】混流 SEI 参数，默认不填写。 【特别说明】参数以 json 字符串形式传入，示例如下： `{` `  "payLoadContent":"xxx",` `  "payloadType":5,` `  "payloadUuid":"1234567890abcdef1234567890abcdef",` `  "interval":1000,` `  "followIdr":false` `}` 当前支持的字段及含义： -  payloadContent: 必填。透传 sei 的 payload 内容，不能为空； -  payloadType: 必填。sei 消息的类型，取值范围: 5 或 [100, 254] 范围内的整数（244 除外，244 是内部自定义的时间戳 sei）； -  payloadUuid: 当 payloadType 为 5 时必须填写，其他情况下该值会被忽略。该值必须是长度为 32 的十六进制数字； -  interval: 选填，默认 1000。sei 的发送间隔，单位毫秒； -  followIdr: 选填，默认 false。该值为 true 时，发送关键帧时会确保带 sei，否则不确保。 |

## TRTCStreamMixingConfig

#### 媒体流转码配置参数。

该配置用于媒体流发布接口（startPublishMediaStream）。

用于指定转码时各路画面的排版位置信息和输入的音频信息。
| 枚举类型 | 描述 |
| --- | --- |
| audioMixUserList | 【字段含义】指定转码流中的每一路输入音频的信息。 【推荐取值】该字段是一个 TRTCUser 类型的数组，数组中的每一个元素都用来代表每一路输入音频的信息。 【特别说明】用户信息支持不填写（即 audioMixUserList 为空）。此时若设置了 TRTCStreamEncoderParam 中音频相关编码输出参数，TRTC 后台服务器将自动将所有主播的音频混合输出（当前仅支持最高 16 路音视频输入）。 |
| backgroundColor | 【字段含义】指定混合画面的底色颜色。 【推荐取值】默认值：0x000000 代表黑色。格式为十六进制数字，例如：“0x61B9F1” 代表 RGB 分别为 （97、158、241）。 |
| backgroundImage | 【字段含义】指定混合画面的背景图 URL，腾讯云的后台服务器会将该 URL 地址指定的图片混合到最终的画面中。 【推荐取值】默认值：空值，即不设置背景图片。 【特别说明】 -  URL 链接长度限制为 512 字节。图片大小限制不超过 2MB。 -  图片格式支持 png、jpg、jpeg、bmp 格式，推荐使用 png 格式的半透明图片作为背景图。 |
| videoLayoutList | 【字段含义】指定混合画面中的每一路视频画面的位置、大小、图层以及流类型等信息。 【推荐取值】该字段是一个 TRTCVideoLayout 类型的数组，数组中的每一个元素都用来代表每一路画面的信息。 |
| watermarkList | 【字段含义】指定混合画面中的每一路水印画面的位置、大小、图层等信息。 【推荐取值】该字段是一个 TRTCWatermark 类型的数组，数组中的每一个元素都用来代表每一路水印的信息。 |

## TRTCPayloadPrivateEncryptionConfig

#### 媒体流私有加密配置。

该配置用于设置媒体流私有加密的算法和密钥。
| 枚举类型 | 描述 |
| --- | --- |
| encryptionAlgorithm | 【字段含义】加密算法，默认为 TRTC_EncryptionAlgorithm_Aes_128_Gcm。 |
| encryptionKey | 【字段含义】加密用密钥，字符串类型。 【推荐取值】若加密算法为 TRTC_EncryptionAlgorithm_Aes_128_Gcm，密匙长度需为 16 字节，若加密算法为 TRTC_EncryptionAlgorithm_Aes_256_Gcm，密匙长度需为 32 字节。 |
| encryptionSalt | 【字段含义】盐，加密用初始向量。 【推荐取值】需确保填入该参数的数组不为空、不全为 0 且数据长度为 32 字节。 |

## TRTCAudioVolumeEvaluateParams

#### 音量评估等相关参数设置。

该设置用于开启人声检测、声音频谱计算。
| 枚举类型 | 描述 |
| --- | --- |
| enablePitchCalculation | 【字段含义】是否开启本地人声频率计算 |
| enableSpectrumCalculation | 【字段含义】是否开启声音频谱计算。 |
| enableVadDetection | 【字段含义】是否开启本地人声检测。 【特别说明】在 startLocalAudio 之前调用才可以生效。 |
| interval | 【字段含义】设置 onUserVoiceVolume 回调的触发间隔，单位为毫秒，最小间隔为 100ms，如果小于等于 0 则会关闭回调。 【推荐取值】推荐值：300，单位为毫秒。 【特别说明】interval 大于 0 时，音量提示将默认开启，无需另外设置。 |
