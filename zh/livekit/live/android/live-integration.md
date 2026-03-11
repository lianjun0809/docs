> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

本文档将帮助您使用 **AtomicXCore SDK**的核心组件 [LiveCoreView](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.view/-live-core-view/index.html)，快速构建一个包含主播开播和观众观看功能的基础直播 App。

### **核心功能**

**LiveCoreView** 是一个专为直播场景设计的轻量级 `View` 组件，是您构建直播场景的核心，它封装了所有复杂的底层直播技术（如推拉流、连麦、音视频渲染）。您可以将 LiveCoreView 作为直播画面的"画布"，专注于上层 UI 与交互的开发。

通过下方的视图层级示意图，您可以直观了解 **LiveCoreView** 在直播界面中的位置和作用：

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032603567/8854e196ae4711f096c2525400454e06.png)


## 准备工作

### 步骤1：开通服务

请参见 [开通服务](https://write.woa.com/document/141302177829593088)，获取体验版或付费版 SDK。

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
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >说明</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >sdkAppId</td>

<td rowspan="1" colSpan="1" >Int</td>

<td rowspan="1" colSpan="1" >从 [控制台](https://console.cloud.tencent.com/trtc) 获取，通常是以 `140` 或 `160` 开头的 10 位整数。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userID</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >当前用户的唯一 ID，仅包含英文字母、数字、连字符和下划线。为避免多端登录冲突，**请勿使用**`1`、`123`**等简单 ID**。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userSig</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >用于腾讯云鉴权的票据。请注意：<br>- 开发环境：您可以采用本地 `GenerateTestUserSig.genTestSig` 函数生成 userSig 或者 通过 [UserSig 辅助工具](https://console.cloud.tencent.com/im/tool-usersig) 生成临时的 UserSig。<br>- 生产环境：为了防止密钥泄露，请务必采用服务端生成 UserSig 的方式。详细信息请参考 [服务端生成 UserSig](https://cloud.tencent.com/document/product/647/17275)。<br>更多信息请参见 [如何计算及使用 UserSig](https://cloud.tencent.com/document/product/647/17275)。</td>
</tr>
</table>


## 搭建基础直播间

### 步骤1：实现主播视频开播

主播开播流程如下，您只需执行以下几步操作，即可快速搭建主播视频直播。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032603567/e302f6e5ae4711f0b08552540044a08e.png)


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

<table>
<tr>
<td rowspan="1" colSpan="1" >**参数名**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**属性**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`liveID`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >必填</td>

<td rowspan="1" colSpan="1" >直播间的唯一标识符。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`liveName`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >直播间的标题。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`notice`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >直播间的公告信息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`isMessageDisable`</td>

<td rowspan="1" colSpan="1" >`Boolean`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >是否禁言（`true`：是，`false`：否）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`isPublicVisible`</td>

<td rowspan="1" colSpan="1" >`Boolean`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >是否公开可见（`true`：是，`false`：否）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`isSeatEnabled`</td>

<td rowspan="1" colSpan="1" >`Boolean`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >是否启用麦位功能（`true`：是，`false`：否）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`keepOwnerOnSeat`</td>

<td rowspan="1" colSpan="1" >`Boolean`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >是否保持房主在麦位上。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`maxSeatCount`</td>

<td rowspan="1" colSpan="1" >`Int`</td>

<td rowspan="1" colSpan="1" >必填</td>

<td rowspan="1" colSpan="1" >最大麦位数量。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`seatMode`</td>

<td rowspan="1" colSpan="1" >[TakeSeatMode](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-take-seat-mode/index.html)</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >上麦模式（`FREE`：自由上麦，`APPLY`：申请上麦）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`seatLayoutTemplateID`</td>

<td rowspan="1" colSpan="1" >`Int`</td>

<td rowspan="1" colSpan="1" >必填</td>

<td rowspan="1" colSpan="1" >麦位布局模板 `ID`。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`coverURL`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >直播间的封面图片地址。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`backgroundURL`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >直播间的背景图片地址。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`categoryList`</td>

<td rowspan="1" colSpan="1" >`List<Int>`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >直播间的分类标签列表。</td>
</tr>

<tr>
<td rowspan="4" colSpan="1" >`activityStatus`</td>

<td rowspan="4" colSpan="1" >`Int`</td>

<td rowspan="4" colSpan="1" >选填</td>

<td rowspan="4" colSpan="1" >直播活动状态。</td>
</tr>

<tr></tr>

<tr></tr>

<tr></tr>

<tr>
<td rowspan="2" colSpan="1" >`isGiftEnabled`</td>

<td rowspan="2" colSpan="1" >`Boolean`</td>

<td rowspan="2" colSpan="1" >选填</td>

<td rowspan="2" colSpan="1" >是否启用礼物功能（`true`：是，`false`：否）。</td>
</tr>

<tr></tr>
</table>

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

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032603567/14058edaae4811f08bcc5254007c27c5.png)


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

