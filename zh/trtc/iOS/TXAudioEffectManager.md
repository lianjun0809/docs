> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

# 腾讯云实时音视频(TRTC SDK )文档

## 概述
`TXAudioEffectManager.h` 是腾讯云实时音视频(TRTC SDK ) iOS 平台的背景音乐、短音效和人声特效的管理类文档，用于对背景音乐、短音效和人声特效进行设置的管理类。

## TXAudioEffectManager
| 函数列表 | 描述 |
| --- | --- |
| enableVoiceEarMonitor: | 开启耳返。 |
| setVoiceEarMonitorVolume: | 设置耳返音量。 |
| setVoiceReverbType: | 设置人声的混响效果。 |
| setVoiceChangerType: | 设置人声的变声特效。 |
| setVoiceVolume: | 设置语音音量。 |
| setVoicePitch: | 设置语音音调。 |
| startPlayMusic:onStart:onProgress:onComplete: | 开始播放背景音乐。 |
| stopPlayMusic: | 停止播放背景音乐。 |
| pausePlayMusic: | 暂停播放背景音乐。 |
| resumePlayMusic: | 恢复播放背景音乐。 |
| setAllMusicVolume: | 设置所有背景音乐的本地音量和远端音量的大小。 |
| setMusicPublishVolume:volume: | 设置某一首背景音乐的远端音量的大小。 |
| setMusicPlayoutVolume:volume: | 设置某一首背景音乐的本地音量的大小。 |
| setMusicPitch:pitch: | 调整背景音乐的音调高低。 |
| setMusicSpeedRate:speedRate: | 调整背景音乐的变速效果。 |
| getMusicCurrentPosInMS: | 获取背景音乐的播放进度（单位：毫秒）。 |
| getMusicDurationInMS: | 获取背景音乐的总时长（单位：毫秒）。 |
| seekMusicToPosInMS:pts: | 设置背景音乐的播放进度（单位：毫秒）。 |
| setMusicScratchSpeedRate:speedRate: | 调整搓碟的变速效果。 |
| preloadMusic:onProgress:onError: | 预加载背景音乐。 |
| getMusicTrackCount: | 获取背景音乐的音轨数量。 |
| setMusicTrack:track: | 指定背景音乐的播放音轨。 |

## 结构体类型
| 函数列表 | 描述 |
| --- | --- |
| TXAudioMusicParam | 背景音乐的播放控制信息 |

## 枚举类型
| 枚举类型 | 描述 |
| --- | --- |
| TXVoiceReverbType | 混响特效 |
| TXVoiceChangeType | 变声特效 |

## enableVoiceEarMonitor:

#### 开启耳返。

主播开启耳返后，可以在耳机里听到麦克风采集到的自己发出的声音，该特效适用于主播唱歌的应用场景中。

需要您注意的是，由于蓝牙耳机的硬件延迟非常高，所以在主播佩戴蓝牙耳机时无法开启此特效，请尽量在用户界面上提示主播佩戴有线耳机。

同时也需要注意，并非所有的手机开启此特效后都能达到优秀的耳返效果，我们已经对部分耳返效果不佳的手机屏蔽了该特效。
| 参数 | 描述 |
| --- | --- |
| enable | YES：开启；NO：关闭。 |

> **注意**
> 

> 仅在主播佩戴耳机时才能开启此特效，同时请您提示主播佩戴有线耳机。
> 

## setVoiceEarMonitorVolume:

#### 设置耳返音量。

通过该接口您可以设置耳返特效中声音的音量大小。
| 参数 | 描述 |
| --- | --- |
| volume | 音量大小，取值范围为 [0, 150]，默认值：100。 |

> **注意**
> 

> 耳返的音量大小是影响用户耳返体验的重要因素之一，考虑到不同用户对音量的敏感度不同，强烈建议您在 UI 界面上开放耳返音量的调节滑杆，调节范围建议在 0~150 之间，其中 100~150 的增益效果对于部分采集音量较小的 Android 手机很有帮助。
> 

## setVoiceReverbType:

#### 设置人声的混响效果。

通过该接口您可以设置人声的混响效果，具体特效请参见枚举定义 TXVoiceReverbType。

