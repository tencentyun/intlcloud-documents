When Auto Scaling adds or deletes CVM instances, you need to ensure that the traffic of applications is assigned across all the CVM instances. If you want the CVMs added for scale-out to be bound with a specific load balancer and receive the traffic forwarded by the load balancer without your intervention, you can specify a load balancer for the CVMs. In this case, the load balancer will work as the single point of contact for all incoming traffic towards the instances in your Auto Scaling group.

**Binding a load balancer with a scaling group**

Associate a scaling group with a CLB. Instances in the security group will be bound to this CLB for traffic forwarding.

In the Auto Scaling [Console](https://console.qcloud.com/autoscaling), click **New**. Select the load balancer you need from the **Cloud Load Balancer** options at the bottom of the page. Click **New** to create a new CLB if there’re no existing CLBs.

>!The CLB instance associated with the scaling group must be in the same network environment (VPC or the basic network of the same region) as the scaling group.


**Unbinding a load balancer from a scaling group**

Click to go to the details page of the scaling group. Click **Modify** below the details to unbind the corresponding CLB.

Once it is deleted, the CVMs in the scaling group will also be automatically unbound from the deleted CLB.
