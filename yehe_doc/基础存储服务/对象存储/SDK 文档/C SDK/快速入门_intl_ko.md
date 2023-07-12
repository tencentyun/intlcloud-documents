## 다운로드 및 설치

#### 관련 리소스

- COS의 XML C SDK 소스 코드 다운로드 주소: [XML C SDK](https://github.com/tencentyun/cos-c-sdk-v5)
- 예시 Demo 다운로드 주소: [XML C SDK Demo](https://github.com/tencentyun/cos-c-sdk-v5/blob/master/cos_c_sdk_test/cos_demo.c)
- SDK 로그 업데이트는 [ChangeLog](https://github.com/tencentyun/cos-c-sdk-v5/blob/master/CHANGELOG.md)를 참고하십시오.
- SDK FAQ는 [C SDK FAQ](https://intl.cloud.tencent.com/document/product/436/40772)를 참고하십시오.


>? SDK 사용 시 함수 또는 메소드 없음 등 오류가 발생하였을 경우, 먼저 SDK를 최신 버전으로 업데이트한 후 재시도하십시오.
>

#### 환경 종속

종속 라이브러리: libcurl apr apr-util minixml。

#### SDK 설치

1. CMake 툴(2.6.0 이상 버전 권장)을 설치합니다. [여기](http://www.cmake.org/download/)를 클릭하여 다운로드하십시오. 설치 방법은 다음과 같습니다.
```bash
./configure
make
make install
```
2. libcurl(7.32.0 이상 버전 권장)을 설치합니다. [여기](http://curl.haxx.se/download.html?spm=5176.doc32132.2.7.23MmBq)를 클릭하여 다운로드하십시오. 설치 방법은 다음과 같습니다.
```bash
./configure
make
make install
```
3. apr(1.5.2 이상 버전 권장)을 설치합니다. [여기](https://apr.apache.org/download.cgi?spm=5176.doc32132.2.9.23MmBq&file=download.cgi)를 클릭하여 다운로드하십시오. 설치 방법은 다음과 같습니다.
```bash
./configure
make
make install
```
4. apr-util(1.5.4 이상 버전 권장)을 설치합니다. [여기](https://apr.apache.org/download.cgi?spm=5176.doc32132.2.10.23MmBq&file=download.cgi)를 클릭하여 다운로드하십시오. 설치 시 `--with-apr` 옵션을 지정해야 합니다. 설치 방법은 다음과 같습니다.
```bash
./configure --with-apr=/your/apr/install/path
make
make install
```
5. minixml(2.8 - 2.12 버전 권장)을 설치합니다. [여기](https://www.msweet.org/mxml/)를 클릭하여 다운로드하십시오. 설치 방법은 다음과 같습니다.
```bash
./configure
make
make install
```
6. COS C SDK를 컴파일합니다. [XML C SDK 소스 코드](https://github.com/tencentyun/cos-c-sdk-v5)를 다운로드하고 다음 컴파일 명령어를 실행합니다.
```bash
cmake .
make
make install
```

## 사용하기

다음은 XML C SDK를 사용하는 일반적인 프로세스입니다.

1. SDK를 초기화합니다.
2. 요청 옵션 매개변수를 설정합니다. APPID, SecretId, SecretKey, Bucket 등의 명칭에 대한 의미 및 획득 방법은 [COS 용어 정보](https://intl.cloud.tencent.com/document/product/436/7751)를 참고하십시오.
 - APPID는 Tencent Cloud 계정 신청 후 시스템에서 할당하는 계정 식별자 중 하나입니다.
 - access_key_id와 access_key_secret는 계정 API 키입니다.
 - endpoint는 COS 액세스 도메인 정보입니다. 자세한 내용은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224) 문서를 참고하십시오. 예를 들어, 광저우 리전의 endpoint는 `cos.ap-guangzhou.myqcloud.com`이며, 글로벌 가속 도메인의 endpoint는 `cos.accelerate.myqcloud.com`입니다. endpoint에는 http 또는 https를 추가할 수 있으며, SDK는 기본적으로 http를 통해 COS에 액세스합니다. https를 통한 광저우 리전 액세스의 endpoint는 `https://cos.ap-guangzhou.myqlcoud.com`입니다.
 - is_cname은 endpoint의 사용자 정의 도메인 여부를 의미합니다. is_cname이 1로 설정된 경우 endpoint는 사용자 정의 도메인이라는 의미입니다.
3. API 인터페이스에 필요한 매개변수를 설정합니다.
4. SDK API를 호출하여 요청을 실행하고 요청 응답 결과를 획득합니다.

### 초기화

```cpp
int main(int argc, char *argv[])
{
    /* 프로그램 게이트에서 cos_http_io_initialize 방법을 호출합니다. 이 방법은 내부적으로 전역 리소스를 초기화하며 네트워크, 메모리 등 부분과 관련되어 있습니다. */
    if (cos_http_io_initialize(NULL, 0) != COSE_OK) {
        exit(1);
    }

    /* COS SDK의 인터페이스를 호출하여 파일 업로드 또는 다운로드 */
    /* ... 여기서는 사용자 로직 코드 생략 */

    /* 프로그램 종료 전, cos_http_io_deinitialize 방법을 호출하여 릴리스하기 전 할당하는 전역 리소스 */
    cos_http_io_deinitialize();
    return 0;
}
```

### 초기화 요청 옵션

```cpp
/* apr_pool_t에 해당하며, 메모리를 관리하는 메모리 풀입니다. apr 라이브러리의 구현 코드입니다. */
cos_pool_t *pool;
cos_request_options_t *options;

/* 새 메모리 풀을 생성합니다. 두 번째 매개변수는 NULL이며, 다른 메모리 풀을 상속하지 않는다는 의미입니다. */
cos_pool_create(&pool, NULL);

/* options를 생성하고 초기화합니다. 이 매개변수 내부에는 주로 endpoint, access_key_id, acces_key_secret, is_cname, curl 매개변수 등 전역 설정 정보가 포함되어 있습니다.
 * options의 메모리는 pool에서 할당합니다. 이후 계속해서 pool을 릴리스한 후 options의 메모리까지 릴리스한 정도가 되면 단독으로 메모리를 릴리스할 필요가 없습니다.
 */ 
options = cos_request_options_create(pool);
options->config = cos_config_create(options->pool);

/* cos_str_set은 char* 유형의 문자열을 사용해 cos_string_t 유형을 초기화합니다. */
cos_str_set(&options->config->endpoint, "<사용자 Endpoint>");              //Endpoint는 사용자가 소재하고 있는 리전의 COS 서비스 도메인에 따라 입력
cos_str_set(&options->config->access_key_id, "<사용자 SecretId>");         //COS 서비스 가입 후 획득하는 SecretId
cos_str_set(&options->config->access_key_secret, "<사용자 SecretKey>");    //COS 서비스 가입 후 획득하는 SecretKey
cos_str_set(&options->config->appid, "<사용자 AppId>");                    //COS 서비스 가입 후 획득하는 AppId

/* sts_token 설정으로 임시 키를 사용할 수 있습니다. 임시 키 사용 시 access_key_id와 access_key_secret은 모두 해당 임시 키의 SecretId와 SecretKey로 설정해야 합니다. */
//cos_str_set(&options->config->sts_token, "MyTokenString");
/* CNAME 사용 여부 */
options->config->is_cname = 0;
/* 사용자 정의 도메인으로 COS 액세스 */
/*
options->config->is_cname = 1;
cos_str_set(&options->config->endpoint, "<사용자 정의 도메인>");
*/

/* 타임아웃 시간 등과 같은 네트워크 설정 관련 매개변수 */
options->ctl = cos_http_controller_create(options->pool, 0);

/* 업로드 요청 시 Content-MD5 헤더 자동 추가 설정 여부에 사용합니다. enable이 COS_FALSE인 경우 업로드 요청 시 Content-MD5 헤더가 자동으로 추가되지 않으며, enable이 COS_TRUE 인 경우 업로드 요청 시 Content-MD5 헤더가 자동으로 추가됩니다. 이 항목을 설정하지 않으면 기본적으로 Content-MD5 헤더가 추가됩니다. */
cos_set_content_md5_enable(options->ctl, COS_FALSE);

/* 요청 라우팅 주소 및 포트를 설정하는 데 사용됩니다. 일반적으로 이 매개변수는 설정할 필요가 없으며, 요청은 리졸브 결과에 따라 라우팅됩니다. */
//cos_set_request_route(options->ctl, "192.168.12.34", 80);
```

>? 임시 키 생성 및 사용에 대한 자세한 내용은 [임시 키 생성 및 사용 가이드](https://intl.cloud.tencent.com/document/product/436/14048)를 참고하십시오.
>


### 버킷 생성하기

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_acl_e cos_acl = COS_ACL_PRIVATE;
cos_string_t bucket;
cos_table_t *resp_headers = NULL;

/* 새 메모리 풀을 생성합니다. 두 번째 매개변수는 NULL이며, 다른 메모리 풀을 상속하지 않는다는 의미입니다. */
cos_pool_create(&p, NULL);

/* options를 생성하고 초기화합니다. 이 매개변수 내부에는 주로 endpoint, access_key_id, acces_key_secret, is_cname, curl 매개변수 등 전역 설정 정보가 포함되어 있습니다.
 * options의 메모리는 pool에서 할당합니다. 이후 계속해서 pool을 릴리스한 후 options의 메모리까지 릴리스한 정도가 되면 단독으로 메모리를 릴리스할 필요가 없습니다.
 */
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
init_test_config(options->config, is_cname);

/* appid, endpoint, access_key_id, acces_key_secret, is_cname, curl 매개변수 등 설정 정보 설정 */
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
/* 버킷의 이름 생성 형식은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 해당 형식을 따라야 합니다. */
cos_str_set(&bucket, TEST_BUCKET_NAME);

/* api를 호출해 버킷 생성 */
s = cos_create_bucket(options, &bucket, cos_acl, &resp_headers);
if (cos_status_is_ok(s)) {
		printf("create bucket succeeded\n");
} else {
		printf("create bucket failed\n");
}

//destroy memory pool
cos_pool_destroy(p); 
```

### 객체 리스트 조회

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_list_object_params_t *list_params = NULL;
cos_string_t bucket;
cos_table_t *resp_headers = NULL;

/* 새 메모리 풀을 생성합니다. 두 번째 매개변수는 NULL이며, 다른 메모리 풀을 상속하지 않는다는 의미입니다. */
cos_pool_create(&p, NULL);

/* options를 생성하고 초기화합니다. 이 매개변수 내부에는 주로 endpoint, access_key_id, acces_key_secret, is_cname, curl 매개변수 등 전역 설정 정보가 포함되어 있습니다.
 * options의 메모리는 pool에서 할당합니다. 이후 계속해서 pool을 릴리스한 후 options의 메모리까지 릴리스한 정도가 되면 단독으로 메모리를 릴리스할 필요가 없습니다.
 */
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
init_test_config(options->config, is_cname);

/* appid, endpoint, access_key_id, acces_key_secret, is_cname, curl 매개변수 등 설정 정보 설정 */
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
/* 버킷의 이름 생성 형식은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 해당 형식을 따라야 합니다. */
cos_str_set(&bucket, TEST_BUCKET_NAME);

/* api를 호출해 객체 리스트 조회 */
list_params = cos_create_list_object_params(p);
cos_str_set(&list_params->encoding_type, "url");
s = cos_list_object(options, &bucket, list_params, &resp_headers);
if (cos_status_is_ok(s)) {
		printf("list object succeeded\n");
} else {
		printf("list object failed\n");
}

//destroy memory pool
cos_pool_destroy(p); 
```

### 객체 업로드

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_string_t file;
cos_table_t *resp_headers = NULL;

/* 새 메모리 풀을 생성합니다. 두 번째 매개변수는 NULL이며, 다른 메모리 풀을 상속하지 않는다는 의미입니다. */
cos_pool_create(&p, NULL);

/* options를 생성하고 초기화합니다. 이 매개변수 내부에는 주로 endpoint, access_key_id, acces_key_secret, is_cname, curl 매개변수 등 전역 설정 정보가 포함되어 있습니다.
 * options의 메모리는 pool에서 할당합니다. 이후 계속해서 pool을 릴리스한 후 options의 메모리까지 릴리스한 정도가 되면 단독으로 메모리를 릴리스할 필요가 없습니다.
 */
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
init_test_config(options->config, is_cname);

/* appid, endpoint, access_key_id, acces_key_secret, is_cname, curl 매개변수 등 설정 정보 설정 */
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
/* 버킷의 이름 생성 형식은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 해당 형식을 따라야 합니다. */
cos_str_set(&bucket, TEST_BUCKET_NAME);

/* api를 호출해 객체 업로드 */
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

### 객체 다운로드

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_string_t file;
cos_table_t *resp_headers = NULL;

/* 새 메모리 풀을 생성합니다. 두 번째 매개변수는 NULL이며, 다른 메모리 풀을 상속하지 않는다는 의미입니다. */
cos_pool_create(&p, NULL);

/* options를 생성하고 초기화합니다. 이 매개변수 내부에는 주로 endpoint, access_key_id, acces_key_secret, is_cname, curl 매개변수 등 전역 설정 정보가 포함되어 있습니다.
 * options의 메모리는 pool에서 할당합니다. 이후 계속해서 pool을 릴리스한 후 options의 메모리까지 릴리스한 정도가 되면 단독으로 메모리를 릴리스할 필요가 없습니다.
 */
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
init_test_config(options->config, is_cname);

/* appid, endpoint, access_key_id, acces_key_secret, is_cname, curl 매개변수 등 설정 정보 설정 */
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
/* 버킷의 이름 생성 형식은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 해당 형식을 따라야 합니다. */
cos_str_set(&bucket, TEST_BUCKET_NAME);

/* api를 호출해 객체 다운로드 */
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

### 객체 삭제

```cpp
cos_pool_t *p = NULL;
int is_cname = 0;
cos_status_t *s = NULL;
cos_request_options_t *options = NULL;
cos_string_t bucket;
cos_string_t object;
cos_table_t *resp_headers = NULL;

/* 새 메모리 풀을 생성합니다. 두 번째 매개변수는 NULL이며, 다른 메모리 풀을 상속하지 않는다는 의미입니다. */
cos_pool_create(&p, NULL);

/* options를 생성하고 초기화합니다. 이 매개변수 내부에는 주로 endpoint, access_key_id, acces_key_secret, is_cname, curl 매개변수 등 전역 설정 정보가 포함되어 있습니다.
 * options의 메모리는 pool에서 할당합니다. 이후 계속해서 pool을 릴리스한 후 options의 메모리까지 릴리스한 정도가 되면 단독으로 메모리를 릴리스할 필요가 없습니다.
 */
options = cos_request_options_create(p);
options->config = cos_config_create(options->pool);
init_test_config(options->config, is_cname);

/* appid, endpoint, access_key_id, acces_key_secret, is_cname, curl 매개변수 등 설정 정보 설정 */
cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
cos_str_set(&options->config->appid, TEST_APPID);
options->config->is_cname = is_cname;
options->ctl = cos_http_controller_create(options->pool, 0);
/* 버킷의 이름 생성 형식은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 해당 형식을 따라야 합니다. */
cos_str_set(&bucket, TEST_BUCKET_NAME);

/* api를 호출해 객체 삭제 */
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
