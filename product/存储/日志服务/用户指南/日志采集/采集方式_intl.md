Logs can be collected via client or API/SDK. Logs collected to CLS will be structured according to certain rules.

## Collection Methods

### Collect logs via API
You can upload structured logs to CLS by calling [CLS API](https://intl.cloud.tencent.com/document/product/614/12445). For more information, see [Uploading Structured Logs](https://intl.cloud.tencent.com/document/product/614/16873).

### Collect logs via SDK
Collecting via SDK is not supported at this time.

### Collect logs via LogListener client in real time

LogListener is a log collection client powered by Tencent Cloud CLS. You can install LogListener on your server to collect logs on a specified path in real time, and perform structured processing on the raw data of your logs. You can use LogListener to collect logs by following the steps below:

1. Install Loglistener on the server.
2. Create a server group on the Tencent Cloud CLS Console.
3. Associate the server group in the log topic, and complete the related configuration.

### Quickly check whether LogListener collects logs successfully
1. You need to enable index feature. For more information, see [Enabling Index](https://intl.cloud.tencent.com/document/product/614/16981).
2. Log in to the [Cloud Log Service Console](https://console.cloud.tencent.com/cls), and click **Log Search** to view logs (there is a short delay in log search).

## Log Structuring

The structuring of logs is to store your log data on the CLS platform in key-value format. After logs are structured, you can download the structured logs, specify keys for search, or ship logs in a structured manner.

- Collection API allows you to upload structured log data directly.
- LogListener allows you to specify a method for structuring log data, and perform structured parsing on the raw data of your unstructured logs. For example, if the raw data of a log is `10002345987;write;error;topic does not exist`, then you can specify a separator when parsing logs. In this case, the separator is semicolon, and keys are eventid, action, status and msg. So, the log is structured into four key-value pairs, i.e. `eventid:10002345987 action:write status:error msg:topic does not exist`.

