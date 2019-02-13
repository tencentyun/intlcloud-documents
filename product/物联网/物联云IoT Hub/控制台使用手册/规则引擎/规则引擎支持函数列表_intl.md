[//]: # (chinagitpath:XXXXX)

In the data processing part of the rule engine, SQL-like statements can be written to filter the data in the topic and then forward the data to the third-party components or send it to other devices. In general, the fields of the new data can be a reference to the original message (via ${}) or a constant. Due to the diversity of device reporting scenarios and the flexibility of rule engine configuration, data sometimes needs to maintain the original context information (for example, when the data is forwarded the CTSDB, data needs to be stored with the devicename of the source message as a tag). This can be achieved by the function list supported by rule engine.

### Function List

| Function name | Description |
|---------|---------|
| productId() | Return the ID of the product from which the message comes |
| deviceName() | Return the name of the device from which the message comes |
| timestamp() | Return the current Unix system timestamp in seconds |
| topic() | Return the original topic from which the message comes |
| topic(n) | Return the nth segment split by '/' in the original topic from which the message comes |
| abs(num) | Return the absolute value of a value |
| upper() | Return the string after conversion to uppercase |
| lower() | Return the string after conversion to lowercase |
| random() | Return a random floating-point number |
| randint(min,max) | Return a random integer between min and max |


