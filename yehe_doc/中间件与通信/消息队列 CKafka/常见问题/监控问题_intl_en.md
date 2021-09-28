### What is the meaning of the number of instance connections on the instance monitoring page?

It refers to the number of connections between client and server.

### Will traffic throttling be triggered if the number of instance connections on the monitoring page exceeds the maximum value?
The maximum number of connections to an instance is 5,000 by default, and you should determine the threshold based on the percentage of the maximum value. After the number of instance connections exceeds this maximum value, the client cannot create more connections. If this maximum value is unreasonable in your actual business, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=876&level2_id=951&source=0&data_title=%E6%B6%88%E6%81%AF%E6%9C%8D%E5%8A%A1%20CKafKa&level3_id=955&radio_title=%E9%85%8D%E9%A2%9D%E6%8F%90%E5%8D%87%E7%94%B3%E8%AF%B7&queue=81&scene_code=18356&step=2) to increase it.

![](https://main.qcloudimg.com/raw/161ed6ca3a9ea78ed6fa26813e08eeef.png)



### Why are there always heaped messages in some partitions as displayed on the monitoring page?

1. This may be because the consumer has not consumed messages in the partition, but the partition has been producing messages.
   ![](https://main.qcloudimg.com/raw/a24f311ae94f205df0a034e0fd95191b.jpg)

2. This may be because there are not enough consumers in the consumer group or the consumption speed is too low. You can add more consumers to accelerate consumption.

3. The consumer program has a bug, where some partitions are not consumed. In this case, you need to check whether the local logs of the consumer have exceptional information first, and if so, you can try restarting the client to solve the problem. If restart works, you can check the client logs or submit a ticket for assistance.



### Why does a topic have no monitoring data?

1. The client may have no production and consumption. You need to check whether the client has production and consumption by running the native production and consumption commands and then viewing the monitoring data. For detailed directions, please see [Running Kafka Client (Optional)](https://intl.cloud.tencent.com/document/product/597/40969).

2. The monitoring data collection system is faulty. Please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
