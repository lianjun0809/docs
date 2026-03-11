> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

**AtomicXCore** provides [CoGuestStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_co_guest_store/CoGuestStore-class.html) and [LiveSeatStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_live_seat_store/LiveSeatStore-class.html) modules, used to manage the complete business process of audience mic connection. Users do not need to worry about complex state synchronization and signaling interaction, just call a few simple methods to add powerful audio-video interaction between audience and anchor to your live stream. This document will guide you on how to use `CoGuestStore` and `LiveSeatStore` for quick implementation of audio mic connection in Flutter application.

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032457995/9751d111f80f11f08d7f52540097cba1.png)


## Core Scenario

`CoGuestStore` and `LiveSeatStore` support the following mainstream scenarios:
- **Audience request to speak**: The audience proactively initiates a mic connection request, and the anchor can grant or reject it upon receiving the request.

- **Anchor invitation to speak**: The anchor can proactively initiate a mic connection invitation to any audience in the live streaming room.

- **Anchor seat management**: The anchor can perform operations such as forced microphone removal, muting, and locking on the user on the seat.


## Implementation Steps

### Step 1: Component Integration

Refer to [quick integration](https://write.woa.com/document/200555778169073664) to integrate **AtomicXCore**.

> **Note:**
> 

> Before implementing the co-anchoring function, you need to get the `liveId` (the unique identifier of the live streaming room) to distinguish different live streaming rooms. The method for obtaining it is as follows.
> 
> - **Anchor**: Specify when creating a live stream via `LiveListStore.shared.createLive(liveInfo)`.
> - **Client**: Get it from `liveInfo` in `LiveListState.liveList.value`, or obtain it by the Anchor sharing the live streaming room ID.


### Step 2: Implement Audience Mic-Link Request

#### Audience Side Implementation

As an audience member, your main tasks are **initiating a request, handling the response**, and **leaving the mic proactively**.
1. **Initiate Mic-Link Request**


   When the user taps the "Request Mic-Link" button in the UI, call the `applyForSeat` method.

   ``` java
   import 'package:atomic_x_core/atomicxcore.dart';
   
   final String liveId = "room ID";
   late CoGuestStore guestStore;
   
   @override
   void initState() {
     super.initState();
     guestStore = CoGuestStore.create(liveId);
   }
   
   // User click "Apply for Mic Connection"
   Future<void> requestToConnect() async {
     // seatIndex: The seat index, starting from 0, represents the applied microphone position. 0 means the first seat. View seat status via LiveSeatState.seatList.value and select an idle seat.
     // timeout: Request timeout (seconds). The audience can call cancelApplication to cancel the request to speak within the timeout period.
     // The request will expire if it hasn't been processed after reaching the timeout period
     final result = await guestStore.applyForSeat(
       seatIndex: 0,
       timeout: 30,
       extraInfo: null,
     );
     if (result.isSuccess) {
       debugPrint('Mic connection request sent, waiting for anchor processing...');
     } else {
       debugPrint('Failed to send request: ${result.message}');
     }
   }
   ```
2. **Listen for Host Response**


   By adding `GuestListener`, you can receive the host's response

   ``` java
   late GuestListener _guestListener;
   
   // Subscribe to events when your Widget initializes
   void subscribeGuestEvents() {
     _guestListener = GuestListener(
       onGuestApplicationResponded: (isAccept, hostUser) {
         if (isAccept) {
           debugPrint('Anchor ${hostUser.userName} granted your request, preparing to join the mic');
           // 1. Turn on microphone
           // DeviceStore is the device management module provided by AtomicXCore, used for managing microphones, cameras and other physical devices.
           // When the host agrees to connect mic, turn on microphone to start collecting audio.
           DeviceStore.shared.openLocalMicrophone();
           // 2. Update UI herein, such as disabling the apply button and displaying the mic connection state
         } else {
           debugPrint('Anchor ${hostUser.userName} refused your request');
           // Pop-up prompts user that the application was rejected
         }
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
3. **Leave Mic Proactively**


   When an audience member on mic wants to end the interaction, call `disConnect` to return to regular audience status.

   ``` java
   // User click "Disconnect" button
   Future<void> leaveSeat() async {
     final result = await guestStore.disconnect();
     if (result.isSuccess) {
       debugPrint('Disconnected successfully');
     } else {
       debugPrint('Failed to leave the seat: ${result.message}');
     }
   }
   ```
4. **(Optional) Cancel Request**


   If the audience member wants to withdraw the request before the host responds, call `cancelApplication`.

   ``` java
   // While waiting, the user clicks "Cancel Application"
   Future<void> cancelApplication() async {
     final result = await guestStore.cancelApplication();
     if (result.isSuccess) {
       debugPrint('Request canceled');
     } else {
       debugPrint('Failed to cancel request: ${result.message}');
     }
   }
   ```

#### Host Side Implementation

As the host, your main tasks are **receiving requests, displaying the request list**, and **handling requests**.
1. **Listen for New Mic-Link Requests**


   By adding `HostListener`, you can receive immediate notification when a new audience applies and prompt.

   ``` java
   import 'package:atomic_x_core/atomicxcore.dart';
   
   final String liveId = "room ID";
   late CoGuestStore guestStore;
   late HostListener _hostListener;
   
   @override
   void initState() {
     super.initState();
     guestStore = CoGuestStore.create(liveId);
   
     // Subscribe to anchor event
     _hostListener = HostListener(
       onGuestApplicationReceived: (guestUser) {
         debugPrint('Received mic connection request from audience ${guestUser.userName}');
         // Update the UI here, for example display a red dot on the "application list" button
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
2. **Display Request List**


   `CoGuestStore`'s `coGuestState` maintains the current applicant list in real time. You can subscribe to it to update your UI.

   ``` java
   late final VoidCallback _applicantsListener = _onApplicantsChanged;
   
   // Subscribe to status change
   void subscribeApplicants() {
     guestStore.coGuestState.applicants.addListener(_applicantsListener);
   }
   
   void _onApplicantsChanged() {
     final applicants = guestStore.coGuestState.applicants.value;
     debugPrint('Current number of applicants: ${applicants.length}');
     // Update your "applicant list" UI here
   }
   
   @override
   void dispose() {
     guestStore.coGuestState.applicants.removeListener(_applicantsListener);
     super.dispose();
   }
   ```
3. **Handle Mic-Link Requests**


   When you select an audience member from the list and tap "Accept" or "Reject", call the corresponding method.

   ``` java
   // Anchor clicks the "Grant" button and imports the applicant's userID
   Future<void> accept(String userId) async {
     final result = await guestStore.acceptApplication(userId);
     if (result.isSuccess) {
       debugPrint('Approved $userId\'s request, the other party is joining the mic');
     }
   }
   
   // Anchor clicks the "Reject" button
   Future<void> reject(String userId) async {
     final result = await guestStore.rejectApplication(userId);
     if (result.isSuccess) {
       debugPrint('$userId\'s application denied');
     }
   }
   ```

### Step 3: Implement Host-Initiated Mic-Link Invitation

#### Host Side Implementation
1. **Invite Audience to Mic**


   When the host selects a viewer from the audience list and taps "Invite to Mic", call the `inviteToSeat` method.

   ``` java
   // Anchor selects audience and initiates invitation
   Future<void> invite(String userId) async {
     // inviteeID: The ID of the invitee, seatIndex: The seat index, timeout: The invitation timeout duration
     final result = await guestStore.inviteToSeat(
       inviteeID: userId,
       seatIndex: 0,
       timeout: 30,
       extraInfo: null,
     );
     if (result.isSuccess) {
       debugPrint('Sent invitation to $userId, waiting for peer response...');
     }
   }
   ```
2. **Listen for Audience Response**


   Listen to the `onHostInvitationResponded` event via `HostListener`.

   ``` java
   // Add to the HostListener configuration
   _hostListener = HostListener(
     onHostInvitationResponded: (isAccept, guestUser) {
       if (isAccept) {
         debugPrint('Audience ${guestUser.userName} accepted your invitation');
       } else {
         debugPrint('Audience ${guestUser.userName} refused your invitation');
       }
     },
   );
   ```

#### Audience Side Implementation
1. **Receive Host Invitation**


   Listen to the `onHostInvitationReceived` event via `GuestListener`.

   ``` java
   // Add to the GuestListener configuration
   _guestListener = GuestListener(
     onHostInvitationReceived: (hostUser) {
       debugPrint('Received mic connection invitation from Anchor ${hostUser.userName}');
       // Pop up a dialog box for user selection between "Accept" or "Reject"
       // showInvitationDialog(hostUser);
     },
   );
   ```
2. **Respond to invitation**


   After the user makes a selection in the pop-up dialog box, call the method accordingly.

   ``` java
   final String inviterId = "anchor ID who initiates invitation"; // obtain from onHostInvitationReceived event
   
   // User clicks "Accept"
   Future<void> accept() async {
     final result = await guestStore.acceptInvitation(inviterId);
     if (result.isSuccess) {
       // Turn the mic on
       // DeviceStore is the device management module provided by AtomicXCore, used for managing microphones, cameras and other physical devices.
       // After accepting the invitation, turn on microphone to start collecting audio
       DeviceStore.shared.openLocalMicrophone();
     }
   }
   
   // User click "Reject"
   Future<void> reject() async {
     await guestStore.rejectInvitation(inviterId);
   }
   ```

## Advanced Features

Once a user is on mic, the host may need to manage mic seats. The following features are primarily provided by `LiveSeatStore`, which functions with `CoGuestStore`.

### DeviceStore and LiveSeatStore Microphone Control Process

When using the seat feature, you need to understand the difference between `DeviceStore` and `LiveSeatStore` in microphone control:
- **DeviceStore**: Manage physical devices. `openLocalMicrophone` starts up the microphone device to perform audio capture. `closeLocalMicrophone` stops audio capture and releases the microphone device.

- **LiveSeatStore**: Manages seat business (i.e., audio stream). `muteMicrophone` mutes and stops sending local audio stream to the remote end, but the microphone device itself keeps running. `unmuteMicrophone` unmutes and restores sending audio stream to the remote end.


   **Recommended workflow**: You should follow the principle of "open the device only once and use the mute switch for Anchor."

1. **When going on stage**: Once the audience succeeds in going on stage, call `openLocalMicrophone` only once to start the device.

2. **When on stage**: For all "unmute" and "mute" operations on the seat, users should call `unmuteMicrophone` and `muteMicrophone` to control the upstream audio stream.

3. **When going off stage**: When a user goes off stage (such as calling `disconnect`), call `closeLocalMicrophone` to release the device.


### On-Mic Users Control Their Own Microphone

On-mic users (including the host) can control their own microphone mute status via the `LiveSeatStore` interface.

#### Implementation:
1. **Mute**: Call the `muteMicrophone()` method. This is a one-way request with no callback.

2. **Unmute**: Call the `unmuteMicrophone()` method.


#### Example code:
``` java
final seatStore = LiveSeatStore.create(liveId);

seatStore.muteMicrophone(); // Mute

await seatStore.unmuteMicrophone(); // Unmute
```

### Host Remotely Controls On-Mic User’s Microphone

The host can perform "force mute" or "invite to unmute" operations on other on-mic users.

#### Implementation:
1. **Force Mute (Lock)**: The host calls `closeRemoteMicrophone` to forcibly mute the target user's microphone and lock their mic control. The muted user will receive the `onLocalMicrophoneClosedByAdmin` event via `liveSeatEventPublisher`, and their local "Open Microphone" button should become disabled.

2. **Invite to Unmute (Unlock)**: The host calls `openRemoteMicrophone`—this does not forcibly open the user's mic, but unlocks their mic control, allowing them to unmute themselves. The target user receives the `onLocalMicrophoneOpenedByAdmin` event, their "Open Microphone" button should become enabled, but they remain muted until they unmute themselves.

3. **User Unmutes Themselves**: After receiving the unlock notification, the user must actively call `LiveSeatStore`'s `unmuteMicrophone()` to actually unmute and be heard in the room.


#### Example code:

##### Host Side:
``` java
final seatStore = LiveSeatStore.create(liveId);
final String targetUserId = "userD";

// 1. Force mute userD and lock
final result1 = await seatStore.closeRemoteMicrophone(targetUserId);
if (result1.isSuccess) {
  debugPrint('Muted and locked $targetUserId');
}

// 2. Unlock userD's microphone permission (at this point userD remains muted)
final result2 = await seatStore.openRemoteMicrophone(
  userID: targetUserId,
  policy: DeviceControlPolicy.unlockOnly,
);
if (result2.isSuccess) {
  debugPrint('Unlocked $targetUserId\'s microphone, user can unmute manually');
}
```

##### Audience Side:
``` java
late LiveSeatListener _seatListener;

// userD listens to the Anchor's operation
void subscribeSeatEvents() {
  _seatListener = LiveSeatListener(
    onLocalMicrophoneClosedByAdmin: () {
      debugPrint('Muted by anchor');
      // muteButton.isEnabled = false;
    },
    onLocalMicrophoneOpenedByAdmin: (policy) {
      debugPrint('Anchor unmuted and unlocked');
      // muteButton.isEnabled = true;
      // muteButton.text = "Turn on microphone";
    },
  );
  seatStore.addLiveSeatEventListener(_seatListener);
}

@override
void dispose() {
  seatStore.removeLiveSeatEventListener(_seatListener);
  super.dispose();
}
```

#### CloseRemoteMicrophone API Parameter
<table>
<tr>
<td rowspan="1" colSpan="1" >**Parameter**</td>

<td rowspan="1" colSpan="1" >**Type**</td>

<td rowspan="1" colSpan="1" >**Description**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`userID`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >Operating user `userID`.</td>
</tr>
</table>


#### OpenRemoteMicrophone API Parameter
<table>
<tr>
<td rowspan="1" colSpan="1" >**Parameter**</td>

<td rowspan="1" colSpan="1" >**Type**</td>

<td rowspan="1" colSpan="1" >**Description**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`userID`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >Operating user `userID`.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`policy`</td>

<td rowspan="1" colSpan="1" >`DeviceControlPolicy`</td>

<td rowspan="1" colSpan="1" >Turn on microphone policy.</td>
</tr>
</table>


### Host Removes On-Mic User from the Seat

#### Implementation:
1. **Remove User from Mic**: The anchor can call the `kickUserOutOfSeat` method to force the specified user off the mic.

2. **Listen for Event Notification**: Users kicked off the mic will receive the `GuestListener``onKickedOffSeat` event notification.


#### Example code:
``` java
// Assume "userB" is to be kicked out
final String targetUserId = "userB";
final result = await seatStore.kickUserOutOfSeat(targetUserId);
if (result.isSuccess) {
  debugPrint('Kicked $targetUserId off the mic');
} else {
  debugPrint('Kick user failed: ${result.message}');
}

// "userB" received the kicked off the mic event
_guestListener = GuestListener(
  onKickedOffSeat: (seatIndex, hostUser) {
    // Show a toast notification
    debugPrint('You have been kicked off the mic by anchor');
  },
);
```

#### KickUserOutOfSeat API Parameter
<table>
<tr>
<td rowspan="1" colSpan="1" >**Parameter**</td>

<td rowspan="1" colSpan="1" >**Type**</td>

<td rowspan="1" colSpan="1" >**Description**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`userID`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >The user kicked off the mic `userID`.</td>
</tr>
</table>


### Host Locks and Unlocks Mic Seats

The host can lock or unlock a specific mic seat.

#### Implementation:
1. **Lock Seat**: The anchor can call the `lockSeat` method to lock the seat with a specified index. Once locked, audiences cannot use `applyForSeat` or `takeSeat` to occupy the seat, but the anchor can invite an audience to the locked seat via `inviteToSeat`.

2. **Unlock Seat**: Call `unlockSeat` to unlock the seat. The seat can be occupied again after unlocking.


#### Example code:
``` java
// Lock seat 2
final result1 = await seatStore.lockSeat(2);
if (result1.isSuccess) {
  debugPrint('Seat 2 locked');
}

// Unlock seat 2
final result2 = await seatStore.unlockSeat(2);
if (result2.isSuccess) {
  debugPrint('Seat 2 unlocked');
}
```

#### LockSeat API Parameter
<table>
<tr>
<td rowspan="1" colSpan="1" >**Parameter**</td>

<td rowspan="1" colSpan="1" >**Type**</td>

<td rowspan="1" colSpan="1" >**Description**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`seatIndex`</td>

<td rowspan="1" colSpan="1" >`int`</td>

<td rowspan="1" colSpan="1" >Index of the mic to lock.</td>
</tr>
</table>


#### UnlockSeat API Parameter
<table>
<tr>
<td rowspan="1" colSpan="1" >**Parameter**</td>

<td rowspan="1" colSpan="1" >**Type**</td>

<td rowspan="1" colSpan="1" >**Description**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`seatIndex`</td>

<td rowspan="1" colSpan="1" >`int`</td>

<td rowspan="1" colSpan="1" >Index of the mic to unlock.</td>
</tr>
</table>


### Move Seat

Anchor and regular Microphone Users can call `moveUserToSeat` to move microphone positions.

#### Implementation:
1. **Host Moves User to Mic Seat**: The host can call this API to move any user to a specified seat. At this point, `userID` is the ID of the target user, `targetIndex` is the index of the target seat, and the `policy` parameter specifies the move strategy if the target seat is occupied. For details, see the [API parameter](https://write.woa.com/#moveusertoseat-.E6.8E.A5.E5.8F.A3.E5.8F.82.E6.95.B0.EF.BC.9A) description.

2. **On-Mic User Moves Themselves**: On-mic users can also call this API to move themselves. In this case, `userID` must be the user's own ID, `targetIndex` is the desired new seat index, and the `policy` parameter is ignored. If the target seat is occupied, the move fails with an error.


#### Example code:
``` java
final result = await seatStore.moveUserToSeat(
  userID: "userC",
  targetIndex: newSeatIndex,
  policy: MoveSeatPolicy.abortWhenOccupied,
);
if (result.isSuccess) {
  debugPrint('Successfully moved to seat $newSeatIndex');
} else {
  debugPrint('Seat change failed, possibly seat is occupied');
}
```

#### MoveUserToSeat API Parameter
<table>
<tr>
<td rowspan="1" colSpan="1" >**Parameter**</td>

<td rowspan="1" colSpan="1" >**Type**</td>

<td rowspan="1" colSpan="1" >**Description**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`userID`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >The user who needs to move the mic `userID`.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`targetIndex`</td>

<td rowspan="1" colSpan="1" >`int`</td>

<td rowspan="1" colSpan="1" >Index of the target seat.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`policy`</td>

<td rowspan="1" colSpan="1" >`MoveSeatPolicy`</td>

<td rowspan="1" colSpan="1" >Processing policy when the target seat is occupied<br>- `abortWhenOccupied`: Abort movement when the target seat is occupied (default policy)<br>- `forceReplace`: Forcibly replace the user on the target seat. The replaced user will be kicked off the mic.<br>- `swapPosition`: Exchange with the user on the target seat.</td>
</tr>
</table>


## API documentation

For detailed information about ALL public interfaces, attributes, and methods of [CoGuestStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_co_guest_store/CoGuestStore-class.html), [LiveSeatStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_live_seat_store/LiveSeatStore-class.html), and its related classes, see the official API documentation of the [AtomicXCore](https://tencent-rtc.github.io/TUIKit_Flutter) framework. The related Store used in this guide is as follows:
<table>
<tr>
<td rowspan="1" colSpan="1" >**Store/Component**</td>

<td rowspan="1" colSpan="1" >**Feature Description**</td>

<td rowspan="1" colSpan="1" >**API Reference**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**CoGuestStore**</td>

<td rowspan="1" colSpan="1" >Audience co-broadcasting management: join microphone application/invite/consent/deny, member permission control (microphone/camera), state synchronization.</td>

<td rowspan="1" colSpan="1" >[API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_co_guest_store/CoGuestStore-class.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**LiveSeatStore**</td>

<td rowspan="1" colSpan="1" >Seat management: mute/unmute, lock/unlock seats, remove speaker, remotely control Anchor microphone, listen to list status.</td>

<td rowspan="1" colSpan="1" >[API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_live_seat_store/LiveSeatStore-class.html)</td>
</tr>
</table>


## FAQs

### What Is the Difference between Voice Room Co-Streaming and Live Streaming Co-Streaming

The main difference between both lies in business form and UI display:
- Live streaming: The core is video footage. You will use `LiveCoreWidget` as the core component to render the video stream of the Anchor and mic-connecting audience. The UI focuses on processing the layout and size of video footage, as well as adding 3D stickers (such as Nickname and placeholder image) on the video stream through `VideoViewDelegate`. You can turn on the camera and microphone at the same time.

- Voice room (voice chat room): The core is the seat grid. You will not use `LiveCoreWidget`, but build a grid UI (such as `GridView`) based on `LiveSeatStore`'s `liveSeatState` (especially `seatList`). The UI focuses on displaying each seat `SeatInfo` state in real time: whether there is a person, whether it is muted, whether it is locked, and whether speaking is ongoing. You only need to turn on microphone.


### How to Real-Time Refresh Seat Information on UI (Such As Whether There Is a Person, Whether Muted)

You should subscribe to the `seatList` property in `LiveSeatState`, which is a responsive data of `ValueListenable<List<SeatInfo>>` data type. It will notify you to re-render the microphone position list whenever the array changes. By traversing this array, you can:
- Get user information on the seat through `seatInfo.userInfo`.

- Check whether the seat is locked through `seatInfo.isLocked`.

- Check the mic status of the on-mic user through `seatInfo.userInfo.microphoneStatus`.


