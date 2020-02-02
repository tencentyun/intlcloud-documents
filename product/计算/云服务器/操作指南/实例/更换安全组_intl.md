## Scenario

Security group is a stateful virtual firewall for filtering packets and is used to set the network access controls for a single or multiple CVMs. It is a logical grouping and an important means of network security isolation. When a CVM instance is created, you must configure the security group for it. Tencent Cloud supports configuring a new security group for the CVM instance after it is created.


>**Note:**
>To configure a new security group for the instance, create a security group first. 


## Steps

- Log in to [CVM Console](https://console.cloud.tencent.com/cvm/index), and select the instance to be assigned to the new security group.
- Click **More** on the right, and then click **Configure Security Group**.
- Enter the security group configuration page, and select the name of the new security group (multiple names can be selected), and click **Confirm**.
- Another way is to select the instance and click **More actions** > **Add to security group** to get into the configuration page.

>**Note:**
>You can only bind a security group in the same project and region as CVM.


- You can also enter the instance details page, click **Security Groups** tab > **Bind** to bind the security group.
- Enter the security group configuration page, and select the name of the new security group (multiple names can be selected), and click **OK** to replace the security group.
