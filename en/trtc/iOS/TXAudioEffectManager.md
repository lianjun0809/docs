> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

# TRTC Real-Time Communication (TRTC SDK) Documentation
## Feature Overview
`TXAudioEffectManager.h` is the manager class for handling background music, sound effects, and vocal effects on the TRTC Real-Time Communication (TRTC SDK) iOS platform. Use this class to configure and control background music, sound effects, and vocal processing features.


## TXAudioEffectManager
<table>
<tr>
<td rowspan="1" colSpan="1" >Function List</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[enableVoiceEarMonitor:](https://write.woa.com/document/87029789200396288)</td>

<td rowspan="1" colSpan="1" >Enable ear return</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setVoiceEarMonitorVolume:](https://write.woa.com/document/87029789200396288)</td>

<td rowspan="1" colSpan="1" >Set ear return volume</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setVoiceReverbType:](https://write.woa.com/document/87029789200396288)</td>

<td rowspan="1" colSpan="1" >Set vocal reverb effect</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setVoiceChangerType:](https://write.woa.com/document/87029789200396288)</td>

<td rowspan="1" colSpan="1" >Set vocal voice changing effect</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setVoiceVolume:](https://write.woa.com/document/87029789200396288)</td>

<td rowspan="1" colSpan="1" >Set speech volume</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setVoicePitch:](https://write.woa.com/document/87029789200396288)</td>

<td rowspan="1" colSpan="1" >Set speech tone</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[startPlayMusic:onStart:onProgress:onComplete:](https://write.woa.com/document/87029789200396288)</td>

<td rowspan="1" colSpan="1" >Start playing background music</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[stopPlayMusic:](https://write.woa.com/document/87029789200396288)</td>

<td rowspan="1" colSpan="1" >Stop playing background music</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[pausePlayMusic:](https://write.woa.com/document/87029789200396288)</td>

<td rowspan="1" colSpan="1" >Pause background music</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[resumePlayMusic:](https://write.woa.com/document/87029789200396288)</td>

<td rowspan="1" colSpan="1" >Resume background music</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setAllMusicVolume:](https://write.woa.com/document/87029789200396288)</td>

<td rowspan="1" colSpan="1" >Set the local and remote volume of all background music</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setMusicPublishVolume:volume:](https://write.woa.com/document/87029789200396288)</td>

<td rowspan="1" colSpan="1" >Set the remote volume of a specific background music track</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setMusicPlayoutVolume:volume:](https://write.woa.com/document/87029789200396288)</td>

<td rowspan="1" colSpan="1" >Set the local volume of a specific background music track</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setMusicPitch:pitch:](https://write.woa.com/document/87029789200396288)</td>

<td rowspan="1" colSpan="1" >Adjust the pitch of background music</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setMusicSpeedRate:speedRate:](https://write.woa.com/document/87029789200396288)</td>

<td rowspan="1" colSpan="1" >Adjust the variable speed effect of background music</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getMusicCurrentPosInMS:](https://write.woa.com/document/87029789200396288)</td>

<td rowspan="1" colSpan="1" >Get the playback progress of background music (unit: milliseconds)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getMusicDurationInMS:](https://write.woa.com/document/87029789200396288)</td>

<td rowspan="1" colSpan="1" >Get the total duration of background music (unit: milliseconds)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[seekMusicToPosInMS:pts:](https://write.woa.com/document/87029789200396288)</td>

<td rowspan="1" colSpan="1" >Set the playback progress of background music (unit: milliseconds)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setMusicScratchSpeedRate:speedRate:](https://write.woa.com/document/87029789200396288)</td>

<td rowspan="1" colSpan="1" >Adjust the variable speed effect of scratching</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[preloadMusic:onProgress:onError:](https://write.woa.com/document/87029789200396288)</td>

<td rowspan="1" colSpan="1" >Preload background music</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getMusicTrackCount:](https://write.woa.com/document/87029789200396288)</td>

<td rowspan="1" colSpan="1" >Obtain the number of background music tracks</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setMusicTrack:track:](https://write.woa.com/document/87029789200396288)</td>

<td rowspan="1" colSpan="1" >Specify the playback track of background music</td>
</tr>
</table>


## Structural type
<table>
<tr>
<td rowspan="1" colSpan="1" >Function List</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[TXAudioMusicParam](https://write.woa.com/document/87029789200396288)</td>

<td rowspan="1" colSpan="1" >Playback control information for background music</td>
</tr>
</table>


## Enumeration Types
<table>
<tr>
<td rowspan="1" colSpan="1" >Enumeration Types</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[TXVoiceReverbType](https://write.woa.com/document/87029789200396288)</td>

<td rowspan="1" colSpan="1" >Reverb effects</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[TXVoiceChangeType](https://write.woa.com/document/87029789200396288)</td>

<td rowspan="1" colSpan="1" >Voice changing effects</td>
</tr>
</table>


## enableVoiceEarMonitor:



#### Enable ear return

After the host enables ear return, they can hear their own voice collected by the microphone in the headphones. This effect is suitable for scenarios where the host is singing.



It should be noted that due to the high hardware latency of Bluetooth headphones, this effect cannot be enabled when the host is wearing Bluetooth headphones. Please try to prompt the host to wear wired headphones in the user interface.

Also, please note that not all mobile phones can achieve excellent ear return effects after enabling this feature. We have blocked this effect for phones with poor ear return performance.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enable</td>

<td rowspan="1" colSpan="1" >YES: On; NO: Off.</td>
</tr>
</table>


> **Note**
> 

> This effect can only be enabled when the host is wearing headphones. Please also prompt the host to wear wired headphones.
> 


## setVoiceEarMonitorVolume:



#### Set ear return volume

Through this interface, you can set the volume of the sound in the ear return effect.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >volume</td>

<td rowspan="1" colSpan="1" >Volume. Value range: 0 - 100. Default value: 100.</td>
</tr>
</table>


> **Note**
> 

> If you still feel the volume is too low after setting it to 100, you can set the maximum volume to 150. However, a volume above 100 carries a risk of pop noise, so proceed with caution.
> 


## setVoiceReverbType:



#### Set vocal reverb effect

Through this interface, you can set the vocal reverb effect. For specific effects, please refer to the enumeration Definition [TXVoiceReverbType](https://write.woa.com/document/87029789200396288).

> **Note**
> 

> The set effect will automatically become invalid after leaving the room. If the corresponding effect is needed next time you enter the room, you need to call this interface to set it again.
> 


## setVoiceChangerType:



#### Set vocal voice changing effect

Through this interface, you can set the voice changing effect. For specific effects, please refer to the enumeration Definition [TXVoiceChangeType](https://write.woa.com/document/87029789200396288).

> **Note**
> 

> The set effect will automatically become invalid after leaving the room. If the corresponding effect is needed next time you enter the room, you need to call this interface to set it again.
> 


## setVoiceVolume:



#### Set speech volume

This interface allows you to set the voice volume. It is generally used in conjunction with the music volume setting interface [setAllMusicVolume](https://write.woa.com/document/87029789200396288), to balance the respective volumes of voice and music before mixing.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >volume</td>

<td rowspan="1" colSpan="1" >Volume. Value range: 0-100. Default value: 100.</td>
</tr>
</table>


> **Note**
> 

> If you still feel the volume is too low after setting it to 100, you can set the maximum volume to 150. However, a volume above 100 carries a risk of pop noise, so proceed with caution.
> 


## setVoicePitch:



#### Set speech tone

This interface can set the voice pitch, achieving pitch change without speed variation.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >pitch</td>

<td rowspan="1" colSpan="1" >Pitch, value range: -1.0f to 1.0f, default value: 0.0f.</td>
</tr>
</table>


## startPlayMusic:onStart:onProgress:onComplete:



#### Start playing background music

Each piece of music requires a specific ID. With this ID, you can control the start, stop, volume, etc., of the music.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >completeBlock</td>

<td rowspan="1" colSpan="1" >Play end callback.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >musicParam</td>

<td rowspan="1" colSpan="1" >Music parameters.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >progressBlock</td>

<td rowspan="1" colSpan="1" >Playback progress callback.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >startBlock</td>

<td rowspan="1" colSpan="1" >Playback start callback.</td>
</tr>
</table>


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
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >id</td>

<td rowspan="1" colSpan="1" >Music ID.</td>
</tr>
</table>


## pausePlayMusic:



#### Pause background music
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >id</td>

<td rowspan="1" colSpan="1" >Music ID.</td>
</tr>
</table>


## resumePlayMusic:



#### Resume background music
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >id</td>

<td rowspan="1" colSpan="1" >Music ID.</td>
</tr>
</table>


## setAllMusicVolume:



#### Set the local and remote volume of all background music

This interface allows you to set both the local and remote volume of all background music.
-  Local Volume: The volume of background music that the host can hear locally.

-  Remote Volume: The volume of background music that the audience can hear.

<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >volume</td>

<td rowspan="1" colSpan="1" >Volume range, value range is 0-100, default value: 60.</td>
</tr>
</table>


> **Note**
> 

> If you still feel the volume is too low after setting it to 100, you can set the maximum volume to 150. However, a volume above 100 carries a risk of pop noise, so proceed with caution.
> 


## setMusicPublishVolume:volume:



#### Set the remote volume of a specific background music track

This interface can finely control the remote volume for each background music track, which is the volume the audience can hear.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >id</td>

<td rowspan="1" colSpan="1" >Music ID.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >volume</td>

<td rowspan="1" colSpan="1" >Volume range, value range is 0-100; default value: 60.</td>
</tr>
</table>


> **Note**
> 

> If you still feel the volume is too low after setting it to 100, you can set the maximum volume to 150. However, a volume above 100 carries a risk of pop noise, so proceed with caution.
> 


## setMusicPlayoutVolume:volume:



#### Set the local volume of a specific background music track

This interface can finely control the local volume for each background music track, which is the volume the host can hear locally.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >id</td>

<td rowspan="1" colSpan="1" >Music ID.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >volume</td>

<td rowspan="1" colSpan="1" >Volume range, value range is 0-100, default value: 60.</td>
</tr>
</table>


> **Note**
> 

> If you still feel the volume is too low after setting it to 100, you can set the maximum volume to 150. However, a volume above 100 carries a risk of pop noise, so proceed with caution.
> 


## setMusicPitch:pitch:



#### Adjust the pitch of background music
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >id</td>

<td rowspan="1" colSpan="1" >Music ID.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >pitch</td>

<td rowspan="1" colSpan="1" >Pitch, default value is 0.0f, value range is a floating point between [-1 ~ 1].</td>
</tr>
</table>


## setMusicSpeedRate:speedRate:



#### Adjust the variable speed effect of background music
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >id</td>

<td rowspan="1" colSpan="1" >Music ID.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >speedRate</td>

<td rowspan="1" colSpan="1" >Speed, default value is 1.0f, value range is a floating point between [0.5 ~ 2].</td>
</tr>
</table>


## getMusicCurrentPosInMS:



#### Get the playback progress of background music (unit: milliseconds)
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >id</td>

<td rowspan="1" colSpan="1" >Music ID.</td>
</tr>
</table>


#### Return value description:

On success, returns current playback time in milliseconds, on failure returns -1.

## getMusicDurationInMS:



#### Get the total duration of background music (unit: milliseconds)
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >path</td>

<td rowspan="1" colSpan="1" >Music file path.</td>
</tr>
</table>


#### Return value description:

On success, returns duration, on failure returns -1.

## seekMusicToPosInMS:pts:



#### Set the playback progress of background music (unit: milliseconds)
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >id</td>

<td rowspan="1" colSpan="1" >Music ID.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >pts</td>

<td rowspan="1" colSpan="1" >Unit: milliseconds.</td>
</tr>
</table>


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
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >id</td>

<td rowspan="1" colSpan="1" >Music ID.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >scratchSpeedRate</td>

<td rowspan="1" colSpan="1" >Scratching speed, the default value is 1.0f, the range is a floating point number between [-12.0 ~ 12.0], the positive/negative value represents the forward/reverse direction, and the absolute value represents the speed.</td>
</tr>
</table>


> **Note**
> 

> Precondition: preloadMusic is successful.
> 


## preloadMusic:onProgress:onError:



#### Preload background music

Each piece of music requires a specific ID. With this ID, you can control the start, stop, volume, etc., of the music.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >preloadParam</td>

<td rowspan="1" colSpan="1" >Preload music parameters.</td>
</tr>
</table>


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
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >id</td>

<td rowspan="1" colSpan="1" >Music ID.</td>
</tr>
</table>


## setMusicTrack:track:



#### Specify the playback track of background music
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >id</td>

<td rowspan="1" colSpan="1" >Music ID.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >index</td>

<td rowspan="1" colSpan="1" >By default, the first audio track is played. The range of values is [0, total number of tracks).</td>
</tr>
</table>


> **Note**
> 

> The total number of tracks can be obtained through the getMusicTrackCount interface.
> 


## TXVoiceReverbType



#### Reverb effects

Reverb effects can be applied to vocals, using acoustic algorithms to overlap the sound and simulate various immersive experiences in different environments. Currently, the following reverb effects are supported:

0:Off; 1:KTV; 2:Small Room; 3:Hall; 4:Deep; 5:Loud; 6:Metallic; 7:Magnetic; 8:Ethereal; 9:Studio; 10:Melodious; 11:Studio2.
<table>
<tr>
<td rowspan="1" colSpan="1" >Enumeration</td>

<td rowspan="1" colSpan="1" >Value</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXVoiceReverbType_0</td>

<td rowspan="1" colSpan="1" >0</td>

<td rowspan="1" colSpan="1" >Turn off effects</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXVoiceReverbType_1</td>

<td rowspan="1" colSpan="1" >1</td>

<td rowspan="1" colSpan="1" >KTV</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXVoiceReverbType_2</td>

<td rowspan="1" colSpan="1" >2</td>

<td rowspan="1" colSpan="1" >Small Room</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXVoiceReverbType_3</td>

<td rowspan="1" colSpan="1" >3</td>

<td rowspan="1" colSpan="1" >Hall</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXVoiceReverbType_4</td>

<td rowspan="1" colSpan="1" >4</td>

<td rowspan="1" colSpan="1" >Low-pitched</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXVoiceReverbType_5</td>

<td rowspan="1" colSpan="1" >5</td>

<td rowspan="1" colSpan="1" >Loud</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXVoiceReverbType_6</td>

<td rowspan="1" colSpan="1" >6</td>

<td rowspan="1" colSpan="1" >Metallic sound</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXVoiceReverbType_7</td>

<td rowspan="1" colSpan="1" >7</td>

<td rowspan="1" colSpan="1" >Magnetic</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXVoiceReverbType_8</td>

<td rowspan="1" colSpan="1" >8</td>

<td rowspan="1" colSpan="1" >Ethereal voice</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXVoiceReverbType_9</td>

<td rowspan="1" colSpan="1" >9</td>

<td rowspan="1" colSpan="1" >Recording studio</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXVoiceReverbType_10</td>

<td rowspan="1" colSpan="1" >10</td>

<td rowspan="1" colSpan="1" >Melodious</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXVoiceReverbType_11</td>

<td rowspan="1" colSpan="1" >11</td>

<td rowspan="1" colSpan="1" >Recording studio 2</td>
</tr>
</table>


## TXVoiceChangeType



#### Voice changing effects

Voice changing effect can be applied to vocals. By using acoustic algorithms for secondary processing, the voice can acquire a different sound quality from the original. Currently, the following voice changing effects are supported:

0: Off; 1: Naughty kid; 2: Lolita; 3: Uncle; 4: Heavy metal; 5: Cold; 6: Foreign accent; 7: Trapped beast; 8: Fat nerd; 9: Strong current; 10: Heavy machinery; 11: Ethereal.
<table>
<tr>
<td rowspan="1" colSpan="1" >Enumeration</td>

<td rowspan="1" colSpan="1" >Value</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXVoiceChangeType_0</td>

<td rowspan="1" colSpan="1" >0</td>

<td rowspan="1" colSpan="1" >Off</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXVoiceChangeType_1</td>

<td rowspan="1" colSpan="1" >1</td>

<td rowspan="1" colSpan="1" >Naughty kid</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXVoiceChangeType_2</td>

<td rowspan="1" colSpan="1" >2</td>

<td rowspan="1" colSpan="1" >Lolita</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXVoiceChangeType_3</td>

<td rowspan="1" colSpan="1" >3</td>

<td rowspan="1" colSpan="1" >Uncle</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXVoiceChangeType_4</td>

<td rowspan="1" colSpan="1" >4</td>

<td rowspan="1" colSpan="1" >Heavy metal</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXVoiceChangeType_5</td>

<td rowspan="1" colSpan="1" >5</td>

<td rowspan="1" colSpan="1" >Cold</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXVoiceChangeType_6</td>

<td rowspan="1" colSpan="1" >6</td>

<td rowspan="1" colSpan="1" >Foreign accent</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXVoiceChangeType_7</td>

<td rowspan="1" colSpan="1" >7</td>

<td rowspan="1" colSpan="1" >Trapped beast</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXVoiceChangeType_8</td>

<td rowspan="1" colSpan="1" >8</td>

<td rowspan="1" colSpan="1" >Otaku</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXVoiceChangeType_9</td>

<td rowspan="1" colSpan="1" >9</td>

<td rowspan="1" colSpan="1" >Strong electric current</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXVoiceChangeType_10</td>

<td rowspan="1" colSpan="1" >10</td>

<td rowspan="1" colSpan="1" >Heavy Machinery</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXVoiceChangeType_11</td>

<td rowspan="1" colSpan="1" >11</td>

<td rowspan="1" colSpan="1" >Ethereal voice</td>
</tr>
</table>


## TXAudioMusicParam



#### Playback control information for background music

This information is used to specify background music details in the interface [startPlayMusic](https://write.woa.com/document/87029789200396288), including play ID, file path, loop count, etc.:

1. If you need to play the same background music multiple times, do not assign a new ID each time. We recommend using the same ID.

2. If you want to play different pieces of music simultaneously, assign different IDs for each piece.

3. If you use the same ID to play different music, the SDK will stop the old music before playing the new one.
<table>
<tr>
<td rowspan="1" colSpan="1" >Enumeration Types</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ID</td>

<td rowspan="1" colSpan="1" >[Field Meaning] Music ID.<br>[Special Instructions] The SDK allows playing multiple music tracks simultaneously, so IDs are needed to control start, stop, volume, etc.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >endTimeMS</td>

<td rowspan="1" colSpan="1" >[Field Meaning] Music play end time, in milliseconds. 0 means play until the end of the file.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >isShortFile</td>

<td rowspan="1" colSpan="1" >[Field Meaning] Whether the played file is a short music file.<br>[Recommended Value] YES: short music file that needs to be played repeatedly; NO: normal music file. Default: NO.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >loopCount</td>

<td rowspan="1" colSpan="1" >[Field Meaning] The number of times the music loops.<br>[Recommended Value] Value range is 0 to any positive integer. Default: 0. 0 means play the music once; 1 means play the music twice; and so on.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >path</td>

<td rowspan="1" colSpan="1" >[Field Meaning] The full path or URL of the audio file. Supported audio formats include MP3, AAC, M4A, WAV.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >publish</td>

<td rowspan="1" colSpan="1" >[Field Meaning] Whether to transmit the music to the remote end.<br>[Recommended Value] YES: The music is played locally and is also heard by remote users; NO: The host hears the music locally, but remote audience cannot. Default: NO.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >startTimeMS</td>

<td rowspan="1" colSpan="1" >[Field Meaning] Music start time, in milliseconds.</td>
</tr>
</table>
