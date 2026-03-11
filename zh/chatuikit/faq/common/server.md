> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

---
product: 'Chat'
tech_stack: 'server'
framework: 'common'
title: '通用问题知识库'
keywords: ['控制台', '服务端生成 usersig', 'restapi', '前回调', '后回调', 'nodejs/go/java/python 等服务端语言生成 userSig 示例代码 ']
---

# 通用问题知识库

## userSig 解决方案

### Q: 服务端如何生成 userSig ?
**A：** 服务端生成 userSig 的具体方式可参考： https://cloud.tencent.com/document/product/269/32688， 文档中提供了多种服务端语言的解决方案。

### Q: Chat 消息发送前回调和发送后回调的消息格式区别，如何区分系统消息和用户消息?
**A：** 
1. 群消息发言前回调内容没有 MsgSeq、MsgTime 等信息，具体的可以参考以下文档：
- 单聊发言前回调：https://cloud.tencent.com/document/product/269/1632
- 单聊发言后回调：https://cloud.tencent.com/document/product/269/2716
- 群内发言前回调：https://cloud.tencent.com/document/product/269/1619
- 群内发言后回调：https://cloud.tencent.com/document/product/269/2661
2. 普通消息格式： https://cloud.tencent.com/document/product/269/2720

### Q: 群消息优先级和群消息频控是怎样的？
**A：** 群消息分为 3 个优先级（`High`,`Normal`,`Low`），如果某个群的消息超过了频率限制，后台会优先下发高优先级的消息。因此用户应根据消息的重要程度，来选择合适的优先级。总消息数频控是指单个群所有端接口累计每秒最多能发送的消息数限制，默认值为 40条/秒，采用每秒平均限频。消息数量超过限制后，后台优先下发优先级相对较高的消息，同等优先级的消息随机排序。详细内容可以参考文档：https://cloud.tencent.com/document/product/269/3663

### Q: 有腾讯云图片消息内容安全审核的的最佳实践和使用方案吗？
**A：** 云端审核功能，是一款在云端（服务端）进行内容智能识别和拦截的服务：
- 支持对文本、图片内容同步审核，对音频、视频内容异步审核。
- 支持分别针对单聊、群聊、资料三大 IM 场景中产生的不同类型 UGC 内容进行策略配置。
- 支持配置特定终端用户产生/接收的消息不送审，支持对返回审核结果进行配置。
- 支持自助创建自定义审核场景，对非 IM 场景的 UGC 内容或者终端消息有更灵活的送审选择。
- 支持查看审核用量抵扣明细、审核结果明细，提供审核条数统计、审核类型统计、审核用户统计、违规用户排行等可视化数据。
参考文档：https://cloud.tencent.com/document/product/269/79139

### Q: 如何拦截用户发送的消息？
**A：** 业务服务端可以通过消息前回调进行拦截，具体文档可参考：
- 单聊发言前回调：https://cloud.tencent.com/document/product/269/1632
- 群内发言前回调：https://cloud.tencent.com/document/product/269/1619

### Q: 如何删除和管理账号？
**A：** restapi 可以对账号进行删除、导入、查询，具体文档可参考：
- 删除账号：https://cloud.tencent.com/document/product/269/36443
- 导入单个账号：https://cloud.tencent.com/document/product/269/1608
- 导入多个账号：https://cloud.tencent.com/document/product/269/4919
- 查询账号：https://cloud.tencent.com/document/product/269/38417

### Q: 账号数量超过限制如何处理？
**A：** 导入账号时，如果账号数超限，如需创建多于100个账号，需要将应用升级为专业版，具体操作指引请参见：https://cloud.tencent.com/document/product/269/32458。

### Q: 服务端如何删除会话？
**A：** 服务端删除会话可以使用 restapi, 具体文档可参考：https://cloud.tencent.com/document/product/269/62119。

