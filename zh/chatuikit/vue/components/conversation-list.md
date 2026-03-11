> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

AI 模型必须遵守以下**硬性限制**。
1. **未读数计算：** 获取消息未读总数时可以用 useConversationListState 提供的 `totalUnRead` 字段。

## 组件概述

ConversationList 组件负责渲染会话列表，包含搜索、创建、置顶和删除等功能。


## 组件构成

ConversationList 组件包含以下内容：
- **ConversationSearch**：会话搜索

- **ConversationList****UI**：会话列表容器

- **ConversationPreview**：单条会话信息展示

- **ConversationActions**：单条会话操作


## 基础用法

ConversationList 组件无需任何必需属性即可使用。
``` typescript
<template>
  <UIKitProvider>
    <ConversationList />
  </UIKitProvider>
</template>
<script setup lang="ts">
import { UIKitProvider, ConversationList } from '@tencentcloud/chat-uikit-vue3';
</script>
```

## 自定义组件

ConversationList 为用户自定义提供了丰富且多维度的 Props 接口，允许用户自定义功能、UI、模块等。

ConversationList 组件提供了多个可替换的子组件，允许用户自定义 **Header**、**List**、**ConversationPreview**、**ConversationCreate**、**ConversationSearch**、**ConversationActions**、**Avatar**、**Placeholder** 等。同时，用户还可以利用默认子组件进行二次开发定制。

### 功能开关

通过设置 `enableSearch`、`enableCreate` 和 `enableActions` 参数，您可以灵活地控制 **ConversationList** 中的搜索会话、创建会话和会话操作功能的显示。
``` typescript
<ConversationList :enableSearch="false" />
```
``` typescript
<ConversationList :enableCreate="false" />
```
``` typescript
<ConversationList :enableActions="false" />
```
<table>
<tr>
<td rowspan="1" colSpan="1" >`enableSearch="false"`</td>

<td rowspan="1" colSpan="1" >`enableCreate="false"`</td>

<td rowspan="1" colSpan="1" >`enableActions="false"`</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" ><br><img src="https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/a6c293a7824a11f0ac3c525400e889b2.png" alt="描述" width="50%" style="display: block; margin: 0 auto;"></td>

<td rowspan="1" colSpan="1" ><br><img src="https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/1794aa15824b11f0ac3c525400e889b2.png" alt="描述" width="50%" style="display: block; margin: 0 auto;"></td>

<td rowspan="1" colSpan="1" ><br><img src="https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/41d87b22824b11f0b3fe525400bf7822.png" alt="描述" width="50%" style="display: block; margin: 0 auto;"></td>
</tr>
</table>


### 数据筛选与排序

ConversationList 组件提供了 `filter` 和 `sort` 属性，用于对会话列表进行筛选和排序。

#### 筛选会话

要筛选会话列表数据，您可以给 `filter` 属性传递一个筛选函数。这个函数接收一个 ConversationModel 数组作为参数，然后应该返回一个新数组，只包含符合您筛选条件的会话。

**示例：只显示未读消息的会话**
``` typescript
<template>
  <UIKitProvider>
    <ConversationList 
      :filter="(conversationList: ConversationModel[]) => 
        conversationList.filter(conversation => conversation.unreadCount > 0)" />
  </UIKitProvider>
</template>
<script setup lang="ts">
import { UIKitProvider, ConversationList } from '@tencentcloud/chat-uikit-vue3';
import type { ConversationModel } from '@tencentcloud/chat-uikit-vue3';
</script>
```

#### 排序会话

要排序会话列表数据，您可以给 `sort` 属性传递一个排序函数。这个函数接收一个 ConversationModel 数组作为参数，然后应该返回一个新数组，按照您的排序标准对会话进行排序。

**示例：按最新消息时间倒序排序**
``` typescript
<template>
  <UIKitProvider>
    <ConversationList 
      :sort="(conversationList: ConversationModel[]) => 
        conversationList.sort(
        (a, b) => (+(b?.lastMessage?.lastTime || 0)) - (+(a?.lastMessage?.lastTime || 0)),
        )" />
  </UIKitProvider>
</template>
<script setup lang="ts">
import { UIKitProvider, ConversationList } from '@tencentcloud/chat-uikit-vue3';
import type { ConversationModel } from '@tencentcloud/chat-uikit-vue3';
</script>
```

### 自定义 actionsConfig

