## RESTful API  
Elasticsearch provides RESTful APIs that have comprehensive and powerful features to interact with clusters. These APIs can be used to:  
- View the health status and statistics of clusters, nodes, and indices.
- Manage clusters, nodes, indexed data, and metadata and adjust cluster configuration.
- Perform (Create, Read, Update, and Delete) CRUD operations and various types of queries on indexed data, such as full-text search, filtering, aggregation, and sorting.

For more information, see Elasticsearch's official [API documentation](https://www.elastic.co/guide/en/elasticsearch/reference/5.6/index.html).

## Client
- You can call a REST API to access a cluster using any client that allows you to send HTTP/REST calls, such as curl and Kibana Dev Tool.  
- Elasticsearch provides clients in a variety of programming languages, such as Java and Python, to meet the needs of different developers. For more information, see [Elasticsearch Clients](https://www.elastic.co/guide/en/elasticsearch/client/index.html). 
- Starting from Elasticsearch 5.6.0, a new official Java client has been released: the Java High Level REST Client. This client can be used to perform search, index, delete, update, and bulk operations using the same core Java classes as the Transport Client does. It is actually designed to replace the Transport Client. For more information, see [Java High Level REST Client](https://www.elastic.co/guide/en/elasticsearch/client/index.html).

> In terms of version compatibility, you are recommended to choose the client version that is compatible with the server version. For more information, see [Compatibility](https://www.elastic.co/guide/en/elasticsearch/client/java-rest/6.0/java-rest-high-compatibility.html). Currently, ES is available in multiple Elasticsearch versions, so be sure to select a compatible client version. 

## Access authentication
If you select the Platinum Edition that comes with Elastic Stack (formerly X-Pack), user authentication will be enabled for Elasticsearch clusters, and you need to enter your username and password when accessing a cluster through various clients or APIs. However, you don't need to do so if you select the Open Source Edition or Basic Edition.

When accessing a cluster, pay attention to the Elastic Stack edition selected. For more information, see [Accessing a Cluster from a Client](https://intl.cloud.tencent.com/document/product/845/19538),  and [Accessing a Cluster from Kibana](https://intl.cloud.tencent.com/document/product/845/19541). 

**Special note on network selection:**
- For security reasons, an ES cluster is built in a VPC, and access to cluster data is limited to the same VPC.  
- When you purchase a cluster, a [VPC](https://intl.cloud.tencent.com/document/product/215) and subnet must have been configured in the region and availability zone selected.  
- Generally, a [CVM instance](https://intl.cloud.tencent.com/document/product/213) in the same VPC needs to be used as a client to access the ES cluster and initiate data storage and query requests.  
- If you are an existing user of Tencent Cloud and want to build an ES cluster based on existing data and services, you need to select the same VPC as that of your existing services when doing so.
