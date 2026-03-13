> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

本文档将帮助您使用 **AtomicXCore SDK**的核心组件 [LiveCoreView](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.view/-live-core-view/index.html)，快速构建一个包含主播开播和观众观看功能的基础直播 App。

### **核心功能**

**LiveCoreView** 是一个专为直播场景设计的轻量级 `View` 组件，是您构建直播场景的核心，它封装了所有复杂的底层直播技术（如推拉流、连麦、音视频渲染）。您可以将 LiveCoreView 作为直播画面的"画布"，专注于上层 UI 与交互的开发。

通过下方的视图层级示意图，您可以直观了解 **LiveCoreView** 在直播界面中的位置和作用：

## 准备工作

### 步骤1：开通服务

请参见 开通服务，获取体验版或付费版 SDK。

### 步骤2：在当前项目中导入 AtomicXCore

**安装组件**：请在您的 **build.gradle** 文件中添加 `implementation 'com.tencent.atomicx:atomicxcore:latest'` 依赖，然后执行 **Gradle Sync**。
``` gradle
dependencies {
    implementation 'io.trtc.uikit:atomicx-core:latest.release'
    api "io.trtc.uikit:rtc_room_engine:3.4.0.1306"
    api "io.trtc.uikit:atomicx-core:3.4.0.1307"
    api "com.tencent.liteav:LiteAVSDK_Professional:12.8.0.19279"
    api "com.tencent.imsdk:imsdk-plus:8.7.7201"
    // 其他依赖...
}
```

### 步骤3：实现登录逻辑

在您的项目中调用 `LoginStore.shared.login`完成登录，**这是使用 **`AtomicXCore`** 所有功能的关键前提**。

> **重要：**
> 

> 推荐在您 App 自身的用户账户登录成功后，再调用 LoginStore.shared.login，以确保登录业务逻辑的清晰和一致。
> 

``` java
import android.os.Bundle
import androidx.appcompat.app.AppCompatActivity
import io.trtc.tuikit.atomicxcore.api.login.LoginStore
import io.trtc.tuikit.atomicxcore.api.CompletionHandler
import android.util.Log

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        LoginStore.shared.login(
            this,              // context
            1400000001,        // 替换为您的 SDKAppID
            "test_001",        // 替换为您的 UserID
            "xxxxxxxxxxx",     // 替换为您的 UserSig
            object : CompletionHandler {
                override fun onSuccess() {
                    // 登录成功处理
                    Log.d("Login", "login success");
                }

                override fun onFailure(code: Int, desc: String) {
                    // 登录失败处理
                    Log.e("Login", "login failed, code: $code, error: $desc");
                }
            }
        )
    }
}
```

