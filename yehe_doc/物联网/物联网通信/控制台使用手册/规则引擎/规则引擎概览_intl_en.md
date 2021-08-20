
## Use
When communication is performed based on a topic, you can use the rule engine to process the data in the topic and then forward it to other Tencent Cloud services or your business backend services. You don't need to purchase a server or deploy a distributed architecture; instead, you can implement full-stack services for message acquisition, computing, and storage simply by configuring the rule engine in the console. The following forwarding types are supported:
- Data forwarding to another topic
- Data forwarding to a third-party service
- Data forwarding to CKafka
- Data forwarding to a CMQ topic
- Data forwarding to a CMQ queue
- Data forwarding to CTSDB
- Data forwarding to TencentDB for MySQL
- Data forwarding to TencentDB for MongoDB

## Creating Rule
1. Log in to the [IoT Hub console](https://console.cloud.tencent.com/iotcloud) and select **Rule Engine** on the left sidebar.
2. Go to the rule engine page, click **Create Rule**, enter the rule name, and click **Confirm**.
 - Rule Name: it can contain up to 32 letters, digits, and underscores (the name cannot be modified once confirmed).
 - Rule Description: it can contain 0–256 characters and can be modified.
![](https://main.qcloudimg.com/raw/fd9387900f2823fe34924981fd20a957.png)
3. After the rule is created successfully, you will be automatically redirected to the rule details page.
![](https://main.qcloudimg.com/raw/7d99d770dc7299475bfb0c823fa813a1.png)

Then, you can write different forwarding rules.


