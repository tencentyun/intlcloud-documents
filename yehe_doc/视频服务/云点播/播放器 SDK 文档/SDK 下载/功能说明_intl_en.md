[](id:functionList)
## Superplayer
Superplayer provides rich capabilities for connection to various platforms as listed below:

| Feature         | Description                                               | iOS and Android | Web |
| ----------- | -------------------------------------------------- | ------------- | --- |
| Multiple formats        | A rich set of audio/video formats such as RTMP, FLV, HLS, MP4, and WebRTC are supported               | &#10003             | &#10003   |
| Playback through URL | Online videos can be played back at URLs | &#10003 | &#10003 |
| DASH protocol     | Videos in standard DASH format are supported                                  | ×             | &#10003   |
| Playback through `FileId`   | Videos can be played back through their `FileId` in VOD                               | &#10003             | &#10003   |
| Instant broadcasting and preloading of the first frame     | Videos can be preloaded with the first frame broadcast instantly                                | &#10003             | &#10003   |
| Quick seeking     | The specified position can be quickly and accurately located to play back the video image there                               | &#10003             | &#10003   |
| H.265 hardware decoding | Playback based on hardware decoding is supported for H.265 videos | &#10003 | &#10003 |
| Automatic switch between software and hardware decoding | If the device does not support hardware decoding, software decoding will be automatically used | &#10003 | &#10003   |
| Adaptive bitrate streaming       | If an HLS adaptive bitstream is played back, the bitrate can be manually specified or automatically selected according to the network bandwidth for playback            | &#10003             | &#10003   |
| Definition switch       | Multiple definitions can be smoothly switched between with no lags                                 | &#10003             | &#10003   |
| Definition naming       | Names can be customized for different definitions                                   | &#10003             | &#10003   |
| Playback control        | Playback control features such as start, end, pause, automatic playback, looped playback, checkpoint restart, and replay are supported                | &#10003             | &#10003   |
| Adjustable-Speed playback        | Videos can be played back at any speed between 0.5 time and 2 times, and the audio tone will stay the same even if the speed changes                      | &#10003             | &#10003   |
| Custom playback start time     | The time when to start the playback of a video is customizable                                     | &#10003             | &#10003   |
| Preview        | Videos with preview enabled can be played back                                      | &#10003             | &#10003   |
| Progress bar operation       | The indicator on the progress bar can be dragged to seek the video                                          | &#10003             | &#10003   |
| Progress bar marking and thumbnail preview | Markers can be added to the progress bar, and thumbnail (sprite) preview is supported                        | &#10003             | &#10003   |
| Player size       | The player size can be customized                                       | &#10003             | &#10003   |
| Screen filling/fitting      | Different display modes can be selected for the video image to match the screen size                             | &#10003             | &#10003   |
| Small window playback        | Videos can be played back in a small window                                          | &#10003             | &#10003   |
| Video mirroring | The video image can be mirrored horizontally or vertically | &#10003 | &#10003 |
| Video rotation        | The video image can be rotated at the specified angle or automatically according to the `rotate` parameter in the video file          | &#10003             | ×   |
| Brightness adjustment        | The system brightness can be adjusted during video playback                                      | &#10003             | \-  |
| Volume adjustment        | The system volume can be adjusted or muted during video playback                                 | &#10003             | &#10003   |
| Dual-Channel audio       | Dual-Channel audios can be played back                                          | &#10003             | &#10003   |
| Pure audio playback | Pure audio playback is supported for MP3 and other files | &#10003| &#10003|
| Screen lock        | Screen lock features are supported, including rotation lock and UI element hiding                               | &#10003             | \-  |
| On-screen commenting          | Comments can be displayed above the video                                        | &#10003             | &#10003   |
| Roll image        | A roll image can be added for ad display when the video is paused                                 | &#10003             | &#10003   |
| Video screencapturing        | Any frame of the video can be captured                                      | &#10003             | ×   |
| Subtitles import        | Custom subtitles files can be imported                                        | &#10003             | &#10003   |
| Thumbnail configuration        | The thumbnail of the video to be played back can be set                                        | &#10003             | &#10003   |
| Multi-Instance         | Multiple players can be added on the same page for concurrent playback                                 | &#10003             | &#10003   |
| Buffering | When a video is played back, its rest content can be downloaded and buffered at the same time | &#10003 | &#10003 |
| Referer hotlink protection | The source of a playback request can be identified through the `Referer` field in the request, so as to control the request sources through a blocklist or allowlist | &#10003             | &#10003   |
| Key hotlink protection     | Control parameters can be added in the playback URL, so as to control the URL validity period, preview duration, number of IPs allowed for playback, etc.          | &#10003             | &#10003   |
| HLS encryption      | Video data can be encrypted with a key and HLS-based AES encryption scheme       | &#10003             | &#10003   |
| Proprietary protocol encryption      | Videos can be encrypted over proprietary protocols in the cloud, and the encrypted videos can be decrypted only through the player SDK for playback     | &#10003             | &#10003   |
| Offline download        | Encrypted videos downloaded offline can be decrypted only through the player SDK for playback                 | &#10003             | \-  |
| Playback callback        | The playback status, first frame, and playback completion or failure can be called back                           | &#10003             | &#10003   |
| Support for HTTPS | HTTPS video resources can be played back | &#10003 | &#10003 |
| Custom HTTP header | HTTP headers in video resource requests are customizable | &#10003 | \-  |

[](id:Adapter)
## Superplayer Adapter
Superplayer Adapter provides rich capabilities for connection to various platforms as listed below:

| Feature      | Description                                         | iOS and Android | Web |
| -------- | -------------------------------------------- | ----------- | --- |
| QUIC protocol   | The QUIC protocol is supported                                     | ×           | &#10003   |
| Playback by `FileId`   | Videos can be played back by their `FileId` in VOD                               | &#10003             | &#10003   |
| Definition switch       | Multiple definitions can be smoothly switched between with no lags                                 | &#10003             | &#10003   |
| Definition naming       | Names can be customized for different definitions                                   | &#10003             | &#10003   |
| Progress bar marking | Markers can be added to the progress bar                        | &#10003             | &#10003   |
| Thumbnail preview | Thumbnails (sprites) can be displayed on the progress bar for preview | &#10003 | &#10003 |
| Thumbnail configuration        | The thumbnail of the video to be played back can be set                                        | &#10003             | &#10003   |
| HLS encryption      | Video data can be encrypted with a key and HLS-based AES encryption scheme       | &#10003             | &#10003   |
| Proprietary protocol encryption      | Videos can be encrypted over proprietary protocols in the cloud, and the encrypted videos can be decrypted only through the player SDK for playback     | &#10003             | &#10003   |
