> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

# 腾讯云实时音视频(TRTC SDK )文档

## 概述
`TXLiteAVCode.h` 是腾讯云实时音视频(TRTC SDK ) C++ 的状态码文档，用于通知客户 TRTC 在使用过程中出现的警告和错误。


## 枚举类型
<table>
<tr>
<td rowspan="1" colSpan="1" >枚举类型</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[TXLiteAVError](https://write.woa.com/document/86735809798561792)</td>

<td rowspan="1" colSpan="1" >错误码。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[TXLiteAVWarning](https://write.woa.com/document/86735809798561792)</td>

<td rowspan="1" colSpan="1" >警告码。</td>
</tr>
</table>


## TXLiteAVError



#### 错误码。
<table>
<tr>
<td rowspan="1" colSpan="1" >枚举</td>

<td rowspan="1" colSpan="1" >取值</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_NULL</td>

<td rowspan="1" colSpan="1" >0</td>

<td rowspan="1" colSpan="1" >无错误</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_FAILED</td>

<td rowspan="1" colSpan="1" >-1</td>

<td rowspan="1" colSpan="1" >暂未归类的通用错误</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_INVALID_PARAMETER</td>

<td rowspan="1" colSpan="1" >-2</td>

<td rowspan="1" colSpan="1" >调用 API 时，传入的参数不合法</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_REFUSED</td>

<td rowspan="1" colSpan="1" >-3</td>

<td rowspan="1" colSpan="1" >API 调用被拒绝</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_NOT_SUPPORTED</td>

<td rowspan="1" colSpan="1" >-4</td>

<td rowspan="1" colSpan="1" >当前 API 不支持调用</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_INVALID_LICENSE</td>

<td rowspan="1" colSpan="1" >-5</td>

<td rowspan="1" colSpan="1" >license 不合法，调用失败</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_REQUEST_SERVER_TIMEOUT</td>

<td rowspan="1" colSpan="1" >-6</td>

<td rowspan="1" colSpan="1" >请求服务器超时</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_SERVER_PROCESS_FAILED</td>

<td rowspan="1" colSpan="1" >-7</td>

<td rowspan="1" colSpan="1" >服务器无法处理您的请求</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_DISCONNECTED</td>

<td rowspan="1" colSpan="1" >-8</td>

<td rowspan="1" colSpan="1" >断开连接</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_CAMERA_START_FAIL</td>

<td rowspan="1" colSpan="1" >-1301</td>

<td rowspan="1" colSpan="1" >打开摄像头失败，在移动端中是授权后调用系统接口开启摄像头异常，在 Windows 或 Mac 设备，摄像头的配置程序（驱动程序）异常，禁用后重新启用设备，或者重启机器，或者更新配置程序</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_CAMERA_NOT_AUTHORIZED</td>

<td rowspan="1" colSpan="1" >-1314</td>

<td rowspan="1" colSpan="1" >摄像头设备未授权，通常在移动设备出现，可能是权限被用户拒绝了</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_CAMERA_SET_PARAM_FAIL</td>

<td rowspan="1" colSpan="1" >-1315</td>

<td rowspan="1" colSpan="1" >摄像头参数设置出错（参数不支持或其它）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_CAMERA_OCCUPY</td>

<td rowspan="1" colSpan="1" >-1316</td>

<td rowspan="1" colSpan="1" >摄像头正在被占用中，可尝试打开其他摄像头</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_SCREEN_CAPTURE_START_FAIL</td>

<td rowspan="1" colSpan="1" >-1308</td>

<td rowspan="1" colSpan="1" >开始录屏失败，如果在移动设备出现，可能是权限被用户拒绝了。在 Windows 或 Mac 系统的设备出现，请检查录屏接口的参数是否符合要求</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_SCREEN_CAPTURE_UNSURPORT</td>

<td rowspan="1" colSpan="1" >-1309</td>

<td rowspan="1" colSpan="1" >录屏失败，在 Android 平台，需要5.0以上的系统，在 iOS 平台，需要11.0以上的系统</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_SCREEN_CAPTURE_STOPPED</td>

<td rowspan="1" colSpan="1" >-7001</td>

<td rowspan="1" colSpan="1" >录屏被系统中止</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_SCREEN_SHARE_NOT_AUTHORIZED</td>

<td rowspan="1" colSpan="1" >-102015</td>

<td rowspan="1" colSpan="1" >没有权限上行辅路</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_SCREEN_SHRAE_OCCUPIED_BY_OTHER</td>

<td rowspan="1" colSpan="1" >-102016</td>

<td rowspan="1" colSpan="1" >其他用户正在上行辅路</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_VIDEO_ENCODE_FAIL</td>

<td rowspan="1" colSpan="1" >-1303</td>

<td rowspan="1" colSpan="1" >视频帧编码失败，编码器异常导致编码失败</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_UNSUPPORTED_RESOLUTION</td>

<td rowspan="1" colSpan="1" >-1305</td>

<td rowspan="1" colSpan="1" >不支持的视频分辨率</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_PIXEL_FORMAT_UNSUPPORTED</td>

<td rowspan="1" colSpan="1" >-1327</td>

<td rowspan="1" colSpan="1" >自定视频采集：设置的 pixel format 不支持</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_BUFFER_TYPE_UNSUPPORTED</td>

<td rowspan="1" colSpan="1" >-1328</td>

<td rowspan="1" colSpan="1" >自定视频采集：设置的 buffer type 不支持</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_NO_AVAILABLE_HEVC_DECODERS</td>

<td rowspan="1" colSpan="1" >-2304</td>

<td rowspan="1" colSpan="1" >找不到可用的 HEVC 解码器</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_MIC_START_FAIL</td>

<td rowspan="1" colSpan="1" >-1302</td>

<td rowspan="1" colSpan="1" >打开麦克风失败，例如在 Windows 或 Mac 设备，麦克风的配置程序（驱动程序）异常，禁用后重新启用设备，或者重启机器，或者更新配置程序</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_MIC_NOT_AUTHORIZED</td>

<td rowspan="1" colSpan="1" >-1317</td>

<td rowspan="1" colSpan="1" >麦克风设备未授权，通常在移动设备出现，可能是权限被用户拒绝了</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_MIC_OCCUPY</td>

<td rowspan="1" colSpan="1" >-1319</td>

<td rowspan="1" colSpan="1" >麦克风正在被占用中，例如移动设备正在通话时，打开麦克风会失败</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_MIC_STOP_FAIL</td>

<td rowspan="1" colSpan="1" >-1320</td>

<td rowspan="1" colSpan="1" >停止麦克风失败</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_SPEAKER_START_FAIL</td>

<td rowspan="1" colSpan="1" >-1321</td>

<td rowspan="1" colSpan="1" >打开扬声器失败，例如在 Windows 或 Mac 设备，扬声器的配置程序（驱动程序）异常，禁用后重新启用设备，或者重启机器，或者更新配置程序</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_SPEAKER_SET_PARAM_FAIL</td>

<td rowspan="1" colSpan="1" >-1322</td>

<td rowspan="1" colSpan="1" >扬声器设置参数失败</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_SPEAKER_STOP_FAIL</td>

<td rowspan="1" colSpan="1" >-1323</td>

<td rowspan="1" colSpan="1" >停止扬声器失败</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_AUDIO_PLUGIN_START_FAIL</td>

<td rowspan="1" colSpan="1" >-1330</td>

<td rowspan="1" colSpan="1" >开启系统声音录制失败，例如音频驱动插件不可用</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_AUDIO_PLUGIN_INSTALL_NOT_AUTHORIZED</td>

<td rowspan="1" colSpan="1" >-1331</td>

<td rowspan="1" colSpan="1" >安装音频驱动插件未授权</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_AUDIO_PLUGIN_INSTALL_FAILED</td>

<td rowspan="1" colSpan="1" >-1332</td>

<td rowspan="1" colSpan="1" >安装音频驱动插件失败</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_AUDIO_PLUGIN_INSTALLED_BUT_NEED_RESTART</td>

<td rowspan="1" colSpan="1" >-1333</td>

<td rowspan="1" colSpan="1" >安装虚拟声卡插件成功，但首次安装后功能暂时不可用，此为 Mac 系统限制，请在收到此错误码后提示用户重启当前 APP</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_AUDIO_ENCODE_FAIL</td>

<td rowspan="1" colSpan="1" >-1304</td>

<td rowspan="1" colSpan="1" >音频帧编码失败，例如传入自定义音频数据，SDK 无法处理</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_UNSUPPORTED_SAMPLERATE</td>

<td rowspan="1" colSpan="1" >-1306</td>

<td rowspan="1" colSpan="1" >不支持的音频采样率</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_SYSTEM_LOOPBACK_START_FAILED</td>

<td rowspan="1" colSpan="1" >-1307</td>

<td rowspan="1" colSpan="1" >系统混音启动出错，常见的出错原因及解决：1.当前系统版本无法支持，指定、排除指定进程混音功能需满足 Windows 系统为10.0.19042（20H2）或更高版本，指定路径混音功能 x64 版本需满足 Windows 系统为10.0.19042（20H2）或更高版本，请检查当前系统版本。2.传入参数非法（包括参数为空、传入路径不存在、传入进程号不存在、传入设备名不存在），请检查传入参数是否合法。3.无可用扬声器设备，请检查是否可用</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_SYSTEM_LOOPBACK_THIRD_PARTY_APP_EXIT</td>

<td rowspan="1" colSpan="1" >-1324</td>

<td rowspan="1" colSpan="1" >第三方应用混音采集出错，该错误可能出现于第三方应用混音启动成功后，在采集声音的过程中指定进程或应用意外退出，请检查指定进程或应用的状态，可通过重新输入进程号进行重试</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_ENTER_ROOM_FAILED</td>

<td rowspan="1" colSpan="1" >-3301</td>

<td rowspan="1" colSpan="1" >进入房间失败，请查看 onError 中的 -3301 对应的 msg 提示确认失败原因</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_REQUEST_IP_TIMEOUT</td>

<td rowspan="1" colSpan="1" >-3307</td>

<td rowspan="1" colSpan="1" >请求 IP 和 sig 超时，请检查网络是否正常，或网络防火墙是否放行 UDP。<br>可尝试访问下列 IP：162.14.22.165:8000 162.14.6.105:8000 和域名：default-query.trtc.tencent-cloud.com:8000</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_CONNECT_SERVER_TIMEOUT</td>

<td rowspan="1" colSpan="1" >-3308</td>

<td rowspan="1" colSpan="1" >请求进房超时，请检查是否断网或者是否开启vpn，您也可以切换4G进行测试确认</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_ROOM_PARAM_NULL</td>

<td rowspan="1" colSpan="1" >-3316</td>

<td rowspan="1" colSpan="1" >进房参数为空，请检查： enterRoom:appScene: 接口调用是否传入有效的 param</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_INVALID_SDK_APPID</td>

<td rowspan="1" colSpan="1" >-3317</td>

<td rowspan="1" colSpan="1" >进房参数 sdkAppId 错误，请检查 TRTCParams.sdkAppId 是否为空</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_INVALID_ROOM_ID</td>

<td rowspan="1" colSpan="1" >-3318</td>

<td rowspan="1" colSpan="1" >进房参数 roomId 错误，请检查 TRTCParams.roomId 或 TRTCParams.strRoomId 是否为空，注意 roomId 和 strRoomId 不可混用</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_INVALID_USER_ID</td>

<td rowspan="1" colSpan="1" >-3319</td>

<td rowspan="1" colSpan="1" >进房参数 userId 不正确，请检查 TRTCParams.userId 是否为空</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_INVALID_USER_SIG</td>

<td rowspan="1" colSpan="1" >-3320</td>

<td rowspan="1" colSpan="1" >进房参数 userSig 不正确，请检查 TRTCParams.userSig 是否为空</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_ENTER_ROOM_REFUSED</td>

<td rowspan="1" colSpan="1" >-3340</td>

<td rowspan="1" colSpan="1" >进房请求被拒绝，请检查是否连续调用 enterRoom 进入相同 Id 的房间</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_INVALID_PRIVATE_MAPKEY</td>

<td rowspan="1" colSpan="1" >-100006</td>

<td rowspan="1" colSpan="1" >您开启了高级权限控制，但参数 TRTCParams.privateMapKey 校验失败，<br>您可参考 [高级权限控制](https://cloud.tencent.com/document/product/647/32240) 进行检查</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_SERVICE_SUSPENDED</td>

<td rowspan="1" colSpan="1" >-100013</td>

<td rowspan="1" colSpan="1" >服务不可用。请检查：套餐包剩余分钟数是否大于0，腾讯云账号是否欠费。<br>您可参考 [套餐包管理](https://cloud.tencent.com/document/product/647/50492) 进行查看与配置</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_USER_SIG_CHECK_FAILED</td>

<td rowspan="1" colSpan="1" >-100018</td>

<td rowspan="1" colSpan="1" >UserSig 校验失败，请检查参数 TRTCParams.userSig 是否填写正确，或是否已经过期。<br>您可参考 [UserSig 生成与校验](https://cloud.tencent.com/document/product/647/50686) 进行校验</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_PUSH_THIRD_PARTY_CLOUD_TIMEOUT</td>

<td rowspan="1" colSpan="1" >-3321</td>

<td rowspan="1" colSpan="1" >旁路转推请求超时</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_MIX_TRANSCODING_TIMEOUT</td>

<td rowspan="1" colSpan="1" >-3322</td>

<td rowspan="1" colSpan="1" >云端混流请求超时</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_PUSH_THIRD_PARTY_CLOUD_FAILED</td>

<td rowspan="1" colSpan="1" >-3323</td>

<td rowspan="1" colSpan="1" >旁路转推回包异常</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_MIX_TRANSCODING_FAILED</td>

<td rowspan="1" colSpan="1" >-3324</td>

<td rowspan="1" colSpan="1" >云端混流回包异常</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_START_PUBLISHING_TIMEOUT</td>

<td rowspan="1" colSpan="1" >-3333</td>

<td rowspan="1" colSpan="1" >开始向腾讯云的直播 CDN 推流信令超时</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_START_PUBLISHING_FAILED</td>

<td rowspan="1" colSpan="1" >-3334</td>

<td rowspan="1" colSpan="1" >开始向腾讯云的直播 CDN 推流信令异常</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_STOP_PUBLISHING_TIMEOUT</td>

<td rowspan="1" colSpan="1" >-3335</td>

<td rowspan="1" colSpan="1" >停止向腾讯云的直播 CDN 推流信令超时</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_STOP_PUBLISHING_FAILED</td>

<td rowspan="1" colSpan="1" >-3336</td>

<td rowspan="1" colSpan="1" >停止向腾讯云的直播 CDN 推流信令异常</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_CONNECT_OTHER_ROOM_TIMEOUT</td>

<td rowspan="1" colSpan="1" >-3326</td>

<td rowspan="1" colSpan="1" >请求连麦超时</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_DISCONNECT_OTHER_ROOM_TIMEOUT</td>

<td rowspan="1" colSpan="1" >-3327</td>

<td rowspan="1" colSpan="1" >请求退出连麦超时</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_CONNECT_OTHER_ROOM_INVALID_PARAMETER</td>

<td rowspan="1" colSpan="1" >-3328</td>

<td rowspan="1" colSpan="1" >无效参数</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_TRTC_CONNECT_OTHER_ROOM_AS_AUDIENCE</td>

<td rowspan="1" colSpan="1" >-3330</td>

<td rowspan="1" colSpan="1" >当前是观众角色，不能请求或断开跨房连麦，需要先 ` switchRole ` 到主播</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_BGM_OPEN_FAILED</td>

<td rowspan="1" colSpan="1" >-4001</td>

<td rowspan="1" colSpan="1" >打开文件失败，如音频数据无效，FFMPEG 协议未找到等</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_BGM_DECODE_FAILED</td>

<td rowspan="1" colSpan="1" >-4002</td>

<td rowspan="1" colSpan="1" >音频文件解码失败</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_BGM_OVER_LIMIT</td>

<td rowspan="1" colSpan="1" >-4003</td>

<td rowspan="1" colSpan="1" >数量超过限定值，如同时预加载两首背景音乐</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_BGM_INVALID_OPERATION</td>

<td rowspan="1" colSpan="1" >-4004</td>

<td rowspan="1" colSpan="1" >无效操作，如开始播放后再调用预加载操作</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_BGM_INVALID_PATH</td>

<td rowspan="1" colSpan="1" >-4005</td>

<td rowspan="1" colSpan="1" >非法路径导致打开文件失败，请检查您传入的路径参数是否指向一个合法的音乐文件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_BGM_INVALID_URL</td>

<td rowspan="1" colSpan="1" >-4006</td>

<td rowspan="1" colSpan="1" >非法URL导致打开文件失败，请用浏览器检查您传入的 URL 地址是否可以下载到期望的音乐文件，如果操作系统为 iOS 或 MacOS 请确保使用 https 链接</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_BGM_NO_AUDIO_STREAM</td>

<td rowspan="1" colSpan="1" >-4007</td>

<td rowspan="1" colSpan="1" >无音频流导致打开文件失败，请确认您传入的文件是否是合法的音频文件，以及文件是否被损坏</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_BGM_FORMAT_NOT_SUPPORTED</td>

<td rowspan="1" colSpan="1" >-4008</td>

<td rowspan="1" colSpan="1" >格式不支持导致打开文件失败，请确认您传入的文件格式是否是支持的文件格式，移动端支持【mp3，aac，m4a，wav，ogg，mp4，mkv】，桌面端支持 【mp3，aac，m4a，wav，mp4，mkv】</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ERR_CONCURRENT_BGM_OVER_LIMIT</td>

<td rowspan="1" colSpan="1" >-4009</td>

<td rowspan="1" colSpan="1" >同时播放 bgm 数量超过限定值，如当前同时播放 bgm 数量超过 10 后提示该错误，请检查并发播放 bgm 数量</td>
</tr>
</table>


## TXLiteAVWarning



#### 警告码。
<table>
<tr>
<td rowspan="1" colSpan="1" >枚举</td>

<td rowspan="1" colSpan="1" >取值</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_HW_ENCODER_START_FAIL</td>

<td rowspan="1" colSpan="1" >1103</td>

<td rowspan="1" colSpan="1" >硬编码启动出现问题，自动切换到软编码</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_CURRENT_ENCODE_TYPE_CHANGED</td>

<td rowspan="1" colSpan="1" >1104</td>

<td rowspan="1" colSpan="1" >表示编码器发生改变，可以通过 onWarning 函数的扩展信息中的相关字段来获取当前的编码格式和类型。<br>type 字段值为 0 代表 H.264 编码，1 代表 H.265 编码<br>hardware 字段值为 0 代表软件编码，1 代表硬件编码<br>stream 字段值为 0 代表大流，1 代表小流，2 代表辅流</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_VIDEO_ENCODER_SW_TO_HW</td>

<td rowspan="1" colSpan="1" >1107</td>

<td rowspan="1" colSpan="1" >当前 CPU 使用率太高，无法满足软件编码需求，自动切换到硬件编码</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_INSUFFICIENT_CAPTURE_FPS</td>

<td rowspan="1" colSpan="1" >1108</td>

<td rowspan="1" colSpan="1" >摄像头采集帧率不足，部分自带美颜算法的 Android 手机上会出现</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_SW_ENCODER_START_FAIL</td>

<td rowspan="1" colSpan="1" >1109</td>

<td rowspan="1" colSpan="1" >软编码启动失败</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_REDUCE_CAPTURE_RESOLUTION</td>

<td rowspan="1" colSpan="1" >1110</td>

<td rowspan="1" colSpan="1" >摄像头采集分辨率被降低，以满足当前帧率和性能最优解。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_CAMERA_DEVICE_EMPTY</td>

<td rowspan="1" colSpan="1" >1111</td>

<td rowspan="1" colSpan="1" >没有检测到可用的摄像头设备</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_CAMERA_NOT_AUTHORIZED</td>

<td rowspan="1" colSpan="1" >1112</td>

<td rowspan="1" colSpan="1" >用户未授权当前应用使用摄像头</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_OUT_OF_MEMORY</td>

<td rowspan="1" colSpan="1" >1113</td>

<td rowspan="1" colSpan="1" >内存不足，部分功能可能不正常。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_CAMERA_IS_OCCUPIED</td>

<td rowspan="1" colSpan="1" >1114</td>

<td rowspan="1" colSpan="1" >摄像头被占用.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_CAMERA_DEVICE_ERROR</td>

<td rowspan="1" colSpan="1" >1115</td>

<td rowspan="1" colSpan="1" >摄像头设备异常.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_CAMERA_DISCONNECTED</td>

<td rowspan="1" colSpan="1" >1116</td>

<td rowspan="1" colSpan="1" >摄像头无法连接.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_CAMERA_START_FAILED</td>

<td rowspan="1" colSpan="1" >1117</td>

<td rowspan="1" colSpan="1" >摄像头启动失败.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_CAMERA_SERVER_DIED</td>

<td rowspan="1" colSpan="1" >1118</td>

<td rowspan="1" colSpan="1" >系统异常.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_SCREEN_CAPTURE_NOT_AUTHORIZED</td>

<td rowspan="1" colSpan="1" >1206</td>

<td rowspan="1" colSpan="1" >用户未授权当前应用使用屏幕录制</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_CURRENT_DECODE_TYPE_CHANGED</td>

<td rowspan="1" colSpan="1" >2008</td>

<td rowspan="1" colSpan="1" >表示解码器发生改变，可以通过 onWarning 函数的扩展信息中的 type 字段来获取当前的解码格式。<br>其中 1 代表 265 解码，0 代表 264 解码。注意 Windows 端不支持此错误码的扩展信息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_VIDEO_FRAME_DECODE_FAIL</td>

<td rowspan="1" colSpan="1" >2101</td>

<td rowspan="1" colSpan="1" >当前视频帧解码失败</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_HW_DECODER_START_FAIL</td>

<td rowspan="1" colSpan="1" >2106</td>

<td rowspan="1" colSpan="1" >硬解启动失败，采用软解码</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_VIDEO_DECODER_HW_TO_SW</td>

<td rowspan="1" colSpan="1" >2108</td>

<td rowspan="1" colSpan="1" >当前流硬解第一个 I 帧失败，SDK 自动切软解</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_SW_DECODER_START_FAIL</td>

<td rowspan="1" colSpan="1" >2109</td>

<td rowspan="1" colSpan="1" >软解码器启动失败</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_VIDEO_RENDER_FAIL</td>

<td rowspan="1" colSpan="1" >2110</td>

<td rowspan="1" colSpan="1" >视频渲染失败</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_VIRTUAL_BACKGROUND_DEVICE_UNSURPORTED</td>

<td rowspan="1" colSpan="1" >8001</td>

<td rowspan="1" colSpan="1" >虚拟背景设备不支持</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_VIRTUAL_BACKGROUND_NOT_AUTHORIZED</td>

<td rowspan="1" colSpan="1" >8002</td>

<td rowspan="1" colSpan="1" >虚拟背景未授权</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_VIRTUAL_BACKGROUND_INVALID_PARAMETER</td>

<td rowspan="1" colSpan="1" >8003</td>

<td rowspan="1" colSpan="1" >虚拟背景参数异常</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_VIRTUAL_BACKGROUND_PERFORMANCE_INSUFFICIENT</td>

<td rowspan="1" colSpan="1" >8004</td>

<td rowspan="1" colSpan="1" >虚拟背景性能不足</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_MICROPHONE_DEVICE_EMPTY</td>

<td rowspan="1" colSpan="1" >1201</td>

<td rowspan="1" colSpan="1" >没有检测到可用的麦克风设备</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_SPEAKER_DEVICE_EMPTY</td>

<td rowspan="1" colSpan="1" >1202</td>

<td rowspan="1" colSpan="1" >没有检测到可用的扬声器设备</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_MICROPHONE_NOT_AUTHORIZED</td>

<td rowspan="1" colSpan="1" >1203</td>

<td rowspan="1" colSpan="1" >用户未授权当前应用使用麦克风</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_MICROPHONE_DEVICE_ABNORMAL</td>

<td rowspan="1" colSpan="1" >1204</td>

<td rowspan="1" colSpan="1" >音频采集设备不可用（例如被占用或者PC判定无效设备）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_SPEAKER_DEVICE_ABNORMAL</td>

<td rowspan="1" colSpan="1" >1205</td>

<td rowspan="1" colSpan="1" >音频播放设备不可用（例如被占用或者PC判定无效设备）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_BLUETOOTH_DEVICE_CONNECT_FAIL</td>

<td rowspan="1" colSpan="1" >1207</td>

<td rowspan="1" colSpan="1" >蓝牙设备连接失败（例如其他应用通过设置通话音量占用音频通道）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_MICROPHONE_IS_OCCUPIED</td>

<td rowspan="1" colSpan="1" >1208</td>

<td rowspan="1" colSpan="1" >音频采集设备被占用</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_AUDIO_FRAME_DECODE_FAIL</td>

<td rowspan="1" colSpan="1" >2102</td>

<td rowspan="1" colSpan="1" >当前音频帧解码失败</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_AUDIO_RECORDING_WRITE_FAIL</td>

<td rowspan="1" colSpan="1" >7001</td>

<td rowspan="1" colSpan="1" >音频录制写入文件失败</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_MICROPHONE_HOWLING_DETECTED</td>

<td rowspan="1" colSpan="1" >7002</td>

<td rowspan="1" colSpan="1" >录制音频时监测到啸叫</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_IGNORE_UPSTREAM_FOR_AUDIENCE</td>

<td rowspan="1" colSpan="1" >6001</td>

<td rowspan="1" colSpan="1" >当前是观众角色，不支持发布音视频，需要先切换成主播角色</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_UPSTREAM_AUDIO_AND_VIDEO_OUT_OF_SYNC</td>

<td rowspan="1" colSpan="1" >6006</td>

<td rowspan="1" colSpan="1" >音视频发送时间戳异常，可能引起音画不同步问题</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >WARNING_RECONNECT_ON_SERVER_STATUS_ABNORMAL</td>

<td rowspan="1" colSpan="1" >6007</td>

<td rowspan="1" colSpan="1" >服务器状态异常，正在进行重连</td>
</tr>
</table>
