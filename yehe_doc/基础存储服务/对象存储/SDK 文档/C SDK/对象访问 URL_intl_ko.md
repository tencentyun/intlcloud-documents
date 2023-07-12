## 소개
본 문서는 객체 액세스 URL을 획득하는 코드 예시를 제공합니다.

## 객체 액세스 URL 획득

#### 기능 설명
객체 액세스 URL을 획득하여 익명 다운로드 또는 배포에 사용합니다.

#### 메소드 프로토타입

```
const char *cos_gen_object_url(const cos_request_options_t *options, const cos_string_t *bucket, const cos_string_t *object)
```

#### 요청 예시

[//]: # ".cssg-snippet-get-object-url-alias"
```go
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
init_test_request_options(options, is_cname);
cos_str_set(&bucket, TEST_BUCKET_NAME);
cos_str_set(&object, "exampleobject");

printf("url:%s\n", cos_gen_object_url(options, &bucket, &object));

cos_pool_destroy(p);
```

#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   |유형 | 필수 입력 여부 |
| -------------- | -------------- |---------- | ----------- |
| options | COS 요청 옵션 | Struct | 예 |
| bucket | 버킷 이름. Bucket의 이름 생성 형식은 BucketName-APPID로 여기에 입력하는 버킷 이름은 반드시 해당 형식을 따라야 함 | Struct  | 예 |
| object | 객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg임 | String | 예 |

#### 반환 결과 설명

해당 방법의 반환값은 객체 액세스 URL입니다.	
