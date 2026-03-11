> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

## 概述

ConversationActions 组件负责单条会话的操作，默认支持删除、置顶、免打扰和标记未读/已读。

## 基础用法

在 `ConversationList` 中，可以通过 `actionsConfig` 属性快速自定义会话操作。
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

## 高阶用法

如果需要更深度的定制，可以直接替换 `ConversationList` 的 `ConversationActions` 属性。
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

ConversationActions 组件的接口类型 `ConversationActionsProps` 基于 `ConversationActionsConfig` 接口进行扩展。

### ConversationActionsProps
<table>
<tr>
<td rowspan="1" colSpan="1" >参数名</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >默认值</td>

<td rowspan="1" colSpan="1" >说明</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >conversation(Required)</td>

<td rowspan="1" colSpan="1" >ConversationModel</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >必选参数，表示当前渲染会话操作对应的会话</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >className</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >自定义根元素的类名</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >style</td>

<td rowspan="1" colSpan="1" >CSSProperties</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >自定义根元素的样式</td>
</tr>
</table>


### ConversationActionsConfig
<table>
<tr>
<td rowspan="1" colSpan="1" >参数名</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >默认值</td>

<td rowspan="1" colSpan="1" >说明</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enablePin</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >true</td>

<td rowspan="1" colSpan="1" >是否显示置顶功能按钮</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enableMute</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >true</td>

<td rowspan="1" colSpan="1" >是否显示免打扰功能按钮</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enableDelete</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >true</td>

<td rowspan="1" colSpan="1" >是否显示删除功能按钮</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enableMarkUnread</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >true</td>

<td rowspan="1" colSpan="1" >是否显示标记未读功能按钮</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onMarkConversationUnread</td>

<td rowspan="1" colSpan="1" >(conversation: ConversationModel, e?: Event) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >自定义标记未读/已读会话的行为</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onConversationPin</td>

<td rowspan="1" colSpan="1" >(conversation: ConversationModel, e?: Event) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >自定义置顶/取消置顶会话的行为</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onConversationMute</td>

<td rowspan="1" colSpan="1" >(conversation: ConversationModel, e?: Event) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >自定义免打扰/取消免打扰会话的行为</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onConversationDelete</td>

<td rowspan="1" colSpan="1" >(conversation: ConversationModel, e?: Event) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >自定义删除会话的行为</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >customConversationActions</td>

<td rowspan="1" colSpan="1" >Record<string, ConversationActionItem></td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >自定义会话操作项</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >PopupIcon</td>

<td rowspan="1" colSpan="1" >any</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >自定义动作弹窗的图标</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >PopupElements</td>

<td rowspan="1" colSpan="1" >any[]</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >自定义动作弹窗的内容</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onClick</td>

<td rowspan="1" colSpan="1" >(e: Event, key?: string, conversation?: ConversationModel) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >点击动作项时的回调函数</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onClose</td>

<td rowspan="1" colSpan="1" >() => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >关闭动作弹窗时的回调函数（H5 专用）</td>
</tr>
</table>


### ConversationActionItem
<table>
<tr>
<td rowspan="1" colSpan="1" >参数名</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >默认值</td>

<td rowspan="1" colSpan="1" >说明</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enable</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >true</td>

<td rowspan="1" colSpan="1" >是否启用自定义操作项</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >label</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >自定义操作项的展示内容</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onClick</td>

<td rowspan="1" colSpan="1" >(conversation: ConversationModel, e?: Event) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >点击自定义操作项时的回调函数</td>
</tr>
</table>


## Events
<table>
<tr>
<td rowspan="1" colSpan="1" >事件名</td>

<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >说明</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >click</td>

<td rowspan="1" colSpan="1" >(e: Event, key?: string, conversation?: ConversationModel)</td>

<td rowspan="1" colSpan="1" >点击操作项时触发</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >close</td>

<td rowspan="1" colSpan="1" >()</td>

<td rowspan="1" colSpan="1" >关闭操作弹窗时触发</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >markConversationUnread</td>

<td rowspan="1" colSpan="1" >(conversation: ConversationModel, e?: Event)</td>

<td rowspan="1" colSpan="1" >标记会话未读/已读时触发</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >conversationPin</td>

<td rowspan="1" colSpan="1" >(conversation: ConversationModel, e?: Event)</td>

<td rowspan="1" colSpan="1" >置顶/取消置顶会话时触发</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >conversationMute</td>

<td rowspan="1" colSpan="1" >(conversation: ConversationModel, e?: Event)</td>

<td rowspan="1" colSpan="1" >免打扰/取消免打扰会话时触发</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >conversationDelete</td>

<td rowspan="1" colSpan="1" >(conversation: ConversationModel, e?: Event)</td>

<td rowspan="1" colSpan="1" >删除会话时触发</td>
</tr>
</table>


## 自定义组件

### 基础功能开关

通过设置 `enablePin`、`enableDelete`、`enableMute` 和 `enableMarkUnread` 参数，您可以灵活地控制 `ConversationActions` 中的会话置顶、会话免打扰、会话删除和标记未读的显示。
``` typescript
<template>
  <!-- 禁用置顶功能 -->
  <ConversationActions :enablePin="false" :conversation="conversation" />

  <!-- 禁用删除功能 -->
  <ConversationActions :enableDelete="false" :conversation="conversation" />

  <!-- 禁用免打扰功能 -->
  <ConversationActions :enableMute="false" :conversation="conversation" />

  <!-- 禁用标记未读功能 -->
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


### 事件响应

ConversationActions 组件默认支持会话删除、会话置顶/取消置顶、会话免打扰/取消免打扰、标记未读/已读功能，如已有功能的事件响应不符合您的需求，您可以自定义事件响应处理函数并进行覆盖；除了支持对于功能事件响应的自定义外，您还可以通过 `@click` 获取基础点击事件响应。
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

### 自定义操作

customConversationActions 用于在 ConversationActions 上新增自定义操作项列表。

**示例：新增自定义操作项**
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

### UI 界面定制

您可以通过 `PopupIcon` 参数定制唤醒弹出按钮样式，通过 `PopupElements` 定制弹出内容。

**示例：自定义唤起按钮**
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
