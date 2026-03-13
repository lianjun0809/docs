> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

## Platform: Android

This document provides a comprehensive guide for iOS developers to quickly integrate a feature-rich, high-performance live chat overlay (barrage/danmaku) system into your live streaming application using the `BarrageStore` module from the **AtomicXCore** framework.

## Core Features

`BarrageStore` delivers a complete barrage solution for your live streaming app. Core features include:
- Receiving and displaying barrage messages in the live room.

- Sending text barrage messages to interact with viewers.

- Sending custom business barrage messages to support complex scenarios such as gifts and likes.

- Inserting system tips into the local message list (for example, "Welcome XX to the live room").

## Core Concepts
| **Core Concept** | **Type** | **Core Responsibility & Description** |
| --- | --- | --- |
| [Barrage](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.barrage/-barrage/index.html) | data class | Represents a single barrage message. Contains sender info (sender), message content (textContent or data), and message type (messageType). |
| [BarrageState](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.barrage/-barrage-state/index.html) | data class | Represents the current state of the barrage module. The main property, messageList, is a StateFlow containing all barrage messages for the current live room, ordered chronologically. This serves as the UI data source. |
| [BarrageStore](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.barrage/-barrage-store/index.html) | abstract class | The main manager for barrage features. Use it to send messages (sendTextMessage, sendCustomMessage) and subscribe to barrage message updates via its state property. |

## Implementation

### Step 1: Component Integration
- **Video Live Streaming**: Please refer to Quick Start to integrate AtomicXCore.

- **Voice Chat Room**: Please refer to Quick Start to integrate AtomicXCore.

### Step 2: Initialize and Listen to Barrages

Create a `BarrageStore` instance bound to the current live room's `liveId`, and subscribe to receive the latest barrage message list in real time.
``` kotlin
import kotlinx.coroutines.*
import kotlinx.coroutines.flow.*
import io.trtc.tuikit.atomicxcore.api.barrage.Barrage
import io.trtc.tuikit.atomicxcore.api.barrage.BarrageStore

class BarrageManager(
    private val liveId: String
) {
    private val barrageStore: BarrageStore = BarrageStore.create(liveId)
    private val scope = CoroutineScope(Dispatchers.Main)
    
    // Expose the [full] message list as a Flow for the UI layer to subscribe to
    private val _messagesFlow = MutableStateFlow<List<Barrage>>(emptyList())
    val messagesFlow: StateFlow<List<Barrage>> = _messagesFlow.asStateFlow()
    
    init {
        // Start listening for barrage messages immediately after initialization
        subscribeToBarrageUpdates()
    }

    private fun subscribeToBarrageUpdates() {
        scope.launch {
            barrageStore.barrageState.messageList
                .collect { messageList ->
                    // When messageList updates, pass the new list to the UI layer via Flow
                    // Note: This is the [complete list], including all historical messages
                    _messagesFlow.value = messageList
                }
        }
    }
}
```

### Step 3: Send Text Barrages

Use `sendTextMessage` to broadcast a plain text message to all users in the live room.
``` kotlin
import io.trtc.tuikit.atomicxcore.api.CompletionHandler
import io.trtc.tuikit.atomicxcore.api.barrage.BarrageStore

class BarrageManager(
    private val liveId: String
) {
    private val barrageStore: BarrageStore = BarrageStore.create(liveId)

    // Send a text barrage
    fun sendTextMessage(text: String) {
        // We recommend adding a non-empty check to avoid sending invalid messages
        if (text.isEmpty()) {
            return
        }
        
        // Call the core API to send the message
        barrageStore.sendTextMessage(
            text,
            mapOf(
                "custom key" to "custom value",
            ),
            object : CompletionHandler {
                override fun onSuccess() {
                    println("Text barrage '$text' sent successfully")
                }

                override fun onFailure(code: Int, desc: String) {
                    println("Failed to send text barrage: $desc")
                }
            }
        )
    }
}
```

#### API Parameters
| **Parameter** | **Type** | **Description** |
| --- | --- | --- |
| `text` | `String?` | The text content to send. |
| `extensionInfo` | `Map<String, String>?` | Additional data for business customization. |
| `completion` | `CompletionHandler?` | Callback invoked after sending, indicating success or failure. |

### Step 4: Send Custom Barrage

Send messages with custom business logic, such as gifts, likes, or gamification commands. The content format of this message is defined by the business layer. The receiver must parse and handle it based on the `businessId` and `data`.
``` kotlin
class BarrageManager(
    private val liveId: String
) {
    // Send a custom barrage, for example, to send a gift
    fun sendGiftMessage(giftId: String, giftCount: Int) {
        // 1. Define a business-recognizable ID
        val businessId = "live_gift"

        // 2. Encode business data as a JSON string
        val giftData = mapOf(
            "gift_id" to giftId,
            "gift_count" to giftCount
        )

        val jsonString = try {
            // Use Gson or another JSON library for serialization
            // Here we assume Gson is used
            Gson().toJson(giftData)
        } catch (e: Exception) {
            return
        }

        // 3. Call the core API to send the custom message
        barrageStore.sendCustomMessage(
            businessId,
            jsonString,
            object : CompletionHandler {
                override fun onSuccess() {
                    println("Gift message (custom barrage) sent successfully")
                }
                
                override fun onFailure(code: Int, desc: String) {
                    println("Failed to send gift message: $desc")
                }
            }
        )
    }
}
```

#### API Parameters
| **Parameter** | **Type** | **Description** |
| --- | --- | --- |
| businessId | String | Unique business identifier (e.g., "live_gift"). Used by receivers to distinguish custom messages. |
| data | String | Business data, typically a JSON string. |
| completion | CompletionHandler? | Callback after sending. |

### Step 5: Insert Local Tip Messages

