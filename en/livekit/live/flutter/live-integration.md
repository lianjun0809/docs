> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/en/llms.txt
> Use this file to discover all available pages before exploring further.

This documentation guides you through using the core component of the AtomicXCore SDK, [LiveCoreWidget](https://tencent-rtc.github.io/TUIKit_Flutter/api_view_live_live_core_widget/api_view_live_live_core_widget-library.html), to quickly build a basic live streaming app with host broadcasting and audience viewing functionality.

## Core Features

**LiveCoreWidget** is a lightweight widget purpose-built for live streaming scenarios and serves as the foundation of your live streaming interface. It abstracts complex live streaming technologies—including streaming, co-hosting, and audio/video rendering—so you can use LiveCoreWidget as the canvas for your live video. This allows you to focus on developing your custom UI and interactive features.

The following diagram illustrates where **LiveCoreWidget** fits within your live streaming interface and its role in the view hierarchy:

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032457995/989ce871f6d411f09fbf525400370dda.png)


## Preparations

### Step 1: Activate the Service

See [Activate Service](https://write.woa.com/document/141936672617742336) to obtain either the trial or paid version of the SDK.Then, go to [the Console](https://console.trtc.io/app) for application management, and get the following:
- `SDKAppID`: Application identifier (required). Tencent Cloud uses `SDKAppID` for billing and details.

- `SDKSecretKey`: Application secret key, used to initialize the configuration file with secret information.

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032457995/bb11696df6d411f09d0352540097cba1.png)


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

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032457995/548e6c77f82711f093ec525400074c32.png)



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
<table>
<tr>
<td rowspan="1" colSpan="1" >**Parameter**</td>

<td rowspan="1" colSpan="1" >**Type**</td>

<td rowspan="1" colSpan="1" >**Note**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`sdkAppID`</td>

<td rowspan="1" colSpan="1" >`int`</td>

<td rowspan="1" colSpan="1" >Get this from [TRTC console](https://console.trtc.io/app).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`userID`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >The unique ID for the current user. Must contain only English letters, numbers, hyphens, and underscores.. To avoid multi-end login conflict, **do not use**`1`, `123`**or other simple IDs**.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`userSig`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >A ticket for Tencent Cloud authentication. Please note:<br>- Development Environment: You can use the local `GenerateTestUserSig.genTestSig` function to generate a `UserSig` or generate a temporary UserSig via the [UserSig Generation Tool](https://console.trtc.io/usersig).<br>- Production Environment: To prevent key leakage, you must use a server-side method to generate `UserSig`. For details, see [Generating UserSig on the Server](https://write.woa.com/document/89644530319802368).</td>
</tr>
</table>


## Building a Basic Live Room

### Step 1: Implement Broadcaster Video Streaming

The anchor starts live streaming process is as follows. You just need to perform the following steps to quickly build a live stream.

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032457995/332cea8bf6d711f09fbf525400370dda.png)


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

<table>
<tr>
<td rowspan="1" colSpan="1" >**Parameter Name**</td>

<td rowspan="1" colSpan="1" >**Type**</td>

<td rowspan="1" colSpan="1" >**Attribute**</td>

<td rowspan="1" colSpan="1" >**Description**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`liveID`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >Required</td>

<td rowspan="1" colSpan="1" >Unique identifier for the live streaming room.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`liveName`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >Optional.</td>

<td rowspan="1" colSpan="1" >Title of the live streaming room.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`notice`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >Optional.</td>

<td rowspan="1" colSpan="1" >Announcement information of the live streaming room.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`isMessageDisable`</td>

<td rowspan="1" colSpan="1" >`bool`</td>

<td rowspan="1" colSpan="1" >Optional.</td>

<td rowspan="1" colSpan="1" >Whether to mute (`true`: yes, `false`: no).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`isPublicVisible`</td>

<td rowspan="1" colSpan="1" >`bool`</td>

<td rowspan="1" colSpan="1" >Optional.</td>

<td rowspan="1" colSpan="1" >Whether publicly visible (`true`: yes, `false`: no).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`isSeatEnabled`</td>

<td rowspan="1" colSpan="1" >`bool`</td>

<td rowspan="1" colSpan="1" >Optional.</td>

<td rowspan="1" colSpan="1" >Whether to enable the seat feature (`true`: yes, `false`: no).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`keepOwnerOnSeat`</td>

<td rowspan="1" colSpan="1" >`bool`</td>

<td rowspan="1" colSpan="1" >Optional.</td>

<td rowspan="1" colSpan="1" >Whether to keep the room owner on the seat.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`maxSeatCount`</td>

<td rowspan="1" colSpan="1" >`int`</td>

<td rowspan="1" colSpan="1" >Optional.</td>

