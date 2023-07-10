The cases in this document are based on real-life processing cases. They will help you get a general and perceptual understanding of data processing. You can also copy the functions in these cases for your own data processing.


## Notes

- `v` function: **v("Field A")** indicates the value of field A. The parameter is **Field** or **Field value** in some functions. The common error is that: the function parameter is **Field value** but the `v` function is not used to get the field value, which leads to function execution failure.     
- If you need to distribute logs to multiple log topics, you need to configure the **target log topic** and its **target name** in advance. The target name is used by the **distribution function**. For more information, please see [Case 1. Log Filtering And Distribution](#case1).   
- `fields_set` function: the `fields_set` function is used to set field values and store the content processed by data processing function. For example, `fields_set("A+B",op_add(v("Field A"),v("Field B")))` is to add the values of fields A and B, and the `op_add` function needs to leverage the `fields_set` function to complete result writing and storage.

<span id="case1"></span>
## Case 1. Log Filtering And Distribution

#### Background

Tom has collected logs to CLS. The logs contain information such as the log time, log level, log content, task ID, process name, and host IP, and the information is separated by two vertical bars (||). Now Tom wants to structure the log to facilitate subsequent indexing and dashboard display. He also wants to **distribute** the logs to three different target log topics according to three log levels (**ERROR**, **WARNING**, and **INFO**) for subsequent analysis. Tom also wants the logs whose content contains the **team B is working** keywords to be filtered out (discarded)**.

#### Scenario analysis

According to Tom's requirements, the processing ideas are as follows:  
1. Filter out (discard) logs that contain the **team B is working** keywords and place the discarded logs up front to reduce subsequent computation.  
2. Structure logs based on the separator of **two vertical bars** (||).  
3. Log distribution: distribute the logs to three different target log topics according to three log levels (**ERROR**, **WARNING**, and **INFO**).  

>! To distribute logs to multiple target log topics, you need to define the target names of the log topics when creating the data processing task. The target names will be used in the **log_output("Target name")** functions.
>

![](https://qcloudimg.tencent-cloud.cn/raw/320532e8fcab9c6eec8504895a806ef5.png)

#### Raw log

``` 
[
    {
        "message": "2021-12-09 11:34:28.279||team A is working||INFO||605c643e29e4||BIN--COMPILE||192.168.1.1"
    },
    {
        "message": "2021-12-09 11:35:28.279||team A is working ||WARNING||615c643e22e4||BIN--Java||192.168.1.1"
    },
    {
        "message": "2021-12-09 11:36:28.279||team A is working ||ERROR||635c643e22e4||BIN--Go||192.168.1.1"
    },
    {
        "message": "2021-12-09 11:37:28.279||team B is working||WARNING||665c643e22e4||BIN--Python||192.168.1.1"
    }
]
```

#### DSL processing function

``` 
log_drop(regex_match(v("message"),regex="team B is working",full=False))
ext_sepstr("message","time,log,loglevel,taskId,ProcessName,ip",sep="\|\|")
fields_drop("message")
t_switch(regex_match(v("loglevel"),regex="INFO",full=True),log_output("info_log"),regex_match(v("loglevel"),regex="WARNING",full=True),log_output("warning_log"),regex_match(v("loglevel"),regex="ERROR",full=True),log_output("error_log"))
```

#### DSL processing function details 

1. Discard logs that contain the **team B is working** keywords. The fourth log contains the **team B is working** keywords and needs to be discarded.
``` 
log_drop(regex_match(v("message"),regex="team B is working",full=False))
```
2. Extract structured data based on the separator of **two vertical bars** (||).
``` 
ext_sepstr("message","time,log,loglevel,taskId,ProcessName,ip",sep="\|\|")
```
3. Discard the **message** field.
``` 
fields_drop("message")
```
4. According to the value of the **loglevel** field, **INFO**, **WARNING**, and **ERROR** logs will be distributed to different target log topics.
``` 
t_switch(regex_match(v("loglevel"),regex="INFO",full=True),log_output("info_log"),regex_match(v("loglevel"),regex="WARNING",full=True),log_output("warning_log"),regex_match(v("loglevel"),regex="ERROR",full=True),log_output("error_log"))
```

#### Processing result

>! Target log topics and target names must be configured in advance.
>

The following log is distributed to **info_log** (**Data processing-target 3**). See the mappings between target names and log topics in the figure above.
``` 
{"ProcessName":"BIN--COMPILE","ip":"192.168.1.1","log":"team A is working","loglevel":"INFO","taskId":"605c643e29e4","time":"2021-12-09 11:34:28.279"}
```
The following log is distributed to **warning_log** (**Data processing-target 2**).
``` 
{"ProcessName":"BIN--COMPILE","ip":"192.168.1.1","log":"team A is working","loglevel":"INFO","taskId":"605c643e29e4","time":"2021-12-09 11:34:28.279"}
```
The following log is distributed to **error_log** (**Data processing-target 1**).
``` 
{"ProcessName":"BIN--Go","ip":"192.168.1.1","log":"team A is working ","loglevel":"ERROR","taskId":"635c643e22e4","time":"2021-12-09 11:36:28.279"}
```

## Case 2. Structuring Single-Line Text Logs

#### Background

Tom has collected a log to CLS. The log does not use a fixed separator and is in single-line text format. Now Tom wants to structure the log and **extract the log time, log level, operation, and URL information** from the text for subsequent search and analysis.   

#### Scenario analysis

According to Tom's requirements, the processing ideas are as follows:  
1.The content in {...} is the detailed information of operations and can be extracted with a regular expression.  
2. Use a regular expression to extract the **log time**, **log level**, and **URL**.  

#### Raw log

``` 
{
    "content": "[2021-11-24 11:11:08,232][328495eb-b562-478f-9d5d-3bf7e][INFO] curl -H 'Host: ' http://abc.com:8080/pc/api -d {\"version\": \"1.0\",\"user\": \"CGW\",\"password\": \"123\",\"interface\": {\"Name\": \"ListDetail\",\"para\": {\"owner\": \"1253\",\"orderField\": \"createTime\"}}}"
}
```

#### DSL processing function

```
fields_set("Action",regex_select(v("content"),regex="\{[^\}]+\}",index=0,group=0)) 
fields_set("loglevel",regex_select(v("content"),regex="\[[A-Z]{4}\]",index=0,group=0)). 
fields_set("logtime",regex_select(v("content"),regex="\d{4}-\d{2}-\d{2} \d{2}:\d{2}:\d{2},\d{3}",index=0,group=0))
fields_set("Url",regex_select(v("content"),regex="([a-z]{3}).([a-z]{3}):([0-9]{4})",index=0,group=0))
fields_drop("content")
```

#### DSL processing function details 

1. Create a field named **Action** and use the regular expression \{[^\}]+\} to match **{...}**.  
```
fields_set("Action",regex_select(v("content"),regex="\{[^\}]+\}",index=0,group=0)) 
```
2. Create a field named **loglevel** and use the regular expression [A-Z]{4} to match **INFO**.
```
fields_set("loglevel",regex_select(v("content"),regex="\[[A-Z]{4}\]",index=0,group=0)).
```
3. Create a field named **logtime** and use the regular expression d{4}-\d{2}-\d{2} \d{2}:\d{2}:\d{2},\d{3} to match **2021-11-24 11:11:08**.
```  
fields_set("logtime",regex_select(v("content"),regex="\d{4}-\d{2}-\d{2} \d{2}:\d{2}:\d{2},\d{3}",index=0,group=0))
```
4. Create a field named **Url**, use the regular expression [a-z]{3}.[a-z]{3} to match **abc.com**, and use [0-9]{4} to match **8080**.  
```
fields_set("Url",regex_select(v("content"),regex="([a-z]{3}).([a-z]{3}):([0-9]{4})",index=0,group=0))
```
5. Discard the **content** field. 
```
fields_drop("content")
```

#### Processing result

```
{"Action":"{\"version\": \"1.0\",\"user\": \"CGW\",\"password\": \"123\",\"interface\": {\"Name\": \"ListDetail\",\"para\": {\"owner\": \"1253\",\"orderField\": \"createTime\"}","Url":"abc.com:8080","loglevel":"[INFO]","logtime":"2021-11-24 11:11:08,232"}
 
```

## Case 3. Masking Data

#### Background

Tom has collected a log to CLS. The log contains sensitive information such as the user ID (**dev@12345**), login IP (**11.111.137.225**), and mobile number (**13912345678**). Tom wants to mask these sensitive information.

#### Scenario analysis

The log itself is a structured log, and therefore its fields can be masked directly.

#### Raw log
``` 
    {
        "Id": "dev@12345",
        "Ip": "11.111.137.225",
        "phonenumber": "13912345678"
    }
```

#### DSL processing function

```
fields_set("Id",regex_replace(v("Id"),regex="\d{3}", replace="***",count=0))
fields_set("Id",regex_replace(v("Id"),regex="\S{2}", replace="**",count=1))
fields_set("phonenumber",regex_replace(v("phonenumber"),regex="(\d{0,3})\d{4}(\d{4})", replace="$1****$2"))
fields_set("Ip",regex_replace(v("Ip"),regex="(\d+\.)\d+(\.\d+\.\d+)", replace="$1***$2",count=0))
```

#### DSL processing function details 

1. Mask the **Id** field. The result is **dev@\*\*\*45**.
```
fields_set("Id",regex_replace(v("Id"),regex="\d{3}", replace="***",count=0))
```
2. Mask the **Id** field again. The result is **\*\*v@\*\*\*45**.
```
fields_set("Id",regex_replace(v("Id"),regex="\S{2}", replace="**",count=1))
```
3. Mask the **phonenumber** field by replacing the middle 4 digits with **\*\*\*\***. The result is **139\*\*\*\*5678**.
```
fields_set("phonenumber",regex_replace(v("phonenumber"),regex="(\d{0,3})\d{4}(\d{4})", replace="$1****$2"))
```
4. Mask the **IP** field by replacing the octet with **\*\*\***. The result is **11.\*\*\*137.225**.
```
fields_set("Ip",regex_replace(v("Ip"),regex="(\d+\.)\d+(\.\d+\.\d+)", replace="$1***$2",count=0))
```

#### Processing result

```
{"Id":"**v@***45","Ip":"11.***.137.225","phonenumber":"139****5678"} 
```


## Case 4. Processing Logs in Nested JSON Format

#### Background

Tom has collected logs to in nested JSON format to CLS. Now he wants to extract the **user** (secondary nested field) and **App** fields from the logs.

#### Raw log

``` 
[
    {
        "content": {
            "App": "App-1",
            "start_time": "2021-10-14T02:15:08.221",
            "resonsebody": {
                "method": "GET",
                "user": "Tom"
            },
            "response_code_details": "3000",
            "bytes_sent": 69
        }
    },
    {
        "content": {
            "App": "App-2",
            "start_time": "2222-10-14T02:15:08.221",
            "resonsebody": {
                "method": "POST",
                "user": "Jerry"
            },
            "response_code_details": "2222",
            "bytes_sent": 1
        }
    }
]
```

#### DSL processing function

- Method 1. Use the **JMES** formula to extract fields directly without expanding all key-value pairs
```
ext_json_jmes("content", jmes="resonsebody.user", output="user")
ext_json_jmes("content", jmes="App", output="App")
```
- Method 2. Expand all key-value pairs and discard unwanted fields
```
ext_json("content")
fields_drop("content")
fields_drop("bytes_sent","method","response_code_details","start_time")
```

#### DSL processing function details 

- Method 1: 
 1. Use the JMES formula **resonsebody.user** to directly specify the secondary nested field **user**.
```
ext_json_jmes("content", jmes="resonsebody.user", output="user")
```
 2. Use the JMES formula **App** to directly specify the **App** field.
```
ext_json_jmes("content", jmes="App", output="App")
```
- Method 2:  
 1. Use the **ext_json** function to extract structured data from the JSON data. All fields are expanded by default.
```
ext_json("content")
```
 2. Discard the **content** field.
```
fields_drop("content")
```
 3. Discard the unwanted fields **bytes_sent**, **method**, **response_code_details**, and **start_time**.
```
fields_drop("bytes_sent","method","response_code_details","start_time")
```


#### Processing result

```
[{"App":"App-1","user":"Tom"},
{"App":"App-2","user":"Jerry"}]
```

## Case 5. Structuring Logs in Multiple Formats

#### Background

Tom has collected **user operation and result** logs to CLS in single-line text format. The formats of contents of the logs **are not identical**. Tom wants to write a set of statements to structure the logs in different formats. 
Analysis found that the logs are basically in three formats: the first contains four fields (**uin**, **requestid**, **action**, and **Reqbody**), the second contains three fields (**uin**, **requestid**, and **action**), and the third contains three fields (**requestid**, **action**, and **TaskId**).

#### Scenario analysis

According to Tom's requirements, the processing ideas are as follows:  
1. Since all three formats of logs contain the **requestid** and **action** fields, use a regular expression to extract these two fields.  
2. Perform special processing on the **uin**, **reqbody**, and TaskId** fields: determine whether the fields exist and then extract them if they exist.

#### Raw log

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

#### DSL processing function

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

#### DSL processing function details 

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

#### Processing result

```
[
{"action":" Describe","requestid":" 7143a51d-caa4-4a6d-bbf3-771b4ac9e135","requestbody":" {\"Key\": \"config\",\"Values\": \"appisrunnning\",\"Action\": \"Describe\",\"RequestId\": \"7143a51d-caa4-4a6d-bbf3-771b4ac9e135\",\"AppId\": 1302953499,\"Uin\": \"100015432829\"}","uin":" 15432829"},
{"action":" DataETL","requestid":" 2ade9fc4-2db2-49d8-b3e0-a6ea78ce8d96","uin":" 15432829"},
{"action":" UploadData","requestid":" 6059b946-25b3-4164-ae93-9178c9e73d75","TaskId":" 51d-caa-a6d-bf3-7ac9e"}
]
```

## Case 6. Using Separators to Extract Specified Content from Logs

#### Background

Tom has collected **Flink task running logs** to CLS in single-line text format. The log content is divided into segments with the **comma (,)** and **colon (:)** separators. Among these segments, there is a segment in escaped JSON format containing Flink task execution details. Tom wants to extract the task details and structure them.  

#### Scenario analysis

According to Tom's requirements, the processing ideas are as follows:  
1. Extract the content in escaped JSON format.  
2. Extract structured data from the JSON content.


#### Raw log

``` 
{
    "regex": "2021-12-02 14:33:35.022 [1] INFO  org.apache.Load - Response:status: 200, resp msg: OK, resp content: {    \"TxnId\": 58322,    \"Label\": \"flink_connector_20211202_1de749d8c80015a8\",    \"Status\": \"Success\",    \"Message\": \"OK\",    \"TotalRows\": 1,    \"LoadedRows\": 1,    \"FilteredRows\": 0,  \"CommitAndPublishTimeMs\": 16}"
}
```

#### DSL processing function

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

#### DSL processing function details 

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

#### Processing result

```
{"CommitAndPublishTimeMs":"16","FilteredRows":"0","Label":"flink_connector_20211202_1de749d8c80015a8","LoadedRows":"1","Message":"OK","Status":"Success","TotalRows":"1","TxnId":"58322"}
```
