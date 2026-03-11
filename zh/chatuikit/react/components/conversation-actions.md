> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

`ConversationActions` 组件负责对于单条会话进行操作，默认支持会话删除、会话置顶/取消置顶、会话免打扰/取消免打扰功能。

## 基础使用

当在 `ConversationList` 使用 `ConversationActions` 时，您可以通过 `ConversationList` 顶层 `actionsConfig` 参数直接进行自定义，`actionsConfig` 支持对于默认会话操作功能开关、事件响应、新增自定义操作项、基础 UI 定制等。

如您需要更高阶的定制，您可以通过 `ConversationActions` 自定义新的组件。

### 使用 actionsConfig 基础定制
``` typescript
import { UIKitProvider, ConversationList } from "@tencentcloud/chat-uikit-react";
import type { ConversationModel } from "@tencentcloud/chat-uikit-react";

const App = () => {
  return (
    <UIKitProvider>
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
      }}/>
    </UIKitProvider>
  );
}
```

### 自定义 ConversationActions 组件
``` typescript
import { UIKitProvider, ConversationList, ConversationActions } from "@tencentcloud/chat-uikit-react";
import type { ConversationActionsProps } from '@tencentcloud/chat-uikit-react';

const CustomConversationActions = (props: ConversationActionsProps) => {
  return <ConversationActions {...props} enableDelete={false} />;
};

const App = () => {
  return (
    <UIKitProvider>
      <ConversationList
        style={{ maxWidth: '300px', height: '600px' }}
        ConversationActions={CustomConversationActions}
      />
    </UIKitProvider>
  );
}
```

## Props

`ConversationActions` 组件的接口类型 `ConversationActionsProps` 基于 `ConversationActionsConfig` 接口进行扩展。 
<table>
<tr>
<td rowspan="1" colSpan="4" >

##### **IConversationActionsProps**</td>


##### 

##### 

##### </tr>

<tr>
<td rowspan="1" colSpan="1" >**参数名**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**默认值**</td>

<td rowspan="1" colSpan="1" >**说明**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**conversation*****(Required)***</td>

<td rowspan="1" colSpan="1" >`ConversationModel`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >必选参数，表示当前渲染会话操作对应的会话。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >className</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >自定义根元素的类名。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >style</td>

<td rowspan="1" colSpan="1" >`React.CSSProperties`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >自定义根元素的样式。</td>
</tr>

<tr>
<td rowspan="1" colSpan="4" >

##### IConversationActionsConfig</td>


##### 

##### 

##### </tr>

<tr>
<td rowspan="1" colSpan="1" >**参数名**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**默认值**</td>

<td rowspan="1" colSpan="1" >**说明**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enablePin</td>

<td rowspan="1" colSpan="1" >`Boolean`</td>

<td rowspan="1" colSpan="1" >`true`</td>

<td rowspan="1" colSpan="1" >是否显示置顶功能按钮。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enableMute</td>

<td rowspan="1" colSpan="1" >`Boolean`</td>

<td rowspan="1" colSpan="1" >`true`</td>

<td rowspan="1" colSpan="1" >是否显示免打扰功能按钮。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enableDelete</td>

<td rowspan="1" colSpan="1" >`Boolean`</td>

<td rowspan="1" colSpan="1" >`true`</td>

<td rowspan="1" colSpan="1" >是否显示删除功能按钮。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onConversationPin</td>

<td rowspan="1" colSpan="1" >`(conversation: ConversationModel, e?: React.MouseEvent) => void`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >自定义置顶/取消置顶会话的行为。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onConversationMute</td>

<td rowspan="1" colSpan="1" >`(conversation: ConversationModel, e?: React.MouseEvent)`<br>`=> void`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >自定义免打扰/取消免打扰会话的行为。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onConversationDelete</td>

<td rowspan="1" colSpan="1" >`(conversation: ConversationModel, e?: React.MouseEvent) => void`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >自定义删除会话的行为。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >customConversationActions</td>

<td rowspan="1" colSpan="1" >`Record<string, `[`ConversationActionItem`](https://write.woa.com/document/157860973841612800)`>`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >自定义会话操作项。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >PopupIcon</td>

<td rowspan="1" colSpan="1" >`ReactElement`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >自定义动作弹窗的图标。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >PopupElements</td>

<td rowspan="1" colSpan="1" >`ReactElement[]`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >自定义动作弹窗的内容。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onClick</td>

<td rowspan="1" colSpan="1" >`(e: React.MouseEvent, key?: string, conversation?: ConversationModel) => void`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >点击动作项时的回调函数。</td>
</tr>
</table>


## 自定义组件

### 基础功能开关

通过设置 `enablePin`, `enableDelete` 和 `enableMute` 参数，您可以灵活地控制 `ConversationActions` 中的会话置顶、会话免打扰和会话删除的显示。
``` typescript
<ConversationActions enablePin={false} />
```
``` typescript
<ConversationActions enableDelete={false} />
```
``` typescript
<ConversationActions enableMute={false} />
```
<table>
<tr>
<td rowspan="1" colSpan="1" >`enablePin={false}`</td>

<td rowspan="1" colSpan="1" >`enableDelete={false}`</td>

<td rowspan="1" colSpan="1" >`enableMute={false} `</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027119864/adaf4f4c7b4211efa87e52540055f650.png)</td>

