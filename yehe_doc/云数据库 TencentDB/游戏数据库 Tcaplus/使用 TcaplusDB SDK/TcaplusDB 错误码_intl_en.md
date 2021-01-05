| No. | Error Code  | Description                                                         |
| ---- | ------- | ------------------------------------------------------------ |
| 1    | \-1792  | The table is read-only. Please check if the usage of RCUs, WCUs, or storage capacity exceeds the threshold set by users.   |
| 3    | 261     | The record does not exist.                                                 |
| 4    | \-525   | The request for `batchget` timed out.                      |
| 5    | \-781   | The `batchget`, `getbypartkey`, or `listgetall` method returns more response data than the upper limit (i.e., 1 MB). |
| 6    | \-1037  | The system is busy.                                      |
| 7    | \-1293  | The record already exists. Please do not insert it again.                                   |
| 8    | \-1549  | The accessed table field does not exist.                                           |
| 9    | \-2061  | Incorrect table field type                                               |
| 10   | \-3085  | An incorrect field is specified in the `SetFieldName` operation.                             |
| 11   | \-3341  | The field value exceeds the maximum size defined by its type.                               |
| 12   | \-4109  | The subscript of a LIST element is out of range.                                 |
| 14   | \-4621  | The request has no primary key field or index field.                                   |
| 15   | \-6157  | The LIST table has more elements than the defined upper limit. Please enable element removal.                    |
| 16   | \-6925  | Incorrect `result\_flag` setting. Please refer to the `result\_flag` instructions in the SDK.            |
| 17   | \-7949  | Please check the optimistic locking. The requested record version number is inconsistent with the actual record version number.           |
| 18   | \-11277 | The method to manipulate the table does not exist.                                           |
| 19   | \-16141 | Failed to perform the `GetRecord` operation on the Protobuf table.                          |
| 20   | \-16397 | The value of the non-primary key field in the Protobuf table exceeds the maximum size (i.e., 256 KB).                       |
| 21   | \-16653 | Failed to perform the `FieldSetRecord` operation on the Protobuf table.                   |
| 22   | \-16909 | Failed to perform the `FieldIncRecord` operation on the Protobuf table.                     |
| 23   | \-275   | The maximum number of primary key fields has been reached. A GENERIC table can have up to 4 primary key fields, and a LIST table 3.     |
| 24   | \-531   | The maximum number of non-primary key fields has been reached. A GENERIC table can have up to 128 non-primary key fields, and a LIST table 127. |
| 25   | \-787   | The field name exceeds the maximum size (i.e., 32 B).                                  |
| 26   | \-1043  | The field value exceeds the maximum size (i.e., 256 KB).                                    |
| 27   | \-1555  | The data type of the field value is inconsistent with the defined type.                           |
| 28   | \-5395  | The request has no primary key.                                               |
| 29   | \-9235  | The index does not exist.                                                  |
| 30   | \-12307 | Failed to send the request due to network overload.                   |
| 31   | \-12819 | The table does not exist.                                                     |
| 32   | \-13843 | Failed to send the request due to backend network errors.       |
| 33   | \-14099 | The inserted record exceeds the maximum size (1 MB).                                |

