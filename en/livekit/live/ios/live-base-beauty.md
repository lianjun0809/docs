> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

`BaseBeautyStore` is the module in **AtomicXCore** responsible for managing basic portrait beautification effects. This module enables you to easily add natural beautification features to your live streaming or video calling applications.

## Core Features
- **Skin Smoothing**: Configure smoothing intensity (0–9).

- **Skin Whitening:** Configure whitening intensity (0–9).

- **Rosy Cheeks**: Configure rosy intensity (0–9).

- **Effect Reset: **Instantly restore all beautification parameters to default.

- **State Monitoring:** Real-time access to currently applied beautification settings.


## Core Concepts
<table>
<tr>
<td rowspan="1" colSpan="1" >**Core Concept**</td>

<td rowspan="1" colSpan="1" >**Type**</td>

<td rowspan="1" colSpan="1" >**Core Responsibilities and Description**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`BaseBeautyState`</td>

<td rowspan="1" colSpan="1" >`struct`</td>

<td rowspan="1" colSpan="1" >- Represents the current state of the basic beautification module. <br>- Contains the currently applied intensity values for smoothing (smoothLevel), whitening (whitenessLevel), and rosy (ruddyLevel).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`BaseBeautyStore`</td>

<td rowspan="1" colSpan="1" >`class`</td>

<td rowspan="1" colSpan="1" >- The core management class for interacting with basic beautification features. <br>- Implemented as a global singleton (`shared`). Responsible for setting parameters, resetting effects, and synchronizing state across the app.</td>
</tr>
</table>


## Implementation

