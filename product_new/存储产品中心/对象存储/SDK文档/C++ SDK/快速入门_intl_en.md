## Download and Installation

### Relevant Resources
- The COS XML SDK for C++ source code can be downloaded [here](https://github.com/tencentyun/cos-cpp-sdk-v5).
- The sample demo can be download [here](https://github.com/tencentyun/cos-cpp-sdk-v5/blob/master/demo/cos_demo.cpp).

### Environmental Dependency
- Static dependency library: jsoncpp boost_system boost_thread Poco (under the lib folder).
- Dynamic dependency library: ssl crypto rt z (installation required).
The JsonCpp libraries and header files are available in the SDK. If you want to install them on your own, please follow the steps below to install the libraries and compile them first and then replace the corresponding libraries and header files in the SDK. If the libraries above are already installed on the system, you can also delete the corresponding libraries and header files in the SDK.

### Installing the SDK
#### 1. Install CMake
```shell
yum install -y gcc gcc-c++ make automake
// Install required packages such as gcc (if they have already been installed, skip this step)
yum install -y wget

// CMake version should be above 3.5
wget https://cmake.org/files/v3.5/cmake-3.5.2.tar.gz
tar -zxvf cmake-3.5.2.tar.gz
cd cmake-3.5.2
./bootstrap --prefix=/usr
gmake
gmake install
```

#### 2. Install Boost libraries and header files
```java
wget http://sourceforge.net/projects/boost/files/boost/1.54.0/boost_1_54_0.tar.gz
tar -xzvf boost_1_54_0.tar.gz
cd boost_1_54_0
./bootstrap.sh --prefix=/usr/local
./b2 install --with=all
# The Boost libraries are installed in the /usr/local/lib directory
```

#### 3. Install OpenSSL
**Method 1**
```shell
yum install openssl openssl-devel
```

**Method 2**

```shell
wget https://www.openssl.org/source/openssl-1.0.1t.tar.gz  
tar -xzvf ./openssl-1.0.1t.tar.gz
cd openssl-1.0.1t/
./config --prefix=/usr/local/ssl --openssldir=/usr/local/ssl

cd /usr/local/
ln -s ssl openssl
echo "/usr/local/openssl/lib" >> /etc/ld.so.conf
ldconfig

# Add header file/library file search paths (which can be written to ~/.bashrc)
LIBRARY_PATH=/usr/local/ssl/lib/:$LIBRARY_PATH
CPLUS_INCLUDE_PATH=/usr/local/ssl/include/:$CPLUS_INCLUDE_PATH
```

#### 4. Install Poco libraries and header files
Download the complete version of Poco libraries and header files from [Poco's official website](https://pocoproject.org/download.html) and install them.
```shell
./configure --omit=Data/ODBC,Data/MySQL
make
make install
```

> You can specify the local Boost header file path by modifying the following statement in the `CMakeList.txt` file: 
```
SET(BOOST_HEADER_DIR "/root/boost_1_61_0")
```

#### 5. Compile the COS SDK for C++ 
Download the [COS XML SDK for C++ source code](https://github.com/tencentyun/cos-cpp-sdk-v5), integrate it into your development environment, and run the following command:
```shell
cd ${cos-cpp-sdk} 
mkdir -p build 
cd build 
cmake .. 
make
```

> The [demo](https://github.com/tencentyun/cos-cpp-sdk-v5/blob/master/demo/cos_demo.cpp) contains examples of common APIs. The generated cos_demo can be executed directly; the generated static library is named libcossdk.a; the generated libcossdk.a should be placed in the lib directory of your project; and the generated include directory should be copied to the include path of your project.

## Getting Started
The section below describes how to perform basic operations in the COS SDK for C++, such as initializing a client, creating a bucket, querying bucket list, uploading an object, querying object list, downloading an object, and deleting an object.

> For more information on the meanings of parameters such as SecretId, SecretKey, and Bucket contained herein and how to get them, see [COS Glossary](https://intl.cloud.tencent.com/document/product/436/18507).

### Initialization
Descriptions of each field in the configuration file:
```
// Use "AccessKey" for configuration files in SDKs before v5.4.3
"SecretId":"COS_SECRETID", 
"SecretKey":"COS_SECRETKEY",

// COS region. For regions and their abbreviations, see https://intl.cloud.tencent.com/document/product/436/6224 
"Region":"Region",

// Signature timeout period in seconds    
"SignExpiredTime":360, 

// connect timeout period in milliseconds
"ConnectTimeoutInms":6000,

// http timeout period in milliseconds 
"HttpTimeoutInms":60000,  

// Part size in multipart upload; value range: 1 MB - 5 GB; default value: 1 MB  
"UploadPartSize":1048576,  

// Thread pool size in single-file multipart upload       
"UploadThreadPoolSize":5, 

// Part size in file download   
"DownloadSliceSize":4194304, 

// Thread pool size in single-file download 
"DownloadThreadPoolSize":5,   

// Thread pool size in async upload and download 
"AsynThreadPoolSize":2, 

// Log output type. 0: no output, 1: output to screen, 2: output to syslog   
"LogoutType":1,       

// Log level, 1: ERR, 2: WARN, 3: INFO, 4: DBG     
"LogLevel":3,                 
```

### Creating a Bucket

```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"

int main(int argc, char *argv[]) {
    // 1. Specify the configuration file path and initialize CosConfig
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. Construct the request to create a bucket
    std::string bucket_name = "examplebucket-1250000000"; // Bucket name
    qcloud_cos::PutBucketReq req(bucket_name);
    qcloud_cos::PutBucketResp resp;
    
    // 3. Call the API to create a bucket
    qcloud_cos::CosResult result = cos.PutBucket(req, &resp);
    
    // 4. Process the call result
    if (result.IsSucc()) {
        // Created successfully
    } else {
        // Failed to create the bucket. You can call the member function of CosResult to output the error information such as requestID
        std::cout << "ErrorInfo=" << result.GetErrorInfo() << std::endl;
        std::cout << "HttpStatus=" << result.GetHttpStatus() << std::endl;
        std::cout << "ErrorCode=" << result.GetErrorCode() << std::endl;
        std::cout << "ErrorMsg=" << result.GetErrorMsg() << std::endl;
        std::cout << "ResourceAddr=" << result.GetResourceAddr() << std::endl;
        std::cout << "XCosRequestId=" << result.GetXCosRequestId() << std::endl;
        std::cout << "XCosTraceId=" << result.GetXCosTraceId() << std::endl;
    }
}
```

### Querying Bucket List
```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"

int main(int argc, char *argv[]) {
    // 1. Specify the configuration file path and initialize CosConfig
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. Construct the request to upload a file
    qcloud_cos::GetServiceReq req;
    qcloud_cos::GetServiceResp resp;
    qcloud_cos::CosResult result = cos.GetService(req, &resp);
    
    // 3. Get the response information
    const qcloud_cos::Owner& owner = resp.GetOwner();
    const std::vector<qcloud_cos::Bucket>& buckets = resp.GetBuckets();
    std::cout << "owner.m_id=" << owner.m_id << ", owner.display_name=" << owner.m_display_name << std::endl;
    
    for (std::vector<qcloud_cos::Bucket>::const_iterator itr = buckets.begin(); itr != buckets.end(); ++itr) {
        const qcloud_cos::Bucket& bucket = *itr;
        std::cout << "Bucket name=" << bucket.m_name << ", location="
            << bucket.m_location << ", create_date=" << bucket.m_create_date << std::endl;
    }
    
    // 4. Process the call result
    if (result.IsSucc()) {
        // File successfully uploaded
    } else {
        // Failed to upload the file. You can call the member function of CosResult to output the error information such as requestID
        std::cout << "ErrorInfo=" << result.GetErrorInfo() << std::endl;
        std::cout << "HttpStatus=" << result.GetHttpStatus() << std::endl;
        std::cout << "ErrorCode=" << result.GetErrorCode() << std::endl;
        std::cout << "ErrorMsg=" << result.GetErrorMsg() << std::endl;
        std::cout << "ResourceAddr=" << result.GetResourceAddr() << std::endl;
        std::cout << "XCosRequestId=" << result.GetXCosRequestId() << std::endl;
        std::cout << "XCosTraceId=" << result.GetXCosTraceId() << std::endl;
    }
}
```

### Uploading an Object
```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"

int main(int argc, char *argv[]) {
    // 1. Specify the configuration file path and initialize CosConfig
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. Construct the request to upload a file
    std::string bucket_name = "examplebucket-1250000000"; // Destination bucket name
    std::string object_name = "exampleobject"; // exampleobject is the object key (Key) which is a unique ID of an object in the bucket. For example, in the object's access domain name examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg, the object key is doc/pic.jpg
    // The constructor of request requires the local file path to be passed in
    qcloud_cos::PutObjectByFileReq req(bucket_name, object_name, "/path/to/local/file");
    req.SetXCosStorageClass("STANDARD_IA"); // Call the Set method to set metadata
    qcloud_cos::PutObjectByFileResp resp;
    
    // 3. Call the API to upload the file
    qcloud_cos::CosResult result = cos.PutObject(req, &resp);
    
    // 4. Process the call result
    if (result.IsSucc()) {
        // File successfully uploaded
    } else {
        // Failed to upload the file. You can call the member function of CosResult to output the error information such as requestID
        std::cout << "ErrorInfo=" << result.GetErrorInfo() << std::endl;
        std::cout << "HttpStatus=" << result.GetHttpStatus() << std::endl;
        std::cout << "ErrorCode=" << result.GetErrorCode() << std::endl;
        std::cout << "ErrorMsg=" << result.GetErrorMsg() << std::endl;
        std::cout << "ResourceAddr=" << result.GetResourceAddr() << std::endl;
        std::cout << "XCosRequestId=" << result.GetXCosRequestId() << std::endl;
        std::cout << "XCosTraceId=" << result.GetXCosTraceId() << std::endl;
    }
}
```

### Querying Object List
```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"

int main(int argc, char *argv[]) {
    // 1. Specify the configuration file path and initialize CosConfig
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. Construct the request to create a bucket
    std::string bucket_name = "examplebucket-1250000000"; // Destination bucket name
    qcloud_cos::GetBucketReq req(bucket_name);
    qcloud_cos::GetBucketResp resp;
    qcloud_cos::CosResult result = cos.GetBucket(req, &resp);   
    
    std::vector<qcloud_cos::Content> cotents = resp.GetContents();
    for (std::vector<qcloud_cos::Content>::const_iterator itr = cotents.begin(); itr != cotents.end(); ++itr) {
    	const qcloud_cos::Content& content = *itr;
        std::cout << "key name=" << content.m_key << ", lastmodified ="
            << content.m_last_modified << ", size=" << content.m_size << std::endl;
    }
    
    // 3. Process the call result
    if (result.IsSucc()) {
        // File successfully uploaded
    } else {
        // Failed to upload the file. You can call the member function of CosResult to output the error information such as requestID
        std::cout << "ErrorInfo=" << result.GetErrorInfo() << std::endl;
        std::cout << "HttpStatus=" << result.GetHttpStatus() << std::endl;
        std::cout << "ErrorCode=" << result.GetErrorCode() << std::endl;
        std::cout << "ErrorMsg=" << result.GetErrorMsg() << std::endl;
        std::cout << "ResourceAddr=" << result.GetResourceAddr() << std::endl;
        std::cout << "XCosRequestId=" << result.GetXCosRequestId() << std::endl;
        std::cout << "XCosTraceId=" << result.GetXCosTraceId() << std::endl;
    }
}
```

### Downloading an Object
```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"

int main(int argc, char *argv[]) {
    // 1. Specify the configuration file path and initialize CosConfig
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. Construct the request to create a bucket
    std::string bucket_name = "examplebucket-1250000000"; // Destination bucket name
    std::string object_name = "exampleobject"; // exampleobject is the object key (Key) which is a unique ID of an object in the bucket. For example, in the object's access domain name examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg, the object key is doc/pic.jpg
    std::string local_path = "/tmp/exampleobject";
    // request needs to carry the appid, bucketname, object, and local path (including filename)
    qcloud_cos::GetObjectByFileReq req(bucket_name, object_name, local_path);
    qcloud_cos::GetObjectByFileResp resp;
    
    // 3. Call the API to create a bucket
    qcloud_cos::CosResult result = cos.GetObject(req, &resp);
    
    // 4. Process the call result
    if (result.IsSucc()) {
        // File successfully downloaded
    } else {
        // Failed to download the file. You can call the member function of CosResult to output the error information such as requestID
        std::cout << "ErrorInfo=" << result.GetErrorInfo() << std::endl;
        std::cout << "HttpStatus=" << result.GetHttpStatus() << std::endl;
        std::cout << "ErrorCode=" << result.GetErrorCode() << std::endl;
        std::cout << "ErrorMsg=" << result.GetErrorMsg() << std::endl;
        std::cout << "ResourceAddr=" << result.GetResourceAddr() << std::endl;
        std::cout << "XCosRequestId=" << result.GetXCosRequestId() << std::endl;
        std::cout << "XCosTraceId=" << result.GetXCosTraceId() << std::endl;
    }
}
```

### Deleting an Object
```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"

int main(int argc, char *argv[]) {
    // 1. Specify the configuration file path and initialize CosConfig
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. Construct the request to create a bucket
    std::string bucket_name = "examplebucket-1250000000"; // Destination bucket name
    std::string object_name = "exampleobject"; // exampleobject is the object key (Key) which is a unique ID of an object in the bucket. For example, in the object's access domain name examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg, the object key is doc/pic.jpg
    // 3. Call the API to create a bucket
	qcloud_cos::DeleteObjectReq req(bucket_name, object_name);
	qcloud_cos::DeleteObjectResp resp;
	qcloud_cos::CosResult result = cos.DeleteObject(req, &resp); 
    
    // 4. Process the call result
    if (result.IsSucc()) {
        // File successfully downloaded
    } else {
        // Failed to download the file. You can call the member function of CosResult to output the error information such as requestID
        std::cout << "ErrorInfo=" << result.GetErrorInfo() << std::endl;
        std::cout << "HttpStatus=" << result.GetHttpStatus() << std::endl;
        std::cout << "ErrorCode=" << result.GetErrorCode() << std::endl;
        std::cout << "ErrorMsg=" << result.GetErrorMsg() << std::endl;
        std::cout << "ResourceAddr=" << result.GetResourceAddr() << std::endl;
        std::cout << "XCosRequestId=" << result.GetXCosRequestId() << std::endl;
        std::cout << "XCosTraceId=" << result.GetXCosTraceId() << std::endl;
    }
}
```
