This document describes how to choose sound quality in the GME SDK.

## Overview of Sound Quality Types

| Sound Quality Type     	| Description | Parameter | Bitrate | Sample Rate | Volume Type | Applicable Scenario |
| ------------- |------------ | ---- |---- |---- |---- |---- |
| ITMG_ROOM_TYPE_FLUENCY			| Smooth	|1| 30 Kbps | 16 kHz |<li>Speaker: Call volume</li><li>Headset: Media volume</li><li>Bluetooth headset: Headset audio capturing over the HFP protocol</li>			| Smooth sound quality and ultra-low delay, which is suitable for group chat in games like FPS and MOBA games.	|
| ITMG_ROOM_TYPE_STANDARD			| Standard	| 2 | 64 Kbps | 48 kHz |<li>Speaker: Call volume</li><li>Headset: Media volume</li><li>Bluetooth headset: Headset audio capturing over the HFP protocol</li>				| Good sound quality with a moderate latency, which is suitable for voice chat in casual games such as Werewolves and board games.	|
| ITMG_ROOM_TYPE_HIGHQUALITY		| HD	| 3 |64 Kbps | 48 kHz |<li>Speaker: Media volume</li><li>Headset: Media volume</li><li>Bluetooth headset: Mobile phone audio capturing over the A2DP protocol</li>	| HD sound quality with a relatively high latency, which is suitable for music and dancing games that require high sound quality such as music playback and online karaoke.	|

<dx-alert infotype="notice" title="Note">
Currently, only the ITMG_ROOM_TYPE_FLUENCY audio quality type is provided by default. To use other audio quality types, [submit a ticket](https://www.tencentcloud.com/account/login?s_url=https%3A%2F%2Fconsole.tencentcloud.com%2Fworkorder%2Fcategory).
</dx-alert>


## Concepts
### Media volume and call volume
Two volume modes are configured in a mobile phone: Media volume and call volume. Media volume is generally used to playback media files, and call volume is used in phone calls and communications.

For an Android mobile phone, the current volume mode is displayed on the screen when you press the volume key. As shown below, the call volume is on the left and the media volume is on the right.


<img src="https://qcloudimg.tencent-cloud.cn/raw/e3418f5852fbe68affa6481b05ed96df.png"  width="10%" /></img>


<dx-fold-block title="Media volume and call volume">
Q: What should I do if the mobile phone volume level becomes very low after room entry but becomes very high after mic-on? A: Troubleshoot as instructed in [Sound and Audio](https://www.tencentcloud.com/document/product/607/39524).
</dx-fold-block>

### Bluetooth headset protocols

There are two Bluetooth headset protocols with different audio performance:


| Protocol | Playback Performance | Capturing Performance |
|---------|---------|---------|
| HFP | The headset audio is mono only. | The headset audio can be captured. |
| A2DP | The headset audio is stereo and has a better audio quality. | The headset audio cannot be directly captured through this channel, and you need to use the phone or the PC mic to capture the audio. |


### Traffic consumption

The traffic is subject to the bitrate and number of users speaking in the room. The specific calculation formula is: bitrate * number of users / 8 = number of bytes.

### Audio processing effect
The audio signal is collected by the capturing module on the mobile device, and is encoded by an audio encoder after audio preprocessing processes such as mixing cancellation, noise reduction, and automatic gain control. The methods used in the preprocessing processes, acoustic echo canceling (AEC), automatic gain control (AGC), and automatic noise suppression (ANS, also known as noise cancellation and noise suppression), are commonly known as 3A.
- The difference between smooth sound quality and the other two sound qualities is ANS (noise reduction). ANS is enabled for the smooth sound quality, and is disabled for the standard and HD sound quality.
