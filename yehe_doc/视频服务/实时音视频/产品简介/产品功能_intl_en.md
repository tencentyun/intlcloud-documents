## Basic Features

<table>
<tr><th>Feature</th><th width="50%">Description</th><th width="35%">Common Use Cases</th>
</tr>
<tr>
<td>Video call</td>
<td><ul style="margin:0">
<li>One-to-one or one-to-many video calls, which support 720p and 1080p definitions.
<li>A single room can sustain up to 300 concurrent online users, and up to 30 of them can simultaneously enable their cameras.</li>
</ul></td>
<td>One-to-one video call, video conferencing with up to 300 attendees, online medical diagnosis, video chat, video customer service, video interview, audiovisual recording, online insurance claim settlement, and video Werewolf.</td>
</tr>
<tr>
<td>Audio call</td>
<td><ul style="margin:0">
<li>One-to-one or one-to-many audio calls, which support the 48 kHz sample rate and dual-channel.</li>
<li>A single room can sustain up to 300 concurrent online users, and up to 30 of them can simultaneously enable their mics.</li>
</ul></td>
<td>One-to-one audio call, multi-person audio call, voice chat, audio conferencing, audio customer service, and audio Werewolf.</td>
</tr><tr>
<td>Interactive video live streaming</td>
<td><ul style="margin:0">
<li>Video co-anchoring between anchors and viewers is supported.</li>
<li>Cross-room anchor competition is supported.</li>
<li>The mic can be turned on/off smoothly without waiting for switchover, and the anchor latency is as low as less than 300 ms.</li>
<li>A single room can sustain an unlimited number of users for co-anchoring, and up to 30 of them can simultaneously co-anchor.</li>
<li>Live streaming to up to 100,000 concurrent viewers is supported and the playback latency can be reduced down to 1,000 ms in the low-latency live streaming mode.</li>
<li>There can be an unlimited number of viewers in the CDN relayed live streaming mode.</li>
</ul></td>
<td>Low-latency live video broadcasting, interactive classroom for up to 100,000 participants, live video competition, video dating room, remote training, large-scale conferencing, etc.</td>
</tr><tr>
<td>Interactive audio live streaming</td>
<td><ul style="margin:0">
<li>Audio co-anchoring between anchors and viewers is supported.</li>
<li>Cross-room anchor competition is supported.</li>
<li>The mic can be turned on/off smoothly without waiting for switchover, and the anchor latency is as low as less than 300 ms.</li>
<li>A single room can sustain an unlimited number of users for co-anchoring, and up to 30 of them can simultaneously co-anchor.</li>
<li>Live streaming to up to 100,000 concurrent viewers is supported and the playback latency can be reduced down to 1,000 ms in the low-latency live streaming mode.</li>
<li>There can be an unlimited number of viewers in the CDN relayed live streaming mode.</li>
</ul></td>
<td>Low-latency live audio broadcasting, live audio co-anchoring, live audio anchor competition, voice chat room, voice dating room, karaoke room, FM radio, etc.</td>
</tr></table>

>? 20 users can simultaneously enable their cameras or mics on the web.

## Advanced Features

