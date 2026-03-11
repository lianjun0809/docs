> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

## 概述

Search 是一个功能完整的搜索解决方案，包含了搜索框、搜索结果展示、高级搜索等功能的完整组件集合。适用于即时通讯、在线会议、在线教育等场景的用户、群组、消息搜索。

> **说明：**
> 

> 此功能属于增值服务，需要您购买云端搜索插件，请点击 [购买](https://cloud.tencent.com/document/product/269/120945)。
> 


![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/a31b2bd2870911f0bd05525400454e06.png)


## 搜索模式
<table>
<tr>
<td rowspan="1" colSpan="1" >**迷你模式 (MINI)**</td>

<td rowspan="1" colSpan="1" >**标准模式 (STANDARD)**</td>

<td rowspan="1" colSpan="1" >**嵌入式模式 (EMBEDDED)**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >适用于侧边栏或小容器<br>显示有限结果数量<br>支持展开查看更多</td>

<td rowspan="1" colSpan="1" >适用于全屏搜索界面<br>完整功能展示<br>支持高级搜索</td>

<td rowspan="1" colSpan="1" >适用于聊天界面<br>专注消息搜索<br>优化的布局</td>
</tr>
</table>


## Props
<table>
<tr>
<td rowspan="1" colSpan="1" >属性名</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >默认值</td>

<td rowspan="1" colSpan="1" >说明</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >variant</td>

<td rowspan="1" colSpan="1" >VariantType</td>

<td rowspan="1" colSpan="1" >VariantType.MINI</td>

<td rowspan="1" colSpan="1" >搜索模式：mini(迷你)、standard(标准)、embedded(嵌入式)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchBar</td>

<td rowspan="1" colSpan="1" >Component<SearchBarProps></td>

<td rowspan="1" colSpan="1" >DefaultSearchBar</td>

<td rowspan="1" colSpan="1" >自定义搜索框组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchResults</td>

<td rowspan="1" colSpan="1" >Component<SearchResultsProps></td>

<td rowspan="1" colSpan="1" >DefaultSearchResults</td>

<td rowspan="1" colSpan="1" >自定义搜索结果组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchAdvanced</td>

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


## 基础用法
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
  console.log('搜索结果点击:', data, type);
};

const handleKeywordChange = (keyword: string) => {
  console.log('搜索关键词变化:', keyword);
};

const handleError = (error: Error) => {
  console.error('搜索错误:', error);
};
</script>
```

## 自定义

`Search` 组件提供了多个可替换的子组件，允许用户自定义 `SearchBar`, `SearchResults`, `SearchAdvanced`, `SearchResultItem`, `SearchResultsPresearch`, `SearchResultsLoading`, `SearchResultsEmpty` 等。同时，用户还可以利用默认子组件进行二次开发定制。



【自定义 SearchBar】

**Props**
<table>
<tr>
<td rowspan="1" colSpan="1" >属性名</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >默认值</td>

<td rowspan="1" colSpan="1" >说明</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >value</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >搜索框值</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onChange</td>

<td rowspan="1" colSpan="1" >(e: Event) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >输入变化回调</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onKeyDown</td>

<td rowspan="1" colSpan="1" >(e: KeyboardEvent) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >键盘事件回调</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onClear</td>

<td rowspan="1" colSpan="1" >() => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >清除回调</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >placeholder</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >占位符文本</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchIcon</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >自定义搜索图标</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ClearIcon</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >自定义清除图标</td>
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
<td rowspan="1" colSpan="1" >onFocus</td>

<td rowspan="1" colSpan="1" >(e: FocusEvent) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >获得焦点回调</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onBlur</td>

<td rowspan="1" colSpan="1" >(e: FocusEvent) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >失去焦点回调</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >autoFocus</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >false</td>

<td rowspan="1" colSpan="1" >是否自动聚焦</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >variant</td>

<td rowspan="1" colSpan="1" >VariantType</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >搜索模式</td>
</tr>
</table>


**示例**
``` typescript
<template>
  <div class="custom-search-bar">
    <div class="search-bar-header">
      <span class="search-icon">🔍</span>
      <span class="search-title">智能搜索</span>
    </div>
    <div class="search-input-wrapper">
      <input
        type="text"
        :value="value"
        :placeholder="placeholder || '输入关键词开始搜索...'"
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

【自定义 SearchResults】

**Props**
<table>
<tr>
<td rowspan="1" colSpan="1" >属性名</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >默认值</td>

<td rowspan="1" colSpan="1" >说明</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >results</td>

<td rowspan="1" colSpan="1" >Map<SearchType, SearchResult></td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >搜索结果数据</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >isLoading</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >是否正在加载</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >error</td>

