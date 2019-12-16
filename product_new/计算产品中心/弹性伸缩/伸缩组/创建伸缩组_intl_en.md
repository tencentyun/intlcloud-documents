Log into [Auto Scaling Console](https://console.cloud.tencent.com/autoscaling/config), and select **Scaling Group** in the left sidebar.

### 1. Select a region

In the upper part of the console, select the target region. CVM instances and CLB instances must be the same region as the one specified for the launch configuration. For example, if Guangzhou is specified for the launch configuration, only CVM instances in Guangzhou will be automatically added to the scaling group. For a scaling group in Guangzhou, you cannot add CVM instances or bind CLB instances in any region (e.g., Shanghai, Beijing, Hong Kong (China), Toronto) other than Guangzhou.

![](https://main.qcloudimg.com/raw/950695bd0e5b50414e929c414fa198b2.png)

### 2. Complete configuration
Click **New** and configure the scaling group:

  - **Scaling Group Name**: identifies the scaling group. For example, **Website Logic Layer**.
  - **Min Capacity**: defines the minimum number of instances in the scaling group
  - **Initial Capacity**: defines the number of **automatically** created instances at the startup of the scaling group. The corresponding number of instances will be created upon the establishment of the scaling group.
  - **Max Capacity**: defines the maximum number of instances in the scaling group
  - **Launch Configuration**: defines the launch configuration. CVMs will be created according to this configuration when scale-out operations are performed.
  - **Supported Networks**: the network attribute of the scaled-out CVMs, that is, whether the scaled-out CVMs are in the basic network or a VPC. Choose **Basic Network**, unless your cluster already uses VPC.
  - **Supported Availability Zones**: defines in which availability zone the CVM will be automatically created during scale-out operations. You can select multiple availability zones. The scaled-out CVMs will be automatically created randomly in the selected availability zones, implementing cross-availability zone disaster recovery.
  - **Removal Policy**: identifies which CVMs should be removed first when AS needs to remove instances from the scaling group for scale-in. Usually, you can select **Remove the oldest instances**. For more information, view the [details](https://intl.cloud.tencent.com/document/product/377/4166) of the two types of policies.
  - **Cloud Load Balancer**: specifies a Cloud Load Balancer. CVMs created in the scale-out event will be automatically mounted to this CLB.

The scaling group is now created. To implement auto-scaling, you need proceed with the following 3 operations:
 - Add existing CVMs
 - Create scaling policies
 - Create notification policies
