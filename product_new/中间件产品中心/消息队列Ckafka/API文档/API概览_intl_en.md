## Topic-related APIs
| Feature | Action ID | Description |
|---------|---------|---------|
| Create Topic | CreateTopic | Used to create a topic on a CKafka instance |
| SetTopicAttributes | SetTopicAttributes | Used to modify the attributes of a topic on a CKafka instance |
| Delete Topic | DeleteTopic | Used to delete a topic on a CKafka instance |
| Add Partition | AddPartition | Used to add a partition in a topic |
| Getting Topic List | ListTopic | Used to display the topic list on a CKafka instance |
| Get Topic Properties | GetTopicAttributes | Used to get the attributes of a created topic on a CKafka instance |
| Set Message Forwarding | SetForward | Used to configure a forwarding rule for a CKafka topic |


## Instance APIs
| Feature | Action ID | Description
|---------|---------|---------|
| Obtain Instance List | ListInstance | Used to obtain the list of CKafka instances under the user account |
| Get Instance Attributes | GetInstanceAttributes | Used to get the attributes of a created instance |
| Set Instance Attributes| SetInstanceAttributes | Used to set the attributes of a CKafka instance |
| Query Consumer Group Information | ListConsumerGroup | Used to get CKafka consumer group information under the user account |
| Query Consumer Group Information (Lite)| ListGroup | Used to get CKafka consumer group information under the user account. This lite API returns less consumer group information. You can call the GetGroupInfo API to query consumer group details |
| Get Consumer Group Information | GetGroupInfo | Used to get CKafka consumer group details under the user account |
| Get Consumer Group Offset| GetGroupOffsets | Used to get the CKafka consumer group offset under the user account |
| Set Consumer Group Offset | SetGroupOffsets | Used to set the offset of a consumer group on a CKafka instance under the user account |


## Access Control APIs
| Feature | Action ID | Description |
|---------|---------|---------|
| Add Topic Allowlist | AddTopicIpwhitelist | Used to add an IP Allowlist for a topic |
| Delete Topic Allowlist | DeleteTopicIpwhitelist | Used to delete an IP Allowlist for a topic |

## ACL Policy APIs
> The ACL policy feature is in beta. If you want to try this feature in the console, [submit a ticket](https://console.cloud.tencent.com/workorder/category) to be allowlisted.

| Feature | Action ID | Description |
|---------|---------|---------|
| Add User | AddUser | Used to add a user to an instance |
| Delete User | DeleteUser | Used to delete a user from an instance |
| Change Password | ModifyPassword | Used to change the user password |
| Enumerate User Information  | ListUser | Used to enumerate all user information |
| Add ACL Policy | AddAcl | Used to add ACL policies for users of an instance |
| Delete ACL policy | DeleteAcl | Used to delete ACL policies for users of an instance |
| Enumerate ACL Policy | ListAcl | Used to enumerate ACL policies for users of an instance |
