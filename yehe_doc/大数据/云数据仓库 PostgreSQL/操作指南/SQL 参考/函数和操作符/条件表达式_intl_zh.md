## CASE
数据库支持 CASE 表达式，和其他语言支持 IF/ELSE 功能一致。

示例：
```sql
SELECT a,
       CASE WHEN a=1 THEN 'one'
            WHEN a=2 THEN 'two'
            ELSE 'other'
       END
    FROM test;
```

## COALESCE 
COALESCE 返回参数中第一个为非 NULL 的值，如果所有参数都为 NULL，则返回 NULL。
```sql
SELECT COALESCE(null,1,2,null) ;       

 coalesce 

----------

       1
```

## NULLIF
NULLIF(value1,value2) 返回值：如果 value1 和 value2 相等，返回 NULL。否则，返回 value1。

## GREATEST 和 LEAST
这两个函数分别获取一列值中的最大值或者最小值。当所有参数都没有（为 NULL）时，则返回 NULL。
