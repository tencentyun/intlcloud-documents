## Basic Features

| Feature | Description | Common Use Cases | 
|------|------|------|
| Video call | TRTC supports one-to-one or multi-person 720p and 1080p HD video calls. There can be a maximum of 300 members in a single room, and up to 50 of them (only 20 for the Web app) can enable their cameras at the same time. | One-to-one video call, video conferencing with up to 300 attendees, online medical diagnosis, video chat, video customer service, video interview, audiovisual recording, online insurance claim settlement, video werewolf, etc. |
| Audio call | TRTC supports 48 kHz dual-channel one-to-one or multi-person audio calls. There can be a maximum of 300 members in a single room, and up to 50 of them (only 20 for the Web app) can enable their mics at the same time. | One-to-one audio call, multi-person audio call, voice chat, audio conferencing, audio customer service, audio werewolf, etc. | 
| Interactive live video streaming | <li>Video co-anchoring between anchors and viewers is supported.</li><li>Cross-room anchor competition is supported.</li><li>Mic can be turned on/off smoothly without waiting for switchover, and the anchor latency is as low as less than 300 ms.</li><li>The number of co-anchoring members in a single room is unlimited, and up to 50 members can co-anchor at the same time.</li><li>Low-latency live streaming supports 100,000 concurrent viewers with the playback latency down to 1,000 ms.</li><li>CDN relayed live streaming has no limit on the number of viewers.</li> | Low-latency live video streaming, interactive classroom for up to 100,000 participants, live video anchor competition, video dating room, remote training, large-scale conferencing, etc. | 
| Interactive live audio streaming | <li>Audio co-anchoring between anchors and viewers is supported.</li><li>Cross-room anchor competition is supported.</li><li>Mic can be turned on/off smoothly without waiting for switchover, and the anchor latency is as low as less than 300 ms.</li><li>The number of co-anchoring members in a single room is unlimited, and up to 50 members can co-anchor at the same time.</li><li>Low-latency live streaming supports 100,000 concurrent viewers with the playback latency down to 1,000 ms.</li><li>CDN relayed live streaming has no limit on the number of viewers.</li> | Low-latency live audio streaming, live audio co-anchoring, live audio anchor competition, audio chat room, voice dating room, karaoke room, FM radio, etc. | 


## Advanced Features

| Feature | Description | Common Use Cases | 
|------|------|------|
|High audio quality|<li>High audio quality at 48 kHz sampling rate is supported.</li><li>Stereo audio with authentic left/right sound channels is supported, which is comparable to the sound effect of CDs.</li>|Audio call, video call, interactive live streaming, audio chat room, high-quality FM radio, music class, karaoke room, online classroom, etc.|
|High image quality|720p and 1080p HD videos are supported.|Video call, interactive live streaming, online classroom, etc.|
|Co-anchoring|Co-anchoring is supported. Viewers can mic on/off smoothly as needed without waiting for switchover.|Interactive live streaming, online classroom, chat room, etc.| 
|Cross-room competition|It is also called "cross-room anchor competition", where viewers can watch multiple anchors compete across rooms.|Live show streaming, co-anchoring competition, cross-room teaching, etc.| 
|Screen sharing|A local desktop, window, or desktop area can be displayed to others; for example, slides presented in Microsoft PowerPoint can be shared to others.| Online classroom, slide sharing, remote assistance, etc.| 
|Local server recording|(Audio/video) recording on a local server is supported. To try this feature out, please [contact us](https://intl.cloud.tencent.com/contact-sales) to get the SDKs and relevant guide.|Audiovisual recording, archiving, compliance, etc.| 
|3A processing |The industry-leading TRAE audio engine is used for 3A processing, namely, acoustic echo cancellation (AEC), active noise suppression, (ANS), and automatic gain control (AGC), in order to render better sound quality in scenarios such as double-talk and noise reduction.|All audio scenarios.|
|Basic beauty filters|Basic beauty filters are supported, such as skin brightening, skin smoothing, and rosy skin filters.|Video call, interactive live streaming, online classroom, etc.|
| Background music |Local music files in formats such as MP3, AAC, and WAV can be used as background music for human voice. |Audio call, video call, interactive live streaming, online classroom, audio chat room, karaoke room, FM radio, etc. |
| Sound effect | Sound effects such as handclaps, cheers, whistles, and boos can be added during a call. | Audio call, video call, interactive live streaming, audio chat room, karaoke room, FM radio, etc.| 
|Harmony and accompaniment|Music played back locally such as songs in QQ Music can be shared to other users.|Interactive live streaming, online classroom, audio chat room, FM radio, etc.|
|Voice changing|Voice changing effects such as little girl, middle-aged man, and heavy metal are provided.|Audio call, video call, interactive live streaming, audio chat room, karaoke room, FM radio, etc.|
|Reverb|Reverb effects such as karaoke room, small room, concert hall, and bathroom are provided.|Audio call, video call, interactive live streaming, audio chat room, karaoke room, FM radio, etc.|
|Volume level callback|Volume level can be called back for display as a waveform or prompt.|Audio call, video call, audio chat room, FM radio, karaoke room, human voice detection, etc.|
|In-ear monitoring|Recorded local sound can be played back in the local earphone, so that users can hear their own voice to correct a slip of the tongue or identify the pitch.|Interactive live streaming, live show streaming, karaoke room, etc.|
|Custom audio data|Audio can be collected for callback, so that raw audio data can be processed for custom operations such as connecting to non-standard devices and processing audio files.|Non-standard device connection, custom audio effect, speech processing, speech recognition, etc.|
|Custom video data|Custom video sources and renderers are supported. Non-camera video sources such as video files, external devices, and third-party custom data sources can be used.|Custom beauty filter, custom data source, multi-device management, video recognition, image processing, etc.|
|SEI information|Custom information such as lyrics and questions can be embedded as SEI frames into video streams to sync such information to other users.|Karaoke room, live Q&A, interactive live video broadcasting, etc.|


## Extended Features
>Extended features are value-added features provided by TRTC in collaboration with other Tencent Cloud services and charged by the corresponding Tencent Cloud services according to their respective billing rules.


| Feature | Description | Common Use Cases | 
|------|------|------|
|CDN LVB watching|Also known as "CDN relayed live streaming". UDP audio and video streams in TRTC are converted to RTMP streams by the relayed transcoding clusters in Tencent Cloud, and then are pushed to the standard LVB system and distributed via CDN to viewers.|Interactive live streaming, live sharing, large-scale conferencing, watch by remote viewers in live streaming, etc.|
|On-cloud recording| On-cloud (audio/video) recording features based on [LVB](https://intl.cloud.tencent.com/document/product/267) are provided through relayed push during the entire live streaming process. Recording files can be stored in the [VOD](https://intl.cloud.tencent.com/document/product/266) platform to ensure recording reliability and real-timeliness.|Audiovisual recording, archiving, compliance, etc.|
|IM| <li>Users can chat, review, send on-screen comments, give gifts, give likes, and perform other operations in one-to-one chat rooms, group chat rooms, and chat rooms with unlimited number of users offered by IM.</li><li>IM can be used for signaling interaction to make calls and collect statistics on the number of users in a room, and perform other operations.</li>|Online customer service, interactive live streaming, interactive classroom, remote training, etc.|
