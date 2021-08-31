When Auto Scaling (AS) adds or deletes CVM instances, you need to ensure that app traffic is distributed across all CVM instances. If you want the scaled-out CVMs to be bound with a specific load balancer (LB) and receive the traffic forwarded by that LB without your intervention, you can specify an LB for the CVMs. In this case, the LB will work as the single point of contact for all inbound traffic towards the instances in your Auto Scaling group.

### Binding an LB to a Scaling Group

Integrate scaling groups with Cloud Load Balancer (CLB) so you can bind a CLB instance to an existing scaling group. After the CLB instance is bound, it automatically registers the instances in the scaling group and distributes inbound traffic to these instances.

1. Log in to the [Auto Scaling console](https://console.cloud.tencent.com/autoscaling/group?rid=1) and click **Scaling Groups** in the left sidebar.
2. On the "Scaling Groups" page, click **Create**.
3. In the "CLB configuration" step of creating a scaling group, select the desired CLB. If no CLBs are available, click **Create** under the option to create one.
>A scaling group and its associated CLB instance (in the case of a cross-region CLB instance, its backend VPC) must be in the same network environment (the same VPC instance or the basic network in the same region).
>

### Unbinding a CLB from a Scaling Group

On the "Scaling Groups" page, click a scaling group ID to go to the details page for the corresponding scaling group. You can delete the corresponding CLB in the "CLB Information" section.

Once the CLB is deleted, CVMs in the scaling group will also be automatically unbound from the deleted CLB.
