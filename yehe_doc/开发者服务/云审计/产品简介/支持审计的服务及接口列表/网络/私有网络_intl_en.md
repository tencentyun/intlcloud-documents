Virtual Private Cloud (VPC) is a private network space in Tencent Cloud that provides network services for your Tencent Cloud resources. A VPC is logically isolated from others, where you can customize the network environment, route table, security policies, etc. In addition, it can be connected to the internet, other VPCs, and your local IDC in various means, helping you easily deploy cloud-based network connectivity.

VPC operations supported by CloudAudit are as shown below:

| Operation Name | Resource Type | Event Name |
|------------------|-----|-----------------------------------------------------|
| CCN accepts instance association        | vpc | AcceptAttachCcnInstances                            |
| Accepting intra-region peering connection | vpc | AcceptVpcPeeringConnection                          |
| Accepting cross-region peering connection        | vpc | AcceptVpcPeeringConnectionEx                        |
| Adding shared bandwidth package resource      | vpc | AddBandwidthPackageResources                        |
| Adding the DNAT policy of NAT gateway    | vpc | AddDnaptRule                                        |
| Creating customer gateway           | vpc | AddUserGw                                           |
| Creating VPN tunnel          | vpc | AddVpnConnEx                                        |
| ENI applies for private IP      | vpc | AssignPrivateIpAddresses                            |
| Binding EIP to NAT gateway      | vpc | AssociateNatGatewayAddress                          |
| Associating network ACL with subnet        | vpc | AssociateNetNetwork ACLworkAclSubnets                          |
| Modifying route table associated with subnet       | vpc | AssociateRouteTable                                 |
| Associating CCN instance with network instance          | vpc | AttachCcnInstances                                  |
| Creating Classiclink between VPC and classic network device  | vpc | AttachClassicLinkVpc                                |
| Binding ENI to CVM instance        | vpc | AttachNetworkInterface                              |
| Checking for secondary CIDR block conflict       | vpc | CheckAssistantCidr                                  |
| Checking whether the default subnet can be created       | vpc | CheckDefaultSubnet                                  |
| Querying whether traffic monitoring is enabled for the gateway     | vpc | CheckGatewayFlowMonitor                             |
| Verifying network detection status           | vpc | CheckNetDetectState                                 |
| Creating IP address           | vpc | CreateAddress                                       |
| Creating IP address group          | vpc | CreateAddressGroup                                  |
| Creating ENI and binding it to CVM instance     | vpc | CreateAndAttachNetworkInterface                     |
| Creating secondary CIDR block         | vpc | CreateAssistantCidr                                 |
| Creating shared bandwidth package          | vpc | CreateBandwidthPackage                              |
| Creating CCN instance            | vpc | CreateCcn                                           |
| Creating Direct Connect gateway           | vpc | CreateDirectConnectGateway                          |
| Creating the IDC IP range of Direct Connect gateway in CCN type | vpc | CreateDirectConnectGatewayCcnRoutes                 |
| Adding flow log            | vpc | CreateFlowLog                                       |
| Creating HAVIP          | vpc | CreateHaVip                                         |
| Adding local destination IP port translation     | vpc | CreateLocalDestinationIPPortTranslationNatRule      |
| Adding ACL policy for local IP translation    | vpc | CreateLocalIPTranslationAclRule                     |
| Adding local IP translation         | vpc | CreateLocalIPTranslationNatRule                     |
| Adding ACL policy for local source IP port translation | vpc | CreateLocalSourceIPPortTranslationAclRule           |
| Adding local source IP port translation      | vpc | CreateLocalSourceIPPortTranslationNatRule           |
| Creating NAT gateway          | vpc | CreateNatGateway                                    |
| Creating the port forwarding rule of NAT gateway    | vpc | CreateNatGatewayDestinationIpPortTranslationNatRule |
| Creating network ACL          | vpc | CreateNetworkAcl                                    |
| Creating ENI           | vpc | CreateNetworkInterface                              |
| Adding opposite IP translation         | vpc | CreatePeerIPTranslationNatRule                      |
| Adding routing policy           | vpc | CreateRoute                                         |
| Creating route table            | vpc | CreateRouteTable                                    |
| Creating security group           | vpc | CreateSecurityGroup                                 |
| Creating protocol port           | vpc | CreateService                                       |
| Creating protocol port group          | vpc | CreateServiceGroup                                  |
| Creating subnet             | vpc | CreateSubnet                                        |
| Binding network ACL to subnet        | vpc | CreateSubnetAclRule                                 |
| Creating traffic mirror           | vpc | CreateTrafficMirror                                 |
| Creating VPC           | vpc | CreateVpc                                           |
| Creating intra-region peering connection        | vpc | CreateVpcPeeringConnection                          |
| Creating cross-region peering connection        | vpc | CreateVpcPeeringConnectionEx                        |
| Deleting IP address           | vpc | DeleteAddress                                       |
| Deleting IP address group          | vpc | DeleteAddressGroup                                  |
| Deleting secondary CIDR block         | vpc | DeleteAssistantCidr                                 |
| Deleting shared bandwidth package          | vpc | DeleteBandwidthPackage                              |
| Deleting CCN instance            | vpc | DeleteCcn                                           |
| Deleting Direct Connect gateway           | vpc | DeleteDirectConnectGateway                          |
| Deleting the IDC IP range of Direct connect gateway in CCN type | vpc | DeleteDirectConnectGatewayCcnRoutes                 |
| Deleting flow log            | vpc | DeleteFlowLog                                       |
| Deleting HAVIP          | vpc | DeleteHaVip                                         |
| Deleting local destination IP port translation     | vpc | DeleteLocalDestinationIPPortTranslationNatRule      |
| Deleting ACL policy for local IP translation    | vpc | DeleteLocalIPTranslationAclRule                     |
| Deleting local IP translation         | vpc | DeleteLocalIPTranslationNatRule                     |
| Deleting ACL policy for local source IP port translation | vpc | DeleteLocalSourceIPPortTranslationAclRule           |
| Deleting local source IP port translation      | vpc | DeleteLocalSourceIPPortTranslationNatRule           |
| Deleting NAT gateway          | vpc | DeleteNatGateway                                    |
| Deleting the port forwarding rule of NAT gateway    | vpc | DeleteNatGatewayDestinationIpPortTranslationNatRule |
| Deleting network ACL          | vpc | DeleteNetworkAcl                                    |
| Deleting ENI           | vpc | DeleteNetworkInterface                              |
| Deleting opposite IP translation         | vpc | DeletePeerIPTranslationNatRule                      |
| Deleting routing policy           | vpc | DeleteRoute                                         |
| Deleting route table            | vpc | DeleteRouteTable                                    |
| Deleting protocol port           | vpc | DeleteService                                       |
| Deleting protocol port group          | vpc | DeleteServiceGroup                                  |
| Deleting subnet             | vpc | DeleteSubnet                                        |
| Deleting traffic mirror           | vpc | DeleteTrafficMirror                                 |
| Deleting customer gateway           | vpc | DeleteUserGw                                        |
| Deleting VPC           | vpc | DeleteVpc                                           |
| Deleting intra-region peering connection        | vpc | DeleteVpcPeeringConnection                          |
| Deleting cross-region peering connection        | vpc | DeleteVpcPeeringConnectionEx                        |
| Deleting VPN tunnel          | vpc | DeleteVpnConn                                       |
| Deleting VPN gateway v2        | vpc | DeleteVpnGw                                         |
| Querying account network attribute         | vpc | DescribeAccountVpcAttributes                        |
| Querying network ACL list        | vpc | DescribeAcl                                         |
| Querying IP address list         | vpc | DescribeAddress                                     |
| Querying IP address group          | vpc | DescribeAddressGroups                               |
| Querying secondary CIDR block list       | vpc | DescribeAssistantCidr                               |
| Querying the bandwidth package quota of specified region       | vpc | DescribeBandwidthPackageQuota                       |
| Querying shared bandwidth package          | vpc | DescribeBandwidthPackages                           |
| Querying the list of network instances associated with CCN instance      | vpc | DescribeCcnAttachedInstances                        |
| Querying the outbound bandwidth upper limit of all regions of CCN instance    | vpc | DescribeCcnRegionBandwidthLimits                    |
| Querying CCN instance routing policy        | vpc | DescribeCcnRoutes                                   |
| Querying CCN instance list          | vpc | DescribeCcns                                        |
| Querying Direct Connect gateway           | vpc | DescribeDirectConnectGateway                        |
| Querying the IDC IP range of Direct connect gateway in CCN type | vpc | DescribeDirectConnectGatewayCcnRoutes               |
| Querying Direct Connect gateway           | vpc | DescribeDirectConnectGateways                       |
| Querying flow log list          | vpc | DescribeFlowLogs                                    |
| Querying whether traffic monitoring is enabled for the gateway     | vpc | DescribeGatewayMonitor                              |
| Querying the upper limit of visiting IP bandwidth       | vpc | DescribeGatewayQos                                  |
| Querying HAVIP list        | vpc | DescribeHaVips                                      |
| Querying the local destination IP port translation of Direct Connect gateway | vpc | DescribeLocalDestinationIPPortTranslationNatRule    |
| Querying local IP translation ACL rule   | vpc | DescribeLocalIPTranslationAclRule                   |
| Querying the local IP translation of Direct Connect gateway     | vpc | DescribeLocalIPTranslationNatRule                   |
| Querying local IP port translation ACL rule | vpc | DescribeLocalSourceIPPortTranslationAclRule         |
| Querying the local source IP port translation of Direct Connect gateway  | vpc | DescribeLocalSourceIPPortTranslationNatRule         |
| Querying high-availability gateway          | vpc | DescribeNatGateway                                  |
| Querying NAT gateway v3        | vpc | DescribeNatGateways                                 |
| Querying network detection list         | vpc | DescribeNetDetects                                  |
| Querying the list of network detection verification results     | vpc | DescribeNetDetectStates                             |
| Querying network ACL list        | vpc | DescribeNetworkAcls                                 |
| Querying ENI IP quota       | vpc | DescribeNetworkInterfaceAttribute                   |
| Querying ENI information         | vpc | DescribeNetworkInterfaces                           |
| Querying the opposite IP translation of Direct connect gateway     | vpc | DescribePeerIPTranslationNatRule                    |
| Querying the list of routing policy conflicts       | vpc | DescribeRouteConflicts                              |
| Querying routing policy           | vpc | DescribeRoutes                                      |
| Querying route table            | vpc | DescribeRouteTable                                  |
| Querying protocol port list         | vpc | DescribeService                                     |
| Querying protocol port group          | vpc | DescribeServiceGroups                               |
| Querying SSL VPN         | vpc | DescribeSSLVpn                                      |
| Querying subnet attribute           | vpc | DescribeSubnet                                      |
| Viewing subnet list           | vpc | DescribeSubnetEx                                    |
| Querying parameter template quota         | vpc | DescribeTemplateLimits                              |
| Querying traffic mirror           | vpc | DescribeTrafficMirrors                              |
| Querying customer gateway           | vpc | DescribeUserGw                                      |
| Querying Classiclink between VPC and classic network device  | vpc | DescribeVpcClassicLink                              |
| Querying VPC list         | vpc | DescribeVpcEx                                       |
| Querying CVM instance information          | vpc | DescribeVpcInstances                                |
| Querying VPC limit information        | vpc | DescribeVpcLimit                                    |
| Getting VPC quota         | vpc | DescribeVpcLimits                                   |
| Querying VPC peering connection       | vpc | DescribeVpcPeeringConnections                       |
| Querying task execution result        | vpc | DescribeVpcTaskResult                               |
| Querying VPN tunnel          | vpc | DescribeVpnConn                                     |
| Querying VPN gateway          | vpc | DescribeVpnGw                                       |
| Dissociating CCN instance from network instance         | vpc | DetachCcnInstances                                  |
| Deleting Classiclink between VPC and classic network CVM instance | vpc | DetachClassicLinkVpc                                |
| Unbinding ENI from CVM instance        | vpc | DetachNetworkInterface                              |
| Unbinding network ACL from subnet        | vpc | DeteleSubnetAclRule                                 |
| Disabling CCN route          | vpc | DisableCcnRoutes                                    |
| Disabling gateway traffic monitoring         | vpc | DisableGatewayFlowMonitor                           |
| Disabling subnet route           | vpc | DisableRoutes                                       |
| Unbinding EIP from NAT gateway      | vpc | DisassociateNatGatewayAddress                       |
| Disassociating network ACL from subnet       | vpc | DisassociateNetworkAclSubnets                       |
| Binding NAT gateway to EIP       | vpc | EipBindNatGateway                                   |
| Unbinding NAT gateway from EIP       | vpc | EipUnBindNatGateway                                 |
| Enabling CCN route          | vpc | EnableCcnRoutes                                     |
| Enabling gateway traffic monitoring         | vpc | EnableGatewayFlowMonitor                            |
| Enabling subnet route           | vpc | EnableRoutes                                        |
| Enabling expired cross-region peering connection      | vpc | EnableVpcPeeringConnectionEx                        |
| Querying the bandwidth information of CCN regions    | vpc | GetCcnRegionBandwidthLimits                         |
| Getting the product information for creating CCN bandwidth   | vpc | GetCreateCcnBandwidthDeal                           |
| Getting the DNAT policy of NAT gateway    | vpc | GetDnaptRule                                        |
| Querying the discount allowlist of cross-region communication      | vpc | GetPeerWhiteList                                    |
| Binding HAVIP to EIP       | vpc | HaVipAssociateAddressIp                             |
| Unbinding HAVIP from EIP       | vpc | HaVipDisassociateAddressIp                          |
| Querying price when creating cross-region CCN bandwidth    | vpc | InquiryPriceCreateCcnBandwidth                      |
| Querying price for CCN instance bandwidth renewal      | vpc | InquiryPriceRenewCcnBandwidth                       |
| Querying price when modifying cross-region CCN bandwidth    | vpc | InquiryPriceUpdateCcnBandwidth                      |
| Migrating ENI           | vpc | MigrateNetworkInterface                             |
| Migrating private IP           | vpc | MigratePrivateIpAddress                             |
| Editing IP address attribute         | vpc | ModifyAddressAttribute                              |
| Editing IP address group attribute        | vpc | ModifyAddressGroupAttribute                         |
| Modifying secondary CIDR block         | vpc | ModifyAssistantCidr                                 |
| Modifying shared bandwidth package attribute          | vpc | ModifyBandwidthPackageAttribute                     |
| Modifying CCN attribute       | vpc | ModifyCcnAttribute                                  |
| Modifying the bandwidth limit policy of postpaid product    | vpc | ModifyCcnRegionBandwidthLimitsType                  |
| Modifying Direct Connect gateway attribute         | vpc | ModifyDirectConnectGatewayAttribute                 |
| Modifying flow log attribute          | vpc | ModifyFlowLogAttribute                              |
| Modifying HAVIP attribute        | vpc | ModifyHaVipAttribute                                |
| Modifying the local destination IP port translation of Direct Connect gateway | vpc | ModifyLocalDestinationIPPortTranslationNatRule      |
| Modifying local IP translation ACL rule   | vpc | ModifyLocalIPTranslationAclRule                     |
| Modifying the local IP translation of Direct Connect gateway     | vpc | ModifyLocalIPTranslationNatRule                     |
| Modifying local IP port translation ACL rule | vpc | ModifyLocalSourceIPPortTranslationAclRule           |
| Modifying the local source IP port translation of Direct Connect gateway  | vpc | ModifyLocalSourceIPPortTranslationNatRule           |
| Modifying NAT gateway          | vpc | ModifyNatGateway                                    |
| Modifying NAT gateway attribute       | vpc | ModifyNatGatewayAttribute                           |
| Modifying the port forwarding rule of NAT gateway     | vpc | ModifyNatGatewayDestinationIpPortTranslationNatRule |
| Changing network detection           | vpc | ModifyNetDetect                                     |
| Modifying network ACL attribute        | vpc | ModifyNetworkAclAttribute                           |
| Modifying network ACL rule        | vpc | ModifyNetworkAclEntries                             |
| Setting ACL rule          | vpc | ModifyNetworkAclEntry                               |
| Modifying ENI           | vpc | ModifyNetworkInterface                              |
| Modifying the opposite IP translation of Direct Connect gateway     | vpc | ModifyPeerIPTranslationNatRule                      |
| Modifying ENI private IP attribute     | vpc | ModifyPrivateIpAddress                              |
| Replacing routing policy           | vpc | ModifyRoute                                         |
| Modifying route table            | vpc | ModifyRouteTableAttribute                           |
| Modifying protocol port attribute         | vpc | ModifyServiceAttribute                              |
| Modifying protocol port group attribute        | vpc | ModifyServiceGroupAttribute                         |
| Modifying subnet attribute           | vpc | ModifySubnetAttribute                               |
| Modifying traffic mirror           | vpc | ModifyTrafficMirrorAttribute                        |
| Modifying customer gateway           | vpc | ModifyUserGw                                        |
| Modifying VPC attribute          | vpc | ModifyVpcAttribute                                  |
| Modifying intra-region peering connection attribute      | vpc | ModifyVpcPeeringConnection                          |
| Modifying cross-region peering connection attribute      | vpc | ModifyVpcPeeringConnectionEx                        |
| Modifying VPN tunnel          | vpc | ModifyVpnConnEx                                     |
| Modifying VPN gateway attribute        | vpc | ModifyVpnGw                                         |
| Rejecting associating CCN instance with network instance        | vpc | RejectAttachCcnInstances                            |
| Rejecting intra-region peering connection        | vpc | RejectVpcPeeringConnection                          |
| Rejecting cross-region peering connection        | vpc | RejectVpcPeeringConnectionEx                        |
| Modifying the bandwidth of shared bandwidth package        | vpc | RemoveBandwidthPackageResources                     |
| Modifying the IDC IP range of Direct connect gateway in CCN type | vpc | ReplaceDirectConnectGatewayCcnRoutes                |
| Adjusting the concurrent connection upper limit of NAT gateway    | vpc | ResetNatGatewayConnection                           |
| Updating the target information of traffic mirror user | vpc | ResetTrafficMirrorTarget                            |
| Resetting VPN tunnel SA        | vpc | ResetVpnConnSA                                      |
| Setting the outbound bandwidth upper limit of all regions of CCN instance    | vpc | SetCcnRegionBandwidthLimits                         |
| Enabling traffic mirror           | vpc | StartTrafficMirror                                  |
| Disabling traffic mirror           | vpc | StopTrafficMirror                                   |
| Returning the private IP of ENI      | vpc | UnassignPrivateIpAddresses                          |
| Updating traffic mirror filter rule or capture object | vpc | UpdateTrafficMirrorAllFilter                        |