### Step 1: Component Integration
- **Video Live Streaming**: Please refer to [Quick Start](https://write.woa.com/document/194571606121816064) to integrate AtomicXCore and complete the setup of LiveCoreView.

- **Voice Chat Room**: Please refer to [Quick Start](https://write.woa.com/document/194571595685527552) to integrate AtomicXCore and complete the setup of LiveCoreView.


### Step 2: Obtain the Instance and Subscribe to State

Obtain the global singleton instance of `BaseBeautyStore` and subscribe to receive real-time updates of the current beautification parameter state.

#### Implementation
1. **Obtain Singleton**: Use `BaseBeautyStore.shared()` to access the global instance.

2. **Subscribe to State**: Subscribe to `baseBeautyStore.baseBeautyState` to receive real-time updates of `BaseBeautyState`.


#### Code Example
``` swift
import Foundation
import AtomicXCore 
import Combine     

class BeautyManager {
    // 1. Get the singleton instance
    private let baseBeautyStore = BaseBeautyStore.shared
    private var cancellables = Set<AnyCancellable>()
    
    // Expose beauty status externally
    let beautyStatePublisher = CurrentValueSubject<BaseBeautyState, Never>(BaseBeautyState())

    init() {
        // 2. Subscribe to the state
        subscribeToBeautyState()
    }
    
    private func subscribeToBeautyState() {
        baseBeautyStore.state
            .subscribe()
            .receive(on: DispatchQueue.main)
            .assign(to: \.value, on: beautyStatePublisher)
            .store(in: &cancellables)
    }
    
    // ... Subsequent methods
}
```

### Step 3: Set Beautification Parameters

When users adjust a beautification slider or select a preset, call the corresponding API to set the desired intensity.

#### Implementation
1. **Get Intensity Value**: 

  - Obtain the intensity value set by the user from the UI control (such as a `UISlider`). 

  - Note that the SDK interface accepts a parameter range of `[0, 9]`, where 0 means the effect is off, and 9 means the effect is most prominent. You need to map the UI control value (e.g., `0.0 - 1.0` for a `UISlider`) to the `0 - 9` range.

2. **Call API**: Use `setSmoothLevel(smoothLevel:)`, `setWhitenessLevel(whitenessLevel:)`, and `setRuddyLevel(ruddyLevel:)` to set the smoothing, whitening, and rosy intensities.


#### Code Example
``` swift
extension BeautyManager {
    /// Set the smoothing level (Input range 0.0 ~ 1.0, converted internally to 0 ~ 9)
    func updateSmoothLevel(uiLevel: Float) {
        // Map UI's 0.0 ~ 1.0 to SDK's 0 ~ 9
        let sdkLevel = uiLevel * 9.0
        baseBeautyStore.setSmoothLevel(smoothLevel: sdkLevel)
    }

    /// Set the whitening level (Input range 0.0 ~ 1.0, converted internally to 0 ~ 9)
    func updateWhitenessLevel(uiLevel: Float) {
        let sdkLevel = uiLevel * 9.0
        baseBeautyStore.setWhitenessLevel(whitenessLevel: sdkLevel)
    }

    /// Set the rosiness level (Input range 0.0 ~ 1.0, converted internally to 0 ~ 9)
    func updateRuddyLevel(uiLevel: Float) {
        let sdkLevel = uiLevel * 9.0
        baseBeautyStore.setRuddyLevel(ruddyLevel: sdkLevel)
    }
}
```

### Step 4: Reset Beautification Effects

When users click "Reset" or "Disable Beauty," restore all beautification parameters to their default values (typically 0).

#### Implementation
- **Call API**: Call the `baseBeautyStore.reset()` method.


#### Code Example
``` swift
extension BeautyManager {
    /// Reset all basic beauty effects
    func resetBeautyEffects() {
        baseBeautyStore.reset()
    }
}
```

## Advanced Features

### Comparison: Basic vs. Advanced Beautification

AtomicXCore also provides advanced beautification features for more demanding scenarios:
<table>
<tr>
<td rowspan="1" colSpan="1" >**Comparison Item**</td>

<td rowspan="1" colSpan="1" >**Basic Beautification (BaseBeautyStore)**</td>

<td rowspan="1" colSpan="1" >**Advanced Beautification (TEBeautyKit)**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Core Features</td>

<td rowspan="1" colSpan="1" >Smoothing, Whitening, Rosy</td>

<td rowspan="1" colSpan="1" >Includes all basic features, plus V-shape face, eye distance adjustment, nose slimming, 3D stickers, filters, makeup, and more</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Pricing</td>

<td rowspan="1" colSpan="1" >Free (included in AtomicXCore license)</td>

<td rowspan="1" colSpan="1" >Paid (Requires separate license)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Integration</td>

<td rowspan="1" colSpan="1" >Built-in by default; use `BaseBeautyStore.shared() `directly</td>

<td rowspan="1" colSpan="1" >Requires additional integration of the TEBeautyKit component and authentication</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Recommended Scenarios</td>

<td rowspan="1" colSpan="1" >Scenarios with basic beautification needs and rapid implementation requirements</td>

<td rowspan="1" colSpan="1" >Scenarios requiring advanced beautification, shaping, stickers, filters, and other premium features</td>
</tr>
</table>


### Integrating Advanced Beautification

To use advanced beautification features, refer to the [Advanced Beauty](https://trtc.io/document/60194?product=beautyar&menulabel=core%20sdk&platform=ios) documentation. After integrating and authenticating TEBeautyKit, use its APIs to control all beautification effects.

## API Documentation

For detailed information on all public interfaces, properties, and methods of [BaseBeautyStore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore/basebeautystore) and related classes, see the official API documentation for the [AtomicXCore](https://tencent-rtc.github.io/TUIKit_iOS/documentation/atomicxcore) framework. The relevant stores referenced in this guide are:
<table>
<tr>
<td rowspan="1" colSpan="1" >**Store/Component**</td>

<td rowspan="1" colSpan="1" >**Description**</td>

<td rowspan="1" colSpan="1" >**API Reference**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`LiveCoreView`</td>

<td rowspan="1" colSpan="1" >- Core view component for displaying and interacting with live video streams. Handles video rendering and view widgets, supports host streaming, audience co-hosting, host connections, and more.</td>

<td rowspan="1" colSpan="1" >[API Documentation](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.view/-live-core-view/index.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`DeviceStore`</td>

<td rowspan="1" colSpan="1" >Controls audio/video devices: microphone (on/off, volume), camera (on/off, switch, quality), screen sharing, and real-time device status monitoring.</td>

<td rowspan="1" colSpan="1" >[API Documentation](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.device/-device-store/index.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`BaseBeautyStore`</td>

<td rowspan="1" colSpan="1" >Basic beauty filters: adjust smoothing/whitening/rosiness (0-100), reset beauty status, and synchronize effect parameters.</td>

<td rowspan="1" colSpan="1" >[API Documentation](https://tencent-rtc.github.io/TUIKit_Android/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.device/-base-beauty-store/index.html)</td>
</tr>
</table>


## FAQs

### I adjusted the parameters, but there is no effect on the video.

**Check the following:**
1. **Camera Status**: Ensure the camera is turned on (e.g., via DeviceStore.shared().openLocalCamera). Beauty effects cannot apply to a black screen or audio-only stream.

2. **SDK Conflict**: If you have integrated `TEBeautyKit`, `BaseBeautyStore` APIs may be overridden. Use the `TEBeautyKit` APIs instead.

3. **Value Range**: Verify that you are passing values between 0 and 9. Passing 0 will result in no visible effect.
