Many business use cases have the tag-based query feature. If the data volume and tag value quantity are high, a large amount of storage capacity will be used, and the performance will be poor. Therefore, how to filter target resources efficiently and quickly without taking up too much storage space has become a challenge for business management optimization.

This document describes how to easily search in an ultra high number of tags based on the pg_roaringbitmap extension.

## pg_roaringbitmap Overview
pg_roaringbitmap is a compressed bitmap storage extension based on roaring bitmap. It supports roaring bitmap access as well as set, aggregation, and other operations.

## Roaring Bitmap Usage
Roaring bitmap is often used to store user attribute tags in business use cases. You can create, read, update, and delete these attribute tags and filter specific users by tag union, intersection, etc. In this way, you can quickly find what you want from a massive amount of attribute data. This not only improves the performance, but also reduces the used storage space, making it very useful for big data analysis scenarios.
For example, in traditional mode, a music application has a user tag list as follows:

| User ID | Username | Interest Tag |
|---------|---------|---------|
| 1 | John | {Classical, jazz, R&B, country} |
| 2 | Jane | {Folk, instrumental} |
| 3 | Harry | {Hip hop, jazz, R&B, reggae} |
| ... | ... | ... |
| 1000000000 | Text 2 | {Rock} |

To find all users who like instrumental music, the system needs to search for them against the interest tag column, find rows with "instrumental" in the tag, and return the data to the application.
Generally, the simplest way is to create a user interest table in the database according to the structure of the above table first, and then run an array query statement to find interest tags for inclusion search. However, if there are high volumes of data and tag values, more storage space will be used, and the performance will be very poor. Therefore, you need to find an alternative. You can split this table into three tables, use the interest tag as the primary key, and store tagged users as bitmaps as shown below:

**User table:**

| User ID | Username |
|---------|---------|
| 1 | John |
| 2 | Jane |
| N | ... |

**Tag table:**

| Tag ID | Username |
|---------|---------|
| 1 | Classical |
| 2 | Folk |
| N | ... |

**User tag table:**

| Tag ID | Username |
|---------|---------|
| 1 | [ 1,3,7,123,423 ] |
| 2 | [ 5,31] |
| N | ... |

When you need to find users who like listening to classical and folk music at the same time, you can directly perform a bitmap query by user ID in the user tag table. This can greatly improve the performance and reduce the capacity usage.

## Query Performance Comparison Between Traditional Method and Roaring Bitmap Method
### Preparing test scenario
1. Create a function for random character generation.
```
create or replace function random_string(length integer) returns text as
$$
declare
chars text[] := '{0,1,2,3,4,5,6,7,8,9,A,B,C,D,E,F,G,H,I,J,K,L,M,N,O,P,Q,R,S,T,U,V,W,X,Y,Z,a,b,c,d,e,f,g,h,i,j,k,l,m,n,o,p,q,r,s,t,u,v,w,x,y,z}';
result text := '';
i integer := 0;
length2 integer := (select trunc(random() * length + 1));
begin
if length2 < 0 then
raise exception 'Given length cannot be less than 0';
end if;
for i in 1..length2 loop
result := result || chars[1+random()*(array_length(chars, 1)-1)];
end loop;
return result;
end;
$$ language plpgsql;
```
2. Create a function that generates an array of random integers.
```
create or replace function random_int_array(int, int)
returns int[] language sql as
$$
select array_agg(round(random()* $1)::int)
from generate_series(1, $2)
$$;
```
3. Create a function that generates an array of random characters.
```
create or replace function random_string_array(int, int)
returns TEXT[] language sql as
$$
select array_agg(random_string($1)) from generate_series(1, $2);
$$;
```

