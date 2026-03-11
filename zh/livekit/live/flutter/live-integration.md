> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

本文档将帮助您使用 **AtomicXCore SDK** 的核心组件 [LiveCoreWidget](https://tencent-rtc.github.io/TUIKit_Flutter/api_view_live_live_core_widget/api_view_live_live_core_widget-library.html)，快速构建一个包含主播开播和观众观看功能的基础直播 App。

## 核心功能

**LiveCoreWidget** 是一个专为直播场景设计的轻量级 Widget 组件，是您构建直播场景的核心，它封装了所有复杂的底层直播技术（例如推拉流、连麦、音视频渲染）。您可以将 LiveCoreWidget 作为直播画面的"画布"，专注于上层 UI 与交互的开发。

通过下方的视图层级示意图，您可以直观了解 **LiveCoreWidget** 在直播界面中的位置和作用：

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032457995/ac234e1ee0a811f095ab5254001c06ec.png)


## 准备工作

### 步骤1：开通服务

请参见 [开通服务](https://write.woa.com/document/141302177829593088)，获取体验版或付费版 SDK。

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

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032457995/8b552502e52811f095b0525400e889b2.png)



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
<table>
<tr>
<td rowspan="1" colSpan="1" >**参数**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**说明**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`sdkAppID`</td>

<td rowspan="1" colSpan="1" >`int`</td>

<td rowspan="1" colSpan="1" >从 [控制台](https://console.cloud.tencent.com/trtc) 获取，通常是以 `140` 或 `160` 开头的 10 位整数。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`userID`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >当前用户的唯一 ID，仅包含英文字母、数字、连字符和下划线。为避免多端登录冲突，**请勿使用**`1`、`123`**等简单 ID**。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`userSig`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >用于腾讯云鉴权的票据。请注意：<br>- 开发环境：您可以采用本地 `GenerateTestUserSig.genTestSig` 函数生成 userSig 或者通过 [UserSig 辅助工具](https://console.cloud.tencent.com/im/tool-usersig) 生成临时的 UserSig。<br>- 生产环境：为了防止密钥泄露，请务必采用服务端生成 UserSig 的方式。详细信息请参考 [服务端生成 UserSig](https://cloud.tencent.com/document/product/647/17275)。<br>更多信息请参见 [如何计算及使用 UserSig](https://cloud.tencent.com/document/product/647/17275)。</td>
</tr>
</table>


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

<td rowspan="1" colSpan="1" >`bool`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >是否禁言（`true`：是，`false`：否）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`isPublicVisible`</td>

<td rowspan="1" colSpan="1" >`bool`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >是否公开可见（`true`：是，`false`：否）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`isSeatEnabled`</td>

<td rowspan="1" colSpan="1" >`bool`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >是否启用麦位功能（`true`：是，`false`：否）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`keepOwnerOnSeat`</td>

<td rowspan="1" colSpan="1" >`bool`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >是否保持房主在麦位上。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`maxSeatCount`</td>

<td rowspan="1" colSpan="1" >`int`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >最大麦位数量。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`seatMode`</td>

<td rowspan="1" colSpan="1" >`TakeSeatMode`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >上麦模式（`TakeSeatMode.free`：自由上麦，`TakeSeatMode.apply`：申请上麦）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`seatLayoutTemplateID`</td>

<td rowspan="1" colSpan="1" >`int`</td>

<td rowspan="1" colSpan="1" >必填</td>

<td rowspan="1" colSpan="1" >麦位布局模板 ID。</td>
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

<td rowspan="1" colSpan="1" >`List<int>`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >直播间的分类标签列表。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`activityStatus`</td>

<td rowspan="1" colSpan="1" >`int`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >直播活动状态。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`isGiftEnabled`</td>

<td rowspan="1" colSpan="1" >`bool`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >是否启用礼物功能（`true`：是，`false`：否）。</td>
</tr>
</table>

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

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032457995/116894aee55e11f095b0525400e889b2.png)


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

