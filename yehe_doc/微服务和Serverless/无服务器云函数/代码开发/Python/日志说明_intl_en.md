## Log Development

You can use the following statements in the program to output a log:
- print
- logging module

For example, you can query the output content in the function log by running the following code:
<dx-codeblock>
::: python
import logging
logger = logging.getLogger()
logger.setLevel(logging.INFO)

def main_handler(event, context):
	logger.info('got event{}'.format(event))
	print("got event{}".format(event))
	return 'Hello World!'  
:::
</dx-codeblock>



## Log Query

Currently, all function logs are delivered to CLS. You can configure the function log delivery. For more information, please see [Log Delivery Configuration](https://intl.cloud.tencent.com/document/product/583/39778).
You can query function execution logs on the log query page of SCF or CLS. For more information on the log query method, please see [Log Search Guide](https://intl.cloud.tencent.com/document/product/583/39777).

>? Function logs are delivered to the `LogSet` log set and `LogTopic` log topic in CLS, both of which can be queried through the function configuration.


## Custom Log Fields

Currently, the string content output by simple `print` or `logger` in the function code will be recorded in the `SCF_Message` field when it is delivered to CLS. For descriptions of CLS fields, please see [Log Delivery Configuration](https://intl.cloud.tencent.com/document/product/583/39778#.E7.B4.A2.E5.BC.95.E9.85.8D.E7.BD.AE).

At present, SCF supports adding custom fields to the content output to CLS. By doing so, you can output business fields and related data content to logs and use the search capability of CLS to query and track them in the execution process.

### Output method

If a single-line log output by a function is in JSON format, the JSON content will be parsed into the format of `field:value` when it is delivered to CLS. Only the first level of the JSON content can be parsed in this way, while other nested structures will be recorded as values.

You can run the following code to test:
<dx-codeblock>
::: python
# -*- coding: utf8 -*-
import json
		
def main_handler(event, context):
	print(json.dumps({"key1": "test value 1","key2": "test value 2"}))
	return("Hello World!")
:::
</dx-codeblock>

### Search method

When using the above code for test:
- You can search for the two fields `key1` and `key2` in CLS.
- You can also enable the key-value index in CLS and use `key1` and `key2` as keywords for search. For more information, please see [Configuring Index](https://intl.cloud.tencent.com/document/product/614/39594).
>! After modifying the index configuration, it will take effect only for newly written data.



**Search result**
After the test is written to CLS, you can find the `key1` and `key2` fields in the log query as shown below:
![](https://main.qcloudimg.com/raw/3cfe31543cb065044fab27b52a7a4242.png)

