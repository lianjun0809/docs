> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/en/llms.txt
> Use this file to discover all available pages before exploring further.

> **Note:**
> 

> **Do not use APIs of new and old versions at the same time**.
> 


## Initialization and Login APIs

To use the Tencent Cloud Chat service, you need to initialize the SDK and log in.          
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[initSDK](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#ac905c315726b517ba62421471bbecf56)</td>

<td rowspan="1" colSpan="1" >Initializes the SDK.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[unInitSDK](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a8ac73b4f71f9d9a1ca01551c919d3cdd)</td>

<td rowspan="1" colSpan="1" >Uninitializes the SDK.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addIMSDKListener](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a2f0297e96d365013e7923275ce2a5d4e)</td>

<td rowspan="1" colSpan="1" >Adds the Chat listener.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeIMSDKListener](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a9b98e6b9ac0f883f055ef82563467b43)</td>

<td rowspan="1" colSpan="1" >Removes the Chat listener.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getVersion](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a8142d4e71e0ee1b8d2ec99740e2cb1ca)</td>

<td rowspan="1" colSpan="1" >Gets the version number.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getServerTime](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a0f95b1e166f22d261e73fbf01987fb0f)</td>

<td rowspan="1" colSpan="1" >Gets the server time.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[login](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a73fc0e14c5f2f5fc06a80081479fb416)</td>

<td rowspan="1" colSpan="1" >Logs in.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[logout](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a0398924fa1b62a8f5cc9b51673273b48)</td>

<td rowspan="1" colSpan="1" >Logs out.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getLoginStatus](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a1836146275265b2a120412f18961db95)</td>