<td rowspan="1" colSpan="1" >Error \| null</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >错误信息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >keyword</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >搜索关键词</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >typeLabels</td>

<td rowspan="1" colSpan="1" >Record<SearchType, string></td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >搜索类型标签</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onLoadMore</td>

<td rowspan="1" colSpan="1" >(type: SearchType) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >加载更多回调</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onResultItemClick</td>

<td rowspan="1" colSpan="1" >(data: SearchResultItemType, type: SearchType) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >结果项点击回调</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchResultsLoading</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >Loading</td>

<td rowspan="1" colSpan="1" >自定义加载组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchResultsPresearch</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >搜索前占位符组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchResultsEmpty</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >EmptyResult</td>

<td rowspan="1" colSpan="1" >空结果占位符组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchResultItem</td>

<td rowspan="1" colSpan="1" >Component<ResultItemProps></td>

<td rowspan="1" colSpan="1" >DefaultSearchResultsItem</td>

<td rowspan="1" colSpan="1" >自定义结果项组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >variant</td>

<td rowspan="1" colSpan="1" >VariantType</td>

<td rowspan="1" colSpan="1" >VariantType.STANDARD</td>

<td rowspan="1" colSpan="1" >显示模式</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >searchType</td>

<td rowspan="1" colSpan="1" >SearchType \| 'all'</td>

<td rowspan="1" colSpan="1" >'all'</td>

<td rowspan="1" colSpan="1" >当前搜索类型</td>
</tr>
</table>


**示例**
``` typescript
<template>
  <div class="custom-search-results">
    <div class="search-results-header">
      <span class="results-icon">📋</span>
      <span class="results-title">搜索结果</span>
    </div>
    <div class="search-results-content">
      <div v-if="!results || results.size === 0" class="no-results">
        暂无搜索结果
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

【自定义 SearchAdvanced】

**Props**
<table>
<tr>
<td rowspan="1" colSpan="1" >属性名</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >默认值</td>

<td rowspan="1" colSpan="1" >说明</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >variant</td>

<td rowspan="1" colSpan="1" >VariantType</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >显示模式</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >searchType</td>

<td rowspan="1" colSpan="1" >SearchTabType</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >当前搜索类型</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >advancedParams</td>

<td rowspan="1" colSpan="1" >Map<SearchType, SearchParamsMap[SearchType]></td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >高级搜索参数</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onAdvancedParamsChange</td>

<td rowspan="1" colSpan="1" >(type: SearchType, params: SearchParamsMap[SearchType]) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >参数变化回调</td>
</tr>
</table>


**示例**
``` typescript
<template>
  <div class="custom-search-advanced">
    <div class="search-advanced-header">
      <span class="advanced-icon">⚙️</span>
      <span class="advanced-title">高级搜索</span>
    </div>
    <div class="search-advanced-content">
      <div class="search-type-section">
        <div class="section-title">
          搜索类型
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
  { value: 'all', label: '全部' },
  { value: SearchType.MESSAGE, label: '消息' },
  { value: SearchType.USER, label: '用户' },
  { value: SearchType.GROUP, label: '群组' },
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

【自定义 SearchResultItem】

**Props**
<table>
<tr>
<td rowspan="1" colSpan="1" >属性名</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >默认值</td>

<td rowspan="1" colSpan="1" >说明</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >data</td>

<td rowspan="1" colSpan="1" >SearchResultItem</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >搜索结果数据</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >type</td>

<td rowspan="1" colSpan="1" >SearchType</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >搜索结果类型</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >keyword</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >搜索关键词</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onClick</td>

<td rowspan="1" colSpan="1" >(data: SearchResultItem, type: SearchType) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >点击回调</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >className</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >自定义样式类名</td>
</tr>
</table>


**示例**
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

【自定义占位符】

**Props**
<table>
<tr>
<td rowspan="1" colSpan="1" >属性名</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >默认值</td>

<td rowspan="1" colSpan="1" >说明</td>
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
</table>


**示例**
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
      h('div', { class: 'placeholder-text' }, '输入关键词开始搜索')
    ]);
  }
});

const LoadingComponent = defineComponent({
  name: 'LoadingComponent',
  setup() {
    return () => h('div', { class: 'loading-placeholder' }, [
      h('div', { class: 'loading-spinner' }),
      h('div', { class: 'loading-text' }, '搜索中...')
    ]);
  }
});

const EmptyComponent = defineComponent({
  name: 'EmptyComponent',
  setup() {
    return () => h('div', { class: 'empty-placeholder' }, [
      h('div', { class: 'empty-icon' }, '😔'),
      h('div', { class: 'empty-text' }, '未找到相关结果'),
      h('div', { class: 'empty-hint' }, '尝试使用其他关键词搜索')
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
