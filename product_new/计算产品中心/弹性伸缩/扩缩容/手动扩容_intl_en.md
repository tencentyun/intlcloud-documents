Beside adding and removing instances automatically, AS also allows you to add and remove instances manually.
- [Adding existing CVM instances to a scaling group](#func1)
- [Modifying the desired capacity of a scaling group to implement one-click scale out](#func2)


<span id = "func1"></span>
## Adding existing CVM instances to a scaling group
You can add existing CVM instances to a scaling group manually. 

### Prerequisites
- The instance is in the running status.
- The instance is in the same region as the scaling group.
- The instance and the scaling group must be in the same basic network or VPC.

### Notes
- AS will add the number of instances to be added to the desired capacity of the group.
  For example, if the current desired capacity of your scaling group is 5, and you add 3 instances manually, the desired capacity of your scaling group will become 5 + 3 = 8. If the sum of the number of instances to be added and the desired capacity exceeds the maximum capacity of the group, the request will fail.
- If the scaling group is associated with one or more load balancers,  manually added instances will be automatically associated with these load balancers.
- The scaling group will remove automatically created CVMs first during scale-in. If there are no more automatically-created CVMs, then the manually added CVMs will be removed.
- For manually added instances, when they are removed from the scaling group, they will be unbound with the CLB and will not be terminated.

### Manually adding instances in console
1. Log in to the [Scaling Group Console](https://console.cloud.tencent.com/autoscaling/group), and click the ID of the scaling group to which you want to add an instance.
2. Go to the scaling group details page. Select **Associate Instances** -> **Add an Instance**. This is shown in the following figure:
![](https://mc.qcloudimg.com/static/img/7fab080a771cd36a18cd669a6e6cf78b/1.jpg)
3. In the dialog box, check the corresponding instance, and click **OK**. This is shown in the following figure:

<span id = "func2"></span>
## Modifying the desired capacity to scale out quickly
### Scenarios
For the following scenario, we recommended to use launch configuration as instructed in [Scale-out with Launch Configuration](#step1). You can complete CLB forwarding rules, CVM configurations and business deployment in advance, and then you can modify the parameters of the scaling group to rapidly complete scale out.
- It’s hard to predict your business traffic, but you do not want to leave the scaling decisions entirely to the system. If the business fluctuations are predictable, see [Managing scheduled actions](https://intl.cloud.tencent.com/document/product/377/3591).
- Your computing needs are based on projects, and the CVMs to be used every time are similar. For example, this may involve collection of social conditions and public opinions, sequencing of genes, or prediction of weather.


<span id = "step1"></span>
### Scale-out with Launch Configuration
Execute the following steps to configure a CVM template as the launch configuration, and to configure the corresponding scaling group.

1. Create a custom image. For more information, see [Creating a custom image](https://intl.cloud.tencent.com/document/product/213/4942).
 >
 >- Instances added later for scale-out will be configured using this image.
 >- Suggested steps to create a custom image: You can deploy your services on an existing CVM or a new CVM, set the services to be launched on the boot of the operating system, and create a custom image.
2. For information about creating a launch configuration based on this custom image, see [Creating a launch configuration](https://intl.cloud.tencent.com/document/product/377/8544).
3. [Create a scaling group](https://intl.cloud.tencent.com/document/product/377/8551).
During the creation process, select the created launch configuration. Enter the minimum capacity, maximum capacity, and initial capacity of the cluster as required by your business.
4. After you complete the preceding steps, when the business needs to scale out, you can modify the scaling group configurations to raise the minimum capacity, the maximum capacity, and the desired capacity, and the AS will rapidly perform scaling.