### Scheme 1: Traditional method
One table does it all.
1. Create a table containing all the data.
```
create table account(
uin bigint primary KEY,
name varchar,
tag TEXT []
);
```
2. Insert the data of ten million simulated accounts with the function as described in the preparations, and then create a GIN index.
```
insert into account select generate_series(1,10000000), random_string(20),random_string_array(5,10);
create index tag_inx on account USING GIN(tag);
```
3. Run a query to list users with tags `GN` and `o`.
```
explain analyze select uin,name from account where tag @>ARRAY['GN','o'];

QUERY PLAN

----------------------------------------------------------------------------------------------------
-----------------
Bitmap Heap Scan on account (cost=52.81..466.86 rows=105 width=19) (actual time=4.263..4.502 rows=
184 loops=1)
Recheck Cond: (tag @> '{GN,o}'::text[])
Heap Blocks: exact=184
-> Bitmap Index Scan on tag_inx (cost=0.00..52.78 rows=105 width=0) (actual time=4.240..4.240 r
ows=184 loops=1)
Index Cond: (tag @> '{GN,o}'::text[])
Planning Time: 0.108 ms
Execution Time: 4.528 ms
```
4. Run a query to list xx users with tags `lvXe` and `Zt` (the query will be slow when executed for the first time).
```
explain analyze select count(uin) from account where tag && ARRAY['lvXe','Zt'];

----------------------------------------------------------------------------------------------------
--------------------------
Aggregate (cost=21816.39..21816.40 rows=1 width=8) (actual time=8.236..8.238 rows=1 loops=1)
-> Bitmap Heap Scan on account (cost=109.08..21800.56 rows=6332 width=8) (actual time=1.655..7.
901 rows=5390 loops=1)
Recheck Cond: (tag && '{lvXe,Zt}'::text[])
Heap Blocks: exact=5327
-> Bitmap Index Scan on tag_inx (cost=0.00..107.49 rows=6332 width=0) (actual time=0.962.
.0.962 rows=5390 loops=1)
Index Cond: (tag && '{lvXe,Zt}'::text[])
Planning Time: 0.110 ms
Execution Time: 8.270 ms
```

