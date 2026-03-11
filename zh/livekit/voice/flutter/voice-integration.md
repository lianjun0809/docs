> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

本文档将帮助开发者使用 `AtomicXCore SDK` 的 `LiveListStore` 和 `LiveSeatStore` 快速构建一个包含主播开播和观众进房功能的语聊房 `App`。

## 核心概念

在开始集成之前，请先通过下表了解一下 `LiveSeatStore` 相关的几个核心概念：
<table>
<tr>
<td rowspan="1" colSpan="1" >**核心概念**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**核心职责与描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[LiveSeatStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_live_seat_store/LiveSeatStore-class.html)</td>

<td rowspan="1" colSpan="1" >`class`</td>

<td rowspan="1" colSpan="1" >麦位管理核心，负责管理房间内的所有麦位信息和麦位相关操作。<br>通过 `liveSeatState.seatList` 暴露实时的麦位列表数据流。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[LiveSeatState](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_live_seat_store/LiveSeatState-class.html)</td>

<td rowspan="1" colSpan="1" >`class`</td>

<td rowspan="1" colSpan="1" >代表麦位的当前状态。<br>- `seatList` 是一个 `ValueListenable<List<SeatInfo>>` 类型，存储了麦位列表的实时状态；<br>- `speakingUsers` 则代表当前正在说话的人和对应的音量。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[SeatInfo](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_live_seat_store/SeatInfo-class.html)</td>

<td rowspan="1" colSpan="1" >`class`</td>

<td rowspan="1" colSpan="1" >单个麦位的数据模型。`LiveSeatStore` 所推送的麦位列表（`seatList`）就是由多个 `SeatInfo` 对象组成的。关键字段：<br>- `index`（麦位的索引）。<br>- `isLocked`（麦位是否被锁定）。<br>- `userInfo`（麦位上的用户信息，如果麦位为空，此字段也为空对象）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[SeatUserInfo](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_live_seat_store/SeatUserInfo-class.html)</td>

<td rowspan="1" colSpan="1" >`class`</td>

<td rowspan="1" colSpan="1" >麦上用户的详细数据模型。当一个用户成功上麦后，`SeatInfo` 中的 `userInfo` 字段就会被填充为此用户。关键字段：<br>- `userID`（用户的唯一 ID）<br>- `userName`（用户的昵称）<br>- `avatarURL`（用户的头像 URL）<br>- `microphoneStatus`（麦克风状态）<br>- `cameraStatus`（摄像头状态）。</td>
</tr>
</table>


## 准备工作

### 步骤1：开通服务

