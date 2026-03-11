> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

**AtomicXCore** provided [CoHostStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_co_host_store/CoHostStore-class.html) and [BattleStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_battle_store/BattleStore-class.html), two core modules used to process **cross-room connection and PK battle**. This document will guide you on how to use these two tools in combination to complete the complete process from connecting line to PK in live broadcasting scenario.

## Core Scenario

A complete "anchor connection PK" usually consists of three core stages, and the overall process is as follows:

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032457995/635c0bc0f76111f0b34b525400ecee81.png)


## Implementation Steps

### Step 1: Integrating the Component

Refer to [Quick Connection](https://write.woa.com/document/200455640177692672) for seamless integration with **AtomicXCore** and complete **LiveCoreWidget** access.

### Step 2: Implementing Cross-Room Connection

The goal of this step is to have two Anchors appear in the same view, and we will use [CoHostStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_co_host_store/api_live_co_host_store-library.html) to complete it.

#### Inviter (Anchor A) Implementation
1. **Initiate connection invitation**


   When Anchor A selects target Anchor B on the interface and initiates connecting line, call the `requestHostConnection` method.

   ``` java
   import 'package:atomic_x_core/atomicxcore.dart';
   
   // Anchor A's webpage
   class AnchorAPage extends StatefulWidget {
     final String liveId;
   
     const AnchorAPage({Key? key, required this.liveId}) : super(key: key);
   
     @override
     State<AnchorAPage> createState() => _AnchorAPageState();
   }
   
   class _AnchorAPageState extends State<AnchorAPage> {
     late final CoHostStore _coHostStore;
     late final CoHostListener _coHostListener;
   
     @override
     void initState() {
       super.initState();
       _coHostStore = CoHostStore.create(widget.liveId);
       _setupListeners();
     }
   
     // User clicks the "connecting line" button and selected Anchor B
     Future<void> inviteHostB(String targetHostLiveId) async {
       final layout = CoHostLayoutTemplate.hostDynamicGrid; // Select a layout template
       const timeout = 30; // Invitation timeout duration (seconds)
   
       final result = await _coHostStore.requestHostConnection(
         targetHostLiveID: targetHostLiveId,
         layoutTemplate: layout,
         timeout: timeout,
       );
   
       if (result.isSuccess) {
         print('Connection invitation sent, waiting for peer to handle...');
       } else {
         print('Invitation sending failure: ${result.errorMessage}');
       }
     }
   
     @override
     void dispose() {
       _coHostStore.removeCoHostListener(_coHostListener);
       super.dispose();
     }
   }
   ```
2. **Listen for invitation result**


   Through `CoHostListener`, you can receive the Anchor B's processing result.

   ``` java
   // Set up monitoring when initializing _AnchorAPageState
   void _setupListeners() {
     _coHostListener = CoHostListener(
       onCoHostRequestAccepted: (invitee) {
         print('Anchor ${invitee.userName} granted your connection invitation');
       },
       onCoHostRequestRejected: (invitee) {
         print('Anchor ${invitee.userName} refused your invitation');
       },
       onCoHostRequestTimeout: (inviter, invitee) {
         print('Invitation timeout, no response from the other party');
       },
       onCoHostUserJoined: (userInfo) {
         print('Anchor ${userInfo.userName} joined the connecting line');
       },
       onCoHostUserLeft: (userInfo) {
         print('Anchor ${userInfo.userName} left the connecting line');
       },
     );
     _coHostStore.addCoHostListener(_coHostListener);
   }
   ```

#### Invitee (Anchor B) Implementation
1. **Receive connection invitation**


   Through `CoHostListener`, Anchor B can listen to the invitation from Anchor A.

   ``` java
   import 'package:atomic_x_core/atomicxcore.dart';
   
   // Anchor B's webpage
   class AnchorBPage extends StatefulWidget {
     final String liveId;
   
     const AnchorBPage({Key? key, required this.liveId}) : super(key: key);
   
     @override
     State<AnchorBPage> createState() => _AnchorBPageState();
   }
   
   class _AnchorBPageState extends State<AnchorBPage> {
     late final CoHostStore _coHostStore;
     late final CoHostListener _coHostListener;
   
     @override
     void initState() {
       super.initState();
       _coHostStore = CoHostStore.create(widget.liveId);
       _setupListeners();
     }
   
     // Set up monitoring during initialization
     void _setupListeners() {
       _coHostListener = CoHostListener(
         onCoHostRequestReceived: (inviter, extensionInfo) {
           print('Received connection invitation from Anchor ${inviter.userName}');
           // _showInvitationDialog(inviter);
         },
       );
       _coHostStore.addCoHostListener(_coHostListener);
     }
   
     @override
     void dispose() {
       _coHostStore.removeCoHostListener(_coHostListener);
       super.dispose();
     }
   }
   ```
2. **Respond to connection invitation**


   When Anchor B makes a selection in the pop-up dialog box, call the method accordingly.

   ``` java
   // Part of _AnchorBPageState
   Future<void> acceptInvitation(String fromHostLiveId) async {
     final result = await _coHostStore.acceptHostConnection(fromHostLiveId);
     if (result.isSuccess) {
       print('Connection invitation accepted');
     } else {
       print('Connection acceptance failure: ${result.errorMessage}');
     }
   }
   
   Future<void> rejectInvitation(String fromHostLiveId) async {
     final result = await _coHostStore.rejectHostConnection(fromHostLiveId);
     if (result.isSuccess) {
       print('Connection invitation denied');
     } else {
       print('Connection rejection failure: ${result.errorMessage}');
     }
   }
   ```

### Step 3: Implement Anchor PK

Upon success of the connecting line, either party can initiate PK. This step will be achieved by using [BattleStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_battle_store/BattleStore-class.html) to implement Anchor PK.

#### Challenger (Such As Anchor A) Implementation
1. **Initiate PK challenge**


   When Anchor A clicks the "PK" button, call the `requestBattle` method.

   ``` java
   // Part of _AnchorAPageState
   late final BattleStore _battleStore;
   late final BattleListener _battleListener;
   
   @override
   void initState() {
     super.initState();
     _coHostStore = CoHostStore.create(widget.liveId);
     _battleStore = BattleStore.create(widget.liveId);
     _setupListeners();
     _setupBattleListeners();
   }
   
   Future<void> startPK(String opponentUserId) async {
     final config = BattleConfig(duration: 300); // PK lasts 5 minutes
     final result = await _battleStore.requestBattle(
       config: config,
       userIDList: [opponentUserId],
       timeout: 30,
     );
   
     if (result.isSuccess) {
       print('Battle request sent, battleID: ${result.battleID}');
     } else {
       print('PK request failure: ${result.errorMessage}');
     }
   }
   ```
2. **Listen for PK status**


   Listen for key events such as PK start and end via `BattleListener`.

   ``` java
   // Add to the _setupBattleListeners method in _AnchorAPageState
   void _setupBattleListeners() {
     _battleListener = BattleListener(
       onBattleStarted: (battleInfo, inviter, invitees) {
         print('PK started');
       },
       onBattleEnded: (battleInfo, reason) {
         print('PK ended, reason: $reason');
       },
       onUserJoinBattle: (battleID, battleUser) {
         print('User ${battleUser.userName} joined PK');
       },
       onUserExitBattle: (battleID, battleUser) {
         print('User ${battleUser.userName} left the PK');
       },
     );
     _battleStore.addBattleListener(_battleListener);
   }
   
   @override
   void dispose() {
     _coHostStore.removeCoHostListener(_coHostListener);
     _battleStore.removeBattleListener(_battleListener);
     super.dispose();
   }
   ```

#### Challenger (Anchor B) Implementation
1. **Accept PK challenge**


   Listen for PK invitation via `BattleListener`.

   ``` java
   // Add to the _setupBattleListeners method in _AnchorBPageState
   void _setupBattleListeners() {
     _battleListener = BattleListener(
       onBattleRequestReceived: (battleId, inviter, invitee) {
         print('Received PK challenge from Anchor ${inviter.userName}');
         // Display a pop-up dialog box for Anchor B to select "Agree" or "Reject"
         // _showPKChallengeDialog(battleId);
       },
       onBattleStarted: (battleInfo, inviter, invitees) {
         print('PK started');
       },
       onBattleEnded: (battleInfo, reason) {
         print('PK ended');
       },
     );
     _battleStore.addBattleListener(_battleListener);
   }
   ```
2. **Respond to PK challenge**


   When Anchor B makes a selection, call the appropriate method.

   ``` java
   // Part of _AnchorBPageState
   // User click "Accept Challenge"
   Future<void> acceptPK(String battleId) async {
     final result = await _battleStore.acceptBattle(battleId);
     if (result.isSuccess) {
       print('PK challenge accepted');
     } else {
       print('PK acceptance failure: ${result.errorMessage}');
     }
   }
   
   // User click "Reject Challenge"
   Future<void> rejectPK(String battleId) async {
     final result = await _battleStore.rejectBattle(battleId);
     if (result.isSuccess) {
       print('PK challenge denied');
     } else {
       print('PK rejection failure: ${result.errorMessage}');
     }
   }
   ```

### Execution Effect

After integrating the above feature implementation, perform the corresponding operation using Anchor A and Anchor B separately. The execution effect is as follows. You can refer to the next chapter [Refine UI Detail](https://write.woa.com/#.E5.AE.8C.E5.96.84-ui-.E7.BB.86.E8.8A.82) to customize UI logic.

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032457995/71fcc39af76111f0ab675254001d6acc.png)


## Refine UI Detail

You can use the "slot" capacity provided by the `VideoWidgetBuilder` parameter of `LiveCoreWidget` to add custom view on top of the video stream image for displaying nickname, avatar, PK progress bar, etc., or provide placeholder image when they turn camera off to optimize visual experience.

### Implementing Nickname Display on Video Stream Image

#### Effect

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032457995/7c936e67f76111f0b34b525400ecee81.png)


