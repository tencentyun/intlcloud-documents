COS 서비스 XML C SDK 조작은 각 유형의 API에 해당하는 호출 결과를 반환하며, 호출 결과에는 응답 코드, 오류 코드, 오류 정보 등의 결과 정보가 포함됩니다. 자세한 정보는 문서 마지막에 있는 비정상에 관한 설명을 참조하십시오.
> 본문에서 나오는 SecretId, SecretKey, Bucket 등과 같은 이름의 의미 및 획득 방법은 [COS 용어집](https://cloud.tencent.com/document/product/436/7751)을 참조하십시오.

SDK에서 각 API를 사용하는 올바른 방법은 다음과 같습니다. 단, 뒤에 나오는 API 예시는 특정 비정상 처리를 더 이상 서술하지 않으며, API 사용 예시만 제공합니다.

```cpp
    cos_status_t *s = NULL;
    s = cos_put_object_from_file(options, &bucket, &object, &file, &headers, &resp_headers);
    if (!s && !cos_status_is_ok(s)) {
        // 필요에 따라 비정상 시나리오의 로그 출력 및 처리를 진행합니다
        cos_warn_log("failed to put object from file", buf);
        if (s->error_code) cos_warn_log("status->error_code: %s", s->error_code);
        if (s->error_msg) cos_warn_log("status->error_msg: %s", s->error_msg);
        if (s->req_id) cos_warn_log("status->req_id: %s", s->req_id);
    }
```

## Bucket 조작
###  Put Bucket
#### 기능 설명
Put Bucket 요청은 지정 계정에서 한 개의 Bucket을 생성할 수 있습니다.
#### 방식 프로토타입
```cpp
cos_status_t *cos_create_bucket(const cos_request_options_t *options,
                                const cos_string_t *bucket,
                                cos_acl_e cos_acl,
                                cos_table_t **resp_headers);
```

#### 매개변수 설명
| 매개변수 이름 | 매개변수 설명 | 유형 |
|---------|---------|---------|
| options | COS 요청 옵션 | Struct |
| bucket | 버킷 이름, 버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다 | String  |
| cos_acl | 사용자가 지정 가능한 권한입니다. <br>유효 값: COS_ACL_PRIVATE(0), COS_ACL_PUBLIC_READ(1), COS_ACL_PUBLIC_READ_WRITE(2). <br>기본값: COS_ACL_PRIVATE(0)| Enum  |
| resp_headers | HTTP 응답 헤더를 반환합니다 | Struct |

#### 반환 결과 설명
| 반환 결과 | 설명 | 유형 |
|---------|---------|---------|
| code | 오류 코드 | Int |        
| error_code | 오류 코드 내용| String |   
| error_msg |오류 코드 설명 | String |   
| req_id | 요청 ID | String |  

#### 예시
```cpp
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_acl_e cos_acl = COS_ACL_PRIVATE;
    cos_string_t bucket;
    cos_table_t *resp_headers = NULL;

    //create memory pool
    cos_pool_create(&p, NULL);

    //init request options
    options = cos_request_options_create(p);
    options->config = cos_config_create(options->pool);
    init_test_config(options->config, is_cname);
    cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
    cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
    cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
    cos_str_set(&options->config->appid, TEST_APPID);
    options->config->is_cname = is_cname;
    options->ctl = cos_http_controller_create(options->pool, 0);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    //create bucket
    s = cos_create_bucket(options, &bucket, cos_acl, &resp_headers);
    if (cos_status_is_ok(s)) {
        printf("create bucket succeeded\n");
    } else {
        printf("create bucket failed\n");
    }

    //destroy memory pool
    cos_pool_destroy(p);
```

###  Delete Bucket
#### 기능 설명
Delete Bucket 요청은 지정 계정에서 버킷을 삭제할 수 있으며, 삭제 전 요청 버킷은 비어 있어야 합니다.

#### 방식 프로토타입
```cpp
cos_status_t *cos_delete_bucket(const cos_request_options_t *options,
                                const cos_string_t *bucket,
                                cos_table_t **resp_headers);
```

#### 매개변수 설명
| 매개변수 이름 | 매개변수 설명 | 유형 |
|---------|---------|---------|
| options | COS 요청 옵션 | Struct |  
| bucket | 버킷 이름, 버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다 | String |  
| resp_headers | HTTP 응답 헤더를 반환합니다 | Struct |

#### 반환 결과 설명
| 반환 결과 | 설명 | 유형 |
|---------|---------|---------|
| code | 오류 코드 | Int |          
| error_code | 오류 코드 내용 | String |   
| error_msg |오류 코드 설명 | String |   
| req_id | 요청 정보 ID | String |

#### 예시
```cpp
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_table_t *resp_headers = NULL;

    //create memory pool
    cos_pool_create(&p, NULL);

    //init request options
    options = cos_request_options_create(p);
    options->config = cos_config_create(options->pool);
    init_test_config(options->config, is_cname);
    cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
    cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
    cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
    cos_str_set(&options->config->appid, TEST_APPID);
    options->config->is_cname = is_cname;
    options->ctl = cos_http_controller_create(options->pool, 0);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    //delete bucket
    s = cos_delete_bucket(options, &bucket, &resp_headers);
    if (cos_status_is_ok(s)) {
        printf("create bucket succeeded\n");
    } else {
        printf("create bucket failed\n");
    }

    //destroy memory pool
    cos_pool_destroy(p);
```

###  Get Bucket
#### 기능 설명
Get Bucket 요청은 List Object 요청과 동일하며, 해당 버킷 아래의 부분 또는 모든 객체를 나열할 수 있습니다. 해당 요청을 시작하려면 읽기 권한이 있어야 합니다.

#### 방식 프로토타입
```cpp
cos_status_t *cos_list_object(const cos_request_options_t *options,
                              const cos_string_t *bucket,
                              cos_list_object_params_t *params,
                              cos_table_t **resp_headers);
```

#### 매개변수 설명
| 매개변수 이름 | 매개변수 설명 | 유형 |
|---------|---------|---------|
| options | COS 요청 옵션 | Struct |  
| bucket | 버킷 이름, 버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다 |String|  
| params | Get Bucket 작업 매개변수. |Struct|  
| encoding_type | 반환값의 인코딩 방식을 규정합니다 |String|  
| prefix |접두사 매칭, 반환되는 파일 접두사 주소 시정에 사용합니다 |String|
| marker | 기본으로 UTF-8 이진 순서로 항목이 나열되며, 모든 나열 항목은 marker에서 시작합니다 |String|  
| delimiter | Get Bucket 작업 매개변수 |String|  
| max_ret | 1회에 최대 반환 항목 수, 기본값 1000 |Struct|  
| truncated | 반환 항목이 잘라내기 여부, 'true' 또는 'false' |Boolean|  
| next_marker | 반환 항목이 잘린 경우, 반환되는 NextMarker는 다음 항목의 시작점입니다 |String|  
| object_list | Get Bucket 작업으로 반환된 객체 리스트 |Struct|  
| key | Get Bucket 작업으로 반환된 객체 이름 |Struct|  
| last_modified | Get Bucket 작업으로 반환된 객체의 마지막 수정 시간 |Struct|  
| etag | Get Bucket 작업으로 반환된 객체의 SHA-1 알고리즘 검증값 |Struct|  
| size | Get Bucket 작업으로 반환된 객체의 크기, 단위는 바이트 |Struct|  
| owner_id | Get Bucket 작업으로 반환된 객체 소유자 UID |Struct|
| storage_class | Get Bucket 작업으로 반환된 객체 스토리지 클래스 |Struct|  
| common_prefix_list | Prefix와 delimiter 사이의 동일한 경로를 같은 종류로 분류하고 Common Prefix라 정의합니다 |Struct|  
| resp_headers | HTTP 응답 헤더를 반환합니다 | Struct |  

#### 반환 결과 설명
| 반환 결과 | 설명 | 유형 |
|---------|---------|---------|
| code | 오류 코드 | Int |          
| error_code | 오류 코드 내용| String |   
| error_msg |오류 코드 설명 | String |   
| req_id | 요청 ID |String|  

#### 예시
```cpp
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_table_t *resp_headers = NULL;

    //create memory pool
    cos_pool_create(&p, NULL);

    //init request options
    options = cos_request_options_create(p);
    options->config = cos_config_create(options->pool);
    init_test_config(options->config, is_cname);
    cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
    cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
    cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
    cos_str_set(&options->config->appid, TEST_APPID);
    options->config->is_cname = is_cname;
    options->ctl = cos_http_controller_create(options->pool, 0);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    //get bucket(list object)
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

    //destroy memory pool
    cos_pool_destroy(p);
```

###  Put Bucket ACL
#### 기능 설명
Put Bucket ACL API는 버킷의 ACL 테이블을 작성하는 데 사용되며, 헤더 "x-cos-acl", "x-cos-grant-read", "x-cos-grant-write", “x-cos-grant-full-control”을 통하여 ACL 정보를 입력할 수 있습니다.

#### 방식 프로토타입
```cpp
cos_status_t *cos_put_bucket_acl(const cos_request_options_t *options,
                                 const cos_string_t *bucket,
                                 cos_acl_e cos_acl,
                                 const cos_string_t *grant_read,
                                 const cos_string_t *grant_write,
                                 const cos_string_t *grant_full_ctrl,
                                 cos_table_t **resp_headers);
```

#### 매개변수 설명
| 매개변수 이름 | 매개변수 설명 | 유형 |
|---------|---------|---------|
| options | COS 요청 옵션 | Struct |  
| bucket | 버킷 이름, 버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다 | String |  
| cos_acl | 사용자가 지정 가능한 권한입니다. <br>유효 값: COS_ACL_PRIVATE(0), COS_ACL_PUBLIC_READ(1), COS_ACL_PUBLIC_READ_WRITE(2). <br>기본값: COS_ACL_PRIVATE(0)|Enum|   
| grant_read | 읽기 권한 부여자 |String|  
| grant_write | 쓰기 권한 부여자|String|  
| grant_full_ctrl | 읽기/쓰기 권한 부여자 |String|  
| resp_headers | HTTP 응답 헤더를 반환합니다 | Struct |

#### 반환 결과 설명
| 반환 결과 | 설명 | 유형 |
|---------|---------|---------|
| code | 오류 코드 | Int |         
| error_code | 오류 코드 내용| String |   
| error_msg |오류 코드 설명 | String |   
| req_id | 요청 정보 ID | String |  

#### 예시
```cpp
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_table_t *resp_headers = NULL;

    //create memory pool
    cos_pool_create(&p, NULL);

    //init request options
    options = cos_request_options_create(p);
    options->config = cos_config_create(options->pool);
    init_test_config(options->config, is_cname);
    cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
    cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
    cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
    cos_str_set(&options->config->appid, TEST_APPID);
    options->config->is_cname = is_cname;
    options->ctl = cos_http_controller_create(options->pool, 0);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    //put bucket acl
    cos_string_t read;
    cos_str_set(&read, "id=\"qcs::cam::uin/12345:uin/12345\", id=\"qcs::cam::uin/45678:uin/45678\"");
    s = cos_put_bucket_acl(options, &bucket, cos_acl, &read, NULL, NULL, &resp_headers);
    if (cos_status_is_ok(s)) {
        printf("put bucket acl succeeded\n");
    } else {
        printf("put bucket acl failed\n");
    }

    //destroy memory pool
    cos_pool_destroy(p);
```

###  Get Bucket ACL
#### 기능 설명
Get Bucket ACL API는 버킷의 ACL, 즉 버킷(Bucket)의 액세스 권한 제어 리스트를 가져오는 데 사용됩니다. 이 API는 버킷의 소유자만 조작 권한이 있습니다.

#### 방식 프로토타입
```cpp
cos_status_t *cos_get_bucket_acl(const cos_request_options_t *options,
                                 const cos_string_t *bucket,
                                 cos_acl_params_t *acl_param,
                                 cos_table_t **resp_headers)
```

#### 매개변수 설명
| 매개변수 이름 | 매개변수 설명 | 유형 |
|---------|---------|---------|
| options | COS 요청 옵션 |Struct|  
| bucket | 버킷 이름, 버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다 |String|  
| acl_param | Get Bucket ACL 작업 매개변수 |Struct|  
| owner_id | Get Bucket ACL 작업으로 반환된 버킷 소유자 ID|String|   
| owner_name | Get Bucket ACL 작업으로 반환된 버킷 소유자 이름 |String|  
| object_list | Get Bucket ACL 작업으로 권한을 부여받은 자 정보 및 권한 정보 |Struct|  
| type | Get Bucket ACL 작업으로 반환된 권한을 부여받은 자 계정 유형 |String|  
| id | Get Bucket ACL 작업으로 반환된 권한을 부여받은 자 계정 ID |String|  
| name | Get Bucket ACL 작업으로 반환된 권한을 부여받은 자의 사용자 이름 |String|  
| permission | Get Bucket ACL 작업으로 반환된 권한을 부여받은 자 권한 정보 | String|  
| resp_headers | HTTP 응답 헤더를 반환합니다 | Struct |  



#### 반환 결과 설명
| 반환 결과 | 설명 | 유형 |
|---------|---------|---------|
| code | 오류 코드 | Int |          
| error_code | 오류 코드 내용| String |   
| error_msg |오류 코드 설명 | String |   
| req_id | 요청 정보 ID | String |   

#### 예시
```cpp
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_table_t *resp_headers = NULL;

    //create memory pool
    cos_pool_create(&p, NULL);

    //init request options
    options = cos_request_options_create(p);
    options->config = cos_config_create(options->pool);
    init_test_config(options->config, is_cname);
    cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
    cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
    cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
    cos_str_set(&options->config->appid, TEST_APPID);
    options->config->is_cname = is_cname;
    options->ctl = cos_http_controller_create(options->pool, 0);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    //get bucket acl
    cos_acl_params_t *acl_params = NULL;
    acl_params = cos_create_acl_params(p);
    s = cos_get_bucket_acl(options, &bucket, acl_params, &resp_headers);
    if (cos_status_is_ok(s)) {
        printf("get bucket acl succeeded\n");
        printf("acl owner id:%s, name:%s\n", acl_params->owner_id.data, acl_params->owner_name.data);
        cos_acl_grantee_content_t *acl_content = NULL;
        cos_list_for_each_entry(cos_acl_grantee_content_t, acl_content, &acl_params->grantee_list, node) {
            printf("acl grantee type:%s, id:%s, name:%s, permission:%s\n", acl_content->type.data, acl_content->id.data, acl_content->name.data, acl_content->permission.data);
        }
    } else {
        printf("get bucket acl failed\n");
    }

    //destroy memory pool
    cos_pool_destroy(p);
```

###  Put Bucket Lifecycle
#### 기능 설명
Put Bucket Lifecycle API는 버킷의 수명 주기 규칙을 작성하는 데 사용됩니다.

#### 방식 프로토타입
```cpp
cos_status_t *cos_put_bucket_lifecycle(const cos_request_options_t *options,
                                       const cos_string_t *bucket,
                                       cos_list_t *lifecycle_rule_list,
                                       cos_table_t **resp_headers);
```

#### 매개변수 설명
| 매개변수 이름 | 매개변수 설명 | 유형 |
|---------|---------|---------|
| options | COS 요청 옵션 |Struct|  
| bucket | 버킷 이름, 버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다 |String|  
| lifecycle_rule_list | Put Bucket Lifecycle 작업 매개변수 |Struct|  
| id | 수명 주기 규칙 ID |String|  
| prefix | 규칙에 맞는 접두사 지정 |String|  
| status | 규칙 활성화 여부 지정, 열거형 값: Enabled, Disabled |String|  
| expire | 규칙 만료 속성 |Struct|  
| days | 며칠 후 삭제 조작 또는 전환 조작을 실시할지 지정. 파트 업로드 시작 후 며칠 내에 업로드를 완료해야 할지 지정 |Int|  
| date | 삭제 조작 또는 전환 조작을 언제 실행할지 지정 |String|  
| transition | 규칙 전환 속성, 객체가 언제 Standard_IA로 전환되는지 지정 |Struct|  
| storage_class | 객체가 전환 저장될 대상 스토리지 클래스 지정, 열거형 값: Standard_IA |String|  
| abort | 멀티파트 업로드 실행 유지 가능한 최장 시간 설정 |Struct|  
| resp_headers | HTTP 응답 헤더를 반환합니다 |Struct|

#### 반환 결과 설명
| 반환 결과 | 설명 | 유형 |
|---------|---------|---------|
| code | 오류 코드 |Int|          
| error_code | 오류 코드 내용 |String|   
| error_msg | 오류 코드 설명 |String|   
| req_id | 요청 정보 ID |String|

#### 예시
```cpp
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_table_t *resp_headers = NULL;

    //create memory pool
    cos_pool_create(&p, NULL);

    //init request options
    options = cos_request_options_create(p);
    options->config = cos_config_create(options->pool);
    init_test_config(options->config, is_cname);
    cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
    cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
    cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
    cos_str_set(&options->config->appid, TEST_APPID);
    options->config->is_cname = is_cname;
    options->ctl = cos_http_controller_create(options->pool, 0);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    //put bucket lifecycle
    cos_list_t rule_list;
    cos_list_init(&rule_list);
    cos_lifecycle_rule_content_t *rule_content = NULL;

    rule_content = cos_create_lifecycle_rule_content(p);
    cos_str_set(&rule_content->id, "testrule1");
    cos_str_set(&rule_content->prefix, "abc/");
    cos_str_set(&rule_content->status, "Enabled");
    rule_content->expire.days = 60;
    cos_list_add_tail(&rule_content->node, &rule_list);

    rule_content = cos_create_lifecycle_rule_content(p);
    cos_str_set(&rule_content->id, "testrule2");
    cos_str_set(&rule_content->prefix, "efg/");
    cos_str_set(&rule_content->status, "Disabled");
    cos_str_set(&rule_content->transition.storage_class, "Standard_IA");
    rule_content->transition.days = 30;
    cos_list_add_tail(&rule_content->node, &rule_list);

    rule_content = cos_create_lifecycle_rule_content(p);
    cos_str_set(&rule_content->id, "testrule3");
    cos_str_set(&rule_content->prefix, "xxx/");
    cos_str_set(&rule_content->status, "Enabled");
    rule_content->abort.days = 1;
    cos_list_add_tail(&rule_content->node, &rule_list);

    s = cos_put_bucket_lifecycle(options, &bucket, &rule_list, &resp_headers);
    if (cos_status_is_ok(s)) {
        printf("put bucket lifecycle succeeded\n");
    } else {
        printf("put bucket lifecycle failed\n");
    }

    //destroy memory pool
    cos_pool_destroy(p);
```

###  Get Bucket Lifecycle
#### 기능 설명
Get Bucket Lifecycle API는 버킷의 수명 주기 규칙을 획득하는 데 사용됩니다.

#### 방식 프로토타입
```cpp
cos_status_t *cos_get_bucket_lifecycle(const cos_request_options_t *options,
                                       const cos_string_t *bucket,
                                       cos_list_t *lifecycle_rule_list,
                                       cos_table_t **resp_headers);
```

#### 매개변수 설명
| 매개변수 이름 | 매개변수 설명 | 유형 |
|---------|---------|---------|
| options | COS 요청 옵션 |Struct|  
| bucket | 버킷 이름, 버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다 |String|  
| lifecycle_rule_list | Get Bucket Lifecycle 작업 매개변수 |Struct|  
| id | 수명 주기 규칙 ID |String|  
| prefix | 규칙에 맞는 접두사 |String|  
| status | 규칙의 활성화 여부 지정, 열거형 값: Enabled, Disabled |String|  
| expire | 규칙 만료 속성 |Struct|  
| days | 며칠 후에 삭제 작업을 실시할지 지정 |Int|  
| date | 삭제 작업을 언제 실행할지 지정 |String|  
| transition | 규칙 전환 속성, 객체가 언제 Standard_IA로 전환되는지 지정 |Struct|  
| days | 며칠 후에 전환 작업을 실시할지 지정 |Int|  
| date | 전환 작업을 언제 실행할지 지정 |String|  
| storage_class | 객체가 전환 저장될 대상 스토리지 클래스 지정, 열거형 값: Standard_IA |String|  
| abort | 멀티파트 업로드 실행 유지 가능한 최장 시간 설정 |Struct|  
| days | 멀티파트 업로드 시작 후 며칠 내에 업로드를 완료할지 지정 |Int|  
| resp_headers | HTTP 응답 헤더를 반환합니다 |Struct|

#### 반환 결과 설명
| 반환 결과 | 설명 | 유형 |
|---------|---------|---------|
| code | 오류 코드 |Int|         
| error_code | 오류 코드 내용 |String|   
| error_msg |오류 코드 설명 | String |   
| req_id | 요청 정보 ID | String |   

#### 예시
```cpp
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_table_t *resp_headers = NULL;

    //create memory pool
    cos_pool_create(&p, NULL);

    //init request options
    options = cos_request_options_create(p);
    options->config = cos_config_create(options->pool);
    init_test_config(options->config, is_cname);
    cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
    cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
    cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
    cos_str_set(&options->config->appid, TEST_APPID);
    options->config->is_cname = is_cname;
    options->ctl = cos_http_controller_create(options->pool, 0);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    //get bucket lifecycle
    cos_list_t rule_list_ret;
    cos_list_init(&rule_list_ret);
    s = cos_get_bucket_lifecycle(options, &bucket, &rule_list_ret, &resp_headers);
    if (cos_status_is_ok(s)) {
        printf("get bucket lifecycle succeeded\n");
    } else {
        printf("get bucket lifecycle failed\n");
    }

    //destroy memory pool
    cos_pool_destroy(p);
```

###  Delete Bucket Lifecycle
#### 기능 설명
Delete Bucket Lifecycle API는 버킷의 수명 주기 규칙을 삭제하는 데 사용됩니다.

#### 방식 프로토타입
```cpp
cos_status_t *cos_delete_bucket_lifecycle(const cos_request_options_t *options,
                                          const cos_string_t *bucket,
                                          cos_table_t **resp_headers);
```

#### 매개변수 설명
| 매개변수 이름 | 매개변수 설명 | 유형 |
|---------|---------|---------|
| options | COS 요청 옵션 | Struct |  
| bucket | 버킷 이름, 버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다 |String|  
| resp_headers | HTTP 응답 헤더를 반환합니다 |Struct|

#### 반환 결과 설명
| 반환 결과 | 설명 | 유형 |
|---------|---------|---------|
| code | 오류 코드 | Int |        
| error_code | 오류 코드 내용 |String|   
| error_msg |오류 코드 설명 | String |   
| req_id | 요청 정보 ID |String|

#### 예시
```cpp
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_table_t *resp_headers = NULL;

    //create memory pool
    cos_pool_create(&p, NULL);

    //init request options
    options = cos_request_options_create(p);
    options->config = cos_config_create(options->pool);
    init_test_config(options->config, is_cname);
    cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
    cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
    cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
    cos_str_set(&options->config->appid, TEST_APPID);
    options->config->is_cname = is_cname;
    options->ctl = cos_http_controller_create(options->pool, 0);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    //delete bucket lifecycle
    s = cos_delete_bucket_lifecycle(options, &bucket, &resp_headers);
    if (cos_status_is_ok(s)) {
        printf("delete bucket lifecycle succeeded\n");
    } else {
        printf("delete bucket lifecycle failed\n");
    }

    //destroy memory pool
    cos_pool_destroy(p);
```

### Put Bucket CORS
#### 기능 설명
Put Bucket CORS API는 버킷의 CORS 권한 설정을 요청하는 데 사용됩니다.

#### 방식 프로토타입
```cpp
cos_status_t *cos_put_bucket_cors(const cos_request_options_t *options,
                                  const cos_string_t *bucket,
                                  cos_list_t *cors_rule_list,
                                  cos_table_t **resp_headers);
```

#### 매개변수 설명
| 매개변수 이름 | 매개변수 설명 | 유형 |
|---------|---------|---------|
| options | COS 요청 옵션 |Struct|  
| bucket | 버킷 이름, 버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다 |String|  
| cors_rule_list | Put Bucket CORS 작업 매개변수 |Struct|  
| id | 구성 규칙 ID |String|  
| allowed_origin | 허용된 액세스 소스, 와일드카드 `*` 지원 |String|  
| allowed_method | 허용된 HTTP 작업, 열거형 값: GET, PUT, HEAD, POST, DELETE |String|  
| allowed_header | OPTIONS 요청 발송 시 서버에 다음 요청은 어떠한 사용자 지정 HTTP 요청 헤더를 사용할 수 있는지를 알려줍니다. 와일드 카드`*` 지원 |String|  
| expose_header | 브라우저가 수신할 수 있는 서버의 사용자 지정 헤더 |String|  
| max_age_seconds | OPTIONS 요청이 얻은 결과의 유효기간 설정 |Int|  
| resp_headers | HTTP 응답 헤더를 반환합니다 |Struct|  


#### 반환 결과 설명
| 반환 결과 | 설명 | 유형 |
|---------|---------|---------|
| code | 오류 코드 | Int |        
| error_code | 오류 코드 내용 |String|   
| error_msg |오류 코드 설명 | String |   
| req_id | 요청 정보 ID |String|

#### 예시
```cpp
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_table_t *resp_headers = NULL;

    //create memory pool
    cos_pool_create(&p, NULL);

    //init request options
    options = cos_request_options_create(p);
    options->config = cos_config_create(options->pool);
    init_test_config(options->config, is_cname);
    cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
    cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
    cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
    cos_str_set(&options->config->appid, TEST_APPID);
    options->config->is_cname = is_cname;
    options->ctl = cos_http_controller_create(options->pool, 0);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    //put bucket cors
    cos_list_t rule_list;
    cos_list_init(&rule_list);
    cos_cors_rule_content_t *rule_content = NULL;

    rule_content = cos_create_cors_rule_content(p);
    cos_str_set(&rule_content->id, "testrule1");
    cos_str_set(&rule_content->allowed_origin, "http://www.qq1.com");
    cos_str_set(&rule_content->allowed_method, "GET");
    cos_str_set(&rule_content->allowed_header, "*");
    cos_str_set(&rule_content->expose_header, "xxx");
    rule_content->max_age_seconds = 3600;
    cos_list_add_tail(&rule_content->node, &rule_list);

    rule_content = cos_create_cors_rule_content(p);
    cos_str_set(&rule_content->id, "testrule2");
    cos_str_set(&rule_content->allowed_origin, "http://www.qq2.com");
    cos_str_set(&rule_content->allowed_method, "GET");
    cos_str_set(&rule_content->allowed_header, "*");
    cos_str_set(&rule_content->expose_header, "yyy");
    rule_content->max_age_seconds = 7200;
    cos_list_add_tail(&rule_content->node, &rule_list);

    rule_content = cos_create_cors_rule_content(p);
    cos_str_set(&rule_content->id, "testrule3");
    cos_str_set(&rule_content->allowed_origin, "http://www.qq3.com");
    cos_str_set(&rule_content->allowed_method, "GET");
    cos_str_set(&rule_content->allowed_header, "*");
    cos_str_set(&rule_content->expose_header, "zzz");
    rule_content->max_age_seconds = 60;
    cos_list_add_tail(&rule_content->node, &rule_list);

    //put cors
    s = cos_put_bucket_cors(options, &bucket, &rule_list, &resp_headers);
    if (cos_status_is_ok(s)) {
        printf("put bucket cors succeeded\n");
    } else {
        printf("put bucket cors failed\n");
    }

    //destroy memory pool
    cos_pool_destroy(p);
```

### Get Bucket CORS
#### 기능 설명
Get Bucket CORS API는 버킷의 CORS 권한 구성 획득을 요청하는 데 사용됩니다.
#### 방식 프로토타입
```cpp
cos_status_t *cos_get_bucket_cors(const cos_request_options_t *options,
                                  const cos_string_t *bucket,
                                  cos_list_t *cors_rule_list,
                                  cos_table_t **resp_headers);
```

#### 매개변수 설명
| 매개변수 이름 | 매개변수 설명 | 유형 |
|---------|---------|---------|
| options | COS 요청 옵션 | Struct |  
| bucket | 버킷 이름, 버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다 |String|  
| cors_rule_list | Get Bucket CORS 작업 매개변수 |Struct|
| id | 구성 규칙 ID |String|  
| allowed_origin | 허용된 액세스 소스, 와일드카드 `*` 지원 |String|
| allowed_method | 허용된 HTTP 작업, 열거형 값: GET, PUT, HEAD, POST, DELETE |String|  
| allowed_header | OPTIONS 요청 발송 시 서버에 다음 요청은 어떠한 사용자 지정 HTTP 요청 헤더를 사용할 수 있는지를 알려줍니다. 와일드 카드`*` 지원 |String|  
| expose_header | 브라우저가 수신할 수 있는 서버의 사용자 지정 헤더 |String|  
| max_age_seconds | OPTIONS 요청이 얻은 결과의 유효기간 설정 |Int|  
| resp_headers | HTTP 응답 헤더를 반환합니다 |Struct|

#### 반환 결과 설명
| 반환 결과 | 설명 | 유형 |
|---------|---------|---------|
| code | 오류 코드 | Int |        
| error_code | 오류 코드 내용 |String|   
| error_msg |오류 코드 설명 | String |   
| req_id | 요청 정보 ID |String|

#### 예시
```cpp
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_table_t *resp_headers = NULL;

    //create memory pool
    cos_pool_create(&p, NULL);

    //init request options
    options = cos_request_options_create(p);
    options->config = cos_config_create(options->pool);
    init_test_config(options->config, is_cname);
    cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
    cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
    cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
    cos_str_set(&options->config->appid, TEST_APPID);
    options->config->is_cname = is_cname;
    options->ctl = cos_http_controller_create(options->pool, 0);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    //get bucket cors
    cos_list_t rule_list_ret;
    cos_list_init(&rule_list_ret);
    s = cos_get_bucket_cors(options, &bucket, &rule_list_ret, &resp_headers);
    if (cos_status_is_ok(s)) {
        printf("get bucket cors succeeded\n");
        cos_cors_rule_content_t *content = NULL;
        cos_list_for_each_entry(cos_cors_rule_content_t, content, &rule_list_ret, node) {
            printf("cors id:%s, allowed_origin:%s, allowed_method:%s, allowed_header:%s, expose_header:%s, max_age_seconds:%d\n",
                content->id.data, content->allowed_origin.data, content->allowed_method.data, content->allowed_header.data, content->expose_header.data, content->max_age_seconds);
        }
    } else {
        printf("get bucket cors failed\n");
    }

    //destroy memory pool
    cos_pool_destroy(p);
```

###  Delete Bucket CORS
#### 기능 설명
Delete Bucket CORS API는 버킷의 권한 구성을 삭제하는 데 사용됩니다.

#### 방식 프로토타입
```cpp
cos_status_t *cos_delete_bucket_cors(const cos_request_options_t *options,
                                     const cos_string_t *bucket,
                                     cos_table_t **resp_headers);
```

#### 매개변수 설명
| 매개변수 이름 | 매개변수 설명 | 유형 |
|---------|---------|---------|
| options | COS 요청 옵션 |Struct|  
| bucket | 버킷 이름, 버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다 |String|  
| resp_headers | HTTP 응답 헤더를 반환합니다 |Struct|

#### 반환 결과 설명
| 반환 결과 | 설명 | 유형 |
|---------|---------|---------|
| code | 오류 코드 | Int |        
| error_code | 오류 코드 내용 |String|   
| error_msg |오류 코드 설명 | String |   
| req_id | 요청 정보 ID |String|

#### 예시
```cpp
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_table_t *resp_headers = NULL;

    //create memory pool
    cos_pool_create(&p, NULL);

    //init request options
    options = cos_request_options_create(p);
    options->config = cos_config_create(options->pool);
    init_test_config(options->config, is_cname);
    cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
    cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
    cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
    cos_str_set(&options->config->appid, TEST_APPID);
    options->config->is_cname = is_cname;
    options->ctl = cos_http_controller_create(options->pool, 0);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    //delete bucket cors
    s = cos_delete_bucket_cors(options, &bucket, &resp_headers);
    if (cos_status_is_ok(s)) {
        printf("delete bucket cors succeeded\n");
    } else {
        printf("delete bucket cors failed\n");
    }

    //destroy memory pool
    cos_pool_destroy(p);
```

###  Put Bucket Versioning
#### 기능 설명
Put Bucket Versioning API는 버킷의 버전 제어 기능을 활성화 또는 일시 중지할 수 있게 합니다.

#### 방식 프로토타입
```cpp
cos_status_t *cos_put_bucket_versioning(const cos_request_options_t *options,
                                        const cos_string_t *bucket,
                                        cos_versioning_content_t *versioning,
                                        cos_table_t **resp_headers);
```

#### 매개변수 설명
| 매개변수 이름 | 매개변수 설명 | 유형 |
|---------|---------|---------|
| options | COS 요청 옵션 | Struct |  
| bucket | 버킷 이름, 버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다 |String|  
| versioning | Put Bucket Versioning 작업 매개변수 |Struct|  
| status | 버전 사용 여부, 열거 값: Suspended, Enabled |String|  
| resp_headers | HTTP 응답 헤더를 반환합니다 |Struct|  

#### 반환 결과 설명
| 반환 결과 | 설명 | 유형 |
|---------|---------|---------|
| code | 오류 코드 | Int |        
| error_code | 오류 코드 내용| String |   
| error_msg |오류 코드 설명 | String |   
| req_id | 요청 정보 ID |String|

#### 예시
```cpp
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_table_t *resp_headers = NULL;

    //create memory pool
    cos_pool_create(&p, NULL);

    //init request options
    options = cos_request_options_create(p);
    options->config = cos_config_create(options->pool);
    init_test_config(options->config, is_cname);
    cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
    cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
    cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
    cos_str_set(&options->config->appid, TEST_APPID);
    options->config->is_cname = is_cname;
    options->ctl = cos_http_controller_create(options->pool, 0);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    //put bucket versioning
    cos_versioning_content_t *versioning = NULL;
    versioning = cos_create_versioning_content(p);
    cos_str_set(&versioning->status, "Enabled");
    s = cos_put_bucket_versioning(options, &bucket, versioning, &resp_headers);
    if (cos_status_is_ok(s)) {
        printf("put bucket versioning succeeded\n");
    } else {
        printf("put bucket versioning failed\n");
    }

    //destroy memory pool
    cos_pool_destroy(p);
```

###  Get Bucket Versioning
#### 기능 설명
Put Bucket Versioning API는 버킷의 버전 제어 정보를 획득합니다.

#### 방식 프로토타입
```cpp
cos_status_t *cos_get_bucket_versioning(const cos_request_options_t *options,
                                        const cos_string_t *bucket,
                                        cos_versioning_content_t *versioning,
                                        cos_table_t **resp_headers);
```

#### 매개변수 설명
| 매개변수 이름 | 매개변수 설명 | 유형 |
|---------|---------|---------|
| options | COS 요청 옵션 | Struct |  
| bucket | 버킷 이름, 버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다 |String|  
| versioning | Get Bucket Versioning 작업 매개변수 |Struct|  
| status | 버전 사용 여부, 열거 값: Suspended, Enabled |String|  
| resp_headers | HTTP 응답 헤더를 반환합니다 |Struct|  

#### 반환 결과 설명
| 반환 결과 | 설명 | 유형 |
|---------|---------|---------|
| code | 오류 코드 | Int |        
| error_code | 오류 코드 내용 |String|   
| error_msg |오류 코드 설명 | String |   
| req_id | 요청 정보 ID |String|

#### 예시
```cpp
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_table_t *resp_headers = NULL;

    //create memory pool
    cos_pool_create(&p, NULL);

    //init request options
    options = cos_request_options_create(p);
    options->config = cos_config_create(options->pool);
    init_test_config(options->config, is_cname);
    cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
    cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
    cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
    cos_str_set(&options->config->appid, TEST_APPID);
    options->config->is_cname = is_cname;
    options->ctl = cos_http_controller_create(options->pool, 0);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    //get bucket versioning
    cos_versioning_content_t *versioning = NULL;
    versioning = cos_create_versioning_content(p);
    s = cos_get_bucket_versioning(options, &bucket, versioning, &resp_headers);
    if (cos_status_is_ok(s)) {
        printf("put bucket versioning succeeded\n");
        printf("bucket versioning status: %s\n", versioning->status.data);
    } else {
        printf("put bucket versioning failed\n");
    }

    //destroy memory pool
    cos_pool_destroy(p);
```

###  Put Bucket Replication
#### 기능 설명
Put Bucket Replication 요청은 버전 관리가 활성화된 버킷에 replication 구성을 추가하는 데 사용됩니다. 만일 버킷에 이미 복제 구성이 있는 경우, 해당 요청은 기존의 구성을 대체합니다.

#### 방식 프로토타입
```cpp
cos_status_t *cos_put_bucket_replication(const cos_request_options_t *options,
                                         const cos_string_t *bucket,
                                         cos_replication_params_t *replication_param,
                                         cos_table_t **resp_headers);
```

#### 매개변수 설명
| 매개변수 이름 | 매개변수 설명 | 유형 |
|---------|---------|---------|
| options | COS 요청 옵션. |Struct|  
| bucket | 버킷 이름, 버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다 |String|  
| replication_param | Put Bucket Replication 작업 매개변수 |Struct|  
| role | 조작자 계정 정보 |String|  
| rule_list | 복제 구성 정보|Struct|  
| id | 구체적인 규칙 이름 표시 |String|  
| status | 규칙 유효 여부 표시, 열거형 값: Enabled, Disabled |String|  
| prefix | 접두사 매칭. 중첩이 불가하며, 중첩 시 오류가 반환됩니다 |String|  
| dst_bucket | 대상 버킷 표시, 형식은 리소스 식별자 qcs:id/0:cos:[Region]:appid/[APPID]:[Bucketname]|String|  
| storage_class | 스토리지 클래스, 열거형 값: Standard, Standard_IA.<br>기본 값은 원본 버킷 클래스|String|  
| resp_headers | HTTP 응답 헤더를 반환합니다. | Struct |  

#### 반환 결과 설명
| 반환 결과 | 설명 | 유형 |
|---------|---------|---------|
| code | 오류 코드 | Int |        
| error_code | 오류 코드 내용| String |   
| error_msg |오류 코드 설명 | String |   
| req_id | 요청 정보 ID |String|

#### 예시
```cpp
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_table_t *resp_headers = NULL;

    //create memory pool
    cos_pool_create(&p, NULL);

    //init request options
    options = cos_request_options_create(p);
    options->config = cos_config_create(options->pool);
    init_test_config(options->config, is_cname);
    cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
    cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
    cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
    cos_str_set(&options->config->appid, TEST_APPID);
    options->config->is_cname = is_cname;
    options->ctl = cos_http_controller_create(options->pool, 0);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    //put bucket replication
    cos_replication_params_t *replication_param = NULL;
    replication_param = cos_create_replication_params(p);
    cos_str_set(&replication_param->role, "qcs::cam::uin/100000616666:uin/100000616666");

    cos_replication_rule_content_t *rule = NULL;
    rule = cos_create_replication_rule_content(p);
    cos_str_set(&rule->id, "Rule_01");
    cos_str_set(&rule->status, "Enabled");
    cos_str_set(&rule->prefix, "test1");
    cos_str_set(&rule->dst_bucket, "qcs:id/0:cos:cn-east:appid/1253686666:replicationtest");
    cos_list_add_tail(&rule->node, &replication_param->rule_list);

    rule = cos_create_replication_rule_content(p);
    cos_str_set(&rule->id, "Rule_02");
    cos_str_set(&rule->status, "Disabled");
    cos_str_set(&rule->prefix, "test2");
    cos_str_set(&rule->storage_class, "Standard_IA");
    cos_str_set(&rule->dst_bucket, "qcs:id/0:cos:cn-east:appid/1253686666:replicationtest");
    cos_list_add_tail(&rule->node, &replication_param->rule_list);

    rule = cos_create_replication_rule_content(p);
    cos_str_set(&rule->id, "Rule_03");
    cos_str_set(&rule->status, "Enabled");
    cos_str_set(&rule->prefix, "test3");
    cos_str_set(&rule->storage_class, "Standard_IA");
    cos_str_set(&rule->dst_bucket, "qcs:id/0:cos:cn-east:appid/1253686666:replicationtest");
    cos_list_add_tail(&rule->node, &replication_param->rule_list);

    s = cos_put_bucket_replication(options, &bucket, replication_param, &resp_headers);
    if (cos_status_is_ok(s)) {
        printf("put bucket replication succeeded\n");
    } else {
        printf("put bucket replication failed\n");
    }

    //destroy memory pool
    cos_pool_destroy(p);
```

###  Get Bucket Replication

#### 기능 설명
Get Bucket Replication API 요청은 읽기 버킷에서 사용자의 도메인 간 구성 정보 복제를 구현합니다.

#### 방식 프로토타입
```cpp
cos_status_t *cos_get_bucket_replication(const cos_request_options_t *options,
                                         const cos_string_t *bucket,
                                         cos_replication_params_t *replication_param,
                                         cos_table_t **resp_headers);
```

#### 매개변수 설명
| 매개변수 이름 | 매개변수 설명 | 유형 |
|---------|---------|---------|
| options | COS 요청 옵션 | Struct |  
| bucket | 버킷 이름, 버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다 | String |  
| replication_param | Get Bucket Replication 작업 매개변수 |Struct|  
| role | 조작자 계정 정보 |String|  
| rule_list | 복제 구성 정보|Struct|  
| id | 구체적인 규칙 이름 표시 |String|  
| status | 규칙 유효 여부 표시, 열거형 값: Enabled, Disabled |String|  
| prefix | 접두사 매칭. 중첩이 불가하며, 중첩 시 오류가 반환됩니다 |String|  
| dst_bucket | 대상 버킷 표시, 형식은 리소스 식별자 qcs:id/0:cos:[Region]:appid/[APPID]:[Bucketname]|String|  
| storage_class | 스토리지 클래스, 열거형 값: Standard, Standard_IA.<br>기본 값은 원본 버킷 클래스|String|  
| resp_headers | HTTP 응답 헤더를 반환합니다 | Struct |  

#### 반환 결과 설명
| 반환 결과 | 설명 | 유형 |
|---------|---------|---------|
| code | 오류 코드 | Int |        
| error_code | 오류 코드 내용| String |   
| error_msg |오류 코드 설명 | String |   
| req_id | 요청 정보 ID |String|

#### 예시
```cpp
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_table_t *resp_headers = NULL;

    //create memory pool
    cos_pool_create(&p, NULL);

    //init request options
    options = cos_request_options_create(p);
    options->config = cos_config_create(options->pool);
    init_test_config(options->config, is_cname);
    cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
    cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
    cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
    cos_str_set(&options->config->appid, TEST_APPID);
    options->config->is_cname = is_cname;
    options->ctl = cos_http_controller_create(options->pool, 0);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    //get bucket replication
    cos_replication_params_t *replication_param2 = NULL;
    replication_param2 = cos_create_replication_params(p);
    s = cos_get_bucket_replication(options, &bucket, replication_param2, &resp_headers);

    if (cos_status_is_ok(s)) {
        printf("get bucket replication succeeded\n");
        printf("ReplicationConfiguration role: %s\n", replication_param2->role.data);
    cos_replication_rule_content_t *content = NULL;
        cos_list_for_each_entry(cos_replication_rule_content_t, content, &replication_param2->rule_list, node) {
        printf("ReplicationConfiguration rule, id:%s, status:%s, prefix:%s, dst_bucket:%s, storage_class:%s\n",
                content->id.data, content->status.data, content->prefix.data, content->dst_bucket.data, content->storage_class.data);
        }
    } else {
        printf("get bucket replication failed\n");
    }

    //destroy memory pool
    cos_pool_destroy(p);
```

###  Delete Bucket Replication
#### 기능 설명
Delete Bucket Replication API는 버킷의 크로스 도메인 복제 구성을 삭제하는 데 사용됩니다.

#### 방식 프로토타입
```cpp
cos_status_t *cos_delete_bucket_replication(const cos_request_options_t *options,
                                            const cos_string_t *bucket,
                                            cos_table_t **resp_headers);
```

#### 매개변수 설명
| 매개변수 이름 | 매개변수 설명 | 유형 |
|---------|---------|---------|
| options | COS 요청 옵션 | Struct |  
| bucket | 버킷 이름, 버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다 |String|  
| resp_headers | HTTP 응답 헤더를 반환합니다 |Struct|  

#### 반환 결과 설명
| 반환 결과 | 설명 | 유형 |
|---------|---------|---------|
| code | 오류 코드 | Int |        
| error_code | 오류 코드 내용 |String|   
| error_msg |오류 코드 설명 | String |   
| req_id | 요청 정보 ID |String|

#### 예시
```cpp
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_table_t *resp_headers = NULL;

    //create memory pool
    cos_pool_create(&p, NULL);

    //init request options
    options = cos_request_options_create(p);
    options->config = cos_config_create(options->pool);
    init_test_config(options->config, is_cname);
    cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
    cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
    cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
    cos_str_set(&options->config->appid, TEST_APPID);
    options->config->is_cname = is_cname;
    options->ctl = cos_http_controller_create(options->pool, 0);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    //delete bucket cors
    s = cos_delete_bucket_replication(options, &bucket, &resp_headers);
    if (cos_status_is_ok(s)) {
        printf("delete bucket replication succeeded\n");
    } else {
        printf("delete bucket replication failed\n");
    }

    //destroy memory pool
    cos_pool_destroy(p);
```

## Object 조작
###  Get Object
#### 기능 설명
Get Object 요청은 파일(Object)을 로컬로 다운로드 할 수 있습니다. 해당 조작은 대상 Object에 대한 읽기 권한이 있거나 또는 대상 Object가 모든 사람에게 읽기 권한을 개방해야 합니다(공개 읽기).

#### 방식 프로토타입
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
| 매개변수 이름 | 매개변수 설명 | 유형 |
|---------|---------|---------|
| options | COS 요청 옵션 |Struct|  
| bucket | 버킷 이름, 버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다 |String|  
| object | 객체 이름 |String|  
| headers | 첨부된 COS 요청 헤더 |Struct|  
| params | COS 요청 작업 매개변수 |Struct|  
| filename | 객체 로컬 저장 파일 이름 |String|  
| resp_headers | HTTP 응답 헤더를 반환합니다 | Struct |  

#### 반환 결과 설명
| 반환 결과 | 설명 | 유형 |
|---------|---------|---------|
| code | 오류 코드 | Int |        
| error_code | 오류 코드 내용| String |   
| error_msg |오류 코드 설명 | String |   
| req_id | 요청 정보 ID |String|

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

    //create memory pool
    cos_pool_create(&p, NULL);

    //init request options
    options = cos_request_options_create(p);
    options->config = cos_config_create(options->pool);
    init_test_config(options->config, is_cname);
    cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
    cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
    cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
    cos_str_set(&options->config->appid, TEST_APPID);
    options->config->is_cname = is_cname;
    options->ctl = cos_http_controller_create(options->pool, 0);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    //get object
    cos_str_set(&file, TEST_DOWNLOAD_NAME);
    cos_str_set(&object, TEST_OBJECT_NAME);
    s = cos_get_object_to_file(options, &bucket, &object, NULL, NULL, &file, &resp_headers);
    if (cos_status_is_ok(s)) {
        printf("get object succeeded\n");
    } else {
        printf("get object failed\n");
    }

    //destroy memory pool
    cos_pool_destroy(p);
```

###  Head Object
#### 기능 설명
Head Object 요청은 해당하는 객체의 메타데이터를 검색할 수 있으며 Head의 권한은 Get의 권한과 일치합니다.

#### 방식 프로토타입
```cpp
cos_status_t *cos_head_object(const cos_request_options_t *options,
                              const cos_string_t *bucket,
                              const cos_string_t *object,
                              cos_table_t *headers,
                              cos_table_t **resp_headers);
```

#### 매개변수 설명
| 매개변수 이름 | 매개변수 설명 | 유형 |
|---------|---------|---------|
| options | COS 요청 옵션 | Struct |  
| bucket | 버킷 이름, 버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다 | String |  
| object | 객체 이름 |String|  
| headers | 첨부된 COS 요청 헤더 |Struct|  
| resp_headers | HTTP 응답 헤더를 반환합니다 | Struct |  

#### 반환 결과 설명
| 반환 결과 | 설명 | 유형 |
|---------|---------|---------|
| code | 오류 코드 | Int |        
| error_code | 오류 코드 내용| String |   
| error_msg |오류 코드 설명 | String |   
| req_id | 요청 정보 ID |String|

#### 예시
```cpp
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_string_t object;
    cos_table_t *resp_headers = NULL;

    //create memory pool
    cos_pool_create(&p, NULL);

    //init request options
    options = cos_request_options_create(p);
    options->config = cos_config_create(options->pool);
    init_test_config(options->config, is_cname);
    cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
    cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
    cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
    cos_str_set(&options->config->appid, TEST_APPID);
    options->config->is_cname = is_cname;
    options->ctl = cos_http_controller_create(options->pool, 0);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    //head object
    cos_str_set(&object, TEST_OBJECT_NAME);
    s = cos_head_object(options, &bucket, &object, NULL, &resp_headers);
    if (cos_status_is_ok(s)) {
        printf("head object succeeded\n");
    } else {
        printf("head object failed\n");
    }

    //destroy memory pool
    cos_pool_destroy(p);
```

###  Put Object
#### 기능 설명
Put Object 요청은 한 개의 파일(Object)을 지정 버킷으로 업로드할 수 있습니다.
> 주의:
> 현재 액세스 정책 항목은 1000으로 제한되어 있습니다. 객체에 대해 ACL 제어가 필요하지 않은 경우 업로드 시 설정하지 마십시오. 기본으로 버킷 권한은 계승됩니다.

#### 방식 프로토타입
```cpp
cos_status_t *cos_put_object_from_file(const cos_request_options_t *options,
                                       const cos_string_t *bucket,
                                       const cos_string_t *object,
                                       const cos_string_t *filename,
                                       cos_table_t *headers,
                                       cos_table_t **resp_headers);
```

#### 매개변수 설명
| 매개변수 이름 | 매개변수 설명 | 유형 |
|---------|---------|---------|
| options | COS 요청 옵션 |Struct|  
| bucket | 버킷 이름, 버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다 |String|  
| object | 객체 이름 |String|  
| filename | 객체 로컬 저장 파일 이름 |String|  
| headers | 첨부된 COS 요청 헤더 |Struct|  
| resp_headers | HTTP 응답 헤더를 반환합니다 | Struct |

#### 반환 결과 설명
| 반환 결과 | 설명 | 유형 |
|---------|---------|---------|
| code | 오류 코드 | Int |        
| error_code | 오류 코드 내용| String |   
| error_msg |오류 코드 설명 | String |   
| req_id | 요청 정보 ID |String|

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

    //create memory pool
    cos_pool_create(&p, NULL);

    //init request options
    options = cos_request_options_create(p);
    options->config = cos_config_create(options->pool);
    init_test_config(options->config, is_cname);
    cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
    cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
    cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
    cos_str_set(&options->config->appid, TEST_APPID);
    options->config->is_cname = is_cname;
    options->ctl = cos_http_controller_create(options->pool, 0);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    //put object
    cos_str_set(&file, TEST_DOWNLOAD_NAME);
    cos_str_set(&object, TEST_OBJECT_NAME);
    s = cos_put_object_from_file(options, &bucket, &object, &file, NULL, &resp_headers);
    if (cos_status_is_ok(s)) {
        printf("put object succeeded\n");
    } else {
        printf("put object failed\n");
    }

    //destroy memory pool
    cos_pool_destroy(p);
```

###  Delete Object
#### 기능 설명
Delete Object 요청은 한 개의 파일(Object)을 삭제할 수 있습니다.

#### 방식 프로토타입
```cpp
cos_status_t *cos_delete_object(const cos_request_options_t *options,
                                const cos_string_t *bucket,
                                const cos_string_t *object,
                                cos_table_t **resp_headers);
```

#### 매개변수 설명
| 매개변수 이름 | 매개변수 설명 | 유형 |
|---------|---------|---------|
| options | COS 요청 옵션 |Struct|  
| bucket | 버킷 이름, 버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다 |String|  
| object | 객체 이름 |String|  
| resp_headers | HTTP 응답 헤더를 반환합니다 | Struct |

#### 반환 결과 설명
| 반환 결과 | 설명 | 유형 |
|---------|---------|---------|
| code | 오류 코드 | Int |        
| error_code | 오류 코드 내용| String |   
| error_msg |오류 코드 설명 | String |   
| req_id | 요청 정보 ID |String|

#### 예시
```cpp
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_string_t object;
    cos_table_t *resp_headers = NULL;

    //create memory pool
    cos_pool_create(&p, NULL);

    //init request options
    options = cos_request_options_create(p);
    options->config = cos_config_create(options->pool);
    init_test_config(options->config, is_cname);
    cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
    cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
    cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
    cos_str_set(&options->config->appid, TEST_APPID);
    options->config->is_cname = is_cname;
    options->ctl = cos_http_controller_create(options->pool, 0);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    //delete object
    cos_str_set(&object, TEST_OBJECT_NAME);
    s = cos_delete_object(options, &bucket, &object, &resp_headers);
    if (cos_status_is_ok(s)) {
        printf("delete object succeeded\n");
    } else {
        printf("delete object failed\n");
    }

    //destroy memory pool
    cos_pool_destroy(p);
```

###  Delete Multiple Object
#### 기능 설명
Delete Multiple Object 요청은 파일 배치 삭제를 할 수 있습니다. 최대 1회 1000개 파일 삭제를 지원합니다. 반환 결과에 대해 COS는 Verbose 및 Quiet의 두 가지 모드를 제공합니다. Verbose 모드는 각 객체의 삭제 결과를 반환하며, Quiet 모드는 오류가 발생한 객체 정보만 반환합니다.

#### 방식 프로토타입
```cpp
cos_status_t *cos_delete_objects(const cos_request_options_t *options,
                                 const cos_string_t *bucket,
                                 cos_list_t *object_list,
                                 int is_quiet,
                                 cos_table_t **resp_headers,
                                 cos_list_t *deleted_object_list);
```

#### 매개변수 설명
| 매개변수 이름 | 매개변수 설명 | 유형 |
|---------|---------|---------|
| options | COS 요청 옵션 |Struct|  
| bucket | 버킷 이름, 버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다 | String |
| object_list | 객체 삭제 대기 리스트|Struct|
  | key | 삭제 대기 중인 객체 이름 |String|  
| is_quiet | Quiet 모드 사용 여부를 결정합니다. <br>True(1): Quiet 모드 사용, False(0): Verbose 모드 사용, 기본값은 False(0)입니다|Boolean|  
| resp_headers | HTTP 응답 헤더를 반환합니다 | Struct |  
| deleted_object_list | 객체 삭제 정보 리스트 |Struct|  

#### 반환 결과 설명
| 반환 결과 | 설명 | 유형 |
|---------|---------|---------|
| code | 오류 코드 | Int |        
| error_code | 오류 코드 내용| String |   
| error_msg |오류 코드 설명 | String |   
| req_id | 요청 정보 ID |String|

#### 예시
```cpp
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_string_t object;
    cos_table_t *resp_headers = NULL;

    //create memory pool
    cos_pool_create(&p, NULL);

    //init request options
    options = cos_request_options_create(p);
    options->config = cos_config_create(options->pool);
    init_test_config(options->config, is_cname);
    cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
    cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
    cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
    cos_str_set(&options->config->appid, TEST_APPID);
    options->config->is_cname = is_cname;
    options->ctl = cos_http_controller_create(options->pool, 0);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    //init delete object list
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

    //delete objects
    int is_quiet = COS_TRUE;
    cos_str_set(&object, TEST_OBJECT_NAME);
    s = cos_delete_objects(options, &bucket, &object_list, is_quiet, &resp_headers, &deleted_object_list);
    if (cos_status_is_ok(s)) {
        printf("delete objects succeeded\n");
    } else {
        printf("delete objects failed\n");
    }

    //destroy memory pool
    cos_pool_destroy(p);
```

###  Put Object ACL
#### 기능 설명
Put Object ACL API는 버킷 중 임의의 ACL 구성을 작성하는 데 사용되며, 헤더 "x-cos-acl"\, “x-cos-grant-read", "x-cos-grant-write", "x-cos-grant-full-control”을 통하여 ACL 정보를 입력할 수 있습니다.

현재 액세스 정책 항목은 1000으로 제한되어 있습니다. 객체에 대해 ACL 제어가 필요하지 않은 경우 설정하지 마십시오. 기본으로 버킷 권한은 계승됩니다.

#### 방식 프로토타입
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
| 매개변수 이름 | 매개변수 설명 | 유형 |
|---------|---------|---------|
| options | COS 요청 옵션 |Struct|  
| bucket | 버킷 이름, 버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다 | String |  
| object | 객체 이름. |String|  
| cos_acl | 사용자가 지정 가능한 권한입니다. 유효 값: COS_ACL_PRIVATE(0), COS_ACL_PUBLIC_READ(1), COS_ACL_PUBLIC_READ_WRITE(2). 기본값: COS_ACL_PRIVATE(0)|Enum|   
| grant_read | 읽기 권한 부여자 |String|  
| grant_write | 쓰기 권한 부여자|String|  
| grant_full_ctrl | 읽기/쓰기 권한 부여자 |String|  
| resp_headers | HTTP 응답 헤더를 반환합니다 | Struct |  

#### 반환 결과 설명
| 반환 결과 | 설명 | 유형 |
|---------|---------|---------|
| code | 오류 코드 | Int |        
| error_code | 오류 코드 내용| String |   
| error_msg |오류 코드 설명 | String |   
| req_id | 요청 정보 ID |String|

#### 예시
```cpp
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_string_t object;
    cos_table_t *resp_headers = NULL;

    //create memory pool
    cos_pool_create(&p, NULL);

    //init request options
    options = cos_request_options_create(p);
    options->config = cos_config_create(options->pool);
    init_test_config(options->config, is_cname);
    cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
    cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
    cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
    cos_str_set(&options->config->appid, TEST_APPID);
    options->config->is_cname = is_cname;
    options->ctl = cos_http_controller_create(options->pool, 0);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    //put object acl
    cos_str_set(&object, TEST_OBJECT_NAME);
    cos_string_t read;
    cos_str_set(&read, "id=\"qcs::cam::uin/12345:uin/12345\", id=\"qcs::cam::uin/45678:uin/45678\"");
    s = cos_put_object_acl(options, &bucket, &object, cos_acl, &read, NULL, NULL, &resp_headers);
    if (cos_status_is_ok(s)) {
        printf("put object acl succeeded\n");
    } else {
        printf("put object acl failed\n");
    }

    //destroy memory pool
    cos_pool_destroy(p);  
```

###  Get Object ACL
#### 기능 설명
Get Object ACL API는 버킷의 어느 객체의 액세스 권한을 가져오는 데 사용됩니다. 이 API는 버킷의 소유자만 조작 권한이 있습니다.

#### 방식 프로토타입
```cpp
cos_status_t *cos_get_object_acl(const cos_request_options_t *options,
                                 const cos_string_t *bucket,
                                 const cos_string_t *object,
                                 cos_acl_params_t *acl_param,
                                 cos_table_t **resp_headers)
```

#### 매개변수 설명
| 매개변수 이름 | 매개변수 설명 | 유형 |
|---------|---------|---------|
| options | COS 요청 옵션 | Struct |  
| bucket | 버킷 이름, 버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다 | String |  
| object | 객체 이름 |String|  
| acl_param | Get Object ACL 작업 매개변수 |Struct|  
| owner_id | Get Object ACL 작업으로 반환된 버킷 소유자 ID |String|  
| owner_name | Get Object ACL 작업으로 반환된 버킷 소유자 이름 |String|  
| object_list | Get Object ACL 작업으로 반환된 권한을 부여받은 자 정보 및 권한 정보 |Struct|  
| type | Get Object ACL 작업으로 반환된 권한을 부여받은 자 계정 유형 |String|  
| id | Get Object ACL 작업으로 반환된 권한을 부여받은 자 계정 ID |String|  
| name | Get Object ACL 작업으로 반환된 권한을 부여받은 자 사용자 이름 |String|  
| permission | Get Object ACL 작업으로 반환된 권한을 부여받은 자 권한 정보 |String|  
| resp_headers | HTTP 응답 헤더를 반환합니다 | Struct |  

#### 반환 결과 설명
| 반환 결과 | 설명 | 유형 |
|---------|---------|---------|
| code | 오류 코드 | Int |        
| error_code | 오류 코드 내용| String |   
| error_msg |오류 코드 설명 | String |   
| req_id | 요청 정보 ID |String|

#### 예시
```cpp
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_string_t object;
    cos_table_t *resp_headers = NULL;

    //create memory pool
    cos_pool_create(&p, NULL);

    //init request options
    options = cos_request_options_create(p);
    options->config = cos_config_create(options->pool);
    init_test_config(options->config, is_cname);
    cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
    cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
    cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
    cos_str_set(&options->config->appid, TEST_APPID);
    options->config->is_cname = is_cname;
    options->ctl = cos_http_controller_create(options->pool, 0);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    //get object acl
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

    //destroy memory pool
    cos_pool_destroy(p);
```

###  Put Object Copy
#### 기능 설명
Put Object Copy 요청은 파일을 소스 경로에서 대상 경로로 복사합니다.

#### 방식 프로토타입
```cpp
cos_status_t *cos_copy_object(const cos_request_options_t *options,
                              const cos_string_t *copy_source,
                              const cos_string_t *dest_bucket,
                              const cos_string_t *dest_object,
                              cos_table_t *headers,
                              cos_copy_object_params_t *copy_object_param,
                              cos_table_t **resp_headers);
```

#### 매개변수 설명
| 매개변수 이름 | 매개변수 설명 | 유형 |
|---------|---------|---------|
| options | COS 요청 옵션 |Struct|  
| copy_source | 소스 파일 경로 |String|  
| dest_bucket | 대상 버킷 이름, 버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다 | String|  
| dest_bucket | 대상 객체 이름 |String|  
| headers | 첨부된 COS 요청 헤더 |Struct|  
| copy_object_param | Put Object Copy 작업 매개변수 |Struct|   
| etag | 반환 파일의 MD5 알고리즘 검증값 |String|  
| last_modify | 반환 파일의 마지막 수정 시간, GMT 형식 |String|  
| resp_headers | HTTP 응답 헤더를 반환합니다 | Struct |

#### 반환 결과 설명
| 반환 결과 | 설명 | 유형 |
|---------|---------|---------|
| code | 오류 코드 | Int |        
| error_code | 오류 코드 내용| String |   
| error_msg |오류 코드 설명 | String |   
| req_id | 요청 정보 ID |String|

#### 예시
```cpp
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_string_t object;
    cos_table_t *resp_headers = NULL;

    //create memory pool
    cos_pool_create(&p, NULL);

    //init request options
    options = cos_request_options_create(p);
    options->config = cos_config_create(options->pool);
    init_test_config(options->config, is_cname);
    cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
    cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
    cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
    cos_str_set(&options->config->appid, TEST_APPID);
    options->config->is_cname = is_cname;
    options->ctl = cos_http_controller_create(options->pool, 0);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    //put object copy
    cos_str_set(&object, TEST_OBJECT_NAME);
    cos_string_t copy_source;
    cos_str_set(&copy_source, TEST_COPY_SRC);
    cos_copy_object_params_t *params = NULL;
    params = cos_create_copy_object_params(p);
    s = cos_copy_object(options, &copy_source, &bucket, &object, NULL, params, &resp_headers);
    if (cos_status_is_ok(s)) {
        printf("put object copy succeeded\n");
    } else {
        printf("put object copy failed\n");
    }

    //destroy memory pool
    cos_pool_destroy(p);  
```

## 멀티파트 업로드 작업
###  Initiate Multipart Upload
#### 기능 설명
Initiate Multipart Upload 요청은 멀티파트 업로드를 초기화합니다. 해당 요청을 성공적으로 실행하면 후속 Upload Part 요청에 사용되는 Upload ID가 반환됩니다.

#### 방식 프로토타입
```cpp
cos_status_t *cos_init_multipart_upload(const cos_request_options_t *options,
                                        const cos_string_t *bucket,
                                        const cos_string_t *object,
                                        cos_string_t *upload_id,
                                        cos_table_t *headers,
                                        cos_table_t **resp_headers);
```

#### 매개변수 설명
| 매개변수 이름 | 매개변수 설명 | 유형 |
|---------|---------|---------|
| options | COS 요청 옵션 |Struct|  
| bucket | 버킷 이름, 버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다 | String |  
| object | 객체 이름 |String|  
| upload_id | 작업으로 반환된 Upload ID |String|  
| headers | 첨부된 COS 요청 헤더 |Struct|  
| resp_headers | HTTP 응답 헤더를 반환합니다 |Struct|

#### 반환 결과 설명
| 반환 결과 | 설명 | 유형 |
|---------|---------|---------|
| code | 오류 코드 | Int |        
| error_code | 오류 코드 내용| String |   
| error_msg |오류 코드 설명 | String |   
| req_id | 요청 정보 ID |String|

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

    //create memory pool
    cos_pool_create(&p, NULL);

    //init request options
    options = cos_request_options_create(p);
    options->config = cos_config_create(options->pool);
    init_test_config(options->config, is_cname);
    cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
    cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
    cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
    cos_str_set(&options->config->appid, TEST_APPID);
    options->config->is_cname = is_cname;
    options->ctl = cos_http_controller_create(options->pool, 0);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    //init mulitipart upload
    cos_str_set(&object, TEST_OBJECT_NAME);
    s = cos_init_multipart_upload(options, &bucket, &object,
                                  &upload_id, headers, &resp_headers);
    if (cos_status_is_ok(s)) {
        printf("init multipart upload succeeded\n");
    } else {
        printf("init multipart upload failed\n");
    }

    //destroy memory pool
    cos_pool_destroy(p);
```

###  Upload Part
#### 기능 설명
Upload Part 요청은 초기화 후 멀티파트 업로드를 구현하며, 지원되는 파트 수량은 1에서 10000까지이고, 파트의 크기는 1MB~5GB입니다. 각 Upload Part 요청 시 partNumber 및 uploadID가 있어야 하며, partNumber는 파트의 번호로서 비순차적 업로드를 지원합니다.

#### 방식 프로토타입
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
| 매개변수 이름 | 매개변수 설명 | 유형 |
|---------|---------|---------|
| options | COS 요청 옵션 | Struct |  
| bucket | 버킷 이름, 버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다 | String |  
| object | 객체 이름 |String|  
| upload_id | 업로드 태스크 번호 |String|  
| part_num | 파트 번호 |Int|  
| upload_file | 업로드 대기 중인 로컬 파일 정보 |Struct|  
| resp_headers | HTTP 응답 헤더를 반환합니다 |Struct|  

#### 반환 결과 설명
| 반환 결과 | 설명 | 유형 |
|---------|---------|---------|
| code | 오류 코드 | Int |        
| error_code | 오류 코드 내용| String |   
| error_msg |오류 코드 설명 | String |   
| req_id | 요청 정보 ID |String|

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

    //create memory pool
    cos_pool_create(&p, NULL);

    //init request options
    options = cos_request_options_create(p);
    options->config = cos_config_create(options->pool);
    init_test_config(options->config, is_cname);
    cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
    cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
    cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
    cos_str_set(&options->config->appid, TEST_APPID);
    options->config->is_cname = is_cname;
    options->ctl = cos_http_controller_create(options->pool, 0);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    //upload part from file
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

    //destroy memory pool
    cos_pool_destroy(p);
```

###  Complete Multipart Upload
#### 기능 설명
Complete Multipart Upload는 전체 멀티파트 업로드를 구현할 수 있습니다. Upload Parts를 사용하여 모든 파트를 업로드한 후, 이 API를 사용하여 업로드를 완료할 수 있습니다. 이 API 사용 시 본문에 각 파트의 PartNumber 및 ETag를 제공하여 파트의 정확성을 인증해야 합니다.

#### 방식 프로토타입
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
| 매개변수 이름 | 매개변수 설명 | 유형 |
|---------|---------|---------|
| options | COS 요청 옵션 |Struct|  
| bucket | 버킷 이름, 버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다 | String |  
| object | 객체 이름 |String|  
| upload_id | 업로드 태스크 번호 |String|  
| part_list | 멀티파트 업로드 완료 매개변수 |Struct|  
| part_number | 파트 번호 |String|  
| etag | 파트의 ETag 값. sha1 인증값이며, 인증값 전후에 큰따옴표를 추가해야 합니다. 예: "3a0f1fd698c235af9cf098cb74aa25bc" |String|  
| headers | 첨부된 COS 요청 헤더 |Struct|
| resp_headers | HTTP 응답 헤더를 반환합니다 | Struct |  

#### 반환 결과 설명
| 반환 결과 | 설명 | 유형 |
|---------|---------|---------|
| code | 오류 코드 | Int |        
| error_code | 오류 코드 내용| String |   
| error_msg |오류 코드 설명 | String |   
| req_id | 요청 정보 ID | String |

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

    //create memory pool
    cos_pool_create(&p, NULL);

    //init request options
    options = cos_request_options_create(p);
    options->config = cos_config_create(options->pool);
    init_test_config(options->config, is_cname);
    cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
    cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
    cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
    cos_str_set(&options->config->appid, TEST_APPID);
    options->config->is_cname = is_cname;
    options->ctl = cos_http_controller_create(options->pool, 0);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    //list part
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

    //complete multipart
    s = cos_complete_multipart_upload(options, &bucket, &object, &upload_id,
            &complete_part_list, complete_headers, &resp_headers);

    if (cos_status_is_ok(s)) {
        printf("Complete multipart upload from file succeeded, upload_id:%.*s\n",
               upload_id.len, upload_id.data);
    } else {
        printf("Complete multipart upload from file failed\n");
    }

    //destroy memory pool
    cos_pool_destroy(p);
```

###  List Parts
#### 기능 설명
List Parts는 특정 멀티파트 업로드에서 이미 업로드된 파트를 조회하는 데 사용됩니다.

#### 방식 프로토타입
```cpp
cos_status_t *cos_list_upload_part(const cos_request_options_t *options,
                                   const cos_string_t *bucket,
                                   const cos_string_t *object,
                                   const cos_string_t *upload_id,
                                   cos_list_upload_part_params_t *params,
                                   cos_table_t **resp_headers);
```

#### 매개변수 설명
| 매개변수 이름 | 매개변수 설명 | 유형 |
|---------|---------|---------|
| options | COS 요청 옵션 |Struct|  
| bucket | 버킷 이름, 버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다 | String |  
| object | 객체 이름 |String|  
| upload_id | 업로드 태스크 번호 |String|  
| params | List Parts 작업 매개변수 |Struct|
| part_number_marker| 기본으로 UTF-8 이진 순서로 항목이 나열되며, 모든 나열 항목은 marker에서 시작합니다 |String|  
| encoding_type | 반환값의 인코딩 방식을 규정합니다 |String|  
| max_ret | 1회에 최대 반환 항목 수, 기본값 1000 |String|  
| truncated | 반환 항목이 잘라내기 여부, 'true' 또는 'false' |Boolean|  
| next_part_number_marker | 반환 항목이 잘린 경우, 반환되는 NextMarker는 다음 항목의 시작점입니다 |String|  
| part_list | 완료된 파트의 정보|Struct|      
| part_number | 파트 번호 |String|  
| size | 파트 크기, 단위는 바이트 |String|  
| etag | 파트의 SHA-1 알고리즘 검증값 |String|  
| last_modified | 파트 마지막 수정 시간 |String|  
| resp_headers | HTTP 응답 헤더를 반환합니다 | Struct |  

#### 반환 결과 설명
| 반환 결과 | 설명 | 유형 |
|---------|---------|---------|
| code | 오류 코드 | Int |        
| error_code | 오류 코드 내용| String |   
| error_msg |오류 코드 설명 | String |   
| req_id | 요청 정보 ID |String|

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

    //create memory pool
    cos_pool_create(&p, NULL);

    //init request options
    options = cos_request_options_create(p);
    options->config = cos_config_create(options->pool);
    init_test_config(options->config, is_cname);
    cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
    cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
    cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
    cos_str_set(&options->config->appid, TEST_APPID);
    options->config->is_cname = is_cname;
    options->ctl = cos_http_controller_create(options->pool, 0);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    //list part
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

    //complete multipart
    s = cos_complete_multipart_upload(options, &bucket, &object, &upload_id,
            &complete_part_list, complete_headers, &resp_headers);

    if (cos_status_is_ok(s)) {
        printf("Complete multipart upload from file succeeded, upload_id:%.*s\n",
               upload_id.len, upload_id.data);
    } else {
        printf("Complete multipart upload from file failed\n");
    }

    //destroy memory pool
    cos_pool_destroy(p);
```

###  Abort Multipart Upload
#### 기능 설명
Abort Multipart Upload는 멀티파트 업로드를 취소하고 이미 업로드된 파트를 삭제하는 데 사용됩니다. Abort Multipart Upload 호출 시, 이 Upload Parts 업로드 파트를 사용 중일 때 요청이 있으면 Upload Parts는 실패를 반환합니다.

#### 방식 프로토타입
```cpp
cos_status_t *cos_abort_multipart_upload(const cos_request_options_t *options,
                                         const cos_string_t *bucket,
                                         const cos_string_t *object,
                                         cos_string_t *upload_id,
                                         cos_table_t **resp_headers);
```

#### 매개변수 설명
| 매개변수 이름 | 매개변수 설명 | 유형 |
|---------|---------|---------|
| options | COS 요청 옵션 | Struct |
| bucket | 버킷 이름, 버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다 | String |  
| object | 객체 이름 |String|  
| upload_id | 업로드 태스크 번호 |String|
| resp_headers | HTTP 응답 헤더를 반환합니다 |Struct|  


#### 반환 결과 설명
| 반환 결과 | 설명 | 유형 |
|---------|---------|---------|
| code | 오류 코드 | Int |        
| error_code | 오류 코드 내용| String |   
| error_msg |오류 코드 설명 | String |   
| req_id | 요청 정보 ID |String|

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

    //create memory pool & init request options
    cos_pool_create(&p, NULL);
    options = cos_request_options_create(p);
    init_test_request_options(options, is_cname);
    headers = cos_table_make(p, 1);
    cos_str_set(&bucket, TEST_BUCKET_NAME);
    cos_str_set(&object, TEST_MULTIPART_OBJECT);

    //init multipart upload
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

    //abort multipart upload
    s = cos_abort_multipart_upload(options, &bucket, &object, &upload_id,
                                   &resp_headers);

    if (cos_status_is_ok(s)) {
        printf("Abort multipart upload succeeded, upload_id::%.*s\n",
               upload_id.len, upload_id.data);
    } else {
        printf("Abort multipart upload failed\n");
    }    

    cos_pool_destroy(p);
```

###  List Multipart Uploads
#### 기능 설명
List Multiparts Uploads는 진행 중인 멀티파트 업로드를 조회하는 데 사용됩니다. 1회 최대 1000개의 진행 중인 멀티파트 업로드를 나열할 수 있습니다.

#### 방식 프로토타입
```cpp
cos_status_t *cos_list_multipart_upload(const cos_request_options_t *options,
                                        const cos_string_t *bucket,
                                        cos_list_multipart_upload_params_t *params,
                                        cos_table_t **resp_headers);
```

#### 매개변수 설명
| 매개변수 이름 | 매개변수 설명 | 유형 |
|---------|---------|---------|
| options | COS 요청 옵션 | Struct |  
| bucket | 버킷 이름, 버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다 | String |  
| params | List Multipart Uploads 작업 매개변수 |Struct|  
| encoding_type | 반환값의 인코딩 방식을 규정합니다 |String|  
| prefix |접두사 매칭, 반환되는 파일 접두사 주소 시정에 사용합니다 |String|
| upload_id_marker | 반환 항목이 잘린 경우, 반환되는 NextMarker는 다음 항목의 시작점입니다 |String|
| delimiter | 구분자는 부호입니다.<br>Prefix가 있으면, 해당 Prefix와 delimiter 사이에 동일한 경로를 같은 종류로 분류하고, Common Prefix라 정의입니다. 그런 다음 모든 Common Prefix를 나열합니다.<br>Prefix가 없을 경우, 경로 시작점에서 시작합니다 |String|  
| max_ret | 1회에 최대 반환 항목 수, 기본값 1000 |String|  
| key_marker | upload-id-marker와 함께 사용합니다.<br>upload-id-marker가 지정되지 않았을 때, ObjectName 알파벳 순서가 key-marker보다 큰 항목이 나열됩니다.<br>upload-id-marker가 지정되었을 때, ObjectName 알파벳 순서가 key-marker보다 큰 항목이 나열되고, ObjectName 알파벳 순서가 key-marker와 동일하고 동시에 UploadID가 upload-id-marker보다 큰 항목을 나열합니다 |String|  
| upload_id_marker | key-marker와 함께 사용합니다.<br>key-marker가 지정되지 않았을 때, upload-id-marker는 무시됩니다.<br>key-marker가 지정되었을 때, ObjectName 알파벳 순서가 key-marker 뒤에 있는 항목을 나열하고, ObjectName 알파벳 순서가 key-marker와 같고 UploadID가 upload-id-marker 뒤에 있는 항목을 나열합니다 |String|
| truncated | 반환 항목이 잘라내기 여부, 'true' 또는 'false' |Boolean|  
| next_key_marker | 반환 항목이 잘린 경우, 반환되는 NextMarker는 다음 항목의 시작점입니다 |String|  
| next_upload_id_marker | 반환 항목이 잘린 경우, 반환되는 NextMarker는 다음 항목의 시작점입니다 |String|  
| upload_list | 멀티파트 업로드 정보 |Struct|  
| key | 객체 이름 |String|  
| upload_id | 이번 멀티파트 업로드의 ID |String|  
| initiated | 이번 멀티파트 업로드 작업의 시작 시간 |String|  
| resp_headers | HTTP 응답 헤더를 반환합니다 | Struct |  

```
typedef struct {
    cos_list_t node;
    cos_string_t key;
    cos_string_t upload_id;
    cos_string_t initiated;
} cos_list_multipart_upload_content_t;
```


#### 반환 결과 설명
| 반환 결과 | 설명 | 유형 |
|---------|---------|---------|
| code | 오류 코드 | Int |        
| error_code | 오류 코드 내용| String |   
| error_msg |오류 코드 설명 | String |   
| req_id | 요청 정보 ID |String|

#### 예시
```cpp
    cos_pool_t *p = NULL;
    cos_string_t bucket;
    int is_cname = 0;
    cos_table_t *resp_headers = NULL;
    cos_request_options_t *options = NULL;
    cos_status_t *s = NULL;
    cos_list_multipart_upload_params_t *list_multipart_params = NULL;

    //create memory pool & init request options
    cos_pool_create(&p, NULL);
    options = cos_request_options_create(p);
    init_test_request_options(options, is_cname);
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    //list multipart upload
    list_multipart_params = cos_create_list_multipart_upload_params(p);
    list_multipart_params->max_ret = 999;
    s = cos_list_multipart_upload(options, &bucket, list_multipart_params, &resp_headers);
    log_status(s);

    cos_pool_destroy(p);
```

## 비정상 설명

SDK 실패 시, 결과 정보는 API에서 반환한 cos_status_t 아키텍처에 포함됩니다.

다음은 cos_status_t 아키텍처의 설명입니다.

| cos_status_t 멤버 | 설명                                       | 유형        |
| ---------------- | ---------------------------------------- | --------- |
| code    | 응답의 상태 코드, 4xx는 클라이언트로 인해 요청이 실패했음을 의미하고, 5xx는 서버 비정상으로 인한 실패입니다. [COS 오류 정보](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오               | Int    |
| error_code      | 요청 실패 시 본문에서 반환된 오류 코드는 [COS 오류 정보](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오                              | String    |
| error_msg   | 요청 실패 시 본문에서 반환된 오류 메시지는 [COS 오류 정보](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오 | String    |
| req_id | 요청 ID, 사용자의 요청을 유일하게 표시하는 데 사용합니다 | String    |