Insert a local message into the current user's message list. This message is not sent to other users and is ideal for displaying system prompts, warnings, or operation tips.
``` kotlin
class BarrageManager(
    private val liveId: String
) {
    // Insert a welcome tip into the local message list
    fun showWelcomeMessage(user: LiveUserInfo) {
        // 1. Create a Barrage message
        val welcomeTip = Barrage(
            liveID = liveId,
            messageType = BarrageType.TEXT, // You can reuse the text type for display
            textContent = "Welcome ${user.userName} to the live room!",
            sender = LiveUserInfo() // sender can be left empty or set to a system user identifier
        )

        // 2. Call the API to append it to the local list
        barrageStore.appendLocalTip(welcomeTip)
    }
}
```

#### API Parameters
| **Parameter** | **Type** | **Description** |
| --- | --- | --- |
| message | Barrage | The message object to insert locally. The SDK appends this to messageList in BarrageState. |

### Step 6: Manage User Speaking Permissions (Mute and Unmute)

As a host or administrator, you can control user messaging permissions to maintain a healthy community environment.

#### Mute/Unmute a Single User

Use the `disableSendMessage` method in `LiveAudienceStore` to mute or unmute a user. This state persists even if the user rejoins the live room.
``` kotlin
import io.trtc.tuikit.atomicxcore.api.*
import io.trtc.tuikit.atomicxcore.api.live.LiveAudienceStore

// 1. Get the LiveAudienceStore instance bound to the current live room
val audienceStore = LiveAudienceStore.create(liveId)

// 2. Define the user ID to operate on and the mute status
val userIdToMute = "user_id_to_be_muted"
val shouldDisable = true // true to mute, false to unmute

// 3. Call the interface to perform the operation
audienceStore.disableSendMessage(
    userIdToMute,
    shouldDisable,
    object : CompletionHandler {
        override fun onSuccess() {
            println("${if (shouldDisable) "Muted" else "Unmuted"} user $userIdToMute successfully")
        }

        override fun onFailure(code: Int, desc: String) {
            println("Operation failed: $desc")
        }
    }
)
```

#### Enable/Disable Global Mute

To mute all users in the live room (usually excluding the host), update the live room information via `LiveListStore`.
``` kotlin
import io.trtc.tuikit.atomicxcore.api.CompletionHandler
import io.trtc.tuikit.atomicxcore.api.live.LiveInfo
import io.trtc.tuikit.atomicxcore.api.live.LiveListStore

// 1. Get the LiveListStore singleton
val liveListStore = LiveListStore.shared()

// 2. Get the current live room info and modify the global mute status
val currentLiveInfo = liveListStore.liveState.currentLive.value.copy(
    isMessageDisable = true // true to enable global mute, false to disable
)

// 3. Call the update interface and specify the modification flag
liveListStore.updateLiveInfo(
    currentLiveInfo,
    listOf(LiveInfo.ModifyFlag.IS_MESSAGE_DISABLE),
    object : CompletionHandler {
        override fun onSuccess() {
            println("Global mute status updated successfully")
        }

        override fun onFailure(code: Int, desc: String) {
            println("Operation failed: $desc")
        }
    }
)
```

## Advanced Features: Performance Optimization in High-Concurrency Scenarios

After implementing barrage features with `BarrageStore`, use the following strategies to ensure smooth and stable user experiences in high-concurrency live streaming scenarios. This section provides optimization strategies and code samples for three core business scenarios.

### Scenario 1: Handling "Barrage Storms" in Popular Live Rooms

#### Scenario Description

During popular events, a large number of viewers may flood into the live room, with barrages updating at dozens of messages per second.

#### Technical Challenge

The SDK returns the complete barrage list at a high frequency. If you call `adapter.notifyDataSetChanged()` on every update, the main thread may be blocked by intensive UI layout and rendering, causing UI lag.

#### Optimization: Batch Processing & Debouncing

Do not respond to every data update. Instead, set a time threshold (e.g., 300 ms). Only refresh the UI if the time since the last update exceeds this threshold. This reduces dozens of `notifyDataSetChanged()`calls per second to just 3–4, greatly improving smoothness.

#### Code Example

Create a `BarrageUIManager` class with a buffer and timer for batch updating data to the `RecyclerView`.
``` kotlin
import android.os.Handler
import androidx.recyclerview.widget.RecyclerView
import io.trtc.tuikit.atomicxcore.api.barrage.Barrage

private const val UPDATE_DURATION_MS = 300L

class BarrageUIManager() {
    private var timestampOnLastUpdate = 0L

    private var dataSource: ArrayList<Barrage> = ArrayList()
    private val updateViewTask = Runnable { notifyDataSetChanged() }
    private val handler = Handler()
    private val adapter = BarrageAdapter(dataSource)

    // This method is called frequently from outside, passing in the latest full list
    fun update(newList: List<Barrage>) {
        handler.removeCallbacks(updateViewTask)
        dataSource.clear()
        dataSource.addAll(newList)
        // If the refresh interval is less than 0.3 seconds, do not refresh
        if (System.currentTimeMillis() - timestampOnLastUpdate < UPDATE_DURATION_MS) {
            handler.postDelayed(updateViewTask, UPDATE_DURATION_MS)
            return
        }
    }

    private fun notifyDataSetChanged() {
        adapter.notifyDataSetChanged()
        timestampOnLastUpdate = System.currentTimeMillis()
    }
}

class BarrageAdapter(dataSource: ArrayList<Barrage>): RecyclerView.Adapter<RecyclerView.ViewHolder>() {
    // Implement adapter capabilities here
}
```

### Scenario 2: Ensuring Memory Stability for Long-Duration Live Streams

#### Scenario Description

Your app may need to support hours-long or even all-day continuous live streaming, such as game streaming or slow live streams. The app must remain stable and avoid crashes due to long-term operation.

#### Technical Challenge

The SDK returns a full `messageList` that grows indefinitely during long live streams. Even if the UI layer throttles updates, a large array in the data layer will continue consuming memory and may eventually cause the app to crash.

#### Optimization: Circular Buffer with Fixed Capacity

Ensure your data source holds only a limited number of messages. Regardless of the size of the full list returned by the SDK, only retain the latest portion for display.

#### Code Example

