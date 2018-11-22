
CCN can help you connect the VPCs in the cloud and the IDCs off the cloud, making it easy to build a simple, intelligent, secure and flexible hybrid cloud and globally interconnected network.
## Example
Connect three VPCs and one IDC under your account through CCN, which are: 
1. Subnet A (192.168.1.0/24) in VPC1 in Guangzhou.
2. Subnet B (10.0.3.0/24) in VPC2 in Shanghai.
3. IDC1 (10.0.1.0/24) in Beijing (connected to Direct Connect gateway 1).
4. Subnet D (172.16.1.0/24) in VPC3 in Beijing.

![](https://main.qcloudimg.com/raw/1ad42871765d9503dab3740612cd85e6.png)

## Steps
In order to realize the purpose above, you need to complete the following steps:
- [Step 1: Create a CCN instance](/document/product/877/18764)
- [Step 2: Associate a network instance (VPC/Direct Connect gateway)](/document/product/877/18765)
- [Step 3: Check the routing table](/document/product/877/18766)
- [Step 4: Set the outbound bandwidth limit](/document/product/877/18767)

