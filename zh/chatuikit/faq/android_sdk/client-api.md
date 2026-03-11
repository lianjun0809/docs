> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

> **注意：**
> 

> 新老版本 API 请勿混合使用。
> 


## 初始化登录接口

初始化并成功登录，是正常使用腾讯云 IM 服务的前提。
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[initSDK](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#ac905c315726b517ba62421471bbecf56)</td>

<td rowspan="1" colSpan="1" >初始化 SDK</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[unInitSDK](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a8ac73b4f71f9d9a1ca01551c919d3cdd)</td>

<td rowspan="1" colSpan="1" >unsubscribeUserInfo 反初始化 SDK</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addIMSDKListener](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a2f0297e96d365013e7923275ce2a5d4e)</td>

<td rowspan="1" colSpan="1" >添加 IM 监听</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeIMSDKListener](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a9b98e6b9ac0f883f055ef82563467b43)</td>

<td rowspan="1" colSpan="1" >移除 IM 监听</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getVersion](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a8142d4e71e0ee1b8d2ec99740e2cb1ca)</td>

<td rowspan="1" colSpan="1" >获取版本号</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getServerTime](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a0f95b1e166f22d261e73fbf01987fb0f)</td>

<td rowspan="1" colSpan="1" >获取服务器当前时间</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[login](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a73fc0e14c5f2f5fc06a80081479fb416)</td>

<td rowspan="1" colSpan="1" >登录</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[logout](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a0398924fa1b62a8f5cc9b51673273b48)</td>

<td rowspan="1" colSpan="1" >登出</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getLoginStatus](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a1836146275265b2a120412f18961db95)</td>

