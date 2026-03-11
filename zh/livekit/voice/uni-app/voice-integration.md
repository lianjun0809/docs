> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

本文档将帮助开发者使用 `AtomicXCore SDK` 的 `LiveListState` 和 `LiveSeatState` 快速构建一个包含主播开播和观众进房功能的语聊房 `App`。

## 准备工作

### 步骤 1. 开通服务

请参见 [开通服务](https://write.woa.com/document/141302177829593088)，获取体验版或付费版 SDK。

### 步骤2. 导入 tuikit-atomic-x
1. **安装组件**：打开 [AtomicXCore SDK](https://ext.dcloud.net.cn/plugin?id=25488) ，单击**下载插件并导入HBuilderX**，选择需要集成的项目并单击**确定**。

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100028028022/b6046271bb8811f0b4c35254001c06ec.png)

2. **配置工程权限:  **请在应用的 manifest.json 文件的app-plus > distribute 节点下，确保添加了以下必要的权限：

  - Android 平台（`android`节点）：在 `permissions` 数组中，请确保包含以下权限：

      ``` json
      "<uses-permission android:name=\"android.permission.RECORD_AUDIO\" />"
      ```
  - iOS 平台（ios 节点）：在 `privacyDescription` 对象中，请确保包含以下描述：

      ``` json
      "NSMicrophoneUsageDescription" : "应用需要访问您的麦克风以进行直播"  
      ```

      在 `UIBackgroundModes` 数组中，添加 `audio` 以支持后台播放音频。

      ``` json
      "UIBackgroundModes" : [ "audio" ]
      ```

### 步骤 3. 完成登录

在您的项目中调用 LoginState 中的 login 方法完成登录，**这是使用 **`AtomicXCore`** 所有功能的关键前提**。

> **重要：**
> 

> 推荐在您 App 自身的用户账户登录成功后，再调用 LoginState 中的 login 方法，以确保登录业务逻辑的清晰和一致。
> 

``` typescript
import { useLoginState } from "@/uni_modules/tuikit-atomic-x/state/LoginState";
  
const { login } = useLoginState();
  
const handleLogin = () => {
    login({
      sdkAppID: 1400000001,  // 替换为您的 SDKAppID
      userID: "test_001",    // 替换为您的 UserID
      userSig: "xxxxxxxxxx"  // 替换为您的 UserSig
    })
 }
```

**登录接口参数说明：**
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >说明</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >sdkAppID</td>

<td rowspan="1" colSpan="1" >number</td>

<td rowspan="1" colSpan="1" >从 [控制台](https://console.cloud.tencent.com/trtc)获取，通常是以 `140` 或 `160` 开头的 10 位整数。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userID</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >当前用户的唯一 ID，仅包含英文字母、数字、连字符和下划线。为避免多端登录冲突，**请勿使用**`1`、`123`**等简单 ID**。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userSig</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >用于腾讯云鉴权的票据。请注意：<br>- 开发环境：您可以采用本地 `GenerateTestUserSig.genTestSig` 函数生成 userSig 或者 通过 [UserSig 辅助工具](https://console.cloud.tencent.com/im/tool-usersig) 生成临时的 UserSig。<br>- 生产环境：为了防止密钥泄露，请务必采用服务端生成 UserSig 的方式。详细信息请参考 [服务端生成 UserSig](https://cloud.tencent.com/document/product/647/17275)。<br>更多信息请参见 [如何计算及使用 UserSig](https://cloud.tencent.com/document/product/647/17275)。</td>
</tr>
</table>


## 搭建语音聊天室

### 步骤1：实现房主创建语聊房

房主开播流程如下，您只需执行以下几步操作，即可快速搭建一个语聊房。

#### **1. 初始化麦位 **`State`

在您的房主页面中，创建一个 `LiveSeatState` 实例。您需要监听响应式数据的变化，以实时获取麦位数据来渲染您的 `UI`。
``` typescript
import { watch } from 'vue';
import { useLiveSeatState } from '@/uni_modules/tuikit-atomic-x/state/LiveSeatState';

// 定义直播间 ID（需要与后续 createLive 中使用的 liveID 保持一致）
const liveID = 'your_live_room_id'; // 替换为您的直播间 ID

// 使用 liveID 获取 LiveSeatState 实例
const { seatList } = useLiveSeatState(liveID);
```

#### **2. 打开麦克风**

通过调用 `DeviceState` 的 `openLocalMicrophone` 接口打开麦克风，示例代码如下：
``` typescript
import { useDeviceState } from "@/uni_modules/tuikit-atomic-x/state/DeviceState";
  
const { openLocalMicrophone } = useDeviceState();

const openMic = () => {
    openLocalMicrophone()
}
```

#### **3. 开始语聊**

通过调用 `LiveListState` 的 `createLive` 接口开始语聊房直播，完整示例代码如下：
``` typescript
import { useLiveListState } from '@/uni_modules/tuikit-atomic-x/state/LiveListState';

// 获取 LiveListState 实例
const { createLive } = useLiveListState();

// 开始直播
const startLive = () => {
    createLive({
      liveInfo: {
        liveID: 'xxx', // 设置直播的房间 id
        liveName: 'text', // 设置直播的房间名称
        keepOwnerOnSeat: true, // 配置主播始终在麦位上
        isSeatEnabled: true,
        seatLayoutTemplateID: 70, // 麦位布局模板（例如 70 为 10 麦位模板）
        seatMode: 'APPLY' // 上麦模式，例如申请上麦
        maxSeatCount: 10 // 最大麦位数
      },
      success: () => {        
        console.log('创建直播间成功')
        //您可以在这里进行页面的跳转
      },
      fail: (error) => {
        console.log('创建直播间失败', error)
      }
    });
  };
```

`LiveInfo`**参数说明:**
<table>
<tr>
<td rowspan="1" colSpan="1" >**参数名**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**属性**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`liveID`</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >必填</td>

<td rowspan="1" colSpan="1" >直播间的唯一标识符</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`liveName`</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >直播间的标题</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`notice`</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >直播间的公告信息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`isMessageDisable`</td>

<td rowspan="1" colSpan="1" >`boolean`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >是否禁言（`true`：是，`false`：否）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`isPublicVisible`</td>

<td rowspan="1" colSpan="1" >`boolean`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >是否公开可见（`true`：是，`false`：否）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`isSeatEnabled`</td>

<td rowspan="1" colSpan="1" >`boolean`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >是否启用麦位功能（`true`：是，`false`：否）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`keepOwnerOnSeat`</td>

<td rowspan="1" colSpan="1" >`boolean`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >是否保持房主在麦位上</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`maxSeatCount`</td>

<td rowspan="1" colSpan="1" >`number`</td>

<td rowspan="1" colSpan="1" >必填</td>

<td rowspan="1" colSpan="1" >最大麦位数量</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`seatMode`</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >上麦模式（`'FREE'`：自由上麦，`'APPLY'`：申请上麦）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`seatLayoutTemplateID`</td>

<td rowspan="1" colSpan="1" >`number`</td>

<td rowspan="1" colSpan="1" >必填</td>

<td rowspan="1" colSpan="1" >麦位布局模板 `ID`</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`coverURL`</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >直播间的封面图片地址</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`backgroundURL`</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >直播间的背景图片地址</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`activityStatus`</td>

<td rowspan="1" colSpan="1" >`number`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >直播活动状态</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`isGiftEnabled`</td>

<td rowspan="1" colSpan="1" >`boolean`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >是否启用礼物功能（`true`：是，`false`：否）</td>
</tr>
</table>


#### **4. 构建麦位 UI 界面**

通过 `LiveSeatState` 实例，监听 `seatList` 的变化，以实时获取麦位数据来渲染您的界面 UI 。您可以在主播页通过以下方式监听数据：
``` typescript
import { watch } from 'vue';
import { useLiveSeatState } from '@/uni_modules/tuikit-atomic-x/state/LiveSeatState';

// 使用 liveID 获取 LiveSeatState 实例
const { seatList } = useLiveSeatState(liveID);

watch( seatList ,(newSeatList) => {
    console.log('新的麦位列表', newSeatList)
    // 用这个数据来维护您的 UI
})
```

#### **5. 结束语聊**

语聊结束后，房主可以调用 `LiveListState` 的 `endLive` 接口结束语聊，`SDK` 会处理停止推流和销毁房间的逻辑。
``` typescript
import { useLiveListState } from '@/uni_modules/tuikit-atomic-x/state/LiveListState';

// 获取 LiveListState 实例
const { endLive } = useLiveListState();

// 结束直播
const handleEndLive = () => {
    endLive({
      success: () => {        
        console.log('结束直播成功')
        //您可以在这里进行页面的跳转
      },
      fail: (error) => {
        console.log('结束直播失败', error)
      }
    });
 }
```

### 步骤2：实现观众进入语聊房

观众进房流程如下，通过简单几步操作，即可实现观众进入语聊房

#### **1. 初始化麦位 **`State`

在您的观众页面 中，创建 `LiveSeatState` 实例，并监听 `seatList` 的变化，以渲染麦位 `UI` 。
``` typescript
import { watch } from 'vue';
import { useLiveSeatState } from '@/uni_modules/tuikit-atomic-x/state/LiveSeatState';

// 观众进房前，需要先获取要加入的直播间 ID（liveID）。通常有以下几种方式：
// 通过房间列表选择（可从 LiveListState 的 liveList 数据中获取）
// 使用 liveID 获取 LiveSeatState 实例
const { seatList } = useLiveSeatState(liveID);

watch(seatList,(newSeatList) => {
    console.log('新的麦位列表', newSeatList)
    // 用这个数据来维护您的 UI
})   
```

#### **2. 进入语聊房**

通过调用 `LiveListState` 的 `joinLive` 接口加入语聊房，完整示例代码如下：
``` typescript
import { useLiveListState } from '@/uni_modules/tuikit-atomic-x/state/LiveListState';

// 获取 LiveListState 实例
const { joinLive } = useLiveListState();

// 加入直播
const handleJoinLive = () => {
    joinLive({
      liveID: 'xxx', // 想要加入语聊房的 liveID
      success: () => {        
        console.log('成功进入语聊房')
        //您可以在这里进行页面的跳转
      },
      fail: (error) => {
        console.log('进入语聊房失败', error)
      }
    });
 }
```

#### **3. 构建麦位 UI 界面**

观众构建麦位 UI的流程与主播完全一致，请参考主播 [构建麦位 UI 界面](https://write.woa.com/#**4.-.E6.9E.84.E5.BB.BA.E9.BA.A6.E4.BD.8D-ui-.E7.95.8C.E9.9D.A2**)

#### **4. 退出语聊房**

观众退出语聊房时，需要调用 `LiveListState` 的 `leaveLive` 接口来退出。
``` typescript

import { useLiveListState } from '@/uni_modules/tuikit-atomic-x/state/LiveListState';

// 获取 LiveListState 实例
const { leaveLive } = useLiveListState();

// 退出语聊房
const handleLeaveLive = () => {
    leaveLive({
      liveID: 'xxx', // 您当前加入语聊房的 liveID
      success: () => {        
        console.log('退出语聊房成功')
        //您可以在这里进行页面的跳转
      },
      fail: (error) => {
        console.log('退出语聊房失败', error)
      }
    });
 }
```

### 运行效果

完成上述步骤后，即可完成一个最基础的语聊直播场景。您可以参考 [丰富语聊场景](https://write.woa.com/#82dbc44c-8a8e-40e2-89b9-66070f4beb72) 来完善语聊场景。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100028028022/0d6ebdebbbb711f0b9945254005ef0f7.png)


## 功能进阶

### **实现麦上用户说话音浪**

在语聊房场景中，一个常见的需求是当麦上用户说话时，在其头像上显示一个波浪动画，以提示全房间用户“谁在说话”，`LiveSeatState` 提供了 `speakingUsers` 数据流，专门用于实现此功能。

#### 实现效果

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100028028022/35399d8dbbb711f0a6c652540044a08e.png)


在您构建的麦位 UI 界面中监听 `speakingUsers` 变化，并更新“正在说话”状态，代码示例如下
``` typescript
import { watch } from 'vue';
import { useLiveSeatState } from '@/uni_modules/tuikit-atomic-x/state/LiveSeatState';

// 使用 liveID 获取 LiveSeatState 实例
const { speakingUsers } = useLiveSeatState(liveID);

watch(speakingUsers,(newSpeaker) => {
    console.log('正在说话的人', newSpeaker)
    // 用这个数据和之前监听的 seatList 进行匹配来更新 UI
})
```

## 丰富语音聊天室场景

当您完成了基础的语音聊天室功能后，您可以参考以下功能指南来为语音聊天室添加丰富的互动玩法。
<table>
<tr>
<td rowspan="1" colSpan="1" >**语音聊天室功能**</td>

<td rowspan="1" colSpan="1" >**功能介绍**</td>

<td rowspan="1" colSpan="1" >**功能 State**</td>

<td rowspan="1" colSpan="1" >**实现指南**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**实现观众音频连麦**</td>

<td rowspan="1" colSpan="1" >观众申请上麦，与主播进行实时音频互动。</td>

<td rowspan="1" colSpan="1" >[CoGuestState](https://liteav.sdk.qcloud.com/doc/product/tuikit/atomic-x/uni-app/zh/v1.0/api/index.html#module-CoGuestState)</td>

<td rowspan="1" colSpan="1" >[实现观众连麦](https://write.woa.com/document/191656302875648000)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**添加弹幕聊天功能**</td>

<td rowspan="1" colSpan="1" >观众可以在语音聊天室发送和接收实时文字消息。</td>

<td rowspan="1" colSpan="1" >[BarrageState](https://liteav.sdk.qcloud.com/doc/product/tuikit/atomic-x/uni-app/zh/v1.0/api/index.html#module-BarrageState)</td>

<td rowspan="1" colSpan="1" >[实现弹幕功能](https://write.woa.com/document/193556011837247488)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**构建礼物赠送系统**</td>

<td rowspan="1" colSpan="1" >观众可以向主播赠送虚拟礼物，增加互动和趣味性。</td>

<td rowspan="1" colSpan="1" >[GiftState](https://liteav.sdk.qcloud.com/doc/product/tuikit/atomic-x/uni-app/zh/v1.0/api/index.html#module-GiftState)</td>

<td rowspan="1" colSpan="1" >[实现礼物功能](https://write.woa.com/document/193556022792466432)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**添加设置音效功能**</td>

<td rowspan="1" colSpan="1" >变声（童声 / 男声）、混响（KTV 等）、耳返调节，实时切换特效。</td>

<td rowspan="1" colSpan="1" >[AudioEffectState](https://liteav.sdk.qcloud.com/doc/product/tuikit/atomic-x/uni-app/zh/v1.0/api/index.html#module-AudioEffectState)</td>

<td rowspan="1" colSpan="1" >[实现音效功能](https://write.woa.com/document/193586883758084096)</td>
</tr>
</table>


##  API 文档
<table>
<tr>
<td rowspan="1" colSpan="1" >**State**</td>

<td rowspan="1" colSpan="1" >**功能描述**</td>

<td rowspan="1" colSpan="1" >**API 文档**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**LiveListState**</td>

<td rowspan="1" colSpan="1" >语音聊天室全生命周期管理：创建 / 加入 / 离开 / 销毁房间，查询房间列表，修改语音聊天室信息（名称、公告等），监听语音聊天室状态（如被踢出、结束）。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://liteav.sdk.qcloud.com/doc/product/tuikit/atomic-x/uni-app/zh/v1.0/api/index.html#module-LiveListState)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**DeviceState**</td>

<td rowspan="1" colSpan="1" >音视频设备控制：麦克风（开关 / 音量），设备状态实时监听。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://liteav.sdk.qcloud.com/doc/product/tuikit/atomic-x/uni-app/zh/v1.0/api/index.html#module-DeviceState)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**CoGuestState**</td>

<td rowspan="1" colSpan="1" >观众连麦管理：连麦申请 / 邀请 / 同意 / 拒绝，连麦成员权限控制（麦克风），状态同步。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://liteav.sdk.qcloud.com/doc/product/tuikit/atomic-x/uni-app/zh/v1.0/api/index.html#module-CoGuestState)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**CoHostState**</td>

<td rowspan="1" colSpan="1" >主播跨房连线：支持多布局模板（动态网格等），发起 / 接受 / 拒绝连线，连麦主播互动管理。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://liteav.sdk.qcloud.com/doc/product/tuikit/atomic-x/uni-app/zh/v1.0/api/index.html#module-CoHostState)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**GiftState**</td>

<td rowspan="1" colSpan="1" >礼物互动：获取礼物列表，发送 / 接收礼物，监听礼物事件（含发送者、礼物详情）。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://liteav.sdk.qcloud.com/doc/product/tuikit/atomic-x/uni-app/zh/v1.0/api/index.html#module-GiftState)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**BarrageState**</td>

<td rowspan="1" colSpan="1" >弹幕功能：发送文本 / 自定义弹幕，维护弹幕列表，实时监听弹幕状态。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://liteav.sdk.qcloud.com/doc/product/tuikit/atomic-x/uni-app/zh/v1.0/api/index.html#module-BarrageState)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**LikeState**</td>

<td rowspan="1" colSpan="1" >点赞互动：发送点赞，监听点赞事件，同步总点赞数。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://liteav.sdk.qcloud.com/doc/product/tuikit/atomic-x/uni-app/zh/v1.0/api/index.html#module-LikeState)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**LiveAudienceState**</td>

<td rowspan="1" colSpan="1" >观众管理：获取实时观众列表（ ID / 名称 / 头像），统计观众数量，监听观众进出事件。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://liteav.sdk.qcloud.com/doc/product/tuikit/atomic-x/uni-app/zh/v1.0/api/index.html#module-LiveAudienceState)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**AudioEffectState**</td>

<td rowspan="1" colSpan="1" >音频特效：变声（童声 / 男声）、混响（ KTV 等）、耳返调节，实时切换特效。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://liteav.sdk.qcloud.com/doc/product/tuikit/atomic-x/uni-app/zh/v1.0/api/index.html#module-AudioEffectState)</td>
</tr>
</table>


## 常见问题

### 代码变更后，没有效果或者编译报错？

引入 uni_modules 后，需要重新制作自定义基座，详情参见 [制作自定义基座流程](https://write.woa.com/document/187305564150689792)。

### 原生能力集成问题
- 问题：插件调用失败或无响应。

- 解决方案：

  - 必须打包自定义基座：在开发调试原生插件时，不能使用标准基座，必须通过 `HBuilderX` > 运行 > 运行到手机或模拟器 > 制作自定义基座，然后选择这个自定义基座来运行。

  - 检查权限：如本文档“准备工作”中所述，`manifest.json` manifest.json必须声明相机、麦克风等权限。

  - 查看原生日志：这是终极调试手段。通过 `Android Studio (Logcat)` 或 `Xcode (Console)` 查看设备的原生日志，通常能发现最直接的错误信息。
