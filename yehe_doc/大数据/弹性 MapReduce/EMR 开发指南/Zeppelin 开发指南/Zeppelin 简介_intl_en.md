Apache Zeppelin is an interactive development system that enables big data visualization and analytics. It can undertake tasks such as data ingestion, discovery, analytics, visualization, and collaboration. It provides a rich set of visual graph libraries such as SparkSQL on the frontend and supports big data systems like HBase and Flink in the form of plugin extension on the backend. In addition, it allows you to perform data preprocessing, algorithm development and debugging, and algorithm job scheduling for machine learning.

For EMR versions later than 3.1.0, the default login permission is set, and both the username and password are admin. To change the password, you can modify the `users` and `roles` options in the configuration file `/usr/local/service/zeppelin-0.8.2/conf/shiro.ini`. For more configuration instructions, see [here](http://shiro.apache.org/configuration.html#Configuration-INISections).


### Performing wordcount using Spark
1. Click **Create new note** on the left and create a notebook on the pop-up page.
 ![](https://main.qcloudimg.com/raw/c31d7b714f22b1170d9c6799572227a3.png)
2. Configure Spark for integration with an EMR cluster (Spark on YARN). Modify and save configuration.
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
