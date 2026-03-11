> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

> **注意：**
> 

> **新老版本 API 请勿混合使用**。
> 


## 初始化登录接口

初始化并成功登录，是正常使用腾讯云 IM 服务的前提。
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[initSDK](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a8035eed3a7c9b3b1c229196ac7bc5da6)</td>

<td rowspan="1" colSpan="1" >初始化</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[unInitSDK](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a286e5358ec4cd0a8f9c66f4d2d7d4544)</td>

<td rowspan="1" colSpan="1" >反初始化</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addIMSDKListener](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#ac569656a58908afba491710a8cb3c8d9)</td>

<td rowspan="1" colSpan="1" >添加 IM 监听</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeIMSDKListener](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a2e2a7e64bf51888c98636e5974a8aca7)</td>

<td rowspan="1" colSpan="1" >移除 IM 监听</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getVersion](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#ae8281def98e669d701171ede7aa3c176)</td>

<td rowspan="1" colSpan="1" >获取版本号</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getServerTime](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a4adcf2642bcb706cd6cfe7e5c5f85f06)</td>

<td rowspan="1" colSpan="1" >获取服务器当前时间</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[login](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a38c42943046acdaf615915c9422af07c)</td>

<td rowspan="1" colSpan="1" >登录</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[logout](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a20b495d7f7a231ea33507ca4a79f811f)</td>

<td rowspan="1" colSpan="1" >退出登录</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getLoginUser](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a78ca7f39bca860e46620f8f766508fb0)</td>

<td rowspan="1" colSpan="1" >获取登录用户</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getLoginStatus](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#acfd2f6366780badf80ebf66d95550f89)</td>

<td rowspan="1" colSpan="1" >获取登录状态</td>
</tr>
</table>


## 简单消息收发接口

如果您只需要使用文本和信令（即一段自定义buffer）消息，只需要使用这套简单消息收发接口即可。
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addSimpleMsgListener](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a149cdf7924aa13746692d18d605def88)</td>

<td rowspan="1" colSpan="1" >设置基本消息（文本消息和自定义消息）的事件监听器，请不要同 [addAdvancedMsgListener](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#acf794752cc6bfa786aea5cd7fabadfab) 混用</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeSimpleMsgListener](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#afa3040f676105f3fb78d4835ee3c898b)</td>

<td rowspan="1" colSpan="1" >移除基本消息（文本消息和自定义消息）的事件监听器</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[sendC2CTextMessage](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a50d63810093eccc0491d058d0b883618)</td>

<td rowspan="1" colSpan="1" >发送单聊（C2C）普通文本消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[sendC2CCustomMessage](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a5fc3b87e9782e679c08926d07e486b90)</td>

<td rowspan="1" colSpan="1" >发送单聊（C2C）自定义（信令）消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[sendGroupTextMessage](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a07788874071937fac6c7093185b145f7)</td>

<td rowspan="1" colSpan="1" >发送群聊普通文本消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[sendGroupCustomMessage](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a537560a58d49aad36406f6d9db6ded65)</td>

<td rowspan="1" colSpan="1" >发送群聊自定义（信令）消息</td>
</tr>
</table>


## 信令接口
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addSignalingListener](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Signaling_08.html#a3a7fde0d4d5a342bd93299deaf98e1d1)</td>

<td rowspan="1" colSpan="1" >添加信令监听</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeSignalingListener](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Signaling_08.html#ae730297ec335735eee3c2f3c464bde33)</td>

<td rowspan="1" colSpan="1" >移除信令监听</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[invite](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Signaling_08.html#a594071fa1a70373582ed6082c581b332)</td>

<td rowspan="1" colSpan="1" >邀请某个人</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[inviteInGroup](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Signaling_08.html#ac01a4e703c925aaf5f78df67faca15be)</td>

<td rowspan="1" colSpan="1" >邀请群内的某些人</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[cancel](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Signaling_08.html#acaac35e5db28db783420b5eb39d53e6f)</td>

<td rowspan="1" colSpan="1" >邀请方取消邀请</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[accept](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Signaling_08.html#a1ffb6daba9deed8780f869205daf7771)</td>

<td rowspan="1" colSpan="1" >接收方接收邀请</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[reject](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Signaling_08.html#a39e685924aaa4d22daa88f2ec96aa827)</td>

<td rowspan="1" colSpan="1" >接收方拒绝邀请</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getSignalingInfo](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Signaling_08.html#a0b149836793b8f2d54889b1c3ae40362)</td>

<td rowspan="1" colSpan="1" >获取信令信息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addInvitedSignaling](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Signaling_08.html#aedfb31fdd3289af36c092b55adeed231)</td>

<td rowspan="1" colSpan="1" >添加邀请信令（可以用于群离线推送消息触发的邀请信令）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[modifyInvitation](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Signaling_08.html#a1f1d6f5053c07996a611e284ac15cbb5)</td>

<td rowspan="1" colSpan="1" >修改邀请信令</td>
</tr>
</table>


## 高级消息收发接口

如果您需要收发图片、视频、文件等富媒体消息，并需要撤回消息、标记已读、查询历史消息等高级功能，推荐使用下面这套高级消息接口（简单消息接口和高级消息接口请不要混用）。
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addAdvancedMsgListener](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#acf794752cc6bfa786aea5cd7fabadfab)</td>

<td rowspan="1" colSpan="1" >设置高级消息的事件监听器，请不要同 [addSimpleMsgListener](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a149cdf7924aa13746692d18d605def88) 混用</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeAdvancedMsgListener](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a28aeebff4a791c9bb8f91a4f61e020e6)</td>

<td rowspan="1" colSpan="1" >移除高级消息监听器</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createTextMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a609f4d4c374d9df3abf9974ff8112fc3)</td>

<td rowspan="1" colSpan="1" >创建文本消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createTextAtMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#aaebbd8ed9b9766d01f996ec722744346)</td>

<td rowspan="1" colSpan="1" >创建 @ 文本消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createCustomMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a7a38c42f63a4e0c9e89f6c56dd0da316)</td>

<td rowspan="1" colSpan="1" >创建自定义消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createImageMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a23033a764f0d95ce83c52f3cdeea4137)</td>

<td rowspan="1" colSpan="1" >创建图片消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createSoundMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a9073007806fa186b8999ce656555032a)</td>

<td rowspan="1" colSpan="1" >创建语音消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createVideoMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a233a9ee5ef2ea371206005d109757f18)</td>

<td rowspan="1" colSpan="1" >创建视频消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createFileMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a9e487ae9541111038ebed900ab639d4c)</td>

