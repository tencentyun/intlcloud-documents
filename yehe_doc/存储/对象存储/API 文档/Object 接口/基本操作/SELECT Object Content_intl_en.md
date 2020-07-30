## Overview

This API is used to extract content from the specified object (in CSV or JSON format) using Structured Query Language (SQL) statements. To send this request, you need to specify the content delimiter and use an appropriate SQL function. COS Select will return matched extraction results in a format you specified for you to save.

For more information on COS Select, see COS [SELECT Overview](https://intl.cloud.tencent.com/document/product/436/32472). For more information on the SQL expressions of COS Select, see [SELECT Command](https://intl.cloud.tencent.com/document/product/436/32473) in the Developer Guide.

>!The `Select Object Content` API currently only supports virtual-hosted requests, but not path-style requests.

#### Permission restrictions

To use COS Select, you must have the permission to `cos:GetObject`.

- If you are using a root account, you have the permission by default.
- If you are using a sub-account, contact your root account to get the permission to this operation. For more information on permission settings, see [Granting Sub-accounts Access to COS](https://intl.cloud.tencent.com/document/product/436/11714).

#### Object data format

COS Select supports extracting object data in the following formats:

- CSV: an object is stored in CSV format with its data records separated with a specific delimiter.
- JSON: an object is stored in JSON format, which can be either a JSON file or a JSON list.

> !
> - CSV and JSON objects need to be encoded in UTF-8.
> - COS Select supports extracting CSV and JSON objects compressed by gzip or bzip2.
> - COS Select supports extracting CSV and JSON objects encrypted with SSE-COS.

## Request

#### Sample request

```shell
POST /<ObjectKey>?select&select-type=2 HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: date
Authorization: Auth String

Request body
```

> ?
> - Authorization: Auth String. For more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).
> - The request parameters `select` and `select-type=2` are required, where the former represents the initiation of a select request, and the latter represents the version information of the API.

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

The following request shows how to initiate a COS Select request to extract all the content of a CSV object and save the result as a CSV object. 

```shell
<?xml version="1.0" encoding="UTF-8"?>
<SelectRequest>
    <Expression>Select * from COSObject</Expression>
    <ExpressionType>SQL</ExpressionType>
    <InputSerialization>
        <CompressionType>GZIP</CompressionType>
        <CSV>
            <FileHeaderInfo>IGNORE</FileHeaderInfo>
            <RecordDelimiter>\n</RecordDelimiter>
            <FieldDelimiter>,</FieldDelimiter>
            <QuoteCharacter>"</QuoteCharacter>
            <QuoteEscapeCharacter>"</QuoteEscapeCharacter>
            <Comments>#</Comments>
            <AllowQuotedRecordDelimiter>FALSE</AllowQuotedRecordDelimiter>
        </CSV>
    </InputSerialization>
    <OutputSerialization>
        <CSV>
            <QuoteFields>ASNEEDED</QuoteFields>
            <RecordDelimiter>\n</RecordDelimiter>
            <FieldDelimiter>,</FieldDelimiter>
            <QuoteCharacter>"</QuoteCharacter>
            <QuoteEscapeCharacter>"</QuoteEscapeCharacter>
        </CSV>
    </OutputSerialization>
    <RequestProgress>
        <Enabled>FALSE</Enabled>
    </RequestProgress>
</SelectRequest> 
```

The following request shows how to initiate a COS Select request to extract all the content of a JSON object and save the result as a JSON object.                    

```shell
<?xml version="1.0" encoding="UTF-8"?>
<SelectRequest>
    <Expression>Select * from COSObject</Expression>
    <ExpressionType>SQL</ExpressionType>
    <InputSerialization>
        <CompressionType>GZIP</CompressionType>
        <JSON>
            <Type>DOCUMENT</Type>
        </JSON>
    </InputSerialization>
    <OutputSerialization>
        <JSON>
            <RecordDelimiter>\n</RecordDelimiter>
        </JSON>                                  
    </OutputSerialization>
    <RequestProgress>
        <Enabled>FALSE</Enabled>
    </RequestProgress>                                  
</SelectRequest> 
```

> ?
> - The `InputSerialization` element describes the format of the object to be extracted. It is a required parameter and can be specified in CSV or JSON format.
> - The `OutputSerialization` element describes the format in which the extraction result is saved. This parameter can be specified in CSV or JSON format.
> - The format of the object to be extracted can be different from that in which the extraction result is saved, so you can extract an object in JSON format and save the extraction result in CSV format, and vice versa.

The following table shows the elements in a request body:

| Node Name | Parent Node | Description | Type | Required |
| ------------------- | ------------- | ------------------------------------------------------------ | --------- | -------- |
| Expression | SelectRequest | An SQL expression that represents the extraction operation which you need to initiate, such as `SELECT s._1 FROM COSObject s`. This expression extracts the first column of content from a CSV object. For more information on SQL expressions, see [SELECT Command](https://intl.cloud.tencent.com/document/product/436/32473). | String | Yes |
| ExpressionType | SelectRequest | Expression type, which is an extension. Currently, only SQL expressions and parameters are supported. | String | Yes |
| InputSerialization | SelectRequest | Describes the format of the object to be extracted. | Container | Yes |
| OutputSerialization | SelectRequest | Describes the output format of the extraction result. | Container | Yes |
| RequestProgress | SelectRequest | Indicates whether to return the query progress (QueryProgress). If this parameter is specified, COS Select will periodically return the query progress. | Container | No |

**InputSerialization container element**

| Node Name | Parent Node | Description | Type | Required |
| --------------- | ------------------ | ------------------------------------------------------------ | --------- | ---------------------------- |
| CompressionType | InputSerialization | Describes the compression format of the object to be extracted: <br><li>`NONE` (default): the object has not been compressed.<br><li>`GZIP` or `BZIP2`: the object has been compressed. | String | No |
| CSV/JSON | InputSerialization | Describes the required file parameters for an object format. For example, for CSV format, the delimiter needs to be specified. | Container | Yes<br>CSV or JSON |

**CSV container element (`InputSerialization` sub-element)**

| Node Name | Parent Node | Description | Type | Required |
| -------------------------- | ------ | ------------------------------------------------------------ | ------- | -------- |
| RecordDelimiter | CSV | A character that separates the data records in a CSV object into different rows, which is `\n` by default. You can specify any octal character such as a comma, semicolon, and tab. This parameter supports up to 2 bytes, i.e., you can enter a delimiter in the format of `\r\n`. Default value: `\n `. | String | No |
| FieldDelimiter | CSV | Specifies the character separating rows in a CSV object, which is `, ` by default. You can specify any octal character. This parameter supports up to 1 byte. | String | No |
| QuoteCharacter | CSV | If there is a string in the CSV object to be extracted that contains delimiters, you can use `QuoteCharacter` to escape it so as to prevent it from being cut into several parts. For example, if there is a string `"a, b"` in the CSV object, double quotation mark `"` can prevent this string from being separated into two characters (`a` and `b`). Default value: `"`. | String | No |
| QuoteEscapeCharacter | CSV | If the string to be extracted contains `"`, then you need to use `"` to escape it properly. For example, your string `""" a , b """` will be parsed as `" a , b  "`. Default value: `"`. | String | No |
| AllowQuotedRecordDelimiter | CSV | Specifies whether the object to be extracted contains any character that is the same as the delimiter and needs to be escaped using `"`. When this parameter is set to TRUE, COS Select will escape the character during extraction, which will result in a decrease in the extraction performance. When it is set to FALSE, no escaping will be performed. Default value: FALSE. | Boolean | No |
| FileHeaderInfo | CSV | Indicates whether the object to be extracted contains a column header. Valid values: NONE, USE, IGNORE. NONE indicates that the object contains no column headers, USE indicates that the object contains a column header which you can use for extraction (such as `SELECT "name" FROM COSObject`), and IGNORE indicates that the object contains a column header which you can, but do not intend to use for extraction (such as `SELECT s._1 FROM COSObject s`). | Enum | No |
| Comments | CSV | A character which indicates a record is a comment line. It is added to the beginning of a record. Once added, COS Select will not perform any analysis on the record. Default value: `#`. | String | No |

**JSON container element (`InputSerialization` sub-element)**

| Node Name | Parent Node | Description | Type | Required |
| ---- | ------ | ------------------------------------------------------------ | ---- | -------- |
| Type | JSON | JSON file type:<br><li>`DOCUMENT` indicates that the JSON file contains only an independent JSON object which can be cut into multiple rows.<br><li>`LINES` indicates that each row in the JSON object contains an independent JSON object.<br>Valid values: DOCUMENT, LINES | Enum | Yes |

**OutputSerialization container element**

| Node Name | Parent Node | Description | Type | Required |
| --------- | ------------------- | ------------------------------------------------- | --------- | --------------------------------- |
| CSV/JSON | OutputSerialization | Specifies the output format of the extraction result. Value range: CSV, JSON | Container | Yes, which must be CSV or JSON |

**CSV container element (`OutputSerialization` sub-element)**

| Node Name | Parent Node | Description | Type | Required |
| -------------------- | ------ | ------------------------------------------------------------ | ------ | -------- |
| QuoteFields | CSV | Specifies whether the output result needs to be escaped with `"` if it is a file. Valid values: ALWAYS, ASNEEDED. ALWAYS indicates applying `"` to all the output extracted files, and ASNEEDED indicates using it only when needed. Default value: ASNEEDED. | String | Yes |
| RecordDelimiter | CSV | A character that separates the data records in the output result into different rows, which is `\n` by default. You can specify any octal character such as a comma, semicolon, and tab. This parameter supports up to 2 bytes, i.e., you can enter a delimiter in the format of `\r\n`. Default value: `\n `. | String | No |
| FieldDelimiter | CSV | A character that separates each row in the output result into different columns. You can specify any octal character. This parameter supports up to 1 byte. Default value: `,`. | String | No |
| QuoteCharacter | CSV | If there is a string that contains delimiters in the output result, you can use `QuoteCharacter` to escape it so as to ensure that the string will not be cut in subsequent analysis. For example, if there is a string `a, b` in the output result, double quotation mark `"` can prevent this string from being separated into two characters (`a` and `b`), and COS Select will convert it to `"a, b"` to be written to the file. Default value: `" `. | String | No |
| QuoteEscapeCharacter | CSV | If the string to be output contains `"`, then you need to use `"` to escape it so as to ensure that the string can be escaped normally. For example, your string `" a , b"` will be converted to `""" a , b """` when written to the file. Default value: `" `. | String | No |

**JSON container element (`OutputSerialization` sub-element)**

| Node Name | Parent Node | Description | Type | Required |
| --------------- | ------ | ------------------------------------------------------------ | ------ | -------- |
| RecordDelimiter | JSON | A character that separates the data records in the output result into different rows, which is `\n` by default. You can specify any octal character such as a comma, semicolon, and tab. This parameter supports up to 2 bytes, i.e., you can enter a delimiter in the format of `\r\n`. Default value: `\n `. | String | No |

**RequestProgress container element**

| Node Name | Parent Node | Description | Type | Required |
| ------- | --------------- | ---------------------------------------------------------- | ------- | -------- |
| Enabled | RequestProgress | Specifies whether COS Select should periodically return the query progress information. Default value: FALSE | Boolean | No |

## Response

A successful extraction operation will return a `200 OK` status code.

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

As the size of the response body is unpredictable, COS presents the response body in serialized form, i.e., dividing it into multiple parts to be returned, as shown below:

```shell
<Message 1>
<Message 2>
<Message 3>
......
<Message n>
```

#### Pre-response (Prelude) and response result (Data)

COS cuts a extraction result into multiple parts, each of which is a message. Each message consists the pre-response (prelude) and response result (data).

- The prelude consists of two parts:
 - Total length of the message.
  - Total length of all headers.
- The data consists of two parts:
  - Headers.
  - Payload.

Both the prelude and data end with a 4-byte CRC code encoded in Big Endian. COS Select uses CRC32 to calculate the CRC code. For more information on CRC32, see the [RFC documentation](https://www.ietf.org/rfc/rfc1952.txt). In addition to data, COS Select additionally spends a total of 16 bytes in transferring the prelude and code.

> !The integer values in all the messages are transferred in network byte order (i.e., encoded in Big Endian).

The figure below shows what a message and a header consist of. One message may contain multiple headers.
![Message construction](https://main.qcloudimg.com/raw/854fe989e1f98b168a038b4fb615d4e5.png)

As shown above, each message consists of a prelude, a prelude CRC code (composed of two pieces of information that record the number of bytes), header(s), a payload, and a message CRC code. As can be seen from the above figure, the length of the entire response body is calculated as follows:
```
Total length of a response body = Length of the prelude + length of the prelude CRC code + length of the payload + length of the header(s) + length of the message CRC code
```

As the total length of the prelude, the prelude CRC code and the message CRC code is always 16 bytes, the total length of the response body can also be quickly calculated as follows:
```
Total length of a response body = Length of the payload + length of the header(s) + 16
```

The following describes the components of the response body in detail:

| Component &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;| Description |
| ------------------------- | ------------------------------------------------------------ |
| prelude | Records the total length of each message and the total length of all headers separately. Each record is of 4 bytes, and the total length is 8 bytes: <br>1. `total byte-length`: the total length of the message, which is encoded in Big Endian and of 4 bytes in total with the capacity of the record itself included. <br>2. `headers byte-length`: the total length of all headers, which is encoded in Big Endian and of 4 bytes in total with the capacity occupied by the record excluded. |
| prelude CRC | A prelude CRC is encoded in Big Endian and contains a total of 4 bytes. It helps the program quickly determine whether the prelude information is correct so as to reduce blocking during buffering. |
| header | Metadata of the extraction result recorded by the message, such as data type and body format. The length of this part in bytes varies by data type. A header is stored as a key-value (KV) pair and encoded in UTF-8. The metadata recorded in a header can be displayed in any order, but each metadata entry is recorded only once. Depending on the data type, the following headers may appear in the result returned by COS Select:<br>1. `MessageType Header`: this header represent the response type, where the key is ":message-type" and the value can be "error" or "event". "error" indicates that this record is an error message, and "event" indicates that this record is a specific event.<br>2. `EventType Header`: this header records the event type, where the key is ":event-type" and the value can be "Records", "Cont", "Progress", "Stats" or "End". "Records" indicates that the event is the returned extraction record, "Cont" the TCP connection hold, "Progress" the periodically returned extraction result, "Stats" the statistics of the query, and "End" the end of query.<br>3. `ErrorCode Header`: this header records the error code, where the key is ":error-code" and the value can be an error code listed in [Special Error Codes](#.E7.89.B9.E6.AE.8A.E9.94.99.E8.AF.AF.E7.A0.81).<br>4. `ErrorMessage Header`: this header records the error message, where the key is ":error-message" and the value can be an error message returned by the server, which can be used to locate the error. |
| Payload | Records the extraction result or useful information related to the request. |
| Message CRC | CRC code encoded in Big Endian containing a total of 4 bytes. |

A message may record multiple headers, and each header consists of the following parts:

| Component | Description |
| ------------------------ | ------------------------------------------------------------ |
| Header Name Byte-Length | Records the length of the header name in bytes |
| Header Name | Header type. Valid values: ":message-type", ":event-type", ":error-code", ":error-message".<br><li>":message-type" indicates that the header records the response type.<br><li>":event-type" indicates that the header records the event type<br><li>":error-code" indicates that the header records the error code <br><li>":error-message" indicates that the header records the error message. |
| Header Value Type | Type of the header value, which is always 7 for COS Select, indicating that the type is String |
| Value String Byte-Length | Length of the header value in bytes, which is always 2 bytes |
| Header Value String | Body of the header, i.e., the metadata of the payload, where the length of the header value in bytes depends on the response type |

COS Select supports the following response types:

| Response Type | Description |
| ------------------------- | ------------------------------------------------------------ |
| Records message | An extraction record message, which can contain a single record, a partial record, or multiple records, depending on the number of extraction results. A response body may contain multiple records messages |
| Continuation message | A connection continuation message that is sent by COS Select periodically to maintain the TCP connection and appears randomly in the response body. It is recommended to make your client able to automatically identify this type of messages and filter them out so as to avoid smudging the extraction results |
| Progress message | A progress message returned by COS Select periodically to indicate the current query progress |
| Stats message | A statistics message about the query returned by COS Select after the query ends |
| End message | An end message indicating that the query has ended and there is no subsequent response data. The query can be considered to have ended only when a message of this type is received |
| RequestLevelError message | An error message which will be returned by COS Select when an error occurs during the query process and contains the cause of the error. If COS Select returns this message, it will not return an end message |

These response types are as detailed below.

#### Records message

- Header format
  A records message contains three types of headers: ":message-type", ":event-type", and ":content-type", as shown below:
  ![Records message](https://main.qcloudimg.com/raw/7e04ad30a1ce335a67975a291bffdac5.png) 
- Body format
  The body of a records message may contain a single record, a partial record, or multiple records, depending on the number of extraction results.

#### Continuation Message

- Header format
  A continuation message contains two types of headers: ":message-type" and ":event-type", as shown below:
  ![ Continuation Message ](https://main.qcloudimg.com/raw/b8488620e8f2989f993e9b5488dfe52b.png) 
- Body format
  A continuation message contains no body content.

#### Progress Message

- Header format
  A progress message contains three types of headers: ":message-type", ":event-type", and ":content-type", as shown below:
  ![Progress Message](https://main.qcloudimg.com/raw/6f262224260381b3c7b233b25ce0fbb0.png) 
- Body format
  The body of a progress message is XML text which contains the current query progress, mainly including:
	- BytesScanned: if the file is compressed, this value represents the size of the file in bytes before it is decompressed; otherwise, this value represents the size of the file in bytes.
	- BytesProcessed: if the file is compressed, this value represents the size of the file in bytes after it is decompressed; otherwise, this value represents the size of the file in bytes.
	- BytesReturned: size of the extraction result currently returned by COS Select in bytes.

Below is a sample:

```shell
<?xml version="1.0" encoding="UTF-8"?>
<Progress>
     <BytesScanned>512</BytesScanned>
     <BytesProcessed>1024</BytesProcessed>
     <BytesReturned>1024</BytesReturned>
</Progress>
```

#### Stats Message

- Header format
  A stats message contains three types of headers: ":message-type", ":event-type", and ":content-type", as shown below:
  ![Stats Message](https://main.qcloudimg.com/raw/8fbe1d40ec19c4f72d18275ff087f264.png)
- Body format
  The body of a stats message is XML text which contains the statistics of the current query, mainly including:
  - BytesScanned: if the file is compressed, this value represents the size of the file in bytes before it is decompressed; otherwise, this value represents the size of the file in bytes.
  - BytesProcessed: if the file is compressed, this value represents the size of the file in bytes after it is decompressed; otherwise, this value represents the size of the file in bytes.
  - BytesReturned: size of the extraction result returned by COS Select in the query in bytes.

Below is a sample:

```shell
<?xml version="1.0" encoding="UTF-8"?>
<Stats>
     <BytesScanned>512</BytesScanned>
     <BytesProcessed>1024</BytesProcessed>
     <BytesReturned>1024</BytesReturned>
</Stats>
```

#### End Message

- Header format
  An end message contains two types of headers: ":message-type" and ":event-type", as shown below:
  ![End messages](https://main.qcloudimg.com/raw/f28f76c719b02258379adf1fcc71f484.png)
- Body format
  An end message contains no body content.

#### Request Level Error Message

- Header format
  A request level error message contains three types of headers: ":error-code", ":error-message", and ":message-type", as shown below:
  ![Request Level Error Message](https://main.qcloudimg.com/raw/72fc70c4cabbc86b67d1cf8cc46a8d70.png) 

For more information on the error code in a request level error message, see [Special Error Codes](#.E7.89.B9.E6.AE.8A.E9.94.99.E8.AF.AF.E7.A0.81).

- Body format
  A request level error message contains no body content.

<span id="errorcode"></span>
#### Special error codes

For common errors related to this request, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). The following describes special error codes:                     

| Error Code | Error Message | Description | HTTP Status Code |
| -- | -- | -- | -- |
| InvalidXML | The XML is invalid | The XML format is invalid. | 400 Bad Request |
| MissingRequiredParameter | The SelectRequest entity is missing a required parameter | A required parameter is missing in the extraction request. | 400 Bad Request |
| MissingExpectedExpression | The SQL expression is missing | An SQL expression is missing. | 400 Bad Request |
| MissingInputSerialization | The input serialization is missing | No data serialization format of the input CSV object is specified. | 400 Bad Request |
| InvalidCompressionFormat | The file is not in a supported compression format. Only GZIP and BZIP2 are supported | The file is in an invalid compression format. Only gzip and bzip2 are supported. | 400 Bad Request |
| MissingInputFormat | The input format is missing | The input format is missing. | 400 Bad Request |
| InvalidFileHeaderInfo | The input FileHeaderInfo is invalid. Only NONE, USE, and IGNORE are supported| The input file header information is invalid. Only NONE, USE, and IGNORE are supported. | 400 Bad Request |
| InvalidRequestParameter | The input RecordDelimiter of CSV is invalid | The record delimiter of the input CSV file is invalid. | 400 Bad Request |
| InvalidRequestParameter | The input FieldDelimiter of CSV is invalid | The field delimiter of the input CSV file is invalid. | 400 Bad Request |
| InvalidRequestParameter | The input QuoteCharacter of CSV is invalid | The quote character of the input CSV file is invalid. | 400 Bad Request |
| InvalidRequestParameter | The input AllowQuoteRecordDelimiter of CSV is invalid. Only TRUE and FALSE are supported | The configuration for enabling the escape character in the input CSV file is invalid. Only TRUE and FALSE are supported. | 400 Bad Request |
| InvalidJsonType | The JsonType is invalid. Only DOCUMENT and LINES are supported | The JSON type is invalid. Only DOCUMENT and LINES are supported. | 400 Bad Request |
| MissingOutputSerialization | The output serialization is missing. | No data serialization format of the output CSV object is specified. | 400 Bad Request |
| MissingOutputFormat | The output format is missing | The output format is missing. | 400 Bad Request |
| InvalidQuoteFields | The QuoteFields is invalid. Only ALWAYS and ASNEEDED are supported | The escaping rule is invalid. Only ALWAYS and ASNEEDED are supported. | 400 Bad Request |
| InvalidRequestParameter | The output RecordDelimiter of CSV is invalid | The record delimiter of the output CSV file is invalid. | 400 Bad Request |
| InvalidRequestParameter | The output FieldDelimiter of CSV is invalid | The field delimiter of the output CSV file is invalid. | 400 Bad Request |
| InvalidRequestParameter | The output QuoteCharacter of CSV is invalid | The escape character of the output CSV file is invalid. | 400 Bad Request |
| InvalidRequestParameter | The output QuoteEscapeCharacter of CSV is invalid | The double quotation mark escape character of the output CSV file is invalid. | 400 Bad Request |
| InvalidRequestParameter | The output RecordDelimiter of JSON is invalid | The record delimiter of the output JSON file is invalid. | 400 Bad Request |
| SQLParsingError | Encountered an error parsing the SQL expression | An error occurred when parsing the SQL expression. | 400 Bad Request |
| SQLParsingError | Other expressions are not allowed in the SELECT list when '\*' is used without dot notation. | The SELECT list does not allow `'*'` to be used without dot notation. | 400 Bad Request |
| SQLParsingError | The SQL expression contains an empty SELECT | The SQL expression contains an empty SELECT clause. | 400 Bad Request |
| SQLParsingError | GROUP is not supported in the SQL expression | The GROUP clause is not supported in the SQL expression. | 400 Bad Request |
| SQLParsingError | UNION is not supported in the SQL expression | The UNION clause is not supported in the SQL expression. | 400 Bad Request |
| SQLParsingError | FROM is missing in the SQL expression | The FROM clause is missing in the SQL expression. | 400 Bad Request |
| SQLParsingError | ORDER is not supported in the SQL expression | The ORDER clause is not supported in the SQL expression. | 400 Bad Request |
| SQLParsingError | The column index is invalid in the SQL expression | The column index specified in the SQL expression is invalid. | 400 Bad Request |
| SQLParsingError | The table alias is invalid in WHERE | The table alias in the WHERE clause is invalid. | 400 Bad Request |
| Bzip2DecompressError | Encountered an error decompressing the bzip2 file | An error occurred when decompressing the bzip2 file. | 400 Bad Request |
| Bzip2DecompressError | BZIP2 is not applicable to the queried object | The bzip2 format is not applicable to decompressing the object to be queried. | 400 Bad Request |
| GzipDecompressError | Encountered an error decompressing the gzip file | An error occurred when decompressing the gzip file. | 400 Bad Request |
| GzipDecompressError | GZIP is not applicable to the queried object | The gzip format is not applicable to decompressing the object to be queried. | 400 Bad Request |
| Busy | The service is busy. Please retry later | The backend service is busy. Please retry later. | 400 Bad Request |
| Overload | The service is overload. Please retry later | The backend service is overloaded. Please retry later. | 400 Bad Request |
| AmbiguousFieldName | Field name matches to multiple fields in the file | The specified header name has multiple identical values. | 400 Bad Request |
| ComparisonFailed | Attempt to compare failed | The attempt to compare failed. Please retry. | 400 Bad Request |
| CastFailed | Attempt to convert from one data type to another using CAST failed in the SQL expression. | The attempt to convert from one data type to another using the CAST function failed in the SQL expression. | 400 Bad Request |
| OverMaxRecordSize | The length of a record in the input or result is greater than maxCharsPerRecord of 1 MB | The size of a record in the input or output exceeds the limit of 1 MB. | 400 Bad Request |
| LastRecordParseFail | Please check the last record in the input | Please check the last record in the input file. | 400 Bad Request |
| CSVParsingError | Encountered an error parsing the CSV file | An error occurred when parsing the CSV file. | 400 Bad Request |
| JSONParsingError | Encountered an error parsing the JSON file | An error occurred when parsing the JSON file. | 400 Bad Request |
| ErrorWritingRow | Encountered an error parsing the SELECT result. Please try again | Unable to format your query result. Please check the file and retry. | 400 Bad Request |
| InvalidRequestParameter | The input Comment of CSV is invalid | The comment of the CSV file is invalid. | 400 Bad Request |
| InvalidTextEncoding | UTF-8 encoding is required. Please check the file and try again. | The file and the result can only be encoded in UTF-8. | 400 Bad Request |
| NoSuchKey | The specified key does not exist | The specified object key does not exist. | 404 Not Found |
| AccessDenied | Access Denied| Access denied due to incorrect signature or permission | 403 Forbidden |
| MethodNotAllowed | The specified method is not allowed against this resource | The current resource does not support the HTTP method. | 405 Method Not Allowed |
| InternalError | We encountered an internal error. Please try again | The server encountered an internal error. | 500 Internal Server |



## Samples

#### Sample 1. Extracting content from an object in CSV format

The following sample shows how to call this API to extract all the content from a CSV object and output the extraction result in CSV format. The object to be extracted is named `exampleobject.csv` and stored in the bucket examplebucket-1250000000 in Beijing (ap-beijing).

```shell
POST /exampleobject.csv?select&select-type=2 HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Tue, 12 Jan 2019 11:49:52 GMT
Authorization: authorization string
Content-Length: content length

<?xml version="1.0" encoding="UTF-8"?>
<SelectRequest>
    <Expression>Select * from COSObject</Expression>
    <ExpressionType>SQL</ExpressionType>
    <InputSerialization>
        <CompressionType>None</CompressionType>
        <CSV>
            <FileHeaderInfo>IGNORE</FileHeaderInfo>
            <RecordDelimiter>\n</RecordDelimiter>
            <FieldDelimiter>,</FieldDelimiter>
            <QuoteCharacter>"</QuoteCharacter>
            <QuoteEscapeCharacter>"</QuoteEscapeCharacter>
            <Comments>#</Comments>
        </CSV>
    </InputSerialization>
    <OutputSerialization>
        <CSV>
            <QuoteFields>ASNEEDED</QuoteFields>
            <RecordDelimiter>\n</RecordDelimiter>
            <FieldDelimiter>,</FieldDelimiter>
            <QuoteCharacter>"</QuoteCharacter>
            <QuoteEscapeCharacter>"</QuoteEscapeCharacter>
        </CSV>                               
    </OutputSerialization>
</SelectRequest> 
```

If you need to execute different extraction commands, you can modify the SQL command in the `Expression` element. For more information on commands, see [SELECT Command](https://intl.cloud.tencent.com/document/product/436/32473). Some common extraction scenarios are described below.

- Suppose that you use a column index to filter the content of an object. You can use `s._n` to filter out the data in the `n` column, with the minimum value of `n` being 1. The following command will filter out the records in column 3 with a value greater than 100 from the object and return columns 1 and 2 of those records: 
```shell
SELECT s._1, s._2 FROM COSObject s WHERE s._3 > 100
```

- If your CSV object has a column header and you want to filter the content of the object using the name of the header (by setting `FileHeaderInfo` to `Use`), you can use `s.name` for indexing. The following command will filter out records with a header named `Id` or `FirstName`:
```shell
SELECT s.Id, s.FirstName FROM COSObject s
```

- You can also specify a function in the SQL expression. The following command will count the number of records in the first column that are smaller than 1:
```shell
SELECT count(*) FROM COSObject s WHERE s._1 < 1
```

The following is a sample response:

```shell
HTTP/1.1 200 OK
x-cos-id-2: cos_id_demo
x-cos-request-id: cos_request_id_demo
Date: Tue, 12 Jan 2019 11:50:29 GMT

A series of messages
```

#### Sample 2. Extracting content from an object in JSON format

The following sample shows how to call this API to extract all the content from a JSON object and output the extraction result in CSV format. The object to be extracted is named `exampleobject.json` and stored in the bucket examplebucket-1250000000 in Beijing (ap-beijing).

```shell
POST /exampleobject.json?select&select-type=2 HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Tue, 12 Jan 2019 11:52:29 GMT
Authorization: authorization string
Content-Length: content length

<?xml version="1.0" encoding="UTF-8"?>
<SelectRequest>
    <Expression>Select * from COSObject</Expression>
    <ExpressionType>SQL</ExpressionType>
    <InputSerialization>
        <CompressionType>NONE</CompressionType>
        <JSON>
            <Type>DOCUMENT</Type>
        </JSON>
    </InputSerialization>
    <OutputSerialization>
        <CSV>
            <QuoteFields>ASNEEDED</QuoteFields>
            <RecordDelimiter>\n</RecordDelimiter>
            <FieldDelimiter>,</FieldDelimiter>
            <QuoteCharacter>"</QuoteCharacter>
            <QuoteEscapeCharacter>"</QuoteEscapeCharacter>
        </CSV>                               
    </OutputSerialization>
</SelectRequest> 
```

Similarly, you can also perform different extraction commands on JSON objects by modifying the SQL command in the `Expression` element. For more information on commands, see [SELECT Command](https://intl.cloud.tencent.com/document/product/436/32473). Some common extraction scenarios are described below.

- You can extract data using the JSON attribute name. The following command will filter out records whose `city` value is Seattle from the object and return the `country` and `city` information of those records:
```shell
SELECT s.country, s.city from COSObject s where s.city = 'Seattle'
```

- You can also specify a function in the SQL expression. The following command will count the total number of records in the JSON object:
```shell
SELECT count(*) FROM COSObject s
```

## Notes

Unlike the [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) API, SELECT Object Content does not support the following features:

- Returning a part of an object: you cannot use parameters such as `Range` to specify a part of an object to return.
- Manipulating archived objects (in ARCHIVE storage class). COS Select cannot directly manipulate archived objects. To do so, you need to retrieve the data first.
