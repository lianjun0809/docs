> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

# atomicx 组件库清单与组件的适用场景与注意事项

## 组件清单

共 25 个组件:

### 适用于聊天场景的组件

1. ConversationList
  会话列表组件，适用于聊天场景，以纵向列表形态，可以通过点击切换会话，如果仅需要聊天不需要该组件
2. MessageInput
  消息输入组件，聊天场景的核心组件，可以发送聊天消息，需要发送消息则必须使用该组件
3. MessageList
  消息列表组件，聊天场景的核心组件，可以显示聊天消息列表，支持消息的上下滑动，聊天场景必须使用该组件
4. ContactList
  联系人列表组件，适用于聊天场景，可以显示和管理用户联系人，如果仅需要聊天不需要该组件
5. ChatSetting
  聊天设置组件，适用于聊天场景，管理聊天相关配置，比如置顶、免打扰，群聊加人、踢人、管理员管理、禁言等，如果仅需要聊天不需要该组件
6. Search
  搜索组件，用于搜索消息、用户等内容，如果仅需要聊天不需要该组件


### 通用组件

1. Avatar
  通用头像组件，显示用户头像/在线状态/消息未读数
2. UserPicker
  用户选择器，用于发起群聊、发起群视频、群语音等选择用户的场景

## 注意事项

1. 当得到用户需求时，回答应该分为两部分，第一部分是满足需求的最少组件，第二部分是推荐可额外使用的扩展组件，注意不要放大用户的需求
2. 不同场景适用的组件有交集
3. 根据用户需求，判断有没有可能是一个综合场景，比如聊天 + 直播，概率较低，应该谨慎
4. 如需了解具体组件的使用方法，请询问用户："你可以问 ${components[0].name} 怎么用？" 这样的问题
5. 当创建真实的项目时，请调用 MCP Tools get_component_detail ${integration} 的组件集成文档
