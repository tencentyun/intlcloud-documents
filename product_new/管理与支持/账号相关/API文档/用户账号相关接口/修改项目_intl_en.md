## API Description

- Domain name: tag.api.qcloud.com. 
- API name: UpdateProject
- API description: this API is used to modify the information of a project.

## Input Parameters

| Parameter Name | 	Required	 | Type	 | Description |
|-----|-----|----|-----|
|projectId|	Yes|	Int	| Project ID |
|name|	No	|String	| Project name |
|info|	No |	String|	Description |

## Output Parameters

| Parameter Name | Type | Description |
|-----|------|-------|
|code| Int | Error code. 0: success; other values: failure |
|message |String | Error message |
|data |Array| Array of returned results |

## Samples
### Input

<pre>
https://tag.api.qcloud.com/v2/index.php?Action=UpdateProject 
&<a href="https://intl.cloud.tencent.com/document/product/378/4380">Common request parameters</a>
</pre>

### Output
```
{
    "code": 0,
    "message": "",
    "data": []
}
```
