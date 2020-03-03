## API Description
 
- Domain name: account.api.qcloud.com.
- API name: DescribeProject
- API description: this API is used to query the project list. Project is a virtual concept. You can create multiple projects under one account and manage different resources in each project.

 

## Input Parameters
 

<table class="t"><tbody><tr>
<th><b>Parameter Name</b></th>
<th><b>Required</b></th>
<th><b>Type</b></th>
<th><b>Description</b></th>
<tr>
<td>  allList <td> No <td> Int
 <td> If this parameter is 1, all projects (including hidden ones) will be queried. If it is left empty or 0, only non-hidden projects will be queried.


</tbody></table>

 

## Output Parameters
 | Parameter | Type | Description |
|---------|---------|---------|
| code |  Int | Error code. 0: success, other values: failure |
| message | String | Error message |
| data | Array | Array of returned results |

Data structure 

<table class="t"><tbody><tr>
<th><b>Parameter Name</b></th>
<th><b>Type</b></th>
<th><b>Description</b></th>
<tr>
<td> projectName <td> String <td> Project name
<tr>
<td> projectId <td> String <td> Project ID
<tr>
<td> createTime <td> String <td> Project creation time
<tr>
<td> creatorUin <td> String <td> Project creator
<tr>
<td> projectInfo <td> String <td> Project description
</tbody></table>

 

## Samples
 
### Input
<pre>
  https://account.api.qcloud.com/v2/index.php?Action=DescribeProject
  &<a href="https://intl.cloud.tencent.com/document/product/378/4380">Common request parameters</a>
</pre>


### Output
```
{
    "code": 0,
    "message": "",
    "data": [
        {
            "projectName": "test1",
            "projectId": 1002189,
            "createTime": "2015-04-28 14:42:53",
            "creatorUin": 670569769,
	        "projectInfo": "info1"
        },  
        {
            "projectName": "test2",
            "projectId": 1002190,
            "createTime": "2015-04-28 14:42:57",
            "creatorUin": 670569769,
	        "projectInfo": "info2"
        }   
    ]
}
```