#### Implementation Method
- **Step 1**: Create a foreground view (**CustomCoHostForegroundView**) to display user information above the video stream.
   

   > **Note:**
   > 

   > You can also refer to the [co_host_foreground_widget.dart](https://github.com/Tencent-RTC/TUIKit_Flutter/blob/main/live/livekit/lib/live_stream/features/decorations/co_host/co_host_foreground_widget.dart) and [co_host_background_widget.dart](https://github.com/Tencent-RTC/TUIKit_Flutter/blob/main/live/livekit/lib/live_stream/features/decorations/co_host/co_host_background_widget.dart) files in the TUILiveKit open-source project to understand the complete implementation logic.
   > 

   ``` java
   import 'package:flutter/material.dart';
   import 'package:rtc_room_engine/rtc_room_engine.dart';
   
   /// Custom connected host message floating view (foreground)
   class CustomCoHostForegroundView extends StatelessWidget {
     final SeatFullInfo seatInfo;
   
     const CustomCoHostForegroundView({
       Key? key, 
       required this.seatInfo,
     }) : super(key: key);
   
     @override
     Widget build(BuildContext context) {
       return Container(
         color: Colors.transparent,
         child: Align(
           alignment: Alignment.bottomLeft,
           child: Container(
             margin: const EdgeInsets.all(5.0),
             padding: const EdgeInsets.symmetric(horizontal: 8, vertical: 4),
             decoration: BoxDecoration(
               color: Colors.black.withOpacity(0.5),
               borderRadius: BorderRadius.circular(12),
             ),
             child: Text(
               seatInfo.userInfo.userName,
               style: const TextStyle(
                 color: Colors.white,
                 fontSize: 14,
               ),
             ),
           ),
         ),
       );
     }
   }
   ```
- **Step 2**: Create a background view (**CustomCoHostBackgroundView**) to display a placeholder image when there is no video stream from the user.

   ``` java
   import 'package:flutter/material.dart';
   import 'package:rtc_room_engine/rtc_room_engine.dart';
   
   /// Custom connected anchor avatar placeholder view (background)
   class CustomCoHostBackgroundView extends StatelessWidget {
     final SeatFullInfo seatInfo;
   
     const CustomCoHostBackgroundView({
       Key? key, 
       required this.seatInfo,
     }) : super(key: key);
   
     @override
     Widget build(BuildContext context) {
       final avatarUrl = seatInfo.userInfo.avatarUrl;
       return Container(
         decoration: BoxDecoration(
           color: Colors.grey[800],
         ),
         child: Center(
           child: Column(
             mainAxisSize: MainAxisSize.min,
             children: [
               ClipOval(
                 child: avatarUrl.isNotEmpty
                     ? Image.network(
                         avatarUrl,
                         width: 60,
                         height: 60,
                         fit: BoxFit.cover,
                         errorBuilder: (context, error, stackTrace) {
                           return _buildDefaultAvatar();
                         },
                       )
                     : _buildDefaultAvatar(),
               ),
               const SizedBox(height: 8),
               Text(
                 seatInfo.userInfo.userName,
                 style: const TextStyle(
                   color: Colors.white,
                   fontSize: 12,
                 ),
               ),
             ],
           ),
         ),
       );
     }
   
     Widget _buildDefaultAvatar() {
       return Container(
         width: 60,
         height: 60,
         color: Colors.grey,
         child: const Icon(Icons.person, size: 40, color: Colors.white),
       );
     }
   }
   ```
- **Step 3**: Build a custom view through the `VideoWidgetBuilder`'s `coHostWidgetBuilder` callback, and return the corresponding view based on the `viewLayer` value.

   ``` java
   import 'package:flutter/material.dart';
   import 'package:atomic_x_core/atomicxcore.dart';
   import 'package:rtc_room_engine/rtc_room_engine.dart';
   
   /// Live streaming page with custom connection view
   class CustomCoHostLiveWidget extends StatefulWidget {
     final String liveId;
   
     const CustomCoHostLiveWidget({
       Key? key, 
       required this.liveId,
     }) : super(key: key);
   
     @override
     State<CustomCoHostLiveWidget> createState() => _CustomCoHostLiveWidgetState();
   }
   
   class _CustomCoHostLiveWidgetState extends State<CustomCoHostLiveWidget> {
     late LiveCoreController _controller;
   
     @override
     void initState() {
       super.initState();
       _controller = LiveCoreController.create();
       _controller.setLiveID(widget.liveId);
     }
   
     @override
     void dispose() {
       _controller.dispose();
       super.dispose();
     }
   
     /// Build a custom view for the connected host
     Widget _buildCoHostWidget(
       BuildContext context, 
       SeatFullInfo seatFullInfo, 
       ViewLayer viewLayer,
     ) {
       if (viewLayer == ViewLayer.foreground) {
         // Foreground layer: Always display on top of the video image for Nickname, information, etc.
         return CustomCoHostForegroundView(seatInfo: seatFullInfo);
       } else {
         // Background layer: Display only when the corresponding user has no video stream, used for avatar placeholder image
         return CustomCoHostBackgroundView(seatInfo: seatFullInfo);
       }
     }
   
     @override
     Widget build(BuildContext context) {
       return Scaffold(
         body: LiveCoreWidget(
           controller: _controller,
           videoWidgetBuilder: VideoWidgetBuilder(
             coHostWidgetBuilder: _buildCoHostWidget,
           ),
         ),
       );
     }
   }
   ```

#### **Parameter description:**
<table>
<tr>
<td rowspan="1" colSpan="1" >**Parameter**</td>

<td rowspan="1" colSpan="1" >**Type**</td>

<td rowspan="1" colSpan="1" >**Note**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`seatFullInfo`</td>

<td rowspan="1" colSpan="1" >`SeatFullInfo`</td>

<td rowspan="1" colSpan="1" >Seat information object, containing the Anchor's detailed information</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`seatFullInfo.userInfo.userId`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >Anchor's user ID</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`seatFullInfo.userInfo.userName`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >Anchor's Nickname</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`seatFullInfo.userInfo.avatarUrl`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >Anchor's profile photo URL</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`viewLayer`</td>

<td rowspan="1" colSpan="1" >`ViewLayer`</td>

<td rowspan="1" colSpan="1" >View hierarchy enumeration<br>`ViewLayer.foreground` refers to the pendant view in the foreground, always displayed on top of the video image.<br>`ViewLayer.background` refers to the pendant view in the background, located in the lower layer of the foreground view. It is only displayed when the corresponding user has no video stream (such as when the camera is off), usually used for displaying the default avatar or placeholder image.</td>
</tr>
</table>


### Implementing Score Display for PK User View

When the Anchor starts PK, you can mount a custom view on the other party's video footage, usually used for showing the value of gifts received or other PK-related information.

#### **Effect**

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032457995/c3973bd3f76111f0ab675254001d6acc.png)


