### How do I migrate HiveServer2 to a router node?
1. Log in to the [EMR console](https://console.cloud.tencent.com/emr), and click the specific cluster ID in the **ID/Name** column on the **Cluster List** page to go to the cluster details page. Click **Cluster Resource** > **Resource Management** to go to the resource management page. Click **Scale Out** to go to the cluster scale-out page.
![](https://main.qcloudimg.com/raw/dcebf8cd1f53dae19f5cbde68b817c99.png)
On the cluster scale-out page, select **Router** in **Node Type** and **Hive-2.3.5** in **Scale-out Service**. Configure other settings as required.
![](https://main.qcloudimg.com/raw/1591783452381d6802ffa38d9f330718.png)
2. Log in to the router node and modify the `hive-site.xml` configuration file.
 ![](https://main.qcloudimg.com/raw/0a9fdf9401f68f799db530bee95d34c0.png)
3. Disable the Hive service on the master node.
On the **Cluster Service** page, select **Operation** > **Role Management** for the Hive component, pause all the Hive processes on the master node, and restart the Hive processes on the router node.
![](https://main.qcloudimg.com/raw/0eac9d885faa61fda2a0deab90ea5712.png)
4. Conduct a test.
On the router node, check whether HiveServer2 can be properly connected to and existing tables can be queried; if yes, the migration is successful.
![](https://main.qcloudimg.com/raw/3ffae19871f972bef3ccd8796deb2e27.png)
5. Modify the Hue configuration file to route requests to the Hive component on the router node.
```
vim /usr/local/service/knox/conf/topologies/emr.xml Modify `HIVE` and `HIVEUI`.
<service>
    <role>HIVE</role>
    <url>http://Router-ip:7003</url>
    <param>
        <name>replayBufferSize</name>
        <value>8</value>
    </param>
</service>
<service>
    <role>HIVEUI</role>
    <url>http://Router-ip:7003</url>
</service>
```
Run the following commands to restart Knox:
```
su hadoop 
/usr/local/service/knox/bin/gateway.sh stop ; /usr/local/service/knox/bin/gateway.sh start
```
