> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
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
<td rowspan="1" colSpan="1" >[initSDK](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a8035eed3a7c9b3b1c229196ac7bc5da6)</td>

<td rowspan="1" colSpan="1" >Initializes the SDK.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[unInitSDK](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a286e5358ec4cd0a8f9c66f4d2d7d4544)</td>

<td rowspan="1" colSpan="1" >Uninitializes the SDK</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addIMSDKListener](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#ac569656a58908afba491710a8cb3c8d9)</td>

<td rowspan="1" colSpan="1" >Adds the Chat listener.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeIMSDKListener](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a2e2a7e64bf51888c98636e5974a8aca7)</td>

<td rowspan="1" colSpan="1" >Removes the Chat listener.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getVersion](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#ae8281def98e669d701171ede7aa3c176)</td>

<td rowspan="1" colSpan="1" >Gets the version number.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getServerTime](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a4adcf2642bcb706cd6cfe7e5c5f85f06)</td>

<td rowspan="1" colSpan="1" >Gets the server time.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[login](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a38c42943046acdaf615915c9422af07c)</td>

<td rowspan="1" colSpan="1" >Logs in.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[logout](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a20b495d7f7a231ea33507ca4a79f811f)</td>

<td rowspan="1" colSpan="1" >Logs a user out</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getLoginUser](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a78ca7f39bca860e46620f8f766508fb0)</td>

<td rowspan="1" colSpan="1" >Gets the currently logged-in user.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getLoginStatus](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#acfd2f6366780badf80ebf66d95550f89)</td>

<td rowspan="1" colSpan="1" >Gets the login status</td>
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
<td rowspan="1" colSpan="1" >[addSimpleMsgListener](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a149cdf7924aa13746692d18d605def88)</td>

<td rowspan="1" colSpan="1" >Sets an event listener for simple messages (text messages and custom messages).Do not use this API and [addAdvancedMsgListener](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#acf794752cc6bfa786aea5cd7fabadfab) at the same time.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeSimpleMsgListener](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#afa3040f676105f3fb78d4835ee3c898b)</td>

<td rowspan="1" colSpan="1" >Removes the event listener for simple messages (text messages and custom messages)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[sendC2CTextMessage](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a50d63810093eccc0491d058d0b883618)</td>

<td rowspan="1" colSpan="1" >Sends a one-to-one chat (C2C) text message</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[sendC2CCustomMessage](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a5fc3b87e9782e679c08926d07e486b90)</td>

<td rowspan="1" colSpan="1" >Sends a one-to-one chat (C2C) custom (signaling) message</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[sendGroupTextMessage](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a07788874071937fac6c7093185b145f7)</td>

<td rowspan="1" colSpan="1" >Sends a group chat text message</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[sendGroupCustomMessage](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a537560a58d49aad36406f6d9db6ded65)</td>

<td rowspan="1" colSpan="1" >Sends a group chat custom (signaling) message</td>
</tr>
</table>


## Signaling APIs
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addSignalingListener](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Signaling_08.html#a3a7fde0d4d5a342bd93299deaf98e1d1)</td>

<td rowspan="1" colSpan="1" >Adds a signaling listener.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeSignalingListener](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Signaling_08.html#ae730297ec335735eee3c2f3c464bde33)</td>

<td rowspan="1" colSpan="1" >Removes a signaling listener.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[invite](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Signaling_08.html#a594071fa1a70373582ed6082c581b332)</td>

<td rowspan="1" colSpan="1" >Invites a user.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[inviteInGroup](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Signaling_08.html#ac01a4e703c925aaf5f78df67faca15be)</td>

<td rowspan="1" colSpan="1" >Invites certain users in a group.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[cancel](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Signaling_08.html#acaac35e5db28db783420b5eb39d53e6f)</td>

<td rowspan="1" colSpan="1" >Cancels an invitation.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[accept](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Signaling_08.html#a1ffb6daba9deed8780f869205daf7771)</td>

<td rowspan="1" colSpan="1" >Accepts an invitation.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[reject](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Signaling_08.html#a39e685924aaa4d22daa88f2ec96aa827)</td>

<td rowspan="1" colSpan="1" >Rejects an invitation.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getSignalingInfo](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Signaling_08.html#a0b149836793b8f2d54889b1c3ae40362)</td>

<td rowspan="1" colSpan="1" >Gets the signaling information.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addInvitedSignaling](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Signaling_08.html#aedfb31fdd3289af36c092b55adeed231)</td>

<td rowspan="1" colSpan="1" >Adds invitation signaling (can be used for invitation signaling triggered by offline push messages for group invitations).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[modifyInvitation](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Signaling_08.html#a1f1d6f5053c07996a611e284ac15cbb5)</td>

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
<td rowspan="1" colSpan="1" >[addAdvancedMsgListener](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#acf794752cc6bfa786aea5cd7fabadfab)</td>

<td rowspan="1" colSpan="1" >Sets an event listener for advanced messages. Do not use this API and [addSimpleMsgListener](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a149cdf7924aa13746692d18d605def88) at the same time.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeAdvancedMsgListener](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a28aeebff4a791c9bb8f91a4f61e020e6)</td>

<td rowspan="1" colSpan="1" >Removes the listener for advanced messages</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createTextMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a609f4d4c374d9df3abf9974ff8112fc3)</td>

<td rowspan="1" colSpan="1" >Creates a text message</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createTextAtMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#aaebbd8ed9b9766d01f996ec722744346)</td>

<td rowspan="1" colSpan="1" >Creates an @ text message.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createCustomMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a7a38c42f63a4e0c9e89f6c56dd0da316)</td>

<td rowspan="1" colSpan="1" >Creates a custom message</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createImageMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a23033a764f0d95ce83c52f3cdeea4137)</td>

<td rowspan="1" colSpan="1" >Creates an image message</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createSoundMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a9073007806fa186b8999ce656555032a)</td>

<td rowspan="1" colSpan="1" >Creates a voice message.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createVideoMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a233a9ee5ef2ea371206005d109757f18)</td>

<td rowspan="1" colSpan="1" >Creates a video message</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createFileMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a9e487ae9541111038ebed900ab639d4c)</td>

<td rowspan="1" colSpan="1" >Creates a file message.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createLocationMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a2a997472dd62d794cfd4e3a42cfab930)</td>

<td rowspan="1" colSpan="1" >Creates a location message</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createFaceMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#ab7a593be2cca1c8eddd7e73255f3f34a)</td>

<td rowspan="1" colSpan="1" >Creates an emoji message</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createMergerMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a2943bb31403aeb22f8582cd9966cf13e)</td>

