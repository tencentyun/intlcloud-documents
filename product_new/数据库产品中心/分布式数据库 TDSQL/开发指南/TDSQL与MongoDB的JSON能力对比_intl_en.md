TDSQL (MySQL 5.7 kernel) currently supports JSON. For more information, see [MySQL's official JSON documentation](https://dev.mysql.com/doc/refman/5.7/en/json-function-reference.html).

## Precautions for Using JSON in TDSQL
1. A JSON field cannot be used as a shardkey;
2. Mixed-type sorting is not supported for aggregation operations of JSON type (such as `orderby` and `groupby`); for example, you cannot compare or sort string type with int type, and sorting is supported only for value type but not other types such as string.

## Comparison of JSON Capabilities Between TDSQL and MongoDB
### Syntax for table creation
**TDSQL**
```
Create table inventory(id int primary key auto_increment, value json) shardkey=id;
```
**MongoDB**
```
sh.shardCollection("test.inventory", {"_id":"hashed"})
```
### **INSERT/UPDATE/DELETE Document**
<table>
  <tbody>
   <tr>
    <td>
     <span style="font-size:14px;"></span><br>
    </td>
    <td>
     <span style="font-size:14px;">MongoDB</span><br>
    </td>
    <td>
     <span style="font-size:14px;">TDSQL</span><br>
    </td>
   </tr>
   <tr>
    <td >
     <span style="font-size:14px;">Insert a single file</span><br>
    </td>
    <td>
     <span style="font-size:14px;">db.inventory.insertOne(<br>
  &emsp; { item: "canvas", qty: 100, tags: ["cotton"], size: { h: 28, w: 35.5, uom: "cm" } }<br>
)</span><br>
    </td>
    <td>
     <span style="font-size:14px;">Insert into inventory(value) values(<br>
 &emsp; '{ "item": "canvas", "qty": 100, "tags": ["cotton"], "size": { "h": 28, "w": 35.5, "uom": "cm" } }'<br>
);</span><br>
    </td>
   </tr>
    <td>
     <span style="font-size:14px;">Insert multiple files</span><br>
    </td>
    <td>
     <span style="font-size:14px;">db.inventory.insertMany([<br>&emsp;
   { item: "journal", qty: 25, size: { h: 14, w: 21, uom: "cm" }, status: "A" },<br>&emsp;
   { item: "mat", qty: 35, size: { h: 27.9, w: 35.5, uom: "cm" }, status: "A" },<br>&emsp;
   { item: "paper", qty: 100, size: { h: 8.5, w: 11, uom: "in" }, status: "D" }<br>
]);<br></span><br>
    </td>
    <td>
     <span style="font-size:14px;">insert into inventory(value) values<br>&emsp;
   ('{ "item": "journal", "qty": 25, "size": { "h": 14, "w": 21, "uom": "cm" }, "status": "A"  }'),<br>&emsp;
   ('{ "item": "mat", "qty": 35, "size": { "h": 27.9, "w": 35.5, "uom": "cm" }, "status": "A" }'),<br>&emsp;
   ('{ "item": "paper", "qty": 100, "size": { "h": 8.5, "w": 11, "uom": "in" }, "status": "D" }') </span><br>
    </td>
   </tr>
   <tr>
      <td>
     <span style="font-size:14px;">Update a single file</span><br>
    </td>
    <td>
     <span style="font-size:14px;">db.inventory.updateOne(<br>&emsp;
   { item: "paper" },<br>&emsp;
   {<br>&emsp;
     $set: { "size.uom": "cm", status: "P" },<br>&emsp;
   }<br>
)<br><br>If no shardkey is carried, an error will be reported; otherwise, the statement can be executed correctly</span>
    </td>
    <td>
     <span style="font-size:14px;">update inventory set value=json_set(value, <br>
    "$.size.uom", "cm", <br>
    "$.status", "P") <br>
where value->"$.item"="paper" limit 1;<br>
<br>A statement without shardkey will be executed on multiple nodes and multiple data entries may be modified, while a statement with shardkey can modify one data entry precisely
</span><br>
    </td>
   </tr>
   <tr>  
    <td>
     <span style="font-size:14px;">Update multiple files</span><br>
    </td>
    <td>
     <span style="font-size:14px;">db.inventory.updateMany(<br>
   { "qty": { $lt: 50 } },<br>
   {<br>
     $set: { "size.uom": "in", status: "P" },<br>
   }
)</span><br>
    </td>
    <td>
     <span style="font-size:14px;">update inventory set value=json_set(value, <br>
    "$.size.uom", "in", <br>
    "$.status", "P") <br>
where value->"$.qty"<50 ;
</span><br>
    </td>
		   </tr>  
    <td>
     <span style="font-size:14px;">Replace a file</span><br>
    </td>
    <td>
     <span style="font-size:14px;">db.inventory.replaceOne(<br>
   { item: "paper" },<br>
   { item: "paper", instock: [ { warehouse: "A", qty: 60 }, { warehouse: "B", qty: 40 } ] }
)<br>
)<br><br>If no shardkey is carried, an error will be reported; otherwise, the statement can be executed correctly
</span><br>
    </td>
    <td>
     <span style="font-size:14px;">update inventory set value= '{ "item": "paper", "instock":<br> [ { "warehouse": "A", "qty": 60 }, <br>{ "warehouse": "B", "qty": 40 }]}'<br>
