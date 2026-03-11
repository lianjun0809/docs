> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/en/llms.txt
> Use this file to discover all available pages before exploring further.

## Overview

The ConversationActions component handles operations for a single conversation, supporting delete, pin, mute, and mark unread/read by default.

## Basic Usage

In `ConversationList`, you can quickly customize conversation actions using the `actionsConfig` prop.
``` typescript
<template>
  <UIKitProvider>
    <ConversationList :actions-config="actionsConfig" />
  </UIKitProvider>
</template>

<script setup lang="ts">
import { UIKitProvider, ConversationList } from '@tencentcloud/chat-uikit-vue3';
import type { ConversationModel } from '@tencentcloud/chat-uikit-vue3';

const actionsConfig = {
  enablePin: false,
  onConversationDelete: (conversation: ConversationModel) => { 
    console.log('Delete conversation success'); 
  },
  customConversationActions: {
    'custom-actions-1': {
      label: 'custom-actions',
      onClick: (conversation: ConversationModel) => { 
        console.log(conversation); 
      },
    },
  },
};
</script>
```

## Advanced Usage

For deeper customization, you can directly replace the `ConversationActions` prop of `ConversationList`.
``` typescript
<template>
  <UIKitProvider>
    <ConversationList
      :ConversationActions="CustomConversationActions"
    />
  </UIKitProvider>
</template>

<script setup lang="ts">
import { defineComponent } from 'vue';
import { UIKitProvider, ConversationList, ConversationActions } from '@tencentcloud/chat-uikit-vue3';
import type { ConversationActionsProps } from '@tencentcloud/chat-uikit-vue3';

const CustomConversationActions = defineComponent({
  name: 'CustomConversationActions',
  setup(props: ConversationActionsProps) {
    return () => h(ConversationActions, {
      ...props,
      enableDelete: false
    });
  }
});
</script>
```

## Props

The `ConversationActionsProps` interface type for the ConversationActions component extends from the `ConversationActionsConfig` interface.

### ConversationActionsProps
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Default</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >conversation(Required)</td>

<td rowspan="1" colSpan="1" >ConversationModel</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Required parameter, represents the conversation for the current rendered conversation action</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >className</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Custom class name for root element</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >style</td>

<td rowspan="1" colSpan="1" >CSSProperties</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Custom style for root element</td>
</tr>
</table>


### ConversationActionsConfig
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Default</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enablePin</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >true</td>

<td rowspan="1" colSpan="1" >Whether to show the pin action button</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enableMute</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >true</td>

<td rowspan="1" colSpan="1" >Whether to show the mute action button</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enableDelete</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >true</td>

<td rowspan="1" colSpan="1" >Whether to show the delete action button</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enableMarkUnread</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >true</td>

<td rowspan="1" colSpan="1" >Whether to show the mark unread action button</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onMarkConversationUnread</td>

<td rowspan="1" colSpan="1" >(conversation: ConversationModel, e?: Event) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Custom callback for marking conversation as unread/read</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onConversationPin</td>

<td rowspan="1" colSpan="1" >(conversation: ConversationModel, e?: Event) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Custom callback for pinning/unpinning conversation</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onConversationMute</td>

<td rowspan="1" colSpan="1" >(conversation: ConversationModel, e?: Event) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Custom callback for muting/unmuting conversation</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onConversationDelete</td>

<td rowspan="1" colSpan="1" >(conversation: ConversationModel, e?: Event) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Custom callback for deleting conversation</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >customConversationActions</td>

<td rowspan="1" colSpan="1" >Record<string, ConversationActionItem></td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Custom conversation action items</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >PopupIcon</td>

<td rowspan="1" colSpan="1" >any</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Custom icon for action popup</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >PopupElements</td>

<td rowspan="1" colSpan="1" >any[]</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Custom content for action popup</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onClick</td>

<td rowspan="1" colSpan="1" >(e: Event, key?: string, conversation?: ConversationModel) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Callback when clicking action item</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onClose</td>

<td rowspan="1" colSpan="1" >() => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Callback when closing action popup (H5 only)</td>
</tr>
</table>


### ConversationActionItem
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Default</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enable</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >true</td>

<td rowspan="1" colSpan="1" >Whether to enable the custom action item</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >label</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Display content for custom action item</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onClick</td>

<td rowspan="1" colSpan="1" >(conversation: ConversationModel, e?: Event) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Callback when clicking custom action item</td>
</tr>
</table>


## Events
<table>
<tr>
<td rowspan="1" colSpan="1" >Event Name</td>

<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >click</td>

<td rowspan="1" colSpan="1" >(e: Event, key?: string, conversation?: ConversationModel)</td>

<td rowspan="1" colSpan="1" >Triggered when clicking an action item</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >close</td>

<td rowspan="1" colSpan="1" >()</td>

<td rowspan="1" colSpan="1" >Triggered when closing the action popup</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >markConversationUnread</td>

