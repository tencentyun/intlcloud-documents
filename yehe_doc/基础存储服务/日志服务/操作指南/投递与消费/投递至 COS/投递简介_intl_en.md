## Shipping to COS

CLS can ship data in a log topic to COS to meet the needs in the following scenarios:
- Logs are shipped to and stored in COS in STANDARD storage class. If you need other storage classes, perform relevant operations in COS. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/436/30925).
- Log data is processed through offline computing or other computing programs. Such data is shipped to COS first and then loaded by Data Lake Compute (data lake) or EMR (big data platform) for further analysis. For more information, see [Using Data Lake Compute (Hive) to Analyze CLS Log](https://intl.cloud.tencent.com/document/product/614/48461). We recommend you choose CSV or Parquet as the shipping format.

## Billing Description

Log shipping generates private network read traffic fees (cross-region shipping is not supported for now), and CLS will charge fees based on the compression format (Snappy/GZIP/lzop). If your raw log is 100 GB and you choose Snappy for compression, around 50 GB will be billable. As the read traffic price is 0.032 USD/GB, the fees will be 50 GB * 0.032 USD/GB =  1.6 USD.


## Feature Limits

- Historical data cannot be shipped.
- Cross-region shipping is not supported. The log topic and COS bucket must be in the same region.
- Cross-account shipping is not supported.


## Shipping Format

<table>
<thead>
<tr><th style="width: 18%">Data Shipping Format</th><th>Description</th><th>Recommended Scenario</th></tr>
</thead>
<tbody><tr>
<td><a href="https://intl.cloud.tencent.com/document/product/614/31582">CSV shipping</a></td>
<td>Log data is shipped to COS based on the specified separator, such as space, tab, comma, semicolon, and vertical bar.</td>
<td><ul style="margin: 0;"><li>It can be used for computing in Data Lake Compute.</li><li>It can be used to <a href="https://www.tencentcloud.com/document/product/614/31584">ship raw logs</a> (logs collected in a single line, in multiple lines, and with separators).</li></ul></td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/614/31583">JSON shipping</a></td>
<td>Log data is shipped to COS in JSON format.</td>
<td>It is a common data format and can be selected as needed.</td>
</tr>
<tr>
<td><a href="https://www.tencentcloud.com/document/product/614/31584">Parquet shipping</a></td>
<td>Log data is shipped to COS in Parquet format.</td>
<td>Log data needs to be structured data. The data type can be converted (data not collected in a single line or multiple lines). This format is mainly used for Hive batch processing.</td>
</tr>
</tbody></table>


>!
> - After log data is shipped to COS, COS storage fees will be incurred. For billing details, see [Billing Overview](https://intl.cloud.tencent.com/document/product/436/16871).
> - To cleanse the log data before shipping to COS, see [Log Filtering and Distribution](https://intl.cloud.tencent.com/document/product/614/46135).
> 
