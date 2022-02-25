[](id:access-jenkins)
### How do I access a local Jenkins instance in a custom build node?

#### Step 1: Access Jenkins

1.  First, you must set your device as a custom build node access point.
2.  To avoid exposing ports, Jenkins instances started by CODING-CI custom nodes only listen to the local loopback address (127.0.0.1) by default. The default listener port is `15740`. In this case, you can only access Jenkins from the build node machine through localhost or 127.0.0.1. The specific access address is `<http://localhost:15740>`.
3.  If you cannot access Jenkins, run the command `cat ~/.coding/cci-agent.yml` to see the port (publicPort).
4.  If you want to access Jenkins from outside the build node, run the `up` command to launch the program and add the `--jserver 0.0.0.0` parameter. At the same time, you can use `--jport` to specify the listening port. Assuming the build node IP address is `NODE_IP` and the listening port is `PORT`, the access address will be `<http://NODE_IP:PORT>`.

#### Step 2: Jenkins login token

Enter the Jenkins access address in your browser to view the login page.
![](https://qcloudimg.tencent-cloud.cn/raw/3638ac8383d9c2ddefd1799f07cf84b0.png)

Here, we assume the Jenkins username and password are `coding` and `11bf48c0403ec88231b530b5f98a113cad`. You can run the ./cci-agent up -h command.
![](https://qcloudimg.tencent-cloud.cn/raw/7e76d9fb20fd7088560cab6269b47efc.png)

[](id:install-plugin)
### How do I install plugins in custom build nodes?

Custom build nodes that use the open-source software [Jenkins](https://www.jenkins.io/zh/) as their build engines can use the over 1,000 plugins Jenkins provides for build, deployment, and automated operations. By default, CODING CI custom build nodes only have the most common Jenkins plugins. You can manually install other plugins as needed.

1.  First, sign in to Jenkins.
2.  After you sign in to Jenkins, you will see the Jenkins management interface. Go to **Manage Jenkins** > **Manage Plugins**.
3.  In the menu on the left, click **Manage Jenkins**.
![](https://qcloudimg.tencent-cloud.cn/raw/e3d8adfc2da2e1cb39c51c3eebca8bbd.png)
4.  On the page, select **Manage Plugins**.
![](https://qcloudimg.tencent-cloud.cn/raw/8958d2843a41b3c5b76c91bdaf3b5c31.png)
5.  Open the Plugin Manager page.
![](https://qcloudimg.tencent-cloud.cn/raw/ea8fb31aab77d6ba2ad945dc0b56b3f5.png)
6.  On the Plugin Manager page, find the **Available** tab, select the plugins to install, and click **Download now and install after restart** at the bottom. On the **Update Center** page that pops up, select **Restart Jenkins when installation is complete**. Wait for Jenkins to install the plugins and automatically restart. You can now use the plugins.
![](https://qcloudimg.tencent-cloud.cn/raw/72d85cff21ae7e5916f2ae014981062f.png)

[](id:quota)
### How do quotas work for custom build nodes?

-   Access custom nodes are not limited by CODING team quotas.
-   Custom build nodes are not counted towards the team's weekly build quota.
-   Custom build nodes are not limited by the team's parallel operation quota.
-   Custom build nodes are not limited by timeout quotas.

[](id:cache)

### How do caches work for custom build nodes?

A build plan configured with a custom build node pool will use the build node's own cache.
![](https://qcloudimg.tencent-cloud.cn/raw/9b25aece37b5c5316a060f882543e867.png)
For a build plan executed by custom build nodes, each execution creates an independent `WorkSpace`, which is cleared after the build is completed. Files produced outside of the workspace during the build process are retained (such as files in the global cache for maven, npm, and other artifact repositories).
![](https://qcloudimg.tencent-cloud.cn/raw/6ffa38362a50341c6b09ca7772ee033c.png)


[](id:repeat-registration)
### How do I re-register cci-agent?
Under normal conditions, if you repeatedly register cci-agent on a machine, you will be prompted that the node is already registered, and you must delete the registered node before registering it again.
![](https://qcloudimg.tencent-cloud.cn/raw/b1e9e5c167e5e7776da2e351438383ff.png)

This is because you must provide a config directory (default: `~/.config`) and a port number (default: 15740) when registering a node. To re-register a node, manually specify a non-conflicting config directory and port number.

Before performing this operation, you must have already applied for a project token password with permissions for the build node by going to **Project Settings** > **Developer Options** > **Project Token**.

In the following example, we use `~/.coding2` and `port 15741` to re-register a node.

```shell
./cci-agent init --config ~/.coding2 --pt <project token password>
```

```shell
./cci-agent up --config ~/.coding2 --jport 15741
```

[](id:abnormal-problem)
### Custom node exceptions

#### Custom node operating system: CentOS Minimal Install 

If your custom node Jenkins fails to start and the warning below is shown, it may be because the node's operating system is CentOS (Minimal Install), and the Jenkins webpage relies on some graphical components.
![](https://main.qcloudimg.com/raw/c469944d823c94ded870b29dd3e63119.png)

To solve this problem, run the following command:

```shell
yum install fontconfig
```

[](id:abnormal-state)
### Abnormal status handling

In actual production, unstable factors such as the client's network environment or a missing configuration environment can affect access to custom build nodes. The list below provides the methods used to handle abnormal statuses.

#### Deleted build node pool
<table>
<tr>
<th>Location</th>
<th>Build Record Error Prompt</th>
<th>Handling Method</th>
</tr>
<tr>
<td>Build plan configuration</td>
<td>-</td>
<td>Deleted build node pools will not appear in the build plan node pool configuration.</td>
</tr>
<tr>
<td>Configured build plan</td>
<td>The configuration page indicates that the build node pool has been deleted.</td>
<td>A build node pool configured in the build plan has been deleted.</td>
</tr>
<tr>
<td>Trigger build task</td>
<td>The build node pool my\-pool configured for this build plan has been deleted. Please reconfigure.</td>
<td>The build task can be triggered, but it will immediately fail.</td>
</tr>
<tr>
<td>In queue, initializing, preparing build, building</td>
<td>The build node pool my\-pool configured for this build plan has been deleted. Please reconfigure.</td>
<td>Build tasks in these statuses will fail immediately.</td>
</tr>
</table>


#### "In Use" build node deleted
<table>
<tr>
<th>Location</th>
<th>Build Record Error Prompt</th>
<th>Handling Method</th>
</tr>
<tr>
<td>Build tasks in queue</td>
<td>-</td>
<td>Unaffected, the build tasks in the queue have not been assigned specific build nodes and will remain in the queue until a valid build node is found.</td>
</tr>
<tr>
<td>Initializing, preparing build, building</td>
<td>Build node xxx offline</td>
<td>Build tasks in these statuses will fail immediately.</td>
</tr>
</table>


#### "In Use" build node is offline

>? The build node may be offline due to the unstable network of the client.

After going offline, the client (build node) will attempt to reconnect. The server will retry the operation after the client reconnects.
-   If the operation times out (after three minutes), the build node is judged to be offline and the build task is marked as failed. 
-   Upon successful reconnection, the client will continue to report build content.
<table>
<tr>
<th>Location</th>
<th>Build Record Error Prompt</th>
<th>Handling Method</th>
</tr>
<tr>
<td>Build tasks in queue</td>
<td>-</td>
<td>Unaffected, the build tasks in the queue have not been assigned specific build nodes and will remain in the queue until a valid build node is found.</td>
</tr>
<tr>
<td>Initializing, preparing build, building</td>
<td>Build node xxx offline</td>
<td>Build tasks in these statuses will fail immediately.</td>
</tr>
</table>


#### Configured build pool has no accessible nodes
<table>
<tr>
<th>Location</th>
<th>Build Record Error Prompt</th>
<th>Handling Method</th>
</tr>
<tr>
<td>Build plan configuration</td>
<td>-</td>
<td>Because the build plan is not directly associated with build nodes, this does not affect the build plan configuration. If there are no build nodes in the node pool, the configuration page will display the corresponding warning.</td>
</tr>
<tr>
<td>Configured build plan</td>
<td>-</td>
<td>Because the build plan is not directly associated with build nodes, this does not affect the build plan configuration. If there are no build nodes in the node pool, the configuration page will display the corresponding warning.</td>
</tr>
<tr>
<td>Initializing, preparing build, building</td>
<td>The build node pool my\-pool configured for this build plan has been deleted. Please reconfigure.</td>
<td>Build tasks in these statuses will fail immediately.</td>
</tr>
</table>


#### Build plan authorization canceled
<table>
<tr>
<th>Location</th>
<th>Build Record Error Prompt</th>
<th>Handling Method</th>
</tr>
<tr>
<td>Build plan configuration</td>
<td>The corresponding prompt is displayed.</td>
<td>Users cannot select unauthorized build plans.</td>
</tr>
<tr>
<td>Configured build plan</td>
<td>-</td>
<td>The Build Record List page and Build Configuration page will display an unauthorized prompt. You must manually adjust the node pool configuration.</td>
</tr>
<tr>
<td>Trigger build task</td>
<td>This build plan does not have authorization for the build node pool default. Please authorize it.</td>
<td>The build task can be triggered, but it will immediately fail.</td>
</tr>
<tr>
<td>Initializing, preparing build, building</td>
<td>The build node pool my\-pool configured for this build plan has been deleted. Please reconfigure.</td>
<td>Build tasks in these statuses will fail immediately.</td>
</tr>
</table>
