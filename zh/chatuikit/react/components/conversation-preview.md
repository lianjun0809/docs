> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

`ConversationPreview` 用于对于会话列表中单条会话内容进行预览，组件负责显示会话信息、未读计数以及提供会话操作功能。

借助原子化的信息展示组件，您可以自由地设计和组合出您所期望的 `ConversationPreview` 布局。

同时，您还可以通过 `onConversationSelect` 函数来自定义选中会话时的行为。

### 基础使用

您可以使用 `ConversationList` 的 `Preview` 属性来自定义会话列表中每个单独会话的预览项，如果没有指定 `Preview` 属性，系统将自动采用 `ConversationPreviewUI` 组件作为默认值。
``` typescript
import { ConversationList, ConversationPreviewUI } from '@tencentcloud/chat-uikit-react';
import type { ConversationPreviewUIProps } from '@tencentcloud/chat-uikit-react';

const CustomConversationPreview = (props: ConversationPreviewUIProps) => {
  const { Title } = props;
  return (
    <ConversationPreviewUI {...props}>
      {Title}
      <div>Your custom preview UI</div>
    </ConversationPreviewUI>
  );
};

<ConversationList Preview={CustomConversationPreviewUI}></ConversationList>
```

### Props
<table>
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

<td rowspan="1" colSpan="1" >必选参数，标识当前渲染的会话列表项。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >isSelected</td>

<td rowspan="1" colSpan="1" >`Boolean`</td>

<td rowspan="1" colSpan="1" >`false`</td>

<td rowspan="1" colSpan="1" >控制会话列表项 UI 是否处于选中状态。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enableActions</td>

<td rowspan="1" colSpan="1" >`Boolean`</td>

<td rowspan="1" colSpan="1" >`true`</td>

<td rowspan="1" colSpan="1" >控制会话操作功能是否显示。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >actionsConfig</td>

<td rowspan="1" colSpan="1" >[ConversationActionsConfig](https://write.woa.com/document/157860973841612800)</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >用于自定义会话操作配置。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >highlightMatchString</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >会话列表项 Title 高亮匹配关键词，常用于会话搜索结果高亮。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Title</td>

<td rowspan="1" colSpan="1" >`String \| JSX.Element`</td>

<td rowspan="1" colSpan="1" >`ConversationPreviewTitle`</td>

<td rowspan="1" colSpan="1" >渲染会话列表项标题区域。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >LastMessageAbstract</td>

<td rowspan="1" colSpan="1" >`String \| JSX.Element`</td>

<td rowspan="1" colSpan="1" >`ConversationPreviewAbstract`</td>

<td rowspan="1" colSpan="1" >渲染会话列表项最新消息摘要区域。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >LastMessageTimestamp</td>

<td rowspan="1" colSpan="1" >`String \| JSX.Element`</td>

<td rowspan="1" colSpan="1" >`ConversationPreviewTimestamp`</td>

<td rowspan="1" colSpan="1" >渲染会话列表项最新消息时间戳区域。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Unread</td>

<td rowspan="1" colSpan="1" >`String \| JSX.Element`</td>

<td rowspan="1" colSpan="1" >`ConversationPreviewUnread`</td>

<td rowspan="1" colSpan="1" >渲染会话列表项消息未读标识区域。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ConversationActions</td>

<td rowspan="1" colSpan="1" >`ReactElement`</td>

<td rowspan="1" colSpan="1" >`ConversationActions`</td>

<td rowspan="1" colSpan="1" >渲染会话列表项会话操作区域。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Avatar</td>

<td rowspan="1" colSpan="1" >`ReactElement`</td>

<td rowspan="1" colSpan="1" >`Avatar`</td>

<td rowspan="1" colSpan="1" >渲染会话列表项头像区域。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onConversationSelect</td>

<td rowspan="1" colSpan="1" >`(conversation: ConversationModel) => void;`</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >指定在选择对话列表中的对话时接收回调的属性。</td>
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


## 自定义案例

### 类 Discord 风格

Discord 是一个流行的聊天应用程序，类似于 Skype 或 Telegram。Discord 中的聊天内容如下图所示:

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027119864/6b0366e57b0b11ef8631525400a9236a.png)


通过对 `ConversationPreview` 布局、功能以及样式的定制，我们可以快速实现类 Discord 效果。



【React】
1. 定制 `ConversationListPreview`

2. 切换主题到深色模式

``` typescript
import { UIKitProvider, ConversationList, ConversationPreviewUI } from '@tencentcloud/chat-uikit-react';
import type { ConversationPreviewUIProps } from '@tencentcloud/chat-uikit-react';

const CustomConversationPreview = (props: ConversationPreviewUIProps) => {
  const { Title } = props;
  return (
    <ConversationPreviewUI {...props}>
      <span> # </span>
      <span>{Title}</span>
    </ConversationPreviewUI>
  );
};

const App = () => {
    <UIKitProvider theme={'dark'}>
      <ConversationList 
        style={{ maxWidth: '300px', height: '600px' }} 
        Preview={CustomConversationPreviewUI}
       />
      ...
    </UIKitProvider>
}
```

【CSS】
``` scss
.custom-preview-ui {
  height: 34px;
  border-radius: 6px;
  padding: 10px;
  margin: 0 10px;
  .custom-preview-ui__tag {
    margin-right: 10px;
    font-size: 16px;
    color: #b3b3b4;
  }
  .custom-preview-ui__title {
    font-size: 14px;
    color: #b3b3b4;
  }
  &.uikit-conversation-preview--active {
    background-color: #3b3d43;
    .custom-preview-ui__tag {
      color: #ffffff;
    }
    .custom-preview-ui__title {
      .uikit-conversation-preview__title {
        color: #ffffff;
      }
    }
  }
}
```

`ConversationListPreview` 定制后效果如下：
<table>
<tr>
<td rowspan="1" colSpan="1" >**修改前**</td>

<td rowspan="1" colSpan="1" >**修改后**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027119864/e044ab307b1911ef82535254002693fd.png)</td>

<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027119864/623e99317b1911ef82535254002693fd.png)</td>
</tr>
</table>
