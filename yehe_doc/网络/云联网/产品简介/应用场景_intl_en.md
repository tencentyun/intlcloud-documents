## Scenario 1. Building a Hybrid Cloud
#### Scenario Description
You have business VPC and disaster recovery VPC in the cloud as well as self-built IDC off the cloud and you want to achieve resource interconnection.

#### Solution
You can build multiple cloud IDCs in Tencent Cloud and then connect them to local IDCs using Direct Connect, thus building a hybrid cloud that enables cloud-based disaster recovery and elastic business deployment. 
After creating a CCN instance, you only have to join the direct connect gateway connecting the IDC, elastic business VPC and backup IDCs to the instance, eliminating the need to create multiple peering connections and Direct Connect tunnels, and generating routes automatically to significantly simplify configuration.
Outcomes:
- Join VPCs in CCN to implement automatic routing, eliminating the need to create multiple peering connections.
- Join a direct connect gateway to CCN and connect multiple VPCs  through one dedicated tunnel, meeting your needs for interconnection between local IDC and cloud data.

![](https://main.qcloudimg.com/raw/d3f95cbed44e0fc8cb29692c259d2985.svg)

## Scenario 2. Online Education
#### Scenario Description
With teachers and students located in different regions, many VPCs and connections are needed for the interconnection using peering connection. In addition, live broadcasting platforms for online education are required to build high-quality interconnection covering multiple regions so as to ensure clear audio and video communications during cross-regional transfer.

#### Solution
Based on the coverage in over 20 regions, Tencent Cloud CCN connects VPCs from POP in multiple regions easily. It uses the intelligent full-mesh scheduling algorithm to connect any two points through the shortest path on the private network with no public network bypassing and link congestion, providing global multi-point interconnection with reduced latency. 
Outcomes:
- Teachers and students have local access to the services with high transfer quality and low delay guaranteed.
- VPCs in different regions can interconnect with all other instances once connected to CCN.

![](https://main.qcloudimg.com/raw/e54118915b4ab0690980b7905b25fd1b.svg)
## Scenario 3. Gaming Acceleration
#### Scenario Description 
Online games typically have players and servers deployed in multiple regions. CCN helps meet the latency requirements of players in scenarios such as cross-server PvP battles by enabling local access.
#### Solution 
Based on the coverage in over 20 regions, Tencent Cloud CCN connects VPCs from POP in multiple regions easily. With the full-mesh network topology and monitoring of routing and real-time bandwidth and with no public network bypassing or link congestion, CCN has an intelligent scheduling system to achieve low-latency interconnection, allowing global players to battle on the same servers for an ultimate gaming experience. 
Outcomes:
- Players have local access to the service VPCs with low latency.
- CCN uses the full-mesh topology to support multi-region VPC joining for building a global network.

![](https://main.qcloudimg.com/raw/1af02ff907b2eb9cea38a05b2a27b8e7.svg)
