## Download and installation

#### Relevant Resources

- The COS XML SDK for C++ source code can be downloaded below:
 - Linux version: [XML SDK for C++ on Linux](https://github.com/tencentyun/cos-cpp-sdk-v5)
 - Windows version: [XML SDK for C++ on Windows](https://github.com/tencentyun/cos-cpp-sdk-v5/tree/windows_dev)
- The sample demo can be download [here](https://github.com/tencentyun/cos-cpp-sdk-v5/blob/master/demo/cos_demo.cpp).

#### Environmental Requirements

- The COS XML SDK for C++ supports Linux and Windows but not macOS.
- Required static library: jsoncpp boost_system boost_thread Poco (under the lib folder).
- Required dynamic library: ssl crypto rt z (installation required).
  The JsonCpp libraries and header files are available in the SDK. If you want to install them on your own, please follow the steps below to install the libraries and finish the compiling, then replace the corresponding libraries and header files in the SDK. If the libraries above are already installed in the system, you can also delete the corresponding libraries and header files in the SDK.



### Installing the SDK on Linux

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

>You can specify the local `Boost` header file path by modifying the following statement in the `CMakeList.txt` file: 
>```
>SET(BOOST_HEADER_DIR "/root/boost_1_61_0")
>```

#### 5. Compile COS SDK for C++ 

Download the [XML C++ SDK source code](https://github.com/tencentyun/cos-cpp-sdk-v5), integrate it into your development environment, and run the following command:

```shell
cd ${cos-cpp-sdk} 
mkdir -p build 
cd build 
cmake .. 
make
```

>The [demo](https://github.com/tencentyun/cos-cpp-sdk-v5/blob/master/demo/cos_demo.cpp) contains examples of common APIs. The generated cos_demo can be executed directly; the generated static library is named libcossdk.a; the generated libcossdk.a should be placed in the lib directory of your project; and the generated include directory should be copied to the include path of your project.



### Installing the SDK on Windows

#### 1. Install Visual Studio 2017

On Windows, install the Visual Studio 2017 development environment.

#### 2. Install CMake

Download the CMake compilation tool for Windows from [CMake's official website](https://cmake.org/download/) and configure `${CMake installation path}/bin` in the system environment variable `Path` on Windows.

#### 3. Install OpenSSL

(1) Download the OpenSSL source code from [OpenSSL's official website](https://www.openssl.org/) and compile it, or select an .exe file of it for Windows [here](https://slproweb.com/products/Win32OpenSSL.html).
(2) Add the `OPENSSL_ROOT_DIR` variable to the system environment variables on Windows and set it to `${OpenSSL installation path}`.
For example, set the system environment variable: `OPENSSL_ROOT_DIR=D:\OpenSSL-Win64`
(3) Configure `${OpenSSL installation path}/bin` in the system environment variable `Path` on Windows.

#### 4. Install Poco

Download the complete version of Poco libraries and header files from [Poco's official website](https://pocoproject.org/download.html) and install them.

(1) Open Windows command line, run `cd` to go to the source code directory of Poco, and run `mkdir examplefolder` to create a folder (replace `examplefolder` with your custom folder name).
(2) On the Windows command line, run `cd examplefolder` (replace `examplefolder` with your custom folder name) and then run `cmake ..`.
(3) Then, use Visual Studio 2017 to open the solution and compile.

#### 5. Install Boost 

Download the Boost source code at [Boost's official website](https://www.boost.org/).

(1) Open Windows command line, run `cd` to go to the source code directory of Boost.
(2) In the Boost source code directory, run `bootstrap`.
(3) Then, run the `b2` compilation command on the Windows command line.

#### Notes
There are four code generation methods in Visual Studio 2017, which correspond to different selection commands in Boost during compilation.

The b2.exe compilation command modes are as follows:

|link	|runtime-link|	Compilation Mode |	Multi-thread Type |
|---------|---------|---------|---------|
|static|	static|	release	|MT|
|static|	static|	debug|	MTd|
|static	|shared|	release	|MD|
|static|	shared	|debug	|MDd|

For example, the 32-bit multi-thread type is MD, and the command is as follows:
```shell
b2 variant=release link=static runtime-link=shared threading=multi address-model=32
```


#### 6. Install JsonCpp

(1) Download the [JsonCpp source code](https://github.com/open-source-parsers/jsoncpp). You are recommended to select a [lower version](https://github.com/open-source-parsers/jsoncpp/tree/0.y.z) on Windows 32-bit.
(2) Open Windows command line, run `cd` to go to the source code directory of JsonCpp, and run `mkdir examplefolder` to create a folder (replace `examplefolder` with your custom folder name).
(3) On the Windows command line, run `cd examplefolder` (replace `examplefolder` with your custom folder name) and then run `cmake ..`.
(4) Use Visual Studio 2017 to open the solution and compile.
(5) After compilation, copy the compiled `jsoncpplib` to the lib folder under the COS SDK for C++ installation directory.

#### 7. Compile the COS SDK for C++ 

(1) Download the [COS XML SDK for C++ on Windows source code](https://github.com/tencentyun/cos-cpp-sdk-v5/tree/windows_dev), integrate it into your development environment, and compile it:
(2) Open Windows command line, run `cd` to go to the source code directory of the SDK for C++, and run `mkdir examplefolder` to create a folder (replace `examplefolder` with your custom folder name).
(3) Modify the `CMakeLists.txt` file in the `${cos-cpp-sdk}` installation directory. Below is an example:

```
# include directories
INCLUDE_DIRECTORIES(./include)
INCLUDE_DIRECTORIES(${OpenSSL installation directory}/include)
INCLUDE_DIRECTORIES(${Boost installation directory}/boost)
INCLUDE_DIRECTORIES(${Poco installation directory}/NetSSL_OpenSSL/include)
INCLUDE_DIRECTORIES(${Poco installation directory}/Foundation/include)
INCLUDE_DIRECTORIES(${Poco installation directory}/Net/include)
INCLUDE_DIRECTORIES(${Poco installation directory}/Crypto/include)
INCLUDE_DIRECTORIES(${Poco installation directory}/Util/include)

# lib directories
link_directories(${OpenSSL installation directory}/lib)
link_directories(${Poco compilation directory}/lib/Release)
link_directories(./lib)
link_directories(${Boost installation directory}/stage/lib)
```
(3) On the Windows command line, run `cd examplefolder` (replace `examplefolder` with your custom folder name) and then run `cmake ..`.
(4) Use Visual Studio 2017 to open the solution and compile.



## Getting Started

The section below describes how to perform basic operations with COS C++ SDK, such as initializing a client, creating a bucket, querying the bucket list, uploading an object, querying the object list, downloading an object, and deleting an object.

> For more information on the meanings of parameters such as SecretId, SecretKey, and Bucket contained herein and how to get them, please see [COS Glossary](https://cloud.tencent.com/document/product/436/7751#.E6.9C.AF.E8.AF.AD.E4.BF.A1.E6.81.AF).

### Initialization

Descriptions of fields in the configuration file:

```
// For SDK config files before V5.4.3, please use "AccessKey"
"SecretId":"COS_SECRETID", 
"SecretKey":"COS_SECRETKEY",

// COS region. For regions and their abbreviations, please visit https://cloud.tencent.com/document/product/436/6224 
"Region":"Region",

// Signature timeout period in seconds    
"SignExpiredTime":360, 

// Connection timeout period in milliseconds
"ConnectTimeoutInms":6000,

// HTTP request timeout period in milliseconds 
"HttpTimeoutInms":60000,  

// Part size in multipart upload; value range: 1 MB–5 GB; default value: 1 MB  
"UploadPartSize":1048576,  

// Thread pool size in single-file multipart upload       
"UploadThreadPoolSize":5, 

// The size of each part in file download   
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

### Creating a bucket

```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"

int main(int argc, char *argv[]) {
    // 1. Specify the path to the configuration file and initialize CosConfig
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

### Querying bucket List

```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"

int main(int argc, char *argv[]) {
    // 1. Specify the path to the configuration file and initialize CosConfig
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

### Uploading an object

```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"

int main(int argc, char *argv[]) {
    // 1. Specify the path to the configuration file and initialize CosConfig
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. Construct the request to upload a file
    std::string bucket_name = "examplebucket-1250000000"; // Destination bucket name
    std::string object_name = "exampleobject"; // exampleobject is the object key (`Key`) which is a unique ID for the object in the bucket. For example, in the object's access domain name examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg, the object key is `doc/pic.jpg`
    // The local file path is required in the constructor of `request`.
    qcloud_cos::PutObjectByFileReq req(bucket_name, object_name, "/path/to/local/file");
    req.SetXCosStorageClass("STANDARD_IA"); // Call the `Set` method to set metadata
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

### Querying the object list

```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"

int main(int argc, char *argv[]) {
    // 1. Specify the path to the configuration file and initialize CosConfig
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
    // 1. Specify the path to the configuration file and initialize CosConfig
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. Construct the request to create a bucket
    std::string bucket_name = "examplebucket-1250000000"; // Destination bucket name
    std::string object_name = "exampleobject"; // exampleobject is the object key (Key) which is a unique ID for the object in the bucket. For example, in the object's access domain name examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg, the object key is doc/pic.jpg
    std::string local_path = "/tmp/exampleobject";
    // Request needs to carry appid, bucketname, object, and local path (including the file name)
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

### Deleting an object

```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"

int main(int argc, char *argv[]) {
    // 1. Specify the path to the configuration file and initialize CosConfig
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. Construct the request to create a bucket
    std::string bucket_name = "examplebucket-1250000000"; // Destination bucket name
    std::string object_name = "exampleobject"; // exampleobject is the object key (Key) which is a unique ID for the object in the bucket. For example, in the object's access domain name examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg, the object key is doc/pic.jpg
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
