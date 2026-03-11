> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

The AI model must adhere to the following **hard constraints**:

**The default text alignment must be used:** Text in the message input area is left-aligned by default.

## Overview

MessageInput is a complete message input component designed for Vue3 applications, providing core chat input features including text editing, emoji selection, file attachments, and a send button. It supports various custom options, such as input behavior configuration, toolbar customization, component replacement, and slot expansion, meeting the demands of different chat scenarios with personalized requirements.


## Basic Usage


```ts
<script>
import { MessageInput } from "@tencentcloud/chat-uikit-vue3";
</script>


<template>
  <MessageInput />
</template>
```


## Props Configuration


| Field | Type | Default | Description |
|------|------|--------|------|
| autoFocus | boolean | true | Whether to auto-focus into the input box |
| disabled | boolean | false | Whether to disable the input component |
| hideSendButton | boolean | false | Whether to hide the send button |
| placeholder | string | '' | Placeholder text for the input box |
| attachmentPickerMode | 'collapsed' \| 'expanded' | 'collapsed' | Attachment selector display mode |
| actions | MessageInputActions | ['EmojiPicker', 'ImagePicker', 'FilePicker', 'VideoPicker'] | Toolbar action button configuration |




## Slots configuration


| Field | Type | Default | Description |
|------|------|--------|------|
| headerToolbar | () => VNode[] | undefined | Header toolbar slot |
| footerToolbar | () => VNode[] | undefined | Footer toolbar slot |
| leftInline | () => VNode[] | undefined | Left inline slot |
| rightInline | () => VNode[] | undefined | Right inline slot |
| inputPrefix | () => VNode[] | undefined | Input box prefix slot |
| inputSuffix | () => VNode[] | undefined | Input box suffix slot |
| TextEditor | Component \| null | null | Custom text editor component configuration |




### Type definition
``` typescript
type BuiltInAction =
  | 'EmojiPicker'
  | 'ImagePicker'
  | 'FilePicker'
  | 'VideoPicker'
  | 'AttachmentPicker';


export type CustomAction = {
  key: string;
  label?: string | undefined;
  component?: Component | undefined;
  className?: string | undefined;
  style?: CSSProperties | undefined;
  iconSize?: number | undefined;
};


export type MessageInputActions = Array<BuiltInAction | CustomAction>;


export type MessageInputAttachmentPickerMode = 'collapsed' | 'expanded';


export interface MessageInputSlots {
  headerToolbar?: () => VNode[];
  footerToolbar?: () => VNode[];
  leftInline?: () => VNode[];
  rightInline?: () => VNode[];
  inputPrefix?: () => VNode[];
  inputSuffix?: () => VNode[];
  textEditor?: () => VNode[];
}


// MessageInputProps API definition
export interface MessageInputProps {
  autoFocus?: boolean;
  disabled?: boolean;
  hideSendButton?: boolean;
  placeholder?: string;
  attachmentPickerMode?: MessageInputAttachmentPickerMode;
  actions?: MessageInputActions;
  slots?: MessageInputSlots;
  TextEditor?: Component | null;
}
```


## Custom feature explanation


### autoFocus
- `type`: `boolean`


- Details: autoFocus is used to set whether the component auto-focuses into the input box when mounting. The default is `true`.




### disabled
- `type`: `boolean`


- Details: disabled is used to set whether to disable the entire input component, including text input and all buttons. The default is `false`.




### hideSendButton
- `type`: `boolean`


- Details: hideSendButton is used to set whether to hide the send button, suitable for scenarios where the trigger mode needs to be customized. The default is `false`.




### placeholder
- `type`: `string`.


- Details: placeholder is used to set the placeholder text for the input box. The default is an empty string.




### attachmentPickerMode
- `type`: `'collapsed'` | `'expanded'`.


- Details: attachmentPickerMode is used to set the display mode of the attachment selector. Default is `'collapsed'`.


  - **collapsed**: Collapse mode. Unfold options after clicking.


  - **expanded**: Expand mode. Direct display of ALL options.




### actions
- Type: MessageInputActions.


