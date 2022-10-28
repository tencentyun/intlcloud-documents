## Use Case

Tom has collected a log to CLS. The log contains sensitive information such as the user ID (**dev@12345**), login IP (**11.111.137.225**), and mobile number (**13912345678**). Tom wants to mask these sensitive information.

## Scenario Analysis

The log itself is a structured log, and therefore its fields can be masked directly.

## Raw Log
``` 
    {
        "Id": "dev@12345",
        "Ip": "11.111.137.225",
        "phonenumber": "13912345678"
    }
```

## DSL Processing Function

```
fields_set("Id",regex_replace(v("Id"),regex="\d{3}", replace="***",count=0))
fields_set("Id",regex_replace(v("Id"),regex="\S{2}", replace="**",count=1))
fields_set("phonenumber",regex_replace(v("phonenumber"),regex="(\d{0,3})\d{4}(\d{4})", replace="$1****$2"))
fields_set("Ip",regex_replace(v("Ip"),regex="(\d+\.)\d+(\.\d+\.\d+)", replace="$1***$2",count=0))
```

## DSL Processing Function Details 

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

## Processing Result

```
{"Id":"**v@***45","Ip":"11.***.137.225","phonenumber":"139****5678"} 
```
