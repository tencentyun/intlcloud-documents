## Overview
A bootstrap action is a custom script executed when a cluster is created to help you modify the cluster environment, install third-party software, and use your own data.

An EMR instance can be created in the following steps:
![](https://main.qcloudimg.com/raw/a36ebd385e369317db55596fd1753937.png)
A bootstrap action can be executed at the following three time slots:

- a (after node initialization): After server resource initialization and before EMR cluster software installation.
- b (before cluster start): Before cluster service start.
- c (after cluster start): After cluster service start.

Bootstrap actions run scripts during cluster creation and scale-out in the order in which the scripts are added. The number of bootstrap actions cannot exceed 16.
>!Create a small pay-as-you-go cluster first to test whether the bootstrap action works properly, and if yes, create a production cluster.

## Directions
**Option 1. Add a bootstrap action when creating a cluster on the [purchase page](https://buy.cloud.tencent.com/emr).**
1. Select **Basic Configuration** > **Advanced Settings** > **Add Bootstrap Action** to add a bootstrap action.
![](https://main.qcloudimg.com/raw/9bbf283b82525bef787a19e4b5596529.png)
2. You can edit or delete the added bootstrap action.
 - Select a run and enter relevant parameters.
 - Name: Your "object name" is recommended.
 - Script Location: We recommend you copy the location information from the COS details page. Go to the [COS console](https://console.cloud.tencent.com/cos5), click **Bucket List**, select the target script, and click **Operation** > **Details**.
![](https://main.qcloudimg.com/raw/b4d84804a68326ccf4f73bb759aa0acf.png)
On the **Details** page, you can see the "object name" and "object address".
![](https://main.qcloudimg.com/raw/ff78c91bb3531bebd8c5471fea7e54d6.png)
 - Parameter: This refers to the parameters for running the script. Separate multiple parameters by spaces, and do not add spaces in individual parameters. The total length of **Parameter** and **Name** cannot exceed 240 characters.

**Option 2. Add a bootstrap action on the **Basic information** page of the cluster.**
1. Log in to the [EMR console](https://console.cloud.tencent.com/emr) and click the **ID/Name** of the target cluster in the cluster list to enter the cluster details page. Then, select **Basic information** > **Bootstrap Actions** and click **Add Bootstrap Action**.
2. You can edit or delete the added bootstrap action.
 - Select a run and enter relevant parameters.
 - Name: Your "object name" is recommended.
 - Script Location: We recommend you copy the location information from the COS details page. Go to the [COS console](https://console.cloud.tencent.com/cos5), click **Bucket List**, select the target script, and click **Operation** > **Details**.
![](https://main.qcloudimg.com/raw/b4d84804a68326ccf4f73bb759aa0acf.png)
![](https://main.qcloudimg.com/raw/ff78c91bb3531bebd8c5471fea7e54d6.png)
 - Parameter: This refers to the parameters for running the script. Separate multiple parameters by spaces, and do not add spaces in individual parameters. The total length of **Parameter** and **Name** cannot exceed 240 characters.

## Viewing Bootstrap Result
Currently, you can specify a bootstrap action during scale-out via API but not in the console. If a bootstrap action is specified, it will be executed during scale-out; otherwise, the one specified during cluster creation will be executed.

Logs and script files to be executed are stored in the `/usr/local/service/scripts/` directory. The script system log is `script_syslog`.
- Naming convention: "Execution order" + "\_" + "run" + "script name" + "\_" + stderr.
- Naming convention: "Execution order" + "\_" + "run" + "script name" + "\_" + stdout.

>!
>- The scripts will be executed on all types of nodes, and the script files and log files output by script execution will be stored on each node.
>- Bootstrap script content needs to be encoded in UTF-8.
