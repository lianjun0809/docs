> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

# TRTC SDK Documentation
## Feature Overview
`ITXBeautyManager.h` provides audio and video device management for the TRTC (Real-Time Communication) SDK on C++. Use this module to control hardware devices such as cameras, microphones, and speakers.


## ITXDeviceManager
<table>
<tr>
<td rowspan="1" colSpan="1" >Function List</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[isFrontCamera](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >Determine whether the current camera is front-facing (only for mobile terminal)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[switchCamera](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >Switch between front and rear cameras (only for mobile terminal)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getCameraZoomMaxRatio](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >Get the maximum zoom level of the camera (only for mobile terminal)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setCameraZoomRatio](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >Set the zoom level of the camera (only for mobile terminal)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[isAutoFocusEnabled](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >Check if automatic face position recognition is supported (only for mobile terminal)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[enableCameraAutoFocus](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >Enable autofocus feature (only for mobile terminal)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setCameraFocusPosition](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >Set the focus position of the camera (only for mobile terminal)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[enableCameraTorch](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >Turn the flash on/off, also known as flashlight mode (only for mobile terminal)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setAudioRoute](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >Set audio routing (only for mobile terminal)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getDevicesList](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >Get the device list (only for desktop terminal)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setCurrentDevice](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >Set the current device to use (only for desktop terminal)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getCurrentDevice](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >Get the current device in use (only for desktop terminal)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setCurrentDeviceVolume](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >Set the current device volume (only for desktop terminal)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getCurrentDeviceVolume](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >Get the current device volume (only for desktop terminal)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setCurrentDeviceMute](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >Set the mute status of the current device (only for desktop terminal)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getCurrentDeviceMute](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >Get the mute status of the current device (only for desktop terminal)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[enableFollowingDefaultAudioDevice](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >Set SDK to use the audio device according to the default system device (only for desktop terminal)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[startCameraDeviceTest](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >Start camera testing (only for desktop terminal)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[stopCameraDeviceTest](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >End camera testing (only for desktop terminal)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[startMicDeviceTest](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >Start mic testing (only for desktop terminal)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[startMicDeviceTest](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >Start mic testing (only for desktop terminal)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[stopMicDeviceTest](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >End mic testing (only for desktop terminal)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[startSpeakerDeviceTest](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >Start speaker testing (only for desktop terminal)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[stopSpeakerDeviceTest](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >End speaker testing (only for desktop terminal)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[startCameraDeviceTest](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >Start camera testing (only for desktop terminal)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setApplicationPlayVolume](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >Set the volume of the current process in the Windows system volume synthesizer (only applicable for Windows system)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getApplicationPlayVolume](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >Get the volume of the current process in the Windows system volume synthesizer (only applicable for Windows system)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setApplicationMuteState](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >Set the mute status of the current process in the Windows system volume synthesizer (only applicable for Windows system)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getApplicationMuteState](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >Get the mute status of the current process in the Windows system volume synthesizer (only applicable for Windows system)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setCameraCapturerParam](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >Set camera capture preferences</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setDeviceObserver](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >Set onDeviceChanged event callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setSystemVolumeType](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >Set system volume type (only for mobile terminal)</td>
</tr>
</table>


## Struct Type
<table>
<tr>
<td rowspan="1" colSpan="1" >Function List</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[TXCameraCaptureParam](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >Camera collection parameters</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[ITXDeviceInfo](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >Information related to audio and video equipment (only for desktop platform)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[ITXDeviceCollection](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >Device Information List (only for desktop platform)</td>
</tr>
</table>


## Enumeration Types
<table>
<tr>
<td rowspan="1" colSpan="1" >Enumeration Types</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[TXSystemVolumeType](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >System Volume Type (Only applicable to mobile devices)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[TXAudioRoute](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >Audio routing (i.e., the sound playback mode)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[TXMediaDeviceType](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >Device type (only for desktop platform)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[TXMediaDeviceState](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >Device operations</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[TXCameraCaptureMode](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >Camera capture preferences</td>
</tr>
</table>


## isFrontCamera



#### Determine whether the current camera is front-facing (only for mobile terminal)

## switchCamera



#### Switch between front and rear cameras (only for mobile terminal)

## getCameraZoomMaxRatio



#### Get the maximum zoom level of the camera (only for mobile terminal)

## setCameraZoomRatio



#### Set the zoom level of the camera (only for mobile terminal)
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >zoomRatio</td>

<td rowspan="1" colSpan="1" >Value range 1 - 5, with 1 representing the farthest view (normal lens) and 5 representing the closest view (magnifier lens). The recommended maximum value is 5; exceeding 5 may cause video data to become blurry.</td>
</tr>
</table>


## isAutoFocusEnabled



#### Check if automatic face position recognition is supported (only for mobile terminal)

## enableCameraAutoFocus



#### Enable autofocus feature (only for mobile terminal)

Once enabled, the SDK will automatically detect the face position in the frame and keep the camera focus on the face position.

## setCameraFocusPosition



#### Set the focus position of the camera (only for mobile terminal)

You can achieve the following interactions with this interface:

1. Allow users to click on the local camera preview screen.

2. Display a rectangular box at the click position to indicate that the camera will focus on this point.

3. Then, pass the coordinates of the user's click position through this interface to the SDK. The SDK will control the camera to focus on the user's desired location.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >position</td>

<td rowspan="1" colSpan="1" >Focus position, please pass the coordinates of the desired focus point</td>
</tr>
</table>


> **Note**
> 

> The prerequisite for using this interface is to disable the auto-focus feature through [enableCameraAutoFocus](https://write.woa.com/document/87030115247763456).
> 


#### Return value description:

0: Operation successful; Negative value: Operation failed.

## enableCameraTorch



#### Turn the flash on/off, also known as flashlight mode (only for mobile terminal)

## setAudioRoute



#### Set audio routing (only for mobile terminal)

A phone has two audio playback devices: one is the earpiece at the top of the phone, and the other is the stereo speaker at the bottom of the phone.

When the audio routing is set to the earpiece, the sound is relatively low, and you need to bring your ear close to hear it clearly, ensuring better privacy. It is suitable for phone calls.

When the audio routing is set to the speaker, the sound is relatively loud. You can hear it clearly without holding the phone to your face, thus enabling the "hands-free" feature.

## getDevicesList



#### Get the device list (only for desktop terminal)
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >type</td>

<td rowspan="1" colSpan="1" >Device type, specify which type of device list to retrieve. See TXMediaDeviceType Definition for details.</td>
</tr>
</table>


> **Note**
> 
> -  After use, please call the release method to release resources so that the SDK can maintain the lifecycle of the ITXDeviceCollection object.
> -  Do not use delete to release the returned Collection object. Deleting the ITXDeviceCollection* pointer will cause an abnormal crash.
> -  type only supports TXMediaDeviceTypeMic, TXMediaDeviceTypeSpeaker, TXMediaDeviceTypeCamera.
> -  This interface only supports Mac and Windows platforms.


## setCurrentDevice



#### Set the current device to use (only for desktop terminal)
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >deviceId</td>

<td rowspan="1" colSpan="1" >Device ID, you can obtain the device ID through the [getDevicesList](https://write.woa.com/document/87030115247763456) interface.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >type</td>

<td rowspan="1" colSpan="1" >Device type, see TXMediaDeviceType Definition for details.</td>
</tr>
</table>


#### Return value description:

0: Operation successful; Negative value: Operation failed.

## getCurrentDevice



#### Get the current device in use (only for desktop terminal)

## setCurrentDeviceVolume



#### Set the current device volume (only for desktop terminal)

The volume here refers to the capture volume of the microphone or the playback volume of the speaker. The camera does not support setting the volume.
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


## getCurrentDeviceVolume



#### Get the current device volume (only for desktop terminal)

The volume here refers to the capture volume of the microphone or the playback volume of the speaker. The camera does not support retrieving the volume.

## setCurrentDeviceMute



#### Set the mute status of the current device (only for desktop terminal)

The volume here refers to the microphone and speaker, and the camera does not support silent operation.

## getCurrentDeviceMute



#### Get the mute status of the current device (only for desktop terminal)

The volume here refers to the microphone and speaker, and the camera does not support silent operation.

## enableFollowingDefaultAudioDevice



#### Set SDK to use the audio device according to the default system device (only for desktop terminal)

Only microphone and speaker types are supported. The camera does not yet support following the system default device
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enable</td>

<td rowspan="1" colSpan="1" >Whether to follow the system default audio device.<br>-  true: Follow. When the system default audio device changes or a new audio device is plugged in, the SDK will immediately switch the audio device.<br>-  false: Do not follow. When the system default audio device changes or a new audio device is plugged in, the SDK will not switch the audio device.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >type</td>

<td rowspan="1" colSpan="1" >Device type, see TXMediaDeviceType Definition for details.</td>
</tr>
</table>


## startCameraDeviceTest



#### Start camera testing (only for desktop terminal)

> **Note**
> 

> During testing, you can use the [setCurrentDevice](https://write.woa.com/document/87030115247763456) interface to switch cameras.
> 


## stopCameraDeviceTest



#### End camera testing (only for desktop terminal)

## startMicDeviceTest



#### Start mic testing (only for desktop terminal)

This interface can test whether the microphone is working properly. The volume of the microphone's audio stream will be notified to you via callback, with the volume range being 0 to 100.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >interval</td>

<td rowspan="1" colSpan="1" >Microphone volume callback interval.</td>
</tr>
</table>


> **Note**
> 

> After invoking this interface, the recorded microphone sound will be played back through the speaker by default.
> 


## startMicDeviceTest



#### Start mic testing (only for desktop terminal)

This interface can test whether the microphone is working properly. The volume of the microphone's audio stream will be notified to you via callback, with the volume range being 0 to 100.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >interval</td>

<td rowspan="1" colSpan="1" >Microphone volume callback interval.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >playback</td>

<td rowspan="1" colSpan="1" >Whether to enable microphone sound playback. When enabled, users will hear their own voice during microphone testing.</td>
</tr>
</table>


## stopMicDeviceTest



#### End mic testing (only for desktop terminal)

## startSpeakerDeviceTest



#### Start speaker testing (only for desktop terminal)

This interface tests the playback device by playing a specified audio file. If the user hears sound during the test, it means the playback device is working properly.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >filePath</td>

<td rowspan="1" colSpan="1" >Path to the audio file</td>
</tr>
</table>


## stopSpeakerDeviceTest



#### End speaker testing (only for desktop terminal)

## startCameraDeviceTest



#### Start camera testing (only for desktop terminal)

This interface supports custom rendering, which means you can take over the camera's rendered image by connecting to the ITRTCVideoRenderCallback Callback Interface.

## setApplicationPlayVolume



#### Set the volume of the current process in the Windows system volume synthesizer (only applicable for Windows system)

## getApplicationPlayVolume



#### Get the volume of the current process in the Windows system volume synthesizer (only applicable for Windows system)

## setApplicationMuteState



#### Set the mute status of the current process in the Windows system volume synthesizer (only applicable for Windows system)

## getApplicationMuteState



#### Get the mute status of the current process in the Windows system volume synthesizer (only applicable for Windows system)

## setCameraCapturerParam



#### Set camera capture preferences

## setDeviceObserver



#### Set onDeviceChanged event callback

## setSystemVolumeType



#### Set system volume type (only for mobile terminal)

@deprecated Not recommended starting from version 9.5. It is advised to use the startLocalAudio(quality) interface in ` TRTCCloud ` as a replacement, and decide the sound quality via the quality parameter.

## TXSystemVolumeType(Deprecated)



#### System Volume Type (Only applicable to mobile devices)

@deprecated Not recommended starting from version 9.5.



Modern smartphones generally have two types of system volume: "Call Volume" and "Media Volume".
-  Call Volume: A volume type designed specifically for making and receiving phone calls, featuring built-in echo cancellation (AEC), and supporting microphone input via Bluetooth headphones. However, the sound quality is relatively average.


If you press the volume button on the side of your phone to lower the volume and it cannot be set to zero (completely silent), it indicates that your phone is currently in Call Volume mode.
-  Media Volume: A volume type designed specifically for music scenarios, which cannot use the system's AEC feature, and does not support microphone input via Bluetooth headphones, but provides better music playback quality.


If you press the volume button on the side of your phone to lower the volume and it can be set to completely silent, it indicates that your phone is currently in Media Volume mode.



The SDK currently offers three control modes for system volume types: Automatic Switching Mode, Full Call Volume Mode, Full Media Volume Mode.
<table>
<tr>
<td rowspan="1" colSpan="1" >Enumeration</td>

<td rowspan="1" colSpan="1" >Value</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXSystemVolumeTypeAuto</td>

<td rowspan="1" colSpan="1" >0</td>

<td rowspan="1" colSpan="1" >Automatic Switching Mode</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXSystemVolumeTypeMedia</td>

<td rowspan="1" colSpan="1" >1</td>

<td rowspan="1" colSpan="1" >Full Media Volume</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXSystemVolumeTypeVOIP</td>

<td rowspan="1" colSpan="1" >2</td>

<td rowspan="1" colSpan="1" >Full Call Volume</td>
</tr>
</table>


## TXAudioRoute



#### Audio routing (i.e., the sound playback mode)

Audio routing, that is, whether the sound is played through the phone's speaker or earpiece. Therefore, this interface is only applicable to mobile devices.

A mobile phone has two speakers: one is the earpiece located at the top of the phone, and the other is the stereo speaker located at the bottom.
-  When the audio routing is set to the earpiece, the sound is relatively low, and you need to bring your ear close to hear it clearly, ensuring better privacy. It is suitable for phone calls.

-  When the audio routing is set to the speaker, the sound is relatively loud. You can hear it clearly without holding the phone to your face, thus enabling the "hands-free" feature.

<table>
<tr>
<td rowspan="1" colSpan="1" >Enumeration</td>

<td rowspan="1" colSpan="1" >Value</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXAudioRouteSpeakerphone</td>

<td rowspan="1" colSpan="1" >0</td>

<td rowspan="1" colSpan="1" >Speakerphone: Play sound through the speaker (i.e., "hands-free"), which is located at the bottom of the phone. The volume tends to be loud, suitable for playing music out loud.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXAudioRouteEarpiece</td>

<td rowspan="1" colSpan="1" >1</td>

<td rowspan="1" colSpan="1" >Earpiece: Plays through the earpiece, the earpiece is located at the top of the phone, the sound is small, suitable for privacy-protected call scenarios.</td>
</tr>
</table>


## TXMediaDeviceType



#### Device type (only for desktop platform)



This enumeration value is used for the three types of audio and video devices in Definition: camera, microphone, and speaker, allowing a single device management interface to control different types of devices.
<table>
<tr>
<td rowspan="1" colSpan="1" >Enumeration</td>

<td rowspan="1" colSpan="1" >Value</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXMediaDeviceTypeUnknown</td>

<td rowspan="1" colSpan="1" >-1</td>

<td rowspan="1" colSpan="1" >Undefined device type</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXMediaDeviceTypeMic</td>

<td rowspan="1" colSpan="1" >0</td>

<td rowspan="1" colSpan="1" >Microphone-type device</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXMediaDeviceTypeSpeaker</td>

<td rowspan="1" colSpan="1" >1</td>

<td rowspan="1" colSpan="1" >Speaker-type device</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXMediaDeviceTypeCamera</td>

<td rowspan="1" colSpan="1" >2</td>

<td rowspan="1" colSpan="1" >Camera-type device</td>
</tr>
</table>


## TXMediaDeviceState



#### Device operations

This enumerated value is used for local equipment status change notification onDeviceChanged.
<table>
<tr>
<td rowspan="1" colSpan="1" >Enumeration</td>

<td rowspan="1" colSpan="1" >Value</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXMediaDeviceStateAdd</td>

<td rowspan="1" colSpan="1" >0</td>

<td rowspan="1" colSpan="1" >Device inserted</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXMediaDeviceStateRemove</td>

<td rowspan="1" colSpan="1" >1</td>

<td rowspan="1" colSpan="1" >Device removed</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXMediaDeviceStateActive</td>

<td rowspan="1" colSpan="1" >2</td>

<td rowspan="1" colSpan="1" >Device enabled</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXMediaDefaultDeviceChanged</td>

<td rowspan="1" colSpan="1" >3</td>

<td rowspan="1" colSpan="1" >System default device changed</td>
</tr>
</table>


## TXCameraCaptureMode



#### Camera capture preferences

This enumeration type is used for camera collection parameter settings.
<table>
<tr>
<td rowspan="1" colSpan="1" >Enumeration</td>

<td rowspan="1" colSpan="1" >Value</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXCameraResolutionStrategyAuto</td>

<td rowspan="1" colSpan="1" >0</td>

<td rowspan="1" colSpan="1" >Auto-adjust collection parameters.<br>The SDK selects appropriate camera output parameters based on the performance of the actual capture device and network conditions, maintaining a balance between device performance and video preview quality.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXCameraResolutionStrategyPerformance</td>

<td rowspan="1" colSpan="1" >1</td>

<td rowspan="1" colSpan="1" >Prioritize device performance.<br>The SDK selects the closest camera output parameters based on the encoder resolution and frame rate set by the user, thus ensuring device performance.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXCameraResolutionStrategyHighQuality</td>

<td rowspan="1" colSpan="1" >2</td>

<td rowspan="1" colSpan="1" >Priority is given to ensuring video preview quality.<br>The SDK selects higher camera output parameters to improve the quality of preview video. In this case, more CPU and memory will be consumed for video preprocessing.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXCameraCaptureManual</td>

<td rowspan="1" colSpan="1" >3</td>

<td rowspan="1" colSpan="1" >Users are allowed to set the video aspect ratio captured by the local camera.</td>
</tr>
</table>


## TXCameraCaptureParam



#### Camera collection parameters

This setting determines the image quality of the local preview.
<table>
<tr>
<td rowspan="1" colSpan="1" >Enumeration Types</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >height</td>

<td rowspan="1" colSpan="1" >**Field Definition:** Captured Image Width</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >mode</td>

<td rowspan="1" colSpan="1" >**Field Definition:** Camera Capture Preferences, refer to [TXCameraCaptureMode](https://write.woa.com/document/87030115247763456)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >width</td>

<td rowspan="1" colSpan="1" >**Field Definition:** Captured Image Length</td>
</tr>
</table>


## TXMediaDeviceInfo



#### Information related to audio and video equipment (only for desktop platform)

This structure is used to describe key information of an audio and video device, such as Device ID, Device Name, etc., so that users can select their desired audio and video device in the user interface.
<table>
<tr>
<td rowspan="1" colSpan="1" >Enumeration Types</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >getDeviceName()</td>

<td rowspan="1" colSpan="1" >Device Name (UTF-8)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >getDevicePID()</td>

<td rowspan="1" colSpan="1" >Device ID (UTF-8)</td>
</tr>
</table>


## ITXDeviceCollection



#### Device Information List (only for desktop platform)

This structure functions similarly to std::vector<ITXDeviceInfo>, used to solve binary compatibility issues with different versions of STL containers.
<table>
<tr>
<td rowspan="1" colSpan="1" >Enumeration Types</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >getCount()</td>

<td rowspan="1" colSpan="1" >Number of Devices</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >index)</td>

<td rowspan="1" colSpan="1" >Device Information (JSON Format)<br>**Note**<br>Example: {"SupportedResolution":[{"width":640,"height":480},{"width":320,"height":240}]}<br>param index Device Index, value is [0,getCount). Return JSON Format Device Information<br></td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >release()</td>

<td rowspan="1" colSpan="1" >Release Device List, please do not use delete to release resources!!!</td>
</tr>
</table>
