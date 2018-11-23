In the connection example, the IP address ranges of VPC1, VPC2, IDC1 and VPC3 do not conflict. As of the second step, the interconnection among the network instances above has been achieved. You can confirm this by checking the corresponding route table. There should be four routes in the CCN route table:

| Target IP Address Range | State | Next Hop | Next Hop Region | Update Time |
| -------------- | ---- | ----- | -------- | ---- |
| 192.168.1.0/24 | Valid | VPC1 | South China (Guangzhou) | - |
| 10.0.3.0/24 | Valid | VPC2 | East China (Shanghai) | - |
| 10.0.1.0/24 | Valid | Dedicated Connect gateway 1 | North China (Beijing) | - |
| 172.16.1.0/24 | Valid | VPC3 | North China (Beijing) | - |

If the IP address ranges of the associated network instances conflict, an invalid route will be present. Follow the steps below to check:
1. Log in to the [Tencent Cloud Console](https://console.cloud.tencent.com/) and select **Products** > **Cloud Compute & Network** > **Virtual Private Cloud** to enter the VPC Console.
2. Click **Cloud Connect Network** in the left pane to enter the CCN management page.
3. In the CCN list, click the ID of the CCN for which to view the route to enter the details page.
4. Click **Route table** to view the CCN route table.
5. Check whether there is any routing policy in invalid state.
 ![](https://main.qcloudimg.com/raw/b2bb1c45b2229cca4111406189784fa8.png)
6. For more information on how to enable a conflicting route, see [Enabling a Route](/document/product/877/18750).
