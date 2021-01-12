## Overview

The COS Select feature only supports the SELECT command to extract the required data and reduce the amount of data transferred, which helps lower the costs and request delay. The following are the standard clauses supported by SELECT queries:

- SELECT statement
- WHERE clause
- LIMIT clause

> COS Select currently does not support clause queries or joins.

## SELECT Statement

The SELECT statement can extract the data you want to see from a COS object. You can query the data at different dimensions such as column name, function, and expression, and the query result will be returned as a list. The format of SELECT statement call is as follows:

```shell
SELECT *
SELECT projection [ AS column_alias | column_alias ] [, ...]
```

The first SELECT statement is marked with `*` (asterisk) and will return all the columns in the COS object. The second one uses a user-defined output scalar expression, and **projection** creates a list of outputs with custom names for each column.


## WHERE Clause

The WHERE clause uses the following syntax:

```shell
WHERE condition
```

The WHERE clause filters data by **condition**. **condition** is an expression that returns a Boolean result, and only rows with a return value of TRUE will be output in the result.

## LIMIT Clause

The LIMIT clause uses the following syntax:

```shell
LIMIT number
```

The LIMIT clause sets a limit on the number of records to be returned per query, which can be specified using the **number** parameter.

## Access Attributes

The SELECT and WHERE clauses can select the fields to be queried in any of the following ways, depending on whether the file format is CSV or JSON.

#### CSV

- **Column number**: You can use `_N` to specify the data in column N for query. For any CSV files, the column number increases from 1. For example, the first column is numbered `_1`, and the second column is numbered `_2`. In the SELECT and WHERE clauses, it is valid to specify the column to be queried using `_N` or `alias._N`.
- **Column header**: If the CSV file to be queried contains column headers, the SELECT and WHERE clauses can use the headers to specify the columns to be queried, which can be specified using `alias.column_name` or `column_name` in the SELECT and WHERE clauses in an SQL statement.

#### JSON 

- **Document**: You can access a JSON document using `alias.name`. A nested array can be accessed in a way such as `alias.name1.name2.name3`.
- **List**: You can access the elements in a list using an index, which is numbered from 0 and uses the `[]` operator. For example, you can access the second element in a JSON list using `alias[1]`. If you need to access a nested array, you can also do so in a way such as `alias.name1.name2[1].name3`.

**Samples** 
The following is the sample data in the samples:

```shell
{
	"name": "Leon",
	"org": "Tencent",
	"projects":
		[
		 {"project_name":"project1", "completed":true},
		 {"project_name":"project2", "completed":false}
		]
}
```

- Sample 1. The following is the SQL statement used to query `name` in the sample data and the query result:
  ```shell
  Select s.name from COSObject s
  ```
  ```shell
  {"name":"Leon"}
  ```
- Sample 2. The following is the SQL statement used to query `project_name` in the sample data and the query result:
  ```shell
  Select s.projects[0].project_name from COSObject s
  ```
  ```shell
  {"project_name":"project1"}
  ```

## Case Sensitivity of Headers and Attribute Names

You can use double quotation marks to indicate whether headers in a CSV file and attribute names in a JSON file are case-sensitive. If no double quotation marks are added, the headers/attribute names are case-insensitive. If this is not explicitly specified, COS Select may throw an exception.

- Sample 1. Query objects with a header/attribute name containing "NAME".
  Because the following sample SQL query does not contain double quotation marks, the query is case-insensitive. As this header is present in the table, a value will be successfully returned eventually.
  ```shell
  SELECT s.name from COSObject s
  ```

  Because the following sample SQL query contains double quotation marks, the query is case-sensitive. As the table does not contain this header, the `SQLParsingError` 400 error will be eventually returned.
  ```shell
  SELECT s."name" from COSObject s
  ```

- Sample 2. Query objects with a header/attribute name containing "NAME" and "name".
  Because the following sample SQL query does not contain double quotation marks, the query is case-insensitive. As the table contains two headers "NAME" and "name", the query command is ambiguous, and the `AmbiguousFieldName` exception will be thrown.
  ```shell
  SELECT s.name from COSObject s
  ```

  Because the following sample SQL query contains double quotation marks, the query is case-sensitive. As the table contains the header "NAME", the query result will be successfully returned.
  ```shell
  SELECT s."NAME" from COSObject s
  ```

## Using Reserved Fields as User-defined Fields

The SQL expressions of COS Select have certain reserved fields such as function name, data type, and operator. Sometimes you probably use these reserved fields as column headers in a CSV file or attribute names in a JSON, which may cause conflicts with reserved fields. In this case, you can use double quotation marks to indicate that you are using a custom field; otherwise, COS will return `400 parse error`.

For the complete list of reserved fields, see [Reserved Words](https://intl.cloud.tencent.com/document/product/436/32475).

- Sample: The header/attribute name in the object to be queried contains a reserved field "CAST".
  The following sample SQL query uses double quotation marks to indicate that CAST is a user-defined field, so the query result will be successfully returned.
  ```shell
  SELECT s."CAST" from COSObject s
  ```
  The following sample SQL query does not use double quotation marks to indicate that CAST is a user-defined field, so COS will treat it as a reserved field and return `400 parse error`.
  ```shell
  SELECT s.CAST from COSObject s
  ```

## Scalar Expressions

In the SELECT statement and the WHERE clause, you can use SQL scalar expressions (expressions that return a scalar). Currently, COS Select supports the following forms:

- **literal**: SQL text.
- **column_reference**: column_name or alias.column_name.
- **unary_op** **expression**: SQL unary operator.
- **expression** **binary_op** **expression**: SQL binary operator.
- **func_name**: Name of the called scalar function.
- **expression** [ NOT ] BETWEEN **expression** AND **expression**
- **expression** LIKE **expression** [ ESCAPE **expression** ]
