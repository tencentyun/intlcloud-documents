## 소개

본 문서는 객체에 대한 간단한 작업, 멀티파트 작업 및 기타 작업 관련 API 개요 및 SDK 예시 코드에 대한 설명입니다.

**간단한 작업**

| API                                                          | 작업 이름         | 작업 설명                   |
| ------------------------------------------------------------ | -------------- | ------------------------------ |
| [GET Bucket(List Objects)](https://intl.cloud.tencent.com/document/product/436/30614) | 객체 리스트 조회   | 버킷의 일부 또는 모든 객체 조회 |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | 객체 간편 업로드(폴더 생성)   | 하나의 객체를 버킷에 업로드           |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | 객체 메타데이터 조회 | 객체 메타데이터 정보 조회           |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | 객체 다운로드       | 로컬에 객체 다운로드             |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | 객체 복사 설정(속성 수정)   | 파일을 타깃 경로에 복사                       |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | 단일 객체 삭제   | 버킷에서 지정 객체 삭제         |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | 다수의 객체 삭제   | 버킷에서 객체 일괄 삭제         |

**멀티파트 작업**

| API                                                          | 작업명         | 작업 설명                             |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | 멀티파트 업로드 조회   | 현재 진행 중인 멀티파트 업로드 정보 조회         |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | 멀티파트 업로드 초기화 | 멀티파트 업로드 작업 초기화                   |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | 파트 업로드       | 파일 멀티파트 업로드                         |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | 멀티파트 복사       | 다른 객체를 한 파트로 복사             |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | 업로드된 파트 조회   | 특정 멀티파트 업로드 작업에서 업로드된 파트 조회   |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | 멀티파트 업로드 완료   | 전체 파일의 멀티파트 업로드 완료               |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | 멀티파트 업로드 중지   | 하나의 멀티파트 업로드 작업 중지 및 이미 업로드한 파트 삭제 |

**기타 작업**

| API                                                          | 작업명       | 작업 설명                           |
| ------------------------------------------------------------ | ------------ | ---------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | 보관된 객체 복구 | 아카이브 유형의 객체 검색 및 액세스           |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | 객체 ACL 설정 | 버킷의 특정 객체의 액세스 제어 리스트 설정 |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | 객체 ACL 조회 | 객체 액세스 제어 리스트 조회             |

## 간단한 작업

### 객체 리스트 조회

#### 기능 설명

버킷의 일부 또는 모든 객체를 조회합니다.

#### 메소드 프로토타입

```cpp
cos_status_t *cos_list_object(const cos_request_options_t *options,
                              const cos_string_t *bucket, 
                              cos_list_object_params_t *params, 
                              cos_table_t **resp_headers);
```

#### 매개변수 설명

| 매개변수 이름           | 매개변수 설명                                                     | 유형   |
| ------------------ | ------------------------------------------------------------ | ------- |
| options            | COS 요청 옵션                                                 | Struct  |
| bucket             | 버킷 이름, Bucket의 이름 생성 포맷은 BucketName-APPID로 여기에 입력하는 버킷 이름은 반드시 해당 포맷을 따라야 함 | String  |
| params             | 리스트 작업 매개변수 정보                                          | Struct  |
| encoding_type      | 규정된 반환 값의 인코딩 방식                                         | String  |
| prefix             | 접두사 매칭, 반환 파일의 접두사 주소 규정에 사용                         | String  |
| marker             | 기본적으로 UTF-8 이진법 순서로 열거되며, 모든 열거 값은 marker부터 시작  | String  |
| delimiter          | 세퍼레이터 조회, 객체 키 그룹 나누기에 사용                             | String  |
| max_ret            | 한 번에 반환하는 최대 항목 수, 기본값: 1000                             | Struct  |
| truncated          | 반환 항목의 잘림 여부는 ’true’ 또는 ’false’                      | Boolean |
| next_marker        | 반환 항목이 잘린 경우, 반환된 NextMarker가 다음 항목의 시작점이 됨   | String  |
| object_list        | Get Bucket 작업에서 반환한 객체 정보 리스트                            | Struct  |
| key                | Get Bucket 작업에서 반환한 Object 이름                            | Struct  |
| last_modified      | Get Bucket 작업에서 반환한 Object의 최종 수정 시간                    | Struct  |
| etag               | Get Bucket 작업에서 반환한 객체의 SHA-1 알고리즘 검증값                 | Struct  |
| size               | Get Bucket 작업에서 반환한 객체 크기, 단위: Byte                     | Struct  |
| owner_id           | Get Bucket 작업에서 반환한 객체 소유자의 UID 정보                     | Struct  |
| storage_class      | Get Bucket 작업에서 반환한 COS 레벨                            | Struct  |
| common_prefix_list | Prefix부터 delimiter 사이의 동일한 경로를 하나로 분류하여 Common Prefix로 정의 | Struct  |
| resp_headers       | HTTP 응답 메시지의 헤더 필드 반환                                     | Struct  |

#### 반환 결과 설명

| 반환 결과   | 설명        | 유형   |
| ---------- | ----------- | ------ |
| code       | 에러 코드      | Int    |
| error_code | 에러 코드 내용  | String |
| error_msg  | 에러 코드 설명  | String |
| req_id     | 메시지 ID 요청 | String |

#### 예시1: 객체 리스트 조회

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_table_t *resp_headers = NULL;

//메모리 풀 생성
cos_pool_create(&p, NULL);

//초기화 요청 옵션
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

//객체 리스트 획득
cos_list_object_params_t *list_params = NULL;
cos_list_object_content_t *content = NULL;
list_params = cos_create_list_object_params(p);
s = cos_list_object(options, &bucket, list_params, &resp_headers);
if (cos_status_is_ok(s)) {
    printf("list object succeeded\n");
    cos_list_for_each_entry(cos_list_object_content_t, content, &list_params->object_list, node) {
        key = printf("%.*s\n", content->key.len, content->key.data);
    }
} else {
    printf("list object failed\n");
}

//메모리 풀 폐기
cos_pool_destroy(p); 
```

#### 예시2: 디렉터리의 객체 나열

COS 자체에는 폴더 및 디렉터리의 개념이 없습니다. 사용자의 습관에 맞춰 세퍼레이터 /로 ‘폴더’를 구현할 수 있습니다.

```c
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_table_t *resp_headers;
int is_truncated = 1;
cos_string_t marker;
  
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
  
//list object (get bucket)
cos_list_object_params_t *list_params = NULL;
list_params = cos_create_list_object_params(p);
// prefix는 나열된 object의 key가 prefix로 시작함을 의미함
cos_str_set(&list_params->prefix, "folder/");
// delimiter는 세퍼레이터를 의미함. /로 설정하면 현재 디렉터리의 object를 나열하고, 공백으로 설정하면 전체 object를 나열함
cos_str_set(&list_params->delimiter, "/");
// 순회할 객체의 최대 수량 설정. listobject 1회당 최대 1000개까지 지원함
list_params->max_ret = 1000;
cos_str_set(&marker, "");
while (is_truncated) {
    list_params->marker = marker;
    s = cos_list_object(options, &bucket, list_params, &resp_headers);
    if (! cos_status_is_ok(s)) {
        printf("list object failed, req_id:%s\n", s->req_id);
        break;
    }
    // list_params->object_list 나열된 object 객체 반환.
    cos_list_object_content_t *content = NULL;
    cos_list_for_each_entry(cos_list_object_content_t, content, &list_params->object_list, node) {
        printf("object: %s\n", content->key.data);
    }
    // list_params->common_prefix_list는 delimiter로 잘린 경로를 표시함. 예를 들어 delimiter를 /로 설정하면 common prefix는 모든 서브 디렉터리의 경로를 표시함
    cos_list_object_common_prefix_t *common_prefix = NULL;
    cos_list_for_each_entry(cos_list_object_common_prefix_t, common_prefix, &list_params->common_prefix_list, node) {
        printf("common prefix: %s\n", common_prefix->prefix.data);
    }

	is_truncated = list_params->truncated;
	marker = list_params->next_marker;
}    
cos_pool_destroy(p);
```

### 간편 객체 업로드(폴더 생성)

#### 기능 설명

객체를 버킷에 업로드합니다. 최대 5GB 이하인 객체의 업로드를 지원하며, 5GB를 초과하는 객체의 경우 [멀티파트 업로드](#.E5.88.86.E5.9D.97.E6.93.8D.E4.BD.9C) 또는 [고급 인터페이스](#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89)를 사용하여 업로드하십시오.

#### 메소드 프로토타입

```cpp
cos_status_t *cos_put_object_from_file(const cos_request_options_t *options,
                                       const cos_string_t *bucket, 
                                       const cos_string_t *object, 
                                       const cos_string_t *filename,
                                       cos_table_t *headers, 
                                       cos_table_t **resp_headers);
```

#### 매개변수 설명

| 매개변수 이름     | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| options      | COS 요청 옵션                                                 | Struct |
| bucket       | 버킷 이름. 버킷의 이름 생성 포맷은 BucketName-APPID로 여기에 입력하는 버킷 이름은 반드시 해당 포맷을 따라야 함 | String |
| object       | Object 이름                                                  | String |
| filename     | Object 로컬에 저장된 파일 이름                                      | String |
| headers      | COS에서 부가 헤더 필드 요청                                             | Struct |
| resp_headers | HTTP 응답 메시지의 헤더 필드 반환                                     | Struct |

#### 반환 결과 설명

| 반환 결과   | 설명        | 유형   |
| ---------- | ----------- | ------ |
| code       | 에러 코드      | Int    |
| error_code | 에러 코드 내용  | String |
| error_msg  | 에러 코드 설명  | String |
| req_id     | 메시지 ID 요청 | String |


#### 예시1: 객체 업로드

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_string_t file;
cos_table_t *resp_headers = NULL;

//메모리 풀 생성
cos_pool_create(&p, NULL);

//초기화 요청 옵션
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

//객체 업로드
cos_str_set(&file, TEST_DOWNLOAD_NAME);
cos_str_set(&object, TEST_OBJECT_NAME);
s = cos_put_object_from_file(options, &bucket, &object, &file, NULL, &resp_headers);
if (cos_status_is_ok(s)) {
    printf("put object succeeded\n");
} else {
    printf("put object failed\n");
}

//메모리 풀 폐기
cos_pool_destroy(p); 
```

#### 예시2: 폴더 생성

COS에서는 `/`로 구분된 객체 경로를 가상 폴더로 인식합니다. 이러한 특성에 따라 이름이 `/`로 끝나는 빈 스트림을 업로드하면 COS에 빈 폴더를 생성할 수 있습니다.

```c
cos_pool_t *p = NULL;
int is_cname = 0; 
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_table_t *resp_headers;
cos_table_t *headers = NULL;
cos_list_t buffer;
  
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
cos_str_set(&object, "folder/");
cos_list_init(&buffer);
s = cos_put_object_from_buffer(options, &bucket, &object, 
		&buffer, headers, &resp_headers);
if (cos_status_is_ok(s)) {
    printf("put object succeeded\n");
} else {
    printf("put object failed\n");
}
cos_pool_destroy(p);
```

#### 예시3: 가상 디렉터리에 파일 업로드

`/`로 구분되는 객체 이름을 업로드하면 파일이 포함된 폴더를 자동으로 생성할 수 있습니다. 해당 폴더에 새로운 파일을 추가하려면 COS에 파일 업로드 시 Key를 해당 디렉터리 접두사로 입력하면 됩니다.

```c
cos_pool_t *p = NULL;
int is_cname = 0; 
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_string_t file;
cos_table_t *resp_headers;
cos_table_t *headers = NULL;
cos_list_t buffer;
  
cos_pool_create(&p, NULL);
options = cos_request_options_create(p);
init_test_request_options(options, is_cname);
cos_str_set(&bucket, TEST_BUCKET_NAME);
cos_str_set(&file, "examplefile");
cos_str_set(&object, "folder/exampleobject");
s = cos_put_object_from_file(options, &bucket, &object, &file, NULL, &resp_headers);
if (cos_status_is_ok(s)) {
    printf("put object succeeded\n");
} else {
    printf("put object failed\n");
}
cos_pool_destroy(p);
```

#### 예시4: 객체 업로드(단일 링크 속도 제한)

>?객체 업로드 및 다운로드 속도 제한 설명은 [단일 링크 속도 제한](https://intl.cloud.tencent.com/document/product/436/34072)을 참고하시기 바랍니다.

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_string_t file;
cos_table_t *resp_headers = NULL;
cos_table_t *headers = NULL;

//메모리 풀 생성
cos_pool_create(&p, NULL);

//초기화 요청 옵션
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

//속도 제한값은 819200 - 838860800, 즉 100KB/s - 100MB/s 범위에서 설정할 수 있으며, 이 범위를 넘으면 400 오류가 반환됨
headers = cos_table_make(p, 1);
cos_table_add_int(headers, "x-cos-traffic-limit", 819200);

//객체 업로드
cos_str_set(&file, TEST_DOWNLOAD_NAME);
cos_str_set(&object, TEST_OBJECT_NAME);
s = cos_put_object_from_file(options, &bucket, &object, &file, headers, &resp_headers);
if (cos_status_is_ok(s)) {
    printf("put object succeeded\n");
} else {
    printf("put object failed\n");
}

//메모리 풀 폐기
cos_pool_destroy(p); 
```


### 객체 메타데이터 조회

#### 기능 설명

객체의 메타데이터 정보 조회

#### 메소드 프로토타입

```cpp
cos_status_t *cos_head_object(const cos_request_options_t *options, 
                              const cos_string_t *bucket, 
                              const cos_string_t *object,
                              cos_table_t *headers, 
                              cos_table_t **resp_headers);
```

#### 매개변수 설명

| 매개변수 이름     | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| options      | COS 요청 옵션                                                 | Struct |
| bucket       | 버킷 이름. 버킷의 이름 생성 포맷은 BucketName-APPID로 여기에 입력하는 버킷 이름은 반드시 해당 포맷을 따라야 함 | String |
| object       | Object 이름                                                  | String |
| headers      | COS에서 부가 헤더 필드 요청                                             | Struct |
| resp_headers | HTTP 응답 메시지의 헤더 필드 반환                                     | Struct |

#### 반환 결과 설명

| 반환 결과   | 설명        | 유형   |
| ---------- | ----------- | ------ |
| code       | 에러 코드      | Int    |
| error_code | 에러 코드 내용  | String |
| error_msg  | 에러 코드 설명  | String |
| req_id     | 메시지 ID 요청 | String |

#### 예시

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_table_t *resp_headers = NULL;

//메모리 풀 생성
cos_pool_create(&p, NULL);

//초기화 요청 옵션
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

//객체 메타데이터 획득
cos_str_set(&object, TEST_OBJECT_NAME);
s = cos_head_object(options, &bucket, &object, NULL, &resp_headers);
if (cos_status_is_ok(s)) {
    printf("head object succeeded\n");
} else {
    printf("head object failed\n");
}

//메모리 풀 폐기
cos_pool_destroy(p); 
```

### 객체 다운로드

#### 기능 설명

객체를 로컬에 다운로드합니다. 해당 작업은 타깃 객체에 대한 읽기 권한을 가지고 있거나 타깃 객체의 읽기 권한이 개방되어 있어야 합니다(공개 읽기).

#### 메소드 프로토타입

```cpp
cos_status_t *cos_get_object_to_file(const cos_request_options_t *options,
                                     const cos_string_t *bucket, 
                                     const cos_string_t *object,
                                     cos_table_t *headers, 
                                     cos_table_t *params,
                                     cos_string_t *filename, 
                                     cos_table_t **resp_headers);
```

#### 매개변수 설명

| 매개변수 이름     | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| options      | COS 요청 옵션                                                 | Struct |
| bucket       | 버킷 이름. 버킷의 이름 생성 포맷은 BucketName-APPID로 여기에 입력하는 버킷 이름은 반드시 해당 포맷을 따라야 함 | String |
| object       | Object 이름                                                  | String |
| headers      | COS에서 부가 헤더 필드 요청                                             | Struct |
| params       | COS에서 작업 매개변수 요청                                             | Struct |
| filename     | Object 로컬에 저장된 파일 이름                                      | String |
| resp_headers | HTTP 응답 메시지의 헤더 필드 반환                                     | Struct |

#### 반환 결과 설명

| 반환 결과   | 설명        | 유형   |
| ---------- | ----------- | ------ |
| code       | 에러 코드      | Int    |
| error_code | 에러 코드 내용  | String |
| error_msg  | 에러 코드 설명  | String |
| req_id     | 메시지 ID 요청 | String |

#### 예시1: 일반 다운로드

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_string_t file;
cos_table_t *resp_headers = NULL;

//메모리 풀 생성
cos_pool_create(&p, NULL);

//초기화 요청 옵션
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

//객체 획득
cos_str_set(&file, TEST_DOWNLOAD_NAME);
cos_str_set(&object, TEST_OBJECT_NAME);
s = cos_get_object_to_file(options, &bucket, &object, NULL, NULL, &file, &resp_headers);
if (cos_status_is_ok(s)) {
    printf("get object succeeded\n");
} else {
    printf("get object failed\n");
}

//메모리 풀 폐기
cos_pool_destroy(p); 
```

#### 예시2: 객체 다운로드(단일 링크 속도 제한)

>?객체 업로드 및 다운로드 속도 제한 설명은 [단일 링크 속도 제한](https://intl.cloud.tencent.com/document/product/436/34072)을 참고하시기 바랍니다.

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_string_t file;
cos_table_t *headers = NULL;
cos_table_t *resp_headers = NULL;

//메모리 풀 생성
cos_pool_create(&p, NULL);

//초기화 요청 옵션
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

//속도 제한값은 819200 - 838860800, 즉 100KB/s - 100MB/s 범위에서 설정할 수 있으며, 이 범위를 넘으면 400 오류가 반환됨
headers = cos_table_make(p, 1);
cos_table_add_int(headers, "x-cos-traffic-limit", 819200);

//객체 획득
cos_str_set(&file, TEST_DOWNLOAD_NAME);
cos_str_set(&object, TEST_OBJECT_NAME);
s = cos_get_object_to_file(options, &bucket, &object, headers, NULL, &file, &resp_headers);
if (cos_status_is_ok(s)) {
    printf("get object succeeded\n");
} else {
    printf("get object failed\n");
}

//메모리 풀 폐기
cos_pool_destroy(p); 
```



### 객체 복사 설정(속성 수정)

#### 기능 설명

파일을 타깃 경로에 복사합니다. 이 인터페이스는 객체 스토리지 유형 수정 등 객체 속성을 수정할 수 있습니다.

#### 메소드 프로토타입

```cpp
cos_status_t *cos_copy_object(const cos_request_options_t *options,
                              const cos_string_t *src_bucket,
                              const cos_string_t *src_object,
                              const cos_string_t *src_endpoint,
                              const cos_string_t *dest_bucket, 
                              const cos_string_t *dest_object,
                              cos_table_t *headers,
                              cos_copy_object_params_t *copy_object_param,
                              cos_table_t **resp_headers);
```

#### 매개변수 설명

| 매개변수 이름          | 매개변수 설명                                                     | 유형   |
| ----------------- | ------------------------------------------------------------ | ------ |
| options           | COS 요청 옵션                                                 | Struct   |
| src_bucket        | 원본 버킷                                                     | String |
| src_object        | 원본 객체 이름                                                   | String |
| src_endpoint      | 원본 객체 액세스 도메인 정보                                           | String |
| dest_bucket       | 타깃 버킷 이름. 버킷의 이름 생성 포맷은 BucketName-APPID로 여기에 입력하는 버킷 이름은 반드시 해당 포맷을 따라야 함 | String |
| dest_object       | 타깃 Object 이름                                             | String |
| headers           | COS에서 부가 헤더 필드 요청                                             | Struct |
| copy_object_param | Put Object Copy 작업 매개변수                                     | Struct |
| etag              | 반환 파일의 MD5 알고리즘 검증값                                    | String |
| last_modify       | 반환 파일의 최종 수정 시간, GMT 포맷                               | String |
| resp_headers      | HTTP 응답 메시지의 헤더 필드 반환                                     | Struct |

#### 반환 결과 설명

| 반환 결과   | 설명        | 유형   |
| ---------- | ----------- | ------ |
| code       | 에러 코드      | Int    |
| error_code | 에러 코드 내용  | String |
| error_msg  | 에러 코드 설명  | String |
| req_id     | 메시지 ID 요청 | String |

#### 예시1: 일반 객체 복사

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_string_t src_bucket;
cos_string_t src_object;
cos_string_t src_endpoint;
cos_table_t *resp_headers = NULL;

//메모리 풀 생성
cos_pool_create(&p, NULL);

//초기화 요청 옵션
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

//객체 복사 설정
cos_str_set(&object, TEST_OBJECT_NAME);
cos_str_set(&src_bucket, TEST_BUCKET_NAME);
cos_str_set(&src_endpoint, "ap-guangzhou.myqcloud.com");
cos_str_set(&src_object, "test.txt");

cos_copy_object_params_t *params = NULL;
params = cos_create_copy_object_params(p);
s = cos_copy_object(options, &src_bucket, &src_object, &src_endpoint, &bucket, &object, NULL, params, &resp_headers);
if (cos_status_is_ok(s)) {
    printf("put object copy succeeded\n");
} else {
    printf("put object copy failed\n");
}

//메모리 풀 폐기
cos_pool_destroy(p);  
```

#### 예시2: 스토리지 유형 변경

>!표준 스토리지는 표준IA 스토리지, 인텔리전트 티어링, 아카이브 스토리지 및 딥 아카이브 스토리지 등으로 변경할 수 있습니다. 아카이브 스토리지 또는 딥 아카이브 스토리지의 객체를 다른 스토리지 유형으로 수정하려면 먼저 cos_post_object_restore() 인터페이스를 사용하여 복구해야 합니다. 스토리지 유형에 대한 자세한 내용은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925)를 참고하시기 바랍니다.


```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_string_t src_bucket;
cos_string_t src_object;
cos_string_t src_endpoint;
cos_table_t *resp_headers = NULL;

//메모리 풀 생성
cos_pool_create(&p, NULL);

//초기화 요청 옵션
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);
//원본 객체와 타깃 객체가 일치함
cos_str_set(&object, "test.txt");
cos_str_set(&src_object, "test.txt");
cos_str_set(&src_bucket, TEST_BUCKET_NAME);
cos_str_set(&src_endpoint, TEST_COS_ENDPOINT);

// x-cos-metadata-directive 및 x-cos-storage-class 헤더 필드를 설정하고, 변경하려는 스토리지 유형으로 대체
cos_table_t *headers = cos_table_make(p, 2);
apr_table_add(headers, "x-cos-metadata-directive", "Replaced");
// 스토리지 유형에는 NTELLIGENT_TIERING, MAZ_INTELLIGENT_TIERING, STANDARD_IA, ARCHIVE, DEEP_ARCHIVE가 있음
apr_table_add(headers, "x-cos-storage-class", "ARCHIVE");

//객체 복사, 스토리지 유형 설정
cos_copy_object_params_t *params = NULL;
params = cos_create_copy_object_params(p);
s = cos_copy_object(options, &src_bucket, &src_object, &src_endpoint, & bucket, &object, headers, params, &resp_headers);
if (cos_status_is_ok(s)) {
    printf("copy object succeeded\n");
} else {
    printf("copy object failed\n");
}

//메모리 풀 폐기
cos_pool_destroy(p); 
```



### 단일 객체 삭제

#### 기능 설명

버킷에서 지정 객체를 삭제합니다.

#### 메소드 프로토타입

```cpp
cos_status_t *cos_delete_object(const cos_request_options_t *options,
                                const cos_string_t *bucket, 
                                const cos_string_t *object, 
                                cos_table_t **resp_headers);
```

#### 매개변수 설명

| 매개변수 이름     | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| options      | COS 요청 옵션                                                 | Struct |
| bucket       | 버킷 이름. 버킷의 이름 생성 포맷은 BucketName-APPID로 여기에 입력하는 버킷 이름은 반드시 해당 포맷을 따라야 함 | String |
| object       | Object 이름                                                  | String |
| resp_headers | HTTP 응답 메시지의 헤더 필드 반환                                     | Struct |

#### 반환 결과 설명

| 반환 결과   | 설명        | 유형   |
| ---------- | ----------- | ------ |
| code       | 에러 코드      | Int    |
| error_code | 에러 코드 내용  | String |
| error_msg  | 에러 코드 설명  | String |
| req_id     | 메시지 ID 요청 | String |


#### 예시1: 객체 삭제

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_table_t *resp_headers = NULL;

//메모리 풀 생성
cos_pool_create(&p, NULL);

//초기화 요청 옵션
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

//단일 객체 삭제
cos_str_set(&object, TEST_OBJECT_NAME);
s = cos_delete_object(options, &bucket, &object, &resp_headers);
if (cos_status_is_ok(s)) {
    printf("delete object succeeded\n");
} else {
    printf("delete object failed\n");
}

//메모리 풀 폐기
cos_pool_destroy(p); 

```

#### 예시2: 폴더 삭제

해당 요청은 폴더 안의 객체가 아닌 지정 key만 삭제합니다.

```
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_table_t *resp_headers = NULL;

//메모리 풀 생성
cos_pool_create(&p, NULL);

//초기화 요청 옵션
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

//디렉터리 객체 삭제
cos_str_set(&object, "folder/");
s = cos_delete_object(options, &bucket, &object, &resp_headers);
if (cos_status_is_ok(s)) {
    printf("delete object succeeded\n");
} else {
    printf("delete object failed\n");
}

//메모리 풀 폐기
cos_pool_destroy(p); 
```



### 다수의 객체 삭제

#### 기능 설명

버킷의 객체 일괄 삭제는 한 번에 최대 1000개의 객체 삭제를 지원합니다. COS는 반환 결과에 대해 Verbose와 Quiet 두 가지 결과 모드를 제공합니다. Verbose 모드는 모든 Object의 삭제 결과를 반환하고, Quiet 모드는 오류가 보고된 Object 정보만 반환합니다.

#### 메소드 프로토타입

```cpp
cos_status_t *cos_delete_objects(const cos_request_options_t *options,
                                 const cos_string_t *bucket, 
                                 cos_list_t *object_list, 
                                 int is_quiet,
                                 cos_table_t **resp_headers, 
                                 cos_list_t *deleted_object_list);
```

#### 매개변수 설명

| 매개변수 이름            | 매개변수 설명                                                     | 유형   |
| ------------------- | ------------------------------------------------------------ | ------- |
| options             | COS 요청 옵션                                                 | Struct  |
| bucket              | 버킷 이름. 버킷의 이름 생성 포맷은 BucketName-APPID로 여기에 입력하는 버킷 이름은 반드시 해당 포맷을 따라야 함 | String  |
| object_list         | 삭제 대기 Object 리스트                                            | Struct  |
| key                 | 삭제 대기 Object 이름                                           | String  |
| is_quiet            | Quiet 모드의 실행 여부 결정: <br>True(1): Quiet 모드 실행, False(0): Verbose 모드 실행, 기본값은 False(0) | Boolean |
| resp_headers        | HTTP 응답 메시지의 헤더 필드 반환                                     | Struct  |
| deleted_object_list | Object 삭제 정보 리스트                                          | Struct  |

#### 반환 결과 설명

| 반환 결과   | 설명        | 유형   |
| ---------- | ----------- | ------ |
| code       | 에러 코드      | Int    |
| error_code | 에러 코드 내용  | String |
| error_msg  | 에러 코드 설명  | String |
| req_id     | 메시지 ID 요청 | String |



#### 예시1: 다수의 객체 삭제

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_table_t *resp_headers = NULL;

//메모리 풀 생성
cos_pool_create(&p, NULL);

//초기화 요청 옵션
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

//객체 일괄 삭제 설정
char *object_name1 = TEST_OBJECT_NAME1;
char *object_name2 = TEST_OBJECT_NAME2;
cos_object_key_t *content1 = NULL;
cos_object_key_t *content2 = NULL;
cos_list_t object_list;
cos_list_t deleted_object_list;
cos_list_init(&object_list);
cos_list_init(&deleted_object_list);
content1 = cos_create_cos_object_key(p);
cos_str_set(&content1->key, object_name1);
cos_list_add_tail(&content1->node, &object_list);
content2 = cos_create_cos_object_key(p);
cos_str_set(&content2->key, object_name2);
cos_list_add_tail(&content2->node, &object_list);

//객체 일괄 삭제
int is_quiet = COS_TRUE;
cos_str_set(&object, TEST_OBJECT_NAME);
s = cos_delete_objects(options, &bucket, &object_list, is_quiet, &resp_headers, &deleted_object_list);
if (cos_status_is_ok(s)) {
    printf("delete objects succeeded\n");
} else {
    printf("delete objects failed\n");
}

//메모리 풀 폐기
cos_pool_destroy(p); 

```

#### 예시2: 폴더 및 해당 파일 삭제

COS 자체에는 폴더 및 디렉터리의 개념이 없습니다. 사용자의 습관에 맞춰 세퍼레이터 /로 ‘폴더’를 구현할 수 있습니다.

폴더 및 파일 삭제는 실제로 COS에서 동일한 접두사를 가진 객체를 삭제하는 것과 같습니다. 현재 COS C SDK는 이러한 작업을 구현할 인터페이스를 제공하지 않지만, **객체 리스트 조회**와 **객체 일괄 삭제**를 함께 사용하는 기본 작업으로 폴더 및 파일을 삭제할 수 있습니다.

```c
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_table_t *resp_headers;
int is_truncated = 1;
cos_string_t marker;
  
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
  
//list object (get bucket)
cos_list_object_params_t *list_params = NULL;
list_params = cos_create_list_object_params(p);
cos_str_set(&list_params->encoding_type, "url");
cos_str_set(&list_params->prefix, "folder/");
cos_str_set(&marker, "");
while (is_truncated) {
	list_params->marker = marker;
	s = cos_list_object(options, &bucket, list_params, &resp_headers);
	if (! cos_status_is_ok(s)) {
		printf("list object failed, req_id:%s\n", s->req_id);
		break;
	}
	cos_list_object_content_t *content = NULL;
	cos_list_for_each_entry(cos_list_object_content_t, content, &list_params->object_list, node) {
        s = cos_delete_object(options, &bucket, &content->key, &resp_headers);
        if (! cos_status_is_ok(s)) {
            printf("delete object[%s] failed, req_id:%s\n", content->key.data, s->req_id);
        }
	}
	is_truncated = list_params->truncated;
	marker = list_params->next_marker;
}    
cos_pool_destroy(p);
```



## 멀티파트 작업

### 멀티파트 업로드 조회

#### 기능 설명

현재 진행 중인 멀티파트 업로드 정보를 조회합니다. 한 번에 최대 1000의 현재 진행 중인 멀티파트 업로드를 나열합니다.

#### 메소드 프로토타입

```cpp
cos_status_t *cos_list_multipart_upload(const cos_request_options_t *options,
                                        const cos_string_t *bucket, 
                                        cos_list_multipart_upload_params_t *params, 
                                        cos_table_t **resp_headers);
```

#### 매개변수 설명

| 매개변수 이름              | 매개변수 설명                                                     | 유형    |
| --------------------- | ------------------------------------------------------------ | ------- |
| options               | COS 요청 옵션                                                 | Struct  |
| bucket                | 버킷 이름. 버킷의 이름 생성 포맷은 BucketName-APPID로 여기에 입력하는 버킷 이름은 반드시 해당 포맷을 따라야 함 | String  |
| params                | List Multipart Uploads 작업 매개변수                              | Struct  |
| encoding_type         | 규정된 반환 값의 인코딩 방식                                         | String  |
| prefix                | 접두사 매칭, 반환 파일의 접두사 주소 규정에 사용                         | String  |
| delimiter             | 세퍼레이터는 하나의 부호입니다. <br><li>Prefix가 있으면 Prefix부터 delimiter 사이의 동일한 경로를 하나로 분류하고 Common Prefix로 정의한 다음 모든 Common Prefix를 나열합니다. <br><li>Prefix가 없으면 경로의 시작점부터 시작합니다. | String  |
| max_ret               | 한 번에 반환하는 최대 항목 수, 기본값: 1000                             | String  |
| key_marker            | upload-id-marker와 함께 사용합니다. <br><li>upload-id-marker가 지정되지 않은 경우 ObjectName 알파벳 순서가 key-marker보다 큰 항목이 나열되며, <br><li>upload-id-marker가 지정된 경우 ObjectName 알파벳 순서가 key-marker보다 큰 항목이 나열됩니다. ObjectName 알파벳 순서가 key-marker와 동일하고 UploadID가 upload-id-marker보다 큰 항목이 나열됩니다. | String  |
| upload_id_marker      | key-marker와 함께 사용합니다. <br><li>key-marker가 지정되지 않은 경우 upload-id-marker는 무시되며, <br><li> key-marker가 지정된 경우 ObjectName 알파벳 순서가 key-marker보다 큰 항목이 나열됩니다. ObjectName 알파벳 순서가 key-marker와 동일하고 UploadID가 upload-id-marker보다 큰 항목이 나열됩니다. | String  |
| truncated             | 반환 항목의 잘림 여부는 ’true’ 또는 ’false’                      | Boolean |
| next_key_marker       | 반환 항목이 잘린 경우, 반환된 NextKeyMarker가 다음 항목의 시작점이 됨   | String  |
| next_upload_id_marker | 반환 항목이 잘린 경우, 반환된 UploadId가 다음 항목의 시작점이 됨     | String  |
| upload_list           | 멀티파트 업로드 정보                                               | Struct  |
| key                   | Object 이름                                                | String  |
| upload_id             | 이번 멀티파트 업로드의 ID                                        | String  |
| initiated             | 이번 멀티파트 업로드 작업의 실행 시간                               | String  |
| resp_headers          | HTTP 응답 메시지의 헤더 필드 반환                                     | Struct  |

```
typedef struct {
    cos_list_t node;
    cos_string_t key;
    cos_string_t upload_id;
    cos_string_t initiated;
} cos_list_multipart_upload_content_t;
```

#### 반환 결과 설명

| 반환 결과   | 설명        | 유형   |
| ---------- | ----------- | ------ |
| code       | 에러 코드      | Int    |
| error_code | 에러 코드 내용  | String |
| error_msg  | 에러 코드 설명  | String |
| req_id     | 메시지 ID 요청 | String |

#### 예시

```cpp
cos_pool_t *p = NULL;
cos_string_t bucket;
int is_cname = 0;
cos_table_t *resp_headers = NULL;
cos_request_options_t *options = NULL;
cos_status_t *s = NULL;
cos_list_multipart_upload_params_t *list_multipart_params = NULL;

//메모리 풀 생성 & 초기화 요청 옵션
cos_pool_create(&p, NULL);
options = cos_request_options_create(p);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
cos_str_set(&bucket, TEST_BUCKET_NAME);

//멀티파트 업로드 조회
list_multipart_params = cos_create_list_multipart_upload_params(p);
list_multipart_params->max_ret = 999;
s = cos_list_multipart_upload(options, &bucket, list_multipart_params, &resp_headers);
log_status(s);

//메모리 풀 폐기
cos_pool_destroy(p);

```

### 멀티파트 업로드 초기화

#### 기능 설명

Initiate Multipart Uploads 요청은 멀티파트 업로드 초기화를 구현합니다. 요청을 성공적으로 처리하면 다음 Upload Part 요청에 사용할 Upload ID를 반환합니다.

#### 메소드 프로토타입

```cpp
cos_status_t *cos_init_multipart_upload(const cos_request_options_t *options, 
                                        const cos_string_t *bucket, 
                                        const cos_string_t *object, 
                                        cos_string_t *upload_id, 
                                        cos_table_t *headers,
                                        cos_table_t **resp_headers);
```

#### 매개변수 설명

| 매개변수 이름     | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| options      | COS 요청 옵션                                                 | Struct |
| bucket       | 버킷 이름. 버킷의 이름 생성 포맷은 BucketName-APPID로 여기에 입력하는 버킷 이름은 반드시 해당 포맷을 따라야 함 | String |
| object       | Object 이름                                                  | String |
| upload_id    | 작업에서 반환한 Upload ID                                         | String |
| headers      | COS에서 부가 헤더 필드 요청                                             | Struct |
| resp_headers | HTTP 응답 메시지의 헤더 필드 반환                                     | Struct |

#### 반환 결과 설명

| 반환 결과   | 설명        | 유형   |
| ---------- | ----------- | ------ |
| code       | 에러 코드      | Int    |
| error_code | 에러 코드 내용  | String |
| error_msg  | 에러 코드 설명  | String |
| req_id     | 메시지 ID 요청 | String |

#### 예시

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_string_t file;
cos_table_t *resp_headers = NULL;

//메모리 풀 생성
cos_pool_create(&p, NULL);

//초기화 요청 옵션
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

//멀티파트 업로드 초기화
cos_str_set(&object, TEST_OBJECT_NAME);
s = cos_init_multipart_upload(options, &bucket, &object, 
                              &upload_id, headers, &resp_headers);
if (cos_status_is_ok(s)) {
    printf("init multipart upload succeeded\n");
} else {
    printf("init multipart upload failed\n");
}

//메모리 풀 폐기
cos_pool_destroy(p); 
```



### 멀티파트 업로드

#### 기능 설명

파일을 멀티파트 업로드합니다. Upload Part는 초기화 이후의 멀티파트 업로드를 요청합니다. 지원되는 파트의 수는 1 - 10000개이며, 파트의 크기는 1MB - 5GB입니다. Upload Part를 요청할 때마다 partNumber와 uploadID가 필요합니다. partNumber는 파트의 번호이며, 비순차적 업로드를 지원합니다.

#### 메소드 프로토타입

```cpp
cos_status_t *cos_upload_part_from_file(const cos_request_options_t *options,
                                        const cos_string_t *bucket, 
                                        const cos_string_t *object,
                                        const cos_string_t *upload_id, 
                                        int part_num, 
                                        cos_upload_file_t *upload_file,
                                        cos_table_t **resp_headers);
```

#### 매개변수 설명

| 매개변수 이름     | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| options      | COS 요청 옵션                                                 | Struct |
| bucket       | 버킷 이름. 버킷의 이름 생성 포맷은 BucketName-APPID로 여기에 입력하는 버킷 이름은 반드시 해당 포맷을 따라야 함 | String |
| object       | Object 이름                                                  | String |
| upload_id    | 업로드 작업 번호                                                 | String |
| part_num     | 멀티파트 번호                                                     | Int    |
| upload_file  | 업로드 대기 로컬 파일 정보                                           | Struct |
| resp_headers | HTTP 응답 메시지의 헤더 필드 반환                                     | Struct |

#### 반환 결과 설명

| 반환 결과   | 설명        | 유형   |
| ---------- | ----------- | ------ |
| code       | 에러 코드      | Int    |
| error_code | 에러 코드 내용  | String |
| error_msg  | 에러 코드 설명  | String |
| req_id     | 메시지 ID 요청 | String |

#### 예시

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_string_t file;
cos_table_t *resp_headers = NULL;
int part_num = 1;
int64_t pos = 0;
int64_t file_length = 0;

//메모리 풀 생성
cos_pool_create(&p, NULL);

//초기화 요청 옵션
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

//멀티파트 업로드
int res = COSE_OK;
cos_upload_file_t *upload_file = NULL;
cos_file_buf_t *fb = cos_create_file_buf(p);
res = cos_open_file_for_all_read(p, TEST_MULTIPART_FILE, fb);
if (res != COSE_OK) {
    cos_error_log("Open read file fail, filename:%s\n", TEST_MULTIPART_FILE);
    return;
}
file_length = fb->file_last;
apr_file_close(fb->file);
while(pos < file_length) {
    upload_file = cos_create_upload_file(p);
    cos_str_set(&upload_file->filename, TEST_MULTIPART_FILE);
    upload_file->file_pos = pos;
    pos += 2 * 1024 * 1024;
    upload_file->file_last = pos < file_length ? pos : file_length; //2MB
    s = cos_upload_part_from_file(options, &bucket, &object, &upload_id,
                                  part_num++, upload_file, &resp_headers);

    if (cos_status_is_ok(s)) {
        printf("upload part succeeded\n");
    } else {
        printf("upload part failed\n");
    }
}

//메모리 풀 폐기
cos_pool_destroy(p); 
```

### 멀티파트 복사

#### 기능 설명

다른 객체를 한 파트로 복사합니다.

#### 메소드 프로토타입

```cpp
cos_status_t *cos_upload_part_copy(const cos_request_options_t *options,
                                   cos_upload_part_copy_params_t *params, 
                                   cos_table_t *headers, 
                                   cos_table_t **resp_headers);
```

#### 매개변수 설명

| 매개변수 이름     | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| options      | COS 요청 옵션                                                 | Struct |
| params       | 멀티파트 매개변수 정보 복사                                             | Struct |
| copy_source  | 원본 파일 경로                                                 | String |
| dest_bucket  | 타깃 버킷 이름. 버킷의 이름 생성 포맷은 BucketName-APPID로 여기에 입력하는 버킷 이름은 반드시 해당 포맷을 따라야 함 | String |
| dest_object  | 타깃 Object 이름                                             | String |
| upload_id    | 업로드 작업 번호                                                 | String |
| part_num     | 멀티파트 번호                                                     | Int    |
| range_start  | 원본 파일 start offset                                               | Int    |
| range_end    | 원본 파일 end offset                                               | Int    |
| rsp_content  | 멀티파트 결과 정보 복사                                             | Struct |
| etag         | 반환 파일의 MD5 알고리즘 검증값                                    | String |
| last_modify  | 반환 파일의 최종 수정 시간, GMT 포맷                               | String |
| resp_headers | HTTP 응답 메시지의 헤더 필드 반환                                     | Struct |

#### 반환 결과 설명

| 반환 결과   | 설명        | 유형   |
| ---------- | ----------- | ------ |
| code       | 에러 코드      | Int    |
| error_code | 에러 코드 내용  | String |
| error_msg  | 에러 코드 설명  | String |
| req_id     | 메시지 ID 요청 | String |

#### 예시

```cpp
cos_pool_t *p = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_string_t file;
int is_cname = 0;
cos_string_t upload_id;
cos_list_upload_part_params_t *list_upload_part_params = NULL;
cos_upload_part_copy_params_t *upload_part_copy_params1 = NULL;
cos_upload_part_copy_params_t *upload_part_copy_params2 = NULL;
cos_table_t *headers = NULL;
cos_table_t *query_params = NULL;
cos_table_t *resp_headers = NULL;
cos_table_t *list_part_resp_headers = NULL;
cos_list_t complete_part_list;
cos_list_part_content_t *part_content = NULL;
cos_complete_part_content_t *complete_content = NULL;
cos_table_t *complete_resp_headers = NULL;
cos_status_t *s = NULL;
int part1 = 1;
int part2 = 2;
char *local_filename = "test_upload_part_copy.file";
char *download_filename = "test_upload_part_copy.file.download";
char *source_object_name = "cos_test_upload_part_copy_source_object";
char *dest_object_name = "cos_test_upload_part_copy_dest_object";
FILE *fd = NULL;
cos_string_t download_file;
cos_string_t dest_bucket;
cos_string_t dest_object;
int64_t range_start1 = 0;
int64_t range_end1 = 6000000;
int64_t range_start2 = 6000001;
int64_t range_end2;
cos_string_t data;

cos_pool_create(&p, NULL);
options = cos_request_options_create(p);

//임의의 10MB 로컬 파일 생성    
make_rand_string(p, 10 * 1024 * 1024, &data);
fd = fopen(local_filename, "w");
fwrite(data.data, sizeof(data.data[0]), data.len, fd);
fclose(fd);    

//로컬 파일로 객체 업로드
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
cos_str_set(&bucket, "source-1253666666");
cos_str_set(&object, "cos_test_upload_part_copy_source_object");
cos_str_set(&file, local_filename);
s = cos_put_object_from_file(options, &bucket, &object, &file, NULL, &resp_headers);
log_status(s);

//멀티파트 업로드 초기화
cos_str_set(&object, dest_object_name);
s = cos_init_multipart_upload(options, &bucket, &object, 
                              &upload_id, NULL, &resp_headers);
log_status(s);

//업로드된 객체로 멀티파트1 복사
upload_part_copy_params1 = cos_create_upload_part_copy_params(p);
cos_str_set(&upload_part_copy_params1->copy_source, "mybucket-1253666666.cn-south.myqcloud.com/cos_test_upload_part_copy_source_object");
cos_str_set(&upload_part_copy_params1->dest_bucket, TEST_BUCKET_NAME);
cos_str_set(&upload_part_copy_params1->dest_object, dest_object_name);
cos_str_set(&upload_part_copy_params1->upload_id, upload_id.data);
upload_part_copy_params1->part_num = part1;
upload_part_copy_params1->range_start = range_start1;
upload_part_copy_params1->range_end = range_end1;
headers = cos_table_make(p, 0);
s = cos_upload_part_copy(options, upload_part_copy_params1, headers, &resp_headers);
log_status(s);
printf("last modified:%s, etag:%s\n", upload_part_copy_params1->rsp_content->last_modify.data, upload_part_copy_params1->rsp_content->etag.data);

//업로드된 객체로 멀티파트2 복사
resp_headers = NULL;
range_end2 = get_file_size(local_filename) - 1;
upload_part_copy_params2 = cos_create_upload_part_copy_params(p);
cos_str_set(&upload_part_copy_params2->copy_source, "mybucket-1253666666.cn-south.myqcloud.com/cos_test_upload_part_copy_source_object");
cos_str_set(&upload_part_copy_params2->dest_bucket, TEST_BUCKET_NAME);
cos_str_set(&upload_part_copy_params2->dest_object, dest_object_name);
cos_str_set(&upload_part_copy_params2->upload_id, upload_id.data);
upload_part_copy_params2->part_num = part2;
upload_part_copy_params2->range_start = range_start2;
upload_part_copy_params2->range_end = range_end2;
headers = cos_table_make(p, 0);
s = cos_upload_part_copy(options, upload_part_copy_params2, headers, &resp_headers);
log_status(s);
printf("last modified:%s, etag:%s\n", upload_part_copy_params1->rsp_content->last_modify.data, upload_part_copy_params1->rsp_content->etag.data);

//업로드된 객체 나열
list_upload_part_params = cos_create_list_upload_part_params(p);
list_upload_part_params->max_ret = 10;
cos_list_init(&complete_part_list);

cos_str_set(&dest_bucket, TEST_BUCKET_NAME);
cos_str_set(&dest_object, dest_object_name);
s = cos_list_upload_part(options, &dest_bucket, &dest_object, &upload_id, 
                         list_upload_part_params, &list_part_resp_headers);
log_status(s);
cos_list_for_each_entry(cos_list_part_content_t, part_content, &list_upload_part_params->part_list, node) {
    complete_content = cos_create_complete_part_content(p);
    cos_str_set(&complete_content->part_number, part_content->part_number.data);
    cos_str_set(&complete_content->etag, part_content->etag.data);
    cos_list_add_tail(&complete_content->node, &complete_part_list);
}

//멀티파트 업로드 완료
headers = cos_table_make(p, 0);
s = cos_complete_multipart_upload(options, &dest_bucket, &dest_object, 
                                  &upload_id, &complete_part_list, headers, &complete_resp_headers);
log_status(s);

//복사한 멀티파트 업로드로 생성한 객체와 로컬 파일의 매칭 여부 대조
headers = cos_table_make(p, 0);
cos_str_set(&download_file, download_filename);
s = cos_get_object_to_file(options, &dest_bucket, &dest_object, headers, 
                           query_params, &download_file, &resp_headers);
log_status(s);
printf("local file len = %"APR_INT64_T_FMT", download file len = %"APR_INT64_T_FMT, get_file_size(local_filename), get_file_size(download_filename));
remove(download_filename);
remove(local_filename);

//메모리 풀 폐기
cos_pool_destroy(p);    
```



### 업로드된 파트 조회

#### 기능 설명

특정 멀티파트 업로드 작업에서 업로드된 파트를 조회합니다.

#### 메소드 프로토타입

```cpp
cos_status_t *cos_list_upload_part(const cos_request_options_t *options,
                                   const cos_string_t *bucket, 
                                   const cos_string_t *object, 
                                   const cos_string_t *upload_id, 
                                   cos_list_upload_part_params_t *params,
                                   cos_table_t **resp_headers);
```

#### 매개변수 설명

| 매개변수 이름                | 매개변수 설명                                                     | 유형    |
| ----------------------- | ------------------------------------------------------------ | ------- |
| options                 | COS 요청 옵션                                                 | Struct  |
| bucket                  | 버킷 이름. 버킷의 이름 생성 포맷은 BucketName-APPID로 여기에 입력하는 버킷 이름은 반드시 해당 포맷을 따라야 함 | String  |
| object                  | Object 이름                                                  | String  |
| upload_id               | 업로드 작업 번호                                                 | String  |
| params                  | List Parts 작업 매개변수                                          | Struct  |
| part_number_marker      | 기본적으로 UTF-8 이진법 순서로 열거되며, 모든 열거 값은 marker부터 시작  | String  |
| encoding_type           | 규정된 반환 값의 인코딩 방식                                         | String  |
| max_ret                 | 한 번에 반환하는 최대 항목 수, 기본값: 1000                             | String  |
| truncated               | 반환 항목의 잘림 여부는 ’true’ 또는 ’false’                      | Boolean |
| next_part_number_marker | 반환 항목이 잘린 경우, 반환된 NextMarker가 다음 항목의 시작점이 됨   | String  |
| part_list               | 완료된 파트의 정보                                               | Struct  |
| part_number             | 멀티파트 번호                                                     | String  |
| size                    | 멀티파트 크기, 단위: Byte                                          | String  |
| etag                    | 멀티파트의 SHA-1 알고리즘 검증값                                      | String  |
| last_modified           | 멀티파트 최종 수정 시간                                             | String  |
| resp_headers            | HTTP 응답 메시지의 헤더 필드 반환                                     | Struct  |

#### 반환 결과 설명

| 반환 결과   | 설명        | 유형   |
| ---------- | ----------- | ------ |
| code       | 에러 코드      | Int    |
| error_code | 에러 코드 내용  | String |
| error_msg  | 에러 코드 설명  | String |
| req_id     | 메시지 ID 요청 | String |

#### 예시

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_string_t file;
cos_table_t *resp_headers = NULL;
cos_list_part_content_t *part_content = NULL;
cos_complete_part_content_t *complete_part_content = NULL;
int part_num = 1;
int64_t pos = 0;
int64_t file_length = 0;

//메모리 풀 생성
cos_pool_create(&p, NULL);

//초기화 요청 옵션
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

//업로드된 파트 조회
params = cos_create_list_upload_part_params(p);
params->max_ret = 1000;
cos_list_init(&complete_part_list);
s = cos_list_upload_part(options, &bucket, &object, &upload_id, 
                         params, &resp_headers);

if (cos_status_is_ok(s)) {
    printf("List multipart succeeded\n");
} else {
    printf("List multipart failed\n");
    cos_pool_destroy(p);
    return;
}

cos_list_for_each_entry(cos_list_part_content_t, part_content, &params->part_list, node) {
    complete_part_content = cos_create_complete_part_content(p);
    cos_str_set(&complete_part_content->part_number, part_content->part_number.data);
    cos_str_set(&complete_part_content->etag, part_content->etag.data);
    cos_list_add_tail(&complete_part_content->node, &complete_part_list);
}

//멀티파트 업로드 완료
s = cos_complete_multipart_upload(options, &bucket, &object, &upload_id,
                                  &complete_part_list, complete_headers, &resp_headers);

if (cos_status_is_ok(s)) {
    printf("Complete multipart upload from file succeeded, upload_id:%.*s\n", 
           upload_id.len, upload_id.data);
} else {
    printf("Complete multipart upload from file failed\n");
}

//메모리 풀 폐기
cos_pool_destroy(p); 
```






### 멀티파트 업로드 완료

#### 기능 설명

전체 파일의 멀티파트 업로드를 완료합니다. Upload Parts로 모든 파트를 업로드한 후, 해당 API로 업로드를 완료할 수 있습니다. 해당 API 사용 시 반드시 Body에서 각 파트의 PartNumber와 ETag로 파트의 정확성을 검증해야 합니다.

#### 메소드 프로토타입

```cpp
cos_status_t *cos_complete_multipart_upload(const cos_request_options_t *options,
                                            const cos_string_t *bucket, 
                                            const cos_string_t *object, 
                                            const cos_string_t *upload_id, 
                                            cos_list_t *part_list, 
                                            cos_table_t *headers,
                                            cos_table_t **resp_headers);
```

#### 매개변수 설명

| 매개변수 이름     | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| options      | COS 요청 옵션                                                 | Struct |
| bucket       | 버킷 이름. 버킷의 이름 생성 포맷은 BucketName-APPID로 여기에 입력하는 버킷 이름은 반드시 해당 포맷을 따라야 함 | String |
| object       | Object 이름                                                  | String |
| upload_id    | 업로드 작업 번호                                                 | String |
| part_list    | 멀티파트 업로드가 완료된 매개변수                                           | Struct |
| part_number  | 멀티파트 번호                                                     | String |
| etag         | 멀티파트의 ETag 값은 sha1의 검증값이며, 검증값 앞뒤에 큰따옴표를 붙여야 합니다. 예시: "3a0f1fd698c235af9cf098cb74aa25bc" | String |
| headers      | COS에서 부가 헤더 필드 요청                                             | Struct |
| resp_headers | HTTP 응답 메시지의 헤더 필드 반환                                     | Struct |

#### 반환 결과 설명

| 반환 결과   | 설명        | 유형   |
| ---------- | ----------- | ------ |
| code       | 에러 코드      | Int    |
| error_code | 에러 코드 내용  | String |
| error_msg  | 에러 코드 설명  | String |
| req_id     | 메시지 ID 요청 | String |

#### 예시

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_string_t file;
cos_table_t *resp_headers = NULL;
cos_list_part_content_t *part_content = NULL;
cos_complete_part_content_t *complete_part_content = NULL;
int part_num = 1;
int64_t pos = 0;
int64_t file_length = 0;

//메모리 풀 생성
cos_pool_create(&p, NULL);

//초기화 요청 옵션
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

//업로드된 멀티파트 조회
params = cos_create_list_upload_part_params(p);
params->max_ret = 1000;
cos_list_init(&complete_part_list);
s = cos_list_upload_part(options, &bucket, &object, &upload_id, 
                         params, &resp_headers);

if (cos_status_is_ok(s)) {
    printf("List multipart succeeded\n");
} else {
    printf("List multipart failed\n");
    cos_pool_destroy(p);
    return;
}

cos_list_for_each_entry(cos_list_part_content_t, part_content, &params->part_list, node) {
    complete_part_content = cos_create_complete_part_content(p);
    cos_str_set(&complete_part_content->part_number, part_content->part_number.data);
    cos_str_set(&complete_part_content->etag, part_content->etag.data);
    cos_list_add_tail(&complete_part_content->node, &complete_part_list);
}

//멀티파트 업로드 완료
s = cos_complete_multipart_upload(options, &bucket, &object, &upload_id,
                                  &complete_part_list, complete_headers, &resp_headers);

if (cos_status_is_ok(s)) {
    printf("Complete multipart upload from file succeeded, upload_id:%.*s\n", 
           upload_id.len, upload_id.data);
} else {
    printf("Complete multipart upload from file failed\n");
}

//메모리 풀 폐기
cos_pool_destroy(p); 
```

### 멀티파트 업로드 중지

#### 기능 설명

멀티파트 업로드 작업을 중지하고 업로드된 파트를 삭제합니다. Abort Multipart Upload 호출 시 해당 Upload Parts를 사용한 파트 업로드 요청이 있는 경우 Upload Parts는 실패를 반환하게 됩니다.

#### 메소드 프로토타입

```cpp
cos_status_t *cos_abort_multipart_upload(const cos_request_options_t *options,
                                         const cos_string_t *bucket, 
                                         const cos_string_t *object, 
                                         cos_string_t *upload_id, 
                                         cos_table_t **resp_headers);
```

#### 매개변수 설명

| 매개변수 이름     | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| options      | COS 요청 옵션                                                 | Struct |
| bucket       | 버킷 이름. 버킷의 이름 생성 포맷은 BucketName-APPID로 여기에 입력하는 버킷 이름은 반드시 해당 포맷을 따라야 함 | String |
| object       | Object 이름                                                  | String |
| upload_id    | 업로드 작업 번호                                                 | String |
| resp_headers | HTTP 응답 메시지의 헤더 필드 반환                                     | Struct |

#### 반환 결과 설명

| 반환 결과   | 설명        | 유형   |
| ---------- | ----------- | ------ |
| code       | 에러 코드      | Int    |
| error_code | 에러 코드 내용  | String |
| error_msg  | 에러 코드 설명  | String |
| req_id     | 메시지 ID 요청 | String |

#### 예시

```cpp
cos_pool_t *p = NULL;
cos_string_t bucket;
cos_string_t object;
int is_cname = 0;
cos_table_t *headers = NULL;
cos_table_t *resp_headers = NULL;
cos_request_options_t *options = NULL;
cos_string_t upload_id;
cos_status_t *s = NULL;

//메모리 풀 생성 & 초기화 요청 옵션
cos_pool_create(&p, NULL);
options = cos_request_options_create(p);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
headers = cos_table_make(p, 1);
cos_str_set(&bucket, TEST_BUCKET_NAME);
cos_str_set(&object, TEST_MULTIPART_OBJECT);

//멀티파트 업로드 초기화
s = cos_init_multipart_upload(options, &bucket, &object, 
                              &upload_id, headers, &resp_headers);

if (cos_status_is_ok(s)) {
    printf("Init multipart upload succeeded, upload_id:%.*s\n", 
           upload_id.len, upload_id.data);
} else {
    printf("Init multipart upload failed\n"); 
    cos_pool_destroy(p);
    return;
}

//멀티파트 업로드 중지
s = cos_abort_multipart_upload(options, &bucket, &object, &upload_id, 
                               &resp_headers);

if (cos_status_is_ok(s)) {
    printf("Abort multipart upload succeeded, upload_id::%.*s\n", 
           upload_id.len, upload_id.data);
} else {
    printf("Abort multipart upload failed\n"); 
}    

//메모리 풀 폐기
cos_pool_destroy(p);
```

## 기타 작업

### 보관된 객체 복구

#### 기능 설명

아카이브 유형의 객체를 검색 및 액세스합니다.

#### 메소드 프로토타입

```cpp
cos_status_t *cos_post_object_restore(const cos_request_options_t *options,
                                      const cos_string_t *bucket, 
                                      const cos_string_t *object,
                                      cos_object_restore_params_t *restore_params,
                                      cos_table_t *headers,
                                      cos_table_t *params,
                                      cos_table_t **resp_headers);
```

#### 매개변수 설명

| 매개변수 이름       | 매개변수 설명                                                     | 유형   |
| -------------- | ------------------------------------------------------------ | ------ |
| options        | COS 요청 옵션                                                 | Struct |
| bucket         | 버킷 이름. 버킷의 이름 생성 포맷은 BucketName-APPID로 여기에 입력하는 버킷 이름은 반드시 해당 포맷을 따라야 함 | String |
| object         | Object 이름                                                  | String |
| restore_params | Post Object Restore 작업 매개변수                                 | Struct |
| days           | Post Object Restore 작업에 설정된 임시 사본 만료 시간               | Int    |
| tier           | Post Object Restore 작업에 지정된 세 가지 아카이브 스토리지 지원 복구 유형: Expedited, Standard, Bulk | String |
| headers        | COS에서 부가 헤더 필드 요청                                             | Struct |
| params         | COS에서 작업 매개변수 요청                                             | Struct |
| resp_headers   | HTTP 응답 메시지의 헤더 필드 반환                                     | Struct |

#### 반환 결과 설명

| 반환 결과   | 설명        | 유형   |
| ---------- | ----------- | ------ |
| code       | 에러 코드      | Int    |
| error_code | 에러 코드 내용  | String |
| error_msg  | 에러 코드 설명  | String |
| req_id     | 메시지 ID 요청 | String |

#### 예시

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_table_t *resp_headers = NULL;

//메모리 풀 생성
cos_pool_create(&p, NULL);

//초기화 요청 옵션
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);
cos_str_set(&object, TEST_OBJECT_NAME);

//보관된 객체 복구
cos_object_restore_params_t *restore_params = cos_create_object_restore_params(p);
restore_params->days = 30;
cos_str_set(&restore_params->tier, "Standard");
s = cos_post_object_restore(options, &bucket, &object, restore_params, NULL, NULL, &resp_headers);
if (cos_status_is_ok(s)) {
    printf("post object restore succeeded\n");
} else {
    printf("post object restore failed\n");
}

//메모리 풀 폐기
cos_pool_destroy(p); 
```

### 객체 ACL 설정

#### 기능 설명

버킷 내 객체의 액세스 제어 리스트를 설정합니다.

#### 메소드 프로토타입

```cpp
cos_status_t *cos_put_object_acl(const cos_request_options_t *options, 
                                 const cos_string_t *bucket,
                                 const cos_string_t *object,  
                                 cos_acl_e cos_acl,
                                 const cos_string_t *grant_read,
                                 const cos_string_t *grant_write,
                                 const cos_string_t *grant_full_ctrl,
                                 cos_table_t **resp_headers);
```

#### 매개변수 설명

| 매개변수 이름        | 매개변수 설명                                                     | 유형   |
| --------------- | ------------------------------------------------------------ | ------ |
| options         | COS 요청 옵션                                                 | Struct |
| bucket          | 버킷 이름. 버킷의 이름 생성 포맷은 BucketName-APPID로 여기에 입력하는 버킷 이름은 반드시 해당 포맷을 따라야 함 | String |
| object          | Object 이름                                                  | String |
| cos_acl         | 사용자 정의 권한 허용. 유효값: COS_ACL_PRIVATE(0)，COS_ACL_PUBLIC_READ(1), COS_ACL_PUBLIC_READ_WRITE(2)<br>기본값: COS_ACL_PRIVATE(0) | Enum   |
| grant_read      |권한 수여자에게 객체 읽기 권한 부여. 형식: id="[OwnerUin]", 예: id="100000000001". 쉼표(,)를 사용하여 여러 인증자 그룹 구분 가능. 예: `id="100000000001",id="100000000002"`   | String |
| grant_write     |승인된 자에게 객체 쓰기 권한 부여. 형식: id="[OwnerUin]", 예: id="100000000001". 쉼표(,)를 사용하여 여러 권한 수여자 그룹 구분 가능. 예: `id="100000000001",id="100000000002"`   | String |
| grant_full_ctrl | 권한 수여자에게 버킷 작업의 모든 권한 부여. 형식: id="[OwnerUin]", 예: id="100000000001". 쉼표(,)를 사용하여 여러 권한 수여자 그룹 구분 가능. 예: `id="100000000001",id="100000000002"`   | String |
| resp_headers    | HTTP 응답 메시지의 헤더 필드 반환                                     | Struct |

>?자세한 내용은 API 문서 [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) 및 [ACL 개요](https://intl.cloud.tencent.com/document/product/436/30583)를 참고하시기 바랍니다.

#### 반환 결과 설명

| 반환 결과   | 설명        | 유형   |
| ---------- | ----------- | ------ |
| code       | 에러 코드      | Int    |
| error_code | 에러 코드 내용  | String |
| error_msg  | 에러 코드 설명  | String |
| req_id     | 메시지 ID 요청 | String |

#### 예시

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_table_t *resp_headers = NULL;

//메모리 풀 생성
cos_pool_create(&p, NULL);

//초기화 요청 옵션
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

//객체 ACL 설정
cos_str_set(&object, TEST_OBJECT_NAME);
cos_string_t read;
cos_str_set(&read, "id=\"qcs::cam::uin/12345:uin/12345\", id=\"qcs::cam::uin/45678:uin/45678\"");
s = cos_put_object_acl(options, &bucket, &object, cos_acl, &read, NULL, NULL, &resp_headers);
if (cos_status_is_ok(s)) {
    printf("put object acl succeeded\n");
} else {
    printf("put object acl failed\n");
}

//메모리 풀 폐기
cos_pool_destroy(p);  
```

### 객체 ACL 조회

#### 기능 설명

객체의 액세스 제어 리스트를 조회합니다.

#### 메소드 프로토타입

```cpp
cos_status_t *cos_get_object_acl(const cos_request_options_t *options, 
                                 const cos_string_t *bucket,
                                 const cos_string_t *object,
                                 cos_acl_params_t *acl_param, 
                                 cos_table_t **resp_headers)
```

#### 매개변수 설명

| 매개변수 이름     | 매개변수 설명                                                     | 유형   |
| ------------ | ------------------------------------------------------------ | ------ |
| options      | COS 요청 옵션                                                 | Struct |
| bucket       | 버킷 이름. 버킷의 이름 생성 포맷은 BucketName-APPID로 여기에 입력하는 버킷 이름은 반드시 해당 포맷을 따라야 함 | String |
| object       | Object 이름                                                  | String |
| acl_param    | 작업 매개변수 요청                                                 | Struct |
| owner_id     | 작업에서 반환한 Bucket 소유자 ID 요청                              | String |
| owner_name   | 작업에서 반환한 Bucket 소유자 이름 요청                           | String |
| object_list  | 작업에서 반환한 권한 피부여자 정보와 권한 정보 요청                         | Struct |
| type         | 작업에서 반환한 권한 피부여자 계정 유형 요청                               | String |
| id           | 작업에서 반환한 권한 피부여자의 사용자 ID 요청                                | String |
| name         | 작업에서 반환한 권한 피부여자의 사용자 이름 요청                               | String |
| permission   | 작업에서 반환한 권한 피부여자의 권한 정보 요청                               | String |
| resp_headers | HTTP 응답 메시지의 헤더 필드 반환                                     | Struct |

#### 반환 결과 설명

| 반환 결과   | 설명        | 유형   |
| ---------- | ----------- | ------ |
| code       | 에러 코드      | Int    |
| error_code | 에러 코드 내용  | String |
| error_msg  | 에러 코드 설명  | String |
| req_id     | 메시지 ID 요청 | String |

#### 예시

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_table_t *resp_headers = NULL;

//메모리 풀 생성
cos_pool_create(&p, NULL);

//초기화 요청 옵션
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

//객체 ACL 획득
cos_acl_params_t *acl_params2 = NULL;
acl_params2 = cos_create_acl_params(p);
s = cos_get_object_acl(options, &bucket, &object, acl_params2, &resp_headers);
if (cos_status_is_ok(s)) {
    printf("get object acl succeeded\n");
    printf("acl owner id:%s, name:%s\n", acl_params2->owner_id.data, acl_params2->owner_name.data);
    acl_content = NULL;
    cos_list_for_each_entry(cos_acl_grantee_content_t, acl_content, &acl_params2->grantee_list, node) {
        printf("acl grantee id:%s, name:%s, permission:%s\n", acl_content->id.data, acl_content->name.data, acl_content->permission.data);
    }
} else {
    printf("get object acl failed\n");
}

//메모리 풀 폐기
cos_pool_destroy(p); 
```

## 고급 인터페이스(권장)

### 객체 업로드(중단된 지점부터 이어서 전송)

#### 기능 설명

업로드 인터페이스는 사용자의 파일 길이에 따라 자동으로 데이터를 분할하여 사용이 편리합니다. 사용자는 멀티파트 업로드의 모든 절차를 신경 쓸 필요가 없으며, 멀티파트 업로드가 완료되지 않은 파일에 대해 업로드가 중단된 지점부터 이어서 전송할 수 있습니다. 멀티파트 크기는 기본적으로 1048576(1MB)이며, part_size 매개변수를 통해 조정할 수 있습니다. 

#### 메소드 프로토타입

```cpp
cos_status_t *cos_resumable_upload_file(cos_request_options_t *options,
                                          cos_string_t *bucket,
                                          cos_string_t *object,
                                          cos_string_t *filepath,
                                          cos_table_t *headers,
                                          cos_table_t *params,
                                          cos_resumable_clt_params_t *clt_params,
                                          cos_progress_callback progress_callback,
                                          cos_table_t **resp_headers,
                                          cos_list_t *resp_body)
```

#### 매개변수 설명

| 매개변수 이름          | 매개변수 설명                                                     | 유형   |
| ----------------- | ------------------------------------------------------------ | -------- |
| options           | COS 요청 옵션                                                 | Struct   |
| bucket            | 버킷 이름. 버킷의 이름 생성 포맷은 BucketName-APPID로 여기에 입력하는 버킷 이름은 반드시 해당 포맷을 따라야 함 | String   |
| object            | Object 이름                                                  | String   |
| filepath          | Object 로컬 파일 이름                                          | String   |
| headers           | COS에서 부가 헤더 필드 요청                                             | Struct   |
| params            | COS에서 작업 매개변수 요청                                             | Struct   |
| clt_params        | 객체 업로드 제어 매개변수                                             | Struct   |
| part_size         | 파트 크기(단위: bytes), 사용자 지정 part_size가 1048576(1MB) 미만인 경우 C SDK에서 자동 분할, 멀티파트 크기는 기본적으로 1048576(1MB)이며, 멀티파트 수가 10,000을 초과하는 경우 파일 크기에 따라 조정 | Int      |
| thread_num        | 스레드 풀 크기, 기본값: 1                                          | Int      |
| enable_checkpoint | 중단된 지점부터 이어서 전송할 수 있는지 여부                                             | Int      |
| checkpoint_path   | 중단된 지점부터 이어서 전송할 수 있는 경우 업로드 진행률을 저장하는 파일 경로를 의미, 기본 경로는 `<filepath>.cp`이며 filepath는 Object 로컬 파일 이름 | String   |
| progress_callback | 업로드 진행률 콜백 함수                                             | Function |
| resp_headers      | HTTP 응답 메시지의 헤더 필드 반환                                     | Struct   |
| resp_body         | 멀티파트 업로드 요청 완료 시 반환된 데이터 저장                             | Struct   |

#### 반환 결과 설명

| 반환 결과   | 설명        | 유형   |
| ---------- | ----------- | ------ |
| code       | 에러 코드      | Int    |
| error_code | 에러 코드 내용  | String |
| error_msg  | 에러 코드 설명  | String |
| req_id     | 메시지 ID 요청 | String |

#### 예시

```c
cos_pool_t *p = NULL;
cos_string_t bucket;
cos_string_t object;
cos_string_t filename;
cos_status_t *s = NULL;
int is_cname = 0;
cos_table_t *headers = NULL;
cos_table_t *resp_headers = NULL;
cos_request_options_t *options = NULL;
cos_resumable_clt_params_t *clt_params;

cos_pool_create(&p, NULL);
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);

headers = cos_table_make(p, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);
cos_str_set(&object, TEST_MULTIPART_OBJECT);
cos_str_set(&filename, TEST_MULTIPART_FILE);

// 업로드 제어 매개변수 설정
clt_params = cos_create_resumable_clt_params_content(p, 0, 1, COS_TRUE, NULL);
// upload
s = cos_resumable_upload_file(options, &bucket, &object, &filename, headers, NULL,
						clt_params, NULL, &resp_headers, NULL);

if (cos_status_is_ok(s)) {
	printf("upload succeeded\n");
} else {
	printf("upload failed\n");
}

cos_pool_destroy(p);
```

### 객체 다운로드(중단된 지점부터 이어서 전송)

#### 기능 설명

멀티파트 다운로드 인터페이스는 사용자 객체 길이에 따라 자동으로 Range를 통해 데이터를 다운로드 하며, 동시 다운로드를 구현합니다. 멀티파트 크기는 기본적으로 1048576(1MB)이며, part_size 매개변수를 통해 조정할 수 있습니다.

#### 메소드 프로토타입

```cpp
cos_status_t *cos_resumable_download_file(cos_request_options_t *options,
                                          cos_string_t *bucket,
                                          cos_string_t *object,
                                          cos_string_t *filepath,
                                          cos_table_t *headers,
                                          cos_table_t *params,
                                          cos_resumable_clt_params_t *clt_params,
                                          cos_progress_callback progress_callback);
```

#### 매개변수 설명

| 매개변수 이름          | 매개변수 설명                                                     | 유형   |
| ----------------- | ------------------------------------------------------------ | -------- |
| options           | COS 요청 옵션                                                 | Struct   |
| bucket            | 버킷 이름. 버킷의 이름 생성 포맷은 BucketName-APPID로 여기에 입력하는 버킷 이름은 반드시 해당 포맷을 따라야 함 | String   |
| object            | Object 이름                                                  | String   |
| filepath          | Object 로컬 파일 이름                                          | String   |
| headers           | COS에서 부가 헤더 필드 요청                                             | Struct   |
| params            | COS에서 작업 매개변수 요청                                             | Struct   |
| clt_params        | 객체 다운로드 제어 매개변수                                             | Struct   |
| part_size         | 파트 크기(단위: bytes), 사용자 지정 part_size가 4194304(4MB) 미만인 경우 4194304(4MB)로 처리 | Int      |
| thread_num        | 스레드 풀 크기, 기본값: 1                                          | Int      |
| enable_checkpoint | 중단된 지점부터 이어서 전송할 수 있는지 여부                                             | Int      |
| checkpoint_path   | 중단된 지점부터 이어서 전송할 수 있는 경우 업로드 진행률을 저장하는 파일 경로를 의미, 기본 경로는 `<filepath>.cp`이며 filepath는 Object 로컬 파일 이름 | String   |
| progress_callback | 다운로드 진행률 콜백 함수                                             | Function |

#### 결과 설명

| 반환 결과   | 설명        | 유형   |
| ---------- | ----------- | ------ |
| code       | 에러 코드      | Int    |
| error_code | 에러 코드 내용  | String |
| error_msg  | 에러 코드 설명  | String |
| req_id     | 메시지 ID 요청 | String |

#### 예시

```c
cos_pool_t *p = NULL;
int is_cname = 0; 
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_string_t filepath;
cos_resumable_clt_params_t *clt_params;
      
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
cos_str_set(&object, TEST_MULTIPART_OBJECT);
cos_str_set(&filepath, TEST_DOWNLOAD_NAME);

clt_params = cos_create_resumable_clt_params_content(p, 5*1024*1024, 3, COS_FALSE, NULL);
s = cos_resumable_download_file(options, &bucket, &object, &filepath, NULL, NULL, clt_params, NULL);
if (cos_status_is_ok(s)) {
	printf("download succeeded\n");
} else {
	printf("download failed\n");
}
cos_pool_destroy(p);
```

### 객체 이동

#### 기능 설명

객체 이동에는 타깃 위치로 원본 객체 복사 및 원본 객체 삭제의 두 가지 주요 작업이 포함되어 있습니다.

COS는 버킷 이름(Bucket)과 객체 키(ObjectKey)로 객체를 식별하므로 객체를 이동하는 경우 해당 객체의 식별자를 수정해야 합니다. 현재 COS C SDK는 객체의 고유 식별자를 수정할 수 있는 개별 인터페이스를 제공하지 않습니다. 그러나 **객체 복사**와 **객체 삭제**를 함께 사용하는 기본 작업으로 객체 식별자를 수정하고 객체를 이동할 수 있습니다.

- 객체 복사 방법에 대한 자세한 내용은 [객체 복사 설정](#.E8.AE.BE.E7.BD.AE.E5.AF.B9.E8.B1.A1.E5.A4.8D.E5.88.B6.EF.BC.88.E4.BF.AE.E6.94.B9.E5.B1.9E.E6.80.A7.EF.BC.89)을 참고하십시오.
- 객체 삭제 방법에 대한 자세한 내용은 [객체 삭제](#.E5.88.A0.E9.99.A4.E5.8D.95.E4.B8.AA.E5.AF.B9.E8.B1.A1)를 참고하십시오.

#### 예시
```c
cos_pool_t *p = NULL;                                                                    
int is_cname = 0;                                                                        
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;                                                                     
cos_string_t src_object;                                                                 
cos_string_t src_endpoint;
cos_table_t *resp_headers = NULL;
  
//메모리 풀 생성
cos_pool_create(&p, NULL);                                                               
//초기화 요청 옵션
options = cos_request_options_create(p);                                                 
options->config = cos_config_create(options->pool);
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
cos_str_set(&bucket, TEST_BUCKET_NAME);

//객체 복사 설정
cos_str_set(&object, TEST_OBJECT_NAME1);
cos_str_set(&src_endpoint, "ap-guangzhou.myqcloud.com");
cos_str_set(&src_object, "example");
cos_copy_object_params_t *params = NULL;
params = cos_create_copy_object_params(p);
s = cos_copy_object(options, &bucket, &src_object, &src_endpoint, &bucket, &object, NULL, params, &resp_headers);
if (cos_status_is_ok(s)) {
	s = cos_delete_object(options, &bucket, &src_object, &resp_headers);
} else {
	printf("move object failed\n");
}
//메모리 풀 폐기
cos_pool_destroy(p);
```
	
	
