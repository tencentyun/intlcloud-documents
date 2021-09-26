## Background

After you adopt storage-compute separation, you will host your data on CHDFS. CHDFS provides a permission system similar to that of native HDFS. In addition to HDFS permissions, Hadoop Ranger implements more refined permission control, including user group permission settings and permission settings for specific prefixes. Plus, as a one-stop permission system solution, Hadoop Ranger supports permission control for not only storage services but also components such as YARN and Hive. Therefore, to suit your use habits, we provide a CHDFS-Ranger connection solution to make it easy for you to control the permissions of CHDFS with Ranger.


## Strengths

- Fine-grained permission control, which suits the use habits with Hadoop permissions.
- Support for unified management of big data component and cloud-hosted storage permissions.

## Solution Architecture

![](https://main.qcloudimg.com/raw/ccbe75fb92788fce02b02cf0ce63de1c.png)

In the Hadoop permission system, authentication is provided by Kerberos and authorized by Ranger. In addition to this, we provide the following components to support the Ranger permission scheme for CHDFS.

- CHDFS-Ranger-Plugin: it provides a service definition plugin on the Ranger server and description of the CHDFS service on the Ranger side. After this plugin is deployed, you can enter the corresponding permission policy on the Ranger control page.
- COSRangerService: it integrates the Ranger client, periodically syncs permission policies from the Ranger server, and verifies the permission locally after receiving an authentication request. In addition, it also provides `DelegationToken` generation and renewal APIs in Hadoop, all of which are defined through Hadoop IPC.
- CosRangerClient: it is dynamically loaded by the COSN plugin to forward permission verification requests to `CosRangerService`.

## Environment Deployment

- Hadoop environment
- ZooKeeper, Ranger, and Kerberos (if there are authentication requirements)

>? As the above services are mature open-source components, you can install them on your own.
>

## Component Deployment

<dx-tabs>
::: Deploy\sCHDFS-Ranger-Plugin
`CHDFS-Ranger-Plugin` extends the service types in the Ranger Admin console. You can set the operation permissions related to CHDFS in the Ranger console.

#### Code address

You can get the code from the `ranger-plugin` directory at [GitHub](https://github.com/tencentyun/cos-ranger-service).

#### Version

v1.2 or above

#### Deployment steps

1. Create a `COS` directory in the service definition directory of Ranger (note: make sure that the directory permissions include at least `x` and `r` permissions).
 1. For an EMR environment, the path is `ranger/ews/webapp/WEB-INF/classes/ranger-plugins`.
 2. For a self-built Hadoop environment, you can find the components connected to the Ranger service through `find hdfs` in the `ranger` directory in order to find the location of the `ranger-plugins` directory.
![](https://main.qcloudimg.com/raw/679f61339b8c3864a84b3b757dd84815.png)
2. Place `cos-chdfs-ranger-plugin-xxx.jar` in the CHDFS directory (note: the JAR package should at least have the `r` permission).
3. Restart Ranger.
4. Register the CHDFS service on Ranger. You can refer to the following command:
<dx-codeblock>
::: plaintext
## To generate a service, you need to pass in the password of the Ranger admin account and the address of the Ranger service.
## For an EMR cluster, the admin user is `root`, and the password is the root password set when the EMR cluster is created. Replace the IP of the Ranger service with the master node IP of EMR.
adminUser=root
adminPasswd=xxxxxx
rangerServerAddr=10.0.0.1:6080
curl -v -u${adminUser}:${adminPasswd} -X POST -H "Accept:application/json" -H "Content-Type:application/json" -d @./chdfs-ranger.json http://${rangerServerAddr}/service/plugins/definitions
## To delete the service just defined, you need to pass in the service ID returned during creation.
serviceId=102
curl -v -u${adminUser}:${adminPasswd} -X DELETE -H "Accept:application/json" -H "Content-Type:application/json" http://${rangerServerAddr}/service/plugins/definitions/${serviceId}
:::
</dx-codeblock>
5. After the service is successfully created, you can see the CHDFS service in the Ranger console as shown below:
![](https://main.qcloudimg.com/raw/163aac38c68931f51ab34c221ea3cef1.png)
6. Click **+** next to the CHDFS service to define a new service instance. The service instance name is customizable; for example, you can enter `chdfs` or `chdfs_test`. The service configuration is as shown below:
![](https://main.qcloudimg.com/raw/255869b8c485a93427585d21476ec001.png)
You need to set the username subsequently used to start the `COSRangerService` service for `policy.grantrevoke.auth.users`. We generally recommend you set it to `hadoop`.
7. Click the generated CHDFS service instance to add a policy as shown below:
![](https://main.qcloudimg.com/raw/f0d76ecf787eec3340f7d923e65b9b48.png)
8. On the displayed page, configure the following parameters as detailed below:
![](https://main.qcloudimg.com/raw/317e1b5cb39abae6904552cb1ebade58.png)
 - **MountPoint**: mount point name in the format of `f4mxxxxxx-yyyy`. You can log in to the [CHDFS console](https://console.cloud.tencent.com/chdfs/filesystem) to view it.
 - **Path**: path of CHDFS, which must start with `/`.
    - include: indicates whether the set permission applies to the specified path itself or other paths except it.
    - recursive: indicates that the permission applies to not only the specified path but also the subpaths under it (i.e., recursive subpaths). It is usually used when the path is set as a directory.
 - **Select Group/Select User**: username and user group in logical OR relationship; that is, the operation is authorized as long as the username or user group condition is met.
 - **Permissions**:
    - Read: read operation, which corresponds to the GET and HEAD operations in COS, such as downloading objects and querying object metadata.
    - Write: write operation, which corresponds to the PUT operation in COS, such as uploading objects.
    - Delete: delete operation, which corresponds to the object deletion operation in COS. To rename a path in Hadoop, you need to have the deletion permission for the original path and write permission for the new path.
    - List: traversal permission, which corresponds to the `List Object` operation in COS.

:::
::: Deploy\sCOSRangerService
COSRangerService is the core of the entire permission system. It is responsible for integrating the Ranger client and receiving its authentication requests, token generation and renewal requests, and temporary key generation requests. It is also where sensitive information (Tencent Cloud key information) resides. Generally, it is deployed on a bastion host, and only the cluster admin is allowed to manipulate it and view its configuration.

COSRangerService supports one-primary-multiple-secondary HA deployment. The `DelegationToken` status is persistently stored in HDFS. The leader role is determined by ZooKeeper lock grabbing. The service that gets the leader role will write its address to ZooKeeper, so that COSRangerClient can perform address routing.

#### Code address

You can get the code from the `cos-ranger-server` directory at [GitHub](https://github.com/tencentyun/cos-ranger-service).

#### Version

v1.2 or above

#### Deployment steps

1. Copy the code of COSRangerService to the servers in the cluster. We recommend you configure at least two servers (one primary server and one secondary server) in the production environment. As sensitive information is involved, we recommend you use bastion hosts or servers with tight permission control.
2. Modify the relevant configuration items in the `cos-ranger.xml` file. Those that must be modified are as follows. For the description of the configuration items, please see the comments in the file.
 -  qcloud.object.storage.rpc.address
 -  qcloud.object.storage.status.port
 -  qcloud.object.storage.enable.chdfs.ranger
 -  qcloud.object.storage.zk.address
3. Modify the relevant configuration items in the `ranger-chdfs-security.xml` file. Those that must be modified are as follows. For the description of the configuration items, please see the comments in the file.
 -  ranger.plugin.chdfs.policy.cache.dir
 -  ranger.plugin.chdfs.policy.rest.url
 -  ranger.plugin.chdfs.service.name
4. Modify the `hadoop_conf_path` and `java.library.path` configuration items in `start_rpc_server.sh`, which point to the directory of the Hadoop configuration file (such as `core-site.xml` and `hdfs-site.xml`) and the `hadoop native lib` path, respectively.
5. Run the following command to start the service.
```
chmod +x start_rpc_server.sh
nohup ./start_rpc_server.sh &> nohup.txt &
```
6. If the start fails, check whether the error log contains an error message.
7. COSRangerService supports displaying the HTTP port status (the port name is `qcloud.object.storage.status.port`, which is 9998 by default). You can run the following command to get the status information (such as whether the leader is contained and the authentication statistics).
```
# Replace `10.xx.xx.xxx` below with the IP of the server where the Ranger service is deployed
# Replace 9998 with the value of `qcloud.object.storage.status.port`
curl -v http://10.xx.xx.xxx:9998/status
```

:::
::: Deploy\sCOSRangerClient
COSRangerClient is dynamically loaded by the Hadoop CHDFS plugin and proxies all COSRangerService access requests, such as token acquisition and authentication.

#### Code address

You can get the code from the `cos-ranger-client` directory at [GitHub](https://github.com/tencentyun/cos-ranger-service).

#### Version

v1.0 or above

#### Deployment method
1. Copy the `cos-ranger-client` JAR package to the same directory as the CHDFS plugin (please choose to copy the JAR package consistent with the major version of your Hadoop).
2. Add the following configuration items in `core-site.xml`:
<dx-codeblock>
::: xml
```
<configuration>
           <!--*****Required********-->
           <!-- ZooKeeper address. The client finds the address of the Ranger service by ZooKeeper query -->
           <property>
               <name>qcloud.object.storage.zk.address</name>
               <value>10.0.0.8:2121</value>
           </property>

           <!--***Optional****-->           
           <!-- Set the Kerberos credentials used by the COSRangerService. Please refer to the configuration of the COSRangerService, which must be consistent. If there are no authentication needs, you can skip this configuration -->
           <property>                
					 <name>qcloud.object.storage.kerberos.principal</name>
					 <value>hadoop/_HOST@EMR-XXXX</value>
           </property>

         <!--***Optional****-->  
         <!-- Ranger server IP path recorded on ZooKeeper. The default value is used here. The configuration must be consistent with that of COSRangerService -->
          <property>              
					<name>qcloud.object.storage.zk.leader.ip.path</name> 
					<value>/ranger_qcloud_object_storage_leader_ip</value>
          </property>
</configuration>
```
:::
</dx-codeblock>
:::
::: Deploy\sCHDFS

#### Version

v2.1 or above

#### Deployment method

For the method of deploying the CHDFS plugin, please see [Mounting CHDFS Instance](https://intl.cloud.tencent.com/document/product/1106/41965). Open Ranger and adding the following:


<dx-codeblock>
::: plaintext 
```
    <property>
        <name>fs.ofs.ranger.enable.flag</name> 
        <value>true</value>
    </property>
```
:::
</dx-codeblock>
:::
</dx-tabs>


## Verification

1. Use `hadoop cmd` to perform operations related to accessing CHDFS as shown below:
```plaintext
# Replace the mount point, path, and other parameters with your actual information.
hadoop fs -ls ofs://f4mxxxxyyyy-zzzz.chdfs.ap-guangzhou.myqcloud.com/doc
hadoop fs -put ./xxx.txt ofs://f4mxxxxyyyy-zzzz.chdfs.ap-guangzhou.myqcloud.com/doc/
hadoop fs -get ofs://f4mxxxxyyyy-zzzz.chdfs.ap-guangzhou.myqcloud.com/exampleobject.txt
hadoop fs -rm ofs://f4mxxxxyyyy-zzzz.chdfs.ap-guangzhou.myqcloud.com/exampleobject.txt
```
2. Use an MR job to verify. Relevant services such as YARN and Hive must be restarted before verification.


## FAQs

#### Do I have to install Kerberos?

If users in the cluster are trustworthy, such as in a cluster that is only used internally, you can install Kerberos to support authentication. If the users only perform authentication operations, in order to avoid maloperations by unauthorized clients, you can choose not to install Kerberos and only use Ranger for authentication.
Installing Kerberos will incur some performance loss. Please consider your own security and performance requirements. If authentication is required, after enabling Kerberos, you need to set the related configuration items of COSRangerService and COSRangerClient.

#### If Ranger is enabled, but no policy is configured, or no policy is matched, what will happen?

If no policy is matched, the operation will be denied by default.

#### After Ranger is enabled, will CHDFS still perform POSIX authentication?

Ranger authentication is performed in the client environment. Requests authenticated by Ranger will be sent to the CHDFS server, which will perform POSIX authentication by default. Therefore, if the permissions are controlled by Ranger, please disable the POSIX permission in the CHDFS console.
