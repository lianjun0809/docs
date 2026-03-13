> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

# TRTC Real-Time Communication (TRTC SDK) Documentation
## Feature Overview
`TXAudioEffectManager.h` is the manager class for handling background music, sound effects, and vocal effects on the TRTC Real-Time Communication (TRTC SDK) iOS platform. Use this class to configure and control background music, sound effects, and vocal processing features.

## TXAudioEffectManager
| Function List | Description |
| --- | --- |
| enableVoiceEarMonitor: | Enable ear return |
| setVoiceEarMonitorVolume: | Set ear return volume |
| setVoiceReverbType: | Set vocal reverb effect |
| setVoiceChangerType: | Set vocal voice changing effect |
| setVoiceVolume: | Set speech volume |
| setVoicePitch: | Set speech tone |
| startPlayMusic:onStart:onProgress:onComplete: | Start playing background music |
| stopPlayMusic: | Stop playing background music |
| pausePlayMusic: | Pause background music |
| resumePlayMusic: | Resume background music |
| setAllMusicVolume: | Set the local and remote volume of all background music |
| setMusicPublishVolume:volume: | Set the remote volume of a specific background music track |
| setMusicPlayoutVolume:volume: | Set the local volume of a specific background music track |
| setMusicPitch:pitch: | Adjust the pitch of background music |
| setMusicSpeedRate:speedRate: | Adjust the variable speed effect of background music |
| getMusicCurrentPosInMS: | Get the playback progress of background music (unit: milliseconds) |
| getMusicDurationInMS: | Get the total duration of background music (unit: milliseconds) |
| seekMusicToPosInMS:pts: | Set the playback progress of background music (unit: milliseconds) |
| setMusicScratchSpeedRate:speedRate: | Adjust the variable speed effect of scratching |
| preloadMusic:onProgress:onError: | Preload background music |
| getMusicTrackCount: | Obtain the number of background music tracks |
| setMusicTrack:track: | Specify the playback track of background music |

## Structural type
| Function List | Description |
| --- | --- |
| TXAudioMusicParam | Playback control information for background music |

## Enumeration Types
| Enumeration Types | Description |
| --- | --- |
| TXVoiceReverbType | Reverb effects |
| TXVoiceChangeType | Voice changing effects |

## enableVoiceEarMonitor:

#### Enable ear return

After the host enables ear return, they can hear their own voice collected by the microphone in the headphones. This effect is suitable for scenarios where the host is singing.

It should be noted that due to the high hardware latency of Bluetooth headphones, this effect cannot be enabled when the host is wearing Bluetooth headphones. Please try to prompt the host to wear wired headphones in the user interface.

Also, please note that not all mobile phones can achieve excellent ear return effects after enabling this feature. We have blocked this effect for phones with poor ear return performance.
| Parameters | Description |
| --- | --- |
| enable | YES: On; NO: Off. |

> **Note**
> 

> This effect can only be enabled when the host is wearing headphones. Please also prompt the host to wear wired headphones.
> 

## setVoiceEarMonitorVolume:

#### Set ear return volume

Through this interface, you can set the volume of the sound in the ear return effect.
| Parameters | Description |
| --- | --- |
| volume | Volume. Value range: 0 - 100. Default value: 100. |

> **Note**
> 

> If you still feel the volume is too low after setting it to 100, you can set the maximum volume to 150. However, a volume above 100 carries a risk of pop noise, so proceed with caution.
> 

## setVoiceReverbType:

#### Set vocal reverb effect

Through this interface, you can set the vocal reverb effect. For specific effects, please refer to the enumeration Definition TXVoiceReverbType.

> **Note**
> 

> The set effect will automatically become invalid after leaving the room. If the corresponding effect is needed next time you enter the room, you need to call this interface to set it again.
> 

## setVoiceChangerType:

#### Set vocal voice changing effect

Through this interface, you can set the voice changing effect. For specific effects, please refer to the enumeration Definition TXVoiceChangeType.

> **Note**
> 

> The set effect will automatically become invalid after leaving the room. If the corresponding effect is needed next time you enter the room, you need to call this interface to set it again.
> 

## setVoiceVolume:

#### Set speech volume

This interface allows you to set the voice volume. It is generally used in conjunction with the music volume setting interface setAllMusicVolume, to balance the respective volumes of voice and music before mixing.
| Parameters | Description |
| --- | --- |
| volume | Volume. Value range: 0-100. Default value: 100. |

> **Note**
> 

> If you still feel the volume is too low after setting it to 100, you can set the maximum volume to 150. However, a volume above 100 carries a risk of pop noise, so proceed with caution.
> 

## setVoicePitch:

#### Set speech tone

This interface can set the voice pitch, achieving pitch change without speed variation.
| Parameters | Description |
| --- | --- |
| pitch | Pitch, value range: -1.0f to 1.0f, default value: 0.0f. |

## startPlayMusic:onStart:onProgress:onComplete:

