## Preparations

1. Multi-File Zipping is implemented with Tencent Cloud Serverless Cloud Function (SCF). You need to log in to the COS console and create a **multi-file zipping** function.For the creation guide, see [Multi-File Zipping](https://www.tencentcloud.com/document/product/436/41625).
2. After creating the function, click **Instructions** on the right of the function to configure it. The configurations are a **JSON string**, which will be described in detail in this document.
 - If your function needs SCF authentication, you need to call the `Invoke` API provided by SCF to run your cloud function, where the `ClientContext` parameter is passed in JSON format (see [Parameter Configuration Sample](#1) for details).
 - For authentication-free functions, you can directly make HTTP requests to the corresponding API gateway to call the function.


<span id=1></span>

## Parameter Configuration Sample

>? In actual use, remove the comments from the code.
>

```plaintext
{
    "bucket": "examplebucket-1250000000",    // Bucket to deliver the final ZIP package
    "region": "ap-guangzhou",         // Region where the bucket resides
    "key": "mypack.zip",              // Name of the final ZIP package
    "flatten": false,                 // Whether to flatten source file paths

    /**
     * “sourceList” (a JSON array) is used to specify the list of source files that need to be zipped.
     * Each item includes the source file URL, “renamePath”, and more.
     * 
     * If the source file list is too long, you can JSON stringify the “sourceList” parameter.
     * Write the .json file, upload it to COS, and specify it with the “sourceConfigList” parameter.
     * 
     * You only need to specify either “sourceList” or “sourceConfigList”.
     */
    "sourceList": [
        {
            "url": "https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/dir1/file1.jpg",
            "renamePath": "dir1_rename/file1.jpg"
        },
        {
            "url": "https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/dir2/file2.mp4",
            "renamePath": "file2.mp4"
        },
        {
            "url": "https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/file3.md"
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
| bucket  | Bucket to store the final ZIP package, formatted as `BucketName-APPID` (e.g., `examplebucket-1250000000`) | String  | Yes |
| region  | Region where the bucket that stores the final ZIP package resides. For more information, please see [Region and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String  | Yes |
| key | Name (i.e., object key that uniquely identifies an object in the bucket) of the final ZIP package. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String  | Yes |
| flatten  | Whether to flatten source file paths (i.e., flatten the original directory structure). For example, if a source file’s URL is `https://domain/source/test.mp4`, its path will be `source/test.mp4`. If you set this parameter to `true`, its path in the ZIP package will be `test.mp4`. If you set this parameter to `false` (default), its path will be `source/test.mp4`. | Boolean | No |
| sourceList | A list of source files. **Either `sourceList` or `sourceConfigList` must be specified.** | Array   | Yes |
| sourceList[].url  | URL of a source file | String  | Yes |
| sourceList[].renamePath | Renames the path of a source file path in the final ZIP package. For example, you can rename `dir1/file1.jpg` to `dir1_rename/file1.jpg`.<br>Note: `renamePath` has a higher priority over `flatten`, which means the flattening operation will not take effect to the renamed path. | String | No |
| sourceConfigList        | A list of `sourceList` configuration files. If you don’t want to include the entire `sourceList` in a request, you can JSON stringify the `sourceList` parameter to generate a JSON configuration file, upload it to COS, and specify the URL of that configuration file in `sourceConfigList` (multiple configuration files can be specified). **Either `sourceList` or `sourceConfigList` must be specified**. | Array   | No |
| sourceConfigList[].url  | URL of a `sourceList` configuration file | String  | No |

## Function Response Sample
```plaintext
{
  code: 0,
  data: {
    Bucket: "examplebucket-1250000000",
    ETag: "\"35bb5e5f050e22bed8f443d8da5dbfb8-1\"",
    Key: "mypack.zip",
    Location: "examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/mypack.zip"
  },
  error: null,
  message: "cos zip file success"
}
```

The response parameters are as follows:

| Parameter | Description | Type |
| ------- | ------------------------------------------------------ | ---------------- |
| code    | Service error code. `0` indicates successful execution. Other numbers indicate failure. | Number  |
| message | Message for the execution results, which may be `null` | String   |
| data    | Message for successful execution. If the execution is successful, this parameter includes the URL of the ZIP package. | Object |
| error   | Error message. If the execution is successful, the value is `null`. | Object/String |

## Samples

### Sample 1: simple use case

### Parameter configuration
```plaintext
{
  "bucket": "examplebucket-1250000000",
  "region": "ap-guangzhou",
  "key": "mypack.zip",
  "flatten": false,
  "sourceList": [
      {
          "url": "https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/dir1/file1.jpg"
      },
      {
          "url": "https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/dir2/file2.mp4"
      },
      {
          "url": "https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/file3.md"
      }
  ]
}
```

#### ZIP package structure

```plaintext
mypack.zip
    ├── dir1/file1.jpg
    ├── dir2/file2.mp4
    └── file3.md
```

### Sample 2: flattening the source file paths

### Parameter configuration
```plaintext
{
  "bucket": "examplebucket-1250000000",
  "region": "ap-guangzhou",
  "key": "mypack.zip",
  "flatten": true,                  // Set “flatten” to “true” to flatten the source file paths.
  "sourceList": [
      {
          "url": "https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/dir1/file1.jpg"
      },
      {
          "url": "https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/dir2/file2.mp4"
      },
      {
          "url": "https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/file3.md"
      }
  ]
}
```

#### ZIP package structure

```plaintext
mypack.zip
    ├── file1.jpg
    ├── file2.mp4
    └── file3.md
```


### Sample3: renaming source file paths

### Parameter configuration
```plaintext
{
  "bucket": "examplebucket-1250000000",
  "region": "ap-guangzhou",
  "key": "mypack.zip",
  "flatten": false,
  "sourceList": [
      {
          "url": "https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/dir1/file1.jpg",
          // Rename “dir1/file1.jpg” to “dir1_rename/file1.jpg”.
          "renamePath": "dir1_rename/file1.jpg"
      },
      {
          "url": "https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/dir2/file2.mp4",
          // Rename “dir2/file2.mp4” to “file2.mp4”.
          "renamePath": "file2.mp4"
      },
      {
          "url": "https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/file3.md"
      }
  ]
}
```

#### ZIP package structure

```plaintext
mypack.zip
    ├── dir1_rename/file1.jpg
    ├── file2.mp4
    └── file3.md
```

### Sample 4: renaming and flattening source file paths

### Parameter configuration
```plaintext
{
  "bucket": "examplebucket-1250000000",
  "region": "ap-guangzhou",
  "key": "mypack.zip",
  "flatten": true,         // Set “flatten” to “true” to flatten source file paths.
  "sourceList": [
      {
          "url": "https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/dir1/file1.jpg"
      },
      {
          "url": "https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/dir2/file2.mp4"
      },
      {
          "url": "https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/file3.md",
          // Rename “file3.md” to “dir3/file3.md”. As “renamePath” has a higher priority over “flatten”, the renamed path will not be flattened.
          "renamePath": "dir3/file3.md"
      }
  ]
}
```

#### ZIP package structure

```plaintext
mypack.zip
    ├── file1.jpg
    ├── file2.mp4
    └── dir3/file3.md
```
