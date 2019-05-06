## 署名の生成

### Sign機能の説明

署名の生成

### 方法プロトタイプ1

```
static std::string Sign(const std::string& secret_id,
                        const std::string& secret_key,
                        const std::string& http_method,
                        const std::string& in_uri,
                        const std::map<std::string, std::string>& headers,
                        const std::map<std::string, std::string>& params);
```

#### パラメータ説明 

| パラメータ名    | パラメータ説明                                              | タイプ                     |
| ----------- | ----------------------------------------------------- | ------------------------ |
| secret_id   | 開発者の保有するプロジェクト身元識別IDで、身元認証に使用されます             | String                   |
| secret_Key  | 開発者の保有するプロジェクト身元暗号鍵                              | String                   |
| http_method | HTTP方法、例えばPOST/GET/HEAD/PUTなど、入力する大文字と小文字を区別しません | String                   |
| in_uri      | HTTP uri                                              | String                   |
| headers     | HTTP headerのキー値ペア                                  | map&lt;string,string&gt; |
| params      | HTTP paramsのキー値ペア                                  | map&lt;string,string&gt; |

#### 戻り結果の説明

署名が返却されると、指定の有効期間以内に（CosSysConfigにより設置できます。デフォルト値は60sです）使用できます。空文字列が返却されると、署名失敗を表します。

### 方法プロトタイプ2

```
static std::string Sign(const std::string& secret_id,
                        const std::string& secret_key,
                        const std::string& http_method,
                        const std::string& in_uri,
                        const std::map<std::string, std::string>& headers,
                        const std::map<std::string, std::string>& params,
                        uint64_t start_time_in_s,
                        uint64_t end_time_in_s);
```

#### パラメータ説明 

| パラメータ名        | パラメータ説明                                             | タイプ                      |
| --------------- | ---------------------------------------------------- | ------------------------- |
| secret_id       | 開発者の保有するプロジェクト身元識別IDで、身元認証に使用されます            | String                    |
| secret_Key      | 開発者の保有するプロジェクト身元暗号鍵                              | String                   |
| http_method     | HTTP方法、例えば POST/GET/HEAD/PUTなどのように、入力する大文字と小文字を区別しません | String                   |
| in_uri          | HTTP uri                                             | String                    |
| headers         | HTTP headerのキー値ペア                                 | map &lt;string,string&gt; |
| params          | HTTP paramsのキー値ペア                                 | map &lt;string,string&gt; |
| start_time_in_s | 署名発効の開始時間                                   | uint64_t                  |
| end_time_in_s   | 署名発効の締切時間                                   | uint64_t                  |

#### 戻り結果の説明

String、署名が返却されると、指定の有効期間以内に使用できます。空文字列が返却されると、署名失敗を表します。

## Service/Bucket/Object操作

すべてのService/Bucket/Objectに関連する方法プロトタイプを、下記に示すフォーマットで表現します：

```
CosResult Operator(BaseReq, BaseResp)
```

### CosResult

CosResultはリクエストエラー時に返却されるエラーコードと対応のエラー情報をカプセル化しており、詳しくは [エラーコード]を参照してください(/document/product/436/7730 "错误码")。

>!SDK内部でカプセル化されるリクエストにつき、CosResultオブジェクトが返却され、毎回の呼び出しが終わったら、IsSucc()メンバー関数でその呼び出しが成功したかを判断する必要があります。

#### メンバー関数

| 関数                      | 関数説明                                                     |
| ------------------------- | ------------------------------------------------------------ |
| bool isSucc()             | その度の呼び出しが成功したか失敗したかの結果が返却されます。<br>falseが返却される場合：次のCosResultメンバー関数は有意義となります。<br>Trueが返却される場合：OperatorRespから具体的に返却されたコンテンツを取得できます。 |
| string GetErrorCode()     |COSから返却されるエラーコードを取得し、エラーシナリオの確認に使用します。                    |
| string GetErrorMsg()      | 具体的なエラー情報を含みます。                                         |
| string GetResourceAddr()  | リソースアドレス、BucketアドレスまたはObjectアドレス。                        |
| string GetXCosRequestId() | リクエストが送信される時、サーバーはリクエストに対して自動で唯一のIDを生成します。<br>使用において問題が発生した時、request-idはCOSに向けて速やかにポジショニングの問題を解決します。 |
| string GetXCosTraceId() | リクエストエラーの場合、サーバーはエラーに対して唯一のIDを生成します。<br>使用において問題が発生した時、trace-idはCOSに向けて速やかにポジショニングの問題を解決します。<br>リクエストエラーの場合、trace-idとrequest-idは一対一対応しています。
| string GetErrorInfo() | SDK内部エラー情報を取得します。|
| int GetHttpStatus() | HTTPステータスコードを取得します。|

#### BaseReq/BaseResp

BaseReq、BaseRespはリクエストとレスポンスをカプセル化しており、それぞれの操作タイプにより異なるOperatorReq（例えば、後に紹介の GetBucketReq）を生成し、またOperatorReqのコンテンツを塗りつぶしすると良いです。
関数が返却された後、対応のBaseRespのメンバー関数を呼び出してリクエスト結果を取得します。

- Requestにつき、特別な説明がない限り、Requestの構造関数にのみ注目する必要があります。
- Responseにつき、全ての方法のResponseは共通応答ヘッダーのメンバー関数を取得します。 
  Responseの共通のメンバー関数を下記に示します。具体的なフィールドの意味につき [共通応答ヘッダー](/document/product/436/7729 "公共返回头部")を参照してください。ここで、記載されていません：

```
uint64_t GetContentLength();
std::string GetContentType();
std::string GetEtag();
std::string GetConnection();
std::string GetDate();
std::string GetServer();
std::string GetXCosRequestId();
std::string GetXCosTraceId();
```

## Bucket操作

### Get Bucket

##### 機能説明

Get BucketリクエストはList Objectリクエストに等しく、当該Bucekt下の一部あるいははすべてのObjectをリストすることができます。当該リクエストを出すには、Read権限が必要です。関連APIドキュメントについては、[Get Bucket](/document/product/436/7734)を参照してください。

#### 方法のプロトタイプ

```cpp
CosResult GetBucket(const GetBucketReq& req, GetBucketResp* resp);
```

#### パラメータ説明

| パラメータ | パラメータ説明                                |
| ---- | --------------------------------------- |
| req | GetBucketReq、GetBucket操作のリクエスト。   |
| resp | GetBucketResp、GetBucket操作のレスポンス。 |

GetBucketRespは以下のメンバー関数を提供し、Get Bucketから返却されるXMLフォーマットにおける具体的内容の取得に使用されます。 

```C++
std::vector<Content> GetContents();
std::string GetName();
std::string GetPrefix();
std::string GetMarker();
uint64_t GetMaxKeys();
bool IsTruncated();
std::vector<std::string> GetCommonPrefixes();
```

そのうち、Contentの定義を下記に示します：

```
struct Content {
    std::string m_key; //ObjectのKey
    std::string m_last_modified; //Objectの最終変更時間
    std::string m_etag; //ファイルのMD-5アルゴリズムチェック値
    std::string m_size; //ファイルのサイズ、単位はByteです
    std::vector<std::string> m_owner_ids; //Bucket保有者情報
    std::string m_storage_class; //Objectのストレージタイプ、列挙値：STANDARD、STANDARD_IA
};
```

#### 例

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-123456789";

//GetBucketReqの構造関数にbucket_nameを入力する必要があります
qcloud_cos::GetBucketReq req(bucket_name);
qcloud_cos::GetBucketResp resp;
qcloud_cos::CosResult result = cos.GetBucket(req, &resp);

//呼び出しに成功した場合、respのメンバー関数を呼び出してレスポンス内容を取得します
if (result.IsSucc()) {
    std::cout << "Name=" << resp.GetName() << std::endl;
    std::cout << "Prefix=" << resp.GetPrefix() << std::endl;
    std::cout << "Marker=" << resp.GetMarker() << std::endl;
    std::cout << "MaxKeys=" << resp.GetMaxKeys() << std::endl;
} else {
    std::cout << "ErrorInfo=" << result.GetErrorInfo() << std::endl;
    std::cout << "HttpStatus=" << result.GetHttpStatus() << std::endl;
    std::cout << "ErrorCode=" << result.GetErrorCode() << std::endl;
    std::cout << "ErrorMsg=" << result.GetErrorMsg() << std::endl;
    std::cout << "ResourceAddr=" << result.GetResourceAddr() << std::endl;
    std::cout << "XCosRequestId=" << result.GetXCosRequestId() << std::endl;
    std::cout << "XCosTraceId=" << result.GetXCosTraceId() << std::endl;
} 
```

### Put Bucket

##### 機能説明

Put Bucket APIリクエストは指定アカウントの下でBucketを作成できます。当該APIが匿名リクエストに対応しないため、Authorization署名認証付きのリクエストで新しいBucketを作成する必要があります。Bucketを作成したユーザーはデフォルトでBucketの所有者となります。関連APIドキュメントにつき、[Put Bucket](/document/product/436/7738)を参照してください。

#### 方法のプロトタイプ

```cpp
CosResult PutBucket(const PutBucketReq& req, PutBucketResp* resp);
```

#### パラメータ説明

| パラメータ | パラメータ説明                              |
| ---- | ------------------------------------- |
| req  | PutBucketReq、PutBucket操作のリクエスト。  |
| resp | PutBucketResp、PutBucket操作のレスポンス。 |

PutBucketReqは以下のメンバー関数を提供します：

```C++
//BucketのACL属性を定義する場合、有効値：private,public-read-write,public-read
// デフォルト値：private
void SetXCosAcl(const std::string& str);

//権限が付与された者に読み取り権限を付与します。フォーマット：x-cos-grant-read: id=" ",id=" "。
// サブアカウントに権限を付与する場合、id="qcs::cam::uin/<OwnerUin>!:uin/<SubUin>!"
//ルートアカウントに権限を付与する場合、id="qcs::cam::uin/<OwnerUin>!:uin/<OwnerUin>!"
void SetXCosGrantRead(const std::string& str);

//権限が付与された者に書き込み権限を付与します。フォーマット：x-cos-grant-write: id=" ",id=" "./
// サブアカウントに権限を付与する場合、id="qcs::cam::uin/<OwnerUin>!:uin/<SubUin>!"、
//ルートアカウントに権限を付与する場合、id="qcs::cam::uin/<OwnerUin>!:uin/<OwnerUin>!"
void SetXCosGrantWrite(const std::string& str);
    
//権限が付与された者に読み取りと書き込み権限を付与します。フォーマット：x-cos-grant-full-control: id=" ",id=" "。
// サブアカウントに権限を付与する場合、id="qcs::cam::uin/<OwnerUin>!:uin/<SubUin>!"、
//ルートアカウントに権限を付与する場合、id="qcs::cam::uin/<OwnerUin>!:uin/<OwnerUin>!"
void SetXCosGrantFullControl(const std::string& str);
```

#### 例

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-123456789";

qcloud_cos::PutBucketReq req(bucket_name);
qcloud_cos::PutBucketResp resp;
qcloud_cos::CosResult result = cos.PutBucket(req, &resp);

//呼び出しに成功した場合、respのメンバー関数を呼び出してレスポンス内容を取得します
if (result.IsSucc()) {
    // ...
} else {
    //Bucketの作成に失敗した場合、CosResultのメンバー関数を呼び出してエラー情報、例えばrequestIDなどを出力することができます
} 
```

