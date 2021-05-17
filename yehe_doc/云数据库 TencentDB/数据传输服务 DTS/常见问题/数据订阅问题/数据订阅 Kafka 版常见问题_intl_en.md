### Why can't I consume data?
- Check the network. The address of the Kafka server is a Tencent Cloud private network address, which can only be accessed in Tencent Cloud VPC that is in the same region of the subscribed instance.
- Check whether the subscription topic, private network address, consumer group name, account or password is correct. You can click the subscription name on the [Data Subscription console](https://console.cloud.tencent.com/dts/dss) to go to the subscription details page and consumption management page to view such information.
- Check whether the encryption parameter is correct. For more information, see [What authentication mechanism does Kafka use?](#faq3).

### What is the data format?
Data Subscription Kafka Edition uses Protobuf for data serialization. You can click [here](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/subscribe.proto) to download the Protobuf file. A demo project also contains the Protobuf file. For more information, see the “Key Demo Logic Description” section of [Data Consumption Demo](https://intl.cloud.tencent.com/document/product/571/39538).

### [What authentication mechanism does Kafka use?](id:faq3)
See the figure below:
![](https://main.qcloudimg.com/raw/83aa8f6122ee106f57568b6f25a1bd08.png)

### When does Kafka commit?
Please first set the `enable_auto_commit` parameter of Kafka as `false` to disable auto commit. The producer inserts a checkpoint message at an appropriate position in the message sequence. After the checkpoint message is consumed, the Kafka client will commit feedback indicating the consumption is completed, so as to ensure message integrity.

### How long are messages in the Kafka client retained? How do I set the consumer offset?
Messages in the Kafka client are retained for 1 day. You can set the `auto_offset_reset` parameter of Kafka as `earliest` or `latest` as needed. If you need to consume data from a specific offset, you can reset the consumer offset with the seek feature of the Kafka client.
