> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/en/llms.txt
> Use this file to discover all available pages before exploring further.

TUIKit is a UI component library based on the Chat SDK. It enables quick implementation of chat, session, search, relationship chain, group, and other features through UI components. This article introduces how to quickly integrate TUIKit and implement core features
<iframe src="https://web.sdk.qcloud.com/im/demo/docs-example/sample-chat/index.html#/inbox?page=intergration" style="width:100%;height:700px;border:none" allow="camera; microphone; accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="no-referrer-when-downgrade" allowfullscreen></iframe>


## Prerequisites
- Node.js v18 or higher, recommend using the current LTS v22 version

- React v18


## Create a project

Create a new React project named **chat-app** (select **React 18** during project creation and use the TypeScript Template), and complete project initialization as prompted by the scaffold.


【shell】
``` bash
npm create rsbuild@latest
```

## Installing and Importing Components

### Step 1: Dependency Installation

Download [chat-uikit-react](https://www.npmjs.com/package/@tencentcloud/chat-uikit-react) via npm and use it in the project.


【shell】
``` bash
npm i @tencentcloud/chat-uikit-react
```

### Step 2: Introducing the chat uikit react component

> **Note:**
> 
> - The following code does not include `SDKAppID`, `userID`, and `UserSig`. You need to replace them with the relevant information obtained in [Step 4](https://write.woa.com/document/108053210129276928).
> - To respect the copyright of emoji designs, the Chat Demo/TUIKit project does not include large emoji graphics. Please replace them with your own designs or other emoji packs for which you hold the copyright before officially launching for commercial use. **The default smiley face emoji pack shown below is copyrighted by Tencent RTC**, you can upgrade to [Chat Pro Plus Edition and Enterprise Edition](https://console.trtc.io/subscription/buy/chat?packType=pro) to use it for free.

> ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027202808/a7c853cf981a11ef834b525400f69702.png)
> 


Copy the following `App.tsx` code and replace the original content in `App.tsx`.

Copy the following `App.css` code and replace the `App.css` style file in the same directory.




【App.tsx】
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
  ContactList,
  ContactInfo,
  useUIKit,
  useConversationListState,
} from "@tencentcloud/chat-uikit-react";
import { useEffect, useState } from "react";
import './App.css';

function App() {
  // Language support en-US(default) / zh-CN / ja-JP / ko-KR / zh-TW
  // Theme supports light(default) / dark
  return (
    <UIKitProvider theme={'light'} language={'en-US'}>
      <ChatApp />
    </UIKitProvider>
  );
}

function ChatApp() {
  const [activeTab, setActiveTab] = useState('chats');
  
  const { language } = useUIKit();
  
const texts = language === 'zh-CN'
    ? { chats: '会话', contacts: '联系人', emptyTitle: '暂无会话', emptySub: '选择一个会话开始聊天', error: '请检查 SDKAppID, userID, userSig, 通过开发人员工具(F12)查看具体的错误信息', loading: '登录中...' }
    : { chats: 'Chats', contacts: 'Contacts', emptyTitle: 'No conversation', emptySub: 'Select a conversation to start chatting', error: 'Please check the SDKAppID, userID, and userSig. View the specific error information through the developer tools (F12).', loading: 'Logging in...'};


  const { status } = useLoginState({
    SDKAppID: 0, // type: number
    userID: '',  // type: string
    userSig: '', // type: string
  })
  const { setActiveConversation } = useConversationListState();

  useEffect(() => {
    async function init() {
      // You can switch to another created userID
      const userID = 'administrator';
      const conversationID = `C2C${userID}`;
      setActiveConversation(conversationID);
    }

    if (status === LoginStatus.SUCCESS) {
      init();
    }
  }, [status]);

  if (status === LoginStatus.ERROR) {
    return (
      <div className="loading-container">
        <div className="loading-spinner"></div>
        <div className="loading-text">{texts.error}</div>
      </div>
    )
  }

  if (status !== LoginStatus.SUCCESS) {
    return (
      <div className="loading-container">
        <div className="loading-spinner"></div>
        <div className="loading-text">{texts.loading}</div>
      </div>
    )
  }

  return (
    <div className="chat-app">
      <ul className="vertical-tabs">
        <li 
          className={`tab-item ${activeTab === 'chats' ? 'active' : ''}`}
          onClick={() => {setActiveTab('chats')}}
        >
          {texts.chats}
        </li>
        <li 
          className={`tab-item ${activeTab === 'contacts' ? 'active' : ''}`}
          onClick={() => {setActiveTab('contacts')}}
        >
          {texts.contacts}
        </li>
      </ul>
      {
        activeTab === 'chats' && (
          <>
            <ConversationList style={{ flex: '0 0 300px'}}/>
            <Chat
              className="chat-box"
              PlaceholderEmpty={
                <div className="empty-chat">
                  <div className="empty-icon">💬</div>
                  <div className="empty-title">{texts.emptyTitle}</div>
                  <div className="empty-subtitle">{texts.emptySub}</div>
                </div>
              }
            >
              <ChatHeader />
              <MessageList />
              <MessageInput />
            </Chat>
          </>
        )
      }
      {
        activeTab === 'contacts' && (
          <>
            <ContactList style={{ flex: '0 0 300px'}}/>
            <ContactInfo
              style={{ flex: '1'}}
              onSendMessage={() => {setActiveTab('chats')}}
              onEnterGroup={() => {setActiveTab('chats')}}
            />
          </>
        )
      }
    </div>
  );
}

export default App;
```


【App.css】
``` css
body {
  margin: 0;
  padding: 20px;
  font-family: Inter, Avenir, Helvetica, Arial, sans-serif;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  min-height: 100vh;
  box-sizing: border-box;
}

.chat-app {
  height: calc(100vh - 40px);
  max-width: 1400px;
  margin: 0 auto;
  display: flex;
  flex-direction: row;
  background: #ffffff;
  border-radius: 16px;
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3),
              0 0 0 1px rgba(0, 0, 0, 0.1);
  overflow: hidden;
  backdrop-filter: blur(10px);
}

