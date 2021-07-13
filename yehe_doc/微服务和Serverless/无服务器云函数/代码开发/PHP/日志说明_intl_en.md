## Logging

You can use the following statements in the program to output the log:

- echo or echo()
- print or print()
- print_r()
- var_dump()

For example, you can query the output in the function log by running the following code.

```php
<?php
function main_handler($event, $context) {
    print_r ($event);
    print_r ($context);
    echo "hello world\n";
    print "hello world\n";
    var_dump ($event);
    return "hello world";
}
?> 
```



## Log Query

Currently, the function logs can be uploaded to Tencent Cloud SCF. You can complete the configuration as instructed in [Log Delivery Configuration](https://intl.cloud.tencent.com/document/product/583/39778).
You can search function execution logs on the log query page of the SCF or CLS console. For more information on how to query logs, see [Log Search Guide](https://intl.cloud.tencent.com/document/product/583/39777).

>? Function logs uploaded to logset and log topic can be both queried with a function configured.

## Custom Log Fields

The output of a simple `echo` or `print` method in the function codes will be recorded in the `SCF_Message` field when being uploaded to CLS. For more information about CLS fields, see [Configuring index](https://intl.cloud.tencent.com/document/product/583/39778).

Currently, SCF supports adding custom fields to logs that are uploaded to CLS. The custom fields allow you to output business fields and relevant data to logs, and track them using the log search feature of CLS.

### Output

If a function outputs a single-line log in JSON, the log will be parsed and uploaded to CLS in the “**field:value**” format. Only the first layer will be parsed, and the remaining nested structure will be recorded as values.

Run the following codes and check results:

```php
<?php
function main_handler($event, $context) {
    echo json_encode($event);
    return "hello world";
}
?> 
```

### Search

When running the following test events to test, you can:

- Search `key1` and `key2` fields in CLS field logs.
- Enable the key-value index configuration in CLS, and search by the keywords `key1` and `key2`. For more information, see [Configuring Index](https://intl.cloud.tencent.com/document/product/614/39594).

**Testing event** (Hello world event template by default):

```
{
    "key1": "test value 1",
    "key2": "test value 2"
}
```

**Search for logs**
After writing the test events to CLS, you can find the `key1` and `key2` fields on the log query page, as shown below:
![](https://main.qcloudimg.com/raw/6667c6e20650eedb43f5e4f3bb4fa047.png)
