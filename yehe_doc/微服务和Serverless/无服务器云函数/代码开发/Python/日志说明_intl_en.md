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

Currently, all function logs are delivered to CLS. You can configure the function log delivery. For more information, see [Log Delivery Configuration](https://intl.cloud.tencent.com/document/product/583/39778).
You can query function execution logs on the log query page of SCF or CLS. For more information on the log query method, see [Log Search Guide](https://intl.cloud.tencent.com/document/product/583/39777).

>? Function logs are delivered to the `LogSet` log set and `LogTopic` log topic in CLS, both of which can be queried through the function configuration.


## Custom Log Fields

Currently, the string content output by simple `print` or `logger` in the function code will be recorded in the `SCF_Message` field when it is delivered to CLS. For descriptions of CLS fields, see [Log Delivery Configuration](https://intl.cloud.tencent.com/document/product/583/39778#.E7.B4.A2.E5.BC.95.E9.85.8D.E7.BD.AE).

At present, SCF supports adding custom fields to the content output to CLS. By doing so, you can output business fields and related data content to logs and use the search capability of CLS to query and track them in the execution process.

> !
>
> - If you need to query the key value of a custom field such as `SCF_CustomKey: SCF`, add a key-value index to the log topic for SCF log delivery as instructed in [Configuring Indexes](https://intl.cloud.tencent.com/document/product/614/39594).
> - To avoid function log query failures caused by misuse of the index configuration, the default destination topic for SCF log delivery (prefixed with `SCF_LogTopic_`) does not support modifying the index configuration. You need to set the destination topic to [custom delivery](https://intl.cloud.tencent.com/document/product/583/39778#.E8.87.AA.E5.AE.9A.E4.B9.89.E6.8A.95.E9.80.92.3Ca-id.3D.22zdytd.22.3E.3C.2Fa.3E) first and then update the log topic's index configuration.
> - After the index configuration is modified for a log topic, it will take effect only for newly written data.

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

After using the above code to perform a test, you can run the following statement to search in **Function Management > Log Query > Advanced Search**:
![](https://qcloudimg.tencent-cloud.cn/raw/2dc535a38d415fbb8002238dee03078e.png)

**Search result**
After the test is written to CLS, you can find the `key1` field in the log query as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/733c1438e46a3c0342d3ad853b3c2b86.png)
