## Overview
This command is used to set a time to live (TTL) in millisecond for a record. The set value will be reduced by the elapsed time. When the TTL value of a record is equal to 0, TcaplusDB will remove it. This command only takes effect on a single record.

## Syntax
```
setttl [table] ttl=[TTL] where key1 = 1 and key2 = "abc";
```

## Parameters

| Parameter             | Required | Limit                                                   | Description                            |
| ---------------- | -------- | ------------------------------------------------------------ |------------------------------- |
| table            | Yes       | No                                                       | Table name                            |
| TTL              | Yes       | The value cannot exceed half of the maximum value of `uint64\_t`. In other words, the maximum TTL value is ULONG\_MAX/2. A value exceeded this limit will be set to the maximum value.    | Time to live in millisecond          |
| Key in the WHERE clause | Yes       | All key values are required for TDR table.      | Key values need to be declared. Multiple key values are joined with `and`.  |

## Errors
For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/1016/38791).


## Return Messages

| Situation             | Return Message                                                   |
| -------------------- | ------------------------------------------------------------ |
| The record does not exist or has expired. | Record does not exist or has expired\.                       |
| Failed to set time to live.            | Failed to set time to live\. The error code is \[error code\] and the error message is \[Error message\]\. |
| Set time to live successfully.            | Set time to live successfully\.                              |


## Sample
Set TTL to 2,000 milliseconds:
```
tcaplus> setttl mails ttl=2000 where key1 = 1 and key2 = "abc";
Set time to live successfully.
```
