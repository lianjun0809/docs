> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

# TRTC Real-Time Communication (TRTC SDK) Documentation
## Feature Overview
`TXAudioEffectManager.java` is the manager class for handling background music, sound effects, and vocal effects on the TRTC Real-Time Communication (TRTC SDK) Android platform. Use this class to configure and control background music, sound effects, and vocal processing features.


## TXMusicPreloadObserver
<table>
<tr>
<td rowspan="1" colSpan="1" >Function List</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onLoadProgress](https://write.woa.com/document/87029952305344512)</td>

<td rowspan="1" colSpan="1" >Background music preloading progress</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onLoadError](https://write.woa.com/document/87029952305344512)</td>

<td rowspan="1" colSpan="1" >Error in background music preloading</td>
</tr>
</table>


## TXMusicPlayObserver
<table>
<tr>
<td rowspan="1" colSpan="1" >Function List</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onStart](https://write.woa.com/document/87029952305344512)</td>

<td rowspan="1" colSpan="1" >Start playing background music</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onPlayProgress](https://write.woa.com/document/87029952305344512)</td>

<td rowspan="1" colSpan="1" >Background music playback progress</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[onComplete](https://write.woa.com/document/87029952305344512)</td>

<td rowspan="1" colSpan="1" >Background music playback completed</td>
</tr>
</table>


## TXAudioEffectManager
<table>
<tr>
<td rowspan="1" colSpan="1" >Function List</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[enableVoiceEarMonitor](https://write.woa.com/document/87029952305344512)</td>

<td rowspan="1" colSpan="1" >Enable ear return</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setVoiceEarMonitorVolume](https://write.woa.com/document/87029952305344512)</td>

<td rowspan="1" colSpan="1" >Set ear return volume</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setVoiceReverbType](https://write.woa.com/document/87029952305344512)</td>

<td rowspan="1" colSpan="1" >Set vocal reverb effect</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setVoiceChangerType](https://write.woa.com/document/87029952305344512)</td>

<td rowspan="1" colSpan="1" >Set vocal voice changing effect</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setVoiceCaptureVolume](https://write.woa.com/document/87029952305344512)</td>

<td rowspan="1" colSpan="1" >Set speech volume</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setVoicePitch](https://write.woa.com/document/87029952305344512)</td>

<td rowspan="1" colSpan="1" >Set speech tone</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setMusicObserver](https://write.woa.com/document/87029952305344512)</td>

<td rowspan="1" colSpan="1" >Set the event callback interface for background music</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[startPlayMusic](https://write.woa.com/document/87029952305344512)</td>

<td rowspan="1" colSpan="1" >Start playing background music</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[stopPlayMusic](https://write.woa.com/document/87029952305344512)</td>

<td rowspan="1" colSpan="1" >Stop playing background music</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[pausePlayMusic](https://write.woa.com/document/87029952305344512)</td>

<td rowspan="1" colSpan="1" >Pause background music</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[resumePlayMusic](https://write.woa.com/document/87029952305344512)</td>

<td rowspan="1" colSpan="1" >Resume background music</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setAllMusicVolume](https://write.woa.com/document/87029952305344512)</td>

<td rowspan="1" colSpan="1" >Set the local and remote volume of all background music</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setMusicPublishVolume](https://write.woa.com/document/87029952305344512)</td>

<td rowspan="1" colSpan="1" >Set the remote volume of a specific background music track</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setMusicPlayoutVolume](https://write.woa.com/document/87029952305344512)</td>

<td rowspan="1" colSpan="1" >Set the local volume of a specific background music track</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setMusicPitch](https://write.woa.com/document/87029952305344512)</td>

<td rowspan="1" colSpan="1" >Adjust the pitch of background music</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setMusicSpeedRate](https://write.woa.com/document/87029952305344512)</td>

<td rowspan="1" colSpan="1" >Adjust the variable speed effect of background music</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getMusicCurrentPosInMS](https://write.woa.com/document/87029952305344512)</td>

<td rowspan="1" colSpan="1" >Get the playback progress of background music (unit: milliseconds)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getMusicDurationInMS](https://write.woa.com/document/87029952305344512)</td>

<td rowspan="1" colSpan="1" >Get the total duration of background music (unit: milliseconds)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[seekMusicToPosInMS](https://write.woa.com/document/87029952305344512)</td>

<td rowspan="1" colSpan="1" >Set the playback progress of background music (unit: milliseconds)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setMusicScratchSpeedRate](https://write.woa.com/document/87029952305344512)</td>

<td rowspan="1" colSpan="1" >Adjust the variable speed effect of scratching</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setPreloadObserver](https://write.woa.com/document/87029952305344512)</td>

<td rowspan="1" colSpan="1" >Set the preloading event callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[preloadMusic](https://write.woa.com/document/87029952305344512)</td>

<td rowspan="1" colSpan="1" >Preload background music</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[getMusicTrackCount](https://write.woa.com/document/87029952305344512)</td>

<td rowspan="1" colSpan="1" >Obtain the number of background music tracks</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[setMusicTrack](https://write.woa.com/document/87029952305344512)</td>

<td rowspan="1" colSpan="1" >Specify the playback track of background music</td>
</tr>
</table>


## Struct Type
<table>
<tr>
<td rowspan="1" colSpan="1" >Function List</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[AudioMusicParam](https://write.woa.com/document/87029952305344512)</td>

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
<td rowspan="1" colSpan="1" >[TXVoiceReverbType](https://write.woa.com/document/87029952305344512)</td>

<td rowspan="1" colSpan="1" >Reverb effects</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[TXVoiceChangerType](https://write.woa.com/document/87029952305344512)</td>

<td rowspan="1" colSpan="1" >Voice changing effects</td>
</tr>
</table>


## onLoadProgress



#### Background music preloading progress

## onLoadError



#### Error in background music preloading
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >errorCode</td>

<td rowspan="1" colSpan="1" >-4001: Failed to open file due to invalid audio data or FFmpeg protocol not found, etc.; -4002: Decoding failed due to corrupted audio file or inaccessible network audio file server, etc.; -4003: Preloading quantity exceeds the limit. Please call stopPlayMusic to release unused preloads first; -4005: Failed to open file due to invalid path. Please check if your path parameter points to a valid music file; -4006: Failed to open file due to illegal URL. Please check if the URL provided can download the expected music file using a browser; -4007: Failed to open file due to no audio stream. Please confirm if the file you provided is a legal audio file and whether it is damaged; -4008: Failed to open file due to unsupported format. Please confirm if the file format you provided is supported. Supported formats on mobile are [mp3, aac, m4a, wav, ogg, mp4, mkv], and supported formats on desktop are [mp3, aac, m4a, wav, mp4, mkv].</td>
</tr>
</table>


## onStart



#### Start playing background music

Called when background music starts playing successfully or fails to play.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >errCode</td>

<td rowspan="1" colSpan="1" >Error Code. 0: Play started successfully; -4001: Failed to open file, such as invalid audio data, FFMPEG protocol not found, etc.; -4005: Invalid path, check if the provided path points to a valid music file; -4006: Invalid URL, check in the browser if the provided URL can download the expected music file; -4007: No audio stream, confirm if the provided file is a valid audio file and is not corrupted; -4008: Unsupported format, verify if the provided file is in a supported format. Mobile supports [mp3, aac, m4a, wav, ogg, mp4, mkv], desktop supports [mp3, aac, m4a, wav, mp4, mkv].</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >id</td>

<td rowspan="1" colSpan="1" >Music ID.</td>
</tr>
</table>


## onPlayProgress



#### Background music playback progress

## onComplete



#### Background music playback completed

Called when background music finishes playing or encounters an error.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >errCode</td>

<td rowspan="1" colSpan="1" >Error Code. 0: Play ended; -4002: Decoding failed, such as corrupted audio file, or unreachable network audio file server.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >id</td>

<td rowspan="1" colSpan="1" >Music ID.</td>
</tr>
</table>


## enableVoiceEarMonitor



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

<td rowspan="1" colSpan="1" >true: on; false: off.</td>
</tr>
</table>


> **Note**
> 

> This effect can only be enabled when the host is wearing headphones. Please also prompt the host to wear wired headphones.
> 


## setVoiceEarMonitorVolume



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


## setVoiceReverbType



#### Set vocal reverb effect

Through this interface, you can set the vocal reverb effect. For specific effects, please refer to the enumeration Definition [TXVoiceReverbType](https://write.woa.com/document/87029952305344512).

> **Note**
> 

> The set effect will automatically become invalid after leaving the room. If the corresponding effect is needed next time you enter the room, you need to call this interface to set it again.
> 


## setVoiceChangerType



#### Set vocal voice changing effect

Through this interface, you can set the voice changing effect. For specific effects, please refer to the enumeration Definition [TXVoiceChangeType](https://write.woa.com/document/87029952305344512).

> **Note**
> 

> The set effect will automatically become invalid after leaving the room. If the corresponding effect is needed next time you enter the room, you need to call this interface to set it again.
> 


## setVoiceCaptureVolume



#### Set speech volume

This interface allows you to set the voice volume. It is generally used in conjunction with the music volume setting interface [setAllMusicVolume](https://write.woa.com/document/87029952305344512), to balance the respective volumes of voice and music before mixing.
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


## setVoicePitch



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


## setMusicObserver



#### Set the event callback interface for background music

Ensure to set the playback event callback using this API before playing the background music. This allows to be aware of the background music's playback progress.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >musicId</td>

<td rowspan="1" colSpan="1" >Music ID.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >observer</td>

<td rowspan="1" colSpan="1" >Refer to ITXMusicPlayObserver Definition interface for details.</td>
</tr>
</table>


> **Note**
> 

> 1. If the ID does not need to be used, the observer can be set to NULL to completely release it.
> 


## startPlayMusic



#### Start playing background music

Each piece of music requires a specific ID. With this ID, you can control the start, stop, volume, etc., of the music.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >musicParam</td>

<td rowspan="1" colSpan="1" >Music parameters.</td>
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


## stopPlayMusic



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


## pausePlayMusic



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


## resumePlayMusic



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


## setAllMusicVolume



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


## setMusicPublishVolume



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


## setMusicPlayoutVolume



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


## setMusicPitch



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


## setMusicSpeedRate



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


## getMusicCurrentPosInMS



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

## getMusicDurationInMS



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

## seekMusicToPosInMS



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


## setMusicScratchSpeedRate



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


## setPreloadObserver



#### Set the preloading event callback

Set the callback using this API before preloading background music to monitor the preload progress.
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >observer</td>

<td rowspan="1" colSpan="1" >Refer to ITXMusicPreloadObserver Definition interface for details.</td>
</tr>
</table>


## preloadMusic



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


## getMusicTrackCount



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


## setMusicTrack



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
<td rowspan="1" colSpan="1" >TXLiveVoiceReverbType_0</td>

<td rowspan="1" colSpan="1" >0</td>

<td rowspan="1" colSpan="1" >Turn off effects</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXLiveVoiceReverbType_1</td>

<td rowspan="1" colSpan="1" >1</td>

<td rowspan="1" colSpan="1" >KTV</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXLiveVoiceReverbType_2</td>

<td rowspan="1" colSpan="1" >2</td>

<td rowspan="1" colSpan="1" >Small Room</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXLiveVoiceReverbType_3</td>

<td rowspan="1" colSpan="1" >3</td>

<td rowspan="1" colSpan="1" >Hall</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXLiveVoiceReverbType_4</td>

<td rowspan="1" colSpan="1" >4</td>

<td rowspan="1" colSpan="1" >Low-pitched</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXLiveVoiceReverbType_5</td>

<td rowspan="1" colSpan="1" >5</td>

<td rowspan="1" colSpan="1" >Loud</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXLiveVoiceReverbType_6</td>

<td rowspan="1" colSpan="1" >6</td>

<td rowspan="1" colSpan="1" >Metallic sound</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXLiveVoiceReverbType_7</td>

<td rowspan="1" colSpan="1" >7</td>

<td rowspan="1" colSpan="1" >Magnetic</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXLiveVoiceReverbType_8</td>

<td rowspan="1" colSpan="1" >8</td>

<td rowspan="1" colSpan="1" >Ethereal voice</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXLiveVoiceReverbType_9</td>

<td rowspan="1" colSpan="1" >9</td>

<td rowspan="1" colSpan="1" >Recording studio</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXLiveVoiceReverbType_10</td>

<td rowspan="1" colSpan="1" >10</td>

<td rowspan="1" colSpan="1" >Melodious</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXLiveVoiceReverbType_11</td>

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
<td rowspan="1" colSpan="1" >TXLiveVoiceChangerType_0</td>

<td rowspan="1" colSpan="1" >0</td>

<td rowspan="1" colSpan="1" >Off</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXLiveVoiceChangerType_1</td>

<td rowspan="1" colSpan="1" >1</td>

<td rowspan="1" colSpan="1" >Naughty kid</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXLiveVoiceChangerType_2</td>

<td rowspan="1" colSpan="1" >2</td>

<td rowspan="1" colSpan="1" >Lolita</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXLiveVoiceChangerType_3</td>

<td rowspan="1" colSpan="1" >3</td>

<td rowspan="1" colSpan="1" >Uncle</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXLiveVoiceChangerType_4</td>

<td rowspan="1" colSpan="1" >4</td>

<td rowspan="1" colSpan="1" >Heavy metal</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXLiveVoiceChangerType_5</td>

<td rowspan="1" colSpan="1" >5</td>

<td rowspan="1" colSpan="1" >Cold</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXLiveVoiceChangerType_6</td>

<td rowspan="1" colSpan="1" >6</td>

<td rowspan="1" colSpan="1" >Foreign accent</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXLiveVoiceChangerType_7</td>

<td rowspan="1" colSpan="1" >7</td>

<td rowspan="1" colSpan="1" >Trapped beast</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXLiveVoiceChangerType_8</td>

<td rowspan="1" colSpan="1" >8</td>

<td rowspan="1" colSpan="1" >Otaku</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXLiveVoiceChangerType_9</td>

<td rowspan="1" colSpan="1" >9</td>

<td rowspan="1" colSpan="1" >Strong electric current</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXLiveVoiceChangerType_10</td>

<td rowspan="1" colSpan="1" >10</td>

<td rowspan="1" colSpan="1" >Heavy Machinery</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >TXLiveVoiceChangerType_11</td>

<td rowspan="1" colSpan="1" >11</td>

<td rowspan="1" colSpan="1" >Ethereal voice</td>
</tr>
</table>


## TXAudioMusicParam



#### Playback control information for background music

This information is used to specify background music details in the interface [startPlayMusic](https://write.woa.com/document/87029952305344512), including play ID, file path, loop count, etc.:

1. If you need to play the same background music multiple times, do not assign a new ID each time. We recommend using the same ID.

2. If you want to play different pieces of music simultaneously, assign different IDs for each piece.

3. If you use the same ID to play different music, the SDK will stop the old music before playing the new one.
<table>
<tr>
<td rowspan="1" colSpan="1" >Enumeration Types</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >endTimeMS</td>

<td rowspan="1" colSpan="1" >[Field Meaning] Music play end time, in milliseconds. 0 means play until the end of the file.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >id</td>

<td rowspan="1" colSpan="1" >[Field Meaning] Music ID.<br>[Special Instructions] The SDK allows playing multiple music tracks simultaneously, so IDs are needed to control start, stop, volume, etc.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >isShortFile</td>

<td rowspan="1" colSpan="1" >[Field Meaning] Whether the played file is a short music file.<br>[Recommended Value] true: Requires repeating short music file; false: Normal music file. Default: false.</td>
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

<td rowspan="1" colSpan="1" >[Field Meaning] Whether to transmit the music to the remote end.<br>[Recommended Value] true: Music can be heard by remote users while playing locally; false: Only the host can hear the music locally, remote audience cannot hear it. Default: false.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >startTimeMS</td>

<td rowspan="1" colSpan="1" >[Field Meaning] Music start time, in milliseconds.</td>
</tr>
</table>
