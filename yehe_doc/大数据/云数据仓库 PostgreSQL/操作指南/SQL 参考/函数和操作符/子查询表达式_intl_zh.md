数据库还支持子查询表达式，下面列举的子查询返回值为 TRUE/FALSE。

原始表 t1 中数据如下：
```sql
select * from t1;
 a1 
----
  1
  3
  2
```

## EXISTS/NOT EXISTS
EXISTS 的参数是一个 SELECT 语句，或者说子查询。系统对子查询进行运算以判断它是否返回行。如果它至少返回一行，则 EXISTS 结果就为 TRUE；如果子查询没有返回任何行，EXISTS 的结果是 FALSE。

这个子查询通常只是运行到能判断它是否可以生成至少一行为止，而不是等到全部结束。因此，通常子查询返回结果内容不是我们正在需要关注的，因此通常优化写法为：`...WHERE EXISTS(SELECT 1 FROM ...) `。

| 示例                                                         | 结果                         |
| ------------------------------------------------------------ | ---------------------------- |
| select   a1 from t1 where EXISTS(select a1 from t1 where a1>2); | a1    ----     2     1     3 |
| select   a1 from t1 where EXISTS(select a1 from t1 where a1>3); | a1    ----                   |
| select   a1 from t1 where EXISTS(select a1 from t1 where a1>1) and a1>2; | a1    ----     3             |

## IN/NOT IN
expression IN (subquery)，右边是一个圆括弧括起来的子查询，它必须只返回一个字段。左边表达式对子查询结果的每一行进行一次计算和比较。如果找到任何相等的子查询行，则 IN 结果为 TRUE。如果没有找到任何相等行，则结果为 FALSE（包括子查询没有返回任何行的情况）。

表达式或子查询行里的 NULL 遵照 SQL 处理布尔值和 NULL 组合时的规则。如果两个行对应的字段都相等且非空，则这两行相等；如果任意对应字段不等且非空，则这两行不等；否则结果是未知（NULL）。如果每一行的结果都是不等或 NULL，并且至少有一个 NULL，则 IN 的结果是 NULL。

特别注意 NOT IN 的子查询如果存在 NULL 值，则直接返回 FALSE。

| 示例                                                         | 结果                       |
| ----------------------------------------------------- | ------------------------- |
| select   * from t1 where a1 in (select a1 from t1 where a1 > 2); | a1    ----     3   (1 row) |
| select   * from t1 where a1 in (4,5,6);                      | a1    ----   (0   rows)    |
| select   * from t1 where a1 in (2,5,6);                      | a1    ----     2   (1 row) |

## ANY/SOME
expression operator SOME/ANY (subquery)，右边是一个子查询，它必须只返回一个字段值。左边表达式使用 operator 对子查询结果的每一行进行一次计算和比较，其结果必须是布尔值。如果至少获得一个真值，则 ANY 结果为 TRUE。如果全部获得假值，则结果是 FALSE（包括子查询没有返回任何行的情况）。SOME 是 ANY 的同义词。IN 与 ANY 可以等效替换。

同 EXISTS 类似，这个与子查询结果的比较通常只是运行到能判断它是 TRUE 为止，而不是等到全部结束。

| 示例                                                         | 结果                                |
| ----------------------------------------------------- | -------------------------------- |
| `select * from t1 where a1 < any(select a1 from t1 where a1 <3);` | a1    ----     1   (1 row)          |
| `select * from t1 where a1 < some(select a1 from t1 where a1 <4);` | a1    ----     1     2   (2   rows) |
| `select * from t1 where a1 < any(select a1 from t1 where a1 <1);` | a1    ----   (0   rows)             |

## ALL
expression operator ALL (subquery)，右边是一个圆括弧括起来的子查询，它必须只返回一个字段。左边表达式使用 operator 对子查询结果的每一行进行一次计算和比较，其结果必须是布尔值。如果全部获得真值，ALL 结果为 TRUE（包括子查询没有返回任何行的情况）。如果至少获得一个假值，则结果是 FALSE。

NOT IN 等价于 ALL。

同 EXISTS 类似，这个与子查询结果的比较通常只是运行到能判断它是 FALSE 为止，而不是等到全部结束。

如果子查询为 NULL，则直接返回 TRUE。

| 示例                                                         | 结果                                      |
| ------------------------------------------------------------ | ----------------------------------------- |
| `select   * from t1 where a1 < all(select a1 from t1 where a1 <1); `| a1    ----     1     3     2   (3   rows) |
| `select   * from t1 where a1 < all(select a1 from t1 where a1 >2);` | a1    ----     2     1   (2   rows)       |
