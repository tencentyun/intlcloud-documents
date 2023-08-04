## Overview
You can create integration apps to meet your integration needs. In a complex project, you can create multiple integration apps for different integration scenarios. On the **Integration apps** page, you can create, configure, rename, export, import, and delete apps.

The options displayed in the **Operation** column vary by app status as follows:
>! The debugging feature in the standalone console manipulates a certain version of the current integration app. You can still configure the current app after minimizing the test window.
>
| Status | Available operations|
|---------|---------|
|  Running | View, rename, copy, configure, export, and stop the app. |
|  Configuring | View, rename, export, configure, publish, and delete the app. |
|  Stopped | View, configure, rename, publish, and delete the app. |
|  Debugging | Vew, configure, rename, and export the app, perform an app test and a unit test, and exit the debug mode. |

## Directions
### Creating an integration app
Create an integration app as follows:
1. Log in to the [iPaaS console](https://ipaas.tencentcloud.com/login) and click **Integration apps** on the left sidebar.
2. On the **Integration apps** page, select the target project name and click **Create integration app**.
![](https://qcloudimg.tencent-cloud.cn/raw/4dbfd3e53f5e67b1fd47dc824fac6a93.png)
3. In the pop-up windown, enter the app name, select the creation method, and click **Confirm** to enter the app configuration page.

### Configuring an integration app
View the details or modify the configuration of an app as follows:
1. Log in to the [iPaaS console](https://ipaas.tencentcloud.com/login) and click **Integration apps** on the left sidebar.
2. On the **Integration apps** page, find the target app and click the **App name** to enter the app details page for configuration.
![](https://qcloudimg.tencent-cloud.cn/raw/a7450558684a3907d3ab0cc2d7410af7.png)

### Renaming an integration app
Rename a modified app as follows for easier identification:
1. Log in to the [iPaaS console](https://ipaas.tencentcloud.com/login) and click **Integration apps** on the left sidebar.
2. On the **Integration apps** page, find the target app, click **Rename** in the **Operation** column, and enter a new name as prompted.
![](https://qcloudimg.tencent-cloud.cn/raw/037fbf863667b57f24defbefb2d85a44.png)

### Importing/Exporting an integration app
To share an integration app with another account or change the project of an app (currently, you cannot directly perform such operations), you can use the import and export features.
1. Log in to the [iPaaS console](https://ipaas.tencentcloud.com/login) and click **Integration apps** on the left sidebar.
2. On the **Integration apps** page, click **Import integration app** in the top-left corner to import an app, or find the target app and click **Export** in the **Operation** column to export the app.
 - When exporting an app, you can select the target version and choose to export all or the specified flows and connections. The exported app will be automatically downloaded as an .ipaas file.
 - To import an app, you only need to upload its .ipaas file.  
![](https://qcloudimg.tencent-cloud.cn/raw/22ad0783a1f37097af48a40f37cbca91.png)

### Deleting an integration app
An integration app that is not running can be deleted.
>!The data of a deleted app cannot be recovered. Therefore, export the data for backup or check whether the data is needed before deleting an app.
>
1. Log in to the [iPaaS console](https://ipaas.tencentcloud.com/login) and click **Integration apps** on the left sidebar.
2. On the **Integration apps** page, find the target app and click **Delete** in the **Operation** column.
![](https://qcloudimg.tencent-cloud.cn/raw/527974072a9a4bb1e4f09600b25ff517.png)
### Viewing running logs
You can quickly view the running logs of a running integration app.
1. Log in to the [iPaaS console](https://ipaas.tencentcloud.com/login) and click **Integration apps** on the left sidebar.
2. On the **Integration apps** page, find the target app and click **Running logs** in the **Operation** column.
![](https://qcloudimg.tencent-cloud.cn/raw/5d68c7905a9fff72914d1cbc1f5fd415.png)
3. On the **Running logs** tab, you can view the running logs of the currently running version of the currently running app (logs in the last 30 minutes are returned by default).
![](https://qcloudimg.tencent-cloud.cn/raw/3da4f2aa26aaeca3643e526c3cb4ee2c.png)

### Zooming in/out the canvas
You can zoom in/out the canvas as needed.
![](https://qcloudimg.tencent-cloud.cn/raw/b0642901ffebc1962e88c7402a5bd838.png)

### Quickly getting started with integration
Documents are provided to help you get started with integration and creating integration apps. The documents describe the concepts and feature modules of integration apps.
![](https://qcloudimg.tencent-cloud.cn/raw/566633d7099908a6748359d9413adbdf.png)

### More features
You can quickly view the connections, security gateways, general storages, and global variables under the current project by clicking the corresponding feature module to enter the details page.
![](https://qcloudimg.tencent-cloud.cn/raw/d175118b4f032e4faf5276ef63124824.png)
On this page, you can quickly add, delete, and edit connections, security gateways, general storages, and global variables. You can also click **>>** to return to the **Integration apps** page.
![](https://qcloudimg.tencent-cloud.cn/raw/39281f1e5d1cf6210e49c05af07f6abd.png)


