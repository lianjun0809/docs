> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

## 组件概述

ChatSetting 是一个聊天设置组件，它能根据当前激活的**会话类型**（单聊或群聊）自动渲染对应的设置界面。该组件通过统一的入口，无缝集成了 C2C（单聊） 和群聊两种模式的设置功能，为用户提供了流畅且一致的操作体验。

核心功能：
- 智能适配： 自动识别**会话类型**，并切换至相应的设置面板。

- 状态驱动： 基于当前会话状态，动态更新设置内容。
   

   > **注意：**
   > 

   > 如果当前没有激活的会话则不会显示。
   > 


## 快速使用
``` typescript
import {
  UIKitProvider,
  useLoginState,
  LoginStatus,
  ConversationList,
  Chat,
  ChatHeader,
  MessageList,
  MessageInput,
  useUIOpenControlState,
  ChatSetting,
  Search,
  VariantType,
  ContactList,
  ContactInfo,
} from "@tencentcloud/chat-uikit-react";
import { useState } from "react";

function App() {
  const { isChatSettingOpen, isChatSearchOpen } = useUIOpenControlState();
  const [activeTab, setActiveTab] = useState('chats');

  // 从控制台获取登录信息
  const { status } = useLoginState({
    SDKAppID: 0,
    userID: '',
    userSig: '',
  })

  if (status !== LoginStatus.SUCCESS) {
    return <div>Loading...</div>
  }
  
  // 语言支持 en-US(default) / zh-CN / ja-JP / ko-KR / zh-TW
  // 主题支持 light(default) / dark
  return (
    <UIKitProvider>
      <div style={{ height: '100vh', width: '100vw', display: 'flex', flexDirection: 'row' }}>
        <ul>
          <li onClick={() => {setActiveTab('chats')}}>chats</li>
          <li onClick={() => {setActiveTab('contacts')}}>contact</li>
        </ul>
        {
          activeTab === 'chats' && (
            <>
              <ConversationList style={{ minWidth: '300px', maxWidth: '350px' }}/>
              <Chat PlaceholderEmpty="No messages yet">
                <ChatHeader />
                <MessageList />
                <MessageInput />
              </Chat>
              {isChatSettingOpen && <ChatSetting />}
              {isChatSearchOpen &&  <Search style={{ minWidth: '300px'}} variant={VariantType.EMBEDDED} />}
            </>
          )
        }
        {
          activeTab === 'contacts' && (
            <>
              <ContactList style={{ minWidth: '300px', maxWidth: '350px' }}/>
              <ContactInfo 
                PlaceholderEmpty="No contact yet"
                onSendMessage={() => {setActiveTab('chats')}}
                onEnterGroup={() => {setActiveTab('chats')}}
              />
            </>
          )
        }
      </div>
    </UIKitProvider>
  );
}

export default App;
```

## 相关文档

**官方文档**
- [自定义组件 - UIKitProvider](https://write.woa.com/document/157860913203511296)

- [自定义组件 - ConversationList](https://write.woa.com/document/157860932619919360)

- [自定义组件 - MessageList](https://write.woa.com/document/181344255270170624)

- [自定义组件 - MessageInput](https://write.woa.com/document/181344257863962624)

- [自定义组件 - ContactList](https://write.woa.com/document/181344260082749440)

- [自定义组件 - Search](https://write.woa.com/document/181344262590197760)


   **NPM 包**

- [chat-uikit-react npm](https://www.npmjs.com/package/@tencentcloud/chat-uikit-react)


   **GitHub**

- [GitHub Demo](https://github.com/TencentCloud/chat-uikit-react)


## 交流与反馈

如遇任何问题，可联系 [官网售后](https://cloud.tencent.com/act/event/connect-service#/) 反馈，享有专业工程师的支持，解决您的难题。
