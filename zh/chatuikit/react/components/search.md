> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

## 组件概述

Search 是一个功能完整的搜索解决方案，包含了搜索框、搜索结果展示、高级搜索等功能的完整组件集合。适用于即时通讯、在线会议、在线教育等场景的用户、群组、消息搜索。

> **说明：**
> 

> 此功能属于增值服务，需要您购买云端搜索插件，请点击 [购买](https://console.cloud.tencent.com/im/plugin/TUICloudSearch)。
> 


![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/69961bab5c7311f094cd52540099c741.png)


## 组件架构
``` bash
Search (主组件)
├── SearchBar              # 搜索框组件
├── SearchResults          # 搜索结果组件
├── SearchAdvanced         # 高级搜索组件
└── SearchResultsItem      # 搜索结果项组件
    ├── User               # 用户结果项
    ├── Group              # 群组结果项
    ├── Message            # 消息结果项
    └── Conversation       # 会话结果项
```

## 搜索模式
<table>
<tr>
<td rowspan="1" colSpan="1" >**迷你模式**</td>

<td rowspan="1" colSpan="1" >**标准模式**</td>

<td rowspan="1" colSpan="1" >**嵌入式模式**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >- 适用于侧边栏或小容器<br>- 显示有限结果数量<br>- 支持展开查看更多</td>

<td rowspan="1" colSpan="1" >- 适用于全屏搜索界面<br>- 完整功能展示<br>- 支持高级搜索</td>

<td rowspan="1" colSpan="1" >- 适用于聊天界面<br>- 专注消息搜索<br>- 优化的布局</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/765af543523311f0a63e525400e889b2.png)</td>

<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/8a336e5e523311f09a935254007c27c5.png)</td>

<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/046f3c98523611f0adb15254005ef0f7.png)</td>
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

<td rowspan="1" colSpan="1" >`VariantType`</td>

<td rowspan="1" colSpan="1" >`VariantType.MINI`</td>

<td rowspan="1" colSpan="1" >搜索模式：`mini`(迷你)、`standard`(标准)、`embedded`(嵌入式)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchBar</td>

<td rowspan="1" colSpan="1" >`React.ComponentType<SearchBarProps>`</td>

<td rowspan="1" colSpan="1" >`DefaultSearchBar`</td>

<td rowspan="1" colSpan="1" >自定义搜索框组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchResults</td>

<td rowspan="1" colSpan="1" >`React.ComponentType<SearchResultsProps>`</td>

<td rowspan="1" colSpan="1" >`DefaultSearchResults`</td>

<td rowspan="1" colSpan="1" >自定义搜索结果组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchAdvanced</td>

<td rowspan="1" colSpan="1" >`React.ComponentType<SearchAdvancedProps>`</td>

<td rowspan="1" colSpan="1" >`DefaultSearchAdvanced`</td>

<td rowspan="1" colSpan="1" >自定义高级搜索组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchResultsPresearch</td>

<td rowspan="1" colSpan="1" >`React.ComponentType`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >搜索前占位符组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchResultsLoading</td>

<td rowspan="1" colSpan="1" >`React.ComponentType`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >加载中占位符组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchResultsEmpty</td>

<td rowspan="1" colSpan="1" >`React.ComponentType`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >空结果占位符组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchResultItem</td>

<td rowspan="1" colSpan="1" >`React.ComponentType<ResultItemProps>`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >自定义搜索结果项组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >debounceTime</td>

<td rowspan="1" colSpan="1" >`number`</td>

<td rowspan="1" colSpan="1" >`300`</td>

<td rowspan="1" colSpan="1" >搜索防抖时间(毫秒)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >autoFocus</td>

<td rowspan="1" colSpan="1" >`boolean`</td>

<td rowspan="1" colSpan="1" >`false`</td>

<td rowspan="1" colSpan="1" >是否自动聚焦搜索框</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >className</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >自定义样式类名</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >style</td>

<td rowspan="1" colSpan="1" >`React.CSSProperties`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >自定义样式</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onKeywordChange</td>

<td rowspan="1" colSpan="1" >`(keyword: string) => void`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >搜索关键词变化回调</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onSearchComplete</td>

<td rowspan="1" colSpan="1" >`(results: Map<SearchType, SearchResult>) => void`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >搜索完成回调</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onResultItemClick</td>

<td rowspan="1" colSpan="1" >`(data: SearchResultItem, type: SearchType) => void`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >搜索结果点击回调</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onError</td>

<td rowspan="1" colSpan="1" >`(error: Error) => void`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >搜索错误回调</td>
</tr>
</table>


## 基础使用
``` typescript
import { Search, VariantType } from '@tencentcloud/chat-uikit-react';

function App() {
  return (
    <Search
      variant={VariantType.STANDARD}
      onResultItemClick={(data, type) => {
        console.log('搜索结果点击:', data, type);
      }}
    />
  );
}
```

## 自定义能力

`Search` 为用户自定义提供了丰富且多维度的 Props 接口，允许用户自定义功能、UI、模块等。

