> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

本文对 TUILiveKit Demo 中的**观看页面**进行了详细的介绍，您可以在已有项目中直接参考本文档集成我们开发好的观看页面，也可以根据您的需求按照文档中的内容对页面的样式，布局以及功能项进行深度的定制。

## 功能展示

观看页面提供默认行为和风格，但如果默认行为和样式不能完全满足您的需求，您也可以对 UI 进行自定义。图中显示的数字与特定功能列表中的类别相对应。其中主要包含直播**信息展示、视频直播区域、在线观众、音视频操作、直播时长、画面分辨率切换、全屏功能、聊天互动、消息列表等。**
- **直播视频播放**：高清流畅的直播体验。

- **弹幕互动**：实时弹幕交流。

- **观众列表**：查看在线观众信息。

- **全屏播放**：沉浸式观看体验。

- **H5 移动平台支持**：跨平台兼容。

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027862798/7a848b70e17311f095ab5254001c06ec.png)


## 快速接入

### 步骤1：环境配置及开通服务

在进行快速接入之前，请参考 [准备工作](https://write.woa.com/document/188228825253294080) 集成组件并实现登录。

### 步骤2：安装依赖

您可以选择以下任一方式安装依赖：




【npm】
``` bash
npm install tuikit-atomicx-vue3 @tencentcloud/uikit-base-component-vue3 --save
```


【pnpm】
``` bash
pnpm add tuikit-atomicx-vue3 @tencentcloud/uikit-base-component-vue3
```


【yarn】
``` bash
yarn add tuikit-atomicx-vue3 @tencentcloud/uikit-base-component-vue3
```

### 步骤3：观看页面接入

在您的项目下创建 **live-player.vue **文件，可直接复制如下代码至您的项目中集成**观看页面**。

> **注意：**
> 

> 您可以直接复制如下代码至您的工程中集成示例工程，也可以访问 [观众观看](https://github.com/Tencent-RTC/TUILiveKit/blob/main/Web/web-vite-vue3/src/TUILiveKit/component/LivePlayer/LivePlayerH5.vue) 地址，查看更加详细的源码内容。
> 

``` typescript
<template>
  <UIKitProvider theme="dark">
    <div class="container">
      <!-- 直播核心区域 -->
      <section class="live">
        <header class="header">
          <IconArrowStrokeBack class="back-btn" size="20" />
          <Avatar :src="currentLive?.liveOwner.avatarUrl" :size="32" class="avatar" />
          <span class="user-name">{{ currentLive?.liveOwner.userName || currentLive?.liveOwner.userId }}</span>
        </header>
        <LiveCoreView class="player" />
      </section>

      <div class="sidebar">
        <!-- 在线观众列表 -->
        <section class="audience">
          <header class="section-header">
            <h3> 在线观众 <span>({{ audienceList.length }})</span></h3>
          </header>
          <LiveAudienceList class="list" />
        </section>

        <!-- 消息列表 & 消息输入框 -->
        <section class="barrage">
          <header class="section-header">
            <h3>消息列表</h3>
          </header>
          <BarrageList class="list" />
          <BarrageInput class="input" height="48px" />
        </section>
      </div>
    </div>
  </UIKitProvider>
</template>

<script setup lang="ts">
import { onMounted } from 'vue';
import { LiveAudienceList, BarrageList, BarrageInput, useLiveAudienceState, LiveCoreView, useLiveListState, Avatar, useLoginState } from 'tuikit-atomicx-vue3';
import { UIKitProvider, IconArrowStrokeBack } from '@tencentcloud/uikit-base-component-vue3';

const { audienceList } = useLiveAudienceState();
const { currentLive } = useLiveListState();
const { login, setSelfInfo } = useLoginState();

const liveId = 'live_xxxx'  // 填入您要观看的直播间的ID

async function initLogin() {
  try {
    await login({
      sdkAppId: 0,     // SDKAppID, 可以参考步骤 1 获取
      userId: '',      // UserID, 可以参考步骤 1 获取
      userSig: '',     // userSig, 可以参考步骤 1 获取
    });
  } catch (error) {
    console.error('登录失败:', error);
  }
}

onMounted(async () => {
  await initLogin();
  await setSelfInfo({
    userName: '我的名字/昵称',    // 用户名
    avatarUrl: '',              // 头像 URL 地址
  });
  await joinLive({ liveId });
});

</script>

<style>html,body,#app{height:100%;width:100%;margin:0;padding:0;overflow:hidden}:global(body){font-size:15px;line-height:1.6;text-rendering:optimizeLegibility;}:global(*),:global(*::before),:global(*::after){box-sizing:border-box;margin:0;}.container{display:grid;grid-template-columns:1fr 320px;height:100%;width:100%;gap:16px;padding:16px;background:var(--bg-color-default);box-sizing:border-box;overflow:hidden;}.live{display:flex;flex-direction:column;background:var(--bg-color-operate);border-radius:12px;overflow:hidden;box-shadow:0 2px 8px var(--shadow-color);}.header{display:flex;align-items:center;gap:12px;padding:16px;border-bottom:1px solid var(--stroke-color-primary);}.back-btn{cursor:pointer;color:var(--text-color-tertiary);transition:color 0.2s;}.back-btn:hover{color:var(--text-color-link-hover);}.avatar{border:1px solid var(--uikit-color-white-7);}.user-name{color:var(--text-color-primary);font-weight:500;}.player{flex:1;background:var(--uikit-color-black-1);min-height:0;}.sidebar{display:flex;flex-direction:column;gap:16px;height:100%;overflow:hidden;}.audience{display:flex;flex-direction:column;background:var(--bg-color-operate);border-radius:12px;overflow:hidden;box-shadow:0 2px 8px var(--shadow-color);flex:1;min-height:0;}.barrage{display:flex;flex-direction:column;background:var(--bg-color-operate);border-radius:12px;overflow:hidden;box-shadow:0 2px 8px var(--shadow-color);flex:1;min-height:0;}.section-header{padding:16px;border-bottom:1px solid var(--stroke-color-primary);background:var(--bg-color-operate);}.section-header h3{margin:0;font-size:16px;font-weight:600;color:var(--text-color-primary);}.section-header span{font-weight:400;color:var(--text-color-secondary);font-size:14px;}.list{flex:1;min-height:0;overflow-y:auto;}.input{border-top:1px solid var(--stroke-color-primary);flex-shrink:0;height:48px;}@media (max-width:1200px){.container{grid-template-columns:1fr;grid-template-rows:60% 20% 20%;gap:12px;}.sidebar{gap:12px;}.audience,.barrage{min-height:200px;}}@media (max-width:768px){.container{padding:8px;gap:8px;grid-template-rows:50% 25% 25%;}.header,.section-header{padding:12px;}.sidebar{gap:8px;}}</style>
```

#### 核心 API 参数说明

##### setSelfInfo

设置用户信息。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >必填</td>

<td rowspan="1" colSpan="1" >说明</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userName</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >是</td>

<td rowspan="1" colSpan="1" >用户昵称，将在直播间及聊天区域显示。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >avatarUrl</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >否</td>

<td rowspan="1" colSpan="1" >用户头像的 URL 地址。</td>
</tr>
</table>


### 步骤4：启动项目

打开终端，进入项目目录，执行以下命令启动项目后，您就可以观看直播了。

> **说明：**
> 

> 上述命令执行成功后，请在浏览器地址栏输入本地访问地址（您可以根据项目配置参考，例如` http://localhost:5173/live-player`，具体端口号可能因您的项目配置而有所不同），即可看到观看页面。
> 

``` bash
npm run dev
```

## 播放直播流

### 步骤1：开启一场直播
- **方式一（推荐）：**


   使用我们提供的 [在线开播网站](https://web.sdk.qcloud.com/trtc/livekit/pusher/index.html#/?fromMark=123471)，开启一场直播来观看，开启后获取直播间 ID

- **方式二：**


   集成我们提供的 [主播开播（Web 桌面浏览器）](https://write.woa.com/document/188483825115738112)，开启一场直播来观看，开启后获取直播间 ID。
   

   > **重要提示：**
   > 

   > 请使用不同的**用户 ID** 开播和观看，否则后登录的设备会强制先登录的设备下线（即“被踢下线”）。
   > 


### 步骤2：观看直播

参考上述快速接入中的 [步骤 3](https://write.woa.com/#c1b852bc-da02-4c9f-bb11-2a63582ce978) 的示例代码，输入对应 `liveId` 后即可进入直播间观看直播：

> **说明：**
> 

> 另外，若您需要修改个人信息，请参考 [步骤 3](https://write.woa.com/#c1b852bc-da02-4c9f-bb11-2a63582ce978) 示例代码中的 `setSelfInfo` 进行个人信息的设置。
> 


### 步骤3：路由配置

由于涉及到直播列表(或首页)到直播间的跳转逻辑，您需要配置 Vue Router。在项目 **src** 目录下新建 **router **文件夹，并创建 **index.ts **文件。然后，在您的主文件（例如 **main.ts** 或 **index.ts**）中引入并使用路由。可参见 [GitHub 上的代码示例](https://github.com/Tencent-RTC/TUILiveKit/blob/main/Web/web-vite-vue3/src/main.ts)，如果需要直播列表，可参见文档 [直播列表](https://write.woa.com/document/185968224430342144)。

> **注意：**
> 

> 如下代码示例中的 `live-player.vue` 文件即代表 [步骤3](https://write.woa.com/#c1b852bc-da02-4c9f-bb11-2a63582ce978) 中创建的示例文件。
> 

``` typescript
// src/router/index.ts
import { createRouter, createWebHistory } from 'vue-router';

const routes = [
  {
    path: '/live-player',
    component: () => import('../live-player.vue'),
  },
  // 如果需要直播列表功能，可添加如下路由，注意以下路径为您项目实际路径
  // {  
    //   path: '/live-list',  
    //   component: () => import('../live-list.vue'),  
  // },
];

const router = createRouter({
  history: createWebHistory(),
  routes,
});
export default router;

// src/main.ts
import { createApp } from 'vue';
import App from './App.vue';
import router from './router';

const app = createApp(App);
app.use(router);
app.mount('#app');
```

## 自由定制

### 颜色主题及语言

通过配置 `App.vue` 中 `UIKitProvider` 的入参，修改主题及语言的默认值。
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

<td rowspan="1" colSpan="1" >-</td>
</tr>
</table>

``` typescript
<UIKitProvider theme="light">
  <router-view />
</UIKitProvider>
 
<script setup lang="ts">
import { UIKitProvider } from '@tencentcloud/uikit-base-component-vue3';
```

### 按钮 Button 和图标 Icon

若您需要对按钮 Button 或图标 Icon 等其他控件进行新增或替换等 UI 定制，您可以通过如下方式实现，以`live-player.vue `文件中的按钮和图标为例，您可以参考下图找到对应按钮或图标的指定位置源码，对当前部分的控件进行**增加、删除、替换**等 UI 定制操作。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027862798/768281cfe17311f0a5a25254007c27c5.png)


根据上述示例，我们同样支持您根据项目需求对**观众观看页面**进行 UI 定制的能力。除了页面 UI 布局调整，我们也支持您对**颜色主题、字体、圆角、按钮、图标、输入框、弹框等**内容进行**增加、删除、修改**等操作，满足您的 UI 定制需要。
<table>
<tr>
<td rowspan="1" colSpan="1" >**类别**</td>

<td rowspan="1" colSpan="1" >**功能**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**素材管理**</td>

<td rowspan="1" colSpan="1" >自定义素材管理区域展示</td>

<td rowspan="1" colSpan="1" >支持调整 Icon 的大小、颜色或对 Icon 进行替换。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**直播工具**</td>

<td rowspan="1" colSpan="1" >自定义直播工具信息展示</td>

<td rowspan="1" colSpan="1" >支持调整 Icon 的大小、颜色或对 Icon 进行替换。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**在线观众**</td>

<td rowspan="1" colSpan="1" >自定义观众信息展示</td>

<td rowspan="1" colSpan="1" >**支持：**<br>- 展示/隐藏观众等级。<br>- 观众信息字体、颜色 UI 自定义设置。<br>- 替换为您需要的 Icon 风格。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**消息列表**</td>

<td rowspan="1" colSpan="1" >自定义消息弹幕区域展示</td>

<td rowspan="1" colSpan="1" >**支持：**<br>- 展示/隐藏聊天输入区域。<br>- 支持 UI 定制聊天气泡风格、定制观众等级等内容。</td>
</tr>
</table>


## 常见问题

### 浏览器自动播放限制

出于用户体验考虑，现代浏览器对网页自动播放（autoplay）功能实施了限制性策略：所有带声音的媒体内容必须经过用户主动交互（例如点击或触摸）后才能播放。这项限制主要是为了防止网站在用户未明确同意的情况下突然播放音频，避免对用户造成干扰。大多数浏览器都不限制无声视频的自动播放，但是在低电量模式下的 iOS Safari 浏览器中以及开启了自定义自动播放限制的 iOS WKWebView 中（例如 iOS 微信浏览器），无声视频的自动播放也会受到限制。

#### 自动播放失败表现

当用户对该站点的媒体互动指数（MEI, Media Engagement Index）未达到阈值时，企图自动播放有声视频会失败。在 SDK 默认情况下，当检测到自动播放失败时，会弹窗引导用户与页面产生交互（例如点击**确认**按钮）。产生交互后，浏览器策略即被满足，有声视频即可正常播放。

#### 解决方案：自定义处理自动播放失败

如果您希望自定义自动播放失败时的交互体验（例如替换默认的弹窗 UI），可以通过监听 SDK 抛出的 `onAutoplayFailed` 回调来实现。以下是在 Vue3 项目中，通过监听事件并弹出自定义对话框的实现代码示例：
``` java
import TUIRoomEngine, { TUIRoomEvents } from '@tencentcloud/tuiroom-engine-js';
import { useUIKit, TUIMessageBox } from '@tencentcloud/uikit-base-component-vue3';
import { useRoomEngine } from 'tuikit-atomicx-vue3';

const roomEngine = useRoomEngine();

let isShowAutoPlayDialog = false;

export default function useCustomizedAutoPlayDialog() {
  const { t } = useUIKit();
  TUIRoomEngine.once('ready', () => {
    roomEngine.instance?.on(TUIRoomEvents.onAutoPlayFailed, () => {
      if (!isShowAutoPlayDialog) {
        isShowAutoPlayDialog = true;
        TUIMessageBox.alert({
          title: t('RoomCommon.Attention'),
          content: t('RoomNotifications.AudioPlaybackFailed'),
          showClose: false,
          modal: false,
          confirmText: t('Confirm'),
          callback: () => {
            isShowAutoPlayDialog = false;
          },
        });
      }
    });
  });
}

export { useCustomizedAutoPlayDialog };
```

> **说明：**
> 

> 您需要安装对应的 `@tencentcloud/tuiroom-engine-js。`
> 


## 下一步

恭喜您，现在您已经成功集成了观众观看。接下来，您可以继续接入 **直播列表、UI 自定义**和**监播**等功能：
<table>
<tr>
<td rowspan="1" colSpan="1" >**功能**</td>

<td rowspan="1" colSpan="1" >**描述**</td>

<td rowspan="1" colSpan="1" >**集成指引**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >直播列表</td>

<td rowspan="1" colSpan="1" >展示直播列表界面和功能，包含直播列表和房间信息展示功能。</td>

<td rowspan="1" colSpan="1" >[直播列表（Web Vue3）](https://write.woa.com/document/185968224430342144)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >UI 自定义</td>

<td rowspan="1" colSpan="1" >更详细的 UI 组件自定义指引。</td>

<td rowspan="1" colSpan="1" >[概述](https://write.woa.com/document/177815913198854144)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Web 监播</td>

<td rowspan="1" colSpan="1" >运营平台，支持直播间管控。</td>

<td rowspan="1" colSpan="1" >[Web 监播页（Web Vue3）](https://write.woa.com/document/185222048061181952)</td>
</tr>
</table>
