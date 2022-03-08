### Segmentation

**Segmentation explanation**

To search for a long log, you usually only need to search for part of the log content. Assume that you need to search for the following complete log that contains `sample`:
```
10.20.20.10;[2018-07-16 13:12:57];GET /online/sample HTTP/1.1;200
```

The full text of the log is long, and the log contains many other content in addition to `sample`. The complete log and the search condition are not identical. Therefore, `sample` cannot be used as the search condition to search for the log. To meet this search requirement, the full text of the log needs to be divided into multiple fragments, and each fragment is called a word, and this process is called "segmentation".

For example, the above sample log can be divided based on symbols `@&()='",;:<>[]{}/ \n\t\r`, that is, wherever the symbols occur, segmentation is executed. The segmentation result is as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/4b55099ec50689e3b18308687f14f287.png)

If the search condition is `sample`, the preceding log after segmentation contains `sample` and therefore is considered to meet the search condition.

The search condition itself is also segmented, such as the 3 types of search conditions in the figure below:
![](https://qcloudimg.tencent-cloud.cn/raw/6d5e38901a2c8968c37dcbf03ce84cb9.png)

- Search condition A: `\/online\/login`
  - `\` is used to escape the `/` symbol (this symbol is a reserved symbol of the search syntax and therefore needs to be escaped).
  - The escaped `/` symbol is a delimiter, so the actual search condition is `online OR login`. A log containing `online` **or** `login` is considered to meet the search condition.
  - The example log provided above **meets** the search condition.
- Search condition B: `"/online/login"`
  - Being enclosed by double quotation marks, the `/` symbol does not need to be escaped.
  - The content in the double quotation marks is also divided into two words. However, the double quotation marks indicate that only a log that **contains both the two words in the exact order** as that in the search condition is considered to meet the search condition.
  - The example log provided above does not contain `login` and therefore **does not meet** the search condition.
- Search condition C:`"/online/sample"`
  - The example log provided above contains both `online` and `sample` in the exact order as that in the search condition and therefore is considered to **meet** the search condition.

In most scenarios, if the search condition contains delimiters, you are advised to use double quotation marks to avoid adding escape characters while accurately searching for desired logs. For more information about the search syntax, see [Syntax and Rules](https://intl.cloud.tencent.com/document/product/614/30439).


**Segmentation configuration**

The basis of log segmentation falls into two categories. For configuration details, please see [Configuring Indexes](https://intl.cloud.tencent.com/document/product/614/39594).

- Delimiter: you can customize the symbols for log segmentation, including English symbols and \n\t\r. For example, in the example above, `@&()='",;:<>[]{}/ \n\t\r` are delimiters.
- Allow Chinese Characters: Chinese is special, and Chinese symbols cannot be used as delimiters, and segmentation according only to symbols often fails to achieve the desired effect. For example, if a log in Chinese is ![image](https://qcloudimg.tencent-cloud.cn/raw/def7d19776bcb8374a1bdb7ae61b6304.png) and you want the log to be searched for by ![image](https://qcloudimg.tencent-cloud.cn/raw/917c4c80cb7d962158030240687c3210.png), segmentation according to symbols cannot be used to meet the search requirement. In this case, you can set the log to **Allow Chinese Characters** by referring to [Configuring Indexes](https://intl.cloud.tencent.com/document/product/614/39594) so that CLS will automatically segment every Chinese character into a separate word.


### Index

To enable quick log searches, CLS performs a lot of preprocessing, including segmentation, on the logs uploaded to the platform, and this process is called "indexing". Indexes determine the conditions under which logs can be searched and analyzed. Therefore, before uploading log data, you need to set a reasonable index rule for the corresponding log topic to facilitate subsequent search and analysis. For more information, please see [Configuring Indexes](https://intl.cloud.tencent.com/document/product/614/39594).

Index rules take effect only for newly uploaded log data, not historical data. Index creation involves index traffic and index storage, resulting in certain usage costs.