集成 **LiveCoreView** 后，您将得到一个纯净的视频渲染视图，它已具备完整的直播业务能力，但没有任何交互 UI。您可以参考下一章节 [丰富直播场景](https://write.woa.com/#789ad452-eaf1-433f-905d-fcb2945c1505) 来完善直播场景。
<table>
<tr>
<td rowspan="1" colSpan="1" ></td>

<td rowspan="1" colSpan="1" >**动态宫格布局**</td>

<td rowspan="1" colSpan="1" >**浮动小窗布局**</td>

<td rowspan="1" colSpan="1" >**固定宫格布局**</td>

<td rowspan="1" colSpan="1" >**固定小窗布局**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**模板 ID**</td>

<td rowspan="1" colSpan="1" >600</td>

<td rowspan="1" colSpan="1" >601</td>

<td rowspan="1" colSpan="1" >800</td>

<td rowspan="1" colSpan="1" >801</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**描述**</td>

<td rowspan="1" colSpan="1" >默认布局，可根据连麦人数动态调整宫格大小。</td>

<td rowspan="1" colSpan="1" >连麦嘉宾以浮动小窗形式显示。</td>

<td rowspan="1" colSpan="1" >连麦人数固定，每个嘉宾占据一个固定宫格。</td>

<td rowspan="1" colSpan="1" >连麦人数固定，嘉宾以固定小窗形式显示。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**运行效果**</td>

<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027182498/394f3851a5b511f09936525400e889b2.png)</td>

<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027182498/395e0e3da5b511f0930a5254007c27c5.png)</td>

<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027182498/39427c02a5b511f0b1565254001c06ec.png)</td>

<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027182498/3942f453a5b511f091df5254005ef0f7.png)</td>
</tr>
</table>


## 丰富直播场景

当您完成了基础的直播功能后，您可以参考以下功能指南来为直播添加丰富的互动玩法。
<table>
<tr>
<td rowspan="1" colSpan="1" >**直播功能**</td>

<td rowspan="1" colSpan="1" >**功能介绍**</td>

<td rowspan="1" colSpan="1" >**功能 Stores**</td>

<td rowspan="1" colSpan="1" >**实现指南**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**实现观众音视频连线**</td>

<td rowspan="1" colSpan="1" >观众申请上麦，与主播进行实时视频互动。</td>

<td rowspan="1" colSpan="1" >[CoGuestStore](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-co-guest-store/index.html)</td>

