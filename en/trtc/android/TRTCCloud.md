> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

# TRTC Real-Time Communication (TRTC SDK) Documentation
## Overview
`TRTCCloud.java` is the API reference for TRTC Real-Time Communication (TRTC SDK) on Android. It provides detailed documentation for features including stream publishing, stream playback, stream mixing, and recording.

## TRTCCloud
| Function List | Description |
| --- | --- |
| sharedInstance | Create a `TRTCCloud` Instance (Singleton Pattern) |
| destroySharedInstance | Terminate `TRTCCloud` Instance (Singleton Pattern) |
| addListener | Add TRTC Event Callback |
| removeListener | Remove TRTC Event Callback |
| setListenerHandler | Set the queue to drive TRTCCloudListener event callbacks |
| enterRoom | Enter Room |
| exitRoom | Leave Room |
| switchRole | Switch Role |
| switchRole | Switch Role (Supports Setting Permission Bit) |
| switchRoom | Switch Room |
| ConnectOtherRoom | Request Cross-room Communication |
| DisconnectOtherRoom | Exit Cross-room Communication |
| setDefaultStreamRecvMode | Set Subscription Mode (Needs to be set before entering the room to take effect) |
| createSubCloud | Create Sub-room Instances (For Multi-room Concurrent Viewing) |
| destroySubCloud | Terminate Sub-room Instances |
| updateOtherRoomForwardMode | Modify the uplink capability of cross-room broadcasters in this room |
| startPublishMediaStream | Start publishing media stream |
| updatePublishMediaStream | Update the published media stream. |
| stopPublishMediaStream | Stop publishing media stream. |
| startLocalPreview | Enable the preview screen of the local camera (Mobile Terminal) |
| updateLocalView | Update the preview screen of the local camera |
| stopLocalPreview | Stop camera preview |
| muteLocalVideo | Suspend/Resume publishing local video stream |
| setVideoMuteImage | Set the alternative image during the suspension of the local screen |
| startRemoteView | Subscribe to the video stream of a remote user and bind the video rendering control |
| updateRemoteView | Update the video rendering control of a remote user |
| stopRemoteView | Unsubscribe from the remote user's video stream and release the rendering control |
| stopAllRemoteView | Unsubscribe from all remote users' video streams and release all rendering resources |
| muteRemoteVideoStream | Suspend/Resume subscription of the remote user's video stream |
| muteAllRemoteVideoStreams | Suspend/Resume subscription of all remote users' video streams |
| setVideoEncoderParam | Set encoding parameters for the video encoder |
| setNetworkQosParam | Set network quality control parameters |
| setLocalRenderParams | Set rendering parameters for the local screen |
| setRemoteRenderParams | Set rendering mode for the remote screen |
| enableEncSmallVideoStream | Enable picture-in-picture dual-stream encoding mode |
| setRemoteVideoStreamType | Switch picture-in-picture for the specified remote user |
| snapshotVideo | Take a video screenshot |
| setPerspectiveCorrectionPoints | Set perspective correction coordinate settings for the video screen |
| setGravitySensorAdaptiveMode | Set gravity sensing adaptive mode (11.7 and above) |
| startLocalAudio | Enable collection and publishing of local audio |
| stopLocalAudio | Stop collection and publishing of local audio |
| muteLocalAudio | Pause/Resume publishing of the local audio stream |
| muteRemoteAudio | Pause/Resume playing of the remote audio stream |
| muteAllRemoteAudio | Pause/Resume playing of all remote users' audio streams |
| setAudioRoute | Sets audio routing. |
| setRemoteAudioVolume | Set the playback volume for a specific remote user |
| setAudioCaptureVolume | Sets the local audio capture volume. |
| getAudioCaptureVolume | Obtains the local audio capture volume. |
| setAudioPlayoutVolume | Sets the remote audio playback volume. |
| getAudioPlayoutVolume | Obtains the remote audio playback volume. |
| enableAudioVolumeEvaluation | Enable volume reminder |
| startAudioRecording | Start recording |
| stopAudioRecording | Stop recording |
| startLocalRecording | Enable local media recording |
| stopLocalRecording | Stop local media recording |
| setRemoteAudioParallelParams | Set intelligent concurrent playback strategy for remote audio streams |
| enable3DSpatialAudioEffect | Enable 3D audio |
| updateSelf3DSpatialPosition | Set self coordinates and orientation information in 3D audio |
| updateRemote3DSpatialPosition | Set remote user coordinate information in 3D audio |
| set3DSpatialReceivingRange | Set the receivable range of sounds emitted by a specified user |
| getDeviceManager | Get Device Management Class (TXDeviceManager) |
| getBeautyManager | Get Beauty Management Class (TXBeautyManager) |
| setWatermark | Watermarking |
| getAudioEffectManager | Get Audio Effect Management Class (TXAudioEffectManager) |
| startSystemAudioLoopback | Enable System Sound Capturing |
| stopSystemAudioLoopback | Stop System Sound Capture (iOS not yet supported) |
| startScreenCapture | Start Screen Sharing |
| stopScreenCapture | Stopping Screen Sharing |
| pauseScreenCapture | Pause Screen Sharing |
| resumeScreenCapture | Resume Screen Sharing |
| setSubStreamEncoderParam | Set Video Encoding Parameters for Screen Sharing (Sub-Stream) (Supported on Both Desktop and Mobile Systems) |
| enableCustomVideoCapture | Enable/Disable Custom Video Capturing Mode |
| sendCustomVideoData | Submit Self-collected Video Frames to the SDK |
| enableCustomAudioCapture | Enable Custom Audio Capturing Mode |
| sendCustomAudioData | Submit Self-collected Audio Data to the SDK |
| enableMixExternalAudioFrame | Enable/Disable Custom Audio Track |
| mixExternalAudioFrame | Mix Custom Audio Track into the SDK |
| setMixExternalAudioVolume | Set the Streaming Volume and Playback Volume for External Audio Mixed During Streaming |
| generateCustomPTS | Generate Timestamp for Custom Capturing |
| setLocalVideoProcessListener | Set Video Data Callback for Third-party Beauty Filter |
| setLocalVideoRenderListener | Set Local Video Custom Rendering Callback |
| setRemoteVideoRenderListener | Sets the rendering callback for remote video self-definition |
| setAudioFrameListener | Sets the audio data self-definition callback |
| setCapturedAudioFrameCallbackFormat | Sets the callback format for audio frames captured by the local microphone |
| setLocalProcessedAudioFrameCallbackFormat | Sets the callback format for local audio frames after preprocessing |
| setMixedPlayAudioFrameCallbackFormat | Sets the callback format for audio frames that will eventually be played by the system |
| enableCustomAudioRendering | Enable self-definition audio playback |
| getCustomAudioRenderingFrame | Get playable audio data |
| sendCustomCmdMsg | Sends a custom message using UDP channel to all users in a room |
| sendSEIMsg | Sends a custom message using SEI channel to all users in a room |
| startSpeedTest | Start internet speed test (use before entering the room) |
| stopSpeedTest | Stops network speed testing |
| getSDKVersion | Obtains the SDK version. |
| setLogLevel | Sets the log output level. |
| setConsoleEnabled | Enables/Disables console log print. |
| setLogCompressEnabled | Enables/Disables local log compression |
| setLogDirPath | Sets the save path for local logs |
| setLogListener | Log callback |
| showDebugView | Show Dashboard |
| TRTCViewMargin | Set the dashboard margin |
| callExperimentalAPI | Calls an experimental API. |
| enablePayloadPrivateEncryption | Enable or disable media stream private encryption |

## sharedInstance

#### Create a `TRTCCloud` Instance (Singleton Pattern)
| Parameters | Description |
| --- | --- |
| context | Only applies to the Android platform. The SDK internally converts it to the Android platform's ApplicationContext to call Android System API. If the passed context parameter is NULL, the SDK will automatically obtain the current process's ApplicationContext. |

> **Note**
> 

> 1. Using delete ITRTCCloud* will cause compilation errors. Please use destroyTRTCCloud to release the object pointer.
> 

> 2. On Windows, Mac, and iOS platforms, please call the getTRTCShareInstance() interface.
> 

> 3. On the Android platform, please call the getTRTCShareInstance(void *context) interface.
> 

## destroySharedInstance

#### Terminate `TRTCCloud` Instance (Singleton Pattern)

## addListener

#### Add TRTC Event Callback

You can receive various event notifications from the SDK (such as error codes, warning codes, audio and video status parameters, etc.) through TRTCCloudListener.

## removeListener

#### Remove TRTC Event Callback

## setListenerHandler

#### Set the queue to drive TRTCCloudListener event callbacks

If you do not specify your own listenerHandler, MainQueue will be used as the default queue to drive TRTCCloudListener event callbacks.

This means that if you do not set the listenerHandler attribute, all callback functions in TRTCCloudListener are driven by MainQueue.
| Parameters | Description |
| --- | --- |
| listenerHandler | Event callback handler |

> **Note**
> 

> If you specify your own listenerHandler, please do not operate the UI in the TRTCCloudListener callback functions, otherwise it will cause thread safety issues.
> 

## enterRoom

#### Enter Room

All TRTC users must enter a room to "publish" or "subscribe" to audio and video streams. "Publish" means pushing your audio and video to the cloud, and "subscribe" means pulling audio and video streams from other users in the room from the cloud.

To call this interface, you need to specify your application scenario TRTCAppScene for the best audio and video transmission experience. These scenarios can be divided into two major categories:

**Real-time Call:**

Including the two options TRTC_APP_SCENE_VIDEOCALL and TRTC_APP_SCENE_AUDIOCALL, which are video call and voice call respectively. This mode is suitable for 1-on-1 audio and video calls or online meetings with fewer than 300 participants.

**Online Live Streaming:**

