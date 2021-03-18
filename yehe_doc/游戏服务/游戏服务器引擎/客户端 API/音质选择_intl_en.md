This document describes how to choose sound quality in the GME SDK.

## Overview of Sound Quality Types

| Sound Quality Type | Description | Parameter | Volume Type | Applicable Scenario |
| ------------- |------------ | ---- |---- |---- |
| ITMG_ROOM_TYPE_FLUENCY | Smooth | 1 | Speaker: call volume; headphone: media volume | Smooth sound quality with ultra-low latency, which is suitable for team voice chat in games such as FPS and MOBA. |
| ITMG_ROOM_TYPE_STANDARD | Standard | 2 |Speaker: call volume; headphone: media volume | Good sound quality with acceptable latency, which is suitable for voice chat in casual games such as Werewolf and board games. |
| ITMG_ROOM_TYPE_HIGHQUALITY | HD | 3 | Speaker: media volume; headphone: media volume | HD sound quality with relative high latency, which is suitable for music and dancing games and voice chat apps that require high sound quality such as music playback and online karaoke. |

## Bitrate
- Smooth sound quality: sample rate: 16k, bitrate: 30 kbps
- Standard and HD sound quality: sample rate: 48k, bitrate: 64 kbps

## Traffic Consumption

For the smooth sound effect, the bitrate is 30 kbps. For the standard and HD sound effect, the bitrate is 64 kbps. The traffic consumption is associated with the bitrate and the number of calling users in the room.
The specific calculation formula: bitrate * the number of users / 8 = bytes.

## Audio Processing Effect
The audio signal is collected by its mobile terminal collection module, and is encoded by an audio encoder after audio pre-processing such as mixing cancellation, noise reduction, and automatic gain control. Among them, the used methods in the pre-processing, Acoustic Echo Cancelling (AEC), Automatic Gain Control (AGC), Active Noise Control (ANC, also known as noise cancellation, noise suppression), are commonly known as 3A.
- The difference between smooth sound quality and the other two sound qualities is ANS (noise reduction). ANS is enabled for the smooth sound quality, and is disabled for the standard and HD sound quality.
