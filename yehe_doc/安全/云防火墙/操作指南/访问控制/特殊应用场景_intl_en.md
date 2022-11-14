This topic describes special scenarios of the Cloud Firewall access control feature.
## Managing the execution priority of the rule lists
You can manage the execution priority of edge firewall rules, NAT firewall rules, and inter-VPC rules. The following takes **Edge firewall rules** as an example.
### Scenario 1: Sorting rules in the list

1. Log in to the [Cloud Firewall console](https://console.cloud.tencent.com/cfw/ac/internet) and select **Access Control** -> **Edge firewall rules** in the left navigation pane.
2. On the **Edge firewall rules** page, click **Sort** on the top of the list to enter the modification mode.
![](https://qcloudimg.tencent-cloud.cn/raw/ed5f0e5a862b17c35a2cae53b1fb1d1b.png)
3. You can move the positions and priority of rules in batch within the current page, and sort the rules by dragging the icons on their left.
![](https://qcloudimg.tencent-cloud.cn/raw/6b6ea521659578c0505e1099889103f3.png)
4. When you are done, click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/d9593519987cc2d7b6e899b369af097b.png)

**Sort operations**:

- If you change the <strong>position</strong> of any rule when you release the mouse cursor, one sort operation has taken place.
- If you do not change the <strong>position</strong> of any rule when you release the mouse cursor, no sort operation has taken place.
- After a sort operation takes place, the **Cancel** button becomes active.
- Click **Recover** once to return the list to the state before the last sort operation.
- If you click **Save**, you will see a <strong>Sorted successfully</strong> toast at the top of the page.
- If you click **Cancel**, the list will return to the initial state and all sort operations will not take effect.

### Scenario 2: Modifying a rule to move it to a specified position
When you need to move a rule within a large range, sorting is inefficient. Instead, you can use the modification feature. You can modify the execution priority of only one rule at a time.
1. Log in to the [Cloud Firewall console](https://console.cloud.tencent.com/cfw/ac/internet) and select **Access Control** -> **Edge firewall rules** in the left navigation pane.
2. On the **Edge firewall rules** page, find the rule you want to move in the list, and determine the new position.
2. Click **Modify** on the right to enter the rule modification mode.
3. Modify the execution priority to the desired value.
>! Execution priority values cannot be repeated and are continuous. As such, the minimum value is 1 and the maximum value is the total number of rules in the current list.

![](https://qcloudimg.tencent-cloud.cn/raw/ae03f6c8493bdcc7f0b30ef9ffc33ce8.png)
&nbsp;

4. Click **Complete** and check the rule priority.
>? When you modify the execution priority of a rule in the list, the positions of all other rules will be automatically adjusted. 

### Scenario 3: Inserting a rule to a specified position in an existing list
Cloud Firewall allows you to insert a rule between any two rules, and the inserted rule will be executed in the priority.

The rule will be inserted above the selected position. In the following example, we want to insert a rule between the rules in positions **2** and **3**:
1. Log in to the [Cloud Firewall console](https://console.cloud.tencent.com/cfw/ac/internet) and select **Access Control** -> **Edge firewall rules** in the left navigation pane.
2. On the **Edge firewall rules** page, find the rule in position **3** in the list, and click **Add one above** on the right.
2. The rule modification box will be displayed above the rule in position **3**.
3. In the box, enter the fields of the new rule and click *Complete** to insert the rule.
>? The inserted rule will take the position of the rule below it, and the execution priority of all the rules below the new rule will be **moved down by one position**.

![](https://qcloudimg.tencent-cloud.cn/raw/63233c27c01a55aa9dfbac8b10c8a1cc.png)

## Checking if rules are effective

- **Method 1**: Check the hit counts in the access control list. If there are hits, the rules have taken effect.
>? If a rule has zero hits, it does not necessarily mean that the rule is incorrectly configured. The rule may simply have no hits for the time being.

![](https://qcloudimg.tencent-cloud.cn/raw/fb65e3d462ec5de8bf2eec5397b13070.png)
&nbsp;

- **Method 2**: Select **Log Auditing** -> **[Access Control Logs](https://console.cloud.tencent.com/cfw/log)** in the left navigation pane to view the access control logs (rule hit logs). If a rule is included in the log, the rule has taken effect.
![](https://qcloudimg.tencent-cloud.cn/raw/87f99a02f30c681518b8bcc134a31faa.png)

## Operation locking

At any one time, only one user is allowed to execute any one of the following operations on a single access control list with the same AppID (the firewall ID is used for VPCs): **Add rule**, **Import rule**, **Sort**, **Modify**, and **Add one above**.

When performing operations on a list, you may see the toast **The list is being modified by others. Please wait.** This means that another user is performing operations on the list.
>? Operations are locked for 5 minutes, and will be automatically unlocked after that time period.

![](https://qcloudimg.tencent-cloud.cn/raw/beac6c4b2867f625115f2f4ed6209a64.png)

## More information
For more information, please see [Access Control](https://intl.cloud.tencent.com/document/product/1160/49833).
