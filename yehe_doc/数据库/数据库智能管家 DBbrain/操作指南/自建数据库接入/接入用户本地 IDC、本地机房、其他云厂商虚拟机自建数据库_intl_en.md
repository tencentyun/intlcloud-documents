This document describes how to connect other self-built databases in local IDCs or data centers or on virtual machines of other cloud vendors to DBbrain to enjoy database autonomy capabilities provided by DBbrain, such as monitoring and alarming, performance optimization, and database management.

## Access Mode
- **Agent-Based Access** (recommended): In this mode, the DBbrain agent is deployed on the database server and can automatically discover the database, and all DBbrain autonomy services can be used. This mode has the following advantages:
 - Data transfer is encrypted.
 - The agent automatically collects and stores data temporarily, so that data will not get lost even when the agent is disconnected from the server.
 - Communication between the server and the agent requires authentication, and the SQL statements sent to the agent for execution carry the verification information.
 - The server resource information and slow logs can be collected, and slow log analysis is supported.
- **Direct Access**: In this mode, there is no need to deploy the DBbrain agent; instead, you can quickly access your database by simply entering the database account and password with an active network connection. It supports part of the DBbrain autonomy services and is suitable for accessing a small number of self-built databases.

>?
>- For feature comparison between the two access modes, see the “Feature Comparison of Different Access Modes” section as described in [Overview](https://intl.cloud.tencent.com/document/product/1035/40594).
>- Other self-built databases in local IDCs or data centers or on virtual machines of other cloud vendors: MySQL.

## [Process of Agent-Based Access](id:ajrlc)
### Entering the access page
1. Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain/instance) and select **Instance Overview** on the left sidebar. On the displayed page, click **Quick Access** on the self-built instance access block to enter the self-built database instance access page.
2. In the **Other Self-Built Databases** section, click **Agent-Based Access** to proceed with the access process.

### Accessing other self-built databases
#### Step 1. Select a server
On the server selection page, add a server with a self-built database and click **Next** to deploy the agent.
- **Select Region to Deploy DBbrain Service**: Currently, the Guangzhou, Beijing, Shanghai, and Chengdu regions are supported. If your database is in another region, we recommend you select the nearest region from the above.
- **Add Server**: You can add a server through the following access modes: public IP, Direct Connect, and VPN.


#### Step 2. Deploy the agent
The agent deployment page displays the servers added in the previous step and their agent status.
1. On the agent deployment page, select a server and click **Deploy** in the **Operation** column, or select multiple servers and click **Batch Deploy** in the top-left corner of the list to deploy the agent.
>?If the agent is not deployed on a server, the agent status will be displayed as **--**.
>
2. In the pop-up window, select the agent port, click **Deploy**, and the agent deployment command will be generated based on the selected port number.
3. Copy the generated agent deployment command and run it on the server. If `Start agent successfully` is displayed, the agent is successfully deployed. Return to the deployment page, and you can see that the agent status has become **Connected**.
Descriptions of agent status and corresponding operations:
<table>
<thead><tr><th width=10%>Agent Status</th><th width=35%>Status Description</th><th width=10%>Operation</th><th width=45%>Operation description</th></tr></thead>
<tbody><tr>
<td >--</td>
<td>The agent is not deployed on the server</td>
<td>Deploy</td><td>You can click <b>Deploy</b> to deploy the agent on the server.</td></tr>
<tr>
<td rowspan=2>Deploying</td>
<td rowspan=2>The agent is being deployed on the server.</td>
<td>View</td><td>You can click <b>View</b> to view the port number and command of the agent being deployed.</td></tr>
<tr>
<td>Reset</td><td>You can click <b>Reset</b> to restore the agent status to <b>--</b> in case you want to change the agent port number and deploy the agent again.</td></tr>
<tr>
<td rowspan=3>Connected</td>
<td rowspan=3>The agent has been successfully deployed on the server and is monitoring the database and collecting information properly. The self-built database can use the autonomy services provided by DBbrain normally.</td>
<td>View</td><td>You can click <b>View</b> to view the port number and command of the deployed agent.</td></tr>
<tr>
<td>Stop</td><td>You can click <b>Stop</b> to close the active connection with the agent</td>
</tr>
<td>Reset</td><td>You can click <b>Reset</b> to restore the agent status to <b>--</b> in case you want to change the agent port number and deploy the agent again.</td></tr>
<tr>
<td rowspan=2>Connection failed</td>
<td rowspan=2>The agent failed to be deployed on the server. For more information, see <a href="https://cloud.tencent.com/document/product/1130/54288">Agent Access</a></td>
<td>View</td><td>You can click <b>View</b> to view the port number and command of the agent.</td></tr>
<tr>
<td>Reset</td><td>You can click <b>Reset</b> to restore the agent status to <b>--</b> if you want to change the agent port number and deploy the agent again.</td></tr>
<tr>
<td rowspan=3>Connection paused</td>
<td rowspan=3>The agent has been successfully deployed on the server, but data monitoring and collection is paused</td>
<td>View</td><td>You can click <b>View</b> to view the port number and command of the agent.</td></tr>
<tr>
<td>Reconnect</td><td>You can click <b>Reconnect</b> to resume the paused agent to **Connected** status.</td></tr>
<tr>
<td>Reset</td><td>You can click <b>Reset</b> to restore the agent status to <b>--</b> in case you want to change the agent port number and deploy the agent again.</td></tr>
</tbody></table>

4. When there is at least one agent in **Connected** status, click **Next** to add a database.


