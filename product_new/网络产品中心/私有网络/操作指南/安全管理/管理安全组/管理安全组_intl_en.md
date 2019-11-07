### Scenario

When initially configuring a CVM, you can configure the security group, and you can also create, view, update, and delete security groups in the console’s security group page, where you can also manage security groups and security group rules. This document describes how to use all security group features in the console.

##  Prerequisites

Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).

## Steps

### Creating a Security Group
> When creating a security group, you can create it by choosing from two templates provided by Tencent Cloud, which are **Open all ports** and **Open ports 22, 80, 443, and 3389 and ICMP protocol to Internet**. You can also create the security group using a custom template.
>
#### Creating Using Tencent Cloud Template
1. In the left sidebar, select **[Security Group](https://console.cloud.tencent.com/cvm/securitygroup)**, and click **+New**.
![](https://main.qcloudimg.com/raw/a9d8baf34b10ae536c35d3286edc22c5.png)
2. In the **New Security Group** pop-up window, select either the **Open all ports** template or the **Open ports 22, 80, 443, and 3389 and ICMP protocol to Internet** template as needed. Enter the security group’s name and configure its settings.
![](https://main.qcloudimg.com/raw/7fece2b00807c7266368aeb5af6f398e.png)
3. Click **OK** to finish the creation process.

#### Creating Using Custom Template
1. In the left sidebar, select **[Security Group](https://console.cloud.tencent.com/cvm/securitygroup)**, and click **+New**.
![](https://main.qcloudimg.com/raw/cebfc052b3ba2f6dffd2a7d5e9eb0672.png)
2. In the **New Security Group** pop-up window, select **Custom** template. Enter the security group’s name and configure its settings. Click **OK**.
![](https://main.qcloudimg.com/raw/4411a21c9ca5df7a17983df1730af78c.png)
3. In the pop-up prompt, click **Set Rules Now**. For details on how to set the rules, see the following document on adding security group rules.
![](https://main.qcloudimg.com/raw/5f98fb929fdbf6fac7928515519b5c82.png)

### Adding a Security Group Rule
1. On the **Security Group Rules** page, click **Add Rule** under **Inbound Rule** or **Outbound Rule** tab as needed.
![](https://main.qcloudimg.com/raw/45e094d4481fcdaaec06213a60f22aeb.png)
2. Configure the rule settings in the **Add Inbound/Outbound Rule** pop-up window, and click **Finish**.
The main parameters required when adding a rule are as follows:
 - **Type**: You can select a system rule template or create a custom rule.
 - **Source/destination**: Traffic source (inbound rules) or destination (outbound rules). Choose one of the following options:
    - Specified individual IP address or IP address range: Indicate using CIDR (for example: `203.0.113.0` or `203.0.113.0/24`).
    - Reference a security group ID. You can reference one of the following security group IDs:
      - Current security group. (Indicates the CVM associated with the security group)
      - Other security group. The ID of another security group under the same project in the same region.
    - Reference an IP address object or an IP address group object in the [Parameter Template](https://cloud.tencent.com/document/product/215/20090). 
 - **Protocol port**: Enter the protocol type and port range, or reference a protocol port or protocol port group in the [Parameter Template](https://cloud.tencent.com/document/product/215/20090).
 - **Policy**: Allow or Reject.

>
>  - Referencing a security group ID is an advanced feature. The rules of the referenced security groups are not added to the current security group.
>  - If you enter the security group ID in Source/Destination when configuring security group rules, the private IP addresses of the CVM instances and the ENIs that are bound with this security group ID are used as Source/Destination. This does not include public IP addresses.

### Modifying a Security Group Rule
> You can modify previously set security group rules based on your actual needs
>
1. Go to the **[Security Group](https://console.cloud.tencent.com/cvm/securitygroup)** management page and select the name/ID of the security group for which rules need to be modified, and click **Modify Rule** on the right side.
![](https://main.qcloudimg.com/raw/d37c7ee3419bd7d3f7a14dabe16fc8b9.png)
2. On the “Security Group Rule” page that needs to be modified, you can **Edit** or **Delete** the rule or adjust the rule’s priority by using **Insert** as required. On the security group rule priority list, **the higher the position, the higher the priority**.
![](https://main.qcloudimg.com/raw/7d13ff994cd11c188f07914cc0614f55.png)

### Associating an Instance to a Security Group

1. Go to the **[Security Group](https://console.cloud.tencent.com/cvm/securitygroup)** management page and select the security group that needs to be associated. Click **Manage Instance** to go to the **Bind with Instance** page.
![](https://main.qcloudimg.com/raw/d258b1dcff6c53de504a311f5e346dad.png)
2. On the **Bind with Instance** page, click **Add Instances**.
![](https://main.qcloudimg.com/raw/5cfc487dfe65acecd4eb3397aaab22ed.png)
3. In the **Add Instances** pop-up window, select one or more instances that need to be associated to this security group and click **OK** to associate the instance or instances to this security group.
![](https://main.qcloudimg.com/raw/906de652155a8cbf27009a2abdb6f9fb.png)

### Cloning or Deleting a Security Group

Go to the **[Security Group](https://console.cloud.tencent.com/cvm/securitygroup)** management page and select the security group that needs to be cloned or deleted. Click **More** and then select **Clone** or **Delete**.
![](https://main.qcloudimg.com/raw/1983012e687057111f40af7e049ae04e.png)
- When you select to **clone** security group, only the security group’s inbound/outbound rules will be cloned, and the security group’s associated instances will not be cloned.
- To **delete** a security group, please make sure it is not associated with instances. If there is an associate instance, please click **Manage Instance** -> **Remove from the security group**. Otherwise, the security group cannot be deleted.
![](https://main.qcloudimg.com/raw/fa359091c7eed2b19bfbb3d025137b6b.png)

### Importing/Exporting Security Group Rules

1. Go to the **[Security Group](https://console.cloud.tencent.com/cvm/securitygroup)** management page and locate the desired security group. Click **Modify Rules** to go to the management page for this security group.
![](https://main.qcloudimg.com/raw/3141fc7e8b6d0f36a149e3e097df1c17.png)
2. Select the **Security Group Rules** > **Inbound Rules** or **Outbound Rules** tab and click **Import Rules**.
> 
> - If a rule already exists, then we recommend that you export this existing rule first. Otherwise, the existing rule will be overwritten when importing the new rule.
> - If no rule exists, then you can first export a template and then import the template file after editing it.
> 
![](https://main.qcloudimg.com/raw/961f55dfc583f1a7896d392123ef9cdc.png)
3. In the “**Batch Import-Inbound/Outbound Rules**” pop-up window, select the edited template file for the inbound/outbound rules and click **Import**.

### Using the Security Group API

In addition to using the CVM console, you can also perform operations for security groups using the security group APIs. For details, refer to [Security Group API](https://cloud.tencent.com/document/product/213/12447).
