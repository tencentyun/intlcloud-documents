## Use Case

Tom has collected logs to in nested JSON format to CLS. Now he wants to extract the **user** (secondary nested field) and **App** fields from the logs.

## Raw Log

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

## DSL Processing Function

- Option 1. Use the **JMES** formula to extract fields directly without expanding all key-value pairs
```
ext_json_jmes("content", jmes="resonsebody.user", output="user")
ext_json_jmes("content", jmes="App", output="App")
```
- Option 2. Expand all key-value pairs and discard unwanted fields
```
ext_json("content")
fields_drop("content")
fields_drop("bytes_sent","method","response_code_details","start_time")
```

## DSL Processing Function Details 

- Option 1: 
 1. Use the JMES formula **resonsebody.user** to directly specify the secondary nested field **user**.
```
ext_json_jmes("content", jmes="resonsebody.user", output="user")
```
 2. Use the JMES formula **App** to directly specify the **App** field.
```
ext_json_jmes("content", jmes="App", output="App")
```
- Option 2:  
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

## Processing Result

```
[{"App":"App-1","user":"Tom"},
{"App":"App-2","user":"Jerry"}]
```
