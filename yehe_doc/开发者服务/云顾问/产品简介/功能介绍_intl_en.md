Tencent Smart Advisor inspection items cover five dimensions: security, reliability, service restriction, cost, and performance.

## Security[](id:Safety)
We recommend you enable the Tencent Cloud security features and inspection permissions to improve the system and business security.

<table>
   <tr>
      <th>Service</th>
      <th>Inspection Item</th>
      <th>Description</th>
   </tr>
   <tr>
      <td>Network ACL</td>
      <td>Public network access permissions</td>
      <td>Check whether the network ACL policies allow for source IP access through all ports or ports except 80 and 443, and if so, security risks such as unauthorized access and DDoS attacks will occur.</td>
   </tr>
   <tr>
      <td rowspan="2">CAM</td>
      <td>Account-MFA device binding</td>
      <td>Check whether an account is bound to an MFA device, and if not, dynamic verification code-based MFA is not required for account login, reducing the security level.</td>
   </tr>
   <tr>
      <td>Account protection enablement</td>
      <td>Check whether features such as login protection, sensitive operation protection, and remote login protection are enabled, and if not, MFA is not required for corresponding operations, reducing the security level.</td>
   </tr>
   <tr>
      <td>CDN</td>
      <td>IP access frequency limit</td>
      <td>If this feature is not enabled, the number of access requests per second from one single IP/node cannot be limited, making the server vulnerable to high-frequency CC attacks and hotlinking by malicious users.</td>
   </tr>
   <tr>
      <td>CFW</td>
      <td>Resource protection</td>
      <td>Check the CFW protection policy. If it is not enabled for CVM, NAT, VPN, or CLB instances, a risk warning will be triggered.</td>
   </tr>
   <tr>
      <td>CLB</td>
      <td>Expiration of certificates bound to instances</td>
      <td>Check whether the certificates bound to CLB instances have expired.</td>
   </tr>
   <tr>
      <td rowspan="4">COS</td>
      <td>Sub-account access permission not restricted</td>
      <td>Check the sub-account permission scope of COS buckets. If a sub-account has full access to buckets, the buckets might have security risks.</td>
   </tr>
   <tr>
      <td>Public read/write permissions of buckets</td>
      <td>Check the public read/write permissions of COS buckets. If such permissions are set, anonymous user groups can directly read from and write to the corresponding buckets, which brings high security risks. We recommend you not grant such permissions in buckets.</td>
   </tr>
   <tr>
      <td>CORS configuration of buckets</td>
      <td>Check the CORS configuration of buckets. If a CORS rule exists but the "Allow-Headers" or "Expose-Headers" header of CORS is not configured, cross-origin access requests might fail.</td>
   </tr>
   <tr>
      <td>Referer hotlink protection configuration of buckets</td>
      <td>Check the permission and referer configurations of COS buckets. If the bucket permission allows access by anonymous users, but no referer access rule is configured or an empty rule is configured, problems such as hotlinking by malicious users might occur.</td>
   </tr>
   <tr>
      <td rowspan="2">CWP</td>
      <td>Vulnerabilities not fixed</td>
      <td>Check whether an instance has unfixed vulnerabilities, and if so, an instance might be compromised and data loss might be occurred.</td>
   </tr>
   <tr>
      <td>Client offline</td>
      <td>Check whether the CWP client is offline, and if so, the CWP instance will not be able to protect your instance.</td>
   </tr>
   <tr>
      <td>TDSQL-C</td>
      <td>TDSQL-C for MySQL root account security</td>
      <td>Check the account configuration. If only the root account exists and there are no other application accounts, the permissions are excessive, and data security risks due to faulty or malicious operations will occur.</td>
   </tr>
   <tr>
      <td rowspan="2">Anti-DDoS</td>
      <td>Available IP blackhole unblockings</td>
      <td>Check whether the proportion of used blackhole unblockings is excessive.</td>
   </tr>
   <tr>
      <td>Blocked EIPs</td>
      <td>Check whether there are any EIPs blocked due to DDoS attacks.</td>
   </tr>
   <tr>
      <td rowspan="2">TDSQL for MySQL</td>
      <td>Restriction of high-risk commands for accounts</td>
      <td>Check the account configuration. If all accounts have the permission to run global commands, such as DROP and DELETE, data may be easily deleted by mistake or maliciously.</td>
   </tr>
   <tr>
      <td>Public network security policy</td>
      <td>Check the public network security policy. If public network access is enabled, but no security group rules are configured, when there are attacks from the public network, application exceptions and data breach will occur.</td>
   </tr>
   <tr>
      <td rowspan="2">ES</td>
      <td>Public network access policy of ES clusters</td>
      <td>Check the public network access policy of ES clusters. If no restrictions are configured, a warning for access risk in the cluster will be triggered, and the bandwidth for public network access will be limited.</td>
   </tr>
   <tr>
      <td>Kibana component's public network access policy of clusters</td>
      <td>Check the Kibana component's public network access policy of ES clusters. If no restrictions are configured, a warning for access risk in Kibana will be triggered.</td>
   </tr>
   <tr>
      <td rowspan="3">TencentDB for MySQL</td>
      <td>Root account security</td>
      <td>Check TencentDB for MySQL account configuration. If only the root account exists and there are no other application accounts, the permissions are excessive, and data security risks due to faulty or malicious operations will occur.</td>
   </tr>
   <tr>
      <td>Restriction of high-risk commands for non-root accounts</td>
      <td>Check the permission scope of TencentDB for MySQL non-root accounts. If an application account has the permission to run high-risk commands, such as DROP and DELETE, data may be easily deleted by mistake or maliciously.</td>
   </tr>
   <tr>
      <td>Public network security policy</td>
      <td>Check the public network security policy in TencentDB for MySQL. If public network access is enabled, but no security group rules are configured, when there are attacks from the public network, application exceptions and data breach might occur.</td>
   </tr>
   <tr>
      <td>TencentDB for Redis</td>
      <td>High-risk commands</td>
      <td>Check the disabled command configuration of TencentDB for Redis instances. If a high-risk command is not disabled, risks such as application blocking and accidental data deletion will occur.</td>
   </tr>
   <tr>
      <td>Security Group</td>
      <td>Public network access</td>
      <td>Check whether the security group allows for source IP access through all ports or ports except 80 and 443, and if so, security risks such as unauthorized access and DDoS attacks will occur.</td>
   </tr>
   <tr>
      <td rowspan="2">TencentDB for MariaDB</td>
      <td>Restriction of high-risk commands for accounts</td>
      <td>Check the account configuration. If all accounts have the permission to run global commands, such as DROP and DELETE, data might be easily deleted by mistake or maliciously.</td>
   </tr>
   <tr>
      <td>Public network security policy</td>
      <td>Check the public network security policy. If public network access is enabled, but no security group rules are configured, when there are attacks from the public network, application exceptions and data breach might occur.</td>
   </tr>
