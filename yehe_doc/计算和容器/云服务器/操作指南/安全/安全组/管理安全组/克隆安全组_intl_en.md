## Scenario
You might need to clone a security group if you:
- Have created a security group sg-A in region A and you want to apply the same rules to an instance in region B. You can clone sg-A to region B, instead of creating a new security group from scratch.
- Need a new security group for your service but want to clone the old security group as a backup.



## Considerations
- By default, when you clone a security group, only the rules are cloned, not the association with instances.
- You can clone a security group across projects and regions.

## Directions

1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. In the left sidebar, select **[Security Group](https://console.cloud.tencent.com/cvm/securitygroup)**. The Security Group page then appears.
3. Select desired region. A list of security groups under the region then appears.
4. Locate the desired security group and click **More**. Then click **Clone**. The **Clone security group** page then appears.
5. Select a **Target region** and **Target project** and input a **New name** for the new security group. Click **OK**.






