## 操作场景
通过 [EMR 控制台](https://console.cloud.tencent.com/emr)，您可以导出存量集群的软件配置参数，后续在新建集群时可使用这些参数进行 [软件配置](https://intl.cloud.tencent.com/document/product/1026/34530)，从而快速新建一个熟悉的集群。
>目前仅以下文件支持导出软件配置：
HDFS：core-site.xml、hdfs-site.xml、hadoop-env.sh、log4j.properties
YARN：yarn-site.xml、mapred-site.xml、fair-scheduler.xml、capacity-scheduler.xml、yarn-env.sh、mapred-env.sh
Hive：hive-site.xml、hive-env.sh、hive-log4j2.properties

## 操作步骤
1. 登录 [EMR 控制台](https://console.cloud.tencent.com/emr) 进入集群列表页。
2. 在待导出集群的【管理】栏选择【更多】>【导出软件配置】。
![](https://main.qcloudimg.com/raw/bc33820400f8ba275f2c810e6c4e5b0d.png)
3. 勾选需要导出的文件，选择【导出配置】即可下载得到软件配置文件。
![](https://main.qcloudimg.com/raw/b19caa18fa93fed5bb5b86bb944e85b9.png)
