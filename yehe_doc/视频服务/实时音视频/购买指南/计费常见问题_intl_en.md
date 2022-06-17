

### Are there discounts for high-demand customers?

If your monthly spending on TRTC services exceeds 3,000 USD, you can [contact us](https://intl.cloud.tencent.com/contact-us) for contractual discounts.

### How are TRTC services billed?

TRTC offers basic services and value-added services. For details about their billing, see [Billing Overview](https://intl.cloud.tencent.com/document/product/647/34610). We provide users with a 10,000-minute [free package](https://intl.cloud.tencent.com/document/product/647/42735) each month.

### Price calculator

You can use the [TRTC Price Calculator](https://intl.cloud.tencent.com/pricing/trtc/calculator) to estimate your cost.

### How do I view my bills and transaction history?

You can view your bills and transaction history in [Billing Center > Bill Details](https://console.cloud.tencent.com/expense/bill/summary).

### How do I view the details of my billable durations?
- Real-time durations: You can find a usage graph and view your usage details in [Usage Statistics](https://console.cloud.tencent.com/trtc/statistics) of the TRTC console. If you select a single day, the page will show usage statistics on a 5-minute basis. If you select multiple days, it will show usage statistics on a daily basis. The statistics are accurate to the minute.
- Billable durations: You can [download](https://console.cloud.tencent.com/expense/bill/dosageDownload) an Excel file of your billable durations in Tencent Cloud’s billing center. The file shows your usage on a 5-minute as well as daily basis. The statistics are accurate to the second.

>! Real-time usage statistics may be slightly different from the durations you are actually billed for. In case of conflicts, **the statistics in your bills shall apply**.

### How do I view the remaining minutes in my package?
Durations are deducted from your package in real time, and the number of remaining minutes in your package is updated every 5 minutes. You can view your remaining minutes in [Package Management](https://console.cloud.tencent.com/trtc/package).

### Given that billable durations are calculated in seconds and rounded up to the nearest minute, will more minutes than I actually use be deducted from my package?
No. Deductions are based on your cumulative usage in a day.
Below is an example of how deductions work:

|Calculation Period|Period Usage|Cumulative Usage|Cumulative Billable Duration|Period Deduction|Cumulative Deduction|
|---|---|---|---|---|---|
|00:00:00 - 00:04:59|30 sec|30 sec|1 min|1 min|1 min|
|00:05:00 - 00:09:59|20 sec|50 sec|1 min|0 min|1 min|
|00:10:00 - 00:14:59|40 sec|90 sec|2 min|1 min|2 min|

### How do I estimate my usage of TRTC services and the cost?
You can use the [TRTC Price Calculator](https://buy.cloud.tencent.com/price/trtc/calculator) to estimate your usage and cost.

### Why does a video call or video streaming session generate audio durations?
In most cases, if a user subscribes to a stream, they receive both audio and video data. However, in cases where the sender’s camera is turned off, the recipient disables remote video or encounters a network problem, or there is only one user in the room, the user will receive no video data. To reduce your expenses, TRTC bills a period during which a user does not receive video data as audio duration.

### How is screen sharing billed?
Screen sharing data is published as a separate stream. If a user receives a screen sharing stream, the user’s duration will be billed as video duration.

### How is relaying to CDN billed?
TRTC leverages the capabilities of [CSS](https://intl.cloud.tencent.com/document/product/267) to relay streams to CDNs. **CSS** charges you according to the billing rules described in [CDN Relayed Live Streaming](https://intl.cloud.tencent.com/document/product/647/35242).

### Are fees charged if there is only one user in a room?
A room with only one user consumes TRTC’s resources, even if no streams are pushed (no upstream data). The only user in a room cannot subscribe to other users’ streams and therefore won’t receive video data. As a result, the duration is billed as **audio duration**.

### Why is my service status "Disabled"?
- Overdue payments will lead to service suspension. The services will be resumed automatically after you [make the payment](https://console.cloud.tencent.com/expense/overview).
- If you manually disabled an application, you can click **Enable Application** to resume TRTC services for the application.
