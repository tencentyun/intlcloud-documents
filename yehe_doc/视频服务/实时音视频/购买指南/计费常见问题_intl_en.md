[](id:que0)

### Are there discounts for high-demand customers?

- Regular discounts: The more minutes a package contains, the higher the discount. For example, you can purchase packages that contain 3 million or more minutes at a discount of 20%.
- Contractual discounts: If your monthly spending on TRTC services exceeds 3,000 USD, you can [contact us](https://intl.cloud.tencent.com/contact-us) for contractual discounts.

### How are TRTC services billed?

TRTC offers basic services and value-added services. For details about their billing, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/647/34610). New users are offered a 10,000-minute [free trial](https://intl.cloud.tencent.com/document/product/647/42735).

[](id:que1)

### How do I view my bills and transaction history?
You can view your bills and transaction history in [Billing Center > Bill Details](https://console.cloud.tencent.com/expense/bill/summary).

[](id:que3)
### How do I view the details of my billable durations?
- Real-time durations: You can find a usage graph and view your usage details in [Usage Statistics](https://console.cloud.tencent.com/trtc/statistics) of the TRTC console. If you select a single day, the page will show usage statistics on a 5-minute basis. If you select multiple days, it will show usage statistics on a daily basis. The statistics are accurate to the minute.
- Billable durations: You can [download](https://console.cloud.tencent.com/expense/bill/dosageDownload) an Excel file of your billable durations in Tencent Cloud’s billing center. The file shows your usage on a 5-minute as well as daily basis. The statistics are accurate to the second.

>! Real-time usage statistics may be slightly different from the durations you are actually billed for. In case of conflicts, **the statistics in your bills shall apply**.

[](id:que4)
### How do I view the remaining minutes in my package?
Durations are deducted from your package in real time, and the number of remaining minutes in your package is updated every 5 minutes. You can view your remaining minutes in [Package Management](https://console.cloud.tencent.com/trtc/package).

[](id:que5)
### Given that billable durations are calculated in seconds and rounded up to the next minute, will more minutes than I actually use be deducted from my package?
No. Deductions are based on your cumulative usage in a day.
Below is an example of how deductions work:

|Calculation Period|Period Usage|Cumulative Usage|Cumulative Billable Duration|Period Deduction|Cumulative Deduction|
|---|---|---|---|---|---|
|00:00:00 - 00:04:59|30 sec|30 sec|1 min|1 min|1 min|
|00:05:00 - 00:09:59|20 sec|50 sec|1 min|0 min|1 min|
|00:10:00 - 00:14:59|40 sec|90 sec|2 min|1 min|2 min|


[](id:que6)
### Why are more minutes deducted from my newly purchased package than I actually use after the purchase?

Once a new package takes effect, durations that are generated after 00:00 of the day of purchase and haven’t been deducted will be deducted from the new package. You can view your usage on the day of purchase in [Usage Statistics](https://console.cloud.tencent.com/trtc/statistics) of the TRTC console.

[](id:que15)
### Can I convert an audio/SD video/HD video package that I have purchased into a general package?
Yes, you can. The rules for conversion are as follows:
- 1 min in an **audio package** = 1 min in a general package
- 1 min in an **SD video package** = 2 min in a general package
- 1 min in an **HD video package** = 4 min in a general package

Self-service conversion is not supported at the moment. If you want to convert your package, please [submit a ticket](https://console.cloud.tencent.com/workorder/category). 

[](id:que7)
### Why am I unable to purchase a general package?
Currently, you must be on our allowlist to use TRTC services. [Contact us](https://console.cloud.tencent.com/workorder/category) to add your account to the allowlist.

[](id:que16)
### How do I estimate my usage of TRTC services and the cost?
You can use the [TRTC Price Calculator](https://buy.cloud.tencent.com/price/trtc/calculator) to estimate your usage and cost.

[](id:que8)
### Why would a video call or video streaming session generate audio durations?
In most cases, if a user has subscribed to a stream, he or she would receive both audio and video data. However, in cases where the sender’s camera is turned off, the recipient has disabled remote video or encounters a network problem, or there is only one user in the room, the user would receive no video data. To reduce your expenses, TRTC bills a period during which a user does not receive video data as an audio duration.

[](id:que9)
### How is screen sharing billed?
Screen sharing data is pushed as a separate video stream. If a user subscribed to the screen sharing stream and received screen sharing images in a period, the period would be billed as a video duration.

[](id:que10)

### How is CDN relayed live streaming billed?
TRTC leverages the capabilities of [CSS](https://intl.cloud.tencent.com/document/product/267) to relay streams to CDNs and enable CDN relayed live streaming. **CSS** charges you according to [CDN Relayed Live Streaming > Billing](https://intl.cloud.tencent.com/document/product/647/35242).

[](id:que12)

### Are fees charged if there is only one user in a room?
A room with only one user consumes TRTC’s resources, even if no streams are pushed (no upstream data). The only user in a room cannot subscribe to other users’ streams and therefore won’t receive video data. As a result, the duration is billed as an **audio duration**.

[](id:que13)
### Why is my service status "Disabled"?
- Overdue payments will lead to service suspension. The services will be resumed automatically after you [make the payment](https://console.cloud.tencent.com/expense/overview).
- If you manually disabled an application, you can click **Enable Application** to resume TRTC services for the application.

