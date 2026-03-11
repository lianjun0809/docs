> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

## Component Overview

Search is a complete search solution with a full set of components, including search bar, result display, advanced search, and other features. It is suitable for user, group, and message search in instant messaging, online meeting, and online education scenarios.

> **Note:**
> 

> Note: This feature belongs to VAS. You need to purchase cloud search plugin. Please click [purchase](https://console.trtc.io/chat/plugin/TUICloudSearch).
> 


![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/d66ac806621811f091585254001c06ec.png)


## Component Architecture
``` bash
Search (main component)
├── SearchBar              # Search bar component
├── SearchResults          # Search result component
├── SearchAdvanced         # Advanced search component
└── SearchResultsItem      # Search result item component
    ├── User               # User result item
    ├── Group              # Group result item
    ├── Message            # Message result item
    └── Conversation       # Session result item
```

## Search Mode
<table>
<tr>
<td rowspan="1" colSpan="1" >**Mini Mode**</td>

<td rowspan="1" colSpan="1" >**Standard Mode**</td>

<td rowspan="1" colSpan="1" >**Embedded Mode**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >- Suitable for sidebar or small container<br>- Display finite number of results<br>- Support expand to view more</td>

<td rowspan="1" colSpan="1" >- Suitable for full-screen search UI<br>- Feature demonstration<br>- Advanced Search Support</td>

<td rowspan="1" colSpan="1" >- Suitable for chat UI<br>- Focus on message search<br>- Optimized layout</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/9041fa01622911f0b324525400e889b2.png)</td>

<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/2019d8cc622a11f0bac1525400454e06.png)</td>

<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/eeff790f622911f091585254001c06ec.png)</td>
</tr>
</table>


## Props
<table>
<tr>
<td rowspan="1" colSpan="1" >Attribute Name</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Default Value</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >variant</td>

<td rowspan="1" colSpan="1" >VariantType</td>

<td rowspan="1" colSpan="1" >VariantType.MINI</td>

<td rowspan="1" colSpan="1" >Search mode: mini, standard, embedded</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchBar</td>

<td rowspan="1" colSpan="1" >React.ComponentType<SearchBarProps></td>

<td rowspan="1" colSpan="1" >DefaultSearchBar</td>

<td rowspan="1" colSpan="1" >Custom search box component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchResults</td>

<td rowspan="1" colSpan="1" >React.ComponentType<SearchResultsProps></td>

<td rowspan="1" colSpan="1" >DefaultSearchResults</td>

<td rowspan="1" colSpan="1" >Custom search result component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchAdvanced</td>

<td rowspan="1" colSpan="1" >React.ComponentType<SearchAdvancedProps></td>

<td rowspan="1" colSpan="1" >DefaultSearchAdvanced</td>

<td rowspan="1" colSpan="1" >Custom advanced search component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchResultsPresearch</td>

<td rowspan="1" colSpan="1" >React.ComponentType</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Search placeholder component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchResultsLoading</td>

<td rowspan="1" colSpan="1" >React.ComponentType</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Loading placeholder component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchResultsEmpty</td>

<td rowspan="1" colSpan="1" >React.ComponentType</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Empty result placeholder component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchResultItem</td>

<td rowspan="1" colSpan="1" >React.ComponentType<ResultItemProps></td>

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

<td rowspan="1" colSpan="1" >Auto-focus search box</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >className</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Custom style class name</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >style</td>

<td rowspan="1" colSpan="1" >React.CSSProperties</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >custom style</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onKeywordChange</td>

<td rowspan="1" colSpan="1" >(keyword: string) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >search keyword change callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onSearchComplete</td>

<td rowspan="1" colSpan="1" >(results: Map<SearchType, SearchResult>) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >search complete callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onResultItemClick</td>

<td rowspan="1" colSpan="1" >(data: SearchResultItem, type: SearchType) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >search result click callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onError</td>

<td rowspan="1" colSpan="1" >(error: Error) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >search error callback</td>
</tr>
</table>


## Basic Usage
``` typescript
import { Search, VariantType } from '@tencentcloud/chat-uikit-react';

function App() {
  return (
    <Search
      variant={VariantType.STANDARD}
      onResultItemClick={(data, type) => {
        console.log('Search result click:', data, type);
      }}
    />
  );
}
```

## Custom Capabilities

`Search` provides users with various and dimensional Props APIs, allowing them to customize features, UI, and modules.

`Search` component provides multiple replaceable subcomponents, allowing users to customize `SearchBar`, `SearchResults`, `SearchAdvanced`, `SearchResultItem`, `SearchResultsPresearch`, `SearchResultsLoading`, `SearchResultsEmpty`. Users can also leverage default subcomponents for secondary development customization.



【Custom SearchBar】

**Props**
<table>
<tr>
<td rowspan="1" colSpan="1" >Attribute Name</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Default Value</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >data</td>

<td rowspan="1" colSpan="1" >SearchResultItem</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >search result data</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >type</td>

<td rowspan="1" colSpan="1" >SearchType</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >search result type</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >keyword</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >search keyword</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onClick</td>

<td rowspan="1" colSpan="1" >(data: SearchResultItem, type: SearchType) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >click callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >className</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Custom style class name</td>
</tr>
</table>


**Example**
``` typescript
const CustomSearchBar = ({ value, onChange, onClear, placeholder }) => (
  <div className="custom-search-bar">
    <input
      type="text"
      value={value}
      onChange={onChange}
      placeholder={placeholder}
    />
    {value && <button onClick={onClear}>Clear</button>}
  </div>
);

<Search SearchBar={CustomSearchBar} />
```