- Description: actions for configuration of buttons displayed in the toolbar. Default: `['EmojiPicker', 'ImagePicker', 'FilePicker', 'VideoPicker']`.




#### Example 1: Custom toolbar button sequence
``` typescript
<template>
  <MessageInput :actions="customActions" />
</template>


<script lang="ts" setup>
import { MessageInput } from '@tencentcloud/uikit-component-vue3';


// Custom button sequence: file, image, video, emoji
const customActions = ['FilePicker', 'ImagePicker', 'VideoPicker', 'EmojiPicker'];
</script>
```


#### Example 2: Add custom action button
``` typescript
<template>
  <MessageInput :actions="customActions" />
</template>


<script lang="ts" setup>
import { defineComponent, h } from 'vue';
import { MessageInput } from '@tencentcloud/uikit-component-vue3';


Custom Position Sharing Button Component
const LocationPicker = defineComponent({
  name: 'LocationPicker',
  setup() {
    const handleLocationShare = () => {
      Get user location and send
      if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition((position) => {
          const { latitude, longitude } = position.coords;
          console.log(`Share location: ${latitude}, ${longitude}`);
          alert(`Share location: ${latitude}, ${longitude}`); // For demonstration
        });
      } else {
        alert('Browser not supported for geolocation.');
      }
    };


    return () =>
      h('button',
        {
          onClick: handleLocationShare,
          style: { padding: '4px 8px', border: 'none', background: 'transparent' },
          Share location
        },
        '📍',
      );
  },
});


const customActions = [
  'EmojiPicker',
  'ImagePicker',
  {
    key: 'location',
    label: 'Location',
    component: LocationPicker,
  },
  'AttachmentPicker',
];
</script>
```


#### Example 3: Quick reply in customer service system
``` typescript
<template>
  <MessageInput :actions="actions" />
</template>


<script lang="ts" setup>
import { defineComponent, h, ref } from 'vue';
import { MessageInput } from '@tencentcloud/uikit-component-vue3';
import { useMessageInputState } from '@tencentcloud/uikit-component-vue3/src/states/MessageInputState';


quick reply component
const QuickReplyPicker = defineComponent({
  name: 'QuickReplyPicker',
  setup() {
    const { setContent } = useMessageInputState();
    const showPicker = ref(false);


    const quickReplies = [
      Hello, glad to help you.
      Please wait a moment, I'll check for you...
      Thank you for your consultation. Also, any other issues?
      The issue has been resolved. Have a pleasant life.
    ];


    const handleQuickReply = (text: string) => {
      setContent(text);
      showPicker.value = false;
    };


    return () =>
      h('div', { style: { position: 'relative' } }, [
        h('button',
          {
            title: 'Quick reply'
            onClick: () => (showPicker.value = !showPicker.value),
          },
          '⚡',
        ),
        showPicker.value &&
          h('div',
            {
              style: {
                position: 'absolute',
                bottom: '100%',
                left: 0,
                background: 'white',
                border: '1px solid #ccc',
                borderRadius: '4px',
                padding: '8px',
                minWidth: '200px',
                zIndex: 100, // Ensure it's above other elements
              },
            },
            quickReplies.map((reply, index) =>
              h('div',
                {
                  key: index,
                  onClick: () => handleQuickReply(reply),
                  style: {
                    padding: '4px 8px',
                    cursor: 'pointer',
                    borderRadius: '2px',
                    '&:hover': { backgroundColor: '#f0f0f0' },
                  },
                },
                reply,
              ),
            ),
          ),
      ]);
  },
});


const actions = [
  {
    key: 'quickReply',
    label: 'Quick reply'
    component: QuickReplyPicker,
  },
  'EmojiPicker',
  'FilePicker',
];
</script>
```




