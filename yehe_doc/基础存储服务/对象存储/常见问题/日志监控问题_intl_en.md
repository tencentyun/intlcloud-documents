## Logging

### Does COS provide file upload, download, and deletion logs?
COS provides the [logging](https://intl.cloud.tencent.com/document/product/436/16920) feature, which records the access details of a source bucket. These logs are then stored in a destination bucket for better bucket management. To get the file upload, download, and deletion logs, enable access logging to record file operations.

### How do I query which files incur the most public network traffic in COS?

You can use the [logging](https://intl.cloud.tencent.com/document/product/436/16920) feature of COS to download bucket access logs and write a program to analyze which files consume the most public network traffic. You can also load the logs to Data Lake Compute (DLC) for statistics collection.

### How do I query from which source IPs most public network traffic in COS comes from?
You can use the [logging](https://intl.cloud.tencent.com/document/product/436/16920) feature of COS to download bucket access logs and write a program to analyze from which source IPs most public network traffic comes from. You can also load the logs to DLC for statistics collection.

### Can I set thresholds for public network downstream traffic and request count in COS?
You can [set an alarm policy](https://intl.cloud.tencent.com/document/product/248/38916) in the [CM console](https://console.cloud.tencent.com/monitor) to receive alarm notifications when the public network downstream traffic in COS reaches the threshold. COS currently can't automatically suspend the service when the threshold is reached.

### How do I view file deletion logs?

You can query the logs shipped by the [logging](https://intl.cloud.tencent.com/document/product/436/16920) feature to view file deletion logs. After access logging is enabled, you can load log files to DLC to filter deletion logs. Below is a sample deletion log. You can search for the `DELETE` operation in the `reqMethod` field to get such logs:

```plaintext
1.0 examplebucket-125000000 ap-chengdu 2020-02-10T13:07:00Z examplebucket-125000000.cos.ap-chengdu.myqcloud.com DELETEObject 110.110.110.110 AKIDSuCmiBvppcdxShtPrCjhEUPF****-J6AsmEPu8NYMOhgx3HLExh - 0 0 / DELETE tencentcloud-cos-console 200 - - 746 146 USER - 100009682373 - 100009682373:100009682373 NWU0MTU1NzRfNWNiMjU4NjRfM2JkMV8yNGFiNGEw - - - - DELETE /filepath HTTP/1.1
```

If you cannot find deletion logs among access logs, check whether rules of deletion upon expiration are set in the [lifecycle configuration](https://intl.cloud.tencent.com/document/product/436/14605).

### How do I query COS bucket configuration logs?

Bucket configuration logs are shipped to CloudAudit. You can search for such logs as instructed in [Viewing Event Details in Operation Record](https://intl.cloud.tencent.com/document/product/1021/40499).


### Where can I query bucket creation and deletion logs?

Bucket creation and deletion logs are shipped to CloudAudit. You can select `DeleteBucket` and `PutBucket` events to filter operation logs as instructed in [Viewing Event Details in Operation Record](https://intl.cloud.tencent.com/document/product/1021/40499).



## Monitoring

### Can traffic be throttled in COS?

No. However, you can [create an alarm policy](https://intl.cloud.tencent.com/document/product/248/38916) in **CM** to trigger alarms and push notifications by email or SMS when the traffic reaches a certain threshold.

### Why does the request count or traffic on the monitoring dashboard increase suddenly?

If your business has an abnormal surge in the request count or traffic, your business may be hotlinked. You need to check whether public read is enabled for your bucket. We recommend you not enable public read, as it will bring uncontrollable risks to your business. You can grant access according to the [principle of least privilege](https://intl.cloud.tencent.com/document/product/436/32972).

If you must use public read, we recommend you use the following methods to guarantee the bucket security:
1. Enable the [logging](https://intl.cloud.tencent.com/document/product/436/16920) feature for your bucket to log bucket access requests.
2. Enable the [hotlink protection](https://intl.cloud.tencent.com/document/product/436/32466) feature to block access requests from abnormal IPs.
3. [Create a COS alarm policy](https://intl.cloud.tencent.com/document/product/248/38916) and set a threshold, so that alarm notifications will be sent to you by SMS or email once the traffic exceeds the threshold.
