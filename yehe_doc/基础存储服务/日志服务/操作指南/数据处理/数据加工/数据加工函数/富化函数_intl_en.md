## Function enrich_table

#### Function definition

This function uses CSV structure data to match fields in logs and, when matched fields are found, the function adds other fields and values in the CSV data to the source logs.

#### Syntax description

```sql
enrich_table(CSV data string, CSV column name string, output=Target field name or list, mode="overwrite")
```

#### Parameter description

| Parameter | Description | Parameter Type | Required | Default Value | Value Range |
|-----------  |  ----------- |  ----------- | ----------- | -------------- |  --------------  |
|data  | Input CSV data, where the first row is column names and the rest rows are corresponding values. Example: region,count\nbj, 200\ngz, 300   |string    | Yes    | -   | -   |
|fields  | Column name to match. If the field name in the CSV data is the same as the field with the same name in the log, the matching is successful. The value can be a single field name or multiple new field names concatenated with commas.   |string   | Yes   | -   | -   |
|output  | Output field list. The value can be a single field name or multiple new field names concatenated with commas.    |string        | Yes      | -       |      -          |
|mode  | Write mode of the new field. Default value: `overwrite` |string  | No   |  overwrite  | -     |


#### Example

Raw log:
```
{"region": "gz"}
```
Processing rule:
```
enrich_table("region,count\nbj,200\ngz,300", "region", output="count")
```
Processing result:
```
{"count":"300","region":"gz"}
```

## Function enrich_dict 

#### Function definition

This function uses dict structure data to match a field value in a log. If the specified field and value match a key in the dict structure data, the function assigns the value of the key to another field in the log.

#### Syntax description

```sql
enrich_dict(Dict data string, Source field name, output=Target field, mode="overwrite")
```

#### Parameter description

| Parameter | Description | Parameter Type | Required | Default Value | Value Range |
|-----------  |  ----------- |  ----------- | ----------- | -------------- |  --------------  |
| data  | Input dict data, which must be the escaped string of a JSON object. Example: enrich_dict("{\"200\":\"SUCCESS\",\"500\":\"FAILED\"}", "status", output="message")  | string | Yes | -  | -  |
| fields | Field name to match. If the value of the key in the dict data is the same as the value of the specified field, the matching is successful. The value can be a single field name or multiple new field names concatenated with commas.  | string | Yes   | -   | -  |
|output | Target field list. After successful matching, the function writes the corresponding values in the dict data to the target field list. The value can be a single field name or multiple new field names concatenated with commas. | string  |  Yes  | -   | -   |
|mode  | Write mode of the new field. |string  | No   |  overwrite  | -     |

#### Example

Raw log:
```
{"status": "500"}
```
Processing rule:
```
enrich_dict("{\"200\":\"SUCCESS\",\"500\":\"FAILED\"}", "status", output="message")
```
Processing result:
```
{"message":"FAILED","status":"500"}
```
