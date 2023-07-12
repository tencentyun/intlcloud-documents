

## Overview

Syslog refers to system logs or records and is a standard for sending log messages in internet protocols. It is supported by network routers, switches, firewalls, and UNIX/Linux servers. Syslog monitoring and management are important for business operations, helping reduce system downtime, improve network performance, and enhance security policies.

## Prerequisites

You have deployed RSyslog.
- You have activated CLS.
- You have installed LogListener 3.0.1.0 or later on the target server with the RSyslog IP.
- The configuration in the console is made available through an allowlist. [Submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.

Use `rsyslog/etc/rsyslog.conf` to enable UDP/TCP forwarding:
![](https://qcloudimg.tencent-cloud.cn/raw/2dad44a1d89d9b0aabbb89ebd339805b.png)

>?For detailed directions on how to install LogListener, see [LogListener Installation Guide](https://intl.cloud.tencent.com/document/product/614/17414).

## Directions


### Configuring RSyslog forwarding
- On the syslog server, modify RSyslog's configuration file `/etc/rsyslog.conf` by adding the forwarding rule in the last line. Then, RSyslog will forward syslog to the specified IP and port. If the current server is used to collect local syslog, the forwarding address should be `127.0.0.1`, and the port can be a random idle port.
- If another server is used to collect local syslog, the forwarding address should be the public network IP of the server, and the port can be a random idle port.

The following configuration indicates to forward all logs to `127.0.0.1:1000` over TCP. For more information on the configuration file, see [RSyslog Documentation](https://www.rsyslog.com/doc/v8-stable/configuration/index.html).

```
*.* @@127.0.0.1:1000
```

Run the following command to restart RSyslog for the log forwarding rule to take effect.
```
sudo service rsyslog restart
```

### Configuring the syslog collection rule in the CLS console

#### **Step 1. Select a log topic**
- To select a new log topic, perform the following steps: Log in to the [CLS console](https://console.cloud.tencent.com/cls).
	1. On the left sidebar, click **Overview** to enter the overview page.
	2. In the **Other Logs** section, find syslog collection and click **Access Now**.

	3. On the **Create Log Topic** page, configure the log topic information such as the name and log retention period as needed and click **Next**.
- To select an existing log topic, perform the following steps: Log in to the [CLS console](https://console.cloud.tencent.com/cls).
  1. On the left sidebar, click **Log Topic** and select the target log topic to enter the log topic management page.
  2. On the **Collection Configuration** tab, click **Add** in the **LogListener Collection Configuration** section.


#### **Step 2. Configure a machine group**

On the **Machine Group Management** page, select the machine group to which to bind the current log topic and click **Next** to proceed to collection configuration. For more information, see [Machine Group](https://intl.cloud.tencent.com/document/product/614/17412).


#### **Step 3. Configure syslog collection**

On the syslog collection configuration page, configure the following information:

| **Configuration Item** | **Type** | **Description** |
| --- | --- | --- |
| Collection Rule Name | Input box | Indicates the name of this collection rule. |
| Network Type | Radio button | Specifies the syslog transfer protocol: UDP or TCP. |
| Parsing Protocol | Radio button | Specifies the protocol for log parsing. It is empty by default, indicating no parsing. Valid values: `rfc3164` (RFC 3164), `rfc 5424` (RFC5424), `auto` (automatic selection). |
| Output Source | Input box | Specifies the protocol, address, and port for LogListener. It is in the format of [tcp/udp]://[ip]:[port]. If it is not specified, [tcp://127.0.0.1:](http://tcp://127.0.0.1:9999)10000 will be used by default. |
| Upload upon Parsing Failure | Toggle | Specifies the operation upon parsing failure. If it is enabled, the full text of the log will be returned based on the input `key`; otherwise, the log will be discarded. |
| Key Name of Parsing-Failed Logs | Input box | Specifies the key name of logs that failed to be parsed. |



#### **Step 4. Configure an index**

1. On the index configuration page, configure the following information:

 - Index Status: Select whether to enable it.
 - Full-Text Index: Select whether to set it to case-sensitive. Full-Text Delimiter: It is "@&()='",;:\<\>[]{}/ \n\t\r" by default and can be modified as needed.
 - Allow Chinese Characters: Select whether to enable this feature.
 - Key-Value Index: Disabled by default. You can configure the field type, delimiters, and whether to enable statistical analysis according to the key name as needed. To enable key-value index, toggle the switch on.
>!
>- Index configuration must be enabled first before you can perform searches.
>- The modified index rules take effect only for newly written logs. The existing data is not updated.

2. Click **Submit**.

## Viewing syslog
After configuring syslog collection in the current log topic, click **Search** to enter the **Search and Analysis** page to view the syslog.


| **Field** | **Description** |
| --- | --- |
| **HOSTNAME** | Hostname. The current hostname will be obtained if it is not provided in the log. |
| **program** | `tag` field in the protocol. |
| **priority** | `priority` field in the protocol. |
| **facility** | `facility` field in the protocol. |
| **severity** | `severity` field in the protocol. |
| **timestamp** | Timestamp of the log. |
| **content** | Log content, which will contain all the content of unparsed logs if parsing fails. |
| **SOURCE** | IP of the current host. |
| **client\_ip** | Client IP for log transfer. |
