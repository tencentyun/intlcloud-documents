>This document briefly describes how to modify the Hadoop configuration to enable it to access Kerberos. For secure clusters purchased through EMR, the required settings are already automatically configured by the system.

## Prerequisites
- The KDC service has been set up.
- The Hadoop-related principals have been created.
- The keytab file has been distributed to each server (assuming that its path is /var/krb5kdc/emr.keytab).

## Accessing Kerberos by Hadoop
Hadoop mainly contains HDFS and Yarn services. You need to modify their configurations separately and restart the service processes.

### HDFS Access
#### Modifying core-site.xml
```properties
hadoop.security.authentication: kerberos
hadoop.security.authorization: true
```

#### Modifying hdfs-site.xml
```properties
dfs.namenode.kerberos.principal: hadoop/_HOST@EMR
dfs.namenode.keytab.file: /var/krb5kdc/emr.keytab
dfs.namenode.kerberos.internal.spnego.principal: HTTP/_HOST@EMR
dfs.secondary.namenode.kerberos.principal: hadoop/_HOST@EMR
dfs.secondary.namenode.keytab.file: /var/krb5kdc/emr.keytab
dfs.secondary.namenode.kerberos.internal.spnego.principal: HTTP/_HOST@EMR
dfs.journalnode.kerberos.principal: hadoop/_HOST@EMR
dfs.journalnode.keytab.file: /var/krb5kdc/emr.keytab
dfs.journalnode.kerberos.internal.spnego.principal: HTTP/_HOST@EMR
dfs.datanode.kerberos.principal: hadoop/_HOST@EMR
dfs.datanode.keytab.file: /var/krb5kdc/emr.keytab
dfs.datanode.data.dir.perm: 700
dfs.web.authentication.kerberos.keytab: /var/krb5kdc/emr.keytab
dfs.web.authentication.kerberos.principal: HTTP/_HOST@EMR
ignore.secure.ports.for.testing: true
```

>The ignore.secure.ports.for.testing option must be set to true; otherwise, the sasl mode has to be configured, and webhdfs has to have HTTPS enabled.

#### Modifying httpfs-site.xml (If httpfs Is Enabled)
```properties
httpfs.authentication.type: kerberos
httpfs.hadoop.authentication.type: kerberos
httpfs.authentication.kerberos.principal: HTTP/_HOST@EMR
httpfs.hadoop.authentication.kerberos.principal: hadoop/_HOST@EMR
httpfs.authentication.kerberos.keytab: /var/krb5kdc/emr.keytab
httpfs.hadoop.authentication.kerberos.keytab: /var/krb5kdc/emr.keytab
```

### Yarn Access
#### Modifying yarn-site.xml
```properties
yarn.resourcemanager.keytab: /var/krb5kdc/emr.keytab
yarn.resourcemanager.principal: hadoop/_HOST@EMR
yarn.nodemanager.keytab: /var/krb5kdc/emr.keytab
yarn.nodemanager.principal: hadoop/_HOST@EMR
```

#### Modifying mapred-site.xml
```properties
mapreduce.jobhistory.keytab: /var/krb5kdc/emr.keytab
mapreduce.jobhistory.principal: hadoop/_HOST@EMR
```

