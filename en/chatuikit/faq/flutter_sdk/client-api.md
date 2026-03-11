> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

## Initialization and Login APIs

To use the Tencent Cloud Chat service, you need to initialize the SDK and log in.
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[initSDK](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/initSDK.html)</td>

<td rowspan="1" colSpan="1" >Initializes the SDK.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[unInitSDK](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/unInitSDK.html)</td>

<td rowspan="1" colSpan="1" >Uninitializes the SDK.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[login](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/login.html)</td>

<td rowspan="1" colSpan="1" >Logs in.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[logout](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/logout.html)</td>

<td rowspan="1" colSpan="1" >Logs out.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getLoginUser](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/getLoginUser.html)</td>

<td rowspan="1" colSpan="1" >Gets the UserID of the current login user.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getLoginStatus](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/getLoginStatus.html)</td>

<td rowspan="1" colSpan="1" >Gets the login status.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getServerTime](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/getServerTime.html)</td>

<td rowspan="1" colSpan="1" >Gets the current server time (not supported on web).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getVersion](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/getVersion.html)</td>

<td rowspan="1" colSpan="1" >Gets the version number.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getConversationManager](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/getConversationManager.html)</td>

<td rowspan="1" colSpan="1" >Conversation feature entry.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getFriendshipManager](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/getFriendshipManager.html)</td>

<td rowspan="1" colSpan="1" >Contacts feature entry.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupManager](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/getGroupManager.html)</td>

<td rowspan="1" colSpan="1" >Advanced group feature entry.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getMessageManager](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/getMessageManager.html)</td>

<td rowspan="1" colSpan="1" >Advanced message feature entry.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getOfflinePushManager](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/getOfflinePushManager.html)</td>

<td rowspan="1" colSpan="1" >Gets the version number.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getSignalingManager](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/getSignalingManager.html)</td>

<td rowspan="1" colSpan="1" >Signaling entry.</td>
</tr>
</table>


## Signaling APIs
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addSignalingListener](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_signaling_manager/V2TIMSignalingManager/addSignalingListener.html)</td>

<td rowspan="1" colSpan="1" >Adds a signaling listener.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeSignalingListener](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_signaling_manager/V2TIMSignalingManager/removeSignalingListener.html)</td>

<td rowspan="1" colSpan="1" >Removes a signaling listener.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[invite](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_signaling_manager/V2TIMSignalingManager/invite.html)</td>

<td rowspan="1" colSpan="1" >Invites a user.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[inviteInGroup](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_signaling_manager/V2TIMSignalingManager/inviteInGroup.html)</td>

<td rowspan="1" colSpan="1" >Invites certain users in the group.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[cancel](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_signaling_manager/V2TIMSignalingManager/cancel.html)</td>

<td rowspan="1" colSpan="1" >The inviter cancels the invitation.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[accept](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_signaling_manager/V2TIMSignalingManager/accept.html)</td>

<td rowspan="1" colSpan="1" >The invitee accepts the invitation.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[reject](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_signaling_manager/V2TIMSignalingManager/reject.html)</td>

<td rowspan="1" colSpan="1" >The invitee rejects the invitation.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getSignalingInfo](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_signaling_manager/V2TIMSignalingManager/getSignalingInfo.html)</td>

<td rowspan="1" colSpan="1" >Gets signaling information.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addInvitedSignaling](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_signaling_manager/V2TIMSignalingManager/addInvitedSignaling.html)</td>

<td rowspan="1" colSpan="1" >Creates a signaling request.</td>
</tr>
</table>


## Message Creation APIs

After a message is created, an `id` field will be returned. You can pass in the `id` field and related information to the message sending API (`sendMessage`) to send the message.
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createTextMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/createTextMessage.html)</td>

<td rowspan="1" colSpan="1" >Creates a text message.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createCustomMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/createCustomMessage.html)</td>

<td rowspan="1" colSpan="1" >Creates a custom message.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createImageMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/createImageMessage.html)</td>