### Delete Bucket

##### 機能説明

Delete Bucket APIリクエストは指定アカウントの下でBucketを削除できます。削除する前に、Bucket内の内容が空白でなければなりません。Bucket内の情報を削除してから、初めてBucket自体を削除できます。関連APIドキュメントについては、[Delete Bucket](/document/product/436/7732)を参照してください。

#### 方法のプロトタイプ

```cpp
CosResult DeleteBucket(const DeleteBucketReq& req, DeleteBucketResp* resp);
```

#### パラメータ説明

| パラメータ | パラメータ説明                                   |
| ---- | ------------------------------------------ |
| req  | DeleteBucketReq、DeleteBucket操作のリクエスト。 |
| resp | DeletBucketResp、DeletBucket操作のレスポンス。  |

#### 例

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-123456789";

//DeleteBucketReqの構造関数にbucket_nameを入力する必要があります
qcloud_cos::DeleteBucketReq req(bucket_name);
qcloud_cos::DeleteBucketResp resp;
qcloud_cos::CosResult result = cos.DeleteBucket(req, &resp);

//呼び出しに成功した場合、respのメンバー関数を呼び出してレスポンス内容を取得します
if (result.IsSucc()) {
    // ...
} else {
    //Bucketの削除に失敗した場合、CosResultのメンバー関数を呼び出してエラー情報、例えばrequestIDなどを出力することができます
} 
```

### Put Bucket Replication

##### 機能説明

Put Bucket Replicationリクエストはバージョン管理を有効にしたバケットにレプリケーション構成を追加するために使用します。バケットにレプリケーション構成が既にある場合は、このリクエストは既存の構成を置き換えます。

#### 方法のプロトタイプ

```cpp
CosResult PutBucketReplication(const DPutBucketReplicationReq& req, PutBucketReplicationResp* resp);
```

#### パラメータ説明

| パラメータ | パラメータ説明                                                    |
| ---- | ----------------------------------------------------------- |
| req  | PutBucketReplicationReq、PutBucketReplication操作のリクエスト。  |
| resp | PutBucketReplicationResp、PutBucketReplication操作のレスポンス。 |

```
//Replicationの発信元身元IDを設定する場合、roleのフォーマット：qcs::cam::uin/[UIN]:uin/[Subaccount]
void SetRole(const std::string& role);

//ReplicationRuleの追加
void AddReplicationRule(const ReplicationRule& rule);

//ReplicationRulesの設定
void SetReplicationRule(const std::vector<ReplicationRule>& rules);
```

そのうち、ReplicationRuleの定義を下記に示します：

```
struct ReplicationRule {
    bool m_is_enable; //当該Ruleが有効になるか
    std::string m_id; //非選択必須フィールドで、具体的なRule名の表示に使用されます
    std::string m_prefix; //プレフィックスのマッチングポリシーとして、重複してはなりません。重複すると、エラーが表示されます。プレフィックスのマッチングのルートディレクトリはブランクです
    std::string m_dest_bucket; //目標Bucketを識別する場合、リソース識別子：qcs:id/0:Cos:[region]:appid/[AppId]:[bucketname]
    std::string m_dest_storage_class; //非選択必須フィールド、ストレージレベル、列挙値：Standard,Standard_IA。ブランクの場合、元バケットレベルのままを表します

    ReplicationRule();
    ReplicationRule(const std::string& prefix,
                    const std::string& dest_bucket,
                    const std::string& storage_class = "", 
                    const std::string& id = "", 
                    bool is_enable = true);
};
```

#### 例

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-123456789";

//PutBucketReplicationReqの構造関数をbucket_nameに入力する必要があります
qcloud_cos::PutBucketReplicationReq req(bucket_name);
req.SetRole("qcs::cam::uin/***:uin/****");
qcloud_cos::ReplicationRule rule("sevenyou_10m", "qcs:id/0:cos:cn-south:appid/***:sevenyousouthtest", "", "RuleId_01", true);
req.AddReplicationRule(rule)

qcloud_cos::PutBucketReplicationResp resp;
qcloud_cos::CosResult result = cos.PutBucketReplication(req, &resp);

//呼び出しに成功した場合、respのメンバー関数を呼び出してレスポンス内容を取得します
if (result.IsSucc()) {
    // ...
} else {
    //オリジン間レプリケーションの設定に失敗した場合、CosResultのメンバー関数を呼び出してエラー情報、例えばrequestIDなどを出力することができます
} 
```

### Get Bucket Replication

##### 機能説明

Get Bucket Replication APIはバケット中のユーザーによるクロスオリジンレプリケーション構成情報を読み取るようにリクエストします。

#### 方法のプロトタイプ

```cpp
CosResult GetBucketReplication(const DGetBucketReplicationReq& req, GetBucketReplicationResp* resp);
```

#### パラメータ説明

| パラメータ | パラメータ説明                                                    |
| ---- | ----------------------------------------------------------- |
| req  | GetBucketReplicationReq、GetBucketReplication操作のリクエスト。  |
| resp | GetBucketReplicationResp、GetBucketReplication操作のレスポンス。 |

```
//Replicationの発信元身元を取得します
std::string GetRole();

//ReplicationRulesを取得する場合、ReplicationRuleの定義については、Put Bucket Replicationを参照してください
std::vector<ReplicationRule> GetRules();
```

#### 例

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-123456789";

// GetBucketReplicationReqの構造関数にbucket_nameを渡す必要があります
qcloud_cos::GetBucketReplicationReq req(bucket_name);
qcloud_cos::GetBucketReplicationResp resp;
qcloud_cos::CosResult result = cos.GetBucketReplication(req, &resp);

//呼び出しに成功した場合、respのメンバー関数を呼び出してレスポンス内容を取得します
if (result.IsSucc()) {
    // ...
} else {
    //オリジン間コピー構成の取得に失敗した場合、CosResultのメンバー関数を呼び出してエラー情報、例えばrequestIDなどを出力することができます
} 
```

### Delete Bucket Replication

##### 機能説明

Delete Bucket Replication APIはバケット中のユーザーによるオリジン間コピー構成を削除するようにリクエストします。

#### 方法のプロトタイプ

```cpp
CosResult DeleteBucketReplication(const DDeleteBucketReplicationReq& req, DeleteBucketReplicationResp* resp);
```

#### パラメータ説明

| パラメータ | パラメータ説明                                                     |
| ---- | ------------------------------------------------------------ |
| req  | DeleteBucketReplicationReq、DeleteBucketReplication操作のリクエスト。 |
| resp | DeleteBucketReplicationResp、DeleteBucketReplication操作のレスポンス。 |

#### 例

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-123456789";

//DeleteBucketReplicationReqの構造関数にbucket_nameを渡す必要があります
qcloud_cos::DeleteBucketReplicationReq req(bucket_name);
qcloud_cos::DeleteBucketReplicationResp resp;
qcloud_cos::CosResult result = cos.DeleteBucketReplication(req, &resp);

//呼び出しに成功した場合、respのメンバー関数を呼び出してレスポンス内容を取得します
if (result.IsSucc()) {
    // ...
} else {
    //オリジン間コピー構成の削除に失敗した場合、CosResultのメンバー関数を呼び出してエラー情報、例えばrequestIDなどを出力することができます
} 
```

### Put Bucket Lifecycle

##### 機能説明

COSを使用すると、ユーザーはライフサイクル構成でバケット内のオブジェクトのライフサイクルを管理できます。ライフサイクル構成には、一連のオブジェクト規則に適用される1つ以上の規則セットが含まれます（各規則はCOSのために一つの操作を定義します）。
これらの操作は、次の2つのタイプに分けられます：

- 変換操作：定義オブジェクトをその他ストレージタイプに変換する場合にかかる時間。例えば、オブジェクト作成の30日後に、それをSTANDARD_IA（IAは、あまりアクセスしない場合に向きます）ストレージタイプに変換することができます。
- 期限切れ操作：Objectの期限切れ時間を指定します。COSは自動でユーザーのために期限切れのObjectを削除します。
  Put Bucket Lifecycleは、バケットのために新しいライフサイクル構成を作成するように使用されます。もしこのバケットにはライフサイクルが構成されている場合、このAPIを使用して新しい構成を作成すると同時に、元の構成が上書きされます。関連APIドキュメントについては、[Put Bucket Lifecycle](/document/product/436/8280)を参照してください。

#### 方法のプロトタイプ

```cpp
CosResult PutBucketLifecycle(const DPutBucketLifecycleReq& req, PutBucketLifecycleResp* resp);
```

#### パラメータ説明

| パラメータ | パラメータ説明                                                |
| ---- | ------------------------------------------------------- |
| req | PutBucketLifecycleReq、PutBucketLifecycle操作のリクエスト。  |
| resp | PutBucketLifecycleResp、PutBucketLifecycle操作のレスポンス。 |

```
//LifecycleRuleの追加
void AddRule(const LifecycleRule& rule)

//LifecycleRuleの設定
void SetRule(const std::vector<LifecycleRule>& rules)
```

LifecycleRuleの定義は少し複雑です。詳しくは下記に示します：

