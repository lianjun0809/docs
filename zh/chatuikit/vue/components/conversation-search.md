> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

ConversationSearch 是使用的 **Search** 组件，支持用户、群组、消息的搜索功能。它集成了搜索框、高级搜索、搜索结果展示等功能。

## 基础使用
``` typescript
<template>
  <ConversationSearch {...props} @ResultItemClick={onSelectResult} />
</template>
<script setup lang="ts">
import { ConversationSearch, SearchType } from '@tencentcloud/chat-uikit-vue3';
import type { SearchResultItem } from '@tencentcloud/chat-uikit-vue3';
const props = defineProps<ConversationSearchProps>();

const onSelectResult = (data: SearchResultItem, type: SearchType) => {
  console.warn(`Select Search Result: ${JSON.stringify(data)}, type: ${type}`);
};
</script>
```
``` typescript
<template>
  <UIKitProvider>
    <ConversationList ConversationSearch={CustomConversationSearch} />
  </UIKitProvider>
</template>
<script setup lang="ts">
import { UIKitProvider, ConversationList } from '@tencentcloud/chat-uikit-vue3';
import CustomConversationSearch from "./CustomConversationSearch.vue";
</script>
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
<td rowspan="1" colSpan="1" >visible</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >true</td>

<td rowspan="1" colSpan="1" >是否可见</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[Search](https://write.woa.com/document/187595449195040768)</td>

<td rowspan="1" colSpan="1" >ComponentType<SearchProps></td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >自定义搜索组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >variant</td>

<td rowspan="1" colSpan="1" >VariantType</td>

<td rowspan="1" colSpan="1" >VariantType.MINI</td>

<td rowspan="1" colSpan="1" >搜索模式：<br>- mini：迷你<br>- standard：标准<br>- embedded：嵌入式</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[SearchBar](https://write.woa.com/document/187595449195040768)</td>

<td rowspan="1" colSpan="1" >Component<SearchBarProps></td>

<td rowspan="1" colSpan="1" >DefaultSearchBar</td>

<td rowspan="1" colSpan="1" >自定义搜索框组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[SearchResults](https://write.woa.com/document/187595449195040768)</td>

<td rowspan="1" colSpan="1" >Component<SearchResultsProps></td>

<td rowspan="1" colSpan="1" >DefaultSearchResults</td>

<td rowspan="1" colSpan="1" >自定义搜索结果组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[SearchAdvanced](https://write.woa.com/document/187595449195040768)</td>

<td rowspan="1" colSpan="1" >Component<SearchAdvancedProps></td>

<td rowspan="1" colSpan="1" >DefaultSearchAdvanced</td>

<td rowspan="1" colSpan="1" >自定义高级搜索组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchResultsPresearch</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >搜索前占位符组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchResultsLoading</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >加载中占位符组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchResultsEmpty</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >空结果占位符组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchResultItem</td>

<td rowspan="1" colSpan="1" >Component<ResultItemProps></td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >自定义搜索结果项组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >debounceTime</td>

<td rowspan="1" colSpan="1" >number</td>

<td rowspan="1" colSpan="1" >300</td>

<td rowspan="1" colSpan="1" >搜索防抖时间(毫秒)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >autoFocus</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >false</td>

<td rowspan="1" colSpan="1" >是否自动聚焦搜索框</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >className</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >自定义样式类名</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >style</td>

<td rowspan="1" colSpan="1" >CSSProperties</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >自定义样式</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onKeywordChange</td>

<td rowspan="1" colSpan="1" >(keyword: string) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >搜索关键词变化回调</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onSearchComplete</td>

<td rowspan="1" colSpan="1" >(results: Map<SearchType, SearchResult>) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >搜索完成回调</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onResultItemClick</td>

<td rowspan="1" colSpan="1" >(data: SearchResultItem, type: SearchType) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >搜索结果点击回调</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onError</td>

<td rowspan="1" colSpan="1" >(error: Error) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >搜索错误回调</td>
</tr>
</table>
