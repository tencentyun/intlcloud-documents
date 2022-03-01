## Error Description
Two VPCs are connected through CCN, but a ping failure occurs.

## Common Causes
- The two VPCs' subnet IP ranges conflict.
- There is a container route.

## Troubleshooting
1. Log in to the [CCN console](https://console.cloud.tencent.com/vpc/ccn).
2. Click a CCN instance ID to enter the details page.
3. Click the **Route Table** tab to check the route status.
  + If there is a failed route, it means that the two VPCs have subnets with the same CIDR block, resulting in a CCN routing conflict. You need to delete the subnets with the same CIDR block and use subnets with different IP ranges.
  + If the routes are normal, proceed to [Step 4](#step4).
    ![]()
4. <span id="step4">Enter the [CVM console](https://console.cloud.tencent.com/cvm/instance/index?rid=16), click **Login** on the right of a CVM instance, enter the password or key as prompted to log in to the instance in the [standard method](https://intl.cloud.tencent.com/document/product/213/5436), and run `route` to view the internal route table of the system.
5. Check whether there is a Docker container route in the system with the same IP range as the subnet of the opposite CVM instance.
  + If so, the container route will conflict with the VPC route. In this case, the system will choose the container route preferably, resulting in a failure to access the other instance. You should use a subnet with another IP range or modify the container IP range to solve this problem.
  + If not, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>?When a CVM instance in a VPC uses the container service, and the container IP range is the same as the subnet IP range, access to other CVM instances in the same VPC may be blocked, which is also caused by the container route conflict. Therefore, you should plan IP ranges appropriately.
>
 ![](https://qcloudimg.tencent-cloud.cn/raw/d539f8bd7364e7bd6edd0b0521be3a00.png)
