### Segmentation

To search for a long log, you usually only need to search for part of the log content. For example, you need to search for the following complete log that contains `sample`:
```
10.20.20.10;[2018-07-16 13:12:57];GET /online/sample HTTP/1.1;200
```

The full text of the log is long, and the log contains many other characters in addition to `sample`. The complete log and the search condition are not identical. To meet this search requirement, the full text of the log needs to be divided into multiple fragments, and each fragment is called a keyword, and this process is called "segmentation".

For example, we can divide the preceding log based on symbols `@&()='",;:<>[]{}/ \n\t\r` and get the following keywords:
```
10.20.20.10
2018-07-16
13
12
57
GET
online
sample
HTTP
1.1
200
```
During log search, a log containing the keyword `sample` in the search condition is considered an eligible log and is found.

The basis of log segmentation falls into two categories. For configuration details, please see [Configuring Indexes](https://intl.cloud.tencent.com/document/product/614/39594).
- Delimiter: you can customize the symbols for log segmentation, including English symbols and \n\t\r. For example, in the example above, `@&()='",;:<>[]{}/ \n\t\r` are delimiters.
- Allow Chinese Characters: Chinese is special, and Chinese symbols cannot be used as delimiters, and segmentation according only to symbols often fails to achieve the desired effect. For example, if a log is in Chinese, and you want the log to be searched for by a part of content, segmentation according to symbols cannot be used to meet the search requirement. In this case, you can set the log to **Allow Chinese Characters** by referring to [Configuring Indexes](https://intl.cloud.tencent.com/document/product/614/39594) so that CLS will automatically segment every Chinese character into a separate keyword.


### Index

To enable quick log searches, CLS performs a lot of processing, including segmentation, on the logs uploaded to the platform, and this process is called "indexing". Indexes determine the conditions under which logs can be searched and analyzed. Therefore, when uploading log data, you need to set a reasonable index rule for the corresponding log topic to facilitate subsequent search and analysis. For more information, please see [Configuring Indexes](https://intl.cloud.tencent.com/document/product/614/39594).

Index rules take effect only for newly uploaded log data, not historical data. Index creation involves index traffic and index storage, resulting in certain usage costs.
