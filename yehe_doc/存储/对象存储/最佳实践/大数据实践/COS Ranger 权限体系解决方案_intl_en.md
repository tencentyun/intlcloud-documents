
## Background

Hadoop Ranger is a permission solution for big data scenarios. A user adopting the compute/storage separation mode can host data in COS. However, COS uses the CAM permission system, meaning that the user roles and permission policies could be different from those of Hadoop Ranger. Therefore, we introduce a solution to integrate COS with Ranger herein.


## Advantages

- Fine-grained and Hadoop-compatible permission control, allowing users to centrally manage permissions for big data components and data hosted in cloud.
- No need to set keys in core-site on the plugin side. Instead, keys are centrally set in COS Ranger Service to avoid key plaintext exposure.


## Solution Architecture

![](https://main.qcloudimg.com/raw/47bcff91b29614141b9c88efd39e50c1.png)

In the Hadoop permission system, the authentication is offered by Kerberos and authorized by Ranger. On the basis of this, the following components are introduced to support the COS Ranger permission solution:


1. COS Ranger Plugin: A service define plugin used on the Ranger server. It provides the COS service description, including permission types and definitions of required parameters (such as bucket and region), on the Ranger side. Once the plugin is deployed, users can set permission policies on the Ranger control panel.
2. COS Ranger Service: Integrates the Ranger client to periodically sync permission policies from the Ranger server, and verifies permissions locally when an authentication request is received. It also offers generation/lease renewal APIs relevant to DelegationToken of Hadoop. All APIs are defined through Hadoop IPC.
3. COS Ranger Client: COSN dynamically loads it and forwards the permission verification requests to COS Ranger Service.

## Environment Deployment

- Hadoop environment
- ZooKeeper, Ranger, and Kerberos (if there are authentication requirements)
>? As the above services are mature open-source components, you can install them on your own.
>

## Component Deployment
Deploy components in the following sequence: CHDFS Ranger Plugin, COS Ranger Service, COS Ranger Client, and COSN.
<dx-tabs>
::: Deploy COS Ranger Plugin
COS Ranger Plugin extends the service types of the Ranger Admin console. Users can configure the COS-related permissions in the Ranger console.


#### Source code download
You can go to [GitHub](https://github.com/tencentyun/cos-ranger-service) > ranger-plugin to obtain the source code.
#### Version
v1.1 or later
#### Deployment directions
1. Create a COS directory in the service definition directory in Ranger. Note that you should at least have execute and read permissions on the directory.
a. In the Tencent Cloud EMR environment, the path is `ranger/ews/webapp/WEB-INF/classes/ranger-plugins`.
b. In the self-built Hadoop environment, you can search the path of the Ranger-integrated components (such as HDFS) to find the path.
![](https://main.qcloudimg.com/raw/793f47a53343657a000b34b7ac66b074.png)
2. Place `cos-chdfs-ranger-plugin-xxx.jar` (with at least the `r` permission) and `cos-ranger.json` files in the COS root directory. You can get them from [GitHub](https://github.com/tencentyun/cos-ranger-service/tree/main/ranger-plugin).
3. Restart Ranger.
4. Register COS service in Ranger. A command sample is as follows:
<dx-codeblock>
::: plaintext
## Create the service. The Ranger admin account and password, as well as the Ranger service address should be specified.
## For an EMR cluster, the admin user is `root`, and the password is the root password set when the EMR cluster is created. Replace the IP of the Ranger service with the master node IP of EMR.
adminUser=root
## Password set during EMR cluster creation, which is also the login password of the Ranger web service.
adminPasswd=xxxxxx
## If the Ranger service has multiple master nodes, select any of them.
rangerServerAddr=10.0.0.1:6080
## Specify the .json file in step 2 as `-d` in the command.
curl -v -u${adminUser}:${adminPasswd} -X POST -H "Accept:application/json" -H "Content-Type:application/json" -d @./cos-ranger.json http://${rangerServerAddr}/service/plugins/definitions
## To delete a defined service, for example, the service created above, pass the service ID that is returned when you created the service.
serviceId=102
curl -v -u${adminUser}:${adminPasswd} -X DELETE -H "Accept:application/json" -H "Content-Type:application/json" http://${rangerServerAddr}/service/plugins/definitions/${serviceId}
:::
</dx-codeblock>
5. When the service is created successfully, you can view the COS service in the Ranger console, as shown in the following figure:
![](https://main.qcloudimg.com/raw/d1a6e2722d11f7177636a5e2c54226e3.png)
6. Click the **+** icon on the right of the COS service to define the service instance. On the **Edit Service** page, customize the **Service Name**, for example, `cos` or `cos_test`, as shown below:
![](https://main.qcloudimg.com/raw/2be86fb2b8232b16679b29e908f82d3a.png)
Where, `policy.grantrevoke.auth.users` needs to be set to the name of the user that is used to launch COS Ranger Service (i.e., the user that is allowed to pull permission policies). We recommend you set it to `hadoop`, which can be used as the username to launch COS Ranger Service in subsequent operations.
7. Click the newly created COS service instance.
![](https://qcloudimg.tencent-cloud.cn/raw/bc48921e23571e81367b1c3aa8ca52a8.png)
Add a policy as shown below:
![](https://main.qcloudimg.com/raw/58ded7125d5c5d161ca6e2f5a98d8e7b.png)
8. On the page that is displayed, configure the following parameters:
 - **Bucket**: Bucket name, for example, `examplebucket-1250000000`. It can be queried in the [COS console](https://console.cloud.tencent.com/cos5/bucket).
 - **Path**: Path of the COS object. Note that it does not start with a slash (/).
    - include: Indicates whether the permission applies to the specified path, or other paths except for the specified path.
    - recursive: Indicates the permission applies to the specified path as well as the subpaths (i.e., the recursive subpaths) under it. It is usually used when the path is set to a directory.
 - **Select Group/Select User**: Username and user group in logical OR relationship; that is, the operation is authorized as long as the username or user group condition is met.
 - **Permissions**:
    -  Read: Permission on operations such as downloading objects and querying the object metadata. It corresponds to the GET and HEAD operations in COS.
    -  Write: Permissions on operations such as uploading objects. It corresponds to the PUT operation in COS.
    -  Delete: Delete permission. It corresponds to the delete object operation in COS. To rename a path in Hadoop, you need to have delete permission on the original path and write permission on the new path.
    -  List: Traverse permission. It corresponds to the List Object operation in COS.
![](https://main.qcloudimg.com/raw/00a619b4b963a9acf766411fad722fe4.png)
:::
::: Deploy COS Ranger Service
COS Ranger Service is the core of the permission system. It integrates with the Ranger client to receive the authentication requests, token generation and lease renewal requests, and temp key generation requests of the Ranger client. It is also where the sensitive information (Tencent Cloud keys) are stored. Usually, it is deployed on the jump server, and only the cluster admin can perform operations and query the configurations.

COS Ranger Service supports the one-master, multiple-slave HA deployment. `DelegationToken` can be stored to HDFS, and the master and slave nodes can be determined by ZooKeeper lock obtaining. Then, the master node will write the address to Zookeeper so that COS Ranger Client can perform address routing.

#### Source code download
You can go to [GitHub](https://github.com/tencentyun/cos-ranger-service) > `cos-ranger-server` directory to obtain the source code.

#### Version
v5.0.6 or later

#### Deployment directions
1. Copy the code of COS Ranger Service to several nodes of the cluster. In the production environment, the code should be copied to at least two nodes (one master node, and one slave node). As sensitive information is involved, we recommend you use jump servers or nodes with tight permission control.
2. Modify the relevant configuration items in the `cos-ranger.xml` file. Those that must be modified are as follows. For the description of the configuration items, see the comments in the file. You can get the configuration file in the `cos-ranger-service/conf` directory at [GitHub](https://github.com/tencentyun/cos-ranger-service).
 -  qcloud.object.storage.rpc.address
 -  qcloud.object.storage.status.port
 -  qcloud.object.storage.enable.cos.ranger
 -  qcloud.object.storage.zk.address (ZooKeeper address. After COS Ranger Service starts, it will be registered in ZooKeeper)
 -  qcloud.object.storage.cos.secret.id
 -  qcloud.object.storage.cos.secret.key
3. Modify the relevant configuration items in the `ranger-cos-security.xml` file. Those that must be modified are as follows. For the description of the configuration items, see the comments in the file. You can get the configuration file in the `cos-ranger-service/conf` directory at [GitHub](https://github.com/tencentyun/cos-ranger-service).
 -  ranger.plugin.cos.policy.cache.dir
 -  ranger.plugin.cos.policy.rest.url
 -  ranger.plugin.cos.service.name
4. In the `start_rpc_server.sh` file, modify the configuration of `hadoop_conf_path` and `java.library.path`, which corresponds to the directory of the Hadoop configuration files (for example, `core-site.xml` and `hdfs-site.xml`) and hadoop native libraries, respectively.
5. Run the following command to launch the service:
```
chmod +x start_rpc_server.sh
nohup ./start_rpc_server.sh &> nohup.txt &
```
6. If the launch failed, check whether an error message is contained in the error log.
7. COS Ranger Service supports displaying the HTTP port status (port name: `qcloud.object.storage.status.port`. Default value: `9998`). You can run the following command to obtain the status information, such as whether the leader is contained, and the authentication statistics:
```
# Replace `10.xx.xx.xxx` with the IP address of the device deployed with the ranger service.
# Replace `9998` in the command with the value of `qcloud.object.storage.status.port`.in the configuration file.
curl -v http://10.xx.xx.xxx:9998/status
```
 - If only one COS Ranger Service node is deployed, you can see that the current node becomes the leader in the above API response.
 - If multiple COS Ranger Service nodes are deployed, you can see that another node becomes the leader in the above API response. After all nodes are restarted, you can see that the first restarted node becomes the leader.

:::
::: Deploy COS Ranger Client
COS Ranger Client is dynamically loaded by the Hadoop COSN plugin. It is a proxy that encapsulates all COS Ranger Service access requests, such as obtaining temp keys, obtaining tokens, and performing authentication.

#### Source code download
You can go to [GitHub](https://github.com/tencentyun/cos-ranger-service) > cos-ranger-client to obtain the source code.

#### Version
v3.8 or later

#### Deployment directions
1. Copy the JAR packages of COS Ranger Client and COS Ranger Interface to the same directory as COSN (in the `/usr/local/service/hadoop/share/hadoop/common/lib/` directory generally). Be sure to select JAR packages whose major version is the same as that of Hadoop and make sure that them have the read permission.
2. Add the following configuration in `core-site.xml`:
<dx-codeblock>
::: xml
```
<configuration>
           <!--*****Required Configuration********-->
           <!-- ZooKeeper address, from which the client can obtain the ranger-service address -->
           <property>
               <name>qcloud.object.storage.zk.address</name>
               <value>10.0.0.8:2181,10.0.0.9:2181,10.0.0.10:2181</value>
           </property>

           <!--***Optional Configuration****-->           
           <!-- Set the Kerberos credential used on the COS Ranger Service side. It should be the same as that configured on the COS Ranger Service side. If verification is not involved, you can skip this configuration. -->
           <property>                
					 <name>qcloud.object.storage.kerberos.principal</name>
					 <value>hadoop/_HOST@EMR-XXXX</value>
           </property>

         <!--***Optional Configuration****-->  
         <!-- IP address path of the Ranger server recorded in ZooKeeper. The default value is used herein. The value must the same as that configured in COS Ranger Service. -->
          <property>              
					<name>qcloud.object.storage.zk.leader.ip.path</name> 
					<value>/ranger_qcloud_object_storage_leader_ip</value>
          </property>
         <!-- IP address path of the COS Ranger Service follower recorded in ZooKeeper. The default value is used here. The value must the same as that configured in COS Ranger Service. The master and slave nodes provide the service at the same time. -->
          <property>
                    <name>qcloud.object.storage.zk.follower.ip.path</name>
                    <value>/ranger_qcloud_object_storage_follower_ip</value>
          </property>
</configuration>
```
:::
</dx-codeblock>
:::
::: Deploy COSN
#### Version
v8.0.1 or later

#### Deployment directions
For detailed directions on the deployment of COSN, see [Hadoop Tool](https://intl.cloud.tencent.com/document/product/436/6884). Note the following:

1. If Ranger is used, the key information of `fs.cosn.userinfo.secretId` and `fs.cosn.userinfo.secretKey` does not need to be configured. COSN will obtain the temp key via COS Ranger Service.
2. `fs.cosn.credentials.provider` needs to be set to `org.apache.hadoop.fs.auth.RangerCredentialsProvider` so that the verification and authentication can be performed via Ranger. The following is an example:
<dx-codeblock>
::: plaintext 
```
<property>
         <name>fs.cosn.credentials.provider</name>
         <value>org.apache.hadoop.fs.auth.RangerCredentialsProvider</value>
</property>
```
:::
</dx-codeblock>
:::
</dx-tabs>


## Verification

1. Use Hadoop commands to perform operations related to COSN access, i.e., check whether the current operations comply with the permissions set by the root account.
```plaintext
# Replace the bucket, path, and other information with that of the root account.
hadoop fs -ls cosn://examplebucket-1250000000/doc
hadoop fs -put ./xxx.txt cosn://examplebucket-1250000000/doc/
hadoop fs -get cosn://examplebucket-1250000000/doc/exampleobject.txt
hadoop fs -rm cosn://examplebucket-1250000000/doc/exampleobject.txt
```
2. Use MR Job for verification. Before the verification, related services, such as Yarn and Hive, should be restarted first.


## FAQs

#### Must Kerberos be installed?
Kerberos meets the authentication needs. If the cluster and users are trusted, and the purpose of the authentication is only to avoid maloperations caused by unauthorized users, you can skip installing Kerberos and only use Ranger for authentication. As a matter of fact, Kerberos also compromises performance. Therefore, you can balance your needs for security and performance. If authentication is needed, you can enable Kerberos, and then configure COS Ranger Service and COS Ranger Client.
#### What would happen if I enable Ranger, but haven’t set any policy or no policy is matched?
If no policy is matched, the operation will be denied by default.
#### Can a sub-account configure the key on the COS Ranger Service side?
Yes. A sub-account with relevant permissions on the operated bucket can generate a temp key for the COSN plugin and operate relevant operations. Normally, you can grant all permissions of the bucket to the configured key.
#### How can I update the temp key? Do I need to obtain it from COS Ranger Service every time before I access COS?
The temp key is cached on the COSN side. It will be periodically updated asynchronously.

### What should I do if the policy modified on the Ranger page doesn't take effect?
Decrease the `ranger.plugin.cos.policy.pollIntervalMs` value (in milliseconds) in the `ranger-cos-security.xml` file and restart COS Ranger Service. After the policy is tested, we recommend you change it back to the original value (if the time interval is too short, the polling frequency will be high, causing a high CPU utilization).
