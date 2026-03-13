> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

This document guides you through building a basic live streaming app with host broadcasting and audience viewing capabilities using the core component [LiveCoreView](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.view/-live-core-view/index.html) from the **AtomicXCore SDK**.

### Core Features

**LiveCoreView** is a lightweight View component purpose-built for live streaming scenarios. It serves as the foundation of your live streaming implementation, encapsulating all complex streaming technologies—including stream publishing and playback, co-hosting, and audio/video rendering. Use LiveCoreView as the "canvas" for your live video, enabling you to focus on developing your custom UI and interactions.

The following view hierarchy diagram illustrates the position and role of **LiveCoreView** within the live streaming interface:

## Core Concepts
| **Core Concept** | **Core Responsibility** | **Key API / Property** |
| --- | --- | --- |
| LiveCoreView | Handles publishing, playing, and rendering audio/video streams. Provides adapter interfaces for integrating custom UI components (e.g., user info, PK progress bar). | - `viewType`:   - `CoreViewType.PUSH_VIEW` (host publishing view)   - `CoreViewType.PLAY_VIEW` (audience playback view) - `setLiveId()`: Binds the live room ID for this view. - `setVideoViewAdapter():` Adapter for custom video display UI slots. |
| LiveListStore | Manages the complete live room lifecycle (create, join, leave), synchronizes state, and listens for passive events (e.g., live ended, kicked out). | - `createLive()`: Start live stream as host. - `endLive()`: End live stream as host. - `joinLive()`: Audience joins live room. - `leaveLive()`: Leave live room. |
| LiveInfo | Defines room parameters before going live, such as room ID, seat layout mode, max co-hosts, etc. | - `liveID`: Unique room identifier. - `seatLayoutTemplateID`: Layout template ID (e.g., 600 for dynamic grid). |

## Preparation

### Step 1: Activate the Service

