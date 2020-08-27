Combining cloud computing and community open-source technologies such as Hadoop, Hive, Spark, and Storm, Tencent Cloud Elastic MapReduce (EMR) provides secure and cost-effective cloud-based Hadoop services featuring high reliability and elastic scalability. A secure and reliable Hadoop cluster can be created in a matter of minutes to analyze petabytes of data stored on the data nodes in the cluster or in COS.

EMR operations supported by CloudAudit are as shown below:

| Operation Name | Resource Type | Event Name |
|-------------------|------|--------------------------------------|
| Adding auto scaling specification         | emr  | AddAutoScaleSpec                     |
| Adding configuration group             | emr  | AddConfigGroup                       |
| Getting metric load scaling rule       | emr  | AddMetricScaleStrategy               |
| Adding node specification configuration         | emr  | AddNodeResourceConfig                |
| Verifying custom configuration parameter       | emr  | CheckCustomConfig                    |
| Checking the network connection of Hive metastore    | emr  | CheckMetaDBNet                       |
| Creating EMR instance           | emr  | CreateInstance                       |
| Deleting auto scaling specification         | emr  | DeleteAutoScaleSpec                  |
| Deleting auto scaling rule         | emr  | DeleteAutoScaleStrategy              |
| Deleting configuration group             | emr  | DeleteConfigGroup                    |
| Deleting node specification configuration          | emr  | DeleteNodeResourceConfig             |
| Getting global auto scaling configuration       | emr  | DescribeAutoScaleGlobalConf          |
| Getting auto scaling metadata        | emr  | DescribeAutoScaleMetaRange           |
| Getting auto scaling history       | emr  | DescribeAutoScaleRecords             |
| Getting auto scaling specification         | emr  | DescribeAutoScaleSpecs               |
| Getting auto scaling rule         | emr  | DescribeAutoScaleStrategies          |
| Getting auto scaling allowlist        | emr  | DescribeAutoScaleWhiteList           |
| Getting boot script            | emr  | DescribeBootScript                   |
| Describing CBS encryption           | emr  | DescribeCbsEncrypt                   |
| Querying TencentDB instance price           | emr  | DescribeCdbPrice                     |
| Querying hardware node information of EMR cluster    | emr  | DescribeClusterNodes                 |
| Describing configuration group             | emr  | DescribeConfigGroup                  |
| Querying CVM instance specification          | emr  | DescribeCvmSpec                      |
| Describing cluster termination information            | emr  | DescribeDestroyInfo                  |
| Getting spread placement group information        | emr  | DescribeDisasterRecoverGroup         |
| Getting unified Hive metastore information    | emr  | DescribeEmrMetaDB                    |
| Querying EMR role           | emr  | DescribeEmrRole                      |
| Querying export configuration            | emr  | DescribeExportConfs                  |
| Querying the list of configuration files that can be exported     | emr  | DescribeExportConfsList              |
| Configuring page and pulling the list of file IPs    | emr  | DescribeFileIps                      |
| Querying the number of EMR cluster processes       | emr  | DescribeFlowNum                      |
| Querying EMR instance process status       | emr  | DescribeFlowStatus                   |
| Querying the details of EMR task running status     | emr  | DescribeFlowStatusDetail             |
| Getting the overview of HBase table monitoring data | emr  | DescribeHbaseTableMetricDataOverview |
| Getting installation component information          | emr  | DescribeInstallSoftwareInfo          |
| Displaying alarm information            | emr  | DescribeInstanceAlerts               |
| Getting alias              | emr  | DescribeInstanceAlias                |
| Getting instance operation log          | emr  | DescribeInstanceOplog                |
| Querying EMR instance           | emr  | DescribeInstances                    |
| Getting monitoring metric values at different levels    | emr  | DescribeMetricsDimension             |
| Querying configuration adjustment order            | emr  | DescribeModifyGoodsDetail            |
| Getting node specification configuration          | emr  | DescribeNodeResourceConfig           |
| Quickly getting node specification configuration        | emr  | DescribeNodeResourceConfigFast       |
| Querying optional specification allowlist         | emr  | DescribeOptionalSpecWhiteList        |
| Querying renewal order            | emr  | DescribeRenewGoodsDetail             |
| Describing expandable service          | emr  | DescribeScaleoutableService          |
| Querying expansion order            | emr  | DescribeScaleoutGoodsDetail          |
| Getting EMR security group          | emr  | DescribeSecurityGroup                |
| Querying service configuration            | emr  | DescribeServiceConfs                 |
| Querying service group information           | emr  | DescribeServiceGroups                |
| Querying service process information          | emr  | DescribeServiceNodeInfos             |
| Describing EMR subtask process        | emr  | DescribeSubJobFlowStatus             |
| Getting account balance            | emr  | DescribleAccountBalance              |
| Generating cluster creation order          | emr  | GenerateCreateGoodsDetail            |
| Generating configuration adjustment order            | emr  | GenerateModifyGoodsDetail            |
| Generating renewal order            | emr  | GenerateRenewGoodsDetail             |
| Generating expansion order            | emr  | GenerateScaleoutGoodsDetail          |
| Querying the parameters of EMR cluster creation order    | emr  | GetCreateGoodsDetail                 |
| Querying price for instance creation            | emr  | InquiryPriceCreateInstance           |
| Querying price for renewal              | emr  | InquiryPriceRenewInstance            |
| Querying price for expansion              | emr  | InquiryPriceScaleOutInstance         |
| Querying price for configuration adjustment              | emr  | InquiryPriceUpdateInstance           |
| Activating COS            | emr  | InstallCos                           |
| Installing component              | emr  | InstallSoftware                      |
| Getting configuration distribution log          | emr  | ListConfLogs                         |
| Updating global auto scaling configuration       | emr  | ModifyAutoScaleGlobalConf            |
| Modifying auto scaling rule         | emr  | ModifyAutoScaleStrategy              |
| Modifying boot script            | emr  | ModifyBootScript                     |
| Modifying configuration group             | emr  | ModifyConfigGroup                    |
| Modifying cluster name            | emr  | ModifyInstanceBasic                  |
| Adjusting instance configuration              | emr  | ModifyResource                       |
| Modifying service component parameter          | emr  | ModifyServiceParams                  |
| Modifying rule priority           | emr  | ModifyStrategyPriority               |
| Restarting component service            | emr  | RestartService                       |
| Configuring rollback              | emr  | RollBackConf                         |
| Expanding instance capacity              | emr  | ScaleOutInstance                     |
| Setting default node specification configuration attribute      | emr  | SetNodeResourceConfigDefault         |
| Starting component monitoring            | emr  | StartMonitor                         |
| Starting component service            | emr  | StartService                         |
| Stopping component monitoring            | emr  | StopMonitor                          |
| Stopping component service            | emr  | StopService                          |
| Checking sync configuration            | emr  | SynchronizeGroupConfCheck            |
| Terminating all auto scaling nodes       | emr  | TerminateAutoScaleNodes              |
| Terminating EMR instance           | emr  | TerminateInstance                    |
| Terminating node              | emr  | TerminateNodes                       |
| Terminating task node          | emr  | TerminateTasks                       |
| Updating proxy component password          | emr  | UpdateWebproxyPassword               |
