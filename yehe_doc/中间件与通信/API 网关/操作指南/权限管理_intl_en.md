## Operation Scenarios
In the CAM Console, the root account can configure permissions of common operations, services that can be manipulated, and API resources on API Gateway for sub-accounts and collaborators.

## Directions
### Sub-account or collaborator permission management (non-tagged resource)
1. Log in to the **[CAM Console](https://console.cloud.tencent.com/cam/overview)** > **[Policy](https://console.cloud.tencent.com/cam/policy)** with the root account.
2. In the policy list, click **Create Custom Policy** in the top-left corner.
3. In the policy creation pop-up window, select **Create by Policy Builder**:
![](https://main.qcloudimg.com/raw/14993bbb8ccfe74e7a82d3e4ed2fc3c5.png)
4. Enter the custom policy information. After the settings are completed, click **Add Statement** and **Next** to enter the policy editing page.
![](https://main.qcloudimg.com/raw/245476792d93ce9ec6e9ada61483cc88.png)
   - Effect: allowed
   - Service: API Gateway
   - Action: select involved operations
   - Resource: you can enter `*` to indicate all resources. If only part of resources are involved, you can set this field as instructed in [Resource Description Method](https://intl.cloud.tencent.com/document/product/598/10606).
5. Enter the policy name and edit the policy content (for detailed directions, please see [Policy Syntax](https://intl.cloud.tencent.com/document/product/598/10604)).
6. Click **Create Policy** to create the policy.
7. Bind the created policy to users or user groups (for detailed directions, please see [Associating Policy with User/User Group](https://intl.cloud.tencent.com/document/product/598/10602)).

### Sub-account or collaborator permission management (tagged resource)
Tag is a unified capability in Tencent Cloud. You can set the same tag for different resources in different Tencent Cloud products so that they can have the same operation permissions.
>?The same entry is used for configuring tagged management permissions and non-tagged management permissions. You can create an **Authorize by Tag** policy in **[CAM](https://console.cloud.tencent.com/cam)** > **[Policy](https://console.cloud.tencent.com/cam/policy)**. For detailed directions, please see [Authorizing by Tag](https://intl.cloud.tencent.com/document/product/598/35596).

1. Log in to the **[API Gateway Console](https://console.cloud.tencent.com/apigateway/index?rid=8)** > **[Service](https://console.cloud.tencent.com/apigateway/service?rid=8)**.
2. In the service list, click a service name to enter the service details page and click **Manage API**.
3. On the API management page, click an API ID to enter the API details page. 
4. On the API details page, click the <img src="https://main.qcloudimg.com/raw/2563f681e1be1f3c3e94f590b912ac96.png" style="margin:0;"> icon under "Tags" at the bottom of the page to modify the tags.
![](https://main.qcloudimg.com/raw/da0219260d001fb03cac2d3179f03526.png)
