> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

`GiftState` 是 `AtomicXCore` 中专门负责管理直播间礼物功能的模块。通过它，您可以为您的直播应用构建一套完整的礼物系统，实现丰富的营收和互动场景。
<table>
<tr>
<td rowspan="1" colSpan="1" >礼物面板</td>

<td rowspan="1" colSpan="1" >弹幕礼物</td>

<td rowspan="1" colSpan="1" >全屏礼物</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100028028022/92743423bbbc11f0b4c35254001c06ec.png)</td>

<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100028028022/98aa70f4bbbc11f0b4c35254001c06ec.png)</td>

<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100028028022/9c60d5edbbbc11f085a55254007c27c5.png)</td>
</tr>
</table>


## 核心功能
- **礼物列表获取**：从服务端拉取礼物面板所需的数据，包括礼物分类和礼物详情。

- **发送礼物**：观众可以向主播发送选定的礼物，并附带数量。

- **礼物事件广播**：实时接收房间内发生的礼物赠送事件，用于展示礼物动画和弹幕通知。


## 实现步骤

### 步骤1：组件集成

> **说明：**
> 

> 使用**礼物系统**要求开通TUILiveKit **多人连麦版**、**大规模直播版**，不同套餐中可配置的礼物数量有所不同，详细参见 [功能与计费说明](https://write.woa.com/document/141302177829593088) 中的**礼物系统**说明。
> 

- **视频直播**：请参考 [快速接入](https://write.woa.com/document/191127271985012736) 集成 **AtomicXCore**，完成接入。

- **语聊房**：请参考 [快速接入](https://write.woa.com/document/191656297444069376) 集成 **AtomicXCore**，完成接入。


### 步骤2：初始化并监听礼物事件

获取 `GiftState` 实例，并设置订阅者以接收礼物事件和礼物列表更新。

#### 实现方式:
1. **获取实例**：使用 `useGiftState(liveID)` 获取与当前直播间绑定的 `GiftState` 实例。

2. **订阅事件**：使用 `addGiftListener` 以订阅 `'onReceiveGift'`事件。

3. **监听状态**：监听 响应式数据`usableGifts `礼物列表，来驱动 `UI` 更新。


#### 代码示例:
``` typescript
import { useGiftState } from "@/uni_modules/tuikit-atomic-x/state/GiftState";
import { onMounted, watch } from 'vue';

// liveID 是语聊房的唯一标识
const liveID = 'your_live_id'; // 替换为实际的语聊房 liveID

// 通过 liveID 获取 GiftState 的实例
const { addGiftListener, usableGifts } = useGiftState(liveID);

onMounted(() => {
    addGiftListener(liveID, 'onReceiveGift', {
       callback: (event) => {
         const gift = JSON.parse(event)
         console.log('收到礼物', gift)
         // 在此进行礼物的处理逻辑，例如 svga 格式的礼物进行播放，其他格式的进行弹窗提示
       }
     })
})

// 监听 usableGifts 的实时变更，用于驱动 UI 变更
watch(usableGifts, (newVal, oldVal) => {
    console.log(newVal)
})
```

#### 礼物列表结构体参数
- `GiftCategory`**参数说明**

<table>
<tr>
<td rowspan="1" colSpan="1" >**参数**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`categoryID`</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >礼物分类的唯一 ID。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`name`</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >礼物分类的显示名称。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`desc`</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >礼物分类的描述信息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`extensionInfo`</td>

<td rowspan="1" colSpan="1" >`[string: string]`</td>

<td rowspan="1" colSpan="1" >扩展信息字段。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`giftList`</td>

<td rowspan="1" colSpan="1" >`[string]`</td>

<td rowspan="1" colSpan="1" >该分类下包含的 Gift 礼物对象数组。</td>
</tr>
</table>

- `Gift`** 参数说明**

<table>
<tr>
<td rowspan="1" colSpan="1" >**参数**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`giftID`</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >  礼物的唯一 ID。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`name`</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >  礼物的显示名称。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`desc`</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >  礼物的描述信息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`iconURL`</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >  礼物图标 URL。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`resourceURL`</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >  礼物动画资源 URL。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`level`</td>

<td rowspan="1" colSpan="1" >`number`</td>

<td rowspan="1" colSpan="1" >  礼物等级。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`coins`</td>

<td rowspan="1" colSpan="1" >`number`</td>

<td rowspan="1" colSpan="1" >  礼物价格。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`extensionInfo`</td>

<td rowspan="1" colSpan="1" >`[string: string]`</td>

<td rowspan="1" colSpan="1" >  扩展信息字段。</td>
</tr>
</table>


### 步骤3：获取礼物列表

调用 `refreshUsableGifts` 方法，从服务端拉取礼物数据。

#### 实现方式:
1. **调用接口**：在合适的时机（例如页面加载时）调用 `refreshUsableGifts()`。

2. **处理回调**：可选地处理 `success`，`fail` 回调以获知拉取结果。

3. **接收数据**：拉取成功后，通过步骤二中对 `usableGifts` 的监听，自动接收到更新后的 `usableGifts` 列表。


#### 代码示例:
``` typescript
import { useGiftState } from "@/uni_modules/tuikit-atomic-x/state/GiftState";
import { onMounted } from 'vue';
﻿
// liveID 是语聊房的唯一标识
const liveID = 'your_live_id'; // 替换为实际的语聊房 liveID

// 通过 liveID 获取 GiftState 的实例
const { addGiftListener, usableGifts } = useGiftState(liveID);
﻿
onMounted(() => {
    refreshUsableGifts({
      liveID: 'xxx', // 当前直播间的 liveID     
      success: () => {
        console.log('礼物列表拉取成功')
        // 成功后，state 响应式数据会自动更新
      },
      faile: (error) => {
        console.log('礼物列表拉取失败', error)
      }
    })
})
```

### 步骤4：发送礼物

当用户在礼物面板选择一个礼物并点击发送时，调用 `sendGift` 接口将礼物发送出去。

#### 实现方式:
1. **获取参数**：从 UI 获取用户选择的 `giftID` 和发送数量 `count`。

2. **调用接口**：调用 `sendGift(giftID,count)`。

3. **处理回调**：在 `fail` 回调中处理发送失败的情况（例如余额不足提示）；发送成功后的 UI 更新（动画、弹幕）应由 `'onReceiveGift'` 事件驱动。


#### 代码示例:
``` typescript

import { useGiftState } from "@/uni_modules/tuikit-atomic-x/state/GiftState";
﻿
// liveID 是语聊房的唯一标识
const liveID = 'your_live_id'; // 替换为实际的语聊房 liveID

// 通过 liveID 获取 GiftState 的实例
const { sendGift } = useGiftState(liveID);

// 用户发送一个礼物
const sendGift = () => {
    sendGift({
      liveID: 'xxx', // 当前直播间 liveID
      giftID: giftID,
      count: 1,
      success: () => {
        console.log('礼物 ${giftID} 发送成功')    
      },
      fail: (error) => { 
        console.log('礼物发送失败', error)
        // 可以在此提示用户，例如“余额不足”或“网络错误”
      },
    })
}
```

#### `sendGift`接口参数
<table>
<tr>
<td rowspan="1" colSpan="1" >**参数名**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`liveID`</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >当前直播间的`liveID`。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`giftID`</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >要发送的礼物的唯一 ID。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`count`</td>

<td rowspan="1" colSpan="1" >`number`</td>

<td rowspan="1" colSpan="1" >发送的数量。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`success`</td>

<td rowspan="1" colSpan="1" >`Function`</td>

<td rowspan="1" colSpan="1" >发送成功的回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`fail`</td>

<td rowspan="1" colSpan="1" >`Function`</td>

<td rowspan="1" colSpan="1" >发送失败的回调。</td>
</tr>
</table>


## 功能进阶

`GiftState` 的功能高度依赖于您的业务后台服务。本章将指导您如何通过服务端配置和客户端实现，构建功能丰富、体验卓越的礼物互动系统。

### **礼物素材配置**

您需要自定义直播间可用的礼物种类、分类、名称、图标、价格以及动画效果，以满足运营需求和品牌特色。

#### **实现方式 **
1. **服务端配置**：使用 LiveKit 服务端 REST API 管理礼物信息、分类、多语言等。请参考 [礼物配置指引文档](https://cloud.tencent.com/document/product/647/121321)。

2. **客户端拉取**：在客户端调用 `refreshUsableGifts` 获取配置数据。

3. **UI 展示**：使用拉取到的 `[GiftCategory]` 数据填充礼物面板。


#### **配置时序图**

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100028028022/bd9fcf8dbbbc11f0a808525400bf7822.png)


#### **涉及 REST API 接口一览**
<table>
<tr>
<td rowspan="1" colSpan="1" >接口分类</td>

<td rowspan="1" colSpan="1" >接口</td>

<td rowspan="1" colSpan="1" >请求示例</td>
</tr>

<tr>
<td rowspan="3" colSpan="1" >​礼物管理​</td>

<td rowspan="1" colSpan="1" >添加礼物信息</td>

<td rowspan="1" colSpan="1" >[请求示例](https://write.woa.com/document/180341527570997248)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >删除礼物信息</td>

<td rowspan="1" colSpan="1" >[请求示例](https://write.woa.com/document/180341544133693440)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >查询礼物信息</td>

<td rowspan="1" colSpan="1" >[请求示例](https://write.woa.com/document/180341539054186496)</td>
</tr>

<tr>
<td rowspan="3" colSpan="1" >礼物​分类管理​</td>

<td rowspan="1" colSpan="1" >添加礼物分类信息</td>

<td rowspan="1" colSpan="1" >[请求示例](https://write.woa.com/document/180807825764642816)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >删除指定礼物分类信息</td>

<td rowspan="1" colSpan="1" >[请求示例](https://write.woa.com/document/180807830209925120)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >获取指定礼物分类信息</td>

<td rowspan="1" colSpan="1" >[请求示例](https://write.woa.com/document/180807827909746688)</td>
</tr>

<tr>
<td rowspan="3" colSpan="1" >​礼物关系管理​</td>

<td rowspan="1" colSpan="1" >添加指定礼物分类和礼物间的关系</td>

<td rowspan="1" colSpan="1" >[请求示例](https://write.woa.com/document/180341551420928000)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >删除指定礼物分类和礼物间的关系</td>

<td rowspan="1" colSpan="1" >[请求示例](https://write.woa.com/document/180341562381627392)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >获取指定礼物分类下的礼物关系</td>

<td rowspan="1" colSpan="1" >[请求示例](https://write.woa.com/document/180341571868094464)</td>
</tr>

<tr>
<td rowspan="6" colSpan="1" >​礼物多语言​管理</td>

<td rowspan="1" colSpan="1" >添加礼物多语言信息</td>

<td rowspan="1" colSpan="1" >[请求示例](https://write.woa.com/document/180341579611611136)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >删除指定礼物多语言信息</td>

<td rowspan="1" colSpan="1" >[请求示例](https://write.woa.com/document/180341598501920768)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >获取礼物多语言信息</td>

<td rowspan="1" colSpan="1" >[请求示例](https://write.woa.com/document/180341588810166272)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >添加礼物分类多语言信息</td>

<td rowspan="1" colSpan="1" >[请求示例](https://write.woa.com/document/180341603609534464)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >删除指定礼物分类多语言信息</td>

<td rowspan="1" colSpan="1" >[请求示例](https://write.woa.com/document/180341624911425536)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >获取礼物分类多语言信息</td>

<td rowspan="1" colSpan="1" >[请求示例](https://write.woa.com/document/180341612525645824)</td>
</tr>
</table>


### 计费与送礼扣费流程

当观众赠送礼物时，需要确保其账户余额充足，并完成实际的扣费操作，然后才能触发礼物特效的播放和广播。

#### 实现方式
1. **后台配置回调**：在 LiveKit 后台配置您的自建计费系统的回调 URL。参考 [回调配置文档](https://write.woa.com/document/183772947196690432)。

2. **客户端发送**：客户端调用 `sendGift`。

3. **后台交互**：LiveKit 后台调用您的回调 URL，您的计费系统执行扣费并返回结果。

4. **结果同步**：扣费成功，AtomicXCore 广播 `'onReceiveGift'` 事件。扣费失败，`sendGift` 的 `fail` 收到错误。


#### 调用流程图

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100028028022/cb539aa9bbbc11f0a808525400bf7822.png)


#### 涉及 REST API 接口一览
<table>
<tr>
<td rowspan="1" colSpan="1" >接口</td>

<td rowspan="1" colSpan="1" >说明</td>

<td rowspan="1" colSpan="1" >请求示例</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >回调配置 - 发送礼物之前回调</td>

<td rowspan="1" colSpan="1" >客户后台可以通过该回调决定是否通过送礼前校验等场景</td>

<td rowspan="1" colSpan="1" >[调用示例](https://write.woa.com/document/183772947196690432)</td>
</tr>
</table>


### 实现全屏礼物动画播放

当直播间有用户（包括自己）发送了“火箭”、“嘉年华”等豪华礼物时，全屏播放一个酷炫的礼物动画（例如 SVGA 动画），营造热烈的氛围。

#### 实现方式

`AtomicXCore` 本身包含礼物动画播放器，您可以根据业务需求选择并集成第三方库。以下是两种方案的对比：
<table>
<tr>
<td rowspan="1" colSpan="1" >**对比项**</td>

<td rowspan="1" colSpan="1" >**内置方案 (SVGAPlayer)**</td>

<td rowspan="1" colSpan="1" >**高级方案 (TCEffectPlayerKit)**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >计费</td>

<td rowspan="1" colSpan="1" >免费 </td>

<td rowspan="1" colSpan="1" >付费 (需购买 License)，请参见 [付费指引](https://cloud.tencent.com/document/product/616/116461)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >集成方式</td>

<td rowspan="1" colSpan="1" >AtomicXCore 内置</td>

<td rowspan="1" colSpan="1" >需额外集成 TCEffectPlayerKit 并进行鉴权</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >动画格式支持</td>

<td rowspan="1" colSpan="1" >仅支持 SVGA</td>

<td rowspan="1" colSpan="1" >SVGA、PAG、WebP、Lottie、MP4 等多种格式</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >性能</td>

<td rowspan="1" colSpan="1" >建议 SVGA 文件 ≤ 10MB</td>

<td rowspan="1" colSpan="1" >支持更大的动画文件，复杂特效/多动画并发/低端机表现更优</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >推荐场景</td>

<td rowspan="1" colSpan="1" >礼物动画格式统一为 SVGA，且文件大小可控</td>

<td rowspan="1" colSpan="1" >需要支持多种动画格式，或对动画性能/设备兼容性有更高要求</td>
</tr>
</table>


本章节主要演示基础方案的集成。如果您选择高级方案，请参考 [TCEffectPlayer 集成指引](https://cloud.tencent.com/document/product/616/116474)。

#### 基础方案实现：使用 SVGAPlayer
1. **使用 SVGAPlayer**：在您的项目中，引入 `svga-player `组件

   ``` typescript
   <svga-player :url="xxx"></svga-player>
   ```
2. **监听礼物事件**：使用 `addGiftListener` 以订阅 `'onReceiveGift'`事件。

3. **解析并播放**：当收到 `'onReceiveGift'`事件时，检查 `gift.resourceURL`是否有效且指向一个 SVGA 文件。如果是，则将`gift.resourceURL`传给`svga-player` 进行播放


#### 代码示例
``` typescript
<template>
    <svga-player :url="giftUrl"></svga-player>
</template>

<script setup lang="ts">
import { useGiftState } from "@/uni_modules/tuikit-atomic-x/state/GiftState";
import { onMounted } from 'vue';

// 通过 liveID 获取 GiftState 的实例
const { addGiftListener } = useGiftState(liveID);
const giftUrl = ref('')

onMounted(() => {
    addGiftListener(liveID, 'onReceiveGift', {
       callback: (event) => {
         const gift = JSON.parse(event)
         if( gift.resourceURL ) {
           giftUrl.value = gift.resourceURL 
         }
       }
     })
})
</script>

```

### 在弹幕区展示礼物赠送消息

当有用户发送礼物时，不仅播放动画，同时在公屏弹幕区域显示一条系统消息，例如：“【观众昵称】送出了【礼物名称】x【数量】”，让所有观众都能看到。

#### 实现方式
1. **监听事件: **使用 `addGiftListener` 以订阅 `'onReceiveGift'`事件。

2. **获取弹幕 State**：使用 `useBarrageState(liveID)`获取与当前房间绑定的实例。

3. **拼接消息**：创建一条消息结构体，设置 `messageType = 'text'`，textContent 为拼接好的字符串（例如 “[`sender.userName`] 送出了 [`gift.name`] x [`count`]”）。

4. **本地插入**：调用 `barrageState`的`appendLocalTip(message: giftTip) `将消息插入本地列表。


#### 代码示例
``` typescript
import { useGiftState } from "@/uni_modules/tuikit-atomic-x/state/GiftState";
import { useBarrageState } from "@/uni_modules/tuikit-atomic-x/state/BarrageState";
import { onMounted } from 'vue';

// 通过 liveID 获取 GiftState 的实例
const { addGiftListener } = useGiftState(liveID);
// 通过 liveID 获取 BarrageState 的实例
const { appendLocalTip } = useBarrageState(liveID);

onMounted(() => {
    addGiftListener(liveID, 'onReceiveGift', {
       callback: (event) => {
         const gift = JSON.parse(event)
         let giftTip = {}
         const tipText = "${ gift.sender.userName } 送出了 ${gift.name} x ${gift.count}"
         giftTip.messageType = 'text'
         giftTip.textContent = tipText
         appendLocalTip({
           liveID: 'xxx', // 当前直播间 liveID
           message: giftTip
         })
         if( gift.resourceURL ) {
           giftUrl.value = gift.resourceURL 
         }
       }
     })
})
</script>
```

## API 文档

关于 [GiftState](https://liteav.sdk.qcloud.com/doc/product/tuikit/atomic-x/uni-app/zh/v1.0/api/index.html#module-GiftState) 及其相关类的所有公开接口、属性和方法的详细信息，请参阅随 [AtomicXCore](https://write.woa.com/document/192223419814899712) 框架的官方 API 文档。本指南使用到的相关 Store 如下：
<table>
<tr>
<td rowspan="1" colSpan="1" >**State**</td>

<td rowspan="1" colSpan="1" >**功能描述**</td>

<td rowspan="1" colSpan="1" >**API 文档**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GiftState</td>

<td rowspan="1" colSpan="1" >礼物互动：获取礼物列表，发送 / 接收礼物，监听礼物事件（含发送者、礼物详情）。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://liteav.sdk.qcloud.com/doc/product/tuikit/atomic-x/uni-app/zh/v1.0/api/index.html#module-GiftState)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >BarrageState</td>

<td rowspan="1" colSpan="1" >弹幕功能：发送文本 / 自定义弹幕，维护弹幕列表，实时监听弹幕状态。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://liteav.sdk.qcloud.com/doc/product/tuikit/atomic-x/uni-app/zh/v1.0/api/index.html#module-BarrageState)</td>
</tr>
</table>


## 常见问题

### `GiftState` 的礼物列表是空的，我该怎么办？

您必须主动调用 `refreshUsableGifts()`来从您的业务后台拉取礼物数据。这些礼物数据需要在您的业务后台通过服务端 REST API 进行配置。

### 如何实现礼物的多语言展示（例如中文、英文）？

`GiftState` 提供了 `setLanguage(language: string)`接口。您可以在 `refreshUsableGifts` 之前调用此方法，传入目标语言代码（例如 "en" 或 "zh-CN"）。服务端会根据此语言代码，返回对应语言的礼物名称和描述。

### 我调用 sendGift 发送了礼物，礼物动画为什么重复播放了两次？

`onReceiveGift` 事件是对房间内所有成员的广播（包括发送者自己）。如果您在 `sendGift` 的 `success` 成功回调里执行了一次UI操作，同时又在 `onReceiveGift` 订阅中执行了相同的 UI 操作，就会造成重复。
- **实践教程**：UI 的更新（例如播放动画、弹幕提示）只在 `onReceiveGift` 事件的订阅中处理。`sendGift` 的 `success` 回调仅用于处理发送失败的逻辑（例如提示用户“发送失败”或“余额不足”）。


### 礼物扣费逻辑在哪里实现？

礼物扣费逻辑完全由您的自建计费系统负责。`AtomicXCore` 通过后台回调机制与您的计费系统对接。客户端调用 `sendGift` 触发回调，您的后台服务完成扣费后，将结果返回给 `AtomicXCore` 后台，从而决定礼物事件是否广播。

### 送礼通知会被禁言或频控拦截吗？

不会。送礼通知（`'onReceiveGift'`事件）不受禁言或消息频控影响，确保可靠投递。

### 礼物动画播放卡顿怎么办？

请检查您的 `SVGA` 文件大小，基础播放器建议不要超过 10MB。如果文件过大或动画复杂，您可以考虑集成 `TUILiveKit` 提供的高级特效播放器，以获得更优的性能表现。