where value->"$.item"="paper" limit 1
)
<br><br>A statement without shardkey will be executed on multiple nodes and multiple data entries may be modified, while a statement with shardkey can modify one data entry precisely
</span><br>
    </td>
   </tr>
 <tr>  
    <td>
     <span style="font-size:14px;">Delete only one eligible file</span><br>
    </td>
    <td>
     <span style="font-size:14px;">db.inventory.deleteOne( { status: "A" } )
		 <br>If no shardkey is carried, an error will be reported; otherwise, the statement can be executed correctly</span><br>
    </td>
    <td>
     <span style="font-size:14px;">delete from inventory where value->"$.status"="A" limit 1;<br>
A statement without shardkey will be executed on multiple nodes and multiple data entries may be modified, while a statement with shardkey can modify one data entry precisely
</span><br>
    </td>
		   </tr>    
	<tr>  
    <td>
     <span style="font-size:14px;">Delete all eligible files</span><br>
    </td>
    <td>
     <span style="font-size:14px;">db.inventory.deleteMany({ status : "A" })
)</span><br>
    </td>
    <td>
     <span style="font-size:14px;">delete from inventory where value->"$.status"="A";
</span><br>
    </td>
		   </tr>  
  </tbody>
</table>

### QUERY Document
||MongoDB|	TDSQL|
|---- |-----| ----|
| Pre-insert data	|db.inventory.insertMany([ <br>&emsp;{ item: "canvas", qty: 100, size: { h: 28, w: 35.5, uom: "cm" }, status: "A" , tags: ["blank", "red"], dim_cm: [ 14, 21 ] , instock: [ { warehouse: "A", qty:, 5 }, { warehouse: "C", qty: 15 } ] } ,<br>&emsp;{ item: "journal", qty: 25, size: { h: 14, w: 21, uom: "cm" }, status: "A" , tags: ["red", "blank"], dim_cm: [ 14, 21 ] , instock: [ { warehouse: "C", qty: 5 } ] }, <br>&emsp;{ item: "mat", qty: 85, size: { h: 27.9, w: 35.5, uom: "cm" }, status: "D" , tags: ["red", "blank", "plain"], dim_cm: [ 14, 21 ] , instock: [ { warehouse: "A", qty: 60 }, { warehouse: "B", qty: 15 } ] },<br>&emsp;{ item: "mousepad", qty: 25, size: { h: 19, w: 22.85, uom: "cm" }, status: "P" , tags: ["blank", "red"], dim_cm: [ 22.85, 30 ] , instock: [ { warehouse: "A", qty: 40 }, { warehouse: "B", qty: 5 } ] },<br>&emsp;{ item: "notebook", qty: 50, size: { h: 8.5, w: 11, uom: "in" }, status: "P" , tags: ["blue"], dim_cm: [ 10, 15.25 ] , instock: [ { warehouse: "B", qty: 15 }, { warehouse: "C", qty: 35 } ] }]); |	insert into inventory(value) values<br>('{ "item": "canvas", "qty": 100, "size": { "h": 28, "w": 35.5, "uom": "cm" }, "status": "A" , "tags": ["blank", "red"], "dim_cm": [ 14, 21 ] , "instock": [ { "warehouse": "A", "qty": 5 }, { "warehouse": "C", "qty": 15 } ] }'),<br>&emsp;('{ "item": "journal", "qty": 25, "size": { "h": 14, "w": 21, "uom": "cm" }, "status": "A" , "tags": ["red", "blank"], "dim_cm": [ 14, 21 ] , "instock": [ { "warehouse": "C", "qty": 5 } ] }'),<br>&emsp;('{ "item": "mat", "qty": 85, "size": { "h": 27.9, "w": 35.5, "uom": "cm" }, "status": "D" , "tags": ["red", "blank", "plain"], "dim_cm": [ 14, 21 ] , "instock": [ { "warehouse": "A", "qty": 60 }, { "warehouse": "B", "qty": 15 } ] }'),<br>&emsp;('{ "item": "mousepad", "qty": 25, "size": { "h": 19, "w": 22.85, "uom": "cm" }, "status": "P" , "tags": ["blank", "red"], "dim_cm": [ 22.85, 30 ] , "instock": [ { "warehouse": "A", "qty": 40 }, { "warehouse": "B", "qty": 5 } ] }'),<br>&emsp;('{ "item": "notebook", "qty": 50, "size": { "h": 8.5, "w": 11, "uom": "in" }, "status": "P" , "tags": ["blue"], "dim_cm": [ 10, 15.25 ] , "instock": [ { "warehouse": "B", "qty": 15 }, { "warehouse": "C", "qty": 35 } ] }') |
| Access any member in JSON via path syntax |	 Supported	 | Supported |
| Query files |db.inventory.find( { status: "D" } )|	SELECT * FROM inventory WHERE value->"$.status" = "D";
||db.inventory.find( { status: { $in: [ "A", "D" ] } } )	|SELECT * FROM inventory WHERE cast(value->"$.status" as char(4)) in ('"A"', '"D"');<br><br>`value->"$.status"` is of JSON type. MySQL does not support IN comparisons of JSON type, so you need to convert the type, and "A" must be quoted with single quotation marks.
| Query embedded/nested documents |db.inventory.find( { size: { h: 14, w: 21, uom: "cm" } } )<br><br>When filtering according to the matching conditions, MongoDB may also take into account the order of fields; for example, no results will be obtained for <br>db.inventory.find(  { size: { w: 21, h: 14, uom: "cm" } }  )<br>	|SELECT \* FROM inventory WHERE value->"$.size" = cast('{"h": 14, "w": 21, "uom": "cm"}' as json)<br><br>MySQL will not take into account the order of fields for such type of queries. <br>SELECT * FROM inventory WHERE value->"$.size" = cast('{"w": 21, "h": 14, "uom": "in"}' as json) <br>will filter out the same results |
| Query an array | db.inventory.find( { tags: ["red", "blank"] } )<br>The order of elements in the array should be taken into account 	|select * from inventory where value->"$.tags"=cast('["red", "blank"]' as json);<br>The order of elements in the array should be taken into account |
 | Find arrays containing "red" and "blank" elements, regardless of the array element order or other elements |	db.inventory.find( { tags: { $all: ["red", "blank"] } } )|select * from inventory where json_contains(value->"$.tags",cast('["red", "blank"]' as json))=1;|
