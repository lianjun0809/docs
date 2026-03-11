> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/en/llms.txt
> Use this file to discover all available pages before exploring further.

**AtomicXCore** provided the [CoGuestStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_co_guest_store/CoGuestStore-class.html) module, specialized to manage the complete business process of audience mic connection. Developers do not need to worry about complex state synchronization and signaling interaction, just call a few simple methods to add powerful audio-video interaction between audience and Anchor to your live stream.

## Core Scenario

`CoGuestStore` supports the following two most mainstream microphone-connected scenarios:
- **Audience request to speak**: The audience proactively initiate mic connection request, and the Anchor can grant or reject after receiving the request.

- **Anchor invitation to speak**: The Anchor can proactively initiate mic connection to any audience in the live streaming room.


## Implementation Steps

### Step 1: Integrating the Component

Refer to [Quick Access](https://write.woa.com/document/200455640177692672) for seamless integration with **AtomicXCore** and complete **LiveCoreWidget** access.

After integration, start implementing the co-anchoring function.

### Step 2: Implementing Audience Request to Speak

#### Client Implementation

As an audience member, your core task is to **initiate application, receive results** and **become a listener**.
1. **Initiate mic connection**


   When the user clicks the "apply for mic connection" button on the interface, call the `applyForSeat` method.

   ``` java
   import 'package:atomic_x_core/atomicxcore.dart';
   
   final String liveId = "room ID";
   final CoGuestStore guestStore = CoGuestStore.create(liveId);
   
   // User clicks "apply for mic connection"
   void requestToConnect() async {
       // seatIndex: The microphone slot index, value range is -1 (auto select an empty slot) and [0, maximum number of microphone slots in the current room -1], timeout: request timeout period (seconds)
       final result = await guestStore.applyForSeat(
           seatIndex: 0, 
           timeout: 30, 
           extraInfo: null,
       );
       if (result.isSuccess) {
           print("Mic connection request sent, wait for anchor processing...");
       } else {
           print("Failed to send request: ${result.errorMessage}");
       }
   }
   ```
2. **Listen to the anchor's response**


   By adding a listener through `addGuestListener`, you can receive the anchor's processing result.

   ``` java
   late GuestListener _guestListener;
   
   // Subscribe to events when your Widget is initialized
   void subscribeGuestEvents() {
       _guestListener = GuestListener(
           onApplicationAccepted: (hostUser) {
               print("Anchor ${hostUser.userName} agreed to your request, preparing to connect mic");
               // 1. Turn on the camera, microphone 
               DeviceStore.shared.openLocalCamera(isFront: true);
               DeviceStore.shared.openLocalMicrophone();
               // 2. Update the UI here, such as disabling the apply button and displaying the mic connection state
           },
           onApplicationRejected: (hostUser) {
               print("Anchor ${hostUser.userName} refused your request");
               // Pop-up prompts user that the request was rejected
           },
           onInvitationReceived: (hostUser) {
               print("Received mic connection invitation from Anchor ${hostUser.userName}");
               // Pop up a dialog box herein for users to choose "Accept" or "Reject"
               _showInvitationDialog(hostUser);
           },
           onKickedOffSeat: () {
               print("You have been kicked off the mic by Anchor");
               // Update UI, turn off the camera and microphone
           },
       );
       guestStore.addGuestListener(_guestListener);
   }
   
   @override
   void dispose() {
       guestStore.removeGuestListener(_guestListener);
       super.dispose();
   }
   ```
3. **Leave the mic**


   When a mic-connecting audience wants to end the interaction, call the `disconnect` method to return to general audience status.

   ``` java
   // User clicks "leave mic" button
   void leaveSeat() async {
       final result = await guestStore.disconnect();
       if (result.isSuccess) {
           print("Left mic successfully");
       } else {
           print("Failed to leave mic: ${result.errorMessage}");
       }
   }
   ```
4. **(Optional) Cancel application**


   If the audience wants to withdraw the application before anchor processing, they can call the API `cancelApplication`.

   ``` java
   // While waiting, the user clicks "Cancel Application"
   void cancelRequest() async {
       final result = await guestStore.cancelApplication();
       if (result.isSuccess) {
           print("Application canceled");
       } else {
           print("Failed to cancel request: ${result.errorMessage}");
       }
   }
   ```

#### Anchor Implementation

As an Anchor, your core task is to **receive applications, show the Application List** and **process applications**.
1. **Listen for new mic connection requests**


   By adding a listener through `addHostListener`, you can receive immediate notification when a new audience applies and get prompted.

   ``` java
   import 'package:atomic_x_core/atomicxcore.dart';
   
   final String liveId = "room ID";
   final CoGuestStore guestStore = CoGuestStore.create(liveId);
   late HostListener _hostListener;
   late final VoidCallback _applicantsChangedListener = _onApplicantsChanged;
   
   // Subscribe to anchor event
   void subscribeHostEvents() {
       _hostListener = HostListener(
           onApplicationReceived: (guestUser) {
               print("Received join microphone application from audience ${guestUser.userName}");
               // Update UI herein, for example display a red dot on the "application list" button
           },
           onInvitationAccepted: (guestUser) {
               print("Audience ${guestUser.userName} accepted your invitation");
           },
           onInvitationRejected: (guestUser) {
               print("Audience ${guestUser.userName} refused your invite");
           },
       );
       guestStore.addHostListener(_hostListener);
   }
   
   @override
   void dispose() {
       guestStore.removeHostListener(_hostListener);
       super.dispose();
   }
   ```
2. **Show application list**


   `CoGuestStore`'s `coGuestState` maintains the current applicant list in real time. You can listen to it to update your UI.

   ``` java
   // Subscription status update
   void subscribeApplicants() {
       guestStore.coGuestState.applicants.addListener(_applicantsChangedListener);
   }
   
   void _onApplicantsChanged() {
       final applicants = guestStore.coGuestState.applicants.value;
       print("Current number of applicants: ${applicants.length}");
       // Refresh your "applicant list" UI herein
       setState(() {
           _applicantList = applicants;
       });
   }
   
   @override
   void dispose() {
       guestStore.coGuestState.applicants.removeListener(_applicantsChangedListener);
       super.dispose();
   }
   ```
3. **Handle mic connection request**


   When you select an audience from the list and click "Grant" or "Reject", call the appropriate method.

   ``` java
   // Anchor clicks the "Grant" button and imports the applicant's userID
   void accept(String userId) async {
       final result = await guestStore.acceptApplication(userId);
       if (result.isSuccess) {
           print("Approved $userId's request, the other party is connecting mic");
       }
   }
   
   // Anchor clicked the "Reject" button
   void reject(String userId) async {
       final result = await guestStore.rejectApplication(userId);
       if (result.isSuccess) {
           print("Denied $userId's request");
       }
   }
   ```

### Step 3: Implementing Anchor Invitation to Speak

#### Anchor Implementation
1. **Initiate invitation to audience**


   When the Anchor selects someone from the audience list and clicks "invite to mic connection", call the `inviteToSeat` method.

   ``` java
   // Anchor selects audience and initiates invitation
   void invite(String userId) async {
       // inviteeID: The invitee ID, seatIndex: The microphone slot index, value range is -1 (auto select an empty slot) and [0, maximum number of microphone slots in the current room -1] 
       // timeout: invitation timeout duration
       final result = await guestStore.inviteToSeat(
           inviteeID: userId,
           seatIndex: 0,
           timeout: 30, 
           extraInfo: null,
       );
       if (result.isSuccess) {
           print("Invitation sent to $userId, waiting for peer response...");
       }
   }
   ```
2. **Listen to the audience response**


   Listen to the invitation event response via `HostListener`.

   ``` java
   // Callback configured in HostListener
   _hostListener = HostListener(
       onInvitationAccepted: (guestUser) {
           print("Audience ${guestUser.userName} accepted your invitation");
       },
       onInvitationRejected: (guestUser) {
           print("Audience ${guestUser.userName} refused your invite");
       },
   );
   ```

#### Client Implementation
1. **Receive the anchor's invitation**


   Listen to the invitation event via `GuestListener`.

   ``` java
   // Callback configured in GuestListener
   _guestListener = GuestListener(
       onInvitationReceived: (hostUser) {
           print("Received mic connection invitation from Anchor ${hostUser.userName}");
           // Pop up a dialog box herein for users to choose "Accept" or "Reject"
           _showInvitationDialog(hostUser);
       },
   );
   ```
2. **Respond to invitation**


   When the user makes a selection in the pop-up dialog box, call the appropriate method.

   ``` java
   String inviterId = "Anchor ID initiating invitation"; // Obtain from onInvitationReceived callback
   
   // User click "Accept"
   void acceptInvitation() async {
       final result = await guestStore.acceptInvitation(inviterId);
       if (result.isSuccess) {
           // Turn on the camera, microphone  
           DeviceStore.shared.openLocalCamera(isFront: true);
           DeviceStore.shared.openLocalMicrophone();
       }
   }
   
   // User click "Reject"
   void rejectInvitation() async {
       await guestStore.rejectInvitation(inviterId);
   }
   ```

### Execution Effect

After integrating the above feature implementation, perform a co-streaming operation using two audiences and an Anchor separately. Audience A turns on the camera and microphone simultaneously, while Audience B turns on microphone only. The execution effect is as follows. You can refer to the next chapter [Refine UI Details](https://write.woa.com/#.E5.AE.8C.E5.96.84-ui-.E7.BB.86.E8.8A.82) to customize your desired UI logic.

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032457995/4bc40212f76011f08586525400380f7d.png)


## Refine UI Details

You can use the "slot" capacity provided by the `VideoWidgetBuilder` parameter of `LiveCoreWidget` to add custom views on the video stream image of audience co-broadcasting, for displaying Nickname, avatar information, etc., or offer placeholder images when they turn camera off, to optimize visual experience.

### Implementing Nickname Display on Video Stream Image

#### **Effect**

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032457995/20cd025ff76111f0831c52540073fd3b.png)


