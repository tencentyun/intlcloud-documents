Based on adaptive learning technologies, the abnormal process feature applies preset rules and custom check rules to monitor abnormal process startups and then trigger alerts or block the exceptions in real time. It consists of the event list and rule configuration modules. This document describes the rule configuration feature of advanced prevention.

## Filtering and Refreshing Rules
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Advanced Prevention** > **Abnormal Processes** > **Rule configuration** on the left sidebar.
2. On the **Rule configuration** page, click the search box and search for configured rules by rule name.
![](https://qcloudimg.tencent-cloud.cn/raw/c29e8d57105c9b08960a9a4d14b0efa7.png)
3. On the **Rule configuration** page, click ![](https://main.qcloudimg.com/raw/84b6cc4d2eabf9ed7fc0bea43503bb1d.png) on the right of the **Operation** column to refresh the rule list.

## Adding a Rule
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Advanced Prevention** > **Abnormal Processes** > **Rule configuration** on the left sidebar.
2. On the **Rule configuration** page, click **Create rule**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/7953fc514320e3c19c865744b0f0ffd0.png" style="zoom:67%;" />
3. On the **Add rule** page, configure the basic information and rules and specify the scope.
 - Basic information: Enter the rule name of the event. Toggle on or off ![](https://main.qcloudimg.com/raw/9053f4e9bc709aa720fccd5045eb8cd0.png) to enable or disable rule check.
>? This rule will no longer be executed once disabled.

![](https://qcloudimg.tencent-cloud.cn/raw/27cf3c930bf2a7dd28e8e46213c81304.png)
 - Configure rules: Enter the process path and select the action. Click **Add** or **Delete** to add or delete a rule.
>?
>- You can configure up to 30 rules.
>- Actions to be executed include:
>  - Block: Once a rule is hit, the process will be blocked and the event details will be recorded.
>  - Alert: Trigger alerts about the event, allow running of the process and log the event details.
>  - Allow: When a rule is hit, the process will be automatically allowed without being recorded.	

 - Images: **All images** or **Specified images**. Click ![](https://main.qcloudimg.com/raw/37d813d17a69271ce31b3233ad0a949e.png) or ![](https://main.qcloudimg.com/raw/be9e47bccb644d8a099149bac4aef1e0.png) to select or delete the target specified image.
>? You can press Shift to select multiple ones.

 ![](https://qcloudimg.tencent-cloud.cn/raw/0abb56b89008e45c97729b71b39d6add.png)
4. After selecting the target content, click **Set** or **Cancel**.

## Copying a Rule
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Advanced Prevention** > **Abnormal Processes** > **Rule configuration** on the left sidebar.
2. On the **Rule configuration** page, click **Copy** on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/3bfb95e0f3efb76350b09f554396507c.png)
3. On the **Copy rule** page, enter the rule name, toggle **On/Off**, configure rules, and specify the scope.
![](https://qcloudimg.tencent-cloud.cn/raw/974d0beb1971db02649617d450084f59.png)
4. After selecting the target content, click **OK** or **Cancel**.


## Editing a Rule
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Advanced Prevention** > **Abnormal Processes** > **Rule configuration** on the left sidebar.
2. On the **Rule configuration** page, click **Edit** on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/1b6ebaf254df4508307b4c5f985df5cc.png)
3. On the **Edit rule** page, modify the basic information, configure rules, and specify the scope.
![](https://qcloudimg.tencent-cloud.cn/raw/948140a88f137e45044f96ac70bff31b.png)
4. After selecting the target content, click **OK** or **Cancel**.


## Deleting a Rule
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Advanced Prevention** > **Abnormal Processes** > **Rule configuration** on the left sidebar.
2. On the **Rule configuration** page, delete a rule in either of the following methods:
 - Select the target rule, click ![](https://main.qcloudimg.com/raw/37d813d17a69271ce31b3233ad0a949e.png), and click **Delete** on the left in the **Operation** column.
![](https://qcloudimg.tencent-cloud.cn/raw/51136a3342f796aa5f8ed58657184124.png)
 - Select the target rule and click **Delete** on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/de865ee03cdbe5234ff24e74ea54cbd7.png)
2. In the pop-up window, click **Delete** or **Cancel**.
>? The rule cannot be recovered once deleted, and images associated with the rule will be automatically associated with the default system rule.

## Exporting a Rule
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Advanced Prevention** > **Abnormal Processes** > **Rule configuration** on the left sidebar.
2. On the **Rule configuration** page, click ![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png) to select the target abnormal process rule and click ![](https://main.qcloudimg.com/raw/24d375a75e4ee95c77910d101f7203dd.png) to export it.
>? Click ![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png) in the **Operation** column to select multiple ones.

![](https://qcloudimg.tencent-cloud.cn/raw/bda1849aff54d9a116a5f15eb1d74ac0.png)


## Custom List Management
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Advanced Prevention** > **Abnormal Processes** > **Rule configuration** on the left sidebar.
2. On the **Rule configuration** page, click ![](https://main.qcloudimg.com/raw/d42b27540eef9bf90a9e30f96b500bf3.png) to pop up the **Custom List Management** window.
3. In the pop-up window, select the target type and click **OK**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/07cf68282b79f005d5f2b74c42985edc.png" style="zoom:67%;" />

### Key fields in the list
1. Rule category: Preset rule or custom rule.
2. Associated images: Number of images for which the rule takes effect. Click the number of affected images to pop up the drawer on the right, which displays the rule details.
![](https://qcloudimg.tencent-cloud.cn/raw/a2aa5b3d703709882bbffd76270b37d7.png)
3. Status: On/Off.
4. Operation: System rules can only be copied, and custom rules can be copied, edited, or deleted.
