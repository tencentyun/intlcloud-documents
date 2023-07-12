

An aggregate function performs calculations on a set of values and returns a single value. It is often used in combination with the [GROUP BY](https://intl.cloud.tencent.com/document/product/614/38732) clause in the [SELECT](https://intl.cloud.tencent.com/document/product/614/38735) statement.

| Statement | Description | Example | Sample SQL |
| -------------------- | ---------------------------------------- | --------------------------------- | ------------------------------------------------------- |
| AVG(KEY) | Calculates the arithmetic average of the KEY column. | Calculates the average response time of requests. | `* \| SELECT AVG(request_time) ` |
| COUNT(\*) | Indicates the number of all rows. | Calculates the number of all requests with a status code greater than 200. | `* \| SELECT COUNT(*)  WHERE http_status  > 200` |
| COUNT(KEY) | Counts the number of non-null rows in the KEY column. | Calculates the number of requests with a request time greater than 5.0 seconds. | `* \| SELECT COUNT(request_time)  WHERE request_time  > 5.0` |
| COUNT(1) | Indicates the number of all rows (equivalent to COUNT(\*)). | - | - |
| COUNT(DISTINCT(KEY)) | Counts the number of deduplicated rows in the KEY column. | Calculates the number of unique client IPs (UV). | `* \| SELECT COUNT(DISTINCT(remote_addr)) AS UV` |
| MAX(KEY) | Returns the maximum value of the KEY column. | Calculates the maximum request time. | `* \| SELECT MAX(request_time) AS max_request_time` |
| MIN(KEY) | Returns the minimum value of the KEY column. | Calculates the maximum request time. | `* \| SELECT MIN(request_time) AS   min_request_time` |
| SUM(KEY) | Returns the sum of the KEY column. | Calculates the total number of requested bytes. | `* \| SELECT SUM(body_bytes_sent) AS sum_bytes` |