<td rowspan="1" colSpan="1" >创建文件消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createLocationMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a2a997472dd62d794cfd4e3a42cfab930)</td>

<td rowspan="1" colSpan="1" >创建地理位置消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createFaceMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#ab7a593be2cca1c8eddd7e73255f3f34a)</td>

<td rowspan="1" colSpan="1" >创建表情消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createMergerMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a2943bb31403aeb22f8582cd9966cf13e)</td>

<td rowspan="1" colSpan="1" >创建合并转发消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createForwardMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a05d088b7d9883e18af41355cdd3f4562)</td>

<td rowspan="1" colSpan="1" >创建单条转发消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createTargetedGroupMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a8bddd2f566a53362b4da5448fdd18fbc)</td>

<td rowspan="1" colSpan="1" >创建定向群消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createAtSignedGroupMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#adfb065794694a2061af2642f18c4aeb7)</td>

<td rowspan="1" colSpan="1" >创建带 @ 标记的群消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[sendMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a681947465d6ab718da40f7f983740a21)</td>

<td rowspan="1" colSpan="1" >发送消息，消息对象可以由 createXXXMessage 接口创建得来</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setC2CReceiveMessageOpt](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#ae628f19d856921d27081c3f40005e9d9)</td>

<td rowspan="1" colSpan="1" >设置单聊消息免打扰</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getC2CReceiveMessageOpt](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a1c743a6fe1d17a21dc80e584fd1de2d1)</td>

<td rowspan="1" colSpan="1" >获取单聊消息免打扰状态</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGroupReceiveMessageOpt](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a379eeef926e41ec5d48287e7fb55b80a)</td>

<td rowspan="1" colSpan="1" >设置群聊消息免打扰状态</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setAllReceiveMessageOpt](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a6495713ce966d3e6cc769616cdfdb846)</td>

<td rowspan="1" colSpan="1" >设置全局消息接收选项（可实现按天重复）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setAllReceiveMessageOpt](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a395aa64727b7743930366be50cc78073)</td>

<td rowspan="1" colSpan="1" >设置全局消息接收选项</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getAllReceiveMessageOpt](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#abca3b16a8f25149867108dad53d43ca0)</td>

<td rowspan="1" colSpan="1" >获取登录用户全局消息接收选项</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getC2CHistoryMessageList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#abca63ad64f69aa4f424cf11849a9b89e)</td>

<td rowspan="1" colSpan="1" >获取单聊（C2C）历史消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupHistoryMessageList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a9e242ba327377fe74b83e8d5572d39a0)</td>

<td rowspan="1" colSpan="1" >获取群组历史消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getHistoryMessageList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a99e8f00ee60df12e346548b743523218)</td>

<td rowspan="1" colSpan="1" >获取历史消息高级接口</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[revokeMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a2ef856a792923811e9d16ed7a101336a)</td>

<td rowspan="1" colSpan="1" >撤回消息，消息对象可以由 createXXXMessage 接口创建得来</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[modifyMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a7609c2dd8550e43b23d24069200d37cb)</td>

<td rowspan="1" colSpan="1" >消息变更</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteMessageFromLocalStorage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a2bb42528f4d166ac826914094655841c)</td>

