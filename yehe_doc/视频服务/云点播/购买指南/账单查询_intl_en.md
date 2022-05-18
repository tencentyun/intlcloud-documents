To view your VOD bills and payment details, go to Tencent Cloud **Billing Center**  > **Bills** > **[Bill Details](https://console.cloud.tencent.com/expense/bill/summary)**.


## Bill Details

The Bill Details page includes the **Bill by Instance** and **Bill Details** tabs:
- Bill by Instance: displays aggregated bills by instance.
- Bill Details: displays one record per bill without performing aggregation.


### Bill by Instance

Click **All products** and then select **VOD** to view the VOD bills.

#### Bill fields
| Field | Description |
-|-
Billing Cycle| <ul style="margin:0;"><li >Daily billing cycle: fees are deducted daily<li >Monthly billing cycle: fees are deducted monthly
Configuration Description|VOD sub-features and their usage in this month. VOD sub-features include:<ul style="margin:0;"><li >VOD storage <li >VOD transcoding <li >VOD traffic <li >VOD bandwidth <li >VOD inappropriate content recognition
Original Cost|Total fees of the sub-features used in this month
Discount Rate|The user’s discount rate this month:<ul style="margin:0;"><li >Users on the daily billing cycle do not receive discounts. Their discount rate is 0.<li >Users on the monthly billing cycle should contact sales to inquire about discounts.
Total Cost|Total cost = Original cost × (1 - Discount rate)

Other fields are assigned by Tencent Cloud. For details, see [Bills](https://intl.cloud.tencent.com/document/product/555/7432).
>? If the component type is **VOD transcoding**, the transcoding template type is indicated in the instance ID. For example:
>- `XXX_h265_sd_640_480` indicates a general transcoding template with codec set to H.265 and resolution set to SD (640 × 480) and below.
>- `XXX_h265_eshd_sd_640_480` indicates a TESHD template with codec set to H.265 and resolution set to SD (640 × 480) and below.

### Bill Details

#### Bill fields
| Field | Description |
-|-
Component Type|VOD sub-feature used in this month
Component Name|Sub-item under this component type
Component’s Published Unit Price|The component’s published unit price without discounts
Component’s Usage|The usage of this component
Discount Rate|The user’s discount rate this month:<ul style="margin:0;"><li >Users on the daily billing cycle do not receive discounts. Their discount rate is 0.<li >Users on the monthly billing cycle will receive discounts and should contact sales for more information.
Usage Duration| Total usage duration of the component
Total Cost| Total cost = Component’s original cost x (1 - Discount rate). <br>Component’s original cost = Component’s published unit price x Component’s price unit x Component’s usage x Usage duration

Other fields are assigned by Tencent Cloud. For details, see [Bills](https://intl.cloud.tencent.com/document/product/555/7432).
>? If the component type is **VOD transcoding**, the transcoding template type is indicated in the instance ID. For example:
>- `XXX_h265_sd_640_480` indicates a general transcoding template with codec set to H.265 and resolution set to SD (640 × 480) and below.
>- `XXX_h265_eshd_sd_640_480` indicates a TESHD transcoding template with codec set to H.265 and resolution set to SD (640 × 480) and below.

For example, suppose a user uses the template with codec set to H.264 and resolution set to HD (1280 × 720) and below, and the component’s published unit price is 0.0061 USD/min.
- Component’s original cost = 0.00610000 × USD/Transcoding type 2/min × 2.00000000 min × 5.00000000 min = 0.03050000 (USD)
- Discount rate = 0

Total cost = 0.0305 USD × 1 = 0.0305 (USD)

<span id="p2"></span>
### VOD bill-by-traffic
- Billing mode: Bill-by-traffic
- Valid days: The number of valid calendar days used for monthly billing
- Billing traffic: The amount of consumed traffic used for billing
Traffic consumption is recorded every five minutes by calendar day, and the total billed traffic is the sum of the traffic of all recorded time points.

<span id="p3"></span>
### VOD pay-as-you-go storage
- Date: A valid calendar day used for monthly billing
- Usage: Peak VOD storage usage in the day
>! Monthly storage cost = Total daily peak storage usage × Unit price (the VOD console displays the peak storage usage of the current day)

<span id="p4"></span>
#### VOD transcoding
- Date: A calendar day
- Appid: User account ID
- Task ID: ID of the executed task
- Transcoding type: General transcoding, TESHD transcoding, audio transcoding, and video editing.
- Codec: H.264, H.265
- Definition: The definition as specified in the transcoding template
- Transcoding duration: Transcoding duration of the day

<span id="p5"></span>
### VOD video inappropriate content recognition
- Date: A calendar day
- Usage: Video duration for inappropriate content recognition in the day




