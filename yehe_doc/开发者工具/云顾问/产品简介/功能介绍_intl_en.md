Advisor inspection items are divided into five dimensions: Security, reliability, service restriction, cost, and performance

### Security

We recommend you enable the Tencent Cloud security features and inspection permissions to improve the system and business security.

<table>
   <tr>
      <td>Service</td>
      <td>Inspection Item</td>
      <td>Description</td>
   </tr>
   <tr>
      <td rowspan="4">Anti-DDoS</td>
      <td>Blocked EIPs</td>
      <td>Check whether there are any EIPs blocked due to DDoS attacks</td>
   </tr>
   <tr>
      <td>Available IP blackhole unblockings</td>
      <td>Check whether the proportion of used blackhole unblockings is excessive</td>
   </tr>
   <tr>
      <td>CC protection status</td>
      <td>Check whether CC protection is enabled for CVM, CLB, and NAT instances</td>
   </tr>
   <tr>
      <td>DDoS protection status</td>
      <td>Check whether DDoS protection is enabled for CVM, CLB, and NAT instances</td>
   </tr>
   <tr>
      <td rowspan="6">COS</td>
      <td>CORS configuration of buckets</td>
      <td>Check the CORS configuration of buckets. If the `CORS Allow-Headers/Expose-Headers` header is not configured, an alarm will be triggered</td>
   </tr>
   <tr>
      <td>Referer hotlink protection configuration of buckets</td>
      <td>Check the referer configuration of COS buckets. If the referer is not configured or an empty referer access rule is configured, an alarm will be triggered</td>
   </tr>
   <tr>
      <td>Referer hotlink protection configuration of buckets</td>
      <td>Check the referer configuration of COS buckets. If the referer is not configured or an empty referer access rule is configured, an alarm will be triggered</td>
   </tr>
   <tr>
      <td>Public read/write permissions of buckets</td>
      <td>Check the public read/write permissions of COS buckets. If the public read/write permissions are set, an alarm will be triggered</td>
   </tr>
   <tr>
      <td>Sub-account access permission not set</td>
      <td>Check the account configuration of COS buckets. If the sub-account access permission is not set, an alarm will be triggered</td>
   </tr>
   <tr>
      <td>Sub-account access permission not restricted</td>
      <td>Check the sub-account permission scope of COS buckets. If a sub-account has full access (COS_ACL_FULL), an alarm will be triggered</td>
   </tr>
   <tr>
      <td rowspan="2">ES</td>
      <td>Elasticsearch component's public network access policy of clusters</td>
      <td>Check the Elasticsearch component's public network access policy of ES clusters. If no restrictions are configured, an alarm will be triggered</td>
   </tr>
   <tr>
      <td>Kibana component's public network access policy of clusters</td>
      <td>Check the Kibana component's public network access policy of ES clusters. If no restrictions are configured, an alarm will be triggered</td>
   </tr>
   <tr>
      <td>CDN</td>
      <td>IP access frequency limit</td>
      <td>Check the IP access frequency limit configuration in CDN. If there are frequent hotlinkings by malicious users, we recommend you enable the limit</td>
   </tr>
   <tr>
      <td>CFW</td>
      <td>Resource protection</td>
      <td>Check the CFW protection policy. If it is not enabled for CVM, NAT, VPN, or CLB instances, an alarm will be triggered</td>
   </tr>
   <tr>
      <td rowspan="3">CVM</td>
      <td>Public login not restricted</td>
      <td>Check the CVM public network access policy. If a public IP is configured for CVM and access to the login port is opened, an alarm will be triggered</td>
   </tr>
   <tr>
      <td>Public access not restricted</td>
      <td>Check the CVM public network access policy. If a public IP is configured for CVM and access from all IPs and ports are opened in the security group, an alarm will be triggered</td>
   </tr>
   <tr>
      <td>Public network ports with high risks enabled</td>
      <td>Check the CVM public network access policy. If a public IP is configured for CVM and access to a high-risk port is opened, an alarm will be triggered</td>
   </tr>
   <tr>
      <td rowspan="3">TencentDB for MySQL</td>
      <td>Restriction of high-risk commands for non-root accounts</td>
      <td>Check the permission scope of TencentDB for MySQL non-root accounts. If a non-root account has permission to run high-risk commands, an alarm will be triggered</td>
   </tr>
   <tr>
      <td>Public network security policy</td>
      <td>Check the public network security policy in TencentDB for MySQL. If public network access is enabled, but no security group rules are configured, an alarm will be triggered</td>
   </tr>
   <tr>
      <td>Root account security</td>
      <td>Check the account configuration of TencentDB for MySQL instances. If only the root account exists, an alarm will be triggered</td>
   </tr>
   <tr>
      <td rowspan="2">TencentDB for Redis</td>
      <td>High-Risk commands</td>
      <td>Check the disabled command configuration of TencentDB for Redis instances. If a high-risk command is not disabled, an alarm will be triggered</td>
   </tr>
   <tr>
      <td>Default account security</td>
      <td>Check the account configuration of TencentDB for Redis instances. If only the default account exists, an alarm will be triggered</td>
   </tr>