<td rowspan="1" colSpan="1" >Maximum number of microphones.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`seatMode`</td>

<td rowspan="1" colSpan="1" >`TakeSeatMode`</td>

<td rowspan="1" colSpan="1" >Optional.</td>

<td rowspan="1" colSpan="1" >Microphone mode (`TakeSeatMode.free`: Free to Join the Podium, `TakeSeatMode.apply`: Request to speak).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`seatLayoutTemplateID`</td>

<td rowspan="1" colSpan="1" >`int`</td>

<td rowspan="1" colSpan="1" >Required</td>

<td rowspan="1" colSpan="1" >layout template ID.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`coverURL`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >Optional.</td>

<td rowspan="1" colSpan="1" >Thumbnail URL of the live streaming room.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`backgroundURL`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >Optional.</td>

<td rowspan="1" colSpan="1" >Background image URL of the live streaming room.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`categoryList`</td>

<td rowspan="1" colSpan="1" >`List<int>`</td>

<td rowspan="1" colSpan="1" >Optional.</td>

<td rowspan="1" colSpan="1" >Tag list of categories in the live streaming room.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`activityStatus`</td>

<td rowspan="1" colSpan="1" >`int`</td>

<td rowspan="1" colSpan="1" >Optional.</td>

<td rowspan="1" colSpan="1" >Live stream status.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`isGiftEnabled`</td>

<td rowspan="1" colSpan="1" >`bool`</td>

<td rowspan="1" colSpan="1" >Optional.</td>

<td rowspan="1" colSpan="1" >Whether to enable the gift function (`true`: yes, `false`: no).</td>
</tr>
</table>

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

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032457995/92e9b016f6d711f0b34b525400ecee81.png)


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

After integrating `LiveCoreWidget`, you will obtain a pure video rendering view with complete live streaming business capability but no interactive UI. You can refer to the next chapter [Enrich Live-Streaming Scenarios](https://write.woa.com/#.E4.B8.B0.E5.AF.8C.E7.9B.B4.E6.92.AD.E5.9C.BA.E6.99.AF) to refine live broadcasting scenarios.
<table>
<tr>
<td rowspan="1" colSpan="1" ></td>

<td rowspan="1" colSpan="1" >**Dynamic Grid Layout**</td>

<td rowspan="1" colSpan="1" >**Floating Window Layout**</td>

<td rowspan="1" colSpan="1" >**Fixed Grid Layout**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Template ID</td>

<td rowspan="1" colSpan="1" >600</td>

<td rowspan="1" colSpan="1" >601</td>

<td rowspan="1" colSpan="1" >800</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Description</td>

<td rowspan="1" colSpan="1" >Default layout; grid size adjusts dynamically based on number of co-hosts.</td>

<td rowspan="1" colSpan="1" >Co-hosts are displayed as floating windows.</td>

<td rowspan="1" colSpan="1" >Fixed number of co-hosts; each occupies a fixed grid.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Example</td>

<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100043650599/6a730a2ecc0d11f084a45254005ef0f7.png)</td>

<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100043650599/71c322e9cc0d11f084a45254005ef0f7.png)</td>

<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100043650599/a1855792cc0d11f0ae4f52540099c741.png)</td>
</tr>
</table>


## Enrich Live Streaming Scenarios

Once the basic live streaming functionality is in place, refer to the following guides to add interactive features to your live stream:
<table>
<tr>
<td rowspan="1" colSpan="1" >**Feature**</td>

<td rowspan="1" colSpan="1" >**Description**</td>

<td rowspan="1" colSpan="1" >**Store**</td>

<td rowspan="1" colSpan="1" >**Implementation Guide**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**Enable Audience Audio/Video Co-hosting**</td>

<td rowspan="1" colSpan="1" >Audience can apply to join the host and interact via real-time video.</td>

<td rowspan="1" colSpan="1" >[CoGuestStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_co_guest_store/CoGuestStore-class.html)</td>

