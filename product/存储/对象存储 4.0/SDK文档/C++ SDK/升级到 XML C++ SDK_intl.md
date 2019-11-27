After comparing JSON C++ SDK and XML C++ SDK documents, you may find XML C++ SDK not only increased the document numbers, but also improved in terms of architecture, availability,  security, usability, robustness and transmission. The following instructions can help you upgrade to XML C++ SDK.

## Feature Comparison

The following table compares the main features of XML C++ SDK and JSON C++ SDK:

| Feature | XML C++ SDK | JSON C++ SDK |
| -------------- | :----------------------------------------------------------: | :----------------------------------------------------------: |
| File upload | Upload of local files, byte streams and input streams is supported.<br>A file with the same name is overwritten.<br>File size is limited to 5 GB in a simple upload.<br>File size is limited to 48.82 TB (50,000 GB) in a multipart upload. | Only local file upload is supported. For files lager than 8 MB, use multipart upload.<br>You need to manually set whether to overwrite a file with the same name.<br>File size is limited to 20 MB in a simple upload.<br>File size is limited to 64 GB in a multipart upload. |
| Basic operations on buckets | Create a bucket<br>Get a bucket<br>Delete a bucket | Not supported |
| Operations on bucket ACLs | Set bucket ACL<br>Get bucket ACL<br>Delete bucket ACL | Not supported |
| Bucket lifecycle | Create bucket lifecycle<br>Get bucket lifecycle<br>Delete bucket lifecycle | Not supported |
| Directory operations | No APIs are provided separately. | Create a directory<br>Query a directory<br>Delete a directory |

## Upgrade Directions

Upgrade C++ SDK by following the 4 steps below.

**1. Update C++ SDK**

