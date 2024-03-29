## 时间分组函数 histogram

日志服务支持按固定时间间隔对日志数据进行分组聚合统计，该函数可用于如统计每5分钟的访问次数等时间数据处理场景。

#### 函数语法

```
`histogram(date_expression,date_interval)`
```

#### 参数说明

- date_expression 必须使用 `TIMESTAMP 类型`数据格式，用户可通过 cast 函数把 ISO8601 格式的时间字符串，或者 UNIX 数值类型的时间转换为 `TIMESTAMP 类型`。
- date_interval 取值如下：

| date_interval | 取值样例                                                     |
| :------------ | :----------------------------------------------------------- |
| MINUTE        | histogram( cast(\_\_TIMESTAMP\_\_ as timestamp),INTERVAL 1 MINUTE) |
| HOUR          | histogram( cast(\_\_TIMESTAMP\_\_ as timestamp),INTERVAL 1 HOUR) |
| DAY           | histogram( cast(\_\_TIMESTAMP\_\_ as timestamp),INTERVAL 1 DAY) |
| MONTH         | histogram( cast(\_\_TIMESTAMP\_\_ as timestamp),INTERVAL 1 MONTH) |
| YEAR          | histogram( cast(\_\_TIMESTAMP\_\_ as timestamp),INTERVAL 1 YEAR) |

#### 场景示例

统计每5分钟访问次数 PV 值。

```
* | select histogram( cast(__TIMESTAMP__ as timestamp),INTERVAL 5 MINUTE) AS dt, count(*) as PV  group by dt order by dt
```

>! histogram 函数时间聚合最小粒度只能为1min，如需更小的粒度聚合，推荐使用数学取模方法。
>

```
* | select cast((__TIMESTAMP__-__TIMESTAMP__%60000) as timestamp) as dt, count(1) as PV,count (distinct(remote_addr)) as UV group by dt order by dt
```

上述公式中，%60000 表示按60秒时间进行对齐聚合。
