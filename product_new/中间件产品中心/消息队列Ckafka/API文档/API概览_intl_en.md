## Topic-related APIs
| Feature | Action ID | Description |
|---------|---------|---------|
| [Create Topic](https://cloud.tencent.com/document/product/597/10096) | CreateTopic | Used to create a topic on a CKafka instance |
| [Set Topic Attributes](https://cloud.tencent.com/document/product/597/10098) | SetTopicAttributes | Used to modify the attributes of a topic on a CKafka instance |
| [Delete Topic](https://cloud.tencent.com/document/product/597/10099) | DeleteTopic | Used to delete a topic on a CKafka instance |
| [Add Partition](https://cloud.tencent.com/document/product/597/10100) | AddPartition | Used to add a partition in a topic |
| [Getting Topic List](https://cloud.tencent.com/document/product/597/10101) | ListTopic | Used to display the topic list on a CKafka instance |
| [Get Topic Properties](https://cloud.tencent.com/document/product/597/10102) | GetTopicAttributes | Used to get the attributes of a created topic on a CKafka instance |
| [Set Message Forwarding](https://cloud.tencent.com/document/product/597/17451) | SetForward | Used to configure a forwarding rule for a CKafka topic |


## Instance APIs
| Feature | Action ID | Description
|---------|---------|---------|
| [Obtain Instance List](https://cloud.tencent.com/document/product/597/10093) | ListInstance | Used to obtain the list of CKafka instances under the user account |
| [Get Instance Attributes](https://cloud.tencent.com/document/product/597/10094) | GetInstanceAttributes | Used to get the attributes of a created instance |
| [Set Instance Attributes](https://cloud.tencent.com/document/product/597/10095) | SetInstanceAttributes | Used to set the attributes of a CKafka instance |
| [Query Consumer Group Information](https://cloud.tencent.com/document/product/597/18339) | ListConsumerGroup | Used to get CKafka consumer group information under the user account |
| [Query Consumer Group Information (Lite)](https://cloud.tencent.com/document/product/597/30028)| ListGroup | Used to get CKafka consumer group information under the user account. This lite API returns less consumer group information. You can call the GetGroupInfo API to query consumer group details |
| [Get Consumer Group Information](https://cloud.tencent.com/document/product/597/30029) | GetGroupInfo | Used to get CKafka consumer group details under the user account |
| [Get Consumer Group Offset](https://cloud.tencent.com/document/product/597/30030) | GetGroupOffsets | Used to get the CKafka consumer group offset under the user account |
| [Set Consumer Group Offset](https://cloud.tencent.com/document/product/597/30058) | SetGroupOffsets | Used to set the offset of a consumer group on a CKafka instance under the user account |


## Access Control APIs
| Feature | Action ID | Description |
|---------|---------|---------|
| [Add Topic Whitelist](https://cloud.tencent.com/document/product/597/10103) | AddTopicIpwhitelist | Used to add an IP whitelist for a topic |
| [Delete Topic Whitelist](https://cloud.tencent.com/document/product/597/10104) | DeleteTopicIpwhitelist | Used to delete an IP whitelists for a topic |

## ACL Policy APIs
> The ACL policy feature is in beta. If you want to try this feature in the console, [submit a ticket](https://console.cloud.tencent.com/workorder/category) to be whitelisted.

| Feature | Action ID | Description |
|---------|---------|---------|
| [Add User](https://cloud.tencent.com/document/product/597/32983) | AddUser | Used to add a user to an instance |
| [Delete User](https://cloud.tencent.com/document/product/597/32984) | DeleteUser | Used to delete a user from an instance |
| [Change Password](https://cloud.tencent.com/document/product/597/32985) | ModifyPassword | Used to change the user password |
| [Enumerate User Information](https://cloud.tencent.com/document/product/597/32986) | ListUser | Used to enumerate all user information |
| [Add ACL Policy](https://cloud.tencent.com/document/product/597/32987) | AddAcl | Used to add ACL policies for users of an instance |
| [Delete ACL policy](https://cloud.tencent.com/document/product/597/32988) | DeleteAcl | Used to delete ACL policies for users of an instance |
| [Enumerate ACL Policy](https://cloud.tencent.com/document/product/597/32989) | ListAcl | Used to enumerate ACL policies for users of an instance |




