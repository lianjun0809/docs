> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

## 概述

ConversationPreview 组件用于预览会话列表中的单个会话。它负责显示会话信息、未读数，并提供会话操作功能。

借助该组件，您可以自由地设计和组合出您所期望的 ConversationPreview 布局。此外，您还可以通过 `@select-conversation` 事件自定义选中会话时的行为。

## 自定义用法

您可以使用 `ConversationList `的 `Preview` prop 来自定义会话列表中每个会话的预览项。如果未指定 `Preview` prop，系统将默认使用 `ConversationPreviewUI` 组件。
``` typescript
<template>
  <div class="custom-preview">
    <div class="content">
      <h4>Custom Preview</h4>
      <p>{{ conversation?.getShowName() }}</p>
    </div>
  </div>
</template>

<script lang="ts" setup>
import type { ConversationModel } from '@tencentcloud/chat-uikit-vue3';

interface Props {
  conversation?: ConversationModel;
}

const props = withDefaults(defineProps<Props>(), {});
</script>
```
``` typescript
<template>
  <ConversationList :Preview="CustomConversationPreview" />
</template>

<script setup lang="ts">
import { ConversationList } from '@tencentcloud/chat-uikit-vue3';
import CustomConversationPreview from './CustomConversationPreview.vue';
</script>
```

## Props

### ConversationPreviewProps
<table>
<tr>
<td rowspan="1" colSpan="1" >参数名</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >默认值</td>

<td rowspan="1" colSpan="1" >说明</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**conversation***(Required)*</td>

<td rowspan="1" colSpan="1" >ConversationModel</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >必选参数，标识当前渲染的会话列表项</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >isSelected</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >false</td>

<td rowspan="1" colSpan="1" >控制会话列表项 UI 是否处于选中状态</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enableActions</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >true</td>

<td rowspan="1" colSpan="1" >控制会话操作功能是否显示</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >actionsConfig</td>

<td rowspan="1" colSpan="1" >ConversationActionsConfig</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >用于自定义会话操作配置</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >highlightMatchString</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >会话列表项 Title 高亮匹配关键词，常用于会话搜索结果高亮</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Preview</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >ConversationPreviewUI</td>

<td rowspan="1" colSpan="1" >自定义预览组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Avatar</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >Avatar</td>

<td rowspan="1" colSpan="1" >渲染会话列表项头像区域</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ConversationActions</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >ConversationActions</td>

<td rowspan="1" colSpan="1" >渲染会话列表项会话操作区域</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >className</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >指定根元素类的 CSS 自定义名称</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >style</td>

<td rowspan="1" colSpan="1" >CSSProperties</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >指定根元素样式的自定义样式</td>
</tr>
</table>


### ConversationPreviewUIProps
<table>
<tr>
<td rowspan="1" colSpan="1" >参数名</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >默认值</td>

<td rowspan="1" colSpan="1" >说明</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**conversation***(Required)*</td>

<td rowspan="1" colSpan="1" >ConversationModel</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >必选参数，标识当前渲染的会话列表项</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >isSelected</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >false</td>

<td rowspan="1" colSpan="1" >控制会话列表项 UI 是否处于选中状态</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enableActions</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >true</td>

<td rowspan="1" colSpan="1" >控制会话操作功能是否显示</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >actionsConfig</td>

<td rowspan="1" colSpan="1" >ConversationActionsConfig</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >用于自定义会话操作配置</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >highlightMatchString</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >会话列表项 Title 高亮匹配关键词</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Title</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >ConversationPreviewTitle</td>

<td rowspan="1" colSpan="1" >渲染会话列表项标题区域</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >LastMessageAbstract</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >ConversationPreviewAbstract</td>

<td rowspan="1" colSpan="1" >渲染会话列表项最新消息摘要区域</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >LastMessageTimestamp</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >ConversationPreviewTimestamp</td>

<td rowspan="1" colSpan="1" >渲染会话列表项最新消息时间戳区域</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Unread</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >ConversationPreviewUnread</td>

<td rowspan="1" colSpan="1" >渲染会话列表项消息未读标识区域</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ConversationActions</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >ConversationActions</td>

