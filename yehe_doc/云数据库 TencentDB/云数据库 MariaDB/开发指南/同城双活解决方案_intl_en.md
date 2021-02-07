Currently, TencentDB for MariaDB supports the intra-city 2-DC active-active scheme, which has the following main features:
- Intra-city 2-DC deployment
- 2-DC writability: if your servers are deployed in different subnets of two DCs, you can connect to the database and write data to it from any server in either DC.
- Automatic failover and recovery
- Unique access IP of both DCs

However, the intra-city 2-DC active-active scheme alone cannot implement disaster recovery at the business system level. Actually, it is easy to switch a single system/module to an intra-city disaster recovery DC, but the complicated correlation among and configurations in enterprise-level system businesses are challenges for the 2-DC scheme.

Therefore, to build an active-active business system, the design, use, management, and system upgrade of the business must be implemented based on real-time use of and configuration interoperability between both DCs. In this way, the business can be quickly resumed with no or only slight modification required in case of failures. This is also the goal of designing TencentDB for MariaDB's intra-city 2-DC active-active scheme. It allows business systems in both DCs to fully read from and write to the database system over the local network while ensuring strong database consistency.

## Design Standard
The active-active feature of TencentDB for MariaDB is designed based on "GB/T 20988-2007 Information Security Technology - Disaster Recovery Specifications for Information System". For a single database module:
- RTO ≤ 60 seconds
- RPO ≤ 5 seconds
- Failover time ≤ 5 seconds
- Failure detection time ≤ 30 seconds

This means that it takes about 40 seconds to complete failover after a failure occurs (including failure detection time).

Risk warning: when performing tests in a production environment, please make sure that the business system has an automatic database reconnection mechanism. The business system usually has multiple modules, and each module may be associated with multiple data sources; therefore, the more complex the system, the longer the recovery time.


## Support
### Supported items
Supported instance editions:
- Standard Edition: one primary and one replica (two nodes) or one primary and two replicas (three nodes);
- Finance Edition: one primary and one replica (two nodes) or one primary and two replicas (three nodes);

Network requirement: VPC only

Supported regions:
- Beijing (Beijing Zone 1, Beijing Zone 3)


### Pricing
Dual-availability zone and single-availability zone schemes are offered at the same price. For more information, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/237/2034).

Risk warning: the Direct Connect service for 2-DC data sync was free of charge before June 30, 2019. If the operating policy changes in the future, the price will not be higher than that of intra-city Direct Connect published by Tencent Cloud. If you do not want to continue using the intra-city 2-DC scheme, you can migrate your data to the intra-city 1-DC scheme free of charge.