.vertical-tabs {
  list-style: none;
  margin: 0;
  padding: 0;
  width: 100px;
  background: linear-gradient(180deg, #f8f9fa 0%, #e9ecef 100%);
  border-right: 1px solid rgba(0, 0, 0, 0.08);
}

.tab-item {
  padding: 16px 20px;
  cursor: pointer;
  background: transparent;
  color: #495057;
  font-size: 14px;
  text-align: center;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  position: relative;
}

.tab-item::before {
  content: '';
  position: absolute;
  left: 0;
  top: 50%;
  transform: translateY(-50%);
  width: 3px;
  height: 0;
  background: linear-gradient(180deg, #667eea 0%, #764ba2 100%);
  border-radius: 0 3px 3px 0;
  transition: height 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.tab-item:hover {
  background: rgba(102, 126, 234, 0.08);
  color: #667eea;
}

.tab-item.active {
  background: linear-gradient(90deg, rgba(102, 126, 234, 0.15) 0%, rgba(102, 126, 234, 0.05) 100%);
  color: #667eea;
}

.tab-item.active::before {
  height: 60%;
}

.chat-box {
  flex: 1;
  border-left: 1px solid rgba(0, 0, 0, 0.08);
}

.empty-chat {
  display: flex;
  flex: 1;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100%;
  color: #adb5bd;
  gap: 12px;
  text-align: center;
  border-left: 1px solid rgba(0, 0, 0, 0.08);
}

.empty-icon {
  font-size: 64px;
  opacity: 0.3;
  animation: float 3s ease-in-out infinite;
}

.empty-title {
  font-size: 16px;
  font-weight: 600;
  color: #6c757d;
}

.empty-subtitle {
  font-size: 14px;
  color: #868e96;
}

@keyframes float {
  0%, 100% {
    transform: translateY(0px);
  }
  50% {
    transform: translateY(-10px);
  }
}

.loading-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  gap: 24px;
}

.loading-spinner {
  width: 60px;
  height: 60px;
  border: 4px solid rgba(255, 255, 255, 0.2);
  border-top-color: #ffffff;
  border-radius: 50%;
  animation: spin 1s cubic-bezier(0.68, -0.55, 0.265, 1.55) infinite;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
}

.loading-text {
  color: #ffffff;
  font-size: 18px;
  font-weight: 500;
  letter-spacing: 0.5px;
  animation: pulse 2s ease-in-out infinite;
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

@keyframes pulse {
  0%, 100% {
    opacity: 1;
  }
  50% {
    opacity: 0.6;
  }
}
```

### Step 3: Obtain SDKAppID, UserID and UserSig

In the previously copied `App.tsx` code, the login authentication information is empty. You need to fill in your Tencent Cloud application authentication information in the `useLoginState hook`, as shown below:
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Note</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userID</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >Unique identifier of the user, defined by you, it is allowed to contain only upper and lower case letters (a-z, A-Z), numbers (0-9), underscores, and hyphens.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SDKAppID</td>

<td rowspan="1" colSpan="1" >Number</td>

<td rowspan="1" colSpan="1" >The unique identifier for the audio and video application created in the [Tencent RTC Console](https://console.trtc.io/).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SDKSecretKey</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >The SDKSecretKey of the audio and video application created in the [Tencent RTC Console](https://console.trtc.io/).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userSig</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >A security protection signature used for user log in authentication to confirm the user's identity and prevent malicious attackers from stealing your cloud service usage rights.</td>
</tr>
</table>


> **Explanation of UserSig：**
> 

> **Development environment**: If you are running a demo locally and developing or debugging, you can use the `genTestUserSig` (Refer to Step 3.2) function in the debug file to generate a 'userSig'. In this method, SDKSecretKey is vulnerable to decompilation and reverse engineering. Once your key is leaked, attackers can steal your Tencent Cloud traffic.
> 

> **Production environment**: If your project is going live, please use the [Server-side Generation of UserSig](https://trtc.io/document/34385) method.
> 

1. Log in to  [Chat Console](https://console.trtc.io/) .

2. Click  **Create Application**, enter your application name, then  click  **Create**.


   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027119864/cdc5fdb411ec11efa2935254005ac0ca.png)

3. After creation, you can view the Application Status, service version, SDKAppID, creation time, Tag, and expiration time of the new application on the console overview page.

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027862798/c73f215c7cf411f0914f52540099c741.png)

4. [Go to the user management page](https://console.trtc.io/chat/account-management), create 2–3 test accounts for experience in C2C chat and group chat.

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100033438418/0be64336adb311f096c2525400454e06.png)

5. UserSig info. Click [IM console > development tool > UserSig tool](https://console.trtc.io/usersig), fill in the created userID, and just generate userSig.


### Step 4: Start the Project

Replace SDKAppID, UserID, and UserSig in App.tsx, then run the following command:


【shell】
``` bash
 npm run dev
```

> **Note:**
> 
> 1. Please ensure that in Step 3 code, SDKAppID, UserID, and UserSig are all successfully replaced. Failure to replace them will result in abnormal project behavior.
> 2. A `userID` corresponds to a `userSig`, for more information, see [Generating UserSig](https://trtc.io/document/39074?product=consoleguide).
> 3. If the project fails to start, please check whether the [development environment requirements](https://write.woa.com/document/108053210129276928) are met.


### Step 6: Send your first message

Enter your message in the input box and press Enter to send.

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027119864/efc5e925595711efb36952540075b605.png)

## FAQs

#### What is UserSig?

A UserSig is a password for users to log in to Chat. It is essentially the ciphertext generated by encrypting information such as the UserID.

#### How can I generate a UserSig?

The issuance method for UserSig involves integrating the calculation code of UserSig into your server, and providing an interface oriented towards your project. When UserSig is needed, your project sends a request to the business server to access the dynamic UserSig. For more information, please see [How to Generate a UserSig on the Server](https://trtc.io/document/39074?product=consoleguide).

> **Note:**
> 

> The exemplary code provided in this document retrieves the UserSig by embedding the SECRETKEY in the client code. This approach makes the SECRETKEY highly susceptible to decompilation and reverse engineering. Once your encryption key is compromised, attackers can misappropriate your Tencent Cloud traffic. Hence, **this procedure is exclusively recommended for running functional debugging locally**. For the correct issuance of UserSig, please refer to the previous sections.
> 


## Communication and Feedback

Join the [Telegram Technical Exchange Group](https://t.me/tencent_imsdk) or [WhatsApp Exchange Group](https://chat.whatsapp.com/IVa11ZkVmKTEwSWsAzSyik) to enjoy support from professional engineers and solve your problems.

## Documentation

#### UIKit  Related:
- [chat-uikit-react npm](https://www.npmjs.com/package/@tencentcloud/chat-uikit-react)

- [Demo Source Code and Running Example](https://github.com/TencentCloud/chat-uikit-react)


#### For more features, refer to the ChatEngine API documentation:
- [chat-uikit-engine API Manual](https://web.sdk.qcloud.com/im/doc/chat-engine-lite/index.html)

- [chat-uikit-engine-lite npm](https://www.npmjs.com/package/@tencentcloud/chat-uikit-engine-lite)
