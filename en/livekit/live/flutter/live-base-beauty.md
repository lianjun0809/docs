> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

`BaseBeautyStore` is the module in `AtomicXCore` for management of basic beauty effects for portraits. Through it, you can easily add natural beauty effects to your live stream or call applications.

## Core Features
- **Skin smoothing adjustment**: Set the skin smoothing strength (0-9).

- **Brightening effect adjustment**: Set the brightening strength (0-9).

- **Rosy effect adjustment**: Set the rosy strength (0-9).

- **Effect reset**: One-click restore all beauty parameters to default value.

- **Listen for status**: Get currently effective beauty parameters in real time.


## Core Concepts

Before starting integration, we first learn about the core concepts related to `BaseBeautyStore` in the following table:
<table>
<tr>
<td rowspan="1" colSpan="1" >**Core Concepts**</td>

<td rowspan="1" colSpan="1" >**Type**</td>

<td rowspan="1" colSpan="1" >**Core Responsibilities and Description**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[BaseBeautyState](https://tencent-rtc.github.io/TUIKit_Flutter/api_device_base_beauty_store/BaseBeautyState-class.html)</td>

<td rowspan="1" colSpan="1" >`class`</td>

<td rowspan="1" colSpan="1" >Represents the current status of the beauty module. It includes the intensity values of currently effective skin smoothing (`smoothLevel`), whitening (`whitenessLevel`), and rosy (`ruddyLevel`). All attributes are `ValueListenable<double>` data type and support subscription listening.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[BaseBeautyStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_device_base_beauty_store/BaseBeautyStore-class.html)</td>

<td rowspan="1" colSpan="1" >`class`</td>

<td rowspan="1" colSpan="1" >This is the core management class for interacting with the basic beauty filter feature. It is a Global Singleton (`shared`), responsible for ALL basic beauty parameter settings, reset and state synchronization.</td>
</tr>
</table>


## Implementation Steps

### Step 1: Integrating the Component

Refer to [Quick Connection](https://write.woa.com/document/200455640177692672) for seamless integration with **AtomicXCore** and access completed.

### Step 2: Getting the Instance and Listening to the Status

Get the Global Singleton of `BaseBeautyStore` and set a listener to get the current beauty effect parameter status in real time.

#### Implementation Method
1. **Get the singleton**: Directly use `BaseBeautyStore.shared` to get the globally unique `BaseBeautyStore` instance.

2. **Subscription status**: Listen for changes in the `baseBeautyState` properties via `addListener` to get beauty parameter updates in real time.


#### Sample Code
``` java
import 'package:flutter/material.dart';
import 'package:atomic_x_core/atomicxcore.dart';

class BeautyManager {
  // 1. Get a singleton
  final _baseBeautyStore = BaseBeautyStore.shared;
  late final VoidCallback _smoothLevelChangedListener = _onSmoothLevelChanged;
  late final VoidCallback _whitenessLevelChangedListener = _onWhitenessLevelChanged;
  late final VoidCallback _ruddyLevelChangedListener = _onRuddyLevelChanged;

  // 2. Subscription status
  void subscribeToBeautyState() {
    _baseBeautyStore.baseBeautyState.smoothLevel.addListener(_smoothLevelChangedListener);
    _baseBeautyStore.baseBeautyState.whitenessLevel.addListener(_whitenessLevelChangedListener);
    _baseBeautyStore.baseBeautyState.ruddyLevel.addListener(_ruddyLevelChangedListener);
  }

  void _onSmoothLevelChanged() {
    final level = _baseBeautyStore.baseBeautyState.smoothLevel.value;
    debugPrint('Skin smoothing strength adjustment: $level');
  }

  void _onWhitenessLevelChanged() {
    final level = _baseBeautyStore.baseBeautyState.whitenessLevel.value;
    debugPrint('Whitening strength adjustment: $level');
  }

  void _onRuddyLevelChanged() {
    final level = _baseBeautyStore.baseBeautyState.ruddyLevel.value;
    debugPrint('Rosy strength adjustment: $level');
  }

  // Execute dispose before logging out of the App
  void dispose() {
    _baseBeautyStore.baseBeautyState.smoothLevel.removeListener(_smoothLevelChangedListener);
    _baseBeautyStore.baseBeautyState.whitenessLevel.removeListener(_whitenessLevelChangedListener);
    _baseBeautyStore.baseBeautyState.ruddyLevel.removeListener(_ruddyLevelChangedListener);
  }
}
```

### Step 3: Set Beauty Parameter

When the user drags the beauty effect slider or clicks the preset button, call the appropriate API to set the intensity of beauty effects.

#### Implementation Method
1. **Get intensity value**: Obtain the intensity value set by the user from the UI control (such as `Slider`). The parameter range accepted by the SDK API is `0-9`, where `0` means disabling the effect and `9` indicates the most obvious effect. You need to map the value of the UI control (for example, `0.0 - 1.0` of the Slider) to the range of `0 - 9`.

2. **API call**: Call `setSmoothLevel()`, `setWhitenessLevel()`, and `setRuddyLevel()` to set the intensity of skin smoothing, whitening, and rosy effect.


#### Sample Code
``` java
extension BeautyManagerExtension on BeautyManager {
  /// Set the skin smoothing strength (input range 0.0 ~ 1.0, internal conversion to 0 ~ 9)
  void updateSmoothLevel(double uiLevel) {
    // Map the UI's 0.0 ~ 1.0 to the SDK's 0 ~ 9
    final sdkLevel = uiLevel * 9.0;
    _baseBeautyStore.setSmoothLevel(sdkLevel);
  }

  /// Set the whitening strength (input range 0.0 ~ 1.0, internal conversion to 0 ~ 9)
  void updateWhitenessLevel(double uiLevel) {
    final sdkLevel = uiLevel * 9.0;
    _baseBeautyStore.setWhitenessLevel(sdkLevel);
  }

  /// Set the ruddy level (input range 0.0 ~ 1.0, internal conversion to 0 ~ 9)
  void updateRuddyLevel(double uiLevel) {
    final sdkLevel = uiLevel * 9.0;
    _baseBeautyStore.setRuddyLevel(sdkLevel);
  }
}
```

### Step 4: Reset Beauty Effect

When the user clicks the "Reset" or "Disable Beauty Effects" button, restore all beauty parameters to the default value (usually 0).

#### Implementation Method

**Calling the API**: call directly the `baseBeautyStore.reset()` method.

#### Sample Code
``` java
extension BeautyManagerReset on BeautyManager {
  /// Reset ALL basic beauty effects
  void resetBeautyEffects() {
    _baseBeautyStore.reset();
  }
}
```

## Building a Beauty Effect UI

Flutter recommended using `ValueListenableBuilder` to build responsive UI, which auto-updates the interface when beauty effect parameters change:
``` java
class BeautySliderWidget extends StatelessWidget {
  final beautyStore = BaseBeautyStore.shared;

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        // Skin smoothing slider
        ValueListenableBuilder<double>(
          valueListenable: beautyStore.baseBeautyState.smoothLevel,
          builder: (context, smoothLevel, child) {
            return Row(
              children: [
                Text('Skin smoothing')
                Expanded(
                  child: Slider(
                    value: smoothLevel,
                    min: 0,
                    max: 9,
                    divisions: 9,
                    onChanged: (value) {
                      beautyStore.setSmoothLevel(value);
                    },
                  ),
                ),
                Text('${smoothLevel.toInt()}'),
              ],
            );
          },
        ),
        // Whitening slider
        ValueListenableBuilder<double>(
          valueListenable: beautyStore.baseBeautyState.whitenessLevel,
          builder: (context, whitenessLevel, child) {
            return Row(
              children: [
                Text('Whitening')
                Expanded(
                  child: Slider(
                    value: whitenessLevel,
                    min: 0,
                    max: 9,
                    divisions: 9,
                    onChanged: (value) {
                      beautyStore.setWhitenessLevel(value);
                    },
                  ),
                ),
                Text('${whitenessLevel.toInt()}'),
              ],
            );
          },
        ),
        // rosy slider
        ValueListenableBuilder<double>(
          valueListenable: beautyStore.baseBeautyState.ruddyLevel,
          builder: (context, ruddyLevel, child) {
            return Row(
              children: [
                Text('Rosy')
                Expanded(
                  child: Slider(
                    value: ruddyLevel,
                    min: 0,
                    max: 9,
                    divisions: 9,
                    onChanged: (value) {
                      beautyStore.setRuddyLevel(value);
                    },
                  ),
                ),
                Text('${ruddyLevel.toInt()}'),
              ],
            );
          },
        ),
      ],
    );
  }
}
```

## Complete Example
``` java
import 'package:flutter/material.dart';
import 'package:atomic_x_core/atomicxcore.dart';

class BeautySettingsPage extends StatelessWidget {
  final beautyStore = BaseBeautyStore.shared;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Beauty settings')),
      body: Padding(
        padding: EdgeInsets.all(16),
        child: Column(
          children: [
            // Skin smoothing
            _buildBeautySlider(
              title: 'Skin smoothing'
              valueListenable: beautyStore.baseBeautyState.smoothLevel,
              onChanged: (value) => beautyStore.setSmoothLevel(value),
            ),
            SizedBox(height: 20),
            // Whitening
            _buildBeautySlider(
              title: 'Whitening',
              valueListenable: beautyStore.baseBeautyState.whitenessLevel,
              onChanged: (value) => beautyStore.setWhitenessLevel(value),
            ),
            SizedBox(height: 20),
            // Rosy
            _buildBeautySlider(
              title: 'Rosy'
              valueListenable: beautyStore.baseBeautyState.ruddyLevel,
              onChanged: (value) => beautyStore.setRuddyLevel(value),
            ),
            SizedBox(height: 40),
            // reset button
            ElevatedButton(
              onPressed: () {
                beautyStore.reset();
              },
              child: Text('Reset beauty effect'),
            ),
          ],
        ),
      ),
    );
  }

  Widget _buildBeautySlider({
    required String title,
    required ValueListenable<double> valueListenable,
    required ValueChanged<double> onChanged,
  }) {
    return ValueListenableBuilder<double>(
      valueListenable: valueListenable,
      builder: (context, value, child) {
        return Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Row(
              mainAxisAlignment: MainAxisAlignment.spaceBetween,
              children: [
                Text(title, style: TextStyle(fontSize: 16)),
                Text('${value.toInt()}', style: TextStyle(fontSize: 16)),
              ],
            ),
            Slider(
              value: value,
              min: 0,
              max: 9,
              divisions: 9,
              onChanged: onChanged,
            ),
          ],
        );
      },
    );
  }
}
```

## Advanced Features

### Basic Beauty Filter Vs Advanced Beauty Effect

AtomicXCore also provided advanced beauty effect support to meet requirements of different scenes:
<table>
<tr>
<td rowspan="1" colSpan="1" >**Comparison Item**</td>

<td rowspan="1" colSpan="1" >**Basic Beauty Filter (BaseBeautyStore)**</td>

<td rowspan="1" colSpan="1" >**Advanced Beauty Effect (TencentEffect Requires Additional Integration)**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Core Features</td>

<td rowspan="1" colSpan="1" >Skin smoothing, whitening, rosy</td>

<td rowspan="1" colSpan="1" >Includes basic beauty filter, with various effects like V-face, eye distance adjustment, nose slimming, 3D stickers, filters, and makeup.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Billing</td>

<td rowspan="1" colSpan="1" >free (included in AtomicXCore license)</td>

<td rowspan="1" colSpan="1" >Payment (Tencent Effect SDK License must be bought extra).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >integration method</td>

<td rowspan="1" colSpan="1" >default built-in, direct use `BaseBeautyStore.shared`</td>

<td rowspan="1" colSpan="1" >Additional integration of the `TencentEffect` component is required and authenticate.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Recommended scenarios</td>

<td rowspan="1" colSpan="1" >Scenarios with low beauty effect requirements that need quick implementation of basic beauty effect features</td>

<td rowspan="1" colSpan="1" >Scenarios with high beauty effect requirements that require various advanced functions such as beauty shaping, stickers, and filters.</td>
</tr>
</table>


### Integrate Advanced Beauty Effect

If you need to use the advanced beauty function, refer to the [Advanced Beauty](https://trtc.io/document/73778?product=beautyar&menulabel=core%20sdk&platform=flutter) document for integration. After successful integration and authentication of `TencentEffect`, you can control ALL beauty effects through the API provided by `TencentEffect`.

## API Reference

### BaseBeautyStore
<table>
<tr>
<td rowspan="1" colSpan="1" >**Property/Method**</td>

<td rowspan="1" colSpan="1" >**Type**</td>

<td rowspan="1" colSpan="1" >**Note**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`shared`</td>

<td rowspan="1" colSpan="1" >`BaseBeautyStore`</td>

<td rowspan="1" colSpan="1" >Singleton instance</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`baseBeautyState`</td>

<td rowspan="1" colSpan="1" >`BaseBeautyState`</td>

<td rowspan="1" colSpan="1" >Beauty effect status</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`setSmoothLevel`</td>

<td rowspan="1" colSpan="1" >`void`</td>

<td rowspan="1" colSpan="1" >Set the skin smoothing strength (0-9).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`setWhitenessLevel`</td>

<td rowspan="1" colSpan="1" >`void`</td>

<td rowspan="1" colSpan="1" >Set the brightening strength (0-9).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`setRuddyLevel`</td>

<td rowspan="1" colSpan="1" >`void`</td>

<td rowspan="1" colSpan="1" >Set the rosy strength (0-9).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`reset`</td>

<td rowspan="1" colSpan="1" >`void`</td>

<td rowspan="1" colSpan="1" >Reset all beauty parameters to default value (0).</td>
</tr>
</table>


### BaseBeautyState
<table>
<tr>
<td rowspan="1" colSpan="1" >**Attribute**</td>

<td rowspan="1" colSpan="1" >**Type**</td>

<td rowspan="1" colSpan="1" >**Note**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`smoothLevel`</td>

<td rowspan="1" colSpan="1" >`ValueListenable<double>`</td>

<td rowspan="1" colSpan="1" >Skin smoothing strength (0-9).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`whitenessLevel`</td>

<td rowspan="1" colSpan="1" >`ValueListenable<double>`</td>

<td rowspan="1" colSpan="1" >Brightening strength (0-9).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`ruddyLevel`</td>

<td rowspan="1" colSpan="1" >`ValueListenable<double>`</td>

<td rowspan="1" colSpan="1" >Rosy strength (0-9).</td>
</tr>
</table>


## FAQs

### I Set Up the Beauty Parameter, Why No Effect?

Please check the following points:
1. **Is the camera enabled**: You must successfully turn on the camera (e.g. by `DeviceStore.shared.openLocalCamera()`) before the beauty effect can apply to the video stream.

2. **Whether to use advanced beauty effect**: If you integrated `TencentEffect` (advanced beauty), ensure you use the API provided by `TencentEffect` to adjust the beauty effect.

3. **Parameter range**: If you use basic beauty filter, confirm the strength value passed in is within the effective range (a double value between `0` and `9`).


