This document introduces the usage and examples of the `LIMIT` syntax.

The `LIMIT` syntax is used to limit the number of rows in the output result.

## Syntax Format

CLS supports either of the following types of `LIMIT` syntax:

- Read the first N rows:
```
limit N
```
- Read N rows starting from row S:
```
offset S limit N
```
>?
> - In page turning read, `LIMIT` is only used to obtain the final result, not the intermediate result of the SQL statement.
> - The `LIMIT` syntax cannot be used in subqueries. Example:
>```
* | select sum(pv) from 
(
select count(1) as pv from log group by status 
)
```
> 

## Example

- Get the first 10 rows of results:
```
* | select status, count(*) as pv group by status limit 10
```
- Get the results for rows 2 to 42 (41 rows in total):
```
* | select status, count(*) as pv group by status offset 2 limit 40
```

## Restrictions

<table>
	<tr><th>Metric</th><th>Restriction</th><th>Remarks</th></tr>
	<tr><td>Number of analysis results</td><td>Each analysis returns up to 10,000 results.</td><td>Default: 100; Maximum: 10,000</td></tr>
</table>

