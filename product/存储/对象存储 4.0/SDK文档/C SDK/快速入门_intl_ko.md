## 개발 준비
### 관련 리소스
COS XML C SDK 리소스 다운로드 주소: [XML C SDK GitHub 다운로드](https://github.com/tencentyun/cos-c-sdk-v5).
예시 데모 다운로드: [XML C SDK 데모](https://github.com/tencentyun/cos-c-sdk-v5/blob/master/cos_c_sdk_test/cos_demo.c).

### 개발 환경
1. CMake 도구(2.6.0 이상 버전 권장)를 설치합니다. [여기](http://www.cmake.org/download/)를 클릭하여 다운로드하십시오. 일반 설치 방법은 다음과 같습니다.
```bash
./configure
make
make install
```
2. libcurl(7.32.0 이상 버전 권장)을 설치합니다. [여기](http://curl.haxx.se/download.html?spm=5176.doc32132.2.7.23MmBq)를 클릭하여 다운로드하십시오. 일반 설치 방법은 다음과 같습니다.
```bash
./configure
make
make install
```
3. apr(1.5.2 이상 버전 권장)을 설치합니다. [여기](https://apr.apache.org/download.cgi?spm=5176.doc32132.2.9.23MmBq&file=download.cgi)를 클릭하여 다운로드하십시오. 일반 설치 방법은 다음과 같습니다.
```bash
./configure
make
make install
```
4. apr-util(1.5.4 이상 버전 권장)을 설치합니다. [여기](https://apr.apache.org/download.cgi?spm=5176.doc32132.2.10.23MmBq&file=download.cgi)를 클릭하여 다운로드하십시오. 설치 시 with-apr 옵션을 지정해야 합니다. 일반 설치 방법은 다음과 같습니다.
```bash
./configure --with-apr=/your/apr/install/path
make
make install
```
5. minixml(2.8 이상 버전 권장)을 설치합니다. [여기](https://www.msweet.org/mxml/)를 클릭하여 다운로드하십시오. 일반 설치 방법은 다음과 같습니다.
```bash
./configure
make
sudo make install
```

### SDK 설치
소스 코드를 설치합니다. [GitHub](https://github.com/tencentyun/cos-c-sdk-v5)에서 소스 코드를 다운로드하십시오. 일반적인 컴파일 명령은 다음과 같습니다.
```bash
cmake .
make
make install
```

## SDK 초기화
### SDK 실행 환경 초기화
```cpp
int main(int argc, char *argv[])
{
    /* 프로그램 입구에서 cos_http_io_initialize 방식을 호출하고, 이 방식 내부에서 네트워크, 메모리 등 부분과 관련 있는 전역 리소스 초기화를 수행할 수 있습니다 */
    if (cos_http_io_initialize(NULL, 0) != COSE_OK) {
        exit(1);
    }

    /* COS SDK의 API를 호출하여 파일 업로드 또는 다운로드 */
    /* ... 사용자 로직 코드, 여기서는 생략 */

    /* 프로그램 종료 전, cos_http_io_deinitialize 방식을 호출하여 이전에 할당된 전역 리소스를 릴리스합니다 */
    cos_http_io_deinitialize();
    return 0;
}
```

### 요청 옵션 초기화
```cpp
    /* apr_pool_t와 효과가 동일하며, 메모리 관리를 위한 메모리 풀이고, 구현 코드는 apr 라이브러리에 있습니다 */
    cos_pool_t *pool;
    cos_request_options_t *options;

    /* 새로운 메모리 풀을 생성하고, 두 번째 매개변수는 NULL이며, 기타 메모리 풀에서 승계되지 않았음을 나타냅니다 */
    cos_pool_create(&pool, NULL);

    /* options을 생성 및 초기화, 이 매개변수 내부에는 주로 endpoint,access_key_id,acces_key_secret, is_cname, curl 매개변수 등 전역 구성 정보가 포함됩니다
     * options의 메모리는 pool에서 할당되고, 이후 pool을 릴리스한 후, options의 메모리도 릴리스된 것과 같으므로, 별도로 메모리를 릴리스할 필요가 없습니다
     */ 
    options = cos_request_options_create(pool);
    options->config = cos_config_create(options->pool);

    /* cos_str_set은 char* 유형의 문자열로 cos_string_t 유형을 초기화합니다*/
    cos_str_set(&options->config->endpoint, "<사용자의 Endpoint>");              //Endpoint는 사용자가 있는 지역의 COS 서비스 도메인 이름에 따라 입력됩니다.
    cos_str_set(&options->config->access_key_id, "<사용자의 SecretId>");         //사용자가 COS 서비스에 등록한 후 얻은 SecretId
    cos_str_set(&options->config->access_key_secret, "<사용자의 SecretKey>");    //사용자가 COS 서비스에 등록한 후 얻은 SecretKey
    cos_str_set(&options->config->appid, "<사용자의 AppId>");                    //사용자가 COS 서비스에 등록한 후 얻은 AppId

    /* sts_token을 설정하여 임시 키를 사용할 수 있으며, 임시 키 사용 시, access_key_id 및 access_key_secret은 모두 임시 키에 할당된 SecretId 및 SecretKey를 설정해야 합니다 */
    //cos_str_set(&options->config->sts_token, "MyTokenString");
    /* CNAME 설정 여부 */
    options->config->is_cname = 0;

    /* 타임아웃 시간과 같은 네트워크 관련 매개변수 설정에 사용합니다*/
    options->ctl = cos_http_controller_create(options->pool, 0);

    /* 업로드 요청이 Content-MD5 헤더를 자동으로 추가할지 여부를 설정하는 데 사용됩니다. enable은 COS_FALSE일 경우 업로드 요청이 자동으로 Content-MD5 헤더를 추가하지 않으며, enable은 COS_TRUE일 경우 업로드 요청이 자동으로 Content-MD5 헤더를 추가합니다. 이 항목을 설정하지 않으면 기본으로 Content-MD5 헤더를 추가합니다 */
    cos_set_content_md5_enable(options->ctl, COS_FALSE);
	
    /* 요청 라우팅 주소 및 포트를 설정하는 데 사용되며, 일반적으로 이 매개변수는 설정할 필요가 없습니다. 도메인 이름 해석 결과에 따라 요청이 라우팅됩니다 */
    //cos_set_request_route(options->ctl, "192.168.12.34", 80);
```

##  SDK 일반 사용 프로세스
1. SDK를 초기화합니다.
2. 요청 옵션 매개변수를 설정합니다.
APPID, SecretId, SecretKey, Bucket 등 이름의 의미 및 획득 방식은 [COS 용어집](https://cloud.tencent.com/document/product/436/7751#.E6.9C.AF.E8.AF.AD.E4.BF.A1.E6.81.AF)을 참조하십시오.
  -  APPID는 Tencent Cloud 계정을 신청한 후, 시스템에서 할당한 계정 ID 중 하나입니다.
  - access_key_id 및 access_key_secret은 계정 API 키입니다.
  - endpoint는 COS 액세스 도메인 이름 정보이며, 상세한 정보는 [가용 영역 및 액세스 도메인 이름](https://cloud.tencent.com/document/product/436/6224) 문서를 참조하십시오. 예를 들어, 광주 지역 endpoint는 `cos.ap-guangzhou.myqcloud.com`입니다.
3. API에 필요한 매개변수를 설정합니다.
4. SDK API를 호출하여 요청을 시작하고 요청 응답의 결과를 가져옵니다.

### 버킷 생성
```cpp
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_acl_e cos_acl = COS_ACL_PRIVATE;
    cos_string_t bucket;
    cos_table_t *resp_headers = NULL;
    
    /* 새로운 메모리 풀을 생성하고, 두 번째 매개변수는 NULL이며, 기타 메모리 풀에서 승계되지 않았음을 나타냅니다 */
    cos_pool_create(&p, NULL);
    
    /* options을 생성 및 초기화, 이 매개변수 내부에는 주로 endpoint,access_key_id,acces_key_secret, is_cname, curl 매개변수 등 전역 구성 정보가 포함됩니다
     * options의 메모리는 pool에서 할당되고, 이후 pool을 릴리스한 후, options의 메모리도 릴리스된 것과 같으므로, 별도로 메모리를 릴리스할 필요가 없습니다
     */
    options = cos_request_options_create(p);
    options->config = cos_config_create(options->pool);
    init_test_config(options->config, is_cname);
    
    /* appid, endpoint, access_key_id, acces_key_secret, is_cname, curl 매개변수 등 구성 정보를 설정합니다 */
    cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
    cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
    cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
    cos_str_set(&options->config->appid, TEST_APPID);
    options->config->is_cname = is_cname;
    options->ctl = cos_http_controller_create(options->pool, 0);
    /* bucket의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다 */
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    /* api를 호출하여 bucket 생성 */
    s = cos_create_bucket(options, &bucket, cos_acl, &resp_headers);
    if (cos_status_is_ok(s)) {
        printf("create bucket succeeded\n");
    } else {
        printf("create bucket failed\n");
    }
    
    //destroy memory pool
    cos_pool_destroy(p); 
```

### 파일 업로드
```cpp
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_string_t object;
    cos_string_t file;
    cos_table_t *resp_headers = NULL;
    
    /* 새로운 메모리 풀을 생성하고, 두 번째 매개변수는 NULL이며, 기타 메모리 풀에서 승계되지 않았음을 나타냅니다 */
    cos_pool_create(&p, NULL);
    
    /* options을 생성 및 초기화, 이 매개변수 내부에는 주로 endpoint,access_key_id,acces_key_secret, is_cname, curl 매개변수 등 전역 구성 정보가 포함됩니다
     * options의 메모리는 pool에서 할당되고, 이후 pool을 릴리스한 후, options의 메모리도 릴리스된 것과 같으므로, 별도로 메모리를 릴리스할 필요가 없습니다
     */
    options = cos_request_options_create(p);
    options->config = cos_config_create(options->pool);
    init_test_config(options->config, is_cname);

    /* appid, endpoint, access_key_id, acces_key_secret, is_cname, curl 매개변수 등 구성 정보를 설정합니다 */
    cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
    cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
    cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
    cos_str_set(&options->config->appid, TEST_APPID);
    options->config->is_cname = is_cname;
    options->ctl = cos_http_controller_create(options->pool, 0);
    /* bucket의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다 */
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    /* api를 호출하여 파일 업로드 */
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

### 파일 다운로드
```cpp
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_string_t object;
    cos_string_t file;
    cos_table_t *resp_headers = NULL;
    
    /* 새로운 메모리 풀을 생성하고, 두 번째 매개변수는 NULL이며, 기타 메모리 풀에서 승계되지 않았음을 나타냅니다 */
    cos_pool_create(&p, NULL);
    
    /* options을 생성 및 초기화, 이 매개변수 내부에는 주로 endpoint,access_key_id,acces_key_secret, is_cname, curl 매개변수 등 전역 구성 정보가 포함됩니다
     * options의 메모리는 pool에서 할당되고, 이후 pool을 릴리스한 후, options의 메모리도 릴리스된 것과 같으므로, 별도로 메모리를 릴리스할 필요가 없습니다
     */
    options = cos_request_options_create(p);
    options->config = cos_config_create(options->pool);
    init_test_config(options->config, is_cname);

    /* appid, endpoint, access_key_id, acces_key_secret, is_cname, curl 매개변수 등 구성 정보를 설정합니다 */
    cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
    cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
    cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
    cos_str_set(&options->config->appid, TEST_APPID);
    options->config->is_cname = is_cname;
    options->ctl = cos_http_controller_create(options->pool, 0);
    /* bucket의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다 */
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    /* api를 호출하여 파일 다운로드 */
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