`Search` 组件提供了多个可替换的子组件，允许用户自定义 `SearchBar`, `SearchResults`, `SearchAdvanced`, `SearchResultItem`, `SearchResultsPresearch`, `SearchResultsLoading`, `SearchResultsEmpty`, 等。同时，用户还可以利用默认子组件进行二次开发定制。



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
<td rowspan="1" colSpan="1" >data</td>

<td rowspan="1" colSpan="1" >`SearchResultItem`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >搜索结果数据</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >type</td>

<td rowspan="1" colSpan="1" >`SearchType`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >搜索结果类型</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >keyword</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >搜索关键词</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onClick</td>

<td rowspan="1" colSpan="1" >`(data: SearchResultItem, type: SearchType) => void`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >点击回调</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >className</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >自定义样式类名</td>
</tr>
</table>


**示例**
``` typescript
const CustomSearchBar = ({ value, onChange, onClear, placeholder }) => (
  <div className="custom-search-bar">
    <input
      type="text"
      value={value}
      onChange={onChange}
      placeholder={placeholder}
    />
    {value && <button onClick={onClear}>清除</button>}
  </div>
);

<Search SearchBar={CustomSearchBar} />
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

<td rowspan="1" colSpan="1" >`Map<SearchType, SearchResult>`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >搜索结果数据</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >isLoading</td>

<td rowspan="1" colSpan="1" >`boolean`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >是否正在加载</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >error</td>

<td rowspan="1" colSpan="1" >`Error \| null`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >错误信息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >keyword</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >搜索关键词</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >typeLabels</td>

<td rowspan="1" colSpan="1" >`Record<SearchType, string>`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >搜索类型标签</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onLoadMore</td>

<td rowspan="1" colSpan="1" >`(type: SearchType) => void`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >加载更多回调</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onResultItemClick</td>

<td rowspan="1" colSpan="1" >`(data: SearchResultItem, type: SearchType) => void`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >结果项点击回调</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchResultsLoading</td>

<td rowspan="1" colSpan="1" >`React.ComponentType`</td>

<td rowspan="1" colSpan="1" >`Loading`</td>

<td rowspan="1" colSpan="1" >自定义加载组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchResultsPresearch</td>

<td rowspan="1" colSpan="1" >`React.ComponentType`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >搜索前占位符组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchResultsEmpty</td>

<td rowspan="1" colSpan="1" >`React.ComponentType`</td>

<td rowspan="1" colSpan="1" >`EmptyResult`</td>

<td rowspan="1" colSpan="1" >空结果占位符组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchResultItem</td>

<td rowspan="1" colSpan="1" >`React.ComponentType<ResultItemProps>`</td>

<td rowspan="1" colSpan="1" >`DefaultSearchResultsItem`</td>

<td rowspan="1" colSpan="1" >自定义结果项组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >variant</td>

<td rowspan="1" colSpan="1" >`VariantType`</td>

<td rowspan="1" colSpan="1" >`VariantType.STANDARD`</td>

<td rowspan="1" colSpan="1" >显示模式</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >searchType</td>

<td rowspan="1" colSpan="1" >`SearchType \| 'all'`</td>

<td rowspan="1" colSpan="1" >`'all'`</td>

<td rowspan="1" colSpan="1" >当前搜索类型</td>
</tr>
</table>


**示例**
``` typescript
const CustomSearchResults = ({ results, keyword, onResultItemClick }) => (
  <div className="custom-results">
    {Array.from(results.entries()).map(([type, result]) => (
      <div key={type}>
        <h3>{type}</h3>
        {result.resultList.map((item, index) => (
          <div key={index} onClick={() => onResultItemClick(item, type)}>
            {/* 自定义结果项 */}
          </div>
        ))}
      </div>
    ))}
  </div>
);

<Search SearchResults={CustomSearchResults} />
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

<td rowspan="1" colSpan="1" >`VariantType`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >显示模式</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >searchType</td>

<td rowspan="1" colSpan="1" >`SearchTabType`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >当前搜索类型</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >advancedParams</td>

<td rowspan="1" colSpan="1" >`Map<SearchType, SearchParamsMap[SearchType]>`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >高级搜索参数</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onAdvancedParamsChange</td>

<td rowspan="1" colSpan="1" >`(type: SearchType, params: SearchParamsMap[SearchType]) => void`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >参数变化回调</td>
</tr>
</table>