请参见 [开通服务](https://write.woa.com/document/141302177829593088)，获取体验版或付费版 `SDK`。

### 步骤2：在当前项目中导入 AtomicXCore
1. **安装组件**：请在您的 `pubspec.yaml` 文件中添加 `atomic_x_core` 依赖，然后执行 `flutter pub get`。

   ``` yaml
   dependencies:
     atomic_x_core: ^3.6.0
   ```
2. **配置工程权限：**Android 和 iOS 工程都需要配置权限。


   

【Android】

在 `android/app/src/main/AndroidManifest.xml` 文件中添加麦克风的使用权限说明。
``` xml
<uses-permission android:name="android.permission.RECORD_AUDIO" />
```

【iOS】

在应用 `ios` 目录的 **Podfile** 和 `ios/Runner` 目录的 `Info.plist` 文件中添加麦克风的使用权限说明。

**Podfile**
``` ruby
post_install do |installer|
  installer.pods_project.targets.each do |target|
    flutter_additional_ios_build_settings(target)
      target.build_configurations.each do |config|
          config.build_settings['GCC_PREPROCESSOR_DEFINITIONS'] ||= [
        '$(inherited)',
        'PERMISSION_MICROPHONE=1',
        ]
      end
  end
end
```

**Info.plist**
``` xml
<key>NSMicrophoneUsageDescription</key>
<string>TUILiveKit需要访问您的麦克风权限，开启后录制的视频才会有声音</string>
```


### 步骤3：实现登录逻辑

在项目中调用 `LoginStore.shared.login` 完成登录，**这是使用 **`AtomicXCore`** 所有功能的关键前提**。

> **重要：**
> 

> 推荐在您 App 自身的用户账户登录成功后，再调用 LoginStore.shared.login，以确保登录业务逻辑的清晰和一致。
> 

``` java
import 'package:flutter/material.dart';
import 'package:atomic_x_core/atomicxcore.dart';

// main.dart
void main() async {
  WidgetsFlutterBinding.ensureInitialized();

  // 登录
  final result = await LoginStore.shared.login(
    sdkAppID: 1400000001,           // 替换为您的 sdkAppID
    userID: "test_001",             // 替换为您的 userID
    userSig: "xxxxxxxxxxx",         // 替换为您的 userSig
  );

  if (result.isSuccess) {
    debugPrint("login success");
  } else {
    debugPrint("login failed code: ${result.code}, message: ${result.message}");
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


## 构建基础语聊房应用

### 步骤1：实现房主创建语聊房

房主开播流程如下，您只需执行以下几步操作，即可快速搭建一个语聊房。

#### 1. 初始化麦位 Store

在您的房主页面中，创建一个 `LiveSeatStore` 实例。您需要监听 `liveSeatStore.liveSeatState` 的变化，以实时获取麦位数据来渲染您的 `UI`。
``` java
import 'package:flutter/material.dart';
import 'package:atomic_x_core/atomicxcore.dart';

// YourAnchorPage 代表您的房主页面
class YourAnchorPage extends StatefulWidget {
  const YourAnchorPage({super.key});

  @override
  State<YourAnchorPage> createState() => _YourAnchorPageState();
}

class _YourAnchorPageState extends State<YourAnchorPage> {
  final _liveListStore = LiveListStore.shared;
  final _deviceStore = DeviceStore.shared;

  // 使用 liveID 初始化 LiveSeatStore
  final String _liveID = "test_voice_room_001";
  late final LiveSeatStore _liveSeatStore;
  late final VoidCallback _seatListListener = _onSeatListChanged;

  @override
  void initState() {
    super.initState();
    _liveSeatStore = LiveSeatStore.create(_liveID);

    // 监听麦位列表变化
    _observeSeatList();
  }

  void _observeSeatList() {
    // 监听 liveSeatState.seatList 的变化，并更新您的麦位 UI
    _liveSeatStore.liveSeatState.seatList.addListener(_seatListListener);
  }

  void _onSeatListChanged() {
    // 在这里根据 seatInfoList 渲染您的麦位 UI
    final seatInfoList = _liveSeatStore.liveSeatState.seatList.value;
    debugPrint("Seat list updated: ${seatInfoList.length} seats");
    setState(() {});
  }

  @override
  void dispose() {
    _liveSeatStore.liveSeatState.seatList.removeListener(_seatListListener);
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    // 假设您有自己的布局
    return Container();
  }
}
```

#### 2. 打开麦克风

通过调用 `DeviceStore` 的 `openLocalMicrophone` 接口打开麦克风，示例代码如下：
``` java
class _YourAnchorPageState extends State<YourAnchorPage> {
  // ... 其他代码 ...

  void _openDevices() {
    // 打开麦克风
    DeviceStore.shared.openLocalMicrophone();
  }
}
```

#### 3. 开始语聊

通过调用 `LiveListStore` 的 `createLive` 接口开始语聊房直播，完整示例代码如下：
``` java
class _YourAnchorPageState extends State<YourAnchorPage> {
  // ... 其他代码 ...
  final String _liveID = "test_voice_room_001";

  @override
  void initState() {
    super.initState();
    // ... 其他代码 ...

    // 开始语聊
    _startLive();
  }

  Future<void> _startLive() async {
    // 1. 准备 LiveInfo 对象
    final liveInfo = LiveInfo(
      // 2. 设置房间 id
      liveID: _liveID,
      // 3. 设置房间名称
      liveName: "test 语聊房",
      // 4. 配置为语聊房（启用麦位）
      isSeatEnabled: true,
      // 5. 房主默认上麦
      keepOwnerOnSeat: true,
      // 6. 设置麦位布局模板（例如 70 为 10 麦位模板）
      // 重要：请根据产品规范传入正确的 ID
      seatLayoutTemplateID: 70,
      // 7. 设置上麦模式，例如申请上麦
      seatMode: TakeSeatMode.apply,
      // 8. 设置最大麦位数
      maxSeatCount: 10,
    );

    // 9. 调用 createLive 开始直播
    final result = await _liveListStore.createLive(liveInfo);

    if (result.isSuccess) {
      debugPrint("Response startLive onSuccess");
      // 房主创建成功后，默认会上麦，此时您可以调用 unmuteMicrophone
      _liveSeatStore.unmuteMicrophone();
    } else {
      debugPrint("Response startLive onError: ${result.message}");
    }
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

<td rowspan="1" colSpan="1" >直播间的唯一标识符</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`liveName`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >直播间的标题</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`notice`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >直播间的公告信息</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`isMessageDisable`</td>

<td rowspan="1" colSpan="1" >`bool`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >是否禁言（`true`：是，`false`：否）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`isPublicVisible`</td>

<td rowspan="1" colSpan="1" >`bool`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >是否公开可见（`true`：是，`false`：否）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`isSeatEnabled`</td>

<td rowspan="1" colSpan="1" >`bool`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >是否启用麦位功能（`true`：是，`false`：否）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`keepOwnerOnSeat`</td>

<td rowspan="1" colSpan="1" >`bool`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >是否保持房主在麦位上</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`maxSeatCount`</td>

<td rowspan="1" colSpan="1" >`int`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >最大麦位数量</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`seatMode`</td>

<td rowspan="1" colSpan="1" >`TakeSeatMode`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >上麦模式（`free`：自由上麦，`apply`：申请上麦）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`seatLayoutTemplateID`</td>

<td rowspan="1" colSpan="1" >`int`</td>

<td rowspan="1" colSpan="1" >必填</td>

<td rowspan="1" colSpan="1" >麦位布局模板 `ID`</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`coverURL`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >直播间的封面图片地址</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`backgroundURL`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >直播间的背景图片地址</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`categoryList`</td>

<td rowspan="1" colSpan="1" >`List<int>`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >直播间的分类标签列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`activityStatus`</td>

<td rowspan="1" colSpan="1" >`int`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >直播活动状态</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`isGiftEnabled`</td>

<td rowspan="1" colSpan="1" >`bool`</td>

<td rowspan="1" colSpan="1" >选填</td>

<td rowspan="1" colSpan="1" >是否启用礼物功能（`true`：是，`false`：否）</td>
</tr>
</table>


#### 4. 构建麦位 UI 界面

> **提示：**
> 

> 麦位 `UI` 效果的业务代码，可参考 `TUILiveKit` 开源项目中的 [seat_grid_widget.dart](https://github.com/Tencent-RTC/TUIKit_Flutter/blob/main/live/livekit/lib/seat_grid_widget/seat_grid_widget.dart) 文件来了解完整的实现逻辑。
> 


通过 `LiveSeatStore` 实例，监听 `liveSeatState.seatList` 的变化，以实时获取麦位数据来渲染您的 UI。您可以在页面中（例如 `YourAnchorPage` 或 `YourAudiencePage`）通过以下方式监听数据：
``` java
class _YourAnchorPageState extends State<YourAnchorPage> {
  // ... 其他代码 ...
  late final LiveSeatStore _liveSeatStore;
  late final VoidCallback _seatListListener = _onSeatListChanged;

  @override
  void initState() {
    super.initState();
    _liveSeatStore = LiveSeatStore.create("your_live_id");
    // ... 其他代码 ...

    // 监听 seatList 变化
    _observeSeatList();
  }

  void _observeSeatList() {
    // 监听 liveSeatState.seatList 变化，并更新您的麦位 UI
    _liveSeatStore.liveSeatState.seatList.addListener(_seatListListener);
  }

  void _onSeatListChanged() {
    // seatInfoList 即为最新的麦位列表 (List<SeatInfo>)
    final seatInfoList = _liveSeatStore.liveSeatState.seatList.value;
    // 在这里根据 seatInfoList 渲染您的麦位 UI
    debugPrint("Seat list updated: ${seatInfoList.length} seats");
    setState(() {});
  }

  @override
  void dispose() {
    _liveSeatStore.liveSeatState.seatList.removeListener(_seatListListener);
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return ValueListenableBuilder<List<SeatInfo>>(
      valueListenable: _liveSeatStore.liveSeatState.seatList,
      builder: (context, seatList, child) {
        return GridView.builder(
          gridDelegate: const SliverGridDelegateWithFixedCrossAxisCount(
            crossAxisCount: 4,
          ),
          itemCount: seatList.length,
          itemBuilder: (context, index) {
            final seat = seatList[index];
            return _buildSeatItem(seat);
          },
        );
      },
    );
  }

  Widget _buildSeatItem(SeatInfo seat) {
    // 构建单个麦位 UI
    return Container();
  }
}
```

#### 5. 结束语聊

语聊结束后，房主可以调用 `LiveListStore` 的 `endLive` 接口结束语聊，`SDK` 会处理停止推流和销毁房间的逻辑。
``` java
class _YourAnchorPageState extends State<YourAnchorPage> {
  // ... 其他代码 ...

  // 结束语聊
  Future<void> _stopLive() async {
    final result = await _liveListStore.endLive();

    if (result.isSuccess) {
      debugPrint("endLive success");
    } else {
      debugPrint("endLive error: ${result.message}");
    }
  }
}
```

### 步骤2：实现观众进入语聊房

观众进房流程如下，通过简单几步操作，即可实现观众进入语聊房。

#### 1. 初始化麦位 Store

在您的观众页面中，创建 `LiveSeatStore` 实例，并监听 `liveSeatState.seatList` 的变化，以渲染麦位 `UI`。
``` java
import 'package:flutter/material.dart';
import 'package:atomic_x_core/atomicxcore.dart';

// YourAudiencePage 代表您的观众页面
class YourAudiencePage extends StatefulWidget {
  const YourAudiencePage({super.key});

  @override
  State<YourAudiencePage> createState() => _YourAudiencePageState();
}

class _YourAudiencePageState extends State<YourAudiencePage> {
  final _liveListStore = LiveListStore.shared;

  // 确保 liveID 与房主一致
  final String _liveID = "test_voice_room_001";
  late final LiveSeatStore _liveSeatStore;
  late final VoidCallback _seatListListener = _onSeatListChanged;

  @override
  void initState() {
    super.initState();
    _liveSeatStore = LiveSeatStore.create(_liveID);

    // 监听麦位列表变化
    _observeSeatList();
  }

  void _observeSeatList() {
    // 监听 liveSeatState.seatList 变化，并更新您的麦位 UI
    _liveSeatStore.liveSeatState.seatList.addListener(_seatListListener);
  }

  void _onSeatListChanged() {
    // 在这里根据 seatInfoList 渲染您的麦位 UI
    final seatInfoList = _liveSeatStore.liveSeatState.seatList.value;
    debugPrint("AudiencePage Seat list updated: ${seatInfoList.length} seats");
    setState(() {});
  }

  @override
  void dispose() {
    _liveSeatStore.liveSeatState.seatList.removeListener(_seatListListener);
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    // 假设您有自己的布局
    return Container();
  }
}
```

#### 2. 进入语聊房

通过调用 `LiveListStore` 的 `joinLive` 接口加入语聊房，完整示例代码如下：
``` java
class _YourAudiencePageState extends State<YourAudiencePage> {
  // ... 其他代码 ...

  @override
  void initState() {
    super.initState();
    // ... 其他代码 ...

    // 进入语聊房
    _joinLive();
  }

  Future<void> _joinLive() async {
    // 调用 joinLive 进入语聊房
    final result = await _liveListStore.joinLive(_liveID);

    if (result.isSuccess) {
      debugPrint("joinLive success");
    } else {
      debugPrint("joinLive error: ${result.message}");
    }
  }
}
```

#### 3. 构建麦位 UI 界面

观众构建麦位 UI 界面的流程与主播完全一致，请参考[构建麦位 UI 界面](https://write.woa.com/#4.-.E6.9E.84.E5.BB.BA.E9.BA.A6.E4.BD.8D-ui-.E7.95.8C.E9.9D.A2)。

#### 4. 退出语聊房

观众退出语聊房时，需要调用 `LiveListStore` 的 `leaveLive` 接口来退出。
``` java
class _YourAudiencePageState extends State<YourAudiencePage> {
  // ... 其他代码 ...

  Future<void> _leaveLive() async {
    final result = await _liveListStore.leaveLive();

    if (result.isSuccess) {
      debugPrint("leaveLive success");
    } else {
      debugPrint("leaveLive error: ${result.message}");
    }
  }
}
```

### 运行效果

完成上述步骤后，即可完成一个最基础的语聊直播场景。您可以参考 [丰富语聊房场景](https://write.woa.com/#.E4.B8.B0.E5.AF.8C.E8.AF.AD.E8.81.8A.E6.88.BF.E5.9C.BA.E6.99.AF) 来完善语聊场景。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032457995/9b1930a4df3011f0a38652540044a08e.png)


## 功能进阶

### 实现麦上用户说话音浪

在语聊房场景中，一个常见的需求是当麦上用户说话时，在其头像上显示一个波浪动画，以提示全房间用户"谁在说话"，`LiveSeatStore` 提供了 `speakingUsers` 数据流，专门用于实现此功能。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032457995/af03283cdf3011f0a4f35254007c27c5.png)


#### 实现方式

> **提示：**
> 

> 麦上用户说话时展示波浪动画效果，可参考 `TUILiveKit` 开源项目中的 [seat_grid_widget.dart](https://github.com/Tencent-RTC/TUIKit_Flutter/blob/main/live/livekit/lib/seat_grid_widget/seat_grid_widget.dart) 文件来了解完整的实现逻辑。
> 


在 `YourAnchorPage` 或 `YourAudiencePage` 中监听 `speakingUsers` 变化，并更新"正在说话"状态，代码示例如下：
``` java
class _YourAnchorPageState extends State<YourAnchorPage> {
  late final VoidCallback _speakingUsersListener = _onSpeakingUsersChanged;
    // ... 其他代码 ...

  @override
  void initState() {
    super.initState();
    // ... 其他代码 ...

    // 监听 speakingUsers 变化
    _observeSpeakingUsersState();
  }

  void _observeSpeakingUsersState() {
    // 监听 liveSeatState.speakingUsers 变化，并更新"正在说话"状态
    _liveSeatStore.liveSeatState.speakingUsers.addListener(_speakingUsersListener);
  }

  void _onSpeakingUsersChanged() {
    // 将 "正在说话" 的用户 ID 集合传递给 UI，更新 UI 状态
    final speakingUserMap = _liveSeatStore.liveSeatState.speakingUsers.value;
    debugPrint("Speaking users updated: ${speakingUserMap.length} users");
    setState(() {});
  }

  @override
  void dispose() {
    _liveSeatStore.liveSeatState.speakingUsers.removeListener(_speakingUsersListener);
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return ValueListenableBuilder<Map<String, int>>(
      valueListenable: _liveSeatStore.liveSeatState.speakingUsers,
      builder: (context, speakingUsers, child) {
        // speakingUsers 是一个 Map，key 是 userID，value 是音量
        return YourSpeakingIndicatorWidget(speakingUsers: speakingUsers);
      },
    );
  }
}

// 示例：正在说话指示器组件
class YourSpeakingIndicatorWidget extends StatelessWidget {
  final Map<String, int> speakingUsers;

  const YourSpeakingIndicatorWidget({
    super.key,
    required this.speakingUsers,
  });

  @override
  Widget build(BuildContext context) {
    return Container();
  }
}
```

## 丰富语聊房场景

当您完成了基础的语聊房功能后，您可以参考以下功能指南来为语聊房添加丰富的互动玩法。
<table>
<tr>
<td rowspan="1" colSpan="1" >**功能**</td>

<td rowspan="1" colSpan="1" >**功能介绍**</td>

<td rowspan="1" colSpan="1" >**功能 Stores**</td>

<td rowspan="1" colSpan="1" >**实现指南**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**实现听众上麦**</td>

<td rowspan="1" colSpan="1" >听众申请上麦，与房主进行实时语音互动。</td>

<td rowspan="1" colSpan="1" >[CoGuestStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_co_guest_store/CoGuestStore-class.html)</td>

<td rowspan="1" colSpan="1" >[观众上麦](https://write.woa.com/document/197477898206908416)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**添加弹幕聊天功能**</td>

<td rowspan="1" colSpan="1" >房间内成员可以发送和接收实时文字消息。</td>

<td rowspan="1" colSpan="1" >[BarrageStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_barrage_barrage_store/BarrageStore-class.html)</td>

<td rowspan="1" colSpan="1" >[实现弹幕功能](https://write.woa.com/document/200285441364750336)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**构建礼物赠送系统**</td>

<td rowspan="1" colSpan="1" >观众可以向主播赠送虚拟礼物，增加互动和趣味性。</td>

<td rowspan="1" colSpan="1" >[GiftStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_gift_gift_store/GiftStore-class.html)</td>

<td rowspan="1" colSpan="1" >[实现礼物功能](https://write.woa.com/document/200285576402239488)</td>
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
<td rowspan="1" colSpan="1" >**LiveListStore**</td>

<td rowspan="1" colSpan="1" >直播间全生命周期管理：创建 / 加入 / 离开 / 销毁房间，查询房间列表，修改直播信息（名称、公告等），监听直播状态（如被踢出、结束）。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_live_list_store/LiveListStore-class.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**LiveSeatStore**</td>

<td rowspan="1" colSpan="1" >麦位管理核心：管理麦位列表、麦上用户状态、麦位相关操作（上麦、下麦、踢人、锁麦、开关麦克风/摄像头等），监听麦位事件。</td>

<td rowspan="1" colSpan="1" >[API 文档](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_live_seat_store/LiveSeatStore-class.html)</td>
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

### 听众进房后无声音
- **检查设备权限**：请确保 `App` 已在 `Info.plist`（iOS）或 `AndroidManifest.xml`（Android）中声明并获得了麦克风的系统使用权限。

- **检查房主端**：房主端是否正常调用 `DeviceStore.shared.openLocalMicrophone()` 打开了麦克风。

- **检查网络**：请检查设备网络连接是否正常。


### 麦位列表未显示或更新
- **检查 Store 初始化**：请确保您在 `createLive` 或 `joinLive` 之前，已经使用相同的 `liveID` 正确创建了 `LiveSeatStore` 实例（`LiveSeatStore.create(liveID)`）。

- **检查数据监听**：请检查您是否正确使用了 `addListener` 来监听 `liveSeatStore.liveSeatState.seatList`，并确保在 `dispose` 中调用 `removeListener` 移除监听。

- **检查接口调用**：请确保 `createLive`（房主）或 `joinLive`（听众）接口已成功调用（在回调结果的 `isSuccess` 为 `true` 时确认）。