<td rowspan="1" colSpan="1" >Creates an image message.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createSoundMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/createSoundMessage.html)</td>

<td rowspan="1" colSpan="1" >Creates an audio message.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createVideoMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/createVideoMessage.html)</td>

<td rowspan="1" colSpan="1" >Creates a video message.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createTextAtMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/createTextAtMessage.html)</td>

<td rowspan="1" colSpan="1" >Creates an @ text message.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createFileMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/createFileMessage.html)</td>

<td rowspan="1" colSpan="1" >Creates a file message.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createLocationMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/createLocationMessage.html)</td>

<td rowspan="1" colSpan="1" >Creates a location message.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createFaceMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/createFaceMessage.html)</td>

<td rowspan="1" colSpan="1" >Creates an emoji message.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createMergerMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/createMergerMessage.html)</td>

<td rowspan="1" colSpan="1" >Creates a combined message.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createForwardMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/createForwardMessage.html)</td>

<td rowspan="1" colSpan="1" >Creates a forward message.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createTargetedGroupMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/createTargetedGroupMessage.html)</td>

<td rowspan="1" colSpan="1" >Creates a targeted group message.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[appendMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/appendMessage.html)</td>

<td rowspan="1" colSpan="1" >Adds a multi-element message.</td>
</tr>
</table>


## Message Sending and Receiving APIs

If you need to send or receive rich media messages (such as image, video, and file messages) and use advanced features such as recalling messages, marking messages as read, and querying message history, we recommend the following advanced message APIs. (The original APIs for simple message sending and receiving used by v3.6.0 and earlier versions have been disused. Please use new APIs to create and send messages.)
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addAdvancedMsgListener](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/addAdvancedMsgListener.html)</td>

<td rowspan="1" colSpan="1" >Sets an event listener for advanced messages.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeAdvancedMsgListener](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/removeAdvancedMsgListener.html)</td>

<td rowspan="1" colSpan="1" >Removes the event listener for advanced messages.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getC2CHistoryMessageList](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/getC2CHistoryMessageList.html)</td>

<td rowspan="1" colSpan="1" >Gets historical one-to-one (C2C) messages.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getHistoryMessageList](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/getHistoryMessageList.html)</td>

<td rowspan="1" colSpan="1" >Gets historical messages (advanced API).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupHistoryMessageList](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/getGroupHistoryMessageList.html)</td>

<td rowspan="1" colSpan="1" >Gets historical group messages.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[markC2CMessageAsRead](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/markC2CMessageAsRead.html)</td>

<td rowspan="1" colSpan="1" >Marks one-to-one (C2C) messages as read.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[markGroupMessageAsRead](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/markGroupMessageAsRead.html)</td>

<td rowspan="1" colSpan="1" >Marks group messages as read.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[markAllMessageAsRead](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/markAllMessageAsRead.html)</td>

<td rowspan="1" colSpan="1" >Marks all messages as read.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteMessageFromLocalStorage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/deleteMessageFromLocalStorage.html)</td>

<td rowspan="1" colSpan="1" >Deletes a message from the local storage.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteMessages](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/deleteMessages.html)</td>

<td rowspan="1" colSpan="1" >Deletes local and roaming messages.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[insertGroupMessageToLocalStorage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/insertGroupMessageToLocalStorage.html)</td>

<td rowspan="1" colSpan="1" >Adds a message to the message list of a group chat.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[insertC2CMessageToLocalStorage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/insertC2CMessageToLocalStorage.html)</td>

<td rowspan="1" colSpan="1" >Adds a message to the message list of a one-to-one chat.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[clearC2CHistoryMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/clearC2CHistoryMessage.html)</td>

<td rowspan="1" colSpan="1" >Clears the chat history with a user from local storage and the cloud (without deleting the conversation).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[clearGroupHistoryMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/clearGroupHistoryMessage.html)</td>

