Apache Spark is an open-source project for fast, general-purpose, large-scale data processing. Its framework is similar to Hadoop's MapReduce but faster and more efficient for batch processing. It utilizes in-memory caching and optimized execution for fast performance, and it supports reading/writing Hadoop data in any format. Now Apache Spark has become a unified big data processing platform with a lightning-fast unified analysis engine for real-time streaming processing, machine learning, and ad hoc queries.

Spark is an in-memory parallel computing framework for big data processing. Its in-memory computing feature improves the real-time performance of data processing in a big data environment, while ensuring high fault tolerance and scalability. Spark can be deployed on a large number of inexpensive hardware devices to create clusters.

- The job submitted in this tutorial is a wordcount job, i.e., counting the number of words. You need to upload the file for counting to the cluster in advance.

## 1. Preparations for Development
- You need to [create a bucket](https://intl.cloud.tencent.com/document/product/436/13309) in COS for this job.
- Confirm that you have activated Tencent Cloud and created an EMR cluster. When creating your EMR cluster, click the Spark component on the software configuration page, click "Enable COS" on the basic configuration page and then enter your SecretId and SecretKey. You can find your SecretId and SecretKey at [API Key Management](https://console.cloud.tencent.com/cam/capi). If you don’t have a SecretKey, click **Create Key** to create one.

## 2. Using Maven to Create a Project
In this tutorial, the demo that comes with the system is not used; instead, you need to create a project and compile, compress, and upload it to the EMR cluster on your own for execution.

Maven is recommended for project management, as it can help you manage project dependencies with ease. Specifically, it can get .jar packages through the configuration of the pom.xml file, eliminating your need to add them manually.

Download and install Maven first and then configure its environment variables. If you are using the IDE, please set the Maven-related configuration items in the IDE.

###	 Creating a Maven project

In the local shell environment, enter the directory where you want to create the Maven project, such as `D://mavenWorkplace`, and enter the following command to create it:
```
mvn archetype:generate -DgroupId=$yourgroupID -DartifactId=$yourartifactID -DarchetypeArtifactId=maven-archetype-quickstart
```
Here, $yourgroupID is your package name, $yourartifactID is your project name, and maven-archetype-quickstart indicates to create a Maven Java project. Some files need to be downloaded during the project creation, so please keep the network connected.

After successfully creating the project, you will see a folder named $yourartifactID in the `D://mavenWorkplace` directory. The files included in the folder have the following structure:
```
simple
	---pom.xml　　　　Core configuration, under the project root directory
	---src
		---main　　　　　　
			---java　　　　  Java source code directory
			---resources　  Java configuration file directory
		---test
			 ---java　　　　  Test source code directory
			 ---resources　  Test configuration directory
```
Among the files above, pay extra attention to the pom.xml file and the Java folder under the main directory. The pom.xml file is primarily used to create dependencies and package configurations; the Java folder is used to store your source code.

First, add the Maven dependencies to pom.xml:
```
<dependencies>
    <dependency>
        <groupId>org.apache.spark</groupId>
        <artifactId>spark-core_2.11</artifactId>
        <version>2.0.2</version>
    </dependency>
</dependencies>
```
Then, add the packaging and compiling plugins to pom.xml:
```
<build>
<plugins>
  <plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <configuration>
      <source>1.8</source>
      <target>1.8</target>
      <encoding>utf-8</encoding>
    </configuration>
  </plugin>
  <plugin>
    <artifactId>maven-assembly-plugin</artifactId>
    <configuration>
      <descriptorRefs>
      <descriptorRef>jar-with-dependencies</descriptorRef>
      </descriptorRefs>
    </configuration>
    <executions>
      <execution>
        <id>make-assembly</id>
        <phase>package</phase>
        <goals>
          <goal>single</goal>
        </goals>
      </execution>
    </executions>
  </plugin>
</plugins>
</build>
```
Right-click in src>main>Java and create a Java Class. Enter the Class name (e.g., WordCountOnCos here) and add the sample code to the Class:
```
import java.util.Arrays;
import org.apache.spark.SparkConf
import org.apache.spark.api.java.JavaRDD;
import org.apache.spark.api.java.JavaSparkContext;
import scala.Tuple2;

/**
 * Created by tencent on 2018/6/28.
 */
public class WordCountOnCos {
    public static void main(String[] args){
        SparkConf sc = new SparkConf().setAppName("spark on cos");
        JavaSparkContext context = new JavaSparkContext(sc);
        JavaRDD<String> lines = context.textFile(args[0]);

        lines.flatMap(x -> Arrays.asList(x.split(" ")).iterator())
                .mapToPair(x -> new Tuple2<String, Integer>(x, 1))
                .reduceByKey((x, y) -> x+y)
                .saveAsTextFile(args[1]);
    }
}
```
If your Maven is configured correctly and its dependencies are successfully imported, the project will be compiled directly. Enter the project directory in the local shell, and run the following command to package the entire project:
```
mvn package
```
Some files may need to be downloaded during the running process. "Build success" indicates that package is successfully created. You can see the generated .jar package in the target folder under the project directory.

### Data preparations
First, you need to upload the compressed .jar package to the EMR cluster with the scp or sftp tool by running the following command in local command line mode:
```
scp $localfile root@public IP address:$remotefolder
```
Here, $localfile is the path and the name of your local file; root is the CVM instance username. You can look up the public IP address in the node information in the EMR or CVM Console. $remotefolder is the path where you want to store the file in the CVM instance. After the upload is completed, you can check whether the file is in the corresponding folder on the EMR command line.

The file to be processed needs to be uploaded to COS in advance. If the file is in your local file system, you can upload it directly through the [COS Console](https://intl.cloud.tencent.com/document/product/436/13321); if it is in the EMR cluster, you can upload it by running the following Hadoop command:
```
[hadoop@10 hadoop]$ hadoop fs -put $testfile cosn://$bucketname/
```
Here, $testfile is the full path plus name of the file for counting, and $bucketname is your bucket name. After the upload is completed, you can check whether the file is present in COS in the COS Console.

### Running the demo
First, you need to log in to any node (preferably a master one) in the EMR cluster. For more information on how to log in to EMR, please see [Logging in to Linux Instances](https://intl.cloud.tencent.com/document/product/213/5436). Here, you can choose to log in with WebShell. Click "Log in" on the right of the desired CVM instance to enter the login page. The default username is `root`, and the password is the one you set when creating the EMR cluster. Once the correct credentials are entered, you can enter the command line interface.

Run the following command in EMR command-line interface to switch to the Hadoop user:
```
[root@172 ~]# su hadoop
```
Then, go to the folder where the .jar package is stored and run the following command:
```
[hadoop@10spark]$ spark-submit    --class    $WordCountOnCOS    --master 
yarn-cluster $packagename.jar cosn:// $bucketname /$testfile cosn:// $bucketname 
/output
```
Here, $WordCountOnCOS is your Java Class name, $packagename is the name of the .jar package generated in the new Maven project you created, $bucketname is your bucket name plus path, and $testfile is the name of the file for counting. The output file is stored in the output folder **which cannot be created beforehand; otherwise, the execution will fail**.

After successful execution, you can see the result of the wordcount job in the specified bucket and folder.
```
[hadoop@172 /]$ hadoop fs -ls cosn:// $bucketname /output
Found 3 items
-rw-rw-rw- 1 hadoop Hadoop  0 2018-06-28 19:20 cosn:// $bucketname /output/_SUCCESS
-rw-rw-rw- 1 hadoop Hadoop 681 2018-06-28 19:20 cosn:// $bucketname /output/part-00000
-rw-rw-rw- 1 hadoop Hadoop 893 2018-06-28 19:20 cosn:// $bucketname /output/part-00001

[hadoop@172 demo]$ hadoop fs -cat cosn://$bucketname/output/part-00000
18/07/05 17:35:01 INFO cosnative.NativeCosFileSystem: Opening 'cosn:// $bucketname/output/part-00000' for reading
(under,1)
(this,3)
(distribution,2)
(Technology,1)
(country,1)
(is,1)
(Jetty,1)
(currently,1)
(permitted.,1)
(Security,1)
(have,1)
(check,1)
```
