> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

# 腾讯云实时音视频(TRTC SDK )文档

## 概述
`TRTCCloudListener.java` 是腾讯云实时音视频(TRTC SDK ) Android 平台的事件回调接口文档。


## TRTCVideoRenderListener
<table>
<tr>
<td rowspan="1" colSpan="1" >函数列表</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onRenderVideoFrame](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >自定义视频渲染回调。</td>
</tr>
</table>


## TRTCVideoFrameListener
<table>
<tr>
<td rowspan="1" colSpan="1" >函数列表</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onGLContextCreated](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >SDK 内部 OpenGL 环境已经创建的通知。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onProcessVideoFrame](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >用于对接第三方美颜组件的视频处理回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onGLContextDestory](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >SDK 内部 OpenGL 环境被销毁的通知。</td>
</tr>
</table>


## TRTCAudioFrameListener
<table>
<tr>
<td rowspan="1" colSpan="1" >函数列表</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onCapturedAudioFrame](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >本地采集并经过音频模块前处理后的音频数据回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onLocalProcessedAudioFrame](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >本地采集并经过音频模块前处理、音效处理和混 BGM 后的音频数据回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onRemoteUserAudioFrame](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >混音前的每一路远程用户的音频数据。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onMixedPlayAudioFrame](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >将各路待播放音频混合之后并在最终提交系统播放之前的数据回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onMixedAllAudioFrame](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >SDK 所有音频混合后的音频数据（包括采集到的和待播放的）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onVoiceEarMonitorAudioFrame](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >耳返的音频数据。</td>
</tr>
</table>


## TRTCLogListener
<table>
<tr>
<td rowspan="1" colSpan="1" >函数列表</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onLog](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >本地 LOG 的打印回调。</td>
</tr>
</table>


## TRTCCloudListener
<table>
<tr>
<td rowspan="1" colSpan="1" >函数列表</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onError](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >错误事件回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onWarning](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >警告事件回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onEnterRoom](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >进入房间成功与否的事件回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onExitRoom](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >离开房间的事件回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onSwitchRole](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >切换角色的事件回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onSwitchRoom](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >切换房间的结果回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onConnectOtherRoom](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >请求跨房通话的结果回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onDisConnectOtherRoom](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >结束跨房通话的结果回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onUpdateOtherRoomForwardMode](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >更改跨房主播上行能力的结果回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onRemoteUserEnterRoom](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >有用户加入当前房间。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onRemoteUserLeaveRoom](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >有用户离开当前房间。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onUserVideoAvailable](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >某远端用户发布/取消了主路视频画面。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onUserSubStreamAvailable](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >某远端用户发布/取消了辅路视频画面。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onUserAudioAvailable](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >某远端用户发布/取消了自己的音频。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onFirstVideoFrame](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >SDK 开始渲染自己本地或远端用户的首帧画面。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onFirstAudioFrame](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >SDK 开始播放远端用户的首帧音频。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onSendFirstLocalVideoFrame](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >自己本地的首个视频帧已被发布出去。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onSendFirstLocalAudioFrame](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >自己本地的首个音频帧已被发布出去。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onRemoteVideoStatusUpdated](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >远端视频状态变化的事件回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onRemoteAudioStatusUpdated](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >远端音频状态变化的事件回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onUserVideoSizeChanged](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >用户视频大小发生改变回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onNetworkQuality](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >网络质量的实时统计回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onStatistics](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >音视频技术指标的实时统计回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onSpeedTestResult](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >网速测试的结果回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onConnectionLost](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >SDK 与云端的连接已经断开。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onTryToReconnect](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >SDK 正在尝试重新连接到云端。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onConnectionRecovery](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >SDK 与云端的连接已经恢复。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onCameraDidReady](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >摄像头准备就绪。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onMicDidReady](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >麦克风准备就绪。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onAudioRouteChanged](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >当前音频路由发生变化（仅适用于移动设备）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onUserVoiceVolume](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >音量大小的反馈回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onRecvCustomCmdMsg](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >收到自定义消息的事件回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onMissCustomCmdMsg](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >自定义消息丢失的事件回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onRecvSEIMsg](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >收到 SEI 消息的回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onStartPublishing](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >开始向腾讯云直播 CDN 上发布音视频流的事件回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onStopPublishing](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >停止向腾讯云直播 CDN 上发布音视频流的事件回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onStartPublishCDNStream](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >开始向非腾讯云 CDN 上发布音视频流的事件回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onStopPublishCDNStream](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >停止向非腾讯云 CDN 上发布音视频流的事件回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onSetMixTranscodingConfig](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >设置云端混流的排版布局和转码参数的事件回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onStartPublishMediaStream](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >开始发布媒体流的事件回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onUpdatePublishMediaStream](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >更新媒体流的事件回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onStopPublishMediaStream](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >停止媒体流的事件回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onCdnStreamStateChanged](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >RTMP/RTMPS 推流状态发生改变回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onScreenCaptureStarted](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >屏幕分享开启的事件回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onScreenCapturePaused](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >屏幕分享暂停的事件回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onScreenCaptureResumed](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >屏幕分享恢复的事件回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onScreenCaptureStopped](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >屏幕分享停止的事件回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onLocalRecordBegin](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >本地录制任务已经开始的事件回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onLocalRecording](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >本地录制任务正在进行中的进展事件回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onLocalRecordFragment](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >本地录制分片的事件回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onLocalRecordComplete](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >本地录制任务已经结束的事件回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onSnapshotComplete](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >本地截图完成的事件回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onUserEnter](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >有主播加入当前房间（已废弃）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onUserExit](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >有主播离开当前房间（已废弃）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onAudioEffectFinished](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >音效播放已结束（已废弃）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onSpeedTest](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >服务器测速的结果回调（已废弃）。</td>
</tr>
</table>


## onRenderVideoFrame



#### 自定义视频渲染回调。

当您设置了本地或者远端的视频自定义渲染回调之后，SDK 就会将原本要交给渲染控件进行渲染的视频帧通过此回调接口抛送给您，以便于您进行自定义渲染。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >frame</td>

<td rowspan="1" colSpan="1" >待渲染的视频帧信息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >streamType</td>

<td rowspan="1" colSpan="1" >频流类型：主路（Main）一般用于承载摄像头画面，辅路（Sub）一般用于承载屏幕分享画面。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >视频源的 userId，如果是本地视频回调（setLocalVideoRenderDelegate），该参数可以忽略。</td>
</tr>
</table>


## onGLContextCreated



#### SDK 内部 OpenGL 环境已经创建的通知。

## onProcessVideoFrame



#### 用于对接第三方美颜组件的视频处理回调。

如果您选购了第三方美颜组件，就需要在 TRTCCloud 中设置第三方美颜回调，之后 TRTC 就会将原本要进行预处理的视频帧通过此回调接口抛送给您。

之后您就可以将 TRTC 抛出的视频帧交给第三方美颜组件进行图像处理，由于抛出的数据是可读且可写的，因此第三方美颜的处理结果也可以同步给 TRTC 进行后续的编码和发送。



情况一：美颜组件自身会产生新的纹理。

如果您使用的美颜组件会在处理图像的过程中产生一帧全新的纹理（用于承载处理后的图像），那请您在回调函数中将 dstFrame.textureId 设置为新纹理的 ID：
``` java
private final TRTCVideoFrameListener mVideoFrameListener = new TRTCVideoFrameListener() {
    @Override
    public void onGLContextCreated() {
        mFURenderer.onSurfaceCreated();
        mFURenderer.setUseTexAsync(true);
    }
    @Override
    public int onProcessVideoFrame(TRTCVideoFrame srcFrame, TRTCVideoFrame dstFrame) {
        dstFrame.texture.textureId = mFURenderer.onDrawFrameSingleInput(srcFrame.texture.textureId, srcFrame.width, srcFrame.height);
        return 0;
    }
    @Override
    public void onGLContextDestory() {
        mFURenderer.onSurfaceDestroyed();
    }
};
```



情况二：美颜组件需要您提供目标纹理。

如果您使用的第三方美颜模块并不生成新的纹理，而是需要您设置给该模块一个输入纹理和一个输出纹理，则可以考虑如下方案：
``` java
int onProcessVideoFrame(TRTCCloudDef.TRTCVideoFrame srcFrame, TRTCCloudDef.TRTCVideoFrame dstFrame) {
    thirdparty_process(srcFrame.texture.textureId, srcFrame.width, srcFrame.height, dstFrame.texture.textureId);
    return 0;
}
```
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >dstFrame</td>

<td rowspan="1" colSpan="1" >用于接收第三方美颜处理过的视频画面。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >srcFrame</td>

<td rowspan="1" colSpan="1" >用于承载 TRTC 采集到的摄像头画面。</td>
</tr>
</table>


> **注意**
> 

> 目前仅支持 OpenGL 纹理方案（ PC 仅支持 TRTCVideoBufferType_Buffer 格式）。
> 


## onGLContextDestory



#### SDK 内部 OpenGL 环境被销毁的通知。

## onCapturedAudioFrame



#### 本地采集并经过音频模块前处理后的音频数据回调。

当您设置完音频数据自定义回调之后，SDK 内部会把刚采集到并经过前处理(ANS、AEC、AGC）之后的数据，以 PCM 格式的形式通过本接口回调给您。
-  此接口回调出的音频时间帧长固定为0.02s，格式为 PCM 格式。

-  由时间帧长转化为字节帧长的公式为 ` 采样率 × 时间帧长 × 声道数 × 采样点位宽 `。

-  以 TRTC 默认的音频录制格式48000采样率、单声道、16采样点位宽为例，字节帧长为 ` 48000 × 0.02s × 1 × 16bit = 15360bit = 1920字节 `。

<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >frame</td>

<td rowspan="1" colSpan="1" >PCM 格式的音频数据帧。</td>
</tr>
</table>


> **注意**
> 

> 1. 请不要在此回调函数中做任何耗时操作，由于 SDK 每隔 20ms 就要处理一帧音频数据，如果您的处理时间超过 20ms，就会导致声音异常。
> 

> 2. 此接口回调出的音频数据是可读写的，也就是说您可以在回调函数中同步修改音频数据，但请保证处理耗时。
> 

> 3. 此接口回调出的音频数据已经经过了前处理(ANS、AEC、AGC），但**不包含**背景音、音效、混响等前处理效果，延迟较低。
> 


## onLocalProcessedAudioFrame



#### 本地采集并经过音频模块前处理、音效处理和混 BGM 后的音频数据回调。

当您设置完音频数据自定义回调之后，SDK 内部会把刚采集到并经过前处理、音效处理和混 BGM 之后的数据，在最终进行网络编码之前，以 PCM 格式的形式通过本接口回调给您。
-  此接口回调出的音频时间帧长固定为0.02s，格式为 PCM 格式。

-  由时间帧长转化为字节帧长的公式为` 采样率 × 时间帧长 × 声道数 × 采样点位宽 `。

-  以 TRTC 默认的音频录制格式48000采样率、单声道、16采样点位宽为例，字节帧长为` 48000 × 0.02s × 1 × 16bit = 15360bit = 1920字节 `。




特殊说明：

您可以通过设置接口中的 ` TRTCAudioFrame.extraData ` 字段，达到传输信令的目的。由于音频帧头部的数据块不能太大，建议您写入 ` extraData ` 时，尽量将信令控制在几个字节的大小，如果超过 100 个字节，写入的数据不会被发送。



房间内其他用户可以通过 [TRTCAudioFrameListener](https://write.woa.com/document/87029920275542016) 中的 ` onRemoteUserAudioFrame ` 中的 ` TRTCAudioFrame.extraData ` 字段回调接收数据。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >frame</td>

<td rowspan="1" colSpan="1" >PCM 格式的音频数据帧。</td>
</tr>
</table>


> **注意**
> 

> 1. 请不要在此回调函数中做任何耗时操作，由于 SDK 每隔 20ms 就要处理一帧音频数据，如果您的处理时间超过 20ms，就会导致声音异常。
> 

> 2. 此接口回调出的音频数据是可读写的，也就是说您可以在回调函数中同步修改音频数据，但请保证处理耗时。
> 

> 3. 此接口回调出的数据已经经过了前处理(ANS、AEC、AGC）、音效和混 BGM 处理，声音的延迟相比于 [onCapturedAudioFrame](https://write.woa.com/document/87029920275542016) 要高一些。
> 


## onRemoteUserAudioFrame



#### 混音前的每一路远程用户的音频数据。

当您设置完音频数据自定义回调之后，SDK 内部会把远端的每一路原始数据，在最终混音之前，以 PCM 格式的形式通过本接口回调给您。
-  此接口回调出的音频时间帧长固定为0.02s，格式为 PCM 格式。

-  由时间帧长转化为字节帧长的公式为` 采样率 × 时间帧长 × 声道数 × 采样点位宽 `。

-  以 TRTC 默认的音频录制格式48000采样率、单声道、16采样点位宽为例，字节帧长为` 48000 × 0.02s × 1 × 16bit = 15360bit = 1920字节 `。

<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >frame</td>

<td rowspan="1" colSpan="1" >PCM 格式的音频数据帧。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >用户标识。</td>
</tr>
</table>


> **注意**
> 

> 此接口回调出的音频数据是只读的，不支持修改。
> 


## onMixedPlayAudioFrame



#### 将各路待播放音频混合之后并在最终提交系统播放之前的数据回调。

当您设置完音频数据自定义回调之后，SDK 内部会把各路待播放的音频混合之后的音频数据，在提交系统播放之前，以 PCM 格式的形式通过本接口回调给您。
-  此接口回调出的音频时间帧长固定为0.02s，格式为 PCM 格式。

-  由时间帧长转化为字节帧长的公式为 ` 采样率 × 时间帧长 × 声道数 × 采样点位宽 `。

-  以 TRTC 默认的音频录制格式48000采样率、单声道、16采样点位宽为例，字节帧长为 ` 48000 × 0.02s × 1 × 16bit = 15360bit = 1920字节 `。

<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >frame</td>

<td rowspan="1" colSpan="1" >PCM 格式的音频数据帧。</td>
</tr>
</table>


> **注意**
> 

> 1. 请不要在此回调函数中做任何耗时操作，由于 SDK 每隔 20ms 就要处理一帧音频数据，如果您的处理时间超过 20ms，就会导致声音异常。
> 

> 2. 此接口回调出的音频数据是可读写的，也就是说您可以在回调函数中同步修改音频数据，但请保证处理耗时。
> 

> 3. 此接口回调出的是对各路待播放音频数据的混合，但其中并不包含耳返的音频数据。
> 


## onMixedAllAudioFrame



#### SDK 所有音频混合后的音频数据（包括采集到的和待播放的）。

当您设置完音频数据自定义回调之后，SDK 内部会把所有采集到的和待播放的音频数据混合起来，以 PCM 格式的形式通过本接口回调给您，便于您进行自定义录制。
-  此接口回调出的音频时间帧长固定为0.02s，格式为 PCM 格式。

-  由时间帧长转化为字节帧长的公式为 ` 采样率 × 时间帧长 × 声道数 × 采样点位宽 `。

-  以 TRTC 默认的音频录制格式48000采样率、单声道、16采样点位宽为例，字节帧长为 ` 48000 × 0.02s × 1 × 16bit = 15360bit = 1920字节 `。

<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >frame</td>

<td rowspan="1" colSpan="1" >PCM 格式的音频数据帧。</td>
</tr>
</table>


> **注意**
> 

> 1. 此接口回调出的是SDK所有音频数据的混合数据，包括：经过 3A 前处理、特效叠加以及背景音乐混音后的本地音频，所有远端音频，但不包括耳返音频。
> 

> 2. 此接口回调出的音频数据不支持修改。
> 


## onVoiceEarMonitorAudioFrame



#### 耳返的音频数据。

当您设置完音频数据自定义回调之后，SDK 内部会把耳返的音频数据在播放之前以 PCM 格式的形式通过本接口回调给您。
-  此接口回调出的音频时间帧长不固定，格式为 PCM 格式。

-  由时间帧长转化为字节帧长的公式为 ` 采样率 × 时间帧长 × 声道数 × 采样点位宽 `。

-  以 TRTC 默认的音频录制格式 48000 采样率、单声道、16采样点位宽为例，0.02s 的音频数据字节帧长为 ` 48000 × 0.02s × 1 × 16bit = 15360bit = 1920字节 `。

<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >frame</td>

<td rowspan="1" colSpan="1" >PCM 格式的音频数据帧。</td>
</tr>
</table>


> **注意**
> 

> 1. 请不要在此回调函数中做任何耗时操作，否则会导致声音异常。
> 

> 2. 此接口回调出的音频数据是可读写的，也就是说您可以在回调函数中同步修改音频数据，但请保证处理耗时。
> 


## onLog



#### 本地 LOG 的打印回调。

如果您希望捕获 SDK 的本地日志打印行为，可以通过设置日志回调，让 SDK 将要打印的日志都通过本回调接口抛送给您。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >level</td>

<td rowspan="1" colSpan="1" >日志等级请参见 [TRTC_LOG_LEVEL](https://write.woa.com/document/87029993616093184)。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >log</td>

<td rowspan="1" colSpan="1" >日志内容。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >module</td>

<td rowspan="1" colSpan="1" >保留字段，暂无具体意义，目前为固定值 ` TXLiteAVSDK `。</td>
</tr>
</table>


## onError



#### 错误事件回调。

错误事件，表示 SDK 抛出的不可恢复的错误，例如进入房间失败或设备开启失败等。

参考文档：[错误码表](https://cloud.tencent.com/document/product/647/38308)
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >errCode</td>

<td rowspan="1" colSpan="1" >错误码</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >errMsg</td>

<td rowspan="1" colSpan="1" >错误信息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >extInfo</td>

<td rowspan="1" colSpan="1" >扩展信息字段，个别错误码可能会带额外的信息帮助定位问题</td>
</tr>
</table>


## onWarning



#### 警告事件回调。

警告事件，表示 SDK 抛出的提示性问题，例如视频出现卡顿或 CPU 使用率太高等。

参考文档：[错误码表](https://cloud.tencent.com/document/product/647/38308)
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >extInfo</td>

<td rowspan="1" colSpan="1" >扩展信息字段，个别警告码可能会带额外的信息帮助定位问题</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >warningCode</td>

<td rowspan="1" colSpan="1" >警告码</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >warningMsg</td>

<td rowspan="1" colSpan="1" >警告信息</td>
</tr>
</table>


## onEnterRoom



#### 进入房间成功与否的事件回调。

调用 TRTCCloud 中的 [enterRoom](https://write.woa.com/document/87029900866228224) 接口执行进房操作后，会收到来自 [TRTCCloudListener](https://write.woa.com/document/87029920275542016) 的 ` onEnterRoom(result) ` 回调：
-  如果加入成功，回调 result 会是一个正数（result > 0），代表进入房间所消耗的时间，单位是毫秒（ms）。

-  如果加入失败，回调 result 会是一个负数（result < 0），代表失败原因的错误码。


进房失败的错误码含义请参见[错误码表](https://cloud.tencent.com/document/product/647/38308)。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >result</td>

<td rowspan="1" colSpan="1" >result > 0 时为进房耗时（ms），result < 0 时为进房错误码。</td>
</tr>
</table>


> **注意**
> 

> 1. 在 Ver6.6 之前的版本，只有进房成功会抛出 ` onEnterRoom(result) ` 回调，进房失败由 [onError](https://write.woa.com/document/87029920275542016) 回调抛出。
> 

> 2. 在 Ver6.6 之后的版本：无论进房成功或失败，均会抛出 ` onEnterRoom(result) ` 回调，同时进房失败也会有 [onError](https://write.woa.com/document/87029920275542016) 回调抛出。
> 


## onExitRoom



#### 离开房间的事件回调。

调用 TRTCCloud 中的 [exitRoom](https://write.woa.com/document/87029900866228224) 接口会执行退出房间的相关逻辑，例如释放音视频设备资源和编解码器资源等。

待 SDK 占用的所有资源释放完毕后，SDK 会抛出 ` onExitRoom() ` 回调通知到您。



如果您要再次调用 [enterRoom](https://write.woa.com/document/87029900866228224) 或者切换到其他的音视频 SDK，请等待 ` onExitRoom ` 回调到来后再执行相关操作。否则可能会遇到例如摄像头、麦克风设备被强占等各种异常问题。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >reason</td>

<td rowspan="1" colSpan="1" >离开房间原因，0：主动调用 exitRoom 退出房间；1：被服务器移出当前房间；2：当前房间整个被解散 3: 服务器状态异常。</td>
</tr>
</table>


## onSwitchRole



#### 切换角色的事件回调。

调用 TRTCCloud 中的 [switchRole](https://write.woa.com/document/87029900866228224) 接口会切换主播和观众的角色，该操作会伴随一个线路切换的过程，待 SDK 切换完成后，会抛出 ` onSwitchRole() ` 事件回调。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >errCode</td>

<td rowspan="1" colSpan="1" >错误码，ERR_NULL 代表切换成功，其他请参见[错误码](https://cloud.tencent.com/document/product/647/32257)。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >errMsg</td>

<td rowspan="1" colSpan="1" >错误信息。</td>
</tr>
</table>


## onSwitchRoom



#### 切换房间的结果回调。

调用 TRTCCloud 中的 [switchRoom](https://write.woa.com/document/87029900866228224) 接口可以让用户快速地从一个房间切换到另一个房间，待 SDK 切换完成后，会抛出 ` onSwitchRoom() ` 事件回调。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >errCode</td>

<td rowspan="1" colSpan="1" >错误码，ERR_NULL 代表切换成功，其他请参见[错误码](https://cloud.tencent.com/document/product/647/32257)。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >errMsg</td>

<td rowspan="1" colSpan="1" >错误信息。</td>
</tr>
</table>


## onConnectOtherRoom



#### 请求跨房通话的结果回调。

调用 TRTCCloud 中的 [connectOtherRoom](https://write.woa.com/document/87029900866228224) 接口会将两个不同房间中的主播拉通视频通话，也就是所谓的“主播PK”功能。

调用者会收到 ` onConnectOtherRoom() ` 回调来获知跨房通话是否成功。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >errCode</td>

<td rowspan="1" colSpan="1" >错误码，ERR_NULL 代表切换成功，其他请参见[错误码](https://cloud.tencent.com/document/product/647/32257)。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >errMsg</td>

<td rowspan="1" colSpan="1" >错误信息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >要跨房通话的另一个房间中的主播的用户 ID。</td>
</tr>
</table>


## onDisConnectOtherRoom



#### 结束跨房通话的结果回调。

调用 TRTCCloud 中的 disConnectOtherRoom 接口会结束两个不同房间中的主播视频通话，也就是所谓的“主播PK”功能。

调用者会收到 ` onDisconnectOtherRoom() ` 回调来获知结束跨房通话是否成功。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >errCode</td>

<td rowspan="1" colSpan="1" >错误码，ERR_NULL 代表成功，其他请参见[错误码](https://cloud.tencent.com/document/product/647/32257)。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >errMsg</td>

<td rowspan="1" colSpan="1" >错误信息。</td>
</tr>
</table>


## onUpdateOtherRoomForwardMode



#### 更改跨房主播上行能力的结果回调。

调用 TRTCCloud 中的 [updateOtherRoomForwardMode](https://write.woa.com/document/87029900866228224) 接口会限制跨房主播在本房间内的上行能力，禁止或允许跨房主播发布音频/主路视频/辅路视频，该行为会影响房间内的所有用户。

调用者会收到 ` onUpdateOtherRoomForwardMode() ` 回调来获知更改跨房主播上行能力是否成功。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >errCode</td>

<td rowspan="1" colSpan="1" >错误码，ERR_NULL 代表成功，其他请参见[错误码](https://cloud.tencent.com/document/product/647/32257)。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >errMsg</td>

<td rowspan="1" colSpan="1" >错误信息。</td>
</tr>
</table>


## onRemoteUserEnterRoom



#### 有用户加入当前房间。

出于性能方面的考虑，在 TRTC 两种不同的应用场景（即 ` AppScene `，在 [enterRoom](https://write.woa.com/document/87029900866228224) 时通过第二个参数指定）下，该通知的行为会有差别：
-  直播类场景（[TRTC_APP_SCENE_LIVE](https://write.woa.com/document/87029993616093184) 和 [TRTC_APP_SCENE_VOICE_CHATROOM](https://write.woa.com/document/87029993616093184)）：该场景下的用户区分主播和观众两种角色，只有主播进入房间时才会触发该通知，观众进入房间时不会触发该通知。

-  通话类场景（[TRTC_APP_SCENE_VIDEOCALL](https://write.woa.com/document/87029993616093184) 和 [TRTC_APP_SCENE_AUDIOCALL](https://write.woa.com/document/87029993616093184)）：该场景下的用户没有角色的区分（可认为都是主播），任何用户进入房间都会触发该通知。

<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >远端用户的用户标识。</td>
</tr>
</table>


> **注意**
> 

> 1. 事件回调 ` onRemoteUserEnterRoom ` 和 [onRemoteUserLeaveRoom](https://write.woa.com/document/87029920275542016) 只适用于维护当前房间里的“用户列表”，有此事件回调不代表一定有视频画面。
> 

> 2. 如果需要显示远程画面，请监听代表某个用户是否有视频画面的 [onUserVideoAvailable](https://write.woa.com/document/87029920275542016) 事件回调。
> 


## onRemoteUserLeaveRoom



#### 有用户离开当前房间。

与 [onRemoteUserEnterRoom](https://write.woa.com/document/87029920275542016) 相对应，在两种不同的应用场景（即 AppScene，在 [enterRoom](https://write.woa.com/document/87029900866228224) 时通过第二个参数指定）下，该通知的行为会有差别：
-  直播类场景（[TRTC_APP_SCENE_LIVE](https://write.woa.com/document/87029993616093184) 和 [TRTC_APP_SCENE_VOICE_CHATROOM](https://write.woa.com/document/87029993616093184)）：该场景下的用户区分主播和观众两种角色，只有主播离开房间时才会触发该通知，观众离开房间时不会触发该通知。

-  通话类场景（[TRTC_APP_SCENE_VIDEOCALL](https://write.woa.com/document/87029993616093184) 和 [TRTC_APP_SCENE_AUDIOCALL](https://write.woa.com/document/87029993616093184)）：该场景下的用户没有角色的区分（可认为都是主播），任何用户离开房间都会触发该通知。

<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >reason</td>

<td rowspan="1" colSpan="1" >离开原因，0表示用户主动退出房间，1表示用户超时退出，2表示被移出房间，3表示主播因切换到观众退出房间。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >远端用户的用户标识。</td>
</tr>
</table>


## onUserVideoAvailable



#### 某远端用户发布/取消了主路视频画面。

**主路画面** 一般被用于承载摄像头画面。当您收到 ` onUserVideoAvailable(userId, true) ` 通知时，表示该路画面已经有可播放的视频帧到达。

此时，您需要调用 [startRemoteView](https://write.woa.com/document/87029900866228224) 接口订阅该用户的远程画面，订阅成功后，您会继续收到该用户的首帧画面渲染回调 ` onFirstVideoFrame(userId) `。



当您收到 ` onUserVideoAvailable(userId, false) ` 通知时，表示该路远程画面已经被关闭，关闭的原因可能是该用户调用了 [muteLocalVideo](https://write.woa.com/document/87029900866228224) 或 [stopLocalPreview](https://write.woa.com/document/87029900866228224)。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >available</td>

<td rowspan="1" colSpan="1" >该用户是否发布（或取消发布）了主路视频画面，true：发布；false：取消发布。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >远端用户的用户标识。</td>
</tr>
</table>


## onUserSubStreamAvailable



#### 某远端用户发布/取消了辅路视频画面。

“辅路画面”一般被用于承载屏幕分享的画面。当您收到 ` onUserSubStreamAvailable(userId, true) ` 通知时，表示该路画面已经有可播放的视频帧到达。

此时，您需要调用 [startRemoteView](https://write.woa.com/document/87029900866228224) 接口订阅该用户的远程画面，订阅成功后，您会继续收到该用户的首帧画面渲染回调 ` onFirstVideoFrame(userId) `。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >available</td>

<td rowspan="1" colSpan="1" >该用户是否发布（或取消发布）了辅路视频画面，true: 发布；false：取消发布。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >远端用户的用户标识。</td>
</tr>
</table>


> **注意**
> 

> 显示辅路画面使用的函数是 [startRemoteView](https://write.woa.com/document/87029900866228224) 而非 startRemoteSubStreamView，startRemoteSubStreamView 已经被废弃。
> 


## onUserAudioAvailable



#### 某远端用户发布/取消了自己的音频。

当您收到 ` onUserAudioAvailable(userId, true) ` 通知时，表示该用户发布了自己的声音，此时 SDK 的表现为：
-  在自动订阅模式下，您无需做任何操作，SDK 会自动播放该用户的声音。

-  在手动订阅模式下，您可以通过 [muteRemoteAudio](https://write.woa.com/document/87029900866228224)(userid, false) 来播放该用户的声音。

<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >available</td>

<td rowspan="1" colSpan="1" >该用户是否发布（或取消发布）了自己的音频，true: 发布；false：取消发布。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >远端用户的用户标识。</td>
</tr>
</table>


> **注意**
> 

> SDK 默认使用自动订阅模式，您可以通过 [setDefaultStreamRecvMode](https://write.woa.com/document/87029900866228224) 设置为手动订阅，但需要在您进入房间之前调用才生效。
> 


## onFirstVideoFrame



#### SDK 开始渲染自己本地或远端用户的首帧画面。

SDK 会在渲染自己本地或远端用户的首帧画面时抛出该事件，您可以通过回调事件中的 userId 参数来判断事件来自于“本地”还是来自于“远端”。
-  如果 userId 为空值，代表 SDK 已经开始渲染自己本地的视频画面，不过前提是您已经调用了 [startLocalPreview](https://write.woa.com/document/87029900866228224) 或 [startScreenCapture](https://write.woa.com/document/87029900866228224)。

-  如果 userId 不为空，代表 SDK 已经开始渲染远端用户的视频画面，不过前提是您已经调用了 [startRemoteView](https://write.woa.com/document/87029900866228224) 订阅了该用户的视频画面。

<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >height</td>

<td rowspan="1" colSpan="1" >画面的高度。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >streamType</td>

<td rowspan="1" colSpan="1" >视频流类型：主路（Main）一般用于承载摄像头画面，辅路（Sub）一般用于承载屏幕分享画面。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >本地或远端的用户标识，如果 userId 为空值代表自己本地的首帧画面已到来，userId 不为空则代表远端用户的首帧画面已到来。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >width</td>

<td rowspan="1" colSpan="1" >画面的宽度。</td>
</tr>
</table>


> **注意**
> 

> 1. 只有当您调用了 [startLocalPreview](https://write.woa.com/document/87029900866228224) 或 [startScreenCapture](https://write.woa.com/document/87029900866228224) 之后，才会触发自己本地的首帧画面事件回调。
> 

> 2. 只有当您调用了 [startRemoteView](https://write.woa.com/document/87029900866228224) 或 startRemoteSubStreamView 之后，才会触发远端用户的首帧画面事件回调。
> 


## onFirstAudioFrame



#### SDK 开始播放远端用户的首帧音频。

SDK 会在播放远端用户的首帧音频时抛出该事件，本地音频的首帧事件暂不抛出。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >远端用户的用户标识。</td>
</tr>
</table>


## onSendFirstLocalVideoFrame



#### 自己本地的首个视频帧已被发布出去。

当您成功进入房间并通过 [startLocalPreview](https://write.woa.com/document/87029900866228224) 或 [startScreenCapture](https://write.woa.com/document/87029900866228224) 开启本地视频采集之后（开启采集和进入房间的先后顺序无影响），SDK 就会开始进行视频编码，并通过自身的网络模块向云端发布自己本地的视频数据。当 SDK 成功地向云端送出自己的第一帧视频数据帧以后，就会抛出 ` onSendFirstLocalVideoFrame ` 事件回调。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >streamType</td>

<td rowspan="1" colSpan="1" >视频流类型：主路（Main）一般用于承载摄像头画面，辅路（Sub）一般用于承载屏幕分享画面。</td>
</tr>
</table>


## onSendFirstLocalAudioFrame



#### 自己本地的首个音频帧已被发布出去。

当您成功进入房间并通过 [startLocalAudio](https://write.woa.com/document/87029900866228224) 开启本地音频采集之后（开启采集和进入房间的先后顺序无影响），SDK 就会开始进行音频编码，并通过自身的网络模块向云端发布自己本地的音频数据。当 SDK 成功地向云端送出自己的第一帧音频数据帧以后，就会抛出 ` onSendFirstLocalAudioFrame ` 事件回调。

## onRemoteVideoStatusUpdated



#### 远端视频状态变化的事件回调。

您可以通过此事件回调获取远端每一路画面的播放状态（包括 Playing、Loading 和 Stopped 三种状态），从而进行相应的 UI 展示。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >extrainfo</td>

<td rowspan="1" colSpan="1" >额外信息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >reason</td>

<td rowspan="1" colSpan="1" >视频状态改变的原因。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >status</td>

<td rowspan="1" colSpan="1" >视频状态：包括 Playing、Loading 和 Stopped 三种状态。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >streamType</td>

<td rowspan="1" colSpan="1" >视频流类型：主路（Main）一般用于承载摄像头画面，辅路（Sub）一般用于承载屏幕分享画面。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >用户标识。</td>
</tr>
</table>


## onRemoteAudioStatusUpdated



#### 远端音频状态变化的事件回调。

您可以通过此事件回调获取远端每一路音频的播放状态（包括 Playing、Loading 和 Stopped 三种状态），从而进行相应的 UI 展示。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >extrainfo</td>

<td rowspan="1" colSpan="1" >额外信息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >reason</td>

<td rowspan="1" colSpan="1" >音频状态改变的原因。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >status</td>

<td rowspan="1" colSpan="1" >音频状态：包括 Playing、Loading 和 Stopped 三种状态。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >用户标识。</td>
</tr>
</table>


## onUserVideoSizeChanged



#### 用户视频大小发生改变回调。

当您收到 ` onUserVideoSizeChanged(userId, streamType, newWidth, newHeight) ` 通知时，表示该路画面大小发生了调整，调整的原因可能是该用户调用了 [setVideoEncoderParam](https://write.woa.com/document/87029900866228224) 或者 [setSubStreamEncoderParam](https://write.woa.com/document/87029900866228224) 重新设置了画面尺寸。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >newHeight</td>

<td rowspan="1" colSpan="1" >视频流的高度（像素）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >newWidth</td>

<td rowspan="1" colSpan="1" >视频流的宽度（像素）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >streamType</td>

<td rowspan="1" colSpan="1" >视频流类型：主路（Main）一般用于承载摄像头画面，辅路（Sub）一般用于承载屏幕分享画面。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >用户标识。</td>
</tr>
</table>


## onNetworkQuality



#### 网络质量的实时统计回调。

该统计回调每间隔2秒抛出一次，用于通知 SDK 感知到的当前网络的上行和下行质量。

SDK 会使用一组内嵌的自研算法对当前网络的延迟高低、带宽大小以及稳定情况进行评估，并计算出一个评估结果：如果评估结果为 1（Excellent） 代表当前的网络情况非常好，如果评估结果为 6（Down）代表当前网络无法支撑 TRTC 的正常通话。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >localQuality</td>

<td rowspan="1" colSpan="1" >上行网络质量。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >remoteQuality</td>

<td rowspan="1" colSpan="1" >下行网络质量，代表数据流历经“远端->云端->本端”这样一条完整的传输链路后，最终在本端统计到的数据质量。因此，这里的下行网络质量代表的是远端上行链路与本端下行链路共同影响的结果。</td>
</tr>
</table>


> **注意**
> 

> 暂时无法通过该接口单独判定远端用户的上行质量。
> 


## onStatistics



#### 音视频技术指标的实时统计回调。

该统计回调每间隔2秒抛出一次，用于通知 SDK 内部音频、视频以及网络相关的专业技术指标，这些信息在 [TRTCStatistics](https://write.woa.com/document/87029938343555072) 均有罗列：
-  视频统计信息：视频的分辨率（resolution）、帧率（FPS）和比特率（bitrate）等信息。

-  音频统计信息：音频的采样率（samplerate）、声道（channel）和比特率（bitrate）等信息。

-  网络统计信息：SDK 和云端一次往返（SDK > Cloud > SDK）的网络耗时（rtt）、丢包率（loss）、上行流量（sentBytes）和下行流量（receivedBytes）等信息。

<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >statistics</td>

<td rowspan="1" colSpan="1" >统计数据，包括自己本地的统计信息和远端用户的统计信息，详情请参考 [TRTCStatistics](https://write.woa.com/document/87029938343555072)。</td>
</tr>
</table>


> **注意**
> 

> 如果您只需要获知当前网络质量的好坏，并不需要花太多时间研究本统计回调，更推荐您使用 [onNetworkQuality](https://write.woa.com/document/87029920275542016) 来解决问题。
> 


## onSpeedTestResult



#### 网速测试的结果回调。

该统计回调由 [startSpeedTest](https://write.woa.com/document/87029900866228224) 触发。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >result</td>

<td rowspan="1" colSpan="1" >网速测试结果，包括丢包、往返延迟、上下行的带宽速率，详情请参见 [TRTCSpeedTestResult](https://write.woa.com/document/87029993616093184)。</td>
</tr>
</table>


## onConnectionLost



#### SDK 与云端的连接已经断开。

SDK 会在跟云端的连接断开时抛出此事件回调，导致断开的原因大多是网络不可用或者网络切换所致，例如用户在通话中走进电梯时就可能会遇到此事件。

在抛出此事件之后，SDK 会努力跟云端重新建立连接，重连过程中会抛出 [onTryToReconnect](https://write.woa.com/document/87029920275542016)，连接恢复后会抛出 [onConnectionRecovery](https://write.woa.com/document/87029920275542016) 。

所以，SDK 会在如下三个连接相关的事件中按如下规律切换：

![](https://qcloudimg.tencent-cloud.cn/raw/fb3c40a4fca55b0010d385cf3b2472cd.png)

## onTryToReconnect



#### SDK 正在尝试重新连接到云端。

SDK 会在跟云端的连接断开时抛出 [onConnectionLost](https://write.woa.com/document/87029920275542016)，之后会努力跟云端重新建立连接并抛出本事件，连接恢复后会抛出 [onConnectionRecovery](https://write.woa.com/document/87029920275542016)。

## onConnectionRecovery



#### SDK 与云端的连接已经恢复。

SDK 会在跟云端的连接断开时抛出 [onConnectionLost](https://write.woa.com/document/87029920275542016)，之后会努力跟云端重新建立连接并抛出 [onTryToReconnect](https://write.woa.com/document/87029920275542016)，连接恢复后会抛出本事件回调。

## onCameraDidReady



#### 摄像头准备就绪。

当您调用 [startLocalPreview](https://write.woa.com/document/87029900866228224) 之后，SDK 会尝试启动摄像头，如果摄像头能够启动成功就会抛出本事件。

如果启动失败，大概率是因为当前应用没有获得访问摄像头的权限，或者摄像头当前正在被其他程序独占使用中。

您可以通过捕获 [onError](https://write.woa.com/document/87029920275542016) 事件回调获知这些异常情况并通过 UI 界面提示用户。

## onMicDidReady



#### 麦克风准备就绪。

当您调用 [startLocalAudio](https://write.woa.com/document/87029900866228224) 之后，SDK 会尝试启动麦克风，如果麦克风能够启动成功就会抛出本事件。

如果启动失败，大概率是因为当前应用没有获得访问麦克风的权限，或者麦克风当前正在被其他程序独占使用中。

您可以通过捕获 [onError](https://write.woa.com/document/87029920275542016) 事件回调获知这些异常情况并通过 UI 界面提示用户。

## onAudioRouteChanged



#### 当前音频路由发生变化（仅适用于移动设备）。

所谓“音频路由”，是指声音是从手机的扬声器还是从听筒中播放出来，音频路由变化也就是声音的播放位置发生了变化。
-  当音频路由为听筒时，声音比较小，只有将耳朵凑近才能听清楚，隐私性较好，适合用于接听电话。

-  当音频路由为扬声器时，声音比较大，不用将手机贴脸也能听清，因此可以实现“免提”的功能。

-  当音频路由为有线耳机。

-  当音频路由为蓝牙耳机。

-  当音频路由为USB专业声卡设备。

<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >fromRoute</td>

<td rowspan="1" colSpan="1" >变更前的音频路由。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >route</td>

<td rowspan="1" colSpan="1" >音频路由，即声音由哪里输出（扬声器、听筒）。</td>
</tr>
</table>


## onUserVoiceVolume



#### 音量大小的反馈回调。

SDK 可以评估每一路音频的音量大小，并每隔一段时间抛出该事件回调，您可以根据音量大小在 UI 上做出相应的提示，例如` 波形图 `或` 音量槽 `。

要完成这个功能， 您需要先调用 [enableAudioVolumeEvaluation](https://write.woa.com/document/87029900866228224) 开启这个能力并设定事件抛出的时间间隔。

需要补充说明的是，无论当前房间中是否有人说话，SDK 都会按照您设定的时间间隔定时抛出此事件回调。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >totalVolume</td>

<td rowspan="1" colSpan="1" >所有远端用户的总音量大小，取值范围 [0, 100]。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userVolumes</td>

<td rowspan="1" colSpan="1" >是一个数组，用于承载所有正在说话的用户的音量大小，取值范围 [0, 100]。</td>
</tr>
</table>


> **注意**
> 

> userVolumes 为一个数组，对于数组中的每一个元素，当 userId 为空时表示本地麦克风采集的音量大小，当 userId 不为空时代表远端用户的音量大小。
> 


## onRecvCustomCmdMsg



#### 收到自定义消息的事件回调。

当房间中的某个用户使用 [sendCustomCmdMsg](https://write.woa.com/document/87029900866228224) 发送自定义 UDP 消息时，房间中的其他用户可以通过 ` onRecvCustomCmdMsg ` 事件回调接收到该条消息。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >cmdID</td>

<td rowspan="1" colSpan="1" >命令 ID。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >message</td>

<td rowspan="1" colSpan="1" >消息数据。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >seq</td>

<td rowspan="1" colSpan="1" >消息序号。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >用户标识。</td>
</tr>
</table>


## onMissCustomCmdMsg



#### 自定义消息丢失的事件回调。

当您使用 [sendCustomCmdMsg](https://write.woa.com/document/87029900866228224) 发送自定义 UDP 消息时，即使设置了可靠传输（reliable），也无法确 100% 不丢失，只是丢消息概率极低，能满足常规可靠性要求。

在发送端设置了可靠运输（reliable）后，SDK 都会通过此回调通知过去时间段内（通常为5s）传输途中丢失的自定义消息数量统计信息。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >cmdID</td>

<td rowspan="1" colSpan="1" >命令 ID。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >errCode</td>

<td rowspan="1" colSpan="1" >错误码。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >missed</td>

<td rowspan="1" colSpan="1" >丢失的消息数量。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >用户标识。</td>
</tr>
</table>


> **注意**
> 

> 只有在发送端设置了可靠传输（reliable），接收方才能收到消息的丢失回调。
> 


## onRecvSEIMsg



#### 收到 SEI 消息的回调。

当房间中的某个用户使用 [sendSEIMsg](https://write.woa.com/document/87029900866228224) 借助视频数据帧发送 SEI 消息时，房间中的其他用户可以通过 ` onRecvSEIMsg ` 事件回调接收到该条消息。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >message</td>

<td rowspan="1" colSpan="1" >数据。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >用户标识。</td>
</tr>
</table>


## onStartPublishing



#### 开始向腾讯云直播 CDN 上发布音视频流的事件回调。

当您调用 startPublishing 开始向腾讯云直播 CDN 上发布音视频流时，SDK 会立刻将这一指令同步给云端服务器。

随后 SDK 会收到来自云端服务器的处理结果，并将指令的执行结果通过本事件回调通知给您。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >err</td>

<td rowspan="1" colSpan="1" >0表示成功，其余值表示失败，详见[错误码](https://cloud.tencent.com/document/product/647/32257)。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >errMsg</td>

<td rowspan="1" colSpan="1" >具体错误原因。</td>
</tr>
</table>


## onStopPublishing



#### 停止向腾讯云直播 CDN 上发布音视频流的事件回调。

当您调用 stopPublishing 停止向腾讯云直播 CDN 上发布音视频流时，SDK 会立刻将这一指令同步给云端服务器。

随后 SDK 会收到来自云端服务器的处理结果，并将指令的执行结果通过本事件回调通知给您。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >err</td>

<td rowspan="1" colSpan="1" >0表示成功，其余值表示失败，详见[错误码](https://cloud.tencent.com/document/product/647/32257)。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >errMsg</td>

<td rowspan="1" colSpan="1" >具体错误原因。</td>
</tr>
</table>


## onStartPublishCDNStream



#### 开始向非腾讯云 CDN 上发布音视频流的事件回调。

当您调用 startPublishCDNStream 开始向非腾讯云直播 CDN 上发布音视频流时，SDK 会立刻将这一指令同步给云端服务器。随后 SDK 会收到来自云端服务器的处理结果，并将指令的执行结果通过本事件回调通知给您。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >err</td>

<td rowspan="1" colSpan="1" >0表示成功，其余值表示失败，详见[错误码](https://cloud.tencent.com/document/product/647/32257)。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >errMsg</td>

<td rowspan="1" colSpan="1" >具体错误原因。</td>
</tr>
</table>


> **注意**
> 

> 当您收到成功的事件回调时，只是说明您的发布指令已经同步到腾讯云后台服务器，但如果目标 CDN 厂商的服务器不接收该条视频流，依然可能导致发布失败。
> 


## onStopPublishCDNStream



#### 停止向非腾讯云 CDN 上发布音视频流的事件回调。

当您调用 stopPublishCDNStream 开始向非腾讯云直播 CDN 上发布音视频流时，SDK 会立刻将这一指令同步给云端服务器。随后 SDK 会收到来自云端服务器的处理结果，并将指令的执行结果通过本事件回调通知给您。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >err</td>

<td rowspan="1" colSpan="1" >0表示成功，其余值表示失败，详见[错误码](https://cloud.tencent.com/document/product/647/32257)。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >errMsg</td>

<td rowspan="1" colSpan="1" >具体错误原因。</td>
</tr>
</table>


## onSetMixTranscodingConfig



#### 设置云端混流的排版布局和转码参数的事件回调。

当您调用 setMixTranscodingConfig 调整云端混流的排版布局和转码参数时，SDK 会立刻将这一调整指令同步给云端服务器。随后 SDK 会收到来自云端服务器的处理结果，并将指令的执行结果通过本事件回调通知给您。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >err</td>

<td rowspan="1" colSpan="1" >错误码：0表示成功，其余值表示失败，详见[错误码](https://cloud.tencent.com/document/product/647/32257)。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >errMsg</td>

<td rowspan="1" colSpan="1" >具体的错误原因。</td>
</tr>
</table>


## onStartPublishMediaStream



#### 开始发布媒体流的事件回调。

当您调用 [startPublishMediaStream](https://write.woa.com/document/87029900866228224) 开始向 TRTC 后台服务发布媒体流时，SDK 会立刻将这一指令同步给云端服务器，随后 SDK 会收到来自云端服务器的处理结果，并将指令的执行结果通过本事件回调通知给您。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >code</td>

<td rowspan="1" colSpan="1" >回调结果，0 表示成功，其余值表示失败，详见[错误码](https://cloud.tencent.com/document/product/647/32257)。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >extraInfo</td>

<td rowspan="1" colSpan="1" >扩展信息字段，个别错误码可能会带额外的信息帮助定位问题。<br>当 code 返回值为 ERR_SERVER_PROCESS_FAILED 时，意味着服务器无法处理您的请求，此时可使用"error_code"做为 key 获取到服务器返回的错误码，具体的错误码以及建议处理措施说明如下：<br>-  2000: 参数错误，建议检查请求参数<br>-  2001: 未开通直播服务，建议去直播控制台开通直播服务<br>-  2021: 未开通转推第三方服务，建议联系产品开通转推第三方服务<br>-  3000: 服务器内部错误，建议重试<br>-  4006: 同一个任务并发冲突，上一个 startPublishMediaStream 任务服务器还在处理中，建议延迟重试<br>-  4007: 同一个任务已经通过 startPublishMediaStream 启动成功，建议使用返回的 taskId 调用 updatePublishMediaStream 接口更新任务<br>-  5001: 资源受限，建议延迟重试</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >message</td>

<td rowspan="1" colSpan="1" >具体回调信息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >taskId</td>

<td rowspan="1" colSpan="1" >当请求成功时，TRTC 后台会在回调中提供给您这项任务的 taskId，后续您可以通过该 taskId 结合 [updatePublishMediaStream](https://write.woa.com/document/87029900866228224) 和 [stopPublishMediaStream](https://write.woa.com/document/87029900866228224) 进行更新和停止。</td>
</tr>
</table>


## onUpdatePublishMediaStream



#### 更新媒体流的事件回调。

当您调用媒体流发布接口 ([updatePublishMediaStream](https://write.woa.com/document/87029900866228224)) 开始向 TRTC 后台服务更新媒体流时，SDK 会立刻将这一指令同步给云端服务器，随后 SDK 会收到来自云端服务器的处理结果，并将指令的执行结果通过本事件回调通知给您。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >code</td>

<td rowspan="1" colSpan="1" >回调结果，0 表示成功，其余值表示失败，详见[错误码](https://cloud.tencent.com/document/product/647/32257)。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >extraInfo</td>

<td rowspan="1" colSpan="1" >扩展信息字段，个别错误码可能会带额外的信息帮助定位问题。<br>当 code 返回值为 ERR_SERVER_PROCESS_FAILED 时，意味着服务器无法处理您的请求，此时可使用"error_code"做为 key 获取到服务器返回的错误码，具体的错误码以及建议处理措施说明如下：<br>-  2000: 参数错误，建议检查请求参数<br>-  2001: 未开通直播服务，建议去直播控制台开通直播服务<br>-  2002: 找不到任务，建议调用 startPublishMediaStream 接口重新启动任务<br>-  2018: 并发请求乱序，建议使用最新混流参数重试<br>-  2021: 未开通转推第三方服务，建议联系产品开通转推第三方服务<br>-  3000: 服务器内部错误，建议重试<br>-  4003: 任务正在退出中，建议先调用 stopPublishMediaStream 接口停止任务，再调用 startPublishMediaStream 接口启动任务</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >message</td>

<td rowspan="1" colSpan="1" >具体回调信息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >taskId</td>

<td rowspan="1" colSpan="1" >您调用媒体流发布接口 ([updatePublishMediaStream](https://write.woa.com/document/87029900866228224)) 时传入的 taskId，会通过此回调再带回给您，用于标识该回调属于哪一次更新请求。</td>
</tr>
</table>


## onStopPublishMediaStream



#### 停止媒体流的事件回调。

当您调用停止发布媒体流 ([stopPublishMediaStream](https://write.woa.com/document/87029900866228224)) 开始向 TRTC 后台服务停止媒体流时，SDK 会立刻将这一指令同步给云端服务器，随后 SDK 会收到来自云端服务器的处理结果，并将指令的执行结果通过本事件回调通知给您。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >code</td>

<td rowspan="1" colSpan="1" >回调结果，0 表示成功，其余值表示失败，详见[错误码](https://cloud.tencent.com/document/product/647/32257)。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >extraInfo</td>

<td rowspan="1" colSpan="1" >扩展信息字段，个别错误码可能会带额外的信息帮助定位问题。<br>当 code 返回值为 ERR_SERVER_PROCESS_FAILED 时，意味着服务器无法处理您的请求，此时可使用"error_code"做为 key 获取到服务器返回的错误码，具体的错误码以及建议处理措施说明如下：<br>-  2000: 参数错误，建议检查请求参数<br>-  2002: 找不到任务，无需处理<br>-  3000: 服务器内部错误，建议重试<br>-  4003: 任务正在退出中，无需处理</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >message</td>

<td rowspan="1" colSpan="1" >具体回调信息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >taskId</td>

<td rowspan="1" colSpan="1" >您调用停止发布媒体流 ([stopPublishMediaStream](https://write.woa.com/document/87029900866228224)) 时传入的 taskId，会通过此回调再带回给您，用于标识该回调属于哪一次停止请求。</td>
</tr>
</table>


## onCdnStreamStateChanged



#### RTMP/RTMPS 推流状态发生改变回调。

当您调用 [startPublishMediaStream](https://write.woa.com/document/87029900866228224) 开始向 TRTC 后台服务发布媒体流时，SDK 会立刻将这一指令同步给云端服务。

若您在目标推流配置 ([TRTCPublishTarget](https://write.woa.com/document/87029993616093184)) 设置了向腾讯或者第三方 CDN 上发布音视频流的 URL 配置，则具体 RTMP 或者 RTMPS 推流状态将通过此回调同步给您。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >cdnUrl</td>

<td rowspan="1" colSpan="1" >您调用 [startPublishMediaStream](https://write.woa.com/document/87029900866228224) 时通过目标推流配置 ([TRTCPublishTarget](https://write.woa.com/document/87029993616093184)) 传入的 url，在推流状态变更时，会通过此回调同步给您。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >code</td>

<td rowspan="1" colSpan="1" >推流结果，0 表示成功，其余值表示出错，详见[错误码](https://cloud.tencent.com/document/product/647/32257)。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >extraInfo</td>

<td rowspan="1" colSpan="1" >扩展信息字段，个别错误码可能会带额外的信息帮助定位问题。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >message</td>

<td rowspan="1" colSpan="1" >具体推流信息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >status</td>

<td rowspan="1" colSpan="1" >推流状态。<br>-  0：推流未开始或者已结束。在您调用 [stopPublishMediaStream](https://write.woa.com/document/87029900866228224) 时会返回该状态。<br>-  1：正在连接 TRTC 服务器和 CDN 服务器。若无法立刻成功，TRTC 后台服务会多次重试尝试推流，并返回该状态（5s回调一次）。如成功进行推流，则进入状态 2；如服务器出错或 60 秒内未成功推流，则进入状态 4。<br>-  2：CDN 推流正在进行。在成功推流后，会返回该状态。<br>-  3：TRTC 服务器和 CDN 服务器推流中断，正在恢复。当 CDN 出现异常，或推流短暂中断时，TRTC 后台服务会自动尝试恢复推流，并返回该状态（5s回调一次）。如成功恢复推流，则进入状态 2；如服务器出错或 60 秒内未成功恢复，则进入状态 4。<br>-  4：TRTC 服务器和 CDN 服务器推流中断，且恢复或连接超时。即此时推流失败，您可以再次调用 [updatePublishMediaStream](https://write.woa.com/document/87029900866228224) 尝试推流。<br>-  5：正在断开 TRTC 服务器和 CDN 服务器。在您调用 [stopPublishMediaStream](https://write.woa.com/document/87029900866228224) 时，TRTC 后台服务会依次同步状态 5 和状态 0。</td>
</tr>
</table>


## onScreenCaptureStarted



#### 屏幕分享开启的事件回调。

当您通过 [startScreenCapture](https://write.woa.com/document/87029900866228224) 等相关接口启动屏幕分享时，SDK 便会抛出此事件回调。

## onScreenCapturePaused



#### 屏幕分享暂停的事件回调。

当您通过 [pauseScreenCapture](https://write.woa.com/document/87029900866228224) 暂停屏幕分享时，SDK 便会抛出此事件回调。

## onScreenCaptureResumed



#### 屏幕分享恢复的事件回调。

当您通过 [resumeScreenCapture](https://write.woa.com/document/87029900866228224) 恢复屏幕分享时，SDK 便会抛出此事件回调。

## onScreenCaptureStopped



#### 屏幕分享停止的事件回调。

当您通过 [stopScreenCapture](https://write.woa.com/document/87029900866228224) 停止屏幕分享时，SDK 便会抛出此事件回调。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >reason</td>

<td rowspan="1" colSpan="1" >停止原因，0：用户主动停止；1：屏幕窗口关闭导致停止；2：表示屏幕分享的显示屏状态变更（如接口被拔出、投影模式变更等）。</td>
</tr>
</table>


## onLocalRecordBegin



#### 本地录制任务已经开始的事件回调。

当您调用 [startLocalRecording](https://write.woa.com/document/87029900866228224) 启动本地媒体录制任务时，SDK 会抛出该事件回调，用于通知您录制任务是否已经顺利启动。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >errCode</td>

<td rowspan="1" colSpan="1" >状态码。<br>-  0：录制任务启动成功。<br>-  -1：内部错误导致录制任务启动失败。<br>-  -2：文件后缀名有误（例如不支持的录制格式）。<br>-  -6：录制已经启动，需要先停止录制。<br>-  -7：录制文件已存在，需要先删除文件。<br>-  -8：录制目录无写入权限，请检查目录权限问题。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >storagePath</td>

<td rowspan="1" colSpan="1" >录制文件存储路径。</td>
</tr>
</table>


## onLocalRecording



#### 本地录制任务正在进行中的进展事件回调。

当您调用 [startLocalRecording](https://write.woa.com/document/87029900866228224) 成功启动本地媒体录制任务后，SDK 会定时地抛出本事件回调。

您可通过捕获该事件回调来获知录制任务的健康状况。

您可以在 [startLocalRecording](https://write.woa.com/document/87029900866228224) 时设定本事件回调的抛出间隔。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >duration</td>

<td rowspan="1" colSpan="1" >已经录制的累计时长，单位毫秒。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >storagePath</td>

<td rowspan="1" colSpan="1" >录制文件存储路径。</td>
</tr>
</table>


## onLocalRecordFragment



#### 本地录制分片的事件回调。

当您开启分片录制时，每完成一个分片，都会通过此接口回调。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >storagePath</td>

<td rowspan="1" colSpan="1" >分片文件存储路径。</td>
</tr>
</table>


## onLocalRecordComplete



#### 本地录制任务已经结束的事件回调。

当您调用 [stopLocalRecording](https://write.woa.com/document/87029900866228224) 停止本地媒体录制任务时，SDK 会抛出该事件回调，用于通知您录制任务的最终结果。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >errCode</td>

<td rowspan="1" colSpan="1" >状态码。<br>-   0：结束录制任务成功。<br>-  -1：录制失败。<br>-  -2：切换分辨率或横竖屏导致录制结束。<br>-  -3：录制时间太短，或未采集到任何视频或音频数据，请检查录制时长，或是否已开启音、视频采集。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >storagePath</td>

<td rowspan="1" colSpan="1" >录制文件存储路径。</td>
</tr>
</table>


## onSnapshotComplete



#### 本地截图完成的事件回调。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >bmp</td>

<td rowspan="1" colSpan="1" >截图结果，如果 bmp 为 null 代表本次截图操作失败。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >data</td>

<td rowspan="1" colSpan="1" >截图数据，为 nullptr 表示截图失败。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >format</td>

<td rowspan="1" colSpan="1" >截图数据格式，目前只支持 TRTCVideoPixelFormat_BGRA32。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >height</td>

<td rowspan="1" colSpan="1" >截图画面的高度。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >length</td>

<td rowspan="1" colSpan="1" >截图数据长度，对于BGRA32而言，` length = width * height * 4 `。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >type</td>

<td rowspan="1" colSpan="1" >视频流类型。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >用户标识，如果 userId 为空字符串，则代表截取的是本地画面。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >width</td>

<td rowspan="1" colSpan="1" >截图画面的宽度。</td>
</tr>
</table>


> **注意**
> 

> 全平台 C++ 接口和 Java 接口在参数上是不一样的，C++ 接口用 7 个参数描述一个截图画面，Java 接口只用一个 Bitmap 描述一个截图画面。
> 


## onUserEnter



#### 有主播加入当前房间（已废弃）。

@deprecated 新版本开始不推荐使用，建议使用 [onRemoteUserEnterRoom](https://write.woa.com/document/87029920275542016) 替代之。

## onUserExit



#### 有主播离开当前房间（已废弃）。

@deprecated 新版本开始不推荐使用，建议使用 [onRemoteUserLeaveRoom](https://write.woa.com/document/87029920275542016) 替代之。

## onAudioEffectFinished



#### 音效播放已结束（已废弃）。

@deprecated 新版本开始不推荐使用，建议使用 [TXAudioEffectManager](https://write.woa.com/document/87029952305344512) 接口替代之。

新的接口中不再区分背景音乐和音效，而是统一用 [startPlayMusic](https://write.woa.com/document/87029952305344512) 取代之。

## onSpeedTest



#### 服务器测速的结果回调（已废弃）。

@deprecated 新版本开始不推荐使用，建议使用 [onSpeedTestResult](https://write.woa.com/document/87029920275542016) 接口替代之。