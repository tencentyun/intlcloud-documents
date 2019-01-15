
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
![](https://main.qcloudimg.com/raw/a6dfa3c427006fa7e2c8cc9d859ce946.png)
- Select the new subnet in the pop-up subnet replacement page, enter the new primary IP, and click **OK**. Then, the instance restarts to complete the replacement.
![](https://main.qcloudimg.com/raw/d90ebc70733d91d23602e98bb7fd3cf7.png)
>Note:
>
>1. If you have not created a subnet in this availability zone, create a new subnet first.
>2. You can only enter the private IP of the current subnet CIDR.
