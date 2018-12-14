1. Log in to the [Tencent Cloud Console](https://console.cloud.tencent.com/) and select **Products** > **Cloud Compute & Network** > **Virtual Private Cloud** to enter the VPC Console.
2. Click **Cloud Connect Network** in the left pane to enter the CCN management page.
3. In the CCN list, click the ID of the CCN for which to associate a network instance to enter the details page.
4. On the new instance page, click **Associate an instance**. 
 ![](https://main.qcloudimg.com/raw/f9144c1abc4992ea20b0328d97850a43.png)
5. - In the pop-up box, select the network instance type, region and the specific instance to be associated.
For example, for subnet B (10.0.3.0/24) in VPC2 in Shanghai, select **VPC**, **South China (Shanghai)** and VPC2. 
 ![](https://main.qcloudimg.com/raw/a76cafac390b4c1f35b196ba59f0d72a.png)
 - (Optional) If you need to associate another network instance, click **+ New**.
For example, for IDC1 (10.0.1.0/24) in Beijing connected to Direct Connect gateway 1, select **Direct Connect Gateway**, **North China (Beijing)** and Direct Connect gateway 1; for VPC3 in Beijing, do the same.
6. Click **New** to add the selected network instance to CCN.
![](https://main.qcloudimg.com/raw/7528bacba53705d8846f45b6b7cd9330.png)