#### Step 3. Add a database
The database instance adding page displays the servers with the agent successfully deployed in the previous step and their database status.
1. On the database instance adding page, select a database type.
2. Select a server and click **Add** in the **Operation** column, or select multiple servers and click **Batch Add Databases** in the top-left corner of the list to add the databases.
>?If a server with the agent successfully deployed has no database on it, the database status will displayed as **--**.
>
3. In the pop-up window, enter the port number, account, password, and configuration of the database, and click **OK**.
>?If database account authorization failed, troubleshoot as instructed in [Database Account Authorization Exceptions](https://intl.cloud.tencent.com/document/product/1035/40662).
> 
The database account configuration is as detailed below:
<table>
<thead><tr><th >Parameter</th><th >Description</th></tr></thead>
<tbody><tr>
<td>Port</td><td>It is the database port number detected by the DBbrain agent (if there are multiple self-built databases on the server, you can click <b>Add Port</b> to manually enter database port numbers to access such databases at the same time).</td></tr>
<tr>
<td >Account</td><td>It is the account of the self-built database (if no account has been created, you need to click <b>Generate Authorization Command</b>, copy the generated command, and run it on the database).</td></tr>
<tr>
<td >Password</td><td>It is the password of the self-built database.</td></tr>
<tr>
<td >Database Configuration</td><td>It is the configuration assigned by the server to the self-built database, including number of CPU cores, memory size, and disk size. DBbrain will configure the computing performance based on the entered values.</td></tr>
</tbody></table>
The database account authorization is as detailed below:
<table>
<thead><tr><th >Permission</th><th >Description</th></tr></thead>
<tbody><tr>
<td>PROCESS</td><td>Permission to view all connection processes, which is used to display processes during a real-time session.</td></tr>
<tr>
<td>REPLICATION SLAVE and REPLICATION CLIENT</td><td>Permissions to view the status of the primary/secondary databases and the `relaylog` and `binlog` events of the secondary database, which are used to diagnose primary/secondary replication exceptions.</td></tr>
<tr>
<td>SHOW DATABASES, SHOW VIEW, RELOAD, and SELECT</td><td>Permissions to read and refresh databases and tables</td></tr>
</tbody></table>
4. Return to the database instance adding page and click **Complete**. The database in **Connected** status can successfully access the DBbrain service.
5. Return to the [DBbrain console](https://console.cloud.tencent.com/dbbrain/instance), enter the instance management page, select the self-built database type at the top, and you can view and manage the accessed self-built database.


## [Process of Direct Access](id:zljrlc)
### Entering access page
1. Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain/instance) and select **Instance Overview** on the left sidebar. On the displayed page, click **Quick Access** on the self-built instance access block to enter the self-built database instance access page.
2. In the **Other Self-Built Databases** section, click **Direct Access** to proceed with the access process.

### Accessing other self-built databases
#### Step 1. Select a server
On the server selection page, add a server with a self-built database and click **Next** to deploy the agent.
- **Select Region to Deploy DBbrain Service**: Currently, the Guangzhou, Beijing, Shanghai, and Chengdu regions are supported. If your database is in another region, we recommend you select the nearest region from the above.
- **Add Server**: You can add a server through the following access modes: public IP, Direct Connect, and VPN.

#### Step 2. Add a database
The database instance adding page displays the servers selected in the previous step and their database status.
1. On the database instance adding page, select a database type.
2. Select a server and click **Add** in the **Operation** column, or select multiple servers and click **Batch Add Databases** in the top-left corner of the list to add the databases.
>?If a server with the agent successfully deployed has no database on it, the database status will displayed as **--**.
>
3. In the pop-up window, enter the port number, account, password, and configuration of the database, and click **OK**.
>?If database account authorization failed, troubleshoot as instructed in [Database Account Authorization Exceptions](https://intl.cloud.tencent.com/document/product/1035/40662).
> 
The database account configuration is as detailed below:
<table>
<thead><tr><th >Parameter</th><th >Description</th></tr></thead>
<tbody><tr>
<td>Port</td><td>It is the database port number detected by the DBbrain agent (if there are multiple self-built databases on the server, you can click <b>Add Port</b> to manually enter database port numbers to access such databases at the same time).</td></tr>
<tr>
<td >Account</td><td>It is the account of the self-built database (if no account has been created, you need to click <b>Generate Authorization Command</b>, copy the generated command, and run it on the database).</td></tr>
<tr>
<td >Password</td><td>It is the password of the self-built database.</td></tr>
<tr>
<td >Database Configuration</td><td>It is the configuration assigned by the server to the self-built database, including number of CPU cores, memory size, and disk size. DBbrain will configure the computing performance based on the entered values.</td></tr>
</tbody></table>
The database account authorization is as detailed below:
<table>
<thead><tr><th >Permission</th><th >Description</th></tr></thead>
<tbody><tr>
<td>PROCESS</td><td>Permission to view all connection processes, which is used to display processes during a real-time session.</td></tr>
<tr>
<td>REPLICATION SLAVE and REPLICATION CLIENT</td><td>Permissions to view the status of the primary/secondary databases and the `relaylog` and `binlog` events of the secondary database, which are used to diagnose primary/secondary replication exceptions.</td></tr>
<tr>
<td>SHOW DATABASES, SHOW VIEW, RELOAD, and SELECT</td><td>Permissions to read and refresh databases and tables</td></tr>
</tbody></table>
4. Return to the database instance adding page and click **Complete**. The database in **Connected** status can successfully access the DBbrain service.
5. Return to the [DBbrain console](https://console.cloud.tencent.com/dbbrain/instance), enter the instance management page, select the self-built database type at the top, and you can view and manage the accessed self-built database.

