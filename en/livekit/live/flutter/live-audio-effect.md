> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

This document aims to guide you on how to use the `AtomicXCore` framework's `AudioEffectStore` and `DeviceStore` modules to quickly integrate audio effect control features for your live stream app, including Microphone Volume, listen, and add multiple fun voice-changing effects and reverb effects.

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032457995/5a187583f76311f0859b52540097cba1.png)


## Core Features

By combining `AudioEffectStore` and `DeviceStore`, you can implement the following core features:
- **Vocal Volume Adjustment**: Controls the capturing volume of Local Audio Uplink, which determines the Anchor's sound level heard by the audience.

- **Ear monitoring function**: Allows the Anchor or co-streaming users to hear their own sound in real-time through headphones for listening and pronunciation correction.

- **Voice-changing effects**: Offers multiple fun voice changing options, such as lolita, uncle, and mischievous child.

- **Reverb effect**: Simulates sound field effects in different environments, such as KTV, metallic sound, deep, and resonant.


## Conceptual Introduction
<table>
<tr>
<td rowspan="1" colSpan="1" >**Core Concept**</td>

<td rowspan="1" colSpan="1" >**Type**</td>

<td rowspan="1" colSpan="1" >**Core Responsibilities and Description**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[AudioEffectState](https://tencent-rtc.github.io/TUIKit_Flutter/api_device_audio_effect_store/AudioEffectState-class.html)</td>

<td rowspan="1" colSpan="1" >`class`</td>

<td rowspan="1" colSpan="1" >Represents the current status of the audio effect module, usually used for UI rendering. Includes voice-changing status, reverberation status, ear return enabled status, ear return volume. All attributes are `ValueListenable` data type, support subscription listen.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[AudioEffectStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_device_audio_effect_store/AudioEffectStore-class.html)</td>

<td rowspan="1" colSpan="1" >`class`</td>

<td rowspan="1" colSpan="1" >Represents the **singleton data management class** of the audio effect module. Through it you can call the audio effect API to modify sound effects. When you call the API, the appropriate `audioEffectState` property will auto-update. You can subscribe to this state's responsive data to receive and listen for status updates.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[DeviceState](https://tencent-rtc.github.io/TUIKit_Flutter/api_device_device_store/DeviceState-class.html)</td>

<td rowspan="1" colSpan="1" >`class`</td>

<td rowspan="1" colSpan="1" >Represents the current status of the device module, usually used for UI rendering. Core attributes include device status of camera, microphone, capturing volume. All attributes are `ValueListenable` data type, support subscription listen.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[DeviceStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_device_device_store/DeviceStore-class.html)</td>

<td rowspan="1" colSpan="1" >`class`</td>

<td rowspan="1" colSpan="1" >Represents the **singleton data management class** of the device module. Through it you can call the API to operate camera and microphone. When you call the API, the appropriate `state` property will auto-update. You can subscribe to this state's responsive data to receive and listen for status updates.</td>
</tr>
</table>


## Implementation Steps

### Step 1: Integrating the Component
- **Live streaming**: Refer to [quick integration](https://write.woa.com/document/200455640177692672) to integrate **AtomicXCore** and complete service access.

- **Voice chat room**: Refer to [quick integration](https://write.woa.com/document/200555778169073664) to integrate **AtomicXCore** and complete service access.


### Step 2: Obtain a Store Instance

`AudioEffectStore` and `DeviceStore` are singleton objects. You can directly get instance via the `shared` property in any location in the project. You can also refer to the [audio_effect_panel_widget.dart](https://github.com/Tencent-RTC/TUIKit_Flutter/blob/main/live/livekit/lib/component/audio_effect/audio_effect_panel_widget.dart) file in the TUILiveKit open-source UI demo project to learn about the complete implementation logic.
``` java
import 'package:flutter/material.dart';
import 'package:atomic_x_core/atomicxcore.dart';

class _AudioEffectPanelWidgetState {
  final _audioEffectStore = AudioEffectStore.shared;
  final _deviceStore = DeviceStore.shared;
}
```

### Step 3: Implement the In-Ear Monitoring Feature

Ear monitoring function allows users to monitor their own microphone sound in real time. Calling the API introduced in this section can manage the ear monitoring function.

> **Note:**
> 

> The in-ear monitoring feature typically needs to connect to headphones to work properly.
> 


#### Implementation Method
1. **Enable/Disable Ear Monitoring**: You can use the `Switch` control to implement the ear monitoring function.

2. **Set the Volume of IEMs**: You can use the `Slider` control to implement the function of dragging the slider left and right to adjust volume, and map the `Slider` value to the volume value, then call `setVoiceEarMonitorVolume(volume)`. Please note, this API accepts a parameter range of `[0, 150]`, so you need to map the UI control value (such as the Slider's `0.0 - 1.0`) to the `0 - 150` range.

3. **Listen for Status Updates to Update UI**: You can subscribe to real-time ear monitoring status value updates to refresh the UI.


#### Sample Code
``` java
import 'package:flutter/material.dart';
import 'package:atomic_x_core/atomicxcore.dart';

/// Ear Monitoring Control Component
class EarMonitorWidget extends StatelessWidget {
  const EarMonitorWidget({super.key});

  @override
  Widget build(BuildContext context) {
    final audioEffectStore = AudioEffectStore.shared;

    return Column(
      crossAxisAlignment: CrossAxisAlignment.start,
      children: [
        // 1. Toggle ear monitoring
        ValueListenableBuilder<bool>(
          valueListenable: audioEffectStore.audioEffectState.isEarMonitorOpened,
          builder: (context, isOpened, child) {
            return SwitchListTile(
              title: const Text('Ear Monitoring'),
              subtitle: const Text('Insert a headset')
              value: isOpened,
              onChanged: (value) {
                audioEffectStore.setVoiceEarMonitorEnable(value);
              },
            );
          },
        ),
        // 2. Adjust ear return volume
        ValueListenableBuilder<int>(
          valueListenable: audioEffectStore.audioEffectState.earMonitorVolume,
          builder: (context, volume, child) {
            return ListTile(
              title: const Text('Ear Monitoring Volume'),
              subtitle: Slider(
                value: volume.toDouble(),
                min: 0,
                max: 150,
                divisions: 150,
                onChanged: (value) {
                  audioEffectStore.setVoiceEarMonitorVolume(value.toInt());
                },
              ),
              trailing: Text('$volume'),
            );
          },
        ),
      ],
    );
  }
}
```

#### SetVoiceEarMonitorEnable API Parameter
<table>
<tr>
<td rowspan="1" colSpan="1" >**Parameter Name**</td>

<td rowspan="1" colSpan="1" >**Type**</td>

<td rowspan="1" colSpan="1" >**Description**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`enable`</td>

<td rowspan="1" colSpan="1" >`bool`</td>

<td rowspan="1" colSpan="1" >Enable earpiece feedback.<br>-  true: Enable<br>-  false: Disable</td>
</tr>
</table>


#### SetVoiceEarMonitorVolume API Parameter
<table>
<tr>
<td rowspan="1" colSpan="1" >**Parameter Name**</td>

<td rowspan="1" colSpan="1" >**Type**</td>

<td rowspan="1" colSpan="1" >**Description**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`volume`</td>

<td rowspan="1" colSpan="1" >`int`</td>

<td rowspan="1" colSpan="1" >Ear return volume.<br>- Value ranges from 0 to 150.<br>- Default value: 100.</td>
</tr>
</table>


### Step 4: Implement Vocal Volume Adjustment

When the Anchor hopes to adjust their own uplink capturing volume, call the `DeviceStore`'s `setCaptureVolume(volume)` method to input the volume value.

#### Implementation Method
1. **Set Capturing Volume**: You can use the `Slider` control to drag the slider left and right to adjust volume, and map the `Slider` value to the volume value before calling `setCaptureVolume(volume)`. Please note, this API accepts a parameter range of `[0, 150]`, so you need to map the UI control value (such as the Slider's `0.0 - 1.0`) to the `0 - 150` range.

2. **Listen for Status Updates to Update UI**: You can subscribe to real-time volume level status value updates to refresh the UI.


#### Sample Code
``` java
import 'package:flutter/material.dart';
import 'package:atomic_x_core/atomicxcore.dart';

/// Voice Volume Control Component
class CaptureVolumeWidget extends StatelessWidget {
  const CaptureVolumeWidget({super.key});

  @override
  Widget build(BuildContext context) {
    final deviceStore = DeviceStore.shared;

    return ValueListenableBuilder<int>(
      valueListenable: deviceStore.state.captureVolume,
      builder: (context, volume, child) {
        return ListTile(
          title: const Text('Voice Volume'),
          subtitle: Slider(
            value: volume.toDouble(),
            min: 0,
            max: 150,
            divisions: 150,
            onChanged: (value) {
              deviceStore.setCaptureVolume(value.toInt());
            },
          ),
          trailing: Text('$volume'),
        );
      },
    );
  }
}
```

#### SetCaptureVolume API Parameter
<table>
<tr>
<td rowspan="1" colSpan="1" >**Parameter Name**</td>

<td rowspan="1" colSpan="1" >**Type**</td>

<td rowspan="1" colSpan="1" >**Description**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`volume`</td>

<td rowspan="1" colSpan="1" >`int`</td>

<td rowspan="1" colSpan="1" >Capture volume size.<br>- Value ranges from 0 to 150.<br>- Default value: 100.</td>
</tr>
</table>


### Step 5: Implement Voice-Changing Effects

When the Anchor hopes to change their own sound, you can call the `setAudioChangerType(type)` method, input the appropriate Type enumeration value to switch effect.

#### Sample Code
``` java
import 'package:flutter/material.dart';
import 'package:atomic_x_core/atomicxcore.dart';

/// Voice changing effect selection component
class VoiceChangerWidget extends StatelessWidget {
  const VoiceChangerWidget({super.key});

  @override
  Widget build(BuildContext context) {
    final audioEffectStore = AudioEffectStore.shared;

    return Column(
      crossAxisAlignment: CrossAxisAlignment.start,
      children: [
        const Padding(
          padding: EdgeInsets.all(16),
          child: Text('Voice-changing effect', style: TextStyle(fontSize: 18, fontWeight: FontWeight.bold)),
        ),
        ValueListenableBuilder<AudioChangerType>(
          valueListenable: audioEffectStore.audioEffectState.audioChangerType,
          builder: (context, changerType, child) {
            return Padding(
              padding: const EdgeInsets.symmetric(horizontal: 16),
              child: Wrap(
                spacing: 8,
                runSpacing: 8,
                children: AudioChangerType.values.map((type) {
                  return ChoiceChip(
                    label: Text(_getChangerTypeName(type)),
                    selected: changerType == type,
                    onSelected: (selected) {
                      if (selected) {
                        audioEffectStore.setAudioChangerType(type);
                      }
                    },
                  );
                }).toList(),
              ),
            );
          },
        ),
      ],
    );
  }

  String _getChangerTypeName(AudioChangerType type) {
    switch (type) {
      case AudioChangerType.none:
        return 'Disable';
      case AudioChangerType.child:
        return 'mischievous child';
      case AudioChangerType.girl:
        return 'loli';
      case AudioChangerType.uncle:
        return 'uncle';
      case AudioChangerType.ethereal:
        return 'ethereal';
    }
  }
}
```

#### SetAudioChangerType API Parameter
<table>
<tr>
<td rowspan="1" colSpan="1" >**Parameter Name**</td>

<td rowspan="1" colSpan="1" >**Type**</td>

<td rowspan="1" colSpan="1" >**Description**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`type`</td>

<td rowspan="1" colSpan="1" >[AudioChangerType](https://tencent-rtc.github.io/TUIKit_Flutter/api_device_audio_effect_store/AudioChangerType.html)</td>

<td rowspan="1" colSpan="1" >Voice-changing effects enumeration.</td>
</tr>
</table>


### Step 6: Implement Reverb Effect

When the Anchor hopes to add reverb effect to their own sound, you can call the `setAudioReverbType(type)` method, input the appropriate Type enumeration value to switch effect.

#### Sample Code
``` java
import 'package:flutter/material.dart';
import 'package:atomic_x_core/atomicxcore.dart';

/// Reverb effect selection component
class ReverbWidget extends StatelessWidget {
  const ReverbWidget({super.key});

  @override
  Widget build(BuildContext context) {
    final audioEffectStore = AudioEffectStore.shared;

    return Column(
      crossAxisAlignment: CrossAxisAlignment.start,
      children: [
        const Padding(
          padding: EdgeInsets.all(16),
          child: Text('Reverb effect', style: TextStyle(fontSize: 18, fontWeight: FontWeight.bold)),
        ),
        ValueListenableBuilder<AudioReverbType>(
          valueListenable: audioEffectStore.audioEffectState.audioReverbType,
          builder: (context, reverbType, child) {
            return Padding(
              padding: const EdgeInsets.symmetric(horizontal: 16),
              child: Wrap(
                spacing: 8,
                runSpacing: 8,
                children: AudioReverbType.values.map((type) {
                  return ChoiceChip(
                    label: Text(_getReverbTypeName(type)),
                    selected: reverbType == type,
                    onSelected: (selected) {
                      if (selected) {
                        audioEffectStore.setAudioReverbType(type);
                      }
                    },
                  );
                }).toList(),
              ),
            );
          },
        ),
      ],
    );
  }

  String _getReverbTypeName(AudioReverbType type) {
    switch (type) {
      case AudioReverbType.none:
        return 'Disable';
      case AudioReverbType.ktv:
        return 'KTV';
      case AudioReverbType.room:
        return 'Small room';
      case AudioReverbType.hall:
        return 'Great hall';
      case AudioReverbType.deep:
        return 'deep';
      case AudioReverbType.loud:
        return 'resonant';
      case AudioReverbType.metallic:
        return 'metallic sound';
      case AudioReverbType.magnetic:
        return 'magnetic';
      case AudioReverbType.recordingStudio:
        return 'studio';
    }
  }
}
```

#### SetAudioReverbType API Parameter
<table>
<tr>
<td rowspan="1" colSpan="1" >**Parameter Name**</td>

<td rowspan="1" colSpan="1" >**Type**</td>

<td rowspan="1" colSpan="1" >**Description**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`type`</td>

<td rowspan="1" colSpan="1" >[AudioReverbType](https://tencent-rtc.github.io/TUIKit_Flutter/api_device_audio_effect_store/AudioReverbType.html)</td>

<td rowspan="1" colSpan="1" >Reverb effects enumeration.</td>
</tr>
</table>


### Step 7: Reset Sound Effect Settings

> **Important:**
> 

> AudioEffectStore and DeviceStore are singletons, so audio effects and device settings take effect globally. If you do not want the settings of the current live streaming room to affect other live streaming rooms created later, you need to reset the audio effects and device settings when the current live streaming room ends.
> 


You may need to reset sound effect settings in the following two scenarios:
1. **When the current live streaming room ends**, call the `store`'s `reset()` method to reset sound effects.

2. **When you need to reset all devices and sound effect settings**, call the `store`'s `reset()` method to reset sound effects.

   ``` java
   import 'package:flutter/material.dart';
   import 'package:atomic_x_core/atomicxcore.dart';
   
   /// Sound effect reset component
   class AudioEffectResetWidget extends StatelessWidget {
     const AudioEffectResetWidget({super.key});
   
     void _resetAudioEffect() {
       AudioEffectStore.shared.reset();
       DeviceStore.shared.reset();
     }
   
     @override
     Widget build(BuildContext context) {
       return ElevatedButton(
         onPressed: _resetAudioEffect,
         child: const Text('Reset sound effect settings'),
       );
     }
   }
   ```

## Complete Example
``` java
import 'package:flutter/material.dart';
import 'package:atomic_x_core/atomicxcore.dart';

/// Sound effect settings page
class AudioEffectPage extends StatelessWidget {
  const AudioEffectPage({super.key});

  @override
  Widget build(BuildContext context) {
    final audioEffectStore = AudioEffectStore.shared;
    final deviceStore = DeviceStore.shared;

    return Scaffold(
      appBar: AppBar(title: const Text('Sound effect settings')),
      body: ListView(
        children: [
          // Voice volume
          const Padding(
            padding: EdgeInsets.all(16),
            child: Text('Voice volume', style: TextStyle(fontSize: 18, fontWeight: FontWeight.bold)),
          ),
          ValueListenableBuilder<int>(
            valueListenable: deviceStore.state.captureVolume,
            builder: (context, volume, child) {
              return ListTile(
                title: const Text('Capture Volume'),
                subtitle: Slider(
                  value: volume.toDouble(),
                  min: 0,
                  max: 150,
                  divisions: 150,
                  onChanged: (value) {
                    deviceStore.setCaptureVolume(value.toInt());
                  },
                ),
                trailing: Text('$volume'),
              );
            },
          ),
          const Divider(),

          // Ear return settings
          const Padding(
            padding: EdgeInsets.all(16),
            child: Text('Ear monitoring', style: TextStyle(fontSize: 18, fontWeight: FontWeight.bold)),
          ),
          ValueListenableBuilder<bool>(
            valueListenable: audioEffectStore.audioEffectState.isEarMonitorOpened,
            builder: (context, isOpened, child) {
              return SwitchListTile(
                title: const Text('Enable Ear Monitoring'),
                subtitle: const Text('Insert a headset')
                value: isOpened,
                onChanged: (value) {
                  audioEffectStore.setVoiceEarMonitorEnable(value);
                },
              );
            },
          ),
          ValueListenableBuilder<int>(
            valueListenable: audioEffectStore.audioEffectState.earMonitorVolume,
            builder: (context, volume, child) {
              return ListTile(
                title: const Text('Ear Monitoring Volume'),
                subtitle: Slider(
                  value: volume.toDouble(),
                  min: 0,
                  max: 150,
                  divisions: 150,
                  onChanged: (value) {
                    audioEffectStore.setVoiceEarMonitorVolume(value.toInt());
                  },
                ),
                trailing: Text('$volume'),
              );
            },
          ),
          const Divider(),

          // Voice changing settings
          const Padding(
            padding: EdgeInsets.all(16),
            child: Text('Voice-changing', style: TextStyle(fontSize: 18, fontWeight: FontWeight.bold)),
          ),
          ValueListenableBuilder<AudioChangerType>(
            valueListenable: audioEffectStore.audioEffectState.audioChangerType,
            builder: (context, changerType, child) {
              return Padding(
                padding: const EdgeInsets.symmetric(horizontal: 16),
                child: Wrap(
                  spacing: 8,
                  runSpacing: 8,
                  children: AudioChangerType.values.map((type) {
                    return ChoiceChip(
                      label: Text(_getChangerTypeName(type)),
                      selected: changerType == type,
                      onSelected: (selected) {
                        if (selected) {
                          audioEffectStore.setAudioChangerType(type);
                        }
                      },
                    );
                  }).toList(),
                ),
              );
            },
          ),
          const SizedBox(height: 16),
          const Divider(),

          // Reverb settings
          const Padding(
            padding: EdgeInsets.all(16),
            child: Text('Reverb', style: TextStyle(fontSize: 18, fontWeight: FontWeight.bold)),
          ),
          ValueListenableBuilder<AudioReverbType>(
            valueListenable: audioEffectStore.audioEffectState.audioReverbType,
            builder: (context, reverbType, child) {
              return Padding(
                padding: const EdgeInsets.symmetric(horizontal: 16),
                child: Wrap(
                  spacing: 8,
                  runSpacing: 8,
                  children: AudioReverbType.values.map((type) {
                    return ChoiceChip(
                      label: Text(_getReverbTypeName(type)),
                      selected: reverbType == type,
                      onSelected: (selected) {
                        if (selected) {
                          audioEffectStore.setAudioReverbType(type);
                        }
                      },
                    );
                  }).toList(),
                ),
              );
            },
          ),
          const SizedBox(height: 24),

          // reset button
          Padding(
            padding: const EdgeInsets.all(16),
            child: ElevatedButton(
              onPressed: () {
                audioEffectStore.reset();
                deviceStore.reset();
              },
              child: const Text('Reset sound effect settings'),
            ),
          ),
        ],
      ),
    );
  }

  String _getChangerTypeName(AudioChangerType type) {
    switch (type) {
      case AudioChangerType.none:
        return 'Disable';
      case AudioChangerType.child:
        return 'mischievous child';
      case AudioChangerType.girl:
        return 'loli';
      case AudioChangerType.uncle:
        return 'uncle';
      case AudioChangerType.ethereal:
        return 'ethereal';
    }
  }

  String _getReverbTypeName(AudioReverbType type) {
    switch (type) {
      case AudioReverbType.none:
        return 'Disable';
      case AudioReverbType.ktv:
        return 'KTV';
      case AudioReverbType.room:
        return 'Small room';
      case AudioReverbType.hall:
        return 'Great hall';
      case AudioReverbType.deep:
        return 'deep';
      case AudioReverbType.loud:
        return 'resonant';
      case AudioReverbType.metallic:
        return 'metallic sound';
      case AudioReverbType.magnetic:
        return 'magnetic';
      case AudioReverbType.recordingStudio:
        return 'studio';
    }
  }
}
```

## API documentation

For detailed information about all public interfaces and attributes of [AudioEffectStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_device_audio_effect_store/AudioEffectStore-class.html), [DeviceStore](https://tencent-rtc.github.io/TUIKit_Flutter/api_device_device_store/DeviceStore-class.html) and its related classes, see the official API documentation of the [AtomicXCore](https://tencent-rtc.github.io/TUIKit_Flutter/index.html) framework.
<table>
<tr>
<td rowspan="1" colSpan="1" >**Store/Component**</td>

<td rowspan="1" colSpan="1" >**Feature Description**</td>

<td rowspan="1" colSpan="1" >**API Reference**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**AudioEffectStore**</td>

<td rowspan="1" colSpan="1" >Audio effect management: Perform audio effect settings and obtain real-time audio effect status.</td>

<td rowspan="1" colSpan="1" >[API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_device_audio_effect_store/AudioEffectStore-class.html)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**DeviceStore**</td>

<td rowspan="1" colSpan="1" >Device management: perform camera and microphone operations and obtain real-time device status.</td>

<td rowspan="1" colSpan="1" >[API documentation](https://tencent-rtc.github.io/TUIKit_Flutter/api_device_device_store/DeviceStore-class.html)</td>
</tr>
</table>


## FAQs

### Is There a Requirement for the Timing of Invocation of Sound Effects and Device Interfaces?

No limit. The settings of `AudioEffectStore` and `DeviceStore` take effect globally. You can call APIs (such as setting voice-changing, reverb, or ear monitoring) at any time before or after entering the live room. The settings will take effect immediately and be reserved.

### What Is the Difference between Voice Volume and Ear Return Volume?

This is a very important and confusing concept. The difference is as follows:
- **Voice Volume (CaptureVolume):** Set via `DeviceStore.shared.setCaptureVolume()`. It determines the Anchor's sound level heard by the audience.

- **Ear Return Volume (EarMonitorVolume):** Set via `AudioEffectStore.shared.setVoiceEarMonitorVolume()`. It only determines the Anchor's headphone monitoring volume and **does not** impact the audience.


### Why Does a Newly Created Live Streaming Room Have Sound Effects Directly or Issues Like Very High or Low Volume?

`AudioEffectStore` and `DeviceStore` are singletons, which means audio effects and device settings take effect globally. This situation probably occurs because you set audio effects earlier but did not reset them. You need to call the `reset()` method in an appropriate place.

### Why Did I Enable "Ear Return" but Cannot Hear My Own Sound?

Please check by the following steps:
1. **Whether to insert headphones**: The in-ear monitoring feature depends on headphones most of the time for the changes to take effect. Please ensure wired or Bluetooth headphones are connected.

2. **Whether the volume is 0**: Check if the "ear return volume" is set to 0.

3. **Is the microphone enabled**: Confirm that the microphone in `DeviceStore` is enabled (the `openLocalMicrophone()` call has been made).


### Can Voice-Changing Effects and Reverb Effects Take Effect at the Same Time?

Yes. `AudioChangerType` and `AudioReverbType` can take effect in superposition. For example, you can simultaneously set `AudioChangerType.girl` voice-changing and `AudioReverbType.ktv` reverb.

