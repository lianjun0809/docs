> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

`LiveAudienceStore` is a module in `AtomicXCore` specialized in managing live streaming room audience information. With `LiveAudienceStore`, you can build a complete audience list and management system for your live stream application.

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032457995/3c4c7159f6dd11f0831c52540073fd3b.png)


## Core Features
- **Real-time Audience List**: Get and show ALL audience information currently in the live streaming room.

- **Audience Statistics**: Get the accurate total number of audience in the live streaming room in real time.

- **Audience Dynamics Monitoring**: Perceive audience join and leave in real time through event subscription.

- **Administrator Permissions**: The Anchor can set a general audience as administrator or revoke their administrator privileges.

- **Room Management**: The Anchor or admin can kick out any general audience from the live streaming room.


## Core Concepts

The following table introduces the core concepts of `LiveAudienceStore`:
<table>
<tr>
<td rowspan="1" colSpan="1" >**Core Concepts**</td>

<td rowspan="1" colSpan="1" >**Type**</td>

<td rowspan="1" colSpan="1" >**Core Responsibilities and Description**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[LiveUserInfo](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_live_audience_store/LiveUserInfo-class.html)</td>

<td rowspan="1" colSpan="1" >`class`</td>

<td rowspan="1" colSpan="1" >Represents a foundation Information Model for an audience (user). It contains the user's unique identifier (`userID`), Nickname (`userName`) and profile photo url (`avatarURL`).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[LiveAudienceState](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_live_audience_store/LiveAudienceState-class.html)</td>

<td rowspan="1" colSpan="1" >`class`</td>

<td rowspan="1" colSpan="1" >Represents the current status of the audience module. Its core attribute `audienceList` is a `ValueListenable<List<LiveUserInfo>>`, storing a snapshot of the audience list; `audienceCount` signifies the total number of current audience.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[LiveAudienceListener](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_live_audience_store/LiveAudienceListener-class.html)</td>

<td rowspan="1" colSpan="1" >`class`</td>

<td rowspan="1" colSpan="1" >Represents a real-time event listener for audience dynamics. It includes two callbacks, `onAudienceJoined` (audience joined) and `onAudienceLeft` (audience left), used to incrementally update the audience list.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[LiveAudienceStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_live_audience_store/LiveAudienceStore-class.html)</td>

<td rowspan="1" colSpan="1" >`class`</td>

<td rowspan="1" colSpan="1" >This is the core management class for interacting with the audience list function. Through it, you can obtain audience list snapshots, perform operation management, and receive real-time updates via `addLiveAudienceListener`.</td>
</tr>
</table>


## Implementation Steps

