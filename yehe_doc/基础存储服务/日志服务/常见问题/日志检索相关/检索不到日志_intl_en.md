The log search may fail sometimes. In case of a search failure, use the following methods for troubleshooting.

## Checking Search Criteria

A log search failure is often caused by an incorrect time range or search statement. To address this issue, first select a larger time range (such as `last 30 minutes`), leave the search bar empty, and search for logs.



If logs are found, it indicates that the log search is available. We recommend that you check the search [syntax and rules](https://intl.cloud.tencent.com/document/product/614/30439) or modify the time range.

## Checking Index Configuration

The index configuration is required for CLS log search. On the top right of the **Search Analysis** page, click **Index Configuration** to enable both full-text index and key-value index. For more information, see [Enabling Index](https://intl.cloud.tencent.com/document/product/614/39594).



>! The index configuration takes effect in about 1 minute. The new configuration is only effective for log data written subsequently.
>

## Checking Log Collection

### Log collection from Tencent Cloud services

To collect logs from other Tencent Cloud services including TKE and CLB, see [Collection for Tencent Cloud Services](https://intl.cloud.tencent.com/document/product/614/38200) to verify the configuration. If you have any question, please contact [smart customer service](https://intl.cloud.tencent.com/contact-sales).

### Log collection by LogListener client

 If you’re using CLS’s LogListener client to collect logs, perform the following steps for troubleshooting:
1. Check the machine group.
On the top right of the **Search Analysis** page, click **LogListener Collection Configuration** to check the machine group from which you want to collect logs.

>!If the server is exceptional, see [Server Group Exception](https://intl.cloud.tencent.com/document/product/614/17424).	 
2. Check if LogListener obtains the collection configuration from the CLS server.
     Run the following CLI commands:
```shell
/etc/init.d/loglistenerd check
```
     If the result returns “[OK] check loglistener config ok” as shown in the following figure, it indicates that the API is successfully called to obtain the configuration from the CLS server.
     ![](https://main.qcloudimg.com/raw/95022fc7832b36e2e8d51b6fe8ed3ab7.jpg)
     The `logconf` field in the result refers to the collection configuration. If this field is empty, it indicates that no collection configuration is obtained. See [LogListener Use Process](https://intl.cloud.tencent.com/document/product/614/31578) to create a machine group and bind the collection configuration via the console.
3. Use the latest version of LogListener.
     Run the following command to check the version number. See [LogListener Installation Guide](https://intl.cloud.tencent.com/document/product/614/17414) to install the latest version of LogListener.
```shell
/etc/init.d/loglistenerd -v
```
>!LogListener earlier than 2.3.0 cannot collect log files in soft links.
>
4. Check that logs are successfully reported.
 1. Open the LogListener Debug log and access the LogListener installation directory. Set **level** to `DEBUG` in the `etc/loglistener.conf` configuration file and restart LogListener.
![](https://main.qcloudimg.com/raw/05bc0bec901147c2b9e6550a85fa7d82.png)
 2. Run the following command to restart LogListener.
```shell
/etc/init.d/loglistenerd restart
```
 3. Run the following commands to check whether logs are successfully reported.
```shell
tail -f log/loglistener.log | grep "ClsFileProc::readFile" | grep send
```
If log information similar to that shown in the following figure is displayed, logs are successfully reported to the CLS server.
![](https://main.qcloudimg.com/raw/109530d249ed468b5ae2c43b3b1e2341.png)
>!If logs are reported through HTTP, you can capture packets from port 80 to verify whether logs are successfully reported.
>
If logs are not reported, perform the following steps for troubleshooting:

 a. Run the following commands in the installation directory to check whether the LogListener collection configuration is correct.
```shell
tail -f log/loglistener.log | grep "ClsServerConf::load"
```
If the configuration has been delivered to LogListener, log information is as follows:    
![](https://main.qcloudimg.com/raw/d8b24591c6f601af31e57cab8995fd52.png)
In the delivered configuration, check whether the information of `log_type` and `path` is correct:        
 - `log_type` indicates the log parsing type. Valid values: `minimalist_log` (full text in a single line), `delimiter_log` (separator), `json_log` (JSON logs), and `regex_log` (full text in multi lines).   
 - `path` indicates the log collection directory.
       
 b. Run the following command in the installation directory to check whether files are correctly listened to:
```shell
grep [Name of the reported log file] log/loglistener.log
```
- If no log information is displayed, run the `grep regex_match log/loglistener.log` command to search for log information and check whether the regular expression is correctly configured in the console. If the content shown in the following figure is displayed, the file name match based on the regular expression fails. In this case, please log in to the console and change the regular expression.
![](https://main.qcloudimg.com/raw/8b9756fc97dc9fe38e49ddde4fb20335.png)
 c. Check whether the log regular expression parse is correct.
For the extraction modes of full regular expression and full text in multi lines, regular expressions need to be specified. For full text in multi lines, the first line regular expression must match the entire content of the first line, instead of the beginning part of the first line.
Use the log content shown in the following figure as an example. Lines beginning with `INFO`, `ERROR`, and `WARN` are the first lines of logs. In addition to `(INFO|ERROR|WARN)`, the characters following `INFO`, `ERROR`, and `WARN` also need to be matched.
![](https://main.qcloudimg.com/raw/c43a440e46ca0ff82d21275d90557e44.png)
-  Incorrect configuration: `^(INFO|ERROR|WARN)`
-  Correct configuration: `^(INFO|ERROR|WARN).*`

5. A file can only be collected to one log topic and a single log line cannot exceed 1 MB.
   Meet these requirements to ensure the complete log collection.



