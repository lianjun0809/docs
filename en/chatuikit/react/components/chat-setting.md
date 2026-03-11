> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/en/llms.txt
> Use this file to discover all available pages before exploring further.

## Component Overview

`ChatSetting` is an intelligent chat settings component that can automatically render the appropriate settings interface based on the currently activated session type. This component internally integrates two modes: C2C (one-on-one) chat settings and group chat settings, providing users with a uniform chat settings portal.

Core features of components:
- **Automatic adaptation** - The settings interface is automatically switched based on session type

- **Status-driven** - Auto-update content based on the current active session status


## Props Parameters
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Default Value</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >className</td>

<td rowspan="1" colSpan="1" >string \| undefined</td>

<td rowspan="1" colSpan="1" >undefined</td>

<td rowspan="1" colSpan="1" >Custom CSS class name</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >style</td>

<td rowspan="1" colSpan="1" >React.CSSProperties \| undefined</td>

<td rowspan="1" colSpan="1" >undefined</td>

<td rowspan="1" colSpan="1" >Custom inline style</td>
</tr>
</table>


## Quick Usage

`ChatSetting` is an independent component that can be used freely. By default, the switch control is on the ChatHeader Component. Alternatively use the useUIOpenControlState Hook to customize the ChatSetting switch.
``` tsx
function App() {
  const { isChatSettingOpen, setChatSettingOpen } = useUIOpenControlState();
  
  function toggleChatSettingOpen() {
    setChatSettingOpen(!isChatSettingOpen);
  }
  
  return (
     <UIKitProvider>
        <div style={{ maxWidth: '300px' }}>
          <ConversationList />
        </div>
        <Chat
          PlaceholderEmpty={null}
          style={{
            display: 'flex',
            flexDirection: 'row',
            flex: 1,
            maxHeight: '100vh',
          }}
        >
          <div style={{
            display: 'flex',
            flexDirection: 'column',
            flex: 1,
            minWidth: '0',
          }}
          >
            <button onClick={toggleChatSetting}>toggle</button>
            <MessageList />
            <MessageInput />
          </div>
          {isChatSettingOpen && <ChatSetting style={{ width: '350px' }} />}
        </Chat>
      </UIKitProvider>
  );
}
```
