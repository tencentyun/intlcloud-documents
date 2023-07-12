### Log

Logs are record data generated during the running of an application system, such as user operation logs, API access logs, and system error logs. Logs are usually stored in text format on the host where the application system resides. A log corresponding to a system running record may contain one line of text (single-line log) or multiple lines of text (multi-line log).

Logs can be uploaded the CLS via [LogListener](https://intl.cloud.tencent.com/document/product/614/31578) or other methods such as APIs or SDKs.

**Example of a single-line log:**

```
59.x.x.x - - [06/Aug/2019:12:12:19 +0800] "GET /nginx-logo.png HTTP/1.1" 200 368 "http://119.x.x.x/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/75.0.3770.142 Safari/537.36" "-"
```

**Example of a multi-line log:**

```
  java.net.SocketTimeoutException:Receive timed out
    at j.n.PlainDatagramSocketImpl.receive0(Native Method)[na:1.8.0_151]
    at j.n.AbstractPlainDatagramSocketImpl.receive(AbstractPlainDatagramSocketImpl.java:143)[^]
    at j.n.DatagramSocket.receive(DatagramSocket.java:812)[^]
    at o.s.n.SntpClient.requestTime(SntpClient.java:213)[classes/]
    at o.s.n.SntpClient$1.call(^:145)[^]
    at ^.call(^:134)[^]
    at o.s.f.SyncRetryExecutor.call(SyncRetryExecutor.java:124)[^]
    at o.s.f.RetryPolicy.call(RetryPolicy.java:105)[^]
    at o.s.f.SyncRetryExecutor.call(SyncRetryExecutor.java:59)[^]
    at o.s.n.SntpClient.requestTimeHA(SntpClient.java:134)[^]
    at ^.requestTimeHA(^:122)[^]
    at o.s.n.SntpClientTest.test2h(SntpClientTest.java:89)[test-classes/]
    at s.r.NativeMethodAccessorImpl.invoke0(Native Method)[na:1.8.0_151]
```

The main components of a log are as follows:

| Component | Description | Example |
| ----------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| \_\_TIMESTAMP\_\_ | Log time, in the format of a UNIX timestamp in milliseconds                           | 1640005601188                                                |
| \_\_FILENAME\_\_  | Log source file                                                 | /data/log/nginx/access.log                                   |
| \_\_SOURCE\_\_    | Log source IP                                                   | 10.0.1.2                                                     |
| Log body          | Log body content, in `key:value` format (`key` is the field name, and `value` is the field value.)<br />If the log extraction mode is full text in a single line or full text in multi lines (the entire raw log is reported without splitting), the entire log is stored in the \_\_CONTENT\_\_ field.<br />If the log extraction mode is any other mode (such as splitting with a separator), each part of the raw log corresponds to a `key:value` pair. | Full text in a single line or full text in multi lines:<br />10.20.20.10;[2018-07-16 13:12:57];GET /online/sample HTTP/1.1;200<br />Other modes:<br />IP: 10.20.20.10 <br />request: GET /online/sample HTTP/1.1 <br />status: 200 <br />time: [2018-07-16 13:12:57] |
| Metadata            | Simple description or categorization of logs. For example, the cluster or container of a TKE log is stored in the `key:value` format, where `key` starts with \_\_TAG\_\_.. | \_\_TAG\_\_.clusterId:1skzv59c                               |


### Log group

A log group (LogGroup) is a collection of multiple logs. In the process of log upload, to increase data read/write efficiency, multiple logs can be packaged into one log group and then sent to CLS.

Logs in the same log group have the same basic information (\_\_TIMESTAMP\_\_, \_\_FILENAME\_\_, \_\_SOURCE\_\_, metadata, etc.).