<td rowspan="1" colSpan="1" >删除本地消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteMessages](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a9e394ea720ecdc10d497b63b6f2b22c4)</td>

<td rowspan="1" colSpan="1" >删除本地及云端的消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[clearC2CHistoryMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a005c7767172d9a3980974b68c780c33b)</td>

<td rowspan="1" colSpan="1" >清空单聊本地及云端的消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[clearGroupHistoryMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a16c01c19a285e2bd11443c868c8256e6)</td>

<td rowspan="1" colSpan="1" >清空群聊本地及云端的消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[insertGroupMessageToLocalStorage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a9b312b67e4da19978b55a7b915815dfe)</td>

<td rowspan="1" colSpan="1" >向群组消息列表中添加一条消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[insertC2CMessageToLocalStorage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#acc1dccd310d1965248cff0d4fd5ca45f)</td>

<td rowspan="1" colSpan="1" >向单聊消息列表中添加一条消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[findMessages](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a4a0c47d706d8784656225c1e9065f6f1)</td>

<td rowspan="1" colSpan="1" >根据 msgID 查找本地消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[searchLocalMessages](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a10878d0bd326b07ec6a605c5695c7de1)</td>

<td rowspan="1" colSpan="1" >搜索本地消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[searchCloudMessages](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#ab672a5d549893b7e22c555593be40322)</td>

<td rowspan="1" colSpan="1" >搜索云端消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[sendMessageReadReceipts](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a375af7e0f3e0f0b3135ccd517de9fdd8)</td>

<td rowspan="1" colSpan="1" >发送消息已读回执</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getMessageReadReceipts](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a69192bc43e551f34f5d483dae5e70410)</td>

<td rowspan="1" colSpan="1" >获取消息已读回执</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupMessageReadMemberList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#aa345a87cfa4da2983f878bb5385d0b82)</td>

<td rowspan="1" colSpan="1" >获取群消息已读群成员列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setMessageExtensions](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a2e8b8f7ef94d02823cfab0cf5b1e1fea)</td>

<td rowspan="1" colSpan="1" >设置消息扩展</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getMessageExtensions](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a3ae68d2d8aeff6abd21981914836dc1a)</td>

<td rowspan="1" colSpan="1" >获取消息扩展</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteMessageExtensions](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#af3fad5575625e7597a482375d7a65fa6)</td>

<td rowspan="1" colSpan="1" >删除消息扩展</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addMessageReaction](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a425d818c392bef6c6daeddef8c9c0cc1)</td>

<td rowspan="1" colSpan="1" >添加消息回应</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeMessageReaction](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a88d3bf59edf75dd06ef9067b08b7db00)</td>

