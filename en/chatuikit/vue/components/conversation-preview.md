> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/en/llms.txt
> Use this file to discover all available pages before exploring further.

## Overview

The ConversationPreview component is used to preview a single conversation in the conversation list. It is responsible for displaying conversation information, unread count, and providing conversation operation functionality.

With this component, you can freely design and combine the ConversationPreview layout you expect. Additionally, you can customize the behavior when selecting a conversation through the `@select-conversation` event.

## Custom Usage

You can use the `Preview` prop of `ConversationList` to customize the preview item for each conversation in the conversation list. If the `Preview` prop is not specified, the system will use the `ConversationPreviewUI` component by default.
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
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Default</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**conversation***(Required)*</td>

<td rowspan="1" colSpan="1" >ConversationModel</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Required parameter, identifies the current rendered conversation list item</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >isSelected</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >false</td>

<td rowspan="1" colSpan="1" >Controls whether the conversation list item UI is in selected state</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enableActions</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >true</td>

<td rowspan="1" colSpan="1" >Controls whether conversation actions are displayed</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >actionsConfig</td>

<td rowspan="1" colSpan="1" >ConversationActionsConfig</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Used to customize conversation actions configuration</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >highlightMatchString</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Highlight match keyword for conversation list item title, commonly used for conversation search result highlighting</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Preview</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >ConversationPreviewUI</td>

<td rowspan="1" colSpan="1" >Custom preview component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Avatar</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >Avatar</td>

<td rowspan="1" colSpan="1" >Renders conversation list item avatar area</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ConversationActions</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >ConversationActions</td>

<td rowspan="1" colSpan="1" >Renders conversation list item actions area</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >className</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >CSS custom class name for root element</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >style</td>

<td rowspan="1" colSpan="1" >CSSProperties</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Custom style for root element</td>
</tr>
</table>


### ConversationPreviewUIProps
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Default</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**conversation***(Required)*</td>

<td rowspan="1" colSpan="1" >ConversationModel</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Required parameter, identifies the current rendered conversation list item</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >isSelected</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >false</td>

<td rowspan="1" colSpan="1" >Controls whether the conversation list item UI is in selected state</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enableActions</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >true</td>

<td rowspan="1" colSpan="1" >Controls whether conversation actions are displayed</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >actionsConfig</td>

<td rowspan="1" colSpan="1" >ConversationActionsConfig</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Used to customize conversation actions configuration</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >highlightMatchString</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Highlight match keyword for conversation list item title</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Title</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >ConversationPreviewTitle</td>

<td rowspan="1" colSpan="1" >Renders conversation list item title area</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >LastMessageAbstract</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >ConversationPreviewAbstract</td>

<td rowspan="1" colSpan="1" >Renders conversation list item last message abstract area</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >LastMessageTimestamp</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >ConversationPreviewTimestamp</td>

<td rowspan="1" colSpan="1" >Renders conversation list item last message timestamp area</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Unread</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >ConversationPreviewUnread</td>

<td rowspan="1" colSpan="1" >Renders conversation list item unread badge area</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ConversationActions</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >ConversationActions</td>

<td rowspan="1" colSpan="1" >Renders conversation list item actions area</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Avatar</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >Avatar</td>

<td rowspan="1" colSpan="1" >Renders conversation list item avatar area</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >className</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >CSS custom class name for root element</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >style</td>

<td rowspan="1" colSpan="1" >CSSProperties</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Custom style for root element</td>
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
<td rowspan="1" colSpan="1" >select-conversation</td>

<td rowspan="1" colSpan="1" >(conversation: ConversationModel)</td>

<td rowspan="1" colSpan="1" >Event triggered when selecting a conversation in the conversation list</td>
</tr>
</table>


## Example: Discord-like Style Customization

Discord is a popular chat application, similar to Skype or Telegram. The chat content in Discord is shown in the image below:

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/869205f6832e11f0ae9d5254001c06ec.png)


By customizing the layout, functionality, and styles of `ConversationPreview`, we can quickly achieve a Discord-like effect.
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

The customized `ConversationListPreview` effect is as follows:
<table>
<tr>
<td rowspan="1" colSpan="1" >**Before**</td>

<td rowspan="1" colSpan="1" >**After**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/fbafa8ff832e11f0b321525400e889b2.png)</td>

<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/a2cf5090832e11f0ae9d5254001c06ec.png)</td>
</tr>
</table>
