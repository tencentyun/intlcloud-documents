### How long are CFW logs stored by default? What is the maximum storage capacity?
- By default, CFW stores logs within 7 days for free, with the maximum storage capacity being 50 GB.
- After the log analysis service is enabled, CFW will store logs within 6 months by default, with the available storage capacity being 1000 GB at least and 300 TB at most.

### What if the log storage duration or capacity exceeds the quota specified in the package?
- For default log storage with a capacity of 50 GB, logs preserved for over 7 days or beyond 50 GB will be automatically overwritten.
- After the log analysis service is enabled, logs preserved for over 6 months will be overwritten.
- After the log analysis service is enabled, if the log storage capacity reaches the upper limit, the earliest logs will be automatically overwritten in a rolling way to store the latest logs. If the total capacity of logs preserved in a rolling way is 9 times as large as the purchased capacity, the system will not store new logs any more.
>?For example, if you purchase 1000 GB for log storage, once the log storage capacity reaches 10000 GB, no new logs will be recorded.

- For better log analysis and query, you are advised to [expand log storage capacity](https://buy.cloud.tencent.com/cfw?type=modify&adtag=cfw.from.console.page.buy) or use the [log shipping](https://intl.cloud.tencent.com/document/product/1160/49862#.E6.97.A5.E5.BF.97.E6.8A.95.E9.80.92) feature.

### What is the relationship among log auditing, log analysis, and CLS?
Currently, log auditing is a built-in feature of CFW, which is unrelated to CLS. CFW logs can be shipped so that users can analyze logs themselves.

### What do access control logs, intrusion defense logs, and traffic logs record respectively?
- Access control logs record traffic that hits the access control rules.
- Intrusion defense logs record traffic that hits the intrusion prevention rules.
- Traffic logs record traffic allowed to pass.

### Can I archive logs in CFW?
Yes. You can export and ship logs to the Kafka instances of customers.

### How can I download logs? [](id:question5)
- You can use the log shipping feature to export logs for analysis (ensure that you have purchased a Tencent Cloud Kafka instance). For details about the configuration method, refer to [Log Analysis](https://intl.cloud.tencent.com/document/product/1160/49862).
- Alternatively, log in to the [Cloud Firewall console](https://console.cloud.tencent.com/cfw), select **Log auditing** -> **Traffic logs** in the left navigation pane to enter the traffic log page, and then click ![](https://main.qcloudimg.com/raw/d8210f09d9a1280ad54eb0661eb0cd4f.png) in the upper right corner to download logs.
>?A maximum of 60,000 log records can be exported based on specified search criteria.

### How long does it take to ship logs successfully?
It takes about 1 minute to ship logs, so related log updates may not be included.

### Do shipped logs have any tag to identify the log type?
No. No tags are available to identify the log type. You are advised to select different topics during log shipping to distinguish your logs.

### Why are "Observe" logs still found when the Block mode is enabled?
If any intrusion contains vulnerability attacks and hits virtual patching, the virtual patching will perform blocking automatically, but automatic blocking is not yet supported in basic protection rules currently. Therefore, only the Observe mode is available in basic protection rules. In future versions, automatic blocking with high confidence and permanent blocking will be supported.

### Do traffic logs record IP traffic blocked by ACL or IPS?
No. Traffic logs do not record IP traffic blocked by ACL or IPS. Only allowed traffic is recorded.

### Will logs be generated for blocked attacks?
- ACL: Access data will be blocked in block mode, rule hitting times, and ACL logs will be recorded, but traffic logs will not be recorded.
- Intrusion detection system (IDS): An intrusion detection event will be generated for any intrusion that hits intrusion detection policies. You can view blocking logs by using the log analysis feature.

### How can I figure out whether access or attack is blocked or allowed in shipped logs?
The strategy field in logs indicates whether access is blocked or observed.
>?The strategy field is unavailable for traffic logs.

### Why can't I select a purchased CKafka instance in Supported environment in log shipping?
You need to add an access method to the CKafka instance first. Currently, the public domain access method is available, while supported environment is unavailable yet. For details, go to the [Cloud Kafka console](https://console.cloud.tencent.com/ckafka/index?rid=1).
