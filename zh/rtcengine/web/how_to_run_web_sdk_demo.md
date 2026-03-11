> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

# 快速跑通 Demo

本文主要介绍如何快速跑通腾讯云 TRTC Web demo。

## 前提条件

您已 [注册腾讯云](https://cloud.tencent.com/document/product/378/17985) 账号，并完成 [实名认证](https://cloud.tencent.com/document/product/378/3629)。

## 操作步骤

### 步骤1：创建新的应用

登录[实时音视频控制台](https://console.cloud.tencent.com/trtc/quickstart)，创建一个 TRTC 应用。

### 步骤2：下载 SDK 和 Demo 源码

1. 下载 Web 端 SDK 及配套的 Demo 源码。
2. 下载完成后，单击 **“已下载，下一步”**。

![下载 SDK 和 Demo 源码](https://qcloudimg.tencent-cloud.cn/raw/694a75aa29fa7ae11cb14f3948bbf386.png)

### 步骤3：获取 SDKAppId 和 密钥（SDKSecretKey)

1. 进入修改配置页，获取 `SDKAppID` 和 `密钥`。
2. 复制粘贴 SDKAppId 和 密钥（SDKSecretKey）完成后，单击 **已复制粘贴，下一步** 即创建成功。

![获取 SDKAppId 和 密钥](https://qcloudimg.tencent-cloud.cn/raw/1aa752664de9fa0dfaf163a8092b9b40.png)

### 步骤4：运行 Demo

TRTC Web 目前提供以下几种基础 Demo，您可以选择您熟悉的项目框架进行运行体验：

1. `quick-demo-js` 为 TRTC Web 快速运行 Demo (原生 Js 版本)，集成了 TRTC Web SDK 的基础音视频通话、设备选择等功能，使用原生 Js 开发，可直接在浏览器中运行。快速体验可访问 [quick-demo-js 在线体验地址](https://web.sdk.qcloud.com/trtc/webrtc/v5/demo/quick-demo-js/index.html)。
2. `quick-demo-vue2-js` 为 TRTC Web 快速运行 Demo (Vue2 版本)，集成了 TRTC Web SDK 的基础音视频通话、设备选择等功能，使用 Vue2 + JavaScript 开发，需要您安装 Node 环境，按下方说明运行体验。快速体验可访问 [quick-demo-vue2-js 在线体验地址](https://web.sdk.qcloud.com/trtc/webrtc/v5/demo/quick-demo-vue2-js/index.html)。
3. `quick-demo-vue3-ts` 为 TRTC Web 快速运行 Demo (Vue3 版本)，集成了 TRTC Web SDK 的基础音视频通话、设备选择等功能，使用 Vue3 + TypeScript 开发，需要您安装 Node 环境，按下方说明运行体验。快速体验可访问 [quick-demo-vue3-ts 在线体验地址](https://web.sdk.qcloud.com/trtc/webrtc/v5/demo/quick-demo-vue3-ts/index.html)。

> **注意：**
> - 本地体验 Demo 可以直接在本地搭建静态服务（本地计算机需要接入互联网），通过 `http://localhost:端口` 访问，打开两个页面即可进行通话。
> - 部署到公网体验，需要通过 HTTPS 协议，即 `https://域名/xxx` 访问，原因可参考文档[页面访问协议限制说明](./tutorial-05-info-browser.html#h2-3)。
> - 目前桌面端 Chrome 浏览器支持 TRTC Web SDK 的相关特性比较完整，因此建议使用 Chrome 浏览器进行体验，参考文档[浏览器兼容信息](./tutorial-05-info-browser.html#h2-2)。

#### Demo 1：quick-demo-js

1. 在下载的源码中找到并使用浏览器打开 `TRTC_Web/quick-demo-js/index.html` 文件。
2. 在浏览器打开的页面中填写 [步骤三](#step3) 获取的 SDKAppId 和 SDKSecretKey。
   ![填写 SDKAppId 和 SDKSecretKey](https://qcloudimg.tencent-cloud.cn/raw/58138291297d6bb58141b750f028ea4c.png)
3. 功能体验
   - 点击【Enter Room】按钮进入房间
   - 点击【Start Local Audio/Video】按钮，可采集麦克风或摄像头
   - 点击【Stop Local Audio/Video】按钮，可终止采集麦克风或摄像头
   - 点击【Start Share Screen】按钮开始屏幕分享
   - 点击【Stop Share Screen】按钮取消屏幕分享
4. 加入房间后您可以通过分享邀请链接与被邀请人一起体验 TRTC Web 语音及视频互通功能。

#### Demo 2：quick-demo-vue2-js

1. 在下载的源码中找到并进入到 `TRTC_Web/quick-demo-vue2-js/` 目录下。
   ```shell
   cd quick-demo-vue2-js
   ```
2. 本地运行 Demo，在终端执行以下命令，将会自动安装依赖并运行 demo
   ```shell
   npm start
   ```
   默认浏览器会自动打开 http://localhost:8080/ 地址。
3. 在浏览器打开的页面中填写 [步骤三](#step3) 获取的 SDKAppId 和 SDKSecretKey。
   ![填写 SDKAppId 和 SDKSecretKey](https://qcloudimg.tencent-cloud.cn/raw/b7accfeba1614a6a1e43089887425406.png)
4. 功能体验
   - 点击【进入房间】按钮进入房间
   - 点击【采集麦克风/摄像头】按钮，可采集麦克风或摄像头
   - 点击【终止采集麦克风/摄像头】按钮，可终止采集麦克风或摄像头
   - 点击【开始共享屏幕】按钮开始屏幕分享
   - 点击【停止共享屏幕】按钮取消屏幕分享
5. 加入房间后您可以通过分享邀请链接与被邀请人一起体验 TRTC Web 语音及视频互通功能。

#### Demo 3：quick-demo-vue3-ts

1. 在下载的源码中找到并进入到 `TRTC_Web/quick-demo-vue3-ts/` 目录下。
2. 本地运行 Demo
   ```shell
   npm start
   ```
   默认浏览器会自动打开 http://localhost:3000/ 地址。
3. 在浏览器打开的页面中填写 [步骤三](#step3) 获取的 SDKAppId 和 SDKSecretKey。
   ![填写 SDKAppId 和 SDKSecretKey](https://qcloudimg.tencent-cloud.cn/raw/d4547af08134896170e89a49dec7a43a.png)
4. 功能体验
   - 输入 userId 和 roomId
   - 点击【Enter Room】按钮进入房间
   - 点击【Start Local Audio/Video】按钮，可采集麦克风或摄像头
   - 点击【Stop Local Audio/Video】按钮，可终止采集麦克风或摄像头
   - 点击【Start Share Screen】按钮开始屏幕分享
   - 点击【Stop Share Screen】按钮取消屏幕分享
5. 加入房间后您可以通过分享邀请链接与被邀请人一起体验 TRTC Web 语音及视频互通功能。

> **注意：**
> - 本文使用的生成 UserSig 的方案是在客户端中配置 SECRETKEY，该方法中 SECRETKEY 很容易被反编译逆向破解，一旦您的密钥泄露，攻击者就可以盗用您的腾讯云流量，因此**该方法仅适合本地跑通 Demo 和功能调试**。
> - 正确的 UserSig 签发方式是将 UserSig 的计算代码集成到您的服务端，并提供面向 App 的接口，在需要 UserSig 时由您的 App 向业务服务器发起请求获取动态 UserSig。更多详情请参见 [服务端生成 UserSig](https://cloud.tencent.com/document/product/647/17275#Server)。