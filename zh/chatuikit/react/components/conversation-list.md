> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

## 组件概述

`ConversationList` 组件主要负责会话列表功能，它包含了 Header 部分和 List 部分，具有搜索会话、创建会话、会话置顶、会话删除等功能。

本文档将详细介绍该组件的基础使用，组件定制，自由组合以及组件的 props 参数列表。
<table>
<tr>
<td rowspan="1" colSpan="1" >**会话列表**</td>

<td rowspan="1" colSpan="1" >**会话操作**</td>

<td rowspan="1" colSpan="1" >**会话搜索**</td>

<td rowspan="1" colSpan="1" >**创建会话**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027119864/c36abe657b2211ef82535254002693fd.png)</td>

<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027119864/9b217da57b2211ef852f52540075b605.png)</td>

<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027119864/d90a84b27b2211efa87a525400bdab9d.png)</td>

<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027119864/07c380377b2311efa87e52540055f650.png)</td>
</tr>
</table>


## 组件构成

`ConversationList` 组件包含以下内容：
- `ConversationSearch` - 会话搜索

- `ConversationList UI` - 会话列表容器

- `ConversationPreview` - 单条会话信息展示

- `ConversationActions` - 单条会话操作

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027119864/6346335903ce11f0ae895254005ef0f7.png)


## 基础使用

`ConversationList` 组件没有任何必须属性，您可以通过以下代码使用 `ConversationList`。
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

## 自定义组件

`ConversationList` 为用户自定义提供了丰富且多维度的 Props 接口，允许用户自定义功能、UI、模块等。

`ConversationList` 组件提供了多个可替换的子组件，允许用户自定义 `Header`, `List`, `ConversationPreview`, `ConversationCreate`, `ConversationSearch`, `ConversationActions`, `Avatar`, `Placeholder` 等。同时，用户还可以利用默认子组件进行二次开发定制。

### 基础功能开关

通过设置 `enableSearch`, `enableCreate` 和 `enableActions` 参数，您可以灵活地控制 `ConversationList` 中的搜索会话、创建会话和会话操作功能的显示。
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


### 数据筛选和排序

ConversationList 组件提供了 `filterConversation` 和 `sortConversation` 属性，可以让您对会话列表数据进行筛选和排序。

#### 筛选会话

要筛选会话列表数据，您可以给 `filterConversation` 属性传递一个筛选函数。这个函数接收一个 ConversationModel 数组作为参数，然后应该返回一个新数组，只包含符合您筛选条件的会话。

下面是一个使用 `filterConversation` 属性来只显示“包含未读消息”的会话的例子：
``` typescript
import { ConversationList } from '@tencentcloud/chat-uikit-react';
import type { ConversationModel } from '@tencentcloud/chat-uikit-react';

<ConversationList
  filter={(conversationList: ConversationModel[]) =>
    conversationList.filter(conversation => conversation.unreadCount > 0)}
/>
```

#### 排序会话

要排序会话列表数据，您可以给 `sortConversation` 属性传递一个排序函数。这个函数接收一个 ConversationModel 数组作为参数，然后应该返回一个新数组，按照您的排序标准对会话进行排序。

下面是一个使用 `sortConversation` 属性来按照“最新消息时间倒序”排序会话列表的例子：
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

通过使用 `filter` 和 `sort` 属性，您可以根据您的需求有效地筛选和排序会话列表数据。

### 自定义 actionsConfig

利用 [actionsConfig](https://write.woa.com/document/157860973841612800) 对 ConversationActions 的基础功能进行控制。

更多定制请详情参见 [ConversationActions](https://write.woa.com/document/157860973841612800) 章节。
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


### 自定义 Placeholder

您可以通过传入 `PlaceholderEmptyList`、`PlaceholderLoading` 以及 `PlaceholderLoadError` 来定制不同状态下的列表展示。

以下是定制一个新的 `PlaceholderLoading` 示例：
``` typescript
import { ConversationList } from '@tencentcloud/chat-uikit-react';

<ConversationList
  PlaceholderEmptyList={<div>Empty List!!!</div>}
/>
```

### 自定义 Header

`ConversationListHeader` 负责 ConversationList Header 部分的渲染工作，作为包裹层渲染默认 `ConversationSearch` 与 `ConversationCreate` 。您可以通过传入 left、right 等属性进行自定义，同时，您也可以自定义整个组件。

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

<td rowspan="1" colSpan="1" >`ReactNode`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >自定义会话列表头部中心组件。<br>在 `<ConversationList>` 中使用时，会默认传入 `<ConversationSearch>` 和 `<ConversationCreate>` 。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >left</td>

<td rowspan="1" colSpan="1" >`ReactElement`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >自定义会话列表头部左侧组件。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >right</td>

<td rowspan="1" colSpan="1" >`ReactElement`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >自定义会话列表头部右侧组件。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >className</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >指定根元素类的 CSS 自定义名称。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >style</td>

<td rowspan="1" colSpan="1" >`React.CSSProperties`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >指定根元素样式的自定义样式。</td>
</tr>
</table>


#### 基础定制

以下是在 Header 组件右侧添加一个新的功能按钮示例。
``` typescript
import { 
  ConversationList,
  ConversationListHeader,
} from '@tencentcloud/chat-uikit-react';
import type { ConversationListHeaderProps } from '@tencentcloud/chat-uikit-react';

const CustomConversationListHeader = (props: ConversationListHeaderProps) => {
    const CustomIcon = <div>自定义 Icon </div>;
    return (
      <ConversationListHeader {...props} right={CustomIcon} />
    );
};	
     
<ConversationList Header={CustomConversationListHeader} />
```

#### 高阶定制

以下是实现一个简易的会话分组功能，按照全部会话、未读会话、单聊会话、群会话四个维度进行区分，通过点击不同分组按钮执行不同的筛选规则。
<table>
<tr>
<td rowspan="1" colSpan="1" >**修改前**</td>

<td rowspan="1" colSpan="1" >**修改后**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027119864/d55e54fb7b3511ef852f52540075b605.png)</td>

<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027119864/7eaf71657b3511efa87a525400bdab9d.png)![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027119864/8d7252bc7b3511efa87a525400bdab9d.png)![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027119864/aad34b767b3511ef80ff525400d5f8ef.png)![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027119864/bd04478f7b3511ef852f52540075b605.png)</td>
</tr>
</table>




