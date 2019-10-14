## Scenario

Tencent Cloud offers basic network and VPC, both of which provide quality services for users. On top of that, we provide more  
services, enabling you to manage the network more flexibly.
- Switching between networks
 - Switching from basic network to VPC: you can switch the network from basic network to VPC for a single CVM or multiple CVMs all at once.
 - Switching from VPC A to VPC B: you can switch the network from VPC A to VPC B for a single CVM or multiple CVMs all at once.
- Setting up a custom IP
- Choosing whether to keep HostName

## Notes

- When you switch the network for multiple CVMs all at once, the selected CVMs must be in the same availability zone.
- Before the migration, please unbind the CVM(s) from the internal and external network LB and ENI, and release the secondary IP of the primary ENI. You can rebind them after the migration.
- During the migration, the host instance needs to be restarted. Do not perform other operations.
- After the migration, please check whether the instance(s) is/are running normally and whether you are able to access the CVM(s) via the private network and log in to the CVM(s) remotely as usual.
- You can only switch from basic network to VPC, not the other way around. After you switch the network from basic network to VPC for your CVMs, they will not be able to communicate with cloud services in basic networks.

## Directions

### Preparing for the migration

1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. On the Instance page, select the instance for which you want to switch the network, click **More** in the Operation column on the right, and select **Resource Adjustment** > **Switch to VPC**.
> For switch the network for multiple CVMs, you can check the instances, click **More actions** at the top of the instance list, and select **Switch to VPC**.
3. Read the notes in the “Switch to VPC” window and click **Next** as shown below:
![](https://main.qcloudimg.com/raw/8f8172cda0a654d18b3303596a63c794.png)

### Selecting Network

Select a VPC and a subnet and click **Next** as shown below:
![](https://main.qcloudimg.com/raw/bfe73130809f1d7a65eb9e6438bfedd3.png)

### Setting IP and HostName

Set a pre-allocated IP address in the selected subnet and set the HostName options according to actual needs as shown below:

> - If you do not set a pre-allocated IP address, the system will automatically allocate one.
> - When configuring the HostName options, you can choose to reset the instance HostName while switching to the VPC or keep the original HostName.
> 
![](https://main.qcloudimg.com/raw/fa8818d58bcf9d999e2f43e5798ad9cc.png)

### Starting migration

Click **Start Migration**, and on the instance list page you will see the status of instance is "Modify instance’s VPC attribute" as shown below:
![](https://main.qcloudimg.com/raw/759d34a61cc6b0d1e430525e3283d43b.png)