**登录接口参数说明：**
| 参数 | 类型 | 说明 |
| --- | --- | --- |
| sdkAppId | Int | 从 [控制台](https://console.cloud.tencent.com/trtc) 获取，通常是以 `140` 或 `160` 开头的 10 位整数。 |
| userID | String | 当前用户的唯一 ID，仅包含英文字母、数字、连字符和下划线。为避免多端登录冲突，**请勿使用**`1`、`123`**等简单 ID**。 |
| userSig | String | 用于腾讯云鉴权的票据。请注意： - 开发环境：您可以采用本地 `GenerateTestUserSig.genTestSig` 函数生成 userSig 或者 通过 [UserSig 辅助工具](https://console.cloud.tencent.com/im/tool-usersig) 生成临时的 UserSig。 - 生产环境：为了防止密钥泄露，请务必采用服务端生成 UserSig 的方式。详细信息请参考 [服务端生成 UserSig](https://cloud.tencent.com/document/product/647/17275)。 更多信息请参见 [如何计算及使用 UserSig](https://cloud.tencent.com/document/product/647/17275)。 |

## 搭建基础直播间

### 步骤1：实现主播视频开播

主播开播流程如下，您只需执行以下几步操作，即可快速搭建主播视频直播。

> **提示：**
> 

> 主播开播推流的业务代码，您也可以参考 TUILiveKit 开源项目中的 [VideoLiveAnchorActivity.kt](https://github.com/Tencent-RTC/TUIKit_Android/blob/main/live/tuilivekit/src/main/java/com/trtc/uikit/livekit/livestream/VideoLiveAnchorActivity.kt) 文件来了解完整的实现逻辑。
> 

1. **初始化主播推流的视图**

   在您的主播 Activity 中，创建一个 `LiveCoreView` 实例，并将 `viewType` 指定为 `PUSH_VIEW`（推流视图）。

   ``` java
   import io.trtc.tuikit.atomicxcore.api.view.CoreViewType
   import io.trtc.tuikit.atomicxcore.api.view.LiveCoreView
   import android.os.Bundle
   import androidx.appcompat.app.AppCompatActivity
   import androidx.constraintlayout.widget.ConstraintLayout
   
   // YourAnchorActivity 代表您的主播开播Activity
   class YourAnchorActivity : AppCompatActivity() {
   
       // 1. 将 LiveCoreView 作为您Activity的一个属性
       private lateinit var coreView: LiveCoreView
   
       override fun onCreate(savedInstanceState: Bundle?) {
           super.onCreate(savedInstanceState)
   
           // 2. 初始化视图
           coreView = LiveCoreView(this, viewType = CoreViewType.PUSH_VIEW)
           coreView.setLiveID("test_live_001")
   
           // 布局 UI
           setupUI()
       }
   
       private fun setupUI() {
           setContentView(R.layout.activity_anchor)
   
           // 3. 将主播推流页面加载到您的视图上
           val container = findViewById<ConstraintLayout>(R.id.container)
           container.addView(coreView)
   
           // 设置布局参数
           val params = ConstraintLayout.LayoutParams(
               ConstraintLayout.LayoutParams.MATCH_PARENT,
               ConstraintLayout.LayoutParams.MATCH_PARENT
           )
           params.topMargin = 36
           params.bottomMargin = 96
           coreView.layoutParams = params
       }
   }
   
   ```
2. **打开摄像头和麦克风**

   通过调用 **DeviceStore** 的 `openLocalCamera、openLocalMicrophone` 接口打开摄像头和麦克风，**您无需做额外操作，LiveCoreView 会自动预览当前摄像头的视频流**，示例代码如下：

   ``` java
   import androidx.appcompat.app.AppCompatActivity
   import android.os.Bundle
   import io.trtc.tuikit.atomicxcore.api.device.DeviceStore
   
   class YourAnchorActivity : AppCompatActivity() {
       // ... 其他代码 ...
   
       override fun onCreate(savedInstanceState: Bundle?) {
           super.onCreate(savedInstanceState)
           // 布局 UI
           setupUI()
           // 打开设备
           openDevices()
       }
   
       private fun openDevices() {
           // 1. 打开前置摄像头
           DeviceStore.shared().openLocalCamera(true, completion = null)
           // 2. 打开麦克风
           DeviceStore.shared().openLocalMicrophone(completion = null)
       }
   }
   ```
3. **开始直播**

   通过调用 **LiveListStore** 的 `createLive` 接口开始视频直播，完整示例代码如下：

   ``` java
   import android.util.Log
   import androidx.appcompat.app.AppCompatActivity
   import io.trtc.tuikit.atomicxcore.api.live.LiveInfo
   import io.trtc.tuikit.atomicxcore.api.live.LiveInfoCompletionHandler
   import io.trtc.tuikit.atomicxcore.api.live.LiveListStore
   
   class YourAnchorActivity : AppCompatActivity() {
   
       // ... 其他代码 ...
   
       // 调用开播接口开始直播
       private fun startLive() {
           val liveInfo = LiveInfo().apply {
               // 1. 设置直播的房间 id
               liveID = "test_live_001"
               // 2. 设置直播的房间名称
               liveName = "test 直播"
               // 3. 配置布局模板，默认：600 动态宫格布局
               seatLayoutTemplateID = 600 
               // 4. 配置主播始终在麦位上
               keepOwnerOnSeat = true
           }
           // 5. 调用 LiveListStore.shared().createLive 开始直播
           LiveListStore.shared().createLive(liveInfo, object: LiveInfoCompletionHandler {
               override fun onFailure(code: Int, desc: String) {
                   Log.e("Live", "Response startLive onError: $desc")
               }
   
               override fun onSuccess(liveInfo: LiveInfo) {
                   Log.d("Live", "Response startLive onSuccess")
               }
           })
       }
   }
   ```

   `LiveInfo`** 参数说明**

| **参数名** | **类型** | **属性** | **描述** |
| --- | --- | --- | --- |
| `liveID` | `String` | 必填 | 直播间的唯一标识符。 |
| `liveName` | `String` | 选填 | 直播间的标题。 |
| `notice` | `String` | 选填 | 直播间的公告信息。 |
| `isMessageDisable` | `Boolean` | 选填 | 是否禁言（`true`：是，`false`：否）。 |
| `isPublicVisible` | `Boolean` | 选填 | 是否公开可见（`true`：是，`false`：否）。 |
| `isSeatEnabled` | `Boolean` | 选填 | 是否启用麦位功能（`true`：是，`false`：否）。 |
| `keepOwnerOnSeat` | `Boolean` | 选填 | 是否保持房主在麦位上。 |
| `maxSeatCount` | `Int` | 必填 | 最大麦位数量。 |
| `seatMode` | [TakeSeatMode](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-take-seat-mode/index.html) | 选填 | 上麦模式（`FREE`：自由上麦，`APPLY`：申请上麦）。 |
| `seatLayoutTemplateID` | `Int` | 必填 | 麦位布局模板 `ID`。 |
| `coverURL` | `String` | 选填 | 直播间的封面图片地址。 |
| `backgroundURL` | `String` | 选填 | 直播间的背景图片地址。 |
| `categoryList` | `List<Int>` | 选填 | 直播间的分类标签列表。 |
| `activityStatus` | `Int` | 选填 | 直播活动状态。 |
| `isGiftEnabled` | `Boolean` | 选填 | 是否启用礼物功能（`true`：是，`false`：否）。 |

4. **结束直播**

   直播结束后，主播可以调用 **LiveListStore** 的 `endLive` 接口结束直播。SDK 会处理停止推流和销毁房间的逻辑。

   ``` java
   import android.util.Log
   import androidx.appcompat.app.AppCompatActivity
   import com.tencent.cloud.tuikit.engine.extension.TUILiveListManager
   import io.trtc.tuikit.atomicxcore.api.device.DeviceStore
   import io.trtc.tuikit.atomicxcore.api.live.LiveListStore
   import io.trtc.tuikit.atomicxcore.api.live.StopLiveCompletionHandler
   
   class YourAnchorActivity : AppCompatActivity() {
   
       // ... 其他代码 ...
   
       // 结束直播
       private fun stopLive() {
           LiveListStore.shared().endLive(object : StopLiveCompletionHandler {
               override fun onSuccess(statisticsData: TUILiveListManager.LiveStatisticsData) {
                   Log.d("Live", "endLive success, duration: ${statisticsData.liveDuration}, totalViewers: ${statisticsData.totalViewers}")
               }
   
               override fun onFailure(code: Int, desc: String) {
                   Log.e("Live", "endLive error: $desc")
               }
           })
       }
   
       // 确保在 Activity 销毁时也调用结束直播
       override fun onDestroy() {
           super.onDestroy()
           stopLive()
           // 关闭本地设备
           DeviceStore.shared().closeLocalCamera()
           DeviceStore.shared().closeLocalMicrophone()
           Log.d("Live", "YourAnchorActivity onDestroy")
       }
   }
   ```

### 步骤2：实现观众进房观看

观众观看流程如下，通过简单几步操作，即可实现观众观看直播。

> **提示：**
> 

> 观众进房拉流的业务代码，您也可以参考 TUILiveKit 开源项目中的 [VideoLiveAudienceActivity.kt](https://github.com/Tencent-RTC/TUIKit_Android/blob/main/live/tuilivekit/src/main/java/com/trtc/uikit/livekit/livestream/VideoLiveAudienceActivity.kt) 文件来了解完整的实现逻辑。
> 

1. **添加观众拉流页面**

   在您的观众 Activity 中，创建 `LiveCoreView` 实例，并将 `viewType` 指定为`PLAY_VIEW`（拉流视图）。

   ``` java
   import io.trtc.tuikit.atomicxcore.api.view.CoreViewType
   import io.trtc.tuikit.atomicxcore.api.view.LiveCoreView
   import android.os.Bundle
   import androidx.appcompat.app.AppCompatActivity
   import androidx.constraintlayout.widget.ConstraintLayout
   
   // YourAudienceActivity 代表您的观众观看Activity
   class YourAudienceActivity : AppCompatActivity() {
   
       // 1. 初始化观众拉流页面
       private lateinit var coreView: LiveCoreView
   
       override fun onCreate(savedInstanceState: Bundle?) {
           super.onCreate(savedInstanceState)
   
           // 2. 初始化视图
           coreView = LiveCoreView(this, viewType = CoreViewType.PLAY_VIEW)
           coreView.setLiveId("test_live_001")
   
           // UI 布局
           setupUI()
       }
   
       private fun setupUI() {
           setContentView(R.layout.activity_audience)
   
           // 3. 将观众拉流页面加载到您的视图上
           val container = findViewById<ConstraintLayout>(R.id.container)
           container.addView(coreView)
   
           // 设置布局参数
           val params = ConstraintLayout.LayoutParams(
               ConstraintLayout.LayoutParams.MATCH_PARENT,
               ConstraintLayout.LayoutParams.MATCH_PARENT
           )
           params.topMargin = 36
           params.bottomMargin = 96
           coreView.layoutParams = params
       }
   }
   ```
2. **进入直播间观看**

   通过调用 **LiveListStore** 的 `joinLive` 接口加入直播，**您无需做额外操作，LiveCoreView 会自动播放当前房间的视频流**，完整示例代码如下：

   ``` java
   import io.trtc.tuikit.atomicxcore.api.live.LiveInfo
   import io.trtc.tuikit.atomicxcore.api.live.LiveInfoCompletionHandler
   import io.trtc.tuikit.atomicxcore.api.live.LiveListStore
   import android.os.Bundle
   import androidx.appcompat.app.AppCompatActivity
   import android.util.Log
   
   // YourAudienceActivity 代表您的观众观看Activity
   class YourAudienceActivity : AppCompatActivity() {
   
       // ... 其他代码 ...
   
       override fun onCreate(savedInstanceState: Bundle?) {
           super.onCreate(savedInstanceState)
           setupUI()
           // 1. 调用 LiveListStore.shared().joinLive 进入直播间
           //       - liveID: 与主播开播同样的 liveID
           LiveListStore.shared().joinLive(liveID, object : LiveInfoCompletionHandler {
               override fun onFailure(code: Int, desc: String) {
                   Log.e("Live", "joinLive error: $desc")
               }
   
               override fun onSuccess(liveInfo: LiveInfo) {
                   Log.d("Live", "joinLive success")
               }
           })
       }
   }
   ```
3. **退出直播**

   观众退出直播间时，需要调用 **LiveListStore** 的 `leaveLive` 接口退出直播。SDK 会自动停止拉流并退出房间。

   ``` java
   import io.trtc.tuikit.atomicxcore.api.live.LiveListStore
   import io.trtc.tuikit.atomicxcore.api.CompletionHandler
   import androidx.appcompat.app.AppCompatActivity
   import android.util.Log
   
   // YourAudienceActivity 代表您的观众观看Activity
   class YourAudienceActivity : AppCompatActivity() {
   
       // ... 其他代码 ...
   
       // 退出直播
       private fun leaveLive() {
           LiveListStore.shared().leaveLive(object : CompletionHandler {
               override fun onSuccess() {
                   Log.d("Live", "leaveLive success")
               }
   
               override fun onFailure(code: Int, desc: String) {
                   Log.e("Live", "leaveLive error: $desc")
               }
           })
       }
   
       // 确保在 Activity 销毁时也调用退出直播
       override fun onDestroy() {
           super.onDestroy()
           leaveLive()
           Log.d("Live", "YourAudienceActivity onDestroy")
       }
   }
   ```

### 步骤3：监听直播事件

在观众加入直播间后，您还需要处理一些房间内的“被动”事件。例如主播主动结束了直播，或者观众因为违规等原因被踢出房间。如果不监听这些事件，观众端 UI 可能会停留在黑屏页面，影响用户体验。

您可以通过实现 `LiveListListener` 监听器，并将其注册到 `LiveListStore` 来实现事件监听。
``` java
import io.trtc.tuikit.atomicxcore.api.live.LiveEndedReason
import io.trtc.tuikit.atomicxcore.api.live.LiveKickedOutReason
import io.trtc.tuikit.atomicxcore.api.live.LiveListListener
import io.trtc.tuikit.atomicxcore.api.live.LiveListStore
import android.os.Bundle
import androidx.appcompat.app.AppCompatActivity
import android.util.Log

// YourAudienceActivity 代表您的观众观看Activity
class YourAudienceActivity : AppCompatActivity() {
    
    // ... (coreView, liveId, setupUI, joinLive, leaveLive 等代码) ...

    // 2. 定义一个 LiveListListener 实例
    private val liveListListener = object : LiveListListener() {
        override fun onLiveEnded(liveID: String, reason: LiveEndedReason, message: String) {
            // 监听到直播结束
            Log.d("Live", "Live ended. liveID: $liveID, reason: $reason, message: $message")
            // 在此处处理退出直播间的逻辑，例如关闭当前 Activity
            // finish()
        }

        override fun onKickedOutOfLive(liveID: String, reason: LiveKickedOutReason, message: String) {
            // 监听到被踢出直播
            Log.d("Live", "Kicked out of live. liveID: $liveID, reason: $reason, message: $message")
            // 在此处处理退出直播间的逻辑
            // finish()
        }
    }

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setupUI() 
        
        // 3. 注册监听器
        LiveListStore.shared().addLiveListListener(liveListListener)

        // 4. 进入直播间
        joinLive()
    }
    
    // ... joinLive() 和 leaveLive() 方法 ...

    override fun onDestroy() {
        super.onDestroy()
        // 5. 确保在 Activity 销毁时移除监听器，防止内存泄漏
        LiveListStore.shared().removeLiveListListener(liveListListener)
        leaveLive()
        Log.d("Live", "YourAudienceActivity onDestroy")
    }
}
```

### 运行效果

集成 **LiveCoreView** 后，您将得到一个纯净的视频渲染视图，它已具备完整的直播业务能力，但没有任何交互 UI。您可以参考下一章节 丰富直播场景 来完善直播场景。
|  | **动态宫格布局** | **浮动小窗布局** | **固定宫格布局** | **固定小窗布局** |
| --- | --- | --- | --- | --- |
| **模板 ID** | 600 | 601 | 800 | 801 |
| **描述** | 默认布局，可根据连麦人数动态调整宫格大小。 | 连麦嘉宾以浮动小窗形式显示。 | 连麦人数固定，每个嘉宾占据一个固定宫格。 | 连麦人数固定，嘉宾以固定小窗形式显示。 |
| **运行效果** |  |  |  |  |

## 丰富直播场景

当您完成了基础的直播功能后，您可以参考以下功能指南来为直播添加丰富的互动玩法。
| **直播功能** | **功能介绍** | **功能 Stores** | **实现指南** |
| --- | --- | --- | --- |
| **实现观众音视频连线** | 观众申请上麦，与主播进行实时视频互动。 | [CoGuestStore](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-co-guest-store/index.html) | 观众连线 |
| **实现主播跨房连线 PK** | 两个不同房间的主播进行连线，实现互动或 PK。 | [CoHostStore](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-co-host-store/index.html) [BattleStore](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-battle-store/index.html) | 主播连线 & PK |
| **添加弹幕聊天功能** | 观众可以在直播间发送和接收实时文字消息。 | [BarrageStore](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.barrage/-barrage-store/index.html) | 实现弹幕功能 |
| **构建礼物赠送系统** | 观众可以向主播赠送虚拟礼物，增加互动和趣味性。 | [GiftStore](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.gift/-gift-store/index.html) | 实现礼物功能 |

## API 文档
| **Store/Component** | **功能描述** | **API 文档** |
| --- | --- | --- |
| **LiveCoreView** | 直播视频流展示与交互的核心视图组件：负责视频流渲染和视图挂件处理，支持主播直播、观众连麦、主播连线等场景。 | [API 文档](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.view/-live-core-view/index.html) |
| **LiveListStore** | 直播间全生命周期管理：创建 / 加入 / 离开 / 销毁房间，查询房间列表，修改直播信息（名称、公告等），监听直播状态（如被踢出、结束）。 | [API 文档](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-live-list-store/index.html) |
| **DeviceStore** | 音视频设备控制：麦克风（开关 / 音量）、摄像头（开关 / 切换 / 画质）、屏幕共享，设备状态实时监听。 | [API 文档](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.device/-device-store/index.html) |
| **CoGuestStore** | 观众连麦管理：连麦申请 / 邀请 / 同意 / 拒绝，连麦成员权限控制（麦克风 / 摄像头），状态同步。 | [API 文档](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-co-guest-store/index.html) |
| **CoHostStore** | 主播跨房连线：支持多布局模板（动态网格等），发起 / 接受 / 拒绝连线，连麦主播互动管理。 | [API 文档](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-co-host-store/index.html) |
| **BattleStore** | 主播 PK 对战：发起 PK（配置时长 / 对手），管理 PK 状态（开始 / 结束），同步分数，监听对战结果。 | [API 文档](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-battle-store/index.html) |
| **GiftStore** | 礼物互动：获取礼物列表，发送 / 接收礼物，监听礼物事件（含发送者、礼物详情）。 | [API 文档](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.gift/-gift-store/index.html) |
| **BarrageStore** | 弹幕功能：发送文本 / 自定义弹幕，维护弹幕列表，实时监听弹幕状态。 | [API 文档](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.barrage/-barrage-store/index.html) |
| **LikeStore** | 点赞互动：发送点赞，监听点赞事件，同步总点赞数。 | [API 文档](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-like-store/index.html) |
| **LiveAudienceStore** | 观众管理：获取实时观众列表（ID / 名称 / 头像），统计观众数量，监听观众进出事件。 | [API 文档](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-live-audience-store/index.html) |
| **AudioEffectStore** | 音频特效：变声（童声 / 男声）、混响（KTV 等）、耳返调节，实时切换特效。 | [API 文档](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.device/-audio-effect-store/index.html) |
| **BaseBeautyStore** | 基础美颜：调节磨皮 / 美白 / 红润（0-100 级），重置美颜状态，同步效果参数。 | [API 文档](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.device/-base-beauty-store/index.html) |

## 常见问题

### 主播调用 createLive 或 观众调用 joinLive 后为什么画面是黑的，没有视频画面？
- **检查 setLiveID**：请确保在调用开播或观看接口前，已经为 LiveCoreView 实例设置了正确的 liveID。

- **检查设备权限**：请确保 App 已获得摄像头和麦克风的系统使用权限。

- **检查主播端**：主播端是否正常调用 `DeviceStore.shared().openLocalCamera(true)` 打开了摄像头。

- **检查网络**：请检查设备网络连接是否正常。

### 主播端打开摄像头后，开播后可以看到本地视频预览画面，开播前视频预览是黑屏？
- **检查主播端**：请检查主播推流视图`LiveCoreView` 的 `viewType`是否配置为`PUSH_VIEW`。

- **检查观众端**：请检查观众拉流视图`LiveCoreView` 的 `viewType`是否配置为 `PLAY_VIEW`。

---

本文档将帮助您使用 **AtomicXCore SDK **的核心组件 [LiveCoreView](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/livecoreview)，快速构建一个包含主播开播和观众观看功能的基础直播 App。

## **核心功能**

**LiveCoreView** 是一个专为直播场景设计的轻量级 `UIView` 组件，是您构建直播场景的核心，它封装了所有复杂的底层直播技术（例如推拉流、连麦、音视频渲染）。您可以将 LiveCoreView 作为直播画面的“画布”，专注于上层 UI 与交互的开发。

通过下方的视图层级示意图，您可以直观了解 **LiveCoreView** 在直播界面中的位置和作用：

## 准备工作

### 步骤1：开通服务

请参见 开通服务，获取体验版或付费版 SDK。

### 步骤2：在当前项目中导入 AtomicXCore
1. **安装组件**：请在您的 **Podfile** 文件中添加 `pod 'AtomicXCore'` 依赖，然后执行`pod install`。

   ``` ruby
   target 'xxxx' do
     pod 'AtomicXCore'
   end
   ```
2. **配置工程权限:  **请在应用的 `Info.plist` 文件中添加相机和麦克风的使用权限说明。

   ``` ruby
   <key>NSCameraUsageDescription</key>
   <string>TUILiveKit需要访问你的相机权限，开启后录制的视频才会有画面</string>
   <key>NSMicrophoneUsageDescription</key>
   <string>TUILiveKit需要访问您的麦克风权限，开启后录制的视频才会有声音</string>
   ```
   

### 步骤3：实现登录逻辑

在您的项目中调用 `LoginStore.shared.login` 完成登录，**这是使用 **`AtomicXCore`** 所有功能的关键前提**。

> **重要：**
> 

> 推荐在您 App 自身的用户账户登录成功后，再调用 LoginStore.shared.login，以确保登录业务逻辑的清晰和一致。
> 

``` swift
import AtomicXCore

//  AppDelegate.swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    LoginStore.shared.login(sdkAppID: 1400000001,                  // 替换为您的 SDKAppID
                            userID: "test_001",                    // 替换为您的 UserID
                            userSig: "xxxxxxxxxxx") { result in    // 替换为您的 UserSig
      switch result {
        case .success(let info):
        debugPrint("login success")
        case .failure(let error):
        debugPrint("login failed code:\(error.code), message:\(error.message)")
      }
    }
    return true
}
```

**登录接口参数说明：**
| 参数 | 类型 | 说明 |
| --- | --- | --- |
| sdkAppId | Int32 | 从 [控制台](https://console.cloud.tencent.com/trtc) 获取，通常是以 `140` 或 `160` 开头的 10 位整数。 |
| userID | String | 当前用户的唯一 ID，仅包含英文字母、数字、连字符和下划线。为避免多端登录冲突，**请勿使用**`1`、`123`**等简单 ID**。 |
| userSig | String | 用于腾讯云鉴权的票据。请注意： - 开发环境：您可以采用本地 `GenerateTestUserSig.genTestSig` 函数生成 userSig 或者通过 [UserSig 辅助工具](https://console.cloud.tencent.com/im/tool-usersig) 生成临时的 UserSig。 - 生产环境：为了防止密钥泄露，请务必采用服务端生成 UserSig 的方式。详细信息请参考 [服务端生成 UserSig](https://cloud.tencent.com/document/product/647/17275)。 更多信息请参见 [如何计算及使用 UserSig](https://cloud.tencent.com/document/product/647/17275)。 |

## 搭建基础直播间

### 步骤1：实现主播视频开播

主播开播流程如下，您只需执行以下几步操作，即可快速搭建主播视频直播。

> **提示：**
> 

> 主播开播推流的业务代码，您也可以参考 TUILiveKit 开源项目中的 [TUILiveRoomAnchorViewController.swift](https://github.com/Tencent-RTC/TUIKit_iOS/blob/main/live/Sources/LiveStream/TUILiveRoomAnchorViewController.swift) 文件来了解完整的实现逻辑。
> 

1. **初始化主播推流的视图**

   在您的主播视图控制器中，创建一个 `LiveCoreView` 实例，并将 `viewType` 指定为 `.pushView`（推流视图）。

   ``` swift
   import AtomicXCore
   
   // YourAnchorViewController 代表您的主播开播视图控制器
   class YourAnchorViewController: UIViewController {
   
       private let liveId: String
       // 1. 将 LiveCoreView 作为您视图控制器的一个属性
       private let coreView = LiveCoreView(viewType:.pushView, frame: UIScreen.main.bounds)
      
       // 2. 新增便利构造函数完成实例初始化
       //    - liveId: 您需要开播的直播房间 id
       public init(liveId: String) {
           self.liveId = liveId
           super.init(nibName: nil, bundle: nil)
           self.coreView.setLiveID(liveId)
       }
       
       required init?(coder: NSCoder) {
           fatalError("init(coder:) has not been implemented")
       }
       
       public override func viewDidLoad() {
           super.viewDidLoad()
           // 3. 将主播推流页面加载到您的视图上
           view.addSubview(coreView)
       }
   }  
   ```
2. **打开摄像头和麦克风**

   通过调用 **DeviceStore** 的 `openLocalCamera、openLocalMicrophone` 接口打开摄像头和麦克风，**您无需做额外操作，LiveCoreView 会自动预览当前摄像头的视频流**，示例代码如下：

   ``` swift
   import AtomicXCore
   
   // YourAnchorViewController 代表您的主播开播视图控制器
   class YourAnchorViewController: UIViewController {
       // ... 其他代码 ...
       public override func viewDidLoad() {
           super.viewDidLoad()
           // 打开设备
           openDevices()
       }
       
       private func openDevices() {
           // 1. 打开前置摄像头 
           DeviceStore.shared.openLocalCamera(isFront: true, completion: nil)
           // 2. 打开麦克风
           DeviceStore.shared.openLocalMicrophone(completion: nil)
       }
   }
   ```
3. **开始直播**

   通过调用 **LiveListStore** 的 `createLive` 接口开始视频直播，完整示例代码如下：

   ``` swift
   import AtomicXCore
   
   // YourAnchorViewController 代表您的主播开播视图控制器
   class YourAnchorViewController: UIViewController {
   
       // ... 其他代码 ...
   
       // 调用开播接口开始直播
       private func startLive() {
           var liveInfo = LiveInfo()
           // 1. 设置直播的房间 id
           liveInfo.liveID = self.liveId
           // 2. 设置直播的房间名称
           liveInfo.liveName = "test 直播"
           // 3. 配置布局模板，默认：600 动态宫格布局
           liveInfo.seatLayoutTemplateID = 600
           // 4. 配置主播始终在麦位上
           liveInfo.keepOwnerOnSeat = true
           // 5. 调用 LiveListStore.shared.createLive 开始直播
           LiveListStore.shared.createLive(liveInfo) { [weak self] result in
               guard let self = self else { return }
               switch result {
               case .success(let info):
                   debugPrint("startLive success")
               case .failure(let error):
                   debugPrint("startLive error:\(error.message)")
               }
           }
       }
   }  
   ```

   `LiveInfo`**参数说明:**

| **参数名** | **类型** | **属性** | **描述** |
| --- | --- | --- | --- |
| `liveID` | `String` | 必填 | 直播间的唯一标识符。 |
| `liveName` | `String` | 选填 | 直播间的标题。 |
| `notice` | `String` | 选填 | 直播间的公告信息。 |
| `isMessageDisable` | `Bool` | 选填 | 是否禁言（`true`：是，`false`：否）。 |
| `isPublicVisible` | `Bool` | 选填 | 是否公开可见（`true`：是，`false`：否）。 |
| `isSeatEnabled` | `Bool` | 选填 | 是否启用麦位功能（`true`：是，`false`：否）。 |
| `keepOwnerOnSeat` | `Bool` | 选填 | 是否保持房主在麦位上。 |
| `maxSeatCount` | `Int` | 必填 | 最大麦位数量。 |
| `seatMode` | `TakeSeatMode` | 选填 | 上麦模式（`.free`：自由上麦，`.apply`：申请上麦）。 |
| `seatLayoutTemplateID` | `UInt` | 必填 | 麦位布局模板 `ID。` |
| `coverURL` | `String` | 选填 | 直播间的封面图片地址。 |
| `backgroundURL` | `String` | 选填 | 直播间的背景图片地址。 |
| `categoryList` | `[NSNumber]` | 选填 | 直播间的分类标签列表。 |
| `activityStatus` | `Int` | 选填 | 直播活动状态。 |
| `isGiftEnabled` | `Bool` | 选填 | 是否启用礼物功能（`true`：是，`false`：否）。 |

4. **结束直播**

   直播结束后，主播可以调用 **LiveListStore** 的 `endLive` 接口结束直播。SDK 会处理停止推流和销毁房间的逻辑。

   ``` swift
   import AtomicXCore
   
   // YourAnchorViewController 代表您的主播开播视图控制器
   class YourAnchorViewController: UIViewController {
   
       // ... 其他代码 ...
   
       // 结束直播
       private func stopLive() {
           LiveListStore.shared.endLive { [weak self] result in
               guard let self = self else { return }
               switch result {
               case .success(let data):
                   debugPrint("endLive success")
               case .failure(let error):
                   debugPrint("endLive error: \(error.message)")
               }
           }
       }
   }
   ```

### 步骤2：实现观众进房观看

观众观看流程如下，通过简单几步操作，即可实现观众观看直播。

> **提示：**
> 

> 观众进房拉流的业务代码，您也可以参考 TUILiveKit 开源项目中的 [TUILiveRoomAudienceViewController.swift](https://github.com/Tencent-RTC/TUIKit_iOS/blob/main/live/Sources/LiveStream/TUILiveRoomAudienceViewController.swift) 文件来了解完整的实现逻辑。
> 

1. **实现观众拉流页面**

   在您的观众视图控制器中，创建 `LiveCoreView` 实例，并将 `viewType` 指定为 `.playView`（拉流视图）。

   ``` swift
   import AtomicXCore
   
   // YourAudienceViewController 代表您的观众观看视图控制器
   class YourAudienceViewController: UIViewController {
      
       // 1. 初始化观众拉流页面
       private let coreView = LiveCoreView(viewType:.playView, frame: UIScreen.main.bounds)
       private let liveId: String
       
       public init(liveId: String) {
           self.liveId = liveId
           super.init(nibName: nil, bundle: nil)
           // 2. 绑定直播 id
           self.coreView.setLiveID(liveId)
       }
       
       required init?(coder: NSCoder) {
           fatalError("init(coder:) has not been implemented")
       }
       
       public override func viewDidLoad() {
           super.viewDidLoad()
           // 3. 将主播推流页面加载到您的视图上
           view.addSubview(coreView)
       }
   }  
   ```
2. **进入直播间观看**

   通过调用 **LiveListStore** 的 `joinLive` 接口加入直播，**您无需做额外操作，LiveCoreView 会自动播放当前房间的视频流**，完整示例代码如下：

   ``` swift
   import AtomicXCore
   
   // YourAudienceViewController 代表您的观众观看视图控制器
   class YourAudienceViewController: UIViewController {
       // ... 其他代码 ...
   
       public override func viewDidLoad() {
           super.viewDidLoad()
           // 3. 将主播推流页面加载到您的视图上
           view.addSubview(coreView)
   
           // 4. 进入直播间
           joinLive()
       }
   
       private func joinLive() {
            // 调用 LiveListStore.shared.joinLive 进入直播间
           // - liveId: 与主播开播同样的 liveId
           LiveListStore.shared.joinLive(liveID: liveId) { [weak self] result in
               guard let self = self else { return }
               switch result {
               case .success(let info):
                   debugPrint("joinLive success")
               case .failure(let error):
                   debugPrint("joinLive error \(error.message)")
                   // 进房失败，也需要退出页面
                   // self.dismiss(animated: true)
               }
           }
       }
   }
   ```
3. **退出直播**

   观众退出直播间时，需要调用 **LiveListStore** 的 `leaveLive` 接口退出直播。SDK 会自动停止拉流并退出房间。

   ``` swift
   import AtomicXCore
   
   // YourAudienceViewController 代表您的观众观看视图控制器
   class YourAudienceViewController: UIViewController {
   
       // ... 其他代码 ...
   
       // 退出直播
       private func leaveLive() {
           LiveListStore.shared.leaveLive { [weak self] result in
               guard let self = self else { return }
               switch result {
               case .success:
                   debugPrint("leaveLive success")
               case .failure(let error):
                   debugPrint("leaveLive error \(error.message)")
               }
           }
       }
   }
   ```

### 步骤3：监听直播事件

在观众加入直播间后，您还需要处理一些房间内的“被动”事件。例如，主播主动结束了直播，或者观众因为违规等原因被踢出房间。如果不监听这些事件，观众端 UI 可能会停留在黑屏页面，影响用户体验。

您可以通过订阅 `LiveListStore` 提供的 `liveListEventPublisher` 来实现事件监听。
``` swift
import AtomicXCore
import Combine // 1. 导入 Combine 框架

// YourAudienceViewController 代表您的观众观看视图控制器
class YourAudienceViewController: UIViewController {
   
    // ... 其他代码 (coreView, liveId, init, deinit, joinLive, leaveLive等) ...

    // 2. 定义 cancellableSet 来管理订阅生命周期
    private var cancellableSet: Set<AnyCancellable> = []
    
    public override func viewDidLoad() {
        super.viewDidLoad()
        view.addSubview(coreView)
        // 3. 监听直播事件
        setupLiveEventListener()
        // 4. 进入直播间
        joinLive()
    }

    // 5. 新增一个方法来设置事件监听
    private func setupLiveEventListener() {
        LiveListStore.shared.liveListEventPublisher
            .receive(on: RunLoop.main) // 确保在主线程处理 UI 更新
            .sink { [weak self] event in
                guard let self = self else { return }
                switch event {
                case .onLiveEnded(let liveID, let reason, let message):
                    // 监听到直播结束
                    debugPrint("Live ended. liveID: \(liveID), reason: \(reason.rawValue), message: \(message)")
                    // 在此处处理退出直播间的逻辑，例如关闭当前页面
                    // self.dismiss(animated: true)
                case .onKickedOutOfLive(let liveID, let reason, let message):
                    // 监听到被踢出直播
                    debugPrint("Kicked out of live. liveID: \(liveID), reason: \(reason.rawValue), message: \(message)")
                    // 在此处处理退出直播间的逻辑
                    // self.dismiss(animated: true)
                }
            }
            .store(in: &cancellableSet) // 管理订阅
    }
    
    // ... joinLive() 和 leaveLive() 方法 ...
}
```

### 运行效果

集成 **LiveCoreView** 后，您将得到一个纯净的视频渲染视图，它已具备完整的直播业务能力，但没有任何交互 UI。您可以参考下一章节 丰富直播场景 来完善直播场景。
|  | **动态宫格布局** | **浮动小窗布局** | **固定宫格布局** | **固定小窗布局** |
| --- | --- | --- | --- | --- |
| **模板 ID** | 600 | 601 | 800 | 801 |
| **描述** | 默认布局，可根据连麦人数动态调整宫格大小。 | 连麦嘉宾以浮动小窗形式显示。 | 连麦人数固定，每个嘉宾占据一个固定宫格。 | 连麦人数固定，嘉宾以固定小窗形式显示。 |
| **运行效果** |  |  |  |  |

## 丰富直播场景

当您完成了基础的直播功能后，您可以参考以下功能指南来为直播添加丰富的互动玩法。
| **直播功能** | **功能介绍** | **功能 Stores** | **实现指南** |
| --- | --- | --- | --- |
| **实现观众音视频连线** | 观众申请上麦，与主播进行实时视频互动。 | [CoGuestStore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/cogueststore) | 实现观众连线 |
| **实现主播跨房连线 PK** | 两个不同房间的主播进行连线，实现互动或 PK。 | [CoHostStore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/cohoststore) [BattleStore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/battlestore) | 实现主播连线 PK |
| **添加弹幕聊天功能** | 观众可以在直播间发送和接收实时文字消息。 | [BarrageStore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/barragestore) | 实现弹幕功能 |
| **构建礼物赠送系统** | 观众可以向主播赠送虚拟礼物，增加互动和趣味性。 | [GiftStore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/giftstore) | 实现礼物功能 |

## API 文档
| **Store/Component** | **功能描述** | **API 文档** |
| --- | --- | --- |
| **LiveCoreView** | 直播视频流展示与交互的核心视图组件：负责视频流渲染和视图挂件处理，支持主播直播、观众连麦、主播连线等场景。 | [API 文档](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/livecoreview) |
| **LiveListStore** | 直播间全生命周期管理：创建 / 加入 / 离开 / 销毁房间，查询房间列表，修改直播信息（名称、公告等），监听直播状态（如被踢出、结束）。 | [API 文档](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/liveliststore) |
| **DeviceStore** | 音视频设备控制：麦克风（开关 / 音量）、摄像头（开关 / 切换 / 画质）、屏幕共享，设备状态实时监听。 | [API 文档](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/devicestore) |
| **CoGuestStore** | 观众连麦管理：连麦申请 / 邀请 / 同意 / 拒绝，连麦成员权限控制（麦克风 / 摄像头），状态同步。 | [API 文档](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/cogueststore) |
| **CoHostStore** | 主播跨房连线：支持多布局模板（动态网格等），发起 / 接受 / 拒绝连线，连麦主播互动管理。 | [API 文档](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/cohoststore) |
| **BattleStore** | 主播 PK 对战：发起 PK（配置时长 / 对手），管理 PK 状态（开始 / 结束），同步分数，监听对战结果。 | [API 文档](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/battlestore) |
| **GiftStore** | 礼物互动：获取礼物列表，发送 / 接收礼物，监听礼物事件（含发送者、礼物详情）。 | [API 文档](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/giftstore) |
| **BarrageStore** | 弹幕功能：发送文本 / 自定义弹幕，维护弹幕列表，实时监听弹幕状态。 | [API 文档](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/barragestore) |
| **LikeStore** | 点赞互动：发送点赞，监听点赞事件，同步总点赞数。 | [API 文档](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/likestore) |
| **LiveAudienceStore** | 观众管理：获取实时观众列表（ID / 名称 / 头像），统计观众数量，监听观众进出事件。 | [API 文档](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/liveaudiencestore) |
| **AudioEffectStore** | 音频特效：变声（童声 / 男声）、混响（KTV 等）、耳返调节，实时切换特效。 | [API 文档](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/audioeffectstore) |
| **BaseBeautyStore** | 基础美颜：调节磨皮 / 美白 / 红润（0-100 级），重置美颜状态，同步效果参数。 | [API 文档](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/basebeautystore) |

## 常见问题

### 主播调用 createLive 或 观众调用 joinLive 后为什么画面是黑的，没有视频画面？
- **检查 setLiveID**：请确保在调用开播或观看接口前，已经为 LiveCoreView 实例设置了正确的 liveID。

- **检查设备权限**：请确保 App 已获得摄像头和麦克风的系统使用权限。

- **检查主播端**：主播端是否正常调用 `DeviceStore.shared.openLocalCamera(isFront: true)` 打开了摄像头。

- **检查网络**：请检查设备网络连接是否正常。

### 主播端打开摄像头后，开播后可以看到本地视频预览画面，开播前视频预览是黑屏？
- **检查主播端**：请检查主播推流视图`LiveCoreView` 的 `viewType`是否配置为`.pushView`。

- **检查观众端**：请检查观众拉流视图`LiveCoreView` 的 `viewType`是否配置为 `.playView`。

### rsync 因权限不足导致依赖三方库资源拷贝失败

例如在使用 Xcode 集成 SnapKit 框架进行开发时，可能会遇到如下编译报错：
``` plaintext
rsync(xxxx):1:1: SnapKit.framework/SnapKit_Privacy.bundle/: mkpathat: Operation not permitted
```

#### 问题原因

Xcode 的用户**脚本沙盒机制**限制了构建过程中 `rsync` 脚本对 `SnapKit.framework` 资源文件的写入权限，导致框架内的 `SnapKit_Privacy.bundle` 无法正常拷贝。

#### 解决步骤
1. 关闭用户脚本沙盒后，打开 Xcode 项目，进入项目的 **Build Settings**，搜索 `User Script Sandboxing`（或标识 `ENABLE_USER_SCRIPT_SANDBOXING`），将其值从 `YES` 修改为 `NO`。

2. 清理并重新构建项目执行 **Product → Clean Build Folder** 清理项目缓存，然后重新编译运行即可。

---

本文档将帮助您使用 **AtomicXCore SDK** 的核心组件 [LiveCoreWidget](https://tencent-rtc.github.io/TUIKit_Flutter/api_view_live_live_core_widget/api_view_live_live_core_widget-library.html)，快速构建一个包含主播开播和观众观看功能的基础直播 App。

## 核心功能

**LiveCoreWidget** 是一个专为直播场景设计的轻量级 Widget 组件，是您构建直播场景的核心，它封装了所有复杂的底层直播技术（例如推拉流、连麦、音视频渲染）。您可以将 LiveCoreWidget 作为直播画面的"画布"，专注于上层 UI 与交互的开发。

通过下方的视图层级示意图，您可以直观了解 **LiveCoreWidget** 在直播界面中的位置和作用：

## 准备工作

### 步骤1：开通服务

请参见 开通服务，获取体验版或付费版 SDK。

### 步骤2：在当前项目中导入 AtomicXCore
1. **安装组件**：请在您的 `pubspec.yaml` 文件中添加 `atomic_x_core` 依赖，然后执行 `flutter pub get`。

   ``` yaml
   dependencies:
     atomic_x_core: ^3.6.0
   ```
2. **配置工程权限：**Android 和 iOS 工程都需要配置权限。

   

【Android】

请在 `android/app/src/main/AndroidManifest.xml` 文件中添加相机和麦克风的使用权限说明。
``` xml
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
```

【iOS】

请在应用 `iOS` 目录的 **Podfile** 和 `ios/Runner` 目录的 `Info.plist` 文件中添加相机和麦克风的使用权限说明。

**Podfile**
``` ruby
post_install do |installer|
  installer.pods_project.targets.each do |target|
    flutter_additional_ios_build_settings(target)
      target.build_configurations.each do |config|
          config.build_settings['GCC_PREPROCESSOR_DEFINITIONS'] ||= [
        '$(inherited)',
        'PERMISSION_MICROPHONE=1',
        'PERMISSION_CAMERA=1',
        ]
      end
  end
end
```

**Info.plist**
``` xml
<key>NSCameraUsageDescription</key>
<string>TUILiveKit需要访问你的相机权限，开启后录制的视频才会有画面</string>
<key>NSMicrophoneUsageDescription</key>
<string>TUILiveKit需要访问您的麦克风权限，开启后录制的视频才会有声音</string>
```

### 步骤3：实现登录逻辑

在您的项目中调用 `LoginStore.shared.login` 完成登录，**这是使用 AtomicXCore 所有功能的关键前提**。

> **重要：**
> 

> 推荐在您 App 自身的用户账户登录成功后，再调用 LoginStore.shared.login，以确保登录业务逻辑的清晰和一致。
> 

``` java
import 'package:flutter/material.dart';
import 'package:atomic_x_core/atomicxcore.dart';

void main() async {
  WidgetsFlutterBinding.ensureInitialized();

  final result = await LoginStore.shared.login(
    sdkAppID: 1400000001,           // 替换为您的 sdkAppID
    userID: "test_001",             // 替换为您的 userID
    userSig: "xxxxxxxxxxx",         // 替换为您的 userSig
  );

  if (result.isSuccess) {
    debugPrint("login success");
  } else {
    debugPrint("login failed code: ${result.errorCode}, message: ${result.errorMessage}");
  }

  runApp(const MyApp());
}
```

**登录接口参数说明：**
| **参数** | **类型** | **说明** |
| --- | --- | --- |
| `sdkAppID` | `int` | 从 [控制台](https://console.cloud.tencent.com/trtc) 获取，通常是以 `140` 或 `160` 开头的 10 位整数。 |
| `userID` | `String` | 当前用户的唯一 ID，仅包含英文字母、数字、连字符和下划线。为避免多端登录冲突，**请勿使用**`1`、`123`**等简单 ID**。 |
| `userSig` | `String` | 用于腾讯云鉴权的票据。请注意： - 开发环境：您可以采用本地 `GenerateTestUserSig.genTestSig` 函数生成 userSig 或者通过 [UserSig 辅助工具](https://console.cloud.tencent.com/im/tool-usersig) 生成临时的 UserSig。 - 生产环境：为了防止密钥泄露，请务必采用服务端生成 UserSig 的方式。详细信息请参考 [服务端生成 UserSig](https://cloud.tencent.com/document/product/647/17275)。 更多信息请参见 [如何计算及使用 UserSig](https://cloud.tencent.com/document/product/647/17275)。 |

## 搭建基础直播间

### 步骤1：实现主播开播

主播开播涉及“预览”和“直播”两个阶段。由于底层视频渲染机制不同，我们需要构建一个状态机来管理视图切换，从而避免预览时出现黑屏。
1. **核心逻辑与状态定义**

   首先，在您的 State 类中定义核心控制器，并增加一个 _isLiveStarted 标记，用于区分当前是“预览态”还是“直播态”。

   ``` java
   class _YourAnchorPageState extends State<YourAnchorPage> {
     // 核心控制器
     late final LiveCoreController _controller;
     // 状态标记：false = 预览中; true = 直播中
     bool _isLiveStarted = false; 
   
     @override
     void initState() {
       super.initState();
       _controller = LiveCoreController.create(CoreViewType.pushView);
       _controller.setLiveID(widget.liveId);
       
       // 初始化时直接打开设备（详见下一步）
       _openDevices();
     }
   }
   ```
2. **打开摄像头和麦克风**

   通过调用 **DeviceStore** 的 `openLocalCamera`、`openLocalMicrophone` 接口打开摄像头和麦克风，**您无需做额外操作，LiveCoreWidget 会自动预览当前摄像头的视频流**，示例代码如下：
   

   > **注意：**
   > 

   > 此步骤对于预览至关重要。只有打开设备，后续的 VideoView 才有画面可渲染。
   > 

   ``` java
   void _openDevices() {
       // 1. 打开前置摄像头 (true 表示前置)
       DeviceStore.shared.openLocalCamera(true);
       // 2. 打开麦克风
       DeviceStore.shared.openLocalMicrophone();
     }
   ```
3. **构建预览视图**

   这是最关键的一步。我们需要根据 `_isLiveStarted` 的状态选择不同的组件：

- **预览态：**使用 `VideoView` + `setLocalVideoView`（直接渲染本地采集数据）。

- **直播态：**使用 `LiveCoreWidget`（渲染直播间流数据）。

   ``` java
   // 3.1 封装预览视图组件
     Widget _buildLocalPreview() {
       return Container(
         color: Colors.black,
         child: VideoView(
           onViewCreated: (viewId) {
             // 关键：将本地摄像头画面绑定到预览 View
             TUIRoomEngine.sharedInstance().setLocalVideoView(viewId);
           },
           onViewDisposed: (viewId) {
             // 销毁时解绑
             TUIRoomEngine.sharedInstance().setLocalVideoView(0);
           },
         ),
       );
     }
   
     // 3.2 组合主视图
     @override
     Widget build(BuildContext context) {
       return Scaffold(
         body: Stack(
           children: [
             // 视图层：根据状态自动切换
             Positioned.fill(
               child: _isLiveStarted 
                   ? LiveCoreWidget(controller: _controller) // 直播中：用核心组件
                   : _buildLocalPreview(),                   // 预览中：用 VideoView
             ),
             
             // UI 层：开播按钮（仅在预览时显示）
             if (!_isLiveStarted)
               Positioned(
                 bottom: 50, left: 0, right: 0,
                 child: Center(
                   child: ElevatedButton(
                     onPressed: _startLive, // 下一步实现此方法
                     child: const Text('开始直播'),
                   ),
                 ),
               ),
           ],
         ),
       );
     }
   ```
4. **实现开播与关播逻辑**

   通过调用 **LiveListStore** 的 `createLive` 接口开始视频直播，示例代码如下：

   ``` java
   Future<void> _startLive() async {
       // 1. 配置直播间参数
       final liveInfo = LiveInfo(
         liveID: widget.liveId,         // 房间唯一标识
         liveName: "Atomic Live Demo",  // 房间标题
         seatLayoutTemplateID: 600,     // 布局模式：600 代表默认动态宫格
         keepOwnerOnSeat: true,         // 房主是否始终占有一个麦位
       );
   
       // 2. 发起开播请求
       final result = await LiveListStore.shared.createLive(liveInfo);
   
       if (result.isSuccess) {
         debugPrint("开播成功");
         // 3. 关键步骤：更新状态
         // 将 _isLiveStarted 置为 true，触发 build 方法重新构建，
         // 从而将 UI 从 VideoView（预览）切换为 LiveCoreWidget（直播）。
         setState(() {
           _isLiveStarted = true;
         });
       } else {
         debugPrint("开播失败: ${result.errorMessage}");
         // 可以在此处添加 Toast 提示用户
       }
     }
   ```

   **LiveInfo 参数说明：**

| **参数名** | **类型** | **属性** | **描述** |
| --- | --- | --- | --- |
| `liveID` | `String` | 必填 | 直播间的唯一标识符。 |
| `liveName` | `String` | 选填 | 直播间的标题。 |
| `notice` | `String` | 选填 | 直播间的公告信息。 |
| `isMessageDisable` | `bool` | 选填 | 是否禁言（`true`：是，`false`：否）。 |
| `isPublicVisible` | `bool` | 选填 | 是否公开可见（`true`：是，`false`：否）。 |
| `isSeatEnabled` | `bool` | 选填 | 是否启用麦位功能（`true`：是，`false`：否）。 |
| `keepOwnerOnSeat` | `bool` | 选填 | 是否保持房主在麦位上。 |
| `maxSeatCount` | `int` | 选填 | 最大麦位数量。 |
| `seatMode` | `TakeSeatMode` | 选填 | 上麦模式（`TakeSeatMode.free`：自由上麦，`TakeSeatMode.apply`：申请上麦）。 |
| `seatLayoutTemplateID` | `int` | 必填 | 麦位布局模板 ID。 |
| `coverURL` | `String` | 选填 | 直播间的封面图片地址。 |
| `backgroundURL` | `String` | 选填 | 直播间的背景图片地址。 |
| `categoryList` | `List<int>` | 选填 | 直播间的分类标签列表。 |
| `activityStatus` | `int` | 选填 | 直播活动状态。 |
| `isGiftEnabled` | `bool` | 选填 | 是否启用礼物功能（`true`：是，`false`：否）。 |

5. **结束直播**

   直播结束后，主播可以调用 **LiveListStore** 的 `endLive` 接口结束直播。SDK 会处理停止推流和销毁房间的逻辑。

   ``` java
   Future<void> _stopLive() async {
       // 1. 调用接口结束直播
       // SDK 内部会自动停止推流、销毁房间并清理媒体资源
       final result = await LiveListStore.shared.endLive();
   
       if (result.isSuccess) {
         debugPrint("关播成功");
         // 2. 退出当前页面
         if (mounted) {
           Navigator.of(context).pop();
         }
       } else {
         debugPrint("关播失败: ${result.errorMessage}");
       }
     }
   ```
6. **完整代码参考**

   为了方便您快速集成，我们将上述步骤整合为完整的 `YourAnchorPage` 文件。您可以直接复制以下代码：

   ``` java
   import 'package:flutter/material.dart';
   import 'package:atomic_x_core/atomicxcore.dart';
   import 'package:rtc_room_engine/rtc_room_engine.dart'; // 引入 RTC 引擎
   
   class YourAnchorPage extends StatefulWidget {
     final String liveId;
     const YourAnchorPage({super.key, required this.liveId});
   
     @override
     State<YourAnchorPage> createState() => _YourAnchorPageState();
   }
   
   class _YourAnchorPageState extends State<YourAnchorPage> {
     late final LiveCoreController _controller;
     bool _isLiveStarted = false; // 直播状态标记
   
     @override
     void initState() {
       super.initState();
       _controller = LiveCoreController.create(CoreViewType.pushView);
       _controller.setLiveID(widget.liveId);
       _openDevices(); // 步骤2：打开设备
     }
   
     void _openDevices() {
       DeviceStore.shared.openLocalCamera(true);
       DeviceStore.shared.openLocalMicrophone();
     }
   
     // 步骤3：构建预览
     Widget _buildLocalPreview() {
       return Container(
         color: Colors.black,
         child: VideoView(
           onViewCreated: (viewId) => TUIRoomEngine.sharedInstance().setLocalVideoView(viewId),
           onViewDisposed: (viewId) => TUIRoomEngine.sharedInstance().setLocalVideoView(0),
         ),
       );
     }
   
     // 步骤4：开播逻辑
     Future<void> _startLive() async {
       final liveInfo = LiveInfo(
         liveID: widget.liveId,
         liveName: "Test Live",
         seatLayoutTemplateID: 600,
         keepOwnerOnSeat: true,
       );
   
       final result = await LiveListStore.shared.createLive(liveInfo);
       if (result.isSuccess) {
         setState(() {
           _isLiveStarted = true; // 切换 UI 状态
         });
       }
     }
   
     @override
     Widget build(BuildContext context) {
       return Scaffold(
         body: Stack(
           children: [
             // 视图自动切换
             Positioned.fill(
               child: _isLiveStarted
                   ? LiveCoreWidget(controller: _controller)
                   : _buildLocalPreview(),
             ),
             // 开播按钮
             if (!_isLiveStarted)
               Positioned(
                 bottom: 50, left: 0, right: 0,
                 child: Center(
                   child: ElevatedButton(onPressed: _startLive, child: const Text('开始直播')),
                 ),
               ),
           ],
         ),
       );
     }
   }
   ```

### 步骤2：实现观众进房观看

观众观看流程如下，通过简单几步操作，即可实现观众观看直播。

> **提示：**
> 

> 观众进房拉流的业务代码，您也可以参考 TUILiveKit 开源项目中的 [audience_widget.dart](https://github.com/Tencent-RTC/TUIKit_Flutter/blob/main/live/livekit/lib/live_stream/features/audience/audience_widget.dart) 文件来了解完整的实现逻辑。
> 

1. **实现观众拉流页面**

   在您的观众页面中，创建 `LiveCoreWidget` 实例，并通过 `LiveCoreController` 控制直播行为。
   

   > **注意：**
   > 

   > **必须确保 LiveCoreWidget 在调用 joinLive() 之前已经完成初始化并处于渲染树中。**
   > 

   > **原理分析：**`LiveCoreWidget` 在 `initState` 中会执行 `controller.init() `以注册对 `currentLive` 信息的监听。如果先调用` joinLive()` 导致房间信息更新，而此时 `Widget` 尚未渲染（监听器未注册），则无法触发内部的自动拉流逻辑，导致画面黑屏。
   > 

   ``` java
   import 'package:flutter/material.dart';
   import 'package:atomic_x_core/atomicxcore.dart';
   
   /// YourAudiencePage 代表您的观众观看页面
   class _YourAudiencePageState extends State<YourAudiencePage> {
     late final LiveCoreController _controller;
     bool _isJoining = true;
   
     @override
     void initState() {
       super.initState();
       _controller = LiveCoreController.create(CoreViewType.playView);
       _controller.setLiveID(widget.liveId);
       
       // 修正：在第一帧渲染完成后再进房，确保 LiveCoreWidget 已完成 init() 
       WidgetsBinding.instance.addPostFrameCallback((_) {
         _joinLive();
       });
     }
   
     Future<void> _joinLive() async {
       final result = await LiveListStore.shared.joinLive(widget.liveId);
       if (result.isSuccess) {
         debugPrint("joinLive success");
         if (mounted) setState(() => _isJoining = false);
       } else {
         debugPrint("joinLive error: ${result.errorMessage}");
       }
     }
   
     @override
     Widget build(BuildContext context) {
       return Scaffold(
         body: Stack(
           children: [
             // 必须始终渲染，不可根据 _isJoining 状态移除，否则会导致监听失效
             LiveCoreWidget(controller: _controller),
             
             if (_isJoining)
               const Center(child: CircularProgressIndicator(color: Colors.white)),
           ],
         ),
       );
     }
   }
   ```
2. **进入直播间观看**

   通过调用 **LiveListStore** 的 `joinLive` 接口加入直播，**您无需做额外操作，LiveCoreWidget 会自动播放当前房间的视频流**，完整示例代码如下：

   ``` java
   import 'package:flutter/material.dart';
   import 'package:atomic_x_core/atomicxcore.dart';
   
   /// YourAudiencePage 代表您的观众观看页面
   class YourAudiencePage extends StatefulWidget {
     final String liveId;
   
     const YourAudiencePage({super.key, required this.liveId});
   
     @override
     State<YourAudiencePage> createState() => _YourAudiencePageState();
   }
   
   class _YourAudiencePageState extends State<YourAudiencePage> {
     late final LiveCoreController _controller;
   
     @override
     void initState() {
       super.initState();
       _controller = LiveCoreController.create();
       _controller.setLiveID(widget.liveId);
       // 进入直播间
       _joinLive();
     }
   
     Future<void> _joinLive() async {
       // 调用 LiveListStore.shared.joinLive 进入直播间
       // - liveId: 与主播开播同样的 liveId
       final result = await LiveListStore.shared.joinLive(widget.liveId);
   
       if (result.isSuccess) {
         debugPrint("joinLive success");
       } else {
         debugPrint("joinLive error: ${result.errorMessage}");
         // 进房失败，也需要退出页面
         // if (mounted) Navigator.of(context).pop();
       }
     }
   
     @override
     Widget build(BuildContext context) {
       return Scaffold(
         body: Stack(
           children: [
             LiveCoreWidget(controller: _controller),
           ],
         ),
       );
     }
   }
   ```
3. **退出直播**

   观众退出直播间时，需要调用 **LiveListStore** 的 `leaveLive` 接口退出直播。SDK 会自动停止拉流并退出房间。

   ``` java
   import 'package:flutter/material.dart';
   import 'package:atomic_x_core/atomicxcore.dart';
   
   /// YourAudiencePage 代表您的观众观看页面
   class YourAudiencePage extends StatefulWidget {
     final String liveId;
   
     const YourAudiencePage({super.key, required this.liveId});
   
     @override
     State<YourAudiencePage> createState() => _YourAudiencePageState();
   }
   
   class _YourAudiencePageState extends State<YourAudiencePage> {
     // ... 其他代码 ...
   
     // 退出直播
     Future<void> _leaveLive() async {
       final result = await LiveListStore.shared.leaveLive();
   
       if (result.isSuccess) {
         debugPrint("leaveLive success");
       } else {
         debugPrint("leaveLive error: ${result.errorMessage}");
       }
     }
   
     // ... 其他代码 ...
   }
   ```

### 步骤3：监听直播事件

在观众加入直播间后，您还需要处理一些房间内的"被动"事件。例如，主播主动结束了直播，或者观众因为违规等原因被踢出房间。如果不监听这些事件，观众端 UI 可能会停留在黑屏页面，影响用户体验。

您可以通过 `LiveListListener` 来实现事件监听。
``` java
import 'package:flutter/material.dart';
import 'package:atomic_x_core/atomicxcore.dart';

/// YourAudiencePage 代表您的观众观看页面
class YourAudiencePage extends StatefulWidget {
  final String liveId;

  const YourAudiencePage({super.key, required this.liveId});

  @override
  State<YourAudiencePage> createState() => _YourAudiencePageState();
}

class _YourAudiencePageState extends State<YourAudiencePage> {
  late final LiveCoreController _controller;
  // 1. 定义 LiveListListener 来管理事件监听
  late final LiveListListener _liveListListener;

  @override
  void initState() {
    super.initState();
    _controller = LiveCoreController.create();
    _controller.setLiveID(widget.liveId);
    // 2. 监听直播事件
    _setupLiveEventListener();
    // 3. 进入直播间
    _joinLive();
  }

  // 4. 新增一个方法来设置事件监听
  void _setupLiveEventListener() {
    _liveListListener = LiveListListener(
      onLiveEnded: (liveID, reason, message) {
        // 监听到直播结束
        debugPrint("Live ended. liveID: $liveID, reason: ${reason.value}, message: $message");
        // 在此处处理退出直播间的逻辑，例如关闭当前页面
        // if (mounted) Navigator.of(context).pop();
      },
      onKickedOutOfLive: (liveID, reason, message) {
        // 监听到被踢出直播
        debugPrint("Kicked out of live. liveID: $liveID, reason: ${reason.value}, message: $message");
        // 在此处处理退出直播间的逻辑
        // if (mounted) Navigator.of(context).pop();
      },
    );
    LiveListStore.shared.addLiveListListener(_liveListListener);
  }

  Future<void> _joinLive() async {
    final result = await LiveListStore.shared.joinLive(widget.liveId);
    if (result.isSuccess) {
      debugPrint("joinLive success");
    } else {
      debugPrint("joinLive error: ${result.errorMessage}");
    }
  }

  Future<void> _leaveLive() async {
    final result = await LiveListStore.shared.leaveLive();
    if (result.isSuccess) {
      debugPrint("leaveLive success");
    } else {
      debugPrint("leaveLive error: ${result.errorMessage}");
    }
  }

  @override
  void dispose() {
    // 5. 移除事件监听
    LiveListStore.shared.removeLiveListListener(_liveListListener);
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Stack(
        children: [
          LiveCoreWidget(controller: _controller),
        ],
      ),
    );
  }
}
```

### 运行效果

集成 **LiveCoreWidget** 后，您将得到一个纯净的视频渲染视图，它已具备完整的直播业务能力，但没有任何交互 UI。您可以参考下一章节 丰富直播场景 来完善直播场景。
|  | **动态宫格布局** | **浮动小窗布局** | **固定宫格布局** | **固定小窗布局** |
| --- | --- | --- | --- | --- |
| **模板 ID** | 600 | 601 | 800 | 801 |
| **描述** | 默认布局，可根据连麦人数动态调整宫格大小。 | 连麦嘉宾以浮动小窗形式显示。 | 连麦人数固定，每个嘉宾占据一个固定宫格。 | 连麦人数固定，嘉宾以固定小窗形式显示。 |

## 丰富直播场景

当您完成了基础的直播功能后，您可以参考以下功能指南来为直播添加丰富的互动玩法。
| **直播功能** | **功能介绍** | **功能 Stores** | **实现指南** |
| --- | --- | --- | --- |
| **实现观众音视频连线** | 观众申请上麦，与主播进行实时视频互动。 | [CoGuestStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_co_guest_store/CoGuestStore-class.html) | 实现观众连线 |
| **实现主播跨房连线 PK** | 两个不同房间的主播进行连线，实现互动或 PK。 | [CoHostStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_co_host_store/CoHostStore-class.html) / [BattleStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_battle_store/BattleStore-class.html) | 实现主播连线 PK |
| **添加弹幕聊天功能** | 观众可以在直播间发送和接收实时文字消息。 | [BarrageStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_barrage_barrage_store/BarrageStore-class.html) | 实现弹幕功能 |
| **构建礼物赠送系统** | 观众可以向主播赠送虚拟礼物，增加互动和趣味性。 | [GiftStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_gift_gift_store/GiftStore-class.html) | 实现礼物功能 |

## API 文档
| **Store/Component** | **功能描述** | **API 文档** |
| --- | --- | --- |
| **LiveCoreWidget** | 直播视频流展示与交互的核心视图组件：负责视频流渲染和视图挂件处理，支持主播直播、观众连麦、主播连线等场景。 | [API 文档](https://tencent-rtc.github.io/TUIKit_Flutter/api_view_live_live_core_widget/LiveCoreWidget-class.html) |
| **LiveCoreController** | LiveCoreWidget 的控制器：用于设置直播 ID、控制预览等操作。 | [API 文档](https://tencent-rtc.github.io/TUIKit_Flutter/api_view_live_live_core_widget/LiveCoreController-class.html) |
| **LiveListStore** | 直播间全生命周期管理：创建 / 加入 / 离开 / 销毁房间，查询房间列表，修改直播信息（名称、公告等），监听直播状态（如被踢出、结束）。 | [API 文档](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_live_list_store/LiveListStore-class.html) |
| **DeviceStore** | 音视频设备控制：麦克风（开关 / 音量）、摄像头（开关 / 切换 / 画质）、屏幕共享，设备状态实时监听。 | [API 文档](https://tencent-rtc.github.io/TUIKit_Flutter/api_device_device_store/DeviceStore-class.html) |
| **CoGuestStore** | 观众连麦管理：连麦申请 / 邀请 / 同意 / 拒绝，连麦成员权限控制（麦克风 / 摄像头），状态同步。 | [API 文档](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_co_guest_store/CoGuestStore-class.html) |
| **CoHostStore** | 主播跨房连线：支持多布局模板（动态网格等），发起 / 接受 / 拒绝连线，连麦主播互动管理。 | [API 文档](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_co_host_store/CoHostStore-class.html) |
| **BattleStore** | 主播 PK 对战：发起 PK（配置时长 / 对手），管理 PK 状态（开始 / 结束），同步分数，监听对战结果。 | [API 文档](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_battle_store/BattleStore-class.html) |
| **GiftStore** | 礼物互动：获取礼物列表，发送 / 接收礼物，监听礼物事件（含发送者、礼物详情）。 | [API 文档](https://tencent-rtc.github.io/TUIKit_Flutter/api_gift_gift_store/GiftStore-class.html) |
| **BarrageStore** | 弹幕功能：发送文本 / 自定义弹幕，维护弹幕列表，实时监听弹幕状态。 | [API 文档](https://tencent-rtc.github.io/TUIKit_Flutter/api_barrage_barrage_store/BarrageStore-class.html) |
| **LikeStore** | 点赞互动：发送点赞，监听点赞事件，同步总点赞数。 | [API 文档](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_like_store/LikeStore-class.html) |
| **LiveAudienceStore** | 观众管理：获取实时观众列表（ID / 名称 / 头像），统计观众数量，监听观众进出事件。 | [API 文档](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_live_audience_store/LiveAudienceStore-class.html) |
| **AudioEffectStore** | 音频特效：变声（童声 / 男声）、混响（KTV 等）、耳返调节，实时切换特效。 | [API 文档](https://tencent-rtc.github.io/TUIKit_Flutter/api_device_audio_effect_store/AudioEffectStore-class.html) |
| **BaseBeautyStore** | 基础美颜：调节磨皮 / 美白 / 红润（0-100 级），重置美颜状态，同步效果参数。 | [API 文档](https://tencent-rtc.github.io/TUIKit_Flutter/api_device_base_beauty_store/BaseBeautyStore-class.html) |

## 常见问题

### 主播调用 createLive 或 观众调用 joinLive 后为什么画面是黑的，没有视频画面？
- **检查 setLiveID**：请确保在调用开播或观看接口前，已经为 `LiveCoreController` 实例设置了正确的 `liveID`。

- **检查设备权限**：请确保 App 已获得摄像头和麦克风的系统使用权限。

- **检查主播端**：主播端是否正常调用 `DeviceStore.shared.openLocalCamera(true)` 打开了摄像头。

- **检查网络**：请检查设备网络连接是否正常。

### 观众端调用了 joinLive 且返回 Success，但依然没有视频画面？
- **时序问题：**是否在 LiveCoreWidget 挂载前就执行了 joinLive？请参考上文使用 addPostFrameCallback。

- **Controller 类型：**创建时是否正确传入了 CoreViewType.playView？

- **Widget 持久性：**在进房过程中，LiveCoreWidget 是否因为 setState 被意外销毁或重新创建？请确保其在 Widget 树中的稳定性。

### Flutter 项目如何请求权限？

您可以使用 `permission_handler` 插件来请求摄像头和麦克风权限：
``` java
import 'package:permission_handler/permission_handler.dart';

Future<void> requestPermissions() async {
  await [
    Permission.camera,
    Permission.microphone,
  ].request();
}
```

### 如何在 Flutter 中处理页面生命周期？

建议在 `dispose` 方法中清理资源，例如移除事件监听器：
``` java
@override
void dispose() {
  LiveListStore.shared.removeLiveListListener(_liveListListener);
  super.dispose();
}
```

---

## 概述

本文对 TUILiveKit Demo 中的**直播列表页面**进行了详细的介绍，您可以在已有项目中直接参考本文档集成我们开发好的直播列表页面，也可以根据您的需求按照文档中的内容对页面的样式，布局以及功能项进行深度的定制。

## 快速体验

您可以在 在线体验 中使用 [在线开播网站](https://web.sdk.qcloud.com/trtc/livekit/pusher/index.html#/?fromMark=123016) 快速开启一场直播，同时您也可以使用 [在线观看网站](https://web.sdk.qcloud.com/trtc/livekit/player/index.html#/?fromMark=123016) 来查看账户下直播列表。

## 快速接入

### 步骤1：环境配置及开通服务

在进行快速接入之前，请参考 准备工作 集成组件并实现登录。

### 步骤2：安装依赖

您可以选择以下任一方式安装依赖：

【npm】
``` bash
npm install tuikit-atomicx-vue3 @tencentcloud/uikit-base-component-vue3 --save
```

【pnpm】
``` bash
pnpm add tuikit-atomicx-vue3 @tencentcloud/uikit-base-component-vue3
```

【yarn】
``` bash
yarn add tuikit-atomicx-vue3 @tencentcloud/uikit-base-component-vue3
```

### 步骤3: 直播列表页面接入

在您的项目下创建 **live-list.vue **文件，可直接复制如下代码至您的项目中集成**直播列表页面**。

> **注意：**
> 

> 您可以直接复制如下代码至您的工程中集成示例工程，也可以访问 [直播列表](https://github.com/Tencent-RTC/TUILiveKit/blob/main/Web/web-vite-vue3/src/TUILiveKit/LiveListView.vue) 地址，查看更加详细的源码内容。
> 

``` typescript
<template>
  <UIKitProvider theme="dark">
    <div class="container">
      <header class="header">
        <h1 class="title">在线直播</h1>
      </header>
      <main class="main">
        <LiveList /> 
      </main>
    </div>
  </UIKitProvider>
</template>

<script setup lang="ts">
import { onMounted } from 'vue';
import { LiveList, useLoginState } from 'tuikit-atomicx-vue3';
import { UIKitProvider } from '@tencentcloud/uikit-base-component-vue3';

const { login } = useLoginState();

async function initLogin() {
  try {
    await login({
      sdkAppId: 0,        // SDKAppID, 可以参考步骤 1 获取
      userId: '',         // UserID, 可以参考步骤 1 获取
      userSig: '',        // userSig, 可以参考步骤 1 获取
    });
  } catch (error) {
    console.error('登录失败:', error);
  }
}

onMounted(async () => {
  await initLogin();
});
</script>

<style scoped>:global(*),:global(::after),:global(::before){box-sizing:border-box;margin:0}.container{display:flex;flex-direction:column;height:100vh;width:100vw;background:var(--bg-color-default)}.header{display:flex;align-items:center;flex-shrink:0}.title{margin:0;font-size:16px;font-weight:600;color:var(--text-color-primary);letter-spacing:-.5px}.main{flex:1;padding:24px;overflow-y:auto;min-height:0}</style>
```

> **注意：**
> 

> 若您需要实现直播列表到进入直播间的跳转逻辑，可参考本文中 指定直播间 部分内容。
> 

## 启动项目

### 开启您的直播列表页面

通过下列命令启动成功后，通过访问本地地址打开直播列表页面。

> **说明：**
> 

> 上述命令执行成功后，请在浏览器地址栏输入本地访问地址（您可以根据项目参考，例如` http://localhost:5173/live-list`，具体端口号可能因您的项目配置而有所不同），即可看到直播列表页面。
> 

``` bash
  npm run dev
```

### 指定直播间

由于涉及到直播列表(或首页)到观看页面的跳转逻辑，您需要配置 Vue Router 来实现页面跳转 。您可以在项目 `src` 目录下新建 `router` 文件夹，并创建 `index.ts` 文件。然后，在您的主文件（例如 **main.ts **或 **index.ts**）中引入并使用路由。可参见 [GitHub 代码示例](https://github.com/Tencent-RTC/TUILiveKit/blob/main/Web/web-vite-vue3/src/main.ts)。

#### 步骤1：配置页面路由

请配置您的 Vue Router，将`live-list.vue` 映射到直播列表页面。

> **注意：**
> 
> - 如果您的业务项目中已有 `src/router/index.ts` 文件，请将以下内容合并到已有代码中。
> - 如果尚未配置路由，请新建 `src/router/index.ts` 文件并添加以下配置。

``` typescript
import { createRouter, createWebHistory } from 'vue-router';

const routes = [
  {
    // 直播列表页面, 注意以下代码路径为您项目实际路径
    path: '/live-list',
    component: () => import('../live-list.vue'),
  },  
  // 若您需要实现通过点击直播列表直播间封面到对应直播间进行观看，则需要参考如下示例配置观看页面的路由
  {
    // 路由跳转至观看页面, 注意以下代码路径为您项目实际路径
    path: '/live-player',
    component: () => import('../live-player.vue'),
  },
];

const router = createRouter({
  history: createWebHistory(),
  routes,
});
export default router;

```

#### 步骤2：配置 src/main.ts 文件

将路由和多语言配置合并到您项目中的入口文件 src/main.ts 中：
``` java
// src/main.ts
import { createApp } from 'vue';
import App from './App.vue';
import router from './router';

const app = createApp(App);
app.use(router);
app.mount('#app');
```

#### 步骤3：配置 live-list 文件

您需要将以下内容合并到上文中的 步骤3 内容中，进行直播列表到观看页面的跳转。
``` typescript
// live-list.vue 可增量添加至您的代码中
<template>
  <UIKitProvider>
     // .....省略部分参考快速接入步骤 3 部分
     <LiveList @live-room-click="handleLiveRoomClick" />
  </UIKitProvider>
</template>

<script setup lang="ts">
import { useRouter, useRoute } from 'vue-router';

const router = useRouter();
const route = useRoute();

function handleLiveRoomClick(liveInfo: LiveInfo) {
  if (liveInfo?.liveId) {
    router.push({ path: '/live-player', query: { ...route.query, liveId: liveInfo.liveId } });
  }
}

</script>
```

## 自由定制

根据上述功能展示图，我们也支持您根据项目需求对直播列表页面进行 UI 定制。主要可供定制的能力如下表所示。
| **类别** | **功能** | **描述** |
| --- | --- | --- |
| **直播间列表** | 自定义直播间列表区域展示 | **支持：** - **直播间信息文字 展示/隐藏、UI 进行定制。** - **直播间一行/一列展示固定数量定制。** |
| **个人信息** | 自定义个人信息展示 | **支持：** - **展示/隐藏个人信息。** - **个人信息字体、颜色 UI 自定义设置。** |

### 颜色主题及语言

通过配置 `App.vue` 中 `UIKitProvider` 的入参，修改主题及语言的默认值。
| UIKitProvider 参数 | 可选值 | 默认值 |
| --- | --- | --- |
| theme | "light" \\| "dark" | "light" |
| language | "zh-CN" \\| "en-US" | - |

``` typescript
<UIKitProvider theme="light">
  <router-view />
</UIKitProvider>
 
<script setup lang="ts">
import { UIKitProvider } from '@tencentcloud/uikit-base-component-vue3';
```

### 按钮 Button 和 图标 Icon

您可以对按钮、图标等控件进行自定义。以` live-list.vue` 为例，对` Button`、`Icon` 控件执行增删改等操作都可以满足您的自定义需求。除布局调整外，我们还支持对颜色、字体、圆角以及输入框、弹框等内容进行全面修改，充分满足您的 UI 定制需求。
| **类别** | **功能** | **描述** |
| --- | --- | --- |
| **素材管理** | 自定义素材管理区域展示 | 支持调整 Icon 的大小、颜色或对 Icon 进行替换。 |
| **直播工具** | 自定义直播工具信息展示 | 支持调整 Icon 的大小、颜色或对 Icon 进行替换。 |
| **在线观众** | 自定义观众信息展示 | 支持： - 展示/隐藏观众等级。 - 观众信息字体、颜色 UI 自定义设置。 - 替换为您需要的 Icon 风格。 |
| **消息列表** | 自定义消息弹幕区域展示 | 支持： - 展示/隐藏聊天输入区域。 - 支持 UI 定制聊天气泡风格、定制观众等级等内容。 |

### 设置昵称及头像

如果您需要自定义昵称或头像，可以在 步骤 3 中的示例代码中通过 [setSelfInfo](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setSelfInfo) 进行设置，具体示例如下：
``` typescript
import { useLoginState } from 'tuikit-atomicx-vue3';

const { setSelfInfo } = useLoginState();

// 设置用户个人信息
await setSelfInfo({
  userName: '张三',
  avatarUrl: 'https://example.com/avatar.png',
});
```

## 下一步

恭喜您，现在您已经成功集成了**直播列表页面**。接下来，您可以实现**主播开播页**、**观众观看页**和 **UI 自定义**等内容，可参考下表：
| **功能** | **描述** | **集成指引** |
| --- | --- | --- |
| **观众观看** | 实现观众进入主播的直播间后观看直播，实现观众连麦 、直播间信息、在线观众、弹幕显示等功能。 | 观众观看（Web Vue3） |
| **主播开播** | 主播在当前页面开始直播及相关设置。 | 主播开播（Web Vue3） |
| **UI 自定义** | 更详细的 UI 组件自定义指引。 | UI 自定义 |
| **Web 监播** | 运营平台，支持直播间管控。 | 监播页面（Web Vue3） |

---

本文将介绍如何接入 TUILiveKit Demo 的**主播开播页**，指导您将我们提供的开播页面集成到您的项目中，同时介绍如何对直播页面的样式、布局、以及功能进行自定义修改。

## 功能展示
- **横屏开播**

   

- **竖屏开播**

   

## 功能概览
- **画面源管理**：支持添加多个摄像头、屏幕分享、窗口分享和本地图片。

- **直播画面排版**：支持对画面源拖拽、缩放，支持通过快捷菜单对画面源设置镜像、旋转和层级调整。

- **观众连麦**：支持房间内观众连麦，内置多种连麦布局。

- **主播 PK**：支持主播跨房连线、PK。

- **互动聊天**：支持收发文字和表情消息，聊天互动。

- **观众管理**：支持对观众禁言、踢出直播间等操作。

## 快速接入

### 步骤1：环境配置及开通服务

在进行快速接入之前，请参考 准备工作 集成组件并实现登录。

### 步骤2:  安装依赖

【npm】
``` bash
npm install tuikit-atomicx-vue3 @tencentcloud/uikit-base-component-vue3 --save
```

【pnpm】
``` bash
pnpm add tuikit-atomicx-vue3 @tencentcloud/uikit-base-component-vue3
```

【yarn】
``` bash
yarn add tuikit-atomicx-vue3 @tencentcloud/uikit-base-component-vue3
```

### 步骤3：主播开播页面接入

在您的项目下创建 `live-pusher.vue` 文件，通过复制如下代码至您新建的 `live-pusher.vue` 文件中集成完整的**主播开播页面**。

> **注意：**
> 

> 您可以直接复制如下代码至您的工程中集成示例工程，也可以访问 [开播页面](https://github.com/Tencent-RTC/TUILiveKit/blob/main/Web/web-vite-vue3/src/TUILiveKit/LivePusherView.vue) 地址，查看更加详细的源码内容。
> 

``` typescript
<template>
  <UIKitProvider language="zh-CN" theme="dark">
    <div class="custom-live-pusher">
      <!-- 主要内容区 -->
      <div class="main-content">
        <!-- 左侧：视频源和工具 -->
        <div class="left-panel">
          <div class="scene-section">
            <div class="panel-title">画面源</div>
            <LiveScenePanel />
          </div>
        </div>

        <!-- 中央：直播画面 -->
        <div class="center-panel">
          <div class="stream-section">
            <div class="stream-header">
              <div class="stream-title">
                <span>{{ liveName }}</span>
              </div>
              <div class="stream-audience">{{ audienceCount }} 人在观看</div>
            </div>
            <StreamMixer />
          </div>
          <div class="live-controls">
            <div class="bottom-panel">
              <!-- <MediaDeviceSetting />// 媒体设置能力请参考本文高级功能集成部分
              <CoGuestButton />          // 连麦观众能力请参考本文高级功能集成部分
              <OrientationSwitch />      // 布局设置请参考本文高级功能集成部分
              <LayoutSwitch />           // 横竖屏推流能力请参考本文高级功能集成部分 -->
            </div>
            <TUIButton type="primary" v-if="!currentLive?.liveId" @click="handleStartLive">开始直播</TUIButton>
            <TUIButton color="red" v-else @click="handleStopLive">停止直播</TUIButton>
          </div>
        </div>

        <!-- 右侧：观众互动 -->
        <div class="right-panel">
          <div class="audience-section">
            <div class="panel-title">在线观众({{ audienceCount }})</div>
            <LiveAudienceList />
          </div>
          <div class="message-section">
            <div class="panel-title">消息列表</div>
            <BarrageList />
            <BarrageInput />
          </div>
        </div>

      </div>
    </div>
  </UIKitProvider>
</template>

<script setup lang="ts">
import { onMounted } from 'vue';
import { UIKitProvider, TUIButton } from '@tencentcloud/uikit-base-component-vue3';
import { LiveScenePanel, StreamMixer, LiveAudienceList, BarrageList, BarrageInput, useLiveListState, useLiveAudienceState, useLoginState } from 'tuikit-atomicx-vue3';

const { login, setSelfInfo } = useLoginState();
const { createLive, currentLive, endLive } = useLiveListState();
const { audienceCount } = useLiveAudienceState();
const liveName = '我的直播间';

const handleStartLive = async () => {
  // 创建直播间
  await createLive({
    liveId: 'my-live-room',       // 直播间 ID
    liveName: liveName,           // 直播间名称
    coverUrl: '',                 // 直播间封面 URL
    isPublicVisible: true,        // 是否公开可见
    seatLayoutTemplateId: 600,    // 麦位布局模板 ID
  });
  // 设置个人信息
  await setSelfInfo({
    userName: '我的名字/昵称',    // 用户名
    avatarUrl: '',              // 头像 URL 地址
  });
};

const handleStopLive = async () => {
  await endLive();
};

async function initLogin() {
  try {
    await login({
      sdkAppId: 0,        // SDKAppID, 可以参考步骤 1 获取
      userId: '',         // UserID, 可以参考步骤 1 获取
      userSig: '',        // userSig, 可以参考步骤 1 获取
    });
  } catch (error) {
    console.error('登录失败:', error);
  }
}

onMounted(async () => {
  await initLogin();
});

</script>

<style>html,body,#app{height:100%;width:100%;margin:0;padding:0}</style>
<style scoped>.custom-live-pusher,.left-panel{flex-direction:column;display:flex}.custom-live-pusher,.live-title{color:var(--text-color-primary)}.live-controls,.tools-section,.top-controls{backdrop-filter:blur(10px)}*{box-sizing:border-box;margin:0;padding:0}:global(::before){box-sizing:border-box;margin:0;padding:0}.layout-label,.template-options{margin-bottom:16px}:global(body){line-height:1.6;color:var(--text-color-primary);background:var(--bg-color-default)}.custom-live-pusher{height:100vh;width:100vw;background:linear-gradient(135deg,var(--bg-color-default) 0,var(--bg-color-function) 100%);overflow:hidden}.top-controls{display:flex;justify-content:space-between;align-items:center;padding:12px 20px;background:var(--bg-color-operate);border-bottom:1px solid var(--stroke-color-primary);z-index:100;min-height:60px}.live-title{font-size:18px;font-weight:600;text-shadow:0 2px 4px var(--shadow-color)}.audience-count{font-size:14px;color:var(--text-color-error);background:var(--uikit-color-red-1);padding:6px 12px;border-radius:20px;border:1px solid var(--uikit-color-red-3)}.live-controls,.tools-section{background:var(--bg-color-operate)}.main-content{display:flex;flex:1;height:calc(100vh - 60px);gap:16px;padding:16px;overflow:hidden}.left-panel{width:320px;gap:16px;flex-shrink:0}.panel-title{font-size:16px;font-weight:600;color:var(--text-color-primary);margin-bottom:12px;text-align:left}.audience-section,.message-section,.scene-section{display:flex;flex-direction:column;background:var(--bg-color-operate);border-radius:12px;border:1px solid var(--stroke-color-primary);padding:16px;overflow:hidden}.scene-section{flex:1;min-height:0}.message-section{flex:1;min-height:0}.message-section :deep(input),.message-section :deep(textarea){text-align:left}.tools-section{border-radius:12px;padding:16px;border:1px solid var(--stroke-color-primary)}.center-panel{display:flex;flex-direction:column;flex:1;gap:16px;min-width:0}.stream-section{display:flex;flex-direction:column;flex:1;min-height:0;background:var(--bg-color-operate);border-radius:12px;border:1px solid var(--stroke-color-primary);overflow:hidden}.stream-header{display:flex;justify-content:space-between;align-items:center;padding:22px;border-bottom:1px solid var(--stroke-color-primary)}.stream-title{display:flex;align-items:center;gap:8px;font-size:18px;font-weight:500;color:var(--text-color-primary)}.stream-audience{font-size:14px;color:var(--text-color-primary)}.live-controls{display:flex;justify-content:space-between;align-items:center;padding:16px;border-radius:12px;border:1px solid var(--stroke-color-primary);gap:16px}.live-controls button{padding:18px 20px}.right-panel{display:flex;flex-direction:column;width:320px;gap:16px;flex-shrink:0}.center-panel>.live-controls,.left-panel>*,.right-panel>*{background:var(--bg-color-operate);border-radius:12px;border:1px solid var(--stroke-color-primary);overflow:hidden}.left-panel>*{padding:16px}.left-panel>.panel-title,.scene-section>.panel-title,.audience-section>.panel-title,.message-section>.panel-title{padding:0;background:transparent;border:none;border-radius:0}.custom-icon-container,.device-setting{padding:8px 12px;background:var(--bg-color-function)}.stream-section :deep(>*:last-child){flex:1;min-height:300px}.bottom-panel,.device-setting{align-items:center;display:flex}.custom-icon-container:hover,.option-card:hover{border-color:var(--stroke-color-primary);background:var(--list-color-hover)}.bottom-panel{gap:16px;flex:1}.device-setting{gap:8px;border-radius:8px;border:1px solid var(--stroke-color-secondary)}.device-icon{cursor:pointer;color:var(--text-color-primary);transition:color .2s}.device-icon:hover{color:var(--text-color-link)}.device-slider{width:80px}.custom-icon-container{display:flex;align-items:center;gap:6px;border-radius:8px;border:1px solid var(--stroke-color-secondary);cursor:pointer;transition:.2s;position:relative}.custom-icon-container.disabled{opacity:.5;cursor:not-allowed}.custom-icon-container.disabled:hover{background:var(--bg-color-function);border-color:var(--stroke-color-secondary)}.custom-icon{width:16px;height:16px;display:inline-block;background-size:contain;background-repeat:no-repeat;background-position:center}.custom-text{font-size:12px;color:var(--text-color-secondary);white-space:nowrap}.unread-count{position:absolute;top:-4px;right:-4px;background:var(--text-color-error);color:var(--text-color-button);border-radius:10px;padding:2px 6px;font-size:10px;font-weight:600;min-width:16px;text-align:center;line-height:1}.layout-label,.option-info h4{color:var(--text-color-primary)}.layout-dialog{max-width:600px}.layout-label{font-size:16px;font-weight:600}.options-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(120px,1fr));gap:12px}.option-card{padding:16px;background:var(--bg-color-function);border:2px solid var(--stroke-color-secondary);border-radius:8px;cursor:pointer;transition:.2s;text-align:center}.option-card.active{border-color:var(--text-color-link);background:var(--bg-color-operate)}.option-info h4{margin:8px 0 0;font-size:12px}.option-icon{width:32px;height:32px;margin:0 auto;color:var(--text-color-secondary)}.co-guest-dialog{max-width:500px}.co-guest-panel{min-height:300px}</style>
```

#### 核心 API 参数说明

##### **createLive**

创建一个新的直播间，并设置直播间的基础信息。
| 参数 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| liveId | String | 是 | 直播间 ID，需保证全局唯一。 |
| liveName | String | 是 | 直播间名称，用于界面展示。 |
| coverUrl | String | 否 | 直播间封面图片的 URL 地址。 |
| isPublicVisible | Boolean | 否 | 是否公开可见。默认为 true，表示公开。 |
| seatLayoutTemplateId | Number | 否 | 麦位布局模板 ID。600 代表竖屏动态宫格布局，更多模板 ID 请参考高级功能章节。 |

##### setSelfInfo

设置用户信息。
| 参数 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| userName | String | 是 | 用户昵称，将在直播间及聊天区域显示。 |
| avatarUrl | String | 否 | 用户头像的 URL 地址。 |

### 步骤4：开启直播

开启您的第一场直播。
``` bash
  npm run dev
```

> **说明：**
> 

> 上述命令执行成功后，请在浏览器地址栏输入本地访问地址（您可以根据项目参考，例如` http://localhost:5173/live-pusher`，具体端口号可能因您的项目配置而有所不同），即可看到开播页面。
> 

### 步骤5：观看直播
- **方式一：（推荐）**

   通过我们提供的 [在线观看网站](https://web.sdk.qcloud.com/trtc/livekit/player/index.html#/?fromMark=123470)，立刻观看您开启的直播。

- **方式二：**

   集成我们提供的 观众观看（Web 桌面浏览器）或者 观众观看（H5 移动端浏览器） 页面，观看直播。
   

   > **重要提示：**
   > 

   > 请使用不同的**用户 ID** 登录观看： 开播端和观看端必须使用**不同**的用户 ID，否则后登录的设备会强制先登录的设备下线（即“被踢下线”）。
   > 

## 高级功能集成

> **注意：**
> 

> 以下高级功能均是基于 步骤 3 中创建的 `live-pusher.vue` 示例文件进行的扩展。请根据您的业务需求，将下方的代码片段集成到 `live-pusher.vue` 的对应位置（`template` 区域或 `script` 逻辑中），以启用相应的能力。
> 

【支持媒体设置能力】

若您需要支持媒体设置能力，包括设置扬声器、麦克风音量大小等内容，请参考如下代码示例复制到`live-pusher.vue `文件中即可。
``` typescript
<!-- MediaDeviceSetting 媒体设备设置 -->
<template>
  <div class="media-device-container">
    <!-- MicVolumeSetting 麦克风设置 -->
    <div class="device-setting">
      <TUIIcon class="device-icon" :icon="microphoneIsOn ? IconAudioOpen : IconAudioClose" :size="20" @click="switchMicrophoneStatus" />
      <TUISlider v-model="microphoneVolume" class="device-slider" :min="0" :max="100" :disabled="!microphoneIsOn" @change="handleMicrophoneVolumeChange" />
    </div>
    <!-- SpeakerVolumeSetting 扬声器设置 -->
    <div class="device-setting">
      <TUIIcon class="device-icon" :icon="speakerIsOn ? IconSpeakerOn : IconSpeakerOff" :size="20" @click="switchSpeaker(!speakerIsOn)" />
      <TUISlider v-model="speakerVolume" class="device-slider" :min="0" :max="100" :disabled="!speakerIsOn" @change="handleSpeakerVolumeChange" />
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref, watch } from 'vue';
import { TUIIcon, TUISlider, IconSpeakerOn, IconSpeakerOff, IconAudioOpen, IconAudioClose } from '@tencentcloud/uikit-base-component-vue3';
import { useDeviceState } from 'tuikit-atomicx-vue3';

const {
  captureVolume,
  setCaptureVolume,
  openLocalMicrophone,
  closeLocalMicrophone,
} = useDeviceState();
const { outputVolume, setOutputVolume } = useDeviceState();
const microphoneVolume = ref(captureVolume.value);
const speakerVolume = ref(outputVolume.value);
const microphoneIsOn = ref(true);
const speakerIsOn = ref(true);
const templateSpeakerVolume = ref(outputVolume.value);
const templateMicrophoneVolume = ref(captureVolume.value);

const handleMicrophoneVolumeChange = (value: number) => {
  if (value !== captureVolume.value) {
    setCaptureVolume(value);
  }
};

const switchMicrophoneStatus = () => {
  microphoneIsOn.value = !microphoneIsOn.value;
  if (!microphoneIsOn.value) {
    templateMicrophoneVolume.value = captureVolume.value;
    closeLocalMicrophone();
  } else {
    openLocalMicrophone();
    setCaptureVolume(templateMicrophoneVolume.value);
  }
};

const switchSpeaker = (open: boolean) => {
  speakerIsOn.value = open;
  if (!open) {
    templateSpeakerVolume.value = outputVolume.value;
    setOutputVolume(0);
  } else {
    setOutputVolume(templateSpeakerVolume.value);
  }
};

const handleSpeakerVolumeChange = (value: number) => {
  if (value !== outputVolume.value) {
    setOutputVolume(value);
  }
};

watch(captureVolume, (newVal) => {
  microphoneVolume.value = newVal;
});

watch(outputVolume, (newVal) => {
  speakerVolume.value = newVal;
});
</script>

<style scoped>.media-device-container{display:flex;align-items:center;gap:12px}.device-setting{display:flex;align-items:center;gap:8px;padding:12px 16px;background:var(--bg-color-function);border-radius:8px;border:1px solid var(--stroke-color-secondary)}.device-slider{width:100px}.device-icon{cursor:pointer;color:var(--text-color-primary);transition:color .2s}.device-icon:hover{color:var(--text-color-link)}</style>

```

【支持横竖屏推流能力】

若您需要支持横竖屏推流能力，包括设置切换横竖屏等内容，请参考如下代码示例复制到`live-pusher.vue `文件中即可。
``` typescript
<!-- LayoutSwitch 横竖屏推流设置 -->
<template>
  <div
    class="custom-icon-container"
    :class="{ disabled: currentLive?.liveId }"
    @click="handleOrientationSwitch"
  >
    <IconHorizontalMode
      v-if="currentOrientation === LiveOrientation.Landscape"
      class="custom-icon"
    />
    <IconPortrait
      v-else
      class="custom-icon"
    />
    <span class="custom-text co-guest-text">{{
      currentOrientation === LiveOrientation.Portrait ? t('Portrait') : t('Landscape')
    }}</span>
  </div>
</template>

<script setup lang="ts">
import { ref, watch } from 'vue';
import { useUIKit, TUIToast, TOAST_TYPE, IconPortrait, IconHorizontalMode } from '@tencentcloud/uikit-base-component-vue3';
import { useLiveListState, LiveOrientation } from 'tuikit-atomicx-vue3';

const { t } = useUIKit();

enum TUISeatLayoutTemplate {
  LandscapeDynamic_1v3 = 200,
  PortraitDynamic_Grid9 = 600,
  PortraitDynamic_1v6 = 601,
  PortraitFixed_Grid9 = 800,
  PortraitFixed_1v6 = 801,
  PortraitFixed_6v6 = 802,
}

const { currentLive, updateLiveInfo } = useLiveListState();
const currentOrientation = ref(LiveOrientation.Portrait);

watch(
  () => currentLive.value?.layoutTemplate,
  newVal => {
    if (newVal === TUISeatLayoutTemplate.LandscapeDynamic_1v3) {
      currentOrientation.value = LiveOrientation.Landscape;
    } else {
      currentOrientation.value = LiveOrientation.Portrait;
    }
  },
  { immediate: true }
);

const handleOrientationSwitch = () => {
  if (currentLive.value?.liveId) {
    TUIToast({
      message: t('Cannot switch orientation during live streaming'),
      type: TOAST_TYPE.ERROR,
    });
    return;
  }
  if (currentOrientation.value === LiveOrientation.Portrait) {
    updateLiveInfo({ layoutTemplate: TUISeatLayoutTemplate.LandscapeDynamic_1v3 });
  } else {
    updateLiveInfo({ layoutTemplate: TUISeatLayoutTemplate.PortraitDynamic_Grid9 });
  }
};
</script>

<style scoped>.custom-icon-container{display:flex;flex-direction:column;align-items:center;justify-content:center;gap:4px;width:56px;height:56px;cursor:pointer;color:var(--text-color-primary);border-radius:12px;position:relative}.custom-icon{width:24px;height:24px;background:transparent}.custom-text{font-size:12px}.custom-icon-container:not(.disabled):hover{box-shadow:0 0 10px 0 var(--bg-color-mask)}.custom-icon-container:not(.disabled):hover .custom-icon,.custom-icon-container:not(.disabled):hover .custom-text{color:var(--text-color-link)}.custom-icon-container.disabled{cursor:not-allowed;opacity:.5;color:var(--text-color-secondary)}.custom-icon-container.disabled .custom-icon,.custom-icon-container.disabled .custom-text{color:var(--text-color-secondary);cursor:not-allowed}</style>
```

【支持连观众能力】

若您需要支持观众连麦能力，包括设置连麦申请、连麦管理等内容，请参考如下代码示例复制到`live-pusher.vue `文件中即可。
``` typescript
<!-- CoGuestButton 观众连麦设置 -->
<template>
  <div class="custom-icon-container" :class="{ disabled: disabled }" @click="handleCoGuest">
    <span v-if="applicants.length > 0" class="unread-count">{{ applicants.length }}</span>
    <IconCoGuest class="custom-icon" />
    <span class="custom-text co-guest-text">{{ t('CoGuest') }}</span>
  </div>
  <TUIDialog :title="t('CoGuest')" :visible="coGuestPanelVisible" :custom-classes="['co-guest-dialog']" @close="coGuestPanelVisible = false" @confirm="coGuestPanelVisible = false" @cancel="coGuestPanelVisible = false">
    <CoGuestPanel class="co-guest-panel" />
    <template #footer>
      <div />
    </template>
  </TUIDialog>
</template>

<script lang="ts" setup>
import { computed, ref, watch } from 'vue';
import { useUIKit, TUIDialog, TUIToast, TOAST_TYPE, IconCoGuest } from '@tencentcloud/uikit-base-component-vue3';
import { CoGuestPanel, CoHostStatus, useCoGuestState, useCoHostState, useLiveListState } from 'tuikit-atomicx-vue3';

const { t } = useUIKit();
const { applicants } = useCoGuestState();
const { currentLive } = useLiveListState();
const { coHostStatus } = useCoHostState();
const disabled = computed(() => !currentLive.value?.liveId || coHostStatus.value !== CoHostStatus.Disconnected);

const coGuestPanelVisible = ref(false);

const handleCoGuest = () => {
  if (disabled.value) {
    const message = !currentLive.value?.liveId
      ? t('Cannot use co-guest before live starts')
      : t('Cannot enable audience co-hosting while co-hosting with other hosts');
    TUIToast({ type: TOAST_TYPE.ERROR, message });
    return;
  }
  coGuestPanelVisible.value = true;
};

watch(disabled, () => {
  if (disabled.value) {
    coGuestPanelVisible.value = false;
  }
});
</script>

<style scoped>.custom-icon-container{display:flex;flex-direction:column;align-items:center;justify-content:center;gap:4px;width:56px;height:56px;cursor:pointer;color:var(--text-color-primary);border-radius:12px;position:relative}.unread-count{position:absolute;top:0;right:0;background-color:var(--text-color-error);border-radius:50%;width:16px;height:16px;display:flex;align-items:center;justify-content:center;font-size:12px}.custom-icon{width:24px;height:24px;background:transparent}.custom-text{font-size:12px}.custom-icon-container:not(.disabled):hover{box-shadow:0 0 10px 0 var(--bg-color-mask)}.custom-icon-container:not(.disabled):hover .custom-icon,.custom-icon-container:not(.disabled):hover .custom-text{color:var(--text-color-link)}.custom-icon-container.disabled{cursor:not-allowed;opacity:.5;color:var(--text-color-secondary)}.custom-icon-container.disabled .custom-icon{cursor:not-allowed}.custom-icon-container.disabled .custom-text{color:var(--text-color-secondary)}.co-guest-panel{height:560px}:deep(.co-guest-dialog){width:520px}</style>
```

【支持布局设置能力】

若您需要支持视频流切换布局能力，包括设置**动态宫格布局、静态宫格布局、静态小窗布局、浮动小窗布局**等内容，请参考如下代码示例复制到`live-pusher.vue `文件中即可。
``` typescript
<!-- OrientationSwitch 布局设置 -->
<template>
  <div
    class="custom-icon-container"
    :class="{ 'disabled': disabled }"
    @click="handleSwitchLayout"
  >
    <IconLayoutTemplate class="custom-icon" />
    <span class="custom-text setting-text">{{ t('Layout Settings') }}</span>
  </div>
  <TUIDialog
    :customClasses="['layout-dialog']"
    :title="t('Layout Settings')"
    :visible="layoutSwitchVisible"
    @close="handleCancel"
    @confirm="handleConfirm"
    @cancel="handleCancel"
    appendTo="body"
  >
    <div class="layout-label">
      {{ t('Audience Layout') }}
    </div>
    <div class="template-options">
      <div class="options-grid">
        <template
          v-for="template in layoutOptions"
          :key="template.id"
        >
          <div
            class="option-card"
            :class="{ active: selectedTemplate === template.templateId }"
            @click="selectTemplate(template.templateId)"
          >
            <div class="option-info">
              <component
                :is="template.icon"
                v-if="template.icon"
                class="option-icon"
              />
              <h4>{{ template.label }}</h4>
            </div>
          </div>
        </template>
      </div>
    </div>
  </TUIDialog>
</template>

<script lang="ts" setup>
import { ref, computed, watch, h, defineComponent } from 'vue';
import { TUIErrorCode } from '@tencentcloud/tuiroom-engine-js';
import { useUIKit, TUIDialog, TUIToast, TOAST_TYPE, IconLayoutTemplate } from '@tencentcloud/uikit-base-component-vue3';
import { useLiveListState, useCoHostState, CoHostStatus } from 'tuikit-atomicx-vue3';

/**
 * 直播间麦位排版模板
 */
enum TUISeatLayoutTemplate {
  LandscapeDynamic_1v3 = 200,
  PortraitDynamic_Grid9 = 600,
  PortraitDynamic_1v6 = 601,
  PortraitFixed_Grid9 = 800,
  PortraitFixed_1v6 = 801,
  PortraitFixed_6v6 = 802,
}

const createSvgIcon = (pathD: string) => defineComponent({
  render: () => h('svg', { xmlns: 'http://www.w3.org/2000/svg', viewBox: '0 0 24 24', fill: 'currentColor', width: '24', height: '24' }, [h('path', { d: pathD })])
});

const Dynamic1v6 = createSvgIcon('M3 3h7v7H3V3zm11 0h7v4h-7V3zm0 6h7v4h-7V9zm0 6h7v6h-7v-6zM3 12h7v9H3v-9z');
const DynamicGrid9 = createSvgIcon('M3 3h5v5H3V3zm7 0h4v5h-4V3zm6 0h5v5h-5V3zM3 10h5v4H3v-4zm7 0h4v4h-4v-4zm6 0h5v4h-5v-4zM3 16h5v5H3v-5zm7 0h4v5h-4v-5zm6 0h5v5h-5v-5z');
const Fixed1v6 = createSvgIcon('M2 2h9v9H2V2zm11 0h9v4h-9V2zm0 5h9v4h-9V7zm0 5h9v4h-9v-4zm0 5h9v5h-9v-5zM2 13h9v9H2v-9z');
const FixedGrid9 = createSvgIcon('M2 2h6v6H2V2zm7 0h6v6H9V2zm7 0h6v6h-6V2zM2 9h6v6H2V9zm7 0h6v6H9V9zm7 0h6v6h-6V9zM2 16h6v6H2v-6zm7 0h6v6H9v-6zm7 0h6v6h-6v-6z');
const HorizontalFloat = createSvgIcon('M2 4h20v12H2V4zm3 14h4v2H5v-2zm6 0h4v2h-4v-2zm6 0h4v2h-4v-2z');

const { t } = useUIKit();
const { currentLive, updateLiveInfo } = useLiveListState();
const { coHostStatus } = useCoHostState();
const disabled = computed(() => coHostStatus.value === CoHostStatus.Connected);

watch(
  () => currentLive.value?.liveId,
  (liveId) => {
    if (!liveId) {
      updateLiveInfo({ layoutTemplate: TUISeatLayoutTemplate.PortraitDynamic_Grid9 });
    }
  },
  { immediate: true },
);

const layoutSwitchVisible = ref(false);

const handleSwitchLayout = () => {
  if (disabled.value) {
    TUIToast({ type: TOAST_TYPE.ERROR, message: t('Layout switching is not available during co-hosting') });
    return;
  }
  layoutSwitchVisible.value = true;
};

const portraitLayoutOptions = computed(() => [
  {
    id: 'PortraitDynamic_Grid9',
    icon: DynamicGrid9,
    templateId: TUISeatLayoutTemplate.PortraitDynamic_Grid9,
    label: t('Dynamic Grid9 Layout'),
  },
  {
    id: 'PortraitFixed_1v6',
    icon: Fixed1v6,
    templateId: TUISeatLayoutTemplate.PortraitFixed_1v6,
    label: t('Fixed 1v6 Layout'),
  },
  {
    id: 'PortraitFixed_Grid9',
    icon: FixedGrid9,
    templateId: TUISeatLayoutTemplate.PortraitFixed_Grid9,
    label: t('Fixed Grid9 Layout'),
  },
  {
    id: 'PortraitDynamic_1v6',
    icon: Dynamic1v6,
    templateId: TUISeatLayoutTemplate.PortraitDynamic_1v6,
    label: t('Dynamic 1v6 Layout'),
  },
]);

const horizontalLayoutOptions = computed(() => [
  {
    id: 'LandscapeDynamic_1v3',
    icon: HorizontalFloat,
    templateId: TUISeatLayoutTemplate.LandscapeDynamic_1v3,
    label: t('Landscape Template'),
  },
]);

const layoutOptions = computed(() => {
  if (currentLive.value && currentLive.value?.layoutTemplate >= 200 && currentLive.value?.layoutTemplate <= 599) {
    return horizontalLayoutOptions.value;
  }
  return portraitLayoutOptions.value;
});

const selectedTemplate = ref<TUISeatLayoutTemplate | null>(currentLive.value?.layoutTemplate ?? null);

function selectTemplate(template: TUISeatLayoutTemplate) {
  selectedTemplate.value = template;
}

watch(() => currentLive.value?.layoutTemplate, (newVal) => {
  if (newVal) {
    selectedTemplate.value = newVal;
  }
});

async function handleConfirm() {
  if (selectedTemplate.value) {
    try {
      await updateLiveInfo({ layoutTemplate: selectedTemplate.value });
      layoutSwitchVisible.value = false;
    } catch (error: any) {
      let errorMessage = t('Layout switch failed');
      if (error.code === TUIErrorCode.ERR_FREQ_LIMIT) {
        errorMessage = t('Operation too frequent, please try again later');
      }
      TUIToast({ type: TOAST_TYPE.ERROR, message: errorMessage });
    }
  } else {
    layoutSwitchVisible.value = false;
  }
}

function handleCancel() {
  selectedTemplate.value = currentLive.value?.layoutTemplate ?? null;
  layoutSwitchVisible.value = false;
}
</script>

<style scoped>
.custom-icon-container { display: flex; flex-direction: column; align-items: center; justify-content: center; gap: 4px; width: 56px; height: 56px; cursor: pointer; color: var(--text-color-primary); border-radius: 12px; position: relative; } .custom-icon-container .custom-icon { display: inline-block; width: 24px; height: 24px; background: transparent; } .custom-icon-container .custom-text { font-size: 12px; font-weight: 400; } .custom-icon-container:not(.disabled):hover { box-shadow: 0 0 10px 0 var(--bg-color-mask); } .custom-icon-container:not(.disabled):hover .custom-icon { color: var(--text-color-link); } .custom-icon-container:not(.disabled):hover .custom-text { color: var(--text-color-link); } .custom-icon-container.disabled { cursor: not-allowed; opacity: 0.5; color: var(--text-color-tertiary); } .custom-icon-container.disabled .custom-icon { color: var(--text-color-tertiary); cursor: not-allowed; } .custom-icon-container.disabled .custom-text { color: var(--text-color-tertiary); } :deep(.layout-dialog) { padding: 24px; width: 480px; } :deep(.layout-dialog) .dialog-body { flex-wrap: wrap; } :deep(.layout-dialog) .dialog-footer { padding-top: 32px; } .layout-label { font-size: 14px; font-weight: 400; color: var(--text-color-primary, #ffffff); margin: 4px 0px 16px 0px; } .template-options { width: 100%; height: 100%; overflow: auto; } .template-options .options-grid { display: flex; flex-wrap: wrap; gap: 16px; justify-content: flex-start; } .template-options .options-grid .option-card { box-sizing: border-box; padding: 12px 13px; width: 208px; background: #3a3a3a; border: 2px solid transparent; border-radius: 12px; cursor: pointer; transition: all 0.2s ease; text-align: center; } .template-options .options-grid .option-card:hover { background: #4a4a4a; border-color: #5a5a5a; } .template-options .options-grid .option-card.active { border: 2px solid var(--text-color-link-hover, #2B6AD6); background: var(--list-color-focused, #243047); } .template-options .options-grid .option-card.active .option-info h4 { color: #ffffff; } .template-options .options-grid .option-card .option-info { display: flex; align-items: center; justify-content: flex-start; gap: 8px; } .template-options .options-grid .option-card .option-info .option-icon { width: 24px; height: 24px; } .template-options .options-grid .option-card .option-info h4 { margin: 0; font-size: 14px; font-weight: 600; color: #ffffff; transition: color 0.2s ease; }
</style>
```

## 自定义您的界面布局

`TUILiveKit` 支持灵活定制开播页与直播页的功能和样式，您可根据业务需求调整布局、隐藏 / 显示功能模块。

### 横竖屏推流设置

`TUILiveKit` 支持**横屏**和**竖屏**两种推流模式，您可根据直播场景选择合适的推流方向：
| **推流模式** | **适用场景** | **说明** |
| --- | --- | --- |
| **竖屏推流** | 秀场直播、电商带货、聊天互动 | 默认模式，适合移动端观看，画面比例为 9:16。 |
| **横屏推流** | 游戏直播、在线教育、会议直播 | 适合 PC 端观看，画面比例为 16:9。 |

> **注意：**
> 

> 横竖屏切换必须在**开播前**进行设置，直播过程中无法切换推流方向。
> 

#### 通过 UI 交互切换

在主播开播页的底部控制栏，点击**横屏 / 竖屏**按钮即可切换推流方向：
- 显示**竖屏**时，当前为**竖屏推流模式**。

- 显示**横屏**时，当前为**横屏推流模式**

#### 通过代码设置

您也可以通过调用 `updateLiveInfo` 方法，在代码中设置推流方向：
``` typescript
import { useLiveListState } from 'tuikit-atomicx-vue3';

const { updateLiveInfo } = useLiveListState();

// 切换为横屏模式（模板 ID: 200）
updateLiveInfo({ layoutTemplate: 200 });

// 切换为竖屏模式（模板 ID: 600）
updateLiveInfo({ layoutTemplate: 600 });
```

> **说明：**
> 
> - 横屏模式对应的布局模板 ID 范围为 200-599，默认使用 200（横屏浮动布局）。
> - 竖屏模式对应的布局模板 ID 范围为 600-899，默认使用 600（动态宫格布局）。
> - 切换横竖屏时，系统会自动切换到对应方向的默认布局模板。

### 直播布局模板选择

`TUILiveKit` 提供多种直播布局模板，用于控制主播与连麦嘉宾的画面排列方式。您可在主播开播页的**布局设置**选择合适样式：

#### 竖屏模式布局模板

竖屏模式下提供 **4 种布局模板**，适用于秀场直播、电商带货等场景：
| **名称** | **动态宫格布局** | **动态 1V6 布局** | **静态宫格布局** | **静态小窗布局** |
| --- | --- | --- | --- | --- |
| **模板 ID** | 600 | 601 | 800 | 801 |
| **描述** | **默认布局**，根据连麦人数动态调整宫格大小，画面自适应填充。 | 主播画面居中大窗显示，连麦嘉宾以**浮动小窗**形式环绕在主播周围。 | 固定 9 宫格布局，每个嘉宾占据一个**固定大小**的宫格位置。 | 主播画面全屏显示，连麦嘉宾以**固定小窗**形式显示在画面边缘。 |
| **适用场景** | 通用场景，连麦人数不固定。 | 主播为主、嘉宾为辅的互动场景。 | 多人连麦、语音聊天室等固定人数场景。 | 主播全屏展示、嘉宾辅助的场景。 |

#### 横屏模式布局模板

横屏模式下提供 **1 种布局模板**，适用于游戏直播、在线教育等场景：
| **名称** | **横屏浮动布局** |
| --- | --- |
| **模板 ID** | 200 |
| **描述** | 主播画面全屏显示，连麦嘉宾以**浮动小窗**形式显示在画面底部。 |
| **适用场景** | 游戏直播、屏幕分享、在线教育等需要横屏展示的场景。 |

#### 通过代码设置布局模板

您可以通过调用 `updateLiveInfo` 方法，在代码中设置布局模板：
``` typescript
import { useLiveListState } from 'tuikit-atomicx-vue3';

const { updateLiveInfo } = useLiveListState();

// 设置竖屏动态宫格布局
updateLiveInfo({ layoutTemplate: 600 });

// 设置竖屏动态 1v6 布局
updateLiveInfo({ layoutTemplate: 601 });

// 设置竖屏静态宫格布局
updateLiveInfo({ layoutTemplate: 800 });

// 设置竖屏静态 1v6 布局
updateLiveInfo({ layoutTemplate: 801 });

// 设置横屏浮动布局
updateLiveInfo({ layoutTemplate: 200 });
```

> **注意：**
> 
> - 布局模板可以在**开播前**和**直播中**进行切换。
> - 在主播 PK 连线期间，**无法切换**布局模板。
> - 切换横竖屏推流方向时，布局模板会自动切换为对应方向的默认模板。

## 自由定制

### 颜色主题及语言

通过配置 `App.vue` 中 `UIKitProvider` 的入参，修改主题及语言的默认值。
| **UIKitProvider 参数** | **可选值** | **默认值** |
| --- | --- | --- |
| theme | "light" \\| "dark" | "light" |
| language | "zh-CN" \\| "en-US" | "en-US" |

``` typescript
<UIKitProvider theme="light">
  <router-view />
</UIKitProvider>
 
<script setup lang="ts">
import { UIKitProvider } from '@tencentcloud/uikit-base-component-vue3';
```

### 按钮 Button 和图标 Icon

若您需要对按钮 Button 或图标 Icon 等其他控件进行新增或替换等 UI 定制，您可以通过如下方式实现，以`live-player.vue `文件中的按钮和图标为例，您可以参考下图找到对应按钮或图标的指定位置源码，对当前部分的控件进行**增加、删除、替换**等 UI 定制操作。

根据上述示例，我们同样支持您根据项目需求对**观众观看页面**进行 UI 定制的能力。除了页面 UI 布局调整，我们也支持您对**颜色主题、字体、圆角、按钮、图标、输入框、弹框等**内容进行**增加、删除、修改**等操作，满足您的 UI 定制需要。
| **类别** | **功能** | **描述** | **组件详细定制指引** |
| --- | --- | --- | --- |
| **素材管理** | 自定义素材管理区域展示 | **支持：** - **调整展示 Icon 的大小、颜色或对 Icon 进行替换。** | [媒体源配置面板](https://cloud.tencent.com/document/product/647/123838) |
| **在线观众** | 自定义观众信息展示 | **支持：** - **展示/隐藏观众等级。** - **观众信息字体、颜色 UI 自定义设置。** - **替换为您需要的 Icon 风格。** | [视频源编辑画板](https://cloud.tencent.com/document/product/647/123834) |
| **消息列表** | 自定义消息弹幕区域展示 | **支持：** - **展示/隐藏聊天输入区域。** - **支持 UI 定制聊天气泡风格、定制观众等级等内容。** | [聊天弹幕组件](https://cloud.tencent.com/document/product/647/123836) |

## 下一步

恭喜您，现在您已经成功集成了**主播开播页面 **。接下来，您可以实现**观众观看页**、**直播列表页**和 **UI 自定义**等内容，可参考下表：
| **功能** | **描述** | **集成指引** |
| --- | --- | --- |
| **观众观看** | 实现观众进入主播的直播间后观看直播，实现观众连麦 、直播间信息、在线观众、弹幕显示等功能。 | 观众观看 |
| **直播列表** | 展示直播列表界面和功能，包含直播列表，房间信息展示功能。 | 直播列表 |
| **UI 自定义** | 更详细的 UI 组件自定义指引。 | 概述 |

---

本文对 TUILiveKit Demo 中的**观看页面**进行了详细的介绍，您可以在已有项目中直接参考本文档集成我们开发好的观看页面，也可以根据您的需求按照文档中的内容对页面的样式，布局以及功能项进行深度的定制。

## 功能展示

观看页面提供默认行为和风格，但如果默认行为和样式不能完全满足您的需求，您也可以对 UI 进行自定义。图中显示的数字与特定功能列表中的类别相对应。其中主要包含直播**信息展示、视频直播区域、在线观众、音视频操作、直播时长、画面分辨率切换、全屏功能、聊天互动、消息列表等。**
- **直播视频播放**：高清流畅的直播体验。

- **弹幕互动**：实时弹幕交流。

- **观众列表**：查看在线观众信息。

- **全屏播放**：沉浸式观看体验。

- **H5 移动平台支持**：跨平台兼容。

   

## 快速接入

### 步骤1：环境配置及开通服务

在进行快速接入之前，请参考 准备工作 集成组件并实现登录。

### 步骤2：安装依赖

您可以选择以下任一方式安装依赖：

【npm】
``` bash
npm install tuikit-atomicx-vue3 @tencentcloud/uikit-base-component-vue3 --save
```

【pnpm】
``` bash
pnpm add tuikit-atomicx-vue3 @tencentcloud/uikit-base-component-vue3
```

【yarn】
``` bash
yarn add tuikit-atomicx-vue3 @tencentcloud/uikit-base-component-vue3
```

### 步骤3：观看页面接入

在您的项目下创建`live-player.vue`文件，可直接复制如下代码至您的项目中集成**观看页面**。

> **注意：**
> 

> 您可以直接复制如下代码至您的工程中集成示例工程，也可以访问 [观众观看](https://github.com/Tencent-RTC/TUILiveKit/blob/main/Web/web-vite-vue3/src/TUILiveKit/component/LivePlayer/LivePlayerPC.vue) 地址，查看更加详细的源码内容。
> 

``` typescript
<template>
  <UIKitProvider theme="dark">
    <div class="container">
      <!-- 直播核心区域 -->
      <section class="live">
        <header class="header">
          <IconArrowStrokeBack class="back-btn" size="20" />
          <Avatar :src="currentLive?.liveOwner.avatarUrl" :size="32" class="avatar" />
          <span class="user-name">{{ currentLive?.liveOwner.userName || currentLive?.liveOwner.userId }}</span>
        </header>
        <LiveCoreView class="player" />
      </section>

      <div class="sidebar">
        <!-- 在线观众列表 -->
        <section class="audience">
          <header class="section-header">
            <h3> 在线观众 <span>({{ audienceList.length }})</span></h3>
          </header>
          <LiveAudienceList class="list" />
        </section>

        <!-- 消息列表 & 消息输入框 -->
        <section class="barrage">
          <header class="section-header">
            <h3>消息列表</h3>
          </header>
          <BarrageList class="list" />
          <BarrageInput class="input" height="48px" />
        </section>
      </div>
    </div>
  </UIKitProvider>
</template>

<script setup lang="ts">
import { onMounted } from 'vue';
import { LiveAudienceList, BarrageList, BarrageInput, useLiveAudienceState, LiveCoreView, useLiveListState, Avatar, useLoginState } from 'tuikit-atomicx-vue3';
import { UIKitProvider, IconArrowStrokeBack } from '@tencentcloud/uikit-base-component-vue3';

const { audienceList } = useLiveAudienceState();
const { currentLive, joinLive } = useLiveListState();
const { login, setSelfInfo } = useLoginState();

const liveId = 'live_xxxx'  // 填入您要观看的直播间的ID

async function initLogin() {
  try {
    await login({
      sdkAppId: 0,     // SDKAppID, 可以参考步骤 1 获取
      userId: '',      // UserID, 可以参考步骤 1 获取
      userSig: '',     // userSig, 可以参考步骤 1 获取
    });
  } catch (error) {
    console.error('登录失败:', error);
  }
}

onMounted(async () => {
  await initLogin();
  await setSelfInfo({
    userName: '我的名字/昵称',    // 用户名
    avatarUrl: '',              // 头像 URL 地址
  });
  await joinLive({ liveId });
});

</script>

<style>html,body,#app{height:100%;width:100%;margin:0;padding:0;overflow:hidden}:global(body){font-size:15px;line-height:1.6;text-rendering:optimizeLegibility;}:global(*),:global(*::before),:global(*::after){box-sizing:border-box;margin:0;}.container{display:grid;grid-template-columns:1fr 320px;height:100%;width:100%;gap:16px;padding:16px;background:var(--bg-color-default);box-sizing:border-box;overflow:hidden;}.live{display:flex;flex-direction:column;background:var(--bg-color-operate);border-radius:12px;overflow:hidden;box-shadow:0 2px 8px var(--shadow-color);}.header{display:flex;align-items:center;gap:12px;padding:16px;border-bottom:1px solid var(--stroke-color-primary);}.back-btn{cursor:pointer;color:var(--text-color-tertiary);transition:color 0.2s;}.back-btn:hover{color:var(--text-color-link-hover);}.avatar{border:1px solid var(--uikit-color-white-7);}.user-name{color:var(--text-color-primary);font-weight:500;}.player{flex:1;background:var(--uikit-color-black-1);min-height:0;}.sidebar{display:flex;flex-direction:column;gap:16px;height:100%;overflow:hidden;}.audience{display:flex;flex-direction:column;background:var(--bg-color-operate);border-radius:12px;overflow:hidden;box-shadow:0 2px 8px var(--shadow-color);flex:1;min-height:0;}.barrage{display:flex;flex-direction:column;background:var(--bg-color-operate);border-radius:12px;overflow:hidden;box-shadow:0 2px 8px var(--shadow-color);flex:1;min-height:0;}.section-header{padding:16px;border-bottom:1px solid var(--stroke-color-primary);background:var(--bg-color-operate);}.section-header h3{margin:0;font-size:16px;font-weight:600;color:var(--text-color-primary);}.section-header span{font-weight:400;color:var(--text-color-secondary);font-size:14px;}.list{flex:1;min-height:0;overflow-y:auto;}.input{border-top:1px solid var(--stroke-color-primary);flex-shrink:0;height:48px;}@media (max-width:1200px){.container{grid-template-columns:1fr;grid-template-rows:60% 20% 20%;gap:12px;}.sidebar{gap:12px;}.audience,.barrage{min-height:200px;}}@media (max-width:768px){.container{padding:8px;gap:8px;grid-template-rows:50% 25% 25%;}.header,.section-header{padding:12px;}.sidebar{gap:8px;}}</style>
```

#### 核心 API 参数说明

##### setSelfInfo

设置用户信息。
| 参数 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| userName | String | 是 | 用户昵称，将在直播间及聊天区域显示。 |
| avatarUrl | String | 否 | 用户头像的 URL 地址。 |

### 步骤4：启动项目

打开终端，进入项目目录，执行以下命令启动项目后，您就可以观看直播了。

> **说明：**
> 

> 上述命令执行成功后，请在浏览器地址栏输入本地访问地址（您可以根据项目参考，例如` http://localhost:5173/live-player`，具体端口号可能因您的项目配置而有所不同），即可看到观看页面。
> 

``` bash
npm run dev
```

## 播放直播流

### 步骤1：开启一场直播
- **方式一（推荐）：**

   使用我们提供的 [在线开播网站](https://web.sdk.qcloud.com/trtc/livekit/pusher/index.html#/?fromMark=123004) ，开启一场直播来观看，开启后获取直播间 ID

- **方式二：**

   集成我们提供的 主播开播（Web 桌面浏览器），开启一场直播来观看，开启后获取直播间 ID。
   

   > **重要提示：**
   > 

   > 请使用不同的**用户 ID** 开播和观看，否则后登录的设备会强制先登录的设备下线（即**被踢下线**）。
   > 

### 步骤2：观看直播

参考上述快速接入 步骤 3 的示例代码，输入对应 `liveId` 后即可进入直播间观看直播，观看效果如下图所示：

### 步骤3：路由配置

由于涉及到直播列表(或首页)到直播间的跳转逻辑，您需要配置 Vue Router。在项目 **src** 目录下新建 **router **文件夹，并创建 **index.ts **文件。然后，在您的主文件（例如 **main.ts** 或 **index.ts**）中引入并使用路由。可参见 [GitHub 代码示例](https://github.com/Tencent-RTC/TUILiveKit/blob/main/Web/web-vite-vue3/src/main.ts)，如果需要直播列表，可参见文档 直播列表。

> **注意：**
> 

> 如下代码示例中的 `live-player.vue` 文件即代表 步骤3 中创建的示例文件。
> 

``` typescript
// src/router/index.ts
import { createRouter, createWebHistory } from 'vue-router';

const routes = [
  {
    path: '/live-player',
    component: () => import('../live-player.vue'),
  },
  // 如果需要直播列表功能，可添加如下路由，注意以下路径为您项目实际路径
  // {  
    //   path: '/live-list',  
    //   component: () => import('../live-list.vue'),  
  // },
];

const router = createRouter({
  history: createWebHistory(),
  routes,
});
export default router;

// src/main.ts
import { createApp } from 'vue';
import App from './App.vue';
import router from './router';

const app = createApp(App);
app.use(router);
app.mount('#app');
```

## 自由定制

### 颜色主题及语言

通过配置 `App.vue` 中 `UIKitProvider` 的入参，修改主题及语言的默认值。
| UIKitProvider 参数 | 可选值 | 默认值 |
| --- | --- | --- |
| theme | "light" \\| "dark" | "light" |
| language | "zh-CN" \\| "en-US" | - |

``` typescript
<UIKitProvider theme="light">
  <router-view />
</UIKitProvider>
 
<script setup lang="ts">
import { UIKitProvider } from '@tencentcloud/uikit-base-component-vue3';
```

### 按钮 Button 和图标 Icon

若您需要对按钮 Button 或图标 Icon 等其他控件进行新增或替换等 UI 定制，您可以通过如下方式实现，以`live-player.vue `文件中的按钮和图标为例，您可以参考下图找到对应按钮或图标的指定位置源码，对当前部分的控件进行**增加、删除、替换**等 UI 定制操作。

根据上述示例，我们同样支持您根据项目需求对**观众观看页面**进行 UI 定制的能力。除了页面 UI 布局调整，我们也支持您对**颜色主题、字体、圆角、按钮、图标、输入框、弹框等**内容进行**增加、删除、修改**等操作，满足您的 UI 定制需要。
| **类别** | **功能** | **描述** |
| --- | --- | --- |
| **素材管理** | 自定义素材管理区域展示 | 支持调整 Icon 的大小、颜色或对 Icon 进行替换。 |
| **直播工具** | 自定义直播工具信息展示 | 支持调整 Icon 的大小、颜色或对 Icon 进行替换。 |
| **在线观众** | 自定义观众信息展示 | **支持：** - 展示/隐藏观众等级。 - 观众信息字体、颜色 UI 自定义设置。 - 替换为您需要的 Icon 风格。 |
| **消息列表** | 自定义消息弹幕区域展示 | **支持：** - 展示/隐藏聊天输入区域。 - 支持 UI 定制聊天气泡风格、定制观众等级等内容。 |

## 常见问题

### 浏览器自动播放限制

出于用户体验考虑，现代浏览器对网页自动播放 (Autoplay) 功能实施了限制性策略：所有带声音的媒体内容必须经过用户主动交互（如点击或触摸）后才能播放。这项限制主要是为了防止网站在用户未明确同意的情况下突然播放音频，避免对用户造成干扰。大多数浏览器都不限制无声视频的自动播放，但是在低电量模式下的 iOS Safari 浏览器中以及开启了自定义自动播放限制的 iOS WKWebView 中（如 iOS 微信浏览器），无声视频的自动播放也会受到限制。

#### 自动播放失败表现

当用户对该站点的媒体互动指数 (MEI, Media Engagement Index) 未达到阈值时，企图自动播放有声视频会失败。在 SDK 默认情况下，当检测到自动播放失败时，会弹窗引导用户与页面产生交互（如点击**确认**按钮）。产生交互后，浏览器策略即被满足，有声视频即可正常播放。

#### 解决方案：自定义处理自动播放失败

如果您希望自定义自动播放失败时的交互体验（例如替换默认的弹窗 UI），可以通过监听 SDK 抛出的 `onAutoplayFailed` 回调来实现。以下是在 Vue3 项目中，通过监听事件并弹出自定义对话框的实现代码示例：
``` java
import TUIRoomEngine, { TUIRoomEvents } from '@tencentcloud/tuiroom-engine-js';
import { useUIKit, TUIMessageBox } from '@tencentcloud/uikit-base-component-vue3';
import { useRoomEngine } from 'tuikit-atomicx-vue3';

const roomEngine = useRoomEngine();

let isShowAutoPlayDialog = false;

export default function useCustomizedAutoPlayDialog() {
  const { t } = useUIKit();
  TUIRoomEngine.once('ready', () => {
    roomEngine.instance?.on(TUIRoomEvents.onAutoPlayFailed, () => {
      if (!isShowAutoPlayDialog) {
        isShowAutoPlayDialog = true;
        TUIMessageBox.alert({
          title: t('RoomCommon.Attention'),
          content: t('RoomNotifications.AudioPlaybackFailed'),
          showClose: false,
          modal: false,
          confirmText: t('Confirm'),
          callback: () => {
            isShowAutoPlayDialog = false;
          },
        });
      }
    });
  });
}

export { useCustomizedAutoPlayDialog };
```

> **说明：**
> 

> 您需要安装对应的 `@tencentcloud/tuiroom-engine-js。`
> 

## 下一步

恭喜您，现在您已经成功集成了观众观看功能。接下来，您可以继续接入**直播列表、UI 自定义**和**监播**等功能：
| **功能** | **描述** | **集成指引** |
| --- | --- | --- |
| **直播列表** | 展示直播列表界面和功能，包含直播列表和房间信息展示功能。 | 直播列表（Web Vue3） |
| **UI 自定义** | 更详细的 UI 组件自定义指引。 | 概述 |
| **Web 监播** | 运营平台，支持直播间管控。 | Web 监播页（Web Vue3） |

---

本文对 TUILiveKit Demo 中的**观看页面**进行了详细的介绍，您可以在已有项目中直接参考本文档集成我们开发好的观看页面，也可以根据您的需求按照文档中的内容对页面的样式，布局以及功能项进行深度的定制。

## 功能展示

观看页面提供默认行为和风格，但如果默认行为和样式不能完全满足您的需求，您也可以对 UI 进行自定义。图中显示的数字与特定功能列表中的类别相对应。其中主要包含直播**信息展示、视频直播区域、在线观众、音视频操作、直播时长、画面分辨率切换、全屏功能、聊天互动、消息列表等。**
- **直播视频播放**：高清流畅的直播体验。

- **弹幕互动**：实时弹幕交流。

- **观众列表**：查看在线观众信息。

- **全屏播放**：沉浸式观看体验。

- **H5 移动平台支持**：跨平台兼容。

   

## 快速接入

### 步骤1：环境配置及开通服务

在进行快速接入之前，请参考 准备工作 集成组件并实现登录。

### 步骤2：安装依赖

您可以选择以下任一方式安装依赖：

【npm】
``` bash
npm install tuikit-atomicx-vue3 @tencentcloud/uikit-base-component-vue3 --save
```

【pnpm】
``` bash
pnpm add tuikit-atomicx-vue3 @tencentcloud/uikit-base-component-vue3
```

【yarn】
``` bash
yarn add tuikit-atomicx-vue3 @tencentcloud/uikit-base-component-vue3
```

### 步骤3：观看页面接入

在您的项目下创建 **live-player.vue **文件，可直接复制如下代码至您的项目中集成**观看页面**。

> **注意：**
> 

> 您可以直接复制如下代码至您的工程中集成示例工程，也可以访问 [观众观看](https://github.com/Tencent-RTC/TUILiveKit/blob/main/Web/web-vite-vue3/src/TUILiveKit/component/LivePlayer/LivePlayerH5.vue) 地址，查看更加详细的源码内容。
> 

``` typescript
<template>
  <UIKitProvider theme="dark">
    <div class="container">
      <!-- 直播核心区域 -->
      <section class="live">
        <header class="header">
          <IconArrowStrokeBack class="back-btn" size="20" />
          <Avatar :src="currentLive?.liveOwner.avatarUrl" :size="32" class="avatar" />
          <span class="user-name">{{ currentLive?.liveOwner.userName || currentLive?.liveOwner.userId }}</span>
        </header>
        <LiveCoreView class="player" />
      </section>

      <div class="sidebar">
        <!-- 在线观众列表 -->
        <section class="audience">
          <header class="section-header">
            <h3> 在线观众 <span>({{ audienceList.length }})</span></h3>
          </header>
          <LiveAudienceList class="list" />
        </section>

        <!-- 消息列表 & 消息输入框 -->
        <section class="barrage">
          <header class="section-header">
            <h3>消息列表</h3>
          </header>
          <BarrageList class="list" />
          <BarrageInput class="input" height="48px" />
        </section>
      </div>
    </div>
  </UIKitProvider>
</template>

<script setup lang="ts">
import { onMounted } from 'vue';
import { LiveAudienceList, BarrageList, BarrageInput, useLiveAudienceState, LiveCoreView, useLiveListState, Avatar, useLoginState } from 'tuikit-atomicx-vue3';
import { UIKitProvider, IconArrowStrokeBack } from '@tencentcloud/uikit-base-component-vue3';

const { audienceList } = useLiveAudienceState();
const { currentLive } = useLiveListState();
const { login, setSelfInfo } = useLoginState();

const liveId = 'live_xxxx'  // 填入您要观看的直播间的ID

async function initLogin() {
  try {
    await login({
      sdkAppId: 0,     // SDKAppID, 可以参考步骤 1 获取
      userId: '',      // UserID, 可以参考步骤 1 获取
      userSig: '',     // userSig, 可以参考步骤 1 获取
    });
  } catch (error) {
    console.error('登录失败:', error);
  }
}

onMounted(async () => {
  await initLogin();
  await setSelfInfo({
    userName: '我的名字/昵称',    // 用户名
    avatarUrl: '',              // 头像 URL 地址
  });
  await joinLive({ liveId });
});

</script>

<style>html,body,#app{height:100%;width:100%;margin:0;padding:0;overflow:hidden}:global(body){font-size:15px;line-height:1.6;text-rendering:optimizeLegibility;}:global(*),:global(*::before),:global(*::after){box-sizing:border-box;margin:0;}.container{display:grid;grid-template-columns:1fr 320px;height:100%;width:100%;gap:16px;padding:16px;background:var(--bg-color-default);box-sizing:border-box;overflow:hidden;}.live{display:flex;flex-direction:column;background:var(--bg-color-operate);border-radius:12px;overflow:hidden;box-shadow:0 2px 8px var(--shadow-color);}.header{display:flex;align-items:center;gap:12px;padding:16px;border-bottom:1px solid var(--stroke-color-primary);}.back-btn{cursor:pointer;color:var(--text-color-tertiary);transition:color 0.2s;}.back-btn:hover{color:var(--text-color-link-hover);}.avatar{border:1px solid var(--uikit-color-white-7);}.user-name{color:var(--text-color-primary);font-weight:500;}.player{flex:1;background:var(--uikit-color-black-1);min-height:0;}.sidebar{display:flex;flex-direction:column;gap:16px;height:100%;overflow:hidden;}.audience{display:flex;flex-direction:column;background:var(--bg-color-operate);border-radius:12px;overflow:hidden;box-shadow:0 2px 8px var(--shadow-color);flex:1;min-height:0;}.barrage{display:flex;flex-direction:column;background:var(--bg-color-operate);border-radius:12px;overflow:hidden;box-shadow:0 2px 8px var(--shadow-color);flex:1;min-height:0;}.section-header{padding:16px;border-bottom:1px solid var(--stroke-color-primary);background:var(--bg-color-operate);}.section-header h3{margin:0;font-size:16px;font-weight:600;color:var(--text-color-primary);}.section-header span{font-weight:400;color:var(--text-color-secondary);font-size:14px;}.list{flex:1;min-height:0;overflow-y:auto;}.input{border-top:1px solid var(--stroke-color-primary);flex-shrink:0;height:48px;}@media (max-width:1200px){.container{grid-template-columns:1fr;grid-template-rows:60% 20% 20%;gap:12px;}.sidebar{gap:12px;}.audience,.barrage{min-height:200px;}}@media (max-width:768px){.container{padding:8px;gap:8px;grid-template-rows:50% 25% 25%;}.header,.section-header{padding:12px;}.sidebar{gap:8px;}}</style>
```

#### 核心 API 参数说明

##### setSelfInfo

设置用户信息。
| 参数 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| userName | String | 是 | 用户昵称，将在直播间及聊天区域显示。 |
| avatarUrl | String | 否 | 用户头像的 URL 地址。 |

### 步骤4：启动项目

打开终端，进入项目目录，执行以下命令启动项目后，您就可以观看直播了。

> **说明：**
> 

> 上述命令执行成功后，请在浏览器地址栏输入本地访问地址（您可以根据项目配置参考，例如` http://localhost:5173/live-player`，具体端口号可能因您的项目配置而有所不同），即可看到观看页面。
> 

``` bash
npm run dev
```

## 播放直播流

### 步骤1：开启一场直播
- **方式一（推荐）：**

   使用我们提供的 [在线开播网站](https://web.sdk.qcloud.com/trtc/livekit/pusher/index.html#/?fromMark=123471)，开启一场直播来观看，开启后获取直播间 ID

- **方式二：**

   集成我们提供的 主播开播（Web 桌面浏览器），开启一场直播来观看，开启后获取直播间 ID。
   

   > **重要提示：**
   > 

   > 请使用不同的**用户 ID** 开播和观看，否则后登录的设备会强制先登录的设备下线（即“被踢下线”）。
   > 

### 步骤2：观看直播

参考上述快速接入中的 步骤 3 的示例代码，输入对应 `liveId` 后即可进入直播间观看直播：

> **说明：**
> 

> 另外，若您需要修改个人信息，请参考 步骤 3 示例代码中的 `setSelfInfo` 进行个人信息的设置。
> 

### 步骤3：路由配置

由于涉及到直播列表(或首页)到直播间的跳转逻辑，您需要配置 Vue Router。在项目 **src** 目录下新建 **router **文件夹，并创建 **index.ts **文件。然后，在您的主文件（例如 **main.ts** 或 **index.ts**）中引入并使用路由。可参见 [GitHub 上的代码示例](https://github.com/Tencent-RTC/TUILiveKit/blob/main/Web/web-vite-vue3/src/main.ts)，如果需要直播列表，可参见文档 直播列表。

> **注意：**
> 

> 如下代码示例中的 `live-player.vue` 文件即代表 步骤3 中创建的示例文件。
> 

``` typescript
// src/router/index.ts
import { createRouter, createWebHistory } from 'vue-router';

const routes = [
  {
    path: '/live-player',
    component: () => import('../live-player.vue'),
  },
  // 如果需要直播列表功能，可添加如下路由，注意以下路径为您项目实际路径
  // {  
    //   path: '/live-list',  
    //   component: () => import('../live-list.vue'),  
  // },
];

const router = createRouter({
  history: createWebHistory(),
  routes,
});
export default router;

// src/main.ts
import { createApp } from 'vue';
import App from './App.vue';
import router from './router';

const app = createApp(App);
app.use(router);
app.mount('#app');
```

## 自由定制

### 颜色主题及语言

通过配置 `App.vue` 中 `UIKitProvider` 的入参，修改主题及语言的默认值。
| UIKitProvider 参数 | 可选值 | 默认值 |
| --- | --- | --- |
| theme | "light" \\| "dark" | "light" |
| language | "zh-CN" \\| "en-US" | - |

``` typescript
<UIKitProvider theme="light">
  <router-view />
</UIKitProvider>
 
<script setup lang="ts">
import { UIKitProvider } from '@tencentcloud/uikit-base-component-vue3';
```

### 按钮 Button 和图标 Icon

若您需要对按钮 Button 或图标 Icon 等其他控件进行新增或替换等 UI 定制，您可以通过如下方式实现，以`live-player.vue `文件中的按钮和图标为例，您可以参考下图找到对应按钮或图标的指定位置源码，对当前部分的控件进行**增加、删除、替换**等 UI 定制操作。

根据上述示例，我们同样支持您根据项目需求对**观众观看页面**进行 UI 定制的能力。除了页面 UI 布局调整，我们也支持您对**颜色主题、字体、圆角、按钮、图标、输入框、弹框等**内容进行**增加、删除、修改**等操作，满足您的 UI 定制需要。
| **类别** | **功能** | **描述** |
| --- | --- | --- |
| **素材管理** | 自定义素材管理区域展示 | 支持调整 Icon 的大小、颜色或对 Icon 进行替换。 |
| **直播工具** | 自定义直播工具信息展示 | 支持调整 Icon 的大小、颜色或对 Icon 进行替换。 |
| **在线观众** | 自定义观众信息展示 | **支持：** - 展示/隐藏观众等级。 - 观众信息字体、颜色 UI 自定义设置。 - 替换为您需要的 Icon 风格。 |
| **消息列表** | 自定义消息弹幕区域展示 | **支持：** - 展示/隐藏聊天输入区域。 - 支持 UI 定制聊天气泡风格、定制观众等级等内容。 |

## 常见问题

### 浏览器自动播放限制

出于用户体验考虑，现代浏览器对网页自动播放（autoplay）功能实施了限制性策略：所有带声音的媒体内容必须经过用户主动交互（例如点击或触摸）后才能播放。这项限制主要是为了防止网站在用户未明确同意的情况下突然播放音频，避免对用户造成干扰。大多数浏览器都不限制无声视频的自动播放，但是在低电量模式下的 iOS Safari 浏览器中以及开启了自定义自动播放限制的 iOS WKWebView 中（例如 iOS 微信浏览器），无声视频的自动播放也会受到限制。

#### 自动播放失败表现

当用户对该站点的媒体互动指数（MEI, Media Engagement Index）未达到阈值时，企图自动播放有声视频会失败。在 SDK 默认情况下，当检测到自动播放失败时，会弹窗引导用户与页面产生交互（例如点击**确认**按钮）。产生交互后，浏览器策略即被满足，有声视频即可正常播放。

#### 解决方案：自定义处理自动播放失败

如果您希望自定义自动播放失败时的交互体验（例如替换默认的弹窗 UI），可以通过监听 SDK 抛出的 `onAutoplayFailed` 回调来实现。以下是在 Vue3 项目中，通过监听事件并弹出自定义对话框的实现代码示例：
``` java
import TUIRoomEngine, { TUIRoomEvents } from '@tencentcloud/tuiroom-engine-js';
import { useUIKit, TUIMessageBox } from '@tencentcloud/uikit-base-component-vue3';
import { useRoomEngine } from 'tuikit-atomicx-vue3';

const roomEngine = useRoomEngine();

let isShowAutoPlayDialog = false;

export default function useCustomizedAutoPlayDialog() {
  const { t } = useUIKit();
  TUIRoomEngine.once('ready', () => {
    roomEngine.instance?.on(TUIRoomEvents.onAutoPlayFailed, () => {
      if (!isShowAutoPlayDialog) {
        isShowAutoPlayDialog = true;
        TUIMessageBox.alert({
          title: t('RoomCommon.Attention'),
          content: t('RoomNotifications.AudioPlaybackFailed'),
          showClose: false,
          modal: false,
          confirmText: t('Confirm'),
          callback: () => {
            isShowAutoPlayDialog = false;
          },
        });
      }
    });
  });
}

export { useCustomizedAutoPlayDialog };
```

> **说明：**
> 

> 您需要安装对应的 `@tencentcloud/tuiroom-engine-js。`
> 

## 下一步

恭喜您，现在您已经成功集成了观众观看。接下来，您可以继续接入 **直播列表、UI 自定义**和**监播**等功能：
| **功能** | **描述** | **集成指引** |
| --- | --- | --- |
| 直播列表 | 展示直播列表界面和功能，包含直播列表和房间信息展示功能。 | 直播列表（Web Vue3） |
| UI 自定义 | 更详细的 UI 组件自定义指引。 | 概述 |
| Web 监播 | 运营平台，支持直播间管控。 | Web 监播页（Web Vue3） |