<td rowspan="1" colSpan="1" >Creates a combined forward message.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createForwardMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a05d088b7d9883e18af41355cdd3f4562)</td>

<td rowspan="1" colSpan="1" >Creates a single forward message.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createTargetedGroupMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a8bddd2f566a53362b4da5448fdd18fbc)</td>

<td rowspan="1" colSpan="1" >Creates a targeted group message.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createAtSignedGroupMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#adfb065794694a2061af2642f18c4aeb7)</td>

<td rowspan="1" colSpan="1" >Creates a group @ message.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[sendMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a681947465d6ab718da40f7f983740a21)</td>

<td rowspan="1" colSpan="1" >Sends a message. The message object can be created using a `createXXXMessage` API.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setC2CReceiveMessageOpt](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#ae628f19d856921d27081c3f40005e9d9)</td>

<td rowspan="1" colSpan="1" >Sets the Mute Notifications option for one-to-one messages.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getC2CReceiveMessageOpt](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a1c743a6fe1d17a21dc80e584fd1de2d1)</td>

<td rowspan="1" colSpan="1" >Gets the Mute Notifications status for one-to-one messages.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGroupReceiveMessageOpt](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a379eeef926e41ec5d48287e7fb55b80a)</td>

<td rowspan="1" colSpan="1" >Sets the Mute Notifications option for group messages.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getC2CHistoryMessageList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#abca63ad64f69aa4f424cf11849a9b89e)</td>

