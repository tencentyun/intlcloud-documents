## Overview
An Elastic Network Interface (ENI) is used to bind CVMs within a VPC instance, and can be freely migrated among CVMs. ENIs can help configure and manage network, as well as develop highly reliable network solutions. You can bind multiple ENIs under the same availability zone in the same VPC to a CVM to set up a high-availability network solution. You can also bind multiple private IPs on an ENI to deploy multiple IPs on a single CVM.

## Features
### Multiple ENIs
A primary ENI will be automatically generated for a created CVM. In addition, you can bind multiple secondary ENIs to the CVM. These ENIs can belong to different subnets in the same VPC instance and availability zone. You can configure a separate security group for each ENI and configure an individual route forwarding policy for the subnet where each ENI resides.

### Flexible migration
ENIs can be freely migrated between CVMs in the same VPC instance and availability zone. When an ENI is unbound from a CVM, the private IP, the EIP, and the security group policy are retained so that you do not need to configure the association again after migration.

### Multiple IPs
Based on the configuration of a CVM, up to 30 private IPs can be bound to an ENI, and each private IP can be bound to an independent EIP. A single CVM can open multiple ports of the same type by using multiple EIPs. The binding relationships among ENIs, private IPs, and public IPs are retained when the ENIs are unbound from CVMs.

### Independent route forwarding
A CVM can be bound to ENIs of different subnets in the same VPC instance and availability zone. You can configure route forwarding policies for each subnet to isolate networks. You can also set route policies in a CVM instance to direct network traffic with a specific destination to different ENIs.

#### Setting of multiple service levels
You can set different service levels for ENIs. When bandwidth congestion occurs, this can ensure that the key services with high priority be forwarded first. Currently, four levels are supported, including Gold, Silver, Bronze and Default. The priority for traffic forwarding is Gold > Silver > Bronze > Default. Unless otherwise stated, select "Default".

### Flow logs
After a flow log is created for an ENI, the log stream of the ENI will be automatically collected and the log data will be synced to CLS. In the CLS topic, each ENI has a unique log stream, which contains flow log records. Only one flow log can be created for an ENI. For more information, see [Creating a Flow Log for an ENI]().
