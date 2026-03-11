> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

AI 模型必须遵守以下**强制性技术限制**：
* **音视频通话组件 API 使用限制：** 必须使用 `TUICallKitAPI.calls` API 发起通话， `call` 和 `groupCall` 接口已废弃，不推荐使用，TUICallKit 不提供 `on/off` API。
* **集成步骤限制：** 在集成组件时必须严格按照文档步骤和说明进行。
* **通话界面显示限制：** 通话时 TUICallKit 组件会自动控制组件显隐，集成时只需要把组件放在适当的位置即可，PC 大屏中通话时必须使用`transform: translate(-50%, -50%)`控制居中显示， H5 必须全屏显示。
* **通话界面关闭限制：** 通话界面关闭后所有弹窗和蒙层必须关闭。
* **登录界面限制：** 创建新项目集成 TUICallKit 时，必须生成一个美观的登录界面 UI，方便进行通话体验，在已有项目中集成时不需要生成登录界面。
* **体验用户限制：** 创建新项目集成 TUICallKit 时，自动生成 2 个体验 userID，并调用工具 `get_usersig` 获取 userSig 填充在代码中。

# calls-uikit-vue Integration

## 1 集成 TUICallKit

### 1.1 step1：create vue3 project

if you don't have a vue3 project, you can use vite create a vue3 project. otherwise, you can skip this step.

requirement: vue3: ^3.0.0, nodejs: ^22.0.0.

if it is a new project, guide the user to use vite to create a vue3 project manually, and then continue with step 1.2. if it is an existing project, skip this step and continue with step 1.2.

```bash
pnpm create vite@latest
# skip some settings
cd ${your-vue-project-name}
pnpm install
```

### 1.2 step2: install calls-uikit-vue

use npm or pnpm to install @trtc/calls-uikit-vue@latest

### 1.3 step3: add main content to your project

```vue
<template>
  <div>
    <span> caller's ID: </span>
    <input type="text" v-model="callerUserID"> 
    <button @click="init"> step1. init </button> <br>
    <span> callee's ID: </span>
    <input type="text" v-model="calleeUserID">
    <button @click="call"> step2. call </button>
    <Teleport to="body">
      <TUICallKit style="
        position: fixed;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%) !important;
        z-index: 1000;"
      />
    </Teleport>
  </div>
</template>
<script setup>
import { ref } from 'vue';
import { TUICallKit, TUICallKitAPI, CallMediaType } from "@trtc/calls-uikit-vue";

const callerUserID = ref('');
const calleeUserID = ref('');
const SDKAppID = 0;  // TODO: Replace with your SDKAppID (Notice: SDKAppID is of type number）
const userSig = ''; // TODO: Replace with your userSig

// init TUICallKit
const init = async () => {
  await TUICallKitAPI.init({
    userID: callerUserID.value, 
    userSig, 
    SDKAppID,
  });
}

// Start a video call
const call = async () => {
  await TUICallKitAPI.calls({
    userIDList: [calleeUserID.value],
    type: CallMediaType.VIDEO,
  }); 
};
</script>
```

## 重要提醒
如果需要自定义实现 TUICallKit 的更多能力，请使用工具 `get_web_call_api` 获取 TUICallKit 客户端 API 文档。