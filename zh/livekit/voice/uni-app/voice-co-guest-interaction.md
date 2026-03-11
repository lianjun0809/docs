> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

**AtomicXCore** 提供了 [CoGuestState](https://liteav.sdk.qcloud.com/doc/product/tuikit/atomic-x/uni-app/zh/v1.0/api/index.html#module-CoGuestState) 和 [LiveSeatState](https://liteav.sdk.qcloud.com/doc/product/tuikit/atomic-x/uni-app/zh/v1.0/api/index.html#module-LiveSeatState) 模块，用于管理观众连麦的完整业务流程。您无需关心复杂的状态同步和信令交互，只需调用几个简单的方法，即可为您的直播添加强大的观众与主播音视频互动功能。本文档将指导您如何使用 `CoGuestState `和 `LiveSeatState`在您的应用中快速实现语音连麦功能。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100028028022/e508b7a6ba1c11f0a6c652540044a08e.png)


## 核心场景

`CoGuestState`和 `LiveSeatState`支持以下几个主流的场景：
- **观众申请上麦**：观众主动发起连麦请求，主播在收到请求后同意或拒绝。

- **主播邀请上麦**：主播可以主动向语聊房内的任意一位观众发起连麦邀请。

- **主播管理麦位**：主播可以对麦位上的用户进行踢人、闭麦、锁麦等操作。


## 实现步骤

### 步骤1：组件集成

请参考 [快速接入](https://write.woa.com/document/191656297444069376) 集成 **AtomicXCore**。

### 步骤2：实现观众申请上麦

#### 观众端实现

作为观众，您的核心任务是**发起申请、接收结果**和**主动下麦**。
1. **发起连麦申请**


   当用户点击界面上的“申请连麦”按钮时，调用 `applyForSeat` 方法。

   ``` typescript
   import { useCoGuestState } from "@/uni_modules/tuikit-atomic-x/state/CoGuestState";
   
   // 先获取要加入的语聊房 ID（liveID）。通常有以下几种方式：
   // 通过房间列表选择（可从 LiveListState 的 liveList 数据中获取）
    
   const liveID = "xxx" // 您当前加入语聊房的 liveID
   
   //通过 liveID 获取 CoGuestState 的实例
   const { applyForSeat } = useCoGuestState(liveID);
   
   // 用户点击“申请连麦”
   const handleRequestToConnect = () => {
       applyForSeat({ 
         liveID,
         seatIndex: -1, // 申请的麦位，申请上麦传 -1, 随机分配麦位
         timeout: 30, // 请求超时时间，例如 30s
       })
   } 
   ```
2. **监听主播的处理结果**


   通过  `addCoGuestGuestListener` 订阅`'onGuestApplicationResponded'` 事件，您可以接收到主播的处理结果。

   ``` typescript
   import { onMounted } from 'vue';
   import { useCoGuestState } from "@/uni_modules/tuikit-atomic-x/state/CoGuestState";
   import { useDeviceState } from "@/uni_modules/tuikit-atomic-x/state/DeviceState";
   const liveID = "xxx" // 您当前加入语聊房的 liveID
   const { addCoGuestGuestListener } = useCoGuestState(liveID);
   const { openLocalMicrophone } = useDeviceState(liveID);
     
   // 在页面初始化时订阅事件
   onMounted(() => {
       addCoGuestGuestListener(liveID, 'onGuestApplicationResponded', handleGuestApplicationResponded)
   })
    
   const handleGuestApplicationResponded = {
       callback: (event) => {
         const res = JSON.parse(event)
         if(res.isAccept){
           console.log('上麦申请被同意')
           // 1.打开麦克风
           openLocalMicrophone()
           // 2. 在此更新 UI，例如变更申请按钮状态，显示为连麦中
         } else {
           console.log('上麦申请被拒绝')
           // 弹窗提示用户申请被拒绝
         }
       }
   }
   ```
3. **主动下麦**


   当连麦观众想结束互动时，调用 `disConnect` 方法即可返回普通观众状态。

   ``` typescript
   import { useCoGuestState } from "@/uni_modules/tuikit-atomic-x/state/CoGuestState";
   const liveID = "xxx" // 您当前加入语聊房的 liveID
   const { disconnect } = useCoGuestState(liveID);
   
   // 用户点击“下麦”按钮
   const leaveSeat = () => {
       disconnect({
         liveID,
         success: () => {
           console.log('下麦成功')
         },
         fail: (error) => {
           console.log('下麦失败', error)
         }
       })
   }
   ```
4. **(可选) 取消申请**


   如果观众在主播处理前想撤回申请，可以调用 `cancelApplication` 。

   ``` typescript
   import { useCoGuestState } from "@/uni_modules/tuikit-atomic-x/state/CoGuestState";
   const liveID = "xxx" // 您当前加入的语聊房的 liveID
   const { cancelApplication } = useCoGuestState(liveID);
   
   // 用户在等待时，点击“取消申请”
   const handelCancelRequest = () => {
       cancelApplication({
         liveID,
         success: () => {
           console.log('取消申请成功')
         },
         fail: (error) => {
           console.log('取消申请失败', error)
         }
       })
   }
   ```

#### 主播端实现

作为主播，您的核心任务是**接收申请、展示申请列表**和**处理申请**。
1. **监听新的连麦申请**


   通过 `CoGuestHostListener` 订阅 `'onGuestApplicationReceived'` 事件您可以在有新观众申请时立即收到通知，并给出提示。

   ``` typescript
   import { onMounted } from 'vue';
   import { useCoGuestState } from "@/uni_modules/tuikit-atomic-x/state/CoGuestState";
   const liveID = "xxx" // 您当前语聊房的 liveID
   const { addCoGuestHostListener } = useCoGuestState(liveID);
   
   // 在页面初始化时订阅事件
   onMounted(() => {
       addCoGuestHostListener(liveID, 'onGuestApplicationReceived', handleGuestApplicationReceived)
   })
    
   const handleGuestApplicationReceived =  {
       callback: (event) => {
         const res = JSON.parse(event)
         console.log('收到观众的连麦申请')
         // 在此更新 UI，例如在"申请列表"按钮上显示红点
       }
   }
   ```
2. **展示申请列表**


   `CoGuestState` 会实时维护当前的申请者列表，数据本身是响应式数据，您可以直接在 UI 上使用。

   ``` typescript
   <template>
       // 在这里绘制您的 “申请者列表” UI
       <view v-for="audience in applicants" :key="audience?.userID">
         <text>{ audience.userName }</text>
         <text>{ audience.userID }</text>
       </view>
   </template>
   <script setup>
       import { useCoGuestState } from "@/uni_modules/tuikit-atomic-x/state/CoGuestState";
       const liveID = "xxxx" // 您当前语聊房的 liveID
       const { applicants } = useCoGuestState(liveID);
   </script>
   ```
3. **处理连麦申请**


   当您在列表中选择一位观众并点击“同意”或“拒绝”时，调用相应的方法。

   ``` typescript
   import { useCoGuestState } from "@/uni_modules/tuikit-atomic-x/state/CoGuestState";
   const liveID = "xxx" // 您当前语聊房的 liveID
   const { acceptApplication, rejectApplication } = useCoGuestState(liveID);
   
   // 主播点击“同意”按钮，传入申请者的 userID
   const handleAccept = (userID: string) => {
       acceptApplication({
         liveID,
         userID,
         success: () => {
           console.log('已同意${userID}的上麦申请')
         },
         fail: (error) => {
           console.log('同意${userID}的上麦申请失败', error)
         }
   
       })
   }
   
   // 主播点击“拒绝”按钮，传入申请者的 userID
   const handleReject = (userID: string) => {
       rejectApplication({
         liveID,
         userID,
         success: () => {
           console.log('已拒绝${userID}的上麦申请')
         },
         fail: (error) => {
           console.log('拒绝${userID}的上麦申请失败', error)
         }
       })
   }
   ```

### 步骤3：实现主播邀请上麦

#### 主播端实现
1. **向观众发起邀请**


   当主播在观众列表中选择某人并点击“邀请连麦”时，调用 `inviteToSeat` 方法。

   ``` typescript
   import { useCoGuestState } from "@/uni_modules/tuikit-atomic-x/state/CoGuestState";
   const liveID = "xxx" // 您当前语聊房的 liveID
   const { inviteToSeat } = useCoGuestState(liveID);
   
   // 主播选择观众并发起邀请
   const handleInviteToSeat = (userID: string) => {
       inviteToSeat({
         liveID,
         userID,
         seatIndex: -1, // 邀请的麦位，传 -1, 随机分配麦位
         timeout: 30, // 超时时间
         success: () => {
           console.log('已向观众 ${userID} 发送上麦邀请，请等待回应...')
         },
         fail: (error) => {
           console.log('向观众 ${userID} 发送上麦邀请失败', error)
         }
       })
   }
   ```
2. **监听观众的回应**


   通过 `CoGuestHostListener` 订阅 `'onHostInvitationResponded'` 事件。

   ``` typescript
   import { onMounted } from 'vue';
   import { useCoGuestState } from "@/uni_modules/tuikit-atomic-x/state/CoGuestState";
   const liveID = "xxx" // 您当前语聊房的 liveID
   const { addCoGuestHostListener } = useCoGuestState(liveID);
   
   // 在页面初始化时订阅事件 
   onMounted(() => {
       addCoGuestHostListener(liveID, 'onHostInvitationResponded', handleHostInvitationResponded)
   })
    
   const handleHostInvitationResponded =  {
       callback: (event) => {
         const res = JSON.parse(event)
         if(res.isAccept){
           console.log('观众 ${res.guestUser.userName} 接受了您的邀请')
         } else {
           console.log('观众 ${res.guestUser.userName} 拒绝了您的邀请')
         }
       }
   }
   ```

#### 观众端实现
1. **接收主播的邀请**


   通过 `addCoGuestGuestListener` 订阅 `'onHostInvitationReceived'` 事件。

   ``` typescript
   import { onMounted } from 'vue';
   import { useCoGuestState } from "@/uni_modules/tuikit-atomic-x/state/CoGuestState";
   const liveID = "xxx" // 您当前加入语聊房的 liveID
   const { addCoGuestGuestListener } = useCoGuestState(liveID);
   
   // 在页面初始化时订阅事件
   onMounted(() => {
       addCoGuestGuestListener(liveID, 'onHostInvitationReceived', handleHostInvitationReceived)
   })
    
   const handleHostInvitationReceived =  {
       callback: (event) => {
         // 在此弹出一个对话框，让用户选择“接受”或“拒绝”
       }
   }
   ```
2. **响应邀请**


   当用户在弹出的对话框中做出选择后，调用相应的方法。

   ``` typescript
   import { useCoGuestState } from "@/uni_modules/tuikit-atomic-x/state/CoGuestState";
   import { useDeviceState } from "@/uni_modules/tuikit-atomic-x/state/DeviceState";
   const liveID = "xxx" // 您当前加入的语聊房的 liveID
   const { acceptInvitation, rejectInvitation } = useCoGuestState(liveID);
   const { openLocalMicrophone, openLocalCamera } = useDeviceState(liveID);
   
   const inviterID = "发起邀请的主播ID" // 从 onHostInvitationReceived 事件中获取
   
   // 用户点击“接受”，
   const handleAccept = () => {
       acceptInvitation({
         liveID,
         inviterID,
         success: () => {
           openLocalMicrophone()
           openLocalCamera({isFront: true})
         },
         fail: (error) => {
           console.log('接受邀请失败', error)
         }
       })
   }
   ```

## 功能进阶

当用户上麦后，主播可能需要对麦位进行管理。以下功能主要由 `LiveSeatState` 提供，它可以与 `CoGuestState` 协同工作。

### 麦上用户自行开/关麦

麦上用户（包括主播自己）可以通过 `LiveSeatState` 提供的接口来控制自己的麦克风静音状态。

#### 实现方式：
1. **静音：**调用 `muteMicrophone()` 方法。这是一个无回调的单向请求。

2. **解除静音**：调用 `unmuteMicrophone(success: fail:) `方法。


#### 示例代码：
``` typescript
import { useLiveSeatState } from "@/uni_modules/tuikit-atomic-x/state/LiveSeatState";

//通过 liveID 获取 LiveSeatState 的实例
const { muteMicrophone, unmuteMicrophone } = useLiveSeatState(liveID);

//静音
const muteMic = () => {
    muteMicrophone()
}

//解除静音
const unmuteMic = () => {
    unmuteMicrophone({
      success: () => {
        console.log('解除静音成功')
      },
      fail: (error) => {
        console.log('解除静音失败', error)
      }
    })
}
```

#### unmuteMicrophone 接口参数：
<table>
<tr>
<td rowspan="1" colSpan="1" >**参数**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`success`</td>

<td rowspan="1" colSpan="1" >`Function`</td>

<td rowspan="1" colSpan="1" >解除静音的回调</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`fail`</td>

<td rowspan="1" colSpan="1" >`Function`</td>

<td rowspan="1" colSpan="1" >解除静音失败的回调。</td>
</tr>
</table>


### 主播远程控制麦上用户开麦或关麦

主播可以对其他麦上用户进行“强制静音”或“邀请开麦”的操作。

#### 实现方式：
1. **强制静音（锁定）**：主播调用 `closeRemoteMicrophone` 会强制关闭对方的麦克风，并锁定对方的麦克风权限。被静音的用户会收到 `'onLocalMicrophoneClosedByAdmin'` 事件，此时其本地的“打开麦克风”按钮应变为不可点击状态。

2. **邀请开麦（解锁）**：主播调用 `openRemoteMicrophone` 并非强制打开对方麦克风，而是解除对方的“锁定状态”，允许对方自行开麦。此时，被操作的用户会收到 `onLocalMicrophoneOpenedByAdmin` 事件，其本地的“打开麦克风”按钮应恢复为可点击状态，但用户仍处于静音中。

3. **用户自行开麦**：用户在收到“解除锁定”的通知后，必须主动调用 `LiveSeatState` 的 `unmuteMicrophone()`方法解除静音，才能让房间内其他人听到自己的声音。


#### 示例代码：

##### 主播端：
``` typescript
import { useLiveSeatState } from "@/uni_modules/tuikit-atomic-x/state/LiveSeatState";

//通过 liveID 获取 LiveSeatState 的实例
const { openRemoteMicrophone, closeRemoteMicrophone } = useLiveSeatState(liveID);
const targetUserID = "userA"

// 1. 强制静音 userA 并锁定
const closeRemoteMic = () => {
    closeRemoteMicrophone({
      liveID: 'xxx', // 当前语聊房 liveID
      userID: targetUserID,
      success: () => {
        console.log('已将 ${targetUserID} 静音并锁定')
      },
      fail: (error) => {
        console.log('静音并锁定 ${targetUserID} 失败', error)
      }
    })
}

// 2. 解锁 userA 的麦克风权限（此时 userA 依然是静音状态）
const openRemoteMic = () => {
    openRemoteMicrophone({
      liveID: 'xxx', // 当前语聊房 liveID
      userID: targetUserID,
      success: () => {
        console.log('已邀请 ${targetUserID} 打开麦克风 （已解锁）')
      },
      fail: (error) => {
        console.log('静音并锁定 ${targetUserID} 失败', error)
      }
    })
}
```

##### 观众端：
``` typescript
import { onMounted } from 'vue';
import { useLiveSeatState } from "@/uni_modules/tuikit-atomic-x/state/LiveSeatState";
const liveID = "xxxx" // 您当前加入语聊房的 liveID

//通过 liveID 获取 LiveSeatState 的实例
const { addLiveSeatEventListener } = useLiveSeatState(liveID);

// userA 监听主播的操作,在页面初始化时订阅事件
onMounted(() => {
    addLiveSeatEventListener(liveID, 'onLocalMicrophoneClosedByAdmin', {
      callback: () => {
        console.log('被主播静音了')
        // 可以在此进行弹框提示
      }
    })
    addLiveSeatEventListener(liveID, 'onLocalMicrophoneOpenedByAdmin', {
      callback: () => {
        console.log('主播已解除静音锁定')
        // 可以在此进行弹框提示
      }
    })
})
```

#### closeRemoteMicrophone 接口参数：
<table>
<tr>
<td rowspan="1" colSpan="1" >**参数**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`liveID`</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >当前语聊房的`liveID`。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`userID`</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >被操作的用户`userID`。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`success`</td>

<td rowspan="1" colSpan="1" >`Function`</td>

<td rowspan="1" colSpan="1" >静音成功的回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`fail`</td>

<td rowspan="1" colSpan="1" >`Function`</td>

<td rowspan="1" colSpan="1" >静音失败的回调。</td>
</tr>
</table>


#### openRemoteMicrophone 接口参数：
<table>
<tr>
<td rowspan="1" colSpan="1" >**参数**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`liveID`</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >当前语聊房的`liveID`。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`userID`</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >被操作的用户`userID`。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`success`</td>

<td rowspan="1" colSpan="1" >`Function`</td>

<td rowspan="1" colSpan="1" >解除静音成功的回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`fail`</td>

<td rowspan="1" colSpan="1" >`Function`</td>

<td rowspan="1" colSpan="1" >解除静音失败的回调。</td>
</tr>
</table>


### 主播将麦上用户踢下麦位

#### 实现方式：
1. **踢人下麦**：主播可以调用 `kickUserOutOfSeat` 方法，强制将指定用户踢下麦位。

2. **监听事件通知**：被踢下麦的用户会收到 `'onKickedOffSeat'` 事件通知。


#### 示例代码：
``` typescript
import { onMounted } from 'vue';
import { useLiveSeatState } from "@/uni_modules/tuikit-atomic-x/state/LiveSeatState";

//通过 liveID 获取 LiveSeatState 的实例
const { kickUserOutOfSeat, addLiveSeatEventListener } = useLiveSeatState(liveID);

// 假设要踢走 "userB"
const targetUserID = "userB"

const kickOutOfSeat = () => {
    kickUserOutOfSeat({
      liveID: 'xxx', // 当前语聊房的 liveID
      userID: targetUserID,
      success: () => {
        console.log('已将 ${targetUserID} 踢下麦位')
      },
      fail: (error) => {
        console.log('踢人失败', error)
      }
    })
}

onMounted(() => {
    // "userB" 收到被踢下麦事件
    addLiveSeatEventListener(liveID, 'onKickedOffSeat', {
      callback: () => {
        console.log('被主播踢下麦')
        // 可以在此进行弹框提示
      }
    })
})
```

#### kickUserOutOfSeat 接口参数：
<table>
<tr>
<td rowspan="1" colSpan="1" >**参数**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`liveID`</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >当前语聊房的`liveID`。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`userID`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >被踢下麦的用户`userID`。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`success`</td>

<td rowspan="1" colSpan="1" >`Function`</td>

<td rowspan="1" colSpan="1" >踢下麦成功的回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`fail`</td>

<td rowspan="1" colSpan="1" >`Function`</td>

<td rowspan="1" colSpan="1" >踢下麦失败的回调。</td>
</tr>
</table>


### 主播锁定和解锁麦位

主播可以锁定或解锁某个麦位。

#### 实现方式：
1. **锁定麦位**：主播可调用 `lockSeat` 方法锁定指定索引的麦位，麦位被锁定后，观众无法通过 `applyForSeat` 或`takeSeat` 占用该麦位。

2. **解锁麦位**：调用 `unlockSeat` 可以解锁麦位，解锁后该麦位可以再次被占用。


#### 示例代码：
``` typescript
import { useLiveSeatState } from "@/uni_modules/tuikit-atomic-x/state/LiveSeatState";

//通过 liveID 获取 LiveSeatState 的实例
const { lockSeat, unlockSeat } = useLiveSeatState(liveID);


// 锁定2号麦位
const lock = () => {
    lockSeat({
      liveID: 'xxx', // 当前语聊房的 liveID
      seatIndex: 2,
      success: () => {
        console.log('已将 2 号麦位锁定')
      },
      fail: (error) => {
        console.log('锁定麦位失败', error)
      }
    })
}

// 解锁2号麦位
const unlock = () => {
    unlockSeat({
      liveID: 'xxx', // 当前语聊房的 liveID
      seatIndex: 2,
      success: () => {
        console.log('已将 2 号麦位解锁')
      },
      fail: (error) => {
        console.log('解锁麦位失败', error)
      }
    })
}
```

#### lockSeat 接口参数：
<table>
<tr>
<td rowspan="1" colSpan="1" >**参数**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`liveID`</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >当前语聊房的`liveID`。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`seatIndex`</td>

<td rowspan="1" colSpan="1" >`number`</td>

<td rowspan="1" colSpan="1" >需要锁定的麦位索引。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`success`</td>

<td rowspan="1" colSpan="1" >`Function`</td>

<td rowspan="1" colSpan="1" >锁麦成功的回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`fail`</td>

<td rowspan="1" colSpan="1" >`Function`</td>

<td rowspan="1" colSpan="1" >锁麦失败的回调。</td>
</tr>
</table>


#### unlockSeat 接口参数：
<table>
<tr>
<td rowspan="1" colSpan="1" >**参数**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`liveID`</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >当前语聊房的`liveID`。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`seatIndex`</td>

<td rowspan="1" colSpan="1" >`number`</td>

<td rowspan="1" colSpan="1" >需要解锁的麦位索引。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`success`</td>

<td rowspan="1" colSpan="1" >`Function`</td>

<td rowspan="1" colSpan="1" >解锁麦位成功的回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`fail`</td>

<td rowspan="1" colSpan="1" >`Function`</td>

<td rowspan="1" colSpan="1" >解锁麦位失败的回调。</td>
</tr>
</table>


### 移动麦位

主播和普通上麦用户可以调用 `moveUserToSeat(userID:targetIndex:policy:success:fail:)` 移动麦位。

#### 实现方式：
1. **主播移动麦位**：主播可以调用此接口将任意用户移动到指定麦位。此时 `userID` 传入目标用户的 ID，`targetIndex`是目标麦位索引，`policy` 参数来指定如果目标麦位有人时的移动策略，详细参见 [接口参数](https://liteav.sdk.qcloud.com/doc/product/tuikit/atomic-x/uni-app/zh/v1.0/api/interface.html#MoveUserToSeatOptions) 说明。

2. **普通上麦用户移动自己麦位**：普通上麦用户也可以调用此接口来移动自己。此时 `userID` 必须传入用户自己的 ID，`targetIndex` 传入想去的新麦位索引，此时`policy` 参数无效，如果目标麦位有人时会报错并停止移动。


#### 示例代码：
``` typescript
import { useLiveSeatState } from "@/uni_modules/tuikit-atomic-x/state/LiveSeatState";

//通过 liveID 获取 LiveSeatState 的实例
const { moveUserToSeat } = useLiveSeatState(liveID);

const moveSeat = () => {
    moveUserToSeat({
      liveID: 'xxx', // 当前语聊房 liveID
      userID: "userC",
      targetIndex: newSeatIndex, // 目标麦位
      policy: 'FORCE_REPLACE',
      success: () => {
        console.log('已成功移动到 ${newSeatIndex} 号麦位')
      },
      fail: (error) => {
        console.log('换座失败', error)
      }
    })
}
```

#### moveUserToSeat 接口参数：
<table>
<tr>
<td rowspan="1" colSpan="1" >**参数**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`userID`</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >需要移麦的用户`userID`。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`targetIndex`</td>

<td rowspan="1" colSpan="1" >`number`</td>

<td rowspan="1" colSpan="1" >目标麦位索引。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`policy`</td>

<td rowspan="1" colSpan="1" >`string`</td>

<td rowspan="1" colSpan="1" >目标麦位有人时的移动策略枚举：<br>- `'ABORT_WHEN_OCCUPIED'`：目标麦位有人时放弃移动（默认策略）​​<br>- `'FORCE_REPLACE'`：强制替换目标麦位上的用户​​，被替换的用户将会被踢下麦<br>- `'SWAP_POSITION'`：与目标麦位用户交换位置​​。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`success`</td>

<td rowspan="1" colSpan="1" >`Function`</td>

<td rowspan="1" colSpan="1" >移动麦位成功的回调。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`fail`</td>

<td rowspan="1" colSpan="1" >`Function`</td>

<td rowspan="1" colSpan="1" >移动麦位失败的回调。</td>
</tr>
</table>


## API 文档

关于 [CoGuestState](https://liteav.sdk.qcloud.com/doc/product/tuikit/atomic-x/uni-app/zh/v1.0/api/index.html#module-CoGuestState) 和 [LiveSeatState](https://liteav.sdk.qcloud.com/doc/product/tuikit/atomic-x/uni-app/zh/v1.0/api/index.html#module-LiveSeatState) 及其相关类的所有公开接口、属性和方法的详细信息，请参阅 [AtomicXCore](https://write.woa.com/document/192223419814899712) 框架的官方 API 文档。本指南使用到的相关 Store 如下：
<table>
<tr>
<td rowspan="1" colSpan="1" >**State**</td>

<td rowspan="1" colSpan="1" >**功能描述**</td>

<td rowspan="1" colSpan="1" >**API 文档**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >CoGuestState</td>

<td rowspan="1" colSpan="1" >观众连麦管理：连麦申请 / 邀请 / 同意 / 拒绝，连麦成员权限控制（麦克风 / 摄像头），状态同步。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://liteav.sdk.qcloud.com/doc/product/tuikit/atomic-x/uni-app/zh/v1.0/api/index.html#module-CoGuestState)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >LiveSeatState</td>

<td rowspan="1" colSpan="1" >麦位管理：静音/解除静音，锁定/解锁麦位，踢人下麦、远程控制麦上用户麦克风，麦列表状态监听</td>

<td rowspan="1" colSpan="1" >[API 文档](https://liteav.sdk.qcloud.com/doc/product/tuikit/atomic-x/uni-app/zh/v1.0/api/index.html#module-LiveSeatState)</td>
</tr>
</table>


## 常见问题

### 语音房连麦和视频直播连麦的实现有何不同？

两者的主要区别在于业务形态与 UI 展现：
- 视频直播：核心是视频画面。您会使用 `LiveCoreView` 作为核心组件来渲染主播和连麦观众的视频流。UI 的重点是处理视频画面的布局、大小，以及通过 在视频流上添加挂件（如昵称、占位图）。您可以同时打开摄像头，麦克风。

- 语音房（语聊房）：核心是麦位网格。您不会使用 `LiveCoreView`，而是会基于 `LiveSeatState` 的数据（特别是 `seatList`）来构建一个网格 UI 。UI 的重点是实时显示每个麦位 `SeatInfo` 的状态：是否有人、是否静音、是否被锁定 ，以及是否正在说话。您只需要打开麦克风。


### 如何在 UI 上实时刷新麦位信息（如是否有人、是否静音）？

您应该订阅 `LiveSeatState` 中的 `seatList` 属性，它是一个`[SeatInfo]` 数组类型的响应式数据，每当数组变化时都会通知您重新渲染麦位列表。遍历此数组，您可以：
- 通过 `seatInfo.userInfo` 来获取麦位上用户信息。

- 通过 `seatInfo.isLocked`判断麦位是否被锁定。

- 通过 `seatInfo.userInfo.microphoneStatus` 判断麦上用户的麦克风状态。


### LiveSeatState 和 DeviceState  都有麦克风接口，它们有何区别？

这是一个非常重要的问题。`DeviceState` 管理的是物理设备，而 `LiveSeatState` 管理的是麦位业务（即音频流）。

`DeviceState`：
- `openLocalMicrophone`：向系统请求权限并启动麦克风设备进行音频采集。这是一个“重”操作。

- `closeLocalMicrophone`：停止音频采集并释放麦克风设备。


   `LiveSeatState`：

- `muteMicrophone`：静音。停止向远端发送本地的音频流，但麦克风设备本身仍在运行。

- `unmuteMicrophone`：解除静音。恢复向远端发送音频流。


   推荐的工作流程：您应该遵循“设备只开一次，麦上只用静音切换”的原则

1. **上麦时**：当观众成功上麦，调用一次 `openLocalMicrophone` 来启动设备。

2. **在麦上时**：用户在麦位上所有的“开麦”和“闭麦”操作，都应该调用 `unmuteMicrophone` 和 `muteMicrophone` 来控制上行音频流的通断。

3. **下麦时**：当用户下麦（例如调用 `disconnect` ），调用 `closeLocalMicrophone` 来释放设备。




