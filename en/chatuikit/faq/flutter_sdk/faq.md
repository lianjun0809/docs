> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

---
product: 'Chat'
tech_stack: 'flutter_sdk'
framework: 'sdk'
title: 'Flutter SDK FAQ'
keywords: ['sdk integration', 'login API', 'create group','send message','receive message']
---

# Flutter SDK FAQ

## Flutter SDK FAQ Solutions (Topic: SDK FAQ)

### Q: How to implement message reactions in SDK?
**A:** The SDK supports message reaction capabilities. You need to purchase the Flagship or Enterprise edition package. There are 3 specific APIs:
- Add message reaction [addMessageReaction](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/addMessageReaction.html) 
- Get message reactions [getMessageReactions](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/getMessageReactions.html)
- Remove message reaction [removeMessageReaction](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/removeMessageReaction.html)

### Q: How to mark one-to-one messages as read?
**A:** If you need to mark one-to-one messages as read and clear the conversation unread count, you can use [markC2CMessageAsRead](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/markC2CMessageAsRead.html).

### Q: How to clear unread count for group messages?
**A:** If you need to clear the unread count for group conversations, you can use [markGroupMessageAsRead](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/markGroupMessageAsRead.html).

### Q: How to implement read receipts for individual messages in one-to-one and group chats?
**A:** If you need to implement read receipt functionality for individual messages, you need to use the message read receipt capability. For detailed information on how to enable read receipts and send read receipts, please refer to: https://trtc.io/document/48020?product=chat&menulabel=core%20sdk&platform=flutter.

### Q: How to send image messages in SDK?
**A:** You can use [createImageMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/createImageMessage.html) to create an image message instance, then use [sendMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/sendMessage.html) to send the image message.

### Q: How to send video messages in SDK?
**A:** You can use [createVideoMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/createVideoMessage.html) to create a video message instance, then use [sendMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/sendMessage.html) to send the video message.

### Q: How to send voice messages in SDK?
**A:** You can use [createSoundMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/createSoundMessage.html) to create a voice message instance, then use [sendMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/sendMessage.html) to send the voice message.

### Q: How to send file messages in SDK?
**A:** You can use [createFileMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/createFileMessage.html) to create a file message instance, then use [sendMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/sendMessage.html) to send the file message.

### Q: How to delete a conversation in SDK?
**A:** Deleting a conversation only supports one-way deletion. The SDK delete conversation API is `deleteConversation`, refer to documentation: https://trtc.io/document/48312?product=chat&menulabel=core%20sdk&platform=flutter

### Q: How to delete conversation history messages in SDK?
**A:** The SDK supports two types of message clearing: clearing one-to-one chat messages and clearing group chat messages. Clearing messages will clear all messages in the current conversation, including both local and cloud messages, but will not delete the conversation itself. The clearing is one-way and will not clear messages in the other party's conversation.
- Clear one-to-one chat messages [clearC2CHistoryMessage](https://trtc.io/document/48012?product=chat&menulabel=core%20sdk&platform=flutter)
- Clear group chat messages [clearGroupHistoryMessage](https://trtc.io/document/48012?product=chat&menulabel=core%20sdk&platform=flutter)

### Q: How to get user online status in SDK?
**A:** 
1. Server-side **online status change callback** can be found at: https://trtc.io/document/34357?product=chat&menulabel=core%20sdk&platform=flutter

### Q: How to get friends list in SDK?
**A:** The SDK supports friend management. Users can actively add or delete friends, and can also set to only allow messages from friends. For details, please refer to: https://trtc.io/document/48154?product=chat&menulabel=core%20sdk&platform=flutter