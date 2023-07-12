This document introduces the basic syntax and examples of estimation functions.

<table>
	<thead>
		<tr>
		<th>Function</th>
		<th>Syntax</th>
		<th>Description</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>approx_distinct</td>
			<td>approx_distinct(x)</td>
			<td>Returns the approximate number of distinct input values (column x).</td>
		</tr>
		<tr>
			<td rowspan=2>approx_percentile</td>
			<td>approx_percentile(x,percentage)</td>
			<td>Sorts the values in the x column in ascending order and returns the value approximately at the given `percentage` position.</td>
		</tr>
		<tr>
			<td>approx_percentile(x,array[percentage01, percentage02...])</td>
			<td>Sorts the values in the x column in ascending order and returns the values approximately at the given `percentage` positions (percentage01, percentage02...).</td>
		</tr>
	</tbody>
</table>

## approx_distinct

The `approx_distinct` function is used to get the approximate number of distinct input values of a field. The standard result deviation is 2.3%.

### Syntax

```
approx_distinct(x)
```

### Field description

| Parameter | Description |
| ---- | ---------------------- |
| x    | The parameter value can be of any data type.           |

### Return value type

Bigint

### Sample

Use the `count` function to calculate the PV value and use the `approx_distinct` function to get the approximate number of distinct input values of the `client_ip` field and use it as the UV value.

```
* | SELECT count(*) AS PV, approx_distinct(ip) AS UV
```



## approx_percentile

The `approx_percentile` function is used to sort values of the target field in ascending order and return the value in the position around `percentage`. It uses the T-Digest algorithm for estimation, which has a low deviation and can meet the most statistical analysis requirements. If needed, you can use `* | select count_if(x<(select approx_percentile(x,percentage))),count(*)` to accurately count the number of field values below `percentage` and the total number of field values respectively and then verify the statistical deviation.

### Syntax

- Return the value (double) approximately at the given `percentage` position
```
approx_percentile(x, percentage)
```
- Return the value (array) approximately at the given `percentage` positions (percentage01,percentage02...)
```
approx_percentile(x, array[percentage01,percentage02...])
```

### Field description

| Parameter | Description |
| ---------- | --------------------------- |
| x          | Value type: double        |
| percentage | Value range: [0,1] |

### Return value type

double or array

### Sample
#### Sample 1
Sort the values of the **resTotalTime** column and return the value of **resTotalTime** approximately at the 50% position.
```
* | select approx_percentile(resTotalTime,0.5)
```



#### Sample 2
Sort the values of the **resTotalTime** column and return the values of **resTotalTime** approximately at the 10%, 20%, and 60% positions.
```
* | select approx_percentile(resTotalTime, array[0.2,0.4,0.6])
```



