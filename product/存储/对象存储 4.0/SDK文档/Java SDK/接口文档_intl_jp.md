COS XML Java SDK操作が成功すると、各APIの対応タイプが返され、失敗すると、異常（CosClientExceptionおよびCosServiception）が報告されます。そのうち、CosClientExceptionは、ネットワーク異常、リクエスト送信失敗などのクライアント異常です。CosServiceExceptionには、顧客のリクエストがサーバーによりエラーとして処理された原因、エラーコードなどが含まれています。例えば、権限を有さず、存在しないファイルにアクセスしました。詳細については、ドキュメント末尾の異常タイプの説明を参照してください。
SDKにおいて各APIを使用する正しい方法は以下のとおりです：簡潔にするために、後続のAPIの例では、異常をキャプチャする例を示しておらず、単にAPIの使用例を示しています。

```java
try {
   // バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名称はこのフォーマットでなければなりません
   String bucketName = "movie-1251668577";
   String key = "abc/def.jpg";
   cosClient.deleteObject(bucket, key);
} catch (CosClientException cle) {
  // 印刷異常などの異常処理をカスタマイズします
  log.error("del object failed.", cle);
  // ...
} catch (CosServiceException cse) {
   // 印刷異常などの異常処理をカスタマイズします
  log.error("del object failed.", cse);
  // ...
}
```

## Bucket API説明

### Put Bucket

バケットを新規作成します。バケットが限られたリソースであり、バケットがディレクトリと同じではなく、かつバケット内のファイルの数が無制限であるため、バケットを大量に作成しないことをお勧めします。バケットの作成が低頻度の操作であるため、コンソールでバケットを作成し、SDKでオブジェクトの操作を実行することをお勧めします。

- **方法のプロトタイプ**

```java
public Bucket createBucket(String  bucketName) throws CosClientException, CosServiceException;
```

- **パラメータ説明**

| パラメータ名     | パラメータ説明                                                     | タイプ   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | バケットの命名規則は{name}-{appid}であり、名称は英数字とハイフンで構成されています | String |

- **戻り値**
  - 成功：バケットに関する説明（バケットの名称、オーナーおよび作成日）を含むバケットタイプ。
  - 失敗：エラー（認証失敗など）が発生した場合、異常CosClientExceptionまたはCosServiceExceptionをスローします。詳細については、異常タイプの説明を参照してください。
- **例**

```java
// バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名称はこのフォーマットでなければなりません
String bucketName = "movie-1251668577";
Bucket bucket = cosClient.createBucket(bucketName);
```

### Delete Bucket

空になったバケットを削除します。

- **方法のプロトタイプ**

```java
 public void deleteBucket(String bucketName) throws CosClientException, CosServiceException;
```

- **パラメータ説明**

| パラメータ名     | パラメータ説明                                                     | タイプ   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | バケットの命名規則は{name}-{appid}であり、名称は英数字とハイフンで構成されています | String |

- **戻り値**
  - 成功：戻り値がない。
  - 失敗：エラー（認証失敗など）が発生した場合、異常CosClientExceptionまたはCosServiceExceptionをスローします。詳細については、異常タイプの説明を参照してください。
- **例**

```java
// バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名称はこのフォーマットでなければなりません
String bucketName = "movie-1251668577";
cosClient.deleteBucket(bucketName);
```

### Head Bucket

バケットの存在を照合します。

- **方法のプロトタイプ**

```java
public boolean doesBucketExist(String bucketName) 
  throws CosClientException, CosServiceException;
```

- **パラメータ説明**

| パラメータ名     | パラメータ説明                                                     | タイプ   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | バケットの命名規則は{name}-{appid}であり、名称は英数字とハイフンで構成されています | String |

- **戻り値**
  - 成功：存在する場合は、trueを返し、そうでない場合は、falseを返します。
  - 失敗：エラー（認証失敗など）が発生した場合、異常CosClientExceptionまたはCosServiceExceptionをスローします。詳細については、異常の説明を参照してください。
- **例**

```java
// バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名称はこのフォーマットでなければなりません
String bucketName = "movie-1251668577";
boolean bucketExistFlag = cosClient.doesBucketExist(bucketName);
```

### Get Bucket Location

バケットが位置する地域を照合します。

- **方法のプロトタイプ**

```java
public String getBucketLocation(String bucketName) 
throws CosClientException， CosServiceException;
```

- **パラメータ説明**

| パラメータ名     | パラメータ説明                                                     | タイプ   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | バケットの命名規則は{name}-{appid}であり、名称は英数字とハイフンで構成されています | String |

- **戻り値**
  - 成功：バケットが位置する地域を返します。 
  - 失敗：エラー（例えば、バケットが存在しない）が発生した場合、異常CosClientExceptionまたはCosServiceExceptionをスローします。詳細については、異常の説明を参照してください。
- **例**

```java
// バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名称はこのフォーマットでなければなりません
String location = cosClient.getBucketLocation("movie-1251668577");
```

### List Buckets

アカウント内のすべてのバケットをリストします

- **方法のプロトタイプ**

```java
public List<Bucket> listBuckets() throws CosClientException, CosServiceException;
```

- **パラメータ説明**

なし

- **戻り値**
  - 成功：すべてのバケットタイプのリストを返し、バケットタイプには、バケットメンバー、位置などの情報が含まれています。
  - 失敗：エラー（例えば、バケットが存在しない）が発生した場合、異常CosClientExceptionまたはCosServiceExceptionをスローします。詳細については、異常の説明を参照してください。
- **例**

```java
List<Bucket> buckets = cosClient.listBuckets();
for (Bucket bucketElement : buckets) {
    String bucketName = bucketElement.getName();
    String bucketLocation = bucketElement.getLocation();
}
```

### バケットの取得（すべてのオブジェクトをリストします）

照合によりCOS上のファイルリストを取得します。

- **方法のプロトタイプ**

```java
// ファイルリストの取得
public ObjectListing listObjects(ListObjectsRequest listObjectsRequest)
            throws CosClientException, CosServiceException;
```

- **パラメータ説明**

| パラメータ名             | パラメータ説明        | パラメータタイプ           |
| ------------------ | ---------------- | ------------------ |
| listObjectsRequest | ファイルリスト取得リクエスト | ListObjectsRequest |

リクエストメンバーの説明：

| リクエストメンバー | 設定方法            | 説明                                                         | タイプ   |
| ------------ | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName   | 構造関数または設定方法 | バケットの命名規則は{name}-{appid}であり、名称は英数字とハイフンで構成されています | String |
| プレフィックス       | 構造関数または設定方法 | リストの中にプレフィックスの値をプレフィックスとするメンバー、デフォルトでは制限せず、即ち、バケット内のすべてのメンバーをマークします。<br>デフォルト値： "" | String |
|   マーカー   |  構造関数または設定方法 |  リストの開始位置をマークし、最初に空であり、後続に前回のリストの戻り値中のマーカーです|String  
| デリミター  | 構造関数または設定方法 |区切り記号、プレフィックスで始まり、かつ一度に出現するデリミターで終わるパスを制限します |String  
|  maxKeys   | 構造関数または設定方法  |           返された最大のメンバー数（1000を超えてはいけません）   <br>デフォルト値：1000          |Integer |  

- **戻り値**
  - 成功：すべてのメンバーおよびnextMarkerを含むObjectListingタイプを返します。  
  - 失敗：異常CosClientExceptionまたはCosServiceExceptionをスローします。詳細については、異常タイプの説明を参照してください。
- **例**

```java
// バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名称はこのフォーマットでなければなりません
String bucketName = "movie-1251668577";

// バケット内のメンバーを取得します（デリミターを設定します）
ListObjectsRequest listObjectsRequest = new ListObjectsRequest();
listObjectsRequest.setBucketName(bucketName);
// リストのプレフィックスを設定し、リストされたファイルのキーがいずれもこのプレフィックスで始まることを示します
listObjectsRequest.setPrefix("");
// デリミターを/に設定し、即ち、取得されたのは直接メンバーであり、ディレクトリ内の再帰的なサブメンバーが含まれません
listObjectsRequest.setDelimiter("/");
// マーカーを設定し、（マーカーは前回のリストにより取得され、または最初のリストのマーカーは空です）
listObjectsRequest.setMarker("");
// 最大100のメンバーをリストするように設定します（設定しないと、デフォルトでは1000であり、一度に最大1000のキーをリストすることが可能です）
listObjectsRequest.setMaxKeys(100);

ObjectListing objectListing = cosClient.listObjects(listObjectsRequest);
// 次回リストするマーカーを取得します
String nextMarker = objectListing.getNextMarker();
// リストが終了したかどうかを判断し、リストが終了した場合、isTruncatedはfalseであり、そうでない場合、trueです
boolean isTruncated = objectListing.isTruncated();
List<COSObjectSummary> objectSummaries = objectListing.getObjectSummaries();
for (COSObjectSummary cosObjectSummary : objectSummaries) {
// ファイルパス
String key = cosObjectSummary.getKey();
// ファイルサイズを取得します
long fileSize = cosObjectSummary.getSize();
// ファイルETagを取得します
String eTag = cosObjectSummary.getETag();
// 最終変更時間を取得します
Date lastModified = cosObjectSummary.getLastModified();
// ファイルのストレージタイプを取得します
String StorageClassStr = cosObjectSummary.getStorageClass();
}
```

### Bucket ACL

バケットのアクセス制御権限リスト（Access Control List）を設定します。

Set Bucket ACLは、既存の権限設定を上書きする上書き操作です。

ACLには、事前定義権限ポリシー（CannedAccessControlList）またはカスタマイズ権限制御（AccessControlList）が含まれています。2種類の権限が同時に設定されている場合、事前定義ポリシーが無視され、カスタマイズポリシーが優先されます。権限の詳細については、権限セクションを参照してください。

- **方法のプロトタイプ**

```java
// 方法1（カスタマイズポリシーを設定します）
public void setBucketAcl(String bucketName, AccessControlList acl)
  throws CosClientException, CosServiceException;
// 方法2（事前定義ポリシーを設定します）
public void setBucketAcl(String bucketName, CannedAccessControlList acl) throws CosClientException, CosServiceException;
// 方法3（以上の2種類の方法のパッケージであり、2種類のポリシーの設定が含まれ、同時に設定されている場合、カスタマイズポリシーが優先されます）
public void setBucketAcl(SetBucketAclRequest setBucketAclRequest) 
  throws CosClientException, CosServiceException;
```

- **パラメータ説明**

方法3のパラメータには1と2の両方が含まれるため、方法3を例として紹介します。

| パラメータ名              | パラメータ説明       | タイプ                 |
| ------------------- | -------------- | ------------------- |
| setBucketAclRequest | 権限設定リクエストタイプ | SetBucketAclRequest |

リクエストメンバーの説明：

| リクエストメンバー | 設定方法            | 説明                                                         | タイプ                    |
| ------------ | ------------------- | ------------------------------------------------------------ | ----------------------- |
| bucketName   | 構造関数または設定方法 | バケットの命名規則は{name}-{appid}であり、名称は英数字とハイフンで構成されています | String                  |
| acl          | 構造関数または設定方法 | カスタマイズ権限ポリシー                                               | AccessControlList       |
| cannedAcl    | 構造関数または設定方法 | パブリック読み取り、パブリック読み書き、プライベート読み取りなどの事前定義ポリシー                         | CannedAccessControlList |

- **戻り値**
  - 成功：戻り値がない。
  - 失敗：エラー（認証失敗など）が発生した場合、異常CosClientExceptionまたはCosServiceExceptionをスローします。詳細については、異常タイプの説明を参照してください。
- **例**

