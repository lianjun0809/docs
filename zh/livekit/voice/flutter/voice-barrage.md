> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

本篇文档旨在指导 Flutter 开发者如何使用 `AtomicXCore` 框架中的 `BarrageStore` 模块，为您的直播应用快速集成功能丰富、性能卓越的弹幕系统。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032457995/bd0558a4f51e11f09d0352540097cba1.png)


## 核心功能

`BarrageStore` 为您的直播应用提供了一套完整的弹幕解决方案，核心功能包括：
- 接收并展示直播间弹幕消息。

- 发送文本弹幕与观众互动。

- 发送自定义业务弹幕，以支持礼物、点赞等复杂场景。

- 在本地消息列表中插入系统提示（例如，"欢迎 XX 进入直播间"）。


## 核心概念解析
<table>
<tr>
<td rowspan="1" colSpan="1" >**核心概念**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**核心职责与描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[Barrage](https://tencent-rtc.github.io/TUIKit_Flutter/api_barrage_barrage_store/Barrage-class.html)</td>

<td rowspan="1" colSpan="1" >`class`</td>

<td rowspan="1" colSpan="1" >代表一条弹幕消息的数据模型。它包含了发送者信息 (`sender`)、消息内容 (`textContent` 或 `data`)、消息类型 (`messageType`) 等所有关键信息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[BarrageState](https://tencent-rtc.github.io/TUIKit_Flutter/api_barrage_barrage_store/BarrageState-class.html)</td>

<td rowspan="1" colSpan="1" >`class`</td>

<td rowspan="1" colSpan="1" >代表弹幕模块的当前状态。其核心属性 `messageList` 是一个 `ValueListenable<List<Barrage>>`，按时间顺序存储了当前直播间的所有弹幕消息，是 UI 渲染的数据源。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[BarrageStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_barrage_barrage_store/BarrageStore-class.html)</td>

<td rowspan="1" colSpan="1" >`class`</td>

<td rowspan="1" colSpan="1" >这是与弹幕功能交互的核心管理类。通过它，您可以发送消息 (`sendTextMessage`, `sendCustomMessage`)，并通过监听其 `barrageState.messageList` 属性来接收和监听所有弹幕消息的更新。</td>
</tr>
</table>


## 实现步骤

### 步骤1：组件集成

请参考 [快速接入](https://write.woa.com/document/197478016886185984) 集成 **AtomicXCore**，完成接入。

完成集成后回到当前工程。

### 步骤2：初始化并监听弹幕

获取一个与当前直播间 `liveId` 绑定的 `BarrageStore` 实例，并设置一个监听器来实时接收最新的**全量**弹幕消息列表。
``` java
import 'package:flutter/foundation.dart';
import 'package:atomic_x_core/atomicxcore.dart';

class BarrageManager {
  final String liveId;
  late final BarrageStore barrageStore;
  late final VoidCallback _messageListChangedListener = _onMessageListChanged;

  // 对外暴露消息列表的变化通知
  final ValueNotifier<List<Barrage>> messagesNotifier = 
      ValueNotifier<List<Barrage>>([]);

  BarrageManager({required this.liveId}) {
    // 1. 通过 liveId 获取 BarrageStore 的单例（位置参数）
    barrageStore = BarrageStore.create(liveId);

    // 2. 初始化后立即开始监听弹幕消息
    _subscribeToBarrageUpdates();
  }

  void _subscribeToBarrageUpdates() {
    // 3. 使用 ValueListenable 的 addListener 监听消息列表变化
    barrageStore.barrageState.messageList.addListener(_messageListChangedListener);
  }

  void _onMessageListChanged() {
    // 4. 当 messageList 更新时，获取新列表并通知 UI 层
    // 关键点：这里获取到的是包含所有历史消息的【完整列表】
    messagesNotifier.value = barrageStore.barrageState.messageList.value;
  }

  void dispose() {
    barrageStore.barrageState.messageList.removeListener(_messageListChangedListener);
    messagesNotifier.dispose();
  }
}
```

### 步骤3：发送文本弹幕

调用 `sendTextMessage` 方法向直播间内的所有用户广播一条纯文本消息。
``` java
extension BarrageManagerSend on BarrageManager {
  /// 发送一条文本弹幕
  Future<void> sendTextMessage(String text) async {
    // 建议：增加非空校验，避免发送无效消息
    if (text.isEmpty) {
      debugPrint("弹幕内容不能为空");
      return;
    }

    // 调用核心 API 发送消息
    final result = await barrageStore.sendTextMessage(
      text: text,
      extensionInfo: null,
    );

    // 使用 isSuccess 检查结果
    if (result.isSuccess) {
      debugPrint("文本弹幕 '$text' 发送成功");
    } else {
      debugPrint("文本弹幕发送失败: ${result.errorMessage}");
    }
  }
}
```

**接口参数：**
<table>
<tr>
<td rowspan="1" colSpan="1" >**参数**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`text`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >要发送的文本内容。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`extensionInfo`</td>

<td rowspan="1" colSpan="1" >`Map<String, String>?`</td>

<td rowspan="1" colSpan="1" >附加的扩展信息，可用于业务自定义。</td>
</tr>
</table>


### 步骤4：发送自定义弹幕

发送一条包含自定义业务逻辑的消息，例如礼物、点赞或游戏化互动指令。这条消息对其他客户端来说是透明的，需要业务层自行解析。
``` java
import 'dart:convert';

extension BarrageManagerCustom on BarrageManager {
  /// 发送一条自定义弹幕，例如用于发送礼物
  Future<void> sendGiftMessage({
    required String giftId,
    required int giftCount,
  }) async {
    // 1. 定义一个能识别业务的 ID
    const businessID = "live_gift";

    // 2. 将业务数据编码为 JSON 字符串
    final giftData = {"gift_id": giftId, "gift_count": giftCount};
    final jsonString = jsonEncode(giftData);

    // 3. 调用核心 API 发送自定义消息
    final result = await barrageStore.sendCustomMessage(
      businessID: businessID,
      data: jsonString,
    );

    if (result.isSuccess) {
      debugPrint("礼物消息（自定义弹幕）发送成功");
    } else {
      debugPrint("礼物消息发送失败: ${result.errorMessage}");
    }
  }
}
```

**接口参数：**
<table>
<tr>
<td rowspan="1" colSpan="1" >**参数**</td>

<td rowspan="1" colSpan="1" >**类型**</td>

<td rowspan="1" colSpan="1" >**描述**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`businessID`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >业务唯一标识符，例如 "live_gift"，用于接收端区分不同的自定义消息。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`data`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >业务数据，通常为 JSON 格式的字符串。</td>
</tr>
</table>


### 步骤5：在本地插入提示消息

在当前用户的消息列表中插入一条本地消息，这条消息不会被发送到直播间的其他用户。这非常适合用来显示系统欢迎、警告或操作提示等信息。
``` java
extension BarrageManagerLocal on BarrageManager {
  /// 在本地消息列表中插入一条欢迎提示
  void showWelcomeMessage(LiveUserInfo user) {
    // 1. 创建一条 Barrage 消息（使用命名参数构造函数）
    final welcomeTip = Barrage(
      messageType: BarrageType.text,
      textContent: "欢迎 ${user.userName} 进入直播间！",
    );

    // 2. 调用 API 将其插入本地列表
    barrageStore.appendLocalTip(welcomeTip);
  }
}
```

### 步骤6：管理用户发言（禁言与解禁）

作为主播或管理员，您可以对直播间内的用户发言权限进行管理，维护健康的社区氛围。

#### 禁止/解禁单个用户发言

通过 `LiveAudienceStore` 中的 `disableSendMessage` 接口来实现对指定用户的禁言或解禁。
``` java
// 1. 获取与当前直播间绑定的 LiveAudienceStore 实例（位置参数）
final liveId = "your_live_id";
final audienceStore = LiveAudienceStore.create(liveId);

// 2. 定义要操作的用户 ID 和禁言状态
final userIdToMute = "user_id_to_be_muted";
final shouldDisable = true; // true 为禁言, false 为解禁

// 3. 调用接口执行操作
final result = await audienceStore.disableSendMessage(
  userID: userIdToMute,
  isDisable: shouldDisable,
);

if (result.isSuccess) {
  debugPrint("${shouldDisable ? "禁言" : "解禁"}用户 $userIdToMute 成功");
} else {
  debugPrint("操作失败: ${result.errorMessage}");
}
```

#### 开启/关闭全体禁言

要对直播间内所有用户（通常不包括主播自己）进行禁言，您需要通过 `LiveListStore` 更新直播间信息来实现。
``` java
// 1. 获取 LiveListStore 单例
final liveListStore = LiveListStore.shared;

// 2. 获取当前直播间信息，并创建新的 LiveInfo 对象修改全体禁言状态
final currentLiveInfo = liveListStore.liveState.currentLive.value;
final updatedLiveInfo = LiveInfo(
  liveID: currentLiveInfo.liveID,
  liveName: currentLiveInfo.liveName,
  isMessageDisable: true, // true 为全体禁言, false 为关闭
);

// 3. 调用更新接口，并指定修改的标志位列表
final result = await liveListStore.updateLiveInfo(
  liveInfo: updatedLiveInfo,
  modifyFlagList: [ModifyFlag.isMessageDisable],
);

if (result.isSuccess) {
  debugPrint("全体禁言状态更新成功");
} else {
  debugPrint("操作失败: ${result.errorMessage}");
}
```

## 完整 UI 示例
``` java
import 'package:flutter/material.dart';
import 'package:atomic_x_core/atomicxcore.dart';

class BarrageWidget extends StatefulWidget {
  final String liveId;

  const BarrageWidget({Key? key, required this.liveId}) : super(key: key);

  @override
  State<BarrageWidget> createState() => _BarrageWidgetState();
}

class _BarrageWidgetState extends State<BarrageWidget> {
  late BarrageManager _barrageManager;
  final TextEditingController _inputController = TextEditingController();
  final ScrollController _scrollController = ScrollController();

  @override
  void initState() {
    super.initState();
    _barrageManager = BarrageManager(liveId: widget.liveId);
  }

  void _scrollToBottom() {
    WidgetsBinding.instance.addPostFrameCallback((_) {
      if (_scrollController.hasClients) {
        _scrollController.animateTo(
          _scrollController.position.maxScrollExtent,
          duration: const Duration(milliseconds: 200),
          curve: Curves.easeOut,
        );
      }
    });
  }

  @override
  void dispose() {
    _barrageManager.dispose();
    _inputController.dispose();
    _scrollController.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        // 弹幕列表
        Expanded(
          child: ValueListenableBuilder<List<Barrage>>(
            valueListenable: _barrageManager.messagesNotifier,
            builder: (context, messageList, child) {
              // 滚动到底部
              _scrollToBottom();
              return ListView.builder(
                controller: _scrollController,
                itemCount: messageList.length,
                itemBuilder: (context, index) {
                  final barrage = messageList[index];
                  return _buildBarrageItem(barrage);
                },
              );
            },
          ),
        ),
        // 输入框
        _buildInputBar(),
      ],
    );
  }

  Widget _buildBarrageItem(Barrage barrage) {
    return Container(
      margin: const EdgeInsets.symmetric(vertical: 4, horizontal: 8),
      padding: const EdgeInsets.symmetric(horizontal: 12, vertical: 6),
      decoration: BoxDecoration(
        color: Colors.black54,
        borderRadius: BorderRadius.circular(16),
      ),
      child: RichText(
        text: TextSpan(
          children: [
            TextSpan(
              text: '${barrage.sender.userName}: ',
              style: const TextStyle(
                color: Colors.yellow,
                fontSize: 14,
                fontWeight: FontWeight.bold,
              ),
            ),
            TextSpan(
              text: barrage.textContent,
              style: const TextStyle(color: Colors.white, fontSize: 14),
            ),
          ],
        ),
      ),
    );
  }

  Widget _buildInputBar() {
    return Container(
      padding: const EdgeInsets.all(8),
      color: Colors.white,
      child: Row(
        children: [
          Expanded(
            child: TextField(
              controller: _inputController,
              decoration: const InputDecoration(
                hintText: '说点什么...',
                border: OutlineInputBorder(),
                contentPadding: EdgeInsets.symmetric(horizontal: 12),
              ),
              onSubmitted: (_) => _sendMessage(),
            ),
          ),
          const SizedBox(width: 8),
          ElevatedButton(
            onPressed: _sendMessage,
            child: const Text('发送'),
          ),
        ],
      ),
    );
  }

  void _sendMessage() {
    final text = _inputController.text.trim();
    if (text.isNotEmpty) {
      _barrageManager.sendTextMessage(text);
      _inputController.clear();
    }
  }
}
```

## 功能进阶：优化高并发场景性能

当您使用 `BarrageStore` 构建弹幕功能后，本章将指导您如何处理更复杂的业务场景，确保它能在真实、复杂的高并发直播场景下，依然为用户提供流畅、稳定的体验。本章将围绕三个核心业务场景，为您提供明确的优化方案和代码示例。

### 场景一：高并发弹幕场景

#### 场景描述

在一场热门活动中，直播间涌入大量观众，弹幕以每秒数十条的频率刷新。

#### **技术挑战**

SDK 会以极高频率返回完整的弹幕列表。如果每次都重建 UI，主线程会被密集的 UI 布局和渲染操作阻塞，导致界面卡顿。

#### **优化方案: **批处理与流量削峰 (Batch Processing & Debouncing)

不必响应每一次的数据更新，而是设定一个时间阈值（例如300毫秒）。只在距离上次 UI 刷新超过这个阈值后，才执行下一次刷新操作。这能将每秒数十次的 UI重绘，降低到每秒3-4次，极大提升流畅度。
``` java
class BarrageUIManager {
  List<Barrage>? _latestMessageList;
  Timer? _refreshTimer;
  final void Function(List<Barrage>) onUpdate;

  BarrageUIManager({required this.onUpdate}) {
    // 每 0.3 秒检查一次是否需要刷新
    _refreshTimer = Timer.periodic(
      const Duration(milliseconds: 300),
      (_) => _refreshUIIfNeeded(),
    );
  }

  /// 外部高频调用此方法，传入最新的全量列表
  void update(List<Barrage> fullList) {
    _latestMessageList = fullList;
  }

  void _refreshUIIfNeeded() {
    // 检查是否有新的数据待刷新
    final newList = _latestMessageList;
    if (newList == null) return;

    _latestMessageList = null; // 清空标志位，避免重复刷新
    
    // 更新数据源并刷新UI
    onUpdate(newList);
  }

  void dispose() {
    _refreshTimer?.cancel();
  }
}
```

### 场景二：保障长时间直播的内存稳定性

#### 场景描述

您的应用需要支持数小时乃至全天候的“不间断直播”，例如游戏直播或慢直播。在此期间，App 必须保持稳定运行，不能因为长时间运行而意外退出。

#### 技术挑战

SDK 返回的全量 `messageList` 会在长时间直播中无限增长，即使 UI 层做了节流，数据层持有的这个巨大数组也会持续侵占内存，最终导致应用闪退。

#### **优化方案**：固定容量的循环数组 (Circular Buffer)

**只让您自己的数据源（DataSource）持有有限数量的消息**。无论 SDK 返回的全量列表有多大，您的应用只截取其中最新的部分用于显示。
``` java
void _refreshUIIfNeeded() {
  final fullList = _latestMessageList;
  if (fullList == null) return;

  _latestMessageList = null;

  // 关键点：截取最新的 N 条消息
  const capacity = 500; // 客户端只保留最新的500条消息
  final cappedList = fullList.length > capacity 
      ? fullList.sublist(fullList.length - capacity)
      : fullList;

  onUpdate(cappedList);
}
```

## API 文档

关于 [BarrageStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_barrage_barrage_store/BarrageStore-class.html) 及其相关类的所有公开接口、属性和方法的详细信息，请参阅随 [AtomicXCore](https://tencent-rtc.github.io/TUIKit_Flutter/index.html) 框架的官方 API 文档。

## 常见问题

### 如何实现彩色弹幕、礼物弹幕等更丰富的弹幕样式？

这是通过自定义消息 `sendCustomMessage` 来实现的。`BarrageStore` 不会限制您的业务想象力。

**实现思路**
1. **定义数据结构:** 与您的客户端和服务器团队共同定义好自定义消息的 JSON 结构。例如，一条彩色弹幕可以这样定义：

   ``` json
   {  "type": "colored_text",  "text": "这是一条彩色弹幕!",  "color": "#FF5733" }
   ```
2. **发送端:** 在发送时，将这个 JSON 结构转换为字符串，并通过 `sendCustomMessage` 的 `data` 参数发送出去。`businessId` 可以设置为一个能代表您业务的唯一标识，例如 "`barrage_style_v1`"。

3. **接收端**: 在接收到弹幕消息后，检查其 `messageType` 是否为 `.custom` 以及 `businessId` 是否匹配。如果匹配，则解析 `data` 字符串（通常是解析 JSON），根据解析出的数据（例如 `color、text`）来渲染您的自定义 UI 样式。


### 不同的类、不同的文件中都调用了 `BarrageStore.create("some_id")`，这会创建出多个实例导致混乱吗？

完全不会。`AtomicXCore` 内部机制会确保只要您传入的 `liveId` 相同，获取到的永远是同一个与该直播间绑定的 `BarrageStore` 实例。您可以在需要的地方随用随取，无需手动管理单例。

### 为什么调用了 sendTextMessage，但是在消息列表中看不到发送的消息？

**请按以下步骤排查：**
1. **检查返回结果**：`sendTextMessage` 方法有一个完成回调。请检查回调返回的结果是成功还是失败。如果失败，错误信息会明确指出问题所在（例如“您已被禁言”、“网络错误”等）。

2. **确认监听时机**：确保您对 `barrageStore.state` 的订阅发生在该 `liveId` 对应的直播开始之后。如果在加入直播房间之前就开始监听，可能会错过部分消息。

3. **检查 liveId**：确认您在创建 `BarrageStore` 实例、加入直播房间、以及发送消息时使用的 `liveId` 完全一致，包括大小写。

4. **网络问题**：检查设备当前的网络连接是否正常。消息发送依赖于网络。


### 新观众进入直播间时，如何让他们看到加入前的历史弹幕消息？

`AtomicXCore` 支持拉取历史弹幕消息，但这需要您在**服务端控制台**进行一项简单的配置。配置完成后，SDK 会自动处理后续的一切，您无需编写额外的代码。

**步骤1：在 IM 控制台进行配置**
1. 登录您的 [即时通讯 IM 控制台](https://cloud.tencent.com/login?s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fim)。

2. 在左侧导航栏按照路径：**消息服务 Chat** >** 功能配置 **>** 群组配置 **> **群功能配置** >** 直播群新成员查看入群前消息量配置**进行导航。

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032457995/c683c9d2dcba11f0be395254005ef0f7.png)

3. 修改“新成员可查看最近消息数”，最大支持 **50** 条。


   **步骤2：客户端无感获取 **


   完成上述配置后，您的客户端代码**无需做任何改动**。 


   当新用户加入直播间时，`AtomicXCore` 的底层 会自动拉取您配置的历史消息数量。这些历史消息会和实时消息一样，通过您已实现的 `BarrageStore.barrageState` 订阅通道推送给您的 UI 层。您的应用会像接收实时弹幕一样，自然地接收并展示这些历史弹幕。
