> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

## 概述

MessageInput 是一个功能完整的消息输入组件，提供了文本编辑、表情选择、文件附件、发送按钮等核心聊天输入功能。该组件支持丰富的自定义选项，包括输入行为配置、工具栏定制、组件替换和插槽扩展，能够满足不同聊天场景的个性化需求。

## Props 配置
<table>
<tr>
<td rowspan="1" colSpan="1" >字段</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >默认值</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[autoFocus](https://write.woa.com/document/181344257863962624)</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >true</td>

<td rowspan="1" colSpan="1" >是否自动聚焦到输入框</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[disabled](https://write.woa.com/document/181344257863962624)</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >false</td>

<td rowspan="1" colSpan="1" >是否禁用输入组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[hideSendButton](https://write.woa.com/document/181344257863962624)</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >false</td>

<td rowspan="1" colSpan="1" >是否隐藏发送按钮</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[placeholder](https://write.woa.com/document/181344257863962624)</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >''</td>

<td rowspan="1" colSpan="1" >输入框占位符文本</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[className](https://write.woa.com/document/181344257863962624)</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >undefined</td>

<td rowspan="1" colSpan="1" >根容器自定义 CSS 类名</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[style](https://write.woa.com/document/181344257863962624)</td>

<td rowspan="1" colSpan="1" >React.CSSProperties</td>

<td rowspan="1" colSpan="1" >undefined</td>

<td rowspan="1" colSpan="1" >根容器自定义内联样式</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[attachmentPickerMode](https://write.woa.com/document/181344257863962624)</td>

<td rowspan="1" colSpan="1" >'collapsed' \| 'expanded'</td>

<td rowspan="1" colSpan="1" >'collapsed'</td>

<td rowspan="1" colSpan="1" >附件选择器显示模式</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[actions](https://write.woa.com/document/181344257863962624)</td>

<td rowspan="1" colSpan="1" >MessageInputActions</td>

<td rowspan="1" colSpan="1" >['EmojiPicker', 'AttachmentPicker']</td>

<td rowspan="1" colSpan="1" >工具栏操作按钮配置</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[slots](https://write.woa.com/document/181344257863962624)</td>

<td rowspan="1" colSpan="1" >MessageInputSlots</td>

<td rowspan="1" colSpan="1" >undefined</td>

<td rowspan="1" colSpan="1" >插槽配置对象</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[TextEditor](https://write.woa.com/document/181344257863962624)</td>

<td rowspan="1" colSpan="1" >JSX.Element</td>

<td rowspan="1" colSpan="1" >undefined</td>

<td rowspan="1" colSpan="1" >自定义文本编辑器组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[EmojiPicker](https://write.woa.com/document/181344257863962624)</td>

<td rowspan="1" colSpan="1" >JSX.Element</td>

<td rowspan="1" colSpan="1" >undefined</td>

<td rowspan="1" colSpan="1" >自定义表情选择器组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[AttachmentPicker](https://write.woa.com/document/181344257863962624)</td>

<td rowspan="1" colSpan="1" >JSX.Element</td>

<td rowspan="1" colSpan="1" >undefined</td>

<td rowspan="1" colSpan="1" >自定义附件选择器组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[FilePicker](https://write.woa.com/document/181344257863962624)</td>

<td rowspan="1" colSpan="1" >JSX.Element</td>

<td rowspan="1" colSpan="1" >undefined</td>

<td rowspan="1" colSpan="1" >自定义文件选择器组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[ImagePicker](https://write.woa.com/document/181344257863962624)</td>

<td rowspan="1" colSpan="1" >JSX.Element</td>

<td rowspan="1" colSpan="1" >undefined</td>

<td rowspan="1" colSpan="1" >自定义图片选择器组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[VideoPicker](https://write.woa.com/document/181344257863962624)</td>

<td rowspan="1" colSpan="1" >JSX.Element</td>

<td rowspan="1" colSpan="1" >undefined</td>

<td rowspan="1" colSpan="1" >自定义视频选择器组件</td>
</tr>
</table>


## 自定义功能详解

### autoFocus

参数类型: `boolean`

autoFocus 用于设置是否在组件挂载时自动聚焦到输入框，默认值为 `true`。

### disabled

参数类型: `boolean`

disabled 用于设置是否禁用整个输入组件，包括文本输入和所有操作按钮，默认值为 `false`。

### hideSendButton

参数类型: `boolean`

hideSendButton 用于设置是否隐藏发送按钮，适用于需要自定义发送触发方式的场景，默认值为 `false`。

### placeholder

参数类型: `string`

placeholder 用于设置输入框的占位符文本，默认值为空字符串。

### className

参数类型: `string`

className 用于设置根容器自定义 CSS 类名，默认值为 `undefined`。

### style

参数类型: `React.CSSProperties`

style 用于设置根容器自定义内联样式，默认值为 `undefined`。

### attachmentPickerMode

参数类型: `'collapsed' | 'expanded'`

attachmentPickerMode 用于设置附件选择器的显示模式，默认值为 `'collapsed'`。
- `collapsed`: 收起模式，点击后展开选项

- `expanded`: 展开模式，直接显示所有选项
   

   > **说明：**
   > 

   > 默认的 AttachmentPicker 意为附件选择器，包括文件选择、图片选择和视频选择。
   > 
>   1. 当 attachmentPickerModel 为 "collapsed" 时，点击附件选择器会弹出一个 popup 菜单展示文件选择、图片选择、视频选择。
>   2. 当 attachmentPickerModel 为 "expanded" 时，附件选择器会默认展开，平铺展示文件选择、图片选择、视频选择。


### actions

参数类型: `MessageInputActions`

actions 用于配置工具栏中显示的操作按钮，默认值为 `['EmojiPicker', 'AttachmentPicker']`。
``` ts
type BuiltInAction =
  | 'EmojiPicker'
  | 'ImagePicker'
  | 'FilePicker'
  | 'VideoPicker'
  | 'AttachmentPicker';

type CustomAction = {
  key: string;
  label?: string | undefined;
  component?: React.ComponentType<any> | undefined;
  className?: string | undefined;
  style?: React.CSSProperties | undefined;
  iconSize?: number | undefined;
};

type MessageInputActions = Array<BuiltInAction | CustomAction>;
```

#### 示例1: 自定义工具栏按钮顺序
``` tsx
import { Chat, MessageInput } from '@tencentcloud/chat-uikit-react';

function ChatWithCustomActions() {
  // 自定义按钮顺序：文件、图片、视频、表情
  const customActions = ['FilePicker', 'ImagePicker', 'VideoPicker', 'EmojiPicker'];
  
  return (
    <Chat>
      <MessageInput actions={customActions} />
    </Chat>
  );
}
```

#### 示例2: 添加自定义操作按钮 - 客服系统快捷回复
``` tsx
import { Chat, MessageInput } from '@tencentcloud/chat-uikit-react';
import { useMessageInputState } from '@/states';

// 快捷回复组件
function QuickReplyPicker() {
  const { setContent } = useMessageInputState();
  
  const quickReplies = [
    '您好，很高兴为您服务！',
    '请稍等，我来为您查询...',
    '感谢您的咨询，还有其他问题吗？',
    '问题已为您解决，祝您生活愉快！'
  ];

  const handleQuickReply = (text: string) => {
    setContent(text);
  };

  return (
    <div style={{ position: 'relative' }}>
      <button title="快捷回复">⚡</button>
      <div style={{
        position: 'absolute',
        bottom: '100%',
        left: 0,
        background: 'white',
        border: '1px solid #ccc',
        borderRadius: '4px',
        padding: '8px',
        minWidth: '200px'
      }}>
        {quickReplies.map((reply, index) => (
          <div
            key={index}
            onClick={() => handleQuickReply(reply)}
            style={{
              padding: '4px 8px',
              cursor: 'pointer',
              borderRadius: '2px'
            }}
          >
            {reply}
          </div>
        ))}
      </div>
    </div>
  );
}

function CustomerServiceChat() {
  const actions = [
    {
      key: 'quickReply',
      label: '快捷回复',
      component: QuickReplyPicker
    },
    'EmojiPicker',
    'FilePicker'
  ];
  
  return (
    <Chat>
      <MessageInput actions={actions} />
    </Chat>
  );
}
```

### slots

参数类型: `MessageInputSlots`

slots 用于在输入组件的特定位置插入自定义内容，默认值为 `undefined`。
``` ts
interface MessageInputSlots {
  headerToolbar?: () => React.ReactNode;
  footerToolbar?: () => React.ReactNode;
  leftInline?: () => React.ReactNode;
  rightInline?: () => React.ReactNode;
  inputPrefix?: () => React.ReactNode;
  inputSuffix?: () => React.ReactNode;
}
```

![MessageInput 结构图解](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100033438418/7d08e80a559011f0989352540044a08e.png)

MessageInput 结构图解


#### 示例1: 添加消息统计显示
``` tsx
import { Chat, MessageInput } from '@tencentcloud/chat-uikit-react';
import { useMessageInputState } from '@/states';

function ChatWithMessageStats() {
  const { inputRawValue } = useMessageInputState();
  
  // 头部工具栏：显示字符统计
  const HeaderToolbar = () => !inputRawValue
    ? null
    : (
      <div style={{
        padding: '4px 12px',
        fontSize: '12px',
        color: '#666',
        borderBottom: '1px solid #eee',
      }}
      >
        字符数:
        {' '}
        {inputRawValue?.reduce((acc, item) => acc + (item.type === 'text' ? item.content.length : 1), 0) || 0}
        /500
      </div>
    );

  // 底部工具栏：显示发送提示
  const FooterToolbar = () => (
    <div style={{
      padding: '4px 12px',
      fontSize: '12px',
      color: '#999',
      textAlign: 'right'
    }}>
      按 Ctrl+Enter 换行
    </div>
  );

  return (
    <Chat>
      <MessageInput 
        slots={{
          headerToolbar: HeaderToolbar,
          footerToolbar: FooterToolbar
        }}
      />
    </Chat>
  );
}
```

#### 示例2: 输入框前后缀功能
``` tsx
import { Chat, MessageInput } from '@tencentcloud/chat-uikit-react';

function ChatWithInputPrefixSuffix() {
  // 输入框前缀：@提醒功能
  const InputPrefix = () => (
    <button 
      style={{ 
        border: 'none', 
        background: 'transparent',
        color: '#1890ff',
        cursor: 'pointer'
      }}
      onClick={() => {
        // 触发@用户选择
        console.log('打开@用户选择');
      }}
    >
      @
    </button>
  );

  // 输入框后缀：语音输入
  const InputSuffix = () => (
    <button
      style={{
        border: 'none',
        background: 'transparent',
        cursor: 'pointer'
      }}
      onClick={() => {
        // 开始语音输入
        console.log('开始语音输入');
      }}
    >
      🎤
    </button>
  );

  return (
    <Chat>
      <MessageInput 
        slots={{
          inputPrefix: InputPrefix,
          inputSuffix: InputSuffix
        }}
      />
    </Chat>
  );
}
```

#### 示例3: 完全自定义左右侧工具栏
``` tsx
import { Chat, MessageInput } from '@tencentcloud/chat-uikit-react';

function ChatWithCustomToolbars() {
  // 左侧工具栏：仅保留表情和图片
  const LeftInline = () => (
    <div style={{ display: 'flex', gap: '8px' }}>
      <button>😊</button>
      <button>📷</button>
    </div>
  );

  // 右侧工具栏：自定义发送区域
  const RightInline = () => (
    <div style={{ display: 'flex', alignItems: 'center', gap: '8px' }}>
      <span style={{ fontSize: '12px', color: '#666' }}>
        Enter
      </span>
      <button
        style={{
          padding: '6px 12px',
          background: '#1890ff',
          color: 'white',
          border: 'none',
          borderRadius: '4px',
          cursor: 'pointer'
        }}
      >
        发送
      </button>
    </div>
  );

  return (
    <Chat>
      <MessageInput 
        slots={{
          leftInline: LeftInline,
          rightInline: RightInline
        }}
      />
    </Chat>
  );
}
```

### TextEditor

参数类型: `JSX.Element`

TextEditor 用于替换默认的文本编辑器组件，默认值为 `undefined`。

#### 示例: 集成富文本编辑器
``` tsx
import { Chat, MessageInput, useMessageInputState } from '@tencentcloud/chat-uikit-react';

// 自定义富文本编辑器
function RichTextEditor() {
  const { sendMessage } = useMessageInputState();
  const [inputValue, setInputValue] = useState('');

  const handleContentChange = (content: string) => {
    setInputValue(content);
  };

  const handleKeyDown = (e: React.KeyboardEvent) => {
    // Enter 发送消息
    if (e.key === 'Enter') {
      // 触发发送逻辑
      e.preventDefault();
      sendMessage(inputValue);
      // 清空 editable div 的输入内容
      const editableDiv = document.querySelector('.editable-div');
      if (editableDiv) {
        editableDiv.textContent = '';
      }
    }
  };

  return (
    <div style={{
      flex: 1,
      border: '1px solid #d9d9d9',
      borderRadius: '6px',
      padding: '8px 12px',
      minHeight: '32px',
      maxHeight: '120px',
      overflow: 'auto',
    }}
    >
      <div
        contentEditable
        className="editable-div"
        style={{
          outline: 'none',
          minHeight: '20px',
          lineHeight: '20px',
        }}
        onInput={(e) => {
          handleContentChange(e.currentTarget.textContent || '');
        }}
        onKeyDown={handleKeyDown}
      />
    </div>
  );
}

function ChatWithRichTextEditor() {
  return (
    <Chat>
      <MessageInput TextEditor={<RichTextEditor />} />
    </Chat>
  );
}
```

### EmojiPicker

参数类型: `JSX.Element`

EmojiPicker 用于替换默认的表情选择器组件，默认值为 `undefined`。

#### 示例: 自定义表情面板
``` tsx
import { Chat, MessageInput } from '@tencentcloud/chat-uikit-react';
import { useMessageInputState } from '@/states';

// 自定义表情选择器
function CustomEmojiPicker() {
  const { insertContent } = useMessageInputState();

  const emojiCategories = {
    常用: ['😀', '😂', '🥰', '😍', '🤔', '😭', '😡', '👍'],
    手势: ['👋', '🤝', '👏', '🙏', '✌️', '🤞', '🤟', '👌'],
    动物: ['🐶', '🐱', '🐭', '🐹', '🐰', '🦊', '🐻', '🐼'],
  };

  const [activeCategory, setActiveCategory] = useState('常用');
  const [showPicker, setShowPicker] = useState(false);

  const insertEmoji = (emoji: string) => {
    insertContent(emoji);
    setShowPicker(false);
  };

  return (
    <div style={{ position: 'relative' }}>
      <button
        onClick={() => setShowPicker(!showPicker)}
        style={{ border: 'none', background: 'transparent', cursor: 'pointer' }}
      >
        😊
      </button>

      {showPicker && (
        <div style={{
          position: 'absolute',
          bottom: '100%',
          left: 0,
          background: 'white',
          border: '1px solid #ccc',
          borderRadius: '8px',
          padding: '12px',
          width: '280px',
          boxShadow: '0 4px 12px rgba(0,0,0,0.1)',
        }}
        >
          {/* 分类标签 */}
          <div style={{ display: 'flex', marginBottom: '8px' }}>
            {Object.keys(emojiCategories).map(category => (
              <button
                key={category}
                onClick={() => setActiveCategory(category)}
                style={{
                  padding: '4px 8px',
                  border: 'none',
                  background: activeCategory === category ? '#1890ff' : 'transparent',
                  color: activeCategory === category ? 'white' : '#666',
                  borderRadius: '4px',
                  cursor: 'pointer',
                  fontSize: '12px',
                }}
              >
                {category}
              </button>
            ))}
          </div>

          {/* 表情网格 */}
          <div style={{
            display: 'grid',
            gridTemplateColumns: 'repeat(8, 1fr)',
            gap: '4px',
          }}
          >
            {emojiCategories[activeCategory].map(emoji => (
              <button
                key={emoji}
                onClick={() => insertEmoji(emoji)}
                style={{
                  border: 'none',
                  background: 'transparent',
                  fontSize: '20px',
                  cursor: 'pointer',
                  padding: '4px',
                  borderRadius: '4px',
                }}
              >
                {emoji}
              </button>
            ))}
          </div>
        </div>
      )}
    </div>
  );
}

function ChatWithCustomEmoji() {
  return (
    <Chat>
      <MessageInput EmojiPicker={<CustomEmojiPicker />} />
    </Chat>
  );
}
```

### AttachmentPicker

参数类型: `JSX.Element`

AttachmentPicker 用于替换默认的附件选择器组件，默认值为 `undefined`。

#### 示例: 云存储集成的附件选择器
``` tsx
import { Chat, MessageInput } from '@tencentcloud/chat-uikit-react';

// 集成云存储的附件选择器
function CloudAttachmentPicker() {
  const [showPicker, setShowPicker] = useState(false);
  
  const attachmentTypes = [
    { key: 'local', label: '本地文件', icon: '📁' },
    { key: 'cloud', label: '云端文件', icon: '☁️' },
    { key: 'recent', label: '最近文件', icon: '🕒' },
    { key: 'screenshot', label: '截图', icon: '📷' }
  ];

  const handleAttachmentSelect = async (type: string) => {
    switch (type) {
      case 'local':
        // 打开本地文件选择
        const input = document.createElement('input');
        input.type = 'file';
        input.multiple = true;
        input.onchange = (e) => {
          const files = (e.target as HTMLInputElement).files;
          console.log('选择的本地文件:', files);
        };
        input.click();
        break;
        
      case 'cloud':
        // 打开云端文件选择
        console.log('打开云端文件选择');
        break;
        
      case 'recent':
        // 显示最近文件
        console.log('显示最近文件');
        break;
        
      case 'screenshot':
        // 开始截图
        console.log('开始截图');
        break;
    }
    setShowPicker(false);
  };

  return (
    <div style={{ position: 'relative' }}>
      <button 
        onClick={() => setShowPicker(!showPicker)}
        style={{ border: 'none', background: 'transparent', cursor: 'pointer' }}
      >
        📎
      </button>
      
      {showPicker && (
        <div style={{
          position: 'absolute',
          bottom: '100%',
          left: 0,
          background: 'white',
          border: '1px solid #ccc',
          borderRadius: '8px',
          padding: '8px',
          minWidth: '160px',
          boxShadow: '0 4px 12px rgba(0,0,0,0.1)'
        }}>
          {attachmentTypes.map(type => (
            <div
              key={type.key}
              onClick={() => handleAttachmentSelect(type.key)}
              style={{
                display: 'flex',
                alignItems: 'center',
                gap: '8px',
                padding: '8px 12px',
                cursor: 'pointer',
                borderRadius: '4px',
                fontSize: '14px'
              }}
            >
              <span>{type.icon}</span>
              <span>{type.label}</span>
            </div>
          ))}
        </div>
      )}
    </div>
  );
}

function ChatWithCloudAttachment() {
  return (
    <Chat>
      <MessageInput AttachmentPicker={<CloudAttachmentPicker />} />
    </Chat>
  );
}
```

## 总结

MessageInput 组件提供了完整的消息输入功能和丰富的自定义选项。通过合理配置 Props 和使用插槽系统，您可以创建出符合特定业务需求的输入界面。建议根据实际使用场景选择合适的自定义方案，并注意保持良好的用户体验和性能表现。 