## Operation Scenarios
You can export the software configuration parameters of existing clusters in the [EMR Console](https://console.cloud.tencent.com/emr), so that when you create clusters in the future, you can quickly reuse these parameters for [software configuration](https://intl.cloud.tencent.com/document/product/1026/34530).
>Currently, software configuration is supported only for the following files:
HDFS: core-site.xml, hdfs-site.xml, hadoop-env.sh, log4j.properties
YARN: yarn-site.xml, mapred-site.xml, fair-scheduler.xml, capacity-scheduler.xml, yarn-env.sh, mapred-env.sh
Hive: hive-site.xml, hive-env.sh, hive-log4j2.properties

## Directions
1. Log in to the [EMR Console](https://console.cloud.tencent.com/emr) and enter the cluster list page.
2. In the **Manage** column of the cluster to be exported, select **More** > **Export Software Configuration**.
![](https://main.qcloudimg.com/raw/bc33820400f8ba275f2c810e6c4e5b0d.png)
3. Select the files to be exported and click **Export Configuration** to download the software configuration files.
![](https://main.qcloudimg.com/raw/b19caa18fa93fed5bb5b86bb944e85b9.png)
