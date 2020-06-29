### In what scenarios do I need to add security group rules?
To ensure the accessibility of CVM instances, you need to add security group rules in the following scenarios:
- There is no security group rule (added or default) for CVM instances. If your CVM instances need to access the public network or communicate with CVM instances associated to other security groups in the same region, you need to add security rules.
- The application you built uses a custom port or port range, instead of the default port. In this case, you need to open the custom port or port range before testing the application connectivity. For example, if you set up an Nginx service on your CVM instances that listens on the TCP 1800 communication port but your security group only opens port 80, you need to add security group rules to ensure the accessibility of the Nginx service.
- For other scenarios, see [Security Group Use Cases](https://intl.cloud.tencent.com/document/product/213/32369).

### What impact will incorrectly configuring security group rules have?
If any security group rule is configured incorrectly, CVM instances will fail to access other devices over the private network or public network. For example:
- You may fail to remotely connect to a Linux instance over SSH or a Windows instance via remote desktop.
- You may fail to remotely ping the public IP of a CVM instance.
- You may fail to access Web services provided by CVM instances over the HTTP or HTTPS protocol.
- You may fail to access other CVM instances over the private network.


### Are the inbound rules and outbound rules of a security group counted separately?
A maximum of 100 inbound and 100 outbound rules can be set for a security group.


### Can I adjust the maximum number of security group rules allowed?
Each security group can configure up to 200 security group rules, including 100 inbound rules and 100 outbound rules. One CVM instance can be associated with up to 5 security groups and can therefore adopt up to 1,000 security group rules, which is enough to meet the needs of most scenarios.
If your usage surpasses this upper limit, check whether redundant rules exist.
- If so, remove them.
- If not, create more security groups.

In addition, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&step=1) to raise the upper limit of security group rules.