</table>

## Reliability[](id:reliable)

Multidimensional monitoring is supported to keep instances running stably.

<table>
   <tr>
      <th>Service</th>
      <th>Inspection Item</th>
      <th>Description</th>
   </tr>
   <tr>
      <td rowspan="2">CBS</td>
      <td>Storage capacity</td>
      <td>Check the storage capacity usage of CBS cloud disks. If the capacity utilization is excessive, cloud disk read/write will be affected.</td>
   </tr>
   <tr>
      <td>No snapshots created</td>
      <td>Check whether CBS cloud disks have snapshots or are configured with a scheduled snapshot policy, and if not, it will be difficult to recover the data when a server or cloud disk is faulty, which may cause serious data loss.</td>
   </tr>
   <tr>
      <td>CKafka</td>
      <td>Cross-AZ deployment</td>
      <td>If instances are not deployed across AZs, when a serious fault occurs in the single-AZ CKafka cluster, the cluster may become unavailable.</td>
   </tr>
   <tr>
      <td rowspan="10">CLB</td>
      <td>CVM instance AZ</td>
      <td>Check whether a CLB instance is in the same AZ as the CVM instance bound to it, and if not, cross-AZ forwarding may affect service reliability, for example, slower forwarding of some requests.</td>
   </tr>
   <tr>
      <td>Single points of failure of the real server</td>
      <td>Check whether a CLB listener or forwarding rule is bound to only one real server, such as CVM or EVM instance, and if so, single points of failure may occur.</td>
   </tr>
   <tr>
      <td>Forwarding rule bound to multiple ports of a CVM instance</td>
      <td>Check whether a CLB forwarding rule is bound to multiple ports of the same CVM instance, and if so, it will be harder to troubleshoot problems when processes compete for resources as the business volume grows, and the system will be less able to accommodate traffic peaks.</td>
   </tr>
   <tr>
      <td>CVM instances in different subnets</td>
      <td>Check whether a CLB listener or forwarding rule is bound to multiple CVM instances in different VPC subnets, and if so, it will be harder to quickly troubleshoot problems when exceptions occur.</td>
   </tr>
   <tr>
      <td>CVM instance weight</td>
      <td>Check the weight of the CVM instance bound to a CLB listener or forwarding rule. If the weight doesn't match the configuration, performance risks will occur during business peaks, affecting business stability.</td>
   </tr>
   <tr>
      <td>Health check configuration</td>
      <td>Check whether health check is configured for a CLB instance, and if not, the CLB instance will forward traffic to all real servers (including abnormal ones).</td>
   </tr>
   <tr>
      <td>Forwarding rule configuration</td>
      <td>Check the CLB listener configuration. If no forwarding rules are configured, CLB features cannot be used normally, and additional fees will be incurred.</td>
   </tr>
   <tr>
      <td>Sudden changes in the health check</td>
      <td>Check for sudden changes of CLB listeners in the health check, i.e., whether the server port is abnormal.</td>
   </tr>
   <tr>
      <td>Instance type</td>
      <td>Check the CLB instance type, which is either classic or application. Application instances have more features, for example, layer-4 listener that can be configured with different real servers, layer-7 listener, CLS log, SNI, and binding with ENI.</td>
   </tr>
   <tr>
      <td>Bandwidth cap of 1 Mbps</td>
      <td>If the bandwidth is not selected during CLB instance purchase, the default limit of 1 Mbps will apply. CLB instances with this limit are scanned, and if they are used by high-traffic businesses, serious packet loss may occur.</td>
   </tr>
   <tr>
      <td rowspan="2">COS</td>
      <td>Bucket versioning</td>
      <td>Check the versioning configuration of COS buckets. If it is not enabled, data may be lost.</td>
   </tr>
   <tr>
      <td>Log management configuration of buckets</td>
      <td>Check the log management feature of COS buckets. If the owners of the destination and source buckets are different, bucket log shipping will fail.</td>
   </tr>
   <tr>
      <td rowspan="4">CVM</td>
      <td>System disk snapshot</td>
      <td>Check CVM system disk snapshots. If no snapshots are created, it will be difficult to recover the data when a server or cloud disk is faulty, which may cause serious loss.</td>
   </tr>
   <tr>
      <td>Excessive disk utilization of instances</td>
      <td>Check the disk utilization of CVM instances. If the utilization is excessive, disk read/write will be affected.</td>
   </tr>
   <tr>
      <td>Local disk type of instances</td>
      <td>Check the local disk usage of CVM instances. If an instance is not an I/O or Big Data model but uses a local disk, its disk data cannot be backed up through snapshots, which may bring risks to disaster recovery.</td>
   </tr>
   <tr>
      <td>Excessive bandwidth utilization</td>
      <td>Check the bandwidth utilization of CVM instances. If the utilization is excessive, the network performance may be affected.</td>
   </tr>
   <tr>
      <td>Anti-DDoS</td>
      <td>Layer-7 forwarding rule health check</td>
      <td>Check whether any exceptions exist in the health check of the current layer-7 forwarding rules.</td>
   </tr>
   <tr>
      <td>TDSQL for MySQL</td>
      <td>Disaster recovery</td>
      <td>Check whether disaster recovery is configured for instances, and if not, business access may be affected when an instance has a serious fault.</td>
   </tr>
   <tr>
      <td>EIP</td>
      <td>Bandwidth cap of 1 Mbps</td>
      <td>If the EIP bandwidth is not selected during purchase, the default limit of 1 Mbps will apply. EIPs with this limit are scanned, and if they are used by high-traffic businesses, serious packet loss may occur.</td>
   </tr>
   <tr>
      <td>ES</td>
      <td>Automatic snapshot backup of ES clusters</td>
      <td>Check the automatic snapshot backup of ES clusters. If it is not configured, a risk warning will be triggered.</td>
   </tr>
   <tr>
      <td rowspan="7">CSS</td>
      <td>CSS code mode</td>
      <td>Check whether the service is in CSS code mode, and if not, a risk warning will be triggered.</td>
   </tr>
   <tr>
      <td>Resolution of CNAME record to dedicated domain name</td>
      <td>If the CNAME record of the domain name is incorrectly configured, normal push and playback in CSS will be affected. If the CNAME record value is incorrect, a risk warning will be triggered.</td>
   </tr>
   <tr>
      <td>Top-level/Second-level domain names included in push domain name</td>
      <td>A second-level domain name is a subordinate of a top-level domain name. CSS domain names are redirected to wildcard domain names through CNAME records, and the domain names will be instantiated if necessary. If a top-level domain name is instantiated, but its second-level domain names are not, normal resolution of the second-level domain names will be affected.</td>
   </tr>
   <tr>
      <td>Top-level/Second-level domain names included in playback domain name</td>
      <td>A second-level domain name is a subordinate of a top-level domain name. CSS domain names are redirected to wildcard domain names through CNAME records, and the domain names will be instantiated if necessary. If a top-level domain name is instantiated, but its second-level domain names are not, normal resolution of the second-level domain names will be affected.</td>
   </tr>
   <tr>
      <td>Push authentication enablement</td>
      <td>Check whether push authentication is enabled and CSS callback is configured, and if both are not, a risk warning will be triggered.</td>
   </tr>
   <tr>
      <td>SSL certificate validity period</td>
      <td>If the certificate expires, HTTPS access will be affected, i.e., HTTPS access requests may fail.</td>
   </tr>
   <tr>
      <td>Bandwidth cap value</td>
      <td>Check whether the bandwidth cap is enabled, and if so, check whether the current bandwidth is close to the cap. After the cap is reached, new user access requests will be limited.</td>
   </tr>
   <tr>
      <td rowspan="3">TencentDB for MongoDB</td>
      <td>Oplog retention period</td>
      <td>Check the oplog retention period of TencentDB for MongoDB instances. If the period is too short, it may cause rollback failures or affect troubleshooting.</td>
   </tr>
   <tr>
      <td>Backup result</td>
      <td>Check whether TencentDB for MongoDB instances are successfully backed up, and if not, data may fail to be recovered.</td>
   </tr>
   <tr>
      <td>Classic network</td>
      <td>Check whether TencentDB for MongoDB instances use classic networks.</td>
   </tr>
   <tr>
      <td rowspan="5">TencentDB for MySQL</td>
      <td>Disaster recovery</td>
      <td>Check whether disaster recovery is configured for TencentDB for MySQL instances, and if not, business access may be affected when an instance has a serious fault.</td>
   </tr>
   <tr>
      <td>Source-replica delay</td>
      <td>Check the source-replica delay of TencentDB for MySQL instances. If the delay is excessive, risks such as removal of database RO instances and excessive source/replica HA switch time will occur.</td>
   </tr>
   <tr>
      <td>Cross-AZ deployment</td>
      <td>Check whether TencentDB for MySQL instances are deployed across AZs, and if not, when a severe fault occurs in the AZ, access to the database may fail.</td>
   </tr>
   <tr>
      <td>Single instance in a read-only group</td>
      <td>Check whether a TencentDB for MySQL read-only group has only one instance, and if so, the read-only business will become unavailable when the instance fails.</td>
   </tr>
   <tr>
      <td>Classic network</td>
      <td>Check whether TencentDB for MySQL instances use classic networks.</td>
   </tr>
   <tr>
      <td rowspan="2">TencentDB for Redis</td>
      <td>Cross-AZ deployment</td>
      <td>Check whether TencentDB for Redis instances are deployed across AZs, and if not, when an AZ-level disaster occurs in an instance, it may become inaccessible.</td>
   </tr>
   <tr>
      <td>Classic network</td>
      <td>Check whether TencentDB for Redis instances use classic networks.</td>
   </tr>
   <tr>
      <td>Security Group</td>
      <td>Redundant rules</td>
      <td>Check for ineffective security group rules, which occupy the limited quota and may result in the failure to create rules and affect your business. Ineffective rules can be repeated and involve port overlaps.</td>
   </tr>
   <tr>
      <td rowspan="3">TDMQ</td>
      <td>Cluster health check</td>
      <td>Use of unhealthy clusters may involve certain risks.</td>
   </tr>
   <tr>
   <td>Backup consumer</td>
      <td>Check whether there is only one consumer, and if so, when a single point of failure occurs, business consumption will be affected.</td>
   </tr>
   <tr>
   <td>Dead letter queue</td>
      <td>If there are no dead letter queues, consumers may be unable to process some special messages.</td>
   </tr>
   <tr>
      <td rowspan="2">TencentDB for MariaDB</td>
      <td>Source-replica delay</td>
      <td>If the source-replica delay is continuously excessive, source-replica data consistency cannot be guaranteed. In this case, if an HA source-replica switch occurs on an instance, data may be lost in extreme cases.</td>
   </tr>
   <tr>
      <td>Disaster recovery</td>
      <td>Check whether disaster recovery is configured for TencentDB for MariaDB instances, and if not, business access may be affected when an instance has a serious fault.</td>
   </tr>
   <tr>
      <td>TKE</td>
      <td>Cross-AZ cluster node deployment</td>
      <td>Check whether the cluster nodes are in the same AZ, and if so, when the AZ is unavailable, the business will be affected, and the cluster cannot be scheduled to other AZs.</td>
   </tr>
   <tr>
      <td rowspan="10">TRTC</td>
      <td>Terminal version of the native SDK</td>
      <td>Check the native SDK terminal version. If it is earlier than expected, the quality may be unstable.</td>
   </tr>
   <tr>
      <td>Terminal version of the web SDK</td>
      <td>Check the web SDK terminal version. If it is earlier than expected, the quality may be unstable.</td>
   </tr>
   <tr>
      <td>Video bitrate of the native SDK</td>
      <td>Check the video bitrate of the native SDK. Video parameters need to balance image quality and smoothness. Configuring reasonable video parameters will deliver a better user experience.</td>
   </tr>
   <tr>
      <td>Scenario consistency of the native SDK</td>
      <td>Check whether the same room involves multiple call scenarios, and if so, unexpected results may occur.</td>
   </tr>
   <tr>
      <td>Time sequence for stream pull of the native SDK</td>
      <td>Check the time sequence for stream pull of the native SDK. If a pull operation is earlier than the arrival of the video stream, the screen may turn black.</td>
   </tr>
   <tr>
      <td>Logic for room exit of the native SDK</td>
      <td>Check the logic for room exit of the native SDK. If it is not properly configured, the SDK will experience internal chaos with exceptions.</td>
   </tr>
   <tr>
      <td>Postpaid billing</td>
      <td>Check whether postpaid billing is enabled, and if not, the service will be suspended after the plan is used up.</td>
   </tr>
   <tr>
      <td>Substream video bitrate of the native SDK</td>
      <td>Check the substream video bitrate of the native SDK. Video parameters need to balance image quality and smoothness. If the bitrate is low, poor image quality or video lag may be caused under poor network conditions.</td>
   </tr>
   <tr>
      <td>Room entry scenario and role match in the native SDK</td>
      <td>Check whether the scenario matches the role configuration in the native SDK. For example, in video and audio call scenarios, the audience role doesn't need to be set; otherwise, a lag or black screen may occur.</td>
   </tr>
   <tr>
      <td>Mutual kick-out under the same `userId` in the native SDK</td>
      <td>Check for mutual kick-out in the same room under the same `userId` in the native SDK. This problem may lead to a black screen or lag.</td>
   </tr>
   <tr>
      <td>VPC</td>
      <td>Subnet planning</td>
      <td>Check whether the subnet IP range is identical to the VPC IP range, and if so, no more subnets can be planned, adversely affecting long-term plans such as cross-AZ expansion.</td>
   </tr>
   <tr>
      <td>VPC - VPN Gateway</td>
      <td>Expiration in one month</td>
      <td>Check the billing mode of VPN gateways. If manual renewal or non-renewal is enabled and a VPN gateway will expire soon, the service may become unavailable, affecting the business.</td>
   </tr>
   <tr>
      <td>VPC - VPN</td>
      <td>VPN tunnel status</td>
      <td>Check whether there is a VPN tunnel that is not connected, and if so, switching to the secondary tunnel may fail.</td>
   </tr>
