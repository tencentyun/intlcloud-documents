If you don't want to restrict the permissions of departments and members in your organization, you can disable the service control policy feature.

## Background

After the service control policy feature is disabled, all policies bound to departments and members will be unbound automatically. The policies won't be deleted, but they can no longer be bound to any target objects.
<dx-alert infotype="notice" title="">
Disabling the service control policy feature will affect the permissions of all departments and members in the organization. Perform this operation with caution.
</dx-alert>

## Directions

1. Log in to the [TCO console](https://console.intl.cloud.tencent.com/organization).

2. On the left sidebar, select **Organization account** > **Service control policy**.

3. At the top of the **Service control policy** page, click **Disable service**.

4. Click **OK**. If the status becomes **Control policy disabled**, the feature has been disabled.
<dx-alert infotype="notice" title="">
You can also click **Enable service control** to enable the service control policy feature again. Then, the system policy `FullQcloudAccess` will be automatically bound to all departments and members by default, but custom policies need to be manually bound again.
</dx-alert>