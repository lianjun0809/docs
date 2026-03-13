> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

# TRTC SDK Documentation
## Feature Overview
`TXDeviceManager.java` provides audio and video device management for the TRTC (Real-Time Communication) SDK on Android. Use this module to control hardware devices such as cameras, microphones, and speakers.

## TXDeviceManager
| Function List | Description |
| --- | --- |
| isFrontCamera | Determine whether the current camera is front-facing (only for mobile terminal) |
| switchCamera | Switch between front and rear cameras (only for mobile terminal) |
| getCameraZoomMaxRatio | Get the maximum zoom level of the camera (only for mobile terminal) |
| setCameraZoomRatio | Set the zoom level of the camera (only for mobile terminal) |
| isAutoFocusEnabled | Check if automatic face position recognition is supported (only for mobile terminal) |
| enableCameraAutoFocus | Enable autofocus feature (only for mobile terminal) |
| setCameraFocusPosition | Set the focus position of the camera (only for mobile terminal) |
| enableCameraTorch | Turn the flash on/off, also known as flashlight mode (only for mobile terminal) |
| setAudioRoute | Set audio routing (only for mobile terminal) |
| setExposureCompensation | Set the exposure parameters of the camera, ranging from -1 to 1 |
| setCameraCapturerParam | Set camera capture preferences |
| setSystemVolumeType | Set system volume type (only for mobile terminal) |

## Struct Type
| Function List | Description |
| --- | --- |
| TXCameraCaptureParam | Camera collection parameters |

## Enumeration Types
| Enumeration Types | Description |
| --- | --- |
| TXSystemVolumeType | System Volume Type (Only applicable to mobile devices) |
| TXAudioRoute | Audio routing (i.e., the sound playback mode) |
| TXCameraCaptureMode | Camera capture preferences |

## isFrontCamera

#### Determine whether the current camera is front-facing (only for mobile terminal)

## switchCamera

#### Switch between front and rear cameras (only for mobile terminal)

## getCameraZoomMaxRatio

#### Get the maximum zoom level of the camera (only for mobile terminal)

## setCameraZoomRatio

#### Set the zoom level of the camera (only for mobile terminal)
| Parameters | Description |
| --- | --- |
| zoomRatio | Value range 1 - 5, with 1 representing the farthest view (normal lens) and 5 representing the closest view (magnifier lens). The recommended maximum value is 5; exceeding 5 may cause video data to become blurry. |

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
| Parameters | Description |
| --- | --- |
| position | Focus position, please pass the coordinates of the desired focus point |

> **Note**
> 

> The prerequisite for using this interface is to disable the auto-focus feature through enableCameraAutoFocus.
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

## setExposureCompensation

#### Set the exposure parameters of the camera, ranging from -1 to 1

## setCameraCapturerParam

#### Set camera capture preferences

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
| Enumeration | Value | Description |
| --- | --- | --- |
| TXSystemVolumeTypeAuto | Not Defined | Automatic Switching Mode |
| TXSystemVolumeTypeMedia | Not Defined | Full Media Volume |
| TXSystemVolumeTypeVOIP | Not Defined | Full Call Volume |

## TXAudioRoute

#### Audio routing (i.e., the sound playback mode)

Audio routing, that is, whether the sound is played through the phone's speaker or earpiece. Therefore, this interface is only applicable to mobile devices.

A mobile phone has two speakers: one is the earpiece located at the top of the phone, and the other is the stereo speaker located at the bottom.
-  When the audio routing is set to the earpiece, the sound is relatively low, and you need to bring your ear close to hear it clearly, ensuring better privacy. It is suitable for phone calls.

-  When the audio routing is set to the speaker, the sound is relatively loud. You can hear it clearly without holding the phone to your face, thus enabling the "hands-free" feature.

| Enumeration | Value | Description |
| --- | --- | --- |
| TXAudioRouteSpeakerphone | Not Defined | Speakerphone: Play sound through the speaker (i.e., "hands-free"), which is located at the bottom of the phone. The volume tends to be loud, suitable for playing music out loud. |
| TXAudioRouteEarpiece | Not Defined | Earpiece: Plays through the earpiece, the earpiece is located at the top of the phone, the sound is small, suitable for privacy-protected call scenarios. |

## TXCameraCaptureMode

#### Camera capture preferences

This enumeration type is used for camera collection parameter settings.
| Enumeration | Value | Description |
| --- | --- | --- |
| TXCameraResolutionStrategyAuto | Not Defined | Auto-adjust collection parameters. The SDK selects appropriate camera output parameters based on the performance of the actual capture device and network conditions, maintaining a balance between device performance and video preview quality. |
| TXCameraResolutionStrategyPerformance | Not Defined | Prioritize device performance. The SDK selects the closest camera output parameters based on the encoder resolution and frame rate set by the user, thus ensuring device performance. |
| TXCameraResolutionStrategyHighQuality | Not Defined | Priority is given to ensuring video preview quality. The SDK selects higher camera output parameters to improve the quality of preview video. In this case, more CPU and memory will be consumed for video preprocessing. |
| TXCameraCaptureManual | Not Defined | Users are allowed to set the video aspect ratio captured by the local camera. |

## TXCameraCaptureParam

#### Camera collection parameters

This setting determines the image quality of the local preview.
| Enumeration Types | Description |
| --- | --- |
| height | **Field Definition:** Captured Image Width |
| mode | **Field Definition:** Camera Capture Preferences, refer to TXCameraCaptureMode |
| width | **Field Definition:** Captured Image Length |