<td rowspan="1" colSpan="1" >Gets the login status.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getLoginUser](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#ad4b2e5a7df5e786ba369054ac582007f)</td>

<td rowspan="1" colSpan="1" >Gets the UserID of the currently logged-in user.</td>
</tr>
</table>


## Simple Message APIs

Use the following APIs for the sending and receiving of text and signaling (custom buffer) messages.
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addSimpleMsgListener](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#afd96fd1591e41f031421c0655d8e5d6b)</td>

<td rowspan="1" colSpan="1" >Sets an event listener for simple messages (text messages and custom messages). Do not use it and [addAdvancedMsgListener](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#aaccdec10b9fbee5e43eaf908e359c823) at the same time.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeSimpleMsgListener](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a86ac462d87f652960d2600a52009849a)</td>

<td rowspan="1" colSpan="1" >Removes the event listener for simple messages (text messages and custom messages).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[sendC2CTextMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a59a8ba6e4a973b4c40a09ae7dfdc6981)</td>

<td rowspan="1" colSpan="1" >Sends a one-to-one (C2C) text message.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[sendC2CCustomMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#af3e08b936df77210c6cdd0ce5c7fa87f)</td>

<td rowspan="1" colSpan="1" >Sends a one-to-one (C2C) custom (signaling) message.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[sendGroupTextMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a56359fd1ce0a96f289dcd4bef522fb52)</td>

<td rowspan="1" colSpan="1" >Sends a group text message.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[sendGroupCustomMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#afbce8ff97be0a3a42c7dc826d316f2c2)</td>

<td rowspan="1" colSpan="1" >Sends a group custom (signaling) message.</td>
</tr>
</table>


## Signaling APIs
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addSignalingListener](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSignalingManager.html#a862073ac16de7f02e5f97b8cbe7eb028)</td>

<td rowspan="1" colSpan="1" >Adds a signaling listener.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeSignalingListener](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSignalingManager.html#a72f6c032de1b0dbaabb227be54d0bcfc)</td>

<td rowspan="1" colSpan="1" >Removes a signaling listener.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[invite](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSignalingManager.html#a3c0592962ef89e1075f3136fc7117da0)</td>

<td rowspan="1" colSpan="1" >Invites a user.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[inviteInGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSignalingManager.html#a4d166ca73210308fbd79fca748145671)</td>

<td rowspan="1" colSpan="1" >Invites certain users in the group.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[cancel](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSignalingManager.html#a9d69707620f038d6e47356cdaa3ab9bd)</td>

<td rowspan="1" colSpan="1" >Cancels an invitation.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[accept](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSignalingManager.html#a4cd3629a0952db7c59186e0c222e17a0)</td>

<td rowspan="1" colSpan="1" >Accepts an invitation.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[reject](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSignalingManager.html#ad9510bf8a333189fd1a0c1eafbde2266)</td>

<td rowspan="1" colSpan="1" >Rejects an invitation.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getSignalingInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSignalingManager.html#ab303f20f53de134e6f6ebe5f9f9bcad0)</td>

<td rowspan="1" colSpan="1" >Gets the signaling information.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addInvitedSignaling](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSignalingManager.html#ac50301e05e1672b771dc2c92fadff8de)</td>

<td rowspan="1" colSpan="1" >Adds invitation signaling (can be used for invitation signaling triggered by offline push messages for group invitations).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[modifyInvitation](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSignalingManager.html#a5f3eba1a04cfd667b409e0b90478c895)</td>

<td rowspan="1" colSpan="1" >Modifies the invitation signaling.</td>
</tr>
</table>


## Advanced Message APIs

If you need to send/receive rich media messages (such as image, video, and file messages) and use advanced features such as recalling messages, marking messages as read, and querying message history, use the following set of advanced message APIs. Do not use simple message APIs and advanced message APIs at the same time.
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addAdvancedMsgListener](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#aaccdec10b9fbee5e43eaf908e359c823)</td>

<td rowspan="1" colSpan="1" >Sets an event listener for advanced messages. Do not use it and [addSimpleMsgListener](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#afd96fd1591e41f031421c0655d8e5d6b) at the same time.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeAdvancedMsgListener](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a44e1e9126bf5b30234330fe19259cd93)</td>

<td rowspan="1" colSpan="1" >Removes the event listener for advanced messages.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createTextMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a3ea254cd12aa0bcfd004f26f759b76a0)</td>

<td rowspan="1" colSpan="1" >Creates a text message.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createCustomMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a313b1ea616f082f535946c83edd2cc7f)</td>

<td rowspan="1" colSpan="1" >Creates a custom message.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createImageMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#adef5bc7a67b9a69f70f6417fd810d4b1)</td>

<td rowspan="1" colSpan="1" >Creates an image message.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createSoundMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a7e661ce2b4eba1535bd04f3b6539b9dc)</td>

<td rowspan="1" colSpan="1" >Creates an audio message.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createVideoMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#ada17dbc78e9876a8f3a9fd24a73752b5)</td>

<td rowspan="1" colSpan="1" >Creates a video message.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createFileMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a39e4b6609321fd188a2e156a00bb3135)</td>

<td rowspan="1" colSpan="1" >Creates a file message.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createLocationMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a67cebe27192392080fc80a86c80a4321)</td>

<td rowspan="1" colSpan="1" >Creates a location message.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createFaceMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a7ad0f3b7eff3978c12d8c912ca164a5d)</td>

<td rowspan="1" colSpan="1" >Creates an emoji message.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createMergerMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#acebe275789ab49cc8abe6af5e07aa3b0)</td>

<td rowspan="1" colSpan="1" >Creates a combined forward message.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createForwardMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#af8f609bfbfe99a0c65611b14159b6b4d)</td>

<td rowspan="1" colSpan="1" >Creates a single forward message.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createTargetedGroupMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a4def1515746b2840e4b82047a53b91a2)</td>

<td rowspan="1" colSpan="1" >Creates a targeted group message.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createAtSignedGroupMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a23c5c1305996f09c7ff004854b551877)</td>

<td rowspan="1" colSpan="1" >Creates a group @ message.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[sendMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a28e01403acd422e53e999f21ec064795)</td>

<td rowspan="1" colSpan="1" >Sends a message. The message object can be created using a `createXXXMessage` API.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setC2CReceiveMessageOpt](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a6524143895cdee25fabd9aeeae73a3c5)</td>

<td rowspan="1" colSpan="1" >Sets the Mute Notifications option for one-to-one messages.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getC2CReceiveMessageOpt](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a9693dd66432f931ac0a1f2168d899501)</td>

<td rowspan="1" colSpan="1" >Gets the Mute Notifications status for one-to-one messages.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGroupReceiveMessageOpt](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a2735427ac22485626aea278a9d465b3e)</td>

<td rowspan="1" colSpan="1" >Sets the Mute Notifications option for group messages.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setAllReceiveMessageOpt](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a21424ee9df839376ad67d824f95ceb51)</td>

<td rowspan="1" colSpan="1" >Sets the Mute Notifications status for global messages (daily repetition allowed).    </td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setAllReceiveMessageOpt](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a5664f8d53ae660f98c84ff2877e9e036)</td>

<td rowspan="1" colSpan="1" >Sets the Mute Notifications status for global messages.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getAllReceiveMessageOpt](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a0a0f68cf02affa07963e13e388400f51)</td>

<td rowspan="1" colSpan="1" >Gets the Mute Notifications status for global messages.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getC2CHistoryMessageList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#afedccbe0e5229ae15e0e07b722ea39df)</td>

<td rowspan="1" colSpan="1" >Gets one-to-one (C2C) message history.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupHistoryMessageList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a671e8737fcea0c05dc661c753e5b3597)</td>

<td rowspan="1" colSpan="1" >Gets the group message history.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getHistoryMessageList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a97fe2d6a7bab8f45b758f84df48c0b12)</td>

