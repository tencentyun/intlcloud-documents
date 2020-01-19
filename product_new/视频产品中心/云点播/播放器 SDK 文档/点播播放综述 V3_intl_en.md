In order to meet the playback requirements in various scenarios such as [video website](https://cloud.tencent.com/document/product/266/34147), VOD provides mobile and web superplayers. You can quickly integrate them to play back videos in VOD in a very simple way.

## Restrictions

The superplayer has the following restrictions on the video and playback methods:

* Only videos in VOD but not on other platforms can be played back.
* Video must be [transcoded to adaptive bitrate streaming](https://cloud.tencent.com/document/product/266/34071) before they can be played back.
* Videos can be played back only by video ID (i.e., `FileId`) but not by video URL.

## Advantages

Compared with common third-party players, the superplayer has the following advantages:

* It offers simple encoding, where videos can be played back with only two parameters: video ID and playback template ID.
* It features adaptive bitrate streaming (HLS and Dash) to improve the playback experience.
* It supports playing back videos encrypted with commercial-grade DRM.
* It supports playing back videos with hotlink protection enabled.


## Selection

- Mobile superplayer: it provides SDKs for Android and iOS suitable for integrating the playback capabilities of VOD into mobile apps.
- Web superplayer: it is integrated into web servers for playback of VOD videos through browsers in clients (PCs and mobile devices).
