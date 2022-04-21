## Use Case

Tom has collected **user operation and result** logs to CLS in single-line text format. The formats of contents of the logs **are not identical**. Tom wants to write a set of statements to structure the logs in different formats. 
Analysis found that the logs are basically in three formats: the first contains four fields (**uin**, **requestid**, **action**, and **Reqbody**), the second contains three fields (**uin**, **requestid**, and **action**), and the third contains three fields (**requestid**, **action**, and **TaskId**).

## Scenario Analysis

According to Tom's requirements, the processing ideas are as follows:  
1. Since all three formats of logs contain the **requestid** and **action** fields, use a regular expression to extract these two fields.  
2. Perform special processing on the **uin**, **reqbody**, and **TaskId** fields: determine whether the fields exist and then extract them if they exist.

## Raw Log

``` 
[
    {
        "__CONTENT__": "2021-11-29 15:51:33.201 INFO request 7143a51d-caa4-4a6d-bbf3-771b4ac9e135 action: Describe uin: 15432829 reqbody {\"Key\": \"config\",\"Values\": \"appisrunnning\",\"Action\": \"Describe\",\"RequestId\": \"7143a51d-caa4-4a6d-bbf3-771b4ac9e135\",\"AppId\": 1302953499,\"Uin\": \"100015432829\"}"
    },
    {
        "__CONTENT__": "2021-11-2915: 51: 33.272 ERROR request 2ade9fc4-2db2-49d8-b3e0-a6ea78ce8d96 has error action DataETL uin 15432829"
    },
    {
        "__CONTENT__": "2021-11-2915: 51: 33.200 INFO request 6059b946-25b3-4164-ae93-9178c9e73d75 action: UploadData hUWZSs69yGc5HxgQ TaskId 51d-caa-a6d-bf3-7ac9e"
    }
]
```

## DSL Processing Function

```
fields_set("requestid",regex_select(v("__CONTENT__"),regex="request [A-Za-z0-9]+-[A-Za-z0-9]+-[A-Za-z0-9]+-[A-Za-z0-9]+-[A-Za-z0-9]+",index=0,group=0))
fields_set("action",regex_select(v("__CONTENT__"),regex="action: \S+|action \S+",index=0,group=0))
t_if(regex_match(v("__CONTENT__"),regex="uin", full=False),fields_set("uin",regex_select(v("__CONTENT__"),regex="uin: \d+|uin \d+",index=0,group=0)))
t_if(regex_match(v("__CONTENT__"),regex="TaskId", full=False),fields_set("TaskId",regex_select(v("__CONTENT__"),regex="TaskId [A-Za-z0-9]+-[A-Za-z0-9]+-[A-Za-z0-9]+-[A-Za-z0-9]+-[A-Za-z0-9]+",index=0,group=0)))
t_if(regex_match(v("__CONTENT__"),regex="reqbody", full=False),fields_set("requestbody",regex_select(v("__CONTENT__"),regex="reqbody \{[^\}]+\}")))
t_if(has_field("requestbody"),fields_set("requestbody",str_replace(v("requestbody"),old="reqbody",new="")))
fields_drop("__CONTENT__")
fields_set("requestid",str_replace(v("requestid"),old="request",new=""))
t_if(has_field("action"),fields_set("action",str_replace(v("action"),old="action:|action",new="")))
t_if(has_field("uin"),fields_set("uin",str_replace(v("uin"),old="uin:|uin",new="")))
t_if(has_field("TaskId"),fields_set("TaskId",str_replace(v("TaskId"),old="TaskId",new="")))
```

## DSL Processing Function Details 