<td rowspan="1" colSpan="1" >获取登录状态</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getLoginUser](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#ad4b2e5a7df5e786ba369054ac582007f)</td>

<td rowspan="1" colSpan="1" >获取当前登录用户的 UserID</td>
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
<td rowspan="1" colSpan="1" >[addSimpleMsgListener](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#afd96fd1591e41f031421c0655d8e5d6b)</td>

<td rowspan="1" colSpan="1" >设置基本消息（文本消息和自定义消息）的事件监听器，请不要同  [addAdvancedMsgListener](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#aaccdec10b9fbee5e43eaf908e359c823)  混用</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeSimpleMsgListener](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a86ac462d87f652960d2600a52009849a)</td>

<td rowspan="1" colSpan="1" >移除基本消息（文本消息和自定义消息）的事件监听器</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[sendC2CTextMessage](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a59a8ba6e4a973b4c40a09ae7dfdc6981)</td>

<td rowspan="1" colSpan="1" >发送单聊（C2C）普通文本消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[sendC2CCustomMessage](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#af3e08b936df77210c6cdd0ce5c7fa87f)</td>

<td rowspan="1" colSpan="1" >发送单聊（C2C）自定义（信令）消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[sendGroupTextMessage](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a56359fd1ce0a96f289dcd4bef522fb52)</td>

<td rowspan="1" colSpan="1" >发送群聊普通文本消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[sendGroupCustomMessage](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#afbce8ff97be0a3a42c7dc826d316f2c2)</td>

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
<td rowspan="1" colSpan="1" >[addSignalingListener](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSignalingManager.html#a862073ac16de7f02e5f97b8cbe7eb028)</td>

<td rowspan="1" colSpan="1" >添加信令监听</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeSignalingListener](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSignalingManager.html#a72f6c032de1b0dbaabb227be54d0bcfc)</td>

<td rowspan="1" colSpan="1" >移除信令监听</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[invite](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSignalingManager.html#a3c0592962ef89e1075f3136fc7117da0)</td>

<td rowspan="1" colSpan="1" >邀请某个人</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[inviteInGroup](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSignalingManager.html#a4d166ca73210308fbd79fca748145671)</td>

<td rowspan="1" colSpan="1" >邀请群内的某些人</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[cancel](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSignalingManager.html#a9d69707620f038d6e47356cdaa3ab9bd)</td>

<td rowspan="1" colSpan="1" >邀请方取消邀请</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[accept](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSignalingManager.html#a4cd3629a0952db7c59186e0c222e17a0)</td>

<td rowspan="1" colSpan="1" >接收方接收邀请</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[reject](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSignalingManager.html#ad9510bf8a333189fd1a0c1eafbde2266)</td>

<td rowspan="1" colSpan="1" >接收方拒绝邀请</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getSignalingInfo](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSignalingManager.html#ab303f20f53de134e6f6ebe5f9f9bcad0)</td>

<td rowspan="1" colSpan="1" >获取信令信息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addInvitedSignaling](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSignalingManager.html#ac50301e05e1672b771dc2c92fadff8de)</td>

<td rowspan="1" colSpan="1" >添加邀请信令（可以用于群离线推送消息触发的邀请信令）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[modifyInvitation](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSignalingManager.html#a5f3eba1a04cfd667b409e0b90478c895)</td>

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
<td rowspan="1" colSpan="1" >[addAdvancedMsgListener](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#aaccdec10b9fbee5e43eaf908e359c823)</td>

<td rowspan="1" colSpan="1" >设置高级消息的事件监听器，请不要同 [addSimpleMsgListener](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#afd96fd1591e41f031421c0655d8e5d6b) 混用</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeAdvancedMsgListener](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a44e1e9126bf5b30234330fe19259cd93)</td>

<td rowspan="1" colSpan="1" >移除高级消息的事件监听器</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createTextMessage](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a3ea254cd12aa0bcfd004f26f759b76a0)</td>

<td rowspan="1" colSpan="1" >创建文本消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createCustomMessage](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a313b1ea616f082f535946c83edd2cc7f)</td>

<td rowspan="1" colSpan="1" >创建自定义消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createImageMessage](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#adef5bc7a67b9a69f70f6417fd810d4b1)</td>

<td rowspan="1" colSpan="1" >创建图片消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createSoundMessage](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a7e661ce2b4eba1535bd04f3b6539b9dc)</td>

<td rowspan="1" colSpan="1" >创建语音消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createVideoMessage](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#ada17dbc78e9876a8f3a9fd24a73752b5)</td>

<td rowspan="1" colSpan="1" >创建视频消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createFileMessage](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a39e4b6609321fd188a2e156a00bb3135)</td>

<td rowspan="1" colSpan="1" >创建文件消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createLocationMessage](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a67cebe27192392080fc80a86c80a4321)</td>

<td rowspan="1" colSpan="1" >创建地理位置消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createFaceMessage](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a7ad0f3b7eff3978c12d8c912ca164a5d)</td>

<td rowspan="1" colSpan="1" >创建表情消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createMergerMessage](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#acebe275789ab49cc8abe6af5e07aa3b0)</td>

<td rowspan="1" colSpan="1" >创建合并转发消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createForwardMessage](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#af8f609bfbfe99a0c65611b14159b6b4d)</td>

<td rowspan="1" colSpan="1" >创建单条转发消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createTargetedGroupMessage](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a4def1515746b2840e4b82047a53b91a2)</td>

<td rowspan="1" colSpan="1" >创建定向群消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createAtSignedGroupMessage](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a23c5c1305996f09c7ff004854b551877)</td>

<td rowspan="1" colSpan="1" >创建带 @ 标记的群消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[sendMessage](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a28e01403acd422e53e999f21ec064795)</td>

<td rowspan="1" colSpan="1" >发送消息，消息对象可以由 createXXXMessage 接口创建得来</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setC2CReceiveMessageOpt](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a6524143895cdee25fabd9aeeae73a3c5)</td>

<td rowspan="1" colSpan="1" >设置单聊消息免打扰</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getC2CReceiveMessageOpt](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a9693dd66432f931ac0a1f2168d899501)</td>

<td rowspan="1" colSpan="1" >获取单聊消息免打扰状态</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGroupReceiveMessageOpt](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a2735427ac22485626aea278a9d465b3e)</td>

<td rowspan="1" colSpan="1" >设置群聊消息免打扰状态</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setAllReceiveMessageOpt](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a21424ee9df839376ad67d824f95ceb51)</td>

<td rowspan="1" colSpan="1" >设置全局消息免打扰状态（可实现按天重复）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setAllReceiveMessageOpt](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a5664f8d53ae660f98c84ff2877e9e036)</td>

<td rowspan="1" colSpan="1" >设置全局消息免打扰状态</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getAllReceiveMessageOpt](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a0a0f68cf02affa07963e13e388400f51)</td>

<td rowspan="1" colSpan="1" >获取全局消息免打扰状态</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getC2CHistoryMessageList](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#afedccbe0e5229ae15e0e07b722ea39df)</td>

<td rowspan="1" colSpan="1" >获取单聊（C2C）历史消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupHistoryMessageList](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a671e8737fcea0c05dc661c753e5b3597)</td>

<td rowspan="1" colSpan="1" >获取群组历史消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getHistoryMessageList](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a97fe2d6a7bab8f45b758f84df48c0b12)</td>

