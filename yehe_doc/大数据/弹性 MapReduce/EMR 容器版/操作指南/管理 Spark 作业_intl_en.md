## Feature Overview
Container-based EMR clusters allow you to submit Spark jobs and view job information in the console.
>! A job should be submitted as a YAML file of up to 10 MB in size.

## Directions
1. Log in to the [container-based EMR console](https://console.cloud.tencent.com/emr/static/containerdeploy) and click the **ID/Name** of the target cluster in the **Cluster list** to enter the cluster details page.
2. On the cluster details page, click **Job Management** to submit and query jobs.
3. You can submit YAML job files through CRD in the EMR console after compiling the files.
4. Click **Submit Job** above the **Job List** to pop up the **Submit Job** window. Then, select the job file to be submitted and click **Confirm**.
![](https://qcloudimg.tencent-cloud.cn/raw/932f03fc922f980845f65824a29719f2.jpg)
5. Click **Details** in the **Job List** to enter the Spark HistoryServer UI to view the job details.
6. Click **Delete** in the **Job List**. Then, in the **Delete job** pop-up window, confirm the information of the job to be deleted and click **Confirm**.

## Sample Job
The process of submitting a Spark job through CRD is as follows:
1. Write a Spark program.
2. Compile and package the program into a JAR package and put the package in the COS or HDFS file system, or write a Dockerfile to create an image for the package.
3. Write a YAML file and submit it in the console.

The following describes four sample Spark jobs:
### Sample 1. Using a Spark JAR package
Below is a sample YAML job file:
```
apiVersion: "sparkoperator.k8s.io/v1beta2"
kind: SparkApplication
metadata:
  name: test1
spec:
  hadoopConf:
    "fs.cosn.userinfo.secretId":"$SecretId"
    "fs.cosn.userinfo.secretKey":"$SecretKey" 
  type: Scala
  mode: cluster
  mainClass: org.apache.spark.examples.SparkPi
  mainApplicationFile: "local:///opt/spark/examples/jars/spark-examples_2.12-3.2.0.jar"
```
For more information on the parameters used in this sample, visit [GitHub](https://github.com/GoogleCloudPlatform/spark-on-k8s-operator/blob/v1beta2-1.2.0-3.0.0/docs/api-docs.md).
- `apiVersion` and `kind` are the resource version and type in K8s, which cannot be changed here.
- `metadata.name` defines the job name, which is `test1` here and can be customized.
- `spec.hadoopConf` defines the configuration information of Hadoop. Interacting with COS requires configuring the key information, which can be obtained on the [Manage API Key](https://console.cloud.tencent.com/cam/capi) page. The `$SecretId` and `$Secretkey` in the code should be replaced with your actual `SecretId` and `Secretkey`.
- `type` defines the type of the Spark program, which can be Java, Scala, Python, or R. It is Scala here and can be selected as needed.
- `mode` defines the deployment mode of `sparkApplication`, which can be cluster or client. It is cluster here and can be selected as needed.
- `driver` and `executor` define the Spark driver and executor respectively. They are automatically generated on the backend as follows by default: 
```
driver:
  cores: 1
  memory: 512m
executor:
  cores: 1
  instances: 2
  memory: 512m

```
You can customize the `driver` and `executor` parameters and add them to the sample YAML job file 1. Then, the custom parameters will overwrite the default parameters. Below is a sample:
```
driver:
    cores: 1
    coreLimit: "1200m"
    memory: "512m"
  executor:
    cores: 1
    instances: 1
    memory: "512m"
```

### Sample 2. Compiling and packaging a Spark program and putting the JAR package in COS (recommended)
The following sample shows the complete process of compiling a Spark program, packaging it into a JAR package, and writing and submitting a YAML job file.
1. Prepare for development.
You need to have a COS bucket for this job, which can be the bucket you selected when creating the cluster or a new bucket created in the same region as the previously selected bucket.
2. Create a project with Maven.
You need to create a project and then compile, package, and upload it. Maven is recommended because it can help you manage project dependency more easily.
3. Write a WordCount program and add the following sample code:
```
import java.util.Arrays;
import java.util.regex.Pattern;

import org.apache.spark.SparkConf;
import org.apache.spark.api.java.JavaPairRDD;
import org.apache.spark.api.java.JavaRDD;
import org.apache.spark.api.java.JavaSparkContext;
import org.apache.spark.sql.SparkSession;
import scala.Tuple2;

public class WordCountOnCos {
    private static final Pattern SPACE = Pattern.compile(" ");
    public static void main(String[] args){
        if (args.length < 1) {
            System.err.println("Usage: JavaWordCount <file>");
            System.exit(1);
        }
        SparkSession spark = SparkSession.builder().appName("wordCountOnCos").getOrCreate();
        JavaRDD<String> lines = spark.read().textFile(args[0]).javaRDD();
        JavaRDD<String> words = lines.flatMap(s -> Arrays.<String>asList(SPACE.split(s)).iterator());
        JavaPairRDD<String, Integer> ones = words.mapToPair(s -> new Tuple2(s, Integer.valueOf(1)));
        JavaPairRDD<String, Integer> counts = ones.reduceByKey((i1, i2) -> Integer.valueOf(i1.intValue() + i2.intValue()));
        counts.saveAsTextFile(args[1]);
        spark.stop();
    }
}
```
4. Run the `mvn package` command to package the entire project.
5. Upload the JAR package to the COS bucket and write a YAML file as follows:
```
apiVersion: "sparkoperator.k8s.io/v1beta2"
kind: SparkApplication
metadata:
  name: test2
spec:
  hadoopConf:
    "fs.cosn.userinfo.secretId":"$SecretId"
    "fs.cosn.userinfo.secretKey":"$SecretKey" 
  type: Java
  mode: cluster
  mainClass: com.tencent.WordCountOnCos
  mainApplicationFile: "cosn://kt-test-251007880/sparkapp/jar/wordcount.jar"
  arguments:
    - "cosn://kt-test-251007880/sparkapp/input/input"
    - "cosn://kt-test-251007880/sparkapp/output"

```
Here, `arguments` is the parameters passed to the main class and indicates the input and output directories of the WordCount program. The `mainApplicationFile` and the input and output directories of the WordCount program here are examples and can be customized.

### Sample 3. Compiling and packaging a Spark program into a JAR package and putting it in HDFS 
Write a Spark program and package it into a JAR package as shown in sample 2. Then, upload the package to HDFS and write a YAML file as follows:
```
apiVersion: "sparkoperator.k8s.io/v1beta2"
kind: SparkApplication
metadata:
  name: test3
spec:
  hadoopConf:
    "fs.cosn.userinfo.secretId":"$SecretId"
    "fs.cosn.userinfo.secretKey":"$SecretKey" 
  type: Java
  mode: cluster
  mainClass: com.tencent.WordCountOnCos
  mainApplicationFile: "hdfs://$ip:$port/sparkapp/jar/wordcount.jar"
  arguments:
    - "cosn://kt-test-251007880/sparkapp/input/input"
    - "hdfs://$ip:$port/sparkapp/output"

```
>! If you store the JAR package in HFDS, HDFS should be in the same VPC as the container-based cluster.

### Sample 4. Compiling and packaging a Spark program into a JAR package and creating an image for it
Write a Spark program and package it into a JAR package as shown in sample 2. Then, create a Dockerfile as follows:
```
FROM ccr.ccs.tencentyun.com/emr-image/spark:BaseImage
USER root
RUN mkdir -p /sparkapp
COPY jars/wordcount.jar /sparkapp
ENTRYPOINT [ "/opt/entrypoint.sh" ]
```
You need to inherit the base image `ccr.ccs.tencentyun.com/emr-image/spark:BaseImage`, which contains the JAR package required to interact with COS.
```
docker build -t ccr.ccs.tencentyun.com/emr-image/spark:wc -f ./bin/Dockerfile .
```
Write a YAML job file as follows:
```
apiVersion: "sparkoperator.k8s.io/v1beta2"
kind: SparkApplication
metadata:
  name: test4
spec:
  hadoopConf:
    "fs.cosn.userinfo.secretId":"$SecretId"
    "fs.cosn.userinfo.secretKey":"$SecretKey" 
  type: Java
  mode: cluster
  mainClass: com.tencent.WordCountOnCos
  image: ccr.ccs.tencentyun.com/emr-image/spark:wc
  mainApplicationFile: "local:///sparkapp/wordcount.jar"
  arguments:
    - "cosn://kt-test-251007880/sparkapp/input/input"
    - "cosn://kt-test-251007880/sparkapp/output"
```
Here, `image` is the image you created through packaging, and `mainApplicationFile` is the path of the JAR package in the image.




