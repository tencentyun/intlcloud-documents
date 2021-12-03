This document describes the basic concepts involved in the VOD playback scenarios of Tencent Cloud RT-Cube Player (Player) to help you quickly understand and use its VOD capabilities.

[](id:basicConception)
## Concepts
Player can be connected to Tencent Cloud VOD through Superplayer or Superplayer Adapter.

### Superplayer
Superplayer is a standalone and complete video player with a full range of video playback features, such as video encryption, thumbnail preview, and definition switch. It comes with complete UIs and demos, is deeply integrated with VOD, and can play back resources in VOD by their `FileId`. In addition, it provides a full-linkage VOD playback quality data service. To quickly connect Superplayer, see [Superplayer Guide](https://intl.cloud.tencent.com/document/product/266/38098).


### Superplayer Adapter
Superplayer Adapter is a player plugin used to connect a third-party player with resources in VOD. It offers diverse capabilities, including video playback and encryption, so you can integrate it into your third-party players to play back resources in VOD by their `FileId`. To quickly connect Superplayer Adapter, see the integration documents for different platforms.


[](id:choosePlayer)
## How to Select Player
To simplify connection and match your business scenarios, we recommend you select the most suitable player type when connecting the player service.
![](https://qcloudimg.tencent-cloud.cn/raw/f793f98980f8f0adb38ee4292ed10d67.png)

- **Superplayer**: suitable for users who haven't integrated a player but need to quickly build VOD playback capabilities. Player is fully featured and easy to connect. VOD provides a detailed [guide](https://intl.cloud.tencent.com/document/product/266/38098) on how to connect it through Superplayer.
- **Superplayer Adapter**: suitable for users who need to play back resources in VOD with a proprietary or third-party player. VOD offers Superplayer Adapter to help you smoothly connect and use resources in VOD.

Platforms supported by Player include:

| Player Type     | Superplayer | Superplayer Adapter |
| --------- | ----- | ------------- |
| Web      | &#10003     | &#10003             |
| iOS      | &#10003     | &#10003             |
| Android | &#10003     | &#10003             |
| Flutter  | &#10003     | \-            |
| UI        | &#10003     | \-            |
| Demo      | &#10003     | \-            |