<td rowspan="1" colSpan="1" >[Implementation Guide](https://write.woa.com/document/200455653984186368)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**Enable Host Cross-room PK**</td>

<td rowspan="1" colSpan="1" >Hosts from different rooms can connect for interaction or PK.</td>

<td rowspan="1" colSpan="1" >[CoHostStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_co_host_store/CoHostStore-class.html) / [BattleStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_battle_store/BattleStore-class.html)</td>

<td rowspan="1" colSpan="1" >[Implementation Guide](https://write.woa.com/document/200455659512819712)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**Add Bullet Chat Feature**</td>

<td rowspan="1" colSpan="1" >Audience can send and receive real-time text messages in the live room.</td>

<td rowspan="1" colSpan="1" >[BarrageStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_barrage_barrage_store/BarrageStore-class.html)</td>

<td rowspan="1" colSpan="1" >[Implementation Guide](https://write.woa.com/document/200455665056206848)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**Build a Gift Giving System**</td>

<td rowspan="1" colSpan="1" >Audience can send virtual gifts to the host, increasing engagement and fun.</td>

<td rowspan="1" colSpan="1" >[GiftStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_gift_gift_store/GiftStore-class.html)</td>

<td rowspan="1" colSpan="1" >[Implementation Guide](https://write.woa.com/document/195925512239050752)</td>
</tr>
</table>


## API documentation
<table>
<tr>
<td rowspan="1" colSpan="1" >**Store/Component**</td>

<td rowspan="1" colSpan="1" >**Feature Description**</td>

<td rowspan="1" colSpan="1" >**API Reference**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**LiveCoreWidget**</td>

<td rowspan="1" colSpan="1" >The core view component for live video stream display and interaction: responsible for video stream rendering and view widget processing, supporting scenarios like live streaming, audience co-broadcasting, and anchor connection.</td>

<td rowspan="1" colSpan="1" >[API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_view_live_live_core_widget/LiveCoreWidget-class.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**LiveCoreController**</td>

<td rowspan="1" colSpan="1" >The controller of LiveCoreWidget: used to set up the live streaming ID, control the preview, and perform other operations.</td>

<td rowspan="1" colSpan="1" >[API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_view_live_live_core_widget/LiveCoreController-class.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**LiveListStore**</td>

<td rowspan="1" colSpan="1" >Full lifecycle management of live streaming room: create/join/leave/terminate room, query room list, modify live information (name, notice), listen to live status (for example, being kicked out, ended).</td>

<td rowspan="1" colSpan="1" >[API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_live_list_store/LiveListStore-class.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**DeviceStore**</td>

<td rowspan="1" colSpan="1" >Audio/Video device control: microphone (on/off, volume), camera (on/off, switchover, video quality), screen sharing, monitor device status in real time.</td>

<td rowspan="1" colSpan="1" >[API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_device_device_store/DeviceStore-class.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**CoGuestStore**</td>

<td rowspan="1" colSpan="1" >Audience co-broadcasting management: join microphone application/invite/grant/deny, attendee permission control (microphone/camera), state synchronization.</td>

<td rowspan="1" colSpan="1" >[API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_co_guest_store/CoGuestStore-class.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**CoHostStore**</td>

<td rowspan="1" colSpan="1" >Anchor cross-room connection: supports multiple layout templates (dynamic grid, etc.), initiate/accept/reject connection, and manage interactive co-broadcasting with Anchors.</td>

<td rowspan="1" colSpan="1" >[API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_co_host_store/CoHostStore-class.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**BattleStore**</td>

<td rowspan="1" colSpan="1" >Anchor PK battle: trigger PK (duration configuration/competitor), manage PK status (start/End), synchronize score, listen to battle results.</td>

<td rowspan="1" colSpan="1" >[API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_battle_store/BattleStore-class.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**GiftStore**</td>

<td rowspan="1" colSpan="1" >Gift interaction: get gift list, send/receive gifts, listen to gift events (including sender, gift details).</td>

<td rowspan="1" colSpan="1" >[API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_gift_gift_store/GiftStore-class.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**BarrageStore**</td>

<td rowspan="1" colSpan="1" >Danmaku function: send text/custom barrage item, maintain bullet screen list, monitor bullet screen status in real time.</td>

<td rowspan="1" colSpan="1" >[API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_barrage_barrage_store/BarrageStore-class.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**LikeStore**</td>

<td rowspan="1" colSpan="1" >Like interaction: send likes, listen to like events, sync total likes.</td>

<td rowspan="1" colSpan="1" >[API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_like_store/LikeStore-class.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**LiveAudienceStore**</td>

<td rowspan="1" colSpan="1" >Audience management: get real-time audience list (ID/name/avatar), check audience size, listen to Enter/Exit Event.</td>

<td rowspan="1" colSpan="1" >[API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_live_live_audience_store/LiveAudienceStore-class.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**AudioEffectStore**</td>

<td rowspan="1" colSpan="1" >Audio effects: voice-changing (child voice/male voice), reverberation (KTV), ear monitoring adjustment, switch effects in real time.</td>

<td rowspan="1" colSpan="1" >[API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_device_audio_effect_store/AudioEffectStore-class.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**BaseBeautyStore**</td>

<td rowspan="1" colSpan="1" >Basic beauty filter: adjust skin smoothing/whitening/rosy (0-100 levels), reset beauty effect status, synchronize effect parameters.</td>

<td rowspan="1" colSpan="1" >[API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_device_base_beauty_store/BaseBeautyStore-class.html)</td>
</tr>
</table>


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



