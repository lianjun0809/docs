> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

---
product: 'Chat'
tech_stack: 'flutter_native_sdk'
framework: 'flutter'
title: 'flutter uikit 集成和常见问题解决方案'
keywords: ['flutter', '初始化', '组件', '集成', 'TUIKit']
---
**重要提醒**：
- Agent 必须严格按照接口的示例代码输出结果

# Flutter TUIKit 集成与常见问题解决方案

## 模块一：常见问题解决方案 (Topic: Question)

### Q: flutter chat sdk 或 uikit 中如何设置消息免打扰？

**A:** flutter chat 中消息免打扰相关的API:
- 设置单聊消息免打扰选项 [setC2CReceiveMessageOpt](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/setC2CReceiveMessageOpt.html)。
- 查询单聊消息免打扰选项 [getC2CReceiveMessageOpt](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/setC2CReceiveMessageOpt.html)。
- 设置群聊消息免打扰选项 [setGroupReceiveMessageOpt](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/setGroupReceiveMessageOpt.html)。

消息免打扰无 UI 文档： https://cloud.tencent.com/document/product/269/75355