<td rowspan="1" colSpan="1" >Clears the chat history of a group from local storage and the cloud (without deleting the conversation).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[downloadMergerMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/downloadMergerMessage.html)</td>

<td rowspan="1" colSpan="1" >Gets the sub messages of a combined message.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setC2CReceiveMessageOpt](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/setC2CReceiveMessageOpt.html)</td>

<td rowspan="1" colSpan="1" >Sets the one-to-one message receiving option for a user (batch setting supported).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getC2CReceiveMessageOpt](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/getC2CReceiveMessageOpt.html)</td>

<td rowspan="1" colSpan="1" >Queries the one-to-one message receiving option of a user.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGroupReceiveMessageOpt](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/setGroupReceiveMessageOpt.html)</td>

<td rowspan="1" colSpan="1" >Modifies the group message receiving option.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setLocalCustomData](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/setLocalCustomData.html)</td>

<td rowspan="1" colSpan="1" >Sets custom message data (saved locally, will not be sent to the peer end, and will become invalid after the app is uninstalled and reinstalled).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setLocalCustomInt](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/setLocalCustomInt.html)</td>

<td rowspan="1" colSpan="1" >Sets custom message data and marks whether a voice or video message is played (such a message will be saved locally, not be sent to the peer end, and become invalid after the app is uninstalled and reinstalled).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[revokeMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/revokeMessage.html)</td>

<td rowspan="1" colSpan="1" >Recalls a message. By default, you can recall only messages that are sent within two minutes. You can customize the time limit for message recall via the console (**Feature Configuration** > **Login and Message** > **Message Recall Settings**).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[modifyMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/modifyMessage.html)</td>

<td rowspan="1" colSpan="1" >Modifies a message.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[sendMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/sendMessage.html)</td>

<td rowspan="1" colSpan="1" >Sends a message.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[searchLocalMessages](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/searchLocalMessages.html)</td>

<td rowspan="1" colSpan="1" >Searches for local messages.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[sendMessageReadReceipts](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/sendMessageReadReceipts.html)</td>

<td rowspan="1" colSpan="1" >Sends group message read receipts.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getMessageReadReceipts](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/getMessageReadReceipts.html)</td>

<td rowspan="1" colSpan="1" >Gets read receipts for messages sent by yourself.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupMessageReadMemberList](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/getGroupMessageReadMemberList.html)</td>

<td rowspan="1" colSpan="1" >Gets the list of members who have (or have not) read a message sent by yourself.</td>
</tr>
</table>


## Group APIs

Tencent Cloud Chat SDK supports five preset group types, each of which pertains to different scenarios.
- Work group (Work): users can join the group only after being invited by group members. This group type is the same as private group (Private) in earlier versions.

- Public group (Public): Users can join a public group through requests, which need to be approved by the group owner or group admin.

- Meeting group (Meeting): used together with [TRTC](https://trtc.io/document) to enable scenarios such as video conferencing and online education. Users can join and leave the group freely and view the message history before they join. Same as chat room (ChatRoom) in earlier versions.

- Community: A user can join and leave a community freely. It is suitable for chat scenarios with a super large number of community members, such as knowledge sharing and game discussion. This feature is supported by a client with the SDK enhanced edition v5.8.1668 or later and the web SDK v2.17.0 or later. To use it, you need to purchase the [Pro edition 、Pro Plus edition、Enterprise edition](https://trtc.io/buy/chat), and then enable it in [Console](https://console.trtc.io/), path: Applications > Your App > Chat > Configuration > Group Configuration > Community.

- Audio-video group (AVChatRoom): An audio-video group allows users to join and leave freely and is suitable for scenarios such as live streaming and chat rooms with on-screen comments. There is no limit on the number of group members.

<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addGroupListener](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/addGroupListener.html)</td>

<td rowspan="1" colSpan="1" >Adds an event listener for groups.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeGroupListener](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/removeGroupListener.html)</td>

<td rowspan="1" colSpan="1" >Removes an event listener for groups.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createGroup](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/createGroup.html)</td>

