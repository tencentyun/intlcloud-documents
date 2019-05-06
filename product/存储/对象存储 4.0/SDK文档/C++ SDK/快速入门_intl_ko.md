## 개발 준비
### 적용 시스템
해당 SDK는 현재 Linux 플랫폼에서만 사용할 수 있습니다.

### SDK 획득
COS 서비스의 XML C++ SDK 리소스 다운로드 주소: [XML C++ SDK 다운로드](https://github.com/tencentyun/cos-cpp-sdk-v5 "cos-cpp-sdk-v5 다운로드 주소").
Demo 예제 다운로드 주소: [XML C++ SDK Demo](https://github.com/tencentyun/cos-cpp-sdk-v5/blob/master/demo/cos_demo.cpp "Cpp SDK 참고").

### 환경 준비
**의존 라이브러리:** jsoncpp boost_system boost_thread Poco(lib 폴더에 있음)
**의존 라이브러리:** ssl crypto rt z(설치 필요).
SDK는 JsonCpp 라이브러리 및 헤더 파일을 제공합니다. 직접 설치하려면 다음 단계에서 설치된 라이브러리를 컴파일하고 SDK의 해당 라이브러리 및 헤더 파일을 교체하십시오. 위의 라이브러리가 이미 시스템에 설치되어 있는 경우, SDK의 해당 라이브러리 및 헤더 파일을 삭제할 수도 있습니다. 구체 설치 절차는 다음과 같습니다.

#### 1. CMake 도구를 설치합니다.
```
yum install -y gcc gcc-c++ make automake
//gcc와 같은 필수 패키지를 설치합니다(설치된 경우 이 단계는 건너뜀)
yum install -y wget

//cmake 버전은 3.5 이상이어야 합니다
wget https://cmake.org/files/v3.5/cmake-3.5.2.tar.gz
tar -zxvf cmake-3.5.2.tar.gz
cd cmake-3.5.2
./bootstrap --prefix=/usr
gmake
gmake install
```

#### 2. Boost의 라이브러리 및 헤더 파일을 설치합니다.
```
wget http://sourceforge.net/projects/boost/files/boost/1.54.0/boost_1_54_0.tar.gz
tar -xzvf boost_1_54_0.tar.gz
cd boost_1_54_0
./bootstrap.sh --prefix=/usr/local
./b2 install --with=all
#Boost 라이브러리는 /usr/local/lib 디렉터리에 설치됩니다
```

#### 3. OpenSSL을 설치합니다.

```
yum install openssl openssl-devel
```

또는

```
wget https://www.openssl.org/source/openssl-1.0.1t.tar.gz  
tar -xzvf ./openssl-1.0.1t.tar.gz
cd openssl-1.0.1t/
./config --prefix=/usr/local/ssl --openssldir=/usr/local/ssl

cd /usr/local/
ln -s ssl openssl
echo "/usr/local/openssl/lib" >> /etc/ld.so.conf
ldconfig

# 헤더 파일/라이브러리 파일 검색 경로를 추가합니다(~/.bashrc에 입력 가능)
LIBRARY_PATH=/usr/local/ssl/lib/:$LIBRARY_PATH
CPLUS_INCLUDE_PATH=/usr/local/ssl/include/:$CPLUS_INCLUDE_PATH
```

#### 4. [Poco 공식 웹사이트](https://pocoproject.org/download.html)에서 Poco의 라이브러리 및 헤더 파일을 다운로드하여 설치하십시오(complete 버전 다운로드).
```
./configure --omit=Data/ODBC,Data/MySQL
make
make install
```

#### 5. 콘솔에서 APPID, SecretId, SecretKey를 획득합니다.
>**주의:**
SecretId, SecretKey, Bucket 등 이름의 의미 및 획득 방식은 [COS 용어집](/document/product/436/7751)을 참조하십시오.
>`CMakeList.txt` 파일을 수정하여 로컬 Boost 헤더 파일 경로를 지정하고 다음 구문을 수정할 수 있습니다.
```
SET(BOOST_HEADER_DIR "/root/boost_1_61_0")
```

### SDK 구성
직접 [SDK 획득](#sdk-.E8.8E.B7.E5.8F.96) 단계 GitHub에서 제공되는 소스 코드를 다운로드하여 사용자의 개발 환경에 통합합니다. 다음의 명령을 실행하십시오.
``` bash
cd ${cos-cpp-sdk}
mkdir -p build
cd build
cmake ..
make
```

cos_demo.cpp에서 일반적인 API의 예가 있습니다. 생성된 cos_demo는 직접 실행될 수 있으며 생성된 정적 라이브러리 이름은 libcossdk.a 입니다. 생성된 libcossdk.a를 자신의 프로젝트의 lib 경로에 넣고, include 디렉터리는 프로젝트의 include 경로에 복사합니다.

## 시작 가이드
### 초기화
```
"SecretId":"*********************************", // V5.4.3 버전 이전의 sdk 구성 파일은 "AccessKey"를 사용하십시오
"SecretKey":"********************************",
"Region":"cn-north",                
// COS 지역, 올바른지 확인하십시오
"SignExpiredTime":360,              
// 서명 타임아웃 시간, 단위: s
"ConnectTimeoutInms":6000,          
// connect 타임아웃 시간, 단위: ms
"HttpTimeoutInms":60000,            
// http 타임아웃 시간, 단위: ms
"UploadPartSize":1048576,           
// 업로드 파일 파트 크기, 범위 1MB~5GB, 기본값은 1
"UploadThreadPoolSize":5,           
// 단일 파일 멀티파트 업로드 스레드 풀 크기
"DownloadSliceSize":4194304,        
// 다운로드 파일 파트 크기
"DownloadThreadPoolSize":5,         
// 단일 파일 다운로드 스레드 풀 크기
"AsynThreadPoolSize":2,             
// 비동기화 업로드 및 다운로드 스레드 풀 크기
"LogoutType":1,                     
// 로그 출력 유형, 0: 출력 안 함, 1: 스크린으로 출력, 2: syslog로 출력
"LogLevel":3                     
// 로그 렙레, 1: ERR, 2: WARN, 3: INFO, 4: DBG
```
### 버킷 생성
```
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"

int main(int argc, char *argv[]) {
    // 1. 구성 파일 경로를 지정하여 CosConfig를 초기화합니다
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);

    // 2. 버킷 생성 요청을 만듭니다
    std::string bucket_name = "cpp_sdk_v5-123456789"; // 버킷 이름
    qcloud_cos::PutBucketReq req(bucket_name);
    qcloud_cos::PutBucketResp resp;

    // 3. 버킷 생성 인터페이스를 호출합니다
    qcloud_cos::CosResult result = cos.PutBucket(req, &resp);

    // 4. 호출 결과를 처리합니다
    if (result.IsSucc()) {
        // 생성 성공
    } else {
        // 버킷 생성에 실패하면, CosResult의 멤버 함수를 호출하여 requestID 등의 오류 정보를 출력할 수 있습니다.
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

### 파일 업로드
```
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"

int main(int argc, char *argv[]) {
    // 1. 구성 파일 경로를 지정하여 CosConfig를 초기화합니다
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);

    // 2. 파일 업로드 요청 구성
    std::string bucket_name = "cpp_sdk_v5-123456789"; // 업로드한 대상 버킷 이름
    std::string object_name = "object_name"; //object_name은 객체 키(Key)이며, 버킷에서 객체의 유일한 식별자입니다. 예를 들어, 객체의 액세스 도메인 이름 bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg 중, 객체 키는 doc1/pic1.jpg입니다.
    // request의 구조 함수에서 로컬 파일 경로의 전송이 필요합니다.
    qcloud_cos::PutObjectByFileReq req(bucket_name, object_name, "/path/to/local/file");
    req.SetXCosStorageClass("STANDARD_IA")； // Set 방법을 호출하여 메타데이터 등을 설정합니다
    qcloud_cos::PutObjectByFileResp resp;

    // 3. 파일 업로드 API를 호출합니다
    qcloud_cos::CosResult result = cos.PutObject(req, &resp);

    // 4. 호출 결과를 처리합니다
    if (result.IsSucc()) {
        // 파일 업로드 성공
    } else {
        // 파일 업로드 실패, CosResult의 멤버 함수를 호출하여 requestID 등의 오류 정보를 출력할 수 있습니다
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

### 파일 다운로드
```
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"

int main(int argc, char *argv[]) {
    // 1. 구성 파일 경로를 지정하여 CosConfig를 초기화합니다
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);

    // 2. 버킷 생성 요청을 만듭니다
    std::string bucket_name = "cpp_sdk_v5-123456789"; // 업로드한 대상 버킷 이름
    std::string object_name = "object_name"; //object_name은 객체 키(Key)이며, 버킷에서 객체의 유일한 식별자입니다. 예를 들어, 객체의 액세스 도메인 이름 bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg 중, 객체 키는 doc1/pic1.jpg입니다.
    std::string local_path = "/tmp/object_name";
    // 매개변수 appid, bucketname, object 및 로컬 경로(파일 이름 포함)가 요청에 필요해야 합니다.
    qcloud_cos::GetObjectByFileReq req(bucket_name, object_name, local_path);
    qcloud_cos::GetObjectByFileResp resp;

    // 3. 버킷 생성 인터페이스를 호출합니다
    qcloud_cos::CosResult result = cos.GetObject(req, &resp);

    // 4. 호출 결과를 처리합니다
    if (result.IsSucc()) {
        // 파일 다운로드 성공
    } else {
        // 파일 다운로드 실패, CosResult의 멤버 함수를 호출하여 requestID 등의 오류 정보를 출력할 수 있습니다
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
