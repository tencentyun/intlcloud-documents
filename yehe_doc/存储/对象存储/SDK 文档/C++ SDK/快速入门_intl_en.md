## Download and Installation

#### Related resources

- Download COS XML C++ SDK source code below:
 - Linux: [XML Linux SDK for C++](https://github.com/tencentyun/cos-cpp-sdk-v5)
 - Windows: [XML Windows SDK for C++](https://github.com/tencentyun/cos-cpp-sdk-v5/tree/windows_dev)
 - macOS: [XML macOS SDK for C++](https://github.com/tencentyun/cos-cpp-sdk-v5)
- Download the demo [here](https://github.com/tencentyun/cos-cpp-sdk-v5/blob/master/demo/cos_demo.cpp)
- For the SDK changelog, please see [Changelog](https://github.com/tencentyun/cos-cpp-sdk-v5/blob/master/CHANGELOG.md).

>? If you encounter errors such as non-existent functions or methods when using the XML version of the SDK, please update the SDK to the latest version and try again.
>

#### Environment dependencies

- Dependent static library: boost_system boost_thread Poco (in the lib folder).
- Dependent dynamic library: ssl crypto rt z (installation required).
The `JsonCpp` libraries and header files are available in the SDK. If you want to install them on your own, please follow the steps below to install the libraries and finish the compiling, then replace the corresponding libraries and header files in the SDK. If the libraries above are already installed in the system, you can also delete the corresponding libraries and header files in the SDK.

### Installing the Linux SDK

#### 1. Install CMake

```shell
yum install -y gcc gcc-c++ make automake
// Install `gcc` and other required packages (skip this step if they have already been installed)
yum install -y wget

// The version of CMake should be above 3.5
wget https://cmake.org/files/v3.5/cmake-3.5.2.tar.gz
tar -zxvf cmake-3.5.2.tar.gz
cd cmake-3.5.2
./bootstrap --prefix=/usr
gmake
gmake install
```

#### 2. Install Boost libraries and header files

```shell
wget http://sourceforge.net/projects/boost/files/boost/1.54.0/boost_1_54_0.tar.gz
tar -xzvf boost_1_54_0.tar.gz
cd boost_1_54_0
./bootstrap.sh --prefix=/usr/local
./b2 install --with=all
#Boost libraries are installed in the `/usr/local/lib` directory
```

>? You can specify the local Boost header file path by modifying the following statement in the `CMakeList.txt` file: 
>```
>SET(BOOST_HEADER_DIR "/root/boost_1_61_0")
>```



#### 3. Install OpenSSL

**Method 1 (recommended)**

​```shell
yum install openssl openssl-devel
```

**Method 2 (not recommended)**

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

# Add a header/lib file search path (can be written into the ~/.bashrc file)
LIBRARY_PATH=/usr/local/ssl/lib/:$LIBRARY_PATH
CPLUS_INCLUDE_PATH=/usr/local/ssl/include/:$CPLUS_INCLUDE_PATH
```

#### 4. Install Poco

Download [Poco v1.9.4](https://github.com/pocoproject/poco/releases/tag/poco-1.9.4-release), compile it, and install the library and header files.

```shell
./configure --omit=Data/ODBC,Data/MySQL
make
make install
```

#### 5. Compile the COS CPP SDK 

Download the [XML C++ SDK source code](https://github.com/tencentyun/cos-cpp-sdk-v5), integrate it into your development environment, and run the following command:

```shell
cd ${cos-cpp-sdk} 
mkdir -p build 
cd build 
cmake .. 
make
```

>? The [Demo](https://github.com/tencentyun/cos-cpp-sdk-v5/blob/master/demo/cos_demo.cpp) provides examples of common APIs. The generated `cos_demo` can be executed directly; the generated static library is named `libcossdk.a` and should be placed in the `lib` path of your project; the generated `include` directory should be copied to the `include` path of your project.
>


### Installing the Windows SDK

#### 1. Install visual studio 2017

Install Visual Studio 2017 as a development environment for Windows.

#### 2. Install CMake

Download the Windows version of the CMake compiler from the [CMake official website](https://cmake.org/download/), and configure `${CMake installation path}\bin` in the `Path` environment variable.

#### 3. Install OpenSSL

i. Download the Windows version of .exe from this [third-party website](https://slproweb.com/products/Win32OpenSSL.html), or download the [OpenSSL source code](https://www.openssl.org/) and compile it.
ii. Add the `OPENSSL_ROOT_DIR` variable to the Windows system environment variables and set it to `${OpenSSL installation path}`.
For example:  `OPENSSL_ROOT_DIR=D:\OpenSSL-Win64`.
iii. Configure `${OpenSSL installation path}\bin` in the `Path` environment variable.

#### 4. Install Poco

Download [Poco v1.9.4](https://github.com/pocoproject/poco/releases/tag/poco-1.9.4-release), compile it, and install the library and header files.
i. Open the Windows Command Prompt program and use the `cd` command to navigate to the Poco source code directory; then, run `mkdir examplefolder` to create a folder (be sure to replace `examplefolder` with your custom folder name).
ii. Continue to run `cd examplefolder` (be sure to replace `examplefolder` with your custom folder name), and run the `cmake ..` command.
iii. Use Visual Studio 2017 to open the solution and compile it.

#### 5. Install Boost 

Download the Boost source code from the [Boost official website](https://www.boost.org/).
i. Open the Windows Command Prompt program and use the `cd` command to navigate to the Boost source code directory.
ii. Run the `bootstrap` command in this directory.
iii. Run the `b2` compilation command in the Windows Command Prompt program.

#### Precautions
Visual Studio 2017 provides four code generation methods which correspond to different commands during Boost compilation.

The code for the `b2.exe` compilation command is as shown below:

|link|runtime-link|compilation mode|multi-thread type|
|---------|---------|---------|---------|
|static|static|release|MT|
|static|static|debug|MTd|
|static|shared|release|MD|
|static|shared|debug|MDd|

For example, if the 32-bit multi-thread type is MD, the command is as follows:
```shell
b2 variant=release link=static runtime-link=shared threading=multi address-model=32
```

#### 6. Install jsoncpp

i. Download the JsonCpp source code [here](https://github.com/open-source-parsers/jsoncpp). For Win32, we recommend that you select an [earlier version](https://github.com/open-source-parsers/jsoncpp/tree/0.y.z).
ii. Open the Windows Command Prompt program and use the `cd` command to navigate to the jsoncpp source code directory; then, run `mkdir examplefolder` to create a folder (be sure to replace `examplefolder` with your custom folder name).
iii. Continue to run `cd  examplefolder` (replace `examplefolder` with your custom folder name), and run the `cmake ..` command.
iv. Use Visual Studio 2017 to open the solution and compile it.
v. Once the compilation is complete, copy the resulting `jsoncpp.lib` to the lib folder under the COS CPP SDK installation directory.

#### 7. Compile the COS CPP SDK 

i. Download [XML Windows C++ SDK source code](https://github.com/tencentyun/cos-cpp-sdk-v5/tree/windows_dev), integrate it into your development environment, and begin compilation.
ii. Open the Windows Command Prompt program and use the `cd` command to navigate to the C++ SDK source code directory; then, run `mkdir examplefolder` to create a folder (be sure to replace `examplefolder` with your custom folder name).
iii. Modify the `CMakeLists.txt` file in the `${cos-cpp-sdk}` installation directory as shown below:
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
iv. In the Windows Command Prompt program, run `cd examplefolder` (replace `examplefolder` with your custom folder name) and run the `cmake ..` command.
v. Use Visual Studio 2017 to open the solution and compile it.

### Installing the Mac SDK

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
#Boost libraries are installed in the `/usr/local/lib` directory
```

#### 3. Install OpenSSL

Download and compile the `openssl-1.1.1d.tar.gz` source code from the [OpenSSL official website](https://www.openssl.org/).

```shell
tar -zxvf openssl-1.1.1d.tar.gz
cd openssl-1.1.1d/
./config  --prefix=/usr/local 
make 
make install
#openssl libraries are installed in the `/usr/local/` directory
```

#### 4. Install Poco

Download [Poco v1.9.4](https://github.com/pocoproject/poco/releases/tag/poco-1.9.4-release), compile it, and install the library and header files.

```shell
cd Poco/ 
./configure --omit=Data/ODBC,Data/MySQL
mkdir examplefolder  #(Poco installation directory; Be sure to replace examplefolder with your custom folder name.）
cd examplefolder
cmake .. 
make
```

#### 5. Compile the COS CPP SDK
i. Download the [XML Mac C++ SDK source code](https://github.com/tencentyun/cos-cpp-sdk-v5) and integrate it into your development environment.
ii. Modify the `CMakeLists.txt` file in the `${cos-cpp-sdk}` installation directory as shown below:
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
iii. Run the following command:
```shell
cd ${cos-cpp-sdk} 
mkdir build 
cd build 
cmake .. 
make
```

## Getting Started

The following describes how to use the COS C++ SDK to perform a basic operation, such as initializing a client, creating a bucket, querying a bucket list, uploading an object, querying an object list, downloading an object, and deleting an object.

>? For the definition of terms such as SecretId, SecretKey, and Bucket, please see [COS Glossary](https://intl.cloud.tencent.com/document/product/436/7751).
>

### Initialization

Overview of each field in the configuration file:

```
// For SDK config files before V5.4.3, please use "AccessKey".
"SecretId":"SECRETID", 
"SecretKey":"SECRETKEY",



// COS region. For regions and their abbreviations, see https://cloud.tencent.com/document/product/436/6224. 
"Region":"Region",



// Signature timeout period in seconds    
"SignExpiredTime":360, 



// Connection timeout period in milliseconds
"ConnectTimeoutInms":6000,



// HTTP request timeout period in milliseconds 
"HttpTimeoutInms":60000,  



// Size of uploaded file part. Range: 1 MB-5 GB; default value: 1 MB.  
"UploadPartSize":1048576,  



// Thread pool size for uploading a single file part       
"UploadThreadPoolSize":5, 



// The size of each part in the downloaded file   
"DownloadSliceSize":4194304, 



// Thread pool size for downloading a single file 
"DownloadThreadPoolSize":5,   



// Thread pool size for asynchronous upload and download 
"AsynThreadPoolSize":2, 



// Log output type. 0: do not output; 1: output to screen; 2: output to syslog   
"LogoutType":1,       



// Log level. 1: ERR; 2: WARN; 3: INFO; 4: DBG     
"LogLevel":3,                 
```

### Using a custom domain name to access COS

Add the following configuration in `config.json`:

```cpp
"IsDomainSameToHost":true,
"DestDomain":"mydomain.com",
```

### Accessing COS using a temporary key

```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"
int main(int argc, char *argv[]) {
    qcloud_cos::CosConfig config("./config.json");
    // Set the temporary key.
    config.SetTmpToken("xxx");
    qcloud_cos::CosAPI cos(config);
}
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
    
    // 3. Call the DELETE Bucket API
    qcloud_cos::CosResult result = cos.PutBucket(req, &resp);
    
    // 4. Process the call result
    if (result.IsSucc()) {
        // Bucket created successfully
    } else {
        // Failed to create the bucket. You can call the CosResult member functions to output the error information such as the requestID.
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

### Querying a bucket list

```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"



int main(int argc, char *argv[]) {
    // 1. Specify the configuration file path and initialize CosConfig
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
    // 1. Specify the configuration file path and initialize CosConfig
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. Construct a request to upload a file
    std::string bucket_name = "examplebucket-1250000000"; // Destination bucket name
    std::string object_name = "exampleobject"; // exampleobject is the ObjectKey (Key), the unique ID of an object in a bucket. For example, if the object’s access domain name is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is `doc/pic.jpg`
    // The local file path is required in the constructor of `request`.
    qcloud_cos::PutObjectByFileReq req(bucket_name, object_name, "/path/to/local/file");
    req.SetXCosStorageClass("STANDARD_IA"); // Call the `Set` method to set metadata
    qcloud_cos::PutObjectByFileResp resp;
    
    // 3. Call the PUT Object API
    qcloud_cos::CosResult result = cos.PutObject(req, &resp);
    
    // 4. Process the call result
    if (result.IsSucc()) {
        // File uploaded successfully
    } else {
        // Failed to upload the file. You can call the CosResult member functions to output the error information such as the requestID.
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

### Querying an object list

```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"



int main(int argc, char *argv[]) {
    // 1. Specify the configuration file path and initialize CosConfig
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. Construct a request to query the object list
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
        // Queried the object list successfully
    } else {
        // Failed to query the object list. You can call the CosResult member functions to output the error information such as requestID.
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
    // 1. Specify the configuration file path and initialize CosConfig
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. Construct a request to download the object
    std::string bucket_name = "examplebucket-1250000000"; // Destination bucket name
    std::string object_name = "exampleobject"; // exampleobject is the ObjectKey (Key), the unique ID of an object in a bucket. For example, if the object's access domain name is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is `doc/pic.jpg`
    std::string local_path = "/tmp/exampleobject";
    // The request needs to carry the appid, bucketname, object, and local path (including the file name)
    qcloud_cos::GetObjectByFileReq req(bucket_name, object_name, local_path);
    qcloud_cos::GetObjectByFileResp resp;
    
    // 3. Call the object download API
    qcloud_cos::CosResult result = cos.GetObject(req, &resp);
    
    // 4. Process the call result
    if (result.IsSucc()) {
        // File downloaded successfully
    } else {
        // Failed to download the file. You can call the CosResult member functions to output the error information such as the requestID.
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
    // 1. Specify the configuration file path and initialize CosConfig
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. Construct a request to delete the object
    std::string bucket_name = "examplebucket-1250000000"; // Destination bucket name
    std::string object_name = "exampleobject"; // exampleobject is the ObjectKey (Key), the unique ID of an object in a bucket. For example, if the object's access domain name is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is `doc/pic.jpg`
    // 3. Call the object deleting API
	qcloud_cos::DeleteObjectReq req(bucket_name, object_name);
	qcloud_cos::DeleteObjectResp resp;
	qcloud_cos::CosResult result = cos.DeleteObject(req, &resp); 
    
    // 4. Process the call result
    if (result.IsSucc()) {
        // Deleted the object successfully
    } else {
        // Failed to delete the object. You can call the CosResult member functions to output the error information such as requestID.
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