#### Implementation Method
- **Step 1**: Create a custom PK user view. You can refer to the [battle_member_info_widget.dart](https://github.com/Tencent-RTC/TUIKit_Flutter/blob/main/live/livekit/lib/live_stream/features/decorations/battle/battle_member_info_widget.dart) file in the TUILiveKit open-source project to learn about the complete implementation logic.

   ``` java
   import 'package:flutter/material.dart';
   import 'package:atomic_x_core/atomicxcore.dart';
   import 'package:rtc_room_engine/rtc_room_engine.dart';
   
   /// Custom PK User View
   class CustomBattleUserView extends StatefulWidget {
     final String liveId;
     final TUIBattleUser battleUser;
   
     const CustomBattleUserView({
       Key? key,
       required this.liveId,
       required this.battleUser,
     }) : super(key: key);
   
     @override
     State<CustomBattleUserView> createState() => _CustomBattleUserViewState();
   }
   
   class _CustomBattleUserViewState extends State<CustomBattleUserView> {
     late final BattleStore _battleStore;
     late final VoidCallback _scoreChangedListener = _onScoreChanged;
     int _score = 0;
   
     @override
     void initState() {
       super.initState();
       _battleStore = BattleStore.create(widget.liveId);
       _subscribeBattleState();
     }
   
     /// Subscribe to PK score changes
     void _subscribeBattleState() {
       _battleStore.battleState.battleScore.addListener(_scoreChangedListener);
       // Initialize the score
       _updateScore(_battleStore.battleState.battleScore.value);
     }
   
     void _onScoreChanged() {
       _updateScore(_battleStore.battleState.battleScore.value);
     }
   
     void _updateScore(Map<String, int> battleScore) {
       final score = battleScore[widget.battleUser.userId] ?? 0;
       if (mounted && score != _score) {
         setState(() {
           _score = score;
         });
       }
     }
   
     @override
     void dispose() {
       _battleStore.battleState.battleScore.removeListener(_scoreChangedListener);
       super.dispose();
     }
   
     @override
     Widget build(BuildContext context) {
       return IgnorePointer(
         child: Align(
           alignment: Alignment.bottomRight,
           child: Container(
             margin: const EdgeInsets.all(5),
             padding: const EdgeInsets.symmetric(horizontal: 8, vertical: 4),
             decoration: BoxDecoration(
               color: Colors.black.withOpacity(0.4),
               borderRadius: BorderRadius.circular(12),
             ),
             child: Text(
               '$_score',
               style: const TextStyle(
                 color: Colors.white,
                 fontSize: 14,
                 fontWeight: FontWeight.bold,
               ),
             ),
           ),
         ),
       );
     }
   }
   ```
- **Step 2**: Build a custom PK view through the `battleWidgetBuilder` callback of `VideoWidgetBuilder`.

   ``` java
   import 'package:flutter/material.dart';
   import 'package:atomic_x_core/atomicxcore.dart';
   import 'package:rtc_room_engine/rtc_room_engine.dart';
   
   Live streaming page with custom PK view
   class CustomBattleLiveWidget extends StatefulWidget {
     final String liveId;
   
     const CustomBattleLiveWidget({
       Key? key, 
       required this.liveId,
     }) : super(key: key);
   
     @override
     State<CustomBattleLiveWidget> createState() => _CustomBattleLiveWidgetState();
   }
   
   class _CustomBattleLiveWidgetState extends State<CustomBattleLiveWidget> {
     late LiveCoreController _controller;
   
     @override
     void initState() {
       super.initState();
       _controller = LiveCoreController.create();
       _controller.setLiveID(widget.liveId);
     }
   
     @override
     void dispose() {
       _controller.dispose();
       super.dispose();
     }
   
     /// Build Custom PK User View
     Widget _buildBattleWidget(BuildContext context, TUIBattleUser battleUser) {
       return CustomBattleUserView(
         liveId: widget.liveId,
         battleUser: battleUser,
       );
     }
   
     @override
     Widget build(BuildContext context) {
       return Scaffold(
         body: LiveCoreWidget(
           controller: _controller,
           videoWidgetBuilder: VideoWidgetBuilder(
             battleWidgetBuilder: _buildBattleWidget,
           ),
         ),
       );
     }
   }
   ```

#### **Parameter description:**
<table>
<tr>
<td rowspan="1" colSpan="1" >**Parameter**</td>

<td rowspan="1" colSpan="1" >**Type**</td>

<td rowspan="1" colSpan="1" >**Note**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`battleUser`</td>

<td rowspan="1" colSpan="1" >`TUIBattleUser`</td>

<td rowspan="1" colSpan="1" >PK user information object.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`battleUser.roomId`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >PK room ID.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`battleUser.userId`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >PK user ID.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`battleUser.userName`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >PK user nickname.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`battleUser.avatarUrl`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >PK user avatar address.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`battleUser.score`</td>

<td rowspan="1" colSpan="1" >`int`</td>

<td rowspan="1" colSpan="1" >PK score.</td>
</tr>
</table>


### Displaying PK Status on Video Stream Image

#### **Effect**

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032457995/73387fddf76211f0859b52540097cba1.png)


