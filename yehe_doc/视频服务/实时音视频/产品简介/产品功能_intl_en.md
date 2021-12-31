## Basic Features

<table>
<tr><th>Feature</th><th width="50%">Description</th><th width="35%">Common Use Cases</th><th>Billing</th>
</tr>
<tr>
<td>Video call</td>
<td><ul style="margin:0">
<li>One-to-one or group video calls, which support 720p and 1080p definitions
<li>Each room allows up to 300 concurrent users, and up to 50 of them can turn their cameras on at the same time.</li>
</ul></td>
<td>One-to-one video calls, video conferences with up to 300 attendees, online medical consultation, video chat, video customer service, video interviews, audiovisual recording, online insurance claim settlement, and video Werewolf</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/39788">Billing of Video Calls</a></td>
</tr>
<tr>
<td>Audio call</td>
<td><ul style="margin:0">
<li>One-to-one or group audio calls, which support 48 kHz sampling and dual channels</li>
<li>Each room allows up to 300 concurrent users, and up to 50 of them can keep their mics on at the same time.</li>
</ul></td>
<td>One-to-one or group audio calls, audio chat, audio conferencing, audio customer service, and audio Werewolf</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/39787">Billing of Audio Calls</a></td>
</tr><tr>
<td>Interactive video streaming</td>
<td><ul style="margin:0">
<li>Video co-anchoring between anchors and audience</li>
<li>Cross-room anchor competition</li>
<li>Smooth mic on/off without waiting; anchor latency less than 300 ms</li>
<li>No upper limit on the cumulative number of co-anchoring users in a room; up to 50 users can keep their mics on at the same time.</li>
<li>Live streaming to up to 100,000 concurrent users and a playback latency as low as 1,000 ms in the low-latency live streaming mode</li>
<li>No upper limit on audience size in the CDN relayed live streaming mode</li>
</ul></td>
<td>Low-latency video live streaming, interactive classrooms with up to 100,000 participants, live video competitions, video dating, remote training, large-scale conferences, etc.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/39786">Billing of Interactive Live Video Streaming</a></td>
</tr><tr>
<td>Interactive audio streaming</td>
<td><ul style="margin:0">
<li>Audio co-anchoring between anchors and audience</li>
<li>Cross-room anchor competition</li>
<li>Smooth mic on/off without waiting; anchor latency less than 300 ms</li>
<li>No upper limit on the cumulative number of co-anchoring users in a room; up to 50 users can keep their mics on at the same time.</li>
<li>Live streaming to up to 100,000 concurrent users and a playback latency as low as 1,000 ms in the low-latency live streaming mode</li>
<li>No upper limit on audience size in the CDN relayed live streaming mode</li>
</ul></td>
<td>Low-latency audio live streaming, live audio co-anchoring, live audio competitions, audio chat rooms, audio dating, karaoke rooms, FM radio, etc.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/39785">Billing of Interactive Live Audio Streaming</a></td>
</tr></table>