After receiving the full list from the SDK, take only the latest 500 messages (or another number you define) to update the UI.
``` kotlin
class BarrageUIManager(
    private val recyclerView: RecyclerView
) {
    private val capacity: Int = 500 // Only retain the latest 500 messages
    // ... (other code as above) ...

    private fun refreshUIIfNeeded() {
        val fullList = this.latestMessageList ?: return
        val adapter = recyclerView.adapter ?: return
        this.latestMessageList = null 

        // Only take the latest N messages
        val cappedList = fullList.takeLast(capacity)
        
        dataSource.clear()
        dataSource.addAll(cappedList)
        adapter.notifyDataSetChanged()
    }
}
```

### Scenario 3: Rendering Complex Barrage Styles with User Levels and Badges

#### Scenario Description

To enhance the live streaming atmosphere and highlight paying users, barrage messages may include rich visual elements such as usernames, user level icons, fan badges, and message content.

#### Technical Challenge

Rendering views with multiple images and texts, custom fonts, or complex layouts is more time-consuming than rendering plain text. High-frequency rendering of these complex views in a list increases the main thread's workload, causing lag during list scrolling.

#### Optimization: Asynchronous Drawing

Move the view rendering process off the main thread and onto a background thread. The main thread should only handle the final display of the already rendered bitmap, significantly reducing its computational load.

#### Code Example

In your custom `RecyclerView.ViewHolder`, use `AsyncLayoutInflater` or a preloading mechanism to perform rendering tasks on a background thread whenever possible.
``` kotlin
import android.view.LayoutInflater
import androidx.asynclayoutinflater.view.AsyncLayoutInflater
import androidx.recyclerview.widget.RecyclerView

// In your custom Barrage ViewHolder
class BarrageViewHolder(
    itemView: View
) : RecyclerView.ViewHolder(itemView) {

    // ... (Declarations for TextView, ImageView, etc.)

    companion object {
        fun create(parent: ViewGroup): BarrageViewHolder {
            // Use async layout inflater to reduce main thread blocking
            val inflater = AsyncLayoutInflater(parent.context)
            val view = LayoutInflater.from(parent.context)
                .inflate(R.layout.item_barrage, parent, false)
            return BarrageViewHolder(view)
        }
    }

    fun bind(viewModel: BarrageViewModel) {
        // Set your TextView text, ImageView images, etc. here
        // With async layout inflation, final rendering is done on a background thread whenever possible
    }

    // Advanced performance optimization: fully manual drawing
    // For finer control, use Canvas to manually draw text and images
    // Generate the Bitmap on a background thread, then draw it in the main thread's onDraw method for fully asynchronous rendering
}
```

## API Documentation

