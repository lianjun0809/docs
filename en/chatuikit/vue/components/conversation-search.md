> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/en/llms.txt
> Use this file to discover all available pages before exploring further.

ConversationSearch uses the **Search** component, supporting search for users, groups, and messages. It integrates search box, advanced search, and search results display features.

## Basic Usage
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
<td rowspan="1" colSpan="1" >**Parameter**</td>

<td rowspan="1" colSpan="1" >**Type**</td>

<td rowspan="1" colSpan="1" >**Default**</td>

<td rowspan="1" colSpan="1" >**Description**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >visible</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >true</td>

<td rowspan="1" colSpan="1" >Whether visible</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[Search](https://write.woa.com/document/187595449195040768)</td>

<td rowspan="1" colSpan="1" >ComponentType<SearchProps></td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Custom search component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >variant</td>

<td rowspan="1" colSpan="1" >VariantType</td>

<td rowspan="1" colSpan="1" >VariantType.MINI</td>

<td rowspan="1" colSpan="1" >Search mode:<br>- mini: Mini<br>- standard: Standard<br>- embedded: Embedded</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[SearchBar](https://write.woa.com/document/187595449195040768)</td>

<td rowspan="1" colSpan="1" >Component<SearchBarProps></td>

<td rowspan="1" colSpan="1" >DefaultSearchBar</td>

<td rowspan="1" colSpan="1" >Custom search bar component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[SearchResults](https://write.woa.com/document/187595449195040768)</td>

<td rowspan="1" colSpan="1" >Component<SearchResultsProps></td>

<td rowspan="1" colSpan="1" >DefaultSearchResults</td>

<td rowspan="1" colSpan="1" >Custom search results component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[SearchAdvanced](https://write.woa.com/document/187595449195040768)</td>

<td rowspan="1" colSpan="1" >Component<SearchAdvancedProps></td>

<td rowspan="1" colSpan="1" >DefaultSearchAdvanced</td>

<td rowspan="1" colSpan="1" >Custom advanced search component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchResultsPresearch</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Pre-search placeholder component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchResultsLoading</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Loading placeholder component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchResultsEmpty</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Empty results placeholder component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchResultItem</td>

<td rowspan="1" colSpan="1" >Component<ResultItemProps></td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Custom search result item component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >debounceTime</td>

<td rowspan="1" colSpan="1" >number</td>

<td rowspan="1" colSpan="1" >300</td>

<td rowspan="1" colSpan="1" >Search debounce time (ms)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >autoFocus</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >false</td>

<td rowspan="1" colSpan="1" >Whether to auto-focus the search box</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >className</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Custom class name</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >style</td>

<td rowspan="1" colSpan="1" >CSSProperties</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Custom style</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onKeywordChange</td>

<td rowspan="1" colSpan="1" >(keyword: string) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Search keyword change callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onSearchComplete</td>

<td rowspan="1" colSpan="1" >(results: Map<SearchType, SearchResult>) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Search complete callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onResultItemClick</td>

<td rowspan="1" colSpan="1" >(data: SearchResultItem, type: SearchType) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Search result item click callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onError</td>

<td rowspan="1" colSpan="1" >(error: Error) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Search error callback</td>
</tr>
</table>
