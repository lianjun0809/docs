> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

# Vue Chat TUIKit Integration Guide

TUIKit is a Vue3 UI component library built on top of Tencent Cloud Chat SDK. It provides common UI components for instant messaging features including conversations, chat, groups, and more. This guide explains how to quickly integrate TUIKit and implement core functionality.

> **Note:**
> 
> Hello! We are developing an instant messaging product called UIKit, based on Tencent Cloud Chat SDK. It is a Vue 3 UI component library that helps you quickly integrate and implement core instant messaging features.
> 

## Key Concepts

The `chat-uikit-vue3` library consists of core UI components including ConversationList, Chat, MessageList, ChatHeader, MessageInput, ChatSetting, Search, and Contact. Each component is responsible for displaying different content:

1. **ConversationList** - Provides the conversation list component.
2. **Chat** - Provides the container component for conversations.
3. **MessageList** - Provides the message list component for conversations.
4. **ChatHeader** - Provides the header information component for conversations.
5. **MessageInput** - Provides the input box component.
6. **ChatSetting** - Provides management components for one-on-one and group chats.
7. **Search** - Provides cloud-based search component.
8. **Contact** - Provides contacts component.

## Prerequisites

- Vue.js@^3.0.0
- TypeScript@^5.0.0
- Node.js (Node.js ≥ 20.0.0, LTS v22 recommended)

## Create Project

Create a new Vue 3 project named **chat-example** using Vite.

> **Note:**
> 
> Higher versions of Vite require the latest Node.js version.
> 

**[shell]**
```bash
npm create vite@latest
```

## Download and Import Components

After creating the project, navigate to the project directory.

**[shell]**
```bash
cd chat-example
npm install
```

### Step 1: Install Dependencies

**[shell]**
```bash
npm i @tencentcloud/chat-uikit-vue3
```

### Step 2: Import Components

#### 2.1 Build the Main Interface

For example, add the following code to `src/App.vue`:

