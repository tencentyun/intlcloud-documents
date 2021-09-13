

>!This document describes the billing of low-latency live streaming in TRTC rooms. You will incur additional costs if you relay audio and video in TRTC rooms to the CSS system and stream them to audience via CDNs. For details, see [CDN Relayed Live Streaming > Billing](https://intl.cloud.tencent.com/document/product/647/35242).


[](id:Billing_items)
## Usage Calculation

Your usage of interactive live video streaming is the cumulative [video duration](#v_duration) and [audio duration](#s_duration) of all users in your [TRTC rooms](https://intl.cloud.tencent.com/document/product/647/37714).

>! A duration is calculated in seconds and monthly cumulative seconds are converted to minutes for billing. A duration of less than one minute is calculated as one minute.


[](id:v_duration)
### Video duration
Video duration is the length of video streams received by users who subscribe to video streams after room entry. TRTC categorizes and bills video durations based on the **actual resolution of video received**.
Below is how video durations are categorized by resolution:

|Category| Receive Resolution|
|-------|--------|
|SD| ≤ 640 × 480|
|HD|640 × 480 - 1280 × 720|
|FHD| > 1280 × 720|

- If a user subscribes to a video stream, you will only pay for the video duration, regardless of whether the stream contains audio.
- If a user subscribes to multiple channels of video streams, TRTC will add up the video duration of each channel.
- The TRTC SDK does not set limits for resolution. You can [choose the video quality](https://intl.cloud.tencent.com/document/product/647/35153) that fits your needs.


[](id:s_duration)
### Audio duration
In interactive live video streaming, audio duration is the total length of users’ stays in TRTC rooms minus the period during which video data is received.
Assume that a user entered a TRTC room at 00:00 and left at 00:50, and the details of the stay are as follows:
![](https://main.qcloudimg.com/raw/b127abe248a205842a6216ccbd7c111e.png)
The segments in blue are the user’s audio duration, which is `The total length of the user’s stay − The period during which video is received = 50 min − 15 min = 35 min`.


- Audio duration is billed only when users do not subscribe to video streams.
- Audio duration is billed as long as a user does not subscribe to video streams in a room, regardless of whether streams are pushed.
- In cases where a user enters and leaves a room multiple times, TRTC will add up the length of the user’s stays in the room.


[](id:Fixed_price)
## Pricing

The prices of interactive live video streaming are listed below:

| Billable Item   | Unit Price (USD/1,000 Min)|
|---|---|
| Audio     | 0.99                |
| SD  | 1.99                |
| HD  | 3.99                |
| FHD | 14.99               |

[](id:Billing_method)
## Billing Mode
TRTC supports two billing modes: **prepaid packages** and **pay-as-you-go**. The former is the default mode. To switch to pay-as-you-go, please see [Enabling Pay-As-You-Go](https://intl.cloud.tencent.com/document/product/647/41979).

[](id:pre-payment)
### Prepaid packages

TRTC offers general packages, from which audio, SD video, HD video, and FHD video durations are deducted in the proportion of **1:1, 2:1, 4:1, and 15:1** respectively. For example, for 1 minute of HD video duration used, 4 minutes will be deducted from a general package.
Below are the prices of general packages:

<table>
     <tr>
         <th style="text-align:center">Package Type</th>  
         <th style="text-align:center">Package Duration (1,000 Min)</th> 
         <th style="text-align:center">List Unit Price (USD/1,000 Min)</th> 
         <th style="text-align:center">Package Unit Price (USD/1,000 Min)</th> 
         <th style="text-align:center">Package Price (USD)</th> 
          <th style="text-align:center">Package Price/List Price</th> 
     </tr>
     <tr>
         <td style="text-align:center" rowspan="4">Fixed-time package</td>   
         <td style="text-align:center">25</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.960</td>
         <td style="text-align:center">24</td>   
         <td style="text-align:center"><97%</td>     
     </tr> 
     <tr>
         <td style="text-align:center">250 </td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.908</td>
         <td style="text-align:center">227</td>   
         <td style="text-align:center"><92%</td>   
     </tr> 
     <tr>
         <td style="text-align:center">1000 </td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.856</td>
         <td style="text-align:center">856</td>   
         <td style="text-align:center"><87%</td>   
     </tr> 
     <tr>
         <td style="text-align:center">3000</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.805</td>
         <td style="text-align:center">2416</td>   
         <td style="text-align:center"><82%</td>   
     </tr> 
     <tr>
         <td style="text-align:center" rowspan="5">Custom package</td>   
         <td style="text-align:center">0 < T < 25</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.99</td>
         <td style="text-align:center" rowspan="5">Package unit price × Package duration (T)</td>   
         <td style="text-align:center">100%</td>    
     </tr> 
     <tr>
         <td style="text-align:center">25 ≤ T < 250</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.960</td>
         <td style="text-align:center"><97%</td>    
     </tr> 
     <tr>
         <td style="text-align:center">250 ≤ T < 1000</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.908</td>
         <td style="text-align:center"><92%</td>   
     </tr> 
     <tr>
         <td style="text-align:center">1000 ≤ T < 3000</td>
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.856</td>
         <td style="text-align:center"><87%</td>   
     </tr> 
     <tr> 
         <td style="text-align:center">T ≥ 3000</td>   
         <td style="text-align:center">0.99</td>
         <td style="text-align:center">0.805</td>
         <td style="text-align:center"><82%</td>   
     </tr> 
</table>



>? The package unit prices in the table are rounded up to 3 decimal places. However, in actual billing, unit prices are rounded to 8 decimal places.

About general packages:

- A general package is valid from the day of purchase to the last day of the same month next year.
 For example, if you purchased a package on May 1, 2021, it would be valid from May 1, 2021 to May 31, 2022.
- You can purchase multiple packages. Durations are deducted in real time from the package that expires the fastest.
- A new package takes effect in about 5 minutes after payment. **If your account has a duration that is generated after 00:00 of the day of purchase and hasn’t been deducted, it will be deducted immediately from the newly purchased package.**
- To avoid interrupting your businesses, **TRTC will not suspend services for your account when your package is used up or expires**. The minutes not deducted from any package will be billed at [pay-as-you-go](#post-payment) rates.
- Once a general package expires, the remaining minutes in the package will become invalid and cannot be retrieved.


[](id:post-payment)
### Pay-as-you-go
When you overuse your package, the extra duration will be billed at [pay-as-you-go rates](#Fixed_price).
You can choose to pay [daily](#daily) or [monthly](#monthly).

[](id:daily)
#### Daily pay-as-you-go
For accounts that create their first [application](https://intl.cloud.tencent.com/document/product/647/37714) in the TRTC console on or after September 1, 2020, **daily** pay-as-you-go applies by default. Fees for a day are deducted at 10:00 AM the next day.


[](id:monthly)
#### Monthly pay-as-you-go
For accounts that created their first [application](https://intl.cloud.tencent.com/document/product/647/37714) in the TRTC console on or before August 31, 2020, **monthly** pay-as-you-go applies by default. Fees for a month are deducted within the first five days of the next month. For details, see [Bills](https://intl.cloud.tencent.com/document/product/555/7432).
>!
>- You cannot change the billing cycle by yourself. If you want to change the billing cycle from monthly to daily, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>- If your account balance is insufficient for the deduction of the incurred fees, the overdue payment may cause other Tencent Cloud services to be suspended for your account too. For example, because on-cloud recording relies on **CSS** and **VOD**, your on-cloud recording task may fail due to overdue payment.

[](id:Billing_examples)
## Billing Example
>! The examples below use list prices. You can [purchase a package](https://buy.cloud.tencent.com/trtc) to reduce your expenses.

### Audio-only scenario

Assume that users A, B, and C stayed in a TRTC room for 30 minutes, during which none of them received video data. The call would be billed as audio duration.

#### Analysis:
- **Cost of audio-only duration = Unit price of audio duration × Sum of all users’ audio durations**
- The **total cost** would be `Unit price of audio duration × The sum of all three users’ audio durations = 0.99 USD/1,000 min × (30 min + 30 min + 30 min) ÷ 1,000 = 0.0891 USD`.

### Audio-video scenario

Assume that users A, B, and C stayed in a TRTC room for 30 minutes, during which they received each other’s audio-video streams, as shown below.

<table style="width:715px;">
<style>.markdown-text-box table td, .markdown-text-box table th {text-align: center;}
.tablestyle{position:absolute;width:1px;height:160px;top:0;left:0;background-color: #d9d9d9;transform:rotate(-69deg);transform-origin:top;}
.th1{position:absolute;right:20px;top:10px;}
.th2{position:absolute;right:80px;top:30px)
</style>
<tr>
<th style ="position:relative;width:150px" >
  <div class="tablestyle"></div>
  <div class="th1">Sender</div>
  <div class="th2">Recipient</div></th>
  <th>A<br>640 × 360 (SD)</th>
  <th>B<br>Audio only</th>
  <th>C<br>1920 × 1080 (FHD)</th>
</tr><tr>
  <td>A</td>
  <td>-</td>
  <td>&#10003;</td>
  <td>&#10003;</td>
</tr><tr>
  <td>B</td>
  <td>&#10003;</td>
  <td>-</td>
  <td>&#10003;</td>
</tr><tr>
  <td>C</td>
  <td>&#10003;</td>
  <td>&#10003;</td>
  <td>-</td>
</tr></table>

#### Analysis:
- A’s billable duration and expense:
  - **A’s expense = The expense of duration received from B + The expense of duration received from C**
  - The expense of duration received from B = Unit price of audio duration × The duration of audio received = 0.99 USD/1,000 min × (30 ÷ 1000) = 0.0297 USD
  - The expense of duration received from C = Unit price of FHD video duration × The duration of FHD video received = 14.99 USD/1,000 min × (30 ÷ 1000) = 0.4497 USD
  - A’s expense = The expense of duration received from B + The expense of duration received from C = 0.0297 + 0.4497 = 0.4794 USD
- B’s billable duration and expense:
  - **B’s expense = The expense of duration received from A + The expense of duration received from C**
  - The expense of duration received from A = Unit price of SD video × The duration of SD video received = 1.99 USD/1,000 min × (30 ÷ 1000) = 0.0597 USD
  - The expense of duration received from C = Unit price of FHD video duration × The duration of FHD video received = 14.99 USD/1,000 min × (30 ÷ 1000) = 0.4497 USD
  - B’s expense = The expense of duration received from A + The expense of duration received from C = 0.0597 + 0.4497 = 0.5094 USD

- C’s billable duration and expense:
  - **C’s expense = The expense of duration received from A + The expense of duration received from B**
  - The expense of duration received from A = Unit price of SD video duration × The duration of SD video received = 1.99 USD/1,000 min × (30 ÷ 1000) = 0.0597 USD
  - The expense of duration received from B = Unit price of audio duration × The duration of audio received = 0.99 USD/1,000 min × (30 ÷ 1000) = 0.0297 USD
  - C’s expense = The expense of duration received from A + The expense of duration received from B = 0.0597 + 0.0297 = 0.0894 USD

The **total cost** of the TRTC room would be `A’s expense + B’s expense + C’s expense = 1.0782 USD`.

[](id:estimate)
## Usage and Cost Estimation
You can use the [TRTC Price Calculator](https://buy.intl.cloud.tencent.com/pricing/trtc) to estimate your usage of interactive live video streaming and the cost.
1. In **Interactive Live Audio/Video Streaming**, specify **Average Rooms Per Day**, **Average Anchors Per Room**, **Average Audience Size Per Room**, and **Average Streaming Duration Per Room**.
2. Select **SD**, **HD**, or **FHD** for **Category** to get your monthly **Usage Estimate**.
![](https://main.qcloudimg.com/raw/871d7e1d43e83674f82a3960a079ff7c.png)
3. In **Cost Estimate**, you will see your **general package usage** and estimated costs under the prepaid and pay-as-you-go modes.
![](https://main.qcloudimg.com/raw/6bcfdbe34129fcc143e8cb4bd49ff07e.png)



## References
- [Billing Overview](https://intl.cloud.tencent.com/document/product/647/34610)
- [Free Trial](https://intl.cloud.tencent.com/document/product/647/39784)
- [Billing of Interactive Live Audio Streaming](https://intl.cloud.tencent.com/document/product/647/39785)
- [Billing of Audio Calls](https://intl.cloud.tencent.com/document/product/647/39787)
- [Billing of Video Calls](https://intl.cloud.tencent.com/document/product/647/39788)
- [Billing of On-Cloud Recording](https://intl.cloud.tencent.com/document/product/647/38385)
- [Billing of On-Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/38929)
- [Purchase Instructions](https://intl.cloud.tencent.com/document/product/647/35440)
- [FAQs](https://intl.cloud.tencent.com/document/product/647/39789)