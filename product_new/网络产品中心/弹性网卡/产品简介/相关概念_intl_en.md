Before using an ENI, you need to understand the following concepts:
## Primary ENIs and Secondary ENIs
- The ENI that is automatically created when a CVM is created in a VPC instance is the primary ENI. ENIs created by users are secondary ENIs.
- The primary ENI cannot be unbound, while secondary ENIs can.

## Primary Private IP Addresses
- The primary private IP address of an ENI can be randomly assigned by the system or defined by users when the ENI is created.
- The primary private IP address of the primary ENI can be changed, while that of an secondary ENI cannot be changed.

## Secondary Private IP Addresses
- A secondary private IP address that is bound to an ENI can be configured by users when the ENI is created or edited.
- A secondary private IP address can be bound and unbound.

## EIPs
EIPs are bound with the private IP addresses of an ENI in one-to-one fashion.

### Security Groups
An ENI can be bound with one or more security groups.

## MAC Addresses
An ENI has a globally unique MAC address.