```typescript
<template>
  <UIKitProvider language="en-US" theme="light">
    <div class="chat-layout">
      <!-- Left Navigation -->
      <SideTab :active-tab="activeTab" @tab-change="handleTabChange" />
      
      <!-- Middle List Panel -->
      <div class="conversation-list-panel">
        <ConversationList v-show="activeTab === 'conversations'" />
        <ContactList v-show="activeTab === 'contacts'" />
      </div>
      
      <!-- Right Chat Panel -->
      <Chat 
        v-show="activeTab === 'conversations'" 
        class="chat-content-panel" 
        :PlaceholderEmpty="EmptyChatTpl"
      >
        <ChatHeader>
          <template #ChatHeaderRight>
            <button class="icon-button" @click="isChatSettingShow = !isChatSettingShow">
              <IconMenu size="20" />
            </button>
          </template>
        </ChatHeader>
        <MessageList />
        <MessageInput class="message-input-container">
          <template #headerToolbar>
            <div class="message-toolbar">
              <div class="message-toolbar-actions">
                <EmojiPicker />
                <FilePicker />
                <VideoPicker />
                <ImagePicker />
                <!-- Refer to documentation to enable audio/video call services -->
                <!-- <AudioCallPicker />
                <VideoCallPicker /> -->
              </div>
              <button class="icon-button" @click="isSearchInChatShow = !isSearchInChatShow">
                <IconSearch size="20" />
              </button>
            </div>
          </template>
        </MessageInput>

        <!-- Chat Settings Sidebar -->
        <div v-show="isChatSettingShow" class="chat-sidebar" :class="{ dark: theme === 'dark' }">
          <div class="chat-sidebar-header">
            <span class="chat-sidebar-title">Settings</span>
            <button class="icon-button" @click="isChatSettingShow = false">✕</button>
          </div>
          <ChatSetting />
        </div>

        <!-- In-Chat Search Sidebar -->
        <div v-show="isSearchInChatShow" class="chat-sidebar" :class="{ dark: theme === 'dark' }">
          <div class="chat-sidebar-header">
            <span class="chat-sidebar-title">Group Search</span>
            <button class="icon-button" @click="isSearchInChatShow = false">✕</button>
          </div>
          <Search :variant="VariantType.EMBEDDED" />
        </div>
      </Chat>

      <!-- Contact Details -->
      <ContactInfo
        v-show="activeTab === 'contacts'" 
        class="contact-detail-panel" 
        @send-message="handleSendMessage" 
      />
    </div>
  </UIKitProvider>
</template>

<script setup lang="ts">
import { ref, h, watch } from 'vue';
import {
  Chat, Search, ChatHeader, MessageList, MessageInput, ContactList, ContactInfo, ChatSetting, UIKitProvider, ConversationList, useUIKit, useLoginState, useConversationListState, EmojiPicker, FilePicker, VideoPicker, ImagePicker, VariantType, AudioCallPicker, VideoCallPicker,
} from '@tencentcloud/chat-uikit-vue3';
import { IconMenu, IconSearch, TUIToast } from '@tencentcloud/uikit-base-component-vue3';
import SideTab from './components/SideTab.vue';

const { theme } = useUIKit();
const { login } = useLoginState();
const { setActiveConversation, activeConversation } = useConversationListState();

const activeTab = ref<'conversations' | 'contacts'>('conversations');
const isChatSettingShow = ref(false);
const isSearchInChatShow = ref(false);

// Close in-chat sidebars when switching conversations
watch(() => activeConversation.value?.conversationID, (newVal, oldVal) => {
  if (newVal !== oldVal) {
    isChatSettingShow.value = false;
    isSearchInChatShow.value = false;
  }
});

// Login
login({
  sdkAppId: 0, // SDKAppID, number type
  userId: '',  // UserID, string type
  userSig: '', // userSig, string type
})
.then(() => {
  const userID = 'administrator';
  const conversationID = `C2C${userID}`;
  setActiveConversation(conversationID);
})
.catch((err) => {
  TUIToast.error({
    message: err.message,
    duration: 5000,
  });
});

const handleTabChange = (tab: 'conversations' | 'contacts') => {
  activeTab.value = tab;
};

const handleSendMessage = () => {
  activeTab.value = 'conversations';
};

// Empty conversation placeholder component
const EmptyChatTpl = h('div', { class: 'empty-placeholder' }, [
  h('div', { class: 'empty-icon' }, '💬'),
  h('div', { class: 'empty-title' }, 'No conversation'),
  h('div', { class: 'empty-subtitle' }, 'Select a conversation to start chatting'),
]);
</script>

<style scoped>
.chat-layout{width:calc(100vw - 64px);height:calc(100vh - 64px);max-width:1600px;max-height:900px;display:flex;border-radius:16px;box-shadow:0 20px 60px rgba(0,0,0,0.3),0 0 0 1px rgba(255,255,255,0.1);overflow:hidden;backdrop-filter:blur(10px);}.conversation-list-panel{width:300px;display:flex;flex-direction:column;border-right:1px solid var(--stroke-color-primary);overflow:hidden;}.chat-content-panel{flex:1;}.contact-detail-panel{flex:1;}.icon-button{padding:4px 6px;display:flex;align-items:center;justify-content:center;border:none;background:transparent;border-radius:4px;font-size:20px;color:var(--text-color-primary);cursor:pointer;transition:background-color 0.2s;outline:none;}.icon-button:focus{outline:none;}.icon-button:hover{background-color:var(--button-color-secondary-hover);}.icon-button:active{background-color:var(--button-color-secondary-active);}.message-toolbar{display:flex;justify-content:space-between;align-items:center;}.message-toolbar-actions{display:flex;align-items:center;gap:4px;}.chat-sidebar{position:absolute;right:0;top:0;bottom:0;min-width:300px;max-width:400px;display:flex;flex-direction:column;background-color:var(--bg-color-operate);box-shadow:var(--shadow-color) 0 0 10px;overflow:auto;z-index:1000;}.chat-sidebar.dark{box-shadow:-4px 0 16px rgba(0,0,0,0.4),-1px 0 0 rgba(255,255,255,0.1);}.chat-sidebar-header{position:sticky;top:0;display:flex;align-items:center;justify-content:space-between;padding:12px 16px;background-color:var(--bg-color-operate);border-bottom:1px solid var(--stroke-color-primary);z-index:10;}.chat-sidebar-title{font-size:16px;font-weight:500;color:var(--text-color-primary);}.empty-placeholder{flex:1;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:12px;background-color:var(--bg-color-operate);border-left:1px solid rgba(0,0,0,0.08);color:#adb5bd;}.empty-icon{font-size:64px;opacity:0.3;}.empty-title{font-size:16px;font-weight:600;color:#6c757d;}.empty-subtitle{font-size:14px;color:#868e96;}img[alt="empty"]{display:none;}.message-input-container{border-top:1px solid var(--stroke-color-primary);}.call-kit{position:fixed;top:50%;left:50%;z-index:999;transform:translate(-50%,-50%);max-width:800px;max-height:600px;}
</style>

<style>
#app{background:linear-gradient(135deg,#667eea 0%,#764ba2 100%) !important;width:100vw !important;height:100vh !important;text-align:start !important;max-width:none !important;display:flex !important;align-items:center !important;justify-content:center !important}
</style>
```

#### 2.2 Add Side Navigation

Create a new file `SideTab.vue` in the `src/component` folder and add the following content:

