
## Error Description
After the SSL certificate is successfully deployed on a cloud VM, you cannot open the website by entering "https://domain name".

## Possible Causes
- Cause 1: Port 443 is disabled.
- Cause 2: The configuration file is incorrect.

## Solutions
#### Disabled port 443
Enable port 443 on the server where the SSL certificate is installed. Besides, add port 443 to the security group so that HTTPS can be used after the installation.
- For Tencent Cloud CVMs, see [Adding Security Group Rules](https://intl.cloud.tencent.com/document/product/213/34272).
- For other cloud providers’ VMs, see the corresponding cloud provider’s documentation.

#### Incorrect configuration file
Check whether the configuration file is correct.
>?If your SSL certificate was installed and deployed by referring to Tencent Cloud’s documentation, please see [Selecting an Installation Type for an SSL Certificate](https://intl.cloud.tencent.com/document/product/1007/30173).


