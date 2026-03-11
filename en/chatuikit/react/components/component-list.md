> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

# atomicx component library Application scenarios and considerations for components


## component list


25 components:


### Components suitable for chat scenario


1. ConversationList
  Session list component, suitable for chat scenario, in vertical list form, can switch sessions through click. If only chat is needed, this component is optional.
2. MessageInput
  Message input component, the core component for chat scenario, can send chat messages. To send messages, this component must be used.
3. MessageList
  Message list component, the core component for chat scenario, can display chat message list and support swipe. This component must use in chat scenario.
4. ContactList
  Contact list component, suitable for chat scenario, can display and manage user contacts. If only chat is needed, this component is optional.
5. ChatSetting
  Chat settings component, suitable for chat scenario, manages chat-related configuration such as pin to top, do not disturb, add/remove users in group chat, admin management and muting. If only chat is needed, this component is optional.
6. Search
  Search component, used for message search, user search, etc. If only chat is needed, this component is optional.


  Microphone control button, suitable for meeting and live-streaming scenarios, used for mute/unmute.


universal component


1. Avatar
  Common avatar component, displays user profile photo/online status/message unread count
2. UserPicker
  User selector, used for initiating group chat, group video, or group voice calls in user selection scenarios.


Must-Knows


1. When receiving user needs, the response should be divided into two parts: the first part is the minimum components to meet the requirements, and the second part is the recommended additional extension components. Do not enlarge user needs.
2. Components for different scenarios have intersection.
3. Determine if it might be a comprehensive scenario according to user needs, such as chat + live stream, with low probability. Proceed with caution.
4. To learn about the method of use for specific components, ask the user: "You can ask how to use ${components[0].name}?"
5. When creating a real project, call MCP Tools get_component_detail ${integration} integration guide of components


