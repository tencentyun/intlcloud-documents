## Other Permissions
Hierarchical permission management in **Employee Management** module only applies to Partner Center. To manage permissions for other products, go to the CAM console.

### Directions
1. Go to the [Tencent Cloud website](https://www.tencentcloud.com/account/login).
2. Click **Log In** at the top-right corner to enter the login page.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/9zFj346_121406.png)
3. Enter the root account login information and click **Log In**.
4. Click the profile photo at the top-right corner and click **Access Management**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/vdUV159_121407.png)
5. Add sub-user permissions in the CAM console.
Select an employee account and click **Authorize**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/gSsK589_other_auth.png)
Select non-Partner Center permissions and click **OK**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/ztdn250_121409.png)

| Common Permissions | Description |
| ------------ | ------------------------------------------------------------ |
| QCloudFinanceFullAccess | Permission to access and manage reseller bills and account assets |
| QcloudCollPasswordManageAccess | Permission to manage the console login password |
| QcloudCollApiKeyManageAccess | Permission to manage API keys |

>!
- You can only add non-Partner Center permissions in CAM, but do not directly create or delete users in the CAM; otherwise, there will be a permission management conflict.
- If you have any questions, [submit a ticket](https://console.tencentcloud.com/workorder/category).
