## Problem description

The **CPU monitoring** metrics stay high on the **System Monitoring** tab on the **Instance Details** page of an instance in the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
![](https://staticintl.cloudcachetci.com/yehe/backend-news/p6hj771_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_16753229907497.png)

## Troubleshooting

1. Check whether the database operations are too frequent.
Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb) and click the ID of the target instance to enter the **Instance Details** page. Then, select the **System Monitoring** tab and view the **Total Requests** (QPS) metric of the instance, which indicates the total number of requests to the instance per second.
If the business QPS is obviously high, determine whether you need to upgrade the instance configuration. For detailed directions, see <a href="https://intl.cloud.tencent.com/document/product/240/31192">Adjusting Instance Specification</a>.
2. Check whether there are slow logs on mongod.
Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb) and view the slow logs of the instance by using **Query statistics**.
![img](https://staticintl.cloudcachetci.com/yehe/backend-news/ctrU959_2-en.png)
Pay attention to keywords such as **command**, **COLLSCAN**, **IXSCAN**, **keysExamined**, and **docsExamined**.
  - **command** indicates an operation request recorded in a slow log.
  - **COLLSCAN** indicates that a full-collection scan is performed for the query.
  - **IXSCAN** indicates that an index scan is performed. For descriptions of other fields, see [Explain Results](https://docs.mongodb.com/manual/reference/explain-results/index.html).
  - **keysExamined** indicates the number of index entries scanned.
  - **docsExamined** indicates the number of documents scanned. Larger **keysExamined** and **docsExamined** values indicate that no index is created or the created index is less distinctive.
For more information on slow logs, see [Log Messages](https://docs.mongodb.com/manual/reference/log-messages/index.html). Analyze the specific cause and solve the problem based on the log message.

## References

For more troubleshooting methods, see [Fixing High CPU Utilization in MongoDB Instance Based on DBbrain](https://www.tencentcloud.com/document/product/240/52499).