<td rowspan="1" colSpan="1" >Creates a group (advanced). The group information and the initial group members can be set during group creation.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[joinGroup](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/joinGroup.html)</td>

<td rowspan="1" colSpan="1" >Joins a group.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[quitGroup](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/quitGroup.html)</td>

<td rowspan="1" colSpan="1" >Leaves a group.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[dismissGroup](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/dismissGroup.html)</td>

<td rowspan="1" colSpan="1" >Deletes a group. Only the group owner and group admin can delete the group.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getJoinedGroupList](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/getJoinedGroupList.html)</td>

<td rowspan="1" colSpan="1" >Gets the list of groups the current user has joined, excluding audio-video groups.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupsInfo](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/getGroupsInfo.html)</td>

<td rowspan="1" colSpan="1" >Gets the profiles of groups.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGroupInfo](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/setGroupInfo.html)</td>

<td rowspan="1" colSpan="1" >Modifies the profile of a group.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[initGroupAttributes](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/initGroupAttributes.html)</td>

<td rowspan="1" colSpan="1" >Initializes group attributes. This will clear the existing group attribute list.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGroupAttributes](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/setGroupAttributes.html)</td>

<td rowspan="1" colSpan="1" >Sets group attributes. If the group attributes already exist, their values are updated. Otherwise, the group attributes are added.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteGroupAttributes](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/deleteGroupAttributes.html)</td>

<td rowspan="1" colSpan="1" >Deletes specified group attributes. Passing in `null` for `keys` means clearing all group attributes.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupAttributes](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/getGroupAttributes.html)</td>

<td rowspan="1" colSpan="1" >Gets specified group attributes. Passing in `null` for `keys` means getting all group attributes.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[searchGroups](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/searchGroups.html)</td>

<td rowspan="1" colSpan="1" >Searches for groups.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupOnlineMemberCount](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/getGroupOnlineMemberCount.html)</td>

<td rowspan="1" colSpan="1" >Gets the number of online users in a group. (This API is currently supported only by audio-video groups.)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupMemberList](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/getGroupMemberList.html)</td>

<td rowspan="1" colSpan="1" >Gets the group member list.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupMembersInfo](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/getGroupMembersInfo.html)</td>

<td rowspan="1" colSpan="1" >Gets the profiles of specified group members.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGroupMemberInfo](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/setGroupMemberInfo.html)</td>

<td rowspan="1" colSpan="1" >Modifies the profile of a specified group member.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[searchGroupMembers](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/searchGroupMembers.html)</td>

<td rowspan="1" colSpan="1" >Searches for group members.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[muteGroupMember](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/muteGroupMember.html)</td>

<td rowspan="1" colSpan="1" >Mutes a group member.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[kickGroupMember](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/kickGroupMember.html)</td>

<td rowspan="1" colSpan="1" >Removes members from a group.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGroupMemberRole](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/setGroupMemberRole.html)</td>

<td rowspan="1" colSpan="1" >Sets a role for a group member.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[transferGroupOwner](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/transferGroupOwner.html)</td>

<td rowspan="1" colSpan="1" >Transfers the ownership of a group.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[inviteUserToGroup](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/inviteUserToGroup.html)</td>

<td rowspan="1" colSpan="1" >Invites users to a group.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupApplicationList](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/getGroupApplicationList.html)</td>

<td rowspan="1" colSpan="1" >Gets the list of requests to join a group.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[acceptGroupApplication](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/acceptGroupApplication.html)</td>

<td rowspan="1" colSpan="1" >Accepts a request to join a group.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[refuseGroupApplication](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/refuseGroupApplication.html)</td>

<td rowspan="1" colSpan="1" >Rejects a request to join a group.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGroupApplicationRead](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/setGroupApplicationRead.html)</td>

<td rowspan="1" colSpan="1" >Marks the request list as read.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getJoinedCommunityList](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/getJoinedCommunityList.html)</td>

