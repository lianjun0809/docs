> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

## Overview

Search is a complete search solution that includes a comprehensive component set for search box, search results display, advanced search, and more. It's suitable for user, group, and message search scenarios in instant messaging, online meetings, online education, and more.

> **Note:**
> 

> This feature is a value-added service that requires you to purchase the Cloud Search Plugin. Please click [Purchase](https://console.trtc.io/chat/plugin/TUICloudSearch).
> 


![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/a31b2bd2870911f0bd05525400454e06.png)


## Search Modes
<table>
<tr>
<td rowspan="1" colSpan="1" >**Mini Mode (MINI)**</td>

<td rowspan="1" colSpan="1" >**Standard Mode (STANDARD)**</td>

<td rowspan="1" colSpan="1" >**Embedded Mode (EMBEDDED)**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Suitable for sidebar or small containers<br>Displays limited number of results<br>Supports expanding to view more</td>

<td rowspan="1" colSpan="1" >Suitable for full-screen search interface<br>Complete feature display<br>Supports advanced search</td>

<td rowspan="1" colSpan="1" >Suitable for chat interface<br>Focuses on message search<br>Optimized layout</td>
</tr>
</table>


## Props
<table>
<tr>
<td rowspan="1" colSpan="1" >Property</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Default Value</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >variant</td>

<td rowspan="1" colSpan="1" >VariantType</td>

<td rowspan="1" colSpan="1" >VariantType.MINI</td>

<td rowspan="1" colSpan="1" >Search mode: mini (Mini), standard (Standard), embedded (Embedded)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchBar</td>

<td rowspan="1" colSpan="1" >Component<SearchBarProps></td>

<td rowspan="1" colSpan="1" >DefaultSearchBar</td>

<td rowspan="1" colSpan="1" >Custom search bar component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchResults</td>

<td rowspan="1" colSpan="1" >Component<SearchResultsProps></td>

<td rowspan="1" colSpan="1" >DefaultSearchResults</td>

<td rowspan="1" colSpan="1" >Custom search results component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchAdvanced</td>

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

<td rowspan="1" colSpan="1" >Search debounce time (milliseconds)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >autoFocus</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >false</td>

<td rowspan="1" colSpan="1" >Whether to auto-focus search box</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >className</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Custom style class name</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >style</td>

<td rowspan="1" colSpan="1" >CSSProperties</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Custom styles</td>
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

<td rowspan="1" colSpan="1" >Search result click callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onError</td>

<td rowspan="1" colSpan="1" >(error: Error) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Search error callback</td>
</tr>
</table>


## Basic Usage
``` typescript
<template>
  <div class="app">
    <Search
      :variant="VariantType.STANDARD"
      @result-item-click="handleResultClick"
      @keyword-change="handleKeywordChange"
      @error="handleError"
    />
  </div>
</template>

<script setup lang="ts">
import { Search, VariantType } from '@tencentcloud/chat-uikit-vue3';
import type { SearchResultItemType, SearchType } from '@tencentcloud/chat-uikit-vue3';

const handleResultClick = (data: SearchResultItemType, type: SearchType) => {
  console.log('Search result clicked:', data, type);
};

const handleKeywordChange = (keyword: string) => {
  console.log('Search keyword changed:', keyword);
};

const handleError = (error: Error) => {
  console.error('Search error:', error);
};
</script>
```

## Customization

The `Search` component provides multiple replaceable child components, allowing users to customize `SearchBar`, `SearchResults`, `SearchAdvanced`, `SearchResultItem`, `SearchResultsPresearch`, `SearchResultsLoading`, `SearchResultsEmpty`, etc. Users can also utilize default child components for further customization.



【Custom SearchBar】

**Props**
<table>
<tr>
<td rowspan="1" colSpan="1" >Property</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Default Value</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >value</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Search box value</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onChange</td>

<td rowspan="1" colSpan="1" >(e: Event) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Input change callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onKeyDown</td>

<td rowspan="1" colSpan="1" >(e: KeyboardEvent) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Keyboard event callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onClear</td>

<td rowspan="1" colSpan="1" >() => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Clear callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >placeholder</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Placeholder text</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchIcon</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Custom search icon</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ClearIcon</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Custom clear icon</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >className</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Custom style class name</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >style</td>

<td rowspan="1" colSpan="1" >CSSProperties</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Custom styles</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onFocus</td>

<td rowspan="1" colSpan="1" >(e: FocusEvent) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Focus callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onBlur</td>

<td rowspan="1" colSpan="1" >(e: FocusEvent) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Blur callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >autoFocus</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >false</td>

<td rowspan="1" colSpan="1" >Whether to auto-focus</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >variant</td>

<td rowspan="1" colSpan="1" >VariantType</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Search mode</td>
</tr>
</table>


**Example**
``` typescript
<template>
  <div class="custom-search-bar">
    <div class="search-bar-header">
      <span class="search-icon">🔍</span>
      <span class="search-title">Smart Search</span>
    </div>
    <div class="search-input-wrapper">
      <input
        type="text"
        :value="value"
        :placeholder="placeholder || 'Enter keywords to start searching...'"
        @input="handleChange"
        class="enhanced-search-input"
      />
      <button
        v-if="value"
        @click="handleClear"
        class="enhanced-clear-btn"
      >
        ✕
      </button>
    </div>
  </div>
</template>

<script setup lang="ts">
interface SearchBarProps {
  value?: string;
  onChange?: (event: Event) => void;
  onClear?: () => void;
  placeholder?: string;
  variant?: string;
}

const props = defineProps<SearchBarProps>();

const emit = defineEmits<{
  change: [event: Event];
  clear: [];
}>();

const handleChange = (event: Event) => {
  if (props.onChange) {
    props.onChange(event);
  }
  emit('change', event);
};

const handleClear = () => {
  if (props.onClear) {
    props.onClear();
  }
  emit('clear');
};
</script>

<style scoped>
.custom-search-bar {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.search-bar-header {
  display: flex;
  align-items: center;
  gap: 8px;
}

.search-icon {
  font-size: 16px;
}

.search-title {
  font-weight: 500;
  color: #333;
}

.search-input-wrapper {
  position: relative;
  display: flex;
  align-items: center;
}

.enhanced-search-input {
  width: 100%;
  padding: 8px 12px;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: 14px;
  outline: none;
}

.enhanced-search-input:focus {
  border-color: #007bff;
}

.enhanced-clear-btn {
  position: absolute;
  right: 8px;
  background: none;
  border: none;
  cursor: pointer;
  color: #999;
  font-size: 16px;
}

.enhanced-clear-btn:hover {
  color: #666;
}
</style>

```
``` typescript
<template>
  <Search :SearchBar="CustomSearchBar" />
</template>

<script setup lang="ts">
import { Search } from '@tencentcloud/chat-uikit-vue3';
import CustomSearchBar from './CustomSearchBar.vue';
</script>

```

【Custom SearchResults】

**Props**
<table>
<tr>
<td rowspan="1" colSpan="1" >Property</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Default Value</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >results</td>

<td rowspan="1" colSpan="1" >Map<SearchType, SearchResult></td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Search result data</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >isLoading</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Whether loading</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >error</td>

<td rowspan="1" colSpan="1" >Error \| null</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Error information</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >keyword</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Search keyword</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >typeLabels</td>

<td rowspan="1" colSpan="1" >Record<SearchType, string></td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Search type labels</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onLoadMore</td>

<td rowspan="1" colSpan="1" >(type: SearchType) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Load more callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onResultItemClick</td>

<td rowspan="1" colSpan="1" >(data: SearchResultItemType, type: SearchType) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Result item click callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchResultsLoading</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >Loading</td>

<td rowspan="1" colSpan="1" >Custom loading component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchResultsPresearch</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Pre-search placeholder component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchResultsEmpty</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >EmptyResult</td>

<td rowspan="1" colSpan="1" >Empty results placeholder component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchResultItem</td>

<td rowspan="1" colSpan="1" >Component<ResultItemProps></td>

<td rowspan="1" colSpan="1" >DefaultSearchResultsItem</td>

<td rowspan="1" colSpan="1" >Custom result item component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >variant</td>

<td rowspan="1" colSpan="1" >VariantType</td>

<td rowspan="1" colSpan="1" >VariantType.STANDARD</td>

<td rowspan="1" colSpan="1" >Display mode</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >searchType</td>

<td rowspan="1" colSpan="1" >SearchType \| 'all'</td>

<td rowspan="1" colSpan="1" >'all'</td>

<td rowspan="1" colSpan="1" >Current search type</td>
</tr>
</table>


**Example**
``` typescript
<template>
  <div class="custom-search-results">
    <div class="search-results-header">
      <span class="results-icon">📋</span>
      <span class="results-title">Search Results</span>
    </div>
    <div class="search-results-content">
      <div v-if="!results || results.size === 0" class="no-results">
        No search results
      </div>
      <div v-else class="results-list">
        <div
          v-for="(item, key) in results.keys()"
          :key="key"
          class="result-item"
        >
          <div class="result-group">
            <div class="result-title">
              {{ item }}
            </div>
            <ul v-if="item === SearchType.MESSAGE" class="result-description">
              <li
                v-for="(data, index) in results.get(item)?.resultList"
                :key="index"
                @click="handleResultClick(data)"
              >
                {{ (data as SearchCloudMessagesResultItem).conversation?.getShowName() }}
              </li>
            </ul>
            <ul v-if="item === SearchType.USER" class="result-description">
              <li
                v-for="(data, index) in results.get(item)?.resultList"
                :key="index"
                @click="handleResultClick(data)"
              >
                {{ (data as SearchCloudUsersResultItem).profile.nick
                 || (data as SearchCloudUsersResultItem).profile.userID }}
              </li>
            </ul>
            <ul v-if="item === SearchType.GROUP" class="result-description">
              <li
                v-for="(data, index) in results.get(item)?.resultList"
                :key="index"
                @click="handleResultClick(data)"
              >
                {{ (data as SearchCloudGroupsResultItem).groupInfo.name 
                || (data as SearchCloudGroupsResultItem).groupInfo.groupID }}
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { SearchType } from '@tencentcloud/chat-uikit-vue3';
import type {
  SearchCloudGroupsResultItem,
  SearchCloudMessagesResultItem,
  SearchCloudUsersResultItem,
  SearchResult,
  SearchResultItemType,
} from '@tencentcloud/chat-uikit-vue3';

interface SearchResultsProps {
  results?: Map<SearchType, SearchResult<any>>;
  loading?: boolean;
  keyword?: string;
  searchType?: SearchType;
}

const props = defineProps<SearchResultsProps>();

const emit = defineEmits<{
  'result-item-click': [data: SearchResultItemType, type: any];
}>();

const handleResultClick = (item: SearchResultItemType) => {
  emit('result-item-click', item, props.searchType || 'ALL');
};
</script>

<style scoped>
.custom-search-results {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.search-results-header {
  display: flex;
  align-items: center;
  gap: 8px;
}

.results-icon {
  font-size: 16px;
}

.results-title {
  font-weight: 500;
  color: #333;
}

.search-results-content {
  max-height: 400px;
  overflow-y: auto;
}

.no-results {
  padding: 20px;
  text-align: center;
  color: #999;
  font-size: 14px;
}

.results-list {
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.result-item {
  padding: 12px;
  border: 1px solid #eee;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.2s;
}

.result-item:hover {
  background-color: #f5f5f5;
}

.result-content {
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.result-title {
  font-weight: 500;
  color: #333;
  font-size: 14px;
}

.result-description {
  color: #666;
  font-size: 12px;
  line-height: 1.4;
}
</style>

```
``` typescript
<template>
  <Search :SearchResults="CustomSearchResults" />
</template>

<script setup lang="ts">
import { Search } from '@tencentcloud/chat-uikit-vue3';
import CustomSearchResults from './CustomSearchResults.vue';
</script>
```

【Custom SearchAdvanced】

**Props**
<table>
<tr>
<td rowspan="1" colSpan="1" >Property</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Default Value</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >variant</td>

<td rowspan="1" colSpan="1" >VariantType</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Display mode</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >searchType</td>

<td rowspan="1" colSpan="1" >SearchTabType</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Current search type</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >advancedParams</td>

<td rowspan="1" colSpan="1" >Map<SearchType, SearchParamsMap[SearchType]></td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Advanced search parameters</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onAdvancedParamsChange</td>

<td rowspan="1" colSpan="1" >(type: SearchType, params: SearchParamsMap[SearchType]) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Parameter change callback</td>
</tr>
</table>


**Example**
``` typescript
<template>
  <div class="custom-search-advanced">
    <div class="search-advanced-header">
      <span class="advanced-icon">⚙️</span>
      <span class="advanced-title">Advanced Search</span>
    </div>
    <div class="search-advanced-content">
      <div class="search-type-section">
        <div class="section-title">
          Search Type
        </div>
        <div class="search-type-options">
          <label
            v-for="type in searchTypes"
            :key="type.value"
            class="type-option"
          >
            <input
              type="radio"
              :value="type.value"
              :checked="searchType === type.value"
              @change="handleSearchTypeChange(type.value as SearchType)"
            >
            <span class="type-label">{{ type.label }}</span>
          </label>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { SearchType, useSearchState } from '@tencentcloud/chat-uikit-vue3';
import type { VariantType } from '@tencentcloud/chat-uikit-vue3';

interface CustomSearchAdvancedProps {
  variant?: VariantType;
  searchType?: SearchType;
}

const props = defineProps<CustomSearchAdvancedProps>();
const { setSelectedType } = useSearchState();

const emit = defineEmits<{
  'search-type-change': [type: SearchType | 'all'];
}>();

const searchTypes = [
  { value: 'all', label: 'All' },
  { value: SearchType.MESSAGE, label: 'Messages' },
  { value: SearchType.USER, label: 'Users' },
  { value: SearchType.GROUP, label: 'Groups' },
];

const searchType = ref<SearchType | 'all'>(props.searchType || 'all');

const handleSearchTypeChange = (type: SearchType) => {
  searchType.value = type;
  setSelectedType(type);
  emit('search-type-change', type);
};
</script>

<style scoped>
.custom-search-advanced {
  display: flex;
  flex-direction: column;
  gap: 16px;
  padding: 16px;
  border: 1px solid #eee;
  border-radius: 8px;
  background-color: #fff;
}

.search-advanced-header {
  display: flex;
  align-items: center;
  gap: 8px;
  padding-bottom: 12px;
  border-bottom: 1px solid #f0f0f0;
}

.advanced-icon {
  font-size: 16px;
}

.advanced-title {
  font-weight: 500;
  color: #333;
  font-size: 16px;
}

.search-advanced-content {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.section-title {
  font-weight: 500;
  color: #333;
  font-size: 14px;
  margin-bottom: 8px;
}

.search-type-options {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
}

.type-option {
  display: flex;
  align-items: center;
  gap: 6px;
  cursor: pointer;
}

.type-option input[type="radio"] {
  margin: 0;
}

.type-label {
  font-size: 14px;
  color: #666;
}
</style>

```
``` typescript
<template>
  <Search :SearchAdvanced="CustomSearchAdvanced" />
</template>

<script setup lang="ts">
import { Search } from '@tencentcloud/chat-uikit-vue3';
import CustomSearchAdvanced from './CustomSearchAdvanced.vue';
</script>
```

【Custom SearchResultItem】

**Props**
<table>
<tr>
<td rowspan="1" colSpan="1" >Property</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Default Value</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >data</td>

<td rowspan="1" colSpan="1" >SearchResultItem</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Search result data</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >type</td>

<td rowspan="1" colSpan="1" >SearchType</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Search result type</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >keyword</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Search keyword</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onClick</td>

<td rowspan="1" colSpan="1" >(data: SearchResultItem, type: SearchType) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Click callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >className</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Custom style class name</td>
</tr>
</table>


**Example**
``` java
<template>
  <div class="custom-search-item">
    <div
      v-if="type === SearchType.USER"
      class="user-item"
      @click="handleClick"
    >
      <div class="user-avatar">
        <img :src="data.profile.avatar" :alt="data.profile.nick" />
      </div>
      <div class="user-info">
        <div class="user-name">{{ data.profile.nick }}</div>
        <div class="user-id">{{ data.profile.userID }}</div>
      </div>
    </div>

    <div
      v-else-if="type === SearchType.GROUP"
      class="group-item"
      @click="handleClick"
    >
      <div class="group-avatar">👥</div>
      <div class="group-info">
        <div class="group-name">{{ data.groupInfo.name }}</div>
        <div class="group-id">{{ data.groupInfo.groupID }}</div>
      </div>
    </div>

    <div
      v-else-if="type === SearchType.MESSAGE"
      class="message-item"
      @click="handleClick"
    >
      <div class="message-content">{{ data.conversation.getShowName() }}</div>
      <div class="message-num">{{ data.messageCount }}</div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { SearchType } from '@tencentcloud/chat-uikit-vue3';
import type { SearchResultItemType } from '@tencentcloud/chat-uikit-vue3';

interface CustomSearchItemProps {
  data: SearchResultItemType;
  type?: SearchType;
  onClick?: (data: SearchResultItemType, type: SearchType) => void;
}

const props = defineProps<CustomSearchItemProps>();

console.warn('CustomSearchItem', props);

const handleClick = () => {
  if (props.onClick && props.type) {
    props.onClick(props.data, props.type);
  }
};

const formatTime = (timestamp: number) => {
  return new Date(timestamp).toLocaleString();
};
</script>

<style scoped>
.custom-search-item {
  cursor: pointer;
  padding: 12px;
  border-bottom: 1px solid #f0f0f0;
  transition: background-color 0.2s;
}

.custom-search-item:hover {
  background-color: #f5f5f5;
}

.user-item,
.group-item,
.message-item {
  display: flex;
  align-items: center;
  gap: 12px;
}

.user-avatar img {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  object-fit: cover;
}

.group-avatar {
  width: 40px;
  height: 40px;
  border-radius: 8px;
  background-color: #e9ecef;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 18px;
}

.user-info,
.group-info {
  flex: 1;
}

.user-name,
.group-name {
  font-weight: 500;
  color: #333;
  font-size: 14px;
  margin-bottom: 4px;
}

.user-id,
.group-id {
  color: #666;
  font-size: 12px;
}

.message-content {
  flex: 1;
  color: #333;
  font-size: 14px;
  line-height: 1.4;
}

.message-num {
  color: #666;
  font-size: 12px;
  white-space: nowrap;
}
</style>
```
``` typescript
<template>
  <Search :SearchResultItem="CustomSearchItem" />
</template>

<script setup lang="ts">
import { Search } from '@tencentcloud/chat-uikit-vue3';
import CustomSearchItem from './CustomSearchItem.vue';
</script>
```

【Custom Placeholders】

**Props**
<table>
<tr>
<td rowspan="1" colSpan="1" >Property</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Default Value</td>

<td rowspan="1" colSpan="1" >Description</td>
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
</table>


**Example**
``` typescript
<template>
  <Search
    :search-results-presearch="PresearchComponent"
    :search-results-loading="LoadingComponent"
    :search-results-empty="EmptyComponent"
  />
</template>

<script setup lang="ts">
import { defineComponent, h } from 'vue';
import { Search } from '@tencentcloud/chat-uikit-vue3';

const PresearchComponent = defineComponent({
  name: 'PresearchComponent',
  setup() {
    return () => h('div', { class: 'presearch-placeholder' }, [
      h('div', { class: 'placeholder-icon' }, '🔍'),
      h('div', { class: 'placeholder-text' }, 'Enter keywords to start searching')
    ]);
  }
});

const LoadingComponent = defineComponent({
  name: 'LoadingComponent',
  setup() {
    return () => h('div', { class: 'loading-placeholder' }, [
      h('div', { class: 'loading-spinner' }),
      h('div', { class: 'loading-text' }, 'Searching...')
    ]);
  }
});

const EmptyComponent = defineComponent({
  name: 'EmptyComponent',
  setup() {
    return () => h('div', { class: 'empty-placeholder' }, [
      h('div', { class: 'empty-icon' }, '😔'),
      h('div', { class: 'empty-text' }, 'No results found'),
      h('div', { class: 'empty-hint' }, 'Try searching with different keywords')
    ]);
  }
});
</script>

<style scoped>
.presearch-placeholder,
.loading-placeholder,
.empty-placeholder {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 60px 20px;
  color: #999;
}

.placeholder-icon,
.empty-icon {
  font-size: 48px;
  margin-bottom: 16px;
}

.loading-spinner {
  width: 32px;
  height: 32px;
  border: 3px solid #f3f3f3;
  border-top: 3px solid #1890ff;
  border-radius: 50%;
  animation: spin 1s linear infinite;
  margin-bottom: 16px;
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

.placeholder-text,
.loading-text,
.empty-text {
  font-size: 16px;
  margin-bottom: 8px;
}

.empty-hint {
  font-size: 14px;
  color: #bbb;
}
</style>
```