<td rowspan="1" colSpan="1" >Gets the one-to-one chat (C2C) message history</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupHistoryMessageList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a9e242ba327377fe74b83e8d5572d39a0)</td>

<td rowspan="1" colSpan="1" >Gets the group chat message history</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getHistoryMessageList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a99e8f00ee60df12e346548b743523218)</td>

<td rowspan="1" colSpan="1" >Gets the message history.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[revokeMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a2ef856a792923811e9d16ed7a101336a)</td>

<td rowspan="1" colSpan="1" >Recalls a message. The message object can be created using a `createXXXMessage` API.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[modifyMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a7609c2dd8550e43b23d24069200d37cb)</td>

<td rowspan="1" colSpan="1" >Modifies a message.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[markC2CMessageAsRead](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#acb3a67bd2fa131b50c611a48fa78f34d)</td>

<td rowspan="1" colSpan="1" >Marks one-to-one chat (C2C) messages as read</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[markGroupMessageAsRead](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a7fc79e30877b8d77fbdfa24e057376dc)</td>

<td rowspan="1" colSpan="1" >Marks group messages as read</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[markAllMessageAsRead](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a53d889a6242b5551aa3655e40967a62f)</td>

<td rowspan="1" colSpan="1" >Marks all conversations as read.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteMessageFromLocalStorage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a2bb42528f4d166ac826914094655841c)</td>

<td rowspan="1" colSpan="1" >Deletes a message from the local storage</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteMessages](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a9e394ea720ecdc10d497b63b6f2b22c4)</td>

<td rowspan="1" colSpan="1" >Deletes messages from local storage and the cloud.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[clearC2CHistoryMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a005c7767172d9a3980974b68c780c33b)</td>

<td rowspan="1" colSpan="1" >Clears chat history with a user from local storage and the cloud.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[clearGroupHistoryMessage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a16c01c19a285e2bd11443c868c8256e6)</td>

<td rowspan="1" colSpan="1" >Clears chat history of a group from local storage and the cloud.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[insertGroupMessageToLocalStorage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a9b312b67e4da19978b55a7b915815dfe)</td>

<td rowspan="1" colSpan="1" >Inserts a message in a group chat.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[insertC2CMessageToLocalStorage](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#acc1dccd310d1965248cff0d4fd5ca45f)</td>

<td rowspan="1" colSpan="1" >Inserts a message in a one-to-one chat.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[findMessages](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a4a0c47d706d8784656225c1e9065f6f1)</td>

<td rowspan="1" colSpan="1" >Finds local messages by `msgID`.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[searchLocalMessages](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a10878d0bd326b07ec6a605c5695c7de1)</td>

<td rowspan="1" colSpan="1" >Search for local messages.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[searchCloudMessages](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#ab672a5d549893b7e22c555593be40322)</td>

<td rowspan="1" colSpan="1" >Search for cloud messages.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[sendMessageReadReceipts](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a375af7e0f3e0f0b3135ccd517de9fdd8)</td>

<td rowspan="1" colSpan="1" >Sends message read receipts.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getMessageReadReceipts](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a69192bc43e551f34f5d483dae5e70410)</td>

<td rowspan="1" colSpan="1" >Gets message read receipts.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupMessageReadMemberList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#aa345a87cfa4da2983f878bb5385d0b82)</td>

<td rowspan="1" colSpan="1" >Gets the list of group members who have read group messages.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setMessageExtensions](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a2e8b8f7ef94d02823cfab0cf5b1e1fea)</td>

<td rowspan="1" colSpan="1" >Sets message extensions.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getMessageExtensions](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a3ae68d2d8aeff6abd21981914836dc1a)</td>

<td rowspan="1" colSpan="1" >Gets message extensions.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteMessageExtensions](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#af3fad5575625e7597a482375d7a65fa6)</td>

<td rowspan="1" colSpan="1" >Deletes message extensions.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addMessageReaction](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a425d818c392bef6c6daeddef8c9c0cc1)</td>

<td rowspan="1" colSpan="1" >Adds message reaction.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeMessageReaction](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a88d3bf59edf75dd06ef9067b08b7db00)</td>

