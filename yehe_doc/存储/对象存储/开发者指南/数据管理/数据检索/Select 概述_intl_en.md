The COS Select feature uses Structured Query Language (SQL) statements to filter the objects stored in COS so as to extract specific objects and get desired data. With COS Select, you can reduce the amount of data transferred by COS for lower costs and latency during data extraction.

The COS Select feature currently allows you to extract objects stored in CSV, JSON, and Parquet formats and compressed by gzip or bzip2 (for CSV and JSON objects only). In addition, you can save extraction results in CSV and JSON formats and specify how to separate the result records.

You can pass in a SQL expression to COS in your request. COS Select currently only supports certain SQL expressions. For more information, see [SQL Functions](https://intl.cloud.tencent.com/document/product/436/32474).

You can use the COS console, API, SDK, or COSCMD to perform SQL queries. Note that certain limits apply to file extraction in the COS console: up to 128 MB of files can be extracted, and up to 40 MB of data can be returned. To extract more data, you need to use other methods.

>?
>- For more information on data types supported by COS Select and current reserved fields, see [Data Types](https://intl.cloud.tencent.com/document/product/436/32476) and [Reserved Fields](https://intl.cloud.tencent.com/document/product/436/32475).
>-Currently, the extraction function only supports public cloud regions in the Chinese mainland.
>

## Restrictions

The following restrictions apply to COS Select:

- You must have the `cos:GetObject` permission to the queried object. A root account has this permission by default.
- Only objects in the STANDARD storage class can be extracted.
- The maximum length of a SQL expression is 256 KB.
- The maximum length of a single record in the extraction result is 1 MB.

SQL clauses currently supported by COS Select include:

- SELECT statement
- FROM clause
- WHERE clause
- LIMIT clause

>?For more information on SQL clauses, see [SELECT Command](https://intl.cloud.tencent.com/document/product/436/32473).

Functions currently supported by COS Select include:

- Aggregate functions, such as AVG, COUNT, MAX, MIN, and SUM.
- Condition functions, such as COALESCE and NULLIF.
- Conversion functions, such as CAST.
- Date functions, such as DATE_ADD, DATE_DIFF, EXTRACT, TO_STRING, TO_TIMESTAMP, and UTCNOW.
- String functions, such as CHAR_LENGTH, CHARACTER_LENGTH, LOWER, SUBSTRING, TRIM, and UPPER.

>?For more information on SQL functions, see [SQL Functions](https://intl.cloud.tencent.com/document/product/436/32474).

COS Select currently supports the following operators:

- Logical operators: AND, NOT, OR
- Comparison operators: <, >, <=, >=, =, <>, !=, BETWEEN, IN
- Pattern matching operators: LIKE
- Mathematical operators: +, -, *, %

>? For more information on operators, see [Operators](https://intl.cloud.tencent.com/document/product/436/32477).
>



## Initiating Extraction Request

You can initiate an extraction request using the console, API, or SDK:

- If you use the console, see [Data Extraction](https://intl.cloud.tencent.com/document/product/436/32538).
- If you use the API, see [SELECT Object Content](https://intl.cloud.tencent.com/document/product/436/32360).
- If you use the SDK, go to [SDK Overview](https://intl.cloud.tencent.com/document/product/436/6474) and select the required SDK API.


## FAQs

If a problem occurs when you perform a query, COS Select will return an error code and error message. For the list of error codes and descriptions, see [Special Error Codes](https://intl.cloud.tencent.com/document/product/436/32360#errorcode).                      


