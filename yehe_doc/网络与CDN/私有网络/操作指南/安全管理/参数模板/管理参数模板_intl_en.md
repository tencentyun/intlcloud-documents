## Parameter Template Use Cases
Parameter template is an efficient, fast, and easy-to-maintain way to add rules in security groups. For example, when you need to add multiple IP ranges, specified IPs, or protocol ports of multiple types, you can define a parameter template. You can also use the parameter template subsequently to maintain the IP sources and protocol ports in the security group rules.
>?All the IP addresses and protocol ports in this document are examples. Please replace them according to your actual business conditions during configuration.
>


## Example Description
Suppose you want to configure the following security group rules and need to update the inbound source IP range and protocol port later:
+ Inbound rules:
 + Allowed source IP range: 10.0.0.16-10.0.0.30; protocol port: TCP:80,443
 + Allowed source CIDR block: 192.168.3.0/24; protocol port: TCP:3600-15000

+ Outbound rules:
 Rejected target IP address: 192.168.10.4; protocol port: TCP:800


## Solution
Because you have the same security group policy for multiple IP ranges and protocol ports, and you need to update the source IP range later, you can use a parameter template to implement the addition and maintenance of security group rules.



### Step 1. Create a parameter template
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Select **Security** > **Parameter Template** on the left sidebar to access the management page.
3. On the **IP Address** tab, click **+ New** to create an IP address parameter template for adding inbound and outbound rules.
4. In the pop-up window, enter the source IP range and click **Submit**.</br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/581bf5c79ec186d05290c8ab73138338.png" width="45%" />
</br>
The newly created IP address parameter template is as shown below.
<img src="https://qcloudimg.tencent-cloud.cn/raw/67f474a18a1f4cca9001995700d80559.png" >
5. On the **Protocol Port** tab, click **+ New** to create a protocol port parameter template for adding inbound and outbound rules.
<img src="https://qcloudimg.tencent-cloud.cn/raw/fa453b19c81e823dee3afc0e5b473d72.png" width="45%" /> 
</br>
The newly created protocol port parameter template is as shown below:
<img src="https://qcloudimg.tencent-cloud.cn/raw/9ce16cdc7fdbeec0f3117ca4c8e3a863.png" >

### Step 2. Add a security group rule
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Select **Security** > **Security Group** on the left sidebar to access the management page.
3. In the list, find the security group that needs to import the parameter template and click its ID to enter the details page.
4. On the **Inbound/Outbound Rules** tab, click **Add Rule**.
5. In the pop-up window, select the custom type, select the corresponding IP address parameter template for the source/target, select the corresponding protocol port parameter template for the protocol port, and click **Complete**.
![](https://qcloudimg.tencent-cloud.cn/raw/9039d1de4a8a2891873faaec92627fee.png)

	
### Step 3. Update the parameter template
Suppose you need to add an inbound rule with the IP source being the `10.0.1.0/27` IP range and the protocol port being `UDP:58`. You can directly update the parameter templates of the IP address `ipm-0ge3ob8e` and the protocol port `ppm-4ty1ck3i`.
1. On the **IP Address** tab of the parameter template, find the `ipm-0ge3ob8e` parameter template.
2. Click **Edit** on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/f7f28bf7fdb77f25c6c1e2fbf5555809.png)
3. In the pop-up window, add the `10.0.1.0/27` IP range in a new line and click **Submit**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/0be07de1ae0e9858ec94327cb0b3ba75.png" width="45%" />
4. On the **Protocol Port** tab of the parameter template, find the `ppm-4ty1ck3i` parameter template.
5. Click **Edit** on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/9ba28cdac71dbded7259eee9e74d128a.png)
6. In the pop-up window, add the `UDP:58` inbound protocol port in a new line and click **Submit**.</br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/b4f15b9ef711caae75920b2f70780667.png" width="45%" />
