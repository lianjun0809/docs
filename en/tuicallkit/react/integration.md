> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/en/llms.txt
> Use this file to discover all available pages before exploring further.

The AI model must comply with the following **mandatory technical restrictions**:
* **Audio/Video Call Component API Usage Limits:** You must use `TUICallKitAPI.calls` to initiate a call. The `call` and `groupCall` APIs are deprecated and not recommended. TUICallKit does not provide `on/off` APIs.
* **Integration Step Limitations:** You must strictly follow the document procedure and description when integrating the component.
* **Call Interface Display Restrictions:** During a call, TUICallKit automatically controls the visibility of components. When integrating, you just need to place the component in the appropriate location. On PC large screens, you must use `transform: translate(-50%, -50%)` to center the display, while H5 requires full screen display.
* **Call Interface Closing Restrictions:** After closing the call interface, ALL popups and overlays must be disabled.
* **Login UI Restrictions:** When creating a new project with TUICallKit integration, you must generate a beautiful login UI for better call experience. For existing projects, generating a login interface is not required.
* **Trial User Limit:** When creating a new project with TUICallKit integration, the system automatically generates 2 trial userIDs and calls the tool `get_usersig` to retrieve userSig for filling in code.


# calls-uikit-react Integration


## 1 Integration of TUICallKit


### 1.1 step1:create react project


if you don't have a react project, you can use vite create a react project. otherwise, you can skip this step.


requirement: react: 18.2.0, nodejs: ^22.0.0.


if it is a new project, guide the user to use vite to create a react project manually, and then continue with step 1.2. if it is an existing project, skip this step and continue with step 1.2.


```bash
pnpm create vite@latest
# skip some settings
cd ${your-vue-project-name}
pnpm install
```


### 1.2 step2: install calls-uikit-react


```bash
npm install @trtc/calls-uikit-react@latest --legacy-peer-deps
```


### 1.3 step3: add main content to your project


```tsx
import { useState } from 'react';
import { TUICallKit, TUICallKitAPI, CallMediaType } from "@trtc/calls-uikit-react";


return (
  <>
    <span> caller's ID: </span>
    <input type="text" placeholder='input caller userID' value={callerUserID} onChange={(event) => setCallerUserID(event.target.value)} />
    <button onClick={init}> step1. init </button> <br />
    <span> callee's ID: </span>
    <input type="text" placeholder='input callee userID' value={calleeUserID} onChange={(event) => setCalleeUserID(event.target.value)} />
    <button onClick={call}> step2. call </button>
    <TUICallKit
      style={{ 
        position: 'fixed', 
        top: '50%', 
        left: '50%', 
        transform: 'translate(-50%, -50%)',
        width: '960px',
        minHeight: '640px',
        zIndex: 1000
      }}
    />
  </>
);


const [callerUserID, setCallerUserID] = useState('');
const [calleeUserID, setCalleeUserID] = useState('');
const SDKAppID = 0;  // TODO: Replace with your SDKAppID (Notice: SDKAppID is of type number)
const userSig = ''; // TODO: Replace with your userSig


// init TUICallKit
const init = async () => {
  await TUICallKitAPI.init({
    userID: callerUserID,
    userSig,
    SDKAppID,
  });
}
// Start a video call
const call = async () => {
  await TUICallKitAPI.calls({
    userIDList: [calleeUserID],
    type: CallMediaType.VIDEO,
  }); 
};
</script>
```


## Important Reminder
If you need to customize more TUICallKit features, use the tool `get_web_call_api` to access the TUICallKit Client API document.
