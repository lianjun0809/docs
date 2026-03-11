> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

# 腾讯云实时音视频(TRTC SDK )文档

## 概述
`ITXDeviceManager.h` 是腾讯云实时音视频(TRTC SDK ) C++ 的音视频设备管理模块文档，用于管理摄像头、麦克风和扬声器等音视频相关的硬件设备。


## ITXDeviceManager
<table>
<tr>
<td rowspan="1" colSpan="1" >函数列表</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[isFrontCamera](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >判断当前是否为前置摄像头（仅适用于移动端）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[switchCamera](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >切换前置或后置摄像头（仅适用于移动端）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getCameraZoomMaxRatio](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >获取摄像头的最大缩放倍数（仅适用于移动端）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setCameraZoomRatio](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >设置摄像头的缩放倍数（仅适用于移动端）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[isAutoFocusEnabled](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >查询是否支持自动识别人脸位置（仅适用于移动端）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[enableCameraAutoFocus](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >开启自动对焦功能（仅适用于移动端）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setCameraFocusPosition](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >设置摄像头的对焦位置（仅适用于移动端）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[enableCameraTorch](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >开启/关闭闪光灯，也就是手电筒模式（仅适用于移动端）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setAudioRoute](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >设置音频路由（仅适用于移动端）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getDevicesList](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >获取设备列表（仅适用于桌面端）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setCurrentDevice](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >设置当前要使用的设备（仅适用于桌面端）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getCurrentDevice](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >获取当前正在使用的设备（仅适用于桌面端）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setCurrentDeviceVolume](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >设置当前设备的音量（仅适用于桌面端）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getCurrentDeviceVolume](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >获取当前设备的音量（仅适用于桌面端）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setCurrentDeviceMute](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >设置当前设备的静音状态（仅适用于桌面端）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getCurrentDeviceMute](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >获取当前设备的静音状态（仅适用于桌面端）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[enableFollowingDefaultAudioDevice](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >设置 SDK 使用的音频设备根据跟随系统默认设备（仅适用于桌面端）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[startCameraDeviceTest](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >开始摄像头测试（仅适用于桌面端）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[stopCameraDeviceTest](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >结束摄像头测试（仅适用于桌面端）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[startMicDeviceTest](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >开始麦克风测试（仅适用于桌面端）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[startMicDeviceTest](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >开始麦克风测试（仅适用于桌面端）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[stopMicDeviceTest](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >结束麦克风测试（仅适用于桌面端）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[startSpeakerDeviceTest](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >开始扬声器测试（仅适用于桌面端）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[stopSpeakerDeviceTest](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >结束扬声器测试（仅适用于桌面端）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[startCameraDeviceTest](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >开始摄像头测试（仅适用于桌面端）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setApplicationPlayVolume](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >设置 Windows 系统音量合成器中当前进程的音量（仅适用于 Windows 系统）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getApplicationPlayVolume](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >获取 Windows 系统音量合成器中当前进程的音量（仅适用于 Windows 系统）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setApplicationMuteState](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >设置 Windows 系统音量合成器中当前进程的静音状态（仅适用于 Windows 系统）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getApplicationMuteState](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >获取 Windows 系统音量合成器中当前进程的静音状态（仅适用于 Windows 系统）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setCameraCapturerParam](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >设置摄像头采集偏好。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setDeviceObserver](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >设置 onDeviceChanged 事件回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setSystemVolumeType](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >设置系统音量类型（仅适用于移动端）。</td>
</tr>
</table>


## 结构体类型
<table>
<tr>
<td rowspan="1" colSpan="1" >函数列表</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[TXCameraCaptureParam](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >摄像头采集参数。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[ITXDeviceInfo](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >音视频设备的相关信息（仅适用于桌面平台）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[ITXDeviceCollection](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >设备信息列表（仅适用于桌面平台）。</td>
</tr>
</table>


## 枚举类型
<table>
<tr>
<td rowspan="1" colSpan="1" >枚举类型</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[TXSystemVolumeType](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >系统音量类型（仅适用于移动设备）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[TXAudioRoute](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >音频路由（即声音的播放模式）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[TXMediaDeviceType](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >设备类型（仅适用于桌面平台）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[TXMediaDeviceState](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >设备操作。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[TXCameraCaptureMode](https://write.woa.com/document/87030115247763456)</td>

<td rowspan="1" colSpan="1" >摄像头采集偏好。</td>
</tr>
</table>


## isFrontCamera



#### 判断当前是否为前置摄像头（仅适用于移动端）。

## switchCamera



#### 切换前置或后置摄像头（仅适用于移动端）。

## getCameraZoomMaxRatio



#### 获取摄像头的最大缩放倍数（仅适用于移动端）。

## setCameraZoomRatio



#### 设置摄像头的缩放倍数（仅适用于移动端）。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >zoomRatio</td>

<td rowspan="1" colSpan="1" >取值范围 [1, 5]，取值为1表示最远视角（正常镜头），取值为5表示最近视角（放大镜头）。最大值推荐为5，若超过5，视频数据会变得模糊不清。</td>
</tr>
</table>


## isAutoFocusEnabled



#### 查询是否支持自动识别人脸位置（仅适用于移动端）。

## enableCameraAutoFocus



#### 开启自动对焦功能（仅适用于移动端）。

开启后，SDK 会自动检测画面中的人脸位置，并将摄像头的焦点始终对焦在人脸位置上。

## setCameraFocusPosition



#### 设置摄像头的对焦位置（仅适用于移动端）。

您可以通过该接口实现如下交互：

1. 在本地摄像头的预览画面上，允许用户单击操作。

2. 在用户的单击位置显示一个矩形方框，以示摄像头会在此处对焦。

3. 随后将用户点击位置的坐标通过本接口传递给 SDK，之后 SDK 会操控摄像头按照用户期望的位置进行对焦。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >position</td>

<td rowspan="1" colSpan="1" >对焦位置，请传入期望对焦点的坐标值</td>
</tr>
</table>


> **注意**
> 

> 使用该接口的前提是先通过 [enableCameraAutoFocus](https://write.woa.com/document/87030115247763456) 关闭自动对焦功能。
> 


#### 返回值说明：

0：操作成功；负数：操作失败。

## enableCameraTorch



#### 开启/关闭闪光灯，也就是手电筒模式（仅适用于移动端）。

## setAudioRoute



#### 设置音频路由（仅适用于移动端）。

手机有两个音频播放设备：一个是位于手机顶部的听筒，一个是位于手机底部的立体声扬声器。

设置音频路由为听筒时，声音比较小，只有将耳朵凑近才能听清楚，隐私性较好，适合用于接听电话。

设置音频路由为扬声器时，声音比较大，不用将手机贴脸也能听清，因此可以实现“免提”的功能。

## getDevicesList



#### 获取设备列表（仅适用于桌面端）。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >type</td>

<td rowspan="1" colSpan="1" >设备类型，指定需要获取哪种设备的列表。详见 [TXMediaDeviceType](https://write.woa.com/document/87030115247763456) 定义。</td>
</tr>
</table>


> **注意**
> 
> -  使用完毕后请调用 release 方法释放资源，这样可以让 SDK 维护 ITXDeviceCollection 对象的生命周期。
> -  不要使用 delete 释放返回的 Collection 对象，` delete ITXDeviceCollection* ` 指针会导致异常崩溃。
> -  type 只支持 ` TXMediaDeviceTypeMic `、` TXMediaDeviceTypeSpeaker `、` TXMediaDeviceTypeCamera `。
> -  此接口只支持 Mac 和 Windows 平台。


## setCurrentDevice



#### 设置当前要使用的设备（仅适用于桌面端）。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >deviceId</td>

<td rowspan="1" colSpan="1" >设备ID，您可以通过接口 [getDevicesList](https://write.woa.com/document/87030115247763456) 获得设备 ID。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >type</td>

<td rowspan="1" colSpan="1" >设备类型，详见 TXMediaDeviceType 定义。</td>
</tr>
</table>


#### 返回值说明：

0：操作成功；负数：操作失败。

## getCurrentDevice



#### 获取当前正在使用的设备（仅适用于桌面端）。

## setCurrentDeviceVolume



#### 设置当前设备的音量（仅适用于桌面端）。

这里的音量指的是麦克风的采集音量或者扬声器的播放音量，摄像头是不支持设置音量的。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >volume</td>

<td rowspan="1" colSpan="1" >音量大小，取值范围为 [0, 100]，默认值：100。</td>
</tr>
</table>


## getCurrentDeviceVolume



#### 获取当前设备的音量（仅适用于桌面端）。

这里的音量指的是麦克风的采集音量或者扬声器的播放音量，摄像头是不支持获取音量的。

## setCurrentDeviceMute



#### 设置当前设备的静音状态（仅适用于桌面端）。

这里的音量指的是麦克风和扬声器，摄像头是不支持静音操作的。

## getCurrentDeviceMute



#### 获取当前设备的静音状态（仅适用于桌面端）。

这里的音量指的是麦克风和扬声器，摄像头是不支持静音操作的。

## enableFollowingDefaultAudioDevice



#### 设置 SDK 使用的音频设备根据跟随系统默认设备（仅适用于桌面端）。

仅支持设置麦克风和扬声器类型，摄像头暂不支持跟随系统默认设备
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enable</td>

<td rowspan="1" colSpan="1" >是否跟随系统默认的音频设备。<br>-  true：跟随。当系统默认音频设备发生改变或者有新音频设备插入时，SDK 立即切换音频设备。<br>-  false：不跟随。当系统默认音频设备发生改变或者有新音频设备插入时，SDK 不会切换音频设备。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >type</td>

<td rowspan="1" colSpan="1" >设备类型，详见 [TXMediaDeviceType](https://write.woa.com/document/87030115247763456) 定义。</td>
</tr>
</table>


## startCameraDeviceTest



#### 开始摄像头测试（仅适用于桌面端）。

> **注意**
> 

> 在测试过程中可以使用 [setCurrentDevice](https://write.woa.com/document/87030115247763456) 接口切换摄像头。
> 


## stopCameraDeviceTest



#### 结束摄像头测试（仅适用于桌面端）。

## startMicDeviceTest



#### 开始麦克风测试（仅适用于桌面端）。

该接口可以测试麦克风是否能正常工作，测试到的麦克风采集音量的大小，会以回调的形式通知给您，其中 volume 的取值范围为 [0, 100]。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >interval</td>

<td rowspan="1" colSpan="1" >麦克风音量的回调间隔。</td>
</tr>
</table>


> **注意**
> 

> 该接口调用后默认会回播麦克风录制到的声音到扬声器中。
> 


## startMicDeviceTest



#### 开始麦克风测试（仅适用于桌面端）。

该接口可以测试麦克风是否能正常工作，测试到的麦克风采集音量的大小，会以回调的形式通知给您，其中 volume 的取值范围为 [0, 100]。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >interval</td>

<td rowspan="1" colSpan="1" >麦克风音量的回调间隔。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >playback</td>

<td rowspan="1" colSpan="1" >是否开启回播麦克风声音，开启后用户测试麦克风时会听到自己的声音。</td>
</tr>
</table>


## stopMicDeviceTest



#### 结束麦克风测试（仅适用于桌面端）。

## startSpeakerDeviceTest



#### 开始扬声器测试（仅适用于桌面端）。

该接口通过播放指定的音频文件，用于测试播放设备是否能正常工作。如果用户在测试时能听到声音，说明播放设备能正常工作。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >filePath</td>

<td rowspan="1" colSpan="1" >声音文件的路径</td>
</tr>
</table>


## stopSpeakerDeviceTest



#### 结束扬声器测试（仅适用于桌面端）。

## startCameraDeviceTest



#### 开始摄像头测试（仅适用于桌面端）。

该接口支持自定义渲染，即您可以通过接 [ITRTCVideoRenderCallback](https://write.woa.com/document/87030021158866944) 回调接口接管摄像头的渲染画面。

## setApplicationPlayVolume



#### 设置 Windows 系统音量合成器中当前进程的音量（仅适用于 Windows 系统）。

## getApplicationPlayVolume



#### 获取 Windows 系统音量合成器中当前进程的音量（仅适用于 Windows 系统）。

## setApplicationMuteState



#### 设置 Windows 系统音量合成器中当前进程的静音状态（仅适用于 Windows 系统）。

## getApplicationMuteState



#### 获取 Windows 系统音量合成器中当前进程的静音状态（仅适用于 Windows 系统）。

## setCameraCapturerParam



#### 设置摄像头采集偏好。

## setDeviceObserver



#### 设置 onDeviceChanged 事件回调。

## setSystemVolumeType



#### 设置系统音量类型（仅适用于移动端）。

@deprecated v9.5 版本开始不推荐使用，建议使用 ` TRTCCloud ` 中的 ` startLocalAudio(quality) ` 接口替代之，通过 quality 参数来决策音质。

## TXSystemVolumeType(Deprecated)



#### 系统音量类型（仅适用于移动设备）。

@deprecated v9.5 版本开始不推荐使用。



现代智能手机中一般都具备两套系统音量类型，即“通话音量”和“媒体音量”。
-  通话音量：手机专门为接打电话所设计的音量类型，自带回声抵消（AEC）功能，并且支持通过蓝牙耳机上的麦克风进行拾音，缺点是音质比较一般。


当您通过手机侧面的音量按键下调手机音量时，如果无法将其调至零（也就是无法彻底静音），说明您的手机当前处于通话音量。
-  媒体音量：手机专门为音乐场景所设计的音量类型，无法使用系统的 AEC 功能，并且不支持通过蓝牙耳机的麦克风进行拾音，但具备更好的音乐播放效果。


当您通过手机侧面的音量按键下调手机音量时，如果能够将手机音量调至彻底静音，说明您的手机当前处于媒体音量。



SDK 目前提供了三种系统音量类型的控制模式：自动切换模式、全程通话音量模式、全程媒体音量模式。
<table>
<tr>
<td rowspan="1" colSpan="1" >枚举</td>

<td rowspan="1" colSpan="1" >取值</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXSystemVolumeTypeAuto</td>

<td rowspan="1" colSpan="1" >0</td>

<td rowspan="1" colSpan="1" >自动切换模式</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXSystemVolumeTypeMedia</td>

<td rowspan="1" colSpan="1" >1</td>

<td rowspan="1" colSpan="1" >全程媒体音量</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXSystemVolumeTypeVOIP</td>

<td rowspan="1" colSpan="1" >2</td>

<td rowspan="1" colSpan="1" >全程通话音量</td>
</tr>
</table>


## TXAudioRoute



#### 音频路由（即声音的播放模式）。

音频路由，即声音是从手机的扬声器还是从听筒中播放出来，因此该接口仅适用于手机等移动端设备。

手机有两个扬声器：一个是位于手机顶部的听筒，一个是位于手机底部的立体声扬声器。
-  设置音频路由为听筒时，声音比较小，只有将耳朵凑近才能听清楚，隐私性较好，适合用于接听电话。

-  设置音频路由为扬声器时，声音比较大，不用将手机贴脸也能听清，因此可以实现“免提”的功能。

<table>
<tr>
<td rowspan="1" colSpan="1" >枚举</td>

<td rowspan="1" colSpan="1" >取值</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXAudioRouteSpeakerphone</td>

<td rowspan="1" colSpan="1" >0</td>

<td rowspan="1" colSpan="1" >Speakerphone：使用扬声器播放（即“免提”），扬声器位于手机底部，声音偏大，适合外放音乐。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXAudioRouteEarpiece</td>

<td rowspan="1" colSpan="1" >1</td>

<td rowspan="1" colSpan="1" >Earpiece：使用听筒播放，听筒位于手机顶部，声音偏小，适合需要保护隐私的通话场景。</td>
</tr>
</table>


## TXMediaDeviceType



#### 设备类型（仅适用于桌面平台）。



该枚举值用于定义三种类型的音视频设备，即摄像头、麦克风和扬声器，以便让一套设备管理接口可以操控三种不同类型的设备。
<table>
<tr>
<td rowspan="1" colSpan="1" >枚举</td>

<td rowspan="1" colSpan="1" >取值</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXMediaDeviceTypeUnknown</td>

<td rowspan="1" colSpan="1" >-1</td>

<td rowspan="1" colSpan="1" >未定义的设备类型</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXMediaDeviceTypeMic</td>

<td rowspan="1" colSpan="1" >0</td>

<td rowspan="1" colSpan="1" >麦克风类型设备</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXMediaDeviceTypeSpeaker</td>

<td rowspan="1" colSpan="1" >1</td>

<td rowspan="1" colSpan="1" >扬声器类型设备</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXMediaDeviceTypeCamera</td>

<td rowspan="1" colSpan="1" >2</td>

<td rowspan="1" colSpan="1" >摄像头类型设备</td>
</tr>
</table>


## TXMediaDeviceState



#### 设备操作。

该枚举值用于本地设备的状态变化通知 onDeviceChanged。
<table>
<tr>
<td rowspan="1" colSpan="1" >枚举</td>

<td rowspan="1" colSpan="1" >取值</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXMediaDeviceStateAdd</td>

<td rowspan="1" colSpan="1" >0</td>

<td rowspan="1" colSpan="1" >设备已被插入</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXMediaDeviceStateRemove</td>

<td rowspan="1" colSpan="1" >1</td>

<td rowspan="1" colSpan="1" >设备已被移除</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXMediaDeviceStateActive</td>

<td rowspan="1" colSpan="1" >2</td>

<td rowspan="1" colSpan="1" >设备已启用</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXMediaDefaultDeviceChanged</td>

<td rowspan="1" colSpan="1" >3</td>

<td rowspan="1" colSpan="1" >系统默认设备变更</td>
</tr>
</table>


## TXCameraCaptureMode



#### 摄像头采集偏好。

该枚举类型用于摄像头采集参数设置。
<table>
<tr>
<td rowspan="1" colSpan="1" >枚举</td>

<td rowspan="1" colSpan="1" >取值</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXCameraResolutionStrategyAuto</td>

<td rowspan="1" colSpan="1" >0</td>

<td rowspan="1" colSpan="1" >自动调整采集参数。<br>SDK 根据实际的采集设备性能及网络情况，选择合适的摄像头输出参数，在设备性能及视频预览质量之间，维持平衡。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXCameraResolutionStrategyPerformance</td>

<td rowspan="1" colSpan="1" >1</td>

<td rowspan="1" colSpan="1" >优先保证设备性能。<br>SDK 根据用户设置编码器的分辨率和帧率，选择最接近的摄像头输出参数，从而保证设备性能。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXCameraResolutionStrategyHighQuality</td>

<td rowspan="1" colSpan="1" >2</td>

<td rowspan="1" colSpan="1" >优先保证视频预览质量。<br>SDK选择较高的摄像头输出参数，从而提高预览视频的质量。在这种情况下，会消耗更多的 CPU 及内存做视频前处理。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXCameraCaptureManual</td>

<td rowspan="1" colSpan="1" >3</td>

<td rowspan="1" colSpan="1" >允许用户设置本地摄像头采集的视频宽高。</td>
</tr>
</table>


## TXCameraCaptureParam



#### 摄像头采集参数。

该设置能决定本地预览图像画质。
<table>
<tr>
<td rowspan="1" colSpan="1" >枚举类型</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >height</td>

<td rowspan="1" colSpan="1" >**字段含义：** 采集图像宽度</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >mode</td>

<td rowspan="1" colSpan="1" >**字段含义：** 摄像头采集偏好，请参见 [TXCameraCaptureMode](https://write.woa.com/document/87030115247763456)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >width</td>

<td rowspan="1" colSpan="1" >**字段含义：** 采集图像长度</td>
</tr>
</table>


## TXMediaDeviceInfo



#### 音视频设备的相关信息（仅适用于桌面平台）。

该结构体用于描述一个音视频设备的关键信息，例如设备 ID、设备名称等等，以便用户能够在用户界面上选择自己期望使用的音视频设备。
<table>
<tr>
<td rowspan="1" colSpan="1" >枚举类型</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >getDeviceName()</td>

<td rowspan="1" colSpan="1" >设备名称 （UTF-8）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >getDevicePID()</td>

<td rowspan="1" colSpan="1" >设备 ID （UTF-8）</td>
</tr>
</table>


## ITXDeviceCollection



#### 设备信息列表（仅适用于桌面平台）。

此结构体的作用相当于 std::vector<ITXDeviceInfo>，用于解决不同版本的 STL 容器的二进制兼容问题。
<table>
<tr>
<td rowspan="1" colSpan="1" >枚举类型</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >getCount()</td>

<td rowspan="1" colSpan="1" >设备数量</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >index)</td>

<td rowspan="1" colSpan="1" >设备信息（JSON 格式）<br>**注意**<br>示例：{"SupportedResolution":[{"width":640,"height":480},{"width":320,"height":240}]}<br>param index 设备索引，值为 [0,getCount)，return 返回 JSON 格式的设备信息<br></td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >release()</td>

<td rowspan="1" colSpan="1" >释放设备列表，请不要使用 delete 释放资源 !!!</td>
</tr>
</table>
