## Preparations

1. The ZIP decompression feature is implemented via the Serverless Cloud Function (SCF) service. Before use, you need to go to [ZIP Decompression](https://console.cloud.tencent.com/cos5/application/cosGunzipApi) in the COS console to create a **ZIP Decompression** function. For more function creation instructions, see [ZIP Decompression](https://intl.cloud.tencent.com/document/product/436/45163).
2. After creating the function, click **Instructions** on the right of the function to configure it. The configurations are a **JSON string**, which will be described in detail in this document.
 - If you select SCF authentication for the function, you need to call the [Invoke](https://intl.cloud.tencent.com/document/product/583/17243) API provided by SCF to run the ZIP decompression function, where the `ClientContext` parameter is passed in JSON format. For more information, see [Function Parameter Configuration Sample](#1).
 - If you configure the function to be authentication free, you can directly send HTTP requests to the corresponding API to call the function.


<span id=1></span>
## Function Parameter Configuration Example

>? In actual practice, delete the comments in the code.
>

```plaintext
{
    "bucket": "examplebucket-1250000000",    // Source bucket storing the ZIP package
    "region": "ap-guangzhou",         // Region where the bucket resides
    "key": "example.zip",              //  Name of the ZIP package
    "targetBucket": "examplebucket-1250000000",    // Target bucket to store the decompressed objects
    "region": "ap-guangzhou",         // Region where the target bucket resides
    "targetPrefix": "target/",              // Prefix of the directory to store the decompressed objects
}
```

The parameters are described as follows:

| Parameter | Description | Type | Required |
| ------------ | ------------------------------------------------------------ | ------ | -------- |
| bucket  | Source bucket storing the ZIP package, formatted as `BucketName-APPID` (e.g., `examplebucket-1250000000`) | String  | Yes |
| region | Source bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| key                     | Name (object name) of the ZIP package. It is the unique ID of an object in a bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String  | Yes       |
| targetBucket                  | Target bucket to store the decompressed objects, formatted as `BucketName-APPID` (e.g., `examplebucket-1250000000`). | String  | Yes       |
| targetRegion                  | Target bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String  | Yes       |
| targetPrefix | Prefix of the directory to store the decompressed objects. End a specified directory with `/` for saving to this directory, or keep it empty for saving to the root directory | String | No       |

## Sample Response
```plaintext
{
    "code": 0,
    "message": "cos gunzip file success",
    "data": {
        "Bucket": "examplebucket-1250000000",
        "Region": "ap-guangzhou"
    }
}
```

Response parameters are described as follows:

| Parameter | Description | Type |
| ------- | ------------------------------------------------------------ | ---------------- |
| code    | Business error code. `0`: the execution is successful. Other values: execution failed.    | Number           |
| message | Text description of the execution result. The message may be `null`.                        | String           |
| data    | Information on successful execution. If the execution is successful, it contains information about the target bucket. | Object           |
| error   | Execution failure information. If the execution is successful, this parameter is `null`.                    | Object or String |

## Examples

### Example 1. Decompress a file `*.zip`

#### Parameter configuration

```plaintext
{
  "bucket": "examplebucket-1250000000",
  "region": "ap-guangzhou",
  "key": "example.zip",
  "targetBucket": "examplebucket-1250000000",
  "targetRegion": "ap-guangzhou",
  "targetPrefix": "target/"
}
```

#### Location of the decompressed objects

```plaintext
target/example.txt
```