<td rowspan="1" colSpan="1" >Gets message history.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[revokeMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#ad0dfce6be749165cd90a9ff67a1308b1)</td>

<td rowspan="1" colSpan="1" >Recalls a message. The message object can be created using a `createXXXMessage` API.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[modifyMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a5464602189e6af536540e86e8bcbbe73)</td>

<td rowspan="1" colSpan="1" >Modifies a message.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[markC2CMessageAsRead](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a7c09d0ba4a8018f5f9eec4760c4c7b9b)</td>

<td rowspan="1" colSpan="1" >Marks one-to-one (C2C) messages as read (a interface to be abandoned. Use the cleanConversationUnreadMessageCount interface).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[markGroupMessageAsRead](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#ac0a65f18d361abde8a0ac16132027e69)</td>

<td rowspan="1" colSpan="1" >Marks group messages as read (a interface to be abandoned. Use the cleanConversationUnreadMessageCount interface).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[markAllMessageAsRead](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#ad097a0da2ea0002f2b0f2d1d11f3a4ab)</td>

<td rowspan="1" colSpan="1" >Marks all conversations as read (a interface to be abandoned. Use the cleanConversationUnreadMessageCount interface).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteMessageFromLocalStorage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#aa31e3b48fb666b970120fc0bc6343534)</td>

<td rowspan="1" colSpan="1" >Deletes a message from the local storage.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteMessages](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#adb346fede13d493e415f6574df911e9a)</td>

<td rowspan="1" colSpan="1" >Deletes messages from local storage and the cloud.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[clearC2CHistoryMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a29aa6e75c2238c35cc609bef0e5a46ce)</td>

<td rowspan="1" colSpan="1" >Clears chat history with a user from local storage and the cloud.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[clearGroupHistoryMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a6e1a1dce441243d0bd5ac2f8bcecb3d9)</td>

<td rowspan="1" colSpan="1" >Clears chat history of a group from local storage and the cloud.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[insertGroupMessageToLocalStorage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a04a3f6c250f9d6c0053fd71be74f047f)</td>

<td rowspan="1" colSpan="1" >Inserts a message in a group chat.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[insertC2CMessageToLocalStorage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a5afe4461b4a47205d2865ea94317d4aa)</td>

<td rowspan="1" colSpan="1" >Inserts a message in a one-to-one chat.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[findMessages](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#ad0dbaec04bc389d01f815f46c550e2fd)</td>

<td rowspan="1" colSpan="1" >Finds local messages by `msgID`.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[searchLocalMessages](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a9364c8a0c6a0899b17c0a479b8ca848a)</td>

<td rowspan="1" colSpan="1" >Searches for local messages.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[searchCloudMessages](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a16a4a38b3f08bf7707d949ba9674102f)</td>

<td rowspan="1" colSpan="1" >Searchs for cloud messages.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[sendMessageReadReceipts](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a66ec09cb444ddca989e9518d5118275d)</td>

<td rowspan="1" colSpan="1" >Sends message read receipts.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getMessageReadReceipts](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a50e3bc679e196866057415a7c192abf6)</td>

<td rowspan="1" colSpan="1" >Gets message read receipts.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupMessageReadMemberList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a93c48782f3e127e8a50aef1bf8829099)</td>

<td rowspan="1" colSpan="1" >Gets the list of group members who have read group messages.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setMessageExtensions](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a155f6219c2bbf7bc510beec9e905d5db)</td>

<td rowspan="1" colSpan="1" >Sets message extensions.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getMessageExtensions](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a832534327c08326d045c44b02f7ddbb7)</td>

<td rowspan="1" colSpan="1" >Gets message extensions.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteMessageExtensions](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a25c02e90cd0940d34fe3bbfd803cc278)</td>

<td rowspan="1" colSpan="1" >Deletes message extensions.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addMessageReaction](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#af47c3e1fb1ac73f7e2ba7bf739c9452a)</td>

<td rowspan="1" colSpan="1" >Adds message reaction.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeMessageReaction](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a8af85ef9a47c6d498c601dad1370de32)</td>

<td rowspan="1" colSpan="1" >Removes message reaction.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getMessageReactions](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#aa6d5f0421950c7354dd4f0de48814881)</td>

<td rowspan="1" colSpan="1" >Gets message reactions.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getAllUserListOfMessageReaction](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a6af80059a956df9948286dc3007d4c1f)</td>

<td rowspan="1" colSpan="1" >Gets all user list of message reaction.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[pinGroupMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#aa345a7876bf0df29491429329a10f469)</td>

<td rowspan="1" colSpan="1" >Sets group message pinning.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getPinnedGroupMessageList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a35c28770388fa0b1c51946b314287786)</td>

<td rowspan="1" colSpan="1" >Gets pinned group message list.</td>
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
<td rowspan="1" colSpan="1" >[addGroupListener](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a8dde0362f00a454945e7811c8a726a38)</td>

