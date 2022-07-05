This document describes how to choose the sound quality in the GME SDK.

## Sound Quality Types


<dx-alert infotype="notice" title="Note">
For Tencent Cloud International users, only smooth sound quality (ITMG_ROOM_TYPE_FLUENCY) is available by default. Submit a ticket if you want to choose other sound qualities.
</dx-alert>



| Sound Quality | Description | Parameter | Volume Type | Applicable Scenario |
| ------------- |------------ | ---- |---- |---- |
| ITMG_ROOM_TYPE_FLUENCY | Smooth | 1 | <li>Speaker: Call volume</li><li>Headset: Media volume</li><li>Bluetooth headset: HFP protocol, headset collection</li> | Smooth sound quality with ultra-low latency, which is suitable for team voice chat in games such as FPS and MOBA. |
| ITMG_ROOM_TYPE_STANDARD| Standard |2| <li>Speaker: Call volume</li><li>Heaset: Media volume</li><li>Bluetooth headset: HFP protocol, headset collection</li> | Standard sound quality with mediate latency, which is suitable for voice chat in casual games such as Werewolves and board games. |
| ITMG_ROOM_TYPE_HIGHQUALITY | HD | 3 | <li>Speaker: Media volume</li><li>Heaset: Media volume</li><li>Bluetooth headset: a2dp protocol, headset collection</li> | HD sound quality with relative high latency, which is suitable for music and dancing games and voice chat apps that require high sound quality such as music playback and online karaoke. |


## Media Volume and Call Volume
Two volume modes are configured in a mobile phone: Media volume and call volume. Media volume is generally used to playback media files, and call volume is used in phone calls and communications.

For an Android phone, the current volume type is displayed on the screen when you press the volume key. As in the following figure, call volume is displayed on the left and media volume is on the right.



<img src="https://qcloudimg.tencent-cloud.cn/raw/e3418f5852fbe68affa6481b05ed96df.png"  width="10%" /></img>


<dx-fold-block title="Media volume and call volume">
[After I entered a room, my mobile phone volume level becomes very low, and then it becomes very high after I turned on the microphone. How to fix it?](https://www.tencentcloud.com/document/product/607/39524)
</dx-fold-block>



## Bitrate
- Smooth: sample rate: 16k, bitrate: 30 kbps
- Standard and HD: sample rate: 48k, bitrate: 64 kbps

## Traffic Consumption

For the smooth sound effect, the bitrate is 30 kbps. For the standard and HD sound effect, the bitrate is 64 kbps. The traffic consumption is calculated according to the bitrate and the number of speaking users in the room.
Formula: bitrate * number of speakers / 8 = bytes.

## Audio Processing
After being collected, the audio signal goes through the audio pre-process (such as mixing cancellation, noise reduction, and automatic gain control), and then encoded by an audio encoder. In the pre-process, Acoustic Echo Cancelling (AEC), Automatic Gain Control (AGC), Active Noise Control (ANC, also known as noise cancellation, noise suppression), are commonly known as 3A.
- ANC is enabled for the smooth sound quality, and is disabled for the standard and HD sound quality.
