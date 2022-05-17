Apache Zeppelin is a web-based notebook that enables interactive data analysis. It allows you to create interactive collaborative documents with various prebuilt language backends (or interpreters), such as Scala (Apache Spark), Python (Apache Spark), Spark SQL, Hive, and Shell.

## Prerequisites
- You have created a cluster and selected the Zeppelin service. For more information, see [Creating EMR Cluster](https://intl.cloud.tencent.com/document/product/1026/31099).
- In the cluster's EMR security group, open ports 22 and 30001 (which are opened by default for new clusters) and the necessary IP ranges for communication over the private network. The new security group is named in the format of `emr-xxxxxxxx_yyyyMMdd`, which shouldn't be modified manually.
- Add services as needed, such as Spark, Flink, HBase, and Kylin.

## Logging in to Zeppelin
1. Create a cluster and select the Zeppelin service. For more information, see [Creating EMR Cluster](https://intl.cloud.tencent.com/document/product/1026/31099).
2. On the left sidebar in the [EMR console](https://console.cloud.tencent.com/emr), select **Cluster Service**.
3. Click the Zeppelin block and click **Web UI Address** to access the web UI.
4. For EMR versions later than 3.1.0, the default login permission is set, and both the username and password are `admin`. To change the password, modify the `users` and `roles` options in the `/usr/local/service/zeppelin-0.8.2/conf/shiro.ini` configuration file. For more configuration instructions, see [Apache Shiro Configuration](https://shiro.apache.org/configuration.html#Configuration-INISections).
5. In EMR 2.6.0 and 3.3.0, Zeppelin login is integrated into the OpenLDAP account, so you can log in only with an OpenLDAP account and password. After a cluster is created, the default OpenLDAP accounts are `root` and `hadoop`, and the default password is the cluster password. Only the `root` account has the Zeppelin admin permissions and has access to the interpreter configuration page.

## Performing `wordcount` with Spark
1. Click **Create new note** on the left of the page to create a notebook in the pop-up window.
 ![](https://main.qcloudimg.com/raw/c31d7b714f22b1170d9c6799572227a3.png)
2. Configure Spark for integration with an EMR cluster (Spark on YARN). Modify and save the configuration.
![](https://main.qcloudimg.com/raw/3794475f902450a00a86e2bb00dd3c42.png)
3. Go to your own notebook.
 ![](https://main.qcloudimg.com/raw/d56fe984a78c0f8f59498d2c24ee5b73.png)
4. Write a wordcount program and run the following commands:
```
val data = sc.textFile("cosn://huanan/zeppelin-spark-randomint-test")
case class WordCount(word: String, count: Integer)
val result = data.flatMap(x => x.split(" ")).map(x => (x, 1)).reduceByKey(_ + _).map(x => WordCount(x._1, x._2))
result.toDF().registerTempTable("result")
%sql select * from result
```
![](https://main.qcloudimg.com/raw/8d70fcea7197c81e2d0235cab6d77843.png)