<td rowspan="1" colSpan="1" >删除消息回应</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getMessageReactions](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#ab3d6d68379e25750ba1b0154d956e62c)</td>

<td rowspan="1" colSpan="1" >批量拉取多条消息回应信息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getAllUserListOfMessageReaction](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#af26823c8deb12d0b0c5dc885431da182)</td>

<td rowspan="1" colSpan="1" >分页拉取消息回应全部用户资料</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[translateText](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#aee0c1e26b0401576ee82967698da35f6)</td>

<td rowspan="1" colSpan="1" >翻译文本消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[pinGroupMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a4bd9a32e4525e75778708bfde5b95c62)</td>

<td rowspan="1" colSpan="1" >设置群消息置顶</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getPinnedGroupMessageList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#afee75362418c0dbd3f2337fea5865179)</td>

<td rowspan="1" colSpan="1" >获取已置顶的群消息列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[markC2CMessageAsRead](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#acb3a67bd2fa131b50c611a48fa78f34d)</td>

<td rowspan="1" colSpan="1" >设置单聊（C2C）消息已读（待废弃接口，请使用 [cleanConversationUnreadMessageCount](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Conversation_08.html#a820c2f598f7554428fb980df3f7357f0) 接口）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[markGroupMessageAsRead](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a7fc79e30877b8d77fbdfa24e057376dc)</td>

<td rowspan="1" colSpan="1" >设置群组消息已读（待废弃接口，请使用 [cleanConversationUnreadMessageCount](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Conversation_08.html#a820c2f598f7554428fb980df3f7357f0) 接口）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[markAllMessageAsRead](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a53d889a6242b5551aa3655e40967a62f)</td>

<td rowspan="1" colSpan="1" >标记所有会话为已读（待废弃接口，请使用 [cleanConversationUnreadMessageCount](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Conversation_08.html#a820c2f598f7554428fb980df3f7357f0) 接口）</td>
</tr>
</table>


## 群组相关接口

腾讯云 IM SDK 支持五种预设的群组类型，每种类型都有其适用场景：
- 工作群（Work） ：类似普通微信群，创建后不能自由加入，必须由已经在群的用户邀请入群，同旧版本中的 Private。

- 公开群（Public）   ：类似 QQ 群，用户申请加入，但需要群主或管理员审批。

- 会议群（Meeting）：适合跟 [TRTC](https://cloud.tencent.com/product/trtc) 结合实现视频会议和在线教育等场景，支持随意进出，支持查看进群前的历史消息，同旧版本中的 ChatRoom。

- 社群（Community）：创建后可以随意进出，适合用于知识分享和游戏交流等超大社区群聊场景。该功能支持终端 SDK 5.8.1668增强版及以上版本、Web SDK 2.17.0及以上版本，需 [购买旗舰版或企业版套餐包](https://buy.cloud.tencent.com/avc?from=17182) 并在 [控制台](https://console.cloud.tencent.com/im) > **功能配置 **> **群组配置 **> **群功能配置 **> **社群**中开通。

- 直播群（AVChatRoom）：适合直播弹幕聊天室等场景，支持随意进出，人数无上限。

<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGroupListener](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a74de68e55d787fd1d4ec83b99cd1fcab)</td>

<td rowspan="1" colSpan="1" >设置群组监听器（待废弃接口，请使用 addGroupListener 和 removeGroupListener 接口）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addGroupListener](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#af583b113cdec570b08ae80d682fba52c)</td>

<td rowspan="1" colSpan="1" >添加群组监听器</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeGroupListener](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a2b2093489bf869f70c03be39f4ed08a1)</td>

<td rowspan="1" colSpan="1" >移除群组监听器</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createGroup](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a3bbcf819c1ec70e520b7f9a42cfbb989)</td>

<td rowspan="1" colSpan="1" >创建群组（简单版本）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createGroup](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a59824434b6096180b94d8152183dcd2c)</td>

<td rowspan="1" colSpan="1" >创建群组（高级版本），可在建群同时设置群信息和初始的群成员</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[joinGroup](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a4762156b7a98489eb4715de53028e12a)</td>

<td rowspan="1" colSpan="1" >加入群组</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[quitGroup](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#ac2a43b3ada447131df0c5f19e8079be5)</td>

<td rowspan="1" colSpan="1" >退出群组</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[dismissGroup](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a5bd55cb04867985253949d8cc78f860e)</td>

<td rowspan="1" colSpan="1" >解散群组（仅群主和管理员可以解散）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getJoinedGroupList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a4599e99791c150cc9f3e2492e8b4ce04)</td>

<td rowspan="1" colSpan="1" >获取已经加入的群列表（不包括已加入的直播群）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupsInfo](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a9bca7e5318cfed44335566a783a6b568)</td>

<td rowspan="1" colSpan="1" >拉取群资料</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[searchGroups](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#ac9a960921e512621340159d82a4b5259)</td>

<td rowspan="1" colSpan="1" >搜索本地群资料</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[searchCloudGroups](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a8c3f83c844be3c8bb13fe9cec6fd658a)</td>

<td rowspan="1" colSpan="1" >搜索云端群资料</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGroupInfo](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#aa9519a479493e56d7920e40aba796144)</td>

<td rowspan="1" colSpan="1" >修改群资料</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[initGroupAttributes](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a1b3a56dfc345f1ef2a575cb36156e745)</td>

<td rowspan="1" colSpan="1" >初始化群属性</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGroupAttributes](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a134342ddb51d1ee83f3981ed91d26885)</td>

<td rowspan="1" colSpan="1" >设置群属性</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteGroupAttributes](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#aa504ffca9492580ca27a45f78a87e2cb)</td>

<td rowspan="1" colSpan="1" >删除群属性</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupAttributes](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#ac8a74db230669d1b49da47bb0895cbf9)</td>

<td rowspan="1" colSpan="1" >获取群属性</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupOnlineMemberCount](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#ada2eadb44f6865e9848df94fb5bae4ae)</td>

<td rowspan="1" colSpan="1" >获取群在线人数</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGroupCounters](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a712b2338d3ea7b8e810111db12709c35)</td>

<td rowspan="1" colSpan="1" >设置群计数器</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupCounters](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#ab4e9e7fd4c6db5f979faf7f103dc5bd6)</td>

<td rowspan="1" colSpan="1" >获取群计数器</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[increaseGroupCounter](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a58647ae926410735a0e9b83c3ae05406)</td>

<td rowspan="1" colSpan="1" >递增群计数器</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[decreaseGroupCounter](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a9fb85e6cf4ad0e538de955c46833bafb)</td>

<td rowspan="1" colSpan="1" >递减群计数器</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupMemberList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a98681b9036e73acbe8f84737b5291326)</td>

<td rowspan="1" colSpan="1" >获取群成员列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupMembersInfo](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a1ab284b80811bcc697d689d7b97edf04)</td>

<td rowspan="1" colSpan="1" >获取指定的群成员资料</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[searchGroupMembers](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a35ceb734976c833047cceb8b31055b18)</td>

