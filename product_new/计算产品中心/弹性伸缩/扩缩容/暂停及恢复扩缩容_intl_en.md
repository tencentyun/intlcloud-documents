## Use cases

If you need to troubleshoot any problems related to configurations or Web applications (for example, shutting down to reset a password, upgrade services, etc.), and you want to modify the applications without triggering the auto scaling process, you can disable the scaling group and recover it after troubleshooting.

## Suspending a scaling group

### Operations

Open the [Auto Scaling Console](https://console.cloud.tencent.com/autoscaling/config), and select **Scaling Group** in the navigation bar. Click **Disable** on the right of the scaling group list.

![](https://main.qcloudimg.com/raw/d34a4b7ad48d5d23620d3e9dbd4afa5e.png)

When this setting has been implemented, you will see **Disabled** in the **Status** column.

### Considerations

When you disable an AS group, the automatic capacity scaling of the scaling group will not be triggered, but the restrictions on the scaling group remain in effect.

Automatic triggered activities include:
- Alarm-based scaling
- Scheduled tasks
- Health checks
- The desired number of instances does not match the desired capacity due to manual operations

Scaling group restrictions include:

- If manual removal leads the number of instances in the group to be less than the min capacity, the removal will not be permitted.
- If manual addition leads the number of instances in the group to be more than the max capacity, the addition will not be permitted.
- Manually increasing the min capacity or the max capacity does not trigger scaling activity.

## Recovering a scaling group

If you have finished troubleshooting, you can recover the auto scaling configuration.

Open the [Auto Scaling Console](https://console.cloud.tencent.com/autoscaling/config), and select **Scaling Group** in the navigation bar. Click **Enable** on the right of the scaling group list.

![](https://main.qcloudimg.com/raw/216fbb71a440af2e1453537531cc0cc1.png)




