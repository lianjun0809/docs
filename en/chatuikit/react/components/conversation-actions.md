> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

`ConversationActions` component is responsible for row operations on a single session, supported by default with delete conversation, pin conversation to top/unpin, and mute/unmute features.

## Basic Usage

When using `ConversationActions` in `ConversationList`, you can customize it directly through the top-level `actionsConfig` parameter of `ConversationList`. `actionsConfig` supports default conversation operation feature toggles, event response, adding new custom action items, and basic UI customization.

For advanced customization, you can create new components through `ConversationActions`.

### Using ActionsConfig Basic Customization
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

### Custom ConversationActions Component
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

`ConversationActions` component API type `ConversationActionsProps` is based on `ConversationActionsConfig` API and expanded. 
<table>
<tr>
<td rowspan="1" colSpan="4" >

##### **ConversationActionsProps**</td>


##### 

##### 

##### </tr>

<tr>
<td rowspan="1" colSpan="1" >**Parameter Name**</td>

<td rowspan="1" colSpan="1" >**Type**</td>

<td rowspan="1" colSpan="1" >**Default Value**</td>

<td rowspan="1" colSpan="1" >**Note**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**conversation*****(Required)***</td>

<td rowspan="1" colSpan="1" >ConversationModel</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >This parameter is required and represents the session for the current rendered conversation operation.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >className</td>

<td rowspan="1" colSpan="1" >String </td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Custom root element class name.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >style</td>

<td rowspan="1" colSpan="1" >React.CSSProperties</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Custom root element style.</td>
</tr>

<tr>
<td rowspan="1" colSpan="4" >

##### ConversationActionsConfig</td>


##### 

##### 

##### </tr>

<tr>
<td rowspan="1" colSpan="1" >**Parameter Name**</td>

<td rowspan="1" colSpan="1" >**Type**</td>

<td rowspan="1" colSpan="1" >**Default Value**</td>

<td rowspan="1" colSpan="1" >**Note**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enablePin</td>

<td rowspan="1" colSpan="1" >Boolean</td>

<td rowspan="1" colSpan="1" >true</td>

<td rowspan="1" colSpan="1" >Whether to display the pin to top feature button.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enableMute</td>

<td rowspan="1" colSpan="1" >Boolean</td>

<td rowspan="1" colSpan="1" >true</td>

<td rowspan="1" colSpan="1" >Whether to display the do not disturb feature button.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enableDelete</td>

<td rowspan="1" colSpan="1" >Boolean</td>

<td rowspan="1" colSpan="1" >true</td>

<td rowspan="1" colSpan="1" >Whether to display the deletion feature button.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onConversationPin</td>

<td rowspan="1" colSpan="1" >(conversation: ConversationModel, e?: React.MouseEvent) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Customize the behavior of pinning/unpinning conversations.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onConversationMute</td>

<td rowspan="1" colSpan="1" >(conversation: ConversationModel, e?: React.MouseEvent)<br>=> void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Customize the behavior of do not disturb/cancel Do Not Disturb session.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onConversationDelete</td>

<td rowspan="1" colSpan="1" >(conversation: ConversationModel, e?: React.MouseEvent) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Customize the behavior of deleting conversations.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >customConversationActions</td>

<td rowspan="1" colSpan="1" >Record<string, [ConversationActionItem](https://write.woa.com/#96079c71-233e-442e-96ef-ba91fbd5e201)></td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Custom session operation items.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >PopupIcon</td>

<td rowspan="1" colSpan="1" >ReactElement</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Custom action pop-up icon.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >PopupElements</td>

<td rowspan="1" colSpan="1" >ReactElement[]</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Content of the custom action popup.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onClick</td>

<td rowspan="1" colSpan="1" >(e: React.MouseEvent, key?: string, conversation?: ConversationModel) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Callback function for click action.</td>
</tr>
</table>


## Customize Component

### Basic Feature Switch

By setting the `enablePin`, `enableDelete`, and `enableMute` parameters, you can flexibly control the display of conversation pinning, mute message notification, and conversation deletion in `ConversationActions`.
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
<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/e7be41055e2f11f091585254001c06ec.png)</td>

<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/e7baa5d75e2f11f0b324525400e889b2.png)</td>

<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/e7be68215e2f11f091585254001c06ec.png)</td>
</tr>
</table>


### Event Response

`ConversationActions` component supports delete conversation, pin conversation to top/unpin, and mute/unmute features by default. If the event response of existing functionality does not meet your needs, you can customize the event response handling function and override it. In addition to customizing feature event responses, you can also obtain basic click event response through onClick.
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

`customConversationActions` is used to add new custom action items to the ConversationActions list.
<table>
<tr>
<td rowspan="1" colSpan="4" >

##### ConversationActionItem</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**Parameter Name**</td>

<td rowspan="1" colSpan="1" >**Type**</td>

<td rowspan="1" colSpan="1" >**Default Value**</td>

<td rowspan="1" colSpan="1" >**Note**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enable</td>

<td rowspan="1" colSpan="1" >Boolean</td>

<td rowspan="1" colSpan="1" >true</td>

<td rowspan="1" colSpan="1" >Whether to enable custom action items.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >label</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Display content of custom action items.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onClick</td>

<td rowspan="1" colSpan="1" >(conversation: ConversationModel, e?: React.MouseEvent) => void</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Callback function for clicking a custom action item.</td>
</tr>
</table>


Here is an example of adding new custom action items using `customConversationActions`:
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
<td rowspan="1" colSpan="1" >**Before modification**</td>

<td rowspan="1" colSpan="1" >**After modification**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/e7c05dbf5e2f11f097ec52540044a08e.png)</td>

<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/e7c27bfd5e2f11f097ec52540044a08e.png)</td>
</tr>
</table>


### UI Interface Customization

You can customize the wakeup popup button style through the `PopupIcon` parameter and the popup content through `PopupElements`.

The following is example code for secondary development on the basis of the default `ConversationActions` component to customize a new awakening button style:
``` typescript
import { ConversationList, ConversationActions, ConversationActionsProps } from '@tencentcloud/chat-uikit-react';
import type { ConversationActionsProps } from '@tencentcloud/chat-uikit-react';

const CustomConversationActions = (props: ConversationActionsProps) => {
  const customIcon = <div>Custom Icon</div>
  return (
    <ConversationActions {...props} PopupIcon={customIcon} />
  );
};
     
<ConversationList ConversationActions={CustomConversationActions} />
```
<table>
<tr>
<td rowspan="1" colSpan="1" >**Before modification**</td>

<td rowspan="1" colSpan="1" >**After modification**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/e7bc736e5e2f11f092fe525400bf7822.png)</td>

<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/e7cccf8a5e2f11f0b30d5254007c27c5.png)</td>
</tr>
</table>
