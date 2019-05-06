COS XML API Python SDKの操作が正常に終了した場合、dictまたはNoneが返され、失敗した場合は、異常（CosClientErrorおよびCosServiceError）がスローされます。異常クラスは、文末の異常タイプの説明に従って、エラーメッセージを提供します。
>?文章に記載されているSecretId、SecretKey、Bucketなどの名称の意味と取得方式については、[COS用語情報](https://cloud.tencent.com/document/product/436/7751)を参照してください。

## Bucket API説明
### Bucketの作成

##### 機能説明

指定アカウントの下で新しいバケットを作成し、バケットが存在している場合、エラーが返されます。

#### 方法のプロトタイプ

```
create_bucket(Bucket, **kwargs)
```
####　リクエスト例

```python
response = client.create_bucket(
    Bucket='test01-123456789',
    ACL='private'|'public-read'|'public-read-write',
    GrantFullControl='string',
    GrantRead='string',
    GrantWrite='string'	
)
```
#### パラメータ説明

| パラメータ名称   | パラメータ説明   |タイプ | 必須項目 | 
| -------------- | -------------- |---------- | ----------- |
| Bucket　|作成するバケット名は、bucketname-appidからなります|String| はい|
| ACL |‘private’、‘public-read’、‘public-read-write’などバケットのACLを設定します。 |String| いいえ|
| GrantFullControl |指定されたアカウントにバケットへの読み取りと書き込み権限を付与します。`id=" ",id=" "`というフォーマットになります。サブアカウントの承認が必要な場合、`id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`というフォーマットになります。ルートアカウントの承認が必要な場合、`id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`というフォーマットになります。例えば、`'id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"'`などです。|String|いいえ|
|GrantRead |指定されたアカウントにバケットへの読み取り権限を付与します。`id=" ",id=" "`というフォーマットになります。サブアカウントの承認が必要な場合、`id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`というフォーマットになります。ルートアカウントの承認が必要な場合、`id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`というフォーマットになります。例えば、`'id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"'`などです。|String|いいえ|
| GrantWrite |指定アカウントに対してバケットへの書き込み権限を付与します。フォーマットは`id=" ",id=" "`サブアカウントに授権する場合、フォーマットは`id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`ルートアカウントに授権する場合、フォーマットは`id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`例えば`'id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"'`|String|いいえ|

#### 戻り結果の説明
このメソッドの戻り値はNoneです。

### バケットの削除

##### 機能説明

指定アカウントの下で存在しているバケットを削除する場合、バケットはブランクでなければなりません。

#### 方法のプロトタイプ

```
delete_bucket(Bucket)
```
####　リクエスト例

```python
response = client.delete_bucket(
    Bucket='test01-123456789'
)
```
#### パラメータ説明

| パラメータ名称   | パラメータ説明   |タイプ | 必須項目 | 
| -------------- | -------------- |---------- | ----------- |
|Bucket |削除するバケット名は、bucketname-appidからなります|String|はい|

#### 戻り結果の説明
このメソッドの戻り値はNoneです。

###　バケットが存在するかの照合

##### 機能説明

バケットが存在するか、あるいはアクセス権があるかを照合します。

#### 方法のプロトタイプ

```
head_bucket(Bucket)
```
####　リクエスト例

```python
response = client.head_bucket(
    Bucket='test01-123456789'
)
```
#### パラメータ説明

| パラメータ名称   | パラメータ説明   |タイプ | 必須項目 | 
| -------------- | -------------- |---------- | ----------- |
|Bucket　|照合するバケット名は、bucketname-appidからなります|String|はい|

#### 戻り結果の説明
このメソッドの戻り値はNoneです。

###　バケット地域情報の取得

##### 機能説明

バケットの所在地域の情報を照合します。

#### 方法のプロトタイプ

```
get_bucket_location(Bucket)
```
####　リクエスト例

```python
response = client.get_bucket_location(
    Bucket='test01-123456789'
)
```
#### パラメータ説明

| パラメータ名称   | パラメータ説明   |タイプ | 必須項目 | 
| -------------- | -------------- |---------- | ----------- |
|Bucket　|照合するバケット名は、bucketname-appidからなります|String|はい|

#### 戻り結果の説明

バケット地域情報、タイプはDictです。
```python
{
    'LocationConstraint': 'ap-beijing-1'|'ap-beijing'|'ap-shanghai'|'ap-guangzhou'|'ap-chengdu'|'ap-chongqing'|'ap-singapore'|'ap-hongkong'|'na-toronto'|'eu-frankfurt'|'ap-mumbai'|'ap-seoul'|'na-siliconvalley'|'na-ashburn'
}
```

| パラメータ名   | パラメータの説明   |タイプ | 
| -------------- | -------------- |---------- | 
| LocationConstraint |バケットの所在地域の情報|String|

### バケットの下にあるすべてのファイルの一覧表示 

##### 機能説明

指定されたバケットにあるすべてのオブジェクトを取得します。

#### 方法のプロトタイプ

```
list_objects(Bucket, Delimiter="", Marker="", MaxKeys=1000, Prefix="", EncodingType="", **kwargs)
```
####　リクエスト例

```python
response = client.list_objects(
    Bucket='test01-123456789',
    Prefix='string',
    Delimiter='/',
    Marker='string',
    MaxKeys=100,
    EncodingType='url'
)
```
#### パラメータ説明

| パラメータ名称   | パラメータ説明   |タイプ | 必須項目 | 
| -------------- | -------------- |---------- | ----------- |
| Bucket   | バケット名は、bucketname-appidからなります　　| String  | はい| 
| Prefix   |  デフォルトではブランクであり、オブジェクトのKeyをフィルタし、入力した場合、prefixを参照しオブジェクトをリストします  | string |  いいえ| 
| Delimiter   |   デフォルトではブランクであり、区切り記号を設定し、例えばフォルダを設定/シミュレートします  | string |  いいえ|
| Marker   |  デフォルトでUTF-8 2進数順のエントリをリストし、返されたオブジェクトのリストの開始位置にタグを付けます。  | String  |  いいえ| 
| MaxKeys   | 返されたオブジェクトの最大数。デフォルトは最大1000  | Int  |  いいえ| 
| EncodingType   |   デフォルトはエンコードなし、戻り値のエンコード方法を指定します。オプションの値：url  | String  | いいえ|

#### 戻り結果の説明

オブジェクトのメタ情報（タイプはDict）を取得します。

```python
{
    'MaxKeys': '1000', 
    'Prefix': 'string',
    'Delimiter': 'string',
    'Marker': 'string',
    'NextMarker': 'string',
    'Name': 'test04-1252448703',  
    'IsTruncated': 'false'|'true',
    'EncodingType': 'url',
    'Contents':[
        {
            'ETag': '"a5b2e1cfb08d10f6523f7e6fbf3643d5"', 
            'StorageClass': 'STANDARD', 
            'Key': 'zh.cn.txt'
            'Owner': {
                'DisplayName': '1252448703',
                'ID': '1252448703'
            }, 
            'LastModified': '2017-08-08T09:43:35.000Z', 
            'Size': '23'
        },
    ],
    'CommonPrefixes':[
        {
            'Prefix': 'string'
        },
    ],
}
```

| パラメータ名   | パラメータの説明   |タイプ | 
| -------------- | -------------- |---------- |
| MaxKeys   | 返されたオブジェクトの最大数、デフォルトでは最大1000です  | int    |
| Prefix   |  デフォルトではブランクであり、オブジェクトのKeyをフィルタし、入力した場合、prefixを参照しオブジェクトをリストします  | string|
| Delimiter   |   デフォルトではブランクであり、区切り記号を設定し、例えばフォルダを設定/シミュレートします  | string |
| Marker   |  デフォルトはUTF-8 2進数順でエントリをリストし、返されたオブジェクトリストのの開始位置にタグを付けます。  | String  |
| NextMarker|  IsTruncatedがtrueの場合、タグは次にオブジェクトのリストの開始位置に返します。  | String  |
| Name   |  バケット名、bucketname-appidからなります  | String  | 
| IsTruncated   |  返されたオブジェクトは切り捨てられたかを示します。  | String|
| EncodingType   | デフォルトはエンコードなし、戻り値のエンコード方法を指定します。オプションの値：url  | String  | いいえ|
|Contents |‘ETag’、‘StorageClass’、‘Key’、‘Owner’、‘LastModified’、‘Size’など、すべてのオブジェクトメタ情報のリストが含まれています。|List|
|CommonPrefixes |Prefixで始まり、Delimiterで終わるすべてのKeyは同じクラスに分類されます|List| 

### バケットの下にあるすべてのマルチパートアップロードの一覧表示

##### 機能説明

指定されたバケットの下にあるすべての進行中のマルチパートアップロードを取得します。

#### 方法のプロトタイプ

```
list_multipart_uploads(Bucket, Prefix="", Delimiter="", KeyMarker="", UploadIdMarker="", MaxUploads=1000, EncodingType="", **kwargs)
```
####　リクエスト例

```python
response = client.list_multipart_uploads(
    Bucket='test01-123456789',
    Prefix='string',
    Delimiter='string',
    KeyMarker='string',
    UploadIdMarker='string'
    MaxUploads=100,
    EncodingType='url'
)
```
#### パラメータ説明

| パラメータ名称   | パラメータ説明   |タイプ | 必須項目 | 
| -------------- | -------------- |---------- | ----------- |
| Bucket   | バケット名は、bucketname-appidからなります　　| String  | はい|
| Prefix   |  デフォルトではブランクであり、マルチパートアップロードしたkeyをフィルタし、prefixをプレフィックスとしたマルチパートアップロードにマッチングします。  | String  |  いいえ| 
| Delimiter   |   デフォルトではブランクであり、区切り記号を設定します| String|  いいえ|
| KeyMarker   |  UploadIdMarkerとともに使用され、マルチパートアップロードの開始位置を示します  | String  |  いいえ|
| UploadIdMarker   |  KeyMarkerとともに使用され、マルチパートアップロードの開始位置を表示します。KeyMarkerが指定されていない場合、UploadIdMarkerは無視されます| String  |  いいえ|
| MaxUploads  | 返されたマルチパートアップロードの最大数。デフォルトは最大1000  | Int  |  いいえ| 
| EncodingType   |   デフォルトはエンコードなし、戻り値のエンコード方法を指定します。オプションの値：url  | String  | いいえ|

#### 戻り結果の説明

マルチパートアップロードの情報（タイプはDict）を取得します。

```python
{
    'Bucket': 'test04-1252448703',
    'Prefix': 'string',
    'Delimiter': 'string',
    'KeyMarker': 'string',
    'UploadIdMarker': 'string',
    'NextKeyMarker': 'string',
    'NextUploadIdMarker': 'string',
    'MaxUploads': '1000',
    'IsTruncated': 'true'|'false',,
    'EncodingType': 'url',
    'Upload':[
        {
            'UploadId': 'string',
            'Key': 'string',
            'Initiated': 'string',
            'StorageClass': 'STANDARD',
            'Owner': {
                'DisplayName': 'string',
                'ID': 'string'
            },
            'Initiator': {
                'ID': 'string',
                'DisplayName': 'string'
            }
        },
    ],
    'CommonPrefixes':[
        {
            'Prefix': 'string'
        },
    ],
}
```

| パラメータ名   | パラメータの説明   |タイプ | 
| -------------- | -------------- |---------- |
| Bucket   |  バケット名は、bucketname-appidからなります  | String  | 
| Prefix   |  デフォルトではブランクであり、マルチパートアップロードしたkeyをフィルタし、prefixをプレフィックスとしたマルチパートアップロードにマッチングします  | String  |
| Delimiter   |   デフォルトではブランクであり、区切り記号を設定します| String|
| KeyMarker   |  UploadIdMarkerとともに使用され、マルチパートアップロードの開始位置を示します  | String  |
| UploadIdMarker   |  KeyMarkerとともに使用され、マルチパートアップロードの開始位置を表示します。KeyMarkerが指定されていない場合、UploadIdMarkerは無視されます| String  |
| NextKeyMarker   |  IsTruncatedがtrueの場合、次にリストされたマルチパートアップロードされたkeyの開始場所を示します  | String  |
| NextUploadIdMarker   |  IsTruncatedがtrueの場合、次にリストされたマルチパートアップロードされたuploadidの開始場所を示します| String  |
| MaxUploads   | 返されたマルチパートアップロードの最大数。デフォルトは最大1000  | Int  |
| IsTruncated   |  返されたマルチパートアップロードは切り捨てられたかを示します  | String|
| EncodingType   |   デフォルトはエンコードなし、戻り値のエンコード方法を指定します。オプションの値：url  | String  |
|Upload |'UploadId'、'StorageClass'、'Key'、'Owner'、'Initiator'、'Initiated'などのすべてのマルチパートアップロードのリストが含まれています|List|
|CommonPrefixes |Prefixで始まり、Delimiterで終わるすべてのKeyは同じクラスに分類されます|List|

###　Bucket ACL情報の設定

##### 機能説明

ACL、GrantFullControl、GrantRead、およびGrantWriteによってヘッダーを渡すことで、あるいは、AccessControlPolicyを使用してボディを渡すことで、バケットのACL情報を設定します。ただ一つの方法が選択できます。そうでなければ、競合が返されます。

#### 方法のプロトタイプ

```
put_bucket_acl(Bucket, AccessControlPolicy={}, **kwargs)
```
####　リクエスト例

```python
response = client.put_bucket_acl(
    Bucket='test01-123456789',
    ACL='private'|'public-read'|'public-read-write',
    GrantFullControl='string',
    GrantRead='string',
    GrantWrite='string',
    AccessControlPolicy={
        'Grant': [
            {
                'Grantee': {
                    'DisplayName': 'string',
                    'Type': 'CanonicalUser'|'Group',
                    'ID': 'string',
                    'URI': 'string'
                },
                'Permission': 'FULL_CONTROL'|'WRITE'|'READ'
            },
        ],
        'Owner': {
            'DisplayName': 'string',
            'ID': 'string'
        }
    }
)
```
#### パラメータ説明

| パラメータ名称   | パラメータ説明   |タイプ | 必須項目 | 
| -------------- | -------------- |---------- | ----------- |
| Bucket　| バケット名は、bucketname-appidからなります|String|はい|
| ACL |‘private’、‘public-read’、‘public-read-write’などバケットのACLを設定します。 |String| いいえ|
| GrantFullControl |指定されたアカウントにバケットへの読み取りと書き込み権限を付与します。`id=" ",id=" "`というフォーマットになります。サブアカウントの承認が必要な場合、`id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`というフォーマットになります。ルートアカウントの承認が必要な場合、`id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`というフォーマットになります。例えば、`'id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"'`などです。|String|いいえ|
|GrantRead |指定されたアカウントにバケットへの読み取り権限を付与します。`id=" ",id=" "`というフォーマットになります。サブアカウントの承認が必要な場合、`id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`というフォーマットになります。ルートアカウントの承認が必要な場合、`id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`というフォーマットになります。例えば、`'id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"'`などです。|String|いいえ|
| GrantWrite |指定アカウントに対してバケットへの書き込み権限を付与します。フォーマットは`id=" ",id=" "`サブアカウントに授権する場合、フォーマットは`id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`ルートアカウントに授権する場合、フォーマットは`id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`例えば`'id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"'`|String|いいえ|
| AccessControlPolicy| 指定されたアカウントにバケットへのアクセス権を付与します。具体的なフォーマットはget bucket aclから返された結果説明を参照してください|Dict|いいえ |

#### 戻り結果の説明
このメソッドの戻り値はNoneです。

###　Bucket ACL情報の取得

##### 機能説明

指定バケットのACL情報を取得します。

#### 方法のプロトタイプ

```
get_bucket_acl(Bucket, **kwargs)
```
####　リクエスト例

```python
response = client.get_bucket_acl(
    Bucket='test01-123456789',
)
```
#### パラメータ説明

| パラメータ名称   | パラメータ説明   |タイプ | 必須項目 | 
| -------------- | -------------- |---------- | ----------- |
|Bucket | バケット名は、bucketname-appidからなります|String|はい|


#### 戻り結果の説明

Bucket ACL情報、タイプはDictです。
```python
{
    'Owner': {
        'DisplayName': 'string',
        'ID': 'string'
    },
    'Grant': [
        {
            'Grantee': {
                'DisplayName': 'string',
                'Type': 'CanonicalUser'|'Group',
                'ID': 'string',
                'URI': 'string'
            },
            'Permission': 'FULL_CONTROL'|'WRITE'|'READ'
        },
    ]
}
```

| パラメータ名   | パラメータの説明   |タイプ | 
| -------------- | -------------- |---------- | 
| Owner |DisplayName、IDなどのバケット所有者の情報|Dict|
| Grant |Grantee、Permissionなどのバケット権限付与者の情報|List|
| Grantee |DisplayName、Type、ID、URIなどの権限付与者の情報|Dict|
| DisplayName |権限付与者の名前|String|
| Type |権限付与者のタイプはCanonicalUserまたはGroupです|String|
| ID |TypeがCanonicalUserの場合、権限付与者のIDに対応します|String|
| URI |TypeがGroupの場合、権限付与者のURIに対応します|String|
| Permission |権限付与者が所有するバケットの権限。オプションの値はFULL_CONTROL、WRITE、READで、それぞれ読み書き権限、書き込み権限、読み取り権限と対応しています|String|

### バケットクロスオリジン構成の設定

##### 機能説明
指定バケットのクロスオリジンリソース構成を設定します。

#### 方法のプロトタイプ

```
put_bucket_cors(Bucket, CORSConfiguration={}, **kwargs)
```
####　リクエスト例

```python
response = client.put_bucket_cors(
    Bucket='test01-123456789',
    CORSConfiguration={
        'CORSRule': [
            {
                'ID': 'string',
                'MaxAgeSeconds': 100,
                'AllowedOrigin': [
                    'string',
                ],
                'AllowedMethod': [
                    'string',
                ],
                'AllowedHeader': [
                    'string',
                ],
                'ExposeHeader': [
                    'string',
                ]
            }
        ]
    },
)
```
#### パラメータ説明

| パラメータ名称   | パラメータ説明   |タイプ | 必須項目 | 
| -------------- | -------------- |---------- | ----------- |
| Bucket　|バケット名は、bucketname-appidからなります|String| はい|
| CORSRule |ID、MaxAgeSeconds、AllowedOrigin、AllowedMethod、AllowedHeader、ExposeHeaderなどのクロスオリジン規則を設定します|List| はい|
| ID |規則IDの設定|String|いいえ|
| MaxAgeSeconds |オプションリクエストの結果が得られる有効期間を設定します|Int|いいえ|
| AllowedOrigin |`"http://cloud.tencent.com"`のような許可されたアクセスソースを設定し、ワイルドカード*が使用可能です |Dict|はい|
| AllowedMethod |GET、PUT、HEAD、POST、DELETEなど許可されるメソッドを設定します|Dict|はい|
| AllowedHeader |リクエストで使用できるカスタムHTTPリクエストヘッダーを設定します。ワイルドカード*が使用可能です |Dict|いいえ|
| ExposeHeader |ブラウザが受信できるサーバーからのカスタムヘッダー情報を設定します|Dict|いいえ|

#### 戻り結果の説明
このメソッドの戻り値はNoneです。

### バケットクロスオリジン構成の取得

##### 機能説明
指定バケットクロスオリジン構成を取得します。

#### 方法のプロトタイプ

```
get_bucket_cors(Bucket, **kwargs)
```
####　リクエスト例

```python
response = client.get_bucket_cors(
    Bucket='test01-123456789',
)
```
#### パラメータ説明

| パラメータ名称   | パラメータ説明   |タイプ | 必須項目 | 
| -------------- | -------------- |---------- | ----------- |
|Bucket| バケット名は、bucketname-appidからなります|String| はい|

#### 戻り結果の説明

バケットクロスオリジン構成、タイプはDictです。
```python
{
    'CORSRule': [
        {
            'ID': 'string',
            'MaxAgeSeconds': 100,
            'AllowedOrigin': [
                'string',
            ],
            'AllowedMethod': [
                'string',
            ],
            'AllowedHeader': [
                'string',
            ],
            'ExposeHeader': [
                'string',
            ],
        }
    ]
}
```

| パラメータ名   | パラメータの説明   |タイプ |
| -------------- | -------------- |---------- |
 | CORSRule  | ID、MaxAgeSeconds、AllowedOrigin、AllowedMethod、AllowedHeader、ExposeHeaderなどのクロスオリジン規則 |  List | 
 | ID  | 規則ID　| String | 
 | MaxAgeSeconds  |  オプションリクエストの結果が得られる有効期間 | String |
 | AllowedOrigin |`"http://cloud.tencent.com"`のような許可されたアクセスソースはワイルドカード*が使用可能です  | Dict | 
 | AllowedMethod  |  GET、PUT、HEAD、POST、DELETEなどの許可されたメソッド　| Dict |
 | AllowedHeader  |リクエストが使用できるカスタムHTTPリクエストヘッダー、ワイルドカード*が使用可能 |  Dict | 
 | ExposeHeader  | ブラウザが受信できるサーバーからのカスタムヘッダー情報 | Dict | 

###　バケットクロスオリジン構成の削除

##### 機能説明
指定バケットのクロスオリジン構成を削除します。

#### 方法のプロトタイプ

```
delete_bucket_cors(Bucket, **kwargs)
```
####　リクエスト例

```python
response = client.delete_bucket_cors(
    Bucket='test01-123456789',
)
```
#### パラメータ説明

| パラメータ名称   | パラメータ説明   |タイプ | 必須項目 | 
| -------------- | -------------- |---------- | ----------- |
|Bucket　|バケット名は、Bucketname-appidからなります|String| はい

#### 戻り結果の説明

このメソッドの戻り値はNoneです。

### バケットライフサイクル構成の設定

##### 機能説明
指定バケットのライフサイクル構成を設定します。

#### 方法のプロトタイプ

```
put_bucket_lifecycle(Bucket, LifecycleConfiguration={}, **kwargs)
```
####　リクエスト例

```python
from qcloud_cos import get_date
response = client.put_bucket_lifecycle(
    Bucket='test01-123456789',
    LifecycleConfiguration={
        'Rule': [
            {
                'ID': 'string',
                'Filter': {
                    'Prefix': 'string',
                    'Tag': [
                        {
                            'Key': 'string',
                            'Value': 'string'
                        }
                    ]
                },
                'Status': 'Enabled'|'Disabled',
                'Expiration': {
                    'Days': 100,
                    'Date': get_date(2018, 4, 20)
                },
                'Transition': [
                    {
                        'Days': 100,
                        'Date': get_date(2018, 4, 20),
                        'StorageClass': 'Standard_IA'|'Archive'
                    },
                ],
                'NoncurrentVersionExpiration': {
                    'NoncurrentDays': 100
                },
                'NoncurrentVersionTransition': [
                    {
                        'NoncurrentDays': 100,
                        'StorageClass': 'Standard_IA'
                    },
                ],
                'AbortIncompleteMultipartUpload': {
                    'DaysAfterInitiation': 100
                }
            }
        ]   
    }
)
```
#### パラメータ説明

| パラメータ名称   | パラメータ説明   |タイプ | 必須項目 | 
| -------------- | -------------- |---------- | ----------- |
 |  Bucket　　| バケット名は、Bucketname-appidからなります | String |   はい | 
 |  Rule  |  対応の規則を設定します。ID、Filter、Status、Expiration、Transition、NoncurrentVersionExpiration、NoncurrentVersionTransition、AbortIncompleteMultipartUploadが含まれています | List |   はい |
 |  ID  |  規則IDの設定 | String |  いいえ |
 |  Filter  | 規則の影響を説明するために使用されるオブジェクト集合、バケット内のすべてのオブジェクトを設定するには、Prefixを空''に設定してください。| Dict |  はい | 
 |  Status  | Ruleを有効にするかどうかを設定します。オプションの値はEnabledまたはDisabledです | Dict |  はい | 
 |  Expiration  | オブジェクトの期限切れ規則を設定し、日数Daysまたは日付Dateを指定できます。Dateのフォーマットは必ずGMT ISO 8601にします。get_dateメソッドを使用して具体的な日付を指定することをお勧めします。| Dict |  いいえ |
 |  Transition  | オブジェクト変換ストレージタイプの規則を設定し、日数Daysまたは日付Dateを指定できます。Dateのフォーマットは必ずGMT ISO 8601に設定します。特定の日付を指定するにはget_dateメソッドを使用することをお勧めします。StorageClassはStandard_IA、Archiveが選択でき、このような複数の規則を同時に設定できます。| List |  いいえ | 
 |  NoncurrentVersionExpiration  | 現在のバージョン以外のオブジェクトの期限切れ規則を設定、日数NoncurrentDaysが指定できます |  Dict |  いいえ |
 |  NoncurrentVersionTransition  | 現在のバージョン以外のオブジェクト変換ストレージタイプの規則を設定し、日数NoncurrentDaysが指定できます。StorageClassはStandard_IA選択可能で、このような複数の規則を同時に設定できます| List |  いいえ | 
 |  AbortIncompleteMultipartUpload  |マルチパートアップロードの開始から何日か以内にアップロードを完了する必要があることを示します |  Dict |  いいえ | 


#### 戻り結果の説明

このメソッドの戻り値はNoneです。

### バケットライフサイクル構成の取得

##### 機能説明
### 指定されたバケットライフサイクル構成の取得

#### 方法のプロトタイプ

```
get_bucket_lifecycle(Bucket, **kwargs)
```
####　リクエスト例

```python
response = client.get_bucket_lifecycle(
    Bucket='test01-123456789',
)
```
#### パラメータ説明

| パラメータ名称   | パラメータ説明   |タイプ | 必須項目 | 
| -------------- | -------------- |---------- | ----------- |
| Bucket |バケット名は、Bucketname-appidからなります|String|はい |

#### 戻り結果の説明

バケットライフサイクル構成、タイプはDictです。
```python
{
    'Rule': [
        {
            'ID': 'string',
            'Filter': {
                'Prefix': 'string',
                'Tag': [
                        {
                            'Key': 'string',
                            'Value': 'string'
                        }
                ]
            },
            'Status': 'string',
            'Expiration': {
                'Days': 100,
                'Date': 'string'
            },
            'Transition': [
                {
                    'Days': 100,
                    'Date': 'string',
                    'StorageClass': 'STANDARD_IA'|'Archive'
                },
            ],
            'NoncurrentVersionExpiration': {
                'NoncurrentDays': 100
            },
            'NoncurrentVersionTransition': [
                {
                    'NoncurrentDays': 100,
                    'StorageClass': 'STANDARD_IA'
                },
            ],
            'AbortIncompleteMultipartUpload': {
                'DaysAfterInitiation': 100
            }
        }
    ]   
}
```

| パラメータ名   | パラメータの説明   |タイプ |
| -------------- | -------------- |---------- | 
|  Rule  |  ID、Filter、Status、Expiration、Transition、NoncurrentVersionExpiration、NoncurrentVersionTransition、AbortIncompleteMultipartUploadなどの対応の規則 | List | 
|  ID  | 規則ID | String | 
|  Filter  |  規則の影響を説明するために必要なオブジェクトコレクション | Dict |
|  Status  | Ruleを有効にするかどうかを設定します。オプションの値はEnabledまたはDisabledです | Dict |
|  Expiration  |オブジェクトの期限切れ規則は日付Daysまたは日付Dateを指定できます |  Dict | 
|  Transition  | オブジェクト変換ストレージタイプの規則は日数Daysまたは日付Dateを指定できます。StorageClassはSTANDARD_IA、Archiveが選択可能です| List | 
|  NoncurrentVersionExpiration  | 現在のバージョン以外のオブジェクトの期限切れ規則、日数NoncurrentDaysを指定できます |  Dict |
|  NoncurrentVersionTransition  | 現在のバージョン以外のオブジェクト変換ストレージタイプの規則は日数NoncurrentDaysが指定できます。StorageClassはSTANDARD_IAが選択可能です| List | 
|  AbortIncompleteMultipartUpload  |  マルチパートアップロードの開始から何日か以内にアップロードを完了します | Dict |

###　 バケットライフサイクル構成の削除

##### 機能説明

指定バケットのライフサイクル構成を削除します。

#### 方法のプロトタイプ

```
delete_bucket_lifecycle(Bucket, **kwargs)
```
####　リクエスト例

```python
response = client.delete_bucket_lifecycle(
    Bucket='test01-123456789',
)
```
#### パラメータ説明

| パラメータ名称   | パラメータ説明   |タイプ | 必須項目 | 
| -------------- | -------------- |---------- | ----------- |
| Bucket |バケット名は、Bucketname-appidからなります|String|はい |

#### 戻り結果の説明

このメソッドの戻り値はNoneです。


###　バケットバージョン制御構成の設定

##### 機能説明
指定されたバケットバージョン制御関連の構成を設定します。

#### 方法のプロトタイプ

```
put_bucket_versioning(Bucket, Status, **kwargs)
```
####　リクエスト例

```pythone
response = client.put_bucket_versioning(
    Bucket='test01-123456789',
    Status='Enabled'|'Suspended'
)
```
#### パラメータ説明

| パラメータ名称   | パラメータ説明   |タイプ | 必須項目 | 
| -------------- | -------------- |---------- | ----------- |
|  Bucket　　| バケット名は、Bucketname-appidからなります | String |   はい | 
|  Status  | バケットバージョン制御のステータスを設定し、オプションの値は‘Enabled’、‘Suspended’です | String |   はい |

#### 戻り結果の説明

このメソッドの戻り値はNoneです。

###　バケットバージョン制御構成の取得

##### 機能説明
指定されたバケットバージョン制御構成を取得します。

#### 方法のプロトタイプ

```
get_bucket_versioning(Bucket, **kwargs)
```
####　リクエスト例

```python
response = client.get_bucket_versioning(
    Bucket='test01-123456789',
)
```
#### パラメータ説明

| パラメータ名称   | パラメータ説明   |タイプ | 必須項目 | 
| -------------- | -------------- |---------- | ----------- |
| Bucket |バケット名は、Bucketname-appidからなります|String|はい |

#### 戻り結果の説明

バケットバージョン制御構成、タイプはDictです。
```python
{
    'Status': 'Enabled'|'Suspended'
}
```

| パラメータ名   | パラメータの説明   |タイプ |
| -------------- | -------------- |---------- | 
|  Status  |  バケットのバージョン制御のステータスについては、オプションの値は‘Enabled’、‘Suspended’です | String | 


###　バケットドメイン間コピー構成の設定

##### 機能説明
指定されたバケットのドメイン間コピー構成を設定します。

#### 方法のプロトタイプ

```
put_bucket_replication(Bucket, ReplicationConfiguration={}, **kwargs)
```
####　リクエスト例

```python
response = client.put_bucket_replication(
    Bucket='test01-123456789',
    ReplicationConfiguration={
        'Role': 'qcs::cam::uin/735901238:uin/735901238',
        'Rule': [
            {
                'ID': 'string',
                'Status': 'Enabled'|'Disabled',
                'Prefix': 'string',
                'Destination': {
                    'Bucket': 'qcs::cos:ap-shanghai::replicationsouth-1252448703',
                    'StorageClass': 'STANDARD'|'STANDARD_IA'
                }
            }
        ]   
    }
)
```
#### パラメータ説明

| パラメータ名称   | パラメータ説明   |タイプ | 必須項目 | 
| -------------- | -------------- |---------- | ----------- |
|  Bucket　　| ソースバケット名は、Bucketname-appidからなります | String |   はい | 
|  Role  |  発起者のIDラベル、フォーマットはqcs::cam::uin/<OwnerUin>:uin/<SubUin>になります | String |  いいえ |
|  Rule  |  ID、Status、Prefix、Destinationなどの対応の規則を設定します | List |   はい |
|  ID  |  規則IDの設定 | String |  いいえ |
|  Status  | Ruleを有効にするかどうか設定し、オプションの値はEnabledまたはDisabledです | String |  はい |
|  Prefix  | Ruleのプレフィックスマッチング規則を設定します。ブランクの場合、バケット内のすべてのオブジェクトに適用することを示します | String |  はい |
|  Destination  | Bucket、StorageClassなど目的リソースを説明します| Dict |  はい | 
|  Bucket  | ドメイン間でコピーする目的バケットを設定します。フォーマット：qcs::cos:[region]::[bucketname-AppId] | String |  はい |
|  StorageClass  | 目的ファイルのストレージタイプを設定します。オプションの値は‘STANDARD’、‘STANDARD_IA’です | String |  いいえ |

#### 戻り結果の説明

このメソッドの戻り値はNoneです。

### バケットドメイン間コピー構成の取得

##### 機能説明
指定されたバケットドメイン間コピー構成を取得します。

#### 方法のプロトタイプ

```
get_bucket_replication(Bucket, **kwargs)
```
####　リクエスト例

```python
response = client.get_bucket_replication(
    Bucket='test01-123456789'
)
```
#### パラメータ説明

| パラメータ名称   | パラメータ説明   |タイプ | 必須項目 | 
| -------------- | -------------- |---------- | ----------- |
|  Bucket　　| バケット名は、Bucketname-appidからなります | String |   はい | 

#### 戻り結果の説明

バケットドメイン間コピー構成、タイプはDictです。
```python
{
    'Role': 'qcs::cam::uin/735901238:uin/735901238',
    'Rule': [
        {
            'ID': 'string',
            'Status': 'Enabled'|'Disabled',
            'Prefix': 'string',
            'Destination': {
                'Bucket': 'qcs::cos:ap-shanghai::replicationsouth-1252448703',
                'StorageClass': 'STANDARD'|'STANDARD_IA'
            }
        }
    ]   
}
```

| パラメータ名   | パラメータの説明   |タイプ |
| -------------- | -------------- |---------- | 
|  Role  |  発起者のIDラベル、フォーマットはqcs::cam::uin/<OwnerUin>:uin/<SubUin>になります | String |  いいえ |
|  Rule  |  ID、Status、Prefix、Destinationなどの対応の規則をドメイン間でコピーします | List |   はい |
|  ID  |のドメイン間での規則コピーのID　| String |  いいえ |
|  Status  | ドメイン間でのRuleコピーを有効にするか、オプションの値はEnabledまたはDisabledです | String |  はい |
|  Prefix  | ドメイン間でRuleのプレフィックスマッチング規則をコピーします。ブランクの場合、バケット内のすべてのオブジェクトに適用することを説明します。| String |  はい |
|  Destination  | Bucket、StorageClassなど目的リソースを説明します| Dict |  はい | 
|  Bucket  | ドメイン間でコピーの目的バケット、フォーマット：qcs::cos:[region]::[bucketname-AppId] | String |  はい |
|  StorageClass  | 目的ファイルのストレージタイプ、オプションの値は‘STANDARD’、‘STANDARD_IA’です。 | String |  いいえ |

### バケットドメイン間コピー構成の削除

##### 機能説明

指定されたバケットドメイン間コピー構成を削除します。

#### 方法のプロトタイプ

```
delete_bucket_replication(Bucket, **kwargs)
```
####　リクエスト例

```python
response = client.delete_bucket_replication(
    Bucket='test01-123456789',
)
```
#### パラメータ説明

| パラメータ名称   | パラメータ説明   |タイプ | 必須項目 | 
| -------------- | -------------- |---------- | ----------- |
| Bucket |バケット名は、Bucketname-appidからなります|String|はい |

#### 戻り結果の説明

このメソッドの戻り値はNoneです。

## Object API説明

### 簡単なファイルアップロード

##### 機能説明

ローカルのファイルまたは入力ストリームを指定のバケットにアップロードすることに対応します。20 MB以内の小型ファイルをアップロードすることが望ましいです。毎回アップロードのサイズ制限は5 GBで、大容量ファイルのアップロードについては、マルチパートアップロードを使用してください。
>!現在のアクセスポリシーエントリは1000条に制限されています。オブジェクトACL制御が不要な場合は、アップロード時に設定しないでください。デフォルトはバケット権限が継承されます。

#### 方法のプロトタイプ

```
put_object(Bucket, Body, Key, **kwargs)
```
####　リクエスト例

```python
response = client.put_object(
    Bucket='test01-123456789',
    Body=b'abc'|file,
    Key='test.txt',
    EnableMD5=False
)
```
#### すべてのパラメータのリクエスト例
```python
response = client.put_object(
    Bucket='test01-123456789',
    Body=b'abc'|file,
    Key='test.txt',
    EnableMD5=False|True,
    ACL='private'|'public-read'|'public-read-write',  # このパラメータは慎重に使用してください。そうしないと、1000条ACL上限値に達します。
    GrantFullControl='string',
    GrantRead='string',
    GrantWrite='string',
    StorageClass='STANDARD'|'STANDARD_IA',
    Expires='string',
    CacheControl='string',
    ContentType='string',
    ContentDisposition='string',
    ContentEncoding='string',
    ContentLanguage='string',
    ContentLength='123',
    ContentMD5='string',
    Metadata={
        'x-cos-meta-key1': 'value1',
        'x-cos-meta-key2': 'value2'
    }
)
```
#### パラメータ説明


| パラメータ名称   | パラメータ説明   |タイプ | 必須項目 | 
| -------------- | -------------- |---------- | ----------- |
 |  Bucket  |  バケット名は、Bucketname-appidからなります | String |   はい |
 |  Body  | アップロードするファイルの内容はファイルストリームまたはバイトストリームです　|　file/bytes　|  はい |
 |  Key  | オブジェクトキー（Key）は、バケット内のオブジェクトの唯一の識別子です。たとえば、オブジェクトのアクセスドメイン名`bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`では、オブジェクトキーはdoc1/pic1.jpgです | String |  はい | 
| EnableMD5 | SDKによるContent-MD5の計算が必要ですか。デフォルトはオフになっています。オンにすると、アップロードに多くの時間がかかります。|Bool | いいえ| 
| ACL |‘private’、‘public-read’、‘public-read-write’などファイルのACLを設定します |String| いいえ|
| GrantFullControl |指定したアカウントにファイルへの読み書き権限を付与します。`id =" ",id = " "`というフォーマットになります。サブアカウントへの承認が必要な場合、`id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`になります。ルートアカウントへの承認が必要な場合は`id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`というフォーマットになります。例えば、`'id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"'`などです。|String|いいえ|
|GrantRead |指定したアカウントにバケットへの読み取り権限を付与します。`id=" ",id=" "`というフォーマットになります。サブアカウントへの承認が必要な場合、`id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`になります。ルートアカウントへの承認が必要な場合は`id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`というフォーマットになります。例えば、`'id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"'`などです。|String|いいえ|
| GrantWrite|指定したアカウントにバケットへの書き込み権限を付与します。`id =" ",id=" "`というフォーマットになります。サブアカウントへの承認が必要な場合、`id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`というフォーマットになります。ルートアカウントへの承認が必要な場合は`id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`になります。例えば、`'id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"'`などです。|String|いいえ|
 |  StorageClass  |  ファイルのストレージタイプ（STANDARD、STANDARD_IA）の設定。デフォルト値：STANDARD | String |   いいえ |
 |  Expires  | Content-Expiresの設定 | String|  いいえ | 
 |  CacheControl  |  キャッシュポリシー、Cache-Controlの設定 | String |   いいえ |
 |  ContentType  | 内容タイプ、Content-Typeの設定 |String |   いいえ |  
 |  ContentDisposition  |  ファイル名、Content-Dispositionの設定 | String |   いいえ |
 |  ContentEncoding  |  エンコードフォーマット、Content-Encodingの設定 | String |   いいえ |
 |  ContentLanguage  |  言語タイプ、Content-Languageの設定 | String |   いいえ |
 |  ContentLength  | 伝送長さの設定 | String |   いいえ | 
 |  ContentMD5  | 検証するためにアップロードされたファイルのMD5値の設定 | String |   いいえ | 
 |  Metadata | ユーザー設定のファイルのメタ情報はx-cos-metaで始まる必要があります。それ以外の場合は無視されます | Dict |  いいえ |

#### 戻り結果の説明
アップロードするファイルのプロパティ、タイプはDictです。

```python
{
    'ETag': 'string',
    'x-cos-expiration': 'string'
}
```


| パラメータ名   | パラメータの説明   |タイプ | 
| -------------- | -------------- |---------- |
|  ETag   |  アップロードファイルのMD5値  | String  |
|  x-cos-expiration   | ライフサイクルを設定した後、ファイルの期限切れ時間を返します  | String  | 
	
### ファイルのダウンロード

##### 機能説明
指定バケットにおけるファイルをローカルにダウンロードします。

#### 方法のプロトタイプ

```
 get_object(Bucket, Key, **kwargs)
```
####　リクエスト例

```python
response = client.get_object(
    Bucket='test01-123456789',
    Key='test.txt',
    Range='string',
    IfMatch='string',
    IfModifiedSince='string',
    IfNoneMatch='string',
    IfUnmodifiedSince='string',
    ResponseCacheControl='string',
    ResponseContentDisposition='string',
    ResponseContentEncoding='string',
    ResponseContentLanguage='string',
    ResponseContentType='string',
    ResponseExpires='string',
    VersionId='string'
)
```
#### パラメータ説明

| パラメータ名称   | パラメータ説明   |タイプ | 必須項目 | 
| -------------- | -------------- |---------- | ----------- |
 |  Bucket　　|  バケット名は、bucketname-appidからなります | String  |  はい | 
 |  Key  |  オブジェクトキー（Key）は、バケット内のオブジェクトの唯一の識別子です。たとえば、オブジェクトのアクセスドメイン名`bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`では、オブジェクトキーはdoc1/pic1.jpgです | String  | はい | 
 |  Range  |  ダウンロードファイルの範囲をbytes=first-lastのフォーマットで設定します  | String  |  いいえ | 
 |  IfMatch  |  ETagが指定した内容と一致する場合に返されます |String  | いいえ |  
 |  IfModifiedSince  |   指定された時間後に変更された場合に返されます　| String  | いいえ |
 |  IfNoneMatch  |  ETagが指定した内容と一致しない場合に返されます | String  | いいえ | 
 |  IfUnmodifiedSince  |  ファイル変更時刻が指定された時刻より早いか等しい時さえ返されます | String  | いいえ|
 |  ResponseCacheControl  |  応答ヘッダーCache-Controlの設定 | String  | いいえ | 
 |  ResponseContentDisposition  |  応答ヘッダーContent-Dispositionの設定| String  | いいえ | 
 |  ResponseContentEncoding  |   応答ヘッダーContent-Encodingの設定 | String  | いいえ |
 |   ResponseContentLanguage |  応答ヘッダーContent-Languageの設定 | String  | いいえ | 
 |  ResponseContentType  |   応答ヘッダーContent-Typeの設定 | String  | いいえ |
 |  ResponseExpires  |応答ヘッダーContent-Expiresの設定 |   String  | いいえ | 
 |  VersionId  | アップロードファイルのバージョンの指定 |  String  | いいえ | 

#### 戻り結果の説明

ファイルのボディとメタ情報（タイプはDict）をアップロードします。

```python
{
    'Body': StreamBody(),
    'Accept-Ranges': 'bytes',
    'Content-Type': 'application/octet-stream',
    'Content-Length': '16807',
    'Content-Disposition': 'attachment; filename="filename.jpg"',
    'Content-Range': 'bytes 0-16086/16087',
    'ETag': '"9a4802d5c99dafe1c04da0a8e7e166bf"',
    'Last-Modified': 'Wed, 28 Oct 2014 20:30:00 GMT',
    'x-cos-request-id': 'NTg3NzQ3ZmVfYmRjMzVfMzE5N182NzczMQ=='
}
```

| パラメータ名   | パラメータの説明   |タイプ | 
| -------------- | -------------- |---------- | 
 | Body  |  ファイルの内容をダウンロードします。get_raw_streamメソッドはファイルのストリームを取得でき、`get_stream_to_file`メソッドはファイルの内容を指定されたローカルファイルにダウンロードできます | StreamBody |
 | ファイルのメタ情報  |  Etagやx-cos-request-idなどのファイルのメタ情報をダウンロードすると、設定されたファイルのメタ情報も返されます | String |


### 事前署名ダウンロードリンクの取得

##### 機能説明
事前署名ダウンロードリンクを取得し、直接なダウンロードに使われます。

#### 方法のプロトタイプ

```
get_presigned_download_url(Bucket, Key, Expired=300, Params={}, Headers={})
```
####　リクエスト例

```python
response = client.get_presigned_download_url(
    Bucket='test01-123456789',
    Key='test.txt'
)
```
#### パラメータ説明

| パラメータ名称   | パラメータ説明   |タイプ | 必須項目 | 
| -------------- | -------------- |---------- | ----------- |
 | Bucket  | バケット名は、Bucketname-appidからなります |  String |  はい | 
 | Key  | オブジェクトキー（Key）は、バケット内のオブジェクトの一意のタグです。たとえば、オブジェクトのアクセスドメイン名`bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`では、オブジェクトキーはdoc1/pic1.jpgです | String | はい | 
 |Expired| 署名の期限切れ時間（秒）| Int| いいえ|
 |Params| 署名時にチェックインする要求パラメータ| Dict| いいえ|
 |Headers| 署名時にチェックインする要求ヘッダー| Dict| いいえ|

#### 戻り結果の説明
このメソッドの戻り値は事前署名のダウンロードURLです。

### ファイルの削除

##### 機能説明
指定されたバケット内の対応するファイルを削除します。

#### 方法のプロトタイプ

```
delete_object(Bucket, Key, **kwargs)
```
####　リクエスト例

```python
response = client.delete_object(
    Bucket='test01-123456789',
    Key='test.txt'
)
```
#### パラメータ説明

| パラメータ名称   | パラメータ説明   |タイプ | 必須項目 | 
| -------------- | -------------- |---------- | ----------- |
 | Bucket  | バケット名は、Bucketname-appidからなります |  String |  はい | 
 | Key  | オブジェクトキー（Key）は、バケット内のオブジェクトの一意のタグです。たとえば、オブジェクトのアクセスドメイン名`bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`では、オブジェクトキーはdoc1/pic1.jpgです | String | はい | 

#### 戻り結果の説明
このメソッドの戻り値はNoneです。

### ファイルの一括削除

##### 機能説明
指定バケットにおけるファイルを一括削除します。

#### 方法のプロトタイプ

```
delete_objects(Bucket, Delete={}, **kwargs)
```
####　リクエスト例

```python
response = client.delete_objects(
    Bucket='test01-123456789',
    Delete={
        'Object': [
            {
                'Key': 'string',
            },
        ],
        'Quiet': 'true'|'false'
    }
)
```
#### パラメータ説明

| パラメータ名称   | パラメータ説明   |タイプ | 必須項目 | 
| -------------- | -------------- |---------- | ----------- |
 | Bucket　　| バケット名は、Bucketname-appidからなります|  String |  はい | 
 | Delete  | 今回削除された戻り結果方式とターゲットオブジェクトを説明します | Dict | はい | 
 | Object  | 削除する各ターゲットオブジェクト情報を説明します | List | はい | 
 | Key     | オブジェクトキー（Key）は、バケット内のオブジェクトの唯一の識別子です。たとえば、オブジェクトのアクセスドメイン名`bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`では、オブジェクトキーはdoc1/pic1.jpgです|　String|いいえ|
 | Quiet   |削除された戻り結果の方式を指定します。オプションの値は'true'、'false'で、デフォルト値は'false'です。'true'に設定する場合、失敗に関するエラーメッセージのみが返されます。'false'に設定する場合、成功および失敗に関するすべての情報が返されます。|String|いいえ|

#### 戻り結果の説明
ファイルの一括削除の結果、タイプはDictです。
```python
{
    'Deleted': [
        {
            'Key': 'string',
        },
    ],
    'Error': [
        {
            'Key': 'string',
            'Code': 'string',
            'Message': 'string'
        },
    ]
}
```

| パラメータ名   | パラメータの説明   |タイプ | 
| -------------- | -------------- |---------- |
 | Deleted  |  正常に削除されたオブジェクトの情報|  List |
 | Key     | 正常に削除されたオブジェクトのパス| String|
 | Error |  正常に削除されなかったオブジェクトの情報| List |
 | Key     | 正常に削除されなかったオブジェクトのパス| String|
 | Code     | 正常に削除されなかったオブジェクトの対応するエラーコード| String|
 | Message   | 正常に削除されなかったオブジェクトの対応するエラーメッセージ| String|


### ファイルプロパティの取得
##### 機能説明
指定ファイルのソース情報の取得。

#### 方法のプロトタイプ

```
head_object(Bucket, Key, **kwargs)
```
####　リクエスト例

```python
response = client.head_object(
    Bucket='test01-123456789',
    Key='test.txt',
    IfModifiedSince='string'
)
```
#### パラメータ説明

| パラメータ名称   | パラメータ説明   |タイプ | 必須項目 | 
| -------------- | -------------- |---------- | ----------- |
  | Bucket   | バケット名は、Bucketname-appidからなります  | String  |  はい | 
  | Key   |  オブジェクトキー（Key）は、バケット内のオブジェクトの唯一の識別子です。たとえば、オブジェクトのアクセスドメイン名`bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`では、オブジェクトキーはdoc1/pic1.jpgです  |String  |　はい |
  | IfModifiedSince   | 指定された時間後に変更された場合に返されます  | String  | いいえ | 

#### 戻り結果の説明

ファイルのメタ情報（タイプはDict）を取得します。

```python
{
    'Content-Type': 'application/octet-stream',
    'Content-Length': '16807',
    'ETag': '"9a4802d5c99dafe1c04da0a8e7e166bf"',
    'Last-Modified': 'Wed, 28 Oct 2014 20:30:00 GMT',
    'x-cos-request-id': 'NTg3NzQ3ZmVfYmRjMzVfMzE5N182NzczMQ=='
}
```

| パラメータ名   | パラメータの説明   |タイプ | 
| -------------- | -------------- |---------- | 
| ファイルのメタ情報 |Etagやx-cos-request-idなどのファイルのメタ情報と設定されたファイルのメタ情報を取得します| String|

### マルチパートアップロードの作成

##### 機能説明

新しいマルチパートアップロードのタスクを作成します。UploadIdが返されます。

#### 方法のプロトタイプ

```
create_multipart_upload(Bucket, Key, **kwargs):
```
####　リクエスト例

```python
response = client.create_multipart_upload(
    Bucket='test01-123456789',
    Key='multipart.txt',
    StorageClass='STANDARD'|'STANDARD_IA',
    Expires='string'
    CacheControl='string',
    ContentType='string',
    ContentDisposition='string',
    ContentEncoding='string',
    ContentLanguage='string',
    Metadata={
        'x-cos-meta-key1': 'value1',
        'x-cos-meta-key2': 'value2'
    },
    ACL='private'|'public-read'|'public-read-write',
    GrantFullControl='string',
    GrantRead='string',
    GrantWrite='string'
)
#　後続のAPIで使用するUploadIdの取得
uploadid = response['UploadId']
```
#### パラメータ説明

| パラメータ名称   | パラメータ説明   |タイプ | 必須項目 | 
| -------------- | -------------- |---------- | ----------- |
 | Bucket　　| バケット名は、Bucketname-appidからなります|  String |  はい |
 | Key  |  オブジェクトキー（Key）は、バケット内のオブジェクトの唯一の識別子です。たとえば、オブジェクトのアクセスドメイン名`bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`では、オブジェクトキーはdoc1/pic1.jpgです | String | はい |
 | StorageClass  | ファイルのストレージタイプの設定：STANDARD、STANDARD_IA。デフォルト値：STANDARD | String |  いいえ | 
 | Expires  |  Content-Expiresの設定 | String| いいえ |
 | CacheControl  | キャッシュポリシー、Cache-Controlの設定 | String |  いいえ | 
 | ContentType  | 内容タイプ、Content-Typeの設定 | String |  いいえ | 
 | ContentDisposition  |  ファイル名、Content-Dispositionの設定 | String |  いいえ | 
 | ContentEncoding  | エンコードフォーマット、Content-Encodingの設定 | String |  いいえ | 
 | ContentLanguage  | 言語タイプ、Content-Languageの設定 |  String |  いいえ |
 | Metadata |ユーザー設定のファイルのメタ情報 | Dict |  いいえ |
 | ACL |‘private’、‘public-read’、‘public-read-write’などファイルのACLを設定します |String| いいえ|
| GrantFullControl |指定したアカウントにファイルへの読み書き権限を付与します。`id =" ",id = " "`というフォーマットになります。サブアカウントへの承認が必要な場合、`id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`になります。ルートアカウントへの承認が必要な場合は`id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`というフォーマットになります。例えば、`'id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"'`などです。|String|いいえ|
|GrantRead |指定したアカウントにバケットへの読み取り権限を付与します。`id=" ",id=" "`というフォーマットになります。サブアカウントへの承認が必要な場合、`id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`になります。ルートアカウントへの承認が必要な場合は`id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`というフォーマットになります。例えば、`'id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"'`などです。|String|いいえ|
| GrantWrite|指定したアカウントにバケットへの書き込み権限を付与します。`id =" ",id=" "`というフォーマットになります。サブアカウントへの承認が必要な場合、`id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`というフォーマットになります。ルートアカウントへの承認が必要な場合は`id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`になります。例えば、`'id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"'`などです。|String|いいえ|

#### 戻り結果の説明

マルチパートアップロードの初期化情報（タイプはDict）を取得します。

```python
{
    'UploadId': '150219101333cecfd6718d0caea1e2738401f93aa531a4be7a2afee0f8828416f3278e5570',
    'Bucket': 'test01-123456789', 
    'Key': 'multipartfile.txt' 
}

```

| パラメータ名   | パラメータの説明   |タイプ | 
| -------------- | -------------- |---------- |
|UploadId | マルチパートアップロードのIDの識別|String|
|Bucket | バケット名は、Bucket-appidからなります|String|
|Key | オブジェクトキー（Key）は、バケット内のオブジェクトの唯一の識別子です。たとえば、オブジェクトのアクセスドメイン名`bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`では、オブジェクトキーはdoc1/pic1.jpg です|String|

### マルチパートアップロードの放棄

##### 機能説明
マルチパートアップロードのタスクを諦め、すべてのアップロード済みのパートを削除します。

#### 方法のプロトタイプ

```
abort_multipart_upload(Bucket, Key, UploadId, **kwargs)
```
####　リクエスト例

```python
response = client.abort_multipart_upload(
    Bucket='test01-123456789',
    Key='multipart.txt',
    UploadId=uploadid
)
```
#### パラメータ説明

| パラメータ名称   | パラメータ説明   |タイプ | 必須項目 | 
| -------------- | -------------- |---------- | ----------- |
|Bucket |バケット名は、Bucketname-appidからなります|String| はい|
|Key |オブジェクトキー（Key）は、バケット内のオブジェクトの唯一の識別子です。たとえば、オブジェクトのアクセスドメイン名`bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`では、オブジェクトキーはdoc1/pic1.jpgです|String| はい|
|UploadId |マルチパートアップロードのIDの識別|String| はい|

#### 戻り結果の説明
このメソッドの戻り値はNoneです。

### パートのアップロード
##### 機能説明
パートを指定のUploadIdにアップロードします。パートごとのサイズは5GB以内でなければなりません。

#### 方法のプロトタイプ

```
upload_part(Bucket, Key, Body, PartNumber, UploadId, **kwargs)
```
####　リクエスト例

```python
# アップロードするマルチパート数は最大10000パートであることに注意してください。
response = client.upload_part(
    Bucket='test01-123456789',
    Key='multipart.txt',
    Body=b'abc'|file,
    PartNumber=1,
    UploadId='string',
    EnableMD5=False|True,
    ContentLength=123,
    ContentMD5='string'
)
```
#### パラメータ説明

| パラメータ名称   | パラメータ説明   |タイプ | 必須項目 | 
| -------------- | -------------- |---------- | ----------- |
 | Bucket  | バケット名は、Bucketname-appidからなります | String |  はい|
 | Key  | オブジェクトキー（Key）は、バケット内のオブジェクトの唯一の識別子です。たとえば、オブジェクトのアクセスドメイン名`bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`では、オブジェクトキーはdoc1/pic1.jpgです | String |  はい|
 | Body  | アップロードするマルチパートの内容はローカルファイルストリームまたは入力ストリームです | file/bytes |  はい|
 | PartNumber  |アップロードするマルチパートの番号の識別 |  Int |  はい|
 | UploadId  | マルチパートアップロードのIDの識別 | String |  はい|
 | EnableMD5 | SDKによるContent-MD5の計算が必要ですか。デフォルトはオフになっています。オンにすると、アップロードに多くの時間がかかります|Bool | いいえ| 
 | ContentLength  |伝送長さの設定 |  Int |  いいえ|
 | ContentMD5  | 検証するためにアップロードされたファイルのMD5値の設定 | String |  いいえ|
 
#### 戻り結果の説明

アップロードするマルチパートのプロパティ、タイプはDictです。

```python
{
    'ETag': 'string'
}
```

| パラメータ名   | パラメータの説明   |タイプ | 
| -------------- | -------------- |---------- | 
| ETag |アップロードするマルチパートのMD5値。|String|

### アップロードするマルチパートのリスト
##### 機能説明
指定UploadIdにおいてアップロード済みのパートの情報をリストします。

#### 方法のプロトタイプ

```
list_parts(Bucket, Key, UploadId, MaxParts=1000, PartNumberMarker=0, EncodingType='', **kwargs)
```
####　リクエスト例

```python
response = client.list_parts(
    Bucket='test01-123456789',
    Key='multipart.txt',
    UploadId=uploadid,
    MaxParts=1000,
    PartNumberMarker=100,
    EncodingType='url'
)
```
#### パラメータ説明

| パラメータ名称   | パラメータ説明   |タイプ | 必須項目 | 
| -------------- | -------------- |---------- | ----------- |
|Bucket |バケット名は、Bucketname-appidからなります|String| はい|
|Key |オブジェクトキー（Key）は、バケット内のオブジェクトの唯一の識別子です。たとえば、オブジェクトのアクセスドメイン名`bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`では、オブジェクトキーはdoc1/pic1.jpgです|String| はい|
|UploadId |マルチパートアップロードのIDの識別|String| はい|
|MaxParts |返されたパートの最大数、デフォルトは最大1000|Int| いいえ|
|PartNumberMarker |デフォルト値は0で、最初のパートからパートを出して、PartNumberMarkerの次のパートからリストされます|Int| いいえ|
| EncodingType |デフォルトはエンコードなし、戻り値のエンコード方法を指定します。オプションの値：url |String|いいえ|

#### 戻り結果の説明

すべてのアップロードするマルチパートの情報、タイプはDictです。

```python
{
    'Bucket': 'test01-123456789', 
    'Key': 'multipartfile.txt', 
    'UploadId': '1502192444bdb382add546a35b2eeab81e06ed84086ca0bb75ea45ca7fa073fa9cf74ec4f2', 
    'EncodingType': None, 
    'MaxParts': '1000',
    'IsTruncated': 'true',
    'PartNumberMarker': '0', 
    'NextPartNumberMarker': '1000', 
    'StorageClass': 'Standard',
    'Part': [
        {
            'LastModified': '2017-08-08T11:40:48.000Z',
            'PartNumber': '1',
            'ETag': '"8b8378787c0925f42ccb829f6cc2fb97"',
            'Size': '10485760'
        },
    ], 
    'Initiator': {
        'DisplayName': '3333333333', 
        'ID': 'qcs::cam::uin/3333333333:uin/3333333333'
    }, 
    'Owner': {
        'DisplayName': '124564654654',
        'ID': '124564654654'
    }
}
```

| パラメータ名   | パラメータの説明   |タイプ | 
| -------------- | -------------- |---------- | 
| Bucket   |  バケット名は、bucketname-appidからなります  | String  |
|  Key  | オブジェクトキー（Key）は、バケット内のオブジェクトの唯一の識別子です。たとえば、オブジェクトのアクセスドメイン名`bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`では、オブジェクトキーはdoc1/pic1.jpgです | String | 
|  UploadId  |  マルチパートアップロードのIDの識別　| String | 
| EncodingType   |   デフォルトはエンコードなし、戻り値のエンコード方法を指定します。オプションの値：url  | String  |
| MaxParts   | 返されたパートの最大数については、デフォルトは最大1000  | String  |
| IsTruncated   |  返されたパートは切り捨てられたかを示します  | String|
| PartNumberMarker   | デフォルト値は0で、最初のパートからパートをリストして、PartNumberMarkerの次のパートからリストされます  | String  |
| NextPartNumberMarker   |  次にリストされるパートの開始位置の指定  | String  |
 | StorageClass |  ファイルのストレージタイプ：STANDARD、STANDARD_IA。デフォルト値：STANDARD | String |
|  Part |ETag、PartNumber、Size、LastModifiedなど、パートに関する情報のアップロード | String |
 |  Initiator  | マルチパートアップロードの作成者はDisplayNameおよびIDを含めています | Dict | 
 |  Owner  | DisplayName、IDなどのファイル所有者の情報 | Dict | 


### マルチパートアップロードの完成

##### 機能説明

指定UploadIdにおけるすべてのパートを完全なるファイルにまとめます。最終的にファイルサイズは1MB以下でなければなりません。さもなければエラーが返されます。

#### 方法のプロトタイプ

```
complete_multipart_upload(Bucket, Key, UploadId, MultipartUpload={}, **kwargs)
```
####　リクエスト例

```python
response = client.complete_multipart_upload(
    Bucket='test01-123456789',
    Key='multipart.txt',
    UploadId=uploadid,
    MultipartUpload={
        'Part': [
            {
                'ETag': 'string',
                'PartNumber': 1
            },
            {
                'ETag': 'string',
                'PartNumber': 2
            },
        ]
    },
)

```
#### パラメータ説明

| パラメータ名称   | パラメータ説明   |タイプ | 必須項目 | 
| -------------- | -------------- |---------- | ----------- |
|  Bucket  | バケット名は、bucketname-appidからなります　| String |   はい| 
|  Key  | オブジェクトキー（Key）は、バケット内のオブジェクトの唯一の識別子です。たとえば、オブジェクトのアクセスドメイン名`bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`では、オブジェクトキーはdoc1/pic1.jpgです | String  |   はい| 
|  UploadId  | マルチパートアップロードのIDの識別 | String  |   はい| 
|  MultipartUpload  |すべてのパートのETagとPartNumber情報 |  Dict |   はい| 

#### 戻り結果の説明

組み立てられたファイルに関する情報、タイプはDict。

```python
{
    'ETag': '"3f866d0050f044750423e0a4104fa8cf-2"', 
    'Bucket': 'test01-123456789', 
    'Location': 'test01-123456789.cn-north.myqcloud.com/multipartfile.txt', 
    'Key': 'multipartfile.txt'
}
```

| パラメータ名   | パラメータの説明   |タイプ | 
| -------------- | -------------- |---------- | 
 |  ETag  | マージされたオブジェクトの一意のラベル値はオブジェクトコンテンツのMD5検証値ではなく、オブジェクトの一意性のチェックにのみ使用できます。ファイルの内容を確認する必要がある場合は、アップロード中に個々のパートのETag値を確認できます。|  String | 
 |  Bucket　　|バケット名は、Bucketname-appidからなります |  String | 
 |  Location  | URLアドレス |  String | 
 |  Key  |  オブジェクトキー（Key）は、バケット内のオブジェクトの唯一の識別子です。たとえば、オブジェクトのアクセスドメイン名`bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`では、オブジェクトキーはdoc1/pic1.jpgです | String |

### Object ACL情報の設定

##### 機能説明

ACL、GrantFullControl、GrantRead、およびGrantWriteによってheaderを渡すことで、あるいは、AccessControlPolicyを使用してボディを渡すことで、ファイルのACL情報を設定します。ただ一つの方法が選択できます。そうでなければ、競合が返されます。
>!現在のアクセスポリシーエントリは1000条に制限されています。オブジェクトACL制御が不要な場合は、設定しないでください。デフォルトはバケット権限が継承されます。

#### 方法のプロトタイプ

```
put_object_acl(Bucket, Key, AccessControlPolicy={}, **kwargs)
```
####　リクエスト例

```python
response = client.put_object_acl(
    Bucket='test01-123456789',
    Key='test.txt',
    ACL='private'|'public-read'|'public-read-write',
    GrantFullControl='string',
    GrantRead='string',
    GrantWrite='string',
    AccessControlPolicy={
        'Grant': [
            {
                'Grantee': {
                    'DisplayName': 'string',
                    'Type': 'CanonicalUser'|'Group',
                    'ID': 'string',
                    'URI': 'string'
                },
                'Permission': 'FULL_CONTROL'|'WRITE'|'READ'
            },
        ],
        'Owner': {
            'DisplayName': 'string',
            'ID': 'string'
        }
    }
)
```
#### パラメータ説明

| パラメータ名称   | パラメータ説明   |タイプ | 必須項目 | 
| -------------- | -------------- |---------- | ----------- |
| Bucket   |  バケット名は、bucketname-appidからなります | String  |  はい  |
| Key   | オブジェクトキー（Key）は、バケット内のオブジェクトの唯一の識別子です。たとえば、オブジェクトのアクセスドメイン名`bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`では、オブジェクトキーはdoc1/pic1.jpgです | String  |  はい  | 
| ACL |‘private’、‘public-read’、‘public-read-write’などファイルのACLを設定します |String| いいえ| 
| GrantFullControl |指定したアカウントにファイルへの読み書き権限を付与します。`id =" ",id = " "`というフォーマットになります。サブアカウントへの承認が必要な場合、`id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`になります。ルートアカウントへの承認が必要な場合は`id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`というフォーマットになります。例えば、`'id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"'`などです。|String|いいえ|
|GrantRead |指定したアカウントにバケットへの読み取り権限を付与します。`id=" ",id=" "`というフォーマットになります。サブアカウントへの承認が必要な場合、`id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`になります。ルートアカウントへの承認が必要な場合は`id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`というフォーマットになります。例えば、`'id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"'`などです。|String|いいえ|
| GrantWrite|指定したアカウントにバケットへの書き込み権限を付与します。`id =" ",id=" "`というフォーマットになります。サブアカウントへの承認が必要な場合、`id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`というフォーマットになります。ルートアカウントへの承認が必要な場合は`id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`になります。例えば、`'id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"'`などです。|String|いいえ|
| AccessControlPolicy   | 指定されたアカウントにファイルへのアクセス権を付与します。具体的なフォーマットはget object aclの返された結果の説明を参照してください。| Dict  | いいえ  | 


#### 戻り結果の説明

このメソッドの戻り値はNoneです。

### Object ACL情報の取得

##### 機能説明
指定ファイルのACLを取得します。

#### 方法のプロトタイプ

```
get_object_acl(Bucket, Key, **kwargs)
```
####　リクエスト例

```python
response = client.get_object_acl(
    Bucket='test01-123456789',
    Key='test.txt'
)
```
#### パラメータ説明

| パラメータ名称   | パラメータ説明   |タイプ | 必須項目 | 
| -------------- | -------------- |---------- | ----------- |
|Bucket| バケット名は、bucketname-appidからなります|String| はい|
|Key |オブジェクトキー（Key）は、バケット内のオブジェクトの唯一の識別子です。たとえば、オブジェクトのアクセスドメイン名`bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`では、オブジェクトキーはdoc1/pic1.jpgです|String|はい|


#### 戻り結果の説明

Bucket ACL情報、タイプはDictです。
```python
{
    'Owner': {
        'DisplayName': 'string',
        'ID': 'string'
    },
    'Grant': [
        {
            'Grantee': {
                'DisplayName': 'string',
                'Type': 'CanonicalUser'|'Group',
                'ID': 'string',
                'URI': 'string'
            },
            'Permission': 'FULL_CONTROL'|'WRITE'|'READ'
        },
    ]
}
```

| パラメータ名   | パラメータの説明   |タイプ |
| -------------- | -------------- |---------- | 
 |  Owner  | DisplayName、IDなどのファイル所有者の情報 | Dict | 
 |  Grant  | Grantee、Permissionなどのファイル権限付与者の情報 | List | 
 |  Grantee  |DisplayName、Type、ID、URIなどのファイル権限付与者の情報 |  Dict | 
 |  DisplayName  |  権限付与者の名前 | String |
 |  Type  |  権限付与者のタイプはCanonicalUserまたはGroupです | String |
 |  ID  | TypeがCanonicalUserの場合、権限付与者のIDに対応します | String | 
 |  URI  |TypeがGroupの場合、権限付与者のURIに対応します |  String | 
 |  Permission  |  権限付与者が所有するファイルの権限。オプションの値はFULL_CONTROL、WRITE、READで、それぞれ読み書き権限、書き込み権限、読み取り権限と対応しています | String |

### ファイルのコピー

##### 機能説明
ファイルをソースパスからターゲットパスにコピーします。コピー中に、ファイルメタ属性とACLを変更できます。コピー操作が必要な場合、オブジェクトが5GBを超え、かつソースオブジェクトとターゲットオブジェクトが同じ地域にないときは、create_multipart_upload() APIを使用してマルチパートアップロードを作成し、upload_part_copy() APIを使用してパートコピーを行い、complete_multipart_upload()を通してマルチパートアップロードを完了する必要があります。コピーするオブジェクトが5GB以下の場合、または同じドメイン内でのコピーである場合は、copy_object()を直接に呼び出すようにすればよいです。

#### 方法のプロトタイプ

```
copy_object(Bucket, Key, CopySource, CopyStatus='Copy', **kwargs)
```
####　リクエスト例

```python
response = client.copy_object(
    Bucket='test01-123456789',
    Key='test.txt',
    CopySource={
        'Appid': '1252408340',
        'Bucket': 'test02', 
        'Key': 'test.txt', 
        'Region': 'ap-guangzhou'
    },
    CopyStatus='Copy'|'Replaced',
    ACL='private'|'public-read'|'public-read-write',
    GrantFullControl='string',
    GrantRead='string',
    GrantWrite='string',
    StorageClass='STANDARD'|'STANDARD_IA',
    Expires='string'
    CacheControl='string',
    ContentType='string',
    ContentDisposition='string',
    ContentEncoding='string',
    ContentLanguage='string',
    Metadata={
        'x-cos-meta-key1': 'value1',
        'x-cos-meta-key2': 'value2'
    }
)
```
#### パラメータ説明

| パラメータ名称   | パラメータ説明   |タイプ | 必須項目 | 
| -------------- | -------------- |---------- | ----------- |
 |  Bucket  |  バケット名は、Bucketname-appidからなります  | String|  はい |
 |  Key  | オブジェクトキー（Key）は、バケット内のオブジェクトの唯一の識別子です。たとえば、オブジェクトのアクセスドメイン名`bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`では、オブジェクトキーはdoc1/pic1.jpgです | String| はい | 
 |  CopySource  | Appid、Bucket、Key、Regionなどを含むソースファイルをコピーするためのパスを説明します |  Dict | はい |
 |  CopyStatus  |  オプションの値が'Copy'、'Replaced'です。'Copy'に設定する場合は、設定されているユーザーメタデータ情報を無視して直接コピーし、'Replaced'に設定する場合は、設定されているメタデータを変更します。ターゲットパスがソースパスと同じである場合は、'Replaced'に設定する必要があります | String| はい |
| ACL |‘private’、‘public-read’、‘public-read-write’などファイルのACLを設定します |String| いいえ|
| GrantFullControl |指定したアカウントにファイルへの読み書き権限を付与します。id =" ",id = " "というフォーマットになります。サブアカウントへの承認が必要な場合、`id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`になります。ルートアカウントへの承認が必要な場合は`id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`というフォーマットになります。例えば、`'id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"'`などです。|String|いいえ|
|GrantRead |指定したアカウントにバケットへの読み取り権限を付与します。`id=" ",id=" "`というフォーマットになります。サブアカウントへの承認が必要な場合、`id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`になります。ルートアカウントへの承認が必要な場合は`id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`というフォーマットになります。例えば、`'id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"'`などです。|String|いいえ|
| GrantWrite|指定したアカウントにバケットへの書き込み権限を付与します。`id =" ",id=" "`というフォーマットになります。サブアカウントへの承認が必要な場合、`id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`というフォーマットになります。ルートアカウントへの承認が必要な場合は`id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`になります。例えば、`'id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"'`などです。|String|いいえ|
 |  StorageClass  |  ファイルのストレージタイプ（STANDARD、STANDARD_IA）の設定。デフォルト値：STANDARD | String|  いいえ |
 |  Expires  | Content-Expiresの設定 | String| いいえ | 
 |  CacheControl  | キャッシュポリシー、Cache-Controlの設定 | String |  いいえ | 
 |  ContentType  | 内容タイプ、Content-Typeの設定 | String|  いいえ | 
 |  ContentDisposition  |  ファイル名、Content-Dispositionの設定 | String|  いいえ |
 |  ContentEncoding  | エンコードフォーマット、Content-Encodingの設定 | String|  いいえ | 
 |  ContentLanguage  |  言語タイプ、Content-Languageの設定 | String|  いいえ |
 |  Metadata |ユーザー設定のファイルのメタ情報 | Dict |  いいえ | 


#### 戻り結果の説明
アップロードするファイルのプロパティ、タイプはDictです。

```python
{
    'ETag': 'string',
    'LastModified': 'string',
}
```

| パラメータ名   | パラメータの説明   |タイプ | 
| -------------- | -------------- |---------- | 
| ETag |ファイルのMD5値のコピー|String|
| LastModified |ファイルの最終変更日のコピー|String|

### パートコピー

##### 機能説明
あるファイルのパートコンテンツをソースパスからターゲットパスへコピーします。

#### 方法のプロトタイプ

```
upload_part_copy(Bucket, Key, PartNumber, UploadId, CopySource, CopySourceRange='', **kwargs)
```
####　リクエスト例

```python
response = client.upload_part_copy(
    Bucket='test01-123456789',
    Key='test.txt',
    PartNumber=100,
    UploadId='string',
    CopySource={
        'Appid': '1252408340',
        'Bucket': 'test02', 
        'Key': 'test.txt', 
        'Region': 'ap-guangzhou'
    },
    CopySourceRange='string',
    CopySourceIfMatch='string',
    CopySourceIfModifiedSince='string',
    CopySourceIfNoneMatch='string',
    CopySourceIfUnmodifiedSince='string'
```
#### パラメータ説明

| パラメータ名称   | パラメータ説明   |タイプ | 必須項目 | 
| -------------- | -------------- |---------- | ----------- |
|  Bucket  |  バケット名は、Bucketname-appidからなります  | String|  はい |
|  Key  | オブジェクトキー（Key）は、バケット内のオブジェクトの唯一の識別子です。たとえば、オブジェクトのアクセスドメイン名`bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`では、オブジェクトキーはdoc1/pic1.jpgです | String| はい |
| PartNumber  |アップロードするマルチパートの番号の識別 |  Int |  はい|
| UploadId  | マルチパートアップロードのIDの識別 | String |  はい|
|  CopySource  | Appid、Bucket、Key、Regionなどを含むソースファイルをコピーするためのパスを説明します |  Dict | はい |
|CopySourceRange| ソースファイルのコピー範囲をbytes=first-lastフォーマットで説明します。指定しない場合、ソースファイル全体がデフォルトでコピーされます|String|いいえ|
|CopySourceIfMatch| ソースファイルのEtagが指定された値と同じときのみにコピーされます|String|いいえ|
|CopySourceIfModifiedSince| ソースファイルは指定された時刻以降に変更されてからコピーされます|String|いいえ|
|CopySourceIfNoneMatch| ソースファイルのEtagが指定された値と一致しないときのみにコピーされます|String|いいえ|
|CopySourceIfUnmodifiedSince| ソースファイルは指定された時刻以降に変更されないときのみコピーされます|String|いいえ|

#### 戻り結果の説明

パートのプロパティをコピーし、タイプはDictです。

```python
{
    'ETag': 'string',
    'LastModified': 'string',
}
```

| パラメータ名   | パラメータの説明   |タイプ | 
| -------------- | -------------- |---------- | 
| ETag |パートのMD5値をコピー|String|
| LastModified |パートの最終変更日をコピーします|String|

### アーカイブファイルの回復

##### 機能説明
COSによってarchiveタイプにアーカイブされたオブジェクトをリカバリします。

#### 方法のプロトタイプ

```
restore_object(Bucket, Key, RestoreRequest={}, **kwargs)
```
####　リクエスト例

```python
response = client.restore_object(
    Bucket='test01-123456789',
    Key='test.txt',
    RestoreRequest={
        'Days': 100,
        'CASJobParameters': {
            'Tier': 'Expedited'|'Standard'|'Bulk'
        }

    }
)
```
#### パラメータ説明

| パラメータ名称   | パラメータ説明   |タイプ | 必須項目 | 
| -------------- | -------------- |---------- | ----------- |
|Bucket| バケット名は、bucketname-appidからなります|String| はい|
|Key |オブジェクトキー（Key）は、バケット内のオブジェクトの唯一の識別子です。たとえば、オブジェクトのアクセスドメイン名`bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`では、オブジェクトキーはdoc1/pic1.jpgです|String|はい|
|RestoreRequest| 取得された一時ファイルの規則の説明| Dict|はい|
|Days|一時ファイルの期限切れ時間の説明| Int|はい|
|CASJobParameters| 回復型構成情報の説明| Dict|いいえ|
|Tier| 一時ファイルを取得するモードを説明します。オプションの値は'Expedited'、'Standard'、'Bulk'で、それぞれ高速、標準、低速の3つのモードに対応します| String|いいえ|

#### 戻り結果の説明
このメソッドの戻り値はNoneです。

## High-level APIの説明（推奨）

### ファイルのアップロード（断続的なアップロード）

##### 機能説明
ファイルアップロードAPIはユーザファイルの長さに基づいて、自動的にシンプルなアップロード及びマルチパートアップロードを選択し、20M以下のファイルに対してシンプルなアップロードを呼び出し、20MB以上のファイルに対してマルチパートアップロードを呼び出し、マルチパートアップロードの未完成ファイルに対して自動的に断続的なアップロードを行います。

#### 方法のプロトタイプ

```
upload_file(Bucket, Key, LocalFilePath, PartSize=1, MAXThread=5, **kwargs)
```
####　リクエスト例

```python
response = client.upload_file(
    Bucket='test01-123456789',
    Key='test.txt',
    LocalFilePath='local.txt',
    EnableMD5=False
)
```

#### すべてのパラメータのリクエスト例
```python
response = client.upload_file(
    Bucket='test01-123456789',
    Key='test.txt',
    LocalFilePath='local.txt',
    PartSize=1,
    MAXThread=5,
    EnableMD5=False|True,
    ACL='private'|'public-read'|'public-read-write', # このパラメータは慎重に使用してください。そうしないと、1000条ACL上限値に達します。
    GrantFullControl='string',
    GrantRead='string',
    GrantWrite='string',
    StorageClass='STANDARD'|'STANDARD_IA',
    Expires='string',
    CacheControl='string',
    ContentType='string',
    ContentDisposition='string',
    ContentEncoding='string',
    ContentLanguage='string',
    ContentLength='123',
    ContentMD5='string',
    Metadata={
        'x-cos-meta-key1': 'value1',
        'x-cos-meta-key2': 'value2'
    }
)
```
#### パラメータ説明


| パラメータ名称   | パラメータ説明   |タイプ | 必須項目 | 
| -------------- | -------------- |---------- | ----------- |
 |  Bucket  |  バケット名は、Bucketname-appidからなります | String |   はい |
 |  Key  | オブジェクトキー（Key）は、バケット内のオブジェクトの唯一の識別子です。たとえば、オブジェクトのアクセスドメイン名`bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`では、オブジェクトキーはdoc1/pic1.jpgです | String |  はい | 
|  LocalFilePath  | ローカルファイルのパス名 |  String |  はい |
|  PartSize  | マルチパートアップロードのパートサイズ、デフォルトは1MBです |  Int |  いいえ |
|  MAXThread  | マルチパートアップロードの同時実行数。デフォルトは5スレッドでマルチパートのアップロード |  Int |  いいえ |
| EnableMD5 | SDKによるContent-MD5の計算が必要ですか。デフォルトはオフになっています。オンにすると、アップロードに多くの時間がかかります|Bool | いいえ| 
| ACL |‘private’、‘public-read’、‘public-read-write’などファイルのACLを設定します |String| いいえ|
| GrantFullControl |指定したアカウントにファイルへの読み書き権限を付与します。`id =" ",id = " "`というフォーマットになります。サブアカウントへの承認が必要な場合、`id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`になります。ルートアカウントへの承認が必要な場合は`id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`というフォーマットになります。例えば、`'id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"'`などです。|String|いいえ|
|GrantRead |指定したアカウントにバケットへの読み取り権限を付与します。`id=" ",id=" "`というフォーマットになります。サブアカウントへの承認が必要な場合、`id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`になります。ルートアカウントへの承認が必要な場合は`id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`というフォーマットになります。例えば、`'id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"'`などです。|String|いいえ|
| GrantWrite|指定したアカウントにバケットへの書き込み権限を付与します。`id =" ",id=" "`というフォーマットになります。サブアカウントへの承認が必要な場合、`id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`というフォーマットになります。ルートアカウントへの承認が必要な場合は`id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`になります。例えば、`'id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"'`などです。|String|いいえ|
 |  StorageClass  |  ファイルのストレージタイプ（STANDARD、STANDARD_IA）の設定。デフォルト値：STANDARD | String |   いいえ |
 |  Expires  | Content-Expiresの設定 | String|  いいえ | 
 |  CacheControl  |  キャッシュポリシー、Cache-Controlの設定 | String |   いいえ |
 |  ContentType  | 内容タイプ、Content-Typeの設定 |String |   いいえ |  
 |  ContentDisposition  |  ファイル名、Content-Dispositionの設定 | String |   いいえ |
 |  ContentEncoding  |  エンコードフォーマット、Content-Encodingの設定 | String |   いいえ |
 |  ContentLanguage  |  言語タイプ、Content-Languageの設定 | String |   いいえ |
 |  ContentLength  | 伝送長さの設定 | String |   いいえ | 
 |  ContentMD5  | 検証するためにアップロードされたファイルのMD5値の設定 | String |   いいえ | 
 |  Metadata | ユーザー設定のファイルのメタ情報 | Dict |   いいえ |

#### 戻り結果の説明
アップロードするファイルのプロパティ、タイプはDictです。

```python
{
    'ETag': 'string',
    'x-cos-expiration': 'string'
}
```

| パラメータ名   | パラメータの説明   |タイプ | 
| -------------- | -------------- |---------- |
|  ETag   |  アップロードファイルのMD5値  | String  |
|  x-cos-expiration   | ライフサイクルを設定した後、ファイルの期限切れ時間を返します  | String  | 

## 署名を取得するAPI説明

### 署名の取得

##### 機能説明
指定された操作の署名を取得し、通常、移動先の署名配布に使用されます。

#### 方法のプロトタイプ

```
get_auth(Method, Bucket, Key, Expired=300, Headers={}, Params={})
```
####　リクエスト例

```python
response = client.get_auth(
    Method='PUT'|'POST'|'GET'|'DELETE'|'HEAD',
    Bucket='test01-123456789',
    Key='test.txt',
    Expired=300,
    Headers={
        'Content-Length': 'string',
        'Content-MD5': 'string'
    },
    Params={
        'param1': 'string',
        'param2': 'string'
    }
)
```
#### パラメータ説明

| パラメータ名称   | パラメータ説明   |タイプ | 必須項目 | 
| -------------- | -------------- |---------- | ----------- |
 | Method  |対応する操作のmethod。オプションの値は‘PUT’、‘POST’、‘GET’、‘DELETE’、‘HEAD’です|  String |  はい | 
 | Bucket  | バケット名は、Bucketname-appidからなります |  String |  はい | 
 | Key  | バケット操作でルートパス/の入力、オブジェクト操作でファイルパスの入力| String | はい| 
 |Expired| 署名の期限切れ時間（秒）| Int| いいえ|
 |Headers| 署名のリクエストヘッダーをチェックインする必要があります| Dict| いいえ|
 |Params| 署名のリクエストパラメータをチェックインする必要があります| Dict| いいえ|

#### 戻り結果の説明
このメソッドの戻り値は、対応する操作の署名値を返します。

### 事前署名リンクの取得

##### 機能説明
配布用の事前署名リンクを取得します。

#### 方法のプロトタイプ

```
get_presigned_url(Bucket, Key, Method, Expired=300, Params={}, Headers={})
```
####　リクエスト例

```python
response = client.get_presigned_url(
    Bucket='test01-123456789',
    Key='test.txt',
    Method='PUT'|'POST'|'GET'|'DELETE'|'HEAD'
)
```
#### パラメータ説明

| パラメータ名称   | パラメータ説明   |タイプ | 必須項目 | 
| -------------- | -------------- |---------- | ----------- |
 | Bucket  | バケット名は、Bucketname-appidからなります |  String |  はい | 
 | Key  | オブジェクトキー（Key）は、バケット内のオブジェクトの一意のタグです。たとえば、オブジェクトのアクセスドメイン名`bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg`では、オブジェクトキーはdoc1/pic1.jpgです | String | はい | 
 | Method  |対応する操作のmethod。オプションの値は‘PUT’、‘POST’、‘GET’、‘DELETE’、‘HEAD’です|  String |  はい | 
 |Expired| 署名の期限切れ時間（秒）| Int| いいえ|
 |Params| 署名時にチェックインする要求パラメータ| Dict| いいえ|
 |Headers| 署名時にチェックインする要求ヘッダー| Dict| いいえ|
 
 
#### 戻り結果の説明
このメソッドの戻り値は事前署名のURLです。

## 異常タイプ説明
CosClientErrorとCosServiceErrorはそれぞれSDKクライアントエラーとCOSサーバーエラーに対応します。

### CosClientError
CosClientErrorは通常timeoutなどによるクライアントエラーを指します。ユーザーは取得した後、再試行またはその他の操作が選択できます。

### CosServiceError
CosServiceErrorは、サーバーから返される具体的な情報を提供し、エラーコードの詳細については、[COSエラーコード](https://cloud.tencent.com/document/product/436/7730)を参照してください。

```python
#except CosServiceError as e
e.get_origin_msg() # XMLフォーマットの元のエラーメッセージの取得
e.get_digest_msg()  # Dictフォーマットの処理済みのエラー情報の取得
e.get_status_code() # HTTPエラーコードの取得（4XX、5XXなど）
e.get_error_code()  # COSで定義されたエラーコードの取得
e.get_error_msg()  # COSエラーコードの具体的な説明の取得
e.get_trace_id()   # 要求のtrace_idの取得
e.get_request_id()  # 要求のrequest_idの取得
e.get_resource_location() # URLアドレスの取得
```

