> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

`LiveAudienceStore` is a module in `AtomicXCore` designed for managing audience information in live streaming rooms. With `LiveAudienceStore`, you can implement a comprehensive audience list and management system for your live streaming application.

## Core Features
- **Real-Time Audience List**: Retrieve and display all audience information currently present in the live room.

- **Audience Count Statistics**: Access the accurate, real-time total number of viewers in the live room.

- **Audience Activity Monitoring**: Subscribe to events to instantly detect when viewers join or leave.

- **Administrator Privileges**: The host can promote regular viewers to administrators or revoke their admin status.

- **Room Management**: The host or administrator can remove (kick out) any regular viewer from the live room.

## Core Concepts
| **Core Concept** | **Type** | **Core Responsibilities & Description** |
| --- | --- | --- |
| `LiveUserInfo` | data class | Represents the basic information model of an audience member (user). It contains the user's unique identifier (`userID`), nickname (`userName`), and avatar URL (`avatarURL`). |
| `LiveAudienceState` | data class | Represents the current state of the audience module. Its core property `audienceList` is a StateFlow that stores the real-time state of the audience list; `audienceCount` represents the real-time state of the current total number of viewers. |
| `LiveAudienceListener` | abstract class | Represents real-time audience activity events. It includes `onAudienceJoined` (audience joins) and `onAudienceLeft` (audience leaves), used for incremental updates to the audience list. |
| `LiveAudienceStore` | abstract class | This is the core management class for interacting with audience list functionality. Through it, you can obtain audience list snapshots, perform management operations, and subscribe to its `LiveAudienceListener` for real-time updates. |

## Implementation Guide

### Step 1: Component Integration
- **Video Live Streaming**: Please refer to Quick Start to integrate AtomicXCore

- **Voice Chat Room**: Please refer to Quick Start to integrate AtomicXCore.

### Step 2: Initialize and Retrieve the Audience List

Obtain a `LiveAudienceStore` instance bound to the current live room's `liveId`, and fetch the current audience list for the initial display.
``` kotlin
import kotlinx.coroutines.*
import kotlinx.coroutines.flow.*
import io.trtc.tuikit.atomicxcore.api.CompletionHandler
import io.trtc.tuikit.atomicxcore.api.live.LiveAudienceStore
import io.trtc.tuikit.atomicxcore.api.live.LiveUserInfo

class AudienceManager(
    private val liveId: String
) {
    private val audienceStore: LiveAudienceStore = LiveAudienceStore.create(liveId)
    private val scope = CoroutineScope(Dispatchers.Main)

    // Expose the [full] audience list state flow for UI layer subscription
    private val _audienceList = MutableStateFlow<List<LiveUserInfo>>(emptyList())
    val audienceList: StateFlow<List<LiveUserInfo>> = _audienceList.asStateFlow()
    
    // Expose the audience count state flow
    private val _audienceCount = MutableStateFlow(0)
    val audienceCount: StateFlow<Int> = _audienceCount.asStateFlow()
    
    init {
        // 1. Subscribe to state and events, see next section for implementation
        subscribeToAudienceState()
        subscribeToAudienceEvents()

        // 2. Actively fetch initial data for the first screen
        fetchInitialAudienceList()
    }

    /// Actively fetch a snapshot of the audience list once
    private fun fetchInitialAudienceList() {
        audienceStore.fetchAudienceList(object : CompletionHandler {
            override fun onSuccess() {
                println("Successfully fetched the initial audience list")
                // After success, the data will be automatically updated via the state subscription channel below
            }

            override fun onFailure(code: Int, desc: String) {
                println("Failed to fetch the initial audience list: $desc")
            }
        })
    }
    
    // ... subsequent code
}
```

### Step 3: Listen to Audience List State and Real-Time Activity