| Specify multiple conditions for array elements | db.inventory.find( { dim_cm: { $gt: 15, $lt: 20 } } )<br>Select at least one element which is greater than 15, or less than 20, or greater than 15 but less than 20 from the array	 | Not supported |
	||db.inventory.find( { dim_cm: { $elemMatch: { $gt: 22, $lt: 30 } } } ) Select at least one element which is greater than 22 but less than 30 from the array	 | Not supported |
| Query elements by array index position |db.inventory.find( { "dim_cm.1": { $gt: 25 } } )	|select * from inventory where value->"$.dim_cm[1]" < 25|
| Query arrays by array length |	db.inventory.find( { "tags": { $size: 3 } } )	|select * from inventory where json_length(value->"$.tags") = 3;|
| Query an array of elements |db.inventory.find( { tags: "red" } )	|select * from inventory where json_contains(value->"$.tags",cast('"red"' as json))=1;|
| Query an array of embedded documents |db.inventory.find( { "instock": { warehouse: "A", qty: 5 } } )<br>The order of (warehouse, qty) should be taken into account <br>db.inventory.find( { "instock": { $elemMatch: { qty: 5, warehouse: "A" } } } )<br>The order of (warehouse, qty) does not matter 	|select * from inventory where json_contains(value->"$.instock", cast('{ "warehouse": "A", "qty": 5 }' as json))=1;<br>The order of (warehouse, qty) does not matter |
| Specify query conditions in the fields of embedded document array |db.inventory.find( { 'instock.qty': { $lte: 20 } } )|	//Not supported (because qty is a field in the array's instock, and it can only be accessed through instock[index].qty. The access method of instock.qty is not supported in MySQL) |

