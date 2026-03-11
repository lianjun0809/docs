> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

## 组件概述

ChatSetting 是一个智能的聊天设置组件，它能够根据当前激活的会话类型自动渲染相应的设置界面。该组件内部集成了 C2C（1 对 1）聊天设置和群聊设置两种模式，为用户提供了统一的聊天设置入口。

组件的核心特点：
- **自动适配**：根据会话类型（分为单聊和群聊）自动切换设置界面。

- **状态驱动**：基于当前激活会话状态自动更新内容。
   

   > **注意：**
   > 

   > 如果当前没有激活的会话则不会显示。
   > 


## 快速使用

ChatSetting 是一个可自由使用的独立组件，为了组件使用的灵活度，UIKit 并没有提供默认的使用方式。

推荐的用法是：结合 ChatHeader 组件的 `ChatHeaderRight` 插槽，来控制 `ChatSetting` 的显示。以下是示例代码：
``` typescript
<template>
  <UIKitProvider>
    <Chat>
      <ChatHeader>
        <template #ChatHeaderRight>
          <button @click="toggleChatSetting">
            ⚙️ 设置
          </button>
        </template>
      </ChatHeader>
      <MessageList />
      <MessageInput />
    </Chat>
    <Drawer 
      :open="isSettingVisible"
      title="聊天设置"
    >
      <ChatSetting />
    </Drawer>
  </UIKitProvider>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { ChatHeader } from '@tencentcloud/chat-uikit-vue3';
// 假设您有一个 Drawer 组件
import { Drawer } from 'your-ui-library';

const isSettingVisible = ref(false);

const toggleChatSetting = () => {
  isSettingVisible.value = !isSettingVisible.value;
};
</script>
```

## 相关文档
- [自定义组件 - UIKitProvider](https://write.woa.com/document/187032638782849024)

- [自定义组件 - ConversationList](https://write.woa.com/document/186960319111872512)

- [自定义组件 - Chat](https://write.woa.com/document/187778215983329280)

- [自定义组件 - MessageInput](https://write.woa.com/document/187058763983568896)

- [自定义组件 - MessageList](https://write.woa.com/document/187036342928752640)

- [自定义组件 - ChatSetting](https://write.woa.com/document/187321409859108864)

- [自定义组件 - C2CSetting State](https://write.woa.com/document/187323861368082432)

- [自定义组件 - GroupSetting State](https://write.woa.com/document/187684794845769728)

- [自定义组件 - ContactList](https://write.woa.com/document/187595466274463744)

- [自定义组件 - Search](https://write.woa.com/document/187595449195040768)

- [chat-uikit-vue3 npm](https://www.npmjs.com/package/@tencentcloud/chat-uikit-vue3)

- [GitHub Demo](https://github.com/Tencent-RTC/TUIKit_Vue3/tree/main/demos/rtcube-vite-vue3)


## 交流与反馈

如遇任何问题，可联系 [官网售后](https://cloud.tencent.com/act/event/connect-service#/) 反馈，享有专业工程师的支持，解决您的难题。
