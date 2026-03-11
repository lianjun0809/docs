> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

# Component Overview


The `ConversationList` component is primarily responsible for the List function. It contains the Header part and List part, and has features such as conversation search, session creation, session pinning, and conversation deletion.


This document introduces in detail the foundation usage, component customization, freely combine and the props parameter list of the component.
<table>
<tr>
<td rowspan="1" colSpan="1" >**Conversation List**</td>


<td rowspan="1" colSpan="1" >**Session Operation**</td>


<td rowspan="1" colSpan="1" >**Conversation Search**</td>


<td rowspan="1" colSpan="1" >**Create Session**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027119864/c36abe657b2211ef82535254002693fd.png)</td>


<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027119864/9b217da57b2211ef852f52540075b605.png)</td>


<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027119864/d90a84b27b2211efa87a525400bdab9d.png)</td>


<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027119864/07c380377b2311efa87e52540055f650.png)</td>
</tr>
</table>




## Component composition


The `ConversationList` component contains the following content:
-`ConversationSearch` - Conversation Search


- `ConversationList UI` - Conversation List Container


- `ConversationPreview` - Show Session Information


- `ConversationActions` - Conversation Action


   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027119864/6346335903ce11f0ae895254005ef0f7.png)




## Basic usage


The `ConversationList` component has no required properties. You can use `ConversationList` with the following code.
``` typescript
import { UIKitProvider, ConversationList } from '@tencentcloud/chat-uikit-react';


const App = () => {
  return (
    <UIKitProvider>
      <ConversationList />
    </UIKitProvider>
  );
};
```


## Custom components


`ConversationList` provides various dimensional Props APIs for user customization, allowing users to customize features, UI, modules and more.


The `ConversationList` component provides multiple replaceable subcomponents, allowing users to customize `Header`, `List`, `ConversationPreview`, `ConversationCreate`, `ConversationSearch`, `ConversationActions`, `Avatar`, `Placeholder`, and more. Meanwhile, users can also use default subcomponents for secondary development customization.


### Basic feature switch


By setting the `enableSearch`, `enableCreate`, and `enableActions` parameters, you can flexibly control the display of conversation search, session creation, and conversation action features in `ConversationList`.
``` typescript
<ConversationList enableSearch={false} />
```
``` typescript
<ConversationList enableCreate={false} />
```
``` typescript
<ConversationList enableActions={false} />
```
<table>
<tr>
<td rowspan="1" colSpan="1" >`enableSearch={false}`</td>


<td rowspan="1" colSpan="1" >`enableCreate={false}`</td>


<td rowspan="1" colSpan="1" >`enableActions={false}`</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027119864/04e7a7b87b2411efa87a525400bdab9d.png)</td>


<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027119864/04eb02137b2411ef82535254002693fd.png)</td>


<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027119864/04e843b67b2411ef8829525400fdb830.png)</td>
</tr>
</table>




### Data filtering and sorting


The `ConversationList` component provides the `filterConversation` and `sortConversation` properties, allowing you to filter and sort the conversation list data.


#### Filter conversations


To filter conversation list data, you can pass a filter function to the `filterConversation` property. This function receives an array of `ConversationModel` as parameter and should return a new array that only contains conversations meeting your filter criteria.


Here is an example of using the `filterConversation` property to only display conversations with "unread messages":
``` typescript
import { ConversationList } from '@tencentcloud/chat-uikit-react';
import type { ConversationModel } from '@tencentcloud/chat-uikit-react';


<ConversationList
  filter={(conversationList: ConversationModel[]) =>
    conversationList.filter(conversation => conversation.unreadCount > 0)}
/>
```


#### Sort conversations


To sort conversation list data, you can pass a sorting function to the `sortConversation` property. This function receives an array of `ConversationModel` as parameter and should return a new array with sessions sorted by your sorting criteria.


Here is an example of using the `sortConversation` property to sort the session list by "latest news time" in descending order:
``` typescript
import { ConversationList } from '@tencentcloud/chat-uikit-react';
import type { ConversationModel } from '@tencentcloud/chat-uikit-react';


<ConversationList
  sort={(conversationList: ConversationModel[]) =>
    conversationList.sort(
      (a, b) => (+(b?.lastMessage?.lastTime || 0)) - (+(a?.lastMessage?.lastTime || 0)),
    )}
/>
```


By using the `filter` and `sort` properties, you can effectively filter and sort the conversation list data according to your needs.


### Custom actionsConfig


