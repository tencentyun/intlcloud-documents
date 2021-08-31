## Use Case 1. Building a Hybrid Cloud
#### Background
You have deployed a business VPC and a disaster recovery VPC on Tencent Cloud, and own an on-premise IDC off the cloud. You want to implement resource interconnection between your VPCs and the on-premise IDC.

#### Solution
Launch a cloud-based environment on Tencent Cloud, and connect it to the local IDC using Direct Connect. In this way, data is stored on cloud for disaster recovery, and elastic services can be deployed locally and on-cloud, creating a hybrid cloud solution. 
After creating a CCN instance, you only need to integrate the direct connect gateway connected with the IDC, elastic business VPC and backup data centers into the instance. You do not need to create multiple peering connections and Direct Connect tunnels. The routes are generated automatically, which greatly simplifies the configuration workload.
Outcomes:
- Add VPCs to CCN to implement automatic routing, eliminating the need to create multiple peering connections.
- Add a direct connect gateway to CCN and connect multiple VPCs through one dedicated tunnel, achieving interconnection between your on-premise and on-cloud environments.

![](https://main.qcloudimg.com/raw/d3f95cbed44e0fc8cb29692c259d2985.svg)

## Use Case 2. Online Education
#### Background
Teachers and students are located in different geographic locations for distance learning, making multiple VPCs and connections necessary for the interconnection if peering connection is used. High-quality interconnection across different regions is also required for live streaming platforms so as to ensure clear audio and video communications.

#### Solution
Based on Tencent Cloud's coverage in over 20 regions around the globe and intelligent full-mesh scheduling algorithm, any two points can be interconnected through the shortest path on the private network with no public network bypassing and link congestion, providing global multi-point interconnection with reduced latency. 
Outcomes:
- Teachers and students have local access to online services with high transfer quality and low latency.
- VPCs in different regions can interconnect with all other instances once connected to CCN.

![](https://main.qcloudimg.com/raw/e54118915b4ab0690980b7905b25fd1b.svg)
## Use Case 3. Gaming Acceleration
#### Background 
Online games have players around the world and is latency-sensitive. Multiple servers need to be deployed in different regions in order to meet the requirements of local access and cross-server PvP battles.
#### Solution 
With coverage in over 20 regions around the globe and based on full-mesh network topology and monitoring of routing and real-time bandwidth, CCN uses an intelligent scheduling system to achieve low-latency interconnection, allowing global players to battle on the same servers for an ultimate gaming experience. 
Outcomes:
- Players have local access to the service VPCs with low latency.
- CCN uses a full-mesh topology to support multi-region VPC connection for a global network.

![](https://main.qcloudimg.com/raw/1af02ff907b2eb9cea38a05b2a27b8e7.svg)