| Feature | Description | Common Use Cases |
| -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Co-anchoring | Co-anchoring is supported. Viewers can mic on/off smoothly as needed without waiting for switchover. | Interactive live streaming, online classroom, chat room, etc. |
| Cross-room competition | It is also called "cross-room anchor competition", where viewers can watch multiple anchors compete across rooms. | Show live streaming, co-anchoring competition, cross-room teaching, etc. |
| Screen sharing | A local desktop, window, or desktop area can be displayed to others. For example, slides presented in Microsoft PowerPoint can be shared to others. | Online classroom, slide sharing, remote assistance, etc. |
| On-cloud recording | On-cloud (audio/video) recording features based on [LVB](https://intl.cloud.tencent.com/document/product/267) are provided through relayed push during the entire live streaming process. Recording files can be stored in the [VOD](https://intl.cloud.tencent.com/document/product/266) platform to ensure recording reliability and real-time performance. | Audiovisual recording, archiving, compliance, etc. |
| Local server recording | (Audio/video) recording on a local server is supported. To try this feature out, please [contact us](https://intl.cloud.tencent.com/support) to get the SDKs and the relevant guide. | Audiovisual recording, archiving, compliance, etc. |
| High audio quality |<li>High audio quality at a 48 kHz sample rate is supported.</li><li>Stereo audio with authentic left/right sound channels is supported, which is comparable to the sound effect of CDs.</li>| Audio call, video call, interactive live streaming, voice chat room, high-quality FM radio, music class, karaoke room, online classroom, etc. |
| High image quality | 720p and 1080p HD videos are supported. | Video call, interactive live streaming, online classroom, etc. |
| 3A processing | The industry-leading TRAE audio engine is used for 3A processing, namely, acoustic echo cancellation (AEC), active noise suppression (ANS), and automatic gain control (AGC), in order to render better sound quality in scenarios such as double-talk and noise reduction. | All audio scenarios. |
| Basic beauty filters | Basic beauty filters are supported, such as skin brightening, skin smoothing, and rosy skin filters. | Video call, interactive live streaming, online classroom, etc. |
| Background music | Local music files in formats such as MP3, AAC, and WAV can be used as background music for human voice. | Audio call, video call, interactive live streaming, online classroom, voice chat room, karaoke room, FM radio, etc. |
| Sound effect | Sound effects such as handclaps, cheers, whistles, and boos can be added during a call. | Audio call, video call, interactive live streaming, voice chat room, karaoke room, FM radio, etc. |
| Harmony and accompaniment | Music played back locally such as songs in QQ Music can be shared to other users. | Interactive live streaming, online classroom, voice chat room, FM radio, etc. |
| Voice changing | Voice changing effects such as little girl, middle-aged man, and heavy metal are provided. | Audio call, video call, interactive live streaming, voice chat room, karaoke room, FM radio, etc. |
| Reverb | Reverb effects such as karaoke room, small room, concert hall, and bathroom are provided. | Audio call, video call, interactive live streaming, voice chat room, karaoke room, FM radio, etc. |
| Callback for volume level | The volume level can be called back for display as a waveform or prompt. | Audio call, video call, voice chat room, FM radio, karaoke room, human voice detection, etc. |
| In-ear monitoring | The recorded local sound can be played back in the local earphone, so that users can hear their own voice to correct a slip of the tongue or identify the pitch. | Interactive live streaming, show live streaming, karaoke room, etc. |
| Custom audio data | Audio can be collected for callback, so that raw audio data can be processed for custom operations such as connecting to non-standard devices and processing audio files. | Non-standard device connection, custom audio effect, speech processing, speech recognition, etc. |
| Custom video data | Custom video sources and renderers are supported. Non-camera video sources such as video files, external devices, and third-party custom data sources can be used. | Custom beauty filter, custom data source, multi-device management, video recognition, image processing, etc. |
| SEI information | Custom information such as lyrics and questions can be embedded as SEI frames into video streams to sync such information to other users. | Karaoke room, Q&A live streaming, interactive live streaming, etc. |


## Extended Features

>?Extended features are value-added features provided by TRTC in collaboration with other Tencent Cloud services and charged by the corresponding Tencent Cloud services according to their respective billing rules.


| Feature | Description | Common Use Cases | Billing Description |
| ------------ | ------------------------------------------------------------ | -------------------------------------------------- | ------------------------------------------------------------ |
| CDN live watching | It is also known as "CDN relayed live streaming". UDP audio and video streams in TRTC are converted to RTMP streams by the relayed transcoding clusters in Tencent Cloud, and then are pushed to the standard LVB system and distributed through CDN to viewers. | Interactive live streaming, live sharing, large-scale conferencing, watch by remote viewers in live streaming, etc. | It is a value-added service and charged by **[LVB](https://intl.cloud.tencent.com/document/product/267)**. For more information, please see “Applicable Fees” in [CDN Relayed Live Streaming](https://intl.cloud.tencent.com/document/product/647/35242). |
| IM | <li>Users can chat, review, send on-screen comments, give gifts, give likes, and perform other operations in one-to-one chat rooms, group chat rooms, and chat rooms with unlimited numbers of users offered by IM.</li><li>IM can be used for signaling interaction to make calls and collect statistics on the number of users in a room, and perform other operations.</li> | Online customer service, interactive live streaming, interactive classroom, remote training, etc. | It is a value-added service and charged by **[Instant Messaging](https://intl.cloud.tencent.com/document/product/1047)**. For more information, please see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).|
