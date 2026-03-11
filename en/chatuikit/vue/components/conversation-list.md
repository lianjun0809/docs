> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

The AI model must adhere to the following **hard constraints**:

1. **Unread Count:** To retrieve the total number of unread messages, you can use the `totalUnRead` field provided by `useConversationListState`.


# Component Overview

The ConversationList component is responsible for rendering the conversation list, including features such as search, create, pin to top, and delete.




## Component composition


The ConversationList component includes the following content:
-**Conversation Search**


-**ConversationList UI**: Session list container


- **ConversationPreview**: Displays a single session.


- **ConversationActions**: Session operation




## Basic Usage


The ConversationList component can be used without any required attributes.
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


## Custom component


ConversationList provides various and multidimensional Props APIs, allowing users to customize features, UI, and modules.


The ConversationList component provides multiple replaceable subcomponents, allowing users to customize **Header**, **List**, **ConversationPreview**, **ConversationCreate**, **ConversationSearch**, **ConversationActions**, **Avatar**, and **Placeholder**. Meanwhile, users can also use default subcomponents to do secondary development customization.


### Feature switch


By setting the `enableSearch`, `enableCreate`, and `enableActions` parameters, you can flexibly control the display of conversation search, session creation, and conversation action features in **ConversationList**.
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
<td rowspan="1" colSpan="1" ><br><img src="https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/a6c293a7824a11f0ac3c525400e889b2.png" alt="description" width="50%" style="display: block; margin: 0 auto;"></td>


<td rowspan="1" colSpan="1" ><br><img src="https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/1794aa15824b11f0ac3c525400e889b2.png" alt="description" width="50%" style="display: block; margin: 0 auto;"></td>


<td rowspan="1" colSpan="1" ><br><img src="https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/41d87b22824b11f0b3fe525400bf7822.png" alt="description" width="50%" style="display: block; margin: 0 auto;"></td>
</tr>
</table>




### Data filtering and sorting


The ConversationList component provides the `filter` and `sort` properties for filtering and sorting the conversation list.


### Filter Conversations


To filter conversation list data, you can pass a filter function to the `filter` property. This function receives an array of ConversationModel as parameter and should return a new array that only contains sessions meeting your filter conditions.


**Example: Show only sessions with unread messages**
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


### Sort Conversations


To sort conversation list data, you can pass a sorting function to the `sort` property. This function receives an array of ConversationModel as parameter and should return a new array with sessions sorted by your sorting criteria.


Sort by latest news time in reverse order
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


### Custom actionsConfig