### INDEXES
<table>
  <tbody>
   <tr>
    <td>
     <span style="font-size:14px;"></span><br>
    </td>
    <td>
     <span style="font-size:14px;">MongoDB</span><br>
    </td>
    <td>
     <span style="font-size:14px;">TDSQL</span><br>
    </td>
   </tr>
   <tr>
    <td >
     <span style="font-size:14px;">Single field index</span><br>
    </td>
    <td>
     <span style="font-size:14px;">Create an index on qty
db.inventory.createIndex( { qty: <br>1 }
)</span><br>
    </td>
    <td>
     <span style="font-size:14px;">MySQL does not support creating indices directly on JSON fields. Virtual columns must be created for type conversion. For example, you can use value->"$.qty" as the index <br>alter table inventory add value_qty int generated always as (value->"$.qty") virtual;
create index idx on inventory(value_qty);</span><br>
    </td>
   </tr>
    <td>
     <span style="font-size:14px;">Compound index</span><br>
    </td>
    <td>
     <span style="font-size:14px;">db.inventory.createIndex( { "item": 1, "qty": 1 } )<br></span><br>
    </td>
    <td>
     <span style="font-size:14px;">alter table inventory add value_item varchar(50) generated always as (value->"$.item") virtual;<br><br>alter table inventory add value_qty int generated always as (value->"$.qty") virtual;<br><br>create index idx_1 on inventory(value_item, value_qty);
</span><br>
    </td>
   <tr>
    <td>
     <span style="font-size:14px;">
Hash index</span><br>
    </td>
    <td>
     <span style="font-size:14px;">db.inventory.createIndex( { qty: "hashed" } )</span>
    </td>
    <td>
     <span style="font-size:14px;">Not supported by InnoDB
</span><br>
    </td>
   </tr>
   <tr>  
    <td>
     <span style="font-size:14px;">Multi-key index</span><br>
    </td>
    <td>
     <span style="font-size:14px;">Multi-key indexing is to index the fields containing array values. MongoDB creates an index key for each element in the array</span><br>
    </td>
    <td>
     <span style="font-size:14px;">Not supported
</span><br>
    </td>
  </tr>  
    <td>
     <span style="font-size:14px;">Unique index</span><br>
    </td>
    <td>
     <span style="font-size:14px;">db.inventory.createIndex( { "_id":1, "qty": 1 }, {unique:true} )<br>Shardkey is required as the prefix
</span><br>
    </td>
		<td>
     <span style="font-size:14px;">alter table inventory add value_qty int generated always as (value->"$.qty") virtual;<br><br>create unique index idx on inventory(id, value_qty);<br>Shardkey should be included in the index
</span><br>
    </td>
   </tr>
 <tr>  
    <td>
     <span style="font-size:14px;">Text index</span><br>
    </td>
    <td>
     <span style="font-size:14px;">Insert data<br>
