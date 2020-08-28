Tencent Cloud Elasticsearch Service (ES) is a highly available and scalable cloud-managed Elasticsearch service built by Tencent Cloud based on the open-source search engine Elasticsearch. It is fully compatible with the ELK architecture and widely used in businesses such as website search and navigation, enterprise-level search, service log exception monitoring, and clickstream analysis in fields like internet, gaming, and internet finance.

ES operations supported by CloudAudit are as shown below:

| Operation Name | Resource Type | Event Name |
|----------|------|----------------------------|
| Creating ES cluster instance | es   | CreateInstance             |
| Terminating ES cluster instance | es   | DeleteInstance             |
| Querying ES cluster log | es   | DescribeInstanceLogs       |
| Querying instance operation log | es   | DescribeInstanceOperations |
| Querying ES cluster instance | es   | DescribeInstances          |
| Restarting ES cluster instance | es   | RestartInstance            |
| Updating ES cluster instance | es   | UpdateInstance             |
| Upgrading ES cluster version | es   | UpgradeInstance            |
| Upgrading ES commercial feature | es   | UpgradeLicense             |
