Access control rules can filter specific domain names or filter traffic by geographic location. NAT firewall has two access control rule lists, namely inbound rules and outbound rules. **Inbound rules** apply to the incoming north-south traffic over the edge firewall, while **outbound rules** apply to the outgoing north-south traffic over the edge firewall. This topic describes operations related to inbound rules, and those for outbound rules are similar.
## Operation guide
1. Log in to the [Cloud Firewall console](https://console.cloud.tencent.com/cfw/ac/internet), select **Access Control** in the left navigation pane, and then select **NAT firewall rules**.
2. On the "NAT firewall rules" page, select a region, and then click **Inbound rules**.
![](https://qcloudimg.tencent-cloud.cn/raw/530a65f3f31f8d3890d3dcfc6ae3a397.png)
3. On the **Inbound rules** page, you can create access control rules for different regions, and view the details about rule lists (the used quota of inbound or outbound rules and the total quota of rule lists), recent operations, and access control rules. "Recent operations" show your recent operations on the rule lists:
   - Click **Details** to view details of a specific operation.
   - Click **View operation logs** to view detailed operation records.
![](https://qcloudimg.tencent-cloud.cn/raw/7e6e597e631acefcbf952052dba59669.png)
4. On the **Inbound rules** page, add a rule and configure it. Here is an example for adding inbound rules.
   i. Click **Add rule** on the **Inbound rules** page.
	 <img src="https://qcloudimg.tencent-cloud.cn/raw/7083bc22c491e86c520d2d31f4a7cb67.png" style="zoom:67%;" />
   ii. Configure the inbound rule in the **Add inbound rule** window displayed. The "Access source type" can be an IP address, geographic location, cloud vendor, or [address template](https://intl.cloud.tencent.com/document/product/1160/49863#IP). The "Access destination type" can be an IP address, asset instance, resource tag, address template, or asset group. Select priority for rules based on their importance. After selecting the access source and destination, enter the destination port, select the protocol and the policy to implement, enter rule descriptions, and then click **OK** to complete the configuration.
>?
>- Access destination type region: The region where the cloud instance is located.
>- Access source type: The type of an external source when an inbound rule is added.

![](https://qcloudimg.tencent-cloud.cn/raw/d354e8d209ed81bbf72b7b821cb11a25.png)

**Field description**:
  - **Priority**: The priority of the access control rule. The priorities of outbound and inbound rules are independent of each other. The rule with the highest priority is evaluated first. If a given rule is matched, rules with lower priorities will not be evaluated. When you modify the priority of a given rule, the priorities of the original rule with that priority and all the subsequent rules will increase by 1. When you delete a given rule, the priorities of all the subsequent rules will decrease by 1.
  - **Access source**: The access source of an inbound rule can be any public IP. It supports an IP, CIDR block, and location.
  - **Access destination**: The access destination of an inbound rule can be any private network asset in the current region. It supports an IP address, asset instance, resource tag, address template, and asset group. The supported access source and destination types of an outbound rule are the opposite.
  - **Destination port**: TCP/UDP rules support single port numbers (e.g., "80"), port ranges (e.g., "80/80", "-1/-1", "0/65535"), and discrete port numbers separated with commas (e.g., "80,443,3380/3389"). For ICMP rules, port configuration is not required.
  - **Protocol**: For the current CFW edition, supported inbound protocols include TCP and UDP, and supported outbound protocols include TCP, UDP, ICMP, HTTP, HTTPS, SMTP, SMTPS, DNS, and FTP.
  - **Policy description**:
     - **Allow**: Allow the matched traffic and record the hit count and traffic logs, but not access control logs.
     - **Observe**: Allow the matched traffic and record the hit count, access control logs, and traffic logs.
     - **Block**: Block the matched traffic and record the hit count and access control logs, but not traffic logs.
  - **Description**: The rule description with up to 50 characters. You can use a pair of # to insert special settings. Your current CFW edition supports #long connection#.
  - **NAT firewall wildcard rules**:
    CFW provides different wildcard rules for IP address, port, and domain name.

  <table>
         <thead>
             <tr>
                 <th >Input field</th>
                 <th >Input example</th>
                 <th >Description</th>
             </tr>
         </thead>
         <tbody>
             <tr>
                 <td>Access source/Access destination</td>
                 <td>0.0.0.0/0</td>
                 <td>Indicates all IP addresses.</td>
             </tr>
             <tr>
                 <td>Domain name</td>
                 <td>*</td>
                 <td>Indicates all domain names.</td>
             </tr>
             <tr>
                 <td><font >Domain name</font></td>
                 <td><font >*.aa.com</font></td>
                 <td><font >Indicates second-level domain names starting with an asterisk (*): aa.com.</font></td>
             </tr>
             <tr>
                 <td><font >Destination port</font></td>
                 <td><font>-1/-1</font></td>
                 <td><font >Indicates all ports.</font></td>
             </tr>
             <tr>
                 <td><font >Destination port</font></td>
                 <td><font >0/65535</font></td>
                 <td><font>Indicates all ports.</font></td>
             </tr>
             <tr>
                 <td><font>Destination port</font></td>
                 <td><font>80,443,3389</font></td>
                 <td><font>Indicates ports 80, 443, and 3389.</font></td>
             </tr>
             <tr>
                 <td><font>Destination port</font></td>
                 <td><font>80/443</font></td>
                 <td><font>Indicates all ports between port 80 and port 443.</font></td>
             </tr>
             <tr>
                 <td><font>Destination port</font></td>
                 <td><font>80/443,3389</font></td>
                 <td><font>Indicates all ports between port 80 and port 443, as well as port 3389.</font></td>
             </tr>
         </tbody>
     </table>

5. Click **Copy** in the action column on the right to add multiple rules.
>? In the **Add inbound rule** window, one rule uses one line, and a new rule is added to the end of the list by default. The last rule added has the largest priority number or the lowest priority.

 * **Scenario 1**: You have configured the rule list, and need to add rules in batch.
     1. Click **Copy** in the action column on the right to add a rule to the next line of the current rule. A maximum of 10 rules can be added at a time.
![](https://qcloudimg.tencent-cloud.cn/raw/13897e07db8a87066a049e94406aa7aa.png)
     2. Complete all fields in the list.
     3. Check whether the priority of the rules added in batch meets your expectations.
     4. Click **OK** to submit the rules configured.
   * **Scenario 2**: You need to configure multiple rules for an IP address.
     1. Edit a rule to fill in the fields that need to be input repeatedly.
     2. Click **Copy** in the action column on the right to add a rule to the next line of the current rule, with the fields automatically populated with the same values as from the edited rule. A maximum of 10 rules can be added at a time.
![](https://qcloudimg.tencent-cloud.cn/raw/823d003c215ce40693d26e3c18b40aec.png)
     3. Complete other fields in the list.
     4. Check whether the priority of the rules added in batch meets your expectations.
     5. Click **OK** to submit the rules configured.

6. Import rules: Click **Import rule** to import rules from a local file. You can specify the import location, download the import template, or export existing rules.
    ![](https://qcloudimg.tencent-cloud.cn/raw/81142bab842058eea1fa7c1bd53f11dc.png)
7. Back up and roll back rules: Click **Backup rules** in the upper right corner to back up existing NAT firewall rules. When the rules are greatly changed, you can click **Roll back** to the right of the backup file to recover the rules.
 1. Click **Backup rules** in the upper right corner to enter the **Back up and roll up rules** page. Click **Create backup**, select **NAT firewall rules** from the drop-down list and enter a description, and then click **OK** to complete the backup.
![](https://qcloudimg.tencent-cloud.cn/raw/730443990ff780bdddad36d2af314853.png)
  2. To roll back rules, click **Roll back** on the right side of the backup file, and you can recover the rules after confirmation.
![](https://qcloudimg.tencent-cloud.cn/raw/1c510076b8ea7926fa00ce1f85d49cd4.png)

## More information
- For the information about how to control the inbound and outbound traffic over the edge firewall on the Cloud Firewall console, please see Edge Firewall Rules.
- For information about how to set inter-VPC firewall rules on the Cloud Firewall console, please see [Inter-VPC Firewall Rules](https://intl.cloud.tencent.com/document/product/1160/49846).
- For the special scenarios of the Cloud Firewall access control feature, please see [Special Scenarios](https://intl.cloud.tencent.com/document/product/1160/49850).
- For questions about NAT firewall rules, please see [NAT Firewall](https://intl.cloud.tencent.com/document/product/1160/49810).
