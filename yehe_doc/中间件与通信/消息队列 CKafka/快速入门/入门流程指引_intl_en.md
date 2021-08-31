The process of accessing CKafka varies according to the network type:

- Access via a VPC: you can use the VPC of an existing CVM to access the CKafka service, eliminating the need to add an extra route.

- Access via a public network route: you need to enable a separate public route and configure an ACL policy for the topic.

>?Currently, a single broker can support up to 1 MB/s public network bandwidth. As public network access runs the risk of issues such as delay and network environment security, we do not recommend long-term use of public network transfer.

### Operation Procedures
![](https://main.qcloudimg.com/raw/a910d6bff17b993ccc07328fe3c53932.png)

