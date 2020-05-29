## Download and Installation

### Relevant resources

- Download COS XML C++ SDK source code:
 - Linux: [ XML Linux C++ SDK ](https://github.com/tencentyun/cos-cpp-sdk-v5)
 - Windows: [ XML Windows C++ SDK ](https://github.com/tencentyun/cos-cpp-sdk-v5/tree/windows_dev)
 - Mac: [ XML Mac C++ SDK ](https://github.com/tencentyun/cos-cpp-sdk-v5)
- Download Demo: [COS XML C++ SDK Demo](https://github.com/tencentyun/cos-cpp-sdk-v5/blob/master/demo/cos_demo.cpp)

#### Environment dependencies

- Dependent static library: jsoncpp boost_system boost_thread Poco (in lib folder).
- Dependent dynamic library: ssl crypto rt z (installation required).
  The JsonCpp libraries and header files are available in the SDK. If you want to install them on your own, please follow the steps below to install the libraries and finish the compiling, then replace the corresponding libraries and header files in the SDK. If the libraries above are already installed in the system, you can also delete the corresponding libraries and header files in the SDK.



### Installing Linux SDK

#### 1. Install CMake

```shell
yum install -y gcc gcc-c++ make automake
//Install gcc and other required packages (skip this step if they have been installed)
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
#Boost libraries are installed in the directory /usr/local/lib
```

#### 3. Install OpenSSL

**Method 1**

```shell
yum install openssl openssl-devel
```

**Method 2**

```shell
wget https://www.openssl.org/source/openssl-1.1.1d.tar.gz  
tar -xzvf ./openssl-1.1.1d.tar.gz
cd openssl-1.1.1d/
./config --prefix=/usr/local/ssl --openssldir=/usr/local/ssl
make 
make install
cd /usr/local/
ln -s ssl openssl
echo "/usr/local/openssl/lib" >> /etc/ld.so.conf
ldconfig

# Add header/lib file search path (can be written to ~/.bashrc)
LIBRARY_PATH=/usr/local/ssl/lib/:$LIBRARY_PATH
CPLUS_INCLUDE_PATH=/usr/local/ssl/include/:$CPLUS_INCLUDE_PATH
```

#### 4. Install Poco libraries and header files

Download the complete version of Poco libraries and header files from [Poco's official website](https://pocoproject.org/download.html) and install them.

>The latest version of Poco requires C++14 support. If your compiler only supports C++11 or below, you can use [Poco 1.9.4](https://github.com/pocoproject/poco/releases/tag/poco-1.9.4-release).

```shell
./configure --omit=Data/ODBC,Data/MySQL
make
make install
```

>You can specify the local Boost header file path by modifying the following statement in the `CMakeList.txt` file: 
>```
>SET(BOOST_HEADER_DIR "/root/boost_1_61_0")
>```

#### 5. Compile COS CPP SDK 

Download the [XML C++ SDK source code](https://github.com/tencentyun/cos-cpp-sdk-v5), integrate it into your development environment, and run the following command:

```shell
cd ${cos-cpp-sdk} 
mkdir -p build 
cd build 
cmake .. 
make
```

>[Demo](https://github.com/tencentyun/cos-cpp-sdk-v5/blob/master/demo/cos_demo.cpp) provides examples of common APIs. The generated `cos_demo` can be executed directly; the generated static library is named `libcossdk.a`; the generated `libcossdk.a` should be placed in the `lib` directory of your project; and the generated `include` directory should be copied to the `include` path of your project.



### Installing Windows SDK

#### 1. Install visual studio 2017

Install visual studio 2017 as development environment for Windows.

#### 2. Install CMake

Download the Windows version of CMake compiler from [CMake official website](https://cmake.org/download/), and configure `${CMake installation path}\bin` in `Path`, the Windows system environment variable.

#### 3. Install OpenSSL

(1) Download the OpenSSL source code from [OpenSSL official website](https://www.openssl.org/) and compile it, or select and install the Window version of the .exe file from a third-party [website](https://slproweb.com/products/Win32OpenSSL.html).
(2) Add `OPENSSL_ROOT_DIR` to Windows system environment variables, and set it to `${OpenSSL installation path}`,
e.g. setting `OPENSSL_ROOT_DIR=D:\OpenSSL-Win64`.
(3) Configure `${OpenSSL installation path}\bin` in the Windows system environment variable Path.

#### 4. Install Poco

Download the complete version of Poco libraries and header files from [Poco's official website](https://pocoproject.org/download.html) and install them.

(1) Open Windows Command Prompt window, use the `cd` command to navigate to the Poco source code directory, and run `mkdir examplefolder `(replace `examplefolder` with your custom folder name) to create a folder.
(2) Continue to run `cd examplefolder` (replace `examplefolder` with your custom folder name), and `cmake ..`.
(3) Use visual studio 2017 to open the solution and compile it.

#### 5. Install Boost 

Download Boost source code from [Boost official website](https://www.boost.org/).

(1) Open Windows Command Prompt window, and use the `cd` command to navigate to the Boost source code directory.
(2) Run the `bootstrap` command in this directory.
(3) Run the `b2` compilation command in Windows Command Prompt window.

#### Considerations
Visual studio 2017 provides 4 code generation modes for different commands you can select during Boost compilation.

The code for b2.exe compilation command is as shown below:

|link|runtime-link|compilation mode|multi-thread type|
|---------|---------|---------|---------|
|static|static|release|MT|
|static|static|debug|MTd|
|static|shared|release|MD|
|static|shared|debug|MDd|

If the 32-bit multi-thread type is MD, for example, the command will be
```shell
b2 variant=release link=static runtime-link=shared threading=multi address-model=32
```


#### 6. Install jsoncpp

(1) Download [jsoncpp source code](https://github.com/open-source-parsers/jsoncpp). For Win32, we recommend you select a [lower version](https://github.com/open-source-parsers/jsoncpp /tree/0.yz).
(2) Open Windows Command Prompt window, use the `cd` command to navigate to the jsoncpp source code directory, and run `mkdir examplefolder `(replace `examplefolder` with your custom folder name) to create a folder.
(3) Continue to run `cd examplefolder `(replace `examplefolder` with your custom folder name), and `cmake ..`.
(5) Use visual studio 2017 to open the solution and compile it.
(5) Once the compilation is complete, copy the resulting jsoncpplib to the lib folder under COS CPP SDK installation directory.

#### 7. Compile COS CPP SDK 

(1) Download [XML Windows C++ SDK source code] (https://github.com/tencentyun/cos-cpp-sdk-v5/tree/windows_dev), integrate it into your development environment, and begin compilation.
(2) Open Windows Command Prompt window, use the `cd` command to navigate to the C++ SDK source code directory, and run `mkdir examplefolder` (replace `examplefolder` with your custom folder name) to create a folder.
(3) Modify the CMakeLists.txt file in the `${cos-cpp-sdk}` installation directory, with an example as shown below:

```cpp
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
(4) In Windows Command Prompt window, run `cd examplefolder` (replace `examplefolder` with your custom folder name) and `cmake ..`.
(5) Use visual studio 2017 to open the solution and compile it.

### Install Mac SDK

#### 1. Install CMake
```shell
brew install cmake
```

#### 2. Install Boost libraries and header files

```shell
wget http://sourceforge.net/projects/boost/files/boost/1.54.0/boost_1_54_0.tar.gz
tar -xzvf boost_1_54_0.tar.gz
cd boost_1_54_0
./bootstrap.sh --prefix=/usr/local
./b2 install --with=all
#Boost libraries are installed in the directory /usr/local/lib
```

#### 3. Install OpenSSL

Download the openssl-1.1.1d.tar.gz source code from [OpenSSL official website](https://www.openssl.org/) for compilation.

```shell
tar -zxvf openssl-1.1.1d.tar.gz
cd openssl-1.1.1d/
./config  --prefix=/usr/local 
make 
make install
#openssl libraries are installed in the /usr/local/ directory
```

#### 4. Install Poco libraries and header files

Download and install the latest version of Poco libraries and header files from [Poco official website](https://pocoproject.org/download.html), or directly use the git command to download [Poco](https://github.com/pocoproject/poco.git).

>The latest version of Poco requires C++14 support. If your compiler only supports C++11 or below, you can use [Poco 1.9.4](https://github.com/pocoproject/poco/releases/tag/poco-1.9.4-release).

```shell
cd Poco/ 
./configure --omit=Data/ODBC,Data/MySQL
mkdir examplefolder  #(Replace examplefolder with your custom folder name.）
cd examplefolder
cmake .. 
make
```

#### 5. Install jsoncpp

Download [jsoncpp source code](https://github.com/open-source-parsers/jsoncpp).

```shell
cd jsoncpp/
mkdir examplefolder  #(jsoncpp installation directory. Replace examplefolder with your custom folder name.）
cd examplefolder
cmake .. 
make
```

Once the compilation is complete, copy the resulting jsoncpplib to the lib folder under COS CPP SDK installation directory.

#### 6. Compile COS CPP SDK
(1) Download [XML C++ SDK source code](https://github.com/tencentyun/cos-cpp-sdk-v5), and integrate it into your development environment.
(2) Modify the CMakeLists.txt file in the `${cos-cpp-sdk}` installation directory, with an example as shown below:
 
```cpp
# include directories
INCLUDE_DIRECTORIES(./include)
INCLUDE_DIRECTORIES(/usr/local/include)
INCLUDE_DIRECTORIES(${Poco installation directory}/NetSSL_OpenSSL/include)
INCLUDE_DIRECTORIES(${Poco installation directory}/Foundation/include)
INCLUDE_DIRECTORIES(${Poco installation directory}/Net/include)
INCLUDE_DIRECTORIES(${Poco installation directory}/Crypto/include)
INCLUDE_DIRECTORIES(${Poco installation directory}/Util/include)

# lib directories
link_directories(/usr/local/lib)
link_directories(${Poco compilation directory}/lib/Release)
link_directories(./lib)
```
 
Then run this command:
 
```shell
cd ${cos-cpp-sdk} 
mkdir build 
cd build 
cmake .. 
make
```

## Getting Started

The following describes how to use COS C# SDK to perform a basic operation, such as initializing the client, creating a bucket, querying the bucket list, uploading an object, querying the object list, downloading an object, and deleting an object.

>For the definitions of parameters such as SecretId, SecretKey, and Bucket, see [COS Glossary](https://intl.cloud.tencent.com/document/product/436/7751).

### Initialization

Descriptions of fields in the configuration file:

```
// For SDK config files before V5.4.3, please use "AccessKey" 
"SecretId":"COS_SECRETID", 
"SecretKey":"COS_SECRETKEY",

// COS region. For regions and their abbreviations, see https://intl.cloud.tencent.com/document/product/436/6224
"Region":"Region",

// Signature timeout (in sec)    
"SignExpiredTime":360, 

// Connection timeout period in milliseconds
"ConnectTimeoutInms":6000,

// HTTP request timeout period in milliseconds 
"HttpTimeoutInms":60000,  

// Size of uploaded file part. Range: 1 MB-5 GB; default value: 1 MB.  
"UploadPartSize":1048576,  

// Thread pool size for uploading a single file part       
"UploadThreadPoolSize":5, 

// The size of each part in file download   
"DownloadSliceSize":4194304, 

// Thread pool size for downloading a single file 
"DownloadThreadPoolSize":5,   

// Thread pool size for asynchronous upload and download 
"AsynThreadPoolSize":2, 

// Log output type. 0: do not output; 1: output to screen; 2: output to syslog   
"LogoutType":1,       

// Log level. 1 :ERR; 2: WARN; 3: INFO; 4:DBG     
"LogLevel":3,                 

```

### Creating a bucket

```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"

int main(int argc, char *argv[]) {
    // 1. Specify the configuration file path and initialize CosConfig
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. Construct the PUT Bucket request
    std::string bucket_name = "examplebucket-1250000000"; // Bucket name
    qcloud_cos::PutBucketReq req(bucket_name);
    qcloud_cos::PutBucketResp resp;
    
    // 3. Call the PUT Bucket API
    qcloud_cos::CosResult result = cos.PutBucket(req, &resp);
    
    // 4. Process the call result
    if (result.IsSucc()) {
        Created successfully
    } else {
        // Failed to create the bucket. You can call the member function of CosResult to output the error information such as requestID.
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

### Querying bucket list

```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"

int main(int argc, char *argv[]) {
    // 1. Specify the path to the configuration file and initialize CosConfig
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. Construct a request to upload a file
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
        // File is uploaded successfully
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
    
    // 2. Construct a request to upload a file
    std::string bucket_name = "examplebucket-1250000000"; // Destination bucket name
    std::string object_name = "exampleobject"; // exampleobject is the object key (`Key`) which is a unique ID for the object in the bucket. For example, in the object's access domain name examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg, the object key is `doc/pic.jpg`
    // The local file path is required in the constructor of `request`.
    qcloud_cos::PutObjectByFileReq req(bucket_name, object_name, "/path/to/local/file");
    req.SetXCosStorageClass("STANDARD_IA"); // Call the `Set` method to set metadata
    qcloud_cos::PutObjectByFileResp resp;
    
    // 3. Call the PUT Object API
    qcloud_cos::CosResult result = cos.PutObject(req, &resp);
    
    // 4. Process the call result
    if (result.IsSucc()) {
        // File is uploaded successfully
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

### Querying object list

```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"

int main(int argc, char *argv[]) {
    // 1. Specify the configuration file path and initialize CosConfig
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. Construct the DELETE Bucket request
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
        // File is uploaded successfully
    } else {
        // Failed to upload the file. You can call the member function of CosResult to output the error information such as requestID.
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

### Downloading an object

```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"

int main(int argc, char *argv[]) {
    // 1. Specify the path to the configuration file and initialize CosConfig
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. Construct the DELETE Bucket request
    std::string bucket_name = "examplebucket-1250000000"; // Destination bucket name
    std::string object_name = "exampleobject"; // exampleobject is the object key (Key) which is a unique ID for the object in the bucket. For example, in the object's access domain name examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg, the object key is doc/pic.jpg
    std::string local_path = "/tmp/exampleobject";
    // Request needs to carry appid, bucketname, object, and local path (including the file name)
    qcloud_cos::GetObjectByFileReq req(bucket_name, object_name, local_path);
    qcloud_cos::GetObjectByFileResp resp;
    
    // 3. Call the PUT Bucket API
    qcloud_cos::CosResult result = cos.GetObject(req, &resp);
    
    // 4. Process the call result
    if (result.IsSucc()) {
        // File is downloaded successfully
    } else {
        // Failed to download the file. You can call the member function of CosResult to output the error information such as requestID.
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
    
    // 2. Construct the DELETE Bucket request
    std::string bucket_name = "examplebucket-1250000000"; // Destination bucket name
    std::string object_name = "exampleobject"; // exampleobject is the object key (Key) which is a unique ID for the object in the bucket. For example, in the object's access domain name examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg, the object key is doc/pic.jpg
    // 3. Call the DELETE Bucket API
	qcloud_cos::DeleteObjectReq req(bucket_name, object_name);
	qcloud_cos::DeleteObjectResp resp;
	qcloud_cos::CosResult result = cos.DeleteObject(req, &resp); 
    
    // 4. Process the call result
    if (result.IsSucc()) {
        // File is downloaded successfully
    } else {
        // Failed to download the file. You can call the member function of CosResult to output the error information, such as requestID.
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
