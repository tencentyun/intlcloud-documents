A parameter template consists of a set of parameters. You can save IP addresses and protocol ports as a template so that you can directly import the template when adding security group rules. Parameter templates, if properly used, can enhance your efficiency in using security groups.
Tencent Cloud supports four types of parameter templates:
- IP address (ipm): supports a single IP address, CIDR block, and IP address range.
- IP address group (ipmg): supports a group of IP address objects.
- Protocol port (ppm): supports a single port, multiple ports, consecutive ports, and all ports. The supported protocols are TCP, UDP, ICMP, and GRE.
- Protocol port group (ppmg): supports a group of protocol port objects.

## Scenarios
Parameter templates are applicable to the following scenarios:
- Manage multiple IP addresses or protocol port groups with the same requirements.
- Manage multiple IP addresses or protocol port groups with frequent editing needs.

## Step 1: Create a Parameter Template
### 1. Create an IP address parameter template
Add IP addresses with the same requirements or frequent editing needs to the IP address object.
1. Log in to [VPC Console](https://console.cloud.tencent.com/vpc).
2. Click **Security** > **Parameter Template** in the left sidebar to go to the management page.
3. On the **IP Address** tab page, click **+New**.
4. In the pop-up box, enter the name and IP address, and click **Submit**.
To add multiple IP addresses, separate them with line breaks. Only IPv4 addresses in the following formats are supported:
 - A single IP address, for example, `10.0.0.1`;
 - An IP range, for example, `10.0.1.0/24`; 
 - Consecutive IP addresses, for example, `10.0.0.1` - `10.0.0.100`.
![](https://main.qcloudimg.com/raw/64ecfd48ffdc728506ef328a0ee19921.png)
5. (Optional) You can add multiple created IP addresses to a group to create an IP address group.
	1. Click the **IP Address Group** tab to enter the management page. On this page, click **+New**.
	2. In the pop-up box, enter the name, select the IP addresses that you want to add, and click **Submit**.
	![](https://main.qcloudimg.com/raw/5b40b996461455a77b723cdd828fd4f3.png)

### 2. Create a protocol port parameter template
Add protocol ports with the same requirements or frequent editing needs to the protocol port object.
1. Log in to [VPC Console](https://console.cloud.tencent.com/vpc).
2. Click **Security** > **Parameter Template** in the left sidebar to go to the management page.
3. Click the **Protocol Port** tab to enter the **Protocol Port** tab page. On this tag page, click **+New**.
4. In the pop-up box, enter the name and protocol port, and click **Submit**.
To add multiple protocol ports, separate them with line breaks. The following protocol port formats are supported:
	- A single port, for example, `TCP:80`;
	- Multiple discrete ports, for example, `TCP:80,443`;
	- Consecutive ports, for example, `TCP:3306-20000`;
	- All ports, for example, `TCP:ALL`.
![](https://main.qcloudimg.com/raw/aae45c5c950f4e6b6cc75aaedebc48e3.png)
5. (Optional) You can add multiple created protocol ports to a group to create a protocol port group.
	1. Click the **Protocol Port Group** tab to enter the management page. On this page, click **+New**.
	2. In the pop-up box, enter the name, select the protocol ports that you want to add, and click **Submit**.
	![](https://main.qcloudimg.com/raw/91f6da2d037239206dcadbdf9a02570a.png)

## Step 2: Import a Parameter Template in a Security Group
1. Log in to [VPC Console](https://console.cloud.tencent.com/vpc).
2. Click **Security** > **Security Group** in the left sidebar to go to the management page.
3. In the list, find the security group to which a parameter template needs to be imported, and click its ID to enter the details page.
4. On the **Inbound Rules or Outbound Rules** tab page, click **Add Rules**.
5. In the pop-up box, choose the corresponding parameter template for the source and protocol port. For detailed instructions for adding inbound and outbound rules, see [Adding Security Group Rules](https://intl.cloud.tencent.com/document/product/215/35513).
> Subsequently, if you need to add new IP addresses or protocol ports, you only need to add them in the corresponding IP address group or protocol port group, without having to modify the security group rules or create another security group.
>
![](https://main.qcloudimg.com/raw/3a06123b12ef4814c0c95e33418952cc.png)

