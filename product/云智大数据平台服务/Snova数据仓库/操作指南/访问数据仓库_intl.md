Only the CVM instances in the same VPC subnet where a Snova cluster is located can access the cluster. Direct access from the Internet to the cluster is temporarily unsupported.

In the created Snova cluster, you need to use a database client to connect to the database before you can use the data warehouse service. Please connect to the database using the psql client tool as per the following instructions.

1. Obtain the cluster access address: Connect to the database using the IP and port in the cluster JDBC URL.
2. Connect to the cluster database: Install the client and connect to the cluster database.

## Prerequisites

1. The database admin password of the Snova cluster has been obtained, which is the admin account password set when the cluster is started.
2. The access IP and port as well as the VPC and subnet of the created Snova cluster have been obtained.

## Getting Cluster Access Address and Local Network Address

Go to the Snova Console and select a cluster as shown below. VPC: vpc-aejsd98p; subnet: subnet-83knqldq; Snova IP: 10.0.6.10; port: 5432; logged-in account: lambuser.

![](https://main.qcloudimg.com/raw/d2fe796b02ee65c85ba200f553bde533.png)

## Connecting to a Cluster Database Using Command Line

Select a CVM instance in the obtained VPC "vpc-aejsd98p" and subnet "subnet-83knqldq" (if there is no instance, purchase one). Log in to the instance and execute the following command to install the PostgreSQL client.

```
yum install -y postgresql.x86_64
```

You can log in successfully by executing the following SQL command and entering the password set when the cluster is created.

```
psql -h10.0.6.10  -p5432  -dpostgres  -Ulambuser
```

### Connecting to a Database Using JDBC

You need to get the official JDBC provided by PostgresSQL which is available [here](https://jdbc.postgresql.org/?spm=a2c4g.11186623.2.11.qEjVVl).

Or, add the following configuration to the pom.xml file:

```
<dependencies>
        <dependency>
            <groupId>org.postgresql</groupId>
            <artifactId>postgresql</artifactId>
            <version>42.2.2</version>
        </dependency>
</dependencies>
```

#### Code Example

```
package com.qcloud.snova_conn;

import java.io.InputStream;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.ResultSetMetaData;
import java.sql.Statement;
import java.sql.Timestamp;
import java.util.ArrayList;
import java.util.List;
import java.util.Properties;
import java.sql.Connection;  
import java.sql.ResultSet;  
import java.sql.SQLException;  
import com.yammer.metrics.core.Meter;

public class SnovaConn {
    /*
     * args: vip vport user pwd
     */
    public static void main(String[] args) throws ClassNotFoundException, SQLException {
        
            if (args.length < 4){
                 System.out.println("args err");
                 return;
            }
            
            String vip =  args[0];
            String vport =  args[1];
            String userName =  args[2];
            String userPwd =  args[3];
            
            System.out.printf("vip:%s, vport:%s, userName:%s, userPwd:%s\n",vip, vport, userName, userPwd);
            String jdbcUrl = "jdbc:postgresql://" + vip+":"+vport+"/maxluo";
            System.out.printf("jdbcUrl:%s \n",jdbcUrl);
            
            Class.forName("org.postgresql.Driver");  
            Connection snova = DriverManager.getConnection(jdbcUrl,userName,userPwd);  
            Statement st = snova.createStatement();  
            ResultSet rs = st.executeQuery("select * from test;");  
            while (rs.next()) {  
                System.out.print(rs.getString(1));  
                System.out.print("\n");  
            }  
            rs.close();  
            st.close(); 
            
        
    }

}
```

#### pom.xml Configuration

```
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>com.qcloud</groupId>
  <artifactId>snova-conn</artifactId>
  <version>0.0.1-SNAPSHOT</version>
  <packaging>jar</packaging>

  <name>snova-conn</name>
  <url>http://maven.apache.org</url>

  <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
        <maven.compiler.source>1.8</maven.compiler.source>
        <maven.compiler.target>1.8</maven.compiler.target>
    </properties>

  <dependencies>
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.40</version>
        </dependency>
        <dependency>
            <groupId>org.postgresql</groupId>
            <artifactId>postgresql</artifactId>
            <version>42.2.2</version>
        </dependency>
        <dependency>
            <groupId>com.microsoft.sqlserver</groupId>
            <artifactId>mssql-jdbc</artifactId>
            <version>6.4.0.jre8</version>
        </dependency>
        <dependency>
            <groupId>com.yammer.metrics</groupId>
            <artifactId>metrics-core</artifactId>
            <version>2.2.0</version>
        </dependency>
        <dependency>
            <groupId>ch.qos.logback</groupId>
            <artifactId>logback-classic</artifactId>
            <version>1.1.9</version>
        </dependency>
    </dependencies>

    <build>
        <plugins>
        
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
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-jar-plugin</artifactId>
                <configuration>
                    <excludes>
                        <exclude>*.properties</exclude>
                        <exclude>*.xml</exclude>
                        <exclude>*.json</exclude>
                        <exclude>*.sh</exclude>
                    </excludes>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-dependency-plugin</artifactId>
                <executions>
                    <execution>
                        <id>copy-dependencies</id>
                        <phase>package</phase>
                        <goals>
                            <goal>copy-dependencies</goal>
                        </goals>
                        <configuration>
                            <type>jar</type>
                            <includeTypes>jar</includeTypes>
                            <outputDirectory>
                                ${project.build.directory}/lib
                            </outputDirectory>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
</project>
```

Then use Maven to package and generate the jar file and upload it to the CVM instance (which can be any CVM instance in the same VPC subnet where the Snova cluster is located).

Execute the following command to install the JDK. 

```
yum install java
```

Executing the following command:

```
java -cp  snova-conn-0.0.1-SNAPSHOT-jar-with-dependencies.jar  com.qcloud.snova_conn.SnovaConn  10.0.8.5  5436   lambuser  lambpwd11
```

> **Note:**
>
> The VIP and port are the Snova cluster access address. The username and password are those set when the cluster is created. For details, see the section above.

Create a database and data table using command line and insert a certain amount of data.

The query result is as follows, which can read the data in the table "test" in the pre-created database "maxluo":

![](https://main.qcloudimg.com/raw/2ea8080f800a42f2d27e5b49d7b5af4f.png)