You can customize session menu options via [actionsConfig](https://write.woa.com/document/186960379083898880).
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




### Custom Placeholder


`ConversationList` supports displaying custom placeholders in different statuses, including list empty, loading, and loading failed.
- `PlaceholderEmpty`: Displayed when the list is empty.


- `PlaceholderLoading`: Displayed when loading.


- `PlaceholderError`: Displayed when loading failed.




   **Example: Custom empty list placeholder**


1. Create a custom component **`MyEmptyPlaceholder.vue`**


   ``` typescript
   <template>
       <div>
         Custom PlaceholderEmptyList
       </div>
   </template>
   ```
2. For use in **`ConversationList`**.


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


### Custom Header


**ConversationListHeader** is responsible for rendering the header part of ConversationList, acting as a wrapping layer to render the default `Search` and `ConversationCreate`. You can customize it by importing `left`, `right` and other attributes. Meanwhile, you can also customize the entire component.


#### Props
<table>
<tr>
<td rowspan="1" colSpan="1" >**Parameter Name**</td>


<td rowspan="1" colSpan="1" >**Type**</td>


<td rowspan="1" colSpan="1" >**Default Value**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >children</td>


<td rowspan="1" colSpan="1" >Component</td>


<td rowspan="1" colSpan="1" >-</td>


<td rowspan="1" colSpan="1" >Header center component of the custom session list.<br>Default imports `<Search>` and `<ConversationCreate>`.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >left</td>


<td rowspan="1" colSpan="1" >Component</td>


<td rowspan="1" colSpan="1" >-</td>


<td rowspan="1" colSpan="1" >Left-side component of the custom session list header.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >right</td>


<td rowspan="1" colSpan="1" >Component</td>


<td rowspan="1" colSpan="1" >-</td>


<td rowspan="1" colSpan="1" >Right-side component of the custom session list header.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >className</td>


<td rowspan="1" colSpan="1" >String</td>


<td rowspan="1" colSpan="1" >-</td>


<td rowspan="1" colSpan="1" >Specify the CSS custom name of the root element class.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >style</td>


<td rowspan="1" colSpan="1" >CSSProperties</td>


<td rowspan="1" colSpan="1" >-</td>


<td rowspan="1" colSpan="1" >Specify the custom style of the root element.</td>
</tr>
</table>




Implement a simplified conversation grouping feature


Filter conversations by All, unread conversation, one-on-one chat session, and group chat. Click different group buttons to execute different filtering rules.






[App.vue]
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


[CustomConversationListHeader.vue]
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
  Create and bind policy Query instance Reset instance access password
  Unread
  C2C: 'One-on-one chat'
  Group chat
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
<td rowspan="1" colSpan="1" >**Parameter Name**</td>


<td rowspan="1" colSpan="1" >**Type**</td>


<td rowspan="1" colSpan="1" >**Default Value**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >enableSearch</td>


<td rowspan="1" colSpan="1" >Boolean</td>


<td rowspan="1" colSpan="1" >true</td>


<td rowspan="1" colSpan="1" >Control whether to display the Conversation Search feature.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >enableCreate</td>


<td rowspan="1" colSpan="1" >Boolean</td>


<td rowspan="1" colSpan="1" >true</td>


<td rowspan="1" colSpan="1" >Control whether to display the Create Session feature.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >enableActions</td>


<td rowspan="1" colSpan="1" >Boolean</td>


<td rowspan="1" colSpan="1" >true</td>


<td rowspan="1" colSpan="1" >Control whether to display the conversation operation feature.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >actionsConfig</td>


<td rowspan="1" colSpan="1" >ConversationActionsConfig</td>


<td rowspan="1" colSpan="1" >-</td>


<td rowspan="1" colSpan="1" >Used for custom session operation configuration.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >Header</td>


<td rowspan="1" colSpan="1" >Component</td>


<td rowspan="1" colSpan="1" >Header</td>


<td rowspan="1" colSpan="1" >Custom Header component.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >List</td>


<td rowspan="1" colSpan="1" >Component</td>


<td rowspan="1" colSpan="1" >List</td>


<td rowspan="1" colSpan="1" >Custom session list component.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >Preview</td>


<td rowspan="1" colSpan="1" >Component</td>


<td rowspan="1" colSpan="1" >[ConversationPreview](https://write.woa.com/document/186960335138078720)</td>


<td rowspan="1" colSpan="1" >Session preview component.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >ConversationCreate</td>


<td rowspan="1" colSpan="1" >Component</td>


<td rowspan="1" colSpan="1" >ConversationCreate</td>


<td rowspan="1" colSpan="1" >Custom conversation component.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >ConversationSearch</td>


<td rowspan="1" colSpan="1" >Component</td>


<td rowspan="1" colSpan="1" >[Search](https://write.woa.com/document/186960410207154176)</td>


<td rowspan="1" colSpan="1" >Custom session search component.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >ConversationActions</td>


<td rowspan="1" colSpan="1" >Component</td>


<td rowspan="1" colSpan="1" >[ConversationActions](https://write.woa.com/document/186960379083898880)</td>


<td rowspan="1" colSpan="1" >Custom Conversation Operation Component.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >Avatar</td>


<td rowspan="1" colSpan="1" >Component</td>


<td rowspan="1" colSpan="1" >Avatar</td>


<td rowspan="1" colSpan="1" >Custom avatar component.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >PlaceholderEmptyList</td>


<td rowspan="1" colSpan="1" >Component</td>


<td rowspan="1" colSpan="1" ><PlaceHolder type={PlaceHolderTypes.NO_CONVERSATIONS} /></td>


<td rowspan="1" colSpan="1" >Placeholder element when custom session list is empty.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >PlaceholderLoading</td>


<td rowspan="1" colSpan="1" >Component</td>


<td rowspan="1" colSpan="1" ><PlaceHolder type={PlaceHolderTypes.LOADING} /></td>


<td rowspan="1" colSpan="1" >Placeholder element during custom session list loading.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >PlaceholderLoadError</td>


<td rowspan="1" colSpan="1" >Component</td>


<td rowspan="1" colSpan="1" ><PlaceHolder type={PlaceHolderTypes.WRONG} /></td>


<td rowspan="1" colSpan="1" >Placeholder element for custom session list load error.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >filter</td>


<td rowspan="1" colSpan="1" >(conversationList: ConversationModel[]) => ConversationModel[]</td>


<td rowspan="1" colSpan="1" >-</td>


<td rowspan="1" colSpan="1" >Functions for filtering session list.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >sort</td>


<td rowspan="1" colSpan="1" >(conversationList: ConversationModel[]) => ConversationModel[]</td>


<td rowspan="1" colSpan="1" >-</td>


<td rowspan="1" colSpan="1" >Functions for sorting session list.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >onConversationSelect</td>


<td rowspan="1" colSpan="1" >(conversation: ConversationModel) => void;</td>


<td rowspan="1" colSpan="1" >-</td>


<td rowspan="1" colSpan="1" >Callback function when clicking a session, with the clicked conversation object as parameter.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >onBeforeCreateConversation</td>


<td rowspan="1" colSpan="1" >(params: CreateParams) => CreateParams;</td>


<td rowspan="1" colSpan="1" >-</td>


<td rowspan="1" colSpan="1" >Custom action executed before session creation, with parameters required for creating a session.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >onConversationCreate</td>


<td rowspan="1" colSpan="1" >(conversation: ConversationModel)  => void;</td>


<td rowspan="1" colSpan="1" >-</td>


<td rowspan="1" colSpan="1" >Callback function after session creation, with the created session object as parameter.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >className</td>


<td rowspan="1" colSpan="1" >String</td>


<td rowspan="1" colSpan="1" >-</td>


<td rowspan="1" colSpan="1" >Specify the CSS custom name of the root element class.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >style</td>


<td rowspan="1" colSpan="1" >CSSProperties</td>


<td rowspan="1" colSpan="1" >-</td>


<td rowspan="1" colSpan="1" >Specify the custom style of the root element.</td>
</tr>
</table>