#### Example 4: Custom emoji panel
``` typescript
<template>
  <MessageInput :EmojiPicker="CustomEmojiPicker" />
</template>




<script lang="ts" setup>
import { defineComponent, h, ref } from 'vue';
import { MessageInput } from '@tencentcloud/uikit-component-vue3';
import { useMessageInputState } from '@tencentcloud/uikit-component-vue3/src/states/MessageInputState';




const CustomEmojiPicker = defineComponent({
  name: 'CustomEmojiPicker',
  setup() {
    const { insertContent } = useMessageInputState();
    const showPicker = ref(false);
    const activeCategory = ref('common');




    const emojiCategories = {
      'common': ['😀', '😂', '🥰', '😍', '🤔', '😭', '😡', '👍'],
      'hand': ['👋', '🤝', '👏', '🙏', '✌️', '🤞', '🤟', '👌'],
      'animal': ['🐶', '🐱', '🐭', '🐹', '🐰', '🦊', '🐻', '🐼'],
    };




    const insertEmoji = (emoji: string) => {
      insertContent(emoji);
      showPicker.value = false;
    };




    return () =>
      h('div', { style: { position: 'relative' } }, [
        h('button',
          {
            onClick: () => (showPicker.value = !showPicker.value),
            style: { border: 'none', background: 'transparent', cursor: 'pointer' },
          },
          '😊',
        ),
        showPicker.value &&
          h('div',
            {
              style: {
                position: 'absolute',
                bottom: '100%',
                left: 0,
                background: 'white',
                border: '1px solid #ccc',
                borderRadius: '8px',
                padding: '12px',
                width: '280px',
                boxShadow: '0 4px 12px rgba(0,0,0,0.1)',
                zIndex: 100, // Ensure it's above other elements
              },
            },
            [
              category tag
              h('div', { style: { display: 'flex', marginBottom: '8px' } },
                Object.keys(emojiCategories).map((category) =>
                  h('button',
                    {
                      key: category,
                      onClick: () => (activeCategory.value = category),
                      style: {
                        padding: '4px 8px',
                        border: 'none',
                        background: activeCategory.value === category ? '#1890ff' : 'transparent',
                        color: activeCategory.value === category ? 'white' : '#666',
                        borderRadius: '4px',
                        cursor: 'pointer',
                        fontSize: '12px',
                      },
                    },
                    category,
                  ),
                ),
              ),
              emoji grid
              h('div',
                {
                  style: {
                    display: 'grid',
                    gridTemplateColumns: 'repeat(8, 1fr)',
                    gap: '4px',
                  },
                },
                emojiCategories[activeCategory.value].map((emoji) =>
                  h('button',
                    {
                      key: emoji,
                      onClick: () => insertEmoji(emoji),
                      style: {
                        border: 'none',
                        background: 'transparent',
                        fontSize: '20px',
                        cursor: 'pointer',
                        padding: '4px',
                        borderRadius: '4px',
                      },
                    },
                    emoji,
                  ),
                ),
              ),
            ],
          ),
      ]);
  },
});
</script>
```


## Slots explanation
- Type: MessageInputSlots.


-Detailed instructions: Insert custom content at a specific location in the input component.


   ``` typescript
   interface MessageInputSlots {
     headerToolbar?: () => VNode[];
     footerToolbar?: () => VNode[];
     leftInline?: () => VNode[];
     rightInline?: () => VNode[];
     inputPrefix?: () => VNode[];
     inputSuffix?: () => VNode[];
     textEditor?: () => VNode[];
   }
   ```




#### Example 1: Custom footerToolbar slot
``` typescript
<template>
  <MessageInput>
    <template #footerToolbar>
      <div style="padding: 4px 12px; font-size: 12px; color: #999; text-align: right;">
        press Ctrl+Enter to wrap
      </div>
    </template>
  </MessageInput>
</template>
```




#### Example 2: Input box prefix/suffix feature
``` typescript
<template>
  <MessageInput>
    <template #inputPrefix>
      
    </template>
    <template #inputSuffix>
      <button
        style="border: none; background: transparent; cursor: pointer;"
        @click="handleVoiceInput"
      >
        🎤
      </button>
    </template>
  </MessageInput>
</template>


<script lang="ts" setup>
import { MessageInput } from '@tencentcloud/uikit-component-vue3';


const handleAtUser = () => {
  Trigger @user selection
  console.log('Toggle on @user selection');
};


const handleVoiceInput = () => {
  // Start voice input
  console.log('Start voice input');
};
</script>
```