</table>

### Reliability

Multidimensional monitoring is supported to keep instances running stably.

<table>
   <tr>
      <td>Service</td>
      <td>Inspection Item</td>
      <td>Description</td>
   </tr>
   <tr>
      <td rowspan="2">CAM</td>
      <td>Account-MFA device binding</td>
      <td>Check whether an account is bound to an MFA device</td>
   </tr>
   <tr>
      <td>Account protection enablement</td>
      <td>Check whether features such as login protection, sensitive operation protection, and remote login protection are enabled</td>
   </tr>
   <tr>
      <td rowspan="2">CBS</td>
      <td>Storage capacity</td>
      <td>Check the storage capacity usage of CBS cloud disks. If the capacity utilization is excessive, an alarm will be triggered</td>
   </tr>
   <tr>
      <td>Storage capacity</td>
      <td>Check the storage capacity usage of CBS cloud disks. If the capacity utilization is excessive, an alarm will be triggered</td>
   </tr>
   <tr>
      <td rowspan="2">COS</td>
      <td>Bucket versioning</td>
      <td>Check the versioning configuration of COS buckets. If it is not enabled, an alarm will be triggered</td>
   </tr>
   <tr>
      <td>Log management configuration of buckets</td>
      <td>Check the log management feature of COS buckets. If it is not configured, an alarm will be triggered</td>
   </tr>
   <tr>
      <td rowspan="4">CVM</td>
      <td>System disk snapshot</td>
      <td>Check CVM system disk snapshots. If no snapshots are created, an alarm will be triggered</td>
   </tr>
   <tr>
      <td>Excessive instance disk space utilization</td>
      <td>Check the disk utilization of CVM instances. If the utilization is excessive, an alarm will be triggered</td>
   </tr>
   <tr>
      <td>Instance local disk type</td>
      <td>Check the local disk usage of CVM instances. If an instance is not an I/O or Big Data model but uses a local disk, an alarm will be triggered</td>
   </tr>
   <tr>
      <td>Excessive bandwidth utilization</td>
      <td>Check the bandwidth utilization of CVM instances. If the utilization is excessive, an alarm will be triggered</td>
   </tr>
   <tr>
      <td>Anti-DDoS</td>
      <td>Layer-7 forwarding rule health check</td>
      <td>Check whether any exceptions exist in the health check of current layer-7 forwarding rules</td>
   </tr>
   <tr>
      <td>ES</td>
      <td>Automatic snapshot backup of clusters</td>
      <td>Check the automatic snapshot backup configuration of ES clusters. If backup is not configured, an alarm will be triggered</td>
   </tr>
   <tr>
      <td>TencentDB for MongoDB</td>
      <td>Oplog retention duration</td>
      <td>Check the oplog retention duration of TencentDB for MongoDB instances. If it is too short, an alarm will be triggered</td>
   </tr>
   <tr>
      <td rowspan="4">TencentDB for MySQL</td>
      <td>Automatic backup</td>
      <td>Check the automatic backup configuration of TencentDB for MySQL instances. If backup is not enabled, an alarm will be triggered</td>
   </tr>
   <tr>
      <td>Cross-Region disaster recovery</td>
      <td>Check the disaster recovery instance configuration of TencentDB for MySQL instances. If no such instances are configured, an alarm will be triggered</td>
   </tr>
   <tr>
      <td>Source-Replica delay</td>
      <td>Check the source-replica delay of TencentDB for MySQL instances. If the delay is excessive, an alarm will be triggered</td>
   </tr>
   <tr>
      <td>Cross-AZ deployment</td>
      <td>Check whether TencentDB for MySQL instances are deployed across AZs. If an instance is not deployed across AZs, an alarm will be triggered</td>
   </tr>
   <tr>
      <td rowspan="2">TencentDB for Redis</td>
      <td>Automatic backup</td>
      <td>Check the automatic backup configuration of TencentDB for Redis instances. If automatic backup is not enabled, an alarm will be triggered</td>
   </tr>
   <tr>
      <td>Cross-AZ deployment</td>
      <td>Check whether TencentDB for Redis instances are deployed across AZs. If an instance is not deployed across AZs, an alarm will be triggered</td>
   </tr>
   <tr>
      <td rowspan="3">TDMQ</td>
      <td>Cluster health check</td>
      <td>Check the health status of TDMQ clusters</td>
   </tr>
   <tr>
      <td>Backup consumer</td>
      <td>Check whether TDMQ subscription has backup consumers</td>
   </tr>
   <tr>
      <td>Dead letter queue</td>
      <td>Check whether there are any dead letter queues under TDMQ namespaces</td>
   </tr>
   <tr>
      <td rowspan="2">TDSQL</td>
      <td>Replica lag</td>
      <td>Check the replica lag of TDSQL instances. If the lag is excessive, an alarm will be triggered</td>
   </tr>
   <tr>
      <td>Replica lag</td>
      <td>Check the replica lag of TDSQL instances. If the lag is excessive, an alarm will be triggered</td>
   </tr>
   <tr>
      <td rowspan="3">TKE</td>
      <td>Cluster pod assignment rate</td>
      <td>Check whether the maximum number of pods that can be created in a TKE cluster is too small</td>
   </tr>
   <tr>
      <td>Cross-AZ cluster node deployment</td>
      <td>Check whether TKE nodes are deployed across AZs</td>
   </tr>
   <tr>
      <td>Node status</td>
      <td>Check the status of TKE nodes. If it is `NotReady`, an alarm will be triggered</td>
   </tr>
