> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/en/llms.txt
> Use this file to discover all available pages before exploring further.

# Tutorial: Demo Quick Run

This article mainly introduces how to quickly run Tencent Cloud TRTC Web demo.

## Prerequisites

You have registered a Tencent Cloud account and completed real-name authentication.

## Operation steps

### Step 1: Create a new application

Please visit the [TRTC console](https://console.trtc.io/) and create an RTC Engine application.

### Step 2. Get your SDKAppId and SDKSecretKey

After your application created, you can get your **SDKAppID** and **SDKSecretKey** in Basic information , which are used to run demo.

![Console information](https://qcloudimg.tencent-cloud.cn/raw/21dfdacea923b78ea4f22bb4f6b47b84.png)

## Step 3: Run the Demo

1. **Run demo online**

   We provides the following basic demos. You can choose the project framework you are familiar with to run and experience:

   1.1 [quick-demo-js](https://web.sdk.qcloud.com/trtc/webrtc/v5/demo/quick-demo-js/index.html) is a demo coded by Javascript. Source code: [github](https://github.com/LiteAVSDK/TRTC_Web/tree/main/quick-demo-js).

   1.2 [quick-demo-vue2-js](https://web.sdk.qcloud.com/trtc/webrtc/v5/demo/quick-demo-vue2-js/index.html) is a demo coded by Vue2 + Javascript. Source code: [github](https://github.com/LiteAVSDK/TRTC_Web/tree/main/quick-demo-vue2-js).

   1.3 [quick-demo-vue3-ts](https://web.sdk.qcloud.com/trtc/webrtc/v5/demo/quick-demo-vue3-ts/index.html) is a demo coded by Vue3 + Typescript. Source code: [github](https://github.com/LiteAVSDK/TRTC_Web/tree/main/quick-demo-vue3-ts).

2. **Run Demo locally**

   2.1 Download source code by [Github](https://github.com/LiteAVSDK/TRTC_Web/tree/main) or [Zip](https://web.sdk.qcloud.com/trtc/webrtc/download/webrtc_latest.zip).

   2.2 Run demo locally by following steps.

   (1) Open the demo file

   - for `quick-demo-js`, open the `TRTC_Web/quick-demo-js/index.html` directly via a browser.
   - for `quick-demo-vue2-js`, enter the `TRTC_Web/quick-demo-vue2-js/` directory, then run `npm start` in this directory, the default browser will automatically open the address [http://localhost:8080/](http://localhost:8080/)
   - for `quick-demo-vue3-ts`, enter the `TRTC_Web/quick-demo-vue3-ts/` directory, then run `npm start` in this directory, the default browser will automatically open the address [http://localhost:3000/](http://localhost:3000/)

   (2) Fill in the SDKAppId and SDKSecretKey obtained in [Step 2](#Step-2.-Get-your-SDKAppId-and-SDKSecretKey) on the page opened in the browser.

   ![Demo interface](https://qcloudimg.tencent-cloud.cn/raw/220c9cf29087471302898415e5075254.png)

   (3) Functional experience

   - Click the [Enter Room] button to enter the room.
   - Click the [Start Local Audio/Video] button to capture the microphone or camera.
   - Click the [Stop Local Audio/Video] button to stop capturing the microphone or camera.
   - Click the [Start Share Screen] button to start screen sharing.
   - Click the [Stop Share Screen] button to cancel screen sharing.

   (4) After joining the room, you can share the invitation link to experience the TRTC Web voice and video communication function with the invitee.

> **Important Notes:**
>
> - To deploy to the public network for experience, you need to access it through HTTPS protocol, that is, `https://domain/xxx`. For the reason, please refer to the document [Page Access Protocol Restriction Description](./tutorial-05-info-browser.html#h2-3).
> - Currently, the desktop Chrome browser supports TRTC Web SDK's related features more completely, so it is recommended to use Chrome browser for experience, please refer to the document [Browser Compatibility Information](./tutorial-05-info-browser.html#h2-2).
> - The correct way to generate UserSig is to integrate the UserSig calculation code into your server and provide an interface for the App. When you need UserSig, your App sends a request to the business server to obtain a dynamic UserSig. For more details, please refer to [Generating UserSig on the Server](https://trtc.io/document/35166?platform=web&product=rtcengine&menulabel=coresdk).