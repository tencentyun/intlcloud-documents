## Overview
This command is used to query the Time to Live (TTL) in millisecond of a record. After a record is configured with TTL, you can use `getttl` to query the TTL of its key, that is, how long it is until the key is removed due to expiration. This command can query the TTL of only one record.

## Syntax
```
getttl from [table]  where key1 = 1 and key2 = "abc";
```

## Parameters

| Parameter             | Required | Use Limits                     | Description                            |
| ---------------- | -------- | ---------------------------- | ------------------------------- |
| table            | Yes       | None                           | Table name                            |
| key in the WHERE clause | Yes       | TDR table: all key values are required | Specify the value of a key. Multiple values are separated with `and`. |

## Errors
For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/1016/38791).

## Return Messages

| Situation                                 | Return Message                                                     |
| ---------------------------------------- | ------------------------------------------------------------ |
| The key does not exist or has expired.                     | Record does not exist or has expired\.                       |
| The key exists but its TTL is not specified. | Record exists and no expiration time is set \(permanent\)\.  |
| Failed to query the TTL.                                 | Failed to get time to live\. The error code is \[error code\] and the error message is \[Error message\]\. |
| Queried the TTL successfully.                                 | The time to live is \[TTL\] milliseconds\.                   |


## Sample
Query the TTL of a record:
```
tcaplus> getttl from mails where key1 = 1 and key2 = "abc";
The time to live is 2000 milliseconds.
```