</table>


### Service restriction

Advisor can monitor the maximum number of available service resources to prompt you to delete resources or apply to increase the quota based on the suggestions.  

<table>
   <tr>
      <td>Service</td>
      <td>Inspection Item</td>
      <td>Description</td>
   </tr>
   <tr>
      <td>CFW</td>
      <td>Rule quota</td>
      <td>Check the CFW rule list quota. If the quota is not sufficient, an alarm will be triggered</td>
   </tr>
   <tr>
      <td rowspan="2">TencentDB for MongoDB</td>
      <td>Instance expiration</td>
      <td>Check whether TencentDB for MongoDB instances have expired. If a monthly subscribed instance is about to expire but auto-renewal is not configured, an alarm will be triggered</td>
   </tr>
   <tr>
      <td>Storage capacity</td>
      <td>Check the storage capacity utilization of TencentDB for MongoDB instances. If the utilization is excessive, an alarm will be triggered</td>
   </tr>
   <tr>
      <td rowspan="3">TencentDB for MySQL</td>
      <td>Instance expiration</td>
      <td>Check whether TencentDB for MongoDB instances have expired. If a monthly subscribed instance is about to expire but auto-renewal is not configured, an alarm will be triggered</td>
   </tr>
   <tr>
      <td>Connection utilization</td>
      <td>Check the connection utilization of TencentDB for MySQL instances. If the utilization is excessive, an alarm will be triggered</td>
   </tr>
   <tr>
      <td>Disk utilization</td>
      <td>Check the disk utilization of TencentDB for MySQL instances. If the utilization is excessive, an alarm will be triggered</td>
   </tr>
   <tr>
      <td>TencentDB for Redis</td>
      <td>Instance expiration</td>
      <td>Check whether TencentDB for Redis instances have expired. If a monthly subscribed instance is about to expire but auto-renewal is not configured, an alarm will be triggered</td>
   </tr>
   <tr>
      <td rowspan="2">TDSQL</td>
      <td>Connection utilization</td>
      <td>Check the connection utilization of TDSQL instances. If the utilization is excessive, an alarm will be triggered</td>
   </tr>
   <tr>
      <td>Data disk utilization</td>
      <td>Check the data disk utilization of TDSQL instances. If the utilization is excessive, an alarm will be triggered</td>
   </tr>
