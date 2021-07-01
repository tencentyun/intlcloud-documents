## 소개

본 문서는 기본 이미지 처리에 대한 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업 설명                                                     |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [크기 조정](https://intl.cloud.tencent.com/document/product/436/36366) | 이미지 확대 및 축소                                         |
| [자르기](https://intl.cloud.tencent.com/document/product/436/36367) | 일반 자르기, 크기 조정 자르기, 원형 자르기, 둥근 모서리 자르기, 스마트 얼굴 자르기를 포함한 이미지 편집 |
| [회전](https://intl.cloud.tencent.com/document/product/436/36368) | 일반 회전 및 자동 회전을 포함한 이미지 회전                     |
| [포맷 변환](https://intl.cloud.tencent.com/document/product/436/36369) | 이미지 포맷 변환, gif 포맷 최적화, 점진적 표시                   |
| [품질 변경](https://intl.cloud.tencent.com/document/product/436/36370) | 이미지 품질 조정                                           |
| [가우시안 블러](https://intl.cloud.tencent.com/document/product/436/36371) | 이미지 가우시안 블러 처리                                           |
| [샤프닝](https://intl.cloud.tencent.com/document/product/436/36372) | 이미지 샤프닝 처리                                               |
| [이미지 워터마크](https://intl.cloud.tencent.com/document/product/436/36373) | 이미지 워터마크 처리                                           |
| [문자 워터마크](https://intl.cloud.tencent.com/document/product/436/36374) | 이미지에 실시간 문자 워터마크 처리                                   |
| [이미지 기본 정보 획득](https://intl.cloud.tencent.com/document/product/436/36375) | 포맷, 길이, 폭 등 이미지 기본 정보 조회                         |
| [이미지 EXIF 획득](https://intl.cloud.tencent.com/document/product/436/36376) | EXIF 정보 조회                                               |
| [이미지 메인 컬러 획득](https://intl.cloud.tencent.com/document/product/436/36377) | 이미지 메인 컬러 정보 조회                                           |
| [메타 정보 제거](https://intl.cloud.tencent.com/document/product/436/36378) | exif 정보를 포함한 이미지 메타 정보 제거                               |
| [빠른 썸네일 템플릿](https://intl.cloud.tencent.com/document/product/436/36379) | 이미지 처리 템플릿을 통해 알맞은 썸네일 생성                           |
| [파이프 연산자](https://intl.cloud.tencent.com/document/product/436/36380) | 순서대로 이미지에 여러 처리 효과 구현                                 |

## 크기 조정

#### 기능 설명

Tencent Cloud CI는 **imageMogr2** 인터페이스를 통해 이미지 크기 조정 기능을 제공합니다.

#### 요청 예시

```c
cos_pool_t *p = NULL;
int is_cname = 0; 
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_string_t file;
cos_table_t *resp_headers;
cos_table_t *params = NULL;
  
cos_pool_create(&p, NULL);
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

params = cos_table_make(p, 1);
apr_table_addn(params, "imageMogr2/thumbnail/!50p", "");
cos_str_set(&file, "test.jpg");
cos_str_set(&object, "test.jpg");
s = cos_get_object_to_file(options, &bucket, &object, NULL, params, &file, &resp_headers);
log_status(s);
if (!cos_status_is_ok(s)) {
    printf("cos_get_object_to_file fail, req_id:%s\n", s->req_id);
}
cos_pool_destroy(p);
```

## 자르기

#### 기능 설명

Tencent Cloud CI는 **imageMogr2** 인터페이스를 통해 일반 자르기, 크기 조정 자르기, 원형 자르기, 둥근 모서리 자르기, 스마트 얼굴 자르기 등을 포함한 자르기 기능을 제공합니다.

#### 요청 예시

```c
cos_pool_t *p = NULL;
int is_cname = 0; 
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_string_t file;
cos_table_t *resp_headers;
cos_table_t *params = NULL;
  
cos_pool_create(&p, NULL);
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

params = cos_table_make(p, 1);
apr_table_addn(params, "imageMogr2/cut/600x600x100x10", "");
cos_str_set(&file, "test.jpg");
cos_str_set(&object, "test.jpg");
s = cos_get_object_to_file(options, &bucket, &object, NULL, params, &file, &resp_headers);
log_status(s);
if (!cos_status_is_ok(s)) {
    printf("cos_get_object_to_file fail, req_id:%s\n", s->req_id);
}
cos_pool_destroy(p);
```

### 기타 기본 이미지 처리

#### 기능 설명

기본 이미지 처리는 모두 위와 같은 방법으로 완료됩니다. 기타 기본 이미지 처리는 operation 매개변수 값만 변경하면 됩니다(예시: 이미지를 시계 방향으로 90도 회전하는 경우).

```c
cos_pool_t *p = NULL;
int is_cname = 0; 
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_string_t file;
cos_table_t *resp_headers;
cos_table_t *params = NULL;
  
cos_pool_create(&p, NULL);
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

params = cos_table_make(p, 1);
apr_table_addn(params, "imageMogr2/rotate/90", "");
cos_str_set(&file, "test.jpg");
cos_str_set(&object, "test.jpg");
s = cos_get_object_to_file(options, &bucket, &object, NULL, params, &file, &resp_headers);
log_status(s);
if (!cos_status_is_ok(s)) {
    printf("cos_get_object_to_file fail, req_id:%s\n", s->req_id);
}
cos_pool_destroy(p);
```

