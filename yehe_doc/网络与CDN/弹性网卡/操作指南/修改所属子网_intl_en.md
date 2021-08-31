>!
>- You can only change the subnet of a primary ENI.
>- You must unbind all secondary IPs before you change the subnet of an ENI.
>- You can only change the subnet of an ENI to another subnet within the same availability zone.
>- Changing the subnet will automatically restart the associated instance and cause business interruption for about 30 seconds, so proceed with caution.

1. Log in to the [VPC Console](https://console.cloud.tencent.com/vpc).
2. Choose **IP and ENI** -> **ENI** in the left sidebar to go to the ENI list page.
3. Locate the ENI you want to change the subnet, and click its ID/Name to enter the details page.
4. In the **Basic Information** tab, click **Change Subnet** next to **Subnet**.
![](https://main.qcloudimg.com/raw/ca351583b467976fd2ba29aef1dd17fa.png)
5. Select the subnet you want to use and specify a new primary IP in the pop-up window.
![](https://main.qcloudimg.com/raw/8fbc63af36c9e65b6d4ea185f45c3b17.png)
5. Click **OK**.