<td rowspan="1" colSpan="1" >[观众连线](https://write.woa.com/document/191126685644365824)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**实现主播跨房连线 PK**</td>

<td rowspan="1" colSpan="1" >两个不同房间的主播进行连线，实现互动或 PK。</td>

<td rowspan="1" colSpan="1" >[CoHostStore](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-co-host-store/index.html)<br>[BattleStore](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-battle-store/index.html)</td>

<td rowspan="1" colSpan="1" >[主播连线 & PK](https://write.woa.com/document/191126527339847680)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**添加弹幕聊天功能**</td>

<td rowspan="1" colSpan="1" >观众可以在直播间发送和接收实时文字消息。</td>

<td rowspan="1" colSpan="1" >[BarrageStore](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.barrage/-barrage-store/index.html)</td>

<td rowspan="1" colSpan="1" >[实现弹幕功能](https://write.woa.com/document/191126771034308608)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**构建礼物赠送系统**</td>

<td rowspan="1" colSpan="1" >观众可以向主播赠送虚拟礼物，增加互动和趣味性。</td>

<td rowspan="1" colSpan="1" >[GiftStore](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.gift/-gift-store/index.html)</td>

<td rowspan="1" colSpan="1" >[实现礼物功能](https://write.woa.com/document/191126992871682048)</td>
</tr>
</table>


## API 文档
<table>
<tr>
<td rowspan="1" colSpan="1" >**Store/Component**</td>

<td rowspan="1" colSpan="1" >**功能描述**</td>

<td rowspan="1" colSpan="1" >**API 文档**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**LiveCoreView**</td>

<td rowspan="1" colSpan="1" >直播视频流展示与交互的核心视图组件：负责视频流渲染和视图挂件处理，支持主播直播、观众连麦、主播连线等场景。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.view/-live-core-view/index.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**LiveListStore**</td>

<td rowspan="1" colSpan="1" >直播间全生命周期管理：创建 / 加入 / 离开 / 销毁房间，查询房间列表，修改直播信息（名称、公告等），监听直播状态（如被踢出、结束）。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-live-list-store/index.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**DeviceStore**</td>

<td rowspan="1" colSpan="1" >音视频设备控制：麦克风（开关 / 音量）、摄像头（开关 / 切换 / 画质）、屏幕共享，设备状态实时监听。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.device/-device-store/index.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**CoGuestStore**</td>

<td rowspan="1" colSpan="1" >观众连麦管理：连麦申请 / 邀请 / 同意 / 拒绝，连麦成员权限控制（麦克风 / 摄像头），状态同步。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-co-guest-store/index.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**CoHostStore**</td>

<td rowspan="1" colSpan="1" >主播跨房连线：支持多布局模板（动态网格等），发起 / 接受 / 拒绝连线，连麦主播互动管理。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-co-host-store/index.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**BattleStore**</td>

<td rowspan="1" colSpan="1" >主播 PK 对战：发起 PK（配置时长 / 对手），管理 PK 状态（开始 / 结束），同步分数，监听对战结果。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-battle-store/index.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**GiftStore**</td>

<td rowspan="1" colSpan="1" >礼物互动：获取礼物列表，发送 / 接收礼物，监听礼物事件（含发送者、礼物详情）。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.gift/-gift-store/index.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**BarrageStore**</td>

<td rowspan="1" colSpan="1" >弹幕功能：发送文本 / 自定义弹幕，维护弹幕列表，实时监听弹幕状态。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.barrage/-barrage-store/index.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**LikeStore**</td>

<td rowspan="1" colSpan="1" >点赞互动：发送点赞，监听点赞事件，同步总点赞数。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-like-store/index.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**LiveAudienceStore**</td>

<td rowspan="1" colSpan="1" >观众管理：获取实时观众列表（ID / 名称 / 头像），统计观众数量，监听观众进出事件。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-live-audience-store/index.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**AudioEffectStore**</td>

<td rowspan="1" colSpan="1" >音频特效：变声（童声 / 男声）、混响（KTV 等）、耳返调节，实时切换特效。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.device/-audio-effect-store/index.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**BaseBeautyStore**</td>

<td rowspan="1" colSpan="1" >基础美颜：调节磨皮 / 美白 / 红润（0-100 级），重置美颜状态，同步效果参数。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.device/-base-beauty-store/index.html)</td>
</tr>
</table>


## 常见问题

### 主播调用 createLive 或 观众调用 joinLive 后为什么画面是黑的，没有视频画面？
- **检查 setLiveID**：请确保在调用开播或观看接口前，已经为 LiveCoreView 实例设置了正确的 liveID。

- **检查设备权限**：请确保 App 已获得摄像头和麦克风的系统使用权限。

- **检查主播端**：主播端是否正常调用 `DeviceStore.shared().openLocalCamera(true)` 打开了摄像头。

- **检查网络**：请检查设备网络连接是否正常。


### 主播端打开摄像头后，开播后可以看到本地视频预览画面，开播前视频预览是黑屏？
- **检查主播端**：请检查主播推流视图`LiveCoreView` 的 `viewType`是否配置为`PUSH_VIEW`。

- **检查观众端**：请检查观众拉流视图`LiveCoreView` 的 `viewType`是否配置为 `PLAY_VIEW`。
