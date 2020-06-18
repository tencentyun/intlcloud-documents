Apache Zeppelin is an interactive development system that enables big data visualization and analytics. Specifically, it can undertake various tasks such as data ingestion, discovery, analytics, visualization, and collaboration. It provides a rich set of graph visualization libraries such as SparkSQL on the frontend and supports big data systems like HBase and Flink in the form of plugin extension on the backend. In addition, it allows you to perform data preprocessing, algorithm development and debugging, and algorithm job scheduling for machine learning.

### Performing `wordcount` with Spark
1. Click **Create new note** on the left and create a notebook on the pop-up page.
 ![](https://main.qcloudimg.com/raw/c31d7b714f22b1170d9c6799572227a3.png)
2. Configure Spark for integration with an EMR cluster (Spark on YARN), modify parameters as needed, and save the configuration.
 ![](https://main.qcloudimg.com/raw/f4702cf3dea049e4bff2685aed9800f3.png)
3. Enter your own notebook.
 ![](https://main.qcloudimg.com/raw/9920f5e879b66075f95311aa691db952.png)
4. Write a `wordcount` program and run the following command:
```
val data = sc.textFile("cosn://huanan/zeppelin-spark-randomint-test")
case class WordCount(word: String, count: Integer)
val result = data.flatMap(x => x.split(" ")).map(x => (x, 1)).reduceByKey(_ + _).map(x => WordCount(x._1, x._2))
result.toDF().registerTempTable("result")
%sql select * from result
```
![](https://main.qcloudimg.com/raw/8d70fcea7197c81e2d0235cab6d77843.png)
