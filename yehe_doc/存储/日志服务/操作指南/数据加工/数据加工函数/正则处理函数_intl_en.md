## Overview

Logs contain a large volume of text. When processing text, you can use regular expression functions to flexibly extract keywords, mask fields, or determine whether the text contains specified characters. See the figure below.

![](https://qcloudimg.tencent-cloud.cn/raw/c8816ff54a4c6551b57ce6da20ed07a3.png)

For examples of regular expressions commonly used in log scenarios, visit [Online Test of Regular Expressions](https://c.runoob.com/front-end/854/).

| Purpose | Raw Log | Regular Expression | Extraction Result |
|---------|---------|---------|---------|
| Extract content in braces. | `[2021-11-24 11:11:08,232][328495eb-b562-478f-9d5d-3bf7e][INFO] curl -H 'Host: ' http://abc.com:8080/pc/api -d '{"version": "1.0", "user": "CGW", "password": "123", "timestamp": 1637723468, "interface": {"Name": "ListDetail", "para": {"owner": "1253", "limit": [10, 14], "orderField": "createTime"}}}` | \\{[^\\}]+\\} | {"version": "1.0", "user": "CGW", "password": "123", "timestamp": 1637723468, "interface": {"Name": "ListDetail", "para": {"owner": "1253", "limit": [10, 10], "orderField": "createTime"} |
| Extract content in brackets. | `[2021-11-24 11:11:08,232][328495eb-b562-478f-9d5d-3bf7e][INFO] curl -H 'Host: ' http://abc.com:8080/pc/api -d '{"version": "1.0", "user": "CGW", "password": "123", "timestamp": 1637723468, "interface": {"Name": "ListDetail", "para": {"owner": "1253", "limit": [10, 14], "orderField": "createTime"}}}` | \\[\S+\\] | [328495eb-b562-478f-9d5d-3bf7e]</br>[INFO] |
| Extract time. | `[2021-11-24 11:11:08,232][328495eb-b562-478f-9d5d-3bf7e][INFO] curl -H 'Host: ' http://abc.com:8080/pc/api -d '{"version": "1.0", "user": "CGW", "password": "123", "timestamp": 1637723468, "interface": {"Name": "ListDetail", "para": {"owner": "1253", "limit": [10, 14], "orderField": "createTime"}}}` | \d{4}-\d{2}-\d{2} \d{2}:\d{2}:\d{2},\d{3} | `2021-11-08 11:11:08,232` |
| Extract uppercase characters of a specific length. | `[2021-11-24 11:11:08,232][328495eb-b562-478f-9d5d-3bf7e][INFO] curl -H 'Host: ' http://abc.com:8080/pc/api -d '{"version": "1.0", "user": "CGW", "password": "123", "timestamp": 1637723468, "interface": {"Name": "ListDetail", "para": {"owner": "1253", "limit": [10, 14], "orderField": "createTime"}}}` | [A-Z]{4} | INFO |
| Extract lowercase characters of a specific length. | `[2021-11-24 11:11:08,232][328495eb-b562-478f-9d5d-3bf7e][INFO] curl -H 'Host: ' http://abc.com:8080/pc/api -d '{"version": "1.0", "user": "CGW", "password": "123", "timestamp": 1637723468, "interface": {"Name": "ListDetail", "para": {"owner": "1253", "limit": [10, 15], "orderField": "createTime"}}}` | [a-z]{6} | versio</br>passwo</br>timest</br>interf</br>create |
| Extract letters and digits. | `[2021-11-24 11:11:08,232][328495eb-b562-478f-9d5d-3bf7e][INFO] curl -H 'Host: ' http://abc.com:8080/pc/api -d '{"version": "1.0", "user": "CGW", "password": "123", "timestamp": 1637723468, "interface": {"Name": "ListDetail", "para": {"owner": "1253", "limit": [10, 14], "orderField": "createTime"}}}` | ([a-z]{3}):([0-9]{4}) | com:8080 |

## Function regex_match

#### Function definition

This function is used to match data in full or partial match mode based on a regular expression and return whether the match is successful.

##### Syntax description

```sql
regex_match(Field value, regex="", full=True)
```

#### Parameter description

| Parameter | Description | Parameter Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
|data| Field value |string| Yes | -  | -  |
|regex| Regular expression |string| Yes | -  | -  |
|full| Whether to enable full match. For full match, the entire value must fully match the regular expression. For partial match, only part of the value needs to match the regular expression. |bool| No |True| -  |


#### Sample

- Example 1. Check whether the regular expression "192\.168.\*" fully matches the value `192.168.0.1` of the field `IP` (full=True). The `regex_match` function returns `True` for the case of full match.
Raw log:
```
{"IP":"192.168.0.1", "status": "500"}
```
Processing rule:
```
// Check whether the regular expression "192\.168.*" fully matches the value `192.168.0.1` of the field `IP` and save the result to the new field `matched`.
t_if(regex_match(v("IP"), regex="192\.168.*", full=True), fields_set("matched", True))
```
Processing result:
```
{"IP":"192.168.0.1","matched":"TRUE","status":"500"}
```
- Example 2. Check whether the regular expression "192\*" partially matches the value `192.168.0.1` of the field `IP` (full=False). The `regex_match` function returns `True` for the case of partial match.
Raw log:
```
{"IP":"192.168.0.1", "status": "500"}
```
Processing rule:
```
t_if(regex_match(v("ip"), regex="192", full=False), fields_set("matched", True))
```
Processing result:
```
{"IP":"192.168.0.1","matched":"TRUE","status":"500"}
```


## Function regex_select

#### Function definition

This function is used to match data based on a regular expression and returns the corresponding partial match result. You can specify the sequence number of the matched expression and the sequence number of the group to return (partial match + sequence number of the specified matched group). If no data is matched, an empty string is returned.

#### Syntax description

```sql
regex_select(Field value, regex="", index=1, group=1)
```

#### Parameter description

| Parameter | Description | Parameter Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
|data| Field value |string| Yes | -  | -  |
|regex| Regular expression |string| Yes | -  | -  |
|index| Sequence number of the matched expression in the match result |number| No | First | -  |
|group| Sequence number of the matched group in the match result |number| No | First | -  |


#### Sample

Capture different content from a field value based on a regular expression. 

Raw log:
```
{"data":"hello123,world456", "status": "500"}
```
Processing rule:
```
fields_set("match_result", regex_select(v("data"), regex="[a-z]+(\d+)",index=0, group=0))
fields_set("match_result1", regex_select(v("data"), regex="[a-z]+(\d+)", index=1, group=0))
fields_set("match_result2", regex_select(v("data"), regex="([a-z]+)(\d+)",index=0, group=0))
fields_set("match_result3", regex_select(v("data"), regex="([a-z]+)(\d+)",index=0, group=1))
```
Processing result:
```
{"match_result2":"hello123","match_result1":"world456","data":"hello123,world456","match_result3":"hello","match_result":"hello123","status":"500"}
```

## Function regex_split

#### Function definition

This function is used to split a string and return a JSON array of the split strings (partial match).

#### Syntax description

```sql
regex_split(Field value, regex=\"\", limit=100)
```

#### Parameter description

| Parameter | Description | Parameter Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
|data| Field value |string| Yes | -  | -  |
|regex| Regular expression |string| Yes | -  | -  |
|limit| Maximum array length for splitting. When this length is exceeded, the excessive part will be split, constructed as an element, and added to the array. |number | No | 100 | -  |


#### Sample

Raw log:
```
{"data":"hello123world456", "status": "500"}
```
Processing rule:
```
fields_set("split_result", regex_split(v("data"), regex="\d+"))
```
Processing result:
```
{"data":"hello123world456","split_result":"[\"hello\",\"world\"]","status":"500"}
```


## Function regex_replace

#### Function definition

This function is used to match data based on a regular expression and replace the matched data (partial match).

#### Syntax description

```sql
regex_replace(Field value, regex="", replace="", count=0)
```

#### Parameter description

| Parameter | Description | Parameter Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
|data| Field value |string| Yes | -  | -  |
|regex| Regular expression |string| Yes | -  | -  |
|replace| Target string, which is used to replace the matched result |string| Yes | -  | -  |
|count| Replacement count. The default value is `0`, indicating complete replacement. |number| No | 0 | -  |


#### Sample

- Example 1. Replaces a field value based on a regular expression
Raw log:
```
{"data":"hello123world456", "status": "500"}
```
Processing rule:
```
fields_set("replace_result", regex_replace(v("data"), regex="\d+", replace="", count=0))
```
Processing result:
```
{"replace_result":"helloworld","data":"hello123world456","status":"500"}
```

- Example 2. Mask the user ID, phone number, and IP address
Raw log:
```
{"Id": "dev@12345","Ip": "11.111.137.225","phonenumber": "13912345678"}
```
Processing rule:
```
// Mask the `Id` field. The result is `dev@***45`.
fields_set("Id",regex_replace(v("Id"),regex="\d{3}", replace="***",count=0))
fields_set("Id",regex_replace(v("Id"),regex="\S{2}", replace="**",count=1))
// Mask the `phonenumber` field by replacing the middle 4 digits with ****. The result is `139****5678`.
fields_set("phonenumber",regex_replace(v("phonenumber"),regex="(\d{0,3})\d{4}(\d{4})", replace="$1****$2"))
// Mask the `Ip` field by replacing the octet with ***. The result is `11.***137.225`.
fields_set("Ip",regex_replace(v("Ip"),regex="(\d+\.)\d+(\.\d+\.\d+)", replace="$1***$2",count=0))
```
Processing result:
```
{"Id":"**v@***45","Ip":"11.***.137.225","phonenumber":"139****5678"}
```

## Function regex_findall

#### Function definition

This function is used to match data based on a regular expression and return a JSON array of the matched data (partial match).

#### Syntax description

```sql
regex_findall(Field value, regex="")
```

#### Parameter description

| Parameter | Description | Parameter Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
|data| Field value |string|Yes| -  | -  |
|regex| Regular expression |string| Yes | -  | -  |

#### Sample

Raw log:
```
{"data":"hello123world456", "status": "500"}
```
Processing rule:
```
fields_set("result", regex_findall(v("data"), regex="\d+"))
```
Processing result:
```
{"result":"[\"123\",\"456\"]","data":"hello123world456","status":"500"}
```
