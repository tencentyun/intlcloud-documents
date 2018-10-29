## Security Group and Network
- Security group is a stateful virtual firewall for filtering packets. You can restrict access by using a firewall (security group) to allow the trusted addresses to access instances. Different security group rules for instance groups of different security levels are created to ensure that the instances running important business cannot be accessed easily from the outside. For more information, see [Security Group](/doc/product/213/5221).
- You need to regularly repair, update and protect the operating system and applications on the instance.
- With EIPs, you can quickly remap an address to another instance in your account (or NAT gateway instance) to block instance failures. For more information, see [Elastic IP](/doc/product/213/5733).
- Log in to user's Linux instances by use of [SSH Key](/doc/product/213/6092) whenever possible. For the instances that you [log in with password](/doc/product/213/6093), the password needs to be changed from time to time.
- Choose to use [Virtual Private Cloud](/doc/product/213/5227) to divide logical areas.

## Storage
- For the data that requires high reliability, use [Tencent Cloud's Cloud Block Storage](/doc/product/362) to ensure the persistent and reliable data storage. Try not to select [Local Disk](/doc/product/213/5798) for storage (Rendering GA2 only supports Cloud Block Storage).
- For databases that are frequently accessed and variable in size, use [Tencent Cloud Database](https://cloud.tencent.com/product/cdb-overview.html).
- You can use [COS](https://cloud.tencent.com/product/cos) to store important data, such as static web pages, massive images and videos.

## Backup and Recovery
- One of the recovery methods is to rollback a [Custom Image](/doc/product/213/4942) you backed up via [CVM Console](https://console.cloud.tencent.com/cvm/index).
- Deploy key components of an application across multiple availability zones, and copy the data as appropriate.
- Regularly view the monitoring data and set alarms as appropriate. For more information, see [Cloud Monitor Product Documentation](/doc/product/248).
- Process emergent requests with Auto Scaling. For more information, see [Auto Scaling Product Documentation](/doc/product/377).

