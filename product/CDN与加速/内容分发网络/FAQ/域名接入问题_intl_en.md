### How to connect a domain name?
You can connect a domain name in the CDN Console. For more information, see [Connect a Domain Name](https://intl.cloud.tencent.com/document/product/228/5734).

### Does CDN support connecting wildcard domain name?
CDN supports connection to wildcard domain name but a verification is needed. Upload the verification files provided by Tencent Cloud to the root directory of the website, and establish the connection to the wildcard domain name after the verification is completed successfully.
In addition:
1. If a wildcard domain name such as \*.test.com is already connected to Tencent Cloud, then any of its sub-domain names cannot be connected to another account.
2. If the wildcard domain name \*.test.com is already connected to your account, then wildcard domain names in formats such as \*.path.test.com cannot be connected to this account.

### How long does it take to configure CDN?
Generally, it takes not more than 30 minutes for the CDN configuration to take effect. If the configuration does not take effect within 30 minutes after you configuring it, you can contact us by submitting a ticket.

### Is there any requirement for connecting a domain name to CDN?
Before a domain name is connected to CDN for acceleration, it must obtain the ICP license from the MIIT, and the business contents on the origin server must be legal.

### Can I configure multiple origin server IPs?
Yes. After you configure multiple IPs, CDN will randomly access one of the entered IPs when forwarding a request to the origin server. If the number of origin-pull failures with this IP exceeds the threshold, it will be isolated for 300 seconds by default and no longer used for origin-pull.

### How to bind CNAME to a domain name after the domain name is connected to CDN?
See CNAME Configuration for how to bind CNAME at your DNS service provider.

### Why can a domain name only be disabled but cannot be deleted?
Please check whether the user is a collaborator. The collaborator's permission is configured by the creator of the CDN service. If the creator does not assign the relevant permission to the collaborator, the collaborator cannot perform the operation. If you are sure that the user have been granted the permission, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

### Will the domain name configuration be retained after the acceleration service is disabled?
After the acceleration service is disabled, the domain name configuration is retained, but no acceleration service is provided any longer. In this case, any request from user will be forwarded to the origin server for origin-pull.

### Will the domain name configuration be retained after an accelerated domain name is deleted?
After the domain name is deleted, its configuration is not retained.

### How to disable the acceleration service?
You can disable the acceleration service in the CDN Console. For more information, see [Disable Acceleration Service](https://intl.cloud.tencent.com/document/product/228/5736).

### How to delete an accelerated domain name?
You can delete the accelerated domain name in the CDN Console. For more information, see [Deleting Accelerated Domain Name](https://intl.cloud.tencent.com/document/product/228/5736).

### How to unblock a domain name?
You need to [submit a ticket](https://console.cloud.tencent.com/workorder/category) for the help from OPS personnel.
