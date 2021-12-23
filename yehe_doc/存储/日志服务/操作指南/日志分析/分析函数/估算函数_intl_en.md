This document introduces the basic syntax and examples of estimation functions.

>? Currently, CLS functions can be used in most regions. If they are required in Beijing, Shanghai, Guangzhou, and Nanjing, please contact [smart customer service](https://intl.cloud.tencent.com/contact-sales).
>

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

The `approx_distinct` function is used to get the approximate number of distinct input values of a field.

### Syntax

```
approx_distinct(x)
```

### Parameter description

| Parameter         | Description              |
| ---- | ---------------------- |
| x    | The parameter value can be of any type. |

### Return value type

bigint

### Example

Use the `count` function to calculate the PV value and use the `approx_distinct` function to get the approximate number of distinct input values of the `client_ip` field and use it as the UV value.

```
* | SELECT count(*) AS PV, approx_distinct(ip) AS UV
```

![image-20210817004306514](https://main.qcloudimg.com/raw/ad47ca879e1149a3a4fb5aa378154f41.png)

## approx_percentile

The `approx_percentile` function is used to sort the values of a target field in ascending order and return the values approximately at the given `percentage` position.

### Syntax

- Return the value (double) approximately at the given `percentage` position
```
approx_percentile(x, percentage)
```
- Return the value (array) approximately at the given `percentage` positions (percentage01,percentage02...)
```
approx_percentile(x, array[percentage01,percentage02...])
```

### Parameter description

| Parameter | Description |
| ---------- | --------------------------- |
| x          | Value type: double        |
| percentage | Value range: [0,1] |

### Return value type

double or array

### Example

Example 1: sort the values of the **resTotalTime** column and return the value of **resTotalTime** approximately at the 50% position

```
* | select approx_percentile(resTotalTime,0.5)
```



Example 2: sort the values of the **resTotalTime** column and return the values of **resTotalTime** approximately at the 10%, 20%, and 60% positions

```
* | select approx_percentile(resTotalTime, array[0.2,0.4,0.6])
```



