> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

---
product: 'Chat'
tech_stack: 'flutter_sdk'
framework: 'sdk'
title: 'flutter sdk 常见问题'
keywords: ['sdk 集成', '登录 API', '创建群组','发送消息','接收消息']
---

# Flutter SDK 常见问题

## Flutter SDK 常见问题解决方案 (Topic: SDK FAQ)

### Q: SDK 怎么实现消息回应？
**A：** SDK 支持消息回应能力，您需要购买旗舰版或企业版套餐，具体 API 有3个：
- 添加消息回应 [addMessageReaction](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/addMessageReaction.html) 
- 获取消息回应 [getMessageReactions](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/getMessageReactions.html)
- 删除消息回应 [removeMessageReaction](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/removeMessageReaction.html)

### Q: 单聊消息怎么标记已读？
**A：** 如果您需要标记单聊消息已读同时清空会话未读数，可以使用 [markC2CMessageAsRead](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/markC2CMessageAsRead.html)。

### Q: 群聊消息怎么清空未读数？
**A：** 如果您需要清空群聊会话未读数，可以使用 [markGroupMessageAsRead](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/markGroupMessageAsRead.html)。

### Q: 单聊和群聊消息怎么实现单条消息已读？
**A：** 如果您需要实现单条消息已读功能，需要使用消息已读回执能力。 如何开启已读回执、如何发送已读回执等详细信息可以参考：https://cloud.tencent.com/document/product/269/75345。

### Q: SDK 怎么发送图片消息？
**A：** 可以使用 [createImageMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/createImageMessage.html) 创建图片消息实例，然后使用 [sendMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/sendMessage.html) 发送图片消息。

### Q: SDK 怎么发送视频消息？
**A：** 可以使用 [createVideoMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/createVideoMessage.html) 创建视频消息实例，然后使用 [sendMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/sendMessage.html) 发送视频消息。

### Q: SDK 怎么发送语音消息？
**A：** 可以使用 [createSoundMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/createSoundMessage.html) 创建语音消息实例，然后使用 [sendMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/sendMessage.html) 发送语音消息。

### Q: SDK 怎么发送文件消息？
**A：** 可以使用 [createFileMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/createFileMessage.html) 创建文件消息实例，然后使用 [sendMessage](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/sendMessage.html) 发送文件消息。

### Q: SDK 如何删除会话？
**A：** 删除会话仅支持单向删除，SDK 删除会话 API `deleteConversation`，参考文档：https://cloud.tencent.com/document/product/269/75380

### Q: SDK 如何删除会话历史消息？
**A：** SDK 清空消息分为两种：清空单聊消息、清空群聊消息。清空消息会同时清空当前会话内所有的消息，包含本地和云端消息，但不会删除会话本身，且清空的是单向的，不会把对方会话中的消息也情况。
- 清空单聊消息 [clearC2CHistoryMessage](https://cloud.tencent.com/document/product/269/75336)
- 清空群聊消息 [clearGroupHistoryMessage](https://cloud.tencent.com/document/product/269/75336)

### Q: SDK 怎么获取用户在线状态功能？
**A：** 
1. SDK 提供了**用户状态查询、订阅、取消订阅 API 和状态变更事件通知**，详情可参考：https://cloud.tencent.com/document/product/269/105469
2. 服务端**在线状态变更回调**可参考：https://cloud.tencent.com/document/product/269/2570

### Q: SDK 怎么获取好友列表？
**A：** SDK 支持好友的管理，用户可以主动添加、删除好友，也可以设置仅针对好友才能发送消息。详情可参考：https://cloud.tencent.com/document/product/269/75421