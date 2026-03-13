> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

`GiftStore` is a dedicated module within **AtomicXCore** for managing live room gifting features. It enables you to build a complete gifting system for your live streaming application, supporting robust monetization and interactive experiences.
| **Gift Panel** | **Barrage Gift** | **Full-Screen Gift** |
| --- | --- | --- |
|  |  |  |

## Core Features
- **Gift List Retrieval**: Retrieve gift panel data from the server, including gift categories and details.

- **Send Gift**: Viewers can send selected gifts and specify the quantity to the host.

- **Gift Event Broadcast:** Receive real-time gift events in the room for displaying gift animations and barrage notifications.

## Core Concepts
| **Core Concept** | **Type** | **Core Responsibilities & Description** |
| --- | --- | --- |
| `Gift` | `data class` | Represents a gift data model, including ID, name, icon URL, animation resource URL (resourceURL), price (coins), and more. |
| `GiftCategory` | `data class` | Represents a gift category (e.g., "Popular", "Luxury"). Contains the category name and a list of Gift objects. |
| `GiftState` | `data class` | Represents the current state of the gift module. The core property, usableGifts, is a StateFlow containing the full gift list from the server. |
| `GiftEvent` | `abstract class` | Defines the event listener for gift events in the live room. Currently, only onReceiveGift is available; all users in the room receive this event when any user sends a gift. |
| `GiftStore` | `abstract class` | The core management class for gift features. Use it to fetch the gift list, send gifts, and receive gift events via listeners. |

## Implementation

### Step 1: Component Integration

> **Note：**
> 

> To use the gifting system, activate either the **Free Trial,** or **Pro **edition. The number of configurable gifts depends on the selected package. For details, see the **Gift System** section in Feature and Billing Description and choose the package that fits your needs.
> 

- **Video Live Streaming**: Please refer to Quick Start to integrate AtomicXCore.

- **Voice Chat Room**: Please refer to Quick Start to integrate AtomicXCore.

### Step 2: Initialize and Listen for Gift Events

Obtain a `GiftStore` instance and set up listeners to receive gift events and updates to the gift list.

#### Implementation
1. **Get Instance**: Use `GiftStore.create(liveID) `to obtain a `GiftStore` instance for the current live room.

2. **Add Listener**: Add a `GiftListener` to receive `onReceiveGift` events.

3. **Subscribe to State**: Subscribe to `giftStore.giftState.usableGifts`to receive gift list updates.

#### Code Example
``` kotlin
import io.trtc.tuikit.atomicxcore.api.gift.Gift
import io.trtc.tuikit.atomicxcore.api.gift.GiftCategory
import io.trtc.tuikit.atomicxcore.api.gift.GiftListener
import io.trtc.tuikit.atomicxcore.api.gift.GiftStore
import io.trtc.tuikit.atomicxcore.api.live.LiveUserInfo
import kotlinx.coroutines.flow.StateFlow
import kotlinx.coroutines.flow.MutableStateFlow
import kotlinx.coroutines.flow.asStateFlow
import kotlinx.coroutines.CoroutineScope
import kotlinx.coroutines.Dispatchers
import kotlinx.coroutines.launch

class GiftManager(
    private val liveId: String
) {
    private val giftStore: GiftStore = GiftStore.create(liveId)
    private val coroutineScope = CoroutineScope(Dispatchers.Main)
    // Expose gift list externally
    private val _giftList = MutableStateFlow<List<GiftCategory>>(emptyList())
    val giftList: StateFlow<List<GiftCategory>> = _giftList.asStateFlow()

    init {
        setupGiftListener()
        subscribeToGiftState()
    }

    // Subscribe to gift events
    private fun setupGiftListener() {
        giftStore.addGiftListener(object : GiftListener() {
            override fun onReceiveGift(liveID: String, gift: Gift, count: Int, sender: LiveUserInfo) {
                // Forward event to UI layer for processing
            }
        })
    }

    // Subscribe to gift list state
    private fun subscribeToGiftState() {
        coroutineScope.launch(Dispatchers.Main) {
            giftStore.giftState.usableGifts.collect { giftList ->
                _giftList.value = giftList
            }
        }
    }
}
```

#### Gift List Structure Parameters
- **GiftCategory Parameter Description**

| **Parameter** | **Type** | **Description** |
| --- | --- | --- |
| `categoryID` | `String` | Unique ID of the gift category. |
| `name` | `String` | Display name of the gift category. |
| `desc` | `String` | Description of the gift category. |
| `extensionInfo` | `Map<String, String>` | Extension information field. |
| `giftList` | `List` | Array of Gift objects in this category. |

- **Gift Parameter Description**

| **Parameter** | **Type** | **Description** |
| --- | --- | --- |
| `giftID` | `String` | Unique ID of the gift. |
| `name` | `String` | Display name of the gift. |
| `desc` | `String` | Description of the gift. |
| `iconURL` | `String` | Gift icon URL. |
| `resourceURL` | `String` | Gift animation resource URL. |
| `level` | `Long` | Gift level. |
| `coins` | `Long` | Gift price. |
| `extensionInfo` | `Map<String, String>` | Extension information field. |

### Step 3: Retrieve Gift List

Call the `refreshUsableGifts` method to fetch gift data from the server.

#### Implementation
1. **Call API**: Call `giftStore.refreshUsableGifts()` at the appropriate time (e.g., after entering the live room).

2. **Handle Callback**: Optionally handle the completion callback to determine the result.

3. **Receive Data**: After a successful fetch, the updated usableGifts list is delivered automatically via your subscription to `giftStore.giftState.usableGifts`.