```typescript
<template>
  <div class="side-tab" :class="{ dark: isDark }">
    <!-- User Avatar -->
    <div class="avatar-wrapper">
      <Avatar class="avatar" :src="loginUserInfo?.avatarUrl" />
      <div class="tooltip">
        <div class="tooltip-name">{{ loginUserInfo?.userName || 'Unnamed' }}</div>
        <div class="tooltip-id">ID: {{ loginUserInfo?.userId }}</div>
      </div>
    </div>
    <!-- Tab Switcher -->
    <div class="tabs">
      <div 
        class="tab-item"
        :class="{ active: props.activeTab === 'conversations' }"
        @click="handleTabChange('conversations')"
        title="Conversations"
      >
        <IconChatNew size="24" />
      </div>
      <div 
        class="tab-item"
        :class="{ active: props.activeTab === 'contacts' }"
        @click="handleTabChange('contacts')"
        title="Contacts"
      >
        <IconContacts size="24" />
      </div>
    </div>
  </div>
</template>


<script lang="ts" setup>
import { computed } from 'vue';
import { useLoginState, useUIKit, Avatar } from '@tencentcloud/chat-uikit-vue3';
import { IconChatNew, IconContacts } from '@tencentcloud/uikit-base-component-vue3';

const { theme } = useUIKit();
const { loginUserInfo } = useLoginState();

const isDark = computed(() => theme.value === 'dark' || theme.value === 'serious');

interface Props {
  activeTab?: 'conversations' | 'contacts';
}

const props = withDefaults(defineProps<Props>(), {
  activeTab: 'conversations'
});

const emit = defineEmits<{
  tabChange: [tab: 'conversations' | 'contacts'];
}>();

const handleTabChange = (tab: 'conversations' | 'contacts') => {
  emit('tabChange', tab);
};
</script>

<style scoped>
.side-tab{width:72px;height:100vh;background:var(--bg-color-function);display:flex;flex-direction:column;align-items:center;padding:20px 0;transition:background 0.3s;}.avatar-wrapper{position:relative;margin-bottom:24px;cursor:pointer;}.avatar-wrapper:hover:deep(.avatar){transform:scale(1.05);box-shadow:0 4px 12px rgba(0,0,0,0.15);}.tooltip{position:absolute;left:60px;top:50%;transform:translateY(-50%);padding:8px 12px;background:rgba(0,0,0,0.85);color:#fff;border-radius:6px;white-space:nowrap;opacity:0;visibility:hidden;pointer-events:none;transition:all 0.3s;z-index:1000;}.tooltip::before{content:'';position:absolute;left:-6px;top:50%;transform:translateY(-50%);border:6px solid transparent;border-right-color:rgba(0,0,0,0.85);}.avatar-wrapper:hover .tooltip{opacity:1;visibility:visible;}.tooltip-name{font-size:14px;font-weight:500;margin-bottom:4px;}.tooltip-id{font-size:12px;opacity:0.8;}.tabs{display:flex;flex-direction:column;gap:16px;}.tab-item{width:48px;height:48px;display:flex;align-items:center;justify-content:center;border-radius:12px;cursor:pointer;transition:all 0.3s;color:var(--text-color-primary);}.tab-item:hover{background:rgba(0,0,0,0.05);}.tab-item.active{background:var(--button-color-primary-default);color:var(--text-color-button);}.side-tab.dark{background:#1a1a1a;}.side-tab.dark .avatar-wrapper:hover:deep(.avatar){box-shadow:0 4px 12px rgba(255,255,255,0.2);}.side-tab.dark .tooltip{background:rgba(255,255,255,0.95);color:#1a1a1a;}.side-tab.dark .tooltip::before{border-right-color:rgba(255,255,255,0.95);}.side-tab.dark .tab-item:hover{background:rgba(255,255,255,0.1);}.side-tab.dark .tab-item.active{background:#1890ff;color:#fff;}
</style>
```

### Step 3: Obtain SDKAppID, userID, and userSig

Fill in the login credentials SDKAppID, userID, and userSig in the login function in the `src/App.vue` file from the previous step.

```typescript
// Login
login({
  sdkAppId: 0, // SDKAppID, number type
  userId: '',  // UserID, string type
  userSig: '', // userSig, string type
});
```

