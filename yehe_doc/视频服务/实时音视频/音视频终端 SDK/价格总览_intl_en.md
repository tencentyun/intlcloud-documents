## Billing Overview

In order to use a capability of Tencent Cloud’s media SDKs (RT-Cube), you need to purchase the corresponding license resource.

>! For details about the capabilities of the SDKs, see [SDK Download](https://www.tencentcloud.com/document/product/647/34615).

<table>
<thead>
<tr>
<th colspan="2" width="40%">Item</th>
<th>Description</th>
<th width="22%">Billing</th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan="4">SDK Licenses</td>
<td>Live stream publishing</td>
<td>This license can activate the <b>live stream publishing and video playback</b> capabilities.</td>
<td><ul style="margin:0">
<li><a href="#live_license">Live stream publishing license fee</a><br></li></td>
</tr>
<tr>
<td>UGSV</td>
<td>This license can activate the <b>UGSV and video playback</b> capabilities.</td>
<td><ul style="margin:0">
<li><a href="#ugsv_license">UGSV license fee</a><br></li></td>
</tr>
<tr>
<td>Video playback</td>
<td>This license can activate the <b>video playback</b> capability.</td>
<td><ul style="margin:0">
<li><a href="#play_license">Video playback license fee</a></li></td>
</tr>
</tbody></table>

Using Tencent Cloud services with the media SDKs will also incur fees.

<table>
<thead>
<tr>
<th colspan="2" width="40%">Item</th>
<th>Description</th>
<th width="22%">Billing</th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan="4">Tencent Cloud services</td>
<td>Cloud Streaming Services (CSS)</td>
<td>CSS service fees will be incurred if you use CSS together with the live stream publishing and video playback capabilities of the media SDKs to quickly publish live streams to the cloud for processing and delivery.</td>
<td><a href="https://www.tencentcloud.com/document/product/267/2819">Billing of CSS</a></td>
</tr>
<tr>
<td>Tencent Real-Time Communication (TRTC)</td>
<td>TRTC service fees will be incurred for using the media SDKs to implement features such as audio/video calls, group conference, and interactive live streaming.</td>
<td><a href="https://www.tencentcloud.com/document/product/647/34610">Billing of TRTC</a></td>
</tr>
<tr>
<td>Video on Demand (VOD)</td>
<td>VOD service fees will be incurred if you use VOD together with the media SDKs to implement capabilities such as live recording, replay, short video editing, video storage, and video distribution.</td>
<td><a href="https://www.tencentcloud.com/document/product/266/2838">Billing of VOD</a></td>
</tr>
<tr>
<td>Instant Messaging (IM)</td>
<td>IM service fees will be incurred if you use Tencent Cloud’s IM service together with the media SDKs to implement capabilities such as room management, on-screen commenting, gift/red packet sending, and messaging.</td>
<td><a href="https://www.tencentcloud.com/document/product/1047/34349">Billing of IM</a></td>
</tr>
</tbody></table>

[](id:license)

## SDK Licenses

### Fees

We use licenses to manage access to different functional modules of the media SDKs. Currently, you need licenses to use the **live stream publishing**, **UGSV**, and **video playback** capabilities. For UGSV, we offer two types of licenses: **UGSV Standard** and **UGSV Lite**.

- A live stream publishing license can activate the **live stream publishing and video playback** capabilities.
- A UGSV license can activate the **UGSV and video playback** capabilities.
- A video playback license can activate the **video playback** capability.

You can **purchase licenses** to activate the corresponding capabilities. A purchased license is **valid for one year after you bind it to an application and expires at 00:00:00 the next day**. Alternatively, **if you buy packages, you will get a live stream publishing license or UGSV license for free**. Such licenses are **valid for one year after you purchase the packages (expire at 00:00:00 the next day)**.

>! The video playback license was introduced in the 10.1 version of the media SDKs (launched at the end of May 2022).

#### Pricing of live stream publishing licenses[](id:live_license)

<table>
<thead>
<tr>
<th>License Type</th>
<th>Validity Period</th>
<th>Capability</th>
<th>Price (USD)</th>
<th>How to Get</th>
</tr>
</thead>
<tbody><tr>
<td>Live stream publishing<br>(<b>trial</b>)</td>
<td>28 days</td>
<td rowspan=2>Live stream publishing + Video playback</td>
<td>0</td>
<td><a href="https://console.tencentcloud.com/vod/license">Apply for free</a></td>
</tr>
<tr>
<td>Live stream publishing</td>
<td >One year</td>
<td>5,988</td>
<td r><a href="https://buy.tencentcloud.com/license">Buy now</a></td>
</tbody></table>



#### Pricing of UGSV licenses[](id:ugsv_license)

<table>
<thead>
<tr>
<th>License Type</th>
<th>Validity Period</th>
<th>Capability</th>
<th>Price (USD)</th>
<th>How to Get</th>
</tr>
</thead>
<tbody><tr>
<td>UGSV Standard <br>(<strong>trial</strong>)</td>
<td>28 days</td>
<td>UGSV (Standard) + Video playback</td>
<td>0</td>
<td><a href="https://console.tencentcloud.com/vod/license">Apply for free</a></td>
</tr>
<tr>
<td>UGSV Lite</td>
<td>One year</td>
<td>UGSV (Lite) + Video playback</td>
<td>1,899</td>
<td rowspan=3><a href="https://buy.tencentcloud.com/license">Buy now</a></td>
</tr>
<tr>
</tr>
<tr>
<td rowspan=2>UGSV Standard</td>
<td rowspan=2>One year</td>
<td rowspan=2>UGSV (Standard) + Video playback</td>
<td>9,999</td>
</tr>
</tbody></table>

>? UGSV Standard offers additional capabilities such as filters, special effects, and transition effects to help you easily build short video applications for mobile devices. For details, see [Different Editions of the UGSV SDK](https://www.tencentcloud.com/document/product/1069/37914).

#### Pricing of video playback licenses[](id:play_license)

The **video playback** license was introduced in the 10.1 version (launched at the end of May 2022) of our media SDKs for mobile devices (Android, iOS and Flutter).

- **If your application is already bound with a live stream publishing license or UGSV license, you can continue to use the corresponding features after you update to v10.1**.
- If your application is not bound with a live stream publishing license or UGSV license, **you need to purchase a video playback license in order to use the live or VOD playback features of the new SDKs**. For details, see [Activating capabilities](#warrant).
- If you don’t use the video playback capability or do not update the SDKs, you will not be affected by the change.

<table>
<thead>
<tr>
<th width=15%>License Type</th>
<th>Validity Period</th>
<th>Capability</th>
<th width=10%>Price<br>(USD)</th>
<th>How to Get</th>
</tr>
</thead>
<tbody><tr>
<td>Video playback (trial)</td>
<td>28 days</td>
<td rowspan=2>Video playback</td>
<td rowspan=2>0</td>
<td rowspan=2><a href="https://console.tencentcloud.com/vod/license">Apply for free</a></td>
</tr>
<tr>
<td>Video playback</td>
<td>One year</td>
</tr>
</tbody></table>

[](id:warrant)

#### Activating capabilities

In v10.1 and later versions, you can activate the **video playback** capability (live and VOD playback) using **any** of the three licenses: live stream publishing, UGSV, or video playback. For more details about the capabilities different licenses can activate, see the table below:

<table>
<thead>
<tr>
<th rowspan="2" width=20%>License</th>
<th colspan="3">Capabilities</th>
<th rowspan="2">How to Get</th>
</tr><tr>
<th>Live stream publishing</th>
<th>UGSV</th>
<th>Video playback</th>
</tr>
</thead>
<tbody>
<tr>
<td>Live stream publishing</td>
<td>&#10003; </td>
<td>-</td>
<td>&#10003; </td>
<td><ul style="margin:0">
<li>Purchase a live stream publishing license (valid for one year)</li></ul></td>
</tr>
<tr>
<td>UGSV</td>
<td>-</td>
<td>&#10003; </td>
<td>&#10003; </td>
<td><ul style="margin:0">
<li>Purchase a UGSV license (valid for one year)</li></ul></td>
</tr>
<tr>
<td>Video playback</td>
<td>-</td>
<td>-</td>
<td>&#10003; </td>
<td><ul style="margin:0">
<li>Apply for a video playback license for free (valid for one year)</li></ul></td>
</tr>
</tbody></table>

#### Billing details

- Each Tencent Cloud account can **apply for one live stream publishing license, one UGSV license, and one video playback license for free** to try out the corresponding capabilities. A trial license is valid for 14 days. You can extend the validity by another 14 days in the console (28 days in total).
- A license can be bound to a new application or replace an existing license. After replacement, the expiration time of the new license will apply. The original license will be automatically unbound from the application. Its validity period will not change.
- About validity:
  - If you purchase a package, the license you get will be valid for one year **from the time of purchase** (expire on 00:00:00 the next day), regardless of whether you have used up the package. For renewal, bind a new package to your application.
  - After you purchase a license, the license will be inactive until you bind it to an application. A purchased license is valid for one year **after you bind it to an application** (expires at 00:00:00 the next day).
- **Each license can be bound to one iOS bundle ID and one Android package name, regardless of whether you use it in the development or production environment.** If you want to use the media SDKs with more than one application, you need to purchase multiple licenses.

- **A purchased license is not refundable after it’s bound to an application.**


### Service fees

[](id:value)

**In addition to license fees, using the media SDKs may also incur the following service fees.**

## Cloud Streaming Services (CSS)

The live stream publishing and video playback capabilities of the media SDKs rely on a backend to receive, process, and deliver live streams. We recommend you use [CSS](https://www.tencentcloud.com/products/css).

CSS offers capabilities including live stream receiving, on-cloud recording, live transcoding, live screencapture, and live stream delivery and playback.

- Using CSS to receive and deliver live streams will incur basic service fees, which are charged based on the traffic/bandwidth consumed.
- Using CSS features such as live transcoding (including stream mixing and watermarking), live recording, live screencapture, RTC-based co-anchoring, and relay to CDN will incur value-added service fees.

>? For more information about the billing of CSS, see [Pricing Overview](https://www.tencentcloud.com/document/product/267/2819).


## Tencent Real-Time Communication (TRTC)

[TRTC](https://www.tencentcloud.com/products/trtc) service fees will be incurred if you use the media SDKs to implement features such as audio/video calls, group conference, and interactive live streaming.

Billing of TRTC:

- Basic service fees are charged based on the duration of an audio/video live streaming session or an audio/video call.
- Value-added service fees are incurred if you use TRTC services such as on-cloud recording and On-Cloud MixTranscoding.

>? For more information about the billing of TRTC, see [Billing Overview](https://www.tencentcloud.com/document/product/647/34610).

## Video on Demand (VOD)

You can use Tencent Cloud’s [VOD](https://www.tencentcloud.com/products/vod) service to record and replay live streams or store and distribute short videos after editing.

Billing of VOD:

- Storage fees are charged based on the storage space used by files uploaded to VOD and their transcoding outputs.
- If you transcode files stored in VOD, transcoding fees are charged based on the specifications and durations of the outputs.
- If you use VOD’s acceleration service to deliver videos, acceleration fees will be charged based on the traffic consumed for playback.

>? For more information about the billing of VOD, see [Billing Overview](https://www.tencentcloud.com/document/product/266/2838).

## Instant Messaging (IM)

You can use Tencent Cloud’s [IM](https://www.tencentcloud.com/products/im) to implement features such as room management, on-screen commenting, red packet/gift sending, and messaging. For the billing details, see [Billing Overview](https://www.tencentcloud.com/document/product/1047/34349).

>!
>- The messaging feature relies on IM’s audio-video group capability. The maximum number of audio-video groups that can be created depends on the IM plan and value-added services you purchase.
>- You can use Tencent Cloud’s IM to implement features such as on-screen commenting, messaging, and red packet/gift sending. You can also develop your own solutions or use a third-party service.
>- IM has a free edition that allows you to try out its features. You can purchase plans or value-added services based on your actual needs.
