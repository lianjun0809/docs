> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

## 初始化登录接口

初始化并成功登录，是正常使用腾讯云 IM 服务的前提。
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[initSDK](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/initSDK.html)</td>

<td rowspan="1" colSpan="1" >初始化 SDK</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[unInitSDK](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/unInitSDK.html)</td>

<td rowspan="1" colSpan="1" >反初始化 SDK</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[login](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/login.html)</td>

<td rowspan="1" colSpan="1" >登录</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[logout](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/logout.html)</td>

<td rowspan="1" colSpan="1" >登出</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getLoginUser](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/getLoginUser.html)</td>

<td rowspan="1" colSpan="1" >获取当前登录用户的 UserID</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getLoginStatus](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/getLoginStatus.html)</td>

<td rowspan="1" colSpan="1" >获取登录状态</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getServerTime](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/getServerTime.html)</td>

<td rowspan="1" colSpan="1" >获取服务器当前时间（Web不支持）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getVersion](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/getVersion.html)</td>

<td rowspan="1" colSpan="1" >获取版本号</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getConversationManager](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/getConversationManager.html)</td>

<td rowspan="1" colSpan="1" >会话功能模块</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getFriendshipManager](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/getFriendshipManager.html)</td>

<td rowspan="1" colSpan="1" >关系链功能模块</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupManager](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/getGroupManager.html)</td>

<td rowspan="1" colSpan="1" >高级群组功能模块</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getMessageManager](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/getMessageManager.html)</td>

<td rowspan="1" colSpan="1" >高级消息功能模块</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getOfflinePushManager](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/getOfflinePushManager.html)</td>

<td rowspan="1" colSpan="1" >离线推送模块</td>
</tr>
</table>


## 创建消息接口

创建的消息会返回一个id字段，将id字段等传递给统一的发送接口（sendMessage）即可发送消息。
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createTextMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/createTextMessage.html)</td>

<td rowspan="1" colSpan="1" >创建文本消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createCustomMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/createCustomMessage.html)</td>

<td rowspan="1" colSpan="1" >创建定制化消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createImageMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/createImageMessage.html)</td>

<td rowspan="1" colSpan="1" >创建图片消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createSoundMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/createSoundMessage.html)</td>

<td rowspan="1" colSpan="1" >创建音频文件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createVideoMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/createVideoMessage.html)</td>

<td rowspan="1" colSpan="1" >创建视频文件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createTextAtMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/createTextAtMessage.html)</td>

<td rowspan="1" colSpan="1" >创建AT消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createFileMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/createFileMessage.html)</td>

<td rowspan="1" colSpan="1" >创建文件消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createLocationMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/createLocationMessage.html)</td>

<td rowspan="1" colSpan="1" >创建位置信息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createFaceMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/createFaceMessage.html)</td>

<td rowspan="1" colSpan="1" >创建表情消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createMergerMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/createMergerMessage.html)</td>

<td rowspan="1" colSpan="1" >创建合并消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createForwardMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/createForwardMessage.html)</td>

<td rowspan="1" colSpan="1" >创建转发消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createTargetedGroupMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/createTargetedGroupMessage.html)</td>

<td rowspan="1" colSpan="1" >创建一条定向群消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[appendMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/appendMessage.html)</td>

<td rowspan="1" colSpan="1" >添加多Element消息</td>
</tr>
</table>


## 消息收发接口

如果您需要收发图片、视频、文件等富媒体消息，并需要撤回消息、标记已读、查询历史消息等高级功能，推荐使用下面这套高级消息接口（原3.6.0前的高级消息部分接口已弃用，请使用新版创建消息接口后调用发送消息接口）。
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addAdvancedMsgListener](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/addAdvancedMsgListener.html)</td>

<td rowspan="1" colSpan="1" >设置高级消息的事件监听器</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeAdvancedMsgListener](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/removeAdvancedMsgListener.html)</td>

<td rowspan="1" colSpan="1" >移除高级消息的事件监听器</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getC2CHistoryMessageList](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/getC2CHistoryMessageList.html)</td>

<td rowspan="1" colSpan="1" >获取单聊（C2C）历史消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getHistoryMessageList](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/getHistoryMessageList.html)</td>

