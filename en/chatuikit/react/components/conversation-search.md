> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/en/llms.txt
> Use this file to discover all available pages before exploring further.

`ConversationSearch` uses the Search component, supporting search functionality for users, groups, and messages. It integrates features such as the search bar, advanced search, and search result display.

## Basic Usage
``` typescript
import { 
   UIKitProvider, 
   ConversationList,
   ConversationSearch,
} from '@tencentcloud/chat-uikit-react';

import type {
   ConversationSearchProps,
   SearchResultItem,
   SearchType,
} from '@tencentcloud/chat-uikit-react';

const CustomConversationSearch = (props: ConversationSearchProps) => {
  const onSelectResult = (data: SearchResultItem, type: SearchType) => {
    console.warn(`Select Search Result: ${JSON.stringify(data)}, type: ${type}`);
  };
  return (
    <ConversationSearch {...props} onResultItemClick={onSelectResult} />
  );
};

const App = () => {
  return (
    <UIKitProvider>
      <ConversationList
        style={{ maxWidth: '300px', height: '600px' }}
        ConversationSearch={CustomConversationSearch}
       />
     </UIKitProvider>
  );
};
```

## Props
<table>
<tr>
<td rowspan="1" colSpan="1" >**Parameter Name**</td>

<td rowspan="1" colSpan="1" >**Type**</td>

<td rowspan="1" colSpan="1" >**Default Value**</td>

<td rowspan="1" colSpan="1" >**Description**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >visible</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >true</td>

<td rowspan="1" colSpan="1" >Whether it is visible.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[Search](https://write.woa.com/document/182866808150605824)</td>

<td rowspan="1" colSpan="1" >ComponentType<SearchProps></td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >custom search component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >variant</td>

<td rowspan="1" colSpan="1" >VariantType</td>

<td rowspan="1" colSpan="1" >VariantType.MINI</td>

<td rowspan="1" colSpan="1" >Search mode: mini, standard, embedded</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[SearchBar](https://write.woa.com/document/182866808150605824)</td>

<td rowspan="1" colSpan="1" >React.ComponentType<SearchBarProps></td>

<td rowspan="1" colSpan="1" >DefaultSearchBar</td>

<td rowspan="1" colSpan="1" >custom search bar component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[SearchResults](https://write.woa.com/document/182866808150605824)</td>

<td rowspan="1" colSpan="1" >React.ComponentType<SearchResultsProps></td>

<td rowspan="1" colSpan="1" >DefaultSearchResults</td>

<td rowspan="1" colSpan="1" >custom search result component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[SearchAdvanced](https://write.woa.com/document/182866808150605824)</td>

<td rowspan="1" colSpan="1" >React.ComponentType<SearchAdvancedProps></td>

<td rowspan="1" colSpan="1" >DefaultSearchAdvanced</td>

<td rowspan="1" colSpan="1" >custom advanced search component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchResultsPresearch</td>

<td rowspan="1" colSpan="1" >React.ComponentType</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >search placeholder component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchResultsLoading</td>

<td rowspan="1" colSpan="1" >React.ComponentType</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >loading placeholder component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchResultsEmpty</td>

<td rowspan="1" colSpan="1" >React.ComponentType</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >empty result placeholder component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchResultItem</td>

<td rowspan="1" colSpan="1" >React.ComponentType<ResultItemProps></td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >custom search result item component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >debounceTime</td>

<td rowspan="1" colSpan="1" >number</td>

<td rowspan="1" colSpan="1" >300</td>

<td rowspan="1" colSpan="1" >search debounce time (ms)</td>
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

<td rowspan="1" colSpan="1" >custom style class name</td>
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

<td rowspan="1" colSpan="1" >searchsearch keywords change callback']</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onSearchComplete</td>

<td rowspan="1" colSpan="1" >(results: Map<SearchType, SearchResult>) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >search completed callback</td>
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

<td rowspan="1" colSpan="1" >error callback</td>
</tr>
</table>


### 
