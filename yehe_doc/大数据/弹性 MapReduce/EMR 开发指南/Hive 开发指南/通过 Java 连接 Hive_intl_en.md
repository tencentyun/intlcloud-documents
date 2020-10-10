Apache Hadoop Hive is integrated with the Thrift service. Thrift, created by Facebook, is an interface definition language and binary communication protocol used for defining and creating services for numerous languages. HiveServer2 is based on Thrift, allowing many languages such as Java and Python to call Hive's APIs. Additionally, JDBC Driver for Apache Hadoop Hive enables Java application to interact with the Hive database.

This section describes how to connect to HiveServer2 through Java code.

## 1. Prerequisites
- Confirm that you have activated Tencent Cloud and created an EMR cluster. When creating the EMR cluster, select the Hive component on the software configuration page. 
- Hive and its dependencies are installed in the EMR cluster directory `/usr/local/service/`.

## 2. Using Maven to Create a Project
### Viewing parameters
First, log in to any node (preferably a master one) in the EMR cluster. For more information about how to log in to EMR, please see [Logging in to a Linux Instance](https://intl.cloud.tencent.com/document/product/213/5436). Here, you can use WebShell to log in. Click *Login* on the right of the desired CVM instance and then enter the login page. The default username is root, and the password is the one you set when you created the EMR cluster. Once your credentials have been validated, you can access the command-line interface.

Run the following command in EMR command-line interface to switch to the Hadoop user, then go to the Hive installation folder:

```
[root@172 ~]# su hadoop
[hadoop@172 root]$ cd /usr/local/service/hive/
[hadoop@172 hive]$

```
View the parameters that are required for the program:
```
[hadoop@172 hive]$ vim conf/hive-site.xml

<property>
        <name>hive.server2.thrift.bind.host</name>
        <value>$hs2host</value>
</property>
<property>
        <name>hive.server2.thrift.port</name>
        <value>$hs2port</value>
</property>
```
Here, $hs2host is the hostID of your HiveServer2, and $hs2port is the port number of your HiveServer2.

### Creating a Maven project
Maven is recommended for project management, as it can help you manage project dependencies with ease. Specifically, it can get .jar packages through the configuration of the pom.xml file, eliminating your need to add them manually.

Download and install Maven in your local system first and then configure its environment variables. If you are using the IDE, please set the Maven-related configuration items in the IDE.

In the local shell environment, enter the directory where you want to create the Maven project, such as `D://mavenWorkplace`, and enter the following command to create it:

```
mvn archetype:generate -DgroupId=$yourgroupID -DartifactId=$yourartifactID -DarchetypeArtifactId=maven-archetype-quickstart
```
Here, $yourgroupID is your package name, $yourartifactID is your project name, and maven-archetype-quickstart indicates to create a Maven Java project. Some files need to be downloaded for creating the project, so please keep the network connected.

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
Among the files above, pay extra attention to the pom.xml file and the Java folder under the main directory. The pom.xml file is primarily used to create dependencies and package configurations; the Java folder is used to store your source codes.

First, add the Maven dependencies to pom.xml:
```
<dependencies>
        <dependency>
            <groupId>org.apache.hive</groupId>
            <artifactId>hive-jdbc</artifactId>
            <version>2.1.1</version>
        </dependency>
        <dependency>
            <groupId>org.apache.hadoop</groupId>
            <artifactId>hadoop-common</artifactId>
            <version>2.7.3</version>
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
Right-click in src>main>Java and create a Java Class. Enter the Class name (e.g., HiveTest.java here) and add the sample code to the Class:
```
import java.sql.*;

/**
 * Created by tencent on 2018/7/6.
*/
public class HiveTest {
    private static String driverName =
            "org.apache.hive.jdbc.HiveDriver";

    public static void main(String[] args)
            throws SQLException {
        try{
            Class.forName(driverName);
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
            System.exit(1);
        }

        Connection con = DriverManager.getConnection(
                "jdbc:hive2://$hs2host:$hs2port/default", "hadoop", "");
        Statement stmt = con.createStatement();
        String tableName = "HiveTestByJava";
        stmt.execute("drop table if exists " + tableName);
        stmt.execute("create table " + tableName +
                " (key int, value string)");
        System.out.println("Create table success!");
        // show tables
        String sql = "show tables '" + tableName + "'";
        System.out.println("Running: " + sql);
        ResultSet res = stmt.executeQuery(sql);
        if (res.next()) {
            System.out.println(res.getString(1));
        }

        // describe table
        sql = "describe " + tableName;
        System.out.println("Running: " + sql);
        res = stmt.executeQuery(sql);
        while (res.next()) {
            System.out.println(res.getString(1) + "\t" + res.getString(2));
        }

        sql = "insert into " + tableName + " values (42,\"hello\"),(48,\"world\")";
        stmt.execute(sql);

        sql = "select * from " + tableName;
        System.out.println("Running: " + sql);
        res = stmt.executeQuery(sql);
        while (res.next()) {
            System.out.println(String.valueOf(res.getInt(1)) + "\t"
                    + res.getString(2));
        }

        sql = "select count(1) from " + tableName;
        System.out.println("Running: " + sql);
        res = stmt.executeQuery(sql);
        while (res.next()) {
            System.out.println(res.getString(1));
        }
    }
}
```
>!The parameters $hs2host and $hs2port in the program should be replaced with the values of the hostID and port number of the HiveServer2 you queried.

The entire program will connect to the HiveServer2 before a table called HiveTestByJava is created in the default database. Then, insert two elements into the table and output the content of the entire table.

If your Maven is configured correctly and its dependencies are successfully imported, the project will be compiled directly. Enter the project directory in the local shell, and run the following command to package the entire project:
```
mvn package
```
Some files may need to be downloaded during the running process. "Build success" indicates that package is successfully created. You can see the generated .jar package in the target folder under the project directory.

## 3. Uploading and Running the Program
First, use the scp or sftp tool to upload the compressed .jar package to the EMR cluster. Run the following command in your local shell:
```
scp $localfile root@public IP address:/usr/local/service/hive
```
Here, $localfile is the path and the name of your local file; root is the CVM instance username. You can look up the public IP address in the node information in the EMR or CVM Console. Upload the compressed .jar package to the `/usr/local/service/hive` directory in the EMR cluster. After the upload is completed, you can check whether the file is in the corresponding folder by using EMR command lines. **Be sure to upload a .jar package that contains the dependencies.**

Log in to the EMR cluster, switch to the Hadoop user, and go to the `/usr/local/service/hive` directory. Then you can run the program:
```
[hadoop@172 hive]$ yarn jar $package.jar HiveTest
```
Here, $package.jar is the path and the name of your .jar package; HiveTest is the name of the previously created Java Class. The result is as follows:

```
Create table success!
Running: show tables 'HiveTestByJava'
hivetestbyjava
Running: describe HiveTestByJava
key	int
value	string
Running: select * from HiveTestByJava
42	hello
48	world
Running: select count(1) from HiveTestByJava
2

```

