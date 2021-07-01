

## 소개

본 문서는 이미지 영구 처리에 대한 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 설명                                 |
| :----------------------------------------------------------- | :----------------------------------- |
| [이미지 영구 처리](https://cloud.tencent.com/document/product/436/54050) | 객체 스토리지는 업로드 시 처리 기능을 제공합니다. 사용자가 업로드 시 이미지 처리를 하고 COS에 저장된 이미지에 알맞은 처리 작업을 하여 결과를 객체 스토리지(Cloud Object Storage, COS)에 저장합니다. |


## 업로드 시 처리

#### 기능 설명

COS가 제공하는 업로드 시 처리 기능은 이미지를 업로드하는 경우 이미지 처리를 실행합니다. 요청 패키지 헤더에 Pic-Operations 항목을 추가하고 해당하는 매개변수를 설정해야 합니다. 즉 이미지 업로드 시 적합한 이미지 처리를 진행하여 원본 이미지와 작업 결과를 COS에 저장합니다. 현재 20M 이하의 파일 처리를 지원합니다.

#### 방법 모델

```c
cos_status_t *ci_put_object_from_file(const cos_request_options_t *options,
                                         const cos_string_t *bucket, 
                                         const cos_string_t *object, 
                                         const cos_string_t *filename,
                                         cos_table_t *headers, 
                                         cos_table_t **resp_headers,
                                         ci_operation_result_t **results)
```


#### 요청 예시

```c
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_string_t file;
cos_table_t *headers = NULL;
cos_table_t *resp_headers = NULL;
ci_operation_result_t *results = NULL;

//메모리 풀 생성
cos_pool_create(&p, NULL);

// 초기화 요청 옵션
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

//업로드 시 처리
headers = cos_table_make(p, 1);
apr_table_addn(headers, "pic-operations", "{\"is_pic_info\":1,\"rules\":[{\"fileid\":\"test.png\",\"rule\":\"imageView2/format/png\"}]}");
cos_str_set(&file, "test.jpg");
cos_str_set(&object, "test.jpg");
s = ci_put_object_from_file(options, &bucket, &object, &file, headers, &resp_headers, &results);
if (! cos_status_is_ok(s)) {
    printf("put object failed: %s\n", s->req_id);
}
printf("origin key: %s\n", results.origin.key.data);
printf("process key: %s\n", results.object.key.data);

//메모리 풀 폐기
cos_pool_destroy(p); 
```

#### 매개변수 설명

| 매개변수 이름     | 매개변수 설명                                                     | 유형   |
| :----------- | :----------------------------------------------------------- | :----- |
| options      | COS 요청 옵션                                                 | Struct |
| bucket       | 버킷 이름. 버킷의 이름 생성 포맷은 BucketName-APPID로 여기에 입력하는 버킷 이름은 반드시 해당 포맷을 따라야 함 | String |
| object       | Object 이름                                                  | String |
| filename     | Object 로컬에 저장된 파일 이름                                      | String |
| headers      | COS에서 부가 헤더 필드 요청                                             | Struct |
| resp_headers | HTTP 응답 메시지의 헤더 필드 반환                                     | Struct |
| results      | 클라우드 데이터 처리에서 반환된 정보                                         | Struct |



## 클라우드 데이터 처리
#### 기능 설명

해당 인터페이스로 COS에 저장된 이미지에 알맞은 처리 작업을 하여 결과를 COS에 저장할 수 있습니다.

#### 방법 모델
```c
cos_status_t *ci_image_process(const cos_request_options_t *options,
								const cos_string_t *bucket,
								const cos_string_t *object,
								cos_table_t *headers,
								cos_table_t **resp_headers,
								ci_operation_result_t *results);
```

#### 요청 예시

```c
cos_pool_t *p = NULL;
int is_cname = 0; 
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_table_t *resp_headers;
cos_table_t *headers = NULL;
ci_operation_result_t results;
  
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

cos_str_set(&object, "test.jpg");
headers = cos_table_make(p, 1);
apr_table_addn(headers, "pic-operations", "{\"is_pic_info\":1,\"rules\":[{\"fileid\":\"test.png\",\"rule\":\"imageView2/format/png\"}]}");
      
s = ci_image_process(options, &bucket, &object, headers, &resp_headers, &results);
if (! cos_status_is_ok(s)) {
    printf("ci image process fail, req_id:%s\n", s->req_id);
}
printf("origin key: %s\n", results.origin.key.data);
printf("process key: %s\n", results.object.key.data);
cos_pool_destroy(p);
```



#### 매개변수 설명

| 매개변수 이름 | 매개변수 설명                                                     | 유형   |
| --------- | ------------------------------------------------------------ | ------ |
| options | COS 요청 옵션 | Struct |
| bucket | 버킷 이름, Bucket의 이름 생성 규칙은 BucketName-APPID로 여기에 입력하는 버킷 이름은 반드시 해당 포맷을 따라야 함 | string |
| object | Object 이름 | string |
| headers | COS가 부가 헤더 필드를 요청하면 자체적으로 Pic-Operations CI를 추가해 헤더 처리 | Struct |
| resp_headers | HTTP 응답 메시지의 헤더 필드 반환 | Struct |
| results | 클라우드 데이터 처리에서 반환된 정보 | Struct |

