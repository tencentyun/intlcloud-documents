## Basic Features


<table>
<tr><th width="9%">Feature</th><th width="45%">Description</th><th width="25%">Common Use Cases</th><th>Billing</th>
</tr>
<tr>
<td>Video call</td>
<td><ul style="margin:0">
<li>720p/1080p one-to-one or group video calls
<li>Each room allows up to 300 concurrent users, and up to 50 of them can turn their cameras on at the same time.</li>
</ul></td>
<td>One-to-one video calls, video conferences with up to 300 participants, online medical consultation, video chat, video customer service, video interviews, audiovisual recording, online insurance claim settlement, and video-based party games</td>
<td rowspan=4>
<a href="https://intl.cloud.tencent.com/document/product/647/42734">Billing of TRTC Basic Services</a>
</td>
</tr>
<tr>
<td>Audio call</td>
<td><ul style="margin:0">
<li>One-to-one or group audio calls, which support 48 kHz sampling and dual channels</li>
<li>Each room allows up to 300 concurrent users, and up to 50 of them can keep their mics on at the same time.</li>
</ul></td>
<td>One-to-one or group audio calls, voice chat, audio conferences, audio customer service, and audio-based party games</td>
</tr><tr>
<td>Interactive video streaming</td>
<td><ul style="margin:0">
<li>Video communication between anchors and audience</li>
<li>Cross-room anchor communication</li>
<li>Smooth mic on/off without waiting; anchor latency less than 300 ms</li>
<li>No upper limit on the cumulative number of co-anchoring users in a room; up to 50 users can keep their mics on at the same time.</li>
<li>Streaming to up to 100,000 concurrent users and a playback latency as low as 1,000 ms in the low-latency live streaming mode</li>
<li>No upper limit on audience size in the CDN live streaming mode</li>
</ul></td>
<td>Low-latency live video streaming, interactive classrooms with up to 100,000 participants, live video competitions, video dating, remote training, large-scale conferences</td>
</tr><tr>
<td>Interactive audio streaming</td>
<td><ul style="margin:0">
<li>Audio communication between anchors and audience</li>
<li>Cross-room anchor communication</li>
<li>Smooth mic on/off without waiting; anchor latency less than 300 ms</li>
<li>No upper limit on the cumulative number of co-anchoring users in a room; up to 50 users can keep their mics on at the same time.</li>
<li>Streaming to up to 100,000 concurrent users and a playback latency as low as 1,000 ms in the low-latency live streaming mode</li>
<li>No upper limit on audience size in the CDN live streaming mode</li>
</ul></td>
<td>Low-latency live audio streaming, live audio co-anchoring, live audio competitions, audio chat rooms, audio dating, karaoke rooms, FM radio</td>
</tr></table>



