## Log Development

You can use the following statements in the program to output a log:

- echo or echo()
- print or print()
- print_r()
- var_dump()

For example, you can query the output content in the function log by running the following code:

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

Currently, all function logs are delivered to CLS. You can configure the function log delivery. For more information, please see [Log Delivery Configuration](https://intl.cloud.tencent.com/document/product/583/39778).
You can query function execution logs on the log query page of SCF or CLS. For more information on the log query method, please see [Log Search Guide](https://intl.cloud.tencent.com/document/product/583/39777).

>? Function logs are delivered to the `LogSet` log set and `LogTopic` log topic in CLS, both of which can be queried through the function configuration.

## Custom Log Fields

Currently, the content output by simple `echo` or `print` in the function code will be recorded in the `SCF_Message` field when it is delivered to CLS. For descriptions of CLS fields, please see [Log Delivery Configuration](https://intl.cloud.tencent.com/document/product/583/39778).

At present, SCF supports adding custom fields to the content output to CLS. By doing so, you can output business fields and related data content to logs and use the search capability of CLS to query and track them in the execution process.

### Output method

If a single-line log output by a function is in JSON format, the JSON content will be parsed into the format of **field:value** when it is delivered to CLS. Only the first level of the JSON content can be parsed in this way, while other nested structures will be recorded as values.

You can run the following code to test:

```php
<?php
function main_handler($event, $context) {
    $custom_key = array('key1' => 'test value 1', 'key2' => 'test value 2');
    echo json_encode($custom_key);
    return "hello world";
}
?>
```

### Search method

When using the above code for test:

- You can search for the two fields `key1` and `key2` in the field log in CLS.
- You can also enable the key-value index in CLS and use `key1` and `key2` as keywords for search. For more information, please see [Configuring Index](https://intl.cloud.tencent.com/document/product/614/39594).

>! After modifying the index configuration, it will take effect only for newly written data.

**Search result**
After the test is written to CLS, you can find the `key1` and `key2` fields in the log query as shown below:
![](https://main.qcloudimg.com/raw/6667c6e20650eedb43f5e4f3bb4fa047.png)
