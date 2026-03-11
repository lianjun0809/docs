> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

本文对 TUILiveKit 组件中的**视频源编辑画板（StreamMixer）**进行了详细的介绍，您可以在已有项目中直接参考本文示例集成我们开发好的组件，也可以根据您的需求按照文档中的组件定制化部分对样式，布局进行深度的定制。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027862798/39af62f299ef11f0bf2352540044a08e.png)


## 核心功能
<table>
<tr>
<td rowspan="1" colSpan="1" >**功能分类**</td>

<td rowspan="1" colSpan="1" >**具体能力**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**实时预览**</td>

<td rowspan="1" colSpan="1" >提供所见即所得的编辑体验，主播可以直观地看到混流效果，支持对元素进行旋转、移动、缩放、镜像、层级调整等操作</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**模板布局**</td>

<td rowspan="1" colSpan="1" >内置多种直播间布局模板，支持自动适配不同连麦场景，包括九宫格、1v6、浮窗等，帮助您快速切换不同风格的直播画面。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**用户状态管理**</td>

<td rowspan="1" colSpan="1" >智能感知连麦用户的加入和退出，自动调整布局，无需手动干预，确保了直播过程的流畅性，为主播提供无缝体验。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**可定制化 UI**</td>

<td rowspan="1" colSpan="1" >为了满足多样化的业务场景，视频源编辑画板提供组件 UI 自定义插槽，让您能够完全掌控连麦用户的视频流区域，重写其 UI 展示，灵活定义连麦用户的头像、昵称、状态等信息，轻松打造符合您 UI 风格的独特视觉体验。</td>
</tr>
</table>


## 组件接入

### 步骤1：环境配置及开通服务

在进行快速接入之前，您需要参见 [准备工作](https://write.woa.com/document/185222107981008896)，满足相关环境配置及开通对应服务。

### 步骤2:  安装依赖




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

### 步骤3：加入直播间

在您的项目中引入并使用**视频源编辑画板**，可直接复制如下代码示例至您的项目中加入对应直播间。
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
  await createLive({               // 主播创建直播间之后， StreamMixer 自动将本地合图画面推流到直播间      
    liveId: `live_${loginUserInfo.value.userId}`,
    liveName: `${loginUserInfo.value?.userName} 的直播间`,
  });
  await sendCoGuestRequest();     // 观众端通过调用相应方法即可加入直播间并根据需要上下麦,观众成功上麦之后，StreamMixer 自动播放实时音视频流
});
</script>

<style>.app {width: 100vw; height: 100vh; display: flex; justify-content: center; align-items: center}</style>
```
``` bash
npm run dev
```

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027862798/395ffe7b99ef11f09936525400e889b2.gif)


## 组件定制化

**视频源编辑画板**提供了灵活的组件自定义插槽，该插槽支持您根据自己需求调整头像、昵称、状态等元素的样式与布局，也支持定制视频流区域连麦 UI。下列分别给出插槽使用示例

### 组件插槽
<table>
<tr>
<td rowspan="1" colSpan="1" >**名称**</td>

<td rowspan="1" colSpan="1" >**参数**</td>

<td rowspan="1" colSpan="1" >**说明**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >seatViewUI</td>

<td rowspan="1" colSpan="1" >seatInfo: SeatInfo</td>

<td rowspan="1" colSpan="1" >自定义麦位的显示 UI</td>
</tr>
</table>

``` java
// seatViewUI 插槽使用示例
<StreamMixer>
  <CustomSeatViewUI #seatViewUI></CustomSeatViewUI>
