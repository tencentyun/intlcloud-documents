## Symptoms
After the SSL certificate is deployed on the server, using HTTPS to access pages is slow, the page is blank, or “This page can’t be reached” is displayed, as shown in the following figure:
![](https://main.qcloudimg.com/raw/0ba55ddaa87b4edb33552c25e9c81447.png)
## Possible Causes
- **Port 443 is closed on the server firewall**: If port 443 is closed, you may not be able to access pages over HTTPS normally. In this case, please open port 443 on the server and then retry.
- **Disabled security group**: A security group is a virtual firewall that features stateful data packet filtering. It is used for vendors to configure the network access control of CVM, Cloud Load Balancer, TencentDB, and other instances while controlling their outbound and inbound traffic. It is an important means of network security isolation. The security group is disabled by default. You can enable the security group on your server and then retry.
- **Browser cache pollution**: Browser cache speeds up the loading and allows you to make better use of network resources. In most cases, the browser caches recently requested resources and returns these resources when they are requested again.
- **Incorrect configuration file**: If the configuration file of the server’s web service is incorrect, requests may not be handled correctly and thus the website cannot be accessed.

## Solutions
### Opening port 443 on the server firewall[](id:openport)
- If you use Tencent Cloud’s Cloud Virtual Machine (CVM) service, you can skip this step as port 443 is open on CVM instances by default. Therefore, you can proceed with [Disabled security group](#opensecurity).
- If you use Tencent Cloud’s Lighthouse service, open port 443 by referring to Firewall Management.
- If you use cloud servers of other vendors, please contact your cloud vendor.

### Enabling a security group[](id:opensecurity)
- If you use Tencent Cloud’s CVM service, open port 443 by referring to [Adding Security Group Rules](https://intl.cloud.tencent.com/document/product/213/34272).
- Tencent Cloud’s Lighthouse service does not have this feature. Therefore, you can check [whether port 443 is opened on the firewall](#openport).
- If you use cloud servers of other vendors, please check whether your vendor supports this policy. If yes, consult your vendor about how to open port 443. If not, check [whether port 443 is opened on the firewall](#openport).

### Browser cache pollution
Clear your browser cache or try to use another browser to access the page.

### Incorrect configuration file
Check whether the configuration file is correct by referring to the corresponding deployment guide, or purchase the certificate deployment service in the Tencent Cloud Market.

>?If your SSL certificate was installed and deployed by referring to Tencent Cloud’s documentation, please see [Selecting an Installation Type for an SSL Certificate](https://intl.cloud.tencent.com/document/product/1007/30173).