<td rowspan="1" colSpan="1" >搜索本地群成员资料</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[searchCloudGroupMembers](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#ae2f92bf458c5b6ef0149d66de7a01896)</td>

<td rowspan="1" colSpan="1" >搜索云端群成员资料</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGroupMemberInfo](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a40b97ee4b138f93e1b2073d1bdff3756)</td>

<td rowspan="1" colSpan="1" >修改指定的群成员资料</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[muteGroupMember](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#aa8a0206f75d75400b517f7e0d80fe9ee)</td>

<td rowspan="1" colSpan="1" >禁言</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[muteAllGroupMembers](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a7749c65c3adca4a48611ab4265407cf6)</td>

<td rowspan="1" colSpan="1" >禁言全体群成员</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[inviteUserToGroup](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a942d75fdea66e22cdbd8c131cf18e1ea)</td>

<td rowspan="1" colSpan="1" >邀请他人入群</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[kickGroupMember](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a0581f28fddf2ade890aa62e4318d7a97)</td>

<td rowspan="1" colSpan="1" >踢人</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGroupMemberRole](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a0f1c341a3dc53d6a6557a438b0c64b65)</td>

<td rowspan="1" colSpan="1" >切换群成员的角色</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[markGroupMemberList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a21238536e7cb2c3fd086797e7dc1b970)</td>

<td rowspan="1" colSpan="1" >标记群成员</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[transferGroupOwner](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a58a2ffae60505a43984fe21bf0bc1101)</td>

<td rowspan="1" colSpan="1" >转让群主</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[kickGroupMember](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a0581f28fddf2ade890aa62e4318d7a97)</td>

<td rowspan="1" colSpan="1" >踢人</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupApplicationList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a29c36ad685159850a30d61a6b9c637e8)</td>

<td rowspan="1" colSpan="1" >获取加群的申请列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[acceptGroupApplication](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a51bb9b4f965cb3d01546fef348ac75e4)</td>

