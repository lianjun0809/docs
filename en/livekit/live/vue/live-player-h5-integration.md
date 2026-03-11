> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/en/llms.txt
> Use this file to discover all available pages before exploring further.

This guide provides a comprehensive overview of the **Viewer Page** in the TUILiveKit Demo. Use this documentation to quickly integrate our pre-built viewer page into your project, or leverage the details here to fully customize its style, layout, and features to fit your specific needs.

## Feature Overview

The viewer page comes with default functionality and styling out of the box. If these defaults don’t match your requirements, you can easily tailor the UI. The numbers in the screenshot map to the main feature categories. Core features include: **stream information display, live video area, online audience, audio/video controls, live duration, resolution switching, fullscreen mode, chat interaction, and message list**.
- **Live Video Playback**: High-definition, low-latency streaming.

- **Live Comments Interaction**: Real-time live comments for audience engagement.

- **Audience List**: View details about online audience members.

- **Fullscreen Playback**: Immersive viewing experience.

- **H5 Mobile Platform Support**: Works seamlessly across platforms.

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027862798/5f6d6051e63211f0ae695254001d6acc.png)


## Quick Integration

### Step 1: Environment Setup and Activate the Service

Before you begin, see [Preparation](https://write.woa.com/document/163673134112337920) for instructions on integrating required components and implementing login.

### Step 2: Install Dependencies

Install the necessary packages using your preferred package manager:




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

### Step 3: Integrate Viewer Page

Create a `live-player.vue` file in your project. Copy and paste the following code to add the **viewer page**.

> **Note：**
> 

> You can use the code below directly, or refer to [Audience Viewing](https://github.com/Tencent-RTC/TUILiveKit/blob/main/Web/web-vite-vue3/src/TUILiveKit/component/LivePlayer/LivePlayerPC.vue) for the full source.
> 

``` typescript
<template>
  <UIKitProvider theme="dark">
    <div class="container">
      <!-- Live Core Area -->
      <section class="live">
        <header class="header">
          <IconArrowStrokeBack class="back-btn" size="20" />
          <Avatar :src="currentLive?.liveOwner.avatarUrl" :size="32" class="avatar" />
          <span class="user-name">{{ currentLive?.liveOwner.userName || currentLive?.liveOwner.userId }}</span>
        </header>
        <LiveCoreView class="player" />
      </section>

      <div class="sidebar">
        <!-- Online Audience List -->
        <section class="audience">
          <header class="section-header">
            <h3> Online Audience <span>({{ audienceList.length }})</span></h3>
          </header>
          <LiveAudienceList class="list" />
        </section>

        <!-- Message List & Input Box -->
        <section class="barrage">
          <header class="section-header">
            <h3>Message List</h3>
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

const liveId = 'live_xxxx'  // Enter the ID of the live stream you want to watch

async function initLogin() {
  try {
    await login({
      sdkAppId: 0,     // SDKAppID, refer to Step 1 for details
      userId: '',      // UserID, refer to Step 1 for details
      userSig: '',     // userSig, refer to Step 1 for details
    });
  } catch (error) {
    console.error('Login failed:', error);
  }
}

onMounted(async () => {
  await initLogin();
  await setSelfInfo({
    userName: 'Your Name/Nickname',    // Username
    avatarUrl: '',                     // Avatar URL
  });
  await joinLive({ liveId });
});

</script>

<style>html,body,#app{height:100%;width:100%;margin:0;padding:0;overflow:hidden}:global(body){font-size:15px;line-height:1.6;text-rendering:optimizeLegibility;}:global(*),:global(*::before),:global(*::after){box-sizing:border-box;margin:0;}.container{display:grid;grid-template-columns:1fr 320px;height:100%;width:100%;gap:16px;padding:16px;background:var(--bg-color-default);box-sizing:border-box;overflow:hidden;}.live{display:flex;flex-direction:column;background:var(--bg-color-operate);border-radius:12px;overflow:hidden;box-shadow:0 2px 8px var(--shadow-color);}.header{display:flex;align-items:center;gap:12px;padding:16px;border-bottom:1px solid var(--stroke-color-primary);}.back-btn{cursor:pointer;color:var(--text-color-tertiary);transition:color 0.2s;}.back-btn:hover{color:var(--text-color-link-hover);}.avatar{border:1px solid var(--uikit-color-white-7);}.user-name{color:var(--text-color-primary);font-weight:500;}.player{flex:1;background:var(--uikit-color-black-1);min-height:0;}.sidebar{display:flex;flex-direction:column;gap:16px;height:100%;overflow:hidden;}.audience{display:flex;flex-direction:column;background:var(--bg-color-operate);border-radius:12px;overflow:hidden;box-shadow:0 2px 8px var(--shadow-color);flex:1;min-height:0;}.barrage{display:flex;flex-direction:column;background:var(--bg-color-operate);border-radius:12px;overflow:hidden;box-shadow:0 2px 8px var(--shadow-color);flex:1;min-height:0;}.section-header{padding:16px;border-bottom:1px solid var(--stroke-color-primary);background:var(--bg-color-operate);}.section-header h3{margin:0;font-size:16px;font-weight:600;color:var(--text-color-primary);}.section-header span{font-weight:400;color:var(--text-color-secondary);font-size:14px;}.list{flex:1;min-height:0;overflow-y:auto;}.input{border-top:1px solid var(--stroke-color-primary);flex-shrink:0;height:48px;}@media (max-width:1200px){.container{grid-template-columns:1fr;grid-template-rows:60% 20% 20%;gap:12px;}.sidebar{gap:12px;}.audience,.barrage{min-height:200px;}}@media (max-width:768px){.container{padding:8px;gap:8px;grid-template-rows:50% 25% 25%;}.header,.section-header{padding:12px;}.sidebar{gap:8px;}}</style>
```

#### Core API Parameters

##### setSelfInfo

Configure user information.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Required</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userName</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >Yes</td>

<td rowspan="1" colSpan="1" >User nickname, shown in the live room and chat area.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >avatarUrl</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >No</td>

<td rowspan="1" colSpan="1" >URL of the user's avatar image.</td>
</tr>
</table>


### Step 4: Start the Project

Open your terminal, navigate to your project directory, and run the following command to launch the project. You’ll then be able to view the live stream.

> **Note：**
> 

> After the command runs successfully, enter your local access URL in your browser (for example, `http://localhost:5173/live-player`; the port may vary based on your setup) to access the viewer page.
> 

``` bash
npm run dev
```

## Play Live Stream

### Step 1: Start a Live Stream
- **Method 1 (Recommended):**


   Use our [Online Hosting Website](https://web.sdk.qcloud.com/trtc/livekit/pusher/index.html) to start a live stream. After starting, copy the live stream room ID.

- **Method 2:**


   Integrate our [Host Streaming (Web Desktop Browser)](https://write.woa.com/document/194114399449153536) to start a live stream. After starting, copy the live stream room ID.
   

   > **Important Tip:****：**
   > 

   > Use different **userID** for hosting and viewing. If the same user ID logs in on multiple devices, the later login will force the earlier device offline (**kick offline**).
   > 


### Step 2: Watch the Live Stream

Refer to the sample code from [Step 3](https://write.woa.com/#7aa32d79-4ed2-4b61-8371-c43549be5e43) of Quick Integration. Enter the corresponding `liveId` to join the live room and view the stream.

### Step 3: Router Configuration

To enable navigation from the Live Stream List or homepage to the live room, configure Vue Router. In your project’s **src** directory, create a **router** folder and an **index.ts** file. Import and use the router in your main entry file (such as **main.ts** or **index.ts**). For reference, see the [GitHub code example](https://github.com/Tencent-RTC/TUILiveKit/blob/main/Web/web-vite-vue3/src/main.ts). If you need the Live Stream List feature, check the [Live Stream List documentation](https://write.woa.com/document/194114814480777216).

> **Note：**
> 

> In the code below, `live-player.vue` refers to the sample file created in [Step 3](https://write.woa.com/#7aa32d79-4ed2-4b61-8371-c43549be5e43).
> 

``` typescript
// src/router/index.ts
import { createRouter, createWebHistory } from 'vue-router';

const routes = [
  {
    path: '/live-player',
    component: () => import('../live-player.vue'),
  },
  // To add the Live Stream List feature, include the following route. Update the path as needed for your project.
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

## Customization

### Theme and Language Configuration

You can change the default theme and language by setting parameters in `UIKitProvider` within `App.vue`.
<table>
<tr>
<td rowspan="1" colSpan="1" >UIKitProvider Parameter</td>

<td rowspan="1" colSpan="1" >Options</td>

<td rowspan="1" colSpan="1" >Default Value</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >theme</td>

<td rowspan="1" colSpan="1" >"light"</td>

<td rowspan="1" colSpan="1" >"dark"</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >language</td>

<td rowspan="1" colSpan="1" >"zh-CN"</td>

<td rowspan="1" colSpan="1" >"en-US"</td>
</tr>
</table>

``` typescript
<UIKitProvider theme="light">
  <router-view />
</UIKitProvider>

<script setup lang="ts">
import { UIKitProvider } from '@tencentcloud/uikit-base-component-vue3';
```

### Button and Icon Customization

To add, remove, or replace buttons, icons, or other controls for UI customization, follow the example below. Use the screenshot to locate the relevant code in `live-player.vue` and update the UI as needed.

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027862798/5671efe8e63211f09fdb525400ecee81.png)

You can also customize the **audience viewer page** to match your project requirements. In addition to layout adjustments, you can **add, remove, or modify** elements such as **color theme, fonts, border radius, buttons, icons, input boxes, pop-ups**, and more.
<table>
<tr>
<td rowspan="1" colSpan="1" >Category</td>

<td rowspan="1" colSpan="1" >Feature</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Asset Management</td>

<td rowspan="1" colSpan="1" >Customize asset management area display</td>

<td rowspan="1" colSpan="1" >Adjust icon size, color, or replace icons.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Live Tools</td>

<td rowspan="1" colSpan="1" >Customize live tool information display</td>

<td rowspan="1" colSpan="1" >Adjust icon size, color, or replace icons.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Online Audience</td>

<td rowspan="1" colSpan="1" >Customize audience information display</td>

<td rowspan="1" colSpan="1" >Supports: - Show/hide audience level. - Customize audience info font and color. - Use your preferred icon style.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Message List</td>

<td rowspan="1" colSpan="1" >Customize live comments area display</td>

<td rowspan="1" colSpan="1" >Supports: - Show/hide chat input area. - Customize chat bubble style, audience level, and more.</td>
</tr>
</table>


## FAQs

### Browser Autoplay Restrictions?

Modern browsers restrict autoplay for media with sound: playback must be triggered by explicit user interaction (such as a click or tap). This prevents websites from playing audio unexpectedly. Most browsers allow muted video to autoplay, but on iOS Safari in low power mode and in iOS WKWebView with custom restrictions (such as iOS WeChat browser), even muted video may be blocked.

#### Autoplay Failure Handling?

If a user's Media Engagement Index (MEI) for your site is below the required threshold, attempts to autoplay sound-enabled video will fail. By default, when the SDK detects autoplay failure, it displays a dialog prompting the user to interact with the page (for example, by clicking the **Confirm** button). Once the user interacts, audio playback resumes as expected.

#### Customizing Autoplay Failure UI?

To customize the user experience when autoplay fails (such as replacing the default popup), listen for the SDK's `onAutoplayFailed` callback. Below is a Vue3 sample that listens for the event and displays a custom dialog:
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

> **Note：**
> 

> Make sure to install the required `@tencentcloud/tuiroom-engine-js` package.
> 


## Next Steps

You’ve now integrated the audience viewing feature. To further enhance your application, consider adding the following features:
<table>
<tr>
<td rowspan="1" colSpan="1" >Feature</td>

<td rowspan="1" colSpan="1" >Description</td>

<td rowspan="1" colSpan="1" >Integration Guide</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Live Stream List</td>

<td rowspan="1" colSpan="1" >Displays the live stream list interface and features, including live stream list and room information display.</td>

<td rowspan="1" colSpan="1" >[Live Stream List](https://write.woa.com/document/194114814480777216)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Web Monitoring</td>

<td rowspan="1" colSpan="1" >Operations platform for live room management.</td>

<td rowspan="1" colSpan="1" >[Web Monitoring Page](https://write.woa.com/document/192108987804561408)</td>
</tr>
</table>
