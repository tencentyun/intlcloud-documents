The COS Select feature uses structured query language (SQL) statements to filter the objects stored in COS so as to extract a specific object and get the desired data. By filtering object data using this feature, you can reduce the amount of data transferred by COS, which helps lower the costs and delay in data extraction.

The COS Select feature currently allows you to extract objects stored in CSV and JSON formats and objects compressed by gzip and bzip2 (for CSV and JSON objects only). In addition, it supports saving the extraction result in CSV and JSON formats and specifying how to separate the records in the result.

You can pass an SQL expression to COS in your request. COS Select currently only supports certain SQL expressions. For more information, see [SQL Functions](https://intl.cloud.tencent.com/document/product/436/32474).

You can use the COS SDK, API, COSCMD, or COS Console to execute SQL queries. Note that there are certain restrictions on file extraction using the COS Console: Up to 128 MB of files can be extracted, and up to 40 MB of data can be returned. To extract more data, you need to use other methods.

>For more information on the data types supported by COS Select and current reserved fields, see [Data Types](https://intl.cloud.tencent.com/document/product/436/32476) and [Reserved Fields](https://intl.cloud.tencent.com/document/product/436/32475).
>Currently, the select feature only supports Chengdu and Chongqing regions.

## Use Limits

The following restrictions apply to COS Select:

- You must have the `cos:GetObject` permission to the object being queried. A root account has this permission by default.
- Only objects in standard storage class can be extracted.
- The maximum length of an SQL expression is 256 KB.
- The maximum length of a single record in the extraction result is 1 MB.

SQL clauses currently supported by the COS Select feature include:

- SELECT statement
- FROM clause
- WHERE clause
- LIMIT clause

>For more information on SQL clauses, see [SELECT Command](https://intl.cloud.tencent.com/document/product/436/32473).

Functions currently supported by COS Select include:

- Aggregate functions, such as AVG function, COUNT function, MAX function, MIN function, and SUM function.
- Condition functions, such as COALESCE function and NULLIF function.
- Conversion functions, such as CAST function.
- Date functions, such as DATE_ADD function, DATE_DIFF function, EXTRACT function, TO_STRING function, TO_TIMESTAMP function, and UTCNOW function.
- String functions, such as CHAR_LENGTH function, CHARACTER_LENGTH function, LOWER function, SUBSTRING function, TRIM function, and UPPER function.

>For more information on SQL functions, see [SQL Functions](https://intl.cloud.tencent.com/document/product/436/32474).

COS Select currently supports the following operators:

- Logical operators: `AND, NOT, OR`
- Comparison operators: `<, >, <=, >=, =, <>, !=, BETWEEN, IN`
- Pattern matching operators: `LIKE`
- Mathematical operators: `+, -, *, %`

>For more information on operators, see [Operators](https://intl.cloud.tencent.com/document/product/436/32477).



## Initiating an Extraction Request

You can initiate an extraction request using the console, API, or SDK:

- To use the console, follow the steps in [Extracting Data].
- To use the SDK, you can go to [SDK Overview](https://intl.cloud.tencent.com/document/product/436/6474) and select the required SDK API.
- To use the API, see [SELECT Object Content](https://intl.cloud.tencent.com/document/product/436/32360).

## FAQs

If a problem occurs when you try to execute a query, COS Select will return an error code and the associated error message. For the list of error codes and descriptions, see [Special Error Codes](https://intl.cloud.tencent.com/document/product/436/32360#errorcode).                      