#### **Implementation Method**
- **Step 1:** Create a custom PK global view **CustomBattleContainerView**. You can refer to the [battle_info_widget.dart](https://github.com/Tencent-RTC/TUIKit_Flutter/blob/main/live/livekit/lib/live_stream/features/decorations/battle/battle_info_widget.dart) file in the TUILiveKit open-source project to achieve the same effect.

- **Step 2**: Build a custom PK container view through the `battleContainerWidgetBuilder` callback of `VideoWidgetBuilder`.

   ``` java
   import 'package:flutter/material.dart';
   import 'package:atomic_x_core/atomicxcore.dart';
   
   Live streaming page with custom PK container view
   class CustomBattleContainerLiveWidget extends StatefulWidget {
     final String liveId;
   
     const CustomBattleContainerLiveWidget({
       Key? key, 
       required this.liveId,
     }) : super(key: key);
   
     @override
     State<CustomBattleContainerLiveWidget> createState() => _CustomBattleContainerLiveWidgetState();
   }
   
   class _CustomBattleContainerLiveWidgetState extends State<CustomBattleContainerLiveWidget> {
     late LiveCoreController _controller;
   
     @override
     void initState() {
       super.initState();
       _controller = LiveCoreController.create();
       _controller.setLiveID(widget.liveId);
     }
   
     @override
     void dispose() {
       _controller.dispose();
       super.dispose();
     }
   
     /// Build PK Container View
     Widget _buildBattleContainerWidget(BuildContext context) {
       // CustomBattleContainerView is your custom PK global view
       return CustomBattleContainerView(liveId: widget.liveId);
     }
   
     @override
     Widget build(BuildContext context) {
       return Scaffold(
         body: LiveCoreWidget(
           controller: _controller,
           videoWidgetBuilder: VideoWidgetBuilder(
             battleContainerWidgetBuilder: _buildBattleContainerWidget,
           ),
         ),
       );
     }
   }
   ```

### Combine Multiple Custom Views

In actual scenarios, you may need to customize the connected host view, PK user view, and PK container view at the same time. The following example shows how to use them in combination.
``` java
import 'package:flutter/material.dart';
import 'package:atomic_x_core/atomicxcore.dart';
import 'package:rtc_room_engine/rtc_room_engine.dart';

/// Complete custom view live streaming page
class FullCustomLiveWidget extends StatefulWidget {
  final String liveId;

  const FullCustomLiveWidget({
    Key? key, 
    required this.liveId,
  }) : super(key: key);

  @override
  State<FullCustomLiveWidget> createState() => _FullCustomLiveWidgetState();
}

class _FullCustomLiveWidgetState extends State<FullCustomLiveWidget> {
  late LiveCoreController _controller;

  @override
  void initState() {
    super.initState();
    _controller = LiveCoreController.create();
    _controller.setLiveID(widget.liveId);
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }

  /// Build a custom view for the connected host
  Widget _buildCoHostWidget(
    BuildContext context, 
    SeatFullInfo seatFullInfo, 
    ViewLayer viewLayer,
  ) {
    if (viewLayer == ViewLayer.foreground) {
      return CustomCoHostForegroundView(seatInfo: seatFullInfo);
    } else {
      return CustomCoHostBackgroundView(seatInfo: seatFullInfo);
    }
  }

  /// Build Custom PK User View
  Widget _buildBattleWidget(BuildContext context, TUIBattleUser userInfo) {
    return CustomBattleUserView(
      liveId: widget.liveId,
      battleUser: userInfo,
    );
  }

  /// Build PK Container View
  Widget _buildBattleContainerWidget(BuildContext context) {
    return CustomBattleContainerView(liveId: widget.liveId);
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: LiveCoreWidget(
        controller: _controller,
        videoWidgetBuilder: VideoWidgetBuilder(
          coHostWidgetBuilder: _buildCoHostWidget,
          battleWidgetBuilder: _buildBattleWidget,
          battleContainerWidgetBuilder: _buildBattleContainerWidget,
        ),
      ),
    );
  }
}
```

## Advanced Features

### Implement PK Score Update Via REST API

In the **live streamer PK scenario**, the value of gifts received by the Anchor will be linked to the PK value (for example: when the audience sends a "rocket" gift, the Anchor's PK score increases by 500 points). You can easily implement real-time score updates in the live PK scenario through our REST API.

> **Important Note:**
> 

> The PK score system in the LiveKit backend uses pure numerical computation and cumulative mechanism. Therefore, you need to complete the PK score calculation before calling the update API based on your operational strategy and business requirement. See the following PK score calculation example:
> 
<table>
<tr>
<td rowspan="1" colSpan="1" >**Gift Type**</td>

<td rowspan="1" colSpan="1" >**Score Calculation Rule**</td>

<td rowspan="1" colSpan="1" >**Example**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Basic Gift</td>

<td rowspan="1" colSpan="1" >Gift Value × 5</td>

<td rowspan="1" colSpan="1" >10 CNY Gift → 50 Points</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Intermediate Gift</td>

<td rowspan="1" colSpan="1" >Gift Value × 8</td>

<td rowspan="1" colSpan="1" >50 CNY Gift → 400 Points</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Senior Gift</td>

<td rowspan="1" colSpan="1" >Gift Value × 12</td>

<td rowspan="1" colSpan="1" >100 CNY Gift → 1200 Points</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Special Effect Gift</td>

<td rowspan="1" colSpan="1" >fixed high score</td>

<td rowspan="1" colSpan="1" >520 CNY Gift → 1314 Points</td>
</tr>
</table>



#### REST API Call Process

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032457995/7dbc23ccf76211f08586525400380f7d.png)


#### Key Process Description
1. **Obtain PK Status:**

  - **Callback Configuration**: Configure [PK Status Callback](https://write.woa.com/document/170203265552953344) to have the `LiveKit` backend actively notify your system when PK starts or ends.

  - **Active Query**: Your backend can call the [PK Status Query](https://write.woa.com/document/170220847572692992) API at any time to check the current PK status.

2. **PK Score Calculation**: Your backend calculates the PK score increment based on your business rules.

3. **PK Score Update**: Your backend calls the [Update PK Score](https://write.woa.com/document/170220034100383744) API to update the PK score in the LiveKit backend.

4. **LiveKit Backend Syncs to Client**: The backend automatically synchronizes the updated PK score to all clients.


#### Involved REST API Endpoints
<table>
<tr>
<td rowspan="1" colSpan="1" >**API**</td>

<td rowspan="1" colSpan="1" >**Function Description**</td>

<td rowspan="1" colSpan="1" >**Request Example**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Active API - Query PK Status</td>

<td rowspan="1" colSpan="1" >Check whether the current room is in PK</td>

<td rowspan="1" colSpan="1" >[Example](https://write.woa.com/document/170220847572692992)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Active API - Update PK Score</td>

<td rowspan="1" colSpan="1" >Update the calculated PK score</td>

<td rowspan="1" colSpan="1" >[Example](https://write.woa.com/document/170220034100383744)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Callback Configuration - PK Start Callback</td>

<td rowspan="1" colSpan="1" >Receive real-time notification when PK starts</td>

<td rowspan="1" colSpan="1" >[Example](https://write.woa.com/document/170203265552953344)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Callback Configuration - PK End Callback</td>

<td rowspan="1" colSpan="1" >Receive real-time notification when PK ends</td>

<td rowspan="1" colSpan="1" >[Example](https://write.woa.com/document/170221608179601408)</td>
</tr>
</table>


## API documentation

For detailed information about all public interfaces, attributes, and methods of [CoHostStore](https://pub.dev/documentation/atomic_x_core/latest/api_live_co_host_store/CoHostStore-class.html) and its related classes, see the official API documentation of the [AtomicXCore](https://tencent-rtc.github.io/TUIKit_Flutter/index.html) framework. The related Store used in this guide is as follows:
<table>
<tr>
<td rowspan="1" colSpan="1" >**Store/Component**</td>

<td rowspan="1" colSpan="1" >**Feature Description**</td>

<td rowspan="1" colSpan="1" >**API Reference**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**LiveCoreWidget**</td>

<td rowspan="1" colSpan="1" >The core view component for live video stream display and interaction: responsible for stream rendering and view widget processing, supporting scenarios such as anchor live streaming, audience mic connection, and cross-room connection with other anchors.</td>

<td rowspan="1" colSpan="1" >[API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_view_live_live_core_widget/LiveCoreWidget-class.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**LiveCoreController**</td>

<td rowspan="1" colSpan="1" >The controller of LiveCoreWidget: are used to set the live stream ID, control the preview, and perform other operations.</td>

<td rowspan="1" colSpan="1" >[API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_view_live_live_core_widget/LiveCoreController-class.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**VideoWidgetBuilder**</td>

<td rowspan="1" colSpan="1" >Video view adapter: used for custom pendant view of video stream in scenarios such as connected host, PK user, and PK containers.</td>

<td rowspan="1" colSpan="1" >[API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_view_live_live_core_widget/VideoWidgetBuilder-class.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**DeviceStore**</td>

<td rowspan="1" colSpan="1" >Audio/Video device control: microphone (on/off, volume), camera (on/off, switchover, video quality), screen sharing, and real-time monitoring of device status.</td>

<td rowspan="1" colSpan="1" >[API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_device_device_store/DeviceStore-class.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**CoHostStore**</td>

<td rowspan="1" colSpan="1" >Anchor cross-room connection: supports multiple layout templates (dynamic grid, etc.), initiate/accept/reject connection, and manage interactive Anchor connections.</td>

<td rowspan="1" colSpan="1" >[API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_co_host_store/api_live_co_host_store-library.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**BattleStore**</td>

<td rowspan="1" colSpan="1" >Anchor PK battle: trigger PK (duration configuration/competitor), manage PK status (started/ended), synchronize score, listen to battle results.</td>

<td rowspan="1" colSpan="1" >[API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_battle_store/BattleStore-class.html)</td>
</tr>
</table>


## FAQs

### **Why Was the Connection Invitation Sent but Not Received by the Other Party?**
- Please check whether `targetHostLiveId` is correct and the other party's live streaming room is in normal live streaming status.

- Check the network connection is connected. The invitation signaling has a default timeout duration of 30 seconds.


### What to Do When Network Disconnection or App Crash Occurs during Connecting Line or PK for an Anchor?

**CoHostStore** and **BattleStore** have internal heartbeat and timeout detection mechanisms. If one party exits abnormally, the other will receive notifications through events such as **onCoHostUserLeft** or **onUserExitBattle**. Based on these events, you can handle the UI, for example, prompt "The other party has gone offline" and end the interaction.

### Why Can PK Score Only Be Updated Via REST API?

Because REST API can satisfy both the **security, real-timeness, and scalability** requirements of PK scores at the same time:
- **Tamper-proof and fair**: Authentication + data validation is required. Each update can trace the source (such as gift actions) to prevent manual score changes or cheating, guaranteeing fair competitive gaming.

- **Multi-end real-time synchronization**: Use a standardized format (such as JSON) to quickly connect the gift, PK, and show systems, ensuring real-time consistency of scores for anchors, audience, and backend with no latency.

- **Flexible rule adaptation**: Just modify the backend configuration (such as adjusting the score corresponding to gifts or bonus points) to adapt to business changes, with no need to modify the frontend, reducing iteration cost.


### How to Manage the Lifecycle and Event of Custom Views Added Via `VideoWidgetBuilder`?

**LiveCoreWidget** automatically manages the addition and removal of views returned by `coHostWidgetBuilder`, `battleWidgetBuilder`, and `battleContainerWidgetBuilder` callbacks, with no need for manual processing. If necessary to handle user interaction (such as click event) in custom views, just add the corresponding event when creating the view.