【React】
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

【CSS】
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

### 自定义 List

`ConversationListContent` 负责 ConversationList 主列表部分的渲染工作。

作为包裹层默认渲染 Context 中计算好的当前会话列表显示数据 `filteredAndSortedConversationList`。

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

<td rowspan="1" colSpan="1" >`ReactNode`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >自定义会话列表内容区域组件。<br>在 `<ConversationList> `中使用时，会默认传入 `filteredAndSortedConversationList` 遍历的 `<Preview>` 列表。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >empty</td>

<td rowspan="1" colSpan="1" >`Boolean`</td>

<td rowspan="1" colSpan="1" >`false`</td>

<td rowspan="1" colSpan="1" >空会话列表标识位, 在 `<ConversationList>` 中使用时，会判断`filteredAndSortedConversationList.length === 0` 并传入。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >loading</td>

<td rowspan="1" colSpan="1" >`Boolean`</td>

<td rowspan="1" colSpan="1" >`false`</td>

<td rowspan="1" colSpan="1" >会话列表加载中标识位，在 `<ConversationList>` 中使用时，使用 `useConversationList() `获取 `isLoading` 并传入。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >error</td>

<td rowspan="1" colSpan="1" >`Boolean`</td>

<td rowspan="1" colSpan="1" >`false`</td>

<td rowspan="1" colSpan="1" >会话列表加载错误标识位，在 `<ConversationList>` 中使用时，使用 `useConversationList() `获取 `isLoadError` 并传入。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >PlaceholderEmptyList</td>

<td rowspan="1" colSpan="1" >`ReactNode`</td>

<td rowspan="1" colSpan="1" >`<PlaceHolder type={PlaceHolderTypes.NO_CONVERSATIONS} />`</td>

<td rowspan="1" colSpan="1" >自定义会话列表为空时的占位元素。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >PlaceholderLoading</td>

<td rowspan="1" colSpan="1" >`ReactNode`</td>

<td rowspan="1" colSpan="1" >`<PlaceHolder type={PlaceHolderTypes.LOADING} />`</td>

<td rowspan="1" colSpan="1" >自定义会话列表加载中的占位元素。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >PlaceholderLoadError</td>

<td rowspan="1" colSpan="1" >`ReactNode`</td>

<td rowspan="1" colSpan="1" >`<PlaceHolder type={PlaceHolderTypes.WRONG} />`</td>

<td rowspan="1" colSpan="1" >自定义会话列表加载错误时的占位元素。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >className</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >指定根元素类的 CSS 自定义名称。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >style</td>

<td rowspan="1" colSpan="1" >`React.CSSProperties`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >指定根元素样式的自定义样式。</td>
</tr>
</table>


#### 基础定制

`List` 组件不同状态 UI 效果如下，在 `ConversationList` 内部已处理好每种状态的触发时机。

同时，您可以通过自定义传入 `empty`、`loading`、`error` 来控制组件状态。
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


### 自定义 ConversationPreview

