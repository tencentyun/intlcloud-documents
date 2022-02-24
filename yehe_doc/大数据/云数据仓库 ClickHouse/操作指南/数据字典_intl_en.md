## Feature Overview 
ClickHouse offers [internal dictionaries](https://clickhouse.com/docs/en/sql-reference/dictionaries/internal-dicts/) and [external dictionaries](https://clickhouse.com/docs/en/sql-reference/dictionaries/external-dictionaries/external-dicts/). The former predefines the content and the latter offers various definitions from external data sources. You can use special functions along with a dictionary for query, which is simpler and more efficient than the combination of `JOIN` and a reference table. This document describes how to use external dictionaries in the console.

## Notes
1. A data dictionary maintained in the console will take effect on all ClickHouse nodes.
2. A data dictionary added in the console can only be maintained (modified and deleted) in the console.
3. A data dictionary added using SQL commands or other backend methods cannot be maintained (modified and deleted) in the console.
4. A dictionary table created in the console will be added to the Cloud Data Warehouse global database **cdwch_{instanceId}_dictionary_database** by default.
>! Do not maintain a dictionary via both the console and other means (such as SQL commands and other backend means). Otherwise, content may be overwritten or lost (such as due to accidental deletion).

## Directions in Console
1. Log in to the [Cloud Data Warehouse console](https://console.cloud.tencent.com/cdwch), select the target cluster in **Cluster List**, and click the **Data Dictionaries** tab on the cluster details page.
2. View the list of existing external dictionaries on the current page.
![](https://qcloudimg.tencent-cloud.cn/raw/e88604b2a27856eb5b084ab0e3c814bc.png) 3. Click **Create Dictionary** in the top-left corner, set the fields as prompted, and click **OK** to create a dictionary.
<table>
<thead>
<tr>
<th width=15%>Parameter</th>
<th>Description</th>
<th>Reference</th>
</tr>
</thead>
<tbody><tr>
<td>Dictionary Name</td>
<td>Enter a custom external dictionary name, which can contain 2–16 lowercase letters, digits, and underscores and must start with a letter and end with a letter or digit.</td>
<td>-</td>
</tr>
<tr>
<td>Data Source</td>
<td>Select the type of data source for the external dictionary. Currently, the Cloud Data Warehouse console supports the MySQLClickHouse data source.</td>
<td><a href="https://clickhouse.com/docs/en/sql-reference/dictionaries/external-dictionaries/external-dicts-dict-sources/">Sources of External Dictionaries</a></td>
</tr>
<tr>
<td>Data Source Connection</td>
<td>Configure data source information to verify the connectivity of the configured external source. Configuration items include:<ul style="margin:0">
<li/>HOST: IP address or domain name. Currently, only VPC connections are supported.
<li/>TCP PORT: TCP port
<li/>USER: external source account
<li/>PASSWORD: password of the external source account
</ul></td>
<td>-</td>
</tr>
<tr>
<td>Source Table Information</td>
<td>Select the databases and tables of the dependent external source and enter `WHERE` (table filter condition) and `INVALIDATEQUERY` (for querying/checking the dictionary status, with only the updated data extracted).</td>
<td><a href="https://clickhouse.com/docs/en/sql-reference/dictionaries/external-dictionaries/external-dicts-dict-lifetime/">Dictionary Updates</a></td>
</tr>
<tr>
<td>Data Structure</td>
<td>Set the primary key and general fields of the external dictionary, including:<ul style="margin:0">
        <li/>PRIMARY_KEY: single or composite primary key.
        <li/>COLUME_NAME: field type. Currently, the console supports the following types: <code>UInt8</code>, <code>UInt16</code>, <code>UInt32</code>, <code>UInt64</code>, <code>Int8</code>, <code>Int16</code>, <code>Int32</code>, <code>Int64</code>, <code>Float32</code>, <code>Float64</code>, <code>Date</code>, <code>DateTime</code>, <code>UUID</code>, and <code>String</code>.
        <li/>DEFAULT_VALUE: default value for empty fields
        <li/>EXPRESSION: expression to describe fields (if applicable)
        <li/>IS_HIERARCHICAL: indicates the support for hierarchy. The default value is `false`.
        <li/>S_INJECTIVE: indicates the inline mapping "id -&gt; attribute". The default value is `false`.
</ul></td>
<td><a href="https://clickhouse.com/docs/en/sql-reference/dictionaries/external-dictionaries/external-dicts-dict-structure/">Dictionary Key and Fields</a></td>
</tr>
<tr>
<td>Storage Format</td>
<td>Select the type of memory layout for the external dictionary, including:<ul style="margin:0">
        <li/>FLAT: stores the entire dictionary in memory as a flat array, which is suitable for a single primary key.
        <li/>HASHED: stores the entire dictionary in memory as a hash table, which is suitable for a single primary key.
        <li/>RANGE_HASHED: stores the entire dictionary in memory as a hash table. It comes with an ordered array of ranges and corresponding values, which is suitable for a single primary key. You need to set the fields to represent the ranges.
        <li/>CACHE: stores the entire dictionary in a cache with a certain number of cells, which is suitable for a single primary key. You need to set the cache size.
        <li/>COMPLEX_KEY_HASHED: similar to HASHED and suitable for composite primary keys.
        <li/>COMPLEX_KEY_CACHE: similar to CACHE and suitable for composite primary keys. You need to set the cache size.
</ul></td>
<td><a href="https://clickhouse.com/docs/en/sql-reference/dictionaries/external-dictionaries/external-dicts-dict-layout/">Storing Dictionaries in Memory</a></td>
</tr>
<tr>
<td>Update Interval</td>
<td>Set the frequency of updating data in the dictionary. The unit is s.</td>
<td><a href="https://clickhouse.com/docs/zh/sql-reference/dictionaries/external-dictionaries/external-dicts-dict-lifetime/">Dictionary Updates</a></td>
</tr>
</tbody></table>
4. After the external dictionary is created, you can view, modify, and delete it in the list.

## Managing External Dictionary via SQL
1. Create a dictionary.
```
CREATE DICTIONARY [IF NOT EXISTS] [db.]dictionary_name [ON CLUSTER cluster]
(
    key1 type1  [DEFAULT|EXPRESSION expr1] [IS_OBJECT_ID],
    key2 type2  [DEFAULT|EXPRESSION expr2],
    attr1 type2 [DEFAULT|EXPRESSION expr3] [HIERARCHICAL|INJECTIVE],
    attr2 type2 [DEFAULT|EXPRESSION expr4] [HIERARCHICAL|INJECTIVE]
)
PRIMARY KEY key1, key2
SOURCE(SOURCE_NAME([param1 value1 ... paramN valueN]))
LAYOUT(LAYOUT_NAME([param_name param_value])``)
LIFETIME({MIN min_val MAX max_val | max_val})
```
2. View the dictionary.
```
SELECT * FROM system.dictionaries
```
3. Delete the dictionary.
```sql
DROP DICTIONARY <database name>.<dictionary name>
```
For more information on dictionary SQL, see [CREATE DICTIONARY](https://clickhouse.com/docs/en/sql-reference/statements/create/dictionary/).

## Using External Dictionary
You can query some types of dictionaries using general `SELECT`:
```sql
SELECT * FROM <database name>.<dictionary name>
```
You can also query them using dictionary functions:
```sql
dictGet('dict_name', attr_names, id_expr)
dictGetOrDefault('dict_name', attr_names, id_expr, default_value_expr)
dictGetOrNull('dict_name', attr_name, id_expr)
```

For more information on dictionary functions, see [Functions for Working with External Dictionaries](https://clickhouse.com/docs/en/sql-reference/functions/ext-dict-functions/).
