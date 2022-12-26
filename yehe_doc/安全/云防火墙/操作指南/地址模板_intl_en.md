This topic describes how to batch manage IP addresses in an address template and match the created templates with access control rules.

## Operation guide

1. Log in to the [Cloud Firewall console](https://console.cloud.tencent.com/cfw/asset), and then click **Address template** in the left navigation pane.
2. On the **Address template** page, you can create and modify templates, and call templates to add rules on the **Access Control** page.
 - [**Create template**](id:new)
   1. On the **Address template** page, click **Create template**.
   2. In the **Create address template** window displayed, enter the address template name and IP address, and then click **OK** to complete the template creation.
>?
>- For a single IP address, Press Enter.
>- For multiple IP addresses, separate them with commas before pasting.
>- Duplicate IP addresses are merged automatically.

<img src="https://qcloudimg.tencent-cloud.cn/raw/f1048582b65a2992e641c2c3c6d6f3ed.png" style="zoom:85%;" />

 - **Modify template**
 After [a template is created](#new), it will be displayed in the address template list, and you can add, delete, or modify IP addresses in the list.
	1. In the action column on the right of the destination address template, click **Modify**.
	2. Select the IP address to modify or delete in the **Modify address template** window displayed, or enter the IP address in the search box, and then click **OK** to complete the modification.
<img src="https://qcloudimg.tencent-cloud.cn/raw/d79394d34116f87d701a221024db8d60.png" style="zoom:80%;" />
- [**Import an address template for configuring rules**](id:IP)
After [creating an address template](#new), you can go to the [Edge firewall rules](https://console.cloud.tencent.com/cfw/ac/internet) or [NAT firewall rules](https://console.cloud.tencent.com/cfw/ac/nat) page to call the template for configuring access control rules. The following example shows how to import an address template for configuring edge firewall rules. This also applies to NAT firewall rules.
>?
>- The access rules configured with the address template are valid for all IP addresses in the template.
>- Address templates can only be used to configure edge firewall rules and NAT firewall rules, rather than inter-VPC firewall rules.
>- **Inbound rules** only allow importing address templates for **Access source**, while **Outbound rules** only allow importing templates for **Access destination**.

   - **Import an address template for inbound rules**
		1. On the [Edge firewall rules](https://console.cloud.tencent.com/cfw/ac/internet) page, select **Inbound rules** -> **Add rule**.
		2. In the "Add inbound rule" window displayed, select "Address template" for "Access destination type", and click the "Access source" drop-down list to select an existing address template for configuring rules. 
![](https://qcloudimg.tencent-cloud.cn/raw/d270e51ad25b72ae863f2d583a439ff2.png)
 - **Import an address template for outbound rules**
		1. On the [Edge firewall rules](https://console.cloud.tencent.com/cfw/ac/internet) page, select **Outbound rules** -> **Add rule**.
		2. In the "Add outbound rule" window displayed, select "Address template" for "Access destination type", and click the "Access destination" drop-down list to select an existing address template for configuring rules.
![](https://qcloudimg.tencent-cloud.cn/raw/9eafcac1eec9a8ebb067cb7192adf2eb.png)