[XML C++ SDK ](https://github.com/tencentyun/cos-cpp-sdk-v5) replaces curl libraries in JSON C++ SDK with Poco libraries. Download the complete edition of Poco from [Poco official website](https://pocoproject.org/download.html), and execute the following command to install Poco libraries and header files.

```
./configure --omit=Data/ODBC,Data/MySQL
make
make install
```
You can also refer to C++ SDK [Getting Started](https://intl.cloud.tencent.com/document/product/436/12301) to select a proper installation method.

**2. Change the SDK configuration file**

XML C++ SDK and JSON C++ SDK are the same in terms of initialization, but differ in the configuration file "config.json". Make the following modifications in the XML C++ SDK configuration file:

- Delete the "APPID" in JSON C++ SDK.
- Replace `CurlConnectTimeoutInms` and `CurlGlobalConnectTimeoutInms` with `ConnectTimeoutInms`. Add `ReceiveTimeoutInms`. Implement setting APIs in the Request basic class to make modifications to different operations.
- The default initialization parameters of XML C++ SDK are described in detail in the file "cos_sys_config.cpp".
- The Region field is described differently in JSON C++ SDK and XML C++ SDK. For more information, see "Change the bucket name and the abbreviations of availability zones" below.

**3. Change the bucket name and the abbreviations of available regions**

The bucket name and the abbreviations of available regions in XML C++ SDK are different from those in JSON C++ SDK. You need to make changes accordingly.

**Bucket**

The name of an XML C++ SDK bucket consists of a user-defined string and an APPID that are connected by a dash ("-"). For example, `mybucket1-1250000000`, where `mybucket1` is a user-defined string and `1250000000` is an APPID.

>APPID is one of the Tencent Cloud account IDs, and is used to associate with cloud resources. After applying for a Tencent Cloud account successfully, you will be assigned an APPID automatically. APPID can be found in **Account Info** on the [Tencent Cloud Console](https://console.cloud.tencent.com/).

Refer to the following sample code to set a bucket:

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
// The APPID of JSON C++ SDK is written in the configuration file. The bucket of JSON C++ SDK is defined as string bucket="mybucket1";
string bucket = "mybucket1-1250000000";
qcloud_cos::HeadBucketReq req(bucket_name);
qcloud_cos::HeadBucketResp resp;
qcloud_cos::CosResult result = cos.HeadBucket(req, &resp);
```

**Abbreviations of available regions for buckets**

The abbreviations of available regions for XML C++ SDK buckets have changed. During initialization, set the abbreviation of the bucket region to `Region` in the configuration file. See the following table for region abbreviations in JSON C++ SDK and XML C++ SDK:

| Region | Abbreviation in XML C++ SDK | Abbreviation in JSON C++ SDK |
| ---------------- | ---------------- | ----------- |
| Beijing Zone 1 (North China) | ap-beijing-1 | tj |
| Beijing | ap-beijing | bj |
| Shanghai (East China) | ap-shanghai | sh |
| Guangzhou (South China) | ap-guangzhou | gz |
| Chengdu (Southwest China) | ap-chengdu | cd |
| Chongqing | ap-chongqing | None |
| Singapore | ap-singapore | sgp |
| Hong Kong | ap-hongkong | hk |
| Toronto | na-toronto | ca |
| Frankfurt | eu-frankfurt | ger |
| Mumbai | ap-mumbai | None |
| Seoul | ap-seoul | None |
| Silicon Valley | na-siliconvalley | None |
| Virginia | na-ashburn | None |
| Bangkok | ap-bangkok | None |
| Moscow | eu-moscow | None |

**4. Change APIs**

After JSON C++ SDK is upgraded to XML C++ SDK, the APIs for some operations have changed. Make the corresponding changes based on your actual needs. In addition, we have encapsulated the APIs to make it easier to use the SDK. For more information, see our examples and [API Documentation](https://intl.cloud.tencent.com/document/product/436/12301).

Here are the main changes:

**1) No directory API**

No separate directory API is provided in XML SDK. As COS comes with no folders and directories, it will not create a "project" folder for uploading the object "project/a.txt".
To make it easier for you to get started, COS simulates the display mode of "folder" or "directory" in the console and graphical tools such as COS browser. This is realized by creating an empty object with a key value of `project/` and displaying it as a traditional folder.

For example, when you upload the object `project/doc/a.txt`, the delimiter `/` simulates the display mode of "folder", and you can see the folders "project" and "doc" on the console. The folder "doc" is displayed under the folder "project" and contains the file "a.txt".

Therefore, in a use case for file upload only, you can directly upload files without creating a folder first. If a folder is allowed in a use case, the feature of creating a folder should be supported. You can upload a 0 KB file whose path ends with '/'. When you call the API GetBucket, you can use the file as a folder.

**2) Multithreaded upload and download**

In XML C++ SDK, we encapsulate the multithreaded multipart upload and download operations as the APIs `MultiUploadObjectReq` and `MultiGetObjectReq`, and optimize the API design and transfer performance.

Main features:

- The size of each part can be set for multithreaded upload and download.
- The API `MultiUploadObjectReq` encapsulates all the APIs for multipart upload, including Init, Upload, Complete, and Abort.

The sample code of upload using `MultiUploadObjectReq`:

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
string bucket_name = "alangz-1253960400";
string object_name = "object_key";
string local_file = "/data/test";
qcloud_cos::MultiUploadObjectReq req(bucket_name,object_name, local_file);
req.SetRecvTimeoutInms(1000 * 60);
qcloud_cos::MultiUploadObjectResp resp;
qcloud_cos::CosResult result = cos.MultiUploadObject(req, &resp);
if (result.IsSucc()) {
    std::cout << "MultiUpload Succ." << std::endl;
    std::cout << resp.GetLocation() << std::endl;
    std::cout << resp.GetKey() << std::endl;
    std::cout << resp.GetBucket() << std::endl;
    std::cout << resp.GetEtag() << std::endl;
} else {
    std::cout << "MultiUpload Fail." << std::endl;
    // Determines the specific step where the failure occurs.
    std::string resp_tag = resp.GetRespTag();
    if ("Init" == resp_tag) {
        // print result
    } else if ("Upload" == resp_tag) {
        // print result
    } else if ("Complete" == resp_tag) {
        // print result
    }
}
```

The sample code of download using `MultiGetObjectReq`:

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
string bucket_name = "alangz-1253960400";
string object_name = "object_key";
string file_path = "/data/test";
qcloud_cos::MultiGetObjectReq req(bucket_name,object_name, file_path);
qcloud_cos::MultiGetObjectResp resp;
qcloud_cos::CosResult result = cos.GetObject(req, &resp);
```

**3) Signature algorithm**

Generally, you do not need to compute a signature manually. However, if you return an SDK signature to the frontend, note that the signature algorithm has changed. One-time signatures and multiple-time signatures are no longer used. Instead, you can set a validity period of the signature to ensure security. For more information, see [XML Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).

**4) New APIs**

The following APIs are added in XML C++ SDK, which can be called as needed:

- Bucket operations, such as PutBucketReq, GetBucketReq, etc.
- Operations on Bucket ACLs, such as PutBucketACLReq, GetBucketACLReq, etc.
- Operations on bucket lifecycle, such as PutBucketLifecycleReq, GetBucketLifecycleReq, etc.

For more information, see C++ SDK [API Documentation](https://intl.cloud.tencent.com/document/product/436/12301).

