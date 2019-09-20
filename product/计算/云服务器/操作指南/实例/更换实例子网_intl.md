
The subnet of the CVM instance in VPC can be directly replaced in the console.

## Limits

- The associated CVM restarts automatically after its subnet is replaced.
- The subnet cannot be replaced for the secondary ENI.

## Procedure

- Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).
- Select a region.
- Click the ID of the instance to go to its details page.
- On the instance details page, click **ENI**, and then click the ID of primary ENI.
![](https://main.qcloudimg.com/raw/b465681aa6adf81c66bc81c41580bcd9.png)
- Go to the primary ENI details page, and click **Replace Subnet**.
![](https://main.qcloudimg.com/raw/713d6383b128a66ae25f5342a7387631.jpg)
- Select the new subnet in the pop-up subnet replacement page, enter the new primary IP, and click **OK**. Then, the instance restarts to complete the replacement.
![](https://main.qcloudimg.com/raw/58c3534b2d6c9da255c5a32bbde8a4c1.png)
>Note:
>
>1. If you have not created a subnet in this availability zone, create a new subnet first.
>2. You can only enter the private IP of the current subnet CIDR.