<td rowspan="1" colSpan="1" >获取历史消息高级接口</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[revokeMessage](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#ad0dfce6be749165cd90a9ff67a1308b1)</td>

<td rowspan="1" colSpan="1" >撤回消息，消息对象可以由 createXXXMessage 接口创建得来</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[modifyMessage](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a5464602189e6af536540e86e8bcbbe73)</td>

<td rowspan="1" colSpan="1" >消息变更</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[markC2CMessageAsRead](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a7c09d0ba4a8018f5f9eec4760c4c7b9b)</td>

<td rowspan="1" colSpan="1" >设置单聊（C2C）消息已读 (待废弃接口，请使用 [cleanConversationUnreadMessageCount](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a5887d1954d32fad68bc569e6f136770d) 接口)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[markGroupMessageAsRead](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#ac0a65f18d361abde8a0ac16132027e69)</td>

<td rowspan="1" colSpan="1" >设置群组消息已读 (待废弃接口，请使用 [cleanConversationUnreadMessageCount](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a5887d1954d32fad68bc569e6f136770d) 接口)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[markAllMessageAsRead](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#ad097a0da2ea0002f2b0f2d1d11f3a4ab)</td>

<td rowspan="1" colSpan="1" >标记所有会话为已读 (待废弃接口，请使用 [cleanConversationUnreadMessageCount](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a5887d1954d32fad68bc569e6f136770d) 接口)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteMessageFromLocalStorage](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#aa31e3b48fb666b970120fc0bc6343534)</td>

<td rowspan="1" colSpan="1" >删除本地消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteMessages](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#adb346fede13d493e415f6574df911e9a)</td>

<td rowspan="1" colSpan="1" >删除本地及云端的消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[clearC2CHistoryMessage](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a29aa6e75c2238c35cc609bef0e5a46ce)</td>

<td rowspan="1" colSpan="1" >清空单聊本地及云端的消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[clearGroupHistoryMessage](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a6e1a1dce441243d0bd5ac2f8bcecb3d9)</td>

<td rowspan="1" colSpan="1" >清空群聊本地及云端的消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[insertGroupMessageToLocalStorage](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a04a3f6c250f9d6c0053fd71be74f047f)</td>

<td rowspan="1" colSpan="1" >向群组消息列表中添加一条消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[insertC2CMessageToLocalStorage](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a5afe4461b4a47205d2865ea94317d4aa)</td>

<td rowspan="1" colSpan="1" >向单聊消息列表中添加一条消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[findMessages](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#ad0dbaec04bc389d01f815f46c550e2fd)</td>

<td rowspan="1" colSpan="1" >根据 msgID 查找本地消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[searchLocalMessages](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a9364c8a0c6a0899b17c0a479b8ca848a)</td>

<td rowspan="1" colSpan="1" >搜索本地消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[searchCloudMessages](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a16a4a38b3f08bf7707d949ba9674102f)</td>

<td rowspan="1" colSpan="1" >搜索云端消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[sendMessageReadReceipts](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a66ec09cb444ddca989e9518d5118275d)</td>

<td rowspan="1" colSpan="1" >发送消息已读回执</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getMessageReadReceipts](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a50e3bc679e196866057415a7c192abf6)</td>

<td rowspan="1" colSpan="1" >获取消息已读回执</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupMessageReadMemberList](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a93c48782f3e127e8a50aef1bf8829099)</td>

<td rowspan="1" colSpan="1" >获取群消息已读群成员列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setMessageExtensions](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a155f6219c2bbf7bc510beec9e905d5db)</td>

<td rowspan="1" colSpan="1" >设置消息扩展</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getMessageExtensions](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a832534327c08326d045c44b02f7ddbb7)</td>

<td rowspan="1" colSpan="1" >获取消息扩展</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteMessageExtensions](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a25c02e90cd0940d34fe3bbfd803cc278)</td>

<td rowspan="1" colSpan="1" >删除消息扩展</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addMessageReaction](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#af47c3e1fb1ac73f7e2ba7bf739c9452a)</td>

<td rowspan="1" colSpan="1" >添加消息回应</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeMessageReaction](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a8af85ef9a47c6d498c601dad1370de32)</td>

<td rowspan="1" colSpan="1" >删除消息回应</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getMessageReactions](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#aa6d5f0421950c7354dd4f0de48814881)</td>

<td rowspan="1" colSpan="1" >批量拉取多条消息回应信息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getAllUserListOfMessageReaction](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a6af80059a956df9948286dc3007d4c1f)</td>

<td rowspan="1" colSpan="1" >分页拉取消息回应全部用户资料</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[translateText](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a1e1806c27bc7b76a3b816492ed9cbe5c)</td>

<td rowspan="1" colSpan="1" >翻译文本消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[pinGroupMessage](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#aa345a7876bf0df29491429329a10f469)</td>

<td rowspan="1" colSpan="1" >设置群消息置顶</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getPinnedGroupMessageList](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a35c28770388fa0b1c51946b314287786)</td>