集成 **LiveCoreWidget** 后，您将得到一个纯净的视频渲染视图，它已具备完整的直播业务能力，但没有任何交互 UI。您可以参考下一章节 [丰富直播场景](https://write.woa.com/#.E4.B8.B0.E5.AF.8C.E7.9B.B4.E6.92.AD.E5.9C.BA.E6.99.AF) 来完善直播场景。
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

<td rowspan="1" colSpan="1" >[CoGuestStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_co_guest_store/CoGuestStore-class.html)</td>

<td rowspan="1" colSpan="1" >[实现观众连线](https://write.woa.com/document/191126722261704704)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**实现主播跨房连线 PK**</td>

<td rowspan="1" colSpan="1" >两个不同房间的主播进行连线，实现互动或 PK。</td>

<td rowspan="1" colSpan="1" >[CoHostStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_co_host_store/CoHostStore-class.html) / [BattleStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_battle_store/BattleStore-class.html)</td>

<td rowspan="1" colSpan="1" >[实现主播连线 PK](https://write.woa.com/document/191126592718098432)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**添加弹幕聊天功能**</td>

<td rowspan="1" colSpan="1" >观众可以在直播间发送和接收实时文字消息。</td>

<td rowspan="1" colSpan="1" >[BarrageStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_barrage_barrage_store/BarrageStore-class.html)</td>

<td rowspan="1" colSpan="1" >[实现弹幕功能](https://write.woa.com/document/191126817095999488)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**构建礼物赠送系统**</td>

<td rowspan="1" colSpan="1" >观众可以向主播赠送虚拟礼物，增加互动和趣味性。</td>

<td rowspan="1" colSpan="1" >[GiftStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_gift_gift_store/GiftStore-class.html)</td>

<td rowspan="1" colSpan="1" >[实现礼物功能](https://write.woa.com/document/191127024797196288)</td>
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
<td rowspan="1" colSpan="1" >**LiveCoreWidget**</td>

<td rowspan="1" colSpan="1" >直播视频流展示与交互的核心视图组件：负责视频流渲染和视图挂件处理，支持主播直播、观众连麦、主播连线等场景。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_Flutter/api_view_live_live_core_widget/LiveCoreWidget-class.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**LiveCoreController**</td>

<td rowspan="1" colSpan="1" >LiveCoreWidget 的控制器：用于设置直播 ID、控制预览等操作。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_Flutter/api_view_live_live_core_widget/LiveCoreController-class.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**LiveListStore**</td>

<td rowspan="1" colSpan="1" >直播间全生命周期管理：创建 / 加入 / 离开 / 销毁房间，查询房间列表，修改直播信息（名称、公告等），监听直播状态（如被踢出、结束）。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_live_list_store/LiveListStore-class.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**DeviceStore**</td>

<td rowspan="1" colSpan="1" >音视频设备控制：麦克风（开关 / 音量）、摄像头（开关 / 切换 / 画质）、屏幕共享，设备状态实时监听。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_Flutter/api_device_device_store/DeviceStore-class.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**CoGuestStore**</td>

<td rowspan="1" colSpan="1" >观众连麦管理：连麦申请 / 邀请 / 同意 / 拒绝，连麦成员权限控制（麦克风 / 摄像头），状态同步。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_co_guest_store/CoGuestStore-class.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**CoHostStore**</td>

<td rowspan="1" colSpan="1" >主播跨房连线：支持多布局模板（动态网格等），发起 / 接受 / 拒绝连线，连麦主播互动管理。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_co_host_store/CoHostStore-class.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**BattleStore**</td>

<td rowspan="1" colSpan="1" >主播 PK 对战：发起 PK（配置时长 / 对手），管理 PK 状态（开始 / 结束），同步分数，监听对战结果。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_battle_store/BattleStore-class.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**GiftStore**</td>

<td rowspan="1" colSpan="1" >礼物互动：获取礼物列表，发送 / 接收礼物，监听礼物事件（含发送者、礼物详情）。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_Flutter/api_gift_gift_store/GiftStore-class.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**BarrageStore**</td>

<td rowspan="1" colSpan="1" >弹幕功能：发送文本 / 自定义弹幕，维护弹幕列表，实时监听弹幕状态。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_Flutter/api_barrage_barrage_store/BarrageStore-class.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**LikeStore**</td>

<td rowspan="1" colSpan="1" >点赞互动：发送点赞，监听点赞事件，同步总点赞数。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_like_store/LikeStore-class.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**LiveAudienceStore**</td>

<td rowspan="1" colSpan="1" >观众管理：获取实时观众列表（ID / 名称 / 头像），统计观众数量，监听观众进出事件。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_live_audience_store/LiveAudienceStore-class.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**AudioEffectStore**</td>

<td rowspan="1" colSpan="1" >音频特效：变声（童声 / 男声）、混响（KTV 等）、耳返调节，实时切换特效。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_Flutter/api_device_audio_effect_store/AudioEffectStore-class.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**BaseBeautyStore**</td>

<td rowspan="1" colSpan="1" >基础美颜：调节磨皮 / 美白 / 红润（0-100 级），重置美颜状态，同步效果参数。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_Flutter/api_device_base_beauty_store/BaseBeautyStore-class.html)</td>
</tr>
</table>


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

