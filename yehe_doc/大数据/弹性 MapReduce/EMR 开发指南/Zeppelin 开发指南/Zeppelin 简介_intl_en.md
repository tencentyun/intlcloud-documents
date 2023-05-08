Apache Zeppelin is a web-based notebook that enables interactive data analysis. It allows you to create interactive collaborative documents with various prebuilt language backends (or interpreters), such as Scala (Apache Spark), Python (Apache Spark), Spark SQL, Hive, and Shell.
>? The Flink, HBase, Kylin, Livy, and Spark interpreters are configured for EMR v3.3.0 or later and EMR v2.6.0 or later by default. For configuring interpreters of other components for other versions of EMR, see [Documentation](https://zeppelin.apache.org/) and configure them based on the Zepplin version.


## Prerequisites
- You have created a cluster and selected the Zeppelin service. For more information, see [Creating EMR Cluster](https://intl.cloud.tencent.com/document/product/1026/31099).
- In the EMR security group of the cluster, ports 22, 30001, and 18000 and necessary private network IP ranges are enabled (ports 22 and 30001 enabled for a new cluster by default). A new security group must be named in the format of "emr-xxxxxxxx_yyyyMMdd", and the name cannot be modified manually.
- Services are added as needed, such as Spark, Flink, HBase, and Kylin.

## Logging In to Zeppelin
1. Create a cluster and select the Zeppelin service. For more information, see [Creating EMR Cluster](https://intl.cloud.tencent.com/document/product/1026/31099).
2. On the left sidebar in the [EMR console](https://console.cloud.tencent.com/emr), select **Cluster Services**.
3. Click the Zeppelin block and click **WebUI address** to access the WebUI.
4. For EMR v2.5.0 or earlier and EMR 3.2.1 or earlier, the default login permission is set, and both the username and password are `admin`. To change the password, you can modify the `users` and `roles` options in the configuration file `/usr/local/service/zeppelin-0.8.2/conf/shiro.ini`. For more configuration instructions, see [here](https://shiro.apache.org/configuration.html#Configuration-INISections).
5. In EMR v2.6.0 or later and EMR v3.3.0 or later, Zeppelin login is integrated into the OpenLDAP account, so you can log in only with an OpenLDAP account and password. After a cluster is created, the default OpenLDAP accounts are `root` and `hadoop`, and the default password is the cluster password. Only the `root` account has the Zeppelin admin permissions and thus the access to the interpreter configuration page.

## Performing Wordcount Using Spark
1. Click **Create new note** on the left and create a notebook on the pop-up page.
 ![](https://main.qcloudimg.com/raw/c31d7b714f22b1170d9c6799572227a3.png)
2. For EMR v3.3.0 or later and EMR v2.6.0 or later, clusters connecting Spark to EMR (Spark on YARN) are configured by default.
	- If you are using EMR v3.1.0, EMR v2.5.0, or EMR v2.3.0, see [Documentation](https://zeppelin.apache.org/docs/0.8.2/interpreter/spark.html) to configure the Spark interpreter.
	- If you are using EMR v3.2.1, see [Documentation](https://zeppelin.apache.org/docs/0.9.0/interpreter/spark.html) to configure the Spark interpreter.
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
