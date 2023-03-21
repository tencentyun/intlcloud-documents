## Download and Installation

#### Related resources

- Download the COS XML C++ SDK source code below:
Linux/Windows/macOS: [XML Linux C++ SDK](https://github.com/tencentyun/cos-cpp-sdk-v5)
- Download the [XML C++ SDK](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-cpp-sdk-v5/latest/cos-cpp-sdk-v5.zip). 
- Download the demo [here](https://github.com/tencentyun/cos-cpp-sdk-v5/blob/master/demo/cos_demo.cpp).
- For the SDK changelog, see [Changelog](https://github.com/tencentyun/cos-cpp-sdk-v5/blob/master/CHANGELOG.md).

>? If you encounter errors such as non-existent functions or methods when using the XML version of the SDK, update the SDK to the latest version and try again.
>


## Precompilation (Recommended)

Download the [XML C++ SDK source code](https://github.com/tencentyun/cos-cpp-sdk-v5). In the `libs` directory, you can find the ready-to-use precompiled libraries. Choose the one that suits your system version.

```shell
libs/linux/libcossdk.a # Linux static library. `libcossdk.a` is compiled based on GCC v4.8.5. If your compilation environment uses a different GCC version, you need to compile `libcossdk.a` again.
libs/linux/libcossdk-shared.so # Linux dynamic library
libs/Win32/cossdk.lib # Windows 32-bit library
libs/x64/cossdk.lib # Windows 64-bit library
libs/macOS/libcossdk.a # macOS static library
libs/macOS/libcossdk-shared.dylib # macOS dynamic library
```

>? Copy the libraries and SDK `include` files for your OS to your project.

The following third-party dependent libraries can be found in the `Third-party` directory:

```shell
third_party/lib/linux/poco/ # Linux-dependent POCO dynamic library. The POCO library is compiled based on OpenSSL v1.0.2. If your compilation environment uses a different OpenSSL version, you need to compile the POCO library again.
third_party/lib/Win32/openssl/ # Windows 32-bit-dependent OpenSSL library
third_party/lib/Win32/poco/ # Windows 32-bit-dependent POCO library
third_party/lib/x64/openssl/ # Windows 64-bit-dependent OpenSSL library
third_party/lib/x64/poco/ # Windows 64-bit-dependent POCO library
third_party/lib/macOS/poco/ # macOS-dependent POCO library
```

>? Copy the dependent libraries for your OS to your project.


## Manual Compilation


### Compilation options

You can configure the following compilation options by using the `CMakeLists.txt` file in the root directory:

```shell
option(BUILD_UNITTEST "Build unittest" OFF) # Configure unit testing compilation
option(BUILD_DEMO "Build demo" ON) # Configure demo testing code compilation
option(BUILD_SHARED_LIB "Build shared library" OFF) # Configure dynamic library compilation
```

### Dependent libraries

Dynamic libraries: POCO, OpenSSL, and Crypto.


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
3. Install the POCO library.
```shell
cd ${cos-cpp-sdk} 
sh install-libpoco.sh
```
>? This script installs the POCO dynamic library to the `/usr/lib64` directory and creates a soft link. To use a COS SDK in the production environment, install the POCO library to the production environment as well.
>
4. Run the demo. 
>?You can skip this step if you don't need to test the demo.
>
```shell
cd ${cos-cpp-sdk} 
vim demo/cos_demo.cpp  # Modify the bucket name and testing code in the demo
vim CMakeLists.txt # Set `BUILD_DEMO` to `ON` in `CMakeLists.txt` to start compiling the demo
cd build && make # Compile the demo
ls bin/cos_demo # The generated executable file is in the `bin` directory
vim bin/config.json # Modify the key and region
cd bin && ./cos_demo # Run the demo
```
5. Use the SDK. 
The compiled libraries can be found in the `build/lib` directory. The static library name is `libcossdk.a`, and the dynamic library name is `libcossdk-shared.so`. During actual use, copy the `include` directory to the `include` path of your project.


### Compiling Windows SDK

1. Install Visual Studio 2017.
Install the Visual Studio 2017 development environment.
2. Install CMake.
Download the CMake for Windows compiler from [CMake official website](https://cmake.org/download/), and then configure `${CMake installation path}\bin` in the `Path` environment variable.
3. Compile the SDK. 
 i. Download the [XML Windows C++ SDK source code](https://github.com/tencentyun/cos-cpp-sdk-v5/tree/windows_dev) to your development environment.
 ii. Open the Windows command-line tool, run `cd` to the directory of the C++ SDK source code, and run the following command:
```shell
mkdir build
cd build
cmake .. # Generate the Windows 32-bit Makefile
cmake -G "Visual Studio 15 Win64" .. # Generate the Windows 64-bit Makefile
```
 iii. Use Visual Studio 2017 to open the Solution Explorer and perform compilation.
4. Run the demo.
>?You can skip this step if you don't need to test the demo.
>
Modify the demo code and compile it. The generated `cos_demo.exe` file is in the `bin` directory. You can modify `bin/config.json` to run `cos_demo.exe`.
5. Use the SDK. 
The compiled libraries can be found in the `build/Release` directory. The static library name is `cossdk.lib`. During actual use, copy the `include` directory to the `include` path of your project.

### Compiling macOS SDK

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
3. Install the POCO library.
The POCO library is in the `third_party/lib/macOS/poco` directory. You can install it by yourself.
4. Run the demo. 
>?You can skip this step if you don't need to test the demo.
>
Modify the demo code and compile it. The generated `cos_demo` is in the `bin` directory. Copy `cos-cpp-sdk-v5/demo/config.json` to the `bin` directory and modify `bin/config.json`. Then, you can run `cos_demo`.
5. Use the SDK. 
The compiled libraries can be found in the `build/lib` directory. The static library name is `libcossdk.a`, and the dynamic library name is `libcossdk-shared.dylib`. During actual use, copy the `include` directory to the `include` path of your project.

### Common compilation errors

1. The following error information is displayed when the executable program is compiled:
```shell
   PocoCrypto.so.64: undefined reference to `PEM_write_bio_PrivateKey@libcrypto.so.10'
   libPocoNetSSL.so.64: undefined reference to `X509_check_host@libcrypto.so.10'
   ibPocoCrypto.so.64: undefined reference to `ECDSA_sign@OPENSSL_1.0.1_EC'
   libPocoCrypto.so.64: undefined reference to `CRYPTO_set_id_callback@libcrypto.so.10'
   ibPocoCrypto.so.64: undefined reference to `EVP_PKEY_id@libcrypto.so.10'
   libPocoNetSSL.so.64: undefined reference to `SSL_get1_session@libssl.so.10'
   libPocoNetSSL.so.64: undefined reference to `SSL_get_shutdown@libssl.so.10'
   libPocoCrypto.so.64: undefined reference to `EVP_PKEY_set1_RSA@libcrypto.so.10'
libPocoCrypto.so.64: undefined reference to `SSL_load_error_strings@libssl.so.10'
```
This is usually caused by the inconsistency between the project's built-in SSL version on which the POCO library compilation depends and the SSL version on your device. You need to compile the POCO library again and replace the POCO library in `third_party`.
```shell
wget https://github.com/pocoproject/poco/archive/refs/tags/poco-1.9.4-release.zip
cd poco-poco-1.9.4-release/
./configure --omit=Data/ODBC,Data/MySQL
mkdir my_build
cd my_build
cmake .. 
make -j5
```
2. The PocoNetSSL library failed to be compiled during POCO library compilation. This is usually because the `openssl-devel` library is not installed.
```shell
yum install -y openssl-devel
```
3. The following error information is displayed when the executable program is compiled:
```shell
undefined reference to `qcloud_cos::CosConfig::CosConfig(std::__cxx11::basic_string<char, std::char_traits<char>, std::allocator<char> > const&)
```
This is usually caused by the inconsistency between the project's built-in GCC version used by the `libcossdk.a` compilation and the GCC version on your device. You need to compile the POCO library and `libcossdk.a` again.

## Getting Started

The section below describes how to use the COS C++ SDK to perform basic operations, such as initializing a client, creating a bucket, querying a bucket list, uploading an object, querying an object list, downloading an object, or deleting an object.

>? For the definitions of terms such as `SecretId`, `SecretKey`, and bucket, see [Introduction](https://intl.cloud.tencent.com/document/product/436/7751).
>

### Initialization

>!
>- We recommend you use a sub-account key and environment variables to call the SDK for security purposes. When authorizing a sub-account, follow the [Notes on Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to avoid leaking resources besides your buckets and objects.
>- If you must use a permanent key, we recommend you follow the [Notes on Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to limit the scope of permission on the permanent key.

Fields in the configuration file are as described below:

``` bash
{
"SecretId":"********************************", // Replace the value with your `SecretId`, which can be viewed at https://console.cloud.tencent.com/cam/capi.
"SecretKey":"*******************************", // Replace the value with your `SecretKey`, which can be viewed at https://console.cloud.tencent.com/cam/capi.
"Region":"ap-guangzhou",                // Bucket region. Replace it with your bucket region, which can be viewed on the overview page in the COS console at https://console.cloud.tencent.com/cos5/bucket/. For more information on regions, visit https://intl.cloud.tencent.com/document/product/436/6224.
"SignExpiredTime":360,              // Signature expiration time in seconds
"ConnectTimeoutInms":6000,          // Connection timeout period in milliseconds
"ReceiveTimeoutInms":60000,         // `Receive` timeout period in milliseconds
"UploadPartSize":10485760,          // Size of the part to be uploaded, which can be 1 MB to 5 GB. Default value: 10 MB.
"UploadCopyPartSize":20971520,      // Size of the copied part for upload, which can be 5 MB to 5 GB. Default value: 20 MB.
"UploadThreadPoolSize":5,           // Size of the upload thread pool for a single multipart upload
"DownloadSliceSize":4194304,        // Size of the part to be downloaded
"DownloadThreadPoolSize":5,         // Size of the download thread pool for a single file
"AsynThreadPoolSize":2,             // Size of the async thread pool for uploads/downloads
"LogoutType":1,                     // Log output type. Valid values: 0 (no output), 1 (output to screen), 2 (output to syslog).
"LogLevel":3,                       // Log level. Valid values: 1 (ERR), 2 (WARN), 3 (INFO), 4 (DBG).
"IsDomainSameToHost":false,         // Whether to use a specific host
"DestDomain":"",                    // Specific host
"IsUseIntranet":false,              // Whether to use a specific IP and port number
"IntranetAddr":""                   // Specific IP and port number, such as `127.0.0.1:80`
}
```

### Accessing COS with temporary key

To access COS with a temporary key, see the code below:

```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"
int main(int argc, char *argv[]) {
    qcloud_cos::CosConfig config("./config.json");
    // Token is required for temporary keys but not permanent keys. For more information on how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
    config.SetTmpToken("xxx");
    qcloud_cos::CosAPI cos(config);
}
```

### Printing SDK internal logs to custom log file

To print SDK internal logs (especially for Windows) to a custom log file, see the code below:

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

### Creating bucket

```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"

int main(int argc, char *argv[]) {
    // 1. Specify the path of the configuration file and initialize CosConfig
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. Construct a request to create a bucket
    std::string bucket_name = "examplebucket-1250000000"; // Bucket name in the format of `bucketname-appid` (`appid` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket. Replace it with your bucket name.
    qcloud_cos::PutBucketReq req(bucket_name);
    qcloud_cos::PutBucketResp resp;
    
    // 3. Call the bucket creation API
    qcloud_cos::CosResult result = cos.PutBucket(req, &resp);
    
    // 4. Process the call result
    if (result.IsSucc()) {
        // Created successfully
    } else {
        // Failed to create the bucket. You can call the CosResult member functions to output the error information such as the `requestID`.
        std::cout << "HttpStatus=" << result.GetHttpStatus() << std::endl;
        std::cout << "ErrorCode=" << result.GetErrorCode() << std::endl;
        std::cout << "ErrorMsg=" << result.GetErrorMsg() << std::endl;
        std::cout << "ResourceAddr=" << result.GetResourceAddr() << std::endl;
        std::cout << "XCosRequestId=" << result.GetXCosRequestId() << std::endl;
        std::cout << "XCosTraceId=" << result.GetXCosTraceId() << std::endl;
    }
}

```

### Querying bucket list

```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"

int main(int argc, char *argv[]) {
    // 1. Specify the path of the configuration file and initialize CosConfig
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
        // Failed to query the bucket list. You can call the CosResult member functions to output the error information such as the `requestID`.
        std::cout << "HttpStatus=" << result.GetHttpStatus() << std::endl;
        std::cout << "ErrorCode=" << result.GetErrorCode() << std::endl;
        std::cout << "ErrorMsg=" << result.GetErrorMsg() << std::endl;
        std::cout << "ResourceAddr=" << result.GetResourceAddr() << std::endl;
        std::cout << "XCosRequestId=" << result.GetXCosRequestId() << std::endl;
        std::cout << "XCosTraceId=" << result.GetXCosTraceId() << std::endl;
    }
}
```

### Uploading object

```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"

int main(int argc, char *argv[]) {
    // 1. Specify the path of the configuration file and initialize CosConfig
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. Construct a request to upload a file
    std::string bucket_name = "examplebucket-1250000000"; // Bucket name in the format of `bucketname-appid` (`appid` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket. Replace it with your bucket name.
    std::string object_name = "exampleobject"; // `exampleobject` is the object key, the unique identifier of the object in the bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. Replace it with your object name.
    qcloud_cos::PutObjectByFileReq req(bucket_name, object_name, "/path/to/local/file"); // Replace the value with your file path
    //req.SetXCosStorageClass("STANDARD_IA"); // `STANDARD_IA` is the default value. You can call the `Set` method to set the storage class.
    qcloud_cos::PutObjectByFileResp resp;
    
    // 3. Call the object uploading API
    qcloud_cos::CosResult result = cos.PutObject(req, &resp);
    
    // 4. Process the call result
    if (result.IsSucc()) {
        // Uploaded the file successfully
    } else {
        // Failed to upload the file. You can call the CosResult member functions to output the error information such as the `requestID`.
        std::cout << "HttpStatus=" << result.GetHttpStatus() << std::endl;
        std::cout << "ErrorCode=" << result.GetErrorCode() << std::endl;
        std::cout << "ErrorMsg=" << result.GetErrorMsg() << std::endl;
        std::cout << "ResourceAddr=" << result.GetResourceAddr() << std::endl;
        std::cout << "XCosRequestId=" << result.GetXCosRequestId() << std::endl;
        std::cout << "XCosTraceId=" << result.GetXCosTraceId() << std::endl;
    }
}
```

### Querying object list

```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"

int main(int argc, char *argv[]) {
    // 1. Specify the path of the configuration file and initialize CosConfig
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. Construct a request to query the object list
    std::string bucket_name = "examplebucket-1250000000"; // Bucket name in the format of `bucketname-appid` (`appid` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket. Replace it with your bucket name.
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
        // Failed to query the object list. You can call the CosResult member functions to output the error information such as the `requestID`.
        std::cout << "HttpStatus=" << result.GetHttpStatus() << std::endl;
        std::cout << "ErrorCode=" << result.GetErrorCode() << std::endl;
        std::cout << "ErrorMsg=" << result.GetErrorMsg() << std::endl;
        std::cout << "ResourceAddr=" << result.GetResourceAddr() << std::endl;
        std::cout << "XCosRequestId=" << result.GetXCosRequestId() << std::endl;
        std::cout << "XCosTraceId=" << result.GetXCosTraceId() << std::endl;
    }
}
```

### Downloading object

```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"

int main(int argc, char *argv[]) {
    // 1. Specify the path of the configuration file and initialize CosConfig
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. Construct a request to download an object
    std::string bucket_name = "examplebucket-1250000000"; // Bucket name in the format of `bucketname-appid` (`appid` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket. Replace it with your bucket name.
    std::string object_name = "exampleobject"; // `exampleobject` is the object key, the unique identifier of the object in the bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. Replace it with your object name.
    std::string local_path = "/tmp/exampleobject";
    // `appid`, `bucketname`, `object`, and a local path (including filename) are required for the request
    qcloud_cos::GetObjectByFileReq req(bucket_name, object_name, local_path);
    qcloud_cos::GetObjectByFileResp resp;
    
    // 3. Call the object downloading API
    qcloud_cos::CosResult result = cos.GetObject(req, &resp);
    
    // 4. Process the call result
    if (result.IsSucc()) {
        // Downloaded the file successfully
    } else {
        // Failed to download the file. You can call the CosResult member functions to output the error information such as the `requestID`.
        std::cout << "HttpStatus=" << result.GetHttpStatus() << std::endl;
        std::cout << "ErrorCode=" << result.GetErrorCode() << std::endl;
        std::cout << "ErrorMsg=" << result.GetErrorMsg() << std::endl;
        std::cout << "ResourceAddr=" << result.GetResourceAddr() << std::endl;
        std::cout << "XCosRequestId=" << result.GetXCosRequestId() << std::endl;
        std::cout << "XCosTraceId=" << result.GetXCosTraceId() << std::endl;
    }
}
```

### Deleting object

```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"

int main(int argc, char *argv[]) {
    // 1. Specify the path of the configuration file and initialize CosConfig
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. Construct a request to delete an object
    std::string bucket_name = "examplebucket-1250000000"; // Bucket name in the format of `bucketname-appid` (`appid` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket. Replace it with your bucket name.
    std::string object_name = "exampleobject"; // `exampleobject` is the object key, the unique identifier of the object in the bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. Replace it with your object name.
    // 3. Call the object deleting API
	qcloud_cos::DeleteObjectReq req(bucket_name, object_name);
	qcloud_cos::DeleteObjectResp resp;
	qcloud_cos::CosResult result = cos.DeleteObject(req, &resp); 
    
    // 4. Process the call result
    if (result.IsSucc()) {
        // Deleted the object successfully
    } else {
        // Failed to delete the object. You can call the CosResult member functions to output the error information such as the `requestID`.
        std::cout << "HttpStatus=" << result.GetHttpStatus() << std::endl;
        std::cout << "ErrorCode=" << result.GetErrorCode() << std::endl;
        std::cout << "ErrorMsg=" << result.GetErrorMsg() << std::endl;
        std::cout << "ResourceAddr=" << result.GetResourceAddr() << std::endl;
        std::cout << "XCosRequestId=" << result.GetXCosRequestId() << std::endl;
        std::cout << "XCosTraceId=" << result.GetXCosTraceId() << std::endl;
    }
}
```
