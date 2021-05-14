<span id="que1"></span>
### How do I get a free trial?
Starting from October 11, 2019, Tencent Cloud accounts creating applications for the first time in the [TRTC console](https://console.cloud.tencent.com/trtc) will get a 10,000-minute free trial, which can be used for [video calls](https://intl.cloud.tencent.com/document/product/647/39788), [audio calls](https://intl.cloud.tencent.com/document/product/647/39787), [interactive live video streaming](https://intl.cloud.tencent.com/document/product/647/39786), and [interactive live audio streaming](https://intl.cloud.tencent.com/document/product/647/39785). For details, see [Free Trial](https://intl.cloud.tencent.com/document/product/647/39784).
)。

<span id="que2"></span>
### How do I view my bills and transaction history?
You can view your bills and transaction history in [Billing Center > Bill Details](https://console.cloud.tencent.com/expense/bill/summary).

<span id="que3"></span>
### How do I view/get the details of my billable durations?
- Real-time duration statistics: you can view your usage and history in the TRTC console > [Usage Statistics](https://console.cloud.tencent.com/trtc/statistics). If you select a single day, the page will show your usage statistics on a 5-minute basis. If you select multiple days, the page will show your usage statistics on a daily basis. The statistics are accurate to the minute.
- Billed duration: you can [download](https://console.cloud.tencent.com/expense/bill/dosageDownload) an Excel file of your billed durations in Tencent Cloud’s billing center, including durations on a 5-minute and daily basis. The statistics are accurate to the second.
- Server API: you can also get the details of your billable durations through a server API. If the period queried is 1 day or shorter, then the usage statistics returned are on a 5-minute basis. If the period queried is longer than 1 day, then the statistics returned are on a daily basis. The statistics are accurate to the second.

>! Real-time usage statistics are updated in real time and may be slightly different from the durations you are actually billed for. In case of conflicts, **the durations listed in your bills shall prevail**.

<span id="que4"></span>
### How do I view the remaining minutes in my package?
Durations are deducted from your package in real time, and the number of remaining minutes in your package is updated every 5 minutes. You can view your remaining minutes in [Package Management](https://console.cloud.tencent.com/trtc/package).

<span id="que5"></span>
### Given that billable durations are calculated in seconds and rounded up to the next minute, will more minutes than I actually use be deducted from my package?
No. Deductions are based on your cumulative usage in a day.
Below is an example of how deductions work:

|Calculation Period|Period Usage|Cumulative Usage|Cumulative Billable Duration|Period Deduction|Cumulative Deduction|
|---|---|---|---|---|---|
|00:00:00 - 00:04:59|30 sec|30 sec|1 min|1 min|1 min|
|00:05:00 - 00:09:59|20 sec|50 sec|1 min|0 min|1 min|
|00:10:00 - 00:14:59|40 sec|90 sec|2 min|1 min|2 min|


<span id="que6"></span>
### Why are more minutes deducted from my newly purchased package than I actually use after the purchase?

Once a new package takes effect, durations that are generated after 00:00 of the day of purchase and haven’t been deducted will be deducted from the new package. You can view your usage on the day of purchase in the TRTC console > [Usage Statistics](https://console.cloud.tencent.com/trtc/statistics).

<span id="que15"></span>
### Can I convert an audio/SD video/HD video package that I have purchased into a universal package?
Yes, you can. The rules for conversion are as follows:
- 1 min in an **audio package** = 1 min in a universal package
- 1 min in a **SD video package** = 2 min in a universal package
- 1 min in a **HD video package** = 4 min in a universal package

- Self-service conversion is not supported at the moment. If you want to convert your package, please [submit a ticket](https://console.cloud.tencent.com/workorder/category). 

<span id="que7"></span>
### Why am I told that I can’t purchase a universal package?
TRTC changed its billing standards on October 11, 2019. Audio and video durations were priced the same in the past (the old billing standards), but are charged different prices now (the new billing standards). A new package must use the new billing standards.
- Tencent Cloud accounts created on and after October 11, 2019 use the new billing standards by default.
- If your account was created before October 11, 2019, you can purchase a package that uses the new billing standards only starting from the second month after your old package is exhausted or expires. The new billing standards will apply after you purchase a new package.

You can also continue to [purchase](https://buy.cloud.tencent.com/trtc) a package that uses the old billing standards. If you want to use the new billing standards before your old package is exhausted or expires, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).



<span id="que8"></span>
### Why does a video call or interactive live video streaming session generates audio duration?
In most cases, a user who has subscribed to streams would receive both audio and video data. However, if the sender’s camera is turned off, the receiver disables remote images or encounters a network problem, or there is only one user in the room, then the user would receive no video data. To help you reduce your expenses, TRTC bills a period during which a user does not receive video data as an audio duration.

<span id="que9"></span>
### How is screen sharing billed?
Screen sharing data is sent as a separate channel of video streams. If a user subscribes to screen sharing streams and receives screen sharing images in a period, the period will be billed as a video duration.

<span id="que10"></span>
### How is on-cloud recording billed?
TRTC records streams by relaying streams to the [CSS](https://intl.cloud.tencent.com/document/product/267) system. The recording files are saved in [VOD](https://intl.cloud.tencent.com/document/product/266) for future playback.
- For Tencent Cloud accounts that create their first applications in the TRTC console on or after July 1, 2020, the billing standards in [On-cloud Recording Billing](https://intl.cloud.tencent.com/document/product/647/38385) will be applied.
- Accounts that created applications in the TRTC console before July 1, 2020 are charged on-cloud recording fees according to the billing standards in [Live Recording](https://intl.cloud.tencent.com/document/product/267/39605).
- Recording files are saved in VOD by default, which charges **storage fees** and **viewing fees** based on your usage. For more information, see “Billing” in [On-cloud Recording and Playback](https://intl.cloud.tencent.com/document/product/647/35426#billing).
- If you use the On-Cloud MixTranscoding feature of CSS before enabling on-cloud recording, you will be charged an additional [standard transcoding](https://intl.cloud.tencent.com/document/product/267/39604) fee.


<span id="que11"></span>
### How is CDN relayed live streaming billed?
TRTC leverages the capabilities of [CSS](https://intl.cloud.tencent.com/document/product/267) to relay streams to CDNs and enable CDN relayed live streaming. TRTC does not charge you for the service, but **CSS** charges you according to the [billing standards of CDN relayed live streaming](https://intl.cloud.tencent.com/document/product/647/35242).

<span id="que12"></span>
### Are fees charged even if there is only one user in a room?
A room with only one user consumes TRTC’s resources, even if no streams are pushed (no upstream data). The only user in a room cannot subscribe to other users’ streams and therefore won’t receive video data. As a result, the duration is billed as an audio duration.

<span id="que13"></span>
### Can I choose the pay-as-you-go billing mode from the beginning?
 With [video calls](https://intl.cloud.tencent.com/document/product/647/39788), [audio calls](https://intl.cloud.tencent.com/document/product/647/39787), [interactive live video streaming](https://intl.cloud.tencent.com/document/product/647/39786), and [interactive live audio streaming](https://intl.cloud.tencent.com/document/product/647/39785), you will be switched to the pay-as-you-go mode automatically after your prepaid package is exhausted or expires. You cannot choose the pay-as-you-go billing mode from the beginning. If you have signed a pay-as-you-go contract with Tencent Cloud sales, please contact sales to enable the mode for your account.
