For each scaling group, you can control the time to add instances (scale-out) to it or delete instances (scale-in). You can scale the scaling group manually by adding or removing instances, or can allow AS to execute this process automatically by using a scaling policy.

When the scaling group is scaled in automatically, it needs to know which instances should be terminated first, and the selection is based on the removal strategy.

During scale-in, you can prevent specified instances from being terminated by AS by using instance protection.

## Removal policy

AS will determine which CVM should be removed based on the removal policy during scale-in. You can choose from the following two removal policies:

- **Remove the oldest CVMs**: Remove the oldest auto-added CVMs first, and when there are no more auto-added instances, remove the oldest manual-added CVMs.
- **Remove the newest CVMs**: Remove the latest auto-added CVMs first, and when there are no more auto-added CVMs, remove the latest manual-added CVMs.

> Note: No matter whether it is the newest or oldest servers to be deleted, AS will delete the automatically created CVMs first, and then delete manually added CVMs.

## Setting and modifying removal policy in the console
There are two ways to set this up:
- Select the removal policy you want when creating the scaling group.
- In the details page of scaling group, click **Edit** to modify the scaling policy.

