> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

本文对 TUILiveKit 组件中的**媒体源配置面板（LiveScenePanel）**进行了详细的介绍，您可以在已有项目中直接参考本文示例集成我们开发好的组件，也可以根据您的需求按照文档中的组件定制化部分对样式和布局进行深度的定制。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027862798/be6ef71a975411f093df52540099c741.png)


## 核心功能
<table>
<tr>
<td rowspan="1" colSpan="1" >**功能分类**</td>

<td rowspan="1" colSpan="1" >**具体能力**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**多素材类型支持**</td>

<td rowspan="1" colSpan="1" >摄像头、屏幕共享、图片、视频、文本等多种素材类型，支持设备选择和参数配置。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**智能显示模式**</td>

<td rowspan="1" colSpan="1" >无素材时显示完整面板，有素材时自动切换为紧凑按钮模式，响应式布局适配。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**素材管理操作**</td>

<td rowspan="1" colSpan="1" >添加、编辑、重命名、删除、排序等完整的素材管理功能，支持批量操作。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**实时预览配置**</td>

<td rowspan="1" colSpan="1" >摄像头配置弹窗提供实时预览，支持参数调整和设备测试。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**权限与错误处理**</td>

<td rowspan="1" colSpan="1" >自动权限检查，友好的错误提示和重试机制，保障用户体验。</td>
</tr>
</table>


## 组件接入

### 步骤1：环境配置及开通服务

在进行快速接入之前，您需要参考[准备工作](https://write.woa.com/document/185222107981008896)，满足相关环境配置及开通对应服务。

### 步骤2：安装依赖




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

### 步骤3：集成**媒体源配置面板**

在您的项目中引入并使用**媒体源配置面板**，可直接复制如下代码示例至您的项目中展示媒体源配置面板。
``` typescript
<template>
  <UIKitProvider theme="dark" language="zh-CN">
    <div class="app-container">
      <LiveScenePanel class="live-scene-panel" />
    </div>
  </UIKitProvider>
</template>

<script setup lang="ts">
import { onMounted } from 'vue';
import { UIKitProvider } from '@tencentcloud/uikit-base-component-vue3';
import { LiveScenePanel, useLoginState } from 'tuikit-atomicx-vue3';

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

<style scoped>.app-container{width:100vw;height:100vh;display:flex;justify-content:center;align-items:center;padding:20px;box-sizing:border-box}.live-scene-panel{width:20%;height:80vh;background:rgba(0,0,0,0.8);border-radius:16px}</style>
```

## 自定义组件

媒体源配置面板为用户自定义提供了丰富且多维度的功能接口，允许用户自定义素材类型、操作行为、样式主题等。在已完成上述**步骤3**的前提下，您可以参考如下示例的方式来调整媒体源配置面板的 UI，也可以直接将下列示例增量复制组件中生成下列效果示例。

### 样式自定义

通过 CSS 类名和变量自定义组件外观，支持主题色彩、布局样式、动画效果等全方位定制。
``` typescript
<template>
  <LiveScenePanel class="custom-live-scene-panel" />
</template>

<style>.app-container{width:100vw;height:100vh;display:flex;justify-content:center;align-items:center;padding:20px;box-sizing:border-box}.custom-live-scene-panel{width:100%;max-width:300px;height:80vh;background:linear-gradient(135deg,#667eea 0%,#764ba2 100%);border:2px solid #4c63d2;border-radius:16px;padding:24px;box-shadow:0 8px 32px rgba(0,0,0,0.1);color:white}.custom-live-scene-panel .add-material-item{background-color:#147fcb!important;color:white;border:none;border-radius:0!important;padding:12px 24px;font-weight:600;transition:all 0.3s ease}.custom-live-scene-panel .materials-list{margin-top:20px;gap:16px;display:grid;grid-template-columns:repeat(auto-fill,minmax(200px,1fr))}.custom-live-scene-panel .material-item{background:rgba(255,255,255,0.1);border:1px solid rgba(255,255,255,0.2);border-radius:12px;padding:16px;backdrop-filter:blur(10px);transition:all 0.3s ease}.custom-live-scene-panel .material-item:hover{background:rgba(255,255,255,0.2);transform:scale(1.02)}</style>
```
<table>
<tr>
<td rowspan="1" colSpan="2" >**修改前**</td>

<td rowspan="1" colSpan="2" >**修改后**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**添加媒体源界面**</td>

<td rowspan="1" colSpan="1" >**媒体源设置界面**</td>

<td rowspan="1" colSpan="1" >**添加媒体源界面**</td>

<td rowspan="1" colSpan="1" >**媒体源设置界面**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027862798/be374b93975411f093df52540099c741.png)</td>

<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027862798/be294e63975411f0a7c6525400e889b2.png)</td>

<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027862798/be90885c975411f0af98525400454e06.png)</td>

<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027862798/be5b3349975411f0b5725254001c06ec.png)</td>
</tr>
</table>


### 状态监听与扩展

通过状态管理 Hooks，您可以监听媒体源配置面板的内部状态变化，实现外部业务逻辑的响应式处理。这种方式允许您在不修改组件内部代码的情况下，对素材的添加、删除、更新等操作进行监听和响应，从而实现数据同步、业务统计、用户提示等扩展功能。
``` typescript
<template>
    <!-- 状态显示 -->
    <div class="status-info">
      <span>素材数量: {{ materialCount }}</span>
      <span>最后操作: {{ lastOperation }}</span>
    </div>
    <!-- LiveScenePanel 组件 -->
    <LiveScenePanel />
    <StreamMixer />
</template>

<script setup lang="ts">
import { ref, computed, watch } from 'vue';
import { LiveScenePanel, useVideoMixerState, StreamMixer } from 'tuikit-atomicx-vue3';

// 使用状态管理 hooks
const { mediaSourceList } = useVideoMixerState();
const lastOperation = ref('无');
const materialCount = computed(() => mediaSourceList.value.length);

// 监听素材列表变化
watch(mediaSourceList, (newList, oldList) => {
  if (newList.length > oldList.length) {
    lastOperation.value = '添加素材';
    console.log('素材已添加');
  } else if (newList.length < oldList.length) {
    lastOperation.value = '删除素材';
    console.log('素材已删除');
  }
}, { deep: true });
</script>

<style>.status-info {display: flex; gap: 20px; padding: 12px; background: #f8f9fa;border-radius: 6px; margin-bottom: 16px;font-size: 14px;}</style>
```