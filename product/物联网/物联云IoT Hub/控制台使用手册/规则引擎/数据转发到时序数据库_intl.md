[//]: # (chinagitpath:XXXXX)

### Overview
The rule engine allows you to configure rules to forward eligible device-reported data to the TimeSeries database (CTSDB). Then your application server can read the data in CTSDB for processing. CTSDB's strong capacities in data storage, compression, collection and display are leveraged, meeting needs for data storage, analytics and visualization on a daily basis.
The figure below shows the entire process of forwarding data to CTSDB by the rule engine:
![avatar](https://main.qcloudimg.com/raw/2dba1bf793dcac62625ae498c1d812b2.png)

### Configuration
Log in to the [Rule Engine](https://console.cloud.tencent.com/iotcloud/rules/rule) console page and click the rule you want to configure.
![](https://main.qcloudimg.com/raw/b8998fc9ad37238c7f1779e4013b0f3c.png)
On the rule details page, click the **Add Action** button. In the pop-up "Add action" window, select the action **Data forwarding to CTSDB**, then select the CTSDB region and instance, enter the basic information and the forwarding fields to be configured and click **Create**.
![avatar](https://main.qcloudimg.com/raw/218e38a4a5593b3ce00b65578f6069e7.png) 
**Note:** You need to authorize CTSDB access if you are using it for the first time. You need to click **Authorize access to CTSDB** to proceed.
![avatar](https://main.qcloudimg.com/raw/6a5e269611263559edcceb671e81fef3.png) 
After the configuration above is completed, the IoT Hub platform will forward the data reported by the device that meets the rule conditions to the CTSDB instance configured; you can see CTSDB Development Guide for more information about how to read data on your own application server for processing or aggregate, search for and query the data in the [CTSDB Console](https://console.cloud.tencent.com/ctsdb).

### Configuration Parameter Descriptions
- Instance login account: This is the account name entered when you create the CTSDB instance before configuring the rule engine.
- Login password: This is the account password entered when you create the CTSDB instance before configuring the rule engine.
- metric: This is to configure to which CTSDB metric to forward the data. If the metric is not present when the rule engine is configured, the IoT Hub platform will create it automatically.
- timestamp: This is the timestamp when the data is written to CTSDB. Currently, 4 types of configurations are supported: the field value of the original message referenced through ${}; the system function timestamp(), i.e., the current system time of the message hitting the rule engine; a constant, which needs to be a Unix timestamp in seconds; if left blank, the current time of the message hitting the rule engine will be used by default.
- Data field: For the type, you can select tag type or field type in CTSDB; for the restriction on field name, see the CTSDB restrictions; the value has 3 configuration methods: the field value of the original message referenced through ${}; system function (see rule engine function list); a constant with a fixed value.

### Advanced Configuration
The advanced configuration items are suitable for scenarios where the device-reported data fields are dynamically expanding and cannot be pre-configured. Suppose there are multiple device sensors to transfer data, and their specifications and configurations are different. The number of sensors are not fixed. Advanced configuration needs to be deployed to store all the device sensors’ data into CTSDB. Here comes the advanced configuration:
![](https://main.qcloudimg.com/raw/d4c61aab9ca6f2461bff3d516c05428a.png)
**Notes:**
- Default storage type: The default storage type of dynamically expanding storage fields is tag in CTSDB.
- key: This is the JSON key that needs to traverse the expanding storage. The IoT Hub platform will traverse the JSON key value nesting under this key with '_' as the connector and finally store the data in CTSDB. The JSON results and configuration retrieved by the SQL SELECT of the rule engine (multiple sub-keys can be configured) transform to the data stored in the CTSDB as shown in the example below:
![](https://main.qcloudimg.com/raw/c3bfb94a9d82abdebdf36d392a1a4151.png)