</table>



## Service Restriction[](id:ServiceRestrictions)


Tencent Smart Advisor can monitor the maximum number of available service resources to prompt you to delete resources or apply to increase the quota based on the suggestions.

<table>
   <tr>
      <th>Service</th>
      <th>Inspection Item</th>
      <th>Description</th>
   </tr>
   <tr>
      <td>CFW</td>
      <td>Rule quota</td>
      <td>Check the CFW rule list quota. If it is insufficient, a risk warning will be triggered.</td>
   </tr>
   <tr>
      <td>CVM</td>
      <td>Instance expiration</td>
      <td>Check whether CVM instances have expired. If a monthly subscribed instance is about to expire but auto-renewal is not configured, it may be terminated after expiration.</td>
   </tr>
   <tr>
      <td>TDSQL-C</td>
      <td>TDSQL-C for MySQL cluster expiration</td>
      <td>Check whether clusters have expired. If a monthly subscribed cluster is about to expire but auto-renewal is not configured, access to the business may be compromised after expiration.</td>
   </tr>
   <tr>
      <td>TDSQL for MySQL</td>
      <td>Instance expiration</td>
      <td>Check whether instances have expired. If a monthly subscribed instance is about to expire but auto-renewal is not configured, access to the business may be compromised after expiration.</td>
   </tr>
   <tr>
      <td>DNSPod</td>
      <td>Paid plan expiration in two months and auto-renewal not configured</td>
      <td>Check whether a paid plan will expire in two months and auto-renewal is configured. If it is not configured, the service will be suspended immediately the plan is used up.</td>
   </tr>
   <tr>
      <td>Domain</td>
      <td>Expiration</td>
      <td>Check whether domain names have expired. If auto-renewal is not configured, access to the business may be compromised after expiration.</td>
   </tr>
   <tr>
      <td>EIP</td>
      <td>Usage</td>
      <td>Check the usage of EIPs in each region. If the usage is close to or exceeds the quota, no more EIPs can be applied for.</td>
   </tr>
   <tr>
      <td rowspan="2">TencentDB for MongoDB</td>
      <td>Instance expiration</td>
      <td>Check whether TencentDB for MongoDB instances have expired. If a monthly subscribed instance is about to expire but auto-renewal is not configured, access to the business may be compromised after expiration.</td>
   </tr>
   <tr>
      <td>Storage capacity</td>
      <td>Check the storage capacity utilization of TencentDB for MongoDB instances. If the utilization reaches 100%, write will fail.</td>
   </tr>
   <tr>
      <td rowspan="4">TencentDB for MySQL</td>
      <td>Instance expiration</td>
      <td>Check whether TencentDB for MySQL instances have expired. If a monthly subscribed instance is about to expire but auto-renewal is not configured, access to the business may be compromised after expiration.</td>
   </tr>
   <tr>
      <td>Connection utilization</td>
      <td>Check the connection utilization of TencentDB for MySQL instances. If the utilization reaches 100%, the business may fail to connect to the database.</td>
   </tr>
   <tr>
      <td>Disk utilization</td>
      <td>Check the disk utilization of TencentDB for MySQL instances. If the utilization is excessive, data may fail to be written.</td>
   </tr>
   <tr>
      <td>Disk usage close to the upper limit of 6 TB</td>
      <td>Check whether the disk usage of TencentDB for MySQL instances is close to the upper limit of 6 TB.</td>
   </tr>
   <tr>
      <td>NAT Gateway</td>
      <td>DNAT usage</td>
      <td>Check the DNAT usage of NAT gateways. If the usage is close to the upper limit, further business deployment may be affected.</td>
   </tr>
   <tr>
      <td rowspan="3">TencentDB for Redis</td>
      <td>Instance expiration</td>
      <td>Check whether TencentDB for Redis instances have expired. If a monthly subscribed instance is about to expire but auto-renewal is not configured, access may fail.</td>
   </tr>
   <tr>
      <td>Memory close to the upper limit of 4 TB</td>
      <td>Check whether the memory usage of TencentDB for Redis instances is close to the upper limit of 4 TB.</td>
   </tr>
   <tr>
      <td>Number of replicas reaching the upper limit of five</td>
      <td>Check whether the number of TencentDB for Redis instance replicas reaches the upper limit of five.</td>
   </tr>
   <tr>
      <td rowspan="3">TencentDB for MariaDB</td>
      <td>Connection utilization</td>
      <td>If the connection utilization reaches 100%, new requests cannot establish connections, and access will fail.</td>
   </tr>
   <tr>
      <td>Data disk utilization</td>
      <td>If the disk utilization reaches 100%, write will fail.</td>
   </tr>
   <tr>
      <td>Instance expiration</td>
      <td>Check whether TencentDB for MariaDB instances have expired. If a monthly subscribed instance is about to expire but auto-renewal is not configured, access to the business may be compromised after expiration.</td>
   </tr>
   <tr>
      <td>VPC</td>
      <td>Number of used route tables</td>
      <td>Check the number of VPC route tables. If it is close to or exceeds the upper limit, new tables may fail to be created.</td>
   </tr>
