
## Scenario
The component management feature enables rolling restart at the component level and component adding. With advanced management, you can perform operations at the component service and node levels such as rolling restart, pause, and maintenance.

**Definitions**
- **Restart**: The selected components and services will be restarted on a rolling basis by node.
- **Add a component**: You can use this feature to add components that were not selected when you created the cluster in the current version.
- **Pause**: The services in the selected node will be paused, which can then be resumed by using the **Start** feature.
- **Maintenance**: The process daemon will be stopped for the services on the selected node. When a process becomes exceptional for various reasons, no alarming or automatic recovery will occur. This is suitable for node debugging. You can use the **Exit Maintenance** function to resume the daemon.

## Directions
Log in to the [EMR Console](https://console.cloud.tencent.com/emr) and go to the **Component Management** page, where you can perform operations such as **Add Component**, **Rolling Restart**, and **Reset Native UI Password**. In the **Action** column of a component, click **Advanced Management** to enter the service/node-level management page of the component.
![](https://main.qcloudimg.com/raw/e84b809ad2a4382b3edfd86b7dc57d4e.png)

### Adding a Component
Existing components in the cluster are selected by default and cannot be canceled. You can only add components that are currently not installed in the cluster.
![](https://main.qcloudimg.com/raw/992b4277cf5c859f8e9dbd8bdb1230b7.png)

### Rolling Restart
This is to restart the components on all nodes in the cluster on a rolling basis. If you need to perform node/service-level operations, go to the **Advanced Management** page.
 ![](https://main.qcloudimg.com/raw/06b14f43d86610fd8ffaf1c7d492181d.png)

### Advanced Management
The **Service Status** column displays whether the current service is **running** or **paused**, and the **Maintenance Status** column displays whether the current service is under maintenance.
![](https://main.qcloudimg.com/raw/568c0002cafb3baf1077db9e8b11670c.png)
