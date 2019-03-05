[//]: # (chinagitpath:XXXXX)

In terms of rule engine’s data processing, SQL-like statements are supported to filter data in topics. The data can then be forwarded to third-party components or sent to other devices. In general, the fields of the new data can be a reference to the original message (via ${}) or a constant. Due to the diversity of device reporting scenarios and the flexibility of rule engine configuration, data sometimes needs to maintain the original context information (for example, when the data is forwarded the CTSDB, data needs to be stored with the devicename of the source message as a tag). This can be achieved by the function list supported by rule engine.

### Function List

| Function | Description |
|---------|---------|
| productId() | Return product ID from the message source |
| deviceName() | Return device name from the message source |
| timestamp() | Return to the current Unix system’s timestamp (in seconds) |
| topic() | Return the original topic from message source |
| topic(n) | Return the nth segment split by '/' in the original topic from the message source |
| abs(num) | Return the absolute value |
| upper() | Return the string after conversion to uppercase |
| lower() | Return the string after conversion to lowercase |
| random() | Return a random floating-point number |
| randint(min,max) | Return a random integer between min and max |


