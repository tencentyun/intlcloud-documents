Security group, an instance-level firewall provided by Tencent Cloud, is used to control inbound/outbound traffic of CVMs.

 1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index), and click **Security Group** in the left navigation pane.
 2. Click the **New** button, enter the security group name (e.g. my-security-group), select **Template** or **Custom**, and then click **OK** after confirming inbound and outbound rules.
 3. Click the **Add an Instance** button on the right of the security group list, and select the CVM to be associated with the security group to complete the process. 

**Or**

You can also enter the CVM list page to view or modify the security group associated with a CVM. On the **CVM** list page, select the CVM for which you want to modify the security group, and click **More** -> **Configure Security Group** on the right side, and then select a security group for association.
(For example, to allow your local computer (IP: 123.45.6.7) to send HTTP requests to the CVM, you can create a rule as shown in the figure below.)
![image-20181010152604227](https://main.qcloudimg.com/raw/c08ca9a0262f4911fdac90925762e4a6.png)