<td rowspan="1" colSpan="1" >获取历史消息高级接口</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupHistoryMessageList](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/getGroupHistoryMessageList.html)</td>

<td rowspan="1" colSpan="1" >获取群组历史消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[markC2CMessageAsRead](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/markC2CMessageAsRead.html)</td>

<td rowspan="1" colSpan="1" >设置单聊（C2C）消息已读</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[markGroupMessageAsRead](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/markGroupMessageAsRead.html)</td>

<td rowspan="1" colSpan="1" >设置群组消息已读</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[markAllMessageAsRead](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/markAllMessageAsRead.html)</td>

<td rowspan="1" colSpan="1" >标记所有消息为已读</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteMessageFromLocalStorage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/deleteMessageFromLocalStorage.html)</td>

<td rowspan="1" colSpan="1" >删除本地消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteMessages](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/deleteMessages.html)</td>

<td rowspan="1" colSpan="1" >删除本地及漫游消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[insertGroupMessageToLocalStorage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/insertGroupMessageToLocalStorage.html)</td>

<td rowspan="1" colSpan="1" >向群组消息列表中添加一条消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[insertC2CMessageToLocalStorage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/insertC2CMessageToLocalStorage.html)</td>

<td rowspan="1" colSpan="1" >向C2C消息列表中添加一条消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[clearC2CHistoryMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/clearC2CHistoryMessage.html)</td>

<td rowspan="1" colSpan="1" >清空单聊本地及云端的消息（不删除会话）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[clearGroupHistoryMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/clearGroupHistoryMessage.html)</td>

<td rowspan="1" colSpan="1" >清空群组及云端的消息（不删除会话）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[downloadMergerMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/downloadMergerMessage.html)</td>

<td rowspan="1" colSpan="1" >获取合并消息的子消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setC2CReceiveMessageOpt](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/setC2CReceiveMessageOpt.html)</td>

<td rowspan="1" colSpan="1" >设置针对某个用户的 C2C 消息接收选项（支持批量设置）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getC2CReceiveMessageOpt](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/getC2CReceiveMessageOpt.html)</td>

<td rowspan="1" colSpan="1" >查询针对某个用户的 C2C 消息接收选项</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGroupReceiveMessageOpt](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/setGroupReceiveMessageOpt.html)</td>

<td rowspan="1" colSpan="1" >修改群消息接收选项</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setLocalCustomData](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/setLocalCustomData.html)</td>

<td rowspan="1" colSpan="1" >设置消息自定义数据（本地保存，不会发送到对端，程序卸载重装后失效）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setLocalCustomInt](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/setLocalCustomInt.html)</td>

<td rowspan="1" colSpan="1" >设置消息自定义数据，可以用来标记语音、视频消息是否已经播放（本地保存，不会发送到对端，程序卸载重装后失效）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[revokeMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/revokeMessage.html)</td>

<td rowspan="1" colSpan="1" >撤回消息的时间限制默认 2 minutes，超过 2 minutes 的消息不能撤回，您也可以在 控制台（功能配置 -> 登录与消息 -> 消息撤回设置）自定义撤回时间限制。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[modifyMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/modifyMessage.html)</td>

<td rowspan="1" colSpan="1" >消息变更</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[sendMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/sendMessage.html)</td>

<td rowspan="1" colSpan="1" >发送消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[searchLocalMessages](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/searchLocalMessages.html)</td>

<td rowspan="1" colSpan="1" >搜索本地消息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[sendMessageReadReceipts](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/sendMessageReadReceipts.html)</td>

<td rowspan="1" colSpan="1" >发送群消息已读回执</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getMessageReadReceipts](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/getMessageReadReceipts.html)</td>

<td rowspan="1" colSpan="1" >获取自己发送消息的已读回执</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupMessageReadMemberList](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/getGroupMessageReadMemberList.html)</td>

<td rowspan="1" colSpan="1" >获取自己发送的群消息已读（未读）群成员列表</td>
</tr>
</table>


## 会话列表相关接口

