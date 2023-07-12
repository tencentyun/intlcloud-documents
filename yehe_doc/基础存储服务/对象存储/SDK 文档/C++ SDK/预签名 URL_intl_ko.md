## 소개
C++ SDK는 서명을 생성하고 사전 서명된 URL을 가져오는 인터페이스를 제공합니다. 자세한 내용은 이 문서의 지침과 예시를 참고하십시오.

>?
> - 사용자는 임시 키를 사용하여 사전 서명을 생성하고, 임시 승인을 통해 사전 서명 업로드 및 다운로드 요청의 보안성을 강화할 것을 권장합니다. 임시 키 신청 시, [최소 권한의 원칙 관련 가이드](https://intl.cloud.tencent.com/document/product/436/32972)를 준수하여 타깃 버킷이나 객체 이외의 리소스가 유출되지 않도록 하시기 바랍니다.
> - 사전 서명 생성을 위해 영구 키를 사용해야 하는 경우, 리스크 방지를 위해 영구 키 권한을 업로드 또는 다운로드 작업으로 제한할 것을 권장합니다.
>



## 서명 생성

### 기능 설명

서명을 계산하고 생성하는 데 사용됩니다.

### 메소드 프로토타입1

```
static std::string Sign(const std::string& secret_id,
                        const std::string& secret_key,
                        const std::string& http_method,
                        const std::string& in_uri,
                        const std::map<std::string, std::string>& headers,
                        const std::map<std::string, std::string>& params);
```

#### 매개변수 설명 

| 매개변수 이름    | 매개변수 설명                                              | 유형                     |
| ----------- | ----------------------------------------------------- | ------------------------ |
| secret_id   | 실명 인증을 위한 개발자 소유 프로젝트 ID             | String                   |
| secret_key  | 개발자 소유 프로젝트 키                              | String                   |
| http_method | 전달될 때 대소문자를 구분하지 않는 POST/GET/HEAD/PUT 등 HTTP 메소드 | String                   |
| in_uri      | HTTP uri                                              | String                   |
| headers     | HTTP header의 키 값 쌍                                  | string |
| params      | HTTP params의 키 값 쌍                                  | string |

#### 반환 결과 설명

지정된 유효 기간(CosSysConfig에서 설정. 기본값: 60초) 내에서 사용할 수 있는 서명 문자열이 반환됩니다. 빈 문자열이 반환되면 서명 계산에 실패한 것입니다.

### 메소드 프로토타입 2

```
static std::string Sign(const std::string& secret_id,
                        const std::string& secret_key,
                        const std::string& http_method,
                        const std::string& in_uri,
                        const std::map<std::string, std::string>& headers,
                        const std::map<std::string, std::string>& params,
                        uint64_t start_time_in_s,
                        uint64_t end_time_in_s);
```

#### 매개변수 설명 

| 매개변수 이름        | 매개변수 설명                                             | 유형                      |
| --------------- | ---------------------------------------------------- | ------------------------- |
| secret_id       | 실명 인증을 위한 개발자 소유 프로젝트 ID            | String                    |
| secret_key      | 개발자 소유 프로젝트 키                             | String                    |
| http_method     | 전달될 때 대소문자를 구분하지 않는 POST/GET/HEAD/PUT 등 HTTP 메소드 | String                    |
| in_uri          | HTTP uri                                             | String                    |
| headers         | HTTP header의 키 값 쌍                                 | string|
| params          | HTTP params의 키 값 쌍                                 | string |
| start_time_in_s | 서명 유효 기간의 시작 시간                                   | uint64_t                  |
| end_time_in_s   | 서명 유효 기간의 종료 시간                                   | uint64_t                  |

#### 반환 결과 설명

지정된 유효 기간(CosSysConfig에서 설정. 기본값: 60초) 내에서 사용할 수 있는 서명 문자열이 반환됩니다. 빈 문자열이 반환되면 서명 계산에 실패한 것입니다.


## 사전 서명된 URL 요청 가져오기 

```go
std::string GeneratePresignedUrl(const GeneratePresignedUrlReq& req)
```

### 매개변수 설명

| 매개변수 | 매개변수 설명                                    |
| ---- | ------------------------------------------- |
| req  | GeneratePresignedUrlReq, GeneratePresignedUrl 작업에 대한 요청  |

HTTP_METHOD 열거 값 정의는 다음과 같습니다.

```
typedef enum {
	HTTP_HEAD,
    HTTP_GET,
    HTTP_PUT,
    HTTP_POST,
    HTTP_DELETE,
    HTTP_OPTIONS
} HTTP_METHOD;
```

## 사전 서명 요청에 대한 예시
CosConfig 클래스에 따라 영구 또는 임시 키를 설정하여 사전 서명 요청을 진행할 수 있습니다. 프로파일에 대한 자세한 내용은 [시작하기](https://intl.cloud.tencent.com/document/product/436/12301)를 참고하십시오.

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "exampleobject";

// 버킷 이름, 객체 키, HTTP 요청 메소드를 추가합니다.
qcloud_cos::GeneratePresignedUrlReq req(bucket_name, object_name, qcloud_cos::HTTP_GET);
std::string presigned_url = cos.GeneratePresignedUrl(req); 

```
