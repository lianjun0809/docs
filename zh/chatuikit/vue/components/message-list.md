> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

## 概述

MessageList 组件是聊天界面的核心组件，负责展示消息列表并提供丰富的交互功能。它支持消息聚合、自动滚动、历史消息加载、已读回执等高级特性，适用于构建高度可定制的聊天界面。组件内部处理滚动行为、消息加载逻辑和消息分组展示，为用户提供流畅的消息浏览体验。

## 功能特性
- 消息展示：支持多种消息类型（文本、图片、视频、文件、自定义消息等）的渲染和显示。

- 消息聚合：根据时间间隔和发送者自动聚合相邻消息。

- 智能滚动：自动滚动到底部，支持手动滚动控制。

- 历史加载：上加载更多历史消息。

- 已读回执：支持消息已读状态显示。

- 消息操作：支持撤回、删除等消息操作。

- 自定义渲染：支持自定义消息组件和时间分割线组件。


## 快速使用

以下示例代码是 MessageList 最简单的用法。
``` typescript
<template>
  <UIKitProvider>
    <Chat>
      <MessageList />
      <MessageInput />
    </Chat>
  </UIKitProvider>
</template>


<script lang="ts" setup>
import { UIKitProvider, Chat, MessageList, MessageInput } from '@tencentcloud/chat-uikit-vue3';
</script>

```

> **说明：**
> 

