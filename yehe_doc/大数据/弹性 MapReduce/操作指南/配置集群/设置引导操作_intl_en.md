## Feature Description
A bootstrap action is a custom script executed when a cluster is created to help you modify the cluster environment, install third-party software, and use your own data.
>Create a small pay-as-you-go cluster first to test whether the bootstrap action works properly, and if yes, create a production cluster.

An EMR instance can be created in the following steps:
 ![](https://main.qcloudimg.com/raw/93634775ebb30c1af5cefedb69e5a74e.png)
A bootstrap action can be executed at the following three time slots:
- a (after server initialization): after server resource initialization before EMR cluster software installation.
- b (before cluster startup): before cluster service startup.
- c (after cluster startup): after cluster service startup.

A bootstrap action will run bootstrap scripts during cluster creation and scaling. Bootstrap scripts will be executed in sequence in the order of addition, and there can be up to 16 bootstrap actions.

## Adding Bootstrap Action
1. Add a bootstrap action when creating a cluster on the [purchase page](https://buy.cloud.tencent.com/emapreduce#/).
Select **Basic Configuration** > **Advanced Settings** > **Add Bootstrap Action** to add a bootstrap action.
2. Add a bootstrap action on the cluster details page.
In the **Cluster List** in the EMR Console, select the target cluster and click **Details** > **Bootstrap Action** > **Add Bootstrap Action** to add a bootstrap action.
![](https://main.qcloudimg.com/raw/33cbcfa9b3b513232ffd5911483ebc9b.png)
You can edit or delete the added bootstrap action.
>When you add, edit, or delete a bootstrap action in an existing cluster, differences may exist between it and the new environment, which will lead to execution failure. Therefore, please do so with caution.
>
![](https://main.qcloudimg.com/raw/0f9e3d12ddb22ab91d42e3357cf8dada.png)
3. Select the running time slot and enter relevant parameters.
 - **Name:** you are recommended to keep it the same as your "object name".
 - **Script Location:** you are recommended to copy the location information on the COS details page. Enter the [COS Console](https://console.cloud.tencent.com/cos5), click **Bucket List**, select the desired script, and select **Operation** > **Details**.
![](https://main.qcloudimg.com/raw/43b75dca47c67002bfef5d1439fc1b09.png)
On the **Details** page, you can view the "Object Name" and "Object Address".
![](https://main.qcloudimg.com/raw/af4ba10ec70f9cbf8f71e359c9f9305c.png)
 - **`SecretID` and `SecretKEY`:** they can be obtained from the COS API key management page. Enter the [COS Console](https://console.cloud.tencent.com/cos5) and select **Key Management** > **TencentCloud API Key**.
Enter the **API Key Management** page. If there are existing `SecretID` and `SecretKEY`, they can be used directly; otherwise, you can click **Create Key** to generate a new pair of them.
![](https://main.qcloudimg.com/raw/63f6214db849c0c327c644ba402de4a2.png)
 - **Parameter:** this refers to the parameters for running the script. Separate multiple parameters by spaces, and do not add spaces in individual parameters. The total length of "Parameter" and "Name" cannot exceed 240 characters.

## Viewing Bootstrap Result
Currently, you cannot specify a bootstrap action during scaling in the console. The bootstrap action specified during cluster creation will be executed during scaling.

If you want to specify a bootstrap action for scaling, use APIs to scale. If a bootstrap action is specified for scaling, it will be executed during scaling; otherwise, the one specified during cluster creation will be executed.

Logs and script files to be executed are stored in the `/usr/local/service/scripts/` directory. The script system log is `script_syslog`.
- Naming convention: **"execution sequence" + "\_" + "running time slot" + "script name" + "\_" + stderr**.
- Naming convention: **"execution sequence" + "\_" + "running time slot" + "script name" + "\_" + stdout**.

>
>- The scripts will be executed on all types of nodes, and the script files and output log files of script execution will be stored on each node.
>- Bootstrap script content needs to be encoded in UTF-8.

