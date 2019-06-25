Log collection feature allows users to specify the Topic of user-built Kafka pod， Topic of specified Tencent Cloud Ckafka pod， and specified CLS log topic as the consumer of log content. Log collection Agent sends collected logs to the specified Topic of specified Kafka or specified CLS log topic.

## Configuring Kafka as Output End of Log

Only Kafka pods without access authentication are supported, and it needs to ensure that all nodes in the cluster can access the Kafka Topic specified by users. Please note that, when Kafka is configured as receiver, the log collection feature only supports Kafka without access authentication.

1. Create log collection rule
![](https://main.qcloudimg.com/raw/e9b7117c6e51282c7fc6cf286a9bf419.png)

2. Specify the collecting source
![](https://main.qcloudimg.com/raw/99c06a48a43d59e5de3644621a237a5d.png)

3. Specify the Topic of Kafka as log receiver
![](https://main.qcloudimg.com/raw/efef2fee715d3d8f6652fab08a148fc2.png)

## Configuring CLS as the log output end

Please note that CLS collects only logs of container clusters in the same region.

1. Create log collection rule
![](https://main.qcloudimg.com/raw/808cf11d046af0b722eab7b611aaac21.png)

2. Specify the collecting source
![](https://main.qcloudimg.com/raw/8fb68a9a2ac662c485cd1f6c4276004b.png)

3. As TKE has independent log collection capability, you don't need to select Agent creating a log collection
![](https://main.qcloudimg.com/raw/3bfd1d17372aa3beeb17c5ef94fa9c81.png)

4. Specified the log topic as the log receiver
![](https://main.qcloudimg.com/raw/ee87d6aa20adbd0c4d2abd1a460ddf9d.png)





