Apache Superset is a web-based data browsing and visualization application.

Superset features:
- It supports almost all popular databases such as MySQL, PostgresSQL, Oracle, SQL Server, SQLite, and SparkSQL as well as [Druid](http://druid.io/).
- It provides a wide variety of visualizations and allows creating custom dashboards.
- It makes data display completely controllable and enables customization of displayed fields, aggregated data, and data sources.

Superset on EMR supports MySQL, Hive, Presto, Impala, Kylin, Druid, and ClickHouse.

## Preparations
1. Confirm that you have activated Tencent Cloud and created an EMR cluster.
2. Select Superset as an optional component when creating the cluster.
3. By default, Superset is installed on the master node of your cluster.
4. Enable the security group policy for the master node and make sure that your network can access port 18088 of the master node.

## Login

Enter `http://${master_ip}:18088` in your browser (or go to **[EMR Console](https://console.cloud.tencent.com/emr)** > **Component Management**) to open the login page of Supserset. The default username is `admin`, and the password is the one you set when creating the cluster.
![](https://main.qcloudimg.com/raw/d250be3123fb3e7da47d69b73ef6343a.png)

## Adding Database

Enter the **Sources** > **Database** page and click **Filter List**.
![](https://main.qcloudimg.com/raw/c98760953f38fc23d27abcbf5208bd83.png)
Enter the following page and add the URI of the component to be added in SQLAlchemy URI.
![](https://main.qcloudimg.com/raw/57b69ecbd6f5c2ac0ca4adde380325ae.png)
 

The SQLAlchemy URI for each database is as follows:

| **Name** | **SQLAlchemy URI**                                         | **Remarks**                                                     |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| MySQL    | `mysql+pymysql://<mysqlname>:<password>@<mysql_ip>:<mysql_port>/<your_database>` | <li>mysqlname: username used to connect to MySQL<li>password: MySQL password<li>your_database: MySQL database to be connected to |
		| Hive     | `hive://hadoop@<master_ip>:7001/default?auth=NONE`             | Master_ip: `master_ip` of EMR cluster |
| Presto   | `presto://hive@<master_ip>:9000/hive/<hive_db_name>`           | <li>Master_ip: `master_ip` of EMR cluster<li>hive_db_name: name of database in Hive. If this parameter is left empty, it will be `default` by default |
| Impala   | `impala://<core_ip>:27000`                                     | core_ip: core IP of EMR cluster |
| Kylin    | `kylin://<kylin_user>:<password>@<master_ip>:16500/<kylin_project>` | <li>kylin_user: Kylin username<li>password: Kylin password<li>master_ip: `master_ip` of EMR cluster<li>kylin_project: Kylin project |
|ClickHouse  |`clickhouse://<user_name>:<password>@<clickhouse-server-endpoint>:8123/<database_name>`| `clickhouse://default:password@localhost:8123/default`<li>user_name: username<li>password: password<li>clickhouse-server-endpoint: ClickHouse service endpoint<li>database_name: name of the database to be accessed


## Adding New Database on Your Own
Superset supports those databases. To install another database, follow the steps below:
1. Log in to the server where the master node of EMR resides.
2. Run the `source /usr/local/service/superset/bin/activate` command.
3. Install the corresponding Python library with pip3.
4. Restart Superset.