See Activate Service to obtain either the trial or paid version of the SDK.Then, go to [the Console](https://console.trtc.io/app) for application management, and get the following:
- `SDKAppID`: Application identifier (required). Tencent Cloud uses `SDKAppId` for billing and details.

- `SDKSecretKey`: Application secret key, used to initialize the configuration file with secret information.

   

### Step 2: Import AtomicXCore into Your Project

**Install the component**: Add the dependency `implementation 'com.tencent.atomicx:atomicxcore:latest`' to your `build.gradle` file, then perform a **Gradle****Sync**.
``` gradle
dependencies {
    implementation 'io.trtc.uikit:atomicx-core:latest.release'
    api "io.trtc.uikit:rtc_room_engine:3.4.0.1306"
    api "io.trtc.uikit:atomicx-core:3.4.0.1307"
    api "com.tencent.liteav:LiteAVSDK_Professional:12.8.0.19279"
    api "com.tencent.imsdk:imsdk-plus:8.7.7201"
    // Other dependencies...
}
```

### Step 3: Implement Login Logic

Call `LoginStore.shared.login` in your project to complete login. **This is required before you can use any functionality in AtomicXCore**.

> **Note：**
> 

> We recommend calling `LoginStore.shared.login` after your app's own user authentication is successful to ensure clear and consistent login logic.
> 

``` java
import android.os.Bundle
import androidx.appcompat.app.AppCompatActivity
import io.trtc.tuikit.atomicxcore.api.login.LoginStore
import io.trtc.tuikit.atomicxcore.api.CompletionHandler
import android.util.Log

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        LoginStore.shared.login(
            this,              // context
            1400000001,        // Replace with your SDKAppID
            "test_001",        // Replace with your UserID
            "xxxxxxxxxxx",     // Replace with your UserSig
            object : CompletionHandler {
                override fun onSuccess() {
                    // Handle login success
                    Log.d("Login", "login success")
                }

                override fun onFailure(code: Int, desc: String) {
                    // Handle login failure
                    Log.e("Login", "login failed, code: $code, error: $desc")
                }
            }
        )
    }
}
```

**Login API Parameter Description**
| Parameter | Type | Description |
| --- | --- | --- |
| SDKAppID | Int | Get this from [TRTC console > Application management](https://console.trtc.io/app). |
| UserID | String | The unique ID for the current user. Must contain only English letters, numbers, hyphens, and underscores. |
| userSig | String | A ticket for Tencent Cloud authentication. Please note: - **Development Environment**: You can use the local `GenerateTestUserSig.genTestSig` function to generate a UserSig or generate a temporary UserSig via the [UserSig Generation Tool](https://console.trtc.io/usersig). - **Production Environment**: To prevent key leakage, you must use a server-side method to generate UserSig. For details, see Generating UserSig on the Server. - For more information, see How to Calculate and Use UserSig. |

## Building a Basic Live Room

### Step 1: Implement Host Video Streaming

Follow these steps to quickly set up host video streaming:

> **Note：**
> 

> For a complete implementation, refer to [VideoLiveAnchorActivity.kt](https://github.com/Tencent-RTC/TUIKit_Android/blob/main/live/tuilivekit/src/main/java/com/trtc/uikit/livekit/livestream/VideoLiveAnchorActivity.kt) in the open-source TUILiveKit project.
> 

1. **Initialize the Broadcaster Streaming View**

   In your host `Activity`, create a LiveCoreView instance and set viewType to `PUSH_VIEW` (publishing view).

   ``` java
   import io.trtc.tuikit.atomicxcore.api.view.CoreViewType
   import io.trtc.tuikit.atomicxcore.api.view.LiveCoreView
   import android.os.Bundle
   import androidx.appcompat.app.AppCompatActivity
   import androidx.constraintlayout.widget.ConstraintLayout
   
   class YourAnchorActivity : AppCompatActivity() {
       private lateinit var coreView: LiveCoreView
   
       override fun onCreate(savedInstanceState: Bundle?) {
           super.onCreate(savedInstanceState)
   
           coreView = LiveCoreView(this, viewType = CoreViewType.PUSH_VIEW)
           coreView.setLiveID("test_live_001")
   
           setupUI()
       }
   
       private fun setupUI() {
           setContentView(R.layout.activity_anchor)
   
           val container = findViewById<ConstraintLayout>(R.id.container)
           container.addView(coreView)
   
           val params = ConstraintLayout.LayoutParams(
               ConstraintLayout.LayoutParams.MATCH_PARENT,
               ConstraintLayout.LayoutParams.MATCH_PARENT
           )
           params.topMargin = 36
           params.bottomMargin = 96
           coreView.layoutParams = params
       }
   }
   ```
2. **Open Camera and Microphone**

   Call the `openLocalCamera` and `openLocalMicrophone` methods of `DeviceStore` to enable the camera and microphone. **No additional action is required—LiveCoreView will automatically preview the current camera video stream**.

   ``` java
   import androidx.appcompat.app.AppCompatActivity
   import android.os.Bundle
   import io.trtc.tuikit.atomicxcore.api.device.DeviceStore
   
   class YourAnchorActivity : AppCompatActivity() {
       // ... other code ...
   
       override fun onCreate(savedInstanceState: Bundle?) {
           super.onCreate(savedInstanceState)
           setupUI()
           openDevices()
       }
   
       private fun openDevices() {
           DeviceStore.shared().openLocalCamera(true, completion = null)
           DeviceStore.shared().openLocalMicrophone(completion = null)
       }
   }
   ```
3. **Start Live Streaming**

   Start the live stream by calling `createLive` on `LiveListStore`.

   ``` java
   import android.util.Log
   import androidx.appcompat.app.AppCompatActivity
   import io.trtc.tuikit.atomicxcore.api.live.LiveInfo
   import io.trtc.tuikit.atomicxcore.api.live.LiveInfoCompletionHandler
   import io.trtc.tuikit.atomicxcore.api.live.LiveListStore
   
   class YourAnchorActivity : AppCompatActivity() {
       // ... other code ...
   
       private fun startLive() {
           val liveInfo = LiveInfo().apply {
               liveID = "test_live_001"
               liveName = "test live"
               seatLayoutTemplateID = 600 // Default: dynamic grid layout
               keepOwnerOnSeat = true
           }
           LiveListStore.shared().createLive(liveInfo, object: LiveInfoCompletionHandler {
               override fun onFailure(code: Int, desc: String) {
                   Log.e("Live", "startLive error: $desc")
               }
   
               override fun onSuccess(liveInfo: LiveInfo) {
                   Log.d("Live", "startLive success")
               }
           })
       }
   }
   ```

   `LiveInfo`** Parameter Description:**

| **Parameter Name** | **Type** | **Required** | **Description** |
| --- | --- | --- | --- |
| `liveID` | `String` | Yes | Unique identifier for the live room. |
| `liveName` | `String` | No | Title of the live room. |
| `notice` | `String` | No | Announcement message for the live room. |
| `isMessageDisable` | `Boolean` | No | Disable chat (true = yes, false = no). |
| `isPublicVisible` | `Boolean` | No | Room is publicly visible (true = yes, false = no). |
| `isSeatEnabled` | `Boolean` | No | Enable seat (co-host) functionality (true = yes, false = no). |
| `keepOwnerOnSeat` | `Boolean` | No | Keep the owner on a seat. |
| `maxSeatCount` | `Int` | Yes | Maximum number of seats. |
| `seatMode` | [TakeSeatMode](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-take-seat-mode/index.html) | No | Seat mode (FREE: free to take seat, APPLY: apply to take seat). |
| `seatLayoutTemplateID` | `Int` | Yes | Seat layout template ID. |
| `coverURL` | `String` | No | Cover image URL for the live room. |
| `backgroundURL` | `String` | No | Background image URL for the live room. |
| `categoryList` | `List` | No | List of category tags for the live room. |
| `activityStatus` | `Int` | No | Live activity status. |
| `isGiftEnabled` | `Boolean` | No | Whether to enable gift functionality (true: yes, false: no). |

4. **End Live Streaming**

   When the live stream ends, call the `endLive` method of `LiveListStore`. The SDK will handle stopping the stream and destroying the room.

   ``` java
   import android.util.Log
   import androidx.appcompat.app.AppCompatActivity
   import com.tencent.cloud.tuikit.engine.extension.TUILiveListManager
   import io.trtc.tuikit.atomicxcore.api.device.DeviceStore
   import io.trtc.tuikit.atomicxcore.api.live.LiveListStore
   import io.trtc.tuikit.atomicxcore.api.live.StopLiveCompletionHandler
   
   class YourAnchorActivity : AppCompatActivity() {
       // ... other code ...
   
       private fun stopLive() {
           LiveListStore.shared().endLive(object : StopLiveCompletionHandler {
               override fun onSuccess(statisticsData: TUILiveListManager.LiveStatisticsData) {
                   Log.d("Live", "endLive success, duration: ${statisticsData.liveDuration}, totalViewers: ${statisticsData.totalViewers}")
               }
   
               override fun onFailure(code: Int, desc: String) {
                   Log.e("Live", "endLive error: $desc")
               }
           })
       }
   
       override fun onDestroy() {
           super.onDestroy()
           stopLive()
           DeviceStore.shared().closeLocalCamera()
           DeviceStore.shared().closeLocalMicrophone()
           Log.d("Live", "YourAnchorActivity onDestroy")
       }
   }
   ```

### Step 2: Implement Audience Join and Watch

Follow these steps to enable audience viewing:

> **Note：**
> 

> For a complete reference implementation of audience viewing logic, see [VideoLiveAudienceActivity.kt](https://github.com/Tencent-RTC/TUIKit_Android/blob/main/live/tuilivekit/src/main/java/com/trtc/uikit/livekit/livestream/VideoLiveAudienceActivity.kt) in the open-source TUILiveKit project.
> 

1. **Add Audience Playback View**

   In your audience `Activity`, create a `LiveCoreView` instance and set `viewType` to `PLAY_VIEW` (playback view).

   ``` java
   import io.trtc.tuikit.atomicxcore.api.view.CoreViewType
   import io.trtc.tuikit.atomicxcore.api.view.LiveCoreView
   import android.os.Bundle
   import androidx.appcompat.app.AppCompatActivity
   import androidx.constraintlayout.widget.ConstraintLayout
   
   // YourAudienceActivity represents your audience viewing Activity
   class YourAudienceActivity : AppCompatActivity() {
   
       // 1. Initialize the audience playback view
       private lateinit var coreView: LiveCoreView
   
       override fun onCreate(savedInstanceState: Bundle?) {
           super.onCreate(savedInstanceState)
   
           // 2. Initialize the view
           coreView = LiveCoreView(this, viewType = CoreViewType.PLAY_VIEW)
           coreView.setLiveId("test_live_001")
   
           // UI layout
           setupUI()
       }
   
       private fun setupUI() {
           setContentView(R.layout.activity_audience)
   
           // 3. Add the playback view to your layout
           val container = findViewById<ConstraintLayout>(R.id.container)
           container.addView(coreView)
   
           // Set layout parameters
           val params = ConstraintLayout.LayoutParams(
               ConstraintLayout.LayoutParams.MATCH_PARENT,
               ConstraintLayout.LayoutParams.MATCH_PARENT
           )
           params.topMargin = 36
           params.bottomMargin = 96
           coreView.layoutParams = params
       }
   }
   ```
2. **Join the Live Room**

   Call the `joinLive` method of `LiveListStore` to join the live stream. **No additional setup is required—LiveCoreView will automatically play the video stream.**

   ``` java
   import io.trtc.tuikit.atomicxcore.api.live.LiveInfo
   import io.trtc.tuikit.atomicxcore.api.live.LiveInfoCompletionHandler
   import io.trtc.tuikit.atomicxcore.api.live.LiveListStore
   import android.os.Bundle
   import androidx.appcompat.app.AppCompatActivity
   import android.util.Log
   
   // YourAudienceActivity represents your audience viewing Activity
   class YourAudienceActivity : AppCompatActivity() {
   
       // ... other code ...
   
       override fun onCreate(savedInstanceState: Bundle?) {
           super.onCreate(savedInstanceState)
           setupUI()
           // 1. Join the live room (liveID must match the host's)
           LiveListStore.shared().joinLive(liveID, object : LiveInfoCompletionHandler {
               override fun onFailure(code: Int, desc: String) {
                   Log.e("Live", "joinLive error: $desc")
               }
   
               override fun onSuccess(liveInfo: LiveInfo) {
                   Log.d("Live", "joinLive success")
               }
           })
       }
   }
   ```
3. **Exit the Live Room**

   When the audience leaves, call the `leaveLive` method of `LiveListStore`. The SDK will automatically stop playback and exit the room.

   ``` java
   import io.trtc.tuikit.atomicxcore.api.live.LiveListStore
   import io.trtc.tuikit.atomicxcore.api.CompletionHandler
   import androidx.appcompat.app.AppCompatActivity
   import android.util.Log
   
   // YourAudienceActivity represents your audience viewing Activity
   class YourAudienceActivity : AppCompatActivity() {
   
       // ... other code ...
   
       // Exit the live room
       private fun leaveLive() {
           LiveListStore.shared().leaveLive(object : CompletionHandler {
               override fun onSuccess() {
                   Log.d("Live", "leaveLive success")
               }
   
               override fun onFailure(code: Int, desc: String) {
                   Log.e("Live", "leaveLive error: $desc")
               }
           })
       }
   
       // Always call leaveLive when Activity is destroyed
       override fun onDestroy() {
           super.onDestroy()
           leaveLive()
           Log.d("Live", "YourAudienceActivity onDestroy")
       }
   }
   ```

### Step 3: Listen for Live Events

After joining a live room, you should handle passive events such as the host ending the stream or the audience being removed for violations. If you do not listen for these events, the audience UI may remain in an invalid state, impacting user experience.

Implement the `LiveListListener` interface and register it with `LiveListStore`:
``` java
import io.trtc.tuikit.atomicxcore.api.live.LiveEndedReason
import io.trtc.tuikit.atomicxcore.api.live.LiveKickedOutReason
import io.trtc.tuikit.atomicxcore.api.live.LiveListListener
import io.trtc.tuikit.atomicxcore.api.live.LiveListStore
import android.os.Bundle
import androidx.appcompat.app.AppCompatActivity
import android.util.Log

// YourAudienceActivity represents your audience viewing Activity
class YourAudienceActivity : AppCompatActivity() {
    
    // ... (coreView, liveId, setupUI, joinLive, leaveLive, etc.) ...

    // 2. Define a LiveListListener instance
    private val liveListListener = object : LiveListListener() {
        override fun onLiveEnded(liveID: String, reason: LiveEndedReason, message: String) {
            // Listen for live stream end
            Log.d("Live", "Live ended. liveID: $liveID, reason: $reason, message: $message")
            // Handle exit logic, e.g., finish()
            // finish()
        }

        override fun onKickedOutOfLive(liveID: String, reason: LiveKickedOutReason, message: String) {
            // Listen for being kicked out of the live room
            Log.d("Live", "Kicked out of live. liveID: $liveID, reason: $reason, message: $message")
            // Handle exit logic
            // finish()
        }
    }

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setupUI() 
        
        // 3. Register the listener
        LiveListStore.shared().addLiveListListener(liveListListener)

        // 4. Join the live room
        joinLive()
    }
    
    // ... joinLive() and leaveLive() methods ...

    override fun onDestroy() {
        super.onDestroy()
        // 5. Remove the listener to prevent memory leaks
        LiveListStore.shared().removeLiveListListener(liveListListener)
        leaveLive()
        Log.d("Live", "YourAudienceActivity onDestroy")
    }
}
```

### Run and Test

After integrating `LiveCoreView`, you will have a pure video rendering view with full live streaming capabilities, but without any interactive UI. To add interactive features, see Enriching the Live Streaming Scene.
|  | Dynamic Grid Layout | Floating Window Layout | Fixed Grid Layout | Fixed Window Layout |
| --- | --- | --- | --- | --- |
| **Template ID** | 600 | 601 | 800 | 801 |
| **Description** | Default layout; grid size adjusts dynamically based on number of co-hosts. | Co-hosts are displayed as floating windows. | Fixed number of co-hosts; each occupies a fixed grid. | Fixed number of co-hosts; guests are displayed as fixed windows. |
| **Example** |  |  |  |  |

## Advanced Features

### Synchronizing Custom State in Live Streaming Room

In Live Streaming Room, hosts may need to synchronize custom information with all participants, such as the current room topic or background music. The `metaData` feature of `LiveListStore` supports this use case.

#### Implementation

On the host side, set custom information using the `updateLiveMetaData` API. `AtomicXCore` synchronizes these changes in real time to all participants. On the audience side, subscribe to `LiveListState.currentLive` and listen for changes in `metaData`. When a relevant key is updated, parse its value and update your business logic.

#### Example Code
``` kotlin
import io.trtc.tuikit.atomicxcore.api.LiveListStore
import io.trtc.tuikit.atomicxcore.api.CompletionHandler
import com.google.gson.Gson
import io.trtc.tuikit.atomicxcore.api.MetaDataCompletionHandler
import io.trtc.tuikit.atomicxcore.api.LiveListStore

// 1. Define a background music model (using data class)
data class MusicModel(
    val musicId: String,
    val musicName: String
)

// 2. Host side: Add a method to push background music in your Host business logic
fun updateBackgroundMusic(music: MusicModel) {
    val gson = Gson()
    val jsonString = gson.toJson(music) ?: ""

    // The metaData to be updated
    val metaData = hashMapOf("music_info" to jsonString)

    // Update metaData
    LiveListStore.shared()
        .updateLiveMetaData(
            metaData,
            object : CompletionHandler {
                override fun onSuccess() {
                    print("Background music ${music.musicName} pushed successfully")
                }

                override fun onFailure(code: Int, desc: String) {
                    print("Failed to push background music: $desc")
                }
            }
        )
}

// 3. Audience side: Add a method to listen for background music changes in your Audience business logic
private fun subscribeToDataUpdates() {
    CoroutineScope(Dispatchers.Main).launch {
        LiveListStore.shared()
            .liveState
            .currentLive
            .map { it.metaData }
            .collect {
                val musicInfo = it["music_info"]
                // Refresh business state, e.g., play new background music
            }
    }
}
```

## Enriching the Live Streaming Scene

Once the basic live streaming functionality is in place, refer to the following guides to add interactive features to your live stream:
| **Feature** | **Description** | **Store** | **Implementation Guide** |
| --- | --- | --- | --- |
| **Enable Audience Audio/Video Co-hosting** | Audience can apply to join the host on stage for real-time video interaction. | [CoGuestStore](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-co-guest-store/index.html) | Implementation Guide |
| **Enable Host Cross-room PK** | Hosts from different rooms can connect for interaction or PK. | [CoHostStore](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-co-host-store/index.html) [BattleStore](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-battle-store/index.html) | Implementation Guide |
| **Add Bullet Chat Feature** | Audience can send and receive real-time text messages in the live room. | [BarrageStore](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.barrage/-barrage-store/index.html) | Implementation Guide |
| **Build a Gift Giving System** | Audience can send virtual gifts to the host, increasing engagement and fun. | [GiftStore](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.gift/-gift-store/index.html) | Implementation Guide |

## API Documentation
| **Store/Component** | **Description** | **API Reference** |
| --- | --- | --- |
| LiveCoreView | Core view component for displaying and interacting with live video streams. Handles video rendering and view widgets, supports host streaming, audience co-hosting, host connections, and more. | [API Documentation](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.view/-live-core-view/index.html) |
| LiveListStore | Manages the full lifecycle of live rooms: create/join/leave/destroy rooms, query room list, modify live info (name, announcement, etc.), and listen to live status events (e.g., kicked out, ended). | [API Documentation](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-live-list-store/index.html) |
| DeviceStore | Controls audio/video devices: microphone (on/off, volume), camera (on/off, switch, quality), screen sharing, and real-time device status monitoring. | [API Documentation](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.device/-device-store/index.html) |
| CoGuestStore | Manages audience co-hosting: apply/invite/accept/reject co-host requests, member permission control (microphone/camera), and status synchronization. | [API Documentation](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-co-guest-store/index.html) |
| CoHostStore | Handles host cross-room connections: supports multiple layout templates (dynamic grid, etc.), initiates/accepts/rejects connections, and manages co-host interactions. | [API Documentation](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-co-host-store/index.html) |
| BattleStore | Manages host PK battles: initiate PK (set duration/opponent), manage PK status (start/end), synchronize scores, and listen for battle results. | [API Documentation](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-battle-store/index.html) |
| GiftStore | Handles gift interactions: get gift list, send/receive gifts, and listen for gift events (including sender and gift details). | [API Documentation](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.gift/-gift-store/index.html) |
| BarrageStore | Supports live chat: send text/custom danmaku, maintain danmaku list, and monitor danmaku status in real time. | [API Documentation](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.barrage/-barrage-store/index.html) |
| LikeStore | Handles like interactions: send likes, listen for like events, and synchronize total like count. | [API Documentation](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-like-store/index.html) |
| LiveAudienceStore | Manages audience: get real-time audience list (ID/name/avatar), count audience, and listen for join/leave events. | [API Documentation](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-live-audience-store/index.html) |
| AudioEffectStore | Audio effects: voice change (child/male), reverb (KTV, etc.), ear return adjustment, and real-time effect switching. | [API Documentation](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.device/-audio-effect-store/index.html) |
| BaseBeautyStore | Basic beauty filters: adjust smoothing/whitening/rosiness (0-9), reset beauty status, and synchronize effect parameters. | [API Documentation](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.device/-base-beauty-store/index.html) |

## FAQs

### Why is the screen black with no video after the host calls createLive or the audience calls joinLive?
- **Check setLiveID**: Ensure you have set the correct liveID for the LiveCoreView instance before calling start or join methods.

- **Check device permissions**: Ensure the app has system permissions for camera and microphone usage.

- **Check the host side**: Has the host called `DeviceStore.shared().openLocalCamera(true)`to enable the camera?

- **Check the network**: Ensure the device has a stable network connection.

### After the host enables the camera, why is there a local video preview after starting the stream, but a black screen before starting?
- **Check the host side**: Make sure the host streaming view (LiveCoreView) has its `viewType` set to `PUSH_VIEW`.

- **Check the audience side**: Make sure the audience playback view (LiveCoreView) has its `viewType` set to `PLAY_VIEW`.

### What restrictions and rules apply to `updateLiveMetaData`?

To maintain system stability and efficiency, metaData usage follows these rules:
- **Permissions**: Only hosts and administrators can call `updateLiveMetaData`. Regular audience members cannot.

- **Quantity and Size Limits:**

  - Each room supports up to **10** keys.

  - Each key can be up to **50 bytes**; each value up to **2KB**.

  - The total size of all values in a room cannot exceed **16KB**.

- **Conflict Resolution**: The update mechanism is "last write wins". If multiple administrators modify the same key in quick succession, the last change takes effect. Avoid concurrent modifications to the same key in your business logic.

---

This document guides you through building a basic live streaming app with host broadcasting and audience viewing capabilities using the core component [LiveCoreView](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.view/-live-core-view/index.html) from the **AtomicXCore SDK**.

### Core Features

**LiveCoreView** is a lightweight `View` component purpose-built for live streaming scenarios. It serves as the foundation of your live streaming implementation, encapsulating all complex streaming technologies—including stream publishing and playback, co-hosting, and audio/video rendering. Use LiveCoreView as the "canvas" for your live video, enabling you to focus on developing your custom UI and interactions.

The following view hierarchy diagram illustrates the position and role of **LiveCoreView** within the live streaming interface:

## Core Concepts
| **Core Concept** | **Core Responsibility** | **Key API / Property** |
| --- | --- | --- |
| LiveCoreView | Handles publishing, playing, and rendering audio/video streams. Provides adapter interfaces for integrating custom UI components (e.g., user info, PK progress bar). | - `viewType`:   - `.pushView` (host publishing view)   - `.playView` (audience playback view) - `setLiveId()`: Binds the live room ID for this view. - `videoViewDelegate`: Adapter for custom video display UI slots. |
| LiveListStore | Manages the complete live room lifecycle (create, join, leave), synchronizes state, and listens for passive events (e.g., live ended, kicked out). | - `createLive()`: Start live stream as host. - `endLive()`: End live stream as host. - `joinLive()`: Audience joins live room. - `leaveLive()`: Leave live room. |
| LiveInfo | Defines room parameters before going live, such as room ID, seat layout mode, max co-hosts, etc. | - `liveID`: Unique room identifier. - `seatLayoutTemplateID`: Layout template ID (e.g., 600 for dynamic grid). |

## Preparation

### Step 1: Activate the Service

See Activate Service to obtain either the trial or paid version of the SDK.Then, go to [the Console](https://console.trtc.io/app) for application management, and get the following:
- `SDKAppID`: Application identifier (required). Tencent Cloud uses `SDKAppID` for billing and details.

- `SDKSecretKey`: Application secret key, used to initialize the configuration file with secret information.

   

### Step 2: Import AtomicXCore into Your Project
1. **Install the Component**: Add `pod 'AtomicXCore'` to your `Podfile`, then run `pod install`.

   ``` ruby
   target 'xxxx' do
     pod 'AtomicXCore'
   end
   ```
2. **Configure App Permissions**: Add camera and microphone usage descriptions to your app's `Info.plist` file.

   ``` xml
   <key>NSCameraUsageDescription</key>
   <string>TUILiveKit needs camera access to enable video recording with picture</string>
   <key>NSMicrophoneUsageDescription</key>
   <string>TUILiveKit needs microphone permission to enable sound in recorded videos</string>
   ```
   

### Step 3: Implement Login Logic

Call `LoginStore.shared.login` in your project to complete authentication. **This is required before using any functionality of AtomicXCore**.

> **Note：**
> 

> We recommend calling LoginStore.shared.login only after your app's own user authentication is successful, to ensure clear and consistent login logic.
> 

``` swift
import AtomicXCore

//  AppDelegate.swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    LoginStore.shared.login(sdkAppID: 1400000001,                  // Replace with your SDKAppID
                            userID: "test_001",                    // Replace with your UserID
                            userSig: "xxxxxxxxxxx") { result in    // Replace with your UserSig
      switch result {
        case .success(let info):
        debugPrint("login success")
        case .failure(let error):
        debugPrint("login failed code:\(error.code), message:\(error.message)")
      }
    }
    return true
}
```

**Login API Parameter Description**
| **Parameter** | **Type** | **Description** |
| --- | --- | --- |
| `SDKAppID` | `Int` | Get this from [TRTC console](https://console.trtc.io/app). |
| `UserID` | `String` | The unique ID for the current user. Must contain only English letters, numbers, hyphens, and underscores. |
| `userSig` | `String` | A ticket for Tencent Cloud authentication. Please note: - Development Environment: You can use the local `GenerateTestUserSig.genTestSig` function to generate a `UserSig` or generate a temporary UserSig via the [UserSig Generation Tool](https://console.trtc.io/usersig). - Production Environment: To prevent key leakage, you must use a server-side method to generate `UserSig`. For details, see Generating UserSig on the Server. |

## Building a Basic Live Room

### Step 1: Implement Broadcaster Video Streaming

Follow these steps to quickly set up broadcaster video streaming:

> **Note：**
> 

> For a complete broadcaster streaming implementation, refer to [TUILiveRoomAnchorViewController.swift](https://github.com/Tencent-RTC/TUIKit_iOS/blob/main/live/Sources/LiveStream/TUILiveRoomAnchorViewController.swift) in the TUILiveKit open source project.
> 

1. **Initialize the Broadcaster Streaming View**

   In your broadcaster view controller, create a `LiveCoreView` instance and set `viewType` to `.pushView`.

   ``` swift
   import AtomicXCore
   
   // YourAnchorViewController represents your broadcaster streaming view controller
   class YourAnchorViewController: UIViewController {
   
       private let liveId: String
       // 1. Add LiveCoreView as a property of your view controller
       private let coreView = LiveCoreView(viewType: .pushView, frame: UIScreen.main.bounds)
   
       // 2. Add a convenience initializer for instance initialization
       //    - liveId: The ID of the live room to start streaming
       public init(liveId: String) {
           self.liveId = liveId
           super.init(nibName: nil, bundle: nil)
           self.coreView.setLiveID(liveId)
       }
   
       required init?(coder: NSCoder) {
           fatalError("init(coder:) has not been implemented")
       }
   
       public override func viewDidLoad() {
           super.viewDidLoad()
           // 3. Add the broadcaster streaming view to your view
           view.addSubview(coreView)
       }
   }
   ```
2. **Open Camera and Microphone**

   Call `DeviceStore.shared.openLocalCamera` and `DeviceStore.shared.openLocalMicrophone` to open the camera and microphone. **No further action is required—LiveCoreView automatically previews the current camera video stream**.

   ``` swift
   import AtomicXCore
   
   class YourAnchorViewController: UIViewController {
       // ... other code ...
       public override func viewDidLoad() {
           super.viewDidLoad()
           // Enable devices
           openDevices()
       }
   
       private func openDevices() {
           // 1. Enable front camera
           DeviceStore.shared.openLocalCamera(isFront: true, completion: nil)
           // 2. Enable microphone
           DeviceStore.shared.openLocalMicrophone(completion: nil)
       }
   }
   ```
3. **Start Live Streaming**

   Call `LiveListStore.shared.createLive` to start streaming.

   ``` swift
   import AtomicXCore
   
   class YourAnchorViewController: UIViewController {
   
       // ... other code ...
   
       // Call the start streaming interface to begin live streaming
       private func startLive() {
           var liveInfo = LiveInfo()
           // 1. Set the live room ID
           liveInfo.liveID = self.liveId
           // 2. Set the live room name
           liveInfo.liveName = "test live"
           // 3. Configure layout template, default: 600 dynamic grid layout
           liveInfo.seatLayoutTemplateID = 600
           // 4. Keep the broadcaster always on the seat
           liveInfo.keepOwnerOnSeat = true
           // 5. Call LiveListStore.shared.createLive to start streaming
           LiveListStore.shared.createLive(liveInfo) { [weak self] result in
               guard let self = self else { return }
               switch result {
               case .success(let info):
                   debugPrint("startLive success")
               case .failure(let error):
                   debugPrint("startLive error:\(error.message)")
               }
           }
       }
   }
   ```

   `LiveInfo` Parameter Descriptions:

| **Parameter Name** | **Type** | **Attribute** | **Description** |
| --- | --- | --- | --- |
| `liveID` | `String` | Required | Unique identifier for the live room. |
| `liveName` | `String` | Optional | Title of the live room. |
| `notice` | `String` | Optional | Announcement for the live room. |
| `isMessageDisable` | `Bool` | Optional | Whether to mute chat (true: yes, false: no). |
| `isPublicVisible` | `Bool` | Optional | Whether the room is publicly visible (true: yes, false: no). |
| `isSeatEnabled` | `Bool` | Optional | Whether to enable seat functionality (true: yes, false: no). |
| `keepOwnerOnSeat` | `Bool` | Optional | Whether to keep the owner on the seat. |
| `maxSeatCount` | `Int` | Required | Maximum number of seats. |
| `seatMode` | `TakeSeatMode` | Optional | Seat mode (.free: free to take seat, .apply: apply to take seat). |
| `seatLayoutTemplateID` | `UInt` | Required | Seat layout template ID. |
| `coverURL` | `String` | Optional | Cover image URL for the live room. |
| `backgroundURL` | `String` | Optional | Background image URL for the live room. |
| `categoryList` | `NSNumber` | Optional | Category tag list for the live room. |
| `activityStatus` | `Int` | Optional | Live activity status. |
| `isGiftEnabled` | `Bool` | Optional | Whether to enable gift functionality (true: yes, false: no). |

4. **End Live Streaming**

   After the live stream ends, call `LiveListStore.shared.endLive `to stop streaming and destroy the room. The SDK handles cleanup automatically.

   ``` swift
   import AtomicXCore
   
   class YourAnchorViewController: UIViewController {
   
       // ... other code ...
   
       // End live streaming
       private func stopLive() {
           LiveListStore.shared.endLive { [weak self] result in
               guard let self = self else { return }
               switch result {
               case .success(let data):
                   debugPrint("endLive success")
               case .failure(let error):
                   debugPrint("endLive error: \(error.message)")
               }
           }
       }
   }
   ```

### Step 2: Implement Audience Join and Watch

Enable audience viewing with the following steps:

> **Note：**
> 

> For a complete audience playback implementation, refer to [TUILiveRoomAudienceViewController.swift](https://github.com/Tencent-RTC/TUIKit_iOS/blob/main/live/Sources/LiveStream/TUILiveRoomAudienceViewController.swift) in the TUILiveKit open source project.
> 

1. **Implement the Audience Playback Page**

   In your audience view controller, create a `LiveCoreView` instance and set `viewType` to `.playView`.

   ``` swift
   import AtomicXCore
   
   class YourAudienceViewController: UIViewController {
   
       // 1. Initialize the audience playback page
       private let coreView = LiveCoreView(viewType: .playView, frame: UIScreen.main.bounds)
       private let liveId: String
   
       public init(liveId: String) {
           self.liveId = liveId
           super.init(nibName: nil, bundle: nil)
           // 2. Bind the live ID
           self.coreView.setLiveID(liveId)
       }
   
       required init?(coder: NSCoder) {
           fatalError("init(coder:) has not been implemented")
       }
   
       public override func viewDidLoad() {
           super.viewDidLoad()
           // 3. Add the playback view to your view
           view.addSubview(coreView)
       }
   }
   ```
2. **Join the Live Room to Watch**

   Call `LiveListStore.shared.joinLive` to join the live stream. **No further action is required—LiveCoreView will automatically play the current room's video stream**.

   ``` swift
   import AtomicXCore
   
   class YourAudienceViewController: UIViewController {
       // ... other code ...
   
       public override func viewDidLoad() {
           super.viewDidLoad()
           view.addSubview(coreView)
           // 4. Join the live room
           joinLive()
       }
   
       private func joinLive() {
           // Call LiveListStore.shared.joinLive to enter the live room
           // - liveId: Same liveId as the broadcaster
           LiveListStore.shared.joinLive(liveID: liveId) { [weak self] result in
               guard let self = self else { return }
               switch result {
               case .success(let info):
                   debugPrint("joinLive success")
               case .failure(let error):
                   debugPrint("joinLive error \(error.message)")
                   // If joining fails, exit the page
                   // self.dismiss(animated: true)
               }
           }
       }
   }
   ```
3. **Leave the Live Room**

   When the audience leaves, call `LiveListStore.shared.leaveLive` to exit. The SDK will automatically stop playback and leave the room.

   ``` swift
   import AtomicXCore
   
   class YourAudienceViewController: UIViewController {
   
       // ... other code ...
   
       // Leave the live room
       private func leaveLive() {
           LiveListStore.shared.leaveLive { [weak self] result in
               guard let self = self else { return }
               switch result {
               case .success:
                   debugPrint("leaveLive success")
               case .failure(let error):
                   debugPrint("leaveLive error \(error.message)")
               }
           }
       }
   }
   ```

### Step 3: Listen for Live Events

After joining a live room, handle "passive" events such as the broadcaster ending the stream or the audience being removed. If you do not listen for these events, the audience UI may remain on a black screen, impacting user experience.

Subscribe to `liveListEventPublisher` from `LiveListStore` to listen for events:
``` swift
import AtomicXCore
import Combine // 1. Import the Combine framework

class YourAudienceViewController: UIViewController {

    // ... other code (coreView, liveId, init, deinit, joinLive, leaveLive, etc.) ...

    // 2. Define cancellableSet to manage subscription lifecycle
    private var cancellableSet: Set<AnyCancellable> = []

    public override func viewDidLoad() {
        super.viewDidLoad()
        view.addSubview(coreView)
        // 3. Listen for live events
        setupLiveEventListener()
        // 4. Join the live room
        joinLive()
    }

    // 5. Add a method to set up event listeners
    private func setupLiveEventListener() {
        LiveListStore.shared.liveListEventPublisher
            .receive(on: RunLoop.main) // Ensure UI updates are handled on the main thread
            .sink { [weak self] event in
                guard let self = self else { return }
                switch event {
                case .onLiveEnded(let liveID, let reason, let message):
                    // Live stream ended
                    debugPrint("Live ended. liveID: \(liveID), reason: \(reason.rawValue), message: \(message)")
                    // Handle logic to exit the live room, e.g., close the current page
                    // self.dismiss(animated: true)
                case .onKickedOutOfLive(let liveID, let reason, let message):
                    // Kicked out of live stream
                    debugPrint("Kicked out of live. liveID: \(liveID), reason: \(reason.rawValue), message: \(message)")
                    // Handle logic to exit the live room
                    // self.dismiss(animated: true)
                }
            }
            .store(in: &cancellableSet) // Manage subscription
    }

    // ... joinLive() and leaveLive() methods ...
}
```

### Run and Test

After integrating `LiveCoreView`, you will have a pure video rendering view with full live streaming capabilities, but without any interactive UI. To add interactive features, see Enriching the Live Streaming Scene.
|  | **Dynamic Grid Layout** | **Floating Window Layout** | **Fixed Grid Layout** | **Fixed Window Layout** |
| --- | --- | --- | --- | --- |
| Template ID | 600 | 601 | 800 | 801 |
| Description | Default layout; grid size adjusts dynamically based on number of co-hosts. | Co-hosts are displayed as floating windows. | Fixed number of co-hosts; each occupies a fixed grid. | Fixed number of co-hosts; guests are displayed as fixed windows. |
| Example |  |  |  |  |

## Advanced Features

### Synchronizing Custom Status in Live Streaming Room

In live streaming room, the host may need to synchronize custom information to all audience members, such as "current room topic" or "background music info". Use the `metaData` feature of LiveListStore to achieve this.

#### Implementation
1. On the host side, set custom information (recommended as JSON) to one or more keys using the `updateLiveMetaData` API. AtomicXCore will synchronize these changes in real time to all audience members.

2. On the audience side, subscribe to `LiveListState.currentLive` and listen for changes in `metaData`. When a relevant key is updated, parse its value and update your business state.

#### Code Example
``` swift
import AtomicXCore
import Combine

// 1. Define a background music model (recommended: Codable)
struct MusicModel: Codable {
    let musicId: String
    let musicName: String
}

// 2. Host side: Push background music info
func updateBackgroundMusic(music: MusicModel) {
    guard let jsonData = try? JSONEncoder().encode(music),
          let jsonString = String(data: jsonData, encoding: .utf8) else { return }

    let metaData = ["music_info": jsonString]

    LiveListStore.shared.updateLiveMetaData(metaData) { result in
        if case .success = result {
            print("Background music \(music.musicName) pushed successfully")
        } else if case .failure(let error) = result {
            print("Background music push failed: \(error.message)")
        }
    }
}

// 3. Audience side: Subscribe and update business logic
private func subscribeToDataUpdates() {
    LiveListStore.shared.state
        // Listen for metaData changes in the current room
        .subscribe(StatePublisherSelector(keyPath: \LiveListState.currentLive))
        .map { $0.metaData["music_info"] }
        .removeDuplicates()
        .receive(on: DispatchQueue.main)
        .sink { jsonString in
            guard let jsonString = jsonString,
                  let data = jsonString.data(using: .utf8),
                  let music = try? JSONDecoder().decode(MusicModel.self, from: data) else {
                return
            }
            // Update business state, play new music
            // ... (e.g.: playMusic(music))
        }
        .store(in: &cancellables)
}
```

## Enriching the Live Streaming Scene

Once the basic live streaming functionality is in place, refer to the following guides to add interactive features to your live stream:
| **Feature** | **Description** | **Store** | **Implementation Guide** |
| --- | --- | --- | --- |
| Enable Audience Audio/Video Co-hosting | Audience can apply to join the host and interact via real-time video. | [CoGuestStore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/cogueststore) | Implementation Guide |
| Enable Host Cross-room PK | Hosts from different rooms can connect for interaction or PK. | [CoHostStore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/cohoststore) | Implementation Guide |
| Add Bullet Chat Feature | Audience can send and receive real-time text messages in the live room. | [BarrageStore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/barragestore) | Implementation Guide |
| Build a Gift Giving System | Audience can send virtual gifts to the host, increasing engagement and fun. | [GiftStore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/giftstore) | Implementation Guide |

## API Documentation
| **Store/Component** | **Description** | **API Reference** |
| --- | --- | --- |
| LiveCoreView | Core view component for displaying and interacting with live video streams. Handles video rendering and view widgets, supports host streaming, audience co-hosting, host connections, and more. | [LiveCoreView](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/livecoreview/) |
| LiveListStore | Manages the full lifecycle of live rooms: create/join/leave/destroy rooms, query room list, modify live info (name, announcement, etc.), and listen to live status events (e.g., kicked out, ended). | [LiveListStore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/liveliststore) |
| DeviceStore | Controls audio/video devices: microphone (on/off, volume), camera (on/off, switch, quality), screen sharing, and real-time device status monitoring. | [DeviceStore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/devicestore) |
| CoGuestStore | Manages audience co-hosting: apply/invite/accept/reject co-host requests, member permission control (microphone/camera), and status synchronization. | [CoGuestStore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/cogueststore) |
| CoHostStore | Handles host cross-room connections: supports multiple layout templates (dynamic grid, etc.), initiates/accepts/rejects connections, and manages co-host interactions. | [CoHostStore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/cohoststore) |
| BattleStore | Manages host PK battles: initiate PK (set duration/opponent), manage PK status (start/end), synchronize scores, and listen for battle results. | [BattleStore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/battlestore) |
| GiftStore | Handles gift interactions: get gift list, send/receive gifts, and listen for gift events (including sender and gift details). | [GiftStore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/giftstore) |
| BarrageStore | Supports live chat: send text/custom danmaku, maintain danmaku list, and monitor danmaku status in real time. | [BarrageStore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/barragestore) |
| LikeStore | Handles like interactions: send likes, listen for like events, and synchronize total like count. | [LikeStore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/likestore) |
| LiveAudienceStore | Manages audience: get real-time audience list (ID/name/avatar), count audience, and listen for join/leave events. | [LiveAudienceStore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/liveaudiencestore) |
| AudioEffectStore | Audio effects: voice change (child/male), reverb (KTV, etc.), ear return adjustment, and real-time effect switching. | [AudioEffectStore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/audioeffectstore) |
| BaseBeautyStore | Basic beauty filters: adjust smoothing/whitening/rosiness (0-9), reset beauty status, and synchronize effect parameters. | [BaseBeautyStore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/basebeautystore) |

## FAQs

### Why is the screen black with no video after the host calls createLive or the audience calls joinLive?
- **Check **`setLiveID`: Ensure you have set the correct liveID for the LiveCoreView instance before calling start or join methods.

- **Check device permissions**: Ensure the app has system permissions for camera and microphone usage.

- **Check the host side**: Has the host called `DeviceStore.shared().openLocalCamera(true)`to enable the camera?

- **Check the network**: Ensure the device has a stable network connection.

### After the host enables the camera, why is there a local video preview after starting the stream, but a black screen before starting?
- **Check the host side**: Make sure the host streaming view (`LiveCoreView`) has its `viewType` set to `PUSH_VIEW`.

- **Check the audience side**: Make sure the audience playback view (`LiveCoreView`) has its `viewType` set to `PLAY_VIEW`.

### What restrictions and rules apply to `updateLiveMetaData`?

To maintain system stability and efficiency, metaData usage follows these rules:
- **Permissions**: Only hosts and administrators can call `updateLiveMetaData`. Regular audience members cannot.

- **Quantity and Size Limits:**

  - Each room supports up to **10** keys.

  - Each key can be up to **50 bytes**; each value up to **2KB**.

  - The total size of all values in a room cannot exceed **16KB**.

- **Conflict Resolution**: The update mechanism is "last write wins". If multiple administrators modify the same key in quick succession, the last change takes effect. Avoid concurrent modifications to the same key in your business logic.

### sync Fails to Copy Third-party Library Resources Due to Insufficient Permissions

For example, when integrating the SnapKit framework with Xcode, you may encounter the following build error:
``` plaintext
rsync(xxxx):1:1: SnapKit.framework/SnapKit_Privacy.bundle/: mkpathat: Operation not permitted
```

**Cause**

Xcode's user script sandboxing mechanism restricts the rsync script's write access to `SnapKit.framework` resource files during the build process, causing the `SnapKit_Privacy.bundle` in the framework to fail to copy properly.

Solution Steps
1. Disable user script sandboxing. Open your Xcode project, go to **Build Settings**, search for User Script Sandboxing (or `ENABLE_USER_SCRIPT_SANDBOXING`), and change its value from YES to NO.

2. Clean and rebuild the project. Run **Product → Clean** Build Folder to clear the project cache, then rebuild and run the project.

---

This documentation guides you through using the core component of the AtomicXCore SDK, [LiveCoreWidget](https://tencent-rtc.github.io/TUIKit_Flutter/api_view_live_live_core_widget/api_view_live_live_core_widget-library.html), to quickly build a basic live streaming app with host broadcasting and audience viewing functionality.

## Core Features

**LiveCoreWidget** is a lightweight widget purpose-built for live streaming scenarios and serves as the foundation of your live streaming interface. It abstracts complex live streaming technologies—including streaming, co-hosting, and audio/video rendering—so you can use LiveCoreWidget as the canvas for your live video. This allows you to focus on developing your custom UI and interactive features.

The following diagram illustrates where **LiveCoreWidget** fits within your live streaming interface and its role in the view hierarchy:

## Preparations

### Step 1: Activate the Service

See Activate Service to obtain either the trial or paid version of the SDK.Then, go to [the Console](https://console.trtc.io/app) for application management, and get the following:
- `SDKAppID`: Application identifier (required). Tencent Cloud uses `SDKAppID` for billing and details.

- `SDKSecretKey`: Application secret key, used to initialize the configuration file with secret information.

   

### Step 2: Import AtomicXCore into Your Project
1. **Component installation**: Please add the `atomic_x_core` dependency in your `pubspec.yaml` file and execute `flutter pub get`.

   ``` yaml
   dependencies:
     atomic_x_core: ^3.6.0
   ```
2. **Configure project permissions:** Both Android and iOS projects require configuration.

   

【Android】

Please add permission to use camera and microphone in the `android/app/src/main/AndroidManifest.xml` file.
``` xml
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
```

【iOS】

Please add permission to use camera and microphone in the `iOS` directory **Podfile** and `ios/Runner` directory `Info.plist` file.

**Podfile**
``` ruby
post_install do |installer|
  installer.pods_project.targets.each do |target|
    flutter_additional_ios_build_settings(target)
      target.build_configurations.each do |config|
          config.build_settings['GCC_PREPROCESSOR_DEFINITIONS'] ||= [
        '$(inherited)',
        'PERMISSION_MICROPHONE=1',
        'PERMISSION_CAMERA=1',
        ]
      end
  end
end
```

**Info.plist**
``` xml
<key>NSCameraUsageDescription</key>
<string>TUILiveKit needs to access your camera permission. Video recording with picture only after enabling.</string>
<key>NSMicrophoneUsageDescription</key>
<string>TUILiveKit needs to access your mic permission. Recorded video will have sound when enabled.</string>
```

### Step 3: Implement Login Logic

Call `LoginStore.shared.login` in your project to complete login. **This is the key premise for using all functions of AtomicXCore.**

> **Important:**
> 

> It is recommended to call LoginStore.shared.login after successful log-in to your App's user account to ensure clear and consistent business logic.
> 

``` java
import 'package:flutter/material.dart';
import 'package:atomic_x_core/atomicxcore.dart';

void main() async {
  WidgetsFlutterBinding.ensureInitialized();

  final result = await LoginStore.shared.login(
    sdkAppID: 1400000001,           // replace with your sdkAppID
    userID: "test_001",             // replace with your userID
    userSig: "xxxxxxxxxxx",         // replace with your userSig
  );

  if (result.isSuccess) {
    debugPrint("login success");
  } else {
    debugPrint("login failed code: ${result.errorCode}, message: ${result.errorMessage}");
  }

  runApp(const MyApp());
}
```

**Logon API parameter description:**
| **Parameter** | **Type** | **Note** |
| --- | --- | --- |
| `sdkAppID` | `int` | Get this from [TRTC console](https://console.trtc.io/app). |
| `userID` | `String` | The unique ID for the current user. Must contain only English letters, numbers, hyphens, and underscores.. To avoid multi-end login conflict, **do not use**`1`, `123`**or other simple IDs**. |
| `userSig` | `String` | A ticket for Tencent Cloud authentication. Please note: - Development Environment: You can use the local `GenerateTestUserSig.genTestSig` function to generate a `UserSig` or generate a temporary UserSig via the [UserSig Generation Tool](https://console.trtc.io/usersig). - Production Environment: To prevent key leakage, you must use a server-side method to generate `UserSig`. For details, see Generating UserSig on the Server. |

## Building a Basic Live Room

### Step 1: Implement Broadcaster Video Streaming

The anchor starts live streaming process is as follows. You just need to perform the following steps to quickly build a live stream.

> **Note:**
> 

> For the business code of live stream publishing, you can also refer to the [live_room_anchor_widget.dart](https://github.com/Tencent-RTC/TUIKit_Flutter/blob/main/live/livekit/lib/live_stream/features/live_room_anchor_widget.dart) file in the TUILiveKit open-source project to understand the complete implementation logic.
> 

1. **Initialize the Anchor live streaming view**

   On your Anchor page, create a `LiveCoreWidget` instance and control the live stream behavior through `LiveCoreController`.

   ``` java
   import 'package:flutter/material.dart';
   import 'package:atomic_x_core/atomicxcore.dart';
   
   /// YourAnchorPage represents your anchor starts live streaming page
   class YourAnchorPage extends StatefulWidget {
     final String liveId;
   
     const YourAnchorPage({super.key, required this.liveId});
   
     @override
     State<YourAnchorPage> createState() => _YourAnchorPageState();
   }
   
   class _YourAnchorPageState extends State<YourAnchorPage> {
     // 1. Create a LiveCoreController instance
     late final LiveCoreController _controller;
   
     @override
     void initState() {
       super.initState();
       // 2. Initialize the controller
       _controller = LiveCoreController.create();
       // 3. Set up live streaming ID
       _controller.setLiveID(widget.liveId);
     }
   
     @override
     Widget build(BuildContext context) {
       return Scaffold(
         body: Stack(
           children: [
             // 4. Load the broadcaster stream page to your view
             LiveCoreWidget(controller: _controller),
             // Your other UI components
           ],
         ),
       );
     }
   }
   ```
2. **Turn on the camera and microphone**

   By calling the **DeviceStore**`openLocalCamera` and `openLocalMicrophone` APIs to turn on the camera and microphone, **no need to do additional configuration as LiveCoreWidget will auto preview the current camera's video stream**. Sample code:

   ``` java
   import 'package:flutter/material.dart';
   import 'package:atomic_x_core/atomicxcore.dart';
   
   /// YourAnchorPage represents your anchor starts live streaming page
   class YourAnchorPage extends StatefulWidget {
     final String liveId;
   
     const YourAnchorPage({super.key, required this.liveId});
   
     @override
     State<YourAnchorPage> createState() => _YourAnchorPageState();
   }
   
   class _YourAnchorPageState extends State<YourAnchorPage> {
     late final LiveCoreController _controller;
   
     @override
     void initState() {
       super.initState();
       _controller = LiveCoreController.create();
       _controller.setLiveID(widget.liveId);
       // Turn on the device
       _openDevices();
     }
   
     void _openDevices() {
       // 1. Open front camera
       DeviceStore.shared.openLocalCamera(true);
       // 2. Turn on the microphone
       DeviceStore.shared.openLocalMicrophone();
     }
   
     @override
     Widget build(BuildContext context) {
       return Scaffold(
         body: Stack(
           children: [
             LiveCoreWidget(controller: _controller),
           ],
         ),
       );
     }
   }
   ```
3. **Start live streaming**

   By calling the **LiveListStore**`createLive` API to start video live streaming, sample code:

   ``` java
   import 'package:flutter/material.dart';
   import 'package:atomic_x_core/atomicxcore.dart';
   
   /// YourAnchorPage represents your anchor starts live streaming page
   class YourAnchorPage extends StatefulWidget {
     final String liveId;
   
     const YourAnchorPage({super.key, required this.liveId});
   
     @override
     State<YourAnchorPage> createState() => _YourAnchorPageState();
   }
   
   class _YourAnchorPageState extends State<YourAnchorPage> {
     late final LiveCoreController _controller;
   
     @override
     void initState() {
       super.initState();
       _controller = LiveCoreController.create();
       _controller.setLiveID(widget.liveId);
       _openDevices();
     }
   
     void _openDevices() {
       DeviceStore.shared.openLocalCamera(true);
       DeviceStore.shared.openLocalMicrophone();
     }
   
     // Call the go live API to start live streaming
     Future<void> _startLive() async {
       // 1. Prepare the LiveInfo object
       final liveInfo = LiveInfo(
         // Set up live streaming room id
         liveID: widget.liveId,
         // Set up live streaming room name
         liveName: "test live stream",
         // Configure the layout template, default: 600 dynamic grid layout
         seatLayoutTemplateID: 600,
         // Configure the anchor to always stay on the seat
         keepOwnerOnSeat: true,
       );
   
       // 2. Call LiveListStore.shared.createLive to start live streaming
       final result = await LiveListStore.shared.createLive(liveInfo);
   
       if (result.isSuccess) {
         debugPrint("startLive success");
       } else {
         debugPrint("startLive error: ${result.errorMessage}");
       }
     }
   
     @override
     Widget build(BuildContext context) {
       return Scaffold(
         body: Stack(
           children: [
             LiveCoreWidget(controller: _controller),
             // Go live button
             Positioned(
               bottom: 50,
               left: 0,
               right: 0,
               child: Center(
                 child: ElevatedButton(
                   onPressed: _startLive,
                   child: const Text('Start live broadcast'),
                 ),
               ),
             ),
           ],
         ),
       );
     }
   }
   ```

   **LiveInfo parameter description:**

| **Parameter Name** | **Type** | **Attribute** | **Description** |
| --- | --- | --- | --- |
| `liveID` | `String` | Required | Unique identifier for the live streaming room. |
| `liveName` | `String` | Optional. | Title of the live streaming room. |
| `notice` | `String` | Optional. | Announcement information of the live streaming room. |
| `isMessageDisable` | `bool` | Optional. | Whether to mute (`true`: yes, `false`: no). |
| `isPublicVisible` | `bool` | Optional. | Whether publicly visible (`true`: yes, `false`: no). |
| `isSeatEnabled` | `bool` | Optional. | Whether to enable the seat feature (`true`: yes, `false`: no). |
| `keepOwnerOnSeat` | `bool` | Optional. | Whether to keep the room owner on the seat. |
| `maxSeatCount` | `int` | Optional. | Maximum number of microphones. |
| `seatMode` | `TakeSeatMode` | Optional. | Microphone mode (`TakeSeatMode.free`: Free to Join the Podium, `TakeSeatMode.apply`: Request to speak). |
| `seatLayoutTemplateID` | `int` | Required | layout template ID. |
| `coverURL` | `String` | Optional. | Thumbnail URL of the live streaming room. |
| `backgroundURL` | `String` | Optional. | Background image URL of the live streaming room. |
| `categoryList` | `List<int>` | Optional. | Tag list of categories in the live streaming room. |
| `activityStatus` | `int` | Optional. | Live stream status. |
| `isGiftEnabled` | `bool` | Optional. | Whether to enable the gift function (`true`: yes, `false`: no). |

4. **End live streaming**

   After the live streaming ends, the Anchor can call the **LiveListStore**'s `endLive` API to end the live stream. The SDK will handle the logic of stopping streaming and room termination.

   ``` java
   import 'package:flutter/material.dart';
   import 'package:atomic_x_core/atomicxcore.dart';
   
   /// YourAnchorPage represents your anchor starts live streaming page
   class YourAnchorPage extends StatefulWidget {
     final String liveId;
   
     const YourAnchorPage({super.key, required this.liveId});
   
     @override
     State<YourAnchorPage> createState() => _YourAnchorPageState();
   }
   
   class _YourAnchorPageState extends State<YourAnchorPage> {
     // ... Other code ...
   
     End live streaming
     Future<void> _stopLive() async {
       final result = await LiveListStore.shared.endLive();
   
       if (result.isSuccess) {
         debugPrint("endLive success");
       } else {
         debugPrint("endLive error: ${result.errorMessage}");
       }
     }
   
     // ... Other code ...
   }
   ```

### Step 2: Implement Audience Join and Watch

The audience viewing process is as follows. In just a few simple steps, you can achieve audience watching live.

> **Note:**
> 

> For the business code of audience enter room to pull stream, you can also refer to the [audience_widget.dart](https://github.com/Tencent-RTC/TUIKit_Flutter/blob/main/live/livekit/lib/live_stream/features/audience/audience_widget.dart) file in the TUILiveKit open-source project to understand the complete implementation logic.
> 

1. **Implement the audience pull stream page**

   On your audience page, create a `LiveCoreWidget` instance and control the live stream behavior through `LiveCoreController`.

   ``` java
   import 'package:flutter/material.dart';
   import 'package:atomic_x_core/atomicxcore.dart';
   
   /// YourAudiencePage represents your audience viewing webpage
   class YourAudiencePage extends StatefulWidget {
     final String liveId;
   
     const YourAudiencePage({super.key, required this.liveId});
   
     @override
     State<YourAudiencePage> createState() => _YourAudiencePageState();
   }
   
   class _YourAudiencePageState extends State<YourAudiencePage> {
     // 1. Create a LiveCoreController instance
     late final LiveCoreController _controller;
   
     @override
     void initState() {
       super.initState();
       // 2. Initialize the controller
       _controller = LiveCoreController.create();
       // 3. Bind live streaming id
       _controller.setLiveID(widget.liveId);
     }
   
     @override
     Widget build(BuildContext context) {
       return Scaffold(
         body: Stack(
           children: [
             // 4. Load the audience pull stream page to your view
             LiveCoreWidget(controller: _controller),
           ],
         ),
       );
     }
   }
   ```
2. **Enter live room to watch**

   By calling the **LiveListStore**`joinLive` API to join the live stream, **no need to do additional configuration, LiveCoreWidget will autoplay the current room video stream**, sample code:

   ``` java
   import 'package:flutter/material.dart';
   import 'package:atomic_x_core/atomicxcore.dart';
   
   /// YourAudiencePage represents your audience viewing webpage
   class YourAudiencePage extends StatefulWidget {
     final String liveId;
   
     const YourAudiencePage({super.key, required this.liveId});
   
     @override
     State<YourAudiencePage> createState() => _YourAudiencePageState();
   }
   
   class _YourAudiencePageState extends State<YourAudiencePage> {
     late final LiveCoreController _controller;
   
     @override
     void initState() {
       super.initState();
       _controller = LiveCoreController.create();
       _controller.setLiveID(widget.liveId);
       // Enter live room
       _joinLive();
     }
   
     Future<void> _joinLive() async {
       // Call LiveListStore.shared.joinLive to enter live room
       // - liveId: same liveId as anchor starts live streaming
       final result = await LiveListStore.shared.joinLive(widget.liveId);
   
       if (result.isSuccess) {
         debugPrint("joinLive success");
       } else {
         debugPrint("joinLive error: ${result.errorMessage}");
         // Failed to enter the room, must exit the page
         // if (mounted) Navigator.of(context).pop();
       }
     }
   
     @override
     Widget build(BuildContext context) {
       return Scaffold(
         body: Stack(
           children: [
             LiveCoreWidget(controller: _controller),
           ],
         ),
       );
     }
   }
   ```
3. **Log out of live stream**

   When the audience exits the live streaming room, they need to call the **LiveListStore**'s `leaveLive` API to exit the live stream. The SDK will automatically stop pulling streams and leave the room.

   ``` java
   import 'package:flutter/material.dart';
   import 'package:atomic_x_core/atomicxcore.dart';
   
   /// YourAudiencePage represents your audience viewing webpage
   class YourAudiencePage extends StatefulWidget {
     final String liveId;
   
     const YourAudiencePage({super.key, required this.liveId});
   
     @override
     State<YourAudiencePage> createState() => _YourAudiencePageState();
   }
   
   class _YourAudiencePageState extends State<YourAudiencePage> {
     // ... Other code ...
   
     End live stream
     Future<void> _leaveLive() async {
       final result = await LiveListStore.shared.leaveLive();
   
       if (result.isSuccess) {
         debugPrint("leaveLive success");
       } else {
         debugPrint("leaveLive error: ${result.errorMessage}");
       }
     }
   
     // ... Other code ...
   }
   ```

### Step 3: Listen for Live Events

After the audience joins the live room, you also need to process some passive events inside the room. For example, the Anchor proactively ends the live stream, or the audience is kicked out of the room due to rule violation. If these events are not listened to, the client UI may stay on a black screen webpage, affecting user experience.

You can achieve event monitoring through `LiveListListener`.
``` java
import 'package:flutter/material.dart';
import 'package:atomic_x_core/atomicxcore.dart';

/// YourAudiencePage represents your audience viewing webpage
class YourAudiencePage extends StatefulWidget {
  final String liveId;

  const YourAudiencePage({super.key, required this.liveId});

  @override
  State<YourAudiencePage> createState() => _YourAudiencePageState();
}

class _YourAudiencePageState extends State<YourAudiencePage> {
  late final LiveCoreController _controller;
  // 1. Define LiveListListener to manage event monitoring
  late final LiveListListener _liveListListener;

  @override
  void initState() {
    super.initState();
    _controller = LiveCoreController.create();
    _controller.setLiveID(widget.liveId);
    // 2. Listen to Live Event
    _setupLiveEventListener();
    // 3. Enter live room
    _joinLive();
  }

  // 4. Add a method to set up event listening
  void _setupLiveEventListener() {
    _liveListListener = LiveListListener(
      onLiveEnded: (liveID, reason, message) {
        // Listen to live streaming end
        debugPrint("Live ended. liveID: $liveID, reason: ${reason.value}, message: $message");
        // Handle the logic for exiting a live streaming room herein, such as closing current page
        // if (mounted) Navigator.of(context).pop();
      },
      onKickedOutOfLive: (liveID, reason, message) {
        // Listen to being kicked out of live stream
        debugPrint("Kicked out of live. liveID: $liveID, reason: ${reason.value}, message: $message");
        // Handle the logic for exiting a live streaming room herein
        // if (mounted) Navigator.of(context).pop();
      },
    );
    LiveListStore.shared.addLiveListListener(_liveListListener);
  }

  Future<void> _joinLive() async {
    final result = await LiveListStore.shared.joinLive(widget.liveId);
    if (result.isSuccess) {
      debugPrint("joinLive success");
    } else {
      debugPrint("joinLive error: ${result.errorMessage}");
    }
  }

  Future<void> _leaveLive() async {
    final result = await LiveListStore.shared.leaveLive();
    if (result.isSuccess) {
      debugPrint("leaveLive success");
    } else {
      debugPrint("leaveLive error: ${result.errorMessage}");
    }
  }

  @override
  void dispose() {
    // 5. Remove event listening
    LiveListStore.shared.removeLiveListListener(_liveListListener);
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Stack(
        children: [
          LiveCoreWidget(controller: _controller),
        ],
      ),
    );
  }
}
```

### Run and Test

After integrating `LiveCoreWidget`, you will obtain a pure video rendering view with complete live streaming business capability but no interactive UI. You can refer to the next chapter Enrich Live-Streaming Scenarios to refine live broadcasting scenarios.
|  | **Dynamic Grid Layout** | **Floating Window Layout** | **Fixed Grid Layout** |
| --- | --- | --- | --- |
| Template ID | 600 | 601 | 800 |
| Description | Default layout; grid size adjusts dynamically based on number of co-hosts. | Co-hosts are displayed as floating windows. | Fixed number of co-hosts; each occupies a fixed grid. |
| Example |  |  |  |

## Enrich Live Streaming Scenarios

Once the basic live streaming functionality is in place, refer to the following guides to add interactive features to your live stream:
| **Feature** | **Description** | **Store** | **Implementation Guide** |
| --- | --- | --- | --- |
| **Enable Audience Audio/Video Co-hosting** | Audience can apply to join the host and interact via real-time video. | [CoGuestStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_co_guest_store/CoGuestStore-class.html) | Implementation Guide |
| **Enable Host Cross-room PK** | Hosts from different rooms can connect for interaction or PK. | [CoHostStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_co_host_store/CoHostStore-class.html) / [BattleStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_battle_store/BattleStore-class.html) | Implementation Guide |
| **Add Bullet Chat Feature** | Audience can send and receive real-time text messages in the live room. | [BarrageStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_barrage_barrage_store/BarrageStore-class.html) | Implementation Guide |
| **Build a Gift Giving System** | Audience can send virtual gifts to the host, increasing engagement and fun. | [GiftStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_gift_gift_store/GiftStore-class.html) | Implementation Guide |

## API documentation
| **Store/Component** | **Feature Description** | **API Reference** |
| --- | --- | --- |
| **LiveCoreWidget** | The core view component for live video stream display and interaction: responsible for video stream rendering and view widget processing, supporting scenarios like live streaming, audience co-broadcasting, and anchor connection. | [API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_view_live_live_core_widget/LiveCoreWidget-class.html) |
| **LiveCoreController** | The controller of LiveCoreWidget: used to set up the live streaming ID, control the preview, and perform other operations. | [API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_view_live_live_core_widget/LiveCoreController-class.html) |
| **LiveListStore** | Full lifecycle management of live streaming room: create/join/leave/terminate room, query room list, modify live information (name, notice), listen to live status (for example, being kicked out, ended). | [API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_live_list_store/LiveListStore-class.html) |
| **DeviceStore** | Audio/Video device control: microphone (on/off, volume), camera (on/off, switchover, video quality), screen sharing, monitor device status in real time. | [API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_device_device_store/DeviceStore-class.html) |
| **CoGuestStore** | Audience co-broadcasting management: join microphone application/invite/grant/deny, attendee permission control (microphone/camera), state synchronization. | [API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_co_guest_store/CoGuestStore-class.html) |
| **CoHostStore** | Anchor cross-room connection: supports multiple layout templates (dynamic grid, etc.), initiate/accept/reject connection, and manage interactive co-broadcasting with Anchors. | [API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_co_host_store/CoHostStore-class.html) |
| **BattleStore** | Anchor PK battle: trigger PK (duration configuration/competitor), manage PK status (start/End), synchronize score, listen to battle results. | [API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_battle_store/BattleStore-class.html) |
| **GiftStore** | Gift interaction: get gift list, send/receive gifts, listen to gift events (including sender, gift details). | [API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_gift_gift_store/GiftStore-class.html) |
| **BarrageStore** | Danmaku function: send text/custom barrage item, maintain bullet screen list, monitor bullet screen status in real time. | [API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_barrage_barrage_store/BarrageStore-class.html) |
| **LikeStore** | Like interaction: send likes, listen to like events, sync total likes. | [API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_like_store/LikeStore-class.html) |
| **LiveAudienceStore** | Audience management: get real-time audience list (ID/name/avatar), check audience size, listen to Enter/Exit Event. | [API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_live_audience_store/LiveAudienceStore-class.html) |
| **AudioEffectStore** | Audio effects: voice-changing (child voice/male voice), reverberation (KTV), ear monitoring adjustment, switch effects in real time. | [API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_device_audio_effect_store/AudioEffectStore-class.html) |
| **BaseBeautyStore** | Basic beauty filter: adjust skin smoothing/whitening/rosy (0-100 levels), reset beauty effect status, synchronize effect parameters. | [API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_device_base_beauty_store/BaseBeautyStore-class.html) |

## FAQs

### Why is the screen black with no video after the host calls createLive or the audience calls joinLive?
- **Check setLiveID**: Please ensure the correct `liveID` has been set for the `LiveCoreController` instance before calling the live streaming or viewing API.

- **Check device permission**: Please ensure the app has obtained system usage permission for the camera and microphone.

- **Check anchor side**: Whether the Anchor side normally called `DeviceStore.shared.openLocalCamera(true)` to open the camera.

- **Check the network**: Please check whether the device network connection is normal.

### How to Request Permission in a Flutter Project?

You can use the `permission_handler` plug-in to request camera and mic permission:
``` java
import 'package:permission_handler/permission_handler.dart';

Future<void> requestPermissions() async {
  await [
    Permission.camera,
    Permission.microphone,
  ].request();
}
```

### How to Handle Page Lifecycle in Flutter?

It is recommended to clean up resources in the `dispose` method, such as removing event listeners:
``` java
@override
void dispose() {
  LiveListStore.shared.removeLiveListListener(_liveListListener);
  super.dispose();
}
```

---

## Overview

This guide introduces the **Live Stream List page** in the TUILiveKit Demo. Use this documentation to quickly integrate our ready-made Live Stream List page into your project, or customize its appearance, layout, and features to fit your needs.

## Quick Experience

Start a live stream instantly using the [Online Hosting Site](https://web.sdk.qcloud.com/trtc/livekit/pusher/index.html), and view your Live Stream List from your account on the [Online Viewing Site](https://web.sdk.qcloud.com/trtc/livekit/player/index.html).

## Quick Integration

### Step 1: Environment Setup and Activate the Service

Before you begin, follow the Preparation guide to integrate required components and enable login functionality.

### Step 2: Install Dependencies

Install the necessary dependencies using one of the following package managers:

【npm】
``` bash
npm install tuikit-atomicx-vue3 @tencentcloud/uikit-base-component-vue3 --save
```

【pnpm】
``` bash
pnpm add tuikit-atomicx-vue3 @tencentcloud/uikit-base-component-vue3
```

【yarn】
``` bash
yarn add tuikit-atomicx-vue3 @tencentcloud/uikit-base-component-vue3
```

### Step 3: Integrate Live Stream List Page

Create a **live-list.vue** file in your project and add the following code to embed the **Live Stream List page**.

> **Note：**
> 

> You can copy the code below directly into your project, or check the [Live Stream List](https://github.com/Tencent-RTC/TUILiveKit/blob/main/Web/web-vite-vue3/src/TUILiveKit/LiveListView.vue) for the full source code.
> 

``` typescript
<template>
  <UIKitProvider theme="dark">
    <div class="container">
      <header class="header">
        <h1 class="title">Online Live</h1>
      </header>
      <main class="main">
        <LiveList /> 
      </main>
    </div>
  </UIKitProvider>
</template>

<script setup lang="ts">
import { onMounted } from 'vue';
import { LiveList, useLoginState } from 'tuikit-atomicx-vue3';
import { UIKitProvider } from '@tencentcloud/uikit-base-component-vue3';

const { login } = useLoginState();

async function initLogin() {
  try {
    await login({
      sdkAppId: 0,        // SDKAppID, see Step 1 for details
      userId: '',         // UserID, see Step 1 for details
      userSig: '',        // userSig, see Step 1 for details
    });
  } catch (error) {
    console.error('Login failed:', error);
  }
}

onMounted(async () => {
  await initLogin();
});
</script>

<style scoped>:global(*),:global(::after),:global(::before){box-sizing:border-box;margin:0}.container{display:flex;flex-direction:column;height:100vh;width:100vw;background:var(--bg-color-default)}.header{display:flex;align-items:center;flex-shrink:0}.title{margin:0;font-size:16px;font-weight:600;color:var(--text-color-primary);letter-spacing:-.5px}.main{flex:1;padding:24px;overflow-y:auto;min-height:0}</style>
```

> **注意：**
> 

> To enable navigation from the Live Stream List to a specific live room, see the Specify Live Room section below.
> 

## Start the Project

### Launch Live Stream List Page

After running the following command, open your browser and visit your local address to access the Live Stream List page.

> **Tip：**
> 

> Once the command completes, enter your local address in the browser (for example, `http://localhost:5173/live-list`; your port number may differ based on your project setup) to view the Live Stream List page.
> 

``` bash
npm run dev
```

### Specify Live Room

To enable navigation from the Live Stream List (or homepage) to the viewing page, set up Vue Router. Create a `router` folder inside your project's `src` directory and add an `index.ts` file. Then, import and register the router in your main file (such as **main.ts** or **index.ts**). For reference, see the [GitHub code example](https://github.com/Tencent-RTC/TUILiveKit/blob/main/Web/web-vite-vue3/src/main.ts).

#### Step 1: Configure Page Routing

Set up Vue Router to map `live-list.vue` to the Live Stream List page.

> **Note：**
> 
> - If your project already has a `src/router/index.ts` file, merge the following code into your existing file.
> - If you haven't set up routing, create a new `src/router/index.ts` file and add the configuration below.

``` typescript
import { createRouter, createWebHistory } from 'vue-router';

const routes = [
  {
    // Live Stream List page; update the path below to match your project structure
    path: '/live-list',
    component: () => import('../live-list.vue'),
  },  
  // To enable navigation from the Live Stream List cover to the corresponding live room, configure the viewing page route as shown below
  {
    // Route to the viewing page; update the path below to match your project structure
    path: '/live-player',
    component: () => import('../live-player.vue'),
  },
];

const router = createRouter({
  history: createWebHistory(),
  routes,
});
export default router;
```

#### Step 2: Configure src/main.ts

Add the router and localization setup to your project's entry file, src/main.ts:
``` java
// src/main.ts
import { createApp } from 'vue';
import App from './App.vue';
import router from './router';

const app = createApp(App);
app.use(router);
app.mount('#app');
```

#### Step 3: Configure live-list File

Add the following code to your **live-list.vue** file to enable navigation from the Live Stream List to the viewing page.
``` typescript
// live-list.vue (can be incrementally added to your code)
<template>
  <UIKitProvider>
     <!-- Refer to Step 3 in Quick Integration above -->
     <LiveList @live-room-click="handleLiveRoomClick" />
  </UIKitProvider>
</template>

<script setup lang="ts">
import { useRouter, useRoute } from 'vue-router';

const router = useRouter();
const route = useRoute();

function handleLiveRoomClick(liveInfo: LiveInfo) {
  if (liveInfo?.liveId) {
    router.push({ path: '/live-player', query: { ...route.query, liveId: liveInfo.liveId } });
  }
}

</script>
```

## Customization

You can tailor the Live Stream List page UI to fit your project’s requirements. The table below summarizes key customization options.
| **Category** | **Feature** | **Description** |
| --- | --- | --- |
| **Live Room List** | Customize Live Room List display area | **Supports:** - **Show/hide live room info text, customize UI.** - **Set the number of live rooms per row/column.** |
| **Personal Info** | Customize personal info display | **Supports:** - **Show/hide personal info.** - **Customize font, color, and UI settings for personal info.** |

### Color Theme and Language

Change the default theme and language by configuring the `UIKitProvider` parameters in `App.vue`.
| UIKitProvider Parameter | Options | Default |
| --- | --- | --- |
| theme | "light" | "dark" |
| language | "zh-CN" | "en-US" |

``` typescript
<UIKitProvider theme="light">
  <router-view />
</UIKitProvider>
 
<script setup lang="ts">
import { UIKitProvider } from '@tencentcloud/uikit-base-component-vue3';
```

### Button and Icon Customization

Customize buttons, icons, and other controls as needed. For example, in `live-list.vue`, you can add, remove, or modify `Button` and `Icon` components. Beyond layout, you have full control over colors, fonts, border radius, input fields, and pop-ups to match your UI design.
| **Category** | **Feature** | **Description** |
| --- | --- | --- |
| **Asset Management** | Customize asset management display area | Supports adjusting icon size, color, or replacing icons. |
| **Live Tools** | Customize live tool info display | Supports adjusting icon size, color, or replacing icons. |
| **Online Audience** | Customize audience info display | Supports: - Show/hide audience level. - Customize audience info font, color, and UI settings. - Replace with your preferred icon style. |
| **Message List** | Customize live comments display area | Supports: - Show/hide chat input area. - Customize chat bubble style, audience level, and more. |

### Set Nickname and Avatar

To customize the nickname or avatar, use [setSelfInfo](https://web.sdk.qcloud.com/trtc/live/web/doc/zh/index.html#setSelfInfo) as shown in the sample code below:
``` typescript
import { useLoginState } from 'tuikit-atomicx-vue3';

const { setSelfInfo } = useLoginState();

// Set user personal info
await setSelfInfo({
  userName: 'Zhang San',
  avatarUrl: 'https://example.com/avatar.png',
});
```

## Next Steps

You’ve now integrated the **Live Stream List page**. Next, you can add the **Host Streaming Page**, **Audience Viewing Page**, and further **UI Customization** features. See the table below for links to each integration guide:
| **Feature** | **Description** | **Integration Guide** |
| --- | --- | --- |
| **Audience Viewing** | Allow audience to join the host’s live room and watch the stream, with features like guest co-hosting, live room info, online audience, and live comments. | Audience Viewing |
| **Host Streaming** | Host starts streaming and configures related settings on the current page. | Host Streaming |

---

This document provides a guide for integrating the **Host Live Start Page** from the TUILiveKit Demo. You'll learn how to embed our start page into your project and customize the style, layout, and features of the live streaming interface.

## Feature Demo
- **Landscape Go Live**

   

- **Portrait Go Live**

   

## Feature Overview
- **Scene Source Management**: Add multiple cameras, share your screen or windows, and use local images as sources.

- **Live Stream Layout**: Drag, zoom, and use quick menu actions for scene sources, including mirroring, rotation, and layer adjustments.

- **Audience Guest Feature**: Enable audience guest connections within the live room, with several built-in guest layouts.

- **Host PK**: Connect with other hosts across rooms for PK battles.

- **Interactive Chat**: Send and receive text and emoji messages for real-time chat.

- **Audience Management**: Mute or remove audience members from the live room.

## Quick Integration

### Step 1: Environment Setup and Service Activation

Before you begin, see Preparations for component integration and login implementation.

### Step 2: Install Dependencies

【npm】
``` bash
npm install tuikit-atomicx-vue3 @tencentcloud/uikit-base-component-vue3 --save
```

【pnpm】
``` bash
pnpm add tuikit-atomicx-vue3 @tencentcloud/livekit-web-vue3 @tencentcloud/uikit-base-component-vue3
```

【yarn】
``` bash
yarn add tuikit-atomicx-vue3 @tencentcloud/livekit-web-vue3 @tencentcloud/uikit-base-component-vue3
```

### Step 3: Integrate Host Go Live Page

Create a `live-pusher.vue` file in your project. Copy the code below into your new `live-pusher.vue` file to integrate the full **Host Live Start Page**.

> **Note：**
> 

> You can copy the code below directly into your project, or visit the [Live Start Page](https://github.com/Tencent-RTC/TUILiveKit/blob/main/Web/web-vite-vue3/src/TUILiveKit/LivePusherView.vue) for the full source code.
> 

``` typescript
<template>
  <UIKitProvider theme="dark">
    <div class="custom-live-pusher">
      <!-- Main Content Area -->
      <div class="main-content">
        <!-- Left: Scene Sources and Tools -->
        <div class="left-panel">
          <div class="scene-section">
            <div class="panel-title">Scene Source</div>
            <LiveScenePanel />
          </div>
        </div>

        <!-- Center: Live Stream Area -->
        <div class="center-panel">
          <div class="stream-section">
            <div class="stream-header">
              <div class="stream-title">
                <span>{{ liveName }}</span>
              </div>
              <div class="stream-audience">{{ audienceCount }} viewers</div>
            </div>
            <StreamMixer />
          </div>
          <div class="live-controls">
            <div class="bottom-panel">
              <!-- <MediaDeviceSetting />// For media settings, refer to the Advanced Feature Integration section below
              <CoGuestButton />          // For audience guest feature, refer to the Advanced Feature Integration section below
              <OrientationSwitch />      // For layout settings, refer to the Advanced Feature Integration section below
              <LayoutSwitch />           // For landscape/portrait streaming, refer to the Advanced Feature Integration section below -->
            </div>
            <TUIButton type="primary" v-if="!currentLive?.liveId" @click="handleStartLive">Start Live</TUIButton>
            <TUIButton color="red" v-else @click="handleStopLive">Stop Live</TUIButton>
          </div>
        </div>

        <!-- Right: Audience Interaction -->
        <div class="right-panel">
          <div class="audience-section">
            <div class="panel-title">Online Audience ({{ audienceCount }})</div>
            <LiveAudienceList />
          </div>
          <div class="message-section">
            <div class="panel-title">Message List</div>
            <BarrageList />
            <BarrageInput />
          </div>
        </div>

      </div>
    </div>
  </UIKitProvider>
</template>

<script setup lang="ts">
import { onMounted } from 'vue';
import { UIKitProvider, TUIButton } from '@tencentcloud/uikit-base-component-vue3';
import { LiveScenePanel, StreamMixer, LiveAudienceList, BarrageList, BarrageInput, useLiveListState, useLiveAudienceState, useLoginState } from 'tuikit-atomicx-vue3';

const { login, setSelfInfo } = useLoginState();
const { createLive, currentLive, endLive } = useLiveListState();
const { audienceCount } = useLiveAudienceState();
const liveName = 'My Live Room';

const handleStartLive = async () => {
  // Create live room
  await createLive({
    liveId: 'my-live-room',       // Live Room ID
    liveName: liveName,           // Live Room Name
    coverUrl: '',                 // Live Room Cover URL
    isPublicVisible: true,        // Publicly Visible
    seatLayoutTemplateId: 600,    // Seat Layout Template ID
  });
  // Set personal info
  await setSelfInfo({
    userName: 'My Name/Nickname', // Username
    avatarUrl: '',                // Avatar URL
  });
};

const handleStopLive = async () => {
  await endLive();
};

async function initLogin() {
  try {
    await login({
      sdkAppId: 0,        // SDKAppID, refer to Step 1 for details
      userId: '',         // UserID, refer to Step 1 for details
      userSig: '',        // userSig, refer to Step 1 for details
    });
  } catch (error) {
    console.error('Login failed:', error);
  }
}

onMounted(async () => {
  await initLogin();
});

</script>

<style>html,body,#app{height:100%;width:100%;margin:0;padding:0}</style>
<style scoped>.custom-live-pusher,.left-panel{flex-direction:column;display:flex}.custom-live-pusher,.live-title{color:var(--text-color-primary)}.live-controls,.tools-section,.top-controls{backdrop-filter:blur(10px)}*{box-sizing:border-box;margin:0;padding:0}:global(::before){box-sizing:border-box;margin:0;padding:0}.layout-label,.template-options{margin-bottom:16px}:global(body){line-height:1.6;color:var(--text-color-primary);background:var(--bg-color-default)}.custom-live-pusher{height:100vh;width:100vw;background:linear-gradient(135deg,var(--bg-color-default) 0,var(--bg-color-function) 100%);overflow:hidden}.top-controls{display:flex;justify-content:space-between;align-items:center;padding:12px 20px;background:var(--bg-color-operate);border-bottom:1px solid var(--stroke-color-primary);z-index:100;min-height:60px}.live-title{font-size:18px;font-weight:600;text-shadow:0 2px 4px var(--shadow-color)}.audience-count{font-size:14px;color:var(--text-color-error);background:var(--uikit-color-red-1);padding:6px 12px;border-radius:20px;border:1px solid var(--uikit-color-red-3)}.live-controls,.tools-section{background:var(--bg-color-operate)}.main-content{display:flex;flex:1;height:calc(100vh - 60px);gap:16px;padding:16px;overflow:hidden}.left-panel{width:320px;gap:16px;flex-shrink:0}.panel-title{font-size:16px;font-weight:600;color:var(--text-color-primary);margin-bottom:12px;text-align:left}.audience-section,.message-section,.scene-section{display:flex;flex-direction:column;background:var(--bg-color-operate);border-radius:12px;border:1px solid var(--stroke-color-primary);padding:16px;overflow:hidden}.scene-section{flex:1;min-height:0}.message-section{flex:1;min-height:0}.message-section :deep(input),.message-section :deep(textarea){text-align:left}.tools-section{border-radius:12px;padding:16px;border:1px solid var(--stroke-color-primary)}.center-panel{display:flex;flex-direction:column;flex:1;gap:16px;min-width:0}.stream-section{display:flex;flex-direction:column;flex:1;min-height:0;background:var(--bg-color-operate);border-radius:12px;border:1px solid var(--stroke-color-primary);overflow:hidden}.stream-header{display:flex;justify-content:space-between;align-items:center;padding:22px;border-bottom:1px solid var(--stroke-color-primary)}.stream-title{display:flex;align-items:center;gap:8px;font-size:18px;font-weight:500;color:var(--text-color-primary)}.stream-audience{font-size:14px;color:var(--text-color-primary)}.live-controls{display:flex;justify-content:space-between;align-items:center;padding:16px;border-radius:12px;border:1px solid var(--stroke-color-primary);gap:16px}.live-controls button{padding:18px 20px}.right-panel{display:flex;flex-direction:column;width:320px;gap:16px;flex-shrink:0}.center-panel>.live-controls,.left-panel>*,.right-panel>*{background:var(--bg-color-operate);border-radius:12px;border:1px solid var(--stroke-color-primary);overflow:hidden}.left-panel>*{padding:16px}.left-panel>.panel-title,.scene-section>.panel-title,.audience-section>.panel-title,.message-section>.panel-title{padding:0;background:transparent;border:none;border-radius:0}.custom-icon-container,.device-setting{padding:8px 12px;background:var(--bg-color-function)}.stream-section :deep(>*:last-child){flex:1;min-height:300px}.bottom-panel,.device-setting{align-items:center;display:flex}.custom-icon-container:hover,.option-card:hover{border-color:var(--stroke-color-primary);background:var(--list-color-hover)}.bottom-panel{gap:16px;flex:1}.device-setting{gap:8px;border-radius:8px;border:1px solid var(--stroke-color-secondary)}.device-icon{cursor:pointer;color:var(--text-color-primary);transition:color .2s}.device-icon:hover{color:var(--text-color-link)}.device-slider{width:80px}.custom-icon-container{display:flex;align-items:center;gap:6px;border-radius:8px;border:1px solid var(--stroke-color-secondary);cursor:pointer;transition:.2s;position:relative}.custom-icon-container.disabled{opacity:.5;cursor:not-allowed}.custom-icon-container.disabled:hover{background:var(--bg-color-function);border-color:var(--stroke-color-secondary)}.custom-icon{width:16px;height:16px;display:inline-block;background-size:contain;background-repeat:no-repeat;background-position:center}.custom-text{font-size:12px;color:var(--text-color-secondary);white-space:nowrap}.unread-count{position:absolute;top:-4px;right:-4px;background:var(--text-color-error);color:var(--text-color-button);border-radius:10px;padding:2px 6px;font-size:10px;font-weight:600;min-width:16px;text-align:center;line-height:1}.layout-label,.option-info h4{color:var(--text-color-primary)}.layout-dialog{max-width:600px}.layout-label{font-size:16px;font-weight:600}.options-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(120px,1fr));gap:12px}.option-card{padding:16px;background:var(--bg-color-function);border:2px solid var(--stroke-color-secondary);border-radius:8px;cursor:pointer;transition:.2s;text-align:center}.option-card.active{border-color:var(--text-color-link);background:var(--bg-color-operate)}.option-info h4{margin:8px 0 0;font-size:12px}.option-icon{width:32px;height:32px;margin:0 auto;color:var(--text-color-secondary)}.co-guest-dialog{max-width:500px}.co-guest-panel{min-height:300px}</style>
```

##### **createLive**

Creates a new live room and sets its basic information.
| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| liveId | String | Yes | Live Room ID, must be globally unique. |
| liveName | String | Yes | Live Room Name, displayed on the UI. |
| coverUrl | String | No | Live Room cover image URL. |
| isPublicVisible | Boolean | No | Whether the room is publicly visible. Defaults to true. |
| seatLayoutTemplateId | Number | No | Seat layout template ID. 600 represents portrait dynamic grid layout. For more template IDs, refer to the Advanced Features section. |

##### setSelfInfo

Sets user information.
| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| userName | String | Yes | User nickname, displayed in the live room and chat area. |
| avatarUrl | String | No | User avatar image URL. |

### Step 4: Start Live Streaming

Start your first live stream.
``` bash
  npm run dev
```

> **Note：**
> 

> After running the above command, open your browser and enter the local address (for example, `http://localhost:5173/live-pusher`; the port may vary by project) to view the live start page.
> 

### Step 5: Watch the Live Stream
- **Method 1 (Recommended):**

    Instantly watch your live stream via our [online viewing site](https://web.sdk.qcloud.com/trtc/livekit/player/index.html).

- **Method 2:**

    Integrate our Audience Viewing (Web Desktop Browser) or Audience Viewing (H5 Mobile Browser) page to watch the live stream.
   

   > **Important Tip:****：**
   > 

   > Use different **userID **for streaming and viewing: The host and audience must use **different** userID. If the same **userID** is used, the second device to log in will force the first device offline.
   > 

## Advanced Feature Integration

> **Note：**
> 

> All advanced features below are extensions based on the `live-pusher.vue` sample file created in Step 3. 
> 

> Depending on your requirements, add the following code snippets to the appropriate sections of `live-pusher.vue` (either in the template or script) to enable each feature.
> 

【Enable Media Device Settings】

To support media device settings, including adjusting speaker and microphone volume, copy the following code into your `live-pusher.vue` file.
``` typescript
<!-- LayoutSwitch Landscape/Portrait Streaming Settings -->
<template>
  <div
    class="custom-icon-container"
    :class="{ disabled: currentLive?.liveId }"
    @click="handleOrientationSwitch"
  >
    <IconHorizontalMode
      v-if="currentOrientation === LiveOrientation.Landscape"
      class="custom-icon"
    />
    <IconPortrait
      v-else
      class="custom-icon"
    />
    <span class="custom-text co-guest-text">{{
      currentOrientation === LiveOrientation.Portrait ? t('Portrait') : t('Landscape')
    }}</span>
  </div>
</template>

<script setup lang="ts">
import { ref, watch } from 'vue';
import { useUIKit, TUIToast, TOAST_TYPE, IconPortrait, IconHorizontalMode } from '@tencentcloud/uikit-base-component-vue3';
import { useLiveListState, LiveOrientation } from 'tuikit-atomicx-vue3';

const { t } = useUIKit();

enum TUISeatLayoutTemplate {
  LandscapeDynamic_1v3 = 200,
  PortraitDynamic_Grid9 = 600,
  PortraitDynamic_1v6 = 601,
  PortraitFixed_Grid9 = 800,
  PortraitFixed_1v6 = 801,
  PortraitFixed_6v6 = 802,
}

const { currentLive, updateLiveInfo } = useLiveListState();
const currentOrientation = ref(LiveOrientation.Portrait);

watch(
  () => currentLive.value?.layoutTemplate,
  newVal => {
    if (newVal === TUISeatLayoutTemplate.LandscapeDynamic_1v3) {
      currentOrientation.value = LiveOrientation.Landscape;
    } else {
      currentOrientation.value = LiveOrientation.Portrait;
    }
  },
  { immediate: true }
);

const handleOrientationSwitch = () => {
  if (currentLive.value?.liveId) {
    TUIToast({
      message: t('Cannot switch orientation during live streaming'),
      type: TOAST_TYPE.ERROR,
    });
    return;
  }
  if (currentOrientation.value === LiveOrientation.Portrait) {
    updateLiveInfo({ layoutTemplate: TUISeatLayoutTemplate.LandscapeDynamic_1v3 });
  } else {
    updateLiveInfo({ layoutTemplate: TUISeatLayoutTemplate.PortraitDynamic_Grid9 });
  }
};
</script>

<style scoped>.custom-icon-container{display:flex;flex-direction:column;align-items:center;justify-content:center;gap:4px;width:56px;height:56px;cursor:pointer;color:var(--text-color-primary);border-radius:12px;position:relative}.custom-icon{width:24px;height:24px;background:transparent}.custom-text{font-size:12px}.custom-icon-container:not(.disabled):hover{box-shadow:0 0 10px 0 var(--bg-color-mask)}.custom-icon-container:not(.disabled):hover .custom-icon,.custom-icon-container:not(.disabled):hover .custom-text{color:var(--text-color-link)}.custom-icon-container.disabled{cursor:not-allowed;opacity:.5;color:var(--text-color-secondary)}.custom-icon-container.disabled .custom-icon,.custom-icon-container.disabled .custom-text{color:var(--text-color-secondary);cursor:not-allowed}</style>
```

【Enable Landscape/Portrait Streaming Feature】

To support switching between landscape and portrait streaming, copy the following code into your `live-pusher.vue` file.
``` typescript
<!-- LayoutSwitch 横竖屏推流设置 -->
<template>
  <div
    class="custom-icon-container"
    :class="{ disabled: currentLive?.liveId }"
    @click="handleOrientationSwitch"
  >
    <IconHorizontalMode
      v-if="currentOrientation === LiveOrientation.Landscape"
      class="custom-icon"
    />
    <IconPortrait
      v-else
      class="custom-icon"
    />
    <span class="custom-text co-guest-text">{{
      currentOrientation === LiveOrientation.Portrait ? t('Portrait') : t('Landscape')
    }}</span>
  </div>
</template>

<script setup lang="ts">
import { ref, watch } from 'vue';
import { useUIKit, TUIToast, TOAST_TYPE, IconPortrait, IconHorizontalMode } from '@tencentcloud/uikit-base-component-vue3';
import { useLiveListState, LiveOrientation } from 'tuikit-atomicx-vue3';

const { t } = useUIKit();

enum TUISeatLayoutTemplate {
  LandscapeDynamic_1v3 = 200,
  PortraitDynamic_Grid9 = 600,
  PortraitDynamic_1v6 = 601,
  PortraitFixed_Grid9 = 800,
  PortraitFixed_1v6 = 801,
  PortraitFixed_6v6 = 802,
}

const { currentLive, updateLiveInfo } = useLiveListState();
const currentOrientation = ref(LiveOrientation.Portrait);

watch(
  () => currentLive.value?.layoutTemplate,
  newVal => {
    if (newVal === TUISeatLayoutTemplate.LandscapeDynamic_1v3) {
      currentOrientation.value = LiveOrientation.Landscape;
    } else {
      currentOrientation.value = LiveOrientation.Portrait;
    }
  },
  { immediate: true }
);

const handleOrientationSwitch = () => {
  if (currentLive.value?.liveId) {
    TUIToast({
      message: t('Cannot switch orientation during live streaming'),
      type: TOAST_TYPE.ERROR,
    });
    return;
  }
  if (currentOrientation.value === LiveOrientation.Portrait) {
    updateLiveInfo({ layoutTemplate: TUISeatLayoutTemplate.LandscapeDynamic_1v3 });
  } else {
    updateLiveInfo({ layoutTemplate: TUISeatLayoutTemplate.PortraitDynamic_Grid9 });
  }
};
</script>

<style scoped>.custom-icon-container{display:flex;flex-direction:column;align-items:center;justify-content:center;gap:4px;width:56px;height:56px;cursor:pointer;color:var(--text-color-primary);border-radius:12px;position:relative}.custom-icon{width:24px;height:24px;background:transparent}.custom-text{font-size:12px}.custom-icon-container:not(.disabled):hover{box-shadow:0 0 10px 0 var(--bg-color-mask)}.custom-icon-container:not(.disabled):hover .custom-icon,.custom-icon-container:not(.disabled):hover .custom-text{color:var(--text-color-link)}.custom-icon-container.disabled{cursor:not-allowed;opacity:.5;color:var(--text-color-secondary)}.custom-icon-container.disabled .custom-icon,.custom-icon-container.disabled .custom-text{color:var(--text-color-secondary);cursor:not-allowed}</style>
```

【Enable Audience Guest Feature】

To support the audience guest feature, including guest requests and management, copy the following code into your `live-pusher.vue` file.
``` typescript
<!-- CoGuestButton Audience Guest Settings -->
<template>
  <div class="custom-icon-container" :class="{ disabled: disabled }" @click="handleCoGuest">
    <span v-if="applicants.length > 0" class="unread-count">{{ applicants.length }}</span>
    <IconCoGuest class="custom-icon" />
    <span class="custom-text co-guest-text">{{ t('CoGuest') }}</span>
  </div>
  <TUIDialog :title="t('CoGuest')" :visible="coGuestPanelVisible" :custom-classes="['co-guest-dialog']" @close="coGuestPanelVisible = false" @confirm="coGuestPanelVisible = false" @cancel="coGuestPanelVisible = false">
    <CoGuestPanel class="co-guest-panel" />
    <template #footer>
      <div />
    </template>
  </TUIDialog>
</template>

<script lang="ts" setup>
import { computed, ref, watch } from 'vue';
import { useUIKit, TUIDialog, TUIToast, TOAST_TYPE, IconCoGuest } from '@tencentcloud/uikit-base-component-vue3';
import { CoGuestPanel, CoHostStatus, useCoGuestState, useCoHostState, useLiveListState } from 'tuikit-atomicx-vue3';

const { t } = useUIKit();
const { applicants } = useCoGuestState();
const { currentLive } = useLiveListState();
const { coHostStatus } = useCoHostState();
const disabled = computed(() => !currentLive.value?.liveId || coHostStatus.value !== CoHostStatus.Disconnected);

const coGuestPanelVisible = ref(false);

const handleCoGuest = () => {
  if (disabled.value) {
    const message = !currentLive.value?.liveId
      ? t('Cannot use co-guest before live starts')
      : t('Cannot enable audience co-hosting while co-hosting with other hosts');
    TUIToast({ type: TOAST_TYPE.ERROR, message });
    return;
  }
  coGuestPanelVisible.value = true;
};

watch(disabled, () => {
  if (disabled.value) {
    coGuestPanelVisible.value = false;
  }
});
</script>
<style scoped>.custom-icon-container{display:flex;flex-direction:column;align-items:center;justify-content:center;gap:4px;width:56px;height:56px;cursor:pointer;color:var(--text-color-primary);border-radius:12px;position:relative}.unread-count{position:absolute;top:0;right:0;background-color:var(--text-color-error);border-radius:50%;width:16px;height:16px;display:flex;align-items:center;justify-content:center;font-size:12px}.custom-icon{width:24px;height:24px;background:transparent}.custom-text{font-size:12px}.custom-icon-container:not(.disabled):hover{box-shadow:0 0 10px 0 var(--bg-color-mask)}.custom-icon-container:not(.disabled):hover .custom-icon,.custom-icon-container:not(.disabled):hover .custom-text{color:var(--text-color-link)}.custom-icon-container.disabled{cursor:not-allowed;opacity:.5;color:var(--text-color-secondary)}.custom-icon-container.disabled .custom-icon{cursor:not-allowed}.custom-icon-container.disabled .custom-text{color:var(--text-color-secondary)}.co-guest-panel{height:560px}:deep(.co-guest-dialog){width:520px}</style>
```

【Enable Layout Settings Feature】

To support video stream layout switching, including **dynamic grid layout, static grid layout, static small window layout, floating small window layout**, copy the following code into your `live-pusher.vue` file.
``` typescript
<!-- OrientationSwitch Layout Settings -->
<template>
  <div
    class="custom-icon-container"
    :class="{ 'disabled': disabled }"
    @click="handleSwitchLayout"
  >
    <IconLayoutTemplate class="custom-icon" />
    <span class="custom-text setting-text">{{ t('Layout Settings') }}</span>
  </div>
  <TUIDialog
    :customClasses="['layout-dialog']"
    :title="t('Layout Settings')"
    :visible="layoutSwitchVisible"
    @close="handleCancel"
    @confirm="handleConfirm"
    @cancel="handleCancel"
    appendTo="body"
  >
    <div class="layout-label">
      {{ t('Audience Layout') }}
    </div>
    <div class="template-options">
      <div class="options-grid">
        <template
          v-for="template in layoutOptions"
          :key="template.id"
        >
          <div
            class="option-card"
            :class="{ active: selectedTemplate === template.templateId }"
            @click="selectTemplate(template.templateId)"
          >
            <div class="option-info">
              <component
                :is="template.icon"
                v-if="template.icon"
                class="option-icon"
              />
              <h4>{{ template.label }}</h4>
            </div>
          </div>
        </template>
      </div>
    </div>
  </TUIDialog>
</template>

<script lang="ts" setup>
import { ref, computed, watch, h, defineComponent } from 'vue';
import { TUIErrorCode } from '@tencentcloud/tuiroom-engine-js';
import { useUIKit, TUIDialog, TUIToast, TOAST_TYPE, IconLayoutTemplate } from '@tencentcloud/uikit-base-component-vue3';
import { useLiveListState, useCoHostState, CoHostStatus } from 'tuikit-atomicx-vue3';

/**
 * Live Room Seat Layout Templates
 */
enum TUISeatLayoutTemplate {
  LandscapeDynamic_1v3 = 200,
  PortraitDynamic_Grid9 = 600,
  PortraitDynamic_1v6 = 601,
  PortraitFixed_Grid9 = 800,
  PortraitFixed_1v6 = 801,
  PortraitFixed_6v6 = 802,
}

const createSvgIcon = (pathD: string) => defineComponent({
  render: () => h('svg', { xmlns: 'http://www.w3.org/2000/svg', viewBox: '0 0 24 24', fill: 'currentColor', width: '24', height: '24' }, [h('path', { d: pathD })])
});

const Dynamic1v6 = createSvgIcon('M3 3h7v7H3V3zm11 0h7v4h-7V3zm0 6h7v4h-7V9zm0 6h7v6h-7v-6zM3 12h7v9H3v-9z');
const DynamicGrid9 = createSvgIcon('M3 3h5v5H3V3zm7 0h4v5h-4V3zm6 0h5v5h-5V3zM3 10h5v4H3v-4zm7 0h4v4h-4v-4zm6 0h5v4h-5v-4zM3 16h5v5H3v-5zm7 0h4v5h-4v-5zm6 0h5v5h-5v-5z');
const Fixed1v6 = createSvgIcon('M2 2h9v9H2V2zm11 0h9v4h-9V2zm0 5h9v4h-9V7zm0 5h9v4h-9v-4zm0 5h9v5h-9v-5zM2 13h9v9H2v-9z');
const FixedGrid9 = createSvgIcon('M2 2h6v6H2V2zm7 0h6v6H9V2zm7 0h6v6h-6V2zM2 9h6v6H2V9zm7 0h6v6H9V9zm7 0h6v6h-6V9zM2 16h6v6H2v-6zm7 0h6v6H9v-6zm7 0h6v6h-6v-6z');
const HorizontalFloat = createSvgIcon('M2 4h20v12H2V4zm3 14h4v2H5v-2zm6 0h4v2h-4v-2zm6 0h4v2h-4v-2z');

const { t } = useUIKit();
const { currentLive, updateLiveInfo } = useLiveListState();
const { coHostStatus } = useCoHostState();
const disabled = computed(() => coHostStatus.value === CoHostStatus.Connected);

watch(
  () => currentLive.value?.liveId,
  (liveId) => {
    if (!liveId) {
      updateLiveInfo({ layoutTemplate: TUISeatLayoutTemplate.PortraitDynamic_Grid9 });
    }
  },
  { immediate: true },
);

const layoutSwitchVisible = ref(false);

const handleSwitchLayout = () => {
  if (disabled.value) {
    TUIToast({ type: TOAST_TYPE.ERROR, message: t('Layout switching is not available during co-hosting') });
    return;
  }
  layoutSwitchVisible.value = true;
};

const portraitLayoutOptions = computed(() => [
  {
    id: 'PortraitDynamic_Grid9',
    icon: DynamicGrid9,
    templateId: TUISeatLayoutTemplate.PortraitDynamic_Grid9,
    label: t('Dynamic Grid9 Layout'),
  },
  {
    id: 'PortraitFixed_1v6',
    icon: Fixed1v6,
    templateId: TUISeatLayoutTemplate.PortraitFixed_1v6,
    label: t('Fixed 1v6 Layout'),
  },
  {
    id: 'PortraitFixed_Grid9',
    icon: FixedGrid9,
    templateId: TUISeatLayoutTemplate.PortraitFixed_Grid9,
    label: t('Fixed Grid9 Layout'),
  },
  {
    id: 'PortraitDynamic_1v6',
    icon: Dynamic1v6,
    templateId: TUISeatLayoutTemplate.PortraitDynamic_1v6,
    label: t('Dynamic 1v6 Layout'),
  },
]);

const horizontalLayoutOptions = computed(() => [
  {
    id: 'LandscapeDynamic_1v3',
    icon: HorizontalFloat,
    templateId: TUISeatLayoutTemplate.LandscapeDynamic_1v3,
    label: t('Landscape Template'),
  },
]);

const layoutOptions = computed(() => {
  if (currentLive.value && currentLive.value?.layoutTemplate >= 200 && currentLive.value?.layoutTemplate <= 599) {
    return horizontalLayoutOptions.value;
  }
  return portraitLayoutOptions.value;
});

const selectedTemplate = ref<TUISeatLayoutTemplate | null>(currentLive.value?.layoutTemplate ?? null);

function selectTemplate(template: TUISeatLayoutTemplate) {
  selectedTemplate.value = template;
}

watch(() => currentLive.value?.layoutTemplate, (newVal) => {
  if (newVal) {
    selectedTemplate.value = newVal;
  }
});

async function handleConfirm() {
  if (selectedTemplate.value) {
    try {
      await updateLiveInfo({ layoutTemplate: selectedTemplate.value });
      layoutSwitchVisible.value = false;
    } catch (error: any) {
      let errorMessage = t('Layout switch failed');
      if (error.code === TUIErrorCode.ERR_FREQ_LIMIT) {
        errorMessage = t('Operation too frequent, please try again later');
      }
      TUIToast({ type: TOAST_TYPE.ERROR, message: errorMessage });
    }
  } else {
    layoutSwitchVisible.value = false;
  }
}

function handleCancel() {
  selectedTemplate.value = currentLive.value?.layoutTemplate ?? null;
  layoutSwitchVisible.value = false;
}
</script>

<style scoped>
.custom-icon-container { display: flex; flex-direction: column; align-items: center; justify-content: center; gap: 4px; width: 56px; height: 56px; cursor: pointer; color: var(--text-color-primary); border-radius: 12px; position: relative; } .custom-icon-container .custom-icon { display: inline-block; width: 24px; height: 24px; background: transparent; } .custom-icon-container .custom-text { font-size: 12px; font-weight: 400; } .custom-icon-container:not(.disabled):hover { box-shadow: 0 0 10px 0 var(--bg-color-mask); } .custom-icon-container:not(.disabled):hover .custom-icon { color: var(--text-color-link); } .custom-icon-container:not(.disabled):hover .custom-text { color: var(--text-color-link); } .custom-icon-container.disabled { cursor: not-allowed; opacity: 0.5; color: var(--text-color-tertiary); } .custom-icon-container.disabled .custom-icon { color: var(--text-color-tertiary); cursor: not-allowed; } .custom-icon-container.disabled .custom-text { color: var(--text-color-tertiary); } :deep(.layout-dialog) { padding: 24px; width: 480px; } :deep(.layout-dialog) .dialog-body { flex-wrap: wrap; } :deep(.layout-dialog) .dialog-footer { padding-top: 32px; } .layout-label { font-size: 14px; font-weight: 400; color: var(--text-color-primary, #ffffff); margin: 4px 0px 16px 0px; } .template-options { width: 100%; height: 100%; overflow: auto; } .template-options .options-grid { display: flex; flex-wrap: wrap; gap: 16px; justify-content: flex-start; } .template-options .options-grid .option-card { box-sizing: border-box; padding: 12px 13px; width: 208px; background: #3a3a3a; border: 2px solid transparent; border-radius: 12px; cursor: pointer; transition: all 0.2s ease; text-align: center; } .template-options .options-grid .option-card:hover { background: #4a4a4a; border-color: #5a5a5a; } .template-options .options-grid .option-card.active { border: 2px solid var(--text-color-link-hover, #2B6AD6); background: var(--list-color-focused, #243047); } .template-options .options-grid .option-card.active .option-info h4 { color: #ffffff; } .template-options .options-grid .option-card .option-info { display: flex; align-items: center; justify-content: flex-start; gap: 8px; } .template-options .options-grid .option-card .option-info .option-icon { width: 24px; height: 24px; } .template-options .options-grid .option-card .option-info h4 { margin: 0; font-size: 14px; font-weight: 600; color: #ffffff; transition: color 0.2s ease; }
</style>
```

## Customize Layout

`TUILiveKit` offers flexible customization for both the start page and live room features and styles. You can adjust the layout and show or hide feature modules to fit your business needs.

### Landscape/Portrait Streaming Settings

`TUILiveKit` supports both **landscape** and **portrait** streaming modes. Choose the streaming direction that best fits your scenario:
| **Streaming Mode** | **Applicable Scenarios** | **Description** |
| --- | --- | --- |
| **Portrait Streaming** | Showroom Live, E-commerce, Chat Interaction | Default mode, optimized for mobile viewing, aspect ratio 9:16. |
| **Landscape Streaming** | Game Streaming, Online Education, Conference Streaming | Optimized for desktop viewing, aspect ratio 16:9. |

> **Note：**
> 

> You must set the streaming direction **before starting the live stream**; you cannot switch directions during a live session.
> 

#### Switch via UI

On the host live start page's bottom control bar, click the **Landscape/Portrait** button to change the streaming direction:
- **Portrait** indicates portrait streaming mode.

- **Landscape** indicates landscape streaming mode.

#### Switch via Code

You can also set the streaming direction in code by calling `updateLiveInfo`:
``` typescript
import { useLiveListState } from 'tuikit-atomicx-vue3';

const { updateLiveInfo } = useLiveListState();

// Switch to landscape mode (template ID: 200)
updateLiveInfo({ layoutTemplate: 200 });

// Switch to portrait mode (template ID: 600)
updateLiveInfo({ layoutTemplate: 600 });
```

> **Note：**
> 
> - Landscape mode uses template IDs 200-599, with 200 (landscape floating layout) as the default.
> - Portrait mode uses template IDs 600-899, with 600 (dynamic grid layout) as the default.
> - When switching between landscape and portrait, the system automatically applies the default template for that direction.

### Live Stream Layout Template Selection

`TUILiveKit` provides multiple layout templates to control how host and guest video feeds are arranged. Select your preferred style in the host live start page's **Layout Settings**:

#### Portrait Mode Layout Templates

Portrait mode offers **4 layout templates**, ideal for showroom live, e-commerce, and similar scenarios:
| **Name** | **Dynamic Grid Layout** | **Dynamic 1V6 Layout** | **Static Grid Layout** | **Static Small Window Layout** |
| --- | --- | --- | --- | --- |
| **Template ID** | 600 | 601 | 800 | 801 |
| **Description** | **Default layout**; grid size adjusts dynamically based on guest count, auto-filling the screen. | Host is centered in a large window, guests appear as **floating small windows** around the host. | Fixed 9-grid layout; each guest occupies a **fixed-size** grid slot. | Host is full screen, guests are shown as **fixed small windows** at the screen edges. |
| **Applicable Scenarios** | General scenarios with variable guest count. | Host-centric, guest-assisted interaction scenarios. | Multi-guest, Voice Chat Room, or fixed participant scenarios. | Host full-screen display, guest auxiliary scenarios. |

#### Landscape Mode Layout Template

Landscape mode provides **1 layout template**, suitable for game streaming, online education, and more:
| **Name** | **Landscape Floating Layout** |
| --- | --- |
| **Template ID** | 200 |
| **Description** | Host is full screen, guests are shown as **floating small windows** at the bottom of the screen. |
| **Applicable Scenarios** | Game streaming, screen sharing, online education, and other landscape scenarios. |

#### Set Layout Template via Code

Set the layout template in code by calling `updateLiveInfo`:
``` typescript
import { useLiveListState } from 'tuikit-atomicx-vue3';

const { updateLiveInfo } = useLiveListState();

// Set portrait dynamic grid layout
updateLiveInfo({ layoutTemplate: 600 });

// Set portrait dynamic 1v6 layout
updateLiveInfo({ layoutTemplate: 601 });

// Set portrait static grid layout
updateLiveInfo({ layoutTemplate: 800 });

// Set portrait static 1v6 layout
updateLiveInfo({ layoutTemplate: 801 });

// Set landscape floating layout
updateLiveInfo({ layoutTemplate: 200 });
```

> **Note：**
> 
> - You can switch layout templates **before** starting the live stream and **during** the session.
> - During host PK, **layout templates cannot be switched**.
> - When switching streaming direction, the layout template automatically changes to the default for that direction.

## Free Customization

### Color Theme and Language

Change the default theme and language by configuring `UIKitProvider` parameters in `App.vue`.
| **UIKitProvider Parameter** | **Options** | **Default** |
| --- | --- | --- |
| theme | "light" \\| "dark" | "light" |
| language | "zh-CN" \\| "en-US" | - |

``` typescript
<UIKitProvider theme="light">
  <router-view />
</UIKitProvider>
 
<script setup lang="ts">
import { UIKitProvider } from '@tencentcloud/uikit-base-component-vue3';
```

### Buttons and Icons

To add or replace Button or Icon controls for further UI customization, follow the example below. In the `live-player.vue` file, you can refer to the diagram to locate the source code for each button or icon, then **add, remove, or replace** UI controls as needed.

You can also customize the **audience viewing page** UI as needed. In addition to layout adjustments, you can freely **add, remove, or modify** color themes, fonts, border radius, buttons, icons, input boxes, dialogs, and more to meet your UI requirements.
| **Category** | **Feature** | **Description** | **Component Customization Guide** |
| --- | --- | --- | --- |
| **Asset Management** | Customize asset management area display | **Supports:** - **Adjust icon size, color, or replace icons.** | Media Source Configuration Panel |
| **Online Audience** | Customize audience info display | **Supports:** - **Show/hide audience level.** - **Customize font and color of audience info.** - **Replace icon style as needed.** | Video Source Editing Canvas |
| **Message List** | Customize live comments area display | **Supports:** - **Show/hide chat input area.** - **Customize chat bubble style, audience level, etc.** | Live Comments Component |

## Next Steps

Congratulations! You've successfully integrated the **Host Live Start Page**. Next, you can implement the **Audience Viewing Page**, **Live Stream List Page**, and further UI customization. See the table below:
| **Feature** | **Description** | **Integration Guide** |
| --- | --- | --- |
| **Audience Viewing** | Enable audience to enter the host's live room and watch the stream, including audience guest, live room info, online audience, live comments, and more. | Audience Viewing |
| **Live Stream List** | Display the live stream list interface and features, including live stream list and room info display. | Live Stream List |

---

This guide provides a comprehensive overview of the **Viewer Page** in the TUILiveKit Demo. Use this documentation to quickly integrate our pre-built viewer page into your project, or leverage the details here to fully customize its style, layout, and features to fit your specific needs.

## Feature Overview

The viewer page comes with default functionality and styling out of the box. If these defaults don’t match your requirements, you can easily tailor the UI. The numbers in the screenshot map to the main feature categories. Core features include: **stream information display, live video area, online audience, audio/video controls, live duration, resolution switching, fullscreen mode, chat interaction, and message list**.
- **Live Video Playback**: High-definition, low-latency streaming.

- **Live Comments Interaction**: Real-time live comments for audience engagement.

- **Audience List**: View details about online audience members.

- **Fullscreen Playback**: Immersive viewing experience.

- **H5 Mobile Platform Support**: Works seamlessly across platforms.

   

## Quick Integration

### Step 1: Environment Setup and Activate the Service

Before you begin, see Preparation for instructions on integrating required components and implementing login.

### Step 2: Install Dependencies

Install the necessary packages using your preferred package manager:

【npm】
``` bash
npm install tuikit-atomicx-vue3 @tencentcloud/uikit-base-component-vue3 --save
```

【pnpm】
``` bash
pnpm add tuikit-atomicx-vue3 @tencentcloud/uikit-base-component-vue3
```

【yarn】
``` bash
yarn add tuikit-atomicx-vue3 @tencentcloud/uikit-base-component-vue3
```

### Step 3: Integrate Viewer Page

Create a `live-player.vue` file in your project. Copy and paste the following code to add the **viewer page**.

> **Note：**
> 

> You can use the code below directly, or refer to [Audience Viewing](https://github.com/Tencent-RTC/TUILiveKit/blob/main/Web/web-vite-vue3/src/TUILiveKit/component/LivePlayer/LivePlayerPC.vue) for the full source.
> 

``` typescript
<template>
  <UIKitProvider theme="dark">
    <div class="container">
      <!-- Live Core Area -->
      <section class="live">
        <header class="header">
          <IconArrowStrokeBack class="back-btn" size="20" />
          <Avatar :src="currentLive?.liveOwner.avatarUrl" :size="32" class="avatar" />
          <span class="user-name">{{ currentLive?.liveOwner.userName || currentLive?.liveOwner.userId }}</span>
        </header>
        <LiveCoreView class="player" />
      </section>

      <div class="sidebar">
        <!-- Online Audience List -->
        <section class="audience">
          <header class="section-header">
            <h3> Online Audience <span>({{ audienceList.length }})</span></h3>
          </header>
          <LiveAudienceList class="list" />
        </section>

        <!-- Message List & Input Box -->
        <section class="barrage">
          <header class="section-header">
            <h3>Message List</h3>
          </header>
          <BarrageList class="list" />
          <BarrageInput class="input" height="48px" />
        </section>
      </div>
    </div>
  </UIKitProvider>
</template>

<script setup lang="ts">
import { onMounted } from 'vue';
import { LiveAudienceList, BarrageList, BarrageInput, useLiveAudienceState, LiveCoreView, useLiveListState, Avatar, useLoginState } from 'tuikit-atomicx-vue3';
import { UIKitProvider, IconArrowStrokeBack } from '@tencentcloud/uikit-base-component-vue3';

const { audienceList } = useLiveAudienceState();
const { currentLive, joinLive } = useLiveListState();
const { login, setSelfInfo } = useLoginState();

const liveId = 'live_xxxx'  // Enter the ID of the live stream you want to watch

async function initLogin() {
  try {
    await login({
      sdkAppId: 0,     // SDKAppID, refer to Step 1 for details
      userId: '',      // UserID, refer to Step 1 for details
      userSig: '',     // userSig, refer to Step 1 for details
    });
  } catch (error) {
    console.error('Login failed:', error);
  }
}

onMounted(async () => {
  await initLogin();
  await setSelfInfo({
    userName: 'Your Name/Nickname',    // Username
    avatarUrl: '',                     // Avatar URL
  });
  await joinLive({ liveId });
});
</script>

<style>html,body,#app{height:100%;width:100%;margin:0;padding:0;overflow:hidden}:global(body){font-size:15px;line-height:1.6;text-rendering:optimizeLegibility;}:global(*),:global(*::before),:global(*::after){box-sizing:border-box;margin:0;}.container{display:grid;grid-template-columns:1fr 320px;height:100%;width:100%;gap:16px;padding:16px;background:var(--bg-color-default);box-sizing:border-box;overflow:hidden;}.live{display:flex;flex-direction:column;background:var(--bg-color-operate);border-radius:12px;overflow:hidden;box-shadow:0 2px 8px var(--shadow-color);}.header{display:flex;align-items:center;gap:12px;padding:16px;border-bottom:1px solid var(--stroke-color-primary);}.back-btn{cursor:pointer;color:var(--text-color-tertiary);transition:color 0.2s;}.back-btn:hover{color:var(--text-color-link-hover);}.avatar{border:1px solid var(--uikit-color-white-7);}.user-name{color:var(--text-color-primary);font-weight:500;}.player{flex:1;background:var(--uikit-color-black-1);min-height:0;}.sidebar{display:flex;flex-direction:column;gap:16px;height:100%;overflow:hidden;}.audience{display:flex;flex-direction:column;background:var(--bg-color-operate);border-radius:12px;overflow:hidden;box-shadow:0 2px 8px var(--shadow-color);flex:1;min-height:0;}.barrage{display:flex;flex-direction:column;background:var(--bg-color-operate);border-radius:12px;overflow:hidden;box-shadow:0 2px 8px var(--shadow-color);flex:1;min-height:0;}.section-header{padding:16px;border-bottom:1px solid var(--stroke-color-primary);background:var(--bg-color-operate);}.section-header h3{margin:0;font-size:16px;font-weight:600;color:var(--text-color-primary);}.section-header span{font-weight:400;color:var(--text-color-secondary);font-size:14px;}.list{flex:1;min-height:0;overflow-y:auto;}.input{border-top:1px solid var(--stroke-color-primary);flex-shrink:0;height:48px;}@media (max-width:1200px){.container{grid-template-columns:1fr;grid-template-rows:60% 20% 20%;gap:12px;}.sidebar{gap:12px;}.audience,.barrage{min-height:200px;}}@media (max-width:768px){.container{padding:8px;gap:8px;grid-template-rows:50% 25% 25%;}.header,.section-header{padding:12px;}.sidebar{gap:8px;}}</style>
```

#### Core API Parameters

##### setSelfInfo

Configure user information.
| Parameters | Type | Required | Description |
| --- | --- | --- | --- |
| userName | String | Yes | User nickname, shown in the live room and chat area. |
| avatarUrl | String | No | URL of the user's avatar image. |

### Step 4: Start the Project

Open your terminal, navigate to your project directory, and run the following command to launch the project. You’ll then be able to view the live stream.

> **Note：**
> 

> After the command runs successfully, enter your local access URL in your browser (for example, `http://localhost:5173/live-player`; the port may vary based on your setup) to access the viewer page.
> 

``` bash
npm run dev
```

## Play Live Stream

### Step 1: Start a Live Stream
- **Method 1 (Recommended):**

   Use our [Online Hosting Website](https://web.sdk.qcloud.com/trtc/livekit/pusher/index.html) to start a live stream. After starting, copy the live stream room ID.

- **Method 2:**

   Integrate our Host Streaming (Web Desktop Browser) to start a live stream. After starting, copy the live stream room ID.
   

   > **Tips：**
   > 

   > Use different **userID** for hosting and viewing. If the same user ID logs in on multiple devices, the later login will force the earlier device offline (**kick offline**).
   > 

### Step 2: Watch the Live Stream

Refer to the sample code from Step 3 of Quick Integration. Enter the corresponding `liveId` to join the live room and view the stream.

### Step 3: Router Configuration

To enable navigation from the Live Stream List or homepage to the live room, configure Vue Router. In your project’s **src** directory, create a **router** folder and an **index.ts** file. Import and use the router in your main entry file (such as **main.ts** or **index.ts**). For reference, see the [GitHub code example](https://github.com/Tencent-RTC/TUILiveKit/blob/main/Web/web-vite-vue3/src/main.ts). If you need the Live Stream List feature, check the Live Stream List documentation.

> **Note：**
> 

> In the code below, `live-player.vue` refers to the sample file created in Step 3.
> 

``` typescript
// src/router/index.ts
import { createRouter, createWebHistory } from 'vue-router';

const routes = [
  {
    path: '/live-player',
    component: () => import('../live-player.vue'),
  },
  // To add the Live Stream List feature, include the following route. Update the path as needed for your project.
  // {
  //   path: '/live-list',
  //   component: () => import('../live-list.vue'),
  // },
];

const router = createRouter({
  history: createWebHistory(),
  routes,
});
export default router;

// src/main.ts
import { createApp } from 'vue';
import App from './App.vue';
import router from './router';

const app = createApp(App);
app.use(router);
app.mount('#app');
```

## Customization

### Customize Theme and Language

You can change the default theme and language by setting parameters in `UIKitProvider` within `App.vue`.
| UIKitProvider Parameter | Options | Default Value |
| --- | --- | --- |
| theme | "light" | "dark" |
| language | "zh-CN" | "en-US" |

``` typescript
<UIKitProvider theme="light">
  <router-view />
</UIKitProvider>

<script setup lang="ts">
import { UIKitProvider } from '@tencentcloud/uikit-base-component-vue3';
```

### Customize Button and Icon

To add, remove, or replace buttons, icons, or other controls for UI customization, follow the example below. Use the screenshot to locate the relevant code in `live-player.vue` and update the UI as needed.

You can also customize the **audience viewer page** to match your project requirements. In addition to layout adjustments, you can **add, remove, or modify** elements such as **color theme, fonts, border radius, buttons, icons, input boxes, pop-ups**, and more.
| Category | Feature | Description |
| --- | --- | --- |
| Asset Management | Customize asset management area display | Adjust icon size, color, or replace icons. |
| Live Tools | Customize live tool information display | Adjust icon size, color, or replace icons. |
| Online Audience | Customize audience information display | Supports: - Show/hide audience level. - Customize audience info font and color. - Use your preferred icon style. |
| Message List | Customize live comments area display | Supports: - Show/hide chat input area. - Customize chat bubble style, audience level, and more. |

## FAQs

### Browser Autoplay Restrictions?

Modern browsers restrict autoplay for media with sound: playback must be triggered by explicit user interaction (such as a click or tap). This prevents websites from playing audio unexpectedly. Most browsers allow muted video to autoplay, but on iOS Safari in low power mode and in iOS WKWebView with custom restrictions (such as iOS WeChat browser), even muted video may be blocked.

#### Autoplay Failure Handling?

If a user's Media Engagement Index (MEI) for your site is below the required threshold, attempts to autoplay sound-enabled video will fail. By default, when the SDK detects autoplay failure, it displays a dialog prompting the user to interact with the page (for example, by clicking the **Confirm** button). Once the user interacts, audio playback resumes as expected.

#### Customizing Autoplay Failure UI?

To customize the user experience when autoplay fails (such as replacing the default popup), listen for the SDK's `onAutoplayFailed` callback. Below is a Vue3 sample that listens for the event and displays a custom dialog:
``` java
import TUIRoomEngine, { TUIRoomEvents } from '@tencentcloud/tuiroom-engine-js';
import { useUIKit, TUIMessageBox } from '@tencentcloud/uikit-base-component-vue3';
import { useRoomEngine } from 'tuikit-atomicx-vue3';

const roomEngine = useRoomEngine();

let isShowAutoPlayDialog = false;

export default function useCustomizedAutoPlayDialog() {
  const { t } = useUIKit();
  TUIRoomEngine.once('ready', () => {
    roomEngine.instance?.on(TUIRoomEvents.onAutoPlayFailed, () => {
      if (!isShowAutoPlayDialog) {
        isShowAutoPlayDialog = true;
        TUIMessageBox.alert({
          title: t('RoomCommon.Attention'),
          content: t('RoomNotifications.AudioPlaybackFailed'),
          showClose: false,
          modal: false,
          confirmText: t('Confirm'),
          callback: () => {
            isShowAutoPlayDialog = false;
          },
        });
      }
    });
  });
}

export { useCustomizedAutoPlayDialog };
```

> **Note：**
> 

> Make sure to install the required `@tencentcloud/tuiroom-engine-js` package.
> 

## Next Steps

You’ve now integrated the audience viewing feature. To further enhance your application, consider adding the following features:
| Feature | Description | Integration Guide |
| --- | --- | --- |
| Live Stream List | Displays the live stream list interface and features, including live stream list and room information display. | Live Stream List |
| Web Monitoring | Operations platform for live room management. | Web Monitoring Page |

---

This guide provides a comprehensive overview of the **Viewer Page** in the TUILiveKit Demo. Use this documentation to quickly integrate our pre-built viewer page into your project, or leverage the details here to fully customize its style, layout, and features to fit your specific needs.

## Feature Overview

The viewer page comes with default functionality and styling out of the box. If these defaults don’t match your requirements, you can easily tailor the UI. The numbers in the screenshot map to the main feature categories. Core features include: **stream information display, live video area, online audience, audio/video controls, live duration, resolution switching, fullscreen mode, chat interaction, and message list**.
- **Live Video Playback**: High-definition, low-latency streaming.

- **Live Comments Interaction**: Real-time live comments for audience engagement.

- **Audience List**: View details about online audience members.

- **Fullscreen Playback**: Immersive viewing experience.

- **H5 Mobile Platform Support**: Works seamlessly across platforms.

   

## Quick Integration

### Step 1: Environment Setup and Activate the Service

Before you begin, see Preparation for instructions on integrating required components and implementing login.

### Step 2: Install Dependencies

Install the necessary packages using your preferred package manager:

【npm】
``` bash
npm install tuikit-atomicx-vue3 @tencentcloud/uikit-base-component-vue3 --save
```

【pnpm】
``` bash
pnpm add tuikit-atomicx-vue3 @tencentcloud/uikit-base-component-vue3
```

【yarn】
``` bash
yarn add tuikit-atomicx-vue3 @tencentcloud/uikit-base-component-vue3
```

### Step 3: Integrate Viewer Page

Create a `live-player.vue` file in your project. Copy and paste the following code to add the **viewer page**.

> **Note：**
> 

> You can use the code below directly, or refer to [Audience Viewing](https://github.com/Tencent-RTC/TUILiveKit/blob/main/Web/web-vite-vue3/src/TUILiveKit/component/LivePlayer/LivePlayerPC.vue) for the full source.
> 

``` typescript
<template>
  <UIKitProvider theme="dark">
    <div class="container">
      <!-- Live Core Area -->
      <section class="live">
        <header class="header">
          <IconArrowStrokeBack class="back-btn" size="20" />
          <Avatar :src="currentLive?.liveOwner.avatarUrl" :size="32" class="avatar" />
          <span class="user-name">{{ currentLive?.liveOwner.userName || currentLive?.liveOwner.userId }}</span>
        </header>
        <LiveCoreView class="player" />
      </section>

      <div class="sidebar">
        <!-- Online Audience List -->
        <section class="audience">
          <header class="section-header">
            <h3> Online Audience <span>({{ audienceList.length }})</span></h3>
          </header>
          <LiveAudienceList class="list" />
        </section>

        <!-- Message List & Input Box -->
        <section class="barrage">
          <header class="section-header">
            <h3>Message List</h3>
          </header>
          <BarrageList class="list" />
          <BarrageInput class="input" height="48px" />
        </section>
      </div>
    </div>
  </UIKitProvider>
</template>

<script setup lang="ts">
import { onMounted } from 'vue';
import { LiveAudienceList, BarrageList, BarrageInput, useLiveAudienceState, LiveCoreView, useLiveListState, Avatar, useLoginState } from 'tuikit-atomicx-vue3';
import { UIKitProvider, IconArrowStrokeBack } from '@tencentcloud/uikit-base-component-vue3';

const { audienceList } = useLiveAudienceState();
const { currentLive } = useLiveListState();
const { login, setSelfInfo } = useLoginState();

const liveId = 'live_xxxx'  // Enter the ID of the live stream you want to watch

async function initLogin() {
  try {
    await login({
      sdkAppId: 0,     // SDKAppID, refer to Step 1 for details
      userId: '',      // UserID, refer to Step 1 for details
      userSig: '',     // userSig, refer to Step 1 for details
    });
  } catch (error) {
    console.error('Login failed:', error);
  }
}

onMounted(async () => {
  await initLogin();
  await setSelfInfo({
    userName: 'Your Name/Nickname',    // Username
    avatarUrl: '',                     // Avatar URL
  });
  await joinLive({ liveId });
});

</script>

<style>html,body,#app{height:100%;width:100%;margin:0;padding:0;overflow:hidden}:global(body){font-size:15px;line-height:1.6;text-rendering:optimizeLegibility;}:global(*),:global(*::before),:global(*::after){box-sizing:border-box;margin:0;}.container{display:grid;grid-template-columns:1fr 320px;height:100%;width:100%;gap:16px;padding:16px;background:var(--bg-color-default);box-sizing:border-box;overflow:hidden;}.live{display:flex;flex-direction:column;background:var(--bg-color-operate);border-radius:12px;overflow:hidden;box-shadow:0 2px 8px var(--shadow-color);}.header{display:flex;align-items:center;gap:12px;padding:16px;border-bottom:1px solid var(--stroke-color-primary);}.back-btn{cursor:pointer;color:var(--text-color-tertiary);transition:color 0.2s;}.back-btn:hover{color:var(--text-color-link-hover);}.avatar{border:1px solid var(--uikit-color-white-7);}.user-name{color:var(--text-color-primary);font-weight:500;}.player{flex:1;background:var(--uikit-color-black-1);min-height:0;}.sidebar{display:flex;flex-direction:column;gap:16px;height:100%;overflow:hidden;}.audience{display:flex;flex-direction:column;background:var(--bg-color-operate);border-radius:12px;overflow:hidden;box-shadow:0 2px 8px var(--shadow-color);flex:1;min-height:0;}.barrage{display:flex;flex-direction:column;background:var(--bg-color-operate);border-radius:12px;overflow:hidden;box-shadow:0 2px 8px var(--shadow-color);flex:1;min-height:0;}.section-header{padding:16px;border-bottom:1px solid var(--stroke-color-primary);background:var(--bg-color-operate);}.section-header h3{margin:0;font-size:16px;font-weight:600;color:var(--text-color-primary);}.section-header span{font-weight:400;color:var(--text-color-secondary);font-size:14px;}.list{flex:1;min-height:0;overflow-y:auto;}.input{border-top:1px solid var(--stroke-color-primary);flex-shrink:0;height:48px;}@media (max-width:1200px){.container{grid-template-columns:1fr;grid-template-rows:60% 20% 20%;gap:12px;}.sidebar{gap:12px;}.audience,.barrage{min-height:200px;}}@media (max-width:768px){.container{padding:8px;gap:8px;grid-template-rows:50% 25% 25%;}.header,.section-header{padding:12px;}.sidebar{gap:8px;}}</style>
```

#### Core API Parameters

##### setSelfInfo

Configure user information.
| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| userName | String | Yes | User nickname, shown in the live room and chat area. |
| avatarUrl | String | No | URL of the user's avatar image. |

### Step 4: Start the Project

Open your terminal, navigate to your project directory, and run the following command to launch the project. You’ll then be able to view the live stream.

> **Note：**
> 

> After the command runs successfully, enter your local access URL in your browser (for example, `http://localhost:5173/live-player`; the port may vary based on your setup) to access the viewer page.
> 

``` bash
npm run dev
```

## Play Live Stream

### Step 1: Start a Live Stream
- **Method 1 (Recommended):**

   Use our [Online Hosting Website](https://web.sdk.qcloud.com/trtc/livekit/pusher/index.html) to start a live stream. After starting, copy the live stream room ID.

- **Method 2:**

   Integrate our Host Streaming (Web Desktop Browser) to start a live stream. After starting, copy the live stream room ID.
   

   > **Important Tip:****：**
   > 

   > Use different **userID** for hosting and viewing. If the same user ID logs in on multiple devices, the later login will force the earlier device offline (**kick offline**).
   > 

### Step 2: Watch the Live Stream

Refer to the sample code from Step 3 of Quick Integration. Enter the corresponding `liveId` to join the live room and view the stream.

### Step 3: Router Configuration

To enable navigation from the Live Stream List or homepage to the live room, configure Vue Router. In your project’s **src** directory, create a **router** folder and an **index.ts** file. Import and use the router in your main entry file (such as **main.ts** or **index.ts**). For reference, see the [GitHub code example](https://github.com/Tencent-RTC/TUILiveKit/blob/main/Web/web-vite-vue3/src/main.ts). If you need the Live Stream List feature, check the Live Stream List documentation.

> **Note：**
> 

> In the code below, `live-player.vue` refers to the sample file created in Step 3.
> 

``` typescript
// src/router/index.ts
import { createRouter, createWebHistory } from 'vue-router';

const routes = [
  {
    path: '/live-player',
    component: () => import('../live-player.vue'),
  },
  // To add the Live Stream List feature, include the following route. Update the path as needed for your project.
  // {
  //   path: '/live-list',
  //   component: () => import('../live-list.vue'),
  // },
];

const router = createRouter({
  history: createWebHistory(),
  routes,
});
export default router;

// src/main.ts
import { createApp } from 'vue';
import App from './App.vue';
import router from './router';

const app = createApp(App);
app.use(router);
app.mount('#app');
```

## Customization

### Theme and Language Configuration

You can change the default theme and language by setting parameters in `UIKitProvider` within `App.vue`.
| UIKitProvider Parameter | Options | Default Value |
| --- | --- | --- |
| theme | "light" | "dark" |
| language | "zh-CN" | "en-US" |

``` typescript
<UIKitProvider theme="light">
  <router-view />
</UIKitProvider>

<script setup lang="ts">
import { UIKitProvider } from '@tencentcloud/uikit-base-component-vue3';
```

### Button and Icon Customization

To add, remove, or replace buttons, icons, or other controls for UI customization, follow the example below. Use the screenshot to locate the relevant code in `live-player.vue` and update the UI as needed.

You can also customize the **audience viewer page** to match your project requirements. In addition to layout adjustments, you can **add, remove, or modify** elements such as **color theme, fonts, border radius, buttons, icons, input boxes, pop-ups**, and more.
| Category | Feature | Description |
| --- | --- | --- |
| Asset Management | Customize asset management area display | Adjust icon size, color, or replace icons. |
| Live Tools | Customize live tool information display | Adjust icon size, color, or replace icons. |
| Online Audience | Customize audience information display | Supports: - Show/hide audience level. - Customize audience info font and color. - Use your preferred icon style. |
| Message List | Customize live comments area display | Supports: - Show/hide chat input area. - Customize chat bubble style, audience level, and more. |

## FAQs

### Browser Autoplay Restrictions?

Modern browsers restrict autoplay for media with sound: playback must be triggered by explicit user interaction (such as a click or tap). This prevents websites from playing audio unexpectedly. Most browsers allow muted video to autoplay, but on iOS Safari in low power mode and in iOS WKWebView with custom restrictions (such as iOS WeChat browser), even muted video may be blocked.

#### Autoplay Failure Handling?

If a user's Media Engagement Index (MEI) for your site is below the required threshold, attempts to autoplay sound-enabled video will fail. By default, when the SDK detects autoplay failure, it displays a dialog prompting the user to interact with the page (for example, by clicking the **Confirm** button). Once the user interacts, audio playback resumes as expected.

#### Customizing Autoplay Failure UI?

To customize the user experience when autoplay fails (such as replacing the default popup), listen for the SDK's `onAutoplayFailed` callback. Below is a Vue3 sample that listens for the event and displays a custom dialog:
``` java
import TUIRoomEngine, { TUIRoomEvents } from '@tencentcloud/tuiroom-engine-js';
import { useUIKit, TUIMessageBox } from '@tencentcloud/uikit-base-component-vue3';
import { useRoomEngine } from 'tuikit-atomicx-vue3';

const roomEngine = useRoomEngine();

let isShowAutoPlayDialog = false;

export default function useCustomizedAutoPlayDialog() {
  const { t } = useUIKit();
  TUIRoomEngine.once('ready', () => {
    roomEngine.instance?.on(TUIRoomEvents.onAutoPlayFailed, () => {
      if (!isShowAutoPlayDialog) {
        isShowAutoPlayDialog = true;
        TUIMessageBox.alert({
          title: t('RoomCommon.Attention'),
          content: t('RoomNotifications.AudioPlaybackFailed'),
          showClose: false,
          modal: false,
          confirmText: t('Confirm'),
          callback: () => {
            isShowAutoPlayDialog = false;
          },
        });
      }
    });
  });
}

export { useCustomizedAutoPlayDialog };
```

> **Note：**
> 

> Make sure to install the required `@tencentcloud/tuiroom-engine-js` package.
> 

## Next Steps

You’ve now integrated the audience viewing feature. To further enhance your application, consider adding the following features:
| Feature | Description | Integration Guide |
| --- | --- | --- |
| Live Stream List | Displays the live stream list interface and features, including live stream list and room information display. | Live Stream List |
| Web Monitoring | Operations platform for live room management. | Web Monitoring Page |
