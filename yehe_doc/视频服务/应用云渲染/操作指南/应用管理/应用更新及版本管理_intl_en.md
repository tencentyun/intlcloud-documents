CAR offers version management capabilities. Under the same application ID, you can maintain up to **five** versions and perform operations such as new version upload and release as well as version rollback.

## Application version Update[](id:update)

>? During application update, make sure that the application startup path is the same as that of the original application package; otherwise, you need to modify the startup parameter configuration. The URL must be a URL that can be accessed and trigger download directly. Download URLs of cloud disks or other URLs requiring verification are not supported.

1. Go to the [CAR console](https://console.cloud.tencent.com/car).
2. Click **Application management** on the left sidebar and click **Versions** on the **Application management** page.

![](https://qcloudimg.tencent-cloud.cn/raw/d11f734b85598eedb76ee3df42bdd5f0.jpg)
3. In the **Manage application versions** pop-up window, click **Upload new version**.

![](https://qcloudimg.tencent-cloud.cn/raw/897c0cf2628af3ab9201a7f0e14f6a8c.jpg)
4. Select an upload method. You can select a file, drag a file, or enter a URL to upload a file.

![](https://qcloudimg.tencent-cloud.cn/raw/d81bd77505af877930282cf51e16cf68.jpg)
5. After submission, the application version will be created immediately. You can view the upload progress in **Manage application versions**.

![](https://qcloudimg.tencent-cloud.cn/raw/0f4b19c2aa2e2966f434f4a3d92e5f97.jpg)
6. After the creation, you can test the new version in the business environment based on the version ID. After the test is completed, click **Release**.


## Application version Rollback[](id:rollback)

>? During version rollback, make sure that the startup paths of different versions are the same; otherwise, the application will be unavailable during version switch as the startup parameter configuration doesn't match the version startup path.

1. Go to the [CAR console](https://console.cloud.tencent.com/car).
2. Click **Application management** on the left sidebar and click **Versions** on the **Application management** page.

![](https://qcloudimg.tencent-cloud.cn/raw/a1a312a41418748c8b1733778df0c7c9.jpg)
3. In the **Manage application versions** pop-up window, select an earlier version and click **Revert to this version**.

![](https://qcloudimg.tencent-cloud.cn/raw/33a061df30e389ddce897862cce56e09.jpg)
4. In the **Confirm revert** pop-up window, confirm that everything is correct and click **Revert**.

![](https://qcloudimg.tencent-cloud.cn/raw/c8afbeff1c2c5394fc0125ca79804def.jpg)