```
struct LifecycleTag {
    std::string key;
    std::string value;
};

class LifecycleFilter {
public:
    LifecycleFilter();

    std::string GetPrefix();
    std::vector<LifecycleTag> GetTags();

    void SetPrefix(const std::string& prefix);
    void SetTags(const std::vector<LifecycleTag>& tags);
    void AddTag(const LifecycleTag& tag);

    bool HasPrefix();
    bool HasTags();

private:
    std::string m_prefix; //規則の適用するプレフィックスを指定します。プレフィックスにマッチングするオブジェクトは当該規則から影響を受けます。Prefix最大は1つです
    std::vector<LifecycleTag> m_tags; //タグ、Tagは0または複数があります
};

class LifecycleTransition {
public:
    LifecycleTransition();

    uint64_t GetDays();
    std::string GetDate();
    std::string GetStorageClass();

    void SetDays(uint64_t days);
    void SetDate(const std::string& date);
    void SetStorageClass(const std::string& storage_class);

    bool HasDays();
    bool HasDate();
    bool HasStorageClass();
    
private:
    //同一規則において同時にDaysとDateを使用してはなりません
    uint64_t m_days; //規則の対応する操作が、オブジェクトの最終変更日後の何日以内に行われれば、有効値が非負整数になるかを表示します
    std::string m_date; //規則の対応する操作がいつ行われるかを表示します
    std::string m_storage_class; //Objectのダンプ先である目標ストレージタイプを指定します。列挙値： Standard_IA
};

class LifecycleExpiration {
public:
    LifecycleExpiration();
    
    uint64_t GetDays();
    std::string GetDate();
    bool IsExpiredObjDelMarker();
    
    void SetDays(uint64_t days);
    void SetDate(const std::string& date);
    void SetExpiredObjDelMarker(bool marker);

    bool HasDays();
    bool HasDate();
    bool HasExpiredObjDelMarker();
    
private:
    //同一規則において同時にDaysとDateを使用してはなりません
    uint64_t m_days; //規則の対応する操作が、オブジェクトの最終変更日後の何日以内に行われれば、有効値が正整数になるかを表示します
    std::string m_date; //規則の対応する操作がいつ行われるかを表示します
    bool m_expired_obj_del_marker; //期限切れオブジェクトの削除タグを削除します。列挙値true、false
};

class LifecycleNonCurrTransition {
public:
    LifecycleNonCurrTransition();

    uint64_t GetDays();
    std::string GetStorageClass();

    void SetDays(uint64_t days);  
    void SetStorageClass(const std::string& storage_class);

    bool HasDays();
    bool HasStorageClass();

private:
    uint64_t m_days; //規則の対応する操作が、オブジェクトの最終変更日後の何日以内に行われれば、有効値が非負整数になるかを表示します
    std::string m_storage_class; //Objectのダンプ先である目標ストレージタイプを指定します。列挙値： Standard_IA
};

class LifecycleNonCurrExpiration {
public:
    LifecycleNonCurrExpiration();
    
    uint64_t GetDays();

    void SetDays(uint64_t days);

    bool HasDays();

private:
    uint64_t m_days; //規則の対応する操作が、オブジェクトの最終変更日後の何日以内に行われれば、有効値が正整数になるかを表示します
};

struct AbortIncompleteMultipartUpload {
    uint64_t m_days_after_init; //マルチパートアップロード開始後の何日以内にアップロードを完成する必要があるかを表示します
};

class LifecycleRule {
public:
    LifecycleRule();

    void SetIsEnable(bool is_enable);
    void SetId(const std::string& id);
    void SetFilter(const LifecycleFilter& filter);
    void AddTransition(const LifecycleTransition& rh);
    void SetExpiration(const LifecycleExpiration& rh);
    void SetNonCurrTransition(const LifecycleNonCurrTransition& rh);
    void SetNonCurrExpiration(const LifecycleNonCurrExpiration& rh);
    void SetAbortIncompleteMultiUpload(const AbortIncompleteMultipartUpload& rh);

    bool IsEnable();
    std::string GetId();
    LifecycleFilter GetFilter();
    std::vector<LifecycleTransition> GetTransitions();
    LifecycleExpiration GetExpiration();
    LifecycleNonCurrTransition GetNonCurrTransition();
    LifecycleNonCurrExpiration GetNonCurrExpiration();
    AbortIncompleteMultipartUpload GetAbortIncompleteMultiUpload();

    bool HasIsEnable();
    bool HasId();
    bool HasFilter();
    bool HasExpiration();
    bool HasNonCurrTransition();
    bool HasNonCurrExpiration();
    bool HasAbortIncomMultiUpload();

private:
    bool m_is_enable; //規則が有効かどうか
    std::string m_id; //規則ID
    LifecycleFilter m_filter; //フィルタは、規則の有効なObject範囲を指定します
    std::vector<LifecycleTransition> m_transitions; //変換操作
    LifecycleExpiration m_expiration; //期限切れ操作
    LifecycleNonCurrTransition m_non_curr_transition; //現在バージョンでない場合の変換操作
    LifecycleNonCurrExpiration m_non_curr_expiration; //現在バージョンでない場合の期限切れ操作
    AbortIncompleteMultipartUpload m_abort_multi_upload; //マルチパートアップロードしながら運行する場合の最長時間を設定します
}
```

#### 例

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-123456789";

//PutBucketLifecycleReqの構造関数にbucket_name渡す必要があります
qcloud_cos::PutBucketLifecycleReq req(bucket_name);
//規則1の設定
{
    qcloud_cos::LifecycleRule rule;
    rule.SetIsEnable(true);
    rule.SetId("lifecycle_rule00");
    qcloud_cos::LifecycleFilter filter;
    filter.SetPrefix("sevenyou_e1");
    rule.SetFilter(filter);
    qcloud_cos::LifecycleExpiration expiration;
    expiration.SetDays(1);
    rule.SetExpiration(expiration);
    req.AddRule(rule);
}

//規則2の設定
{
    qcloud_cos::LifecycleRule rule;
    rule.SetIsEnable(true);
    rule.SetId("lifecycle_rule01");
    qcloud_cos::LifecycleFilter filter;
    filter.SetPrefix("sevenyou_e2");
    rule.SetFilter(filter);
    qcloud_cos::LifecycleExpiration expiration;
    expiration.SetDays(3);
    rule.SetExpiration(expiration);
    req.AddRule(rule);
}

qcloud_cos::PutBucketLifecycleResp resp;
qcloud_cos::CosResult result = cos.PutBucketLifecycle(req, &resp);

//呼び出しに成功した場合、respのメンバー関数を呼び出してレスポンス内容を取得します
if (result.IsSucc()) {
    // ...
} else {
    //ライフサイクルの設定に失敗した場合、CosResultのメンバー関数を呼び出してエラー情報、例えばrequestIDなどを出力することができます
} 
```

### Get Bucket Lifecycle

##### 機能説明

Get Bucket LifecycleでBucketのライフサイクル構成を照合できます。当該Bucketにはライフサイクル 規則が構成されていない場合、NoSuchLifecycleConfigurationが返却されます。関連APIドキュメントについては、[Get Bucket Lifecycle](/document/product/436/8278)を参照してください。

#### 方法のプロトタイプ

```cpp
CosResult GetBucketLifecycle(const GetBucketLifecycleReq& req, GetBucketLifecycleResp* resp);
```

#### パラメータ説明

| パラメータ | パラメータ説明                                                |
| ---- | ------------------------------------------------------- |
| req  | GetBucketLifecycleReq、GetBucketLifecycle操作のリクエスト。  |
| resp | GetBucketLifecycleResp、GetBucketLifecycle操作のレスポンス。 |

```
//LifecycleRulesの取得
std::vector<LifecycleRule> GetRules()
```

そのうち、LifecycleRuleの定義については、Put Bucket Lifecycleを参照してください。

#### 例

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-123456789";

//GetBucketLifecycleReqの構造関数にbucket_nameを渡す必要があります
qcloud_cos::GetBucketLifecycleReq req(bucket_name);
qcloud_cos::GetBucketLifecycleResp resp;
qcloud_cos::CosResult result = cos.GetBucketLifecycle(req, &resp);

//呼び出しに成功した場合、respのメンバー関数を呼び出してレスポンス内容を取得します
if (result.IsSucc()) {
    // ...
} else {
    //ライフサイクル構成の取得に失敗した場合、CosResultのメンバー関数を呼び出してエラー情報、例えばrequestIDなどを出力することができます
} 
```

### Delete Bucket Lifecycle

##### 機能説明

Delete Bucket LifecycleでBucketのライフサイクル構成を削除できます。当該Bucketにはライフサイクル規則が構成されていない場合、NoSuchLifecycleConfigurationが返却されます。関連APIドキュメントについては、[Delete Bucket Lifecycle](/document/product/436/8284)を参照してください。

#### 方法のプロトタイプ

```cpp
CosResult DeleteBucketLifecycle(const DeleteBucketLifecycleReq& req, DeleteBucketLifecycleResp* resp);
```

#### パラメータ説明

| パラメータ | パラメータ説明                                                     |
| ---- | ------------------------------------------------------------ |
| req  | DeleteBucketLifecycleReq、DeleteBucketLifecycle操作のリクエスト。 |
| resp | DeleteBucketLifecycleResp、DeleteBucketLifecycle操作のレスポンス。 |

#### 例

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-123456789";

//DeleteBucketLifecycleReqの構造関数にbucket_nameを渡す必要があります
qcloud_cos::DeleteBucketLifecycleReq req(bucket_name);
qcloud_cos::DeleteBucketLifecycleResp resp;
qcloud_cos::CosResult result = cos.DeleteBucketLifecycle(req, &resp);

//呼び出しに成功した場合、respのメンバー関数を呼び出してレスポンス内容を取得します
if (result.IsSucc()) {
    // ...
} else {
    //ライフサイクル構成の削除に失敗した場合、CosResultのメンバー関数を呼び出してエラー情報、例えばrequestIDなどを出力することができます
} 
```

### Put Bucket CORS

##### 機能説明

CPut Bucket CORS APIでBucketのクロスオリジンリソース共有権限の設定をリクエストできます。XMLフォーマットの構成ファイルで構成できます。ファイルのサイズ制限は64KBです。デフォルトでは、Bucketの所有者は当該APIを直接使用する権限を有し、またBucketの所有者はその権限をその他ユーザーに付与することができます。関連APIドキュメントにつては、[Put Bucket CORS](/document/product/436/8279)を参照してください。

#### 方法のプロトタイプ

```cpp
CosResult PutBucketCORS(const DPutBucketCORSReq& req, PutBucketCORSResp* resp);
```

#### パラメータ説明

| パラメータ | パラメータ説明                                      |
| ---- | --------------------------------------------- |
| req  | PutBucketCORSReq、PutBucketCORS操作のリクエスト。  |
| resp | PutBucketCORSResp、PutBucketCORS操作のレスポンス。 |

```
//CORSRuleの追加
void AddRule(const CORSRule& rule);

//CORSRuleの設定
void SetRules(const std::vector<CORSRule>& rules)


```

CORSRuleの定義を下記に示します：

```
struct CORSRule {
    std::string m_id; //構成規則のID、オプション
    std::string m_max_age_secs; //OPTIONSリクエストに得られた結果の有効期を設定します
    std::vector<std::string> m_allowed_headers; //OPTIONSリクエスト送信の際、サーバーに、次のリクエストにおいて使用可能なカスタマイズ HTTPリクエストヘッダーを伝えます。ワイルドカードに対応します*
    std::vector<std::string> m_allowed_methods; //許可されるHTTP操作、列挙値：GET、PUT、HEAD、POST、DELETE
    std::vector<std::string> m_allowed_origins; //許可されるアクセス元、ワイルドカードに対応し*、フォーマットは：プロトコル://ドメイン名[:ポート]例えば：http://www.qq.com
    std::vector<std::string> m_expose_headers;  //ブラウザの受信可能で、サーバーからのカスタマイズヘッダー情報を設定します
};


```

#### 例

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-123456789";

//PutBucketCORSReqの構造関数にbucket_nameを渡す必要があります
qcloud_cos::PutBucketCORSReq req(bucket_name);
qcloud_cos::CORSRule rule;
rule.m_id = "123";
rule.m_allowed_headers.push_back("x-cos-meta-test");
rule.m_allowed_origins.push_back("http://www.qq.com");
rule.m_allowed_origins.push_back("http://cloud.tentent.com");
rule.m_allowed_methods.push_back("PUT");
rule.m_allowed_methods.push_back("GET");
rule.m_max_age_secs = "600";
rule.m_expose_headers.push_back("x-cos-expose");
req.AddRule(rule);

qcloud_cos::PutBucketCORSResp resp;
qcloud_cos::CosResult result = cos.PutBucketCORS(req, &resp);

//呼び出しに成功した場合、respのメンバー関数を呼び出してレスポンス内容を取得します
if (result.IsSucc()) {
    // ...
} else {
    //ライフサイクルの設定に失敗した場合、CosResultのメンバー関数を呼び出してエラー情報、例えばrequestIDなどを出力することができます
} 
```

### Get Bucket CORS

##### 機能説明