#### Code Example
``` kotlin
class GiftManager(
    private val liveId: String
) {
    private val giftStore: GiftStore = GiftStore.create(liveId)

    // Refresh the gift list from the server
    fun fetchGiftList() {
        giftStore.refreshUsableGifts(object : CompletionHandler {
            override fun onSuccess() {
                println("Gift list fetched successfully")
                // Data will be updated via the giftState subscription
            }

            override fun onFailure(code: Int, desc: String) {
                println("Failed to fetch gift list: $desc")
            }
        })
    }
}
```

### Step 4: Send Gift

When a user selects a gift and clicks send, call the `sendGift` API.

#### Implementation
1. **Get Parameters**: Obtain the selected `giftID` and `quantity (count)` from the UI.

2. **Call API**: Call `giftStore.sendGift(giftID, count, completion)`.

3. **Handle Callback**: Use the completion `callback` to handle failures (e.g., insufficient balance). UI updates (animations, barrage) after a successful send should be triggered by the `onReceiveGift` event.

#### Code Example
``` kotlin
class GiftManager(
    private val liveId: String
) {
    private val giftStore: GiftStore = GiftStore.create(liveId)

    // Send a gift
    fun sendGift(giftID: String, count: Int) {
        giftStore.sendGift(giftID, count, object : CompletionHandler {
            override fun onSuccess() {
                println("Gift $giftID sent successfully")
                // All users, including the sender, will receive the onReceiveGift event
            }

            override fun onFailure(code: Int, desc: String) {
                println("Gift send failed: $desc")
                // Prompt user if needed, e.g., "Insufficient balance" or "Network error"
            }
        })
    }
}
```

#### **sendGift API Parameters**
| **Parameter Name** | **Type** | **Description** |
| --- | --- | --- |
| `giftID` | `String` | Unique ID of the gift to send. |
| `count` | `Int` | Number of gifts to send. |
| `completion` | `CompletionHandler?` | Callback invoked after sending completes. |

## Advanced Features

The capabilities of `GiftStore` are closely tied to your backend services. This section explains how to build a feature-rich gifting system through server-side configuration and client integration.

### Gift Asset Configuration

Customize available gift types, categories, names, icons, prices, and animation effects to meet your operational and branding requirements.

#### Implementation
1. **Server-Side Configuration**: Use the `LiveKit` server REST API to manage gift information, categories, and multi-language support. See the Gift Configuration Guide.

2. **Client Fetch**: On the client, call `refreshUsableGifts` to retrieve configuration data.

3. **UI Display**: Use the retrieved `List<GiftCategory>` to populate the gift panel.

#### Configuration Sequence Diagram

#### Related REST API Interfaces Overview
| **Interface Category** | **Interface** | **Request Example** |
| --- | --- | --- |
| **​Gift Management** | Add Gift Information | Example |
| Delete Gift Information | Example |  |
| Query Gift Information | Example |  |
| **Gift Category Management** | Add Gift Category Information | Example |
| Delete Specific Gift Category Information | Example |  |
| Get Specific Gift Category Information | Example |  |
| **Gift Relationship Management** | Add Relationship between a Specific Gift Category and Gift | Example |
| Delete Relationship between a Specific Gift Category and Gift | Example |  |
| Get Gift Relationships under a Specific Gift Category | Example |  |
| **Gift Multi-language Management** | Add Gift Multi-language Information | Example |
| Delete Specific Gift Multi-language Information | Example |  |
| Get Gift Multi-language Information | Example |  |
| Add Gift Category Multi-language Information | Example |  |
| Delete Specific Gift Category Multi-language Information | Example |  |
| Get Gift Category Multi-language Information | Example |  |

### Billing and Gift Deduction Process

When a viewer sends a gift, ensure their account balance is sufficient and complete the deduction before triggering the gift effect playback and broadcast.

#### Implementation
1. **Backend Callback Configuration**: Configure your billing system's callback URL in the LiveKit backend. See Callback Configuration Documentation.

2. **Client Send**: The client calls `sendGift`.

3. **Backend Interaction**: The LiveKit backend calls your callback URL; your billing system processes the deduction and returns the result.

4. **Result Synchronization**: If successful, **AtomicXCore** broadcasts the `onReceiveGift` event; if failed, the completion callback of sendGift receives an error.

#### Call Flow

#### Related REST API Interfaces Overview
| **Interface** | **Description** | **Request Example** |
| --- | --- | --- |
| **Callback Configuration - Callback before sending a gift** | The customer's backend can use this callback to decide whether to pass pre-gifting checks, etc. | Example |

### Implement Full-Screen Gift Animation Playback

When a user sends a luxury gift (e.g., "Rocket", "Carnival"), play a full-screen animation (such as SVGA) to enhance engagement.

#### Implementation