<td rowspan="1" colSpan="1" >(conversation: ConversationModel, e?: Event)</td>

<td rowspan="1" colSpan="1" >Triggered when marking conversation as unread/read</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >conversationPin</td>

<td rowspan="1" colSpan="1" >(conversation: ConversationModel, e?: Event)</td>

<td rowspan="1" colSpan="1" >Triggered when pinning/unpinning conversation</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >conversationMute</td>

<td rowspan="1" colSpan="1" >(conversation: ConversationModel, e?: Event)</td>

<td rowspan="1" colSpan="1" >Triggered when muting/unmuting conversation</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >conversationDelete</td>

<td rowspan="1" colSpan="1" >(conversation: ConversationModel, e?: Event)</td>

<td rowspan="1" colSpan="1" >Triggered when deleting conversation</td>
</tr>
</table>


## Custom Components

### Basic Feature Toggles

By setting `enablePin`, `enableDelete`, `enableMute`, and `enableMarkUnread` parameters, you can flexibly control the display of conversation pin, mute, delete, and mark unread in `ConversationActions`.
``` typescript
<template>
  <!-- Disable pin feature -->
  <ConversationActions :enablePin="false" :conversation="conversation" />

  <!-- Disable delete feature -->
  <ConversationActions :enableDelete="false" :conversation="conversation" />

  <!-- Disable mute feature -->
  <ConversationActions :enableMute="false" :conversation="conversation" />

  <!-- Disable mark unread feature -->
  <ConversationActions :enableMarkUnread="false" :conversation="conversation" />
</template>
```
<table>
<tr>
<td rowspan="1" colSpan="1" >`enablePin: false`</td>

<td rowspan="1" colSpan="1" >`enableDelete: false`</td>

<td rowspan="1" colSpan="1" >`enableMute: false`</td>

<td rowspan="1" colSpan="1" > enableMarkUnread="false"</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/f47a44ba824d11f0ac3c525400e889b2.png)</td>

<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/20ee3ea6824e11f0b1df52540044a08e.png)</td>

<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/31a0a7da825011f0b1df52540044a08e.png)</td>

<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/a9273911833211f097755254007c27c5.png)</td>
</tr>
</table>


### Event Handling

The ConversationActions component supports conversation delete, pin/unpin, mute/unmute, and mark unread/read by default. If the existing event handling doesn't meet your needs, you can customize and override the event handling functions. In addition to customizing event handling, you can also get basic click events through `@click`.
``` typescript
<template>
  <ConversationList :conversation-actions="CustomConversationActions" />
</template>

<script setup lang="ts">
import { defineComponent, h } from 'vue';
import { ConversationActions, Toast } from '@tencentcloud/chat-uikit-vue3';
import type { ConversationActionsProps, ConversationModel } from '@tencentcloud/chat-uikit-vue3';

const CustomConversationActions = defineComponent({
  name: 'CustomConversationActions',
  setup(props: ConversationActionsProps) {
    const handleConversationDelete = (conversation: ConversationModel) => {
      conversation.deleteConversation().then(() => {
        console.log('delete conversation successfully!');
      }).catch(() => {
        console.log('delete conversation failed!');
      });
    };

    return () => h(ConversationActions, {
      ...props,
      onConversationDelete: handleConversationDelete
    });
  }
});
</script>
```

### Custom Actions

customConversationActions is used to add custom action items to ConversationActions.

**Example: Add Custom Action Item**
``` typescript
<template>
  <ConversationList :ConversationActions="CustomConversationActions" />
</template>

<script setup lang="ts">
import { defineComponent, h } from 'vue';
import { ConversationActions } from '@tencentcloud/chat-uikit-vue3';
import type { ConversationActionsProps, ConversationModel } from '@tencentcloud/chat-uikit-vue3';

const CustomConversationActions = defineComponent({
  name: 'CustomConversationActions',
  setup(props: ConversationActionsProps) {
    return () => h(ConversationActions, {
      ...props,
      customConversationActions: {
        'custom-actions-1': {
          label: 'custom-actions',
          onClick: (conversation: ConversationModel) => { 
            console.log(conversation); 
          },
        },
      }
    });
  }
});
</script>
```

### UI Customization

You can customize the popup trigger button style through the `PopupIcon` parameter, and customize the popup content through `PopupElements`.

**Example: Custom Trigger Button**
``` typescript
<template>
  <ConversationList :ConversationActions="CustomConversationActions" />
</template>

<script setup lang="ts">
import { defineComponent, h } from 'vue';
import { ConversationActions } from '@tencentcloud/chat-uikit-vue3';
import type { ConversationActionsProps } from '@tencentcloud/chat-uikit-vue3';

const CustomConversationActions = defineComponent({
  name: 'CustomConversationActions',
  setup(props: ConversationActionsProps) {
    const customIcon = h('div', '自定义 Icon');

    return () => h(ConversationActions, {
      ...props,
      PopupIcon: customIcon
    });
  }
});
</script>
```
