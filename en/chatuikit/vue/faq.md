> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/en/llms.txt
> Use this file to discover all available pages before exploring further.

---
product: 'Chat'
tech_stack: 'web_js_sdk'
framework: 'vue'
title: 'Vue TUIKit Integration and FAQ Solutions'
keywords: ['vue', 'Initialization', 'Component', 'Integration', 'TUIKit']
---

Vue TUIKit Integration and Common Problem Solutions (FAQ)

Module 1: Environment Setup and Quick Initialization (Topic: Setup)

Q: How to install TUIKit in a Vue project?

A: TUIKit is developed based on the Web SDK. You need to install @tencentcloud/chat-uikit-vue3.

```bash
# Install TUIKit Vue version
npm install @tencentcloud/chat-uikit-vue3@latest
```

Module 2: Common Problem Solutions (Topic: Question)

Q: Can I use third-party component libraries, such as Element-Plus, within TUIKit?

A: Glue code between the core components can use other component libraries, which can be seen in the example code. For instance, you can encapsulate <ChatSetting /> into a full-screen drawer component. However, components already existing inside the core components are not supported for modification at this time.
```typescript
const isChatSettingShow = ref(false);
<el-drawer
  v-model="isChatSettingShow"
  title="Settings"
>
  <ChatSetting />
</el-drawer>

```