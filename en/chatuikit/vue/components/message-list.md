> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/en/llms.txt
> Use this file to discover all available pages before exploring further.

# Overview

The MessageList component is the core component of the chat UI, responsible for showing the message list and providing abundant interaction features. It supports advanced features like message aggregation, auto-scroll, historical message loading, and read receipts, ideal for building highly customizable chat interfaces. Within the component, it handles scrolling behavior, message loading logic, and message grouping display, delivering a smooth browsing experience for users.


## Features
-Message display: support various message types (text, image, video, file, custom message) for rendering and display.

- Message aggregation: auto-group adjacent messages based on time interval and sender.

- Smart scroll: auto-scroll to the bottom with manual scroll control.

- History load: load more historical messages.

- Read receipt: support message read status display.

- Message operations: support actions such as recall and delete.

- Custom rendering: support custom message component and time segmentation component.

## Quick and Easy to Use

The following example shows the simplest usage of MessageList.
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

**Note:**
> 
Practical advice:
> 
> 1. The MessageList component must be placed in UIKitProvider and Chat containers.
> 2. MessageList is recommended to be used in conjunction with the MessageInput component.
> 3. MessageList will default read the currently active session. If you do not integrate the ConversationList component, see the integrated chat only (https://write.woa.com/document/181344022523346944) document.




## Props
<table>
<tr>
<td rowspan="1" colSpan="1" >Field</td>


<td rowspan="1" colSpan="1" >Type</td>


<td rowspan="1" colSpan="1" >Default Value</td>


<td rowspan="1" colSpan="1" >Description</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[alignment](https://write.woa.com/#alignment)</td>


<td rowspan="1" colSpan="1" >'left' \| 'right' \| 'two-sided'</td>


<td rowspan="1" colSpan="1" >'two-sided'</td>


<td rowspan="1" colSpan="1" >Message alignment mode, supports align left, align right and justify.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[messageAggregationTime](https://write.woa.com/#messageAggregationTime)</td>


<td rowspan="1" colSpan="1" >number</td>


<td rowspan="1" colSpan="1" >300 (seconds)</td>


<td rowspan="1" colSpan="1" >Message aggregation interval (seconds). Messages from the same sender sent within this time will be aggregated. Set to 0 to disable message aggregation.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[enableReadReceipt](https://write.woa.com/#enableReadReceipt)</td>


<td rowspan="1" colSpan="1" >boolean</td>


<td rowspan="1" colSpan="1" >false</td>


<td rowspan="1" colSpan="1" >Whether to enable the message read receipt feature.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[messageActionList](https://write.woa.com/#messageActionList)</td>


<td rowspan="1" colSpan="1" >MessageAction[]</td>


<td rowspan="1" colSpan="1" >undefined</td>


<td rowspan="1" colSpan="1" >Custom message operations list, such as recall and delete.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[filter](https://write.woa.com/#filter)</td>


<td rowspan="1" colSpan="1" >(message: MessageModel) => boolean</td>


<td rowspan="1" colSpan="1" >undefined</td>


<td rowspan="1" colSpan="1" >Custom message filter function, used to control which messages should display.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[Message](https://write.woa.com/#Message)</td>


<td rowspan="1" colSpan="1" >Component</td>


<td rowspan="1" colSpan="1" >undefined</td>


<td rowspan="1" colSpan="1" >Custom message component for rendering individual messages.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[MessageTimeDivider](https://write.woa.com/#MessageTimeDivider)</td>


<td rowspan="1" colSpan="1" >Component</td>


<td rowspan="1" colSpan="1" >undefined</td>


<td rowspan="1" colSpan="1" >Custom message time segmentation component.</td>
</tr>
</table>




## Props detailed introduction


### alignment
-Type: 'left' | 'right' | 'two-sided'


- Details: Message alignment mode in the list. `'left'` means all messages align left, `'right'` means all messages align right, `'two-sided'` means sender messages align right and recipient messages align left. Default value is `'two-sided'`.


### messageAggregationTime
- Type: number

- Details: Message aggregation interval in seconds. When the same sender sends multiple messages consecutively within the specified time interval, these messages will be aggregated and displayed. Set to `0` or a negative value to disable the aggregation function, and each message will be displayed independently. Default value is `300` (5 minutes).

### enableReadReceipt
- Type: boolean
- Details: Whether to enable the read receipt feature. When set to `true`, the component will attempt to display the read status of messages. Default value is `false`.

### messageActionList
- Type: MessageAction[]

- Details: Defines a list of custom actions that can be performed on messages, such as copy, recall, forward, and delete. This is a complex type that can be customized by importing an array of `MessageAction` objects. Default value is `undefined`, and the component will provide a default action list based on the `useMessageActions` hook.


   The current default sequence is: `['copy', 'recall', 'quote', 'forward', 'delete']`.

   **MessageAction** type definition:

   ``` typescript
   import type { Component } from 'vue';
   import type { MessageModel } from '@tencentcloud/chat-uikit-vue3';
   
   interface MessageAction {
     /** Unique operation identifier */
     key: string;
     /** Display text of the operation */
     label: string;
     /** Icon component or icon name for the operation */
     icon?: Component | string;
     /** Callback function when the operation is clicked */
     onClick?: (message: MessageModel) => void;
     /** Controls the visibility of the operation, can be a boolean value or a function that determines visibility based on the message */
     visible?: boolean | ((message: MessageModel) => boolean);
     /** Customize component, if provided, will replace the default tag and icon */
     component?: Component;
     /** Custom class name */
     className?: string;
     /** Custom style */
     style?: Record<string, any>;
   }
   ```


   Use the `useMessageActions` hook to obtain the complete message actions list, then customize as needed. The `useMessageActions` hook accepts an optional parameter, which can be an array of action keys (`string`) or complete `MessageAction` objects. If a `string` array is input, the default operation configuration will be used. If `MessageAction` objects are input, they will merge and override the default configuration.




#### Example code 1: Change the order of message actions list


The following code places the `forward` action first in the message actions list.
``` typescript
<template>
  <MessageList :messageActionList="actions" />
</template>


<script lang="ts" setup>
import { MessageList, useMessageActions } from '@tencentcloud/chat-uikit-vue3';


const actions = useMessageActions(['forward', 'copy', 'recall', 'quote', 'delete']);
</script>
```


example effect


![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100033438418/8eaaf60188a811f0818a52540099c741.png)




#### Example code 2: Only show some message actions


Only show `copy` and `recall` operations, hide other operations.
``` typescript
<template>
  <MessageList :messageActionList="actions" />
</template>


<script lang="ts" setup>
import { MessageList, useMessageActions } from '@tencentcloud/chat-uikit-vue3';


const actions = useMessageActions(['copy', 'recall']);
</script>
```


example effect


![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100033438418/d481cee988a811f0b321525400e889b2.png)


#### Example code 3: Customize message action style and logic


Here is an example of a custom forward operation:
1. Change the tag to 'Forward ⚠️'


2. Change the color to orange


3. Only messages from others can be forwarded


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


   example effect


   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100033438418/9aa48621824811f0b1df52540044a08e.png)




#### Example code 4: Add new custom message action


Assume messages need to be customized, such as only allowing others' sent messages to be tagged as 'like', and inserting this after the 'undo' operation.
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
    Implement the like logic here, for example by calling the backend API
  },
};


const actions = useMessageActions(['forward', 'copy', 'recall', customLikeAction, 'quote', 'delete']);
</script>
```


example effect


![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100033438418/9f5aa2e4824b11f0a8ae5254005ef0f7.png)




### filter
- type:((message: MessageModel) => boolean) | undefined


-A custom filter function for filtering messages before list rendering. The function receives a `MessageModel` message object and returns a boolean value. If it returns `true`, the message will be displayed; if `false`, the message will not be displayed. The default value is `undefined`, meaning no additional filtering is performed (but the component will filter out messages with `isDeleted` set to `true` by default).




#### Example code: Filter out text messages sent by robots


This example shows how to use the `filter` prop to filter out specific messages sent by users.
``` typescript
<template>
  <MessageList :filter="customMessageFilter" />
</template>


<script lang="ts" setup>
import { MessageList, MessageType } from '@tencentcloud/chat-uikit-vue3';
import type { MessageModel } from '@tencentcloud/chat-uikit-vue3';


// Define custom message filter function
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
- Type: Component | undefined


-Description: Custom render for individual messages in the message list.




   If you need full control over message display style and internal logic, you can pass in a Vue component to replace the default message rendering. The custom component will receive props like `message` (IMessageModel type), `alignment`, and `messageActionList`. By default, the internal default message component `Message` is used.




#### Example code: CUSTOM message component for message click redirection


This example shows how to create a custom message component to render specific `CUSTOM` messages (`businessID` as `text_link`) as clickable URLs.
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
    // MessageList will pass other props, which can be received as needed, such as alignment, messageActionList
  },
  setup(props) {
    return () => {
      const { message } = props;


      if (message.type === MessageType.CUSTOM as any) {
        const { businessID, ...restData } = JSON.parse(message.payload.data);
        if (businessID === 'text_link') {
          return h('div', { class: 'custom-text-link-message' }, [
            h('div', restData.text),
            h('a', { href: restData.link, target: '_blank' }, `Redirect to external website address ${restData.link}`),
          ]);
        }
      }
      Other message types use the default message component
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


example effect


![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100033438418/abd6f2ea825411f0b1df52540044a08e.png)




### MessageTimeDivider
- Type: Component | undefined


- Description: for custom rendering time segmentation component.




   You can pass in a Vue component to replace the default time divider rendering. The custom component will receive props like `currentMessage` (the associated message of the current time divider) and `previousMessage` (the previous message), and can determine the display logic and style based on this information. By default, it uses the internal `MessageTimeDivider` component.


   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100033438418/4d5e72b688ae11f0974b52540044a08e.png)




#### Example code: Custom time divider component to display whether it's working hours


This example shows how to create a custom time dividing line component, determine whether the time of the last message is a working hour, and display the appropriate tag and color.
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


    // Display only when crossing days or the interval exceeds 4 hours
    const shouldShow = currentTime.toDateString() !== prevTime.toDateString()
      || (currentTime.getTime() - prevTime.getTime()) > 4 * 60 * 60 * 1000;


    if (!shouldShow) {
      return () => null;
    }


    Working hours (9:00-18:00, Monday through Friday)
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


example effect


![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100033438418/1de6fe94825711f0a8ae5254005ef0f7.png)




supplementary information


Common fields of the `MessageModel` type:
``` typescript
// API definition for MessageModel, see the @tencentcloud/chat-uikit-engine document for details
// This is a complex message model containing properties such as message ID, event type, sender, content, time, and status.
Sample structure (not a complete definition)
interface MessageModel {
  ID: string;
  conversationID: string;
  type: MessageType;
  payload: any;
  flow: 'in' | 'out';
  from: string;
  to: string;
  time: number; // Unix timestamp (seconds)
  status: 'unSend' | 'success' | 'fail';
  isDeleted: boolean;
  isRevoked: boolean;
  hasRiskContent: boolean; // whether the content contains risk
  // ... other attributes
}


enum MessageType {
  TEXT,     // Text
  IMAGE
  AUDIO,    // Audio
  VIDEO,    // Video
  FILE,     // File
  FACE,     // Large Sticker
  LOCATION, // Location
  GRP_TIP,  // Group prompt
  CUSTOM,   // Custom
  MERGER,   // Combine and forward
}


```


For the complete content of MessageModel, see the [TUIChatEngine reference document](https://web.sdk.qcloud.com/im/doc/chat-engine/IMessageModel.html).


Reference
- [Customize Component - UIKitProvider](https://write.woa.com/document/187032638782849024)


- [Customize Component - ConversationList](https://write.woa.com/document/186960319111872512)


- [Customize Component - Chat](https://write.woa.com/document/187778215983329280)


- [Customize Component - MessageInput](https://write.woa.com/document/187058763983568896)


- [Customize Component - ChatSetting](https://write.woa.com/document/187321409859108864)


- [Customize Component - ContactList](https://write.woa.com/document/187595466274463744)


- [Customize Component - Search](https://write.woa.com/document/187595449195040768)


- [chat-uikit-vue3 npm](https://www.npmjs.com/package/@tencentcloud/chat-uikit-vue3)


- [github Demo](https://github.com/Tencent-RTC/TUIKit_Vue3/tree/main/demos/rtcube-vite-vue3)
