EMR uses Tencent Cloud VPC as the underlying network. Security groups in EMR are used as virtual firewalls to control the access between the internal nodes in a cluster and access from external nodes to internal nodes. This document describes the best practices of using security groups in EMR to help you choose security group policies.

## Security Groups
A security group is a virtual firewall for stateful data packet filtering. As an important network isolation approach provided by Tencent Cloud, it is used to control network access to CVM instances (nodes). When creating an EMR cluster, you can select an existing security group. If there is no existing security group, EMR will automatically create one for you. If the number of security groups has reached the upper limit and you want to create a new one, delete those you no longer use. You can view existing security groups in the [VPC console](https://console.cloud.tencent.com/vpc/securitygroup). 

## Use Limits and Rules
For use limits and quotas of security groups, see the **Security Group Limits** section in [Use Limits Overview](https://intl.cloud.tencent.com/document/product/213/15379).

A security group rule consists of:
- Source: IP address of the source data (inbound) or target data (outbound)
- Protocol type and protocol port: protocol type such as TCP and UDP
- Policy: allow or reject access requests

## Rules for Selecting a Security Group
By default, **Select an existing security group** is selected and an EMR security group is selected. You can create a new EMR security group or select a non-EMR security group.
1. For a new EMR security group, port 22, port 30001, and necessary private network IP ranges are enabled. The security group is named in the format of "emr-xxxxxxxx_yyyyMMdd". Do not modify its name.
2. Select an existing security group available in the current region for the current instance. A security group starting with "emr" is recommended, as EMR service has been activated and necessary policies are running properly for such security groups. Security groups not starting with "emr" may lack necessary inbound and outbound rules. This may cause cluster creation failure or cluster unavailability.
3. If you add nodes in a cluster, by default, the nodes inherit the security group policy selected for the cluster when it is created.

## Details of EMR Security Group Policies
If you select a non-EMR security group when creating an EMR cluster, the following inbound and outbound rules must be included. Otherwise, the cluster creation will fail.
### Inbound rules

| **Source** | **Protocol Port** | **Policy** | **Note** |      
| -------------- | ------------ | -------- | ------------ |
| 10.0.0.0/8 | ALL | ACCEPT | Opens IP range A. |      
| 172.16.0.0/12 | ALL | ACCEPT | Opens IP range B. |      
| 192.168.0.0/16 | ALL | ACCEPT | Opens IP range C. |      
| 0.0.0.0/0 | ICMP | ACCEPT | Opens local ICMP. |      


### Outbound rules

| **Source** | **Protocol Port** | **Policy** | **Note** |
| --------- | ------------ | -------- | ------------ |
| 0.0.0.0/0 | ALL | ACCEPT | Opens all outbound ports. |

### Inbound rules for accessing webUI
To access the cluster service WebUI normally when using a non-EMR security group, the inbound rules must include the following policies:

| **Source** | **Protocol Port** | **Policy** | **Note** |      
| --------- | ------------ | -------- | ----------------- | 
| 0.0.0.0/0 | TCP:13000 | ACCEPT | Opens port 13000 and port hue. |      
| 0.0.0.0/0 | TCP:30001 | ACCEPT | Opens port 30001. |      
| 0.0.0.0/0 | TCP:30002 | ACCEPT | Opens port 30002. |      
| 0.0.0.0/0 | TCP:22 | ACCEPT | Opens the remote login port.  |      

For more information, see [Security Group](https://intl.cloud.tencent.com/document/product/213/12452).
