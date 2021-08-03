## 다운로드 및 설치

#### 관련 리소스

- COS의 XML C++ SDK 소스 코드 다운로드 주소는 다음과 같습니다.
 - Linux 버전: [XML Linux C++ SDK](https://github.com/tencentyun/cos-cpp-sdk-v5)
 - Windows 버전: [XML Windows C++ SDK](https://github.com/tencentyun/cos-cpp-sdk-v5/tree/windows_dev)
 - Mac 버전: [XML Mac C++ SDK](https://github.com/tencentyun/cos-cpp-sdk-v5)
- 예시 Demo 다운로드 주소: [COS XML C++ SDK 예시](https://github.com/tencentyun/cos-cpp-sdk-v5/blob/master/demo/cos_demo.cpp)
- SDK 로그 업데이트는 [ChangeLog](https://github.com/tencentyun/cos-cpp-sdk-v5/blob/master/CHANGELOG.md)를 참고하십시오.

>? XML 버전 SDK 사용 시 함수 또는 메소드 없음 등 오류가 발생하였을 경우, 먼저 XML 버전 SDK를 최신 버전으로 업데이트한 후 재시도하십시오.
>

#### 환경 종속

- 종속 정적 라이브러리: boost_system boost_thread Poco(lib 폴더에 있음)
- 종속 동적 라이브러리: ssl crypto rt z(설치 필요)
SDK에서 JsonCpp 라이브러리 및 헤더 파일을 제공합니다. 직접 설치하려면 다음 순서에 따라 라이브러리를 설치하고 컴파일 완료 후 SDK의 해당 라이브러리 및 헤더 파일로 변경합니다. 상기 라이브러리가 시스템에 설치된 경우 SDK의 해당 라이브러리 및 헤더 파일을 삭제할 수 있습니다.

### Linux버전 SDK 설치

#### 1. CMake 툴 설치

```shell
yum install -y gcc gcc-c++ make automake
//gcc 등 필수 프로그램 패키지를 설치(이미 설치한 경우 생략)
yum install -y wget

// cmake 버전은 3.5보다 커야 함
wget https://cmake.org/files/v3.5/cmake-3.5.2.tar.gz
tar -zxvf cmake-3.5.2.tar.gz
cd cmake-3.5.2
./bootstrap --prefix=/usr
gmake
gmake install
```

#### 2. Boost 라이브러리 및 헤더 파일 설치

```shell
wget http://sourceforge.net/projects/boost/files/boost/1.54.0/boost_1_54_0.tar.gz
tar -xzvf boost_1_54_0.tar.gz
cd boost_1_54_0
./bootstrap.sh --prefix=/usr/local
./b2 install --with=all
#Boost 라이브러리를 /usr/local/lib 디렉터리에 설치
```

>? CMakeList.txt 파일을 수정하여 로컬 Boost 헤더 파일 경로를 지정하고 다음 명령어를 수정합니다. 
>```
>SET(BOOST_HEADER_DIR "/root/boost_1_61_0")
>```
```


#### 3. OpenSSL 설치

** 방법1(권장) **

​```shell
yum install openssl openssl-devel
```

** 방법2(권장하지 않음) **

```shell
wget https://www.openssl.org/source/openssl-1.1.1d.tar.gz  
tar -xzvf./openssl-1.1.1d.tar.gz
cd openssl-1.1.1d/
./config --prefix=/usr/local/ssl --openssldir=/usr/local/ssl
make 
make install
cd /usr/local/
ln -s ssl openssl
echo "/usr/local/openssl/lib" >> /etc/ld.so.conf
ldconfig

# 헤더 파일 추가/라이브러리 파일 경로 조회(~/.bashrc에 입력할 수 있음)
LIBRARY_PATH=/usr/local/ssl/lib/:$LIBRARY_PATH
CPLUS_INCLUDE_PATH=/usr/local/ssl/include/:$CPLUS_INCLUDE_PATH
```

#### 4. Poco 설치

[Poco 1.9.4](https://github.com/pocoproject/poco/releases/tag/poco-1.9.4-release) 버전을 다운로드하여 컴파일한 후 해당 라이브러리 및 헤더 파일을 설치합니다.

```shell
./configure --omit=Data/ODBC, Data/MySQL
make
make install
```

#### 5. COS CPP SDK 컴파일 

[XML C++ SDK 소스 코드](https://github.com/tencentyun/cos-cpp-sdk-v5)를 다운로드하여 개발 환경에 통합하고 다음 명령어를 실행합니다.

```shell
cd ${cos-cpp-sdk} 
mkdir -p build 
cd build 
cmake .. 
make
```

>? [예시 Demo](https://github.com/tencentyun/cos-cpp-sdk-v5/blob/master/demo/cos_demo.cpp)는 자주 사용되는 API 예시를 제공합니다. 생성한 cos_demo는 바로 실행할 수 있으며, 생성된 정적 라이브러리 이름은 `libcossdk.a`입니다. 생성된 `libcossdk.a`는 프로젝트의 lib 경로에 놓고, include 디렉터리는 프로젝트 include 경로에 복사합니다.
>


### Windows 버전 SDK 설치

#### 1. visual studio 2017 설치

Windows 환경에서 visual studio 2017 개발 환경을 설치합니다.

#### 2. CMake 툴 설치

 [CMake 공식 홈페이지](https://cmake.org/download/)에서 Windows버전 CMake 컴파일 툴을 다운로드하고 `${CMake의 설치 경로}\bin`을 Windows 시스템 환경 변수 Path에 설정합니다.

#### 3. OpenSSL 설치

i. 3rd party [웹 사이트](https://slproweb.com/products/Win32OpenSSL.html)에서 Window 버전 .exe 파일을 선택하여 설치하거나, [OpenSSL 공식 홈페이지](https://www.openssl.org/)에서 OpenSSL 소스 코드를 다운로드하여 컴파일 설치할 것을 권장합니다. 
ii. Windows 시스템에서 시스템 환경 변수인 `OPENSSL_ROOT_DIR` 변수를 추가하고 `${OpenSSL의 설치 경로}`로 설정합니다.
예를 들어, 시스템 환경 변수를 `OPENSSL_ROOT_DIR=D:\OpenSSL-Win64`로 설정합니다.
iii. `${OpenSSL의 설치 경로}\bin`를  Windows 시스템 환경 변수 Path에 설정합니다.

#### 4. Poco 설치

[Poco 1.9.4](https://github.com/pocoproject/poco/releases/tag/poco-1.9.4-release) 버전을 다운로드하여 컴파일한 후 해당 라이브러리 및 헤더 파일을 설치합니다.
i. Windows 명령 라인을 열어 Poco 소스 코드 디렉터리에서 cd 명령어를 사용하여 `mkdir examplefolder `(examplefolder를 사용자 정의 폴더 이름으로 변경) 명령을 실행하고 폴더를 생성합니다.
ii. Windows 명령 라인에서 `cd examplefolder `(examplefolder는 사용자 정의 폴더 이름) 명령을 실행한 후 `cmake ..` 명령어를 실행합니다.
iii. visual studio 2017로 솔루션을 열고 컴파일을 진행합니다.

#### 5. Boost 설치 

[Boost 공식 홈페이지](https://www.boost.org/)에서 Boost 소스 코드를 다운로드합니다.
i. Windows 명령 라인을 열어 Boost 소스 코드 디렉터리에서 cd 명령어를 사용합니다.
ii. Boost 소스 코드 디렉터리에서 bootstrap 명령어를 실행합니다.
iii. Windows 명령 라인에서 b2 컴파일 명령어를 실행합니다.

#### 주의사항
visual studio 2017에는 4가지 코드 생성 방식이 있으며 boost가 컴파일 시 서로 다른 명령어와 대응됩니다.

b2.exe 컴파일 명령어 모드는 다음과 같습니다.

|link	|runtime-link|	컴파일 모드|	멀티 스레드 유형|
|---------|---------|---------|---------|
|static|	static|	release	|MT|
|static|	static|	debug|	MTd|
|static	|shared|	release	|MD|
|static|	shared	|debug	|MDd|

예를 들어, 32비트 멀티 스레드 유형은 MD이며 명령어는 다음과 같습니다.
```shell
b2 variant=release link=static runtime-link=shared threading=multi address-model=32
```

#### 6. jsoncpp 설치

i. [jsoncpp 소스 코드](https://github.com/open-source-parsers/jsoncpp)를 다운로드합니다. Win32는 [낮은 버전](https://github.com/open-source-parsers/jsoncpp/tree/0.y.z)의 jsoncpp 선택을 권장합니다.
ii. Windows 명령 라인을 열어 jsoncpp 소스 코드 디렉터리에서 cd 명령어를 사용하여 `mkdir examplefolder `(examplefolder를 사용자 정의 폴더 이름으로 변경) 명령을 실행하고 폴더를 생성합니다.
iii. Windows 명령 라인에서 `cd examplefolder`(examplefolder는 사용자 정의 폴더 이름) 명령을 실행한 후 `cmake .. ` 명령어를 실행합니다.
iv. visual studio 2017로 솔루션을 열고 컴파일을 진행합니다.
v. 컴파일 완료 후 컴파일로 얻은 jsoncpp.lib을 COS CPP SDK 설치 디렉터리에 있는 lib 폴더에 복사합니다.

#### 7. COS CPP SDK 컴파일 

i. [XML Windows C++ SDK 소스코드](https://github.com/tencentyun/cos-cpp-sdk-v5/tree/windows_dev)를 다운로드하여 개발 환경에 통합하고 컴파일을 진행합니다.
ii. Windows 명령 라인을 열어 C++ SDK 소스 코드 디렉터리에서 cd 명령어를 사용하여 `mkdir examplefolder `(examplefolder를 사용자 정의 폴더 이름으로 변경) 명령을 실행하고 폴더를 생성합니다.
iii. `${cos-cpp-sdk}`설치 디렉터리의 CMakeLists.txt 파일을 수정합니다. 수정 예시는 다음과 같습니다.
```cpp
# include directories
INCLUDE_DIRECTORIES(./include)
INCLUDE_DIRECTORIES(${OpenSSL 설치 디렉터리}/include)
INCLUDE_DIRECTORIES(${Boost 설치 디렉터리}/boost)
INCLUDE_DIRECTORIES(${Poco 설치 디렉터리}/NetSSL_OpenSSL/include)
INCLUDE_DIRECTORIES(${Poco 설치 디렉터리}/Foundation/include)
INCLUDE_DIRECTORIES(${Poco 설치 디렉터리}/Net/include)
INCLUDE_DIRECTORIES(${Poco 설치 디렉터리}/Crypto/include)
INCLUDE_DIRECTORIES(${Poco 설치 디렉터리}/Util/include)

# lib directories
link_directories(${OpenSSL 설치 디렉터리}/lib)
link_directories(${Poco 컴파일 디렉터리}/lib/Release)
link_directories(./lib)
link_directories(${Boost 설치 디렉터리}/stage/lib)
```
iv. Windows 명령 라인에서 `cd examplefolder`(examplefolder는 사용자 정의 폴더 이름) 명령을 실행한 후 `cmake ..` 명령어를 실행합니다.
v. visual studio 2017로 솔루션을 열고 컴파일을 진행합니다.

### Mac 버전 SDK 설치

#### 1. CMake 툴 설치
```shell
brew install cmake
```

#### 2. Boost 라이브러리 및 헤더 파일 설치

```shell
wget http://sourceforge.net/projects/boost/files/boost/1.54.0/boost_1_54_0.tar.gz
tar -xzvf boost_1_54_0.tar.gz
cd boost_1_54_0
./bootstrap.sh --prefix=/usr/local
./b2 install --with=all
#Boost 라이브러리를 /usr/local/lib 디렉터리에 설치
```

#### 3. OpenSSL 설치

[OpenSSL 공식 홈페이지](https://www.openssl.org/)에서 openssl-1.1.1d.tar.gz 소스 코드를 다운로드하여 컴파일을 진행합니다.

```shell
tar -zxvf openssl-1.1.1d.tar.gz
cd openssl-1.1.1d/
./config --prefix=/usr/local 
make 
make install
#openssl 라이브러리를 /usr/local/ 디렉터리에 설치
```

#### 4. Poco 설치

[Poco 1.9.4](https://github.com/pocoproject/poco/releases/tag/poco-1.9.4-release) 버전을 다운로드하여 컴파일한 후 해당 라이브러리 및 헤더 파일을 설치합니다.

```shell
cd Poco/ 
./configure --omit=Data/ODBC, Data/MySQL
mkdir examplefolder #(examplefolder를 사용자 정의 폴더 이름으로 변경)
cd examplefolder
cmake .. 
make
```

#### 5. COS CPP SDK 컴파일
i. [XML Mac C++ SDK 소스 코드](https://github.com/tencentyun/cos-cpp-sdk-v5)를 다운로드하여 개발 환경에 통합합니다.
ii. `${cos-cpp-sdk}`설치 디렉터리의 CMakeLists.txt 파일을 수정합니다. 수정 예시는 다음과 같습니다.
```cpp
# include directories
INCLUDE_DIRECTORIES(./include)
INCLUDE_DIRECTORIES(/usr/local/include)
INCLUDE_DIRECTORIES(${Poco 설치 디렉터리}/NetSSL_OpenSSL/include)
INCLUDE_DIRECTORIES(${Poco 설치 디렉터리}/Foundation/include)
INCLUDE_DIRECTORIES(${Poco 설치 디렉터리}/Net/include)
INCLUDE_DIRECTORIES(${Poco 설치 디렉터리}/Crypto/include)
INCLUDE_DIRECTORIES(${Poco 설치 디렉터리}/Util/include)

# lib directories
link_directories(/usr/local/lib)
link_directories(${Poco 컴파일 디렉터리}/lib/Release)
link_directories(./lib)
```
iii. 다음 명령어를 실행하십시오.
```shell
cd ${cos-cpp-sdk} 
mkdir build 
cd build 
cmake .. 
make
```

## 사용하기

COS C++ SDK를 사용한 초기화 클라이언트, 버킷 생성, 버킷 리스트 조회, 객체 업로드, 객체 리스트 조회, 객체 다운로드, 객체 삭제 등의 기본 작업 방법은 아래와 같습니다.

>? 본 문서에 나오는 SecretId, SecretKey, Bucket 등의 명칭의 의미 및 획득 방법은 [COS 용어 정보](https://intl.cloud.tencent.com/document/product/436/7751)를 참고하십시오.
>

### 초기화

구성 파일의 각 필드 소개:

```
// V5.4.3 이전 버전의 SDK 구성 파일은 "AccessKey"를 사용하십시오.
"SecretId":"SECRETID", 
"SecretKey":"SECRETKEY",



// COS 리전, 리전 및 약칭은 https://cloud.tencent.com/document/product/436/6224 참고 
"Region":"Region",



// 서명 타임아웃 시간, 단위: s    
"SignExpiredTime":360, 



// connect 타임아웃 시간, 단위: ms
"ConnectTimeoutInms":6000,



// http 타임아웃 시간, 단위: ms 
"HttpTimeoutInms":60000,  



// 파일 멀티파트 업로드 크기, 범위: 1MB~5GB, 기본값: 1MB  
"UploadPartSize":1048576,  



// 단일 파일 멀티파트 업로드 스레드 풀 크기       
"UploadThreadPoolSize":5, 



// 파일 샤드 다운로드 크기   
"DownloadSliceSize":4194304, 



// 단일 파일 다운로드 스레드 풀 크기 
"DownloadThreadPoolSize":5,   



// 비동기화 업로드/다운로드 스레드 풀 크기 
"AsynThreadPoolSize":2, 



// 로그 출력 유형. 0: 출력하지 않음, 1: 화면에 출력, 2: syslog에 출력   
"LogoutType":1,       



// 로그 레벨. 1: ERR, 2: WARN, 3: INFO, 4: DBG     
"LogLevel":3,                 
```

### 사용자 정의 도메인으로 COS 액세스 */

config.json에 아래 설정을 추가하십시오.

```cpp
"IsDomainSameToHost":true,
"DestDomain":"mydomain.com",
```

### 임시 키를 사용한 COS 액세스

```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"
int main(int argc, char *argv[]) {
    qcloud_cos::CosConfig config("./config.json");
    // 임시 키 설정
    config.SetTmpToken("xxx");
    qcloud_cos::CosAPI cos(config);
}
```

###버킷 생성하기

```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"



int main(int argc, char *argv[]) {
    // 1. 구성 파일 경로를 지정하고 CosConfig 초기화
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. 버킷 생성 요청의 구조
    std::string bucket_name = "examplebucket-1250000000"; // Bucket 이름
    qcloud_cos::PutBucketReq req(bucket_name);
    qcloud_cos::PutBucketResp resp;
    
    // 3. 버킷 생성 인터페이스 호출
    qcloud_cos::CosResult result = cos.PutBucket(req, &resp);
    
    // 4. 호출 결과 처리
    if (result.IsSucc()) {
        // 생성 성공
    } else {
        // 버킷 생성 실패 시, CosResult의 멤버 함수를 호출하여 오류 정보를 출력할 수 있음(예: requestID 등)
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

### 버킷 리스트 조회

```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"



int main(int argc, char *argv[]) {
    // 1. 구성 파일 경로를 지정하고 CosConfig 초기화
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. 버킷 리스트 조회 요청의 구조
    qcloud_cos::GetServiceReq req;
    qcloud_cos::GetServiceResp resp;
    qcloud_cos::CosResult result = cos.GetService(req, &resp);
    
    // 3. 응답 정보 획득
    const qcloud_cos::Owner& owner = resp.GetOwner();
    const std::vector<qcloud_cos::Bucket>& buckets = resp.GetBuckets();
    std::cout << "owner.m_id=" << owner.m_id << ", owner.display_name=" << owner.m_display_name << std::endl;
    
    for (std::vector<qcloud_cos::Bucket>::const_iterator itr = buckets.begin(); itr != buckets.end(); ++itr) {
        const qcloud_cos::Bucket& bucket = *itr;
        std::cout << "Bucket name=" << bucket.m_name << ", location="
            << bucket.m_location << ", create_date=" << bucket.m_create_date << std::endl;
    }
    
    // 4. 호출 결과 처리
    if (result.IsSucc()) {
        // 버킷 리스트 조회 성공
    } else {
        // 버킷 리스트 조회 실패 시, CosResult의 멤버 함수를 호출하여 오류 정보를 출력할 수 있음(예: requestID 등)
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

### 객체 업로드

```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"



int main(int argc, char *argv[]) {
    // 1. 구성 파일 경로를 지정하고 CosConfig 초기화
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. 파일 업로드 요청의 구조
    std::string bucket_name = "examplebucket-1250000000"; // 업로드한 타깃 Bucket 이름
    std::string object_name = "exampleobject"; //exampleobject는 객체 키(Key)이며 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg에서 객체 키는 doc/pic.jpg임
    // request의 구조 함수에 로컬 파일 경로 입력 필요
    qcloud_cos::PutObjectByFileReq req(bucket_name, object_name, "/path/to/local/file");
    req.SetXCosStorageClass("STANDARD_IA")； // Set 방법을 호출하여 메타데이터 등을 설정
    qcloud_cos::PutObjectByFileResp resp;
    
    // 3. 파일 업로드 인터페이스 호출
    qcloud_cos::CosResult result = cos.PutObject(req, &resp);
    
    // 4. 호출 결과 처리
    if (result.IsSucc()) {
        // 파일 업로드 완료
    } else {
        // 파일 업로드 실패 시, CosResult의 멤버 함수를 호출하여 오류 정보를 출력할 수 있음(예: requestID 등)
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

### 객체 리스트 조회

```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"



int main(int argc, char *argv[]) {
    // 1. 구성 파일 경로를 지정하고 CosConfig 초기화
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. 객체 리스트 조회 요청의 구조
    std::string bucket_name = "examplebucket-1250000000"; // 업로드한 타깃 버킷 이름
    qcloud_cos::GetBucketReq req(bucket_name);
    qcloud_cos::GetBucketResp resp;
    qcloud_cos::CosResult result = cos.GetBucket(req, &resp);   
    
    std::vector<qcloud_cos::Content> cotents = resp.GetContents();
    for (std::vector<qcloud_cos::Content>::const_iterator itr = cotents.begin(); itr != cotents.end(); ++itr) {
    	const qcloud_cos::Content& content = *itr;
        std::cout << "key name=" << content.m_key << ", lastmodified ="
            << content.m_last_modified << ", size=" << content.m_size << std::endl;
    }
    
    // 3. 호출 결과 처리
    if (result.IsSucc()) {
        // 객체 리스트 조회 성공
    } else {
        // 객체 리스트 조회 실패 시, CosResult의 멤버 함수를 호출하여 오류 정보를 출력할 수 있음(예: requestID 등)
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

### 객체 다운로드

```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"



int main(int argc, char *argv[]) {
    // 1. 구성 파일 경로를 지정하고 CosConfig 초기화
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. 객체 다운로드 요청의 구조
    std::string bucket_name = "examplebucket-1250000000"; // 업로드한 타깃 Bucket 이름
    std::string object_name = "exampleobject"; // exampleobject는 객체 키(Key)이며 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg에서 객체 키는 doc/pic.jpg임
    std::string local_path = "/tmp/exampleobject";
    // request는 appid, bucketname, object, 로컬 경로를 제공해야 함(파일 이름 포함)
    qcloud_cos::GetObjectByFileReq req(bucket_name, object_name, local_path);
    qcloud_cos::GetObjectByFileResp resp;
    
    // 3. 객체 다운로드 인터페이스 호출
    qcloud_cos::CosResult result = cos.GetObject(req, &resp);
    
    // 4. 호출 결과 처리
    if (result.IsSucc()) {
        // 파일 다운로드 성공
    } else {
        // 파일 다운로드 실패 시, CosResult의 멤버 함수를 호출하여 오류 정보를 출력할 수 있음(예: requestID 등)
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

### 객체 삭제

```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"



int main(int argc, char *argv[]) {
    // 1. 구성 파일 경로를 지정하고 CosConfig 초기화
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. 객체 삭제 요청의 구조
    std::string bucket_name = "examplebucket-1250000000"; // 업로드한 타깃 버킷 이름
    std::string object_name = "exampleobject"; // exampleobject는 객체 키(Key)이며 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg에서 객체 키는 doc/pic.jpg임
    // 3. 객체 삭제 인터페이스 호출
	qcloud_cos::DeleteObjectReq req(bucket_name, object_name);
	qcloud_cos::DeleteObjectResp resp;
	qcloud_cos::CosResult result = cos.DeleteObject(req, &resp); 
    
    // 4. 호출 결과 처리
    if (result.IsSucc()) {
        // 객체 삭제 성공
    } else {
        // 객체 삭제 실패 시, CosResult의 멤버 함수를 호출하여 오류 정보를 출력할 수 있음(예: requestID 등)
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
