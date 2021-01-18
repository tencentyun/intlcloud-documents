As the basic data unit in CLS, a log group (LogGroup) is a collection of multiple logs. In the process of log upload and consumption, to increase the read/write efficiency and alleviate the pressure, multiple logs can be packaged into one log group and then sent to CLS.

Logs in the same log group have the same meta information (\_\_FILENAME__, \_\_SOURCE\_\_, \_\_LogTag\_\_, etc.). For more information, please see the CLS Protobuf data format in [Uploading Structured Log](https://intl.cloud.tencent.com/document/product/614/16873).

Limits:

- One [log group](https://intl.cloud.tencent.com/document/product/614/16873) data packet can contain 1–10,000 logs.
-  The total size of all values in one log group cannot exceed 5 MB.

  

  

