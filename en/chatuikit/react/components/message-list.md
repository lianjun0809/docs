> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/en/llms.txt
> Use this file to discover all available pages before exploring further.

# Component Overview

MessageList is a powerful chat message list component with complete message display, interaction, and custom function. The component support includes message grouping, read receipt, message manipulation, scroll control, and other core chat features, while providing various custom options to satisfy different business needs.


## Props Configuration
<table>
<tr>
<td rowspan="1" colSpan="1">Field</td>


<td rowspan="1" colSpan="1">Type</td>


<td rowspan="1" colSpan="1">Default Value</td>


<td rowspan="1" colSpan="1">Description</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[alignment](https://write.woa.com/document/181344255270170624)</td>


<td rowspan="1" colSpan="1" >'left' \| 'right' \| 'two-sided'</td>


<td rowspan="1" colSpan="1" >'two-sided'</td>


<td rowspan="1" colSpan="1">Message alignment mode.<br>- left: Align all messages to the left.<br>- right: Align all messages to the right.<br>- two-sided: Right-align sent messages and left-align received messages.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[enableReadReceipt](https://write.woa.com/document/181344255270170624)</td>


<td rowspan="1" colSpan="1" >boolean</td>


<td rowspan="1" colSpan="1" >false</td>


<td rowspan="1" colSpan="1">Whether to enable the read receipt feature.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[messageActionList](https://write.woa.com/document/181344255270170624)</td>


<td rowspan="1" colSpan="1" >IMessageAction[]</td>


<td rowspan="1" colSpan="1" >undefined</td>


<td rowspan="1" colSpan="1">Custom message operation list, such as copy, revoke, delete.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[messageAggregationTime](https://write.woa.com/document/181344255270170624)</td>


<td rowspan="1" colSpan="1" >number</td>


<td rowspan="1" colSpan="1">300 (5 minutes)</td>


<td rowspan="1" colSpan="1">Message aggregation interval (seconds). Consecutive messages from the same sender within this period will be aggregated and displayed.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[filter](https://write.woa.com/document/181344255270170624)</td>


<td rowspan="1" colSpan="1" >(message: IMessageModel) => boolean</td>


<td rowspan="1" colSpan="1" >undefined</td>


<td rowspan="1" colSpan="1">Message filtering function, used to control which messages to display.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[className](https://write.woa.com/document/181344255270170624)</td>


<td rowspan="1" colSpan="1" >string</td>


<td rowspan="1" colSpan="1" >undefined</td>


<td rowspan="1" colSpan="1">Custom CSS class name.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[style](https://write.woa.com/document/181344255270170624)</td>


<td rowspan="1" colSpan="1" >React.CSSProperties</td>


<td rowspan="1" colSpan="1" >undefined</td>


<td rowspan="1" colSpan="1">Custom inline style.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[Message](https://write.woa.com/document/181344255270170624)</td>


<td rowspan="1" colSpan="1" >React.ComponentType</td>


<td rowspan="1" colSpan="1" >Message</td>


<td rowspan="1" colSpan="1">Custom message component.</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[MessageTimeDivider](https://write.woa.com/document/181344255270170624)</td>


<td rowspan="1" colSpan="1" >React.ComponentType</td>


<td rowspan="1" colSpan="1" >MessageTimeDivider</td>


<td rowspan="1" colSpan="1">Custom time dividing line component.</td>
</tr>
</table>




## Prop field explanation


### alignment


Parameter type: `'left' | 'right' | 'two-sided'`


alignment is used to set the message alignment mode, supporting three modes: `left`, `right`, and `two-sided`. Default value is `'two-sided'`.
- `two-sided`: Non-person messages are on the left, my messages are on the right


- `left`: All messages are on the left


- `right`: All messages are on the right




### enableReadReceipt


Parameter type: `boolean`


enableReadReceipt is used to set whether the message read receipt feature is enabled. Default value: `false`.


### messageActionList


Parameter type: `IMessageAction[]`


The messageActionList is used to set the actions list of messages, such as copy, recall, and delete. The default value is the complete message operation list `['copy', 'recall', 'quote', 'forward', 'delete']`.
``` tsx
interface IMessageAction {
  key: 'copy' | 'recall' | 'quote' | 'forward' | 'delete' | string;
  label?: string;
  icon?: React.ReactNode;
  onClick?: (message: IMessageModel) => void;
  visible?: ((message: IMessageModel) => boolean) | boolean;
  component?: React.ComponentType<{ message: IMessageModel }>;
  style?: React.CSSProperties;
}
```


Use `useMessageAction` to obtain the complete message operation list, then customize as needed.


#### Example 1: Change the order of the action list


Assuming the message actions list is displayed in the order: `forward`, `copy`, `recall`, `quote`, `delete`.
``` tsx
import { Chat, MessageList, useMessageActions } from '@tencentcloud/chat-uikit-react';


const App = () => {
  const actions = useMessageActions(['forward', 'copy', 'recall', 'quote', 'delete']);
  return (
    <Chat>
      <MessageList messageActionList={actions} />
    </Chat>
  );
}
```


#### Example 2: Only show some message actions


Only show `forward`, `copy`, `recall` operations.
``` tsx
import { Chat, MessageList, useMessageActions } from '@tencentcloud/chat-uikit-react';


const App = () => {
  const actions = useMessageActions(['forward', 'copy', 'recall']);
  return (
    <Chat>
      <MessageList messageActionList={actions} />
    </Chat>
  );
}


```


#### Example 3: Customize the style of message actions


Here is an example of a custom recall operation:
1. Change the tag to 'recall ⚠️'


2. Change the color to orange


3. Only text messages can be withdrawn


   ``` tsx
   import TUIChatEngine from '@tencentcloud/chat-uikit-engine';
   import { Chat, MessageList, useMessageActions } from '@tencentcloud/chat-uikit-react';
   
   const ChatApp = () => {
     const actions = useMessageActions(['copy', {
       key: 'recall',
       label: 'Recall ⚠️',
       style: {
         color: 'orange'
       },
       visible: (message) => message.type === TUIChatEngine.TYPES.MSG_TEXT,
     }, 'quote', 'forward', 'delete']);
   
     return (
       <Chat>
         <MessageList messageActionList={actions} />
       </Chat>
     );
   }
   ```


#### Example 4: Add new custom message actions


Assuming custom message actions are required, for example, only messages sent by others can be tagged as 'like' and inserted after the 'recall' operation.
``` tsx
import { useMessageAction } from '@tencentcloud/chat-uikit-react';
import { yourApi } from '@/api/yourApi';


const customActions = {
  key: 'like',
  label: 'Like',
  icon: <span>👍</span>,
  style: {
    color: '#E53888',
  },
  visible: (message) => message.flow === 'in',
  onClick: (message) => {
    yourApi.likeMessage(message.ID);
  }
}


function ChatApp() {
  const actions = useMessageAction(['forward', 'copy', 'recall', customActions, 'quote', 'delete']);
  return <MessageList messageActionList={actions} />;
}
```


### messageAggregationTime


Parameter type: `number`


messageAggregationTime is used to set the message aggregation interval. Consecutive messages from the same sender will be aggregated and displayed. Default value: `300` (seconds).


### filter


Parameter type: `(message: IMessageModel) => boolean`


filter is used to set the message filtering function to control which messages to display. Default value: `undefined`.


#### Example: Filter out error messages sent by robots
``` tsx
import { MessageList } from '@/components/MessageList';
import TUIChatEngine from '@tencentcloud/chat-uikit-engine';


const messageFilter = (message) => {
  // Filter out text messages where sender nickname contains '_robot' and content contains 'operation-failed'
  if (
    message.nick?.includes('_robot') 
    && message.type === TUIChatEngine.TYPES.MSG_TEXT
    && message.payload?.text?.includes('operation-failed')
  ) {
    return false;
  }
  return true;
};


function ChatApp() {
  return <MessageList filter={messageFilter} />;
}
```


### className


Parameter type: `string`


className is used to set the root container's custom CSS class name. Default value: `undefined`.


### style


Parameter type: `React.CSSProperties`


style is used to set the root container's custom inline style. Default value: `undefined`.


### Message


Parameter type: `React.ComponentType`


Message is used to set the custom message component, replacing the default message rendering component. Default value: built-in `Message` component.


#### Example: Custom CUSTOM message click redirection component of messages
``` tsx
import TUIChatEngine from '@tencentcloud/chat-uikit-engine';
import { Chat, MessageList, Message } from '@tencentcloud/chat-uikit-react';


function CustomMessage(props) {
  const { message } = props;


  if (message.type === TUIChatEngine.TYPES.MSG_CUSTOM) {
    const { businessID, ...restData } = JSON.parse(message.payload.data);
    if (businessID === 'text_link') {
      return (
        <div>
          <div>{restData.text}</div>
          <a href={restData.link}>
            Redirect to external website address {restData.link}
          </a>
        </div>
      );
    }
  } else {
    Other message types use the default message component
    return <Message {...props} />;
  }
}


function ChatApp() {
  return (
    <Chat>
      <MessageList Message={CustomMessage} />
    </Chat>
  );
}
```


### MessageTimeDivider


Parameter type: `React.ComponentType`


MessageTimeDivider is used to set the custom time dividing line component. Default value: built-in `MessageTimeDivider` component.


#### Example: Case-sensitive working hour dividing line
``` tsx
import { Chat, MessageList, MessageTimeDivider } from '@tencentcloud/chat-uikit-react';


const BusinessTimeDivider: typeof MessageTimeDivider = ({ prevMessage, currentMessage }) => {
  if (!prevMessage || !currentMessage) return null;
  
  For each message to be rendered, get the current and previous message time, convert them to date objects, and determine whether they cross days or exceed a 4-hour interval.
  const currentTime = new Date(currentMessage.time * 1000);
  const prevTime = new Date(prevMessage.time * 1000);
  
  // Display only when crossing days or the interval exceeds 4 hours
  const shouldShow = currentTime.toDateString() !== prevTime.toDateString() ||
                    (currentTime.getTime() - prevTime.getTime()) > 4 * 60 * 60 * 1000;
  
  if (!shouldShow) return null;
  
  Check working hours (9:00-18:00, Monday through Friday)
  const isWorkingTime = () => {
    const hour = currentTime.getHours();
    const day = currentTime.getDay();
    return day >= 1 && day <= 5 && hour >= 9 && hour <= 18;
  };
  
  const timeLabel = isWorkingTime() ? 'working hour' : 'off hours';
  const timeColor = isWorkingTime() ? '#52c41a' : '#faad14';
  
  return (
    <div style={{ textAlign: 'center', margin: '16px 0' }}>
      <span style={{
        backgroundColor: timeColor,
        color: 'white',
        padding: '2px 8px',
        borderRadius: '12px',
        marginRight: '8px'
      }}>
        {timeLabel}
      </span>
      {currentTime.toLocaleString()}
    </div>
  );
};


function ChatApp() {
  return (
    <Chat>
      <MessageList MessageTimeDivider={BusinessTimeDivider} />
    </Chat>
  );
}
```


## Summary

The MessageList component provides complete message list functionality and various custom options. By reasonably configuring Props and custom components, you can create a chat interface that meets business requirements. It is advisable to select appropriate configuration based on specific scenarios in actual use.