Leverages [actionsConfig](https://write.woa.com/document/157860973841612800) to control the basic feature of ConversationActions.


For more customization, see the [ConversationActions](https://write.woa.com/document/157860973841612800) chapter.
``` typescript
import { ConversationList } from '@tencentcloud/chat-uikit-react';
import type { ConversationModel } from '@tencentcloud/chat-uikit-react';


<ConversationList
  actionsConfig={{
    enablePin: false,
    onConversationDelete: (conversation: ConversationModel) => { console.log('Delete conversation success'); },
    customConversationActions: {
      'custom-actions-1': {
        label: 'custom-actions',
        onClick: (conversation: ConversationModel) => { console.log(conversation); },
      },
    },
  }}
/>
```
<table>
<tr>
<td rowspan="1" colSpan="1" >`enablePin: false`</td>


<td rowspan="1" colSpan="1" >`enableDelete: false`</td>


<td rowspan="1" colSpan="1" >`enableMute: false`</td>


<td rowspan="1" colSpan="1" >`customConversationActions`</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027119864/adaf4f4c7b4211efa87e52540055f650.png)</td>


<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027119864/d05321b37b4211ef82535254002693fd.png)</td>


<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027119864/e45d60e87b4211ef8829525400fdb830.png)</td>


<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027119864/fd8cbea27b4211efb9d8525400f69702.png)</td>
</tr>
</table>




### Custom Placeholder


You can customize the list display in different statuses by importing `PlaceholderEmptyList`, `PlaceholderLoading`, and `PlaceholderLoadError`.


Here is a custom `PlaceholderLoading` example:
``` typescript
import { ConversationList } from '@tencentcloud/chat-uikit-react';


<ConversationList
  PlaceholderEmptyList={<div>Empty List!!!</div>}
/>
```


### Custom Header


`ConversationListHeader` is responsible for rendering the header part of `ConversationList`, serving as a wrapping layer to render the default `ConversationSearch` and `ConversationCreate`. You can customize it by importing left, right and other attributes, and you can also customize the entire component.


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


<td rowspan="1" colSpan="1" >`ReactNode`</td>


<td rowspan="1" colSpan="1" >-</td>


<td rowspan="1" colSpan="1" >Custom session list header center component.<br>When used in `<ConversationList>`, it imports `<ConversationSearch>` and `<ConversationCreate>` by default.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >left</td>


<td rowspan="1" colSpan="1" >`ReactElement`</td>


<td rowspan="1" colSpan="1" >-</td>


<td rowspan="1" colSpan="1" >Custom session list header left-side component.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >right</td>


<td rowspan="1" colSpan="1" >`ReactElement`</td>


<td rowspan="1" colSpan="1" >-</td>


<td rowspan="1" colSpan="1" >Custom session list header right-side component.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >className</td>


<td rowspan="1" colSpan="1" >`String`</td>


<td rowspan="1" colSpan="1" >-</td>


<td rowspan="1" colSpan="1" >Specify the custom name for the root element's CSS class.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >style</td>


<td rowspan="1" colSpan="1" >`React.CSSProperties`</td>


<td rowspan="1" colSpan="1" >-</td>


<td rowspan="1" colSpan="1" >Specify the custom style for the root element.</td>
</tr>
</table>


### Basic customization


Here is an example of adding a new function button on the right side of the Header Component.
``` typescript
import { 
  ConversationList,
  ConversationListHeader,
} from '@tencentcloud/chat-uikit-react';
import type { ConversationListHeaderProps } from '@tencentcloud/chat-uikit-react';


const CustomConversationListHeader = (props: ConversationListHeaderProps) => {
    const CustomIcon = <div>Custom Icon</div>;
    return (
      <ConversationListHeader {...props} right={CustomIcon} />
    );
};  
     
<ConversationList Header={CustomConversationListHeader} />
```


#### Advanced customization


Here is how to implement a simplified conversation grouping feature, distinguishing by All conversations, unread conversations, one-on-one chat sessions, and group chats across four key dimensions. Click different group buttons to execute different filtering rules.
<table>
<tr>
<td rowspan="1" colSpan="1" >**Before modification**</td>


<td rowspan="1" colSpan="1" >**Modified**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027119864/d55e54fb7b3511ef852f52540075b605.png)</td>


<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027119864/7eaf71657b3511efa87a525400bdab9d.png)![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027119864/8d7252bc7b3511efa87a525400bdab9d.png)![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027119864/aad34b767b3511ef80ff525400d5f8ef.png)![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027119864/bd04478f7b3511ef852f52540075b605.png)</td>
</tr>
</table>