#### **Implementation Method**
- **Step 1**: Create a foreground view (**CustomSeatForegroundView**) used for displaying user information above the video stream.

   ``` java
   import 'package:flutter/material.dart';
   import 'package:rtc_room_engine/rtc_room_engine.dart';
   
   /// Custom user information floating view (foreground)
   class CustomSeatForegroundView extends StatelessWidget {
       final SeatFullInfo seatInfo;
   
       const CustomSeatForegroundView({
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
                       margin: const EdgeInsets.all(5),
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
- **Step 2**: Create a background view (**CustomSeatBackgroundView**) used as a placeholder image when the user has no video stream.

   ``` java
   import 'package:flutter/material.dart';
   import 'package:rtc_room_engine/rtc_room_engine.dart';
   
   /// Custom avatar placeholder view (background)
   class CustomSeatBackgroundView extends StatelessWidget {
       final SeatFullInfo seatInfo;
   
       const CustomSeatBackgroundView({
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
- **Step 3**: Build a custom view through the `VideoWidgetBuilder`'s `coGuestWidgetBuilder` callback, and return the corresponding view based on the `viewLayer` value.

   ``` java
   import 'package:flutter/material.dart';
   import 'package:atomic_x_core/atomicxcore.dart';
   import 'package:rtc_room_engine/rtc_room_engine.dart';
   
   /// Live streaming page with custom connection view
   class CustomCoGuestLiveWidget extends StatefulWidget {
       final String liveId;
   
       const CustomCoGuestLiveWidget({
           Key? key, 
           required this.liveId,
       }) : super(key: key);
   
       @override
       State<CustomCoGuestLiveWidget> createState() => _CustomCoGuestLiveWidgetState();
   }
   
   class _CustomCoGuestLiveWidgetState extends State<CustomCoGuestLiveWidget> {
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
   
       /// Build a custom view for the mic-connecting audience
       Widget _buildCoGuestWidget(
           BuildContext context, 
           SeatFullInfo seatFullInfo, 
           ViewLayer viewLayer,
       ) {
           if (viewLayer == ViewLayer.foreground) {
               // Foreground layer: Always display on top of the video image, used for Nickname, information, etc.
               return CustomSeatForegroundView(seatInfo: seatFullInfo);
           } else {
               // Background layer: Displayed only when the corresponding user has no video stream, used for displaying avatar placeholder images
               return CustomSeatBackgroundView(seatInfo: seatFullInfo);
           }
       }
   
       @override
       Widget build(BuildContext context) {
           return Scaffold(
               body: LiveCoreWidget(
                   controller: _controller,
                   videoWidgetBuilder: VideoWidgetBuilder(
                       coGuestWidgetBuilder: _buildCoGuestWidget,
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

<td rowspan="1" colSpan="1" >Seat information object, containing the Anchor's detailed information.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`seatFullInfo.userInfo.userId`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >Anchor's user ID.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`seatFullInfo.userInfo.userName`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >On-mic user's nickname.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`seatFullInfo.userInfo.avatarUrl`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >On-mic user's profile photo URL.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`viewLayer`</td>

<td rowspan="1" colSpan="1" >`ViewLayer`</td>

<td rowspan="1" colSpan="1" >View hierarchy enumeration.<br>- `ViewLayer.foreground` represents the pendant view, always displayed on top of the video image.<br>- `ViewLayer.background` represents the background pendant view, located in the lower layer of the foreground view. It is displayed only when the corresponding user has no video stream (for example, when the camera is not turned on), usually used for displaying the default avatar or placeholder image of the user.</td>
</tr>
</table>


## API documentation

For details about ALL public interfaces, properties, and methods of [CoGuestStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_co_guest_store/CoGuestStore-class.html) and its related classes, see the official API documentation of the [AtomicXCore](https://tencent-rtc.github.io/TUIKit_Flutter/index.html) framework. The related Stores used in this guide are as follows:
<table>
<tr>
<td rowspan="1" colSpan="1" >**Store/Component**</td>

<td rowspan="1" colSpan="1" >**Feature Description**</td>

<td rowspan="1" colSpan="1" >**API Reference**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >LiveCoreWidget</td>

<td rowspan="1" colSpan="1" >Core view component for live video stream display and interaction: Responsible for stream rendering and view widget processing, supporting scenarios such as Anchor live streaming, audience co-broadcasting, and cross-room connection with other anchors.</td>

<td rowspan="1" colSpan="1" >[API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_view_live_live_core_widget/LiveCoreWidget-class.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >LiveCoreController</td>

<td rowspan="1" colSpan="1" >Controller for LiveCoreWidget: Used to set the live stream ID, control the preview, and perform other operations.</td>

<td rowspan="1" colSpan="1" >[API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_view_live_live_core_widget/LiveCoreController-class.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >VideoWidgetBuilder</td>

<td rowspan="1" colSpan="1" >Video view adapter: Used for custom pendant views in scenarios such as mic-connecting audience, cross-room connection with other anchors, and PK.</td>

<td rowspan="1" colSpan="1" >[API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_view_live_live_core_widget/VideoWidgetBuilder-class.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >DeviceStore</td>

<td rowspan="1" colSpan="1" >Audio/Video device control: Microphone (on/off, volume), camera (on/off, switchover, video quality), screen sharing, and real-time monitoring of device status.</td>

<td rowspan="1" colSpan="1" >[API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_device_device_store/DeviceStore-class.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >CoGuestStore</td>

<td rowspan="1" colSpan="1" >Audience co-broadcasting management: Join microphone application/invite/grant/reject, attendee permission control (microphone/camera), state synchronization.</td>

<td rowspan="1" colSpan="1" >[API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_co_guest_store/CoGuestStore-class.html)</td>
</tr>
</table>


## FAQs

### How to Manage the Lifecycle and Event of a Custom View Added Via `VideoWidgetBuilder`?

**LiveCoreWidget** will automatically manage the addition and removal of views returned by the `coGuestWidgetBuilder` callback, so you don't need to handle them manually. If necessary to process user interaction (such as click events) in a custom view, just add corresponding event handling when creating the view.

### `ViewLayer` What Are the Functions of the Parameter?

`ViewLayer` is used to distinguish between foreground and background widgets.
- `ViewLayer.foreground`: The foreground layer, always displayed on top of the video image.

- `ViewLayer.background`: The background layer, displayed only when the corresponding user has no video stream (for example, when the camera is not turned on), usually used for displaying the default avatar or placeholder image of the user.


### Why Is My Custom View Not Displayed?
- **Check VideoWidgetBuilder settings**: Please confirm the `LiveCoreWidget`'s `videoWidgetBuilder` parameter is correctly set.

- **Check callback implementation**: Please check if the `coGuestWidgetBuilder` callback function is correctly implemented.

- **Check the return value**: Ensure your callback function returns an effective `Widget` instance.


