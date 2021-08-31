创建 Dashboard 之后，通过配置 Panel 信息，即可获取腾讯云监控的相应监控数据。现在以简单的 Graph 为例，展示如何配置 Panel 信息。

## CVM 云服务器监控

1. 单击 **New Panel** 面板的 **Add Query** 选项，进入 Panel 配置页面。在左侧第一个 `Query` 选项卡，通过配置选项获取腾讯云 CVM 云服务器的监控数据。
2. `Queries to` 数据源列表，选择已配置的包含 CVM 监控服务的腾讯云监控数据源。
3. 配置项的内容对齐腾讯云服务器监控接口的输入参数，可参见 [云服务器监控接口文档](https://intl.cloud.tencent.com/document/product/248/6843)，更好地理解各配置项。
    - `Namespace` 命名空间，云服务器监控的命名空间为 `QCE/CVM`。
    - `Region` 地域，地域列表会根据 `Namespace` 选项自动获取，单击选择某一地域。
    - `MetricName` 指标名称，指标列表会根据 `Namespace` 和 `Region` 选项自动获取，单击选择某一指标。
    - `Period` 监控统计周期，周期列表会根据 `MetricName` 选项自动获取，单击选择某一统计周期。
    - `Instance` 实例，对应输入参数的 `Instances.N` 字段，实例列表会自动获取。
      - 为了适应不同用户的习惯，实例列表会以不同的字段展示，默认为 `As InstanceId`，以 **实例 ID** 展示实例列表。此外，可以选择 `As InstanceName` 实例名称、`As PrivateIpAddress` 主网卡的内网IP、 `As PublicIpAddress` 主网卡的公网IP。
      - 可实例列表的获取可参见 [云服务器查询实例列表接口文档](https://intl.cloud.tencent.com/document/product/213/33258)。切换 `Show Details` 为 `true`，可展示实例请求参数，默认参数为`Offset = 0` 和 `Limit = 20`。如果需要变更实例查询条件，可参见接口文档，配置相应参数。
      - **注意：** 在本应用中，监控数据的单次查询为原子操作，即查询某一实例的某一指标的监控数据，故实例只能单选，如需查询多实例的监控数据，单击右上角的 `Add Query` 增加新的查询。
      - `Show Details` 按钮仅在选择非模板变量时显示。

![](https://main.qcloudimg.com/raw/6108f8baa95def11d082022aa163927f.png)

## TencentDB 云数据库 MySQL
1. 单击 **New Panel** 面板的 **Add Query** 选项，进入 Panel 配置页面。在左侧第一个 `Query` 选项卡，通过配置选项获取腾讯云数据库 MySQL 的监控数据。
2. `Queries to` 数据源列表，选择已配置的包含 TencentDB 监控服务的腾讯云监控数据源。
3. 配置项的内容对齐腾讯云数据库MySQL监控接口的输入参数，可参见 [云数据库MySQL监控接口文档](https://intl.cloud.tencent.com/document/product/248/11006)，更好地理解各配置项。

    - `Namespace` 命名空间，云服务器监控的命名空间为 `QCE/CDB`。
    - `Region` 地域，地域列表会根据 `Namespace` 选项自动获取，单击选择某一地域。
    - `MetricName` 指标名称，指标列表会根据 `Namespace` 和 `Region` 选项自动获取，单击选择某一指标。
    - `Period` 监控统计周期，周期列表会根据 `MetricName` 选项自动获取，单击选择某一统计周期。
    - `Instance` 实例，对应输入参数的 `Instances.N` 字段，实例列表会自动获取。
      - 为了适应不同用户的习惯，实例列表会以不同的字段展示，默认为 `As InstanceId`，以 **实例ID** 展示实例列表。此外，可以选择 `As InstanceName` 实例名称、 `As Vip` 内网IP。
      - 实例列表的获取可参见 [云数据库MySQL查询实例列表接口文档](https://intl.cloud.tencent.com/document/api/236/15872)。切换 `Show Details` 为 `true`，可展示实例请求参数，默认参数为`Offset = 0` 和 `Limit = 20`。如果需要变更实例查询条件，可参见接口文档，配置相应参数。
      - **注意：** 在本应用中，监控数据的单次查询为原子操作，即查询某一实例的某一指标的监控数据，故实例只能单选，如需查询多实例的监控数据，单击右上角的 `Add Query` 增加新的查询。  
      - `Show Details` 按钮仅在选择非模板变量时显示。

![](https://main.qcloudimg.com/raw/8f14371f5286e1f2bb1c09dadbafc006.png)

## 云数据库 PostgreSql

1. 单击 **New Panel** 面板的 **Add Query** 选项，进入 Panel 配置页面。在左侧第一个 `Query` 选项卡，通过配置选项获取腾讯云数据库 PostgreSQL 的监控数据。
2. `Queries to` 数据源列表，选择已配置的包含 PostgreSQL 监控服务的腾讯云监控数据源。
3. 配置项的内容对齐腾讯云数据库PostgreSQL监控接口的输入参数，可参见 [云数据库PostgreSQL监控接口文档](https://intl.cloud.tencent.com/document/product/248/17945)，更好地理解各配置项。
    - `Namespace` 命名空间，云服务器监控的命名空间为 `QCE/POSTGRES`。
    - `Region` 地域，地域列表会根据 `Namespace` 选项自动获取，单击选择某一地域。
    - `MetricName` 指标名称，指标列表会根据 `Namespace` 和 `Region` 选项自动获取，单击选择某一指标。
    - `Period` 监控统计周期，周期列表会根据 `MetricName` 选项自动获取，单击选择某一统计周期。
    - `Instance` 实例，对应输入参数的 `Instances.N` 字段，实例列表会自动获取。
      - 为了适应不同用户的习惯，实例列表会以不同的字段展示，默认为 `As InstanceId`，以 **实例ID** 展示实例列表。此外，可以选择 `As DBInstanceName`数据库名称, `PrivateIpAddresses`内网ip, `PublicIpAddresses`公网ip。
      - 实例列表的获取可参见 [云数据库PostgreSQL查询实例列表接口文档](https://intl.cloud.tencent.com/document/api/409/16773)。切换 `Show Details` 为 `true`，可展示实例请求参数，默认参数为`Offset = 0` 和 `Limit = 20`。如果需要变更实例查询条件，可参见接口文档，配置相应参数。
      - **注意：** 在本应用中，监控数据的单次查询为原子操作，即查询某一实例的某一指标的监控数据，故实例只能单选，如需查询多实例的监控数据，单击右上角的 `Add Query` 增加新的查询。  
      - `Show Details` 按钮仅在选择非模板变量时显示。

![](https://main.qcloudimg.com/raw/3b0f15968a4c049a23794e7116117298.png)

## 云数据库 MongoDB

1. 单击 **New Panel** 面板的 **Add Query** 选项，进入 Panel 配置页面。在左侧第一个 `Query` 选项卡，通过配置选项获取腾讯云云数据库 MongoDB 的监控数据。
2. `Queries to` 数据源列表，选择已配置的包含 mongodb 监控服务的腾讯云监控数据源。
3. 配置项的内容对齐腾讯云服务器监控接口的输入参数，可参见 [mongodb云监控接口文档](https://intl.cloud.tencent.com/document/product/248/35671)，更好地理解各配置项。
    - `Namespace` 命名空间，例如 `QCE/CMONGO`。
    - `Region` 地域，地域列表会根据 `Namespace` 选项自动获取，单击选择某一地域。
    - `MetricName` 指标名称，指标列表会根据 `Namespace` 和 `Region` 选项自动获取，单击选择某一指标。
    - `Period` 监控统计周期，周期列表会根据 `MetricName` 选项自动获取，单击选择某一统计周期。
    - `Instance` 实例，对应输入参数的 `Instances.N` 字段，实例列表会自动获取。
      - 为了适应不同用户的习惯，实例列表会以不同的字段展示，默认为 `As InstanceId`，以 **实例id** 展示实例列表。此外，可以选择 `As InstanceName` 实例名称。
      - 实例列表的获取可参见 [mongodb列表接口文档](https://intl.cloud.tencent.com/document/product/240/34702)。切换 `Show Details` 为 `true`，可展示实例请求参数，默认参数为`Offset = 0` 和 `Limit = 20`。如果需要变更实例查询条件，可参见接口文档，配置相应参数。
      - **注意：** 在本应用中，监控数据的单次查询为原子操作，即查询某一实例的某一指标的监控数据，故实例只能单选，如需查询多实例的监控数据，单击右上角的 `Add Query` 增加新的查询。  
      - `Show Details` 按钮仅在选择非模板变量时显示。

![](https://main.qcloudimg.com/raw/4b397465608905d153d970449b197c09.png)

## 云数据库 Redis

1. 单击 **New Panel** 面板的 **Add Query** 选项，进入 Panel 配置页面。在左侧第一个 `Query` 选项卡，通过配置选项获取腾讯云云数据库 Redis的监控数据。
2. `Queries to` 数据源列表，选择已配置的包含 redis 监控服务的腾讯云监控数据源。
3. 云数据库 Redis 分两个命名空间：内存版（5秒）（Namespace=QCE/REDIS_MEM），ckv版和内存版（1分钟）（Namespace=QCE/REDIS）可根据自己需要在`Namespace`选择。
4. 配置项的内容对齐腾讯云服务器监控接口的输入参数，可参见 [Redis云监控接口文档](https://intl.cloud.tencent.com/document/product/248/39507)，更好地理解各配置项。
    - `Namespace` 命名空间，例如 `QCE/REDIS_MEM`。
    - `Region` 地域，地域列表会根据 `Namespace` 选项自动获取，单击选择某一地域。
    - `MetricName` 指标名称，指标列表会根据 `Namespace` 和 `Region` 选项自动获取，单击选择某一指标。
    - `Period` 监控统计周期，周期列表会根据 `MetricName` 选项自动获取，单击选择某一统计周期。
    - `Instance` 实例，对应输入参数的 `Instances.N` 字段，实例列表会自动获取。
      - 为了适应不同用户的习惯，实例列表会以不同的字段展示，默认为 `As InstanceId`，以 **实例id** 展示实例列表。此外，可以选择 `As InstanceName` 实例名称。
      - 实例列表的获取可参见 [Redis实例列表接口文档](https://intl.cloud.tencent.com/document/product/239/32065)。切换 `Show Details` 为 `true`，可展示实例请求参数，默认参数为`Offset = 0` 和 `Limit = 20`。如果需要变更实例查询条件，可参见接口文档，配置相应参数。
      - **注意：** 在本应用中，监控数据的单次查询为原子操作，即查询某一实例的某一指标的监控数据，故实例只能单选，如需查询多实例的监控数据，单击右上角的 `Add Query` 增加新的查询。  
      - `Show Details` 按钮仅在选择非模板变量时显示。

![](https://main.qcloudimg.com/raw/057de4d5a18efca58f8b2be365563b87.png)

## 云数据库 CYNOSDB_MYSQL

1. 单击 **New Panel** 面板的 **Add Query** 选项，进入 Panel 配置页面。在左侧第一个 `Query` 选项卡，通过配置选项获取腾讯云云数据库  CYNOSDB(CYNOSDB_MYSQL) 的监控数据。
2. `Queries to` 数据源列表，选择已配置的包含 cynosdbMysql 监控服务的腾讯云监控数据源。
3. 配置项的内容对齐腾讯云监控cynosdbMysql监控接口的输入参数，可参见 [云数据库 CYNOSDB(CYNOSDB_MYSQL) 云监控接口文档](https://intl.cloud.tencent.com/document/product/248/37383)，更好地理解各配置项。
    - `Namespace` 命名空间，例如 `QCE/CYNOSDB_MYSQL`。
    - `Region` 地域，地域列表会根据 `Namespace` 选项自动获取，单击选择某一地域。
    - `MetricName` 指标名称，指标列表会根据 `Namespace` 和 `Region` 选项自动获取，单击选择某一指标。
    - `Period` 监控统计周期，周期列表会根据 `MetricName` 选项自动获取，单击选择某一统计周期。
    - `Instance` 实例，对应输入参数的 `Instances.N` 字段，实例列表会自动获取。
      - 为了适应不同用户的习惯，实例列表会以不同的字段展示，默认为 `As InstanceId`，以 **实例ID** 展示实例列表。此外，可以选择 `As InstanceName` 实例名称。
      - 实例列表的获取可参见云数据库 CYNOSDB(CYNOSDB_MYSQL)列表接口文档。切换 `Show Details` 为 `true`，可展示实例请求参数，默认参数为`Offset = 0` 和 `Limit = 20`。如果需要变更实例查询条件，可参见接口文档，配置相应参数。
      - **注意：** 在本应用中，监控数据的单次查询为原子操作，即查询某一实例的某一指标的监控数据，故实例只能单选，如需查询多实例的监控数据，单击右上角的 `Add Query` 增加新的查询。  
      - `Show Details` 按钮仅在选择非模板变量时显示。

![](https://main.qcloudimg.com/raw/9b8c3ad36e1de3f9053057bfc354e1e0.png)
    

## 云数据库 TcaplusDB

1. 单击 **New Panel** 面板的 **Add Query** 选项，进入 Panel 配置页面。在左侧第一个 `Query` 选项卡，通过配置选项获取腾讯云云数据库 TcaplusDB(TCAPLUS)的监控数据。
2. `Queries to` 数据源列表，选择已配置的包含 tcaplus 监控服务的腾讯云监控数据源。
3. 配置项的内容对齐腾讯云监控tcaplus监控接口的输入参数，可参见 [云数据库  TcaplusDB(TCAPLUS) 云监控接口文档](https://intl.cloud.tencent.com/document/product/248/34592)，更好地理解各配置项。
  - `Namespace` 命名空间，例如 `QCE/TCAPLUS`。
  - `Region` 地域，地域列表会根据 `Namespace` 选项自动获取，单击选择某一地域。
  - `MetricName` 指标名称，指标列表会根据 `Namespace` 和 `Region` 选项自动获取，单击选择某一指标。
  - `Period` 监控统计周期，周期列表会根据 `MetricName` 选项自动获取，单击选择某一统计周期。
  - `Instance` 实例，对应输入参数的 `Instances.N` 字段，实例列表会自动获取。
    - 为了适应不同用户的习惯，实例列表会以不同的字段展示，默认为 `As InstanceId`，以 **实例ID** 展示实例列表。此外，可以选择 `As InstanceName` 实例名称。
    - 实例列表的获取可参见云数据库 TcaplusDB(TCAPLUS)列表接口文档。切换 `Show Details` 为 `true`，可展示实例请求参数，默认参数为`Offset = 0` 和 `Limit = 20`。如果需要变更实例查询条件，可参见接口文档，配置相应参数。
    - **注意：** 在本应用中，监控数据的单次查询为原子操作，即查询某一实例的某一指标的监控数据，故实例只能单选，如需查询多实例的监控数据，单击右上角的 `Add Query` 增加新的查询。  
    - `Show Details` 按钮仅在选择非模板变量时显示。

![](https://main.qcloudimg.com/raw/69219fff55a5d40cbdb0fed31e13d900.png)

## 云数据库 SQL Server

1. 单击 **New Panel** 面板的 **Add Query** 选项，进入 Panel 配置页面。在左侧第一个 `Query` 选项卡，通过配置选项获取腾讯云云数据库 sqlserver(SQLSERVER) 的监控数据。
2. `Queries to` 数据源列表，选择已配置的包含 sqlserver 监控服务的腾讯云监控数据源。
3. 配置项的内容对齐腾讯云监控 sqlserver 监控接口的输入参数，可参见 [云数据库sqlserver(SQLSERVER)云监控接口文档](https://intl.cloud.tencent.com/document/product/248/11008)，更好地理解各配置项。
  - `Namespace` 命名空间，例如 `QCE/SQLSERVER`。
  - `Region` 地域，地域列表会根据 `Namespace` 选项自动获取，单击选择某一地域。
  - `MetricName` 指标名称，指标列表会根据 `Namespace` 和 `Region` 选项自动获取，单击选择某一指标。
  - `Period` 监控统计周期，周期列表会根据 `MetricName` 选项自动获取，单击选择某一统计周期。
  - `Instance` 实例，对应输入参数的 `Instances.N` 字段，实例列表会自动获取。
    - 为了适应不同用户的习惯，实例列表会以不同的字段展示，默认为 `As InstanceId`，以 **实例ID** 展示实例列表。此外，可以选择 `As Name` 实例名称。
    - 实例列表的获取可参见 [云数据库sqlserver(SQLSERVER)列表接口文档](https://intl.cloud.tencent.com/document/product/238/32115)。切换 `Show Details` 为 `true`，可展示实例请求参数，默认参数为`Offset = 0` 和 `Limit = 20`。如果需要变更实例查询条件，可参见接口文档，配置相应参数。
    - **注意：** 在本应用中，监控数据的单次查询为原子操作，即查询某一实例的某一指标的监控数据，故实例只能单选，如需查询多实例的监控数据，单击右上角的 `Add Query` 增加新的查询。  
    - `Show Details` 按钮仅在选择非模板变量时显示。

![](https://main.qcloudimg.com/raw/df5671f1b987dd68145ff522a38647f1.png)

## CDN 内容分发式网络

1. 单击 **New Panel** 面板的 **Add Query** 选项，进入 Panel 配置页面。在左侧第一个 `Query` 选项卡，通过配置选项获取腾讯云 CDN 的监控数据。
2. `Queries to` 数据源列表，选择已配置的包含 CDN 监控服务的腾讯云监控数据源。
3. CDN 指标分两个命名空间：国内域名（Namespace=QCE/CDN），国外域名（Namespace=QCE/OV_CDN）可根据自己需要在`Namespace`选择。
4. 配置项的内容对齐腾讯 CDN 监控接口的输入参数，可参见 [CDN云监控接口文档](https://intl.cloud.tencent.com/document/product/248/39554)，更好地理解各配置项。
    - `Namespace` 命名空间，例如 `QCE/CDN`。
    - `Region` 地域，地域列表会根据 `Namespace` 选项自动获取，单击选择某一地域。
    - `MetricName` 指标名称，指标列表会根据 `Namespace` 和 `Region` 选项自动获取，单击选择某一指标。
    - `Period` 监控统计周期，周期列表会根据 `MetricName` 选项自动获取，单击选择某一统计周期。
    - `Instance` 实例，对应输入参数的 `Instances.N` 字段，实例列表会自动获取。
      - 为了适应不同用户的习惯，实例列表会以不同的字段展示，默认为 `As Domain`，以 **域名** 展示实例列表。此外，可以选择 `As ProjectId` 项目id。
      - 域名列表的获取可参见 [CDN域名列表接口文档](https://intl.cloud.tencent.com/document/product/228/34020)。切换 `Show Details` 为 `true`，可展示实例请求参数，默认参数为`Offset = 0` 和 `Limit = 20`。如果需要变更实例查询条件，可参见接口文档，配置相应参数。
      - **注意：** 在本应用中，监控数据的单次查询为原子操作，即查询某一实例的某一指标的监控数据，故实例只能单选，如需查询多实例的监控数据，单击右上角的 `Add Query` 增加新的查询。  
      - `Show Details` 按钮仅在选择非模板变量时显示。

## BWP 带宽包

1. 单击 **New Panel** 面板的 **Add Query** 选项，进入 Panel 配置页面。在左侧第一个 `Query` 选项卡，通过配置选项获取腾讯云 BWP 的监控数据。
2. `Queries to` 数据源列表，选择已配置的包含 BWP 监控服务的腾讯云监控数据源。
3. 配置项的内容对齐腾讯云 BWP 监控接口的输入参数，可参见 [BWP云监控接口文档](https://intl.cloud.tencent.com/document/product/248/34645)，更好地理解各配置项。
    - `Namespace` 命名空间，例如 `QCE/BWP`。
    - `Region` 地域，地域列表会根据 `Namespace` 选项自动获取，单击选择某一地域。
    - `MetricName` 指标名称，指标列表会根据 `Namespace` 和 `Region` 选项自动获取，单击选择某一指标。
    - `Period` 监控统计周期，周期列表会根据 `MetricName` 选项自动获取，单击选择某一统计周期。
    - `Instance` 实例，对应输入参数的 `Instances.N` 字段，实例列表会自动获取。
      - 为了适应不同用户的习惯，实例列表会以不同的字段展示，默认为`As BandwidthPackageId`，以 **带宽包id** 展示实例列表。此外，可以选择 `As BandwidthPackageName` 名称。
      - 域名列表的获取可参见 [BWP域名列表接口文档](https://intl.cloud.tencent.com/document/product/215/36919)。切换 `Show Details` 为 `true`，可展示实例请求参数，默认参数为`Offset = 0` 和 `Limit = 20`。如果需要变更实例查询条件，可参见接口文档，配置相应参数。
      - **注意：** 在本应用中，监控数据的单次查询为原子操作，即查询某一实例的某一指标的监控数据，故实例只能单选，如需查询多实例的监控数据，单击右上角的 `Add Query` 增加新的查询。  
      - `Show Details` 按钮仅在选择非模板变量时显示。

![](https://main.qcloudimg.com/raw/dccea7d8c6dfe3bd080853906cf62fc7.png)

## CKAFKA 消息队列

1. 单击 **New Panel** 面板的 **Add Query** 选项，进入 Panel 配置页面。在左侧第一个 `Query` 选项卡，通过配置选项获取腾讯云 ckafka 消息队列的监控数据。
2. `Queries to` 数据源列表，选择已配置的包含 ckafka 监控服务的腾讯云监控数据源。
3. 配置项的内容对齐腾讯 ckafka 监控接口的输入参数，可参见 [ckafka云监控接口文档](https://intl.cloud.tencent.com/document/product/248/17297)，更好地理解各配置项。
    - `Namespace` 命名空间，例如 `QCE/CKAFKA`。
    - `Region` 地域，地域列表会根据 `Namespace` 选项自动获取，单击选择某一地域。
    - `MetricName` 指标名称，指标列表会根据 `Namespace` 和 `Region` 选项自动获取，单击选择某一指标。
    - `Period` 监控统计周期，周期列表会根据 `MetricName` 选项自动获取，单击选择某一统计周期。
    - `Instance` 实例，对应输入参数的 `Instances.N` 字段，实例列表会自动获取。
      - 为了适应不同用户的习惯，实例列表会以不同的字段展示，默认为 `As InstanceId`，以 **实例id** 展示实例列表。此外，可以选择 `As InstanceName` 实例名称。
      - 实例列表的获取可参见 [ckafka列表接口文档](https://intl.cloud.tencent.com/document/product/597/35357)。切换 `Show Details` 为 `true`，可展示实例请求参数，默认参数为`Offset = 0` 和 `Limit = 10`。如果需要变更实例查询条件，可参见接口文档，配置相应参数。
      - **注意：** 在本应用中，监控数据的单次查询为原子操作，即查询某一实例的某一指标的监控数据，故实例只能单选，如需查询多实例的监控数据，单击右上角的 `Add Query` 增加新的查询。  
      - `Show Details` 按钮仅在选择非模板变量时显示。

![](https://main.qcloudimg.com/raw/a2f158398226dc3883ba115877da5d47.png)

## CLB 负载均衡

1. 单击 **New Panel** 面板的 **Add Query** 选项，进入 Panel 配置页面。在左侧第一个 `Query` 选项卡，通过配置选项获取腾讯云 负载均衡的监控数据。
2. `Queries to` 数据源列表，选择已配置的包含 CLB 监控服务的腾讯云监控数据源。
3. 负载均衡指标分三个命名空间：公网负载均衡监控指标（Namespace=QCE/LB_PUBLIC），内网负载均衡四层协议监控指标（Namespace=QCE/LB_PRIVATE）， 七层协议监控指标（Namespace=QCE/LOADBALANCE），可根据自己需要在`Namespace`选择。
4. 配置项的内容对齐腾讯云服务器监控接口的输入参数，可参见 [负载均衡云监控接口文档](https://intl.cloud.tencent.com/document/product/248/10997)，更好地理解各配置项。
    - `Namespace` 命名空间，例如 `QCE/LB_PUBLIC`。
    - `Region` 地域，地域列表会根据 `Namespace` 选项自动获取，单击选择某一地域。
    - `MetricName` 指标名称，指标列表会根据 `Namespace` 和 `Region` 选项自动获取，单击选择某一指标。
    - `Period` 监控统计周期，周期列表会根据 `MetricName` 选项自动获取，单击选择某一统计周期。
    - `Instance` 实例，对应输入参数的 `Instances.N` 字段，实例列表会自动获取。
      - 为了适应不同用户的习惯，实例列表会以不同的字段展示，默认为 `As LoadBalancerId`，以 **实例ID** 展示实例列表。此外，可以选择 `As LoadBalancerName` 实例名称、`As LoadBalancerVips` 网络ip。
      - 实例列表的获取可参见 [负载均衡实例列表接口文档](https://intl.cloud.tencent.com/document/product/214/33830)。切换 `Show Details` 为 `true`，可展示实例请求参数，默认参数为`Offset = 0` 和 `Limit = 20`。如果需要变更实例查询条件，可参见接口文档，配置相应参数。
      - **注意：** 在本应用中，监控数据的单次查询为原子操作，即查询某一实例的某一指标的监控数据，故实例只能单选，如需查询多实例的监控数据，单击右上角的 `Add Query` 增加新的查询。  
      - `Show Details` 按钮仅在选择非模板变量时显示。
    - `Listener` 【可选】监听器，可不选择，这时采用实例维度请求，对应输入参数的 `Listener.N` 字段，列表会自动获取。
      - 为了适应不同用户的习惯，监听器列表会以不同的字段展示，默认为 `As ListenerId`，以 **监听器ID** 展示实例列表。此外，可以选择 `As ListenerName` 监听器名称、`As Port` 端口。
      - 监听器列表的获取可参见 [负载均衡监听器列表接口文档](https://intl.cloud.tencent.com/document/product/214/33831)。

![](https://main.qcloudimg.com/raw/d82b9c974060162b0e8e3b80c3e169f0.png)

## LB 弹性公网 IP

1. 单击 **New Panel** 面板的 **Add Query** 选项，进入 Panel 配置页面。在左侧第一个 `Query` 选项卡，通过配置选项获取腾讯云lb弹性公网ip的监控数据。
2. `Queries to` 数据源列表，选择已配置的包含 lb 监控服务的腾讯云监控数据源。
3. 配置项的内容对齐腾讯 lb 监控接口的输入参数，可参见 [lb云监控接口文档](https://intl.cloud.tencent.com/document/product/248/34646)，更好地理解各配置项。
    - `Namespace` 命名空间，例如 `QCE/LB`。
    - `Region` 地域，地域列表会根据 `Namespace` 选项自动获取，单击选择某一地域。
    - `MetricName` 指标名称，指标列表会根据 `Namespace` 和 `Region` 选项自动获取，单击选择某一指标。
    - `Period` 监控统计周期，周期列表会根据 `MetricName` 选项自动获取，单击选择某一统计周期。
    - `Instance` 实例，对应输入参数的 `Instances.N` 字段，实例列表会自动获取。
      - 为了适应不同用户的习惯，实例列表会以不同的字段展示，默认为 `As AddressId`，以 **实例地址id** 展示实例列表。此外，可以选择 `As AddressName`地址名称和`As AddressIp` 地址IP。
      - 实例列表的获取可参见 [lb列表接口文档](https://intl.cloud.tencent.com/document/api/215/16702)。切换 `Show Details` 为 `true`，可展示实例请求参数，默认参数为`Offset = 0` 和 `Limit = 20`。如果需要变更实例查询条件，可参见接口文档，配置相应参数。
      - **注意：** 在本应用中，监控数据的单次查询为原子操作，即查询某一实例的某一指标的监控数据，故实例只能单选，如需查询多实例的监控数据，单击右上角的 `Add Query` 增加新的查询。  
      - `Show Details` 按钮仅在选择非模板变量时显示。

![](https://main.qcloudimg.com/raw/952733c4781b975c5a7128785fac8e86.png)

## CFS 文件存储

1. 单击 **New Panel** 面板的 **Add Query** 选项，进入 Panel 配置页面。在左侧第一个 `Query` 选项卡，通过配置选项获取腾讯云cfs文件存储的监控数据。
2. `Queries to` 数据源列表，选择已配置的包含 cfs 监控服务的腾讯云监控数据源。
3. 配置项的内容对齐腾讯cfs监控接口的输入参数，可参见 [cfs云监控接口文档](https://intl.cloud.tencent.com/document/product/248/34644)，更好地理解各配置项。
    - `Namespace` 命名空间，例如 `QCE/CFS`。
    - `Region` 地域，地域列表会根据 `Namespace` 选项自动获取，单击选择某一地域。
    - `MetricName` 指标名称，指标列表会根据 `Namespace` 和 `Region` 选项自动获取，单击选择某一指标。
    - `Period` 监控统计周期，周期列表会根据 `MetricName` 选项自动获取，单击选择某一统计周期。
    - `Instance` 实例，对应输入参数的 `Instances.N` 字段，实例列表会自动获取。
      - 为了适应不同用户的习惯，实例列表会以不同的字段展示，默认为 `As FileSystemId`，以 **文件系统id** 展示实例列表。此外，可以选择 `As FsName` 文件系统名称。
      - 实例列表的获取可参见 [CFS列表接口文档](https://intl.cloud.tencent.com/document/product/582/34514)。切换 `Show Details` 为 `true`，可展示实例请求参数，默认参数为`Offset = 0` 和 `Limit = 20`。如果需要变更实例查询条件，可参见接口文档，配置相应参数。
      - **注意：** 在本应用中，监控数据的单次查询为原子操作，即查询某一实例的某一指标的监控数据，故实例只能单选，如需查询多实例的监控数据，单击右上角的 `Add Query` 增加新的查询。  
      - `Show Details` 按钮仅在选择非模板变量时显示。

![](https://main.qcloudimg.com/raw/e645a947e2e7491cb1de766652893a2b.png)

## SCF 云函数

1. 单击 **New Panel** 面板的 **Add Query** 选项，进入 Panel 配置页面。在左侧第一个 `Query` 选项卡，通过配置选项获取腾讯云scf云函数的监控数据。
2. `Queries to` 数据源列表，选择已配置的包含 scf 监控服务的腾讯云监控数据源。
3. 配置项的内容对齐腾讯 scf 监控接口的输入参数，可参见 [ scf 云监控接口文档](https://intl.cloud.tencent.com/document/product/248/34638)，更好地理解各配置项。
    - `Namespace` 命名空间，例如 `QCE/SCF_V2`。
    - `Region` 地域，地域列表会根据 `Namespace` 选项自动获取，单击选择某一地域。
    - `MetricName` 指标名称，指标列表会根据 `Namespace` 和 `Region` 选项自动获取，单击选择某一指标。
    - `Period` 监控统计周期，周期列表会根据 `MetricName` 选项自动获取，单击选择某一统计周期。
    - `Instance` 实例，对应输入参数的 `Instances.N` 字段，实例列表会自动获取。
      - 为了适应不同用户的习惯，实例列表会以不同的字段展示，默认为 `As FunctionId`，以 **函数id** 展示实例列表。此外，可以选择 `As FunctionName` 函数名称。
      - 实例列表的获取可参见 [ SCF 列表接口文档](https://intl.cloud.tencent.com/document/api/583/18582)。切换 `Show Details` 为 `true`，可展示实例请求参数，默认参数为`Offset = 0` 和 `Limit = 20`。如果需要变更实例查询条件，可参见接口文档，配置相应参数。
      - **注意：** 在本应用中，监控数据的单次查询为原子操作，即查询某一实例的某一指标的监控数据，故实例只能单选，如需查询多实例的监控数据，单击右上角的 `Add Query` 增加新的查询。  
      - `Show Details` 按钮仅在选择非模板变量时显示。

![](https://main.qcloudimg.com/raw/679409acfac1081ff87edd1883a7f6f9.png)

## DCX 专线接入-专用通道

1. 单击 **New Panel** 面板的 **Add Query** 选项，进入 Panel 配置页面。在左侧第一个 `Query` 选项卡，通过配置选项获取腾讯云专线接入-专用通道(DCX)的监控数据。
2. `Queries to` 数据源列表，选择已配置的包含 dcx 监控服务的腾讯云监控数据源。
3. 配置项的内容对齐腾讯云监控dcx监控接口的输入参数，可参见 [专线接入-专用通道(DCX)云监控接口文档](https://intl.cloud.tencent.com/document/product/248/10995)，更好地理解各配置项。
 - `Namespace` 命名空间，例如 `QCE/DCX`。
 - `Region` 地域，地域列表会根据 `Namespace` 选项自动获取，单击选择某一地域。
 - `MetricName` 指标名称，指标列表会根据 `Namespace` 和 `Region` 选项自动获取，单击选择某一指标。
 - `Period` 监控统计周期，周期列表会根据 `MetricName` 选项自动获取，单击选择某一统计周期。
 - `Instance` 实例，对应输入参数的 `Instances.N` 字段，实例列表会自动获取。
   - 为了适应不同用户的习惯，实例列表会以不同的字段展示，默认为 `As DirectConnectTunnelId`，以 **通道ID** 展示实例列表。此外，可以选择 `As DirectConnectTunnelName` 通道名称。
   - 实例列表的获取可参见 [专线接入-专用通道(DCX)列表接口文档](https://intl.cloud.tencent.com/document/api/216/19819)。切换 `Show Details` 为 `true`，可展示实例请求参数，默认参数为`Offset = 0` 和 `Limit = 20`。如果需要变更实例查询条件，可参见接口文档，配置相应参数。
   - **注意：** 在本应用中，监控数据的单次查询为原子操作，即查询某一实例的某一指标的监控数据，故实例只能单选，如需查询多实例的监控数据，单击右上角的 `Add Query` 增加新的查询。  
   - `Show Details` 按钮仅在选择非模板变量时显示。

![](https://main.qcloudimg.com/raw/87b7219031f6b0166c7057e974751b92.png)
    

## DC 专线接入-物理专线

1. 单击 **New Panel** 面板的 **Add Query** 选项，进入 Panel 配置页面。在左侧第一个 `Query` 选项卡，通过配置选项获取腾讯云专线接入-物理专线(DC)的监控数据。
2. `Queries to` 数据源列表，选择已配置的包含 dc 监控服务的腾讯云监控数据源。
3. 配置项的内容对齐腾讯云监控dc监控接口的输入参数，可参见 [专线接入-物理专线(DC)云监控接口文档](https://intl.cloud.tencent.com/document/product/248/10994)，更好地理解各配置项。
  - `Namespace` 命名空间，例如 `QCE/DC`。
  - `Region` 地域，地域列表会根据 `Namespace` 选项自动获取，单击选择某一地域。
  - `MetricName` 指标名称，指标列表会根据 `Namespace` 和 `Region` 选项自动获取，单击选择某一指标。
  - `Period` 监控统计周期，周期列表会根据 `MetricName` 选项自动获取，单击选择某一统计周期。
  - `Instance` 实例，对应输入参数的 `Instances.N` 字段，实例列表会自动获取。
    - 为了适应不同用户的习惯，实例列表会以不同的字段展示，默认为 `As DirectConnectId`，以 **专线ID** 展示实例列表。此外，可以选择 `As DirectConnectName` 专线名称。
    - 实例列表的获取可参见 [专线接入-物理专线(DC)列表接口文档](https://intl.cloud.tencent.com/document/product/216/35330)。切换 `Show Details` 为 `true`，可展示实例请求参数，默认参数为`Offset = 0` 和 `Limit = 20`。如果需要变更实例查询条件，可参见接口文档，配置相应参数。
    - **注意：** 在本应用中，监控数据的单次查询为原子操作，即查询某一实例的某一指标的监控数据，故实例只能单选，如需查询多实例的监控数据，单击右上角的 `Add Query` 增加新的查询。  
    - `Show Details` 按钮仅在选择非模板变量时显示。

![](https://main.qcloudimg.com/raw/c83992c63e875df31faf24a2e2162400.png)

## VPNGW 私有网络-VPN 网关

1. 单击 **New Panel** 面板的 **Add Query** 选项，进入 Panel 配置页面。在左侧第一个 `Query` 选项卡，通过配置选项获取腾讯云私有网络-VPN 网关(VPNGW)的监控数据。
2. `Queries to` 数据源列表，选择已配置的包含 vpngw 监控服务的腾讯云监控数据源。
3. 配置项的内容对齐腾讯云监控vpngw监控接口的输入参数，可参见 [私有网络-VPN 网关(VPNGW)云监控接口文档](https://intl.cloud.tencent.com/document/product/248/10988)，更好地理解各配置项。
  - `Namespace` 命名空间，例如 `QCE/VPNGW`。
  - `Region` 地域，地域列表会根据 `Namespace` 选项自动获取，单击选择某一地域。
  - `MetricName` 指标名称，指标列表会根据 `Namespace` 和 `Region` 选项自动获取，单击选择某一指标。
  - `Period` 监控统计周期，周期列表会根据 `MetricName` 选项自动获取，单击选择某一统计周期。
  - `Instance` 实例，对应输入参数的 `Instances.N` 字段，实例列表会自动获取。
    - 为了适应不同用户的习惯，实例列表会以不同的字段展示，默认为 `As VpnGatewayId`，以 **VPN网关ID** 展示实例列表。此外，可以选择 `As VpnGatewayName` VPN网关名称。
    - 实例列表的获取可参见 [私有网络-VPN 网关(VPNGW)列表接口文档](https://intl.cloud.tencent.com/document/api/215/17514)。切换 `Show Details` 为 `true`，可展示实例请求参数，默认参数为`Offset = 0` 和 `Limit = 20`。如果需要变更实例查询条件，可参见接口文档，配置相应参数。
    - **注意：** 在本应用中，监控数据的单次查询为原子操作，即查询某一实例的某一指标的监控数据，故实例只能单选，如需查询多实例的监控数据，单击右上角的 `Add Query` 增加新的查询。  
    - `Show Details` 按钮仅在选择非模板变量时显示。

![](https://main.qcloudimg.com/raw/290e06d4329f852118fd19526d65b08c.png)
    

## DCG 私有网络-专线网关

1. 单击 **New Panel** 面板的 **Add Query** 选项，进入 Panel 配置页面。在左侧第一个 `Query` 选项卡，通过配置选项获取腾讯云私有网络-专线网关(DCG)的监控数据。
2. `Queries to` 数据源列表，选择已配置的包含 dcg 监控服务的腾讯云监控数据源。
3. 配置项的内容对齐腾讯云监控dcg监控接口的输入参数，可参见 [私有网络-专线网关(DCG)云监控接口文档](https://intl.cloud.tencent.com/document/product/248/10990)，更好地理解各配置项。
  - `Namespace` 命名空间，例如 `QCE/DCG`。
  - `Region` 地域，地域列表会根据 `Namespace` 选项自动获取，单击选择某一地域。
  - `MetricName` 指标名称，指标列表会根据 `Namespace` 和 `Region` 选项自动获取，单击选择某一指标。
  - `Period` 监控统计周期，周期列表会根据 `MetricName` 选项自动获取，单击选择某一统计周期。
  - `Instance` 实例，对应输入参数的 `Instances.N` 字段，实例列表会自动获取。
    - 为了适应不同用户的习惯，实例列表会以不同的字段展示，默认为 `As DirectConnectGatewayId`，以 **专线网关ID** 展示实例列表。此外，可以选择 `As DirectConnectGatewayName` 专线网关名称。
    - 实例列表的获取可参见 [私有网络-专线网关(DCG)列表接口文档](https://intl.cloud.tencent.com/document/product/215/36913)。切换 `Show Details` 为 `true`，可展示实例请求参数，默认参数为`Offset = 0` 和 `Limit = 20`。如果需要变更实例查询条件，可参见接口文档，配置相应参数。
    - **注意：** 在本应用中，监控数据的单次查询为原子操作，即查询某一实例的某一指标的监控数据，故实例只能单选，如需查询多实例的监控数据，单击右上角的 `Add Query` 增加新的查询。  
    - `Show Details` 按钮仅在选择非模板变量时显示。

![](https://main.qcloudimg.com/raw/d354fc6078787541da65d05567758ca0.png)
    

## CDNPROVINCE 省份域名

1. 单击 **New Panel** 面板的 **Add Query** 选项，进入 Panel 配置页面。在左侧第一个 `Query` 选项卡，通过配置选项获取腾讯云省份域名(CDN_LOG_DATA)的监控数据。
2. `Queries to` 数据源列表，选择已配置的包含 cdnProvince 监控服务的腾讯云监控数据源。
3. 配置项的内容对齐腾讯云监控 cdnProvince 监控接口的输入参数，可参见 [省份域名(CDN_LOG_DATA)云监控接口文档](https://intl.cloud.tencent.com/document/product/248/39556)，更好地理解各配置项。
    - `Namespace` 命名空间，例如 `QCE/CDN_LOG_DATA`。
    - `Region` 地域，地域列表会根据 `Namespace` 选项自动获取，单击选择某一地域。
    - `MetricName` 指标名称，指标列表会根据 `Namespace` 和 `Region` 选项自动获取，单击选择某一指标。
    - `Period` 监控统计周期，周期列表会根据 `MetricName` 选项自动获取，单击选择某一统计周期。
    - `Instance` 实例，对应输入参数的 `Instances.N` 字段，实例列表会自动获取。
      - 为了适应不同用户的习惯，实例列表会以不同的字段展示，默认为 `As Domain`，以 **域名** 展示实例列表。此外，可以选择 `As ProjectId` 。
      - 实例列表的获取可参见 [省份域名(CDN_LOG_DATA)列表接口文档](https://intl.cloud.tencent.com/document/product/228/34020)。切换 `Show Details` 为 `true`，可展示实例请求参数，默认参数为`Offset = 0` 和 `Limit = 20`。如果需要变更实例查询条件，可参见接口文档，配置相应参数。
      - **注意：** 在本应用中，监控数据的单次查询为原子操作，即查询某一实例的某一指标的监控数据，故实例只能单选，如需查询多实例的监控数据，单击右上角的 `Add Query` 增加新的查询。  
      - `Show Details` 按钮仅在选择非模板变量时显示。
    - `Isp` 运营商列表。
    - `Province` 可选省份列表。


![](https://main.qcloudimg.com/raw/8135e3fcbbd3873eddf4d77c91e2e360.png)
    

## APIGATEWAY API 网关

1. 单击 **New Panel** 面板的 **Add Query** 选项，进入 Panel 配置页面。在左侧第一个 `Query` 选项卡，通过配置选项获取腾讯云API 网关(APIGATEWAY)的监控数据。
2. `Queries to` 数据源列表，选择已配置的包含 apigateway 监控服务的腾讯云监控数据源。
3. 配置项的内容对齐腾讯云监控apigateway监控接口的输入参数，可参见 [API 网关(APIGATEWAY)云监控接口文档](https://intl.cloud.tencent.com/document/product/248/19130)，更好地理解各配置项。
    - `Namespace` 命名空间，例如 `QCE/APIGATEWAY`。
    - `Region` 地域，地域列表会根据 `Namespace` 选项自动获取，单击选择某一地域。
    - `MetricName` 指标名称，指标列表会根据 `Namespace` 和 `Region` 选项自动获取，单击选择某一指标。
    - `Period` 监控统计周期，周期列表会根据 `MetricName` 选项自动获取，单击选择某一统计周期。
    - `Instance` 实例，对应输入参数的 `Instances.N` 字段，实例列表会自动获取。
      - 为了适应不同用户的习惯，实例列表会以不同的字段展示，默认为 `As ServiceId`，以 **协议端口 ID** 展示实例列表。此外，可以选择 `As ServiceName` 。
      - 实例列表的获取可参见 [API 网关(APIGATEWAY)列表接口文档](https://intl.cloud.tencent.com/document/product/628/36627)。切换 `Show Details` 为 `true`，可展示实例请求参数，默认参数为`Offset = 0` 和 `Limit = 20`。如果需要变更实例查询条件，可参见接口文档，配置相应参数。
      - **注意：** 在本应用中，监控数据的单次查询为原子操作，即查询某一实例的某一指标的监控数据，故实例只能单选，如需查询多实例的监控数据，单击右上角的 `Add Query` 增加新的查询。  
      - `Show Details` 按钮仅在选择非模板变量时显示。
    - `EnvironmentName` 环境名称，会根据上面Instance内容获取。


![](https://main.qcloudimg.com/raw/c7bcc133e8decde3a9f6814e2b7de4a5.png)
    

## CBS 云硬盘

1. 单击 **New Panel** 面板的 **Add Query** 选项，进入 Panel 配置页面。在左侧第一个 `Query` 选项卡，通过配置选项获取腾讯云云硬盘(BLOCK_STORAGE)的监控数据。
2. `Queries to` 数据源列表，选择已配置的包含 cbs 监控服务的腾讯云监控数据源。
3. 配置项的内容对齐腾讯云监控cbs监控接口的输入参数，可参见 [云硬盘(BLOCK_STORAGE)云监控接口文档](https://intl.cloud.tencent.com/document/product/248/37085)，更好地理解各配置项。
  - `Namespace` 命名空间，例如 `QCE/BLOCK_STORAGE`。
  - `Region` 地域，地域列表会根据 `Namespace` 选项自动获取，单击选择某一地域。
  - `MetricName` 指标名称，指标列表会根据 `Namespace` 和 `Region` 选项自动获取，单击选择某一指标。
  - `Period` 监控统计周期，周期列表会根据 `MetricName` 选项自动获取，单击选择某一统计周期。
  - `Instance` 实例，对应输入参数的 `Instances.N` 字段，实例列表会自动获取。
    - 为了适应不同用户的习惯，实例列表会以不同的字段展示，默认为 `As DiskId`，以 **云硬盘ID** 展示实例列表。此外，可以选择 `As DiskName` 云硬盘名称。
    - 实例列表的获取可参见 [云硬盘(BLOCK_STORAGE)列表接口文档](https://intl.cloud.tencent.com/document/api/362/16315)。切换 `Show Details` 为 `true`，可展示实例请求参数，默认参数为`Offset = 0` 和 `Limit = 20`。如果需要变更实例查询条件，可参见接口文档，配置相应参数。
    - **注意：** 在本应用中，监控数据的单次查询为原子操作，即查询某一实例的某一指标的监控数据，故实例只能单选，如需查询多实例的监控数据，单击右上角的 `Add Query` 增加新的查询。  
    - `Show Details` 按钮仅在选择非模板变量时显示。

![](https://main.qcloudimg.com/raw/be10b0c4c15255344379f549f56a8f7d.png)
    

## CES Elasticsearch指标

1. 单击 **New Panel** 面板的 **Add Query** 选项，进入 Panel 配置页面。在左侧第一个 `Query` 选项卡，通过配置选项获取腾讯云Elasticsearch指标(CES)的监控数据。
2. `Queries to` 数据源列表，选择已配置的包含 ces 监控服务的腾讯云监控数据源。
3. 配置项的内容对齐腾讯云监控ces监控接口的输入参数，可参见 [Elasticsearch指标(CES)云监控接口文档](https://intl.cloud.tencent.com/document/product/248/34642)，更好地理解各配置项。
  - `Namespace` 命名空间，例如 `QCE/CES`。
  - `Region` 地域，地域列表会根据 `Namespace` 选项自动获取，单击选择某一地域。
  - `MetricName` 指标名称，指标列表会根据 `Namespace` 和 `Region` 选项自动获取，单击选择某一指标。
  - `Period` 监控统计周期，周期列表会根据 `MetricName` 选项自动获取，单击选择某一统计周期。
  - `Instance` 实例，对应输入参数的 `Instances.N` 字段，实例列表会自动获取。
    - 为了适应不同用户的习惯，实例列表会以不同的字段展示，默认为 `As InstanceId`，以 **实例ID** 展示实例列表。此外，可以选择 `As InstanceName` 实例名称。
    - 实例列表的获取可参见 [Elasticsearch指标(CES)列表接口文档](https://intl.cloud.tencent.com/document/product/845/32214)。切换 `Show Details` 为 `true`，可展示实例请求参数，默认参数为`Offset = 0` 和 `Limit = 20`。如果需要变更实例查询条件，可参见接口文档，配置相应参数。
    - **注意：** 在本应用中，监控数据的单次查询为原子操作，即查询某一实例的某一指标的监控数据，故实例只能单选，如需查询多实例的监控数据，单击右上角的 `Add Query` 增加新的查询。  
    - `Show Details` 按钮仅在选择非模板变量时显示。

![](https://main.qcloudimg.com/raw/18ff8a75e3f4259bf0b613107f42335d.png)
    

## CMQ 消息队列服务监控

1. 单击 **New Panel** 面板的 **Add Query** 选项，进入 Panel 配置页面。在左侧第一个 `Query` 选项卡，通过配置选项获取腾讯云消息队列CMQ(队列服务监控CMQ)的监控数据。
2. `Queries to` 数据源列表，选择已配置的包含 cmq 监控服务的腾讯云监控数据源。
3. 配置项的内容对齐腾讯云监控cmq监控接口的输入参数，可参见 [消息队列CMQ(队列服务监控CMQ)云监控接口文档](https://intl.cloud.tencent.com/document/product/248/34643)，更好地理解各配置项。
  - `Namespace` 命名空间，例如 `QCE/CMQ`。
  - `Region` 地域，地域列表会根据 `Namespace` 选项自动获取，单击选择某一地域。
  - `MetricName` 指标名称，指标列表会根据 `Namespace` 和 `Region` 选项自动获取，单击选择某一指标。
  - `Period` 监控统计周期，周期列表会根据 `MetricName` 选项自动获取，单击选择某一统计周期。
  - `Instance` 实例，对应输入参数的 `Instances.N` 字段，实例列表会自动获取。
    - 为了适应不同用户的习惯，实例列表会以不同的字段展示，默认为 `As QueueName`，以 **队列名称** 展示实例列表。此外，可以选择 `As QueueId` 队列ID。
    - 实例列表的获取可参见 [消息队列CMQ(队列服务监控CMQ)列表接口文档](https://intl.cloud.tencent.com/document/product/406/35944)。切换 `Show Details` 为 `true`，可展示实例请求参数，默认参数为`Offset = 0` 和 `Limit = 20`。如果需要变更实例查询条件，可参见接口文档，配置相应参数。
    - **注意：** 在本应用中，监控数据的单次查询为原子操作，即查询某一实例的某一指标的监控数据，故实例只能单选，如需查询多实例的监控数据，单击右上角的 `Add Query` 增加新的查询。  
    - `Show Details` 按钮仅在选择非模板变量时显示。

![](https://main.qcloudimg.com/raw/f4ce3fe963ee384797fbf8162e095da3.png)
    

## CMQTOPIC 消息队列主题订阅监控

1. 单击 **New Panel** 面板的 **Add Query** 选项，进入 Panel 配置页面。在左侧第一个 `Query` 选项卡，通过配置选项获取腾讯云消息队列CMQTOPIC(主题订阅监控)的监控数据。
2. `Queries to` 数据源列表，选择已配置的包含 cmqTopic 监控服务的腾讯云监控数据源。
3. 配置项的内容对齐腾讯云监控cmqTopic监控接口的输入参数，可参见 [消息队列CMQTOPIC(主题订阅监控)云监控接口文档](https://intl.cloud.tencent.com/document/product/248/11013)，更好地理解各配置项。
  - `Namespace` 命名空间，例如 `QCE/CMQTOPIC`。
  - `Region` 地域，地域列表会根据 `Namespace` 选项自动获取，单击选择某一地域。
  - `MetricName` 指标名称，指标列表会根据 `Namespace` 和 `Region` 选项自动获取，单击选择某一指标。
  - `Period` 监控统计周期，周期列表会根据 `MetricName` 选项自动获取，单击选择某一统计周期。
  - `Instance` 实例，对应输入参数的 `Instances.N` 字段，实例列表会自动获取。
    - 为了适应不同用户的习惯，实例列表会以不同的字段展示，默认为 `As TopicName`，以 **主题名称** 展示实例列表。此外，可以选择 `As TopicId` 主题ID。
    - 实例列表的获取可参见 [消息队列CMQTOPIC(主题订阅监控)列表接口文档](https://intl.cloud.tencent.com/document/product/406/35931)。切换 `Show Details` 为 `true`，可展示实例请求参数，默认参数为`Offset = 0` 和 `Limit = 20`。如果需要变更实例查询条件，可参见接口文档，配置相应参数。
    - **注意：** 在本应用中，监控数据的单次查询为原子操作，即查询某一实例的某一指标的监控数据，故实例只能单选，如需查询多实例的监控数据，单击右上角的 `Add Query` 增加新的查询。  
    - `Show Details` 按钮仅在选择非模板变量时显示。

![](https://main.qcloudimg.com/raw/950d8ceea76ff95ce3df8c532baf6d2c.png)
