> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

# TRTC Real-Time Communication (TRTC SDK) Documentation
## Overview
`TRTCStatistics.h` provides read-only statistics for TRTC Real-Time Communication (TRTC SDK) on iOS. The TRTC SDK reports real-time audio and video metrics—including frame rate, bitrate, and stutter status—every two seconds.


## Struct Type
<table>
<tr>
<td rowspan="1" colSpan="1" >Function List</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[TRTCLocalStatistics](https://write.woa.com/document/87029770633089024)</td>

<td rowspan="1" colSpan="1" >Local Audio and Video Statistics</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[TRTCRemoteStatistics](https://write.woa.com/document/87029770633089024)</td>

<td rowspan="1" colSpan="1" >Remote Audio and Video Statistics</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >[TRTCStatistics](https://write.woa.com/document/87029770633089024)</td>

<td rowspan="1" colSpan="1" >Summary Statistics of Network and Performance</td>
</tr>
</table>


## TRTCLocalStatistics



#### Local Audio and Video Statistics
<table>
<tr>
<td rowspan="1" colSpan="1" >Enumeration Types</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >audioBitrate</td>

<td rowspan="1" colSpan="1" >[Field Meaning] Local audio bitrate, that is, how much new audio data is generated per second, in Kbps.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >audioCaptureState</td>

<td rowspan="1" colSpan="1" >[Field Meaning] Audio device collection status (used to detect the health of audio peripherals).<br>0: Collection Device Status Normal; 1: Long Period of Silence Detected; 2: Crackling Sound Detected; 3: Abnormal Sound Intermittence Detected.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >audioSampleRate</td>

<td rowspan="1" colSpan="1" >[Field Meaning] Local audio sampling rate, in Hz.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >frameRate</td>

<td rowspan="1" colSpan="1" >[Field Meaning] Local video frame rate, that is, how many video frames per second, unit: FPS.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >height</td>

<td rowspan="1" colSpan="1" >[Field Meaning] Local video height, in px.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >streamType</td>

<td rowspan="1" colSpan="1" >[Field Meaning] Video stream type (HD large screen \| Low-definition Small Picture \| Auxiliary Stream Picture).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >videoBitrate</td>

<td rowspan="1" colSpan="1" >[Field Meaning] Local video bitrate, that is, how much new video data is generated per second, in Kbps.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >width</td>

<td rowspan="1" colSpan="1" >[Field Meaning] Local video width, in pixels (px).</td>
</tr>
</table>


## TRTCRemoteStatistics



#### Remote Audio and Video Statistics
<table>
<tr>
<td rowspan="1" colSpan="1" >Enumeration Types</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >audioBitrate</td>

<td rowspan="1" colSpan="1" >[Field Meaning] Local audio bitrate, in Kbps</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >audioBlockRate</td>

<td rowspan="1" colSpan="1" >[Field Meaning] Audio playback stuttering rate, in percentage (%)<br>Audio playback stuttering rate (audioBlockRate) = cumulative stuttering duration during audio playback (audioTotalBlockTime) / total duration of audio playback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >audioPacketLoss</td>

<td rowspan="1" colSpan="1" >[Field Meaning] Total audio stream packet loss rate (%).<br>audioPacketLoss represents the packet loss rate at the audience end after an audio stream completes the transmission chain from ` Broadcaster > Cloud > Audience `.<br>The smaller the audioPacketLoss, the better. A packet loss rate of 0 means all audio stream data has been completely received by the audience.<br>If downLoss == 0 but audioPacketLoss != 0 occurs, it indicates that the audio stream has no packet loss on the "cloud=>audience" segment, but there is irrecoverable packet loss on the ` host>cloud ` segment.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >audioSampleRate</td>

<td rowspan="1" colSpan="1" >[Field Meaning] Local audio sampling rate, in Hz.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >audioTotalBlockTime</td>

<td rowspan="1" colSpan="1" >[Field Meaning] Cumulative stuttering duration during audio playback, in milliseconds (ms)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >finalLoss</td>

<td rowspan="1" colSpan="1" >[Field Meaning] Overall packet loss rate of the audio and video stream (%). Deprecated; it is recommended to use audioPacketLoss and videoPacketLoss instead.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >frameRate</td>

<td rowspan="1" colSpan="1" >[Field Meaning] Remote video frame rate, in FPS.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >height</td>

<td rowspan="1" colSpan="1" >[Field Meaning] Remote video height, in pixels (px).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >jitterBufferDelay</td>

<td rowspan="1" colSpan="1" >[Field Meaning] Playback latency, in milliseconds (ms)<br>To avoid audio and screen freezing caused by network jitter and packet disorder, TRTC manages a playback buffer at the playback end to organize received network packets. The size of this buffer is adaptively adjusted based on current network quality. This buffer size is translated into a time length in milliseconds, referred to as jitterBufferDelay.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >point2PointDelay</td>

<td rowspan="1" colSpan="1" >[Field Meaning] End-to-end latency, in milliseconds (ms)<br>point2PointDelay represents the delay from "Anchors => Cloud => Audience". More precisely, it represents the full-link latency of "Collection => Encoding => Network Transmission => Receive => Buffering => Decoding => Play".<br>point2PointDelay requires both local and remote SDKs to be version 8.5 or above to be effective. If the remote user is on a version before 8.5, this value will always be 0, meaning it is not applicable.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >remoteNetworkRTT</td>

<td rowspan="1" colSpan="1" >[Field Meaning] The round-trip time from the SDK to the cloud, in milliseconds (ms)<br>This value represents the total time it takes for a network packet to travel from the SDK to the cloud and back, summing up the "SDK => Cloud => SDK" time.<br>The smaller this value, the better: if remoteNetworkRTT < 50ms, it indicates low audio and video call latency; if remoteNetworkRTT > 200ms, it suggests high audio and video call latency.<br>It is important to note that remoteNetworkRTT represents the total time for "SDK => Cloud => SDK", so there is no need to differentiate between remoteNetworkUpRTT and remoteNetworkDownRTT</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >remoteNetworkUplinkLoss</td>

<td rowspan="1" colSpan="1" >[Field Meaning] The uplink packet loss rate from the SDK to the cloud, in percentage (%)<br>The smaller the value, the better. If remoteNetworkUplinkLoss is 0%, it means the uplink network quality is good, with almost no data packet loss when uploading to the cloud.<br>If remoteNetworkUplinkLoss is 30%, it means that 30% of the audio and video data packets sent by the SDK to the cloud are lost in the transmission link.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >streamType</td>

<td rowspan="1" colSpan="1" >[Field Meaning] Video stream type (HD large screen \| Low-definition Small Picture \| Auxiliary Stream Picture).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >[Field Meaning] User ID</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >videoBitrate</td>

<td rowspan="1" colSpan="1" >[Field Meaning] Remote video bitrate, in Kbps.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >videoBlockRate</td>

<td rowspan="1" colSpan="1" >[Field Meaning] Video playback stutter rate, in percentage (%). Video playback stutter rate (videoBlockRate) = cumulative stutter duration during video playback (videoTotalBlockTime) / total duration of video playback.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >videoPacketLoss</td>

<td rowspan="1" colSpan="1" >[Field Meaning] Total packet loss rate of the video stream (%).<br>videoPacketLoss represents the packet loss rate at the audience end after the video stream completes the transmission chain from ` Anchors > Cloud > Audience `.<br>The smaller the videoPacketLoss, the better. A packet loss rate of 0 means all video stream data has been completely received by the audience.<br>If downLoss == 0 but videoPacketLoss != 0 occurs, it indicates that the video stream has no packet loss on the ` Cloud > Audience ` segment, but there is irrecoverable packet loss on the ` Anchors > Cloud ` segment.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >videoTotalBlockTime</td>

<td rowspan="1" colSpan="1" >[Field Meaning] Cumulative stutter duration during video playback, in milliseconds (ms)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >width</td>

<td rowspan="1" colSpan="1" >[Field Meaning] Remote video width, in pixels (px).</td>
</tr>
</table>


## TRTCStatistics



#### Summary Statistics of Network and Performance
<table>
<tr>
<td rowspan="1" colSpan="1" >Enumeration Types</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >appCpu</td>

<td rowspan="1" colSpan="1" >[Field Meaning] Current application CPU utilization, in percentage (%); not supported on Android 8.0 and above.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >downLoss</td>

<td rowspan="1" colSpan="1" >[Field Meaning] Downlink packet loss rate from the cloud to SDK, in percentage (%)<br>The smaller the value, the better. If downLoss is 0%, it means the downlink network quality is good, with almost no data packet loss from the cloud.<br>If downLoss is 30%, it means that 30% of the audio and video data packets transmitted from the cloud to the SDK are lost in the transmission link.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >gatewayRtt</td>

<td rowspan="1" colSpan="1" >[Field Meaning] Round-trip latency from the SDK to the local router, in milliseconds (ms). This value represents the total time it takes for a network packet to travel from the SDK to the local router gateway and back, summing up the [SDK -> Gateway -> SDK] time.<br>The smaller the value, the better. If gatewayRtt < 50ms, it means lower audio and video call latency. If gatewayRtt > 200ms, it means higher audio and video call latency.<br>This value is invalid when the network type is cellular.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >localStatistics</td>

<td rowspan="1" colSpan="1" >[Field Meaning] Local audio and video statistical information<br>Since there may be three local audio and video streams (i.e., high-definition main screen, low-definition small screen, and auxiliary screen), the local audio and video statistical information is an array.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >receivedBytes</td>

<td rowspan="1" colSpan="1" >[Field Meaning] Total received bytes (including signaling data and audio and video data), in bytes.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >remoteStatistics</td>

<td rowspan="1" colSpan="1" >[Field Meaning] Remote audio and video statistical information<br>Since there may be multiple remote users at the same time, and each remote user may simultaneously have multiple audio and video streams (i.e., high-definition main screen, low-definition small screen, and auxiliary screen), the remote audio and video statistical information is an array.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >rtt</td>

<td rowspan="1" colSpan="1" >[Field Meaning] Round-trip latency from the SDK to the cloud, in milliseconds (ms)<br>This value represents the total time it takes for a network packet to travel from the SDK to the cloud and back, summing up the "SDK => Cloud => SDK" time.<br>The smaller the value, the better: if RTT < 50ms, it means lower audio and video call latency; if RTT > 200ms, it means higher audio and video call latency.<br>It needs to be specifically explained that RTT represents the total time for "SDK => Cloud => SDK," so there is no need to distinguish between upRtt and downRtt.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >sentBytes</td>

<td rowspan="1" colSpan="1" >[Field Meaning] Total bytes sent (including signaling data and audio and video data), in bytes (Bytes).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >systemCpu</td>

<td rowspan="1" colSpan="1" >[Field Meaning] Current system CPU utilization, in percentage (%); not supported on Android 8.0 and above.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >upLoss</td>

<td rowspan="1" colSpan="1" >[Field Meaning] Uplink packet loss rate from the SDK to the cloud, in percentage (%)<br>The smaller the value, the better. If upLoss is 0%, it means the uplink network quality is good, with almost no data packet loss when uploading to the cloud.<br>If upLoss is 30%, it means that 30% of the audio and video data packets sent by the SDK to the cloud are lost in the transmission link.</td>
</tr>
</table>
