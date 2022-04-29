## Logging

You can use the `System.out.println()` and `java.util.logging.Logger()` statements in the program to output a log:



For example, you can query the output in the function log by running the following code.

```java
System.out.println("Hello world!");
```

```java
Logger logger = Logger.getLogger("AnyLoggerName");
logger.setLevel(Level.INFO);
logger.info("logging message here!");
```



## Log Query

Currently, the function logs can be uploaded to Tencent Cloud SCF. You can complete the configuration as instructed in [Log Delivery Configuration](https://intl.cloud.tencent.com/document/product/583/39778).
You can search function execution logs on the log query page of the SCF or CLS console. For more information on how to query logs, see [Log Search Guide](https://intl.cloud.tencent.com/document/product/583/39777).

>? Function logs uploaded to logset and log topic can be both queried with a function configured.


## Custom Log Fields

Currently, the content output by simple log print statements in the function code will be recorded in the `SCF_Message` field when it is delivered to CLS. For descriptions of CLS fields, see [Log Delivery Configuration](https://intl.cloud.tencent.com/document/product/583/39778#.E7.B4.A2.E5.BC.95.E9.85.8D.E7.BD.AE).

Currently, SCF supports adding custom fields to logs that are uploaded to CLS. The custom fields allow you to output business fields and relevant data to logs, and track them using the log search feature of CLS.

> !
>
> - If you need to query the key value of a custom field such as `SCF_CustomKey: SCF`, add a key-value index to the log topic for SCF log delivery as instructed in [Configuring Indexes](https://intl.cloud.tencent.com/document/product/614/39594).
> - To avoid function log query failures caused by misuse of the index configuration, the default destination topic for SCF log delivery (prefixed with `SCF_LogTopic_`) does not support modifying the index configuration. You need to set the destination topic to [custom delivery](https://intl.cloud.tencent.com/document/product/583/39778#.E8.87.AA.E5.AE.9A.E4.B9.89.E6.8A.95.E9.80.92.3Ca-id.3D.22zdytd.22.3E.3C.2Fa.3E) first and then update the log topic's index configuration.
> - After the index configuration is modified for a log topic, it will take effect only for newly written data.



### Output

If a function outputs a single-line log in JSON, the log will be parsed and uploaded to CLS in the `field:value` format. Only the first layer will be parsed, and the remaining nested structure will be recorded as values.

Run the following codes and check results:

```java
package example;

public class Hello {
    public String mainHandler(KeyValueClass kv) {
        System.out.println("{\"key1\": \"test value 1\",\"key2\": \"test value 2\"}");
      return String.format("hello world");
    }
}
```

### Search

After using the above code to perform a test, you can run the following statement to search in **Function Service > Log Query > Advanced Search**:
![](https://qcloudimg.tencent-cloud.cn/raw/6a603daa8141a9d1ea3232ed594fc8a6.png)
For detailed directions, see [Log Search Guide](https://intl.cloud.tencent.com/document/product/583/39777#.E6.8E.A7.E5.88.B6.E5.8F.B0.E6.A3.80.E7.B4.A2).

**Search for logs**
After the test is written to CLS, you can find the `key1` field in the log query as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/9a0bddd851738f8c68338563913a63ca.png)