**AtomicXCore** does not include a built-in gift animation player. Integrate a third-party library based on your requirements. Below is a comparison of two options:
| **Comparison Item** | **Basic Solution (SVGAPlayer)** | **Gift AR (TCEffectPlayerKit)** |
| --- | --- | --- |
| Billing | Free (open source) | Paid (requires license). See [Billing Guide](https://trtc.io/document/69949?product=beautyar&menulabel=core%20sdk&platform=android#X-Series-Capabilities) |
| Integration Method | Manual integration via Gradle | Requires additional integration and authentication |
| Supported Animation Formats | SVGA only | SVGA, PAG, WebP, Lottie, MP4, and more |
| Performance | Recommended SVGA file size ≤ 10MB | Supports larger files, better performance for complex/multiple/low-end scenarios |
| Recommended Scenario | Uniform SVGA format, controllable file size | Multiple formats or higher performance/device compatibility needs |

This section demonstrates the basic solution. For the **Gift AR** see the [TCEffectPlayer Integration Guide](https://trtc.io/document/70531?product=beautyar&menulabel=core%20sdk&platform=android).

#### Basic Solution: Using SVGAPlayer
1. **Integrate SVGAPlayer**: Add the SVGAPlayer dependency to your build.gradle and sync the project.

   ``` gradle
   dependencies {
       // ... other dependencies
       implementation 'com.github.yyued:SVGAPlayer-Android:2.6.1'
   }
   ```
2. **Listen for Gift Events**: Subscribe to the `GiftListener` in `GiftStore`.

3. **Parse and Play**: On `onReceiveGift`, check if `gift.resourceURL` is a valid SVGA file. Use `SVGAParser` to parse and play the animation.

#### Code Example
``` kotlin
import android.os.Bundle
import androidx.appcompat.app.AppCompatActivity
import com.opensource.svgaplayer.SVGAParser
import com.opensource.svgaplayer.SVGAVideoEntity
import com.opensource.svgaplayer.SVGAImageView
import io.trtc.tuikit.atomicxcore.api.gift.Gift
import io.trtc.tuikit.atomicxcore.api.gift.GiftListener
import io.trtc.tuikit.atomicxcore.api.gift.GiftStore
import io.trtc.tuikit.atomicxcore.api.live.LiveUserInfo
import java.net.URL

class LiveRoomActivity : AppCompatActivity() {
    private lateinit var giftStore: GiftStore
    private lateinit var svgaImageView: SVGAImageView
    private lateinit var svgaParser: SVGAParser

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_live_room)
        setupSVGAPlayer()
    }

private fun setupSVGAPlayer() {
        svgaImageView = findViewById(R.id.svga_player)
        svgaParser = SVGAParser(this)
        svgaImageView.visibility = android.view.View.GONE
        
        // Set the gift animation to play only once.
        svgaImageView.loops = 1
        
        // Set a completion callback to hide and clean up resources after playback.
        svgaImageView.callback = object : SVGACallback {
            override fun onFinished() {
                svgaImageView.visibility = android.view.View.GONE
                svgaImageView.clear()
            }
            override fun onPause() {}
            override fun onRepeat() {}
            override fun onStep(frame: Int, percentage: Double) {}
        }
    }

    fun setupGiftSubscription(liveId: String) {
        giftStore = GiftStore.create(liveId)

        giftStore.addGiftListener(object : GiftListener() {
            override fun onReceiveGift(liveID: String, gift: Gift, count: Int, sender: LiveUserInfo) {
                if (gift.resourceURL.isNotEmpty()) {
                    try {
                        val url = URL(gift.resourceURL)
                        playAnimation(url)
                    } catch (e: Exception) {
                        println("Invalid animation URL: ${gift.resourceURL}")
                    }
                }
            }
        })
    }
    
    private fun playAnimation(url: URL) {
        svgaParser.decodeFromURL(url, object : SVGAParser.ParseCompletion {
            override fun onComplete(videoItem: SVGAVideoEntity) {
                runOnUiThread {
                    svgaImageView.setVideoItem(videoItem)
                    svgaImageView.visibility = android.view.View.VISIBLE
                    svgaImageView.startAnimation()
                }
            }
            
            override fun onError() {
                println("SVGA animation parsing failed")
                // Optionally add retry or error reporting
            }
        })
    }
}
```

### Display Gift Messages in the Barrage Area

When a user sends a gift, display a system message in the public barrage area (e.g., "[Viewer Nickname] sent [Gift Name] x [Quantity]") for all viewers.

#### Implementation
1. **Listen for Events**: Subscribe to the `GiftListener` in `giftStore`.

2. **Obtain Information**: On `onReceiveGift`, extract the sender, gift, and count.

3. **Get Barrage Store**: Use `BarrageStore.create(liveID)` for the current room.

4. **Compose Message**: Create a Barrage object, set `messageType = BarrageType.TEXT`, and set textContent to your message.

5. **Insert Locally**: Call `barrageStore.appendLocalTip(message: giftTip)` to add the message to the local barrage list.

#### Code Example
``` kotlin
import io.trtc.tuikit.atomicxcore.api.barrage.Barrage
import io.trtc.tuikit.atomicxcore.api.barrage.BarrageStore
import io.trtc.tuikit.atomicxcore.api.barrage.BarrageType
import io.trtc.tuikit.atomicxcore.api.gift.Gift
import io.trtc.tuikit.atomicxcore.api.gift.GiftListener
import io.trtc.tuikit.atomicxcore.api.gift.GiftStore
import io.trtc.tuikit.atomicxcore.api.live.LiveUserInfo

class LiveRoomManager(
    private val liveId: String
) {
    private val giftStore: GiftStore = GiftStore.create(liveId)
    private val barrageStore: BarrageStore = BarrageStore.create(liveId)

    private fun setupGiftToBarrageFlow() {
        giftStore.addGiftListener(object : GiftListener() {
            override fun onReceiveGift(liveID: String, gift: Gift, count: Int, sender: LiveUserInfo) {
                val tipText = "sent ${gift.name} x $count"
                val giftTip = Barrage(
                    liveID = liveID,
                    messageType = BarrageType.TEXT,
                    textContent = tipText
                    sender = sender
                )
                barrageStore.appendLocalTip(giftTip)
            }
        })
    }
}
```

## API Documentation

For complete details on all public interfaces, properties, and methods of [GiftStore](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.gift/-gift-store/index.html) and related classes, see the official API documentation for [AtomicXCore](https://tencent-rtc.github.io/TUIKit_Android/index.html). Key stores referenced in this guide include:
| **Store/Component** | **Feature Description** | **API Documentation** |
| --- | --- | --- |
| GiftStore | Gift interactions: fetch gift list, send/receive gifts, listen for gift events (including sender and gift details). | [API Documentation](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.gift/-gift-store/index.html) |
| BarrageStore | Barrage features: send text/custom barrage, maintain barrage list, listen to barrage status in real time. | [API Documentation](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.barrage/-barrage-store/index.html) |

## FAQs

### The gift list in GiftStore is empty. What should I do?

You must call `refreshUsableGifts(completion)` to fetch gift data from your backend. Ensure your backend is configured with gift data via the server REST API.

### How do I implement multi-language display for gifts (e.g., Chinese, English)?

Use the `GiftStore.setLanguage(language: String)` API before calling `refreshUsableGifts`, passing the target language code (e.g., "en" or "zh-CN"). The server will return gift names and descriptions in the specified language.

### I called sendGift, but the gift animation plays twice. Why?

The `onReceiveGift` event is broadcast to all room members, including the sender. If you update the UI both in the sendGift completion callback and in the `onReceiveGift` event, the animation will play twice.
- **Best Practice**: Only update the UI (e.g., play animations, show barrage) in the `onReceiveGift` event handler. Use the `sendGift` completion callback only for handling failures (such as "Send failed" or "Insufficient balance").

### Where is the gift deduction logic implemented?

Gift deduction is handled entirely by your billing system. AtomicXCore integrates with your billing system via a backend callback. When the client calls sendGift, your backend performs the deduction. After returning the result to the AtomicXCore backend, it determines whether to broadcast the gift event.

### Will gift notifications be blocked by mute or message frequency controls?

No. Gift notifications (`onReceiveGift` events) are not affected by mute or frequency controls and are always delivered reliably.

### What should I do if gift animation playback stutters?

Check your SVGA file size; the basic player recommends files no larger than 10MB. For large or complex animations, consider integrating the **Gift AR** provided by TUILiveKit for improved performance.

---

`GiftStore` is a dedicated module within **AtomicXCore** for managing live room gifting features. It enables you to build a complete gifting system for your live streaming application, supporting robust monetization and interactive experiences.
| **Gift Panel** | **Barrage Gift** | **Full-Screen Gift** |
| --- | --- | --- |
|  |  |  |

## Core Features
- **Gift List Retrieval**: Retrieve gift panel data from the server, including gift categories and details.

- **Send Gift**: Viewers can send virtual gifts to the host.

- **Gift Event Broadcasting:** Real-time synchronization of gift events across all clients in the room to trigger animations and barrage notifications.

## Core Concepts
| **Core Concept** | **Type** | **Core Responsibilities & Description** |
| --- | --- | --- |
| `Gift` | `struct` | Represents a gift data model, including ID, name, icon URL, animation resource URL (resourceURL), price (coins), and more. |
| `GiftCategory` | `struct` | - Represents a grouping of gifts (e.g., "Popular", "Luxury").  - Contains a category name and an array of Gift objects. |
| `GiftState` | `struct` | - Represents the current state of the gift module.  - The core property, usableGifts, is a StateFlow containing the full gift list from the server. |
| `GiftEvent` | `enum` | Defines the event listener for gift events in the live room. Currently, only `onReceiveGift` is available. This event is broadcast to all users in the room (including the sender) whenever a gift is successfully sent. |
| `GiftStore` | `class` | - The core management class for gift features.  - Used to fetch gift lists, execute send requests, and listen for global gift events. |

## Implementation

### Step 1: Component Integration

> **Note：**
> 

> To use the gifting system, activate either the **Free Trial,** or **Pro **edition. The number of configurable gifts depends on the selected package. For details, see the **Gift System** section in Feature and Billing Description and choose the package that fits your needs.
> 

- **Video Live Streaming**: Please refer to Quick Start to integrate AtomicXCore.

- **Voice Chat Room**: Please refer to Quick Start to integrate AtomicXCore.

### Step 2: Initialize and Listen for Gift Events

Obtain a `GiftStore` instance and set up subscribers to receive gift events and gift list updates.

#### Implementation
1. **Get Instance**: Call `GiftStore.create(liveID:)` to obtain a `GiftStore` instance bound to the current live room.

2. **Subscribe to Events**: Subscribe to `giftStore.giftEventPublisher` to receive `.onReceiveGift` events.

3. **Subscribe to State**: Subscribe to `giftStore.state` to obtain the `usableGifts` gift list.

#### Code Example
``` swift
import Foundation
import AtomicXCore 
import Combine     

class GiftManager {
    private let liveId: String
    private let giftStore: GiftStore
    private var cancellables = Set<AnyCancellable>()
    
    // Expose gift events for the UI layer to subscribe and trigger animations
    let giftEventPublisher = PassthroughSubject<GiftEvent, Never>()
    // Expose gift list externally
    let giftListPublisher = CurrentValueSubject<[GiftCategory], Never>([])

    init(liveId: String) {
        self.liveId = liveId
        // 1. Obtain GiftStore instance using liveId
        self.giftStore = GiftStore.create(liveID: liveId)
        
        subscribeToGiftState()
        subscribeToGiftEvents()
    }

    /// 2. Subscribe to gift events
    private func subscribeToGiftEvents() {
        giftStore.giftEventPublisher
            .receive(on: DispatchQueue.main)
            .sink { [weak self] event in
                // Forward the event to the UI layer for handling
                self?.giftEventPublisher.send(event)
            }
            .store(in: &cancellables)
    }
    
    /// 3. Subscribe to gift list state
    private func subscribeToGiftState() {
        giftStore.state
            .subscribe(StatePublisherSelector(keyPath: \GiftState.usableGifts))
            .receive(on: DispatchQueue.main)
            .assign(to: \.value, on: giftListPublisher)
            .store(in: &cancellables)
    }
}
```

#### Gift List Struct Parameters
- **GiftCategory Parameter Description**

| **Parameter** | **Type** | **Description** |
| --- | --- | --- |
| `categoryID` | `String` | Unique ID of the gift category. |
| `name` | `String` | Display name of the gift category. |
| `desc` | `String` | Description of the gift category. |
| `extensionInfo` | `[String: String]` | Extension information field. |
| `giftList` | `[`[Gift](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/gift)`]` | Array of Gift objects contained in this category. |

- **Gift Parameter Description**

| **Parameter** | **Type** | **Description** |
| --- | --- | --- |
| `giftID` | `String` | Unique ID of the gift. |
| `name` | `String` | Display name of the gift. |
| `desc` | `String` | Description of the gift. |
| `iconURL` | `String` | Gift icon URL. |
| `resourceURL` | `String` | Gift animation resource URL. |
| `level` | `UInt` | Gift level. |
| `coins` | `UInt` | Gift price. |
| `extensionInfo` | `[String: String]` | Extension information field. |

### Step 3: Retrieve Gift List

Call the `refreshUsableGifts` method to fetch gift data from the server.

#### Implementation
1. **Call API**: Call `giftStore.refreshUsableGifts` (typically after entering the room).

2. **Handle Callback**: Handle the completion block for error checking.

3. **Receive Data**: Upon success, the data flows automatically through the giftListPublisher set up in Step 2.

#### Code Example
``` swift
extension GiftManager {
    /// Refresh the gift list from the server
    func fetchGiftList() {
        giftStore.refreshUsableGifts { result in
            switch result {
            case .success:
                print("Gift list fetched successfully")
                // On success, data is automatically updated via the state subscription
            case .failure(let error):
                print("Failed to fetch gift list: \(error.localizedDescription)")
            }
        }
    }
}
```

### Step 4: Send Gift

Trigger the sending logic when a user interacts with the gift panel.

#### Implementation
1. **Prepare Data**: Retrieve the selected `giftID` and quantity (`count`) from your UI.

2. **Call API**: Call `giftStore.sendGift(giftID:count:completion:)`.

3. **Handle Result**: Use the completion block only to handle failures (e.g., balance errors). Successful sends are handled via the global `.onReceiveGift` event listener to ensure consistency.

#### Code Example
``` swift
extension GiftManager {
    /// User sends a gift
    func sendGift(giftID: String, count: UInt) {
        giftStore.sendGift(giftID: giftID, count: count) { result in
            switch result {
            case .success:
                print("Gift \(giftID) sent successfully")
                // After a successful send, everyone in the room, including the sender, will receive the onReceiveGift event
            case .failure(let error):
                print("Failed to send gift: \(error.localizedDescription)")
                // Prompt the user, e.g., "Insufficient balance" or "Network error"
            }
        }
    }
}
```

#### sendGift API Parameters
| **Parameter Name** | **Type** | **Description** |
| --- | --- | --- |
| `giftID` | `String` | The unique ID of the gift to send. |
| `count` | `UInt` | The number of gifts to send. |
| `completion` | `CompletionClosure?` | Callback after sending is complete. |

## Advanced Features

The `GiftStore` module is designed to work seamlessly with your backend infrastructure. This section outlines how to configure assets and integrate advanced playback features.

### Gift Asset Configuration

You can fully customize your gift inventory (names, icons, prices, animations) to match your branding.

#### Implementation
1. **Server-Side Configuration**: Use the LiveKit server REST API to manage gift information, categories, and multi-language support. See the Gift Configuration Guide.

2. **Client Fetch**: On the client, call `refreshUsableGifts` to retrieve configuration data.

3. **UI Display**: Use the retrieved `List<GiftCategory>` to render the gift panel.

#### Configuration Sequence Diagram

#### Related REST API Interfaces Overview
| **Interface Category** | **Interface** | **Request Example** |
| --- | --- | --- |
| **​Gift Management** | Add Gift Information | Example |
| Delete Gift Information | Example |  |
| Query Gift Information | Example |  |
| **Gift Category Management** | Add Gift Category Information | Example |
| Delete Specific Gift Category Information | Example |  |
| Get Specific Gift Category Information | Example |  |
| **Gift Relationship Management** | Add Relationship between a Specific Gift Category and Gift | Example |
| Delete Relationship between a Specific Gift Category and Gift | Example |  |
| Get Gift Relationships under a Specific Gift Category | Example |  |
| **Gift Multi-language Management** | Add Gift Multi-language Information | Example |
| Delete Specific Gift Multi-language Information | Example |  |
| Get Gift Multi-language Information | Example |  |
| Add Gift Category Multi-language Information | Example |  |
| Delete Specific Gift Category Multi-language Information | Example |  |
| Get Gift Category Multi-language Information | Example |  |

### Billing and Gift Deduction Process

AtomicXCore delegates the billing logic to your backend to ensure security and flexibility.

#### Workflow
1. **Backend Callback Configuration**: Configure your billing system's callback URL in the LiveKit backend. See Callback Configuration Documentation.

2. **Client Request**: The client calls `sendGift`.

3. **Backend Verification**: The LiveKit backend calls your callback URL; your billing system processes the deduction and returns the result.

4. **Result Synchronization**: If succeeds, **AtomicXCore** broadcasts the `onReceiveGift` event; if fails, the completion callback of `sendGift` receives an error.

#### Call Flow

#### Related REST API Interfaces Overview
| **Interface** | **Description** | **Request Example** |
| --- | --- | --- |
| **Callback Configuration - Callback before sending a gift** | Pre-gifting validation hook.  Allows your backend to intercept gift requests to perform necessary checks (e.g., sufficient balance, risk control) before the gift is processed. | Example |

### Full-Screen Animation (SVGA Integration)

When a user sends a luxury gift (e.g., "Rocket", "Carnival"), play a full-screen animation (such as SVGA) to enhance engagement.

#### Implementation

**AtomicXCore** does not include a built-in gift animation player. Integrate a third-party library based on your requirements. Below is a comparison of two options:
| **Comparison Item** | **Basic Solution (SVGAPlayer)** | **Gift AR (TCEffectPlayerKit)** |
| --- | --- | --- |
| Billing | Free (open source) | Paid (License Required). See [Billing Guide](https://trtc.io/document/69949?product=beautyar&menulabel=core%20sdk&platform=android#X-Series-Capabilities) |
| Integration Method | Manual integration via Gradle | Requires additional integration and authentication |
| Formats | SVGA only | SVGA, PAG, WebP, Lottie, MP4, and more |
| Performance | Good for files < 10MB | Optimized for large assets & complex layering |
| Recommended Scenario | Uniform SVGA format, controllable file size | Multiple formats or higher performance/device compatibility needs |

This section demonstrates the basic solution. For the **Gift AR**, see the [TCEffectPlayer Integration Guide](https://trtc.io/document/70537?product=beautyar&menulabel=core%20sdk&platform=ios).

#### Basic Solution Implementation: Using SVGAPlayer
1. **Integrate SVGAPlayer**: In your `Podfile`, add the dependency for `SVGAPlayer` and run `pod install` in the terminal.

   ``` ruby
   target 'YourApp' do
     # ... other pods
     pod 'SVGAPlayer'
   end
   ```
2. **Listen for Gift Events**: Subscribe to GiftStore's `giftEventPublisher`.

3. **Parse and Play**: When receiving an `.onReceiveGift` event, check if `gift.resourceURL` is valid and points to an SVGA file. If so, use `SVGAParser` to parse the URL and pass the parsed `SVGAVideoEntity` to the `SVGAPlayer` instance for playback.

#### Code Example
``` swift
import UIKit
import AtomicXCore 
import Combine
import SVGAPlayer // 1. Import

class LiveRoomViewController: UIViewController, SVGAPlayerDelegate {
    private var giftManager: GiftManager!
    private var cancellables = Set<AnyCancellable>()
    private let svgaPlayer = SVGAPlayer() // 2. Prepare instance
    private let svgaParser = SVGAParser()

    override func viewDidLoad() {
        super.viewDidLoad()
        setupSVGAPlayer()
    }

    private func setupSVGAPlayer() {
        svgaPlayer.delegate = self
        svgaPlayer.loops = 1 // Play once by default
        svgaPlayer.clearsAfterStop = true // Automatically clear after playback
        view.addSubview(svgaPlayer)
        svgaPlayer.frame = view.bounds // Full screen by default
        svgaPlayer.isHidden = true
    }

    func setupGiftSubscription(liveId: String) {
        self.giftManager = GiftManager(liveId: liveId)

        giftManager.giftEventPublisher
            .sink { [weak self] event in // 3. Listen for events
                guard case .onReceiveGift(_, let gift, _, _) = event else { return }

                if !gift.resourceURL.isEmpty, let url = URL(string: gift.resourceURL) { // 4. Parse and play
                    self?.playAnimation(from: url)
                }
            }
            .store(in: &cancellables)
    }

    private func playAnimation(from url: URL) {
        svgaParser.parse(with: url, completionBlock: { [weak self] videoItem in
            guard let self = self, let videoItem = videoItem else { return }
            DispatchQueue.main.async {
                self.svgaPlayer.videoItem = videoItem
                self.svgaPlayer.isHidden = false
                self.svgaPlayer.startAnimation()
            }
        }, failureBlock: { error in
            print("Failed to parse SVGA animation: \(error?.localizedDescription ?? "unknown error")")
            // Add retry or error reporting logic as needed
        })
    }

    func svgaPlayerDidFinishedAnimation(_ player: SVGAPlayer!) { /* ... Handle end of playback ... */ }
}
```

### Display Gift Notifications in Barrage

Enhance social interaction by displaying a system notification in the public barrage (chat) area whenever a gift is sent (e.g., "[User] sent [Gift] x [Count]").

#### Implementation
1. **Listen for Events**: Subscribe to `giftStore.giftEventPublisher`.

2. **Extract Information**: After receiving the` .onReceiveGift` event, extract the sender, gift, and count.

3. **Get Barrage Store**: Use `BarrageStore.create(liveID:)` to get the instance bound to the current room.

4. **Compose Message**: Create a `Barrage` struct, set `messageType = .text`, and set `textContent` to the composed string (e.g., "[sender.userName] sent [gift.name] x [count]").

5. **Insert Locally**: Call `barrageStore.appendLocalTip(message: giftTip)` to insert the message into the local list.

#### Code Example
``` swift
// In LiveRoomManager or a similar top-level manager
private func setupGiftToBarrageFlow() {
    giftStore.giftEventPublisher
        .receive(on: DispatchQueue.main)
        .sink { [weak self] event in // 1. Listen for events
            guard case .onReceiveGift(_, let gift, let count, let sender) = event else { return } // 2. Extract information

            guard let self = self else { return }
            // 3. Get BarrageStore (assume barrageStore is already initialized)

            // 4. Compose message
            let tipText = "\(sender.userName) sent \(gift.name) x \(count)"
            var giftTip = Barrage()
            giftTip.messageType = .text 
            giftTip.textContent = tipText
            // Optional: set a special sender

            // 5. Insert locally
            self.barrageStore.appendLocalTip(message: giftTip)
        }
        .store(in: &cancellables)
}
```

## API Documentation

For complete details on all public interfaces, properties, and methods of [GiftStore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/giftstore) and related classes, see the official API documentation for [AtomicXCore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore). Key stores referenced in this guide include:
| **Store/Component** | **Feature Description** | **API Documentation** |
| --- | --- | --- |
| GiftStore | Fetch gift list, send/receive gifts, listen for gift events (including sender and gift details). | [API Documentation](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/giftstore) |
| BarrageStore | Send text/custom barrage, maintain barrage list, listen to barrage status in real time. | [API Documentation](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/barragestore) |

## FAQs

### The gift list in GiftStore is empty. What should I do?

You must call `refreshUsableGifts(completion)` to fetch gift data from your backend. Ensure your backend is configured with gift data via the server REST API.

### How do I implement multi-language display for gifts (e.g., Chinese, English)?

Use the `GiftStore.setLanguage(language: String)` API before calling `refreshUsableGifts`, passing the target language code (e.g., "en" or "zh-CN"). The server will return gift names and descriptions in the specified language.

### I called sendGift, but the gift animation plays twice. Why?

The `onReceiveGift` event is broadcast to all room members, including the sender. If you update the UI both in the sendGift completion callback and in the `onReceiveGift` event, the animation will play twice.
- **Best Practice**: Only update the UI (e.g., play animations, show barrage) in the `onReceiveGift` event handler. Use the `sendGift` completion callback only for handling failures (such as "Send failed" or "Insufficient balance").

### Where is the gift deduction logic implemented?

Gift deduction is handled entirely by your billing system. AtomicXCore integrates with your billing system via a backend callback. When the client calls `sendGift`, your backend performs the deduction. After returning the result to the AtomicXCore backend, it determines whether to broadcast the gift event.

### Will gift notifications be blocked by mute or message frequency controls?

No. Gift notifications (`onReceiveGift` events) are not affected by mute or frequency controls and are always delivered reliably.

### What should I do if gift animation playback stutters?

Check your SVGA file size; the basic player recommends files no larger than 10MB. For large or complex animations, consider integrating the **Gift AR** provided by TUILiveKit for improved performance.

---

`GiftStore` is a module in `AtomicXCore` specialized in managing the gift function of live streaming rooms. With it, you can build a complete gift system for your live stream application to achieve various revenue and interactive scenarios.
| **Gift Panel** | **Barrage Gift** | **Full-Screen Gift** |
| --- | --- | --- |
|  |  |  |

## Core Features
- **Gift List Retrieval**: Obtain the required data for the gift panel from the server, including gift categories and gift details.

- **Send a Gift**: The audience can send a selected gift to the Anchor with quantity.

- **Gift Event Broadcast**: Receive gift giveaway events inside the room in real time for showing gift animation and bullet screen notification.

## Core Concepts

Before starting integration, let's learn about several core concepts related to `GiftStore` in the following table:
| **Core Concepts** | **Type** | **Core Responsibilities and Description** |
| --- | --- | --- |
| [Gift](https://tencent-rtc.github.io/TUIKit_Flutter/api_gift_gift_store/Gift-class.html) | `class` | Represents a specific gift data model. It contains the gift ID, name, icon address, animation resource URL and price (coins). |
| [GiftCategory](https://tencent-rtc.github.io/TUIKit_Flutter/api_gift_gift_store/GiftCategory-class.html) | `class` | Represents a gift category, such as "popular" and "luxury". It contains the category name as well as the **Gift** list under this category. |
| [GiftState](https://tencent-rtc.github.io/TUIKit_Flutter/api_gift_gift_store/GiftState-class.html) | `class` | Represents the current status of the gift module. Its core attribute `usableGifts` is a `ValueListenable<List<GiftCategory>>`, storing the complete gift list fetched from the server. |
| [GiftListener](https://tencent-rtc.github.io/TUIKit_Flutter/api_gift_gift_store/GiftListener-class.html) | `class` | Gift event listener, receive gift giveaway event through the `onReceiveGift` callback. When anyone (including itself) sends a gift, all people in the room will receive this event. |
| [GiftStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_gift_gift_store/GiftStore-class.html) | `class` | This is the core management class for interacting with the gift function. Through it, you can fetch the gift list, send a gift, and receive gift events via `addGiftListener`. |

## Implementation Steps

### Step 1: Integrating the Component

> **Note：**
> 

> To use the gifting system, activate either the **Free Trial,** or **Pro **edition. The number of configurable gifts depends on the selected package. For details, see the **Gift System** section in Feature and Billing Description and choose the package that fits your needs.
> 

- **Live streaming**: Refer to Quick Access for seamless integration with **AtomicXCore** and access completed.

- **Voice chat room**: Refer to Quick Access for seamless integration with **AtomicXCore** and access completed.

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

| **Parameter** | **Type** | **Description** |
| --- | --- | --- |
| `categoryID` | `String` | Unique ID of the gift category. |
| `name` | `String` | Display name of the gift category. |
| `desc` | `String` | Description of the gift category. |
| `extensionInfo` | `Map<String, String>` | Extended information field. |
| `giftList` | `List<Gift>` | Array of Gift objects under this category. |

- `Gift`**Parameter description**

| **Parameter** | **Type** | **Description** |
| --- | --- | --- |
| `giftID` | `String` | Unique ID of the gift. |
| `name` | `String` | Display name of the gift. |
| `desc` | `String` | Description of the gift. |
| `iconURL` | `String` | Icon URL of the gift. |
| `resourceURL` | `String` | Resource URL of the gift animation. |
| `level` | `int` | Gift level. |
| `coins` | `int` | Gift price. |
| `extensionInfo` | `Map<String, String>` | Extended information field. |

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
| **Parameter Name** | **Type** | **Description** |
| --- | --- | --- |
| `giftID` | `String` | Unique ID of the gift to send. |
| `count` | `int` | The number of sent. |

## Advanced Features

`GiftStore` feature heavily depends on your business backend service. This chapter will guide you on how to build a feature-rich, outstanding experience interactive system through server configuration and client implementation.

### **Gift Material Configuration**

You need to customize the available gift type, category, name, icon, price, and animated effects in the live streaming room to meet operational needs and brand feature.

#### Implementation
1. **Server-Side Configuration**: Use the LiveKit server REST API to manage gift information, categories, and multi-language support. See the Gift Configuration Guide.

2. **Client Fetch**: On the client, call `refreshUsableGifts` to retrieve configuration data.

3. **UI Display**: Use the retrieved `List<GiftCategory>` to render the gift panel.

#### Configuration Sequence Diagram

#### Related REST API Interfaces Overview
| **Interface Category** | **Interface** | **Request Example** |
| --- | --- | --- |
| **​Gift Management** | Add Gift Information | Example |
| Delete Gift Information | Example |  |
| Query Gift Information | Example |  |
| **Gift Category Management** | Add Gift Category Information | Example |
| Delete Specific Gift Category Information | Example |  |
| Get Specific Gift Category Information | Example |  |
| **Gift Relationship Management** | Add Relationship between a Specific Gift Category and Gift | Example |
| Delete Relationship between a Specific Gift Category and Gift | Example |  |
| Get Gift Relationships under a Specific Gift Category | Example |  |
| **Gift Multi-language Management** | Add Gift Multi-language Information | Example |
| Delete Specific Gift Multi-language Information | Example |  |
| Get Gift Multi-language Information | Example |  |
| Add Gift Category Multi-language Information | Example |  |
| Delete Specific Gift Category Multi-language Information | Example |  |
| Get Gift Category Multi-language Information | Example |  |

### Billing and Gift Sending Process

When the audience sends gifts, ensure sufficient account balance and complete the actual deduction before triggering the gift effect playback and broadcast.

#### Workflow
1. **Backend Callback Configuration**: Configure your billing system's callback URL in the LiveKit backend. See Callback Configuration Documentation.

2. **Client Request**: The client calls `sendGift`.

3. **Backend Verification**: The LiveKit backend calls your callback URL; your billing system processes the deduction and returns the result.

4. **Result Synchronization**: If succeeds, **AtomicXCore** broadcasts the `onReceiveGift` event; if fails, the completion callback of `sendGift` receives an error.

#### Call Flow

#### Related REST API Interfaces Overview
| **Interface** | **Description** | **Request Example** |
| --- | --- | --- |
| **Callback Configuration - Callback before sending a gift** | Pre-gifting validation hook.  Allows your backend to intercept gift requests to perform necessary checks (e.g., sufficient balance, risk control) before the gift is processed. | Example |

### Play Full-Screen Gift Animation

When a user (including itself) sends luxury gifts such as "rocket" or "carnival" in the live streaming room, play a cool gift animation (for example, SVGA animation) in full-screen playback to create a lively communication environment.

#### Implementation

`AtomicXCore` itself does not include a gift animation player. You need to select and integrate a third-party library based on business requirements. The following is a comparison of two solutions:
| **Comparison Item** | **Basic Solution (Svgaplayer_flutter)** | **Advanced Plan (TCEffectPlayerKit)** |
| --- | --- | --- |
| Billing | Free (open-source library) | Paid (License purchase required), please see [Payment Guide](https://trtc.io/document/69949?product=beautyar&menulabel=core%20sdk&platform=android#X-Series-Capabilities) |
| Integration Method | Manual integration of the [svgaplayer_flutter](https://pub.dev/packages/svgaplayer_flutter) library is required. | Additional integration of the [flutter_effect_player](https://github.com/Tencent-RTC/EffectPlayer_Flutter) library and authentication are required. |
| Animation Format Support | SVGA only | SVGA, PAG, WebP, Lottie, MP4, and other formats |
| Performance | Recommend SVGA files ≤ 10MB | Support larger animation files, better performance for complex effects, multi-animation concurrency, and low-end devices |
| Recommended scenarios | Gift animation format is unified as SVGA with controllable file size | Support multiple animation formats or higher performance/compatibility requirements |

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
| **Store/Component** | **Feature Description** | **API Reference** |
| --- | --- | --- |
| **GiftStore** | Gift interaction: Get gift list, send/receive gifts, listen to gift events (including sender, gift details). | [API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_gift_gift_store/GiftStore-class.html) |
| **BarrageStore** | Danmaku function: send text / custom barrage item, maintain bullet screen list, monitor in real time. | [API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_barrage_barrage_store/BarrageStore-class.html) |

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