Get Bucket CORS APIによりBucket所有者はBucketにおいてクロスオリジンリソース共有の情報構成を取得できます。CORSとは、クロスオリジンリリソース共有のことで、正式名称がCross-Origin Resource Sharingで、W3C基準です。デフォルトでは、Bucket所有者は当該APIを直接使用する権限があり、またBucket所有者はその権限をその他ユーザーに授与することもできます。関連APIドキュメントについては、[Get Bucket CORS](/document/product/436/8274)を参照してください。

#### 方法のプロトタイプ

```cpp
CosResult GetBucketCORS(const DGetBucketCORSReq& req, GetBucketCORSResp* resp);
```

#### パラメータ説明

| パラメータ | パラメータ説明                                      |
| ---- | --------------------------------------------- |
| req  | GetBucketCORSReq、GetBucketCORS操作のリクエスト。  |
| resp | GetBucketCORSResp、GetBucketCORS操作のレスポンス。 |

```
//CORSRulesを取得する場合、CORSRuleの定義については、Put Bucket CORSを参照してください
std::vector<CORSRule> GetCORSRules();

```

#### 例

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-123456789";

//GetBucketCORSReqの構造関数にbucket_nameを渡す必要があります
qcloud_cos::GetBucketCORSReq req(bucket_name);
qcloud_cos::GetBucketCORSResp resp;
qcloud_cos::CosResult result = cos.GetBucketCORS(req, &resp);

//呼び出しに成功した場合、respのメンバー関数を呼び出してレスポンス内容を取得します
if (result.IsSucc()) {
    // ...
} else {
    //ライフサイクル構成の取得に失敗した場合、CosResultのメンバー関数を呼び出してエラー情報、例えばrequestIDなどを出力することができます
} 
```

### Delete Bucket CORS

##### 機能説明

Delete Bucket CORSでBucketのライフサイクル構成を削除できます。当該Bucketにはライフサイクル規則が構成されていない場合、NoSuchCORSConfigurationが返却されます。関連APIドキュメントについては、[Delete Bucket CORS](/document/product/436/8283)を参照してください。

#### 方法のプロトタイプ

```cpp
CosResult DeleteBucketCORS(const DDeleteBucketCORSReq& req, DeleteBucketCORSResp* resp);
```

#### パラメータ説明

| パラメータ | パラメータ説明                                            |
| ---- | --------------------------------------------------- |
| req  | DeleteBucketCORSReq、DeleteBucketCORS操作のリクエスト。  |
| resp | DeleteBucketCORSResp、DeleteBucketCORS操作のレスポンス。 |

#### 例

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-123456789";

//DeleteBucketCORSReqの構造関数にbucket_nameを渡す必要があります
qcloud_cos::DeleteBucketCORSReq req(bucket_name);
qcloud_cos::DeleteBucketCORSResp resp;
qcloud_cos::CosResult result = cos.DeleteBucketCORS(req, &resp);

//呼び出しに成功した場合、respのメンバー関数を呼び出してレスポンス内容を取得します
if (result.IsSucc()) {
    // ...
} else {
    //ライフサイクル構成の削除に失敗した場合、CosResultのメンバー関数を呼び出してエラー情報、例えばrequestIDなどを出力することができます
} 
```

### Put Bucket ACL

##### 機能説明

Put Bucket ACL APIはBucketを書き込むためのACL（Access Control List）リストで、Header："x-cos-acl"、"x-cos-grant-read"、"x-cos-grant-write"、"x-cos-grant-full-control" でACL情報を渡し、あるいはBodyによりXMLフォーマットでACL情報を渡すことができます。関連APIドキュメントについては、[Put Bucket ACL](/document/product/436/7737)を参照してください。

#### 方法のプロトタイプ

```cpp
CosResult PutBucketACL(const DPutBucketACLReq& req, PutBucketACLResp* resp);
```

#### パラメータ説明

| パラメータ | パラメータ説明                                    |
| ---- | ------------------------------------------- |
| req  | PutBucketACLReq、PutBucketACL操作のリクエスト。  |
| resp | PutBucketACLResp、PutBucketACL操作のレスポンス。 |

```
//BucketのACL属性を定義する場合、有効値：private,public-read-write,public-read
// デフォルト値：private
void SetXCosAcl(const std::string& str);

//権限が付与された者に読み取り権限を付与します。フォーマット：x-cos-grant-read: id=" ",id=" "。
// サブアカウントに権限を付与する場合、id="qcs::cam::uin/<OwnerUin>!:uin/<SubUin>!"
//ルートアカウントに権限を付与する場合、id="qcs::cam::uin/<OwnerUin>!:uin/<OwnerUin>!"
void SetXCosGrantRead(const std::string& str);

//権限が付与された者に書き込み権限を付与します。フォーマット：x-cos-grant-write: id=" ",id=" "./
// サブアカウントに権限を付与する場合、id="qcs::cam::uin/<OwnerUin>!:uin/<SubUin>!"、
//ルートアカウントに権限を付与する場合、id="qcs::cam::uin/<OwnerUin>!:uin/<OwnerUin>!"
void SetXCosGrantWrite(const std::string& str);

//権限が付与された者に読み取りと書き込み権限を付与します。フォーマット：x-cos-grant-full-control: id=" ",id=" "。
// サブアカウントに権限を付与する場合、id="qcs::cam::uin/<OwnerUin>!:uin/<SubUin>!"、
//ルートアカウントに権限を付与する場合、id="qcs::cam::uin/<OwnerUin>!:uin/<OwnerUin>!"
void SetXCosGrantFullControl(const std::string& str);

//Bucket所有者ID
void SetOwner(const Owner& owner);

//授権対象者情報と権限情報の設定
void SetAccessControlList(const std::vector<Grant>& grants);

//単独Bucketの授権情報の追加
void AddAccessControlList(const Grant& grant);
        

```

>!SetXCosAcl/SetXCosGrantRead/SetXCosGrantWrite/SetXCosGrantFullControlこのタイプのAPIとSetAccessControlList/AddAccessControlListは同時に使用できません。前者はHTTP Headerの設定により実現され、一方、後者はBodyにXMLフォーマットの内容を加えることで実現されていますから。二者から1つのみ選ぶことです。SDK内部では優先的に第1類を使用します。

ACLRuleの定義を下記に示します：

```
struct Grantee {
    //typeタイプはRootAccountまたはSubAccountであってもよい
    //typeがRootAccountである場合、idのuinにアカウントIDを記入し、もしくはanyone（すべてのタイプのユーザーを指します）でuin/<OwnerUin>!と uin/<SubUin>!を代替することができます
    //typeがRootAccountである場合、uinはルートアカウントを意味し、Subaccountはサブアカウントを表します
    std::string m_type; 
    std::string m_id; // qcs::cam::uin/<OwnerUin>:uin/<SubUin>
    std::string m_display_name; //選択必須ではありません
    std::string m_uri;
};

struct Grant {
    Grantee m_grantee; //権限が付与された者リソース情報
    std::string m_perm; //権限が付与された者の権限情報を表示します。列挙値：READ、WRITE、FULL_CONTROL
};


```

#### 例

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-123456789";

//PutBucketACLReqの構造関数にbucket_nameを渡す必要があります
qcloud_cos::PutBucketACLReq req(bucket_name);
qcloud_cos::ACLRule rule;
rule.m_id = "123";
rule.m_allowed_headers.push_back("x-cos-meta-test");
rule.m_allowed_origins.push_back("http://www.qq.com");
rule.m_allowed_origins.push_back("http://cloud.tentent.com");
rule.m_allowed_methods.push_back("PUT");
rule.m_allowed_methods.push_back("GET");
rule.m_max_age_secs = "600";
rule.m_expose_headers.push_back("x-cos-expose");
req.AddRule(rule);

qcloud_cos::PutBucketACLResp resp;
qcloud_cos::CosResult result = cos.PutBucketACL(req, &resp);

//呼び出しに成功した場合、respのメンバー関数を呼び出してレスポンス内容を取得します
if (result.IsSucc()) {
    // ...
} else {
    //ACLを設定する場合、CosResultのメンバー関数を呼び出してエラー情報、例えばrequestIDなどを出力することができます
} 
```

### Get Bucket ACL

##### 機能説明

Get Bucket ACL APIでBucketのACL、即ちバケット（Bucket）のアクセス権限管理リストを取得できます。当該APIに対してBucket所有者にのみ操作権限があります。関連APIドキュメントについては、[Get Bucket ACL](/document/product/436/7733)を参照してください。

#### 方法のプロトタイプ

```cpp
CosResult GetBucketACL(const DGetBucketACLReq& req, GetBucketACLResp* resp);
```

#### パラメータ説明

| パラメータ | パラメータ説明                                    |
| ---- | ------------------------------------------- |
| req  | GetBucketACLReq、GetBucketACL操作のリクエスト。  |
| resp | GetBucketACLResp、GetBucketACL操作のレスポンス。 |

```
std::string GetOwnerID();
std::string GetOwnerDisplayName();
std::vector<Grant> GetAccessControlList();

```

#### 例

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-123456789";

//GetBucketACLReqの構造関数にbucket_nameを渡す必要があります
qcloud_cos::GetBucketACLReq req(bucket_name);
qcloud_cos::GetBucketACLResp resp;
qcloud_cos::CosResult result = cos.GetBucketACL(req, &resp);

//呼び出しに成功した場合、respのメンバー関数を呼び出してレスポンス内容を取得します
if (result.IsSucc()) {
    // ...
} else {
    //ACLの取得に失敗した場合、CosResultのメンバー関数を呼び出してエラー情報、例えばrequestIDなどを出力することができます
} 
```

## オブジェクト操作

object_nameとはオブジェクト鍵（Key）のことで、バケットにおけるオブジェクトの唯一の識別子です。例えば、オブジェクトのアクセスドメイン名bucket1-1250000000.Cos.ap-guangzhou.myqcloud.com/doc1/pic1.Jpgにおいて、オブジェクト鍵はdoc1/pic1.jpgです。