<td rowspan="1" colSpan="1" >同意某一条加群申请</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[refuseGroupApplication](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#a46aa78c54986b2c0b7cc0012a3dc94ef)</td>

<td rowspan="1" colSpan="1" >拒绝某一条加群申请</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGroupApplicationRead](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Group_08.html#ade11e93b96206ef851641c42788132d1)</td>

<td rowspan="1" colSpan="1" >标记申请列表为已读</td>
</tr>
</table>


## 社群话题相关接口

如果您需要在社群下创建话题，请使用这套接口。社群用来管理群成员，社群下的所有话题不仅可以共享社群成员，还可以独立收发消息而不相互干扰。
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addCommunityListener](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Community_08.html#a81eb155a16e6b43927ced7bbf656dd84)</td>

<td rowspan="1" colSpan="1" >添加社群监听器</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeCommunityListener](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Community_08.html#ae6f37357363d362bb2f1348dec7c0cb4)</td>

<td rowspan="1" colSpan="1" >移除社群监听器</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createCommunity](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Community_08.html#afeb826964ea5882c5077bda33b8a5853)</td>

<td rowspan="1" colSpan="1" >创建支持话题的社群</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getJoinedCommunityList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Community_08.html#a17350dec83b7cd32d308a1f2b2827fdd)</td>

<td rowspan="1" colSpan="1" >获取当前用户已经加入的支持话题的社群列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createTopicInCommunity](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Community_08.html#a8cc04d04254867787060cf1cae0fc5b8)</td>

<td rowspan="1" colSpan="1" >创建话题</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteTopicFromCommunity](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Community_08.html#a31b726136637a58b5bb246eaac41187c)</td>

<td rowspan="1" colSpan="1" >删除话题</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setTopicInfo](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Community_08.html#a237e2fa6e16e55143c516c5428a23936)</td>

<td rowspan="1" colSpan="1" >修改话题信息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getTopicInfoList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Community_08.html#af93ad10e0e2b21d6ae3c8ec45021b159)</td>

<td rowspan="1" colSpan="1" >获取话题列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createPermissionGroupInCommunity](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Community_08.html#a476609aac093b8d0aa3404992c4919bd)</td>

<td rowspan="1" colSpan="1" >创建社群权限组</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deletePermissionGroupFromCommunity](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Community_08.html#a63e60a9a9f671f176d570ce245f8ea5f)</td>

<td rowspan="1" colSpan="1" >删除社群权限组</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[modifyPermissionGroupInfoInCommunity](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Community_08.html#a70b591fc96714320a4e7b12212cc4211)</td>

<td rowspan="1" colSpan="1" >修改社群权限组</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getJoinedPermissionGroupListInCommunity](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Community_08.html#a4cb129d433f107489f11e99354643d76)</td>

<td rowspan="1" colSpan="1" >获取已加入的社群权限组列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getPermissionGroupListInCommunity](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Community_08.html#a63b062f9695c3d6b0fe8129b6811b1e7)</td>

<td rowspan="1" colSpan="1" >获取社群权限组列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addCommunityMembersToPermissionGroup](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Community_08.html#a581cfc8070a6c6aa37bf54c0f496a2c4)</td>

<td rowspan="1" colSpan="1" >向社群权限组添加成员</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeCommunityMembersFromPermissionGroup](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Community_08.html#a266ab0a4ca2bf77daf84b96dadea5e93)</td>

<td rowspan="1" colSpan="1" >从社群权限组删除成员</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getCommunityMemberListInPermissionGroup](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Community_08.html#ae9099678b494dd0c442e0075b3abab99)</td>

<td rowspan="1" colSpan="1" >获取社群权限组成员列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addTopicPermissionToPermissionGroup](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Community_08.html#a538a722d29fa2e0f2841b70cb6e050f4)</td>

<td rowspan="1" colSpan="1" >向权限组添加话题权限</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteTopicPermissionFromPermissionGroup](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Community_08.html#a62e4be9f54405ddb0f16a158fb1b410f)</td>

<td rowspan="1" colSpan="1" >从权限组中删除话题权限</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[modifyTopicPermissionInPermissionGroup](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Community_08.html#acad1c1d96c6860cf2a29643fbe8b6c7f)</td>

<td rowspan="1" colSpan="1" >修改权限组中的话题权限</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getTopicPermissionInPermissionGroup](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Community_08.html#a7370db7c5f09c8106cd27c142d386262)</td>

<td rowspan="1" colSpan="1" >获取权限组中的话题权限</td>
</tr>
</table>


## 会话列表相关接口

会话列表，即登录微信或 QQ 后首屏看到的列表，包含会话节点、会话名称、群名称、最后一条消息以及未读消息数等元素。
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setConversationListener](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Conversation_08.html#a95bac7330779a8a970fc7689e436257f)</td>

<td rowspan="1" colSpan="1" >设置会话监听器 （待废弃接口，请使用 addConversationListener 和 removeConversationListener 接口）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addConversationListener](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Conversation_08.html#a39b4f352f1740171fb56143149201cd9)</td>

<td rowspan="1" colSpan="1" >添加会话监听器</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeConversationListener](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Conversation_08.html#ab9e1627559fb4259228b4e547b192c83)</td>

<td rowspan="1" colSpan="1" >移除会话监听器</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getConversationList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Conversation_08.html#ab1f5e86e270b122cb725266d234d9dd5)</td>

<td rowspan="1" colSpan="1" >获取会话列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getConversation](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Conversation_08.html#ad4b7b80fbe0cff25027371b416ede9f9)</td>

<td rowspan="1" colSpan="1" >获取指定单个会话</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getConversationList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Conversation_08.html#af94d9d44e90da448a395e6d92b4e512e)</td>

<td rowspan="1" colSpan="1" >获取指定多个会话</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[ getConversationListByFilter](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Conversation_08.html#ac1b77eedff7f2f8742a873cf766daec9)</td>

<td rowspan="1" colSpan="1" >获取会话高级接口，可以指定会话类型、标记类型、分组名等</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteConversation](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Conversation_08.html#a142f5289632f29a603937f1d770748c6)</td>

<td rowspan="1" colSpan="1" >删除会话</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteConversationList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Conversation_08.html#a4a82f8f6e9e6b56f14e57d096b16c73c)</td>

<td rowspan="1" colSpan="1" >删除会话列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setConversationDraft](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Conversation_08.html#a462cd163c03cdce230ed3647b414382b)</td>

<td rowspan="1" colSpan="1" >设置会话草稿</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setConversationCustomData](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Conversation_08.html#af82623b98c07f36767a47c59f5a23927)</td>

<td rowspan="1" colSpan="1" >设置会话自定义数据</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[pinConversation](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Conversation_08.html#a06cefb398f5a327dff4cefe6fb18c5b8)</td>

<td rowspan="1" colSpan="1" >置顶会话</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[markConversation](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Conversation_08.html#a77c02a146f774979e1e04d7334cd2d06)</td>

<td rowspan="1" colSpan="1" >标记会话</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getTotalUnreadMessageCount](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Conversation_08.html#abe76208f616713a09df582a6c1665d38)</td>

<td rowspan="1" colSpan="1" >获取会话总未读数</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getUnreadMessageCountByFilter](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Conversation_08.html#a6ddcab75125f4b09e8bfc4521817d09d)</td>

<td rowspan="1" colSpan="1" >获取根据 filter 过滤的会话未读总数</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[subscribeUnreadMessageCountByFilter](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Conversation_08.html#a123e1e578a92fa68b7087857c816fbd2)</td>

<td rowspan="1" colSpan="1" >注册监听指定 filter 的会话未读总数变化</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[unsubscribeUnreadMessageCountByFilter](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Conversation_08.html#ae87d91af763df945ed4750cbda079bf2)</td>

<td rowspan="1" colSpan="1" >取消监听指定 filter 的会话未读总数变化</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[cleanConversationUnreadMessageCount](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Conversation_08.html#a820c2f598f7554428fb980df3f7357f0)</td>

<td rowspan="1" colSpan="1" >清理会话的未读消息计数</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[ createConversationGroup](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Conversation_08.html#a2f5f4587c881aa26fbdce3b4d469aa0a)</td>

<td rowspan="1" colSpan="1" >创建会话分组</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[ getConversationGroupList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Conversation_08.html#a037b0973be9feef207a64f2e043792ab)</td>

<td rowspan="1" colSpan="1" >获取会话分组列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[ deleteConversationGroup](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Conversation_08.html#aa7b91ded9e451335bc931525839ce736)</td>

<td rowspan="1" colSpan="1" >删除会话分组</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[ renameConversationGroup](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Conversation_08.html#a1a9492196c94450b2992079cffab96a6)</td>

<td rowspan="1" colSpan="1" >重命名会话分组</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[ addConversationsToGroup](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Conversation_08.html#a37c78d27216882504d2710a066478db5)</td>

<td rowspan="1" colSpan="1" >添加会话到一个会话分组</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[ deleteConversationsFromGroup](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Conversation_08.html#a16ee46fa4b7278a0386be9ff633fa552)</td>

<td rowspan="1" colSpan="1" >从一个会话分组中删除会话</td>
</tr>
</table>


## 用户资料相关接口

包含查询用户资料、修改个人资料以及屏蔽某人消息（即把某用户加入黑名单中）的相关接口。
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getUsersInfo](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#ac638c1dd6ec1e5204637e4b87129cd38)</td>

<td rowspan="1" colSpan="1" >获取用户资料</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setSelfInfo](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a328a0d2d07e8d34e12effb73937c3437)</td>

<td rowspan="1" colSpan="1" >修改个人资料</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[subscribeUserInfo](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a4d14dda5e99d821c84dea4ae25e403af)</td>

<td rowspan="1" colSpan="1" >订阅用户资料</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[unsubscribeUserInfo](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#af42e383f564f7d5bb9b4d39a3e00d4d9)</td>

<td rowspan="1" colSpan="1" >取消订阅用户资料</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getUserStatus](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#abe44a4c51c686248d483674d77d71053)</td>

<td rowspan="1" colSpan="1" >订阅用户资料</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setSelfStatus](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a7d771431a61635888bdc4def438c4328)</td>

<td rowspan="1" colSpan="1" >取消订阅用户资料</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[subscribeUserStatus](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a20e6cbe409549e0d2ff62be76914e0b3)</td>

<td rowspan="1" colSpan="1" >订阅用户状态</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[unsubscribeUserStatus](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a3780734bb50398ebe65155c3223542f0)</td>

<td rowspan="1" colSpan="1" >取消订阅用户状态</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[searchUsers](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMManager.html#a978df4d80011f4da38dc80f8ab217f48)</td>

<td rowspan="1" colSpan="1" >搜索云端用户资料</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addToBlackList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a67d998da5085b5004bb6aa8d4322022c)</td>

<td rowspan="1" colSpan="1" >屏蔽某人的消息（添加该用户到黑名单中）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteFromBlackList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#aa7e69a67185eaca658ba429cf6309a5f)</td>

<td rowspan="1" colSpan="1" >取消某人的消息屏蔽（把该用户从黑名单中移除）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getBlackList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a0d854d64c8ae936014a8424d55508fa3)</td>

<td rowspan="1" colSpan="1" >获取黑名单列表</td>
</tr>
</table>


## 离线推送相关接口

如果想要在 App 切后台时依然能够实时收到 IM 消息，可以使用离线推送服务，详细配置请参考 [离线推送](https://cloud.tencent.com/document/product/269/75429)。
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setAPNSListener](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07APNS_08.html#a62e1694cf9e1d65b76f90064cbcbb683)</td>

<td rowspan="1" colSpan="1" >设置 APNs 监听</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setAPNS](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07APNS_08.html#a73bf19c0c019e5e27ec441bc753daa9e)</td>

<td rowspan="1" colSpan="1" >配置 APNS 推送信息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setVOIP](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07VOIP_08.html#a0bd652eed597771ca1381d0d6ea67704)</td>

<td rowspan="1" colSpan="1" >配置 VOIP 推送信息</td>
</tr>
</table>


## 好友管理相关接口

腾讯云 IM 在收发消息时默认不检查是不是好友关系，您可以在 [**控制台**](https://console.cloud.tencent.com/im) >**功能配置**>**登录与消息**>**好友关系检查**中开启"发送单聊消息检查关系链"开关，并使用如下接口增删好友和管理好友列表。
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setFriendListener](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#acd403f586f3df84f56b1b757efb2d443)</td>

<td rowspan="1" colSpan="1" >设置关系链与好友资料监听器（待废弃接口，请使用 addFriendListener 和 removeFriendListener 接口）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addFriendListener](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a1de011b63b3c20b1be519dc7ba124704)</td>

<td rowspan="1" colSpan="1" >添加关系链监听器</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeFriendListener](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#aed40ccbbc4e15be79154077a6d3ec085)</td>

<td rowspan="1" colSpan="1" >移除关系链监听器</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getFriendList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a81131d76924a03ec2b593addd6e4e101)</td>

<td rowspan="1" colSpan="1" >获取好友列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getFriendsInfo](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a39f6752da11b595e4a5b6dcb0eb6a584)</td>

<td rowspan="1" colSpan="1" >获取指定好友资料</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setFriendInfo](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#ac258312c000c1af69fcf51dd6898b74b)</td>

<td rowspan="1" colSpan="1" >设置指定好友资料</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[searchFriends](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a9a036dcc1bd65474a3d2e90f2bb6b9c6)</td>

<td rowspan="1" colSpan="1" >搜索好友列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addFriend](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#ac1ea1c7de2bfc2b0a25e5f6b3192e304)</td>

<td rowspan="1" colSpan="1" >添加好友</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteFromFriendList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#af967134fb177b32d4060fedf3663ace3)</td>

<td rowspan="1" colSpan="1" >删除好友</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[checkFriend](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#aad1b09fab6523d9a36147b4ed4efac67)</td>

<td rowspan="1" colSpan="1" >检查指定用户的好友关系</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getFriendApplicationList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#acda7968f1e9adc12261a7e533d709a1c)</td>

<td rowspan="1" colSpan="1" >获取好友申请列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[acceptFriendApplication](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a51b913927028025e2e450e6e8ce848c0)</td>

<td rowspan="1" colSpan="1" >同意好友申请</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[refuseFriendApplication](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a406b964a6513219cfe4803f87f0f00f8)</td>

<td rowspan="1" colSpan="1" >拒绝好友申请</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteFriendApplication](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a363e0622f653694999293c595d552896)</td>

<td rowspan="1" colSpan="1" >删除好友申请</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setFriendApplicationRead](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#ad46c70c18b8f69bf272cbf3466477a85)</td>

<td rowspan="1" colSpan="1" >设置好友申请已读</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createFriendGroup](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a8b33edab15ae7d179e4e2d885e7d2b7d)</td>

<td rowspan="1" colSpan="1" >新建好友分组</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getFriendGroups](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a63f3eaae567586077d5a8d27c31e2229)</td>

<td rowspan="1" colSpan="1" >获取分组信息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteFriendGroup](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a2dc49f2abb1238fc2d47ce6d4f14c1e7)</td>

<td rowspan="1" colSpan="1" >删除好友分组</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[renameFriendGroup](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a93f6ba132d9706db7c74daff97a2abd0)</td>

<td rowspan="1" colSpan="1" >修改好友分组的名称</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addFriendsToFriendGroup](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a0265241c39600c390406ca1f8f6ff75d)</td>

<td rowspan="1" colSpan="1" >添加好友到一个好友分组</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteFriendsFromFriendGroup](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a4a14a878816c8d6a20981d1903fcf359)</td>

<td rowspan="1" colSpan="1" >从好友分组中删除好友</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[subscribeOfficialAccount](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a0209825847b854bafdd337aab3c43f02)</td>

<td rowspan="1" colSpan="1" >订阅公众号</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[unsubscribeOfficialAccount](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a44a804583ee8dd3eac2a6cab7c8d5fe1)</td>

<td rowspan="1" colSpan="1" >取消订阅公众号</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getOfficialAccountsInfo](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#acdf22b26fe5b6d40b2d7d411a361f904)</td>

<td rowspan="1" colSpan="1" >获取公众号列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[followUser](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a7cde546df61efd1327db38c37f905d31)</td>

<td rowspan="1" colSpan="1" >关注用户</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[unfollowUser](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#ad15c2c5f7ba04f58046ddc23fa84b697)</td>

<td rowspan="1" colSpan="1" >取消关注用户</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getMyFollowingList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#aa4f6480569a8b98066e551ae2d9cf0cf)</td>

<td rowspan="1" colSpan="1" >获取我的关注列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getMutualFollowersList](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#ada4fc3b4b1e9a044e73a4b2330d93100)</td>

<td rowspan="1" colSpan="1" >获取我的互关列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getUserFollowInfo](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a6a01145bcdfba7fe49d7882fac047b29)</td>

<td rowspan="1" colSpan="1" >获取指定用户的 关注/粉丝/互关 数量信息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[checkFollowType](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Friendship_08.html#a6a01145bcdfba7fe49d7882fac047b29)</td>

<td rowspan="1" colSpan="1" >检查指定用户的关注类型</td>
</tr>
</table>


