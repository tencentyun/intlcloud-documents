[//]: # (chinagitpath:XXXXX)

IoT Hub Restrictions:

| Type of Restriction | Description |
|--------- | --------- |
| Product | Up to 2,000 products can be created under one account |
| Device | Up to 200,000 devices can be created under one product |
| Product Name | Up to 32 bytes in length |
| Device Name | Up to 48 bytes in length |
| Shadow Document Size | Up to 8 KB |
| Shadow Document Object | Up to 5 layers in depth |
| Custom Attributes Aupported by Device | Up to 100 |
| Task History | Retained for up to 30 days |
| Single-user Task | Up to 5 concurrences |
| Single Firmware Size | Up to 10 MB |
| Uploaded Firmware Count per Product | Up to 50 |
| Monitoring Data History | Retained for up to 30 days |
| Topic Broadcast | Topic broadcast not supported |
| Broadcast Topic | No broadcast topic |
| Custom Topic | Up to 64 bytes in length |
| CoAP Protocol Packet Size | Up to 1 KB |
| MQTT Protocol Packet Size | Up to 256 KB |
| Communication | Devices can only publish and subscribe to messages of their own topics. |
| Device Subscription | Device subscription and subscription cancellation take effect immediately. F  or example, if device sends an SUB request to topic A, and a message is immediately sent to topic A , the device will receive the message |
| Rule Engine | Up to 100 rules under one account |
| Rule Engine | Data must be in JSON format to be forwarded using the rule engine (binary data format will be supported in the future). |
| Rule Engine | Up to 10 data forwarding operations can be performed in one rule. |
| Traffic Limit | Report up to 30 QoS0 messages per second or 10 QoS1 messages per second; receive up to 50 messages per second per device. |
| Offline message count and retention period | Up to 50 unconfirmed Qos=1 messages; up to 1 day. |


