> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

TUIKit 是基于腾讯云 Chat SDK 的一款 vue3 UI 组件库，它提供了一些通用的 UI 组件，包含会话、聊天、群组等功能。本文介绍如何快速集成 TUIKit 并实现核心功能。

> **推荐使用更高效的 AI 集成助手**
> 

> 我们为您提供了全新的 AI 集成方式，只需要简单描述您的需求，即可**自动生成集成代码**，大幅提升开发效率。
> 

> [点击这里，立即体验 AI 集成](https://cloud.tencent.com/document/product/269/124481)
> 


![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100033438418/642eec49c9ec11f0a7775254005ef0f7.png)


## 关键概念

chat-uikit-react 主要分为 ConversationList、Chat、MessageList、ChatHeader、MessageInput、ChatSetting、Search、Contact 等核心 UI 组件，每个 UI 组件负责展示不同的内容。
1. ConversationList 提供会话列表组件。

2. Chat 提供会话的容器组件。

3. MessageList 提供会话的消息列表组件。

4. ChatHeader 提供会话的头部信息组件。

5. MessageInput 提供输入框组件。

6. ChatSetting 提供单聊和群聊的管理组件。

7. Search 提供云端搜索组件。

8. Contact 提供联系人组件。


## 前提条件
- Node.js v18 版本及以上，建议使用当前的 LTS v22 版本

- React v18 版本

- TypeScript@^5.0.0


## 创建项目

创建一个新的名为 **chat-example** 的 React 项目（创建项目时选择 **React 18**，并且使用 TypeScript 模板），并按照脚手架提示完成项目的初始化。


【shell】
``` bash
npm create rsbuild@latest 
# 初始化脚手架项目
cd chat-example
npm i
npm run dev
```

## 下载并导入组件

### 步骤 1. 安装依赖

通过 npm 方式下载 [chat-uikit-react](https://www.npmjs.com/package/@tencentcloud/chat-uikit-react) 并在项目中使用。


【shell】
``` bash
npm i @tencentcloud/chat-uikit-react
```

### 步骤 2. 引入组件

> **注意：**
> 
> - 以下代码中未填入 `SDKAppID`、`userID` 和 `userSig`，需在 [步骤3](https://write.woa.com/#e0579535-1fc9-4344-8878-ed25ced85819) 中获取相关信息后进行替换。
> - 为了尊重版权，IM Demo/TUIKit 工程中默认不包含大表情元素切图。正式上线商用前请您替换为自己设计或拥有版权的其他表情包。下图所示默认的**小黄脸表情包版权归腾讯云所有**，可以有偿授权使用，如需获得授权您可以通过升级至 [IM 企业版套餐](https://buy.cloud.tencent.com/avc) 免费使用该表情包。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100033438418/ef57d018a9a111f09b75525400bf7822.png)



复制以下 `App.tsx` 代码并替换原有的 `src/App.tsx` 中的内容。




【src/App.tsx】
``` typescript
import { useEffect, useLayoutEffect, useState, useMemo } from "react";
import {
  UIKitProvider,
  useLoginState,
  LoginStatus,
  ConversationList,
  Chat,
  ChatHeader,
  MessageList,
  MessageInput,
  ContactList,
  ContactInfo,
  ChatSetting,
  Search,
  VariantType,
  Avatar,
  useUIKit,
  useConversationListState,
} from "@tencentcloud/chat-uikit-react";
import { IconChat, IconUsergroup, IconBulletpoint, IconSearch } from "@tencentcloud/uikit-base-component-react";
import './App.css';

function App() {
  // 语言支持 en-US(default) / zh-CN / ja-JP / ko-KR / zh-TW
  // 主题支持 light(default) / dark
  return (
    <UIKitProvider theme={'light'} language={'zh-CN'}>
      <ChatApp />
    </UIKitProvider>
  );
}

function ChatApp() {
  const [activeTab, setActiveTab] = useState<'conversations' | 'contacts'>('conversations');
  const [isChatSettingShow, setIsChatSettingShow] = useState(false);
  const [isSearchInChatShow, setIsSearchInChatShow] = useState(false);
  
  const { language, theme } = useUIKit();

  const isDark = theme === 'dark';

  const texts = useMemo(() => 
    language === 'zh-CN'
      ? { emptyTitle: '暂无会话', emptySub: '选择一个会话开始聊天', error: '请检查 SDKAppID, userID, userSig, 通过开发人员工具(F12)查看具体的错误信息', loading: '登录中...' }
      : { emptyTitle: 'No conversation', emptySub: 'Select a conversation to start chatting', error: 'Please check the SDKAppID, userID, and userSig. View the specific error information through the developer tools (F12).', loading: 'Logging in...'},
    [language]
  );

  const { status } = useLoginState({
    SDKAppID: 0, // number 类型
    userID: '',  // string 类型
    userSig: '', // string 类型
  });

  const { setActiveConversation, activeConversation } = useConversationListState();

  // 初始化默认会话 可删除
  useEffect(() => {
    if (status === LoginStatus.SUCCESS) {
      const userID = 'administrator';
      const conversationID = `C2C${userID}`;
      setActiveConversation(conversationID);
    }
  }, [status, setActiveConversation]);

  // 切换会话时自动关闭侧边栏
  useLayoutEffect(() => {
    setIsChatSettingShow(false);
    setIsSearchInChatShow(false);
  }, [activeConversation?.conversationID]);

  if (status === LoginStatus.ERROR) {
    return (
      <div className="loading-container">
        <div className="loading-spinner"></div>
        <div className="loading-text">{texts.error}</div>
      </div>
    );
  }

  if (status !== LoginStatus.SUCCESS) {
    return (
      <div className="loading-container">
        <div className="loading-spinner"></div>
        <div className="loading-text">{texts.loading}</div>
      </div>
    );
  }

  return (
    <div className={`chat-layout ${isDark ? 'dark' : ''}`}>
      {/* 左侧导航 */}
      <SideTab activeTab={activeTab} onTabChange={setActiveTab} />

      {/* 中间列表 会话列表-联系人列表 */}
      <div className="conversation-list-panel">
        {activeTab === 'conversations' ? <ConversationList /> : <ContactList className="contact-list" />}
      </div>

      {/* 右侧聊天 */}
      {activeTab === 'conversations' && (
        <Chat
          className="chat-content-panel"
          PlaceholderEmpty={
            <div className="empty-placeholder">
              <div className="empty-icon">💬</div>
              <div className="empty-title">{texts.emptyTitle}</div>
              <div className="empty-subtitle">{texts.emptySub}</div>
            </div>
          }
        >
          <ChatHeader
            ChatHeaderRight={
              <div className="header-actions">
                <button
                  className="icon-button"
                  onClick={() => setIsSearchInChatShow(!isSearchInChatShow)}
                >
                  <IconSearch size="20px" />
                </button>
                <button
                  className="icon-button"
                  onClick={() => setIsChatSettingShow(!isChatSettingShow)}
                >
                  <IconBulletpoint size="20px" />
                </button>
              </div>
            }
          />
          <MessageList />
          <MessageInput />
          {/* 聊天设置侧边栏 */}
          {isChatSettingShow && (
            <div className="chat-sidebar">
              <div className="chat-sidebar-header">
                <span className="chat-sidebar-title">设置</span>
                <button
                  className="icon-button"
                  onClick={() => setIsChatSettingShow(false)}
                >
                  ✕
                </button>
              </div>
              <ChatSetting />
            </div>
          )}

          {/* 会话内搜索侧边栏 */}
          {isSearchInChatShow && (
            <div className="chat-sidebar">
              <div className="chat-sidebar-header">
                <span className="chat-sidebar-title">群搜索</span>
                <button
                  className="icon-button"
                  onClick={() => setIsSearchInChatShow(false)}
                >
                  ✕
                </button>
              </div>
              <Search variant={VariantType.EMBEDDED} />
            </div>
          )}
        </Chat>
      )}

      {/* 联系人详情 */}
      {activeTab === 'contacts' && (
        <ContactInfo
          className="contact-detail-panel"
          onSendMessage={() => setActiveTab('conversations')}
          onEnterGroup={() => setActiveTab('conversations')}
        />
      )}
    </div>
  );
}

// SideTab 组件：左侧导航栏
interface SideTabProps {
  activeTab: 'conversations' | 'contacts';
  onTabChange: (tab: 'conversations' | 'contacts') => void;
}

function SideTab({ activeTab, onTabChange }: SideTabProps) {
  const { theme } = useUIKit();
  const { loginUserInfo } = useLoginState();
  const isDark = theme === 'dark';

  return (
    <div className={`side-tab ${isDark ? 'dark' : ''}`}>
      {/* 用户头像 */}
      <div className="avatar-wrapper">
        <Avatar src={loginUserInfo?.avatarUrl} />
        <div className="tooltip">
          <div className="tooltip-name">{loginUserInfo?.userName || loginUserInfo?.userId || '未命名'}</div>
          <div className="tooltip-id">ID: {loginUserInfo?.userId}</div>
        </div>
      </div>

      {/* Tab 切换 */}
      <div className="tabs">
        <div
          className={`tab-item ${activeTab === 'conversations' ? 'active' : ''}`}
          onClick={() => onTabChange('conversations')}
          title="会话"
        >
          <IconChat size="24px" />
        </div>

        <div
          className={`tab-item ${activeTab === 'contacts' ? 'active' : ''}`}
          onClick={() => onTabChange('contacts')}
          title="联系人"
        >
          <IconUsergroup size="24px" />
        </div>
      </div>
    </div>
  );
}

export default App;
```

复制以下 `App.css` 代码并替换同级目录的 `src/App.css` 样式文件。




【src/App.css】
``` java

body{margin:0;padding:0;font-family:Inter,Avenir,Helvetica,Arial,sans-serif;background:linear-gradient(135deg,#667eea 0%,#764ba2 100%);min-height:100vh;box-sizing:border-box;}#root{height:100vh;display:flex;justify-content:center;align-items:center;}.chat-layout{height:60vh;aspect-ratio:16 / 9;margin:0 auto;display:flex;border-radius:16px;box-shadow:0 20px 60px rgba(0,0,0,0.3),0 0 0 1px rgba(255,255,255,0.1);overflow:hidden;backdrop-filter:blur(10px);}@media (max-width:1920px){.chat-layout{height:80vh;}}.conversation-list-panel{width:300px;display:flex;flex-direction:column;border-right:1px solid var(--uikit-theme-light-stroke-color-primary);overflow:hidden;}.dark .conversation-list-panel{border-right:1px solid var(--uikit-theme-dark-stroke-color-primary);}.contact-list{border-radius:0;}.chat-content-panel{flex:1;border-left:1px solid var(--uikit-theme-light-stroke-color-primary);}.dark .chat-content-panel{border-left:1px solid var(--uikit-theme-dark-stroke-color-primary);}.contact-detail-panel{flex:1;}.icon-button{padding:4px 6px;display:flex;align-items:center;justify-content:center;border:none;background:transparent;border-radius:4px;font-size:20px;color:var(--uikit-theme-light-text-color-link);cursor:pointer;transition:background-color 0.2s;}.dark .icon-button{color:var(--uikit-theme-dark-text-color-link);}.icon-button:hover{background-color:var(--uikit-theme-light-button-color-secondary-hover);}.dark .icon-button:hover{background-color:var(--uikit-theme-dark-button-color-secondary-hover);}.icon-button:active{background-color:var(--uikit-theme-light-button-color-secondary-active);}.dark .icon-button:active{background-color:var(--uikit-theme-dark-button-color-secondary-active);}.header-actions{display:flex;gap:8px;margin-left:8px;color:var(--uikit-theme-light-text-color-link);}.dark .header-actions{color:var(--uikit-theme-dark-text-color-link);}.message-toolbar{display:flex;justify-content:space-between;align-items:center;}.message-toolbar-actions{display:flex;align-items:center;gap:12px;}.chat-sidebar{position:absolute;right:0;top:0;bottom:0;min-width:300px;max-width:400px;display:flex;flex-direction:column;background-color:var(--uikit-theme-light-bg-color-operate);box-shadow:-2px 0 8px rgba(0,0,0,0.04),-4px 0 16px rgba(0,0,0,0.06),-8px 0 32px rgba(0,0,0,0.08);overflow:auto;z-index:1000;}.dark .chat-sidebar{background-color:var(--uikit-theme-dark-bg-color-operate);box-shadow:-2px 0 8px rgba(0,0,0,0.2),-4px 0 16px rgba(0,0,0,0.3),-8px 0 32px rgba(0,0,0,0.4),-1px 0 0 rgba(255,255,255,0.08);}.chat-sidebar-header{position:sticky;top:0;display:flex;align-items:center;justify-content:space-between;padding:12px 16px;background-color:var(--uikit-theme-light-bg-color-operate);border-bottom:1px solid var(--uikit-theme-light-stroke-color-primary);z-index:10;}.dark .chat-sidebar-header{background-color:var(--uikit-theme-dark-bg-color-operate);border-bottom:1px solid var(--uikit-theme-dark-stroke-color-primary);}.chat-sidebar-title{font-size:16px;font-weight:500;color:var(--uikit-theme-light-text-color-primary);}.dark .chat-sidebar-title{color:var(--uikit-theme-dark-text-color-primary);}.empty-placeholder{flex:1;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:12px;background-color:var(--uikit-theme-light-bg-color-operate);border-left:1px solid var(--uikit-theme-light-stroke-color-primary);color:#adb5bd;}.dark .empty-placeholder{background-color:var(--uikit-theme-dark-bg-color-operate);border-left:1px solid var(--uikit-theme-dark-stroke-color-primary);}.empty-icon{font-size:64px;opacity:0.3;}.empty-title{font-size:16px;font-weight:600;color:#6c757d;}.empty-subtitle{font-size:14px;color:#868e96;}.loading-container{display:flex;flex-direction:column;align-items:center;justify-content:center;height:100vh;gap:24px;}.loading-spinner{width:60px;height:60px;border:4px solid rgba(255,255,255,0.2);border-top-color:#ffffff;border-radius:50%;animation:spin 1s cubic-bezier(0.68,-0.55,0.265,1.55) infinite;box-shadow:0 4px 12px rgba(0,0,0,0.15);}.loading-text{color:#ffffff;font-size:18px;font-weight:500;letter-spacing:0.5px;animation:pulse 2s ease-in-out infinite;}@keyframes spin{0%{transform:rotate(0deg);}100%{transform:rotate(360deg);}}@keyframes pulse{0%,100%{opacity:1;}50%{opacity:0.6;}}.icon-image-effort{display:none;}.side-tab{width:72px;height:100%;background:var(--uikit-theme-light-bg-color-function);display:flex;flex-direction:column;align-items:center;padding:20px 0;transition:background 0.3s;}.side-tab.dark{background:var(--uikit-theme-dark-bg-color-function);}.avatar-wrapper{position:relative;margin-bottom:24px;cursor:pointer;}.avatar-wrapper:hover .tui-avatar{transform:scale(1.05);box-shadow:0 4px 12px rgba(0,0,0,0.15);}.tooltip{position:absolute;left:60px;top:50%;transform:translateY(-50%);padding:8px 12px;background:rgba(0,0,0,0.85);color:#fff;border-radius:6px;white-space:nowrap;opacity:0;visibility:hidden;pointer-events:none;transition:all 0.3s;z-index:1000;}.tooltip::before{content:'';position:absolute;left:-6px;top:50%;transform:translateY(-50%);border:6px solid transparent;border-right-color:rgba(0,0,0,0.85);}.avatar-wrapper:hover .tooltip{opacity:1;visibility:visible;}.tooltip-name{font-size:14px;font-weight:500;margin-bottom:4px;}.tooltip-id{font-size:12px;opacity:0.8;}.tabs{display:flex;flex-direction:column;gap:16px;}.tab-item{width:48px;height:48px;display:flex;align-items:center;justify-content:center;border-radius:12px;cursor:pointer;transition:all 0.3s;color:var(--uikit-theme-light-text-color-primary);}.dark .tab-item{color:var(--uikit-theme-dark-text-color-primary);}.tab-item:hover{background:rgba(0,0,0,0.05);}.tab-item.active{background:var(--uikit-theme-light-button-color-primary-default);color:var(--uikit-theme-light-text-color-button);}.dark .tab-item.active{background:var(--uikit-theme-dark-button-color-primary-default);color:var(--uikit-theme-dark-text-color-button);}.call-kit{position:fixed !important;top:50%;left:50%;z-index:999;transform:translate(-50%,-50%);max-width:800px;max-height:600px;}
```

### 步骤 3. 获取 SDKAppID、userID 和 userSig

在步骤2复制的 `App.tsx` 代码中，登录鉴权信息是空缺的，您还需要在 `useLoginState hook` 中填写您的腾讯云应用的鉴权信息，如下所示：
``` java
const { status } = useLoginState({
    SDKAppID: 0, // number 类型
    userID: '',  // string 类型
    userSig: '', // string 类型
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

<td rowspan="1" colSpan="1" >用户登录即时通信 IM 的密码，其本质是对 UserID 等信息加密后得到的密文。<br>**说明：**<br>- 开发环境：快速跑通 Demo，可以通过 [即时通信 IM 控制台](https://console.cloud.tencent.com/im) 获取 UserSig。<br>- 生产环境：将 UserSig 的计算代码集成到您的服务端，并提供面向项目的接口， 正确的 UserSig 签发方式请参见 [服务端生成 UserSig](https://cloud.tencent.com/document/product/269/32688)。<br></td>
</tr>
</table>


> **注意：**
> 

> 本文示例代码采用从 [即时通信 IM 控制台](https://console.cloud.tencent.com/im) 获取 UserSig 的方案，**该方法仅适合本地跑通功能调试**。 正确的 UserSig 签发方式请参见 [服务端生成 UserSig](https://cloud.tencent.com/document/product/269/32688)。
> 

- SDKAppID：在 [即时通信 IM 控制台 > 应用管理](https://console.cloud.tencent.com/im) 单击**创建新应用**，获取 SDKAppID。

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/797a92558a3211f0b321525400e889b2.png)

- userID：单击 [即时通信 IM 控制台 > 消息服务 Chat > 账号管理](https://console.cloud.tencent.com/im/account-management)，切换至目标应用所在账号，您可以创建 2～3 个账号用于体验单聊、群聊的功能。

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/796a45708a3211f0ae9d5254001c06ec.png)

- userSig：单击 [即时通信 IM 控制台 > 开发工具 > UserSig生成校验](https://console.cloud.tencent.com/im/tool-usersig)，切换至目标应用所在账号，填写创建的 userID，即可生成 userSig。

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/7991b0798a3211f0974b52540044a08e.png)


## 运行和测试

填入登录鉴权信息后即可运行项目开始体验。


【shell】
``` bash
npm run dev
```

> **注意：**
> 
> - 请确保 [步骤3](https://write.woa.com/#step3) 代码中  SDKAppID、userID 和 userSig 均已成功替换，如未替换将会导致项目表现异常。
> - userID 和 userSig  为一一对应关系，具体参见 [生成 UserSig（用户鉴权）](https://write.woa.com/document/107052240244191232)。
> - 如遇到项目启动失败，请检查 开发环境要求 是否满足。


## 集成更多高级特性

### 音视频通话

> **说明：**
> 

> TUICallKit 是腾讯云推出一款音视频通话 UI 组件，通过集成该组件，您只需要编写几行代码就可以在聊天应用中体验音视频通话功能。
> 

> 更多详细信息可参考：[音视频通话-开通服务](https://write.woa.com/document/140130594134605824)。
> 

1. 安装 `@trtc/calls-uikit-react` 依赖

   ``` bash
   npm install @trtc/calls-uikit-react
   ```
2. 从 `@trtc/calls-uikit-react` 导出 `TUICallKit`，并挂载到 DOM 节点上。


   在 `src/App.tsx` 文件中继续补充下面的代码：

   ``` typescript
   // src/App.tsx
   import { TUICallKit } from '@trtc/calls-uikit-react';
   
   function App() {
     return (
       <UIKitProvider>
         // 导入 TUICallKit 并添加到代码中
         <TUICallKit className="call-kit" />
         <ChatApp />
       </UIKitProvider>
     );
   }
   ```
3. 在 `<ChatHeader />` 上启用 `enableCall` 属性

   ``` java
   <ChatHeader enableCall={true} />
   ```
4. 拨打语音通话

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100033438418/31eeca37c9fa11f0aedb525400454e06.png)


### 云端搜索

> **说明：**
> 

> 搜索，在客服、社交、在线教育、在线医疗、OA 等场景下是刚需功能，可帮助用户快速查找群组、用户、消息，提升产品使用体验和用户粘性。
> 

> 由于 Web 平台本地存储特殊性等原因，Vue **无法实现本地搜索**，为了更好的满足对于搜索能力的需求，推出了**云端搜索能力**。**云端搜索功能支持全局搜索和会话内搜索，同时支持搜索群组、用户和消息。**
> 

> 此功能属于增值服务，需要您购买云端搜索插件，请点击 [购买](https://console.cloud.tencent.com/im/plugin/TUICloudSearch)。
> 


云端搜索在“步骤 2”中已经默认集成，如果需要关闭云端搜索功能，请参考以下代码：
1. 注释 `ChatHeader` 中 `ChatHeaderRight` 属性，和会话内搜索侧边栏相关的代码

   ``` typescript
   
   <ChatHeader enableCall={true}
     ChatHeaderRight={
       <div className="header-actions">
         <button
           className="icon-button"
           onClick={() => setIsSearchInChatShow(!isSearchInChatShow)}
         >
           <IconSearch size="20px" />
         </button>
         {/* <button
           className="icon-button"
           onClick={() => setIsChatSettingShow(!isChatSettingShow)}
         >
           <IconBulletpoint size="20px" />
         </button> */}
       </div>
     }
   />
   ```

## 常见问题

### 什么是 UserSig？如何生成 UserSig？

UserSig 是用户登录即时通信 IM 的密码，其本质是对 UserID 等信息加密后得到的密文。UserSig 签发方式是需将 UserSig 的计算代码集成到您的服务端，并提供面向项目的接口，在需要 UserSig 时由您的项目向业务服务器发起请求获取动态 UserSig。更多详情请参见 [服务端生成 UserSig](https://cloud.tencent.com/document/product/269/32688)。

> **注意：**
> 

> 本文示例代码采用在 [即时通信 IM 控制台](https://console.cloud.tencent.com/im) 获取 UserSig 的方案，**该方法仅适合本地跑通功能调试**。 正确的 UserSig 签发方式请参见[服务端生成 UserSig](https://cloud.tencent.com/document/product/269/32688)。
> 


### 是否支持 react 17/19 版本？

目前不支持 17.x/19.x 版本，仅支持 React v18。

### 我能不能使用第三方组件库，例如 Ant-Design？

核心组件之间的粘连代码可以使用其他组件库，这一点在示例代码中也可以看到，例如您可以将 `<ChatSetting />` 封装成全屏抽屉组件。但是核心组件内部已经存在的组件暂时不支持修改。
``` typescript
import { Drawer } from 'antd';

const [isChatSettingShow, setIsChatSettingShow] = useState(false);

function onChatSettingClose() {
  setIsChatSettingShow(false);
}

<Drawer
  title="设置"
  onClose={onClose}
  open={isChatSettingShow}
>
  <ChatSetting />
</Drawer>
```

## 参考信息

### 相关文档
- [自定义组件 - UIKitProvider](https://write.woa.com/document/157860913203511296)

- [自定义组件 - ConversationList](https://write.woa.com/document/157860932619919360)

- [自定义组件 - MessageList](https://write.woa.com/document/181344255270170624)

- [自定义组件 - MessageInput](https://write.woa.com/document/181344257863962624)

- [自定义组件 - ContactList](https://write.woa.com/document/181344260082749440)

- [自定义组件 - Search](https://write.woa.com/document/181344262590197760)

- [自定义组件 - ChatSetting](https://write.woa.com/document/187957510151921664)

- [chat-uikit-react npm](https://www.npmjs.com/package/@tencentcloud/chat-uikit-react)

- [GitHub Demo](https://github.com/TencentCloud/chat-uikit-react)


## 联系我们

如遇任何问题，可联系 [官网售后](https://cloud.tencent.com/act/event/connect-service#/) 反馈，享有专业工程师的支持，解决您的难题。
