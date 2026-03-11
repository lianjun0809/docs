> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

This document provides a detailed introduction to the **barrage component**, including the **barrage message component (BarrageList)** and the **message sending component (BarrageInput)**. You can refer to the sample code in this document for seamless integration of our pre-developed components into your existing project, or customize the style and layout according to your needs by following the component customization section in the document.

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027862798/9de2371a98f611f0b38f5254001c06ec.png)


## Component Composition
<table>
<tr>
<td rowspan="1" colSpan="1" >**Component Name**</td>

<td rowspan="1" colSpan="1" >**Detailed Description**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**Barrage Message Component (BarrageList)**</td>

<td rowspan="1" colSpan="1" >A component responsible for real-time display and management of barrage message streams, providing a complete message display solution including **message list rendering, time aggregation, user interaction, and responsive adaptation**.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**Message Sending Component (BarrageInput)**</td>

<td rowspan="1" colSpan="1" >An input component that provides rich text editing and message sending features, with seamless integration of **emoji selector, character limit, status management, and cross-platform adaptation**, offering users a smooth input experience.</td>
</tr>
</table>


## Component Integration

### Step 1: Configuring the Environment and Activating the Service

Before performing quick integration, you need to refer to [preparations](https://write.woa.com/document/185222107981008896), meet the related environment configuration and activate the corresponding service.

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

### Step 3: Integrating the Barrage Component

Introduce and use the barrage component in your project. You can copy the following example directly to show **a complete live streaming room barrage message component and message send component** in your project.
``` typescript
<template>
  <UIKitProvider theme="dark" language="en-US">
    <div class="app">
      <div class="chat-container">
        <div class="chat-content">
          <BarrageList class="barrage-list" />
        </div>
        <div class="chat-input">
          <BarrageInput class="barrage-input" />
        </div>
      </div>
    </div>
  </UIKitProvider>
</template>

<script setup lang="ts">
import { onMounted, ref } from 'vue';
import { UIKitProvider } from '@tencentcloud/uikit-base-component-vue3';
import { BarrageList, BarrageInput, useLoginState, useLiveState } from 'tuikit-atomicx-vue3';

const { login, loginUserInfo } = useLoginState();
const { joinLive } = useLiveState();

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
  await joinLive({
    liveId: 'input corresponding live streaming room LiveId',     // enter live room by inputting corresponding liveId
  });
});
</script>

<style scoped>.app{width:100vw;height:100vh;display:flex;justify-content:center;align-items:center;padding:20px;box-sizing:border-box}.chat-container{width:100%;max-width:500px;height:600px;border-radius:16px;display:flex;flex-direction:column;overflow:hidden}.chat-content{flex:1;overflow:hidden}.barrage-list{width:100%;height:100%}.chat-input{background-color:var(--bg-color-dialog);padding:16px}.barrage-input{width:100%}</style>
```

## Customize Component

**Barrage Message Component** provides users with various and dimensional `Props` APIs for custom requirements, allowing users to customize features or UI. Parameter content is as shown in the table below.

> **Note:**
> 

> Note: To directly learn about the custom details of the Barrage Message Component (BarrageList), quickly jump to the following link: [Barrage Message Component Customization](https://write.woa.com/#872b809d-0251-49c3-8b4c-4c97b2801bdf);
> 

> Note: To directly learn about the custom details of the Message Sending Component (BarrageInput), quickly jump to the following link: [Message Sending Component Customization](https://write.woa.com/#566ae5d7-6c69-4ba1-858a-bf839428b171);
> 


### Barrage Message Component (BarrageList) Customization

#### **Props**
<table>
<tr>
<td rowspan="1" colSpan="1" >**Parameter Name**</td>

<td rowspan="1" colSpan="1" >**Parameter Type**</td>

<td rowspan="1" colSpan="1" >**Default Value**</td>

<td rowspan="1" colSpan="1" >**Description**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >messageAggregationTime</td>

<td rowspan="1" colSpan="1" >Number</td>

<td rowspan="1" colSpan="1" >300</td>

<td rowspan="1" colSpan="1" >Maximum time interval for message grouping (seconds).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >filter</td>

<td rowspan="1" colSpan="1" >(message: IMessageModel) => boolean</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Functions for filtering messages.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Message</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >Message</td>

<td rowspan="1" colSpan="1" >Custom Message Component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >MessageTimeDivider</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >MessageTimeDivider</td>

<td rowspan="1" colSpan="1" >Custom Message Time Segmentation Component.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >LocalNoticeMessage</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >LocalNoticeMessage</td>

<td rowspan="1" colSpan="1" >Custom Local Notification Component.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >containerStyle</td>

<td rowspan="1" colSpan="1" >CSSProperties</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Custom message list container style.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >itemStyle</td>

<td rowspan="1" colSpan="1" >CSSProperties</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Custom single message item style.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >height</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Component height, supports CSS units.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >style</td>

<td rowspan="1" colSpan="1" >CSSProperties</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Specify the root element's custom style.</td>
</tr>
</table>


As indicated in the table above, the Props custom part of the Barrage Message Component consists of three sections: **component properties, replaceable subcomponents, and custom styles.** Specific content is as shown in the table below.
<table>
<tr>
<td rowspan="1" colSpan="1" >**Content**</td>

<td rowspan="1" colSpan="1" >**Parameter**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**Component Property**</td>

<td rowspan="1" colSpan="1" >`filter`,`messageAggregationTime`</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**Replaceable subcomponent**</td>

<td rowspan="1" colSpan="1" >`Message`,`MessageTimeDivider`,`LocalNoticeMessage`</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**Custom style**</td>

<td rowspan="1" colSpan="1" >`ContainerStyle`,`ItemStyle`,`height`,`style`</td>
</tr>
</table>


#### Filter Message

By setting the `filter` parameter, you can flexibly control the message content displayed in the barrage message component.
``` typescript
<BarrageList :filter="(message) => message.type === 'TIMTextElem'" />
```

#### Message Aggregation Time

By setting the `messageAggregationTime` parameter, you can control the grouping time interval.
``` typescript
<BarrageList :messageAggregationTime="300" />
```

#### Custom Style

Barrage Message Component provides `containerStyle`, `itemStyle`, `custom child component`, etc., for customizing component styles.
1. To customize the message list container style, you can pass a style object to the `containerStyle` attribute.


   **Example: Custom container padding**

   ``` typescript
   <BarrageList :containerStyle="{ padding: '0px' }" />
   ```
2. To customize a single message style, you can pass a style object to the `itemStyle` attribute.


   **Example: Custom message item spacing, border, and message bubble color**

   ``` typescript
   <BarrageList :itemStyle="{ borderRadius: '10px', background: '#1C66e5', padding: '10px', boxSizing: 'border-box'}" />
   ```
3. The barrage message component supports custom message display components, and you can fully control the rendering method.


   **Example: Custom Message Component**

   ``` typescript
   // MyCustomMessage.vue
   <template>
     <div class="custom-message">
       <div class="message-header">
         <span class="user-name">{{ getUserName(message) }}</span>
         <span class="message-time">{{ formatTime(message.time) }}</span>
       </div>
       <div class="message-content">
         {{ getMessageText(message) }}
       </div>
     </div>
   </template>
   
   <script setup lang="ts">
   interface SimpleMessage {
     id: string;
     from: string;
     nick?: string;
     nameCard?: string;
     time: number;
     type: string;
     content: string;
     avatar?: string;
   }
   
   interface Props {
     message: SimpleMessage;
     isLastInChunk?: boolean;
   }
   
   const props = defineProps<Props>();
   
   const formatTime = (timestamp: number) => {
     return new Date(timestamp * 1000).toLocaleTimeString('zh-CN', {
       hour: '2-digit',
       minute: '2-digit'
     });
   };
   
   const getUserName = (message: SimpleMessage) => {
     return message.nameCard || message.nick || message.from || 'anonymous user';
   };
   
   const getMessageText = (message: SimpleMessage) => {
     if (message.type === 'text') {
       return message.content || '';
     } else if (message.type === 'image') {
       return '[image message]';
     } else if (message.type === 'emoji') {
       return '[emoji message]';
     }
     return '[other types of messages]';
   };
   </script>
   
   <style scoped>.custom-message{background:linear-gradient(135deg,#667eea 0%,#764ba2 100%);color:white;padding:12px;border-radius:12px;margin:4px 0;box-shadow:0 2px 8px rgba(0,0,0,0.1);transition:transform 0.2s ease}.custom-message:hover{transform:translateY(-2px)}.message-header{display:flex;justify-content:space-between;align-items:center;margin-bottom:8px;font-size:12px;opacity:0.9}.user-name{font-weight:500;max-width:120px;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}.message-time{font-size:11px;opacity:0.7}.message-content{font-size:14px;line-height:1.4;word-break:break-word}</style>
   
   // Use the barrage message component for use in
   <template>
      <BarrageList :Message="MyCustomMessage" />
   </template>
   
   <script setup lang="ts">
   import MyCustomMessage from "./MyCustomMessage.vue";
   </script>
   ```
<table>
<tr>
<td rowspan="2" colSpan="1" >**Before modification**</td>

<td rowspan="1" colSpan="3" >**After modification**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**Custom container padding**</td>

<td rowspan="1" colSpan="1" >**Custom message item spacing and border**</td>

<td rowspan="1" colSpan="1" >**Custom Message Component**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027862798/bfe98f52991711f0961e52540099c741.png)</td>

<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027862798/dc2f7512991711f0961e52540099c741.png)</td>

<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027862798/ecaf4bfc991711f0a207525400bf7822.png)</td>

