Spark SQL is Apache Spark's module for structured data processing. It provides a DataFrame abstraction in a variety of languages to simplify working with structured datasets and lets you query the data with distributed SQL.
## 1. Preparations for Development
Confirm that you have activated Tencent Cloud and created an EMR cluster. When creating the EMR cluster, select the Spark component on the software configuration page.
 
## 2. Using the Interactive SparkSQL Console
First, log in to a master node of the EMR cluster before using SparkSQL. For more information on how to log in to EMR, please see [Logging in to a Linux Instance](https://intl.cloud.tencent.com/document/product/213/5436). Here, you can use WebShell to log in. Click *Login* button on the right of the desired CVM instance and then enter the login page. The default username is root, and the password is the one you set when creating the EMR cluster. Once your credentials have been validated, you can access to the EMR command-line interface.

Run the following command in EMR command-line interface to switch to the Hadoop user and go to the directory `/usr/local/service/spark`:
```
[root@172 ~]# su hadoop
[hadoop@172 root]$ cd /usr/local/service/spark
```
You can access the interactive SparkSQL Console by running the following command:
```
[hadoop@10spark]$ bin/spark-sql --master yarn --num-executors 64 --executor-memory 2g
```
Here, --master indicates your master URL, --num-executors the number of executors, and --executor-memory the storage capacity of the executors. You can modify these parameters based on your actual conditions and start/stop a SparkSQLthriftserver through `sbin/start-thriftserver.sh`/`sbin/stop-thriftserver.sh`.

Below are some basic operations in SparkSQL.


Create and view a database:
```
spark-sql> create database sparksql;
Time taken: 0.907 seconds

spark-sql> show databases;
default
sparksql
test
Time taken: 0.131 seconds, Fetched 5 row(s)
```
Create a new table in the database you just created and view the table:
```
spark-sql> use sparksql;
Time taken: 0.076 seconds

spark-sql> create table sparksql_test(a int,b string);
Time taken: 0.374 seconds

spark-sql> show tables;
sparksql_test	false
Time taken: 0.12 seconds, Fetched 1 row(s)
```
Insert two rows of data into the table and view them:
```
spark-sql> insert into sparksql_test values (42,'hello'),(48,'world');
Time taken: 2.641 seconds

spark-sql> select * from sparksql_test;
42	hello
48	world
Time taken: 0.503 seconds, Fetched 2 row(s)
```
For more information on Spark command line parameters, please see the [community documentation](http://spark.apache.org/docs/latest/sql-programming-guide.html).

## 3. Creating a Project with Maven
Download and install Maven first and then configure its environment variables. If you are using the IDE, please set the Maven-related configuration items in the IDE.


### Creating a Maven project
Enter the directory of the Maven project, such as `D://mavenWorkplace`, and create the project by running the following commands:
```
mvn    archetype:generate    -DgroupId=$yourgroupID    -DartifactId=$yourartifactID
-DarchetypeArtifactId=maven-archetype-quickstart
```
Here, $yourgroupID is your package name; $yourartifactID is your project name; maven-archetype-quickstart indicates to create a Maven Java project. Some files need to be downloaded during the project is being created, so please stay connected to the Internet.
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

### Adding Hadoop dependencies and sample code
First, add the Maven dependencies to the pom.xml file:
```
<dependencies>
　　　    <dependency>
　　　        <groupId>org.apache.spark</groupId>
　　　        <artifactId>spark-core_2.11</artifactId>
　　　        <version>2.0.2</version>
　　　    </dependency>
　　　    <!--spark sql-->
　　　    <dependency>
　　　        <groupId>org.apache.spark</groupId>
　　　        <artifactId>spark-sql_2.11</artifactId>
　　　        <version>2.0.2</version>
　　　    </dependency>
</dependencies>
```
Then, add the packaging and compiling plugins to the pom.xml file:
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
Below is an example of a complete pom.xml file:
```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>$yourgroupID </groupId>
    <artifactId>$yourartifactID </artifactId>
    <version>1.0-SNAPSHOT</version>

    <dependencies>
        <dependency>
            <groupId>org.apache.spark</groupId>
            <artifactId>spark-core_2.11</artifactId>
            <version>2.0.2</version>
        </dependency>
        <!--spark sql-->
        <dependency>
            <groupId>org.apache.spark</groupId>
            <artifactId>spark-sql_2.11</artifactId>
            <version>2.0.2</version>
        </dependency>
    </dependencies>

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
</project>
```
>Replace $yourgroupID and $yourartifactID with your real information.

Then, create a Java Class named Demo.java in the main>Java folder and add the following code to it:
```
import org.apache.spark.rdd.RDD;
import org.apache.spark.sql.Dataset;
import org.apache.spark.sql.Row;
import org.apache.spark.sql.SparkSession;

/**
 * Created by tencent on 2018/6/28.
 */
public class Demo {
    public static void main(String[] args){
        SparkSession spark = SparkSession
                .builder()
                .appName("Java Spark Hive Example")
                .enableHiveSupport()
                .getOrCreate();

        Dataset<Row> df = spark.read().json(args[0]);

        RDD<Row> test = df.rdd();
        
        test.saveAsTextFile(args[1]);
    }
}
```

### Compiling code and packaging it for upload
Use the local command prompt to enter the project directory and run the following command to compile and package the project:
```
mvn package
```
"Build success" indicates that package is successfully created. You can see the generated .jar package in the target folder under the project directory.
Use the scp or sftp tool to upload the compressed .jar package to the EMR cluster. Run the following command in your local shell:
```
scp $localfile root@public IP address:$remotefolder
```
Here, $localfile is the path and the name of your local file; root is the CVM instance username. You can look up the public IP address in the node information in the EMR or CVM Console. $remotefolder is the path where you want to store the file in the CVM instance. After the upload is completed, you can check whether the file is in the corresponding folder on the EMR command line.

## 4. Preparing the Data and Running the Demo
You can use SparkSQL to process data stored in HDFS. First, upload the data to HDFS. The built-in file people.json stored in `/usr/local/service/spark/exa-mples/src/main/resources/` is used as an example here. Run the following command to upload it to HDFS:
```
[hadoop@10 hadoop]$ hadoop fs -put /usr/local/service/spark/examples/src/ma-in/resources/ 
/user/hadoop
```
You can choose a different test file. Here, `/user/hadoop/` is a folder under HDFS, which you can create if it does not exist.

Run the demo. First, log in to a master node of the EMR cluster and switch to the Hadoop user, as shown in the interactive SparkSQL Console. Run the following command:
```
[hadoop@10spark]$ bin/spark-submit --class Demo --master yarn-client $yourjarpackage /  
/user/hadoop/people.json  /user/hadoop/$output
```
Here, --class is the executed entry class. In this example, Demo is the class, which is also the name of the Java Class you created when adding Hadoop dependencies and sample code. --master is the master URL of the cluster, $yourjarpackage is the package name, and $output is the output folder (**if the $output folder already exists before the command is executed, the program will fail**).

After the program is successfully executed, you can see the result in `/user/hadoop/$output`:
```
[hadoop@172 spark]$ hadoop fs -cat /user/hadoop/$output/part-00000
[null,Michael]
[30,Andy]
[19,Justin]
```
For more spark-submit parameters, run the following commands, or see the [official documentation](https://spark.apache.org/docs/latest/submitting-applications.html).
```
[hadoop@10spark]$ spark-submit -h
```
