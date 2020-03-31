### What is TencentDB for MariaDB?
TencentDB for MariaDB is a highly secure enterprise-level cloud database dedicated to the online transaction processing (OLTP) scenario. It has been used in Tencent's billing business for more than a decade. It is [compatible with MySQL syntax](https://intl.cloud.tencent.com/document/product/237/6988?from_cn_redirect=1) and has various advanced features such as thread pool, audit, and remote disaster recovery while delivering easy scalability, simplicity, and high cost performance of TencentDB.

### What are the typical use cases of TencentDB for MariaDB?
- Scenario 1: cloud-based data disaster recovery (remote disaster recovery)
- Scenario 2: business system cloudification
- Scenario 3: hybrid cloud
- Scenario 4: read/write separation
- Scenario 5: development testing
For more information on each use case, please see [Use Cases](https://intl.cloud.tencent.com/document/product/237/1056).

### What are the strengths of TencentDB for MariaDB?
- Strong data consistency
2. Higher security
3. More powerful features
4. Higher availability
5. Higher performance
6. Compatibility with MySQL
7. Cost effectiveness and ease of use
For more information on each strength, please see [Strengths](https://intl.cloud.tencent.com/document/product/237/6864).

### What is the distributed architecture of TencentDB for MariaDB?
For more information on the distributed architecture, please see [TDSQL](https://intl.cloud.tencent.com/document/product/1042).

### What are the standards and certifications of TencentDB for MariaDB?
TencentDB for MariaDB has earned many Chinese and international certifications on behalf of TencentDB, including but not limited to:
- Software Copyright
- ISO22301 Certification
- ISO27001 Certification
- ISO20000 Certification
- ISO9001 Certification
- Trusted Cloud Service Certification
- Cybersecurity Classified Protection Certification
- STAR Certification

Some features of TencentDB for MariaDB are designed based on the following standards:
- GBT 20273-2006 Information Security Technology - Security Techniques Requirement for Database Management System
- JRT 0072-2012 Testing and Evaluation Guide for Classified Protection of Information System of Financial Industry

### Why does an error occur when I specify some storage engines for a TencentDB for MariaDB instance?
Consistency requirements are first matched when TencentDB for MariaDB initializes parameters, but some storage engines may cause data inconsistency; therefore, an error may occur in some storage engines when you create a table. You can use the `SHOW ENGINES` command to view the storage engines supported by the current database. For more information on storage engines, please see [Storage Engines](https://intl.cloud.tencent.com/document/product/237/5276).

### Why does a newly purchased TencentDB for MariaDB instance with 2 GB memory only have about 1 GB cache capacity after initialization?
Please see "Parameter Settings" of the corresponding instance in the TencentDB for MariaDB Console. 1 GB out of the 2 GB memory will be assigned to the threads executed by SQL, such as temporary table variables in the figure below.
![](https://main.qcloudimg.com/raw/03a6cdb679e9400f3e64c9572435573b.png)

### Why does the `max_tmp_size` parameter have a size of at most 60 MB in a TencentDB for MariaDB instance with 6 GB memory?
The default value of this parameter in TencentDB for MariaDB system is 64 MB. You are not recommended to set it to a greater value.
If you need to set a specific value for this parameter, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.

### Why does the CPU utilization reach 50% when there is no operation on the TencentDB for MariaDB instance?
Due to the TencentDB architecture design, binlogs and slow logs are analyzed and uploaded once every five minutes; therefore, there will be one minute with high CPU utilization every five minutes.
The monitoring page in the console displays the maximum value in five minutes, so the utilization seems high; however, the actual utilization is lower than the displayed value.

### Why does the CPU utilization exceed 100% in a TencentDB for MariaDB instance?
By default, TencentDB for MariaDB adopts the policy of overuse of idle resources that allows your business to preempt some idle CPU resources. Therefore, when the number of CPU cores of your instance exceeds the default value assigned, the CPU utilization may appear to exceed 100% in the monitoring view, which is actually normal.
However, if your CPU utilization always exceeds 60%, you are recommended to upgrade the database as soon as possible.

### I have purchased 16 GB of memory. The monitoring page of the TencentDB for MariaDB instance shows that the memory has been almost used up, but why is my business not affected?
The memory allocation mechanism of the database makes the most of idle memory to improve the cache hit rate rather than reading data from the disk. Therefore, it is normal that your memory is used up. Generally, you only need to pay attention to whether your business is affected.

### Why is only one IP address displayed for the TencentDB for MariaDB Standard Edition (one master and one slave)?
The slave server does not provide an IP address. You can purchase read-only instances if needed.

### Why doesn't the available disk capacity increase after I delete content from tables in a TencentDB for MariaDB instance?
Data deletion does not release available physical capacity (similar to other databases). You can use Percona Toolkit to perform the `alter table xxxx engine=innodb` operation on the desired table.

### The download link for a TencentDB for MariaDB instance is valid for only 15 minutes. What can I do if there is a high volume of data that cannot be fully downloaded within 15 minutes?
To ensure security of the download link, the URL is valid for only 15 minutes; however, if the download has already started, the connection will remain valid throughout the download (a copied URL will be invalid).

### Why does the available cache capacity keep decreasing even to 0 or –1?
The actual captured capacity is the available capacity for Innodb_buffer. As the database generally uses the LRU scheduling scheme, this value tends to be 0 in normal cases, and you do not need to worry about it. Please first check whether the cache hit rate is too low, e.g., lower than 90%. 
When a large transaction is processed, this value may be negative, which means that the database memory usage exceeds the assigned value. This is because some idle memory resources are overused in the physical space to ensure proper operation of your business. Therefore, overuse does exist.

### Can I change the previously configured character set and the number of bytes during initialization of a TencentDB for MariaDB instance?
To change the character set, you can modify `character_set_server` in parameter settings or specify the character set when creating a table; to modify the `innodb_page_size` parameter, you need to submit a ticket (for reinstalling the instance).

### What will happen if the number of connections to a TencentDB for MariaDB instance is too large? Or how do I avoid the problem where new business requests cannot properly connect to the database?
The maximum number of connections is 4,096 for a running TDSQL client. After the threshold is reached, new connections will be denied. In this case, please view the following monitoring metrics: number of active connections and connection utilization. You can analyze this problem based on the following situations:
- If the client is a short connection application, please check whether there are unclosed connections (in this case, the number of active connections usually increases linearly to 4,096). If metrics such as number of query requests increase drastically at the same time, please check whether there is a sudden increase in the number of requests.
- If the client is a persistent connection application, please check the number of connections in all connection pools to the TDSQL instance. If the connection utilization in monitoring metrics is low, the number of connections to a connection pool is too large.

### How can I verify that read/write separation has been performed on the slave in a TencentDB for MariaDB instance?
You can check the number of queries in the slave (SELECT) through the corresponding monitoring metric in the console. If read/write separation is enabled, this value will be greater than 0.

### What are the differences between the aggregated, master node, and slave node data in monitoring metrics of a TencentDB for MariaDB instance? Why are some monitoring values obviously different?
The aggregated data is the aggregation of all monitoring data of the entire instance and may be the sum of values of all master nodes or master and slave nodes.
Master and slave node data is data of a single node; therefore, the values are certainly different.