<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027862798/83c99885991b11f0961e52540099c741.png)</td>
</tr>
</table>


### Message Sending Component (BarrageInput) Customization

#### **Props**
<table>
<tr>
<td rowspan="1" colSpan="1" >**Parameter Name**</td>

<td rowspan="1" colSpan="1" >**Type**</td>

<td rowspan="1" colSpan="1" >**Default Value**</td>

<td rowspan="1" colSpan="1" >**Description**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >containerClass</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >''</td>

<td rowspan="1" colSpan="1" >Custom container CSS class name.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >containerStyle</td>

<td rowspan="1" colSpan="1" >Record<br></td>

<td rowspan="1" colSpan="1" >{}</td>

<td rowspan="1" colSpan="1" >Inline style of custom container.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >width</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Component width, supports CSS units.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >height</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Component height, supports CSS units.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >minHeight</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >'40px'</td>

<td rowspan="1" colSpan="1" >Minimum component height, supports CSS units.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >maxHeight</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >'140px'</td>

<td rowspan="1" colSpan="1" >Max component height, supports CSS units.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >placeholder</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Placeholder text in the input box.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >disabled</td>

<td rowspan="1" colSpan="1" >Boolean</td>

<td rowspan="1" colSpan="1" >false</td>

<td rowspan="1" colSpan="1" >Whether to disable the input box.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >autoFocus</td>

