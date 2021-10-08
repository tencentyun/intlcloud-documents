This document will guide you to set a security group and allow only traffic from WAF to access websites.
## Directions
Security group is an instance-level firewall service provided by Tencent Cloud to control inbound and outbound traffic of CVM instances. You can configure a security group to allow only traffic from WAF to access your website, preventing attackers from bypassing WAF and directly attacking your real server.
The following uses allowing the WAF intermediate IP `111.230.27.90` in the security group as an example to describe how to configure the security group.
> !You can get the intermediate IP on the [Domain Name Connection](https://console.cloud.tencent.com/guanjia/instance/domain) page in the WAF console.

1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/securitygroup) and click **Security Group** on the left sidebar.
2. On the security group page, click **Create**, enter the information as required, select **Custom** as the template, enter the security group name (such as `my-security-group`) and remarks, and click **OK**.
	![](https://main.qcloudimg.com/raw/bf46812f1d687bae4a9cc2eebb597c11.png)
3. In the security group list, find the newly created security group, and click its ID to enter its details page.
4. On the inbound rule page, click **Add Rule**.
	 ![2](https://main.qcloudimg.com/raw/89645efab201d0b208aee920091b9667.png)
5. In the pop-up window, enter relevant information, select "HTTP (80)" as the type, enter the intermediate IP that needs to be allowed for the source, and enter the port and policy as required. After completing the settings, click **OK**.
	 ![3](https://main.qcloudimg.com/raw/c7e29280ba05af06e0c166121ec74492.png)
6. Click the **Associate Instance** tab and click **Add Association** on the CVM page.
	 ![4](https://main.qcloudimg.com/raw/0aa15ebd40459ea94d872ebdb6e5527f.png)
7. In the pop-up window, select the CVM instance to be bound to and click **OK**.
	 ![](https://main.qcloudimg.com/raw/f2cdbcf796282302b5dfa3f3ad836d5c.png)
   Alternatively, you can go to the [CVM instance list page](https://console.cloud.tencent.com/cvm) to view or modify the security group bound to a CVM instance. On the list page, select the ID of the CVM instance whose security group you want to adjust and click **More** -> **Security Group** -> **Configure Security Group** in the **Operation** column on the right for configuration.
![](https://main.qcloudimg.com/raw/5b675850fc547864760ef37ab2875f82.png)