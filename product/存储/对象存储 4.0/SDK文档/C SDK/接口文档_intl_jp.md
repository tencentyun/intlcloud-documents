COSのXML C SDK操作は、各APIに対応する呼び出し結果を返し、呼び出し結果には、応答コード、エラーコード、エラーメッセージなどの結果情報が含まれ、詳細については、ドキュメントの最後の異常説明を参照してください。
> 文章に記載されているSecretId、SecretKey、Bucketなどの名前の意味および取得方式については、[COS用語情報](https://cloud.tencent.com/document/product/436/7751)を参照してください。

SDKにおいて各APIを使用する正しい方法は以下のとおりです：簡潔にするために、後続のAPIの例では、具体的な異常を処理する例を示しておらず、単にAPIの使用例を示しています。

```cpp
    cos_status_t *s = NULL;
    s = cos_put_object_from_file(options, &bucket, &object, &file, &headers, &resp_headers);
    if (!s && !cos_status_is_ok(s)) {
        // 必要に応じて異常シナリオのログ出力および処理を行います
        cos_warn_log("failed to put object from file", buf);
        if (s->error_code) cos_warn_log("status->error_code: %s", s->error_code);
        if (s->error_msg) cos_warn_log("status->error_msg: %s", s->error_msg);
        if (s->req_id) cos_warn_log("status->req_id: %s", s->req_id);
    }
```

## Bucket操作
### Put Bucket
##### 機能説明
Put Bucketリクエストは指定アカウントで1つのバケットを作成できます。
#### 方法のプロトタイプ
```cpp
cos_status_t *cos_create_bucket(const cos_request_options_t *options, 
                                const cos_string_t *bucket, 
                                cos_acl_e cos_acl, 
                                cos_table_t **resp_headers);
```

#### パラメータ説明
| パラメータ名 | パラメータ説明 | タイプ | 
|---------|---------|---------|
| options | COSリクエストオプション | Struct | 
| bucket | Bucketの名前。Bucketの命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません | String  |
| cos_acl | ユーザーカスタマイズ権限を許可します。<br>有効値：COS_ACL_PRIVATE(0)、COS_ACL_PUBLIC_READ(1)、COS_ACL_PUBLIC_READ_WRITE(2)。<br>デフォルト値：COS_ACL_PRIVATE(0)| Enum  |
| resp_headers | HTTP応答メッセージのヘッダーフィールドを返します| Struct | 

#### 戻り結果の説明
| 返された結果 | 説明 | タイプ | 
|---------|---------|---------|
| code | エラーコード  |Int|        
| error_code | エラーコードの内容|String|   
| error_msg |エラーコードの説明 |String|   
| req_id | リクエストメッセージID |String|  

#### 例
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

### Delete Bucket
##### 機能説明
Delete Bucketリクエストは指定されたアカウントでバケットを削除でき、削除する前にバケットをブランクにする必要があります。

#### 方法のプロトタイプ
```cpp
cos_status_t *cos_delete_bucket(const cos_request_options_t *options,
                                const cos_string_t *bucket, 
                                cos_table_t **resp_headers);
```

#### パラメータ説明
| パラメータ名 | パラメータ説明 | タイプ | 
|---------|---------|---------|
| options | COSリクエストオプション |Struct|  
| bucket | Bucketの名前。Bucketの命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません|String|  
| resp_headers | HTTP応答メッセージのヘッダーフィールドを返します|Struct| 

#### 戻り結果の説明
| 返された結果 | 説明 | タイプ | 
|---------|---------|---------|
| code | エラーコード|Int|          
| error_code |エラーコードの内容 |String|   
| error_msg | エラーコードの説明|String|   
| req_id | リクエストメッセージID|String| 

#### 例
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
##### 機能説明
Get BucketリクエストはList Objectリクエストに等しく、当該Bucekt下の一部あるいはすべてのObjectをリストすることができます。当該リクエストを出すには、Read権限が必要です。

#### 方法のプロトタイプ
```cpp
cos_status_t *cos_list_object(const cos_request_options_t *options,
                              const cos_string_t *bucket, 
                              cos_list_object_params_t *params, 
                              cos_table_t **resp_headers);
```

#### パラメータ説明
| パラメータ名 | パラメータ説明 | タイプ | 
|---------|---------|---------|
| options | COSリクエストオプション |Struct|  
| bucket | Bucketの名前。Bucketの命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません |String|  
| params | Get Bucket操作パラメータ。|Struct|  
| encoding_type  | 戻り値のエンコーディング方式を規定します|String|  
| prefix | プレフィックスのマッチング。返されたファイルのプレフィックスアドレスの設定に使用されます|String|
| marker | デフォルトではUTF-8の二進法の順でエントリを一覧表示します。すべての一覧表示されたエントリはmarkerから開始します|String|  
| delimiter | Get Bucket操作パラメータ|String|  
| max_ret |一度に返されたエントリの最大数、デフォルト：1000 |Struct|  
| truncated | 返されたエントリが遮断されたかどうか、'true'または'false'|Boolean|  
| next_marker | 返されたエントリが遮断された場合、返されたNextMarkerは次のエントリの開始点です|String|  
| object_list | Get Bucket操作によって返されたオブジェクト情報リスト |Struct|  
| key | Get Bucket操作によって返されたObjectの名前|Struct|  
| last_modified | Get Bucket操作によって返されたObjectの最終変更時間|Struct|  
| etag | Get Bucket操作によって返されたオブジェクトのSHA-1アルゴリズムチェック値|Struct|  
| size | Get Bucket操作によって返されたオブジェクトのサイズ、単位：Byte|Struct|  
| owner_id | Get Bucket操作によって返されたオブジェクト所有者のUID情報|Struct| 
| storage_class | Get Bucket操作によって返されたオブジェクトストレージレベル|Struct|  
| common_prefix_list | Prefixとdelimiterとの間の同じパスを1つのタイプに分類され、Common Prefixとして定義します|Struct|  
| resp_headers | HTTP応答メッセージのヘッダーフィールドを返します|Struct|  

#### 戻り結果の説明
| 返された結果 | 説明 | タイプ | 
|---------|---------|---------|
| code | エラーコード|Int|          
| error_code | エラーコードの内容|String|   
| error_msg |エラーコードの説明 |String|   
| req_id |リクエストメッセージID |String|  

#### 例
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

    //get bucket（list object）
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
##### 機能説明
Put Bucket ACL APIは、バケットのACLテーブルを書き込むために使用されます。ヘッダー：「x-cos-acl」、「x-cos-grant-read」、「x-cos-grant-full-control」を介してACL情報を渡すことができます。

#### 方法のプロトタイプ
```cpp
cos_status_t *cos_put_bucket_acl(const cos_request_options_t *options, 
                                 const cos_string_t *bucket, 
                                 cos_acl_e cos_acl,
                                 const cos_string_t *grant_read,
                                 const cos_string_t *grant_write,
                                 const cos_string_t *grant_full_ctrl,
                                 cos_table_t **resp_headers);
```

#### パラメータ説明
| パラメータ名 | パラメータ説明 | タイプ | 
|---------|---------|---------|
| options | COSリクエストオプション |Struct|  
| bucket | Bucketの名前。Bucketの命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません|String|  
| cos_acl | ユーザーカスタマイズ権限を許可します。<br>有効値：COS_ACL_PRIVATE(0)、COS_ACL_PUBLIC_READ(1)、COS_ACL_PUBLIC_READ_WRITE(2)。<br>デフォルト値：COS_ACL_PRIVATE(0)|Enum|   
| grant_read | 読み取り権限付与者|String|  
| grant_write | 書き込み権限付与者|String|  
| grant_full_ctrl | 読み書き権限付与者|String|  
| resp_headers | HTTP応答メッセージのヘッダーフィールドを返します|Struct| 

#### 戻り結果の説明
| 返された結果 | 説明 | タイプ | 
|---------|---------|---------|
| code | エラーコード|Int|         
| error_code | エラーコードの内容|String|   
| error_msg | エラーコードの説明|String|   
| req_id | リクエストメッセージID|String|  

#### 例
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
##### 機能説明
Get Bucket ACL APIでBucketのACL、即ちバケット（Bucket）のアクセス権限管理リストを取得できます。当該APIに対してBucket所有者にのみ操作権限があります。

#### 方法のプロトタイプ
```cpp
cos_status_t *cos_get_bucket_acl(const cos_request_options_t *options, 
                                 const cos_string_t *bucket, 
                                 cos_acl_params_t *acl_param, 
                                 cos_table_t **resp_headers)
```

#### パラメータ説明
| パラメータ名 | パラメータ説明 | タイプ | 
|---------|---------|---------|
| options | COSリクエストオプション|Struct|  
| bucket | Bucketの名前。Bucketの命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません |String|  
| acl_param | Get Bucket ACL操作パラメータ|Struct|  
| owner_id | Get Bucket ACL操作によって返されたBucket所有者のID|String|   
| owner_name | Get Bucket ACL操作によって返されたBucket所有者の名前 |String|  
| object_list | Get Bucket ACL操作によって返された権限付与対象者の情報および権限情報|Struct|  
| type | Get Bucket ACL操作によって返された権限付与対象者のアカウントタイプ |String|  
| id | Get Bucket ACL操作によって返された権限付与対象者のユーザーID |String|  
| name | Get Bucket ACL操作によって返された権限付与対象者のユーザーの名前 |String|  
| permission | Get Bucket ACL操作によって返された権限付与対象者の権限情報|String|  
| resp_headers | HTTP応答メッセージのヘッダーフィールドを返します|Struct|  



#### 戻り結果の説明
| 返された結果 | 説明 | タイプ | 
|---------|---------|---------|
| code | エラーコード|Int|          
| error_code | エラーコードの内容|String|   
| error_msg | エラーコードの説明|String|   
| req_id | リクエストメッセージID|String|   

#### 例
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
##### 機能説明
Put Bucket Lifecycle APIはBucketのライフサイクル規則を書き込むために使用されます。

#### 方法のプロトタイプ
```cpp
cos_status_t *cos_put_bucket_lifecycle(const cos_request_options_t *options,
                                       const cos_string_t *bucket, 
                                       cos_list_t *lifecycle_rule_list, 
                                       cos_table_t **resp_headers);
```

#### パラメータ説明
| パラメータ名 | パラメータ説明 | タイプ | 
|---------|---------|---------|
| options | COSリクエストオプション|Struct|  
| bucket | Bucketの名前。Bucketの命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません |String|  
| lifecycle_rule_list | Put Bucket Lifecycle操作パラメータ |Struct|  
| id  |  ライフサイクル規則ID |String|  
| prefix |規則に適用されるプレフィックスを指定します |String|  
| status | 規則が有効になっているかどうかを示します。列挙値：Enabled、Disabled |String|  
| expire | 規則期限切れ属性 |Struct|  
| days |削除操作または変換操作が何日後に実行されるかを指定します。マルチパートアップロードを開始した後に何日以内にアップロードを完了する必要があるかを指定します |Int|  
| date | 削除操作または変換操作がいつ実行されるかを指定します |String|  
| transition | 規則変換属性。オブジェクトがいつStandard_IAに変換されるか |Struct|  
| storage_class | Objectのダンプ先である目標ストレージタイプを指定します。列挙値：Standard_IA |String|  
| abort | マルチパートアップロードの実行を維持する最大時間を設定します |Struct|  
| resp_headers | HTTP応答メッセージのヘッダーフィールドを返します |Struct|

#### 戻り結果の説明
| 返された結果 | 説明 | タイプ | 
|---------|---------|---------|
| code | エラーコード |Int|          
| error_code | エラーコードの内容 |String|   
| error_msg | エラーコードの説明 |String|   
| req_id | リクエストメッセージID |String|

#### 例
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
##### 機能説明
Get Bucket Lifecycle APIはBucketのライフサイクル規則を取得するために使用されます。

#### 方法のプロトタイプ
```cpp
cos_status_t *cos_get_bucket_lifecycle(const cos_request_options_t *options,
                                       const cos_string_t *bucket, 
                                       cos_list_t *lifecycle_rule_list, 
                                       cos_table_t **resp_headers);
```

#### パラメータ説明
| パラメータ名 | パラメータ説明 | タイプ | 
|---------|---------|---------|
| options | COSリクエストオプション|Struct|  
| bucket | Bucketの名前。Bucketの命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません |String|  
| lifecycle_rule_list | Get Bucket Lifecycle操作パラメータ|Struct|  
| id  |  ライフサイクル規則ID |String|  
| prefix | 規則に適用されるプレフィックス |String|  
| status | 規則が有効になっているかどうか。列挙値：Enabled、Disabled |String|  
| expire | 規則期限切れ属性 |Struct|  
| days |削除操作が何日後に実行されるかを指定します |Int|  
| date | 削除操作がいつ実行されるかを指定します |String|  
| transition | 規則変換属性。オブジェクトがいつStandard_IAに変換されるか |Struct|  
| days | 変換操作が何日後に実行されるかを指定します |Int|  
| date | 変換操作がいつ実行されるかを指定します |String|  
| storage_class | Objectのダンプ先である目標ストレージタイプを指定します。列挙値：Standard_IA |String|  
| abort | マルチパートアップロードの実行を維持する最大時間を設定します |Struct|  
| days | マルチパートアップロードを開始した後に何日以内にアップロードを完了する必要があるかを指定します |Int|  
| resp_headers |HTTP応答メッセージのヘッダーフィールドを返します |Struct| 

#### 戻り結果の説明
| 返された結果 | 説明 | タイプ | 
|---------|---------|---------|
| code | エラーコード |Int|         
| error_code | エラーコードの内容 |String|   
| error_msg |エラーコードの説明 |String|   
| req_id | リクエストメッセージID|String|   

#### 例
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
##### 機能説明
Delete Bucket Lifecycle APIはBucketのライフサイクル規則を削除するために使用されます。

#### 方法のプロトタイプ
```cpp
cos_status_t *cos_delete_bucket_lifecycle(const cos_request_options_t *options,
                                          const cos_string_t *bucket, 
                                          cos_table_t **resp_headers);
```

#### パラメータ説明
| パラメータ名 | パラメータ説明 | タイプ | 
|---------|---------|---------|
| options | COSリクエストオプション |Struct|  
| bucket | Bucketの名前。Bucketの命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません |String|  
| resp_headers | HTTP応答メッセージのヘッダーを返します |Struct| 

#### 戻り結果の説明
| 返された結果 | 説明 | タイプ | 
|---------|---------|---------|
| code | エラーコード  |Int|        
| error_code | エラーコードの内容 |String|   
| error_msg |エラーコードの説明 |String|   
| req_id | リクエストメッセージID |String| 

#### 例
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
##### 機能説明
Put Bucket CORS APIはBucketのCORS権限の設定をリクエストするために使用されます。

#### 方法のプロトタイプ
```cpp
cos_status_t *cos_put_bucket_cors(const cos_request_options_t *options,
                                  const cos_string_t *bucket, 
                                  cos_list_t *cors_rule_list, 
                                  cos_table_t **resp_headers);
```

#### パラメータ説明
| パラメータ名 | パラメータ説明 | タイプ | 
|---------|---------|---------|
| options | COSリクエストオプション|Struct|  
| bucket | Bucketの名前。Bucketの命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません |String|  
| cors_rule_list | Put Bucket CORS操作パラメータ |Struct|  
| id  | 構成規則ID |String|  
| allowed_origin | 許可されるアクセスソース。ワイルドカード`*`をサポートします |String|  
| allowed_method |許可されるHTTP操作。列挙値：GET、PUT、HEAD、POST、DELETE |String|  
| allowed_header | OPTIONSリクエストを送信するときにサーバーに対し、次のリクエストがどのようなカスタマイズしたHTTPリクエストヘッダーを使用できるかを通知します。ワイルドカード`*`をサポートします |String|  
|expose_header | ブラウザの受信可能で、サーバーからのカスタムヘッダー情報を設定します |String|  
| max_age_seconds |OPTIONSリクエストの結果を取得する有効期間を設定します |Int|  
| resp_headers | HTTP応答メッセージのヘッダーフィールドを返します |Struct|  


#### 戻り結果の説明
| 返された結果 | 説明 | タイプ | 
|---------|---------|---------|
| code | エラーコード  |Int|        
| error_code | エラーコードの内容 |String|   
| error_msg |エラーコードの説明 |String|   
| req_id | リクエストメッセージID |String| 

#### 例
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
##### 機能説明
Get Bucket CORS APIはBucketのCORS権限構成の取得をリクエストするために使用されます。
#### 方法のプロトタイプ
```cpp
cos_status_t *cos_get_bucket_cors(const cos_request_options_t *options,
                                  const cos_string_t *bucket, 
                                  cos_list_t *cors_rule_list, 
                                  cos_table_t **resp_headers);
```

#### パラメータ説明
| パラメータ名 | パラメータ説明 | タイプ | 
|---------|---------|---------|
| options | COSリクエストオプション |Struct|  
| bucket | Bucketの名前。Bucketの命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません |String|  
| cors_rule_list | Get Bucket CORS操作パラメータ |Struct| 
| id  | 構成規則ID|String|  
| allowed_origin | 許可されるアクセスソース。ワイルドカード`*`をサポートします |String| 
| allowed_method | 許可されるHTTP操作。列挙値：GET、PUT、HEAD、POST、DELETE |String|  
| allowed_header | OPTIONSリクエストを送信するときにサーバーに対し、次のリクエストがどのようなカスタマイズしたHTTPリクエストヘッダーを使用できるかを通知します。ワイルドカード`*`をサポートします |String|  
|expose_header | ブラウザの受信可能で、サーバーからのカスタムヘッダー情報を設定します |String|  
| max_age_seconds | OPTIONSリクエストの結果を取得する有効期間を設定します |Int|  
| resp_headers | HTTP応答メッセージのヘッダーフィールドを返します |Struct| 

#### 戻り結果の説明
| 返された結果 | 説明 | タイプ | 
|---------|---------|---------|
| code | エラーコード  |Int|        
| error_code | エラーコードの内容 |String|   
| error_msg |エラーコードの説明 |String|   
| req_id | リクエストメッセージID |String| 

#### 例
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
##### 機能説明
Delete Bucket CORS APIはBucketのCORS権限構成を削除するために使用されます。

#### 方法のプロトタイプ
```cpp
cos_status_t *cos_delete_bucket_cors(const cos_request_options_t *options,
                                     const cos_string_t *bucket, 
                                     cos_table_t **resp_headers);
```

#### パラメータ説明
| パラメータ名 | パラメータ説明 | タイプ | 
|---------|---------|---------|
| options | COSリクエストオプション|Struct|  
| bucket | Bucketの名前。Bucketの命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません |String|  
| resp_headers |HTTP応答メッセージのヘッダーフィールドを返します |Struct| 

#### 戻り結果の説明
| 返された結果 | 説明 | タイプ | 
|---------|---------|---------|
| code | エラーコード  |Int|        
| error_code | エラーコードの内容 |String|   
| error_msg |エラーコードの説明 |String|   
| req_id | リクエストメッセージID |String| 

#### 例
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
##### 機能説明
Put Bucket Versioning APIは、バケットを有効または無効にするバージョンコントロール機能を実現します。

#### 方法のプロトタイプ
```cpp
cos_status_t *cos_put_bucket_versioning(const cos_request_options_t *options,
                                        const cos_string_t *bucket, 
                                        cos_versioning_content_t *versioning, 
                                        cos_table_t **resp_headers);
```

#### パラメータ説明
| パラメータ名 | パラメータ説明 | タイプ | 
|---------|---------|---------|
| options | COSリクエストオプション |Struct|  
| bucket | Bucketの名前。Bucketの命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません |String|  
| versioning | Put Bucket Versioning操作パラメータ |Struct|  
| status  | バージョンが有効になっているかどうか、列挙値：Suspended、Enabled |String|  
| resp_headers | HTTP応答メッセージのヘッダーフィールドを返します |Struct|  

#### 戻り結果の説明
| 返された結果 | 説明 | タイプ | 
|---------|---------|---------|
| code | エラーコード  |Int|        
| error_code | エラーコードの内容|String|   
| error_msg |エラーコードの説明 |String|   
| req_id | リクエストメッセージID |String| 

#### 例
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
##### 機能説明
Get Bucket Versioning APIは、バケットのバージョンコントロール情報の取得を実現します。

#### 方法のプロトタイプ
```cpp
cos_status_t *cos_get_bucket_versioning(const cos_request_options_t *options,
                                        const cos_string_t *bucket, 
                                        cos_versioning_content_t *versioning, 
                                        cos_table_t **resp_headers);
```

#### パラメータ説明
| パラメータ名 | パラメータ説明 | タイプ | 
|---------|---------|---------|
| options | COSリクエストオプション |Struct|  
| bucket | Bucketの名前。Bucketの命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません |String|  
| versioning | Get Bucket Versioning操作パラメータ |Struct|  
| status  | バージョンが有効になっているかどうか、列挙値：Suspended、Enabled |String|  
| resp_headers | HTTP応答メッセージのヘッダーフィールドを返します |Struct|  

#### 戻り結果の説明
| 返された結果 | 説明 | タイプ | 
|---------|---------|---------|
| code | エラーコード  |Int|        
| error_code | エラーコードの内容 |String|   
| error_msg |エラーコードの説明 |String|   
| req_id | リクエストメッセージID |String| 

#### 例
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
##### 機能説明
Put Bucket Replicationリクエストは、バージョン管理を有効化したバケットにreplication構成を追加するために使用されます。バケットにreplication構成が既存の場合、このリクエストは既存の構成を置き換えます。

#### 方法のプロトタイプ
```cpp
cos_status_t *cos_put_bucket_replication(const cos_request_options_t *options,
                                         const cos_string_t *bucket, 
                                         cos_replication_params_t *replication_param, 
                                         cos_table_t **resp_headers);
```

#### パラメータ説明
| パラメータ名 | パラメータ説明 | タイプ | 
|---------|---------|---------|
| options | COSリクエストオプション。 |Struct|  
| bucket | Bucketの名前。Bucketの命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません |String|  
| replication_param | Put Bucket Replication操作パラメータ |Struct|  
| role | オペレータのアカウント情報|String|  
| rule_list | replication構成情報|Struct|  
| id | 具体的なRule名を示すために使用されます|String|  
| status | 規則が有効になっているかどうかを示します。列挙値：Enabled、Disabled|String|  
| prefix | プレフィックスのマッチング。重複することはできません。重複の場合はエラーを返します|String|  
| dst_bucket | 目的バケット識別子。フォーマット：リソース識別子qcs:id/0:cos:[Region]:appid/[APPID]:[Bucketname]|String|  
| storage_class | ストレージタイプ、列挙値：Standard、Standard_IA。<br>デフォルト値：元のバケットレベル|String|  
| resp_headers | HTTP応答メッセージのヘッダーフィールドを返します。|Struct|  

#### 戻り結果の説明
| 返された結果 | 説明 | タイプ | 
|---------|---------|---------|
| code | エラーコード  |Int|        
| error_code | エラーコードの内容|String|   
| error_msg |エラーコードの説明 |String|   
| req_id | リクエストメッセージID |String| 

#### 例
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

##### 機能説明
Get Bucket Replication APIはバケット中のユーザーによるクロスリージョンレプリケーション構成情報の読み取りを実現するようにリクエストします。

#### 方法のプロトタイプ
```cpp
cos_status_t *cos_get_bucket_replication(const cos_request_options_t *options,
                                         const cos_string_t *bucket, 
                                         cos_replication_params_t *replication_param, 
                                         cos_table_t **resp_headers);
```

#### パラメータ説明
| パラメータ名 | パラメータ説明 | タイプ | 
|---------|---------|---------|
| options | COSリクエストオプション |Struct|  
| bucket | Bucketの名前。Bucketの命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません|String|  
| replication_param | Get Bucket Replication操作パラメータ |Struct|  
| role | オペレータのアカウント情報|String|  
| rule_list | replication構成情報|Struct|  
| id | 具体的なRule名を示すために使用されます|String|  
| status | 規則が有効になっているかどうかを示します。列挙値：Enabled、Disabled|String|  
| prefix | プレフィックスのマッチング。重複することはできません。重複の場合はエラーを返します|String|  
| dst_bucket | 目的バケット識別子。フォーマット：リソース識別子qcs:id/0:cos:[Region]:appid/[APPID]:[Bucketname]|String|  
| storage_class | ストレージタイプ、列挙値：Standard、Standard_IA。<br>デフォルト値：元のバケットレベル|String|  
| resp_headers | HTTP応答メッセージのヘッダーフィールドを返します|Struct|  

#### 戻り結果の説明
| 返された結果 | 説明 | タイプ | 
|---------|---------|---------|
| code | エラーコード  |Int|        
| error_code | エラーコードの内容|String|   
| error_msg |エラーコードの説明 |String|   
| req_id | リクエストメッセージID |String| 

#### 例
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
##### 機能説明
Delete Bucket Replication APIは、Bucketのクロスリージョンレプリケーション構成を削除するために使用されます。

#### 方法のプロトタイプ
```cpp
cos_status_t *cos_delete_bucket_replication(const cos_request_options_t *options,
                                            const cos_string_t *bucket, 
                                            cos_table_t **resp_headers);
```

#### パラメータ説明
| パラメータ名 | パラメータ説明 | タイプ | 
|---------|---------|---------|
| options | COSリクエストオプション |Struct|  
| bucket | Bucketの名前。Bucketの命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません |String|  
| resp_headers | HTTP応答メッセージのヘッダーフィールドを返します |Struct|  

#### 戻り結果の説明
| 返された結果 | 説明 | タイプ | 
|---------|---------|---------|
| code | エラーコード  |Int|        
| error_code | エラーコードの内容 |String|   
| error_msg |エラーコードの説明 |String|   
| req_id | リクエストメッセージID |String|

#### 例
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

## Object操作
###  Get Object
##### 機能説明
Get Objectリクエストによりファイル（オブジェクト）をローカルにダウンロードできます。当該操作については、目標Objectにリード権限があり、あるいは目標Objectが全員にリード権限を開放する必要があります（パブリック読み取り）。

#### 方法のプロトタイプ
```cpp
cos_status_t *cos_get_object_to_file(const cos_request_options_t *options,
                                     const cos_string_t *bucket, 
                                     const cos_string_t *object,
                                     cos_table_t *headers, 
                                     cos_table_t *params,
                                     cos_string_t *filename, 
                                     cos_table_t **resp_headers);
```

#### パラメータ説明
| パラメータ名 | パラメータ説明 | タイプ | 
|---------|---------|---------|
| options | COSリクエストオプション|Struct|  
| bucket | Bucketの名前。Bucketの命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません |String|  
| object | Object名 |String|  
| headers | COSリクエストの追加ヘッダーフィールド|Struct|  
| params | COSリクエストの操作パラメータ|Struct|  
| filename | Objectがローカルに保存されたファイル名|String|  
| resp_headers | HTTP応答メッセージのヘッダーフィールドを返します|Struct|  

#### 戻り結果の説明
| 返された結果 | 説明 | タイプ | 
|---------|---------|---------|
| code | エラーコード  |Int|        
| error_code | エラーコードの内容|String|   
| error_msg |エラーコードの説明 |String|   
| req_id | リクエストメッセージID |String| 

#### 例
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
##### 機能説明
Head Objectリクエストは、対応するオブジェクトのメタデータを取り戻すことができ、Headの権限はGetの権限と一致します。

#### 方法のプロトタイプ
```cpp
cos_status_t *cos_head_object(const cos_request_options_t *options, 
                              const cos_string_t *bucket, 
                              const cos_string_t *object,
                              cos_table_t *headers, 
                              cos_table_t **resp_headers);
```

#### パラメータ説明
| パラメータ名 | パラメータ説明 | タイプ | 
|---------|---------|---------|
| options | COSリクエストオプション |Struct|  
| bucket | Bucketの名前。Bucketの命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません|String|  
| object | Object名|String|  
| headers | COSリクエストの追加ヘッダーフィールド|Struct|  
| resp_headers | HTTP応答メッセージのヘッダーフィールドを返します|Struct|  

#### 戻り結果の説明
| 返された結果 | 説明 | タイプ | 
|---------|---------|---------|
| code | エラーコード  |Int|        
| error_code | エラーコードの内容|String|   
| error_msg |エラーコードの説明 |String|   
| req_id | リクエストメッセージID |String| 

#### 例
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
##### 機能説明
Put Objectリクエストは1つのファイル（Object）を指定のBucketにアップロードできます。
> 注意：
> 現在のアクセスポリシーエントリは1000条に制限されています。オブジェクトACL制御が不要な場合は、アップロード時に設定しないでください。デフォルトはバケット権限が継承されます。

#### 方法のプロトタイプ
```cpp
cos_status_t *cos_put_object_from_file(const cos_request_options_t *options,
                                       const cos_string_t *bucket, 
                                       const cos_string_t *object, 
                                       const cos_string_t *filename,
                                       cos_table_t *headers, 
                                       cos_table_t **resp_headers);
```

#### パラメータ説明
| パラメータ名 | パラメータ説明 | タイプ | 
|---------|---------|---------|
| options | COSリクエストオプション|Struct|  
| bucket | Bucketの名前。Bucketの命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません |String|  
| object | Object名 |String|  
| filename | Objectがローカルに保存されたファイル名|String|  
| headers | COSリクエストの追加ヘッダーフィールド|Struct|  
| resp_headers | HTTP応答メッセージのヘッダーフィールドを返します|Struct| 

#### 戻り結果の説明
| 返された結果 | 説明 | タイプ | 
|---------|---------|---------|
| code | エラーコード  |Int|        
| error_code | エラーコードの内容|String|   
| error_msg |エラーコードの説明 |String|   
| req_id | リクエストメッセージID |String| 

#### 例
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
##### 機能説明
Delete Objectリクエストは1つのファイル（オブジェクト）を削除できます。

#### 方法のプロトタイプ
```cpp
cos_status_t *cos_delete_object(const cos_request_options_t *options,
                                const cos_string_t *bucket, 
                                const cos_string_t *object, 
                                cos_table_t **resp_headers);
```

#### パラメータ説明
| パラメータ名 | パラメータ説明 | タイプ | 
|---------|---------|---------|
| options | COSリクエストオプション|Struct|  
| bucket | Bucketの名前。Bucketの命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません |String|  
| object | Object名 |String|  
| resp_headers | HTTP応答メッセージのヘッダーフィールドを返します|Struct| 

#### 戻り結果の説明
| 返された結果 | 説明 | タイプ | 
|---------|---------|---------|
| code | エラーコード  |Int|        
| error_code | エラーコードの内容|String|   
| error_msg |エラーコードの説明 |String|   
| req_id | リクエストメッセージID |String| 

#### 例
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
##### 機能説明
Delete Multiple Objectリクエストは、ファイルの一括削除を実現し、単回リクエストで最大1000個のファイルの一括削除をサポートします。戻り結果に対して、COSはVerboseとQuietという2つのモードを提供します：Verboseモードは各オブジェクトの削除結果を返します；Quietモードはエラーのオブジェクト情報のみを返します。

#### 方法のプロトタイプ
```cpp
cos_status_t *cos_delete_objects(const cos_request_options_t *options,
                                 const cos_string_t *bucket, 
                                 cos_list_t *object_list, 
                                 int is_quiet,
                                 cos_table_t **resp_headers, 
                                 cos_list_t *deleted_object_list);
```

#### パラメータ説明
| パラメータ名 | パラメータ説明 | タイプ | 
|---------|---------|---------|
| options | COSリクエストオプション|Struct|  
| bucket | Bucketの名前。Bucketの命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません|String| 
| object_list | 削除待ちのObjectリスト|Struct| 
  | key |削除待ちのObject名 |String|  
| is_quiet | Quietモードを起動するかどうかを決定します。<br>True(1)：Quietモードを起動し、False(0)：Verboseモードを起動し、デフォルトではFalse(0)です|Boolean|  
| resp_headers | HTTP応答メッセージのヘッダーフィールドを返します|Struct|  
| deleted_object_list | Object削除情報リスト|Struct|  

#### 戻り結果の説明
| 返された結果 | 説明 | タイプ | 
|---------|---------|---------|
| code | エラーコード  |Int|        
| error_code | エラーコードの内容|String|   
| error_msg |エラーコードの説明 |String|   
| req_id | リクエストメッセージID |String|

#### 例
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
##### 機能説明
Put Object ACL APIは、Bucket中のあるObjectのACL構成を書き込むために使用されます。Header：「x-cos-acl」、「x-cos-grant-read」、「x-cos-grant-full-control」を介してACL情報を渡すことができます。

現在のアクセスポリシーエントリは1000件までとします。オブジェクトACLのコントロールが必要とされない場合、設定しないでください。デフォルトでBucket権限が継承されます。

#### 方法のプロトタイプ
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

#### パラメータ説明
| パラメータ名 | パラメータ説明 | タイプ | 
|---------|---------|---------|
| options | COSリクエストオプション|Struct|  
| bucket | Bucketの名前。Bucketの命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません|String|  
| object | Object名。|String|  
| cos_acl | ユーザーカスタマイズ権限を許可します。有効値：COS_ACL_PRIVATE(0)、COS_ACL_PUBLIC_READ(1)、COS_ACL_PUBLIC_READ_WRITE(2)。デフォルト値：COS_ACL_PRIVATE(0)|Enum|   
| grant_read |読み取り権限付与者 |String|  
| grant_write | 書き込み権限付与者|String|  
| grant_full_ctrl | 読み書き権限付与者|String|  
| resp_headers | HTTP応答メッセージのヘッダーフィールドを返します|Struct|  

#### 戻り結果の説明
| 返された結果 | 説明 | タイプ | 
|---------|---------|---------|
| code | エラーコード  |Int|        
| error_code | エラーコードの内容|String|   
| error_msg |エラーコードの説明 |String|   
| req_id | リクエストメッセージID |String| 

#### 例
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
##### 機能説明
Get Object ACL APIは、Bucket中のあるObjectのアクセス権限を取得するために使用されます。このAPIに対してBucketの所有者のみはその操作権限を持っています。

#### 方法のプロトタイプ
```cpp
cos_status_t *cos_get_object_acl(const cos_request_options_t *options, 
                                 const cos_string_t *bucket,
                                 const cos_string_t *object,
                                 cos_acl_params_t *acl_param, 
                                 cos_table_t **resp_headers)
```

#### パラメータ説明
| パラメータ名 | パラメータ説明 | タイプ | 
|---------|---------|---------|
| options | COSリクエストオプション |Struct|  
| bucket | Bucketの名前。Bucketの命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません|String|  
| object | Object名|String|  
| acl_param | Get Object ACL操作パラメータ|Struct|  
| owner_id  | Get Object ACL操作によって返されたBucket所有者のID|String|  
| owner_name | Get Object ACL操作によって返されたBucket所有者の名前|String|  
| object_list | Get Object ACL操作によって返された権限付与対象者の情報および権限情報|Struct|  
| type | Get Object ACL操作によって返された権限付与対象者のアカウントタイプ|String|  
| id | Get Object ACL 操作によって返された権限付与対象者のユーザーID |String|  
| name | Get Object ACL操作によって返された権限付与対象者のユーザーの名前|String|  
| permission | Get Object ACL操作によって返された権限付与対象者の権限情報|String|  
| resp_headers | HTTP応答メッセージのヘッダーフィールドを返します|Struct|  

#### 戻り結果の説明
| 返された結果 | 説明 | タイプ | 
|---------|---------|---------|
| code | エラーコード  |Int|        
| error_code | エラーコードの内容|String|   
| error_msg |エラーコードの説明 |String|   
| req_id | リクエストメッセージID |String| 

#### 例
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
##### 機能説明
Put Object Copyリクエストは、1つのファイルをソースパスからターゲットパスにコピーすることを実現します。

#### 方法のプロトタイプ
```cpp
cos_status_t *cos_copy_object(const cos_request_options_t *options,
                              const cos_string_t *copy_source, 
                              const cos_string_t *dest_bucket, 
                              const cos_string_t *dest_object,
                              cos_table_t *headers,
                              cos_copy_object_params_t *copy_object_param,
                              cos_table_t **resp_headers);
```

#### パラメータ説明
| パラメータ名 | パラメータ説明 | タイプ | 
|---------|---------|---------|
| options | COSリクエストオプション|Struct|  
| copy_source | ソースファイルパス|String|  
| dest_bucket | 目的Bucketの名前。Bucketの命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません |String|  
| dest_object | 目的Object名|String|  
| headers | COSリクエストの追加ヘッダーフィールド|Struct|  
| copy_object_param | Put Object Copy操作パラメータ|Struct|   
| etag | ファイルのMD5アルゴリズムチェック値を返します|String|  
| last_modify |ファイルの最終変更時間が返され、GMTフォーマットです|String|  
| resp_headers | HTTP応答メッセージのヘッダーフィールドを返します|Struct| 

#### 戻り結果の説明
| 返された結果 | 説明 | タイプ | 
|---------|---------|---------|
| code | エラーコード  |Int|        
| error_code | エラーコードの内容|String|   
| error_msg |エラーコードの説明 |String|   
| req_id | リクエストメッセージID |String| 

#### 例
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

## マルチパートアップロード操作
###  Initiate Multipart Upload
##### 機能説明
Initiate Multipart Uploadリクエストは、マルチパートアップロードの初期化を実現します。このリクエストを実行した後にUpload IDを返します。今後のUpload Partリクエストに使用されます。

#### 方法のプロトタイプ
```cpp
cos_status_t *cos_init_multipart_upload(const cos_request_options_t *options, 
                                        const cos_string_t *bucket, 
                                        const cos_string_t *object, 
                                        cos_string_t *upload_id, 
                                        cos_table_t *headers,
                                        cos_table_t **resp_headers);
```

#### パラメータ説明
| パラメータ名 | パラメータ説明 | タイプ | 
|---------|---------|---------|
| options | COSリクエストオプション|Struct|  
| bucket | Bucketの名前。Bucketの命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません|String|  
| object | Object名|String|  
| upload_id | 操作によって返されたUpload ID|String|  
| headers | COSリクエストの追加ヘッダーフィールド|Struct|  
| resp_headers |HTTP応答メッセージのヘッダーフィールドを返します |Struct| 

#### 戻り結果の説明
| 返された結果 | 説明 | タイプ | 
|---------|---------|---------|
| code | エラーコード  |Int|        
| error_code | エラーコードの内容|String|   
| error_msg |エラーコードの説明 |String|   
| req_id | リクエストメッセージID |String| 

#### 例
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
##### 機能説明
Upload Partリクエストは、初期化後のマルチパートアップロードを実行し、サポートされるパート数は1から10000までであり、パートのサイズは1MBから5GBまでです。Upload Partをリクエストするたびに、partNumberとuploadIDを運ぶ必要があり、partNumberはパートの番号であり、アウトオブオーダアップロードをサポートします。

#### 方法のプロトタイプ
```cpp
cos_status_t *cos_upload_part_from_file(const cos_request_options_t *options,
                                        const cos_string_t *bucket, 
                                        const cos_string_t *object,
                                        const cos_string_t *upload_id, 
                                        int part_num, 
                                        cos_upload_file_t *upload_file,
                                        cos_table_t **resp_headers);
```

#### パラメータ説明
| パラメータ名 | パラメータ説明 | タイプ | 
|---------|---------|---------|
| options | COSリクエストオプション |Struct|  
| bucket | Bucketの名前。Bucketの命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません|String|  
| object | Object名 |String|  
| upload_id | アップロードタスク番号|String|  
| part_num | パート番号|Int|  
| upload_file | アップロード待ちのローカルファイル情報|Struct|  
| resp_headers |HTTP応答メッセージのヘッダーフィールドを返します |Struct|  

#### 戻り結果の説明
| 返された結果 | 説明 | タイプ | 
|---------|---------|---------|
| code | エラーコード  |Int|        
| error_code | エラーコードの内容|String|   
| error_msg |エラーコードの説明 |String|   
| req_id | リクエストメッセージID |String|

#### 例
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
##### 機能説明
Complete Multipart Uploadは、全体のマルチパートアップロードを完了するために使用されます。Upload Partsを使用してすべてのパートをアップロードした後、このAPIでアップロードを完了できます。このAPIを使用するとき、パートの正確さを検証するために、ボディの各パートにPartNumberとETagを指定する必要があります。

#### 方法のプロトタイプ
```cpp
cos_status_t *cos_complete_multipart_upload(const cos_request_options_t *options,
                                            const cos_string_t *bucket, 
                                            const cos_string_t *object, 
                                            const cos_string_t *upload_id, 
                                            cos_list_t *part_list, 
                                            cos_table_t *headers,
                                            cos_table_t **resp_headers);
```

#### パラメータ説明
| パラメータ名 | パラメータ説明 | タイプ | 
|---------|---------|---------|
| options | COSリクエストオプション|Struct|  
| bucket | Bucketの名前。Bucketの命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません|String|  
| object | Object名|String|  
| upload_id | アップロードタスク番号|String|  
| part_list | マルチパートアップロードが完了したパラメータ|Struct|  
| part_number | パート番号|String|  
| etag | パートのETag値は、sha1チェック値であり、チェック値の前後に二重引用符を追加する必要があります。例えば"3a0f1fd698c235af9cf098cb74aa25bc"|String|  
| headers | COSリクエストの追加ヘッダーフィールド|Struct| 
| resp_headers | HTTP応答メッセージのヘッダーフィールドを返します|Struct|  

#### 戻り結果の説明
| 返された結果 | 説明 | タイプ | 
|---------|---------|---------|
| code | エラーコード  |Int|        
| error_code | エラーコードの内容|String|   
| error_msg |エラーコードの説明 |String|   
| req_id | リクエストメッセージID|String| 

#### 例
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
##### 機能説明
List Partsは、特定のマルチパートアップロードでアップロードされたパートを照合するために使用されます。

#### 方法のプロトタイプ
```cpp
cos_status_t *cos_list_upload_part(const cos_request_options_t *options,
                                   const cos_string_t *bucket, 
                                   const cos_string_t *object, 
                                   const cos_string_t *upload_id, 
                                   cos_list_upload_part_params_t *params,
                                   cos_table_t **resp_headers);
```

#### パラメータ説明
| パラメータ名 | パラメータ説明 | タイプ | 
|---------|---------|---------|
| options | COSリクエストオプション|Struct|  
| bucket | Bucketの名前。Bucketの命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません|String|  
| object | Object名 |String|  
| upload_id | アップロードタスク番号|String|  
| params | List Parts操作パラメータ |Struct| 
| part_number_marker |デフォルトではUTF-8のバイナリ順でエントリを一覧表示します。すべての一覧表示されるエントリはmarkerから開始します |String|  
| encoding_type  |戻り値のエンコーディング方式を規定します |String|  
| max_ret |一度に返されたエントリの最大数、デフォルト：1000|String|  
| truncated | 返されたエントリが遮断されたかどうか、'true'または'false'|Boolean|  
| next_part_number_marker | 仮に返されたエントリが遮断された場合、返されたNextMarkerは次のエントリの起点です|String|  
| part_list | 完了したパートの情報|Struct|      
| part_number | パート番号|String|  
| size |パートのサイズ、単位：Byte |String|  
| etag | パートのSHA-1アルゴリズムチェック値|String|  
| last_modified | パートの最終変更時間|String|  
| resp_headers | HTTP応答メッセージのヘッダーフィールドを返します|Struct|  

#### 戻り結果の説明
| 返された結果 | 説明 | タイプ | 
|---------|---------|---------|
| code | エラーコード  |Int|        
| error_code | エラーコードの内容|String|   
| error_msg |エラーコードの説明 |String|   
| req_id | リクエストメッセージID |String| 

#### 例
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
##### 機能説明
Abort Multipart Uploadは、1つのマルチパートアップロードを破棄し、アップロードされたパートを削除するために使用されます。このAbort Multipart Uploadを呼び出すとき、このUpload Partsを使用しているリクエストがあると、Upload Partsは失敗を返します。

#### 方法のプロトタイプ
```cpp
cos_status_t *cos_abort_multipart_upload(const cos_request_options_t *options,
                                         const cos_string_t *bucket, 
                                         const cos_string_t *object, 
                                         cos_string_t *upload_id, 
                                         cos_table_t **resp_headers);
```

#### パラメータ説明
| パラメータ名 | パラメータ説明 | タイプ | 
|---------|---------|---------|
| options | COSリクエストオプション |Struct| 
| bucket | Bucketの名前。Bucketの命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません|String|  
| object | Object名|String|  
| upload_id | アップロードタスク番号|String| 
| resp_headers |HTTP応答メッセージのヘッダーフィールドを返します |Struct|  


#### 戻り結果の説明
| 返された結果 | 説明 | タイプ | 
|---------|---------|---------|
| code | エラーコード  |Int|        
| error_code | エラーコードの内容|String|   
| error_msg |エラーコードの説明 |String|   
| req_id | リクエストメッセージID |String|

#### 例
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
##### 機能説明
List Multiparts Uploadsは、実行中のマルチパートアップロードを照合するために使用されます。単回リクエスト操作で、最大1000個の実行中のマルチパートアップロードがリストされます。

#### 方法のプロトタイプ
```cpp
cos_status_t *cos_list_multipart_upload(const cos_request_options_t *options,
                                        const cos_string_t *bucket, 
                                        cos_list_multipart_upload_params_t *params, 
                                        cos_table_t **resp_headers);
```

#### パラメータ説明
| パラメータ名 | パラメータ説明 | タイプ | 
|---------|---------|---------|
| options | COSリクエストオプション |Struct|  
| bucket | Bucketの名前。Bucketの命名規則は{name}-{appid}とします。ここに入力するバケット名をこのフォーマットにしなければなりません|String|  
| params | List Multipart Uploads操作パラメータ|Struct|  
| encoding_type  | 戻り値のエンコーディング方式を規定します|String|  
| prefix | プレフィックスのマッチング。返されたファイルのプレフィックスアドレスの設定に使用されます|String| 
|upload_id_marker |仮に返されたエントリが遮断された場合、返されたNextMarkerは次のエントリの起点です|String|
| delimiter | 区切り文字は記号です。<br>Prefixがある場合、プレフィックスからデリミターまでの間にある同じパスが1つのタイプに分類され、Common Prefixとして定義し、その後、すべてのCommon Prefixをリストアウトされます。<br>プレフィックスがない場合、パスの先頭から開始します|String|  
| max_ret |一度に返されたエントリの最大数、デフォルト：1000|String|  
| key_marker | upload-id-markerと一緒に使用します。<br>upload-id-markerが指定されていない場合は、ObjectNameがkey-markerの後（アルファベット順）にあるエントリがリストされます。<br>upload-id-markerが指定されている場合、ObjectNameがkey-markerの後（アルファベット順）にあるエントリがリストされます。ObjectNameがアルファベット順でkey-markerと同じ、同時にUploadIDがupload-id-markerの後（アルファベット順）にあるエントリがリストされます。|String|  
| upload_id_marker |key-markerと共に使用されます。<br>key-markerが指定されていない場合、upload-id-markerが無視されます。<br>key-markerが指定された場合、ObjectNameがkey-markerの前（アルファベット順）にあるエントリがリストされます。ObjectNameがアルファベット順でkey-markerと同じ、同時にUploadIDがupload-id-markerの前（アルファベット順）にあるエントリがリストされます。| String| 
| truncated | 返されたエントリが遮断されたかどうか、'true'または'false'|Boolean|  
| next_key_marker | 仮に返されたエントリが遮断された場合、返されたNextMarkerは次のエントリの起点です|String|  
| next_upload_id_marker |仮に返されたエントリが遮断された場合、返されたNextMarkerは次のエントリの起点です |String|  
| upload_list | マルチパートアップロードの情報|Struct|  
| key | Object名|String|  
| upload_id |今回のマルチパートアップロードのIDを示します |String|  
| initiated | 今回のマルチパートアップロードタスクの開始時間を示します|String|  
| resp_headers | HTTP応答メッセージのヘッダーフィールドを返します|Struct|  

```
typedef struct {
    cos_list_t node;
    cos_string_t key;
    cos_string_t upload_id;
    cos_string_t initiated;
} cos_list_multipart_upload_content_t;
```


#### 戻り結果の説明
| 返された結果 | 説明 | タイプ | 
|---------|---------|---------|
| code | エラーコード  |Int|        
| error_code | エラーコードの内容|String|   
| error_msg |エラーコードの説明 |String|   
| req_id | リクエストメッセージID |String|

#### 例
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

## 異常説明

SDKが失敗した時、結果情報はAPIによって返されたcos_status_t構造に含まれています。

以下はcos_status_t構造の説明です：

| cos_status_tメンバー | 説明                                       | タイプ        |
| ---------------- | ---------------------------------------- | --------- |
| code    | 応答のステータスコードであり、4xxはクライアントによるリクエストの失敗を指し、5xxはサーバー異常による失敗です。[COSエラーメッセージ](https://cloud.tencent.com/document/product/436/7730)を参照してください               | Int    |
| error_code      | リクエストが失敗した時にボディにより返されたError Codeについては、[COSエラーメッセージ](https://cloud.tencent.com/document/product/436/7730)を参照してください                              | String    |
| error_msg   | リクエストが失敗した時にボディにより返されたError Messageについては、[COSエラーメッセージ](https://cloud.tencent.com/document/product/436/7730)を参照してください | String    |
| req_id | リクエストID、ユーザーの一意のリクエストを示すために使用されます | String    |