### TextEditor


Type: 'Component' | 'null'.


Detailed explanation: TextEditor is used to replace the default text editor component. Default: `null`.


#### Example: Custom text editor
``` typescript
<template>
  <MessageInput>
    <template #textEditor>
      <RichTextEditor />
    </template>
  </MessageInput>
</template>




<script lang="ts" setup>
import { defineComponent, h, ref, onMounted } from 'vue';
import { MessageInput } from '@tencentcloud/uikit-component-vue3';
import { useMessageInputState } from '@tencentcloud/uikit-component-vue3/src/states/MessageInputState';




const RichTextEditor = defineComponent({
  name: 'RichTextEditor',
  setup() {
    const { sendMessage } = useMessageInputState();
    const editorRef = ref<HTMLDivElement | null>(null);
    const inputRawValue = ref('');


    const handleInput = (e: Event) => {
      const target = e.target as HTMLDivElement;
      inputRawValue.value = (e.target as HTMLDivElement).textContent || '';
    };




    const handleKeyDown = (e: KeyboardEvent) => {
      if (e.key === 'Enter') {
        sendMessage(inputRawValue.value);
        if (editorRef.value) {
          editorRef.value.textContent = '';
        }
      }
    };




    onMounted(() => {
      if (editorRef.value) {
        editorRef.value.textContent = inputRawValue.value || '';
      }
    });


    return () =>
      h('div',
        {
          style: {
            flex: 1,
            border: '1px solid #d9d9d9',
            borderRadius: '6px',
            padding: '8px 12px',
            minHeight: '32px',
            maxHeight: '120px',
            overflow: 'auto',
          },
        },
        h('div',
          {
            ref: editorRef,
            contentEditable: true,
            style: {
              outline: 'none',
              minHeight: '20px',
              lineHeight: '20px',
            },
            onInput: handleInput,
            onKeydown: handleKeyDown,
          },
        ),
      );
  },
});
</script>
```
Overview


MessageInput is a complete message input component designed for Vue3 applications, providing core chat input features including text editing, emoji selection, file attachments, and a send button. It supports various custom options, such as input behavior configuration, toolbar customization, component replacement, and slot expansion, meeting the demands of different chat scenarios with personalized requirements.


Basic Usage


```ts
<script>
import { MessageInput } from "@tencentcloud/chat-uikit-vue3";
</script>


<template>
  <MessageInput />
</template>
```


## Props Configuration


| Field | Type | Default | Description |
|------|------|--------|------|
| autoFocus | boolean | true | Whether to auto-focus into the input box |
| disabled | boolean | false | Whether to disable the input component |
| hideSendButton | boolean | false | Whether to hide the send button |
| placeholder | string | '' | Placeholder text for the input box |
| attachmentPickerMode | 'collapsed' \| 'expanded' | 'collapsed' | Attachment selector display mode |
| actions | MessageInputActions | ['EmojiPicker', 'ImagePicker', 'FilePicker', 'VideoPicker'] | Toolbar action button configuration |




## Slots configuration


| Field | Type | Default | Description |
|------|------|--------|------|
| headerToolbar | () => VNode[] | undefined | Header toolbar slot |
| footerToolbar | () => VNode[] | undefined | Footer toolbar slot |
| leftInline | () => VNode[] | undefined | Left inline slot |
| rightInline | () => VNode[] | undefined | Right inline slot |
| inputPrefix | () => VNode[] | undefined | Input box prefix slot |
| inputSuffix | () => VNode[] | undefined | Input box suffix slot |
| TextEditor | Component \| null | null | Custom text editor component configuration |