sh.shardCollection("test.stores", {"_id":"hashed"}}<br><br>
db.stores.insertMany(<br>
   [<br>
     { _id: 1, name: "Java Hut", description: "Coffee and cakes" },<br>
     { _id: 2, name: "Burger Buns", description: "Gourmet hamburgers" },<br>
     { _id: 3, name: "Coffee Shop", description: "Just coffee" },<br>
     { _id: 4, name: "Clothes Clothes Clothes", description: "Discount clothing" },<br>
     { _id: 5, name: "Java Shopping", description: "Indonesian goods" }<br>
   ]
)
<br><br>
Create an index<br><br>
db.stores.createIndex( { name: "text", description: "text" } )<br><br>
Find by index<br><br>
db.stores.find( { $text: { $search: "java coffee shop" } } )</span><br>
    </td>
    <td>
     <span style="font-size:14px;">Not supported by TDSQL currently. This can be done in the following way in MySQL 5.7<br><br>
Insert data<br>
create table stores(id int primary key auto_increment, value json);<br>
insert into stores(value) values('{ "name": "Java Hut", "description": "Coffee and cakes" }'),<br>
('{ "name": "Burger Buns", "description": "Gourmet hamburgers" }'),<br>
('{ "name": "Coffee Shop", "description": "Just coffee" }'),<br>
('{ "name": "Clothes Clothes Clothes", "description": "Discount clothing" }'),<br>
('{ "name": "Java Shopping", "description": "Indonesian goods" }');<br><br>
Create a generated column<br><br>
alter table stores add value_name varchar(50) generated always as (value->"$.name") stored;<br><br>
alter table stores add value_description varchar(50) generated always as (value->"$.description") stored;<br><br>

create FULLTEXT index full_idx on stores(value_name, value_description);<br>
(<br>
**If generated column is stored, the performance of insert and update may be affected. For more information, please see**<br>
<a class=n href=http://mysqlserverteam.com/virtual-columns-and-effective-functional-indexes-in-innodb/>http://mysqlserverteam.com/virtual-columns-and-effective-functional-indexes-in-innodb/</a> 
<br>
)
</span><br>
   </td>
		   </tr>    
 
  </tbody>
</table>

### SHARDING

||MongoDB|	TDSQL|
|---- |-----| ----|
|Ranged sharding	|Supported	| Not supported
|Hashed sharding|db.t1.createIndex({"key1":"hashed"})<br>sh.shardCollection("test.t1", {"key1":"hashed"})<br>db.t1.insertOne({"key1":"value1","key2":"value2"})|TDSQL does not need to create the hashed index in advance <br><br>create table t1(key1 varchar(20), value json) shardkey=key1;<br>insert into t1(key1, value) values("value1", '{"key2":"value2"}');<br><br>TDSQL does not support hashed sharding according to any field in JSON. If necessary, take the field serving as the shardkey out as an independent column
| Modify a non-sharded table containing data into a sharded table | 	Supported	 | Not supported |
MongoDB uses an architecture similar to the sharding-based distributed architecture of TDSQL, so they have their own advantages in terms of horizontal scaling and disaster recovery, which will not be detailed in this document.

### SHARD INDEX
The indices of both TDSQL and MongoDB are created on shards, and only the index containing shardkey has the globally unique constraint effect. No matter whether it is compound indices containing shardkey or indices created on the shardkey itself, the shard is located based on the shardkey first, and this index is used on the corresponding shard. Without shardkey, the query will be sent to all shards.