#### Start playing background music

Each piece of music requires a specific ID. With this ID, you can control the start, stop, volume, etc., of the music.
| Parameters | Description |
| --- | --- |
| completeBlock | Play end callback. |
| musicParam | Music parameters. |
| progressBlock | Playback progress callback. |
| startBlock | Playback start callback. |

> **Note**
> 

> 1. If you need to play the same background music multiple times, do not assign a new ID each time. We recommend using the same ID.
> 

> 2. If you want to play different pieces of music simultaneously, assign different IDs for each piece.
> 

> 3. If you use the same ID to play different music, the SDK will stop the old music before playing the new one.
> 

## stopPlayMusic:

#### Stop playing background music
| Parameters | Description |
| --- | --- |
| id | Music ID. |

## pausePlayMusic:

#### Pause background music
| Parameters | Description |
| --- | --- |
| id | Music ID. |

## resumePlayMusic:

#### Resume background music
| Parameters | Description |
| --- | --- |
| id | Music ID. |

## setAllMusicVolume:

#### Set the local and remote volume of all background music

This interface allows you to set both the local and remote volume of all background music.
-  Local Volume: The volume of background music that the host can hear locally.

-  Remote Volume: The volume of background music that the audience can hear.

| Parameters | Description |
| --- | --- |
| volume | Volume range, value range is 0-100, default value: 60. |

> **Note**
> 

> If you still feel the volume is too low after setting it to 100, you can set the maximum volume to 150. However, a volume above 100 carries a risk of pop noise, so proceed with caution.
> 

## setMusicPublishVolume:volume:

#### Set the remote volume of a specific background music track

This interface can finely control the remote volume for each background music track, which is the volume the audience can hear.
| Parameters | Description |
| --- | --- |
| id | Music ID. |
| volume | Volume range, value range is 0-100; default value: 60. |

> **Note**
> 

> If you still feel the volume is too low after setting it to 100, you can set the maximum volume to 150. However, a volume above 100 carries a risk of pop noise, so proceed with caution.
> 

## setMusicPlayoutVolume:volume:

#### Set the local volume of a specific background music track

This interface can finely control the local volume for each background music track, which is the volume the host can hear locally.
| Parameters | Description |
| --- | --- |
| id | Music ID. |
| volume | Volume range, value range is 0-100, default value: 60. |

> **Note**
> 

> If you still feel the volume is too low after setting it to 100, you can set the maximum volume to 150. However, a volume above 100 carries a risk of pop noise, so proceed with caution.
> 

## setMusicPitch:pitch:

#### Adjust the pitch of background music
| Parameters | Description |
| --- | --- |
| id | Music ID. |
| pitch | Pitch, default value is 0.0f, value range is a floating point between [-1 ~ 1]. |

## setMusicSpeedRate:speedRate:

#### Adjust the variable speed effect of background music
| Parameters | Description |
| --- | --- |
| id | Music ID. |
| speedRate | Speed, default value is 1.0f, value range is a floating point between [0.5 ~ 2]. |

## getMusicCurrentPosInMS:

#### Get the playback progress of background music (unit: milliseconds)
| Parameters | Description |
| --- | --- |
| id | Music ID. |

#### Return value description:

On success, returns current playback time in milliseconds, on failure returns -1.

## getMusicDurationInMS:

#### Get the total duration of background music (unit: milliseconds)
| Parameters | Description |
| --- | --- |
| path | Music file path. |

#### Return value description:

On success, returns duration, on failure returns -1.

## seekMusicToPosInMS:pts:

#### Set the playback progress of background music (unit: milliseconds)
| Parameters | Description |
| --- | --- |
| id | Music ID. |
| pts | Unit: milliseconds. |

> **Note**
> 

> Please avoid calling this interface too frequently as it may read and write music files again, which can be time-consuming.
> 

> Therefore, when users drag the playback progress bar of the music, please call this interface after the user completes the drag operation.
> 

> Because the progress bar control on the UI often feeds back the user's drag progress at a high frequency, it would lead to a poor user experience without frequency limitations.
> 

## setMusicScratchSpeedRate:speedRate:

#### Adjust the variable speed effect of scratching
| Parameters | Description |
| --- | --- |
| id | Music ID. |
| scratchSpeedRate | Scratching speed, the default value is 1.0f, the range is a floating point number between [-12.0 ~ 12.0], the positive/negative value represents the forward/reverse direction, and the absolute value represents the speed. |

> **Note**
> 

> Precondition: preloadMusic is successful.
> 

## preloadMusic:onProgress:onError:

#### Preload background music

Each piece of music requires a specific ID. With this ID, you can control the start, stop, volume, etc., of the music.
| Parameters | Description |
| --- | --- |
| preloadParam | Preload music parameters. |

> **Note**
> 

> 1. Preloading supports up to 2 different IDs simultaneously, and the preload duration does not exceed 10 minutes. After use, stopPlayMusic must be called to prevent memory from not being released.
> 

