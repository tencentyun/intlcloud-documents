## 開発準備
### 関連するリソース
COSのXML C SDKリソースのダウンロードアドレス：[XML C SDK GitHubダウンロード](https://github.com/tencentyun/cos-c-sdk-v5)。
Demoのダウンロードアドレス：[XML C SDK Demo](https://github.com/tencentyun/cos-c-sdk-v5/blob/master/cos_c_sdk_test/cos_demo.c)。

### 開発環境
1. CMakeツール（2.6.0以上推奨）をインストールして、[こちら](http://www.cmake.org/download/)をクリックしてダウンロードします。典型的なインストール方法は次のとおりです：
```bash
./configure
make
make install
```
2. libcurl（7.32.0以上推奨）をインストールして、[こちら](http://curl.haxx.se/download.html?spm=5176.doc32132.2.7.23MmBq)をクリックしてダウンロードします。典型的なインストール方法は次のとおりです：
```bash
./configure
make
make install
```
3. apr（1.5.2推奨）をインストールして、[こちら](https://apr.apache.org/download.cgi?spm=5176.doc32132.2.9.23MmBq&file=download.cgi)をクリックしてダウンロードします。典型的なインストール方法は次のとおりです：
```bash
./configure
make
make install
```
4. apr-util（1.5.4以上推奨）をインストールして、[こちら](https://apr.apache.org/download.cgi?spm=5176.doc32132.2.10.23MmBq&file=download.cgi)をクリックしてダウンロードします。インストール中に--with-aprオプションを指定する必要があります。典型的なインストール方法は次のとおりです：
```bash
./configure --with-apr=/your/apr/install/path
make
make install
```
5. minixml（2.8以上推奨）をインストールして、[こちら](https://www.msweet.org/mxml/)をクリックしてダウンロードします。典型的なインストール方法は次のとおりです：
```bash
./configure
make
sudo make install
```

### SDKインストール
ソースコードインストール。[GitHub](https://github.com/tencentyun/cos-c-sdk-v5)からソースコードをダウンロードします。典型的なコンパイルコマンドは次のとおりです：
```bash
cmake .
make
make install
```

## SDKの初期化
### SDK実行環境の初期化
```cpp
int main(int argc, char *argv[])
{
    /* プログラムのエントリでcos_http_io_initializeメソッドを呼び出します。ネットワーク、メモリなどを含むグローバルリソースの初期化を内部的に行います */
    if (cos_http_io_initialize(NULL, 0) != COSE_OK) {
        exit(1);
    }

    /* COS SDKのAPIを呼び出して、ファイルをアップロードまたはダウンロードします */
    /* ... ユーザーのロジックコード、ここでは省略されます*/

    /* プログラムが終了する前に、cos_http_io_deinitializeメソッドを呼び出して、以前に割り当てられたグローバルリソースをリリースします */
    cos_http_io_deinitialize();
    return 0;
}
```

### リクエストオプションの初期化
```cpp
    /* apr_pool_tと同じ、メモリ管理用のメモリプール、実装コードはaprライブラリにあります */
    cos_pool_t *pool;
    cos_request_options_t *options;

    /* 新しいメモリプールを再作成します。2番目のパラメータはNULLで、他のメモリプールから継承されていないことを示しています */
    cos_pool_create(&pool, NULL);

    /* optionsの作成と初期化、このパラメータには、主にendpoint、access_key_id、acces_key_secret、is_cname、curlパラメータなどのグローバル構成情報が含まれます
     * optionsのメモリはpoolによって割り当てられ、poolがリリースされた後は、optionsのメモリもリリースされ、メモリを個別にリリースする必要がなくなります
     */ 
    options = cos_request_options_create(pool);
    options->config = cos_config_create(options->pool);

    /* cos_str_setはchar*タイプの文字列を使用してcos_string_tタイプを初期化します*/
    cos_str_set(&options->config->endpoint, "<ユーザーのEndpoint>");              //Endpointは、ユーザーが所在するキャンパスのCOSサービスドメイン名に基づいて記入されます
    cos_str_set(&options->config->access_key_id, "<ユーザーのSecretId>");         //ユーザーがCOSサービスを登録した後に取得されたSecretId
    cos_str_set(&options->config->access_key_secret, "<ユーザーのSecretKey>");    //ユーザーがCOSサービスを登録した後に取得されたSecretKey
    cos_str_set(&options->config->appid, "<ユーザーのAppId>");                    //ユーザーがCOSサービスを登録した後に取得されたAppId

    /* sts_tokenの設定を通して、一時暗号鍵を使用します。一時暗号鍵を使用する場合、access_key_idとaccess_key_secretの両方を、対応一時暗号鍵にセットするSecretIdとSecretKeyに設定する必要があります */
    //cos_str_set(&options->config->sts_token, "MyTokenString");
    /* CNAMEを使用するかどうか */
    options->config->is_cname = 0;

    /* タイムアウト時間などのネットワーク関連パラメータを設定するために使用されます*/
    options->ctl = cos_http_controller_create(options->pool, 0);

    /* アップロードリクエストがContent-MD5ヘッダーを自動的に追加するかどうかを設定するために使用されます。enableはCOS_FALSEの場合、アップロードリクエストがContent-MD5ヘッダーを自動的に追加しません。enableはCOS_TRUEの場合、アップロードリクエストがContent-MD5ヘッダーを自動的に追加します。このオプションを設定しない場合、デフォルトでContent-MD5ヘッダーを追加します */
    cos_set_content_md5_enable(options->ctl, COS_FALSE);
	
    /* リクエストルーティングのアドレスとポートの設定に使用されます。通常はこのパラメータを設定する必要がありません。リクエストがドメイン名に従ってルーティングを解析します */
    //cos_set_request_route(options->ctl, "192.168.12.34", 80);
```

##  SDK一般使用手順
1. SDKを初期化します。
2. リクエストオプションパラメータを設定します。
APPID、SecretId、SecretKey、Bucketなどの名称の意味と取得方法については、[COS用語情報](https://cloud.tencent.com/document/product/436/7751#.E6.9C.AF.E8.AF.AD.E4.BF.A1.E6.81.AF)を参照してください。
  -  APPIDは、Tencent Cloudアカウントの申請後にシステムによって割り当てられたアカウントIDの1つです。
  - access_key_idとaccess_key_secretはアカウントAPI暗号鍵。
  - endpointはCOSアクセスドメイン情報です。詳細情報について、[使用可能な地域およびアクセスドメイン](https://cloud.tencent.com/document/product/436/6224)ドキュメントを確認してください。例えば、広州地区endpointが`cos.ap-guangzhou.myqcloud.com`です。
3. APIの必要なパラメータを設定します。
4. SDK APIを呼び出して、リクエストし、リクエスト応答結果を取得します。

### Bucketの作成
```cpp
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_acl_e cos_acl = COS_ACL_PRIVATE;
    cos_string_t bucket;
    cos_table_t *resp_headers = NULL;
    
    /* 新しいメモリプールを再作成します。2番目のパラメータはNULLで、他のメモリプールから継承されていないことを示しています */
    cos_pool_create(&p, NULL);
    
    /* optionsの作成と初期化、このパラメータには、主にendpoint、access_key_id、acces_key_secret、is_cname、curlパラメータなどのグローバル構成情報が含まれます
     * optionsのメモリはpoolによって割り当てられ、poolがリリースされた後は、optionsのメモリもリリースされ、メモリを個別にリリースする必要がなくなります
     */
    options = cos_request_options_create(p);
    options->config = cos_config_create(options->pool);
    init_test_config(options->config, is_cname);
    
    /* appid、endpoint、access_key_id、acces_key_secret、is_cname、curlパラメータなどの構成情報を設定します */
    cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
    cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
    cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
    cos_str_set(&options->config->appid, TEST_APPID);
    options->config->is_cname = is_cname;
    options->ctl = cos_http_controller_create(options->pool, 0);
    /* bucketの命名規則は{name}-{appid}です。ここに記入するバケット名称はこのフォーマットでなければなりません */
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    /* apiを呼び出してbucketを作成します */
    s = cos_create_bucket(options, &bucket, cos_acl, &resp_headers);
    if (cos_status_is_ok(s)) {
        printf("create bucket succeeded\n");
    } else {
        printf("create bucket failed\n");
    }
    
    //destroy memory pool
    cos_pool_destroy(p); 
```

### ファイルのアップロード
```cpp
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_string_t object;
    cos_string_t file;
    cos_table_t *resp_headers = NULL;
    
    /* 新しいメモリプールを再作成します。2番目のパラメータはNULLで、他のメモリプールから継承されていないことを示しています */
    cos_pool_create(&p, NULL);
    
    /* optionsの作成と初期化、このパラメータには、主にendpoint、access_key_id、acces_key_secret、is_cname、curlパラメータなどのグローバル構成情報が含まれます
     * optionsのメモリはpoolによって割り当てられ、poolがリリースされた後は、optionsのメモリもリリースされ、メモリを個別にリリースする必要がなくなります
     */
    options = cos_request_options_create(p);
    options->config = cos_config_create(options->pool);
    init_test_config(options->config, is_cname);

    /* appid、endpoint、access_key_id、acces_key_secret、is_cname、curlパラメータなどの構成情報を設定します */
    cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
    cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
    cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
    cos_str_set(&options->config->appid, TEST_APPID);
    options->config->is_cname = is_cname;
    options->ctl = cos_http_controller_create(options->pool, 0);
    /* bucketの命名規則は{name}-{appid}です。ここに記入するバケット名称はこのフォーマットでなければなりません */
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    /* apiを呼び出してファイルをアップロードします */
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

### ファイルのダウンロード
```cpp
    cos_pool_t *p = NULL;
    int is_cname = 0;
    cos_status_t *s = NULL;
    cos_request_options_t *options = NULL;
    cos_string_t bucket;
    cos_string_t object;
    cos_string_t file;
    cos_table_t *resp_headers = NULL;
    
    /* 新しいメモリプールを再作成します。2番目のパラメータはNULLで、他のメモリプールから継承されていないことを示しています */
    cos_pool_create(&p, NULL);
    
    /* optionsの作成と初期化、このパラメータには、主にendpoint、access_key_id、acces_key_secret、is_cname、curlパラメータなどのグローバル構成情報が含まれます
     * optionsのメモリはpoolによって割り当てられ、poolがリリースされた後は、optionsのメモリもリリースされ、メモリを個別にリリースする必要がなくなります
     */
    options = cos_request_options_create(p);
    options->config = cos_config_create(options->pool);
    init_test_config(options->config, is_cname);

   /* appid、endpoint、access_key_id、acces_key_secret、is_cname、curlパラメータなどの構成情報を設定します */
    cos_str_set(&options->config->endpoint, TEST_COS_ENDPOINT);
    cos_str_set(&options->config->access_key_id, TEST_ACCESS_KEY_ID);
    cos_str_set(&options->config->access_key_secret, TEST_ACCESS_KEY_SECRET);
    cos_str_set(&options->config->appid, TEST_APPID);
    options->config->is_cname = is_cname;
    options->ctl = cos_http_controller_create(options->pool, 0);
    /* bucketの命名規則は{name}-{appid}です。ここに記入するバケット名称はこのフォーマットでなければなりません */
    cos_str_set(&bucket, TEST_BUCKET_NAME);

    /* apiを呼び出してファイルをダウンロードします */
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

