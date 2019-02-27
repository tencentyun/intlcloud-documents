[//]: # (chinagitpath:XXXXX)

## Use

When communication is performed based on a topic, you can use a rule engine to process the data in the topic and then forward it to other Tencent Cloud services or your business backend services. You do not need to purchase a server or deploy a distributed framework. Instead, you can implement full-stack services for message acquisition, computation and storage by simply configuring the rule engine in the console. The following forwarding types are supported:
- Data forwarding to another topic
- Data forwarding to third-party services
- Data forwarding to CKafka
- Data forwarding to CMQ topic
- Data forwarding to CTSDB
- Data forwarding to TencentDB for MySQL
- Data forwarding to TencentDB for MongoDB

## Creating a Rule
Log in to the [IoT Hub Console](https://console.cloud.tencent.com/iotcloud), select "Rule Engine" in the left pane, click **Create Rule** and enter the rule name to create it.
 - Rule name: 1-32 letters, numbers and underscores. The name cannot be modified. Please name it carefully.
 - Rule description: 0-256 characters, which can be modified.

![](https://main.qcloudimg.com/raw/8a158303b4dec62396dd0d47635d3305.png)

Once the rule is successfully created, the rule details page will be displayed automatically, and then you can write different forwarding rules.
![](https://main.qcloudimg.com/raw/5d12e090d472b6509a9c4cce5f4efe46.png)

