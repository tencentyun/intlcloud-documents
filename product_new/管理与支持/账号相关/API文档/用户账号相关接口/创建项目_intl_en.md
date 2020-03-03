## API Description
 
- Domain name: account.api.qcloud.com.
- API name: AddProject
- API description: this API is used to create a project. Project is a virtual concept. You can create up to 100 projects under one account and manage different resources in each project.

 

## Input Parameters
 

<table class="t"><tbody><tr>
<th><b>Parameter Name</b></th>
<th><b>Required</b></th>
<th><b>Type</b></th>
<th><b>Description</b></th>
<tr>
<td> projectName <td> Yes <td> String <td> Project name containing letters and digits
<tr>
<td> projectDesc <td> No <td> String <td> Project description
</tbody></table>

 

## Output Parameters
 

<table class="t"><tbody><tr>
<th><b>Parameter Name</b></th>
<th><b>Type</b></th>
<th><b>Description</b></th>
<tr>
<td> code <td> Int <td> Error code. 0: success; other values: failure
<tr>
<td> message <td> String <td> Error message
<tr>
<td> projectId <td> Int <td> Project ID
</tbody></table>

 

## Samples
 
### Input
<pre>
  https://account.api.qcloud.com/v2/index.php?Action=AddProject
  &projectName=test
  &projectDesc=For testing
  &<a href="https://intl.cloud.tencent.com/document/product/378/4380">Common request parameters</a>
</pre>

### Output
```

{
    "code": 0,
    "message": "",
    "projectId": 1002996
}

```
