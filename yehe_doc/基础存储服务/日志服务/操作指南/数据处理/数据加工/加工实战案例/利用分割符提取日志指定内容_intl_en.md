## Use Case

Tom has collected **Flink task running logs** to CLS in single-line text format. The log content is divided into segments with the **comma (,)** and **colon (:)** separators. Among these segments, there is a segment in escaped JSON format containing Flink task execution details. Tom wants to extract the task details and structure them.  

## Scenario Analysis

According to Tom's requirements, the processing ideas are as follows:  
1. Extract the content in escaped JSON format.  
2. Extract structured data from the JSON content.


## Raw Log

``` 
{
    "regex": "2021-12-02 14:33:35.022 [1] INFO  org.apache.Load - Response:status: 200, resp msg: OK, resp content: {    \"TxnId\": 58322,    \"Label\": \"flink_connector_20211202_1de749d8c80015a8\",    \"Status\": \"Success\",    \"Message\": \"OK\",    \"TotalRows\": 1,    \"LoadedRows\": 1,    \"FilteredRows\": 0,  \"CommitAndPublishTimeMs\": 16}"
}
```

## DSL Processing Function

```
ext_sepstr("regex", "f1, f2, f3", sep=",")
fields_drop("regex")
fields_drop("f1")
fields_drop("f2")
ext_sepstr("f3", "f1,resp_content", sep=":")
fields_drop("f1")
fields_drop("f3")
ext_json("resp_content", prefix="")
fields_drop("resp_content")
```

## DSL Processing Function Details 

1. Use commas (,) to divide the log into 3 segments, where the third segment **f3** is **resp content:{JSON}**.
```
ext_sepstr("regex", "f1, f2, f3", sep=",")
```
2. Discard unwanted fields.
```
fields_drop("regex")
fields_drop("f1")
fields_drop("f2")
```
3. Use colons (:) to divide the **f3** field into two segments.
```
ext_sepstr("f3", "f1,resp_content", sep=":")
```
4. Discard useless fields.
```
fields_drop("f1")
fields_drop("f3")
```
5. Use the **ext_json** function to extract structured data from the **resp_content** field.
```
ext_json("resp_content", prefix="")
```
6. Discard the **resp_content** field.
```
fields_drop("resp_content")
```

## Processing Result

```
{"CommitAndPublishTimeMs":"16","FilteredRows":"0","Label":"flink_connector_20211202_1de749d8c80015a8","LoadedRows":"1","Message":"OK","Status":"Success","TotalRows":"1","TxnId":"58322"}
```