### Scheme 2: Optimized scheme
In order to reduce the performance loss caused by the types of tag fields in the query, change the actual `tag` in the above table to `tagid`.
1. Introduce a new tag dictionary table.
```
create table tag_dict (  
tagid int primary key,
taginfo text
);
```
2. Suppose there are 100,000 dictionary types in total.
```
insert into tag_dict select generate_series(1,100000), md5(random()::text);
```
3. Create another table to store user and tag information.
```
create table account1(
uin bigint primary KEY,
name varchar,
tag INT []
);
```
4. Insert the data of ten million accounts.
```
insert into account1 select generate_series(1,10000000), random_string(20),random_int_array(100000,10);
```
5. List users with both tag IDs 100 and 5711.
**Before indexing**:
```
test=> explain analyze select uin,name from account1 where tag @> ARRAY[100,5711];
QUERY PLAN
-----------------------------------------------------------------------------------------------------------------------------
Gather (cost=1000.00..191007.68 rows=250 width=19) (actual time=982.585..1000.806 rows=0 loops=1)
Workers Planned: 2
Workers Launched: 2
-> Parallel Seq Scan on account1 (cost=0.00..189982.68 rows=104 width=19) (actual time=962.640..962.640 rows=0 loops=3)
Filter: (tag @> '{100,5711}'::integer[])
Rows Removed by Filter: 3333333
Planning Time: 0.205 ms
JIT:
Functions: 12
Options: Inlining false, Optimization false, Expressions true, Deforming true
Timing: Generation 2.280 ms, Inlining 0.000 ms, Optimization 1.176 ms, Emission 14.189 ms, Total 17.645 ms
Execution Time: 1001.574 ms
(12 rows)
```
**Add an index:**
```
create index tag_inx_2 on account1 USING GIN(tag);
```
**After indexing:**
```
test=> explain analyze select uin,name from account1 where tag @> ARRAY[100,5711];
QUERY PLAN
---------------------------------------------------------------------------------------------------------------------
Bitmap Heap Scan on account1 (cost=49.94..1021.13 rows=250 width=19) (actual time=0.126..0.127 rows=0 loops=1)
Recheck Cond: (tag @> '{100,5711}'::integer[])
-> Bitmap Index Scan on tag_inx_2 (cost=0.00..49.87 rows=250 width=0) (actual time=0.124..0.124 rows=0 loops=1)
Index Cond: (tag @> '{100,5711}'::integer[])
Planning Time: 0.410 ms
Execution Time: 0.171 ms
(6 rows)
```
6. List users with both tag IDs 61568 and 97350.
```
test=> explain analyze select uin,name from account1 where tag @> ARRAY[61568,97350];
QUERY PLAN
---------------------------------------------------------------------------------------------------------------------
Bitmap Heap Scan on account1 (cost=49.94..1021.13 rows=250 width=19) (actual time=0.130..0.131 rows=1 loops=1)
Recheck Cond: (tag @> '{61568,97350}'::integer[])
Heap Blocks: exact=1
-> Bitmap Index Scan on tag_inx_2 (cost=0.00..49.87 rows=250 width=0) (actual time=0.125..0.125 rows=1 loops=1)
Index Cond: (tag @> '{61568,97350}'::integer[])
Planning Time: 0.071 ms
Execution Time: 0.151 ms
(7 rows)
```
7. List xx users who share interests with xx users (tag IDs 100 and 5711).
```
test=> explain analyze select count(uin) from account1 where tag && ARRAY[61568,97350];
QUERY PLAN

---------------------------------------------------------------------------------------------------------------------------------
------
Gather (cost=1961.06..173801.15 rows=99750 width=19) (actual time=5.020..28.885 rows=2066 loops=1)
Workers Planned: 2
Workers Launched: 2
-> Parallel Bitmap Heap Scan on account1 (cost=961.06..162826.15 rows=41562 width=19) (actual time=1.623..3.305 rows=689 loo
ps=3)
Recheck Cond: (tag && '{61568,97350}'::integer[])
Heap Blocks: exact=2053
-> Bitmap Index Scan on tag_inx_2 (cost=0.00..936.12 rows=99750 width=0) (actual time=0.685..0.685 rows=2066 loops=1)
Index Cond: (tag && '{61568,97350}'::integer[])
Planning Time: 0.082 ms
JIT:
Functions: 12
Options: Inlining false, Optimization false, Expressions true, Deforming true
Timing: Generation 2.078 ms, Inlining 0.000 ms, Optimization 0.270 ms, Emission 3.489 ms, Total 5.836 ms
Execution Time: 29.725 ms
(14 rows)
```

