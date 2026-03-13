> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

## Platform: Vue

本文对**直播视频组件（LiveView）**进行了详细的介绍，您可以在已有项目中直接参考本文示例集成我们开发好的组件，也可以根据您的需求按照文档中的组件定制化部分对样式，布局进行深度的定制。

## 核心功能
| **功能分类** | **具体能力** |
| --- | --- |
| **智能流切换** | LiveView 能够根据当前用户的身份（观众或连麦者）自动切换流类型。 - 观众模式： 组件将播放超低延迟视频流，确保数百万观众都能流畅观看，同时大幅节省流量成本。 - 连线模式： 组件会自动切换到实时音视频流，提供毫秒级的超低延迟，保证连线用户之间实时、清晰的互动体验。 |
| **可定制化 UI** | 为了满足多样化的业务场景，LiveView 提供组件 UI 自定义插槽，让您能够完全掌控连麦用户的视频流区域，重写其 UI 展示，灵活定义连麦用户的头像、昵称、状态等信息，轻松打造符合您品牌风格的独特视觉体验。 |

## 组件接入

### 步骤1：环境配置及开通服务

在进行快速接入之前，您需要参考 准备工作，满足相关环境配置及开通对应服务。

### 步骤2: 安装依赖

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

### 步骤3：加入直播间并进行连麦

在您的项目中引入并使用 LiveView，可直接复制如下代码示例至您的项目中加入对应直播间进行连麦。
``` typescript
<template>
  <UIKitProvider theme="dark" language="zh-CN">
    <div class="app">
      <LiveView />
    </div>
  </UIKitProvider>
</template>

<script setup lang="ts">
import { onMounted } from 'vue';
import { UIKitProvider } from '@tencentcloud/uikit-base-component-vue3';
import { LiveView, useLoginState, useLiveState, useCoGuestState } from 'tuikit-atomicx-vue3';

const { login } = useLoginState();
const { joinLive } = useLiveState();
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
  await joinLive({
    liveId: '已经存在的直播间 Id',   // 观众进入直播间之后， LiveView 自动播放超低延时流
  })
  await sendCoGuestRequest();     // 观众端通过调用相应方法即可加入直播间并根据需要上下麦,观众成功上麦之后，LiveView 自动播放实时音视频流
});
</script>

<style>.app {width: 100vw; height: 100vh; display: flex; justify-content: center; align-items: center}</style>
```

## 组件定制化

LiveView 提供了灵活的组件自定义插槽，该插槽支持您根据自己需求调整头像、昵称、状态等元素的样式与布局，也支持定制视频流区域连麦 UI。下列分别给出插槽使用示例

#### 组件插槽
| **名称** | **参数** | **说明** |
| --- | --- | --- |
| streamViewUI | userInfo | 自定义麦位的显示 UI |

``` java
// streamViewUI 插槽使用示例
<LiveView>
  <CustomStreamViewUI #streamViewUI></CustomStreamViewUI>
</LiveView>
```
1. `userInfo` 定义了直播房间中每个麦位的基本信息和状态：

| 参数 | 类型 | 属性 | 说明 |
| --- | --- | --- | --- |
| userInfo | userInfo | 非必填 | 当前坐在该麦位上的用户信息，如果麦位为空则为 `undefined`。 |

   ``` typescript
   interface userInfo {
     userInfo: userInfo; // 麦位上的用户信息
   } 
   ```
2. `userInfo` 定义了直播房间中每个麦位上的用户详细信息：

| 参数 | 类型 | 属性 | 说明 |
| --- | --- | --- | --- |
| roomId | string | 必填 | 当前直播房间的唯一标识符，用于区分不同的直播房间。 |
| userId | string | 必填 | 用户的唯一标识符，在整个系统中保持唯一性。 |
| userName | string | 必填 | 用户在直播中显示的名称，支持中文、英文等字符。 |
| avatarUrl | string | 必填 | 用户头像的完整URL地址，支持 HTTPS 协议。 |
| microphoneStatus | DeviceStatus | 必填 | 麦克风的当前状态。 |
| microphoneStatusReason | DeviceStatusReason | 必填 | 麦克风状态变更的原因，用于区分是用户主动操作还是管理员操作。 |
| cameraStatus | DeviceStatus | 必填 | 摄像头的当前状态。 |
| cameraStatusReason | DeviceStatusReason | 必填 | 摄像头状态变更的原因，用于区分是用户主动操作还是管理员操作。 |

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

| 参数 | 类型 | 属性 | 说明 |
| --- | --- | --- | --- |
| x | number | 必填 | 区域左上角相对于画布左上角的X坐标（像素值）。 |
| y | number | 必填 | 区域左上角相对于画布左上角的Y坐标（像素值）。 |
| w | number | 必填 | 区域的宽度（像素值），必须大于0。 |
| h | number | 必填 | 区域的高度（像素值），必须大于0。 |
| zOrder | number | 必填 | 层级顺序，数值越大越靠前显示，用于处理重叠区域的显示优先级。 |

   ``` typescript
   interface RegionInfo {
     x: number;      // 区域左上角X坐标
     y: number;      // 区域左上角Y坐标
     w: number;      // 区域宽度
     h: number;      // 区域高度
     zOrder: number; // 层级顺序
   }
   ```

#### 自定义插槽示例

为了更好地让您体验及理解 LiveView 组件的 streamViewUI 插槽定制化能力，我们提供了**直播连麦场景**示例供您参考，您可以参考上述**步骤3**将如下代码增量复制至您的项目中实现类似场景的效果。
``` typescript
<template>
  <LiveView>
    <template #streamViewUI="{ userInfo }">
      <div 
        class="live-stream-view"
        :class="{ 'is-anchor': isAnchor(userInfo), 'is-guest': !isAnchor(userInfo) }"
      >
        <!-- 视频流区域 -->
        <div class="video-area">
          <!-- 视频流会自动渲染 -->
        </div>
        
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
  </LiveView>
</template>

<script setup lang="ts">
import { LiveView } from 'tuikit-atomicx-vue3';
import type { SeatUserInfo } from 'tuikit-atomicx-vue3';

// 判断是否为主播（根据业务逻辑）
const isAnchor = (userInfo: SeatUserInfo) => {
  // 这里可以根据用户ID、角色等判断
  return userInfo.userId.includes('anchor') || userInfo.userName.includes('主播');
};
</script>

<style scoped>.live-stream-view{position:relative;width:100%;height:100%;border-radius:8px;overflow:hidden}.live-stream-view.is-anchor{border:3px solid #ff6b35;box-shadow:0 0 20px rgba(255,107,53,.3)}.live-stream-view.is-guest{border:1px solid #ddd}.video-area{width:100%;height:100%;background:#000}.user-overlay{position:absolute;bottom:0;left:0;right:0;background:linear-gradient(transparent,rgba(0,0,0,.8));padding:10px;color:#fff}.user-badge{display:inline-block;padding:2px 8px;border-radius:10px;font-size:12px;margin-bottom:5px;background:#666}.anchor-badge{background:#ff6b35;color:#fff}.user-name{font-weight:700;margin-bottom:5px}.device-status span{margin-right:5px;opacity:.8}.device-status .camera.Off,.device-status .mic.Off{opacity:.3}</style>
```