</StreamMixer>
```
1. `SeatInfo` 定义了直播房间中每个麦位的基本信息和状态：

<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >属性</td>

<td rowspan="1" colSpan="1" >说明</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >index</td>

<td rowspan="1" colSpan="1" >number</td>

<td rowspan="1" colSpan="1" >必填</td>

<td rowspan="1" colSpan="1" >麦位的索引号，从0开始递增，用于标识麦位在房间中的位置。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >isLocked</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >必填</td>

<td rowspan="1" colSpan="1" >麦位锁定状态，true 表示麦位被锁定，其他用户无法进入；false 表示麦位开放。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userInfo</td>

<td rowspan="1" colSpan="1" >SeatUserInfo</td>

<td rowspan="1" colSpan="1" >非必填</td>

<td rowspan="1" colSpan="1" >当前坐在该麦位上的用户信息，如果麦位为空则为 `undefined`。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >region</td>

<td rowspan="1" colSpan="1" >RegionInfo</td>

<td rowspan="1" colSpan="1" >非必填</td>

<td rowspan="1" colSpan="1" >麦位在视频画布中的显示区域信息，用于多路视频布局。</td>
</tr>
</table>

   ``` typescript
   interface SeatInfo {
     index: number;           // 麦位索引
     isLocked: boolean;       // 麦位是否被锁定
     userInfo?: SeatUserInfo; // 麦位上的用户信息（可选）
     region?: RegionInfo;     // 麦位在画布中的区域信息（可选）
   } 
   ```
2. `SeatUserInfo` 定义了直播房间中每个麦位上的用户详细信息：

<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >属性</td>

<td rowspan="1" colSpan="1" >说明</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >roomId</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >必填</td>

<td rowspan="1" colSpan="1" >当前直播房间的唯一标识符，用于区分不同的直播房间。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >必填</td>

<td rowspan="1" colSpan="1" >用户的唯一标识符，在整个系统中保持唯一性。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userName</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >必填</td>

<td rowspan="1" colSpan="1" >用户在直播中显示的名称，支持中文、英文等字符。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >avatarUrl</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >必填</td>

<td rowspan="1" colSpan="1" >用户头像的完整URL地址，支持 HTTPS 协议。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >microphoneStatus</td>

<td rowspan="1" colSpan="1" >DeviceStatus</td>

<td rowspan="1" colSpan="1" >必填</td>

<td rowspan="1" colSpan="1" >麦克风的当前状态。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >microphoneStatusReason</td>

<td rowspan="1" colSpan="1" >DeviceStatusReason</td>

<td rowspan="1" colSpan="1" >必填</td>

<td rowspan="1" colSpan="1" >麦克风状态变更的原因，用于区分是用户主动操作还是管理员操作。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >cameraStatus</td>

<td rowspan="1" colSpan="1" >DeviceStatus</td>

<td rowspan="1" colSpan="1" >必填</td>

<td rowspan="1" colSpan="1" >摄像头的当前状态。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >cameraStatusReason</td>

<td rowspan="1" colSpan="1" >DeviceStatusReason</td>

<td rowspan="1" colSpan="1" >必填</td>

<td rowspan="1" colSpan="1" >摄像头状态变更的原因，用于区分是用户主动操作还是管理员操作。</td>
</tr>
</table>

   ``` typescript
   interface SeatUserInfo {
     roomId: string;                    // 直播房间ID
     userId: string;                    // 用户唯一标识
     userName: string;                  // 用户显示名称
     avatarUrl: string;                 // 用户头像URL
     microphoneStatus: DeviceStatus;    // 麦克风状态
     allowOpenMicrophone: boolean;      // 是否允许打开麦克风
     cameraStatus: DeviceStatus;        // 摄像头状态
     allowOpenCamera: boolean;          // 是否允许打开摄像头
   }
   
   export type SeatUserInfo = {
     liveId: string;                                // 直播房间ID
     userId: string;                                // 用户唯一标识
     userName: string;                              // 用户显示名称
     avatarUrl: string;                             // 用户头像URL
     microphoneStatus: DeviceStatus;                // 麦克风状态
     microphoneStatusReason: DeviceStatusReason;    // 麦克风状态变更原因
     cameraStatus: DeviceStatus;                    // 摄像头状态
     cameraStatusReason: DeviceStatusReason;        // 摄像头状态变更原因
   }
   ```
3. `RegionInfo` 定义了麦位在视频画布中的显示区域和层级信息：

<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >属性</td>

<td rowspan="1" colSpan="1" >说明</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >x</td>

<td rowspan="1" colSpan="1" >number</td>

<td rowspan="1" colSpan="1" >必填</td>

<td rowspan="1" colSpan="1" >区域左上角相对于画布左上角的X坐标（像素值）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >y</td>

<td rowspan="1" colSpan="1" >number</td>

<td rowspan="1" colSpan="1" >必填</td>

<td rowspan="1" colSpan="1" >区域左上角相对于画布左上角的Y坐标（像素值）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >w</td>

<td rowspan="1" colSpan="1" >number</td>

<td rowspan="1" colSpan="1" >必填</td>

<td rowspan="1" colSpan="1" >区域的宽度（像素值），必须大于0。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >h</td>

<td rowspan="1" colSpan="1" >number</td>

<td rowspan="1" colSpan="1" >必填</td>

<td rowspan="1" colSpan="1" >区域的高度（像素值），必须大于0。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >zOrder</td>

<td rowspan="1" colSpan="1" >number</td>

<td rowspan="1" colSpan="1" >必填</td>

<td rowspan="1" colSpan="1" >层级顺序，数值越大越靠前显示，用于处理重叠区域的显示优先级。</td>
</tr>
</table>

   ``` typescript
   interface RegionInfo {
     x: number;      // 区域左上角X坐标
     y: number;      // 区域左上角Y坐标
     w: number;      // 区域宽度
     h: number;      // 区域高度
     zOrder: number; // 层级顺序
   }
   ```

### 自定义插槽示例

为了更好地让您体验及理解视频源编辑画板 组件的 seatViewUI 插槽定制化能力，我们提供了**直播连麦场景**示例场景供您参考，您可以参考上述**步骤3**将以下代码增量复制至您的项目中实现类似场景的效果。
``` typescript
<template>
  <StreamMixer>
    <template #seatViewUI="{ userInfo }">
      <div 
        class="live-stream-view"
        :class="{ 'is-anchor': isAnchor(userInfo), 'is-guest': !isAnchor(userInfo) }"
      >
        <!-- 用户信息覆盖层 -->
        <div class="user-overlay">
          <div class="user-badge" :class="{ 'anchor-badge': isAnchor(userInfo) }">
            {{ isAnchor(userInfo) ? '主播' : '观众' }}
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

// 判断是否为主播（根据业务逻辑）
const isAnchor = (userInfo: SeatUserInfo) => {
  // 这里可以根据用户ID、角色等判断
  return userInfo.userId.includes('anchor') || userInfo.userName.includes('主播');
};
</script>

<style scoped>.live-stream-view{position:relative;width:100%;height:100%;border-radius:8px;overflow:hidden}.live-stream-view.is-anchor{border:3px solid #ff6b35;box-shadow:0 0 20px rgba(255,107,53,.3)}.live-stream-view.is-guest{border:1px solid #ddd}.video-area{width:100%;height:100%;background:#000}.user-overlay{position:absolute;bottom:0;left:0;right:0;background:linear-gradient(transparent,rgba(0,0,0,.8));padding:10px;color:#fff}.user-badge{display:inline-block;padding:2px 8px;border-radius:10px;font-size:12px;margin-bottom:5px;background:#666}.anchor-badge{background:#ff6b35;color:#fff}.user-name{font-weight:700;margin-bottom:5px}.device-status span{margin-right:5px;opacity:.8}.device-status .camera.Off,.device-status .mic.Off{opacity:.3}</style>
```