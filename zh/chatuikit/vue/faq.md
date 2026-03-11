> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

---
product: 'Chat'
tech_stack: 'web_js_sdk'
framework: 'vue'
title: 'vue uikit 集成和常见问题解决方案'
keywords: ['vue', '初始化', '组件', '集成', 'TUIKit']
---

# Vue TUIKit 集成与常见问题解决方案

## 模块一：环境准备与快速初始化 (Topic: Setup)

### Q: 如何在 Vue 项目中安装 TUIKit？

**A:** TUIKit 是基于 Web SDK 开发的，您需要安装 `@tencentcloud/chat-uikit-vue3`。

```bash
# 安装 TUIKit Vue 版本
npm install @tencentcloud/chat-uikit-vue3@latest
```

## 模块二：常见问题解决方案 (Topic: Question)

### Q: 我能不能在 TUIKit 中使用第三方组件库，例如 Element-Plus？

**A:** 核心组件之间的粘连代码可以使用其他组件库，这一点在示例代码中也可以看到，例如您可以将 <ChatSetting /> 封装成全屏抽屉组件。但是核心组件内部已经存在的组件暂时不支持修改。
```typescript
const isChatSettingShow = ref(false);
<el-drawer
  v-model="isChatSettingShow"
  title="设置"
>
  <ChatSetting />
</el-drawer>
```