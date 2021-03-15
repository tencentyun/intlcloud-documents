Apache Superset is a web-based application for data exploration and visualization.

Superset features:
- Supports almost all major databases such as MySQL, PostgresSQL, Oracle, SQL Server, SQLite, and Spark SQL as well as [Druid](http://druid.io/).
- Provides a wide variety of visual displays and allows you to create custom dashboards.
- Makes data display controllable and enables customization of displayed fields, aggregated data, and data sources.

By default, Superset on EMR supports MySQL, Hive, Presto, Impala, Kylin, Druid, and ClickHouse.

## Preparations
1. Confirm that you have activated the Tencent Cloud service and created an EMR cluster.
2. Select Superset as an optional component when creating the cluster.
3. Superset is installed on the master node of your cluster by default.
4. Enable the security group policy for the master node and make sure that your network can access port 18088 of the master node.
5. Add initialization actions.
```
export PYTHONPATH=/usr/local/service/superset/conf
/usr/local/service/superset/bin/superset db upgrade
/usr/local/service/superset/bin/superset fab create-admin   Set the username (default value: `admin`) and password.
/usr/local/service/superset/bin/superset init
```

## Login

Enter `http://${master_ip}:18088` in your browser (or go to **[EMR console]((https://console.cloud.tencent.com/emr)** > **Component Management**) to open the login page of Superset. The default username is `admin`, and the password is the one you set when creating the cluster.
![](https://main.qcloudimg.com/raw/d250be3123fb3e7da47d69b73ef6343a.png)

## Adding Databases

Enter the **Sources** > **Databases** page and click **Filter List**.
![](https://main.qcloudimg.com/raw/c98760953f38fc23d27abcbf5208bd83.png)
On the following page, add the URI of the component to be added in **SQLAlchemy URI**.
![](https://main.qcloudimg.com/raw/57b69ecbd6f5c2ac0ca4adde380325ae.png)
 

The SQLAlchemy URI for each database is as follows:

| **Name** | **SQLAlchemy URI** | **Remarks** |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| MySQL | `mysql+pymysql://<mysqlname>:<password>@<mysql_ip>:<mysql_port>/<your_database>` | <li>`mysqlname`: username used to connect to MySQL.<li>`password`: MySQL password.<li>`your_database`: MySQL database to be connected to. |
		| Hive | `hive://hadoop@<master_ip>:7001/default?auth=NONE` | `master_ip`: master IP of EMR cluster. |
| Presto | `presto://hive@<master_ip>:9000/hive/<hive_db_name>` | <li>`master_ip`: master IP of EMR cluster.<li>`hive_db_name`: name of database in Hive. If this parameter is left empty, it will be `default` by default. |
| Impala | `impala://<core_ip>:27000` | `core_ip`: core IP of EMR cluster. |
| Kylin | `kylin://<kylin_user>:<password>@<master_ip>:16500/<kylin_project>` | <li>`kylin_user`: Kylin username.<li>`password`: Kylin password.<li>`master_ip`: master IP of EMR cluster.<li>`kylin_project`: Kylin project. |
| ClickHouse | `clickhouse://<user_name>:<password>@<clickhouse-server-endpoint>:8123/<database_name>` | `clickhouse://default:password@localhost:8123/default`<li>`user_name`: username.<li>`password`: password.<li>`clickhouse-server-endpoint`: ClickHouse service endpoint.<li>`database_name`: name of the database to be accessed.


## Adding New Databases on Your Own
Superset supports databases. To install another database, follow the steps below:
1. Log in to the server where the master node of EMR cluster resides.
2. Run the `source /usr/local/service/superset/bin/activate` command.
3. Install the corresponding Python library with pip3.
4. Restart Superset.

