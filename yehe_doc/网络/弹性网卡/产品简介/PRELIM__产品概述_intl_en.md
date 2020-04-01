## Introduction
An Elastic Network Interface (ENI) is used to bind CVM within a VPC instance, and can be freely migrated among CVMs. ENIs can help configure and manage, as well as develop highly reliable network solutions. You can bind multiple ENIs in the same availability zone to a CVM to set up a high-availability network solution. You can also bind multiple private IP addresses on an ENI to deploy multiple IP addresses on a single CVM.

## Features
### Multiple ENIs
A primary ENI will be automatically generated for a created CVM. In addition, you can bind multiple secondary ENIs to the CVM. These ENIs can belong to different subnets in the same VPC instance and availability zone. You can configure a separate security group for each ENI and configure an individual route forwarding policy for the subnet where each ENI resides.

### Flexible Migration
ENIs can be freely migrated between CVMs in the same VPC instance and availability zone. When an ENI is unbound from a CVM, the private IP address, the EIP, and the security group policy are retained so that you do not need to configure the association again after migration.

### Multiple IP Addresses
Based on the configuration of a CVM, up to 30 private IP addresses can be bound to an ENI, and each private IP address can be bound to an independent EIP. A single CVM can open multiple ports of the same type by using multiple EIPs. The binding relationships among ENIs, private IP addresses, and public IP addresses are retained when the ENIs are unbound from CVMs.

### Independent Route Forwarding
A CVM can be bound to ENIs of different subnets in the same VPC instance and availability zone. You can configure route forwarding policies for each subnet to isolate networks. You can also set route policies in a CVM instance to direct network traffic with a specific destination to different ENIs.

