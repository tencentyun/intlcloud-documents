## Scenario

Tencent Cloud provides basic networks and VPCs for different scenarios. Various features are offered to help you flexibly manage your networks.
- Switch between networks:
 - Switch from a basic network to a VPC: Tencent Cloud allows you to switch a CVM instance from a basic network to a VPC and batch switch CVM instances from basic networks to a VPC.
 - Switch between VPCs: Tencent Cloud allows you to switch one or more CVM instances from VPC A to VPC B at a time.
- Specify a custom IP address.
- Choose to retain the HostName.

## Notes

- When you batch switch multiple CVM instances between networks, the selected CVM instances must be located in the same availability zone.
- Before migration, unbind the CVM instance or instances from the CLB and ENI in the private and public networks and release the secondary IP address of the primary ENI. Rebind them after the migration.
- During the migration, the CVM instance or instances need to be restarted. Therefore, do not perform other operations.
- After the migration, please check whether the CVM instance or instances are running normally and can be accessed via a private network and logged in to remotely.
- Switching from a basic network to a VPC is irreversible. A CVM instance cannot communicate with CVM instances in basic networks after being switched from a basic network to a VPC.

## Procedure

1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. On the Instances page, find the CVM instance to be switched between networks. In the Actions column, click **More** and then choose **Resource Adjustment** > **Switch VPC**.
> To switch the VPCs of multiple CVM instances in a batch, select the CVM instances to be switched, click **More actions** at the top of the page and then choose **Resource Adjustment** > **Switch VPC**.
3. In the **Switch VPC** window that appears, read the notes and then click **Next**.
4. Select the destination VPC and the corresponding subnet and then click **Next**.
5. In the selected subnet section, specify the pre-assigned IP address and the HostName options as required and then click **Next**.
>
> - If no pre-assigned IP address is specified, the system will automatically assign an IP address.
> - When specifying the HostName options, you can select **Reset HostName** or **Retain original HostName of the instance**.
> 
6. Perform operations according to the instructions on the **Shutdown CVM** page and then click **Start Migration**. After the migration is complete, you can log in to the CVM console, and on the Instances page, you will see **Modifies instance VPC attributes** is displayed in the Status column of the instances to be switched.
![](https://main.qcloudimg.com/raw/759d34a61cc6b0d1e430525e3283d43b.png)