> **注意**
> 

> 设置的效果在退出房间后会自动失效，如果下次进房还需要对应特效，需要调用此接口再次进行设置。
> 

## setVoiceChangerType:

#### 设置人声的变声特效。

通过该接口您可以设置人声的变声特效，具体特效请参见枚举定义 TXVoiceChangeType。

> **注意**
> 

> 设置的效果在退出房间后会自动失效，如果下次进房还需要对应特效，需要调用此接口再次进行设置。
> 

## setVoiceVolume:

#### 设置语音音量。

该接口可以设置语音音量的大小，一般配合音乐音量的设置接口 setAllMusicVolume 协同使用，用于调谐语音和音乐在混音前各自的音量占比。
| 参数 | 描述 |
| --- | --- |
| volume | 音量大小，取值范围为 [0 - 150]，默认值：100。 |

> **注意**
> 

> 如果将 volume 设置成 100 之后感觉音量还是太小，可以将 volume 最大设置成 150，但超过 100 的 volume 会有爆音的风险，请谨慎操作。
> 

## setVoicePitch:

#### 设置语音音调。

该接口可以设置语音音调，用于实现变调不变速的目的。
| 参数 | 描述 |
| --- | --- |
| pitch | 音调，取值范围[-1.0f, 1.0f]，默认值：0.0f。 |

## startPlayMusic:onStart:onProgress:onComplete:

#### 开始播放背景音乐。

每个音乐都需要您指定具体的 ID，您可以通过该 ID 对音乐的开始、停止、音量等进行设置。
| 参数 | 描述 |
| --- | --- |
| completeBlock | 播放结束回调。 |
| musicParam | 音乐参数。 |
| progressBlock | 播放进度回调。 |
| startBlock | 播放开始回调。 |

> **注意**
> 

> 1. 如果要多次播放同一首背景音乐，请不要每次播放都分配一个新的 ID，我们推荐使用相同的 ID。
> 

> 2. 若您希望同时播放多首不同的音乐，请为不同的音乐分配不同的 ID 进行播放。
> 

> 3. 如果使用同一个 ID 播放不同音乐，SDK 会先停止播放旧的音乐，再播放新的音乐。
> 

## stopPlayMusic:

#### 停止播放背景音乐。
| 参数 | 描述 |
| --- | --- |
| id | 音乐 ID。 |

## pausePlayMusic:

#### 暂停播放背景音乐。
| 参数 | 描述 |
| --- | --- |
| id | 音乐 ID。 |

## resumePlayMusic:

#### 恢复播放背景音乐。
| 参数 | 描述 |
| --- | --- |
| id | 音乐 ID。 |

## setAllMusicVolume:

#### 设置所有背景音乐的本地音量和远端音量的大小。

该接口可以设置所有背景音乐的本地音量和远端音量。
-  本地音量：即主播本地可以听到的背景音乐的音量大小。

-  远端音量：即观众端可以听到的背景音乐的音量大小。

| 参数 | 描述 |
| --- | --- |
| volume | 音量大小，取值范围为 [0, 150]，默认值：60。 |

> **注意**
> 

> 如果将 volume 设置成 100 之后感觉音量还是太小，可以将 volume 最大设置成 150，但超过 100 的 volume 会有爆音的风险，请谨慎操作。
> 

## setMusicPublishVolume:volume:

#### 设置某一首背景音乐的远端音量的大小。

该接口可以细粒度地控制每一首背景音乐的远端音量，也就是观众端可听到的背景音乐的音量大小。
| 参数 | 描述 |
| --- | --- |
| id | 音乐 ID。 |
| volume | 音量大小，取值范围为 [0, 150]；默认值：60。 |

> **注意**
> 

> 如果将 volume 设置成 100 之后感觉音量还是太小，可以将 volume 最大设置成 150，但超过 100 的 volume 会有爆音的风险，请谨慎操作。
> 

## setMusicPlayoutVolume:volume:

#### 设置某一首背景音乐的本地音量的大小。

该接口可以细粒度地控制每一首背景音乐的本地音量，也就是主播本地可以听到的背景音乐的音量大小。
| 参数 | 描述 |
| --- | --- |
| id | 音乐 ID。 |
| volume | 音量大小，取值范围为 [0, 150]，默认值：60。 |

