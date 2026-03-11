> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

`ConversationPreview` is used for previewing session content in the list. The component displays session information, unread count, and provides conversation action feature.

With the aid of atomic information display components, you can freely design and combine your desired `ConversationPreview` layout.

Meanwhile, you can also use the `onConversationSelect` function to define selected session behavior.

### Basic Usage

You can use the `Preview` property of `ConversationList` to customize the preview item for each individual conversation in the list. If the `Preview` property is not specified, the system will automatically adopt the `ConversationPreviewUI` component as the default value.
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
<td rowspan="1" colSpan="1" >**Parameter Name**</td>

<td rowspan="1" colSpan="1" >**Type**</td>

<td rowspan="1" colSpan="1" >**Default Value**</td>

<td rowspan="1" colSpan="1" >**Description**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**conversation*****(Required)***</td>

<td rowspan="1" colSpan="1" >ConversationModel</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Required parameter to indicate the currently rendered conversation list item.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >isSelected</td>

<td rowspan="1" colSpan="1" >Boolean</td>

<td rowspan="1" colSpan="1" >false</td>

<td rowspan="1" colSpan="1" >Control if the conversation list item UI is in selected status.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enableActions</td>

<td rowspan="1" colSpan="1" >Boolean</td>

<td rowspan="1" colSpan="1" >true</td>

<td rowspan="1" colSpan="1" >Control whether to display the conversation operation feature.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >actionsConfig</td>

<td rowspan="1" colSpan="1" >[ConversationActionsConfig](https://write.woa.com/document/155521386852253696)</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >For custom session operation configuration.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >highlightMatchString</td>

<td rowspan="1" colSpan="1" >String </td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Conversation list item Title highlights matching keywords, commonly used for Conversation Search results.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Title</td>

<td rowspan="1" colSpan="1" >`String ｜ JSX.Element`</td>

<td rowspan="1" colSpan="1" >ConversationPreviewTitle</td>

<td rowspan="1" colSpan="1" >Render the title area of the conversation list item.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >LastMessageAbstract</td>

<td rowspan="1" colSpan="1" >`String ｜ JSX.Element`</td>

<td rowspan="1" colSpan="1" >ConversationPreviewAbstract</td>

<td rowspan="1" colSpan="1" >Render the latest message abstract area of the conversation list item.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >LastMessageTimestamp</td>

<td rowspan="1" colSpan="1" >`String ｜ JSX.Element`</td>

<td rowspan="1" colSpan="1" >ConversationPreviewTimestamp</td>

<td rowspan="1" colSpan="1" >Render the latest message timestamp area of the conversation list item.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Unread</td>

<td rowspan="1" colSpan="1" >`String ｜ JSX.Element`</td>

<td rowspan="1" colSpan="1" >ConversationPreviewUnread</td>

<td rowspan="1" colSpan="1" >Render the unread indicator area of the conversation list item.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ConversationActions</td>

<td rowspan="1" colSpan="1" >`ReactElement`</td>

<td rowspan="1" colSpan="1" >ConversationActions</td>

<td rowspan="1" colSpan="1" >Render the conversation operations area of the conversation list item.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Avatar</td>

<td rowspan="1" colSpan="1" >ReactElement</td>

<td rowspan="1" colSpan="1" >Avatar</td>

<td rowspan="1" colSpan="1" >Render the avatar area of the conversation list item.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onConversationSelect</td>

<td rowspan="1" colSpan="1" >(conversation: ConversationModel) => void;</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Specify the attributes of receiving callback when selecting a dialogue in the conversation list.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >className</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Set a custom name for the root element class in CSS.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >style</td>

<td rowspan="1" colSpan="1" >React.CSSProperties</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Set custom styles for the root element.</td>
</tr>
</table>


## Custom Case

### Discord-Like Style

Discord is a popular chat application, similar to Skype or Telegram. The message content in Discord is as shown below:

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/656b6c8c5e3011f0b30d5254007c27c5.png)


By customizing the `ConversationPreview` layout, features, and style, we can quickly achieve a Discord-like effect.



【React】
1. Customize the `ConversationListPreview`

2. Switch theme to dark mode

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

`ConversationListPreview` effect as follows after customization:
<table>
<tr>
<td rowspan="1" colSpan="1" >**Before Modification**</td>

<td rowspan="1" colSpan="1" >**Modified**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/6545c5575e3011f091585254001c06ec.png)</td>

<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/6544f8a25e3011f0bac1525400454e06.png)</td>
</tr>
</table>


### 