<td rowspan="1" colSpan="1" >Removes message reaction.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getMessageReactions](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#ab3d6d68379e25750ba1b0154d956e62c)</td>

<td rowspan="1" colSpan="1" >Gets message reactions.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getAllUserListOfMessageReaction](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#af26823c8deb12d0b0c5dc885431da182)</td>

<td rowspan="1" colSpan="1" >Gets all user list of message reaction.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[translateText](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#aee0c1e26b0401576ee82967698da35f6)</td>

<td rowspan="1" colSpan="1" >Translates a text message.</td>
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
<td rowspan="1" colSpan="1" >[setGroupListener](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a74de68e55d787fd1d4ec83b99cd1fcab)</td>

<td rowspan="1" colSpan="1" >Sets an event listener for groups. (This API is to be disused. Please use the `addGroupListener` and `removeGroupListener` APIs.)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addGroupListener](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#af583b113cdec570b08ae80d682fba52c)</td>

<td rowspan="1" colSpan="1" >Adds an event listener for groups.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeGroupListener](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a2b2093489bf869f70c03be39f4ed08a1)</td>

<td rowspan="1" colSpan="1" >Removes an event listener for groups.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createGroup](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a3bbcf819c1ec70e520b7f9a42cfbb989)</td>

<td rowspan="1" colSpan="1" >(Simple API) Creates a group.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createGroup](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a59824434b6096180b94d8152183dcd2c)</td>

<td rowspan="1" colSpan="1" >(Advanced API) Creates a group. The group information and the initial group members can be set during group creation.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[joinGroup](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a4762156b7a98489eb4715de53028e12a)</td>

<td rowspan="1" colSpan="1" >Joins a group</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[quitGroup](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#ac2a43b3ada447131df0c5f19e8079be5)</td>

<td rowspan="1" colSpan="1" >Leaves a group.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[dismissGroup](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a5bd55cb04867985253949d8cc78f860e)</td>

<td rowspan="1" colSpan="1" >Disbands a group. Only the group owner and group admin can disband a group.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getJoinedGroupList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a4599e99791c150cc9f3e2492e8b4ce04)</td>

<td rowspan="1" colSpan="1" >Gets the list of groups the current user has joined, excluding audio-video groups.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupsInfo](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a9bca7e5318cfed44335566a783a6b568)</td>

<td rowspan="1" colSpan="1" >Pulls the profiles of groups</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[searchGroups](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#ac9a960921e512621340159d82a4b5259)</td>

<td rowspan="1" colSpan="1" >Search for local group profiles</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[searchCloudGroups](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a8c3f83c844be3c8bb13fe9cec6fd658a)</td>

<td rowspan="1" colSpan="1" >Search for cloud group profiles</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGroupInfo](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#aa9519a479493e56d7920e40aba796144)</td>

<td rowspan="1" colSpan="1" >Modifies the profile of a group</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[initGroupAttributes](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a1b3a56dfc345f1ef2a575cb36156e745)</td>

<td rowspan="1" colSpan="1" >Initializes group attributes.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGroupAttributes](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a134342ddb51d1ee83f3981ed91d26885)</td>

<td rowspan="1" colSpan="1" >Sets group attributes.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteGroupAttributes](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#aa504ffca9492580ca27a45f78a87e2cb)</td>

<td rowspan="1" colSpan="1" >Deletes group attributes.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupAttributes](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#ac8a74db230669d1b49da47bb0895cbf9)</td>

<td rowspan="1" colSpan="1" >Gets group attributes.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupOnlineMemberCount](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#ada2eadb44f6865e9848df94fb5bae4ae)</td>

<td rowspan="1" colSpan="1" >Gets the number of online group members.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupMemberList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a98681b9036e73acbe8f84737b5291326)</td>

<td rowspan="1" colSpan="1" >Gets the group member list</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupMembersInfo](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a1ab284b80811bcc697d689d7b97edf04)</td>

<td rowspan="1" colSpan="1" >Gets the profiles of specified group members</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[searchGroupMembers](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a35ceb734976c833047cceb8b31055b18)</td>

