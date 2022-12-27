You can create custom service control policies to restrict specified operations on specified resources and define the permissions boundary for departments and members in your organization.

## Creation Methods

**1. Create a custom service control policy in visual editing mode**
The system offers an easy-to-use WYSIWYG editing page. You only need to select an effect, Tencent Cloud service, action (operation), resource, and condition to create a custom service control policy. In addition, it also offers a smart verification feature to help you guarantee the correctness and effectiveness of the policy.

**2. Create a custom service control policy by editing a script**
The system offers a JSON script editing page, where you can write a custom service control policy according to the policy syntax and structure. This method is flexible and suitable if you are familiar with the policy syntax.

### Creating a custom service control policy in visual editing mode

1. Log in to the [TCO console](https://console.intl.cloud.tencent.com/organization).

2. On the left sidebar, select **Organization account** > **Service control policy**.

3. On the **Policy list** tab, click **Create policy**.

4. On the **Create policy** page, click the **Visual policy generator** tab.

5. Configure the service control policy and click **Next** to edit basic information.

(1) In the **Effect** section, select **Allow** or **Deny**.

(2) In the **Service** section, select a Tencent Cloud service.
<dx-alert infotype="notice" title="">
Only Tencent Cloud services displayed on the page support the visual editing mode.
</dx-alert>
(3) In the **Action** section, select **All actions** or **Custom action**.

The system automatically filters configurable actions based on the Tencent Cloud service selected in the previous step. If you select **Custom action**, you need to select specific actions.

(4) In the **Resource** section, select **All resources** or **Specific resources**.

The system automatically filters configurable resource types based on the actions selected in the previous step. If you select **Specific resources**, you need to click **Add a six-segment resource description** and configure the specific resource ARN. You can click **Match all** to quickly select all resources corresponding to the configuration item.

(5) **(Optional)** In the **Condition** section, click **Source IP** to configure a condition.

You can enter an IP (or IP range) or add other conditions, including Tencent Cloud general or service-level conditions. The system automatically filters configurable conditions based on the service and actions selected in previous steps. You only need to select the condition keys to configure the specific content.

6. Enter the **Name** and **Description** of the service control policy and click **Complete**.

### Creating a custom service control policy in JSON mode

1. Log in to the [TCO console](https://console.intl.cloud.tencent.com/organization).

2. On the left sidebar, select **Organization account** > **Service control policy**.

3. On the **Policy list** tab, click **Create policy**.

4. On the **Create policy** page, click the **JSON** tab.

5. Enter the content of the service control policy and click **Next** to edit basic information.

6. Enter the **Name** and **Description** of the service control policy.

## Subsequent Steps

After creating the custom service control policy successfully, you need to bind it to a department or member for it to take effect. For detailed directions, see [Binding Custom Service Control Policy](https://www.tencentcloud.com/document/product/1031/51875).
