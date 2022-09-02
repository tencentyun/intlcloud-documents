When AS adds or removes CVM instances, you need to ensure that application traffic is distributed across all CVM instances. If you want the added CVM instances to be bound to a specific CLB instance and receive the traffic forwarded by that CLB instance without your intervention, you can specify a CLB instance for the CVM instances. In this case, the CLB instance will work as the single point of contact for all traffic to the instances in your scaling group.

## Adding an CLB Instance to a Scaling Group

The scaling group is integrated with CLB instances, so that you can add CLB instances to an existing scaling group. A CLB instance added to a scaling group automatically registers instances in the group and distributes inbound traffic among them. In addition, automatically or manually added instances will be automatically mounted to and unmounted from the CLB instance after being removed or deleted.

1. Log in to the AS console and select **[Scaling group](https://console.cloud.tencent.com/autoscaling/group?rid=1)** on the left sidebar.
2. On the **Scaling group** list page, click **Create**.
3. In the **Load Balancer Configuration** step of **Create scaling group**, select the target CLB instance. If you have not created one, click **Create** under the option to create one.
<dx-alert infotype="notice" title="">
A scaling group and its associated CLB instance (in the case of a cross-region CLB instance, its backend VPC) must be in the same network environment (VPC or the classic network in the same region).
</dx-alert>



## Deleting a CLB Instance from a Scaling Group

On the "Scaling Groups" page, click a scaling group ID to go to the details page of the corresponding scaling group. You can delete the corresponding CLB in the "CLB Information" module.
<dx-alert infotype="notice" title="">
Once it is deleted, the CVMs in the scaling group will also be automatically unbound from the deleted CLB.
</dx-alert>




