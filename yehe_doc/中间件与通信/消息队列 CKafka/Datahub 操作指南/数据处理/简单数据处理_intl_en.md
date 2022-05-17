## Overview

DataHub provides the simple data processing feature. You only need to pass in data and configuration items, and this feature can format the data, return the processed structured data, and distribute it to offline/online processing systems, connecting data sources to data processing systems.

## Directions

### Creating rule

1. Log in to the [CKafka console](https://console.intl.cloud.tencent.com/ckafka).
2. Click **Data Processing** on the left sidebar, select the region, and click **Create Task**.
3. Enter the basic task information.
   ![](https://qcloudimg.tencent-cloud.cn/raw/73e8fc56b2851cefa6603d697e9dd986.png)
   - Task Name: It can only contain letters, digits, underscores, or symbols ("-" and".").
   - Source Topic: CKafka topic of the source data.
   - Target Topic: CKafka topic of the target data.
   - Starting Position: Select the topic offset of historical messages when dumping.
   - Use EventBridge as Underlying Engine: You can select to use EventBridge as the underlying engine.
     <dx-alert infotype="explain" title="">
     This is supported only in Beijing, Shanghai, and Guangzhou regions.
     </dx-alert>
   - Role Authorization: To use the EventBridge service as the underlying engine, you need to grant a third-party role to perform access to related products for you.
4. Click **Next** to set a data processing rule.
   ![](https://qcloudimg.tencent-cloud.cn/raw/49bf010bada193aada2557bc6937e0b8.png)
   - Original Data: You can select **Pulled from the source topic** or **Custom**.
   - Parsing Mode: You can select **JSON**, **Separator**, or **Regex**.
     - JSON
     - Separator: You can select a `Space`, `Tab`, `,`, `;`, `|`, or `Custom`.
     - Regex: You need to enter a regex.
5. After selecting the parsing mode, click **OK** to start parsing data.
6. After data parsing is completed, set the filtering rule and data processing mode.
>?Currently, only JSON is supported as an output format.
>
<img src = "https://qcloudimg.tencent-cloud.cn/raw/173eb91993a5e4333066f7ebf034811a.png" style="width: 100%">  
   - Filter: It outputs only data meeting the filter rules. Supported filter match modes include **By prefix**, **By suffix**, **Contains**, **Except**, **By value**, and **By IP**. For more information, see [Filter Rule Description](https://intl.cloud.tencent.com/document/product/597/46823).
   - Data Processing: Valid values of `TYPE` are **Default**, **Preset**, **Mapping**, **Custom**, and **JSONPATH**.
     - TYPE = Default: `VALUE` is mapped based on the parsing result and cannot be modified.
     - TYPE = Preset: You can select a system preset value for `VALUE`. Currently, `DATE` (timestamp) is supported.
     - TYPE = Mapping: You can select an existing key. The final output value of `VALUE` is mapped by the specified key.
     - TYPE = Custom: You can enter a custom value for `VALUE`.
     - TYPE = JSONPATH: Parse nested JSON data. Use `$` as the first character and `.` as the last character to locate a specific field in nested JSON data.
7. Click **Test** to check the test result.
8. Set the failure handling rule.
   - Retry Interval: Specify the interval for retry upon failure, which can range from 60 seconds to 1 hour.
   - Retry Count: Specify the maximum number of retries upon failure. After this limit is exceeded, the message will be considered a failed message. The result of `Retry Count` multiplied by `Retry Interval` should be equal to or less than 6 hours.
   - Handle Failed Message: Specify the method of processing failed messages. You can choose to **discard** or **retain** failed messages, or deliver them to the **dead letter queue** (in this case, you need to specify the dead letter topic).
9. Click **Submit**.

### Editing rule

1. In the task list on the **[Data Processing](https://console.intl.cloud.tencent.com/ckafka/datahub-process)** page, click the **ID** of the target task to enter its basic information page.
2. Click **Edit Rule** in the top-right corner of the **Processing Rule** module to modify the data processing rule.

### Changing configuration

1. In the task list on the **[Data Processing](https://console.intl.cloud.tencent.com/ckafka/datahub-process)** page, click the **ID** of the target task to enter its basic information page.
2. Click **Change Configurations** in the top-right corner of the **Configuration Information** module to modify the configuration of the data processing rule.

### Viewing monitoring data

1. In the task list on the **[Data Processing](https://console.intl.cloud.tencent.com/ckafka/datahub-process)** page, click the **ID** of the target task to enter its basic information page.
2. Enter the basic task information page.
3. At the top of the task details page, click **Monitoring**, select the resource to be viewed, and set the time range to view the corresponding monitoring data.


### Pausing task

On the **[Data Processing](https://console.intl.cloud.tencent.com/ckafka/datahub-process)** page, click **Pause** in the **Operation** column of the target task to pause the task.

> ? As this operation is an async task with a delay, the task status may not change immediately.

### Resuming task

On the **[Data Processing](https://console.intl.cloud.tencent.com/ckafka/datahub-process)** page, click **Resume** in the **Operation** column of the target task to resume the paused task.

> ? A paused task can be resumed to continue processing data.


### Deleting task

On the **[Data Processing](https://console.intl.cloud.tencent.com/ckafka/datahub-process)** page, click **Delete** in the **Operation** column of the target task and click **OK** in the pop-up window to delete the task.

> ?
>
> - Once the task is deleted, data processing will be stopped and the task record will be deleted, but the previously processed data and CKafka instance involved will not be affected.
> - A task cannot be recovered once deleted. Proceed with caution.
