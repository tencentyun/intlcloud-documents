
## Use Case

Tom has collected a log to CLS. The log does not use a fixed separator and is in single-line text format. Now Tom wants to structuralize the log and **extract the log time, log level, operation, and URL information** from the text for subsequent search and analysis.   

## Scenario Analysis

According to Tom's requirements, the processing ideas are as follows:  
1.The content in {...} is the detailed information of operations and can be extracted with a regular expression.  
2. Use a regular expression to extract the **log time**, **log level**, and **URL**.  

## Raw Log

``` 
{
    "content": "[2021-11-24 11:11:08,232][328495eb-b562-478f-9d5d-3bf7e][INFO] curl -H 'Host: ' http://abc.com:8080/pc/api -d {\"version\": \"1.0\",\"user\": \"CGW\",\"password\": \"123\",\"interface\": {\"Name\": \"ListDetail\",\"para\": {\"owner\": \"1253\",\"orderField\": \"createTime\"}}}"
}
```

## DSL Processing Function

```
fields_set("Action",regex_select(v("content"),regex="\{[^\}]+\}",index=0,group=0)) 
fields_set("loglevel",regex_select(v("content"),regex="\[[A-Z]{4}\]",index=0,group=0)). 
fields_set("logtime",regex_select(v("content"),regex="\d{4}-\d{2}-\d{2} \d{2}:\d{2}:\d{2},\d{3}",index=0,group=0))
fields_set("Url",regex_select(v("content"),regex="([a-z]{3}).([a-z]{3}):([0-9]{4})",index=0,group=0))
fields_drop("content")
```

## DSL Processing Function Details 

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

## Processing Result

```
{"Action":"{\"version\": \"1.0\",\"user\": \"CGW\",\"password\": \"123\",\"interface\": {\"Name\": \"ListDetail\",\"para\": {\"owner\": \"1253\",\"orderField\": \"createTime\"}","Url":"abc.com:8080","loglevel":"[INFO]","logtime":"2021-11-24 11:11:08,232"}
 
```

