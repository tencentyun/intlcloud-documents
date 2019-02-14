[//]: # (chinagitpath:XXXXX)

Restrictions in IoT Hub:

| Category | Description |
|--------- | --------- |
| Product | Up to 2,000 products can be created under one account |
| Device | Up to 200,000 devices can be created under one product |
| Product name | Up to 32 bytes in length |
| Device name | Up to 48 bytes in length |
| Shadow document size | Up to 8 KB |
| Shadow document object | Up to 5 layers in depth |
| Custom attributes supported by device | Up to 100 |
| Task history | Retained for up to 30 days |
| Single-user task | Up to 5 concurrences |
| Single firmware size | Up to 10 MB |
| Uploaded firmware count per product | Up to 50 |
| Monitoring data history | Retained for up to 30 days |
| Topic class | Up to 100 topic classes can be defined for one product |
| Broadcast topic | No broadcast topic |
| Custom topic | Up to 64 bytes in length |
| CoAP protocol packet size | Up to 1 KB |
| MQTT protocol packet size | Up to 256 KB |
| Communication | Devices can only publish and subscribe to messages of their own topics. |
| Device subscription | Device subscription and subscription cancellation take effect immediately; for example, if device sends an SUB request to topic A, and a message is immediately sent to topic A , the device will receive the message. |
| Rule engine | Up to 100 rules for one account |
| Rule engine | Data must be in JSON format to be forwarded using the rule engine (binary data format will be supported in the future) |
| Rule engine | Up to 10 data forwarding operations can be performed in one rule |
| Traffic limit | One single device can report up to 30 QoS0 messages per second or 10 QoS1 messages per second and receive up to 50 messages per second |
| Offline message count and retention period | Up to 50 unconfirmed Qos=1 messages can be retained for 1 day |