[React]
``` typescript
import { useState } from 'react';
import TUIChatEngine from '@tencentcloud/chat-uikit-engine';
import { ConversationList, UIKitProvider } from '@tencentcloud/chat-uikit-react';
import type { ConversationListHeaderProps, ConversationModel } from '@tencentcloud/chat-uikit-react';


const App = () => {
  const [currentFilter, setCurrentFilter] = useState<string>('all');
  const conversationGroupFilter: Record<string, (conversationList: ConversationModel[]) => ConversationModel[]> = {
    all: (conversationList: ConversationModel[]) => conversationList,
    unread: (conversationList: ConversationModel[]) => conversationList?.filter((item: ConversationModel) => item.unreadCount > 0),
    c2c: (conversationList: ConversationModel[]) => conversationList?.filter((item: ConversationModel) => item.type === TUIChatEngine.TYPES.CONV_C2C),
    group: (conversationList: ConversationModel[]) => conversationList?.filter((item: ConversationModel) => item.type === TUIChatEngine.TYPES.CONV_GROUP),
  };


  const CustomConversationListHeader = (props: IConversationListHeaderProps) => {
    return (
      <div className="conversation-group-wrapper">
        <button className={currentFilter === 'all' ? 'btn-active' : 'btn-default'} onClick={() => setCurrentFilter('all')}>All</button>
        <button className={currentFilter === 'unread' ? 'btn-active' : 'btn-default'} onClick={() => setCurrentFilter('unread')}>Unread</button>
        <button className={currentFilter === 'c2c' ? 'btn-active' : 'btn-default'} onClick={() => setCurrentFilter('c2c')}>C2C</button>
        <button className={currentFilter === 'group' ? 'btn-active' : 'btn-default'} onClick={() => setCurrentFilter('group')}>Group</button>
      </div>
    );
  };


  return (
    <UIKitProvider>
      <ConversationList
        style={{ maxWidth: '300px', height: '600px' }}
        Header={CustomConversationListHeader}
        filter={conversationGroupFilter[currentFilter]}
      />
    </UIKitProvider>
  );
};
```


[CSS]
``` scss
.conversation-group-wrapper {
  display: flex;
  justify-content: space-around;
  align-items: center;
  margin: 10px;
  font-size: 14px;
  .btn-default{
    display: flex;
    padding: 5px 10px;
    border: 1px solid #b3b3b4;
    color: #3b3d43;
    background-color: transparent;
    border-radius: 2px;
  }
  .btn-active{
    display: flex;
    padding: 5px 10px;
    border: 1px solid #1c66e5;
    color: #1c66e5;
    background-color: transparent;
    border-radius: 2px;
  }
}
```


Custom List


`ConversationListContent` is responsible for the rendering work of the main list part in `ConversationList`.


Render the precomputed current session list `filteredAndSortedConversationList` from Context as the default wrapping layer.


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


<td rowspan="1" colSpan="1" >`ReactNode`</td>


<td rowspan="1" colSpan="1" >-</td>


<td rowspan="1" colSpan="1" >Custom session list content area component.<br>When used in `<ConversationList>`, it imports the `<Preview>` list traversed by `filteredAndSortedConversationList` by default.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >empty</td>


<td rowspan="1" colSpan="1" >`Boolean`</td>


<td rowspan="1" colSpan="1" >`false`</td>


<td rowspan="1" colSpan="1" >Conversation list identifier bit. When used in `<ConversationList>`, it judges `filteredAndSortedConversationList.length === 0` and imports it.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >loading</td>


<td rowspan="1" colSpan="1" >`Boolean`</td>


<td rowspan="1" colSpan="1" >`false`</td>


<td rowspan="1" colSpan="1" >Conversation list loading flag bit. When used in `<ConversationList>`, it uses `useConversationList()` to get `isLoading` and imports it.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >error</td>


<td rowspan="1" colSpan="1" >`Boolean`</td>


<td rowspan="1" colSpan="1" >`false`</td>


<td rowspan="1" colSpan="1" >Conversation list load error flag bit. When used in `<ConversationList>`, it uses `useConversationList()` to get `isLoadError` and imports it.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >PlaceholderEmptyList</td>


<td rowspan="1" colSpan="1" >`ReactNode`</td>


<td rowspan="1" colSpan="1" >`<PlaceHolder type={PlaceHolderTypes.NO_CONVERSATIONS} />`</td>


<td rowspan="1" colSpan="1" >Placeholder element when the custom session list is empty.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >PlaceholderLoading</td>