type definition
``` typescript
type BuiltInAction =
  | 'EmojiPicker'
  | 'ImagePicker'
  | 'FilePicker'
  | 'VideoPicker'
  | 'AttachmentPicker';


export type CustomAction = {
  key: string;
  label?: string | undefined;
  component?: Component | undefined;
  className?: string | undefined;
  style?: CSSProperties | undefined;
  iconSize?: number | undefined;
};


export type MessageInputActions = Array<BuiltInAction | CustomAction>;


export type MessageInputAttachmentPickerMode = 'collapsed' | 'expanded';


export interface MessageInputSlots {
  headerToolbar?: () => VNode[];
  footerToolbar?: () => VNode[];
  leftInline?: () => VNode[];
  rightInline?: () => VNode[];
  inputPrefix?: () => VNode[];
  inputSuffix?: () => VNode[];
  textEditor?: () => VNode[];
}


// MessageInputProps API definition
export interface MessageInputProps {
  autoFocus?: boolean;
  disabled?: boolean;
  hideSendButton?: boolean;
  placeholder?: string;
  attachmentPickerMode?: MessageInputAttachmentPickerMode;
  actions?: MessageInputActions;
  slots?: MessageInputSlots;
  TextEditor?: Component | null;
}
```


Custom Function Explanation


### autoFocus
-boolean


- Details: autoFocus is used to set whether to auto-focus into the input box when mounting. Default: `true`.




### disabled
-boolean


- Details: disabled is used to set whether to disable the entire input component, including text input and ALL buttons. Default: `false`.




### hideSendButton
-boolean


- Details: hideSendButton is used to set whether to hide the send button, suitable for scenarios where the trigger mode needs to be customized. Default: `false`.




### placeholder
- Type: string.


- Details: placeholder is used to set the placeholder text for the input box. Default is an empty string.




### attachmentPickerMode
- Type: 'collapsed' | 'expanded'.


- Details: attachmentPickerMode is used to set the display mode of the attachment selector. Default is `'collapsed'`.


  - **collapsed**: Collapse mode. Unfold options after clicking.


  - **expanded**: Expand mode. Direct display of ALL options.




### actions
- Type: MessageInputActions.


- Description: actions for configuration of buttons displayed in the toolbar. Default: `['EmojiPicker', 'ImagePicker', 'FilePicker', 'VideoPicker']`.




#### Example 1: Custom toolbar button sequence
``` typescript
<template>
  <MessageInput :actions="customActions" />
</template>


<script lang="ts" setup>
import { MessageInput } from '@tencentcloud/uikit-component-vue3';


Custom button sequence: file, image, video, emoji
const customActions = ['FilePicker', 'ImagePicker', 'VideoPicker', 'EmojiPicker'];
</script>
```


#### Example 2: Add custom action button
``` typescript
<template>
  <MessageInput :actions="customActions" />
</template>


<script lang="ts" setup>
import { defineComponent, h } from 'vue';
import { MessageInput } from '@tencentcloud/uikit-component-vue3';


Custom Position Sharing Button Component
const LocationPicker = defineComponent({
  name: 'LocationPicker',
  setup() {
    const handleLocationShare = () => {
      Get user location and send
      if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition((position) => {
          const { latitude, longitude } = position.coords;
          console.log(`Share location: ${latitude}, ${longitude}`);
          alert(`Share location: ${latitude}, ${longitude}`); // For demonstration
        });
      } else {
        alert('Browser not supported for geolocation.');
      }
    };


    return () =>
      h('button',
        {
          onClick: handleLocationShare,
          style: { padding: '4px 8px', border: 'none', background: 'transparent' },
          Share location
        },
        '📍',
      );
  },
});


const customActions = [
  'EmojiPicker',
  'ImagePicker',
  {
    key: 'location',
    label: 'Location',
    component: LocationPicker,
  },
  'AttachmentPicker',
];
</script>
```