Subscribe to the `liveAudienceState` of `audienceStore` and add a `LiveAudienceListener` to receive full list snapshots and real-time audience join/leave events. Use these updates to drive UI changes.
``` kotlin
class AudienceManager {
    /// Subscribe to state for audience count and list snapshots
    private fun subscribeToAudienceState() {
        scope.launch {
            // audienceList is a full snapshot
            audienceStore.liveAudienceState.audienceList.collect { audienceList ->
                _audienceList.value = audienceList
            }
        }

        scope.launch {   
            // audienceCount is the real-time total
            audienceStore.liveAudienceState.audienceCount.collect { count ->
                _audienceCount.value = count
            }
        }
    }

    /// Subscribe to events to handle real-time audience join/leave
    private fun subscribeToAudienceEvents() {
        audienceStore.addLiveAudienceListener(object : LiveAudienceListener() {
            override fun onAudienceJoined(newAudience: LiveUserInfo) {
                println("Audience ${newAudience.userName} joined the live room")
                // Incremental update: add the new audience member to the end of the current list
                val currentList = _audienceList.value.toMutableList()
                if (!currentList.any { it.userID == newAudience.userID }) {
                    currentList.add(newAudience)
                    _audienceList.value = currentList
                }
            }

            override fun onAudienceLeft(departedAudience: LiveUserInfo) {
                println("Audience ${departedAudience.userName} left the live room")
                // Incremental update: remove the departed audience member from the current list
                val currentList = _audienceList.value.toMutableList()
                currentList.removeAll { it.userID == departedAudience.userID }
                _audienceList.value = currentList
            }
        })
    }
}
```

### Step 4: Manage Audience (Kick and Set Administrator)

As a host or administrator, you can manage viewers in the live room.

#### 4.1 Kick a Viewer Out of the Live Room

Call the `kickUserOutOfRoom` method to remove a specified user from the live room.
``` kotlin
class AudienceManager {
    fun kick(userId: String) {
        audienceStore.kickUserOutOfRoom(userId, object : CompletionHandler {
            override fun onSuccess() {
                println("Successfully kicked user $userId out of the room")
                // After a successful kick, you will receive an onAudienceLeft event
            }

            override fun onFailure(code: Int, desc: String) {
                println("Failed to kick user $userId: $desc")
            }
        })
    }
}
```

#### 4.2 Set or Revoke Administrator Status

Use the `setAdministrator` and `revokeAdministrator` methods to manage a user's administrator status.
``` kotlin
class AudienceManager {
    /// Promote user to administrator
    fun promoteToAdmin(userId: String) {
        audienceStore.setAdministrator(userId, object : CompletionHandler {
            override fun onSuccess() {
                println("Successfully promoted user $userId to administrator")
            }
            
            override fun onFailure(code: Int, desc: String) {
                println("Failed to set administrator: $desc")
            }
        })
    }

    /// Revoke user's administrator status
    fun revokeAdmin(userId: String) {
        audienceStore.revokeAdministrator(userId, object : CompletionHandler {
            override fun onSuccess() {
                println("Successfully revoked administrator status for user $userId")
            }

            override fun onFailure(code: Int, desc: String) {
                println("Failed to revoke administrator: $desc")
            }
        })
    }
}
```

## Advanced Features

### Display a Welcome Message in the Barrage Area When a Viewer Joins

When a new viewer enters the live room, a welcome message such as `"Welcome [user nickname] to the live room"` is automatically displayed locally in the barrage/chat area.

#### Implementation

Add a listener for the audience join event `LiveAudienceListener.onAudienceJoined` in `LiveAudienceStore` to receive real-time notifications when a new viewer joins. When triggered, extract the new viewer's nickname and call the `appendLocalTip` method of BarrageStore to insert the message locally.
``` kotlin
import io.trtc.tuikit.atomicxcore.api.live.LiveAudienceListener
import io.trtc.tuikit.atomicxcore.api.live.LiveAudienceStore
import io.trtc.tuikit.atomicxcore.api.live.LiveUserInfo
import io.trtc.tuikit.atomicxcore.api.barrage.Barrage
import io.trtc.tuikit.atomicxcore.api.barrage.BarrageStore
import io.trtc.tuikit.atomicxcore.api.barrage.BarrageType

class LiveRoomManager(
    private val liveId: String
) {

    init {
        // Initialize two core managers
        setupWelcomeMessageFlow()
    }

    private fun setupWelcomeMessageFlow() {
        // 1. Get an instance of LiveAudienceStore
        val audienceStore = LiveAudienceStore.create(liveId)

        // 2. Get an instance of BarrageStore (this will be the same instance due to internal mechanisms)
        val barrageStore = BarrageStore.create(liveId)

        // 3. Subscribe to audience events
        audienceStore.addLiveAudienceListener(object : LiveAudienceListener() {
            override fun onAudienceJoined(audience: LiveUserInfo) {
                // 4. Create a local tip message
                val welcomeTip = Barrage().apply {
                    liveID = liveId
                    messageType = BarrageType.TEXT
                    textContent = "Welcome ${audience.userName} to the live room!"
                }

                // 5. Use BarrageStore's method to insert it into the barrage list
                barrageStore.appendLocalTip(welcomeTip)
            }
        })
    }
}
```

