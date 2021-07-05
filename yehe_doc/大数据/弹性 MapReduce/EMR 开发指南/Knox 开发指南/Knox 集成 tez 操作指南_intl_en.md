This document describes how to integrate Knox with Tez, such as installing Tomcat and Tez UI, creating roles, configuring Timeline Server, configuring Tez, and starting services. `172.**.**.9` is the private IP of the master node, `159.**.**.70` is the public IP of the master node, and the Tez version is v0.9.2.

## Installing Tomcat and Tez UI 
```
cd  /usr/local/service
wget https://mirror-hk.koddos.net/apache/tomcat/tomcat-9/v9.0.46/bin/apache-tomcat-9.0.46.tar.gz
tar -zxvf apache-tomcat-9.0.46.tar.gz
mv /usr/local/service/apache-tomcat-9.0.46 /usr/local/service/tomcat
```
Modify Tomcat port numbers:
```
vim /usr/local/service/tomcat/conf/server.xml
```
1. Change `8005` to `2020`.
![](https://main.qcloudimg.com/raw/f2671aa74d382897c4a373d8a994802a.png)                      
2. Change `8080` to `2000`.
![](https://main.qcloudimg.com/raw/40176a1db40180919d47924b7544a901.png)

```
mkdir -p /usr/local/service/tomcat/webapps/tez-ui
cp /usr/local/service/tez/tez-ui-0.9.2.war /usr/local/service/tomcat/webapps/tez-ui/
cd /usr/local/service/tomcat/webapps/tez-ui
unzip tez-ui-0.9.2.war
vim ./config/configs.env
```
Change `localhost` to the private IP of the current server.
![](https://main.qcloudimg.com/raw/c62c7ad792096c3033d1e38ba94a3cbe.png)

## Creating roles
```
vim /usr/local/service/knox/conf/topologies/emr.xml 
```
**Modify the `emr.xml` file:**
1. Add the following content:
![](https://main.qcloudimg.com/raw/81c51a74c086002a9089ae2ca676865b.png)
```
<param>
    <name>TEZUI</name>
<value>maxFailoverAttempts=3;failoverSleep=1000;enabled=true</value>
</param>
 <param>
     <name>APPLICATIONHISTORY</name>
<value>maxFailoverAttempts=3;failoverSleep=1000;enabled=true</value>
</param>
```

2. Add the following content:
![](https://main.qcloudimg.com/raw/f97bacdc69f9b28a34f4789dbf715991.png)
```
<service>
		<role>TEZUI</role>
		<url>http://172.**.**.9:2000/tez-ui</url>
		<version>0.9.2</version>
</service>
<service>
		<role>APPLICATIONHISTORY</role>
		<url>http://172.**.**.9:8188</url>
		<version>2.7.3</version>
</service>
```

## Configuring YARN Timeline Server
Modify the `yarn-site.xml` file in configuration management, save the changes, and restart the components whose configuration has been changed.

| Parameter                                                     | Value               |
| --------------------------------------------------------- | ----------------- |
| yarn.timeline-service.enabled                             | true              |
| yarn.timeline-service.hostname                            | `172.**.**.9` (replace it with your IP)       |
| yarn.timeline-service.http-cross-origin.enabled           | true              |
| yarn.resourcemanager.system-metrics-publisher.enabled     | true              |
| yarn.timeline-service.address                             | `172.**.**.9:10201` (replace it with your IP) |
| yarn.timeline-service.webapp.address                      |`172.**.**.9:8188` (replace it with your IP.) |
| yarn.timeline-service.webapp.https.address                | `172.**.**.9:2191` (replace it with your IP) |
| yarn.timeline-service.generic-application-history.enabled | true              |
| yarn.timeline-service.handler-thread-count                | 24                |

   
## Modifying Tez Configuration
In the `tez-site.xml` file, add the following parameters, save the changes, and restart the components whose configuration has been changed.

| Parameter                             | Value                                                          |
| --------------------------------- | ------------------------------------------------------------ |
| tez.tez-ui.history-url.base       | `http://172.**.**.9:2000/tez-ui/` (replace it with your IP)                           |
| tez.history.logging.service.class | org.apache.tez.dag.history.logging.ats.ATSHistoryLoggingService |
 

## Starting Services
1. Start Timeline Server.
```
/usr/local/service/hadoop/sbin/yarn-daemon.sh  start timelineserver  
```
2. Start Tomcat.
```
/usr/local/service/tomcat/bin/startup.sh  
```
3. Restart Tez.
```
su hadoop
rm -rf  /usr/local/service/knox/data/deployments/*
/usr/local/service/knox/bin/ldap.sh stop
/usr/local/service/knox/bin/ldap.sh start
/usr/local/service/knox/bin/gateway.sh stop
/usr/local/service/knox/bin/gateway.sh start
```
4. Access Tez UI at the following address.
>?The account and password are the same as the server login account and password.
>
```
https://{public IP of the cluster}:30002/gateway/emr/tez/  
```