### Purchase and use
Go to the [purchase page of TencentDB for MariaDB](https://console.cloud.tencent.com/mariadb/buy) and click **Buy Now**.
- If the primary and replica availability zones are the same, the single-availability zone deployment scheme is used.
- If the primary and replica availability zones are different, the intra-city 2-DC deployment scheme is used.
![](https://main.qcloudimg.com/raw/410caff31809e43100ae570ad1ffc3c7.png)

>!
>
>- The primary availability zone is the zone where your primary server is located. The database should be deployed in the same VPC subnet as the primary server to reduce access delay. A replica availability zone is the zone where a replica node of the database is located. For the one-primary-two-replica architecture (three nodes), two nodes will be deployed in the primary availability zone. For the one-primary-one-replica architecture (two nodes), one node will be deployed in the primary availability zone.
- If intra-city 2-DC policy is required for the finance cloud cage solution, an intra-city 2-DC cage solution needs to be built first. For more information, please contact your sales rep and architect.


### Instance initialization
Initialize your instance by referring to [Initializing Instance](https://intl.cloud.tencent.com/document/product/237/7055).

### Viewing details of instance availability zones
Log in to the [MariaDB console](https://console.cloud.tencent.com/mariadb), click the instance ID/name or **Manage** in the **Operation** column, and view the availability zones on the instance details page.

### Primary/replica switch
To switch the primary node from one availability zone to another, click **Primary-Replica Switch** on the instance details page in the console. As this operation is highly risky, the IP address of the login account must be verified. The switch process may cause a momentary disconnection from the database (≤ 1 second). Please make sure that your business has a database reconnection mechanism. Frequent switching may result in business system exceptions or even data exceptions.
![](https://main.qcloudimg.com/raw/7e342068ca132fef5bf287ebf46b92f3.png)

## How It Works
By integrating the highly available primary/replica architecture of TencentDB for MariaDB with virtual IP drifting of VPC availability zone, simultaneous reads from and writes to two DCs can be implemented. This architecture has the following features:
- Proxy modules are deployed in a mixed manner on the frontend of each TencentDB for MariaDB database node, which are responsible for routing data requests to corresponding database nodes.
- Cross-region VPC gateway is deployed on the frontend of the proxy module to support virtual IP drifting.
![](https://main.qcloudimg.com/raw/f9bffbf32d311e6a0fe2a1046732b589.png)

Taking data writes as an example: as shown above, if the business server is deployed in availability zone A, the VPC gateway will forward the data request to the proxy gateway in availability zone A which will then transparently forward it to the primary node. If the business server is deployed in availability zone B, the VPC gateway will forward the data request to proxy gateway in availability zone B which will then forward it to the primary node over Tencent Cloud's BGP network.
No matter whether it is a read or write request, the entire process is imperceptible to the business. In case of database exception, the database cluster will be processed as follows:
1. If both the primary and proxy fail, the cluster will automatically promote the optimal replica to the new primary. The system will notify the VPC to modify the association between the virtual and physical IPs. The business will only perceive that some write requests are disconnected.
2. If the primary fails but the proxy is normal, the cluster will automatically promote the optimal replica to the new primary. The proxy will block requests until primary/replica switch is completed. In this case, the business will only perceive that some requests time out.
3. If the replica fails (no matter whether the proxy fails), if read/write separation is enabled, an operation will be performed according to the read-only policy of the preconfigured read-only account (there are three types of policies).
4. If availability zone A completely fails, while the VPC and database are still working in availability zone B, the replica 2 node will be automatically promoted to the primary node. **The read/write policy of the node will be adjusted according to the strong sync policy**, and the VPC IP will drift to availability zone B. In this case, the cluster will try to recover the node in availability zone A. If the node cannot be recovered within 30 minutes, at least one replica node will be automatically created on node B. As there is an IP drifting policy, no database configuration modification is required of the business.
5. If DC B completely fails, it is equivalent to the failure of a replica node in the TencentDB for MariaDB cluster, and the failure can be processed in the same way as described in item 3 above.

## FAQs
#### 1. Compared with intra-city 1-DC, will the intra-city 2-DC scheme cause a decrease in performance?
Based on the strong sync replication scheme, as the cross-DC delay is slightly larger than that between devices in the same DC, the speed of SQL response will drop by about 5% in theory.

#### 2. Is it possible for a primary node to switch from the primary availability zone to the replica availability zone?
Yes. You can ignore this if it does not affect the use of your business. If you are concerned about the impact, you can switch back by using the primary/replica switch feature in the console during off-peak hours.

#### 3. How do I know that primary/replica switch is performed in the database cluster?
Log in to the [Cloud Monitor console](https://console.cloud.tencent.com/monitor/policylist), select **Alarm Policy** on the left sidebar, and click **Create**. On the displayed page, select TencentDB for MariaDB as the **Policy Type** and configure an alarm on primary/replica switch.

#### 4. If part of the read or write requests are read from or written to the replica availability zone, the network delay will cause a decrease in performance, but I need the intra-city 2-DC feature. What should I do?
You can [submit a ticket](https://console.cloud.tencent.com/workorder/category) indicating the instance ID, deployment scheme of your servers in the availability zone, and the ratio between read and write requests. Tencent Cloud DBA can help you adjust the dual-availability zone loading mechanism to minimize the number of read and write requests sustained by the replica availability zone.

#### 5. If I want to change from the 1-DC architecture to intra-city 2-DC architecture, what should I do?
Check whether the intra-city 2-DC scheme is supported in your region. It is now available in Beijing. Then, submit a ticket indicating the information of the account to be adjusted, instance ID, two availability zones to be used, and recommended OPS time. Tencent Cloud staff will conduct an audit. If your request is eligible, the operation can be performed; otherwise, it will be rejected.