> 2. If the music corresponding to this ID is playing, preloading will fail. You need to call stopPlayMusic first.
> 

> 3. When the musicParam is exactly the same as the musicParam passed to startPlayMusic, preloading is effective.
> 

## getMusicTrackCount:

#### Obtain the number of background music tracks
| Parameters | Description |
| --- | --- |
| id | Music ID. |

## setMusicTrack:track:

#### Specify the playback track of background music
| Parameters | Description |
| --- | --- |
| id | Music ID. |
| index | By default, the first audio track is played. The range of values is 0, total number of tracks). |

> **Note**
> 

> The total number of tracks can be obtained through the getMusicTrackCount interface.
> 

## TXVoiceReverbType

#### Reverb effects

Reverb effects can be applied to vocals, using acoustic algorithms to overlap the sound and simulate various immersive experiences in different environments. Currently, the following reverb effects are supported:

0:Off; 1:KTV; 2:Small Room; 3:Hall; 4:Deep; 5:Loud; 6:Metallic; 7:Magnetic; 8:Ethereal; 9:Studio; 10:Melodious; 11:Studio2.
| Enumeration | Value | Description |
| --- | --- | --- |
| TXVoiceReverbType_0 | 0 | Turn off effects |
| TXVoiceReverbType_1 | 1 | KTV |
| TXVoiceReverbType_2 | 2 | Small Room |
| TXVoiceReverbType_3 | 3 | Hall |
| TXVoiceReverbType_4 | 4 | Low-pitched |
| TXVoiceReverbType_5 | 5 | Loud |
| TXVoiceReverbType_6 | 6 | Metallic sound |
| TXVoiceReverbType_7 | 7 | Magnetic |
| TXVoiceReverbType_8 | 8 | Ethereal voice |
| TXVoiceReverbType_9 | 9 | Recording studio |
| TXVoiceReverbType_10 | 10 | Melodious |
| TXVoiceReverbType_11 | 11 | Recording studio 2 |

## TXVoiceChangeType

#### Voice changing effects

Voice changing effect can be applied to vocals. By using acoustic algorithms for secondary processing, the voice can acquire a different sound quality from the original. Currently, the following voice changing effects are supported:

0: Off; 1: Naughty kid; 2: Lolita; 3: Uncle; 4: Heavy metal; 5: Cold; 6: Foreign accent; 7: Trapped beast; 8: Fat nerd; 9: Strong current; 10: Heavy machinery; 11: Ethereal.
| Enumeration | Value | Description |
| --- | --- | --- |
| TXVoiceChangeType_0 | 0 | Off |
| TXVoiceChangeType_1 | 1 | Naughty kid |
| TXVoiceChangeType_2 | 2 | Lolita |
| TXVoiceChangeType_3 | 3 | Uncle |
| TXVoiceChangeType_4 | 4 | Heavy metal |
| TXVoiceChangeType_5 | 5 | Cold |
| TXVoiceChangeType_6 | 6 | Foreign accent |
| TXVoiceChangeType_7 | 7 | Trapped beast |
| TXVoiceChangeType_8 | 8 | Otaku |
| TXVoiceChangeType_9 | 9 | Strong electric current |
| TXVoiceChangeType_10 | 10 | Heavy Machinery |
| TXVoiceChangeType_11 | 11 | Ethereal voice |

## TXAudioMusicParam

#### Playback control information for background music

This information is used to specify background music details in the interface [startPlayMusic, including play ID, file path, loop count, etc.:

1. If you need to play the same background music multiple times, do not assign a new ID each time. We recommend using the same ID.

2. If you want to play different pieces of music simultaneously, assign different IDs for each piece.

3. If you use the same ID to play different music, the SDK will stop the old music before playing the new one.
| Enumeration Types | Description |
| --- | --- |
| ID | [Field Meaning] Music ID. [Special Instructions] The SDK allows playing multiple music tracks simultaneously, so IDs are needed to control start, stop, volume, etc. |
| endTimeMS | [Field Meaning] Music play end time, in milliseconds. 0 means play until the end of the file. |
| isShortFile | [Field Meaning] Whether the played file is a short music file. [Recommended Value] YES: short music file that needs to be played repeatedly; NO: normal music file. Default: NO. |
| loopCount | [Field Meaning] The number of times the music loops. [Recommended Value] Value range is 0 to any positive integer. Default: 0. 0 means play the music once; 1 means play the music twice; and so on. |
| path | [Field Meaning] The full path or URL of the audio file. Supported audio formats include MP3, AAC, M4A, WAV. |
| publish | [Field Meaning] Whether to transmit the music to the remote end. [Recommended Value] YES: The music is played locally and is also heard by remote users; NO: The host hears the music locally, but remote audience cannot. Default: NO. |
| startTimeMS | [Field Meaning] Music start time, in milliseconds. |
