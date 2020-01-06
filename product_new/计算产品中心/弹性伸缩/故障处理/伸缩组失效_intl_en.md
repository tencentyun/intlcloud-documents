## Problem Description
When you cannot create a CVM manually or through AS due to insufficient balance and other reasons, or you accidentally delete the resources associated after creation (such as Load Balancers and VPC). Scaling group invalidation is a mechanism to identify risks in advance, which helps avoid any scale-out failures when you need to scale-out, greatly improving the security of your cluster.


## Problem Analysis
View the status of scaling groups in the [Scaling group list](https://console.cloud.tencent.com/autoscaling/group). If <img style="margin:-3px 0;" src="https://main.qcloudimg.com/raw/653cff66183ba681f01873603de9eda6.png"> is displayed, it indicates that the scaling activity is in **exceptional** status. At this time the scaling group is no longer available.
>?Mouse-over the icon to view the cause of the exception.
>


## Exception causes
 - [Launch configuration exceptions](#startConfig)
 - [Cloud Load Balancer exceptions](#load)
 - [VPC exceptions](#vpc)
 - [Insufficient balance](#balance)


## Troubleshooting

<span id="startConfig"></span>
### Launch configuration exceptions
**Problem:** if the launch configuration displays a failure, the reason is that the resource (image, snapshot, security group, etc.) that is associated with the launch configuration has been deleted.
**Solution:** click the launch configuration ID in the row where the scaling group is located to go to the corresponding launch configuration details page and view whether the resources have been deleted. 


<span id="load"></span>
### Cloud Load Balancer exceptions
**Solution:** click **Cloud Load Balancer** in the row where the scaling group is located to go to the corresponding Cloud Load Balancer details page and view the specific circumstances. This includes the listener, domain name, and URL path. 

<span id="vpc"></span>
### VPC exceptions
**Solution:** click **Network** in the row where the scaling group is located to go to the corresponding VPC details page and view the specific circumstances. This includes the subnet, route table, and so on. 


<span id="balance"></span>
### Insufficient balance
**Solution:** the account does not have sufficient funds to pay for the scaled out resources, leading to the failure of the scaling activity. You must promptly top up your account to restore the scaling group activity status. 



## Impact of scaling group invalidation
Scaling groups do not stop working immediately after becoming invalid:
- Normal scale-in activities will not be affected.
- The limits on max capacity, min capacity, and desired capacity will still be applicable.
- Scale-out activities will stop, as your environment no longer meets the conditions for creating CVMs.
