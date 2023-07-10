
The sub-account Developer of the master account CompanyExample needs to have permission to access the embedded Tencent Cloud console CLS page.

>?CLS allows you to embed the [CLS Console](https://console.cloud.tencent.com/cls) into an external system (such as an OPS or business system) so you can conduct log search and analysis without logging in to Tencent Cloud console.

## Preparations

1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam) and create the sub-account Developer. For more information, see [Creating a Custom Sub-user](https://intl.cloud.tencent.com/document/product/598/13674).
2. Click **Custom Create** on the **Create User** page to select **Access Resources and Receive Messages** for **User Type**.
3. Click **Next** to configure user information. Check **Programming access** and **Tencent Cloud console access**.

## Directions

You need to perform 3 steps: use master account CompanyExample to create a custom role and a custom policy, and associate the policy with the sub-account.

1. Use master account CompanyExample to create a custom role
 1. On the **Roles** page, click **Create Role**.
 1. In the pop-up window, select **Tencent Cloud Account** as the role entity.
 4. In the **Enter role entity info** tab, check **Current root account** and **Allow the current role to access console**.
 1. In the **Configure role policy** tab, select the policies you want to associate with the role, or directly click **Next**.
 1. Enter the role name (such as ClsBuildInRole), review the information, and click **Done**.
      
2. Use master account CompanyExample to create a custom policy for the embedded console permission.
 1. On the **Policies** page, click **Create Custom Policy**.
 1. In the pop-up window, click **Create by Policy Syntax**.
 1. Check **Blank Template** for **Select Policy Template**, and click **Next**.
 1. Enter information in **Policy Name** (such as ClsBuildInStrategy), **Description** and **Policy Content**, and click **Done**.
>?You can fill in **Policy Content** by referring to the sample syntax below. **Replace `uin` with the master account UIN, and `rolename` with the role (such as ClsBuildInRole) created in Step 1.

   ```
   {
       "version": "2.0",
       "statement": [
           {
               "effect": "allow",
               "action": [
                   "name/sts:AssumeRole"
               ],
               "resource": [
                   "qcs::cam::uin/100001234567:roleName/ClsBuildInRole"
               ]
           }
       ]
   }
   ```

3. Associate the custom policy with the sub-account
 1. On the **Policies**, search by **Policy Name** (such as ClsBuildInStrategy) to locate the policy that you want to associate with the sub-account.
 5. Click **Associate** in the **Action** column on the right.
 1. In the pop-up window, select the sub-account Developer and click **Confirm**. You can also click **Authorize** on the **User List** page to associate the policy. For more information, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).
