This document will guide you to set a security group and allow only traffic from WAF to access websites.

## Directions
Security group is an instance-level firewall service provided by Tencent Cloud to control inbound and outbound traffic of CVM instances. You can configure a security group to allow only traffic from WAF to access your website, preventing attackers from bypassing WAF and directly attacking your origin server.
The following uses allowing the WAF intermediate IP `111.230.27.90` in the security group as an example to describe how to configure the security group.
>! The intermediate IP can be viewed at [Domain Name List](https://console.cloud.tencent.com/guanjia/instance/domain) in the WAF console.

1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/securitygroup) and click **Security Group** on the left sidebar.
2. Click **Create**. On the pop-page, select **Custom** for the template, enter the security group name (such as `my-security-group`) and remarks, and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/e9a229b026da2233859215b1291018f6.png)
3. In the security group list, find the newly created security group, and click its ID to enter its details page.
4. On the inbound rule page, click **Add rule**.
![2](https://qcloudimg.tencent-cloud.cn/raw/20c1e5ffd0d4d460c3e9a2f66778b254.png)
5. In the pop-up window, select "HTTP (80)" as the type, enter the intermediate IP that needs to be allowed for the source, and enter the port and policy as required. After completing the settings, click **OK**.
![3](https://qcloudimg.tencent-cloud.cn/raw/7a475e72f0f594a6b96b659c805b2cb8.png)
6. Click the **Associate Instance** tab and click **Add Instance** on the CVM page.
![4](https://qcloudimg.tencent-cloud.cn/raw/1870a93c8c42e304ac9c60da1a29de23.png)
7. In the pop-up window, select the CVM instance to be bound to and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/b5a07268d014454810c745f93607f526.png)

Alternatively, you can go to the [CVM instance list page](https://console.cloud.tencent.com/cvm) to view or modify the security group bound to a CVM instance. On the list page, select the ID of the CVM instance whose security group you want to adjust and click **More** > **Security Groups** > **Configure Security Groups** in the **Operation** column on the right for configuration.
![](https://qcloudimg.tencent-cloud.cn/raw/4d34211ee96ea16e0932983434e542e8.png)



