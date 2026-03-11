> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

This document provides a detailed introduction to **Video Source Editing Canvas (StreamMixer)**. You can refer to the sample code in this document to integrate our pre-developed components into your existing project, or customize the style and layout according to your needs by following the component customization section in the document.

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027862798/245486a898f311f0a207525400bf7822.png)


## Core Features
<table>
<tr>
<td rowspan="1" colSpan="1" >**Feature Category**</td>

<td rowspan="1" colSpan="1" >**Specific Capabilities**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**Real-time preview**</td>

<td rowspan="1" colSpan="1" >Provide a WYSIWYG editing experience where hosts can intuitively see the mixed stream effect, supporting operations like rotation, move, scale, mirror, and hierarchy adjustment.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**Template layout**</td>

<td rowspan="1" colSpan="1" >Built-in multiple live streaming room layout templates support automatic adaptation to different microphone-connected scenarios, including nine-grid, 1v6, floating window, helping you quickly switch between different live stream styles.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**User status management**</td>

<td rowspan="1" colSpan="1" >Intelligent detection of co-broadcasting users joining and exiting, automatic layout adjustment with no manual intervention required, ensuring smooth live streaming and providing seamless experience for hosts.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**Customizable UI**</td>

<td rowspan="1" colSpan="1" >To meet diverse business scenarios, the video source editing canvas provides component UI customization slots, enabling full control over co-broadcasting users' video stream areas. Rewrite their UI display, flexibly define avatars, nicknames, status, and other information, and easily create a unique visual experience that matches your UI style.</td>
</tr>
</table>


## Component Integration

### Step 1: Configuring the Environment and Activating the Service

Before quick integration, you need to refer to [Preparations](https://write.woa.com/document/185222107981008896), meet related environment configuration and activate corresponding service.

### Step 2: Installing Dependencies




【npm】
``` bash
npm install tuikit-atomicx-vue3@latest @tencentcloud/uikit-base-component-vue3 --save
```


【pnpm】
``` bash
pnpm add tuikit-atomicx-vue3@latest @tencentcloud/uikit-base-component-vue3
```


【yarn】
``` bash
yarn add tuikit-atomicx-vue3@latest @tencentcloud/uikit-base-component-vue3
```

### Step 3: Joining Live Room

Introduce and use the **Video Source Editing Canvas** in your project. You can copy the following example code directly to your project and add the corresponding live streaming room.
``` typescript
<template>
  <UIKitProvider theme="dark" language="zh-CN">
    <div class="app">
      <LiveScenePanel class="live-scene-panel" />
      <StreamMixer class="live-stream-mixer" />
    </div>
  </UIKitProvider>
</template>

<script setup lang="ts">
import { onMounted } from 'vue';
import { UIKitProvider } from '@tencentcloud/uikit-base-component-vue3';
import { LiveScenePanel, StreamMixer, useLoginState, useLiveState, useCoGuestState } from 'tuikit-atomicx-vue3';

const { login } = useLoginState();
const { createLive } = useLiveState();
const { sendCoGuestRequest } = useCoGuestState();

async function initLogin() {
  try {
    await login({
      sdkAppId: 0,        // SDKAppID, see Step 1 to get
      userId: '',         // UserID, see Step 1 to get
      userSig: '',        // userSig, see Step 1 to get
    });
  } catch (error) {
    console.error('login error:', error);
  }
}

onMounted(async () => {
  await initLogin();                                                          
  // After the anchor creates a live streaming room
  // StreamMixer automatically pushes the local composite video stream to the room
  await createLive({               
    liveId: `live_${loginUserInfo.value.userId}`,
    liveName: `${loginUserInfo.value?.userName}'s live streaming room`,
  });
  // The client can join the live room by calling the method and switch on/off mic as needed. 
  // After the audience succeeds in going on mic, StreamMixer starts TRTC streaming automatically
  await sendCoGuestRequest();     
});
</script>