> 实践建议：
> 
> 1. MessageList 组件需要放在 UIKitProvider、Chat 容器中使用。
> 2. MessageList 建议和 MessageInput 组件搭配使用。
> 3. MessageList 会默认读取当前激活的会话，如果您不集成 ConversationList 组件，请参考 [仅集成聊天](https://write.woa.com/document/181344022523346944) 文档。


## Props 字段速查表
<table>
<tr>
<td rowspan="1" colSpan="1" >字段</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >默认值</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[alignment](https://write.woa.com/#alignment)</td>

<td rowspan="1" colSpan="1" >'left' \| 'right' \| 'two-sided'</td>

<td rowspan="1" colSpan="1" >'two-sided'</td>

<td rowspan="1" colSpan="1" >消息的对齐方式，支持左对齐、右对齐和双边对齐。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[messageAggregationTime](https://write.woa.com/#messageAggregationTime)</td>

<td rowspan="1" colSpan="1" >number</td>

<td rowspan="1" colSpan="1" >300 (秒)</td>

<td rowspan="1" colSpan="1" >消息聚合的时间间隔（秒），在此时间内发送的同一发送者的消息会被聚合。设置为 0 可禁用消息聚合。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[enableReadReceipt](https://write.woa.com/#enableReadReceipt)</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >false</td>

<td rowspan="1" colSpan="1" >是否启用消息已读回执功能。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[messageActionList](https://write.woa.com/#messageActionList)</td>

<td rowspan="1" colSpan="1" >MessageAction[]</td>

<td rowspan="1" colSpan="1" >undefined</td>

<td rowspan="1" colSpan="1" >自定义消息操作列表，例如撤回、删除等。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[filter](https://write.woa.com/#filter)</td>

<td rowspan="1" colSpan="1" >(message: MessageModel) => boolean</td>

<td rowspan="1" colSpan="1" >undefined</td>

<td rowspan="1" colSpan="1" >自定义消息过滤函数，用于控制哪些消息应该显示。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[Message](https://write.woa.com/#Message)</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >undefined</td>

<td rowspan="1" colSpan="1" >自定义消息组件，用于渲染单条消息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[MessageTimeDivider](https://write.woa.com/#MessageTimeDivider)</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >undefined</td>

<td rowspan="1" colSpan="1" >自定义消息时间分割线组件。</td>
</tr>
</table>


## Props 详细介绍

### alignment
- 类型：'left' | 'right' | 'two-sided'

- 详细说明：消息在列表中的对齐方式。`'left'` 表示所有消息左对齐，`'right'` 表示所有消息右对齐，`'two-sided'` 表示发送方消息右对齐，接收方消息左对齐。默认值为 `'two-sided'`。


### messageAggregationTime
- 类型：number

- 详细说明：消息聚合的时间间隔，单位为秒。当同一发送者在指定时间间隔内连续发送多条消息时，这些消息将被聚合显示。设置为 `0` 或更小的值将禁用消息聚合功能，每条消息都会独立显示。默认值为 `300` (5分钟)。


### enableReadReceipt
- 类型：boolean

- 详细说明：是否启用消息的已读回执功能。当设置为 `true` 时，组件将尝试显示消息的已读状态。默认值为 `false`。


### messageActionList
- 类型：MessageAction[]

- 详细说明：用于定义在消息上可以执行的自定义操作列表，例如复制、撤回、转发、删除等。这是一个复杂类型，可以通过传入一个 `MessageAction` 对象数组来定制消息的操作行为。默认值为 `undefined`，组件内部会根据 `useMessageActions` 钩子提供默认的操作列表。


   目前默认的顺序是： `['copy', 'recall', 'quote', 'forward', 'delete']`。


   **MessageAction** 类型定义:

   ``` typescript
   import type { Component } from 'vue';
   import type { MessageModel } from '@tencentcloud/chat-uikit-vue3';
   
   interface MessageAction {
     /** 唯一的操作标识符 */
     key: string;
     /** 操作的显示文本 */
     label: string;
     /** 操作的图标组件或图标名称 */
     icon?: Component | string;
     /** 操作点击时的回调函数 */
     onClick?: (message: MessageModel) => void;
     /** 控制操作的可见性，可以是布尔值或一个根据消息决定可见性的函数 */
     visible?: boolean | ((message: MessageModel) => boolean);
     /** 自定义组件，如果提供了，将替代默认的标签和图标 */
     component?: Component;
     /** 自定义类名 */
     className?: string;
     /** 自定义样式 */
     style?: Record<string, any>;
   }
   ```

   可以使用 `useMessageActions` 钩子获取完整的消息操作列表，然后根据需要进行自定义。`useMessageActions` 钩子接收一个可选参数，可以是一个包含操作键（`string`）或完整 `MessageAction` 对象的数组。如果传入 `string` 数组，则会使用默认操作的配置；如果传入 `MessageAction` 对象，则会合并并覆盖默认配置。


#### 代码示例1：变更消息操作列表的顺序

下面的代码将 `forward`操作放到消息操作列表的第一个。
``` typescript
<template>
  <MessageList :messageActionList="actions" />
</template>

<script lang="ts" setup>
import { MessageList, useMessageActions } from '@tencentcloud/chat-uikit-vue3';

const actions = useMessageActions(['forward', 'copy', 'recall', 'quote', 'delete']);
</script>
```

示例效果：

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100033438418/8eaaf60188a811f0818a52540099c741.png)


#### 代码示例2：仅展示部分消息操作

仅展示 `copy`、`recall` 操作，其他操作隐藏。
``` typescript
<template>
  <MessageList :messageActionList="actions" />
</template>

<script lang="ts" setup>
import { MessageList, useMessageActions } from '@tencentcloud/chat-uikit-vue3';

const actions = useMessageActions(['copy', 'recall']);
</script>
```

示例效果：

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100033438418/d481cee988a811f0b321525400e889b2.png)


#### 代码示例3：自定义消息操作的样式和逻辑

下面是一个自定义转发操作的示例：
1. 将标签修改为 '转发 ⚠️'

2. 将颜色修改为橙色

3. 只有别人发的消息可以转发

   ``` typescript
   <template>
     <MessageList :messageActionList="actions" />
   </template>
   
   <script lang="ts" setup>
   import { MessageList, useMessageActions } from '@tencentcloud/chat-uikit-vue3';
   
   const actions = useMessageActions(['copy', {
     key: 'forward',
     label: 'Forward ⚠️',
     style: {
       color: 'orange',
     },
     visible: (message) => message.flow === 'in',
   }, 'quote', 'recall', 'delete']);
   </script>
   ```

   示例效果：

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100033438418/9aa48621824811f0b1df52540044a08e.png)


#### 代码示例4：新增自定义消息操作

假设需要自定义消息操作，例如仅其他人发送的消息可以标记'喜欢'，且插入在'撤回'操作之后。
``` typescript
<template>
  <MessageList :messageActionList="actions" />
</template>

<script lang="ts" setup>
import { MessageList, useMessageActions } from '@tencentcloud/chat-uikit-vue3';

const customLikeAction = {
  key: 'like',
  label: 'Like',
  icon: '🩷',
  visible: (message) => message.flow === 'in',
  onClick: (message) => {
    console.log('like message:', message.ID);
    // 在这里实现点赞逻辑，例如调用后端API
  },
};

const actions = useMessageActions(['forward', 'copy', 'recall', customLikeAction, 'quote', 'delete']);
</script>
```

示例效果：

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100033438418/9f5aa2e4824b11f0a8ae5254005ef0f7.png)


### filter
- type：((message: MessageModel) => boolean) | undefined

- 详细说明：一个自定义的过滤函数，用于在消息列表渲染之前对消息进行筛选。该函数接收一个 `MessageModel` 类型的消息对象，并返回一个布尔值。如果返回 `true`，则消息会显示；如果返回 `false`，则消息不会显示。默认值为 `undefined`，表示不进行额外过滤（但组件内部会默认过滤掉 `isDeleted` 为 `true` 的消息）。


#### 代码示例：过滤掉机器人发送的文本消息

这个示例展示了如何使用 `filter` prop 来过滤掉某些用户发送的特定消息。
``` typescript
<template>
  <MessageList :filter="customMessageFilter" />
</template>

<script lang="ts" setup>
import { MessageList, MessageType } from '@tencentcloud/chat-uikit-vue3';
import type { MessageModel } from '@tencentcloud/chat-uikit-vue3';

// 定义自定义消息过滤函数
const customMessageFilter = (message: MessageModel): boolean => {
  if (
    message.nick?.includes('_robot') 
    && message.type === MessageType.TEXT as any
  ) {
    return false;
  }
  return true;
};
</script>
```

### Message
- 类型：Component | undefined

- 详细说明：用于自定义渲染消息列表中的单个消息组件。


   如果您需要完全控制消息的显示样式和内部逻辑，可以传入一个 Vue 组件来替代默认的消息渲染。自定义组件将接收 `message` (IMessageModel 类型)、`alignment`、`messageActionList` 等 props。默认值会使用内部的默认消息组件 `Message`。


#### 代码示例：自定义 CUSTOM 消息点击跳转的消息组件

这个示例展示了如何创建一个自定义消息组件，用于渲染特定 `CUSTOM` 消息（`businessID` 为 `text_link`）为可点击跳转的链接。
``` typescript
<template>
  <MessageList :Message="CustomMessage" />
</template>

<script lang="ts" setup>
import { defineComponent, h } from 'vue';
import { MessageList, Message, MessageType } from '@tencentcloud/chat-uikit-vue3';
import type { MessageModel } from '@tencentcloud/chat-uikit-vue3';

const CustomMessage = defineComponent({
  name: 'CustomMessage',
  props: {
    message: {
      type: Object as () => MessageModel,
      required: true,
    },
    // MessageList 会传递其他 props，这里可以按需接收，例如 alignment, messageActionList 等
  },
  setup(props) {
    return () => {
      const { message } = props;

      if (message.type === MessageType.CUSTOM as any) {
        const { businessID, ...restData } = JSON.parse(message.payload.data);
        if (businessID === 'text_link') {
          return h('div', { class: 'custom-text-link-message' }, [
            h('div', restData.text),
            h('a', { href: restData.link, target: '_blank' }, `跳转到外部网址 ${restData.link}`),
          ]);
        }
      }
      // 其他消息类型使用默认消息组件
      return h(Message, props);
    };
  },
});
</script>

<style scoped>
.custom-text-link-message {
  padding: 8px;
  background-color: #f0f8ff;
  border-radius: 8px;
  max-width: 60%;
  margin-bottom: 4px;
}

.custom-text-link-message a {
  color: #1890ff;
  text-decoration: underline;
}
</style>
```

示例效果：

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100033438418/abd6f2ea825411f0b1df52540044a08e.png)


### MessageTimeDivider
- 类型：Component | undefined

- 详细说明：用于自定义渲染时间分割线组件。


   您可以传入一个 Vue 组件来替代默认的时间分割线渲染。自定义组件将接收 `currentMessage` (当前时间分割线关联的消息)、`previousMessage` (上一条消息) 等 props，可以根据这些信息决定时间分割线的显示逻辑和样式。默认值会使用内部的默认时间分割线组件 `MessageTimeDivider`。

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100033438418/4d5e72b688ae11f0974b52540044a08e.png)


#### 代码示例：自定义时间分割线组件，根据时间展示是否为上班时间

这个示例展示了如何创建一个自定义时间分隔线组件，根据消息时间判断是否为工作时间，并显示相应的标签和颜色。
``` typescript
<template>
  <MessageList :MessageTimeDivider="BusinessTimeDivider" />
</template>

<script lang="ts" setup>
import { defineComponent, h } from 'vue';
import { MessageList } from '@tencentcloud/chat-uikit-vue3';
import type { MessageModel } from '@tencentcloud/chat-uikit-vue3';

const BusinessTimeDivider = defineComponent({
  name: 'BusinessTimeDivider',
  props: {
    previousMessage: {
      type: Object as () => MessageModel | undefined,
      default: undefined,
    },
    currentMessage: {
      type: Object as () => MessageModel,
      required: true,
    },
  },
  setup(props) {
    if (!props.previousMessage || !props.currentMessage) {
      return () => null;
    }

    const currentTime = new Date(props.currentMessage.time * 1000);
    const prevTime = new Date(props.previousMessage.time * 1000);

    // 跨天或间隔超过4小时才显示
    const shouldShow = currentTime.toDateString() !== prevTime.toDateString()
      || (currentTime.getTime() - prevTime.getTime()) > 4 * 60 * 60 * 1000;

    if (!shouldShow) {
      return () => null;
    }

    // 判断工作时间 (9:00-18:00, 周一到周五)
    const isWorkingTime = () => {
      const hour = currentTime.getHours();
      const day = currentTime.getDay();
      return day >= 1 && day <= 5 && hour >= 9 && hour <= 18;
    };

    const timeLabel = isWorkingTime() ? 'Working' : 'Non working';
    const timeColor = isWorkingTime() ? '#52c41a' : '#faad14';

    return () =>
      h('div', { style: { textAlign: 'center', margin: '16px 0' } }, [
        h('span', {
          style: {
            backgroundColor: timeColor,
            color: 'white',
            padding: '2px 8px',
            borderRadius: '12px',
            marginRight: '8px',
          },
        }, timeLabel),
        currentTime.toLocaleString(),
      ]);
  },
});
</script>
```

示例效果：

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100033438418/1de6fe94825711f0a8ae5254005ef0f7.png)


## 扩展资料

`MessageModel` 类型常用字段：
``` typescript
// MessageModel 接口定义，详细内容请参考 @tencentcloud/chat-uikit-engine 文档
// 这是一个复杂的消息模型，包含消息ID、类型、发送者、内容、时间、状态等属性。
// 示例结构 (非完整定义):
interface MessageModel {
  ID: string;
  conversationID: string;
  type: MessageType;
  payload: any;
  flow: 'in' | 'out';
  from: string;
  to: string;
  time: number; // Unix 时间戳 (秒)
  status: 'unSend' | 'success' | 'fail';
  isDeleted: boolean;
  isRevoked: boolean;
  hasRiskContent: boolean; // 是否包含风险内容
  // ... 其他属性
}

enum MessageType {
  TEXT,     // 文本
  IMAGE,    // 图像
  AUDIO,    // 音频
  VIDEO,    // 视频
  FILE,     // 文件
  FACE,     // 大表情
  LOCATION, // 定位
  GRP_TIP,  // 群提示
  CUSTOM,   // 自定义
  MERGER,   // 合并转发
}

```

MessageModel 的完整内容请参见：[TUIChatEngine 参考文档](https://web.sdk.qcloud.com/im/doc/chat-engine/IMessageModel.html)。

## 相关文档
- [自定义组件 - UIKitProvider](https://write.woa.com/document/187032638782849024)

- [自定义组件 - ConversationList](https://write.woa.com/document/186960319111872512)

- [自定义组件 - Chat](https://write.woa.com/document/187778215983329280)

- [自定义组件 - MessageInput](https://write.woa.com/document/187058763983568896)

- [自定义组件 - ChatSetting](https://write.woa.com/document/187321409859108864)

- [自定义组件 - ContactList](https://write.woa.com/document/187595466274463744)

- [自定义组件 - Search](https://write.woa.com/document/187595449195040768)

- [chat-uikit-vue3 npm](https://www.npmjs.com/package/@tencentcloud/chat-uikit-vue3)

- [github Demo](https://github.com/Tencent-RTC/TUIKit_Vue3/tree/main/demos/rtcube-vite-vue3)


## 交流与反馈

如遇任何问题，可联系 [官网售后](https://cloud.tencent.com/act/event/connect-service#/) 反馈，享有专业工程师的支持，解决您的难题。