<td rowspan="1" colSpan="1" >Search for local group members</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[searchCloudGroupMembers](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#ae2f92bf458c5b6ef0149d66de7a01896)</td>

<td rowspan="1" colSpan="1" >Search for cloud group members</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGroupMemberInfo](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a40b97ee4b138f93e1b2073d1bdff3756)</td>

<td rowspan="1" colSpan="1" >Modifies the profile of a specified group member</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[muteGroupMember](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#aa8a0206f75d75400b517f7e0d80fe9ee)</td>

<td rowspan="1" colSpan="1" >Mutes a group member.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[inviteUserToGroup](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a942d75fdea66e22cdbd8c131cf18e1ea)</td>

<td rowspan="1" colSpan="1" >Invites users to a group</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[kickGroupMember](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a0581f28fddf2ade890aa62e4318d7a97)</td>

<td rowspan="1" colSpan="1" >Removes a member from a group.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGroupMemberRole](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a0f1c341a3dc53d6a6557a438b0c64b65)</td>

<td rowspan="1" colSpan="1" >Sets a role for a group member.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[markGroupMemberList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a21238536e7cb2c3fd086797e7dc1b970)</td>

<td rowspan="1" colSpan="1" >Marks group members.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[transferGroupOwner](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a58a2ffae60505a43984fe21bf0bc1101)</td>

<td rowspan="1" colSpan="1" >Transfers the ownership of a group</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getGroupApplicationList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a29c36ad685159850a30d61a6b9c637e8)</td>

<td rowspan="1" colSpan="1" >Gets the list of applications to join a group</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[acceptGroupApplication](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a51bb9b4f965cb3d01546fef348ac75e4)</td>

<td rowspan="1" colSpan="1" >Accepts an application to join a group</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[refuseGroupApplication](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a46aa78c54986b2c0b7cc0012a3dc94ef)</td>

<td rowspan="1" colSpan="1" >Rejects a request to join a group.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setGroupApplicationRead](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#ade11e93b96206ef851641c42788132d1)</td>

<td rowspan="1" colSpan="1" >Marks the application list as read</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getJoinedCommunityList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a17350dec83b7cd32d308a1f2b2827fdd)</td>

<td rowspan="1" colSpan="1" >Gets the list of community groups the current user has joined.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createTopicInCommunity](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a8cc04d04254867787060cf1cae0fc5b8)</td>

<td rowspan="1" colSpan="1" >Creates a topic.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteTopicFromCommunity](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a31b726136637a58b5bb246eaac41187c)</td>

<td rowspan="1" colSpan="1" >Deletes a topic.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setTopicInfo](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a237e2fa6e16e55143c516c5428a23936)</td>

<td rowspan="1" colSpan="1" >Modifies topic information.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getTopicInfoList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#af93ad10e0e2b21d6ae3c8ec45021b159)</td>

<td rowspan="1" colSpan="1" >Gets the message list.</td>
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
<td rowspan="1" colSpan="1" >[setConversationListener](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a95bac7330779a8a970fc7689e436257f)</td>

<td rowspan="1" colSpan="1" >Sets a conversation listener. (This API is to be disused. Please use the `addConversationListener` and `removeConversationListener` APIs.)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addConversationListener](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a39b4f352f1740171fb56143149201cd9)</td>

<td rowspan="1" colSpan="1" >Adds a conversation listener.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeConversationListener](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#ab9e1627559fb4259228b4e547b192c83)</td>

<td rowspan="1" colSpan="1" >Removes a conversation listener.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getConversationList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#ab1f5e86e270b122cb725266d234d9dd5)</td>

<td rowspan="1" colSpan="1" >Gets the conversation list</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getConversation](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#ad4b7b80fbe0cff25027371b416ede9f9)</td>

<td rowspan="1" colSpan="1" >Gets a specified conversation.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getConversationList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#af94d9d44e90da448a395e6d92b4e512e)</td>

<td rowspan="1" colSpan="1" >Gets multiple conversations.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[ getConversationListByFilter](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#ac1b77eedff7f2f8742a873cf766daec9)</td>

<td rowspan="1" colSpan="1" >Gets the advanced conversation API to specify the conversation type, mark type, and group name.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteConversation](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a142f5289632f29a603937f1d770748c6)</td>

<td rowspan="1" colSpan="1" >Deletes a conversation</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setConversationDraft](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a462cd163c03cdce230ed3647b414382b)</td>