<style>.app {width: 100vw; height: 100vh; display: flex; justify-content: center; align-items: center}</style>
```
``` bash
npm run dev
```

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027862798/671e3f42ad8e11f08bcc5254007c27c5.gif)


## Component Customization

**Video Source Editing Canvas** provides a flexible component customization slot that supports you in adjusting the style and layout of elements such as avatar, nickname, and status based on your own needs. It also supports customizing the video stream area for co-streaming UI. Below are slot usage examples.

### Component Slot
<table>
<tr>
<td rowspan="1" colSpan="1" >**Name**</td>

<td rowspan="1" colSpan="1" >**Parameter**</td>

<td rowspan="1" colSpan="1" >**Description**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >seatViewUI</td>

<td rowspan="1" colSpan="1" >seatInfo: SeatInfo</td>

<td rowspan="1" colSpan="1" >Display UI for custom seat</td>
</tr>
</table>

``` java
// Example of using the seatViewUI slot
<StreamMixer>
  <CustomSeatViewUI #seatViewUI></CustomSeatViewUI>
</StreamMixer>
```
1. `SeatInfo` defines the basic info and status of each seat in a live streaming room:

<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Required</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`index`</td>

<td rowspan="1" colSpan="1" >`number`</td>

<td rowspan="1" colSpan="1" >Required</td>

<td rowspan="1" colSpan="1" >The seat index number starts incrementing from 0, used to identify the seat position in the room.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`isLocked`</td>

<td rowspan="1" colSpan="1" >`boolean`</td>

<td rowspan="1" colSpan="1" >Required</td>

<td rowspan="1" colSpan="1" >The seat lock status, `true` means the seat is locked and other users are unable to enter; `false` means the seat is open.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`userInfo`</td>

<td rowspan="1" colSpan="1" >`SeatUserInfo`</td>

<td rowspan="1" colSpan="1" >optional</td>

<td rowspan="1" colSpan="1" >The user information of the current occupant in this seat. If the seat is empty, it is `undefined`.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`region`</td>

<td rowspan="1" colSpan="1" >`RegionInfo`</td>

<td rowspan="1" colSpan="1" >optional</td>

<td rowspan="1" colSpan="1" >The display region information of the seat in the video canvas, for multiple streams video layout.</td>
</tr>
</table>

   ``` typescript
   interface SeatInfo {
     index: number;           // Seat index
     isLocked: boolean;       // Whether the seat is locked
     userInfo?: SeatUserInfo; // User information on the seat (optional)
     region?: RegionInfo;     // Region information of the seat in the canvas (optional)
   } 
   ```
2. `SeatUserInfo` defines the user details of each seat in a live streaming room:

<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Required</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`roomId`</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >Required</td>

<td rowspan="1" colSpan="1" >The current unique identifier of the live streaming room, used to distinguish different live streaming rooms</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`userId`</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >Required</td>

<td rowspan="1" colSpan="1" >User's Unique Identifier, must be unique in the entire system</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`userName`</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >Required</td>

<td rowspan="1" colSpan="1" >The name displayed for users in live streams supports Chinese, English, and other characters.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`avatarUrl`</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >Required</td>

<td rowspan="1" colSpan="1" >The complete URL of the user profile photo supports HTTPS protocol.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`microphoneStatus`</td>

<td rowspan="1" colSpan="1" >`DeviceStatus`</td>

<td rowspan="1" colSpan="1" >Required</td>

<td rowspan="1" colSpan="1" >Microphone status</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`microphoneStatusReason`</td>

<td rowspan="1" colSpan="1" >`DeviceStatusReason`</td>

<td rowspan="1" colSpan="1" >Required</td>

<td rowspan="1" colSpan="1" >Reasons for microphone status changes, to distinguish between user proactive operation and administrator operation</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`cameraStatus`</td>

<td rowspan="1" colSpan="1" >`DeviceStatus`</td>

<td rowspan="1" colSpan="1" >Required</td>

<td rowspan="1" colSpan="1" >Camera status</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`cameraStatusReason`</td>

<td rowspan="1" colSpan="1" >`DeviceStatusReason`</td>

<td rowspan="1" colSpan="1" >Required</td>

<td rowspan="1" colSpan="1" >Reasons for camera status changes, to distinguish between user proactive operation and administrator operation</td>
</tr>
</table>

   ``` typescript
   interface SeatUserInfo {
     roomId: string;                    // Live streaming room ID
     userId: string;                    // User ID
     userName: string;                  // User Display Name
     avatarUrl: string;                 // User Avatar URL
     microphoneStatus: DeviceStatus;    // mic status
     allowOpenMicrophone: boolean;      // whether to allow turning on microphone
     cameraStatus: DeviceStatus;        // camera status
     allowOpenCamera: boolean;          // whether to allow turning on camera
   }
   
   export type SeatUserInfo = {
     liveId: string;                                // Live streaming room ID
     userId: string;                                // User ID
     userName: string;                              // User Display Name
     avatarUrl: string;                             // User Avatar URL
     microphoneStatus: DeviceStatus;                // mic status
     microphoneStatusReason: DeviceStatusReason;    // reason for change
     cameraStatus: DeviceStatus;                    // camera status
     cameraStatusReason: DeviceStatusReason;        // reason for change
   }
   ```
3. `RegionInfo` defines the display area and hierarchical information of the seat in the video canvas:

<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Required</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`x`</td>

<td rowspan="1" colSpan="1" >`number`</td>

<td rowspan="1" colSpan="1" >Required</td>

<td rowspan="1" colSpan="1" >X-coordinate of the region's top-left corner relative to the canvas (pixel value)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`y`</td>

<td rowspan="1" colSpan="1" >`number`</td>

<td rowspan="1" colSpan="1" >Required</td>

<td rowspan="1" colSpan="1" >Y-coordinate of the region's top-left corner relative to the canvas (pixel value)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`w`</td>

<td rowspan="1" colSpan="1" >`number`</td>

<td rowspan="1" colSpan="1" >Required</td>

<td rowspan="1" colSpan="1" >Width of the region (pixel value), must be greater than 0</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`h`</td>

<td rowspan="1" colSpan="1" >`number`</td>

<td rowspan="1" colSpan="1" >Required</td>

<td rowspan="1" colSpan="1" >Height of the region (pixel value), must be greater than 0</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`zOrder`</td>

<td rowspan="1" colSpan="1" >`number`</td>

<td rowspan="1" colSpan="1" >Required</td>

<td rowspan="1" colSpan="1" >Z-order, the larger the value, the more positioned towards the front for processing overlap display priority</td>
</tr>
</table>

   ``` typescript
   interface RegionInfo {
     x: number;      // Top-left X-axis coordinate of the region
     y: number;      // Top-left Y-axis coordinate of the region
     w: number;      // Region width
     h: number;      // Region height
     zOrder: number; // Z-order
   }
   ```

### Custom Slot Example

To help you better experience and understand the customized capability of the seatViewUI slot in the video source editing Canvas component, we provide a **live streaming and mic connection scenario** example for your reference. You can refer to the above **step 3** to incrementally copy the following code into your project to achieve a similar effect.
``` typescript
<template>
  <StreamMixer>
    <template #seatViewUI="{ userInfo }">
      <div 
        class="live-stream-view"
        :class="{ 'is-anchor': isAnchor(userInfo), 'is-guest': !isAnchor(userInfo) }"
      >
        User information overlay
        <div class="user-overlay">
          <div class="user-badge" :class="{ 'anchor-badge': isAnchor(userInfo) }">
            {{ isAnchor(userInfo) ? 'Anchor' : 'Audience' }}
          </div>
          <div class="user-name">{{ userInfo.userName }}</div>
          <div class="device-status">
            <span :class="['mic', userInfo.microphoneStatus]"></span>
            <span :class="['camera', userInfo.cameraStatus]"></span>
          </div>
        </div>
      </div>
    </template>
  </StreamMixer>