### Step 1: Component Integration
- **Live streaming**: Refer to [Quick Access](https://write.woa.com/document/200455640177692672) for seamless integration with **AtomicXCore** and service access.

- **Voice chat room**: Refer to [Quick Access](https://write.woa.com/document/200555778169073664) for integration with **AtomicXCore** and access completed.


### Step 2: Initialize and Obtain Audience List

Retrieve a `LiveAudienceStore` instance bound to the current live streaming room liveId, actively pull the current audience list once for first-time show.

When exiting the live streaming room, you can reclaim resources by calling the `AudienceManager`'s `dispose` method.
``` java
import 'package:atomic_x_core/atomicxcore.dart';

class AudienceManager {
    final String liveId;
    late final LiveAudienceStore audienceStore;
    late LiveAudienceListener _audienceListener;
    late final VoidCallback _audienceListChangedListener = _onAudienceListChanged;
    late final VoidCallback _audienceCountChangedListener = _onAudienceCountChanged;

    // Externally exposed [full] audience list
    List<LiveUserInfo> audienceList = [];
    // Externally exposed total audience count
    int audienceCount = 0;

    // Status change callback
    Function()? onStateChanged;

    AudienceManager({required this.liveId}) {
        // 1. Retrieve an instance of LiveAudienceStore by liveId
        audienceStore = LiveAudienceStore.create(liveId);

        // 2. Subscribe to status and events
        _subscribeToAudienceState();
        _subscribeToAudienceEvents();

        // 3. Actively pull first screen data
        fetchInitialAudienceList();
    }

    /// Proactively retrieve an audience list snapshot once
    Future<void> fetchInitialAudienceList() async {
        final result = await audienceStore.fetchAudienceList();
        if (result.isSuccess) {
            print("First pull audience list successfully");
            // Upon success, data will be auto-updated via the state subscription channel below
        } else {
            print("First pull audience list failed: ${result.errorMessage}");
        }
    }

    void dispose() {
        audienceStore.liveAudienceState.audienceList.removeListener(_audienceListChangedListener);
        audienceStore.liveAudienceState.audienceCount.removeListener(_audienceCountChangedListener);
        audienceStore.removeLiveAudienceListener(_audienceListener);
    }
}
```

The audience list and other `state` subscriptions will be explained in detail in the next step.

### Step 3: Monitoring the Audience List Status and Real-Time Updates

Subscribe to `audienceStore`'s `liveAudienceState` and `LiveAudienceListener` to receive full list snapshots and real-time audience Enter/Exit Events, thereby driving UI updates.
``` java
extension AudienceManagerSubscription on AudienceManager {
    /// Subscribe to state to obtain the total count of audience and list snapshots
    void _subscribeToAudienceState() {
        // Listen to audience list adjustments
        audienceStore.liveAudienceState.audienceList.addListener(_audienceListChangedListener);
        // Listen to audience change rate
        audienceStore.liveAudienceState.audienceCount.addListener(_audienceCountChangedListener);
    }

    void _onAudienceListChanged() {
        // audienceList is a full snapshot
        audienceList = audienceStore.liveAudienceState.audienceList.value;
        onStateChanged?.call();
    }

    void _onAudienceCountChanged() {
        // audienceCount is the real-time total count
        audienceCount = audienceStore.liveAudienceState.audienceCount.value;
        onStateChanged?.call();
    }

    /// Subscribe to events for processing real-time audience entry and exit
    void _subscribeToAudienceEvents() {
        _audienceListener = LiveAudienceListener(
            onAudienceJoined: (audience) {
                print("Audience ${audience.userName} joined the live streaming room");
                // Incremental update: Add new audience at the end of the current list
                if (!audienceList.any((a) => a.userID == audience.userID)) {
                    audienceList.add(audience);
                    onStateChanged?.call();
                }
            },
            onAudienceLeft: (audience) {
                print("Audience ${audience.userName} left the live streaming room");
                // Incremental update: Remove leaving audience from the current list
                audienceList.removeWhere((a) => a.userID == audience.userID);
                onStateChanged?.call();
            },
        );
        audienceStore.addLiveAudienceListener(_audienceListener);
    }
}
```

### Step 4: Manage Audience (Remove User and Set Administrator)

As an Anchor or admin, perform management operations on the audience in the live streaming room.

#### 4.1 Kick Out Audience From Live Streaming Room

Call the `kickUserOutOfRoom` API to remove designated users from the live streaming room.
``` java
extension AudienceManagerActions on AudienceManager {
    Future<void> kick(String userId) async {
        final result = await audienceStore.kickUserOutOfRoom(userId);
        if (result.isSuccess) {
            print("Successfully kicked user $userId out of room");
            // Upon success, you will receive the onAudienceLeft event
        } else {
            print("Failed to kick out user $userId: ${result.errorMessage}");
        }
    }
}
```

#### 4.2 Set/Revoke Admin

Use the `setAdministrator` and `revokeAdministrator` APIs to manage user administrator privileges.
``` java
extension AudienceManagerAdmin on AudienceManager {
    /// Set the user as administrator
    Future<void> promoteToAdmin(String userId) async {
        final result = await audienceStore.setAdministrator(userId);
        if (result.isSuccess) {
            print("Successfully set user $userId as administrator");
        }
    }

    /// Revoke the user's administrator privileges
    Future<void> revokeAdmin(String userId) async {
        final result = await audienceStore.revokeAdministrator(userId);
        if (result.isSuccess) {
            print("Successfully revoked user $userId's administrator privileges");
        }
    }
}
```

## Advanced Features

### Show the Welcome Message in the Bullet Screen Area

When a new audience enters the live room, the bullet screen/chat area will automatically display a welcome message locally, such as "Welcome [user nickname] to the live room."

#### Implementation Method

We subscribe to the audience join event (`onAudienceJoined`) of `LiveAudienceStore` to get real-time notifications of new audience joins. Once the event is triggered, we extract the nickname information of the new audience, then immediately call the local insert API `appendLocalTip` of `BarrageStore`.

When exiting the live streaming room, you can reclaim resources by calling the `LiveRoomManager`'s `dispose` method.
``` java
import 'package:atomic_x_core/atomicxcore.dart';

class LiveRoomManager {
    final String liveId;
    late LiveAudienceListener _welcomeListener;

    LiveRoomManager({required this.liveId}) {
        _setupWelcomeMessageFlow();
    }

    void _setupWelcomeMessageFlow() {
        // 1. Retrieve an instance of LiveAudienceStore
        final audienceStore = LiveAudienceStore.create(liveId);

        // 2. Retrieve an instance of BarrageStore (thanks to the internal mechanism, this will be the same instance)
        final barrageStore = BarrageStore.create(liveId);

        // 3. Subscribe to audience events
        _welcomeListener = LiveAudienceListener(
            onAudienceJoined: (audience) {
                // 4. Create a local Prompt message
                final welcomeTip = Barrage(
                    messageType: BarrageType.text,
                    textContent: "Welcome ${audience.userName} to the live streaming room."
                );

                // 5. Call the BarrageStore API to insert it into the bullet screen list
                barrageStore.appendLocalTip(welcomeTip);
            },
        );
        audienceStore.addLiveAudienceListener(_welcomeListener);
    }

    void dispose() {
        final audienceStore = LiveAudienceStore.create(liveId);
        audienceStore.removeLiveAudienceListener(_welcomeListener);
    }
}
```

## API documentation

For details about ALL public interfaces, properties, and methods of [LiveAudienceStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_live_audience_store/LiveAudienceStore-class.html) and its related classes, refer to the official API documentation of the [AtomicXCore](https://tencent-rtc.github.io/TUIKit_Flutter/index.html) framework. The related Store used in this document is as follows:
<table>
<tr>
<td rowspan="1" colSpan="1" >**Store/Component**</td>

<td rowspan="1" colSpan="1" >**Feature Description**</td>

<td rowspan="1" colSpan="1" >**API Reference**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**LiveCoreWidget**</td>

<td rowspan="1" colSpan="1" >The core view component for live video stream display and interaction: responsible for stream rendering and view widget processing, supporting live streaming, audience co-broadcasting, cross-room connection with other anchors, and other scenarios.</td>

<td rowspan="1" colSpan="1" >[API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_view_live_live_core_widget/LiveCoreWidget-class.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**LiveCoreController**</td>

<td rowspan="1" colSpan="1" >LiveCoreWidget controller: used to set up live streaming ID, control preview, and perform other operations.</td>

<td rowspan="1" colSpan="1" >[API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_view_live_live_core_widget/LiveCoreController-class.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**LiveAudienceStore**</td>

<td rowspan="1" colSpan="1" >Audience management: get real-time audience list (ID/name/avatar), check audience size, listen to Enter/Exit Event.</td>

<td rowspan="1" colSpan="1" >[API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_live_audience_store/LiveAudienceStore-class.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**BarrageStore**</td>

<td rowspan="1" colSpan="1" >Danmaku function: send text/custom barrage item, maintain bullet screen list, monitor in real time.</td>

<td rowspan="1" colSpan="1" >[API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_barrage_barrage_store/api_barrage_barrage_store-library.html)</td>
</tr>
</table>


## FAQs

### `LiveAudienceState` How Is the Number of Online Users (`AudienceCount`) Updated? What Is the Timing and How Often?

`audienceCount` update is not always real-time. The mechanism is as follows:
- **Proactive enter and exit rooms**: When users proactively join or normally exit live streaming room, the change notification of number of online users will immediate trigger. You will soon observe the changes of `audienceCount` in `LiveAudienceState`.

- **Unexpected disconnection**: When a user unexpectedly disconnects due to network issue, application crash, etc., the system needs to determine their actual status through heartbeat mechanism. Only when the user has no heartbeat for 90 consecutive seconds will the system deem them offline and trigger the change notification of number of users.

- **Update mechanism and frequency control:**

  - Whether it is immediate trigger or delay trigger, all change notifications of number of users are broadcast in the room in the form of messages.

  - The message total inside the room has a capacity limit per second, with a single room message frequency control of **40 messages per second**.

  - **Key points:** In scenarios with extremely high message traffic such as "bullet screen storm" or gift spam, if the message rate inside the room exceeds the threshold of 40 messages per second, to ensure the delivery of core messages (for example, bullet screen), **messages of number of users change may be dropped by the frequency control policy**.


      **What does this mean for developers?**


      `audienceCount` is a **high-precision estimate** very close to real time, but under extreme high concurrency scenarios, it may have brief delay or data loss. Therefore, we recommend that you use it for **UI display** and should not take it as the only basis for scenarios requiring absolute accuracy such as billing or statistics.
