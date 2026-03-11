> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/en/llms.txt
> Use this file to discover all available pages before exploring further.

# TRTC Real-Time Communication (TRTC SDK) Documentation
## Overview
`TRTCCloudListener.java` provides the event callback interface for TRTC Real-Time Communication (TRTC SDK) on Android.


## TRTCVideoRenderListener
<table>
<tr>
<td rowspan="1" colSpan="1" >Function List</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onRenderVideoFrame](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Self-definition video rendering callback</td>
</tr>
</table>


## TRTCVideoFrameListener
<table>
<tr>
<td rowspan="1" colSpan="1" >Function List</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onGLContextCreated](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Notification that the SDK's internal OpenGL environment has been created</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onProcessVideoFrame](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Video processing callback for integrating third-party beauty components</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onGLContextDestory](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Notification that the SDK's internal OpenGL environment has been destroyed</td>
</tr>
</table>


## TRTCAudioFrameListener
<table>
<tr>
<td rowspan="1" colSpan="1" >Function List</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onCapturedAudioFrame](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Local audio data callback after preprocessing by the audio module</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onLocalProcessedAudioFrame](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Local audio data callback after preprocessing, sound-effect processing, and mixing BGM by the audio module</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onRemoteUserAudioFrame](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Audio data of each remote user before mixing</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onMixedPlayAudioFrame](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Callback of mixed audio data before final submission to the system for playback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onMixedAllAudioFrame](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Audio data mixed by the SDK (including collected and to-be-played audio)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onVoiceEarMonitorAudioFrame](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Audio data for ear return</td>
</tr>
</table>


## TRTCLogListener
<table>
<tr>
<td rowspan="1" colSpan="1" >Function List</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onLog](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Local LOG printing callback</td>
</tr>
</table>


## TRTCCloudListener
<table>
<tr>
<td rowspan="1" colSpan="1" >Function List</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onError](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Error event callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onWarning](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Warning event callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onEnterRoom](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Event callback for room entry success or failure</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onExitRoom](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Event callback for leaving the room</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onSwitchRole](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Event callback for switching roles</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onSwitchRoom](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Event callback for switching rooms result</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onConnectOtherRoom](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Event callback for cross-room communication request result</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onDisConnectOtherRoom](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Event callback for ending cross-room communication result</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onUpdateOtherRoomForwardMode](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Event callback for modifying cross-room broadcaster uplink capability result</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onRemoteUserEnterRoom](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >A user has joined the current room</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onRemoteUserLeaveRoom](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >A user has left the current room</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onUserVideoAvailable](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >A remote user has started/stopped publishing the main video stream</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onUserSubStreamAvailable](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >A remote user has started/stopped publishing the auxiliary video stream</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onUserAudioAvailable](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >A remote user has started/stopped publishing their audio</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onFirstVideoFrame](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >The SDK has started rendering the first frame of the local or remote user's video</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onFirstAudioFrame](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >The SDK has started playing the remote user's first audio frame</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onSendFirstLocalVideoFrame](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >The first local video frame has been published</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onSendFirstLocalAudioFrame](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >The first local audio frame has been published</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onRemoteVideoStatusUpdated](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Event callback for remote video status changes</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onRemoteAudioStatusUpdated](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Event callback for remote audio status changes</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onUserVideoSizeChanged](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Callback for changes in user video size</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onNetworkQuality](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Real-time statistics callback for network quality</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onStatistics](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Real-time statistics callback for audio and video technical indicators</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onSpeedTestResult](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Callback for internet speed test results</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onConnectionLost](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >The connection between the SDK and the cloud has been disconnected.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onTryToReconnect](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >The SDK is trying to reconnect to the cloud.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onConnectionRecovery](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >The connection between the SDK and the cloud has been restored.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onCameraDidReady](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Camera is ready</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onMicDidReady](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Microphone is ready</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onAudioRouteChanged](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Current audio routing has changed (applicable only to mobile devices)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onUserVoiceVolume](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Callback for volume feedback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onRecvCustomCmdMsg](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Receipt of a custom Definition message</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onMissCustomCmdMsg](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Event callback for lost custom Definition messages</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onRecvSEIMsg](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Callback for receiving SEI message</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onStartPublishing](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Event callback for starting to publish audio and video streams to Tencent CSS CDN</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onStopPublishing](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Event callback for stopping the publishing of audio and video streams to Tencent CSS CDN</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onStartPublishCDNStream](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Event callback for starting to publish audio and video streams to a non-Tencent Cloud CDN</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onStopPublishCDNStream](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Event callback for stopping the publishing of audio and video streams to a non-Tencent Cloud CDN</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onSetMixTranscodingConfig](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Event callback for setting the layout and transcoding parameters of Cloud Mixed Streaming</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onStartPublishMediaStream](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Event callback for starting to publish the media stream</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onUpdatePublishMediaStream](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Event callback for updating the media stream</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onStopPublishMediaStream](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Event callback for stopping the media stream</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onCdnStreamStateChanged](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >RTMP/RTMPS streaming status change callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onScreenCaptureStarted](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Event callback for starting screen sharing</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onScreenCapturePaused](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Event callback for pausing screen sharing</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onScreenCaptureResumed](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Event callback for resuming screen sharing</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onScreenCaptureStopped](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Event callback for stopping screen sharing</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onLocalRecordBegin](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Event callback for the local recording task that has started</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onLocalRecording](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Progress event callback for an ongoing local recording task</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onLocalRecordFragment](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Event callback for local recording shard</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onLocalRecordComplete](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Event callback for the local recording task that has ended</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onSnapshotComplete](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Event callback for local screenshot completion</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onUserEnter](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >A host has joined the current room (deprecated)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onUserExit](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >A host has left the current room (deprecated)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onAudioEffectFinished](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Sound effect playback has ended (deprecated)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onSpeedTest](https://write.woa.com/document/87029920275542016)</td>

<td rowspan="1" colSpan="1" >Callback for server speed test results (deprecated)</td>
</tr>
</table>


## onRenderVideoFrame



#### Self-definition video rendering callback

When you set a local or remote self-definition video rendering callback, the SDK will deliver the video frames, originally intended for the rendering controls, to you through this callback interface for self-definition rendering.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >frame</td>

<td rowspan="1" colSpan="1" >Information on video frames to be rendered.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >streamType</td>

<td rowspan="1" colSpan="1" >Frequency stream type: Main (generally used for carrying camera footage) and Sub (generally used for carrying screen sharing footage).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >UserId of the video source. If it's a local video callback (setLocalVideoRenderDelegate), this parameter can be ignored.</td>
</tr>
</table>


## onGLContextCreated



#### Notification that the SDK's internal OpenGL environment has been created

## onProcessVideoFrame



#### Video processing callback for integrating third-party beauty components

If you have purchased a third-party beauty filter component, you need to set the third-party beauty filter callback in TRTCCloud. TRTC will then deliver the video frames that need preprocessing through this callback interface.

You can then hand over the video frames from TRTC to the third-party beauty filter component for image processing. Since the data is readable and writable, the results from the third-party beauty filter can be synchronized back to TRTC for subsequent encoding and transmission.



Scenario 1: The beauty filter component generates a new texture on its own.

If the beauty filter component you are using generates a new texture (to carry the processed image) during the image processing, please set dstFrame.textureId to the new texture ID in the callback function:
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

Scenario 2: The beauty filter component requires you to provide the target texture.

If the third-party beauty filter module does not generate a new texture but requires an input texture and an output texture, you can consider the following solution:
``` java
int onProcessVideoFrame(TRTCCloudDef.TRTCVideoFrame srcFrame, TRTCCloudDef.TRTCVideoFrame dstFrame) {
    thirdparty_process(srcFrame.texture.textureId, srcFrame.width, srcFrame.height, dstFrame.texture.textureId);
    return 0;
}
```
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >dstFrame</td>

<td rowspan="1" colSpan="1" >Used to receive video frames processed by the third-party beauty filter.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >srcFrame</td>

<td rowspan="1" colSpan="1" >Used to carry camera footage collected by TRTC.</td>
</tr>
</table>


> **Note**
> 

> Currently supports only OpenGL texture schemes (PC supports only TRTCVideoBufferType_Buffer format).
> 


## onGLContextDestory



#### Notification that the SDK's internal OpenGL environment has been destroyed

## onCapturedAudioFrame



#### Local audio data callback after preprocessing by the audio module

After you set the audio data self-definition callback, the SDK will deliver the freshly collected and preprocessed (ANS, AEC, AGC) data to you in PCM format through this interface callback.
-  The time frame length of the audio callback from this interface is fixed at 0.02s, in PCM format.

-  The formula to convert time frame length to byte frame length is ` Sampling Rate × Time Frame Length × Number of Channels × Sampling Point Width `.

-  For example, with TRTC's default audio recording format of 48000 sampling rate, mono channel, and 16-bit sampling point width, the byte frame length is ` 48000 × 0.02s × 1 × 16bit = 15360bit = 1920 bytes `.

<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >frame</td>

<td rowspan="1" colSpan="1" >Audio data frame in PCM format.</td>
</tr>
</table>


> **Note**
> 

> 1. Please avoid any time-consuming operations in this callback function, as the SDK processes one frame of audio data every 20ms. If your processing time exceeds 20ms, it will cause sound anomalies.
> 

> 2. The audio data from this interface callback is read-write, meaning you can modify the audio data synchronously within the callback function, but ensure that the processing time is efficient.
> 

> 3. The audio data callback from this interface has undergone preprocessing (ANS, AEC, AGC) but does ** not include ** background music, sound effects, reverb, etc., with low latency.
> 


## onLocalProcessedAudioFrame



#### Local audio data callback after preprocessing, sound-effect processing, and mixing BGM by the audio module

After you set the audio data self-definition callback, the SDK will deliver the freshly collected and preprocessed audio data, processed with sound effects and mixed BGM, in PCM format through this interface callback before final network encoding.
-  The time frame length of the audio callback from this interface is fixed at 0.02s, in PCM format.

-  The formula to convert time frame length to byte frame length is ` Sampling Rate × Time Frame Length × Number of Channels × Sampling Point Width `.

-  Taking TRTC's default audio recording format as an example: 48000 sampling rate, mono, 16 sampling point width, the byte frame length is ` 48000 × 0.02s × 1 × 16bit = 15360bit = 1920 bytes `.




Special note:

You can achieve the signaling transmission purpose by setting the ` TRTCAudioFrame.extraData ` field in the interface. Since the data block at the head of the audio frame cannot be too large, it is recommended that when you write ` extraData `, try to control the signaling to be within a few bytes. If it exceeds 100 bytes, the written data will not be sent.



Other users in the room can receive data through the `TRTCAudioFrame.extraData` field callback in `onRemoteUserAudioFrame` of [TRTCAudioFrameListener](https://write.woa.com/document/87029920275542016).
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >frame</td>

<td rowspan="1" colSpan="1" >Audio data frame in PCM format.</td>
</tr>
</table>


> **Note**
> 

> 1. Please avoid any time-consuming operations in this callback function, as the SDK processes one frame of audio data every 20ms. If your processing time exceeds 20ms, it will cause sound anomalies.
> 

> 2. The audio data from this interface callback is read-write, meaning you can modify the audio data synchronously within the callback function, but ensure that the processing time is efficient.
> 

> 3. The data from this callback interface has undergone preprocessing (ANS, AEC, AGC), sound effects and mixed BGM processing, resulting in higher sound delay compared to [ onCapturedAudioFrame ](https://write.woa.com/document/87029920275542016).
> 


## onRemoteUserAudioFrame



#### Audio data of each remote user before mixing

After you set the audio data self-definition callback, the SDK will deliver the raw data of each remote source to you in PCM format through this interface callback before final mixing.
-  The time frame length of the audio callback from this interface is fixed at 0.02s, in PCM format.

-  The formula to convert time frame length to byte frame length is ` Sampling Rate × Time Frame Length × Number of Channels × Sampling Point Width `.

-  Taking TRTC's default audio recording format as an example: 48000 sampling rate, mono, 16 sampling point width, the byte frame length is ` 48000 × 0.02s × 1 × 16bit = 15360bit = 1920 bytes `.

<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >frame</td>

<td rowspan="1" colSpan="1" >Audio data frame in PCM format.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >User identifier.</td>
</tr>
</table>


> **Note**
> 

> The audio data from this callback interface is read-only and cannot be modified.
> 


## onMixedPlayAudioFrame



#### Callback of mixed audio data before final submission to the system for playback

After you set the audio data self-definition callback, the SDK will deliver the mixed audio data of each audio track to you in PCM format through this interface callback before submitting it for system playback.
-  The time frame length of the audio callback from this interface is fixed at 0.02s, in PCM format.

-  The formula to convert time frame length to byte frame length is ` Sampling Rate × Time Frame Length × Number of Channels × Sampling Point Width `.

-  For example, with TRTC's default audio recording format of 48000 sampling rate, mono channel, and 16-bit sampling point width, the byte frame length is ` 48000 × 0.02s × 1 × 16bit = 15360bit = 1920 bytes `.

<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >frame</td>

<td rowspan="1" colSpan="1" >Audio data frame in PCM format.</td>
</tr>
</table>


> **Note**
> 

> 1. Please avoid any time-consuming operations in this callback function, as the SDK processes one frame of audio data every 20ms. If your processing time exceeds 20ms, it will cause sound anomalies.
> 

> 2. The audio data from this interface callback is read-write, meaning you can modify the audio data synchronously within the callback function, but ensure that the processing time is efficient.
> 

> 3. This interface callback delivers the mixed data of each audio track to be played, but it does not include ear return audio data.
> 


## onMixedAllAudioFrame



#### Audio data mixed by the SDK (including collected and to-be-played audio)

After you set the audio data self-definition callback, the SDK will mix all the collected and to-be-played audio data and deliver it to you in PCM format through this interface callback for your self-definition recording.
-  The time frame length of the audio callback from this interface is fixed at 0.02s, in PCM format.

-  The formula to convert time frame length to byte frame length is ` Sampling Rate × Time Frame Length × Number of Channels × Sampling Point Width `.

-  For example, with TRTC's default audio recording format of 48000 sampling rate, mono channel, and 16-bit sampling point width, the byte frame length is ` 48000 × 0.02s × 1 × 16bit = 15360bit = 1920 bytes `.

<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >frame</td>

<td rowspan="1" colSpan="1" >Audio data frame in PCM format.</td>
</tr>
</table>


> **Note**
> 

> 1. This interface callback delivers the mixed data of all audio data from the SDK, including: local audio after 3A preprocessing, special effects overlay, and background music mixing; all remote audio; but not including ear return audio.
> 

> 2. The audio data from this interface callback does not support modification.
> 


## onVoiceEarMonitorAudioFrame



#### Audio data for ear return

After you set the audio data self-definition callback, the SDK will deliver the ear return audio data to you in PCM format through this interface callback before playback.
-  The audio time frame length from this interface callback is not fixed and is in PCM format.

-  The formula to convert time frame length to byte frame length is ` Sampling Rate × Time Frame Length × Number of Channels × Sampling Point Width `.

-  Taking the default audio recording format of TRTC with a sampling rate of 48000, mono, and 16-bit sample depth as an example, the byte frame length of 0.02s audio data is ` 48000 × 0.02s × 1 × 16bit = 15360bit = 1920 bytes `.

<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >frame</td>

<td rowspan="1" colSpan="1" >Audio data frame in PCM format.</td>
</tr>
</table>


> **Note**
> 

> 1. Please avoid performing any time-consuming operations in this callback function, as it may cause sound anomalies.
> 

> 2. The audio data from this interface callback is read-write, meaning you can modify the audio data synchronously within the callback function, but ensure that the processing time is efficient.
> 


## onLog



#### Local LOG printing callback

If you wish to capture the SDK's local log printing behavior, you can set a log callback, allowing the SDK to send all logs to you through this callback interface.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >level</td>

<td rowspan="1" colSpan="1" >For log levels, please refer to TRTC_LOG_LEVEL.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >log</td>

<td rowspan="1" colSpan="1" >Log content.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >module</td>

<td rowspan="1" colSpan="1" >Reserved field; currently has no specific meaning and is fixed at TXLiteAVSDK.</td>
</tr>
</table>


## onError



#### Error event callback

Error events indicate unrecoverable errors thrown by the SDK, such as room entry failure or device startup failure.

Reference document: [Error Code Table](https://cloud.tencent.com/document/product/647/38308)
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >errCode</td>

<td rowspan="1" colSpan="1" >Error Code</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >errMsg</td>

<td rowspan="1" colSpan="1" >Error Message</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >extInfo</td>

<td rowspan="1" colSpan="1" >Expand Information Field, some error codes may carry additional information to help pinpoint issues</td>
</tr>
</table>


## onWarning



#### Warning event callback

Warning events indicate prompt issues thrown by the SDK, such as video stuttering or high CPU utilization.

Reference document: [Error Code Table](https://cloud.tencent.com/document/product/647/38308)
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >extInfo</td>

<td rowspan="1" colSpan="1" >Expand Information Field, some warning codes may carry additional information to help pinpoint issues</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >warningCode</td>

<td rowspan="1" colSpan="1" >Warning Codes</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >warningMsg</td>

<td rowspan="1" colSpan="1" >Warning Information</td>
</tr>
</table>


## onEnterRoom



#### Event callback for room entry success or failure

After calling the enterRoom() method in TRTCCloud to enter the room, you will receive the onEnterRoom(result) callback from TRTCCloudListener:
-  If the entry is successful, the result will be a positive number (result > 0), representing the time taken to enter the room, in milliseconds (ms).

-  If the entry fails, the result will be a negative number (result < 0), representing the error code of the failure reason.


For the meaning of error codes of room entry failure, please see [Error Code Table](https://cloud.tencent.com/document/product/647/38308).
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >result</td>

<td rowspan="1" colSpan="1" >When result > 0, it means the time taken to enter the room (ms). When result < 0, it means the error code for entering the room.</td>
</tr>
</table>


> **Note**
> 

> 1. In versions before Ver6.6, only successful room entry would throw the onEnterRoom(result) callback; failure would be thrown by the onError() callback.
> 

> 2. In versions after Ver6.6: regardless of success or failure, the onEnterRoom(result) callback will be thrown, and room entry failure will also throw the onError() callback.
> 


## onExitRoom



#### Event callback for leaving the room

Calling the exitRoom interface in TRTCCloud will execute the related logic of leaving the room, such as releasing audio/video device resources and codec resources.

After all resources occupied by the SDK are released, the SDK will trigger the onExitRoom() callback to notify you.



If you want to call enterRoom again or switch to another audio and video SDK, please wait for the onExitRoom callback before performing related operations. Otherwise, you may encounter various abnormal issues, such as the camera and microphone equipment being forcibly occupied.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >reason</td>

<td rowspan="1" colSpan="1" >Reasons for leaving the room: 0: Actively call exitRoom to leave the room; 1: Kicked out of the current room by the server; 2: The entire current room is dissolved.</td>
</tr>
</table>


## onSwitchRole



#### Event callback for switching roles

Calling the switchRole() interface in TRTCCloud will switch the roles of anchor and audience. This operation will involve a circuit switching process, and once the SDK completes the switch, it will trigger the onSwitchRole() event callback.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >errCode</td>

<td rowspan="1" colSpan="1" >Error Code, ERR_NULL represents successful switching. For others, please refer to [ Error Code ](https://cloud.tencent.com/document/product/647/32257).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >errMsg</td>

<td rowspan="1" colSpan="1" >Error message.</td>
</tr>
</table>


## onSwitchRoom



#### Event callback for switching rooms result

Calling the switchRoom() interface in TRTCCloud allows the user to quickly switch from one room to another. After the SDK completes the switch, it will trigger the onSwitchRoom() event callback.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >errCode</td>

<td rowspan="1" colSpan="1" >Error Code, ERR_NULL represents successful switching. For others, please refer to [ Error Code ](https://cloud.tencent.com/document/product/647/32257).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >errMsg</td>

<td rowspan="1" colSpan="1" >Error message.</td>
</tr>
</table>


## onConnectOtherRoom



#### Event callback for cross-room communication request result

Calling the connectOtherRoom() interface in TRTCCloud will initiate a video call between broadcasters in two different rooms, which is the so-called “Host PK” feature.

The caller will receive the onConnectOtherRoom() callback to learn whether the cross-room communication is successful

If successful, all users in both rooms will receive the onUserVideoAvailable() callback from the PK anchor in the other room.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >errCode</td>

<td rowspan="1" colSpan="1" >Error Code, ERR_NULL represents successful switching. For others, please refer to [ Error Code ](https://cloud.tencent.com/document/product/647/32257).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >errMsg</td>

<td rowspan="1" colSpan="1" >Error message.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >User ID of the anchor in the other room for cross-room communication.</td>
</tr>
</table>


## onDisConnectOtherRoom



#### Event callback for ending cross-room communication result

## onUpdateOtherRoomForwardMode



#### Event callback for modifying cross-room broadcaster uplink capability result

## onRemoteUserEnterRoom



#### A user has joined the current room

For performance considerations, the behavior of this notification differs in two different TRTC application scenarios (i.e., AppScene, specified by the second parameter when calling enterRoom):
-  Live streaming scenarios (TRTC_APP_SCENE_LIVE and TRTC_APP_SCENE_VOICE_CHATROOM): In this scenario, users are distinguished between hosts and audience. This notification is only triggered when a host enters the room. Audience members entering the room will not trigger this notification.

-  Call scenarios (TRTC_APP_SCENE_VIDEOCALL and TRTC_APP_SCENE_AUDIOCALL): In this scenario, users are not distinguished by roles (all users can be considered as hosts). Any user entering the room will trigger this notification.

<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >User Identifier of the remote user.</td>
</tr>
</table>


> **Note**
> 

> 1. The event callbacks onRemoteUserEnterRoom and onRemoteUserLeaveRoom are only applicable for maintaining the "user list" in the current room. The presence of these callbacks does not necessarily imply video streams.
> 

> 2. To display the remote screen, please listen for the onUserVideoAvailable() event callback, which indicates whether a specific user has video footage.
> 


## onRemoteUserLeaveRoom



#### A user has left the current room

Corresponding to onRemoteUserEnterRoom, the behavior of this notification differs in two different application scenarios (i.e., AppScene, specified by the second parameter when calling enterRoom):
-  In live streaming scenarios (TRTC_APP_SCENE_LIVE and TRTC_APP_SCENE_VOICE_CHATROOM): This notification is triggered only when a host leaves the room. Audience members leaving the room will not trigger this notification.

-  In call scenarios (TRTC_APP_SCENE_VIDEOCALL and TRTC_APP_SCENE_AUDIOCALL): In this scenario, users are not distinguished by roles. Any user leaving the room will trigger this notification.

<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >reason</td>

<td rowspan="1" colSpan="1" >Reason for leaving: 0 indicates the user left the room voluntarily, 1 indicates a timeout exit, 2 indicates the user was kicked out of the room, and 3 indicates the anchor switched to audience mode and left the room.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >User Identifier of the remote user.</td>
</tr>
</table>


## onUserVideoAvailable



#### A remote user has started/stopped publishing the main video stream

**The primary video** is generally used to carry the camera's video feed. When you receive the onUserVideoAvailable(userId, true) notification, it indicates that video frames are available for playback on this channel.

At this point, you need to call the [startRemoteView](https://write.woa.com/document/87029900866228224) interface to subscribe to the user's remote screen. Upon successful subscription, you will continue to receive the user's first frame rendering callback onFirstVideoFrame(userId).



When you receive the onUserVideoAvailable(userId, false) notification, it means that the remote video on this channel has been turned off. The shutdown may be due to the user invoking [muteLocalVideo](https://write.woa.com/document/87029900866228224) or [stopLocalPreview](https://write.woa.com/document/87029900866228224).
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >available</td>

<td rowspan="1" colSpan="1" >Whether the user has published (or cancelled publishing) the Main Road Picture, true: published; false: cancelled.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >User Identifier of the remote user.</td>
</tr>
</table>


## onUserSubStreamAvailable



#### A remote user has started/stopped publishing the auxiliary video stream

"Auxiliary Road Picture" is generally used to carry the screen sharing content. When you receive the onUserSubStreamAvailable(userId, true) notification, it indicates that video frames are available for playback on this channel.

At this point, you need to call the [startRemoteView](https://write.woa.com/document/87029900866228224) interface to subscribe to the user's remote screen. Upon successful subscription, you will continue to receive the user's first frame rendering callback onFirstVideoFrame(userId).
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >available</td>

<td rowspan="1" colSpan="1" >Whether the user has published (or cancelled publishing) the auxiliary video content, true: published; false: cancelled.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >User Identifier of the remote user.</td>
</tr>
</table>


> **Note**
> 

> The function used to display the auxiliary road picture is [startRemoteView](https://write.woa.com/document/87029900866228224), not startRemoteSubStreamView. The latter has been deprecated.
> 


## onUserAudioAvailable



#### A remote user has started/stopped publishing their audio

When you receive the onUserAudioAvailable(userId, true) notification, it means the user has published their audio. At this time, the SDK behaves as follows:
-  In Automatic Subscription Mode, you do not need to take any action; the SDK will automatically play the user's audio.

-  In manual subscription mode, you can use [muteRemoteAudio](https://write.woa.com/document/87029900866228224)(userid, false) to play the user's audio.

<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >available</td>

<td rowspan="1" colSpan="1" >Whether the user has published (or cancelled publishing) their audio, true: published; false: cancelled.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >User Identifier of the remote user.</td>
</tr>
</table>


> **Note**
> 

> The SDK uses automatic subscription mode by default. You can set it to manual subscription by calling [setDefaultStreamRecvMode](https://write.woa.com/document/87029900866228224), but this must be done before you enter the room.
> 


## onFirstVideoFrame



#### The SDK has started rendering the first frame of the local or remote user's video

The SDK triggers this event when rendering the first video frame of the local or remote user. You can use the userId parameter in the callback event to determine whether the event is from "Local" or "Remote".
-  If userId is empty, it means the SDK has started rendering your local video footage, but you must have called [startLocalPreview](https://write.woa.com/document/87029900866228224) or [startScreenCapture](https://write.woa.com/document/87029900866228224).

-  If userId is not empty, it means the SDK has started rendering the remote user's video footage. However, you must have called [startRemoteView](https://write.woa.com/document/87029900866228224) to subscribe to the user's video footage.

<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >height</td>

<td rowspan="1" colSpan="1" >Height of the video footage.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >streamType</td>

<td rowspan="1" colSpan="1" >Video stream type: Main is generally used for carrying camera footage, while Sub is generally used for carrying screen sharing footage.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >The user identifier of local or remote. If userId is empty, it means your local first video frame has arrived. If userId is not empty, it means the remote user's first video frame has arrived.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >width</td>

<td rowspan="1" colSpan="1" >Width of the video footage.</td>
</tr>
</table>


> **Note**
> 

> 1. The local first video frame event callback is triggered only after you call [startLocalPreview](https://write.woa.com/document/87029900866228224) or [startScreenCapture](https://write.woa.com/document/87029900866228224).
> 

> 2. The remote user's first video frame event callback is triggered only after you call [startRemoteView](https://write.woa.com/document/87029900866228224) or startRemoteSubStreamView.
> 


## onFirstAudioFrame



#### The SDK has started playing the remote user's first audio frame

The SDK will throw this event when playing the remote user's first frame of audio. The first frame event of local audio is not thrown for now.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >User Identifier of the remote user.</td>
</tr>
</table>


## onSendFirstLocalVideoFrame



#### The first local video frame has been published

After successfully joining the room and starting local video capture via [startLocalPreview](https://write.woa.com/document/87029900866228224) or [startScreenCapture](https://write.woa.com/document/87029900866228224) (the order of starting capture and joining the room does not matter), the SDK will start video encoding and publish the local video data to the cloud using its network module. Once the SDK successfully sends the first frame of local video data to the cloud, the onSendFirstLocalVideoFrame event callback will be triggered.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >streamType</td>

<td rowspan="1" colSpan="1" >Video stream type: Main is generally used for carrying camera footage, while Sub is generally used for carrying screen sharing footage.</td>
</tr>
</table>


## onSendFirstLocalAudioFrame



#### The first local audio frame has been published

After successfully joining the room and starting local audio capture via [startLocalAudio](https://write.woa.com/document/87029900866228224) (the order of starting capture and joining the room does not matter), the SDK will start audio encoding and publish the local audio data to the cloud using its network module. Once the SDK successfully sends the first frame of local audio data to the cloud, the onSendFirstLocalAudioFrame event callback will be triggered.

## onRemoteVideoStatusUpdated



#### Event callback for remote video status changes

You can use this event callback to obtain the playback status of each remote video stream (including three states: Playing, Loading, and Stopped) for corresponding UI display.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >extrainfo</td>

<td rowspan="1" colSpan="1" >Additional Information.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >reason</td>

<td rowspan="1" colSpan="1" >Reasons for video status changes.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >status</td>

<td rowspan="1" colSpan="1" >Video Status: Including Playing, Loading, and Stopped states.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >streamType</td>

<td rowspan="1" colSpan="1" >Video stream type: Main is generally used for carrying camera footage, while Sub is generally used for carrying screen sharing footage.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >User identifier.</td>
</tr>
</table>


## onRemoteAudioStatusUpdated



#### Event callback for remote audio status changes

You can use this event callback to obtain the playback status of each remote audio stream (including three states: Playing, Loading, and Stopped) for corresponding UI display.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >extrainfo</td>

<td rowspan="1" colSpan="1" >Additional Information.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >reason</td>

<td rowspan="1" colSpan="1" >Reasons for audio status changes.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >status</td>

<td rowspan="1" colSpan="1" >Audio Status: Including Playing, Loading, and Stopped states.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >User identifier.</td>
</tr>
</table>


## onUserVideoSizeChanged



#### Callback for changes in user video size

When you receive the onUserVideoSizeChanged(userId, streamtype, newWidth, newHeight) notification, it indicates that the video size has changed, possibly because the user has called setVideoEncoderParam or setSubStreamEncoderParam to reset the video dimensions.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >newHeight</td>

<td rowspan="1" colSpan="1" >The height of the video stream (in pixels).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >newWidth</td>

<td rowspan="1" colSpan="1" >The width of the video stream (in pixels).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >streamType</td>

<td rowspan="1" colSpan="1" >Video stream type: Main is generally used for carrying camera footage, while Sub is generally used for carrying screen sharing footage.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >User identifier.</td>
</tr>
</table>


## onNetworkQuality



#### Real-time statistics callback for network quality

This statistical callback is thrown every 2 seconds to notify the SDK of the perceived current network's uplink and downlink quality.

The SDK uses a set of proprietary algorithms to assess the current network's latency, bandwidth, and stability, and calculates an evaluation result: An evaluation result of 1 (Excellent) indicates that the current network condition is very good, while a result of 6 (Down) indicates that the current network cannot support normal calls on TRTC.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >localQuality</td>

<td rowspan="1" colSpan="1" >Uplink network quality.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >remoteQuality</td>

<td rowspan="1" colSpan="1" >Downlink network quality, represents the data quality finally gathered at the client-end after the data stream travels through a complete transmission link from "remote-end -> cloud -> client-end". Thus, the downlink network quality represents the result influenced by both the remote uplink and the client downlink.</td>
</tr>
</table>


> **Note**
> 

> It is temporarily impossible to assess the remote user's uplink quality through this interface alone.
> 


## onStatistics



#### Real-time statistics callback for audio and video technical indicators

This statistical callback is thrown every 2 seconds, notifying the SDK internal audio, video, and network-related technical indicators. This information is listed in [TRTCStatistics](https://write.woa.com/document/87029938343555072):
-  Video statistical information: Video resolution, frame rate (FPS), and bitrate information.

-  Audio statistical information: Audio sample rate, channel, and bitrate information.

-  Network Statistics: Network Latency (RTT), Packet Loss Rate (loss), Upstream Traffic (sentBytes), Downstream Traffic (receivedBytes), and other information from a round-trip (SDK > Cloud > SDK).

<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >statistics</td>

<td rowspan="1" colSpan="1" >Statistics including local and remote user statistics, for details refer to [TRTCStatistics](https://write.woa.com/document/87029938343555072).</td>
</tr>
</table>


> **Note**
> 

> If you just need to know the current network quality and do not want to spend too much time studying this statistical callback, it is recommended to use [onNetworkQuality](https://write.woa.com/document/87029920275542016) to solve the problem.
> 


## onSpeedTestResult



#### Callback for internet speed test results

This statistical callback is triggered by startSpeedTest.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >result</td>

<td rowspan="1" colSpan="1" >Internet Speed Test results, including packet loss, round-trip delay, upstream and downstream bandwidth rates; for details, refer to [TRTCSpeedTestResult](https://write.woa.com/document/87029993616093184).</td>
</tr>
</table>


## onConnectionLost



#### The connection between the SDK and the cloud has been disconnected.

The SDK will throw this event callback when the connection to the cloud is disconnected. The main reasons for disconnection are network unavailability or network switching, such as when the user enters an elevator during a call.

After throwing this event, the SDK will attempt to re-establish the connection with the cloud. During the reconnection process, it will throw [onTryToReconnect](https://write.woa.com/document/87029920275542016), and once the connection is restored, it will throw [onConnectionRecovery](https://write.woa.com/document/87029920275542016).

Thus, the SDK will switch among the following three connection-related events in the following manner:

![](https://qcloudimg.tencent-cloud.cn/raw/fb3c40a4fca55b0010d385cf3b2472cd.png)

## onTryToReconnect



#### The SDK is trying to reconnect to the cloud.

The SDK will throw [onConnectionLost](https://write.woa.com/document/87029920275542016) when the connection to the cloud is disconnected, then it will attempt to re-establish the connection with the cloud and throw this event. Once the connection is restored, it will throw [onConnectionRecovery](https://write.woa.com/document/87029920275542016).

## onConnectionRecovery



#### The connection between the SDK and the cloud has been restored.

The SDK will throw [onConnectionLost](https://write.woa.com/document/87029920275542016) when the connection to the cloud is disconnected. It will then attempt to re-establish the connection and throw [onTryToReconnect](https://write.woa.com/document/87029920275542016). Once the connection is restored, this event callback will be triggered.

## onCameraDidReady



#### Camera is ready

When you call startLocalPreivew, the SDK will attempt to enable the camera. If successful, this event will be thrown.

If enabling the camera fails, it is most likely because the current application does not have access permissions to the camera or the camera is currently being used exclusively by another application.

You can capture the [onError](https://write.woa.com/document/87029920275542016) event callback to understand these exceptional conditions and prompt users through the UI interface.

## onMicDidReady



#### Microphone is ready

When you call [startLocalAudio](https://write.woa.com/document/87029900866228224), the SDK will attempt to enable the microphone. If successful, this event will be thrown.

If enabling the microphone fails, it is most likely because the current application does not have access permissions to the microphone or the microphone is currently being used exclusively by another application.

You can capture the [onError](https://write.woa.com/document/87029920275542016) event callback to understand these exceptional conditions and prompt users through the UI interface.

## onAudioRouteChanged



#### Current audio routing has changed (applicable only to mobile devices)

The term "Audio Routing" refers to whether the sound is played through the phone's speaker or receiver. A change in audio routing means a change in the playback location of the sound.
-  When the audio routing is set to receiver, the sound is quieter, and you need to bring the phone close to your ear to hear clearly. This offers better privacy and is suitable for phone calls.

-  When the audio routing is set to speaker, the sound is louder, allowing for clear listening without holding the phone to your face, thus enabling the "hands-free" feature.

-  When the audio routing is set to wired headphones.

-  When the audio routing is set to Bluetooth headphones.

-  When the audio routing is set to USB professional sound card device.

<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >fromRoute</td>

<td rowspan="1" colSpan="1" >Audio routing before the change.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >route</td>

<td rowspan="1" colSpan="1" >Audio routing, which refers to where the sound is output (speaker, receiver).</td>
</tr>
</table>


## onUserVoiceVolume



#### Callback for volume feedback

The SDK can assess the volume of each audio stream and periodically trigger this event callback. You can provide corresponding UI indications based on the volume, such as `waveform chart` or `volume slider`.

To implement this feature, you need to call [enableAudioVolumeEvaluation](https://write.woa.com/document/87029900866228224) to enable this capability and set the time interval for event triggers.

It is important to note that, regardless of whether anyone is speaking in the current room, the SDK will periodically trigger this event callback at the interval you set.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >totalVolume</td>

<td rowspan="1" colSpan="1" >The total volume level of all remote users, with a range of 0 to 100.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userVolumes</td>

<td rowspan="1" colSpan="1" >It is an array that holds the volume levels of all speaking users, with a range of 0 to 100.</td>
</tr>
</table>


> **Note**
> 

> userVolumes is an array. For each element in the array, if the userId is empty, it represents the volume level collected by the local microphone. If the userId is not empty, it represents the volume level of remote users.
> 


## onRecvCustomCmdMsg



#### Receipt of a custom Definition message

When a user in a room uses [sendCustomCmdMsg](https://write.woa.com/document/87029900866228224) to send a Definition UDP Message, other users in the room can receive the message through the onRecvCustomCmdMsg event callback.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >cmdID</td>

<td rowspan="1" colSpan="1" >Command ID.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >message</td>

<td rowspan="1" colSpan="1" >Message Data.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >seq</td>

<td rowspan="1" colSpan="1" >Message serial number.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >User identifier.</td>
</tr>
</table>


## onMissCustomCmdMsg



#### Event callback for lost custom Definition messages

When you use [sendCustomCmdMsg](https://write.woa.com/document/87029900866228224) to send a Definition UDP message, even if reliable transmission is set, it cannot guarantee 100% message delivery, but the probability of message loss is very low and meets conventional reliability requirements.

After setting reliable transmission on the sender side, the SDK will notify the number of lost Definition messages during the past time period (usually 5 seconds) through this callback.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >cmdID</td>

<td rowspan="1" colSpan="1" >Command ID.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >errCode</td>

<td rowspan="1" colSpan="1" >Error code.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >missed</td>

<td rowspan="1" colSpan="1" >Number of lost messages.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >User identifier.</td>
</tr>
</table>


> **Note**
> 

> Only if reliable transmission is set on the sender side can the receiver receive the message loss callback.
> 


## onRecvSEIMsg



#### Callback for receiving SEI message

When a user in the room sends an SEI message through the video frame using [sendSEIMsg](https://write.woa.com/document/87029900866228224), other users in the room can receive the message via the onRecvSEIMsg event callback.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >message</td>

<td rowspan="1" colSpan="1" >Data.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >User identifier.</td>
</tr>
</table>


## onStartPublishing



#### Event callback for starting to publish audio and video streams to Tencent CSS CDN

When you call startPublishing to start publishing audio and video streams to the Tencent CSS CDN, the SDK will immediately synchronize this command to the cloud server.

The SDK will then receive the processing results from the cloud server and notify you of the execution results of the command through this event callback.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >err</td>

<td rowspan="1" colSpan="1" >0 indicates success, other values indicate failure.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >errMsg</td>

<td rowspan="1" colSpan="1" >Specific error reasons.</td>
</tr>
</table>


## onStopPublishing



#### Event callback for stopping the publishing of audio and video streams to Tencent CSS CDN

When you call stopPublishing to stop publishing audio and video streams to the Tencent CSS CDN, the SDK will immediately synchronize this command to the cloud server.

The SDK will then receive the processing results from the cloud server and notify you of the execution results of the command through this event callback.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >err</td>

<td rowspan="1" colSpan="1" >0 indicates success, other values indicate failure.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >errMsg</td>

<td rowspan="1" colSpan="1" >Specific error reasons.</td>
</tr>
</table>


## onStartPublishCDNStream



#### Event callback for starting to publish audio and video streams to a non-Tencent Cloud CDN

When you call startPublishCDNStream to start publishing audio and video streams to a non-Tencent CSS CDN, the SDK will immediately synchronize this command to the cloud server. The SDK will then receive the processing results from the cloud server and notify you of the execution results of the command through this event callback.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >err</td>

<td rowspan="1" colSpan="1" >0 indicates success, other values indicate failure.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >errMsg</td>

<td rowspan="1" colSpan="1" >Specific error reasons.</td>
</tr>
</table>


> **Note**
> 

> When you receive a successful event callback, it only indicates that your publishing command has been synchronized to the Tencent Cloud backend server, but if the target CDN provider's server does not accept the video stream, it may still result in a publishing failure.
> 


## onStopPublishCDNStream



#### Event callback for stopping the publishing of audio and video streams to a non-Tencent Cloud CDN

When you call stopPublishCDNStream to stop publishing audio and video streams to a non-Tencent CSS CDN, the SDK will immediately synchronize this command to the cloud server. The SDK will then receive the processing results from the cloud server and notify you of the execution results of the command through this event callback.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >err</td>

<td rowspan="1" colSpan="1" >0 indicates success, other values indicate failure.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >errMsg</td>

<td rowspan="1" colSpan="1" >Specific error reasons.</td>
</tr>
</table>


## onSetMixTranscodingConfig



#### Event callback for setting the layout and transcoding parameters of Cloud Mixed Streaming

When you call setMixTranscodingConfig to adjust the layout and transcoding parameters of cloud mixed streaming, the SDK will immediately sync this adjustment command to the cloud server. The SDK will then receive the process results from the cloud server and notify you of the execution results through this event callback.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >err</td>

<td rowspan="1" colSpan="1" >Error code: 0 indicates success, other values indicate failure.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >errMsg</td>

<td rowspan="1" colSpan="1" >Specific error reason.</td>
</tr>
</table>


## onStartPublishMediaStream



#### Event callback for starting to publish the media stream

When you call [startPublishMediaStream](https://write.woa.com/document/87029900866228224) to start publishing the media stream to TRTC backend services, the SDK will immediately sync this command to the cloud server. The SDK will then receive the process results from the cloud server and notify you of the execution results through this event callback.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >code</td>

<td rowspan="1" colSpan="1" >Callback result, 0 indicates success, other values indicate failure.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >extraInfo</td>

<td rowspan="1" colSpan="1" >Expand information field, some error codes may carry additional information to help locate the problem.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >message</td>

<td rowspan="1" colSpan="1" >Specific callback information.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >taskId</td>

<td rowspan="1" colSpan="1" >When the request is successful, the TRTC backend will provide the taskId of this task in the callback. Subsequently, you can use this taskId in combination with [updatePublishMediaStream](https://write.woa.com/document/87029900866228224) and [stopPublishMediaStream](https://write.woa.com/document/87029900866228224) to update and stop.</td>
</tr>
</table>


## onUpdatePublishMediaStream



#### Event callback for updating the media stream

When you call the media stream publishing interface ([updatePublishMediaStream](https://write.woa.com/document/87029900866228224)) to start updating the media stream to the TRTC backend services, the SDK will immediately sync this command to the cloud server. The SDK will then receive the process results from the cloud server and notify you of the execution results through this event callback.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >code</td>

<td rowspan="1" colSpan="1" >Callback result, 0 indicates success, other values indicate failure.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >extraInfo</td>

<td rowspan="1" colSpan="1" >Expand information field, some error codes may carry additional information to help locate the problem.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >message</td>

<td rowspan="1" colSpan="1" >Specific callback information.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >taskId</td>

<td rowspan="1" colSpan="1" >The taskId you provide when calling the media stream publishing interface ([updatePublishMediaStream](https://write.woa.com/document/87029900866228224)) will be brought back to you through this callback, to identify which update request this callback belongs to.</td>
</tr>
</table>


## onStopPublishMediaStream



#### Event callback for stopping the media stream

When you call stop publishing media stream ([stopPublishMediaStream](https://write.woa.com/document/87029900866228224)) to stop the media stream to TRTC backend service, the SDK will immediately synchronize this command to the cloud server. Subsequently, the SDK will receive the process results from the cloud server and notify you of the execution results of the command through this event callback.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >code</td>

<td rowspan="1" colSpan="1" >Callback result, 0 indicates success, other values indicate failure.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >extraInfo</td>

<td rowspan="1" colSpan="1" >Expand information field, some error codes may carry additional information to help locate the problem.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >message</td>

<td rowspan="1" colSpan="1" >Specific callback information.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >taskId</td>

<td rowspan="1" colSpan="1" >The taskId you passed in when you called stop publishing media stream ([stopPublishMediaStream](https://write.woa.com/document/87029900866228224)) will be brought back to you through this callback, identifying which stop request this callback belongs to.</td>
</tr>
</table>


## onCdnStreamStateChanged



#### RTMP/RTMPS streaming status change callback

When you call [startPublishMediaStream](https://write.woa.com/document/87029900866228224) to start publishing media stream to TRTC backend service, the SDK will immediately synchronize this command to the cloud service.

If you set the URL configuration for publishing audio and video streaming to Tencent or third-party CDN in the target stream configuration ([TRTCPublishTarget](https://write.woa.com/document/87029993616093184)), the specific RTMP or RTMPS streaming status will be synchronized to you through this callback.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >cdnUrl</td>

<td rowspan="1" colSpan="1" >The URL you passed in through the target stream configuration ([TRTCPublishTarget](https://write.woa.com/document/87029993616093184)) when you called [startPublishMediaStream](https://write.woa.com/document/87029900866228224) will be synchronized to you through this callback when the streaming status changes.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >code</td>

<td rowspan="1" colSpan="1" >Stream Push Result, 0 means success, other values indicate an error.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >extraInfo</td>

<td rowspan="1" colSpan="1" >Expand information field, some error codes may carry additional information to help locate the problem.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >message</td>

<td rowspan="1" colSpan="1" >Specific Stream Push Information.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >status</td>

<td rowspan="1" colSpan="1" >Streaming Status.<br>-  0: Streaming not started or already ended. This status is returned when you call [stopPublishMediaStream](https://write.woa.com/document/87029900866228224).<br>-  1: Connecting to TRTC server and CDN server. If not immediately successful, TRTC backend service will retry multiple times and return this status (callback every 5s). If successful, it enters status 2; if server error occurs or streaming is not successful within 60 seconds, it enters status 4.<br>-  2: CDN streaming is in progress. This status is returned when streaming is successful.<br>-  3: TRTC server and CDN server streaming interruption, recovering. When CDN has an issue or streaming briefly interrupts, the TRTC backend service will automatically attempt to recover streaming and return this status (callback every 5 seconds). If streaming recovers successfully, it will transition to status 2; if server error occurs or recovery fails within 60 seconds, it will transition to status 4.<br>-  4: TRTC server and CDN server streaming interrupted, and recovery or connection timeout. At this point, streaming failed, you can call [updatePublishMediaStream](https://write.woa.com/document/87029900866228224) again to attempt streaming.<br>-  5: Disconnecting TRTC server and CDN server. When you call [stopPublishMediaStream](https://write.woa.com/document/87029900866228224), the TRTC backend service will transition to status 5 and then status 0.</td>
</tr>
</table>


## onScreenCaptureStarted



#### Event callback for starting screen sharing

When you start screen sharing through [startScreenCapture](https://write.woa.com/document/87029900866228224) or related interfaces, the SDK will trigger this event callback.

## onScreenCapturePaused



#### Event callback for pausing screen sharing

When you pause screen sharing through [pauseScreenCapture](https://write.woa.com/document/87029900866228224), the SDK will trigger this event callback.

## onScreenCaptureResumed



#### Event callback for resuming screen sharing

When you resume screen sharing through [resumeScreenCapture](https://write.woa.com/document/87029900866228224), the SDK will trigger this event callback.

## onScreenCaptureStopped



#### Event callback for stopping screen sharing

When you stop screen sharing by calling [stopScreenCapture](https://write.woa.com/document/87029900866228224), the SDK will trigger this event callback.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >reason</td>

<td rowspan="1" colSpan="1" >Stop Reason, 0: User proactively stopped; 1: Screen window closed causing stop; 2: Indicates a change in the display screen status for screen sharing (e.g., interface unplugged, change in projection mode, etc.).</td>
</tr>
</table>


## onLocalRecordBegin



#### Event callback for the local recording task that has started

When you start a local media recording task by calling [startLocalRecording](https://write.woa.com/document/87029900866228224), the SDK will trigger this event callback to notify you whether the recording task has successfully started.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >errCode</td>

<td rowspan="1" colSpan="1" >Status Code.<br>-  0: Recording task started successfully.<br>-  -1: Internal error caused the recording task to fail to start.<br>-  -2: Incorrect file suffix name (e.g., unsupported recording format).<br>-  -6: Recording has already started, needs to stop recording first.<br>-  -7: Recording file already exists, needs to delete the file first.<br>-  -8: No write permission in the recording directory, please check directory permissions.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >storagePath</td>

<td rowspan="1" colSpan="1" >CFS path for recording.</td>
</tr>
</table>


## onLocalRecording



#### Progress event callback for an ongoing local recording task

After you successfully start a local media recording task by calling [startLocalRecording](https://write.woa.com/document/87029900866228224), the SDK will periodically trigger this event callback.

You can capture this event callback to know the health status of the recording task.

You can set the interval for this event callback when you call [startLocalRecording](https://write.woa.com/document/87029900866228224).
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >duration</td>

<td rowspan="1" colSpan="1" >The cumulative recorded duration in milliseconds.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >storagePath</td>

<td rowspan="1" colSpan="1" >CFS path for recording.</td>
</tr>
</table>


## onLocalRecordFragment



#### Event callback for local recording shard

When you enable shard recording, each completed shard will trigger a callback through this interface.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >storagePath</td>

<td rowspan="1" colSpan="1" >Shard CFS path.</td>
</tr>
</table>


## onLocalRecordComplete



#### Event callback for the local recording task that has ended

When you call [stopLocalRecording](https://write.woa.com/document/87029900866228224) to stop the local media recording task, the SDK will trigger this event callback to notify you of the final result of the recording task.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >errCode</td>

<td rowspan="1" colSpan="1" >Status Code.<br>-   0: Successfully ended the recording task.<br>-  -1: Recording failed.<br>-  -2: Changing resolution or switching between portrait and landscape mode caused the recording to end.<br>-  -3: The recording duration is too short, or no video or audio data was captured. Please check the recording duration, or whether audio and video capture is enabled.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >storagePath</td>

<td rowspan="1" colSpan="1" >CFS path for recording.</td>
</tr>
</table>


## onSnapshotComplete



#### Event callback for local screenshot completion
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >bmp</td>

<td rowspan="1" colSpan="1" >Screenshot result, if bmp is null it means the screenshot operation failed.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >data</td>

<td rowspan="1" colSpan="1" >Screenshot data, nullptr means the screenshot failed.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >format</td>

<td rowspan="1" colSpan="1" >Screenshot data format, currently only supports TRTCVideoPixelFormat_BGRA32.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >height</td>

<td rowspan="1" colSpan="1" >Height of the screenshot.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >length</td>

<td rowspan="1" colSpan="1" >Length of the screenshot data, for BGRA32, length = width * height * 4.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >type</td>

<td rowspan="1" colSpan="1" >Video stream type.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >User Identifier, if userId is an empty string, it means the local screen was captured.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >width</td>

<td rowspan="1" colSpan="1" >Width of the screenshot.</td>
</tr>
</table>


> **Note**
> 

> The parameters for the C++ interface and the Java interface across all platforms are different. The C++ interface uses 7 parameters to describe a screenshot, while the Java interface uses only one Bitmap to describe a screenshot.
> 


## onUserEnter



#### A host has joined the current room (deprecated)

@deprecated Starting from the new version, it is recommended to use [onRemoteUserEnterRoom](https://write.woa.com/document/87029920275542016) instead.

## onUserExit



#### A host has left the current room (deprecated)

@deprecated Starting from the new version, it is recommended to use [onRemoteUserLeaveRoom](https://write.woa.com/document/87029920275542016) instead.

## onAudioEffectFinished



#### Sound effect playback has ended (deprecated)

@deprecated Starting from the new version, it is recommended to use the ITXAudioEffectManager interface instead.

In the new interface, background music and sound effects are no longer distinguished and are unified with [startPlayMusic](https://write.woa.com/document/87029952305344512) instead.

## onSpeedTest



#### Callback for server speed test results (deprecated)

@deprecated Starting from the new version, it is recommended to use the [onSpeedTestResult](https://write.woa.com/document/87029920275542016) interface instead.