1. Create a field named **requestid** and use a regular expression to match "**request 7143a51d-caa4-4a6d-bbf3-771b4ac9e135**".
```
fields_set("requestid",regex_select(v("__CONTENT__"),regex="request [A-Za-z0-9]+-[A-Za-z0-9]+-[A-Za-z0-9]+-[A-Za-z0-9]+-[A-Za-z0-9]+",index=0,group=0))
```
2. Create a field named **action** and use a regular expression to match "**action: UploadData**" and "**action DataETL**" (they exist in two formats of the raw logs).
```
fields_set("action",regex_select(v("__CONTENT__"),regex="action: \S+|action \S+",index=0,group=0))
```
 - If the **\_\_CONTENT\_\_** field contains the **uin** keyword, create the **uin** field and use the regular expression "**uin: \d+|uin \d+**" to match **uin: 15432829** and **uin 15432829**.
```
t_if(regex_match(v("__CONTENT__"),regex="uin", full=False),fields_set("uin",regex_select(v("__CONTENT__"),regex="uin: \d+|uin \d+",index=0,group=0)))
```
 - If the **TaskId** keyword exists, create the **TaskId** field and use a regular expression to match "**TaskId 51d-caa-a6d-bf3-7ac9e**".
```
t_if(regex_match(v("__CONTENT__"),regex="TaskId", full=False),fields_set("TaskId",regex_select(v("__CONTENT__"),regex="TaskId [A-Za-z0-9]+-[A-Za-z0-9]+-[A-Za-z0-9]+-[A-Za-z0-9]+-[A-Za-z0-9]+",index=0,group=0)))
```
 - If the **reqbody** keyword exists, create the **requestbody** field and use a regular expression to match "**reqbody{...}**".
```
t_if(regex_match(v("__CONTENT__"),regex="reqbody", full=False),fields_set("requestbody",regex_select(v("__CONTENT__"),regex="reqbody \{[^\}]+\}")))
```
3. Discard the **\_\_CONTENT\_\_** field.
```
fields_drop("__CONTENT__")
```

Now we have extracted the fields we need. However, unnecessary characters (**action**, **uin**, **requestbody**, **requestid**, and **TaskId**) are generated during regular expression matching. Therefore, we need to use the **str_replace()** function to remove the unnecessary characters and use the **fields_set()** function to reset field values.

1. If the **requestbody** field exists, remove the unnecessary characters **reqbody** from the field value.
```
t_if(has_field("requestbody"),fields_set("requestbody",str_replace(v("requestbody"),old="reqbody",new="")))
```
2. Remove the unnecessary characters **requestid** from the v("**requestid**") field value. Because every log contains **requestid**, we do not determine whether the field exists.
```
fields_set("requestid",str_replace(v("requestid"),old="request",new=""))
```
3. If the **action** field exists, remove the unnecessary characters **action:** or **action** from the field value.
```
t_if(has_field("action"),fields_set("action",str_replace(v("action"),old="action:|action",new="")))
```
4. If the **uin** field exists, remove the unnecessary characters **uin:** or **uin** from the field value.
```
t_if(has_field("uin"),fields_set("uin",str_replace(v("uin"),old="uin:|uin",new="")))
```
5. If the **TaskId** field exists, remove the unnecessary characters **TaskId** from the field value.
```
t_if(has_field("tTaskId"),fields_set("TaskId",str_replace(v("TaskId"),old="TaskId",new="")))
```

## Processing Result

```
[
{"action":" Describe","requestid":" 7143a51d-caa4-4a6d-bbf3-771b4ac9e135","requestbody":" {\"Key\": \"config\",\"Values\": \"appisrunnning\",\"Action\": \"Describe\",\"RequestId\": \"7143a51d-caa4-4a6d-bbf3-771b4ac9e135\",\"AppId\": 1302953499,\"Uin\": \"100015432829\"}","uin":" 15432829"},
{"action":" DataETL","requestid":" 2ade9fc4-2db2-49d8-b3e0-a6ea78ce8d96","uin":" 15432829"},
{"action":" UploadData","requestid":" 6059b946-25b3-4164-ae93-9178c9e73d75","TaskId":" 51d-caa-a6d-bf3-7ac9e"}
]
```