#### Example 3: Quick reply in customer service system
``` typescript
<template>
  <MessageInput :actions="actions" />
</template>


<script lang="ts" setup>
import { defineComponent, h, ref } from 'vue';
import { MessageInput } from '@tencentcloud/uikit-component-vue3';
import { useMessageInputState } from '@tencentcloud/uikit-component-vue3/src/states/MessageInputState';


quick reply component
const QuickReplyPicker = defineComponent({
  name: 'QuickReplyPicker',
  setup() {
    const { setContent } = useMessageInputState();
    const showPicker = ref(false);


    const quickReplies = [
      Hello, glad to help you.
      Please wait a moment, I'll check for you...
      Thank you for your consultation. Also, any other issues?
      The issue has been resolved. Have a pleasant life.
    ];


    const handleQuickReply = (text: string) => {
      setContent(text);
      showPicker.value = false;
    };


    return () =>
      h('div', { style: { position: 'relative' } }, [
        h('button',
          {
            title: 'Quick reply',
            onClick: () => (showPicker.value = !showPicker.value),
          },
          '⚡',
        ),
        showPicker.value &&
          h('div',
            {
              style: {
                position: 'absolute',
                bottom: '100%',
                left: 0,
                background: 'white',
                border: '1px solid #ccc',
                borderRadius: '4px',
                padding: '8px',
                minWidth: '200px',
                zIndex: 100, // Ensure it's above other elements
              },
            },
            quickReplies.map((reply, index) =>
              h('div',
                {
                  key: index,
                  onClick: () => handleQuickReply(reply),
                  style: {
                    padding: '4px 8px',
                    cursor: 'pointer',
                    borderRadius: '2px',
                    '&:hover': { backgroundColor: '#f0f0f0' },
                  },
                },
                reply,
              ),
            ),
          ),
      ]);
  },
});


const actions = [
  {
    key: 'quickReply',
    label: 'Quick reply',
    component: QuickReplyPicker,
  },
  'EmojiPicker',
  'FilePicker',
];
</script>
```




#### Example 4: Custom emoji panel
``` typescript
<template>
  <MessageInput :EmojiPicker="CustomEmojiPicker" />
</template>




<script lang="ts" setup>
import { defineComponent, h, ref } from 'vue';
import { MessageInput } from '@tencentcloud/uikit-component-vue3';
import { useMessageInputState } from '@tencentcloud/uikit-component-vue3/src/states/MessageInputState';




const CustomEmojiPicker = defineComponent({
  name: 'CustomEmojiPicker',
  setup() {
    const { insertContent } = useMessageInputState();
    const showPicker = ref(false);
    const activeCategory = ref('common');




    const emojiCategories = {
      'common': ['😀', '😂', '🥰', '😍', '🤔', '😭', '😡', '👍'],
      'hand': ['👋', '🤝', '👏', '🙏', '✌️', '🤞', '🤟', '👌'],
      'animal': ['🐶', '🐱', '🐭', '🐹', '🐰', '🦊', '🐻', '🐼'],
    };




    const insertEmoji = (emoji: string) => {
      insertContent(emoji);
      showPicker.value = false;
    };




    return () =>
      h('div', { style: { position: 'relative' } }, [
        h('button',
          {
            onClick: () => (showPicker.value = !showPicker.value),
            style: { border: 'none', background: 'transparent', cursor: 'pointer' },
          },
          '😊',
        ),
        showPicker.value &&
          h('div',
            {
              style: {
                position: 'absolute',
                bottom: '100%',
                left: 0,
                background: 'white',
                border: '1px solid #ccc',
                borderRadius: '8px',
                padding: '12px',
                width: '280px',
                boxShadow: '0 4px 12px rgba(0,0,0,0.1)',
                zIndex: 100, // Ensure it's above other elements
              },
            },
            [
              category tag
              h('div', { style: { display: 'flex', marginBottom: '8px' } },
                Object.keys(emojiCategories).map((category) =>
                  h('button',
                    {
                      key: category,
                      onClick: () => (activeCategory.value = category),
                      style: {
                        padding: '4px 8px',
                        border: 'none',
                        background: activeCategory.value === category ? '#1890ff' : 'transparent',
                        color: activeCategory.value === category ? 'white' : '#666',
                        borderRadius: '4px',
                        cursor: 'pointer',
                        fontSize: '12px',
                      },
                    },
                    category,
                  ),
                ),
              ),
              emoji grid
              h('div',
                {
                  style: {
                    display: 'grid',
                    gridTemplateColumns: 'repeat(8, 1fr)',
                    gap: '4px',
                  },
                },
                emojiCategories[activeCategory.value].map((emoji) =>
                  h('button',
                    {
                      key: emoji,
                      onClick: () => insertEmoji(emoji),
                      style: {
                        border: 'none',
                        background: 'transparent',
                        fontSize: '20px',
                        cursor: 'pointer',
                        padding: '4px',
                        borderRadius: '4px',
                      },
                    },
                    emoji,
                  ),
                ),
              ),
            ],
          ),
      ]);
  },
});
</script>
```


