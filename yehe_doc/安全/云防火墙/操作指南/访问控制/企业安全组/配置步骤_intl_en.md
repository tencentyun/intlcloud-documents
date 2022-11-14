## Adding rules
1. Log in to the [Cloud Firewall console](https://console.cloud.tencent.com/cfw/ac/secgroupnew), select **Access Control** in the left navigation pane, and then select **Enterprise security groups**.
2. On the **Enterprise security groups** page, click **Add rule**.
3. In the **Add rule** window displayed, configure the parameters and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/7885d50903093d454006bb15093daca2.png)
**Parameters**
 - **Priority**: The execution order of access control rules. The rule with the highest priority is evaluated first. If a given rule is matched, rules with lower priorities will not be evaluated. When you modify the priority of a given rule, the priorities of the original rule with that priority and all the subsequent rules will increase by 1. When you delete a given rule, the priorities of all the subsequent rules will decrease by 1.
 - Access source: It can be an IP/CIDR, parameter template, asset instance, asset group, resource tag, region, and other types.
 - Access destination: It can be an IP/CIDR, parameter template, asset instance, asset group, resource tag, region, and other types.
>? You can select any type for the access source and access destination as listed above. But you cannot select region for the access source and access destination at the same time.

 - Destination port: Supports single port numbers (e.g., "80"), port ranges (e.g., "80/80", "-1/-1", "1/65535"), and discrete port numbers separated with commas (15 at most).
 - Protocol: The current CFW edition supports UDP, TCP, and ICMP.
 - Policy:
    - Allow: Allow the matched traffic but do not record the hit logs of enterprise security groups.
    - Block: Block the matched traffic and record the hit logs of enterprise security groups.
 - Description**: The rule description with up to 50 characters. You can use a pair of # to insert special settings. Your current CFW edition supports #Only publish to source# and #Only publish to destination#.
>? When the access destination address is an instance, subnet, or private network address, an identical inbound rule can be automatically assigned using "Auto two-way publishing". To cancel auto two-way publishing, you can add keywords to the description: #Only publish to source# (the security group rules are only published to the source); #Only publish to destination# (the security group rules are only published to the destination).

4. Once added, the rules will be displayed in the rule list.
 ![](https://qcloudimg.tencent-cloud.cn/raw/dcf3266787e1fe2511594d066a2d2eb7.png)
5. Once the rules are added and published successfully, you can view security groups on the **CFW security group details** page or the [Security group page](https://console.cloud.tencent.com/vpc/securitygroup?rid=1&rid=1) on the VPC console, which are associated with instances automatically.

## Viewing security group details
1. Log in to the [Cloud Firewall console](https://console.cloud.tencent.com/cfw/ac/secgroupnew), select **Access Control** in the left navigation pane, and then select **Enterprise security groups**.
2. On the **Enterprise security group** page, click **Security group details**.
![](https://qcloudimg.tencent-cloud.cn/raw/7bd36e721d5b6127853f63a6a5b0167f.png)
3. On the **Security group details** page, you can view the regions of instances and quota information. The quota can be increased as needed.
![](https://qcloudimg.tencent-cloud.cn/raw/ebcc2c8d01525a436e24b256ff0e9e14.png)
4. At the bottom of the **Security group details** page, you can view associated instances, security group lists, and security group rules.
 - Associated instances: Display information of all instances in a region, such as instance name, instance type, network, and IP address. Click the number in the "Security group" or "Security group rule" column to go to the security group list or rule details page of an instance. Click **View details** to go to the instance details page.
![](https://qcloudimg.tencent-cloud.cn/raw/97bdaaa2f3f3eb9983baa1a92e7aa494.png)
 - Security group list: It displays all the security group lists for the current region, the instances associated with each security group, the number of security group rules, the creation time, and other information. Click the number in the "Associated instance" or "Security group rule" column to go to the security group list or rule details page of an instance. Click **View details** to go to the security group details page in the VPC console.
 ![](https://qcloudimg.tencent-cloud.cn/raw/f8155a2a69773014b75c93a896eae3a8.png)
 - Security group rules: Display the inbound and outbound rules of all security groups in the current region. Click ![](https://qcloudimg.tencent-cloud.cn/raw/41eb4aef52d06599b05022e5dfabd945.png) to view the rule details, or check whether the enterprise security group rules are published successfully.
 ![](https://qcloudimg.tencent-cloud.cn/raw/44ee82266f0f84473e6017c5ea742d11.png)
5. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/securitygroup), click **Security** -> **Security groups** in the left navigation pane, and select the regions and items.
![](https://qcloudimg.tencent-cloud.cn/raw/1e0ba16be9d24517273cb81710f0b0ee.png)
6. Click the ID/name of a security group to view its inbound rules, outbound rules, and associated instances.
![](https://qcloudimg.tencent-cloud.cn/raw/e89f2358136eaa3ebdade9e59dd180aa.png)

## Managing rules
After setting enterprise security group rules, you can modify, insert, delete, or sort the rules on the **Enterprise security group** page.
#### Editing rules
On the [Enterprise security groups page](https://console.cloud.tencent.com/cfw/ac/secgroupnew), select a rule, click **Modify** to modify the parameters, and then click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/e17eb728c752eb7075d99bff9d7465ad.png)

#### Disabling rules
On the [Enterprise security groups page](https://console.cloud.tencent.com/cfw/ac/secgroupnew), you can disable or enable rules. Once you disable a rule, it will no longer be matched.
![](https://qcloudimg.tencent-cloud.cn/raw/a15d37e54e5f91816f4dd221fcff43a4.png)

#### Inserting rules
On the [Enterprise security groups page](https://console.cloud.tencent.com/cfw/ac/secgroupnew), select a rule, click **Insert**, enter parameters, and click **OK** to add a rule above the current rule. The new rule has higher priority than the current rule.
![](https://qcloudimg.tencent-cloud.cn/raw/f08aabccb11838d2e07176484882da44.png)

#### Deleting rules
On the [Enterprise security groups page](https://console.cloud.tencent.com/cfw/ac/secgroupnew), select a rule and click **Delete** to delete it upon second confirmation.
![](https://qcloudimg.tencent-cloud.cn/raw/779c691335105427fa6d07bc3cd48007.png)

#### Sort
The priority of a rule depends on its order in the list.
1. On the [Enterprise security groups page](https://console.cloud.tencent.com/cfw/ac/secgroupnew), click **Sort**, select a rule, and click and hold the rule to drag it to the desired position.
![](https://qcloudimg.tencent-cloud.cn/raw/b69063f6c2e5fb77bfa351125d58be6c.png)
2. Click **Save**, and the new priority of rules will take effect and be automatically published to the instance.

#### Exporting rules
1. On the [Enterprise security groups page](https://console.cloud.tencent.com/cfw/ac/secgroupnew), click ![](https://qcloudimg.tencent-cloud.cn/raw/8006bef9330b3f1da99531210014319c.png) in the upper right corner of the rule list, and the **Export custom list** window will pop up.
![](https://qcloudimg.tencent-cloud.cn/raw/9ae905aae0ebbd420ca70d79273d4daa.png)
2. In the pop-up window, select "Export all" or "Export matched results", and then click **Export**.
![](https://qcloudimg.tencent-cloud.cn/raw/7339532c069aab4bf88232242878f774.png)
