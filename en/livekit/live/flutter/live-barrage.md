> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

This document aims to guide Flutter developers on how to use the `BarrageStore` module in the `AtomicXCore` framework to quickly integrate a bullet screen system with various features and outstanding performance for your live stream app.

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032457995/e62bfa87f76211f0822d525400074c32.png)


## Core Features

`BarrageStore` provides a complete bullet screen solution for your live stream app. Core features include:
- Receive and show danmakus information in live rooms.

- Send text bullet screen for audience interaction.

- Send custom business bullet screen to support complex scenarios such as gift and likes.

- Insert a system prompt in the local message list (for example, "Welcome XX to enter live room").


## Core Concept Analysis
<table>
<tr>
<td rowspan="1" colSpan="1" >**Core Concept**</td>

<td rowspan="1" colSpan="1" >**Type**</td>

<td rowspan="1" colSpan="1" >**Core Responsibility and Description**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[Barrage](https://tencent-rtc.github.io/TUIKit_Flutter/api_barrage_barrage_store/Barrage-class.html)</td>

<td rowspan="1" colSpan="1" >`class`</td>

<td rowspan="1" colSpan="1" >Represents a data model for a Danmu Message. It contains all key information such as sender information (`sender`), message content (`textContent` or `data`), and message type (`messageType`).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[BarrageState](https://tencent-rtc.github.io/TUIKit_Flutter/api_barrage_barrage_store/BarrageState-class.html)</td>

<td rowspan="1" colSpan="1" >`class`</td>

<td rowspan="1" colSpan="1" >Represents the current status of the bullet screen module. Its core attribute `messageList` is a `ValueListenable<List<Barrage>>`, storing all Danmu messages in the live streaming room in chronological order, serving as the data source for UI rendering.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[BarrageStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_barrage_barrage_store/BarrageStore-class.html)</td>

<td rowspan="1" colSpan="1" >`class`</td>

<td rowspan="1" colSpan="1" >This is the core management class for danmu function interaction. Through it, you can send messages (`sendTextMessage`, `sendCustomMessage`) and receive and listen to ALL Danmu Message updates by listening to its `barrageState.messageList` property.</td>
</tr>
</table>


## Implementation Steps

### Step 1: Integrating the Component
- **Live streaming**: Refer to [quick integration](https://write.woa.com/document/200455640177692672) for seamless integration with **AtomicXCore** and service access.

- **Voice chat room**: Refer to [quick integration](https://write.woa.com/document/200555778169073664) for seamless integration with **AtomicXCore** and service access.


   Return to the current project after integration.


### Step 2: Initialize and Listen to the Bullet Screen

Retrieve a `BarrageStore` instance bound to the current live streaming room `liveId`, and set a listener to receive the latest **Full** barrage message list in real time.
``` java
import 'package:flutter/foundation.dart';
import 'package:atomic_x_core/atomicxcore.dart';

class BarrageManager {
  final String liveId;
  late final BarrageStore barrageStore;
  late final VoidCallback _messageListChangedListener = _onMessageListChanged;

  // Expose message list change notification to the public
  final ValueNotifier<List<Barrage>> messagesNotifier = 
      ValueNotifier<List<Barrage>>([]);

  BarrageManager({required this.liveId}) {
    // 1. Get the singleton of BarrageStore by liveId (location parameter)
    barrageStore = BarrageStore.create(liveId);

    // 2. Start listening to the bullet screen immediately after initialization
    _subscribeToBarrageUpdates();
  }

  void _subscribeToBarrageUpdates() {
    // 3. Use ValueListenable's addListener to listen for messages list adjustment
    barrageStore.barrageState.messageList.addListener(_messageListChangedListener);
  }

  void _onMessageListChanged() {
    // 4. When the messageList is updating, get the new list and notify the UI layer
    // Key point: The complete list obtained here contains ALL historical messages
    messagesNotifier.value = barrageStore.barrageState.messageList.value;
  }

  void dispose() {
    barrageStore.barrageState.messageList.removeListener(_messageListChangedListener);
    messagesNotifier.dispose();
  }
}
```

### Step 3: Send Text Bullet Screen

Call the `sendTextMessage` method to broadcast a text message to all users in the live streaming room.
``` java
extension BarrageManagerSend on BarrageManager {
  Send a text bullet screen
  Future<void> sendTextMessage(String text) async {
    // Recommendation: Add non-null verification to avoid sending invalid messages.
    if (text.isEmpty) {
      debugPrint("Bullet screen content cannot be empty");
      return;
    }

    // Call the core API to sendMessage
    final result = await barrageStore.sendTextMessage(
      text: text,
      extensionInfo: null,
    );

    // Use isSuccess to check the result
    if (result.isSuccess) {
      debugPrint("Bullet screen text '$text' sent successfully");
    } else {
      debugPrint("Bullet screen text sending failure: ${result.errorMessage}");
    }
  }
}
```

**API parameter:**
<table>
<tr>
<td rowspan="1" colSpan="1" >**Parameter**</td>

<td rowspan="1" colSpan="1" >**Type**</td>

<td rowspan="1" colSpan="1" >**Description**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`text`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >The text content to be sent.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`extensionInfo`</td>

<td rowspan="1" colSpan="1" >`Map<String, String>?`</td>

<td rowspan="1" colSpan="1" >Attach extra extended information applicable to business customization.</td>
</tr>
</table>


### Step 4: Send Custom Barrage Item

Send a message containing custom business logic, such as gift, like or gaming interaction command. This message is transparent to other clients and requires the business layer to parse.
``` java
import 'dart:convert';

extension BarrageManagerCustom on BarrageManager {
  /// Send a custom barrage item, for example for sending a gift
  Future<void> sendGiftMessage({
    required String giftId,
    required int giftCount,
  }) async {
    // 1. Define a business ID
    const businessID = "live_gift";

    // 2. Encode business data as a JSON string
    final giftData = {"gift_id": giftId, "gift_count": giftCount};
    final jsonString = jsonEncode(giftData);

    // 3. Call the core API to send custom messages
    final result = await barrageStore.sendCustomMessage(
      businessID: businessID,
      data: jsonString,
    );

    if (result.isSuccess) {
      debugPrint("Gift message (custom barrage item) sent successfully");
    } else {
      debugPrint("Gift message send fail: ${result.errorMessage}");
    }
  }
}
```

**API parameter:**
<table>
<tr>
<td rowspan="1" colSpan="1" >**Parameter**</td>

<td rowspan="1" colSpan="1" >**Type**</td>

<td rowspan="1" colSpan="1" >**Description**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`businessID`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >Business unique identifier, such as "live_gift", used for recipient to distinguish different custom messages.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`data`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >Business data, typically strings in JSON format.</td>
</tr>
</table>


### Step 5: Insert Prompt Message Locally

Insert a local message into the current user's message list. This message will not be sent to other users in the live streaming room. It is suitable for displaying system welcome, warning or operation prompt information.
``` java
extension BarrageManagerLocal on BarrageManager {
  Insert a welcome notification into the local message list
  void showWelcomeMessage(LiveUserInfo user) {
    // 1. Create a Barrage message (using named parameters construct function)
    final welcomeTip = Barrage(
      messageType: BarrageType.text,
      Welcome ${user.userName} to the live room.
    );

    // 2. Call API to insert it into the local list
    barrageStore.appendLocalTip(welcomeTip);
  }
}
```

### Step 6: Manage User Speaking (Mute and Unblock)

As an Anchor or admin, you can manage the user speaking permission in the live streaming room to maintain a healthy communication environment.

#### Forbid/Unblock Single-User Speaking

Mute or unblock designated users can be achieved by the `disableSendMessage` API in `LiveAudienceStore`.
``` java
// 1. Get the LiveAudienceStore instance bound to the current live streaming room (location parameter)
final liveId = "your_live_id";
final audienceStore = LiveAudienceStore.create(liveId);

// 2. Define the operating user ID and mute status
final userIdToMute = "user_id_to_be_muted";
final shouldDisable = true; // true for mute, false for unblock

// 3. Call API to perform operation
final result = await audienceStore.disableSendMessage(
  userID: userIdToMute,
  isDisable: shouldDisable,
);

if (result.isSuccess) {
  debugPrint("${shouldDisable ? "mute" : "unblock"} user $userIdToMute successfully");
} else {
  debugPrint("Operation failure: ${result.errorMessage}");
}
```

#### Enable/Disable Global Mute

To mute all users in the live streaming room (normally excluding the Anchor), you need to update the live room information through `LiveListStore`.
``` java
// 1. Get the LiveListStore singleton
final liveListStore = LiveListStore.shared;

// 2. Get the current live room information, create a new LiveInfo object, and modify the global mute status
final currentLiveInfo = liveListStore.liveState.currentLive.value;
final updatedLiveInfo = LiveInfo(
  liveID: currentLiveInfo.liveID,
  liveName: currentLiveInfo.liveName,
  isMessageDisable: true, // true for mute all, false for shutdown
);

// 3. Call the update API and specify the modify flags list
final result = await liveListStore.updateLiveInfo(
  liveInfo: updatedLiveInfo,
  modifyFlagList: [ModifyFlag.isMessageDisable],
);

if (result.isSuccess) {
  debugPrint("Global mute status updated successfully");
} else {
  debugPrint("Operation failure: ${result.errorMessage}");
}
```

## Complete UI Example
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
        // Bullet screen list
        Expanded(
          child: ValueListenableBuilder<List<Barrage>>(
            valueListenable: _barrageManager.messagesNotifier,
            builder: (context, messageList, child) {
              // Scroll to the bottom
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
        // input box
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
                hintText: 'Say something...',
                border: OutlineInputBorder(),
                contentPadding: EdgeInsets.symmetric(horizontal: 12),
              ),
              onSubmitted: (_) => _sendMessage(),
            ),
          ),
          const SizedBox(width: 8),
          ElevatedButton(
            onPressed: _sendMessage,
            child: const Text('Send')
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

## Advanced Features: Optimizing Performance in High Concurrency Scenarios

After using `BarrageStore` to build the danmaku function, this chapter will guide you on how to handle more complex business scenarios, ensuring it can still provide users with a smooth and stable experience in real, complex high-concurrency live broadcasting scenarios. This chapter will focus on three core business scenarios, offering clear optimization schemes and example code.

### Scenario One: High-Concurrency Bullet Screen Scenario

#### Scenario Description

During a popular event, a large number of audience flooded into the live streaming room, with bullet screens updating at a frequency of dozens per second.

#### **Technical Challenge**

The SDK returns the complete bullet screen list at an extremely high frequency. Each time the UI is rebuilt, the main thread will be blocked by intensive UI layout and rendering operations, causing interface lag.

#### **Optimization Scheme: **Batch Processing & Traffic Peak Shaving

Do not respond to every data update, but set a time threshold (such as 300 ms). Only when the distance from the last UI refresh exceeds this threshold, execute the next refresh operation. This reduces UI redraws from dozens per second to 3-4 per second, significantly improving smoothness.
``` java
class BarrageUIManager {
  List<Barrage>? _latestMessageList;
  Timer? _refreshTimer;
  final void Function(List<Barrage>) onUpdate;

  BarrageUIManager({required this.onUpdate}) {
    // Check whether need to refresh every 0.3 seconds
    _refreshTimer = Timer.periodic(
      const Duration(milliseconds: 300),
      (_) => _refreshUIIfNeeded(),
    );
  }

  /// This method is frequently invoked externally with the latest full list
  void update(List<Barrage> fullList) {
    _latestMessageList = fullList;
  }

  void _refreshUIIfNeeded() {
    // Check whether there is new data pending refresh
    final newList = _latestMessageList;
    if (newList == null) return;

    _latestMessageList = null; // Clear flags to avoid repeated refresh
    
    // Update data source and refresh UI
    onUpdate(newList);
  }

  void dispose() {
    _refreshTimer?.cancel();
  }
}
```

### Scenario 2: Guarantee Memory Stability for Long-Term Live Stream

#### Scenario Description

Your application requires support for uninterrupted live streaming lasting several hours or even around the clock, such as game live broadcast or slow live streaming. During this period, the App must maintain stable operation and cannot exit unexpectedly due to long-running.

#### Technical Challenge

The full `messageList` returned by the SDK will grow infinitely during long-term live streams. Even if the UI layer implements traffic throttling, the huge array held by the data layer will continue to occupy memory, eventually causing the app to crash.

#### **Optimization Scheme**: Fixed Capacity Circular Buffer

**Only let your own data source (DataSource) hold a finite number of messages**. Regardless of how large the full list returned by the SDK is, your application only takes the latest part for display.
``` java
void _refreshUIIfNeeded() {
  final fullList = _latestMessageList;
  if (fullList == null) return;

  _latestMessageList = null;

  // Key point: Take the latest N messages
  const capacity = 500; // The client keeps the latest 500 messages only
  final cappedList = fullList.length > capacity 
      ? fullList.sublist(fullList.length - capacity)
      : fullList;

  onUpdate(cappedList);
}
```

## API documentation

For detailed information about ALL public interfaces, attributes, and methods of [BarrageStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_barrage_barrage_store/BarrageStore-class.html) and its related classes, see the official API documentation included with the [AtomicXCore](https://tencent-rtc.github.io/TUIKit_Flutter/index.html) framework.

## FAQs

### How to Achieve Various Bullet Screen Styles Such As Color Bullet Screen and Gift Bullet Screen

This is actually achieved by the custom message `sendCustomMessage`. `BarrageStore` does not limit your business imagination.

**Implementation Approach**
1. **Define data structure:** Work with your client and server team to define the JSON structure of custom messages. For example, a color bullet screen can be defined as follows:

   ``` json
   {  "type": "colored_text",  "text": "This is a color bullet screen!",  "color": "#FF5733" }
   ```
2. **Sender:** During sending, convert this JSON structure to a string and send it via the `data` parameter of `sendCustomMessage`. `businessId` can be set to a unique identifier representing your business, such as "`barrage_style_v1`".

3. **Receiver**: After receiving the Danmu Message, check whether its `messageType` is `.custom` and whether `businessId` matches. If matched, parse the `data` string (usually parsing JSON), and render your custom UI style based on the parsed data (such as `color, text`).


### Different Classes and Files Call `BarrageStore.create("some_id")`. Will This Create Multiple Instances and Cause Chaos?

No worries at all. `AtomicXCore`'s internal mechanism will underwrite that as long as the `liveId` passed in is identical, the `BarrageStore` instance obtained will always be the same one bound to the live streaming room. You can use it wherever required without manually managing the singleton.

### Why Call SendTextMessage but Can'T See Messages Sent in the Message List?

**Take the following steps to troubleshoot:**
1. **Check returned results**: The `sendTextMessage` method has a complete callback. Please check if the callback returned a successful status or failure. If unsuccessful, the error information will specify the issue (such as "You are muted", "network error").

2. **Confirm the timing of listening**: Underwrite your `barrageStore.state` subscription occurs after the `liveId` live stream starts. If you start listening before joining the live streaming room, you may miss some messages.

3. **Check liveId**: Confirm the `liveId` used when creating the `BarrageStore` instance, joining the live streaming room, and sending messages is the same, including case sensitivity.

4. **Network issue**: Check whether the current network connection of the device is normal. Sending messages depends on the network.


### How to Show New Audience the History Danmu Messages When They Enter the Live Room

`AtomicXCore` supports pulling history Danmu Messages, but this requires you to perform one simple configuration in the **server console**. Once configured, the SDK will automatically handle everything subsequently with no need to write additional code.

#### **Procedure 1: Perform Configuration in the Live Console**
1. Log in to the [**console > Live > Configuration**](https://console.trtc.io/live/configuration), and select the target application at the **top**.

2. On the Live configuration page, select **new member pull historical messages**, modify **new member viewable latest message count**, supports a maximum of **50**.

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032457995/f7e29319f76211f0831c52540073fd3b.png)


   **Step 2: Client Seamless Retrieval**


   After completing the above configuration, your client-side code **requires no modification**. 


   When a new user joins the live room, the `AtomicXCore` underlying layer will automatically pull your configuration history message count. These historical messages will be pushed to your UI layer through your realized `BarrageStore.barrageState` subscription channel, just like real-time messages. Your application will naturally receive and show these historical bullet screens, same as receiving real-time bullet screens.