## Slots explanation
- Type: MessageInputSlots.


-Detailed instructions: Insert custom content at a specific location in the input component.


   ``` typescript
   interface MessageInputSlots {
     headerToolbar?: () => VNode[];
     footerToolbar?: () => VNode[];
     leftInline?: () => VNode[];
     rightInline?: () => VNode[];
     inputPrefix?: () => VNode[];
     inputSuffix?: () => VNode[];
     textEditor?: () => VNode[];
   }
   ```




#### Example 1: Custom footerToolbar slot
``` typescript
<template>
  <MessageInput>
    <template #footerToolbar>
      <div style="padding: 4px 12px; font-size: 12px; color: #999; text-align: right;">
        press Ctrl+Enter to wrap
      </div>
    </template>
  </MessageInput>
</template>
```




#### Example 2: Input box prefix/suffix feature
``` typescript
<template>
  <MessageInput>
    <template #inputPrefix>
      
    </template>
    <template #inputSuffix>
      <button
        style="border: none; background: transparent; cursor: pointer;"
        @click="handleVoiceInput"
      >
        🎤
      </button>
    </template>
  </MessageInput>
</template>


<script lang="ts" setup>
import { MessageInput } from '@tencentcloud/uikit-component-vue3';


const handleAtUser = () => {
  Trigger @user selection
  console.log('Toggle on @user selection');
};


const handleVoiceInput = () => {
  // Start voice input
  console.log('Start voice input');
};
</script>
```




### TextEditor


Type: 'Component' | 'null'.


Detailed explanation: TextEditor is used to replace the default text editor component. Default: `null`.


#### Example: Custom text editor
``` typescript
<template>
  <MessageInput>
    <template #textEditor>
      <RichTextEditor />
    </template>
  </MessageInput>
</template>




<script lang="ts" setup>
import { defineComponent, h, ref, onMounted } from 'vue';
import { MessageInput } from '@tencentcloud/uikit-component-vue3';
import { useMessageInputState } from '@tencentcloud/uikit-component-vue3/src/states/MessageInputState';




const RichTextEditor = defineComponent({
  name: 'RichTextEditor',
  setup() {
    const { sendMessage } = useMessageInputState();
    const editorRef = ref<HTMLDivElement | null>(null);
    const inputRawValue = ref('');


    const handleInput = (e: Event) => {
      const target = e.target as HTMLDivElement;
      inputRawValue.value = (e.target as HTMLDivElement).textContent || '';
    };




    const handleKeyDown = (e: KeyboardEvent) => {
      if (e.key === 'Enter') {
        sendMessage(inputRawValue.value);
        if (editorRef.value) {
          editorRef.value.textContent = '';
        }
      }
    };




    onMounted(() => {
      if (editorRef.value) {
        editorRef.value.textContent = inputRawValue.value || '';
      }
    });


    return () =>
      h('div',
        {
          style: {
            flex: 1,
            border: '1px solid #d9d9d9',
            borderRadius: '6px',
            padding: '8px 12px',
            minHeight: '32px',
            maxHeight: '120px',
            overflow: 'auto',
          },
        },
        h('div',
          {
            ref: editorRef,
            contentEditable: true,
            style: {
              outline: 'none',
              minHeight: '20px',
              lineHeight: '20px',
            },
            onInput: handleInput,
            onKeydown: handleKeyDown,
          },
        ),
      );
  },
});
</script>
```