会话列表，即登录微信或 QQ 后首屏看到的列表，亦被称作消息列表，包含会话节点、会话名称、群名称、最后一条消息以及未读消息数等元素。
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addConversationListener](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_conversation_manager/V2TIMConversationManager/addConversationListener.html)</td>

<td rowspan="1" colSpan="1" >添加关系链监听器</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeConversationListener](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_conversation_manager/V2TIMConversationManager/removeConversationListener.html)</td>

<td rowspan="1" colSpan="1" >移除关系链监听器</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getConversationList](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_conversation_manager/V2TIMConversationManager/getConversationList.html)</td>

<td rowspan="1" colSpan="1" >获取会话列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getConversationListByConversationIds](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_conversation_manager/V2TIMConversationManager/getConversationListByConversationIds.html)</td>

<td rowspan="1" colSpan="1" >通过会话ID获取指定会话列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[pinConversation](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_conversation_manager/V2TIMConversationManager/pinConversation.html)</td>

<td rowspan="1" colSpan="1" >会话置顶</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getTotalUnreadMessageCount](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_conversation_manager/V2TIMConversationManager/getTotalUnreadMessageCount.html)</td>

<td rowspan="1" colSpan="1" >获取会话未读总数</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getConversation](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_conversation_manager/V2TIMConversationManager/getConversation.html)</td>

<td rowspan="1" colSpan="1" >获取指定会话</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteConversation](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_conversation_manager/V2TIMConversationManager/deleteConversation.html)</td>

<td rowspan="1" colSpan="1" >删除会话</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setConversationDraft](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_conversation_manager/V2TIMConversationManager/setConversationDraft.html)</td>

<td rowspan="1" colSpan="1" >设置会话草稿</td>
</tr>
</table>


## 群组相关接口

腾讯云 IM SDK 支持五种预设的群组类型，每种类型都有其适用场景：
- 工作群（Work） ：类似普通微信群，创建后不能自由加入，必须由已经在群的用户邀请入群，同旧版本中的 Private。

- 公开群（Public） ：类似 QQ 群，用户申请加入，但需要群主或管理员审批。

- 会议群（Meeting）：适合跟 [TRTC](https://cloud.tencent.com/product/trtc) 结合实现视频会议和在线教育等场景，支持随意进出，支持查看进群前的历史消息，同旧版本中的 ChatRoom。

- 社群（Community）：创建后可以随意进出，适合用于知识分享和游戏交流等超大社区群聊场景。

- 直播群（AVChatRoom）：适合直播弹幕聊天室等场景，支持随意进出，人数无上限。

<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addGroupListener](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/addGroupListener.html)</td>

<td rowspan="1" colSpan="1" >添加群组监听器</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeGroupListener](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/removeGroupListener.html)</td>

<td rowspan="1" colSpan="1" >移除群组监听器</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createGroup](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/createGroup.html)</td>

<td rowspan="1" colSpan="1" >创建群组（高级版本），可在建群同时设置群信息和初始的群成员</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[joinGroup](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/joinGroup.html)</td>

<td rowspan="1" colSpan="1" >加入群组</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[quitGroup](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/quitGroup.html)</td>

<td rowspan="1" colSpan="1" >退出群组</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[dismissGroup](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/dismissGroup.html)</td>

<td rowspan="1" colSpan="1" >解散群组（仅群主和管理员可以解散）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getJoinedGroupList](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/getJoinedGroupList.html)</td>

<td rowspan="1" colSpan="1" >获取已经加入的群列表（不包括已加入的直播群）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupsInfo](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/getGroupsInfo.html)</td>

<td rowspan="1" colSpan="1" >拉取群资料</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGroupInfo](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/setGroupInfo.html)</td>

<td rowspan="1" colSpan="1" >修改群资料</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[initGroupAttributes](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/initGroupAttributes.html)</td>

<td rowspan="1" colSpan="1" >初始化群属性，会清空原有的群属性列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGroupAttributes](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/setGroupAttributes.html)</td>

<td rowspan="1" colSpan="1" >设置群属性。已有该群属性则更新其 value 值，没有该群属性则添加该属性。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteGroupAttributes](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/deleteGroupAttributes.html)</td>

