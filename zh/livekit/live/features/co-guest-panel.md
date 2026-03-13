> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

## Platform: Vue

本文对**连麦管理面板（CoGuestPanel）**进行了详细的介绍，您可以在已有项目中直接参考本文示例集成我们开发好的组件，也可以根据您的需求按照文档中的组件定制化部分对样式和布局进行深度的定制。

## 核心功能
| **功能名称** | **具体内容** |
| --- | --- |
| **Tab 切换** | 提供双 Tab 界面设计，用户可在连麦申请和连麦管理两个功能模块间快速切换，支持状态记忆和消息提示。 |
| **申请列表** | 实时展示所有待审核的连麦申请，显示用户头像、昵称等信息，支持按时间排序和状态筛选功能。 |
| **主播操作** | 提供丰富的一键式操作按钮，支持接受申请、拒绝申请、断开连麦等功能，实时反馈操作结果。 |

## 组件接入

### 步骤1：环境配置及开通服务

在进行快速接入之前，您需要参考 准备工作，满足相关环境配置及开通对应服务。

### 步骤2：安装依赖

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

### 步骤3：集成连麦管理面板

在您的项目中引入并使用**连麦管理面板**，可直接复制如下代码示例至您的项目中展示连麦管理面板。
``` typescript
<template>
  <UIKitProvider theme="light" language="zh-CN">
    <div class="app">
      <CoGuestPanel class="co-guest-panel" />
    </div>
  </UIKitProvider>
</template>

<script setup lang="ts">
import { onMounted, ref } from 'vue';
import { UIKitProvider } from '@tencentcloud/uikit-base-component-vue3';
import { CoGuestPanel, useLoginState, useLiveState } from 'tuikit-atomicx-vue3';

const { login, loginUserInfo } = useLoginState();
const { joinLive } = useLiveState();

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
    liveId: '输入对应直播间 LiveId',     // 输入对应 liveId 进入直播间
  });
});
</script>

<style scoped>.app{width:100vw;height:100vh;display:flex;justify-content:center;align-items:center;padding:20px;box-sizing:border-box}.co-guest-panel{width:100%;max-width:500px;padding: 24px;height:600px;background:rgba(255,255,255,0.9);border-radius:12px;box-shadow:0 8px 32px rgba(0,0,0,0.1);overflow:hidden}</style>
```

## 自定义样式定制

连麦管理面板支持通过 CSS 变量进行样式定制，您可以覆盖以下变量来调整组件外观，在已完成**步骤3**的前提下，您可以参考如下示例的方式来调整连麦管理面板的 UI，也可以直接将下列示例增量复制进您的组件中生成下列效果示例。
``` typescript
<template>
   <CoGuestPanel class="co-guest-panel" />
</template>

<style>.co-guest-panel{--text-color-primary:#2d3748;--text-color-secondary:#93a3bb;--text-color-link:#20c9e7;--bg-color-primary:#ffffff;--bg-color-hover:#d6e7f3;--stroke-color-primary:#8bb6ef;--stroke-color-secondary:#90c0f4;--shadow-light:0 2px 8px rgba(69,67,67,0.08);--shadow-medium:0 4px 16px rgba(93,87,87,0.12);--transition:all 0.3s ease;}.co-guest-panel .panel-content{background:var(--bg-color-primary);border-radius:16px;border:1px solid var(--stroke-color-primary);box-shadow:var(--shadow-medium);transition:var(--transition);overflow:hidden;}.co-guest-panel .panel-content:hover{box-shadow:0 8px 24px rgba(0,0,0,0.15);transform:translateY(-2px);border-color:var(--stroke-color-secondary);}.co-guest-panel .user-item{padding:16px;margin:8px 0;background:var(--bg-color-primary);border:1px solid var(--stroke-color-primary);border-radius:12px;transition:var(--transition);cursor:pointer;}.co-guest-panel .user-item:hover{background:var(--bg-color-hover);border-color:var(--text-color-link);box-shadow:var(--shadow-light);transform:translateY(-1px);}.co-guest-panel .user-item:active{transform:translateY(0);transition:all 0.15s ease;}.co-guest-panel .user-item.selected{background:rgba(102,126,234,0.08);border-color:var(--text-color-link);box-shadow:var(--shadow-light);}</style></style>
```
| **修改前** | **修改后** |
| --- | --- |
|  |  |
