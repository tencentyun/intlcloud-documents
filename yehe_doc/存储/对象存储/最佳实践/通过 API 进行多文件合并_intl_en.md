## Preparations

1. The object concatenation feature is implemented via Serverless Cloud Function (SCF). Before using it, you need to go to the COS console to create an **object concatenation** function on [Application Integration - Object Concatenation](https://console.cloud.tencent.com/cos5/application/cosConcatFile).
2. After creating the function, set the function parameters according to the **instructions** in the operation column of the function list. The parameters are in **JSON string** format and detailed below.
 - If you select SCF authentication for the function, you need to call the [Invoke](https://intl.cloud.tencent.com/document/api/583/17243) API provided by SCF to run the object concatenation function, where the `ClientContext` parameter is passed in JSON format. For more information, please see [Function Parameter Configuration Sample](#1).
 - If you configure the function to be authentication free, you can directly send HTTP requests to the corresponding API to call the function.


<span id=1></span>

## Function Parameter Configuration Sample

>? In actual practice, delete the comments in the code.
>

```plaintext
{
    "bucket": "examplebucket-1250000000",    // Bucket of the output merged file for final delivery
    "region": "ap-guangzhou",         // Region of the bucket of the output merged file for final delivery
    "key": "concat.txt",              // Name of the output merged file for final delivery

    /**
     * `sourceList` specifies the list of source files that need to be packaged and is a JSON array.
     * Each item contains information such as the source file URL, and more parameters may be extended in the future.
     * 
     * If the source file list is excessively long, you can convert the value of `sourceList` into a JSON string,
     * write the JSON string into a .json file, upload the file to COS, and specify the URL of the file in the `sourceConfigList` parameter.
     * 
     * You only need to specify either `sourceList` or `sourceConfigList`.
     */
    "sourceList": [
        {
            "url": "https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/file1.txt"
        },
        {
            "url": "https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/file2.txt"
        },
        {
            "url": "https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/file3.txt"
        }
    ],
    "sourceConfigList": [
        {
             "url": "https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceList.json"
        }
    ]
}
```

The parameters are described as follows:

| Parameter | Description | Type | Required |
| ----------------------- | ------------------------------------------------------------ | ------- | -------- |
| bucket                  | Bucket of the output merged file for final delivery, in the format of `BucketName-APPID`, for example, `examplebucket-1250000000`. | String  | Yes       |
| region                  | Region of the bucket of the output merged file for final delivery. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String  | Yes       |
| key                     | Name (object name) of the output merged file for final delivery. It is the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String  | Yes       |
| sourceList              | List of source files. **`sourceList` and `sourceConfigList` cannot be empty at the same time.**  | Array   | Yes       |
| sourceList[].url        | URL of the source files.                                                 | String  | Yes       |
| sourceConfigList        | Configuration file list of `sourceList`. If you do not want the request to carry the entire `sourceList`, you can convert the value of the `sourceList` into a JSON string, generate a JSON configuration file, upload the file to COS, and specify the URL of the file in the `sourceConfigList` parameter. **`sourceList` and `sourceConfigList` cannot be empty at the same time. ** | Array   | No       |
| sourceConfigList[].url  | URL of the `sourceList` configuration file.                                    | String  | No       |

## Function Response Sample
```plaintext
{
    "code": 0,
    "message": "cos concat file success",
    "data": {
        "Location": "examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/concat.txt",
        "Bucket": "examplebucket-1250000000",
        "Key": "concat.txt",
        "ETag": "\"152958e4f4bfded94c0b30f03343d6b8-1\""
    }
}
```

Response parameters are described as follows:

| Parameter  | Description                                               | Type             |
| ------- | ------------------------------------------------------ | ---------------- |
| code    | Business error code. `0`: the execution is successful. Other values: execution failed.    | Number           |
| message | Text description of the execution result. The message may be `null`.                        | String           |
| data    | Execution success information. If the execution is successful, this parameter contains the URL of the output merged file. | Object           |
| error   | Execution failure information. If the execution is successful, this parameter is `null`.                    | Object or String |

## Example



### Parameter configuration
```plaintext
{
  "bucket": "examplebucket-1250000000",
  "region": "ap-guangzhou",
  "key": "concat.txt",
  "sourceList": [
      {
          "url": "https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/file1.txt"
      },
      {
          "url": "https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/file2.txt"
      },
      {
          "url": "https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/file3.txt"
      }
  ]
}
```

### Structure of the final output of object concatenation

```plaintext
concat.txt
    ├── content of file1.txt
    ├── content of file2.txt
    └── content of file3.txt
```
