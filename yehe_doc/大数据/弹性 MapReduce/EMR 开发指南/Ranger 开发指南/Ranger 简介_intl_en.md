## Ranger Overview
Ranger is a framework for centralized security management of Hadoop components in the field of big data. Users can use Ranger to securely access data in a cluster. It is mainly designed to monitor Hadoop components, and control service launch and resource access. The major goals of Ranger include:
- Centralized security management of big data components in the web UI or using RESTful APIs provided by Ranger.
- Authorization to perform specific operations with big data components based on roles and attributes.
- Centralized auditing of user access and administrative operations (security-related) with big data components.

## Ranger Architecture
Ranger is mainly composed of Ranger Admin, Ranger UserSync, and Ranger Plugin. Both Ranger Admin and Ranger UserSync are a separate JVM process, while Ranger Plugin needs to be installed on different nodes depending on different components.

![](https://main.qcloudimg.com/raw/0da76efca9b7bbf806f287116112193a.png)
- Ranger Admin is used to manage configured policies, created services, and audit logs and reports. It also persistently saves the policies and services to the database for regular queries from Ranger Plugin.
- Ranger UserSync is used to synchronize information from LDAP, File, and Unix to Ranger Admin, for example, user and group information from users' Unix or LDAP directory access systems. To synchronize user and group information from Unix, you need to enable the `unixAuthenticationService` process and persistently store the synchronized information.
- Ranger Plugin will be deployed on service nodes as needed and periodically synchronize policy information from Ranger Admin.

The following table lists the components that can be integrated with Ranger.

| **Service** | **Installation Nodes** | **EMR Versions** |
| ----------- | -------------------- | ----------------- |
| HDFS | NameNode | EMR v2.0.1 and above |
| HBase | Master, RegionServer | EMR v2.0.1 and above |
| Hive | HiveServer2 | EMR v2.0.1 and above |
| YARN | ResourceManager | EMR v2.0.1 and above |
| Presto | All coordinators | EMR v2.0.1 and above |
| Impala | All daemons | EMR v2.2.0 and above |
| Kudu | All masters | EMR v3.2.0 |