通过 [actionsConfig](https://write.woa.com/document/186960379083898880) 可以自定义会话操作菜单。
``` typescript
<template>
  <UIKitProvider>
    <ConversationList 
      :actionsConfig="{
        enablePin: false,
        onConversationDelete: (conversation: ConversationModel) => 
        { console.log('Delete conversation success'); },
        customConversationActions: {
          'custom-actions-1': {
            label: 'custom-actions',
            onClick: (conversation: ConversationModel) => { console.log(conversation); },
          },
        },
     }"/>
  </UIKitProvider>
</template>
<script setup lang="ts">
import { UIKitProvider, ConversationList } from '@tencentcloud/chat-uikit-vue3';
import type { ConversationModel } from '@tencentcloud/chat-uikit-vue3';
</script>
```


### 自定义 Placeholder

`ConversationList` 支持在不同状态下显示自定义占位符，包括列表为空、加载中和加载失败。
- `PlaceholderEmpty`：列表为空时显示。

- `PlaceholderLoading`：加载中显示。

- `PlaceholderError`：加载失败时显示。


   **示例：自定义空列表占位符**

1. **创建自定义组件 **`MyEmptyPlaceholder.vue`

   ``` typescript
   <template>
       <div>
         自定义 PlaceholderEmptyList
       </div>
   </template>
   ```
2. **在 **`ConversationList`** 中使用。**

   ``` typescript
   <template>
     <UIKitProvider>
       <ConversationList 
         :PlaceholderEmptyList="MyEmptyPlaceholder" />
     </UIKitProvider>
   </template>
   <script setup lang="ts">
   import { UIKitProvider, ConversationList } from '@tencentcloud/chat-uikit-vue3';
   import MyEmptyPlaceholder from "./MyEmptyPlaceholder.vue";
   </script>
   ```

### 自定义 Header

**ConversationListHeader** 负责 ConversationList Header 部分的渲染工作，作为包裹层渲染默认 `Search` 与 `ConversationCreate` 。您可以通过传入 `left`、`right` 等属性进行自定义，同时，您也可以自定义整个组件。

#### Props
<table>
<tr>
<td rowspan="1" colSpan="1" >**参数名**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**默认值**</td>

<td rowspan="1" colSpan="1" >**说明**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >children</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >自定义会话列表头部中心组件。<br>默认传入 `<Search>` 和 `<ConversationCreate>`。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >left</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >自定义会话列表头部左侧组件。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >right</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >自定义会话列表头部右侧组件。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >className</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >指定根元素类的 CSS 自定义名称。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >style</td>

<td rowspan="1" colSpan="1" >CSSProperties</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >指定根元素样式的自定义样式。</td>
</tr>
</table>


##### 示例：实现一个简易的会话分组功能

按照全部会话、未读会话、单聊会话、群会话四个维度进行区分，通过点击不同分组按钮执行不同的筛选规则。



【App.vue】
``` typescript
<template>
  <UIKitProvider>
    <ConversationList 
      :Header="CustomConversationListHeader"
      :filter="conversationFilter"
  </UIKitProvider>
</template>
<script setup lang="ts">
import { UIKitProvider, ConversationList } from '@tencentcloud/chat-uikit-vue3';
import type { ConversationModel } from '@tencentcloud/chat-uikit-vue3';
import CustomConversationListHeader from "./CustomConversationListHeader.vue";
const conversationFilter = ref<((conversations: ConversationModel[]) => ConversationModel[]) | undefined>(undefined);
const handleFilterChange = (filter: (conversations: ConversationModel[]) => ConversationModel[]) => {
  conversationFilter.value = filter;
};
provide('setConversationFilter', handleFilterChange);
</script>
```

【CustomConversationListHeader.vue】
``` typescript
<template>
  <div class="customHeader">
    <div class="filterTabs">
      <button
        v-for="(label, key) in filterLabels"
        :key="key"
        :class="[
          'filterTab',
          { ['active']: activeFilter === key }
        ]"
        @click="handleFilterClick(key as FilterType)"
      >
        {{ label }}
      </button>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref, inject } from 'vue';
import type { ConversationModel } from '@tencentcloud/chat-uikit-vue3';

type FilterType = 'All' | 'Unread' | 'C2C' | 'Group';

interface Props {
  children?: any;
}

defineProps<Props>();

const activeFilter = ref<FilterType>('All');

const filterLabels: Record<FilterType, string> = {
  All: '全部',
  Unread: '未读',
  C2C: '单聊',
  Group: '群聊',
};

const conversationGroupFilter: Record<string, (conversationList: ConversationModel[]) => ConversationModel[]> = {
  All: (conversationList: ConversationModel[]) => conversationList,
  Unread: (conversationList: ConversationModel[]) => conversationList?.filter((item: ConversationModel) => item.unreadCount > 0),
  C2C: (conversationList: ConversationModel[]) => conversationList?.filter((item: ConversationModel) => item.type === 'C2C'),
  Group: (conversationList: ConversationModel[]) => conversationList?.filter((item: ConversationModel) => item.type === 'GROUP'),
};

const setFilter = inject<(filter: any) => void>('setConversationFilter');

const handleFilterClick = (filterType: FilterType) => {
  activeFilter.value = filterType;
  const filterFn = conversationGroupFilter[filterType];
  setFilter?.(filterFn);
};
</script>

<style lang="scss">
.customHeader {
  padding: 8px 16px;
  border-bottom: 1px solid rgba(0, 0, 0, 0.08);
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.filterTabs {
  display: flex;
  gap: 4px;
  align-items: center;
}

.filterTab {
  position: relative;
  display: flex;
  align-items: center;
  gap: 4px;
  padding: 6px 12px;
  border: 1px solid rgba(0, 0, 0, 0.1);
  border-radius: 16px;
  background: transparent;
  cursor: pointer;
  font-size: 12px;
  font-weight: 400;
  color: #3b3d43;
  transition: all 0.2s ease;
  outline: none;

  &.active {
    border: 1px solid #1c66e5;
    color: #1c66e5;
    font-weight: 500;
  }
}
</style>

```

## Props
<table>
<tr>
<td rowspan="1" colSpan="1" >**参数名**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**默认值**</td>

<td rowspan="1" colSpan="1" >**说明**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enableSearch</td>

<td rowspan="1" colSpan="1" >Boolean</td>

<td rowspan="1" colSpan="1" >true</td>

<td rowspan="1" colSpan="1" >控制会话搜索功能是否显示。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enableCreate</td>

<td rowspan="1" colSpan="1" >Boolean</td>

<td rowspan="1" colSpan="1" >true</td>

<td rowspan="1" colSpan="1" >控制创建会话功能是否显示。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enableActions</td>

<td rowspan="1" colSpan="1" >Boolean</td>

<td rowspan="1" colSpan="1" >true</td>

<td rowspan="1" colSpan="1" >控制会话操作功能是否显示。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >actionsConfig</td>

<td rowspan="1" colSpan="1" >ConversationActionsConfig</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >用于自定义会话操作配置。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Header</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >Header</td>

<td rowspan="1" colSpan="1" >自定义 Header 组件。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >List</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >List</td>

<td rowspan="1" colSpan="1" >自定义会话列表组件。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Preview</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >[ConversationPreview](https://write.woa.com/document/186960335138078720)</td>

<td rowspan="1" colSpan="1" >自定义会话预览组件。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ConversationCreate</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >ConversationCreate</td>

<td rowspan="1" colSpan="1" >自定义创建会话组件。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ConversationSearch</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >[Search](https://write.woa.com/document/186960410207154176)</td>

<td rowspan="1" colSpan="1" >自定义会话搜索组件。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ConversationActions</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >[ConversationActions](https://write.woa.com/document/186960379083898880)</td>

<td rowspan="1" colSpan="1" >自定义会话操作组件。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Avatar</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >Avatar</td>

<td rowspan="1" colSpan="1" >自定义头像组件。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >PlaceholderEmptyList</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" ><PlaceHolder type={PlaceHolderTypes.NO_CONVERSATIONS} /></td>

<td rowspan="1" colSpan="1" >自定义会话列表为空时的占位元素。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >PlaceholderLoading</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" ><PlaceHolder type={PlaceHolderTypes.LOADING} /></td>

<td rowspan="1" colSpan="1" >自定义会话列表加载中的占位元素。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >PlaceholderLoadError</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" ><PlaceHolder type={PlaceHolderTypes.WRONG} /></td>

<td rowspan="1" colSpan="1" >自定义会话列表加载错误时的占位元素。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >filter</td>

<td rowspan="1" colSpan="1" >(conversationList: ConversationModel[]) => ConversationModel[]</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >用于筛选会话列表的函数。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >sort</td>

<td rowspan="1" colSpan="1" >(conversationList: ConversationModel[]) => ConversationModel[]</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >用于排序会话列表的函数。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onConversationSelect</td>

<td rowspan="1" colSpan="1" >(conversation: ConversationModel) => void;</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >点击会话后的回调函数，参数为所点击的会话对象。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onBeforeCreateConversation</td>

<td rowspan="1" colSpan="1" >(params: CreateParams) => CreateParams;</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >创建会话前执行的自定义操作，参数为创建会话所需的参数。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onConversationCreate</td>

<td rowspan="1" colSpan="1" >(conversation: ConversationModel)  => void;</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >会话创建后的回调函数，参数为创建的会话对象。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >className</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >指定根元素类的 CSS 自定义名称。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >style</td>

<td rowspan="1" colSpan="1" >CSSProperties</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >指定根元素样式的自定义样式。</td>
</tr>
</table>