<td rowspan="1" colSpan="1" >Boolean</td>

<td rowspan="1" colSpan="1" >true</td>

<td rowspan="1" colSpan="1" >Whether to auto-focus into the input box.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >maxLength</td>

<td rowspan="1" colSpan="1" >Number</td>

<td rowspan="1" colSpan="1" >80</td>

<td rowspan="1" colSpan="1" >Maximum character limit for input content.</td>
</tr>
</table>


#### **Events**
<table>
<tr>
<td rowspan="1" colSpan="1" >**Event Name**</td>

<td rowspan="1" colSpan="1" >**Parameter**</td>

<td rowspan="1" colSpan="1" >**Description**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >focus</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Trigger when the input box gets focus.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >blur</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Trigger when the input box loses focus.</td>
</tr>
</table>


As indicated in the table above, the Props custom part of the Message Sending Component consists of three sections: **size control, input restriction, and custom styles.** Specific content is as shown in the table below.
<table>
<tr>
<td rowspan="1" colSpan="1" >**Content**</td>

<td rowspan="1" colSpan="1" >**Parameter**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**Size control**</td>

<td rowspan="1" colSpan="1" >`width`,`height`,`minHeight`,`minWidth`</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**Input restriction**</td>

<td rowspan="1" colSpan="1" >`maxLength`</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**Custom style**</td>

<td rowspan="1" colSpan="1" >`ContainerStyle`,`ContainerClass`</td>
</tr>
</table>


#### Size Control

By setting `width`, `height`, `minHeight`, `maxHeight` parameters, you can flexibly control the size of **BarrageInput**.
``` typescript
<BarrageInput width="400px" height="60px" minHeight="40px" maxHeight="120px" />
```

#### Input Restriction

By setting the `maxLength` parameter, you can control the maximum number of characters for input content.
``` typescript
<BarrageInput :maxLength="100" />
```

#### Custom Style

The message send component provides `containerStyle` and `containerClass` attributes for customizing component style.
1. To customize the input box container style, you can pass a style object to the `containerStyle` attribute.


   **Example: Custom container background and border rounded corners**

   ``` typescript
   <BarrageInput :containerStyle="{ backgroundColor: '#a8abb2', borderRadius: '0 0', boxShadow: '0 2px 8px rgba(0,0,0,0.1)'}" />
   ```
2. To customize the input box container class name, you can pass a class name string to the `containerClass` attribute.


   **Example: Custom container class name**

   ``` typescript
   <template>
     <BarrageInput containerClass="my-custom-input-container" />
   </template>
   
   <style>.my-custom-input-container {background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);border: none;border-radius: 20px;padding: 8px 20px;}.my-custom-input-container:focus-within {box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.3);}</style>
   ```
<table>
<tr>
<td rowspan="2" colSpan="1" >**Before modification**</td>

<td rowspan="1" colSpan="2" >**After modification**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**Custom container background and border rounded corners**</td>

<td rowspan="1" colSpan="1" >**Custom message item spacing and border**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027862798/9c1eca1e991b11f0961e52540099c741.png)</td>

<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027862798/bd9f3926991b11f0a207525400bf7822.png)</td>

<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027862798/e1d02d0f991b11f081465254007c27c5.png)</td>
</tr>
</table>

