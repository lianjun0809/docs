> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/en/llms.txt
> Use this file to discover all available pages before exploring further.

## Important Notice

**Documentation Content Description:**
- The documentation covers two parts: `TUICallEngine` API and `TUICallKit` UI component API.
- For `TUICallEngine` API documentation, please refer to **Part One**
- For `TUICallKit` UI component API documentation, please refer to **Part Two**

---

## Part One: TUICallEngine API Documentation

**TUICallEngine API Overview**
- When users query `TUICallEngine` API, you must first consult the official TUICallEngine API documentation, then provide correct API usage examples. **Do not speculate on API usage.**
- Below are the documentation links for each platform. Please access the documentation links directly to obtain API usage:
  - [TUICallEngine Web API List Documentation](https://trtc.io/document/51016?product=call&menulabel=uikit&platform=web)
  - [TUICallEngine Web API Usage Examples Documentation](https://web.sdk.qcloud.com/component/trtccalling/doc/TUICallEngine/web/en/TUICallEngine.html)

---

## Part Two: TUICallKit UI Component API Documentation

The TUICallKit API is the **audio and video call component that includes a UI interface**. With the TUICallKit API, you can swiftly develop audio and video call scenarios reminiscent of WeChat through simple interfaces. For further comprehensive steps to access this, please refer to: [Integrating TUICallKit](https://trtc.io/document/50993).

## API Overview
<table>
<tr>
<td rowspan="1" colSpan="1" >API</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[<TUICallKit/>](https://www.tencentcloud.com/document/product/647/51015#TUICallKit)</td>

<td rowspan="1" colSpan="1" >The core UI call component.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[init](https://www.tencentcloud.com/document/product/647/51015#init)</td>

<td rowspan="1" colSpan="1" >Initialize TUICallKit.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[calls](https://www.tencentcloud.com/document/product/647/51015#calls)</td>

<td rowspan="1" colSpan="1" >Initiate a one-to-one or multi-person call.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[join](https://www.tencentcloud.com/document/product/647/51015#join)</td>

<td rowspan="1" colSpan="1" >Proactively join a call.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setCallingBell](https://www.tencentcloud.com/document/product/647/51015#setCallingBell)</td>

<td rowspan="1" colSpan="1" >Customize user's ringtone.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setSelfInfo](https://www.tencentcloud.com/document/product/647/51015#setSelfInfo)</td>

<td rowspan="1" colSpan="1" >Set your own nickname and avatar.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[enableMuteMode](https://www.tencentcloud.com/document/product/647/51015#enableMuteMode)</td>

<td rowspan="1" colSpan="1" >Turn on/off ringtone.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[enableFloatWindow](https://www.tencentcloud.com/document/product/647/51015#enableFloatWindow)</td>

<td rowspan="1" colSpan="1" >Turn on/off the floating window function.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[enableVirtualBackground](https://www.tencentcloud.com/document/product/647/51015#enableVirtualBackground)</td>

<td rowspan="1" colSpan="1" >Turn on/off the blurred background function button.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setLanguage](https://www.tencentcloud.com/document/product/647/51015#setLanguage)</td>

<td rowspan="1" colSpan="1" >Set the call language for the TUICallKit component.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[hideFeatureButton](https://www.tencentcloud.com/document/product/647/51015#hideFeatureButton)</td>

<td rowspan="1" colSpan="1" >Hidden Button.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setLocalViewBackgroundImage](https://www.tencentcloud.com/document/product/647/51015#setLocalViewBackgroundImage)</td>

<td rowspan="1" colSpan="1" >Set the background image for the local user's call interface.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setRemoteViewBackgroundImage](https://www.tencentcloud.com/document/product/647/51015#setRemoteViewBackgroundImage)</td>

<td rowspan="1" colSpan="1" >Set the background image for the remote user's call interface.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setLayoutMode](https://www.tencentcloud.com/document/product/647/51015#setLayoutMode)</td>

<td rowspan="1" colSpan="1" >Set the call interface layout mode.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setCameraDefaultState](https://www.tencentcloud.com/document/product/647/51015#setCameraDefaultState)</td>

<td rowspan="1" colSpan="1" >et whether the camera is opened by default.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[destroyed](https://www.tencentcloud.com/document/product/647/51015#destroyed)</td>

<td rowspan="1" colSpan="1" >Destroy TUICallKit.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getTUICallEngineInstance](https://www.tencentcloud.com/document/product/647/51015#getTUICallEngineInstance)</td>

<td rowspan="1" colSpan="1" >Get TUICallEngine instance.</td>
</tr>
</table>


## `<TUICallKit/>` attributes

### Attribute Overview
<table>
<tr>
<td rowspan="1" colSpan="1" >Attribute</td>

<td rowspan="1" colSpan="1" >Description</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Required</td>

<td rowspan="1" colSpan="1" >Default Value</td>

<td rowspan="1" colSpan="1" >Vue</td>

<td rowspan="1" colSpan="1" >React</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >allowedMinimized</td>

<td rowspan="1" colSpan="1" >Is the floating window permitted?</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >No</td>

<td rowspan="1" colSpan="1" >false</td>

<td rowspan="1" colSpan="1" ><br>√</td>

<td rowspan="1" colSpan="1" >√</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >allowedFullScreen</td>

<td rowspan="1" colSpan="1" >Whether to permit full screen mode for the call interface</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >No</td>

<td rowspan="1" colSpan="1" >true</td>

<td rowspan="1" colSpan="1" >√</td>

<td rowspan="1" colSpan="1" >√</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[videoDisplayMode](https://www.tencentcloud.com/document/product/647/51015#videoDisplayMode)</td>

<td rowspan="1" colSpan="1" >Display mode for the call interface</td>

<td rowspan="1" colSpan="1" >VideoDisplayMode</td>

<td rowspan="1" colSpan="1" >No</td>

<td rowspan="1" colSpan="1" >VideoDisplayMode.COVER</td>

<td rowspan="1" colSpan="1" >√</td>

<td rowspan="1" colSpan="1" >√</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[videoResolution](https://www.tencentcloud.com/document/product/647/51015#videoResolution)</td>

<td rowspan="1" colSpan="1" >Call Resolution</td>

<td rowspan="1" colSpan="1" >VideoResolution</td>

<td rowspan="1" colSpan="1" >No</td>

<td rowspan="1" colSpan="1" >VideoResolution.RESOLUTION_480P</td>

<td rowspan="1" colSpan="1" >√</td>

<td rowspan="1" colSpan="1" >√</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >beforeCalling</td>

<td rowspan="1" colSpan="1" >This function will be executed prior to making a call and before receiving an invitation to talk</td>

<td rowspan="1" colSpan="1" >function(type, error)</td>

<td rowspan="1" colSpan="1" >No</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >√</td>

<td rowspan="1" colSpan="1" >√</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >afterCalling</td>

<td rowspan="1" colSpan="1" >This function will be executed after the termination of the call</td>

<td rowspan="1" colSpan="1" >function()</td>

<td rowspan="1" colSpan="1" >No</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >√</td>

<td rowspan="1" colSpan="1" >√</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" ><br>onMinimized</td>

<td rowspan="1" colSpan="1" >This function will be executed when the component switches to a minimized state. The explanation for the [STATUS value is](https://write.woa.com/document/95825268984856576)</td>

<td rowspan="1" colSpan="1" >function(oldStatus, newStatus)</td>

<td rowspan="1" colSpan="1" >No</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >√</td>

<td rowspan="1" colSpan="1" >√</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" ><br>kickedOut</td>

<td rowspan="1" colSpan="1" >The events thrown by the component occur when the current logged-in user is ejected. The call will also automatically terminate</td>

<td rowspan="1" colSpan="1" >function()</td>

<td rowspan="1" colSpan="1" >No</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >√</td>

<td rowspan="1" colSpan="1" >×</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" ><br>statusChanged</td>

<td rowspan="1" colSpan="1" >Event thrown by the component; this event is triggered when the call status changes. For detailed types of call status, refer to [STATUS value description](https://write.woa.com/document/95825268984856576)</td>

<td rowspan="1" colSpan="1" >function({oldStatus, newStatus})</td>

<td rowspan="1" colSpan="1" >No</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >√</td>

<td rowspan="1" colSpan="1" >×</td>
</tr>
</table>


### Sample code




【React】
``` bash
import { TUICallKit, VideoDisplayMode, VideoResolution } from "@trtc/calls-uikit-react";

<TUICallKit
    videoDisplayMode={VideoDisplayMode.CONTAIN}
    videoResolution={VideoResolution.RESOLUTION_1080P}
    beforeCalling={handleBeforeCalling} 
    afterCalling={handleAfterCalling} 
/>

function handleBeforeCalling(type: string, error: any) {
  console.log("[TUICallkit Demo] handleBeforeCalling:", type, error);
}
function handleAfterCalling() {
  console.log("[TUICallkit Demo] handleAfterCalling");
}
```


【Vue3】
``` bash
<template>
   <TUICallKit
    :allowedMinimized="true"
    :allowedFullScreen="true"
    :videoDisplayMode="VideoDisplayMode.CONTAIN"
    :videoResolution="VideoResolution.RESOLUTION_1080P"
    :beforeCalling="beforeCalling"
    :afterCalling="afterCalling"
    :onMinimized="onMinimized"
    :kickedOut="handleKickedOut"
    :statusChanged="handleStatusChanged"
  />
</template>
<script lang="ts" setup>
import { TUICallKit, TUICallKitAPI, VideoDisplayMode, VideoResolution, STATUS } from "@trtc/calls-uikit-vue";

function beforeCalling(type: string, error: any) {
  console.log("[TUICallkit Demo] beforeCalling:", type, error);
}
function afterCalling() {
  console.log("[TUICallkit Demo] afterCalling");
}
function onMinimized(oldStatus: string, newStatus: string) {
  console.log("[TUICallkit Demo] onMinimized: " + oldStatus + " -> " + newStatus);
}
function kickedOut() {
  console.log("[TUICallkit Demo] kickedOut");
}
function statusChanged(args: { oldStatus: string; newStatus: string; }) {
  const { oldStatus, newStatus } = args;
  if (newStatus === STATUS.CALLING_C2C_VIDEO) {
    console.log(`[TUICallkit Demo] statusChanged: ${oldStatus} -> ${newStatus}`);
  }
}
</script>
```

## Detailed information on TUICallKitAPI API




【React】
``` javascript
import { TUICallKitAPI } from "@trtc/calls-uikit-react"; 
```


【Vue3】
``` javascript
import { TUICallKitAPI } from "@trtc/calls-uikit-vue"; 
```

### init

Initialize TUICallKit.
``` javascript
try {
  await TUICallKitAPI.init({ SDKAppID, userID, userSig });
  // If you already have a tim instance in your project, you need to pass it in here
  // await TUICallKitAPI.init({ tim, SDKAppID, userID, userSig}); 
  console.log("[TUICallKit] Initialization succeeds.");
} catch (error: any) {
  console.error(`[TUICallKit] Initialization failed. Reason: ${error}`);
}
```

The parameters are described below:
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Required</td>

<td rowspan="1" colSpan="1" >Meaning</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SDKAppID</td>

<td rowspan="1" colSpan="1" >Number</td>

<td rowspan="1" colSpan="1" >Yes</td>

<td rowspan="1" colSpan="1" >The SDKAppID of your app, you can find your SDKAppID in the Live Audio and Video console. For details, see [Activating Services](https://write.woa.com/document/140196392040579072)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userID</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >Yes</td>

<td rowspan="1" colSpan="1" >The current user's ID is of string type, only allowing for the inclusion of English letters (a-z and A-Z), digits (0-9), hyphens (-) and underscores (_)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userSig</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >Yes</td>

<td rowspan="1" colSpan="1" >Use SDKSecretKey to encrypt SDKAppID, UserID and other information to obtain userSig.<br>It is an authentication ticket used by Tencent Cloud to identify whether the current user can use TRTC services. For how to obtain it, please refer to How to Calculate [UserSig](https://write.woa.com/document/140287034184511488)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >tim</td>

<td rowspan="1" colSpan="1" >TencentCloudChat</td>

<td rowspan="1" colSpan="1" >No</td>

<td rowspan="1" colSpan="1" >tim is an instance of [TencentCloudChat](https://www.npmjs.com/package/@tencentcloud/chat) SDK.</td>
</tr>
</table>


### calls

Initiate a one-to-one or multi-person call.
``` javascript
try {
  await TUICallKitAPI.calls({ 
    userIDList: ['jack', 'tom'], 
    type: CallMediaType.VIDEO 
  });
} catch (error: any) {
  console.error(`[TUICallKit] Failed to call the groupCall API. Reason:${error}`);
}
```

The parameters are described below:
<table>
<tr>
<td rowspan="1" colSpan="1" >**Parameter**</td>

<td rowspan="1" colSpan="1" >**Type**</td>

<td rowspan="1" colSpan="1" >**Required**</td>

<td rowspan="1" colSpan="1" >**Meaning**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userIDList</td>

<td rowspan="1" colSpan="1" >Array<String></td>

<td rowspan="1" colSpan="1" >Yes</td>

<td rowspan="1" colSpan="1" >List of called users</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >type</td>

<td rowspan="1" colSpan="1" >[CallMediaType](https://www.tencentcloud.com/document/product/647/51015#Type)</td>

<td rowspan="1" colSpan="1" >Yes</td>

<td rowspan="1" colSpan="1" >The type of media for the call, you can refer to [CallMediaType for the explanation of parameter values](https://write.woa.com/document/95825268984856576)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >chatGroupID</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >Yes</td>

<td rowspan="1" colSpan="1" >chat group Id.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >roomID</td>

<td rowspan="1" colSpan="1" >Number</td>

<td rowspan="1" colSpan="1" >No</td>

<td rowspan="1" colSpan="1" >Numerical Room ID, range [1, 2147483647]</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >strRoomID</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >No</td>

<td rowspan="1" colSpan="1" >String room ID. **v3.3.1+ supported**<br>**range：**<br>Limited to 64 bytes in length. The supported character set range is as follows (a total of 89 characters):<br>- Lowercase and uppercase English letters.（a-zA-Z）；<br>- Number（0-9）；<br>- `Spaces`、`!`、`#`、`$`、`%`、`&`、`(`、`)`、`+`、`-`、`:`、`;`、`<`、`=`、`.`、`>`、`?`、`@`、`[`、`]`、`^`、`_`、`{`、`}`、`\|`、`~`、`,`。<br>1. roomID and strRoomID are mutually exclusive, if you use strRoomID, then roomID should be 0. If you use both, the SDK will prioritize the roomID. 2.<br>2. don't mix roomID and strRoomID, because they are not interchangeable, for example, the number 123 and the string "123" are two completely different rooms.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >timeout</td>

<td rowspan="1" colSpan="1" >Number</td>

<td rowspan="1" colSpan="1" >No</td>

<td rowspan="1" colSpan="1" >Call timeout, default: 30s, unit: seconds. timeout = 0, set to no timeout</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userData</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >No</td>

<td rowspan="1" colSpan="1" >Customize the extended fields when initiating a call. The called user has this parameter in the [ON_CALL_RECEIVED](https://write.woa.com/document/95825290217033728) event.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[offlinePushInfo](https://www.tencentcloud.com/document/product/647/51015#offlinePushInfo)</td>

<td rowspan="1" colSpan="1" >Object</td>

<td rowspan="1" colSpan="1" >No</td>

<td rowspan="1" colSpan="1" >Customize offline message push parameters</td>
</tr>
</table>


### join

Proactively join a call.
``` javascript
try {
  await TUICallKitAPI.join({ 
    callId: 'xx'
  });
} catch (error: any) {
  console.error(`[TUICallKit] Failed to call the join API. Reason:${error}`);
}
```

The parameters are described below:
<table>
<tr>
<td rowspan="1" colSpan="1" >**Parameter**</td>

<td rowspan="1" colSpan="1" >**Type**</td>

<td rowspan="1" colSpan="1" >**Required**</td>

<td rowspan="1" colSpan="1" >**Meaning**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >callId</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >Yes</td>

<td rowspan="1" colSpan="1" >Unique ID for this call</td>
</tr>
</table>


### setLanguage

Set language, currently supports: Chinese, English, Japanese.
``` javascript
TUICallKitAPI.setLanguage("zh-cn"); // "en" | "zh-cn" | "ja_JP"
```

The parameters are described below:
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Required</td>

<td rowspan="1" colSpan="1" >Meaning</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >lang</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >Yes</td>

<td rowspan="1" colSpan="1" >Language type `en`,`zh-cn` and `ja_JP`. </td>
</tr>
</table>


### setSelfInfo

Set your own nickname and avatar.

> **Note: **
> 

> **If you use this interface to modify user information during a call, the UI will not be updated immediately, and you will need to wait until the next call to see the changes.**
> 

``` javascript
try {
  await TUICallKitAPI.setSelfInfo({ nickName: "xxx", avatar: "http://xxx" });
} catch (error: any) {
  console.error(`[TUICallKit] Failed to call the setSelfInfo API. Reason: ${error}`;
}
```

The parameters are described below:
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Required</td>

<td rowspan="1" colSpan="1" >Meaning</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >nickName</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >Yes</td>

<td rowspan="1" colSpan="1" >own nickname</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >avatar</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >Yes</td>

<td rowspan="1" colSpan="1" >own avatar address</td>
</tr>
</table>


### setCallingBell
- Customize the user's incoming call ringtone.

- The input is restricted to the local MP3 format file address. It is imperative to ensure that the application has access to this file directory.

- Use the import method to import the ringtone file.

- If you need to restore the default ringtone, just pass empty filePath.

   ``` javascript
   import filePath from '../assets/phone_ringing.mp3';
   try {
     await TUICallKitAPI.setCallingBell(filePath);
   } catch (error: any) {
     console.error(`[TUICallKit] Failed to call the setCallingBell API. Reason: ${error}`);
   }
   ```

   The parameters are described below:

<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Required</td>

<td rowspan="1" colSpan="1" >Meaning</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >filePath</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >Yes</td>

<td rowspan="1" colSpan="1" >Ringtone file path</td>
</tr>
</table>


### enableFloatWindow

Turn on/off the floating window function. The default is false. The floating window button in the upper left corner of the call interface is hidden. It will be displayed after setting it to true.
``` javascript
try {
  const enable = true;
  await TUICallKitAPI.enableFloatWindow(enable);
} catch (error: any) {
  console.error(`[TUICallKit] Failed to call the enableFloatWindow API. Reason: ${error}`);
}
```

The parameters are described below:
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Required</td>

<td rowspan="1" colSpan="1" >Meaning</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enable</td>

<td rowspan="1" colSpan="1" >Boolean</td>

<td rowspan="1" colSpan="1" >Yes</td>

<td rowspan="1" colSpan="1" >Turn on/off the floating window function. default false.</td>
</tr>
</table>


### enableMuteMode

Turn on/off the ringtone for incoming calls. When turned on, the incoming call ringtone will not be played when a call request is received.
``` javascript
try {
  const enable = true;
  await TUICallKitAPI.enableMuteMode(enable);
} catch (error: any) {
  console.error(`[TUICallKit] Failed to call the enableMuteMode API. Reason: ${error}`);
}
```

### enableVirtualBackground

Turn on/off the blurred background function. If you want to set the picture background to be blurry see [Web](https://write.woa.com/document/145193410188582912). By calling the interface, you can display the blurred background function button on the UI, and click the button to directly enable the blurred background function.
``` javascript
import { TUICallKitAPI } from "@trtc/calls-uikit-react";
const enable = true;
TUICallKitAPI.enableVirtualBackground(enable);
```

The parameters are described below:
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Required</td>

<td rowspan="1" colSpan="1" >Meaning</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enable</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >Yes</td>

<td rowspan="1" colSpan="1" >- enable = true, show blur background button<br>- enable = false, don't show blur background button</td>
</tr>
</table>


### destroyed
- Terminate the TUICallKit instance.

- This method won't automatically log out of `tim`, manual logging out is required: `tim.logout();`.

   ``` javascript
   try {
     await TUICallKitAPI.destroyed();
   } catch (error: any) {
     console.error(`[TUICallKit] Failed to call the destroyed API. Reason: ${error}`);
   }
   ```

### hideFeatureButton

Hidden feature buttons, currently only support Camera, Microphone, and Switch Camera Button.
``` typescript
TUICallKitAPI.hideFeatureButton(buttonName: FeatureButton);
```

The parameters are described below:
<table>
<tr>
<td rowspan="1" colSpan="1" >**Parameter**</td>

<td rowspan="1" colSpan="1" >**Type**</td>

<td rowspan="1" colSpan="1" >**Required**</td>

<td rowspan="1" colSpan="1" >**Meaning**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >buttonName</td>

<td rowspan="1" colSpan="1" >[FeatureButton](https://www.tencentcloud.com/document/product/647/51015#FeatureButton)</td>

<td rowspan="1" colSpan="1" >Yes</td>

<td rowspan="1" colSpan="1" >Button Name</td>
</tr>
</table>


### setLocalViewBackgroundImage

Set the background image for the local user's call interface.
``` typescript
TUICallKitAPI.setLocalViewBackgroundImage(url: string);
```

The parameters are described below:
<table>
<tr>
<td rowspan="1" colSpan="1" >**Parameter**</td>

<td rowspan="1" colSpan="1" >**Type**</td>

<td rowspan="1" colSpan="1" >**Required**</td>

<td rowspan="1" colSpan="1" >**Meaning**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >url</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >Yes</td>

<td rowspan="1" colSpan="1" >Image Address (supports Local Path and Network Address)</td>
</tr>
</table>


### setRemoteViewBackgroundImage

Set the background image for the remote user's call interface.
``` typescript
TUICallKitAPI.setRemoteViewBackgroundImage(userId: string, url: string);
```

The parameters are described below:
<table>
<tr>
<td rowspan="1" colSpan="1" >**Parameter**</td>

<td rowspan="1" colSpan="1" >**Type**</td>

<td rowspan="1" colSpan="1" >**Required**</td>

<td rowspan="1" colSpan="1" >**Meaning**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >Yes</td>

<td rowspan="1" colSpan="1" >Remote User userId, setting to '*' means it applies to all Remote Users</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >url</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >Yes</td>

<td rowspan="1" colSpan="1" >Image Address (supports Local Path and Network Address)</td>
</tr>
</table>


### setLayoutMode

Set the call interface layout mode.




【Vue】
``` javascript
import { TUICallKitAPI, LayoutMode } from "@trtc/calls-uikit-vue";
TUICallKitAPI.setLayoutMode(LayoutMode.LocalInLargeView);
```


【React】
``` javascript
import { TUICallKitAPI, LayoutMode } from "@trtc/calls-uikit-react";
TUICallKitAPI.setLayoutMode(LayoutMode.LocalInLargeView);
```

Parameter list:
<table>
<tr>
<td rowspan="1" colSpan="1" >**Parameter**</td>

<td rowspan="1" colSpan="1" >**Type**</td>

<td rowspan="1" colSpan="1" >**Required**</td>

<td rowspan="1" colSpan="1" >**Meaning**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >layoutMode</td>

<td rowspan="1" colSpan="1" >[LayoutMode](https://www.tencentcloud.com/document/product/647/51015#LayoutMode)</td>

<td rowspan="1" colSpan="1" >Yes</td>

<td rowspan="1" colSpan="1" >User flow layout mode</td>
</tr>
</table>


### setCameraDefaultState

Set whether the camera is on by default.
``` javascript
TUICallKitAPI.setCameraDefaultState(true);
```

Parameter list:
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Required</td>

<td rowspan="1" colSpan="1" >Meaning</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >isOpen</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >Yes</td>

<td rowspan="1" colSpan="1" >Whether to enable the camera</td>
</tr>
</table>


### getTUICallEngineInstance

Get TUICallEngine instance.
``` javascript
TUICallKitAPI.getTUICallEngineInstance();
```

## TUICallKit Type Definition

### videoDisplayMode

There are three values for the `videoDisplayMode` display mode:
- `VideoDisplayMode.CONTAIN`

- `VideoDisplayMode.COVER`

- `VideoDisplayMode.FILL`, the default value is `VideoDisplayMode.COVER`.

<table>
<tr>
<td rowspan="1" colSpan="1" >Attribute</td>

<td rowspan="1" colSpan="1" >Value</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="3" colSpan="1" >videoDisplayMode</td>

<td rowspan="1" colSpan="1" >VideoDisplayMode.CONTAIN</td>

<td rowspan="1" colSpan="1" >- Ensuring the full display of video content is our top priority.<br>- The dimensions of the video are scaled proportionally until one side aligns with the frame of the viewing window.<br>- In case of discrepancy in sizes between the video and the display window, the video is scaled - on the premise of maintaining the aspect ratio - to fill the window, resulting in a black border around the scaled video.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >VideoDisplayMode.COVER</td>

<td rowspan="1" colSpan="1" >- Priority is given to ensure that the viewing window is filled.<br>- The video size is scaled proportionally until the entire window is filled.<br>- If the video's dimensions are different from those of the display window, the video stream will be cropped or stretched to match the window's ratio.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >VideoDisplayMode.FILL</td>

<td rowspan="1" colSpan="1" >- Ensuring that the entire video content is displayed while filling the window does not guarantee preservation of the original video's proportion.<br>- The dimensions of the video will be stretched to match those of the window.</td>
</tr>
</table>


### videoResolution

The resolution `videoResolution` has three possible values:
- `VideoResolution.RESOLUTION_480P`

- `VideoResolution.RESOLUTION_720P`

- `VideoResolution.RESOLUTION_1080P`, the default value is `VideoResolution.RESOLUTION_480P`.


   **Resolution Explanation:**

<table>
<tr>
<td rowspan="1" colSpan="1" >Video Profile</td>

<td rowspan="1" colSpan="1" >Resolution (W x H)</td>

<td rowspan="1" colSpan="1" >Frame Rate (fps)</td>

<td rowspan="1" colSpan="1" >Bitrate (Kbps)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >480p</td>

<td rowspan="1" colSpan="1" >640 × 480</td>

<td rowspan="1" colSpan="1" >15</td>

<td rowspan="1" colSpan="1" >900</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >720p</td>

<td rowspan="1" colSpan="1" >1280 × 720</td>

<td rowspan="1" colSpan="1" >15</td>

<td rowspan="1" colSpan="1" >1500</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >1080p</td>

<td rowspan="1" colSpan="1" >1920 × 1080</td>

<td rowspan="1" colSpan="1" >15</td>

<td rowspan="1" colSpan="1" >2000</td>
</tr>
</table>


   **Frequently Asked Questions:**

- iOS 13&14 does not support encoding videos higher than 720P. It is suggested to limit the highest collection to 720P on these two system versions. Refer to [iOS Safari known issue case 12](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-02-info-webrtc-issues.html#h2-4).

- Firefox does not permit the customization of video frame rates (default is set to 30fps).

- Due to the influence of system performance usage, camera collection capabilities, browser restrictions, and other factors, the actual values of video resolution, frame rate, and bit rate may not necessarily match the set values exactly. In such scenarios, the browser will automatically adjust the Profile to get as close to the set values as feasible.


### STATUS
<table>
<tr>
<td rowspan="1" colSpan="1" >STATUS attribute value</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >STATUS.IDLE</td>

<td rowspan="1" colSpan="1" >Idle status</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >STATUS.BE_INVITED</td>

<td rowspan="1" colSpan="1" >Received an Audio/Video Call Invite</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >STATUS.DIALING_C2C</td>

<td rowspan="1" colSpan="1" >Initiating a one-to-one call</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >STATUS.DIALING_GROUP</td>

<td rowspan="1" colSpan="1" >Initiating a group call</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >STATUS.CALLING_C2C_AUDIO</td>

<td rowspan="1" colSpan="1" >Engaged in a 1v1 Audio Call</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >STATUS.CALLING_C2C_VIDEO</td>

<td rowspan="1" colSpan="1" >In the midst of a one-to-one video call</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >STATUS.CALLING_GROUP_AUDIO</td>

<td rowspan="1" colSpan="1" >Engaged in Group Audio Communication</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >STATUS.CALLING_GROUP_VIDEO</td>

<td rowspan="1" colSpan="1" >Engaged in group video call</td>
</tr>
</table>


### **CallMediaType**
<table>
<tr>
<td rowspan="1" colSpan="1" >CallMediaType Type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >CallMediaType.AUDIO_CALL </td>

<td rowspan="1" colSpan="1" >Audio Call</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >CallMediaType.VIDEO </td>

<td rowspan="1" colSpan="1" >Video Call</td>
</tr>
</table>


### **offlinePushInfo**
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Required</td>

<td rowspan="1" colSpan="1" >Meaning</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >offlinePushInfo.title</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >No</td>

<td rowspan="1" colSpan="1" >Offline Push Title (Optional)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >offlinePushInfo.description</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >No</td>

<td rowspan="1" colSpan="1" >Offline Push Content (Optional)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >offlinePushInfo.androidOPPOChannelID</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >No</td>

<td rowspan="1" colSpan="1" >Setting the channel ID for OPPO phones with 8.0 system and above for offline pushes (Optional)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >offlinePushInfo.extension</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >No</td>

<td rowspan="1" colSpan="1" >Offline push through content. Can be used to set Android [Notification mode](https://write.woa.com/document/95825268984856576) and [VoIP mode](https://write.woa.com/document/95825268984856576).** Default**: Notification mode, it will be a notification from the system; VoIP mode is required to pass the field.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >offlinePushInfo.ignoreIOSBadge</td>

<td rowspan="1" colSpan="1" >Boolean</td>

<td rowspan="1" colSpan="1" >No</td>

<td rowspan="1" colSpan="1" >Ignore badge count for offline push (only for iOS), if set to true, the message will not increase the unread count of the app icon on the iOS receiver's side.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >offlinePushInfo.iOSSound</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >No</td>

<td rowspan="1" colSpan="1" >Offline push sound setting (only for iOS).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >offlinePushInfo.androidSound</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >No</td>

<td rowspan="1" colSpan="1" >Offline push sound setting.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >offlinePushInfo.androidVIVOClassification</td>

<td rowspan="1" colSpan="1" >Number</td>

<td rowspan="1" colSpan="1" >No</td>

<td rowspan="1" colSpan="1" >Classification of VIVO push messages (deprecated interface, VIVO push service will optimize message classification rules on April 3, 2023. It is recommended to use setAndroidVIVOCategory to set the message category). 0: Operational messages, 1: System messages. The default value is 1. </td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >offlinePushInfo.androidXiaoMiChannelID</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >No</td>

<td rowspan="1" colSpan="1" >Set the channel ID for Xiaomi phones with Android 8.0 and above systems. </td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >offlinePushInfo.androidFCMChannelID</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >No</td>

<td rowspan="1" colSpan="1" >Set the channel ID for google phones with Android 8.0 and above systems.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >offlinePushInfo.androidHuaWeiCategory</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >No</td>

<td rowspan="1" colSpan="1" >Classification of Huawei push messages. </td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >offlinePushInfo.isDisablePush</td>

<td rowspan="1" colSpan="1" >Boolean</td>

<td rowspan="1" colSpan="1" >No</td>

<td rowspan="1" colSpan="1" >Whether to turn off push notifications (default is on). </td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >offlinePushInfo.iOSPushType</td>

<td rowspan="1" colSpan="1" >Number</td>

<td rowspan="1" colSpan="1" >No</td>

<td rowspan="1" colSpan="1" >iOS offline push type，default is 0。0-APNs；1-VoIP. </td>
</tr>
</table>


#### Android Notification Mode
``` javascript
const extension = {
  timPushFeatures: {        
    fcmPushType: 0, // 0, VoIP; 1, notification
  }
};
offlinePushInfo.extension = JSON.stringify(extension);
```

#### Android VoIP Mode
``` javascript
const extension = {
  timPushFeatures: {        
    fcmPushType: 0, // 0, data; 1, notification
    fcmNotificationType: 1, // 0, TIMPush implementation； 1, business implementation after transparent transmission 
  }
};
offlinePushInfo.extension = JSON.stringify(extension);
```

### FeatureButton
<table>
<tr>
<td rowspan="1" colSpan="1" >FeatureButton Type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >FeatureButton.Camera</td>

<td rowspan="1" colSpan="1" >Camera Button</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >FeatureButton.Microphone</td>

<td rowspan="1" colSpan="1" >Microphone Button</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >FeatureButton.SwitchCamera</td>

<td rowspan="1" colSpan="1" >Switches between the front and rear cameras.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >FeatureButton.InviteUser</td>

<td rowspan="1" colSpan="1" >Invite users button</td>
</tr>
</table>


### LayoutMode
<table>
<tr>
<td rowspan="1" colSpan="1" >LayoutMode type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >LayoutMode.LocalInLargeView</td>

<td rowspan="1" colSpan="1" >Local user in large window display</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >LayoutMode.RemoteInLargeView</td>

<td rowspan="1" colSpan="1" >Remote user in large window display</td>
</tr>
</table>


