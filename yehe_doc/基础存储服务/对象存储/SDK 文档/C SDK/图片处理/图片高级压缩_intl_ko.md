## 소개

본 문서는 이미지 고급 압축에 대한 API 개요 및 SDK 예시 코드를 제공합니다.


| API           |  작업 설명               |
| :--------------- |  :--------------------- |
| [이미지 고급 압축](https://intl.cloud.tencent.com/document/product/436/40119)|이미지 고급 압축은 이미지를 TPG 또는 HEIF 등 압축 비율이 높은 포맷으로 변환하여 이미지 전송 링크 및 로딩 시 소모되는 시간을 효과적으로 단축하고 대역폭 및 트래픽 비용을 절감합니다. |

#### 방법 모델

객체 다운로드 방법으로 구현하며 사용자는 요청 매개변수를 추가하면 됩니다. 요청 매개변수 포맷은 다음과 같습니다. 객체 다운로드에 대한 자세한 설명은 [객체 다운로드](https://intl.cloud.tencent.com/document/product/436/31518)를 참조하십시오.

```c
imageMogr2/format/<Format>
```
| 매개변수       | 의미                                           |
| :--------- | :--------------------------------------------- |
| format | 압축 포맷으로, 타깃 썸네일 이미지는 TPG 또는 HEIF 형식 |



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
apr_table_addn(params, "imageMogr2/format/tpg", "");
cos_str_set(&object, "test.jpg");
cos_str_set(&file, "test.tpg");
s = cos_get_object_to_file(options, &bucket, &object, NULL, params, &file, &resp_headers);
log_status(s);
if (! cos_status_is_ok(s)) {
    printf("cos_get_object_to_file fail, req_id:%s\n", s->req_id);
}

params = cos_table_make(p, 1);
apr_table_addn(params, "imageMogr2/format/heif", "");
cos_str_set(&file, "test.heif");
s = cos_get_object_to_file(options, &bucket, &object, NULL, params, &file, &resp_headers);
log_status(s);
if (! cos_status_is_ok(s)) {
    printf("cos_get_object_to_file fail, req_id:%s\n", s->req_id);
}
```