### Scheme 3: Roaring bitmap
1. Create the extension first. It is integrated in TencentDB for PostgreSQL natively, so you don't need to care about compilation and other operations. You can directly create it in the database.
```
create extension roaringbitmap;
```
2. Create a tag-user mapping table.
```
create table tag_uin_list(
tagid int primary key,
uin_offset int,
uinbits roaringbitmap
);
```
3. Insert 100,000 tags and corresponding user data according to the previously created tag table.
```
insert into tag_uin_list
select tagid, uin_offset, rb_build_agg(uin::int) as uinbits from
(
select
unnest(tag) as tagid,
(uin / (2^31)::int8) as uin_offset,
mod(uin, (2^31)::int8) as uin
from account1
) t
group by tagid, uin_offset;
```
4. Query the number of users with tags 1, 3, 10, and 200.
```
explain analyze select sum(ub) from
(
select uin_offset,rb_or_cardinality_agg(uinbits) as ub
from tag_uin_list
where tagid in (1,3,10,200)
group by uin_offset
) t;


QUERY PLAN

---------------------------------------------------------------------------------------------------------------------------------
------------
Aggregate (cost=32.47..32.48 rows=1 width=32) (actual time=0.964..0.966 rows=1 loops=1)
-> GroupAggregate (cost=32.42..32.46 rows=1 width=12) (actual time=0.955..0.956 rows=1 loops=1)
Group Key: tag_uin_list.uin_offset
-> Sort (cost=32.42..32.43 rows=4 width=22) (actual time=0.107..0.109 rows=4 loops=1)
Sort Key: tag_uin_list.uin_offset
Sort Method: quicksort Memory: 25kB
-> Bitmap Heap Scan on tag_uin_list (cost=17.20..32.38 rows=4 width=22) (actual time=0.044..0.067 rows=4 loops=1
)
Recheck Cond: (tagid = ANY ('{1,3,10,200}'::integer[]))
Heap Blocks: exact=4
-> Bitmap Index Scan on tag_uin_list_pkey (cost=0.00..17.20 rows=4 width=0) (actual time=0.031..0.031 rows
=4 loops=1)
Index Cond: (tagid = ANY ('{1,3,10,200}'::integer[]))
Planning Time: 0.289 ms
Execution Time: 1.083 ms
(13 rows)
```
5. View the list of users with tags 1, 3, 10, and 200.
```
explain analyze select uin_offset,rb_or_agg(uinbits) as ub
from tag_uin_list
where tagid in (1,3,10,200)
group by uin_offset;
QUERY PLAN

---------------------------------------------------------------------------------------------------------------------------------
------
GroupAggregate (cost=32.42..32.46 rows=1 width=36) (actual time=0.246..0.246 rows=1 loops=1)
Group Key: uin_offset
-> Sort (cost=32.42..32.43 rows=4 width=22) (actual time=0.043..0.045 rows=4 loops=1)
Sort Key: uin_offset
Sort Method: quicksort Memory: 25kB
-> Bitmap Heap Scan on tag_uin_list (cost=17.20..32.38 rows=4 width=22) (actual time=0.029..0.036 rows=4 loops=1)
Recheck Cond: (tagid = ANY ('{1,3,10,200}'::integer[]))
Heap Blocks: exact=4
-> Bitmap Index Scan on tag_uin_list_pkey (cost=0.00..17.20 rows=4 width=0) (actual time=0.021..0.021 rows=4 loops=1)
Index Cond: (tagid = ANY ('{1,3,10,200}'::integer[]))
Planning Time: 0.119 ms
Execution Time: 0.310 ms
(12 rows)
```

### Viewing index size and table size
```
test=> select relname, pg_size_pretty(pg_relation_size(relid)) from pg_stat_user_tables where schemaname='public' order by pg_relation_size(relid) desc;
   relname    | pg_size_pretty 
--------------+----------------
 account      | 1545 MB
 account1     | 1077 MB
 t_user       | 651 MB
 tag_dict     | 6672 kB
 tag_uin_list | 5888 kB
(5 rows)

test=> select indexrelname, pg_size_pretty(pg_relation_size(relid)) from pg_stat_user_indexes where schemaname='public' order by pg_relation_size(relid) desc;
   indexrelname    | pg_size_pretty 
-------------------+----------------
 tag_inx           | 1545 MB
 account_pkey      | 1545 MB
 tag_inx_2         | 1077 MB
 account1_pkey     | 1077 MB
 t_user_pkey       | 651 MB
 tag_dict_pkey     | 6672 kB
 tag_uin_list_pkey | 5888 kB
(7 rows)
```

### Conclusion
The query performance comparison of different schemes is as follows:

| Query Item | Scheme 1 | Scheme 2 | Roaring Bitmap Scheme |
|---------|---------|---------|---------|
| Query the list of users with the specified tag | 4.528 ms | 0.151 ms | 0.310 ms |
| Query the number of users with the same tag | 8.27 ms | 29.725 ms | 1.083 ms |
| Storage capacity statistics | 4,635 MB | 3,244.344 MB | 1,237.12 MB |

As can be clearly seen from the above three schemes, the optimization effect is very obvious. The roaring bitmap scheme works very well in terms of query speed and storage capacity usage.


