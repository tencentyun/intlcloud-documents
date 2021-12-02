The relay feature pulls and pushes contents. You can use relay to quickly pull existing videos or live streaming contents and then push them to the destination URL, without initiating a live streaming session. This feature is billed by the [relay task duration](#time) and the [usage of push to third-party URLs](#third_part).



## Notes
- Billing rules for relay **have taken effect since 00:00, July 1, 2021**. Relay tasks executed after that will incur costs, regardless of when such tasks are created.
- When you are using relay, pulling will generate playback traffic/bandwidth usage. Pulling from source URLs of CSS, VOD, COS, etc. will incur corresponding playback fees as well as download fees.


[](id:time)
## Relay Task Duration

### Pricing
A relay task is billed by duration.

| Billable Item        | Price (USD/Min) |
| ---------------- | ----------------- |
| Relay task duration | 0.00032           |



### Billing
- Billable item: relay task duration
- Billing mode: pay-as-you-go
- Billing cycle: daily billing cycle. Relay fees generated in one day will be deducted at 10 AM the next day. See your billing statement for details.
- Billing rules: duration of relay tasks under execution will be billed. Duration of paused and expired tasks is not billed, and will be billed after task resumption.

>! If pulling fails due to abnormal source contents, the relay task will not stop until the specified end time, and **the corresponding task duration will be billed**.


[](id:third_part)
## Push to Third-Party URLs
>! 
>- For a relay task, pushing to a CSS push URL under the Tencent Cloud account which created the task will not be billed.
>- Pushing to a URL other than a CSS push URL of the current Tencent Cloud account will incur fees for pushing to third-party URLs. 

### Pricing

| Billable Item       | Price (USD/Mbps/Month) | Description              |
| :------------- | :------------------- | :------------------------- |
| Push to third-party URLs | 12.67        | Billed by the corresponding bandwidth usage |


### Billing
- Billing mode: monthly pay-as-you-go
- Billing cycle: monthly billing cycle. Your bill for a month will be generated between the 1st and 3rd day of the next month.
- Billing rules: the concurrent bandwidth usage of all pushes to third-party URLs will be billed. The default billing mode is pay-as-you-go bill-by-average daily peak bandwidth within the billing cycle. If any other monthly bill-by-bandwidth mode is used for the LVB service under the account, that mode will apply to push to third-party URLs.


