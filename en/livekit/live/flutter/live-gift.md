> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/en/llms.txt
> Use this file to discover all available pages before exploring further.

`GiftStore` is a module in `AtomicXCore` specialized in managing the gift function of live streaming rooms. With it, you can build a complete gift system for your live stream application to achieve various revenue and interactive scenarios.
<table>
<tr>
<td rowspan="1" colSpan="1" >**Gift Panel**</td>

<td rowspan="1" colSpan="1" >**Barrage Gift**</td>

<td rowspan="1" colSpan="1" >**Full-Screen Gift**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032457995/1b8d35def76311f0b34b525400ecee81.png)</td>

<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032457995/1a99ec96f76311f0831c52540073fd3b.png)</td>

<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032457995/26d1f324f76311f0859b52540097cba1.gif)</td>
</tr>
</table>


## Core Features
- **Gift List Retrieval**: Obtain the required data for the gift panel from the server, including gift categories and gift details.

- **Send a Gift**: The audience can send a selected gift to the Anchor with quantity.

- **Gift Event Broadcast**: Receive gift giveaway events inside the room in real time for showing gift animation and bullet screen notification.


## Core Concepts

Before starting integration, let's learn about several core concepts related to `GiftStore` in the following table:
<table>
<tr>
<td rowspan="1" colSpan="1" >**Core Concepts**</td>

<td rowspan="1" colSpan="1" >**Type**</td>