> **注意**
> 

> 如果将 volume 设置成 100 之后感觉音量还是太小，可以将 volume 最大设置成 150，但超过 100 的 volume 会有爆音的风险，请谨慎操作。
> 

## setMusicPitch:pitch:

#### 调整背景音乐的音调高低。
| 参数 | 描述 |
| --- | --- |
| id | 音乐 ID。 |
| pitch | 音调，取值范围为 [-1.0f, 1.0f] 之间的浮点数，默认值：0.0f。 |

## setMusicSpeedRate:speedRate:

#### 调整背景音乐的变速效果。
| 参数 | 描述 |
| --- | --- |
| id | 音乐 ID。 |
| speedRate | 速度，取值范围为 [0.5f, 2.0f] 之间的浮点数，默认值：1.0f。 |

## getMusicCurrentPosInMS:

#### 获取背景音乐的播放进度（单位：毫秒）。
| 参数 | 描述 |
| --- | --- |
| id | 音乐 ID。 |

#### 返回值说明：

成功返回当前播放时间，单位：毫秒，失败返回 -1。

## getMusicDurationInMS:

#### 获取背景音乐的总时长（单位：毫秒）。
| 参数 | 描述 |
| --- | --- |
| path | 音乐文件路径。 |

#### 返回值说明：

成功返回时长，失败返回 -1。

## seekMusicToPosInMS:pts:

#### 设置背景音乐的播放进度（单位：毫秒）。
| 参数 | 描述 |
| --- | --- |
| id | 音乐 ID。 |
| pts | 单位: 毫秒。 |

> **注意**
> 

> 请尽量避免过度频繁地调用该接口，因为该接口可能会再次读写音乐文件，耗时稍高。
> 

> 因此，当用户拖拽音乐的播放进度条时，请在用户完成拖拽操作后再调用本接口。
> 

> 因为 UI 上的进度条控件往往会以很高的频率反馈用户的拖拽进度，如不做频率限制，会导致较差的用户体验。
> 

## setMusicScratchSpeedRate:speedRate:

#### 调整搓碟的变速效果。
| 参数 | 描述 |
| --- | --- |
| id | 音乐 ID。 |
| scratchSpeedRate | 搓碟速度，取值范围为 [-12.0, 12.0] 之间的浮点数，默认值是 1.0f，速度值正/负表示方向正/反，绝对值大小表示速度快慢。 |

> **注意**
> 

> 前置条件 preloadMusic 成功。
> 

## preloadMusic:onProgress:onError:

#### 预加载背景音乐。

每个音乐都需要您指定具体的 ID，您可以通过该 ID 对音乐的开始、停止、音量等进行设置。
| 参数 | 描述 |
| --- | --- |
| preloadParam | 预加载音乐参数。 |

> **注意**
> 

> 1. 预先加载最多同时支持2个不同 ID 的预加载，且预加载时长不超过10分钟，使用完需调用 stopPlayMusic，否则内存不释放。
> 

> 2. 若该ID对应的音乐正在播放中，预加载会失败，需先调用 stopPlayMusic。
> 

> 3. 当 ` musicParam ` 和传入 startPlayMusic 的 ` musicParam ` 完全相同时，预加载有效。
> 

## getMusicTrackCount:

#### 获取背景音乐的音轨数量。
| 参数 | 描述 |
| --- | --- |
| id | 音乐 ID。 |

## setMusicTrack:track:

#### 指定背景音乐的播放音轨。
| 参数 | 描述 |
| --- | --- |
| id | 音乐 ID。 |
| index | 默认播放第一个音轨。取值范围0, 音轨总数)。 |

> **注意**
> 

> 音轨总数量可通过 getMusicTrackCount 接口获取。
> 

## TXVoiceReverbType

#### 混响特效

混响特效可以作用于人声之上，通过声学算法对声音进行叠加处理，模拟出各种不同环境下的临场感受，目前支持如下几种混响效果：

