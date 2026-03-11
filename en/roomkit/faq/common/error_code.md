> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/en/llms.txt
> Use this file to discover all available pages before exploring further.

---
product: 'Room'
tech_stack: 'roomKit'
framework: 'common'
title: 'RoomKit Error Code Reference'
keywords: ['error code', 'error', 'roomKit', 'room package issue', 'microphone permission issue', 'camera/microphone issue']
---

# RoomKit Error Code Reference

## RoomKit Error Codes (Topic: RoomKit Error Code)

## Error Code -2
**Cause:** Operation frequency limit exceeded. Requests are too frequent, please try again later.
**Solution:** Operation frequency limit exceeded. Requests are too frequent, please try again later.

## Error Code -1002
**Cause:** SDK not initialized.
**Solution:** Please call the initialization interface first to complete SDK initialization.

## Error Code -1004
**Cause:** No package purchased or account is in arrears.
**Solution:** Visit the [Tencent Cloud Console](https://console.trtc.io/subscription/buy/live) to purchase. For first-time use, you can [activate the trial version](https://trtc.io/document/60033?product=live&menulabel=uikit&platform=web).

## Error Code -1101
**Cause:** Camera permission denied.
**Solution:** Please check your browser settings to ensure camera access is allowed. If you have confirmed permission is granted, please visit the [Audio/Video Capability Detection Tool](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html) to check if your device and environment are supported.

## Error Code -1105
**Cause:** Microphone permission denied.
**Solution:** Please check your browser settings to ensure microphone access is allowed. If you have confirmed permission is granted, please visit the [Audio/Video Capability Detection Tool](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html) to check if your device and environment are supported.

## Error Code -1100
**Cause:** Failed to open camera.
**Solution:** Please check your browser settings to ensure camera access is allowed. If you have confirmed permission is granted, please visit the [Audio/Video Capability Detection Tool](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html) to check if your device and environment are supported.

## Error Code -1104
**Cause:** Failed to open microphone.
**Solution:** Please check your browser settings to ensure microphone access is allowed. If you have confirmed permission is granted, please visit the [Audio/Video Capability Detection Tool](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html) to check if your device and environment are supported.

## Error Code 100007
**Cause:** No package purchased or account is in arrears.
**Solution:** Visit the [Tencent Cloud Console](https://console.trtc.io/subscription/buy/live) to purchase. For first-time use, you can [activate the trial version](https://trtc.io/document/60033?product=live&menulabel=uikit&platform=web).

## Error Code 70001
**Cause:** User signature has expired.
**Solution:** It is recommended to set the signature validity period to no less than 24 hours. Refer to [Generate UserSig (User Authentication)](https://trtc.io/document/35166?product=live&menulabel=uikit&platform=web).

## Error Code 70003
**Cause:** Invalid user signature.
**Solution:** Please regenerate. Refer to [Generate UserSig (User Authentication)](https://trtc.io/document/35166?product=live&menulabel=uikit&platform=web).

## Error Code 70014
**Cause:** SDKAppID does not match the user signature.
**Solution:** Please verify. You can validate the signature at the [Tencent Cloud Console](https://console.trtc.io/usersig).

## Error Code 5300
**Cause:** Exception occurred while accessing device or capturing audio/video.
**Solution:** Please visit the [Audio/Video Capability Detection Tool](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html) to check if your device and environment are supported.

## Error Code 5301
**Cause:** Camera/microphone device not detected.
**Solution:** Please ensure your camera/microphone is connected and check if the camera/microphone is available in system or browser settings.

## Error Code 5302
**Cause:** Camera/microphone permission denied.
**Solution:** Please check your browser settings to ensure camera and microphone access is allowed. If you have confirmed permission is granted, please visit the [Audio/Video Capability Detection Tool](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html) to check if your device and environment are supported.
