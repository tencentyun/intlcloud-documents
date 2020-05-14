The following concepts are essential in understanding ENIs and how to use. You should read them before using ENIs.
## Primary ENIs and Secondary ENIs
- The ENI that is automatically created when you create a CVM instance is the primary ENI.
- ENIs created by users are secondary ENIs.
- The primary ENI cannot be unbound, while secondary ENIs can.

## Primary Private IP Addresses
- The primary private IP address of an ENI can be randomly assigned by the system or defined by users when the ENI is created.
- The primary private IP address of the primary ENI can be modified, while that of a secondary ENI cannot be modified.

## Secondary Private IP Addresses
- A secondary private IP address is any private IP address other than the primary private IP address. You can configure secondary private IP addresses when you create or edit an ENI.
- A secondary private IP address can be bound and unbound.

## EIPs
EIPs are bound to the ENI private IP addresses one to one.

## Security Groups
Multiple security groups can bind to an ENI.

## MAC Addresses
An ENI has a globally unique MAC address.

