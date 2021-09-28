## Does CKafka support public network access?

CKafka transfers data over the private network by default. To access over the public network, you need to activate a public network route separately. For detailed directions, please see [Adding Routing Policy](https://intl.cloud.tencent.com/document/product/597/32555). Currently, a broker provides 3 Mbps public network bandwidth free of charge by default.

CKafka Pro Edition supports increasing the public network bandwidth to up to 198 Mbps for a fee. For the specific prices, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/597/11745).

As public network access runs the risk of issues such as delay and network environment security, we do not recommend long-term use of public network transfer.

## How do I continue accessing CKafka over VPC after SASL is enabled for the public network?

If you use the PLAINTEXT method to access CKafka while enabling public network access routing, the ACL previously set for the topics will still take effect. If you want PLAINTEXT access to be unaffected, please add the read/write permissions of all users for the topics that PLAINTEXT needs to access.

>?When adding an ACL policy, you don't need to select any user, and read/write permissions are added to **all users** by default.

![img](https://main.qcloudimg.com/raw/27e8e0b9b20da5f123eaee2212633dba.png)

The effect after addition is as follows:

![img](https://main.qcloudimg.com/raw/6d1b4b5dd89343530deae827e76d38ab.png)
