## Hadoop Commands

### Ticket not obtained
If Kerberos is enabled, you need to obtain a ticket before running a Hadoop command.

Otherwise, the following error message will appear:
```
hadoop fs -ls /
19/04/19 19:59:03 WARN ipc.Client: Exception encountered while connecting to the server : javax.security.sasl.SaslException: GSS initiate failed [Caused by GSSException: No valid credentials provided (Mechanism level: Failed to find any Kerberos tgt)]
ls: Failed on local exception: java.io.IOException: javax.security.sasl.SaslException: GSS initiate failed [Caused by GSSException: No valid credentials provided (Mechanism level: Failed to find any Kerberos tgt)]; Host Details : local host is: "172.30.0.27/172.30.0.27"; destination host is: "172.30.0.27":4007; 
```

### Obtaining a ticket
Prerequisites: The principal of hadoop@EMR has been added.
```
kinit -kt /var/krb5kdc/emr.keytab hadoop@EMR
```

Run the command to access normally.
```
hadoop fs -ls /

Found 8 items
-rw-r--r--   3 hadoop supergroup       3809 2019-03-06 11:10 /README.md
drwxr-xr-x   - hadoop supergroup          0 2019-01-14 21:43 /apps
drwxrwx---   - hadoop supergroup          0 2019-01-17 19:46 /emr
drwxr-xr-x   - hadoop supergroup          0 2019-01-23 20:02 /hbase
drwxr-xr-x   - hadoop supergroup          0 2019-03-07 11:10 /spark-history
drwx-wx-wx   - hadoop supergroup          0 2019-03-06 20:23 /tmp
drwxr-xr-x   - hadoop supergroup          0 2019-01-17 14:43 /user
drwxr-xr-x   - hadoop supergroup          0 2019-01-17 19:43 /usr
```

## Accessing HDFS Through Java Code

### Using a local ticket

>!You need to run kinit in advance to obtain a ticket. After the ticket expires, the program cannot be accessed.

```java
public static void main(String[] args) throws IOException {
	Configuration conf = new Configuration();
	conf.addResource(new Path("/usr/local/service/hadoop/etc/hadoop/hdfs-site.xml"));
	conf.addResource(new Path("/usr/local/service/hadoop/etc/hadoop/core-site.xml"));
	UserGroupInformation.setConfiguration(conf);
	UserGroupInformation.loginUserFromSubject(null);
	FileSystem fileSystem = FileSystem.get(conf);
	FileStatus[] fileStatus = fileSystem.listStatus(new Path("/"));
	for (int i = 0; i < fileStatus.length; i++) {
		System.out.println(fileStatus[i].getPath());
	}
}
```

### Using a keytab file

```java
public static void main(String[] args) throws IOException {
	Configuration conf = new Configuration();
	conf.addResource(new Path("/usr/local/service/hadoop/etc/hadoop/hdfs-site.xml"));
	conf.addResource(new Path("/usr/local/service/hadoop/etc/hadoop/core-site.xml"));
	UserGroupInformation.setConfiguration(conf);
	UserGroupInformation.loginUserFromKeytab("hadoop@EMR", "/var/krb5kdc/emr.keytab");
	FileSystem fileSystem = FileSystem.get(conf);
	FileStatus[] fileStatus = fileSystem.listStatus(new Path("/"));
	for (int i = 0; i < fileStatus.length; i++) {
		System.out.println(fileStatus[i].getPath());
	}
}
```
