> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

## 概述

本文对 TUILiveKit Demo 中的**直播列表页面**进行了详细的介绍，您可以在已有项目中直接参考本文档集成我们开发好的直播列表页面，也可以根据您的需求按照文档中的内容对页面的样式，布局以及功能项进行深度的定制。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027862798/f73d96db8c8611f0ae9d5254001c06ec.png)


## 快速体验

您可以在 [在线体验](https://write.woa.com/document/193874503063744512) 中使用 [在线开播网站](https://web.sdk.qcloud.com/trtc/livekit/pusher/index.html#/?fromMark=123016) 快速开启一场直播，同时您也可以使用 [在线观看网站](https://web.sdk.qcloud.com/trtc/livekit/player/index.html#/?fromMark=123016) 来查看账户下直播列表。

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

### 步骤3: 直播列表页面接入

在您的项目下创建 **live-list.vue **文件，可直接复制如下代码至您的项目中集成**直播列表页面**。

> **注意：**
> 

> 您可以直接复制如下代码至您的工程中集成示例工程，也可以访问 [直播列表](https://github.com/Tencent-RTC/TUILiveKit/blob/main/Web/web-vite-vue3/src/TUILiveKit/LiveListView.vue) 地址，查看更加详细的源码内容。
> 

``` typescript
<template>
  <UIKitProvider theme="dark">
    <div class="container">
      <header class="header">
        <h1 class="title">在线直播</h1>
      </header>
      <main class="main">
        <LiveList /> 
      </main>
    </div>
  </UIKitProvider>
</template>

<script setup lang="ts">
import { onMounted } from 'vue';
import { LiveList, useLoginState } from 'tuikit-atomicx-vue3';
import { UIKitProvider } from '@tencentcloud/uikit-base-component-vue3';

const { login } = useLoginState();

async function initLogin() {
  try {
    await login({
      sdkAppId: 0,        // SDKAppID, 可以参考步骤 1 获取
      userId: '',         // UserID, 可以参考步骤 1 获取
      userSig: '',        // userSig, 可以参考步骤 1 获取
    });
  } catch (error) {
    console.error('登录失败:', error);
  }
}

onMounted(async () => {
  await initLogin();
});
</script>

<style scoped>:global(*),:global(::after),:global(::before){box-sizing:border-box;margin:0}.container{display:flex;flex-direction:column;height:100vh;width:100vw;background:var(--bg-color-default)}.header{display:flex;align-items:center;flex-shrink:0}.title{margin:0;font-size:16px;font-weight:600;color:var(--text-color-primary);letter-spacing:-.5px}.main{flex:1;padding:24px;overflow-y:auto;min-height:0}</style>
```

> **注意：**
> 

> 若您需要实现直播列表到进入直播间的跳转逻辑，可参考本文中 [指定直播间](https://write.woa.com/#61f1bbc9-1f23-4b69-aceb-7ab3f35a0ec2) 部分内容。
> 


## 启动项目

### 开启您的直播列表页面

通过下列命令启动成功后，通过访问本地地址打开直播列表页面。

> **说明：**
> 

> 上述命令执行成功后，请在浏览器地址栏输入本地访问地址（您可以根据项目参考，例如` http://localhost:5173/live-list`，具体端口号可能因您的项目配置而有所不同），即可看到直播列表页面。
> 

``` bash
  npm run dev
```

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027862798/dbeb808be58811f0a4ee52540044a08e.png)


### 指定直播间

由于涉及到直播列表(或首页)到观看页面的跳转逻辑，您需要配置 Vue Router 来实现页面跳转 。您可以在项目 `src` 目录下新建 `router` 文件夹，并创建 `index.ts` 文件。然后，在您的主文件（例如 **main.ts **或 **index.ts**）中引入并使用路由。可参见 [GitHub 代码示例](https://github.com/Tencent-RTC/TUILiveKit/blob/main/Web/web-vite-vue3/src/main.ts)。

#### 步骤1：配置页面路由

请配置您的 Vue Router，将`live-list.vue` 映射到直播列表页面。

> **注意：**
> 
> - 如果您的业务项目中已有 `src/router/index.ts` 文件，请将以下内容合并到已有代码中。
> - 如果尚未配置路由，请新建 `src/router/index.ts` 文件并添加以下配置。

``` typescript
import { createRouter, createWebHistory } from 'vue-router';

const routes = [
  {
    // 直播列表页面, 注意以下代码路径为您项目实际路径
    path: '/live-list',
    component: () => import('../live-list.vue'),
  },  
  // 若您需要实现通过点击直播列表直播间封面到对应直播间进行观看，则需要参考如下示例配置观看页面的路由
  {
    // 路由跳转至观看页面, 注意以下代码路径为您项目实际路径
    path: '/live-player',
    component: () => import('../live-player.vue'),
  },
];

const router = createRouter({
  history: createWebHistory(),
  routes,
});
export default router;

```

#### 步骤2：配置 src/main.ts 文件

将路由和多语言配置合并到您项目中的入口文件 src/main.ts 中：
``` java
// src/main.ts
import { createApp } from 'vue';
import App from './App.vue';
import router from './router';

const app = createApp(App);
app.use(router);
app.mount('#app');
```

#### 步骤3：配置 live-list 文件

您需要将以下内容合并到上文中的 [步骤3](https://write.woa.com/#c1b852bc-da02-4c9f-bb11-2a63582ce978) 内容中，进行直播列表到观看页面的跳转。
``` typescript
// live-list.vue 可增量添加至您的代码中
<template>
  <UIKitProvider>
     // .....省略部分参考快速接入步骤 3 部分
     <LiveList @live-room-click="handleLiveRoomClick" />
  </UIKitProvider>
</template>

<script setup lang="ts">
import { useRouter, useRoute } from 'vue-router';

const router = useRouter();
const route = useRoute();

function handleLiveRoomClick(liveInfo: LiveInfo) {
  if (liveInfo?.liveId) {
    router.push({ path: '/live-player', query: { ...route.query, liveId: liveInfo.liveId } });
  }
}

</script>
```

## 自由定制

根据上述功能展示图，我们也支持您根据项目需求对直播列表页面进行 UI 定制。主要可供定制的能力如下表所示。
<table>
<tr>
<td rowspan="1" colSpan="1" >**类别**</td>

<td rowspan="1" colSpan="1" >**功能**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**直播间列表**</td>

<td rowspan="1" colSpan="1" >自定义直播间列表区域展示</td>

<td rowspan="1" colSpan="1" >**支持：**<br>- **直播间信息文字 展示/隐藏、UI 进行定制。**<br>- **直播间一行/一列展示固定数量定制。**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**个人信息**</td>

<td rowspan="1" colSpan="1" >自定义个人信息展示</td>

<td rowspan="1" colSpan="1" >**支持：**<br>- **展示/隐藏个人信息。**<br>- **个人信息字体、颜色 UI 自定义设置。**</td>
</tr>
</table>


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

### 按钮 Button 和 图标 Icon

您可以对按钮、图标等控件进行自定义。以` live-list.vue` 为例，对` Button`、`Icon` 控件执行增删改等操作都可以满足您的自定义需求。除布局调整外，我们还支持对颜色、字体、圆角以及输入框、弹框等内容进行全面修改，充分满足您的 UI 定制需求。
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

<td rowspan="1" colSpan="1" >支持：<br>- 展示/隐藏观众等级。<br>- 观众信息字体、颜色 UI 自定义设置。<br>- 替换为您需要的 Icon 风格。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**消息列表**</td>

<td rowspan="1" colSpan="1" >自定义消息弹幕区域展示</td>

<td rowspan="1" colSpan="1" >支持：<br>- 展示/隐藏聊天输入区域。<br>- 支持 UI 定制聊天气泡风格、定制观众等级等内容。</td>
</tr>
</table>


### 设置昵称及头像

如果您需要自定义昵称或头像，可以在 [步骤 3](https://write.woa.com/#c1b852bc-da02-4c9f-bb11-2a63582ce978) 中的示例代码中通过 [setSelfInfo](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setSelfInfo) 进行设置，具体示例如下：
``` typescript
import { useLoginState } from 'tuikit-atomicx-vue3';

const { setSelfInfo } = useLoginState();

// 设置用户个人信息
await setSelfInfo({
  userName: '张三',
  avatarUrl: 'https://example.com/avatar.png',
});
```

## 下一步

恭喜您，现在您已经成功集成了**直播列表页面**。接下来，您可以实现**主播开播页**、**观众观看页**和 **UI 自定义**等内容，可参考下表：
<table>
<tr>
<td rowspan="1" colSpan="1" >**功能**</td>

<td rowspan="1" colSpan="1" >**描述**</td>

<td rowspan="1" colSpan="1" >**集成指引**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**观众观看**</td>

<td rowspan="1" colSpan="1" >实现观众进入主播的直播间后观看直播，实现观众连麦 、直播间信息、在线观众、弹幕显示等功能。</td>

<td rowspan="1" colSpan="1" >[观众观看（Web Vue3）](https://write.woa.com/document/185968222948704256)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**主播开播**</td>

<td rowspan="1" colSpan="1" >主播在当前页面开始直播及相关设置。</td>

<td rowspan="1" colSpan="1" >[主播开播（Web Vue3）](https://write.woa.com/document/188483825115738112)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**UI 自定义**</td>

<td rowspan="1" colSpan="1" >更详细的 UI 组件自定义指引。</td>

<td rowspan="1" colSpan="1" >[UI 自定义](https://write.woa.com/document/177815913198854144)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**Web 监播**</td>

<td rowspan="1" colSpan="1" >运营平台，支持直播间管控。</td>

<td rowspan="1" colSpan="1" >[监播页面（Web Vue3）](https://write.woa.com/document/185222048061181952)</td>
</tr>
</table>