<td rowspan="1" colSpan="1" >Sets a draft for a conversation</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setConversationCustomData](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#af82623b98c07f36767a47c59f5a23927)</td>

<td rowspan="1" colSpan="1" >Sets custom conversation data.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[pinConversation](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a06cefb398f5a327dff4cefe6fb18c5b8)</td>

<td rowspan="1" colSpan="1" >Pins a conversation to the top.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[markConversation](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a77c02a146f774979e1e04d7334cd2d06)</td>

<td rowspan="1" colSpan="1" >Marks a conversation.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getTotalUnreadMessageCount](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#abe76208f616713a09df582a6c1665d38)</td>

<td rowspan="1" colSpan="1" >Gets the total unread message count.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[ createConversationGroup](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a2f5f4587c881aa26fbdce3b4d469aa0a)</td>

<td rowspan="1" colSpan="1" >Creates a conversation group.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[ getConversationGroupList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a037b0973be9feef207a64f2e043792ab)</td>

<td rowspan="1" colSpan="1" >Gets the list of conversation groups.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[ deleteConversationGroup](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#aa7b91ded9e451335bc931525839ce736)</td>

<td rowspan="1" colSpan="1" >Deletes a conversation group.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[ renameConversationGroup](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a1a9492196c94450b2992079cffab96a6)</td>

<td rowspan="1" colSpan="1" >Renames a conversation group.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[ addConversationsToGroup](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a37c78d27216882504d2710a066478db5)</td>

<td rowspan="1" colSpan="1" >Adds a conversation to a conversation group.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[ deleteConversationsFromGroup](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Conversation_08.html#a16ee46fa4b7278a0386be9ff633fa552)</td>

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
<td rowspan="1" colSpan="1" >[getUsersInfo](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#ac638c1dd6ec1e5204637e4b87129cd38)</td>

<td rowspan="1" colSpan="1" >Gets users’ profiles</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setSelfInfo](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a328a0d2d07e8d34e12effb73937c3437)</td>

<td rowspan="1" colSpan="1" >Modifies one’s own user profile</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getUserStatus](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#abe44a4c51c686248d483674d77d71053)</td>

<td rowspan="1" colSpan="1" >Queries a user's status.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setSelfStatus](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a7d771431a61635888bdc4def438c4328)</td>

<td rowspan="1" colSpan="1" >Sets one's own status.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[subscribeUserStatus](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a20e6cbe409549e0d2ff62be76914e0b3)</td>

<td rowspan="1" colSpan="1" >Subscribes to a user's status.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[unsubscribeUserStatus](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a3780734bb50398ebe65155c3223542f0)</td>

<td rowspan="1" colSpan="1" >Unsubscribes from a user's status.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[searchUsers](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a978df4d80011f4da38dc80f8ab217f48)</td>

<td rowspan="1" colSpan="1" >Search cloud users</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addToBlackList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a67d998da5085b5004bb6aa8d4322022c)</td>

<td rowspan="1" colSpan="1" >Blocks messages from a specified user, which means adding the user to the blocklist.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteFromBlackList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#aa7e69a67185eaca658ba429cf6309a5f)</td>

<td rowspan="1" colSpan="1" >Unblocks messages from a specified user, which means removing the user from the blocklist.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getBlackList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a0d854d64c8ae936014a8424d55508fa3)</td>

<td rowspan="1" colSpan="1" >Gets the blocklist</td>
</tr>
</table>


## Offline Push APIs

Use the offline push service if you want your app to receive Chat service messages in real time when it is in the background.
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setAPNSListener](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07APNS_08.html#a62e1694cf9e1d65b76f90064cbcbb683)</td>

<td rowspan="1" colSpan="1" >Sets an APNs listener.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setAPNS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07APNS_08.html#a73bf19c0c019e5e27ec441bc753daa9e)</td>

<td rowspan="1" colSpan="1" >Configures APNs Push info.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setVOIP](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07VOIP_08.html#a0bd652eed597771ca1381d0d6ea67704)</td>

<td rowspan="1" colSpan="1" >Configures VoIP Push info.</td>
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
<td rowspan="1" colSpan="1" >[setFriendListener](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#acd403f586f3df84f56b1b757efb2d443)</td>

<td rowspan="1" colSpan="1" >Sets a contacts and friend profile listener. (This API is to be disused. Please use the `addFriendListener` and `removeFriendListener` APIs.)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addFriendListener](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a1de011b63b3c20b1be519dc7ba124704)</td>

<td rowspan="1" colSpan="1" >Adds a contacts listener.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[removeFriendListener](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#aed40ccbbc4e15be79154077a6d3ec085)</td>

<td rowspan="1" colSpan="1" >Removes a contacts listener.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getFriendList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a81131d76924a03ec2b593addd6e4e101)</td>

<td rowspan="1" colSpan="1" >Gets the contacts.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getFriendsInfo](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a39f6752da11b595e4a5b6dcb0eb6a584)</td>

