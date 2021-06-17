## Basic Features

<table>
<tr><th>Feature</th><th width="50%">Description</th><th width="35%">Common Use Cases</th><th>Billing</th>
</tr>
<tr>
<td>Video call</td>
<td><ul style="margin:0">
<li>One-to-one or group video calls, which support 720p and 1080p definitions
<li>Each room can accommodate up to 300 concurrent users, and up to 30 of them can turn on their cameras at the same time.</li>
</ul></td>
<td>One-to-one video calls, video conferences with up to 300 attendees, online medical consultation, video chat, video customer service, video interviews, audiovisual recording, online insurance claim settlement, and video Werewolf</td>
<td><a href="https://cloud.tencent.com/document/product/647/44246">Billing of video calls</a></td>
</tr>
<tr>
<td>Audio call</td>
<td><ul style="margin:0">
<li>One-to-one or group audio calls, which support the 48 kHz sample rate and dual channels.</li>
<li>Each room can accommodate up to 300 concurrent users, and up to 30 of them can keep their mics on at the same time.</li>
</ul></td>
<td>One-to-one or group audio calls, audio chat, audio conferencing, audio customer service, and audio Werewolf</td>
<td><a href="https://cloud.tencent.com/document/product/647/44226">Billing of audio calls</a></td>
</tr><tr>
<td>Interactive video live streaming</td>
<td><ul style="margin:0">
<li>Video co-anchoring between anchors and audience</li>
<li>Cross-room anchor competition</li>
<li>Smooth mic on/off without waiting; anchor latency less than 300 ms</li>
<li>No upper limit on the number of concurrent users in a room; up to 50 users can keep their mics on at the same time.</li>
<li>Live streaming to up to 100,000 concurrent users and a playback latency as low as 1,000 ms in the low-latency live streaming mode</li>
<li>No upper limit on audience size in the CDN relayed live streaming mode</li>
</ul></td>
<td>Low-latency video live streaming, interactive classrooms with up to 100,000 participants, live video competitions, video dating, remote training, large-scale conferences, etc.</td>
<td><a href="https://cloud.tencent.com/document/product/647/44247">Billing of interactive video live streaming</a></td>
</tr><tr>
<td>Interactive audio live streaming</td>
<td><ul style="margin:0">
<li>Audio co-anchoring between anchors and audience</li>
<li>Cross-room anchor competition</li>
<li>Smooth mic on/off without waiting; anchor latency less than 300 ms</li>
<li>No upper limit on the cumulative number of anchors in a room; up to 50 users can keep their mics on at the same time.</li>
<li>Live streaming to up to 100,000 concurrent users and a playback latency as low as 1,000 ms in the low-latency live streaming mode</li>
<li>No upper limit on audience size in the CDN relayed live streaming mode</li>
</ul></td>
<td>Low-latency audio live streaming, live audio co-anchoring, live audio competitions, audio chat rooms, audio dating, karaoke rooms, FM radio, etc.</td>
<td><a href="https://cloud.tencent.com/document/product/647/44248">Billing of interactive audio live streaming</a></td>
</tr></table>


## Advanced Features

