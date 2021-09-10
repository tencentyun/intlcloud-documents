<dx-fold-block title="Traffic Throttling Mechanism Description">
Kafka's traffic throttling mechanism is soft throttling; that is, when the user's traffic exceeds the quota, it uses the delayed response method for processing instead of returning an error to the client.

Take API traffic throttling as an example:

**Hard traffic throttling**: if the call rate is 100 times/s, when the client calls more than 100 times per second, the server will return an error, and the client needs to process it according to the business logic.

**Soft traffic throttling**: if the call rate is 100 times/s, and the normal duration is 10 ms, when the client calls more than 100 times per second:
- If it is 110 times, this request will take 20 ms.
- If it is 200 times, this request will take 50 ms. In this case, throttling is friendly to the client, no error alarms will be triggered due to traffic surges or fluctuations, and the business can continue normally.

Therefore, in high-traffic scenarios such as Kafka, soft traffic throttling is better for a smooth user experience.

<dx-alert infotype="explain">
<ul>
Relationship between purchased bandwidth and production/consumption bandwidth:
<li>Maximum production bandwidth (per second) = purchased bandwidth/number of replicas</li>
<li>Maximum consumption bandwidth (per second) = purchased bandwidth</li> 
</ul>
</dx-alert>


<dx-fold-block title="How Delayed Response Works">
The underlying traffic throttling mechanism of a CKafka instance is implemented based on token bucket. Each second is divided into multiple time buckets measured in ms.

The traffic throttling policy divides every second (1000 ms) into several time buckets. For example, if one second is divided into 10 time buckets, then the time of each bucket is 100 ms, and the traffic throttling threshold of each time bucket is 1/10 of the total instance specification speed. If the TCP request traffic in a certain time bucket exceeds such threshold, the delayed response time of the request will be increased according to the internal traffic throttling algorithm, so that the client cannot quickly receive the TCP response, thus achieving the traffic throttling effect in a period of time.

![](https://main.qcloudimg.com/raw/08c055819baed6c403ef38c7ca42c0aa.png)
</dx-fold-block>


### Why is traffic throttling triggered when the monitored production/consumption traffic is lower than the instance specification?

As mentioned above, traffic throttling is measured in ms, but the monitoring platform in the console collects data at the second level and aggregates the data at the minute level (maximum or average value).

According to the principle of token bucket, a single bucket does not force throttle the traffic. Suppose the bandwidth specification of instance A is 100 MB/s, then the traffic throttling threshold of each 100-ms time bucket is 100 MB/10 = 10 MB/bucket. If the production traffic of instance A reaches 30 MB in the first 100-ms time bucket of a certain second (3 times the threshold), then the broker's traffic throttling policy will be triggered to increase the delayed response time. Suppose the original normal TCP response time is 100 ms, then the delay may be increased by 500 ms before response after the threshold is exceeded. The final traffic in this second is 30 MB * 1 + 0 MB * 5 + 10 MB * 4 = 70 MB, so the traffic speed in this second (70 MB/s) is lower than the instance specification (100 MB/s).

![](https://main.qcloudimg.com/raw/6fc11aa3b0dceb38dcc6bb5477e4851a.png) 

### Why is the peak production/consumption traffic higher than the instance specification?

Suppose again the bandwidth specification of instance A is 100 MB/s, then the traffic throttling threshold of each 100-ms time bucket is 10 MB. If the production traffic of instance A reaches 70 MB in the first 100-ms time bucket of a certain second (7 times the threshold), then the broker's traffic throttling policy will be triggered to increase the delayed response time. Suppose the original normal TCP response time is 100 ms, then the delay may be increased by 800 ms before response after the threshold is exceeded. After the response is returned at the 900th ms, the client immediately injects 70 MB of traffic into the 10th time bucket. The final traffic in this second is (70 MB * 1 + 0 MB * 8 + 70 MB * 1) = 140 MB, so the traffic speed in this second (140 MB/s) is higher than the instance specification (100 MB/s).

![](https://main.qcloudimg.com/raw/726f5a605fde9b087c818134124e887e.png) 

### Why does the number of traffic throttling events surge?

The number of traffic throttling events is counted based on TCP requests. If instance A exceeds the traffic threshold in the first time bucket in a certain second, all TCP requests in the remaining time of this time bucket after the threshold is exceeded will be throttled and counted as traffic throttling events.

### How does CKafka throttle traffic?

To ensure stability of the service, CKafka implement network traffic control strategies on both inputting and outputting messages.

- Throttling occurs when the total traffic of the user's all replicas exceeds the purchased peak traffic.
- When the producer side is throttled, CKafka will extend the response time of a TCP connection. The delay period depends on how much the instantaneous traffic exceeds the limit. It is similar to the principle of road traffic control. The more traffic flow, the higher the delay value from the delay algorithm, up to 5 minutes.
- When the consumer side is throttled, CKafka will reduce the size of each `fetch.request.max.bytes` request to control the traffic.

### How do I determine whether CKafka has been throttled?

1. In the instance list, you can see the health status of each cluster. If it's "Warning", you can hover your mouse over it to view the detailed data. The data displays your peak traffic and the throttling times, by which you can determine whether this instance has been throttled.

2. You can click the **Monitor** tab to view the max traffic value. If **the value of max traffic multiplied by replica quantity is greater than that of the purchased peak bandwidth**, you can determine that at least one throttling has occurred. You can also configure an alarm for traffic throttling to check whether throttling occurs.
   ![](https://main.qcloudimg.com/raw/3c0b2b6346b358287eea11c3f889b90d.png)

3. A monitoring chart for displaying the number of traffic throttling times will be added in the console.
