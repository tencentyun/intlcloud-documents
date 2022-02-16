
- [How should I get the definition of the error codes in a response packet?](#42)
- [How does TcaplusDB's optimistic locking work and how to use it?](#44)
- [What are the use cases and precautions for the LIST table?](#45)
- [What is the difference between INSERT, UPDATE and REPLACE?](#46)
- [How do I get the number of records in a table?](#47)
- [Does TcaplusDB support traversal operations?](#48)
- [Does TcaplusDB support updating and obtaining partial fields?](#49)
- [Is TcaplusDB order-preserving for the continuous operations of a single primary key?](#50)
- [Does TcaplusDB support table definition changes?](#51)
- [How do I know whether the packeting of response packet has ended?](#54)
- [What is the difference between GetRecordCount and GetRecordMatchCount?](#55)
- [Does TcaplusDB have a pass-through field?](#56)
- [What is the role of SetResultFlag?](#57)
- [Can I perform increase operations on multiple non-primary key fields at a time? What if the primary key does not exist?](#58)
- [How do I reduce traffic costs when TcaplusDB reads records?](#60)
- [Does TcaplusDB support rollbacks? What is the supported rollback granularity?](#64)
- [How efficient are queries by partial keys (indexes) with TcaplusDB?](#70)
- [What is the timeout mechanism for the TcaplusDB API? What does "it is timeout" error mean?](#75)
- [What are the roles of SendRequest, OnUpdate, and ReceiveResponse functions of TcaplusDB API?](#76)
- [How does TcaplusDB achieve global auto increase of fields?](#77)
- [What rules are defined for queries by partial keys (indexes)?](#78)
- [How do I achieve two-way query of the ID and name of a single table?](#79)
- [Does tcaplus_client support the display of fields at the second nesting level or above?](#83)
- [What should be noted when changing the table in TcaplusDB?](#86)
- [What should be noted when defining the table in TcaplusDB?](#87)

<span id="42"></span>
### How should I get the definition of the error codes in a response packet?
We recommend calling the functions of `TcapErrCode::TcapErrCodeInit` and `TcapErrCode::GetErrStr` in the game server to get error codes, or searching the header files of the TcaplusDB API locally.

<span id="44"></span>
### How does TcaplusDB's optimistic locking work and how to use it?
Let's use the purchase of train tickets as an example:
1. 100 people want to snap up the same train ticket. The recorded version number of the train ticket is 10, and the 100 people use the same recorded version number to snap up the train ticket.
2. 100 people conduct write operations to this ticket. After the write operation is completed, the recorded version number will increase. Therefore, for the operation of a single key, the tcapsvr worker threads are queued. When the first person successfully purchased the ticket, the recorded version number of the train ticket changed to 11, and the recorded version number of the remaining 99 people is still 10.
3. When tcapsvr handles the write requests of the 99 people, an error will occur because the recorded version number at tcapsvr end is inconsistent with the version number in the request. The concurrent principles are as follows:
 - N requests. If only the first request succeeds and the remaining N-1 requests fail, the version protection rules are used.
 - N requests. If all N requests are required to be executed, no version protection rules are required. TcaplusDB operates on the same key.
 
Queue and call the `SetCheckDataVersionPolicy` function, whose values include:
 - `CHECKDATAVERSION_AUTOINCREASE`: the recorded version number is detected, which will only automatically increase if it is the same as the server-side version number.
 - `NOCHECKDATAVERSION_OVERWRITE`: the recorded version number is not detected, and the recorded version number of the client is forcibly written to the server.
 - `NOCHECKDATAVERSION_AUTOINCREASE`: the recorded version number is not detected, and the recorded version number of the server will automatically increase.
 - You are recommended to use the default type `CHECKDATAVERSION_AUTOINCREASE`.

<span id="45"></span>
### What are the use cases and precautions for the LIST table?
Where there is a 1:N use case, when N < 1024, the LIST table is prioritized, such as storing the player's most recent 100 emails, the most recent 100 battle records, and so on. The LIST table supports insertion at the head of the queue and removal at the end of the queue, insertion at the end of the queue and removal at the head of the queue, as well as the Top N operations sorted by insertion time. The number of units under a single key can be increased by modifying the table, because the old data needs to be compatible and cannot be modified to become smaller. You can obtain the total number of records under a single key by using `listgetall`. It is recommended to obtain data according to the offset and limit of a certain threshold that you set. For `listreplace`, `listdelete`, and `listdeletebatch`, you need to specify the correct index. For `listaddafter`, you need to specify the elimination rule when the number of element units under a single key reaches the upper limit. If the `SetListShiftFlag` function are called, the LIST table has two increasing and two obtaining directions. There are 4 possibilities:
1. Query A, B, C, D, E as offset = positive number and limit = 2, and the result is A, B; C, D; E.
2. Query A, B, C, D, E as offset = negative number and limit = 2, and the result is D, E; B, C; A.
3. Query E, D, C, B, A as offset = positive number and limit = 2, and the result is E, D; C, B; A.
4. Query E, D, C, B, A as offset = negative number and limit = 2, and the result is B, A; D, C; E.

In addition, calling `GetRecordMatchCount` can get the total number of records.

<span id="46"></span>
### What is the difference between INSERT, UPDATE and REPLACE?
For INSERT operation, when the key does not exist, an INSERT operation is performed; when the key exists, an error code is returned: `TcapErrCode::SVR_ERR_FAIL_RECORD_EXIST`.
For REPLACE operation, when the key does not exist, an INSERT operation is performed; when the key exists, if the optimistic lock is used, different operations are performed based on the result of the optimistic lock. If the operation is successful, the REPLACE operation is performed, and if it fails, an error code is returned: `TcapErrCode::SVR_ERR_FAIL_INVALID_VERSION;`. If optimistic locking is not used, the REPLACE operation is performed.
For UPDATE operation, when the key exists, if the optimistic lock is used, different operations are performed based on the result of the optimistic lock. If the operation is successful, the UPDATE operation is performed, and if it fails, the error code is returned: `TcapErrCode::SVR_ERR_FAIL_INVALID_VERSION`. If optimistic locking is not used, the UPDATE operation is performed. When the key does not exist, an error code is returned: `TcapErrCode::TXHDB_ERR_RECORD_NOT_EXIST`.

<span id="47"></span>
### How do I get the number of records in a table?
There is a count command word in the TcaplusDB API. If `tcaplus_client` is used, you can use the `count` table name command to get the number of records in the table.

<span id="48"></span>
### Does TcaplusDB support traversal operations?
TcaplusDB supports traversal operations, including traversal operations for GENERIC and LIST tables. You can use the `SetOnlyReadFromSlave(bool flag)` API to traverse the data from the secondary tcapsvr, which will not affect the services provided by the primary tcapsvr.

<span id="49"></span>
### Does TcaplusDB support updating and obtaining partial fields?
TcaplusDB support updating partial fields. When updating and obtaining records, it is recommended to explicitly call API `SetFieldNames(IN const char* field_name[], IN const unsigned field_count)` to determine the fields of this read and write operation, and reduce the network traffic overhead caused by invalid fields.

<span id="50"></span>
### Is TcaplusDB order-preserving for the continuous operations of a single primary key?
For the same game server, the operations of the same primary key are order-preserving, while the operations of different primary keys are not order-preserving. For different game servers, the order is not preserved.

<span id="51"></span>
### Does TcaplusDB support table definition changes?
TcaplusDB supports table definition changes. To add non-primary key fields and change macros, you can just change the table. For more complex changes, you can dynamically change the table structure using data migration and logs. To use this feature, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) and select **Other** on the **Select the related product** page.

<span id="54"></span>
### How do I know whether the packeting of response packet has ended?
For traversal, check whether the traversal ends according to state, that is, the `GetState` API. For the rest of packeting scenarios, check whether the packeting ends according to the `HaveMoreResPkgs` function.

<span id="55"></span>
### What is the difference between GetRecordCount and GetRecordMatchCount?
A request may have N response packets. If there are multiple packets, `GetRecordCount` refers to the number of records in the response packet, and `GetRecordMatchCount` refers to the data records stored at the tcapsvr (storage layer) (total number of records for a single key).

<span id="56"></span>
### Does TcaplusDB have a pass-through field?
The CS protocol of TcaplusDB is divided into two parts: head and body. `UserBuff` (maximum size is 1 KB), `AsyncID` and `Sequence` in head are all pass-through fields. You can use them accordingly.

<span id="57"></span>
### What is the role of SetResultFlag?
When performing write operations, the response packet supports returning records. When performing read operations, calling this function is invalid. The specific values of `result_flag` are as follows:
0: only return whether the operation is successful or not without returning the value field.
1: return data consistent with the request field.
2: return the latest data for all fields of the changed record.
3: return the old data for all fields of the changed record.

The `SetResultFlagForSuccess` API can be used to return the data if the operation succeeds; the `SetResultFlagForFail` API can be used to return the data if the operation fails.

<span id="58"></span>
### Can I perform increase operations on multiple non-primary key fields at a time? What if the primary key does not exist?
To increase multiple non-primary key fields, these fields need to be assigned with values by the request from game server. If one of keys does not exist, you can use the `SetAddableIncreaseFlag` function to perform increase operations. If no key exists, insert a key and then perform increase operations, where the non-increased fields of the key will not be stored and they will take the default value when the record is read. If the key exists, the increase operation can be performed immediately.

<span id="60"></span>
### How do I reduce traffic costs when TcaplusDB reads records?
When TcaplusDB reads a record, it can be set so it does not return the value field if the record has no change in a fixed period of time, neither does it return the value field if the record version number does not change. For more information, see the `SetFlags` function.

<span id="64"></span>
### Does TcaplusDB support rollbacks? What is the supported rollback granularity?
TcaplusDB supports rollbacks, including all-server/all-region rollback, single-table rollback, and can roll back N records from 100 billion records. It also supports cold standby time rollback (most recent 01:05:00 am), precise time rollback (to the second), and fuzzy rollback (you can specify the rollback rules). For speed reference, precise time rollback takes about 2 hours for a rollback of 300 GB data and 200 GB Ulog. The principle of the cold standby time rollback is to replace the engine file. The principle of precise time rollback is to roll back the cold standby engine file + Ulog to the needed time point. A key-based rollback requires you to block these keys first and then unblock them after TcaplusDB has finished the rollback.

<span id="70"></span>
### How efficient are queries by partial keys (indexes) with TcaplusDB?
It is recommended to use queries by partial keys (indexes) in 1:N (N > 1024) app scenarios. The number of primary keys under a single index key is equal to 10 GB/the size of primary key of a single record. A single read-write index operation takes about 100 ms (there are more than 100,000 pieces of data records under a single index key).

<span id="75"></span>
### What is the timeout mechanism for the TcaplusDB API? What does "it is timeout" error mean?
The TcaplusDB API assigns an ID to each request. After it is successfully sent, the ID is pushed into the timeout judgment structure. If the response packet for the request returns, the ID is removed from the structure. If the response packet of the request has not been processed by the application layer within 3 seconds, an error log with the keyword "it is timeout" is printed. You will then need to check whether the game server is blocked. It may be that tcaproxy (access layer) dropped the packets when returning packets to the game server, or the response packet has arrived at the game server, but the game server did not process it in time.
TcaplusDB recommends that you implement the timeout mechanism yourself, which allows you to perform retry and other processes to timeout requests.

<span id="76"></span>
### What are the roles of SendRequest, OnUpdate, and ReceiveResponse functions of TcaplusDB API?
The role of `SendRequest` is to send requests. This request may have been sent to the network, or it may be blocked in the sending channel of the game server and a tcaproxy (access layer). The role of `ReceiveResponse` is to get the response packet from the local receive queue. `OnUpdate` is responsible for sending the requests of the send queue to the network and receiving response packets from the network to the receive queue. In message-driven programming mode, the `OnUpdate` is recommended to be called once every millisecond.

<span id="77"></span>
### How does TcaplusDB achieve global auto increase of fields?
You need to define a single table, and set the field type of a single key and a single value to int64_t (multiple value fields can implement counter arrays). Multiple game servers can increase a single key concurrently (without setting the version protection rules), and get the increase result returned for this operation, then the result of the increase will be a global auto increase.

<span id="78"></span>
### What rules are defined for queries by partial keys (indexes)?
The index key must be a part of the primary key, the index key must contain the shardkey, and the index key cannot be the primary key.

<span id="79"></span>
### How do I achieve two-way query of the ID and name of a single table?
The third key field x is used as the shardkey, and the index is built on ID and x, name and x to achieve this feature. For example, when storing player information, the player's district can be added, that is, the primary key is uin, name, district, and the index key is uin and district, and name and district.

<span id="83"></span>
### Does tcaplus_client support the display of fields at the second nesting level or above?
Yes. You may execute `help select` to see how `select * into a.xml` is used.

<span id="86"></span>
### What should be noted when changing the table in TcaplusDB?
1. You can only add new fields. You cannot modify the type and name of an existing field, or delete an existing field. To modify these, you need to dynamically modify the table structure.
2. The length of an array or string in a non-primary key field can be increased but not reduced. To modify these, you need to dynamically modify the table structure.
3. The version number should be incremented by 1 for each new field, and the version number defined at the top of the XML file should also be incremented by 1 (that is, the version number of the XML file must be the same as that of the new field). The table in TcaplusDB needs to be changed before the table on game server is changed. TcaplusDB supports dynamic table structure modification, and to use this feature, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) and select **Other** on the **Select the related product** page.

<span id="87"></span>
### What should be noted when defining the table in TcaplusDB?
1. The `refer` field needs to be added to the `count` field.
2. The table shardkey should be highly discrete.
3. The index key cannot be the same as the primary key.


