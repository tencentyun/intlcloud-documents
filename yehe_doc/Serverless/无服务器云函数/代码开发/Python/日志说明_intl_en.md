## Logging

You can use methods such as `print` or `logging` in the program to output a log. For example, you can run the following codes to query the output in the function logs.

```python
import logging
logger = logging.getLogger()
logger.setLevel(logging.INFO)
	

def main_handler(event, context):
      logger.info('got event{}'.format(event))
      print("got event{}".format(event))
      return 'Hello World!'  
```



## Log Query

Currently, the function logs can be uploaded to Tencent Cloud SCF. You can complete the configuration as instructed in [Log Delivery Configuration](https://intl.cloud.tencent.com/document/product/583/39778).
You can search function execution logs on the log query page of the SCF or CLS console. For more information on how to query logs, see [Log Search Guide](https://intl.cloud.tencent.com/document/product/583/39777).

>? Function logs uploaded to logset and log topic can be both queried with a function configured.


## Custom Log Fields

The output of a simple `print` or `logger` method in the function codes will be recorded in the `SCF_Message` field when being uploaded to CLS. For more information about CLS fields, see [Configuring index](https://intl.cloud.tencent.com/document/product/583/39778#configuring-index).

Currently, SCF supports adding custom fields to logs that are uploaded to CLS. The custom fields allow you to output business fields and relevant data to logs, and track them using the log search feature of CLS.

### Output

If a function outputs a single-line log in JSON, the log will be parsed and uploaded to CLS in the `field:value` format. Only the first layer will be parsed, and the remaining nested structure will be recorded as values.

Run the following codes and check results:

```python
# -*- coding: utf8 -*-
import json
		
def main_handler(event, context):
			print(json.dumps(event))
			return("Hello World!")
```

### Search

After running the following test events, you can search `key1` and `key2` fields in CLS logs. In addition, you can enable the key-value index configuration in CLS, and search the `key1` and `key2` keywords. For more information, see [Configuring Index](https://intl.cloud.tencent.com/document/product/614/39594).

**Test events**
```
{
    "key1": "test value 1",
    "key2": "test value 2"
}
```
**Search for logs**
After writing the test events to CLS, you can find the `key1` and `key2` fields on the log query page, as shown below:
![](https://main.qcloudimg.com/raw/3cfe31543cb065044fab27b52a7a4242.png)

