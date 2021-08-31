Upon first use of Tencent Cloud Infrastructure as Code (TIC), you must authorize the service to access cloud resources under your Tencent Cloud account for orchestration. Without the authorization, TIC is unable to orchestrate Tencent cloud resources.

TIC supports the following authorization methods:

1. TIC authorization (recommended): based on the built-in service-related role assignment mechanism of Cloud Access Management (CAM), you can orchestrate Tencent Cloud resources through TIC with no need to manage API credentials in TIC. This method is more efficient and secure and meets audit compliance requirements.
2. Managed API credentials (deprecated): you must manage [API credentials](https://console.cloud.tencent.com/cam/capi) (SecretID and SecretKey) in TIC. After TIC encrypts and stores an API credential, it signs requests with the managed API credential to orchestrate cloud resources. This method is available only for existing users who have API credentials managed in TIC.


>The TIC authorization method provides a more efficient and secure permission management mechanism. It is recommended that you switch to the TIC authorization method at the earliest possible time and clear the managed API credentials from TIC.

## Directions

### TIC authorization

#### Enabling TIC authorization

1. Log in to the [TIC console](https://console.cloud.tencent.com/tic).
2. In the left sidebar, choose **Settings** -> **API Credentials** to go to the **API Credentials** page.
3. Click the **TIC Authorization** switch to enable the feature. A message appears prompting you to redirect to the CAM console for authorization.![Enable TIC authorization](https://main.qcloudimg.com/raw/12bfc355259a53d04b0359cd78ffcf23.png)
4. Go to the CAM console to complete authorization.![Complete authorization in CAM](https://main.qcloudimg.com/raw/3e379ef890932bdc3241c29eca4ddc8a.png)
5. Go back to the **API Credentials** page after the authorization is complete. The TIC authorization feature is enabled.![TIC authorization enabled](https://main.qcloudimg.com/raw/76a7856f2743005462b2633e0de29ec7.png)



After TIC authorization is enabled, you can [create a stack](https://console.cloud.tencent.com/tic/stacks/create-stack).

#### Disabling TIC authorization

1. Log in to the [TIC console](https://console.cloud.tencent.com/tic).
2. In the left sidebar, choose **Settings** -> **API Credentials** to go to the **API Credentials** page.
3. Click the **TIC Authorization** switch to disable the feature.![Disable TIC authorization](https://main.qcloudimg.com/raw/ee521f3484cf485af21ed6715c6b0de2.png)
4. This operation cannot be performed if the TIC authorization feature is still being used by a stack. Before you disable TIC authorization, you must manually destroy the stack.![Confirm to disable TIC authorization](https://main.qcloudimg.com/raw/aa92c19e049cb4e8f360d50414c1ce52.png)



>Disabling TIC authorization does not delete the TIC-related role assignment configuration in the CAM console. To delete the TIC-related role assignment configuration in the CAM console, go to the [Roles](https://console.cloud.tencent.com/cam/role) page, find the TIC_QCSLinkedRole role, and then click **Delete** in the **Operation** column.![Delete role assignment configuration in the CAM console](https://main.qcloudimg.com/raw/a9caed0b9a56a129e6cf61eee0328e95.png)

#### Handling authorization failures

If you delete the TIC_QCSLinkedRole role in the CAM console but do not disable TIC authorization in the TIC console, the **Authorization failed** message appears on the **API Credentials** page. Hover over the ![TIC authorization failure icon](https://main.qcloudimg.com/raw/ad9e06421b49df1717643d2e3f161f86.png) icon. The system prompts you to reauthorize TIC.![TIC authorization failure prompt](https://main.qcloudimg.com/raw/4ada396201747261694fd3de2bab2966.png)

Click **Reauthorize** to redirect to the CAM console.![Role assignment in the CAM console](https://main.qcloudimg.com/raw/1bd808ed1c79411e2491390634dc7ab4.png)

After the authorization is complete, the status restores to normal state.![Authorization success](https://main.qcloudimg.com/raw/76a7856f2743005462b2633e0de29ec7.png)

#### Permitted services

TIC is authorized to access the following Tencent Cloud services for orchestration:



>This list is continuously updated. If you want to include a Tencent Cloud service in TIC for orchestration, [submit a ticket](https://console.cloud.tencent.com/workorder/category) to inform the TIC team.

### Managed API credentials (deprecated)

This method is available only for existing users (with managed API credentials in TIC).

#### Clearing API credentials

After you enable TIC authorization, the **Clear** button is displayed. Click this button to delete configuration of all API credentials managed in TIC.

After the API credentials are deleted, existing stacks associated with the API credentials use the TIC authorization method to complete subsequent orchestration operations by default.

>The TIC authorization method does not support cross-account resource orchestration in Tencent Cloud. If you need resource orchestration for other Tencent Cloud root accounts, it is recommended that you retain the managed API credentials to ensure service continuity.

#### Deleting an API credential

Select an API credential and click **Delete**.

>If TIC authorization is enabled, existing stacks associated with the API credential use the TIC authorization method to complete subsequent orchestration operations by default.
>
>If TIC authorization is disabled, API credentials in the Active state cannot be deleted. When a credential is being used by a stack, it cannot be deleted even if it is in the Ready state. To delete such an API credential, you must first destroy the associated stack.

#### Creating an API credential

Click **New**. In the dialog box that appears, complete the following settings:

 - **Name**: enter the name of the API credential.
 - **Provider**: the default provider is Tencent Cloud (only option available).
 - **SecretID** and **SecretKey**: enter the corresponding SecretID and SecretKey. Obtain the SecretID and SecretKey on the [API Keys](https://console.cloud.tencent.com/cam/capi) page.

<!--![](https://main.qcloudimg.com/raw/7e2f57c00d4f4bd7bac10e1b8dfa2fc4.png)-->

>A provider allows only one credential that is in the Active state. When a stack is created, TIC automatically selects the credential in the Active state for API calls.
>
>If TIC authorization is enabled, no additional API credentials cannot be created.
Click **OK** to add the API credential.