</table>

## Cost[](id:cost)

Tencent Smart Advisor can provide suggestions for more cost-effective configurations based on the running status of resources to reduce your costs.

<table>
   <tr>
      <th>Service</th>
      <th>Inspection Item</th>
      <th>Description</th>
   </tr>
   <tr>
      <td>CBS</td>
      <td>Underutilization</td>
      <td>Check the mounting and I/O status of CBS cloud disks. If a cloud disk was unmounted in the past five days, or its daily IOPS did not exceed one in the last seven days, an alarm will be triggered. Cloud disks that are idle for a long time will incur unnecessary fees.</td>
   </tr>
   <tr>
      <td rowspan="2">CLB</td>
      <td>Idle instances</td>
      <td>Check whether CLB instances are bound to backend Tencent Cloud resources (CVM instances or ENIs), and if not, they will be considered idle, and additional fees will be incurred.</td>
   </tr>
   <tr>
      <td>Low utilization</td>
      <td>Check the utilization of CLB instances. If the number of connections is smaller than 10% of the quota, the costs of redundancy may be incurred.</td>
   </tr>
   <tr>
      <td rowspan="2">COS</td>
      <td>Bucket lifecycle configuration</td>
      <td>Check whether the lifecycle rules of COS buckets are configured, and if not, objects that are accessed infrequently in buckets will incur unnecessary fees.</td>
   </tr>
   <tr>
      <td>Incomplete multipart uploads in buckets</td>
      <td>Check for the incomplete multipart upload clearing rules of COS buckets. If no such rules are configured, unnecessary fees may be incurred.</td>
   </tr>
   <tr>
      <td rowspan="2">CVM</td>
      <td>Low utilization of instances</td>
      <td>Check the CPU and network I/O utilization of CVM instances. If it is low for a long time, a risk warning will be triggered.</td>
   </tr>
   <tr>
      <td>Billing mode</td>
      <td>Check whether CVM instances are in pay-as-you-go billing mode for a long time (more than two months). The unit price in this mode is high, which will incur unnecessary fees.</td>
   </tr>
   <tr>
      <td>TDSQL-C</td>
      <td>DSQL-C for MySQL underutilization</td>
      <td>Check whether clusters are idle. If the business lifecycle is stable, resources that are idle for a long time will incur unnecessary fees.</td>
   </tr>
   <tr>
      <td>TencentDB for MongoDB</td>
      <td>Underutilization</td>
      <td>Check whether instances are idle. If the business lifecycle is stable, resources that are idle for a long time will incur unnecessary fees.</td>
   </tr>
   <tr>
      <td>TencentDB for MySQL</td>
      <td>Underutilization</td>
      <td>Check whether instances are idle. If the business lifecycle is stable, resources that are idle for a long time will incur unnecessary fees.</td>
   </tr>
   <tr>
      <td>NAT Gateway</td>
      <td>Idleness</td>
      <td>Check whether NAT instances are configured in route tables, and if not, they will be idle and incur fees.</td>
   </tr>
   <tr>
      <td>TencentDB for Redis</td>
      <td>Underutilization</td>
      <td>Check whether instances are idle. If the business lifecycle is stable, resources that are idle for a long time will incur unnecessary fees.</td>
   </tr>
   <tr>
      <td>TencentDB for MariaDB</td>
      <td>Underutilization</td>
      <td>Check whether instances are idle. If the business lifecycle is stable, resources that are idle for a long time will incur unnecessary fees.</td>
   </tr>
   <tr>
      <td>VPC - VPN Gateway</td>
      <td>Idleness</td>
      <td>Check whether VPN gateways are associated with VPN tunnels, and if not, additional fees may be incurred.</td>
   </tr>