0：关闭；1：KTV；2：小房间；3：大会堂；4：低沉；5：洪亮；6：金属声；7：磁性；8：空灵；9：录音棚；10：悠扬 11：录音棚2。
| 枚举 | 取值 | 描述 |
| --- | --- | --- |
| TXVoiceReverbType_0 | 0 | 关闭特效 |
| TXVoiceReverbType_1 | 1 | KTV |
| TXVoiceReverbType_2 | 2 | 小房间 |
| TXVoiceReverbType_3 | 3 | 大会堂 |
| TXVoiceReverbType_4 | 4 | 低沉 |
| TXVoiceReverbType_5 | 5 | 洪亮 |
| TXVoiceReverbType_6 | 6 | 金属声 |
| TXVoiceReverbType_7 | 7 | 磁性 |
| TXVoiceReverbType_8 | 8 | 空灵 |
| TXVoiceReverbType_9 | 9 | 录音棚 |
| TXVoiceReverbType_10 | 10 | 悠扬 |
| TXVoiceReverbType_11 | 11 | 录音棚2 |

## TXVoiceChangeType

#### 变声特效

变声特效可以作用于人声之上，通过声学算法对人声进行二次处理，以获得与原始声音所不同的音色，目前支持如下几种变声特效：

0：关闭；1：熊孩子；2：萝莉；3：大叔；4：重金属；5：感冒；6：外语腔；7：困兽；8：肥宅；9：强电流；10：重机械；11：空灵；12：猪八戒；13：绿巨人。
| 枚举 | 取值 | 描述 |
| --- | --- | --- |
| TXVoiceChangeType_0 | 0 | 关闭 |
| TXVoiceChangeType_1 | 1 | 熊孩子 |
| TXVoiceChangeType_2 | 2 | 萝莉 |
| TXVoiceChangeType_3 | 3 | 大叔 |
| TXVoiceChangeType_4 | 4 | 重金属 |
| TXVoiceChangeType_5 | 5 | 感冒 |
| TXVoiceChangeType_6 | 6 | 外语腔 |
| TXVoiceChangeType_7 | 7 | 困兽 |
| TXVoiceChangeType_8 | 8 | 肥宅 |
| TXVoiceChangeType_9 | 9 | 强电流 |
| TXVoiceChangeType_10 | 10 | 重机械 |
| TXVoiceChangeType_11 | 11 | 空灵 |
| TXVoiceChangeType_12 | 12 | 猪八戒 |
| TXVoiceChangeType_13 | 13 | 绿巨人 |

## TXAudioMusicParam

#### 背景音乐的播放控制信息

该信息用于在接口 [startPlayMusic 中指定背景音乐的相关信息，包括播放 ID、文件路径和循环次数等：

1. 如果要多次播放同一首背景音乐，请不要每次播放都分配一个新的 ID，我们推荐使用相同的 ID。

2. 若您希望同时播放多首不同的音乐，请为不同的音乐分配不同的 ID 进行播放。

3. 如果使用同一个 ID 播放不同音乐，SDK 会先停止播放旧的音乐，再播放新的音乐。
| 枚举类型 | 描述 |
| --- | --- |
| ID | 【字段含义】音乐 ID。 【特殊说明】SDK 允许播放多路音乐，因此需要使用 ID 进行标记，用于控制音乐的开始、停止、音量等。 |
| endTimeMS | 【字段含义】音乐结束播放时间点，单位毫秒，0表示播放至文件结尾。 |
| isShortFile | 【字段含义】播放的是否为短音乐文件。 【推荐取值】YES：需要重复播放的短音乐文件；NO：正常的音乐文件。默认值：NO。 |
| loopCount | 【字段含义】音乐循环播放的次数。 【推荐取值】取值范围为 [0, 任意正整数]，默认值：0。0 表示播放音乐一次；1 表示播放音乐两次；以此类推。 |
| path | 【字段含义】音效文件的完整路径或 URL 地址。支持的音频格式包括 MP3、AAC、M4A、WAV。 |
| publish | 【字段含义】是否将音乐传到远端。 【推荐取值】YES：音乐在本地播放的同时，远端用户也能听到该音乐；NO：主播只能在本地听到该音乐，远端观众听不到。默认值：NO。 |
| startTimeMS | 【字段含义】音乐开始播放时间点，单位：毫秒。 |
