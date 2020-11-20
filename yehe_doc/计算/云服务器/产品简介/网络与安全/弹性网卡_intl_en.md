[Elastic Network Interface (ENI)](https://intl.cloud.tencent.com/product/eni?from_cn_redirect=1) is an elastic interface for network access that binds Cloud Virtual Machine (CVM) servers on a Virtual Private Cloud (VPC) for seamless migration among multiple CVM servers. Multiple ENIs can be bound to one CVM server to create a highly available network. 

An ENI is part of a subnet, which is part of a VPC, which in turn is part of an availability zone. An ENI can only be associated with a CVM instance in the same availability zone. Multiple ENIs can be associated with the same CVM instance. The specific number depends on the specification of the CVM.

## Concepts

 - **Primary ENI and secondary ENI**: when you create a CVM instance, an ENI is automatically created in the process. That is the primary ENI. Any subsequent ENIs you create are secondary ENIs. You cannot bind or unbind a primary ENI. Secondary ENIs support binding and unbinding.
 - :**Primary private IP:** the primary private IP of an ENI is assigned by the system or specified by the user when the ENI is created. You can modify the primary private IP of the primary ENI, but not those of secondary ENIs.
  **Secondary private IP:** other than the primary private IP, all IP addresses bound to the ENI are secondary private IPs. You can bind/unbind these IPs.
 - **EIP**: EIPs are mapped one-to-one to the private IPs of an ENI.
 - **Security group**: an ENI can be associated with one or more security groups.
 - **MAC address**: each ENI has a globally unique MAC address.

## Use Cases
- **Isolation among private network, public network, and management network**:
Critical business often requires different routing policies and security groups for private networks, public networks, and management to ensure data security and network isolation. You can use CVM to achieve the same level of isolation as different physical servers. Simply assign different ENIs to different subnets.
**Highly reliable application deployment:**
Critical system components require multiple hot backups to ensure high availability. The flexible binding and unbinding of ENIs and private IPs is the foundation of Tencent Cloud’s high availability architecture. Use Keepalived to implement this feature.

## Use Limits

The number of ENIs a CVM instance can be associated with and the number of private IPs an ENI can be associated with depend on the CPU and memory configurations. They are shown in the following table:
> The number of IP addresses bound to a single ENI only represents the upper limit of IP addresses that ENIs can be bound to, not the available EIP quota. For the EIP quota of your account, please refer to EIP [use limits](https://intl.cloud.tencent.com/document/product/213/5733).

| CVM specification | Number of ENIs | Number of private IPs |
| ------------------- | :---- | :------ |
| CPU: 1 core </br>Memory: 1 GB | 2 | 2 |
| CPU: 1 core </br>Memory: > 1 GB | 2 | 6 |
| CPU: 2 cores | 2 | 10 |
| CPU: 4 cores </br>Memory: < 16 GB | 4 | 10 |
| CPU: 4 cores </br>Memory: > 16 GB | 4 | 20 |
| CPU: 8 - 12 cores | 6 | 20 |
| CPU: > 12 cores | 8 | 30 |


## API Overview
The following is a list of APIs related to ENI and CVM. For more information, refer to [Overview of ENI APIs](https://intl.cloud.tencent.com/document/product/215/15755?from_cn_redirect=1#.E5.BC.B9.E6.80.A7.E7.BD.91.E5.8D.A1.E7.9B.B8.E5.85.B3.E6.8E.A5.E5.8F.A3).

| Feature | Action ID | Description |
|---------|---------|---------|
| Create ENI | [CreateNetworkInterface](https://intl.cloud.tencent.com/document/api/215/15818?from_cn_redirect=1) | Creates an ENI |
| Apply for private IPs | [AssignPrivateIpAddresses](https://intl.cloud.tencent.com/document/api/215/15813?from_cn_redirect=1) | Applies for private IPs for an ENI |
| Bind an ENI to a CVM instance | [AttachNetworkInterface](https://intl.cloud.tencent.com/document/api/215/15819?from_cn_redirect=1) | Binds an ENI to a CVM instance |
