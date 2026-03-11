> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

本文对**弹幕组件**进行了详细的介绍，其中包含**弹幕消息组件（BarrageList）**和**消息发送组件（BarrageInput）。**您可以在已有项目中直接参考本文示例集成我们开发好的整体组件，也可以根据您的需求按照文档中的组件自定义部分对样式，布局进行深度的定制。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027862798/97b51d7b975411f093df52540099c741.png)


## 组件构成
<table>
<tr>
<td rowspan="1" colSpan="1" >**组件名称**</td>

<td rowspan="1" colSpan="1" >**具体内容**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**弹幕消息组件（BarrageList）**</td>

<td rowspan="1" colSpan="1" >负责实时展示和管理弹幕消息流的组件，提供**消息列表渲染、时间聚合、用户交互和响应式适配**等完整的消息展示解决方案。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**消息发送组件（BarrageInput）**</td>

<td rowspan="1" colSpan="1" >提供富文本编辑和消息发送功能的输入组件，集成**表情选择器、字符限制、状态管理和跨平台适配**，为用户提供流畅的消息输入体验。</td>
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

### 步骤3：集成弹幕组件

在您的项目中引入并使用弹幕组件，可直接复制如下示例至您的项目中展示**完整的直播间弹幕消息组件以及消息发送组件**。
``` typescript
<template>
  <UIKitProvider theme="dark" language="zh-CN">
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

<style scoped>.app{width:100vw;height:100vh;display:flex;justify-content:center;align-items:center;padding:20px;box-sizing:border-box}.chat-container{width:100%;max-width:500px;height:600px;border-radius:16px;display:flex;flex-direction:column;overflow:hidden}.chat-content{flex:1;overflow:hidden}.barrage-list{width:100%;height:100%}.chat-input{background-color:var(--bg-color-dialog);padding:16px}.barrage-input{width:100%}</style>
```

## 自定义组件

**弹幕消息组件**分别为用户自定义需求提供了丰富且多维度的`Props` 接口，允许用户自定义功能或自定义 UI 等，具体参数内容如下表所示。

> **说明：**
> 

