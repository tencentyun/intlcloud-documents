This document introduces the basic syntax and examples of conditional expressions.

<table>
	<tr><th>Expression</th><th>Syntax</th><th>Description</th></tr>
	<tr><td><a href="#CASEWHEN">CASE WHEN</a></td><td>CASE WHEN condition1 THEN result1 [WHEN condition2 THEN result2] [ELSE result3] END</td><td>Classifies data according to specified conditions.</td></tr>
	<tr><td rowspan=2><a href="#IF">IF</a></td><td>IF(condition, result1)</td><td>If `condition` is `true`, returns `result1`. Otherwise, returns `null`.</td></tr>
	<tr><td>IF(condition, result1, result2)</td><td>If `condition` is `true`, returns `result1`. Otherwise, returns `result2`.</td></tr>
	<tr><td><a href="#NULLIF">NULLIF</a></td><td>NULLIF(expression1, expression2)</td><td>Determines whether the values of two expressions are equal. If the values are equal, returns `null`. Otherwise, returns the value of the first expression.</td></tr>
	<tr><td><a href="#TRY">TRY</a></td><td>TRY(expression)</td><td>Captures exception information to enable the system to continue query and analysis operations.</td></tr>
	<tr><td><a href="#COALESCE">COALESCE</a></td><td>COALESCE(expression1, expression2...)</td><td>Gets the first non-null value in multiple expressions.</td></tr>
</table>


<span id="CASEWHEN"></span>
## CASE WHEN

The `CASE WHEN` expression is used to classify data.

### Syntax

```
CASE WHEN condition1 THEN result1
			[WHEN condition2 THEN result2]
			[ELSE result3]
END
```

### Parameter description

| Parameter | Description |
| --------- | ------------ |
| condition | Conditional expression |
| result    | Return result   |

### Example
#### Example 1. 
Extract browser information from the `http_user_agent` field, classify the information into the Chrome, Safari, and unknown types, and calculate the PVs of the three types.
- Query and analysis statement
```
* |
SELECT
  CASE
    WHEN http_user_agent like '%Chrome%' then 'Chrome'
    WHEN http_user_agent like '%Safari%' then 'Safari'
    ELSE 'unknown'
  END AS http_user_agent,
  count(*) AS pv
GROUP BY
  http_user_agent
```
  - Query and analysis result
![image-20211108042836003](https://qcloudimg.tencent-cloud.cn/raw/fc5871dabac0087c4bcd90f89872f2b1.png)

#### Example 2. 
Get the statistics on the distribution of different request times.
- Query and analysis statement
```
* |
SELECT
  CASE
    WHEN request_time < 0.001 then 't0.001'
    WHEN request_time < 0.01 then 't0.01'
    WHEN request_time < 0.1 then 't0.1'
    WHEN request_time < 1 then 't1'
    ELSE 'overtime'
  END AS request_time,
  count(*) AS pv
GROUP BY
  request_time
```
  - Query and analysis result
![image-20211108043145849](https://qcloudimg.tencent-cloud.cn/raw/e374910d8b6f772d2bb90dd062fa7083.png)


<span id="IF"></span>
## IF

The `IF` expression is used to classify data. It is similar to the `CASE WHEN` expression.

### Syntax

- If `condition` is `true`, return `result1`. Otherwise, return `null`.
```
IF(condition, result1)
```
- If `condition` is `true`, return `result1`. Otherwise, return `result2`.
```
IF(condition, result1, result2)
```

### Parameter description

| Parameter | Description |
| --------- | ------------ |
| condition | Conditional expression |
| result    | Return result   |

### Example

Calculate the proportion of requests with status code 200 to all requests.

- Query and analysis statement
```
* |
SELECT
  sum(IF(status = 200, 1, 0)) * 1.0 / count(*) AS status_200_percentag
```
- Query and analysis result
![image-20211108043554359](https://qcloudimg.tencent-cloud.cn/raw/5e6a960b29adf2b8e248618534fc8556.png)


<span id="NULLIF"></span>
## NULLIF

The `NULLIF` expression is used to determine whether the values of two expressions are equal. If the values are equal, return `null`. Otherwise, return the value of the first expression.

### Syntax

```
NULLIF(expression1, expression2)
```

### Parameter description

| Parameter | Description |
| ---------- | ---------------------- |
| expression | Any valid scalar expression |

### Example

Determine whether the values of the `server_addr` and `http_host` fields are the same. If the values are different, return the value of the `server_addr`.

- Query and analysis statement
```
* | SELECT NULLIF(server_addr,http_host)
```
- Query and analysis result
![image-20211108044354167](https://qcloudimg.tencent-cloud.cn/raw/385643b55d531b8828eb699c5f69834e.png)


<span id="TRY"></span>
## TRY

The `TRY` expression is used to capture exception information to enable the system to continue query and analysis operations.

### Syntax

```
TRY(expression)
```

### Parameter description

| Parameter | Description |
| ---------- | ------------------ |
| expression | Expression of any type |

### Example

When an exception occurs during the `regexp_extract` function execution, the `TRY` expression captures the exception information, continues the query and analysis operation, and returns the query and analysis result.

- Query and analysis statement
```
* | 
SELECT
  TRY(regexp_extract(uri, '.*\/(index.*)', 1)) 
	AS file, count(*) 
	AS count 
GROUP BY 
  file
```
- Query and analysis result
![image-20211108044634878](https://qcloudimg.tencent-cloud.cn/raw/be64b0943d47ba13ed251fc8bf453373.png)


<span id="COALESCE"></span>
## COALESCE

The `COALESCE` expression is used to get the first non-null value in multiple expressions.

### Syntax

```
COALESCE(expression1, expression2...)
```

### Parameter description

| Parameter | Description |
| ---------- | ------------------ |
| expression | Any valid scalar expression |


### Example

- Query and analysis statement
```
* | select COALESCE(null, 'test')
```
- Query and analysis result
![](https://qcloudimg.tencent-cloud.cn/raw/9a55a530e9970f5b6d3470da22fa0dea.png)