<td rowspan="1" colSpan="1" >删除指定群属性，keys 传 null 则清空所有群属性。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupAttributes](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/getGroupAttributes.html)</td>

<td rowspan="1" colSpan="1" >获取指定群属性，keys 传 null 则获取所有群属性。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[searchGroups](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/searchGroups.html)</td>

<td rowspan="1" colSpan="1" >搜索群列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupOnlineMemberCount](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/getGroupOnlineMemberCount.html)</td>

<td rowspan="1" colSpan="1" >获取指定群在线人数(目前只支持直播群)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupMemberList](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/getGroupMemberList.html)</td>

<td rowspan="1" colSpan="1" >获取群成员列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupMembersInfo](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/getGroupMembersInfo.html)</td>

<td rowspan="1" colSpan="1" >获取指定的群成员资料</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGroupMemberInfo](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/setGroupMemberInfo.html)</td>

<td rowspan="1" colSpan="1" >修改指定的群成员资料</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[searchGroupMembers](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/searchGroupMembers.html)</td>

<td rowspan="1" colSpan="1" >搜索群成员</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[muteGroupMember](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/muteGroupMember.html)</td>

<td rowspan="1" colSpan="1" >禁言</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[kickGroupMember](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/kickGroupMember.html)</td>

<td rowspan="1" colSpan="1" >踢人</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGroupMemberRole](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/setGroupMemberRole.html)</td>

<td rowspan="1" colSpan="1" >切换群成员的角色</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[transferGroupOwner](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/transferGroupOwner.html)</td>

<td rowspan="1" colSpan="1" >转让群主</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[inviteUserToGroup](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/inviteUserToGroup.html)</td>

<td rowspan="1" colSpan="1" >邀请他人入群</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupApplicationList](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/getGroupApplicationList.html)</td>

<td rowspan="1" colSpan="1" >获取加群的申请列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[acceptGroupApplication](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/acceptGroupApplication.html)</td>

<td rowspan="1" colSpan="1" >同意某一条加群申请</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[refuseGroupApplication](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/refuseGroupApplication.html)</td>

<td rowspan="1" colSpan="1" >拒绝某一条加群申请</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGroupApplicationRead](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/setGroupApplicationRead.html)</td>

<td rowspan="1" colSpan="1" >标记申请列表为已读</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getJoinedCommunityList](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/getJoinedCommunityList.html)</td>

<td rowspan="1" colSpan="1" >获取当前用户已经加入的支持话题的社群列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createTopicInCommunity](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/createTopicInCommunity.html)</td>

<td rowspan="1" colSpan="1" >创建话题</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteTopicFromCommunity](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/deleteTopicFromCommunity.html)</td>

<td rowspan="1" colSpan="1" >删除话题</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setTopicInfo](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/setTopicInfo.html)</td>

<td rowspan="1" colSpan="1" >设置话题属性</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getTopicInfoList](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/getTopicInfoList.html)</td>

<td rowspan="1" colSpan="1" >获取话题属性的列表</td>
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
<td rowspan="1" colSpan="1" >[getUsersInfo](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/getUsersInfo.html)</td>

<td rowspan="1" colSpan="1" >获取用户资料</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getUserStatus](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/getUserStatus.html)</td>

<td rowspan="1" colSpan="1" >获取用户在线状态</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setSelfInfo](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/setSelfInfo.html)</td>

<td rowspan="1" colSpan="1" >修改个人资料</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setSelfStatus](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/setSelfStatus.html)</td>

<td rowspan="1" colSpan="1" >设置当前登录用户在线状态</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addToBlackList](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/addToBlackList.html)</td>

<td rowspan="1" colSpan="1" >屏蔽某人的消息（添加该用户到黑名单中）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteFromBlackList](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/deleteFromBlackList.html)</td>

<td rowspan="1" colSpan="1" >取消某人的消息屏蔽（把该用户从黑名单中移除）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getBlackList](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/getBlackList.html)</td>

<td rowspan="1" colSpan="1" >获取黑名单列表</td>
</tr>
</table>


## 好友管理相关接口