<td rowspan="1" colSpan="1" >Adds a group listener.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeGroupListener](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#ab4d57bd5fd4b2d71c29daaeee8b9b760)</td>

<td rowspan="1" colSpan="1" >Removes a group listener.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#af836e4912f668dddf6cc679233cfb0bb)</td>

<td rowspan="1" colSpan="1" >Creates a (simple) group</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a121d53137a38d0fc0bc8a8e0a9c55647)</td>

<td rowspan="1" colSpan="1" >Creates an (advanced) group. The group information and the initial group members can be set during group creation.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[joinGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#ad64a09bea508672d6d5a402b3455b564)</td>

<td rowspan="1" colSpan="1" >Joins a group.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[quitGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a6d140dbeb44906de9cb69f69c2ce5919)</td>

<td rowspan="1" colSpan="1" >Leaves a group.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[dismissGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#afd0221c0c842a6dcfa0acc657e50caeb)</td>

<td rowspan="1" colSpan="1" >Disbands a group. Only the group owner and group admin can delete a group.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getJoinedGroupList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a0199b7cacc6919938d8342474bd252da)</td>

<td rowspan="1" colSpan="1" >Gets the list of groups the current user has joined, excluding audio-video groups.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupsInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ada614335043d548c11f121500e279154)</td>

<td rowspan="1" colSpan="1" >Pulls the profiles of groups.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[searchGroups](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a94a72082b7e2682942f35196a7e28023)</td>

<td rowspan="1" colSpan="1" >Search for local group profiles</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[searchCloudGroups](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a322641b6386d4698dd1611fee69891e0)</td>

<td rowspan="1" colSpan="1" >Search for cloud group profiles</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGroupInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ad4ceef92975fa00c4a5dddc8f7e1edcf)</td>

<td rowspan="1" colSpan="1" >Modifies a group profile.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[initGroupAttributes](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a17569b57abc77adb6be9356b9eb70182)</td>

<td rowspan="1" colSpan="1" >Initializes group attributes.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGroupAttributes](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a3ec31101e4763dab7a1c99a71bc3da08)</td>

<td rowspan="1" colSpan="1" >Sets group attributes.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteGroupAttributes](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a45f211bafddc58bf5e199e18a6814578)</td>

<td rowspan="1" colSpan="1" >Deletes group attributes.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupAttributes](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ade2155fb24ed1c0b8eb976e146c14e3d)</td>

<td rowspan="1" colSpan="1" >Gets group attributes.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupOnlineMemberCount](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a56840105a4b3371eeab2046d8c300bce)</td>

<td rowspan="1" colSpan="1" >Gets the number of online group members.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGroupCounters](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ab2359bff0ebe5a07a87242023206989f)</td>

<td rowspan="1" colSpan="1" >Sets group counters.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupCounters](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a3f70b0f1054a7bf78a9069a01b842cad)</td>

<td rowspan="1" colSpan="1" >Gets group counters.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[increaseGroupCounter](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ad770cab3620a21671d7f83776d56814e)</td>

<td rowspan="1" colSpan="1" >Increment group counters.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[decreaseGroupCounter](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ad5841f8f77442c8d0cf1a209a55db6c2)</td>

<td rowspan="1" colSpan="1" >Decrement group counters.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupMemberList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a69fc0831aacaa0585c1855f4c91320be)</td>

<td rowspan="1" colSpan="1" >Gets the group member list.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupMembersInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#adb08e1c4fa9aff407c7b2678757f66d5)</td>

<td rowspan="1" colSpan="1" >Gets the profiles of specified group members.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[searchGroupMembers](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a493fb73258019961f3ca8934ff625b0a)</td>

<td rowspan="1" colSpan="1" >Search for local group members</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[searchCloudGroupMembers](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a1db4218077a0db6c623a19d66ba72b5a)</td>

<td rowspan="1" colSpan="1" >Search for cloud group members</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGroupMemberInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a6f1cf8ede41348b4cd7b63b8e4caa77b)</td>

<td rowspan="1" colSpan="1" >Modifies the profile of a specified group member.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[muteGroupMember](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a450230c4d129611e1b0519827ec0f8b5)</td>

<td rowspan="1" colSpan="1" >Mutes group members.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[muteAllGroupMembers](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ab3f057b439e976b17dcc0e2e9be5e7d1)</td>

<td rowspan="1" colSpan="1" >Mute all group members. Only administrators or group owners can call this function.  </td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[kickGroupMember](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a6da6755c6e0c46e96cb02575074a5333)</td>

<td rowspan="1" colSpan="1" >Removes a member from a group.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGroupMemberRole](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a34ebf60528d02626834f022b4ebabfa8)</td>

