After you authorize your Grafana instance with a service role, it can access corresponding APIs with the temporary key of the service role. Do not enter sensitive `SecretID`/`SecretKey`; otherwise, the data security may be compromised.


## Prerequisites
1. Log in to the [TCMG console](https://console.cloud.tencent.com/monitor/grafana).
2. In the instance list, find the target instance and click **Instance ID**.
3. On the instance details page, click **Tencent Cloud Service Integration** in the list on the left.

## Directions

Click the **service role editing** icon in the top-right corner of the **Tencent Cloud Service Integration** page to configure a service role for the current instance.
![](https://qcloudimg.tencent-cloud.cn/raw/6db484aa599d544337be516691776007.png)

### Selecting service role
1. Click the **Service Role** drop-down list, and eligible service roles will be automatically loaded.
2. Select a preconfigured or self-created service role. Different Tencent Cloud services have different requirements for service role permissions, and you can create service roles as needed.
3. Click **Save**, and the instance will be rebooted.
   ![](https://qcloudimg.tencent-cloud.cn/raw/743cd3716f41ebed9ee89911627b40ad.png)

### Creating service role
For demonstration purposes, this section uses the preconfigured `ReadOnlyAccess` policy as an example. You can view the policies required by Tencent Cloud services at the end of this document and configure read-only access as needed.
1. Go to the [CAM > Role](https://console.cloud.tencent.com/cam/role) page.
2. Click **Create Role** in the top-right corner and select **Tencent Cloud Product Service** in the pop-up window.
3. In the **Enter role entity info** step, select **Cloud Virtual Machine (CVM)** and click **Next**.
4. In the **Configure role policy** step, search for and select **ReadOnlyAccess** and click **Next**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/149a16795b761a113008410c18317588.png)
5. Preview the custom role, name it, and click **Complete**.

### Policies required by Tencent Cloud services
#### Policies required by TCMG plugins

| **Policy Description**                            | **Policy Name**                       |
| ----------------------------------- | --------------------------- |
| Read-Only access to CM       | QcloudMonitorReadOnlyAccess |
| Read-Only access to CVM resources | QcloudCVMReadOnlyAccess     |
| Read-Only access to CLS         | QcloudCLSReadOnlyAccess     |


####  Policy required by CLS

| **Policy Description**                            | **Policy Name**                       |
| --------------------------- | ----------------------- |
| Read-Only access to CLS         | QcloudCLSReadOnlyAccess     |
