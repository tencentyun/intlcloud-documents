
## Raw Log

A raw log contains only the `content` field, and the log content is separated with vertical bars (|).
``` 
content: 2021-10-07 13: 32: 21|100|Customer not checked in|Jack|Beijing|101123199001230123| 
content: 2021-10-07 13: 32: 21|500|Checked in successfully|Jane|Sanya|501123199001230123|
content: 2021-10-07 13: 32: 21|1000|Checked out|Lily|Sanya|101123196001230123|
```
    
## Processing Target

- Extract New Field: extract the log content separated with vertical bars (|), generate new field values, and add field names.
- Discard Field: discard unwanted fields
- Discard Log: discard the log if no customer checks in.
- Desensitize Log: desensitize customer ID numbers.
- Distribute Log: distribute logs to log topics **VIP customer** and Common customer** by taking the rate of 1,000 yuan as the boundary.

## DSL Processing Function

Run the following DSL function statement to achieve the preceding processing targets:
```
ext_sep("content","time,Rate,Customer status,Customer name,Region,ID",sep="|")
fields_drop("content")
log_drop(regex_match(v("Customer status"),regex="Customer not checked in",full=False))
fields_set("ID", regex_replace(v("ID"), regex="(\d{6})\d{6}(\d{6})", replace="$1******$2", count=0))
t_switch(op_ge(v("Rate"),1000),log_output("VIP customer"),op_lt(v("Rate"),1000),log_output("Common customer"))

```

## Processing Result

If result information similar to the following is returned, the log is distributed to the log topic named **Common customer**.
```
time:2021-10-07 13: 32: 21 Region:Sanya Customer name:Jane   Customer status:Checked in successfully  Rate:500 ID:501123******230123
```
If result information similar to the following is returned, the log is distributed to the log topic named **VIP customer**. 
```
time:2021-10-07 13: 32: 21 Region:Sanya Customer name:Lily  Customer status:Checked out    Rate:1000 ID:101123******230123  
```

## Example Procedure

The following shows the procedure for the DSK function processing statement as an example.

### Step 1. Extract new fields

Use the `ext_sep("Source field name","Target field list",sep="Separator")` function to fill the value of the source field to the target field list according to the separator:
```code
ext_sep("content","time,Rate,Customer status,Customer name,Region,ID",sep="|")
```
Execution result:
```   
content:2021-10-07 13: 32: 21|100|Customer not checked in|Jack|Beijing|101123199001230123|  
time:2021-10-07 13: 32: 21 Region:Beijing Customer name:Jack Customer status:Customer not checked in Rate:100 ID:101123199001230123
content:2021-10-07 13: 32: 21|500|Checked in successfully|Jane|Sanya|501123199001230123|   
time:2021-10-07 13: 32: 21 Region:Sanya Customer name:Jane   Customer status:Checked in successfully  Rate:500 ID:501123199001230123
content:2021-10-07 13: 32: 21|1000|Checked out|Lily|Sanya|101123196001230123|  
time:2021-10-07 13: 32: 21 Region:Sanya Customer name:Lily  Customer status:Checked out    Rate:1000 ID:101123196001230123  
```
After field extraction, the `content` field becomes redundant and can be deleted.

### Step 2. Discard the source field

Because the `content` field is no longer needed, use the `fields_drop("Field name")` function to discard it:
```
fields_drop("content")
```
Execution result: 
```   
time:2021-10-07 13: 32: 21 Region:Beijing Customer name:Jack Customer status:Customer not checked in Rate:100 ID:101123199001230123
time:2021-10-07 13: 32: 21 Region:Sanya Customer name:Jane   Customer status:Checked in successfully  Rate:500 ID:501123199001230123
time:2021-10-07 13: 32: 21 Region:Sanya Customer name:Lily  Customer status:Checked out    Rate:1000 ID:101123196001230123  
```

### Step 3. Discard logs

If `Customer status` is `Customer not checked in` in a log, use the `log_drop(Condition=TRUE)` to discard the log.
Because Jack did not check in, the log is discarded. Use `regex_match(v("Field value"),regex="String",full=False)` to determine whether `Customer status` is `Customer not checked in`. `full=False` indicates that only partial match, instead of full match, is required.
```
log_drop(regex_match(v("Customer status"),regex="Customer not checked in",full=False))
```
Execution result: 
```
time:2021-10-07 13: 32: 21 Region:Sanya Customer name:Jane   Customer status:Checked in successfully  Rate:500 ID:501123199001230123
time:2021-10-07 13: 32: 21 Region:Sanya Customer name:Lily  Customer status:Checked out    Rate:1000 ID:101123196001230123  
```

### Step 4. Desensitize logs

Desensitize customer ID numbers. An ID number consists of 18 digits. The regular expression divides an ID number into three parts by brackets and replaces the 6 digits in the middle with \*\*\*\*\*\*.  
The `regex_replace("Field name",regex="Regular expression match statement",repalce="Replaced string")` function is used. Because the function returns a string, you need to use `fields_set("Field name","Field value")` to fill the string into the target field.
```
fields_set("ID", regex_replace(v("ID"), regex="(\d{6})\d{6}(\d{6})", replace="$1******$2", count=0))
```
Execution result: 
```
time:2021-10-07 13: 32: 21 Region:Sanya Customer name:Jane   Customer status:Checked in successfully  Rate:500 ID:501123******230123
time:2021-10-07 13: 32: 21 Region:Sanya Customer name:Lily  Customer status:Checked out    Rate:1000 ID:101123******230123  
```

### Step 5. Distribute logs

Logs where `Rate` is greater than or equal to 1,000 are distributed to the **VIP customer** log topic. Logs where `Rate` is less than 1,000 are distributed to the **Common customer** log topic.
Use the `t_switch(Condition 1,Function 1,Condition 2,Function 2)` statement to create logic determination conditions. Then use `op_ge(a,b)`, which returns `TRUE` when `a` is greater than or equal to `b`, and use `op_lt(a,b)`, which returns `TRUE` when `a` is less than `b`. The `log_output("Log topic alias")` function outputs logs to the specified log topic.
```
t_switch(op_ge(v("Rate"),1000),log_output("VIP customer"),op_lt(v("Rate"),1000),log_output("Common customer"))
```
Execution result: the log is distributed to the **Common customer** log topic.
```
time:2021-10-07 13: 32: 21 Region:Sanya Customer name:Jane   Customer status:Checked in successfully  Rate:500 ID:501123******230123
```
Execution result: the log is distributed to the **VIP customer** log topic. 
```
time:2021-10-07 13: 32: 21 Region:Sanya Customer name:Lily  Customer status:Checked out    Rate:1000 ID:101123******230123  
```


## Notes

- The `log_output("Log topic alias")` function is used to specify an alias for a target log topic when creating a data processing task. An alias provides certain readability without writing the logset and the log topic parameters. It is convenient for users to change the alias without changing the log topic name.
- The `regex_replace("Field name",regex="Regular expression match statement",repalce="Replaced string")` function returns a string and therefore cannot be used alone. You need to use `fields_set("Field name","Field value")` to fill the string into the target field.

