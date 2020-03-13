The COS Select feature uses structured query language (SQL) to filter objects stored in COS in order to extract a specific object and get the desired data. By filtering object data using this feature, you can reduce the amount of data transferred by COS, which helps lower the cost and delay in data extraction.

The COS Select feature currently allows you to extract objects stored in CSV and JSON formats and compressed by gzip and bzip2 (for CSV and JSON objects only). In addition, you can save the extraction result in CSV and JSON formats and specify how to separate the result records.

You can pass in an SQL expression to COS in your request. COS Select currently only supports certain SQL expressions. For more information, see [SQL Functions](https://cloud.tencent.com/document/product/436/37637).

You can use the COS SDK, API, COSCMD, or COS Console to execute on SQL queries. Note that certain restrictions apply on file extraction if you use the COS Console: Up to 128 MB of files can be extracted, and up to 40 MB of data can be returned. To extract more data, use other methods.

>
>- For more information on data types supported by COS Select and current reserved fields, see [Data Types](https://cloud.tencent.com/document/product/436/37639) and [Reserved Fields](https://cloud.tencent.com/document/product/436/37638).
>-Currently, the extraction function only supports public cloud regions in mainland China.

## Use Limits

The following restrictions apply to COS Select:

- You must have the `cos:GetObject` permission to the queried object. A root account has this permission by default.
- Only objects in standard storage class can be extracted.
- The maximum length of an SQL expression is 256 KB.
- The maximum length of a single record in the extraction result is 1 MB.

SQL clauses currently supported by COS Select include:

- SELECT statement
- FROM clause
- WHERE clause
- LIMIT clause

> For more information on SQL clauses, see [SELECT Command](https://cloud.tencent.com/document/product/436/37636).

Functions currently supported by COS Select include:

- Aggregate functions, such as AVG function, COUNT function, MAX function, MIN function, and SUM function.
- Condition functions, such as COALESCE function and NULLIF function.
- Conversion functions, such as CAST function.
- Date functions, such as DATE_ADD function, DATE_DIFF function, EXTRACT function, TO_STRING function, TO_TIMESTAMP function, and UTCNOW function.
- String functions, such as CHAR_LENGTH function, CHARACTER_LENGTH function, LOWER function, SUBSTRING function, TRIM function, and UPPER function.

>- For more information on SQL functions, see [SQL Functions](https://cloud.tencent.com/document/product/436/37637).

COS Select currently supports the following operators:

- Logical operators: `AND, NOT, OR`
- Comparison operators: `<, >, <=, >=, =, <>, !=, BETWEEN, IN`
- Pattern matching operators: `LIKE`
- Mathematical operators: `+, -, *, %`

>- For more information on operators, see [Operators](https://cloud.tencent.com/document/product/436/37640).



## Initiating an extraction request

You can initiate an extraction request using the console, API, or SDK:

- If you use the console, see [Data Extraction](https://cloud.tencent.com/document/product/436/37642).
- If you use the SDK, go to [SDK Overview](https://intl.cloud.tencent.com/document/product/436/6474) and select the required SDK API.
- If you use the API, see [SELECT Object Content](https://cloud.tencent.com/document/product/436/37641).

## FAQ

If a problem occurs when you execute on a query, COS Select will return an error code and associated error message. For the list of error codes and descriptions, see [Special Error Codes](https://cloud.tencent.com/document/product/436/37641#errorcode).                      
