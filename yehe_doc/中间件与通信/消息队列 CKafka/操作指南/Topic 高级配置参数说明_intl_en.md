## Operation Scenarios
The new version of CKafka supports fine-grained configuration of topic parameters in the CKafka Console.

## Prerequisites
- You have [created an instance](https://intl.cloud.tencent.com/document/product/597/32543).
- You have [created a topic](https://intl.cloud.tencent.com/document/product/597/34003).

## Directions
1. Log in to the [CKafka Console](https://console.cloud.tencent.com/ckafka).
2. In the instance list, click the target instance ID to enter the **Topic Management** tab.
3. Click **Edit** > **Show advanced configuration** in the "Operation" column to set the following parameters:
![](https://main.qcloudimg.com/raw/7e08a1dcda6baf1eb3100351cb7983b0.png)

Parameter description:

| Parameter Name | Default Value | Value Range | Description |
| :-------- | :--------| :------ |:------ |
| cleanup.policy|delete|delete/compact | Log can be deleted by retention time or can be compacted by key (the compact mode is required for Kafka Connect). |
|min.insync.replicas|1|-| When "producer" sets "request.required.acks" to 1, "min.insync.replicas" will specify the minimum number of replicas. |
| unclean.leader.election.enable | true | true/false | Specifies whether a replica not in ISR can be set as a leader. |
|segment.ms|-|1–90 days| Segment shard rolling duration in ms. Minimum value: 86,400,000 ms. |
| retention.ms | Message retention period for instance by default | 60,000 ms–90 days | Message retention period at the topic level. |
| max.message.bytes |-| 0B–8 MB| Maximum message size at the topic level. If this parameter is left empty, the message size will be 1 MB by default. |