<td rowspan="1" colSpan="1" >Gets the list of community groups the current user has joined.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createTopicInCommunity](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/createTopicInCommunity.html)</td>

<td rowspan="1" colSpan="1" >Creates a topic.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteTopicFromCommunity](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/deleteTopicFromCommunity.html)</td>

<td rowspan="1" colSpan="1" >Deletes a topic.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setTopicInfo](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/setTopicInfo.html)</td>

<td rowspan="1" colSpan="1" >Sets topic attributes.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getTopicInfoList](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_group_manager/V2TIMGroupManager/getTopicInfoList.html)</td>

<td rowspan="1" colSpan="1" >Gets the topics of a group.</td>
</tr>
</table>


## Conversation List APIs

The conversation list is the list a user sees on the first screen after login. It includes elements such as conversation node, conversation name, group name, last message, and unread count.
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addConversationListener](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_conversation_manager/V2TIMConversationManager/addConversationListener.html)</td>

<td rowspan="1" colSpan="1" >Adds a contacts listener.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeConversationListener](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_conversation_manager/V2TIMConversationManager/removeConversationListener.html)</td>

<td rowspan="1" colSpan="1" >Removes a contacts listener.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getConversationList](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_conversation_manager/V2TIMConversationManager/getConversationList.html)</td>

<td rowspan="1" colSpan="1" >Gets the conversation list.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getConversationListByConversaionIds](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_conversation_manager/V2TIMConversationManager/getConversationListByConversaionIds.html)</td>

<td rowspan="1" colSpan="1" >Gets the list of specified conversations by conversation IDs.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[pinConversation](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_conversation_manager/V2TIMConversationManager/pinConversation.html)</td>

<td rowspan="1" colSpan="1" >Pins a conversation to the top.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getTotalUnreadMessageCount](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_conversation_manager/V2TIMConversationManager/getTotalUnreadMessageCount.html)</td>

<td rowspan="1" colSpan="1" >Gets the total unread message count of a conversation.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getConversation](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_conversation_manager/V2TIMConversationManager/getConversation.html)</td>

<td rowspan="1" colSpan="1" >Gets a specified conversation.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteConversation](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_conversation_manager/V2TIMConversationManager/deleteConversation.html)</td>

<td rowspan="1" colSpan="1" >Deletes a conversation.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setConversationDraft](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_conversation_manager/V2TIMConversationManager/setConversationDraft.html)</td>

<td rowspan="1" colSpan="1" >Sets a draft for a conversation.</td>
</tr>
</table>


## User Profile APIs

You can use the following APIs to query user profiles, modify your profile, and block messages from a specified user (that is, adding a specified user to the blocklist).
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getUsersInfo](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/getUsersInfo.html)</td>

<td rowspan="1" colSpan="1" >Gets user profiles.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getUserStatus](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/getUserStatus.html)</td>

<td rowspan="1" colSpan="1" >Gets users' online statuses.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setSelfInfo](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/setSelfInfo.html)</td>

<td rowspan="1" colSpan="1" >Modifies one's own user profile.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setSelfStatus](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/setSelfStatus.html)</td>

<td rowspan="1" colSpan="1" >Sets the status of the current logged-in user.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addToBlackList](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/addToBlackList.html)</td>

<td rowspan="1" colSpan="1" >Blocks messages from a user, which means adding the user to the blocklist.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteFromBlackList](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/deleteFromBlackList.html)</td>

<td rowspan="1" colSpan="1" >Unblocks messages from a user, which means removing the user from the blocklist.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getBlackList](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/getBlackList.html)</td>

<td rowspan="1" colSpan="1" >Gets the blocklist.</td>
</tr>
</table>


## Offline Push APIs

We recommend you use the offline push service if you want your app to receive Chat service messages in real time when it runs in the background. As there is no unified push service in the Chinese mainland, you need to configure Android offline push for devices of different vendors separately.
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setAPNSListener](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_manager/V2TIMManager/setAPNSListener.html)</td>

