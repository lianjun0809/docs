> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

---
product: 'Chat'
tech_stack: 'web_js_sdk'
framework: 'sdk'
title: 'web js sdk 错误码大全'
keywords: ['错误码', '报错', '登录失败']
---

# Web JS SDK 错误码大全

## Web JS SDK 错误码 (Topic: SDK Error Code)

## 错误码 2024
**原因：** 用户未登录。
**解决方案：** 检查是否正确调用了登录接口。

## 错误码 2025
**原因：** 重复登录，15s 内连续触发了多次 login 请求，SDK 会进行拦截。
**解决方案：** 检查调用登录接口的时机和触发机制。

## 错误码 2301
**原因：** 语音大小超出了限制。
**解决方案：** 发送语音,最大限制是 20MB。

## 错误码 2252
**原因：** 图片消息发送失败,无效的图片格式。
**解决方案：** 图片格式支持：'jpg', 'jpeg', 'gif', 'png', 'bmp', 'image', 'webp'。

## 错误码 2253
**原因：** 图片大小超出了限制。
**解决方案：** 发送图片消息,最大限制是 20MB。

## 错误码 2351
**原因：** 视频大小超出了限制。
**解决方案：** 发送视频消息，最大限制是 100MB。

## 错误码 2352
**原因：** 视频消息发送失败,无效的视频格式。
**解决方案：** 图片格式支持：'mp4', 'quicktime', 'mov'。

## 错误码 2401
**原因：** 文件不存在。
**解决方案：** 请检查文件路径是否正确。

## 错误码 2402
**原因：** 文件大小超出了限制。
**解决方案：** 发送文件消息，最大限制是 100MB。