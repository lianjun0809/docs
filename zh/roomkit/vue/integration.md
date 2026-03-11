> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

TUIRoomKit 是腾讯云推出的音视频房间 UI 应用。本次升级引入了全新的原子化组件接入方案，开发者可以灵活组合这些原子化组件，以构建个性化的音视频房间界面。

> **推荐使用更高效的 AI 集成助手**
> 

> 我们为您提供了全新的 AI 集成方式，只需要描述您的需求，即可自动生成集成代码，大幅提升开发效率。
> 

> [点击这里，立即体验 AI 集成](https://cloud.tencent.com/document/product/647/127873)
> 


本文档介绍如何将 TUIRoomKit 集成到现有的 Vue3 项目中，同时介绍如何对 TUIRoomKit 的样式、布局及功能进行自定义修改。
- 桌面端多人会议

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027337918/31045da2d73111f097cb5254005ef0f7.png)

- H5 多人会议

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027337918/1d8af2f1fd3611f0b5c0525400380f7d.png)


## 前提条件

### 开通服务

请参考 [开通服务](https://cloud.tencent.com/document/product/647/104842) 领取 TUIRoomKit 体验版，并在 [应用管理](https://console.cloud.tencent.com/trtc) 页面获取以下信息:
- **SDKAppID**: 应用标识，腾讯云基于 `SDKAppID` 完成计费统计。

- **SDKSecretKey**: 应用密钥，用于初始化配置文件的密钥信息。


### 环境准备
- **Node.js**: ≥ 18.19.1 (推荐使用官方 LTS 版本)。

- **Vue**: ≥ 3.4.21。

- **现代浏览器**：支持 [WebRTC APIs](https://cloud.tencent.com/document/product/647/17249#.E6.94.AF.E6.8C.81.E7.9A.84.E5.B9.B3.E5.8F.B0) 的现代浏览器。

- **设备**：摄像头、麦克风、扬声器。


## 源码接入

### 步骤1：安装项目依赖

在您的业务项目中安装以下依赖。




【npm】
``` bash
npm install @tencentcloud/roomkit-web-vue3@latest tuikit-atomicx-vue3 @tencentcloud/uikit-base-component-vue3 @tencentcloud/universal-api 
```


【pnpm】
``` bash
pnpm install @tencentcloud/roomkit-web-vue3@latest tuikit-atomicx-vue3 @tencentcloud/uikit-base-component-vue3 @tencentcloud/universal-api
```


【yarn】
``` bash
yarn add @tencentcloud/roomkit-web-vue3@latest tuikit-atomicx-vue3 @tencentcloud/uikit-base-component-vue3 @tencentcloud/universal-api
```

### 步骤2：**引用 **TUIRoomKit** 组件**
``` typescript
<template>
  <ConferenceMainView v-if="isPC"></ConferenceMainView>
  <ConferenceMainViewH5 v-else></ConferenceMainViewH5>
</template>
<script setup>
import { ref } from 'vue';
import { ConferenceMainView, ConferenceMainViewH5 } from '@tencentcloud/roomkit-web-vue3';
import { getPlatform } from '@tencentcloud/universal-api';

const isPC = ref(getPlatform() === 'pc');
</script>

```

### 步骤3：配置 App.vue 文件

将以下内容合并到项目的 App.vue 文件中，以配置全局 UI 样式和用户登录逻辑：
- 配置全局 `UIKitProvider`：引入 `UIKitProvider` 组件，并设置默认主题和语言；

- 用户登录： 在 `onMounted` 钩子中执行 `login` 和 `setSelfInfo`；

   ``` typescript
   <template>
     <!-- Step 1: 配置全局 UIKitProvider -->
     <UIKitProvider theme="light" language="zh-CN">
       <!-- 您包含 ConferenceMainView 的业务组件 -->
     </UIKitProvider>
   </template>
    
   <script setup>
   import { UIKitProvider } from '@tencentcloud/uikit-base-component-vue3';
   import { onMounted } from 'vue';
   import { useLoginState } from 'tuikit-atomicx-vue3/room';
   
   // step 2: 用户登陆
   const { login, setSelfInfo } = useLoginState();
   const SDKAppID = 0;    // 注意：请替换为实时音视频控制台获取的 SDKAppID 信息
   const userId = '填入您真实的 userId';    // 注意：请替换为真实的 userId
   const userName = '填入您真实的 userName';  // 注意：请替换为真实的 userName
   const userSig = '填入您真实的 userSig';    // 注意：生成临时 userSig 请参考 https://cloud.tencent.com/document/product/647/17275#console
   onMounted(async () => {
     try {
       await login({
         userId,
         userSig,
         sdkAppId: SDKAppID,
       });
       await setSelfInfo({
         userName,
         avatarUrl: '',
       });
     } catch (error: any) {
       console.error('Login failed:', error);
     }
   });
   </script>
   
   <!-- Step 3: 配置全局样式（此样式用来覆盖脚手架搭建的新项目的默认样式，可按需配置）-->
   <style>
   html, body {
     padding: 0 !important;
     margin: 0 !important;
   }
   
   #app {
     width: 100% !important;
     height: 100% !important;
     padding: 0 !important;
     margin: 0 !important;
     max-width: 100% !important;
     max-height: 100% !important;
     text-align: left !important;
     overflow: hidden;
   }
   </style>
   ```

### 步骤4：发起新的会议

会议主持人可以通过调用 `conference.start`  接口来发起一场新的会议，其他参会者可以参见 [步骤6](https://write.woa.com/#061c9593-1112-4763-aff2-7289b3af0c41) 的描述，调用 `conference.join` 接口加入该会议。

> **注意：**
> 

> 请参考步骤 3 在用户登录成功后调用 `conference.start `接口发起会议。
> 

``` typescript
import { conference } from '@tencentcloud/roomkit-web-vue3';
const startConference = async () => {  
  await conference.start({
    roomId: '123456',   // 请替换为您真实的 roomId
    options: {
      roomName: '我的临时会议',
    },
  });
}
startConference();
```

### 步骤5：进入已有会议

参与者可以通过调用 `conference.join` 接口，填写对应的 roomId 参数，来加入由会议主持人在 [步骤4](https://write.woa.com/#7e2fb3c2-2b17-4445-985d-4af641ff66be) 中发起的会议。

> **注意：**
> 

> 请参考步骤 3 在用户登录成功后调用 `conference.join `接口加入会议。
> 

``` typescript
import { conference } from '@tencentcloud/roomkit-web-vue3';
const joinConference = async () => {
  await conference.join({
    roomId: '123456',   // 请替换为您真实的 roomId
  });
}
joinConference();
```

## 启动项目




【npm】
``` bash
npm run dev
```


【pnpm】
``` bash
pnpm run dev
```


【yarn】
``` bash
yarn run dev
```

启动成功后，请在浏览器中打开调试地址（通常为 http://localhost:5173）访问应用。您将看到如下所示的会议界面：

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027337918/7986ed3bfd3711f098c8525400370dda.png)


## UI 快速自定义

### 主题及语言

通过配置 App.vue 中 `UIKitProvider` 的入参，修改主题及语言的默认值。
<table>
<tr>
<td rowspan="1" colSpan="1" >UIKitProvider 参数</td>

<td rowspan="1" colSpan="1" >可选值</td>

<td rowspan="1" colSpan="1" >默认值</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >theme</td>

<td rowspan="1" colSpan="1" >"light" \| "dark"</td>

<td rowspan="1" colSpan="1" >"light"</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >language</td>

<td rowspan="1" colSpan="1" >"zh-CN" \| "en-US"</td>

<td rowspan="1" colSpan="1" >"en-US"</td>
</tr>
</table>

``` typescript
<UIKitProvider theme="light" language="zh-CN">
  <router-view />
</UIKitProvider>
 
<script setup lang="ts">
import { UIKitProvider } from '@tencentcloud/uikit-base-component-vue3';
```

### 配置用户联系人列表

TUIRoomKit 预定会议用户选择列表和会中呼叫用户选择列表默认展示用户关系链列表，批量导入用户关系链请参考以下步骤：

步骤1：使用 [账号管理 > 导入多个账号](https://cloud.tencent.com/document/product/269/4919) REST API 接口批量导入用户账号；

步骤2：使用 [好友管理 > 导入好友](https://cloud.tencent.com/document/product/269/8301) REST API 接口批量导入用户关系链；

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027337918/c8e55003fd8611f08080525400074c32.png)


## TUIRoomKit 界面定制

### 源码导出



【Vue3】
1. 执行源码导出脚本，默认拷贝路径为 `./src/components/RoomKit`

``` bash
  node ./node_modules/@tencentcloud/roomkit-web-vue3/scripts/eject.js
```
2. 根据脚本提示确认是否要将 TUIRoomKit 源码拷贝到 `./src/components/RoomKit` 目录。如您需要自定义拷贝目录请输入 'y', 否则输入'n'。


![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027337918/05a672b6fd8711f0a1eb52540073fd3b.png)

3. 源码导出后，在您指定的项目路径中会新增 TUIRoomKit 源码。此时，您需要手动将 ConferenceMainView 组件，ConferenceMainViewH5 组件的 conference 对象的引用从 npm 包地址更改为 TUIRoom 源码的相对路径地址。

``` typescript
- import { ConferenceMainView, conference } from '@tencentcloud/roomkit-web-vue3';
// 替换引用路径为 TUIRoomKit 源码的真实路径
+ import { ConferenceMainView, ConferenceMainViewH5, conference } from './components/RoomKit/index.ts';
```
4. 配置 ESLint 校验


如果您导出 TUIRoomKit 源码后运行项目出现 ESLint 报错，您可以在`.eslintignore`文件中添加 RoomKit 文件夹忽略 ESLint 检测。
``` javascript
// 请替换为 TUIRoomKit 源码真实路径
src/components/RoomKit
```

### 自定义房间流布局

TUIRoomKit 目前支持九宫格、侧边栏及顶部栏三种流布局，默认为九宫格布局。
``` typescript
// RoomKit/views/ConferenceMainView/index.vue
import { RoomLayoutTemplate } from 'tuikit-atomicx-vue3/room';
// 修改默认视频流布局为侧边栏布局
const participantViewLayout = ref(RoomLayoutTemplate.SidebarLayout);
function handleLayoutUpdate(layout: RoomLayoutTemplate) {
  participantViewLayout.value = layout;
}

// 修改默认视频流布局为顶部栏布局
const participantViewLayout = ref(RoomLayoutTemplate.CinemaLayout);
function handleLayoutUpdate(layout: RoomLayoutTemplate) {
  participantViewLayout.value = layout;
}
```

### 自定义视频流挂件

TUIRoomKit 默认视频流挂件如图所示，如需自定义视频流挂件请修改 `RoomKit/components/RoomLayoutView/ParticipantViewUI/ParticipantViewUI.vue` 组件。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027337918/2fab38f2d73111f0929b525400bf7822.png)


## 常见问题

#### **TUIRoomKit 在本地开发时使用正常，但部署到线上环境后无法**正常采集用户的摄像头或麦克风设备**？**
- **原因分析：**浏览器出于安全和隐私保护的考虑，对音视频设备（麦克风、摄像头）的采集有着严格限制。只有在安全环境下，采集操作才会被允许。安全环境协议包括：https://、localhost、file:// 等。HTTP 协议被视为不安全，浏览器会默认禁止访问媒体设备。

- **解决方案：**若您在本地（localhost）测试一切正常，但部署后出现采集失败，请立即检查您的网页是否部署在 HTTP 协议上。您必须使用 HTTPS 协议部署您的网页，并确保具备有效的安全证书。

- **相关资源：**更多关于 URL 域名及协议的限制详情，请参见 [URL 域名及协议限制说明](https://cloud.tencent.com/document/product/647/17249#URL-.E5.9F.9F.E5.90.8D.E5.8D.8F.E8.AE.AE.E9.99.90.E5.88.B6)。


#### **TUIRoomKit 是否支持使用 iframe 集成?**

支持。使用 iframe 集成 TUIRoomKit 时, 需要在 iframe 标签中配置 allow 属性以授予必要的浏览器权限（麦克风、摄像头、屏幕共享、全屏等），示例如下: 
``` typescript
// 开启麦克风、摄像头、屏幕分享、全屏权限
<iframe allow="microphone; camera; display-capture; display; fullscreen;">
```

#### TUIRoomKit 是否支持设置内网代理？

支持。请参考如下指引设置内网代理参数。更多内网代理信息请参考 [应对防火墙受限](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-34-advanced-proxy.html)。
``` typescript
// 请在进房前设置内网代理参数
import TUIRoomEngine from '@tencentcloud/tuiroom-engine-js';
import { useRoomEngine } from 'tuikit-atomicx-vue3/room';
const { roomEngine } = useRoomEngine();

TUIRoomEngine.once('ready', () => {
  const trtcCloud = roomEngine.instance?.getTRTCCloud();
  trtcCloud.callExperimentalAPI(JSON.stringify({
    api: 'setNetworkProxy',
    params: {
      websocketProxy: "wss://proxy.example.com/ws/",
      turnServer: [{
        url: '14.3.3.3:3478',
        username: 'turn',
        credential: 'turn',
      }],
      iceTransportPolicy: 'relay',
    },
  }));
});
```

## 联系我们

如果您在接入或使用过程有任何疑问或者建议，欢迎 [联系我们](https://cloud.tencent.com/document/product/269/59590) 提交反馈。
