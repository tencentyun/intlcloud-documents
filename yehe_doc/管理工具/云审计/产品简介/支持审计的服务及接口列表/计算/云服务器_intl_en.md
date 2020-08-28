Tencent Cloud Virtual Machine (CVM) provides secure and reliable elastic computing services. Within just a few minutes, you can get and activate your CVM instances in Tencent Cloud to implement your computing needs. As your business needs change, you can add or remove computing resources in real time. CVM is pay-as-you-go, saving your computing costs. With CVM, you can greatly reduce your software and hardware purchase costs and simplify IT OPS.

CVM operations supported by CloudAudit are as shown below:

| Operation Name | Resource Type | Event Name |
|------------------------------|------|------------------------------------------|
| Changing public IP                       | cvm  | AdjustPublicAddress                      |
| Applying for EIP v3                      | cvm  | AllocateAddresses                        |
| Creating CDH instance                      | cvm  | AllocateHosts                            |
| Rolling back CBS snapshot                      | cvm  | ApplySnapshot                            |
| Binding EIP v3                      | cvm  | AssociateAddress                         |
| Binding key v3                       | cvm  | AssociateInstancesKeyPairs               |
| Associating instance with security group v3                    | cvm  | AssociateSecurityGroups                  |
| Mounting cloud disk                         | cvm  | AttachCbsStorages                        |
| Binding automatic snapshot policy                     | cvm  | BindAutoSnapshotPolicy                   |
| Cold-Migrating service to instance                      | cvm  | ColdMigrateInstance                      |
| Creating automatic snapshot policy                     | cvm  | CreateAutoSnapshotPolicy                 |
| Purchasing cloud disk                         | cvm  | CreateCbsStorages                        |
| Creating image v3                       | cvm  | CreateImage                              |
| Creating key v3                       | cvm  | CreateKeyPair                            |
| Creating security group                        | cvm  | CreateSecurityGroup                      |
| Creating security group rule                      | cvm  | CreateSecurityGroupPolicy                |
| Creating CBS snapshot                      | cvm  | CreateSnapshot                           |
| Deleting automatic snapshot policy                     | cvm  | DeleteAutoSnapshotPolicies               |
| Deleting the security configuration of user cloud disk                   | cvm  | DeleteDiskSecurityConfigurations         |
| Deleting image v3                       | cvm  | DeleteImages                             |
| Deleting key v3                       | cvm  | DeleteKeyPairs                           |
| Deleting security group                        | cvm  | DeleteSecurityGroup                      |
| Deleting security group rule                      | cvm  | DeleteSecurityGroupPolicy                |
| Deleting CBS snapshot                      | cvm  | DeleteSnapshot                           |
| Querying EIP v3                      | cvm  | DescribeAddresses                        |
| Querying block storage                        | cvm  | DescribeAllBlockStorages                 |
| Viewing automatic snapshot policy                     | cvm  | DescribeAutoSnapshotPolicies             |
| Querying bound automatic snapshot policy                  | cvm  | DescribeCbsAssociatedAsp                 |
| Querying cloud disk                         | cvm  | DescribeCbsStorages                      |
| Querying the security configuration of user cloud disk                   | cvm  | DescribeDiskSecurityConfigurations       |
| Querying independent host v3                     | cvm  | DescribeHosts                            |
| Querying image v3                       | cvm  | DescribeImages                           |
| Querying image sharing v3                     | cvm  | DescribeImageSharePermission             |
| Querying instance bandwidth configuration                     | cvm  | DescribeInstanceInternetBandwidthConfigs |
| Querying instance attribute                       | cvm  | DescribeInstancesAttribute               |
| Viewing the number of cloud disks that can be mounted to CVM instance                 | cvm  | DescribeInstancesCbsNum                  |
| Viewing the list of instance operation limits                   | cvm  | DescribeInstancesDeniedActions           |
| Querying whether the server can be returned                     | cvm  | DescribeInstancesReturnable              |
| Querying instance status v3                     | cvm  | DescribeInstancesStatus                  |
| Querying the URL of instance management client                   | cvm  | DescribeInstanceVncUrl                   |
| Querying key list v3                     | cvm  | DescribeKeyPairs                         |
| Querying the number of resources bound to security group                   | cvm  | DescribeSecurityGroupAssociateInstances  |
| Querying security group list                      | cvm  | DescribeSecurityGroupEx                  |
| Querying security group quota                    | cvm  | DescribeSecurityGroupLimits              |
| Querying security group rule                      | cvm  | DescribeSecurityGroupPolicy              |
| DescribeSecurityGroupPolicys | cvm  | DescribeSecurityGroupPolicys             |
| Querying security group                        | cvm  | DescribeSecurityGroups                   |
| Querying CBS snapshot                      | cvm  | DescribeSnapshots                        |
| Unmounting cloud disk                         | cvm  | DetachCbsStorages                        |
| Unbinding EIP v3                      | cvm  | DisassociateAddress                      |
| Unbinding key v3                       | cvm  | DisassociateInstancesKeyPairs            |
| Dissociating instance form security group v3                   | cvm  | DisassociateSecurityGroups               |
| Entering rescue mode                         | cvm  | EnterRescueMode                          |
| Exiting the hot migration of service                      | cvm  | ExitLiveMigrateInstance                  |
| Exiting rescue mode                       | cvm  | ExitRescueMode                           |
| Migrating service to data disk                      | cvm  | ImportCbs                                |
| Importing key v3                       | cvm  | ImportKeyPair                            |
| Querying CBS snapshot price                    | cvm  | InquirySnapshotPrice                     |
| Querying cloud disk price                       | cvm  | InquiryStoragePrice                      |
| Hot-Migrating service to instance                      | cvm  | LiveMigrateInstance                      |
| Modifying EIPv3                      | cvm  | ModifyAddressAttribute                   |
| Adjusting EIP bandwidth v3                    | cvm  | ModifyAddressesBandwidth                 |
| Modifying automatic snapshot policy                     | cvm  | ModifyAutoSnapshotPolicy                 |
| Setting auto-renewal flag for CBS instance                  | cvm  | ModifyCbsRenewFlag                       |
| Modifying cloud disk attribute                       | cvm  | ModifyCbsStorageAttributes               |
| Modifying the security configuration of user cloud disk                   | cvm  | ModifyDiskSecurityConfigurations         |
| Modifying CDH instance attribute                   | cvm  | ModifyHostsAttribute                     |
| Modifying image v3                       | cvm  | ModifyImageAttribute                     |
| Setting image sharing v3                     | cvm  | ModifyImageSharePermission               |
| Switching network billing mode                     | cvm  | ModifyInstanceInternetChargeType         |
| Modifying instance attribute                       | cvm  | ModifyInstancesAttribute                 |
| Modifying instance project                       | cvm  | ModifyInstancesProject                   |
| Modifying instance renewal flag                     | cvm  | ModifyInstancesRenewFlag                 |
| Modifying key v3                       | cvm  | ModifyKeyPairAttribute                   |
| Modifying security group attribute                      | cvm  | ModifySecurityGroupAttributes            |
| Modifying security group rules                      | cvm  | ModifySecurityGroupPolicys               |
| Modifying security group rule                    | cvm  | ModifySingleSecurityGroupPolicy          |
| Modifying CBS snapshot attribute                    | cvm  | ModifySnapshot                           |
| Terminating CVM instance v3                      | cvm  | PurgeInstances                           |
| Restarting CVM instance v3                      | cvm  | RebootInstances                          |
| Releasing EIP v3                      | cvm  | ReleaseAddresses                         |
| Renewing cloud disk                         | cvm  | RenewCbsStorage                          |
| Renewing CDH instance                      | cvm  | RenewHosts                               |
| Renewing CVM instance                        | cvm  | RenewInstances                           |
| Reinstalling CVM instance v3                      | cvm  | ResetInstance                            |
| Adjusting the bandwidth upper limit of instance v3                   | cvm  | ResetInstancesInternetMaxBandwidth       |
| Modifying instance password v3                     | cvm  | ResetInstancesPassword                   |
| Adjusting CVM instance configuration v3                     | cvm  | ResetInstancesType                       |
| Expanding cloud disk capacity                         | cvm  | ResizeCbsStorage                         |
| Expanding the data disk capacity of CVM instance v3                    | cvm  | ResizeInstanceDisks                      |
| Creating CVM instance v3                      | cvm  | RunInstances                             |
| Starting CVM instance v3                      | cvm  | StartInstances                           |
| Disabling CVM instance v3                      | cvm  | StopInstances                            |
| Syncing image v3                       | cvm  | SyncImages                               |
| Terminating CBS instance                        | cvm  | TerminateCbsStorages                     |
| Deleting CVM instance v3                      | cvm  | TerminateInstances                       |
| Unbinding automatic snapshot policy                     | cvm  | UnbindAutoSnapshotPolicy                 |