## Advanced Features
<table>
<tr><th width=15%>Feature</th><th width=40%>Description</th><th width=25%>Common Use Cases</th><th width=25%>Billing</th></tr>
<tr>
<td>Co-anchoring</td>
<td>Audience can mic on and off smoothly as needed without waiting.</td>
<td>Interactive live streaming, online class, chat room, etc.</td>
<td>You will be charged <a href="https://intl.cloud.tencent.com/document/product/647/34610">basic service fees</a> for using the co-anchoring feature.</td>
</tr><tr>
<td>Cross-room competition</td>
<td>Anchors from different rooms can compete with each other while audience watch.</td>
<td>Showroom, competition, cross-room class, etc.</td>
<td>You will be charged <a href="https://intl.cloud.tencent.com/document/product/647/34610">basic service fees</a> for using the cross-room competition feature.</td>
</tr><tr>
<td>Screen sharing</td>
<td>Sharing your desktop, a window (e.g., a Microsoft PowerPoint window), or a portion of your desktop</td>
<td>Online class, slideshow sharing, remote assistance, etc.</td>
<td>You will be charged <a href="https://intl.cloud.tencent.com/document/product/647/34610">basic service fees</a> for using the screen sharing feature.</td>
</tr><tr>
<td>Server-side local recording</td>
<td>Server-side recording relies on the SDK for Linux, which is not commercially available yet. If you have questions about the SDK or want to use it, please contact us at colleenyu@tencent.com.</td>
<td>Audiovisual recording, archiving, compliance, etc.</td>
<td>You will be charged <a href="https://intl.cloud.tencent.com/document/product/647/34610">basic service fees</a> for using the server-side local recording feature.</td>
</tr><tr>
<td>On-cloud recording</td>
<td> TRTC leverages the capabilities of <a href="https://intl.cloud.tencent.com/document/product/267">CSS</a> to allow you to record entire live streaming sessions (audio/video) through relayed push and save the recording files securely and in real time in <a href="https://intl.cloud.tencent.com/document/product/266">VOD</a>.</td>
<td> Audiovisual recording, archiving, compliance, etc.</td>
<td>On-cloud recording is a value-added service, for which you will be charged additional <a href="https://intl.cloud.tencent.com/document/product/647/38385">on-cloud recording fees</a>.</td>
</tr><tr>
<td>On-Cloud MixTranscoding</td>
<td>TRTC uses an MCU cluster to mix and transcode the audio and video streams in a room and publishes the mixtranscoded stream to CSS for on-cloud recording or CDN playback.</td>
<td>Stream mixing, recording format conversion, etc.</td>
<td>On-Cloud MixTranscoding is a value-added service, for which you will be charged additional <a href="https://intl.cloud.tencent.com/document/product/647/38929">On-Cloud MixTranscoding fees</a>.</td>
</tr><tr>
<td>High audio quality</td>
<td><li>48 kHz sample rate</li><li>Stereo audio with quality comparable to that of CDs</li></td>
<td>Audio call, video call, interactive live streaming, audio chat room, high-audio-quality FM radio, music class, karaoke, online class, etc.</td>
<td>Free</td>
</tr><tr>
<td>High video quality</td>
<td>720p/1080p HD video</td>
<td>Video call, interactive live streaming, online class, etc.</td>
<td>Free</td>
</tr><tr>
<td>3A processing</td>
<td>Leveraging the industry-leading 3A (acoustic echo cancellation, active noise suppression, automatic gain control) technologies of Tencent Ethereal Audio Lab, TRTC can ensure audio quality even when multiple people speak at the same time or in the presence of background noises.</td>
<td>All audio scenarios</td>
<td>Free</td>
</tr><tr>
<td>AI-based noise suppression</td>
<td>Removing inconstant noises that traditional noise suppression technologies cannot handle, such as cough, sneeze, and car horn</td>
<td>Audio call, video call, interactive live streaming, audio chat room, online class, etc.</td>
<td><a href="https://intl.cloud.tencent.com/apply/p/9q0qt0bg5l4">Apply for beta testing</a></td>
</tr><tr>
<td>Basic beauty filters</td>
<td>Basic beautification features, including skin brightening, skin smoothing, rosy skin, and basic filters</td>
<td>Video call, interactive live streaming, online class, etc.</td>
<td>Free</td>
</tr><tr>
<td>Background music</td>
<td>Using local music files in formats such as MP3, AAC, and WAV as background music</td>
<td>Audio call, video call, interactive live streaming, online class, audio chat room, karaoke, FM radio, etc.</td>
<td>Free</td>
</tr><tr>
<td>Audio effects</td>
<td>Audio effects such as applauding, cheering, whistling, and booing</td>
<td>Audio call, video call, interactive live streaming, audio chat room, karaoke, FM radio</td>
<td>Free</td>
</tr><tr>
<td>Publishing system audio</td>
<td>Publishing the audio you play locally, for example, the music played by QQ Music on your computer, to remote users</td>
<td>Interactive live streaming, online class, audio chat room, FM radio, etc.</td>
<td>Free</td>
</tr><tr>
<td>Voice changing</td>
<td>Voice changing effects such as little girl, middle-aged man, and metal</td>
<td>Audio call, video call, interactive live streaming, audio chat room, karaoke, FM radio, etc.</td>
<td>Free</td>
</tr><tr>
<td>Reverb</td>
<td>Reverb effects such as karaoke, small room, hall, and bathroom</td>
<td>Audio call, video call, interactive live streaming, audio chat room, karaoke, FM radio</td>
<td>Free</td>
</tr><tr>
<td>Volume callback</td>
<td>Callback of volume, which you can use to generate audio waveforms or volume reminders</td>
<td>Audio call, video call, audio chat room, FM radio, karaoke, and speech detection, etc.</td>
<td>Free</td>
</tr><tr>
<td>In-ear monitoring</td>
<td>Recording local audio and playing it back in the local user’s earphones, usually for detection of speech errors or pitch control during singing</td>
<td>Interactive live streaming, showroom, karaoke, etc.</td>
<td>Free</td>
</tr><tr>
<td>Custom audio data</td>
<td>Callback of raw audio for custom processing. You can connect the SDK to non-standard external devices or use audio files, etc.</td>
<td>Non-standard device connection, custom audio effect, speech processing, speech recognition, etc.</td>
<td>Free</td>
</tr><tr>
<td>Custom video data</td>
<td>Custom video sources and renderers. You can use non-camera video sources such as video files, external devices, and third-party sources.</td>
<td>Custom beauty filters, custom data sources, multi-device management, video recognition, image processing, etc.</td>
<td>Free</td>
</tr><tr>
<td>SEI message</td>
<td>Embedding custom information such as lyrics and questions as SEI frames into published video streams</td>
<td>Karaoke, live quiz, interactive live streaming, etc.</td>
<td>Free</td>
</tr>
</table>

