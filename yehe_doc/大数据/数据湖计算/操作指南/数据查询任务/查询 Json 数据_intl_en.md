## Query steps
1. Create a data table and specify the JSON format for parsing.
```
CREATE EXTERNAL TABLE `order_demo`(
  `docid` string COMMENT 'from deserializer',
  `user` struct < id :int,
  username :string,
  name :string,
  shippingaddress :struct < address1 :string,
  address2 :string,
  city :string,
  state :string > > COMMENT 'from deserializer',
  `children` array < string >
) ROW FORMAT SERDE 'org.apache.hive.hcatalog.data.JsonSerDe' LOCATION 'cosn://dlc-bucket/order'
```
2. Run a query statement to query the JSON data. Data Lake Compute supports `json_parse()`, `json_extract_scalar()`, and `json_extract()` parsing functions.
```sql
SELECT `user`.`shippingaddress`.`address1` FROM `order_demo` limit 10;
```

## System restraints
- The data must be in complete JSON format; otherwise, Data Lake Compute cannot parse it.
- A data row cannot contain a line break, and the JSON format cannot be optimized visually; for example:
```json
{"name":"Michael"}
{"name":"Andy", "age":30}
{"name":"Justin", "age":19}
```
- Data Lake Compute will automatically recognize the first JSON level as the attribute column of a data table and recognize other nested structures as corresponding attribute values.
