The new version of CKafka supports fine-grained configuration of topic parameters. You can set the following parameters in **Topic Management** > **Edit** > **Advanced Configuration**:
![](https://main.qcloudimg.com/raw/7e08a1dcda6baf1eb3100351cb7983b0.png)

Parameter description:

| Parameter Name | Default Value | Value Range | Description |
| :-------- | :--------| :------ |:------ |
| cleanup.policy|delete|delete/compact | It allows you to delete logs by storage time or compress them by key (the compact mode is required for Kafka Connect). |
| min.insync.replicas | 1 |-| When the producer sets `request.required.acks` to 1, min.insync.replicas specifies the minimum number of replicas. |
| unclean.leader.election.enable | true | true/false | Specifies whether a replica not in ISR can be set as a leader. |
| segment.ms |-| 1-30 days | The segment rolling duration in ms, with a minimum of 86,400,000 ms. |
| retention.ms | The message retention period for the instance by default | 60,000 ms to 30 days | The message retention period at the topic level. |
| max.message.bytes |-| 0B - 8 MB| The maximum message size at the topic level. If this parameter is left empty, the message size will be 1 MB by default. |
