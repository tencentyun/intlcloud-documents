
## 原始日志

只有一个字段 content，日志内容以竖线作为分隔符。
``` 
content: 2021-10-07 13: 32: 21|100|客人未入住|韦小宝|北京|101123199001230123| 
content: 2021-10-07 13: 32: 21|500|入住成功|阿珂|三亚|501123199001230123|
content: 2021-10-07 13: 32: 21|1000|退房|韦春花|三亚|101123196001230123|
```
    
## 加工目标

- 提取新字段：将竖线分割的日志内容提取出来，成为新的字段值，并添加字段名。
- 丢弃字段：将不需要的字段丢弃。
- 丢弃日志：如果客人没有入住，将该条日志丢弃。
- 日志脱敏：将客人的身份证号码脱敏。
- 日志分发：客人的费用以1000元为界限，将日志分发到别名为“VIP客户”和“普通客户”的日志主题。

## DSL 加工函数

执行如下 DSL 函数语句，即可完成上述的加工目标。
```
ext_sep("content","time,费用,客人状态,客人姓名,地域,身份证",sep="|")
fields_drop("content")
log_drop(regex_match(v("客人状态"),regex="客人未入住",full=False))
fields_set("身份证", regex_replace(v("身份证"), regex="(\d{6})\d{6}(\d{6})", replace="$1******$2", count=0))
t_switch(op_ge(v("费用"),1000),log_output("VIP客户"),op_lt(v("费用"),1000),log_output("普通客户"))

```

## 加工结果

返回类似如下结果，表示日志分发到别名为“普通客户”日志主题。
```
time:2021-10-07 13: 32: 21 地域:三亚 客人姓名:阿珂   客人状态:入住成功  费用:500 身份证:501123******230123
```
返回类似如下结果，表示日志分发到别名为“VIP客户”日志主题。 
```
time:2021-10-07 13: 32: 21 地域:三亚 客人姓名:韦春花  客人状态:退房    费用:1000 身份证:101123******230123  
```

## 示例步骤

如下操作介绍了本文示例的 DSL 函数加工语句。

### 步骤1：提取新字段

ext_sep("源字段名","目标字段列表",sep="分隔符")这个函数按照分隔符，将源字段中的值，填入目标字段列表。
```code
ext_sep("content","time,费用,客人状态,客人姓名,地域,身份证",sep="|")
```
执行结果：
```   
content:2021-10-07 13: 32: 21|100|客人未入住|韦小宝|北京|101123199001230123|  
time:2021-10-07 13: 32: 21 地域:北京 客人姓名:韦小宝 客人状态:客人未入住 费用:100 身份证:101123199001230123
content:2021-10-07 13: 32: 21|500|入住成功|阿珂|三亚|501123199001230123|   
time:2021-10-07 13: 32: 21 地域:三亚 客人姓名:阿珂   客人状态:入住成功  费用:500 身份证:501123199001230123
content:2021-10-07 13: 32: 21|1000|退房|韦春花|三亚|101123196001230123|  
time:2021-10-07 13: 32: 21 地域:三亚 客人姓名:韦春花  客人状态:退房    费用:1000 身份证:101123196001230123  
```
可得知，提取完新的字段后，content 字段成为多余字段，可以丢弃该字段。

### 步骤2：丢弃字段

由于 content 字段已不再需要，使用 fields_drop("字段名") 函数将其丢弃。
```
fields_drop("content")
```
执行结果： 
```   
time:2021-10-07 13: 32: 21 地域:北京 客人姓名:韦小宝 客人状态:客人未入住 费用:100 身份证:101123199001230123
time:2021-10-07 13: 32: 21 地域:三亚 客人姓名:阿珂   客人状态:入住成功  费用:500 身份证:501123199001230123
time:2021-10-07 13: 32: 21 地域:三亚 客人姓名:韦春花  客人状态:退房    费用:1000 身份证:101123196001230123  
```

### 步骤3：丢弃日志

当客人状态是“客人未入住”时，将该条日志日志丢弃，使用 log_drop(条件=TURE) 函数进行处理。
由于韦小宝没有入住，所以这条日志被丢弃，使用 regex_match(v("字段值"),regex="字符串",full=False) 判断客人状态是否为“客人未入住”。full=False 表示不需要完全匹配，部分匹配。
```
log_drop(regex_match(v("客人状态"),regex="客人未入住",full=False))
```
执行结果： 
```
time:2021-10-07 13: 32: 21 地域:三亚 客人姓名:阿珂   客人状态:入住成功  费用:500 身份证:501123199001230123
time:2021-10-07 13: 32: 21 地域:三亚 客人姓名:韦春花  客人状态:退房    费用:1000 身份证:101123196001230123  
```

### 步骤4：日志脱敏

将客人的身份证号码进行脱敏处理。身份证是18位，在正则表达式中，使用()将其切分成三段，将中间的6位数替换成\*\*\*\*\*\*。  
使用的是 regex_replace("字段名"，regex="正则匹配语句",repalce="替换的字符串")函数。 由于它返回的是字符串，所以要使用 fields_set("字段名","字段值") 将其写入目标字段。
```
fields_set("身份证", regex_replace(v("身份证"), regex="(\d{6})\d{6}(\d{6})", replace="$1******$2", count=0))
```
执行结果： 
```
time:2021-10-07 13: 32: 21 地域:三亚 客人姓名:阿珂   客人状态:入住成功  费用:500 身份证:501123******230123
time:2021-10-07 13: 32: 21 地域:三亚 客人姓名:韦春花  客人状态:退房    费用:1000 身份证:101123******230123  
```

### 步骤5：日志分发

当费用大于等于1000时，将日志分发到别名为“VIP客户”的日志主题；当费用小于1000时，分发到别名为“普通客户”的日志主题。
使用 t_switch(条件1，函数1，条件2，函数2) 语句创建逻辑判断条件，然后使用 op_ge(a,b)，如果 a ≥ b，返回 TRUE，和 op_lt(a,b)，如果 a < b，返回 TRUE。log_output(“日志主题别名”) 这个函数将日志输出到指定的日志主题。
```
t_switch(op_ge(v("费用"),1000),log_output("VIP客户"),op_lt(v("费用"),1000),log_output("普通客户"))
```
执行结果： 该日志分发到别名为“普通客户”日志主题。
```
time:2021-10-07 13: 32: 21 地域:三亚 客人姓名:阿珂   客人状态:入住成功  费用:500 身份证:501123******230123
```
执行结果：该日志分发到别名为“VIP客户”日志主题。 
```
time:2021-10-07 13: 32: 21 地域:三亚 客人姓名:韦春花  客人状态:退房    费用:1000 身份证:101123******230123  
```


## 注意事项

- log_output(“日志主题别名”)，在新建数据加工任务时，给目标日志主题指定一个别名。别名的好处在于不用写日志集合和日志主题两个参数，也具备一定的可读性，方便用户后续修改名字，但无需更改日志主题的名称。
- regex_replace("字段名",regex="正则匹配语句",repalce="替换的字符串")，函数返回的是字符串，因此不能单独使用，要使用 fields_set("字段名","字段值") 将其写入目标字段。