```java
// バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名称はこのフォーマットでなければなりません
String bucketName = "movie-1251668577";
// カスタマイズACLを設定します
AccessControlList acl = new AccessControlList();
Owner owner = new Owner();
owner.setId("qcs::cam::uin/2779643970:uin/2779643970");
acl.setOwner(owner);
String id = "qcs::cam::uin/2779643970:uin/734505014";
UinGrantee uinGrantee = new UinGrantee("qcs::cam::uin/2779643970:uin/734505014");
uinGrantee.setIdentifier(id);
acl.grantPermission(uinGrantee, Permission.FullControl);
cosClient.setBucketAcl(bucketName, acl);

// 事前定義ACLを設定します
//プライベート読み書きを設定します（デフォルトでは、新規作成されたバケットはいずれもプライベート読み書きです）
cosClient.setBucketAcl(bucketName, CannedAccessControlList.Private);
// パブリック読み取りとプライベート書き込みを設定します
cosClient.setBucketAcl(bucketName, CannedAccessControlList.PublicRead);
// パブリック読み書きを設定します
cosClient.setBucketAcl(bucketName, CannedAccessControlList.PublicReadWrite);
```

### Get Bucket ACL

バケットのアクセスポリシーACLを照合します。

- **方法のプロトタイプ**

```java
public AccessControlList getBucketAcl(String bucketName)
       throws CosClientException, CosServiceException
```

- **パラメータ説明**

| パラメータ名     | パラメータ説明                                                     | タイプ   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | バケットの命名規則は{name}-{appid}であり、名称は英数字とハイフンで構成されています | String |

- **戻り値**
  - 成功：バケットのACLを返します。 
  - 失敗：エラー（認証失敗など）が発生した場合、異常CosClientExceptionまたはCosServiceExceptionをスローします。詳細については、異常タイプの説明を参照してください。
- **例**

```java
// バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名称はこのフォーマットでなければなりません
String bucketName = "movie-1251668577";
AccessControlList acl = cosClient.getBucketAcl(bucketName);
```

### Set Bucket CORS

バケットのクロスオリジンアクセス規則を設定します。

- **方法のプロトタイプ**

```java
public void setBucketCrossOriginConfiguration(String bucketName, BucketCrossOriginConfiguration bucketCrossOriginConfiguration);
```

- **パラメータ説明**

| パラメータ名                         | パラメータ説明                                                     | タイプ                           |
| ------------------------------ | ------------------------------------------------------------ | ------------------------------ |
| bucketName                     | バケットの命名規則は{name}-{appid}であり、名称は英数字とハイフンで構成されています | String                         |
| bucketCrossOriginConfiguration | 設定されたバケットのクロスオリジンポリシー                                      | BucketCrossOriginConfiguration |

- **戻り値**
  - 成功：戻り値がない。
  - 失敗：エラー（認証失敗など）が発生した場合、異常CosClientExceptionまたはCosServiceExceptionをスローします。詳細については、異常タイプの説明を参照してください。
- **例**

```java
// バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名称はこのフォーマットでなければなりません
String bucketName = "movie-1251668577";
BucketCrossOriginConfiguration bucketCORS = new BucketCrossOriginConfiguration();
List<CORSRule> corsRules = new ArrayList<>();
CORSRule corsRule = new CORSRule();
// 規則名称
corsRule.setId("set-bucket-cors-test");  
// 許容されるHTTP方法
corsRule.setAllowedMethods(AllowedMethods.PUT, AllowedMethods.GET, AllowedMethods.HEAD);
corsRule.setAllowedHeaders("x-cos-grant-full-control");
corsRule.setAllowedOrigins("http://mail.qq.com", "http://www.qq.com",
        "http://video.qq.com");
corsRule.setExposedHeaders("x-cos-request-id");
corsRule.setMaxAgeSeconds(60);
corsRules.add(corsRule);
bucketCORS.setRules(corsRules);
cosClient.setBucketCrossOriginConfiguration(bucketName, bucketCORS);
```

### Get Bucket CORS

バケットのクロスオリジンアクセス規則を取得します。

- **方法のプロトタイプ**

```java
public BucketCrossOriginConfiguration getBucketCrossOriginConfiguration(String bucketName)
throws CosClientException, CosServiceException;
```

- **パラメータ説明**

| パラメータ名     | パラメータ説明                                                     | タイプ   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | バケットの命名規則は{name}-{appid}であり、名称は英数字とハイフンで構成されています | String |

- **戻り値**
  - 成功：バケットのクロスオリジン規則を返します。
  - 失敗：エラー（認証失敗など）が発生した場合、異常CosClientExceptionまたはCosServiceExceptionをスローします。詳細については、異常タイプの説明を参照してください。
- **例**

```java
// バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名称はこのフォーマットでなければなりません
String bucketName = "movie-1251668577";
BucketCrossOriginConfiguration corsGet = cosClient.getBucketCrossOriginConfiguration(bucketName);
List<CORSRule> corsRules = corsGet.getRules();
for (CORSRule rule : corsRules) {
List<AllowedMethods> allowedMethods = rule.getAllowedMethods();
List<String> allowedHeaders = rule.getAllowedHeaders();
List<String> allowedOrigins = rule.getAllowedOrigins();
List<String> exposedHeaders = rule.getExposedHeaders();
int maxAgeSeconds = rule.getMaxAgeSeconds();
}
```

### Delete Bucket CORS

バケットのクロスオリジンアクセス規則を削除します。

- **方法のプロトタイプ**

```java
public void deleteBucketCrossOriginConfiguration(String bucketName)
throws CosClientException, CosServiceException;
```

- **パラメータ説明**

| パラメータ名     | パラメータ説明                                                     | タイプ   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | バケットの命名規則は{name}-{appid}であり、名称は英数字とハイフンで構成されています | String |

- **戻り値**
  - 成功：戻り値がない。
  - 失敗：エラー（認証失敗など）、異常CosClientExceptionまたはCosServiceExceptionをスローします。詳細については、異常タイプの説明を参照してください。
- **例**

```java
// バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名称はこのフォーマットでなければなりません
String bucketName = "movie-1251668577";
cosClient.deleteBucketCrossOriginConfiguration(bucketName);
```

### Set Bucket MultiVersioning

バケットのバージョン制御を有効にし、バージョン制御を有効にした後、各ファイルは複数のバージョンを保持します。

- **方法のプロトタイプ**

```java
public void setBucketVersioningConfiguration(SetBucketVersioningConfigurationRequest setBucketVersioningConfigurationRequest)
    throws CosClientException, CosServiceException;
```

- **パラメータ説明**

| パラメータ名                                  | パラメータ説明                                                     | タイプ                                    |
| --------------------------------------- | ------------------------------------------------------------ | --------------------------------------- |
| bucketName                              | バケットの命名規則は{name}-{appid}であり、名称は英数字とハイフンで構成されています | String                                  |
| setBucketVersioningConfigurationRequest | バージョン制御構成                                                 | SetBucketVersioningConfigurationRequest |

- **戻り値**
  - 成功：戻り値がない。
  - 失敗：エラー（認証失敗など）が発生した場合、異常CosClientExceptionまたはCosServiceExceptionをスローします。詳細については、異常タイプの説明を参照してください。
- **例**

```java
String bucketName = "movie-1251668577";

// バージョン制御を有効にします
cosClient.setBucketVersioningConfiguration(
        new SetBucketVersioningConfigurationRequest(bucketName,
                new BucketVersioningConfiguration(BucketVersioningConfiguration.ENABLED)));

// バージョン制御を無効にします
cosClient.setBucketVersioningConfiguration(
        new SetBucketVersioningConfigurationRequest(bucketName,
                new BucketVersioningConfiguration(BucketVersioningConfiguration.SUSPENDED)));
```

### Get  Bucket MultiVersioning

バケットのバージョン制御状態を取得します

- **方法のプロトタイプ**

```java
// 方法1：バケット名を渡しすればよいです
public BucketVersioningConfiguration getBucketVersioningConfiguration(String bucketName)
            throws CosClientException, CosServiceException;

// 方法2：GetBucketVersioningConfigurationRequestにより取得します			
public BucketVersioningConfiguration getBucketVersioningConfiguration(
    GetBucketVersioningConfigurationRequest getBucketVersioningConfigurationRequest)
        throws CosClientException, CosServiceException;
```

- **パラメータ説明**

| パラメータ名                                  | パラメータ説明                                                     | タイプ                                    |
| --------------------------------------- | ------------------------------------------------------------ | --------------------------------------- |
| bucketName                              | バケットの命名規則は{name}-{appid}であり、名称は英数字とハイフンで構成されています | String                                  |
| getBucketVersioningConfigurationRequest | バージョン制御構成の取得リクエスト                                         | SetBucketVersioningConfigurationRequest |

- **戻り値**
  - 成功：戻り値がない。
  - 失敗：エラー（認証失敗など）が発生した場合、異常CosClientExceptionまたはCosServiceExceptionをスローします。詳細については、異常タイプの説明を参照してください。
- **例**

```java
String bucketName = "movie-1251668577";

// バージョン制御を取得します
BucketVersioningConfiguration bvc =
        cosClient.getBucketVersioningConfiguration(bucketName);

// バージョン制御を取得します
BucketVersioningConfiguration bvc2 = cosClient.getBucketVersioningConfiguration(
                new GetBucketVersioningConfigurationRequest(bucketName));
```

### Set Bucket Replication

バケットキャンパス間レプリケーションを設定し、キャンパス間レプリケーションがバージョン制御に依存するため、先にバージョン制御を有効にしてください

- **方法のプロトタイプ**

```java
public void setBucketReplicationConfiguration(
        SetBucketReplicationConfigurationRequest setBucketReplicationConfigurationRequest)
                throws CosClientException, CosServiceException;
```

- **パラメータ説明**

| パラメータ名                                   | パラメータ説明                                                     | タイプ                                    |
| ---------------------------------------- | ------------------------------------------------------------ | --------------------------------------- |
| bucketName                               | バケットの命名規則は{name}-{appid}であり、名称は英数字とハイフンで構成されています | String                                  |
| setBucketReplicationConfigurationRequest | キャンパス間レプリケーション構成                                               | SetBucketVersioningConfigurationRequest |

- **戻り値**
  - 成功：戻り値がない。
  - 失敗：エラー（認証失敗など）が発生した場合、異常CosClientExceptionまたはCosServiceExceptionをスローします。詳細については、異常タイプの説明を参照してください。
- **例**

```java
String bucketName = "movie-1251668577";

ReplicationRule replicationRule = new ReplicationRule();
replicationRule.setStatus(ReplicationRuleStatus.Enabled);
replicationRule.setPrefix("");

ReplicationDestinationConfig replicationDestinationConfig =
     new ReplicationDestinationConfig();
// bucketQCSは、レプリケーションされる目的バケットフォーマットがqcs:id/0:cos:${dest-region}:appid/${appid}:${bucketname-not-contain-appid}であることを説明するために使用されます
String bucketQCS = "qcs:id/0:cos:ap-chongqing:appid/1251668577:moviebak-chongqing";
replicationDestinationConfig.setBucketQCS(bucketQCS);
replicationDestinationConfig.setStorageClass(StorageClass.Standard);
replicationRule.setDestinationConfig(replicationDestinationConfig);
BucketReplicationConfiguration bucketReplicationConfiguration =
     new BucketReplicationConfiguration();
// ruleNameはqcs::cam::uin/${uin}:uin/${uin}を構成します
String ruleName = "qcs::cam::uin/111222333:uin/111222333";
bucketReplicationConfiguration.setRoleName(ruleName);
// ruidは、レプリケーション規則のIDを表すために使用されます
String ruleId = "moviebak-chongqing-copy";
bucketReplicationConfiguration.addRule(ruleId, replicationRule);
cosClient.setBucketReplicationConfiguration(bucketName, bucketReplicationConfiguration);
```

### Get Bucket Replication

バケットキャンパス間レプリケーションを取得します。

- **方法のプロトタイプ**

