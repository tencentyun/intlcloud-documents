### How do I migrate HiveServer2 to a router node?
1. Log in to the EMR Console and select **Cloud Hardware Management** on the left sidebar. Click **Add Router Node** to enter the router node adding page and choose to install the **Hive 2.1.1** component.
![](https://main.qcloudimg.com/raw/6a0e18c90a0e1ea0f5c92f117204c3ee.png)
2. Log in to the router node and modify the configuration file `hive-site.xml`.
 ![](https://main.qcloudimg.com/raw/0a9fdf9401f68f799db530bee95d34c0.png)
3. Disable the Hive service on the master node.
On the Hive role management page in component management, suspend all Hive processes on the master node and restart Hive processes on the router node.
![](https://main.qcloudimg.com/raw/86dc44afdb6234d88d84881ac1caf115.png)
4. Conduct a test.
On the router node, check whether HiveServer2 can be properly connected to and existing tables can be queried; and if yes, the migration is successful.
![](https://main.qcloudimg.com/raw/3ffae19871f972bef3ccd8796deb2e27.png)
5. Modify the Hue configuration file to route requests to the Hive component on the router node.
```
vim /usr/local/service/knox/conf/topologies/emr.xml   Modify `HIVE` and `HIVEUI`.
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
Run the following command to restart Knox.
```
su hadoop 
/usr/local/service/knox/bin/gateway.sh stop ; /usr/local/service/knox/bin/gateway.sh start
```
