### MongoDB and DynamoDB
MongoDB is a high-performance, non-relational, schema-free, document-oriented database that supports dynamic queries and full indexing. Performance excellence and the ease of use make MongoDB the most widely used NoSQL database for data management.

**Core advantages of MongoDB:** 
1. Document Oriented Storage. Suitable for storing and managing collections of documents, where one collection can hold the unlimited size of documents. 
2. Schema-free. Data is stored in the form of JSON style documents, which can have varying sets of fields, with different types for each field.
3. Index on any of attributes, including the internal objects. Geospatial-based indexes are also supported.
4. Rich queries. MongoDB supports a rich query language.
5. Aggregation capabilities, such as count and group.
6. Replication and data recovery. MongoDB's master-slave replication system provides a variety of features such as data backup, disaster recovery and read extension.

AWS DynamoDB is a fully managed proprietary NoSQL service that supports document and key-value data structures and provides fast, predictable performance at any scale.

**Core advantages of DynamoDB:**
1. Scalability. DynamoDB is built on a fully distributed and non-shared architecture that can scale the table assets to a large number of servers.
2. Predictable performance. The average latency of AWS DynamoDB server can be as low as a few milliseconds.
3. Easy to manage. As a fully managed service, AWS DynamoDB saves your time and money from the complexities of setting up and running a  distributed database cluster with high reliability
4. Built-in fault tolerance. AWS DynamoDB’s built-in fault tolerance supports automatic and synchronous replication of your data to multiple availability zones in a Region.
5. Flexibility. AWS DynamoDB does not have a fixed schema.
6. Strong consistency and atomic counter. AWS DynamoDB offers consistent read operations to ensure your data up-to-date. The atomic counter is supported.

Based on the existing NoSQL module framework, Tencent Cloud adds protocol-compatibility to AWS DynamoDB database service. Now DynamoDB is compatible with most basic protocols to meet database access requirements. Also, it supports instance-level backup and rollback, and automatic disaster recovery mechanism to ensure high reliability and availability of the service.
1. If you are a DynamoDB development enthusiast, Tencent Cloud database service is good for addressing your needs as a developer.
2. If you are from outside of China and need to deploy DynamoDB services in China for your projects that have been developed using the DynamoDB protocol, you can access Tencent Cloud Database via the DynamoDB protocol with minimum modification needed.