```java
// バケット地域間レプリケーション構成を取得する方法1
public BucketCrossOriginConfiguration getBucketCrossOriginConfiguration(String bucketName)
        throws CosClientException, CosServiceException;

// バケット地域間レプリケーションを取得する方法2		
public BucketCrossOriginConfiguration getBucketCrossOriginConfiguration(
        GetBucketCrossOriginConfigurationRequest getBucketCrossOriginConfigurationRequest)
                throws CosClientException, CosServiceException;
```

- **パラメータ説明**

| パラメータ名                                   | パラメータ説明                                                     | タイプ                                     |
| ---------------------------------------- | ------------------------------------------------------------ | ---------------------------------------- |
| bucketName                               | バケットの命名規則は{name}-{appid}であり、名称は英数字とハイフンで構成されています | String                                   |
| getBucketCrossOriginConfigurationRequest | 地域間レプリケーション構成の取得リクエスト                                       | GetBucketCrossOriginConfigurationRequest |

- **戻り値**
  - 成功：戻り値がない。
  - 失敗：エラー（認証失敗など）が発生した場合、異常CosClientExceptionまたはCosServiceExceptionをスローします。詳細については、異常タイプの説明を参照してください。
- **例**

```java
String bucketName = "movie-1251668577";

// バケット地域間レプリケーション構成を取得する方法1
BucketReplicationConfiguration brcfRet = cosClient.getBucketReplicationConfiguration(bucketName);

// バケット地域間レプリケーション構成を取得する方法2
BucketReplicationConfiguration brcfRet2 = cosClient.getBucketReplicationConfiguration(
                new GetBucketCrossOriginConfigurationRequest(bucketName));
```

### Delete Bucket Replication

バケットキャンパス間レプリケーションを削除します。

- **方法のプロトタイプ**

```java
// バケット地域間レプリケーション構成を削除する方法1
public void deleteBucketCrossOriginConfiguration(String bucketName)
        throws CosClientException, CosServiceException;

// バケット地域間レプリケーションを削除する方法2		
public void deleteBucketCrossOriginConfiguration(
        DeleteBucketCrossOriginConfigurationRequest deleteBucketCrossOriginConfigurationRequest)
                throws CosClientException, CosServiceException;
```

- **パラメータ説明**

| パラメータ名                                      | パラメータ説明                                                     | タイプ                                        |
| ------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------- |
| bucketName                                  | バケットの命名規則は{name}-{appid}であり、名称は英数字とハイフンで構成されています | String                                      |
| deleteBucketCrossOriginConfigurationRequest | 地域間レプリケーション構成の削除リクエスト                                       | DeleteBucketCrossOriginConfigurationRequest |

- **戻り値**
  - 成功：戻り値がない。
  - 失敗：エラー（認証失敗など）が発生した場合、異常CosClientExceptionまたはCosServiceExceptionをスローします。詳細については、異常タイプの説明を参照してください。
- **例**

```java
String bucketName = "movie-1251668577";

// バケット地域間レプリケーション構成を削除する方法1
BucketReplicationConfiguration brcfRet =  cosClient.deleteBucketReplicationConfiguration(bucketName);

// バケット地域間レプリケーション構成を削除する方法2
BucketReplicationConfiguration brcfRet2 = cosClient.getBucketReplicationConfiguration(
                new DeleteBucketCrossOriginConfigurationRequest(bucketName));
```

### Set Bucket LifeCycle

バケットのライフサイクル規則を設定します。

- **方法のプロトタイプ**

```java
public void setBucketLifecycleConfiguration(String bucketName, BucketLifecycleConfiguration bucketLifecycleConfiguration) 
        throws CosClientException, CosServiceException;
```

- **パラメータ説明**

| パラメータ名                       | パラメータ説明                                                     | タイプ                         |
| ---------------------------- | ------------------------------------------------------------ | ---------------------------- |
| bucketName                   | バケットの命名規則は{name}-{appid}であり、名称は英数字とハイフンで構成されています | String                       |
| bucketLifecycleConfiguration | ライフサイクル構成                                                 | BucketLifecycleConfiguration |

- **戻り値**
  - 成功：戻り値がない。
  - 失敗：エラー（認証失敗など）が発生した場合、異常CosClientExceptionまたはCosServiceExceptionをスローします。詳細については、異常タイプの説明を参照してください。
- **例**

```java
List<Rule> rules = new ArrayList<>();
// 規則1  パスが hongkong_movie/ で始まるファイルを30日後に削除します
Rule deletePrefixRule = new Rule();
deletePrefixRule.setId("delete prefix xxxy after 30 days");
deletePrefixRule
.setFilter(new LifecycleFilter(newLifecyclePrefixPredicate("hongkong_movie/")));
// ファイルをアップロードまたは変更した後、30日後に削除します
deletePrefixRule.setExpirationInDays(30);
// 規則を有効状態に設定します
deletePrefixRule.setStatus(BucketLifecycleConfiguration.ENABLED);

// 規則2  20日後に低頻度にウングレードし、1年後に削除します
Rule standardIaRule = new Rule();
standardIaRule.setId("standard_ia transition");
standardIaRule.setFilter(new LifecycleFilter(new LifecyclePrefixPredicate("standard_ia/")));
List<Transition> standardIaTransitions = new ArrayList<>();
Transition standardTransition = new Transition();
standardTransition.setDays(20);
standardTransition.setStorageClass(StorageClass.Standard_IA.toString());
standardIaTransitions.add(standardTransition);
standardIaRule.setTransitions(standardIaTransitions);
standardIaRule.setStatus(BucketLifecycleConfiguration.ENABLED);
standardIaRule.setExpirationInDays(365);
		
// 2つの規則をポリシーセットに追加します
rules.add(deletePrefixRule);
rules.add(standardIaRule);

// bucketLifecycleConfigurationを生成します
BucketLifecycleConfiguration bucketLifecycleConfiguration =
new BucketLifecycleConfiguration();
bucketLifecycleConfiguration.setRules(rules);

// バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名称はこのフォーマットでなければなりません
String bucketName = "movie-1251668577";
SetBucketLifecycleConfigurationRequest setBucketLifecycleConfigurationRequest =
new SetBucketLifecycleConfigurationRequest(bucketName, bucketLifecycleConfiguration);

// ライフサイクルを設定します
cosClient.setBucketLifecycleConfiguration(setBucketLifecycleConfigurationRequest);
```

### Get Bucket LifeCycle

バケットのライフサイクル規則を取得します。

- **方法のプロトタイプ**

```java
public BucketLifecycleConfiguration getBucketLifecycleConfiguration(String bucketName)
throws CosClientException, CosServiceException;
```

- **パラメータ説明**

| パラメータ名     | パラメータ説明                                                     | タイプ   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | バケットの命名規則は{name}-{appid}であり、名称は英数字とハイフンで構成されています | String |

- **戻り値**
  - 成功：バケットのライフサイクル規則を含むBucketLifecycleConfigurationタイプを返します。
  - 失敗：エラー（認証失敗など）が発生した場合、異常CosClientExceptionまたはCosServiceExceptionをスローします。詳細については、異常タイプの説明を参照してください。
- **例**

```java
// バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名称はこのフォーマットでなければなりません
String bucketName = "movie-1251668577";
BucketLifecycleConfiguration queryLifeCycleRet =
        cosClient.getBucketLifecycleConfiguration(bucketName);
List<Rule> ruleLists = queryLifeCycleRet.getRules();
```

### Delete Bucket LifeCycle

バケットのライフサイクル規則を削除してクリアします。

- **方法のプロトタイプ**

```java
public void deleteBucketLifecycleConfiguration(String bucketName)
throws CosClientException, CosServiceException;
```

- **パラメータ説明**

| パラメータ名     | パラメータ説明                                                     | タイプ   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | バケットの命名規則は{name}-{appid}であり、名称は英数字とハイフンで構成されています | String |

- **戻り値**
  - 成功：戻り値がない。
  - 失敗：エラー（認証失敗など）が発生した場合、異常CosClientExceptionまたはCosServiceExceptionをスローします。詳細については、異常タイプの説明を参照してください。
- **例**

```java
// バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名称はこのフォーマットでなければなりません
String bucketName = "movie-1251668577";
cosClient.deleteBucketLifecycleConfiguration(bucketName);
```

## Object API説明

### PUT Object（オブジェクトをアップロードします）

ローカルファイルまたはサイズが既知となる入力ストリームコンテンツをCOSにアップロードします。画像のような小さいファイルのアップロード（20MB以下）に適し、最大5GB（含む）をサポートし、5GB以上であれば、マルチパートアップロードまたは高レベルAPIによるアップロードを使用してください。

- アップロードプロセスにおいて、デフォルトでは、ファイルサイズとMD5をチェックします（MD5チェック参照サンプルコードを終了します）。
- 同じキーのオブジェクトが既にCOSに存在する場合、アップロードする時に上書きします。
- 現在のアクセスポリシーエントリは1000に制限され、オブジェクトのACL制御を行う必要がない場合、アップロードする時に設定しないでください。デフォルトでは、バケット権限を継承します。
- アップロードした後、同じ `key`を使用して、`GetObject`APIを呼び出してファイルをローカルにダウンロードすることができ、事前署名リンクを生成し（ダウンロードする際に`GET`としてmethodを指定してください。具体的なAPIの説明について後述します）、他の側に送信してダウンロードすることもできます。


- **方法のプロトタイプ**

```java
// 方法1：ローカルファイルをCOSにアップロードします
public PutObjectResult putObject(String bucketName, String key, File file)
            throws CosClientException, CosServiceException;
// 方法2：入力ストリームをCOSにアップロードします
public PutObjectResult putObject(String bucketName, String key, InputStream input,
ObjectMetadata metadata) throws CosClientException, CosServiceException;
// 方法3：以上の2つの方法をパッケージ化し、content-type、content-dispositionなど、より細かい粒度のパラメータ制御をサポートします
public PutObjectResult putObject(PutObjectRequest putObjectRequest)
throws CosClientException, CosServiceException;
```

- **パラメータ説明**

| パラメータ名           | パラメータ説明     | パラメータタイプ         |
| ---------------- | ------------ | ---------------- |
| putObjectRequest | ファイルのアップロードのリクエスト| PutObjectRequest |

リクエストメンバーの説明：