For detailed information on all public interfaces, properties, methods of [BarrageStore](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.barrage/-barrage-store/index.html) and its related classes, refer to the official API documentation included with the [AtomicXCore](https://tencent-rtc.github.io/TUIKit_Android/index.html) framework.

## FAQs

### In addition to basic text barrages, we also want to implement richer styles such as "colored barrages" and "gift barrages." How can we achieve this?

You can implement these features using custom messages with `sendCustomMessage`. 

**Implementation Steps**
1. **Define the Data Structure**: Collaborate with your client and server teams to define the JSON structure for custom messages. For example, a colored barrage can be defined as:

   ``` json
   {  "type": "colored_text",  "text": "This is a colored bullet comment!",  "color": "#FF5733" }
   ```
2. **Sender**: When sending, serialize this JSON structure to a string and send it via the `data` parameter of `sendCustomMessage`. The businessID can be set to a unique identifier for your use case, such as `barrage_style_v1`.

3. **Receiver**: Upon receiving a barrage message, check whether its messageType is `BarrageType.CUSTOM` and whether the `businessID` matches. If so, parse the data string (usually as JSON), and render your custom UI style based on the parsed data (such as `color`, `text`).

### If I call BarrageStore.create(liveID = "some_id") in different classes or files, will this create multiple instances and cause confusion?

No. The internal mechanism of **AtomicXCore** ensures that as long as you pass in the same `liveID`, you always get the same `BarrageStore` instance for that live room. You do not need to manage singletons manually.

### Why can't I see the message I sent after calling sendTextMessage in the message list?

**Troubleshooting steps:**
1. **Check the completion callback**: The `sendTextMessage` method provides a completion callback. Check whether the callback indicates success or failure. If it fails, the error message will indicate the problem (such as "You have been muted," "Network error," etc.).

2. **Confirm subscription timing**: Make sure you subscribe to `barrageStore.barrageState.messageList` after the live session for the corresponding `liveID` has started. If you start listening before joining the live room, you may miss some messages.

3. **Check liveID**: Ensure that the liveID used when creating the BarrageStore instance, joining the live room, and sending messages is exactly the same, including case sensitivity.

4. **Network issues**: Ensure the device's network connection is normal. Message sending depends on network connectivity.

### How can new viewers see historical barrage messages sent before they joined the live room?

`AtomicXCore` supports retrieving historical chat messages, but you need to enable this feature in the **server console**. Once configured, the SDK handles everything automatically—no additional client code is required.

#### **Step 1: Configure in the Live Console**
1. Log in to [**Console > Live > Configuration**](https://console.trtc.io/live/configuration), and select your target application at the top of the page.

2. On the Live Configuration page, select **View Past Messages**, and set Previous Messages Viewable to specify the number of messages (up to a maximum of 50) that new viewers can see.

   

#### **Step 2: Automatic Retrieval on the Client Side**

After completing the above configuration, **no changes are needed** in your client code.

When a new user joins the live room, `AtomicXCore` automatically retrieves the configured number of historical chat messages in the background. These messages are delivered to the UI layer through the `BarrageState` subscription channel, just like real-time messages. Your application will receive and display these historical chat messages in the same way as live messages.

---

## Platform: iOS

This document provides a comprehensive guide for iOS developers to quickly integrate a feature-rich, high-performance live chat overlay (barrage/danmaku) system into your live streaming application using the `BarrageStore` module from the **AtomicXCore** framework.

## Core Features

`BarrageStore` delivers a complete barrage solution for your live streaming app. Core features include:
- Receiving and displaying barrage messages in the live room.

- Sending text barrage messages to interact with viewers.

- Sending custom business barrage messages to support complex scenarios such as gifts and likes.

- Inserting system tips into the local message list (for example, "Welcome XX to the live room").

## Core Concepts
| **Core Concept** | **Type** | **Core Responsibility & Description** |
| --- | --- | --- |
| [Barrage](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/barrage) | struct | Represents the data model for a single barrage message. Contains all essential information such as sender (sender), message content (textContent or data), message type (messageType), and more. |
| [BarrageState](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/barragestate) | struct | Represents the current state of the barrage module. The main property, messageList, is an array of [Barrage] storing all barrage messages in chronological order for the current live room. This serves as the data source for UI rendering. |
| [BarrageStore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/barragestore) | class | The core management class for barrage functionality. Use it to send messages (sendTextMessage, sendCustomMessage), and subscribe to its state property to receive all barrage message updates. |

## Implementation

### Step 1: Component Integration
- **Video Live Streaming**: Please refer to Quick Start to integrate AtomicXCore. Quick Start to

- **Voice Chat Room**: Please refer to Quick Start to integrate AtomicXCore.

### Step 2: Initialize and Listen for Barrage

Obtain a `BarrageStore` instance bound to the current live room's `liveId`, and set up a subscriber to receive the latest complete barrage message list in real time.
``` swift
import Foundation
import AtomicXCore // Import the core library
import Combine     // For reactive programming

class BarrageManager {
    private let liveId: String
    private let barrageStore: BarrageStore
    private var cancellables = Set<AnyCancellable>()
    
    // Publisher for the complete message list, for UI layer subscription
    let messagesPublisher = PassthroughSubject<[Barrage], Never>()
    
    init(liveId: String) {
        self.liveId = liveId
        // 1. Obtain the BarrageStore singleton for the given liveId
        self.barrageStore = BarrageStore.create(liveID: liveId)
        // 2. Start listening for barrage messages immediately after initialization
        subscribeToBarrageUpdates()
    }
    
    private func subscribeToBarrageUpdates() {
        barrageStore.state
            .subscribe() // Subscribe to all BarrageState changes
            .receive(on: DispatchQueue.main) // Ensure main thread for UI safety
            .sink { [weak self] barrageState in
                // 3. Forward the updated message list to the UI layer
                // Note: This provides the complete list, including all historical messages
                self?.messagesPublisher.send(barrageState.messageList)
            }
            .store(in: &cancellables) // Manage subscription lifecycle
    }

```

### Step 3: Send Text Barrage

Use the `sendTextMessage` method to broadcast a plain text message to all users in the live room.
``` swift
extension BarrageManager {
    /// Send a text barrage message
    func sendTextMessage(text: String) {
        // Prevent sending empty messages
        guard !text.isEmpty else {
            print("Barrage content cannot be empty")
            return
        }
        
        // Send the message using the core API
        barrageStore.sendTextMessage(text: text, extensionInfo: nil) { result in
            // Handle the result in the callback, e.g., show a prompt to the user
            switch result {
            case .success:
                print("Text barrage '\(text)' sent successfully")
            case .failure(let error):
                print("Failed to send text barrage: \(error.localizedDescription)")
            }
        }
    }
}
```

#### API Parameters
| **Parameter** | **Type** | **Description** |
| --- | --- | --- |
| `text` | `String` | The text content to send. |
| `extensionInfo` | `[String: String]?` | Additional extension information for business customization. |
| `completion` | `CompletionClosure?` | Callback after sending is complete, containing the success or failure result. |

### Step 4: Send Custom Barrage

Send a message containing custom business logic, such as gifts, likes, or gamification commands. The content format of this message is defined by the business layer. The receiver must parse and handle it based on the `businessId` and `data`.
``` swift
extension BarrageManager {
    /// Send a custom barrage, e.g., for sending gifts
    func sendGiftMessage(giftId: String, giftCount: Int) {
        // 1. Define a business-recognizable ID
        let businessId = "live_gift"
        
        // 2. Encode business data as a JSON string
        let giftData: [String: Any] = ["gift_id": giftId, "gift_count": giftCount]
        guard let jsonData = try? JSONSerialization.data(withJSONObject: giftData),
              let jsonString = String(data: jsonData, encoding: .utf8) else {
            print("Failed to encode gift data as JSON")
            return
        }
        
        // 3. Send the custom message using the core API
        barrageStore.sendCustomMessage(businessID: businessId, data: jsonString) { result in
            switch result {
            case .success:
                print("Gift message (custom barrage) sent successfully")
            case .failure(let error):
                print("Failed to send gift message: \(error.localizedDescription)")
            }
        }
    }
}
```

#### API Parameters
| **Parameter** | **Type** | **Description** |
| --- | --- | --- |
| `businessId` | `String` | Unique business identifier, e.g., "live_gift", used by the receiver to distinguish different custom messages. |
| `data` | `String` | Business data, usually a JSON-formatted string. |
| `completion` | `CompletionClosure?` | Callback after sending is complete. |

### Step 5: Insert Local Tip Message

Insert a local message into the current user's message list. This message is not sent to other users in the live room. Use this for system welcomes, warnings, or action tips.
``` swift
extension BarrageManager {
    /// Insert a welcome tip into the local message list
    func showWelcomeMessage(for user: LiveUserInfo) {
        // 1. Create a Barrage message
        var welcomeTip = Barrage()
        welcomeTip.messageType = .text // Reuse the text type for display
        welcomeTip.textContent = "Welcome \(user.userName) to the live room!"
        // sender can be left empty or set to a system user identifier
        
        // 2. Insert the message into the local list
        barrageStore.appendLocalTip(message: welcomeTip)
    }
}
```

#### API Parameters
| **Parameter** | **Type** | **Description** |
| --- | --- | --- |
| message | Barrage | The message object to insert locally. The SDK appends this message to the messageList in BarrageState. |

### Step 6: Manage User Speaking Permissions (Mute and Unmute)

As a host or administrator, you can manage users' chat permissions in the live room to maintain a healthy community environment.

#### Mute/Unmute a Single User

Use the `disableSendMessage` method in `LiveAudienceStore` to mute or unmute a user. This state persists even if the user rejoins the live room.
``` swift
import AtomicXCore

// 1. Get the LiveAudienceStore instance for the current live room
let audienceStore = LiveAudienceStore.create(liveID: "your_live_id")

// 2. Specify the user ID and mute status
let userIdToMute = "user_id_to_be_muted"
let shouldDisable = true // true to mute, false to unmute

// 3. Call the API to perform the operation
audienceStore.disableSendMessage(userID: userIdToMute, isDisable: shouldDisable) { [weak self] result in
    guard let self = self else { return }
    switch result {
    case .success:
        print("\(shouldDisable ? "Muted" : "Unmuted") user \(userIdToMute) successfully")
    case .failure(let error):
        print("Operation failed: \(error.localizedDescription)")
    }
}
```

#### Enable/Disable Global Mute

To mute all users in the live room (usually excluding the host), update the live room information via `LiveListStore`.
``` swift
import AtomicXCore

// 1. Get the LiveListStore singleton
let liveListStore = LiveListStore.shared

// 2. Get the current live room info and modify the global mute status
var currentLiveInfo = liveListStore.state.value.currentLive 
currentLiveInfo.isMessageDisable = true // true to enable global mute, false to disable

// 3. Call the update API and specify the modify flag
liveListStore.updateLiveInfo(currentLiveInfo, modifyFlag: .isMessageDisable) { result in
    switch result {
    case .success:
        print("Global mute status updated successfully")
    case .failure(let error):
        print("Operation failed: \(error.localizedDescription)")
    }
}
```

## Advanced Features: Performance Optimization in High-Concurrency Scenarios

After implementing barrage features with `BarrageStore`, use the following strategies to ensure smooth and stable user experiences in high-concurrency live streaming scenarios. This section provides optimization strategies and code samples for three core business scenarios.

### Scenario 1: Handling "Barrage Storms" in Popular Live Rooms

#### Scenario Description

During popular events, a large number of viewers may flood into the live room, with barrages updating at dozens of messages per second.

#### Technical Challenge

The SDK returns the complete barrage list at a high frequency. If you call `tableView.reloadData()` on every update, the main thread will be blocked by intensive UI layout and rendering, causing UI lag.

#### Optimization: Batch Processing & Debouncing

Do not respond to every data update. Instead, set a time threshold (e.g., 300 milliseconds). Only refresh the UI if this threshold has passed since the last refresh. This reduces dozens of `reloadData()` calls per second to just 3-4, greatly improving smoothness.

#### Code Example

Create a `BarrageUIManager` class with an internal buffer and timer to batch update data to the `UITableView`.
``` swift
class BarrageUIManager {
    private var latestMessageList: [BarrageViewModel]?
    private var refreshTimer: Timer?
    private weak var tableView: UITableView?
    private var dataSource: [BarrageViewModel] = []

    init(tableView: UITableView) {
        self.tableView = tableView
        // Check every 0.3 seconds if a refresh is needed
        self.refreshTimer = Timer.scheduledTimer(withTimeInterval: 0.3, repeats: true) { [weak self] _ in
            self?.refreshUIIfNeeded()
        }
    }

    /// Frequently called from outside, passing in the latest full list
    func update(with fullList: [BarrageViewModel]) {
        self.latestMessageList = fullList
    }

    private func refreshUIIfNeeded() {
        // Check if there is new data to refresh
        guard let newList = self.latestMessageList, let tableView = self.tableView else { return }
        self.latestMessageList = nil // Clear the flag to avoid repeated refreshes

        // Update the data source and refresh the UI
        self.dataSource = newList
        tableView.reloadData()
    }

    deinit {
        refreshTimer?.invalidate()
    }
}
```

### Scenario 2: Ensuring Memory Stability for Long-Duration Live Streams

#### Scenario Description

Your app may need to support hours-long or even all-day continuous live streaming, such as game streaming or slow live streams. The app must remain stable and avoid crashes due to long-term operation.

#### Technical Challenge

The SDK returns a full `messageList` that grows indefinitely during long live streams. Even if the UI layer throttles updates, the data layer's large array will continue to consume memory, eventually causing the app to crash.

#### Optimization: Circular Buffer with Fixed Capacity

Ensure your data source holds only a limited number of messages. Regardless of the size of the full list returned by the SDK, only retain the latest portion for display.

#### Code Example

After receiving the full list from the SDK, take only the latest 500 messages (or another number you define) to update the UI.
``` swift
class BarrageUIManager {
    private let capacity: Int = 500 // Retain only the latest 500 messages
    // ... (other code as above) ...

    private func refreshUIIfNeeded() {
        guard let fullList = self.latestMessageList, let tableView = self.tableView else { return }
        self.latestMessageList = nil 

        // Only keep the latest N messages
        let cappedList = Array(fullList.suffix(self.capacity))

        self.dataSource = cappedList
        tableView.reloadData()
    }
}
```

### Scenario 3: Rendering Complex Barrage Styles with User Levels and Badges

#### Scenario Description

To enhance the live streaming atmosphere and highlight paying users, barrage messages may include rich visual elements such as usernames, user level icons, fan badges, and message content.

#### Technical Challenge

Rendering views with multiple images and texts, custom fonts, or complex layouts is more time-consuming than rendering plain text. High-frequency rendering of these complex views in a list increases the main thread's workload, causing lag during list scrolling.

#### Optimization: Asynchronous Drawing

Move the view rendering process off the main thread and onto a background thread. The main thread should only handle the final display of the already rendered bitmap, significantly reducing its computational load.

#### Code Example

In your custom `UITableViewCell`, enable the layer's `drawsAsynchronously` property to allow the system to perform drawing tasks on a background thread.
``` swift
import UIKit

// In your custom barrage cell
class BarrageCell: UITableViewCell {

    // ... (UILabel, UIImageView, and other subview declarations)

    override init(style: UITableViewCell.CellStyle, reuseIdentifier: String?) {
        super.init(style: style, reuseIdentifier: reuseIdentifier)

        // Enable asynchronous drawing
        self.layer.drawsAsynchronously = true
    }

    required init?(coder: NSCoder) {
        fatalError("init(coder:) has not been implemented")
    }

    func configure(with viewModel: BarrageViewModel) {
        // Set label text, images, etc.
        // With asynchronous drawing enabled, rendering occurs on a background thread when possible
    }

    // Advanced: fully manual drawing
    override func draw(_ rect: CGRect) {
        // For finer control, manually draw text and images here using Core Graphics
        // Combine generating UIImage on a background thread, then draw it in the main thread's draw method for fully asynchronous rendering
    }
}
```

## API Documentation

For detailed information on all public interfaces, properties, and methods of [BarrageStore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/barragestore) and related classes, refer to the official API documentation included with the [AtomicXCore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore) framework.

## FAQs

### In addition to basic text barrages, we also want to implement richer styles such as "colored barrages" and "gift barrages." How can we achieve this?

You can implement these features using custom messages with `sendCustomMessage`. 

**Implementation Steps**
1. **Define the Data Structure**: Collaborate with your client and server teams to define the JSON structure for custom messages. For example, a colored barrage can be defined as:

   ``` json
   {  "type": "colored_text",  "text": "This is a colored bullet comment!",  "color": "#FF5733" }
   ```
2. **Sender**: When sending, serialize this JSON structure to a string and send it via the `data` parameter of `sendCustomMessage`. The businessID can be set to a unique identifier for your use case, such as `barrage_style_v1`.

3. **Receiver**: Upon receiving a barrage message, check whether its messageType is `BarrageType.CUSTOM` and whether the `businessID` matches. If so, parse the data string (usually as JSON), and render your custom UI style based on the parsed data (such as `color`, `text`).

### If I call BarrageStore.create(liveID = "some_id") in different classes or files, will this create multiple instances and cause confusion?

No. The internal mechanism of **AtomicXCore** ensures that as long as you pass in the same liveID, you always get the same `BarrageStore` instance for that live room. You do not need to manage singletons manually.

### Why can't I see the message I sent after calling sendTextMessage in the message list?

**Troubleshooting steps:**
1. **Check the completion callback**: The `sendTextMessage` method provides a completion callback. Check whether the callback indicates success or failure. If it fails, the error message will indicate the problem (such as "You have been muted," "Network error," etc.).

2. **Confirm subscription timing**: Make sure you subscribe to `barrageStore.barrageState.messageList` after the live session for the corresponding liveID has started. If you start listening before joining the live room, you may miss some messages.

3. **Check liveID**: Ensure that the liveID used when creating the BarrageStore instance, joining the live room, and sending messages is exactly the same, including case sensitivity.

4. **Network issues**: Ensure the device's network connection is normal. Message sending depends on network connectivity.

### How can new viewers see historical barrage messages sent before they joined the live room?

`AtomicXCore` supports retrieving historical chat messages, but you need to enable this feature in the **server console**. Once configured, the SDK handles everything automatically—no additional client code is required.

#### **Step 1: Configure in the Live Console**
1. Log in to [**Console > Live > Configuration**](https://console.trtc.io/live/configuration), and select your target application at the top of the page.

2. On the Live Configuration page, select **View Past Messages**, and set Previous Messages Viewable to specify the number of messages (up to a maximum of 50) that new viewers can see.

   

#### **Step 2: Automatic Retrieval on the Client Side**

After completing the above configuration, **no changes are needed** in your client code.

When a new user joins the live room, `AtomicXCore` automatically retrieves the configured number of historical chat messages in the background. These messages are delivered to the UI layer through the `BarrageState` subscription channel, just like real-time messages. Your application will receive and display these historical chat messages in the same way as live messages.

---

## Platform: Flutter

This document aims to guide Flutter developers on how to use the `BarrageStore` module in the `AtomicXCore` framework to quickly integrate a bullet screen system with various features and outstanding performance for your live stream app.

## Core Features

`BarrageStore` provides a complete bullet screen solution for your live stream app. Core features include:
- Receive and show danmakus information in live rooms.

- Send text bullet screen for audience interaction.

- Send custom business bullet screen to support complex scenarios such as gift and likes.

- Insert a system prompt in the local message list (for example, "Welcome XX to enter live room").

## Core Concept Analysis
| **Core Concept** | **Type** | **Core Responsibility and Description** |
| --- | --- | --- |
| [Barrage](https://tencent-rtc.github.io/TUIKit_Flutter/api_barrage_barrage_store/Barrage-class.html) | `class` | Represents a data model for a Danmu Message. It contains all key information such as sender information (`sender`), message content (`textContent` or `data`), and message type (`messageType`). |
| [BarrageState](https://tencent-rtc.github.io/TUIKit_Flutter/api_barrage_barrage_store/BarrageState-class.html) | `class` | Represents the current status of the bullet screen module. Its core attribute `messageList` is a `ValueListenable<List<Barrage>>`, storing all Danmu messages in the live streaming room in chronological order, serving as the data source for UI rendering. |
| [BarrageStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_barrage_barrage_store/BarrageStore-class.html) | `class` | This is the core management class for danmu function interaction. Through it, you can send messages (`sendTextMessage`, `sendCustomMessage`) and receive and listen to ALL Danmu Message updates by listening to its `barrageState.messageList` property. |

## Implementation Steps

### Step 1: Integrating the Component
- **Live streaming**: Refer to quick integration for seamless integration with **AtomicXCore** and service access.

- **Voice chat room**: Refer to quick integration for seamless integration with **AtomicXCore** and service access.

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
| **Parameter** | **Type** | **Description** |
| --- | --- | --- |
| `text` | `String` | The text content to be sent. |
| `extensionInfo` | `Map<String, String>?` | Attach extra extended information applicable to business customization. |

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
| **Parameter** | **Type** | **Description** |
| --- | --- | --- |
| `businessID` | `String` | Business unique identifier, such as "live_gift", used for recipient to distinguish different custom messages. |
| `data` | `String` | Business data, typically strings in JSON format. |

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

   

   **Step 2: Client Seamless Retrieval**

   After completing the above configuration, your client-side code **requires no modification**. 

   When a new user joins the live room, the `AtomicXCore` underlying layer will automatically pull your configuration history message count. These historical messages will be pushed to your UI layer through your realized `BarrageStore.barrageState` subscription channel, just like real-time messages. Your application will naturally receive and show these historical bullet screens, same as receiving real-time bullet screens.

---

## Platform: Vue

This document provides a detailed introduction to the **barrage component**, including the **barrage message component (BarrageList)** and the **message sending component (BarrageInput)**. You can refer to the sample code in this document for seamless integration of our pre-developed components into your existing project, or customize the style and layout according to your needs by following the component customization section in the document.

## Component Composition
| **Component Name** | **Detailed Description** |
| --- | --- |
| **Barrage Message Component (BarrageList)** | A component responsible for real-time display and management of barrage message streams, providing a complete message display solution including **message list rendering, time aggregation, user interaction, and responsive adaptation**. |
| **Message Sending Component (BarrageInput)** | An input component that provides rich text editing and message sending features, with seamless integration of **emoji selector, character limit, status management, and cross-platform adaptation**, offering users a smooth input experience. |

## Component Integration

### Step 1: Configuring the Environment and Activating the Service

Before performing quick integration, you need to refer to preparations, meet the related environment configuration and activate the corresponding service.

### Step 2: Installing Dependencies

【npm】
``` bash
npm install tuikit-atomicx-vue3@latest @tencentcloud/uikit-base-component-vue3 --save
```

【pnpm】
``` bash
pnpm add tuikit-atomicx-vue3@latest @tencentcloud/uikit-base-component-vue3
```

【yarn】
``` bash
yarn add tuikit-atomicx-vue3@latest @tencentcloud/uikit-base-component-vue3
```

### Step 3: Integrating the Barrage Component

Introduce and use the barrage component in your project. You can copy the following example directly to show **a complete live streaming room barrage message component and message send component** in your project.
``` typescript
<template>
  <UIKitProvider theme="dark" language="en-US">
    <div class="app">
      <div class="chat-container">
        <div class="chat-content">
          <BarrageList class="barrage-list" />
        </div>
        <div class="chat-input">
          <BarrageInput class="barrage-input" />
        </div>
      </div>
    </div>
  </UIKitProvider>
</template>

<script setup lang="ts">
import { onMounted, ref } from 'vue';
import { UIKitProvider } from '@tencentcloud/uikit-base-component-vue3';
import { BarrageList, BarrageInput, useLoginState, useLiveState } from 'tuikit-atomicx-vue3';

const { login, loginUserInfo } = useLoginState();
const { joinLive } = useLiveState();

async function initLogin() {
  try {
    await login({
      sdkAppId: 0,        // SDKAppID, see Step 1 to get
      userId: '',         // UserID, see Step 1 to get
      userSig: '',        // userSig, see Step 1 to get
    });
  } catch (error) {
    console.error('login error:', error);
  }
}

onMounted(async () => {
  await initLogin();
  await joinLive({
    liveId: 'input corresponding live streaming room LiveId',     // enter live room by inputting corresponding liveId
  });
});
</script>

<style scoped>.app{width:100vw;height:100vh;display:flex;justify-content:center;align-items:center;padding:20px;box-sizing:border-box}.chat-container{width:100%;max-width:500px;height:600px;border-radius:16px;display:flex;flex-direction:column;overflow:hidden}.chat-content{flex:1;overflow:hidden}.barrage-list{width:100%;height:100%}.chat-input{background-color:var(--bg-color-dialog);padding:16px}.barrage-input{width:100%}</style>
```

## Customize Component

**Barrage Message Component** provides users with various and dimensional `Props` APIs for custom requirements, allowing users to customize features or UI. Parameter content is as shown in the table below.

> **Note:**
> 

> Note: To directly learn about the custom details of the Barrage Message Component (BarrageList), quickly jump to the following link: Barrage Message Component Customization;
> 

> Note: To directly learn about the custom details of the Message Sending Component (BarrageInput), quickly jump to the following link: Message Sending Component Customization;
> 

### Barrage Message Component (BarrageList) Customization

#### **Props**
| **Parameter Name** | **Parameter Type** | **Default Value** | **Description** |
| --- | --- | --- | --- |
| messageAggregationTime | Number | 300 | Maximum time interval for message grouping (seconds). |
| filter | (message: IMessageModel) => boolean | - | Functions for filtering messages. |
| Message | Component | Message | Custom Message Component |
| MessageTimeDivider | Component | MessageTimeDivider | Custom Message Time Segmentation Component. |
| LocalNoticeMessage | Component | LocalNoticeMessage | Custom Local Notification Component. |
| containerStyle | CSSProperties | - | Custom message list container style. |
| itemStyle | CSSProperties | - | Custom single message item style. |
| height | String | - | Component height, supports CSS units. |
| style | CSSProperties | - | Specify the root element's custom style. |

As indicated in the table above, the Props custom part of the Barrage Message Component consists of three sections: **component properties, replaceable subcomponents, and custom styles.** Specific content is as shown in the table below.
| **Content** | **Parameter** |
| --- | --- |
| **Component Property** | `filter`,`messageAggregationTime` |
| **Replaceable subcomponent** | `Message`,`MessageTimeDivider`,`LocalNoticeMessage` |
| **Custom style** | `ContainerStyle`,`ItemStyle`,`height`,`style` |

#### Filter Message

By setting the `filter` parameter, you can flexibly control the message content displayed in the barrage message component.
``` typescript
<BarrageList :filter="(message) => message.type === 'TIMTextElem'" />
```

#### Message Aggregation Time

By setting the `messageAggregationTime` parameter, you can control the grouping time interval.
``` typescript
<BarrageList :messageAggregationTime="300" />
```

#### Custom Style

Barrage Message Component provides `containerStyle`, `itemStyle`, `custom child component`, etc., for customizing component styles.
1. To customize the message list container style, you can pass a style object to the `containerStyle` attribute.

   **Example: Custom container padding**

   ``` typescript
   <BarrageList :containerStyle="{ padding: '0px' }" />
   ```
2. To customize a single message style, you can pass a style object to the `itemStyle` attribute.

   **Example: Custom message item spacing, border, and message bubble color**

   ``` typescript
   <BarrageList :itemStyle="{ borderRadius: '10px', background: '#1C66e5', padding: '10px', boxSizing: 'border-box'}" />
   ```
3. The barrage message component supports custom message display components, and you can fully control the rendering method.

   **Example: Custom Message Component**

   ``` typescript
   // MyCustomMessage.vue
   <template>
     <div class="custom-message">
       <div class="message-header">
         <span class="user-name">{{ getUserName(message) }}</span>
         <span class="message-time">{{ formatTime(message.time) }}</span>
       </div>
       <div class="message-content">
         {{ getMessageText(message) }}
       </div>
     </div>
   </template>
   
   <script setup lang="ts">
   interface SimpleMessage {
     id: string;
     from: string;
     nick?: string;
     nameCard?: string;
     time: number;
     type: string;
     content: string;
     avatar?: string;
   }
   
   interface Props {
     message: SimpleMessage;
     isLastInChunk?: boolean;
   }
   
   const props = defineProps<Props>();
   
   const formatTime = (timestamp: number) => {
     return new Date(timestamp * 1000).toLocaleTimeString('zh-CN', {
       hour: '2-digit',
       minute: '2-digit'
     });
   };
   
   const getUserName = (message: SimpleMessage) => {
     return message.nameCard || message.nick || message.from || 'anonymous user';
   };
   
   const getMessageText = (message: SimpleMessage) => {
     if (message.type === 'text') {
       return message.content || '';
     } else if (message.type === 'image') {
       return '[image message]';
     } else if (message.type === 'emoji') {
       return '[emoji message]';
     }
     return '[other types of messages]';
   };
   </script>
   
   <style scoped>.custom-message{background:linear-gradient(135deg,#667eea 0%,#764ba2 100%);color:white;padding:12px;border-radius:12px;margin:4px 0;box-shadow:0 2px 8px rgba(0,0,0,0.1);transition:transform 0.2s ease}.custom-message:hover{transform:translateY(-2px)}.message-header{display:flex;justify-content:space-between;align-items:center;margin-bottom:8px;font-size:12px;opacity:0.9}.user-name{font-weight:500;max-width:120px;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}.message-time{font-size:11px;opacity:0.7}.message-content{font-size:14px;line-height:1.4;word-break:break-word}</style>
   
   // Use the barrage message component for use in
   <template>
      <BarrageList :Message="MyCustomMessage" />
   </template>
   
   <script setup lang="ts">
   import MyCustomMessage from "./MyCustomMessage.vue";
   </script>
   ```
| **Before modification** | **After modification** |  |  |
| --- | --- | --- | --- |
| **Custom container padding** | **Custom message item spacing and border** | **Custom Message Component** |  |
|  |  |  |  |

### Message Sending Component (BarrageInput) Customization

#### **Props**
| **Parameter Name** | **Type** | **Default Value** | **Description** |
| --- | --- | --- | --- |
| containerClass | String | '' | Custom container CSS class name. |
| containerStyle | Record | {} | Inline style of custom container. |
| width | String | - | Component width, supports CSS units. |
| height | String | - | Component height, supports CSS units. |
| minHeight | String | '40px' | Minimum component height, supports CSS units. |
| maxHeight | String | '140px' | Max component height, supports CSS units. |
| placeholder | String | - | Placeholder text in the input box. |
| disabled | Boolean | false | Whether to disable the input box. |
| autoFocus | Boolean | true | Whether to auto-focus into the input box. |
| maxLength | Number | 80 | Maximum character limit for input content. |

#### **Events**
| **Event Name** | **Parameter** | **Description** |
| --- | --- | --- |
| focus | - | Trigger when the input box gets focus. |
| blur | - | Trigger when the input box loses focus. |

As indicated in the table above, the Props custom part of the Message Sending Component consists of three sections: **size control, input restriction, and custom styles.** Specific content is as shown in the table below.
| **Content** | **Parameter** |
| --- | --- |
| **Size control** | `width`,`height`,`minHeight`,`minWidth` |
| **Input restriction** | `maxLength` |
| **Custom style** | `ContainerStyle`,`ContainerClass` |

#### Size Control

By setting `width`, `height`, `minHeight`, `maxHeight` parameters, you can flexibly control the size of **BarrageInput**.
``` typescript
<BarrageInput width="400px" height="60px" minHeight="40px" maxHeight="120px" />
```

#### Input Restriction

By setting the `maxLength` parameter, you can control the maximum number of characters for input content.
``` typescript
<BarrageInput :maxLength="100" />
```

#### Custom Style

The message send component provides `containerStyle` and `containerClass` attributes for customizing component style.
1. To customize the input box container style, you can pass a style object to the `containerStyle` attribute.

   **Example: Custom container background and border rounded corners**

   ``` typescript
   <BarrageInput :containerStyle="{ backgroundColor: '#a8abb2', borderRadius: '0 0', boxShadow: '0 2px 8px rgba(0,0,0,0.1)'}" />
   ```
2. To customize the input box container class name, you can pass a class name string to the `containerClass` attribute.

   **Example: Custom container class name**

   ``` typescript
   <template>
     <BarrageInput containerClass="my-custom-input-container" />
   </template>
   
   <style>.my-custom-input-container {background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);border: none;border-radius: 20px;padding: 8px 20px;}.my-custom-input-container:focus-within {box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.3);}</style>
   ```
| **Before modification** | **After modification** |  |
| --- | --- | --- |
| **Custom container background and border rounded corners** | **Custom message item spacing and border** |  |
|  |  |  |
