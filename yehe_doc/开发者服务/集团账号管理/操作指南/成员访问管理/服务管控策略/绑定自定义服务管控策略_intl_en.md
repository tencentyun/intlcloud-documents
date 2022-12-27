You can bind a custom service control policy to departments or members, which will be controlled by it immediately. Make sure that the result of the binding operation is as expected to avoid affecting the normal business operations.

## Background

1. The system binds the system policy `FullQcloudAccess` to the resource folders and members by default.

2. A service control policy takes effect for the entire bound node; that is, a policy bound to a parent department also takes effect for child departments and their members.

## Directions

1. Log in to the [TCO console](https://console.intl.cloud.tencent.com/organization).

2. On the left sidebar, select **Organization account** > **Service control policy**.

3. Click the name of the target policy to enter the policy details page and select **Binding management**.

4. Click **Bind**. In the pop-up window, select the target departments or members.

5. Click **OK**.