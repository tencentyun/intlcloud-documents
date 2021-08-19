| Item | Description |
| ---------------------- | ------------------------------------------------------------ |
| Product | Up to 2,000 products can be created under one account |
| Device | Up to 1,000,000 devices can be created under one product |
| Gateway subdevice | One gateway device can be bound to 1,500 subdevices at most |
| Product name | Up to 32 bytes in length |
| Device name | Up to 48 bytes in length |
| Shadow document size | Up to 8 KB |
| Shadow document object | Up to 5 layers in depth |
| Custom attributes supported by device | Up to 100 |
| Historical tasks | Retained for up to 30 days |
| Tasks for a single user | Up to 5 concurrent tasks |
| Single firmware size | Up to 1,024 MB |
| Number of uploaded firmware files per product | Up to 100 |
| Historical monitoring data | Retained for up to 30 days |
| Topic class | Up to 100 topic classes can be defined for one product |
| Broadcast topic | Supported |
| Custom topic | Up to 64 bytes in length |
| CoAP protocol packet size | Up to 1 KB |
| MQTT protocol packet size | Up to 16 KB |
| Communication | Devices can only publish and subscribe to messages in their own topics. For transfer over MQTT, only QoS=0 and QoS=1 are supported |
| Device subscription | Device subscription and unsubscription take effect immediately. For example, if a device sends a SUB request to topic A, and a message is immediately sent to topic A, the device will receive the message |
| Rule engine | One account can have up to 100 rules <br>Forwarding in JSON and binary formats is supported <br>Up to 10 data forwarding operations can be performed in one rule |
| Traffic limit | One device can report up to 30 QoS 0 messages per second or 10 QoS 1 messages per second and receive up to 50 messages per second |
| Number of offline messages and retention period | Up to 150 messages can be retained for 24 hours at most for one device |
| `KeepAlive` value range  | 0–900s                                                       |
