HBase is an open-source, high-reliability, high-performance, column-oriented, scalable distributed storage system developed based on Google BigTable. It uses Hadoop file system (HDFS) as the file storage system, Hadoop MapReduce for processing massive amounts of data in HBase, and ZooKeeper for collaboration.

HBase consists of ZooKeeper, HMaster, and HRegionServer.
ZooKeeper prevents single points of failure on Hmaster, and its master election mechanism guarantees that there is always a master node available in the cluster.

HMaster manages the CRUD operations on the tables and the load balancing of the HRegionServers. In addition, when a HRegionServer exits, it moves the HRegion of that HRegionServer to another.
HRegionServer is the core module in HBase and responsible for reading and writing data from and to HDFS based on user's I/O requests. HRegionServer internally manages a series of HRegion objects, each of which corresponds to a Region and consists of multiple Stores. Each Store corresponds to the storage in the Column Family.

This developer guide describes how to use an EMR cluster for development from a technical perspective.
Due to data security purposes, only VPC access is currently supported for EMR.

## 1. Preparations for Development
- Confirm that you have activated Tencent Cloud and created an EMR cluster. When creating the EMR cluster, select the HBase and ZooKeeper componentS on the software configuration page.

## 2. Using HBase Shell
Log in to a master node of the EMR cluster first before using HBase Shell. For more information on how to log in to EMR, please see [Logging in to a Linux Instance](https://intl.cloud.tencent.com/document/product/213/5436). Here, you can use WebShell to log it. Click Login on the right of the desired CVM instance to enter the login page. The default username is root, and the password is the one you set when creating the EMR cluster. Once your credentials have been validated, you can access to the command-line interface of EMR.

Run the following command on the EMR command-line interface to switch to the Hadoop user and go to the directory `/usr/local/service/hbase`:
```
[root@172 ~]# su hadoop
[hadoop@10root]$ cd /usr/local/service/hbase
```

You can enter HBase Shell by running the following command:
```
[hadoop@10hbase]$ bin/hbase shell
```

Enter help in HBase Shell to see basic usage information and command examples. Next, create a table by running the following command:
```
hbase(main):001:0> create 'test', 'cf'
```
Once the table is created, you can run the `list` command to see whether it is present correctly.
```
hbase(main):002:0> list 'test'
TABLE                                                                             
test                                                                               
1 row(s) in 0.0030 seconds

=> ["test"]
```

Run the `put` command to add elements to the table you created:
```
hbase(main):003:0> put 'test', 'row1', 'cf:a', 'value1'
0 row(s) in 0.0850 seconds

hbase(main):004:0> put 'test', 'row2', 'cf:b', 'value2'
0 row(s) in 0.0110 seconds

hbase(main):005:0> put 'test', 'row3', 'cf:c', 'value3'
0 row(s) in 0.0100 seconds
```

Three values are added to the created table. The first is "value1" inserted into row "row1" column "cf:a", and so on.
Run the `scan` command to traverse the entire table:
```
hbase(main):006:0> scan 'test'
ROW  COLUMN+CELL                                                                   
row1   column=cf:a, timestamp=1530276759697, value=value1                         
row2   column=cf:b, timestamp=1530276777806, value=value2                         
row3   column=cf:c, timestamp=1530276792839, value=value3                         
3 row(s) in 0.2110 seconds
```

Run the `get` command to get the value of the specified row in the table:
```
hbase(main):007:0> get 'test', 'row1'
COLUMN  CELL                                                                       
 cf:a       timestamp=1530276759697, value=value                                   
1 row(s) in 0.0790 seconds
```

Run the `drop` command to delete a table, which should be disabled first before deletion by running the `disable` command:
```
hbase(main):010:0> disable 'test'
hbase(main):011:0> drop 'test'
```
Finally, run the `quit` command to close HBase Shell.

For more HBase Shell commands, please see the [official documentation](http://hbase.apache.org/book.html).

## 3. Using HBase with APIs
[Download and install Maven](http://maven.apache.org/download.cgi) first and then configure its environment variables. If you are using IDE, please configure Maven-related items in your IDE.

### Creating a Maven project

Enter the directory of the Maven project, such as `D://mavenWorkplace`, and create the project by running the following commands:
```
mvn      archetype:generate      -DgroupId=$yourgroupID       -DartifactId=$yourartifactID 
-DarchetypeArtifactId=maven-archetype-quickstart
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

### Adding Hadoop dependencies and sample code
First, add the Maven dependencies to the pom.xml file:
```
<dependencies>
　　　    <dependency>
　　　            <groupId>org.apache.hbase</groupId>
　　　            <artifactId>hbase-client</artifactId>
　　　            <version>1.2.4</version>
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
Before adding the sample code, you need to get the ZooKeeper address of the HBase cluster. Log in to any master or core node in EMR, go to the `/usr/local/service/hbase/conf` directory, and view the hbase.zookeeper.quorum configuration in the base-site.xml file for ZooKeeper's IP address $quorum and the hbase.zookeeper.property.clientPort configuration for the port number $clientPort.

Then, add the sample code by creating a Java Class named PutExample.java in the main>java folder and adding the following code to it:
```
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.hbase.*;
import org.apache.hadoop.hbase.client.*;
import org.apache.hadoop.hbase.util.Bytes;
import org.apache.hadoop.hbase.io.compress.Compression.Algorithm;

import java.io.IOException;

/**
 * Created by tencent on 2018/6/30.
 */
public class PutExample {
    public static void main(String[] args) throws IOException {
        Configuration conf = HBaseConfiguration.create();
        conf.set("hbase.zookeeper.quorum","$quorum");
        conf.set("hbase.zookeeper.property.clientPort","$clientPort");

        Connection connection = ConnectionFactory.createConnection(conf);
        Admin admin = connection.getAdmin();

        HTableDescriptor table = new HTableDescriptor(TableName.valueOf("test1"));
        table.addFamily(new HColumnDescriptor("cf").setCompressionType(Algorithm.NONE));

        System.out.print("Creating table. ");
        if (admin.tableExists(table.getTableName())) {
            admin.disableTable(table.getTableName());
            admin.deleteTable(table.getTableName());
        }
        admin.createTable(table);

        Table table1 = connection.getTable(TableName.valueOf("test1"));
        Put put1 = new Put(Bytes.toBytes("row1"));
        put1.addColumn(Bytes.toBytes("cf"), Bytes.toBytes("a"),
                Bytes.toBytes("value1"));
        table1.put(put1);
        Put put2 = new Put(Bytes.toBytes("row2"));
        put2.addColumn(Bytes.toBytes("cf"), Bytes.toBytes("b"),
                Bytes.toBytes("value2"));
        table1.put(put2);
        Put put3 = new Put(Bytes.toBytes("row3"));
        put3.addColumn(Bytes.toBytes("cf"), Bytes.toBytes("c"),
                Bytes.toBytes("value3"));
        table1.put(put3);

        System.out.println(" Done.");
    }
}
```

### Compiling code and packaging it for upload
Use the local command prompt to enter the project directory and run the following command to compile and package the project:
```
mvn package
```
"Build success" indicates that package is successfully created. You can see the generated .jar package in the target folder under the project directory.
Upload the package file to the EMR cluster with the scp or sftp tool. Be sure to include the dependencies in the .jar package to be uploaded. Run the following command in local command line mode:
```
scp $localfile root@public IP address:$remotefolder
```
Here, $localfile is the path and the name of your local file; root is the CVM instance username. You can look up the public IP address in the node information in the EMR or CVM Console. $remotefolder is the path where you want to store the file in the CVM instance. After the upload is completed, you can check whether the file is in the corresponding folder on the EMR command line.

## 4. Running the Demo
Log in to a master node of the EMR cluster and switch to the Hadoop user. Run the following command to run the demo:
```
[hadoop@10 hadoop]$ java –jar $package.jar
```
If the console outputs "Done", all operations are completed. You can switch to HBase Shell and run the `list` command to see whether the HBase table is successfully created with the API, and if yes, you can run the `scan` command to see the detailed content of the table.
```
[hadoop@10hbase]$ bin/hbase shell
hbase(main):002:0> list 'test1'
TABLE                                                                                           
Test1                                                                                           
1 row(s) in 0.0030 seconds

=> ["test1"]
hbase(main):006:0> scan 'test1'
ROW  COLUMN+CELL                                                                                 
row1   column=cf:a, timestamp=1530276759697, value=value1                                       
row2   column=cf:b, timestamp=1530276777806, value=value2                                       
row3   column=cf:c, timestamp=1530276792839, value=value3                                       
3 row(s) in 0.2110 seconds
```

For more information on API usage, please see the [official documentation](http://hbase.apache.org/book.html).
