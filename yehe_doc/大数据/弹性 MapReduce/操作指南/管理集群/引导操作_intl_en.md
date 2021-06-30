
## Feature Overview
A bootstrap action is a custom script executed when a cluster is created to help you modify the cluster environment, install third-party software, and use your own data.

An EMR instance can be created in the following steps:
![](https://main.qcloudimg.com/raw/a36ebd385e369317db55596fd1753937.png)
A bootstrap action can be executed on the following three occasions:
- a (after the node is initialized): after server resource initialization and  before EMR cluster software installation.
- b (before the cluster is launched): before cluster service startup.
- c (after the cluster is launched): after cluster service startup.

A bootstrap action will run bootstrap scripts during cluster creation and scaling. Bootstrap scripts will be executed in sequence in the order of addition, and there can be up to 16 bootstrap actions.

>!Create a small pay-as-you-go cluster first to test whether the bootstrap action works properly, and if yes, create a production cluster.

## Directions
**Method 1. Add a bootstrap action when creating a cluster on the [purchase page](https://buy.cloud.tencent.com/emapreduce#/).**
1. Select **Basic Configuration** > **Advanced Settings** > **Add Bootstrap Action** to add a bootstrap action.
![](https://main.qcloudimg.com/raw/9bbf283b82525bef787a19e4b5596529.png)
2. You can edit or delete the added bootstrap action.
 - Select the running occasion and enter relevant parameters.
 - Name: you are recommended to keep it the same as your "object name".
 - Script Location: you are recommended to copy the location information on the COS details page. Enter the [COS Console](https://console.cloud.tencent.com/cos5), click **Bucket List**, select the desired script, and select **Operation** > **Details**.
![](https://main.qcloudimg.com/raw/b4d84804a68326ccf4f73bb759aa0acf.png)
On the **Details** page, you can view the "Object Name" and "Object Address".
![](https://main.qcloudimg.com/raw/ff78c91bb3531bebd8c5471fea7e54d6.png)

 - Parameter: this refers to the parameters for running the script. Separate multiple parameters by spaces, and do not add spaces in individual parameters. The total length of "Parameter" and "Name" cannot exceed 240 characters.


**Method 2. Add a bootstrap action on the **Basic Info** page of the cluster.**
1. Log in to the [EMR Console](https://console.cloud.tencent.com/emr), select **Cluster List**, and click the ID/Name of the target cluster to enter the cluster details page. Select **Basic Info** -> **Bootstrap Actions** -> **Add Bootstrap Action** to add a bootstrap action.
2. You can edit or delete the added bootstrap action.
 - Select the running occasion and enter relevant parameters.
 - Name: you are recommended to keep it the same as your "object name".
 - Script Location: you are recommended to copy the location information on the COS details page. Enter the [COS Console](https://console.cloud.tencent.com/cos5), click **Bucket List**, select the desired script, and select **Operation** > **Details**.
![](https://main.qcloudimg.com/raw/b4d84804a68326ccf4f73bb759aa0acf.png)
![](https://main.qcloudimg.com/raw/ff78c91bb3531bebd8c5471fea7e54d6.png)
 - Parameter: this refers to the parameters for running the script. Separate multiple parameters by spaces, and do not add spaces in individual parameters. The total length of "Parameter" and "Name" cannot exceed 240 characters.

## Viewing Bootstrap Result
Currently, you cannot specify a bootstrap action during scaling in the console. The bootstrap action specified during cluster creation will be executed during scaling.

If you want to specify a bootstrap action for scaling, use APIs to scale. If a bootstrap action is specified for scaling, it will be executed during scaling; otherwise, the one specified during cluster creation will be executed.

Logs and script files to be executed are stored in the `/usr/local/service/scripts/` directory. The script system log is `script_syslog`.
- Naming convention: "execution sequence" + "\_" + "running occasion" + "script name" + "\_" + stderr.
- Naming convention: "execution sequence" + "\_" + "running occasion" + "script name" + "\_" + stdout.
>!
>The scripts will be executed on all types of nodes, and the script files and output log files of script execution will be stored on each node.
> Bootstrap script content needs to be encoded in UTF-8.