详情请参见 [ConversationPreview](https://write.woa.com/document/157860950620008448) 章节。
``` typescript
<ConversationList ConversationPreview={CustomConversationPreview} />
```

### 自定义 ConversationActions

详情请参见 [ConversationActions](https://write.woa.com/document/157860973841612800) 章节。
``` typescript
  <ConversationList ConversationActions={CustomConversationActions} />
```

### 自定义 ConversationSearch

详情请参见 [ConversationSearch](https://write.woa.com/document/157860965047783424) 章节。
``` typescript
<ConversationList ConversationSearch={CustomConversationSearch} />
```

### 自定义 ConversationCreate
``` typescript
<ConversationList ConversationCreate={CustomConversationCreate} />
```

### 自定义 Avatar
``` typescript
<ConversationList Avatar={CustomAvatar} />
```

## APIs/Props
<table>
<tr>
<td rowspan="1" colSpan="1" >**参数名**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**默认值**</td>

<td rowspan="1" colSpan="1" >**说明**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enableSearch</td>

<td rowspan="1" colSpan="1" >`Boolean`</td>

<td rowspan="1" colSpan="1" >`true`</td>

<td rowspan="1" colSpan="1" >控制会话搜索功能是否显示。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enableCreate</td>

<td rowspan="1" colSpan="1" >`Boolean`</td>

<td rowspan="1" colSpan="1" >`true`</td>

<td rowspan="1" colSpan="1" >控制创建会话功能是否显示。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enableActions</td>

<td rowspan="1" colSpan="1" >`Boolean`</td>

<td rowspan="1" colSpan="1" >`true`</td>

<td rowspan="1" colSpan="1" >控制会话操作功能是否显示。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >actionsConfig</td>

<td rowspan="1" colSpan="1" >`ConversationActionsConfig`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >用于自定义会话操作配置。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Header</td>

<td rowspan="1" colSpan="1" >`ReactElement`</td>

<td rowspan="1" colSpan="1" >`Header`</td>

<td rowspan="1" colSpan="1" >自定义 Header 组件。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >List</td>

<td rowspan="1" colSpan="1" >`ReactElement`</td>

<td rowspan="1" colSpan="1" >`List`</td>

<td rowspan="1" colSpan="1" >自定义会话列表组件。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Preview</td>

<td rowspan="1" colSpan="1" >`ReactElement`</td>

<td rowspan="1" colSpan="1" >[ConversationPreview](https://write.woa.com/document/157860950620008448)</td>

<td rowspan="1" colSpan="1" >自定义会话预览组件。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ConversationCreate</td>

<td rowspan="1" colSpan="1" >`ReactElement`</td>

<td rowspan="1" colSpan="1" >`ConversationCreate`</td>

<td rowspan="1" colSpan="1" >自定义创建会话组件。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ConversationSearch</td>

<td rowspan="1" colSpan="1" >`ReactElement`</td>

<td rowspan="1" colSpan="1" >[ConversationSearch](https://write.woa.com/document/157860965047783424)</td>

<td rowspan="1" colSpan="1" >自定义会话搜索组件。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ConversationActions</td>

<td rowspan="1" colSpan="1" >`ReactElement`</td>

<td rowspan="1" colSpan="1" >[ConversationActions](https://write.woa.com/document/157860973841612800)</td>

<td rowspan="1" colSpan="1" >自定义会话操作组件。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Avatar</td>

<td rowspan="1" colSpan="1" >`ReactElement`</td>

<td rowspan="1" colSpan="1" >`Avatar`</td>

<td rowspan="1" colSpan="1" >自定义头像组件。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >PlaceholderEmptyList</td>

<td rowspan="1" colSpan="1" >`ReactNode`</td>

<td rowspan="1" colSpan="1" >`<PlaceHolder type={PlaceHolderTypes.NO_CONVERSATIONS} />`</td>

<td rowspan="1" colSpan="1" >自定义会话列表为空时的占位元素。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >PlaceholderLoading</td>

<td rowspan="1" colSpan="1" >`ReactNode`</td>

<td rowspan="1" colSpan="1" >`<PlaceHolder type={PlaceHolderTypes.LOADING} />`</td>

<td rowspan="1" colSpan="1" >自定义会话列表加载中的占位元素。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >PlaceholderLoadError</td>

<td rowspan="1" colSpan="1" >`ReactNode`</td>

<td rowspan="1" colSpan="1" >`<PlaceHolder type={PlaceHolderTypes.WRONG} />`</td>

<td rowspan="1" colSpan="1" >自定义会话列表加载错误时的占位元素。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >filter</td>

<td rowspan="1" colSpan="1" >`(conversationList: ConversationModel[]) => ConversationModel[]`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >用于筛选会话列表的函数。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >sort</td>

<td rowspan="1" colSpan="1" >`(conversationList: ConversationModel[]) => ConversationModel[]`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >用于排序会话列表的函数。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onConversationSelect</td>

<td rowspan="1" colSpan="1" >`(conversation: ConversationModel) => void;`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >点击会话后的回调函数，参数为所点击的会话对象。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onBeforeCreateConversation</td>

<td rowspan="1" colSpan="1" >`(params: CreateParams) => CreateParams;`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >创建会话前执行的自定义操作，参数为创建会话所需的参数。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onConversationCreate</td>

<td rowspan="1" colSpan="1" >`(conversation: ConversationModel)  => void;`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >会话创建后的回调函数，参数为创建的会话对象。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >className</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >指定根元素类的 CSS 自定义名称。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >style</td>

<td rowspan="1" colSpan="1" >`React.CSSProperties`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >指定根元素样式的自定义样式。</td>
</tr>
</table>
