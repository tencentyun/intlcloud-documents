The process of accessing CKafka varies according to the network type:

- Access via a VPC: you can use the VPC of an existing CVM to access the CKafka service, eliminating the need to add an extra route.
- Access via a public route: you need to enable an independent public route and configure an ACL policy for the topic.

### Flowchart

![](https://main.qcloudimg.com/raw/30e64181949f2df1bc21cb81dbf2d020.png)