<td rowspan="1" colSpan="1" >Sets the APNs offline push listener.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[doBackground](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_offline_push_manager/V2TIMOfflinePushManager/doBackground.html)</td>

<td rowspan="1" colSpan="1" >Configures offline push.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[doForeground](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_offline_push_manager/V2TIMOfflinePushManager/doForeground.html)</td>

<td rowspan="1" colSpan="1" >Configures offline push.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setOfflinePushConfig](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_offline_push_manager/V2TIMOfflinePushManager/setOfflinePushConfig.html)</td>

<td rowspan="1" colSpan="1" >Configures offline push.</td>
</tr>
</table>


## Friend Management APIs

Tencent Cloud Chat SDK does not check friend relationships by default when sending and receiving messages. To achieve the interactive experience of "add friends first, then send messages", you can log in to the [Console](https://console.trtc.io/) to modify Relationship Check. When enabled, users can only send messages to their friends. When a user sends a message to a non-friend, SDK will report a 20009 error code. The configuration path is: Applications > Your App > Chat > Configuration > Login and Message > Relationship Check.

Use the following API to add or delete friends and manage friend lists.
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addFriendListener](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/addFriendListener.html)</td>

<td rowspan="1" colSpan="1" >Adds a contacts listener.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeFriendListener](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/removeFriendListener.html)</td>

<td rowspan="1" colSpan="1" >Removes a contacts listener.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getFriendList](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/getFriendList.html)</td>

<td rowspan="1" colSpan="1" >Gets the contacts.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getFriendsInfo](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/getFriendsInfo.html)</td>

<td rowspan="1" colSpan="1" >Gets the profiles of specified friends.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setFriendInfo](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/setFriendInfo.html)</td>

<td rowspan="1" colSpan="1" >Sets the profile of a specified friend.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addFriend](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/addFriend.html)</td>

<td rowspan="1" colSpan="1" >Adds a friend.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteFromFriendList](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/deleteFromFriendList.html)</td>

<td rowspan="1" colSpan="1" >Deletes friends.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[checkFriend](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/checkFriend.html)</td>

<td rowspan="1" colSpan="1" >Checks your relationship with a specified user.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getFriendApplicationList](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/getFriendApplicationList.html)</td>

<td rowspan="1" colSpan="1" >Gets the list of friend requests.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[acceptFriendApplication](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/acceptFriendApplication.html)</td>

<td rowspan="1" colSpan="1" >Accepts a friend request.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[refuseFriendApplication](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/refuseFriendApplication.html)</td>

<td rowspan="1" colSpan="1" >Rejects a friend request.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteFriendApplication](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/deleteFriendApplication.html)</td>

<td rowspan="1" colSpan="1" >Deletes a friend request.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setFriendApplicationRead](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/setFriendApplicationRead.html)</td>

<td rowspan="1" colSpan="1" >Marks a friend request as read.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createFriendGroup](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/createFriendGroup.html)</td>

<td rowspan="1" colSpan="1" >Creates a friend list.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getFriendGroups](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/getFriendGroups.html)</td>

<td rowspan="1" colSpan="1" >Gets the information of friend lists.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteFriendGroup](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/deleteFriendGroup.html)</td>

<td rowspan="1" colSpan="1" >Deletes a friend list.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[renameFriendGroup](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/renameFriendGroup.html)</td>

<td rowspan="1" colSpan="1" >Modifies the name of a friend list.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addFriendsToFriendGroup](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/addFriendsToFriendGroup.html)</td>

<td rowspan="1" colSpan="1" >Adds friends to a friend list.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteFriendsFromFriendGroup](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/deleteFriendsFromFriendGroup.html)</td>

<td rowspan="1" colSpan="1" >Deletes friends from a friend list.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[searchFriends](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_friendship_manager/V2TIMFriendshipManager/searchFriends.html)</td>

<td rowspan="1" colSpan="1" >Searches for friends.</td>
</tr>
</table>