<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027119864/d05321b37b4211ef82535254002693fd.png)</td>

<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027119864/e45d60e87b4211ef8829525400fdb830.png)</td>
</tr>
</table>


### 事件响应

`ConversationActions` 组件默认支持会话删除、会话置顶/取消置顶、会话免打扰/取消免打扰功能，如已有功能的事件响应不符合您的需求，您可以自定义事件响应处理函数并进行覆盖; 除了支持对于功能事件响应的自定义外，您还可以通过 onClick 获取基础点击事件响应。
``` typescript
import { ConversationList, ConversationActions, Toast } from '@tencentcloud/chat-uikit-react';
import type { ConversationActionsProps, ConversationModel } from '@tencentcloud/chat-uikit-react';

const CustomConversationActions = (props: ConversationActionsProps) => {
  return (
    <ConversationActions
      {...props}
      onConversationDelete={(conversation: ConversationModel) => {
        conversation.deleteConversation().then(() => {
          Toast({ text: 'delete conversation successfully!', type: 'info' });
        }).catch(() => {
          Toast({ text: 'delete conversation failed!', type: 'error' });
        });
      }}
    />
  );
};

<ConversationList ConversationActions={CustomConversationActions} />
```

### customConversationActions

`customConversationActions` 用于在 ConversationActions 上新增自定义操作项列表。
<table>
<tr>
<td rowspan="1" colSpan="4" >

##### ConversationActionItem</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**参数名**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**默认值**</td>

<td rowspan="1" colSpan="1" >**说明**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enable</td>

<td rowspan="1" colSpan="1" >`Boolean`</td>

<td rowspan="1" colSpan="1" >`true`</td>

<td rowspan="1" colSpan="1" >是否启用自定义操作项。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >label</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >自定义操作项的展示内容。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onClick</td>

<td rowspan="1" colSpan="1" >`(conversation: ConversationModel, e?: React.MouseEvent) => void`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >点击自定义操作项时的回调函数。</td>
</tr>
</table>


以下是使用 `customConversationActions` 新增自定义操作项的示例：
``` typescript
import { ConversationList, ConversationActions } from '@tencentcloud/chat-uikit-react';
import type { ConversationActionsProps, ConversationModel } from '@tencentcloud/chat-uikit-react';

const CustomConversationActions = (props: ConversationActionsProps) => {
  return (
    <ConversationActions 
      {...props} 
      customConversationActions={{
        'custom-actions-1': {
           label: 'custom-actions',
           onClick: (conversation: ConversationModel) => { console.log(conversation); },
         },
      }}
    />
  );
};
     
<ConversationList ConversationActions={CustomConversationActions} />
```
<table>
<tr>
<td rowspan="1" colSpan="1" >**修改前**</td>

<td rowspan="1" colSpan="1" >**修改后**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027119864/3e78ddb27c0d11ef8631525400a9236a.png)</td>

<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027119864/47348c867c0d11ef852f52540075b605.png)</td>
</tr>
</table>


### UI 界面定制

您可以通过 `PopupIcon` 参数定制唤醒弹出按钮样式，通过 `PopupElements` 定制弹出内容。

以下是在默认的 `ConversationActions` 组件的基础上进行二次开发，为其定制新的唤起按钮样式代码示例：
``` typescript
import { ConversationList, ConversationActions, ConversationActionsProps } from '@tencentcloud/chat-uikit-react';
import type { ConversationActionsProps } from '@tencentcloud/chat-uikit-react';

const CustomConversationActions = (props: ConversationActionsProps) => {
  const customIcon = <div> 自定义 Icon </div>
  return (
    <ConversationActions {...props} PopupIcon={customIcon} />
  );
};
     
<ConversationList ConversationActions={CustomConversationActions} />
```
<table>
<tr>
<td rowspan="1" colSpan="1" >**修改前**</td>

<td rowspan="1" colSpan="1" >**修改后**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027119864/8df495ac7c0d11ef82535254002693fd.png)</td>

<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027119864/778e580f7c0d11ef80ff525400d5f8ef.png)</td>
</tr>
</table>
