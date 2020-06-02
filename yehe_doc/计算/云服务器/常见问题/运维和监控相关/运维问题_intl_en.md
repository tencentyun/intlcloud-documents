### Could you give some OPS advices on a CVM hosting small websites?
To maintain the website applications, you can:
- Back up data in the cloud disk daily. For more information, see [Creating Snapshots](https://intl.cloud.tencent.com/document/product/362/5755).
- Complete the identity verification and encrypted data transfer of the websites using SSL Certificate Service. For more information, see [SSL Certificates](https://intl.cloud.tencent.com/document/product/1007/30152).
- Install malware removal plugins or Anti-DDoS, or purchase Cloud Workload Protection.
- Monitor the traffic to and from the website, and recognize the abnormal traffic range. Add the security group rules of denied access to temporarily control the abnormal request of a single point. For more information, see [Getting Monitoring Statistics](https://intl.cloud.tencent.com/document/product/213/5178) and [Adding Security Group Rules](https://intl.cloud.tencent.com/document/product/213/34272).
- Monitor the performance of CVM instances and cloud disk, and mark the traffic/access peak period. Know well about the upgrade/degrade, auto scaling or cloud disk expansion in advance to respond to request surges. For more information, see [Changing Instance Configuration](https://intl.cloud.tencent.com/document/product/213/2178), [What is Auto Scaling (AS)](https://intl.cloud.tencent.com/document/product/377/3154) or [Cloud Disk Expansion Scenarios](https://intl.cloud.tencent.com/document/product/362/31600).
- Update Admin password regularly for scenarios where you log in to CVM instances with credentials of username such as root/Administrator and password. For more information, see [Resetting Instance Password](https://intl.cloud.tencent.com/document/product/213/16566).
- Update software patches regularly.