<td rowspan="1" colSpan="1" >渲染会话列表项会话操作区域</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Avatar</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >Avatar</td>

<td rowspan="1" colSpan="1" >渲染会话列表项头像区域</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >className</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >指定根元素类的 CSS 自定义名称</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >style</td>

<td rowspan="1" colSpan="1" >CSSProperties</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >指定根元素样式的自定义样式</td>
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
<td rowspan="1" colSpan="1" >select-conversation</td>

<td rowspan="1" colSpan="1" >(conversation: ConversationModel)</td>

<td rowspan="1" colSpan="1" >指定在选择对话列表中的对话时接收回调的事件</td>
</tr>
</table>


## 示例：自定义类 Discord 风格

Discord 是一个流行的聊天应用程序，类似于 Skype 或 Telegram。Discord 中的聊天内容如下图所示:

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/869205f6832e11f0ae9d5254001c06ec.png)


通过对 `ConversationPreview` 布局、功能以及样式的定制，我们可以快速实现类 Discord 效果。
``` java
<template>
  <div
    :class="[
      'discord-preview-ui',
      {
        'conversationPreview--active': activeConversation?.conversationID === props.conversation.conversationID,
      }
    ]"
    @click="handleSelectConversation"
  >
    <label class="discord-preview-ui__tag">
      #
    </label>
    <span class="discord-preview-ui__title">{{ conversation?.getShowName() }}</span>
  </div>
</template>

<script lang="ts" setup>
import { useConversationListState } from '@tencentcloud/chat-uikit-vue3';
import type { ConversationModel } from '@tencentcloud/chat-uikit-vue3';

const { setActiveConversation, activeConversation } = useConversationListState();

interface Props {
  conversation: ConversationModel;
}

const emit = defineEmits<{
  selectConversation: [conversation: ConversationModel];
}>();

const props = withDefaults(defineProps<Props>(), {});

const handleSelectConversation = () => {
  setActiveConversation(props.conversation.conversationID);
  emit('selectConversation', props.conversation);
};
</script>
<style scoped>
.discord-style-app {
  background-color: #2f3136;
  padding: 20px;
  border-radius: 8px;
}

.discord-conversation-list {
  background-color: #2f3136;
}

.discord-preview-ui {
  height: 34px;
  border-radius: 4px;
  padding: 6px 8px;
  margin: 1px 8px;
  display: flex;
  align-items: center;
  cursor: pointer;
  transition: all 0.15s ease;
  position: relative;
}

.discord-preview-ui__tag {
  margin-right: 6px;
  font-size: 16px;
  color: #8e9297;
  font-weight: 600;
  line-height: 1;
}

.discord-preview-ui__title {
  font-size: 16px;
  color: #8e9297;
  font-weight: 500;
  line-height: 1.2;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  flex: 1;
}

.discord-preview-ui:hover {
  background-color: #393c43;
}

.discord-preview-ui:hover .discord-preview-ui__tag,
.discord-preview-ui:hover .discord-preview-ui__title {
  color: #dcddde;
}

.conversationPreview--active {
  background-color: #404249 !important;
}

.conversationPreview--active .discord-preview-ui__tag,
.conversationPreview--active .discord-preview-ui__title {
  color: #ffffff !important;
}

.discord-preview-ui::before {
  content: '';
  position: absolute;
  left: 0;
  top: 50%;
  transform: translateY(-50%);
  width: 4px;
  height: 8px;
  background-color: #ffffff;
  border-radius: 0 4px 4px 0;
  opacity: 0;
  transition: opacity 0.15s ease;
}
</style>

```
``` typescript
<template>
  <ConversationList :Preview="CustomConversationPreview" />
</template>

<script setup lang="ts">
import { ConversationList } from '@tencentcloud/chat-uikit-vue3';
import CustomConversationPreview from './CustomConversationPreview.vue';
</script>
```

`ConversationListPreview` 定制后效果如下：
<table>
<tr>
<td rowspan="1" colSpan="1" >**修改前**</td>

<td rowspan="1" colSpan="1" >**修改后**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/fbafa8ff832e11f0b321525400e889b2.png)</td>

<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/a2cf5090832e11f0ae9d5254001c06ec.png)</td>
</tr>
</table>