腾讯云 IM 在收发消息时默认不检查是不是好友关系，您可以在 [**控制台**](https://console.cloud.tencent.com/im) > **功能配置 **> **登录与消息 **> **好友关系检查**中开启"发送单聊消息检查关系链"开关，并使用如下接口增删好友和管理好友列表。
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addFriendListener](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/addFriendListener.html)</td>

<td rowspan="1" colSpan="1" >添加关系链监听器</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeFriendListener](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/removeFriendListener.html)</td>

<td rowspan="1" colSpan="1" >移除关系链监听器</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getFriendList](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/getFriendList.html)</td>

<td rowspan="1" colSpan="1" >获取好友列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getFriendsInfo](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/getFriendsInfo.html)</td>

<td rowspan="1" colSpan="1" >获取指定好友资料</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setFriendInfo](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/setFriendInfo.html)</td>

<td rowspan="1" colSpan="1" >设置指定好友资料</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addFriend](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/addFriend.html)</td>

<td rowspan="1" colSpan="1" >添加好友</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteFromFriendList](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/deleteFromFriendList.html)</td>

<td rowspan="1" colSpan="1" >删除好友</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[checkFriend](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/checkFriend.html)</td>

<td rowspan="1" colSpan="1" >检查指定用户的好友关系</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getFriendApplicationList](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/getFriendApplicationList.html)</td>

<td rowspan="1" colSpan="1" >获取好友申请列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[acceptFriendApplication](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/acceptFriendApplication.html)</td>

<td rowspan="1" colSpan="1" >同意好友申请</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[refuseFriendApplication](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/refuseFriendApplication.html)</td>

<td rowspan="1" colSpan="1" >拒绝好友申请</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteFriendApplication](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/deleteFriendApplication.html)</td>

<td rowspan="1" colSpan="1" >删除好友申请</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setFriendApplicationRead](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/setFriendApplicationRead.html)</td>

<td rowspan="1" colSpan="1" >设置好友申请已读</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createFriendGroup](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/createFriendGroup.html)</td>

<td rowspan="1" colSpan="1" >新建好友分组</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getFriendGroups](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/getFriendGroups.html)</td>

<td rowspan="1" colSpan="1" >获取分组信息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteFriendGroup](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/deleteFriendGroup.html)</td>

<td rowspan="1" colSpan="1" >删除好友分组</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[renameFriendGroup](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/renameFriendGroup.html)</td>

<td rowspan="1" colSpan="1" >修改好友分组的名称</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addFriendsToFriendGroup](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/addFriendsToFriendGroup.html)</td>

<td rowspan="1" colSpan="1" >添加好友到一个好友分组</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteFriendsFromFriendGroup](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/deleteFriendsFromFriendGroup.html)</td>

<td rowspan="1" colSpan="1" >从好友分组中删除好友</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[searchFriends](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/searchFriends.html)</td>

<td rowspan="1" colSpan="1" >搜索好友</td>
</tr>
</table>


## 离线推送相关接口

如果您希望应用切到后台时依然能够稳定接收 IM 消息，建议您使用 [推送服务（Push）](https://cloud.tencent.com/document/product/269/100621)，其全面覆盖主流厂商通道、最快3分钟即可实现一键式集成，支持丰富多样的推送方式和消息全链路统计分析能力，保障精准送达、服务安全稳定，助您轻松提升用户留存和互动活跃度。若您希望自行实现离线推送能力，也可参考 [自集成推送](https://cloud.tencent.com/document/product/269/75428) 指引逐一适配每个设备厂商的推送服务，将用到以下接口。
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setAPNSListener](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/setAPNSListener.html)</td>

<td rowspan="1" colSpan="1" >设置苹果系统离线推送专用监听器</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[doBackground](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_offline_push_manager/V2TIMOfflinePushManager/doBackground.html)</td>

<td rowspan="1" colSpan="1" >设置离线推送配置信息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[doForeground](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_offline_push_manager/V2TIMOfflinePushManager/doForeground.html)</td>

<td rowspan="1" colSpan="1" >设置离线推送配置信息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setOfflinePushConfig](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_offline_push_manager/V2TIMOfflinePushManager/setOfflinePushConfig.html)</td>

<td rowspan="1" colSpan="1" >设置离线推送配置信息</td>
</tr>
</table>