<td rowspan="1" colSpan="1" >`ReactNode`</td>


<td rowspan="1" colSpan="1" >`<PlaceHolder type={PlaceHolderTypes.LOADING} />`</td>


<td rowspan="1" colSpan="1" >Placeholder element for custom session list loading.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >PlaceholderLoadError</td>


<td rowspan="1" colSpan="1" >`ReactNode`</td>


<td rowspan="1" colSpan="1" >`<PlaceHolder type={PlaceHolderTypes.WRONG} />`</td>


<td rowspan="1" colSpan="1" >Placeholder element for custom session list load error.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >className</td>


<td rowspan="1" colSpan="1" >`String`</td>


<td rowspan="1" colSpan="1" >-</td>


<td rowspan="1" colSpan="1" >Specify the custom name for the root element's CSS class.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >style</td>


<td rowspan="1" colSpan="1" >`React.CSSProperties`</td>


<td rowspan="1" colSpan="1" >-</td>


<td rowspan="1" colSpan="1" >Specify the custom style for the root element.</td>
</tr>
</table>




Basic customization


The UI effects of the `List` component in different statuses are as follows. The trigger timing for each state is handled inside the `ConversationList`.


Meanwhile, you can control the component status through custom input of `empty`, `loading`, and `error`.
``` typescript
import { ConversationList, ConversationListContent } from '@tencentcloud/chat-uikit-react';
import type { ConversationListContentProps } from '@tencentcloud/chat-uikit-react';


const CustomConversationListContent = (props: ConversationListContentProps) => {
    return <ConversationListContent {...props} loading={true} />;
};


<ConversationList  List={CustomConversationListContent} />
```
<table>
<tr>
<td rowspan="1" colSpan="1" >`default`</td>


<td rowspan="1" colSpan="1" >`empty={true}`</td>


<td rowspan="1" colSpan="1" >`loading={true}`</td>


<td rowspan="1" colSpan="1" >`error={true}`</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027119864/672801bf7b3f11efa87e52540055f650.png)</td>


<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027119864/38392e897b3f11efb9d8525400f69702.png)</td>


<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027119864/4a40aeb27b3f11ef8631525400a9236a.png)</td>


<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027119864/5b245e9b7b3f11efb9d8525400f69702.png)</td>
</tr>
</table>




Custom ConversationPreview