> 若您需要直接了解弹幕消息组件（BarrageList）的自定义的详细内容可快速跳转如下链接：[弹幕消息组件自定义](https://write.woa.com/#872b809d-0251-49c3-8b4c-4c97b2801bdf)；
> 

> 若您需要直接了解消息发送组件（BarrageInput）的自定义的详细内容可快速跳转如下链接：[消息发送组件自定义](https://write.woa.com/#566ae5d7-6c69-4ba1-858a-bf839428b171)；
> 


### 弹幕消息组件（BarrageList）自定义

#### **Props**
<table>
<tr>
<td rowspan="1" colSpan="1" >**参数名**</td>

<td rowspan="1" colSpan="1" >**参数类型**</td>

<td rowspan="1" colSpan="1" >**默认值**</td>

<td rowspan="1" colSpan="1" >**说明**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >messageAggregationTime</td>

<td rowspan="1" colSpan="1" >Number</td>

<td rowspan="1" colSpan="1" >300</td>

<td rowspan="1" colSpan="1" >消息分组的最大时间间隔（秒）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >filter</td>

<td rowspan="1" colSpan="1" >(message: IMessageModel) => boolean</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >用于筛选消息的函数。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Message</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >Message</td>

<td rowspan="1" colSpan="1" >自定义消息组件。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >MessageTimeDivider</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >MessageTimeDivider</td>

<td rowspan="1" colSpan="1" >自定义消息时间分割线组件。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >LocalNoticeMessage</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >LocalNoticeMessage</td>

<td rowspan="1" colSpan="1" >自定义本地通知消息组件。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >containerStyle</td>

<td rowspan="1" colSpan="1" >CSSProperties</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >自定义消息列表容器样式。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >itemStyle</td>

<td rowspan="1" colSpan="1" >CSSProperties</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >自定义单条消息项样式。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >height</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >组件高度，支持CSS单位。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >style</td>

<td rowspan="1" colSpan="1" >CSSProperties</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >指定根元素样式的自定义样式。</td>
</tr>
</table>


如上表所示，弹幕消息组件的 Props 自定义部分由三块内容组成，分别为**组件属性、可替换子组件、自定义样式，**具体内容如下表所示。
<table>
<tr>
<td rowspan="1" colSpan="1" >**内容**</td>

<td rowspan="1" colSpan="1" >**参数**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**组件属性**</td>

<td rowspan="1" colSpan="1" >`filter`、`messageAggregationTime`</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**可替换子组件**</td>

<td rowspan="1" colSpan="1" >`Message`、`MessageTimeDivider`、`LocalNoticeMessage`</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**自定义样式**</td>

<td rowspan="1" colSpan="1" >`ContainerStyle`、`ItemStyle`、`height`、`style`</td>
</tr>
</table>


#### 消息筛选

通过设置 `filter` 参数，您可以灵活地控制弹幕消息组件中显示的消息内容。
``` typescript
<BarrageList :filter="(message) => message.type === 'TIMTextElem'" />
```

#### 消息聚合时间

通过设置 `messageAggregationTime` 参数，您可以控制消息分组的时间间隔。
``` typescript
<BarrageList :messageAggregationTime="300" />
```

#### 自定义样式

弹幕消息组件提供了 `containerStyle`、`itemStyle`、`自定义子组件` 等内容，用于自定义组件样式。
1. 要自定义消息列表容器样式，您可以给 `containerStyle` 属性传递一个样式对象。


   **示例：自定义容器内边距**

   ``` typescript
   <BarrageList :containerStyle="{ padding: '0px' }" />
   ```
2. 要自定义单条消息样式，您可以给 `itemStyle` 属性传递一个样式对象。


   **示例：自定义消息项间距和边框及消息气泡颜色**

   ``` typescript
   <BarrageList :itemStyle="{ borderRadius: '10px', background: '#1C66e5', padding: '10px', boxSizing: 'border-box'}" />
   ```
3. 弹幕消息组件支持自定义消息展示组件，您可以完全控制消息的渲染方式。


   **示例：自定义消息组件**

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
     return message.nameCard || message.nick || message.from || '匿名用户';
   };
   
   const getMessageText = (message: SimpleMessage) => {
     if (message.type === 'text') {
       return message.content || '';
     } else if (message.type === 'image') {
       return '[图片消息]';
     } else if (message.type === 'emoji') {
       return '[表情消息]';
     }
     return '[其他类型消息]';
   };
   </script>
   
   <style scoped>.custom-message{background:linear-gradient(135deg,#667eea 0%,#764ba2 100%);color:white;padding:12px;border-radius:12px;margin:4px 0;box-shadow:0 2px 8px rgba(0,0,0,0.1);transition:transform 0.2s ease}.custom-message:hover{transform:translateY(-2px)}.message-header{display:flex;justify-content:space-between;align-items:center;margin-bottom:8px;font-size:12px;opacity:0.9}.user-name{font-weight:500;max-width:120px;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}.message-time{font-size:11px;opacity:0.7}.message-content{font-size:14px;line-height:1.4;word-break:break-word}</style>
   
   // 在 弹幕消息组件 中使用
   <template>
      <BarrageList :Message="MyCustomMessage" />
   </template>
   
   <script setup lang="ts">
   import MyCustomMessage from "./MyCustomMessage.vue";
   </script>
   ```
<table>
<tr>
<td rowspan="2" colSpan="1" >**修改前**</td>

<td rowspan="1" colSpan="3" >**修改后**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**自定义容器内边距**</td>

<td rowspan="1" colSpan="1" >**自定义消息项间距和边框**</td>

<td rowspan="1" colSpan="1" >**自定义消息组件**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027862798/9692f904975411f09b0c525400bf7822.png)</td>

<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027862798/96a32914975411f08ceb5254005ef0f7.png)</td>

<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027862798/969e911d975411f0b5725254001c06ec.png)</td>

<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027862798/970a3d94975411f0af98525400454e06.png)</td>
</tr>
</table>


### 消息发送组件（BarrageInput）自定义

#### **Props**
<table>
<tr>
<td rowspan="1" colSpan="1" >**参数名**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**默认值**</td>

<td rowspan="1" colSpan="1" >**说明**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >containerClass</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >''</td>

<td rowspan="1" colSpan="1" >自定义容器的 CSS 类名。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >containerStyle</td>

<td rowspan="1" colSpan="1" >Record<br></td>

<td rowspan="1" colSpan="1" >{}</td>

<td rowspan="1" colSpan="1" >自定义容器的内联样式。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >width</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >组件宽度，支持CSS单位。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >height</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >组件高度，支持CSS单位。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >minHeight</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >'40px'</td>

<td rowspan="1" colSpan="1" >组件最小高度，支持CSS单位。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >maxHeight</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >'140px'</td>

<td rowspan="1" colSpan="1" >组件最大高度，支持CSS单位。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >placeholder</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >输入框占位符文本。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >disabled</td>

<td rowspan="1" colSpan="1" >Boolean</td>

<td rowspan="1" colSpan="1" >false</td>

<td rowspan="1" colSpan="1" >是否禁用输入框。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >autoFocus</td>

<td rowspan="1" colSpan="1" >Boolean</td>

<td rowspan="1" colSpan="1" >true</td>

<td rowspan="1" colSpan="1" >是否自动聚焦到输入框。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >maxLength</td>

<td rowspan="1" colSpan="1" >Number</td>

<td rowspan="1" colSpan="1" >80</td>

<td rowspan="1" colSpan="1" >输入内容的最大字符数限制。</td>
</tr>
</table>


#### **Events**
<table>
<tr>
<td rowspan="1" colSpan="1" >**事件名**</td>

<td rowspan="1" colSpan="1" >**参数**</td>

<td rowspan="1" colSpan="1" >**说明**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >focus</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >输入框获得焦点时触发。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >blur</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >输入框失去焦点时触发。</td>
</tr>
</table>


如上表所示，消息发送组件的 Props 自定义部分由三块内容组成，分别为**尺寸控制、输入限制、自定义样式，**具体内容如下表所示。
<table>
<tr>
<td rowspan="1" colSpan="1" >**内容**</td>

<td rowspan="1" colSpan="1" >**参数**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**尺寸控制**</td>

<td rowspan="1" colSpan="1" >`width`、`height`、`minHeight`、`minWidth`</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**输入限制**</td>

<td rowspan="1" colSpan="1" >`maxLength`</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**自定义样式**</td>

<td rowspan="1" colSpan="1" >`ContainerStyle`、`ContainerClass`</td>
</tr>
</table>


#### 尺寸控制

通过设置 `width`、`height`、`minHeight`、`maxHeight` 参数，您可以灵活地控制 **BarrageInput** 的尺寸。
``` typescript
<BarrageInput width="400px" height="60px" minHeight="40px" maxHeight="120px" />
```

#### 输入限制

通过设置 `maxLength` 参数，您可以控制输入内容的最大字符数。
``` typescript
<BarrageInput :maxLength="100" />
```

#### 自定义样式

消息发送组件提供了 `containerStyle`、`containerClass` 属性，用于自定义组件样式。
1. 若需要自定义输入框容器样式，您可以给 `containerStyle` 属性传递一个样式对象。


   **示例：自定义容器背景和边框圆角**

   ``` typescript
   <BarrageInput :containerStyle="{ backgroundColor: '#a8abb2', borderRadius: '0 0', boxShadow: '0 2px 8px rgba(0,0,0,0.1)'}" />
   ```
2. 若需要自定义输入框容器类名，您可以给 `containerClass` 属性传递一个类名字符串。


   **示例：自定义容器类名**

   ``` typescript
   <template>
     <BarrageInput containerClass="my-custom-input-container" />
   </template>
   
   <style>.my-custom-input-container {background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);border: none;border-radius: 20px;padding: 8px 20px;}.my-custom-input-container:focus-within {box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.3);}</style>
   ```
<table>
<tr>
<td rowspan="2" colSpan="1" >**修改前**</td>

<td rowspan="1" colSpan="2" >**修改后**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**自定义容器背景和边框圆角**</td>

<td rowspan="1" colSpan="1" >**自定义消息项间距和边框**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027862798/96a14c89975411f0af98525400454e06.png)</td>

<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027862798/96b8b32f975411f09b0c525400bf7822.png)</td>

<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027862798/96a7c372975411f0a7c6525400e889b2.png)</td>
</tr>
</table>
