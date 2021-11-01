Before learning how to access an ES cluster, you need to understand user authentication in ES clusters first.

## ES Cluster User Authentication

This feature is used to improve the data access security of ES clusters (for more information, please see [Protect your data in the Elastic Stack](https://www.elastic.co/what-is/elastic-stack-security)). You must pass the authentication based on username and password before you can access an ES cluster through Kibana, clients, or APIs. For more information, please see [Accessing Cluster from API](https://intl.cloud.tencent.com/document/product/845/19540), [Accessing Cluster from Client](https://intl.cloud.tencent.com/document/product/845/19538), and [Accessing Cluster from Kibana](https://intl.cloud.tencent.com/document/product/845/19541).

>?You are required to set the username and password when creating an ES cluster.
> - For clusters with this feature not enabled, the username and password will be used only for Kibana login.
> - For clusters with this feature enabled, the username and password can be used for authentication for ES cluster login in any method.

## Elasticsearch Editions Supporting ES Cluster User Authentication

Not all Elasticsearch editions support this feature. The support conditions of all editions are as follows:
- Open Source Edition: it does not support this feature.
- Basic Edition: only v6.8 or above allows you to enable or disable this feature, **while legacy versions do not support this feature**.
- Platinum Edition: this feature is enabled by default and cannot be disabled.

## Notes on Enabling ES Cluster User Authentication

If you did not enable user authentication for an ES cluster previously and now want to enable it by upgrading the cluster or toggling the configuration switch, you need to complete the following steps first:
- Modify your business code in advance, so that the username and password can be passed in when relevant APIs are called to normally access the cluster after this feature is enabled.
- According to Elasticsearch's official design requirements, you need to fully restart the cluster after enabling this feature. During the restart, the cluster will be unavailable; therefore, please do so at an appropriate time.

## Enabling/Disabling ES Cluster User Authentication on Basic Edition v6.8 or Above

- When creating a cluster, you can choose whether to enable or disable ES cluster user authentication.
- After a cluster is created, if you need to change the feature status, you can enter the cluster details page for configuration.
![](https://qcloudimg.tencent-cloud.cn/raw/26015c19840211ff58852c202fe85725.png)