<td rowspan="1" colSpan="1" >**Core Responsibilities and Description**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[Gift](https://tencent-rtc.github.io/TUIKit_Flutter/api_gift_gift_store/Gift-class.html)</td>

<td rowspan="1" colSpan="1" >`class`</td>

<td rowspan="1" colSpan="1" >Represents a specific gift data model. It contains the gift ID, name, icon address, animation resource URL and price (coins).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[GiftCategory](https://tencent-rtc.github.io/TUIKit_Flutter/api_gift_gift_store/GiftCategory-class.html)</td>

<td rowspan="1" colSpan="1" >`class`</td>

<td rowspan="1" colSpan="1" >Represents a gift category, such as "popular" and "luxury". It contains the category name as well as the **Gift** list under this category.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[GiftState](https://tencent-rtc.github.io/TUIKit_Flutter/api_gift_gift_store/GiftState-class.html)</td>

<td rowspan="1" colSpan="1" >`class`</td>

<td rowspan="1" colSpan="1" >Represents the current status of the gift module. Its core attribute `usableGifts` is a `ValueListenable<List<GiftCategory>>`, storing the complete gift list fetched from the server.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[GiftListener](https://tencent-rtc.github.io/TUIKit_Flutter/api_gift_gift_store/GiftListener-class.html)</td>

<td rowspan="1" colSpan="1" >`class`</td>

<td rowspan="1" colSpan="1" >Gift event listener, receive gift giveaway event through the `onReceiveGift` callback. When anyone (including itself) sends a gift, all people in the room will receive this event.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[GiftStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_gift_gift_store/GiftStore-class.html)</td>

<td rowspan="1" colSpan="1" >`class`</td>

<td rowspan="1" colSpan="1" >This is the core management class for interacting with the gift function. Through it, you can fetch the gift list, send a gift, and receive gift events via `addGiftListener`.</td>
</tr>
</table>


## Implementation Steps

### Step 1: Integrating the Component

> **Note：**
> 

> To use the gifting system, activate either the **Free Trial,** or **Pro **edition. The number of configurable gifts depends on the selected package. For details, see the **Gift System** section in [Feature and Billing Description](https://write.woa.com/document/137771241658241024) and choose the package that fits your needs.
> 

- **Live streaming**: Refer to [Quick Access](https://write.woa.com/document/200455640177692672) for seamless integration with **AtomicXCore** and access completed.

- **Voice chat room**: Refer to [Quick Access](https://write.woa.com/document/200555778169073664) for seamless integration with **AtomicXCore** and access completed.


### Step 2: Initialize and Listen for Gift Events

Get the `GiftStore` instance and set a listener for receiving gifts and list update events.

#### Implementation Approach
1. **Get instance**: Use `GiftStore.create(liveId)` to get the `GiftStore` instance bound to the current live streaming room.

2. **Subscribe to events**: Add a gift event listener via `giftStore.addGiftListener(listener)`.

3. **Subscription status**: Listen to `giftStore.giftState.usableGifts` to get gift list updates.


#### Sample code:
``` java
import 'package:flutter/foundation.dart';
import 'package:atomic_x_core/atomicxcore.dart';

class GiftManager {
  final String liveId;
  late final GiftStore giftStore;
  late final GiftListener _giftListener;
  late final VoidCallback _giftListChangedListener = _onGiftListChanged;

  // Expose gift event callback externally
  void Function(String liveID, Gift gift, int count, LiveUserInfo sender)? onReceiveGift;

  // Expose the gift list externally
  ValueNotifier<List<GiftCategory>> giftListNotifier = ValueNotifier([]);

  GiftManager({required this.liveId}) {
    // 1. Get the instance of GiftStore by liveId
    giftStore = GiftStore.create(liveId);

    _subscribeToGiftState();
    _subscribeToGiftEvents();
  }

  /// 2. Subscribe to gift events
  void _subscribeToGiftEvents() {
    _giftListener = GiftListener(
      onReceiveGift: (liveID, gift, count, sender) {
        // After receiving the event, forward it to external processing
        onReceiveGift?.call(liveID, gift, count, sender);
      },
    );
    giftStore.addGiftListener(_giftListener);
  }

  /// 3. Subscribe to gift list status
  void _subscribeToGiftState() {
    giftStore.giftState.usableGifts.addListener(_giftListChangedListener);
  }

  void _onGiftListChanged() {
    giftListNotifier.value = giftStore.giftState.usableGifts.value;
  }

  // Call the dispose method to reclaim resources when exiting the live streaming room
  void dispose() {
    giftStore.removeGiftListener(_giftListener);
    giftStore.giftState.usableGifts.removeListener(_giftListChangedListener);
    giftListNotifier.dispose();
  }
}
```

#### Gift List Structure Parameter
- `GiftCategory`**Parameter description**

<table>
<tr>
<td rowspan="1" colSpan="1" >**Parameter**</td>

<td rowspan="1" colSpan="1" >**Type**</td>

<td rowspan="1" colSpan="1" >**Description**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`categoryID`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >Unique ID of the gift category.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`name`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >Display name of the gift category.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`desc`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >Description of the gift category.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`extensionInfo`</td>

<td rowspan="1" colSpan="1" >`Map<String, String>`</td>

<td rowspan="1" colSpan="1" >Extended information field.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`giftList`</td>

<td rowspan="1" colSpan="1" >`List<Gift>`</td>

<td rowspan="1" colSpan="1" >Array of Gift objects under this category.</td>
</tr>
</table>

- `Gift`**Parameter description**

<table>
<tr>
<td rowspan="1" colSpan="1" >**Parameter**</td>

<td rowspan="1" colSpan="1" >**Type**</td>

<td rowspan="1" colSpan="1" >**Description**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`giftID`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >Unique ID of the gift.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`name`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >Display name of the gift.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`desc`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >Description of the gift.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`iconURL`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >Icon URL of the gift.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`resourceURL`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >Resource URL of the gift animation.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`level`</td>

<td rowspan="1" colSpan="1" >`int`</td>

<td rowspan="1" colSpan="1" >Gift level.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`coins`</td>

<td rowspan="1" colSpan="1" >`int`</td>

<td rowspan="1" colSpan="1" >Gift price.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`extensionInfo`</td>

<td rowspan="1" colSpan="1" >`Map<String, String>`</td>

<td rowspan="1" colSpan="1" >Extended information field.</td>
</tr>
</table>


### Step 3: Obtain the Gift List

Call the `refreshUsableGifts` method to fetch gift data from the server.

#### Implementation Approach
1. **API call**: Call `giftStore.refreshUsableGifts()` at the appropriate timing (such as after entering the live room).

2. **Processing result**: Optionally process the returned results to fetch the pull results.

3. **Data reception**: After the update, the gift list is automatically received by listening to `giftStore.giftState.usableGifts` in procedure 2.


#### Sample code:
``` java
extension GiftManagerFetch on GiftManager {
  /// Refresh the gift list from the server
  Future<void> fetchGiftList() async {
    final result = await giftStore.refreshUsableGifts();
    if (result.isSuccess) {
      debugPrint("Gift list success message");
      // Upon success, the data is auto-updated via usableGifts listen
    } else {
      debugPrint("Gift list failed to pull: ${result.errorMessage}");
    }
  }
}
```

### Step 4: Sending a Gift

When a user selects a gift in the gift panel and clicks send, call the `sendGift` API to send the gift.

#### Implementation Approach
1. **Get parameter**: Obtain the giftID selected by the user and the number of messages sent (count) from the UI.

2. **API call**: Call `giftStore.sendGift(giftID:, count:)`.

3. **Processing result**: Handle failure cases (such as insufficient account balance notification) in the returned result. UI updates (animation, bullet screen) after successful sending should be event-driven by `onReceiveGift`.


#### Sample code:
``` java
extension GiftManagerSend on GiftManager {
  /// User sends a gift
  Future<void> sendGift(String giftID, int count) async {
    final result = await giftStore.sendGift(giftID: giftID, count: count);
    if (result.isSuccess) {
      debugPrint("Gift $giftID sent successfully");
      // After the message is sent successfully, everyone including the sender will receive the onReceiveGift event
    } else {
      debugPrint("Gift sending failed: ${result.errorMessage}");
      // You can prompt user here, such as "Insufficient balance" or "Network error"
    }
  }
}
```

#### `SendGift` API Parameter
<table>
<tr>
<td rowspan="1" colSpan="1" >**Parameter Name**</td>

<td rowspan="1" colSpan="1" >**Type**</td>

<td rowspan="1" colSpan="1" >**Description**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`giftID`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >Unique ID of the gift to send.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`count`</td>

<td rowspan="1" colSpan="1" >`int`</td>

<td rowspan="1" colSpan="1" >The number of sent.</td>
</tr>
</table>


## Advanced Features

`GiftStore` feature heavily depends on your business backend service. This chapter will guide you on how to build a feature-rich, outstanding experience interactive system through server configuration and client implementation.

### **Gift Material Configuration**

You need to customize the available gift type, category, name, icon, price, and animated effects in the live streaming room to meet operational needs and brand feature.

#### Implementation
1. **Server-Side Configuration**: Use the LiveKit server REST API to manage gift information, categories, and multi-language support. See the [Gift Configuration Guide](https://write.woa.com/document/185130564680273920).

2. **Client Fetch**: On the client, call `refreshUsableGifts` to retrieve configuration data.

3. **UI Display**: Use the retrieved `List<GiftCategory>` to render the gift panel.


#### Configuration Sequence Diagram

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032457995/3c7377bcf76311f0b34b525400ecee81.png)


#### Related REST API Interfaces Overview
<table>
<tr>
<td rowspan="1" colSpan="1" >**Interface Category**</td>

<td rowspan="1" colSpan="1" >**Interface**</td>

<td rowspan="1" colSpan="1" >**Request Example**</td>
</tr>

<tr>
<td rowspan="3" colSpan="1" >**​Gift Management**</td>

<td rowspan="1" colSpan="1" >Add Gift Information</td>

<td rowspan="1" colSpan="1" >[Example](https://write.woa.com/document/185130814885187584)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Delete Gift Information</td>

<td rowspan="1" colSpan="1" >[Example](https://write.woa.com/document/185131021432451072)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Query Gift Information</td>

<td rowspan="1" colSpan="1" >[Example](https://write.woa.com/document/185130925608591360)</td>
</tr>

<tr>
<td rowspan="3" colSpan="1" >**Gift Category Management**</td>

<td rowspan="1" colSpan="1" >Add Gift Category Information</td>

<td rowspan="1" colSpan="1" >[Example](https://write.woa.com/document/185131054187974656)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Delete Specific Gift Category Information</td>

<td rowspan="1" colSpan="1" >[Example](https://write.woa.com/document/185131288984932352)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Get Specific Gift Category Information</td>

<td rowspan="1" colSpan="1" >[Example](https://write.woa.com/document/185131164168736768)</td>
</tr>

<tr>
<td rowspan="3" colSpan="1" >**Gift Relationship Management**</td>

<td rowspan="1" colSpan="1" >Add Relationship between a Specific Gift Category and Gift</td>

<td rowspan="1" colSpan="1" >[Example](https://write.woa.com/document/185131388068356096)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Delete Relationship between a Specific Gift Category and Gift</td>

<td rowspan="1" colSpan="1" >[Example](https://write.woa.com/document/185131491225227264)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Get Gift Relationships under a Specific Gift Category</td>

<td rowspan="1" colSpan="1" >[Example](https://write.woa.com/document/185131634710056960)</td>
</tr>

<tr>
<td rowspan="6" colSpan="1" >**Gift Multi-language Management**</td>

<td rowspan="1" colSpan="1" >Add Gift Multi-language Information</td>

<td rowspan="1" colSpan="1" >[Example](https://write.woa.com/document/185131766094020608)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Delete Specific Gift Multi-language Information</td>

<td rowspan="1" colSpan="1" >[Example](https://write.woa.com/document/185132041665441792)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Get Gift Multi-language Information</td>

<td rowspan="1" colSpan="1" >[Example](https://write.woa.com/document/185131910582956032)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Add Gift Category Multi-language Information</td>

<td rowspan="1" colSpan="1" >[Example](https://write.woa.com/document/185132145524985856)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Delete Specific Gift Category Multi-language Information</td>

<td rowspan="1" colSpan="1" >[Example](https://write.woa.com/document/185132396568891392)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Get Gift Category Multi-language Information</td>

<td rowspan="1" colSpan="1" >[Example](https://write.woa.com/document/185132283123777536)</td>
</tr>
</table>


### Billing and Gift Sending Process

When the audience sends gifts, ensure sufficient account balance and complete the actual deduction before triggering the gift effect playback and broadcast.

#### Workflow
1. **Backend Callback Configuration**: Configure your billing system's callback URL in the LiveKit backend. See [Callback Configuration Documentation](https://write.woa.com/document/155612057789870080).

2. **Client Request**: The client calls `sendGift`.

3. **Backend Verification**: The LiveKit backend calls your callback URL; your billing system processes the deduction and returns the result.

4. **Result Synchronization**: If succeeds, **AtomicXCore** broadcasts the `onReceiveGift` event; if fails, the completion callback of `sendGift` receives an error.


#### Call Flow

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032457995/43b1ae0df76311f0ab675254001d6acc.png)


#### Related REST API Interfaces Overview
<table>
<tr>
<td rowspan="1" colSpan="1" >**Interface**</td>

<td rowspan="1" colSpan="1" >**Description**</td>

<td rowspan="1" colSpan="1" >**Request Example**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**Callback Configuration - Callback before sending a gift**</td>

<td rowspan="1" colSpan="1" >Pre-gifting validation hook. <br>Allows your backend to intercept gift requests to perform necessary checks (e.g., sufficient balance, risk control) before the gift is processed.</td>

<td rowspan="1" colSpan="1" >[Example](https://write.woa.com/document/183772991768039424)</td>
</tr>
</table>


### Play Full-Screen Gift Animation

When a user (including itself) sends luxury gifts such as "rocket" or "carnival" in the live streaming room, play a cool gift animation (for example, SVGA animation) in full-screen playback to create a lively communication environment.

#### Implementation

`AtomicXCore` itself does not include a gift animation player. You need to select and integrate a third-party library based on business requirements. The following is a comparison of two solutions:
<table>
<tr>
<td rowspan="1" colSpan="1" >**Comparison Item**</td>

<td rowspan="1" colSpan="1" >**Basic Solution (Svgaplayer_flutter)**</td>

<td rowspan="1" colSpan="1" >**Advanced Plan (TCEffectPlayerKit)**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Billing</td>

<td rowspan="1" colSpan="1" >Free (open-source library)</td>

<td rowspan="1" colSpan="1" >Paid (License purchase required), please see [Payment Guide](https://trtc.io/document/69949?product=beautyar&menulabel=core%20sdk&platform=android#X-Series-Capabilities)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Integration Method</td>

<td rowspan="1" colSpan="1" >Manual integration of the [svgaplayer_flutter](https://pub.dev/packages/svgaplayer_flutter) library is required.</td>

<td rowspan="1" colSpan="1" >Additional integration of the [flutter_effect_player](https://github.com/Tencent-RTC/EffectPlayer_Flutter) library and authentication are required.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Animation Format Support</td>

<td rowspan="1" colSpan="1" >SVGA only</td>

<td rowspan="1" colSpan="1" >SVGA, PAG, WebP, Lottie, MP4, and other formats</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Performance</td>

<td rowspan="1" colSpan="1" >Recommend SVGA files ≤ 10MB</td>

<td rowspan="1" colSpan="1" >Support larger animation files, better performance for complex effects, multi-animation concurrency, and low-end devices</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Recommended scenarios</td>

<td rowspan="1" colSpan="1" >Gift animation format is unified as SVGA with controllable file size</td>

<td rowspan="1" colSpan="1" >Support multiple animation formats or higher performance/compatibility requirements</td>
</tr>
</table>


This section demonstrates the basic solution. If you select the advanced plan, refer to [EffectPlayer Flutter integration guide](https://trtc.io/document/73975?product=beautyar&menulabel=core%20sdk&platform=flutter).

#### Basic Solution Implementation: Use Svgaplayer_flutter
1. **Integrate svgaplayer_flutter**: In your `pubspec.yaml` file, add dependency and run `flutter pub get`.

   ``` yaml
   dependencies:
     svgaplayer_flutter: ^2.0.0
   ```
2. **Listen for gift events**: Add a listener via `GiftStore`'s `addGiftListener`.

3. **Parse and play**: When the `onReceiveGift` event is received, check if `gift.resourceURL` is valid and points to an SVGA file. If so, use `SVGAAnimationController` to play the animation.


#### Sample Code
``` java
import 'package:flutter/material.dart';
import 'package:atomic_x_core/atomicxcore.dart';
import 'package:svgaplayer_flutter/svgaplayer_flutter.dart';

class LiveRoomWidget extends StatefulWidget {
  final String liveId;
  const LiveRoomWidget({Key? key, required this.liveId}) : super(key: key);

  @override
  State<LiveRoomWidget> createState() => _LiveRoomWidgetState();
}

class _LiveRoomWidgetState extends State<LiveRoomWidget> with SingleTickerProviderStateMixin {
  late GiftManager giftManager;

  // SVGA player
  late SVGAAnimationController _svgaController;
  bool _showAnimation = false;

  @override
  void initState() {
    super.initState();
    _svgaController = SVGAAnimationController(vsync: this);
    _setupGiftSubscription();
  }

  void _setupGiftSubscription() {
    giftManager = GiftManager(liveId: widget.liveId);

    giftManager.onReceiveGift = (liveID, gift, count, sender) {
      if (gift.resourceURL.isNotEmpty) {
        _playAnimation(gift.resourceURL);
      }
    };
  }

  Future<void> _playAnimation(String url) async {
    try {
      final videoItem = await SVGAParser.shared.decodeFromURL(url);
      _svgaController.videoItem = videoItem;
      setState(() {
        _showAnimation = true;
      });
      _svgaController.forward().whenComplete(() {
        setState(() {
          _showAnimation = false;
        });
      });
    } catch (e) {
      debugPrint("SVGA animation parsing failure: $e");
    }
  }

  @override
  void dispose() {
    _svgaController.dispose();
    giftManager.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Stack(
      children: [
        // Live stream
        // ...

        // Full-Screen Gift Animation
        if (_showAnimation)
          Positioned.fill(
            child: SVGAImage(_svgaController),
          ),
      ],
    );
  }
}
```

### Show Gift Giveaway Messages in the Bullet Screen Area

When a user sends a gift, it not only plays the animation but also displays a system message in the on-screen comment area, such as "[Nickname] sent [gift name] x [quantity]", so all audience can see.

#### Implementation Method
1. **Listen for events**: Add a listener via `giftStore.addGiftListener`.

2. **Obtain information**: After the `onReceiveGift` event is received, extract the sender, gift, and count.

3. **Retrieve the bullet screen Store**: Use `BarrageStore.create(liveId)` to get the instance bound to the current room.

4. **Concatenate messages**: Create a `Barrage` object, set `messageType = BarrageType.text`, and `textContent` as the concatenated string (such as "[`sender.userName`] sent [`gift.name`] x [`count`]").

5. **Local insertion**: Call `barrageStore.appendLocalTip(giftTip)` to insert the message into the local list.


#### Sample Code
``` java
// In LiveRoomManager or similar top-level managers
void _setupGiftToBarrageFlow() {
  final giftStore = GiftStore.create(liveId);
  final barrageStore = BarrageStore.create(liveId);

  final giftListener = GiftListener(
    onReceiveGift: (liveID, gift, count, sender) {
      // Concatenate the message
      final tipText = "${sender.userName} sent ${gift.name} x $count";
      final giftTip = Barrage(
        messageType: BarrageType.text,
        textContent: tipText,
      );
      // Optional: Set a special sender

      // local insertion
      barrageStore.appendLocalTip(giftTip);
    },
  );

  giftStore.addGiftListener(giftListener);
}
```

## API documentation

For detailed information about all public interfaces, attributes, and methods of [GiftStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_gift_gift_store/GiftStore-class.html) and its related classes, see the official API documentation of the [AtomicXCore](https://tencent-rtc.github.io/TUIKit_Flutter/index.html) framework. The related Stores used in this guide are as follows:
<table>
<tr>
<td rowspan="1" colSpan="1" >**Store/Component**</td>

<td rowspan="1" colSpan="1" >**Feature Description**</td>

<td rowspan="1" colSpan="1" >**API Reference**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**GiftStore**</td>

<td rowspan="1" colSpan="1" >Gift interaction: Get gift list, send/receive gifts, listen to gift events (including sender, gift details).</td>

<td rowspan="1" colSpan="1" >[API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_gift_gift_store/GiftStore-class.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**BarrageStore**</td>

<td rowspan="1" colSpan="1" >Danmaku function: send text / custom barrage item, maintain bullet screen list, monitor in real time.</td>

<td rowspan="1" colSpan="1" >[API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_barrage_barrage_store/BarrageStore-class.html)</td>
</tr>
</table>


## FAQs

### `GiftStore` Gift List Is Empty. What Should Be Done?

You must actively call `refreshUsableGifts()` to fetch gift data from your backend. These gift data need to be configured in your backend via server-side REST API.

### How to Achieve Multilingual Gift Display (Such As Chinese, English)

`GiftStore` provides the `setLanguage(String language)` API. You can call this method before `refreshUsableGifts`, input the target language code (such as "en" or "zh-CN"). The server will return the gift name and description in the corresponding language based on this language code.

### I Called SendGift to Send the Gift, Why Did the Gift Animation Repeat Playback Twice?

`onReceiveGift` is a broadcast to all members in the room (including the sender). If you perform a UI operation in the success callback of `sendGift`, and simultaneously execute the same UI operation in the `onReceiveGift` callback, it can lead to duplication.
- **Best practice**: UI updates (such as playing animation, bullet screen notification) should only be handled in the callback of the `onReceiveGift` event. The returned results of `sendGift` are only used to process the logic of sending failure (such as prompting the user "sending failure" or "insufficient balance").


### Where Is the Gift Charge Logic Implemented?

The gift charge logic is fully handled by your self-built billing system. `AtomicXCore` connects with your billing system through a backend callback mechanism. The client calls `sendGift` to trigger the callback. After your backend service completes the charge, it returns the result to the `AtomicXCore` backend, thereby determining whether to broadcast the gift event.

### Will Gift Sending Notifications Be Muted or Blocked by Frequency Control?

No. Gift sending notifications (`onReceiveGift` event) are not affected by muting or message frequency control, ensuring reliable delivery.

### What to Do About Playback Lag in Gift Animation

Please check your SVGA file size. Player SDKs recommend not exceeding 10MB. If the file is too large or the animation is complex, you can consider seamless integration with the advanced effect player provided by TUILiveKit to get better performance.

