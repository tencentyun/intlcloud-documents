## Download and Installation

#### Relevant resources

- Download COS XML C++ SDK source code below:
Linux/Windows/macOS: [ XML Linux C++ SDK](https://github.com/tencentyun/cos-cpp-sdk-v5)
- Download [XML C++ SDK](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-cpp-sdk-v5/latest/cos-cpp-sdk-v5.zip). 
- Download the demo [here](https://github.com/tencentyun/cos-cpp-sdk-v5/blob/master/demo/cos_demo.cpp)
- For the SDK changelog, see [Changelog](https://github.com/tencentyun/cos-cpp-sdk-v5/blob/master/CHANGELOG.md).

>? If you encounter errors such as non-existent functions or methods when using the XML version of the SDK, please update the SDK to the latest version and try again.
>


## Pre-Compiled (Recommended)

Download the [XML C++ SDK source code](https://github.com/tencentyun/cos-cpp-sdk-v5). In the `libs` directory, you can find the ready-to-use pre-compiled libraries. Please choose one that suits your system version.

```shell
libs/linux/libcossdk.a # Linux static library. `libcossdk.a` is compiled based on GCC v4.8.5. If your compilation environment uses a different GCC version, you need to compile `libcossdk.a` again.
libs/linux/libcossdk-shared.so # Linux dynamic library
libs/Win32/cossdk.lib # Win32 library
libs/x64/cossdk.lib # Win64 library
libs/macOS/libcossdk.a # macOS static library
libs/macOS/libcossdk-shared.dylib # macOS dynamic library
```

>? Copy the libraries and the SDK include files that suit your OS to your project.

The following third-party dependent libraries can be found in the `Third-party` directory:

```shell
third_party/lib/linux/poco/ # Linux-dependent POCO dynamic library. The POCO library is compiled based on OpenSSL v1.0.2. If your compilation environment uses a different OpenSSL version, you need to compile the POCO library again.
third_party/lib/Win32/openssl/ # Win32-dependent OpenSSL library
third_party/lib/Win32/poco/ # Win32-dependent POCO library
third_party/lib/x64/openssl/ # Win64-dependent OpenSSL library
third_party/lib/x64/poco/ # Win64-dependent POCO library
third_party/lib/macOS/poco/ # macOS-dependent POCO library
```

>? Copy the dependent libraries that suit your OS to your project.


## Manual Compilation


### Compilation options

You can configure the following compilation options using the `CMakeLists.txt` file in the root directory:

```shell
option(BUILD_UNITTEST "Build unittest" OFF) # Configure unit testing compilation.
option(BUILD_DEMO "Build demo" ON) # Configure demo testable code compilation.
option(BUILD_SHARED_LIB "Build shared library" OFF) # Configure dynamic library compilation.
```

### Dependent libraries

Shared libraries: POCO, OpenSSL, Crypto


### Compiling Linux SDK

1. Install the compiler and dependent libraries.
```shell
yum install -y gcc gcc-c++ make cmake openssl
# The CMake version should be later than 2.8.
```
2. Compile the SDK. 
Download the [XML C++ SDK source code](https://github.com/tencentyun/cos-cpp-sdk-v5) to your development environment and run the following command:
```shell
cd ${cos-cpp-sdk} 
mkdir -p build 
cd build 
cmake .. 
make
```
3. Install the POCO libraries.
```shell
cd ${cos-cpp-sdk} 
sh install-libpoco.sh
```
>? This script installs the POCO dynamic library to the `/usr/lib64` directory and creates a soft link. To use a COS SDK in the production environment, install the POCO library to the production environment as well.
>
4. Run the demo. 
>?You can skip this step if you don’t need to test the demo.
>
```shell
cd ${cos-cpp-sdk} 
vim demo/cos_demo.cpp  # Modify the bucket name and testable code in the demo.
vim CMakeLists.txt # Set "BUILD_DEMO" to "ON" in "CMakeLists.txt" in the root directory to start compiling the demo.
cd build && make # Compile the demo.
ls bin/cos_demo # The generated executable file is in the "bin" directory.
vim bin/config.json # Modify the key and the region.
cd bin && ./cos_demo # Run the demo.
```
5. Use the SDK. 
The compiled libraries can be found in the `build/lib` directory. The static library name is `libcossdk.a` and the dynamic library name is `libcossdk-shared.so`. During actual use, copy the libraries to your project and copy the `include` directory to the `include` directory of your project.


### Compiling Windows SDK

1. Install Visual Studio 2017.
Install the Visual Studio 2017 development environment.
2. Install CMake.
Download the Windows version of the CMake compiler from the [CMake official website](https://cmake.org/download/), and configure `${CMake installation path}\bin` in the `Path` environment variable.
3. Compile the SDK. 
 i. Download [XML Windows C++ SDK source code](https://github.com/tencentyun/cos-cpp-sdk-v5) to your development environment.
    ii. Open the Windows command-line tool, cd to the directory of the C++ SDK source code, and run the following command:
```shell
mkdir build
cd build
cmake .. # Generate the Win32 Makefile.
cmake -G "Visual Studio 15 Win64" .. # Generate the Win64 Makefile.
```
 iii. Use Visual Studio 2017 to open the Solution Explorer and perform compilation.
4. Test the demo. <br>
>?You can skip this step if you don’t need to test the demo.
>
Modify the demo code and compile it. The generated `cos_demo.exe` file is in the `bin` directory. You can modify `bin/config.json` to run `cos_demo.exe`.
5. Use the SDK. 
The compiled libraries can be found in the `build/Release` directory. The static library is named `cossdk.lib`. During actual use, copy the library to your project and copy the `include` directory to the `include` directory of your project.

### Compiling Mac SDK

1. Install the compiler and dependent libraries.
```shell
brew install gcc make cmake openssl
```
2. Compile the SDK. 
Download the [XML C++ SDK source code](https://github.com/tencentyun/cos-cpp-sdk-v5) to your development environment and run the following command:
```shell
cd ${cos-cpp-sdk} 
mkdir -p build 
cd build 
cmake .. 
make
```
3. Install the POCO libraries.
The POCO libraries are in the `third_party/lib/macOS/poco` directory. You can install them by yourself.
4. Run the demo. 
>?You can skip this step if you don’t need to test the demo.
>
Modify the demo code and compile it. The generated `cos_demo` is in the `bin` directory. Copy `cos-cpp-sdk-v5/demo/config.json` to the `bin` directory and modify `bin/config.json`. Then you can run `cos_demo`.
5. Use the SDK. 
The compiled libraries can be found in the `build/lib` directory. The static library is named `libcossdk.a`, and the dynamic library is named `libcossdk-shared.dylib`. During actual use, copy the libraries to your project and copy the `include` directory to the `include` directory of your project.

>? If you encounter compilation problems, please refer to [C++ SDK FAQ](https://www.tencentcloud.com/document/product/436/54482).

## Getting Started

The section below describes how to use the COS C++ SDK to perform basic operations, such as initializing a client, creating a bucket, querying a bucket list, uploading an object, querying an object list, downloading an object, and deleting an object.

>? For the definition of terms such as SecretId, SecretKey, and Bucket, see [COS Glossary](https://intl.cloud.tencent.com/document/product/436/7751).
>

### Initialization

>!
>- We recommend you use a sub-account key and environment variables to call the SDK for security purposes. When authorizing a sub-account, follow the [Notes on Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to avoid leaking resources besides your buckets and objects.
>- If you must use a permanent key, we recommend you follow the [Notes on Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to limit the scope of permission on the permanent key.

### Accessing COS using a temporary key

To access COS using a temporary key, see the code below:

```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"
int main(int argc, char *argv[]) {
    // Using the configuration file for initialization is not recommended because secret_id and secret_key of a temporary key will change.
    qcloud_cos::CosConfig config(appid, "secret_id", "secret_key", "region");
    // secret_id and secret_key of a temporary key are required. For details on how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048.
    config.SetTmpToken("xxx");
    qcloud_cos::CosAPI cos(config);
}
```

### Accessing COS using a permanent key (not recommended)

To access COS using a permanent key, see the code below:

```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"
int main(int argc, char *argv[]) {
    qcloud_cos::CosConfig config("./config.json");  // Use the configuration file for initialization
    // Or use constructor parameters for initialization directly
    //qcloud_cos::CosConfig config(appid, "secret_id", "secret_key", "region");  // Permanent key
    qcloud_cos::CosAPI cos(config);
}
```

Fields in the configuration file are described as follows:

```
{
"SecretId":"********************************", // Replace `sercret_id` with your `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
"SecretKey":"*******************************", // Replace `sercret_key` with your `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
"Region":"ap-guangzhou",                // Bucket region. Replace it with your bucket region, which can be viewed on the overview page in the COS console at https://console.cloud.tencent.com/cos5/bucket/. For more information about regions, visit https://cloud.tencent.com/document/product/436/6224.
"SignExpiredTime":360,              // Signature expiration time, in seconds
"ConnectTimeoutInms":6000,          // Connection timeout, in milliseconds
"ReceiveTimeoutInms":60000,         // Receive timeout, in milliseconds
"UploadPartSize":10485760,          // Size of the part to upload, which can be 1 MB to 5 GB. Defaults to 10 MB.
"UploadCopyPartSize":20971520,      // Size of the copied part for upload, which can be 5 MB to 5 GB. Defaults to 20 MB.
"UploadThreadPoolSize":5,           // Size of the upload thread pool for a single multipart upload
"DownloadSliceSize":4194304,        // Size of a part to download
"DownloadThreadPoolSize":5,         // Size of the download thread pool for a single file
"AsynThreadPoolSize":2,             // Async thread pool size for uploads/downloads
"LogoutType":1,                     // Log output type. Valid values: 0 (no output), 1 (output to screen), 2 (output to syslog)
"LogLevel":3,                       // Log level. Valid values: 1 (ERR), 2 (WARN), 3 (INFO), 4 (DBG)
"IsDomainSameToHost":false,         // Whether there is a dedicated host
"DestDomain":"",                    // Dedicated host
"IsUseIntranet":false,              // Whether a specific IP and port number are used
"IntranetAddr":""                   // IP and port number, such as "127.0.0.1:80"
}
```

### Printing SDK internal logs to a custom log file

To print SDK internal logs (especially for Windows OS) to a custom log file, see the code below:

```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"
void TestLogCallback(const std::string& log) {
    std::ofstream ofs;
    ofs.open("test.log", std::ios_base::app);
    ofs << log;
    ofs.close();
}
int main(int argc, char** argv) {
    qcloud_cos::CosConfig config("./config.json");
    config.SetLogCallback(&TestLogCallback);
    qcloud_cos::CosAPI cos(config);
}
```

### Creating a bucket

```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"

int main(int argc, char *argv[]) {
    // 1. Specify the path to the configuration file and initialize CosConfig
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. Construct the PUT Bucket request
    std::string bucket_name = "examplebucket-1250000000"; // Replace it with your bucket name, which is in the format of BucketName-APPID (APPID is required). It can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    qcloud_cos::PutBucketReq req(bucket_name);
    qcloud_cos::PutBucketResp resp;
    
    // 3. Call the PUT Bucket API
    qcloud_cos::CosResult result = cos.PutBucket(req, &resp);
    
    // 4. Process the call result
    if (result.IsSucc()) {
        // Group created successfully
    } else {
        // Failed to create the bucket. You can call the CosResult member functions to output the error information such as the requestID.
        std::cout << "HttpStatus=" << result.GetHttpStatus() << std::endl;
        std::cout << "ErrorCode=" << result.GetErrorCode() << std::endl;
        std::cout << "ErrorMsg=" << result.GetErrorMsg() << std::endl;
        std::cout << "ResourceAddr=" << result.GetResourceAddr() << std::endl;
        std::cout << "XCosRequestId=" << result.GetXCosRequestId() << std::endl;
        std::cout << "XCosTraceId=" << result.GetXCosTraceId() << std::endl;
    }
}

```

### Querying the bucket list

```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"

int main(int argc, char *argv[]) {
    // 1. Specify the path to the configuration file and initialize CosConfig
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. Construct a request to query the bucket list
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
        // Queried the bucket list successfully
    } else {
        // Failed to query the bucket list. You can call the CosResult member functions to output the error information such as requestID.
        std::cout << "HttpStatus=" << result.GetHttpStatus() << std::endl;
        std::cout << "ErrorCode=" << result.GetErrorCode() << std::endl;
        std::cout << "ErrorMsg=" << result.GetErrorMsg() << std::endl;
        std::cout << "ResourceAddr=" << result.GetResourceAddr() << std::endl;
        std::cout << "XCosRequestId=" << result.GetXCosRequestId() << std::endl;
        std::cout << "XCosTraceId=" << result.GetXCosTraceId() << std::endl;
    }
}
```

### Uploading an object

```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"

int main(int argc, char *argv[]) {
    // 1. Specify the path to the configuration file and initialize CosConfig
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. Construct a request to upload a file
    std::string bucket_name = "examplebucket-1250000000"; // Replace it with your bucket name, which is in the format of BucketName-APPID (APPID is required). It can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    std::string object_name = "exampleobject"; // `exampleobject` is the ObjectKey (Key), the unique ID of an object in a bucket. For example, if the object's access domain name is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is `doc/pic.jpg`. Replace it with your object name.
    qcloud_cos::PutObjectByFileReq req(bucket_name, object_name, "/path/to/local/file"); // Replace the value with your file path.
    //req.SetXCosStorageClass("STANDARD_IA"); // `STANDARD_IA` is the default value. You can call the `Set` method to set the storage class.
    qcloud_cos::PutObjectByFileResp resp;
    
    // 3. Call the PUT Object API
    qcloud_cos::CosResult result = cos.PutObject(req, &resp);
    
    // 4. Process the call result
    if (result.IsSucc()) {
        // File uploaded successfully
    } else {
        // Failed to upload the file. You can call the `CosResult` member functions to output the error information such as the requestID.
        std::cout << "HttpStatus=" << result.GetHttpStatus() << std::endl;
        std::cout << "ErrorCode=" << result.GetErrorCode() << std::endl;
        std::cout << "ErrorMsg=" << result.GetErrorMsg() << std::endl;
        std::cout << "ResourceAddr=" << result.GetResourceAddr() << std::endl;
        std::cout << "XCosRequestId=" << result.GetXCosRequestId() << std::endl;
        std::cout << "XCosTraceId=" << result.GetXCosTraceId() << std::endl;
    }
}
```

### Querying objects

```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"

int main(int argc, char *argv[]) {
    // 1. Specify the path to the configuration file and initialize CosConfig
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. Construct a request to query the object list
    std::string bucket_name = "examplebucket-1250000000"; // Replace it with your bucket name, which is in the format of BucketName-APPID (APPID is required). It can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
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
        // Queried the object list successfully
    } else {
        // Failed to query the object list. You can call the CosResult member functions to output the error information such as requestID.
        std::cout << "HttpStatus=" << result.GetHttpStatus() << std::endl;
        std::cout << "ErrorCode=" << result.GetErrorCode() << std::endl;
        std::cout << "ErrorMsg=" << result.GetErrorMsg() << std::endl;
        std::cout << "ResourceAddr=" << result.GetResourceAddr() << std::endl;
        std::cout << "XCosRequestId=" << result.GetXCosRequestId() << std::endl;
        std::cout << "XCosTraceId=" << result.GetXCosTraceId() << std::endl;
    }
}
```

### Downloading an object

```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"

int main(int argc, char *argv[]) {
    // 1. Specify the path to the configuration file and initialize CosConfig
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. Construct a request to download the object
    std::string bucket_name = "examplebucket-1250000000"; // Replace it with your bucket name, which is in the format of BucketName-APPID (APPID is required). It can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    std::string object_name = "exampleobject"; // `exampleobject` is the ObjectKey (Key), the unique ID of an object in a bucket. For example, if the object's access domain name is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is `doc/pic.jpg`. Replace it with your object name.
    std::string local_path = "/tmp/exampleobject";
    // appid, bucketname, object, and a local path (including filename) are required for the request.
    qcloud_cos::GetObjectByFileReq req(bucket_name, object_name, local_path);
    qcloud_cos::GetObjectByFileResp resp;
    
    // 3. Call the object download API
    qcloud_cos::CosResult result = cos.GetObject(req, &resp);
    
    // 4. Process the call result
    if (result.IsSucc()) {
        // File downloaded successfully
    } else {
        // Failed to download the file. You can call the CosResult member functions to output the error information such as the requestID.
        std::cout << "HttpStatus=" << result.GetHttpStatus() << std::endl;
        std::cout << "ErrorCode=" << result.GetErrorCode() << std::endl;
        std::cout << "ErrorMsg=" << result.GetErrorMsg() << std::endl;
        std::cout << "ResourceAddr=" << result.GetResourceAddr() << std::endl;
        std::cout << "XCosRequestId=" << result.GetXCosRequestId() << std::endl;
        std::cout << "XCosTraceId=" << result.GetXCosTraceId() << std::endl;
    }
}
```

### Deleting an object

```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"

int main(int argc, char *argv[]) {
    // 1. Specify the path to the configuration file and initialize CosConfig
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. Construct a request to delete the object
    std::string bucket_name = "examplebucket-1250000000"; // Replace it with your bucket name, which is in the format of BucketName-APPID (APPID is required). It can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    std::string object_name = "exampleobject"; // `exampleobject` is the ObjectKey (Key), the unique ID of an object in a bucket. For example, if the object's access domain name is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is `doc/pic.jpg`. Replace it with your object name.
    // 3. Call the object deleting API
	qcloud_cos::DeleteObjectReq req(bucket_name, object_name);
	qcloud_cos::DeleteObjectResp resp;
	qcloud_cos::CosResult result = cos.DeleteObject(req, &resp); 
    
    // 4. Process the call result
    if (result.IsSucc()) {
        // Deleted the object successfully
    } else {
        // Failed to delete the object. You can call the CosResult member functions to output the error information such as requestID.
        std::cout << "HttpStatus=" << result.GetHttpStatus() << std::endl;
        std::cout << "ErrorCode=" << result.GetErrorCode() << std::endl;
        std::cout << "ErrorMsg=" << result.GetErrorMsg() << std::endl;
        std::cout << "ResourceAddr=" << result.GetResourceAddr() << std::endl;
        std::cout << "XCosRequestId=" << result.GetXCosRequestId() << std::endl;
        std::cout << "XCosTraceId=" << result.GetXCosTraceId() << std::endl;
    }
}
```
