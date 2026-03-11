> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

This document guides developers through building a voice chat room application with host broadcasting and audience participation features using the **AtomicXCore** SDK's `LiveListStore` and `LiveSeatStore`.

## Core Concepts
<table>
<tr>
<td rowspan="1" colSpan="1" >**Core Concept**</td>

<td rowspan="1" colSpan="1" >**Type**</td>

<td rowspan="1" colSpan="1" >**Core Responsibilities & Description**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`LiveListStore`</td>

<td rowspan="1" colSpan="1" >`abstract class`</td>

<td rowspan="1" colSpan="1" >- `createLive()`: Start live stream as host.<br>- `endLive()`: End live stream as host.<br>- `joinLive()`: Audience joins live room.<br>- `leaveLive()`: Leave live room.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`LiveInfo`</td>

<td rowspan="1" colSpan="1" >`data class`</td>

<td rowspan="1" colSpan="1" >- `liveID`: Unique room identifier.<br>- `seatLayoutTemplateID`: Layout template ID (e.g., 600 for dynamic grid).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`LiveSeatStore`</td>

<td rowspan="1" colSpan="1" >`abstract class`</td>

<td rowspan="1" colSpan="1" >Core seat management class. Manages all seat information and seat-related operations in the room.<br>Provides a real-time seat list data stream via liveSeatState.seatList.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`LiveSeatState`</td>

<td rowspan="1" colSpan="1" >`data class`</td>

<td rowspan="1" colSpan="1" >Represents the current state of all seats.<br>- `seatList`: a StateFlow containing the real-time seat list.<br>- `speakingUsers`: users currently speaking and their volume.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`SeatInfo`</td>

<td rowspan="1" colSpan="1" >`data class`</td>

<td rowspan="1" colSpan="1" >Data model for a single seat. The seat list (seatList) emitted by LiveSeatStore is a list of SeatInfo objects.<br>Key fields:<br>- `index`: seat position.<br>- `isLocked`: whether the seat is locked.<br>- `userInfo`: user information for the seat. If the seat is empty, this field is empty.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`SeatUserInfo`</td>

<td rowspan="1" colSpan="1" >`data class`</td>

<td rowspan="1" colSpan="1" >Detailed data model for the user occupying a seat. When a user successfully takes a seat, the userInfo field in SeatInfo is populated.<br>Key fields:<br>- `userID`: unique user ID.<br>- `userName`: user nickname.<br>- `avatarURL`: user avatar URL.<br>- `microphoneStatus`: microphone status (on/off).<br>- `cameraStatus`: camera status (on/off).</td>
</tr>
</table>


## Prerequisites

### Step 1: Activate the Service

See [Activate Service](https://write.woa.com/document/141936672617742336) to obtain either the trial or paid version of the SDK.Then, go to [the Console](https://console.trtc.io/app) for application management, and get the following:
- `SDKAppID`: Application identifier (required). Tencent Cloud uses `SDKAppId` for billing and details.

- `SDKSecretKey`: Application secret key, used to initialize the configuration file with secret information.

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027182498/018c103bc9f411f09e745254007c27c5.png)


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

Call `LoginStore.shared.login` in your project to complete authentication. **This is required before using any functionality of AtomicXCore**.

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
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`sdkAppID`</td>

<td rowspan="1" colSpan="1" >`Int`</td>

