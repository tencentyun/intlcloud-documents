
## Overview

After entering an integration app, you can create multiple flows to implement your business logic. The flow canvas reserves a trigger component position for you to place a logical component or connector with trigger capabilities such as HTTP Listener, Kafka connector, and Scheduler. Flows with trigger capabilities are main flows, while those without trigger capabilities can only be referenced as subflows by other flows through the [Flow Reference](https://www.tencentcloud.com/document/product/1165/51620) logical component.  


## Flow

In iPaaS, you can create a folder to aggregate relevant flows for hierarchical flow management. Within the same integration app, you can create and copy folders and flows for subsequent development and maintenance.

### Creating a flow

You can create, copy, share, rename, and delete flows.
![](https://qcloudimg.tencent-cloud.cn/raw/7e0efc1bc6563ffe098d393e1e92fdbb.png)

### Copying a flow
You can copy flows within the same integration app. Click **Copy**, and the system will automatically create a flow named **XXX_copy**.
![](https://qcloudimg.tencent-cloud.cn/raw/506fc5bb40cd9cb26edd02d5e0f05917.png)
The **Batch copy** operation is also supported.
![](https://qcloudimg.tencent-cloud.cn/raw/583f4ea2a9dc47cc64b9b4145e6d974b.png)
Click **Batch copy**, select all, a single, or multiple consecutive nodes (as with a unit test), and click **Copy** to batch copy the nodes.
If no nodes are selected, the **Copy** button is grayed out. It will be clickable after you select one or more nodes.
After clicking **Copy**, you can paste the content into other flows within the same project.
![](https://qcloudimg.tencent-cloud.cn/raw/e5ea9194464162eaff564e23ada7256a.png)

### Sharing a flow

A shared flow can be referenced across integration apps within the same project through the [Flow Reference](https://www.tencentcloud.com/document/product/1165/51620) component.
![](https://qcloudimg.tencent-cloud.cn/raw/6beef3ecaf89e3b265e611205503a8b0.png)
Select the Flow Reference component.
![](https://qcloudimg.tencent-cloud.cn/raw/4e910cb5382f7d1e7d56294af36ce796.png)

### Deleting a flow

When a flow is deleted, all its configurations are cleared and cannot be recovered. Therefore, please exercise caution when deleting a flow.
![](https://qcloudimg.tencent-cloud.cn/raw/844b64570d90bcbb730d338f02aa3cf6.png)

### Folder

A folder can be used to aggregate relevant flows. You can create, copy, and add flows to folders for flow management and maintenance.
![](https://qcloudimg.tencent-cloud.cn/raw/6363ba2cab1190814201470669b5017d.png)
You can drag and drop existing flows to adjust their order or drag and drop them to a folder for unified management. When dragging a flow, you can drop it after a blue line appears.
![](https://qcloudimg.tencent-cloud.cn/raw/87a632fcda08954f315d15092d2bb56c.png)

## Component Library

After a flow is created, it will be displayed on the canvas. Click **+** on the canvas to open the component library, select a component, and configure the flow. Components include connectors and logical components, the former of which include common connectors and app connectors.

- Common connector: Protocol for app system interaction.
- App connector: Encapsulation of an app. For example, if a system interacts with other systems over HTTP, you can select the HTTP connector and configure the parameters for connection; if you want to connect to Tencent Meeting, you can directly use the Tencent Meeting connector, which encapsulates the APIs, authentication information, and interaction protocols of Tencent Meeting.
- Logical component: Implementation of business logic for app interconnection, such as loop, choice, variable configuration, data conversion, parallel processing, and async processing.
  ![](https://qcloudimg.tencent-cloud.cn/raw/0ef51e79885d7e42c58c16f773f11c7c.png)

### Logical component operation guide
1. For a newly created flow, click **+** to select a trigger component.
![](https://qcloudimg.tencent-cloud.cn/raw/9374cd9759ca65011a168a2d6badb3b3.png)
2. When you add a sub-node, the information of the parent node will be displayed.
![](https://qcloudimg.tencent-cloud.cn/raw/eb7bad5ee20eef6a637ebb57a51970ea.png)
3. If you add a logical component, the component configuration page will be directly displayed. Then, configure the component as prompted.
![](https://qcloudimg.tencent-cloud.cn/raw/2854565bf916f73ea02de400199c4cb9.png)

### Common/App connector operation guide

For a newly created flow, click **+** to select a trigger component. If you select an app connector or common connector, select the required operation first and then [configure the app connector](#layout) or [common connector](#1) as prompted. General configuration items are required, while advanced configuration items are optional. After completing the configuration, click **Execute** in the **Preview** step to check whether the configuration is correct and whether the output data is as expected and can be used on the next node. You can **click the data to input it**.
![](https://qcloudimg.tencent-cloud.cn/raw/37447a48d59830b1c4414cc0ef79b1df.png)

[](id:layout)

#### Connection

- Create a connection: After you select **Connector** and create a connector on the canvas, the message "No connections are bound yet. Select an existing connection or create one" will be displayed in the top-left corner of the pop-up configuration page. Click **Add connection** and configure the information as prompted.
  ![](https://qcloudimg.tencent-cloud.cn/raw/cfa063c0e267c70254e4fbb4d5495f07.png)
- Select an existing connection: For a non-newly created integration app, if there are existing connections in the same app, you can select one as needed. To modify the third-party credential information, you can return to the **Connection** page to create a connection or switch to another existing one.
  ![](https://qcloudimg.tencent-cloud.cn/raw/51bfef179c386b9a53702aec90820ebb.png)
- Connection: When a connector is created, its connections will be displayed on its **Connection** page. You can click **Edit** to enter the connection page and edit the connection information.
  ![](https://qcloudimg.tencent-cloud.cn/raw/84e90ddeab0578218bdf065bc90922bc.png)
- Switch the app connector version: If the selected app connector has multiple versions, you can click **Tools** in the top-right corner and click **Connector version** to switch to the target version.
> ?If there is a red exclamation mark after the selected version, the version is not the latest one.
> 
[](id:1)
- Common connector configuration
>?Common configurations are displayed only for apps created after the launch of the standalone console.
>Reason: Connection configurations of common connectors (like HTTP Request) of apps created before the launch of the standalone console are called common configurations. Configurations of both common connectors and app connectors of apps created after the launch of the standalone console are collectively called connection configurations; therefore, common configurations are no longer displayed.
>
 - Edit a common connector configuration: Select the target common connector, click **Tools** in the top-right corner, select **Connection**, and click the name of the target configuration to edit the configuration.

 - Delete a common connector configuration: Select the target common connector, click **Tools** in the top-right corner, select **Connection**, and click ![](https://qcloudimg.tencent-cloud.cn/raw/4def1a29337302a82d29669232eaa184.png) to delete the target configuration.


### Online preview

After configuring a node, you can view the node's output data and schema immediately in the preview step.
![](https://qcloudimg.tencent-cloud.cn/raw/6b5e0561454c4f35f018ca5b539c7dbe.png)

### Flow data panel

After you click a flow node, the flow data panel will be displayed. You can select the data content on the previous nodes to reference data variables easily. If multiple variables are selected, they will be spliced automatically.
![](https://qcloudimg.tencent-cloud.cn/raw/2010b4f6d2cda025fc7740dc17b61573.png)

### Single-line expression input

If you want to simply edit some variables when entering parameters, you don't need to open the code input box. Instead, you can switch to the **Expression** input mode to perform over 100 quick operations for orchestration, such as type conversion, operator, method reference, and attribute reference. The input process is further simplified through capabilities such as smart prompt and autocomplete.

## Multi-User Collaboration Mode

iPaaS supports **multi-user collaboration**. This feature allows multiple members in your team to develop the same integration app at the same time. In addition, you can enable the editing lock to avoid version inconsistency caused by simultaneous editing of the app by multiple users.

>!In multi-user development, multiple users can develop multiple flows together in the same integration app, but a single flow can be edited by only one user at a time and is locked (uneditable) for other users during editing. This helps avoid version inconsistency caused by simultaneous editing of the app by multiple users.
>
![](https://qcloudimg.tencent-cloud.cn/raw/53c8f043245f8c3eb0775116ca5a0d1a.png)
## Testing Feature

### Integration app test

#### Viewing test information and errors

During integration app test, you can publish an integration app to the sandbox environment, directly copy the URL after the trigger, and simulate a trigger operation to debug the entire app. After the operation, the operation result will be displayed on the canvas. You can click the name of each component to view the detailed input and output information. All errors are displayed at the top of the page, and you can click **View** to view the error details of each component.

#### Viewing historical test records

Click the **Test history** drop-down list to view the test snapshot at each time point. In each snapshot, you can view the specific test parameters and errors at the corresponding time point. The last 10 test records are displayed to help you check the errors reported during each test.
![](https://qcloudimg.tencent-cloud.cn/raw/eea61c03d92dac2e503da39c3e64ffe1.png)

#### Viewing trigger conditions

You can view all trigger conditions of the current integration app and manually trigger the app. The following example shows how to manually trigger the Webhook component:
![](https://qcloudimg.tencent-cloud.cn/raw/e2c7cc3db98d193e12edf2efa71ab54d.png)

### Unit test

In unit test, you can partially test one or multiple consecutive components. If the flow is complex, it may take a long time to test the entire app. In this case, you can perform partial testing to quickly locate possibly abnormal components (the first trigger component of the flow cannot be selected). To perform unit testing, click **Unit test** in the top-right corner and select the components to be tested. You can select only the first and last target components, and the nodes between them will be selected automatically, eliminating the need to click nodes one by one.
![](https://qcloudimg.tencent-cloud.cn/raw/99e188bbec36c231549e45003027dfd6.png)
After you select the nodes for unit test, you need to simulate the input data for test. If you have performed unit or app test or previewed the component data before, the platform will automatically pull the historical test data, and you can select different historical data or automatically construct input data for test. If there is no historical data, you need to manually enter the simulated data for test.

[](id:2)

### Minimizing the test window

The test feature in the standalone console manipulates a certain version of the current app. You can still configure the app after minimizing the test window.

- In app test, you can click **Minimize** to minimize the app test window.
- In unit test, after you click **Close**, the unit test window will be minimized automatically.

> !As the configured version and the tested version are separate, we recommend you test the app again after configuring it to verify the availability of the latest configured version.
>
You can also click the minimized test window to restore it and view the test details.

### Viewing test records

After [minimizing the test window](#2), click **Test record** to view the historical app or unit test records.

## Search
You can search for flows, components/connectors, and configuration content, so as to quickly confirm the valid content and built-in fields in the app.
Click **Search** and enter a keyword. Here, keyword `webhook` is used as an example.
![](https://qcloudimg.tencent-cloud.cn/raw/cca8b41a8cfd7b3ea1b2e45c2c08a0aa.png)

## Tools
The toolbar provides many features such as [connection group switch](https://www.tencentcloud.com/document/product/1165/51644#.E8.BF.9E.E6.8E.A5.E9.85.8D.E7.BD.AE.E5.88.86.E7.BB.84), connector version switch, and custom script configuration.

>?Common configurations are displayed only for apps created after the launch of the standalone console.
>Reason: Connection configurations of common connectors (like HTTP Request) of apps created before the launch of the standalone console are called common configurations. Configurations of both common connectors and app connectors of apps created after the launch of the standalone console are collectively called connection configurations; therefore, common configurations are no longer displayed.
>
![](https://qcloudimg.tencent-cloud.cn/raw/6172e09edd0c7ed09d69d4fee3c641ff.png)

### Switching connection groups
You can switch between [connection groups](https://www.tencentcloud.com/document/product/1165/51644#.E8.BF.9E.E6.8E.A5.E9.85.8D.E7.BD.AE.E5.88.86.E7.BB.84) on the toolbar for preview and testing.

### Switching connector versions
Switch the app connector version: If the selected app connector has multiple versions, you can click **Tools** in the top-right corner and click **Connector version** to switch to the target version.
>?If there is a red exclamation mark after the selected version, the version is not the latest one.
>

[](id:1)
### Custom script
iPaaS offers the custom Dataway script feature, which enables you to write custom functions and components. Custom scripts can be referenced only in the integration app where they are created. They cannot be referenced across projects or integration apps.

#### Adding/Deleting a custom script

Click **Tools** in the top-right corner and click **+** next to **Custom script** to add a custom script. Click a custom script name to view or modify the script. Click ![](https://qcloudimg.tencent-cloud.cn/raw/972522315f12a4e7072e5fdaa846a8cb.png) to delete a script.

>!Once a script is deleted, apps bound to it will throw an exception. Therefore, please exercise caution when deleting a script.
> 
![](https://qcloudimg.tencent-cloud.cn/raw/a64c45c8ea1f20f690aa5acd1ef4e918.png)

#### Referencing a custom script

After you select a component and click a Dataway expression for configuration, click ![](https://qcloudimg.tencent-cloud.cn/raw/be6abf09b4b4a3f2e15dfc1c17133138.png) in the top-right corner or **Click to bind** to reference an existing custom script.
![](https://qcloudimg.tencent-cloud.cn/raw/6b9d286dd3b4b5b98f60402b76b20539.png) 

## Publishing

After you have configured an integration app, you can publish it in one or multiple regions.	
![](https://qcloudimg.tencent-cloud.cn/raw/2e00eb298a210fbe963bfa7e4c0a2a86.png)

## Versioning

Each integration app has a version number. After it is published, an integration app cannot be modified while it is running. In this case, you can copy the integration app to modify and debug a new version, which will not affect the version that is currently running.
>?The **Publishing environment** field is added for apps created after September 20, 2022. When you publish an app again, the publishing environment selected last time is retained for easier management.
>
![](https://qcloudimg.tencent-cloud.cn/raw/04b882ca1225587bd00a1c4cbd14e1d4.png)

