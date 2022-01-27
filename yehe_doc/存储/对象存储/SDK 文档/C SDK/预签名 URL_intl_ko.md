## 소개

C SDK는 사전 서명된 URL 요청을 가져오는 인터페이스를 제공합니다. 자세한 내용은 본 문서의 설명과 예시를 참고하십시오.

>?
> - 사용자는 임시 키를 사용하여 사전 서명을 생성하고, 임시 승인을 통해 사전 서명 업로드 및 다운로드 요청의 보안성을 강화할 것을 권장합니다. 임시 키 신청 시, [최소 권한 가이드](https://intl.cloud.tencent.com/document/product/436/32972)를 준수하여 타깃 버킷이나 객체 이외의 리소스가 유출되지 않도록 하시기 바랍니다.
> - 사전 서명 생성을 위해 영구 키를 사용해야 하는 경우, 리스크 방지를 위해 영구 키 권한을 업로드 또는 다운로드 작업으로 제한할 것을 권장합니다.
> 

## 사전 서명된 URL 요청 가져오기 

### 사전 서명된 URL 요청 생성

#### 기능 설명

이 인터페이스는 사전 서명된 URL 요청 생성에 사용됩니다.

#### 메소드 프로토타입

```cpp
int cos_gen_presigned_url(const cos_request_options_t *options,
                          const cos_string_t *bucket, 
                          const cos_string_t *object,
                          const int64_t expire,
                          http_method_e method,
                          cos_string_t *presigned_url);
```

#### 매개변수 설명

| 매개변수 이름      | 매개변수 설명                                                     | 유형   |
| ------------- | ------------------------------------------------------------ | ------ |
| options       | COS 요청 옵션                                                 | Struct |
| bucket        | 버킷 이름. 형식: BucketName-APPID. | String |
| object        | Object 이름                                                  | String |
| expire        | 서명 유효 시간. 단위: 초                                       | Int    |
| method        | HTTP 요청 방법 열거 유형. 각각 HTTP_GET, HTTP_HEAD, HTTP_PUT, HTTP_POST, HTTP_DELETE. | Enum   |
| presigned_url | 생성된 사전 서명된 URL 요청                                         | String |

#### 반환 결과 설명

| 반환 결과 | 설명   | 유형 |
| -------- | ------ | ---- |
| code     | 오류 코드 | Int  |

#### 사전 서명 요청 예시

options 매개변수에서 영구 키 또는 임시 키를 설정하여 사전 서명된 URL을 얻을 수 있습니다.

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_string_t presigned_url;

//create memory pool
cos_pool_create(&p, NULL);

//init request options
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
init_test_config(options->config, is_cname);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
/* sts_token 설정으로 임시 키를 사용할 수 있습니다. 임시 키 사용 시 access_key_id와 access_key_secret은 모두 해당 임시 키의 SecretId와 SecretKey로 설정해야 합니다. */
//cos_str_set(&options->config->sts_token, "MyTokenString");
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);
cos_str_set(&object, TEST_OBJECT_NAME);

//generate presigned URL
cos_gen_presigned_url(options, &bucket, &object, 300, HTTP_GET, &presigned_url);
printf("presigned url: %s\n", presigned_url.data);

//destroy memory pool
cos_pool_destroy(p); 
```

## 사전 서명된 URL 요청 안전하게 가져오기 

#### 사전 서명된 URL 요청 안전하게 생성

#### 기능 설명

이 인터페이스는 사전 서명된 URL 요청을 안전하게 생성하는 데 사용됩니다.

#### 메소드 프로토타입

```cpp
int cos_gen_presigned_url_safe(const cos_request_options_t *options,
                          const cos_string_t *bucket, 
                          const cos_string_t *object,
                          const int64_t expire,
                          http_method_e method,
                          cos_table_t *headers,
                          cos_table_t *params,
                          int sign_host,
                          cos_string_t *presigned_url);
```

#### 매개변수 설명

| 매개변수 이름      | 매개변수 설명                                                     | 유형   |
| ------------- | ------------------------------------------------------------ | ------ |
| options       | COS 요청 옵션                                                 | Struct |
| bucket        | 버킷 이름. 형식: BucketName-APPID. | String |
| object        | Object 이름                                                  | String |
| expire        | 서명 유효 시간. 단위: 초                                       | Int    |
| method        | HTTP 요청 방법 열거 유형. 각각 HTTP_GET, HTTP_HEAD, HTTP_PUT, HTTP_POST, HTTP_DELETE. | Enum   |
| headers       | COS에서 부가 헤더 필드 요청                                             | Struct |
| params        | COS에서 작업 매개변수 요청                                             | Struct |
| sign_host     | host 헤더 필드 서명 여부. 보안을 위해 활성화 권장.                    | Int    |
| presigned_url | 생성된 사전 서명된 URL 요청                                         | String |

#### 반환 결과 설명

| 반환 결과 | 설명   | 유형 |
| -------- | ------ | ---- |
| code     | 오류 코드 | Int  |

#### 보안 사전 서명 요청 예시

options 매개변수에서 영구 키 또는 임시 키를 설정하여 사전 서명된 URL을 얻을 수 있습니다.

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_string_t presigned_url;
cos_table_t *params;
cos_table_t *headers;

//create memory pool
cos_pool_create(&p, NULL);

//init request options
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
init_test_config(options->config, is_cname);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
/* sts_token 설정으로 임시 키를 사용할 수 있습니다. 임시 키 사용 시 access_key_id와 access_key_secret은 모두 해당 임시 키의 SecretId와 SecretKey로 설정해야 합니다. */
//cos_str_set(&options->config->sts_token, "MyTokenString");
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);
cos_str_set(&object, TEST_OBJECT_NAME);

// 자신의 params 및 headers 추가
params = cos_table_make(p, 0);
headers = cos_table_make(p, 0);

// sign_host를 1로 설정하여 host 헤더 필드가 서명 리스트에 강제로 추가되도록 하여 승인되지 않은 액세스를 방지할 것을 강력히 권장합니다.
cos_gen_presigned_url_safe(options, &bucket, &object, 300, HTTP_GET, headers, params, 1, &presigned_url);
printf("presigned_url_safe: %s\n", presigned_url.data);

//destroy memory pool
cos_pool_destroy(p); 
```