「オブジェクト鍵」の詳細については、[オブジェクト概要](https://cloud.tencent.com/document/product/436/13324)を参照してください。

### Get Object

##### 機能説明

Get Objectリクエストによりファイル（Object）をローカルあるいは指定ストリームにダウンロードできます。当該操作については、目標Objectにリード権限があり、あるいは目標Objectが全員にリード権限を開放する必要があります（パブリック読み取り）。

#### 方法のプロトタイプ

```cpp
//Objectをローカルファイルにダウンロードします
CosResult GetObject(const GetObjectByFileReq& req, GetObjectByFileResp* resp);

//Objectをストリームにダウンロードします
CosResult GetObject(const GetObjectByStreamReq& req, GetObjectByStreamResp* resp);

//Objectをローカルファイルにダウンロードします（マルチスレッド）
CosResult GetObject(const MultiGetObjectReq& req, MultiGetObjectResp* resp);
```

#### パラメータ説明

| パラメータ | パラメータ説明                                                     |
| ---- | ------------------------------------------------------------ |
| req  | GetObjectByFileReq/GetObjectByStreamReq/MultiGetObjectReq、GetObject操作のリクエスト。 |
| resp | GetObjectByFileResp/GetObjectByStreamResp/MultiGetObjectResp、GetObject操作のレスポンス。 |

メンバー関数を下記に示します：

```
//応答ヘッダーにおけるContent-Typeパラメータの設定
void SetResponseContentType(const std::string& str);

//応答ヘッダーにおけるContent-Languageパラメータの設定
void SetResponseContentLang(const std::string& str);

//応答ヘッダーにおけるContent-Expiresパラメータの設定
void SetResponseExpires(const std::string& str);

//応答ヘッダーにおけるCache-Controlパラメータの設定
void SetResponseCacheControl(const std::string& str);

//応答ヘッダーにおけるContent-Dispositionパラメータの設定
void SetResponseContentDisposition(const std::string& str);

//応答ヘッダーにおけるContent-Encodingパラメータの設定
void SetResponseContentEncoding(const std::string& str);

```

GetObjectRespは共通のヘッダーのメンバー関数を読み取る以外、以下のメンバー関数も提供します：

```C++
//Objectの最終変更時間を取得します。その文字列フォーマットはDateであり、例えば「Wed, 28 Oct 2014 20:30:00 GMT」
std::string GetLastModified();

//Object typeを取得します。これはObjectが追加でアップロードできるかどうかを表示します。列挙値：normalまたはAppendable
std::string GetXCosObjectType();

//Objectのストレージタイプを取得します。列挙値：STANDARD、STANDARD_IA
std::string GetXCosStorageClass();

//mapフォーマットで全てのカスタマイズmetaを返却します。mapのKeyはいずれも「x-cos-meta-」プレフィックスを含みません
std::map<std::string, std::string> GetXCosMetas();

//カスタマイズのmetaを取得します。パラメータはx-cos-meta-*における*であることができます
std::string GetXCosMeta(const std::string& key);

//Server側の暗号化によるアルゴリズムの取得
std::string GetXCosServerSideEncryption(); 
```

#### 例

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-123456789";
std::string object_name = "object_name";
std::string local_path = "/tmp/object_name";

//ローカルファイルにダウンロードします
{
    //requestに関して、appid、bucketname、objectおよびローカルのパスを提供する必要があります（ファイル名を含みます）
    qcloud_cos::GetObjectByFileReq req(bucket_name, object_name, local_path);
    qcloud_cos::GetObjectByFileResp resp;
    qcloud_cos::CosResult result = cos.GetObject(req, &resp);
    if (result.IsSucc()) {
        //ダウンロード成功の場合、GetObjectByFileRespのメンバー関数を呼び出せます
    } else {
        //ダウンロード失敗の場合、CosResultのメンバー関数を呼び出してエラー情報、例えばrequestIDなどを出力することができます
    }
}

//ストリームにダウンロードします
{
    //requestに関して、appid、bucketname、objectおよび出力ストリームを提供する必要があります
    std::ostringstream os;
    qcloud_cos::GetObjectByStreamReq req(bucket_name, object_name, os);
    qcloud_cos::GetObjectByStreamResp resp;
    qcloud_cos::CosResult result = cos.GetObject(req, &resp);
    if (result.IsSucc()) {
        //ダウンロードに成功した場合、GetObjectByStreamRespのメンバー関数を呼び出せます
    } else {
        //ダウンロード失敗の場合、CosResultのメンバー関数を呼び出してエラー情報、例えばrequestIDなどを出力することができます
    }
}

//マルチスレッドでファイルをローカルにダウンロードします
{
    //requestはappid、bucketname、objectおよびローカルのパスを提供する必要があります（ファイル名を含みます）
    qcloud_cos::MultiGetObjectReq req(bucket_name, object_name, local_path);
    qcloud_cos::MultiGetObjectResp resp;
    qcloud_cos::CosResult result = cos.GetObject(req, &resp);
    if (result.IsSucc()) {
        //ダウンロードに成功した場合、MultiGetObjectRespのメンバー関数を呼び出せます
    } else {
        //ダウンロード失敗の場合、CosResultのメンバー関数を呼び出してエラー情報、例えばrequestIDなどを出力することができます
    }
}
```

### Head Object

##### 機能説明

Head Objectリクエストは、対応するオブジェクトのメタデータを取り戻すことができ、Headの権限はGetの権限と一致します。

#### 方法のプロトタイプ

```cpp
CosResult HeadObject(const HeadObjectReq& req, HeadObjectResp* resp);
```

#### パラメータ説明

| パラメータ | パラメータ説明                                |
| ---- | --------------------------------------- |
| req  | HeadObjectReq、HeadObject操作のリクエスト。  |
| resp | HeadObjectResp、HeadObject操作のレスポンス。 |

HeadObjectRespは共通のヘッダーのメンバー関数を読み取る以外、以下のメンバー関数も提供します：

```C++
std::string GetXCosObjectType();

std::string GetXCosStorageClass();

//カスタマイズのmetaを取得します。パラメータはx-cos-meta-*における*であることができます
std::string GetXCosMeta(const std::string& key);

//mapフォーマットで全てのカスタマイズmetaを返却します。mapのKeyはいずれも「x-cos-meta-」プレフィックスを含みません
std::map<std::string, std::string> GetXCosMetas();

//Server側の暗号化によるアルゴリズムの取得
std::string GetXCosServerSideEncryption(); 
```

#### 例

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-123456789";
std::string object_name = "object_name";
qcloud_cos::HeadObjectReq req(bucket_name, object_name);
qcloud_cos::HeadObjectResp resp;
qcloud_cos::CosResult result = cos.HeadObject(req, &resp);
if (result.IsSucc()) {
    //ダウンロードに成功した場合、HeadObjectRespのメンバー関数を呼び出せます
} else {
    //ダウンロード失敗の場合、CosResultのメンバー関数を呼び出してエラー情報、例えばrequestIDなどを出力することができます
}
```

### Put Object

##### 機能説明

Put Objectリクエストは1つのファイル（Object）を指定のBucketにアップロードできます。

- アップロードにおいてデフォルトでファイルに対してMD5チェックを行います（アップロードしないMD5チェックサンプルコードを参照してください）
- 現在のアクセスポリシーのエントリは1000条に限られており、オブジェクトACL管理が不要な場合、アップロードする前に設定しないでください。デフォルトでBucket権限を受け継ぎます。

#### 方法のプロトタイプ

```cpp
/// Streamを通じてアップロードします
CosResult PutObject(const PutObjectByStreamReq& req, PutObjectByStreamResp* resp);

/// ローカルファイルをアップロードします
CosResult PutObject(const PutObjectByFileReq& req, PutObjectByFileResp* resp);
```

#### パラメータ説明

| パラメータ | パラメータ説明                                                     |
| ---- | ------------------------------------------------------------ |
| req  | PutObjectByStreamReq/PutObjectByFileReq、PutObject操作のリクエスト。 |
| resp | PutObjectByStreamResp/PutObjectByFileResp、PutObject操作のレスポンス。 |

パラメータReqは下記に示すメンバー関数を含みます：

```C++
//Cache-Control RFC 2616において定義されるキャッシュメモリポリシーは、Objectのメタデータとして保存されます
void SetCacheControl(const std::string& str);

//Content-Disposition RFC 2616において定義されるファイル名は、Objectのメタデータとして保存されます
void SetContentDisposition(const std::string& str);

//Content-Encoding RFC 2616において定義されるエンコーディングフォーマットは、Objectのメタデータとして保存されます-
void SetContentEncoding(const std::string& str);

//Content-Type RFC 2616において定義される内容タイプ（MIME）は、Objectのメタデータとして保存されます
void SetContentType(const std::string& str);

//Expectについては、Expect:100-continueを使用する場合、サーバーの確認を受信してから、はじめてリクエスト内容を送信します
void SetExpect(const std::string& str);

//Expires RFC 2616において定義される期限切れ時間は、Objectのメタデータとして保存されます
void SetExpires(const std::string& str);

//ユーザーカスタマイズ可能なヘッダー情報は、Objectのメタデータとして返却されます。サイズは2Kに限られます
void SetXCosMeta(const std::string& key, const std::string& value);

//x-cos-storage-classでObjectのストレージレベルを設定します。列挙値：STANDARD,STANDARD_IA
// デフォルト値：STANDARD（現在、華南パークにのみ対応します）
void SetXCosStorageClass(const std::string& storage_class);

//ObjectのACL属性を定義する場合、有効値：private,public-read-write,public-read
// デフォルト値：private
void SetXcosAcl(const std::string& str);

//権限が付与された者に読み取り権限を付与します。フォーマット：x-cos-grant-read: id=" ",id=" "。
// サブアカウントに権限を付与する場合、id="qcs::cam::uin/<OwnerUin>!:uin/<SubUin>!"
//ルートアカウントに権限を付与する場合、id="qcs::cam::uin/<OwnerUin>!:uin/<OwnerUin>!"
void SetXcosGrantRead(const std::string& str);

//権限が付与された者に書き込み権限を付与します。フォーマット：x-cos-grant-write: id=" ",id=" "./
// サブアカウントに権限を付与する場合、id="qcs::cam::uin/<OwnerUin>!:uin/<SubUin>!"、
//ルートアカウントに権限を付与する場合、id="qcs::cam::uin/<OwnerUin>!:uin/<OwnerUin>!"
void SetXcosGrantWrite(const std::string& str);

//権限が付与された者に読み取りと書き込み権限を付与します。フォーマット：x-cos-grant-full-control: id=" ",id=" "。
// サブアカウントに権限を付与する場合、id="qcs::cam::uin/<OwnerUin>!:uin/<SubUin>!"、
//ルートアカウントに権限を付与する場合、id="qcs::cam::uin/<OwnerUin>!:uin/<OwnerUin>!"
void SetXcosGrantFullControl(const std::string& str);

/// Server側の暗号化によるアルゴリズムを設定します。現在、AES256に対応しています
void SetXCosServerSideEncryption(const std::string& str);
```

パラメータRespは下記に示すメンバー関数を含みます：

```C++
/// Objectのバージョン番号を取得します。Bucketにはマルチバージョンがない場合、空白文字列が返却されます
std::string GetVersionId();

/// Server側の暗号化によるアルゴリズム
std::string GetXCosServerSideEncryption();
```

#### 例

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-123456789";
std::string object_name = "object_name";

//簡単アップロード(ストリーム)
{
    std::istringstream iss("put object");
    //requestの構造関数にistreamを渡す必要があります
    qcloud_cos::PutObjectByStreamReq req(bucket_name, object_name, iss);
    //Setメソッドを呼び出してメタデータまたはACLなどを設定します
    req.SetXCosStorageClass("STANDARD_IA");
    //MD5チェックをオフにし、req.TurnOnComputeConentMd5()をオンにします。デフォルトではオンにされています
    req.TurnOffComputeConentMd5();
    qcloud_cos::PutObjectByStreamResp resp;
    qcloud_cos::CosResult result = cos.PutObject(req, &resp);
    
    if (result.IsSucc()) {
        //呼び出しに成功した場合、respのメンバー関数を呼び出してレスポンス内容を取得します
        do sth
    } else {
        //呼び出し失敗の場合、resultのメンバー関数を呼び出してエラー情報を取得できます
        std::cout << "ErrorInfo=" << result.GetErrorInfo() << std::endl;
        std::cout << "HttpStatus=" << result.GetHttpStatus() << std::endl;
        std::cout << "ErrorCode=" << result.GetErrorCode() << std::endl;
        std::cout << "ErrorMsg=" << result.GetErrorMsg() << std::endl;
        std::cout << "ResourceAddr=" << result.GetResourceAddr() << std::endl;
        std::cout << "XCosRequestId=" << result.GetXCosRequestId() << std::endl;
        std::cout << "XCosTraceId=" << result.GetXCosTraceId() << std::endl;
     }
}

//簡単アップロード(ファイル)
{
    //requestの構造関数にローカルファイルのパスを入力する必要があります
    qcloud_cos::PutObjectByFileReq req(bucket_name, object_name, "/path/to/local/file");
    //Setメソッドを呼び出してメタデータまたはACLなどを設定します
    req.SetXCosStorageClass("STANDARD_IA");
    //MD5チェックをオフにし、req.TurnOnComputeConentMd5()をオンにします。デフォルトではオンにされています
    req.TurnOffComputeConentMd5();
    qcloud_cos::PutObjectByFileResp resp;
    qcloud_cos::CosResult result = cos.PutObject(req, &resp);
        if (result.IsSucc()) {
        //呼び出しに成功した場合、respのメンバー関数を呼び出してレスポンス内容を取得します
        do sth
    } else {
        //呼び出し失敗の場合、resultのメンバー関数を呼び出してエラー情報を取得できます
        std::cout << "ErrorInfo=" << result.GetErrorInfo() << std::endl;
        std::cout << "HttpStatus=" << result.GetHttpStatus() << std::endl;
        std::cout << "ErrorCode=" << result.GetErrorCode() << std::endl;
        std::cout << "ErrorMsg=" << result.GetErrorMsg() << std::endl;
        std::cout << "ResourceAddr=" << result.GetResourceAddr() << std::endl;
        std::cout << "XCosRequestId=" << result.GetXCosRequestId() << std::endl;
        std::cout << "XCosTraceId=" << result.GetXCosTraceId() << std::endl;
     }
}
```

### Delete Object

##### 機能説明

Delete Object APIリクエストでCOSのBucketにおいてファイル（Object）を削除できます。当該操作については、リクエスターはBucketに対してWRITE権限を持たなければなりません。関連APIドキュメントについては[Delete Object](/document/product/436/7743)を参照してください。

#### 方法のプロトタイプ

```cpp
CosResult DeleteObject(const DeleteObjectReq& req, DeleteObjectResp* resp);
```

#### パラメータ説明

| パラメータ | パラメータ説明                                   |
| ---- | ------------------------------------------ |
| req  | DeleteObjectReq、DeleteObject操作のリクエスト。 |
| resp | DeletObjectResp、DeletObject操作のレスポンス。  |

#### 例

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-123456789";
std::string object_name = "test_object";

qcloud_cos::DeleteObjectReq req(bucket_name, object_name);
qcloud_cos::DeleteObjectResp resp;
qcloud_cos::CosResult result = cos.DeleteObject(req, &resp);

//呼び出しに成功した場合、respのメンバー関数を呼び出してレスポンス内容を取得します
if (result.IsSucc()) {
    // ...
} else {
    //Objectの削除失敗の場合、CosResultのメンバー関数を呼び出してエラー情報、例えばrequestIDなどを出力することができます
} 
```

## マルチパートアップロード操作

### Initiate Multipart Upload

##### 機能説明

Initiate Multipart Uploadリクエストは、シャードアップロードの初期化を実現します。このリクエストを実行した後にUpload IDを返します。今後のUpload Partリクエストに使用されます。

#### 方法のプロトタイプ

```cpp
CosResult InitMultiUpload(const InitMultiUploadReq& req, InitMultiUploadResp* resp);
```

#### パラメータ説明

| パラメータ | パラメータ説明                                          |
| ---- | ------------------------------------------------- |
| req  | InitMultiUploadReq、InitMultiUpload操作のリクエスト。  |
| resp | InitMultiUploadResp、InitMultiUpload操作のレスポンス。 |

InitMultiUploadReqのメンバー関数を下記に示します：

```
//Cache-Control RFC 2616において定義されるキャッシュメモリポリシーは、Objectのメタデータとして保存されます
void SetCacheControl(const std::string& str);

//Content-Disposition RFC 2616において定義されるファイル名は、Objectのメタデータとして保存されます
void SetContentDisposition(const std::string& str);

//Content-Encoding RFC 2616において定義されるエンコーディングフォーマットは、Objectのメタデータとして保存されます-
void SetContentEncoding(const std::string& str);

//Content-Type RFC 2616において定義される内容タイプ（MIME）は、Objectのメタデータとして保存されます
void SetContentType(const std::string& str);

//Expires RFC 2616において定義される期限切れ時間は、Objectのメタデータとして保存されます
void SetExpires(const std::string& str);

//ユーザーカスタマイズ可能なヘッダー情報は、Objectのメタデータとして返却されます。サイズは2Kに限られます
void SetXCosMeta(const std::string& key, const std::string& value);

//x-cos-storage-classでObjectのストレージレベルを設定します。列挙値：STANDARD,STANDARD_IA
// デフォルト値：STANDARD
void SetXCosStorageClass(const std::string& storage_class);

//ObjectのACL属性を定義する場合、有効値：private,public-read-write,public-read
// デフォルト値：private
void SetXcosAcl(const std::string& str);

//権限が付与された者に読み取り権限を付与します。フォーマット：x-cos-grant-read: id=" ",id=" "。
// サブアカウントに権限を付与する場合、id="qcs::cam::uin/<OwnerUin>!:uin/<SubUin>!"
//ルートアカウントに権限を付与する場合、id="qcs::cam::uin/<OwnerUin>!:uin/<OwnerUin>!"
void SetXcosGrantRead(const std::string& str);

//権限が付与された者に書き込み権限を付与します。フォーマット：x-cos-grant-write: id=" ",id=" "./
// サブアカウントに権限を付与する場合、id="qcs::cam::uin/<OwnerUin>!:uin/<SubUin>!"、
//ルートアカウントに権限を付与する場合、id="qcs::cam::uin/<OwnerUin>!:uin/<OwnerUin>!"
void SetXcosGrantWrite(const std::string& str);

//権限が付与された者に読み取りと書き込み権限を付与します。フォーマット：x-cos-grant-full-control: id=" ",id=" "。
// サブアカウントに権限を付与する場合、id="qcs::cam::uin/<OwnerUin>!:uin/<SubUin>!"、
//ルートアカウントに権限を付与する場合、id="qcs::cam::uin/<OwnerUin>!:uin/<OwnerUin>!"
void SetXcosGrantFullControl(const std::string& str);

/// Server側の暗号化によるアルゴリズムを設定します。現在、AES256に対応しています
void SetXCosServerSideEncryption(const std::string& str);

```

このリクエストの実行ができたら、返却されるresponseはbucket、Key、uploadIdを含み、それぞれマルチパートアップロードの目標Bucket、Objectの名称および次のマルチパートアップロードに必要な番号を表します。

InitMultiUploadRespのメンバー関数を下記に示します：

```C++
std::string GetBucket();
std::string GetKey();
std::string GetUploadId();

//Server側の暗号化によるアルゴリズム
std::string GetXCosServerSideEncryption();
```

#### 例

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "cpp_sdk_v5-123456789";
std::string object_name = "object_name";

qcloud_cos::InitMultiUploadReq req(bucket_name, object_name);
qcloud_cos::InitMultiUploadResp resp;
qcloud_cos::CosResult result = cos.InitMultiUpload(req, &resp);

std::string upload_id = "";
if (result.IsSucc()) {
    upload_id = resp.GetUploadId();
}
```

### Upload Part

##### 機能説明

Upload Partリクエストは、初期化後のマルチパートアップロードを実行し、サポートされるパート数は1から10000までであり、パートのサイズは1MBから5GBまでです。Upload Partをリクエストするたびに、partNumberとuploadIDを運ぶ必要があり、partNumberはパートの番号であり、アウトオブオーダアップロードをサポートします。

> Tips:アップロードにおいてデフォルトでファイルに対してMD5チェックを行います（アップロードしないMD5チェックサンプルコードを参照してください）

#### 方法のプロトタイプ

```cpp
CosResult UploadPartData(const UploadPartDataReq& request, UploadPartDataResp* response);
```

#### パラメータ説明

| パラメータ | パラメータ説明                                        |
| ---- | ----------------------------------------------- |
| req  | UploadPartDataReq、UploadPartData操作のリクエスト。  |
| resp | UploadPartDataResp、UploadPartData操作のレスポンス。 |

UploadPartDataReqの構造にあたって、リクエストするAPPID、Bucket、Object、初期化できて取得したUploadId、およびアップロードしたデータストリームを表示する必要があります（呼び出しが終わったら、ストリームについては、呼び出し側は自らオフにしなければなりません）。

```
UploadPartDataReq(const std::string& bucket_name,
                    const std::string& object_name, const std::string& upload_id,
                    std::istream& in_stream);

```

更に、リクエストにあたって、パート番号を設定する必要もあります。当該パートはパートのアップロード完了後も使われます。

```
void SetPartNumber(uint64_t part_number);

```

UploadPartDataRespのメンバー関数を下記に示します：

```
/// Server側の暗号化によるアルゴリズム
std::string GetXCosServerSideEncryption();

```

#### 例

```cpp
//第1パートのアップロード
{
    std::fstream is("demo_5M.part1");
    qcloud_cos::UploadPartDataReq req(bucket_name, object_name,
                                      upload_id, is);
    req.SetPartNumber(1);
    //MD5チェックをオフにし、req.TurnOnComputeConentMd5()をオンにします。デフォルトではオンにされています
    req.TurnOffComputeConentMd5();
    qcloud_cos::UploadPartDataResp resp;
    qcloud_cos::CosResult result = cos.UploadPartData(req, &resp);

    //アップロードができたら、パート番号および返却されるETagを記録する必要があります
    if (result.IsSucc()) {
        etags.push_back(resp.GetEtag());
        part_numbers.push_back(1);
    }
    is.close();
}

//第2パートのアップロード
{
    std::fstream is("demo_5M.part2");
    qcloud_cos::UploadPartDataReq req(bucket_name, object_name,
                                      upload_id, is);
    req.SetPartNumber(2);
    qcloud_cos::UploadPartDataResp resp;
    qcloud_cos::CosResult result = cos.UploadPartData(req, &resp);

    //アップロードができたら、パート番号および返却されるETagを記録する必要があります 
    if (result.IsSucc()) {
        etags.push_back(resp.GetEtag());
        part_numbers.push_back(2);
    }
    is.close();
}
```

### Complete Multipart Upload

##### 機能説明

Complete Multipart Uploadは、全体のマルチパートアップロードを完了するために使用されます。Upload Partsを使用してすべてのパートをアップロードした後、このAPIでアップロードを完了できます。このAPIを使用するとき、パートの正確さを検証するために、ボディの各パートにPartNumberとETagを指定する必要があります。

#### 方法のプロトタイプ

```cpp
CosResult CompleteMultiUpload(const CompleteMultiUploadReq& request, CompleteMultiUploadResp* response);
```

#### パラメータ説明

| パラメータ | パラメータ説明                                                  |
| ---- | --------------------------------------------------------- |
| req  | CompleteMultiUploadReq、CompleteMultiUpload操作のリクエスト。  |
| resp | CompleteMultiUploadResp、CompleteMultiUpload操作のレスポンス。 |

CompleteMultiUploadReqの構造にあたって、リクエストするAPPID、Bucket、Object、初期化できて取得したUploadIdを表示する必要があります。

```
CompleteMultiUploadReq(const std::string& bucket_name,
                       const std::string& object_name, const std::string& upload_id)

```

また、requestについては、アップロードしたすべてのパート番号とETagを設定する必要があります。

```
//下記の方法を呼び出す場合、番号とETagの順序が必ず一対一対応するように確保しなければなりません
void SetPartNumbers(const std::vector<uint64_t>& part_numbers);
void SetEtags(const std::vector<std::string>& etags) ;

//part_numberとETagペアの追加
void AddPartEtagPair(uint64_t part_number, const std::string& etag);

/// Server側の暗号化によるアルゴリズムを設定します。現在、AES256に対応しています
void SetXCosServerSideEncryption(const std::string& str);

```

CompleteMultiUploadRespの返却内容はLocation、Bucket、Key、ETagを含み、作成したObjectがパブリックネットワークへアクセスする場合のドメイン名、マルチパートアップロードした目標Bucket、Objectの名称、マージ後のファイルのMD5アルゴリズムチェック値をそれぞれ意味します。下記のメンバー関数を呼び出すことでresponseにおける内容にアクセスできます。

```
std::string GetLocation();
std::string GetKey();
std::string GetBucket();
std::string GetEtag();

/// Server側の暗号化によるアルゴリズム
std::string GetXCosServerSideEncryption();

```

#### 例

```cpp
qcloud_cos::CompleteMultiUploadReq req(bucket_name, object_name, upload_id);
qcloud_cos::CompleteMultiUploadResp resp;
req.SetEtags(etags);
req.SetPartNumbers(part_numbers);

qcloud_cos::CosResult result = cos.CompleteMultiUpload(req, &resp);
```

### Multipart Upload

##### 機能説明

Multipart Uploadはマルチパートアップロードの初期化、マルチパートアップロード、マルチパートアップロードの完成という3つのステップをカプセル化しています。リクエストにおいてアップロードするファイルを表示するのみで良いです。

#### 方法のプロトタイプ

```cpp
CosResult MultiUploadObject(const MultiUploadObjectReq& request,        MultiUploadObjectResp* response);
```

#### パラメータ説明

| パラメータ | パラメータ説明                                              |
| ---- | ----------------------------------------------------- |
| req  | MultiUploadObjectReq、MultiUploadObject操作のリクエスト。  |
| resp | MultiUploadObjectResp、MultiUploadObject操作のレスポンス。 |

MultiUploadObjectReqの構造にあたって、Bucket、Objectおよびアップロード待ちのファイルのローカルパスを表示しなければなりません。ローカルパスを表示しない場合、デフォルトでは既存のワーキングパスにおけるObjectと同名であるファイルとなります。

```
MultiUploadObjectReq(const std::string& bucket_name,
                     const std::string& object_name, const std::string& local_file_path = "");

/// Server側の暗号化によるアルゴリズムを設定します。現在、AES256に対応しています
void SetXCosServerSideEncryption(const std::string& str);

```

- マルチパートアップロードができたら、当該Responseの返し内容はCompleteMultiUploadRespと一致します。
- マルチパートアップロードに失敗した場合、当該Responseがその実状に応じて返す内容はInitMultiUploadResp、UploadPartDataResp、CompleteMultiUploadRespと一致します。`GetRespTag()`を呼び出すことでどのステップで失敗したかを特定できます。

```
//Init、Upload、Completeが返されます
std::string GetRespTag();

/// Server側の暗号化によるアルゴリズム
std::string GetXCosServerSideEncryption();

```

#### 例

```cpp
qcloud_cos::MultiUploadObjectReq req( bucket_name, object_name, "/temp/demo_6G.tmp");
qcloud_cos::MultiUploadObjectResp resp;
qcloud_cos::CosResult result = cos.MultiUploadObject(req, &resp);

if (result.IsSucc()) {
    std::cout << resp.GetLocation() << std::endl;
    std::cout << resp.GetKey() << std::endl;
    std::cout << resp.GetBucket() << std::endl;
    std::cout << resp.GetEtag() << std::endl;
} else {
    //具体的にどのステップで失敗したかを取得します
    std::string resp_tag = resp.GetRespTag();
    if ("Init" == resp_tag) {
        //print result
    } else if ("Upload" == resp_tag) {
        //print result
    } else if ("Complete" == resp_tag) {
        //print result
    }
}
```

### Abort Multipart Upload

##### 機能説明

Abort Multipart Uploadは、1つのマルチパートアップロードを破棄し、アップロードされたパートを削除するために使用されます。このAbort Multipart Uploadを呼び出すとき、このUpload Partsを使用しているリクエストがあると、Upload Partsは失敗を返します。

#### 方法のプロトタイプ

```cpp
CosResult AbortMultiUpload(const AbortMultiUploadReq& request, AbortMultiUploadResp* response);
```

#### パラメータ説明

| パラメータ | パラメータ説明                                            |
| ---- | --------------------------------------------------- |
| req  | AbortMultiUploadReq、AbortMultiUpload操作のリクエスト。  |
| resp | AbortMultiUploadResp、AbortMultiUpload操作のレスポンス。 |

AbortMultiUploadReqの構造にあたって、Bucket、ObjectおよびUpload_idを表示する必要があります。

```C++
AbortMultiUploadReq(const std::string& bucket_name,
                    const std::string& object_name, const std::string& upload_id);
```

特殊な方法がない場合、BaseRespのメンバー関数を呼び出すことで共通のヘッダーの内容を取得できます。

#### 例

```cpp
qcloud_cos::AbortMultiUploadReq req(bucket_name, object_name,
                                                    upload_id);
qcloud_cos::AbortMultiUploadResp resp;
qcloud_cos::CosResult result = cos.AbortMultiUpload(req, &resp);
```

### List Parts

##### 機能説明

List Partsで特定のマルチパートアップロードにおけるアップロード済みのパートを照合できます。即ち指定されたUploadIdの所属するすべてのアップロード済みのパートをリストすることです。関連APIドキュメントについては、[List Parts](/document/product/436/7747)を参照してください。

#### 方法のプロトタイプ

```cpp
CosResult ListParts(const ListPartsReq& req, ListPartsResp* resp);
```

#### パラメータ説明

| パラメータ | パラメータ説明                              |
| ---- | ------------------------------------- |
| req  | ListPartsReq、ListParts操作のリクエスト。  |
| resp | ListPartsResp、ListParts操作のレスポンス。 |

```
//構造関数、Bucket名、Object名、マルチパートアップロードしたID
ListPartsReq(const std::string& bucket_name,                                                                                                                                      
             const std::string& object_name,
             const std::string& upload_id); 

//\brief戻り値のエンコーディング方式を指定します
void SetEncodingType(const std::string& encoding_type);

//\briefレスポンスごとの最大エントリ数。設定しない場合、デフォルト値は1000です
void SetMaxParts(uint64_t max_parts);

//\briefデフォルトではUTF-8二進法の順でエントリをリストします。リストされるすべてのエントリはmarkerから始まります
void SetPartNumberMarker(const std::string& part_number_marker);

```

```
//マルチパートアップロードの目標Bucket
std::string GetBucket();

//戻り値のエンコーディング方式の規定
std::string GetEncodingType();

//Objectの名称
std::string GetKey();

//今回マルチパートアップロードするIDを識別します
std::string GetUploadId();

//今回アップロード発起人の情報を表示するために使用されます
Initiator GetInitiator();

//これらのパート所有者の情報を表示するために使用されます
Owner GetOwner();

//デフォルトではUTF-8二進法の順でエントリをリストします。リストされるすべてのエントリはmarkerから始まります
uint64_t GetPartNumberMarker();

//それぞれのパートの情報を返す
std::vector<Part> GetParts();

//返されたエントリが切り捨てられた場合、返されたNextMarkerは次のエントリの起点となります
uint64_t GetNextPartNumberMarker();

//これらのパートのストレージレベルを表示するために使用されます。列挙値：Standard、Standard_IA
std::string GetStorageClass();

//一度に返されるエントリーの最大数
uint64_t GetMaxParts();

//返されたエントリが切り捨てられたか。ブール値：TRUE、FALSE
bool IsTruncated();

```

そのうち、Part、Owner、Initiatorの定義を下記に示します：

```
struct Initiator {
    std::string m_id; //作成者の唯一の識別子
    std::string m_display_name; //作成者のユーザー名の説明
};

struct Owner {
    std::string m_id; //ユーザーの唯一の識別子
    std::string m_display_name; //ユーザー名の説明
};

struct Part {
    uint64_t m_part_num; //パートの番号
    uint64_t m_size; //パートのサイズ、単位はByteです
    std::string m_etag; //ObjectパートのMD5アルゴリズムチェック値
    std::string m_last_modified; //パートの最終変更時間
};

```

#### 例

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-123456789";
std::string object_name = "test_object";

//uploadIdは、InitMultiUploadを呼び出すことで取得できます
qcloud_cos::ListPartsReq req(bucket_name, object_name, upload_id);
req.SetMaxParts(1);                                                                                                                                                               
req.SetPartNumberMarker("1");
qcloud_cos::ListPartsResp resp;
qcloud_cos::CosResult result = cos.ListParts(req, &resp);

//呼び出しに成功した場合、respのメンバー関数を呼び出してレスポンス内容を取得します
if (result.IsSucc()) {
    // ...
} else {
    //Objectの削除失敗の場合、CosResultのメンバー関数を呼び出してエラー情報、例えばrequestIDなどを出力することができます
} 
```

### Put Object ACL

##### 機能説明

Put Object ACL APIはObjectを書き込むためのACL表で、 Header："x-cos-acl"、"x-cos-grant-read"、"x-cos-grant-write"、"x-cos-grant-full-control"でACL情報を渡し、あるいはBodyによりXMLフォーマットでACL情報を渡すことができます。関連APIドキュメントについては、[Put Object ACL](/document/product/436/7748)を参照してください。

>!現在のアクセスポリシーのエントリは1000条に限られており、オブジェクトACL管理が不要な場合、設定しないでください。デフォルトでBucket権限を受け継ぎます。

#### 方法のプロトタイプ

```cpp
CosResult PutObjectACL(const PutObjectACLReq& req, PutObjectACLResp* resp);
```

#### パラメータ説明

| パラメータ | パラメータ説明                                    |
| ---- | ------------------------------------------- |
| req  | PutObjectACLReq、PutObjectACL操作のリクエスト。  |
| resp | PutObjectACLResp、PutObjectACL操作のレスポンス。 |

```
//ObjectのACL属性を定義する場合、有効値：private,public-read-write,public-read
// デフォルト値：private
void SetXCosAcl(const std::string& str);

//権限が付与された者に読み取り権限を付与します。フォーマット：x-cos-grant-read: id=" ",id=" "。
// サブアカウントに権限を付与する場合、id="qcs::cam::uin/<OwnerUin>!:uin/<SubUin>!"
//ルートアカウントに権限を付与する場合、id="qcs::cam::uin/<OwnerUin>!:uin/<OwnerUin>!"
void SetXCosGrantRead(const std::string& str);

//権限が付与された者に書き込み権限を付与します。フォーマット：x-cos-grant-write: id=" ",id=" "./
// サブアカウントに権限を付与する場合、id="qcs::cam::uin/<OwnerUin>!:uin/<SubUin>!"、
//ルートアカウントに権限を付与する場合、id="qcs::cam::uin/<OwnerUin>!:uin/<OwnerUin>!"
void SetXCosGrantWrite(const std::string& str);

//権限が付与された者に読み取りと書き込み権限を付与します。フォーマット：x-cos-grant-full-control: id=" ",id=" "。
// サブアカウントに権限を付与する場合、id="qcs::cam::uin/<OwnerUin>!:uin/<SubUin>!"、
//ルートアカウントに権限を付与する場合、id="qcs::cam::uin/<OwnerUin>!:uin/<OwnerUin>!"
void SetXCosGrantFullControl(const std::string& str);

//Object所有者ID
void SetOwner(const Owner& owner);

//授権対象者情報と権限情報の設定
void SetAccessControlList(const std::vector<Grant>& grants);

//単独Objectの権限を付与する情報の追加
void AddAccessControlList(const Grant& grant);
        

```

>!SetXCosAcl/SetXCosGrantRead/SetXCosGrantWrite/SetXCosGrantFullControlこのタイプのAPIとSetAccessControlList/AddAccessControlListは同時に使用できません。前者はHTTP Headerの設定により実現され、一方、後者はBodyにXMLフォーマットの内容を加えることで実現されていますから。二者から1つのみ選ぶことです。SDK内部では優先的に第1類を使用します。

ACLRuleの定義を下記に示します：

```
struct Grantee {
    //typeタイプはRootAccountまたはSubAccountであってもよい
    //typeがRootAccountである場合、idのuinにアカウントIDを記入し、もしくはanyone（すべてのタイプのユーザーを指します）でuin/<OwnerUin>!と uin/<SubUin>!を代替することができます
    //typeがRootAccountである場合、uinはルートアカウントを意味し、Subaccountはサブアカウントを表します
    std::string m_type; 
    std::string m_id; // qcs::cam::uin/<OwnerUin>:uin/<SubUin>
    std::string m_display_name; //選択必須ではありません
    std::string m_uri;
};

struct Grant {
    Grantee m_grantee; //権限が付与された者リソース情報
    std::string m_perm; //権限が付与された者の権限情報を表示します。列挙値：READ、WRITE、FULL_CONTROL
};


```

#### 例

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-123456789";
std::string object_name = "sevenyou";

//1 ACL構成を設定します（Bodyを通じます。ACLの設定に関してBodyとHeaderの２つの方式があるが、二者から1つのみ選ぶことです。さもなければ競合が発生します）
{   
    qcloud_cos::PutObjectACLReq req(bucket_name, object_name);
    qcloud_cos::Owner owner = {"qcs::cam::uin/xxxxx:uin/xxx", "qcs::cam::uin/xxxxxx:uin/xxxxx" };
    qcloud_cos::Grant grant;
    req.SetOwner(owner);
    grant.m_grantee.m_type = "Group";
    grant.m_grantee.m_uri = "http://cam.qcloud.com/groups/global/AllUsers";
    grant.m_perm = "READ";
    req.AddAccessControlList(grant);

    qcloud_cos::PutObjectACLResp resp;
    qcloud_cos::CosResult result = cos.PutObjectACL(req, &resp);
    //呼び出しに成功した場合、respのメンバー関数を呼び出してレスポンス内容を取得します
    if (result.IsSucc()) {
        // ...
    } else {
        //ACLの設定に関して、CosResultのメンバー関数を呼び出してエラー情報、例えばrequestIDなどを出力することができます
    } 
}   

//2 ACL構成を設定します（Headerを通じます。ACLの設定に関してBodyとHeaderの2つの方式があるが、二者から1つのみ選ぶことです。さもなければ競合が発生します）
{   
    qcloud_cos::PutObjectACLReq req(bucket_name, object_name);                                                                                                                    
    req.SetXCosAcl("public-read-write");

    qcloud_cos::PutObjectACLResp resp;
    qcloud_cos::CosResult result = cos.PutObjectACL(req, &resp);
    //呼び出しに成功した場合、respのメンバー関数を呼び出してレスポンス内容を取得します
    if (result.IsSucc()) {
        // ...
    } else {
        //ACLの設定に関して、CosResultのメンバー関数を呼び出してエラー情報、例えばrequestIDなどを出力することができます
    } 
}   
```

### Get Object ACL

##### 機能説明

Get Object ACL APIでObjectのACL、即ちバケット（Object）のアクセス権限管理リストを取得できます。当該APIに対してObject所有者にのみ操作権限があります。関連APIドキュメントについては、[Get Object ACL](/document/product/436/7744)を参照してください。

#### 方法のプロトタイプ

```cpp
CosResult GetObjectACL(const DGetObjectACLReq& req, GetObjectACLResp* resp);
```

#### パラメータ説明

| パラメータ | パラメータ説明                                    |
| ---- | ------------------------------------------- |
| req  | GetObjectACLReq、GetObjectACL操作のリクエスト。  |
| resp | GetObjectACLResp、GetObjectACL操作のレスポンス。 |

```
std::string GetOwnerID();
std::string GetOwnerDisplayName();
std::vector<Grant> GetAccessControlList();

```

#### 例

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string Object_name = "cpp_sdk_v5-123456789";

//GetObjectACLReqの構造関数にObject_nameを渡す必要があります
qcloud_cos::GetObjectACLReq req(Object_name);
qcloud_cos::GetObjectACLResp resp;
qcloud_cos::CosResult result = cos.GetObjectACL(req, &resp);

//呼び出しに成功した場合、respのメンバー関数を呼び出してレスポンス内容を取得します
if (result.IsSucc()) {
    // ...
} else {
    //ACLの取得に失敗した場合、CosResultのメンバー関数を呼び出してエラー情報、例えばrequestIDなどを出力することができます
} 
```

### Put Object Copy

##### 機能説明

Put Object Copyリクエストでファイルをソースパスから目標パスにコピーすることができます。コピーにおいて、ファイルの元属性とACLは変更可能です。ユーザーは当該APIによりファイルの移動、ファイルの再命名、ファイル属性の変更とコピーができます。推奨のファイルサイズは1MB〜5GBです。5GB以上のファイルについては、マルチパートアップロードを使用してくださいUpload - Copy。関連APIドキュメントについては、[Put Object Copy](/document/product/436/10881)を参照してください。

#### 方法のプロトタイプ

```cpp
CosResult PutObjectCopy(const PutObjectCopyReq& req, PutObjectCopyResp* resp);
```

#### パラメータ説明

| パラメータ | パラメータ説明                                      |
| ---- | --------------------------------------------- |
| req  | PutObjectCopyReq、PutObjectCopy操作のリクエスト。  |
| resp | PutObjectCopyResp、PutObjectCopy操作のレスポンス。 |

```
//ソースファイルURLパス、versionidサブリソースにより履歴バージョンを指定できます
void SetXCosCopySource(const std::string& str);

//メタデータをコピーしますか。列挙値：Copy, Replaced、デフォルト値Copy。
// タグがCopyであれば、Headerにおけるユーザーのメタデータ情報を無視して直接コピーします。
//タグがReplacedであれば、Header情報によりメタデータを変更します。
// 目標パスと元パスが一致する場合、即ちユーザーがメタデータを変更しようとする時、Replacedでなければなりません
void SetXCosMetadataDirective(const std::string& str);

//Objectが指定時間後に変更されると、操作が実行されます。さもなければ412が返されます。
// x-cos-copy-source-If-None-Matchと併用することができます。その他条件と併用する場合、競合が返されます。
void SetXCosCopySourceIfModifiedSince(const std::string& str);

//Objectが指定時間後に変更されていない場合、操作が実行されます。さもなければ412が返されます。
// x-cos-copy-source-If-Matchと併用することができます。その他条件と併用する場合、競合が返されます。
void SetXCosCopySourceIfUnmodifiedSince(const std::string& str);

//ObjectのEtagが所与の条件と一致する場合、操作が実行されます。さもなければ412が返されます。
// x-cos-copy-source-If-Unmodified-Sinceと併用することができます。その他条件と併用する場合、競合が返されます
void SetXCosCopySourceIfMatch(const std::string& str);

// ObjectのEtagが所与の条件と一致していない場合、操作が実行されます。さもなければ412が返されます。
// x-cos-copy-source-If-Modified-Sinceと併用することができます。その他条件と併用する場合、競合が返されます。
void SetXCosCopySourceIfNoneMatch(const std::string& str);

//x-cos-storage-classでObjectのストレージレベルを設定します。列挙値：STANDARD,STANDARD_IA
// デフォルト値：STANDARD（現在、華南パークにのみ対応します）
void SetXCosStorageClass(const std::string& storage_class);

//ObjectのACL属性を定義する場合、有効値：private,public-read-write,public-read
// デフォルト値：private
void SetXCosAcl(const std::string& str);

//権限が付与された者に読み取り権限を付与します。フォーマット：x-cos-grant-read: id=" ",id=" "。
// サブアカウントに権限を付与する場合、id="qcs::cam::uin/<OwnerUin>!:uin/<SubUin>!"
//ルートアカウントに権限を付与する場合、id="qcs::cam::uin/<OwnerUin>!:uin/<OwnerUin>!"
void SetXCosGrantRead(const std::string& str);

//権限が付与された者に書き込み権限を付与します。フォーマット：x-cos-grant-write: id=" ",id=" "./
// サブアカウントに権限を付与する場合、id="qcs::cam::uin/<OwnerUin>!:uin/<SubUin>!"、
//ルートアカウントに権限を付与する場合、id="qcs::cam::uin/<OwnerUin>!:uin/<OwnerUin>!"
void SetXCosGrantWrite(const std::string& str);

//権限が付与された者に読み取りと書き込み権限を付与します。フォーマット：x-cos-grant-full-control: id=" ",id=" "。
// サブアカウントに権限を付与する場合、id="qcs::cam::uin/<OwnerUin>!:uin/<SubUin>!"、
//ルートアカウントに権限を付与する場合、id="qcs::cam::uin/<OwnerUin>!:uin/<OwnerUin>!"
void SetXCosGrantFullControl(const std::string& str);

//ユーザーカスタマイズ可能なヘッダー情報は、Objectのメタデータとして返却されます。サイズは2Kに限られます
void SetXCosMeta(const std::string& key, const std::string& value);

/// Server側の暗号化によるアルゴリズムを設定します。現在、AES256に対応しています
void SetXCosServerSideEncryption(const std::string& str);

```

```
//ファイルのMD5アルゴリズムチェック値が返されます。ETagの値により、Object内容変化の有無を検査できます。
std::string GetEtag();

//ファイルの最終変更時間が返され、GMTフォーマットです
std::string GetLastModified();

//バージョン番号が返されます
std::string GetVersionId();

/// Server側の暗号化によるアルゴリズム
std::string GetXCosServerSideEncryption();

```

#### 例

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-123456789";
std::string object_name = "sevenyou";

qcloud_cos::PutObjectCopyReq req(bucket_name, object_name);                                                                                                                       
req.SetXCosCopySource("sevenyousouthtest-12345656.cn-south.myqcloud.com/sevenyou_source_obj");
qcloud_cos::PutObjectCopyResp resp;
qcloud_cos::CosResult result = cos.PutObjectCopy(req, &resp);
```