Including the two options TRTC_APP_SCENE_LIVE and TRTC_APP_SCENE_VOICE_CHATROOM, which are video live streaming and voice live streaming respectively. This mode is suitable for online live streaming scenarios with less than 100,000 participants. However, you need to specify the **role** field in the TRTCParams parameter introduced next, distinguishing users in the room as **Anchors** (TRTCRoleAnchor) and **Audience** (TRTCRoleAudience).

After calling this interface, you will receive the onEnterRoom(result) callback from TRTCCloudListener
-  If entering the room is successful, the result parameter will be a positive number (result > 0), indicating the time taken from the function call to entering the room, in milliseconds (ms).

-  If entering the room fails, the result parameter will be a negative number (result < 0), indicating the failure [Error Code](https://cloud.tencent.com/document/product/647/32257).

| Parameters | Description |
| --- | --- |
| param | Room entry parameters are used to specify the user's identity, role, and security token information. For details, please refer to TRTCParams. |
| scene | Application scenario parameters are used to specify your business scenario. All users in the same room need to set the same TRTCAppScene. |

> **Note**
> 

> 1. All users in the same room need to set the same scene. Different scenes can occasionally lead to anomalies.
> 

> 2. When you set the parameter scene to TRTC_APP_SCENE_LIVE or TRTC_APP_SCENE_VOICE_CHATROOM, you must specify the role of the current user in the room through the "role" field in TRTCParams.
> 

> 3. Please ensure that enterRoom and exitRoom are paired before and after use, i.e., ensure "exit the previous room before entering the next room," otherwise, many anomalies may occur.
> 

## exitRoom

#### Leave Room

Calling this interface will make the user leave the audio and video room they are in and release resources such as the camera, microphone, and speaker.

After the resources are released, the SDK will notify you through the TRTCCloudListener callback onExitRoom.

If you want to call enterRoom again or switch to another provider's SDK, it is recommended to wait for the onExitRoom callback before performing subsequent operations to avoid camera or microphone occupation issues.

## switchRole

#### Switch Role

This interface allows users to switch between the roles of `Anchor` and `Audience`.

Since video streaming and voice chat rooms need to support up to 100,000 viewers simultaneously, the rule is set that **only anchors can publish their audio and video**. Therefore, if some audience members wish to publish their audio and video streams (to interact with the anchors), they need to switch their role to **Anchor** first.

When entering a room, you can predefine the user's role using the role field in TRTCParams, or dynamically switch roles after entering the room using the switchRole interface.
| Parameters | Description |
| --- | --- |
| role | Role, defaults to **Anchor**. - TRTCRoleAnchor: Anchor, can publish their own audio and video. A maximum of 50 anchors can simultaneously publish audio and video in the same room. - TRTCRoleAudience: Audience, cannot publish their own audio and video streams, can only view audio and video of other anchors in the room. To publish their own audio and video, they need to switch to **Anchor** via the switchRole interface. A maximum of 100,000 audience members can be accommodated in the same room. |

> **Note**
> 

> 1. This interface is only applicable to video live streaming (TRTC_APP_SCENE_LIVE) and voice chat rooms (TRTC_APP_SCENE_VOICE_CHATROOM).
> 

> 2. If you specify the scene as TRTC_APP_SCENE_VIDEOCALL or TRTC_APP_SCENE_AUDIOCALL when calling enterRoom, do not call this interface.
> 

## switchRole

#### Switch Role (Supports Setting Permission Bit)

This interface allows users to switch between the roles of `Anchor` and `Audience`.

Due to video live streaming and voice chat rooms needing to support up to 100,000 viewers simultaneously, a rule has been established that "only the host can publish their own audio and video".

Therefore, when some viewers wish to publish their own audio and video streams (in order to interact with the host), they need to first switch their role to "host".

When entering a room, you can predefine the user's role using the role field in TRTCParams, or dynamically switch roles after entering the room using the switchRole interface.
| Parameters | Description |
| --- | --- |
| privateMapKey | Permission tickets are used for permission control. When you want to restrict a specific room to allow only specific userIds to enter or upload videos, you need to use privateMapKey for permission protection. -  It is recommended only for customers with high-level security requirements. For more details, please refer to [Enabling Advanced Permission Control](https://cloud.tencent.com/document/product/647/32240). |
| role | Role, defaults to "Anchor": - TRTCRoleAnchor: Anchor, can publish their own audio and video. A maximum of 50 anchors can simultaneously publish audio and video in the same room. - TRTCRoleAudience: Audience cannot publish their own audio and video streams and can only watch other anchors' audio and video in the room. If you want to publish your own audio and video, you need to switch to "Anchor" through switchRole. A maximum of 100,000 audience members can be accommodated in the same room. |

> **Note**
> 

> 1. This interface is only applicable to video live streaming (TRTC_APP_SCENE_LIVE) and voice chat rooms (TRTC_APP_SCENE_VOICE_CHATROOM).
> 

> 2. If you specify the scene as TRTC_APP_SCENE_VIDEOCALL or TRTC_APP_SCENE_AUDIOCALL when calling enterRoom, do not call this interface.
> 

## switchRoom

#### Switch Room

This interface allows users to quickly switch from one room to another.
-  If the user's role is "Audience", the effect of calling this interface is equivalent to exitRoom (current room) + enterRoom (new room).

-  If the user's role is "Anchor", this interface will maintain the user's audio and video publishing status while switching rooms. As a result, the preview of the camera and the collection of sound will not be interrupted during the room switching process.

This interface is suitable for scenarios in online education where supervising teachers need to switch quickly between multiple rooms. In this scenario, using switchRoom can achieve better smoothness and less code volume compared to using exitRoom + enterRoom.

The result of the interface call will be notified through the onSwitchRoom(errCode, errMsg) callback in TRTCCloudListener.
| Parameters | Description |
| --- | --- |
| config | For room parameters, please refer to TRTCSwitchRoomConfig. |

> **Note**
> 

> Due to the need for compatibility with older SDK versions, the config parameters contain both roomId and strRoomId. The specifications for filling these parameters are particularly important, so please take note of the following:
> 

> 1. If you choose strRoomId, then roomId needs to be set to 0. If both are filled, roomId will be selected by default.
> 

> 2. All rooms must either use strRoomId or roomId consistently. Mixing both will result in unexpected bugs.
> 

## ConnectOtherRoom

#### Request Cross-room Communication

By default, only users within the same room can make audio and video calls. Audio and video streams in different rooms are isolated.

However, you can use this interface to publish the audio and video streams of a host in another room to your own room. At the same time, this interface will also publish your own audio and video streams to the target host's room.

In other words, you can use this interface to enable cross-room audio and video stream sharing between hosts in two different rooms, allowing audiences in each room to watch the audio and video streams of both hosts. This feature can be used to implement a PK feature between hosts.

The result of the cross-room call request will be notified to you through the TRTCCloudListener callback onConnectOtherRoom.

For example, when Host A in room "101" establishes a cross-room call with Host B in room "102" using connectOtherRoom(),
-  All users in room "101" will receive the two event callbacks onRemoteUserEnterRoom(B) and onUserVideoAvailable(B,true) for host B, meaning all users in room "101" can subscribe to host B's audio and video.

-  Users in room "102" will receive the onRemoteUserEnterRoom(A) and onUserVideoAvailable(A,true) event callbacks for Anchor A. This means users in room "102" can subscribe to Anchor A's audio and video.

![](https://qcloudimg.tencent-cloud.cn/raw/c5e6c72fc163ad5c0b6b7b00e1da55b5.png)

To consider compatibility issues with subsequent extension fields, the parameters for cross-room communication temporarily use JSON format:

**Case 1: Numeric Room Number**

If Host A in room '101' wants to connect with Host B in room '102', Host A needs to pass in the following when calling the interface: {"roomId": 102, "userId": "userB"}

Below is the sample code:
``` java
  JSONObject jsonObj = new JSONObject();
  jsonObj.put("roomId", 102);
  jsonObj.put("userId", "userB");
  trtc.ConnectOtherRoom(jsonObj.toString());
```

**Case 2: String Room Number**

If you are using a string room number, be sure to replace "roomId" in the JSON with "strRoomId": {"strRoomId": "102", "userId": "userB"}

Below is the sample code:
``` java
  JSONObject jsonObj = new JSONObject();
  jsonObj.put("strRoomId", "102");
  jsonObj.put("userId", "userB");
  trtc.ConnectOtherRoom(jsonObj.toString());
```
| Parameters | Description |
| --- | --- |
| param | You need to pass in a JSON-formatted string argument, where roomId represents the room number in numeric format, strRoomId represents the room number in string format, and userId represents the target broadcaster's user ID. |

## DisconnectOtherRoom

#### Exit Cross-room Communication

The exit result will be notified through the onDisconnectOtherRoom callback in TRTCCloudListener.

## setDefaultStreamRecvMode

#### Set Subscription Mode (Needs to be set before entering the room to take effect)

You can switch between "auto-subscribe" and "manual subscribe" modes via this interface:
-  Automatic Subscription: Default mode where users receive audio and video streams from the room immediately after entering. Audio plays automatically and video starts decoding automatically (you still need to bind the rendering control through the startRemoteView interface).

-  Manual subscription: After the user enters the room, they need to manually call the startRemoteView interface to start the subscription and decoding of the video stream. They need to manually call the muteRemoteAudio(false) interface to start the playback of the sound.

In most scenarios, users entering a room will subscribe to all the audio and video streams from the broadcasters within that room. Therefore, TRTC defaults to an automatic subscription mode to achieve the best "instant start experience".

If your application scenario involves many audio and video streams being published in each room and each user only wants to selectively subscribe to 1-2 of them, it is recommended to use the "manual subscription" mode to save on bandwidth costs.
| Parameters | Description |
| --- | --- |
| autoRecvAudio | true: Automatically subscribe to audio; false: You need to manually call muteRemoteAudio(false) to subscribe to audio. Default value: true. |
| autoRecvVideo | true: Automatically subscribe to video; false: You need to manually call startRemoteView to subscribe to video. Default value: true. |

> **Note**
> 

> 1. This setting needs to be called before entering the room to take effect.
> 

> 2. In automatic subscription mode, if the user does not call startRemoteView to subscribe to the video stream after entering the room, the SDK will automatically stop subscribing to the video stream to save traffic.
> 

## createSubCloud

#### Create Sub-room Instances (For Multi-room Concurrent Viewing)

TRTCCloud was initially designed as a Singleton Pattern, limiting the ability to watch multiple rooms concurrently.

By calling this interface, you can create multiple TRTCCloud instances to watch audio and video streams from multiple rooms simultaneously.

However, please note that the ability to publish audio and video streams across multiple TRTCCloud instances is subject to certain restrictions.

This feature is primarily used in a business scenario called "super small class" in online education settings, aimed at addressing the limitation that "each TRTC room can only have up to 50 people broadcasting their audio and video streams simultaneously".

Below is the sample code:
``` java
    //In the small room that needs interaction, enter the room as an anchor and push audio and video streams
    TRTCCloud mainCloud = TRTCCloud.sharedInstance(mContext);
    TRTCCloudDef.TRTCParams mainParams = new TRTCCloudDef.TRTCParams();
    //Fill your params
    mainParams.role = TRTCCloudDef.TRTCRoleAnchor;
    mainCloud.enterRoom(mainParams, TRTCCloudDef.TRTC_APP_SCENE_LIVE);
    //...
    mainCloud.startLocalPreview(true, videoView);
    mainCloud.startLocalAudio(TRTCCloudDef.TRTC_AUDIO_QUALITY_DEFAULT);

    //In the large room that only needs to watch, enter the room as an audience and pull audio and video streams
    TRTCCloud subCloud = mainCloud.createSubCloud();
    TRTCCloudDef.TRTCParams subParams = new TRTCCloudDef.TRTCParams();
    //Fill your params
    subParams.role = TRTCCloudDef.TRTCRoleAudience;
    subCloud.enterRoom(subParams, TRTCCloudDef.TRTC_APP_SCENE_LIVE);
    //...
    subCloud.startRemoteView(userId, TRTCCloudDef.TRTC_VIDEO_STREAM_TYPE_BIG, view);
    //...
    //Exit from new room and release it.
    subCloud.exitRoom();
    mainCloud.destroySubCloud(subCloud);
```

> **Note**
> 
> -  The same user can enter multiple rooms with different roomIds using the same userId.
> -  Two different terminal devices cannot use the same userId to enter the same roomId simultaneously.
> -  You can set different instances to receive their respective event notifications via TRTCCloudListener.
> -  The same user can stream on multiple TRTCCloud instances and call interfaces related to local audio and video in sub-instances. However, please note:
> -  The audio for multiple instances must be either microphone capture or custom data collection, and invoking interfaces related to audio devices will be based on the last call
> -  Calls related to the camera will take the last one as definitive: startLocalPreview.

#### Return value description:

Sub TRTCCloud instances

## destroySubCloud

#### Terminate Sub-room Instances
| Parameters | Description |
| --- | --- |
| subCloud | Sub-room instances |

## updateOtherRoomForwardMode

#### Modify the uplink capability of cross-room broadcasters in this room

Usually, after calling the connectOtherRoom interface to conduct cross-room communication with another room's broadcaster, all viewers in this room will receive the audio and video stream published by that broadcaster.

You can call this interface to restrict the uplink capability of a cross-room broadcaster in this room, either forbidding or allowing them to publish audio/main video/auxiliary video. This action will affect all users in the room.

After disabling certain uplink capabilities of the cross-room broadcaster, all users in this room will not be able to receive the corresponding audio and video streams, nor will they be able to subscribe to them.

It should be noted that this interface can only be called by the broadcaster conducting cross-room communication, and the restrictions set through this interface will reset if the cross-room communication is interrupted or the corresponding broadcaster exits the room.

The result of this API call will be notified to you via the TRTCCloudListener in the onUpdateOtherRoomForwardMode callback.

For example:

In room "101", there is Host A and Audience B, while in room "102", there is Host C, who is normally publishing audio and video streams. Host A establishes a cross-room call with Host C using connectOtherRoom().
-  At this time, both Anchor A and Viewer B will receive the onRemoteUserEnterRoom(C), onUserVideoAvailable(C,true), and onUserAudioAvailable(C,true) event callbacks for Anchor C and can subscribe to Anchor C's audio and video.

Later, Host A calls this interface to disable Host C's ability to publish audio in the current room.
-  After that, Anchor C's audio stream cannot be published to room "101." Anchor A and Viewer B will receive the onUserAudioAvailable(C,false) event callback and can no longer subscribe to Anchor C's audio through muteRemoteAudio(C,false).

-  Host C's video stream will not be affected. Other audience members in room "102" are also unaffected and can normally subscribe to Host C's audio.

To consider compatibility issues with subsequent extension fields, the parameters for this interface temporarily use JSON format. The example is as follows:

**Case 1: Numeric Room Number**
``` java
{
  "roomId":102,
  "userId":"userC",
  "muteAudio":false,
  "muteVideo":true,
  "muteSubStream":false
}
```

**Case 2: String Room Number**
``` java
{
  "strRoomId":"102",
  "userId":"userC",
  "muteAudio":false,
  "muteVideo":true,
  "muteSubStream":false
}
```
| Parameters | Description |
| --- | --- |
| param | You need to pass in a JSON-formatted string argument where roomId represents the room number in numeric format, strRoomId represents the room number in string format, userId represents the target broadcaster's user ID. The options muteAudio, muteVideo, and muteSubStream denote whether to disable or allow the cross-room broadcaster to publish audio, main stream video, and sub-stream video respectively. |

## startPublishMediaStream

#### Start publishing media stream

This interface sends an instruction to the TRTC server to relay/transcode the current user's audio and video streams to the Live CDN or push them back into the TRTC room. You can specify the publishing mode through TRTCPublishTarget configuration and TRTCPublishMode
| Parameters | Description |
| --- | --- |
| config | Media stream transcoding configuration parameters. Refer to TRTCStreamMixingConfig for detailed configuration. This is required when transcoding and pushing back to the TRTC room. You need to specify your desired transcoding configuration parameters. It is invalid in relay mode. |
| params | Media stream encoding output parameters. Refer to TRTCStreamEncoderParam for detailed configuration. This is required when transcoding and pushing back to the TRTC room. You need to specify your desired transcoding output parameters. For better relay stability and CDN compatibility, it is also recommended to configure this during relay. |
| target | The target address for media stream publishing. Refer to TRTCPublishTarget for detailed configuration. Supports relay/transcoding to Tencent or third-party CDNs, and also supports transcoding pushback to the TRTC room. |

> **Note**
> 

> 1. The SDK will provide the task identifier (taskId) for the backend startup through the callback onStartPublishMediaStream.
> 

> 2. The same task (both TRTCPublishMode and TRTCPublishCdnUrl are identical) can only be started once. If you need to update or stop this task later, you must record and use the returned taskId to operate through updatePublishMediaStream or stopPublishMediaStream.
> 

> 3. The target supports configuring multiple CDN URLs simultaneously (up to 10). If the same relay/transcoding task needs to be published to multiple CDNs, you only need to configure multiple CDN URLs in the target. Even if there are multiple relay addresses for the same transcoding task, only one transcoding fee will be charged.
> 

> 4. When using, do not push multiple tasks to the same URL addresses simultaneously to avoid abnormal streaming status. A recommended scheme is to use "sdkappid_roomid_userid_main" in the URL as a distinguishing identifier. This naming convention is easy to recognize and will not cause conflicts in your multiple applications.
> 

## updatePublishMediaStream

#### Update the published media stream.

This interface will send directives to the TRTC server to update the media stream started by startPublishMediaStream
| Parameters | Description |
| --- | --- |
| config | Media stream transcoding configuration parameters. Refer to TRTCStreamMixingConfig for detailed configuration. This is required when transcoding and pushing back to the TRTC room. You need to specify your desired transcoding configuration parameters. It is invalid in relay mode. |
| params | Media stream encoding output parameters. Refer to TRTCStreamEncoderParam for detailed configuration. This is required when transcoding and pushing back to the TRTC room. You need to specify your desired transcoding output parameters. For better relay stability and CDN compatibility, it is also recommended to configure this during relay. |
| target | The target address for media stream publishing. Refer to TRTCPublishTarget for detailed configuration. Supports relay/transcoding to Tencent or third-party CDNs, and also supports transcoding pushback to the TRTC room. |
| taskId | It will provide you with the task identifier (i.e., taskId) for the background start task through the onStartPublishMediaStream callback |

> **Note**
> 

> 1. You can use this interface to update the published CDN URL (supports add and delete, up to 10 at the same time), but ensure you do not push multiple tasks to the same URL addresses simultaneously to avoid abnormal streaming status.
> 

> 2. You can update or adjust relay/transcoding tasks using taskId. For example, in PK business, you can initiate relay through startPublishMediaStream first, then use taskId and this interface to update the relay to a transcoding task when the anchor initiates PK. At this time, CDN playback will be continuous and without stream disconnection (you need to keep the media stream encoding output parameters consistent).
> 

> 3. The same task does not support switching between Audio Only, Audio and Video, and Pure Video.
> 

## stopPublishMediaStream

#### Stop publishing media stream.

This interface will send directives to the TRTC server to stop the media stream started by startPublishMediaStream
| Parameters | Description |
| --- | --- |
| taskId | It will provide you with the task identifier (i.e., taskId) for the background start task through the onStartPublishMediaStream callback |

> **Note**
> 

> 1. If your business backend has not saved the taskId, after your host re-enters the room following an abnormal exit, you can call startPublishMediaStream again to start the task. TRTC backend will return a task start failure and provide you with the taskId from the last attempt
> 

> 2. If the taskId is an empty string, all media streams started by startPublishMediaStream for that user will stop. If you have only started one media stream or want to stop all media streams you started, this method is recommended.
> 

## startLocalPreview

#### Enable the preview screen of the local camera (Mobile Terminal)

Call this function before enterRoom. The SDK will only enable the camera and wait until you call enterRoom to start streaming.

Call this function after enterRoom. The SDK will turn on the camera and automatically start video push streaming. You will receive the onCameraDidReady callback notification in TRTCCloudListener when the first frame of the camera is rendered.
| Parameters | Description |
| --- | --- |
| frontCamera | true: Front-facing camera; false: Rear-facing camera. |
| view | Control carrying the video screen. |

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

This interface is equivalent to the start/stopLocalPreview interfaces when specifying TRTC_VIDEO_STREAM_TYPE_BIG, but with better response speed.

Because start/stopLocalPreview requires turning on and off the camera, and turning on and off the camera is a hardware-related operation, which is very time-consuming.

In comparison, muteLocalVideo only needs to suspend or pass the data stream at the software layer. Therefore, it is more efficient and more suitable for scenarios requiring frequent openings and closings.

When pausing/resuming the release of TRTC_VIDEO_STREAM_TYPE_BIG, other users in the same room will receive the onUserVideoAvailable callback notification.

When pausing/resuming the release of TRTC_VIDEO_STREAM_TYPE_SUB, other users in the same room will receive the onUserSubStreamAvailable callback notification.
| Parameters | Description |
| --- | --- |
| mute | true: pause; false: resume. |
| streamType | The type of video stream to pause/resume (only supports TRTC_VIDEO_STREAM_TYPE_BIG and TRTC_VIDEO_STREAM_TYPE_SUB). |

## setVideoMuteImage

#### Set the alternative image during the suspension of the local screen

When you call muteLocalVideo(true) to pause the local video, you can set a placeholder image through this interface. After setting, other users in the room will see this placeholder image instead of a black screen.
| Parameters | Description |
| --- | --- |
| fps | Set the frame rate for the alternative image, with a minimum value of 5 and a maximum value of 10. The default is 5. |
| image | Set the alternative image. A null value means no video stream data will be sent after muteLocalVideo. The default is null. |

## startRemoteView

#### Subscribe to the video stream of a remote user and bind the video rendering control

By calling this API, the SDK can pull the video stream of the specified user ID and render it on the rendering control specified by the parameter view. You can set the display mode of the screen through setRemoteRenderParams.
-  If you already know the user ID of a user who has a video stream in the room, you can directly call startRemoteView to subscribe to that user's video feed.

-  If you do not know which users in the room are publishing video, you can wait for a notification from onUserVideoAvailable after entering the room.

Calling this API only starts pulling the video stream, at this point the screen still needs to load and buffer. When buffering is complete, you will receive a notification from onFirstVideoFrame.
| Parameters | Description |
| --- | --- |
| streamType | Specify the type of video stream of the user you want to watch. -  HD main video stream: TRTC_VIDEO_STREAM_TYPE_BIG. -  Low-res sub video stream: TRTC_VIDEO_STREAM_TYPE_SMALL (effective only if the remote user has enabled dual encoding through enableEncSmallVideoStream). -  Substream video (typically used for screen sharing): TRTC_VIDEO_STREAM_TYPE_SUB. |
| userId | Specify the remote user's ID. |
| view | Rendering control used to display the video screen. |

> **Note**
> 

> Note a few rules:
> 

> 1. The SDK supports watching the main stream and substream of a certain user ID simultaneously, or watching the substream and small stream of a certain user ID simultaneously, but does not support watching the main stream and small stream simultaneously.
> 

> 2. You can only watch the small stream of the specified user ID when dual-stream encoding is enabled through enableEncSmallVideoStream.
> 

> 3. When the small stream of the specified user ID does not exist, the SDK will default to the user's main stream.
> 

## updateRemoteView

#### Update the video rendering control of a remote user

This interface can be used to update the rendering control of a remote video image and is commonly used in scenarios that involve switching display areas.
| Parameters | Description |
| --- | --- |
| streamType | The type of stream to set the preview window for (only supports TRTC_VIDEO_STREAM_TYPE_BIG and TRTC_VIDEO_STREAM_TYPE_SUB). |
| userId | Specify the remote user's ID. |
| view | Control carrying the video screen. |

## stopRemoteView

#### Unsubscribe from the remote user's video stream and release the rendering control

Calling this interface will make the SDK stop receiving the video stream of the user and release the decoding and rendering resources of that video stream.
| Parameters | Description |
| --- | --- |
| streamType | Specify the type of video stream of the user you want to watch. -  HD main video stream: TRTC_VIDEO_STREAM_TYPE_BIG. -  Low-res sub video stream: TRTC_VIDEO_STREAM_TYPE_SMALL. -  Substream video (typically used for screen sharing): TRTC_VIDEO_STREAM_TYPE_SUB. |
| userId | Specify the remote user's ID. |

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
| Parameters | Description |
| --- | --- |
| mute | Pause receiving or not. |
| streamType | The video stream type to be paused/resumed. -  HD main video stream: TRTC_VIDEO_STREAM_TYPE_BIG. -  Low-res sub video stream: TRTC_VIDEO_STREAM_TYPE_SMALL. -  Substream video (typically used for screen sharing): TRTC_VIDEO_STREAM_TYPE_SUB. |
| userId | Specify the remote user's ID. |

> **Note**
> 

> This interface supports calling before entering the room (enterRoom), and the paused state will be reset after leaving the room (exitRoom).
> 

> After calling this interface to pause receiving a specified user's video stream, calling only the startRemoteView interface will not play the specified user's video. You need to call muteRemoteVideoStream(false) or muteAllRemoteVideoStreams(false) to recover.
> 

## muteAllRemoteVideoStreams

#### Suspend/Resume subscription of all remote users' video streams

This interface only pauses/resumes receiving all users' video streams but does not release the display resources. The video image will be frozen on the last frame at the time of the interface call.
| Parameters | Description |
| --- | --- |
| mute | Pause receiving or not. |

> **Note**
> 

> This interface supports calling before entering the room (enterRoom), and the paused state will be reset after leaving the room (exitRoom).
> 

> After calling this interface to pause receiving all users' video streams, calling only the startRemoteView interface will not play a specified user's video. You need to call muteRemoteVideoStream(false) or muteAllRemoteVideoStreams(false) to recover.
> 

## setVideoEncoderParam

#### Set encoding parameters for the video encoder

This setting determines the screen quality seen by remote users, and also affects the screen quality of the recorded video file on the cloud.
| Parameters | Description |
| --- | --- |
| param | Used to set the video encoder parameters. For details, see TRTCVideoEncParam. |

> **Note**
> 

> Starting from version v11.5, the encoding output resolution will align with width 8 height 2 bytes, and it will be adjusted downwards; eg: input resolution 540x960, actual encoding output resolution 536x960.
> 

## setNetworkQosParam

#### Set network quality control parameters

This setting determines the quality control strategy under poor network conditions, such as "Quality Priority" or "Smoothness Priority" strategies.
| Parameters | Description |
| --- | --- |
| param | Used to set the network quality control parameters. For details, see TRTCNetworkQosParam. |

## setLocalRenderParams

#### Set rendering parameters for the local screen

Configurable parameters include: rotation angle, fill mode, and left-right mirroring of the picture.
| Parameters | Description |
| --- | --- |
| params | Picture render parameters, see TRTCRenderParams for details. |

## setRemoteRenderParams

#### Set rendering mode for the remote screen

Configurable parameters include: rotation angle, fill mode, and left-right mirroring of the picture.
| Parameters | Description |
| --- | --- |
| params | Picture render parameters, see TRTCRenderParams for details. |
| streamType | It can be set as the main road picture (TRTC_VIDEO_STREAM_TYPE_BIG) or the auxiliary stream picture (TRTC_VIDEO_STREAM_TYPE_SUB). |
| userId | Specify the remote user's ID. |

## enableEncSmallVideoStream

#### Enable picture-in-picture dual-stream encoding mode

After enabling the dual-stream encoding mode, the current user's encoder will output both [HD large screen] and [low-definition small picture] video streams (but only one audio stream).

This way, other users in the room can choose to subscribe to [HD large screen] or [low-definition small screen] based on their network conditions or screen size.
| Parameters | Description |
| --- | --- |
| enable | Whether to enable small picture encoding, default value: false. |
| smallVideoEncParam | Video parameters for the substream. |

> **Note**
> 

> When the dual-stream encoding mode is enabled, it consumes more CPU and network bandwidth. Therefore, it may be considered for use on Mac, Windows, or high-performance Pads. It is not recommended for mobile devices.
> 

#### Return value description:

0: Success; -1: The current main screen has been set to lower quality, making dual-channel encoding unnecessary.

## setRemoteVideoStreamType

#### Switch picture-in-picture for the specified remote user

After a host in the room has enabled dual-channel encoding, the default screen subscribed by other users in the room through startRemoteView will be [HD large screen].

You can use this interface to select whether you want to subscribe to the large screen or small screen. This interface is effective whether called before or after startRemoteView.
| Parameters | Description |
| --- | --- |
| streamType | Video stream type, i.e., choose to watch the large screen or the small screen, default is large screen. |
| userId | Specify the remote user's ID. |

> **Note**
> 

> This feature requires the target user to have already enabled dual-channel encoding mode through enableEncSmallVideoStream in advance; otherwise, this call has no actual effect.
> 

## snapshotVideo

#### Take a video screenshot

You can use this interface to capture the local video footage, the main stream picture of a remote user, and the auxiliary stream (screen sharing) picture of a remote user.
| Parameters | Description |
| --- | --- |
| sourceType | Picture source can be chosen as video stream capture (TRTCSnapshotSourceTypeStream), video rendering picture (TRTCSnapshotSourceTypeView), or captured frame (TRTCSnapshotSourceTypeCapture). Captured frame screenshots are clearer. |
| streamType | Video stream type can be selected as the main road picture (TRTC_VIDEO_STREAM_TYPE_BIG, commonly used for the camera) or auxiliary stream picture (TRTC_VIDEO_STREAM_TYPE_SUB, commonly used for screen sharing). |
| userId | User ID, if left blank, indicates capturing the local video footage. |

> **Note**
> 

> The Windows platform currently only supports capturing video pictures from TRTCSnapshotSourceTypeStream sources.
> 

## setPerspectiveCorrectionPoints

#### Set perspective correction coordinate settings for the video screen

You can specify the coordinate area for perspective correction of the rendered image through this interface.
| Parameters | Description |
| --- | --- |
| dstPoints | The target coordinates area to be corrected to, consists of 4 vertex coordinates. They need to be passed in the order of top-left, bottom-left, top-right, and bottom-right. All coordinates need to be normalized to the [0,1] range based on the image width and height; passing null will stop the perspective correction. |
| srcPoints | The original image coordinate area consists of 4 vertex coordinates. They need to be passed in the order of top-left, bottom-left, top-right, and bottom-right. All coordinates need to be normalized to the [0,1] range based on the image width and height; passing null will stop the perspective correction. |
| userId | User ID, if left blank, indicates correcting the local video footage. |

## setGravitySensorAdaptiveMode

#### Set gravity sensing adaptive mode (11.7 and above)

After gravity sensing is enabled, if the collection end device rotates, both the collection end and audience side will render the image accordingly to ensure the image in the view is always upright.

It only takes effect in the SDK internal camera capture scene and only works on the mobile terminal.

1. This interface only affects the collection end. If you are just watching the image in the room, enabling this interface is ineffective

2. When the collection end device rotates 90 degrees or 270 degrees, the image seen by the collection end or audience side may be cropped to maintain aspect ratio coordination
| Parameters | Description |
| --- | --- |
| mode | Gravity sensing mode: for details, please refer to TRTC_GRAVITY_SENSOR_ADAPTIVE_MODE_DISABLE, TRTC_GRAVITY_SENSOR_ADAPTIVE_MODE_FILL_BY_CENTER_CROP, and TRTC_GRAVITY_SENSOR_ADAPTIVE_MODE_FIT_WITH_BLACK_BORDER. Default value: TRTC_GRAVITY_SENSOR_ADAPTIVE_MODE_DISABLE. |

## startLocalAudio

#### Enable collection and publishing of local audio

The SDK does not enable the microphone by default. When users need to publish local audio, they need to call this interface to enable microphone collection and encoding and publish the audio to the current room.

After enabling the collection and publishing of local audio, other users in the room will receive onUserAudioAvailable(userId, true) notification.
| Parameters | Description |
| --- | --- |
| quality | Sound quality - TRTC_AUDIO_QUALITY_SPEECH, Smooth: Sample rate: 16k; Mono; Audio bitrate: 16kbps; Suitable for voice call-centric scenarios, such as online meetings and voice calls. - TRTC_AUDIO_QUALITY_DEFAULT, Default: Sample rate: 48k; Mono; Audio bitrate: 50kbps; Default SDK audio quality, recommended if there are no special requirements. - TRTC_AUDIO_QUALITY_MUSIC, High quality: Sample rate: 48k; Stereo + Full band; Audio bitrate: 128kbps; Suitable for high-fidelity music transmission scenarios, such as online karaoke and music live streaming. |

> **Note**
> 

> This function checks the microphone permissions. If the current app does not have microphone permissions, the SDK will automatically request microphone permissions from the user.
> 

## stopLocalAudio

#### Stop collection and publishing of local audio

After stopping the collection and publishing of local audio, other users in the room will receive onUserAudioAvailable(userId, false) notification.

## muteLocalAudio

#### Pause/Resume publishing of the local audio stream

When you pause the publishing of the local audio stream, other users in the room will receive onUserAudioAvailable(userId, false) notification.

When you resume the publishing of the local audio stream, other users in the room will receive onUserAudioAvailable(userId, true) notification.

The difference from stopLocalAudio is that muteLocalAudio(true) does not release the microphone permissions but continues to send a low-bit-rate silent packet.

This is very suitable for scenarios that require cloud recording because video files in formats like MP4 demand high continuity of audio data, and using stopLocalAudio will make the recorded MP4 files difficult to play.

Therefore, in scenarios where the quality of the recorded files is highly required, it is recommended to choose muteLocalAudio instead of stopLocalAudio.
| Parameters | Description |
| --- | --- |
| mute | true: Mute; false: Unmute. |

## muteRemoteAudio

#### Pause/Resume playing of the remote audio stream

When you mute a user's remote audio, the SDK will stop playing the specified user's sound and will also stop pulling that user's audio data.
| Parameters | Description |
| --- | --- |
| mute | true: Mute; false: Unmute. |
| userId | Used to specify the remote user's ID. |

> **Note**
> 

> This interface is effective whether called before or after entering the room (enterRoom). The mute status will be reset to false after exiting the room (exitRoom).
> 

## muteAllRemoteAudio

#### Pause/Resume playing of all remote users' audio streams

When you mute all users' remote audio, the SDK will stop playing all remote audio streams and will also stop pulling all users' audio data.
| Parameters | Description |
| --- | --- |
| mute | true: Mute; false: Unmute. |

> **Note**
> 

> This interface is effective whether called before or after entering the room (enterRoom). The mute status will be reset to false after exiting the room (exitRoom).
> 

## setAudioRoute

#### Sets audio routing.

Set "audio routing", i.e., whether the sound is played through the mobile phone's speaker or earpiece. Therefore, this interface is only applicable to mobile devices such as phones.

A mobile phone has two speakers: one is the earpiece located at the top of the phone, and the other is the stereo speaker located at the bottom.

When the audio routing is set to the earpiece, the sound is relatively low, and you need to bring your ear close to hear it clearly, ensuring better privacy. It is suitable for phone calls.

When the audio routing is set to the speaker, the sound is relatively loud. You can hear it clearly without holding the phone to your face, thus enabling the "hands-free" feature.
| Parameters | Description |
| --- | --- |
| route | Audio routing, i.e., where the sound is output (speaker, earpiece), default value: TRTC_AUDIO_ROUTE_SPEAKER. |

## setRemoteAudioVolume

#### Set the playback volume for a specific remote user

You can mute a remote user's sound by using setRemoteAudioVolume(userId, 0).
| Parameters | Description |
| --- | --- |
| userId | Used to specify the remote user's ID. |
| volume | Volume. Value range: 0-100. Default value: 100. |

> **Note**
> 

> If you still feel the volume is too low after setting it to 100, you can set the maximum volume to 150. However, a volume above 100 carries a risk of pop noise, so proceed with caution.
> 

## setAudioCaptureVolume

#### Sets the local audio capture volume.
| Parameters | Description |
| --- | --- |
| volume | Volume. Value range: 0-100. Default value: 100. |

> **Note**
> 

> If you still feel the volume is too low after setting it to 100, you can set the maximum volume to 150. However, a volume above 100 carries a risk of pop noise, so proceed with caution.
> 

## getAudioCaptureVolume

#### Obtains the local audio capture volume.

## setAudioPlayoutVolume

#### Sets the remote audio playback volume.

This interface controls the volume that the SDK finally delivers to the system for playback. The adjustment will affect the volume of the local audio recording file, but it will not affect the volume of the ear return.
| Parameters | Description |
| --- | --- |
| volume | Volume. Value range: 0-100. Default value: 100. |

> **Note**
> 

> If you still feel the volume is too low after setting it to 100, you can set the maximum volume to 150. However, a volume above 100 carries a risk of pop noise, so proceed with caution.
> 

## getAudioPlayoutVolume

#### Obtains the remote audio playback volume.

## enableAudioVolumeEvaluation

#### Enable volume reminder

After enabling this feature, the SDK will provide feedback on the audio volume evaluation information of local or remote users in the callback TRTCCloudListeneronUserVoiceVolume, including volume level, voice detection, audio spectrum, etc.
| Parameters | Description |
| --- | --- |
| enable | Whether to enable volume prompts, disabled by default. |
| params | For volume assessment and other related parameters, please refer to TRTCAudioVolumeEvaluateParams. |

## startAudioRecording

#### Start recording

When you call this interface, the SDK will mix and record all local and remote audio (including local audio, remote audio, background music, and sound effects) into a local file.

This interface can be called both before and after entering the room. If the recording task is not stopped by stopAudioRecording before exiting the room, the task will automatically stop after exiting the room.

The start and completion status of this recording will be notified through local recording-related callbacks. See the TRTCCloud related callbacks.
| Parameters | Description |
| --- | --- |
| param | For recording parameters, please refer to TRTCAudioRecordingParams. |

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
| Parameters | Description |
| --- | --- |
| params | For recording parameters, please refer to TRTCLocalRecordingParams. |

## stopLocalRecording

#### Stop local media recording

If the recording task is not stopped by this interface before exiting the room, the recording task will automatically stop after exiting the room.

## setRemoteAudioParallelParams

#### Set intelligent concurrent playback strategy for remote audio streams

Set intelligent concurrent playback strategy for remote audio streams, suitable for scenarios with a large number of people on the microphone.
| Parameters | Description |
| --- | --- |
| params | For audio concurrency parameters, please refer to TRTCAudioParallelParams. |

## enable3DSpatialAudioEffect

#### Enable 3D audio

Enable 3D audio effects. Note that smooth audio quality TRTC_AUDIO_QUALITY_SPEECH or default audio quality TRTC_AUDIO_QUALITY_DEFAULT is required.
| Parameters | Description |
| --- | --- |
| enabled | Whether to enable 3D audio effects, disabled by default. |

## updateSelf3DSpatialPosition

#### Set self coordinates and orientation information in 3D audio

Update your position and orientation in the world coordinate system. The SDK will calculate the relative position between yourself and remote users based on the parameters of this method and render spatial audio effects accordingly. Note that each parameter should be passed in as an array of length 3.
| Parameters | Description |
| --- | --- |
| axisForward | The unit vector of the front axis of the local coordinate system in the world coordinate system, with three values representing the front, right, and up coordinate values, respectively. |
| axisRight | The unit vector of the right axis of the local coordinate system in the world coordinate system, with three values representing the front, right, and up coordinate values, respectively. |
| axisUp | The unit vector of the up axis of the local coordinate system in the world coordinate system, with three values representing the front, right, and up coordinate values, respectively. |
| position | Your coordinate in the world coordinate system, with three values representing the front, right, and up coordinate values, respectively. |

> **Note**
> 

> Please appropriately limit the invocation frequency. It is recommended to set coordinates at intervals of at least 100ms.
> 

## updateRemote3DSpatialPosition

#### Set remote user coordinate information in 3D audio

Update the position of remote users in the world coordinate system. The SDK will render spatial audio effects based on the relative position between yourself and the remote users. Note that the parameter is an array of length 3.
| Parameters | Description |
| --- | --- |
| position | The coordinate of the remote user in the world coordinate system, with three values representing the front, right, and up coordinate values, respectively. |
| userId | Specify the remote user's ID. |

> **Note**
> 

> Please appropriately limit the invocation frequency. It is recommended to set coordinates for the same remote user at intervals of at least 100ms.
> 

## set3DSpatialReceivingRange

#### Set the receivable range of sounds emitted by a specified user

After setting this range size, the specified user's voice will be audible within this range, and any sound beyond this range will be attenuated to 0.
| Parameters | Description |
| --- | --- |
| range | Maximum range at which the sound can be received. |
| userId | Specify the remote user's ID. |

## getDeviceManager

#### Get Device Management Class (TXDeviceManager)

## getBeautyManager

#### Get Beauty Management Class (TXBeautyManager)

Through beauty management, you can use the following features:
-  Set beauty effects such as "Skin Smoothing", "Whitening", "Rosy".

-  Set facial enhancement effects like "Big Eyes", "Slim Face", "V Face", "Chin", "Short Face", "Small Nose", "Bright Eyes", "White Teeth", "Remove Eye Bags", "Remove Wrinkles", "Remove Nasolabial Folds".

-  Set facial enhancement effects such as "Hairline", "Eye Distance", "Eye Tilt", "Mouth Shape", "Nasal Sides", "Nose Position", "Lip Thickness", "Face Shape".

-  Set makeup effects like "Eyeshadow", "Blush".

-  Set dynamic stickers and face pendants for animation effects.

## setWatermark

#### Watermarking

The position of the watermark is specified through the rect parameter. Rect is a quadruplet parameter in the format (x, y, width, height)
-  x: Coordinate of the watermark, with a value range of 0-1 as a float.

-  y: Coordinate of the watermark, with a value range of 0-1 as a float.

-  width: Width of the watermark, with a value range of 0-1 as a float.

-  height does not need to be set; the SDK will automatically calculate an appropriate height based on the aspect ratio of the watermark image.

Example of parameter settings:

If the current video encoding resolution is 540 × 960, and the rect parameter is set to (0.1, 0.1, 0.2, 0.0),

Then, the top-left coordinate of the watermark is (540 * 0.1, 960 * 0.1), which is (54, 96). The width of the watermark is 540 * 0.2 = 108px. The height of the watermark will be automatically calculated by the SDK based on the aspect ratio of the watermark image.
| Parameters | Description |
| --- | --- |
| image | Watermark image, ** must be in png format with a transparent background **. |
| rect | Normalized coordinates of the watermark relative to the encoding resolution: x, y, width, height. Value range: 0 - 1. |
| streamType | Specify which stream to set the watermark for. For details, see TRTCVideoStreamType. |

> **Note**
> 

> If you need to set the watermark for both the main stream (usually the camera) and the auxiliary stream (usually used for screen sharing), you need to call this interface twice and set different streamTypes.
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

#### Enable System Sound Capturing

This interface will capture audio data from other applications and mix it into the current audio data stream of the SDK, so that other users in the room can also hear the sound played by the broadcaster's other applications.

In online education scenarios, teachers can use this feature to allow the SDK to capture the audio from educational videos and broadcast it to students in the same room.

In music live streaming scenarios, the host can use this feature to allow the SDK to capture audio from the music player to add background music to their live stream.

> **Note**
> 

> 1. This interface only takes effect on Android API 29 and above.
> 

> 2. You need to use this interface to enable system sound capture before the screen sharing interface can be effectively used.
> 

> 3. You need to add a foreground service to ensure that system sound capture is not silenced, and set android:foregroundServiceType="mediaProjection".
> 

> 4. The SDK only captures the application audio that meets the capture strategy and audio usage. Currently, the captured audio usage includes USAGE_MEDIA and USAGE_GAME.
> 

## stopSystemAudioLoopback

#### Stop System Sound Capture (iOS not yet supported)

## startScreenCapture

#### Start Screen Sharing

This interface supports capturing the entire Android system screen, enabling system-wide screen sharing similar to Tencent Meeting.

Refer to documentation: [Real-time Screen Sharing (Android)](https://cloud.tencent.com/document/product/647/45751)

Recommended screen sharing video encoding parameters for Android (TRTCVideoEncParam):
-  Resolution (videoResolution): 1280×720.

-  Frame Rate (videoFps): 10 FPS.

-  Bitrate (videoBitrate): 1200 kbps.

-  Resolution Adaptation (enableAdjustRes): false.

| Parameters | Description |
| --- | --- |
| encParams | For encoding parameters, please refer to TRTCVideoEncParam. If you set encParams to null, the SDK will automatically use the previously set encoding parameters. |
| shareParams | Please refer to TRTCScreenShareParams. You can pop up a floating window using the floatingView parameter (or use the Android system's WindowManager interface to pop it up yourself). |
| streamType | The circuit used for screen sharing can be set to primary channel (TRTC_VIDEO_STREAM_TYPE_BIG) or secondary channel (TRTC_VIDEO_STREAM_TYPE_SUB). |

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

## setSubStreamEncoderParam

#### Set Video Encoding Parameters for Screen Sharing (Sub-Stream) (Supported on Both Desktop and Mobile Systems)

This interface can set the screen sharing (sub-stream) quality seen by remote users, and also determine the screen sharing quality in the cloud-recorded video file.

Please note the differences between the following two interfaces:
- setVideoEncoderParam is used to set video encoding parameters for the primary channel (TRTC_VIDEO_STREAM_TYPE_BIG, typically used for the camera).

- setSubStreamEncoderParam is used to set video encoding parameters for the secondary channel (TRTC_VIDEO_STREAM_TYPE_SUB, typically used for screen sharing).

| Parameters | Description |
| --- | --- |
| param | For auxiliary stream encoding parameters, please refer to TRTCVideoEncParam. |

## enableCustomVideoCapture

#### Enable/Disable Custom Video Capturing Mode

After enabling this mode, the SDK will stop running the original video capture process. It will no longer collect data from the camera and apply beauty filters, retaining only video encoding and sending capabilities.

You need to continuously send self-collected video frames to the SDK via sendCustomVideoData.
| Parameters | Description |
| --- | --- |
| enable | Whether to enable, default value: false. |
| streamType | Used to specify video stream type, TRTC_VIDEO_STREAM_TYPE_BIG: high-definition large image; TRTC_VIDEO_STREAM_TYPE_SUB: secondary channel image. |

## sendCustomVideoData

#### Submit Self-collected Video Frames to the SDK

This interface allows you to submit self-collected video frames to the SDK. The SDK will encode the video frames and transmit them through its network module.

There are two casting schemes on the Android platform:
-  Memory transfer scheme: simpler to integrate but performs poorly, not suitable for high-resolution scenarios.

-  Video memory transfer scheme: requires some OpenGL basics but performs better; resolutions above 640 × 360 should use this scheme.

Refer to documentation: [Custom Collection and Rendering](https://cloud.tencent.com/document/product/647/34066).
| Parameters | Description |
| --- | --- |
| frame | Video data, if using the memory transfer scheme, please set the data field; if using the video memory transfer scheme, please set the TRTCTexture field. For details, please refer to TRTCVideoFrame. |
| streamType | Used to specify video stream type, TRTC_VIDEO_STREAM_TYPE_BIG: HD large screen; TRTC_VIDEO_STREAM_TYPE_SUB: secondary channel image. |

> **Note**
> 

> 1. It is recommended to call the generateCustomPTS interface to get the timestamp value of the frame after capturing a video frame, to achieve the best audio-video synchronization.
> 

> 2. The final frame rate of the encoded video by the SDK is determined by the FPS you set in setVideoEncoderParam, not by the frequency at which you call this interface.
> 

> 3. Please try to keep the intervals between calls to this interface uniform. Otherwise, it may cause unstable encoder output frame rates or audio-video asynchrony.
> 

## enableCustomAudioCapture

#### Enable Custom Audio Capturing Mode

After enabling this mode, the SDK will no longer run the original audio capture process, meaning it will stop capturing audio data from the microphone and only retain audio encoding and sending capabilities.

You need to continuously feed the SDK with your own collected audio data through sendCustomAudioData.
| Parameters | Description |
| --- | --- |
| enable | Whether to enable, default value: false. |

> **Note**
> 

> As Echo Cancellation (AEC) requires strict control over the timing of audio capture and playback, enabling custom audio capture may result in AEC capabilities becoming ineffective.
> 

## sendCustomAudioData

#### Submit Self-collected Audio Data to the SDK

Parameter TRTCAudioFrame is recommended to be filled as follows (other fields do not need to be filled):
-  audioFormat: Audio data format, only supports TRTCAudioFrameFormatPCM.

-  data: Audio frame buffer. Audio frame data only supports PCM format, with frame lengths ranging from [5ms ~ 100ms]. A frame length of 20ms is recommended. Calculation method: [48000 sampling rate, mono channel frame length: 48000 × 0.02s × 1 × 16bit = 15360bit = 1920 bytes].

-  sampleRate: Sampling rate, supported values are 16000, 24000, 32000, 44100, 48000.

-  channel: Number of channels (if stereo, data is interleaved), mono: 1; stereo: 2.

-  timestamp: Timestamp, in milliseconds (ms). Please use the timestamp recorded when the audio frame is captured (you can get the timestamp by calling generateCustomPTS after capturing an audio frame).

Refer to documentation: [Custom Collection and Rendering](https://cloud.tencent.com/document/product/647/74692).
| Parameters | Description |
| --- | --- |
| frame | Audio Data |

> **Note**
> 

> Please call this interface accurately at intervals corresponding to the duration of each frame. Feeding data at uneven intervals is likely to cause audio stutter.
> 

## enableMixExternalAudioFrame

#### Enable/Disable Custom Audio Track

Once enabled, you can use this interface to mix a Custom Audio Track into the SDK. With two boolean parameters, you can control whether the track should play remotely and locally.
| Parameters | Description |
| --- | --- |
| enablePlayout | Control whether the mixed audio track should be played locally. Default value: false. |
| enablePublish | Control whether the mixed audio track should be played remotely. Default value: false. |

> **Note**
> 

> If you set both enablePublish and enablePlayout parameters to false, it means you completely disable your custom audio track.
> 

## mixExternalAudioFrame

#### Mix Custom Audio Track into the SDK

Before calling this interface, you need to enable the Custom Audio Track with enableMixExternalAudioFrame first. After that, you can use this interface to mix your own audio track into the SDK in PCM format.

Ideally, we expect your code to provide track data to the SDK at a very consistent rate. However, we understand that maintaining perfect call intervals is a significant challenge.

Therefore, the SDK will initiate a buffer for audio track data internally. This buffer acts like a "reservoir", capable of temporarily storing the audio track data you input, smoothing out the jitter caused by intervals between interface calls.

The return value of this interface represents the size of this track buffer zone, measured in milliseconds (ms). For example: if this interface returns 50, it means the current track buffer zone has 50ms worth of track data. Therefore, as long as you call this interface again within 50ms, the SDK can ensure the continuity of your mixed track data.

When you call this interface, if you find the return value > 100ms, you can wait for one frame of audio playback time before calling again; if the return value < 100ms, it means the buffer is relatively small, you can mix in some more audio track data to ensure the size of the audio track buffer remains above the "safe level".

Parameter TRTCAudioFrame is recommended to be filled as follows (other fields do not need to be filled):
-  data: Audio frame buffer. Audio frame data only supports PCM format, with frame lengths ranging from [5ms ~ 100ms]. A frame length of 20ms is recommended. Calculation method: [48000 sampling rate, mono channel frame length: 48000 × 0.02s × 1 × 16bit = 15360bit = 1920 bytes].

-  sampleRate: Sampling rate, supported values are 16000, 24000, 32000, 44100, 48000.

-  channel: Number of channels (if stereo, data is interleaved), mono: 1; stereo: 2.

-  timestamp: Timestamp, in milliseconds (ms). Please use the timestamp recorded when the audio frame is captured (you can get the timestamp by calling generateCustomPTS after capturing an audio frame).

| Parameters | Description |
| --- | --- |
| frame | Audio Data |

> **Note**
> 

> Please call this interface accurately at intervals corresponding to the duration of each frame. Feeding data at uneven intervals is likely to cause audio stutter.
> 

#### Return value description:

>= 0 Buffered length, unit: ms. < 0 Error (-1 mixExternalAudioFrame not enabled)

## setMixExternalAudioVolume

#### Set the Streaming Volume and Playback Volume for External Audio Mixed During Streaming
| Parameters | Description |
| --- | --- |
| playoutVolume | Set the playback volume level, ranging from 0 to 100. -1 means no change. |
| publishVolume | Set the streaming volume level, ranging from 0 to 100. -1 means no change. |

## generateCustomPTS

#### Generate Timestamp for Custom Capturing

This interface is only applicable to custom capturing mode, used to solve the issue of audio and video out of sync caused by the discrepancy between capture time and delivery time.

When you use interfaces such as sendCustomVideoData or sendCustomAudioData for custom video or audio capturing, please follow these steps to use this interface:

1. First, when capturing a video or audio frame, call this interface to obtain the PTS timestamp of that moment.

2. Then, you can send the video or audio frame to the preprocessing module you use (such as third-party beauty components or third-party audio effect components).

3. When actually calling sendCustomVideoData or sendCustomAudioData for streaming, please assign the PTS timestamp recorded during capture to the timestamp field in TRTCVideoFrame or TRTCAudioFrame.

#### Return value description:

Timestamp (unit: ms)

## setLocalVideoProcessListener

#### Set Video Data Callback for Third-party Beauty Filter

After setting this callback, the SDK will pass the collected video frames to the listener you set for third-party beauty filter components for secondary processing. After that, the SDK will encode and send the processed video frames.
| Parameters | Description |
| --- | --- |
| bufferType | Specify the data format for the callback. Currently supported: - TRTC_VIDEO_BUFFER_TYPE_TEXTURE: Suitable when pixelFormat is set to TRTC_VIDEO_PIXEL_FORMAT_Texture_2D. - TRTC_VIDEO_BUFFER_TYPE_BYTE_BUFFER: Suitable when pixelFormat is set to TRTC_VIDEO_PIXEL_FORMAT_I420. - TRTC_VIDEO_BUFFER_TYPE_BYTE_ARRAY: Suitable when pixelFormat is set to TRTC_VIDEO_PIXEL_FORMAT_I420. |
| listener | Custom pre-processing callback, see TRTCVideoFrameListener for details. |
| pixelFormat | Specify the pixel format for the callback. Currently supported: - TRTC_VIDEO_PIXEL_FORMAT_Texture_2D: Graphics Memory Texture Solution. - TRTC_VIDEO_PIXEL_FORMAT_I420: Memory Data Solution. |

#### Return value description:

0: Success; < 0: Error

## setLocalVideoRenderListener

#### Set Local Video Custom Rendering Callback

After setting this callback, the SDK will skip the original rendering process and return the captured data. You need to handle the rendering yourself.
-  pixelFormat specifies the data format for the callback. Currently supports Texture2D, I420, and RGBA formats.

-  bufferType specifies the type of buffer. BYTE_BUFFER is suitable for use in the JNI layer, while BYTE_ARRAY can be used for direct operations in the Java layer.

Refer to documentation: [Custom Collection and Rendering](https://cloud.tencent.com/document/product/647/34066).
| Parameters | Description |
| --- | --- |
| bufferType | Specify the data structure of the video frame: - TRTC_VIDEO_BUFFER_TYPE_TEXTURE: Suitable when pixelFormat is set to TRTC_VIDEO_PIXEL_FORMAT_Texture_2D. - TRTC_VIDEO_BUFFER_TYPE_BYTE_BUFFER: Suitable when pixelFormat is set to TRTC_VIDEO_PIXEL_FORMAT_I420 and TRTC_VIDEO_PIXEL_FORMAT_RGBA. - TRTC_VIDEO_BUFFER_TYPE_BYTE_ARRAY: Suitable when pixelFormat is set to TRTC_VIDEO_PIXEL_FORMAT_I420 and TRTC_VIDEO_PIXEL_FORMAT_RGBA. |
| listener | Custom video rendering callback, each video frame triggers a callback. |
| pixelFormat | Specify the pixel format of the video frame, such as: - TRTC_VIDEO_PIXEL_FORMAT_Texture_2D: OpenGL texture format, more suitable for GPU processing, high processing efficiency. - TRTC_VIDEO_PIXEL_FORMAT_I420: Standard I420 format, more suitable for CPU processing, low processing efficiency. - TRTC_VIDEO_PIXEL_FORMAT_RGBA: RGBA format, more suitable for CPU processing, low processing efficiency. |

#### Return value description:

0: Success; < 0: Error.

## setRemoteVideoRenderListener

#### Sets the rendering callback for remote video self-definition

After setting this callback, the SDK will skip the original rendering process and return the captured data. You need to handle the rendering yourself.
-  pixelFormat specifies the data format for the callback, such as NV12, i420, and 32BGRA.

-  bufferType specifies the type of buffer. Using PixelBuffer has the highest efficiency; using NSData involves an internal memory conversion within the SDK, resulting in additional performance loss.

Refer to documentation: [Custom Collection and Rendering](https://cloud.tencent.com/document/product/647/34066).
| Parameters | Description |
| --- | --- |
| bufferType | Specify the data structure of the video frame, such as TRTC_VIDEO_BUFFER_TYPE_BYTE_BUFFER, TRTC_VIDEO_BUFFER_TYPE_BYTE_ARRAY. |
| listener | Custom video rendering callback, each video frame triggers a callback. |
| pixelFormat | Specify the pixel format of the video frame. Currently supports TRTC_VIDEO_PIXEL_FORMAT_I420, TRTC_VIDEO_PIXEL_FORMAT_RGBA. |
| userId | Specify the remote user's ID. |

> **Note**
> 

> In actual use, you need to first call startRemoteView(userid, null) to start the remote video stream pulling and set view to null; otherwise, no data callback will occur.
> 

#### Return value description:

0: Success; < 0: Error.

## setAudioFrameListener

#### Sets the audio data self-definition callback

After setting this callback, the SDK will internally callback the audio data (PCM format), including:
- onCapturedAudioFrame: Audio data callback captured by the local microphone

- onLocalProcessedAudioFrame: Audio data callback captured locally and preprocessed by the audio module

- onRemoteUserAudioFrame: Audio data of each remote user before mixing

- onMixedPlayAudioFrame: Audio data callback after mixing various audio streams and finally to be played by the system

> **Note**
> 

> Setting the callback to null means stopping the Definition audio callback; vice versa, setting the callback to non-null means starting the Definition audio callback.
> 

## setCapturedAudioFrameCallbackFormat

#### Sets the callback format for audio frames captured by the local microphone

This interface is used to set the format of the AudioFrame callback for onCapturedAudioFrame:
-  sampleRate: Sampling rate, supported values are 16000, 32000, 44100, 48000.

-  channel: Number of channels (if stereo, data is interleaved), mono: 1; stereo: 2.

-  samplesPerCall: Number of sampling points, Definition callback data frame length. The frame length must be an integer multiple of 10ms.

If you want to calculate the callback frame length in milliseconds, the formula to convert milliseconds to sampling points is: sampling points = milliseconds * sampling rate / 1000.

Example: For a 48000 sampling rate and a desired callback frame length of 20ms, the number of sampling points should be: 960 = 20 * 48000 / 1000.
| Parameters | Description |
| --- | --- |
| format | Audio Data Callback Format. |

> **Note**
> 

> The final callback frame length is in bytes. The formula to convert sampling points to bytes is: Byte Count = Sampling Points * Channels * 2 (Bit Width). Example: For a 48000 sampling rate, stereo, and 20ms frame length, the number of sampling points is 960, and the byte count is 3840 = 960 * 2 * 2
> 

#### Return value description:

0: Success; <0: Error

## setLocalProcessedAudioFrameCallbackFormat

#### Sets the callback format for local audio frames after preprocessing

This interface is used to set the format of the AudioFrame callback for onLocalProcessedAudioFrame:
-  sampleRate: Sampling rate, supported values are 16000, 32000, 44100, 48000.

-  channel: Number of channels (if stereo, data is interleaved), mono: 1; stereo: 2.

-  samplesPerCall: Number of sampling points, Definition callback data frame length. The frame length must be an integer multiple of 10ms.

If you want to calculate the callback frame length in milliseconds, the formula to convert milliseconds to sampling points is: sampling points = milliseconds * sampling rate / 1000.

Example: For a 48000 sampling rate and a desired callback frame length of 20ms, the number of sampling points should be: 960 = 20 * 48000 / 1000.
| Parameters | Description |
| --- | --- |
| format | Audio Data Callback Format. |

> **Note**
> 

> The final callback frame length is in bytes. The formula to convert sampling points to bytes is: Byte Count = Sampling Points * Channels * 2 (Bit Width). Example: For a 48000 sampling rate, stereo, and 20ms frame length, the number of sampling points is 960, and the byte count is 3840 = 960 * 2 * 2
> 

#### Return value description:

0: Success; <0: Error

## setMixedPlayAudioFrameCallbackFormat

#### Sets the callback format for audio frames that will eventually be played by the system

This interface is used to set the format of the AudioFrame callback for onMixedPlayAudioFrame:
-  sampleRate: Sampling rate, supported values are 16000, 32000, 44100, 48000.

-  channel: Number of channels (if stereo, data is interleaved), mono: 1; stereo: 2.

-  samplesPerCall: Number of sampling points, Definition callback data frame length. The frame length must be an integer multiple of 10ms.

If you want to calculate the callback frame length in milliseconds, the formula to convert milliseconds to sampling points is: sampling points = milliseconds * sampling rate / 1000.

Example: For a 48000 sampling rate and a desired callback frame length of 20ms, the number of sampling points should be: 960 = 20 * 48000 / 1000.
| Parameters | Description |
| --- | --- |
| format | Audio Data Callback Format. |

> **Note**
> 

> The final callback frame length is in bytes. The formula to convert sampling points to bytes is: Byte Count = Sampling Points * Channels * 2 (Bit Width). Example: For a 48000 sampling rate, stereo, and 20ms frame length, the number of sampling points is 960, and the byte count is 3840 = 960 * 2 * 2
> 

#### Return value description:

0: Success; <0: Error

## enableCustomAudioRendering

#### Enable self-definition audio playback

If you need to connect specific audio devices or want to control the audio playback logic yourself, you can enable Custom Playback through this interface.

After enabling Custom Playback, the SDK will no longer use the system's audio interface to play data. You need to get the audio frame that the SDK wants to play through getCustomAudioRenderingFrame and play it yourself.
| Parameters | Description |
| --- | --- |
| enable | Whether to enable Custom Playback is off by default. |

> **Note**
> 

> You need to set it before entering the room for it to take effect. It is not supported to set it after entering the room.
> 

## getCustomAudioRenderingFrame

#### Get playable audio data

Before calling this interface, you need to enable Custom Playback through enableCustomAudioRendering first.

Parameter TRTCAudioFrame is recommended to be filled as follows (other fields do not need to be filled):
-  sampleRate: Sampling rate, required, supported values are 16000, 24000, 32000, 44100, 48000.

-  channel: Number of channels, required. Fill in 1 for mono, 2 for stereo. The data is interleaved for stereo.

-  data: Buffer for obtaining audio data. You need to allocate the memory size of data according to the frame length of an audio frame. The obtained PCM data supports frame lengths of 10ms or 20ms. It is recommended to use a frame length of 20ms.

Calculation formula: Sampling rate x Playback duration x Number of channels x 2 (bytes per sample). For example, for a frame of audio with a sampling rate of 48000, mono channel, and a playback duration of 20ms, the buffer size is 48000 × 0.02s × 1 × 16bit = 15360bit = 1920 bytes.
| Parameters | Description |
| --- | --- |
| audioFrame | Audio data frame. |

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

Other users in the room can receive messages through the onRecvCustomCmdMsg callback in TRTCCloudListener.
| Parameters | Description |
| --- | --- |
| cmdID | Message ID, the value range is 1 - 10. |
| data | Message to be sent, the maximum length of a single message is limited to 1KB. |
| ordered | Whether orderly sending is enabled, i.e., whether the order of data packets at the receiver matches the order at the sender (this will cause some reception delay). |
| reliable | Whether reliable transmission is enabled. Reliable transmission offers a higher success rate but will cause higher reception delays compared to unreliable transmission. |

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

Therefore, compared to sendCustomCmdMsg, signaling transmitted via the SEI channel has better compatibility: the signaling can be transmitted along with the video frame all the way to the live CDN.

However, because the data block in the video frame header cannot be too large, it is recommended to control the signaling size to just a few bytes when using this interface.

The most common usage is to embed a self-defined timestamp (timestamp) into the video frame using this interface to achieve perfect alignment of messages and screen (e.g., in educational scenarios for aligning courseware and video signals).

Other users in the room can receive messages through the onRecvSEIMsg callback in TRTCCloudListener.
| Parameters | Description |
| --- | --- |
| data | Data to be sent, which can contain up to 1 KB (1,000 bytes) of data |
| repeatCount | Number of data sends |

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
| Parameters | Description |
| --- | --- |
| params | Speed Test Options |

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
| Parameters | Description |
| --- | --- |
| level | Refer to TRTCLogLevel, default value: TRTCLogLevelNone |

## setConsoleEnabled

#### Enables/Disables console log print.
| Parameters | Description |
| --- | --- |
| enabled | Specify whether to enable it. Default: Disabled. |

## setLogCompressEnabled

#### Enables/Disables local log compression

After enabling compression, the log storage volume is significantly reduced, but you need to use a Python script provided by Tencent Cloud to decompress and read it.

After disabling compression, logs are stored in plaintext, which can be opened and read directly with Notepad but occupy more space.
| Parameters | Description |
| --- | --- |
| enabled | Specify whether to enable it. Default: Enabled |

## setLogDirPath

#### Sets the save path for local logs

This interface allows you to change the default storage path of SDK local logs. The default local log storage locations are:
-  Windows platform: C:/Users/[system username]/AppData/Roaming/liteav/log, i.e., %appdata%/liteav/log.

-  iOS or Mac platform: sandbox Documents/log.

-  Android platform: /app private directory/files/log/liteav/.

| Parameters | Description |
| --- | --- |
| path | Storage path for logs |

> **Note**
> 

> Make sure to call this before all other interfaces and ensure that the specified directory exists and that your application has read and write permissions for that directory.
> 

## setLogListener

#### Log callback

## showDebugView

#### Show Dashboard

The "Dashboard" is a semi-transparent debug information overlay located above the video rendering control, used to display audio and video information and event information, aiding in integration and debugging.
| Parameters | Description |
| --- | --- |
| showType | 0: Do not display; 1: Display simplified edition (audio and video information only); 2: Display full version (including audio and video information and event information). |

## TRTCViewMargin

#### Set the dashboard margin

Used to adjust the position of the dashboard within the video rendering control. Must be called before showDebugView to take effect.
| Parameters | Description |
| --- | --- |
| margin | Dashboard inner padding. Note that here it is based on the percentage of the parentView. Margin value range is 0 - 1. |
| userId | User ID. |

## callExperimentalAPI

#### Calls an experimental API.

## enablePayloadPrivateEncryption

#### Enable or disable media stream private encryption

In scenarios with high security requirements, TRTC recommends calling the enablePayloadPrivateEncryption method to enable media stream private encryption before joining a room.

After the user leaves the room, the SDK will automatically disable private encryption. If you need to re-enable private encryption, you must call this method before the user rejoins the room.
| Parameters | Description |
| --- | --- |
| config | For configuring the media stream private encryption algorithm and key, refer to TRTCPayloadPrivateEncryptionConfig. |
| enabled | Whether to enable media stream private encryption. |

> **Note**
> 

> TRTC already encrypts media streams before transmission. When media stream private encryption is enabled, it will use the key and initialization vector you provided for additional encryption.
> 

#### Return value description:

API invocation results: 0: Method call successful, -1: Invalid input parameter, -2: Feature expired. To unlock: Please visit the Chinese mainland site to activate the [TRTC Enterprise Edition Package](https://buy.cloud.tencent.com/trtc?tab=month&trtcversion=ultimate), and submit an [application](https://cloud.tencent.com/apply/p/diifjcmffhw). You can use it upon approval.