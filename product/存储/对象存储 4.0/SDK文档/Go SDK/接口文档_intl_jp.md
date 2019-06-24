COS Go SDK（XML API）操作により、関連APIのResult構造とGolang HTTPスタンダードライブラリの[Response](https://golang.org/pkg/net/http/#Response)構造が返されます。

> ?本書に記載されるSecretId、SecretKey、Bucketなどの名前の意味と取得方法について[COS用語情報](https://cloud.tencent.com/document/product/436/7751)を参照してください。

## Service APIの説明

### バケットリストの取得

##### 機能説明

リクエスターの名義によるすべてのバケットリスト（Bucket list）の取得に用いられます。

#### 方法のプロトタイプ

```go
func (s *ServiceService) Get(ctx context.Context) (*ServiceGetResult, *Response, error)
```

####　リクエスト例

```go
s, resp, err := c.Service.Get(context.Background()) 
```

#### 戻り結果の説明

```go
type ServiceGetResult struct {
    Owner   *Owner  
    Buckets []Bucket 
}
type Owner struct {
    ID          string 
    DisplayName string                                              
}
type Bucket struct {
	Name       string
    Region     string
    CreationDate string                                               
} 
```

| パラメータ名     | パラメータ説明                                                     | タイプ   |
| ------------ | ------------------------------------------------------------ | ------ |
| ID           | バケット所有者のID                                           | String |
| DisplayName | バケット所有者の名前情報                                      | String |
| Name         | バケットの名称                                                | String |
| Region       | バケットの所在地域                                              | String |
| CreationDate | バケットの作成時間。ISO8601フォーマット、例えば2016-11-09T08:46:32.000Z | String |

## Bucket API説明

### バケットの作成

##### 機能説明

指定アカウントの下で新しいバケットを作成し、バケットが存在している場合、エラーが返されます。

#### 方法のプロトタイプ

```go
func (s *BucketService) Put(ctx context.Context, opt *BucketPutOptions) (*Response, error)
```

####　リクエスト例

```go
opt := &cos.BucketPutOptions{
	XCosACL: "public-read",
}
resp, err := client.Bucket.Put(context.Background(), opt)
```

#### パラメータ説明

```go
type BucketPutOptions struct {
	XCosACL              string 
	XCosGrantRead        string  
	XCosGrantWrite       string  
	XCosGrantFullControl string 
}
```

| パラメータ名称             | パラメータ説明                                                     | タイプ   | 必須項目 |
| -------------------- | ------------------------------------------------------------ | ------ | ---- |
| XCosACL              | バケットのACLを設定します。例えばprivate、public-read、public-read-write | string | いいえ   |
| XCosGrantFullControl | 指定アカウントに対してバケットへの読み書き権限を付与します。フォーマットは`id=" ",id=" "`サブアカウントに授権する場合、フォーマットは`id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`ルートアカウントに授権する場合、フォーマットは`id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`例えば`id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | String | いいえ   |
| XCosGrantRead        | 指定アカウントに対してバケットへの読み取り権限を付与します。フォーマットは`id=" ",id=" "`サブアカウントに授権する場合、フォーマットは`id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`ルートアカウントに授権する場合、フォーマットは`id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`例えば`id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | いいえ   |
| XCosGrantWrite       | 指定アカウントに対してバケットへの書き込み権限を付与します。フォーマットは`id=" ",id=" "`サブアカウントに授権する場合、フォーマットは`id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`ルートアカウントに授権する場合、フォーマットは`id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`例えば`id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | いいえ   |

### バケットの削除

##### 機能説明

指定アカウントの下で存在しているバケットを削除する場合、バケットはブランクでなければなりません。

#### 方法のプロトタイプ

```go
func (s *BucketService) Delete(ctx context.Context) (*Response, error)
```

####　リクエスト例

```go
resp, err := client.Bucket.Delete(context.Background())
```

### バケット及びその権限の照合

##### 機能説明

バケットが存在するか、あるいはアクセス権があるかを照合します。

#### 方法のプロトタイプ

```go
func (s *BucketService) Head(ctx context.Context) (*Response, error)
```

####　リクエスト例

```go
resp, err := client.Bucket.Head(context.Background())
```

### 地域情報の取得

##### 機能説明

バケットの所在地域の情報を照合します。

#### 方法のプロトタイプ

```go
func (s *BucketService) GetLocation(ctx context.Context) (*BucketGetLocationResult, *Response, error)
```

####　リクエスト例

```go
v, resp, err := client.Bucket.GetLocation(context.Background())
```

#### 戻り結果の説明

```go
type BucketGetLocationResult struct {
	Location string                                      
}
```

```go
{
    'Location': 'ap-beijing-1'|'ap-beijing'|'ap-shanghai'|'ap-guangzhou'|'ap-chengdu'|'ap-chongqing'|'ap-singapore'|'ap-hongkong'|'na-toronto'|'eu-frankfurt'|'ap-mumbai'|'ap-seoul'|'na-siliconvalley'|'na-ashburn'
}
```

| パラメータ名 | パラメータ説明              | タイプ   |
| -------- | --------------------- | ------ |
| Location | バケットの所在地域の情報 | string |

### オブジェクトリストの取得

##### 機能説明

指定されたバケットにあるすべてのオブジェクトを取得します。

#### 方法のプロトタイプ

```go
func (s *BucketService) Get(ctx context.Context, opt *BucketGetOptions) (*BucketGetResult, *Response, error)
```

####　リクエスト例

```go
opt := &cos.BucketGetOptions{
	Prefix:  "test",
	MaxKeys: 100,                                
}
v, resp, err := client.Bucket.Get(context.Background(), opt)
```

#### パラメータ説明

```go
type BucketGetOptions struct {
	Prefix       string 
	Delimiter    string 
	EncodingType string 
	Marker       string 
	MaxKeys      int    
}
```

| パラメータ名称     | パラメータ説明                                                     | タイプ   | 必須項目 |
| ------------ | ------------------------------------------------------------ | ------ | ---- |
| Prefix       | デフォルトではブランクであり、オブジェクトのKeyを選別し、prefixが指定プレフィックスのオブジェクトをマッチングします | string | いいえ   |
| Delimiter    | デフォルトではブランクであり、区切り記号を設定し、例えばフォルダを設定/シミュレートします                  | string | いいえ   |
| EncodingType | デフォルトではエンコーディングせず、返された値のエンコーディング方式を定め、選択可能値：URL                | string | いいえ   |
| Marker       | デフォルトではUTF-8 2進法の順でエントリをリストし、オブジェクトを返すリストの起点位置をマークします | string | いいえ   |
| MaxKeys      | 返却されるオブジェクトの最大数、デフォルトでは最大1000です                    | int    | いいえ   |

#### 戻り結果の説明

```go
type BucketGetResult struct {
	Name           string
	Prefix         string 
	Marker         string 
	NextMarker     string 
	Delimiter      string 
	MaxKeys        int
	IsTruncated    bool
	Contents       []Object 
	CommonPrefixes []string 
	EncodingType   string   
}
```

| パラメータ名    | パラメータ説明                                              | タイプ     |
| -------------- | ------------------------------------------------------------ | -------- |
| Name           | バケット名称、bucketname-appidからなります                        | string   |
| Prefix       | デフォルトではブランクであり、オブジェクトのKeyを選別し、prefixが指定プレフィックスのオブジェクトをマッチングします | string   |
| Marker       | デフォルトではUTF-8 2進法の順でエントリをリストし、オブジェクトを返すリストの起点位置をマークします | string   |
| NextMarker     | IsTruncatedがtrueである場合、次回オブジェクトを返すリストの起点位置をマークします | string   |
| Delimiter    | デフォルトではブランクであり、区切り記号を設定し、例えばフォルダを設定/シミュレートします                  | string   |
| MaxKeys      | 返されたオブジェクトの最大数、デフォルトでは最大1000です                    | int    |
| IsTruncated    | 返されたオブジェクトが遮断されたかを示します                                  | bool     |
| Contents       | すべてのオブジェクトのソース情報のリストを含み、それぞれのオブジェクトタイプはETag、StorageClass、Key、Owner、LastModified、Sizeなどの情報を含みます | []Object |
| CommonPrefixes | すべてのPrefixで始まり、Delimiterで終わるKeyは同類にされます      | []string |
| EncodingType   | デフォルトではエンコーディングせず、返された値のエンコーディング方式を定め、選択可能値：URL                | string   |

### マルチパートアップロードの照合

##### 機能説明

指定バケット下のすべての進行中のマルチパートアップロードを照合します。

#### 方法のプロトタイプ

```go
func (s *BucketService) ListMultipartUploads(ctx context.Context, opt *ListMultipartUploadsOptions) (*ListMultipartUploadsResult, *Response, error)
```

####　リクエスト例

```go
opt := &cos.ListMultipartUploadsOptions{
	Prefix: "test",
}
v, resp, err := client.Bucket.ListMultipartUploads(context.Background(), opt)
```

#### パラメータ説明

```go
type ListMultipartUploadsOptions struct {
	Delimiter      string 
	EncodingType   string 
	Prefix         string 
	MaxUploads     int    
	KeyMarker      string 
	UploadIDMarker string 
}
```

| パラメータ名称       | パラメータ説明                                                     | タイプ   | 必須項目 |
| -------------- | ------------------------------------------------------------ | ------ | ---- |
| Delimiter    | デフォルトではブランクであり、区切り記号を設定します| string | いいえ   |
| EncodingType   | デフォルトではエンコーディングせず、返された値のエンコーディング方式を定め、選択可能値：URL                | string | いいえ   |
| Prefix       | デフォルトではブランクであり、マルチパートアップロードのKeyを選別し、prefixをプレフィックスとするパートとマッチングします | string   | いいえ   |
| MaxUploads      | 返されたパートの最大数、デフォルトでは最大1000です                    | int    | いいえ   |
| KeyMarker      | UploadIdMarkerと併用し、マルチパートアップロードの開始位置をリストします | string | いいえ   |
| UploadIdMarker | KeyMarkerと併用し、マルチパートアップロードの開始位置をリストします。KeyMarkerを指定していない場合、UploadIdMarkerは無視されます | string | いいえ   |

#### 戻り結果の説明

```go
type ListMultipartUploadsResult struct {
	Bucket             string   
	EncodingType       string   
	KeyMarker          string
	UploadIDMarker     string 
	NextKeyMarker      string
	NextUploadIDMarker string 
	MaxUploads         int
	IsTruncated        bool
	Uploads            []struct {
        Key          string
        UploadID     string 
        StorageClass string
        Initiator    *Initiator
        Owner        *Owner
        Initiated    string
	} 
	Prefix         string
	Delimiter      string   
	CommonPrefixes []string 
}
```

| パラメータ名           | パラメータ説明                                                     | タイプ     |
| ------------------ | ------------------------------------------------------------ | -------- |
| Bucket             | バケット名称は、bucketname-appidからなります                        | string   |
| EncodingType       | デフォルトではエンコーディングせず、返された値のエンコーディング方式を定め、選択可能値：URL                | string   |
| KeyMarker          | UploadIdMarkerと併用し、マルチパートアップロードの開始位置をリストします  | string   |
| UploadIdMarker     | KeyMarkerと併用し、マルチパートアップロードのuploadid開始位置をリストします。KeyMarkerを指定していない場合、UploadIdMarkerは無視されます | string   |
| NextKeyMarker      |  IsTruncatedがtrueである場合、次回マルチパートアップロードをリストするKeyの開始位置を表示します | string   |
| NextUploadIDMarker      |  IsTruncatedがtrueである場合、次回マルチパートアップロードをリストするuploadidの開始位置を表示します | string   |
| MaxUploads         | 返却されたパートの最大数、デフォルトでは最大1000です                   | int    |
| IsTruncated        | 返却されたマルチパートアップロードが遮断されたかを示します                                  | bool     |
| Upload             | すべてのマルチパートアップロードのリスト、すなわちUploadId、storageClass、Key、Owner、Initiator、Initiatedなどの情報を含みます | []struct |
| Prefix       | デフォルトではブランクであり、マルチパートアップロードのKeyを選別し、prefixをプレフィックスとするパートとマッチングします | string   |
| Delimiter          | デフォルトではブランクであり、区切り記号を設定します| string   |
| CommonPrefixes     | すべてのPrefixで始まり、Delimiterで終わるKeyは同類にされます      | []string |

### バケットACLの設定

##### 機能説明

バケットのACL情報を設定する場合、XCosACL、XCosGrantFullControl、XCosGrantRead、XCosGrantWriteを通じてヘッダーを入力するか、あるいはACLXMLを通じてボディを入力することでACLを設定します。競合が発生しないように、二者から1つしか選択できません。

#### 方法のプロトタイプ

```go
func (s *BucketService) PutACL(ctx context.Context, opt *BucketPutACLOptions) (*Response, error)
```

####　リクエスト例

ヘッダーを通じてBucket ACLを設定します

```go
opt := &cos.BucketPutACLOptions{
	Header: &cos.ACLHeaderOptions{
		//private、public-read、public-read-write
		XCosACL: "private",
	},
}
resp, err := client.Bucket.PutACL(context.Background(), opt)
```

ボディを通じてBucket ACLを設定します

```go
opt = &cos.BucketPutACLOptions{
    Body: &cos.ACLXml{
        Owner: &cos.Owner{
            ID: "qcs::cam::uin/100000760461:uin/100000760461",
        },
        AccessControlList: []cos.ACLGrant{
            {
                Grantee: &cos.ACLGrantee{
                    Type: "RootAccount",
                    ID:"qcs::cam::uin/100000760461:uin/100000760461",
                },
                Permission: "FULL_CONTROL",
            },
        },
    },
}
resp, err := client.Bucket.PutACL(context.Background(), opt)
```

#### パラメータ説明

```go
type ACLHeaderOptions struct {
	XCosACL              string 
	XCosGrantRead        string 
	XCosGrantWrite       string 
	XCosGrantFullControl string 
}
```

| パラメータ名称             | パラメータ説明                                                     | タイプ   | 必須項目 |
| -------------------- | ------------------------------------------------------------ | ------ | ---- |
| XCosACL              | バケットのACLを設定します。例えばprivate、public-read、public-read-write | string | いいえ   |
| XCosGrantFullControl | 指定アカウントに対してバケットへの読み書き権限を付与します。フォーマットは`id=" ",id=" "`サブアカウントに授権する場合、フォーマットは`id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`ルートアカウントに授権する場合、フォーマットは`id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`例えば`id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | String | いいえ   |
| XCosGrantRead        | 指定アカウントに対してバケットへの読み取り権限を付与します。フォーマットは`id=" ",id=" "`サブアカウントに授権する場合、フォーマットは`id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`ルートアカウントに授権する場合、フォーマットは`id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`例えば`id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | いいえ   |
| XCosGrantWrite       | 指定アカウントに対してバケットへの書き込み権限を付与します。フォーマットは`id=" ",id=" "`サブアカウントに授権する場合、フォーマットは`id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`ルートアカウントに授権する場合、フォーマットは`id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`例えば`id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | いいえ   |
| ACLXML               | 指定アカウントに対してバケットへのアクセス権限を授与します。詳しいフォーマットについては、get bucket aclの返された結果の説明を参照してください | struct | いいえ   |



### バケットACLの取得

##### 機能説明

指定バケットのACL情報を取得します。

#### 方法のプロトタイプ

```go
func (s *BucketService) GetACL(ctx context.Context) (*BucketGetACLResult, *Response, error)
```

####　リクエスト例

```go
v, resp, err := client.Bucket.GetACL(context.Background())
```

#### 戻り結果の説明

```go
type ACLXml struct {
	Owner             *Owner
	AccessControlList []ACLGrant 
}
type Owner struct { 
	ID          string 
	DisplayName string
}
type ACLGrant struct {
	Grantee    *ACLGrantee
	Permission string
}
type ACLGrantee struct {
	Type        string 
	ID          string 
	DisplayName string
    UIN         string 
}
```

| パラメータ名          | パラメータ説明                                                     | タイプ   |
| ----------------- | ------------------------------------------------------------ | ------ |
| Owner             | バケット保有者の情報、DisplayNameとIDを含みます                  | struct |
| AccessControlList | バケット権限授与者の情報、GranteeとPermissionを含みます           | struct |
| Grantee           | 権限授与者の情報、DisplayName、Type、IDとUINを含みます          | struct |
| Type              | 権限授与者のタイプ、タイプはCanonicalUserあるいはGroupです            | string |
| ID                | TypeがCanonicalUserである場合、権限授与者のIDに対応します                 | string |
| DisplayName       | 権限授与者の名前                                             | string |
| UIN               | TypeがGroupである場合、権限授与者のUINに対応します                       | string |
| Permission        | 授与者の保有するバケットの権限、選択可能値はFULL_CONTROL、WRITE、READであり、それぞれ読み書き権限、書き込み権限、読み取り権限に対応します | string |

### クロスオリジン構成の設定

##### 機能説明

指定バケットのクロスオリジンリソース構成を設定します。

#### 方法のプロトタイプ

```go
func (s *BucketService) PutCORS(ctx context.Context, opt *BucketPutCORSOptions) (*Response, error)
```

####　リクエスト例

```go
opt := &cos.BucketPutCORSOptions{
    Rules: []cos.BucketCORSRule{
        {
            AllowedOrigins: []string{"http://www.qq.com"},
            AllowedMethods: []string{"PUT", "GET"},
            AllowedHeaders: []string{"x-cos-meta-test", "x-cos-xx"},
            MaxAgeSeconds:  500,
            ExposeHeaders:  []string{"x-cos-meta-test1"},
        },
        {
            ID:             "1234",
            AllowedOrigins: []string{"http://www.baidu.com", "twitter.com"},
            AllowedMethods: []string{"PUT", "GET"},
            MaxAgeSeconds:  500,
        },
    },
}
resp, err := client.Bucket.PutCORS(context.Background(), opt)
```

#### パラメータ説明

```go
type BucketCORSRule struct {
	ID             string   
	AllowedMethods []string 
	AllowedOrigins []string 
	AllowedHeaders []string 
	MaxAgeSeconds  int      
	ExposeHeaders  []string 
}
```

| パラメータ名称       | パラメータ説明                                                     | タイプ | 必須項目 |
| -------------- | ------------------------------------------------------------ | -------- | ---- |
| BucketCORSRule | 対応のクロスオリジン規則を設定します。それはID、MaxAgeSeconds、AllowedOrigin、AllowedMethod、AllowedHeader、ExposeHeaderを含みます | struct   | はい   |
| ID             | 規則のIDを設定します                                                | string   | いいえ   |
| AllowedMethods | 許可される方法を設定します。それはGET、PUT、HEAD、POST、DELETEを含みます              | []string | はい   |
| AllowedOrigins | 許可されるアクセス元を設定します。例えば`"http://cloud.tencent.com"`。ワイルドカード*に対応します | []string |はい   |
| AllowedHeaders | どのカスタマイズHTTPを使用できるかというリクエストヘッダーを設定します。ワイルドカード*に対応します     | []string | いいえ   |
| MaxAgeSeconds  | OPTIONSリクエストの結果が得られる有効期を設定します                            | int      | いいえ   |
| ExposeHeaders  | ブラウザの受信可能で、サーバーからのカスタムヘッダー情報を設定します           | []string | いいえ   |

### クロスオリジン構成の取得

##### 機能説明

指定バケットクロスオリジン構成を取得します。

#### 方法のプロトタイプ

```go
func (s *BucketService) GetCORS(ctx context.Context) (*BucketGetCORSResult, *Response, error)
```

####　リクエスト例

```go
v, resp, err := client.Bucket.GetCORS(context.Background())
```

#### 戻り結果の説明

```go
type BucketCORSRule struct {
	ID             string   
	AllowedMethods []string 
	AllowedOrigins []string 
	AllowedHeaders []string 
	MaxAgeSeconds  int      
	ExposeHeaders  []string 
}
```

| パラメータ名称       | パラメータ説明                                                     | タイプ | 必須項目 |
| -------------- | ------------------------------------------------------------ | -------- | ---- |
| BucketCORSRule | 対応のクロスオリジン規則を設定します。それはID、MaxAgeSeconds、AllowedOrigin、AllowedMethod、AllowedHeader、ExposeHeaderを含みます | struct   | はい   |
| ID             | 規則のIDを設定します                                                | string   | いいえ   |
| AllowedMethods | 許可される方法を設定します。それはGET、PUT、HEAD、POST、DELETEを含みます              | []string | はい   |
| AllowedOrigins | 許可されるアクセス元を設定します。例えば`"http://cloud.tencent.com"`。ワイルドカード*に対応します | []string |はい   |
| AllowedHeaders | どのカスタマイズHTTPを使用できるかというリクエストヘッダーを設定します。ワイルドカード*に対応します     | []string | いいえ   |
| MaxAgeSeconds  | OPTIONSリクエストの結果が得られる有効期を設定します                            | int      | いいえ   |
| ExposeHeaders  | ブラウザの受信可能で、サーバーからのカスタムヘッダー情報を設定します           | []string | いいえ   |

### クロスオリジン構成の削除

##### 機能説明

指定バケットのクロスオリジン構成を削除します。

#### 方法のプロトタイプ

```go
func (s *BucketService) DeleteCORS(ctx context.Context) (*Response, error)
```

####　リクエスト例

```go
resp, err := client.Bucket.DeleteCORS(context.Background())
```

### ライフサイクルの設定

##### 機能説明

指定バケットのライフサイクル構成を設定します。

#### 方法のプロトタイプ

```go
func (s *BucketService) PutLifecycle(ctx context.Context, opt *BucketPutLifecycleOptions) (*Response, error)
```

####　リクエスト例

```go
lc := &cos.BucketPutLifecycleOptions{
    Rules: []cos.BucketLifecycleRule{
        {
            ID:     "1234",
            Filter: &cos.BucketLifecycleFilter{Prefix: "test"},
            Status: "Enabled",
            Transition: &cos.BucketLifecycleTransition{
                Days:         10,
                StorageClass: "Standard",
            },
        },
        {
            ID:     "123422",
            Filter: &cos.BucketLifecycleFilter{Prefix: "gg"},
            Status: "Disabled",
            Expiration: &cos.BucketLifecycleExpiration{
                Days: 10,
            },
        },
    },
}
resp, err := client.Bucket.PutLifecycle(context.Background(), lc)
```

#### パラメータ説明

```go
type BucketLifecycleRule struct {
	ID                             string
	Status                         string
	Filter                         *BucketLifecycleFilter
	Transition                     *BucketLifecycleTransition
	Expiration                     *BucketLifecycleExpiration
	AbortIncompleteMultipartUpload  *BucketLifecycleAbortIncompleteMultipartUpload 
}
type BucketLifecycleFilter struct {
	Prefix       string 
}
type BucketLifecycleTransition struct {
	Date         string 
	Days         int    
	StorageClass string
}
type BucketLifecycleExpiration struct {
	Date string 
	Days int    
}
type BucketLifecycleAbortIncompleteMultipartUpload struct {
	DaysAfterInitiation string 
}
```

| パラメータ名称                       | パラメータ説明                                                     | タイプ   | 必須項目 |
| ------------------------------ | ------------------------------------------------------------ | ------ | ---- |
| BucketLifecycleRule | 対応の規則を設定します。それはID、Filter、Status、Expiration、Transition、AbortIncompleteMultipartUploadを含みます | List   | はい   |
| ID                             | 規則のIDを設定します                                                | string  | いいえ   |
| Status                         | Ruleをオンにするかを設定します。選択可能値はEnabledあるいはDisabledです          | string | はい   |
| Filter                         | 規則から影響を受けるオブジェクトセットの説明に用いられます。バケットにおけるすべてのオブジェクトを設定するには、Prefixをブランクに設定してください | struct | はい   |
| Transition                     | オブジェクトのストレージクラスの転換規則を設定します。日数Daysあるいは日付Dateを指定できます。DateのフォーマットはGMT ISO 8601でなければなりません。StorageClassはStandard_IA、Archiveから選択できます。同時に複数のこのタイプの規則を設定できます | struct | いいえ   |
| Expiration                     | オブジェクトの期限切れ規則を設定します。日数Daysあるいは日付Dateを指定できます。DateのフォーマットはGMT ISO 8601でなければなりません。 | struct | いいえ   |
| AbortIncompleteMultipartUpload | マルチパートアップロード開始後、何日以内にアップロードを完成する必要があるかを示します                       | struct | いいえ   |

### ライフサイクルの照合

##### 機能説明

指定バケットのライフサイクル構成を照合します。

#### 方法のプロトタイプ

```go
func (s *BucketService) GetLifecycle(ctx context.Context) (*BucketGetLifecycleResult, *Response, error)
```

####　リクエスト例

```go
v, resp, err := client.Bucket.GetLifecycle(context.Background()) 
```

#### 戻り結果の説明

```go
type BucketLifecycleRule struct {
	ID                             string
	Status                         string
	Filter                         *BucketLifecycleFilter
	Transition                     *BucketLifecycleTransition
	Expiration                     *BucketLifecycleExpiration
	AbortIncompleteMultipartUpload  *BucketLifecycleAbortIncompleteMultipartUpload 
}
type BucketLifecycleFilter struct {
	Prefix       string 
}
type BucketLifecycleTransition struct {
	Date         string 
	Days         int    
	StorageClass string
}
type BucketLifecycleExpiration struct {
	Date string 
	Days int    
}
type BucketLifecycleAbortIncompleteMultipartUpload struct {
	DaysAfterInitiation string 
}
```

| パラメータ名称                       | パラメータ説明                                                     | タイプ   | 必須項目 |
| ------------------------------ | ------------------------------------------------------------ | ------ | ---- |
| BucketLifecycleRule | 対応の規則を設定します。それはID、Filter、Status、Expiration、Transition、AbortIncompleteMultipartUploadを含みます | List   | はい   |
| ID                             | 規則のIDを設定します                                                | string  | いいえ   |
| Status                         | Ruleをオンにするかを設定します。選択可能値はEnabledあるいはDisabledです          | string | はい   |
| Filter                         | 規則から影響を受けるオブジェクトセットの説明に用いられます。バケットにおけるすべてのオブジェクトを設定するには、Prefixをブランクに設定してください | struct | はい   |
| Transition                     | オブジェクトのストレージクラスの転換規則を設定します。日数Daysあるいは日付Dateを指定できます。DateのフォーマットはGMT ISO 8601でなければなりません。StorageClassはStandard_IA、Archiveから選択できます。同時に複数のこのタイプの規則を設定できます | struct | いいえ   |
| Expiration                     | オブジェクトの期限切れ規則を設定します。日数Daysあるいは日付Dateを指定できます。DateのフォーマットはGMT ISO 8601でなければなりません。 | struct | いいえ   |
| AbortIncompleteMultipartUpload | マルチパートアップロード開始後、何日以内にアップロードを完成する必要があるかを示します                       | struct | いいえ   |

### ライフサイクルの削除

##### 機能説明

指定バケットのライフサイクル構成を削除します。

#### 方法のプロトタイプ

```go
func (s *BucketService) DeleteLifecycle(ctx context.Context) (*Response, error)
```

####　リクエスト例

```go
resp, err := client.Bucket.DeleteLifecycle(context.Background())
```

## Object API説明

### アップデートオブジェクト

##### 機能説明

ローカルのファイルまたは入力ストリームを指定のバケットにアップロードすることに対応します。20 Mb以内の小型ファイルをアップロードすることが望ましいです。毎回アップロードのサイズ制限は5 GBで、大容量ファイルのアップロードについては、マルチパートアップロードを使用してください。

>!現在のアクセスポリシーのエントリは1000条に限られており、オブジェクトACL制御が不要な場合、アップロードする前に設定しないでください。デフォルトでバケット権限を受け継ぎます。

#### 方法のプロトタイプ

```go
func (s *ObjectService) Put(ctx context.Context, key string, r io.Reader, opt *ObjectPutOptions) (*Response, error)
```

####　リクエスト例

```go	
    key := "put_option.go"
	f := strings.NewReader("test xxx")
	opt := &cos.ObjectPutOptions{
		ObjectPutHeaderOptions: &cos.ObjectPutHeaderOptions{
			ContentType: "text/html",
		},
		ACLHeaderOptions: &cos.ACLHeaderOptions{
			XCosACL: "private",
		},
	}
resp, err = client.Object.Put(context.Background(), key, f, opt)
```

#### パラメータ説明

```go
type ObjectPutOptions struct {
	*ACLHeaderOptions       
	*ObjectPutHeaderOptions 
}
type ACLHeaderOptions struct {
	XCosACL              string                           
    XCosGrantRead        string
    XCosGrantWrite       string 
    XCosGrantFullControl string                                           
} 
type ObjectPutHeaderOptions struct {
	CacheControl       string 
	ContentDisposition string 
	ContentEncoding    string 
	ContentType        string 
	ContentLength      int   
	Expires            string 
	//カスタマイズのx-cos-meta-* header
	XCosMetaXXX        *http.Header 
	XCosStorageClass   string      
}
```

| パラメータ名称             | パラメータ説明                                                     | タイプ        | 必須項目 |
| -------------------- | ------------------------------------------------------------ | ----------- | ---- |
| r                    | アップロードするファイルの内容は、ファイルストリームまたはバイトストリームであってよいです。rがbytes.Buffer/bytes.Reader/strings.Readerでない場合、opt.ObjectPutHeaderOptions.ContentLengthを指定しなければなりません | io.Readerはい   |
| Key                  | オブジェクトキー（Key）はバケットにおけるオブジェクトの唯一の識別子です。例えば、オブジェクトのアクセスドメイン名` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg `において、オブジェクトキーは doc1/pic1.jpgです | string      | はい   |
| XCosACL              | ファイルのACLを設定します。例えば、private、public-read、public-read-write    | string      | いいえ   |
| XCosGrantFullControl | 指定アカウントに対してファイルへの読み書き権限を付与します。フォーマットは`id=" ",id=" "`サブアカウントに授権する場合、フォーマットは`id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`ルートアカウントに授権する場合、フォーマットは`id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`例えば`id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | String      | いいえ   |
| XCosGrantRead        | 指定アカウントに対してファイルへの読み取り権限を授与します。フォーマットは`id=" ",id=" "`サブアカウントに授権する場合、フォーマットは`id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`ルートアカウントに授権する場合、フォーマットは`id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`例えば`id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string      | いいえ   |
| XCosGrantWrite       | 指定アカウントに対してファイルへの書き込み権限を付与します。フォーマットは`id=" ",id=" "`サブアカウントに授権する場合、フォーマットは`id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`ルートアカウントに授権する場合、フォーマットは`id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`例えば`id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string      | いいえ   |
| XCosStorageClass     | ファイルのストレージクラスを設定します、STANDARD、STANDARD_IA、デフォルト値：STANDARD | string      | いいえ   |
| Expires              | Content-Expiresの設定                                         | string      | いいえ   |
| CacheControl         | キャッシュメモリポリシー、Cache-Controlの設定                                 | string      | いいえ   |
| ContentType              | 内容タイプ、Content-Typeの設定                                         | string      | いいえ   |
| ContentDisposition   | ファイル名、Content-Dispositionの設定                           | string      | いいえ   |
| ContentEncoding      | エンコーディングフォーマット、Content-Encodingの設定                              | string | いいえ   |
| ContentLength        | 送信長さの設定                                                 | string      | いいえ   |
| XCosMetaXXX          | ユーザーカスタマイズのファイルのソース情報、x-cos-metaで始まらなければなりません。さもなければ無視されます | http.Header | いいえ   |

#### 戻り結果の説明

```go
{
    'ETag': 'string',
    'x-cos-expiration': 'string'
}
```

| パラメータ名         | パラメータ説明                         | タイプ   |
| ---------------- | -------------------------------- | ------ |
| ETag             | ファイルのMD5値のアップロード                | string |
| x-cos-expiration | ライフサイクルの設定後、ファイルの期限切れ規則が返却されます | string |

### オブジェクトの取得

##### 機能説明

指定バケットにおけるファイルをローカルにダウンロードします。

#### 方法のプロトタイプ

```go
func (s *ObjectService) Get(ctx context.Context, key string, opt *ObjectGetOptions) (*Response, error)
```

####　リクエスト例

```go
	key := "test/hello.txt"
	opt := &cos.ObjectGetOptions{
		ResponseContentType: "text/html",
		Range:               "bytes=0-3",
	}
	//optは選択可能で、特別な設定がない限り、nilに設定して良いです
	resp, err = client.Object.Get(context.Background(), key, opt)
	bs, _ = ioutil.ReadAll(resp.Body)
	resp.Body.Close()
	fmt.Printf("%s\n", string(bs))
```

#### パラメータ説明

```go
type ObjectGetOptions struct {
	ResponseContentType        string 
	ResponseContentLanguage    string 
	ResponseExpires            string 
	ResponseCacheControl       string 
	ResponseContentDisposition string 
	ResponseContentEncoding    string 
	Range                      string 
	IfModifiedSince            string 
}
```

| パラメータ名称                   | パラメータ説明                                                     | タイプ   | 必須項目 |
| -------------------------- | ------------------------------------------------------------ | ------ | ---- |
| Key                        | オブジェクトキー（Key）はバケットにおけるオブジェクトの唯一の識別子です。例えば、オブジェクトのアクセスドメイン名` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg `において、オブジェクトキーは doc1/pic1.jpgです | string | はい   |
| ResponseContentType        | 応答ヘッダーContent-Typeの設定                                    | string | いいえ   |
| ResponseContentLanguage    | 応答ヘッダーContent-Languageの設定                                | string | いいえ   |
| ResponseExpires            | 応答ヘッダーContent-Expiresの設定                                 | string | いいえ   |
| ResponseCacheControl        | 応答ヘッダーCache-Controlの設定                                    | string | いいえ   |
| ResponseContentDisposition | 応答ヘッダーContent-Dispositionの設定                             | string | いいえ   |
| ResponseContentEncoding    | 応答ヘッダーContent-Encodingの設定                                | string | いいえ   |
| Range                      | ファイルのダウンロード範囲を設定します。フォーマットはbytes=first-last                  | string | いいえ   |
| IfModifiedSince            | 指定時間後に変更される場合にのみ返却されます                                     | string | いいえ   |

#### 戻り結果の説明

```go
{
    'Body': '',
    'Accept-Ranges': 'bytes',
    'Content-Type': 'application/octet-stream',
    'Content-Length': '16807',
    'Content-Disposition': 'attachment; filename="filename.jpg"',
    'Content-Range': 'bytes 0-16086/16087',
    'ETag': '"9a4802d5c99dafe1c04da0a8e7e166bf"',
    'Last-Modified': 'Wed, 28 Oct 2014 20:30:00 GMT',
    'X-Cos-Request-Id': 'NTg3NzQ3ZmVfYmRjMzVfMzE5N182NzczMQ=='
}
```

| パラメータ名   | パラメータ説明                                                     | タイプ       |
| ---------- | ------------------------------------------------------------ | ---------- |
| Body       | ダウンロードするファイルの内容                                               | StreamBody |
| ファイルソース情報 | ダウンロードするファイルのソース情報。EtagとX-cos-Request-Idなどの情報を含みます。また設定したファイルのソース情報を返却します | string     |

### 単一オブジェクトの削除

##### 機能説明

バケットにおいて対応するファイルを削除します。

#### 方法のプロトタイプ

```go
func (s *ObjectService) Delete(ctx context.Context, key string) (*Response, error)
```

####　リクエスト例

```go
key := "test/objectPut.go"
resp, err := client.Object.Delete(context.Background(), name)
```

#### パラメータ説明

| パラメータ名称 | パラメータ説明                                                     | タイプ | 必須項目 |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| Key      | オブジェクトキー（Key）はバケットにおけるオブジェクトの唯一の識別子です。例えば、オブジェクトのアクセスドメイン名` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg `において、オブジェクトキーは doc1/pic1.jpgです | string | はい   |

### 複数オブジェクトの削除

##### 機能説明

指定バケットにおけるファイルを一括削除します。

#### 方法のプロトタイプ

```go
func (s *ObjectService) DeleteMulti(ctx context.Context, opt *ObjectDeleteMultiOptions) (*ObjectDeleteMultiResult, *Response, error)
```

####　リクエスト例

```go
var keys = []string{"a","b","c"}
obs := []cos.Object{}
for _, v := range keys {
    obs = append(obs, cos.Object{Key: v})
}
opt := &cos.ObjectDeleteMultiOptions{
    Objects: obs,
    Quiet: true,
}
v, resp, err := client.Object.DeleteMulti(ctx, opt)
```

#### パラメータ説明

```go
type ObjectDeleteMultiOptions struct {
	Quiet   bool     
	Objects []Object 
}
type Object struct {
	Key		string 
}
```

| パラメータ名称 | パラメータ説明                                                     | タイプ | 必須項目 |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| Objects  | 削除する各目標オブジェクト情報の説明                           | List   | はい   |
| Key                  | オブジェクトキー（Key）はバケットにおけるオブジェクトの唯一の識別子です。例えば、オブジェクトのアクセスドメイン名` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg `において、オブジェクトキーは doc1/pic1.jpgです | string | いいえ   |
| Quiet    | 削除後の結果返却方式を表示します。選択可能値はtrueとfalseで、デフォルトではfalseです。trueに設定する場合、失敗のエラー情報のみが返却されます。falseに設定する場合、成功と失敗のすべての情報が返却されます。 | bool   | いいえ   |

#### 戻り結果の説明

```go
type ObjectDeleteMultiResult struct {
	DeletedObjects []Object
	Errors         []struct {
		Key     string
		Code    string
		Message string
	}
}
type Object struct {
	Key		string 
}
```

| パラメータ名       | パラメータ説明                         | タイプ     |
| -------------- | -------------------------------- | -------- |
| DeletedObjects | 成功したオブジェクト情報の削除           | []struct |
| Errors         | 失敗したオブジェクト情報の削除           | string   |
| Key            | 失敗したオブジェクトのパスの削除         | string   |
| Code           | 失敗したオブジェクトの対応するエラーコードの削除   | string   |
| Message        | 失敗したオブジェクトの対応するエラー情報の削除 | string   |

### オブジェクトのメタデータの取得

##### 機能説明

指定ファイルのソース情報の取得。

#### 方法のプロトタイプ

```go
func (s *ObjectService) Head(ctx context.Context, key string, opt *ObjectHeadOptions) (*Response, error)
```

####　リクエスト例

```go
key := "test/hello.txt"
resp, err := client.Object.Head(context.Background(), key, nil)
```

#### パラメータ説明

```go
type ObjectHeadOptions struct {
	IfModifiedSince string 
}
```

| パラメータ名称        | パラメータ説明                                                     | タイプ   | 必須項目 |
| --------------- | ------------------------------------------------------------ | ------ | ---- |
| Key             | オブジェクトキー（Key）はバケットにおけるオブジェクトの唯一の識別子です。例えば、オブジェクトのアクセスドメイン名` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg `において、オブジェクトキーは doc1/pic1.jpgです | string | はい   |
| IfModifiedSince | 指定時間後に変更される場合にのみ返却されます                                     | string | いいえ   |

#### 戻り結果の説明

```go
{
    'Content-Type': 'application/octet-stream',
    'Content-Length': '16807',
    'ETag': '"9a4802d5c99dafe1c04da0a8e7e166bf"',
    'Last-Modified': 'Wed, 28 Oct 2014 20:30:00 GMT',
    'X-Cos-Request-Id': 'NTg3NzQ3ZmVfYmRjMzVfMzE5N182NzczMQ=='
}
```

| パラメータ名   | パラメータ説明                                                     | タイプ   |
| ---------- | ------------------------------------------------------------ | ------ |
| ファイルソース情報 | 取得するファイルのソース情報。EtagとX-Cos-Request-Idなどの情報を含みます。また設定したファイルのソース情報を含みます | string |

### マルチパートアップロードの初期化

##### 機能説明

新しいマルチパートアップロードのタスクを作成します。UploadIdが返されます。

#### 方法のプロトタイプ

```go
func (s *ObjectService) InitiateMultipartUpload(ctx context.Context, name string, opt *InitiateMultipartUploadOptions) (*InitiateMultipartUploadResult, *Response, error)
```

####　リクエスト例

```go
name := "test_multipart"
//選択可能なopt
v, resp, err := client.Object.InitiateMultipartUpload(context.Background(), name, nil）
```

#### パラメータ説明

```go
type ObjectPutOptions struct {
	*ACLHeaderOptions       
	*ObjectPutHeaderOptions 
}
type ACLHeaderOptions struct {
	XCosACL              string                           
    XCosGrantRead        string
    XCosGrantWrite       string 
    XCosGrantFullControl string                                           
} 
type ObjectPutHeaderOptions struct {
	CacheControl       string 
	ContentDisposition string 
	ContentEncoding    string 
	ContentType        string 
	ContentLength      int   
	Expires            string 
	//カスタマイズのx-cos-meta-* header
	XCosMetaXXX        *http.Header 
	XCosStorageClass   string      
}
```

| パラメータ名称             | パラメータ説明                                                     | タイプ        | 必須項目 |
| -------------------- | ------------------------------------------------------------ | ----------- | ---- |
| r                    | アップロードするファイルの内容は、ファイルストリームまたはバイトストリームであってよいです。rがbytes.Buffer/bytes.Reader/strings.Readerでない場合、opt.ObjectPutHeaderOptions.ContentLengthを指定しなければなりません | io.Readerはい   |
| Key                  | オブジェクトキー（Key）はバケットにおけるオブジェクトの唯一の識別子です。例えば、オブジェクトのアクセスドメイン名` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg `において、オブジェクトキーは doc1/pic1.jpgです | string      | はい   |
| XCosACL              | ファイルのACLを設定します。例えば、private、public-read、public-read-write    | string      | いいえ   |
| XCosGrantFullControl | 指定アカウントに対してファイルへの読み書き権限を付与します。フォーマットは`id=" ",id=" "`サブアカウントに授権する場合、フォーマットは`id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`ルートアカウントに授権する場合、フォーマットは`id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`例えば`id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | String      | いいえ   |
| XCosGrantRead        | 指定アカウントに対してファイルへの読み取り権限を授与します。フォーマットは`id=" ",id=" "`サブアカウントに授権する場合、フォーマットは`id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`ルートアカウントに授権する場合、フォーマットは`id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`例えば`id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string      | いいえ   |
| XCosGrantWrite       | 指定アカウントに対してファイルへの書き込み権限を付与します。フォーマットは`id=" ",id=" "`サブアカウントに授権する場合、フォーマットは`id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`ルートアカウントに授権する場合、フォーマットは`id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`例えば`id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string      | いいえ   |
| XCosStorageClass     | ファイルのストレージクラスを設定します、STANDARD、STANDARD_IA、デフォルト値：STANDARD | string      | いいえ   |
| Expires              | Content-Expiresの設定                                         | string      | いいえ   |
| CacheControl         | キャッシュメモリポリシー、Cache-Controlの設定                                 | string      | いいえ   |
| ContentType              | 内容タイプ、Content-Typeの設定                                         | string      | いいえ   |
| ContentDisposition   | ファイル名、Content-Dispositionの設定                           | string      | いいえ   |
| ContentEncoding      | エンコーディングフォーマット、Content-Encodingの設定                              | string | いいえ   |
| ContentLength        | 送信長さの設定                                                 | string      | いいえ   |
| XCosMetaXXX          | ユーザーカスタマイズのファイルのソース情報、x-cos-metaで始まらなければなりません。さもなければ無視されます | http.Header | いいえ   |

#### 戻り結果の説明

```go
type InitiateMultipartUploadResult struct {
	Bucket   string
	Key      string
	UploadID string                   
} 
```

| パラメータ名 | パラメータ説明                                              | タイプ  |
| -------- | ------------------------------------------------------------ | ------ |
| UploadId | マルチパートアップロードのIDにタグを付けます                                            | string |
| Bucket   | バケット名。bucket-appidからなります                            | string |
| Key      | オブジェクトキー（Key）はバケットにおけるオブジェクトの唯一の識別子です。例えば、オブジェクトのアクセスドメイン名` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg `において、オブジェクトキーは doc1/pic1.jpgです | string |

### マルチパートアップロードの終了

##### 機能説明

マルチパートアップロードのタスクを諦め、すべてのアップロード済みのパートを削除します。

#### 方法のプロトタイプ

```go
func (s *ObjectService) AbortMultipartUpload(ctx context.Context, key, uploadID string) (*Response, error)
```

####　リクエスト例

```go
key := "test_multipart.txt"
v, _, err := client.Object.InitiateMultipartUpload(context.Background(), key, nil)
// Abort
resp, err := client.Object.AbortMultipartUpload(context.Background(), key, v.UploadID)
```

#### パラメータ説明

| パラメータ名称 | パラメータ説明                                                     | タイプ | 必須項目 |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| Key      | オブジェクトキー（Key）はバケットにおけるオブジェクトの唯一の識別子です。例えば、オブジェクトのアクセスドメイン名` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg `において、オブジェクトキーは doc1/pic1.jpgです | string | はい   |
| UploadId | マルチパートアップロードのIDにタグを付けます                                            | string |はい   |

### パートのアップロード

##### 機能説明

パートを指定のUploadIdにアップロードします。パートごとのサイズは5GB以内でなければなりません。

#### 方法のプロトタイプ

```go
func (s *ObjectService) UploadPart(ctx context.Context, key, uploadID string, partNumber int, r io.Reader, opt *ObjectUploadPartOptions) (*Response, error)
```

####　リクエスト例

```go
//ご注意：アップロードするパート数は最大で10000パートです
key := "test/test_multi_upload.go"
f := strings.NewReader("test heoo")
//opt選択可能
_, err := client.Object.UploadPart(
    context.Background(), key, uploadID, 1, f, nil,
)
```

#### パラメータ説明

```go
type ObjectUploadPartOptions struct {
    ContentLength   int                                      
}
```

| パラメータ名称      | パラメータ説明                                                     | タイプ      | 必須項目 |
| ------------- | ------------------------------------------------------------ | --------- | ---- |
| Key           | オブジェクトキー（Key）はバケットにおけるオブジェクトの唯一の識別子です。例えば、オブジェクトのアクセス ドメイン名` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg ` において、オブジェクトキーはdoc1/pic1.jpgです | string    | はい   |
| UploadId      | マルチパートアップロードのIDにタグ付けます。InitiateMultipartUploadにより生成します             | string    | はい   |
| PartNumber | アップロードするパートの番号にタグを付けます                                           | int       | はい   |
| r             | アップロードするファイルの内容は、ファイルストリームまたはバイトストリームであってよいです。rがbytes.Buffer/bytes.Reader/strings.Readerでない場合、opt.ContentLength | io.Readerを指定しなければなりません | io.Reader | はい   |
| ContentLength        | 送信長さの設定                                                 | int      | いいえ   |

#### 戻り結果の説明

```go
{
    'ETag': 'string'
}
```

| パラメータ名    | パラメータ説明            | タイプ   |
| -------- | ------------------- | ------ |
| ETag     | パートのMD5値のアップロード。 | string |

### パートのリスト 

##### 機能説明

指定UploadIdにおいてアップロード済みのパートの情報をリストします。

#### 方法のプロトタイプ

```go
func (s *ObjectService) ListParts(ctx context.Context, name, uploadID string) (*ObjectListPartsResult, *Response, error)
```

####　リクエスト例

```go
key := "test/test_list_parts.go"
v, resp, err := client.Object.ListParts(context.Background(), key, uploadID) 
```

#### パラメータ説明

| パラメータ名称 | パラメータ説明                                                     | タイプ | 必須項目 |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| Key      | オブジェクトキー（Key）はバケットにおけるオブジェクトの唯一の識別子です。例えば、オブジェクトのアクセスドメイン名` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg `において、オブジェクトキーは doc1/pic1.jpgです | string | はい   |
| UploadId | マルチパートアップロードのIDにタグ付けます。InitiateMultipartUploadにより生成します             | string | はい   |

#### 戻り結果の説明

```go
type ObjectListPartsResult struct {
	Bucket               string
	EncodingType         string 
	Key                  string
	UploadID             string     
	Initiator            *Initiator 
	Owner                *Owner     
	StorageClass         string
	PartNumberMarker     int
	NextPartNumberMarker int 
	MaxParts             int
	IsTruncated          bool
	Parts                []Object 
}
type Initiator struct {
	UIN         string
	ID          string 
	DisplayName string                                
}
type Owner struct {
	UIN         string
	ID          string 
	DisplayName string                                
}
type Object struct {
	Key          string 
	ETag         string 
	Size         int    
	PartNumber   int    
	LastModified string 
	StorageClass string 
	Owner        *Owner
}
```

| パラメータ名             | パラメータ説明                                                     | タイプ   |
| -------------------- | ------------------------------------------------------------ | ------ |
| Bucket             | バケット名称は、bucketname-appidからなります                        | string |
| EncodingType         | デフォルトではエンコーディングせず、返された値のエンコーディング方式を定め、選択可能値：url                | string |
| Key                  | オブジェクトキー（Key）はバケットにおけるオブジェクトの唯一の識別子です。例えば、オブジェクトのアクセスドメイン名` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg `において、オブジェクトキーは doc1/pic1.jpgです | string |
| UploadId             | マルチパートアップロードのIDにタグ付けます。InitiateMultipartUploadにより生成します             | string |
| Initiator            | マルチパートアップロードの作成者。DisplayName、UINとIDを含みます                | struct |
| Owner             | ファイル保有者の情報。DisplayName、UINとIDを含みます                  | struct |
| StorageClass         | ファイルのストレージタイプ。STANDARD、STANDARD_IA、デフォルト値：STANDARD       | string  |
| PartNumberMarker     | デフォルトでは0です。最初のパートからパートをリストし、PartNumberMarkerの次のパートからリストします | int    |
| NextPartNumberMarker | 次回パートをリストする開始位置を表示します                                 | int    |
| MaxParts             | 返されたパートの最大数。デフォルトでは、最大は1000です                       | int    |
| IsTruncated        | 返されたパートが遮断されたかを示します                                  | bool     |
| Part                 | アップロードするパートの関連情報。ETag、PartNumber、Size、LastModifiedを含みます | struct |

### マルチパートアップロードの完成

##### 機能説明

指定UploadIdにおけるすべてのパートを完全なるファイルにまとめます。最終的にファイルサイズは1MB以下でなければなりません。さもなければエラーが返されます。

#### 方法のプロトタイプ

```go
func (s *ObjectService) CompleteMultipartUpload(ctx context.Context, key, uploadID string, opt *CompleteMultipartUploadOptions) (*CompleteMultipartUploadResult, *Response, error)
```

####　リクエスト例

```go
key := "test/test_complete_upload.go"
v, resp, err := client.Object.InitiateMultipartUpload(context.Background(), key, nil)
uploadID := v.UploadID
blockSize := 1024 * 1024 * 3

opt := &cos.CompleteMultipartUploadOptions{}
for i := 1; i < 5; i++ {
    etag := uploadPart(c, key, uploadID, blockSize, i)
    opt.Parts = append(opt.Parts, cos.Object{
        PartNumber: i, ETag: etag},
    )
}

v, resp, err = client.Object.CompleteMultipartUpload(
    context.Background(), key, uploadID, opt,
)
```

#### パラメータ説明

```go
type CompleteMultipartUploadOptions struct {
	Parts   []Object 
}
type Object struct { 
	ETag         string 
	PartNumber   int     
}
```

| パラメータ名称                       | パラメータ説明                                                     | タイプ   | 必須項目 |
| ------------------------------ | ------------------------------------------------------------ | ------ | ---- |
| Key                            | オブジェクトキー（Key）はバケットにおけるオブジェクトの唯一の識別子です。例えば、オブジェクトのアクセスドメイン名` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg `において、オブジェクトキーは doc1/pic1.jpgです | string | はい   |
| UploadId                       | マルチパートアップロードのIDにタグ付けます。InitiateMultipartUploadにより生成します             | string | はい   |
| CompleteMultipartUploadOptions | すべてのパートのETagとPartNumber情報                           | struct | はい   |

#### 戻り結果の説明

```go
type CompleteMultipartUploadResult struct {
	Location string
	Bucket   string
	Key      string
	ETag     string
}
```

| パラメータ名 | パラメータ説明                                              | タイプ  |
| -------- | ------------------------------------------------------------ | ------ |
| Location | URLアドレス                                                     | string |
| Bucket   | バケット名称は、bucketname-appidからなります                        | string   |
| Key      | オブジェクトキー（Key）はバケットにおけるオブジェクトの唯一の識別子です。例えば、オブジェクトのアクセスドメイン名` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg `において、オブジェクトキーは doc1/pic1.jpgです | string |
| ETag     | マージされた後のオブジェクトの唯一のタグ値です。この値はオブジェクト内容のMD5チェックサムではなく、オブジェクト唯一性の検査にのみ用いられます。ファイル内容をチェックするには、アップロードにおいて単独パートのETag値をチェックして良いです。 | string |

### オブジェクトACLの設定

##### 機能説明

ファイルのACL情報を設定する場合、XCosACL、XCosGrantFullControl、XCosGrantRead、XCosGrantWriteを通じてヘッダーを入力するか、あるいはACLXMLを通じてボディを入力することでACLを設定します。競合が発生しないように、二者から1つしか選択できません。

> !現在のアクセスポリシーのエントリは1000条に限られており、オブジェクトACL制御が不要な場合、設定しないでください。デフォルトでバケット権限を受け継ぎます。

#### 方法のプロトタイプ

```go
func (s *ObjectService) PutACL(ctx context.Context, key string, opt *ObjectPutACLOptions) (*Response, error)
```

####　リクエスト例

ヘッダーを通じてObject ACLを設定します

```go
opt := &cos.ObjectPutACLOptions{
    Header: &cos.ACLHeaderOptions{
        XCosACL: "private",
    },
}
key := "test/hello.txt"
resp, err := client.Object.PutACL(context.Background(), key, opt)
```

ボディを通じてObject ACLを設定します

```go
opt = &cos.ObjectPutACLOptions{
    Body: &cos.ACLXml{
        Owner: &cos.Owner{
            ID: "qcs::cam::uin/100000760461:uin/100000760461",
        },
        AccessControlList: []cos.ACLGrant{
            {
                Grantee: &cos.ACLGrantee{
                    Type: "RootAccount",
                    ID:   "qcs::cam::uin/100000760461:uin/100000760461",
                },

                Permission: "FULL_CONTROL",
            },
        },
    },
}

resp, err = client.Object.PutACL(context.Background(), key, opt)
```

#### パラメータ説明

```go
type ACLHeaderOptions struct {
	XCosACL              string 
	XCosGrantRead        string 
	XCosGrantWrite       string 
	XCosGrantFullControl string 
}
```

| パラメータ名称             | パラメータ説明                                                     | タイプ   | 必須項目 |
| -------------------- | ------------------------------------------------------------ | ------ | ---- |
| Key                  | オブジェクトキー（Key）はバケットにおけるオブジェクトの唯一の識別子です。例えば、オブジェクトのアクセスドメイン名` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg `において、オブジェクトキーは doc1/pic1.jpgです | string | はい   |
| XCosACL              | バケットのACLを設定します。例えばprivate、public-read、public-read-write | string | いいえ   |
| XCosGrantFullControl | 指定アカウントに対してバケットへの読み書き権限を付与します。フォーマットは`id=" ",id=" "`サブアカウントに授権する場合、フォーマットは`id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`ルートアカウントに授権する場合、フォーマットは`id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`例えば`id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | String | いいえ   |
| XCosGrantRead        | 指定アカウントに対してバケットへの読み取り権限を付与します。フォーマットは`id=" ",id=" "`サブアカウントに授権する場合、フォーマットは`id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`ルートアカウントに授権する場合、フォーマットは`id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`例えば`id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | いいえ   |
| XCosGrantWrite       | 指定アカウントに対してバケットへの書き込み権限を付与します。フォーマットは`id=" ",id=" "`サブアカウントに授権する場合、フォーマットは`id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`ルートアカウントに授権する場合、フォーマットは`id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`例えば`id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | いいえ   |
| ACLXML               | 指定アカウントに対してバケットへのアクセス権限を付与します。詳しいフォーマットについては、get object aclの返した結果の説明を参照してください | struct | いいえ   |

### オブジェクトACLの取得

##### 機能説明

指定ファイルのACLを取得します。

#### 方法のプロトタイプ

```go
func (s *ObjectService) GetACL(ctx context.Context, key string) (*ObjectGetACLResult, *Response, error)
```

####　リクエスト例

```go
key := "test/hello.txt"
v, resp, err := client.Object.GetACL(context.Background(), key)
```

#### パラメータ説明

| パラメータ名称 | パラメータ説明                                                     | タイプ | 必須項目 |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| Key      | オブジェクトキー（Key）はバケットにおけるオブジェクトの唯一の識別子です。例えば、オブジェクトのアクセスドメイン名` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg `において、オブジェクトキーは doc1/pic1.jpgです | string | はい   |

#### 戻り結果の説明

```go
type ACLXml struct {
	Owner             *Owner
	AccessControlList []ACLGrant 
}
type Owner struct { 
	ID          string 
	DisplayName string
}
type ACLGrant struct {
	Grantee    *ACLGrantee
	Permission string
}
type ACLGrantee struct {
	Type        string 
	ID          string 
	DisplayName string
    UIN         string 
}
```

| パラメータ名          | パラメータ説明                                                     | タイプ   |
| ----------------- | ------------------------------------------------------------ | ------ |
| Owner             | バケット保有者の情報、DisplayNameとIDを含みます                  | struct |
| AccessControlList | バケット権限授与者の情報、GranteeとPermissionを含みます           | struct |
| Grantee           | 権限授与者の情報、DisplayName、Type、IDとUINを含みます          | struct |
| Type              | 権限授与者のタイプ、タイプはCanonicalUserあるいはGroupです            | string |
| ID                | TypeがCanonicalUserである場合、権限授与者のIDに対応します                 | string |
| DisplayName       | 権限授与者の名前                                             | string |
| UIN               | TypeがGroupである場合、権限授与者のUINに対応します                       | string |
| Permission        | 授与者の保有するバケットの権限、選択可能値はFULL_CONTROL、WRITE、READであり、それぞれ読み書き権限、書き込み権限、読み取り権限に対応します | string |

### オブジェクトコピーの設定

##### 機能説明

ファイルをソースパスから目標パスに複製します。推奨のファイルサイズは1M~5Gです。5G以上のファイルについては、マルチパートアップロードしてください（Upload - Copy）。コピーにおいて、ファイルの元プロパティとACLを変更できます。ユーザーはこのAPIを通じてファイルの移動、ファイル名の変更、ファイルプロパティの変更とコピー作成ができます。
>!クロスアカウントでコピーする場合は、コピーされたファイルの権限をパブリック読み取りに設定するか、またはターゲットアカウントに対して、権限を付与する必要があります。同じアカウントは設定する必要がありません。

#### 方法のプロトタイプ

```go
func (s *ObjectService) Copy(ctx context.Context, key, sourceURL string, opt *ObjectCopyOptions) (*ObjectCopyResult, *Response, error)
```

####　リクエスト例

```go
u, _ := url.Parse("http://test-1253846586.cos.ap-guangzhou.myqcloud.com")
source := "test/objectMove_src"
soruceURL := fmt.Sprintf("%s/%s", u.Host, source)
dest := "test/objectMove_dest"
//opt := &cos.ObjectCopyOptions{}
r, resp, err := client.Object.Copy(context.Background(), dest, soruceURL, nil)
```

#### パラメータ説明

```go
type ObjectCopyOptions struct {
	*ObjectCopyHeaderOptions 
	*ACLHeaderOptions        
}
type ACLHeaderOptions struct {
	XCosACL              string 
	XCosGrantRead        string 
	XCosGrantWrite       string 
	XCosGrantFullControl string 
}
type ObjectCopyHeaderOptions struct {
	XCosMetadataDirective           string 
	XCosCopySourceIfModifiedSince   string 
	XCosCopySourceIfUnmodifiedSince string 
	XCosCopySourceIfMatch           string 
	XCosCopySourceIfNoneMatch       string 
	XCosStorageClass                string 
	//カスタマイズのx-cos-meta-* header
	XCosMetaXXX    				    *http.Header 
	XCosCopySource 					string      
}
```

| パラメータ名称                        | パラメータ説明                                                     | タイプ        | 必須項目 |
| ------------------------------- | ------------------------------------------------------------ | ----------- | ---- |
| Key                             | オブジェクトキー（Key）はバケットにおけるオブジェクトの唯一の識別子です。例えば、オブジェクトのアクセスドメイン名` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg `において、オブジェクトキーは doc1/pic1.jpgです | string      | はい   |
| sourceURL                       | ソースファイルのURLの説明                                          | string      | はい   |
| XCosACL                         | ファイルのACLを設定します。例えば、private、public-read、public-read-write    | string      | いいえ   |
| XCosGrantFullControl            | 指定アカウントに対してファイルへの読み書き権限を付与します。フォーマットは：id=" ",id=" "。サブアカウントに授権する場合、フォーマットは`id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`ルートアカウントに授権する場合、フォーマットは`id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`例えば`id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | String      | いいえ   |
| XCosGrantRead                   | 指定アカウントに対してファイルへの読み取り権限を授与します。フォーマットは`id=" ",id=" "`サブアカウントに授権する場合、フォーマットは`id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`ルートアカウントに授権する場合、フォーマットは`id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`例えば`id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string      | いいえ   |
| XCosGrantWrite                  | 指定アカウントに対してファイルへの書き込み権限を付与します。フォーマットは`id=" ",id=" "`サブアカウントに授権する場合、フォーマットは`id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`ルートアカウントに授権する場合、フォーマットは`id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`例えば`id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string      | いいえ   |
| XCosMetadataDirective           | 選択可能値は CopyとReplacedです。Copyに設定する場合、設定したユーザーのメタデータ情報を無視して直接コピーできます。Replacedに設定する場合、設定したソース情報によりメタデータを変更します。目標パスとソースパスが同じである場合、Replacedに設定しなければなりません | string      | はい   |
| XCosCopySourceIfModifiedSince   |  オブジェクトが指定時間後に変更される場合、操作は実行されます。さもなければ412が返されます。XCosCopySourceIfNoneMatchと併用できますが、その他条件と併用する場合、競合が返されます。 | string      | いいえ   |
| XCosCopySourceIfUnmodifiedSince |  オブジェクトが指定時間後に変更される場合、操作は実行されます。さもなければ412が返されます。XCosCopySourceIfMatchと併用できますが、その他条件と併用する場合、競合が返されます。 | string      | いいえ   |
| XCosCopySourceIfMatch           | オブジェクトのEtagと所与の条件が一致する場合、操作は実行されます。さもなければ412が返されます。XCosCopySourceIfUnmodifiedSinceと併用できますが、その他条件と併用する場合、競合が返されます。 | string      | いいえ   |
| XCosCopySourceIfNoneMatch           | オブジェクトのEtagと所与の条件が不一致である場合、操作は実行されます。さもなければ412が返されます。XCosCopySourceIfModifiedSinceと併用できますが、その他条件と併用する場合、競合が返されま。 | string      | いいえ   |
| XCosStorageClass                | ファイルのストレージクラスを設定します。STANDARD、STANDARD_IA、デフォルト値：STANDARD   | string      | いいえ   |
| XCosMetaXXX                     | ユーザーカスタマイズのファイルのソース情報                                       | http.Header | いいえ   |
| XCosCopySource                  | ソースファイルURLパス。versionidサブリソースにより履歴バージョンを指定できます       | string      | いいえ   |

#### 戻り結果の説明

アップロードするファイルのプロパティ：

```go
type ObjectCopyResult struct {
    ETag         string 
    LastModified string
}
```

| パラメータ名     | パラメータ説明                   | タイプ   |
| ------------ | -------------------------- | ------ |
| ETag         | ファイルのMD5値のコピー          | string |
| LastModified | コピーファイルの最終変更時間 | string |

## 異常説明

APIの返すResponseはGolang httpスタンダードライブラリ[Response](https://golang.org/pkg/net/http/#Response)タイプです。
err.Error()によりエラー情報（サーバーから返された詳細情報）を取得できます。エラーコードに関する詳細については：[COSエラーコード](https://cloud.tencent.com/document/product/436/7730)を参照してください。

