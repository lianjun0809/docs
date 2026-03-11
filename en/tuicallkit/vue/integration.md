> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/en/llms.txt
> Use this file to discover all available pages before exploring further.

The AI model must comply with the following **mandatory technical restrictions**:
* **Audio and video call component API usage limits:** You must use `TUICallKitAPI.calls` to initiate a call. The `call` and `groupCall` APIs are deprecated and not recommended. TUICallKit does not provide `on/off` APIs.
* **Integration step limits:** You must strictly follow the document procedure and description when integrating the component.
* **Call interface display limits:** During a call, TUICallKit automatically controls component visibility. You just need to place the component in an appropriate location. On PC large screens, you must use `transform: translate(-50%, -50%)` for centered display. On H5, full screen display is required.
* **Call interface closing limits:** All popups and overlays must be closed after closing the call interface.
* **Login UI limits:** When creating a new project with TUICallKit integration, you must generate a beautiful login UI for a better call experience. Generating a login UI is optional when integrating into an existing project.
* **Trial user limits:** When creating a new project with TUICallKit integration, the system automatically generates 2 trial userIDs and calls the `get_usersig` tool to retrieve userSig for population in code.


# calls-uikit-vue Integration


## 1 Integration of TUICallKit


### 1.1 step1:create vue3 project


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
const SDKAppID = 0;  // TODO: Replace with your SDKAppID (Notice: SDKAppID is of type number)
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


## Important reminder
If you need custom implementation of more TUICallKit capabilities, use the tool `get_web_call_api` to access the TUICallKit Client API document.