For details, see the [ConversationPreview](https://write.woa.com/document/157860950620008448) chapter.
``` typescript
<ConversationList ConversationPreview={CustomConversationPreview} />
```


Custom ConversationActions


For details, see the [ConversationActions](https://write.woa.com/document/157860973841612800) chapter.
``` typescript
  <ConversationList ConversationActions={CustomConversationActions} />
```


Custom ConversationSearch


For details, see the [ConversationSearch](https://write.woa.com/document/157860965047783424) chapter.
``` typescript
<ConversationList ConversationSearch={CustomConversationSearch} />
```


Create and Bind Policy Query Instance Reset Instance Access Password
``` typescript
<ConversationList ConversationCreate={CustomConversationCreate} />
```


Custom Avatar
``` typescript
<ConversationList Avatar={CustomAvatar} />
```


## APIs/Props
<table>
<tr>
<td rowspan="1" colSpan="1" >**Parameter Name**</td>


<td rowspan="1" colSpan="1" >**Type**</td>


<td rowspan="1" colSpan="1" >**Default Value**</td>


<td rowspan="1" colSpan="1" >**Description**</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >enableSearch</td>


<td rowspan="1" colSpan="1" >`Boolean`</td>


<td rowspan="1" colSpan="1" >`true`</td>


<td rowspan="1" colSpan="1" >Whether to display the control session search feature.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >enableCreate</td>


<td rowspan="1" colSpan="1" >`Boolean`</td>


<td rowspan="1" colSpan="1" >`true`</td>


<td rowspan="1" colSpan="1" >Whether to display the control session creation feature.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >enableActions</td>


<td rowspan="1" colSpan="1" >`Boolean`</td>


<td rowspan="1" colSpan="1" >`true`</td>


<td rowspan="1" colSpan="1" >Whether to display the conversation action feature.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >actionsConfig</td>


<td rowspan="1" colSpan="1" >`ConversationActionsConfig`</td>


<td rowspan="1" colSpan="1" >-</td>


<td rowspan="1" colSpan="1" >For custom session operation configuration.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >Header</td>


<td rowspan="1" colSpan="1" >`ReactElement`</td>


<td rowspan="1" colSpan="1" >`Header`</td>


<td rowspan="1" colSpan="1" >Custom Header component.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >List</td>


<td rowspan="1" colSpan="1" >`ReactElement`</td>


<td rowspan="1" colSpan="1" >`List`</td>


<td rowspan="1" colSpan="1" >Custom session list component.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >Preview</td>


<td rowspan="1" colSpan="1" >`ReactElement`</td>


<td rowspan="1" colSpan="1" >[ConversationPreview](https://write.woa.com/document/157860950620008448)</td>


<td rowspan="1" colSpan="1" >Session preview component.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >ConversationCreate</td>


<td rowspan="1" colSpan="1" >`ReactElement`</td>


<td rowspan="1" colSpan="1" >`ConversationCreate`</td>


<td rowspan="1" colSpan="1" >Custom conversation component.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >ConversationSearch</td>


<td rowspan="1" colSpan="1" >`ReactElement`</td>


<td rowspan="1" colSpan="1" >[ConversationSearch](https://write.woa.com/document/157860965047783424)</td>


<td rowspan="1" colSpan="1" >Custom session search component.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >ConversationActions</td>


<td rowspan="1" colSpan="1" >`ReactElement`</td>


<td rowspan="1" colSpan="1" >[ConversationActions](https://write.woa.com/document/157860973841612800)</td>


<td rowspan="1" colSpan="1" >Custom Conversation Operation Component.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >Avatar</td>


<td rowspan="1" colSpan="1" >`ReactElement`</td>


<td rowspan="1" colSpan="1" >`Avatar`</td>


<td rowspan="1" colSpan="1" >Custom avatar component.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >PlaceholderEmptyList</td>


<td rowspan="1" colSpan="1" >`ReactNode`</td>


<td rowspan="1" colSpan="1" >`<PlaceHolder type={PlaceHolderTypes.NO_CONVERSATIONS} />`</td>


<td rowspan="1" colSpan="1" >Placeholder element when the custom session list is empty.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >PlaceholderLoading</td>


<td rowspan="1" colSpan="1" >`ReactNode`</td>


<td rowspan="1" colSpan="1" >`<PlaceHolder type={PlaceHolderTypes.LOADING} />`</td>


<td rowspan="1" colSpan="1" >Placeholder element for custom session list loading.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >PlaceholderLoadError</td>


<td rowspan="1" colSpan="1" >`ReactNode`</td>


<td rowspan="1" colSpan="1" >`<PlaceHolder type={PlaceHolderTypes.WRONG} />`</td>


<td rowspan="1" colSpan="1" >Placeholder element for custom session list load error.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >filter</td>


<td rowspan="1" colSpan="1" >`(conversationList: ConversationModel[]) => ConversationModel[]`</td>


<td rowspan="1" colSpan="1" >-</td>


<td rowspan="1" colSpan="1" >Functions for filtering session list.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >sort</td>


<td rowspan="1" colSpan="1" >`(conversationList: ConversationModel[]) => ConversationModel[]`</td>


<td rowspan="1" colSpan="1" >-</td>


<td rowspan="1" colSpan="1" >Functions for sorting session list.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >onConversationSelect</td>


<td rowspan="1" colSpan="1" >`(conversation: ConversationModel) => void;`</td>


<td rowspan="1" colSpan="1" >-</td>


<td rowspan="1" colSpan="1" >Callback function when clicking a session, with the clicked conversation object as parameter.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >onBeforeCreateConversation</td>


<td rowspan="1" colSpan="1" >`(params: CreateParams) => CreateParams;`</td>


<td rowspan="1" colSpan="1" >-</td>


<td rowspan="1" colSpan="1" >Custom action executed before session creation, with required parameters for creating a session.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >onConversationCreate</td>


<td rowspan="1" colSpan="1" >`(conversation: ConversationModel)  => void;`</td>


<td rowspan="1" colSpan="1" >-</td>


<td rowspan="1" colSpan="1" >Callback function after session creation, with the created session object as parameter.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >className</td>


<td rowspan="1" colSpan="1" >`String`</td>


<td rowspan="1" colSpan="1" >-</td>


<td rowspan="1" colSpan="1" >Specify the custom name for the root element's CSS class.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >style</td>


<td rowspan="1" colSpan="1" >`React.CSSProperties`</td>


<td rowspan="1" colSpan="1" >-</td>


<td rowspan="1" colSpan="1" >Specify the custom style for the root element.</td>
</tr>
</table>
