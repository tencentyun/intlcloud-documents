Flink excels at processing unbounded and bounded data sets. Precise control of time and state enables Flink's runtime to run any kind of application on unbounded streams. Bounded streams are internally processed by algorithms and data structures that are specifically designed for fixed sized data sets, yielding excellent performance.
The following are the directions for bounded or unbounded data sets in COS. Here, the YARN Session Mode is used for job submission to better observe job running. Flink on YARN supports the Session Mode and Application Mode. For more information, see the [community documentation](https://nightlies.apache.org/flink/flink-docs-release-1.16/docs/deployment/resource-providers/yarn/).
The job submitted in this tutorial is a wordcount job, i.e., counting the number of words. You need to upload the file for counting to the cluster in advance.
## Development Preparations
1. [Create a bucket](https://intl.cloud.tencent.com/document/product/436/13309) in COS for this job.
2. Create an EMR cluster. When creating the EMR cluster, you need to select the Flink component on the software configuration page and enable access to COS on the basic configuration page.
3. After purchasing the cluster, access COS with HDFS to ensure that its basic features are available. The specific commands are as follows:
```
[hadoop@10 ~]$ hdfs dfs -ls cosn://$BUCKET_NAME/path
Found 1 items
-rw-rw-rw-   1 hadoop hadoop      27040 2022-10-28 15:08 cosn://$BUCKET_NAME/path/LICENSE
```

## Example
```
# `-n` indicates the number of containers applied for, i.e., the number of TaskManagers.
# `-tm` indicates the memory size per TaskManager.
# `-s` indicates the number of slots per TaskManager.
# `-d` indicates to run as a backend application, which is followed by the session name.
[hadoop@10 ~]$ yarn-session.sh -jm 1024 -tm 1024 -n 1 -s 1 -nm wordcount-example -d
```
```
/usr/local/service/flink/bin/flink run -m yarn-cluster /usr/local/service/flink/examples/batch/WordCount.jar --input cosn://$BUCKET_NAME/path/LICENSE -output cosn://$BUCKET_NAME/path/wdp_test
[hadoop@10 ~]$ hdfs dfs -ls cosn://$BUCKET_NAME/path/wdp_test
-rw-rw-rw-   1 hadoop hadoop       7484 2022-11-04 00:47 cosn://$BUCKET_NAME/path/wdp_test
```

## Maven Demo
Here, the demo that comes with the system is not used; instead, you need to create a project and compile, compress, and upload it to the EMR cluster on your own for execution. Maven is recommended for project management, as it can help you manage project dependencies with ease. Specifically, it can get .jar packages through the configuration of the `pom.xml` file, eliminating the need to add them manually.
1. Download and install Maven first and then configure its environment variables. If you are using the IDE, set the Maven configuration items in the IDE.
2. In the local shell environment, enter the directory where you want to create the Maven project, such as `D://mavenWorkplace`, and enter the following command to create it:

```
mvn archetype:generate -DgroupId=$yourgroupID -DartifactId=$yourartifactID -DarchetypeArtifactId=maven-archetype-quickstart
```
Here, `yourgroupID` is your package name, `yourartifactID` is your project name, and `maven-archetype-quickstart` indicates to create a Maven Java project. Some files need to be downloaded during the project creation, so you should keep the network connected.
After successfully creating the project, you will see a folder named `$yourartifactID` in the `D://mavenWorkplace` directory. The files in the folder have the following structure:
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
Among the files above, pay extra attention to the `pom.xml` file and the Java folder under the main directory. The `pom.xml` file is primarily used to create dependencies and package configurations; the Java folder is used to store your source code.
First, add the Maven dependencies to pom.xml:
```
<properties>
    <scala.version>2.12</scala.version>
    <flink.version>1.14.3</scala.version>
</properties>

<dependencies>
    <dependency>
        <groupId>org.apache.flink</groupId>
        <artifactId>flink-java</artifactId>
        <version>1.14.3</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>org.apache.flink</groupId>
        <artifactId>flink-streaming-scala_${scala.version}</artifactId>
        <version>${flink.version}</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>org.apache.flink</groupId>
        <artifactId>flink-clients_${scala.version}</artifactId>
        <version>${flink.version}</version>
        <scope>provided</scope>
    </dependency>
</dependencies>
```
>? Use your actual `scala.version` and `flink.version` values.

Then, add the packaging and compiling plugins to `pom.xml`:
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
If your Maven is configured correctly and its dependencies are successfully imported, the project will be compiled directly. Enter the project directory in the local shell, and run the following command to package the entire project:
```
mvn package
```
Some files may need to be downloaded during the running process. "Build success" indicates that a package is successfully created. You can see the generated .jar package in the target folder under the project directory.

### Data preparations
First, you need to upload the compressed .jar package to the EMR cluster using the scp or sftp tool by running the following command in local command line mode:
```
scp $localfile root@public IP address:$remotefolder
```
Here, `$localfile` is the path plus name of your local file; `root` is the CVM instance username. You can look up the public IP address in the node information in the EMR console or the CVM console. `remotefolder` is the path where you want to store the file in the CVM instance. After the upload is completed, you can check whether the file is in the corresponding folder on the EMR command line.
The file to be processed needs to be uploaded to COS in advance. If the file is in your local file system, you can upload it directly through the [COS console](https://intl.cloud.tencent.com/document/product/436/13321); if it is in the EMR cluster, you can upload it by running the following Hadoop command:
```
[hadoop@10 hadoop]$ hadoop fs -put $testfile cosn://BUCKET_NAME/
```

### Running the demo
First, log in to any node (preferably a master one) in the EMR cluster. For more information on how to log in to EMR, see [Logging In To Linux Instance (Web Shell)](https://intl.cloud.tencent.com/document/product/213/5436). Here, you can use WebShell to log in. Click **Login** on the right of the desired CVM instance to enter the login page. The default username is `root`, and the password is the one you set when creating the EMR cluster. Once your credentials are validated, you can enter the command line interface.
Run the following command in EMR command-line interface to switch to the Hadoop user:
```
[root@172 ~]# su hadoop
[hadoop@172 ~]$ flink  run  -m yarn-cluster -c com.tencent.flink.CosWordcount ./flink-example-1.0-SNAPSHOT.jar cosn://$BUCKET_NAME/test/data.txt cosn://$BUCKET_NAME/test/result
[hadoop@172 ~]$ hdfs dfs -cat cosn://becklong-cos/test/result
(Flink,8)
(Hadoop,3)
(Spark,7)
(Hbase,3)
```