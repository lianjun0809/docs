> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

## 组件概述

MessageList 是一个功能强大的聊天消息列表组件，提供了完整的消息展示、交互和自定义功能。该组件支持消息分组、已读回执、消息操作、滚动控制等核心聊天功能，同时提供了丰富的自定义选项来满足不同的业务需求。

## Props 配置
<table>
<tr>
<td rowspan="1" colSpan="1" >字段</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >默认值</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[alignment](https://write.woa.com/document/181344255270170624)</td>

<td rowspan="1" colSpan="1" >'left' \| 'right' \| 'two-sided'</td>

<td rowspan="1" colSpan="1" >'two-sided'</td>

<td rowspan="1" colSpan="1" >消息对齐方式。<br>- left: 所有消息左对齐。<br>- right: 所有消息右对齐。<br>- two-sided: 发送消息右对齐，接收消息左对齐。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[enableReadReceipt](https://write.woa.com/document/181344255270170624)</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >false</td>

<td rowspan="1" colSpan="1" >是否启用已读回执功能。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[messageActionList](https://write.woa.com/document/181344255270170624)</td>

<td rowspan="1" colSpan="1" >IMessageAction[]</td>

<td rowspan="1" colSpan="1" >undefined</td>

<td rowspan="1" colSpan="1" >自定义消息操作列表，例如复制、撤回、删除等。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[messageAggregationTime](https://write.woa.com/document/181344255270170624)</td>

<td rowspan="1" colSpan="1" >number</td>

<td rowspan="1" colSpan="1" >300 (5分钟)</td>

<td rowspan="1" colSpan="1" >消息聚合时间间隔（秒），相同发送者在此时间内的连续消息会被聚合显示。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[filter](https://write.woa.com/document/181344255270170624)</td>

<td rowspan="1" colSpan="1" >(message: IMessageModel) => boolean</td>

<td rowspan="1" colSpan="1" >undefined</td>

<td rowspan="1" colSpan="1" >消息过滤函数，用于控制哪些消息需要显示。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[className](https://write.woa.com/document/181344255270170624)</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >undefined</td>

<td rowspan="1" colSpan="1" >自定义 CSS 类名。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[style](https://write.woa.com/document/181344255270170624)</td>

<td rowspan="1" colSpan="1" >React.CSSProperties</td>

<td rowspan="1" colSpan="1" >undefined</td>

<td rowspan="1" colSpan="1" >自定义内联样式。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[Message](https://write.woa.com/document/181344255270170624)</td>

<td rowspan="1" colSpan="1" >React.ComponentType</td>

<td rowspan="1" colSpan="1" >Message</td>

<td rowspan="1" colSpan="1" >自定义消息组件。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[MessageTimeDivider](https://write.woa.com/document/181344255270170624)</td>

<td rowspan="1" colSpan="1" >React.ComponentType</td>

<td rowspan="1" colSpan="1" >MessageTimeDivider</td>

<td rowspan="1" colSpan="1" >自定义时间分隔线组件。</td>
</tr>
</table>


## Prop 字段详解

### alignment

参数类型: `'left' | 'right' | 'two-sided'`

alignment 用于设置消息对齐方式，支持 `left`、`right`、`two-sided` 三种模式。默认值为 `'two-sided'`。
- `two-sided`: 非本人的消息位于左侧，本人的消息位于右侧

- `left`: 所有消息位于左侧

- `right`: 所有消息位于右侧


### enableReadReceipt

参数类型: `boolean`

enableReadReceipt 用于设置是否开启单条消息已读回执功能，默认值为 `false`。

### messageActionList

参数类型: `IMessageAction[]`

messageActionList 用于设置消息操作列表，例如复制、撤回、删除等操作，默认值为完整的消息操作列表 `['copy', 'recall', 'quote', 'forward', 'delete']`。
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

可以使用 `useMessageAction` 获取完整的消息操作列表，然后根据需要进行自定义。

#### 示例1: 变更消息操作列表的顺序

假设按照 `forward`、`copy`、`recall`、`quote`、`delete` 的顺序显示消息操作列表。
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

#### 示例2: 仅展示部分消息操作

假设仅展示 `forward`、`copy`、`recall` 三个操作。
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

#### 示例3: 自定义消息操作的样式

下面是一个自定义撤回操作的示例：
1. 将标签修改为'撤回 ⚠️'

2. 将颜色修改为橙色

3. 只有文本消息可以撤回

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

#### 示例4: 新增自定义消息操作

假设需要自定义消息操作，如仅其他人发送的消息可以标记'喜欢'，且插入在'撤回'操作之后。
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

参数类型: `number`

messageAggregationTime 用于设置消息聚合时间间隔，将相同发送者的连续消息聚合显示，默认值为 `300`（秒）。

### filter

参数类型: `(message: IMessageModel) => boolean`

filter 用于设置消息过滤函数，控制哪些消息需要显示，默认值为 `undefined`。

#### 示例: 过滤掉机器人发送的错误消息
``` tsx
import { MessageList } from '@/components/MessageList';
import TUIChatEngine from '@tencentcloud/chat-uikit-engine';

const messageFilter = (message) => {
  // 过滤掉发送者昵称包含 '_robot' 且内容包含 'operation-failed' 的文本消息
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

参数类型: `string`

className 用于设置根容器自定义 CSS 类名，默认值为 `undefined`。

### style

参数类型: `React.CSSProperties`

style 用于设置根容器自定义内联样式，默认值为 `undefined`。

### Message

参数类型: `React.ComponentType`

Message 用于设置自定义消息组件，替换默认的消息渲染组件，默认值为内置的 `Message` 组件。

#### 示例: 自定义 CUSTOM 消息点击跳转的消息组件
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
            跳转到外部网址 {restData.link}
          </a>
        </div>
      );
    }
  } else {
    // 其他消息类型使用默认消息组件
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

参数类型: `React.ComponentType`

MessageTimeDivider 用于设置自定义时间分隔线组件，默认值为内置的 `MessageTimeDivider` 组件。

#### 示例: 区分工作时间的时间分隔线
``` tsx
import { Chat, MessageList, MessageTimeDivider } from '@tencentcloud/chat-uikit-react';

const BusinessTimeDivider: typeof MessageTimeDivider = ({ prevMessage, currentMessage }) => {
  if (!prevMessage || !currentMessage) return null;
  
  // 对于即将渲染的每一条消息获取当前消息和上一消息的时间，并转换为日期对象，判断是否跨天或间隔超过4小时
  const currentTime = new Date(currentMessage.time * 1000);
  const prevTime = new Date(prevMessage.time * 1000);
  
  // 跨天或间隔超过4小时才显示
  const shouldShow = currentTime.toDateString() !== prevTime.toDateString() ||
                    (currentTime.getTime() - prevTime.getTime()) > 4 * 60 * 60 * 1000;
  
  if (!shouldShow) return null;
  
  // 判断工作时间 (9:00-18:00, 周一到周五)
  const isWorkingTime = () => {
    const hour = currentTime.getHours();
    const day = currentTime.getDay();
    return day >= 1 && day <= 5 && hour >= 9 && hour <= 18;
  };
  
  const timeLabel = isWorkingTime() ? '工作时间' : '非工作时间';
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

## 总结

MessageList 组件提供了完整的消息列表功能和丰富的自定义选项。通过合理配置 Props 和自定义组件，您可以创建出符合业务需求的聊天界面。建议在实际使用中根据具体场景选择合适的配置。