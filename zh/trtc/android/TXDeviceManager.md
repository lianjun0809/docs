> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

# 腾讯云实时音视频(TRTC SDK )文档

## 概述
`TXDeviceManager.java` 是腾讯云实时音视频(TRTC SDK ) Android 平台的音视频设备管理模块文档，用于管理摄像头、麦克风和扬声器等音视频相关的硬件设备。


## TXDeviceManager
<table>
<tr>
<td rowspan="1" colSpan="1" >函数列表</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[isFrontCamera](https://write.woa.com/document/87029980188905472)</td>

<td rowspan="1" colSpan="1" >判断当前是否为前置摄像头（仅适用于移动端）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[switchCamera](https://write.woa.com/document/87029980188905472)</td>

<td rowspan="1" colSpan="1" >切换前置或后置摄像头（仅适用于移动端）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getCameraZoomMaxRatio](https://write.woa.com/document/87029980188905472)</td>

<td rowspan="1" colSpan="1" >获取摄像头的最大缩放倍数（仅适用于移动端）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setCameraZoomRatio](https://write.woa.com/document/87029980188905472)</td>

<td rowspan="1" colSpan="1" >设置摄像头的缩放倍数（仅适用于移动端）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[isAutoFocusEnabled](https://write.woa.com/document/87029980188905472)</td>

<td rowspan="1" colSpan="1" >查询是否支持自动识别人脸位置（仅适用于移动端）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[enableCameraAutoFocus](https://write.woa.com/document/87029980188905472)</td>

<td rowspan="1" colSpan="1" >开启自动对焦功能（仅适用于移动端）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setCameraFocusPosition](https://write.woa.com/document/87029980188905472)</td>

<td rowspan="1" colSpan="1" >设置摄像头的对焦位置（仅适用于移动端）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[enableCameraTorch](https://write.woa.com/document/87029980188905472)</td>

<td rowspan="1" colSpan="1" >开启/关闭闪光灯，也就是手电筒模式（仅适用于移动端）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setAudioRoute](https://write.woa.com/document/87029980188905472)</td>

<td rowspan="1" colSpan="1" >设置音频路由（仅适用于移动端）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setExposureCompensation](https://write.woa.com/document/87029980188905472)</td>

<td rowspan="1" colSpan="1" >设置摄像头的曝光参数，取值范围为 [-1, 1]。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setCameraCapturerParam](https://write.woa.com/document/87029980188905472)</td>

<td rowspan="1" colSpan="1" >设置摄像头采集偏好。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setSystemVolumeType](https://write.woa.com/document/87029980188905472)</td>

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
<td rowspan="1" colSpan="1" >[TXCameraCaptureParam](https://write.woa.com/document/87029980188905472)</td>

<td rowspan="1" colSpan="1" >摄像头采集参数。</td>
</tr>
</table>


## 枚举类型
<table>
<tr>
<td rowspan="1" colSpan="1" >枚举类型</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[TXSystemVolumeType](https://write.woa.com/document/87029980188905472)</td>

<td rowspan="1" colSpan="1" >系统音量类型（仅适用于移动设备）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[TXAudioRoute](https://write.woa.com/document/87029980188905472)</td>

<td rowspan="1" colSpan="1" >音频路由（即声音的播放模式）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[TXCameraCaptureMode](https://write.woa.com/document/87029980188905472)</td>

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

> 使用该接口的前提是先通过 [enableCameraAutoFocus](https://write.woa.com/document/87029980188905472) 关闭自动对焦功能。
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

## setExposureCompensation



#### 设置摄像头的曝光参数，取值范围为 [-1, 1]。

## setCameraCapturerParam



#### 设置摄像头采集偏好。

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

<td rowspan="1" colSpan="1" >Not Defined</td>

<td rowspan="1" colSpan="1" >自动切换模式</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXSystemVolumeTypeMedia</td>

<td rowspan="1" colSpan="1" >Not Defined</td>

<td rowspan="1" colSpan="1" >全程媒体音量</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXSystemVolumeTypeVOIP</td>

<td rowspan="1" colSpan="1" >Not Defined</td>

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

<td rowspan="1" colSpan="1" >Not Defined</td>

<td rowspan="1" colSpan="1" >Speakerphone：使用扬声器播放（即“免提”），扬声器位于手机底部，声音偏大，适合外放音乐。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXAudioRouteEarpiece</td>

<td rowspan="1" colSpan="1" >Not Defined</td>

<td rowspan="1" colSpan="1" >Earpiece：使用听筒播放，听筒位于手机顶部，声音偏小，适合需要保护隐私的通话场景。</td>
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

<td rowspan="1" colSpan="1" >Not Defined</td>

<td rowspan="1" colSpan="1" >自动调整采集参数。<br>SDK 根据实际的采集设备性能及网络情况，选择合适的摄像头输出参数，在设备性能及视频预览质量之间，维持平衡。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXCameraResolutionStrategyPerformance</td>

<td rowspan="1" colSpan="1" >Not Defined</td>

<td rowspan="1" colSpan="1" >优先保证设备性能。<br>SDK 根据用户设置编码器的分辨率和帧率，选择最接近的摄像头输出参数，从而保证设备性能。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXCameraResolutionStrategyHighQuality</td>

<td rowspan="1" colSpan="1" >Not Defined</td>

<td rowspan="1" colSpan="1" >优先保证视频预览质量。<br>SDK选择较高的摄像头输出参数，从而提高预览视频的质量。在这种情况下，会消耗更多的 CPU 及内存做视频前处理。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXCameraCaptureManual</td>

<td rowspan="1" colSpan="1" >Not Defined</td>

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

<td rowspan="1" colSpan="1" >**字段含义：** 摄像头采集偏好，请参见 [TXCameraCaptureMode](https://write.woa.com/document/87029980188905472)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >width</td>

<td rowspan="1" colSpan="1" >**字段含义：** 采集图像长度</td>
</tr>
</table>
