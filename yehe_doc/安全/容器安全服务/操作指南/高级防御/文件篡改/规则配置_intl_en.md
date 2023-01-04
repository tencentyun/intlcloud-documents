The file tampering feature provides the lists of monitored events and configured rules. The rule configuration module displays the list of configured rules.

## Filtering and Refreshing Rules
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Advanced Prevention** > **File Tampering** > **Rule configuration** on the left sidebar.
2. On the **Rule configuration** page, click the search box and search for configured rules by rule name.
<img src="https://qcloudimg.tencent-cloud.cn/raw/664fa67770ae2cbf6bad99445f5759c1.png" style="zoom:67%;" />
3. On the **Rule configuration** page, click ![](https://main.qcloudimg.com/raw/84b6cc4d2eabf9ed7fc0bea43503bb1d.png) on the right of the **Operation** column to refresh the rule list.

## Adding a Rule
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Advanced Prevention** > **File Tampering** > **Rule configuration** on the left sidebar.
2. On the **Rule configuration** page, click **Create rule**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/a79a2c063f36b2f45b59414dbe1b28cc.png" style="zoom:67%;" />
3. On the **Add rule** page, configure the basic information and rules and specify the scope.
 - Basic information: Enter the rule name of the event. Toggle on or off ![](https://main.qcloudimg.com/raw/9053f4e9bc709aa720fccd5045eb8cd0.png) to enable or disable rule check.
>? This rule will no longer be executed once disabled.

![](https://qcloudimg.tencent-cloud.cn/raw/a2e17ca06ea6c9011ede4f81a6f968ba.png)
 - Configure rules: Enter the process path and accessed file path and select the action. Click **Add** or **Delete** to add or delete a rule.
>?
>- You can configure up to 30 rules.
>- Actions to be executed include:
>  - Block: Once a rule is hit, the process will be blocked and the event details will be recorded.
>  - Alert: Trigger alerts about the event, allow running of the process and log the event details.
>  - Allow: When a rule is hit, the process will be automatically allowed without being recorded.

 - Images: **All images** or **Specified images**. Click ![](https://main.qcloudimg.com/raw/37d813d17a69271ce31b3233ad0a949e.png) or ![](https://main.qcloudimg.com/raw/be9e47bccb644d8a099149bac4aef1e0.png) to select or delete the target specified image.
>? You can press Shift to select multiple ones.

 ![](https://qcloudimg.tencent-cloud.cn/raw/0298cff443320bf034a655e3b8ebe735.png)
4. After selecting the target content, click **Set** or **Cancel**.

## Copying a Rule
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Advanced Prevention** > **File Tampering** > **Rule configuration** on the left sidebar.
2. On the **Rule configuration** page, click **Copy** on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/3307de390d0e071e1420d22f04c07b8b.png)
3. On the **Copy rule** page, enter the rule name, toggle **On/Off**, configure rules, and specify the scope.
![](https://qcloudimg.tencent-cloud.cn/raw/a9891daab86479479679d8c9acfcb45b.png)
4. After selecting the target content, click **OK** or **Cancel**.


## Editing a Rule
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Advanced Prevention** > **File Tampering** > **Rule configuration** on the left sidebar.
2. On the **Rule configuration** page, click **Edit** on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/eaac14e992358c784e69d7ea471de8c1.png)
3. On the **Edit rule** page, modify the basic information, configure rules, and specify the scope.
![](https://qcloudimg.tencent-cloud.cn/raw/2b13a0ebfe617b456422a74c19b115cf.png)
4. After selecting the target content, click **OK** or **Cancel**.

## Deleting a Rule
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Advanced Prevention** > **File Tampering** > **Rule configuration** on the left sidebar.
2. On the **Rule configuration** page, delete a rule in either of the following methods:
 - Select the target rule, click ![](https://main.qcloudimg.com/raw/37d813d17a69271ce31b3233ad0a949e.png), and click **Delete** on the left in the **Operation** column.
![](https://qcloudimg.tencent-cloud.cn/raw/196ff3f63be330fa1bbef173d2c6c201.png)
 - Select the target rule and click **Delete**.
![](https://qcloudimg.tencent-cloud.cn/raw/4b74b56b3b5cd97d267476eb0cc18526.png)
3. In the pop-up window, click **Delete** or **Cancel**.
>? The rule cannot be recovered once deleted, and images associated with the rule will be automatically associated with the default system rule.

## Exporting a Rule
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Advanced Prevention** > **File Tampering** > **Rule configuration** on the left sidebar.
2. On the **Rule configuration** page, click ![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png) to select the target file tampering rule and click ![](https://main.qcloudimg.com/raw/24d375a75e4ee95c77910d101f7203dd.png) to export it.
>? Click ![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png) in the **Operation** column to select multiple ones.

![](https://qcloudimg.tencent-cloud.cn/raw/a98fb4850b43a42d168a87ed4260f101.png)

## Custom List Management
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Advanced Prevention** > **File Tampering** > **Rule configuration** on the left sidebar.
2. On the **Rule configuration** page, click ![](https://main.qcloudimg.com/raw/d42b27540eef9bf90a9e30f96b500bf3.png) to pop up the **Custom List Management** window.
3. In the pop-up window, select the target type and click **OK**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/199307590502bb4da3904698949b9980.png" style="zoom:67%;" />

### Key fields in the list
1. Rule category: Preset rule or custom rule.
2. Associated images: Number of images for which the rule takes effect. Click the number of affected images to pop up the drawer on the right, which displays the rule details.
3. Status: On/Off.
4. Operation: System rules can only be copied, and custom rules can be copied, edited, or deleted.
