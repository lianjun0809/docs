> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

# TRTC Real-Time Communication (TRTC SDK) Documentation
## Overview
`ITRTCCloud.h` is the API reference for TRTC Real-Time Communication (TRTC SDK) on C++. It provides detailed documentation for features including stream publishing, stream playback, stream mixing, and recording.


## ITRTCCloud
<table>
<tr>
<td rowspan="1" colSpan="1" >Function List</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getTRTCShareInstance](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Create a `TRTCCloud` Instance (Singleton Pattern)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[destroyTRTCShareInstance](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Terminate `TRTCCloud` Instance (Singleton Pattern)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addCallback](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Add TRTC Event Callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeCallback](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Remove TRTC Event Callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[enterRoom](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Enter Room</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[exitRoom](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Leave Room</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[switchRole](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Switch Role</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[switchRole](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Switch Role (Supports Setting Permission Bit)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[switchRoom](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Switch Room</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[connectOtherRoom](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Request Cross-room Communication</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[disconnectOtherRoom](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Exit Cross-room Communication</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setDefaultStreamRecvMode](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Set Subscription Mode (Needs to be set before entering the room to take effect)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createSubCloud](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Create Sub-room Instances (For Multi-room Concurrent Viewing)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[destroySubCloud](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Terminate Sub-room Instances</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[updateOtherRoomForwardMode](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Modify the uplink capability of cross-room broadcasters in this room</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[startPublishMediaStream](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Start publishing media stream</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[updatePublishMediaStream](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Update the published media stream.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[stopPublishMediaStream](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Stop publishing media stream.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[startLocalPreview](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Enable the preview screen of the local camera (Mobile Terminal)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[startLocalPreview](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Enable the preview screen of the local camera (Desktop Terminal)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[updateLocalView](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Update the preview screen of the local camera</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[stopLocalPreview](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Stop camera preview</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[muteLocalVideo](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Suspend/Resume publishing local video stream</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setVideoMuteImage](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Set the alternative image during the suspension of the local screen</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[startRemoteView](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Subscribe to the video stream of a remote user and bind the video rendering control</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[updateRemoteView](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Update the video rendering control of a remote user</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[stopRemoteView](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Unsubscribe from the remote user's video stream and release the rendering control</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[stopAllRemoteView](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Unsubscribe from all remote users' video streams and release all rendering resources</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[muteRemoteVideoStream](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Suspend/Resume subscription of the remote user's video stream</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[muteAllRemoteVideoStreams](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Suspend/Resume subscription of all remote users' video streams</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setVideoEncoderParam](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Set encoding parameters for the video encoder</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setNetworkQosParam](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Set network quality control parameters</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setLocalRenderParams](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Set rendering parameters for the local screen</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setRemoteRenderParams](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Set rendering mode for the remote screen</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[enableSmallVideoStream](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Enable picture-in-picture dual-stream encoding mode</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setRemoteVideoStreamType](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Switch picture-in-picture for the specified remote user</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[snapshotVideo](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Take a video screenshot</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGravitySensorAdaptiveMode](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Set gravity sensing adaptive mode (11.7 and above)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[startLocalAudio](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Enable collection and publishing of local audio</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[stopLocalAudio](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Stop collection and publishing of local audio</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[muteLocalAudio](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Pause/Resume publishing of the local audio stream</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[muteRemoteAudio](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Pause/Resume playing of the remote audio stream</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[muteAllRemoteAudio](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Pause/Resume playing of all remote users' audio streams</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setRemoteAudioVolume](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Set the playback volume for a specific remote user</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setAudioCaptureVolume](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Sets the local audio capture volume.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getAudioCaptureVolume](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Obtains the local audio capture volume.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setAudioPlayoutVolume](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Sets the remote audio playback volume.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getAudioPlayoutVolume](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Obtains the remote audio playback volume.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[enableAudioVolumeEvaluation](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Enable volume reminder</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[startAudioRecording](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Start recording</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[stopAudioRecording](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Stop recording</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[startLocalRecording](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Enable local media recording</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[stopLocalRecording](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Stop local media recording</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setRemoteAudioParallelParams](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Set intelligent concurrent playback strategy for remote audio streams</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[enable3DSpatialAudioEffect](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Enable 3D audio</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[updateSelf3DSpatialPosition](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Set self coordinates and orientation information in 3D audio</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[updateRemote3DSpatialPosition](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Set remote user coordinate information in 3D audio</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[set3DSpatialReceivingRange](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Set the receivable range of sounds emitted by a specified user</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getDeviceManager](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Get Device Management Class (TXDeviceManager)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setBeautyStyle](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Set special effects like beauty filter, whitening, and rosy skin</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setWaterMark](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Watermarking</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getAudioEffectManager](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Get Audio Effect Management Class (TXAudioEffectManager)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[startSystemAudioLoopback](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Enable System Sound Capture (iOS not yet supported)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[stopSystemAudioLoopback](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Stop System Sound Capture (iOS not yet supported)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setSystemAudioLoopbackVolume](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Sets the Volume of System Sound Capture</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[startScreenCapture](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Start Screen Sharing</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[stopScreenCapture](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Stopping Screen Sharing</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[pauseScreenCapture](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Pause Screen Sharing</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[resumeScreenCapture](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Resume Screen Sharing</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getScreenCaptureSources](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Enumerate shareable screens and windows (this interface supports only desktop systems)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[selectScreenCaptureTarget](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Select the screen or window to share (this interface supports only desktop systems)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setSubStreamEncoderParam](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Set Video Encoding Parameters for Screen Sharing (Sub-Stream) (Supported on Both Desktop and Mobile Systems)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setSubStreamMixVolume](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Set the Mixing Volume for Screen Sharing (This Interface Supports Only Desktop Systems)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addExcludedShareWindow](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Add the Specified Window to the Exclusion List of Screen Sharing (This Interface Supports Only Desktop Systems)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeExcludedShareWindow](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Remove the Specified Window from the Exclusion List of Screen Sharing (This Interface Supports Only Desktop Systems)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeAllExcludedShareWindow](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Remove All Windows from the Exclusion List of Screen Sharing (This Interface Supports Only Desktop Systems)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addIncludedShareWindow](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Add the Specified Window to the Contains List of Screen Sharing (This Interface Supports Only Desktop Systems)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeIncludedShareWindow](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Remove the Specified Window from the Contains List of Screen Sharing (This Interface Supports Only Desktop Systems)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeAllIncludedShareWindow](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Remove All Windows from the Contains List of Screen Sharing (This Interface Supports Only Desktop Systems)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[enableCustomVideoCapture](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Enable/Disable Custom Video Capturing Mode</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[sendCustomVideoData](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Submit Self-collected Video Frames to the SDK</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[enableCustomAudioCapture](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Enable Custom Audio Capturing Mode</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[sendCustomAudioData](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Submit Self-collected Audio Data to the SDK</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[enableMixExternalAudioFrame](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Enable/Disable Custom Audio Track</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[mixExternalAudioFrame](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Mix Custom Audio Track into the SDK</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setMixExternalAudioVolume](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Set the Streaming Volume and Playback Volume for External Audio Mixed During Streaming</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[generateCustomPTS](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Generate Timestamp for Custom Capturing</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[enableLocalVideoCustomProcess](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >.1 Enable third-party beauty filter for video</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setLocalVideoCustomProcessCallback](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >.2 Set video data callback for third-party beauty filter</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setLocalVideoRenderCallback](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Set Local Video Custom Rendering Callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setRemoteVideoRenderCallback](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Sets the rendering callback for remote video self-definition</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setAudioFrameCallback](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Sets the audio data self-definition callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setCapturedAudioFrameCallbackFormat](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Sets the callback format for audio frames captured by the local microphone</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setLocalProcessedAudioFrameCallbackFormat](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Sets the callback format for local audio frames after preprocessing</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setMixedPlayAudioFrameCallbackFormat](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Sets the callback format for audio frames that will eventually be played by the system</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[enableCustomAudioRendering](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Enable self-definition audio playback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getCustomAudioRenderingFrame](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Get playable audio data</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[sendCustomCmdMsg](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Sends a custom message using UDP channel to all users in a room</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[sendSEIMsg](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Sends a custom message using SEI channel to all users in a room</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[startSpeedTest](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Start internet speed test (use before entering the room)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[stopSpeedTest](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Stops network speed testing</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getSDKVersion](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Obtains the SDK version.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setLogLevel](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Sets the log output level.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setConsoleEnabled](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Enables/Disables console log print.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setLogCompressEnabled](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Enables/Disables local log compression</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setLogDirPath](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Sets the save path for local logs</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setLogCallback](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Log callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[showDebugView](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Show Dashboard</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[callExperimentalAPI](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Calls an experimental API.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[enablePayloadPrivateEncryption](https://write.woa.com/document/87030026264555520)</td>

<td rowspan="1" colSpan="1" >Enable or disable media stream private encryption</td>
</tr>
</table>


## getTRTCShareInstance



#### Create a `TRTCCloud` Instance (Singleton Pattern)
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >context</td>

<td rowspan="1" colSpan="1" >Only applies to the Android platform. The SDK internally converts it to the Android platform's ApplicationContext to call Android System API.<br>If the passed context parameter is NULL, the SDK will automatically obtain the current process's ApplicationContext.</td>
</tr>
</table>


> **Note**
> 

> 1. Using delete ITRTCCloud* will cause compilation errors. Please use destroyTRTCCloud to release the object pointer.
> 

> 2. On Windows, Mac, and iOS platforms, please call the getTRTCShareInstance() interface.
> 

> 3. On the Android platform, please call the getTRTCShareInstance(void *context) interface.
> 


## destroyTRTCShareInstance



#### Terminate `TRTCCloud` Instance (Singleton Pattern)

## addCallback



#### Add TRTC Event Callback

You can obtain various event notifications from the SDK through [ITRTCCloudCallback](https://write.woa.com/document/87030021158866944) (e.g., Error Code, Warning Code, Audio and Video Status Parameters, etc.).

## removeCallback



#### Remove TRTC Event Callback

## enterRoom



#### Enter Room

All TRTC users must enter a room to "publish" or "subscribe" to audio and video streams. "Publish" means pushing your audio and video to the cloud, and "subscribe" means pulling audio and video streams from other users in the room from the cloud.

To call this interface, you need to specify your application scenario [TRTCAppScene](https://write.woa.com/document/87030132707430400) for the best audio and video transmission experience. These scenarios can be divided into two major categories:



**Real-time Call:**

Includes [TRTCAppSceneVideoCall](https://write.woa.com/document/87030132707430400) and [TRTCAppSceneAudioCall](https://write.woa.com/document/87030132707430400) as two options: video call and audio call. This mode is suitable for 1-on-1 audio and video calls or online meetings with up to 300 participants.



**Online Live Streaming:**

Includes [TRTCAppSceneLIVE](https://write.woa.com/document/87030132707430400) and [TRTCAppSceneVoiceChatRoom](https://write.woa.com/document/87030132707430400) as two options: video live streaming and voice live streaming. This mode is suitable for online live streaming scenarios with up to 100,000 participants. However, you need to specify the **role** field in the TRTCParams parameter introduced later, distinguishing users in the room into two different roles: **Anchor** ([TRTCRoleAnchor](https://write.woa.com/document/87030132707430400)) and **Audience** ([TRTCRoleAudience](https://write.woa.com/document/87030132707430400)).



After calling this interface, you will receive the onEnterRoom(result) callback from [ITRTCCloudCallback](https://write.woa.com/document/87030021158866944):
-  If entering the room is successful, the result parameter will be a positive number (result > 0), indicating the time taken from the function call to entering the room, in milliseconds (ms).

-  If entering the room fails, the result parameter will be a negative number (result < 0), indicating the failure [Error Code](https://cloud.tencent.com/document/product/647/32257).

<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >param</td>

<td rowspan="1" colSpan="1" >Room entry parameters are used to specify the user's identity, role, and security token information. For details, please refer to [TRTCParams](https://write.woa.com/document/87030132707430400).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >scene</td>

<td rowspan="1" colSpan="1" >Application scenario parameters are used to specify your business scenario. All users in the same room need to set the same [TRTCAppScene](https://write.woa.com/document/87030132707430400).</td>
</tr>
</table>


> **Note**
> 

> 1. All users in the same room need to set the same scene. Different scenes can occasionally lead to anomalies.
> 

> 2. When you set the parameter scene to [TRTCAppSceneLIVE](https://write.woa.com/document/87030132707430400) or [TRTCAppSceneVoiceChatRoom](https://write.woa.com/document/87030132707430400), you must use the "role" field in [TRTCParams](https://write.woa.com/document/87030132707430400) to set the role of the current user in the room.
> 

> 3. Please ensure that [enterRoom](https://write.woa.com/document/87030026264555520) and [exitRoom](https://write.woa.com/document/87030026264555520) are paired before and after use, i.e., ensure "exit the previous room before entering the next room," otherwise, many anomalies may occur.
> 


## exitRoom



#### Leave Room

Calling this interface will make the user leave the audio and video room they are in and release resources such as the camera, microphone, and speaker.

After the resources are fully released, the SDK will notify you via the [ITRTCCloudCallback](https://write.woa.com/document/87030021158866944) in the [onExitRoom](https://write.woa.com/document/87030021158866944) callback.



If you want to call [enterRoom](https://write.woa.com/document/87030026264555520) again or switch to another provider's SDK, it is recommended to wait for the [onExitRoom](https://write.woa.com/document/87030021158866944) callback before performing subsequent operations to avoid camera or microphone occupation issues.

## switchRole



#### Switch Role

This interface allows users to switch between the roles of `Anchor` and `Audience`.



Since video streaming and voice chat rooms need to support up to 100,000 viewers simultaneously, the rule is set that **only anchors can publish their audio and video**. Therefore, if some audience members wish to publish their audio and video streams (to interact with the anchors), they need to switch their role to **Anchor** first.



When entering a room, you can predefine the user's role using the role field in [TRTCParams](https://write.woa.com/document/87030132707430400), or dynamically switch roles after entering the room using the switchRole interface.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >role</td>

<td rowspan="1" colSpan="1" >Role, defaults to **Anchor**.<br>- [TRTCRoleAnchor](https://write.woa.com/document/87030132707430400): Anchor, can publish their own audio and video. A maximum of 50 anchors can simultaneously publish audio and video in the same room.<br>- [TRTCRoleAudience](https://write.woa.com/document/87030132707430400): Audience, cannot publish their own audio and video streams, can only view audio and video of other anchors in the room. To publish their own audio and video, they need to switch to **Anchor** via the [switchRole](https://write.woa.com/document/87030026264555520) interface. A maximum of 100,000 audience members can be accommodated in the same room.</td>
</tr>
</table>


> **Note**
> 

> 1. This interface is only applicable to video live streaming ([TRTCAppSceneLIVE](https://write.woa.com/document/87030132707430400)) and voice chat room ([TRTCAppSceneVoiceChatRoom](https://write.woa.com/document/87030132707430400)) scenarios.
> 

> 2. If the scene specified in [enterRoom](https://write.woa.com/document/87030026264555520) is [TRTCAppSceneVideoCall](https://write.woa.com/document/87030132707430400) or [TRTCAppSceneAudioCall](https://write.woa.com/document/87030132707430400), do not call this interface.
> 


## switchRole



#### Switch Role (Supports Setting Permission Bit)

This interface allows users to switch between the roles of `Anchor` and `Audience`.



Due to video live streaming and voice chat rooms needing to support up to 100,000 viewers simultaneously, a rule has been established that "only the host can publish their own audio and video".

Therefore, when some viewers wish to publish their own audio and video streams (in order to interact with the host), they need to first switch their role to "host".

When entering a room, you can predefine the user's role using the role field in [TRTCParams](https://write.woa.com/document/87030132707430400), or dynamically switch roles after entering the room using the switchRole interface.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >privateMapKey</td>

<td rowspan="1" colSpan="1" >Permission tickets are used for permission control. When you want to restrict a specific room to allow only specific userIds to enter or upload videos, you need to use privateMapKey for permission protection.<br>-  It is recommended only for customers with high-level security requirements. For more details, please refer to [Enabling Advanced Permission Control](https://cloud.tencent.com/document/product/647/32240).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >role</td>

<td rowspan="1" colSpan="1" >Role, defaults to "Anchor":<br>- [TRTCRoleAnchor](https://write.woa.com/document/87030132707430400): Anchor, can publish their own audio and video. A maximum of 50 anchors can simultaneously publish audio and video in the same room.<br>- [TRTCRoleAudience](https://write.woa.com/document/87030132707430400): Audience cannot publish their own audio and video streams and can only watch other anchors' audio and video in the room. If you want to publish your own audio and video, you need to switch to "Anchor" through [switchRole](https://write.woa.com/document/87030026264555520). A maximum of 100,000 audience members can be accommodated in the same room.</td>
</tr>
</table>


> **Note**
> 

> 1. This interface is only applicable to video live streaming ([TRTCAppSceneLIVE](https://write.woa.com/document/87030132707430400)) and voice chat room ([TRTCAppSceneVoiceChatRoom](https://write.woa.com/document/87030132707430400)) scenarios.
> 

> 2. If the scene specified in [enterRoom](https://write.woa.com/document/87030026264555520) is [TRTCAppSceneVideoCall](https://write.woa.com/document/87030132707430400) or [TRTCAppSceneAudioCall](https://write.woa.com/document/87030132707430400), do not call this interface.
> 


## switchRoom



#### Switch Room

This interface allows users to quickly switch from one room to another.
-  If the user's role is "Audience", the effect of calling this interface is equivalent to exitRoom (current room) + enterRoom (new room).

-  If the user's role is "Anchor", this interface will maintain the user's audio and video publishing status while switching rooms. As a result, the preview of the camera and the collection of sound will not be interrupted during the room switching process.




This interface is suitable for scenarios in online education where supervising teachers need to switch quickly between multiple rooms. In this scenario, using switchRoom can achieve better smoothness and less code volume compared to using exitRoom + enterRoom.

The result of the interface call will be notified to you through the onSwitchRoom(errCode, errMsg) callback in [ITRTCCloudCallback](https://write.woa.com/document/87030021158866944).
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >config</td>

<td rowspan="1" colSpan="1" >For room parameters, please refer to [TRTCSwitchRoomConfig](https://write.woa.com/document/87030132707430400).</td>
</tr>
</table>


> **Note**
> 

> Due to the need for compatibility with older SDK versions, the config parameters contain both roomId and strRoomId. The specifications for filling these parameters are particularly important, so please take note of the following:
> 

> 1. If you choose strRoomId, then roomId needs to be set to 0. If both are filled, roomId will be selected by default.
> 

> 2. All rooms must either use strRoomId or roomId consistently. Mixing both will result in unexpected bugs.
> 


## connectOtherRoom



#### Request Cross-room Communication

By default, only users within the same room can make audio and video calls. Audio and video streams in different rooms are isolated.

However, you can use this interface to publish the audio and video streams of a host in another room to your own room. At the same time, this interface will also publish your own audio and video streams to the target host's room.



In other words, you can use this interface to enable cross-room audio and video stream sharing between hosts in two different rooms, allowing audiences in each room to watch the audio and video streams of both hosts. This feature can be used to implement a PK feature between hosts.



The result of the cross-room call request will be notified to you via the [ITRTCCloudCallback](https://write.woa.com/document/87030021158866944) in the [onConnectOtherRoom](https://write.woa.com/document/87030021158866944) callback.



For example, when Host A in room "101" establishes a cross-room call with Host B in room "102" using connectOtherRoom(),
-  All users in room "101" will receive the two event callbacks onRemoteUserEnterRoom(B) and onUserVideoAvailable(B,true) for host B, meaning all users in room "101" can subscribe to host B's audio and video.

-  Users in room "102" will receive the onRemoteUserEnterRoom(A) and onUserVideoAvailable(A,true) event callbacks for Anchor A. This means users in room "102" can subscribe to Anchor A's audio and video.




![](https://qcloudimg.tencent-cloud.cn/raw/c5e6c72fc163ad5c0b6b7b00e1da55b5.png)

To consider compatibility issues with subsequent extension fields, the parameters for cross-room communication temporarily use JSON format:



**Case 1: Numeric Room Number**

If Host A in room '101' wants to connect with Host B in room '102', Host A needs to pass in the following when calling the interface: {"roomId": 102, "userId": "userB"}

Below is the sample code:
``` cpp
  Json::Value jsonObj;
  jsonObj["roomId"] = 102;
  jsonObj["userId"] = "userB";
  Json::FastWriter writer;
  std::string params = writer.write(jsonObj);
  trtc.ConnectOtherRoom(params.c_str());
```



**Case 2: String Room Number**

If you are using a string room number, be sure to replace "roomId" in the JSON with "strRoomId": {"strRoomId": "102", "userId": "userB"}

Below is the sample code:
``` cpp
  Json::Value jsonObj;
  jsonObj["strRoomId"] = "102";
  jsonObj["userId"] = "userB";
  Json::FastWriter writer;
  std::string params = writer.write(jsonObj);
  trtc.ConnectOtherRoom(params.c_str());
```
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >param</td>

<td rowspan="1" colSpan="1" >You need to pass in a JSON-formatted string argument, where roomId represents the room number in numeric format, strRoomId represents the room number in string format, and userId represents the target broadcaster's user ID.</td>
</tr>
</table>


## disconnectOtherRoom



#### Exit Cross-room Communication

The exit result will be notified to you via the [ITRTCCloudCallback](https://write.woa.com/document/87030021158866944) in the [onDisconnectOtherRoom](https://write.woa.com/document/87030021158866944) callback.

## setDefaultStreamRecvMode



#### Set Subscription Mode (Needs to be set before entering the room to take effect)

You can switch between "auto-subscribe" and "manual subscribe" modes via this interface:
-  Automatic Subscription: Default mode where users receive audio and video streams from the room immediately after entering. Audio plays automatically and video starts decoding automatically (you still need to bind the rendering control through the [startRemoteView](https://write.woa.com/document/87030026264555520) interface).

-  Manual subscription: After the user enters the room, they need to manually call the [startRemoteView](https://write.woa.com/document/87030026264555520) interface to start the subscription and decoding of the video stream. They need to manually call the [muteRemoteAudio](https://write.woa.com/document/87030026264555520)(false) interface to start the playback of the sound.




In most scenarios, users entering a room will subscribe to all the audio and video streams from the broadcasters within that room. Therefore, TRTC defaults to an automatic subscription mode to achieve the best "instant start experience".

If your application scenario involves many audio and video streams being published in each room and each user only wants to selectively subscribe to 1-2 of them, it is recommended to use the "manual subscription" mode to save on bandwidth costs.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >autoRecvAudio</td>

<td rowspan="1" colSpan="1" >true: Automatically subscribe to audio; false: You need to manually call muteRemoteAudio(false) to subscribe to audio. Default value: true.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >autoRecvVideo</td>

<td rowspan="1" colSpan="1" >true: Automatically subscribe to video; false: You need to manually call startRemoteView to subscribe to video. Default value: true.</td>
</tr>
</table>


> **Note**
> 

> 1. This setting needs to be called before entering the room to take effect.
> 

> 2. In automatic subscription mode, if the user does not call [startRemoteView](https://write.woa.com/document/87030026264555520) to subscribe to the video stream after entering the room, the SDK will automatically stop subscribing to the video stream to save traffic.
> 


## createSubCloud



#### Create Sub-room Instances (For Multi-room Concurrent Viewing)

TRTCCloud was initially designed as a Singleton Pattern, limiting the ability to watch multiple rooms concurrently.

By calling this interface, you can create multiple TRTCCloud instances to watch audio and video streams from multiple rooms simultaneously.



However, please note that the ability to publish audio and video streams across multiple TRTCCloud instances is subject to certain restrictions.



This feature is primarily used in a business scenario called "super small class" in online education settings, aimed at addressing the limitation that "each TRTC room can only have up to 50 people broadcasting their audio and video streams simultaneously".



Below is the sample code:
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

> **Note**
> 
> -  The same user can enter multiple rooms with different roomIds using the same userId.
> -  Two different terminal devices cannot use the same userId to enter the same roomId simultaneously.
> -  You can set [ITRTCCloudCallback](https://write.woa.com/document/87030021158866944) for different instances to get their respective event notifications.
> -  The same user can stream on multiple TRTCCloud instances and call interfaces related to local audio and video in sub-instances. However, please note:
> -  The audio for multiple instances must be either microphone capture or custom data collection, and invoking interfaces related to audio devices will be based on the last call
> -  Calls related to the camera will take the last one as definitive: [startLocalPreview](https://write.woa.com/document/87030026264555520).


#### Return value description:

Sub TRTCCloud instances

## destroySubCloud



#### Terminate Sub-room Instances
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >subCloud</td>

<td rowspan="1" colSpan="1" >Sub-room instances</td>
</tr>
</table>


## updateOtherRoomForwardMode



#### Modify the uplink capability of cross-room broadcasters in this room

Usually, after calling the connectOtherRoom interface to conduct cross-room communication with another room's broadcaster, all viewers in this room will receive the audio and video stream published by that broadcaster.

You can call this interface to restrict the uplink capability of a cross-room broadcaster in this room, either forbidding or allowing them to publish audio/main video/auxiliary video. This action will affect all users in the room.

After disabling certain uplink capabilities of the cross-room broadcaster, all users in this room will not be able to receive the corresponding audio and video streams, nor will they be able to subscribe to them.



It should be noted that this interface can only be called by the broadcaster conducting cross-room communication, and the restrictions set through this interface will reset if the cross-room communication is interrupted or the corresponding broadcaster exits the room.



The result of calling this interface will be notified to you via the [ITRTCCloudCallback](https://write.woa.com/document/87030021158866944) in the [onUpdateOtherRoomForwardMode](https://write.woa.com/document/87030021158866944) callback.



For example:

In room "101", there is Host A and Audience B, while in room "102", there is Host C, who is normally publishing audio and video streams. Host A establishes a cross-room call with Host C using connectOtherRoom().
-  At this time, both Anchor A and Viewer B will receive the onRemoteUserEnterRoom(C), onUserVideoAvailable(C,true), and onUserAudioAvailable(C,true) event callbacks for Anchor C and can subscribe to Anchor C's audio and video.




Later, Host A calls this interface to disable Host C's ability to publish audio in the current room.
-  After that, Anchor C's audio stream cannot be published to room "101." Anchor A and Viewer B will receive the onUserAudioAvailable(C,false) event callback and can no longer subscribe to Anchor C's audio through muteRemoteAudio(C,false).

-  Host C's video stream will not be affected. Other audience members in room "102" are also unaffected and can normally subscribe to Host C's audio.




To consider compatibility issues with subsequent extension fields, the parameters for this interface temporarily use JSON format. The example is as follows:

**Case 1: Numeric Room Number**
``` cpp
{
  "roomId":102,
  "userId":"userC",
  "muteAudio":false,
  "muteVideo":true,
  "muteSubStream":false
}
```



**Case 2: String Room Number**
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
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >param</td>

<td rowspan="1" colSpan="1" >You need to pass in a JSON-formatted string argument where roomId represents the room number in numeric format, strRoomId represents the room number in string format, userId represents the target broadcaster's user ID. The options muteAudio, muteVideo, and muteSubStream denote whether to disable or allow the cross-room broadcaster to publish audio, main stream video, and sub-stream video respectively.</td>
</tr>
</table>


## startPublishMediaStream



#### Start publishing media stream

This interface sends an instruction to the TRTC server to relay/transcode the current user's audio and video streams to the Live CDN or push them back into the TRTC room. You can specify the publishing mode through [TRTCPublishTarget](https://write.woa.com/document/87030132707430400) configuration and [TRTCPublishMode](https://write.woa.com/document/87030132707430400)
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >config</td>

<td rowspan="1" colSpan="1" >Media stream transcoding configuration parameters. Refer to [TRTCStreamMixingConfig](https://write.woa.com/document/87030132707430400) for detailed configuration. This is required when transcoding and pushing back to the TRTC room. You need to specify your desired transcoding configuration parameters. It is invalid in relay mode.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >params</td>

<td rowspan="1" colSpan="1" >Media stream encoding output parameters. Refer to [TRTCStreamEncoderParam](https://write.woa.com/document/87030132707430400) for detailed configuration. This is required when transcoding and pushing back to the TRTC room. You need to specify your desired transcoding output parameters. For better relay stability and CDN compatibility, it is also recommended to configure this during relay.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >target</td>

<td rowspan="1" colSpan="1" >The target address for media stream publishing. Refer to [TRTCPublishTarget](https://write.woa.com/document/87030132707430400) for detailed configuration. Supports relay/transcoding to Tencent or third-party CDNs, and also supports transcoding pushback to the TRTC room.</td>
</tr>
</table>


> **Note**
> 

> 1. The SDK will provide the task identifier (taskId) for the backend startup through the callback [onStartPublishMediaStream](https://write.woa.com/document/87030021158866944).
> 

> 2. The same task (both TRTCPublishMode and TRTCPublishCdnUrl are identical) can only be started once. If you need to update or stop this task later, you must record and use the returned taskId to operate through [updatePublishMediaStream](https://write.woa.com/document/87030026264555520) or [stopPublishMediaStream](https://write.woa.com/document/87030026264555520).
> 

> 3. The target supports configuring multiple CDN URLs simultaneously (up to 10). If the same relay/transcoding task needs to be published to multiple CDNs, you only need to configure multiple CDN URLs in the target. Even if there are multiple relay addresses for the same transcoding task, only one transcoding fee will be charged.
> 

> 4. When using, do not push multiple tasks to the same URL addresses simultaneously to avoid abnormal streaming status. A recommended scheme is to use "sdkappid_roomid_userid_main" in the URL as a distinguishing identifier. This naming convention is easy to recognize and will not cause conflicts in your multiple applications.
> 


## updatePublishMediaStream



#### Update the published media stream.

This interface will send directives to the TRTC server to update the media stream started by [startPublishMediaStream](https://write.woa.com/document/87030026264555520)
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >config</td>

<td rowspan="1" colSpan="1" >Media stream transcoding configuration parameters. Refer to [TRTCStreamMixingConfig](https://write.woa.com/document/87030132707430400) for detailed configuration. This is required when transcoding and pushing back to the TRTC room. You need to specify your desired transcoding configuration parameters. It is invalid in relay mode.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >params</td>

<td rowspan="1" colSpan="1" >Media stream encoding output parameters. Refer to [TRTCStreamEncoderParam](https://write.woa.com/document/87030132707430400) for detailed configuration. This is required when transcoding and pushing back to the TRTC room. You need to specify your desired transcoding output parameters. For better relay stability and CDN compatibility, it is also recommended to configure this during relay.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >target</td>

<td rowspan="1" colSpan="1" >The target address for media stream publishing. Refer to [TRTCPublishTarget](https://write.woa.com/document/87030132707430400) for detailed configuration. Supports relay/transcoding to Tencent or third-party CDNs, and also supports transcoding pushback to the TRTC room.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >taskId</td>

<td rowspan="1" colSpan="1" >It will provide you with the task identifier (i.e., taskId) for the background start task through the [onStartPublishMediaStream](https://write.woa.com/document/87030021158866944) callback</td>
</tr>
</table>


> **Note**
> 

> 1. You can use this interface to update the published CDN URL (supports add and delete, up to 10 at the same time), but ensure you do not push multiple tasks to the same URL addresses simultaneously to avoid abnormal streaming status.
> 

> 2. You can update or adjust relay/transcoding tasks using taskId. For example, in PK business, you can initiate relay through [startPublishMediaStream](https://write.woa.com/document/87030026264555520) first, then use taskId and this interface to update the relay to a transcoding task when the anchor initiates PK. At this time, CDN playback will be continuous and without stream disconnection (you need to keep the media stream encoding output parameters consistent).
> 

> 3. The same task does not support switching between Audio Only, Audio and Video, and Pure Video.
> 


## stopPublishMediaStream



#### Stop publishing media stream.

This interface will send directives to the TRTC server to stop the media stream started by [startPublishMediaStream](https://write.woa.com/document/87030026264555520)
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >taskId</td>

<td rowspan="1" colSpan="1" >It will provide you with the task identifier (i.e., taskId) for the background start task through the [onStartPublishMediaStream](https://write.woa.com/document/87030021158866944) callback</td>
</tr>
</table>


> **Note**
> 

> 1. If your business backend has not saved the taskId, after your host re-enters the room following an abnormal exit, you can call [startPublishMediaStream](https://write.woa.com/document/87030026264555520) again to start the task. TRTC backend will return a task start failure and provide you with the taskId from the last attempt
> 

> 2. If the taskId is an empty string, all media streams started by [startPublishMediaStream](https://write.woa.com/document/87030026264555520) for that user will stop. If you have only started one media stream or want to stop all media streams you started, this method is recommended.
> 


## startLocalPreview



#### Enable the preview screen of the local camera (Mobile Terminal)

Call this function before enterRoom. The SDK will only enable the camera and wait until you call enterRoom to start streaming.

After calling this function after enterRoom, the SDK will enable the Camera and automatically start Video Push Streaming. When the first frame of the camera image starts to render, you will receive the onCameraDidReady callback notification from [ITRTCCloudCallback](https://write.woa.com/document/87030021158866944).
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >frontCamera</td>

<td rowspan="1" colSpan="1" >true: Front-facing camera; false: Rear-facing camera.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >view</td>

<td rowspan="1" colSpan="1" >Control carrying the video screen.</td>
</tr>
</table>


> **Note**
> 

> If you wish to preview the camera screen and use BeautyManager to adjust the beauty parameters before streaming, you can:
> 
> -  Option 1: Call startLocalPreview before enterRoom.
> -  Option 2: Call startLocalPreview + muteLocalVideo(true) after enterRoom.


## startLocalPreview



#### Enable the preview screen of the local camera (Desktop Terminal)

Before calling this interface, you can call setCurrentCameraDevice to choose between the Mac's built-in camera or an external camera.

Call this function before enterRoom. The SDK will only enable the camera and wait until you call enterRoom to start streaming.

Call this function after enterRoom. The SDK will enable the camera and automatically begin video streaming.

When the first frame of the camera image starts to render, you will receive the onCameraDidReady callback notification from TRTCCloudDelegate.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >view</td>

<td rowspan="1" colSpan="1" >Control carrying the video screen.</td>
</tr>
</table>


> **Note**
> 

> If you wish to preview the camera screen and use BeautyManager to adjust the beauty parameters before streaming, you can:
> 
> -  Option 1: Call startLocalPreview before enterRoom.
> -  Option 2: Call startLocalPreview + muteLocalVideo(true) after enterRoom.


## updateLocalView



#### Update the preview screen of the local camera

## stopLocalPreview



#### Stop camera preview

## muteLocalVideo



#### Suspend/Resume publishing local video stream

This interface can suspend (or recover) the publishing of local video screens. After suspension, other users in the same room will not be able to see your screen.

This interface is equivalent to start/stopLocalPreview when specifying TRTCVideoStreamTypeBig, but has better response speed.

Because start/stopLocalPreview requires turning on and off the camera, and turning on and off the camera is a hardware-related operation, which is very time-consuming.

In comparison, muteLocalVideo only needs to suspend or pass the data stream at the software layer. Therefore, it is more efficient and more suitable for scenarios requiring frequent openings and closings.



When suspending/recovering the publishing of the specified TRTCVideoStreamTypeBig, other users in the same room will receive the onUserVideoAvailable callback notification.

When suspending/recovering the publishing of the specified TRTCVideoStreamTypeSub, other users in the same room will receive the onUserSubStreamAvailable callback notification.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >mute</td>

<td rowspan="1" colSpan="1" >true: pause; false: resume.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >streamType</td>

<td rowspan="1" colSpan="1" >The video stream type to be suspended/recovered (only supports [TRTCVideoStreamTypeBig](https://write.woa.com/document/87030132707430400) and [TRTCVideoStreamTypeSub](https://write.woa.com/document/87030132707430400)).</td>
</tr>
</table>


## setVideoMuteImage



#### Set the alternative image during the suspension of the local screen

When you call muteLocalVideo(true) to pause the local video, you can set a placeholder image through this interface. After setting, other users in the room will see this placeholder image instead of a black screen.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >fps</td>

<td rowspan="1" colSpan="1" >Set the frame rate for the alternative image, with a minimum value of 5 and a maximum value of 10. The default is 5.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >image</td>

<td rowspan="1" colSpan="1" >Set the alternative image. A null value means no video stream data will be sent after muteLocalVideo. The default is null.</td>
</tr>
</table>


## startRemoteView



#### Subscribe to the video stream of a remote user and bind the video rendering control

By calling this API, the SDK can pull the video stream of the specified user ID and render it on the rendering control specified by the parameter view. You can set the display mode of the screen through [setRemoteRenderParams](https://write.woa.com/document/87030026264555520).
-  If you already know the user ID of a user who has a video stream in the room, you can directly call startRemoteView to subscribe to that user's video feed.

-  If you do not know which users in the room are publishing video, you can wait for a notification from [onUserVideoAvailable](https://write.woa.com/document/87030021158866944) after entering the room.




Calling this API only starts pulling the video stream, at this point the screen still needs to load and buffer. When buffering is complete, you will receive a notification from [onFirstVideoFrame](https://write.woa.com/document/87030021158866944).
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >streamType</td>

<td rowspan="1" colSpan="1" >Specify the type of video stream of the user you want to watch.<br>-  High-definition main stream: [TRTCVideoStreamTypeBig](https://write.woa.com/document/87030132707430400).<br>-  Low-quality small screen: [TRTCVideoStreamTypeSmall](https://write.woa.com/document/87030132707430400) (effective only after the remote user enables Dual-channel encoding through [enableSmallVideoStream](https://write.woa.com/document/87030026264555520)).<br>-  Substream (commonly used for screen sharing): [TRTCVideoStreamTypeSub](https://write.woa.com/document/87030132707430400).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >Specify the remote user's ID.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >view</td>

<td rowspan="1" colSpan="1" >Rendering control used to display the video screen.</td>
</tr>
</table>


> **Note**
> 

> Note a few rules:
> 

> 1. The SDK supports watching the main stream and substream of a certain user ID simultaneously, or watching the substream and small stream of a certain user ID simultaneously, but does not support watching the main stream and small stream simultaneously.
> 

> 2. Only when the specified userid enables Dual-channel encoding through [enableSmallVideoStream](https://write.woa.com/document/87030026264555520) can you watch the user's small screen.
> 

> 3. When the small stream of the specified user ID does not exist, the SDK will default to the user's main stream.
> 


## updateRemoteView



#### Update the video rendering control of a remote user

This interface can be used to update the rendering control of a remote video image and is commonly used in scenarios that involve switching display areas.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >streamType</td>

<td rowspan="1" colSpan="1" >To set the stream type of the preview window (only supports [TRTCVideoStreamTypeBig](https://write.woa.com/document/87030132707430400) and [TRTCVideoStreamTypeSub](https://write.woa.com/document/87030132707430400)).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >Specify the remote user's ID.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >view</td>

<td rowspan="1" colSpan="1" >Control carrying the video screen.</td>
</tr>
</table>


## stopRemoteView



#### Unsubscribe from the remote user's video stream and release the rendering control

Calling this interface will make the SDK stop receiving the video stream of the user and release the decoding and rendering resources of that video stream.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >streamType</td>

<td rowspan="1" colSpan="1" >Specify the type of video stream of the user you want to watch.<br>-  High-definition main stream: [TRTCVideoStreamTypeBig](https://write.woa.com/document/87030132707430400).<br>-  Low-definition small picture: [TRTCVideoStreamTypeSmall](https://write.woa.com/document/87030132707430400).<br>-  Substream (commonly used for screen sharing): [TRTCVideoStreamTypeSub](https://write.woa.com/document/87030132707430400).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >Specify the remote user's ID.</td>
</tr>
</table>


## stopAllRemoteView



#### Unsubscribe from all remote users' video streams and release all rendering resources

Calling this interface will make the SDK stop receiving all remote video streams and release all decoding and rendering resources.

> **Note**
> 

> If there is a currently displayed substream (screen sharing), it will also be stopped.
> 


## muteRemoteVideoStream



#### Suspend/Resume subscription of the remote user's video stream

This interface only pauses/resumes receiving the video stream of a designated user but does not release the display resources. The video image will be frozen on the last frame at the time of the interface call.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >mute</td>

<td rowspan="1" colSpan="1" >Pause receiving or not.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >streamType</td>

<td rowspan="1" colSpan="1" >The video stream type to be paused/resumed.<br>-  High-definition main stream: [TRTCVideoStreamTypeBig](https://write.woa.com/document/87030132707430400).<br>-  Low-definition small picture: [TRTCVideoStreamTypeSmall](https://write.woa.com/document/87030132707430400).<br>-  Substream (commonly used for screen sharing): [TRTCVideoStreamTypeSub](https://write.woa.com/document/87030132707430400).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >Specify the remote user's ID.</td>
</tr>
</table>


> **Note**
> 

> This interface supports calling before entering the room ([enterRoom](https://write.woa.com/document/87030026264555520)), and the paused state will be reset after leaving the room ([exitRoom](https://write.woa.com/document/87030026264555520)).
> 

> After calling this interface to pause receiving a specified user's video stream, calling only the [startRemoteView](https://write.woa.com/document/87030026264555520) interface will not play the specified user's video. You need to call [muteRemoteVideoStream](https://write.woa.com/document/87030026264555520)(false) or [muteAllRemoteVideoStreams](https://write.woa.com/document/87030026264555520)(false) to recover.
> 


## muteAllRemoteVideoStreams



#### Suspend/Resume subscription of all remote users' video streams

This interface only pauses/resumes receiving all users' video streams but does not release the display resources. The video image will be frozen on the last frame at the time of the interface call.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >mute</td>

<td rowspan="1" colSpan="1" >Pause receiving or not.</td>
</tr>
</table>


> **Note**
> 

> This interface supports calling before entering the room ([enterRoom](https://write.woa.com/document/87030026264555520)), and the paused state will be reset after leaving the room ([exitRoom](https://write.woa.com/document/87030026264555520)).
> 

> After calling this interface to pause receiving all users' video streams, calling only the [startRemoteView](https://write.woa.com/document/87030026264555520) interface will not play a specified user's video. You need to call [muteRemoteVideoStream](https://write.woa.com/document/87030026264555520)(false) or [muteAllRemoteVideoStreams](https://write.woa.com/document/87030026264555520)(false) to recover.
> 


## setVideoEncoderParam



#### Set encoding parameters for the video encoder

This setting determines the screen quality seen by remote users, and also affects the screen quality of the recorded video file on the cloud.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >param</td>

<td rowspan="1" colSpan="1" >Used to set the video encoder parameters. For details, see [TRTCVideoEncParam](https://write.woa.com/document/87030132707430400).</td>
</tr>
</table>


> **Note**
> 

> Starting from version v11.5, the encoding output resolution will align with width 8 height 2 bytes, and it will be adjusted downwards; eg: input resolution 540x960, actual encoding output resolution 536x960.
> 


## setNetworkQosParam



#### Set network quality control parameters

This setting determines the quality control strategy under poor network conditions, such as "Quality Priority" or "Smoothness Priority" strategies.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >param</td>

<td rowspan="1" colSpan="1" >Used to set the network quality control parameters. For details, see [TRTCNetworkQosParam](https://write.woa.com/document/87030132707430400).</td>
</tr>
</table>


## setLocalRenderParams



#### Set rendering parameters for the local screen

Configurable parameters include: rotation angle, fill mode, and left-right mirroring of the picture.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >params</td>

<td rowspan="1" colSpan="1" >Picture render parameters, see [TRTCRenderParams](https://write.woa.com/document/87030132707430400) for details.</td>
</tr>
</table>


## setRemoteRenderParams



#### Set rendering mode for the remote screen

Configurable parameters include: rotation angle, fill mode, and left-right mirroring of the picture.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >params</td>

<td rowspan="1" colSpan="1" >Picture render parameters, see [TRTCRenderParams](https://write.woa.com/document/87030132707430400) for details.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >streamType</td>

<td rowspan="1" colSpan="1" >It can be set as the main road picture ([TRTCVideoStreamTypeBig](https://write.woa.com/document/87030132707430400)) or auxiliary road picture ([TRTCVideoStreamTypeSub](https://write.woa.com/document/87030132707430400)).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >Specify the remote user's ID.</td>
</tr>
</table>


## enableSmallVideoStream



#### Enable picture-in-picture dual-stream encoding mode

After enabling the dual-stream encoding mode, the current user's encoder will output both [HD large screen] and [low-definition small picture] video streams (but only one audio stream).

This way, other users in the room can choose to subscribe to [HD large screen] or [low-definition small screen] based on their network conditions or screen size.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enable</td>

<td rowspan="1" colSpan="1" >Whether to enable small picture encoding, default value: false.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >smallVideoEncParam</td>

<td rowspan="1" colSpan="1" >Video parameters for the substream.</td>
</tr>
</table>


> **Note**
> 

> When the dual-stream encoding mode is enabled, it consumes more CPU and network bandwidth. Therefore, it may be considered for use on Mac, Windows, or high-performance Pads. It is not recommended for mobile devices.
> 


#### Return value description:

0: Success; -1: The current main screen has been set to lower quality, making dual-channel encoding unnecessary.

## setRemoteVideoStreamType



#### Switch picture-in-picture for the specified remote user

After a host in the room has enabled dual-channel encoding, the default screen subscribed by other users in the room through [startRemoteView](https://write.woa.com/document/87030026264555520) will be [HD large screen].

You can use this interface to select whether you want to subscribe to the large screen or small screen. This interface is effective whether called before or after [startRemoteView](https://write.woa.com/document/87030026264555520).
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >streamType</td>

<td rowspan="1" colSpan="1" >Video stream type, i.e., choose to watch the large screen or the small screen, default is large screen.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >Specify the remote user's ID.</td>
</tr>
</table>


> **Note**
> 

> This feature requires the target user to have already enabled Dual-channel encoding mode in advance through [enableSmallVideoStream](https://write.woa.com/document/87030026264555520), otherwise, this call will have no actual effect.
> 


## snapshotVideo



#### Take a video screenshot

You can use this interface to capture the local video footage, the main stream picture of a remote user, and the auxiliary stream (screen sharing) picture of a remote user.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >sourceType</td>

<td rowspan="1" colSpan="1" >Source of the picture can be chosen as captured video stream ([TRTCSnapshotSourceTypeStream](https://write.woa.com/document/87030132707430400)), video rendering picture ([TRTCSnapshotSourceTypeView](https://write.woa.com/document/87030132707430400)), or captured picture ([TRTCSnapshotSourceTypeCapture](https://write.woa.com/document/87030132707430400)). Captured picture screenshots are clearer.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >streamType</td>

<td rowspan="1" colSpan="1" >Video stream type, you can choose to capture the main stream picture ([TRTCVideoStreamTypeBig](https://write.woa.com/document/87030132707430400), commonly used for cameras) or the auxiliary stream picture ([TRTCVideoStreamTypeSub](https://write.woa.com/document/87030132707430400), commonly used for screen sharing).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >User ID, if left blank, indicates capturing the local video footage.</td>
</tr>
</table>


> **Note**
> 

> Windows platform currently only supports capturing [TRTCSnapshotSourceTypeStream](https://write.woa.com/document/87030132707430400) source video footage.
> 


## setGravitySensorAdaptiveMode



#### Set gravity sensing adaptive mode (11.7 and above)

After gravity sensing is enabled, if the collection end device rotates, both the collection end and audience side will render the image accordingly to ensure the image in the view is always upright.

It only takes effect in the SDK internal camera capture scene and only works on the mobile terminal.

1. This interface only affects the collection end. If you are just watching the image in the room, enabling this interface is ineffective

2. When the collection end device rotates 90 degrees or 270 degrees, the image seen by the collection end or audience side may be cropped to maintain aspect ratio coordination
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >mode</td>

<td rowspan="1" colSpan="1" >Gravity sensing mode. For details, see [TRTCGravitySensorAdaptiveMode_Disable](https://write.woa.com/document/87030132707430400), [TRTCGravitySensorAdaptiveMode_FillByCenterCrop](https://write.woa.com/document/87030132707430400), and [TRTCGravitySensorAdaptiveMode_FitWithBlackBorder](https://write.woa.com/document/87030132707430400). Default value: [TRTCGravitySensorAdaptiveMode_Disable](https://write.woa.com/document/87030132707430400).</td>
</tr>
</table>


## startLocalAudio



#### Enable collection and publishing of local audio

The SDK does not enable the microphone by default. When users need to publish local audio, they need to call this interface to enable microphone collection and encoding and publish the audio to the current room.

After enabling the collection and publishing of local audio, other users in the room will receive [onUserAudioAvailable](https://write.woa.com/document/87030021158866944)(userId, true) notification.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >quality</td>

<td rowspan="1" colSpan="1" >Sound quality<br>- [TRTCAudioQualitySpeech](https://write.woa.com/document/87030132707430400), Fluent: Sample rate: 16k; Mono; Audio bitrate: 16kbps; Suitable for voice call-dominated scenarios, such as online meetings and voice calls.<br>- [TRTCAudioQualityDefault](https://write.woa.com/document/87030132707430400), Default: Sample rate: 48k; Mono; Audio bitrate: 50kbps; The default audio quality of the SDK, recommended unless there are special requirements.<br>- [TRTCAudioQualityMusic](https://write.woa.com/document/87030132707430400), High Quality: Sample rate: 48k; Stereo + full band; Audio bitrate: 128kbps; Suitable for high-fidelity music transmission scenarios, such as online KTV and music live streaming.</td>
</tr>
</table>


> **Note**
> 

> This function checks the microphone permissions. If the current app does not have microphone permissions, the SDK will automatically request microphone permissions from the user.
> 


## stopLocalAudio



#### Stop collection and publishing of local audio

After stopping the collection and publishing of local audio, other users in the room will receive [onUserAudioAvailable](https://write.woa.com/document/87030021158866944)(userId, false) notification.

## muteLocalAudio



#### Pause/Resume publishing of the local audio stream

When you pause the publishing of the local audio stream, other users in the room will receive [onUserAudioAvailable](https://write.woa.com/document/87030021158866944)(userId, false) notification.

When you resume the publishing of the local audio stream, other users in the room will receive [onUserAudioAvailable](https://write.woa.com/document/87030021158866944)(userId, true) notification.



The difference from [stopLocalAudio](https://write.woa.com/document/87030026264555520) is that muteLocalAudio(true) does not release the microphone permissions but continues to send a low-bit-rate silent packet.

This is very suitable for scenarios that require cloud recording because video files in formats like MP4 demand high continuity of audio data, and using [stopLocalAudio](https://write.woa.com/document/87030026264555520) will make the recorded MP4 files difficult to play.

Therefore, in scenarios where the quality of the recorded files is highly required, it is recommended to choose muteLocalAudio instead of stopLocalAudio.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >mute</td>

<td rowspan="1" colSpan="1" >true: Mute; false: Unmute.</td>
</tr>
</table>


## muteRemoteAudio



#### Pause/Resume playing of the remote audio stream

When you mute a user's remote audio, the SDK will stop playing the specified user's sound and will also stop pulling that user's audio data.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >mute</td>

<td rowspan="1" colSpan="1" >true: Mute; false: Unmute.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >Used to specify the remote user's ID.</td>
</tr>
</table>


> **Note**
> 

> This interface is effective whether called before or after entering the room (enterRoom). The mute status will be reset to false after exiting the room (exitRoom).
> 


## muteAllRemoteAudio



#### Pause/Resume playing of all remote users' audio streams

When you mute all users' remote audio, the SDK will stop playing all remote audio streams and will also stop pulling all users' audio data.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >mute</td>

<td rowspan="1" colSpan="1" >true: Mute; false: Unmute.</td>
</tr>
</table>


> **Note**
> 

> This interface is effective whether called before or after entering the room (enterRoom). The mute status will be reset to false after exiting the room (exitRoom).
> 


## setRemoteAudioVolume



#### Set the playback volume for a specific remote user

You can mute a remote user's sound by using setRemoteAudioVolume(userId, 0).
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >Used to specify the remote user's ID.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >volume</td>

<td rowspan="1" colSpan="1" >Volume. Value range: 0-100. Default value: 100.</td>
</tr>
</table>


> **Note**
> 

> If you still feel the volume is too low after setting it to 100, you can set the maximum volume to 150. However, a volume above 100 carries a risk of pop noise, so proceed with caution.
> 


## setAudioCaptureVolume



#### Sets the local audio capture volume.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >volume</td>

<td rowspan="1" colSpan="1" >Volume. Value range: 0-100. Default value: 100.</td>
</tr>
</table>


> **Note**
> 

> If you still feel the volume is too low after setting it to 100, you can set the maximum volume to 150. However, a volume above 100 carries a risk of pop noise, so proceed with caution.
> 


## getAudioCaptureVolume



#### Obtains the local audio capture volume.

## setAudioPlayoutVolume



#### Sets the remote audio playback volume.

This interface controls the volume that the SDK finally delivers to the system for playback. The adjustment will affect the volume of the local audio recording file, but it will not affect the volume of the ear return.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >volume</td>

<td rowspan="1" colSpan="1" >Volume. Value range: 0-100. Default value: 100.</td>
</tr>
</table>


> **Note**
> 

> If you still feel the volume is too low after setting it to 100, you can set the maximum volume to 150. However, a volume above 100 carries a risk of pop noise, so proceed with caution.
> 


## getAudioPlayoutVolume



#### Obtains the remote audio playback volume.

## enableAudioVolumeEvaluation



#### Enable volume reminder

After enabling this feature, the SDK will provide feedback on the local or remote user's audio volume assessment information, including volume level, voice detection, audio spectrum, etc., in the [ITRTCCloudCallback](https://write.woa.com/document/87030021158866944) callback [onUserVoiceVolume](https://write.woa.com/document/87030021158866944).
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enable</td>

<td rowspan="1" colSpan="1" >Whether to enable volume prompts, disabled by default.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >params</td>

<td rowspan="1" colSpan="1" >For volume assessment and other related parameters, please refer to [TRTCAudioVolumeEvaluateParams](https://write.woa.com/document/87030132707430400).</td>
</tr>
</table>


## startAudioRecording



#### Start recording

When you call this interface, the SDK will mix and record all local and remote audio (including local audio, remote audio, background music, and sound effects) into a local file.

This interface can be called both before and after entering the room. If the recording task is not stopped by stopAudioRecording before exiting the room, the task will automatically stop after exiting the room.

The start and completion status of this recording will be notified through local recording-related callbacks. See the TRTCCloud related callbacks.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >param</td>

<td rowspan="1" colSpan="1" >For recording parameters, please refer to [TRTCAudioRecordingParams](https://write.woa.com/document/87030132707430400).</td>
</tr>
</table>


> **Note**
> 

> Starting from version 11.5, the status results of audio recording are uniformly adjusted to asynchronous callback notifications. See the TRTCCloud related callbacks.
> 


#### Return value description:

0: Success; -1: Recording has already started; -2: File or directory creation failed; -3: The audio format specified by the extension is not supported.

## stopAudioRecording



#### Stop recording

If the recording task is not stopped by this interface before exiting the room, the recording task will automatically stop after exiting the room.

## startLocalRecording



#### Enable local media recording

After enabling, the audio and video content during the live stream will be recorded to a local file.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >params</td>

<td rowspan="1" colSpan="1" >For recording parameters, please refer to [TRTCLocalRecordingParams](https://write.woa.com/document/87030132707430400).</td>
</tr>
</table>


## stopLocalRecording



#### Stop local media recording

If the recording task is not stopped by this interface before exiting the room, the recording task will automatically stop after exiting the room.

## setRemoteAudioParallelParams



#### Set intelligent concurrent playback strategy for remote audio streams

Set intelligent concurrent playback strategy for remote audio streams, suitable for scenarios with a large number of people on the microphone.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >params</td>

<td rowspan="1" colSpan="1" >For audio concurrency parameters, please refer to [TRTCAudioParallelParams](https://write.woa.com/document/87030132707430400).</td>
</tr>
</table>


## enable3DSpatialAudioEffect



#### Enable 3D audio

Enable 3D audio effects. Note that smooth sound quality [TRTCAudioQualitySpeech](https://write.woa.com/document/87030132707430400) or default sound quality [TRTCAudioQualityDefault](https://write.woa.com/document/87030132707430400) should be used.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enabled</td>

<td rowspan="1" colSpan="1" >Whether to enable 3D audio effects, disabled by default.</td>
</tr>
</table>


## updateSelf3DSpatialPosition



#### Set self coordinates and orientation information in 3D audio

Update your position and orientation in the world coordinate system. The SDK will calculate the relative position between yourself and remote users based on the parameters of this method and render spatial audio effects accordingly. Note that each parameter should be passed in as an array of length 3.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >axisForward</td>

<td rowspan="1" colSpan="1" >The unit vector of the front axis of the local coordinate system in the world coordinate system, with three values representing the front, right, and up coordinate values, respectively.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >axisRight</td>

<td rowspan="1" colSpan="1" >The unit vector of the right axis of the local coordinate system in the world coordinate system, with three values representing the front, right, and up coordinate values, respectively.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >axisUp</td>

<td rowspan="1" colSpan="1" >The unit vector of the up axis of the local coordinate system in the world coordinate system, with three values representing the front, right, and up coordinate values, respectively.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >position</td>

<td rowspan="1" colSpan="1" >Your coordinate in the world coordinate system, with three values representing the front, right, and up coordinate values, respectively.</td>
</tr>
</table>


> **Note**
> 

> Please appropriately limit the invocation frequency. It is recommended to set coordinates at intervals of at least 100ms.
> 


## updateRemote3DSpatialPosition



#### Set remote user coordinate information in 3D audio

Update the position of remote users in the world coordinate system. The SDK will render spatial audio effects based on the relative position between yourself and the remote users. Note that the parameter is an array of length 3.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >position</td>

<td rowspan="1" colSpan="1" >The coordinate of the remote user in the world coordinate system, with three values representing the front, right, and up coordinate values, respectively.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >Specify the remote user's ID.</td>
</tr>
</table>


> **Note**
> 

> Please appropriately limit the invocation frequency. It is recommended to set coordinates for the same remote user at intervals of at least 100ms.
> 


## set3DSpatialReceivingRange



#### Set the receivable range of sounds emitted by a specified user

After setting this range size, the specified user's voice will be audible within this range, and any sound beyond this range will be attenuated to 0.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >range</td>

<td rowspan="1" colSpan="1" >Maximum range at which the sound can be received.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >Specify the remote user's ID.</td>
</tr>
</table>


## getDeviceManager



#### Get Device Management Class (TXDeviceManager)

## setBeautyStyle



#### Set special effects like beauty filter, whitening, and rosy skin

The SDK integrates two different skin smoothing algorithms:

-"Smooth": This algorithm is more aggressive, providing a more noticeable smoothing effect, suitable for show live streaming.

-"Natural": This algorithm retains more facial details, offering a more natural smoothing effect, suitable for most live streaming scenarios.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >beautyLevel</td>

<td rowspan="1" colSpan="1" >Beauty level, value range 0 - 9, 0 means disabled, the greater the value from 1 - 9, the more obvious the effect.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ruddinessLevel</td>

<td rowspan="1" colSpan="1" >Rosy level, value range 0 - 9, 0 means disabled, the greater the value from 1 - 9, the more obvious the effect.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >style</td>

<td rowspan="1" colSpan="1" >Skin smoothing algorithm, available in two types: "Smooth" and "Natural".</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >whitenessLevel</td>

<td rowspan="1" colSpan="1" >Whitening level, value range 0 - 9, 0 means disabled, the greater the value from 1 - 9, the more obvious the effect.</td>
</tr>
</table>


## setWaterMark



#### Watermarking

The watermark position is specified by xOffset, yOffset, and fWidthRatio.
-  xOffset: The watermark's coordinate in the range of 0 - 1 as a floating point number.

-  yOffset: The watermark's coordinate in the range of 0 - 1 as a floating point number.

-  fWidthRatio: The watermark's size ratio in the range of 0 - 1 as a floating point number.

<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >fWidthRatio</td>

<td rowspan="1" colSpan="1" >The width of the watermark displayed as a proportion of the screen width (the watermark is proportionally scaled according to this parameter).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >isVisibleOnLocalPreview</td>

<td rowspan="1" colSpan="1" >true: Watermark displayed in local preview; false: Watermark not displayed in local preview, effective only on win/mac.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >nHeight</td>

<td rowspan="1" colSpan="1" >Watermark image pixel height (ignored if source data is file path).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >nWidth</td>

<td rowspan="1" colSpan="1" >Watermark image pixel width (ignored if source data is file path).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >srcData</td>

<td rowspan="1" colSpan="1" >Watermark image source data (set to nullptr to remove watermark).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >srcType</td>

<td rowspan="1" colSpan="1" >Watermark image source data type.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >streamType</td>

<td rowspan="1" colSpan="1" >Stream type to apply the watermark (TRTCVideoStreamTypeBig, TRTCVideoStreamTypeSub).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >xOffset</td>

<td rowspan="1" colSpan="1" >X-axis offset for the top-left corner of watermark display.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >yOffset</td>

<td rowspan="1" colSpan="1" >Y-axis offset for the top-left corner of watermark display.</td>
</tr>
</table>


> **Note**
> 

> This interface only supports adding image watermarks to the main video stream.
> 


## getAudioEffectManager



#### Get Audio Effect Management Class (TXAudioEffectManager)

TXAudioEffectManager is the audio effect management interface. Through this interface, you can implement the following features:
-  Background Music: Supports online and local music, variable speed, pitch shift, and other special effects. Supports native and accompaniment playback as well as loop playback.

-  In-ear monitor feedback: The microphone captures the sound and plays it in real-time through the earphones, commonly used in music live streaming.

-  Reverb Effect: KTV, small room, hall, deep, resonant....

-  Voice changing effect: Lolita, uncle, heavy metal....

-  Short sound effects: short sound effect files such as applause, laughter, etc. (for files less than 10 seconds, please set the isShortFile parameter to true).


## startSystemAudioLoopback



#### Enable System Sound Capture (iOS not yet supported)

This interface captures audio data from the computer's sound card and mixes it into the current audio data stream of the SDK, so that other users in the room can also hear the sound played by the broadcaster's computer.

In online education scenarios, teachers can use this feature to allow the SDK to capture the audio from educational videos and broadcast it to students in the same room.

In music live streaming scenarios, the host can use this feature to allow the SDK to capture audio from the music player to add background music to their live stream.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >deviceName</td>

<td rowspan="1" colSpan="1" >You can set this parameter to nullptr, indicating the SDK captures the entire system sound.</td>
</tr>
</table>


> **Note**
> 

> On the Windows platform, you can also set the parameter deviceName to the absolute path of an application executable (e.g., QQMusic.exe). In this case, the SDK will capture only the application's sound (supports 32-bit SDK, and 64-bit SDK requires Windows version 10.0.19042 or higher).
> 

> You can also set the parameter to a specific speaker device name to capture sound from that speaker (get the speaker devices of type [TXMediaDeviceTypeSpeaker](https://write.woa.com/document/87030115247763456) from the TXDeviceManager's getDevicesList interface).
> 

> On the Windows platform, you can also set this parameter to a process id (format as "process_xxx", where xxx is the process id). The SDK will capture the sound from that process (requires Windows version 10.0.19042 or higher).
> 

> On the Windows platform, you can also set this parameter as a process ID (format as "exclude_process_xxx", where xxx is the process ID). In this case, the SDK will capture all audio except for the specified process (requires Windows version 10.0.19042 or higher).
> 


## stopSystemAudioLoopback



#### Stop System Sound Capture (iOS not yet supported)

## setSystemAudioLoopbackVolume



#### Sets the Volume of System Sound Capture
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >volume</td>

<td rowspan="1" colSpan="1" >Set the volume level, range: [0 ~ 150], default value is 100.</td>
</tr>
</table>


## startScreenCapture



#### Start Screen Sharing

This interface can capture the entire screen content or the content of a specific application window you designate, sharing it with other users in the same room.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >encParam</td>

<td rowspan="1" colSpan="1" >Screen Sharing Encoding Parameters: The SDK prioritizes the encoding parameters you set through this interface<br>-  If you set encParam to null and have set substream video encoding parameters through setSubStreamEncoderParam, the SDK will use those parameters for screen sharing.<br>-  If you set encParam to null and have not set substream video encoding parameters through setSubStreamEncoderParam, the SDK will automatically select the best encoding parameters for screen sharing.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >streamType</td>

<td rowspan="1" colSpan="1" >The circuit used for screen sharing can be set to Main Road (TRTCVideoStreamTypeBig) or Auxiliary Road (TRTCVideoStreamTypeSub), with the auxiliary road being recommended.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >view</td>

<td rowspan="1" colSpan="1" >The parent control of the rendering control can be set to null, indicating that the preview effect of screen sharing will not be displayed.</td>
</tr>
</table>


> **Note**
> 

> 1. The same user can publish only one main road ([TRTCVideoStreamTypeBig](https://write.woa.com/document/87030132707430400)) screen and one auxiliary road ([TRTCVideoStreamTypeSub](https://write.woa.com/document/87030132707430400)) screen at the same time.
> 

> 2. By default, screen sharing uses the auxiliary road. If you use the main road for screen sharing, you need to stop local preview ([stopLocalPreview](https://write.woa.com/document/87030026264555520)) in advance to avoid conflicts.
> 

> 3. Only one user can use the auxiliary road for screen sharing in the same room at any given time. In other words, only one user can enable the auxiliary road in the same room simultaneously.
> 

> 4. If another user in the room is already sharing the screen using an auxiliary road, calling this interface will receive an onError(ERR_SERVER_CENTER_ANOTHER_USER_PUSH_SUB_VIDEO) callback from [ITRTCCloudCallback](https://write.woa.com/document/87030021158866944).
> 


## stopScreenCapture



#### Stopping Screen Sharing

## pauseScreenCapture



#### Pause Screen Sharing

> **Note**
> 

> Starting from version 11.5, suspending screen capture will output the last frame at a frame rate of 1fps.
> 


## resumeScreenCapture



#### Resume Screen Sharing

## getScreenCaptureSources



#### Enumerate shareable screens and windows (this interface supports only desktop systems)

When integrating the screen sharing feature on a desktop system, it is usually necessary to display an interface for selecting a sharing target. This allows users to choose whether to share the entire screen or a specific window.

Through this interface, you can query the current system for the ID, name, and thumbnail of available windows for sharing. We provide a default interface implementation in our Demo for your reference.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >iconSize</td>

<td rowspan="1" colSpan="1" >Specify the size of the window icon to be retrieved.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >thumbnailSize</td>

<td rowspan="1" colSpan="1" >Specify the size of the window thumbnail to be retrieved. Thumbnails can be used to render on the window selection interface.</td>
</tr>
</table>


> **Note**
> 

> 1. The returned list includes screens and application windows, with the screen being the first element in the list. If the user has multiple monitors, each monitor is a sharing target.
> 

> 2. Do not use delete ITRTCScreenCaptureSourceList* to remove SourceList as it is prone to cause crashes. Use the release method in ITRTCScreenCaptureSourceList to release the list.
> 


#### Return value description:

The window list includes the screen.

## selectScreenCaptureTarget



#### Select the screen or window to share (this interface supports only desktop systems)

After you retrieve the shareable screens and windows using getScreenCaptureSources, you can call this interface to select the desired target screen or window for sharing.

During screen sharing, you can also call this interface at any time to switch the sharing target.



Supports the following four cases:
-  Share the entire screen: The type in sourceInfoList is Screen, and captureRect is set to { 0, 0, 0, 0 }

-  Share a specified area: The type in sourceInfoList is Screen, and captureRect is set to a non-nullptr, for example, { 100, 100, 300, 300 }

-  Share the entire window: The type in sourceInfoList is Window, and captureRect is set to { 0, 0, 0, 0 }

-  Share a window area: The type in sourceInfoList is Window, and captureRect is set to a non-nullptr, for example, { 100, 100, 300, 300 }

<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >captureRect</td>

<td rowspan="1" colSpan="1" >Specify the capture area</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >property</td>

<td rowspan="1" colSpan="1" >Specify the properties of the screen sharing target, including capturing the mouse, highlighting the capture window, etc. For details, refer to the TRTCScreenCaptureProperty Definition</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >source</td>

<td rowspan="1" colSpan="1" >Specifying sharing source</td>
</tr>
</table>


> **Note**
> 

> Setting highlight border color and width parameter is not effective on Mac platform.
> 


## setSubStreamEncoderParam



#### Set Video Encoding Parameters for Screen Sharing (Sub-Stream) (Supported on Both Desktop and Mobile Systems)

This interface can set the screen sharing (sub-stream) quality seen by remote users, and also determine the screen sharing quality in the cloud-recorded video file.

Please note the differences between the following two interfaces:
- [setVideoEncoderParam](https://write.woa.com/document/87030026264555520) is used to set the video encoding parameters for the main stream ([TRTCVideoStreamTypeBig](https://write.woa.com/document/87030132707430400), usually for the camera).

- [setSubStreamEncoderParam](https://write.woa.com/document/87030026264555520) is used to set the video encoding parameters for the auxiliary stream ([TRTCVideoStreamTypeSub](https://write.woa.com/document/87030132707430400), usually for screen sharing).

<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >param</td>

<td rowspan="1" colSpan="1" >For auxiliary stream encoding parameters, please refer to [TRTCVideoEncParam](https://write.woa.com/document/87030132707430400).</td>
</tr>
</table>


## setSubStreamMixVolume



#### Set the Mixing Volume for Screen Sharing (This Interface Supports Only Desktop Systems)

The higher this value, the higher the proportion of screen sharing volume, and the lower the proportion of microphone volume. Therefore, it is not recommended to set it too high, as it will suppress the microphone sound.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >volume</td>

<td rowspan="1" colSpan="1" >Set the mix volume level, ranging from 0 to 100.</td>
</tr>
</table>


## addExcludedShareWindow



#### Add the Specified Window to the Exclusion List of Screen Sharing (This Interface Supports Only Desktop Systems)

Windows added to the exclusion list will not be shared. A common use case is to add a window from an application to the exclusion list to avoid privacy issues.

Support setting filter windows before starting screen sharing, and also dynamically adding filter windows during screen sharing.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >windowID</td>

<td rowspan="1" colSpan="1" >Windows that you do not want to share</td>
</tr>
</table>


> **Note**
> 

> 1. This interface only takes effect when the type in [TRTCScreenCaptureSourceInfo](https://write.woa.com/document/87030132707430400) is specified as [TRTCScreenCaptureSourceTypeScreen](https://write.woa.com/document/87030132707430400), meaning the exclusion feature only works when sharing the entire screen content.
> 

> 2. Windows added to the exclusion list using this interface will be automatically cleared by the SDK upon exiting the room.
> 

> 3. On Mac platform, please pass in the window ID (i.e., CGWindowID), which can be obtained from the sourceId member in [TRTCScreenCaptureSourceInfo](https://write.woa.com/document/87030132707430400).
> 


## removeExcludedShareWindow



#### Remove the Specified Window from the Exclusion List of Screen Sharing (This Interface Supports Only Desktop Systems)
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >windowID</td>

<td rowspan="1" colSpan="1" >The window ID to be excluded.</td>
</tr>
</table>


## removeAllExcludedShareWindow



#### Remove All Windows from the Exclusion List of Screen Sharing (This Interface Supports Only Desktop Systems)

## addIncludedShareWindow



#### Add the Specified Window to the Contains List of Screen Sharing (This Interface Supports Only Desktop Systems)

This interface only takes effect when the type in [TRTCScreenCaptureSourceInfo](https://write.woa.com/document/87030132707430400) is specified as [TRTCScreenCaptureSourceTypeWindow](https://write.woa.com/document/87030132707430400). This means that the feature of including an additional specified window is only effective when sharing window content.

You can call it both before and after [startScreenCapture](https://write.woa.com/document/87030026264555520).
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >windowID</td>

<td rowspan="1" colSpan="1" >Windows desired to be shared (Window Handle: HWND on Windows platform)</td>
</tr>
</table>


> **Note**
> 

> Windows added to the inclusion list through this method will be automatically cleared by the SDK upon exiting the room.
> 


## removeIncludedShareWindow



#### Remove the Specified Window from the Contains List of Screen Sharing (This Interface Supports Only Desktop Systems)

This interface only takes effect when the type in [TRTCScreenCaptureSourceInfo](https://write.woa.com/document/87030132707430400) is specified as [TRTCScreenCaptureSourceTypeWindow](https://write.woa.com/document/87030132707430400).

This means that the feature of including an additional specified window is only effective when sharing window content.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >windowID</td>

<td rowspan="1" colSpan="1" >Windows desired to be shared (Window ID on Mac platform; HWND on Windows platform)</td>
</tr>
</table>


## removeAllIncludedShareWindow



#### Remove All Windows from the Contains List of Screen Sharing (This Interface Supports Only Desktop Systems)

This interface only takes effect when the type in [TRTCScreenCaptureSourceInfo](https://write.woa.com/document/87030132707430400) is specified as [TRTCScreenCaptureSourceTypeWindow](https://write.woa.com/document/87030132707430400).

This means that the feature of including an additional specified window is only effective when sharing window content.

## enableCustomVideoCapture



#### Enable/Disable Custom Video Capturing Mode

After enabling this mode, the SDK will stop running the original video capture process. It will no longer collect data from the camera and apply beauty filters, retaining only video encoding and sending capabilities.

You need to continuously send self-collected video frames to the SDK via [sendCustomVideoData](https://write.woa.com/document/87030026264555520).
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enable</td>

<td rowspan="1" colSpan="1" >Whether to enable, default value: false.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >streamType</td>

<td rowspan="1" colSpan="1" >Used to specify the video stream type, [TRTCVideoStreamTypeBig](https://write.woa.com/document/87030132707430400): High-definition main stream; [TRTCVideoStreamTypeSub](https://write.woa.com/document/87030132707430400): Auxiliary stream.</td>
</tr>
</table>


## sendCustomVideoData



#### Submit Self-collected Video Frames to the SDK

This interface allows you to submit self-collected video frames to the SDK. The SDK will encode the video frames and transmit them through its network module.



Parameter [TRTCVideoFrame](https://write.woa.com/document/87030132707430400) is recommended to be filled as follows (other fields do not need to be filled):
-  pixelFormat: Windows and Android platforms only support [TRTCVideoPixelFormat_I420](https://write.woa.com/document/87030132707430400); iOS and Mac platforms support [TRTCVideoPixelFormat_I420](https://write.woa.com/document/87030132707430400) and [TRTCVideoPixelFormat_BGRA32](https://write.woa.com/document/87030132707430400).

-  bufferType: Recommended choice is [TRTCVideoBufferType_Buffer](https://write.woa.com/document/87030132707430400).

-  data: Buffer used to carry video frame data.

-  length: Video frame data length. If pixelFormat is set to I420 format, length can be calculated as follows: length = width × height × 3 / 2.

-  width: Video image width, such as 640 px.

-  height: Video image height, such as 480 px.

-  timestamp: Timestamp, in milliseconds (ms). Please use the timestamp recorded when the video frame is captured (you can get the timestamp by calling [generateCustomPTS](https://write.woa.com/document/87030026264555520) after capturing a video frame).




Refer to documentation: [Custom Collection and Rendering](https://cloud.tencent.com/document/product/647/34066).
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >frame</td>

<td rowspan="1" colSpan="1" >Video data, supports I420 format data.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >streamType</td>

<td rowspan="1" colSpan="1" >Used to specify the video stream type,[TRTCVideoStreamTypeBig](https://write.woa.com/document/87030132707430400): HD large screen;[TRTCVideoStreamTypeSub](https://write.woa.com/document/87030132707430400): Auxiliary stream.</td>
</tr>
</table>


> **Note**
> 

> 1. It is recommended to call the [generateCustomPTS](https://write.woa.com/document/87030026264555520) interface to get the timestamp value of the frame after capturing a video frame, to achieve the best audio-video synchronization.
> 

> 2. The final frame rate of the encoded video by the SDK is determined by the FPS you set in [setVideoEncoderParam](https://write.woa.com/document/87030026264555520), not by the frequency at which you call this interface.
> 

> 3. Please try to keep the intervals between calls to this interface uniform. Otherwise, it may cause unstable encoder output frame rates or audio-video asynchrony.
> 

> 4. iOS and Mac platforms currently support video frames in [TRTCVideoPixelFormat_I420](https://write.woa.com/document/87030132707430400) or [TRTCVideoPixelFormat_BGRA32](https://write.woa.com/document/87030132707430400) format.
> 

> 5. Windows and Android platforms currently support video frames in [TRTCVideoPixelFormat_I420](https://write.woa.com/document/87030132707430400) format only.
> 


## enableCustomAudioCapture



#### Enable Custom Audio Capturing Mode

After enabling this mode, the SDK will no longer run the original audio capture process, meaning it will stop capturing audio data from the microphone and only retain audio encoding and sending capabilities.

You need to continuously feed the SDK with your own collected audio data through [sendCustomAudioData](https://write.woa.com/document/87030026264555520).
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enable</td>

<td rowspan="1" colSpan="1" >Whether to enable, default value: false.</td>
</tr>
</table>


> **Note**
> 

> As Echo Cancellation (AEC) requires strict control over the timing of audio capture and playback, enabling custom audio capture may result in AEC capabilities becoming ineffective.
> 


## sendCustomAudioData



#### Submit Self-collected Audio Data to the SDK

Parameter [TRTCAudioFrame](https://write.woa.com/document/87030132707430400) is recommended to be filled as follows (other fields do not need to be filled):
-  audioFormat: Audio data format, only supports TRTCAudioFrameFormatPCM.

-  data: Audio frame buffer. Audio frame data only supports PCM format, with frame lengths ranging from [5ms ~ 100ms]. A frame length of 20ms is recommended. Calculation method: [48000 sampling rate, mono channel frame length: 48000 × 0.02s × 1 × 16bit = 15360bit = 1920 bytes].

-  sampleRate: Sampling rate, supported values are 16000, 24000, 32000, 44100, 48000.

-  channel: Number of channels (if stereo, data is interleaved), mono: 1; stereo: 2.

-  timestamp: Timestamp, in milliseconds (ms). Please use the timestamp recorded when the audio frame is captured (you can get the timestamp by calling [generateCustomPTS](https://write.woa.com/document/87030026264555520) after capturing an audio frame).




Refer to documentation: [Custom Collection and Rendering](https://cloud.tencent.com/document/product/647/74692).
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >frame</td>

<td rowspan="1" colSpan="1" >Audio Data</td>
</tr>
</table>


> **Note**
> 

> Please call this interface accurately at intervals corresponding to the duration of each frame. Feeding data at uneven intervals is likely to cause audio stutter.
> 


## enableMixExternalAudioFrame



#### Enable/Disable Custom Audio Track

Once enabled, you can use this interface to mix a Custom Audio Track into the SDK. With two boolean parameters, you can control whether the track should play remotely and locally.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enablePlayout</td>

<td rowspan="1" colSpan="1" >Control whether the mixed audio track should be played locally. Default value: false.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enablePublish</td>

<td rowspan="1" colSpan="1" >Control whether the mixed audio track should be played remotely. Default value: false.</td>
</tr>
</table>


> **Note**
> 

> If you set both enablePublish and enablePlayout parameters to false, it means you completely disable your custom audio track.
> 


## mixExternalAudioFrame



#### Mix Custom Audio Track into the SDK

Before calling this interface, you need to enable the Custom Audio Track with [enableMixExternalAudioFrame](https://write.woa.com/document/87030026264555520) first. After that, you can use this interface to mix your own audio track into the SDK in PCM format.

Ideally, we expect your code to provide track data to the SDK at a very consistent rate. However, we understand that maintaining perfect call intervals is a significant challenge.

Therefore, the SDK will initiate a buffer for audio track data internally. This buffer acts like a "reservoir", capable of temporarily storing the audio track data you input, smoothing out the jitter caused by intervals between interface calls.

The return value of this interface represents the size of this track buffer zone, measured in milliseconds (ms). For example: if this interface returns 50, it means the current track buffer zone has 50ms worth of track data. Therefore, as long as you call this interface again within 50ms, the SDK can ensure the continuity of your mixed track data.

When you call this interface, if you find the return value > 100ms, you can wait for one frame of audio playback time before calling again; if the return value < 100ms, it means the buffer is relatively small, you can mix in some more audio track data to ensure the size of the audio track buffer remains above the "safe level".



Parameter [TRTCAudioFrame](https://write.woa.com/document/87030132707430400) is recommended to be filled as follows (other fields do not need to be filled):
-  data: Audio frame buffer. Audio frame data only supports PCM format, with frame lengths ranging from [5ms ~ 100ms]. A frame length of 20ms is recommended. Calculation method: [48000 sampling rate, mono channel frame length: 48000 × 0.02s × 1 × 16bit = 15360bit = 1920 bytes].

-  sampleRate: Sampling rate, supported values are 16000, 24000, 32000, 44100, 48000.

-  channel: Number of channels (if stereo, data is interleaved), mono: 1; stereo: 2.

-  timestamp: Timestamp, in milliseconds (ms). Please use the timestamp recorded when the audio frame is captured (you can get the timestamp by calling [generateCustomPTS](https://write.woa.com/document/87030026264555520) after capturing an audio frame).

<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >frame</td>

<td rowspan="1" colSpan="1" >Audio Data</td>
</tr>
</table>


> **Note**
> 

> Please call this interface accurately at intervals corresponding to the duration of each frame. Feeding data at uneven intervals is likely to cause audio stutter.
> 


#### Return value description:

>= 0 Buffered length, unit: ms. < 0 Error (-1 mixExternalAudioFrame not enabled)

## setMixExternalAudioVolume



#### Set the Streaming Volume and Playback Volume for External Audio Mixed During Streaming
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >playoutVolume</td>

<td rowspan="1" colSpan="1" >Set the playback volume level, ranging from 0 to 100. -1 means no change.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >publishVolume</td>

<td rowspan="1" colSpan="1" >Set the streaming volume level, ranging from 0 to 100. -1 means no change.</td>
</tr>
</table>


## generateCustomPTS



#### Generate Timestamp for Custom Capturing

This interface is only applicable to custom capturing mode, used to solve the issue of audio and video out of sync caused by the discrepancy between capture time and delivery time.



When you use interfaces such as [sendCustomVideoData](https://write.woa.com/document/87030026264555520) or [sendCustomAudioData](https://write.woa.com/document/87030026264555520) for custom video or audio capturing, please follow these steps to use this interface:

1. First, when capturing a video or audio frame, call this interface to obtain the PTS timestamp of that moment.

2. Then, you can send the video or audio frame to the preprocessing module you use (such as third-party beauty components or third-party audio effect components).

3. When actually calling [sendCustomVideoData](https://write.woa.com/document/87030026264555520) or [sendCustomAudioData](https://write.woa.com/document/87030026264555520) for streaming, please assign the PTS timestamp recorded during capture to the timestamp field in [TRTCVideoFrame](https://write.woa.com/document/87030132707430400) or [TRTCAudioFrame](https://write.woa.com/document/87030132707430400).

#### Return value description:

Timestamp (unit: ms)

## enableLocalVideoCustomProcess



#### .1 Enable third-party beauty filter for video

Once enabled, you can use [ITRTCVideoFrameCallback](https://write.woa.com/document/87030021158866944) to obtain image frames of specified pixel format and video data structure type.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >bufferType</td>

<td rowspan="1" colSpan="1" >Specifying video data structure type.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enable</td>

<td rowspan="1" colSpan="1" >Enable third-party video beautification, disabled by default.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >pixelFormat</td>

<td rowspan="1" colSpan="1" >Specify the pixel format for the callback.</td>
</tr>
</table>


#### Return value description:

0: Success; <0: Error

## setLocalVideoCustomProcessCallback



#### .2 Set video data callback for third-party beauty filter

After setting this callback, the SDK will output the collected video frames through the callback you set for secondary processing by third-party beauty filter components. The SDK will then encode and send the processed video frames.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >callback</td>

<td rowspan="1" colSpan="1" >Custom beauty filter callback. See [ITRTCVideoFrameCallback](https://write.woa.com/document/87030021158866944).</td>
</tr>
</table>


## setLocalVideoRenderCallback



#### Set Local Video Custom Rendering Callback

After setting this callback, the SDK will skip the original rendering process and return the captured data. You need to handle the rendering yourself.
-  You can stop the callback by calling setLocalVideoRenderCallback(TRTCVideoPixelFormat_Unknown, TRTCVideoBufferType_Unknown, nullptr).

-  iOS, Mac, and Windows platforms currently support video frames in [TRTCVideoPixelFormat_I420](https://write.woa.com/document/87030132707430400) or [TRTCVideoPixelFormat_BGRA32](https://write.woa.com/document/87030132707430400) pixel formats.

-  Android platform currently supports video frames in [TRTCVideoPixelFormat_I420](https://write.woa.com/document/87030132707430400), [TRTCVideoPixelFormat_RGBA32](https://write.woa.com/document/87030132707430400), or [TRTCVideoPixelFormat_Texture_2D](https://write.woa.com/document/87030132707430400) pixel formats.

<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >bufferType</td>

<td rowspan="1" colSpan="1" >Specifying video data structure type</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >callback</td>

<td rowspan="1" colSpan="1" >Set Definition Rendering Callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >pixelFormat</td>

<td rowspan="1" colSpan="1" >Specify the pixel format for callback</td>
</tr>
</table>


#### Return value description:

0: Success; <0: Error

## setRemoteVideoRenderCallback



#### Sets the rendering callback for remote video self-definition

After setting this callback, the SDK will skip the original rendering process and return the captured data. You need to handle the rendering yourself.
-  You can stop the callback by calling setRemoteVideoRenderCallback(TRTCVideoPixelFormat_Unknown, TRTCVideoBufferType_Unknown, nullptr).

-  iOS, Mac, and Windows platforms currently support video frames in [TRTCVideoPixelFormat_I420](https://write.woa.com/document/87030132707430400) or [TRTCVideoPixelFormat_BGRA32](https://write.woa.com/document/87030132707430400) pixel formats.

-  Android platform currently supports video frames in [TRTCVideoPixelFormat_I420](https://write.woa.com/document/87030132707430400), [TRTCVideoPixelFormat_RGBA32](https://write.woa.com/document/87030132707430400), or [TRTCVideoPixelFormat_Texture_2D](https://write.woa.com/document/87030132707430400) pixel formats.

<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >bufferType</td>

<td rowspan="1" colSpan="1" >Specifying video data structure type, currently only supports [TRTCVideoBufferType_Buffer](https://write.woa.com/document/87030132707430400)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >callback</td>

<td rowspan="1" colSpan="1" >Set Definition Rendering Callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >pixelFormat</td>

<td rowspan="1" colSpan="1" >Specify the pixel format for callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >Remote user ID</td>
</tr>
</table>


> **Note**
> 

> In actual use, you need to call startRemoteView(userid, nullptr) to get the remote user's video stream (set view to nullptr), otherwise, no data will be called back.
> 


#### Return value description:

0: Success; <0: Error

## setAudioFrameCallback



#### Sets the audio data self-definition callback

After setting this callback, the SDK will internally callback the audio data (PCM format), including:
- [onCapturedAudioFrame](https://write.woa.com/document/87030021158866944): Audio data callback captured by the local microphone

- [onLocalProcessedAudioFrame](https://write.woa.com/document/87030021158866944): Audio data callback captured locally and preprocessed by the audio module

- [onPlayAudioFrame](https://write.woa.com/document/87030021158866944): Audio data of each remote user before mixing

- [onMixedPlayAudioFrame](https://write.woa.com/document/87030021158866944): Audio data callback after mixing various audio streams and finally to be played by the system


> **Note**
> 

> Setting the callback to null means stopping the Definition audio callback; vice versa, setting the callback to non-null means starting the Definition audio callback.
> 


## setCapturedAudioFrameCallbackFormat



#### Sets the callback format for audio frames captured by the local microphone

This interface is used to set the format of the AudioFrame callback for [onCapturedAudioFrame](https://write.woa.com/document/87030021158866944):
-  sampleRate: Sampling rate, supported values are 16000, 32000, 44100, 48000.

-  channel: Number of channels (if stereo, data is interleaved), mono: 1; stereo: 2.

-  samplesPerCall: Number of sampling points, Definition callback data frame length. The frame length must be an integer multiple of 10ms.




If you want to calculate the callback frame length in milliseconds, the formula to convert milliseconds to sampling points is: sampling points = milliseconds * sampling rate / 1000.

Example: For a 48000 sampling rate and a desired callback frame length of 20ms, the number of sampling points should be: 960 = 20 * 48000 / 1000.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >format</td>

<td rowspan="1" colSpan="1" >Audio Data Callback Format.</td>
</tr>
</table>


> **Note**
> 

> The final callback frame length is in bytes. The formula to convert sampling points to bytes is: Byte Count = Sampling Points * Channels * 2 (Bit Width). Example: For a 48000 sampling rate, stereo, and 20ms frame length, the number of sampling points is 960, and the byte count is 3840 = 960 * 2 * 2
> 


#### Return value description:

0: Success; <0: Error

## setLocalProcessedAudioFrameCallbackFormat



#### Sets the callback format for local audio frames after preprocessing

This interface is used to set the format of the AudioFrame callback for [onLocalProcessedAudioFrame](https://write.woa.com/document/87030021158866944):
-  sampleRate: Sampling rate, supported values are 16000, 32000, 44100, 48000.

-  channel: Number of channels (if stereo, data is interleaved), mono: 1; stereo: 2.

-  samplesPerCall: Number of sampling points, Definition callback data frame length. The frame length must be an integer multiple of 10ms.




If you want to calculate the callback frame length in milliseconds, the formula to convert milliseconds to sampling points is: sampling points = milliseconds * sampling rate / 1000.

Example: For a 48000 sampling rate and a desired callback frame length of 20ms, the number of sampling points should be: 960 = 20 * 48000 / 1000.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >format</td>

<td rowspan="1" colSpan="1" >Audio Data Callback Format.</td>
</tr>
</table>


> **Note**
> 

> The final callback frame length is in bytes. The formula to convert sampling points to bytes is: Byte Count = Sampling Points * Channels * 2 (Bit Width). Example: For a 48000 sampling rate, stereo, and 20ms frame length, the number of sampling points is 960, and the byte count is 3840 = 960 * 2 * 2
> 


#### Return value description:

0: Success; <0: Error

## setMixedPlayAudioFrameCallbackFormat



#### Sets the callback format for audio frames that will eventually be played by the system

This interface is used to set the format of the AudioFrame callback for [onMixedPlayAudioFrame](https://write.woa.com/document/87030021158866944):
-  sampleRate: Sampling rate, supported values are 16000, 32000, 44100, 48000.

-  channel: Number of channels (if stereo, data is interleaved), mono: 1; stereo: 2.

-  samplesPerCall: Number of sampling points, Definition callback data frame length. The frame length must be an integer multiple of 10ms.




If you want to calculate the callback frame length in milliseconds, the formula to convert milliseconds to sampling points is: sampling points = milliseconds * sampling rate / 1000.

Example: For a 48000 sampling rate and a desired callback frame length of 20ms, the number of sampling points should be: 960 = 20 * 48000 / 1000.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >format</td>

<td rowspan="1" colSpan="1" >Audio Data Callback Format.</td>
</tr>
</table>


> **Note**
> 

> The final callback frame length is in bytes. The formula to convert sampling points to bytes is: Byte Count = Sampling Points * Channels * 2 (Bit Width). Example: For a 48000 sampling rate, stereo, and 20ms frame length, the number of sampling points is 960, and the byte count is 3840 = 960 * 2 * 2
> 


#### Return value description:

0: Success; <0: Error

## enableCustomAudioRendering



#### Enable self-definition audio playback

If you need to connect specific audio devices or want to control the audio playback logic yourself, you can enable Custom Playback through this interface.

After enabling Custom Playback, the SDK will no longer use the system's audio interface to play data. You need to get the audio frame that the SDK wants to play through [getCustomAudioRenderingFrame](https://write.woa.com/document/87030026264555520) and play it yourself.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enable</td>

<td rowspan="1" colSpan="1" >Whether to enable Custom Playback is off by default.</td>
</tr>
</table>


> **Note**
> 

> You need to set it before entering the room for it to take effect. It is not supported to set it after entering the room.
> 


## getCustomAudioRenderingFrame



#### Get playable audio data

Before calling this interface, you need to enable Custom Playback through [enableCustomAudioRendering](https://write.woa.com/document/87030026264555520) first.



Parameter [TRTCAudioFrame](https://write.woa.com/document/87030132707430400) is recommended to be filled as follows (other fields do not need to be filled):
-  sampleRate: Sampling rate, required, supported values are 16000, 24000, 32000, 44100, 48000.

-  channel: Number of channels, required. Fill in 1 for mono, 2 for stereo. The data is interleaved for stereo.

-  data: Buffer for obtaining audio data. You need to allocate the memory size of data according to the frame length of an audio frame. The obtained PCM data supports frame lengths of 10ms or 20ms. It is recommended to use a frame length of 20ms.




Calculation formula: Sampling rate x Playback duration x Number of channels x 2 (bytes per sample). For example, for a frame of audio with a sampling rate of 48000, mono channel, and a playback duration of 20ms, the buffer size is 48000 × 0.02s × 1 × 16bit = 15360bit = 1920 bytes.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >audioFrame</td>

<td rowspan="1" colSpan="1" >Audio data frame.</td>
</tr>
</table>


> **Note**
> 

> 1. Parameters sampleRate and channel in audioFrame should be set in advance, and the data space required for the frame length to be read should be allocated.
> 

> 2. The SDK will automatically fill the data according to sampleRate and channel.
> 

> 3. It is recommended to call this function driven by the system's audio playback thread. After playing one frame of audio, call this API to get the next playable frame of audio data.
> 


## sendCustomCmdMsg



#### Sends a custom message using UDP channel to all users in a room

This interface allows you to use TRTC's UDP Channel to broadcast custom data to other users in the room, achieving the purpose of transmitting signaling.

Other users in the room can receive messages through the onRecvCustomCmdMsg callback in [ITRTCCloudCallback](https://write.woa.com/document/87030021158866944).
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >cmdID</td>

<td rowspan="1" colSpan="1" >Message ID, the value range is 1 - 10.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >data</td>

<td rowspan="1" colSpan="1" >Message to be sent, the maximum length of a single message is limited to 1KB.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ordered</td>

<td rowspan="1" colSpan="1" >Whether orderly sending is enabled, i.e., whether the order of data packets at the receiver matches the order at the sender (this will cause some reception delay).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >reliable</td>

<td rowspan="1" colSpan="1" >Whether reliable transmission is enabled. Reliable transmission offers a higher success rate but will cause higher reception delays compared to unreliable transmission.</td>
</tr>
</table>


> **Note**
> 

> 1. Sending messages to all users in the room (currently not supporting Web/Mini program end), up to 30 messages per second.
> 

> 2. Each data packet can be up to 1KB. If it exceeds this size, it is very likely to be discarded by intermediate routers or servers.
> 

> 3. Each client can send up to 8 KB of data per second.
> 

> Please set both reliable and ordered to true or both to false. Interleaved settings are not supported.
> 

> 5. It is strongly recommended to set different types of messages with different cmdIDs. This can reduce message latency when ordering is required.
> 

> 6. Currently, only anchor roles are supported.
> 


#### Return value description:

true: Message has been sent; false: Message sending failed.

## sendSEIMsg



#### Sends a custom message using SEI channel to all users in a room

This interface allows you to broadcast self-defined data to other users in the current room using TRTC's SEI channel to achieve signaling transmission.



There is a header data block called SEI in the video frame header. The principle of this interface is to use this SEI header data block to embed the self-defined signaling you want to send, so it is sent out along with the video frame.

Therefore, compared to [sendCustomCmdMsg](https://write.woa.com/document/87030026264555520), signaling transmitted via the SEI channel has better compatibility: the signaling can be transmitted along with the video frame all the way to the live CDN.

However, because the data block in the video frame header cannot be too large, it is recommended to control the signaling size to just a few bytes when using this interface.



The most common usage is to embed a self-defined timestamp (timestamp) into the video frame using this interface to achieve perfect alignment of messages and screen (e.g., in educational scenarios for aligning courseware and video signals).

Other users in the room can receive messages through the onRecvSEIMsg callback in [ITRTCCloudCallback](https://write.woa.com/document/87030021158866944).
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >data</td>

<td rowspan="1" colSpan="1" >Data to be sent, which can contain up to 1 KB (1,000 bytes) of data</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >repeatCount</td>

<td rowspan="1" colSpan="1" >Number of data sends</td>
</tr>
</table>


> **Note**
> 

> This interface has the following limitations:
> 

> 1. Data will not be sent immediately after the API invocation, but will be sent along with the next video frame.
> 

> 2. Send messages to all users in the room, up to 30 messages per second (shared limit with sendCustomCmdMsg).
> 

> 3. Each package is a maximum of 1 KB. Sending large amounts of data will increase the video bitrate and possibly cause reduced image quality or lag (shared limit with sendCustomCmdMsg).
> 

> 4. Each client can send up to 8 KB of data per second (shared limit with sendCustomCmdMsg).
> 

> 5. If multiple sends are specified (repeatCount > 1), the data will be sent with the subsequent repeatCount number of video frames, which will also increase the video bitrate.
> 

> 6. If repeatCount > 1 and there are multiple sends, the onRecvSEIMsg callback may receive the same message multiple times, and deduplication is needed.
> 


#### Return value description:

true: Message has passed the restriction, waiting for subsequent video frame to be sent; false: Message is restricted from being sent

## startSpeedTest



#### Start internet speed test (use before entering the room)
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >params</td>

<td rowspan="1" colSpan="1" >Speed Test Options</td>
</tr>
</table>


> **Note**
> 

> 1. The speed test process will incur a small basic service fee. For details, refer to [Billing Overview > Basic Service](https://cloud.tencent.com/document/product/647/17157#.E5.9F.BA.E7.A1.80.E6.9C.8D.E5.8A.A1) documentation.
> 

> 2. Please perform the internet speed test before entering the room. Conducting the test in the room will affect normal audio and video transmission and will also be inaccurate due to too much interference.
> 

> 3. Only one internet speed test task is allowed to run at the same time.
> 


#### Return value description:

API Invocation Result, < 0: Failure

## stopSpeedTest



#### Stops network speed testing

## getSDKVersion



#### Obtains the SDK version.

## setLogLevel



#### Sets the log output level.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >level</td>

<td rowspan="1" colSpan="1" >Refer to [TRTCLogLevel](https://write.woa.com/document/87030132707430400), default value: [TRTCLogLevelNone](https://write.woa.com/document/87030132707430400)</td>
</tr>
</table>


## setConsoleEnabled



#### Enables/Disables console log print.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enabled</td>

<td rowspan="1" colSpan="1" >Specify whether to enable it. Default: Disabled.</td>
</tr>
</table>


## setLogCompressEnabled



#### Enables/Disables local log compression

After enabling compression, the log storage volume is significantly reduced, but you need to use a Python script provided by Tencent Cloud to decompress and read it.

After disabling compression, logs are stored in plaintext, which can be opened and read directly with Notepad but occupy more space.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enabled</td>

<td rowspan="1" colSpan="1" >Specify whether to enable it. Default: Enabled</td>
</tr>
</table>


## setLogDirPath



#### Sets the save path for local logs

This interface allows you to change the default storage path of SDK local logs. The default local log storage locations are:
-  Windows platform: C:/Users/[system username]/AppData/Roaming/liteav/log, i.e., %appdata%/liteav/log.

-  iOS or Mac platform: sandbox Documents/log.

-  Android platform: /app private directory/files/log/liteav/.

<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >path</td>

<td rowspan="1" colSpan="1" >Storage path for logs</td>
</tr>
</table>


> **Note**
> 

> Make sure to call this before all other interfaces and ensure that the specified directory exists and that your application has read and write permissions for that directory.
> 


## setLogCallback



#### Log callback

## showDebugView



#### Show Dashboard

The "Dashboard" is a semi-transparent debug information overlay located above the video rendering control, used to display audio and video information and event information, aiding in integration and debugging.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >showType</td>

<td rowspan="1" colSpan="1" >0: Do not display; 1: Display simplified edition (audio and video information only); 2: Display full version (including audio and video information and event information).</td>
</tr>
</table>


## callExperimentalAPI



#### Calls an experimental API.

## enablePayloadPrivateEncryption



#### Enable or disable media stream private encryption

In scenarios with high security requirements, TRTC recommends calling the enablePayloadPrivateEncryption method to enable media stream private encryption before joining a room.

After the user leaves the room, the SDK will automatically disable private encryption. If you need to re-enable private encryption, you must call this method before the user rejoins the room.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >config</td>

<td rowspan="1" colSpan="1" >For configuring the media stream private encryption algorithm and key, refer to [TRTCPayloadPrivateEncryptionConfig](https://write.woa.com/document/87030132707430400).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enabled</td>

<td rowspan="1" colSpan="1" >Whether to enable media stream private encryption.</td>
</tr>
</table>


> **Note**
> 

> TRTC already encrypts media streams before transmission. When media stream private encryption is enabled, it will use the key and initialization vector you provided for additional encryption.
> 


#### Return value description:

API invocation results: 0: Method call successful, -1: Invalid input parameter, -2: Feature expired. To unlock: Please visit the Chinese mainland site to activate the [TRTC Enterprise Edition Package](https://buy.cloud.tencent.com/trtc?tab=month&trtcversion=ultimate), and submit an [application](https://cloud.tencent.com/apply/p/diifjcmffhw). You can use it upon approval.