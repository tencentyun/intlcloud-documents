AS needs to know in advance the configurations used to produce CVM instances during scale-out. Therefore, you should predefine related resources such as images, data on disks, instance configurations, key pairs, security groups, and block storage device.

It is worth noting that a launch configuration is just a template, based on which instances will be produced during automatic scale-out. **Creating a launch configuration itself will not produce any instances, so it is completely free to use.**

Log in to the [AS console](https://console.cloud.tencent.com/autoscaling/config) and click **Launch Configuration** in the navigation pane.

### Step 1. Select a region

On the menu at the top of the screen, select a region for your scaling group as needed.

>Note:
>You should select the region of the CVM instances to which you want to bind the scaling group as the launch configuration and the scaling group are both region-based. For example, if the region selected for the launch configuration is Guangzhou, then only a scaling group in Guangzhou can be bound, and the CVM instances automatically added are also instances in Guangzhou.

![](https://mc.qcloudimg.com/static/img/653ebf516d940a90fd79728e5d319cdc/image.png)

### Step 2. Specify specifications

Click **Create** and follow the on-screen instructions to create a launch configuration in the same steps as purchasing a CVM instance.

1. Enter a **configuration name** such as "front end server cluster configuration A";

2. Select a model such as 1-core 1G, which means 1-core CPU and 1GB memory;

3. Select an image. You can select a clean "public image" or a "custom image" where your application has already been deployed.
In order to make an instance available directly after creation, it is highly recommended that you deploy your business application in a custom image. **In addition, the application in the image should be set to run at system startup**, so that the instances produced by AS can be automated.

4. Select the capacities of system and data disks.
If you want the data disk of the produced instance to have your own data, you can specify a data disk snapshot, so that the instance comes with the data in the snapshot upon production.
> Note:
> - Since the instances in a scaling group are generally stateless, it is recommended that you put your own data into a custom image for convenience. If the system disk is not large enough, you can apply for a larger one by submitting a ticket.
> - If you want to use the data disk to store data, you need to set it to be automatically mounted, so that scale-out can be unattended. For more information, see [here](https://cloud.tencent.com/document/product/377/4166#16.-.E5.90.AF.E5.8A.A8.E9.85.8D.E7.BD.AE.E4.B8.AD.E6.8C.87.E5.AE.9A.E4.BA.86.E6.95.B0.E6.8D.AE.E7.9B.98.E5.BF.AB.E7.85.A7.E8.A6.81.E6.B3.A8.E6.84.8F.E4.BB.80.E4.B9.88.EF.BC.9F).

5. Select the bandwidth just like when you purchase a CVM instance.

6. Set the user name, password, and security group.

7. Click **Finish**.

8. Create a scaling group based on this launch configuration. The launch configuration determines what instances to be created during scale-out, while the scaling group determines when to scale out.
