## Prerequisites

1. The GZIP decompression feature is implemented via the Serverless Cloud Function (SCF) service. Before use, you need to create a **GZIP Decompression** function in the COS console. For detailed directions on how to create a function, see [Using Console to Configure Auto GZIP File Decompression](https://intl.cloud.tencent.com/document/product/436/46202).
2. After creating the function, click **Instructions** on the right of the function to configure it. The configuration items are a **JSON string**, which will be as described in detail in this document.
 - If your function needs SCF authentication, you need to call the `Invoke` API provided by SCF to run your cloud function, where the `ClientContext` parameter is passed in JSON format (see [Sample Function Parameter Configuration](#1) for details).
 - If you configure the function to be authentication free, you can directly send HTTP requests to the corresponding API gateway to call the function.


<span id=1></span>
## Sample Function Parameter Configuration

>? In actual practice, delete the comments in the code.
>

```plaintext
{
    "bucket": "examplebucket-1250000000",    // Source bucket storing the GZIP package
    "region": "ap-guangzhou",         // Region where the source bucket storing the GZIP package resides
    "key": "example.txt.gz",              //  GZIP package name
    "targetBucket": "examplebucket-1250000000",    // Destination bucket to store the decompressed objects
    "targetRegion": "ap-guangzhou",         // Region where the destination bucket resides
    "targetPrefix": "target/",              // Prefix of the directory to store the decompressed objects
}
```

The parameters are as described below:

| Parameter | Description | Type | Required |
| ----------------------- | ------------------------------------------------------------ | ------- | -------- |
| bucket  | Source bucket storing the GZIP package in the format of `BucketName-APPID`, such as `examplebucket-1250000000`. | String  | Yes |
| region | Region of the source bucket storing the GZIP package. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| key | GZIP package name (object name), which is the unique identifier of the object in the bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| targetBucket                  | Destination bucket to store the decompressed objects in the format of `BucketName-APPID`, such as `examplebucket-1250000000`. | String  | Yes       |
| targetRegion                  | Destination bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String  | Yes       |
| targetPrefix | Prefix of the directory to store the decompressed objects. End a specified directory with a slash for saving to this directory, or keep it empty for saving to the root directory. | String | No       |

## Sample Function Response
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

Response parameters are as described below:

| Parameter  | Description                                               | Type             |
| ------- | ------------------------------------------------------ | ---------------- |
| code    | Business error code. 0: The execution is successful. Other values: Execution failed.    | Number           |
| message | Text description of the execution result. The message may be `null`.                        | String           |
| data    | Information of successful execution. If the execution is successful, it contains information of the destination bucket. | Object           |
| error   | Execution failure information. If the execution is successful, this parameter is `null`.                    | Object or String |

## Use Cases

### Use case 1: Decompressing a *.gz file

### Parameter configuration

```plaintext
{
  "bucket": "examplebucket-1250000000",
  "region": "ap-guangzhou",
  "key": "example.txt.gz",
  "targetBucket": "examplebucket-1250000000",
  "targetRegion": "ap-guangzhou",
  "targetPrefix": "target/"
}
```

#### Location of decompressed objects

```plaintext
target/example.txt
```

### Use case 2: Decompressing *.tar.gz and *.tgz files

### Parameter configuration
```plaintext
{
  "bucket": "examplebucket-1250000000",
  "region": "ap-guangzhou",
  "key": "example.tar.gz",
  "targetBucket": "examplebucket-1250000000",
  "targetRegion": "ap-guangzhou",
  "targetPrefix": "target/"
}
```

#### Compressed package structure

```
example.tar.gz
    ├── example-subfile-1.txt
    ├── example-subfile-2.png
    └── example-subfile-3.mp4
```

#### Location of decompressed objects

```plaintext
target/example-subfile-1.txt
target/example-subfile-2.png
target/example-subfile-3.mp4
```
