
업로드한 객체에 암호화가 필요할 경우, 다음과 같은 암호화 방식을 지원합니다.

#### COS에서 호스팅하는 암호화 키를 사용한 서버 암호화(SSE-COS)로 데이터 보호

Tencent Cloud COS에서 마스터 키를 호스팅하고 데이터를 관리합니다. COS는 데이터센터에 데이터를 쓸 때 자동으로 암호화하며, 해당 데이터 사용 시 자동으로 암호화를 해제합니다. 현재 COS의 마스터 키를 사용한 AES-256 데이터 암호화를 지원합니다.

C SDK는 'x-cos-server-side-encryption' 헤더 설정을 통해 완료합니다.

```cpp
int main(int argc, char *argv[])
{
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_string_t object;
    cos_table_t *resp_headers = NULL;
    cos_table_t *headers = NULL;
    cos_string_t file;
    cos_string_t download_file;
	// 초기화
    if (cos_http_io_initialize(NULL, 0) != COSE_OK) {
       exit(1);
    }
    cos_pool_create(&p, NULL);
    // 초기화 요청 옵션
    options = cos_request_options_create(p);
    options->config = cos_config_create(options->pool);
    cos_str_set(&options->config->endpoint, "cos.ap-guangzhou.myqcloud.com"); // your endpoint
    cos_str_set(&options->config->access_key_id, "SECRETID");	// your SecretId 
    cos_str_set(&options->config->access_key_secret, "SECRETKEY"); // your SecretKey
    cos_str_set(&options->config->appid, "APPID");	//your appid
    options->config->is_cname = is_cname;
    options->ctl = cos_http_controller_create(options->pool, 0);
    cos_str_set(&bucket, "<BucketName-APPID>");	//your bucketname, <BucketName-APPID>

    // 서버 암호화 헤더 설정, SSE-COS
    headers = cos_table_make(p, 1);
    apr_table_add(headers, "x-cos-server-side-encryption", "AES256");

    cos_str_set(&file, "example1.txt");		// your filename
    cos_str_set(&object, "example_object");	// your object name

    // 객체 업로드
    s = cos_put_object_from_file(options, &bucket, &object, &file, headers, &resp_headers);
    if (cos_status_is_ok(s)) {
        printf("put object succeeded\n");
    } else {
        printf("put object failed\n");
    }
    
    // 객체 다운로드
    cos_str_set(&download_file, "example2.txt");
    s = cos_get_object_to_file(options, &bucket, &object, NULL, NULL, &download_file, &resp_headers);
    if (cos_status_is_ok(s)) {
        printf("get object succeeded\n");
    } else {
        printf("get object failed\n");
    }
    
    cos_pool_destroy(p);

    cos_http_io_deinitialize();
    return 0;
}
```

#### 고객이 제공한 암호화 키를 사용한 서버 암호화(SSE-C)로 데이터 보호

사용자가 암호화 키를 제공하며, 객체 업로드 시 COS가 사용자가 제공한 암호화 키를 사용하여 사용자 데이터에 대해 AES-256 암호화를 진행합니다. C SDK는 'x-cos-server-side-encryption-customer-*' 헤더 설정을 통해 완료합니다.

> !
>- 해당 암호화로 실행되는 서비스는 HTTPS를 사용해 요청해야 합니다.
>- customerKey: 사용자가 제공한 키로 32 바이트의 문자열입니다. 숫자, 알파벳, 문자 조합을 지원하지만 중국어는 지원하지 않습니다.
>- 업로드하는 원본 파일에서 해당 방법을 호출하는 경우 GET(다운로드), HEAD(조회) 사용 시, 원본 객체를 작업할 때도 해당 방법을 호출합니다.

```cpp
int main(int argc, char *argv[])
{
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_string_t object;
    cos_table_t *resp_headers = NULL;
    cos_table_t *headers = NULL;
    cos_string_t file;
    cos_string_t download_file;
	// 초기화
    if (cos_http_io_initialize(NULL, 0) != COSE_OK) {
       exit(1);
    }
    cos_pool_create(&p, NULL);
    // 초기화 요청 옵션
    options = cos_request_options_create(p);
    options->config = cos_config_create(options->pool);
    cos_str_set(&options->config->endpoint, "https://cos.ap-guangzhou.myqcloud.com"); // your endpoint, HTTPS를 사용해 요청해야 합니다.
    cos_str_set(&options->config->access_key_id, "SECRETID");	// your SecretId 
    cos_str_set(&options->config->access_key_secret, "SECRETKEY"); // your SecretKey
    cos_str_set(&options->config->appid, "APPID");	//your appid
    options->config->is_cname = is_cname;
    options->ctl = cos_http_controller_create(options->pool, 0);
    cos_str_set(&bucket, "<BucketName-APPID>");	//your bucketname, <BucketName-APPID>

    // 서버 암호화 헤더 설정, SSE-C
    headers = cos_table_make(p, 3);
    apr_table_add(headers, "x-cos-server-side-encryption-customer-algorithm", "AES256");
    apr_table_add(headers, "x-cos-server-side-encryption-customer-key", "MDEyMzQ1Njc4OUFCQ0RFRjAxMjM0NTY3ODlBQkNERUY=");	//사용자 서버 암호화 키의 Base64 인코딩으로 변경합니다.
    apr_table_add(headers, "x-cos-server-side-encryption-customer-key-MD5", "U5L61r7jcwdNvT7frmUG8g==");	//	사용자 서버 암호화 키 MD5 해시값의 Base64 인코딩으로 변경합니다.

    cos_str_set(&file, "example1.txt");		// your filename
    cos_str_set(&object, "example_object");	// your object name

    // 객체 업로드
    s = cos_put_object_from_file(options, &bucket, &object, &file, headers, &resp_headers);
    if (cos_status_is_ok(s)) {
        printf("put object succeeded\n");
    } else {
        printf("put object failed\n");
    }
    
    // 객체 다운로드, 객체 다운로드도 서버 암호화 헤더 제공 필요
    cos_str_set(&download_file, "example2.txt");
    s = cos_get_object_to_file(options, &bucket, &object, headers, NULL, &download_file, &resp_headers);
    if (cos_status_is_ok(s)) {
        printf("get object succeeded\n");
    } else {
        printf("get object failed\n");
    }

    cos_pool_destroy(p);

    cos_http_io_deinitialize();
    return 0;
}
```
