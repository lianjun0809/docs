> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

TUIKit 是基于腾讯云 Chat SDK 的一款 Vue 3 UI 组件库，它提供了一些通用的 UI 组件，包含会话、聊天、群组等功能。本文介绍如何快速集成 TUIKit 并实现核心功能。

> **说明：**
> 

> 您好！我们正在开发一款即时通讯产品 UIKit，它基于腾讯云 Chat SDK，是一款 Vue3 UI 组件库，能帮助您快速集成并实现核心功能。
> 

> **为了更好地提升我们的产品，了解您的需求**，特邀请您[参与本次问卷调查](https://wj.qq.com/s2/25022971/d8b4/)。
> 

> 您的反馈我们会**高度重视**，本问卷填写**仅需要 30 秒**！诚邀您的参与。
> 


> **推荐使用更高效的 AI 集成助手**
> 

> 我们为您提供了全新的 AI 集成方式，只需要简单描述您的需求，即可**自动生成集成代码**，大幅提升开发效率。
> 

> [点击这里，立即体验 AI 集成](https://cloud.tencent.com/document/product/269/124481)
> 


![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100033438418/38ff95e4c9ec11f0a93d52540044a08e.png)


## 关键概念

chat-uikit-vue3 主要分为 ConversationList、Chat、MessageList、ChatHeader、MessageInput、ChatSetting、Search、Contact 等核心 UI 组件，每个 UI 组件负责展示不同的内容。
1. ConversationList 提供会话列表组件。

2. Chat 提供会话的容器组件。

3. MessageList 提供会话的消息列表组件。

4. ChatHeader 提供会话的头部信息组件。

5. MessageInput 提供输入框组件。

6. ChatSetting 提供单聊和群聊的管理组件。

7. Search 提供云端搜索组件。

8. Contact 提供联系人组件。


## 前提条件
- Vue.js@^3.0.0

- TypeScript@^5.0.0

- Node.js（Node.js ≥ 20.0.0，建议使用目前的 LTS v22 版本）


## 创建项目

使用 Vite 创建一个新的名称为 **chat-example** 的 Vue3 项目。

> **说明：**
> 

> 高版本 Vite 需要使用最新的 Node.js 版本。
> 



【shell】
``` bash
npm create vite@latest
```

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/f67b7f3a886611f0b321525400e889b2.png)


## 下载并导入组件

创建项目完成后，切换到项目所在目录。


【shell】
``` bash
cd chat-example
npm install
```

### 步骤1：安装依赖


【shell】
``` bash
npm i @tencentcloud/chat-uikit-vue3
```

### 步骤2：引入组件

> **注意：**
> 
> - 以下代码中未填入 `SDKAppID`、`userID` 和 `userSig`，需在 [步骤3](https://write.woa.com/#e0579535-1fc9-4344-8878-ed25ced85819) 中获取相关信息后进行替换。
> - 为了尊重版权，下图所示的**默认小黄脸表情包版权属于腾讯云**，您可以通过升级至 [IM 企业版套餐](https://buy.cloud.tencent.com/avc) 免费使用该表情包。

> ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/d9f2ac13886711f0bd05525400454e06.png)
> 


#### 2.1 搭建主界面

例如：在  `src/App.vue` 页面中写入以下代码：
``` typescript
<template>
  <UIKitProvider language="zh-CN" theme="light">
    <div class="chat-layout">
      <!-- 左侧导航 -->
      <SideTab :active-tab="activeTab" @tab-change="handleTabChange" />
      
      <!-- 中间列表 -->
      <div class="conversation-list-panel">
        <ConversationList v-show="activeTab === 'conversations'" />
        <ContactList v-show="activeTab === 'contacts'" />
      </div>
      
      <!-- 右侧聊天 -->
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
                <!-- 参考文档开通音视频通话服务 -->
                <!-- <AudioCallPicker />
                <VideoCallPicker /> -->
              </div>
              <button class="icon-button" @click="isSearchInChatShow = !isSearchInChatShow">
                <IconSearch size="20" />
              </button>
            </div>
          </template>
        </MessageInput>

        <!-- 聊天设置侧边栏 -->
        <div v-show="isChatSettingShow" class="chat-sidebar" :class="{ dark: theme === 'dark' }">
          <div class="chat-sidebar-header">
            <span class="chat-sidebar-title">设置</span>
            <button class="icon-button" @click="isChatSettingShow = false">✕</button>
          </div>
          <ChatSetting />
        </div>

        <!-- 会话内搜索侧边栏 -->
        <div v-show="isSearchInChatShow" class="chat-sidebar" :class="{ dark: theme === 'dark' }">
          <div class="chat-sidebar-header">
            <span class="chat-sidebar-title">群搜索</span>
            <button class="icon-button" @click="isSearchInChatShow = false">✕</button>
          </div>
          <Search :variant="VariantType.EMBEDDED" />
        </div>
      </Chat>

      <!-- 联系人详情 -->
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

// 切换会话时关闭会话内侧边栏
watch(() => activeConversation.value?.conversationID, (newVal, oldVal) => {
  if (newVal !== oldVal) {
    isChatSettingShow.value = false;
    isSearchInChatShow.value = false;
  }
});

// 登录
login({
  sdkAppId: 0, // SDKAppID, number 类型
  userId: '',  // UserID, string 类型
  userSig: '', // userSig, string 类型
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

// 空会话占位组件
const EmptyChatTpl = h('div', { class: 'empty-placeholder' }, [
  h('div', { class: 'empty-icon' }, '💬'),
  h('div', { class: 'empty-title' }, '暂无会话'),
  h('div', { class: 'empty-subtitle' }, '选择一个会话开始聊天'),
]);
</script>

<style scoped>
.chat-layout{width:calc(100vw - 64px);height:calc(100vh - 64px);max-width:1600px;max-height:900px;display:flex;border-radius:16px;box-shadow:0 20px 60px rgba(0,0,0,0.3),0 0 0 1px rgba(255,255,255,0.1);overflow:hidden;backdrop-filter:blur(10px);}.conversation-list-panel{width:300px;display:flex;flex-direction:column;border-right:1px solid var(--stroke-color-primary);overflow:hidden;}.chat-content-panel{flex:1;}.contact-detail-panel{flex:1;}.icon-button{padding:4px 6px;display:flex;align-items:center;justify-content:center;border:none;background:transparent;border-radius:4px;font-size:20px;color:var(--text-color-primary);cursor:pointer;transition:background-color 0.2s;outline:none;}.icon-button:focus{outline:none;}.icon-button:hover{background-color:var(--button-color-secondary-hover);}.icon-button:active{background-color:var(--button-color-secondary-active);}.message-toolbar{display:flex;justify-content:space-between;align-items:center;}.message-toolbar-actions{display:flex;align-items:center;gap:4px;}.chat-sidebar{position:absolute;right:0;top:0;bottom:0;min-width:300px;max-width:400px;display:flex;flex-direction:column;background-color:var(--bg-color-operate);box-shadow:var(--shadow-color) 0 0 10px;overflow:auto;z-index:1000;}.chat-sidebar.dark{box-shadow:-4px 0 16px rgba(0,0,0,0.4),-1px 0 0 rgba(255,255,255,0.1);}.chat-sidebar-header{position:sticky;top:0;display:flex;align-items:center;justify-content:space-between;padding:12px 16px;background-color:var(--bg-color-operate);border-bottom:1px solid var(--stroke-color-primary);z-index:10;}.chat-sidebar-title{font-size:16px;font-weight:500;color:var(--text-color-primary);}.empty-placeholder{flex:1;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:12px;background-color:var(--bg-color-operate);border-left:1px solid rgba(0,0,0,0.08);color:#adb5bd;}.empty-icon{font-size:64px;opacity:0.3;}.empty-title{font-size:16px;font-weight:600;color:#6c757d;}.empty-subtitle{font-size:14px;color:#868e96;}img[alt="empty"]{display:none;}.message-input-container{border-top:1px solid var(--stroke-color-primary);}.call-kit{position:fixed;top:50%;left:50%;z-index:999;transform:translate(-50%,-50%);max-width:800px;max-height:600px;}
</style>

<style>
#app{background:linear-gradient(135deg,#667eea 0%,#764ba2 100%) !important;width:100vw !important;height:100vh !important;text-align:start !important;max-width:none !important;display:flex !important;align-items:center !important;justify-content:center !important}
</style>
```

#### 2.2 引入侧边导航

在 `src/component` 文件夹中新建一个 `SideTab.vue` 的文件，并写入以下内容：
``` typescript
<template>
  <div class="side-tab" :class="{ dark: isDark }">
    <!-- 用户头像 -->
    <div class="avatar-wrapper">
      <Avatar class="avatar" :src="loginUserInfo?.avatarUrl" />
      <div class="tooltip">
        <div class="tooltip-name">{{ loginUserInfo?.userName || '未命名' }}</div>
        <div class="tooltip-id">ID: {{ loginUserInfo?.userId }}</div>
      </div>
    </div>
    <!-- Tab 切换 -->
    <div class="tabs">
      <div 
        class="tab-item"
        :class="{ active: props.activeTab === 'conversations' }"
        @click="handleTabChange('conversations')"
        title="会话"
      >
        <IconChatNew size="24" />
      </div>
      <div 
        class="tab-item"
        :class="{ active: props.activeTab === 'contacts' }"
        @click="handleTabChange('contacts')"
        title="联系人"
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

### 步骤3：获取 SDKAppID、userID 和 userSig

在上一步的 `src/App.vue`文件中的 login 函数，填入登录信息 SDKAppID、userID 和 userSig。
``` java
// 登录
login({
  sdkAppId : , // SDKAppID, number 类型
  userId: '',  // UserID, string 类型
  userSig: '', // userSig, string 类型
});
```
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >说明</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SDKAppID</td>

<td rowspan="1" colSpan="1" >Number</td>

<td rowspan="1" colSpan="1" >SDKAppID 是腾讯云 IM 客户应用的唯一标识。您可以在 [即时通信 IM 控制台](https://console.cloud.tencent.com/im) 创建新应用，获取 SDKAppID 。<br>**说明：**<br>SDKAppID 是腾讯云 IM 客户应用的唯一标识。我们建议每一个独立的 App 都申请一个新的 SDKAppID。不同 SDKAppID 之间的消息是天然隔离的，不能互通。<br></td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userID</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >用户的唯一标识符，由您定义，只能包含大小写字母（a-z，A-Z）、数字（0-9）、下划线和连字符。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userSig</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >用户登录即时通信 IM 的密码，其本质是对 UserID 等信息加密后得到的密文。<br>**说明：**<br>开发环境：快速跑通 Demo，可以通过 [即时通信 IM 控制台](https://console.cloud.tencent.com/im) 获取 UserSig。<br>生产环境：将 UserSig 的计算代码集成到您的服务端，并提供面向项目的接口， 正确的 UserSig 签发方式请参见 [服务端生成 UserSig](https://cloud.tencent.com/document/product/269/32688)。<br></td>
</tr>
</table>


> **注意：**
> 

> 本文示例代码采用在[即时通信 IM 控制台](https://console.cloud.tencent.com/im) 获取 UserSig 的方案，**该方法仅适合本地跑通功能调试**。 正确的 UserSig 签发方式请参见[服务端生成 UserSig](https://cloud.tencent.com/document/product/269/32688)。
> 

- SDKAppID：在 [即时通信 IM 控制台 > 应用管理](https://console.cloud.tencent.com/im) 单击**创建新应用**，获取 SDKAppID。

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/748bfda2886c11f088af5254005ef0f7.png)

- userID：单击 [即时通信 IM 控制台 > 消息服务 Chat > 账号管理](https://console.cloud.tencent.com/im/account-management)，切换至目标应用所在账号，您可以创建 2～3 个账号用于体验单聊、群聊的功能。

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/b9a2b2aa886d11f0ae9d5254001c06ec.png)

- userSig：单击 [即时通信 IM 控制台 > 开发工具 > UserSig生成校验](https://console.cloud.tencent.com/im/tool-usersig)，切换至目标应用所在账号，填写创建的 UserID，即可生成 UserSig。

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/ea68ff91886e11f0ae9d5254001c06ec.png)


## 运行和测试

使用以下命令运行项目


【shell】
``` bash
 npm run dev
```

> **注意：**
> 
> 1. 请确保 [步骤3](https://write.woa.com/#step3) 代码中  SDKAppID、userID 和 userSig 均已成功替换，如未替换将会导致项目表现异常。
> 2. userID 和 userSig  为一一对应关系。
> 3. 如遇到项目启动失败，请检查 开发环境要求 是否满足。


## 集成更多高级特性

### 音视频通话

> **说明：**
> 

> TUICallKit 是腾讯云推出一款音视频通话 UI 组件，通过集成该组件，您只需要编写几行代码就可以在聊天应用中体验音视频通话功能。
> 

> 更多详细信息可参考：[音视频通话-开通服务](https://write.woa.com/document/140130594134605824)。
> 

1. 安装 `@tencentcloud/call-uikit-vue` 依赖。

   ``` bash
     npm install @tencentcloud/call-uikit-vue
   ```
2. 从 `@tencentcloud/call-uikit-vue` 导出 `TUICallKit`，并挂载到 DOM 节点上。


   在 `src/App.vue` 文件中继续补充下面的代码：

   ``` typescript
   // src/App.vue
   <template>
     <UIKitProvider language="zh-CN" theme="light">
       <!-- 挂载音视频通话核心组件 -->
       <TUICallKit class="call-kit" />
       ...
     </UIKitProvider>
   <template>
   
   <script setup lang="ts">
   // 导入音视频通话核心组件
   import { TUICallKit } from '@tencentcloud/call-uikit-vue';
   </script>
   ```
3. 打开 `<MessageInput />` 组件中 `#headerToolbar` 插槽内的注释。

   ``` java
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
4. 拨打语音通话。

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100033438418/ce88eb5ac9f911f0a7775254005ef0f7.png)


### 云端搜索

> **说明：**
> 

> 搜索，在客服、社交、在线教育、在线医疗、OA 等场景下是刚需功能，可帮助用户快速查找群组、用户、消息，提升产品使用体验和用户粘性。
> 

> 由于 Web 平台本地存储特殊性等原因，Vue **无法实现本地搜索**，为了更好的满足对于搜索能力的需求，推出了**云端搜索能力**。**云端搜索功能支持全局搜索和会话内搜索，同时支持搜索群组、用户和消息。**
> 

> 
> 

> 此功能属于增值服务，需要您购买云端搜索插件，请点击 [购买](https://console.cloud.tencent.com/im/plugin/TUICloudSearch)。
> 


云端搜索在“步骤 2”中已经默认集成，如果需要关闭云端搜索功能，请参考以下代码：
1. 设置 `ConversationList` 的 `enableSearch` 属性为 `false`

   ``` typescript
   <template>
     <ConversationList v-show="activeTab === 'conversations'" :enable-search="false" />
   </template>
   ```
2. 注释会话内搜索侧边栏相关的代码

   ``` typescript
   <template>
     <Chat>
       <!-- <div v-show="isSearchInChatShow" class="chat-sidebar" :class="{ dark: theme === 'dark' }">
         <div class="chat-sidebar-header">
           <span class="chat-sidebar-title">搜索</span>
           <button class="icon-button" @click="isSearchInChatShow = false">✕</button>
         </div>
         <Search :variant="VariantType.EMBEDDED" />
       </div> -->
     </Chat>
   </template>
   ```

## 常见问题

### 什么是 UserSig？如何生成 UserSig？

UserSig 是用户登录即时通信 IM 的密码，其本质是对 UserID 等信息加密后得到的密文。UserSig 签发方式是将 UserSig 的计算代码集成到您的服务端，并提供面向项目的接口，在需要 UserSig 时由您的项目向业务服务器发起请求获取动态 UserSig。更多详情请参见 [服务端生成 UserSig](https://cloud.tencent.com/document/product/269/32688)。

> **注意：**
> 

> 本文示例代码采用在 [即时通信 IM 控制台](https://console.cloud.tencent.com/im) 获取 UserSig 的方案，**该方法仅适合本地跑通功能调试**。 正确的 UserSig 签发方式请参见 [服务端生成 UserSig](https://cloud.tencent.com/document/product/269/32688)。
> 


### 我能不能使用第三方组件库，例如 Element-Plus？

核心组件之间的粘连代码可以使用其他组件库，这一点在示例代码中也可以看到，例如您可以将 `<ChatSetting />` 封装成全屏抽屉组件。但是核心组件内部已经存在的组件暂时不支持修改。
``` java
const isChatSettingShow = ref(false);

<el-drawer
  v-model="isChatSettingShow"
  title="设置"
>
    <ChatSetting />
</el-drawer>
```

## 参考信息

### 官网文档
- [自定义组件 - UIKitProvider](https://write.woa.com/document/187032638782849024)

- [自定义组件 - Chat](https://write.woa.com/document/187778215983329280)

- [自定义组件 - ChatHeader](https://write.woa.com/document/187852524064485376)

- [自定义组件 - ConversationList](https://write.woa.com/document/186960319111872512)

- [自定义组件 - MessageList](https://write.woa.com/document/187036342928752640)

- [自定义组件 - MessageInput](https://write.woa.com/document/187058763983568896)

- [自定义组件 - ChatSetting](https://write.woa.com/document/187321409859108864)

- [自定义组件 - ContactList](https://write.woa.com/document/187595466274463744)

- [自定义组件 - Search](https://write.woa.com/document/187595449195040768)


### NPM 包

[chat-uikit-vue3 npm](https://www.npmjs.com/package/@tencentcloud/chat-uikit-vue3)

### GitHub

[GitHub Demo](https://github.com/Tencent-RTC/TUIKit_Vue3/tree/main/demos/rtcube-vite-vue3)

## 联系我们

如遇任何问题，可联系 [官网售后](https://cloud.tencent.com/act/event/connect-service#/) 反馈，享有专业工程师的支持，解决您的难题。
