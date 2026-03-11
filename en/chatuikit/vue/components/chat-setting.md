> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/en/llms.txt
> Use this file to discover all available pages before exploring further.

## Component Overview

ChatSetting is an intelligent chat settings component that automatically renders the appropriate settings interface based on the currently active conversation type. The component internally integrates two modes: C2C (1-to-1) chat settings and group chat settings, providing users with a unified chat settings entry point.

Core features of the component:
- **Auto-adaptive**: Automatically switches the settings interface based on conversation type (C2C or group chat).

- **State-driven**: Automatically updates content based on the currently active conversation state.
   

   > **Note:**
   > 

   > Will not be displayed if there is no active conversation.
   > 


## Quick Start

ChatSetting is a standalone component that can be used freely. For flexibility in component usage, UIKit does not provide a default usage pattern.

The recommended approach is to use the `ChatHeaderRight` slot of the ChatHeader component to control the display of `ChatSetting`. Here's the sample code:
``` typescript
<template>
  <UIKitProvider>
    <Chat>
      <ChatHeader>
        <template #ChatHeaderRight>
          <button @click="toggleChatSetting">
            ⚙️ Settings
          </button>
        </template>
      </ChatHeader>
      <MessageList />
      <MessageInput />
    </Chat>
    <Drawer 
      :open="isSettingVisible"
      title="Chat Settings"
    >
      <ChatSetting />
    </Drawer>
  </UIKitProvider>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { ChatHeader } from '@tencentcloud/chat-uikit-vue3';
// Assuming you have a Drawer component
import { Drawer } from 'your-ui-library';

const isSettingVisible = ref(false);

const toggleChatSetting = () => {
  isSettingVisible.value = !isSettingVisible.value;
};
</script>
```

## Related Documentation

- [chat-uikit-vue3 npm](https://www.npmjs.com/package/@tencentcloud/chat-uikit-vue3)

- [GitHub Demo](https://github.com/Tencent-RTC/TUIKit_Vue3/tree/main/demos/rtcube-vite-vue3)
