## Operation Scenario
You may need to clone a security group in the following scenarios:
- You have created a security group named sg-A in region A and want to apply sg-A rules to instances in region B. In this case, you can clone sg-A to region B instead of creating another security group in region B.
- Your business needs to execute a new security group rule. In this case, you can clone the original security group for backup.



## Notes
- By default, only the inbound and outbound rules of a security group are cloned, but not the instances associated with the security group.
- Security groups can be cloned between projects or regions.

## Steps

1. Log in to [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. In the left sidebar, click **[Security Group](https://console.cloud.tencent.com/cvm/securitygroup)** to enter the security group management page.
3. On the security group management page, choose **Region** and locate the row of the security group to be cloned.
4. In the operation column, click **More** > **Clone**.
5. In the "Clone Security Group" window that appears, select **Target Project** and **Target Region** for the cloning, enter a **New Name** for the security group, and click **OK**.






