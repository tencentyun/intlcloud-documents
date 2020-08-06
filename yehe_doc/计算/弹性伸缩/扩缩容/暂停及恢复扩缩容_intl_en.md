## Use Cases

If you need to troubleshoot any problems related to configurations or Web applications (for example, shutdown to reset a password and upgrade services), and you want to modify the applications without triggering the auto scaling process, you can disable the scaling group and recover it after troubleshooting.

## Suspending a Scaling Group

### Directions
1. Log in to the Auto Scaling console and select **[Scaling Groups](https://console.cloud.tencent.com/autoscaling/group)** in the left sidebar.
2. On the “Scaling Groups” page, click **Disable** on the right side of the row of the scaling group to be disabled and click **OK** in the pop-up window.
Then, you can see that the scaling group is in “Disabled” status, as shown in the following figure:
![](https://main.qcloudimg.com/raw/d34a4b7ad48d5d23620d3e9dbd4afa5e.png)


### Considerations

After you disable a scaling group, the automatic capacity scaling of the scaling group will not be triggered, but the restrictions on the scaling group remain in effect.

- Automatically triggered activities include:
	- Alarm-based scaling
	- Scheduled actions
	- Health checks
	- The desired number of instances does not match the desired capacity due to manual operations.
	
- Scaling group restrictions include:
	- If manual removal causes the number of instances in the group to be less than the min capacity, removal will not be permitted.
	- If manual addition causes the number of instances in the group to be more than the max capacity, the addition will not be permitted.
	- Manually increasing the min capacity or the max capacity does not trigger scaling activity.

## Recovering a Scaling Group

If you have finished troubleshooting, you can recover the auto scaling configuration.

1. Log in to the Auto Scaling console and select **[Scaling Groups](https://console.cloud.tencent.com/autoscaling/group)** in the left sidebar.
2. On the **Scaling Groups** page, click **Enable** on the right side of the row of the scaling group to be enabled, as shown in the following figure:
![](https://main.qcloudimg.com/raw/216fbb71a440af2e1453537531cc0cc1.png)