## API Documentation

For detailed information on all public interfaces, properties, and methods of [LiveAudienceStore](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-live-audience-store/index.html) and its related classes, refer to the official API documentation included with the [AtomicX Core](https://tencent-rtc.github.io/TUIKit_Android/index.html) framework. The relevant Stores used in this document are as follows:
| **Store/Component** | **Feature Description** | **API Documentation** |
| --- | --- | --- |
| LiveCoreView | Core view component for live video stream display and interaction: responsible for video stream rendering and view widget handling, supporting scenarios such as host streaming, audience co-hosting, and host-to-host connection. | [API Documentation](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.view/-live-core-view/index.html) |
| LiveAudienceStore | Audience management: obtain real-time audience list (ID / name / avatar), count audience numbers, and listen for audience join/leave events. | [API Documentation](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.view/-live-core-view/index.html) |
| BarrageStore | Barrage feature: send text/custom barrage, maintain barrage list, and listen to barrage status in real time. | [API Documentation](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.barrage/-barrage-store/index.html) |

## FAQs

### How is the online audience count (audienceCount) in LiveAudienceState updated? What are the timing and frequency?

The update of `audienceCount` is not always strictly real-time. The mechanism is as follows:
- **Active Join/Leave**: When a user actively joins or leaves the live room, the audience count change notification is triggered instantly. You will quickly observe the change in `audienceCount` in `LiveAudienceState`.

- **Unexpected Disconnection**: If a user disconnects unexpectedly due to network issues, app crashes, and so on, the system determines their actual status using a heartbeat mechanism. Only when the user has no heartbeat for 90 consecutive seconds does the system consider them offline and trigger a count change notification.

- **Update Mechanism and Frequency Control:**

  - Whether triggered instantly or with a delay, all audience count change notifications are broadcast as messages within the room.

  - There is an upper limit to the total number of messages per second in a room, with a per-room message rate limit of 40 messages per second.

  - Key Point: In scenarios with extremely high message traffic, such as "barrage storms" or rapid-fire gifting, if the message rate in the room exceeds the 40 messages/second threshold, to ensure the delivery of core messages (such as barrage), audience count change messages may be dropped by the rate-limiting policy.

- **What does this mean for developers?**

   `audienceCount` is a near real-time, high-precision estimate, but in extreme high-concurrency scenarios, there may be brief delays or data loss. We recommend using it for UI display only, and not as the sole basis for billing, statistics, or other scenarios requiring absolute accuracy.

---

`LiveAudienceStore` is a module in `AtomicXCore` designed for managing audience information in live streaming rooms. With `LiveAudienceStore`, you can implement a comprehensive audience list and management system for your live streaming application.

## Core Features
- **Real-Time Audience List**: Fetch and display the list of users currently in the room.

- **Audience Statistics**: Get the real-time total viewer count.

- **Event Monitoring**: Listen for events when viewers join or leave the room.

- **Role Management**: The host can grant or revoke administrator privileges for viewers.

- **Room Management**: The host or administrator can remove specific viewers from the live room.

## Core Concepts
| **Core Concept** | **Type** | **Core Responsibilities & Description** |
| --- | --- | --- |
| `LiveUserInfo` | `class` | - Data model representing a viewer. - Contains basic profile information such as userID, userName, and avatarURL. |
| `LiveAudienceState` | `struct` | - State container for the audience module. - Exposes `audienceList` (StateFlow) for the real-time user list and `audienceCount` for the total viewer count. |
| `LiveAudienceEvent` | `enum` | - Event listener for audience changes. - Provides callbacks like `.onAudienceJoined` and` .onAudienceLeft` to handle incremental list updates. |
| `LiveAudienceStore` | `class` | - Primary interface for audience management. - Used to fetch list snapshots, perform admin operations (e.g., kicking users), and subscribe to real-time events. |

## Implementation

### Step 1: Component Integration
- **Video Live Streaming**: Please refer to Quick Start to integrate AtomicXCore.

- **Voice Chat Room**: Please refer to Quick Start to integrate AtomicXCore.

### Step 2: Initialize and Retrieve the Audience List

Get a `LiveAudienceStore` instance linked to the `liveId` and fetch the initial audience snapshot. 
``` swift
import Foundation
import AtomicXCore 
import Combine     

class AudienceManager {
    private let liveId: String
    private let audienceStore: LiveAudienceStore
    private var cancellables = Set<AnyCancellable>()
    
    // Expose the [full] audience list publisher for UI layer subscription
    let audienceListPublisher = CurrentValueSubject<[LiveUserInfo], Never>([])
    // Expose the audience count publisher
    let audienceCountPublisher = PassthroughSubject<UInt, Never>()

    init(liveId: String) {
        self.liveId = liveId
        // 1. Get the LiveAudienceStore instance by liveId
        self.audienceStore = LiveAudienceStore.create(liveID: liveId)
        
        // 2. Subscribe to state and events
        subscribeToAudienceState()
        subscribeToAudienceEvents()
        
        // 3. Proactively fetch initial data for the first screen
        fetchInitialAudienceList()
    }

    /// Proactively fetch a snapshot of the audience list
    func fetchInitialAudienceList() {
        audienceStore.fetchAudienceList { [weak self] result in
            switch result {
            case .success:
                print("Successfully fetched the audience list for the first time")
                // On success, data will be automatically updated via the state subscription channel below
            case .failure(let error):
                print("Failed to fetch the audience list for the first time: \(error.localizedDescription)")
            }
        }
    }
    
    // ... subsequent code
}
```

### Step 3: Subscribe to State and Events

Observe the `audienceStore` state and listen for events to receive list snapshots and real-time join/leave updates
``` swift
extension AudienceManager {
    /// Subscribe to state to get audience count and list snapshot
    private func subscribeToAudienceState() {
        audienceStore.state
            .subscribe()
            .receive(on: DispatchQueue.main)
            .sink { [weak self] state in
                // state.audienceList is a full snapshot
                self?.audienceListPublisher.send(state.audienceList)
                // state.audienceCount is the real-time total
                self?.audienceCountPublisher.send(state.audienceCount)
            }
            .store(in: &cancellables)
    }

    /// Subscribe to events to handle real-time audience join/leave
    private func subscribeToAudienceEvents() {
        audienceStore.liveAudienceEventPublisher
            .receive(on: DispatchQueue.main)
            .sink { [weak self] event in
                guard let self = self else { return }
                
                var currentList = self.audienceListPublisher.value
                
                switch event {
                case .onAudienceJoined(let newAudience):
                    print("Audience \(newAudience.userName) joined the live room")
                    // Incremental update: add the new audience member to the end of the current list
                    if !currentList.contains(where: { $0.userID == newAudience.userID }) {
                        currentList.append(newAudience)
                        self.audienceListPublisher.send(currentList)
                    }
                    
                case .onAudienceLeft(let departedAudience):
                    print("Audience \(departedAudience.userName) left the live room")
                    // Incremental update: remove the departed audience member from the current list
                    currentList.removeAll { $0.userID == departedAudience.userID }
                    self.audienceListPublisher.send(currentList)
                }
            }
            .store(in: &cancellables)
    }
}
```

### Step 4: Manage Audience

As a host or administrator, you can manage viewers in the live room.

#### 4.1 Kick a Viewer Out of the Live Room

Call the `kickUserOutOfRoom` API to remove a specified user from the live room.
``` swift
extension AudienceManager {
    func kick(userId: String) {
        audienceStore.kickUserOutOfRoom(userID: userId) { result in
            switch result {
            case .success:
                print("Successfully kicked user \(userId) out of the room")
                // After a successful kick, you will receive an onAudienceLeft event
            case .failure(let error):
                print("Failed to kick user \(userId) out: \(error.localizedDescription)")
            }
        }
    }
}
```

#### 4.2 Manage Admin Roles

Use the `setAdministrator` and `revokeAdministrator` APIs to grant or revoke administrator privileges for a user.
``` swift
extension AudienceManager {
    /// Promote user to administrator
    func promoteToAdmin(userId: String) {
        audienceStore.setAdministrator(userID: userId) { result in
            if case .success = result {
                print("Successfully promoted user \(userId) to administrator")
            }
        }
    }

    /// Revoke user's administrator status
    func revokeAdmin(userId: String) {
        audienceStore.revokeAdministrator(userID: userId) { result in
            if case .success = result {
                print("Successfully revoked administrator status for user \(userId)")
            }
        }
    }
}
```

## Advanced Features

### Display Welcome Message on Entry

When a new audience member enters the live room, a welcome message is automatically displayed locally in the barrage/chat area, such as: `"Welcome [User Nickname] to the live room"`.

#### Implementation
1. Listen for Join Events: Observe the `LiveAudienceEvent.onAudienceJoined` callback in `LiveAudienceStore` to receive real-time notifications when a new user enters.

2. Insert Local Message: Upon triggering the event, extract the user's nickname and immediately call the `appendLocalTip` API in BarrageStore to insert the system message locally.

   ``` swift
   import Foundation
   import AtomicXCore 
   import Combine
   
   class LiveRoomManager {
       private let liveId: String
       private let audienceManager: AudienceManager
       private let barrageManager: BarrageManager // Assume you have implemented BarrageManager as described in the barrage documentation
       private var cancellables = Set<AnyCancellable>()
   
       init(liveId: String) {
           self.liveId = liveId
           // Initialize two core managers
           self.audienceManager = AudienceManager(liveId: liveId)
           self.barrageManager = BarrageManager(liveId: liveId)
   
           // Set up linkage
           setupWelcomeMessageFlow()
       }
   
       private func setupWelcomeMessageFlow() {
           // 1. Get the LiveAudienceStore instance
           let audienceStore = LiveAudienceStore.create(liveID: self.liveId)
   
           // 2. Get the BarrageStore instance (thanks to internal mechanisms, this will be the same instance)
           let barrageStore = BarrageStore.create(liveID: self.liveId)
   
           // 3. Subscribe to audience events
           audienceStore.liveAudienceEventPublisher
               .receive(on: DispatchQueue.main)
               .sink { event in
                   // 4. Only handle audience join events
                   guard case .onAudienceJoined(let newAudience) = event else {
                       return
                   }
   
                   // 5. Create a local tip message
                   var welcomeTip = Barrage()
                   welcomeTip.messageType = .text 
                   welcomeTip.textContent = "Welcome \(newAudience.userName) to the live room!"
   
                   // 6. Call BarrageStore's API to insert it into the barrage list
                   barrageStore.appendLocalTip(message: welcomeTip)
               }
               .store(in: &cancellables)
       }
   }
   ```

## API Documentation

For detailed information on all public interfaces, properties, and methods of [LiveAudienceStore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/liveaudiencestore) and its related classes, refer to the official API documentation included with the [AtomicX Core](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore) framework. The relevant Stores used in this document are as follows:
| **Store/Component** | **Feature Description** | **API Documentation** |
| --- | --- | --- |
| LiveCoreView | Core view component for live video stream display and interaction: responsible for video stream rendering and view widget handling, supporting scenarios such as host streaming, audience co-hosting, and host-to-host connection. | [API Documentation](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/livecoreview) |
| LiveAudienceStore | Audience management: obtain real-time audience list (ID / name / avatar), count audience numbers, and listen for audience join/leave events. | [API Documentation](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/liveaudiencestore) |
| BarrageStore | Barrage feature: send text/custom barrage, maintain barrage list, and listen to barrage status in real time. | [API Documentation](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/barragestore) |

## FAQs

### How is the online audience count (audienceCount) in LiveAudienceState updated? What are the timing and frequency?

The `audienceCount` is a high-precision estimate. Updates occur based on specific triggers and are subject to system frequency controls:
- **Active Entry/Exit (Immediate)**:When a user explicitly joins or leaves the room, the count updates immediately in `LiveAudienceState`.

- **Unexpected Disconnection (Delayed)**:If a user disconnects abnormally (e.g., app crash, network loss), the system uses a heartbeat mechanism to verify status. The user is marked offline only after 90 seconds of inactivity, triggering a delayed count update.

- **Frequency Control & Rate Limiting**: Audience count updates are broadcast as room messages. The system enforces a limit of 40 messages per second per room.
   

   > **Note：**
   > 

   > During high-traffic spikes (e.g., chat floods or rapid gifting), if the message rate exceeds this threshold, the system prioritizes core messages (like chat/barrage). Consequently, audience count update messages may be dropped to maintain stability.
   > 

- **What does this mean for developers?**

   Treat `audienceCount` as a metric for UI display purposes only. Do not rely on it for billing, critical statistics, or scenarios requiring 100% accuracy, as brief delays or data loss may occur during high-concurrency events.
