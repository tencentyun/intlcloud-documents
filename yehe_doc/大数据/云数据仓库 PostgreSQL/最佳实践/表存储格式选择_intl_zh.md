本文介绍云数据仓库 PostgreSQL 如何选择存储格式。

## 存储格式介绍
Greenplum（以下简称 GP）有2种存储格式，Heap 表和 AO 表（AORO 表，AOCO 表）。
- Heap 表：这种存储格式是从 PostgreSQL 继承而来的，目前是 GP 默认的表存储格式，只支持行存储。
- AO 表：   AO 表最初设计是只支持 append 的（就是只能 insert），因此全称是 Append-Only，在4.3之后进行了优化，目前已经可以 update 和 delete 了，全称也改为 Append-Optimized。AO 支持行存储（AORO）和列存储（AOCO）。

## HEAP 表
Heap 表是从 PostgreSQL 继承而来，使用 MVCC 来实现一致性。如果您在创建表的时候没有指定任何存储格式，那么 GP 就会使用 Heap 表。
Heap 表支持分区表，只支持行存，不支持列存和压缩。需要注意的是在处理 update 和 delete 的时候，Heap 表并没有真正删除数据，而只是依靠 version 信息屏蔽老的数据，因此如果您的表有大量的 update 或者 delete，表占用的物理空间会不断增大，这个时候需要依靠 vacuum 来清理老数据。
Heap 表不支持逻辑增量备份，因此如果要对Heap表做快照，每次都需要导出全量数据。

建表语句：
```
CREATE TABLE heap(
	a int,
	b varchar(32)
) DISTRIBUTED BY (a);
```

### 最佳实践
- 如果该表是一张小表，例如数仓中的维度表，或者数据量在百万以下，推荐使用 Heap 表。
- 如果该表的使用场景是 OLTP 的，例如有较多的 update 和 delete，查询多是带索引的点查询等，推荐使用 Heap 表。

## AO 表
AO 表设计的目的就是为了数仓中大型的事实表。AO 表支持行存(不推荐使用)和列存，并且也支持对数据进行压缩。
AO 表无论是在表的逻辑结构还是物理结构上，都与 Heap 表有很大的不同。例如上文所述 Heap 表使用 MVCC 控制 update 和 delete 之后数据的可见性，而 AO 表则使用一个附加的 bitmap 表来实现，这个表的内容就是表示 AO 表中哪些数据是可见的。
对于有大量 update 和 delete 的 AO 表，同样需要 vacuum 进行维护，不过在 AO 表中，vacuum 需要对 bitmap 进行重置并压缩物理文件，因此通常比 Heap 的 vacuum 要慢。

### AO 列存
AOC 列存表按列方式组织数据，同时也支持列级别压缩。
建表语句如下，这里还加入了分区特性：
```
CREATE TABLE aoco(
	a int  ENCODING (compresstype=zlib, compresslevel=5),
	b int  ENCODING (compresstype=none),
	c varchar(32) ENCODING (compresstype=RLE_TYPE, blocksize=32768),
	d varchar(32),
	fdate date
)
WITH (appendonly=true, orientation=column, compresstype=zlib, compresslevel=6, blocksize=65536)
DISTRIBUTED BY (a)
PARTITION BY RANGE(fdate) 
(
	PARTITION pn START ('2018-11-01'::date) END ('2018-11-10'::date) EVERY ('1 day'::interval),
	DEFAULT PARTITION pdefault
);
```

### 压缩
压缩主要用于列存表或者追加写（"appendonly=true"）的行存表，有以下两种类型的压缩可用。
- 应用于整个表的表级压缩。
- 应用到指定列的列级压缩。用户可以为不同的列应用不同的列级压缩算法。

目前腾讯云数据仓库 PostgreSQL 支持 zstd、zlib、rle_type。

示例：
创建一个使用 zlib 压缩且压缩级别为5的列存表。
```
CREATE TABLE foo (a int, b text) 
   WITH (appendonly=true, orientation=column, compresstype=zlib, compresslevel=5);
```

创建一个使用 zstd 压缩且压缩级别为5的列存表。
```
CREATE TABLE foo (a int, b text) 
   WITH (appendonly=true, orientation=column, compresstype=zstd, compresslevel=5);
```

### 最佳实践
- AOCO 表通常用于数仓中的核心事实表，这种表字段多，数据量大，主要是用于 OLAP 场景，也就是查询的过程不会S ELECT \* FROM，而是对其中部分字段进行读取和聚合。
- 由于 AOCO 表一般用于大表，因此经常搭配压缩和分区，以减少表的实际存储量来提升性能。
- 一般情况下，压缩格式选择 zlib，压缩级别可以采用折中的4或者5，但是对于有大量重复值的字段，记得要采用 RLE_TYPE 压缩格式。
- blocksize 不要设置过大，特别是对于分区表，GP 对于每个分区的每个字段都会维护一个 buffer，blocksize 过大，会导致消耗的内存过大，通常就采用默认值32768即可。

