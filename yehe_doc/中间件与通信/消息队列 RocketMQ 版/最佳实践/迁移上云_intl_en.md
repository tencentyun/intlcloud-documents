## Overview

When using a TDMQ for RocketMQ exclusive cluster, you may need to migrate your existing business, for example, from a self-built or third-party RocketMQ cluster to the TDMQ for RocketMQ cluster.

This document describes how to migrate metadata from open-source RocketMQ to TDMQ for RocketMQ.

## Directions

### Step 1. Export the metadata file

#### Exporting the metadata file from open-source RocketMQ

If you are using self-built open-source RocketMQ, you can export metadata in the following two ways:

Option 1: If your RocketMQ server can access the public network, run the following script on your server directly (if there are multiple servers in your RocketMQ cluster, you can run the script on any server as long as the network is interconnected in the cluster).
<dx-codeblock>
:::  bash
/bin/bash -c "$(curl -fsSL https://rocketmq-1306598660.cos.ap-guangzhou.myqcloud.com/rocketmq-export.sh)"
:::
</dx-codeblock>



Option 2: If your RocketMQ server has no permission to access the public network, follow the steps below:

1. Download the [migration tool](https://rocketmq-1306598660.cos.ap-guangzhou.myqcloud.com/rocketmq-migration.zip).
2. Upload the tool to your self-built RocketMQ cluster (if there are multiple servers in your RocketMQ cluster, you can run the tool on any server as long as the network is interconnected in the cluster).
3. Decompress the tool and enter the directory.
<dx-codeblock>
:::  bash
unzip rocketmq-migration.zip
cd rocketmq-migration
:::
</dx-codeblock>
4. Run the following command for migration.
<dx-codeblock>
:::  bash
./bin/export.sh
// Enter the open-source RocketMQ address, such as `localhost:9876`
Enter name server address list:localhost:9876
// Select a cluster to export, such as `DefaultCluster`
Choose a cluster to export:DefaultCluster
// Enter a directory for saving the exported metadata, which is `/tmp/rocketmq/config/rocketmq-metadata-export.json` by default.
Enter file path to export [default /tmp/rocketmq/export]:
:::
</dx-codeblock>

#### Exporting the metadata file from ONS

1. Obtain the `AccessKey ID` and `AccessKey Secret` of the ONS root account as instructed in [Obtain an AccessKey pair](https://www.alibabacloud.com/help/en/message-queue-for-rabbitmq/latest/obtain-an-accesskey-pair).
2. Run the following migration command on any server in Linux environment that is connected to the public network.
<dx-codeblock>
:::  bash
CONF_ACCESSKEY_ID=LTAD****k59ppyN CONF_ACCESSKEY_SECRET=Xx8e86****L2lgI38Z /bin/bash -c "$(curl -fsSL https://rocketmq-1306598660.cos.ap-guangzhou.myqcloud.com/export-ali.sh )"
:::
</dx-codeblock>
<dx-alert infotype="notice" title="">
Set the values of `CONF_ACCESSKEY_ID` and `CONF_ACCESSKEY_SECRET` to the `AccessKey ID` and `AccessKey Secret` you obtained, respectively.
</dx-alert>
3. Export and save the metadata file as prompted. You can also set the environment variable `CONF_LOG_LEVEL=debug` before the command to enable the debug mode for troubleshooting.



### Step 2. Create a migration task

1. Log in to the [TDMQ for RocketMQ console](https://console.cloud.tencent.com/tdmq/rocket-cluster) and enter the **Cluster** page.
2. Switch to the **Exclusive cluster** tab and click **Migration to Cloud** to enter the migration task list page. Click **Create Task** to create a migration task.
![](https://qcloudimg.tencent-cloud.cn/raw/378cf771ace5643c67fb5f27cff14911.png)          
3. Select a migration task type:
  - **Cluster migration**: This type of task migrates metadata from the self-built RocketMQ cluster to the TDMQ for RocketMQ cluster. The migration tool will parse the part before “%” of each topic name in the open-source dashboard as the namespace name by default, so that you can create multiple logically isolated namespaces. If no topic name can be parsed in the self-built cluster, a namespace named `default` will be generated automatically.
  - **Specified namespace import**: This type of task migrates metadata from the self-built RocketMQ cluster to a specified TDMQ for RocketMQ namespace. If there are no namespaces in topics in the self-built cluster, you can select specific topics and groups you want to import, and specify the TDMQ for RocketMQ namespaces to which they are imported to distinguish between businesses or environments.
![](https://qcloudimg.tencent-cloud.cn/raw/865200e3dff2958fc6817aa65de63651.png)        
4. Upload the metadata file obtained in step 1 and select the topics and groups you want to import.
> !Up to 1,000 topics and 1,000 groups can be imported in a single task. Excess data will fail to be imported.
> 
![](https://qcloudimg.tencent-cloud.cn/raw/5d8dbb349fb067adb66179d82c5b1b67.png)              



### Step 3. Check the task status

After the task is successfully created, you can go to the task list to check its status. If there is too much data, it may take a period of time to load the task. Click **View Details**, and you can check the task status.

![](https://qcloudimg.tencent-cloud.cn/raw/983619844f8e1446eadeeb9f0e2c9a70.png)                     

If the task status is “Some failed” or “All failed”, you can filter causes of the failures in the **Task Status** column.
![](https://qcloudimg.tencent-cloud.cn/raw/f8a2b3ee4f6aed959a7868665942aac0.png)
