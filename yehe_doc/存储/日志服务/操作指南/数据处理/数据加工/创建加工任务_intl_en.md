## Overview

The data processing feature provides the capabilities to filter, cleanse, mask, enrich, and distribute log data. It can be benchmarked against the open-source component Logstash, but its input and output are CLS log topics.

![](https://qcloudimg.tencent-cloud.cn/raw/d974fd27c17733119feb79035516d6a0.png)

You can select a source log topic and write Domain Specific Language (DSL) processing function statements to process logs line by line and send logs that meet certain requirements to specified target log topics.   
If your business uses only processed logs, we recommend you configure the log retention period of the source log topic as one day and not enable the index in order to reduce costs.

## Billing
Data processing incurs fees. For example, if you have a log topic in Guangzhou and 100 GB raw data that becomes 50 GB after being filtered, and the target topic is written (with index not enabled), you need to pay:  
- Data processing fees: 100 GB * 0.026 USD/GB = 2.6 USD 
- Write traffic fees of the target topic: 50 GB * 0.3 (compression ratio) * 0.032 USD/GB = 0.48 USD  
- Storage fees of the target topic: 50 GB * 0.3 (compression ratio) * 0.0024 USD/GB  = 0.036 USD  

The total is 3.116 USD, which is generally the case for regions in the Chinese mainland. For billing details in special regions, see [Product Pricing](https://intl.cloud.tencent.com/document/product/614/37510).

## Use cases

For most users, data processing can achieve the following:
- Extract structured data to facilitate future operations such as search, analysis, and dashboard generation.   
- Simplify logs to reduce use costs. Unnecessary logs will be discarded to reduce storage and traffic costs.
- Mask sensitive data, such as users' ID numbers and phone numbers.
- Ship logs by category. For example, logs are categorized by ERROR, WARNING, or INFO and then distributed to different log topics.


## Common DSL functions

The following describes some DSL functions that are commonly used for data processing. The corresponding use cases can be viewed in **DSL Statement Generator** on the **Create Data Processing Task** > **Edit Processing Statement** page in the console. You can directly copy the sample code and modify parameters as needed for quick use.
- Extracting structured data: `ext_sep()` for extracting by separator, `ext_json` or `ext_json_jmes` for extracting by JSON, and `ext_regex()` for extracting by regular expression
- Simplifying logs: `log_drop` for discarding a line of log and `fields_drop()` for discarding log fields
- Masking sensitive data: `regex_replace()`
- Classifying logs: `t_if_else()` and `t_switch()` for determining conditions, and `log_output()` for distributing logs
- Editing fields: `fields_set()` for adding/resetting fields, and `fields_rename()` for renaming fields
- Determining the presence of a field or data in logs: `has_field()` for determining whether a field exists and `regex_match()` for determining whether certain data exists
- Comparing numerical values in logs: `op_gt()` (greater than), `op_ge()` (greater than or equal to), and `op_eq()` (equal to); functions for addition, subtraction, multiplication, and division, such as `op_mul()` for multiplication and `op_add()` for addition
- Processing text in logs: `str_uppercase()` for uppercase or lowercase switching and `str_replace()` for text replacement
- Processing time values in logs: `dt_to_timestamp()` for converting a time value to a UTC timestamp     

The preceding are common DSL functions used in data processing scenarios. The DSL statement generator also provides other DSL functions for your reference. You can copy a desired function to the DSL function editing box, modify parameters, and use it.

The following describes how to create a data processing task.

## Prerequisites

- You have activated CLS, created a source log topic, and successfully collected log data.
- You have created a target log topic, which is recommended to be empty to allow the writing of processed data.
- The current account has the permission to configure data processing tasks.

>! 
> - Data processing can process only real-time log streams but not historical logs.
> - If the data processing console does not automatically load raw log data, the possible cause is that your log topic does not have real-time log streams. In that case, you need to manually add custom logs in JSON format to complete writing the data processing script.
> 

## Directions

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. On the left sidebar, click **Data Processing**.  
3. Click **Create Processing Task**.
![](https://qcloudimg.tencent-cloud.cn/raw/e96c95d62e1c810492d68b1663f366e8.png)
4. On the **Basic Info** page, configure the following information:
![](https://qcloudimg.tencent-cloud.cn/raw/1076f04e3090f71483e843f4d8a2e679.png)
 - Task Name: Enter the custom task name.
 - Source Log Topic: Select the source log topic.
 - Target Log Topic: Enter the target name and select the log topic. Here, the target name can be the alias of the target log topic and used as an input parameter of the written DSL function. You can configure up to ten target log topics.
5. Click **Next**.
6. On the **Edit Processing Statement** page, perform the following operations:
 1. A DSL function can be tested by two types of data: raw log data and custom data. The system automatically loads raw log data, 100 records by default. If you think the raw log data is insufficient for testing the DSL function, you can directly enter custom data on the **Custom Data** tab. Alternatively, you can click **Add Custom Data** on the **Raw Data** tab, modify the data, and use it as your custom data.
![](https://qcloudimg.tencent-cloud.cn/raw/a80edc9e020d5d2847ad66728e515dfd.png)
>! Custom data must be in JSON format.
> 
 If there are multiple entries of custom data, add them in the following format:
```
[
    {
        "content": "2021-10-07 13: 32: 21|100|Customer not checked in|Jack|Beijing|101123199001230123|"
    },
    {
        "content": "2021-10-07 13: 32: 21|500|Checked in successfully|Jane|Sanya|501123199001230123|"
    },
    {
        "content": "2021-10-07 13: 32: 21|1000|Checked out|Lily|Sanya|101123196001230123|"
    }
]
```
 2. Click **DSL Statement Generator**.

 3. In the pop-up window, select a function, and click **Insert Function**.
The DSL statement generator provides the descriptions and examples of multiple types of functions. You can copy and paste the examples to the processing statement editing box and modify parameters as needed to write your own DSL functions. You can also refer to [Processing Example](https://intl.cloud.tencent.com/document/product/614/43570) to quickly understand how to write a DSL function. 

 4. After writing the DSL processing statement, click **Preview** or **Checkpoint Debugging** to run and debug the DSL function.
The running result will be displayed at the bottom right of the page. You can adjust the DSL statement according to the running result until it meets your requirements.
![](https://qcloudimg.tencent-cloud.cn/raw/e3a8a47fc5d0e50532ca4f7b186eb421.png)
7. Click **OK** to submit the data processing task.
