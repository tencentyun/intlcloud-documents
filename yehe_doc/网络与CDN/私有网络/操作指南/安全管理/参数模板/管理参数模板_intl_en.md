This document describes how to create and maintain parameter templates (IP address, IP address group, protocol port, and protocol port group) in the console and how to use them in security groups.


## Creating a Parameter Template

### Creating an IP Parameter Template
Add the IPs with the same usage or need to be edited frequently to the template.

#### Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Click **Security** > **Parameter Template** on the left sidebar to access the management page.
3. Select the **IP Address** tab and click **+ New**.
4. In the pop-up window, enter the name and IP addresses and click **Submit**.
 You can add multiple IPs in the following ranges and separate them by line breaks:
 + Single IP: Such as “10.0.0.1” or “FF05::B5”
 + CIDR block: Such as “10.0.1.0/24” or “FF05:B5::/60” 
 - Consecutive IPs: Such as `10.0.0.1`-`10.0.0.100`;
![](https://main.qcloudimg.com/raw/64ecfd48ffdc728506ef328a0ee19921.png)

### Creating an IP Group Template
You can add multiple addresses to an IP group for easy management.

#### Directions
1. Select the **IP Address Group** tab and click **+ New**.
	![](https://qcloudimg.tencent-cloud.cn/raw/333211f6e4bb94b7611cb6d4bb327c98.png)
2. In the pop-up window, enter the name, select the addresses to add, and click **Submit**.
	![](https://main.qcloudimg.com/raw/5b40b996461455a77b723cdd828fd4f3.png)

### Creating a Protocol + Port Group Template
Create a template and add combinations of protocol and port to it for easy management.

#### Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Click **Security** > **Parameter Template** on the left sidebar to access the management page.
3. Select the **Protocol Port** tab and click **+ New**.
4. In the pop-up window, enter the name and protocol ports and click **Submit**.
   You can add multiple protocol ports in the following ranges and separate them with line breaks:
	- Single port: Such as `TCP:80`;
	- Multiple ports: Such as `TCP:80,443`;
	- Port range: Such as `TCP:3306-20000`;
	- All ports: `TCP:ALL`.
   ![](https://main.qcloudimg.com/raw/aae45c5c950f4e6b6cc75aaedebc48e3.png)

### Creating protocol port group parameter template
You can add multiple created protocol port objects to a protocol port group for unified management.
#### Directions	
1. Select the **Protocol Port Group** tab and click **+ New**.
	![](https://qcloudimg.tencent-cloud.cn/raw/5101e8b5139198a06f6d2a28036af32a.png)
2. In the pop-up window, enter the name, select the protocol port object to be added, and click **Submit**.
	![](https://main.qcloudimg.com/raw/91f6da2d037239206dcadbdf9a02570a.png)

## Modifying a Parameter Template
If you need to modify a created parameter template, for example, to add/delete IP addresses or protocol ports, follow the steps below.

### Directions
1. Click the created IP address, IP address group, protocol port, or protocol port group parameter template and click **Edit** on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/cbb3cb328b614baad17cd236fbe5cb61.png)
2. In the pop-up window, modify the corresponding parameters and click **Submit**.
   
## Deleting a Parameter Template
When a template is deleted, all the policy configurations containing it in the security group will be deleted at the same time. Please evaluate and proceed with caution.

### Directions
1. Click **Delete** on the right of the template.
![](https://qcloudimg.tencent-cloud.cn/raw/bc33be2141b5b267ba2d56cd40793258.png)
2. When this template is deleted, all the policies containing the corresponding IP address or protocol port will also be deleted. After confirming that everything is correct, click **Delete** in the **Confirm Deletion** pop-up window.

## Referring the Template in a Security Group
When you add a security group rule, you can refer to the templates to add IPs and ports quickly.

### Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Click **Security** > **Security Group** on the left sidebar to access the management page.
3. In the list, find the target security group and click its ID to enter the details page.
4. On the **Inbound/Outbound Rules** tab, click **Add Rule**.
5. In the pop-up window, select the **Custom** type, select the created parameter template in **Source** and **Protocol Port**, and click **Complete**. For more information on how to add inbound/outbound rules, please see [Adding a Security Group Rule](https://intl.cloud.tencent.com/document/product/215/35513).
>?If you need to add a new IP address or protocol port in the future, you only need to add it to the corresponding IP address group or protocol port group, and there is no need to modify the security group rules or create another security group.
>
 ![](https://main.qcloudimg.com/raw/3a06123b12ef4814c0c95e33418952cc.png)

## Viewing Associated Security Group
You can view all security group instances that import a parameter template in the following steps.
1. Click **View Association** on the right of the created parameter template.
![](https://qcloudimg.tencent-cloud.cn/raw/1a56775ee22def20e25cb6d54548712d.png)
2. The associated security group list that pops up displays all security group instances associated with this parameter template.
![](https://qcloudimg.tencent-cloud.cn/raw/128b47cf7b2c8e2e9bf0f6a3bbbd37cf.png)


## Importing a Parameter Template
To batch add parameter template configurations, do the following: 
1. Click **Import** on the right of the created parameter template.
![](https://qcloudimg.tencent-cloud.cn/raw/168b2bb3a0b33e520d62a6003dd41a55.png)
2. Upload a local file.
![](https://qcloudimg.tencent-cloud.cn/raw/e9d4e909a47eef27fea79cb1fe86ffdc.png)


## Exporting a Parameter Template
To back up the parameter templates to local, click **Export** on the right of the created parameter template.
![](https://qcloudimg.tencent-cloud.cn/raw/b2e852df8702ef005582c3dcc19549e8.png)
