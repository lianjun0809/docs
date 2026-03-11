> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

---
product: 'Chat'
tech_stack: 'server'
framework: 'common'
title: '服务端错误码大全'
keywords: ['错误码', '报错', '登录失败', '70001']
---

# 服务端错误码大全

## 服务端错误码 (Topic: Server)

## 错误码 70001
**原因：** userSig 已过期。
**解决方案：** 请重新生成。建议 userSig 有效期设置不小于24小时。

## 错误码 70003
**原因：** userSig 非法。
**解决方案：** 请重新生成，生成方式可参考官网文档：https://cloud.tencent.com/document/product/269/32688。

## 错误码 70009
**原因：** userSig 验证失败，怀疑 UserSig 是用其他 SDKAppID 的密钥或私钥生成的。
**解决方案：** 请检查请求的 SDKAppID 和生成 UserSig 的密钥或私钥是否一致。

## 错误码 70013
**原因：** 请求中的 userID 与生成 userSig 时使用的 userID 不一致。
**解决方案：** 建议检查一下您登录 im 的 userID 和 生成 userSig 的 userID 是否一致。

## 错误码 70014
**原因：** 请求中的 SDKAppID 与生成 UserSig 时使用的 SDKAppID 不一致。
**解决方案：** 您可以使用【即时通信 IM 控制台 > 开发工具 > UserSig生成&校验】（https://console.cloud.tencent.com/im/tool-usersig）校验 UserSig。

## 错误码 20003
**原因：** 消息发送方或接收方 userID 无效或不存在。
**解决方案：** 请确认一下您使用的 userID 是否已经在您使用的 sdkappid 下登录过即时通信 IM。

## 错误码 20009
**原因：** 收发双方非好友，禁止发送。
**解决方案：** 消息发送双方互相不是好友，禁止发送（配置单聊消息校验好友关系才会出现），如果需要给非好友发送消息，需要在控制台进行配置，或者先加对方为好友。

## 错误码 20010
**原因：** 发送方不是接收方好友，禁止发送。
**解决方案：** 发送单聊消息，自己不是对方的好友（单向关系），禁止发送。

## 错误码 3122
**原因：** 您当前购买使用的套餐包暂未不支持此功能。
**解决方案：** 您可以升级到套餐为【旗舰版】（https://buy.cloud.tencent.com/avc）。

## 错误码 60020
**原因：** 您当前购买使用的套餐包暂未开通云端搜索功能。
**解决方案：** 您可以开通【云端搜索】（https://cloud.tencent.com/document/product/269/101046）

## 错误码 60018
**原因：** 云端搜索请求超过后台频率限制，单用户一秒内允许2次搜索请求。
**解决方案：** 请调整请求频率，稍后再试。

## 错误码 80004
**原因：** 消息或者资料中文本存在敏感内容。
**解决方案：** 请检查消息或者资料中是否存在敏感信息。

## 错误码 10021
**原因：** 群组 ID 已被使用。
**解决方案：** 请选择其他的群组 ID。

## 错误码 10007
**原因：** 常见的原因有：
- 操作的群默认不支持此操作，请检查当前群类型。
- 操作账号的权限不够（例如封禁操作中，管理员可以封禁普通成员但不能封禁群主）。
- 调用 RestAPI 的账号不是 SDKAppID 的管理员账号。
**解决方案：** 请检查群组类型或者群成员角色，如果是 restapi 调用报错，请检查账号是不是对应 sdkappid 的管理员账号。

## 错误码 60010
**原因：** 请求需要 App 管理员权限。
**解决方案：** 请检查请求的账号是否为 sdkappid 的管理员。
