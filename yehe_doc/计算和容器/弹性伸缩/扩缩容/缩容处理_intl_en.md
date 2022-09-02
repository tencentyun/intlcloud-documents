For each scaling group, you can set the time for adding (scale-out) or removing (scale-in) instances. You can scale the scaling group manually by adding or removing instances, or you can enable AS to execute this process automatically by using a scaling policy.


<dx-alert infotype="explain" title="">
- When a scaling group is scaled in automatically, it needs to know which instances should be terminated first, and the selection is based on the removal policy.
- During scale-in, you can prevent specified instances from being terminated by AS by using instance protection.
- For a scaling group configured with a CLB instance, when the instances are automatically or manually removed or deleted, they will be automatically disassociated from the CLB instance.
</dx-alert>




## Removal policy

AS will determine which CVM should be removed based on the removal policy during scale-in. You can choose from the following two removal policies:

- **Remove the oldest instances**: Remove the earliest automatically added instances from the scaling group. Instances added automatically are removed first, followed by the earliest manually added instances.
- **Remove the latest instances**: Remove the latest automatically added CVM instances from the scaling group. Instances added automatically are removed first, followed by the latest manually added instances.


<dx-alert infotype="notice" title="">
Under both of the removal policies, AS will remove automatically created CVM instances before those manually added.
</dx-alert>



## Setting and modifying removal policy in the console
There are two ways to set this up:
- Select the removal policy you want when creating the scaling group.
- On the **Scaling Group Details** page, click **Edit** to modify the scaling policy.

