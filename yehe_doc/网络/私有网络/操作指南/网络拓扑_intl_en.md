The network topology map displays all VPC resources, so that you can obtain VPC deployments and connections in real time.

## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **Network Topology Map** on the left sidebar.
    ![](https://main.qcloudimg.com/raw/c7e8ecf743767784df696cf149413d75.png)
3. Select a region and VPC to view cloud resources of the VPC such as CVM, CLB, TencentDB, and NoSQL, and their network topology relation.
  In the two subnets of the sample VPC as shown below, the `test6` subnet contains two CLB instances. This VPC communicates with the Internet through NAT Gateway and public network CLB. It communicates with the opposite VPC through peering connection.
    ![](https://main.qcloudimg.com/raw/1cc6ff3a212bc7ef26b261ba8610cba5.png)
