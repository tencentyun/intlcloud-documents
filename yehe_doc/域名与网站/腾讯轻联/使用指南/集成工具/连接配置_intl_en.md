## Overview
The **Connection** page centrally displays the configuration information of all authorized app accounts under the current account. In the same integration app, you can add multiple connections. In the same project, you can use an applicable configuration for different integration apps. You can also quickly add and modify connections. The configuration content of used integration apps will also be updated in real time.

## Directions

### Adding a connection
#### Step 1. Configure the basic information
Log in to the [iPaaS console](https://ipaas.tencentcloud.com/login) and select **Integration tools** > **Connection**. On the **Connection** page, select the target project name and click **Create connection** to enter the connection creation page.
![](https://qcloudimg.tencent-cloud.cn/raw/afc7e307cb26a23b099a98d0f4c17164.png)

#### Step 2. Complete authorization and configuration
Enter the information as prompted and click **Next** to enter the authorization/configuration page. The information required for third-party app authorization varies by connector. Therefore, enter the information after getting the key or account password document from the third party.
![](https://qcloudimg.tencent-cloud.cn/raw/0f1a4b1dbe93d0e045513f6ab795b546.png)

#### Step 3. Test the connection
Some connections can be tested. After entering the connection configuration, you can test the connection to verify whether the connection configuration is normal. If the test succeeds, the configuration is completed and can be used normally; if the test fails, you need to check whether the entered information is correct.

### Modifying a connection
You can modify existing connections but need to note the following:
>!
>- If the connection is modified, the connector's associated integration apps will be affected.
>- To make the modification of the connection take effect, you need to restart associated integration app tasks; otherwise, running tasks will throw an exception. Restarting tasks will stop running tasks instantly.
>

### Connection group
Connection management uses groups to suit multi-environment and multi-account use cases. You can switch between groups to quickly switch to different configurations for connection. For example, in the production/test environment, you can use the configurations in group 1/2.
Group: The same connection can exist in different groups, and different groups can have different connections, so that you can switch between them quickly. The default group cannot be deleted.  

#### Step 1. Add a group
You can create multiple groups. In each group, you can configure different authorized accounts for the same connection for different business environments.
![](https://qcloudimg.tencent-cloud.cn/raw/8c9e21fa48e8d117cb952703b0c0fdb6.png)

#### Step 2. Switch between groups
When publishing an app, you can select different connection groups to quickly switch to the connection required for the environment.
![](https://qcloudimg.tencent-cloud.cn/raw/8ad590cac8b7dd1b32e60358d6ec795c.png)