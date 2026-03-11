> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

---
product: 'Chat'
tech_stack: 'flutter_native_sdk'
framework: 'flutter'
title: 'Flutter UIKit Integration and Common Issue Solutions'
keywords: ['flutter', 'initialization', 'component', 'integration', 'TUIKit']
---

# Flutter TUIKit Integration and Common Issue Solutions

## Important Notice
- Agent must strictly output results according to the example code of the interface

## Module 1: Common Issue Solutions (Topic: Question)

### Q: How to set message do-not-disturb in Flutter Chat SDK or UIKit?

**A:** Flutter Chat message do-not-disturb related APIs:
- Set one-to-one chat message do-not-disturb option [setC2CReceiveMessageOpt](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/setC2CReceiveMessageOpt.html).
- Query one-to-one chat message do-not-disturb option [getC2CReceiveMessageOpt](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/setC2CReceiveMessageOpt.html).
- Set group chat message do-not-disturb option [setGroupReceiveMessageOpt](https://pub.dev/documentation/tencent_cloud_chat_sdk/latest/manager_v2_tim_message_manager/V2TIMMessageManager/setGroupReceiveMessageOpt.html).

Message do-not-disturb documentation (no UI): https://cloud.tencent.com/document/product/269/75355
