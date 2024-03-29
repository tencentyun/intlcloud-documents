云数据仓库 Postgresql 数据库中的表与其它关系型数据库中的表类似，不同的是表中的行被分布在不同 Segment 上，表的分布策略决定了在不同 Segment 上面的分布情况。

### 创建普通表
CREATE TABLE 命令用于创建一个表，创建表时可以定义以下内容：
- 表的列以及 [数据类型](https://intl.cloud.tencent.com/document/product/1138/45120)
- 表约束的定义
- [表分布定义](https://intl.cloud.tencent.com/document/product/1138/47248)
- [表存储格式](https://intl.cloud.tencent.com/document/product/1138/47249)
- [分区表定义](https://intl.cloud.tencent.com/document/product/1138/45025)

使用`CREATE TABLE`命令创建表，格式如下：
```
CREATE TABLE table_name ( 
[ { column_name data_type [ DEFAULT default_expr ]   -- 表的列定义
   [column_constraint [ ... ]                        -- 列的约束定义
] 
   | table_constraint                                -- 表级别的约束定义                            
   ])
   [ WITH ( storage_parameter=value [, ... ] )       -- 表存储格式定义
   [ DISTRIBUTED BY (column, [ ... ] ) | DISTRIBUTED RANDOMLY ]  -- 表的分布键定义          
   [ partition clause]                               -- 表的分区定义
```

**示例：**
以下示例中的建表语句创建了一个表，使用 **trans_id** 作为分布键，并基于 **date** 设置了 RANGE 分区功能。
```
CREATE TABLE sales (
  trans_id int,
  date date, 
  amount decimal(9,2), 
  region text)
  DISTRIBUTED BY (trans_id)  
  PARTITION BY RANGE(date)    
  (start (date '2018-01-01') inclusive
   end (date '2019-01-01') exclusive every (interval '1 month'),
   default partition outlying_dates);
```

## 创建临时表
临时表（Temporary Table）会在会话结束时自动删除，或选择性地在当前事务结束的时候删除，用于存储临时中间结果。创建临时表的命令如下：
```
CREATE TEMPORARY TABLE table_name(…)
    [ON COMMIT {PRESERVE ROWS | DELETE ROWS | DROP}]
```

**说明:**临时表的行为在事务块结束时的行为可以通过上述语句中的ON COMMIT来控制。

- PRESERVE ROWS：在事务结束时候保留数据，这是默认的行为。
- DELETE ROWS：在每个事务块结束时，临时表的所有行都将被删除。
- DROP：在当前事务结束时，会删除临时表。

**示例：**
创建一个临时表，事务结束时候删除该临时表。
```
CREATE TEMPORARY TABLE temp_foo (a int, b text) ON COMMIT DROP;
```

## 表约束的定义
您可以在列和表上定义约束来限制表中的数据，但是有以下一些限制：
- CHECK 约束引用的列只能在其所在的表中。
- UNIQUE 和 PRIMARY KEY 约束必须包含分布键列，UNIQUE 和 PRIMARY KEY 约束不支持追加优化表和列存表。
- 允许 FOREIGN KEY 约束在云数仓 Postgresql 上无效。

实际使用约束命令如下:
```
UNIQUE ( column_name [, ... ] )
   | PRIMARY KEY ( column_name [, ... ] ) 
   | CHECK ( expression )
```

### 检查约束
检查约束（Check Constraints）指定列中的值必须满足一个布尔表达式，例如：
```
CREATE TABLE products
            ( product_no integer,
              name text,
              price numeric CHECK (price > 0) );
```

### 非空约束（Not-Null Constraints）
非空约束（Not-Null Constraints）指定列不能有空值，例如：
```
CREATE TABLE products
       ( product_no integer NOT NULL,
         name text NOT NULL,
         price numeric );
```



### 唯一约束（Unique Constraints）
唯一约束（Unique Constraints）确保一列或者一组列中包含的数据对于表中所有的行都是唯一的。包含唯一约束的表必须是哈希分布，并且约束列需要包含分布键列，例如：
```
CREATE TABLE products
       ( product_no integer UNIQUE,
         name text,
         price numeric)
      DISTRIBUTED BY (product_no);
```
>! 仅行存 HEAP 表支持主键约束，APPEDN ONLY 表均不支持主键约束。

### 主键约束（Primary Keys Constraints）
主键约束（Primary Keys Constraints）是一个 UNIQUE 约束和一个 NOT NULL 约束的组合。包含主键约束的表必须是哈希分布，并且约束列需要包含分布键列。如果一个表具有主键，这个列（或者这一组列）会被默认选中为该表的分布键，例如：
```
CREATE TABLE products
       ( product_no integer PRIMARY KEY,
         name text,
         price numeric)
      DISTRIBUTED BY (product_no);
```
>! 仅行存 HEAP 表支持主键约束，APPEDN ONLY 表均不支持主键约束。