## Advanced Features
<table>
<tr><th width=12%>Feature</th><th width=40%>Description</th><th width=25%>Common Use Cases</th><th width=25%>Billing</th></tr>
<tr>
<td>Co-anchoring</td>
<td>Smooth mic on/off without waiting</td>
<td>Interactive live streaming, online class, chat room</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34610">Basic service fees</a> are charged for using the co-anchoring feature.</td>
</tr><tr>
<td>Cross-room communication</td>
<td>Anchors from different rooms can communicate with each other while audience members watch.</td>
<td>Showroom streaming, cross-room communication, cross-room class</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34610">Basic service fees</a> are charged for using the cross-room communication feature.</td>
</tr><tr>
<td>Screen sharing</td>
<td>Sharing the desktop, a window (for example, a Microsoft PowerPoint window), or a portion of the desktop</td>
<td>Online class, slideshow sharing, remote assistance</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34610">Basic service fees</a> are charged for using the screen sharing feature.</td>
</tr><tr>
<td>Server-side local recording</td>
<td>Server-side recording relies on the Linux SDK, which is not commercially available yet. If you have questions about the SDK or want to use it, please contact us at colleenyu@tencent.com.</td>
<td> Audiovisual recording, archiving, compliance</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34610">Basic service fees</a> are charged for using the server-side local recording feature.</td>
</tr><tr>
<td>On-cloud recording</td>
<td>On-cloud recording relies on the relay-to-CDN feature and leverage the capabilities of <a href="https://intl.cloud.tencent.com/document/product/267">CSS</a> to record live streaming sessions (audio/video). Recording files are saved securely and in real time to <a href="https://intl.cloud.tencent.com/document/product/266">VOD</a>.</td>
<td> Audiovisual recording, archiving, compliance</td>
<td>On-cloud recording is a value-added service and incurs additional fees.</td>
</tr><tr>
<td>On-Cloud MixTranscoding</td>
<td>TRTC uses an MCU cluster to mix and transcode the audio and video streams in a room and publishes the mixed stream to CSS for on-cloud recording or CDN playback.</td>
<td>Stream mixing, recording format conversion</td>
<td>On-Cloud MixTranscoding is a value-added service and incurs additional fees.</td>
</tr><tr>
<td>High audio quality</td>
<td>48 kHz sample rate, end-to-end 192 Kbps bitrate, and dual channels for a clear and immersive audio interaction experience</td>
<td>Audio call, video call, interactive live streaming, audio chat room, high-audio-quality FM radio, music class, karaoke, online class</td>
<td>Free of charge</td>
</tr><tr>
<td>High video quality</td>
<td>720p/1080p HD video</td>
<td>Video call, interactive live streaming, online class</td>
<td>Free of charge</td>
</tr><tr>
<td>3A processing</td>
<td>Leveraging the industry-leading 3A (acoustic echo cancellation, active noise suppression, automatic gain control) technologies of Tencent Ethereal Audio Lab, TRTC can ensure audio quality even when multiple people speak at the same time or in the presence of background noises.</td>
<td>All audio scenarios</td>
<td>Free of charge</td>
</tr><tr>
<td>AI-based noise suppression</td>
<td>Removing inconstant noises that traditional noise suppression technologies cannot handle, such as cough, sneeze, and car horn</td>
<td>Audio call, video call, interactive live streaming, audio chat room, online class</td>
<td><a href="https://intl.cloud.tencent.com/apply/p/9q0qt0bg5l4">Apply for beta testing</a></td>
</tr><tr>
<td>Basic beauty filters</td>
<td>Basic beautification features, including skin brightening, skin smoothing, blush, and basic filters</td>
<td>Video call, interactive live streaming, online class</td>
<td>Free of charge</td>
</tr><tr>
<td>Background music</td>
<td>Using local music files in formats such as MP3, AAC, and WAV as background music</td>
<td>Audio call, video call, interactive live streaming, online class, audio chat room, karaoke, FM radio</td>
<td>Free of charge</td>
</tr><tr>
<td>Audio effects</td>
<td>Audio effects such as applauding, cheering, whistling, and booing</td>
<td>Audio call, video call, interactive live streaming, audio chat room, karaoke, FM radio</td>
<td>Free of charge</td>
</tr><tr>
<td>Publishing system audio</td>
<td>Publishing the audio you play locally, for example, the music played by QQ Music on your computer, to remote users</td>
<td>Interactive live streaming, online class, audio chat room, FM radio</td>
<td>Free of charge</td>
</tr><tr>
<td>Voice changing</td>
<td>Voice changing effects such as little girl, middle-aged man, and metal</td>
<td>Audio call, video call, interactive live streaming, audio chat room, karaoke, FM radio</td>
<td>Free of charge</td>
</tr><tr>
<td>Reverb</td>
<td>Reverb effects such as karaoke, small room, hall, and bathroom</td>
<td>Audio call, video call, interactive live streaming, audio chat room, karaoke, FM radio</td>
<td>Free of charge</td>
</tr><tr>
<td>Volume callback</td>
<td>Callback of audio volumes, which you can use to display audio waveforms or volume reminders</td>
<td>Audio call, video call, audio chat room, FM radio, karaoke, and speech detection</td>
<td>Free of charge</td>
</tr><tr>
<td>In-ear monitoring</td>
<td>Recording local audio and playing it back in the local user’s earphones, usually for detection of speech errors or pitch control during singing</td>
<td>Interactive live streaming, showroom streaming, karaoke</td>
<td>Free of charge</td>
</tr><tr>
<td>Custom audio data</td>
<td>Callback of raw audio for custom processing. You can connect the SDK to non-standard external devices or use local audio files.</td>
<td>Non-standard device connection, custom audio effect, speech processing, speech recognition</td>
<td>Free of charge</td>
</tr><tr>
<td>Custom video data</td>
<td>Custom video sources and renderers. You can use non-camera video sources such as video files, external devices, and third-party sources.</td>
<td>Custom beauty filters, custom data sources, multi-device management, video recognition, image processing</td>
<td>Free of charge</td>
</tr><tr>
<td>SEI message</td>
<td>Embedding custom information such as lyrics and questions as SEI frames into published video streams</td>
<td>Karaoke, live quiz, interactive live streaming</td>
<td>Free of charge</td>
</tr>
</table>

## Extended Features

>? Extended features are provided by other Tencent Cloud products and are charged according to the billing standards of the corresponding products.

<table>
<thead><tr><th width=9%>Feature</th><th>Description</th><th>Common Use Cases</th><th>Billing</th></tr></thead>
<tbody><tr>
<td>CDN live streaming</td>
<td>TRTC uses relaying and transcoding clusters to convert its UDP audio/video streams into RTMP streams in the cloud, which are then pushed to the standard live streaming system and distributed through CDNs to the audience.</td>
<td>Interactive live streaming, live sharing, large-scale conferencing, live stream viewing by remote users</td>
<td>CDN live streaming is charged by <a href="https://intl.cloud.tencent.com/document/product/267">CSS</a>.</td>
</tr>
<tr>
<td>IM</td>
<td><ul style="margin:0"><li>You can use the capabilities of IM, including one-to-one chat, group chat, and chat rooms with no upper limit on user number, to implement features such as chat, comments, and sending on-screen comments, gifts, and likes.</li><li>You can also use IM for signaling-based interaction, call invitations, and user counting.</li></ul></td>
<td>Video customer service, interactive live streaming, interactive classroom, remote training</td>
<td>IM features are charged by <a href="https://intl.cloud.tencent.com/document/product/1047">IM</a>. For details, see <a href="https://intl.cloud.tencent.com/document/product/1047/34350">Pricing</a>.</td>
</tr>
<tr>
<td>AI-based beauty filters</td>
<td>Diverse effects enabled by face recognition technologies, such as AI-based beautification, makeup effects, facial feature adjustment, and green screen keying</td>
<td>Video call, interactive live streaming, showroom streaming</td>
<td>AI-based beauty filters are charged by Tencent Effect SDK.</a></td>
</tr>
</tbody></table>
