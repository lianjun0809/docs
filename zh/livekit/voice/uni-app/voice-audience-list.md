> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

`LiveAudienceState` 是 `AtomicXCore` 中专门负责管理语聊房观众信息的模块。通过 `LiveAudienceState`，您可以为您的直播应用构建一套完整的观众列表及管理系统。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100028028022/ef4d5ed8bbbf11f085a55254007c27c5.png)


## 核心功能
- **实时观众列表**：获取并展示当前在语聊房内的所有观众信息。

- **观众人数统计**：实时获取当前语聊房的准确观众总数。

- **观众动态监听**：通过事件订阅，实时感知观众的加入和离开。

- **管理员权限**：主播可以将普通观众设为管理员，或撤销其管理员身份。

- **房间管理**：主播或管理员可以将任意普通观众请出（踢出）语聊房。


## 实现步骤

### 步骤1：组件集成

请参考 [开始直播](https://write.woa.com/document/191127271985012736) 集成 **AtomicXCore**，完成接入。

### 步骤2：初始化并获取观众列表

获取一个与当前语聊房 liveID 绑定的 `LiveAudienceState` 实例，并主动拉取一次当前的观众列表，用于首次展示。
``` typescript
import { useLiveAudienceState } from "@/uni_modules/tuikit-atomic-x/state/LiveAudienceState";
import { onMounted, watch } from 'vue';

// liveID 是语聊房的唯一标识
const liveID = 'your_live_id'; // 替换为实际的语聊房 liveID

// 通过 liveID 获取 LiveAudienceState 的实例
const { fetchAudienceList, audienceList } = useLiveAudienceState(liveID)

onMounted(() => {
    fetchAudienceList({
      liveID: 'xxx', // 当前语聊房的 liveID
      success: () => {        
        // 成功后，响应式数据会自动更新
        console.log('首次拉取观众列表成功')
      },
      fail: (error) => {
        console.log('首次拉取观众列表失败', error)
      }
    })
})

// 监听 audienceList 的实时变更，用于驱动 UI 变更
watch(audienceList, (newVal, oldVal) => {
    console.log(newVal)
})

// ... 后续代码 
```

### 步骤3：监听观众列表状态与实时动态

订阅和监听 `audienceState` 的 `event` 和 `响应式数据`，用来接收全量列表快照和实时的观众进出事件，从而驱动 UI 更新。
``` typescript
import { useLiveAudienceState } from "@/uni_modules/tuikit-atomic-x/state/LiveAudienceState";
import { onMounted, watch } from 'vue';

const liveID = 'your_live_id'; // 替换为实际的语聊房 liveID
//通过 liveID 获取 LiveAudienceState 的实例
const { audienceList, audienceCount, addAudienceListener, removeAudienceListener } = useLiveAudienceState(liveID)

// 监听 audienceList 的实时变更，用于驱动 UI 更新
watch(audienceList, (newVal, oldVal) => {
    console.log(newVal)
})

// 监听 audienceCount 的实时变更，用于驱动 UI 更新
watch(audienceCount, (newVal, oldVal) => {
    console.log(newVal)
})

onMounted(() => {
    addAudienceListener( liveID, 'onAudienceJoined', 
      { callback: (event) => {
        const newAudience = JSON.parse(event)
        console.log("观众 ${newAudience.userName} 加入了语聊房")
      }
    })
    
    addAudienceListener( liveID, 'onAudienceLeft',
      { callback: (event) => {
        const departedAudience = JSON.parse(event)
        console.log("观众 ${departedAudience.userName} 离开了语聊房")
      }
    })
})
```

### 步骤4：管理观众（踢人与设置管理员）

作为主播或管理员，对语聊房内的观众进行管理操作。

#### 4.1 将观众踢出语聊房

调用 `kickUserOutOfRoom` 接口可以将指定用户请出语聊房。
``` typescript
import { useLiveAudienceState } from "@/uni_modules/tuikit-atomic-x/state/LiveAudienceState";

// liveID 是语聊房的唯一标识
const liveID = 'your_live_id'; // 替换为实际的语聊房 liveID

//通过 liveID 获取 LiveAudienceState 的实例
const { kickUserOutOfRoom } = useLiveAudienceState(liveID)

const kickOut = () => {
    kickUserOutOfRoom({
      liveID: 'xxx', // 当前语聊房的 liveID
      userID: 'xxx', // 想要踢出成员的 userID
      success: () => {
        console.log("成功将用户 ${userID} 踢出房间")
        // 踢出成功后，您会收到 onAudienceLeft 事件
      },
      fail: (error) => {
        console.log("将用户 ${userID} 踢出房间失败", error)
      } 
    })
}
```

#### 4.2 设置/撤销管理员

通过 `setAdministrator` 和 `revokeAdministrator` 接口可以管理用户的管理员身份。
``` typescript
import { useLiveAudienceState } from "@/uni_modules/tuikit-atomic-x/state/LiveAudienceState";

// liveID 是语聊房的唯一标识
const liveID = 'your_live_id'; // 替换为实际的语聊房 liveID

//通过 liveID 获取 LiveAudienceState 的实例
const { setAdministrator, revokeAdministrator } = useLiveAudienceState(liveID)

// 将用户设为管理员
const promoteToAdmin = () => {
    setAdministrator({
      liveID: 'xxx', // 当前语聊房的 liveID
      userID: 'xxx', // 想要设为管理员的 userID 
      success: () => {
        console.log("成功将用户 ${userID} 设为管理员")
      },
      fail: (error) => {
        console.log("将用户 ${userID} 设为管理员失败", error)
      }
    })
}

// 撤销用户的管理员身份
const revokeAdmin = () => {
    revokeAdministrator({
      liveID: 'xxx', // 当前语聊房的 liveID
      userID: 'xxx', // 想要撤销管理员的 userID 
      success: () => {
        console.log("成功将用户 ${userID} 的管理员身份撤销")
      },
      fail: (error) => {
        console.log("将用户 ${userID} 设为管理员身份撤销失败", error)
      }
    })

}
```

## 功能进阶

### 在弹幕区展示观众入场欢迎语

当有新观众进入语聊房时，弹幕/聊天区域会在本地自动显示一条欢迎消息，例如：“欢迎 [用户昵称] 进入语聊房”。

#### 实现方式

我们通过订阅 `LiveAudienceState` 的观众加入事件（ `'onAudienceJoined'` ）来获取新观众加入的实时通知。一旦事件触发，我们便提取出新观众的昵称信息，然后立即调用 `BarrageState` 的本地插入接口 `appendLocalTip`。
``` typescript
import { useLiveAudienceState } from "@/uni_modules/tuikit-atomic-x/state/LiveAudienceState";
import { useBarrageState } from '@/uni_modules/tuikit-atomic-x/state/BarrageState';
import { onMounted } from 'vue';

// liveID 是语聊房的唯一标识
const liveID = 'your_live_id'; // 替换为实际的语聊房 liveID

//通过 liveID 获取 LiveAudienceState 的实例
const { addAudienceListener, removeAudienceListener } = useLiveAudienceState(liveID)
//通过 liveID 获取 BarrageState 的实例
const { appendLocalTip } = useBarrageState(liveID)

onMounted(() => {
    addAudienceListener(liveID, 'onAudienceJoined', 
      { callback: (event) => {
        const newAudience = JSON.parse(event)
        // 创建一条本地提示消息
        let welcomeTip = {}   
        welcomeTip.liveID = liveID,
        welcomeTip.sender = { userID: 'xxx' },
        welcomeTip.sequence = Date.now(),
        welcomeTip.timestampInSecond = Date.now(),
        welcomeTip.messageType = 'TEXT',
        welcomeTip.textContent = "欢迎 ${newAudience.userName} 进入语聊房！"
        // 调用 BarrageStore 的接口将其插入弹幕列表
        appendLocalTip(welcomeTip)
        console.log("观众 ${newAudience.userName} 加入了语聊房")
       }
    })
})
```

## API 文档

关于 [LiveAudienceState](https://liteav.sdk.qcloud.com/doc/product/tuikit/atomic-x/uni-app/zh/v1.0/api/index.html#module-LiveAudienceState) 及其相关类的所有公开接口、属性和方法的详细信息，请参阅随 [AtomicXCore](https://write.woa.com/document/192223419814899712) 框架的官方 API 文档。本文档使用到的相关 State 如下：
<table>
<tr>
<td rowspan="1" colSpan="1" >**State**</td>

<td rowspan="1" colSpan="1" >**功能描述**</td>

<td rowspan="1" colSpan="1" >**API 文档**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >LiveAudienceState</td>

<td rowspan="1" colSpan="1" >观众管理：获取实时观众列表（ID / 名称 / 头像），统计观众数量，监听观众进出事件。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://liteav.sdk.qcloud.com/doc/product/tuikit/atomic-x/uni-app/zh/v1.0/api/index.html#module-LiveAudienceState)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >BarrageState</td>

<td rowspan="1" colSpan="1" >弹幕功能：发送文本 / 自定义弹幕，维护弹幕列表，实时监听弹幕状态。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://liteav.sdk.qcloud.com/doc/product/tuikit/atomic-x/uni-app/zh/v1.0/api/index.html#module-BarrageState)</td>
</tr>
</table>


## 常见问题

### `LiveAudienceState` 中的在线人数（`audienceCount`）是如何更新的？时机和频率是怎样的？

`audienceCount` 的更新并非总是实时的，其机制如下：
- **主动进出房间**：当用户主动加入或正常退出语聊房时，在线人数的变更通知会即时触发。您会很快在 `LiveAudienceState` 中观察到 `audienceCount` 的变化。

- **异常掉线**：当用户因网络问题、应用崩溃等原因异常掉线时，系统需要通过心跳机制来判断其真实状态。只有当该用户连续 90 秒没有心跳后，系统才会判定其为离线，并触发人数变更通知。

- **更新机制与频率控制：**

  - 无论是即时触发还是延迟触发，所有的人数变更通知都是以消息的形式在房间内广播的。

  - 房间内每秒的消息总量有上限，单房间消息频控是**每秒 40 条消息**。

  - **关键点：**在“弹幕风暴”或礼物刷屏等消息流量极高的场景下，如果房间内的消息速率超过了 40条/秒 的阈值，为了保证核心消息（例如弹幕）的送达，**人数变更的消息可能会被频控策略丢弃**。


      **这对开发者意味着什么？**


      `audienceCount` 是一个非常接近实时的**高精度估算值**，但在极端高并发场景下，它可能存在短暂的延迟或数据丢失。因此，我们建议您将其用于 **UI 展示**，而不应作为计费、统计等需要绝对精准场景的唯一依据。