### JOIN
MongoDB only supports left join operations of multiple tables in a non-sharded table, but does not support join operations in a shard table. The following code shows the specific implementation method:
```
Insert data:
db.users.insertMany([{
		"email" : "admin@gmail.com",
		"userId" : "AD",
		"userName" : "admin"
	},
	
	{ 
		"email" : "admin1@gmail.com",
		"userId" : "AD",
		"userName" : "admin1"
	}
]);

db.userinfo.insertMany([{
		"userId" : "AD",
		"phone" : "0000000000"
	},
	{
		"userId" : "AD",
		"phone" : "0000000000"
	}
]);

db.userrole.insertMany([{
		"userId" : "AD",
		"role": "admin"
	},
	{
		"userId" : "AC",
		"role" : "admin"
	}
]);

Left join:
db.users.aggregate([{
// Join with user_info table
		lookup:{
					from: "userinfo", // other tablename
					localField: "userId", // name of users table field
					foreignField: "userId", // name of userinfo table field
					as: "user_info" // alias for userinfo table
				}
	},
		{ $unwind:"$user_info" },
		// $unwind used for getting data in object or for one record only
		
		// Join with user_role table
	{
		$lookup:{
					from: "userrole", 
					localField: "userId", 
					foreignField: "userId",
					as: "user_role"
					
		{ $unwind:"$user_role" },
		
		// define some conditions here 
	{
		$match:{$and:[{"userName" : "admin"}]}
	},
	
	// define which fields are you want to fetch
	{
		$project:
					_id : 1,
					email : 1,
					userName : 1,
					userPhone : "$user_info.phone",
					role : "$user_role.role",
	} 
}
]);

```
Compared with MongoDB, TDSQL can use JSON fields to create various join conditions in a non-sharded table. It supports join operations in one single sharded table but not in multiple ones (for more information, see the code below)
```
Insert data
create table users(id int primary key auto_increment, value json);
create table userinfo(id int primary key auto_increment, value json);
create table userrole(id int primary key auto_increment, value json);

insert into users(value) values('{ 
									"email" : "admin@gmail.com",
									"userId" : "AD",
									"userName" : "admin"}'),
								('{
									"email" : "admin1@gmail.com",
									"userId" : "AD",
									"userName" : "admin1"}');
									
insert into userinfo(value) values('{
										"userId" : "AD",
										"phone" : "0000000000"}'),
								('{
										"userId" : "AD",
										"phone" : "0000000000"}');
										
insert into userrole(value) values('{
										"userId" : "AD",
										"role" : "admin"}'),
								('{
										"userId" : "AC",
										"role" : "admin"}');

Multiple join operations can be performed on JSON fields according to the join syntax of MySQL
select * from users left join userinfo on users.value
					->"$.userId" = userinfo.value
					->"$.userId" left join userrole on users.value
					->"$.userId" = userrole.value
					->"$.userId" where users.value
					->"$.userName"="admin";

select * from users left join userinfo on users.value
					->"$.userId" = userinfo.value
					->"$.userId" right join userrole on users.value
					->"$.userId" = userrole.value
					->"$.userId" where userrole.value
					->"$.role"="admin";
```


## Summary
### Data write
Both MongoDB and TDSQL can easily write JSON strings and update some fields in JSON. However, MongoDB does not support transactions, and it can only ensure the atomicity of single-line operations. If the atomicity of multiple-line operations needs to be ensured, two-phase commit must be implemented at the application layer. JSON operations of TDSQL can completely support transactions as well as distributed transactions in sharding mode.

### Data query
1. Join: TDSQL supports join operations on multiple tables by JSON fields, while MongoDB only supports left join operations on multiple non-sharded tables.
2. Index: Both TDSQL and MongoDB support creating indices by some fields (e.g., int and string) of JSON. MongoDB also supports multi-key index.
3. Access to internal JSON elements: Both TDSQL and MangoDB have complete syntax to access each filed in JSON, so there is no need to perform JSON parsing at the application layer.
4. Search criteria: The searching and matching features of MongoDB are more comprehensive. In contrast, TDSQL is not very friendly to developers as they have to perform type conversion on the criteria before making any judgment. In addition, due to its poorer filtering feature than MangoDB, TDSQL is suitable for applications with simple JSON operations.

### Overall Comparison
In general, TDSQL has all the three core features of MongoDB (JSON flexibility, high availability ensured by replica set, and scalability ensured by sharding). MongoDB supports relatively detailed JSON features. Because TDSQL is created on the basis of Tencent's TDSQL finance-grade distributed architecture, it offers complete solutions for high data consistency, availability, and scalability. Furthermore, TDSQL is capable of processing transactions and join operations of relational databases.

If you want to use JSON types and enjoy the capabilities of traditional databases such as data consistency, transactions, and joins, TDSQL will be a good choice.
