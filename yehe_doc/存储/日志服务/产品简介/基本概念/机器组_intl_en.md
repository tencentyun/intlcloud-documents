### Machine group

A machine group is a list of machines for which logs need to be collected. In machine groups, CLS manages all servers for which logs are collected using [LogListener](https://intl.cloud.tencent.com/document/product/614/31578).

A machine group can contain multiple machines. When an application/service is deployed on multiple machines with the same log file path, the machines can be grouped into a machine group. In this way, you only need to configure the log data collection rule once in the console, and the rule takes effect on all the machines in the machine group in batches.

A machine group can be associated with a log topic. That is, all the logs in the machine group are reported to the same log topic. You can also associate a machine group with multiple log topics. That is, logs of different paths in a machine group are reported to different log topics.

Machine groups can be defined in two ways:
- IP address: add an IP address list to a machine group. Then the machines corresponding to the IPs will be automatically added to the machine group.
- Label: add labels to machines when installing [LogListener](https://intl.cloud.tencent.com/document/product/614/17414). Then the machines with the labels will be automatically added to the machine group.

### Examples

An e-commerce project has 6 machines and 3 services (payService, userService, and stockService). The deployment method is as follows:
payService is deployed on 2 machines, and there are 2 log file paths. userService and stockService are deployed on 4 machines, and there are 4 log file paths. Each of the log types (access_log and error_log) of each of the services needs to be reported to an independent log topic.

| Machine        | Service Deployed                 | Log File Path                                                 |
| ----------- | ------------------------ | ------------------------------------------------------------ |
| 192.168.1.1 | payService               | /data/log/payService/access_log.log<br />/data/log/payService/error_log.log |
| 192.168.1.2 | payService               | /data/log/payService/access_log.log<br />/data/log/payService/error_log.log |
| 192.168.1.3 | userService,stockService | /data/log/userService/access_log.log<br />/data/log/userService/error_log.log<br />/data/log/stockService/access_log.log<br />/data/log/stockService/error_log.log |
| 192.168.1.4 | userService,stockService | /data/log/userService/access_log.log<br />/data/log/userService/error_log.log<br />/data/log/stockService/access_log.log<br />/data/log/stockService/error_log.log |
| 192.168.1.5 | userService,stockService | /data/log/userService/access_log.log<br />/data/log/userService/error_log.log<br />/data/log/stockService/access_log.log<br />/data/log/stockService/error_log.log |
| 192.168.1.6 | userService,stockService | /data/log/userService/access_log.log<br />/data/log/userService/error_log.log<br />/data/log/stockService/access_log.log<br />/data/log/stockService/error_log.log |

When deploying LogListener on servers, you can add a label for each machine according to the services running on the machine. See the table below.

|   Machine     | Service Deployed                 | Label                     |
| ----------- | ------------------------ | ------------------------ |
| 192.168.1.1 | payService               | payService               |
| 192.168.1.2 | payService               | payService               |
| 192.168.1.3 | userService,stockService | userService,stockService |
| 192.168.1.4 | userService,stockService | userService,stockService |
| 192.168.1.5 | userService,stockService | userService,stockService |
| 192.168.1.6 | userService,stockService | userService,stockService |

Then create 3 machine groups in the console and define them with labels payService, userService, and stockService. Then, associate the machine groups with log topics and add the corresponding collection configuration. By now, log reporting configuration is completed.

| Log Topic                      | Associated Machine Group   | Collection Path                              |
| ----------------------------- | ------------ | ------------------------------------- |
| payService_access_log_topic   | payService   | /data/log/payService/access_log.log   |
| payService_error_log_topic    | payService   | /data/log/payService/error_log.log    |
| userService_access_log_topic  | userService  | /data/log/userService/access_log.log  |
| userService_error_log_topic   | userService  | /data/log/userService/error_log.log   |
| stockService_access_log_topic | stockService | /data/log/stockService/access_log.log |
| stockService_error_log_topic  | stockService | /data/log/stockService/error_log.log  |

If a service needs to be expanded in the future, you only need to add the service label to the machines to be added so that the new machines can be automatically added to the corresponding machine group for log collection, significantly improving Ops and deployment efficiency.