## Extended Features

>?Extended features are value-added services provided by TRTC in collaboration with other Tencent Cloud products and are charged according to the billing standards of the corresponding products.


| Feature | Description | Common Use Cases | Billing |
| ------------ | ------------------------------------------------------------ | -------------------------------------------------- | ------------------------------------------------------------ |
| CDN live streaming | TRTC uses relaying and transcoding clusters to convert its UDP audio/video streams into RTMP streams in the cloud, which are then pushed to the standard live streaming system and distributed through CDNs to audience. | Interactive live streaming, live sharing, large-scale conferencing, live stream watching by remote audience, etc. | Relayed live streaming is a value-added service and is charged by [CSS](https://intl.cloud.tencent.com/document/product/267). For more information, please see [CDN Relayed Live Streaming > Billing](https://intl.cloud.tencent.com/document/product/647/35242). |
| Instant messaging (IM) | <ul style="margin:0"><li>TRTC leverages the capabilities of IM, including one-to-one chat, group chat, and chat rooms with no upper limit on user number, to enable features such as chatting, commenting, and sending on-screen comments, gifts, and likes.</li><li>IM can also be used for signaling-based interaction, call making, and user number counting.</li></ul> | Online customer service, interactive live streaming, interactive classrooms, remote training, etc. | IM is a value-added service and is charged by [IM](https://intl.cloud.tencent.com/document/product/1047). For more information, please see [IM > Purchase Guide > Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).|
| AI beauty filter| Multiple effects based on face recognition such as AI beauty filters, makeup effects, facial feature adjustment, and green screen keying| Video call, interactive live streaming, live show streaming, etc.| AI beauty filters are a value-added service and are charged by the beauty filter SDK. |
|Speech content moderation|Detecting pornographic and other problematic audio content for content-related risk management |Business security protection, compliance, etc.|Speech content moderation is a value-added service and is charged by **Business Security Protection (BSP)**. To try it out, [contact us](https://intl.cloud.tencent.com/contact-us) to activate the service.|
| Video content moderation| Detecting pornographic and other problematic video content for content-related risk management | Business security protection, compliance, etc.| Video content moderation is a value-added service and is charged by [CSS](https://intl.cloud.tencent.com/document/product/267). For more information, please see [Intelligent Porn Detection](https://intl.cloud.tencent.com/document/product/267/39607). |