| Parameter | Type | Description |
|-----------|------|-------------|
| SDKAppID | Number | SDKAppID is the unique identifier for Tencent Cloud Chat client applications. You can create a new application in the [Tencent Cloud Chat Console](https://console.trtc.io/) to obtain the SDKAppID.<br>**Note:**<br>SDKAppID is the unique identifier for Tencent Cloud Chat client applications. We recommend that each independent App apply for a new SDKAppID. Messages between different SDKAppIDs are naturally isolated and cannot communicate with each other. |
| userID | String | The unique identifier for the user, defined by you. It can only contain uppercase and lowercase letters (a-z, A-Z), numbers (0-9), underscores, and hyphens. |
| userSig | String | The password for users to log in to Tencent Cloud Chat, which is essentially a ciphertext obtained by encrypting UserID and other information.<br>**Note:**<br>Development environment: To quickly run the demo, you can obtain UserSig through the [Tencent Cloud Chat Console](https://console.trtc.io/).<br>Production environment: Integrate the UserSig calculation code into your server and provide a project-facing interface. For the correct UserSig issuance method, please refer to [Generating UserSig on the Server](https://trtc.io/document/34385). |

## Run and Test

Use the following command to run the project:

**[shell]**
```bash
npm run dev
```

> **Note:**
> 
> 1. Please ensure that SDKAppID, userID, and userSig in [Step 3] have been successfully replaced. Failure to replace them will cause the project to behave abnormally.
> 2. userID and userSig have a one-to-one correspondence.
> 3. If the project fails to start, please check whether the development environment requirements are met.

## Integrate Advanced Features

### Audio/Video Calling

> **Note:**
> 
> TUICallKit is an audio/video calling UI component launched by Tencent Cloud. By integrating this component, you only need to write a few lines of code to experience audio/video calling functionality in your chat application.
> 

1. Install the `@tencentcloud/call-uikit-vue` dependency.

   ```bash
   npm install @tencentcloud/call-uikit-vue
   ```

2. Export `TUICallKit` from `@tencentcloud/call-uikit-vue` and mount it to a DOM node.

   Continue to add the following code in the `src/App.vue` file:

   ```typescript
   // src/App.vue
   <template>
     <UIKitProvider language="en-US" theme="light">
       <!-- Mount audio/video call core component -->
       <TUICallKit class="call-kit" />
       ...
     </UIKitProvider>
   <template>
   
   <script setup lang="ts">
   // Import audio/video call core component
   import { TUICallKit } from '@tencentcloud/call-uikit-vue';
   </script>
   ```

3. Uncomment the code in the `#headerToolbar` slot of the `<MessageInput />` component.

   ```typescript
   <MessageInput class="message-input-container">
     <template #headerToolbar>
       <div class="message-toolbar">
         <div class="message-toolbar-actions">
           <EmojiPicker />
           <FilePicker />
           <VideoPicker />
           <ImagePicker />
           <AudioCallPicker />
           <VideoCallPicker />
         </div>
         <button class="icon-button" @click="isSearchInChatShow = !isSearchInChatShow">
           <IconSearch size="20" />
         </button>
       </div>
     </template>
   </MessageInput>
   ```

### Cloud Search

> **Note:**
> 
> Search is an essential feature in customer service, social, online education, online medical, OA and other scenarios. It helps users quickly find groups, users, and messages, improving product user experience and user stickiness.
> 
> Due to the special nature of local storage on the Web platform, Vue **cannot implement local search**. To better meet the demand for search capabilities, a **cloud search capability** has been launched. **Cloud search functionality supports global search and in-conversation search, and supports searching for groups, users, and messages.**
> 
> This feature is a value-added service that requires you to purchase the cloud search plugin.
> 

Cloud search is integrated by default in "Step 2". If you need to disable the cloud search functionality, please refer to the following code:

1. Set the `enableSearch` property of `ConversationList` to `false`

   ```typescript
   <template>
     <ConversationList v-show="activeTab === 'conversations'" :enable-search="false" />
   </template>
   ```

2. Comment out the code related to the in-conversation search sidebar

   ```typescript
   <template>
     <Chat>
       <!-- <div v-show="isSearchInChatShow" class="chat-sidebar" :class="{ dark: theme === 'dark' }">
         <div class="chat-sidebar-header">
           <span class="chat-sidebar-title">Search</span>
           <button class="icon-button" @click="isSearchInChatShow = false">✕</button>
         </div>
         <Search :variant="VariantType.EMBEDDED" />
       </div> -->
     </Chat>
   </template>
   ```

## FAQ

### Can I use third-party component libraries, such as Element-Plus?

You can use other component libraries for the glue code between core components, as shown in the example code. For example, you can wrap `<ChatSetting />` as a full-screen drawer component. However, components that already exist within core components are not currently supported for modification.

```typescript
const isChatSettingShow = ref(false);

<el-drawer
  v-model="isChatSettingShow"
  title="Settings"
>
    <ChatSetting />
</el-drawer>
```

### NPM Package

[chat-uikit-vue3 npm](https://www.npmjs.com/package/@tencentcloud/chat-uikit-vue3)

### GitHub

[GitHub Demo](https://github.com/Tencent-RTC/TUIKit_Vue3/tree/main/demos/rtcube-vite-vue3)
