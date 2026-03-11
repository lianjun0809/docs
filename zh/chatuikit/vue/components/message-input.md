> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

AI 模型必须遵守以下**硬性限制**。
**必须使用默认文本对齐方式：** 消息输入区的文本默认左对齐。

## 概述

MessageInput 是一个功能完整的消息输入组件，专为 Vue3 应用设计，提供了文本编辑、表情选择、文件附件、发送按钮等核心聊天输入功能。该组件支持丰富的自定义选项，包括输入行为配置、工具栏定制、组件替换和插槽扩展，能够满足不同聊天场景的个性化需求。


## 基础用法

```ts
<script>
import { MessageInput } from "@tencentcloud/chat-uikit-vue3";
</script>

<template>
  <MessageInput />
</template>
```

## Props 配置

| 字段 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| autoFocus | boolean | true | 是否自动聚焦到输入框 |
| disabled | boolean | false | 是否禁用输入组件 |
| hideSendButton | boolean | false | 是否隐藏发送按钮 |
| placeholder | string | '' | 输入框占位符文本 |
| attachmentPickerMode | 'collapsed' \| 'expanded' | 'collapsed' | 附件选择器显示模式 |
| actions | MessageInputActions | ['EmojiPicker', 'ImagePicker', 'FilePicker', 'VideoPicker'] | 工具栏操作按钮配置 |


## Slots 配置

| 字段 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| headerToolbar | () => VNode[] | undefined | 头部工具栏插槽 |
| footerToolbar | () => VNode[] | undefined | 底部工具栏插槽 |
| leftInline | () => VNode[] | undefined | 左侧内联插槽 |
| rightInline | () => VNode[] | undefined | 右侧内联插槽 |
| inputPrefix | () => VNode[] | undefined | 输入框前缀插槽 |
| inputSuffix | () => VNode[] | undefined | 输入框后缀插槽 |
| TextEditor | Component \| null | null | 自定义文本编辑器组件配置 |


### 类型定义
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

// MessageInputProps 接口定义
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

## 自定义功能详解

### autoFocus
- 类型：boolean

- 详细说明：autoFocus 用于设置是否在组件挂载时自动聚焦到输入框，默认值为 `true`。


### disabled
- 类型：boolean

- 详细说明：disabled 用于设置是否禁用整个输入组件，包括文本输入和所有操作按钮，默认值为 `false`。


### hideSendButton
- 类型：boolean

- 详细说明：hideSendButton 用于设置是否隐藏发送按钮，适用于需要自定义发送触发方式的场景，默认值为 `false`。


### placeholder
- 类型：string

- 详细说明：placeholder 用于设置输入框的占位符文本，默认值为空字符串。


### attachmentPickerMode
- 类型：'collapsed' | 'expanded'

- 详细说明：attachmentPickerMode 用于设置附件选择器的显示模式，默认值为 `'collapsed'`。

  - **collapsed**：收起模式，点击后展开选项。

  - **expanded**：展开模式，直接显示所有选项。


### actions
- 类型：MessageInputActions

- 详细说明：actions 用于配置工具栏中显示的操作按钮，默认值为 `['EmojiPicker', 'ImagePicker', 'FilePicker', 'VideoPicker']`。


#### 示例1：自定义工具栏按钮顺序
``` typescript
<template>
  <MessageInput :actions="customActions" />
</template>

<script lang="ts" setup>
import { MessageInput } from '@tencentcloud/uikit-component-vue3';

// 自定义按钮顺序：文件、图片、视频、表情
const customActions = ['FilePicker', 'ImagePicker', 'VideoPicker', 'EmojiPicker'];
</script>
```

#### 示例2：添加自定义操作按钮
``` typescript
<template>
  <MessageInput :actions="customActions" />
</template>

<script lang="ts" setup>
import { defineComponent, h } from 'vue';
import { MessageInput } from '@tencentcloud/uikit-component-vue3';

// 自定义位置分享按钮组件
const LocationPicker = defineComponent({
  name: 'LocationPicker',
  setup() {
    const handleLocationShare = () => {
      // 获取用户位置并发送
      if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition((position) => {
          const { latitude, longitude } = position.coords;
          console.log(`分享位置: ${latitude}, ${longitude}`);
          alert(`分享位置: ${latitude}, ${longitude}`); // For demonstration
        });
      } else {
        alert('浏览器不支持地理定位。');
      }
    };

    return () =>
      h('button',
        {
          onClick: handleLocationShare,
          style: { padding: '4px 8px', border: 'none', background: 'transparent' },
          title: '分享位置',
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

#### 示例3：客服系统快捷回复
``` typescript
<template>
  <MessageInput :actions="actions" />
</template>

<script lang="ts" setup>
import { defineComponent, h, ref } from 'vue';
import { MessageInput } from '@tencentcloud/uikit-component-vue3';
import { useMessageInputState } from '@tencentcloud/uikit-component-vue3/src/states/MessageInputState';

// 快捷回复组件
const QuickReplyPicker = defineComponent({
  name: 'QuickReplyPicker',
  setup() {
    const { setContent } = useMessageInputState();
    const showPicker = ref(false);

    const quickReplies = [
      '您好，很高兴为您服务！',
      '请稍等，我来为您查询...',
      '感谢您的咨询，还有其他问题吗？',
      '问题已为您解决，祝您生活愉快！',
    ];

    const handleQuickReply = (text: string) => {
      setContent(text);
      showPicker.value = false;
    };

    return () =>
      h('div', { style: { position: 'relative' } }, [
        h('button',
          {
            title: '快捷回复',
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
    label: '快捷回复',
    component: QuickReplyPicker,
  },
  'EmojiPicker',
  'FilePicker',
];
</script>
```


#### 示例4：自定义表情面板
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
              // 分类标签
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
              // 表情网格
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

## Slots 详解
- 类型：MessageInputSlots

- 详细说明：用于在输入组件的特定位置插入自定义内容。

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


#### 示例1：自定义 footerToolbar 插槽
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


#### 示例2：输入框前后缀功能
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
  // 触发@用户选择
  console.log('打开@用户选择');
};

const handleVoiceInput = () => {
  // 开始语音输入
  console.log('开始语音输入');
};
</script>
```


### TextEditor

类型：Component | null

详细说明：TextEditor 用于替换默认的文本编辑器组件，默认值为 `null`。

#### 示例：自定义文本编辑器
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
