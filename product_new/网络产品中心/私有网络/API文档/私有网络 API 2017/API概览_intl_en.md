## 1. VPC APIs

| API function | Action ID | Description |
| --------------- | ---------------------------------------- | ----------------------- |
| Create a VPC | [CreateVpc](http://intl.cloud.tencent.com/doc/api/245/%E5%88%9B%E5%BB%BA%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9C) | Create a VPC and configure its IP range. |
| Delete a VPC | [DeleteVpc](http://intl.cloud.tencent.com/doc/api/245/%E5%88%A0%E9%99%A4%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9C) | Delete a VPC. |
| Change the VPC name | [ModifyVpcAttribute](http://intl.cloud.tencent.com/doc/api/245/%E4%BF%AE%E6%94%B9%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9C%E5%90%8D%E7%A7%B0) | Change the name of the specified VPC. |
| Query the VPC list | [DescribeVpcEx](http://intl.cloud.tencent.com/doc/api/245/%E6%9F%A5%E8%AF%A2%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9C%E5%88%97%E8%A1%A8) | Batch query VPC information, supports paging query and fuzzy matching. |
| Bind a VPC CVM to a VIP | [AssociateVip](http://intl.cloud.tencent.com/doc/api/245/%E7%BB%91%E5%AE%9A%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9C%E5%86%85%E4%B8%BB%E6%9C%BA%E4%B8%8EVIP) | Bind a VIP to a VPC CVM. |
| Establish a connection between the VPC and basic network devices | [AttachClassicLinkVpc](https://intl.cloud.tencent.com/doc/api/245/2098) | Create a connection between the VPC and basic network devices. |
| Delete the connection between the VPC and basic network devices | [DetachClassicLinkVpc](https://intl.cloud.tencent.com/doc/api/245/2097) | Delete the connection between the VPC and basic network devices. |
| Query the connections between the VPC and basic network devices | [DescribeVpcClassicLink](https://intl.cloud.tencent.com/document/api/215/2112) | Query the connections between the VPC and basic network devices. |

## 2. Subnet APIs
| API function | Action ID | Description |
| ------ | ---------------------------------------- | ------------------------------------- |
| Create a subnet | [CreateSubnet](http://intl.cloud.tencent.com/doc/api/245/%E5%88%9B%E5%BB%BA%E5%AD%90%E7%BD%91) | Create a subnet and specify its availability zone. |
| Delete a subnet | [DeleteSubnet](http://intl.cloud.tencent.com/doc/api/245/%E5%88%A0%E9%99%A4%E5%AD%90%E7%BD%91) | Delete the specified subnet. |
| Change the subnet name | [ModifySubnetAttribute](https://intl.cloud.tencent.com/document/api/215/1313) | Change the name of the specified subnet. |
| Query the subnet list | [DescribeSubnetEx](http://intl.cloud.tencent.com/doc/api/245/%E6%9F%A5%E8%AF%A2%E5%AD%90%E7%BD%91%E5%88%97%E8%A1%A8) | Batch query subnet information, supports paging query and fuzzy matching. |
| Query subnet details | [DescribeSubnet](http://intl.cloud.tencent.com/doc/api/245/%E6%9F%A5%E8%AF%A2%E5%AD%90%E7%BD%91%E8%AF%A6%E6%83%85) | Query the details of a subnet based on the input information, such as subnetId and the subnet name. |


## 3. Routing Table APIs
| API function | Action ID | Description |
| -------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Create a routing table | [CreateRouteTable](http://intl.cloud.tencent.com/doc/api/245/%E5%88%9B%E5%BB%BA%E8%B7%AF%E7%94%B1%E8%A1%A8) | Create a routing table. |
| Delete the routing table | [DeleteRouteTable](http://intl.cloud.tencent.com/doc/api/245/%E5%88%A0%E9%99%A4%E8%B7%AF%E7%94%B1%E8%A1%A8) | Delete the specified routing table, after which all the routing policies in the routing table become invalid. |
| Modify the routing table | [ModifyRouteTableAttribute](http://intl.cloud.tencent.com/doc/api/245/%E4%BF%AE%E6%94%B9%E8%B7%AF%E7%94%B1%E8%A1%A8) | Change the name of the specified routing table. |
| Query a routing table | [DescribeRouteTable](http://intl.cloud.tencent.com/doc/api/245/%E6%9F%A5%E8%AF%A2%E8%B7%AF%E7%94%B1%E8%A1%A8) | Query the details of a routing table based on the input information, such as routeTableId and the routing table name. |
| Modify the routing table associated with a subnet | [AssociateRouteTable](https://intl.cloud.tencent.com/document/api/215/1416) | Modify the routing table associated with a subnet. |
| Create a routing policy | [CreateRoute](http://intl.cloud.tencent.com/doc/api/245/5688) | Create a routing policy. |
| Delete a routing policy | [DeleteRoute](http://intl.cloud.tencent.com/doc/api/245/5689) | Delete a routing policy. |


## 4. Network ACL APIs
| API function | Action ID | Description |
| ---------- | ---------------------------------------- | ------------- |
| Create a VPC network ACL | [CreateNetworkAcl](http://intl.cloud.tencent.com/doc/api/245/%E5%88%9B%E5%BB%BAVPC%E7%BD%91%E7%BB%9CACL) | Create a security firewall. |
| Delete a network ACL | [DeleteNetworkAcl](http://intl.cloud.tencent.com/doc/api/245/%E5%88%A0%E9%99%A4%E7%BD%91%E7%BB%9CACL) | Delete the specified security firewall. |
| Change a network ACL name | [ModifyNetworkAcl](http://intl.cloud.tencent.com/doc/api/245/%E4%BF%AE%E6%94%B9%E7%BD%91%E7%BB%9CACL%E5%90%8D%E7%A7%B0) | Change the name of a security firewall. |
| Query the network ACL list | [DescribeNetworkAcl](http://intl.cloud.tencent.com/doc/api/245/%E6%9F%A5%E8%AF%A2%E7%BD%91%E7%BB%9CACL%E5%88%97%E8%A1%A8) | Query the VPC security firewall list. |
| Set network ACL rules | [ModifyNetworkAclEntry](http://intl.cloud.tencent.com/doc/api/245/%E8%AE%BE%E7%BD%AE%E7%BD%91%E7%BB%9CACL%E8%A7%84%E5%88%99) | Set security firewall ACL rules. |
| Bind a network ACL to a subnet | [CreateSubnetAclRule](http://intl.cloud.tencent.com/doc/api/245/%E7%BD%91%E7%BB%9CACL%E7%BB%91%E5%AE%9A%E5%AD%90%E7%BD%91) | Bind a security firewall with a subnet. |
| Unbind a network ACL from a subnet | [DeteleSubnetAclRule](http://intl.cloud.tencent.com/doc/api/245/%E7%BD%91%E7%BB%9CACL%E8%A7%A3%E7%BB%91%E5%AD%90%E7%BD%91) | Unbind a security firewall from a subnet. |


## 5. VPN APIs
| API function | Action ID | Description |
| --------- | ---------------------------------------- | -------------------------------- |
| Query the price of a VPN gateway | [InquiryVpnPrice](http://intl.cloud.tencent.com/doc/api/245/5104) | Query the price of a VPN gateway. |
| Purchase a VPN gateway | [CreateVpn](http://intl.cloud.tencent.com/doc/api/245/5106) | Purchase a VPN gateway. |
| Modify VPN gateway attributes | [ModifyVpnGw](http://intl.cloud.tencent.com/doc/api/245/5107) | Modify the information of the specified VPN gateway, such as the name. |
| Query the VPN gateway list | [DescribeVpnGw](http://intl.cloud.tencent.com/doc/api/245/5108) | Query the information of a VPN gateway based on the iinput information, such as the ID and name of the VPN gateway. |
| Renew a VPN gateway | [RenewVpn](http://intl.cloud.tencent.com/doc/api/245/5109) | Renew a VPN gateway. |

## 6. User Gateway APIs
| API function | Action ID | Description |
| -------------- | ---------------------------------------- | ------------------------------ |
| Create a user gateway | [AddUserGw](http://intl.cloud.tencent.com/doc/api/245/5116) | Create a user gateway to be connected to. |
| Delete a user gateway | [DeleteUserGw](http://intl.cloud.tencent.com/doc/api/245/5117) | Delete a user gateway. |
| Change the name of a user gateway | [ModifyUserGw](http://intl.cloud.tencent.com/doc/api/245/5118) | Change the name of a user gateway. |
| Query the user gateway list | [DescribeUserGw](http://intl.cloud.tencent.com/doc/api/245/5119) | Query the information of a user gateway based on input information, such as the ID and name of the user gateway. |
| Obtain information about supported user gateway vendors | [DescribeUserGwVendor](http://intl.cloud.tencent.com/doc/api/245/5120) | Query the information about user gateway vendors supported by Tencent Cloud VPN gateways. |


## 7. VPN Tunnel APIs
| API function | Action ID | Description |
| ------------ | ---------------------------------------- | -------------------------- |
| Create a VPN tunnel | [AddVpnConnEx](http://intl.cloud.tencent.com/doc/api/245/5110) | Create an encrypted VPN tunnel to connect a VPC to other network resources. |
| Delete a VPN tunnel | [DeleteVpnConn](http://intl.cloud.tencent.com/doc/api/245/5111) | Delete the specified VPN tunnel. |
| Modify a VPN tunnel | [ModifyVpnConnEx](http://intl.cloud.tencent.com/doc/api/245/5112) | Modify the information of the specified VPN tunnel, such as the name. |
| Query the VPN tunnel list | [DescribeVpnConn](http://intl.cloud.tencent.com/doc/api/245/5113) | Query the information of a tunnel based on input information, such as the ID and name of the VPN tunnel. |
| Download VPN tunnel configuration | [GetVpnConnConfig](http://intl.cloud.tencent.com/doc/api/245/5114) | Download the configuration of a VPN tunnel to modify it. |
| Obtain the monitoring data of a VPN tunnel | [DescribeVpnConnMonitor](http://intlcloud.tencent.com/doc/api/245/5115) | Obtain the monitoring data of a VPN tunnel. |

## 8. SSL VPN APIs
| API function | Action ID | Description |
| --------- | ---------------------------------------- | ---------- |
| Query sslVPN | DescribeSSLVpn | Query sslVPN. |
| Query the sslVPN domain | DescribeSSLVpnDomain | Query the sslVPN domain. |
| Set sslVPN domain | SetSSLVpnDomain | Set the sslVPN domain. |

## 9. Peering Connection APIs
| API function | Action ID | Description |
| ----------- | ---------------------------------------- | ------------ |
| Establish an intra-region peering connection | [CreateVpcPeeringConnection](https://intl.cloud.tencent.com/doc/api/245/2107) | Create an intra-region peering connection. |
| Delete an intra-region peering connection | [DeleteVpcPeeringConnection](https://intl.cloud.tencent.com/doc/api/245/2104) | Delete an intra-region peering connection. |
| Modify an intra-region peering connection | [ModifyVpcPeeringConnection](https://intl.cloud.tencent.com/doc/api/245/2103) | Modify an intra-region peering connection. |
| Accept an intra-region peering connection | [AcceptVpcPeeringConnection](https://intl.cloud.tencent.com/doc/api/245/2106) | Accept an intra-region peering connection. |
| Reject an intra-region peering connection | [RejectVpcPeeringConnection](https://intl.cloud.tencent.com/doc/api/245/2105) | Reject an intra-region peering connection. |
| Enable an expired intra-region peering connection | [EnableVpcPeeringConnection](https://intl.cloud.tencent.com/doc/api/245/2102) | Enable an expired intra-region peering connection. |
| Create a cross-region peering connection | [CreateVpcPeeringConnectionEx](https://intl.cloud.tencent.com/doc/api/245/4803) | Create a cross-region peering connection. |
| Delete a cross-region peering connection | [DeleteVpcPeeringConnectionEx](https://intl.cloud.tencent.com/doc/api/245/4804) | Delete a cross-region peering connection. |
| Modify the attributes of a cross-region peering connection | [ModifyVpcPeeringConnectionEx](https://intl.cloud.tencent.com/doc/api/245/4805) | Modify the attributes of a cross-region peering connection. |
| Accept a cross-region peering connection | [AcceptVpcPeeringConnectionEx](https://intl.cloud.tencent.com/doc/api/245/4806) | Accept a cross-region peering connection. |
| Reject a cross-region peering connection | [RejectVpcPeeringConnectionEx](https://intl.cloud.tencent.com/doc/api/245/4807) | Reject a cross-region peering connection. |
| Enable an expired cross-region peering connection | [EnableVpcPeeringConnectionEx](https://intl.cloud.tencent.com/doc/api/245/4808) | Enable an expired cross-region peering connection. |
| Query a peering connection | [DescribeVpcPeeringConnections](https://intl.cloud.tencent.com/doc/api/245/2101) | Query a peering connection. |

## 10. Direct Connect Gateway APIs
| API function | Action ID | Description |
| ---------------- | ---------------------------------------- | ----------------- |
| Create a direct connect gateway | [CreateDirectConnectGateway](https://intl.cloud.tencent.com/doc/api/245/4824) | Create a direct connect gateway.           |
| Modify the attributes of a direct connect gateway | [ModifyDirectConnectGateway](https://intl.cloud.tencent.com/doc/api/245/4826) | Modify the attributes of a direct connect gateway. |
| Delete a direct connect gateway | [DeleteDirectConnectGateway](https://intl.cloud.tencent.com/doc/api/245/4825) | Delete a direct connect gateway.           |
| Query a direct connect gateway | DescribeDirectConnectGateway | Query a direct connect gateway.           |
| Create a local IP translation rule for a direct connect gateway | [CreateLocalIPTranslationNatRule](https://intl.cloud.tencent.com/doc/api/245/5185) | Create a local IP translation rule for a direct connect gateway. |
| Delete the local IP translation rule for a direct connect gateway | [DeleteLocalIPTranslationNatRule](https://intl.cloud.tencent.com/document/product/215/5186) | Delete the local IP translation rule for a direct connect gateway. |
| Modify the local IP translation rule for a direct connect gateway | [ModifyLocalIPTranslationNatRule](https://intl.cloud.tencent.com/doc/api/245/5187) | Modify the local IP translation rule for a direct connect gateway. |
| Query the local IP translation rule for a direct connect gateway | [DescribeLocalIPTranslationNatRule](https://intl.cloud.tencent.com/doc/api/245/5188) | Query the local IP translation rule for a direct connect gateway. |
| Create a local source IP port translation rule for a direct connect gateway | [CreateLocalSourceIPPortTranslationNatRule](https://intl.cloud.tencent.com/document/api/215/5190) | Create a local source IP port translation rule for a direct connect gateway. |
| Delete the local source IP port translation rule for a direct connect gateway | [DeleteLocalSourceIPPortTranslationNatRule](https://intl.cloud.tencent.com/document/api/215/5191) | Delete the local source IP port translation rule for a direct connect gateway. |
| Modify the local source IP port translation rule for a direct connect gateway | [ModifyLocalSourceIPPortTranslationNatRule](https://intl.cloud.tencent.com/document/api/215/5192) | Modify the local source IP port translation rule for a direct connect gateway. |
| Query the local source IP port translation rule for a direct connect gateway | [DescribeLocalSourceIPPortTranslationNatRule](https://intl.cloud.tencent.com/document/api/215/5193) | Query the local source IP port translation rule for a direct connect gateway. |
| Create a local destination IP port translation rule for a direct connect gateway | [CreateLocalDestinationIPPortTranslationNatRule](https://intl.cloud.tencent.com/document/api/215/5195) | Create a local destination IP port translation rule for a direct connect gateway. |
| Delete the local destination IP port translation rule for a direct connect gateway | [DeleteLocalDestinationIPPortTranslationNatRule](https://intl.cloud.tencent.com/document/product/215/5196) | Delete the local destination IP port translation rule for a direct connect gateway. |
| Modify the local destination IP port translation rule for a direct connect gateway | [ModifyLocalDestinationIPPortTranslationNatRule](https://intl.cloud.tencent.com/document/api/215/5197) | Modify the local destination IP port translation rule for a direct connect gateway. |
| Query the local destination IP port translation rule for a direct connect gateway | [DescribeLocalDestinationIPPortTranslationNatRule](https://intl.cloud.tencent.com/document/api/215/5198) | Query the local destination IP port translation rule for a direct connect gateway. |
| Create a peer IP translation rule for a direct connect gateway | [CreatePeerIPTranslationNatRule](https://intl.cloud.tencent.com/document/api/215/5201) | Create a peer IP translation rule for a direct connect gateway. |
| Delete the peer source IP translation rule for a direct connect gateway | [DeletePeerIPTranslationNatRule](https://intl.cloud.tencent.com/document/api/215/5202) | Delete the peer source IP translation rule for a direct connect gateway. |
| Modify the peer IP translation rule for a direct connect gateway | [ModifyPeerIPTranslationNatRule](https://intl.cloud.tencent.com/document/api/215/5203) | Modify the peer IP translation rule for a direct connect gateway. |
| Query the peer IP translation rule for a direct connect gateway | [DescribePeerIPTranslationNatRule](https://intl.cloud.tencent.com/document/api/215/5204) | Query the peer IP port translation rule for a direct connect gateway. |
| Create a local IP translation ACL policy | [CreateLocalIPTranslationAclRule](https://intl.cloud.tencent.com/doc/api/245/5205) | Create a local IP translation ACL policy. |
| Delete a local IP translation ACL policy | [DeleteLocalIPTranslationAclRule](https://intl.cloud.tencent.com/doc/api/245/5206) | Delete a local IP translation ACL policy. |
| Modify a local IP translation ACL policy | [ModifyLocalIPTranslationAclRule](https://intl.cloud.tencent.com/doc/api/245/5207) | Modify a local IP translation ACL policy. |
| Query a local IP translation ACL policy | [DescribeLocalIPTranslationAclRule](https://intl.cloud.tencent.com/doc/api/245/5208) | Query a local IP translation ACL policy. |
| Create a local IP port translation ACL policy | [CreateLocalSourceIPPortTranslationAclRule](https://intl.cloud.tencent.com/doc/api/245/5211) | Create a local IP port translation ACL policy. |
| Delete a local IP port translation ACL policy | [DeleteLocalSourceIPPortTranslationAclRule](https://intl.cloud.tencent.com/doc/api/245/5212) | Delete a local IP port translation ACL policy. |
| Modify a local IP port translation ACL policy | [ModifyLocalSourceIPPortTranslationAclRule](https://intl.cloud.tencent.com/doc/api/245/5213) | Modify a local IP port translation ACL policy. |
| Query a local IP port translation ACL policy | [DescribeLocalSourceIPPortTranslationAclRule](https://intl.cloud.tencent.com/doc/api/245/5214) | Query a local IP port translation ACL policy. |

## 11. NAT Gateway APIs
| API function | Action ID | Description |
| ----------- | ---------------------------------------- | ------------ |
| Create a NAT Gateway | [CreateNatGateway](https://intl.cloud.tencent.com/doc/api/245/4094) | Create a NAT gateway. |
| Query the NAT gateway creation progress | [QueryNatGatewayProductionStatus](https://intl.cloud.tencent.com/doc/api/245/4089) | Query the creation progress of a NAT gateway. |
| Delete a NAT gateway | [DeleteNatGateway](https://intl.cloud.tencent.com/doc/api/245/4087) | Delete a NAT gateway. |
| Modify a NAT gateway | [ModifyNatGateway](https://intl.cloud.tencent.com/doc/api/245/4086) | Modify a NAT gateway. |
| Query a NAT gateway | [DescribeNatGateway](https://intl.cloud.tencent.com/doc/api/245/4088) | Query a NAT gateway. |
| Bind an EIP to a NAT gateway | [EipBindNatGateway](https://intl.cloud.tencent.com/doc/api/245/4093) | Bind an EIP to a NAT gateway. |
| Unbind an EIP from a NAT gateway | [EipUnBindNatGateway](https://intl.cloud.tencent.com/doc/api/245/4092) | Unbind an EIP from a NAT gateway. |
| Upgrade NAT gateway specification | [UpgradeNatGateway](https://intl.cloud.tencent.com/doc/api/245/4090) | Upgrade the specification of a NAT gateway. |

## 12. ENI APIs
| API function | Action ID | Description |
| ---------- | ---------------------------------------- | ----------- |
| Create an ENI | [CreateNetworkInterface](https://intl.cloud.tencent.com/doc/api/245/4811) | Create an ENI. |
| Delete an ENI | [DeleteNetworkInterface](https://intl.cloud.tencent.com/doc/api/245/4813) | Delete an ENI. |
| Query ENI Information | [DescribeNetworkInterfaces](https://intl.cloud.tencent.com/doc/api/245/4814) | Query the information of an ENI. |
| Assign a private IP address for an ENI | [AssignPrivateIpAddresses](https://intl.cloud.tencent.com/doc/api/245/4817) | Assign a private IP address for an ENI. |
| Unassign a private IP address from an ENI | [UnassignPrivateIpAddresses](https://intl.cloud.tencent.com/doc/api/245/4819) | Unassign a private IP address from an ENI. |
| Bind an ENI to a CVM | [AttachNetworkInterface](https://intl.cloud.tencent.com/doc/api/245/4820) | Bind an ENI to a CVM. |
| Unbind an ENI from a CVM | [DetachNetworkInterface](https://intl.cloud.tencent.com/document/product/215/4822) | Unbind an ENI from a CVM. |
| Migrate an ENI | [MigrateNetworkInterface](https://intl.cloud.tencent.com/doc/api/245/5384) | Migrate an ENI. |
| Migrate a private IP address | [MigratePrivateIpAddress](https://intl.cloud.tencent.com/doc/api/245/5385) | Migrate a private IP address. |

## 13. Flow Log APIs
| API function | Action ID | Description |
| ------- | ---------------------------------------- | ---------- |
| Create a flow log | CreateFlowLog| Create a flow log. |
| Delete a flow log | DeleteFlowLog | Delete a flow log. |
| Query flow log information | DescribeFlowLog | Query the information of a flow log. |
| Query the flow log list | DescribeFlowLogs | Query the information of the flow log list. |
| Modify flow log attributes | ModifyFlowLogAttribute | Modify the attributes of a flow log. |
