## 1. API Description
This API (DuplicateImage) duplicates the specified an image tag.
API domain name: `ccr.api.qcloud.com`

## 2. Input Parameters
The following parameters are action-specific. For common parameters required for all API requests, see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/457/9463).

| Parameter Name | Description | Type | Required | 
|---------|---------|---------|---------
| src_image | Source image name (domain not included). For example: tencentyun/foo:v1 | String | Yes |wf 
| dest_image | Destination image name (domain not included). For example: tencentyun/foo:latest | String | Yes |

## 3. Output Parameters
 
| Parameter Name | Description | Type | 
|---------|---------|---------|
| code | Common error code. 0: Successful; other values: Failed. | Int | 
| codeDesc | Description of the action status. When the action has succeeded, "Success" is returned. When the action has failed, a message describing the cause of the error is returned. | String |
| message | Description of the Module error related to this API | String |

## 4. Samples
Input

```
  https://domain/v2/index.php?Action=DuplicateImage
  &src_image=tencentyun/foo:v1
  &dest_image=tencentyun/foo:latest  
  &other common parameters
```
Output

```
{
    "code": 0,
    "message": "", 
    "codeDesc": "Success"
}

```