## Feature Description

A bootstrap action is a custom script executed when a cluster is created to help you modify the cluster environment, install third-party software, and use your own data.
>Create a small pay-as-you-go cluster first to test whether the bootstrap action works properly, and if yes, create a production cluster.

An EMR instance can be created in the following steps:
![](https://main.qcloudimg.com/raw/088a5a0b08633a0baec06710df440f30.png)
A bootstrap action can be executed at the following two time slots:
- After resource initialization: after **server resource initialization** before **EMR cluster software installation**.
- After cluster startup: after **cluster monitoring service startup** before the **end**.

A bootstrap action will run bootstrap scripts during cluster creation and scaling (except for router nodes). Bootstrap scripts will be executed in sequence in the order of addition, and there can be up to 16 bootstrap actions.

## Adding a Bootstrap Action

#### 1. Perform the **basis configuration** step on the official website when creating a cluster
Select **Basic Configuration** > **Advanced Settings** > **Add Bootstrap Action** to add a bootstrap action.
![](https://main.qcloudimg.com/raw/7d9c30bb439a8897a1b267eb1b333912.png)   

#### 2. Select the running time point and enter relevant parameters
- Name: you are recommended to keep it the same as your "object name".
- Script Location: you are recommended to copy the location information on the COS details page. Enter the COS Console, click **Bucket List**, select the desired script, and click **Details** to view the "Object Name" and "Object Address".
![](https://main.qcloudimg.com/raw/23f600cc7f7a431a7fd370ec2c1cb5ae.png)
![](https://main.qcloudimg.com/raw/b7418baf9e746f8b96f4beefb7b1489a.png)
- `SecretID` and `SecretKEY`: they can be obtained from the COS API key management page. Enter the COS Console, select **Key Management** > **TencentCloud API Key** to enter the **API Key Management** page. If there are existing `SecretID` and `SecretKEY`, they can be used directly; otherwise, you can click **Create Key** to generate a new pair of them.

![](https://main.qcloudimg.com/raw/a938376b3ab7ed55e579db72af31e70c.png)
- Parameter: this refers to the parameters for running the script. Separate multiple parameters by spaces, and do not add spaces in individual parameters. The total length of "Parameter" and "Name" cannot exceed 240 characters.

## Viewing the Bootstrap Result
Currently, you cannot specify a bootstrap action during scaling in the console. The bootstrap action specified during cluster creation will be executed during scaling.
If you want to specify a bootstrap action for scaling, use APIs to scale. If a bootstrap action is specified for scaling, it will be executed during scaling; otherwise, the one specified during cluster creation will be executed.

- The executed script files are stored in the `/usr/local/service/scripts/` directory of each node. The naming convention is "execution order" + "_" + "script name".
- The log files of script execution are stored in the `/data/logs/script-logs/` directory of each node. The naming convention is "execution order" + "_" + "script name" + "-" + "parameter 1" + "-" + "parameter 2" + ... + "-exec.log".
> The scripts will be executed on all types of nodes, and the script files and output log files of script execution will be stored on each node.
>
	![](https://main.qcloudimg.com/raw/cb7918b11e5f8da9d8089e643c4bee7e.png)

