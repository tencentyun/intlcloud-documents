### How Do I Ensure the Security of CVMs in VPC Instances?
The VPC itself is a logically isolated network environment, and traffic can be controlled by configuring security groups and network ACLs:
- Security group: provides network traffic control for CVMs at the instance level. Traffic that is disallowed to flow in or out of the instance is automatically rejected.
- [Network ACL](https://intl.cloud.tencent.com/document/product/215/31850): provides subnet-level network traffic control.
