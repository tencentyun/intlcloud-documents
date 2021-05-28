After creating a dashboard, you can configure the panel information to get the monitoring data from Tencent Cloud Monitor. The following describes how to do so by taking Graph as an example.

## CVM Monitoring

1. Click **Add Query** in **New Panel** to go to the panel configuration page. On the `Query` tab on the left, configure the options to get the monitoring data of CVM.
2. Select the configured Tencent Cloud Monitor data source that includes CVM monitoring from the `Queries to` data source list.
3. Use the input parameters of the CVM monitoring API for the configuration items here. For more information on the configuration items, please see [here](https://intl.cloud.tencent.com/document/product/248/6843).
    - `Namespace`: select a namespace. The namespace of CVM monitoring is `QCE/CVM`.
    - `Region`: select a region. The region list will be automatically obtained according to the `Namespace` option.
    - `MetricName`: select a metric name. The metric list will be automatically obtained according to the `Namespace` and `Region` options.
    - `Period`: select a statistical period. The period list will be automatically obtained according to the `MetricName` option.
    - `Instance`: select an instance, which corresponds to the `Instances.N` field of the input parameter. The instance list will be automatically obtained.
      - To adapt to the habits of different users, the instance list is displayed as different fields, which is `As InstanceId` by default, meaning that the instance list is displayed as **instance IDs**. You can also select `As InstanceName` (as instance names), `As PrivateIpAddress` (as private IPs of primary ENIs), or `As PublicIpAddress` (as public IPs of primary ENIs).
      - For more information on how to get the instance list, please see [here](https://intl.cloud.tencent.com/document/product/213/33258). You can toggle `Show Details` to `true` to display the instance request parameters, which are `Offset = 0` and `Limit = 20` by default. If you need to change the instance query criteria, you can configure corresponding parameters as instructed in the API documentation.
      - **Note:** In this application, a single query to get the monitoring data is an atomic operation, i.e., querying the monitoring data of a certain metric of a certain instance. Therefore, you can select only one instance at a time. If you need to query the monitoring data of multiple instances, you can click `Add Query` in the upper-right corner to add new queries.
      - The `Show Details` button is displayed only when a non-template variable is selected.

![](https://main.qcloudimg.com/raw/f36a04815d5d0c2157ef8450df658b1f.png)

## TencentDB for MySQL

1. Click **Add Query** in **New Panel** to enter the panel configuration page. On the `Query` tab on the left, configure the options to get the monitoring data of TencentDB for MySQL.
2. Select the configured Tencent Cloud Monitor data source that includes TencentDB for MySQL monitoring from the `Queries to` data source list.
3. Use the input parameters of the TencentDB for MySQL monitoring API for the configuration items here. For more information on the configuration items, please see [here](https://intl.cloud.tencent.com/document/product/248/11006).
    - `Namespace`: select a namespace. The namespace of TencentDB monitoring is `QCE/CDB`.
    - `Region`: select a region. The region list will be automatically obtained according to the `Namespace` option.
    - `MetricName`: select a metric name. The metric list will be automatically obtained according to the `Namespace` and `Region` options.
    - `Period`: select a statistical period. The period list will be automatically obtained according to the `MetricName` option.
    - `Instance`: select an instance, which corresponds to the `Instances.N` field of the input parameter. The instance list will be automatically obtained.
      - To adapt to the habits of different users, the instance list is displayed as different fields, which is `As InstanceId` by default, meaning that the instance list is displayed as **instance IDs**. You can also select `As InstanceName` (as instance names) and `As Vip` (as private IPs).
      - For more information on how to get the instance list, please see [here](https://intl.cloud.tencent.com/document/api/236/15872). You can toggle `Show Details` to `true` to display the instance request parameters, which are `Offset = 0` and `Limit = 20` by default. If you need to change the instance query criteria, you can configure corresponding parameters as instructed in the API documentation.
      - **Note:** In this application, a single query to get the monitoring data is an atomic operation, i.e., querying the monitoring data of a certain metric of a certain instance. Therefore, you can select only one instance at a time. If you need to query the monitoring data of multiple instances, you can click `Add Query` in the upper-right corner to add new queries.  
      - The `Show Details` button is displayed only when a non-template variable is selected.

![](https://main.qcloudimg.com/raw/fa269951d10a6bef77517b49bf15dc57.png)

## TencentDB for PostgreSQL

1. Click **Add Query** in **New Panel** to enter the panel configuration page. On the `Query` tab on the left, configure the options to get the monitoring data of TencentDB for PostgreSQL.
2. Select the configured Tencent Cloud Monitor data source that includes TencentDB for PostgreSQL monitoring from the `Queries to` data source list.
3. Use the input parameters of the TencentDB for PostgreSQL monitoring API for the configuration items here. For more information on the configuration items, please see [here](https://intl.cloud.tencent.com/document/product/248/17945).
    - `Namespace`: select a namespace. The namespace of TencentDB for PostgreSQL monitoring is `QCE/POSTGRES`.
    - `Region`: select a region. The region list will be automatically obtained according to the `Namespace` option.
    - `MetricName`: select a metric name. The metric list will be automatically obtained according to the `Namespace` and `Region` options.
    - `Period`: select a statistical period. The period list will be automatically obtained according to the `MetricName` option.
    - `Instance`: select an instance, which corresponds to the `Instances.N` field of the input parameter. The instance list will be automatically obtained.
      - To adapt to the habits of different users, the instance list is displayed as different fields, which is `As InstanceId` by default, meaning that the instance list is displayed as **instance IDs**. You can also select `As DBInstanceName` (as database names), `PrivateIpAddresses` (as private IPs), or `PublicIpAddresses` (as public IPs).
      - For more information on how to get the instance list, please see [here](https://intl.cloud.tencent.com/document/api/409/16773). You can toggle `Show Details` to `true` to display the instance request parameters, which are `Offset = 0` and `Limit = 20` by default. If you need to change the instance query criteria, you can configure corresponding parameters as instructed in the API documentation.
      - **Note:** In this application, a single query to get the monitoring data is an atomic operation, i.e., querying the monitoring data of a certain metric of a certain instance. Therefore, you can select only one instance at a time. If you need to query the monitoring data of multiple instances, you can click `Add Query` in the upper-right corner to add new queries.  
      - The `Show Details` button is displayed only when a non-template variable is selected.

![](https://main.qcloudimg.com/raw/23b08f6712bf0ab80a7fea0fdc1194dd.png)

## TencentDB for MongoDB

1. Click **Add Query** in **New Panel** to enter the panel configuration page. On the `Query` tab on the left, configure the options to get the monitoring data of TencentDB for MongoDB.
2. Select the configured Tencent Cloud Monitor data source that includes TencentDB for MongoDB monitoring from the `Queries to` data source list.
3. Use the input parameters of the TencentDB for MongoDB monitoring API for the configuration items here. For more information on the configuration items, please see [here](https://intl.cloud.tencent.com/document/product/248/35671).
    - `Namespace`: select a namespace, for example, `QCE/CMONGO`.
    - `Region`: select a region. The region list will be automatically obtained according to the `Namespace` option.
    - `MetricName`: select a metric name. The metric list will be automatically obtained according to the `Namespace` and `Region` options.
    - `Period`: select a statistical period. The period list will be automatically obtained according to the `MetricName` option.
    - `Instance`: select an instance, which corresponds to the `Instances.N` field of the input parameter. The instance list will be automatically obtained.
      - To adapt to the habits of different users, the instance list is displayed as different fields, which is `As InstanceId` by default, meaning that the instance list is displayed as **instance IDs**. You can also select `As InstanceName` (as instance names).
      - For more information on how to get the instance list, please see [here](https://intl.cloud.tencent.com/document/product/240/34702). You can toggle `Show Details` to `true` to display the instance request parameters, which are `Offset = 0` and `Limit = 20` by default. If you need to change the instance query criteria, you can configure corresponding parameters as instructed in the API documentation.
      - **Note:** In this application, a single query to get the monitoring data is an atomic operation, i.e., querying the monitoring data of a certain metric of a certain instance. Therefore, you can select only one instance at a time. If you need to query the monitoring data of multiple instances, you can click `Add Query` in the upper-right corner to add new queries.  
      - The `Show Details` button is displayed only when a non-template variable is selected.

![](https://main.qcloudimg.com/raw/e631aa55f937e03aa5a7a90fbaaf4cde.png)

## TencentDB for Redis

1. Click **Add Query** in **New Panel** to enter the panel configuration page. On the `Query` tab on the left, configure the options to get the monitoring data of TencentDB for Redis.
2. Select the configured Tencent Cloud Monitor data source that includes TencentDB for Redis monitoring from the `Queries to` data source list.
3. TencentDB for Redis metrics are divided into two namespaces: Memory Edition (5-second) (Namespace=QCE/REDIS_MEM) and CKV Edition and Memory Edition (1-minute) (Namespace=QCE/REDIS). You can select a value in `Namespace` as needed.
4. Use the input parameters of the TencentDB for Redis monitoring API for the configuration items here. For more information on the configuration items, please see [here](https://intl.cloud.tencent.com/document/product/248/39507).
    - `Namespace`: select a namespace, for example, `QCE/REDIS_MEM`.
    - `Region`: select a region. The region list will be automatically obtained according to the `Namespace` option.
    - `MetricName`: select a metric name. The metric list will be automatically obtained according to the `Namespace` and `Region` options.
    - `Period`: select a statistical period. The period list will be automatically obtained according to the `MetricName` option.
    - `Instance`: select an instance, which corresponds to the `Instances.N` field of the input parameter. The instance list will be automatically obtained.
      - To adapt to the habits of different users, the instance list is displayed as different fields, which is `As InstanceId` by default, meaning that the instance list is displayed as **instance IDs**. You can also select `As InstanceName` (as instance names).
      - For more information on how to get the instance list, please see [here](https://intl.cloud.tencent.com/document/product/239/32065). You can toggle `Show Details` to `true` to display the instance request parameters, which are `Offset = 0` and `Limit = 20` by default. If you need to change the instance query criteria, you can configure corresponding parameters as instructed in the API documentation.
      - **Note:** In this application, a single query to get the monitoring data is an atomic operation, i.e., querying the monitoring data of a certain metric of a certain instance. Therefore, you can select only one instance at a time. If you need to query the monitoring data of multiple instances, you can click `Add Query` in the upper-right corner to add new queries.  
      - The `Show Details` button is displayed only when a non-template variable is selected.

![](https://main.qcloudimg.com/raw/88d13ac80ec80bc2696371b43312f506.png)

## TencentDB for CYNOSDB_MYSQL

  1. Click **Add Query** in **New Panel** to enter the panel configuration page. On the `Query` tab on the left, configure the options to get the monitoring data of TencentDB for CYNOSDB_MYSQL.
  2. Select the configured Tencent Cloud Monitor data source that includes TencentDB for CYNOSDB_MYSQL monitoring from the `Queries to` data source list.
  3. Use the input parameters of the TencentDB for CYNOSDB_MYSQL monitoring API for the configuration items here. For more information on the configuration items, please see [here](https://intl.cloud.tencent.com/document/product/248/37383).

    - `Namespace`: select a namespace, for example, `QCE/CYNOSDB_MYSQL`.
    - `Region`: select a region. The region list will be automatically obtained according to the `Namespace` option.
    - `MetricName`: select a metric name. The metric list will be automatically obtained according to the `Namespace` and `Region` options.
    - `Period`: select a statistical period. The period list will be automatically obtained according to the `MetricName` option.
    - `Instance`: select an instance, which corresponds to the `Instances.N` field of the input parameter. The instance list will be automatically obtained.
      - To adapt to the habits of different users, the instance list is displayed as different fields, which is `As InstanceId` by default, meaning that the instance list is displayed as **instance IDs**. You can also select `As InstanceName` (as instance names).
      - You can toggle `Show Details` to `true` to display the instance request parameters, which are `Offset = 0` and `Limit = 20` by default. If you need to change the instance query criteria, you can configure corresponding parameters as instructed in the API documentation.
      - **Note:** In this application, a single query to get the monitoring data is an atomic operation, i.e., querying the monitoring data of a certain metric of a certain instance. Therefore, you can select only one instance at a time. If you need to query the monitoring data of multiple instances, you can click `Add Query` in the upper-right corner to add new queries.  
      - The `Show Details` button is displayed only when a non-template variable is selected.

![](https://main.qcloudimg.com/raw/713309fe64571e80c221d7b110712c8e.png)
    

## TencentDB for TcaplusDB

1. Click **Add Query** in **New Panel** to enter the panel configuration page. On the `Query` tab on the left, configure the options to get the monitoring data of TencentDB for TcaplusDB.
2. Select the configured Tencent Cloud Monitor data source that includes TencentDB for TcaplusDB monitoring from the `Queries to` data source list.
3. Use the input parameters of the TencentDB for TcaplusDBL monitoring API for the configuration items here. For more information on the configuration items, please see [here](https://intl.cloud.tencent.com/document/product/248/34592).
  - `Namespace`: select a namespace, for example, `QCE/TCAPLUS`.
  - `Region`: select a region. The region list will be automatically obtained according to the `Namespace` option.
  - `MetricName`: select a metric name. The metric list will be automatically obtained according to the `Namespace` and `Region` options.
  - `Period`: select a statistical period. The period list will be automatically obtained according to the `MetricName` option.
  - `Instance`: select an instance, which corresponds to the `Instances.N` field of the input parameter. The instance list will be automatically obtained.
    - To adapt to the habits of different users, the instance list is displayed as different fields, which is `As InstanceId` by default, meaning that the instance list is displayed as **instance IDs**. You can also select `As InstanceName` (as instance names).
    - For more information on how to get the instance list, please see [here](https://intl.cloud.tencent.com/zh/document/product/1016/3505). You can toggle `Show Details` to `true` to display the instance request parameters, which are `Offset = 0` and `Limit = 20` by default. If you need to change the instance query criteria, you can configure corresponding parameters as instructed in the API documentation.
    - **Note:** In this application, a single query to get the monitoring data is an atomic operation, i.e., querying the monitoring data of a certain metric of a certain instance. Therefore, you can select only one instance at a time. If you need to query the monitoring data of multiple instances, you can click `Add Query` in the upper-right corner to add new queries.  
    - The `Show Details` button is displayed only when a non-template variable is selected.

![](https://main.qcloudimg.com/raw/cd365a087b317d0af25daed5161651c4.png)

## TencentDB for SQL Server

1. Click **Add Query** in **New Panel** to enter the panel configuration page. On the `Query` tab on the left, configure the options to get the monitoring data of TencentDB for SQL Server.
2. Select the configured Tencent Cloud Monitor data source that includes TencentDB for SQL Server monitoring from the `Queries to` data source list.
3. Use the input parameters of the TencentDB for SQL Server monitoring API for the configuration items here. For more information on the configuration items, please see [here](https://intl.cloud.tencent.com/document/product/248/11008).
  - `Namespace`: select a namespace, for example, `QCE/SQLSERVER`.
  - `Region`: select a region. The region list will be automatically obtained according to the `Namespace` option.
  - `MetricName`: select a metric name. The metric list will be automatically obtained according to the `Namespace` and `Region` options.
  - `Period`: select a statistical period. The period list will be automatically obtained according to the `MetricName` option.
  - `Instance`: select an instance, which corresponds to the `Instances.N` field of the input parameter. The instance list will be automatically obtained.
    - To adapt to the habits of different users, the instance list is displayed as different fields, which is `As InstanceId` by default, meaning that the instance list is displayed as **instance IDs**. You can also select `As Name` (as instance names).
    - For more information on how to get the instance list, please see [here](https://intl.cloud.tencent.com/document/product/238/32115). You can toggle `Show Details` to `true` to display the instance request parameters, which are `Offset = 0` and `Limit = 20` by default. If you need to change the instance query criteria, you can configure corresponding parameters as instructed in the API documentation.
    - **Note:** In this application, a single query to get the monitoring data is an atomic operation, i.e., querying the monitoring data of a certain metric of a certain instance. Therefore, you can select only one instance at a time. If you need to query the monitoring data of multiple instances, you can click `Add Query` in the upper-right corner to add new queries.  
    - The `Show Details` button is displayed only when a non-template variable is selected.

![](https://main.qcloudimg.com/raw/abe8a325cd0ee17114f8eae4b76068d9.png)

## Content Delivery Network (CDN)

1. Click **Add Query** in **New Panel** to go to the panel configuration page. On the `Query` tab on the left, configure the options to get the monitoring data of CDN.
2. Select the configured Tencent Cloud Monitor data source that includes CDN monitoring from the `Queries to` data source list.
3. CDN metrics are divided into two namespaces: domain name in the Chinese mainland (Namespace=QCE/CDN) and domain name outside the Chinese mainland (Namespace=QCE/OV_CDN). You can select a value in `Namespace` as needed.
4. Use the input parameters of the CDN monitoring API for the configuration items here. For more information on the configuration items, please see [here](https://intl.cloud.tencent.com/document/product/248/39554).
    - `Namespace`: select a namespace, for example, `QCE/CDN`.
    - `Region`: select a region. The region list will be automatically obtained according to the `Namespace` option.
    - `MetricName`: select a metric name. The metric list will be automatically obtained according to the `Namespace` and `Region` options.
    - `Period`: select a statistical period. The period list will be automatically obtained according to the `MetricName` option.
    - `Instance`: select an instance, which corresponds to the `Instances.N` field of the input parameter. The instance list will be automatically obtained.
      - To adapt to the habits of different users, the instance list is displayed as different fields, which is `As Domain` by default, meaning that the instance list is displayed as **domain names**. You can also select `As ProjectId` (as project IDs).
      - For more information on how to get the domain name list, please see [here](https://intl.cloud.tencent.com/document/product/228/34020). You can toggle `Show Details` to `true` to display the instance request parameters, which are `Offset = 0` and `Limit = 20` by default. If you need to change the instance query criteria, you can configure corresponding parameters as instructed in the API documentation.
      - **Note:** In this application, a single query to get the monitoring data is an atomic operation, i.e., querying the monitoring data of a certain metric of a certain instance. Therefore, you can select only one instance at a time. If you need to query the monitoring data of multiple instances, you can click `Add Query` in the upper-right corner to add new queries.  
      - The `Show Details` button is displayed only when a non-template variable is selected.

## Bandwidth Package (BWP)

1. Click **Add Query** in **New Panel** to go to the panel configuration page. On the `Query` tab on the left, configure the options to get the monitoring data of BWP.
2. Select the configured Tencent Cloud Monitor data source that includes BWP monitoring from the `Queries to` data source list.
3. Use the input parameters of the BWP monitoring API for the configuration items here. For more information on the configuration items, please see [here](https://intl.cloud.tencent.com/document/product/248/34645).
    - `Namespace`: select a namespace, for example, `QCE/BWP`.
    - `Region`: select a region. The region list will be automatically obtained according to the `Namespace` option.
    - `MetricName`: select a metric name. The metric list will be automatically obtained according to the `Namespace` and `Region` options.
    - `Period`: select a statistical period. The period list will be automatically obtained according to the `MetricName` option.
    - `Instance`: select an instance, which corresponds to the `Instances.N` field of the input parameter. The instance list will be automatically obtained.
      - To adapt to the habits of different users, the instance list is displayed as different fields, which is `As BandwidthPackageId` by default, meaning that the instance list is displayed as **package IDs**. You can also select `As BandwidthPackageName` (as package names).
      - For more information on how to get the domain name list, please see [here](https://intl.cloud.tencent.com/document/product/215/36919). You can toggle `Show Details` to `true` to display the instance request parameters, which are `Offset = 0` and `Limit = 20` by default. If you need to change the instance query criteria, you can configure corresponding parameters as instructed in the API documentation.
      - **Note:** In this application, a single query to get the monitoring data is an atomic operation, i.e., querying the monitoring data of a certain metric of a certain instance. Therefore, you can select only one instance at a time. If you need to query the monitoring data of multiple instances, you can click `Add Query` in the upper-right corner to add new queries.  
      - The `Show Details` button is displayed only when a non-template variable is selected.

![](https://main.qcloudimg.com/raw/5ab6db7adb0dfe9ab98258b84d44ee95.png)

## Message Queue CKafka

1. Click **Add Query** in **New Panel** to go to the panel configuration page. On the `Query` tab on the left, configure the options to get the monitoring data of CKafka.
2. Select the configured Tencent Cloud Monitor data source that includes CKafka monitoring from the `Queries to` data source list.
3. Use the input parameters of the CKafka monitoring API for the configuration items here. For more information on the configuration items, please see [here](https://intl.cloud.tencent.com/document/product/248/17297).
    - `Namespace`: select a namespace, for example, `QCE/CKAFKA`.
    - `Region`: select a region. The region list will be automatically obtained according to the `Namespace` option.
    - `MetricName`: select a metric name. The metric list will be automatically obtained according to the `Namespace` and `Region` options.
    - `Period`: select a statistical period. The period list will be automatically obtained according to the `MetricName` option.
    - `Instance`: select an instance, which corresponds to the `Instances.N` field of the input parameter. The instance list will be automatically obtained.
      - To adapt to the habits of different users, the instance list is displayed as different fields, which is `As InstanceId` by default, meaning that the instance list is displayed as **instance IDs**. You can also select `As InstanceName` (as instance names).
      - For more information on how to get the instance list, please see [here](https://intl.cloud.tencent.com/document/product/597/35357). You can toggle `Show Details` to `true` to display the instance request parameters, which are `Offset = 0` and `Limit = 10` by default. If you need to change the instance query criteria, you can configure corresponding parameters as instructed in the API documentation.
      - **Note:** In this application, a single query to get the monitoring data is an atomic operation, i.e., querying the monitoring data of a certain metric of a certain instance. Therefore, you can select only one instance at a time. If you need to query the monitoring data of multiple instances, you can click `Add Query` in the upper-right corner to add new queries.  
      - The `Show Details` button is displayed only when a non-template variable is selected.

![](https://main.qcloudimg.com/raw/a4dbbbc2012ef393cc87419d7e531b2b.png)

## Cloud Load Balancer (CLB)

1. Click **Add Query** in **New Panel** to go to the panel configuration page. On the `Query` tab on the left, configure the options to get the monitoring data of CLB.
2. Select the configured Tencent Cloud Monitor data source that includes CLB monitoring from the `Queries to` data source list.
3. CLB metrics are divided into three namespaces: public network CLB monitoring metrics (Namespace=QCE/LB_PUBLIC), private network layer-4 CLB protocol monitoring metrics (Namespace=QCE/LB_PRIVATE), and layer-7 protocol monitoring metrics (Namespace=QCE/LOADBALANCE). You can select a value in `Namespace` as needed.
4. Use the input parameters of the CVM monitoring API for the configuration items here. For more information on the configuration items, please see [here](https://intl.cloud.tencent.com/document/product/248/10997).
    - `Namespace`: select a namespace, for example, `QCE/LB_PUBLIC`.
    - `Region`: select a region. The region list will be automatically obtained according to the `Namespace` option.
    - `MetricName`: select a metric name. The metric list will be automatically obtained according to the `Namespace` and `Region` options.
    - `Period`: select a statistical period. The period list will be automatically obtained according to the `MetricName` option.
    - `Instance`: select an instance, which corresponds to the `Instances.N` field of the input parameter. The instance list will be automatically obtained.
      - To adapt to the habits of different users, the instance list is displayed as different fields, which is `As LoadBalancerId` by default, meaning that the instance list is displayed as **instance IDs**. You can also select `As LoadBalancerName` (as instance names) or `As LoadBalancerVips` (as IPs).
      - For more information on how to get the instance list, please see [here](https://intl.cloud.tencent.com/document/product/214/33830). You can toggle `Show Details` to `true` to display the instance request parameters, which are `Offset = 0` and `Limit = 20` by default. If you need to change the instance query criteria, you can configure corresponding parameters as instructed in the API documentation.
      - **Note:** In this application, a single query to get the monitoring data is an atomic operation, i.e., querying the monitoring data of a certain metric of a certain instance. Therefore, you can select only one instance at a time. If you need to query the monitoring data of multiple instances, you can click `Add Query` in the upper-right corner to add new queries.  
      - The `Show Details` button is displayed only when a non-template variable is selected.
    - `Listener`: select a listener, which is **optional**. At this time, the instance dimension is used for request, which corresponds to the `Listener.N` field of the input parameter. The list will be automatically obtained.
      - To adapt to the habits of different users, the listener list is displayed as different fields, which is `As ListenerId` by default, meaning that the listener list is displayed as **listener IDs**. You can also select `As ListenerName` (as listener names) or `As Port` (as ports).
      - For more information on how to get the listener list, please see [here](https://intl.cloud.tencent.com/document/product/214/33831).

![](https://main.qcloudimg.com/raw/f0e32efbe3df41460ca53380baff3d25.png)

## Elastic IP (EIP)

1. Click **Add Query** in **New Panel** to go to the panel configuration page. On the `Query` tab on the left, configure the options to get the monitoring data of EIP.
2. Select the configured Tencent Cloud Monitor data source that includes EIP monitoring from the `Queries to` data source list.
3. Use the input parameters of the EIP monitoring API for the configuration items here. For more information on the configuration items, please see [here](https://intl.cloud.tencent.com/document/product/248/34646).
    - `Namespace`: select a namespace, for example, `QCE/LB`.
    - `Region`: select a region. The region list will be automatically obtained according to the `Namespace` option.
    - `MetricName`: select a metric name. The metric list will be automatically obtained according to the `Namespace` and `Region` options.
    - `Period`: select a statistical period. The period list will be automatically obtained according to the `MetricName` option.
    - `Instance`: select an instance, which corresponds to the `Instances.N` field of the input parameter. The instance list will be automatically obtained.
      - To adapt to the habits of different users, the instance list is displayed as different fields, which is `As AddressId` by default, meaning that the instance list is displayed as **instance address IDs**. You can also select `As AddressName` (as address names) or `As AddressIp` (as address IPs).
      - For more information on how to get the instance list, please see [here](https://intl.cloud.tencent.com/document/api/215/16702). You can toggle `Show Details` to `true` to display the instance request parameters, which are `Offset = 0` and `Limit = 20` by default. If you need to change the instance query criteria, you can configure corresponding parameters as instructed in the API documentation.
      - **Note:** In this application, a single query to get the monitoring data is an atomic operation, i.e., querying the monitoring data of a certain metric of a certain instance. Therefore, you can select only one instance at a time. If you need to query the monitoring data of multiple instances, you can click `Add Query` in the upper-right corner to add new queries.  
      - The `Show Details` button is displayed only when a non-template variable is selected.

![](https://main.qcloudimg.com/raw/b9b926cd1a5e4720a99edaa1bd84dc21.png)

## Cloud File Storage (CFS)

1. Click **Add Query** in **New Panel** to go to the panel configuration page. On the `Query` tab on the left, configure the options to get the monitoring data of CFS.
2. Select the configured Tencent Cloud Monitor data source that includes CFS monitoring from the `Queries to` data source list.
3. Use the input parameters of the CFS monitoring API for the configuration items here. For more information on the configuration items, please see [here](https://intl.cloud.tencent.com/document/product/248/34644).
    - `Namespace`: select a namespace, for example, `QCE/CFS`.
    - `Region`: select a region. The region list will be automatically obtained according to the `Namespace` option.
    - `MetricName`: select a metric name. The metric list will be automatically obtained according to the `Namespace` and `Region` options.
    - `Period`: select a statistical period. The period list will be automatically obtained according to the `MetricName` option.
    - `Instance`: select an instance, which corresponds to the `Instances.N` field of the input parameter. The instance list will be automatically obtained.
      - To adapt to the habits of different users, the instance list is displayed as different fields, which is `As FileSystemId` by default, meaning that the instance list is displayed as **file system IDs**. You can also select `As FsName` (as file system names).
      - For more information on how to get the instance list, please see [here](https://intl.cloud.tencent.com/document/product/582/34514). You can toggle `Show Details` to `true` to display the instance request parameters, which are `Offset = 0` and `Limit = 20` by default. If you need to change the instance query criteria, you can configure corresponding parameters as instructed in the API documentation.
      - **Note:** In this application, a single query to get the monitoring data is an atomic operation, i.e., querying the monitoring data of a certain metric of a certain instance. Therefore, you can select only one instance at a time. If you need to query the monitoring data of multiple instances, you can click `Add Query` in the upper-right corner to add new queries.  
      - The `Show Details` button is displayed only when a non-template variable is selected.

![](https://main.qcloudimg.com/raw/419b5c2db298315be1d8a704cc8c8b5d.png)

## Serverless Cloud Function (SCF)

1. Click **Add Query** in **New Panel** to go to the panel configuration page. On the `Query` tab on the left, configure the options to get the monitoring data of SCF.
2. Select the configured Tencent Cloud Monitor data source that includes SCF monitoring from the `Queries to` data source list.
3. Use the input parameters of the SCF monitoring API for the configuration items here. For more information on the configuration items, please see [here](https://intl.cloud.tencent.com/document/product/248/34638).
    - `Namespace`: select a namespace, for example, `QCE/SCF_V2`.
    - `Region`: select a region. The region list will be automatically obtained according to the `Namespace` option.
    - `MetricName`: select a metric name. The metric list will be automatically obtained according to the `Namespace` and `Region` options.
    - `Period`: select a statistical period. The period list will be automatically obtained according to the `MetricName` option.
    - `Instance`: select an instance, which corresponds to the `Instances.N` field of the input parameter. The instance list will be automatically obtained.
      - To adapt to the habits of different users, the instance list is displayed as different fields, which is `As FunctionId` by default, meaning that the instance list is displayed as **function IDs**. You can also select `As FunctionName` (as function names).
      - For more information on how to get the instance list, please see [here](https://intl.cloud.tencent.com/document/api/583/18582). You can toggle `Show Details` to `true` to display the instance request parameters, which are `Offset = 0` and `Limit = 20` by default. If you need to change the instance query criteria, you can configure corresponding parameters as instructed in the API documentation.
      - **Note:** In this application, a single query to get the monitoring data is an atomic operation, i.e., querying the monitoring data of a certain metric of a certain instance. Therefore, you can select only one instance at a time. If you need to query the monitoring data of multiple instances, you can click `Add Query` in the upper-right corner to add new queries.  
      - The `Show Details` button is displayed only when a non-template variable is selected.

![](https://main.qcloudimg.com/raw/1c5ce839f001757f149635d798f4f6b4.png)

## Direct Connect - Dedicated Tunnel (DCX)

1. Click **Add Query** in **New Panel** to go to the panel configuration page. On the `Query` tab on the left, configure the options to get the monitoring data of DCX.
2. Select the configured Tencent Cloud Monitor data source that includes DCX monitoring from the `Queries to` data source list.
3. Use the input parameters of the DCX monitoring API for the configuration items here. For more information on the configuration items, please see [here](https://intl.cloud.tencent.com/document/product/248/10995).
 - `Namespace`: select a namespace, for example, `QCE/DCX`.
 - `Region`: select a region. The region list will be automatically obtained according to the `Namespace` option.
 - `MetricName`: select a metric name. The metric list will be automatically obtained according to the `Namespace` and `Region` options.
 - `Period`: select a statistical period. The period list will be automatically obtained according to the `MetricName` option.
 - `Instance`: select an instance, which corresponds to the `Instances.N` field of the input parameter. The instance list will be automatically obtained.
   - To adapt to the habits of different users, the instance list is displayed as different fields, which is `As DirectConnectTunnelId` by default, meaning that the instance list is displayed as **tunnel IDs**. You can also select `As DirectConnectTunnelName` (as tunnel names).
   - For more information on how to get the instance list, please see [here](https://intl.cloud.tencent.com/document/api/216/19819). You can toggle `Show Details` to `true` to display the instance request parameters, which are `Offset = 0` and `Limit = 20` by default. If you need to change the instance query criteria, you can configure corresponding parameters as instructed in the API documentation.
   - **Note:** In this application, a single query to get the monitoring data is an atomic operation, i.e., querying the monitoring data of a certain metric of a certain instance. Therefore, you can select only one instance at a time. If you need to query the monitoring data of multiple instances, you can click `Add Query` in the upper-right corner to add new queries.  
   - The `Show Details` button is displayed only when a non-template variable is selected.

![](https://main.qcloudimg.com/raw/7bfa939046d03bddcab30c44b3e14490.png)
    

## Direct Connect - Connection (DC)

1. Click **Add Query** in **New Panel** to go to the panel configuration page. On the `Query` tab on the left, configure the options to get the monitoring data of DC.
2. Select the configured Tencent Cloud Monitor data source that includes DC monitoring from the `Queries to` data source list.
3. Use the input parameters of the DC monitoring API for the configuration items here. For more information on the configuration items, please see [here](https://intl.cloud.tencent.com/document/product/248/10994).
  - `Namespace`: select a namespace, for example, `QCE/DC`.
  - `Region`: select a region. The region list will be automatically obtained according to the `Namespace` option.
  - `MetricName`: select a metric name. The metric list will be automatically obtained according to the `Namespace` and `Region` options.
  - `Period`: select a statistical period. The period list will be automatically obtained according to the `MetricName` option.
  - `Instance`: select an instance, which corresponds to the `Instances.N` field of the input parameter. The instance list will be automatically obtained.
    - To adapt to the habits of different users, the instance list is displayed as different fields, which is `As DirectConnectId` by default, meaning that the instance list is displayed as **connection IDs**. You can also select `As DirectConnectName` (as connection names).
    - For more information on how to get the instance list, please see [here](https://intl.cloud.tencent.com/document/product/216/35330). You can toggle `Show Details` to `true` to display the instance request parameters, which are `Offset = 0` and `Limit = 20` by default. If you need to change the instance query criteria, you can configure corresponding parameters as instructed in the API documentation.
    - **Note:** In this application, a single query to get the monitoring data is an atomic operation, i.e., querying the monitoring data of a certain metric of a certain instance. Therefore, you can select only one instance at a time. If you need to query the monitoring data of multiple instances, you can click `Add Query` in the upper-right corner to add new queries.  
    - The `Show Details` button is displayed only when a non-template variable is selected.

![](https://main.qcloudimg.com/raw/7c509f6453fa4f07c05ca9a52e98e71d.png)

## VPC - VPN Gateway

1. Click **Add Query** in **New Panel** to go to the panel configuration page. On the `Query` tab on the left, configure the options to get the monitoring data of the VPN gateway.
2. Select the configured Tencent Cloud Monitor data source that includes VPN gateway monitoring from the `Queries to` data source list.
3. Use the input parameters of the VPN gateway monitoring API for the configuration items here. For more information on the configuration items, please see [here](https://intl.cloud.tencent.com/document/product/248/10988).
  - `Namespace`: select a namespace, for example, `QCE/VPNGW`.
  - `Region`: select a region. The region list will be automatically obtained according to the `Namespace` option.
  - `MetricName`: select a metric name. The metric list will be automatically obtained according to the `Namespace` and `Region` options.
  - `Period`: select a statistical period. The period list will be automatically obtained according to the `MetricName` option.
  - `Instance`: select an instance, which corresponds to the `Instances.N` field of the input parameter. The instance list will be automatically obtained.
    - To adapt to the habits of different users, the instance list is displayed as different fields, which is `As VpnGatewayId` by default, meaning that the instance list is displayed as **VPN gateway IDs**. You can also select `As VpnGatewayName` (as VPN gateway names).
    - For more information on how to get the instance list, please see [here](https://intl.cloud.tencent.com/document/api/215/17514). You can toggle `Show Details` to `true` to display the instance request parameters, which are `Offset = 0` and `Limit = 20` by default. If you need to change the instance query criteria, you can configure corresponding parameters as instructed in the API documentation.
    - **Note:** In this application, a single query to get the monitoring data is an atomic operation, i.e., querying the monitoring data of a certain metric of a certain instance. Therefore, you can select only one instance at a time. If you need to query the monitoring data of multiple instances, you can click `Add Query` in the upper-right corner to add new queries.  
    - The `Show Details` button is displayed only when a non-template variable is selected.

![](https://main.qcloudimg.com/raw/81b7d5b2b74fd9b3890ac3b47727e4ef.png)
    

## VPC -Direct Connect Gateway (DCG)

1. Click **Add Query** in **New Panel** to go to the panel configuration page. On the `Query` tab on the left, configure the options to get the monitoring data of DCG.
2. Select the configured Tencent Cloud Monitor data source that includes DCG monitoring from the `Queries to` data source list.
3. Use the input parameters of the DCG monitoring API for the configuration items here. For more information on the configuration items, please see [here](https://intl.cloud.tencent.com/document/product/248/10990).
  - `Namespace`: select a namespace, for example, `QCE/DCG`.
  - `Region`: select a region. The region list will be automatically obtained according to the `Namespace` option.
  - `MetricName`: select a metric name. The metric list will be automatically obtained according to the `Namespace` and `Region` options.
  - `Period`: select a statistical period. The period list will be automatically obtained according to the `MetricName` option.
  - `Instance`: select an instance, which corresponds to the `Instances.N` field of the input parameter. The instance list will be automatically obtained.
    - To adapt to the habits of different users, the instance list is displayed as different fields, which is `As DirectConnectGatewayId` by default, meaning that the instance list is displayed as **direct connect gateway IDs**. You can also select `As DirectConnectGatewayName` (as direct connect gateway names).
    - For more information on how to get the instance list, please see [here](https://intl.cloud.tencent.com/document/product/215/36913). You can toggle `Show Details` to `true` to display the instance request parameters, which are `Offset = 0` and `Limit = 20` by default. If you need to change the instance query criteria, you can configure corresponding parameters as instructed in the API documentation.
    - **Note:** In this application, a single query to get the monitoring data is an atomic operation, i.e., querying the monitoring data of a certain metric of a certain instance. Therefore, you can select only one instance at a time. If you need to query the monitoring data of multiple instances, you can click `Add Query` in the upper-right corner to add new queries.  
    - The `Show Details` button is displayed only when a non-template variable is selected.

![](https://main.qcloudimg.com/raw/e7a2af8cf618ccc6e84709c0db295273.png)
    

## CDN - Province Domain

1. Click **Add Query** in **New Panel** to go to the panel configuration page. On the `Query` tab on the left, configure the options to get the monitoring data of CDN Province Domain (CDN_LOG_DATA).
2. Select the configured Tencent Cloud Monitor data source that includes CDN Province Domain monitoring from the `Queries to` data source list.
3. Use the input parameters of the CDN Province Domain monitoring API for the configuration items here. For more information on the configuration items, please see [here](https://intl.cloud.tencent.com/document/product/248/39556).
    - `Namespace`, select a namespace, for example, `QCE/CDN_LOG_DATA`.
    - `Region`: select a region. The region list will be automatically obtained according to the `Namespace` option.
    - `MetricName`: select a metric name. The metric list will be automatically obtained according to the `Namespace` and `Region` options.
    - `Period`: select a statistical period. The period list will be automatically obtained according to the `MetricName` option.
    - `Instance`: select an instance, which corresponds to the `Instances.N` field of the input parameter. The instance list will be automatically obtained.
      - To adapt to the habits of different users, the instance list is displayed as different fields, which is `As Domain` by default, meaning that the instance list is displayed as **domain names**. You can also select `As ProjectId` (as project IDs).
      - For more information on how to get the domain name list, please see [here](https://intl.cloud.tencent.com/document/product/228/34020). You can toggle `Show Details` to `true` to display the instance request parameters, which are `Offset = 0` and `Limit = 20` by default. If you need to change the instance query criteria, you can configure corresponding parameters as instructed in the API documentation.
      - **Note:** In this application, a single query to get the monitoring data is an atomic operation, i.e., querying the monitoring data of a certain metric of a certain instance. Therefore, you can select only one instance at a time. If you need to query the monitoring data of multiple instances, you can click `Add Query` in the upper-right corner to add new queries.  
      - The `Show Details` button is displayed only when a non-template variable is selected.
    - `Isp`: ISP list.
    - `Province`: province list.


![](https://main.qcloudimg.com/raw/9b09df7de6b157974d0bfcbbb38cd776.png)
    

## API Gateway

1. Click **Add Query** in **New Panel** to go to the panel configuration page. On the `Query` tab on the left, configure the options to get the monitoring data of the API gateway.
2. Select the configured Tencent Cloud Monitor data source that includes API gateway monitoring from the `Queries to` data source list.
3. Use the input parameters of the API gateway monitoring API for the configuration items here. For more information on the configuration items, please see [here](https://intl.cloud.tencent.com/document/product/248/19130).
    - `Namespace`: select a namespace, for example, `QCE/APIGATEWAY`.
    - `Region`: select a region. The region list will be automatically obtained according to the `Namespace` option.
    - `MetricName`: select a metric name. The metric list will be automatically obtained according to the `Namespace` and `Region` options.
    - `Period`: select a statistical period. The period list will be automatically obtained according to the `MetricName` option.
    - `Instance`: select an instance, which corresponds to the `Instances.N` field of the input parameter. The instance list will be automatically obtained.
      - To adapt to the habits of different users, the instance list is displayed as different fields, which is `As ServiceId` by default, meaning that the instance list is displayed as **protocol port IDs**. You can also select `As ServiceName` (as protocol port names).
      - For more information on how to get the instance list, please see [here](https://intl.cloud.tencent.com/document/product/628/36627). You can toggle `Show Details` to `true` to display the instance request parameters, which are `Offset = 0` and `Limit = 20` by default. If you need to change the instance query criteria, you can configure corresponding parameters as instructed in the API documentation.
      - **Note:** In this application, a single query to get the monitoring data is an atomic operation, i.e., querying the monitoring data of a certain metric of a certain instance. Therefore, you can select only one instance at a time. If you need to query the monitoring data of multiple instances, you can click `Add Query` in the upper-right corner to add new queries.  
      - The `Show Details` button is displayed only when a non-template variable is selected.
    - `EnvironmentName`: environment name, which is automatically obtained based on the instance content.


![](https://main.qcloudimg.com/raw/a9ceee232b0d7e07c835e933a32c21e7.png)
    

## Cloud Block Storage (CBS)

1. Click **Add Query** in **New Panel** to go to the panel configuration page. On the `Query` tab on the left, configure the options to get the monitoring data of CBS.
2. Select the configured Tencent Cloud Monitor data source that includes CBS monitoring from the `Queries to` data source list.
3. Use the input parameters of the CBS monitoring API for the configuration items here. For more information on the configuration items, please see [here](https://intl.cloud.tencent.com/document/product/248/37085).
  - `Namespace`: select a namespace, for example, `QCE/BLOCK_STORAGE`.
  - `Region`: select a region. The region list will be automatically obtained according to the `Namespace` option.
  - `MetricName`: select a metric name. The metric list will be automatically obtained according to the `Namespace` and `Region` options.
  - `Period`: select a statistical period. The period list will be automatically obtained according to the `MetricName` option.
  - `Instance`: select an instance, which corresponds to the `Instances.N` field of the input parameter. The instance list will be automatically obtained.
    - To adapt to the habits of different users, the instance list is displayed as different fields, which is `As DiskId` by default, meaning that the instance list is displayed as **cloud disk IDs**. You can also select `As DiskName` (as cloud disk names).
    - For more information on how to get the instance list, please see [here](https://intl.cloud.tencent.com/document/api/362/16315). You can toggle `Show Details` to `true` to display the instance request parameters, which are `Offset = 0` and `Limit = 20` by default. If you need to change the instance query criteria, you can configure corresponding parameters as instructed in the API documentation.
    - **Note:** In this application, a single query to get the monitoring data is an atomic operation, i.e., querying the monitoring data of a certain metric of a certain instance. Therefore, you can select only one instance at a time. If you need to query the monitoring data of multiple instances, you can click `Add Query` in the upper-right corner to add new queries.  
    - The `Show Details` button is displayed only when a non-template variable is selected.

![](https://main.qcloudimg.com/raw/e022476856e5d42e2681d4dc608fba26.png)
    

## Elasticsearch Service (ES)

1. Click **Add Query** in **New Panel** to go to the panel configuration page. On the `Query` tab on the left, configure the options to get the monitoring data of ES.
2. Select the configured Tencent Cloud Monitor data source that includes ES monitoring from the `Queries to` data source list.
3. Use the input parameters of the ES monitoring API for the configuration items here. For more information on the configuration items, please see [here](https://intl.cloud.tencent.com/document/product/248/34642).
  - `Namespace`: select a namespace, for example, `QCE/CES`.
  - `Region`: select a region. The region list will be automatically obtained according to the `Namespace` option.
  - `MetricName`: select a metric name. The metric list will be automatically obtained according to the `Namespace` and `Region` options.
  - `Period`: select a statistical period. The period list will be automatically obtained according to the `MetricName` option.
  - `Instance`: select an instance, which corresponds to the `Instances.N` field of the input parameter. The instance list will be automatically obtained.
    - To adapt to the habits of different users, the instance list is displayed as different fields, which is `As InstanceId` by default, meaning that the instance list is displayed as **instance IDs**. You can also select `As InstanceName` (as instance names).
    - For more information on how to get the instance list, please see [here](https://intl.cloud.tencent.com/document/product/845/32214). You can toggle `Show Details` to `true` to display the instance request parameters, which are `Offset = 0` and `Limit = 20` by default. If you need to change the instance query criteria, you can configure corresponding parameters as instructed in the API documentation.
    - **Note:** In this application, a single query to get the monitoring data is an atomic operation, i.e., querying the monitoring data of a certain metric of a certain instance. Therefore, you can select only one instance at a time. If you need to query the monitoring data of multiple instances, you can click `Add Query` in the upper-right corner to add new queries.  
    - The `Show Details` button is displayed only when a non-template variable is selected.

![](https://main.qcloudimg.com/raw/62f83d047bd95887f5be0a315d022cbd.png)
    

## CMQ Queue Model

1. Click **Add Query** in **New Panel** to go to the panel configuration page. On the `Query` tab on the left, configure the options to get the monitoring data of the CMQ queue model.
2. Select the configured Tencent Cloud Monitor data source that includes CMQ queue model monitoring from the `Queries to` data source list.
3. Use the input parameters of the CMQ queue model monitoring API for the configuration items here. For more information on the configuration items, please see [here](https://intl.cloud.tencent.com/document/product/248/34643).
  - `Namespace`: select a namespace, for example, `QCE/CMQ`.
  - `Region`: select a region. The region list will be automatically obtained according to the `Namespace` option.
  - `MetricName`: select a metric name. The metric list will be automatically obtained according to the `Namespace` and `Region` options.
  - `Period`: select a statistical period. The period list will be automatically obtained according to the `MetricName` option.
  - `Instance`: select an instance, which corresponds to the `Instances.N` field of the input parameter. The instance list will be automatically obtained.
    - To adapt to the habits of different users, the instance list is displayed as different fields, which is `As QueueName` by default, meaning that the instance list is displayed as **queue names**. You can also select `As QueueId` (as queue IDs).
    - For more information on how to get the instance list, please see [here](https://intl.cloud.tencent.com/document/product/406/35944). You can toggle `Show Details` to `true` to display the instance request parameters, which are `Offset = 0` and `Limit = 20` by default. If you need to change the instance query criteria, you can configure corresponding parameters as instructed in the API documentation.
    - **Note:** In this application, a single query to get the monitoring data is an atomic operation, i.e., querying the monitoring data of a certain metric of a certain instance. Therefore, you can select only one instance at a time. If you need to query the monitoring data of multiple instances, you can click `Add Query` in the upper-right corner to add new queries.  
    - The `Show Details` button is displayed only when a non-template variable is selected.

![](https://main.qcloudimg.com/raw/192fa4e13dd2a8374520373402c70dff.png)
    

## CMQ Topic Model

1. Click **Add Query** in **New Panel** to go to the panel configuration page. On the `Query` tab on the left, configure the options to get the monitoring data of the CMQ topic model.
2. Select the configured Tencent Cloud Monitor data source that includes CMQ topic model monitoring from the `Queries to` data source list.
3. Use the input parameters of the CMQ topic model monitoring API for the configuration items here. For more information on the configuration items, please see [here](https://intl.cloud.tencent.com/document/product/248/11013).
  - `Namespace`: select a namespace, for example, `QCE/CMQTOPIC`.
  - `Region`: select a region. The region list will be automatically obtained according to the `Namespace` option.
  - `MetricName`: select a metric name. The metric list will be automatically obtained according to the `Namespace` and `Region` options.
  - `Period`: select a statistical period. The period list will be automatically obtained according to the `MetricName` option.
  - `Instance`: select an instance, which corresponds to the `Instances.N` field of the input parameter. The instance list will be automatically obtained.
    - To adapt to the habits of different users, the instance list is displayed as different fields, which is `As TopicName` by default, meaning that the instance list is displayed as **topic names**. You can also select `As TopicId` (as topic IDs).
    - For more information on how to get the instance list, please see [here](https://intl.cloud.tencent.com/document/product/406/35931). You can toggle `Show Details` to `true` to display the instance request parameters, which are `Offset = 0` and `Limit = 20` by default. If you need to change the instance query criteria, you can configure corresponding parameters as instructed in the API documentation.
    - **Note:** In this application, a single query to get the monitoring data is an atomic operation, i.e., querying the monitoring data of a certain metric of a certain instance. Therefore, you can select only one instance at a time. If you need to query the monitoring data of multiple instances, you can click `Add Query` in the upper-right corner to add new queries.  
    - The `Show Details` button is displayed only when a non-template variable is selected.

![](https://main.qcloudimg.com/raw/17ea626b3c07132396ff5aa6bb78312d.png)
