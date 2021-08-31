### Do you have any advice regarding OPS for small websites hosted on CVM?
To maintain the website applications, you can:
- Back up data to the cloud disk daily. For more information, see [Creating Snapshots](https://intl.cloud.tencent.com/document/product/362/5755).
- Use [SSL Certificates Service](https://intl.cloud.tencent.com/document/product/1007/30152) for identity verification and encrypted connections. 
- Install anti-virus plugins or anti-DDoS services or purchase Cloud Workload Protection.
- Monitor the traffic to and from the website and identify exceptions in the traffic range. Add the security group rules of denied access to temporarily control the exception request of a single point. For more information, see [Getting Monitoring Statistics](https://intl.cloud.tencent.com/document/product/213/5178) and [Adding Security Group Rules](https://intl.cloud.tencent.com/document/product/213/34272).
- Monitor the performance of CVM instances and the cloud disk, and mark the traffic/access peak period. Familiarize yourself in advance with upgrade/degrade, auto scaling, or cloud disk expansion to respond to request surges. For more information, see [Change Instance Configuration](https://intl.cloud.tencent.com/document/product/213/2178), [What is Auto Scaling (AS)?](https://intl.cloud.tencent.com/document/product/377/3154), or [Cloud Disk Expansion Scenarios](https://intl.cloud.tencent.com/document/product/362/31600).
- Update the admin password regularly for scenarios where you log in to CVM instances with the root/Administrator username and password. For more information, see [Reset Instance Password](https://intl.cloud.tencent.com/document/product/213/16566).
- Update the software patches regularly.