</table>

## Performance[](id:performance)

Tencent Smart Advisor provides performance improvement suggestions based on the resource usage monitored during instance operations and best practices.

<table>
   <tr>
      <th>Service</th>
      <th>Inspection Item</th>
      <th>Description</th>
   </tr>
   <tr>
      <td rowspan="3">CBS</td>
      <td>High I/O load</td>
      <td>Check the I/O load of CBS cloud disks. If it is excessive, an alarm will be triggered.</td>
   </tr>
   <tr>
      <td>Excessive IOPS</td>
      <td>Check whether the peak IOPS of CBS cloud disks reaches the upper limit configured for the corresponding cloud disk type, and if so, traffic throttling may be triggered.</td>
   </tr>
   <tr>
      <td>Excessive throughput</td>
      <td>Check whether the peak throughput of CBS cloud disks reaches the upper limit configured for the corresponding cloud disk type, and if so, traffic throttling may be triggered.</td>
   </tr>
   <tr>
      <td>CCN</td>
      <td>Outbound bandwidth usage</td>
      <td>Check whether the outbound bandwidth usage of cross-region CCN instances in each region is close to the threshold, and if so, packets may be lost due to bandwidth limiting, affecting the business.</td>
   </tr>
   <tr>
      <td rowspan="6">CDN</td>
      <td>Single-link downstream speed limit configuration</td>
      <td>If this feature is not set, the single-link speed is not limited by default, which may cause a high peak bandwidth during events.</td>
   </tr>
   <tr>
      <td>Bandwidth cap configuration</td>
      <td>If this feature is not disabled, when the bandwidth cap is reached, the CDN service will be disabled, and requests will be forwarded to the origin server or the 404 error code will be returned. This feature can reduce bandwidth fees to a certain degree. After the CDN service is disabled, you need to set and enable the domain name again before you can use the CDN service again.</td>
   </tr>
   <tr>
      <td>Expiration of certificates bound to domain names</td>
      <td>If the certificate expires, HTTPS access will be affected, i.e., HTTPS access requests may fail.</td>
   </tr>
   <tr>
      <td>Cache hit rate</td>
      <td>If the hit rate is low, the pressure on the origin server cannot be effectively alleviated, and user access acceleration cannot reach a satisfactory optimization effect.</td>
   </tr>
   <tr>
      <td>Error code proportion</td>
      <td>If the proportion of error codes is high, events affecting the business may have occurred, or there will be potential faults.</td>
   </tr>
   <tr>
      <td>Secondary origin server</td>
      <td>If no secondary origin servers are configured, when the primary origin server is unavailable, disaster recovery will be impossible.</td>
   </tr>
   <tr>
      <td>CLB</td>
      <td>404 or 502 error code returned by the real server</td>
      <td>Check whether the CLB real server returns the 404 or 502 error code, which indicates that no corresponding resources can be found or a gateway error occurs, and if so, business quality may be affected.</td>
   </tr>
   <tr>
      <td>COS</td>
      <td>5xx error rate</td>
      <td>Check COS error codes. If there are too many 5xx error codes with a high occurrence frequency, normal access to buckets may be affected.</td>
   </tr>
   <tr>
      <td rowspan="2">CVM</td>
      <td>High memory load of instances</td>
      <td>Check the memory utilization of CVM instances. If it is excessive, a risk warning will be triggered.</td>
   </tr>
   <tr>
      <td>High CPU load of instances</td>
      <td>Check the CPU utilization of CVM instances. If it is excessive, a risk warning will be triggered.</td>
   </tr>
   <tr>
      <td rowspan="2">TDSQL-C</td>
      <td>TDSQL-C for MySQL CPU utilization</td>
      <td>Check the CPU utilization. If it is excessive, risks such as longer business request delays and no response will occur.</td>
   </tr>
   <tr>
      <td>TDSQL-C for MySQL number of full-table scans</td>
      <td>Check the number of full-table scans of instances per second.</td>
   </tr>
   <tr>
      <td rowspan="2">TencentDB for MongoDB</td>
      <td>Dirty data in cache</td>
      <td>Check the dirty data in the cache of TencentDB for MongoDB instances. If its proportion exceeds 20%, user threads will be flushed, and the business will be blocked.</td>
   </tr>
   <tr>
      <td>CPU utilization</td>
      <td>Check the CPU utilization of TencentDB for MongoDB instances. If it is excessive, risks such as longer business request delays and waits will occur.</td>
   </tr>
   <tr>
      <td rowspan="2">TencentDB for MySQL</td>
      <td>CPU utilization</td>
      <td>Check the CPU utilization of TencentDB for MySQL instances. If it is excessive, risks such as longer business request delays and no response will occur.</td>
   </tr>
   <tr>
      <td>Number of running threads</td>
      <td>Check the number of running threads on TencentDB for MySQL instances. If it is far more than the number of CPU cores, risks such as longer request waits and delays will occur.</td>
   </tr>
   <tr>
      <td rowspan="3">TencentDB for Redis</td>
      <td>Outbound traffic throttling triggered on proxy nodes</td>
      <td>Check the number of trigger times of outbound traffic throttling on TencentDB for Redis proxy nodes. If traffic throttling was triggered, the business may have been compromised during peak hours. If the number is excessive, business traffic has reached the upper limit, and business access may have longer delays or fail.</td>
   </tr>
   <tr>
      <td>CPU utilization</td>
      <td>Check the CPU utilization of TencentDB for Redis instances. If it is excessive for a long time, problems such as longer request delays and request blocking may occur.</td>
   </tr>
   <tr>
      <td>Excessive node requests</td>
      <td>Check whether the number of requests of TencentDB for Redis nodes is close to the upper limit.</td>
   </tr>
   <tr>
      <td rowspan="2">TencentDB for MariaDB</td>
      <td>CPU utilization</td>
      <td>If the CPU utilization is high, the current instance is busy, and problems such as slower and blocked queries may occur.</td>
   </tr>
   <tr>
      <td>Number of active connections</td>
      <td>If the number of active connections is excessive, the instance is currently under high pressure, and requests are likely to be blocked.</td>
   </tr>
</table>
