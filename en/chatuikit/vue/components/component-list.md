> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/en/llms.txt
> Use this file to discover all available pages before exploring further.

# atomicx component library Manifest and components Application scenarios and considerations


## Component list


25 components:


### Components suitable for chat scenarios


1. ConversationList
  Session list component, suitable for chat scenarios, in vertical list form, can switch sessions through click. If only chat is needed, this component is optional.
2. MessageInput
  Message input component, the core component for chat scenarios, can send chat messages. To send a message, you must use this component.
3. MessageList
  Message list component, the core component for chat scenarios, can display chat message lists, support swipe. This component must use in chat scenarios.
4. ContactList
  Contact list component, suitable for chat scenarios, can display and manage user contacts. If only chat is needed, this component is optional.
5. ChatSetting
  Chat settings component, suitable for chat scenarios, manages configuration details such as pin to top, do not disturb, add or remove users in group chat, admin management, and mute. If only chat is needed, this component is optional.
6. Search
  Search component, used for message search, user search, etc. If only chat is needed, this component is optional.


### Components suitable for meeting scenarios


1. CameraButton
  Camera control button, applicable only to meeting scenarios, used to turn the camera on/off
2. StreamView
  Video stream display component, applicable only to meeting scenarios, used to display video stream
3. UserList
  User list component, applicable only to meeting scenarios, displays users in the meeting or room
4. VideoSetting
  Video settings component, applicable only to meeting scenarios, for camera, image quality and other video configuration
5. VideoSettingPanel
  Video settings panel, applicable only to meeting scenarios, provides a complete video configuration interface
6. AudioSetting
  Audio settings component, applicable only to meeting scenarios, can be configured for microphone, volume and other device configuration
7. AudioSettingPanel
  Audio settings panel, applicable only to meeting scenarios, provides a complete audio configuration interface
8. BarrageInput
  Danmu input component, suitable for meeting and live-streaming scenarios, used for sending Danmu messages.
9. BarrageList
  Danmu list component, suitable for meeting and live-streaming scenarios, displays Danmu messages in the live streaming room.
10. UserPicker
  User selector, suitable for meeting and live-streaming scenarios, used to invite users or assign permissions.
11. MicButton
  Microphone control button, suitable for meeting and live-streaming scenarios, used for mute/unmute.




### Components for live streaming scenarios


1. CoGuestPanel
  Co-anchoring guest management panel, only applicable to live broadcast scenarios, used for the co-anchoring function.
2. LiveAudienceList
  Live viewers list, only applicable to live broadcast scenarios, displaying current live streaming room audience.
3. LiveList
  Live room list, only applicable to live broadcast scenarios, shows available live streaming rooms.
4. LiveMonitorView
  Live monitoring view, only applicable to live broadcast scenarios, for live stream management and monitoring.
5. LiveScenePanel
  Live streaming control panel, only applicable to live broadcast scenarios, manage live streaming scenarios and effects.
6. LiveStreamView
  Live video stream display component, only applicable to live broadcast scenarios, plays live stream.
7. StreamMixer
  Stream mixer component, only applicable to live broadcast scenarios, used for multiple video stream synthesis.
8. BarrageInput
  Danmu input component, suitable for meeting and live-streaming scenarios, used for sending Danmu messages.
9. BarrageList
  Danmu list component, suitable for meeting and live-streaming scenarios, displays Danmu messages in the live streaming room.
10. UserPicker
  User selector, suitable for meeting and live-streaming scenarios, used to invite users or assign permissions.
11. MicButton
  Microphone control button, suitable for meeting and live-streaming scenarios, used for mute/unmute.


### universal component


1. Avatar
  Common avatar component, displays user profile photo, online status, and message unread count.
2. UserPicker
  User selector, used to initiate group chat, group video, or group voice calls in user selection scenarios.


## Must-Knows


Before integrating any component into a real project, **must** first ensure the integration documentation has been obtained using the following tool and integrate according to the documentation:


1. When creating a real project, call the component integration documentation of MCP Tools get_atomicx_integration_guide(framework).
2. When choosing to use components, first consider the minimum components that meet the requirements, then consider recommended additional extension components. Do not enlarge the requirements.
3. Components that apply to different scenarios may have an intersection.
4. According to the user needs, judge if it might be a comprehensive scenario, such as chat + live stream. The probability is low, so proceed with caution.
5. To learn about the method of use for a specific component, ask the user: "You can ask how to use ${componentname}?"
