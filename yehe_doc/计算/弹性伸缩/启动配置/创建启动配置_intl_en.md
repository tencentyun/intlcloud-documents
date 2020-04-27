During scale-out, Auto Scaling needs to know in advance the configurations used to produce CVM instances. Therefore, you must predefine related resources such as images, data on data disks, instance configurations, key pairs, security groups, and block storage devices.

A launch configuration is a template based on which instances will be produced during automatic scale-out. **Creating a launch configuration itself will not produce any instances, so it is completely free to use.**

Log in to the [Auto Scaling console](https://console.cloud.tencent.com/autoscaling/config) and click **Launch Configuration** in the left sidebar.

### Step 1. Select a region

On the menu at the top of the page, select a region for your scaling group based on your requirements.

> Select the region of the CVM instances to which you want to bind the scaling group as the launch configuration and the scaling group are both region-based. For example, when the Guangzhou region is specified for the launch configuration, only CVM instances in Guangzhou will be automatically added in the scaling group.
>
![](https://main.qcloudimg.com/raw/014744e64c1b5bb3f251a478baa84540.png)

### Step 2. Specify parameters

1. Click **Create** and follow the instructions to create a launch configuration in the same steps as purchasing a CVM.

1. Enter a **configuration name** such as "frontend server cluster configuration A".

2. Select a model such as 1-core 1G, which means 1-core CPU and 1 GB memory.

3. Select an image. You can either select a clean "public image" or a "custom image" where your application has already been deployed.
To make an instance available directly after creation, we strongly recommend that you deploy your business application in a custom image. **In addition, the application in the image needs to be set to run upon system startup**, so that the instances produced by AS can be automated.

4. Select the capacities of system disk and data disks.
If you want the data disk of the produced instance to have your own data, you can specify a data disk snapshot so that the instance comes with the data in the snapshot upon production.
>
> - Since the instances in a scaling group are generally stateless, we recommend that you load your own data into a custom image for convenience. If the capacity of the system disk is insufficient, you can apply for a larger disk by submitting a ticket.
> - If you want to use the data disk to store data, you need to set it to be automatically mounted, so that scale-out can be unattended. For more information, see [the specific method](https://intl.cloud.tencent.com/document/product/377/4166).
>
5. Select the bandwidth in a similar way of purchasing a CVM instance.

6. Set the username, password, and security group.

7. Click **Confirm**.

8. Create a scaling group based on the launch configuration. The launch configuration determines the instances to be created during scale-out, whereas the scaling group determines when to scale out.