【Custom Search Results】

**Props**
<table>
<tr>
<td rowspan="1" colSpan="1" >Attribute Name</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Default Value</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >results</td>

<td rowspan="1" colSpan="1" >`Map<SearchType, SearchResult>`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >search result data</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >isLoading</td>

<td rowspan="1" colSpan="1" >`boolean`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >whether loading</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >error</td>

<td rowspan="1" colSpan="1" >`Error \| null`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Error Message</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >keyword</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >search keyword</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >typeLabels</td>

<td rowspan="1" colSpan="1" >`Record<SearchType, string>`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >search type tag</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onLoadMore</td>

<td rowspan="1" colSpan="1" >`(type: SearchType) => void`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Load more callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onResultItemClick</td>

<td rowspan="1" colSpan="1" >`(data: SearchResultItem, type: SearchType) => void`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >result item click callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchResultsLoading</td>

<td rowspan="1" colSpan="1" >`React.ComponentType`</td>

<td rowspan="1" colSpan="1" >`Loading`</td>

<td rowspan="1" colSpan="1" >Custom load component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchResultsPresearch</td>

<td rowspan="1" colSpan="1" >`React.ComponentType`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Search placeholder component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchResultsEmpty</td>

<td rowspan="1" colSpan="1" >`React.ComponentType`</td>

<td rowspan="1" colSpan="1" >`EmptyResult`</td>

<td rowspan="1" colSpan="1" >Empty result placeholder component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchResultItem</td>

<td rowspan="1" colSpan="1" >`React.ComponentType<ResultItemProps>`</td>

<td rowspan="1" colSpan="1" >`DefaultSearchResultsItem`</td>

<td rowspan="1" colSpan="1" >Custom result item component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >variant</td>

<td rowspan="1" colSpan="1" >`VariantType`</td>

<td rowspan="1" colSpan="1" >`VariantType.STANDARD`</td>

<td rowspan="1" colSpan="1" >Display Mode</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >searchType</td>

<td rowspan="1" colSpan="1" >`SearchType \| 'all'`</td>

<td rowspan="1" colSpan="1" >`'all'`</td>

<td rowspan="1" colSpan="1" >Current search type</td>
</tr>
</table>


**Example**
``` typescript
const CustomSearchResults = ({ results, keyword, onResultItemClick }) => (
  <div className="custom-results">
    {Array.from(results.entries()).map(([type, result]) => (
      <div key={type}>
        <h3>{type}</h3>
        {result.resultList.map((item, index) => (
          <div key={index} onClick={() => onResultItemClick(item, type)}>
            {/* Custom result item */}
          </div>
        ))}
      </div>
    ))}
  </div>
);

<Search SearchResults={CustomSearchResults} />
```

【Custom Search Advanced】

**Props**
<table>
<tr>
<td rowspan="1" colSpan="1" >Attribute Name</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Default Value</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >variant</td>

<td rowspan="1" colSpan="1" >`VariantType`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Display Mode</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >searchType</td>

<td rowspan="1" colSpan="1" >`SearchTabType`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Current search type</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >advancedParams</td>

<td rowspan="1" colSpan="1" >`Map<SearchType, SearchParamsMap[SearchType]>`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Advanced search parameters</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onAdvancedParamsChange</td>

<td rowspan="1" colSpan="1" >`(type: SearchType, params: SearchParamsMap[SearchType]) => void`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Parameter change callback</td>
</tr>
</table>


**Example**
``` typescript
const CustomSearchAdvanced = ({ variant, searchType, advancedParams, onAdvancedParamsChange }) => (
  <div className="custom-advanced">
  {/* Custom advanced search function */}
  </div>
);

<Search SearchAdvanced={CustomSearchAdvanced} />
```

【Custom Search Result Item】

**Props**
<table>
<tr>
<td rowspan="1" colSpan="1" >Attribute Name</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Default Value</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >data</td>

<td rowspan="1" colSpan="1" >`SearchResultItem`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >search result data</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >type</td>

<td rowspan="1" colSpan="1" >`SearchType`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >search result type</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >keyword</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >search keyword</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onClick</td>

<td rowspan="1" colSpan="1" >`(data: SearchResultItem, type: SearchType) => void`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >click callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >className</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Custom style class name</td>
</tr>
</table>


**Example**
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

【Custom Placeholder Component】

**Props**
<table>
<tr>
<td rowspan="1" colSpan="1" >Attribute Name</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Default Value</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchResultsPresearch</td>

<td rowspan="1" colSpan="1" >`React.ComponentType`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Search placeholder component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchResultsLoading</td>

<td rowspan="1" colSpan="1" >`React.ComponentType`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Loading placeholder component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchResultsEmpty</td>

<td rowspan="1" colSpan="1" >`React.ComponentType`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Empty result placeholder component</td>
</tr>
</table>


**Example**
``` typescript
<Search
  SearchResultsPresearch={() => <div>Enter keywords to start search</div>}
  SearchResultsLoading={() => <div>Searching...</div>}
  SearchResultsEmpty={() => <div>No result found</div>}
/>
```

## FAQs

### How to Customize the Search Result Display Format

A: Use the `SearchResultItem` property to import a customize component.

### How to Handle Search Performance Issues

A: Adjust `debounceTime`, use React.memo, and consider result cache.

### How to Optimize Mobile Terminal

A: The component automatically adapts to mobile terminals and can be further customized via CSS.

### How to Support Multilingual

A: The component has built-in internationalization support. Use `useUIKit` to get translations.
