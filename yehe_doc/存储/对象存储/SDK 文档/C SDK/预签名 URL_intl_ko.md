## 소개

C SDK는 사전 서명된 URL 요청을 가져오는 인터페이스를 제공합니다. 자세한 내용은 본 문서의 설명과 예시를 참고하십시오.

>?
> - 사용자는 임시 키를 사용하여 사전 서명을 생성하고, 임시 승인을 통해 사전 서명 업로드 및 다운로드 요청의 보안성을 강화할 것을 권장합니다. 임시 키 신청 시, [최소 권한의 원칙 관련 가이드](https://intl.cloud.tencent.com/document/product/436/32972)를 준수하여 타깃 버킷이나 객체 이외의 리소스가 유출되지 않도록 하시기 바랍니다.
> - 사전 서명 생성을 위해 영구 키를 사용해야 하는 경우, 리스크 방지를 위해 영구 키 권한을 업로드 또는 다운로드 작업으로 제한할 것을 권장합니다.
> 

## 사전 서명된 URL 요청 가져오기 

#### 사전 서명된 URL 요청 생성

#### 기능 설명

이 인터페이스는 사전 서명된 URL 요청을 생성하는 데 사용됩니다.

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
| bucket        | 버킷 이름. 버킷의 이름 생성 포맷은 BucketName-APPID로 여기에 입력하는 버킷 이름은 반드시 해당 포맷을 따라야 함 | String |
| object        | Object 이름                                                  | String |
| expire        | 서명 유효 기간(초)                                       | Int    |
| method        | HTTP_GET, HTTP_HEAD, HTTP_PUT, HTTP_POST 및 HTTP_DELETE를 포함한 열거 유형의 HTTP 요청 메소드 | Enum   |
| presigned_url | 생성된 사전 서명된 URL 요청                                         | String |

#### 반환 결과 설명

| 반환 결과 | 설명   | 유형 |
| -------- | ------ | ---- |
| code     | 에러 코드 | Int  |

## 사전 서명 요청의 예시

options 매개변수에서 영구 또는 임시 키를 설정하여 사전 서명된 URL을 가져올 수 있습니다.

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
