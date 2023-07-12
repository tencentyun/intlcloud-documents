## Use Case

Tom has collected logs to CLS. The logs contain information such as the log time, log level, log content, task ID, process name, and host IP, and the information is separated by two vertical bars (||). Now Tom wants to structure the log to facilitate subsequent indexing and dashboard display. He also wants to **distribute** the logs to three different target log topics according to three log levels (**ERROR**, **WARNING**, and **INFO**) for subsequent analysis. Tom also wants the logs whose content contains the **team B is working** keywords to be filtered out (discarded)**.

## Scenario Analysis

According to Tom's requirements, the processing ideas are as follows:  
1. Filter out (discard) logs that contain the **team B is working** keywords and place the discarded logs up front to reduce subsequent computation.  
2. Structure logs based on the separator of **two vertical bars** (||).  
3. Log distribution: Distribute the logs to three different target log topics according to three log levels (**ERROR**, **WARNING**, and **INFO**).  

>! To distribute logs to multiple target log topics, you need to define the target names of the log topics when creating the data processing task. The target names will be used in the **log_output("Target name")** functions.
>



## Raw Log

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

## DSL Processing Function

``` 
log_drop(regex_match(v("message"),regex="team B is working",full=False))
ext_sepstr("message","time,log,loglevel,taskId,ProcessName,ip",sep="\|\|")
fields_drop("message")
t_switch(regex_match(v("loglevel"),regex="INFO",full=True),log_output("info_log"),regex_match(v("loglevel"),regex="WARNING",full=True),log_output("warning_log"),regex_match(v("loglevel"),regex="ERROR",full=True),log_output("error_log"))
``` 

## DSL Processing Function Details 

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

## Processing Result

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
