## Operation Scenarios
Since March 23, 2020, all certificate operations of CLB have been connected to Cloud Access Management (CAM) for authentication. Therefore, when a sub-user account performs CLB certificate operations, if "You are not authorized for this operation. Please contact your developer." is displayed, you can grant certificate permissions to the sub-user account as instructed below.

## Prerequisites
The logged-in account needs to be the root account or a sub-user account with CAM permissions (i.e., associated with the `QcloudCamFullAccess` policy).
>?
>- To check whether the sub-user account has CAM permissions, go to [User List](https://console.cloud.tencent.com/cam) in the CAM Console, enter the details page of the sub-user, and check whether the `QcloudCamFullAccess` policy has been associated.
>- If the `QcloudCamFullAccess` policy is associated, but "No API permissions (message:GetReceiversOnAllType). Please contact your developer." is displayed when the sub-user performs certificate operations, they can ignore and proceed anyway. 

## Directions
Please grant certificate permissions in the following methods:

### Method 1. Associate a custom policy
1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam/overview).
2. On the left sidebar, click **Policies**.
3. Click **Create Custom Policy** and select **Create by Policy Syntax** in the pop-up box.
4. On the "Select Template Policy" page, select **Blank Template** and click **Next**.
5. On the "Edit Policy" page, enter the policy name and enter the following policy content in the "Edit Policy Content" input box:
```
   {
    "version": "2.0",
    "statement": [
        {
            "action": "name/ssl:*",
            "resource": "qcs::ssl:::*",
            "effect": "allow"
        }
    ]
}  
```
6. Then, click **Done** to return to the "Policy" list page.
7. At the top of the "Policy" list page, select **Custom Policy**, find the row of the policy you just created in the list, and click **Associate User/Group** in the "Operation" column.
![](https://main.qcloudimg.com/raw/2a0cf97e6de81cbbc3fcc6af9164bb5a.png)
8. In the pop-up box, select the user to be authorized and click **OK**.
![](https://main.qcloudimg.com/raw/2105e8b1ebf79f0d6b1d063aa0bcd158.png)

### Method 2. Associate a preset policy
1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam/overview).
2. On the left sidebar, select **User** > **User List** to enter the "User List" page.
3. In the row of the sub-user to be authorized, click **Authorize** in the "Operation" bar.
4. In the pop-up box, select `QcloudSSLFullAccess` or `QcloudSSLReadOnlyAccess` and click **OK**.
![](https://main.qcloudimg.com/raw/a18245f729467395f801002f6defcb8d.png)
