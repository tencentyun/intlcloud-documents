This document describes how to import advanced live streaming features into your program.

## AV1 Video Playback
AV1 is an open-source and royalty-free video compression format. Compared with its predecessor H.265 (HEVC) encoding, it can further reduce the bitrate by over 30% while maintaining the same level of image quality. This means that it can deliver a higher image quality at the same bandwidth. Currently, CSS supports AV1 encoding. However, to play back AV1 videos, your player must support decoding the AV1 format.
You can implement AV1 decoding in your own player as follows:

### Container format and distribution protocol
Tencent Cloud has implemented a proprietary extension to AV1 in FLV in T-FFmpeg. To modify your player, you can extend the code based on the [patch files](https://github.com/tencentyun/AV1/tree/main/patch) of T-FFmpeg. For more information, see [tencentyun/AV1](https://github.com/tencentyun/AV1).

### Decoding
- **Hardware decoding**
On PC, almost all new models of AMD, Intel, and Nvidia GPUs support AV1 hardware decoding.
Device models supporting AV1 hardware decoding are as listed below:
<table>
<thead>
<tr>
<th>Type</th>
<th>Brand</th>
<th>Processor</th>
</tr>
</thead>
<tbody><tr>
<td rowspan=23>Mobile phone</td>
<td>Realme X7 Pro</td><td>Dimensity 1000+</td>
</tr><tr>
<td>OPPO Reno5 Pro</td><td>Dimensity 1000+</td>
</tr><tr>
<td>HONOR V40</td><td>Dimensity 1000+</td>
</tr><tr>
<td>Redmi K30 Ultra</td><td>Dimensity 1000+</td>
</tr><tr>
<td>Vivo iQOO Z1</td><td>Dimensity 1000+</td>
</tr><tr>
<td>Redmi Note 10 Pro</td><td>Dimensity 1000+</td>
</tr><tr>
<td>Vivo S9</td><td>Dimensity 1100</td>
</tr><tr>
<td>Realme Q3 Pro</td><td>Dimensity 1100</td>
</tr><tr>
<td>Vivo S10</td><td>Dimensity 1100</td>
</tr><tr>
<td>Vivo S12</td><td>Dimensity 1100</td>
</tr><tr>
<td>Vivo S12 Pro</td><td>Dimensity 1200</td>
</tr><tr>
<td>OPPO Reno6 Pro</td><td>Dimensity 1200</td>
</tr><tr>
<td>OPPO Reno7 Pro</td><td>Dimensity 1200</td>
</tr><tr>
<td>Redmi K40 Pro</td><td>Dimensity 1200</td>
</tr><tr>
<td>Realme GT NEO</td><td>Dimensity 1200</td>
</tr><tr>
<td>HONOR X20</td><td>Dimensity 1200</td>
</tr><tr>
<td>OnePlus Nord 2</td><td>Dimensity 1200</td>
</tr><tr>
<td>Realme GT NEO 2</td><td>Dimensity 1200</td>
</tr><tr>
<td>OPPO K9 Pro</td><td>Dimensity 1200</td>
</tr><tr>
<td>OPPO Find X5 Pro Dimensity Edition</td><td>Dimensity 9000</td>
</tr><tr>
<td>Redmi K50</td><td>Dimensity 9000</td>
</tr><tr>
<td>Galaxy S21 (Exynos Edition)</td><td>Exynos 2100</td>
</tr><tr>
<td>Galaxy S22 (Exynos Edition)</td><td>Exynos 2200</td>
</tr><tr>
<td>TV</td><td>Samsung Q950TS QLED 8K TV</td><td>-</td>
</tr>
</tbody></table>

- **Software decoding**
	- av1d (Tencent Cloud's optimized AV1 decoder, which outperforms dav1d and can provide closed-source libraries. You can integrate it as instructed in [av1d Integration Guide](https://doc.weixin.qq.com/doc/w3_APEAMQbpAEs1nkQ8rfiR02j8K8srn?scode=AJEAIQdfAAo21jd3VvAPEAMQbpAEs&version=4.0.8.6617&platform=win). T-FFmpeg provides FFmpeg patches to be integrated and av1d libraries.)
	- [dav1d](https://code.videolan.org/videolan/dav1d) 
	- libgav1
	- Android 10.0 integrates an AV1 decoder.
	- The Chrome family supports AV1 decoding.

### Support by browsers
The Chrome family supports AV1 decoding while browsers on iOS don't.
![](https://qcloudimg.tencent-cloud.cn/raw/5e2045b9c9f721306675c3f812a52d04.png)
>! The above information was collected from this [website](https://caniuse.com/?search=AV1) in July 2022. To view the latest information, please visit the website.

## TMIO SDK
The TMIO SDK customizes, encapsulates, and optimizes streaming media protocols such as SRT and QUIC. It safeguards upstreaming and implements low-latency transfer with a high packet loss prevention rate, multi-linkage transfer optimization, and the retransmission timeout (RTO) mechanism. It promises wide application in scenarios that require a high data source stability and long-range transfer.

### Feature description
- The TMIO SDK is suitable for long-range transfer and the radio and TV industry.
- The TMIO SDK supports mainstream platforms, including Android, iOS, Windows, macOS, and Linux.

### Integration method
You can integrate the SDK as instructed in [Integration Steps](https://www.tencentcloud.com/document/product/267/51158).


## libLebConnection SDK
The libLebConnection SDK provides upgraded transfer capabilities based on the native WebRTC. It allows you to connect your existing player to LEB with just a few simple modifications. Based on LVB-compatible stream push and cloud-based media processing capabilities, it can implement live streaming at a low latency even under high concurrency, so as to help you smoothly migrate from standard LVB streaming to low-latency LEB streaming. For large rooms in modern real-time communication (RTC) scenarios, it can also help you quickly implement relayed live streaming at low costs and low latency.

### Feature description
- The libLebConnection SDK can pull audio/video streams at a low latency even under poor network conditions.
- It can play back H.264. H.265, and AV1 videos with B frames and output them as raw video frame data such as Annex B and OBU files for H.264/H.265 and AV1 input videos respectively.
- It can play back AAC and Opus audios and output them as raw audio frame data.
- It supports Android, iOS, Windows, Linux, and macOS.

### Integration method
You can integrate the libLebConnection SDK as instructed in [Integrating libLebConnection SDK into a Player](https://www.tencentcloud.com/document/product/267/51159#.E6.8E.A5.E5.85.A5.E6.96.B9.E5.BC.8F).

### Beauty filters and special effects
To integrate beauty filters and special effects and import beauty filters, image filters, and stickers during live streaming, you can integrate the Tencent Effect SDK.

### Integration into an application
Download the Tencent Effect SDK [here](https://www.tencentcloud.com/document/product/1143/45377) and integrate it as instructed in the [iOS ](https://www.tencentcloud.com/document/product/1143/45387) and [Android](https://www.tencentcloud.com/document/product/1143/45388) integration guides.


## More
Using the [Tencent Effect SDK](https://www.tencentcloud.com/document/product/1143/45377) will incur fees. For billing details, see [Pricing Overview](https://www.tencentcloud.com/document/product/1143/45371).