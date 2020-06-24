Before using an ENI, you need to understand the following concepts:
## Primary ENIs and Secondary ENIs
- The ENI that is automatically created when a CVM is created in a VPC instance is the primary ENI.
- ENIs created by users are secondary ENIs.
- The primary ENI cannot be unbound, while secondary ENIs can.

## Primary Private IP Addresses
When an ENI is created:
 - The primary private IP address of the primary ENI is randomly assigned, which can be modified.
 - The primary private IP address of the secondary ENI is randomly assigned or customized, which cannot be modified.

## Secondary Private IP Addresses
- A secondary private IP address is any private IP address other than the primary private IP address. You can configure secondary private IP addresses when you create or edit an ENI.
- A secondary private IP address can be bound and unbound.

## EIPs
EIPs are bound to the ENI private IP addresses one to one.

## Security Groups
An ENI can be bound with one or more security groups.

## MAC Addresses
An ENI has a globally unique MAC address.

