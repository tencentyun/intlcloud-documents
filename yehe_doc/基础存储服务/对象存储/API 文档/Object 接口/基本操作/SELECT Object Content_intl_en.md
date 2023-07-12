## Overview

This API is used to extract content from a CSV/JSON/Parquet object with Structured Query Language (SQL) statements. During the extraction process, you need to specify the content delimiter and use an appropriate SQL function. COS Select will return the matching extraction result, and you can specify a format to save the result.

For more information about COS Select, please see [COS Select Overview](https://intl.cloud.tencent.com/document/product/436/32472). You can also see [SELECT Command](https://intl.cloud.tencent.com/document/product/436/32473) in Developer Guide to learn about the SQL expressions for COS Select.

>!Currently, this API (`Select Object Content`) supports only virtual-hosted-style requests, but not path-style requests.

#### Permission restrictions

To use COS Select, you must have the `cos:GetObject` permission.

- The root account has this permission by default.
- Sub-accounts need to contact the root account for permission. For more information about permission settings, please see [Granting Sub-accounts Access to COS](https://intl.cloud.tencent.com/document/product/436/11714).

#### Object formats

COS Select supports extracting content from objects in the following formats:

- CSV: The object’s data records are separated by a specific delimiter.
- JSON: either a JSON file or a JSON list
- Parquet: It can contain nested structures.

> !
>- To use COS Select, the object must be UTF-8 encoded.
>- COS Select supports extracting CSV or JSON objects that are compressed with GZIP or bzip2, and Parquet objects that are compressed with GZIP or Snappy.
>- COS Select supports extracting data from objects encrypted with SSE-COS.

## Requests

#### Sample request

```shell
POST /<ObjectKey>?select&select-type=2 HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: date
Authorization: Auth String

Request body
```

>?
> - In `Host: <BucketName-APPID>.cos.<Region>.myqcloud.com`, <BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and <Region> is a COS region (see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224)).
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
> - The request parameters `select` and `select-type=2` are required, where the former represents a select request and the latter represents the version of this API.
> 

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

The following COS Select request extracts all content of a CSV object and saves the result in CSV format: 

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

The following COS Select request extracts all content of a JSON object and saves the result in JSON format:                    

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

The following COS Select request extracts all content of a Parquet object and saves the result in JSON format:

```shell
<?xml version="1.0" encoding="UTF-8"?>
<SelectRequest>
    <Expression>Select * from COSObject</Expression>
    <ExpressionType>SQL</ExpressionType>
    <InputSerialization>
        <CompressionType>GZIP</CompressionType>
        <Parquet>
        </Parquet>
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





>?
>- `InputSerialization` (required) specifies the format of the object to extract. It can be set to `CSV`, `JSON`, or `Parquet`.
>- `OutputSerialization` specifies the format to save the extraction result. It can be set to `CSV` or `JSON`.
>- The formats of the object to extract and the extraction result do not need to be the same. For example, you may extract data from a JSON object and save the extraction result in CSV format.

The following table describes all nodes in the request body:

| Node Name | Parent Node | Description | Type | Required |
| ------------------- | ------------- | ------------------------------------------------------------ | --------- | -------- |
| Expression | SelectRequest | An SQL expression for the extraction. For example, `SELECT s._1 FROM COSObject s` extracts the first column of data from a CSV object. For more information about SQL expressions, please see [SELECT Command](https://intl.cloud.tencent.com/document/product/436/32473). | String | Yes |
| ExpressionType | SelectRequest | Expression type. This parameter is an extension. Currently, only SQL expressions and parameters are supported. | String | Yes |
| InputSerialization | SelectRequest | Format of the object to extract | Container | Yes |
| OutputSerialization | SelectRequest | Format to save the extraction result | Container | Yes |
| RequestProgress | SelectRequest | Whether to return the query progress (`QueryProgress`). If this feature is enabled, COS Select will return the query progress periodically. | Container | No |


**Content of `InputSerialization`**

| Node Name | Parent Node | Description | Type | Required |
| :--------------- | :----------------- | :----------------------------------------------------------- | :-------- | :------- |
| CompressionType | InputSerialization | Compression type of the object to extract. If the object is not compressed, set this parameter to `NONE` (default). Otherwise, set it to `GZIP` or `BZIP2`, which are the only two compression types supported by COS Select. | String | No |
| CSV/JSON/PARQUET | InputSerialization | Parameters required for each object format. For example, if the object format is CSV, the delimiter needs to be specified. | Container | Yes |

**Content of `CSV` (a subnode of `InputSerialization`)**

| Node Name | Parent Node | Description | Type | Required |
| -------------------------- | ------ | ------------------------------------------------------------ | ------- | -------- |
| RecordDelimiter | CSV | A delimiter that separates data records of the CSV object into multiple rows. You can set this parameter to any octal character such as a comma (,), semicolon (:), or tab. The delimiter can be up to 2 bytes, which means that delimiters such as `\r\n` are supported. Default value: `\n` | String | No |
| FieldDelimiter | CSV | A delimiter that separates data records into multiple columns for each row. You can set this parameter to any octal character. This parameter can be up to 1 byte. Default value: `,` | String | No |
| QuoteCharacter | CSV | If a string in the CSV object to extract contains delimiters, you can use this parameter as the escape so that the string will not be interpreted as several parts. The default value is `"`. For example, if the object contains the string `"a, b"`, the double quotation marks can prevent the string from being interpreted as two separate characters `a` and `b`. | String | No |
| QuoteEscapeCharacter | CSV | If the string to extract contains `"`, use another `"` as the escape so that the string can be interpreted. For example, the string `""" a , b """` will be parsed as `" a , b "`. Default value: `"` | String | No |
| AllowQuotedRecordDelimiter | CSV | Whether the object contains characters that are identical with the delimiter and need to be escaped with `"` <br>`TRUE`: yes (compromises extraction performance) <br>`FALSE` (default): no | Boolean | No |
| FileHeaderInfo | CSV | Whether the object to extract contains a column header. Valid values: <br>`NONE`: no <br> `USE`: yes, and you want to use it for extraction (example: `SELECT "name" FROM COSObject`) <br>`IGNORE`: yes, but you don’t want to use it for extraction (You can still use the column index for extraction, for example, `SELECT s._1 FROM COSObject s`). | Enum | No |
| Comments | CSV | Sets a comment column. This character will be added to the first character of the column. If a column is specified as the comment column, COS Select will not analyze it. Default value: `#` | String | No |

**Content of `JSON` (a subnode of `InputSerialization`)**

| Node Name | Parent Node | Description | Type | Required |
| ---- | ------ | ------------------------------------------------------------ | ---- | -------- |
| Type | JSON | JSON type. Valid values: <br><li>`DOCUMENT`: The JSON file contains only an independent JSON object that is divided into multiple rows<br><li>`LINES`: Each row in the JSON file contains an independent JSON object.  | Enum | Yes |

**Content of `OutputSerialization`**

| Node Name | Parent Node | Description | Type | Required |
| --------- | ------------------- | ------------------------------------------------- | --------- | --------------------------------- |
| CSV /JSON | OutputSerialization | Format of the extraction result. Valid values: `CSV`, `JSON` | Container | Yes (either CSV or JSON) |

**Content of `CSV` (a subnode of `OutputSerialization`)**

| Node Name | Parent Node | Description | Type | Required |
| -------------------- | ------ | ------------------------------------------------------------ | ------ | -------- |
| QuoteFields | CSV | Whether to use `"` as the escape for the extraction result. Valid values: <br>`ALWAYS`: yes <br>`ASNEEDED` (default): as needed | String | Yes |
| RecordDelimiter | CSV | A delimiter that separates data records of the extraction result into multiple rows. You can set this parameter to any octal character such as a comma (,), semicolon (:), or tab. The delimiter can be up to 2 bytes, which means that delimiters such as `\r\n` are supported. Default value: `\n` | String | No |
| FieldDelimiter | CSV | A delimiter that separates data records of the extraction result into multiple columns for each row. You can set this parameter to any octal character. This parameter can be up to 1 byte. Default value: `,` | String | No |
| QuoteCharacter | CSV | If a string in the extraction result contains delimiters, you can use this parameter as the escape so that the string will not be interpreted as several parts in subsequent analysis. The default value is `"`. For example, if the extraction result contains the string `a, b`, the double quotation marks can prevent the string from being interpreted as two separate characters `a` and `b`. Instead, COS Select will save the string as `"a, b"`. | String | No |
| QuoteEscapeCharacter | CSV | If a string in the extraction result contains `"`, use another `"` as the escape so that the string can be interpreted. For example, the string `" a , b"` will be saved as `""" a , b """`. Default value: `"` | String | No |

**Content of `JSON` (a subnode of `OutputSerialization`)**

| Node Name | Parent Node | Description | Type | Required |
| --------------- | ------ | ------------------------------------------------------------ | ------ | -------- |
| RecordDelimiter | JSON | A delimiter that separates data records of the extraction result into multiple rows. You can set this parameter to any octal character such as a comma (,), semicolon (:), or tab. The delimiter can be up to 2 bytes, which means that delimiters such as `\r\n` are supported. Default value: `\n` | String | No |

**Content of `RequestProgress`**

| Node Name | Parent Node | Description | Type | Required |
| ------- | --------------- | ---------------------------------------------------------- | ------- | -------- |
| Enabled | RequestProgress | Whether COS Select should return the query progress periodically. Default value: `FALSE` | Boolean | No |

## Response

If the extraction is successful, “200 OK” will be returned.

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

As the size of the response body is unpredictable, COS presents the response body in serialized form, i.e., dividing the response body into multiple parts. The following shows an overview of the returned response body:

```shell
<Message 1>
<Message 2>
<Message 3>
......
<Message n>
```

#### Pre-response (prelude) and response result (data)

COS cuts the extraction result into multiple parts, each of which is a message. Each message consists of the pre-response (prelude) and response result (data).

- The prelude consists of two parts:
 - Total length of the message
  - Total length of all headers
- The data consists of two parts:
  - Response header
  - Response body (payload)

Both the prelude and data end with a 4-byte CRC code encoded in Big Endian. COS Select uses CRC32 to calculate the CRC code. For more information on CRC32, see the [RFC documentation](https://www.ietf.org/rfc/rfc1952.txt). In addition to data, COS Select additionally spends a total of 16 bytes in transferring the prelude and code.

> !The integer values in all the messages are transferred in network byte order (i.e., encoded in Big Endian).

The figure below shows what a message and a header consist of. One message may contain multiple headers.
![Message construction](https://main.qcloudimg.com/raw/854fe989e1f98b168a038b4fb615d4e5.png)

As shown above, each message consists of a prelude, a prelude CRC code (composed of two pieces of information that record the number of bytes), header(s), a payload, and a message CRC code. As can be seen from the above figure, the length of the entire response body is calculated as follows:
```shell
Total length of a response body = Length of the prelude + length of the prelude CRC code + length of the payload + length of the header(s) + length of the message CRC code
```

As the total length of the prelude, the prelude CRC code and the message CRC code is always 16 bytes, the total length of the response body can also be quickly calculated as follows:
```shell
Total length of a response body = Length of the payload + length of the header(s) + 16
```

The following describes the components of the response body in detail:

| Component | Description |
| ------------------------- | ------------------------------------------------------------ |
| prelude | Records the total length of each message and the total length of all headers separately. Each record is of 4 bytes, and the total length is 8 bytes: <br>1. `total byte-length`: the total length of the message, which is encoded in Big Endian and of 4 bytes in total with the capacity of the record itself included. <br>2. `headers byte-length`: the total length of all headers, which is encoded in Big Endian and of 4 bytes in total with the capacity occupied by the record excluded. |
| prelude CRC | A prelude CRC is encoded in Big Endian and contains a total of 4 bytes. It helps the program quickly determine whether the prelude information is correct so as to reduce blocking during buffering. |
| header | Metadata of the extraction result recorded by the message, such as data type and body format. The length of this part in bytes varies by data type. A header is stored as a key-value (KV) pair and encoded in UTF-8. The metadata recorded in a header can be displayed in any order, but each metadata entry is recorded only once. Depending on the data type, the following headers may appear in the result returned by COS Select: <br>1. `MessageType Header`: This header represents the response type, where the key is ":message-type" and the value can be "error" or "event". "error" indicates that this record is an error message, and "event" indicates that this record is a specific event. <br>2. `EventType Header`: This header records the event type, where the key is ":event-type" and the value can be "Records", "Cont", "Progress", "Stats", or "End". "Records" indicates that the event is the returned extraction record, "Cont" the TCP connection hold, "Progress" the periodically returned extraction result, "Stats" the statistics of the query, and "End" the end of the query. <br>3. `ErrorCode Header`: This header records the error code, where the key is ":error-code" and the value can be an error code listed in [Special Error Codes](#.E7.89.B9.E6.AE.8A.E9.94.99.E8.AF.AF.E7.A0.81). <br>4. `ErrorMessage Header`: This header records the error message, where the key is ":error-message" and the value can be an error message returned by the server, which can be used to locate the error. |
| Payload | Records the extraction result or official information related to the request. |
| Message CRC | CRC code encoded in Big Endian containing a total of 4 bytes. |

A message may record multiple headers, and each header consists of the following parts:

| Component | Description |
| ------------------------ | ------------------------------------------------------------ |
| Header Name Byte-Length | Records the length of the header name in bytes |
| Header Name | Header type. Value range: ":message-type", ":event-type", ":error-code", ":error-message" <br><li>":message-type" indicates that the header records the response type <br><li> ":event-type" indicates that the header records the event type <br><li>":error-code" indicates that the header records the error code <br><li>" :error-message" indicates that the header records the error message. |
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
| RequestLevelError message | Error message including the error causes. This parameter is returned when a COS Select error occurs during the query. If COS Select returns this message, it will not return an end message. |

These response types are as detailed below.

#### Records message

- Header format
  A records message contains three types of headers: ":message-type", ":event-type", and ":content-type", as shown below:
  ![Records message ](https://main.qcloudimg.com/raw/7e04ad30a1ce335a67975a291bffdac5.png) 
- Body format
  The body of a records message may contain a single record, a partial record, or multiple records, depending on the number of extraction results.

#### Continuation Message

- Header format
  A continuation message contains two types of headers: ":message-type" and ":event-type", as shown below:
  ![ Continuation Message ](https://main.qcloudimg.com/raw/b8488620e8f2989f993e9b5488dfe52b.png) 
- Body format
  A continuation message contains no body content.

#### Progress message

- Header format
  A progress message contains three types of headers: ":message-type", ":event-type", and ":content-type", as shown below:
  ![Progress Message](https://main.qcloudimg.com/raw/6f262224260381b3c7b233b25ce0fbb0.png) 
- Body format
  The body of a progress message is XML text which contains the current query progress, mainly including:
	- BytesScanned: If the file is compressed, this value represents the size of the file in bytes before it is decompressed; otherwise, this value represents the size of the file in bytes.
	- BytesProcessed: If the file is compressed, this value represents the size of the file in bytes after it is decompressed; otherwise, this value represents the size of the file in bytes.
	- BytesReturned: Size of the extraction result currently returned by COS Select in bytes.

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
  ![ Stats Message ](https://main.qcloudimg.com/raw/8fbe1d40ec19c4f72d18275ff087f264.png)
- Body format
  The body of a stats message is XML text which contains the statistics of the current query, mainly including:
  - BytesScanned: If the file is compressed, this value represents the size of the file in bytes before it is decompressed; otherwise, this value represents the size of the file in bytes.
  - BytesProcessed: If the file is compressed, this value represents the size of the file in bytes after it is decompressed; otherwise, this value represents the size of the file in bytes.
  - BytesReturned: Size of the extraction result returned by COS Select in the query in bytes.

Example:

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
  ![ End messages ](https://main.qcloudimg.com/raw/f28f76c719b02258379adf1fcc71f484.png)
- Body format
  An end message contains no body content.

#### Request Level Error Message

- Header format
  A request level error message contains three types of headers: ":error-code", ":error-message", and ":message-type", as shown below:
  ![ Request Level Error Message](https://main.qcloudimg.com/raw/72fc70c4cabbc86b67d1cf8cc46a8d70.png) 

For more information on the error code in a request level error message, see [Special Error Codes](#.E7.89.B9.E6.AE.8A.E9.94.99.E8.AF.AF.E7.A0.81).

- Body format
  A request level error message contains no body content.

<span id="errorcode"></span>
#### Special error codes

For common errors related to this request, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). The following describes special error codes:                     

| Error Code | Error Message | HTTP Status Code |
| -- | -- | -- | -- |
| InvalidXML | The XML is invalid | 400 Bad Request|
| MissingRequiredParameter | The SelectRequest entity is missing a required parameter | 400 Bad Request|
| MissingExpectedExpression | The SQL expression is missing | 400 Bad Request|
| MissingInputSerialization | The input serialization is missing | 400 Bad Request|
| InvalidCompressionFormat |  The file is not in a supported compression format. Only GZIP and BZIP2 are supported | | 400 Bad Request|
| MissingInputFormat | The input format is missing | 400 Bad Request|
| InvalidFileHeaderInfo |  The input FileHeaderInfo is invalid. Only NONE, USE, and IGNORE are supported | 400 Bad Request|
| InvalidRequestParameter | The input RecordDelimiter of CSV is invalid  | 400 Bad Request |
| InvalidRequestParameter | The input FieldDelimiter of CSV is invalid  | 400 Bad Request |
| InvalidRequestParameter | The input QuoteCharacter of CSV is invalid | 400 Bad Request|
| InvalidRequestParameter |  The input AllowQuoteRecordDelimiter of CSV is invalid. Only TRUE and FALSE are supported | 400 Bad Request|
| InvalidJsonType | The JsonType is invalid. Only DOCUMENT and LINES are supported | 400 Bad Request|
| MissingOutputSerialization |  The output serialization is missing | 400 Bad Request |
| MissingOutputFormat | The output format is missing | 400 Bad Request |
| InvalidQuoteFields | The QuoteFields is invalid. Only ALWAYS and ASNEEDED are supported | 400 Bad Request |
| InvalidRequestParameter |  The output RecordDelimiter of CSV is invalid | 400 Bad Request |
| InvalidRequestParameter |  The output FieldDelimiter of CSV is invalid | 400 Bad Request |
| InvalidRequestParameter | The output QuoteCharacter of CSV is invalid  | 400 Bad Request|
| InvalidRequestParameter | The output QuoteEscapeCharacter of CSV is invalid  | 400 Bad Request|
| InvalidRequestParameter |  The output RecordDelimiter of JSON is invalid | 400 Bad Request|
| SQLParsingError | Encountered an error parsing the SQL expression  | 400 Bad Request|
| SQLParsingError |  Other expressions are not allowed in the SELECT list when '\*' is used without dot notation. | 400 Bad Request|
| SQLParsingError |  The SQL expression contains an empty SELECT | 400 Bad Request|
| SQLParsingError | GROUP is not supported in the SQL expression | 400 Bad Request|
| SQLParsingError | UNION is not supported in the SQL expression | 400 Bad Request|
| SQLParsingError | FROM is missing in the SQL expression | 400 Bad Request|
| SQLParsingError | ORDER is not supported in the SQL expression | 400 Bad Request|
| SQLParsingError | The column index is invalid in the SQL expression | 400 Bad Request|
| SQLParsingError | The table alias is invalid in WHERE | 400 Bad Request|
| Bzip2DecompressError | Encountered an error decompressing the bzip2 file | 400 Bad Request|
| Bzip2DecompressError | bzip2 is not applicable to the queried object | 400 Bad Request|
| GzipDecompressError |  Encountered an error decompressing the GZIP file | 400 Bad Request|
| GzipDecompressError | GZIP is not applicable to the queried object  | 400 Bad Request|
| Busy |  The service is busy. Please retry later | 400 Bad Request|
| Overload | The service is overload. Please retry later | 400 Bad Request|
| AmbiguousFieldName |  Field name matches to multiple fields in the file | 400 Bad Request|
| ComparisonFailed | Attempt to compare failed | 400 Bad Request|
| CastFailed | Attempt to convert from one data type to another using CAST failed in the SQL expression. | 400 Bad Request|
| OverMaxRecordSize |  The length of a record in the input or result is greater than maxCharsPerRecord of 1 MB | 400 Bad Request|
| LastRecordParseFail |  Please check the last record in the input | 400 Bad Request|
| CSVParsingError | Encountered an error parsing the CSV file | 400 Bad Request|
| JSONParsingError | Encountered an error parsing the JSON file  | 400 Bad Request|
| ErrorWritingRow | Encountered an error parsing the SELECT result. Please try again  | 400 Bad Request|
| InvalidRequestParameter | The input Comment of CSV is invalid  |400 Bad Request|
| InvalidTextEncoding | UTF-8 encoding is required. Please check the file and try again. | 400 Bad Request|
| NoSuchKey | The specified key does not exist  | 404 Not Found|
| AccessDenied |  Access Denied | 403 Forbidden|
| MethodNotAllowed | The specified method is not allowed against this resource | 405 Method Not Allowed|
| InternalError | We encountered an internal error. Please try again | 500 Internal Server|



## Samples

#### Sample 1: extracting content from a CSV object

The following sample extracts all content from a CSV object and saves the extraction result in CSV format. The object to extract is named `exampleobject.csv` and stored in the `examplebucket-1250000000` bucket that resides in the Beijing (ap-beijing) region.

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

To run different extraction commands, modify the SQL command in the `Expression` node. For more information about commands, please see [SELECT Command](https://intl.cloud.tencent.com/document/product/436/32473). Some common extraction scenarios are described below.

- Suppose that you use a column index to filter the content from an object. You can use `s._n` to filter data records in the `n` column (the minimum value of `n` is 1). The following command filters data records that are greater than 100 in column 3 and returns columns 1 and 2 of these matching records: 
```shell
SELECT s._1, s._2 FROM COSObject s WHERE s._3 > 100
```

- If your CSV object has a column header and you want to filter the content of the object using the name of the header (you need to set `FileHeaderInfo` to `Use`), you can use `s.name` for indexing. The following command filters records using a header named `Id` and `FirstName`:
```shell
SELECT s.Id, s.FirstName FROM COSObject s
```

- You can also specify a function in the SQL expression. The following command counts the number of records whose values are smaller than 1 in column 1:
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

#### Sample 2: extracting content from an object in JSON format

The following sample extracts all content from a JSON object and saves the extraction result in CSV format. The object to extract is named `exampleobject.json` and stored in the `examplebucket-1250000000` bucket that resides in the Beijing (ap-beijing) region.

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

Similarly, you can also perform different extraction commands on JSON objects by modifying the SQL command in the `Expression` node. For more information about commands, please see [SELECT Command](https://intl.cloud.tencent.com/document/product/436/32473). Some common extraction scenarios are described below.

- You can use a JSON attribute name to extract content. The following command filters records whose `city` value is Seattle from the object and returns the `country` and `city` information of these records:
```shell
SELECT s.country, s.city from COSObject s where s.city = 'Seattle'
```

- You can also specify a function in the SQL expression. The following command counts the total number of records in the JSON object:
```shell
SELECT count(*) FROM COSObject s
```

## Notes

Unlike the [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) API, SELECT Object Content does not support:

- Returning a part of an object. You cannot use parameters such as `Range` to specify a part of an object to return.
- Extracting content from ARCHIVE or DEEP ARCHIVE objects. You need to restore them first.
