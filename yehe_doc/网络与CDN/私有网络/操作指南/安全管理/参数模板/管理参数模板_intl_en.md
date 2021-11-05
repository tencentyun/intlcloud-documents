This document describes how to create and maintain parameter templates (IP address, IP address group, protocol port, and protocol port group) in the console and how to use them in security groups.


## Creating Parameter Template

### Creating IP address parameter template
Add the IPs with the same needs or frequently edited to this IP address object.

#### Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Click **Security** > **Parameter Template** on the left sidebar to access the management page.
3. Select the **IP Address** tab and click **+ New**.
4. In the pop-up window, enter the name and IP addresses and click **Submit**.
 You can add multiple IPv4 addresses in the following ranges and separate them by line breaks:
 - Single IP address: such as `10.0.0.1`;
 - CIDR block: such as `10.0.1.0/24`; 
 - IP range: such as `10.0.0.1` - `10.0.0.100`.
![](https://main.qcloudimg.com/raw/64ecfd48ffdc728506ef328a0ee19921.png)

### Creating IP address group parameter template
You can add multiple IP address objects to an IP address group for unified management.

#### Directions
1. Select the **IP Address Group** tab and click **+ New**.
	![](https://qcloudimg.tencent-cloud.cn/raw/333211f6e4bb94b7611cb6d4bb327c98.png)
2. In the pop-up window, enter the name, select the IP address objects to be added, and click **Submit**.
	![](https://main.qcloudimg.com/raw/5b40b996461455a77b723cdd828fd4f3.png)

### Creating protocol port parameter template
You can add the protocol ports with the same needs or frequently edited to this protocol port object.

#### Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Click **Security** > **Parameter Template** on the left sidebar to access the management page.
3. Select the **Protocol Port** tab and click **+ New**.
4. In the pop-up window, enter the name and protocol ports and click **Submit**.
   You can add multiple protocol ports in the following ranges and separate them with line breaks:
	- Single port: such as `TCP:80`;
	- Multiple ports: such as `TCP:80,443`;
	- Port range: such as `TCP:3306-20000`;
	- All ports: such as `TCP:ALL`.
![](https://main.qcloudimg.com/raw/aae45c5c950f4e6b6cc75aaedebc48e3.png)

### Creating protocol port group parameter template
You can add multiple created protocol port objects to a protocol port group for unified management.
#### Directions	
1. Select the **Protocol Port Group** tab and click **+ New**.
	![](https://qcloudimg.tencent-cloud.cn/raw/5101e8b5139198a06f6d2a28036af32a.png)
2. In the pop-up window, enter the name, select the protocol port object to be added, and click **Submit**.
	![](https://main.qcloudimg.com/raw/91f6da2d037239206dcadbdf9a02570a.png)

## Modifying Parameter Template
If you need to modify a created parameter template, for example, to add/delete IP addresses or protocol ports, follow the steps below.

### Directions
1. Click the created IP address, IP address group, protocol port, or protocol port group parameter template and click **Edit** on the right. For example, the following figure shows how to modify IP address objects.
    ![](https://qcloudimg.tencent-cloud.cn/raw/cbb3cb328b614baad17cd236fbe5cb61.png)
2. In the pop-up window, modify the corresponding parameters and click **Submit**.
   
## Deleting Parameter Template
If you no longer use a parameter template, you can delete it. When this template is deleted, all the policy configurations containing it in the security group will be deleted at the same time. Please evaluate and proceed with caution.

### Directions
1. Click **Delete** on the right of the created parameter template.
   ![](https://qcloudimg.tencent-cloud.cn/raw/bc33be2141b5b267ba2d56cd40793258.png)
2. When this template is deleted, all the policies containing the corresponding IP address or protocol port will also be deleted. After confirming that everything is correct, click **Delete** in the **Confirm Deletion** pop-up window.

## Importing Parameter Template into Security Group
After creating a parameter template, you can directly import it when adding rules in a security group to quickly add IP sources or protocol ports, which helps improve your efficiency of adding security group rules.

### Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Click **Security** > **Security Group** on the left sidebar to access the management page.
3. In the list, find the security group that needs to import the parameter template and click its ID to enter the details page.
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
