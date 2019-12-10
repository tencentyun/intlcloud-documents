## Scenario 1: Creating a Hybrid Cloud
#### Scenario Description
A customer has deployed a business VPC and a disaster recovery VPC on Tencent Cloud, and a IDC on premises. The customer wants to implement resource interconnection between the VPCs and the IDC.

#### Solution
Create multiple data centers on Tencent Cloud, and connect them to local IDC through direct connections. In this way, data is stored on cloud for disaster recovery, and elastic services are deployed in local, so as to build up a hybrid cloud. 
CCN connects local IDCs, cloud-based elastic service expansion zones and backup IDCs, eliminating the need to create multiple peering connections and Direct Connect tunnels and generating routes automatically to simplify configuration. 
Achievements:
- Add VPCs to CCN to implement automatic routing, eliminating the need to create multiple peering connections.
- By adding a direct connect gateway to CCN, one dedicated tunnel can connects multiple VPCs, so as to implement the data communication between local IDC and data on cloud.

![](https://main.qcloudimg.com/raw/b7a745ef998e3c73eccea6ae7fdb75e6.png)

## Scenario 2: Online Education
#### Scenario Description
With teachers and students located all over the world, live broadcasting platforms for online education are required to build high-quality interconnection covering multiple regions so as to ensure clear audio and video communications during cross-regional transfer.

#### Solution
Based on Tencent Cloud's coverage in over 20 regions around the globe and intelligent full-mesh scheduling algorithm, any two points can be interconnected through the shortest path on the private network with no public network bypassing and link congestion, providing global multi-point interconnection with reduced latency. 
Achievements:
- Teachers and students can access the nearest online education services, to enjoy the highest quality with the lowest delay.
- VPCs in different regions can interconnect with all of other instances once connected to CCN.

![](
https://main.qcloudimg.com/raw/db9c81c795bfa80ad160866e270e8f68.png)

## Scenario 3: Gaming Acceleration
#### Scenario Description 
Online games typically have players all over the world and servers deployed in multiple regions. CCN helps meet the sensitive latency requirements of players in scenarios such as cross-server PvP battles by enabling local access.
#### Solution 
With coverage in over 20 regions around the globe and based on full-mesh network topology and monitoring of routing and real-time bandwidth, CCN uses an intelligent scheduling system to achieve low-latency interconnection, allowing global players to battle on the same servers for an ultimate gaming experience. 
Achievements:
- Gamers at different locations can access the nearest serving VPCs to implement interconnection with a low latency.
- With the topology of public and private networks, CCN allows you to add VPCs from multiple regions to create a global network.

![](https://main.qcloudimg.com/raw/d745ea747268667fb14164760c7c856f.png)
