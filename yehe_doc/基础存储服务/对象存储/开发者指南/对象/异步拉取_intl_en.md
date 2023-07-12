
## Overview

The asynchronous origin-pull feature allows you to pull specific files from a specified origin server and store them to COS. To use this feature, the COS service role needs to be authorized.

## Authorizing a COS Service Role 

To use asynchronous origin-pull, the COS service role needs to be authorized so that it can upload data from the specified origin server to the specified bucket. Therefore, you need to add a corresponding policy to your bucket. The policy syntax is as follows:

```
{
      "Statement": [
        {
          "Principal": {
             "service": "cos.qcloud.com"
          },
          "Effect": "Allow",
          "Action": [
             "name/cos:PutObject",
             "name/cos:InitiateMultipartUpload",
             "name/cos:UploadPart",
             "name/cos:CompleteMultipartUpload"
          ],
          "Resource": [
             "qcs::cos:<Region>:uid/<APPID>:<BucketName-APPID>/*"
          ]
        }
      ],
      "version": "2.0"
}
```

>? In the policy syntax above, the six-segment value of the `Resource` field needs to be modified as needed. Please change `Region` to the region where your bucket resides, `APPID` to your actual `APPID`, and `BucketName` to the name of your bucket.
>

Take the `examplebucket-12500000000` bucket in the Guangzhou region as an example. If you want to allow uploading files to the root directory, the policy syntax should be changed to:

```
"Resource": [
         "qcs::cos:ap-guangzhou:uid/12500000000:examplebucket-12500000000/*"
]
```

To allow uploading files to the `prefix` directory, change the policy syntax to:

```
"Resource": [
         "qcs::cos:ap-guangzhou:uid/12500000000:examplebucket-12500000000/prefix/*"
]
```

## How to Use

### Using RESTful APIs

You can use RESTful APIs to initiate an asynchronous origin-pull request. For more information, please see **Querying Origin-Pull Progress** and **Initiating Offline Origin-Pull**.

### Using SDKs

You can call the SDK to perform asynchronous origin-pull. For more information, please see the [Demo on GitHub](https://github.com/tencentyun/cos-python-sdk-v5/blob/master/demo/fetch_demo.py).

