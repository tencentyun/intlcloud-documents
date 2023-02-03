### Does an Anti-DDoS Pro instance take effect immediately after purchase?
It will take effect immediately after successful purchase and access.

### How is the 95th percentile bandwidth calculated?
In each calendar month, the inbound/outbound bandwidth is sampled every 5 minutes and the maximum is taken as the peak bandwidth on each day. At the end of the month, the sampled values are sorted from highest to lowest, and the top 5% are removed. The 95th largest value is the billable bandwidth of the month.

For example, one traffic point is taken every 5 minutes in a month, so there are 12 points in an hour, 12 * 24 points in a day, 12 * 24 * 30 = 8640 points in the month (30 days); the highest 5% of values are removed, and the remaining highest bandwidth is the billable 95th percentile bandwidth.


### What are the billing differences between the full protection of Anti-DDoS Pro and resilient protection of Anti-DDoS Advanced?
When an attack occurs, the maximum DDoS protection capability of Tencent Cloud in the region of the Anti-DDoS Pro instance will be automatically called to provide full protection, which is included in the instance and will not incur additional resilient protection fees.
The resilient protection of Anti-DDoS Advanced is billed by the bandwidth of the resilient protection range corresponding to the maximum attack traffic generated on the day.