<td rowspan="1" colSpan="1" >Gets the profiles of specified friends</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setFriendInfo](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#ac258312c000c1af69fcf51dd6898b74b)</td>

<td rowspan="1" colSpan="1" >Sets the profile of a specified friend</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[searchFriends](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a9a036dcc1bd65474a3d2e90f2bb6b9c6)</td>

<td rowspan="1" colSpan="1" >Searches for friends.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addFriend](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#ac1ea1c7de2bfc2b0a25e5f6b3192e304)</td>

<td rowspan="1" colSpan="1" >Adds a friend</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteFromFriendList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#af967134fb177b32d4060fedf3663ace3)</td>

<td rowspan="1" colSpan="1" >Deletes a friend</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[checkFriend](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#aad1b09fab6523d9a36147b4ed4efac67)</td>

<td rowspan="1" colSpan="1" >Checks relationship with specified users.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getFriendApplicationList](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#acda7968f1e9adc12261a7e533d709a1c)</td>

<td rowspan="1" colSpan="1" >Gets the list of friend requests</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[acceptFriendApplication](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a51b913927028025e2e450e6e8ce848c0)</td>

<td rowspan="1" colSpan="1" >Accepts a friend request</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[refuseFriendApplication](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a406b964a6513219cfe4803f87f0f00f8)</td>

<td rowspan="1" colSpan="1" >Rejects a friend request</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteFriendApplication](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a363e0622f653694999293c595d552896)</td>

<td rowspan="1" colSpan="1" >Deletes a friend request</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setFriendApplicationRead](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#ad46c70c18b8f69bf272cbf3466477a85)</td>

<td rowspan="1" colSpan="1" >Marks a friend request as read.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[createFriendGroup](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a8b33edab15ae7d179e4e2d885e7d2b7d)</td>

<td rowspan="1" colSpan="1" >Creates a friend list</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getFriendGroups](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a63f3eaae567586077d5a8d27c31e2229)</td>

<td rowspan="1" colSpan="1" >Gets the information of friend lists</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteFriendGroup](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a2dc49f2abb1238fc2d47ce6d4f14c1e7)</td>

<td rowspan="1" colSpan="1" >Deletes friend lists</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[renameFriendGroup](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a93f6ba132d9706db7c74daff97a2abd0)</td>

<td rowspan="1" colSpan="1" >Modifies the name of a friend list</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[addFriendsToFriendGroup](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a0265241c39600c390406ca1f8f6ff75d)</td>

<td rowspan="1" colSpan="1" >Adds friends to a friend list</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[deleteFriendsFromFriendGroup](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Friendship_08.html#a4a14a878816c8d6a20981d1903fcf359)</td>

<td rowspan="1" colSpan="1" >Removes friends from a friend list.</td>
</tr>
</table>