</table>


### Cost

Advisor can provide suggestions for more cost-effective configurations based on the running status of resources to reduce the costs.

<table>
   <tr>
      <td>Service</td>
      <td>Inspection Item</td>
      <td>Description</td>
   </tr>
   <tr>
      <td>CBS</td>
      <td>Underutilization</td>
      <td>Check the mounting and I/O status of CBS disks.</td>
   </tr>
   <tr>
      <td rowspan="2">COS</td>
      <td>Bucket lifecycle configuration</td>
      <td>Check the lifecycle rules of COS buckets. If no rules are configured, an alarm will be triggered</td>
   </tr>
   <tr>
      <td>Incomplete multipart uploads in buckets</td>
      <td>Check the incomplete multipart upload clearing rules of COS buckets. If no rules are configured, an alarm will be triggered</td>
   </tr>
   <tr>
      <td>CVM</td>
      <td>Billing mode</td>
      <td>Check whether CVM instances are in pay-as-you-go billing mode for a long period of time (more than 2 months)</td>
   </tr>
   <tr>
      <td>EIP</td>
      <td>Idle EIPs</td>
      <td>Check EIP binding information. If an EIP has not been bound to a cloud resource (CVM instance, NAT Gateway, EIP, or high-availability VIP), an alarm will be triggered</td>
   </tr>
</table>

### Performance

Advisor provides performance improvement suggestions based on the resource usage monitored during instance operations and best practices.

<table>
   <tr>
      <td>Service</td>
      <td>Inspection Item</td>
      <td>Description</td>
   </tr>
   <tr>
      <td rowspan="7">CDN</td>
      <td>Single-Link downstream speed limit configuration</td>
      <td>Check the single-link downstream speed limit configuration in CDN</td>
   </tr>
   <tr>
      <td>Special header caching configuration of origin servers</td>
      <td>Check the header caching configuration of CDN origin servers</td>
   </tr>
   <tr>
      <td>Bandwidth cap configuration</td>
      <td>Check the bandwidth cap configuration. If the cap is not disabled, an alarm will be triggered</td>
   </tr>
   <tr>
      <td>Expiration of certificate bound to domain names</td>
      <td>Check the certificate validity period. If it will expire in one month, an alarm will be triggered</td>
   </tr>
   <tr>
      <td>Cache hit rate</td>
      <td>Check the cache hit rate. If it is too low, an alarm will be triggered</td>
   </tr>
   <tr>
      <td>Error code proportion</td>
      <td>Check the error code proportion. If it is excessive, an alarm will be triggered</td>
   </tr>
   <tr>
      <td>Standby origin server</td>
      <td>If the primary origin server does not use COS, we recommend you configure a standby origin server</td>
   </tr>
   <tr>
      <td>COS</td>
      <td>5xx error rate</td>
      <td>Check COS status codes. If there are too many 5XX status codes with a high occurrence frequency, an alarm will be triggered</td>
   </tr>
   <tr>
      <td  rowspan="2">TencentDB for MongoDB</td>
      <td>Dirty data in cache</td>
      <td>Check the dirty data in TencentDB for MongoDB. If the cache dirty data has a high proportion, an alarm will be triggered</td>
   </tr>
   <tr>
      <td>CPU utilization</td>
      <td>Check the CPU utilization of TencentDB for MongoDB instances. If the utilization is excessive, an alarm will be triggered</td>
   </tr>
   <tr>
      <td>TencentDB for MySQL</td>
      <td>CPU utilization</td>
      <td>Check the CPU utilization of TencentDB for MySQL instances. If the utilization is excessive, an alarm will be triggered</td>
   </tr>
   <tr>
      <td rowspan="2">TencentDB for Redis</td>
      <td>Outbound traffic throttling triggered on proxy nodes</td>
      <td>Check the number of trigger times of outbound traffic throttling on TencentDB for Redis proxy nodes. If it is excessive, an alarm will be triggered</td>
   </tr>
   <tr>
      <td>Node CPU utilization</td>
      <td>Check the CPU utilization of TencentDB for Redis nodes</td>
   </tr>
   <tr>
      <td>TDSQL</td>
      <td>CPU utilization</td>
      <td>Check the CPU utilization of TDSQL instances. If the utilization is excessive, an alarm will be triggered</td>
   </tr>
</table>
