
## Overview
The rule engine allows you to configure rules to forward eligible data reported by devices to [CTSDB](https://intl.cloud.tencent.com/product/ctsdb), and then your application server can read the data from CTSDB for processing. This takes advantage of CTSDB's high storage compression rate and aggregate display for massive amounts of data, effectively meeting the daily needs of devices for data storage, analysis, and visual display.  

The figure below shows the entire process of forwarding data to CTSDB by the rule engine:
![](https://main.qcloudimg.com/raw/92cc367db0e8109fbf380e708517fa02.png)

## Configuration
1. Log in to the [IoT Hub console](https://console.cloud.tencent.com/iotcloud) and select **Rule Engine** on the left sidebar.
2. On the rule details page, click **Add Action**.
>?You will be prompted to authorize access to CTSDB upon the first use. You need to click **Authorize Now** before you can proceed.
![avatar](https://main.qcloudimg.com/raw/ba935a001132582dfa25d3df4978bfd8.png) 
3. In the pop-up **Add Action** window, select **Forward data to TencentDB for CTSDB**, select the CTSDB region and instance, enter the basic information and the fields to be forwarded, and click **Save**.
![avatar](https://main.qcloudimg.com/raw/691bd051f99388ad6eee93dacdfaf774.png) 


After the above configuration is completed, IoT Hub will forward eligible data reported by devices to the configured CTSDB instance. You can refer to [Overview](https://intl.cloud.tencent.com/document/product/1100/40910) to read the data on your own application server for processing or aggregate, search for, and query the data in the [CTSDB console](https://console.cloud.tencent.com/ctsdb).

## Configuration Parameter Description
- **Instance Account**: this is the account name entered when you create the CTSDB instance before configuring the rule engine.
- **Password**: this is the account password entered when you create the CTSDB instance before configuring the rule engine.
- **Metric**: this configures to which CTSDB metric to forward the data. If the metric is not present when the rule engine is configured, IoT Hub will create it automatically.
- **Timestamp**: this is the timestamp when the data is written to CTSDB. Currently, 4 types of configurations are supported:
 - The field value of the original message imported through `${}`.
 - System function. 
 - timestamp(): the current system time of the message hitting the rule engine.
 - Constant: it needs to be a Unix timestamp in seconds; if it is left empty, the current time of the message hitting the rule engine will be used by default.
>!If you change the unit of the timestamp of the CTSDB metric to a unit other than second (such as millisecond) after the rule is created, subsequent data writes may fail.
- **Data Fields**: for the type, you can select tag or field type in CTSDB; for the restriction on field name, please see [Overview](https://intl.cloud.tencent.com/document/product/1100/40910); the value has 3 configuration methods: field value of the original message imported through `${}`, constant, or fixed value.


## Advanced Configuration Description
The advanced configuration items are suitable for scenarios where the device-reported data fields are dynamically expanding and cannot be preconfigured. For example, if there are many sensors on the devices that need to transfer data, but different devices have different specifications and configurations, and the number of sensors is variable, then you can use the following advanced configuration to store the data from all device sensors to CTSDB through the rule engine:
![](https://main.qcloudimg.com/raw/cad85dd0aa614631f710f4b55a565370.png)

>?
>- Default Storage Type: the default storage type of dynamically expanding storage fields in CTSDB is tag.
>- Key: this is the JSON key that needs to traverse the expanding storage. IoT Hub will traverse the JSON key value nesting under this key with `_` as the connector and finally store the data in CTSDB. The following example shows the JSON results and configuration retrieved by SQL SELECT in the rule engine (multiple subkeys can be configured) as well as the data actually stored in CTSDB:



## Resending Mechanism

The resending mechanism is used to send the message again in case of a failure in the message forwarding process, which makes sure that the message is received. The details are as follows:
- If message forwarding fails, the system will retry forwarding at intervals of 1s, 3s, and 10s in sequence. If all three retries fail, the message will be discarded.
- If you have configured the forward error action, then after three unsuccessful retries, the message will be forwarded again according to the configured action. If forwarding still fails, the message will be discarded.