<td rowspan="1" colSpan="1" >Sets the role of a group member.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[markGroupMemberList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#abdd5f157904dd50012c7a93f66f85dba)</td>

<td rowspan="1" colSpan="1" >Marks group members.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[transferGroupOwner](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ac16d66c8e293c2ee95c7b673e5ad80c4)</td>

<td rowspan="1" colSpan="1" >Transfers the group ownership.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[inviteUserToGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#afd219107653b877e446c149531d65e92)</td>

<td rowspan="1" colSpan="1" >Invites users to a group.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupApplicationList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a240db7bdc023ad6fc63e9ee9b72714c4)</td>

<td rowspan="1" colSpan="1" >Gets the list of requests to join a group.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[acceptGroupApplication](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ad743008d30c909ef0be0f8aa91102e07)</td>

<td rowspan="1" colSpan="1" >Approves a request to join a group.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[refuseGroupApplication](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#aa518c54e77f7c0f6e7dd129d6c433acd)</td>

<td rowspan="1" colSpan="1" >Rejects a request to join a group.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGroupApplicationRead](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a498d9d76217cbae0aa235ac928ad02d8)</td>

<td rowspan="1" colSpan="1" >Marks the request list as read.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getJoinedCommunityList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#acb37b83f357fc7ee04905f8bcd5a5c67)</td>

<td rowspan="1" colSpan="1" >Gets the list of community groups the current user has joined.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createTopicInCommunity](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a52eed1b07ad64a3aa3d3561d8cd147f0)</td>

<td rowspan="1" colSpan="1" >Creates a topic.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteTopicFromCommunity](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a77c4502346e800e43c22a0f15138d699)</td>

<td rowspan="1" colSpan="1" >Deletes a topic.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setTopicInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#acaff2edad6eb208478be9ab06d30035d)</td>

<td rowspan="1" colSpan="1" >Modifies topic information.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getTopicInfoList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a5d2b18a76cff650cb9bb2abf2ef07306)</td>

<td rowspan="1" colSpan="1" >Gets the list of topics.</td>
</tr>
</table>


## Community Topic-Related APIs

