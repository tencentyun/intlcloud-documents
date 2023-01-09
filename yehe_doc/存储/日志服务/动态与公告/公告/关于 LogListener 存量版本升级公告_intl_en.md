Dear Tencent Cloud user,

To improve the user experience and avoid the influence from issues in legacy versions, we recommend upgrading the LogListener instances to [v2.5.0 or above](https://intl.cloud.tencent.com/document/product/614/17414).

Log in to the [CLS console](https://console.cloud.tencent.com/cls/hosts) to try out more CLS features.


**New features supported on different LogListener versions are detailed as flows:**

| LogListener Version | Supported Feature | Feature Description | Documentation |
| --------------- | ----------------------- | ------------------------------- | -------------------------------------- |
| v2.6.2         | Incremental collection | When performing collection configuration, users can choose the full or incremental collection policy. | -     |
| v2.6.0         | CVM batch deployment | Users can deploy LogListener on CVM instances in batches for CVM log collection without manually installing LogListener related configuration. | -     |
| v2.5.4 | LogListener service logs | LogListener service logs are used to record the operation, collection, and monitoring activities of LogListener, and you can configure visualized graphs to display such log data. | [LogListener Service Logs](https://intl.cloud.tencent.com/document/product/614/40232) |
| v2.5.2 | Uploading parsing-failure logs | Added the support for uploading parsing-failure logs, using `LogParseFailure` as the key name (`Key`) and the raw log content as the key value (`Value`). |  -                                                            |
| v2.5.0 | Support LogListener auto-upgrade function |  Users can set a time period for Agent auto upgrade or select specific machines to upgrade manually. | [LogListener Upgrade Guide](https://intl.cloud.tencent.com/document/product/614/40233) |
| v2.4.5 | Extracting multi-line logs with regex | Added the extraction mode of **Multi-line - Full regular expression** to LogListener collection configuration rules for log collection. | [Full Regular Expression (Multi-Line)](https://intl.cloud.tencent.com/document/product/614/39590) |
| v2.4.5 | Millisecond-precision logging | LogListener supports millisecond-precision timestamps for log collection. After time-based log collection is enabled, LogListener uploads logs with millisecond-precision UNIX timestamps. |-                                                            |
| v2.3.9 | Configuring blocklist of the collection path | Added support for configuring blocklist of the collection path, allowing users to specify directories and files to be ignored during collection. | -                                                            |
| v2.3.5 | Context search | Added the feature for locating the current log, allowing users to quickly locate a target log and scroll to view the log context. Added the feature to highlight a number of strings, quickly marking the keywords that users use to search. Added the filter condition feature, allowing users to quickly locate the log where a target character string resides. | [Context Search and Analysis](https://intl.cloud.tencent.com/document/product/614/39795) |

Thank you for your support. We will continue to update features to provide you with better services.
If you have any questions, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).


Regards,

Tencent Cloud Team