<td rowspan="1" colSpan="1" >获取已置顶的群消息列表</td>
</tr>
</table>


## 群组相关接口

腾讯云 IM SDK 支持五种预设的群组类型，每种类型都有其适用场景：
- 工作群（Work）	：类似普通微信群，创建后不能自由加入，必须由已经在群的用户邀请入群，同旧版本中的 Private。

- 公开群（Public）	：类似 QQ 群，用户申请加入，但需要群主或管理员审批。

- 会议群（Meeting）：适合跟 [TRTC](https://cloud.tencent.com/product/trtc) 结合实现视频会议和在线教育等场景，支持随意进出，支持查看进群前的历史消息，同旧版本中的 ChatRoom。

- 社群（Community）：创建后可以随意进出，适合用于知识分享和游戏交流等超大社区群聊场景。该功能支持终端 SDK 5.8.1668增强版及以上版本、Web SDK 2.17.0及以上版本，需 [购买旗舰版或企业版套餐包](https://buy.cloud.tencent.com/avc?from=17182) 并在 [控制台](https://console.cloud.tencent.com/im) > **功能配置 **> **群组配置 **> **群功能配置 **> **社群**中开通。

- 直播群（AVChatRoom）：适合直播弹幕聊天室等场景，支持随意进出，人数无上限。

<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addGroupListener](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a8dde0362f00a454945e7811c8a726a38)</td>

<td rowspan="1" colSpan="1" >添加群组监听器</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeGroupListener](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#ab4d57bd5fd4b2d71c29daaeee8b9b760)</td>

<td rowspan="1" colSpan="1" >移除群组监听器</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createGroup](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#af836e4912f668dddf6cc679233cfb0bb)</td>

<td rowspan="1" colSpan="1" >创建群组（简单版本）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createGroup](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a121d53137a38d0fc0bc8a8e0a9c55647)</td>

<td rowspan="1" colSpan="1" >创建群组（高级版本），可在建群同时设置群信息和初始的群成员</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[joinGroup](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#ad64a09bea508672d6d5a402b3455b564)</td>

<td rowspan="1" colSpan="1" >加入群组</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[quitGroup](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a6d140dbeb44906de9cb69f69c2ce5919)</td>

<td rowspan="1" colSpan="1" >退出群组</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[dismissGroup](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#afd0221c0c842a6dcfa0acc657e50caeb)</td>

<td rowspan="1" colSpan="1" >解散群组（仅群主和管理员可以解散）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getJoinedGroupList](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a0199b7cacc6919938d8342474bd252da)</td>

<td rowspan="1" colSpan="1" >获取已经加入的群列表（不包括已加入的直播群）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupsInfo](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ada614335043d548c11f121500e279154)</td>

<td rowspan="1" colSpan="1" >拉取群资料</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[searchGroups](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a94a72082b7e2682942f35196a7e28023)</td>

<td rowspan="1" colSpan="1" >搜索本地群资料</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[searchCloudGroups](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a322641b6386d4698dd1611fee69891e0)</td>

<td rowspan="1" colSpan="1" >搜索云端群资料</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGroupInfo](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ad4ceef92975fa00c4a5dddc8f7e1edcf)</td>

<td rowspan="1" colSpan="1" >修改群资料</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[initGroupAttributes](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a17569b57abc77adb6be9356b9eb70182)</td>

<td rowspan="1" colSpan="1" >初始化群属性</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGroupAttributes](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a3ec31101e4763dab7a1c99a71bc3da08)</td>

<td rowspan="1" colSpan="1" >设置群属性</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteGroupAttributes](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a45f211bafddc58bf5e199e18a6814578)</td>

<td rowspan="1" colSpan="1" >删除群属性</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupAttributes](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ade2155fb24ed1c0b8eb976e146c14e3d)</td>

<td rowspan="1" colSpan="1" >获取群属性</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupOnlineMemberCount](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a56840105a4b3371eeab2046d8c300bce)</td>

<td rowspan="1" colSpan="1" >获取群在线人数</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGroupCounters](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ab2359bff0ebe5a07a87242023206989f)</td>

<td rowspan="1" colSpan="1" >设置群计数器</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupCounters](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a3f70b0f1054a7bf78a9069a01b842cad)</td>

<td rowspan="1" colSpan="1" >获取群计数器</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[increaseGroupCounter](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ad770cab3620a21671d7f83776d56814e)</td>

<td rowspan="1" colSpan="1" >递增群计数器</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[decreaseGroupCounter](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ad5841f8f77442c8d0cf1a209a55db6c2)</td>

<td rowspan="1" colSpan="1" >递减群计数器</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupMemberList](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a69fc0831aacaa0585c1855f4c91320be)</td>