</template>

<script setup lang="ts">
import { StreamMixer } from 'tuikit-atomicx-vue3';
import type { SeatUserInfo } from 'tuikit-atomicx-vue3';

// Determine whether it is an anchor (based on business logic)
const isAnchor = (userInfo: SeatUserInfo) => {
  // Here access can be judged based on uid and role
  return userInfo.userId.includes('anchor') || userInfo.userName.includes('Anchor');
};
</script>

<style scoped>.live-stream-view{position:relative;width:100%;height:100%;border-radius:8px;overflow:hidden}.live-stream-view.is-anchor{border:3px solid #ff6b35;box-shadow:0 0 20px rgba(255,107,53,.3)}.live-stream-view.is-guest{border:1px solid #ddd}.video-area{width:100%;height:100%;background:#000}.user-overlay{position:absolute;bottom:0;left:0;right:0;background:linear-gradient(transparent,rgba(0,0,0,.8));padding:10px;color:#fff}.user-badge{display:inline-block;padding:2px 8px;border-radius:10px;font-size:12px;margin-bottom:5px;background:#666}.anchor-badge{background:#ff6b35;color:#fff}.user-name{font-weight:700;margin-bottom:5px}.device-status span{margin-right:5px;opacity:.8}.device-status .camera.Off,.device-status .mic.Off{opacity:.3}</style>
```