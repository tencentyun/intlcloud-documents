By default, only CVM instances in the same VPC subnet can access a CDWPG cluster. If you need to access it over the public network, apply for a [public IP](https://intl.cloud.tencent.com/document/product/1138/45132).

After creating a cluster, you need to use the database client to connect to the database before you can use the database services. Connect to the database with the client tool psql as instructed below.
1. Get the cluster access address: Connect to the database through the IP and port number in the JDBC URL of the cluster.
2. Connect to the cluster database: Install the client and connect to the cluster database.

## Prerequisites
1. You have obtained the password of the database admin account for the CDWPG cluster. The password is the one set when the cluster is created.
2. You have obtained the IP, port number, VPC, and subnet information to access the created CDWPG cluster.

## Getting Cluster Access Address and Local Network Information
Select the corresponding cluster with the details as shown below. Get the information of the `vpc-aejsd98p` VPC and `subnet-83knqldq` subnet. The IP to access CDWPG is `10.0.6.10`, the port number is `5432`, and the login account is `lambuser`.
![](https://qcloudimg.tencent-cloud.cn/raw/2f6149a9cb528c10a8b241298e67ce82.png)

## Connecting to Cluster Database on Command Line
Select a CVM instance in the obtained `vpc-aejsd98p` VPC and `subnet-83knqldq` subnet or purchase one if there is none. Log in to the instance and run the following command to install the PostgreSQL client.
```
yum install -y postgresql.x86_64
```
Run the following SQL command and enter the password set during cluster creation to log in.
```
psql –h10.0.6.10  –p5432  –dpostgres  –Ulambuser
```

## Connecting to Database with JDBC
Get the JDBC officially provided by PostgresSQL [here](https://jdbc.postgresql.org/?spm=a2c4g.11186623.2.11.qEjVVl).

Or, add the following configuration to the `pom.xml` file:
```
<dependencies>
        <dependency>
            <groupId>org.postgresql</groupId>
            <artifactId>postgresql</artifactId>
            <version>42.2.2</version>
        </dependency>
</dependencies>
```

#### Sample code
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

#### `pom.xml` configuration
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

Then, use Maven to package the `jar` file and upload the `jar` package to the CVM instance (any instance in the VPC subnet where the CDWPG cluster resides).

Run the following command to install JDK. 
```
yum install java
```

Run the following command:
```
java –cp  snova-conn-0.0.1-SNAPSHOT-jar-with-dependencies.jar  com.qcloud.snova_conn.SnovaConn  10.0.8.5  5436   lambuser  lambpwd11
```

>!The VIP and port number are the address to access the CDWPG cluster, and the username and password are those entered during cluster creation as detailed above.

Create a database and data table on the command line and insert a certain amount of data.

The query result is as shown below, where you can read the data in the `test` table in the `maxluo` database created previously.
![](https://main.qcloudimg.com/raw/2ea8080f800a42f2d27e5b49d7b5af4f.png)