<td rowspan="1" colSpan="1" >获取群成员列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupMembersInfo](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#adb08e1c4fa9aff407c7b2678757f66d5)</td>

<td rowspan="1" colSpan="1" >获取指定的群成员资料</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[searchGroupMembers](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a493fb73258019961f3ca8934ff625b0a)</td>

<td rowspan="1" colSpan="1" >搜索本地群成员资料</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[searchCloudGroupMembers](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a1db4218077a0db6c623a19d66ba72b5a)</td>

<td rowspan="1" colSpan="1" >搜索云端群成员资料</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGroupMemberInfo](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a6f1cf8ede41348b4cd7b63b8e4caa77b)</td>

<td rowspan="1" colSpan="1" >修改指定的群成员资料</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[muteGroupMember](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a450230c4d129611e1b0519827ec0f8b5)</td>

<td rowspan="1" colSpan="1" >禁言</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[muteAllGroupMembers](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ab3f057b439e976b17dcc0e2e9be5e7d1)</td>

<td rowspan="1" colSpan="1" >禁言全体群成员，只有管理员或群主能够调用</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[kickGroupMember](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a6da6755c6e0c46e96cb02575074a5333)</td>

<td rowspan="1" colSpan="1" >踢人</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGroupMemberRole](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a34ebf60528d02626834f022b4ebabfa8)</td>

<td rowspan="1" colSpan="1" >切换群成员的角色</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[markGroupMemberList](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#abdd5f157904dd50012c7a93f66f85dba)</td>

<td rowspan="1" colSpan="1" >标记群成员</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[transferGroupOwner](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ac16d66c8e293c2ee95c7b673e5ad80c4)</td>

<td rowspan="1" colSpan="1" >转让群主</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[inviteUserToGroup](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#afd219107653b877e446c149531d65e92)</td>

<td rowspan="1" colSpan="1" >邀请他人入群</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupApplicationList](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a240db7bdc023ad6fc63e9ee9b72714c4)</td>

<td rowspan="1" colSpan="1" >获取加群的申请列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[acceptGroupApplication](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ad743008d30c909ef0be0f8aa91102e07)</td>

<td rowspan="1" colSpan="1" >同意某一条加群申请</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[refuseGroupApplication](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#aa518c54e77f7c0f6e7dd129d6c433acd)</td>

<td rowspan="1" colSpan="1" >拒绝某一条加群申请</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGroupApplicationRead](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a498d9d76217cbae0aa235ac928ad02d8)</td>

<td rowspan="1" colSpan="1" >标记申请列表为已读</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getJoinedCommunityList](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#acb37b83f357fc7ee04905f8bcd5a5c67)</td>

<td rowspan="1" colSpan="1" >获取当前用户已经加入的支持话题的社群列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createTopicInCommunity](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a52eed1b07ad64a3aa3d3561d8cd147f0)</td>

<td rowspan="1" colSpan="1" >创建话题</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteTopicFromCommunity](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a77c4502346e800e43c22a0f15138d699)</td>

<td rowspan="1" colSpan="1" >删除话题</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setTopicInfo](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#acaff2edad6eb208478be9ab06d30035d)</td>

<td rowspan="1" colSpan="1" >修改话题信息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getTopicInfoList](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a5d2b18a76cff650cb9bb2abf2ef07306)</td>