<td rowspan="1" colSpan="1" >Get this from [TRTC console > Application management](https://console.trtc.io/app).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`userID`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >The unique ID for the current user. Must contain only English letters, numbers, hyphens, and underscores.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`userSig`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >A ticket for Tencent Cloud authentication. Please note:<br>- **Development Environment**: You can use the local `GenerateTestUserSig.genTestSig` function to generate a UserSig or generate a temporary UserSig via the [UserSig Generation Tool](https://console.trtc.io/usersig).<br>- **Production Environment**: To prevent key leakage, you must use a server-side method to generate UserSig. For details, see [Generating UserSig on the Server](https://write.woa.com/document/89644530319802368).<br>- For more information, see [How to Calculate and Use UserSig](https://write.woa.com/document/89644530319802368).</td>
</tr>
</table>


## Building a Basic Voice Chat Room

### Step 1: Host Room Creation

Follow the steps below to quickly set up a voice chat room as the host.

#### **1. Initialize the Seat **`Store`

In your host `Activity`, create a `LiveSeatStore` instance. Observe changes in `liveSeatState.seatList` to get real-time mic seat data and update your UI.
``` java
import android.os.Bundle
import android.util.Log
import androidx.appcompat.app.AppCompatActivity
import io.trtc.tuikit.atomicxcore.api.device.DeviceStore
import io.trtc.tuikit.atomicxcore.api.live.LiveListStore
import io.trtc.tuikit.atomicxcore.api.live.LiveSeatStore
import kotlinx.coroutines.CoroutineScope
import kotlinx.coroutines.Dispatchers
import kotlinx.coroutines.launch

// YourHostActivity represents your Host Activity
class YourHostActivity : AppCompatActivity() {

    private lateinit var liveListStore: LiveListStore
    private lateinit var liveSeatStore: LiveSeatStore
    private lateinit var deviceStore: DeviceStore
    private val liveID = "test_voice_room_001"

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_host) // Assume you have your own layout

        // 1. Initialize Stores
        liveListStore = LiveListStore.shared()
        liveSeatStore = LiveSeatStore.create(liveID)
        deviceStore = DeviceStore.shared()

        // 2. Listen for mic seat list changes
        observeSeatList()
    }

    private fun observeSeatList() {
         // Listen for seatList changes and update your mic seat UI
         CoroutineScope(Dispatchers.Main).launch {
             liveSeatStore.liveSeatState.seatList.collect { seatInfoList ->
                 // Render your mic seat UI here based on seatInfoList
                 // Example: updateMicSeatView(seatInfoList)
                 Log.d("HostActivity", "Seat list updated: ${seatInfoList.size} seats")
             }
         }
    }
}
```

#### **2. **Turn On Microphone

Turn On Microphone by calling the `openLocalMicrophone` method from `DeviceStore`:
``` java
import androidx.appcompat.app.AppCompatActivity
import io.trtc.tuikit.atomicxcore.api.device.DeviceStore

class YourHostActivity : AppCompatActivity() {
    // ... Other code ...

    private fun openDevices() {
        // 1. Turn on the microphone
        DeviceStore.shared().openLocalMicrophone(completion = null)
    }
}
```

#### **3. Start Voice Chat**

Start the live voice chat by calling the `createLive` method of `LiveListStore`:
``` java
import android.os.Bundle
import android.util.Log
import androidx.appcompat.app.AppCompatActivity
import io.trtc.tuikit.atomicxcore.api.live.LiveInfo
import io.trtc.tuikit.atomicxcore.api.live.LiveInfoCompletionHandler
import io.trtc.tuikit.atomicxcore.api.live.TakeSeatMode

class YourHostActivity : AppCompatActivity() {
    // ... Other code ...

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        // ... Other code ...

        // Start voice chat
        startLive()
    }

    private fun startLive() {
        val liveInfo = LiveInfo().apply {
            // 1. Set room id
            liveID = this@YourHostActivity.liveID
            // 2. Set room name
            liveName = "test voice room"
            // 3. Configure as a voice chat room (enable mic seats)
            isSeatEnabled = true
            // 4. Host takes mic by default
            keepOwnerOnSeat = true
            // 5. Set mic seat layout template (e.g., 70 for a 10-seat template)
            seatLayoutTemplateID = 70
            // 6. Set mic-taking mode, e.g., apply to take mic
            seatMode = TakeSeatMode.APPLY
            // 7. Set maximum number of mic seats
            maxSeatCount = 10
        }

        // 8. Call createLive to start the stream
        liveListStore.createLive(liveInfo, object : LiveInfoCompletionHandler {
            override fun onFailure(code: Int, desc: String) {
                Log.e("Live", "Response startLive onError: $desc")
            }

            override fun onSuccess(liveInfo: LiveInfo) {
                Log.d("Live", "Response startLive onSuccess")
                // After successful creation, the Host is on the mic by default, now you can call unmuteMicrophone
                liveSeatStore.unmuteMicrophone(null)
            }
        })
    }
}
```

**LiveInfo Parameter Description**
<table>
<tr>
<td rowspan="1" colSpan="1" >**Parameter Name**</td>

<td rowspan="1" colSpan="1" >**Type**</td>

<td rowspan="1" colSpan="1" >**Required**</td>

<td rowspan="1" colSpan="1" >**Description**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`liveID`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >Required</td>

<td rowspan="1" colSpan="1" >Unique identifier for the live room</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`liveName`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >Optional</td>

<td rowspan="1" colSpan="1" >Title of the live room</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`notice`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >Optional</td>

<td rowspan="1" colSpan="1" >Announcement information for the live room</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`isMessageDisable`</td>

<td rowspan="1" colSpan="1" >`Boolean`</td>

<td rowspan="1" colSpan="1" >Optional</td>

<td rowspan="1" colSpan="1" >Mute status (`true`: muted, `false`: not muted)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`isPublicVisible`</td>

<td rowspan="1" colSpan="1" >`Boolean`</td>

<td rowspan="1" colSpan="1" >Optional</td>

<td rowspan="1" colSpan="1" >Public visibility (`true`: visible, `false`: hidden)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`isSeatEnabled`</td>

<td rowspan="1" colSpan="1" >`Boolean`</td>

<td rowspan="1" colSpan="1" >Optional</td>

<td rowspan="1" colSpan="1" >Enable mic seat feature (`true`: enabled, `false`: disabled)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`keepOwnerOnSeat`</td>

<td rowspan="1" colSpan="1" >`Boolean`</td>

<td rowspan="1" colSpan="1" >Optional</td>

<td rowspan="1" colSpan="1" >Keep host on mic seat</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`maxSeatCount`</td>

<td rowspan="1" colSpan="1" >`Int`</td>

<td rowspan="1" colSpan="1" >Required</td>

<td rowspan="1" colSpan="1" >Maximum number of mic seats</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`seatMode`</td>

<td rowspan="1" colSpan="1" >[TakeSeatMode](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-take-seat-mode/index.html)</td>

<td rowspan="1" colSpan="1" >Optional</td>

<td rowspan="1" colSpan="1" >Mic seat mode (`FREE`: free to take seat, `APPLY`: apply to take seat)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`seatLayoutTemplateID`</td>

<td rowspan="1" colSpan="1" >`Int`</td>

<td rowspan="1" colSpan="1" >Required</td>

<td rowspan="1" colSpan="1" >Mic seat layout template ID</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`coverURL`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >Optional</td>

<td rowspan="1" colSpan="1" >Cover image URL for the live room</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`backgroundURL`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >Optional</td>

<td rowspan="1" colSpan="1" >Background image URL for the live room</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`categoryList`</td>

<td rowspan="1" colSpan="1" >`List<Int>`</td>

<td rowspan="1" colSpan="1" >Optional</td>

<td rowspan="1" colSpan="1" >Category tag list for the live room</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`activityStatus`</td>

<td rowspan="1" colSpan="1" >`Int`</td>

<td rowspan="1" colSpan="1" >Optional</td>

<td rowspan="1" colSpan="1" >Live activity status</td>
</tr>
</table>


#### **4. Build the Mic Seat UI**

> **Note：**
> 

> For the complete business logic of mic seat UI effects, refer to the open-source [SeatGridView.kt](https://github.com/Tencent-RTC/TUILiveKit/blob/main/Android/tuilivekit/src/main/java/com/trtc/uikit/livekit/voiceroomcore/SeatGridView.kt) in the TUILiveKit project.
> 


Use the `LiveSeatStore` instance to observe changes in `liveSeatState.seatList` and update your UI in real time. In your Activity (such as `YourAnchorActivity` or `YourAudienceActivity`), observe the data as follows:
``` java
import android.os.Bundle
import android.util.Log
import androidx.appcompat.app.AppCompatActivity
import kotlinx.coroutines.CoroutineScope
import kotlinx.coroutines.Dispatchers
import kotlinx.coroutines.launch

class YourHostActivity : AppCompatActivity() {
    // ... Other code ...

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        // ... Other code ...

        // Listen for seatList changes
        observeSeatList()
    }

    private fun observeSeatList() {
        // Listen for seatList changes and update your mic seat UI
        CoroutineScope(Dispatchers.Main).launch {
            liveSeatStore.liveSeatState.seatList.collect { seatInfoList ->
                // seatInfoList is the latest mic seat list (List<SeatInfo>), render your mic seat UI here based on seatInfoList
                Log.d("HostActivity", "Seat list updated: ${seatInfoList.size} seats")
            }
        }
    }
}
```

#### **5. End Voice Chat**

To end the voice chat, call the `endLive` method of `LiveListStore`. The SDK will handle stopping the stream and destroying the room.
``` java
import android.util.Log
import androidx.appcompat.app.AppCompatActivity
import com.tencent.cloud.tuikit.engine.extension.TUILiveListManager
import io.trtc.tuikit.atomicxcore.api.live.StopLiveCompletionHandler

class YourHostActivity : AppCompatActivity() {
    // ... Other code ...

    // End voice chat
    private fun stopLive() {
        liveListStore.endLive(object : StopLiveCompletionHandler {
            override fun onSuccess(statisticsData: TUILiveListManager.LiveStatisticsData) {
                Log.d("Live", "endLive success, duration: ${statisticsData.liveDuration}")
            }

            override fun onFailure(code: Int, desc: String) {
                Log.e("Live", "endLive error: $desc")
            }
        })
    }

    // Ensure this is also called when the Activity is destroyed
    override fun onDestroy() {
        super.onDestroy()
        stopLive()
        Log.d("Live", "YourHostActivity onDestroy")
    }
}
```

### Step 2: Audience Joins the Voice Chat Room

Follow these steps to allow audience members to join the voice chat room.

#### **1. Initialize the Mic Seat Store**

In your audience `Activity`, create a `LiveSeatStore` instance and observe changes in `liveSeatState.seatList` to update the mic seat UI.
``` java
import io.trtc.tuikit.atomicxcore.api.live.LiveListStore
import io.trtc.tuikit.atomicxcore.api.live.LiveSeatStore
import android.os.Bundle
import androidx.appcompat.app.AppCompatActivity
import kotlinx.coroutines.CoroutineScope
import kotlinx.coroutines.Dispatchers
import kotlinx.coroutines.launch
import android.util.Log

// YourAudienceActivity represents your Audience Activity
class YourAudienceActivity : AppCompatActivity() {

    private lateinit var liveListStore: LiveListStore
    private lateinit var liveSeatStore: LiveSeatStore
    private val liveID = "test_voice_room_001" // Ensure liveID matches the Host's

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_audience) // Assume you have your own layout

        // 1. Initialize Stores
        liveListStore = LiveListStore.shared()
        liveSeatStore = LiveSeatStore.create(liveID)

        // 2. Listen for mic seat list changes
        observeSeatList()
    }

    private fun observeSeatList() {
         // 3. Listen for seatList changes and update your mic seat UI
         CoroutineScope(Dispatchers.Main).launch {
             liveSeatStore.liveSeatState.seatList.collect { seatInfoList ->
                 // Render your mic seat UI here based on seatInfoList
                 // Example: updateMicSeatView(seatInfoList)
                 Log.d("AudienceActivity", "Seat list updated: ${seatInfoList.size} seats")
             }
         }
    }
}
```

#### **2. Join Voice Chat Room**

Join the voice chat room by calling the `joinLive` method of `LiveListStore`:
``` java
import android.os.Bundle
import androidx.appcompat.app.AppCompatActivity
import android.util.Log
import io.trtc.tuikit.atomicxcore.api.live.LiveInfo
import io.trtc.tuikit.atomicxcore.api.live.LiveInfoCompletionHandler

// YourAudienceActivity represents your Audience Activity
class YourAudienceActivity : AppCompatActivity() {
    
    // ... Other code ...
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_audience) // Assume you have your own layout
        // ... Other code ...
        
        // Enter voice chat room
        joinLive()
    }

    private fun joinLive() {
        // 1. Call joinLive to enter the voice chat room
        liveListStore.joinLive(liveID, object : LiveInfoCompletionHandler {
            override fun onSuccess(liveInfo: LiveInfo) {
                Log.d("Live", "joinLive success")
            }
            override fun onFailure(code: Int, desc: String) {
                Log.e("Live", "joinLive error: $desc")
            }
        })
    }
}
```

#### **3. Build the Mic Seat UI**

The process for building the mic seat UI as an audience member is the same as for the host. Refer to the host [Build the Mic Seat UI](https://write.woa.com/#9a917c47-816f-4930-81b1-d35ee01c519d).

#### **4. Leave the Voice Chat Room**

When an audience member leaves the voice chat room, call the `leaveLive` method of `LiveListStore`:
``` java
import android.util.Log
import androidx.appcompat.app.AppCompatActivity
import io.trtc.tuikit.atomicxcore.api.CompletionHandler

// YourAudienceActivity represents your Audience Activity
class YourAudienceActivity : AppCompatActivity() {
    // ... Other code ...

    private fun leaveLive() {
        liveListStore.leaveLive(object : CompletionHandler {
            override fun onSuccess() {
                Log.d("Live", "leaveLive success")
            }

            override fun onFailure(code: Int, desc: String) {
                Log.e("Live", "leaveLive error: $desc")
            }
        })
    }

    // Ensure this is also called when the Activity is destroyed
    override fun onDestroy() {
        super.onDestroy()
        leaveLive()
        Log.d("Live", "YourAudienceActivity onDestroy")
    }
}
```

### Run and Test

After completing the steps above, you will have a basic voice chat live streaming setup. For more advanced features, see the "Enrich Voice Chat Room Scenarios" section.

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027182498/159d41cdc9f411f0b011525400bf7822.png)

## Advanced Features

### **Implementing Speaking Wave Animation for Mic Seat Users**

In voice chat rooms, it is common to show a wave animation on the avatar of users who are speaking, so everyone can see who is currently talking. `LiveSeatStore` provides a `speakingUsers` data stream for this purpose.

#### Example

#### ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027182498/159f07ffc9f411f09e745254007c27c5.gif)

#### Implementation

> **Note：**
> 

> For a complete implementation of the speaking wave animation, refer to [SeatGridView.kt](https://github.com/Tencent-RTC/TUILiveKit/blob/main/Android/tuilivekit/src/main/java/com/trtc/uikit/livekit/voiceroomcore/SeatGridView.kt) in the open-source TUILiveKit project.
> 


In `YourAnchorActivity`, observe changes in `speakingUsers` and update the UI to reflect the speaking status:
``` java
import android.os.Bundle
import android.util.Log
import androidx.appcompat.app.AppCompatActivity
import kotlinx.coroutines.CoroutineScope
import kotlinx.coroutines.Dispatchers
import kotlinx.coroutines.launch

// In YourHostActivity or YourAudienceActivity
class YourHostActivity : AppCompatActivity() {
    // ... (omitting other code) ...

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        // ... (omitting other code) ...

        // Listen for speakingUsers changes
        observeSpeakingUsersState()
    }

    private fun observeSpeakingUsersState() {
        // Listen for speakingUsers changes and update the "currently speaking" status
        CoroutineScope(Dispatchers.Main).launch {
            liveSeatStore.liveSeatState.speakingUsers.collect { speakingUserSet ->
                // Pass the set of "currently speaking" user IDs to the UI, update UI state
                Log.d("HostActivity", "Speaking users updated: ${speakingUserSet.size} users")
            }
        }
    }
}
```

### Synchronizing Custom State in Live Streaming Room

In Live Streaming Room, hosts may need to synchronize custom information with all participants, such as the current room topic or background music. The `metaData` feature of `LiveListStore` supports this use case.

#### Implementation
1. On the host side, set custom information using the `updateLiveMetaData` API. `AtomicXCore` synchronizes these changes in real time to all participants. 

2. On the audience side, subscribe to `LiveListState.currentLive` and listen for changes in `metaData`. When a relevant key is updated, parse its value and update your business logic.


#### Code Example
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

## Enrich Voice Chat Room Scenarios

After implementing the basic voice chat room, you can add more interactive features by referring to the following guides:
<table>
<tr>
<td rowspan="1" colSpan="1" >**Feature**</td>

<td rowspan="1" colSpan="1" >**Feature Description**</td>

<td rowspan="1" colSpan="1" >**Feature Stores**</td>

<td rowspan="1" colSpan="1" >**Implementation Guide**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**Enable Audience to Take Mic Seat**</td>

<td rowspan="1" colSpan="1" >Audience can apply to take a mic seat and interact with the host in real time.</td>

<td rowspan="1" colSpan="1" >[CoGuestStore](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-co-guest-store/index.html)</td>

<td rowspan="1" colSpan="1" >[Implementation](https://write.woa.com/document/194571595728519168)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**Host Cross-Room Connection & PK**</td>

<td rowspan="1" colSpan="1" >Hosts from different rooms can connect for interaction or PK.</td>

<td rowspan="1" colSpan="1" >[CoHostStore](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-co-host-store/index.html)<br>[BattleStore](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-battle-store/index.html)</td>

<td rowspan="1" colSpan="1" >[Implementation](https://write.woa.com/document/194571595874271232)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**Add Barrage Chat**</td>

<td rowspan="1" colSpan="1" >Members in the room can send and receive real-time text messages.</td>

<td rowspan="1" colSpan="1" >[BarrageStore](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.barrage/-barrage-store/index.html)</td>

<td rowspan="1" colSpan="1" >[Implementation](https://write.woa.com/document/195218523636584448)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**Build Gift System**</td>

<td rowspan="1" colSpan="1" >Audience can send virtual gifts to hosts to increase engagement and fun.</td>

<td rowspan="1" colSpan="1" >[GiftStore](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.gift/-gift-store/index.html)</td>

<td rowspan="1" colSpan="1" >[Implementation](https://write.woa.com/document/195218406705512448)</td>
</tr>
</table>


## API Documentation
<table>
<tr>
<td rowspan="1" colSpan="1" >**Store/Component**</td>

<td rowspan="1" colSpan="1" >**Feature Description**</td>

<td rowspan="1" colSpan="1" >**API Documentation**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`LiveListStore`</td>

<td rowspan="1" colSpan="1" >Manages the full lifecycle of live rooms: create, join, leave, destroy rooms; query room list; modify live info (name, announcement, etc.); listen to live status (such as being kicked out, ended).</td>

<td rowspan="1" colSpan="1" >[API Documentation](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-live-list-store/index.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`LiveSeatStore`</td>

<td rowspan="1" colSpan="1" >Core mic seat management: manage mic seat list, user status, seat operations (take seat, leave seat, kick, lock, toggle microphone/camera, etc.), listen to mic seat events.</td>

<td rowspan="1" colSpan="1" >[API Documentation](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-live-seat-store/index.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`DeviceStore`</td>

<td rowspan="1" colSpan="1" >Audio/video device control: microphone (toggle/volume), camera (toggle/switch/quality), screen sharing, real-time device status monitoring.</td>

<td rowspan="1" colSpan="1" >[API Documentation](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.device/-device-store/index.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`CoGuestStore`</td>

<td rowspan="1" colSpan="1" >Audience co-host management: co-host application/invitation/approval/rejection, member permission control (microphone/camera), status synchronization.</td>

<td rowspan="1" colSpan="1" >[API Documentation](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-co-guest-store/index.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`CoHostStore`</td>

<td rowspan="1" colSpan="1" >Host cross-room connection: supports multiple layout templates (dynamic grid, etc.), initiate/accept/reject connection, manage co-host interaction.</td>

<td rowspan="1" colSpan="1" >[API Documentation](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-co-host-store/index.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`BattleStore`</td>

<td rowspan="1" colSpan="1" >Host PK battle: initiate PK (set duration/opponent), manage PK status (start/end), synchronize scores, listen to battle results.</td>

<td rowspan="1" colSpan="1" >[API Documentation](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-battle-store/index.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`GiftStore`</td>

<td rowspan="1" colSpan="1" >Gift interaction: get gift list, send/receive gifts, listen to gift events (including sender and gift details).</td>

<td rowspan="1" colSpan="1" >[API Documentation](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.gift/-gift-store/index.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`BarrageStore`</td>

<td rowspan="1" colSpan="1" >Bullet chat feature: send text/custom barrage, maintain barrage list, real-time barrage status monitoring.</td>

<td rowspan="1" colSpan="1" >[API Documentation](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.barrage/-barrage-store/index.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`LikeStore`</td>

<td rowspan="1" colSpan="1" >Like interaction: send likes, listen to like events, synchronize total like count.</td>

<td rowspan="1" colSpan="1" >[API Documentation](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-like-store/index.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`LiveAudienceStore`</td>

<td rowspan="1" colSpan="1" >Audience management: get real-time audience list (ID/name/avatar), count audience number, listen to audience join/leave events.</td>

<td rowspan="1" colSpan="1" >[API Documentation](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.live/-live-audience-store/index.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`AudioEffectStore`</td>

<td rowspan="1" colSpan="1" >Audio effects: voice changer (child/male), reverb (KTV, etc.), ear monitor adjustment, real-time effect switching.</td>

<td rowspan="1" colSpan="1" >[API Documentation](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.device/-audio-effect-store/index.html)</td>
</tr>
</table>


## FAQs

### Why is there no sound after the audience calls joinLive?
- **Check device permissions:** Ensure the app has system permission to use the microphone.

- **Check the host:** Confirm the host has called `DeviceStore.shared().openLocalMicrophone(null)` to enable the microphone.

- **Check the network:** Ensure the device's network connection is stable.


### Why is the mic seat list not displayed or not updating?
- **Check store initialization:** Make sure you have created the `LiveSeatStore` instance with the same `liveID` before calling `createLive` or `joinLive` (`LiveSeatStore.create(liveID)`).

- **Check data observation:** Ensure you are observing the `liveSeatStore.liveSeatState.seatList` data stream.

- **Check API calls:** Confirm that `createLive` (host) or `joinLive` (audience) was successfully called (check the `onSuccess` callback).åå


