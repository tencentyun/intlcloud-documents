
## Background

Hadoop Ranger is a permission solution for big data scenarios. By adopting the computing/storage separation mode, you can host data in COS. However, COS uses the CAM permission system, meaning that user roles and permission policies may be different from those of Hadoop Ranger. Therefore, a solution is introduced here to integrate COS with Ranger.


## Strengths

- Fine-grained and Hadoop-compatible permission control allow you to centrally manage permissions for big data components and data hosted in the cloud.
- There is no need to set keys in core-site on the plugin side; instead, keys are centrally set in COS Ranger Service to avoid key plaintext exposure.


## Solution Architecture

![](https://main.qcloudimg.com/raw/47bcff91b29614141b9c88efd39e50c1.png)

In the Hadoop permission system, authentication is offered by Kerberos and authorized by Ranger. On the basis of this, the following components are provided to support the COS Ranger permission solution:


1. COS Ranger Plugin: As a service defining plugin used on the Ranger server, it provides the COS service description on the Ranger side, including permission types and definitions of required parameters (such as bucket and region). Once it is deployed, you can set permission policies on the Ranger control panel.
2. COS Ranger Service: It integrates the Ranger client, periodically syncs permission policies from the Ranger server, and verifies the permission locally after receiving an authentication request. In addition, it also provides `DelegationToken` generation and renewal APIs in Hadoop, all of which are defined through Hadoop IPC.
3. Cos Ranger Client: It is dynamically loaded by the COSN plugin to forward permission verification requests to COS Ranger Service.

## Environment Deployment

- Hadoop environment
- ZooKeeper, Ranger, and Kerberos (if there are authentication requirements)
>? The components above are open-source and stable. You can install them on your own.
>

## Component Deployment
Deploy components in the following sequence: COS Ranger Plugin, COS Ranger Service, COS Ranger Client, COSN.
<dx-tabs>
::: Deploying COS Ranger Plugin
COS Ranger Plugin extends the service types in the Ranger Admin console. You can set the operation permissions related to COS in the Ranger console.


#### Code address
You can get the code from the `ranger-plugin` directory at [GitHub](https://github.com/tencentyun/cos-ranger-service).
#### Version
v1.0 or later.
#### Deployment steps
1. Create a `COS` directory in the service definition directory of Ranger (note: make sure that the directory permissions include at least `x` and `r` permissions).
a. For an EMR environment, the path is `ranger/ews/webapp/WEB-INF/classes/ranger-plugins`.
b. For a self-built Hadoop environment, you can find the components connected to the Ranger service through `find hdfs` in the `ranger` directory in order to find the location of the directory.
![](https://main.qcloudimg.com/raw/793f47a53343657a000b34b7ac66b074.png)
2. Place `cos-chdfs-ranger-plugin-xxx.jar` (with at least the `r` permission) and `cos-ranger.json` files in the COS directory. You can get them from [GitHub](https://github.com/tencentyun/cos-ranger-service/tree/main/ranger-plugin).
3. Restart Ranger.
4. Register the COS service on Ranger. You can refer to the following command:
<dx-codeblock>
::: plaintext
## Create the service. The Ranger admin account and password as well as the Ranger service address should be specified.
## For an EMR cluster, the admin user is `root`, and the password is the root password set when the EMR cluster is created. Replace the IP of the Ranger service with the primary node IP of EMR.
adminUser=root
## The password set during EMR cluster creation, which is also the login password of the Ranger web service.
adminPasswd=xxxxxx
## If the Ranger service has multiple primary nodes, select any of them.
rangerServerAddr=10.0.0.1:6080
## Specify the .json file in step 2 as `-d` in the command.
curl -v -u${adminUser}:${adminPasswd} -X POST -H "Accept:application/json" -H "Content-Type:application/json" -d @./cos-ranger.json http://${rangerServerAddr}/service/plugins/definitions
## To delete the service just defined, you need to pass in the service ID returned during creation.
serviceId=102
curl -v -u${adminUser}:${adminPasswd} -X DELETE -H "Accept:application/json" -H "Content-Type:application/json" http://${rangerServerAddr}/service/plugins/definitions/${serviceId}
:::
</dx-codeblock>
5. After the service is successfully created, you can see the COS service in the Ranger console.
![](https://main.qcloudimg.com/raw/d1a6e2722d11f7177636a5e2c54226e3.png)
6. Click **+** next to the COS service to define a new service instance. The service instance name is customizable; for example, you can enter `cos` or `cos_test`. The service configuration is as follows:
![](https://main.qcloudimg.com/raw/2be86fb2b8232b16679b29e908f82d3a.png)
You need to set the username subsequently used to start COS Ranger Service (i.e., the user allowed to pull permission policies) as `policy.grantrevoke.auth.users`. We generally recommend you set it to `hadoop`.
7. Click the newly created COS service instance.
![](https://qcloudimg.tencent-cloud.cn/raw/bc48921e23571e81367b1c3aa8ca52a8.png)
Add a policy.
![](https://main.qcloudimg.com/raw/58ded7125d5c5d161ca6e2f5a98d8e7b.png)
8. On the page that is displayed, configure the following parameters:
 - **Bucket**: Bucket name, such as `examplebucket-1250000000`, which can be viewed in the [COS console](https://console.cloud.tencent.com/cos5/bucket).
 - **Path**: Path of the COS object. Note that it does not start with a slash (/).
    - include: Indicates whether the set permission applies to the specified path itself or other paths except it.
    - recursive: Indicates that the permission applies to not only the specified path but also the subpaths under it (i.e., recursive subpaths). It is usually used when the path is set as a directory.
 - **User/Group**: Username and user group in logical OR relationship; that is, the operation is authorized as long as the username or user group condition is met.
 - **Permissions**:
    - Read: Read operation, which corresponds to the GET and HEAD operations in COS, such as downloading objects and querying object metadata.
    - Write: Write operation, which corresponds to the PUT operation in COS, such as uploading objects.
    - Delete: Deletion operation, which corresponds to the object deletion operation in COS. To rename a path in Hadoop, you need to have the deletion permission for the original path and write permission for the new path.
    - List: Traversal permission, which corresponds to the `List Object` operation in COS.
![](https://main.qcloudimg.com/raw/00a619b4b963a9acf766411fad722fe4.png)
:::
::: Deploying COS Ranger Service
COS Ranger Service is the core of the entire permission system. It is responsible for integrating the Ranger client and receiving its authentication requests, token generation and renewal requests, and temporary key generation requests. It is also where sensitive information (Tencent Cloud key information) resides. Generally, it is deployed on a bastion host, and only the cluster admin is allowed to manipulate it and view its configuration.

COS Ranger Service supports the one-primary-multiple-secondary HA deployment. `DelegationToken` can be persisted to HDFS, and the primary and secondary nodes can be determined by ZooKeeper lock obtaining. Then, the primary node (leader) will write the address to ZooKeeper so that COS Ranger Client can perform address routing.

#### Code address
You can get the code from the `cos-ranger-server` directory at [GitHub](https://github.com/tencentyun/cos-ranger-service).

#### Version
v5.1.2 or later.

#### Deployment steps
1. Copy the code of COS Ranger Service to the servers in the cluster. We recommend you configure at least two servers (one primary server and one secondary server) in the production environment. As sensitive information is involved, we recommend you use bastion hosts or servers with tight permission control.
2. Modify the relevant configuration items in the `cos-ranger.xml` file. Those that must be modified are as follows. For the description of the configuration items, see the comments in the file. You can get the configuration file in the `cos-ranger-service/conf` directory at [GitHub](https://github.com/tencentyun/cos-ranger-service).
 -  qcloud.object.storage.rpc.address
 -  qcloud.object.storage.status.port
 -  qcloud.object.storage.enable.cos.ranger
 -  qcloud.object.storage.zk.address (ZooKeeper address. After COS Ranger Service starts, it will be registered in ZooKeeper.)
 -  qcloud.object.storage.cos.secret.id
 -  qcloud.object.storage.cos.secret.key
3. Modify the relevant configuration items in the `ranger-cos-security.xml` file. Those that must be modified are as follows. For the description of the configuration items, see the comments in the file. You can get the configuration file in the `cos-ranger-service/conf` directory at [GitHub](https://github.com/tencentyun/cos-ranger-service).
 -  ranger.plugin.cos.policy.cache.dir
 -  ranger.plugin.cos.policy.rest.url
 -  ranger.plugin.cos.service.name
4. In the `start_rpc_server.sh` file, modify the configuration of `hadoop_conf_path` and `java.library.path`, which correspond to the directory of the Hadoop configuration file (for example, `core-site.xml` or `hdfs-site.xml`) and Hadoop native libraries, respectively.
5. Run the following command to start the service:
```
chmod +x start_rpc_server.sh
nohup ./start_rpc_server.sh &> nohup.txt &
```
6. If the start failed, check whether an error message is contained in the error log.
7. COS Ranger Service supports displaying the HTTP port status (port name: `qcloud.object.storage.status.port`; default value: `9998`). You can run the following command to get the status information, such as whether the leader is contained and the authentication statistics:
```
# Replace `10.xx.xx.xxx` with the IP address of the server deployed with the Ranger service.
# Replace `9998` in the command with the value of `qcloud.object.storage.status.port` in the configuration file.
curl -v http://10.xx.xx.xxx:9998/status
```
 - If only one COS Ranger Service node is deployed, you can see that the current node becomes the leader in the above API response.
 - If multiple COS Ranger Service nodes are deployed, you can see that another node becomes the leader in the above API response. After all nodes are restarted, you can see that the first restarted node becomes the leader.

:::
::: Deploying COS Ranger Client
COS Ranger Client is dynamically loaded by the Hadoop COSN plugin. It is a proxy that encapsulates all COS Ranger Service access requests, such as obtaining temporary keys, obtaining tokens, and performing authentication.

#### Code address

You can get the code from the `cos-ranger-client` and `cosn-ranger-interface` directories at [GitHub](https://github.com/tencentyun/cos-ranger-service).

#### Version

v5.0 or later for COS Ranger Client.  
v1.0.4 or later for COSN Ranger Interface.

#### Deployment directions
1. Copy the JAR packages of COS Ranger Client and COSN Ranger Interface to the same directory as COSN (in the `/usr/local/service/hadoop/share/hadoop/common/lib/` directory generally). Be sure to select JAR packages with the same major version as Hadoop and make sure that they have the read permission.
2. Add the following configuration in `core-site.xml`:
<dx-codeblock>
::: xml
```
<configuration>
           <!--*****Required configuration********-->
           <!-- Address of the COS Ranger server deployed in the previous step -->
           <property>
               <name>qcloud.object.storage.ranger.service.address</name>
               <value>10.0.0.8:9999,10.0.0.10:9999</value>
           </property>

           <!--***Optional configuration****-->           
           <!-- Set the Kerberos credential used in COS Ranger Service. It should be the same as that configured in COS Ranger Service. If verification is not involved, you can skip this configuration. -->
           <property>                
					 <name>qcloud.object.storage.kerberos.principal</name>
					 <value>hadoop/_HOST@EMR-XXXX</value>
           </property>

         <!--***Optional configuration****-->  
         <!-- IP address path of the Ranger server recorded in ZooKeeper. The default value is used here. The value must the same as that configured in COS Ranger Service. -->
          <property>              
					<name>qcloud.object.storage.zk.leader.ip.path</name> 
					<value>/ranger_qcloud_object_storage_leader_ip</value>
          </property>
         <!-- IP address path of the COS Ranger Service follower recorded in ZooKeeper. The default value is used here. The value must the same as that configured in COS Ranger Service. Both the primary and secondary nodes provide services at the same time. -->
          <property>
                    <name>qcloud.object.storage.zk.follower.ip.path</name>
                    <value>/ranger_qcloud_object_storage_follower_ip</value>
          </property>
</configuration>
```
:::
</dx-codeblock>
:::
::: Deploying COSN
#### Version
v8.0.1 or later.

#### Deployment directions
For detailed directions on the deployment of COSN, see [Hadoop](https://intl.cloud.tencent.com/document/product/436/6884). Note the following:

1. If Ranger is used, the key information of `fs.cosn.userinfo.secretId` and `fs.cosn.userinfo.secretKey` does not need to be configured. COSN will get temporary keys through COS Ranger Service.
2. `fs.cosn.credentials.provider` needs to be set to `org.apache.hadoop.fs.auth.RangerCredentialsProvider`, so that the verification and authentication can be passed through Ranger. Below is an example:
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

1. Use Hadoop commands to perform operations involving COSN access to check whether the current operations comply with the permissions set by the root account. Below is an example:
```plaintext
# Replace the bucket, path, and other information with that of the root account.
hadoop fs -ls cosn://examplebucket-1250000000/doc
hadoop fs -put ./xxx.txt cosn://examplebucket-1250000000/doc/
hadoop fs -get cosn://examplebucket-1250000000/doc/exampleobject.txt
hadoop fs -rm cosn://examplebucket-1250000000/doc/exampleobject.txt
```
2. Use MR Job for verification. Before the verification, be sure to restart related services such as YARN and Hive.


## FAQs

#### Do I have to install Kerberos?
Kerberos meets the authentication needs. If users in a cluster are trusted, and the purpose of the authentication is only to avoid maloperations performed by unauthorized users, you can skip installing Kerberos and only use Ranger for authentication. As a matter of fact, Kerberos also compromises the performance. Therefore, you can balance your needs for security and performance as needed. If authentication is needed, you can enable Kerberos and then configure COS Ranger Service and COS Ranger Client.
#### What would happen if I enable Ranger but don't set any policy or no policy is matched?
If no policy is matched, the operation will be denied by default.
#### Can a sub-account configure the key in COS Ranger Service?
Yes. A sub-account with relevant permissions of the manipulated bucket can generate a temporary key for the COSN plugin to perform corresponding operations. Normally, you can grant all permissions of the bucket to the configured key.
#### How do I update a temporary key? Do I need to get it from COS Ranger Service every time before I access COS?
The temporary key is cached in the COSN plugin. It will be periodically updated asynchronously.
#### What should I do if the policy modified on the Ranger page doesn't take effect?
Decrease the `ranger.plugin.cos.policy.pollIntervalMs` value (in milliseconds) in the `ranger-cos-security.xml` file and restart COS Ranger Service. After the policy is tested, we recommend you change it back to the original value (if the time interval is too short, the polling frequency will be high, causing a high CPU utilization).