<td rowspan="1" colSpan="1" >获取话题列表</td>
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
<td rowspan="1" colSpan="1" >[addCommunityListener](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMCommunityManager.html#a431aca797c3047dee3b5f8db4722902d)</td>

<td rowspan="1" colSpan="1" >添加社群监听器</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeCommunityListener](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMCommunityManager.html#a96411e5a6c3896aff3bdbcf86387e928)</td>

<td rowspan="1" colSpan="1" >移除社群监听器</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createCommunity](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMCommunityManager.html#acde81364ecec194dfa20720f670d8537)</td>

<td rowspan="1" colSpan="1" >创建支持话题的社群</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getJoinedCommunityList](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMCommunityManager.html#acb37b83f357fc7ee04905f8bcd5a5c67)</td>

<td rowspan="1" colSpan="1" >获取当前用户已经加入的支持话题的社群列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createTopicInCommunity](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMCommunityManager.html#a52eed1b07ad64a3aa3d3561d8cd147f0)</td>

<td rowspan="1" colSpan="1" >创建话题</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteTopicFromCommunity](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMCommunityManager.html#a77c4502346e800e43c22a0f15138d699)</td>

<td rowspan="1" colSpan="1" >删除话题</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setTopicInfo](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMCommunityManager.html#acaff2edad6eb208478be9ab06d30035d)</td>

<td rowspan="1" colSpan="1" >修改话题信息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getTopicInfoList](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMCommunityManager.html#a5d2b18a76cff650cb9bb2abf2ef07306)</td>

<td rowspan="1" colSpan="1" >获取话题列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createPermissionGroupInCommunity](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMCommunityManager.html#a92908f8d46063504d6f8b0d0f04f3a6b)</td>

<td rowspan="1" colSpan="1" >创建社群权限组</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deletePermissionGroupFromCommunity](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMCommunityManager.html#a74e98c5144576fca599378e672b54d1f)</td>

<td rowspan="1" colSpan="1" >删除社群权限组</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[modifyPermissionGroupInfoInCommunity](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMCommunityManager.html#a2a5d15a05b455c73f5e8e8c7eab7ad0d)</td>

<td rowspan="1" colSpan="1" >修改社群权限组</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getJoinedPermissionGroupListInCommunity](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMCommunityManager.html#af3b2e3c995525d3f6be17fbd4f42ad2b)</td>

<td rowspan="1" colSpan="1" >获取已加入的社群权限组列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getPermissionGroupListInCommunity](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMCommunityManager.html#a9f6e4a2c4f4380db7b7066f9c8a13379)</td>

<td rowspan="1" colSpan="1" >获取社群权限组列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addCommunityMembersToPermissionGroup](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMCommunityManager.html#a79757d4803e94cdfe15deb4e7789e043)</td>

<td rowspan="1" colSpan="1" >向社群权限组添加成员</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeCommunityMembersFromPermissionGroup](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMCommunityManager.html#a5d48a2141728bd791129eefb9d88e262)</td>

<td rowspan="1" colSpan="1" >从社群权限组删除成员</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getCommunityMemberListInPermissionGroup](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMCommunityManager.html#a2d8f6477d76254d4dec9bd0f1a4c8051)</td>

<td rowspan="1" colSpan="1" >获取社群权限组成员列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addTopicPermissionToPermissionGroup](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMCommunityManager.html#a7e7d5b6960571ddbf61ba5a6f7390bc9)</td>

<td rowspan="1" colSpan="1" >向权限组添加话题权限</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteTopicPermissionFromPermissionGroup](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMCommunityManager.html#af3ee95182ef6b9520cb2d1c2729e575f)</td>

<td rowspan="1" colSpan="1" >从权限组中删除话题权限</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[modifyTopicPermissionInPermissionGroup](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMCommunityManager.html#a52852fc6b1c18b6a3379d25ea4001acf)</td>

<td rowspan="1" colSpan="1" >修改权限组中的话题权限</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getTopicPermissionInPermissionGroup](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMCommunityManager.html#a380f75b59c0ee32911a7cba6a2a88971)</td>

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
<td rowspan="1" colSpan="1" >[addConversationListener](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a806534684e5d4d01b94126cd1397fee4)</td>

<td rowspan="1" colSpan="1" >添加会话监听器</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeConversationListener](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a661d479b6f704a2e319d0c744b8ad2bc)</td>

<td rowspan="1" colSpan="1" >移除会话监听器</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getConversationList](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#abf71156b8b6423e98943e25a77dc1967)</td>

<td rowspan="1" colSpan="1" >获取会话列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getConversationListByFilter](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#abf71156b8b6423e98943e25a77dc1967)</td>

<td rowspan="1" colSpan="1" >获取会话高级接口，可以指定会话类型、标记类型、分组名等</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getConversation](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a619aaff2bb5664e094d2341819b95096)</td>

<td rowspan="1" colSpan="1" >获取指定单个会话</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getConversationList](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a1bb5ba2beecb4f68146e7f664124fd8b)</td>

<td rowspan="1" colSpan="1" >获取指定多个会话</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteConversation](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a7a6e38c5a7431646bd4c0c4c66279077)</td>

