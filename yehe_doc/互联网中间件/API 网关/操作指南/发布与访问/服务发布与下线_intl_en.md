## Operation Scenarios
Once APIs are configured in a service, the service can be published. The system will use the system time as the release log to facilitate release rollback as needed.

## Directions
#### Service release
1. Log in to the **[API Gateway Console](https://console.cloud.tencent.com/apigateway/index?rid=1)** and click **Service** on the left sidebar.
2. Select the name of the service to be published from the service list and click **Publish** in the "Operation" column.
![](https://main.qcloudimg.com/raw/d98a258c46ebcb0992c73ff08e669b03.png)
3. Select the release environment and enter remarks.
 - Release environment: currently supported environments include test, pre-release, and release.
 - Remarks: this field can contain up to 200 characters, which is required.
4. Click **Submit**.

#### Service deactivation
>
>- After a service is deactivated, it cannot be accessed externally.
>- Unpublished services cannot be deactivated.

After a service is published to a specific environment, if you want to unpublish it, click **Deactivate** in the "Operation" column on the environment management page.
![](https://main.qcloudimg.com/raw/0e22f36c56debe792c348410ae878e48.png)