**示例**
``` typescript
const CustomSearchAdvanced = ({ variant, searchType, advancedParams, onAdvancedParamsChange }) => (
  <div className="custom-advanced">
  {/* 自定义高级搜索功能 */}
  </div>
);

<Search SearchAdvanced={CustomSearchAdvanced} />
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

<td rowspan="1" colSpan="1" >`SearchResultItem`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >搜索结果数据</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >type</td>

<td rowspan="1" colSpan="1" >`SearchType`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >搜索结果类型</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >keyword</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >搜索关键词</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onClick</td>

<td rowspan="1" colSpan="1" >`(data: SearchResultItem, type: SearchType) => void`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >点击回调</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >className</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >自定义样式类名</td>
</tr>
</table>


**示例**
``` typescript
const CustomSearchItem = ({ data, type, keyword, onClick }) => (
  <div className="custom-item">
    {type === SearchType.MESSAGE && (
        <Conversation
          data={data}
          keyword={keyword}
          onClick={onClick}
        />
      )}
      {type === SearchType.USER && (
        <User
          data={data}
          keyword={keyword}
          onClick={onClick}
        />
      )}
      {type === SearchType.GROUP && (
        <Group
          data={data}
          keyword={keyword}
          onClick={onClick}
        />
      )}
      {type === SearchType.CHAT_MESSAGE && (
        <Message
          data={data}
          keyword={keyword}
          onClick={onClick}
        />
      )}
  </div>
);

<Search SearchResultItem={CustomSearchItem} />
```

【自定义占位组件】

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

<td rowspan="1" colSpan="1" >`React.ComponentType`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >搜索前占位符组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchResultsLoading</td>

<td rowspan="1" colSpan="1" >`React.ComponentType`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >加载中占位符组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchResultsEmpty</td>

<td rowspan="1" colSpan="1" >`React.ComponentType`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >空结果占位符组件</td>
</tr>
</table>


**示例**
``` typescript
<Search
  SearchResultsPresearch={() => <div>输入关键词开始搜索</div>}
  SearchResultsLoading={() => <div>搜索中...</div>}
  SearchResultsEmpty={() => <div>未找到相关结果</div>}
/>
```

## SearchState

SearchState 是基于 Zustand 的搜索状态管理钩子，为 Search 组件提供完整的状态管理能力。它支持多种搜索模式（标准模式、嵌入式模式），管理搜索关键词、搜索结果、加载状态、错误处理等功能。如果自定义组件能力不能支持您的业务，可以使用 SearchState 实现您的需求。

#### 数据
<table>
<tr>
<td rowspan="1" colSpan="1" >属性名</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >说明</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >keyword</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >当前搜索关键词</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >results</td>

<td rowspan="1" colSpan="1" >`Map<SearchType, SearchResult<SearchType>>`</td>

<td rowspan="1" colSpan="1" >搜索结果集合</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >isLoading</td>

<td rowspan="1" colSpan="1" >`boolean`</td>

<td rowspan="1" colSpan="1" >是否正在搜索</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >error</td>

<td rowspan="1" colSpan="1" >`Error \| null`</td>

<td rowspan="1" colSpan="1" >搜索错误信息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >searchAdvancedParams</td>

<td rowspan="1" colSpan="1" >`Map<ISearchType, SearchParamsMap[SearchType]>`</td>

<td rowspan="1" colSpan="1" >高级搜索参数</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >selectedSearchType</td>

<td rowspan="1" colSpan="1" >`SearchType \| 'all'`</td>

<td rowspan="1" colSpan="1" >当前选中的搜索类型</td>
</tr>
</table>


#### 操作方法
<table>
<tr>
<td rowspan="1" colSpan="1" >方法名</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >说明</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >setKeyword</td>

<td rowspan="1" colSpan="1" >`(k: string) => void`</td>

<td rowspan="1" colSpan="1" >设置搜索关键词</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >loadMore</td>

<td rowspan="1" colSpan="1" >`(type?: SearchType) => Promise<void>`</td>

<td rowspan="1" colSpan="1" >加载更多搜索结果</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >setSelectedType</td>

<td rowspan="1" colSpan="1" >`(type: SearchType \| 'all') => void`</td>

<td rowspan="1" colSpan="1" >设置搜索类型</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >setSearchMessageAdvancedParams</td>

<td rowspan="1" colSpan="1" >`(params: SearchCloudMessagesParams) => void`</td>

<td rowspan="1" colSpan="1" >设置消息搜索高级参数</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >setSearchUserAdvancedParams</td>

<td rowspan="1" colSpan="1" >`(params: SearchCloudUsersParams) => void`</td>

<td rowspan="1" colSpan="1" >设置用户搜索高级参数</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >setSearchGroupAdvancedParams</td>

<td rowspan="1" colSpan="1" >`(params: SearchCloudGroupsParams) => void`</td>

<td rowspan="1" colSpan="1" >设置群组搜索高级参数</td>
</tr>
</table>


## 使用示例
``` typescript
import { useSearchState, VariantType } from '@tencentcloud/chat-uikit-react';
const {
    keyword,
    results,
    isLoading,
    error,
    setKeyword,
    setSelectedType,
    loadMore
  } = useSearchState(VariantType.STANDARD);
  
```

## 常见问题

### Q: 如何自定义搜索结果的显示格式？

A: 使用 `SearchResultItem` 属性传入自定义组件。

### Q: 如何处理搜索性能问题？

A: 调整 `debounceTime`，使用 React.memo，考虑结果缓存。

### Q: 移动端如何优化？

A: 组件自动适配移动端，也可通过 CSS 进一步定制。

### Q: 如何支持多语言？

A: 组件内置国际化支持，通过 `useUIKit` 获取翻译。