<td rowspan="1" colSpan="1" >删除会话</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteConversationList](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#acd95bca253be53ce89395f77c1b42c70)</td>

<td rowspan="1" colSpan="1" >删除会话列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setConversationDraft](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#ae7f2f52bf375dae69368eae42edb28ab)</td>

<td rowspan="1" colSpan="1" >设置会话草稿</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setConversationCustomData](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#ac11ca7227145e3f359f6a3473ed600a5)</td>

<td rowspan="1" colSpan="1" >设置会话自定义数据</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[pinConversation](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a4da7467f54c891c4929152260e42f4b6)</td>

<td rowspan="1" colSpan="1" >置顶会话</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[markConversation](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#aa1dab66f08df9aef4acb0aad8cb77d72)</td>

<td rowspan="1" colSpan="1" >标记会话</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getTotalUnreadMessageCount](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a08bdd15d7ee2737335a01285d7f9c44a)</td>

<td rowspan="1" colSpan="1" >获取会话总未读数</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getUnreadMessageCountByFilter](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#ad68a1302b6cb775e09c4b4277bcb0c96)</td>

<td rowspan="1" colSpan="1" >获取按会话 filter 过滤的未读总数</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[subscribeUnreadMessageCountByFilter](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a27b7c9477c5a2fb4c4f05b2e499d6f61)</td>

<td rowspan="1" colSpan="1" >注册监听指定 filter 的会话未读总数变化</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[unsubscribeUnreadMessageCountByFilter](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#adbf33f34fa911bbeec55cf3a4f320ba7)</td>

<td rowspan="1" colSpan="1" >取消监听指定 filter 的会话未读总数变化</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[cleanConversationUnreadMessageCount](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a5887d1954d32fad68bc569e6f136770d)</td>

<td rowspan="1" colSpan="1" >清理会话的未读消息计数</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createConversationGroup](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a280dff193ef770efd5d878ca3e3821d5)</td>

<td rowspan="1" colSpan="1" >创建会话分组</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getConversationGroupList](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#ab469fbf92cfdf27d7b268e494028b589)</td>

<td rowspan="1" colSpan="1" >获取会话分组列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteConversationGroup](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a5ec09de4e1fb5e898e4c0800b06a63bc)</td>

<td rowspan="1" colSpan="1" >删除会话分组</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[renameConversationGroup](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a0eba052e8f21602b5dbd249ada0c18eb)</td>

<td rowspan="1" colSpan="1" >重命名会话分组</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addConversationsToGroup](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#abf0cd490796ff60730aa0a8fec037d87)</td>

<td rowspan="1" colSpan="1" >添加会话到一个会话分组</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteConversationsFromGroup](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a9ca6ea0ac6d8f61c7d0f8a85f14a91b9)</td>

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
<td rowspan="1" colSpan="1" >[getUsersInfo](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a7ca8c0f71a9875021fc35dfcaff68d1e)</td>

<td rowspan="1" colSpan="1" >获取用户资料</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setSelfInfo](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#af004ab2f1d1458de354883f1995b678a)</td>

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
<td rowspan="1" colSpan="1" >[getUserStatus](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a2428c7f87859dd85bed1730ad8d3b92a)</td>

<td rowspan="1" colSpan="1" >查询用户状态</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setSelfStatus](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a7520045679f1493c890f2b3b5eee7b84)</td>

<td rowspan="1" colSpan="1" >设置自己的状态</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[subscribeUserStatus](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a9c6deb154d0042d5472ec55cfe0962bb)</td>

<td rowspan="1" colSpan="1" >订阅用户状态</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[unsubscribeUserStatus](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a9254db13bd53dc48a04d05ba5f116d39)</td>

<td rowspan="1" colSpan="1" >取消订阅用户状态</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[searchUsers](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a20281f80a6dddc7b5dd61c203a6efadb)</td>

<td rowspan="1" colSpan="1" >搜索云端用户资料</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addToBlackList](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a8804c7f47000bf1c26aa6ab744a53456)</td>

<td rowspan="1" colSpan="1" >屏蔽某人的消息（添加该用户到黑名单中）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteFromBlackList](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a3dcd8f1c70dceafa94ab48796c2f26aa)</td>

<td rowspan="1" colSpan="1" >取消某人的消息屏蔽（把该用户从黑名单中移除）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getBlackList](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a6269df2d96c910648ab2f0c43e1931c6)</td>

<td rowspan="1" colSpan="1" >获取黑名单列表</td>
</tr>
</table>


## 离线推送相关接口

如果想要在 App 切后台时依然能够实时收到 IM 消息，可以使用离线推送服务。由于大陆境内尚没有统一的推送服务，Android 的离线推送需要针对不同厂商的手机进行 [逐一适配](https://cloud.tencent.com/document/product/269/75428)。
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setOfflinePushConfig](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushManager.html#a494d6cafe50ba25503979a4e0f14c28e)</td>

<td rowspan="1" colSpan="1" >设置离线推送配置信息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[doBackground](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushManager.html#a2b191294ac4d68a2d69e482eae1b638f)</td>

<td rowspan="1" colSpan="1" >APP 检测到应用退后台时可以调用此接口，可以用作桌面应用角标的初始化未读数量。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[doForeground](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushManager.html#a4c2ff4eea609da1d0950648905fbf6aa)</td>

<td rowspan="1" colSpan="1" >APP 检测到应用进前台时可以调用此接口</td>
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
<td rowspan="1" colSpan="1" >[addFriendListener](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#af09d0d2297fe73cc81b8e8941bcd35b2)</td>

<td rowspan="1" colSpan="1" >添加关系链监听器</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeFriendListener](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a6a823459f109bcd8744806f8f1b8bfea)</td>

<td rowspan="1" colSpan="1" >移除关系链监听器</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getFriendList](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#ae478de55db21d42b72a6c5a6a5d16624)</td>

<td rowspan="1" colSpan="1" >获取好友列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getFriendsInfo](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a8c4e51e508d140e4a7ce5f4caf49c870)</td>

<td rowspan="1" colSpan="1" >获取指定好友资料</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setFriendInfo](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a151b7de6219d966b4194ad7fcc8450fe)</td>

<td rowspan="1" colSpan="1" >设置指定好友资料</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[searchFriends](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a3e657c9ec5d68a4c423a64d71f5f9c6e)</td>

<td rowspan="1" colSpan="1" >搜索好友列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addFriend](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a19d0f22aaea285e8cee85a5dd6ed9208)</td>

