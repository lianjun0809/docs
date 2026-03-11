> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

# 腾讯云实时音视频(TRTC SDK )文档

## 概述
`ITRTCCloud.h` 是腾讯云实时音视频(TRTC SDK ) C++ 的 API 文档，包含了推流、拉流、拉流、混流、录制等功能详细说明。


## ITRTCCloud
<table>
<tr>
<td rowspan="1" colSpan="1" >函数列表</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getTRTCShareInstance](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >创建 TRTCCloud 实例（单例模式）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[destroyTRTCShareInstance](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >销毁 TRTCCloud 实例（单例模式）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addCallback](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >添加 TRTC 事件回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeCallback](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >移除 TRTC 事件回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[enterRoom](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >进入房间。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[exitRoom](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >离开房间。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[switchRole](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >切换角色。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[switchRole](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >切换角色（支持设置权限位）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[switchRoom](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >切换房间。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[connectOtherRoom](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >请求跨房通话。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[disconnectOtherRoom](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >退出跨房通话。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setDefaultStreamRecvMode](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >设置订阅模式（需要在进入房前设置才能生效）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createSubCloud](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >创建子房间实例（用于多房间并发观看）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[destroySubCloud](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >销毁子房间实例。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[updateOtherRoomForwardMode](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >更改跨房主播在本房间的上行能力。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[startPublishMediaStream](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >开始发布媒体流。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[updatePublishMediaStream](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >更新发布媒体流。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[stopPublishMediaStream](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >停止发布媒体流。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[startLocalPreview](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >开启本地摄像头的预览画面（移动端）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[startLocalPreview](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >开启本地摄像头的预览画面（桌面端）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[updateLocalView](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >更新本地摄像头的预览画面。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[stopLocalPreview](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >停止摄像头预览。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[muteLocalVideo](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >暂停/恢复发布本地的视频流。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setVideoMuteImage](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >设置本地画面被暂停期间的替代图片。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[startRemoteView](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >订阅远端用户的视频流，并绑定视频渲染控件。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[updateRemoteView](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >更新远端用户的视频渲染控件。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[stopRemoteView](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >停止订阅远端用户的视频流，并释放渲染控件。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[stopAllRemoteView](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >停止订阅所有远端用户的视频流，并释放全部渲染资源。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[muteRemoteVideoStream](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >暂停/恢复订阅远端用户的视频流。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[muteAllRemoteVideoStreams](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >暂停/恢复订阅所有远端用户的视频流。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setVideoEncoderParam](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >设置视频编码器的编码参数。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setNetworkQosParam](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >设置网络质量控制的相关参数。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setLocalRenderParams](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >设置本地画面的渲染参数。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setRemoteRenderParams](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >设置远端画面的渲染模式。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[enableSmallVideoStream](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >开启大小画面双路编码模式。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setRemoteVideoStreamType](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >切换指定远端用户的大小画面。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[snapshotVideo](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >视频画面截图。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGravitySensorAdaptiveMode](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >设置重力感应的适配模式（11.7 及以上版本）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[startLocalAudio](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >开启本地音频的采集和发布。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[stopLocalAudio](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >停止本地音频的采集和发布。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[muteLocalAudio](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >暂停/恢复发布本地的音频流。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[muteRemoteAudio](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >暂停/恢复播放远端的音频流。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[muteAllRemoteAudio](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >暂停/恢复播放所有远端用户的音频流。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setRemoteAudioVolume](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >设定某一个远端用户的声音播放音量。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setAudioCaptureVolume](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >设定本地音频的采集音量。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getAudioCaptureVolume](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >获取本地音频的采集音量。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setAudioPlayoutVolume](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >设定远端音频的播放音量。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getAudioPlayoutVolume](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >获取远端音频的播放音量。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[enableAudioVolumeEvaluation](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >启用音量大小提示。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[startAudioRecording](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >开始录音。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[stopAudioRecording](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >停止录音。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[startLocalRecording](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >开启本地媒体录制。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[stopLocalRecording](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >停止本地媒体录制。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setRemoteAudioParallelParams](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >设置远端音频流智能并发播放策略。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[enable3DSpatialAudioEffect](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >启用 3D 音效。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[updateSelf3DSpatialPosition](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >设置 3D 音效中自身坐标及朝向信息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[updateRemote3DSpatialPosition](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >设置 3D 音效中远端用户坐标信息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[set3DSpatialReceivingRange](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >设置指定用户所发出声音的可被接收范围。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getDeviceManager](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >获取设备管理类（TXDeviceManager）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getBeautyManager](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >获取美颜管理类（TXBeautyManager）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setWaterMark](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >添加水印。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getAudioEffectManager](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >获取音效管理类（TXAudioEffectManager）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[startSystemAudioLoopback](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >开启系统声音采集（iOS 端暂未支持）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[stopSystemAudioLoopback](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >停止系统声音采集（iOS 端暂未支持）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setSystemAudioLoopbackVolume](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >设置系统声音的采集音量。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[startScreenCapture](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >启动屏幕分享。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[stopScreenCapture](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >停止屏幕分享。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[pauseScreenCapture](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >暂停屏幕分享。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[resumeScreenCapture](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >恢复屏幕分享。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getScreenCaptureSources](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >枚举可分享的屏幕和窗口（该接口仅支持桌面系统）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[selectScreenCaptureTarget](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >选取要分享的屏幕或窗口（该接口仅支持桌面系统）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setSubStreamEncoderParam](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >设置屏幕分享（即辅路）的视频编码参数（桌面系统和移动系统均已支持）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setSubStreamMixVolume](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >设置屏幕分享时的混音音量大小（该接口仅支持桌面系统）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addExcludedShareWindow](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >将指定窗口加入屏幕分享的排除列表中（该接口仅支持桌面系统）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeExcludedShareWindow](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >将指定窗口从屏幕分享的排除列表中移除（该接口仅支持桌面系统）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeAllExcludedShareWindow](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >将所有窗口从屏幕分享的排除列表中移除（该接口仅支持桌面系统）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addIncludedShareWindow](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >将指定窗口加入屏幕分享的包含列表中（该接口仅支持桌面系统）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeIncludedShareWindow](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >将指定窗口从屏幕分享的包含列表中移除（该接口仅支持桌面系统）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeAllIncludedShareWindow](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >将全部窗口从屏幕分享的包含列表中移除（该接口仅支持桌面系统）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[enableCustomVideoCapture](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >启用/关闭视频自定义采集模式。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[sendCustomVideoData](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >向 SDK 投送自己采集的视频帧。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[enableCustomAudioCapture](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >启用音频自定义采集模式。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[sendCustomAudioData](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >向 SDK 投送自己采集的音频数据。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[enableMixExternalAudioFrame](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >启用/关闭自定义音轨。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[mixExternalAudioFrame](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >向 SDK 混入自定义音轨。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setMixExternalAudioVolume](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >设置推流时混入外部音频的推流音量和播放音量。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[generateCustomPTS](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >生成自定义采集时的时间戳。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[enableLocalVideoCustomProcess](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >.1 开启视频第三方美颜。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setLocalVideoCustomProcessCallback](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >.2 设置第三方美颜的视频数据回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setLocalVideoRenderCallback](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >设置本地视频自定义渲染回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setRemoteVideoRenderCallback](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >设置远端视频自定义渲染回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setAudioFrameCallback](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >设置音频数据自定义回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setCapturedAudioFrameCallbackFormat](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >设置本地麦克风采集出的音频帧回调格式。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setLocalProcessedAudioFrameCallbackFormat](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >设置经过前处理后的本地音频帧回调格式。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setMixedPlayAudioFrameCallbackFormat](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >设置最终要由系统播放出的音频帧回调格式。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[enableCustomAudioRendering](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >开启音频自定义播放。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getCustomAudioRenderingFrame](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >获取可播放的音频数据。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[sendCustomCmdMsg](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >使用 UDP 通道发送自定义消息给房间内所有用户。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[sendSEIMsg](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >使用 SEI 通道发送自定义消息给房间内所有用户。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[startSpeedTest](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >开始进行网速测试（进入房间前使用）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[stopSpeedTest](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >停止网络测速。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getSDKVersion](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >获取 SDK 版本信息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setLogLevel](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >设置 Log 输出级别。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setConsoleEnabled](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >启用/禁用控制台日志打印。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setLogCompressEnabled](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >启用/禁用日志的本地压缩。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setLogDirPath](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >设置本地日志的保存路径。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setLogCallback](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >设置日志回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[showDebugView](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >显示仪表盘。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[callExperimentalAPI](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >调用实验性接口。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[enablePayloadPrivateEncryption](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >开启或关闭媒体流私有加密。</td>
</tr>
</table>


## getTRTCShareInstance



#### 创建 TRTCCloud 实例（单例模式）。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >context</td>

<td rowspan="1" colSpan="1" >仅适用于 Android 平台，SDK 内部会将其转化为 Android 平台的 ApplicationContext 用于调用 Android System API。<br>如果传入的 ` context ` 参数为空，SDK 内部会自动获取当前进程的 ApplicationContext。</td>
</tr>
</table>


> **注意**
> 

> 1. 如果您使用 ` delete ITRTCCloud* ` 会导致编译错误，请使用 [destroyTRTCShareInstance](https://write.woa.com/document/87030026264555520) 释放对象指针。
> 

> 2. 在 Windows、Mac 和 iOS 平台上，请调用 ` getTRTCShareInstance() ` 接口。
> 

> 3. 在 Android 平台上，请调用 ` getTRTCShareInstance(void *context) ` 接口。
> 


## destroyTRTCShareInstance



#### 销毁 TRTCCloud 实例（单例模式）。

## addCallback



#### 添加 TRTC 事件回调。

您可以通过 [ITRTCCloudCallback](https://write.woa.com/document/87030021158866944) 获得来自 SDK 的各类事件通知（例如：错误码，警告码，音视频状态参数等）。

## removeCallback



#### 移除 TRTC 事件回调。

## enterRoom



#### 进入房间。

TRTC 的所有用户都需要进入房间才能“发布”或“订阅”音视频流，“发布”是指将自己的音频和视频推送到云端，“订阅”是指从云端拉取房间里其他用户的音视频流。

调用该接口时，您需要指定您的应用场景 [TRTCAppScene](https://write.woa.com/document/87030132707430400) 以获取最佳的音视频传输体验，这些场景可以分成两大类：



**实时通话：**

包括 [TRTCAppSceneVideoCall](https://write.woa.com/document/87030132707430400) 和 [TRTCAppSceneAudioCall](https://write.woa.com/document/87030132707430400) 两个可选项，分别是视频通话和语音通话，该模式适合 1对1 的音视频通话，或者参会人数在 300 人以内的在线会议。



**在线直播：**

包括 [TRTCAppSceneLIVE](https://write.woa.com/document/87030132707430400) 和 [TRTCAppSceneVoiceChatRoom](https://write.woa.com/document/87030132707430400) 两个可选项，分别是视频直播和语音直播，该模式适合十万人以内的在线直播场景，但需要您在接下来介绍的 [TRTCParams](https://write.woa.com/document/87030132707430400) 参数中指定 **角色(role)** 这个字段，也就是将房间中的用户区分为 **主播** ([TRTCRoleAnchor](https://write.woa.com/document/87030132707430400)) 和 **观众** ([TRTCRoleAudience](https://write.woa.com/document/87030132707430400)) 两种不同的角色。



调用该接口后，您会收到来自 [ITRTCCloudCallback](https://write.woa.com/document/87030021158866944) 中的 [onEnterRoom](https://write.woa.com/document/87030021158866944) 回调：
-  如果进房成功，参数 ` result ` 会是一个正数（result > 0），表示从函数调用到进入房间所花费的时间，单位是毫秒（ms）。

-  如果进房失败，参数 ` result ` 会是一个负数（result < 0），表示进房失败的[错误码](https://cloud.tencent.com/document/product/647/32257)。

<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >param</td>

<td rowspan="1" colSpan="1" >进房参数，用于指定用户的身份、角色和安全票据等信息，详情请参见  [TRTCParams](https://write.woa.com/document/87030132707430400) 。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >scene</td>

<td rowspan="1" colSpan="1" >应用场景，用于指定您的业务场景，同一个房间内的所有用户需要设定相同的 [TRTCAppScene](https://write.woa.com/document/87030132707430400)。</td>
</tr>
</table>


> **注意**
> 

> 1. 同一个房间内的所有用户需要设定相同的 ` scene `。不同的 ` scene ` 会导致偶现的异常问题。
> 

> 2. 当您指定参数 ` scene ` 为 [TRTCAppSceneLIVE](https://write.woa.com/document/87030132707430400) 或 [TRTCAppSceneVoiceChatRoom](https://write.woa.com/document/87030132707430400) 时，您必须通过 [TRTCParams](https://write.woa.com/document/87030132707430400) 中的 ` role `字段为当前用户设定他/她在房间中的角色。
> 

> 3. 请您尽量保证 [enterRoom](https://write.woa.com/document/87030026264555520) 与 [exitRoom](https://write.woa.com/document/87030026264555520) 前后配对使用，即保证“先退出前一个房间再进入下一个房间”，否则会导致很多异常问题。
> 


## exitRoom



#### 离开房间。

调用该接口会让用户离开自己所在的音视频房间，并释放摄像头、麦克风、扬声器等设备资源。

等资源释放完毕之后，SDK 会通过 [ITRTCCloudCallback](https://write.woa.com/document/87030021158866944) 中的 [onExitRoom](https://write.woa.com/document/87030021158866944) 回调向您通知。



如果您要再次调用  [enterRoom](https://write.woa.com/document/87030026264555520)  或者切换到其他的供应商的 SDK，建议等待 [onExitRoom](https://write.woa.com/document/87030021158866944) 回调到来之后再执行之后的操作，以避免摄像头或麦克风被占用的问题。

## switchRole



#### 切换角色。

调用本接口可以实现用户在“主播”和“观众”两种角色之间来回切换。



由于视频直播和语音聊天室需要支持多达10万名观众同时观看，所以设定了 **只有主播才能发布自己的音视频** 的规则。因此，当有些观众希望发布自己的音视频流（以便能跟主播互动）时，就需要先把自己的角色切换成 **主播**。



您可以在进入房间时通过 [TRTCParams](https://write.woa.com/document/87030132707430400) 中的 ` role ` 字段事先确定用户的角色，也可以在进入房间后通过该接口动态切换角色。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >role</td>

<td rowspan="1" colSpan="1" >角色，默认为 **主播**。<br>- [TRTCRoleAnchor](https://write.woa.com/document/87030132707430400) ：主播，可以发布自己的音视频，同一个房间里最多支持50个主播同时发布音视频。<br>- [TRTCRoleAudience](https://write.woa.com/document/87030132707430400) ：观众，不能发布自己的音视频流，只能观看房间中其他主播的音视频。如果要发布自己的音视频，需要先通过 [switchRole](https://write.woa.com/document/87030026264555520) 切换成 **主播**，同一个房间内同时最多可以容纳 10 万名观众。</td>
</tr>
</table>


> **注意**
> 

> 1. 该接口仅适用于视频直播（[TRTCAppSceneLIVE](https://write.woa.com/document/87030132707430400)）和语音聊天室（[TRTCAppSceneVoiceChatRoom](https://write.woa.com/document/87030132707430400)）这两个场景。
> 

> 2. 如果您在调用 [enterRoom](https://write.woa.com/document/87030026264555520) 时指定的 ` scene ` 为 [TRTCAppSceneVideoCall](https://write.woa.com/document/87030132707430400) 或 [TRTCAppSceneAudioCall](https://write.woa.com/document/87030132707430400)，请不要调用这个接口。
> 


## switchRole



#### 切换角色（支持设置权限位）。

调用本接口可以实现用户在“主播”和“观众”两种角色之间来回切换。



由于视频直播和语音聊天室需要支持多达10万名观众同时观看，所以设定了 **只有主播才能发布自己的音视频** 的规则。因此，当有些观众希望发布自己的音视频流（以便能跟主播互动）时，就需要先把自己的角色切换成 **主播**。



您可以在进入房间时通过 [TRTCParams](https://write.woa.com/document/87030132707430400) 中的 ` role ` 字段事先确定用户的角色，也可以在进入房间后通过该接口动态切换角色。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >privateMapKey</td>

<td rowspan="1" colSpan="1" >用于权限控制的权限票据，当您希望某个房间只能让特定的 userId 进入或者上行视频时，需要使用 ` privateMapKey ` 进行权限保护。<br>-  仅建议有高级别安全需求的客户使用，更多详情请参见 [开启高级权限控制](https://cloud.tencent.com/document/product/647/32240)。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >role</td>

<td rowspan="1" colSpan="1" >角色，默认为 **主播**。<br>- [TRTCRoleAnchor](https://write.woa.com/document/87030132707430400) ：主播，可以发布自己的音视频，同一个房间里最多支持50个主播同时发布音视频。<br>- [TRTCRoleAudience](https://write.woa.com/document/87030132707430400) ：观众，不能发布自己的音视频流，只能观看房间中其他主播的音视频。如果要发布自己的音视频，需要先通过 [switchRole](https://write.woa.com/document/87030026264555520) 切换成 **主播**，同一个房间内同时最多可以容纳 10 万名观众。</td>
</tr>
</table>


> **注意**
> 

> 1. 该接口仅适用于视频直播（[TRTCAppSceneLIVE](https://write.woa.com/document/87030132707430400)）和语音聊天室（[TRTCAppSceneVoiceChatRoom](https://write.woa.com/document/87030132707430400)）这两个场景。
> 

> 2. 如果您在 [enterRoom](https://write.woa.com/document/87030026264555520) 时指定的 ` scene ` 为 [TRTCAppSceneVideoCall](https://write.woa.com/document/87030132707430400) 或 [TRTCAppSceneAudioCall](https://write.woa.com/document/87030132707430400)，请不要调用这个接口。
> 


## switchRoom



#### 切换房间。

使用该接口可以让用户快速从一个房间切换到另一个房间。
-  如果用户的身份是“观众”，该接口的调用效果等同于 ` exitRoom(当前房间) + enterRoom（新的房间） `。

-  如果用户的身份是“主播”，该接口在切换房间的同时还会保持自己的音视频发布状态，因此在房间切换过程中，摄像头的预览和声音的采集都不会中断。




该接口适用于在线教育场景中，监课老师在多个房间中进行快速切换的场景。在该场景下使用 ` switchRoom ` 可以获得比 ` exitRoom + enterRoom ` 更好的流畅性和更少的代码量。

接口调用结果会通过 [ITRTCCloudCallback](https://write.woa.com/document/87030021158866944) 中的 [onSwitchRoom](https://write.woa.com/document/87030021158866944) 回调。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >config</td>

<td rowspan="1" colSpan="1" >房间参数，详情请参见 [TRTCSwitchRoomConfig](https://write.woa.com/document/87030132707430400)。</td>
</tr>
</table>


> **注意**
> 

> 由于对老版本 SDK 兼容的需求，参数 ` config ` 中同时包含 ` roomId ` 与 ` strRoomId ` 两个参数，这两个参数的填写格外讲究，请注意如下事项：
> 

> 1. 若您选用 ` strRoomId `，则 ` roomId ` 需要填写为0。若两者都填，将优先选用 ` roomId `。
> 

> 2. 所有房间需要同时使用 ` strRoomId ` 或同时使用 ` roomId `，不可混用，否则将会出现很多预期之外的 bug。
> 


## connectOtherRoom



#### 请求跨房通话。

默认情况下，只有同一个房间中的用户之间可以进行音视频通话，不同的房间之间的音视频流是相互隔离的。

但您可以通过调用该接口，将另一个房间中某个主播音视频流发布到自己所在的房间中，与此同时，该接口也会将自己的音视频流发布到目标主播的房间中。



也就是说，您可以使用该接口让身处两个不同房间中的主播进行跨房间的音视频流分享，从而让每个房间中的观众都能观看到这两个主播的音视频。该功能可以用来实现主播之间的 PK 功能。



跨房通话的请求结果会通过 [ITRTCCloudCallback](https://write.woa.com/document/87030021158866944) 中的 [onConnectOtherRoom](https://write.woa.com/document/87030021158866944) 回调通知给您。



例如：当房间“101”中的主播 A 通过 ` connectOtherRoom() ` 跟房间“102”中的主播 B 建立跨房通话后，
-  房间“101”中的用户都会收到主播 B 的 ` onRemoteUserEnterRoom(B) ` 和 ` onUserVideoAvailable(B,true) ` 这两个事件回调，即房间“101”中的用户都可以订阅主播 B 的音视频。

-  房间“102”中的用户都会收到主播 A 的 ` onRemoteUserEnterRoom(A) ` 和 ` onUserVideoAvailable(A,true) ` 这两个事件回调，即房间“102”中的用户都可以订阅主播 A 的音视频。




![](https://qcloudimg.tencent-cloud.cn/raw/c5e6c72fc163ad5c0b6b7b00e1da55b5.png)

跨房通话的参数考虑到后续扩展字段的兼容性问题，暂时采用了 JSON 格式的参数：



**情况一：数字房间号**

如果房间“101”中的主播 A 要跟房间“102”中的主播 B 连麦，那么主播 A 调用该接口时需要传入：` {"roomId": 102, "userId": "userB"} `

示例代码如下：
``` cpp
  Json::Value jsonObj;
  jsonObj["roomId"] = 102;
  jsonObj["userId"] = "userB";
  Json::FastWriter writer;
  std::string params = writer.write(jsonObj);
  trtc.connectOtherRoom(params.c_str());
```



**情况二：字符串房间号**

如果您使用的是字符串房间号，务必请将 json 中的 “roomId” 替换成 “strRoomId”: ` {"strRoomId": "102", "userId": "userB"} `

示例代码如下：
``` cpp
  Json::Value jsonObj;
  jsonObj["strRoomId"] = "102";
  jsonObj["userId"] = "userB";
  Json::FastWriter writer;
  std::string params = writer.write(jsonObj);
  trtc.connectOtherRoom(params.c_str());
```
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >param</td>

<td rowspan="1" colSpan="1" >需要您传入 JSON 格式的字符串参数，` roomId ` 代表数字格式的房间号，` strRoomId ` 代表字符串格式的房间号，` userId ` 代表目标主播的用户 ID。</td>
</tr>
</table>


## disconnectOtherRoom



#### 退出跨房通话。

退出结果会通过 [ITRTCCloudCallback](https://write.woa.com/document/87030021158866944) 中的 [onDisconnectOtherRoom](https://write.woa.com/document/87030021158866944) 回调通知给您。

## setDefaultStreamRecvMode



#### 设置订阅模式（需要在进入房前设置才能生效）。

您可以通过该接口在“自动订阅”和“手动订阅”两种模式下进行切换：
-  自动订阅：默认模式，用户在进入房间后会立刻接收到该房间中的音视频流，音频会自动播放，视频会自动开始解码（依然需要您通过 [startRemoteView](https://write.woa.com/document/87030026264555520) 接口绑定渲染控件）。

-  手动订阅：在用户进入房间后，需要手动调用 [startRemoteView](https://write.woa.com/document/87030026264555520) 接口才能启动视频流的订阅和解码，需要手动调用 [muteRemoteAudio](https://write.woa.com/document/87030026264555520) (false) 接口才能启动声音的播放。




在绝大多数场景下，用户进入房间后都会订阅房间中所有主播的音视频流，因此 TRTC 默认采用了自动订阅模式，以求得最佳的“秒开体验”。

如果您的应用场景中每个房间同时会有很多路音视频流在发布，而每个用户只想选择性地订阅其中的 1-2 路，则推荐使用“手动订阅”模式以节省流量费用。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >autoRecvAudio</td>

<td rowspan="1" colSpan="1" >true：自动订阅音频；false：需手动调用 ` muteRemoteAudio(false) ` 订阅音频。默认值：true。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >autoRecvVideo</td>

<td rowspan="1" colSpan="1" >true：自动订阅视频；false：需手动调用 ` startRemoteView ` 订阅视频。默认值：true。</td>
</tr>
</table>


> **注意**
> 

> 1. 需要在进入房间前调用该接口进行设置才能生效。
> 

> 2. 在自动订阅模式下，如果用户在进入房间后没有调用  [startRemoteView](https://write.woa.com/document/87030026264555520) 订阅视频流，SDK 会自动停止订阅视频流，以便达到节省流量的目的。
> 


## createSubCloud



#### 创建子房间实例（用于多房间并发观看）。

TRTCCloud 一开始被设计成单例模式，限制了多房间并发观看的能力。

通过调用该接口，您可以创建出多个 TRTCCloud 实例，以便同时进入多个不同的房间观看音视频流。



但需要注意的是，您在多个 TRTCCloud 实例中发布音视频流的能力会受到一定限制。



该功能主要用于在线教育场景中一种被称为“超级小班课”的业务场景中，用于解决“每个 TRTC 的房间中最多只能有 50 人同时发布自己音视频流”的限制。



示例代码如下：
``` cpp
    //In the small room that needs interaction, enter the room as an anchor and push audio and video streams
    ITRTCCloud *mainCloud = getTRTCShareInstance();
    TRTCParams mainParams;
    //Fill your params
    mainParams.role = TRTCRoleAnchor;
    mainCloud->enterRoom(mainParams, TRTCAppSceneLIVE);
    //...
    mainCloud->startLocalAudio(TRTCAudioQualityDefault);
    mainCloud->startLocalPreview(renderView);
    
    //In the large room that only needs to watch, enter the room as an audience and pull audio and video streams
    ITRTCCloud *subCloud = mainCloud->createSubCloud();
    TRTCParams subParams;
    //Fill your params
    subParams.role = TRTCRoleAudience;
    subCloud->enterRoom(subParams, TRTCAppSceneLIVE);
    //...
    subCloud->startRemoteView(userId, TRTCVideoStreamTypeBig, renderView);
    //...
    //Exit from new room and release it.
    subCloud->exitRoom();
    mainCloud->destroySubCloud(subCloud);
```

> **注意**
> 

> 1. 同一个用户，可以使用同一个 userId 进入多个不同 roomId 的房间。
> 

> 2. 两台不同的终端设备不可以同时使用同一个 userId 进入同一个 roomId 的房间。
> 

> 3. 您可以分别为不同实例分别设置 [ITRTCCloudCallback](https://write.woa.com/document/87030021158866944) 获取各自的事件通知。
> 

> 4. 同一个用户可以在多个 TRTCCloud 实例中推流，也可以调用子实例中与本地音视频相关的接口。但需要注意：
> 
> -  多实例的音频需要同时为麦克风采集或自定义采集，而且与音频设备相关的接口调用会以最后一次为准；
> -  与摄像头相关的调用会以最后一次为准：[startLocalPreview](https://write.woa.com/document/87030026264555520)。


#### 返回值说明：

子 TRTCCloud 实例

## destroySubCloud



#### 销毁子房间实例。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >subCloud</td>

<td rowspan="1" colSpan="1" >子房间实例</td>
</tr>
</table>


## updateOtherRoomForwardMode



#### 更改跨房主播在本房间的上行能力。

通常情况下，在调用 [connectOtherRoom](https://write.woa.com/document/87030026264555520) 接口与另一个房间的主播进行跨房通话后，本房间内的所有观众都将收到该主播发布的音视频流。

您可以通过调用该接口，限制跨房主播在本房间内的上行能力，禁止或允许跨房主播发布音频/主路视频/辅路视频，该行为会影响房间内的所有用户。

在禁用跨房主播某种上行能力后，本房间内所有用户将无法收到对应音视频流，且无法再订阅对应的音视频。



需要注意的是，该接口只能由进行跨房通话的主播调用，且通过该接口设置的限制会因为跨房通话的中断或对应主播退房重置。



该接口的调用结果会通过 [ITRTCCloudCallback](https://write.woa.com/document/87030021158866944) 中的 [onUpdateOtherRoomForwardMode](https://write.woa.com/document/87030021158866944) 回调通知给您。



例如：

房间“101”中有主播 A 与观众 B，房间“102”中有主播 C，主播 C 正常发布音视频流。主播 A 通过 [connectOtherRoom](https://write.woa.com/document/87030026264555520) 跟主播 C 建立跨房通话。
-  此时，主播 A 与观众 B 都会收到主播 C 的 ` onRemoteUserEnterRoom(C) `, ` onUserVideoAvailable(C,true) ` 和 ` onUserAudioAvailable(C,true) ` 这三个事件回调，可以订阅主播 C 的音视频。




之后，主播 A 调用该接口禁用主播 C 在本房间发布音频的能力。
-  此后，主播 C 的音频流将无法发布至房间“101”，主播 A 与观众 B 都将收到 ` onUserAudioAvailable(C,false) ` 事件回调，且无法再通过 ` muteRemoteAudio(C,false) ` 订阅主播 C 的音频。

-  主播 C 的视频流将不受影响。房间“102”中的其他观众也不受影响，可以正常订阅主播 C 的音频。




该接口的参数考虑到后续扩展字段的兼容性问题，暂时采用了 JSON 格式的参数，示例如下：

**情况一：数字房间号**
``` cpp
{
  "roomId":102,
  "userId":"userC",
  "muteAudio":false,
  "muteVideo":true,
  "muteSubStream":false
}
```



**情况二：字符串房间号**
``` cpp
{
  "strRoomId":"102",
  "userId":"userC",
  "muteAudio":false,
  "muteVideo":true,
  "muteSubStream":false
}
```
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >param</td>

<td rowspan="1" colSpan="1" >需要您传入 JSON 格式的字符串参数，` roomId ` 代表数字格式的房间号，` strRoomId ` 代表字符串格式的房间号，` userId ` 代表目标主播的用户 ID，` muteAudio `, ` muteVideo `,` muteSubStream ` 均为可选项，分表代表禁止或允许跨房主播发布音频/主路视频/辅路视频的能力。</td>
</tr>
</table>


## startPublishMediaStream



#### 开始发布媒体流。

该接口会向 TRTC 服务器发送指令，要求其将当前用户的音视频流转推/转码到直播 CDN 或者回推到 TRTC 房间中您可以通过 [TRTCPublishTarget](https://write.woa.com/document/87030132707430400) 配置中的 [TRTCPublishMode](https://write.woa.com/document/87030132707430400) 指定具体的发布模式
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >config</td>

<td rowspan="1" colSpan="1" >媒体流转码配置参数。具体配置参考 [TRTCStreamMixingConfig](https://write.woa.com/document/87030132707430400)。转码和回推到 TRTC 房间中时为必填项，您需要指定您预期的转码配置参数。转推模式下则无效。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >params</td>

<td rowspan="1" colSpan="1" >媒体流编码输出参数，具体配置参考 [TRTCStreamEncoderParam](https://write.woa.com/document/87030132707430400)。转码和回推到 TRTC 房间中时为必填项，您需要指定您预期的转码输出参数。在转推时，为了更好的转推稳定性和 CDN 兼容性，也建议您进行配置。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >target</td>

<td rowspan="1" colSpan="1" >媒体流发布的目标地址，具体配置参考 [TRTCPublishTarget](https://write.woa.com/document/87030132707430400)。支持转推/转码到腾讯或者第三方 CDN，也支持转码回推到 TRTC 房间中。</td>
</tr>
</table>


> **注意**
> 

> 1. SDK 会通过回调 [onStartPublishMediaStream](https://write.woa.com/document/87030021158866944) 带给您后台启动的任务标识（即 taskId）。
> 

> 2. 同一个任务（[TRTCPublishMode](https://write.woa.com/document/87030132707430400) 与 [TRTCPublishCdnUrl](https://write.woa.com/document/87030132707430400) 均相同）仅支持启动一次。若您后续需要更新或者停止该项任务，需要记录并使用返回的 taskId，通过 [updatePublishMediaStream](https://write.woa.com/document/87030026264555520) 或者 [stopPublishMediaStream](https://write.woa.com/document/87030026264555520) 来操作。
> 

> 3. ` target ` 支持同时配置多个 CDN URL（最多同时 10 个）。若您的同一个转推/转码任务需要发布至多路 CDN，则仅需要在 ` target ` 中配置多个 CDN URL 即可。同一个转码任务即使有多个转推地址，对应的转码计费仍只收取一份。
> 

> 4. 使用时需要注意不要多个任务同时往相同的 URL 地址推送，以免引起异常推流状态。一种推荐的方案是 URL 中使用 “sdkappid_roomid_userid_main” 作为区分标识，这种命名方式容易辨认且不会在您的多个应用中发生冲突。
> 


## updatePublishMediaStream



#### 更新发布媒体流。

该接口会向 TRTC 服务器发送指令，更新通过 [startPublishMediaStream](https://write.woa.com/document/87030026264555520) 启动的媒体流
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >config</td>

<td rowspan="1" colSpan="1" >媒体流转码配置参数。具体配置参考 [TRTCStreamMixingConfig](https://write.woa.com/document/87030132707430400)。转码和回推到 TRTC 房间中时为必填项，您需要指定您预期的转码配置参数。转推模式下则无效。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >params</td>

<td rowspan="1" colSpan="1" >媒体流编码输出参数，具体配置参考 [TRTCStreamEncoderParam](https://write.woa.com/document/87030132707430400)。转码和回推到 TRTC 房间中时为必填项，您需要指定您预期的转码输出参数。在转推时，为了更好的转推稳定性和 CDN 兼容性，也建议您进行配置。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >target</td>

<td rowspan="1" colSpan="1" >媒体流发布的目标地址，具体配置参考 [TRTCPublishTarget](https://write.woa.com/document/87030132707430400)。支持转推/转码到腾讯或者第三方 CDN，也支持转码回推到 TRTC 房间中。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >taskId</td>

<td rowspan="1" colSpan="1" >通过回调 [onStartPublishMediaStream](https://write.woa.com/document/87030021158866944) 带给您后台启动的任务标识（即 taskId）</td>
</tr>
</table>


> **注意**
> 

> 1. 您可以通过本接口来更新发布的 CDN URL（支持增删，最多同时 10 个），但您使用时需要注意不要多个任务同时往相同的 URL 地址推送，以免引起异常推流状态。
> 

> 2. 您可以通过 ` taskId ` 来更新调整转推/转码任务。例如在 pk 业务中，您可以先通过 [startPublishMediaStream](https://write.woa.com/document/87030026264555520) 发起转推，接着在主播发起 pk 时，通过 ` taskId ` 和本接口将转推更新为转码任务。此时，CDN 播放将连续并且不会发生断流（您需要保持媒体流编码输出参数 param 一致）。
> 

> 3. 同一个任务不支持纯音频、音视频、纯视频之间的切换。
> 


## stopPublishMediaStream



#### 停止发布媒体流。

该接口会向 TRTC 服务器发送指令，停止通过 [startPublishMediaStream](https://write.woa.com/document/87030026264555520) 启动的媒体流
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >taskId</td>

<td rowspan="1" colSpan="1" >通过回调 [onStartPublishMediaStream](https://write.woa.com/document/87030021158866944) 带给您后台启动的任务标识（即 taskId）</td>
</tr>
</table>


> **注意**
> 

> 1. 若您的业务后台并没有保存该 ` taskId `，在您的主播异常退房重进后，如果您需要重新获取 ` taskId `，您可以再次调用 [startPublishMediaStream](https://write.woa.com/document/87030026264555520) 启动任务。此时 TRTC 后台会返回任务启动失败，同时带给您上一次启动的 ` taskId `。
> 

> 2. 若 ` taskId ` 填空字符串，将会停止该用户所有通过 [startPublishMediaStream](https://write.woa.com/document/87030026264555520) 启动的媒体流，如果您只启动了一个媒体流或者想停止所有通过您启动的媒体流，推荐使用这种方式。
> 


## startLocalPreview



#### 开启本地摄像头的预览画面（移动端）。

在 [enterRoom](https://write.woa.com/document/87030026264555520) 之前调用此函数，SDK 只会开启摄像头，并一直等到您调用 [enterRoom](https://write.woa.com/document/87030026264555520) 之后才开始推流。

在 [enterRoom](https://write.woa.com/document/87030026264555520) 之后调用此函数，SDK 会开启摄像头并自动开始视频推流。

当开始渲染首帧摄像头画面时，您会收到 [ITRTCCloudCallback](https://write.woa.com/document/87030021158866944) 中的 [onCameraDidReady](https://write.woa.com/document/87030021158866944) 回调通知。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >frontCamera</td>

<td rowspan="1" colSpan="1" >true：前置摄像头；false：后置摄像头。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >view</td>

<td rowspan="1" colSpan="1" >承载视频画面的控件。</td>
</tr>
</table>


> **注意**
> 

> 如果希望开播前预览摄像头画面并通过 BeautyManager 调节美颜参数，您可以：
> 
> -  方案一：在调用 [enterRoom](https://write.woa.com/document/87030026264555520) 之前调用 ` startLocalPreview `。
> -  方案二：在调用 [enterRoom](https://write.woa.com/document/87030026264555520) 之后调用 ` startLocalPreview + muteLocalVideo(true) `。


## startLocalPreview



#### 开启本地摄像头的预览画面（桌面端）。

在调用该接口之前，您可以先调用 [setCurrentDevice](https://write.woa.com/document/87030115247763456) 选择使用桌面端设备自带摄像头或外接摄像头。

在 [enterRoom](https://write.woa.com/document/87030026264555520) 之前调用此函数，SDK 只会开启摄像头，并一直等到您调用 [enterRoom](https://write.woa.com/document/87030026264555520) 之后才开始推流。

在 [enterRoom](https://write.woa.com/document/87030026264555520) 之后调用此函数，SDK 会开启摄像头并自动开始视频推流。

当开始渲染首帧摄像头画面时，您会收到 [ITRTCCloudCallback](https://write.woa.com/document/87030021158866944)  中的 [onCameraDidReady](https://write.woa.com/document/87030021158866944) 回调通知。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >view</td>

<td rowspan="1" colSpan="1" >承载视频画面的控件。</td>
</tr>
</table>


> **注意**
> 

> 如果希望开播前预览摄像头画面并通过 BeautyManager 调节美颜参数，您可以：
> 
> -  方案一：在调用 [enterRoom](https://write.woa.com/document/87030026264555520) 之前调用 ` startLocalPreview `。
> -  方案二：在调用 [enterRoom](https://write.woa.com/document/87030026264555520) 之后调用 ` startLocalPreview + muteLocalVideo(true) `。


## updateLocalView



#### 更新本地摄像头的预览画面。

## stopLocalPreview



#### 停止摄像头预览。

## muteLocalVideo



#### 暂停/恢复发布本地的视频流。

该接口可以暂停（或恢复）发布本地的视频画面，暂停之后，同一房间中的其他用户将无法继续看到自己画面。

该接口在指定 [TRTCVideoStreamTypeBig](https://write.woa.com/document/87030132707430400) 时等效于 ` startLocalPreview + stopLocalPreview ` 这两个接口，但具有更好的响应速度。

因为 ` startLocalPreview + stopLocalPreview ` 需要打开和关闭摄像头，而打开和关闭摄像头都是硬件设备相关的操作，非常耗时。

相比之下，` muteLocalVideo ` 只需要在软件层面对数据流进行暂停或者放行即可，因此效率更高，也更适合需要频繁打开关闭的场景。



当暂停/恢复发布指定 [TRTCVideoStreamTypeBig](https://write.woa.com/document/87030132707430400) 后，同一房间中的其他用户将会收到 [onUserVideoAvailable](https://write.woa.com/document/87030021158866944) 回调通知。

当暂停/恢复发布指定 [TRTCVideoStreamTypeSub](https://write.woa.com/document/87030132707430400) 后，同一房间中的其他用户将会收到 [onUserSubStreamAvailable](https://write.woa.com/document/87030021158866944) 回调通知。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >mute</td>

<td rowspan="1" colSpan="1" >true：暂停；false：恢复。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >streamType</td>

<td rowspan="1" colSpan="1" >要暂停/恢复的视频流类型（仅支持 [TRTCVideoStreamTypeBig](https://write.woa.com/document/87030132707430400) 和 [TRTCVideoStreamTypeSub](https://write.woa.com/document/87030132707430400)）。</td>
</tr>
</table>


## setVideoMuteImage



#### 设置本地画面被暂停期间的替代图片。

当您调用 ` muteLocalVideo(true) ` 暂停本地画面时，您可以通过调用本接口设置一张替代图片，设置后，房间中的其他用户会看到这张替代图片，而不是黑屏画面。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >fps</td>

<td rowspan="1" colSpan="1" >设置替代图片帧率，最小值为5，最大值为10，默认5。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >image</td>

<td rowspan="1" colSpan="1" >设置替代图片，空值代表在 [muteLocalVideo](https://write.woa.com/document/87030026264555520) 之后不再发送视频流数据，默认值为空。</td>
</tr>
</table>


## startRemoteView



#### 订阅远端用户的视频流，并绑定视频渲染控件。

调用该接口可以让 SDK 拉取指定 userId 的视频流，并渲染到参数 ` view ` 指定的渲染控件上。您可以通过 [setRemoteRenderParams](https://write.woa.com/document/87030026264555520) 设置画面的显示模式。
-  如果您已经知道房间中有视频流的用户的 userId，可以直接调用 ` startRemoteView ` 订阅该用户的画面。

-  如果您不知道房间中有哪些用户在发布视频，您可以在 [enterRoom](https://write.woa.com/document/87030026264555520) 之后等待来自 [onUserVideoAvailable](https://write.woa.com/document/87030021158866944) 的通知。




调用本接口只是启动视频流的拉取，此时画面还需要加载和缓冲，当缓冲完毕后您会收到来自 [onFirstVideoFrame](https://write.woa.com/document/87030021158866944) 的通知。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >streamType</td>

<td rowspan="1" colSpan="1" >指定要观看 userId 的视频流类型。<br>-  高清大画面：[TRTCVideoStreamTypeBig](https://write.woa.com/document/87030132707430400)。<br>-  低清小画面：[TRTCVideoStreamTypeSmall](https://write.woa.com/document/87030132707430400)（需要远端用户通过 [enableSmallVideoStream](https://write.woa.com/document/87030026264555520) 开启双路编码后才有效果）。<br>-  辅流画面（常用于屏幕分享）：[TRTCVideoStreamTypeSub](https://write.woa.com/document/87030132707430400)。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >指定远端用户的 ID。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >view</td>

<td rowspan="1" colSpan="1" >用于承载视频画面的渲染控件。</td>
</tr>
</table>


> **注意**
> 

> 注意几点规则需要您关注：
> 

> 1. SDK 支持同时观看某 userId 的大画面和辅路画面，或者同时观看某 userId 的小画面和辅路画面，但不支持同时观看大画面和小画面。
> 

> 2. 只有当指定的 userId 通过 [enableSmallVideoStream](https://write.woa.com/document/87030026264555520) 开启双路编码后，才能观看该用户的小画面。
> 

> 3. 当指定的 userId 的小画面不存在时，SDK 默认切换到该用户的大画面。
> 


## updateRemoteView



#### 更新远端用户的视频渲染控件。

该接口可用于更新远端视频画面的渲染控件，常被用于切换显示区域的交互场景中。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >streamType</td>

<td rowspan="1" colSpan="1" >要设置预览窗口的流类型（仅支持 [TRTCVideoStreamTypeBig](https://write.woa.com/document/87030132707430400) 和 [TRTCVideoStreamTypeSub](https://write.woa.com/document/87030132707430400)）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >指定远端用户的 ID。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >view</td>

<td rowspan="1" colSpan="1" >承载视频画面的控件。</td>
</tr>
</table>


## stopRemoteView



#### 停止订阅远端用户的视频流，并释放渲染控件。

调用此接口会让 SDK 停止接收该用户的视频流，并释放该路视频流的解码和渲染资源。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >streamType</td>

<td rowspan="1" colSpan="1" >指定要观看 userId 的视频流类型。<br>-  高清大画面：[TRTCVideoStreamTypeBig](https://write.woa.com/document/87030132707430400)。<br>-  低清小画面：[TRTCVideoStreamTypeSmall](https://write.woa.com/document/87030132707430400)。<br>-  辅流画面（常用于屏幕分享）：[TRTCVideoStreamTypeSub](https://write.woa.com/document/87030132707430400)。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >指定远端用户的 ID。</td>
</tr>
</table>


## stopAllRemoteView



#### 停止订阅所有远端用户的视频流，并释放全部渲染资源。

调用此接口会让 SDK 停止接收所有来自远端的视频流，并释放全部的解码和渲染资源。

> **注意**
> 

> 如果当前有正在显示的辅路画面（屏幕分享）也会一并被停止。
> 


## muteRemoteVideoStream



#### 暂停/恢复订阅远端用户的视频流。

该接口仅暂停/恢复接收指定用户的视频流，但并不释放显示资源，视频画面会被冻屏在接口调用时的最后一帧。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >mute</td>

<td rowspan="1" colSpan="1" >是否暂停接收。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >streamType</td>

<td rowspan="1" colSpan="1" >要暂停/恢复的视频流类型。<br>-  高清大画面：[TRTCVideoStreamTypeBig](https://write.woa.com/document/87030132707430400)。<br>-  低清小画面：[TRTCVideoStreamTypeSmall](https://write.woa.com/document/87030132707430400)。<br>-  辅流画面（常用于屏幕分享）：[TRTCVideoStreamTypeSub](https://write.woa.com/document/87030132707430400)。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >指定远端用户的 ID。</td>
</tr>
</table>


> **注意**
> 

> 该接口支持您在进入房间（[enterRoom](https://write.woa.com/document/87030026264555520)）前调用，暂停状态在退出房间（[exitRoom](https://write.woa.com/document/87030026264555520)）之后会被重置。调用该接口暂停接收指定用户的视频流后，只调用 [startRemoteView](https://write.woa.com/document/87030026264555520) 接口无法播放指定用户的视频，需要调用 [muteRemoteVideoStream](https://write.woa.com/document/87030026264555520)(false) 或 [muteAllRemoteVideoStreams](https://write.woa.com/document/87030026264555520)(false) 才能恢复。
> 


## muteAllRemoteVideoStreams



#### 暂停/恢复订阅所有远端用户的视频流。

该接口仅暂停/恢复接收所有用户的视频流，但并不释放显示资源，视频画面会被冻屏在接口调用时的最后一帧。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >mute</td>

<td rowspan="1" colSpan="1" >是否暂停接收。</td>
</tr>
</table>


> **注意**
> 

> 该接口支持您在进入房间（[enterRoom](https://write.woa.com/document/87030026264555520)）前调用，暂停状态在退出房间（[exitRoom](https://write.woa.com/document/87030026264555520)）之后会被重置。
> 

> 调用该接口暂停接收所有用户的视频流后，只调用 [startRemoteView](https://write.woa.com/document/87030026264555520) 接口无法播放指定用户的视频，需要调用 [muteRemoteVideoStream](https://write.woa.com/document/87030026264555520)(false) 或 [muteAllRemoteVideoStreams](https://write.woa.com/document/87030026264555520)(false) 才能恢复。
> 


## setVideoEncoderParam



#### 设置视频编码器的编码参数。

该设置能够决定远端用户看到的画面质量，同时也能决定云端录制出的视频文件的画面质量。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >param</td>

<td rowspan="1" colSpan="1" >用于设置视频编码器的相关参数，详情请参见 [TRTCVideoEncParam](https://write.woa.com/document/87030132707430400)。</td>
</tr>
</table>


> **注意**
> 

> 从v11.5版本开始，编码输出分辨率会按照宽8高2字节对齐，并且是向下调整，eg:输入分辨率540x960，实际编码输出分辨率536x960。
> 


## setNetworkQosParam



#### 设置网络质量控制的相关参数。

该设置决定在差网络环境下的质量调控策略，如“画质优先”或“流畅优先”等策略。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >param</td>

<td rowspan="1" colSpan="1" >用于设置网络质量控制的相关参数，详情请参见 [TRTCNetworkQosParam](https://write.woa.com/document/87030132707430400)。</td>
</tr>
</table>


## setLocalRenderParams



#### 设置本地画面的渲染参数。

可设置的参数包括有：画面的旋转角度、填充模式以及左右镜像等。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >params</td>

<td rowspan="1" colSpan="1" >画面渲染参数，详情请参见 [TRTCRenderParams](https://write.woa.com/document/87030132707430400)。</td>
</tr>
</table>


## setRemoteRenderParams



#### 设置远端画面的渲染模式。

可设置的参数包括有：画面的旋转角度、填充模式以及左右镜像等。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >params</td>

<td rowspan="1" colSpan="1" >画面渲染参数，详情请参见 [TRTCRenderParams](https://write.woa.com/document/87030132707430400)。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >streamType</td>

<td rowspan="1" colSpan="1" >可以设置为主路画面（[TRTCVideoStreamTypeBig](https://write.woa.com/document/87030132707430400)）或辅路画面（[TRTCVideoStreamTypeSub](https://write.woa.com/document/87030132707430400)）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >指定远端用户的 ID。</td>
</tr>
</table>


## enableSmallVideoStream



#### 开启大小画面双路编码模式。

开启双路编码模式后，当前用户的编码器会同时输出【高清大画面】和【低清小画面】两路视频流（但只有一路音频流）。

如此以来，房间中的其他用户就可以根据自身的网络情况或屏幕大小选择订阅【高清大画面】或是【低清小画面】。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enable</td>

<td rowspan="1" colSpan="1" >是否开启小画面编码，默认值：false。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >smallVideoEncParam</td>

<td rowspan="1" colSpan="1" >小流的视频参数。</td>
</tr>
</table>


> **注意**
> 

> 双路编码开启后，会消耗更多的 CPU 和 网络带宽，所以 Mac、Windows 或者高性能 Pad 可以考虑开启，不建议手机端开启。
> 


#### 返回值说明：

0：成功；-1：当前大画面已被设置为较低画质，开启双路编码已无必要。

## setRemoteVideoStreamType



#### 切换指定远端用户的大小画面。

当房间中某个主播开启了双路编码之后，房间中其他用户通过 [startRemoteView](https://write.woa.com/document/87030026264555520) 订阅到的画面默认会是【高清大画面】。

您可以通过此接口选定希望订阅的画面是大画面还是小画面，该接口在 [startRemoteView](https://write.woa.com/document/87030026264555520) 之前和之后调用均可生效。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >streamType</td>

<td rowspan="1" colSpan="1" >视频流类型，即选择看大画面还是小画面，默认为大画面。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >指定远端用户的 ID。</td>
</tr>
</table>


> **注意**
> 

> 此功能需要目标用户已经通过 [enableSmallVideoStream](https://write.woa.com/document/87030026264555520) 提前开启了双路编码模式，否则此调用无实际效果。
> 


## snapshotVideo



#### 视频画面截图。

您可以通过本接口截取本地的视频画面，远端用户的主路画面以及远端用户的辅路（屏幕分享）画面。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >sourceType</td>

<td rowspan="1" colSpan="1" >画面来源，可选择截取视频流画面（[TRTCSnapshotSourceTypeStream](https://write.woa.com/document/87030132707430400)）、视频渲染画面（[TRTCSnapshotSourceTypeView](https://write.woa.com/document/87030132707430400)）或 采集画面（[TRTCSnapshotSourceTypeCapture](https://write.woa.com/document/87030132707430400)），采集画面截图更清晰。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >streamType</td>

<td rowspan="1" colSpan="1" >视频流类型，可选择截取主路画面（[TRTCVideoStreamTypeBig](https://write.woa.com/document/87030132707430400)，常用于摄像头）或辅路画面（[TRTCVideoStreamTypeSub](https://write.woa.com/document/87030132707430400)，常用于屏幕分享）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >用户 ID，如指定空置表示截取本地的视频画面。</td>
</tr>
</table>


> **注意**
> 

> Windows 平台目前仅支持截取 [TRTCSnapshotSourceTypeStream](https://write.woa.com/document/87030132707430400) 来源的视频画面。
> 


## setGravitySensorAdaptiveMode



#### 设置重力感应的适配模式（11.7 及以上版本）。

开启重力感应后，如果采集端的设备发生旋转，采集端和观众端的画面都会进行相应地渲染以确保视野中的画面始终朝上。

只在sdk内部摄像头采集场景生效，并且只在移动端生效。

1. 该接口仅对采集端起作用，如果只是观看房间中的画面，开启此接口是无效的

2. 当采集端设备发生 90 度或 270 度旋转时，采集端或者观众看到的画面可能会被裁剪以保持比例的协调
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >mode</td>

<td rowspan="1" colSpan="1" >重力感应模式，详情请参见 [TRTCGravitySensorAdaptiveMode_Disable](https://write.woa.com/document/87030132707430400)、[TRTCGravitySensorAdaptiveMode_FillByCenterCrop](https://write.woa.com/document/87030132707430400) 和 [TRTCGravitySensorAdaptiveMode_FitWithBlackBorder](https://write.woa.com/document/87030132707430400) 默认值：[TRTCGravitySensorAdaptiveMode_Disable](https://write.woa.com/document/87030132707430400)。</td>
</tr>
</table>


## startLocalAudio



#### 开启本地音频的采集和发布。

SDK 默认不开启麦克风，当用户需要发布本地音频时，需要调用该接口开启麦克风采集，并将音频编码并发布到当前的房间中。

开启本地音频的采集和发布后，房间中的其他用户会收到 [onUserAudioAvailable](https://write.woa.com/document/87030021158866944)(userId, true) 的通知。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >quality</td>

<td rowspan="1" colSpan="1" >声音音质<br>- [TRTCAudioQualitySpeech](https://write.woa.com/document/87030132707430400)，流畅：单声道；音频裸码率：18kbps；适合语音通话为主的场景，例如在线会议，语音通话。<br>- [TRTCAudioQualityDefault](https://write.woa.com/document/87030132707430400)，默认：单声道；音频裸码率：50kbps；SDK 默认的音频质量，如无特殊需求推荐选择之。<br>- [TRTCAudioQualityMusic](https://write.woa.com/document/87030132707430400)，高音质：双声道 + 全频带；音频裸码率：128kbps；适合需要高保真传输音乐的场景，例如在线K歌、音乐直播等。</td>
</tr>
</table>


> **注意**
> 

> 该函数会检查麦克风的使用权限，如果当前 App 没有麦克风权限，SDK 会自动向用户申请麦克风使用权限。
> 


## stopLocalAudio



#### 停止本地音频的采集和发布。

停止本地音频的采集和发布后，房间中的其他用户会收到 [onUserAudioAvailable](https://write.woa.com/document/87030021158866944)(userId, false) 的通知。

## muteLocalAudio



#### 暂停/恢复发布本地的音频流。

当您暂停发布本地音频流之后，房间中的其他用户会收到 [onUserAudioAvailable](https://write.woa.com/document/87030021158866944)(userId, false) 的通知。

当您恢复发布本地音频流之后，房间中的其他用户会收到 [onUserAudioAvailable](https://write.woa.com/document/87030021158866944)(userId, true) 的通知。



与 [stopLocalAudio](https://write.woa.com/document/87030026264555520) 的不同之处在于，` muteLocalAudio(true) ` 并不会释放麦克风权限，而是继续发送码率极低的静音包。

这对于需要云端录制的场景非常适用，因为 MP4 等格式的视频文件，对于音频数据的连续性要求很高，使用 [stopLocalAudio](https://write.woa.com/document/87030026264555520) 会导致录制出的 MP4 文件不易播放。

因此在对录制文件的质量要求较高的场景中，建议选择 ` muteLocalAudio ` 而不建议使用 [stopLocalAudio](https://write.woa.com/document/87030026264555520)。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >mute</td>

<td rowspan="1" colSpan="1" >true：静音；false：恢复。</td>
</tr>
</table>


## muteRemoteAudio



#### 暂停/恢复播放远端的音频流。

当您静音某用户的远端音频时，SDK 会停止播放指定用户的声音，同时也会停止拉取该用户的音频数据。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >mute</td>

<td rowspan="1" colSpan="1" >true：静音；false：取消静音。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >用于指定远端用户的 ID。</td>
</tr>
</table>


> **注意**
> 

> 在进入房间（[enterRoom](https://write.woa.com/document/87030026264555520)）之前或之后调用本接口均生效，静音状态在退出房间（[exitRoom](https://write.woa.com/document/87030026264555520)）之后会被重置为 false。
> 


## muteAllRemoteAudio



#### 暂停/恢复播放所有远端用户的音频流。

当您静音所有用户的远端音频时，SDK 会停止播放所有来自远端的音频流，同时也会停止拉取所有用户的音频数据。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >mute</td>

<td rowspan="1" colSpan="1" >true：静音；false：取消静音。</td>
</tr>
</table>


> **注意**
> 

> 在进入房间（[enterRoom](https://write.woa.com/document/87030026264555520)）之前或之后调用本接口均生效，静音状态在退出房间（[exitRoom](https://write.woa.com/document/87030026264555520)）之后会被重置为 false。
> 


## setRemoteAudioVolume



#### 设定某一个远端用户的声音播放音量。

您可以通过 ` setRemoteAudioVolume(userId, 0) ` 将某一个远端用户的声音静音。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >用于指定远端用户的 ID。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >volume</td>

<td rowspan="1" colSpan="1" >音量大小，取值范围为 [0, 150]，默认值：100。</td>
</tr>
</table>


> **注意**
> 

> 如果将 ` volume ` 设置成 100 之后感觉音量还是太小，可以将 ` volume ` 最大设置成 150，但超过 100 的 ` volume ` 会有爆音的风险，请谨慎操作。
> 


## setAudioCaptureVolume



#### 设定本地音频的采集音量。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >volume</td>

<td rowspan="1" colSpan="1" >音量大小，取值范围为 [0, 150]；默认值：100。</td>
</tr>
</table>


> **注意**
> 

> 如果将 ` volume ` 设置成 100 之后感觉音量还是太小，可以将 ` volume ` 最大设置成 150，但超过 100 的 ` volume ` 会有爆音的风险，请谨慎操作。
> 


## getAudioCaptureVolume



#### 获取本地音频的采集音量。

#### 返回值说明：

采集音量。

## setAudioPlayoutVolume



#### 设定远端音频的播放音量。

该接口会控制 SDK 最终交给系统播放的声音音量，调节效果会影响到本地音频录制文件的音量大小，但不会影响到耳返的音量大小。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >volume</td>

<td rowspan="1" colSpan="1" >音量大小，取值范围为 [0, 150]，默认值：100。</td>
</tr>
</table>


> **注意**
> 

> 如果将 volume 设置成 100 之后感觉音量还是太小，可以将 volume 最大设置成 150，但超过 100 的 volume 会有爆音的风险，请谨慎操作。
> 


## getAudioPlayoutVolume



#### 获取远端音频的播放音量。

## enableAudioVolumeEvaluation



#### 启用音量大小提示。

开启此功能后，SDK 会在 [ITRTCCloudCallback](https://write.woa.com/document/87030021158866944) 中的 [onUserVoiceVolume](https://write.woa.com/document/87030021158866944) 回调中反馈本地和远端用户的音频音量评估信息，包括音量大小、人声检测、音频频谱等。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enable</td>

<td rowspan="1" colSpan="1" >是否启用音量提示，默认为关闭状态。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >params</td>

<td rowspan="1" colSpan="1" >音量评估等相关参数，请参见 [TRTCAudioVolumeEvaluateParams](https://write.woa.com/document/87030132707430400)。</td>
</tr>
</table>


> **注意**
> 

> 如需启用音量大小提示，请在调用 [startLocalAudio](https://write.woa.com/document/87030026264555520) 之前调用该接口.
> 


## startAudioRecording



#### 开始录音。

当您调用该接口后， SDK 会将本地和远端的所有音频（包括本地音频，远端音频，背景音乐和音效等）混合并录制到一个本地文件中。

该接口在进入房间前后调用均可生效，如果录制任务在退出房间前尚未通过 [stopAudioRecording](https://write.woa.com/document/87030026264555520) 停止，则退出房间后录制任务会自动被停止。

本次录制的启动、完成状态会通过本地录制相关回调进行通知。参见 [ITRTCCloudCallback](https://write.woa.com/document/87030021158866944) 相关回调。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >param</td>

<td rowspan="1" colSpan="1" >录音参数，请参见 [TRTCAudioRecordingParams](https://write.woa.com/document/87030132707430400)。</td>
</tr>
</table>


> **注意**
> 

> 自 v11.5 版本，音频录制的状态结果由返回值统一调整为异步回调进行通知。参见 [ITRTCCloudCallback](https://write.woa.com/document/87030021158866944) 相关回调。
> 


#### 返回值说明：

0：成功；-1：录音已开始；-2：文件或目录创建失败；-3：后缀指定的音频格式不支持。

## stopAudioRecording



#### 停止录音。

如果录制任务在退出房间前尚未通过本接口停止，则退出房间后录音任务会自动被停止。

## startLocalRecording



#### 开启本地媒体录制。

开启后把直播过程中的音视频内容录制到本地的一个文件中，该功能不会产生额外费用。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >params</td>

<td rowspan="1" colSpan="1" >录制参数，请参见 [TRTCLocalRecordingParams](https://write.woa.com/document/87030132707430400)。</td>
</tr>
</table>


## stopLocalRecording



#### 停止本地媒体录制。

如果录制任务在退出房间前尚未通过本接口停止，则退出房间后录音任务会自动被停止。

## setRemoteAudioParallelParams



#### 设置远端音频流智能并发播放策略。

设置远端音频流智能并发播放策略，适用于上麦人数比较多的场景。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >params</td>

<td rowspan="1" colSpan="1" >音频并发参数，请参见 [TRTCAudioParallelParams](https://write.woa.com/document/87030132707430400)。</td>
</tr>
</table>


## enable3DSpatialAudioEffect



#### 启用 3D 音效。

启用 3D 音效。注意需使用流畅音质 [TRTCAudioQualitySpeech](https://write.woa.com/document/87030132707430400) 或默认音质 [TRTCAudioQualityDefault](https://write.woa.com/document/87030132707430400)。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enabled</td>

<td rowspan="1" colSpan="1" >是否启用 3D 音效，默认为关闭状态。</td>
</tr>
</table>


## updateSelf3DSpatialPosition



#### 设置 3D 音效中自身坐标及朝向信息。

更新自身在世界坐标系中的位置和朝向， SDK 会根据该方法参数计算自身和远端用户之间的相对位置，进而渲染出空间音效。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >axisForward</td>

<td rowspan="1" colSpan="1" >自身坐标系前轴在世界坐标系中的单位向量，三个值依次表示前、右、上坐标值。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >axisRight</td>

<td rowspan="1" colSpan="1" >自身坐标系右轴在世界坐标系中的单位向量，三个值依次表示前、右、上坐标值。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >axisUp</td>

<td rowspan="1" colSpan="1" >自身坐标系上轴在世界坐标系中的单位向量，三个值依次表示前、右、上坐标值。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >position</td>

<td rowspan="1" colSpan="1" >自身在世界坐标系中的坐标，三个值依次表示前、右、上坐标值。</td>
</tr>
</table>


> **注意**
> 

> 1. 各参数应分别传入长度为 3 的数组。
> 

> 2. 请适当限制调用频率，推荐两次坐标设置至少间隔 100ms。
> 


## updateRemote3DSpatialPosition



#### 设置 3D 音效中远端用户坐标信息。

更新远端用户在世界坐标系中的位置，SDK 会根据自身和远端用户之间的相对位置，进而渲染出空间音效。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >position</td>

<td rowspan="1" colSpan="1" >该远端用户在世界坐标系中的坐标，三个值依次表示前、右、上坐标值。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >指定远端用户的 ID。</td>
</tr>
</table>


> **注意**
> 

> 1. 各参数应分别传入长度为 3 的数组。
> 

> 2. 请适当限制调用频率，推荐同一远端用户两次坐标设置至少间隔 100ms。
> 


## set3DSpatialReceivingRange



#### 设置指定用户所发出声音的可被接收范围。

设置该范围大小之后，该指定用户的声音将在该范围内可被听见，超出该范围将被衰减为 0。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >range</td>

<td rowspan="1" colSpan="1" >声音最大可被接收范围。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >指定远端用户的 ID。</td>
</tr>
</table>


## getDeviceManager



#### 获取设备管理类（TXDeviceManager）。

通过设备管理，您可以设置摄像头、麦克风和扬声器等音视频相关的硬件设备功能。

#### 返回值说明：

设备管理类 TXDeviceManager。

## getBeautyManager



#### 获取美颜管理类（TXBeautyManager）。

通过美颜管理，您可以使用以下功能：
-  设置“磨皮”、“美白”、“红润”等美颜特效。

-  以下功能仅iOS/Android支持：

-  设置“大眼”、“瘦脸”、“V脸”、“下巴”、“短脸”、“小鼻”、“亮眼”、“白牙”、“祛眼袋”、“祛皱纹”、“祛法令纹”等修脸特效。

-  设置“发际线”、“眼间距”、“眼角”、“嘴形”、“鼻翼”、“鼻子位置”、“嘴唇厚度”、“脸型”等修脸特效。

-  设置“眼影”、“腮红”等美妆特效。

-  设置动态贴纸和人脸挂件等动画特效。


#### 返回值说明：

美颜管理类 TXBeautyManager。

## setWaterMark



#### 添加水印。

水印的位置是通过 xOffset, yOffset, fWidthRatio 来指定的。
-  xOffset：水印的坐标，取值范围为 [0, 1] 的浮点数。

-  yOffset：水印的坐标，取值范围为 [0, 1] 的浮点数。

-  fWidthRatio：水印的大小比例，取值范围为 [0, 1] 的浮点数。

<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >fWidthRatio</td>

<td rowspan="1" colSpan="1" >水印显示的宽度占画面宽度比例（水印按该参数等比例缩放显示）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >isVisibleOnLocalPreview</td>

<td rowspan="1" colSpan="1" >true：本地预览显示水印；false：本地预览不显示水印，仅在win/mac下生效。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >nHeight</td>

<td rowspan="1" colSpan="1" >水印图片像素高度（源数据为文件路径时忽略该参数）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >nWidth</td>

<td rowspan="1" colSpan="1" >水印图片像素宽度（源数据为文件路径时忽略该参数）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >srcData</td>

<td rowspan="1" colSpan="1" >水印图片源数据（传 nullptr 表示去掉水印）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >srcType</td>

<td rowspan="1" colSpan="1" >水印图片源数据类型。请参见 [TRTCWaterMarkSrcType](https://write.woa.com/document/87030132707430400)。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >streamType</td>

<td rowspan="1" colSpan="1" >要设置水印的流类型（[TRTCVideoStreamTypeBig](https://write.woa.com/document/87030132707430400)，[TRTCVideoStreamTypeSub](https://write.woa.com/document/87030132707430400)）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >xOffset</td>

<td rowspan="1" colSpan="1" >水印显示的左上角 x 轴偏移。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >yOffset</td>

<td rowspan="1" colSpan="1" >水印显示的左上角 y 轴偏移。</td>
</tr>
</table>


> **注意**
> 

> 本接口只支持给主路视频添加图片水印。
> 


## getAudioEffectManager



#### 获取音效管理类（TXAudioEffectManager）。

TXAudioEffectManager 是音效管理接口，您可以通过该接口实现如下功能：
-  背景音乐：支持在线音乐和本地音乐，支持变速、变调等特效、支持原生和伴奏并播放和循环播放。

-  耳机耳返：麦克风捕捉的声音实时通过耳机播放，常用于音乐直播。

-  混响效果：KTV、小房间、大会堂、低沉、洪亮等。

-  变声特效：萝莉、大叔、重金属等。

-  短音效：鼓掌声、欢笑声等简短的音效文件（对于小于10秒的文件，请将 isShortFile 参数设置为 true）。


#### 返回值说明：

音效管理类 TXAudioEffectManager。

## startSystemAudioLoopback



#### 开启系统声音采集（iOS 端暂未支持）。

该接口会从电脑的声卡中采集音频数据，并将其混入到 SDK 当前的音频数据流中，从而使房间中的其他用户也能听到主播的电脑所播放出的声音。

在线教育场景中，老师可以使用此功能让 SDK 采集教学影片中的声音，并广播给同房间中的学生。

音乐直播场景中，主播可以使用此功能让 SDK 采集音乐播放器中的音乐，从而为自己的直播间增加背景音乐。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >deviceName</td>

<td rowspan="1" colSpan="1" >您可以指定该参数为空值（nullptr），代表让 SDK 采集整个系统的声音。</td>
</tr>
</table>


> **注意**
> 

> 在 Windows 平台下，您也可以将参数 ` deviceName ` 设置为某个应用程序的可执行文件（如 QQMuisc.exe）的绝对路径，此时 SDK 只会采集该应用程序的声音（支持 32 位版本的 SDK，64 位版本的 SDK 需要满足 Windows 版本为 10.0.19042 或更高版本）。
> 

> 您也可以指定该参数为某个扬声器设备的名称来采集特定扬声器声音（通过接口 TXDeviceManager 中的 getDevicesList 接口，可以获取类型为 [TXMediaDeviceTypeSpeaker](https://write.woa.com/document/87030115247763456) 的扬声器设备）。
> 

> 在 Windows 平台下您也可以指定该参数为某个进程的进程 id（格式为 “process_xxx”，其中 xxx 为进程 id），此时 SDK 知会采集该进程的声音（需要满足 Windows 版本为 10.0.19042或更高版本）。
> 

> 在 Windows 平台下您也可以指定该参数为某个进程的进程 id（格式为 “exclude_process_xxx”，其中 xxx 为进程 id），此时 SDK 会采集除了该进程的其他所有声音（需要满足 Windows 版本为 10.0.19042或更高版本）。
> 


## stopSystemAudioLoopback



#### 停止系统声音采集（iOS 端暂未支持）。

## setSystemAudioLoopbackVolume



#### 设置系统声音的采集音量。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >volume</td>

<td rowspan="1" colSpan="1" >设置的音量大小，范围是：[0, 150]，默认值为 100。</td>
</tr>
</table>


## startScreenCapture



#### 启动屏幕分享。

该接口可以抓取整个屏幕的内容，或抓取您指定的某个应用的窗口内容，并将其分享给同房间中的其他用户。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >encParam</td>

<td rowspan="1" colSpan="1" >屏幕分享的画面编码参数，SDK 会优先使用您通过此接口设置的编码参数：<br>-  如果您设置 ` encParam ` 为空值，且您已通过 [setSubStreamEncoderParam](https://write.woa.com/document/87030026264555520) 设置过辅路视频编码参数，SDK 将使用您设置过的辅路编码参数进行屏幕分享。<br>-  如果您设置 ` encParam ` 为空值，且您未通过 [setSubStreamEncoderParam](https://write.woa.com/document/87030026264555520) 设置过辅路视频编码参数，SDK 将自动选择一个最佳的编码参数进行屏幕分享。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >streamType</td>

<td rowspan="1" colSpan="1" >屏幕分享使用的线路，可以设置为主路（TRTCVideoStreamTypeBig）或者辅路（TRTCVideoStreamTypeSub），推荐使用辅路。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >view</td>

<td rowspan="1" colSpan="1" >渲染控件所在的父控件，可以设置为空值，表示不显示屏幕分享的预览效果。</td>
</tr>
</table>


> **注意**
> 

> 1. 同一个用户同时最多只能发布一路主路（[TRTCVideoStreamTypeBig](https://write.woa.com/document/87030132707430400)）画面和一路辅路（[TRTCVideoStreamTypeSub](https://write.woa.com/document/87030132707430400)）画面。
> 

> 2. 默认情况下，屏幕分享使用辅路画面。如果使用主路做屏幕分享，您需要提前停止摄像头采集（[stopLocalPreview](https://write.woa.com/document/87030026264555520)）以避免相互冲突。
> 

> 3. 同一个房间中同时只能有一个用户使用辅路做屏幕分享，也就是说，同一个房间中同时只允许一个用户开启辅路。
> 

> 4. 当房间中已经有其他用户在使用辅路分享屏幕时，此时调用该接口会收到来自 [ITRTCCloudCallback](https://write.woa.com/document/87030021158866944) 的 ` onError(ERR_SERVER_CENTER_ANOTHER_USER_PUSH_SUB_VIDEO) ` 回调。
> 


## stopScreenCapture



#### 停止屏幕分享。

## pauseScreenCapture



#### 暂停屏幕分享。

> **注意**
> 

> 从v11.5版本开始，暂停屏幕采集会使用最后一帧按照 1 fps 帧率输出。
> 


## resumeScreenCapture



#### 恢复屏幕分享。

## getScreenCaptureSources



#### 枚举可分享的屏幕和窗口（该接口仅支持桌面系统）。

当您在对接桌面端系统的屏幕分享功能时，一般都需要展示一个选择分享目标的界面，这样用户能够使用这个界面选择是分享整个屏幕还是某个窗口。

通过本接口，您就可以查询到当前系统中可用于分享的窗口的 ID、名称以及缩略图。我们在 Demo 中提供了一份默认的界面实现供您参考。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >iconSize</td>

<td rowspan="1" colSpan="1" >指定要获取的窗口图标大小。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >thumbnailSize</td>

<td rowspan="1" colSpan="1" >指定要获取的窗口缩略图大小，缩略图可用于绘制在窗口选择界面上。</td>
</tr>
</table>


> **注意**
> 

> 1. 返回的列表中包含屏幕和应用窗口，屏幕是列表中的第一个元素。如果用户有多个显示器，那么每个显示器都是一个分享目标。
> 

> 2. 请不要使用 ` delete ITRTCScreenCaptureSourceList* ` 删除 SourceList，这很容易导致崩溃，请使用 ITRTCScreenCaptureSourceList 中的 release 方法释放列表。
> 


#### 返回值说明：

窗口列表包括屏幕。

## selectScreenCaptureTarget



#### 选取要分享的屏幕或窗口（该接口仅支持桌面系统）。

当您通过 [getScreenCaptureSources](https://write.woa.com/document/87030026264555520) 获取到可以分享的屏幕和窗口之后，您可以调用该接口选定期望分享的目标屏幕或目标窗口。

在屏幕分享的过程中，您也可以随时调用该接口以切换分享目标。



支持如下四种情况：
-  共享整个屏幕：source 中 type 为 [TRTCScreenCaptureSourceTypeScreen](https://write.woa.com/document/87030132707430400) 的 source，captureRect 设为 { 0, 0, 0, 0 }。

-  共享指定区域：source 中 type 为 [TRTCScreenCaptureSourceTypeScreen](https://write.woa.com/document/87030132707430400) 的 source，captureRect 设为非 nullptr，例如 { 100, 100, 300, 300 }。

-  共享整个窗口：source 中 type 为 [TRTCScreenCaptureSourceTypeWindow](https://write.woa.com/document/87030132707430400) 的 source，captureRect 设为 { 0, 0, 0, 0 }。

-  共享窗口区域：source 中 type 为 [TRTCScreenCaptureSourceTypeWindow](https://write.woa.com/document/87030132707430400) 的 source，captureRect 设为非 nullptr，例如 { 100, 100, 300, 300 }。

<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >captureRect</td>

<td rowspan="1" colSpan="1" >指定捕获的区域。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >property</td>

<td rowspan="1" colSpan="1" >指定屏幕分享目标的属性，包括捕获鼠标，高亮捕获窗口等，详情参考 [TRTCScreenCaptureProperty](https://write.woa.com/document/87030132707430400)。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >source</td>

<td rowspan="1" colSpan="1" >指定分享源。详情参考 [TRTCScreenCaptureSourceInfo](https://write.woa.com/document/87030132707430400)</td>
</tr>
</table>


> **注意**
> 

> 设置高亮边框颜色、宽度参数在 Mac 平台不生效。
> 


## setSubStreamEncoderParam



#### 设置屏幕分享（即辅路）的视频编码参数（桌面系统和移动系统均已支持）。

该接口可以设定远端用户所看到的屏幕分享（即辅路）的画面质量，同时也能决定云端录制出的视频文件中屏幕分享的画面质量。

请注意如下两个接口的差异：
- [setVideoEncoderParam](https://write.woa.com/document/87030026264555520) 用于设置主路画面（[TRTCVideoStreamTypeBig](https://write.woa.com/document/87030132707430400)，一般用于摄像头）的视频编码参数。

- [setSubStreamEncoderParam](https://write.woa.com/document/87030026264555520) 用于设置辅路画面（[TRTCVideoStreamTypeSub](https://write.woa.com/document/87030132707430400)，一般用于屏幕分享）的视频编码参数。

<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >param</td>

<td rowspan="1" colSpan="1" >辅流编码参数，详情请参见 [TRTCVideoEncParam](https://write.woa.com/document/87030132707430400)。</td>
</tr>
</table>


## setSubStreamMixVolume



#### 设置屏幕分享时的混音音量大小（该接口仅支持桌面系统）。

这个数值越高，屏幕分享音量的占比就越高，麦克风音量占比就越小，所以不推荐设置得太大，否则会导致麦克风的声音被压制。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >volume</td>

<td rowspan="1" colSpan="1" >设置的混音音量大小，范围 [0, 150]。</td>
</tr>
</table>


## addExcludedShareWindow



#### 将指定窗口加入屏幕分享的排除列表中（该接口仅支持桌面系统）。

加入排除列表中的窗口不会被分享出去，常见的用法是将某个应用的窗口加入到排除列表中以避免隐私问题。

支持启动屏幕分享前设置过滤窗口，也支持屏幕分享过程中动态添加过滤窗口。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >windowID</td>

<td rowspan="1" colSpan="1" >不希望分享出去的窗口</td>
</tr>
</table>


> **注意**
> 

> 1. 该接口只有在 [TRTCScreenCaptureSourceInfo](https://write.woa.com/document/87030132707430400) 中的 type 指定为 [TRTCScreenCaptureSourceTypeScreen](https://write.woa.com/document/87030132707430400) 时生效，即只有在分享整个屏幕内容时，排除指定窗口的功能才生效。
> 

> 2. 使用该接口添加到排除列表中的窗口会在退出房间后被 SDK 自动清除。
> 

> 3. Mac 平台下请传入窗口 ID（即 CGWindowID），您可以通过 [TRTCScreenCaptureSourceInfo](https://write.woa.com/document/87030132707430400) 中的 ` sourceId ` 成员获得。
> 


## removeExcludedShareWindow



#### 将指定窗口从屏幕分享的排除列表中移除（该接口仅支持桌面系统）。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >windowID</td>

<td rowspan="1" colSpan="1" >要排除的窗口 id。</td>
</tr>
</table>


## removeAllExcludedShareWindow



#### 将所有窗口从屏幕分享的排除列表中移除（该接口仅支持桌面系统）。

## addIncludedShareWindow



#### 将指定窗口加入屏幕分享的包含列表中（该接口仅支持桌面系统）。

该接口只有在 [TRTCScreenCaptureSourceInfo](https://write.woa.com/document/87030132707430400) 中的 type 指定为 [TRTCScreenCaptureSourceTypeWindow](https://write.woa.com/document/87030132707430400) 时生效。即只有在分享窗口内容时，额外包含指定窗口的功能才生效。

您在 [startScreenCapture](https://write.woa.com/document/87030026264555520) 之前和之后调用均可。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >windowID</td>

<td rowspan="1" colSpan="1" >希望被分享出去的窗口（Windows 平台下为窗口句柄： HWND）</td>
</tr>
</table>


> **注意**
> 

> 通过该方法添加到包含列表中的窗口，会在退出房间后被 SDK 自动清除。
> 


## removeIncludedShareWindow



#### 将指定窗口从屏幕分享的包含列表中移除（该接口仅支持桌面系统）。

该接口只有在 [TRTCScreenCaptureSourceInfo](https://write.woa.com/document/87030132707430400) 中的 type 指定为 [TRTCScreenCaptureSourceTypeWindow](https://write.woa.com/document/87030132707430400) 时生效。

即只有在分享窗口内容时，额外包含指定窗口的功能才生效。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >windowID</td>

<td rowspan="1" colSpan="1" >希望被分享出去的窗口（Mac 平台：窗口 ID；Windows 平台：HWND）</td>
</tr>
</table>


## removeAllIncludedShareWindow



#### 将全部窗口从屏幕分享的包含列表中移除（该接口仅支持桌面系统）。

该接口只有在 [TRTCScreenCaptureSourceInfo](https://write.woa.com/document/87030132707430400) 中的 type 指定为 [TRTCScreenCaptureSourceTypeWindow](https://write.woa.com/document/87030132707430400) 时生效。

即只有在分享窗口内容时，额外包含指定窗口的功能才生效。

## enableCustomVideoCapture



#### 启用/关闭视频自定义采集模式。

开启该模式后，SDK 不再运行原有的视频采集流程，即不再继续从摄像头采集数据和美颜，而是只保留视频编码和发送能力。

您需要通过 [sendCustomVideoData](https://write.woa.com/document/87030026264555520) 不断地向 SDK 塞入自己采集的视频画面。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enable</td>

<td rowspan="1" colSpan="1" >是否启用视频自定义采集，默认值：false。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >streamType</td>

<td rowspan="1" colSpan="1" >用于指定视频流类型，[TRTCVideoStreamTypeBig](https://write.woa.com/document/87030132707430400)：高清大画面；[TRTCVideoStreamTypeSub](https://write.woa.com/document/87030132707430400)：辅路画面。</td>
</tr>
</table>


## sendCustomVideoData



#### 向 SDK 投送自己采集的视频帧。

使用此接口可以向 SDK 投送自己采集的视频帧，SDK 会将视频帧进行编码并通过自身的网络模块传输出去。



参数 [TRTCVideoFrame](https://write.woa.com/document/87030132707430400) 推荐下列填写方式（其他字段不需要填写）：
-  pixelFormat：Windows 和 Android 平台仅支持 [TRTCVideoPixelFormat_I420](https://write.woa.com/document/87030132707430400)，iOS 和 Mac平台支持 [TRTCVideoPixelFormat_I420](https://write.woa.com/document/87030132707430400) 和 [TRTCVideoPixelFormat_BGRA32](https://write.woa.com/document/87030132707430400)。

-  bufferType：推荐选择 [TRTCVideoBufferType_Buffer](https://write.woa.com/document/87030132707430400)。

-  data：用于承载视频帧数据的 buffer。

-  length：视频帧数据长度，如果 pixelFormat 设定为 I420 格式，length 可以按照如下公式计算：` length = width × height × 3 / 2 `。

-  width：视频图像的宽度，如 640 px。

-  height：视频图像的高度，如 480 px。

-  timestamp：时间戳，单位为毫秒（ms），请使用视频帧在采集时被记录下来的时间戳（可以在采集到一帧视频帧之后，通过调用 [generateCustomPTS](https://write.woa.com/document/87030026264555520) 获取时间戳）。




参考文档：[自定义采集和渲染](https://cloud.tencent.com/document/product/647/34066)。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >frame</td>

<td rowspan="1" colSpan="1" >视频数据，支持 I420 格式数据。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >streamType</td>

<td rowspan="1" colSpan="1" >用于指定视频流类型，[TRTCVideoStreamTypeBig](https://write.woa.com/document/87030132707430400)： 高清大画面；[TRTCVideoStreamTypeSub](https://write.woa.com/document/87030132707430400)： 辅路画面。</td>
</tr>
</table>


> **注意**
> 

> 1. 推荐您在采集到的一帧视频帧后，即调用 [generateCustomPTS](https://write.woa.com/document/87030026264555520) 接口获取该帧的 timestamp 数值，这样可以获得最佳的音画同步效果。
> 

> 2. SDK 最终编码出的视频帧率并不是由您调用本接口的频率决定的，而是由您在 [setVideoEncoderParam](https://write.woa.com/document/87030026264555520) 中所设置的 FPS 决定的。
> 

> 3. 请尽量保持本接口的调用间隔是均匀的，否则会导致编码器输出帧率不稳或者音画不同步等问题。
> 

> 4. iOS 和 Mac平台目前支持传入 [TRTCVideoPixelFormat_I420](https://write.woa.com/document/87030132707430400) 或 [TRTCVideoPixelFormat_BGRA32](https://write.woa.com/document/87030132707430400) 格式的视频帧。
> 

> 5. Windows 和 Android 平台目前仅支持传入 [TRTCVideoPixelFormat_I420](https://write.woa.com/document/87030132707430400) 格式的视频帧。
> 


## enableCustomAudioCapture



#### 启用音频自定义采集模式。

开启该模式后，SDK 不再运行原有的音频采集流程，即不再继续从麦克风采集音频数据，而是只保留音频编码和发送能力。

您需要通过 [sendCustomAudioData](https://write.woa.com/document/87030026264555520) 不断地向 SDK 塞入自己采集的音频数据。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enable</td>

<td rowspan="1" colSpan="1" >是否启用音频自定义采集模式，默认值：false。</td>
</tr>
</table>


> **注意**
> 

> 由于回声抵消（AEC）需要严格的控制声音采集和播放的时间，所以开启自定义音频采集后，AEC 能力可能会失效。
> 


## sendCustomAudioData



#### 向 SDK 投送自己采集的音频数据。

参数 [TRTCAudioFrame](https://write.woa.com/document/87030132707430400) 推荐下列填写方式（其他字段不需要填写）：
-  audioFormat：音频数据格式，仅支持 TRTCAudioFrameFormatPCM。

-  data：音频帧 buffer。音频帧数据只支持 PCM 格式，支持 5-100 ms 帧长，推荐使用 20ms 帧长，长度计算方法：48000采样率，单声道的帧长度：` 48000 × 0.02s × 1 × 16bit = 15360bit = 1920字节 `。

-  sampleRate：采样率，支持：16000、24000、32000、44100、48000。

-  channel：声道数（如果是立体声，数据是交叉的），单声道：1； 双声道：2。

-  timestamp：时间戳，单位为毫秒（ms），请使用音频帧在采集时被记录下来的时间戳（可以在采集到一帧音频帧之后，通过调用 [generateCustomPTS](https://write.woa.com/document/87030026264555520) 获取时间戳）。




参考文档：[自定义采集和渲染](https://cloud.tencent.com/document/product/647/74692)。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >frame</td>

<td rowspan="1" colSpan="1" >音频数据</td>
</tr>
</table>


> **注意**
> 

> 请您精准地按每帧时长的间隔调用本接口，数据投送间隔不均匀时极易触发声音卡顿。
> 


## enableMixExternalAudioFrame



#### 启用/关闭自定义音轨。

开启后，您可以通过本接口向 SDK 混入一条自定义的音轨。通过两个布尔型参数，您可以控制该音轨是否要在远端和本地播放。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enablePlayout</td>

<td rowspan="1" colSpan="1" >控制混入的音轨是否要在本地播放，默认值：false。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enablePublish</td>

<td rowspan="1" colSpan="1" >控制混入的音轨是否要在远端播放，默认值：false。</td>
</tr>
</table>


> **注意**
> 

> 如果您指定参数 ` enablePublish ` 和 ` enablePlayout ` 均为 false，代表完全关闭您的自定义音轨。
> 


## mixExternalAudioFrame



#### 向 SDK 混入自定义音轨。

调用该接口之前，您需要先通过 [enableMixExternalAudioFrame](https://write.woa.com/document/87030026264555520) 开启自定义音轨，之后就可以通过本接口将自己的音轨以 PCM 格式混入到 SDK 中。

理想情况下，我们期望您的代码能够以非常均匀的速度向 SDK 提供音轨数据。但我们也非常清楚，完美的调用间隔是一个巨大的挑战。

所以 SDK 内部会开启一个音轨数据的缓冲区，该缓冲区的作用类似一个“蓄水池”，它能够暂存您传入的音轨数据，平抑由于接口调用间隔的抖动问题。

本接口的返回值代表这个音轨缓冲区的大小，单位是毫秒（ms），例如：如果该接口返回 50，则代表当前的音轨缓冲区有 50ms 的音轨数据。因此只要您在 50ms 内再次调用本接口，SDK 就能保证您混入的音轨数据是连续的。

当您调用该接口后，如果发现返回值大于 100ms，则可以等待一帧音频帧的播放时间之后再次调用；如果返回值小于 100ms，则代表缓冲区比较小，您可以再次混入一些音轨数据以确保音轨缓冲区的大小维持在“安全水位”以上。



参数 [TRTCAudioFrame](https://write.woa.com/document/87030132707430400) 推荐下列填写方式（其他字段不需要填写）：
-  data：音频帧 buffer。音频帧数据只支持 PCM 格式，支持 5ms - 100ms 帧长，推荐使用 20ms 帧长，长度计算方法：48000采样率, 单声道的帧长度：` 48000 × 0.02s × 1 × 16bit = 15360bit = 1920字节 `。

-  sampleRate：采样率，支持：16000、24000、32000、44100、48000。

-  channel：声道数（如果是立体声，数据是交叉的），单声道：1； 双声道：2。

-  timestamp：时间戳，单位为毫秒（ms），请使用音频帧在采集时被记录下来的时间戳（可以在获得一帧音频帧之后，通过调用 [generateCustomPTS](https://write.woa.com/document/87030026264555520) 获得时间戳）。

<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >frame</td>

<td rowspan="1" colSpan="1" >音频数据</td>
</tr>
</table>


> **注意**
> 

> 请您精准地按每帧时长的间隔调用本接口，数据投送间隔不均匀时极易触发声音卡顿。
> 


#### 返回值说明：

>= 0 缓冲的长度，单位：ms。< 0 错误（-1 未启用 ` mixExternalAudioFrame `）

## setMixExternalAudioVolume



#### 设置推流时混入外部音频的推流音量和播放音量。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >playoutVolume</td>

<td rowspan="1" colSpan="1" >设置的播放音量大小，范围 [0, 150]，-1 表示不改变。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >publishVolume</td>

<td rowspan="1" colSpan="1" >设置的推流音量大小，范围 [0, 150]，-1 表示不改变。</td>
</tr>
</table>


## generateCustomPTS



#### 生成自定义采集时的时间戳。

本接口仅适用于自定义采集模式，用于解决音视频帧的采集时间（capture time）和投送时间（send time）不一致所导致的音画不同步问题。



当您通过 [sendCustomVideoData](https://write.woa.com/document/87030026264555520) 或 [sendCustomAudioData](https://write.woa.com/document/87030026264555520) 等接口进行自定义视频或音频采集时，请按照如下操作使用该接口：

1. 首先，在采集到一帧视频或音频帧时，通过调用本接口获得当时的 PTS 时间戳。

2. 之后可以将该视频或音频帧送入您使用的前处理模块（如第三方美颜组件，或第三方音效组件）。

3. 在真正调用 [sendCustomVideoData](https://write.woa.com/document/87030026264555520) 或 [sendCustomAudioData](https://write.woa.com/document/87030026264555520) 进行投送时，请将该帧在采集时记录的 PTS 时间戳赋值给 [TRTCVideoFrame](https://write.woa.com/document/87030132707430400) 或 [TRTCAudioFrame](https://write.woa.com/document/87030132707430400) 中的 timestamp 字段。

#### 返回值说明：

时间戳（单位：ms）

## enableLocalVideoCustomProcess



#### .1 开启视频第三方美颜。

开启后，您可以通过 [ITRTCVideoFrameCallback](https://write.woa.com/document/87030021158866944) 获取到指定像素格式和视频数据结构类型的图像帧。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >bufferType</td>

<td rowspan="1" colSpan="1" >指定视频数据结构类型。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enable</td>

<td rowspan="1" colSpan="1" >是否启用视频第三方美颜，默认为关闭状态。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >pixelFormat</td>

<td rowspan="1" colSpan="1" >指定回调的像素格式。</td>
</tr>
</table>


#### 返回值说明：

0：成功；<0：错误

## setLocalVideoCustomProcessCallback



#### .2 设置第三方美颜的视频数据回调。

设置该回调之后，SDK 会把采集到的视频帧通过您设置的 callback 回调出来，用于第三方美颜组件进行二次处理，之后 SDK 会将处理后的视频帧进行编码和发送。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >callback</td>

<td rowspan="1" colSpan="1" >自定义美颜回调，详见 [ITRTCVideoFrameCallback](https://write.woa.com/document/87030021158866944)。</td>
</tr>
</table>


## setLocalVideoRenderCallback



#### 设置本地视频自定义渲染回调。

设置该回调之后，SDK 内部会跳过原来的渲染流程，并把采集到的数据回调出来，您需要自己完成画面渲染。
-  您可以通过调用 ` setLocalVideoRenderCallback(TRTCVideoPixelFormat_Unknown, TRTCVideoBufferType_Unknown, nullptr) ` 停止回调。

-  iOS、Mac、Windows 平台目前仅支持回调 [TRTCVideoPixelFormat_I420](https://write.woa.com/document/87030132707430400) 或 [TRTCVideoPixelFormat_BGRA32](https://write.woa.com/document/87030132707430400) 像素格式的视频帧。

-  Android 平台目前仅支持传入 [TRTCVideoPixelFormat_I420](https://write.woa.com/document/87030132707430400), [TRTCVideoPixelFormat_RGBA32](https://write.woa.com/document/87030132707430400) 或 [TRTCVideoPixelFormat_Texture_2D](https://write.woa.com/document/87030132707430400) 像素格式的视频帧。

<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >bufferType</td>

<td rowspan="1" colSpan="1" >指定视频数据结构类型</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >callback</td>

<td rowspan="1" colSpan="1" >自定义渲染回调</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >pixelFormat</td>

<td rowspan="1" colSpan="1" >指定回调的像素格式</td>
</tr>
</table>


#### 返回值说明：

0：成功；<0：错误（详见 [错误码](https://cloud.tencent.com/document/product/647/38308)）。

## setRemoteVideoRenderCallback



#### 设置远端视频自定义渲染回调。

设置该回调之后，SDK 内部会跳过原来的渲染流程，并把采集到的数据回调出来，您需要自己完成画面渲染。
-  您可以通过调用 ` setRemoteVideoRenderCallback(TRTCVideoPixelFormat_Unknown, TRTCVideoBufferType_Unknown, nullptr) ` 停止回调。

-  iOS、Mac、Windows 平台目前仅支持回调 [TRTCVideoPixelFormat_I420](https://write.woa.com/document/87030132707430400) 或 [TRTCVideoPixelFormat_BGRA32](https://write.woa.com/document/87030132707430400) 像素格式的视频帧。

-  Android 平台目前仅支持传入 [TRTCVideoPixelFormat_I420](https://write.woa.com/document/87030132707430400), [TRTCVideoPixelFormat_RGBA32](https://write.woa.com/document/87030132707430400) 或 [TRTCVideoPixelFormat_Texture_2D](https://write.woa.com/document/87030132707430400) 像素格式的视频帧。

<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >bufferType</td>

<td rowspan="1" colSpan="1" >指定视频数据结构类型，目前只支持 [TRTCVideoBufferType_Buffer](https://write.woa.com/document/87030132707430400)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >callback</td>

<td rowspan="1" colSpan="1" >自定义渲染回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >pixelFormat</td>

<td rowspan="1" colSpan="1" >指定回调的像素格式</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >远端用户id</td>
</tr>
</table>


> **注意**
> 

> 实际使用时，需要先调用 startRemoteView(userid, nullptr) 来获取远端用户的视频流（view 设置为 nullptr 即可），否则不会有数据回调出来。
> 


#### 返回值说明：

0：成功；< 0：错误（详见 [错误码](https://cloud.tencent.com/document/product/647/38308)）。

## setAudioFrameCallback



#### 设置音频数据自定义回调。

设置该回调之后，SDK 内部会把音频数据（PCM 格式）回调出来，包括：
- [onCapturedAudioFrame](https://write.woa.com/document/87030021158866944)：本地麦克风采集到的音频数据回调

- [onLocalProcessedAudioFrame](https://write.woa.com/document/87030021158866944)：本地采集并经过音频模块前处理后的音频数据回调

- [onPlayAudioFrame](https://write.woa.com/document/87030021158866944)：混音前的每一路远程用户的音频数据

- [onMixedPlayAudioFrame](https://write.woa.com/document/87030021158866944)：将各路音频混合之后并最终要由系统播放出的音频数据回调


> **注意**
> 

> 设置回调为空即代表停止自定义音频回调，反之，设置回调不为空则代表启动自定义音频回调。
> 


## setCapturedAudioFrameCallbackFormat



#### 设置本地麦克风采集出的音频帧回调格式。

本接口用于设置 [onCapturedAudioFrame](https://write.woa.com/document/87030021158866944) 回调出来的 AudioFrame 的格式：
-  sampleRate：采样率，支持：16000、32000、44100、48000。

-  channel：声道数（如果是立体声，数据是交叉的），单声道：1； 双声道：2。

-  samplesPerCall：采样点数，定义回调数据帧长。帧长必须为 10ms 的整数倍。




如果希望用毫秒数计算回调帧长，则将毫秒数转换成采样点数的公式为：` 采样点数 = 毫秒数 * 采样率 / 1000 `。

举例：48000Hz 采样率希望回调 20ms 帧长的数据，则采样点数应该填：` 960 = 20 * 48000 / 1000 `。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >format</td>

<td rowspan="1" colSpan="1" >音频数据回调格式。</td>
</tr>
</table>


> **注意**
> 

> 最终回调的帧长度是以字节为单位，采样点数转换成字节数的计算公式为：` 字节数 = 采样点数 * channel * 2（位宽） `。举例：48000Hz 采样率，双声道，20ms 帧长，采样点数为 960，字节数为 ` 3840 = 960 * 2 * 2 `。
> 


#### 返回值说明：

0：成功；<0：错误。

## setLocalProcessedAudioFrameCallbackFormat



#### 设置经过前处理后的本地音频帧回调格式。

本接口用于设置 [onLocalProcessedAudioFrame](https://write.woa.com/document/87030021158866944) 回调出来的 AudioFrame 的格式：
-  sampleRate：采样率，支持：16000、32000、44100、48000。

-  channel：声道数（如果是立体声，数据是交叉的），单声道：1； 双声道：2。

-  samplesPerCall：采样点数，定义回调数据帧长。帧长必须为 10ms 的整数倍。




如果希望用毫秒数计算回调帧长，则将毫秒数转换成采样点数的公式为：` 采样点数 = 毫秒数 * 采样率 / 1000 `。

举例：48000Hz 采样率希望回调20ms帧长的数据，则采样点数应该填: ` 960 = 20 * 48000 / 1000 `。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >format</td>

<td rowspan="1" colSpan="1" >音频数据回调格式。</td>
</tr>
</table>


> **注意**
> 

> 最终回调的帧长度是以字节为单位，采样点数转换成字节数的计算公式为：` 字节数 = 采样点数 * channel * 2（位宽） `。 举例：48000Hz 采样率，双声道，20ms 帧长，采样点数为 960，字节数为 ` 3840 = 960 * 2 * 2 `。
> 


#### 返回值说明：

0：成功；<0：错误。

## setMixedPlayAudioFrameCallbackFormat



#### 设置最终要由系统播放出的音频帧回调格式。

本接口用于设置 [onMixedPlayAudioFrame](https://write.woa.com/document/87030021158866944) 回调出来的 AudioFrame 的格式：
-  sampleRate：采样率，支持：16000、32000、44100、48000。

-  channel：声道数（如果是立体声，数据是交叉的），单声道：1； 双声道：2。

-  samplesPerCall：采样点数，定义回调数据帧长。帧长必须为 10ms 的整数倍。




如果希望用毫秒数计算回调帧长，则将毫秒数转换成采样点数的公式为：` 采样点数 = 毫秒数 * 采样率 / 1000 `。

举例：48000Hz 采样率希望回调 20ms 帧长的数据，则采样点数应该填: ` 960 = 20 * 48000 / 1000 `。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >format</td>

<td rowspan="1" colSpan="1" >音频数据回调格式。</td>
</tr>
</table>


> **注意**
> 

> 最终回调的帧长度是以字节为单位，采样点数转换成字节数的计算公式为：` 字节数 = 采样点数 * channel * 2（位宽） `。 举例：48000Hz 采样率，双声道，20ms 帧长，采样点数为 960，字节数为 ` 3840 = 960 * 2 * 2 `。
> 


#### 返回值说明：

0：成功；<0：错误。

## enableCustomAudioRendering



#### 开启音频自定义播放。

如果您需要外接一些特定的音频设备，或者希望自己掌控音频的播放逻辑，您可以通过该接口启用音频自定义播放。

启用音频自定义播放后，SDK 将不再调用系统的音频接口播放数据，您需要通过 [getCustomAudioRenderingFrame](https://write.woa.com/document/87030026264555520) 获取 SDK 要播放的音频帧并自行播放。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enable</td>

<td rowspan="1" colSpan="1" >是否启用音频自定义播放，默认为关闭状态。</td>
</tr>
</table>


> **注意**
> 

> 需要您在进入房间前设置才能生效，暂不支持进入房间后再设置。
> 


## getCustomAudioRenderingFrame



#### 获取可播放的音频数据。

调用该接口之前，您需要先通过 [enableCustomAudioRendering](https://write.woa.com/document/87030026264555520) 开启音频自定义播放。



参数 [TRTCAudioFrame](https://write.woa.com/document/87030132707430400) 推荐下列填写方式（其他字段不需要填写）：
-  sampleRate：采样率，必填，支持 16000、24000、32000、44100、48000。

-  channel：声道数，必填，单声道请填1，双声道请填2，双声道时数据是交叉的。

-  data：用于获取音频数据的 buffer。需要您根据一帧音频帧的帧长度分配好 data 的内存大小。获取的 PCM 数据支持 10ms 或 20ms 两种帧长，推荐使用 20ms 的帧长。




计算公式为：` 采样率 x 播放时长 x 声道数量 x 2（每个样点的字节数） `， 例如： 48000Hz 采样率、单声道、且播放时长为 20ms 的一帧音频帧的 buffer 大小为 ` 48000 × 0.02s × 1 × 16bit = 15360bit = 1920字节 `。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >audioFrame</td>

<td rowspan="1" colSpan="1" >音频数据帧。</td>
</tr>
</table>


> **注意**
> 

> 1. 参数 audioFrame 中的 sampleRate、channel 需提前设置好，同时分配好所需读取帧长的 data 空间。
> 

> 2. SDK 内部会根据 sampleRate 和 channel 自动填充 data 数据。
> 

> 3. 建议由系统的音频播放线程直接驱动该函数的调用，在播放完一帧音频之后，即调用该接口获取下一帧可播放的音频数据。
> 


## sendCustomCmdMsg



#### 使用 UDP 通道发送自定义消息给房间内所有用户。

该接口可以让您借助 TRTC 的 UDP 通道，向当前房间里的其他用户广播自定义数据，以达到传输信令的目的。

房间中的其他用户可以通过 [ITRTCCloudCallback](https://write.woa.com/document/87030021158866944) 中的 onRecvCustomCmdMsg 回调接收消息。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >cmdID</td>

<td rowspan="1" colSpan="1" >消息 ID，取值范围为 [1, 10]。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >data</td>

<td rowspan="1" colSpan="1" >待发送的消息，单个消息的最大长度被限制为 1KB。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ordered</td>

<td rowspan="1" colSpan="1" >是否要求有序，即是否要求接收端的数据包顺序和发送端的数据包顺序一致（这会带来一定的接收延时）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >reliable</td>

<td rowspan="1" colSpan="1" >是否可靠发送，可靠发送可以获得更高的发送成功率，但可靠发送比不可靠发送会带来更大的接收延迟。</td>
</tr>
</table>


> **注意**
> 

> 1. 发送消息到房间内所有用户（暂时不支持 Web/小程序端），每秒最多能发送30条消息（与 [sendSEIMsg](https://write.woa.com/document/87030026264555520) 共享限制）。
> 

> 2. 每个包最大为 1KB，超过则很有可能会被中间路由器或者服务器丢弃。
> 

> 3. 每个客户端每秒最多能发送总计 16KB 数据（与 [sendSEIMsg](https://write.woa.com/document/87030026264555520) 共享限制）。
> 

> 4. 请将 ` reliable ` 和 ` ordered ` 同时设置为 true 或同时设置为 false，暂不支持交叉设置。
> 

> 5. 强烈建议您将不同类型的消息设定为不同的 cmdID，这样可以在要求有序的情况下减小消息时延。
> 

> 6. 目前仅支持主播身份。
> 


#### 返回值说明：

true：消息已经发出；false：消息发送失败。

## sendSEIMsg



#### 使用 SEI 通道发送自定义消息给房间内所有用户。

该接口可以让您借助 TRTC 的 SEI 通道，向当前房间里的其他用户广播自定义数据，已达到传输信令的目的。



视频帧的头部有一个叫做 SEI 的头部数据块，该接口的原理就是利用这个被称为 SEI 的头部数据块，将您要发送的自定义信令嵌入其中，使其同视频帧一并发送出去。

因此，与 [sendCustomCmdMsg](https://write.woa.com/document/87030026264555520) 相比，SEI 通道传输的信令具有更好的兼容性：信令可以伴随着视频帧一直传输到直播 CDN 上。

不过，由于视频帧头部的数据块不能太大，建议您使用该接口时，尽量将信令控制在几个字节的大小。



最常见的用法是把自定义的时间戳（timestamp）用本接口嵌入视频帧中，实现消息和画面的完美对齐（例如：教育场景下的课件和视频信号的对齐）。

房间中的其他用户可以通过 [ITRTCCloudCallback](https://write.woa.com/document/87030021158866944) 中的 [onRecvSEIMsg](https://write.woa.com/document/87030021158866944) 回调接收消息。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >data</td>

<td rowspan="1" colSpan="1" >待发送的数据，最大支持 1KB（1000字节）的数据大小</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >repeatCount</td>

<td rowspan="1" colSpan="1" >发送数据次数</td>
</tr>
</table>


> **注意**
> 

> 本接口有以下限制：
> 

> 1. 数据在接口调用完后不会被即时发送出去，而是从下一帧视频帧开始与视频帧一起发送。
> 

> 2. 发送消息到房间内所有用户，每秒最多能发送 40 条消息（与 [sendCustomCmdMsg](https://write.woa.com/document/87030026264555520) 共享限制）。
> 

> 3. 每个包最大为 1KB，若发送大量数据，会导致视频码率增大，可能导致视频画质下降甚至卡顿（与 [sendCustomCmdMsg](https://write.woa.com/document/87030026264555520) 共享限制）。
> 

> 4. 每个客户端每秒最多能发送总计 16KB 数据（与 [sendCustomCmdMsg](https://write.woa.com/document/87030026264555520) 共享限制）。
> 

> 5. 若指定多次发送（repeatCount > 1），则数据会被带在后续的连续 repeatCount 个视频帧中发送出去，同样会导致视频码率增大。接收消息 [onRecvSEIMsg](https://write.woa.com/document/87030021158866944) 回调也可能会收到多次相同的消息，需要去重。
> 


#### 返回值说明：

true：消息已通过限制，等待后续视频帧发送；false：消息被限制发送

## startSpeedTest



#### 开始进行网速测试（进入房间前使用）。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >params</td>

<td rowspan="1" colSpan="1" >测速选项</td>
</tr>
</table>


> **注意**
> 

> 1. 测速过程将产生少量的基础服务费用，详见 [计费概述 > 基础服务](https://cloud.tencent.com/document/product/647/17157#.E5.9F.BA.E7.A1.80.E6.9C.8D.E5.8A.A1) 文档说明。
> 

> 2. 请在进入房间前进行网速测试，在房间中网速测试会影响正常的音视频传输效果，而且由于干扰过多，网速测试结果也不准确。
> 

> 3. 同一时间只允许一项网速测试任务运行。
> 


#### 返回值说明：

接口调用结果，< 0：失败

## stopSpeedTest



#### 停止网络测速。

## getSDKVersion



#### 获取 SDK 版本信息。

## setLogLevel



#### 设置 Log 输出级别。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >level</td>

<td rowspan="1" colSpan="1" >参见 [TRTCLogLevel](https://write.woa.com/document/87030132707430400)，默认值：[TRTCLogLevelNone](https://write.woa.com/document/87030132707430400)</td>
</tr>
</table>


## setConsoleEnabled



#### 启用/禁用控制台日志打印。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enabled</td>

<td rowspan="1" colSpan="1" >指定是否启用，默认：禁止状态。</td>
</tr>
</table>


## setLogCompressEnabled



#### 启用/禁用日志的本地压缩。

开启压缩后，Log 存储体积明显减小，但需要腾讯云提供的 Python 脚本解压后才能阅读。

禁用压缩后，Log 采用明文存储，可以直接用记事本打开阅读，但占用空间较大。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enabled</td>

<td rowspan="1" colSpan="1" >指定是否启用，默认为启动状态</td>
</tr>
</table>


## setLogDirPath



#### 设置本地日志的保存路径。

通过该接口您可以更改 SDK 本地日志的默认存储路径，SDK 默认的本地日志的存储位置：
-  Windows 平台：在 C:/Users/[系统用户名]/AppData/Roaming/liteav/log，即 %appdata%/liteav/log 下。

-  iOS 或 Mac 平台：在 sandbox Documents/log 下。

-  Android 平台：在 /app私有目录/files/log/liteav/ 下。

<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >path</td>

<td rowspan="1" colSpan="1" >存储日志的路径</td>
</tr>
</table>


> **注意**
> 

> 请务必在所有其他接口之前调用，并且保证您指定的目录是存在的，并且您的应用程序拥有对该目录的读写权限。
> 


## setLogCallback



#### 设置日志回调。

## showDebugView



#### 显示仪表盘。

“仪表盘”是位于视频渲染控件之上的一个半透明的调试信息浮层，用于展示音视频信息和事件信息，便于对接和调试。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >showType</td>

<td rowspan="1" colSpan="1" >0：不显示；1：显示精简版（仅显示音视频信息）；2：显示完整版（包含音视频信息和事件信息）。</td>
</tr>
</table>


## callExperimentalAPI



#### 调用实验性接口。

## enablePayloadPrivateEncryption



#### 开启或关闭媒体流私有加密。

在安全要求较高的场景下，TRTC 建议您在加入房间前，调用 ` enablePayloadPrivateEncryption ` 方法开启媒体流私有加密。

用户退出房间后，SDK 会自动关闭私有加密。如需重新开启私有加密，您需要在用户再次加入房间前调用该方法。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >config</td>

<td rowspan="1" colSpan="1" >配置媒体流私有加密的算法和密钥，参见 [TRTCPayloadPrivateEncryptionConfig](https://write.woa.com/document/87030132707430400)。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enabled</td>

<td rowspan="1" colSpan="1" >是否开启媒体流私有加密。</td>
</tr>
</table>


> **注意**
> 

> TRTC 已经内置对媒体流进行加密后再传输，启用媒体流私有加密后将使用您传入的密匙与初始向量进行再次加密。
> 


#### 返回值说明：

接口调用结果，0: 方法调用成功， -1: 传入参数无效， -2: 功能已过期。若需解锁：请前往购买 [TRTC 旗舰版（国内站）/ 专业版（国际站）套餐](https://buy.cloud.tencent.com/trtc?tab=uikit&type=call&pkg=top)，并[联系我们](https://console.cloud.tencent.com/workorder/category?from=connect-us)审核后使用。