| Feature           | Description                                                     | Common Use Cases                                                 | Billing                                                     |
| -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Co-anchoring |Audience-anchor interaction via co-anchoring; smooth mic on/off without waiting | Interactive live streaming, online classrooms, chat rooms, etc.| You will be charged [basic service fees](https://intl.cloud.tencent.com/document/product/647/34610) for using this feature.|
| Cross-room competition |Anchors from different rooms compete with each other while audience watch.| Live show streaming, anchor competition, cross-room teaching, etc.| You will be charged [basic service fees](https://intl.cloud.tencent.com/document/product/647/34610) for using this feature. |
|Screen sharing|Sharing the desktop, a window (e.g., a PowerPoint playback window), or a desktop section of the local user to others| Online classrooms, slide sharing, remote assistance, etc.| You will be charged [basic service fees](https://intl.cloud.tencent.com/document/product/647/34610) for using this feature. |
| On-cloud recording       | TRTC leverages the capabilities of [CSS](https://intl.cloud.tencent.com/document/product/267) and the relayed push technology to offer on-cloud (audio/video) recording throughout a call. Recording files are saved reliably and in real time in [VOD](https://intl.cloud.tencent.com/document/product/266).  | Audiovisual recording, archiving, compliance, etc.                                         | On-cloud recording is a value-added service, for which you will be charged an additional [on-cloud recording](https://intl.cloud.tencent.com/document/product/647/38385) fee. |
| Local server recording| (Audio/Video) recording on a local server. To try this feature out, [contact us](https://intl.cloud.tencent.com/support) for the SDK and instructions.| Audiovisual recording, archiving, compliance, etc.| You will be charged [basic service fees](https://intl.cloud.tencent.com/document/product/647/34610) for using this feature. |
| High audio quality |<li>High audio quality at 48 kHz sample rate</li><li>Stereo with left and right sound channels, comparable in audio quality to CDs</li>| Audio calls, video calls, interactive live streaming, audio chat rooms, high-quality FM radio, music classes, karaoke rooms, online classrooms, etc. | Free |
| High image quality | 720p and 1080p HD videos | Video calls, interactive live streaming, online classrooms, etc. | Free |
| 3A processing | TRTC uses the industry-leading Tencent Real-time Audio Engine (TRAE) for acoustic echo cancellation (AEC), active noise suppression (ANS), and automatic gain control (AGC) to deliver better audio quality when multiple people speak at the same time or in the presence of background noises. | All audio scenarios | Free |
| Basic beauty filters | Basic beauty filters such as skin brightening, skin smoothing, and rosy skin | Video calls, interactive live streaming, online classrooms, etc. | Free |
| Background music | Using local music files in the formats of MP3, AAC, WAV, and others as background music | Audio calls, video calls, interactive live streaming, online classrooms, audio chat rooms, karaoke rooms, FM radio, etc. | Free |
| Audio effects | Adding audio effects such as applauding, cheering, whistling, and booing during a call | Audio calls, video calls, interactive live streaming, audio chat rooms, karaoke rooms, FM radio, etc. | Free |
| Local background audio| Sending audio played locally, for example, the music played via QQ Music on the local user’s computer, to others | Interactive live streaming, online classrooms, audio chat rooms, FM radio, etc. | Free |
| Voice changing | Voice effects such as little girl, middle-aged man, and heavy metal | Audio calls, video calls, interactive live streaming, audio chat rooms, karaoke rooms, FM radio, etc. | Free |
| Reverb | Reverb effects such as karaoke room, small room, concert hall, and bathroom | Audio calls, video calls, interactive live streaming, audio chat rooms, karaoke rooms, FM radio, etc. | Free |
| Volume callback | Showing volume in waveform animations or via prompts | Audio calls, video calls, audio chat rooms, FM radio, karaoke rooms, voice activity detection, etc. | Free |
| In-ear monitoring | Recording local audio and playing it back in the local user’s earphone, usually for detection of speech errors or pitch control during singing | Interactive live streaming, live show streaming, karaoke rooms, etc. | Free |
| Custom audio data | Calling back raw audio for custom processing. You can connect the SDK to non-standard external devices or use audio files, etc. | Non-standard device connection, custom audio effect, speech processing, speech recognition, etc. | Free |
| Custom video data | Custom video sources and renderers. Non-camera video sources such as video files, external devices, and third-party custom data sources can be used. | Custom beauty filters, custom data sources, multi-device management, video recognition, image processing, etc. | Free |
| SEI information | Embedding custom information such as lyrics and questions as SEI frames into video streams | Karaoke rooms, live quizzes, interactive live streaming, etc. | Free |


## Extended Features

>?Extended features are value-added services provided by TRTC in collaboration with other Tencent Cloud products and are charged according to the billing standards of the corresponding products.


| Feature | Description | Common Use Cases | Billing |
| ------------ | ------------------------------------------------------------ | -------------------------------------------------- | ------------------------------------------------------------ |
| CDN live streaming | TRTC uses relaying and transcoding clusters to convert its UDP audio/video streams into RTMP streams in the cloud, which are then pushed to the standard live streaming system and distributed through CDNs to audience. | Interactive live streaming, live sharing, large-scale conferencing, live stream watching by remote audience, etc. | Relayed live streaming is a value-added service and is charged by **[CSS](https://intl.cloud.tencent.com/document/product/267)**. For more information, please see [CDN Relayed Live Streaming > Billing](https://intl.cloud.tencent.com/document/product/647/35242). |
| Instant messaging (IM) | <li>TRTC leverages the capabilities of IM, including one-to-one chat, group chat, and chat rooms with no upper limit on the number of users, to enable features such as chatting, commenting, sending on-screen comments and gifts, and giving likes.</li><li>IM can also be used for signaling-based interaction, call making, and user number counting.</li> | Online customer service, interactive live streaming, interactive classrooms, remote training, etc. | IM is a value-added service and is charged by **[IM](https://intl.cloud.tencent.com/document/product/1047)**. For more information, please see [IM > Purchase Guide > Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).|
|Speech content moderation|Detecting pornographic, politically sensitive content, etc. for content-related risk management |Business security protection, compliance, etc.|Speech content moderation is a value-added service and is charged by **Business Security Protection (BSP)**. To try it out, [contact us](https://intl.cloud.tencent.com/support) to activate the service.|
| Video content moderation| Detecting pornographic, politically sensitive content, etc. for content-related risk management| Business security protection, compliance, etc.| Video content moderation is a value-added service and is charged by [CSS](https://intl.cloud.tencent.com/document/product/267). For more information, please see [Intelligent Porn Detection](https://intl.cloud.tencent.com/document/product/267/39607). |