<td rowspan="1" colSpan="1" >添加好友</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteFromFriendList](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#af7ecf8641b58462d038a9c97bfbd4d61)</td>

<td rowspan="1" colSpan="1" >删除好友</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[checkFriend](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a96bb74f3bbd1aef147ec914a81104d11)</td>

<td rowspan="1" colSpan="1" >检查指定用户的好友关系</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getFriendApplicationList](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a2dbf4da19f3b9b170089b8e8cb210166)</td>

<td rowspan="1" colSpan="1" >获取好友申请列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[acceptFriendApplication](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#ab69ed69330428caff6f468b7df5259fa)</td>

<td rowspan="1" colSpan="1" >同意好友申请</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[refuseFriendApplication](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#af1bcbc196015de8e7a94b1575c466f89)</td>

<td rowspan="1" colSpan="1" >拒绝好友申请</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteFriendApplication](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a5c869e3358ca74f9cd2eaebfc7298490)</td>

<td rowspan="1" colSpan="1" >删除好友申请</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setFriendApplicationRead](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a022b4817a31dd25707f14b8184c42675)</td>

<td rowspan="1" colSpan="1" >设置好友申请已读</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createFriendGroup](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#afe729e7a74d1e7fd06a5f23c155a08ae)</td>

<td rowspan="1" colSpan="1" >新建好友分组</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getFriendGroups](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a0043ca81fdeec5d3e842e85278003d1e)</td>

<td rowspan="1" colSpan="1" >获取分组信息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteFriendGroup](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#ac9f06f447ee4452aa12e078b48023cee)</td>

<td rowspan="1" colSpan="1" >删除好友分组</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[renameFriendGroup](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a5345957f4d75d8e57ea3b4cff9adee13)</td>

<td rowspan="1" colSpan="1" >修改好友分组的名称</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addFriendsToFriendGroup](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a6de9168d476ac14e21025ec5c26251df)</td>

<td rowspan="1" colSpan="1" >添加好友到一个好友分组</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteFriendsFromFriendGroup](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#ae367dfec88522e96d96c5ab942e50653)</td>

<td rowspan="1" colSpan="1" >从好友分组中删除好友</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[subscribeOfficialAccount](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a561a3334dd1f4b75de9099d161ed7f5b)</td>

<td rowspan="1" colSpan="1" >订阅公众号</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[unsubscribeOfficialAccount](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a7569dd95b90eab4293a6f7e99dba2c6f)</td>

<td rowspan="1" colSpan="1" >取消订阅公众号</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getOfficialAccountsInfo](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a7493324aced496edd8ca7a9feac3055e)</td>

<td rowspan="1" colSpan="1" >获取公众号列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[followUser](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a136b5a3e39002162738972e891c7e82d)</td>

<td rowspan="1" colSpan="1" >关注用户</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[unfollowUser](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a4342b42c4cf9fc8bc2bea86d60f2d9c9)</td>

<td rowspan="1" colSpan="1" >取消关注用户</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getMyFollowingList](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#aaa2fde74e3558d19bd6535e434ccf8ec)</td>

<td rowspan="1" colSpan="1" >获取我的关注列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getMyFollowersList](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a614faf44b87c209825de3e65fa90ff58)</td>

<td rowspan="1" colSpan="1" >获取我的粉丝列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getMutualFollowersList](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#ac0eaedf339566bfcbd0ad5b5f2080c64)</td>

<td rowspan="1" colSpan="1" >获取我的互关列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getUserFollowInfo](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a86ff97aed8e6476ff6393660c8433f5d)</td>

<td rowspan="1" colSpan="1" >获取指定用户的 关注/粉丝/互关 数量信息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[checkFollowType](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#aeb364a11188590a7e6093522f5bad415)</td>

<td rowspan="1" colSpan="1" >检查指定用户的关注类型</td>
</tr>
</table>

