> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

# Overview

MessageInput is a fully functional message input component with core chat input features including text editing, emoji selection, file attachment, and a send button. It supports various custom options such as input behavior configuration, toolbar customization, component replacement, and slot expansion, meeting the demands of different chat scenarios with personalized requirements.


## Props Configuration
<table>
<tr>
<td rowspan="1" colSpan="1" >Field</td>


<td rowspan="1" colSpan="1" >Type</td>


<td rowspan="1" colSpan="1" >Default Value</td>


<td rowspan="1" colSpan="1" >Description</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[autoFocus](https://write.woa.com/document/181344257863962624)</td>


<td rowspan="1" colSpan="1" >boolean</td>


<td rowspan="1" colSpan="1" >true</td>


<td rowspan="1" colSpan="1" >Auto-focus to input box</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[disabled](https://write.woa.com/document/181344257863962624)</td>


<td rowspan="1" colSpan="1" >boolean</td>


<td rowspan="1" colSpan="1" >false</td>


<td rowspan="1" colSpan="1" >Disable input component</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[hideSendButton](https://write.woa.com/document/181344257863962624)</td>


<td rowspan="1" colSpan="1" >boolean</td>


<td rowspan="1" colSpan="1" >false</td>


<td rowspan="1" colSpan="1" >Whether to hide send button</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[placeholder](https://write.woa.com/document/181344257863962624)</td>


<td rowspan="1" colSpan="1" >string</td>


<td rowspan="1" colSpan="1" >''</td>


<td rowspan="1" colSpan="1" >Input box placeholder text</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[className](https://write.woa.com/document/181344257863962624)</td>


<td rowspan="1" colSpan="1" >string</td>


<td rowspan="1" colSpan="1" >undefined</td>


<td rowspan="1" colSpan="1" >Root container custom CSS class</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[style](https://write.woa.com/document/181344257863962624)</td>


<td rowspan="1" colSpan="1" >React.CSSProperties</td>


<td rowspan="1" colSpan="1" >undefined</td>


<td rowspan="1" colSpan="1" >Root container inline style</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[attachmentPickerMode](https://write.woa.com/document/181344257863962624)</td>


<td rowspan="1" colSpan="1" >'collapsed' \| 'expanded'</td>


<td rowspan="1" colSpan="1" >'collapsed'</td>


<td rowspan="1" colSpan="1" >Attachment selector display mode</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[actions](https://write.woa.com/document/181344257863962624)</td>


<td rowspan="1" colSpan="1" >MessageInputActions</td>


<td rowspan="1" colSpan="1" >['EmojiPicker', 'AttachmentPicker']</td>


<td rowspan="1" colSpan="1" >Toolbar button configuration</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[slots](https://write.woa.com/document/181344257863962624)</td>


<td rowspan="1" colSpan="1" >MessageInputSlots</td>


<td rowspan="1" colSpan="1" >undefined</td>


<td rowspan="1" colSpan="1" >Slot configuration object</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[TextEditor](https://write.woa.com/document/181344257863962624)</td>


<td rowspan="1" colSpan="1" >JSX.Element</td>


<td rowspan="1" colSpan="1" >undefined</td>


<td rowspan="1" colSpan="1" >Custom text editor component</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[EmojiPicker](https://write.woa.com/document/181344257863962624)</td>


<td rowspan="1" colSpan="1" >JSX.Element</td>


<td rowspan="1" colSpan="1" >undefined</td>


<td rowspan="1" colSpan="1" >Custom emoji selector component</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[AttachmentPicker](https://write.woa.com/document/181344257863962624)</td>


<td rowspan="1" colSpan="1" >JSX.Element</td>


<td rowspan="1" colSpan="1" >undefined</td>


<td rowspan="1" colSpan="1" >Custom attachment selector component</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[FilePicker](https://write.woa.com/document/181344257863962624)</td>


<td rowspan="1" colSpan="1" >JSX.Element</td>


<td rowspan="1" colSpan="1" >undefined</td>


<td rowspan="1" colSpan="1" >Custom file selector component</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[ImagePicker](https://write.woa.com/document/181344257863962624)</td>


<td rowspan="1" colSpan="1" >JSX.Element</td>


<td rowspan="1" colSpan="1" >undefined</td>


<td rowspan="1" colSpan="1" >Custom image selector component</td>
</tr>


<tr>
<td rowspan="1" colSpan="1" >[VideoPicker](https://write.woa.com/document/181344257863962624)</td>


<td rowspan="1" colSpan="1" >JSX.Element</td>


<td rowspan="1" colSpan="1" >undefined</td>


<td rowspan="1" colSpan="1" >Custom video selector component</td>
</tr>
</table>




Custom Function Explanation


### autoFocus


Parameter type: `boolean`


autoFocus is used to set whether to auto-focus into the input box when mounting, default value is `true`.


### disabled


Parameter type: `boolean`


disabled is used to set whether to disable the entire input component, including text input and all operation buttons, default value is `false`.


### hideSendButton


Parameter type: `boolean`


hideSendButton is used to set whether to hide the send button, suitable for scenarios where custom trigger modes are needed, default value is `false`.


### placeholder


Parameter type: `string`


placeholder is used to set the placeholder text for the input box, default value is an empty string.


### className


Parameter type: `string`


className is used to set the root container's custom CSS class name, default value is `undefined`.


### style


Parameter type: `React.CSSProperties`


style is used to set the root container's custom inline style, default value is `undefined`.


### attachmentPickerMode


Parameter type: `'collapsed' | 'expanded'`


attachmentPickerMode is used to set the display mode of the attachment selector, default value is `'collapsed'`.
- `collapsed`: Collapse mode, unfold options after clicking


- `expanded`: Expand mode, display all options directly
   


   **Note:**
   > 


   By default, AttachmentPicker refers to the attachment selector, including file selection, image selection, and video selection.
   > 
When the attachmentPickerModel is "collapsed", clicking the attachment selector pops up a menu displaying file selection, image selection, and video selection.
2. When the attachmentPickerModel is "expanded", the attachment selector will expand by default, showing file selection, image selection, and video selection in tile display.




### actions


Parameter type: `MessageInputActions`


actions for configuration toolbar display buttons, default value `['EmojiPicker', 'AttachmentPicker']`.
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


#### Example 1: Custom toolbar button sequence
``` tsx
import { Chat, MessageInput } from '@tencentcloud/chat-uikit-react';


function ChatWithCustomActions() {
  Custom button sequence: file, image, video, emoji
  const customActions = ['FilePicker', 'ImagePicker', 'VideoPicker', 'EmojiPicker'];
  
  return (
    <Chat>
      <MessageInput actions={customActions} />
    </Chat>
  );
}
```


#### Example 2: Add custom action button - Quick reply for customer service system
``` tsx
import { Chat, MessageInput } from '@tencentcloud/chat-uikit-react';
import { useMessageInputState } from '@/states';


Quick reply component
function QuickReplyPicker() {
  const { setContent } = useMessageInputState();
  
  const quickReplies = [
    Hello, glad to serve you.
    Please wait, I'll check for you...
    Thank you for your consultation. Any other issues?
    The issue has been resolved. Have a pleasant life!
  ];


  const handleQuickReply = (text: string) => {
    setContent(text);
  };


  return (
    <div style={{ position: 'relative' }}>
      <button title="quick reply">⚡</button>
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
      quick reply
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


Parameter type: `MessageInputSlots`


slots for inserting custom content in specific locations of the input component, default value is `undefined`.
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


![MessageInput structure diagram](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100033438418/7d08e80a559011f0989352540044a08e.png)


MessageInput structure diagram




#### Example 1: Add message statistics display
``` tsx
import { Chat, MessageInput } from '@tencentcloud/chat-uikit-react';
import { useMessageInputState } from '@/states';


function ChatWithMessageStats() {
  const { inputRawValue } = useMessageInputState();
  
  Header toolbar: Display character statistics
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
        Number of characters
        {' '}
        {inputRawValue?.reduce((acc, item) => acc + (item.type === 'text' ? item.content.length : 1), 0) || 0}
        /500
      </div>
    );


  // toolbar: display sending notification
  const FooterToolbar = () => (
    <div style={{
      padding: '4px 12px',
      fontSize: '12px',
      color: '#999',
      textAlign: 'right'
    }}>
      Press Ctrl+Enter to wrap text
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


#### Example 2: Input box prefix/suffix feature
``` tsx
import { Chat, MessageInput } from '@tencentcloud/chat-uikit-react';


function ChatWithInputPrefixSuffix() {
  @reminder feature in input box
  const InputPrefix = () => (
    <button 
      style={{ 
        border: 'none', 
        background: 'transparent',
        color: '#1890ff',
        cursor: 'pointer'
      }}
      onClick={() => {
        // Trigger @user selection
        console.log('turn on @user selection');
      }}
    >
      @
    </button>
  );


  voice input in input box
  const InputSuffix = () => (
    <button
      style={{
        border: 'none',
        background: 'transparent',
        cursor: 'pointer'
      }}
      onClick={() => {
        Start voice input
        console.log('start voice input');
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


#### Example 3: Full customization of left and right toolbars
``` tsx
import { Chat, MessageInput } from '@tencentcloud/chat-uikit-react';


function ChatWithCustomToolbars() {
  // Left toolbar: Only retain emoji and images
  const LeftInline = () => (
    <div style={{ display: 'flex', gap: '8px' }}>
      <button>😊</button>
      <button>📷</button>
    </div>
  );


  // the tool bar on the right: custom send area
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
        Send
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


Parameter type: `JSX.Element`


TextEditor replaces the default text editor component. Default value: `undefined`.


Integrate a rich text editor
``` tsx
import { Chat, MessageInput, useMessageInputState } from '@tencentcloud/chat-uikit-react';


// Custom rich text editor
function RichTextEditor() {
  const { sendMessage } = useMessageInputState();
  const [inputValue, setInputValue] = useState('');


  const handleContentChange = (content: string) => {
    setInputValue(content);
  };


  const handleKeyDown = (e: React.KeyboardEvent) => {
    // Press Enter to send a message
    if (e.key === 'Enter') {
      // Trigger send logic
      e.preventDefault();
      sendMessage(inputValue);
      Clear input
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


Parameter type: `JSX.Element`


EmojiPicker replaces the default emoji selector component with a default value of `undefined`.


#### Example: Custom emoji panel
``` tsx
import { Chat, MessageInput } from '@tencentcloud/chat-uikit-react';
import { useMessageInputState } from '@/states';


Custom emoji selector
function CustomEmojiPicker() {
  const { insertContent } = useMessageInputState();


  const emojiCategories = {
    Common: ['😀', '😂', '🥰', '😍', '🤔', '😭', '😡', '👍']
    Gestures: ['👋', '🤝', '👏', '🙏', '✌️', '🤞', '🤟', '👌']
    Animals: ['🐶', '🐱', '🐭', '🐹', '🐰', '🦊', '🐻', '🐼']
  };


  const [activeCategory, setActiveCategory] = useState('Common');
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
          category tag
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


          {/* Emoji grid */}
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


Parameter type: `JSX.Element`


AttachmentPicker is used to replace the default attachment selector component, default value is `undefined`.


Storage integration attachment selector
``` tsx
import { Chat, MessageInput } from '@tencentcloud/chat-uikit-react';


// Cloud storage attachment selector with seamless integration
function CloudAttachmentPicker() {
  const [showPicker, setShowPicker] = useState(false);
  
  const attachmentTypes = [
    { key: 'local', label: 'Local file', icon: '📁' },
    { key: 'cloud', label: 'Cloud file', icon: '☁️' },
    { key: 'recent', label: 'Recent files', icon: '🕒' },
    { key: 'screenshot', label: 'Screenshot', icon: '📷' }
  ];


  const handleAttachmentSelect = async (type: string) => {
    switch (type) {
      case 'local':
        Open local file selection
        const input = document.createElement('input');
        input.type = 'file';
        input.multiple = true;
        input.onchange = (e) => {
          const files = (e.target as HTMLInputElement).files;
          console.log('selected local files:', files);
        };
        input.click();
        break;
        
      case 'cloud':
        Open cloud-based file selection
        console.log('Open cloud-based file selection');
        break;
        
      case 'recent':
        Display recent files
        console.log('display recent files');
        break;
        
      case 'screenshot':
        Start screenshot
        console.log('start screenshot');
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


## Summary

The MessageInput component provides complete message input functionality and various custom options. By reasonably configuring Props and using the slot system, you can create an input interface that meets specific business requirements. It is advisable to choose appropriate customized schemes based on actual use scenes and maintain good user experience and performance. 
