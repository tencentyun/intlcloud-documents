You can modify the private IP of a CVM instance in the VPC directly on the console or by changing the subnet of the CVM instance. For more information on how to change the subnet, please see [Change Subnet]().

## Limits

- Changing the primary IP of a primary ENI may cause a restart of associated CVM.
- The primary IP of a secondary ENI cannot be modified.

## Procedure

- Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
- Select a region.
- Click the ID of the instance to go to its details page.
- On the instance details page, click **ENI** -> **Modify Primary IP**.
![](https://main.qcloudimg.com/raw/4c645d0804f51e263080ca5bebd13d3a.png)
- Enter a new IP in the pop-up window and then click **OK**. It takes effect after the instance is restarted.
![](https://main.qcloudimg.com/raw/63be3d8152f3f27c114c4354340bed5d.png)
>Note: You can only enter the private IP of the current subnet CIDR.