| リクエストメンバー | 設定方法            | 説明                                                         | タイプ           |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |
| bucketName   | 構造関数または設定方法 | バケットの命名規則は{name}-{appid}であり、名称は英数字とハイフンで構成されています | String         |
| key          | 構造関数または設定方法 | オブジェクトキー（Key）はオブジェクトのバケットにおける一意な識別子です。例えば、オブジェクトのアクセスドメイン名 `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg` において、オブジェクトキーは doc1/pic1.jpg であり、詳細については、 [オブジェクトキー](https://cloud.tencent.com/document/product/436/13324)を参照してください | String         |
| file         | 構造関数または設定方法 | ローカルファイル                                                     | File           |
| input        | 構造関数または設定方法 | 入力ストリーム                                                       | InputStream    |
| metadata     | 構造関数または設定方法 | ファイルのメタ情報                                                 | ObjectMetadata |

- **戻り値**
  - 成功：ファイルのETagなどの情報を含むPutObjectResult。
  - 失敗：エラー（認証失敗など）が発生した場合、異常CosClientExceptionまたはCosServiceExceptionをスローします。詳細については、異常タイプの説明を参照してください。
- **例**

```java
// バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名称はこのフォーマットでなければなりません
String bucketName = "movie-1251668577";
// 方法1：ローカルファイルをアップロードします
File localFile = new File("/data/test.txt");
String key = "aaa.txt";
PutObjectResult putObjectResult = cosClient.putObject(bucketName, key, localFile);
String etag = putObjectResult.getETag();  // ファイルのetagを取得します

// 方法2：入力ストリームからアップロードします（入力ストリームのサイズを事前に通知する必要があり、そうしないと、oomを引き起こす可能性があります）
FileInputStream fileInputStream = new FileInputStream(localFile);
ObjectMetadata objectMetadata = new ObjectMetadata();
// 入力ストリームのサイズを500に設定します
objectMetadata.setContentLength(500);  
// Content typeを設定し、デフォルトでは、application/octet-streamです
objectMetadata.setContentType("application/pdf");
PutObjectResult putObjectResult = cosClient.putObject(bucketName, key, fileInputStream, objectMetadata);
String etag = putObjectResult.getETag();
// 入力ストリームを閉じます...

// 方法3：より多くの細かい粒度の制御を提供し、一般的な設定は以下のとおりです：
// 1 storage-class ストレージタイプであり、標準（デフォルト）、低頻度、ニアラインを設定するために使用されます
// 2 content-type、ローカルファイルのアップロードに対して、デフォルトでは、ローカルファイルのサフィックスに従ってマッピングし、例えば、jpgファイルをimage / jpegにマッピングします
// ストリーミングアップロードに対して、デフォルトでは、application/octet-streamです
// 3 アップロードすると同時に権限を設定します（API set object aclの呼び出しにより設定することもできます）
//4 アップロードのMD5チェックをグローバルに閉じるには、システム環境変数を設定し、この設定はすべてのアップロードチェックに影響を与えます。デフォルトでは、チェックします。
// チェックを閉じます  System.setProperty(SkipMd5CheckStrategy.DISABLE_PUT_OBJECT_MD5_VALIDATION_PROPERTY, "true");
//チェックを再び開きます  System.setProperty(SkipMd5CheckStrategy.DISABLE_PUT_OBJECT_MD5_VALIDATION_PROPERTY, null);
File localFile = new File("/data/dog.jpg");
String key = "mypic.jpg";
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, file);
// ストレージタイプを低頻度に設定します
putObjectRequest.setStorageClass(StorageClass.Standard_IA);
// カスタマイズプロパティ（content-type、content-dispositionなど）を設定します
ObjectMetadata objectMetadata = new ObjectMetadata();
// Content typeを設定し、デフォルトでは、application/octet-streamです
objectMetadata.setContentType("image/jpeg");
putObjectRequest.setMetadata(objectMetadata);
PutObjectResult putObjectResult = cosClient.putObject(putObjectRequest);
String etag = putObjectResult.getETag();  // ファイルのetagを取得します
```

- **パートファイルアップロード**

パートファイルアップロードは、ファイルを複数のパートに分割してアップロードし、複数のパートを同時にアップロードすることができ、最大40 TBをサポートします。

パートファイルアップロード手順は以下のとおりです：

1. マルチパートアップロードを初期化し、uploadidを取得します。（initiateMultipartUpload）
2. パートデータを（同時に）アップロードします。（uploadPart）
3. マルチパートアップロードを完了します。（completeMultipartUpload）

また、マルチパートアップロードの取得（listParts）、マルチパートアップロードの終了（abortMultipartUpload）を含むことができます。マルチパートアップロードの手順および制限が多く、後続のパッケージの高レベルAPIでアップロードすることをお勧めします。

**Tips**： マルチパートアップロードプロセスにおいて、デフォルトでは、各パートのサイズとMD5をチェックします（MD5チェック参照サンプルコードの終了については、前述した終了方法を参照してください）。

- **方法のプロトタイプ**

```java
// 方法1：マルチパートアップロードを初期化します
public InitiateMultipartUploadResult initiateMultipartUpload(
    InitiateMultipartUploadRequest request) throws CosClientException, CosServiceException;
// 方法2：データパートをアップロードします
public UploadPartResult uploadPart(UploadPartRequest uploadPartRequest)
            throws CosClientException, CosServiceException;
// 方法3：マルチパートアップロードを完了します
public CompleteMultipartUploadResult completeMultipartUpload(
            CompleteMultipartUploadRequest request) throws CosClientException, CosServiceException;
// 方法4：アップロードされたパートをリストします
public PartListing listParts(ListPartsRequest request)
            throws CosClientException, CosServiceException;
// 方法5：マルチパートアップロードを終了します
public void abortMultipartUpload(AbortMultipartUploadRequest request)
            throws CosClientException, CosServiceException;
```

- **戻り値**
- **方法1 （initiateMultipartUpload）**
  - 成功：後続のマルチパートアップロードに使用する必要があるupload IDを含むInitiateMultipartUploadResultタイプを返します。
  - 失敗：エラー（認証失敗など）、異常CosClientExceptionまたはCosServiceExceptionをスローします。詳細については、異常タイプの説明を参照してください。
- **方法2 （uploadPart）**
  - 成功：このパートのEtagとpartNumberを含むUploadPartResultを返します。
  - 失敗：エラー（認証失敗など）、異常CosClientExceptionまたはCosServiceExceptionをスローします。詳細については、異常タイプの説明を参照してください。
- **方法3 （completeMultipartUpload）**
  - 成功：全文のEtagを含むCompleteMultipartUploadResultを返します。 
  - 失敗：エラー（認証失敗など）が発生した場合、異常CosClientExceptionまたはCosServiceExceptionをスローします。詳細については、異常タイプの説明を参照してください。
- **方法4 （listParts）**
  - Success：各パートのETagと番号、および次回のリストの開始マーカーを含むPartListingを返します。
  - 失敗：エラー（認証失敗など）が発生した場合、異常CosClientExceptionまたはCosServiceExceptionをスローします。詳細については、異常タイプの説明を参照してください。
- **方法5 (abortMultipartUpload)**
  - 成功：戻り値がない。
  - 失敗：エラー（認証失敗など）、異常CosClientExceptionまたはCosServiceExceptionをスローします。詳細については、異常タイプの説明を参照してください。
- **例**

```java
// バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名称はこのフォーマットでなければなりません
String bucketName = "movie-1251668577";
// パートを初期化します
InitiateMultipartUploadRequest initRequest =
                new InitiateMultipartUploadRequest(bucketName, key);
InitiateMultipartUploadResult initResponse = cosClient.initiateMultipartUpload(initRequest);
String uploadId = initResponse.getUploadId()
// マルチパートアップロード、最大1000のパートであり、パートサイズは1M * 5Gをサポートします。
// パートサイズを4Mに設定し、全部でn個のパートの場合、1～n-1のパートサイズは同じであり、最後のパートサイズは前のパートサイズ以下です
List<PartETag> partETags = new ArrayList<PartETag>();
int partNumber = 1;
int partSize = 4 * 1024 * 1024;
// partStreamはパートデータの入力ストリームを表し、ストリームサイズはpartSizeです
UploadPartRequest uploadRequest =  new    UploadPartRequest().withBucketName(bucketName).
 withUploadId(uploadId).withKey(key).withPartNumber(partNumber).
  withInputStream(partStream).withPartSize(partSize);  
UploadPartResult uploadPartResult = cosClient.uploadPart(uploadRequest);
String eTag = uploadPartResult.getETag();  // partのEtagを取得します
partETags.add(new PartETag(partNumber, eTag));  // partETagsはアップロードされたすべてのパートのEtag情報を記録します
// ... partNumberの2番目からn番目までのパートをアップロードします

// マルチパートアップロードを完了します。
CompleteMultipartUploadRequest compRequest = new CompleteMultipartUploadRequest(bucketName, key,
           uploadId, partETags);
CompleteMultipartUploadResult result =  cosClient.completeMultipartUpload(compRequest);

// ListPartは、マルチパートアップロードの完了の前またはマルチパートアップロードの中止の前に、uploadIdに対応するアップロードされたパート情報を取得するために使用され、partEtagsを構築するために用いることができます
ListPartsRequest listPartsRequest = new ListPartsRequest(bucket, key, uploadId);
do {
      partListing = cosClient.listParts(listPartsRequest);
      for (PartSummary partSummary : partListing.getParts()) {
           partETags.add(new PartETag(partSummary.getPartNumber(), partSummary.getETag()));
      }
      listPartsRequest.setPartNumberMarker(partListing.getNextPartNumberMarker());
} while (partListing.isTruncated());

// abortMultipartUploadは、完了していないマルチパートアップロードを終了するために使用されます
AbortMultipartUploadRequest abortMultipartUploadRequest = 
  									new AbortMultipartUploadRequest(bucket, key, uploadId);
cosClient.abortMultipartUpload(abortMultipartUploadRequest);
```

### Get Object

ファイルをローカルにダウンロードしますか、またはダウンロードファイルのダウンロード入力ストリームを取得します。

- **方法のプロトタイプ**

```java
// バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名称はこのフォーマットでなければなりません
String bucketName = "movie-1251668577";
// 方法1：ファイルをダウンロードし、かつ入力ストリームを取得します
public COSObject getObject(GetObjectRequest getObjectRequest)
            throws CosClientException, CosServiceException;
// 方法2：ファイルをローカルにダウンロードします。
public ObjectMetadata getObject(GetObjectRequest getObjectRequest, File destinationFile)
            throws CosClientException, CosServiceException;
```

- **パラメータ説明**

| パラメータ名           | パラメータ説明       | パラメータタイプ         |
| ---------------- | -------------- | ---------------- |
| getObjectRequest | ファイルのダウンロードリクエスト| GetObjectRequest |
| destinationFile  | ローカル保存ファイル | File             |

リクエストメンバーの説明：

| リクエストメンバー | 設定方法            | 説明                                                         | タイプ   |
| ------------ | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName   | 構造関数または設定方法 | バケットの命名規則は{name}-{appid}であり、名称は英数字とハイフンで構成されています | String |
| key          | 構造関数または設定方法 | オブジェクトキー（Key）はオブジェクトのバケットにおける一意な識別子です。例えば、オブジェクトのアクセスドメイン名 `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg` において、オブジェクトキーは doc1/pic1.jpg であり、詳細については、 [オブジェクトキー](https://cloud.tencent.com/document/product/436/13324)を参照してください | String |
| range        | 設定方法            | ダウンロード範囲                                             | Long[] |

- **戻り値**
- **方法1（ダウンロード入力ストリームを取得します）**
  - 成功：入力ストリームとファイル属性を含むCOSObjectタイプを返します。
  - 失敗：エラー（認証失敗など）が発生した場合、異常CosClientExceptionまたはCosServiceExceptionをスローします。詳細については、異常タイプの説明を参照してください。
- **方法2 （ファイルをローカルにダウンロードします）**
  - 成功：ファイルのカスタマイズヘッダーとcontent-typeなどの属性を含むファイルの属性objectMetadataを返します。
  - 失敗：エラー（認証失敗など）が発生した場合、異常CosClientExceptionまたはCosServiceExceptionをスローします。詳細については、異常タイプの説明を参照してください。
- **例**

```java
// バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名称はこのフォーマットでなければなりません
String bucketName = "movie-1251668577";
String key = "abc/def.jpg";
// 方法1 ：ダウンロード入力ストリームを取得します
GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
COSObject cosObject = cosClient.getObject(getObjectRequest);
COSObjectInputStream cosObjectInput = cosObject.getObjectContent();

// 方法2：ファイルをローカルにダウンロードします
File downFile = new File("src/test/resources/mydown.txt");
GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
ObjectMetadata downObjectMeta = cosClient.getObject(getObjectRequest, downFile);
```

### Delete Object

COS上のファイルを削除します。

- **方法のプロトタイプ**

```java
// ファイルを削除します
public void deleteObject(String bucketName, String key)
            throws CosClientException, CosServiceException;
```

- **パラメータ説明**

| パラメータ名     | パラメータ説明                                                     | タイプ   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | バケットの命名規則は{name}-{appid}であり、名称は英数字とハイフンで構成されています | String |
| key        | オブジェクトキー（Key）はオブジェクトのバケットにおける一意な識別子です。例えば、オブジェクトのアクセスドメイン名 `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg` において、オブジェクトキーは doc1/pic1.jpg であり、詳細については、 [オブジェクトキー](https://cloud.tencent.com/document/product/436/13324)を参照してください | String |

- **戻り値**
  - 成功：戻り値がない。
  - 失敗：エラー（認証失敗など）が発生した場合、異常CosClientExceptionまたはCosServiceExceptionをスローします。詳細については、異常タイプの説明を参照してください。
- **例**

```java
// COSファイルを削除します
//バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名称はこのフォーマットでなければなりません
String bucketName = "movie-1251668577";
String key = "abc/def.jpg";
cosClient.deleteObject(bucket, key);
```

### Head Object

照合によりCOS上のファイル属性を取得します。

- **方法のプロトタイプ**

```java
// ファイル属性を取得します
public ObjectMetadata getObjectMetadata(String bucketName, String key)
  throws CosClientException, CosServiceException;
```

- **パラメータ説明**

| パラメータ名     | パラメータ説明                                                     | タイプ   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | バケットの命名規則は{name}-{appid}であり、名称は英数字とハイフンで構成されています | String |
| key        | オブジェクトキー（Key）はオブジェクトのバケットにおける一意な識別子です。例えば、オブジェクトのアクセスドメイン名 `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg` において、オブジェクトキーは doc1/pic1.jpg であり、詳細については、 [オブジェクトキー](https://cloud.tencent.com/document/product/436/13324)を参照してください | String |

- **戻り値**
  - 成功：戻り値がない。
  - 失敗：エラー（認証失敗など）が発生した場合、異常CosClientExceptionまたはCosServiceExceptionをスローします。詳細については、異常タイプの説明を参照してください。
- **例**

```java
// COSファイル属性を取得します
//バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名称はこのフォーマットでなければなりません
String bucketName = "movie-1251668577";
String key = "abc/def.jpg";
ObjectMetadata objectMetadata = cosClient.getObjectMetadata(bucketName, key);
```

### Put Object Copy

オブジェクトを新しいパスまたは新しいバケットにコピーします。キャンパス間アカウント間バケット間コピーをサポートし、ソースファイルに対する読み取り権限と目的ファイルに対する書き込み権限を持っている必要があります。最大5Gのファイルコピーをサポートし、5G以上のファイルは、高レベルAPIでコピーしてください。

- **方法のプロトタイプ**

```java
// ファイル属性を取得します
public CopyObjectResult copyObject(CopyObjectRequest copyObjectRequest)
      throws CosClientException, CosServiceException
```

- **パラメータ説明**

| パラメータ名            | パラメータ説明     | パラメータタイプ          |
| ----------------- | ------------ | ----------------- |
| copyObjectRequest | ファイルのコピーリクエスト | CopyObjectRequest |

リクエストメンバーの説明：

| パラメータ名                | パラメータ説明                                                     | タイプ   |
| --------------------- | ------------------------------------------------------------ | ------ |
| sourceBucketRegion    | ソースバケット地域。デフォルト値：現在のclientconfigの地域と一致し、統一的なキャンパス間コピーを表します | String |
| sourceBucketName      | ソースバケット名、バケットの命名規則は{name}-{appid}であり、名称は英数字とハイフンで構成されています | String |
| sourceKey             |ソースオブジェクトキー、オブジェクトキー（Key）はオブジェクトのバケットにおける一意な識別子です。例えば、オブジェクトのアクセスドメイン名 `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg` において、オブジェクトキーは doc1/pic1.jpg であり、詳細については、 [オブジェクトキー](https://cloud.tencent.com/document/product/436/13324)を参照してください | String |
| sourceVersionId |ソースファイルのバージョンID（バージョン制御が有効になったソースバケットに適用される）。デフォルト値：ソースファイルの現在の最新バージョン | String |
| destinationBucketName | 目的バケット名、バケットの命名規則は{name}-{appid}であり、名称は英数字とハイフンで構成されています | String |
| destinationKey        | 目的オブジェクトキー、オブジェクトキー（Key）はオブジェクトのバケットにおける一意な識別子です。例えば、オブジェクトのアクセスドメイン名 `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg` において、オブジェクトキーは doc1/pic1.jpg であり、詳細については、 [オブジェクトキー](https://cloud.tencent.com/document/product/436/13324)を参照してください | String |
| storageClass          | コピーされた目的ファイルのストレージタイプ（標準、低頻度、ニアライン）、デフォルト値：標準 | String |

- **戻り値**
  - 成功：新しいファイルのETagなどの情報を含むCopyObjectResultを返します。
  - 失敗：エラー（認証失敗など）が発生した場合、異常CosClientExceptionまたはCosServiceExceptionをスローします。詳細については、異常タイプの説明を参照してください。
- **例**

```java
// 同じキャンパス同じアカウントコピー
// ソースバケット、バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名称はこのフォーマットでなければなりません
String srcBucketName = "srcBucket-1251668577";
// コピーされるソースファイル
String srcKey = "aaa/bbb.txt";
// 目的バケット、バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名称はこのフォーマットでなければなりません
String destBucketName = "destBucket-1251668577";
// コピーされる目的ファイル
String destKey = "ccc/ddd.txt";
CopyObjectRequest copyObjectRequest = new CopyObjectRequest(srcBucketName, srcKey, destBucketName, destKey);
CopyObjectResult copyObjectResult = cosClient.copyObject(copyObjectRequest);

// アカウント間キャンパス間コピー（ソースファイルに対する読み取り権限と目的ファイルに対する書き込み権限を持っている必要があります）
String srcBucketNameOfDiffAppid = "srcBucket-125100000";
Region srcBucketRegion = new Region("ap-shanghai");
copyObjectRequest = new CopyObjectRequest(srcBucketRegion, srcBucketNameOfDiffAppid, srcKey, destBucketName, destKey);
copyObjectResult = cosClient.copyObject(copyObjectRequest);
```

### Set Object ACL

オブジェクトのアクセス制御権限リスト（Access Control List）を設定します。Set Object ACL は、既存の権限設定を上書きする上書き操作です。

> !現在のアクセスポリシーエントリは1000に制限され、オブジェクトのACL制御を行う必要がない場合、設定しないでください。デフォルトではバケット権限を継承します。

ACLには、事前定義権限ポリシー（CannedAccessControlList）またはカスタマイズ権限制御（AccessControlList）が含まれています。2種類の権限が同時に設定されている場合、事前定義ポリシーが無視され、カスタマイズポリシーが優先されます。権限の詳細については、権限セクションを参照してください。

- **方法のプロトタイプ**

```java
// 方法1（カスタマイズポリシーを設定します）
public void setObjectAcl(String bucketName, String key, AccessControlList acl)
       throws CosClientException, CosServiceException
// 方法2（事前定義ポリシーを設定します）
public void setObjectAcl(String bucketName, String key, CannedAccessControlList acl)
       throws CosClientException, CosServiceException
// 方法3（以上の2種類の方法のパッケージであり、2種類のポリシーの設定が含まれ、同時に設定されている場合、カスタマイズポリシーが優先されます）
public void setObjectAcl(SetObjectAclRequest setObjectAclRequest)
  throws CosClientException, CosServiceException;
```

- **パラメータ説明**
  - **方法3**パラメータには1と2の両方が含まれるため、方法3を例として紹介します。

| パラメータ名              | パラメータ説明  | タイプ                |
| ------------------- | -------- | ------------------- |
| SetObjectAclRequest | リクエストタイプ   | setObjectAclRequest |

リクエストメンバーの説明：

| リクエストメンバー | 設定方法            | 説明                                                         | タイプ                    |
| ------------ | ------------------- | ------------------------------------------------------------ | ----------------------- |
| bucketName   | 構造関数または設定方法 | バケットの命名規則は{name}-{appid}であり、名称は英数字とハイフンで構成されています | String                  |
| key          | 構造関数または設定方法 | オブジェクトキー（Key）はオブジェクトのバケットにおける一意な識別子です。例えば、オブジェクトのアクセスドメイン名 `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg` において、オブジェクトキーは doc1/pic1.jpg であり、詳細については、 [オブジェクトキー](https://cloud.tencent.com/document/product/436/13324)を参照してください | String                  |
| acl          | 構造関数または設定方法 | カスタマイズ権限ポリシー                                               | AccessControlList       |
| cannedAcl    | 構造関数または設定方法 | パブリック読み取り、パブリック読み書き、プライベート読み取りなどの事前定義ポリシー                         | CannedAccessControlList |

- **戻り値**
  - 成功：戻り値がない。
  - 失敗：エラー（認証失敗など）が発生した場合、異常CosClientExceptionまたはCosServiceExceptionをスローします。詳細については、異常タイプの説明を参照してください。
- **例**

```java
// バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名称はこのフォーマットでなければなりません
String bucketName = "movie-1251668577";
String key = "abc/def.jpg";
// カスタマイズACLを設定します
AccessControlList acl = new AccessControlList();
Owner owner = new Owner();
owner.setId("qcs::cam::uin/2779643970:uin/2779643970");
acl.setOwner(owner);
String id = "qcs::cam::uin/2779643970:uin/734505014";
UinGrantee uinGrantee = new UinGrantee("qcs::cam::uin/2779643970:uin/734505014");
uinGrantee.setIdentifier(id);
acl.grantPermission(uinGrantee, Permission.FullControl);
cosClient.setObjectAcl(buckeName, key, acl);

// 事前定義ACLを設定します
// プライベート読み書きを設定します（オブジェクトの権限はデフォルトでバケットの権限を統合します）
cosClient.setObjectAcl(buckeName, key, CannedAccessControlList.Private);
// パブリック読み取りとプライベート書き込みを設定します
cosClient.setObjectAcl(buckeName, key, CannedAccessControlList.PublicRead);
// パブリック読み書きを設定します
cosClient.setObjectAcl(buckeName, key, CannedAccessControlList.PublicReadWrite);
```

### Get Object ACL

オブジェクトのアクセスポリシーACLを照合します。

- **方法のプロトタイプ**

```java
public AccessControlList getObjectAcl(String bucketName, String key)
  throws CosClientException, CosServiceException;
```

- **パラメータ説明**

| パラメータ名     | パラメータ説明                                                     | タイプ   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | バケットの命名規則は{name}-{appid}であり、名称は英数字とハイフンで構成されています | String |
| key        | オブジェクトキー（Key）はオブジェクトのバケットにおける一意な識別子です。例えば、オブジェクトのアクセスドメイン名 `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg` において、オブジェクトキーは doc1/pic1.jpg であり、詳細については、 [オブジェクトキー](https://cloud.tencent.com/document/product/436/13324)を参照してください | String |

- **戻り値**
  - 成功：オブジェクトが位置するACLを返します。
  - 失敗：エラー（認証失敗など）が発生した場合、異常CosClientExceptionまたはCosServiceExceptionをスローします。詳細については、異常タイプの説明を参照してください。
- **例**

```java
// バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名称はこのフォーマットでなければなりません
String bucketName = "movie-1251668577";
String key = "abc/def.jpg";
AccessControlList acl = cosClient.getObjectAcl(bucketName, key);
```

## 事前署名リンクを生成します

COSClientは、ダウンロードまたはアップロードのためにクライアントに配布できる事前署名のURLを生成または作成します。しかしながら、ユーザーのファイルがプライベート読み取り権限である場合、事前署名リンクは一定の有効期間しかありません。

- **方法のプロトタイプ**

```java
// 事前署名付きURLを作成します
public URL generatePresignedUrl(GeneratePresignedUrlRequest req) throws CosClientException
```

- **パラメータ説明**

| パラメータ名 | パラメータ説明     | タイプ                        |
| ------ | ------------ | --------------------------- |
| req    | 事前署名リクエストタイプ | GeneratePresignedUrlRequest |

リクエストメンバーの説明：

| Requestメンバー    | 設定方法            | 説明                                                         | タイプ                    |
| --------------- | ------------------- | ------------------------------------------------------------ | ----------------------- |
| method          | 構造関数または設定方法 | HTTP方法、 PUT（アップロード用）、GET（ダウンロード用）、DELETE（削除用）    | HttpMethodName          |
| bucketName      | 構造関数または設定方法 | バケットの命名規則は{name}-{appid}であり、名称は英数字とハイフンで構成されています | String                  |
| key             | 構造関数または設定方法 | オブジェクトキー（Key）はオブジェクトのバケットにおける一意な識別子です。例えば、オブジェクトのアクセスドメイン名 `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg` において、オブジェクトキーは doc1/pic1.jpg であり、詳細については、 [オブジェクトキー](https://cloud.tencent.com/document/product/436/13324)を参照してください | String                  |
| expiration      | 設定方法            | 署名の期限切れ時間                                               | Date                    |
| contentType     | 設定方法            | 署名されるリクエストにおけるContent-Type                                | String                  |
| contentMd5      | 設定方法            | 署名されるリクエストにおけるContent-Md5                                 | String                  |
| responseHeaders | 設定方法            | 署名のダウンロードリクエストにおける上書きされる返されたHTTPヘッダー                       | ResponseHeaderOverrides |

- **戻り値**

URL

- **例**

例1：署名付きダウンロードリンクを生成し、サンプルコードは以下のとおりです：

```java
// ダウンロードリンクを生成します
// バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名はこのフォーマットでなければなりません
String bucketName = "mybucket-1251668577";
String key = "aaa.txt";
GeneratePresignedUrlRequest req =
        new GeneratePresignedUrlRequest(bucketName, key, HttpMethodName.GET);
// 署名の期限切れ時間を設定し（オプション）、設定していない場合、デフォルトでは、ClientConfigにおける署名の期限切れ時間（1時間）を使用します
// ここでの署名が30分後に期限切れになるように設定します
Date expirationDate = new Date(System.currentTimeMillis() + 30L * 60L * 1000L);
req.setExpiration(expirationDate);
URL downloadUrl = cosClient.generatePresignedUrl(req);
String downloadUrlStr = downloadUrl.toString();
```

例2：署名付きダウンロードリンクを生成し、かつcontent-type、content-languageなどの返される共通ヘッダーを上書きするように設定し、サンプルコードは以下のとおりです：

```java
// バケットの命名規則は{name}-{appid}であり、名称は英数字とハイフンで構成されています 
String bucketName = "mybucket-1251668577";
String key = "aaa.txt";
GeneratePresignedUrlRequest req =
        new GeneratePresignedUrlRequest(bucketName, key, HttpMethodName.GET);
// ダウンロード時に返されるhttpヘッダーを設定します
ResponseHeaderOverrides responseHeaders = new ResponseHeaderOverrides();
String responseContentType = "image/x-icon";
String responseContentLanguage = "zh-CN";
String responseContentDispositon = "filename=\"abc.txt\"";
String responseCacheControl = "no-cache";
String cacheExpireStr =
        DateUtils.formatRFC822Date(new Date(System.currentTimeMillis() + 24L * 3600L * 1000L));
responseHeaders.setContentType(responseContentType);
responseHeaders.setContentLanguage(responseContentLanguage);
responseHeaders.setContentDisposition(responseContentDispositon);
responseHeaders.setCacheControl(responseCacheControl);
responseHeaders.setExpires(cacheExpireStr);
req.setResponseHeaders(responseHeaders);
// 署名の期限切れ時間を設定し（オプション）、設定していない場合、デフォルトでは、ClientConfigにおける署名の期限切れ時間（1時間）を使用します
// ここでの署名が30分後に期限切れになるように設定します
Date expirationDate = new Date(System.currentTimeMillis() + 30L * 60L * 1000L);
req.setExpiration(expirationDate);
URL url = cosClient.generatePresignedUrl(req);
```

例3：署名されたリンクを必要としないパブリックバケット（匿名読み取り可能）を生成し、サンプルコードは以下のとおりです：

```java
// 匿名のリクエスト署名を生成し、匿名のcosClientを再初期化する必要があります
//1 ユーザー身元情報を初期化し、匿名身元であればak skをインバウンドする必要がありません
COSCredentials cred = new AnonymousCOSCredentials();
// 2 バケットのエリアを設定し、COS地域の略称については、以下を参照してください：https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3 cosクライアントの生成
COSClient cosClient = new COSClient(cred, clientConfig);
// バケット名はappidを含む必要があります
String bucketName = "mybucket-1251668577";

String key = "aaa.txt";
GeneratePresignedUrlRequest req =
        new GeneratePresignedUrlRequest(bucketName, key, HttpMethodName.GET);
URL url = cosClient.generatePresignedUrl(req);

System.out.println(url.toString());

cosClient.shutdown();
```

例4：事前署名されたアップロードリンクをいくつか生成し、クライアントに直接配布してファイルをアップロードすることができ、サンプルコードは以下のとおりです：

```java
// バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名称はこのフォーマットでなければなりません
String bucketName = "mybucket-1251668577";

String key = "aaa.txt";
// 署名の期限切れ時間を設定し（オプション）、設定していない場合、デフォルトでは、ClientConfigにおける署名の期限切れ時間（1時間）を使用します
//ここでの署名が30分後に期限切れになるように設定します
Date expirationTime = new Date(System.currentTimeMillis() + 30L * 60L * 1000L);
URL url = cosClient.generatePresignedUrl(bucketName, key, expirationTime, HttpMethodName.PUT);
```

## 署名の生成

COSSignerタイプは、モバイル側SDKに配布してファイルのアップロードおよびダウンロードを行うためのCOS署名の作成方法を提供します。
署名されたパスは、配布後に操作されるキーと一致します。

- **方法のプロトタイプ**

```java
// COS署名を作成します
public String buildAuthorizationStr(HttpMethodName methodName, String resouce_path,
        COSCredentials cred, Date expiredTime);

// COS署名を作成します
//第２の方法は第１の方法に比べて一部のHTTP Header およびすべてのインバウンドされたURLにおけるパラメータに対する署名を追加提供します。
// より複雑な署名制御に使用され、生成された署名はアップロードとダウンロードなどの操作の時に対応するヘッダーとパラメータを含めなければなりません。
public String buildAuthorizationStr(HttpMethodName methodName, String resouce_path,
        Map<String, String> headerMap, Map<String, String> paramMap, COSCredentials cred,
        Date expiredTime);
```

- **パラメータ説明**

| パラメータ名 | パラメータ説明                                                     | タイプ           |
| ------------ | ------------------------------------------------------------ | -------------- |
| methodName   | HTTPリクエスト方法、PUT、GET、DELETE、HEAD、POSTを設定できます            | HttpMethodName |
| resouce_path |署名されるパスは、アップロードされたファイルのキーと同様に、/で始まる必要があります。                 | HttpMethodName |
| cred         | 暗号鍵情報                                                     | COSCredentials |
| expiredTime  | 期限切れ時間                                                     | Date           |
| headerMap    | 署名されるHTTP Header map、インバウンドされたContent-Type、Content-Md5とxで始まるヘッダーのみを署名します | Map 
| paramMap     | 署名されるURL Param map                                        | Map            |

- **戻り値**
String

- **例**

例1：アップロード署名を生成します

```java
// バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名称はこのフォーマットでなければなりません
String bucketName = "mybucket-1251668577";
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
COSSigner signer = new COSSigner();
//期限切れ時間を1時間に設定します
Date expiredTime = new Date(System.currentTimeMillis() + 3600L * 1000L);
// 署名されるキー、生成された署名はこのキーに対応するアップロードにのみ用いることができます
String key = "/aaa.txt";
String sign = signer.buildAuthorizationStr(HttpMethodName.PUT, key, cred, expiredTime);
```

例2：ダウンロード署名を生成します

```java
// バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名称はこのフォーマットでなければなりません
String bucketName = "mybucket-1251668577";
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
COSSigner signer = new COSSigner();
//期限切れ時間を1時間に設定します
Date expiredTime = new Date(System.currentTimeMillis() + 3600L * 1000L);
// 署名されるキー、生成された署名はこのキーに対応するダウンロードにのみ用いることができます
String key = "/aaa.txt";
String sign = signer.buildAuthorizationStr(HttpMethodName.GET, key, cred, expiredTime);
```

例3：削除署名を生成します

```java
// バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名称はこのフォーマットでなければなりません
String bucketName = "mybucket-1251668577";
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
COSSigner signer = new COSSigner();
//期限切れ時間を1時間に設定します
Date expiredTime = new Date(System.currentTimeMillis() + 3600L * 1000L);
// 署名されるキー、生成された署名はこのキーに対応する削除にのみ用いることができます
String key = "/aaa.txt";
String sign = signer.buildAuthorizationStr(HttpMethodName.DELETE, key, cred, expiredTime);
```

##高レベルAPIによるファイルのアップロード（推奨）

高レベルAPIはタイプTransferMangerでアップロードおよびダウンロードAPIをカプセル化することにより、内部にスレッドプールを備え、ユーザーのアップロードおよびダウンロードリクエストを受け入れ、したがって、ユーザーはタスクを非同期的に提出することを選択できます。

```java
// スレッドプールサイズについて、クライアントとCOSネットワークが十分である（例えば、Tencent CloudのCVMを使用して、同じキャンパスでCOSをアップロードする）場合、ネットワークリソースを十分に利用できるように16または32に設定することをお勧めします
// パブリックネットワークで伝送し、かつネットワーク帯域幅の品質が低い場合、ネットワーク速度が遅いことによりリクエストタイムアウトになることを回避するために、この値を減らすことをお勧めします。
ExecutorService threadPool = Executors.newFixedThreadPool(32);
// threadpoolをインバウンドし、スレッドプールをインバウンドしない場合、デフォルトでは、TransferManagerにシングルスレッドのスレッドプールが生成されます。
TransferManager transferManager = new TransferManager(cosClient, threadPool);
// .....（下記のように、アップロードおよびダウンロードリクエストを送信します）
// TransferMangerを終了します
transferManager.shutdownNow();
```

### ファイルのアップロード

アップロードAPIは、ユーザーファイルのサイズに応じて簡単アップロードとマルチパートアップロードを自動的に選択し、ユーザーにとって使いやすくなっています。ユーザーはマルチパートアップロードのすべてのステップを気にする必要がありません。

Tips 他の設定属性、ストレージタイプ、MD5チェックなどについては、Put Object Apiを参照してください。

- **方法のプロトタイプ**

```java
// ファイルのアップロード
public Upload upload(final PutObjectRequest putObjectRequest)
            throws CosServiceException, CosClientException;
```

- **パラメータ説明**

| パラメータ名           | パラメータ説明     | パラメータタイプ         |
| ---------------- | ------------ | ---------------- |
| putObjectRequest | ファイルのアップロードのリクエスト| PutObjectRequest |

リクエストメンバーの説明：

| リクエストメンバー | 設定方法            | 説明                                                         | タイプ           |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |
| bucketName   | 構造関数または設定方法 | バケットの命名規則は{name}-{appid}であり、名称は英数字とハイフンで構成されています | String         |
| key          | 構造関数または設定方法 | オブジェクトキー（Key）はオブジェクトのバケットにおける一意な識別子です。例えば、オブジェクトのアクセスドメイン名 `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg` において、オブジェクトキーは doc1/pic1.jpg であり、詳細については、 [オブジェクトキー](https://cloud.tencent.com/document/product/436/13324)を参照してください | String         |
| file         | 構造関数または設定方法 | ローカルファイル                                                     | File           |
| input        | 構造関数または設定方法 | 入力ストリーム                                                       | InputStream    |
| metadata     | 構造関数または設定方法 | ファイルのメタ情報                                                 | ObjectMetadata |

- **戻り値**
  - 成功：Uploadを返し、アップロードが終了したかどうかを照合でき、アップロードの終了を同期的に待つこともできます。
  - 失敗：エラー（認証失敗など）が発生した場合、異常CosClientExceptionまたはCosServiceExceptionをスローします。詳細については、異常タイプの説明を参照してください。
- **例**

```java
// バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名称はこのフォーマットでなければなりません
String bucketName = "movie-1251668577";
String key = "/mypic.jpg";
File localFile = new File("/data/dog.jpg");
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, file);
// ローカルファイルをアップロードします
Upload upload = transferManager.upload(putObjectRequest);
 // 伝送の終了を待ちます（アップロードの終了を同期的に待とうとする場合、waitForCompletionを呼び出します）
UploadResult uploadResult = upload.waitForUploadResult();
```

### ファイルのダウンロード

COS上のファイルをローカルにダウンロードします。

- **方法のプロトタイプ**

```java
// ファイルのダウンロード
public Download download(final GetObjectRequest GetObjectRequest, final File file);
```

- **パラメータ説明**

| パラメータ名           | パラメータ説明           | パラメータタイプ         |
| ---------------- | ------------------ | ---------------- |
| getObjectRequest | ファイルのダウンロードリクエスト       | GetObjectRequest |
| file             | ローカルにダウンロードされるファイル | File             |

リクエストメンバーの説明：

| リクエストメンバー | 設定方法            | 説明                                                         | タイプ   |
| ------------ | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName   | 構造関数または設定方法 | バケットの命名規則は{name}-{appid}であり、名称は英数字とハイフンで構成されています | String |
| key          | 構造関数または設定方法 | オブジェクトキー（Key）はオブジェクトのバケットにおける一意な識別子です。例えば、オブジェクトのアクセスドメイン名 `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg` において、オブジェクトキーは doc1/pic1.jpg であり、詳細については、 [オブジェクトキー](https://cloud.tencent.com/document/product/436/13324)を参照してください | String |
| range        | 設定方法            | ダウンロード範囲                                            | Long[] |

- **戻り値**
  - 成功：Downloadを返し、ダウンロードが終了したかどうかを照合でき、ダウンロードの終了を同期的に待つこともできます。
  - 失敗：エラー（認証失敗など）が発生した場合、異常CosClientExceptionまたはCosServiceExceptionをスローします。詳細については、異常タイプの説明を参照してください。
- **例**

```java
// バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名称はこのフォーマットでなければなりません
String bucketName = "movie-1251668577";
String key = "/mypic.jpg";
File localDownFile = new File("/data/dog.jpg");
GetObjectRequest getObjectRequest = new GetObjectRequest(bucket, key);
// ファイルのダウンロード
Download download = transferManager.download(getObjectRequest, localDownFile);
 // 伝送の終了を待ちます（アップロードの終了を同期的に待とうとする場合、waitForCompletionを呼び出します）
download.waitForCompletion();
```

###ファイルのコピー

copyAPIは、ファイルサイズに応じてcopyまたはパートコピーを自動的に選択することをサポートし、ユーザーはコピーのファイルサイズを気にする必要がありません。

- **方法のプロトタイプ**

```java
// ファイルのアップロード
public Copy copy(final CopyObjectRequest copyObjectRequest);
```

- **パラメータ説明**

| パラメータ名            | パラメータ説明     | パラメータタイプ          |
| ----------------- | ------------ | ----------------- |
| copyObjectRequest | ファイルのコピーリクエスト | CopyObjectRequest |

リクエストメンバーの説明：

| パラメータ名                | パラメータ説明                                                     | タイプ   |
| --------------------- | ------------------------------------------------------------ | ------ |
| sourceBucketRegion    | ソースバケット地域。デフォルト値：現在のclientconfigの地域と一致し、統一的なキャンパス間コピーを表します | String |
| sourceBucketName      | ソースバケット名、バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名称はこのフォーマットでなければなりません | String |
| sourceKey             |ソースオブジェクトキー、オブジェクトキー（Key）はオブジェクトのバケットにおける一意な識別子です。例えば、オブジェクトのアクセスドメイン名 `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg` において、オブジェクトキーは doc1/pic1.jpg であり、詳細については、 [オブジェクトキー](https://cloud.tencent.com/document/product/436/13324)を参照してください | String |
| sourceVersionId |ソースファイルのバージョンID（バージョン制御が有効になったソースバケットに適用される）。デフォルト値：ソースファイルの現在の最新バージョン | String |
| destinationBucketName | 目的バケット名、バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名称はこのフォーマットでなければなりません | String |
| destinationKey        | 目的オブジェクトキー、オブジェクトキー（Key）はオブジェクトのバケットにおける一意な識別子です。例えば、オブジェクトのアクセスドメイン名 `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg` において、オブジェクトキーは doc1/pic1.jpg であり、詳細については、 [オブジェクトキー](https://cloud.tencent.com/document/product/436/13324)を参照してください | String |
| storageClass          | コピーされた目的ファイルのストレージタイプ（標準、低頻度、ニアライン）、デフォルト値：標準 | String |

- **戻り値**
  - 成功：コピーを返し、コピーが終了したかどうかを照合でき、アップロードの終了を同期的に待つこともできます。
  - 失敗：エラー（認証失敗など）が発生した場合、異常CosClientExceptionまたはCosServiceExceptionをスローします。詳細については、異常タイプの説明を参照してください。
- **例**

```java
// コピーされるバケット地域、キャンパス間コピーをサポートします
Region srcBucketRegion = new Region("ap-shanghai");
// ソースバケット、バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名称はこのフォーマットでなければなりません
String srcBucketName = "srcBucket-1251668577";
// コピーされるソースファイル
String srcKey = "aaa/bbb.txt";
// 目的バケット、バケットの命名規則は{name}-{appid}であり、ここで記入するバケット名称はこのフォーマットでなければなりません
String destBucketName = "destBucket-1251668577";
// コピーされる目的ファイル
String destKey = "ccc/ddd.txt";

// ソースファイル情報を取得するためのsrcCOSClientを生成します
COSClient srcCOSClient = new COSClient(cred, new ClientConfig(srcBucketRegion));
CopyObjectRequest copyObjectRequest = new CopyObjectRequest(srcBucketRegion, srcBucketName,
        srcKey, destBucketName, destKey);
try {
    Copy copy = transferManager.copy(copyObjectRequest, srcCOSClient, null);
    // 非同期結果copyを返し、waitForCopyResultを同期的に呼び出してcopyの終了を待つことができ、成功した場合、CopyResultを返し、失敗した場合、異常をスローします。
    CopyResult copyResult = copy.waitForCopyResult();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}
```

## 権限の設定

COS内の権限は、SET/GET Object ACLおよびSET/GET Bucket ACLにより設定・取得されます。主な2つのタイプであるAccessControlListおよびCannedAccessListにより設定・取得されます。オブジェクトはデフォルトではバケットの権限を継承し、現在、COSは、アカウント（appid）に対して1000のACLを設定することしかサポートせず、したがって、権限の数がしきい値を超えないように、バケットの権限と一致しない個々のオブジェクトのみに対してACLを設定することをお勧めし、上限のないACL機能のサポートは現在開発中です。

### AccessControlList

あるユーザーに対するポリシー制御を設定するためのカスタマイズアクセス制御ポリシー。

AccessControlListタイプメンバー

| メンバー名         | 説明                            | タイプ     |
| -------------- | ------------------------------- | -------- |
| List＆lt; Grant> | 許可されるすべての情報を含む            | 配列     |
| owner          | オブジェクトまたはオーナーの所有者を表す | オーナータイプ |

Grantタイプメンバー

| メンバー名     | 説明                                       | タイプ       |
| ---------- | ------------------------------------------ | ---------- |
| grantee    | 権限が付与された者の身元情報                         | Grantee    |
| permission | 承認された権限情報（例：読み取り可能、書き込み可能、読み書き可能） | Permission |

オーナータイプメンバー

| メンバー名      | 説明                           | タイプ   |
| ----------- | ------------------------------ | ------ |
| id          | 所有者の身元情報               | String |
| displayname | 所有者の名前（現在IDと同じである） | String |

- **例**

```java
// 権限情報内の身元情報にはフォーマット要件があり、ルートアカウントとサブアカウントのパラダイムは以下のとおりです：
//以下のroot_uinとsub_uinはいずれも有効なQQ番号でなければなりません
// ルートアカウントqcs::cam::uin/<root_uin>:uin/<root_uin>は、ルートアカウントにroot_uinユーザーを付与することを表します（即ち、前後に記入されたuinが同じである）
// 例えば、qcs::cam::uin/2779643970:uin/2779643970
// サブアカウントqcs::cam::uin/<root_uin>:uin/<sub_uin>はroot_uinのサブアカウントにsub_uinユーザーを付与することを表します
// 例えば、qcs::cam::uin/2779643970:uin/73001122 

AccessControlList acl = new AccessControlList();
Owner owner = new Owner();
// オーナー情報を設定し、オーナーはルートアカウントにしかなれません
owner.setId("qcs::cam::uin/2779643970:uin/2779643970");
acl.setOwner(owner);

// ルートアカウント73410000に読み書き権限を付与します
UinGrantee uinGrantee1 = new UinGrantee("qcs::cam::uin/73410000:uin/73410000");
acl.grantPermission(uinGrantee1, Permission.FullControl);
// 2779643970のサブアカウント72300000に読み取り権限を付与します
UinGrantee uinGrantee2 = new UinGrantee("qcs::cam::uin/2779643970:uin/72300000");
acl.grantPermission(uinGrantee2, Permission.Read);
// 2779643970のサブアカウント7234444に書き込み権限を付与します
UinGrantee uinGrantee3 = new UinGrantee("qcs::cam::uin/7234444:uin/7234444");
acl.grantPermission(uinGrantee3, Permission.Write);

// オブジェクトのaclを設定します
cosClient.setObjectAcl(bucket, key, acl);

```

### CannedAccessControlList

CannedAccessControlListは、全員に対するプリセットポリシーを表します。列挙型であり、列挙値は以下のとおりです。

| 列挙値          | 説明                                             |
| --------------- | ------------------------------------------------ |
| Private         | プライベート読み書き（オーナーだけは読み書き可能である）                  |
PublicRead | パブリック読み取りとプライベート書き込み（オーナーは読み書き可能であり、他のユーザーは読み取り可能である）|
| PublicReadWrite | パブリック読み書き（即ち、全員は読み書き可能である）                   |

## クライアント暗号化

Java SDKは、クライアント暗号化をサポートし、ファイルを暗号化した後にアップロードし、かつダウンロードする時に復号化します。クライアント暗号化は、対称AESおよび非対称RSA暗号化をサポートします。
ここで、対称と非対称は毎回生成されたランダム暗号鍵を暗号化するためにのみ使用され、ファイルデータに対する暗号化には常にAES256対称暗号化を使用します。
クライアント暗号化は機密データを保存する顧客に適し、クライアント暗号化は一部のアップロード速度を犠牲にし、SDK内部はマルチパートアップロードに対してシリアル方式でアップロードします。

### クライアント暗号化を使用する前の準備

クライアント暗号化内部はAES256でデータを暗号化し、デフォルトでは、JDK6 - JDK8の初期バージョンは、256ビット暗号化をサポートせず、ランタイムにおいて以下の異常`java.security.InvalidKeyException: Illegal key size or default parameters`が報告される場合、OracleのJCE無制限強度管轄ポリシーファイルを追加し、JRE環境に展開する必要があります。現在使用されているJDKバージョンに従って対応するファイルをそれぞれダウンロードし、解凍した後にJAVA_HOME内のjre/lib/securityディレクトリに保存してください。

1. [JDK6 JCEパッチ](http://www.oracle.com/technetwork/java/javase/downloads/jce-6-download-429243.html)。
2. [JDK7 JCEパッチ](http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html)。
3. [JDK8 JCEパッチ](http://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html)。

### アップロード暗号化プロセス

1. 毎回ファイルオブジェクトをアップロードする前に、対称暗号鍵をランダムに生成し、ランダムに生成された暗号鍵をユーザーにより提供された対称または非対称暗号鍵で暗号化し、暗号化結果のbase64コードをオブジェクトのメタ情報に保存します。
2. ファイルオブジェクトをアップロードし、アップロードする時にメモリ内でAES256アルゴリズムで暗号化します。

### ダウンロード復号化プロセス

1. ファイルのメタ情報から暗号化に必要な情報を取得し、base64を解読した後にユーザー暗号鍵で復号化し、当時データを暗号化する暗号鍵を取得します。
2. ダウンロード入力ストリームに対して暗号鍵でAES256による復号を行い、復号されたファイル入力ストリームを取得します。


- **例**

例1：毎回生成されたランダム暗号鍵を対称AES256で暗号化する例、完全なサンプルコードについては、[クライアント対称暗号鍵による暗号化の完全な例](https://github.com/tencentyun/cos-java-sdk-v5/blob/master/src/main/java/com/qcloud/cos/demo/SymmetricKeyEncryptionClientDemo.java)を参照してください。

```java
// ユーザー身元情報（secretId、secretKey）を初期化します
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXXXXXXXXXX",
		"YYZZZZZZZZZZZZZZZZZ");
// バケットの地域を設定し、COS地域の略称については、https://www..com/document/product/436/6224を参照してください
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));

// ファイルに保存された暗号鍵をロードし、存在しない場合、まず、buildAndSaveSymmetricKeyで暗号鍵を生成してください
// buildAndSaveSymmetricKey();
SecretKey symKey = loadSymmetricAESKey();

EncryptionMaterials encryptionMaterials = new EncryptionMaterials(symKey);
// AES/GCMモードを使用し、かつ暗号化された情報をファイルのメタ情報に保存します
CryptoConfiguration cryptoConf = new CryptoConfiguration(CryptoMode.AuthenticatedEncryption)
		.withStorageMode(CryptoStorageMode.ObjectMetadata);

// 暗号化クライアントEncryptionClientを生成し、EncryptionClientは、COSClientのサブタイプであり、COSClientがサポートするすべてのAPIをサポートします。
// EncryptionClientはCOSClientのアップロードおよびダウンロードロジックを上書きし、操作内部は暗号化操作を実行しますが、他の操作実行ロジックはCOSClientと一致します
COSEncryptionClient cosEncryptionClient =
		new COSEncryptionClient(new COSStaticCredentialsProvider(cred),
				new StaticEncryptionMaterialsProvider(encryptionMaterials), clientConfig,
				cryptoConf);

// ファイルのアップロード
// ここで、putObjectの例が示され、高レベルAPIによるアップロードに対して、TransferManagerを生成する時にCOSEncryptionClientオブジェクトをインバウンドするだけでよいです
String bucketName = "mybucket-1251668577";
String key = "xxx/yyy/zzz.txt";
File localFile = new File("src/test/resources/plain.txt");
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
cosEncryptionClient.putObject(putObjectRequest);
```

例2：毎回生成されたランダム暗号鍵を非対称RSAで暗号化する例、完全なサンプルコードについては、[クライアント非対称暗号鍵による暗号化の完全な例](https://github.com/tencentyun/cos-java-sdk-v5/blob/master/src/main/java/com/qcloud/cos/demo/AsymmetricKeyEncryptionClientDemo.java)を参照してください。

```java
// ユーザー身元情報（secretId、secretKey）を初期化します
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXXXXXXXXXXXXXX",
		"YYZZZZZZZZZZZZZZZZZZ");
// バケットの地域を設定し、COS地域の略称については、以下を参照してください：https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));


// ファイルに保存された暗号鍵をロードし、存在しない場合、まず、buildAndSaveAsymKeyPairで暗号鍵を生成してください
buildAndSaveAsymKeyPair();
KeyPair asymKeyPair = loadAsymKeyPair();

EncryptionMaterials encryptionMaterials = new EncryptionMaterials(asymKeyPair);
// AES/GCMモードを使用し、かつ暗号化された情報をファイルのメタ情報に保存します
CryptoConfiguration cryptoConf = new CryptoConfiguration(CryptoMode.AuthenticatedEncryption)
		.withStorageMode(CryptoStorageMode.ObjectMetadata);

// 暗号化クライアントEncryptionClientを生成し、COSEncryptionClientは、COSClientのサブタイプであり、COSClientがサポートするすべてのAPIをサポートします。
//EncryptionClientはCOSClientのアップロードおよびダウンロードロジックを上書きし、操作内部は暗号化操作を実行しますが、他の操作実行ロジックはCOSClientと一致します
COSEncryptionClient cosEncryptionClient =
		new COSEncryptionClient(new COSStaticCredentialsProvider(cred),
				new StaticEncryptionMaterialsProvider(encryptionMaterials), clientConfig,
				cryptoConf);

// ファイルのアップロード
// ここで、putObjectの例が示され、 高レベルAPIによるアップロードに対して、TransferManagerを生成する時にCOSEncryptionClientオブジェクトをインバウンドするだけでよいです
String bucketName = "mybucket-1251668577";
String key = "xxx/yyy/zzz.txt";
File localFile = new File("src/test/resources/plain.txt");
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
cosEncryptionClient.putObject(putObjectRequest);
```

## 異常説明

SDK失敗の場合、スローされた異常はいずれもRuntimeExcpetionであり、現在、SDKの一般的な異常はCosClientException、CosServiceException、およびIllegalArgumentExceptionです。

### CosClientException

クライアント異常は、クライアントの原因でサーバーとの正常な対話を完了できないことによる失敗（例えば、クライアントがサーバーに接続できず、サーバーから返されたデータを解析できず、ローカルファイルの読み取りにIO異常が発生した）を指すために使用されます。CosClientExceptionはRuntimeExceptionから統合され、カスタマイズされたメンバー変数を有さず、使用方法はRuntimeExceptionと同じです。

### CosServiceException

CosServiceExceptionサービス異常は、対話を正常に完了したが、操作が失敗したシナリオを指すために使用されます。例えば、クライアントが存在しないバケットにアクセスし、存在しないファイルを削除し、ある操作を実行する権限を有さず、サーバー故障異常等です。CosServiceExceptionには、サーバーから返されたステータスコード、requesttid、エラーの詳細などが含まれています。異常をキャプチャした後、必要なトラブルシューティング要因を含む異常全体を印刷することをお勧めします。以下は、異常メンバー変数の説明です：

| request メンバー | 説明                                                         | タイプ       |
| ------------ | ------------------------------------------------------------ | --------- |
| requestId    | リクエストIDであり、リクエストを表すために使用され、トラブルシューティングに非常に重要です            | String    |
| traceId      | トラブルシューティング用のID                                          | String    |
| statusCode   | 応答のステータスコードであり、4xxはクライアントによるリクエストの失敗を指し、5xxはサーバー異常による失敗です。[COSエラーメッセージ](https://cloud.tencent.com/document/product/436/7730)を参照してください | String    |
| errorType    | 列挙型であり、異常の種類を表し、Client、Service、Unknownに分けられます    | ErrorType |
| errorCode    |  リクエストが失敗した時にボディにより返されたError Codeについては、[COSエラーメッセージ](https://cloud.tencent.com/document/product/436/7730)を参照してください | String    |
| errorMessage | リクエストが失敗した時にボディにより返されたError Messageについては、[COSエラーメッセージ](https://cloud.tencent.com/document/product/436/7730)を参照してください | String    |

## FAQ

### SDKを導入して実行した後、java.lang.NoSuchMethodErrorの異常が発生しますか？

原因は、一般的に、JARパッケージの衝突であり、例えば、ユーザーのプロジェクト内のHTTPのJARパッケージにはAメソッドはありませんが、SDKが依存するJARパッケージにはAメソッドがあります。この時、ランタイムロード順序により、ユーザーのプロジェクト内のHTTPライブラリがロードされ、ランタイムにおいてNoSuchMethodErrorの異常がスローされます。ソリューション：含まれたプロジェクトにおけるNoSuchMethodErrorの原因となったパッケージのバージョンをSDK中のpom.xml内の対応するライブラリのバージョンに一致させます。

### SDKのアップロード速度が遅く、ログにIOExceptionが頻繁に印刷されますか？

原因およびソリューション
 a. まず、パブリックネットワークを介してCOSにアクセスするかどうかを確認し、現在、同じキャンパスのCVMによるCOSへのアクセスがプライベートネットワークを介し（プライベートネットワークの名前解決により得られたIPは10、100、169IPアドレス範囲であり、COSドメイン名については、[COS使用可能な地域](https://cloud.tencent.com/document/product/436/6224)を参照してください）、パブリックネットワークを利用する場合、アウトバウンド帯域幅が小さいかどうか、または他のプログラムが帯域幅リソースを占有しているかどうかを確認します。
 b. 生産環境内のログレベルがdebugでないことを確保し、INFOログを使用することをお勧めし、log4jのログ構成については、[log4jログ構成テンプレート](https://github.com/tencentyun/cos-java-sdk-v5/blob/master/src/main/resources/log4j.properties)を参照してください。
 c. 現在、簡単なアップロード速度は10MBに達することができ、高レベルAPIについて、32並行の場合、速度は60MBに達することができ、速度がこの2つの値より遥かに小さい場合、aとbを参照してください。
 d. 警告ログに印刷されたIOExceptionが無視できる場合、SDKは再試行し、複数回再試行しても失敗した場合、IOExceptionが印刷されます。IOExceptionの原因は即ちネットワーク速度が遅すぎることであり、原因については、aとbを参照してください。

### SDKにおいて、どのようにディレクトリを作成しますか？

COSにおいて、ファイルとディレクトリの両方はオブジェクトであり、ディレクトリは「/」で終わるオブジェクトだけです。ファイルを作成する時、ディレクトリを作成する必要はありません。例えば、オブジェクトキーがxxx/yyy/zzz.txtのファイルを作成する時、キーをxxx/yyy/zzz.txtに設定するだけでよく、xxx/yyy/というオブジェクトを作成する必要はありません。コンソールに表示する時も、「/」で区切って、ディレクトリの階層効果を示します。しかしながら、これらのディレクトリオブジェクトが存在しません。ディレクトリオブジェクトを作成しようとする場合、以下のサンプルコードを使用してください：

```java
String bucketName = "mybucket-125166000";=
String key = "xxx/yyy/";
// ディレクトリオブジェクトは、/で終わる空のファイルであり、サイズが0であるバイトストリームをアップロードします
InputStream input = new ByteArrayInputStream(new byte[0]);
ObjectMetadata objectMetadata = new ObjectMetadata();
objectMetadata.setContentLength(0);

PutObjectRequest putObjectRequest =
new PutObjectRequest(bucketName, key, input, objectMetadata);
PutObjectResult putObjectResult = cosClient.putObject(putObjectRequest);
```

### SDKにおいて、どのようにHTTPSを使用しますか？

SDKにおける関連構成はいずれもClientConfigタイプに一括して置かれ、COSClientを生成する時にHTTPSを使用するように構成でき、サンプルコードは以下のとおりです：

```java
// 1 ユーザー身元情報（secretId、secretKey）を初期化します
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2 バケットのエリアを設定し、COS地域の略称については、以下を参照してください：https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// httpsを使用するように構成します
clientConfig.setHttpProtocol(HttpProtocol.https);
// 3 cosクライアントの生成
COSClient cosClient = new COSClient(cred, clientConfig);
```

### SDKにおいて、どのようにプロキシを使用しますか？

COSにアクセスするためにプロキシを使用する必要がある顧客に対して、ClientConfigタイプにおいて、プロキシIP（またはドメイン名）とポートを使用するように構成し、サンプルコードは以下のとおりです：

```java
// 1 ユーザー身元情報（secretId、secretKey）を初期化します
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2 バケットのエリアを設定し、COS地域の略称については、以下を参照してください：https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// プロキシを使用するように構成します（IPとポートを同時に設定する必要があります）
// プロキシIPを設定します（ドメイン名をインバウンドすることもできます）
clientConfig.setHttpProxyIp("192.168.2.3");
// プロキシポートを設定します
clientConfig.setHttpProxyPort(8080);
// 3 cosクライアントの生成
COSClient cosClient = new COSClient(cred, clientConfig);
```

