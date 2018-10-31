## Scenario 1. Building a Hybrid Cloud Solution
#### Scenario Description
You have business VPC and disaster recovery VPC in the cloud as well as self-built IDC off the cloud and you want to achieve resource interconnection.

#### Solution
Multiple cloud IDCs can be built in Tencent Cloud and then connected to local IDCs through Direct Connect lines, creating a hybrid cloud that enables cloud-based disaster recovery and elastic business deployment. 
After creating a CCN instance, you only have to join the Direct Connect gateway connecting the IDC, elastic business VPC and backup VPC to the instance, eliminating the need to create multiple peering connections and Direct Connect tunnels and generating routes automatically to significantly simplify configuration.
Outcomes:

- There is no need to create multiple peering connections for interconnecting multiple VPCs. Once they are joined to CCN, the routes are automatically distributed with no repeated operations required.
- Direct Connect gateway can be joined to CCN and multiple VPCs can be connected through one Direct Connect tunnel, meeting your needs for interconnection between local IDC and cloud data.

![](https://main.qcloudimg.com/raw/b7a745ef998e3c73eccea6ae7fdb75e6.png)

## Scenario 2. Online Education
#### Scenario Description
In online education scenarios, teachers and students are located all over the world and there are many VPCs. To interconnect them one by one through peering connection, it requires the creation of many connections. In addition, live broadcasting platforms for online education are required to build high-quality interconnection covering multiple regions so as to ensure clear audio and video communications during cross-regional transfer.

#### Solution
Based on CCN's coverage in over 20 regions around the globe, POP access VPCs in multiple regions can be joined to CCN with easy operations and management; leveraging the intelligent full-mesh scheduling algorithm, any two points can be interconnected through the shortest path on the private network with no public network bypassing and link congestion, providing global multi-point interconnection with reduced latency. 
Outcomes:

- Teachers and students have local access to the services with high transfer quality and low delay guaranteed.
- Once joined to CCN for the first time, the VPCs in different regions can interconnect with all instances without having to set up connections one by one.

![](
https://main.qcloudimg.com/raw/db9c81c795bfa80ad160866e270e8f68.png)

## Scenario 3. Gaming Acceleration
#### Scenario Description 
Online games typically have players all over the world who need to access latency-sensitive services. It requires the deployment of multiple servers in multiple regions to enable local assess for players and meet their gaming needs in scenarios such as cross-server PvP battles.
#### Solution 
With coverage in over 20 regions around the globe, POP access VPCs in multiple regions can be joined to CCN with easy operations and management; based on full-mesh network topology and monitoring of routing and real-time bandwidth and with no public network bypassing or link congestion, CCN uses an intelligent scheduling system to achieve low-latency interconnection, allowing global players to battle on the same servers for an ultimate gaming experience. 
Outcomes:

- Players have local access to the service VPCs with low latency.
- Full-mesh topology supports multi-region VPC joining for building a global network.

![](https://main.qcloudimg.com/raw/c8bc1797e156acec0df396474452bd04.png)
