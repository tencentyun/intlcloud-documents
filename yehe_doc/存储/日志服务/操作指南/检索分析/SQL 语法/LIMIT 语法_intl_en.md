The `LIMIT` syntax is used to limit the number of rows in the output result.

## Syntax Format

- Read the first N rows:
```
limit N
```
- Read N rows starting from row S:
```
offset S limit N
```


## Syntax Example

- Get the first 10 rows of results:
```
* | select status, count(*) as pv group by status limit 10
```
- Get the results for rows 3 to 42 (40 rows in total):
```
* | select status, count(*) as pv group by status offset 2 limit 40
```



## Restrictions

<table>
	<tr><th>Metric</th><th>Restriction</th><th>Remarks</th></tr>
	<tr><td>Number of SQL results</td><td>Each SQL returns up to 10,000 results.</td><td>Default: 100; Maximum: 10,000</td></tr>
</table>

