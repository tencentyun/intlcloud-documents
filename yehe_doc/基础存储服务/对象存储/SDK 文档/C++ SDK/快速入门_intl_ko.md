## 다운로드 및 설치

#### 관련 리소스

- COS의 XML C++ SDK 소스 코드 다운로드 주소는 다음과 같습니다.
Linux 버전/Windows 버전/macOS 버전: [ XML Linux C++ SDK](https://github.com/tencentyun/cos-cpp-sdk-v5).
- SDK 고속 다운로드 주소: [XML C++ SDK](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-cpp-sdk-v5/latest/cos-cpp-sdk-v5.zip). 
- 예시 Demo 다운로드 주소: [COS XML C++ SDK 예시](https://github.com/tencentyun/cos-cpp-sdk-v5/blob/master/demo/cos_demo.cpp).
- SDK 로그 업데이트는 [ChangeLog](https://github.com/tencentyun/cos-cpp-sdk-v5/blob/master/CHANGELOG.md)를 참고하십시오.

>? XML 버전 SDK 사용 중 함수 또는 메소드가 존재하지 않는 등의 오류 발생 시, XML 버전 SDK를 최신 버전으로 업그레이드한 후 재시도하십시오.
>


## 컴파일 완료(추천)

[XML C++ SDK 소스 코드](https://github.com/tencentyun/cos-cpp-sdk-v5)를 다운로드하고, libs 디렉터리에 컴파일 완료된 라이브러리가 있으면 직접 사용할 수 있습니다. 사용 시, 해당 시스템 버전을 선택하시기 바랍니다. 

```shell
libs/linux/libcossdk.a #linux의 정적 라이브러리
libs/linux/libcossdk-shared.so #linux 동적 라이브러리
libs/Win32/cossdk.lib #Win32 라이브러리
libs/x64/cossdk.lib #Win64 라이브러리
libs/macOS/libcossdk.a #macOS 정적 라이브러리
libs/macOS/libcossdk-shared.dylib #macOS 동적 라이브러리
```

>? 사용 시, 해당 시스템의 라이브러리 파일과 SDK include 헤더 파일을 프로그램으로 복사하십시오.

Third-party 디렉터리에 3rd party 종속 라이브러리가 있는 경우는 다음과 같습니다. 

```shell
third_party/lib/linux/poco/ #linux에 종속된 Poco 동적 라이브러리
third_party/lib/Win32/openssl/ #Win32 종속된 openssl 라이브러리
third_party/lib/Win32/poco/ #Win32 종속된 poco 라이브러리
third_party/lib/x64/openssl/ #Win64 종속된 openssl 라이브러리
third_party/lib/x64/poco/ #Win64 종속된 poco 라이브러리
third_party/lib/macOS/poco/ #macOS 종속된 poco 라이브러리
```

>? 사용 시, 해당 시스템의 종속 라이브러리를 프로그램으로 복사하십시오.


## 수동 컴파일


### 컴파일 옵션

루트 디렉터리의 CMakeLists.txt 파일은 다음과 같은 컴파일 옵션을 설정할 수 있습니다.

```shell
option(BUILD_UNITTEST "Build unittest" OFF) #유닛 테스트 컴파일 설정
option(BUILD_DEMO "Build demo" ON) #demo 테스트 코드 컴파일 설정
option(BUILD_SHARED_LIB "Build shared library" OFF) #동적 라이브러리 컴파일 설정
```

### 종속 라이브러리

종속 동적 라이브러리: poco, openssl, crypto.


### Linux버전 SDK 컴파일

1. 컴파일 툴 및 종속 라이브러리 설치
```shell
yum install -y gcc gcc-c++ make cmake openssl
#cmake 버전 2.8 이상
```
2. SDK 컴파일 
[XML C++ SDK 소스 코드](https://github.com/tencentyun/cos-cpp-sdk-v5)를 개발 환경으로 다운로드하고 다음 명령어를 실행합니다.
```shell
cd ${cos-cpp-sdk} 
mkdir -p build 
cd build 
cmake .. 
make
```
3. Poco 라이브러리 설치
```shell
cd ${cos-cpp-sdk} 
sh install-libpoco.sh
```
>? 해당 스크립트는 Poco 동적 라이브러리를 /usr/lib64 디렉터리에 설치하고, 소프트 링크를 생성합니다. 프로덕션 환경에서 COS SDK를 사용하려는 경우에도 프로덕션 환경에 Poco 라이브러리를 설치해야 합니다.
>
4. 테스트 Demo 
>? 테스트 demo가 필요하지 않은 경우, 이 단계를 건너 뛰십시오.
>
```shell
cd ${cos-cpp-sdk} 
vim demo/cos_demo.cpp  #demo의 버킷 이름 및 테스트 코드 수정
vim CMakeLists.txt #루트 디렉터리 내 CMakeLists.txt의 BUILD_DEMO를 ON으로 수정하고, 컴파일 demo 활성화
cd build && make #컴파일demo
ls bin/cos_demo #생성된 실행 가능 파일은 bin 디렉터리에 있음
vim bin/config.json #키 및 단지 수정
cd bin && ./cos_demo #demo 실행
```
5. SDK 사용 
컴파일하여 생성된 라이브러리 파일은 build/lib 디렉터리에 있으며 정적 라이브러리 이름은 `libcossdk.a`, 동적 라이브러리 이름은 `libcossdk-shared.so`입니다. 사용 시, 라이브러리는 프로그램에 복사하고 include 디렉터리는 프로그램의 include 경로에 복사하십시오.


### Windows 버전 SDK 컴파일

1. visual studio 2017 설치
visual studio 2017 개발 환경 설치
2. CMake 툴 설치
[CMake 공식 홈페이지](https://cmake.org/download/)에서 Windows버전 CMake 컴파일 툴을 다운로드하고 `${CMake의 설치 경로}\bin`을 Windows 시스템 환경 변수 Path에 설정합니다.
3. SDK 컴파일 
 i. [XML Windows C++ SDK 소스 코드](https://github.com/tencentyun/cos-cpp-sdk-v5/tree/windows_dev)를 개발 환경에 다운로드합니다.
 ii. Windows 명령 라인을 열어 C++ SDK 소스 코드 디렉터리에 cd 명령어를 사용하여 다음 명령을 실행합니다.
```shell
mkdir build
cd build
cmake .. #Win32 makefile 생성
cmake -G "Visual Studio 15 Win64" .. #Win64 makefile 생성
```
 iii. visual studio 2017로 솔루션 리소스 관리자를 열고 컴파일을 진행합니다.
4. 테스트 demo <br>
>? 테스트 demo가 필요하지 않은 경우, 이 단계를 건너 뛰십시오.
>
demo 코드를 수정 및 컴파일하여 생성된 cos_demo.exe 파일은 bin 디렉터리에 있으며 bin/config.json을 수정하여 cos_demo.exe를 실행할 수 있습니다.
5. SDK 사용 
컴파일하여 생성된 라이브러리 파일은 build/Release 디렉터리에 있으며, 정적 라이브러리 이름은`cossdk.lib`입니다. 사용 시, 라이브러리는 프로그램에 복사하고 include 디렉터리는 프로그램의 include 경로에 복사하십시오.

### Mac 버전 SDK 컴파일

1. 컴파일 툴 및 종속 라이브러리 설치
```shell
brew install gcc make cmake openssl
```
2. SDK 컴파일 
[XML C++ SDK 소스 코드](https://github.com/tencentyun/cos-cpp-sdk-v5)를 개발 환경으로 다운로드하고 다음 명령어를 실행합니다.
```shell
cd ${cos-cpp-sdk} 
mkdir -p build 
cd build 
cmake .. 
make
```
3. Poco 라이브러리 설치
Poco 라이브러리는 third_party/lib/macOS/poco 디렉터리에 있습니다. 직접 설치해 주십시오.
4. 테스트 Demo 
>?테스트 demo가 필요하지 않은 경우, 이 단계를 건너 뛰십시오.
>
demo 코드를 수정 및 컴파일하여 생성된 cos_demo는 bin 디렉터리에 있으며 bin/config.json을 수정하여 cos_demo를 실행할 수 있습니다.
5. SDK 사용 
컴파일하여 생성된 라이브러리 파일은 build/lib 디렉터리에 있으며 정적 라이브러리 이름은 `libcossdk.a`, 동적 라이브러리 이름은 `libcossdk-shared.dylib`입니다. 사용 시, 라이브러리는 프로그램에 복사하고, include 디렉터리는 include 경로에 복사하십시오.

## 사용하기

COS C++ SDK를 사용한 클라이언트 초기화, 버킷 생성, 버킷 리스트 조회, 객체 업로드, 객체 리스트 조회, 객체 다운로드, 객체 삭제 등의 기본 작업 방법은 아래와 같습니다.

>? 본 문서에 나오는 SecretId, SecretKey, Bucket 등의 이름의 의미 및 획득 방법은 [COS 용어 정보](https://intl.cloud.tencent.com/document/product/436/7751)를 참고하십시오.
>

### 초기화

구성 파일의 각 필드 소개:

```
"SecretId":"********************************",  // V5.4.3 이전 버전은 AccessKey 사용
"SecretKey":"*******************************",
"Region":"ap-guangzhou",                // COS리전은 정확해야하며, 리전 및 약칭은 https://cloud.tencent.com/document/product/436/6224를 참고하십시오 
"SignExpiredTime":360,              // 서명 타임아웃 시간, 단위s
"ConnectTimeoutInms":6000,          // connect 타임아웃 시간, 단위ms
"ReceiveTimeoutInms":60000,         // recv 타임아웃 시간, 단위ms
"UploadPartSize":10485760,          // 파일 파트 업로드 크기, 1M-5G, 기본값은 10M
"UploadCopyPartSize":20971520,      // 복사 파일 파트 업로드 크기, 5M-5G, 기본값은 20M
"UploadThreadPoolSize":5,           // 단일 파일 멀티파트 업로드 스레드 풀 크기
"DownloadSliceSize":4194304,        // 파일 멀티파트 다운로드 크기
"DownloadThreadPoolSize":5,         // 단일 파일 다운로드 스레드 풀 크기
"AsynThreadPoolSize":2,             // 비동기화 업로드/다운로드 스레드 풀 크기
"LogoutType":1,                     // 로그 출력 유형, 0: 출력하지 않음, 1: 화면에 출력, 2: syslog에 출력
"LogLevel":3,                       // 로그 레벨:1: ERR, 2: WARN, 3: INFO, 4: DBG
"IsDomainSameToHost":false,         // 전용 host 사용 여부
"DestDomain":"",                    // 특정 host
"IsUseIntranet":false,              // 특정 ip와 포트 번호 사용 여부
"IntranetAddr":""                   // 특정 ip와 포트 번호, 예‘127.0.0.1:80’               
```

### 사용자 정의 도메인으로 COS 액세스

본인의 도메인을 사용하여 COS에 액세스할 경우, 우선 COS 콘솔에서 사용자 정의 도메인을 설정하십시오. 작업 가이드는 [사용자 정의 원본 서버 도메인 활성화](https://intl.cloud.tencent.com/document/product/436/31507)를 참고하십시오.

사용한 도메인이 mydomain.com이라고 가정하면 config.json에서 다음 설정을 추가해야 합니다.

```cpp
"IsDomainSameToHost":true,
"DestDomain":"mydomain.com",
```

### 임시 키를 사용한 COS 액세스

임시 키를 사용하여 COS에 액세스할 경우, 다음 코드를 참고하십시오.

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

### SDK 내부 로그를 사용자 정의 로그 파일로 출력합니다.

SDK 내부 로그를 사용자 정의 로그 파일 특히 Windows 시스템으로 출력할 경우, 다음 코드를 참고하십시오.

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

### 버킷 생성

```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"

int main(int argc, char *argv[]) {
    // 1. 구성 파일 경로 지정, CosConfig 초기화
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. 버킷 생성 요청 구성
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
    // 1. 구성 파일 경로 지정, CosConfig 초기화
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. 버킷 리스트 조회 요청 구성
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
    // 1. 구성 파일 경로 지정, CosConfig 초기화
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. 파일 업로드 요청 구성
    std::string bucket_name = "examplebucket-1250000000"; // 업로드한 타깃 Bucket 이름
    std::string object_name = "exampleobject"; //exampleobject는 객체 키(Key)이며 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg에서 객체 키는 doc/pic.jpg임
    // request의 생성자에 로컬 파일 경로 전달 필요
    qcloud_cos::PutObjectByFileReq req(bucket_name, object_name, "/path/to/local/file");
    req.SetXCosStorageClass("STANDARD_IA"); // Set 메소드를 호출하여 메타데이터 등을 설정
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
    // 1. 구성 파일 경로 지정, CosConfig 초기화
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. 객체 리스트 조회 요청 구성
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
    // 1. 구성 파일 경로 지정, CosConfig 초기화
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. 객체 다운로드 요청 구성
    std::string bucket_name = "examplebucket-1250000000"; // 업로드한 타깃 Bucket 이름
    std::string object_name = "exampleobject"; // exampleobject는 객체 키(Key)이며 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg에서 객체 키는 doc/pic.jpg임.
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
    // 1. 구성 파일 경로 지정, CosConfig 초기화
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. 객체 삭제 요청 구성
    std::string bucket_name = "examplebucket-1250000000"; // 업로드한 타깃 버킷 이름
    std::string object_name = "exampleobject"; // exampleobject는 객체 키(Key)이며 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg에서 객체 키는 doc/pic.jpg임.
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
