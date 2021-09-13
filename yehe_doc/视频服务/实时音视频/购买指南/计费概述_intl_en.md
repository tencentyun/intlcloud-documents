TRTC offers two types of services: **basic services** and **value-added services**.

## Basic Services

Basic services include interactive live audio streaming, interactive live video streaming, audio calls, and video calls. They can be used separately or together. Their pricing is detailed below:

<table>
<tr><th>Service</th><th>Description</th><th>Billing Details</th></tr>
<tr>
<td>Interactive live audio streaming</td>
<td><ul style="margin:0">
<li>Audio co-anchoring between anchors and audience</li>
<li>Cross-room anchor competition</li>
<li>Smooth mic on/off without waiting; anchor latency less than 300 ms</li>
<li>No upper limit on the cumulative number of anchors in a room; up to 50 users can keep their mics on at the same time.</li>
<li>Live streaming to up to 100,000 concurrent users and a playback latency as low as 1,000 ms in the low-latency live streaming mode</li>
<li>No upper limit on audience size in the CDN relayed live streaming mode</li>
</ul></td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/39785">Billing of Interactive Live Audio Streaming</a></td>
</tr>
<tr>
<td>Interactive live video streaming</td>
<td><ul style="margin:0">
<li>Video co-anchoring between anchors and audience</li>
<li>Cross-room anchor competition</li>
<li>Smooth mic on/off without waiting; anchor latency less than 300 ms</li>
<li>No upper limit on the cumulative number of co-anchoring users in a room; up to 50 users can keep their mics on at the same time.</li>
<li>Live streaming to up to 100,000 concurrent users and a playback latency as low as 1,000 ms in the low-latency live streaming mode</li>
<li>No upper limit on audience size in the CDN relayed live streaming mode</li>
</ul></td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/39786">Billing of Interactive Live Video Streaming</a></td>
</tr>
<tr>
<td>Audio call</td>
<td><ul style="margin:0">
<li>One-to-one or group audio calls, which support 48 kHz sampling and dual channels</li>
<li>Each room allows up to 300 concurrent users, and up to 50 of them can keep their mics on at the same time.</li>
</ul></td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/39787">Billing of Audio Calls</a></td>
</tr>
<tr>
<td>Video call</td>
<td><ul style="margin:0">
<li>One-to-one or group video calls, which support 720p and 1080p definitions</li>
<li>Each room allows up to 300 concurrent users, and up to 50 of them can keep their cameras on at the same time.</li></ul></td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/39788">Billing of Video Calls</a></td>
</tr>
</table>

## Value-Added Services

TRTC provides two additional features on top of the four basic services, namely **on-cloud recording** and **On-Cloud MixTranscoding**. These two value-added services must be used together with the basic services and are charged additional fees. Their pricing is detailed below:

| Service                                                         | Description                                                     | Billing Details                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| [On-cloud recording](https://intl.cloud.tencent.com/document/product/647/35426) | TRTC leverages the capabilities of **CSS** to allow you to record entire live streaming sessions through relayed push and save the recording files in **VOD** | [Billing of On-Cloud Recording](https://intl.cloud.tencent.com/document/product/647/38385) |
| [On-Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618) | TRTC uses an MCU cluster to mix and transcode the audio and video streams in a room and pushes the mixtranscoded stream to CSS for **on-cloud recording** or **CDN live streaming**. | [Billing of On-cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/38929) |

## Free Trial

Starting from August 20, 2021, accounts creating applications for the first time in the [TRTC console](https://console.cloud.tencent.com/trtc) will get a 10,000-minute free trial, which can be used for [video calls](https://intl.cloud.tencent.com/document/product/647/39788), [audio calls](https://intl.cloud.tencent.com/document/product/647/39787), [interactive live video streaming](https://intl.cloud.tencent.com/document/product/647/39786), and [interactive live audio streaming](https://intl.cloud.tencent.com/document/product/647/39785). For details, see [Free Trial](https://intl.cloud.tencent.com/document/product/647/39784).