If you need to create topics under a community, please use this set of interfaces. Communities are used to manage group members, and all topics under a community can not only share community members but also send and receive messages independently without interfering with each other.
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[﻿addCommunityListener﻿](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMCommunityManager.html#a431aca797c3047dee3b5f8db4722902d)</td>

<td rowspan="1" colSpan="1" >Adds a community listener.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[﻿removeCommunityListener﻿](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMCommunityManager.html#a96411e5a6c3896aff3bdbcf86387e928)</td>

<td rowspan="1" colSpan="1" >Removes a community listener.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[﻿createCommunity﻿](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMCommunityManager.html#acde81364ecec194dfa20720f670d8537)</td>

<td rowspan="1" colSpan="1" >Creates a community with topic support.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[﻿getJoinedCommunityList﻿](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMCommunityManager.html#acb37b83f357fc7ee04905f8bcd5a5c67)</td>

<td rowspan="1" colSpan="1" >Gets the list of communities with topic support that the current user has joined.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[﻿createTopicInCommunity﻿](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMCommunityManager.html#a52eed1b07ad64a3aa3d3561d8cd147f0)</td>

<td rowspan="1" colSpan="1" >Creates a topic.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[﻿deleteTopicFromCommunity﻿](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMCommunityManager.html#a77c4502346e800e43c22a0f15138d699)</td>

<td rowspan="1" colSpan="1" >Deletes a topic.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[﻿setTopicInfo﻿](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMCommunityManager.html#acaff2edad6eb208478be9ab06d30035d)</td>

<td rowspan="1" colSpan="1" >Modifies topic information.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[﻿getTopicInfoList﻿](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMCommunityManager.html#a5d2b18a76cff650cb9bb2abf2ef07306)</td>

<td rowspan="1" colSpan="1" >Gets a topic list.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[﻿createPermissionGroupInCommunity﻿](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMCommunityManager.html#a92908f8d46063504d6f8b0d0f04f3a6b)</td>

<td rowspan="1" colSpan="1" >Creates a community permission group.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[﻿deletePermissionGroupFromCommunity﻿](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMCommunityManager.html#a74e98c5144576fca599378e672b54d1f)</td>

<td rowspan="1" colSpan="1" >Deletes a community permission group.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[﻿modifyPermissionGroupInfoInCommunity﻿](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMCommunityManager.html#a2a5d15a05b455c73f5e8e8c7eab7ad0d)</td>

<td rowspan="1" colSpan="1" >Modifies a community permission group.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[﻿getJoinedPermissionGroupListInCommunity﻿](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMCommunityManager.html#af3b2e3c995525d3f6be17fbd4f42ad2b)</td>

<td rowspan="1" colSpan="1" >Gets the list of community permission groups the current user has joined.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[﻿getPermissionGroupListInCommunity﻿](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMCommunityManager.html#a9f6e4a2c4f4380db7b7066f9c8a13379)</td>

<td rowspan="1" colSpan="1" >Gets the list of community permission groups.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[﻿addCommunityMembersToPermissionGroup﻿](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMCommunityManager.html#a79757d4803e94cdfe15deb4e7789e043)</td>

<td rowspan="1" colSpan="1" >Adds members to a community permission group.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[﻿removeCommunityMembersFromPermissionGroup﻿](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMCommunityManager.html#a5d48a2141728bd791129eefb9d88e262)</td>

<td rowspan="1" colSpan="1" >Removes members from a community permission group.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[﻿getCommunityMemberListInPermissionGroup﻿](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMCommunityManager.html#a2d8f6477d76254d4dec9bd0f1a4c8051)</td>

<td rowspan="1" colSpan="1" >Gets the member list of a community permission group.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[﻿addTopicPermissionToPermissionGroup﻿](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMCommunityManager.html#a7e7d5b6960571ddbf61ba5a6f7390bc9)</td>

<td rowspan="1" colSpan="1" >Adds topic permissions to a permission group.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[﻿deleteTopicPermissionFromPermissionGroup﻿](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMCommunityManager.html#af3ee95182ef6b9520cb2d1c2729e575f)</td>

<td rowspan="1" colSpan="1" >Removes topic permissions from a permission group.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[﻿modifyTopicPermissionInPermissionGroup﻿](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMCommunityManager.html#a52852fc6b1c18b6a3379d25ea4001acf)</td>

<td rowspan="1" colSpan="1" >Modifies topic permissions in a permission group.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[﻿getTopicPermissionInPermissionGroup﻿](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMCommunityManager.html#a380f75b59c0ee32911a7cba6a2a88971)</td>

<td rowspan="1" colSpan="1" >Gets topic permissions in a permission group.</td>
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
<td rowspan="1" colSpan="1" >[addConversationListener](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a806534684e5d4d01b94126cd1397fee4)</td>

<td rowspan="1" colSpan="1" >Adds a conversation listener.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeConversationListener](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a661d479b6f704a2e319d0c744b8ad2bc)</td>

<td rowspan="1" colSpan="1" >Removes a conversation listener.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getConversationList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#abf71156b8b6423e98943e25a77dc1967)</td>

<td rowspan="1" colSpan="1" >Gets the conversation list.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getConversationListByFilter](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#abf71156b8b6423e98943e25a77dc1967)</td>

<td rowspan="1" colSpan="1" >Gets the advanced conversation API to specify the conversation type, mark type, and group name.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getConversation](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a619aaff2bb5664e094d2341819b95096)</td>

<td rowspan="1" colSpan="1" >Gets a conversation.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getConversationList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a1bb5ba2beecb4f68146e7f664124fd8b)</td>

<td rowspan="1" colSpan="1" >Gets multiple conversations.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteConversation](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a7a6e38c5a7431646bd4c0c4c66279077)</td>

<td rowspan="1" colSpan="1" >Deletes a conversation.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteConversationList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#acd95bca253be53ce89395f77c1b42c70)</td>

<td rowspan="1" colSpan="1" >Deletes a conversation list.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setConversationDraft](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#ae7f2f52bf375dae69368eae42edb28ab)</td>

<td rowspan="1" colSpan="1" >Sets a draft for a conversation.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setConversationCustomData](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#ac11ca7227145e3f359f6a3473ed600a5)</td>

<td rowspan="1" colSpan="1" >Sets custom conversation data.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[pinConversation](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a4da7467f54c891c4929152260e42f4b6)</td>

<td rowspan="1" colSpan="1" >Pins a conversation to the top.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[markConversation](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#aa1dab66f08df9aef4acb0aad8cb77d72)</td>

<td rowspan="1" colSpan="1" >Marks a conversation.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getTotalUnreadMessageCount](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a08bdd15d7ee2737335a01285d7f9c44a)</td>

<td rowspan="1" colSpan="1" >Gets the total unread message count.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getUnreadMessageCountByFilter](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#ad68a1302b6cb775e09c4b4277bcb0c96)</td>

<td rowspan="1" colSpan="1" >Gets the total number of unread messages filtered by conversation.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[﻿subscribeUnreadMessageCountByFilter﻿](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a27b7c9477c5a2fb4c4f05b2e499d6f61)</td>

<td rowspan="1" colSpan="1" >Registers a listener for changes in the total number of unread messages in a specific conversation.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[﻿unsubscribeUnreadMessageCountByFilter﻿](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#adbf33f34fa911bbeec55cf3a4f320ba7)</td>

<td rowspan="1" colSpan="1" >Unregisters a listener for changes in the total number of unread messages in a specific conversation.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[cleanConversationUnreadMessageCount](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a5887d1954d32fad68bc569e6f136770d)</td>

<td rowspan="1" colSpan="1" >Clears the unread message count for a conversation.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[ createConversationGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a280dff193ef770efd5d878ca3e3821d5)</td>

<td rowspan="1" colSpan="1" >Creates a conversation group.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[ getConversationGroupList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#ab469fbf92cfdf27d7b268e494028b589)</td>

<td rowspan="1" colSpan="1" >Gets the list of conversation groups.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[ deleteConversationGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a5ec09de4e1fb5e898e4c0800b06a63bc)</td>

<td rowspan="1" colSpan="1" >Deletes a conversation group.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[ renameConversationGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a0eba052e8f21602b5dbd249ada0c18eb)</td>

<td rowspan="1" colSpan="1" >Renames a conversation group.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[ addConversationsToGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#abf0cd490796ff60730aa0a8fec037d87)</td>

<td rowspan="1" colSpan="1" >Adds a conversation to a conversation group.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[ deleteConversationsFromGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a9ca6ea0ac6d8f61c7d0f8a85f14a91b9)</td>

<td rowspan="1" colSpan="1" >Deletes a conversation from a conversation group.</td>
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
<td rowspan="1" colSpan="1" >[getUsersInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a7ca8c0f71a9875021fc35dfcaff68d1e)</td>

<td rowspan="1" colSpan="1" >Gets user profiles.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setSelfInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#af004ab2f1d1458de354883f1995b678a)</td>

<td rowspan="1" colSpan="1" >Modifies one's own user profile.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[﻿subscribeUserInfo﻿](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a4d14dda5e99d821c84dea4ae25e403af)</td>

<td rowspan="1" colSpan="1" >Subscribe to user profile.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[﻿unsubscribeUserInfo﻿](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#af42e383f564f7d5bb9b4d39a3e00d4d9)</td>

<td rowspan="1" colSpan="1" >Unsubscribe from user profile.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getUserStatus](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a2428c7f87859dd85bed1730ad8d3b92a)</td>

<td rowspan="1" colSpan="1" >Queries a user's status.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setSelfStatus](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a7520045679f1493c890f2b3b5eee7b84)</td>

<td rowspan="1" colSpan="1" >Sets one's own status.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[subscribeUserStatus](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a9c6deb154d0042d5472ec55cfe0962bb)</td>

<td rowspan="1" colSpan="1" >Subscribes to a user's status.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[unsubscribeUserStatus](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a9254db13bd53dc48a04d05ba5f116d39)</td>

<td rowspan="1" colSpan="1" >Unsubscribes from a user's status.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[searchUsers](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a20281f80a6dddc7b5dd61c203a6efadb)</td>

<td rowspan="1" colSpan="1" >Search cloud users</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addToBlackList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a8804c7f47000bf1c26aa6ab744a53456)</td>

<td rowspan="1" colSpan="1" >Blocks messages from a user, which means adding the user to the blocklist.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteFromBlackList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a3dcd8f1c70dceafa94ab48796c2f26aa)</td>

<td rowspan="1" colSpan="1" >Unblocks messages from a user, which means removing the user from the blocklist.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getBlackList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a6269df2d96c910648ab2f0c43e1931c6)</td>

<td rowspan="1" colSpan="1" >Gets the blocklist.</td>
</tr>
</table>


## Offline Push APIs

We recommend you use the offline push service if you want your app to receive Chat service messages in real time when it runs in the background. As there is no unified push service in the Chinese mainland, you need to [configure Android offline push](https://intl.cloud.tencent.com/document/product/1047/39156) for devices of different vendors separately.
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setOfflinePushConfig](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushManager.html#a494d6cafe50ba25503979a4e0f14c28e)</td>

<td rowspan="1" colSpan="1" >Configures offline push.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[﻿doBackground﻿](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushManager.html#a2b191294ac4d68a2d69e482eae1b638f)</td>

<td rowspan="1" colSpan="1" >The APP can call this interface when it detects that the application has entered the background, which can be used to initialize the unread count for the desktop application badge.  </td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[﻿doForeground﻿](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushManager.html#a4c2ff4eea609da1d0950648905fbf6aa)</td>

<td rowspan="1" colSpan="1" >The APP can call this interface when it detects that the application has entered the foreground.  </td>
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
<td rowspan="1" colSpan="1" >[addFriendListener](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#af09d0d2297fe73cc81b8e8941bcd35b2)</td>

<td rowspan="1" colSpan="1" >Adds a contacts listener.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeFriendListener](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a6a823459f109bcd8744806f8f1b8bfea)</td>

<td rowspan="1" colSpan="1" >Removes a contacts listener.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getFriendList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#ae478de55db21d42b72a6c5a6a5d16624)</td>

<td rowspan="1" colSpan="1" >Gets the contacts.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getFriendsInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a8c4e51e508d140e4a7ce5f4caf49c870)</td>

<td rowspan="1" colSpan="1" >Gets the profiles of specified friends.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setFriendInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a151b7de6219d966b4194ad7fcc8450fe)</td>

<td rowspan="1" colSpan="1" >Sets the profile of a specified friend.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[searchFriends](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a3e657c9ec5d68a4c423a64d71f5f9c6e)</td>

<td rowspan="1" colSpan="1" >Searches for friends.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addFriend](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a19d0f22aaea285e8cee85a5dd6ed9208)</td>

<td rowspan="1" colSpan="1" >Adds a friend.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteFromFriendList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#af7ecf8641b58462d038a9c97bfbd4d61)</td>

<td rowspan="1" colSpan="1" >Deletes a friend.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[checkFriend](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a96bb74f3bbd1aef147ec914a81104d11)</td>

<td rowspan="1" colSpan="1" >Checks relationship with specified users.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getFriendApplicationList](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a2dbf4da19f3b9b170089b8e8cb210166)</td>

<td rowspan="1" colSpan="1" >Gets the list of friend requests.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[acceptFriendApplication](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#ab69ed69330428caff6f468b7df5259fa)</td>

<td rowspan="1" colSpan="1" >Accepts a friend request.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[refuseFriendApplication](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#af1bcbc196015de8e7a94b1575c466f89)</td>

<td rowspan="1" colSpan="1" >Rejects a friend request.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteFriendApplication](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a5c869e3358ca74f9cd2eaebfc7298490)</td>

<td rowspan="1" colSpan="1" >Deletes a friend request.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setFriendApplicationRead](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a022b4817a31dd25707f14b8184c42675)</td>

<td rowspan="1" colSpan="1" >Marks a friend request as read.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createFriendGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#afe729e7a74d1e7fd06a5f23c155a08ae)</td>

<td rowspan="1" colSpan="1" >Creates a friend list.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getFriendGroups](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a0043ca81fdeec5d3e842e85278003d1e)</td>

<td rowspan="1" colSpan="1" >Gets the information of friend lists.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteFriendGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#ac9f06f447ee4452aa12e078b48023cee)</td>

<td rowspan="1" colSpan="1" >Deletes friend lists.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[renameFriendGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a5345957f4d75d8e57ea3b4cff9adee13)</td>

<td rowspan="1" colSpan="1" >Modifies the name of a friend list.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addFriendsToFriendGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a6de9168d476ac14e21025ec5c26251df)</td>

<td rowspan="1" colSpan="1" >Adds friends to a friend list.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteFriendsFromFriendGroup](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#ae367dfec88522e96d96c5ab942e50653)</td>

<td rowspan="1" colSpan="1" >Removes friends from a friend list.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[﻿subscribeOfficialAccount﻿](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a561a3334dd1f4b75de9099d161ed7f5b)</td>

<td rowspan="1" colSpan="1" >Subscribes to official accounts.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[unsubscribeOfficialAccount](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a7569dd95b90eab4293a6f7e99dba2c6f)</td>

<td rowspan="1" colSpan="1" >Unsubscribes from official accounts.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[﻿getOfficialAccountsInfo﻿](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a7493324aced496edd8ca7a9feac3055e)</td>

<td rowspan="1" colSpan="1" >Gets the list of official accounts.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[﻿followUser﻿](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a136b5a3e39002162738972e891c7e82d)</td>

<td rowspan="1" colSpan="1" >Follows users.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[﻿unfollowUser﻿](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a4342b42c4cf9fc8bc2bea86d60f2d9c9)</td>

<td rowspan="1" colSpan="1" >Unfollows users.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[﻿getMyFollowingList﻿](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a973bb520f0f7a28973ac84643dbd5583)</td>

<td rowspan="1" colSpan="1" >Gets my follow list.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[﻿getMyFollowersList﻿](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a856e9a9ecaaac6b1b855749de4bcbdcd)</td>

<td rowspan="1" colSpan="1" >Gets my fan list.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[﻿getMutualFollowersList﻿](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a18bad586fdd7ddd2d4bfc4a3f514d3c6)</td>

<td rowspan="1" colSpan="1" >Gets my mutual follow list.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[﻿getUserFollowInfo﻿](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#a86ff97aed8e6476ff6393660c8433f5d)</td>

<td rowspan="1" colSpan="1" >Gets the follow/fan/mutual follow count information for a specified user.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[﻿checkFollowType﻿](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFriendshipManager.html#aeb364a11188590a7e6093522f5bad415)</td>

<td rowspan="1" colSpan="1" >Checks the follow type of a specified user.</td>
</tr>
</table>
