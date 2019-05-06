COS XML API Python SDK 조작 성공 시 dict 또는 None이 반환되며 실패 시 이상(CosClientError 및 CosServiceError)을 throw합니다. 이상 클래스는 관련 오류 정보를 제공하며 자세한 내용은 본 문서 마지막의 이상 클래스 소개를 참조하십시오.
>?문서에서 나오는 SecretId, SecretKey, Bucket 같은 명칭의 함의 및 획득 방법은 [COS 용어집](https://cloud.tencent.com/document/product/436/7751)을 참조하십시오.

## Bucket API 설명
### 버킷 생성

#### 기능 설명

지정 계정 하에 하나의 새로운 버킷을 생성합니다. 버킷이 이미 있을 경우 오류를 반환합니다.

#### 방식 프로토타입

```
create_bucket(Bucket, **kwargs)
```
#### 요청 예시

```python
response = client.create_bucket(
    Bucket='test01-123456789',
    ACL='private'|'public-read'|'public-read-write',
    GrantFullControl='string',
    GrantRead='string',
    GrantWrite='string'
)
```
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   | 유형 | 필수 입력 |
| -------------- | -------------- |---------- | ----------- |
| Bucket | 생성 대기 중인 버킷 이름이며 bucketname-appid로 구성됩니다 | String | 예 |
| ACL | 버킷의 ACL 설정, 예: 'private', 'public-read', 'public-read-write' | String | 아니요 |
| GrantFullControl | 지정 계정의 버킷에 대한 읽기/쓰기 권한을 부여합니다. 형식은 `id=" ",id=" "` 서브 계정에 권한을 부여해야 할 경우 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}" `루트 계정에 권한을 부여해야 할 경우 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"` 예: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | String | 아니요 |
| GrantRead | 지정 계정에 버킷의 읽기 권한을 부여합니다. 형식은 `id=" ",id=" "` 서브 계정에 권한을 부여해야 할 경우 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"` 루트 계정에 권한을 부여해야 할 경우 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"` 예: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | String | 아니요 |
| GrantWrite | 지정 계정에 버킷의 쓰기 권한을 부여합니다. 형식은 `id=" ",id=" "` 서브 계정에 권한을 부여해야 할 경우 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"` 루트 계정에 권한을 부여해야 할 경우 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"` 예: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | String | 아니요 |

#### 반환 결과 설명
해당 방법의 반환값은 None입니다.

### 버킷 삭제

#### 기능 설명

지정 계정에서 이미 존재하는 버킷을 삭제하고, 삭제 시 버킷은 비어있어야 합니다.

#### 방식 프로토타입

```
delete_bucket(Bucket)
```
#### 요청 예시

```python
response = client.delete_bucket(
    Bucket='test01-123456789'
)
```
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   | 유형 | 필수 입력 |
| -------------- | -------------- |---------- | ----------- |
| Bucket | 삭제 대기 중인 버킷 이름, bucketname-appid로 구성 | String | 예 |

#### 반환 결과 설명
해당 방법의 반환값은 None입니다.

### 버킷 존재 여부 조회

#### 기능 설명

버킷이 존재하는지 또는 액세스 권한이 있는지를 조회합니다.

#### 방식 프로토타입

```
head_bucket(Bucket)
```
#### 요청 예시

```python
response = client.head_bucket(
    Bucket='test01-123456789'
)
```
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   | 유형 | 필수 입력 |
| -------------- | -------------- |---------- | ----------- |
| Bucket | 조회 대기 중인 버킷 이름, bucketname-appid로 구성 | String | 예 |

#### 반환 결과 설명
해당 방법의 반환값은 None입니다.

### 버킷 지역 정보 획득

#### 기능 설명

버킷이 위치한 지역의 정보를 조회합니다.

#### 방식 프로토타입

```
get_bucket_location(Bucket)
```
#### 요청 예시

```python
response = client.get_bucket_location(
    Bucket='test01-123456789'
)
```
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   | 유형 | 필수 입력 |
| -------------- | -------------- |---------- | ----------- |
| Bucket | 조회 대기 중인 버킷 이름, bucketname-appid로 구성 | String | 예 |

#### 반환 결과 설명

버킷 지역 정보이며 유형은 dict입니다.
```python
{
    'LocationConstraint': 'ap-beijing-1'|'ap-beijing'|'ap-shanghai'|'ap-guangzhou'|'ap-chengdu'|'ap-chongqing'|'ap-singapore'|'ap-hongkong'|'na-toronto'|'eu-frankfurt'|'ap-mumbai'|'ap-seoul'|'na-siliconvalley'|'na-ashburn'
}
```

| 매개변수 이름   | 매개변수 설명   | 유형 |
| -------------- | -------------- |---------- |
| LocationConstraint | 버킷 소재 지역의 정보 | String |

### 버킷의 모든 파일 나열

#### 기능 설명

지정 버킷의 모든 객체를 획득합니다.

#### 방식 프로토타입

```
list_objects(Bucket, Delimiter="", Marker="", MaxKeys=1000, Prefix="", EncodingType="", **kwargs)
```
#### 요청 예시

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
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   | 유형 | 필수 입력 |
| -------------- | -------------- |---------- | ----------- |
| Bucket   |  버킷이름, bucketname-appid로 구성  | String  | 예 |
| Prefix   |  기본값은 비어 있으며 object의 key에 대해 필터링을 진행하여 접두사가 Prefix인 objects를 매칭합니다  | String  |  아니요 |
| Delimiter   |   기본값은 비어 있으며 구분 기호를 설정하여, 예를 들어 / 설정으로 폴더를 시뮬레이트합니다  | String |  아니요 |
| Marker   |  기본으로 UTF-8 이진 순서로 항목을 나열하고 objects를 반환하는 list의 시작 위치를 표시합니다  | String  |  아니요 |
| MaxKeys   | 반환되는 objects 최대 수량, 기본값은 1000  | Int  |  아니요 |
| EncodingType   |   기본으로 인코딩하지 않음, 반환값의 인코딩 방식을 규정합니다. 선택 가능 값: url  | String  | 아니요 |

#### 반환 결과 설명

Objects의 메타 정보를 획득하며 유형은 dict입니다:

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

| 매개변수 이름   | 매개변수 설명   | 유형 |
| -------------- | -------------- |---------- |
| MaxKeys   | 반환되는 objects 최대 수량, 기본값은 1000  | String |
| Prefix   |  기본값은 비어 있으며 object의 key에 대해 필터링을 진행하여 접두사가 Prefix인 objects를 매칭합니다  | String |
| Delimiter   |   기본값은 비어 있으며 구분 기호를 설정하여, 예를 들어 / 설정으로 폴더를 시뮬레이트합니다  | String |
| Marker   |  기본으로 UTF-8 이진 순서로 항목을 나열하고 objects를 반환하는 list의 시작 위치를 표시합니다  | String  |
| NextMarker |  IsTruncated가 true일 경우 다음에 objects를 반환하는 list의 시작 위치를 표시합니다  | String  |
| Name   |  버킷 이름, bucketname-appid로 구성  | String  |
| IsTruncated   |  반환된 objects가 잘렸는지 표시합니다  | String |
| EncodingType   | 기본으로 인코딩하지 않음, 반환값의 인코딩 방식을 규정합니다. 선택 가능 값: url  | String  | 아니요|
| Contents | 모든 objects의 메타 정보를 포함한 list, ETag, StorageClass, Key, Owner, LastModified, Size 등의 정보가 포함됩니다 | List |
| CommonPrefixes | Prefix로 시작하고 Delimiter로 끝나는 모든 Key는 같은 클래스로 분류됩니다 | List |

### 버킷의 모든 멀티파트 업로드 나열

#### 기능 설명

지정된 버킷에서 진행되는 모든 멀티파트 업로드를 획득합니다.

#### 방식 프로토타입

```
list_multipart_uploads(Bucket, Prefix="", Delimiter="", KeyMarker="", UploadIdMarker="", MaxUploads=1000, EncodingType="", **kwargs)
```
#### 요청 예시

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
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   | 유형 | 필수 입력 |
| -------------- | -------------- |---------- | ----------- |
| Bucket   |  버킷이름, bucketname-appid로 구성  | String  | 예 |
| Prefix   |  기본값은 비어 있으며 멀티파트 업로드의 key에 대해 필터링을 진행하여 접두사가 Prefix인 멀티파트 업로드를 매칭합니다  | String  |  아니요 |
| Delimiter   |   기본값은 비어 있으며 구분 기호를 설정합니다 | String |  아니요 |
| KeyMarker   |  UploadIdMarker와 함께 사용하며 멀티파트 업로드의 시작 위치를 나타냅니다  | String  |  아니요 |
| UploadIdMarker   |  KeyMarker와 함께 사용하며 멀티파트 업로드의 시작 위치를 나타냅니다. KeyMarker를 지정하지 않으면 UploadIdMarker는 무시됩니다| String  |  아니요 |
| MaxUploads   | 멀티파트 업로드의 최대 반환 수량, 기본값은 1000  | Int  |  아니요|
| EncodingType   |   기본으로 인코딩하지 않음, 반환값의 인코딩 방식을 규정합니다. 선택 가능 값: url  | String  | 아니요 |

#### 반환 결과 설명

멀티파트 업로드의 정보를 획득하며 유형은 dict입니다.

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

| 매개변수 이름   | 매개변수 설명   | 유형 |
| -------------- | -------------- |---------- |
| Bucket   |  버킷 이름, bucketname-appid로 구성  | String  |
| Prefix   |  기본값은 비어 있으며 멀티파트 업로드의 key에 대해 필터링을 진행하여 접두사가 prefix인 멀티파트 업로드를 매칭합니다  | String  |
| Delimiter   |   기본값은 비어 있으며 구분 기호를 설정합니다 | String |
| KeyMarker   |  UploadIdMarker와 함께 사용하며 멀티파트 업로드의 key 시작 위치를 나타냅니다  | String  |
| UploadIdMarker   |  KeyMarker와 함께 사용하며 멀티파트 업로드의 uploadid 시작 위치를 나타냅니다. KeyMarker를 지정하지 않으면 UploadIdMarker는 무시됩니다| String  |
| NextKeyMarker   | IsTruncated가 true일 경우, 다음 멀티파트 업로드의 키 시작 위치를 표시합니다 | String   |
| NextUploadIdMarker | IsTruncated가 true일 경우, 다음 멀티파트 업로드의 uploadid 시작 위치를 표시합니다 | tring   |
| MaxUploads   | 멀티파트 업로드의 최대 반환 수량, 기본값은 1000 | Int    |
| IsTruncated   |  반환된 멀티파트 업로드가 잘렸는지 표시합니다  | String|
| EncodingType   | 기본으로 인코딩하지 않음, 반환값의 인코딩 방식을 지정합니다. 선택 가능값: url  | String |
|Upload | 모든 멀티파트 업로드를 포함한 list, 'UploadId', 'StorageClass', 'Key', 'Owner', 'Initiator', 'Initiated 등의 정보가 포함됩니다|List|
| CommonPrefixes | Prefix로 시작하고 Delimiter로 끝나는 모든 Key는 같은 클래스로 분류됩니다 | List |

### Bucket ACL 정보 설정

#### 기능 설명

버킷의 ACL 정보를 설정하고 ACL, GrantFullControl, GrantRead, GrantWrite를 통해 헤더를 가져오는 방식으로 ACL을 설정하거나 AccessControlPolicy를 통해 본문을 가져오며 ACL을 설정할 수 있습니다. 두 방식 중 하나만 선택해야 하며 그렇지 않으면 충돌이 반환됩니다.

#### 방식 프로토타입

```
put_bucket_acl(Bucket, AccessControlPolicy={}, **kwargs)
```
#### 요청 예시

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
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   | 유형 | 필수 입력 |
| -------------- | -------------- |---------- | ----------- |
| Bucket | 버킷 이름, bucketname-appid로 구성|String|예|
| ACL | 버킷의 ACL 설정, 예: 'private', 'public-read', 'public-read-write' | String | 아니요 |
| GrantFullControl | 지정 계정의 버킷에 대한 읽기/쓰기 권한을 부여합니다. 형식은 `id=" ",id=" "` 서브 계정에 권한을 부여해야 할 경우 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}" `루트 계정에 권한을 부여해야 할 경우 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"` 예: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | String | 아니요 |
| GrantRead | 지정 계정에 버킷의 읽기 권한을 부여합니다. 형식은 `id=" ",id=" "` 서브 계정에 권한을 부여해야 할 경우 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"` 루트 계정에 권한을 부여해야 할 경우 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"` 예: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | String | 아니요 |
| GrantWrite | 지정 계정에 버킷의 쓰기 권한을 부여합니다. 형식은 `id=" ",id=" "` 서브 계정에 권한을 부여해야 할 경우 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"` 루트 계정에 권한을 부여해야 할 경우 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"` 예: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | String | 아니요 |
| AccessControlPolicy| 지정 계정에 버킷에 대한 액세스 권한을 부여하며 구체적인 형식은 get bucket acl 반환 결과 설명을 참조하십시오|Dict|아니요 |

#### 반환 결과 설명
해당 방법의 반환값은 None입니다.

### Bucket ACL 정보 획득

#### 기능 설명

지정 버킷의 ACL 정보를 획득합니다.

#### 방식 프로토타입

```
get_bucket_acl(Bucket, **kwargs)
```
#### 요청 예시

```python
response = client.get_bucket_acl(
    Bucket='test01-123456789',
)
```
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   | 유형 | 필수 입력 |
| -------------- | -------------- |---------- | ----------- |
|Bucket |버킷 이름, bucketname-appid로 구성|String|예|


#### 반환 결과 설명

Bucket ACL 정보이며 유형은 dict입니다.
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

| 매개변수 이름   | 매개변수 설명   | 유형 |
| -------------- | -------------- |---------- |
| Owner |버킷 소유자의 정보, DisplayName 및 ID가 포함됩니다|Dict|
| Grant |버킷 권한 부여자의 정보, Grantee 및 Permission이 포함됩니다|List|
| Grantee |권한 부여자의 정보, DisplayName, Type, ID 및 URI가 포함됩니다|Dict|
| DisplayName |권한 부여자의 이름|String|
| Type |권한 부여자의 유형, CanonicalUser 또는 Group입니다|String|
| ID |Type이 CanonicalUser일 경우 해당 권한 부여자의 ID|String|
| URI |Type이 Group일 때 해당 권한 부여자의 URI|String|
| Permission |부여자가 소유한 버킷의 권한, 선택 가능 값은 FULL_CONTROL, WRITE, READ이며 각각 읽기/쓰기 권한, 쓰기 권한, 읽기 권한에 해당합니다|String|

### 버킷 CORS 구성 설정

#### 기능 설명
지정 버킷의 CORS 구성을 설정합니다.

#### 방식 프로토타입

```
put_bucket_cors(Bucket, CORSConfiguration={}, **kwargs)
```
#### 요청 예시

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
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   | 유형 | 필수 입력 |
| -------------- | -------------- |---------- | ----------- |
| Bucket |버킷 이름, bucketname-appid로 구성|String| 예|
| CORSRule |해당하는 CORS 규칙을 설정하며 ID, MaxAgeSeconds, AllowedOrigin, AllowedMethod, AllowedHeader, ExposeHeader 등이 포함됩니다|List| 예|
| ID |규칙 ID 설정|String|아니요|
| MaxAgeSeconds |OPTIONS 요청이 얻은 결과의 유효기간 설정|Int|아니요|
| AllowedOrigin |허용된 액세스 소스를 설정합니다. 예: `"http://cloud.tencent.com"`, 와일드카드 * 를 지원합니다|Dict|예|
| AllowedMethod |허용된 방법 설정, 예: GET, PUT, HEAD, POST, DELETE|Dict|예|
| AllowedHeader | 요청이 어떠한 사용자 지정 HTTP 요청 헤더를 사용할 수 있도록 설정하며 와일드카드 * 를 지원합니다|Dict|아니요|
| ExposeHeader |브라우저가 수신할 수 있는 서버의 사용자 지정 헤더 정보 설정 |Dict|아니요|

#### 반환 결과 설명
해당 방법의 반환값은 None입니다.

### 버킷의 CORS 구성 획득

#### 기능 설명
지정 버킷의 CORS 구성을 획득합니다.

#### 방식 프로토타입

```
get_bucket_cors(Bucket, **kwargs)
```
#### 요청 예시

```python
response = client.get_bucket_cors(
    Bucket='test01-123456789',
)
```
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   | 유형 | 필수 입력 |
| -------------- | -------------- |---------- | ----------- |
|Bucket|버킷 이름, bucketname-appid로 구성|String| 예|

#### 반환 결과 설명

버킷의 CORS 구성이며 유형은 dict입니다.
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

| 매개변수 이름   | 매개변수 설명   | 유형 |
| -------------- | -------------- |---------- |
 | CORSRule  | CORS 규칙, ID, MaxAgeSeconds, AllowedOrigin, AllowedMethod, AllowedHeader, ExposeHeader 등이 포함됩니다 |  List |
 | ID  | 규칙의 ID| String |
 | MaxAgeSeconds  |  OPTIONS 요청이 얻은 결과의 유효기간 | String |
 | AllowedOrigin  | 허용된 액세스 소스, 예: `"http://cloud.tencent.com"`, 와일드카드 * 를 지원합니다 | Dict |
 | AllowedMethod  |  허용된 방법, 예: GET, PUT, HEAD, POST, DELETE | Dict |
 | AllowedHeader  |요청이 어떠한 사용자 지정 HTTP 요청 헤더도 사용할 수 있도록 설정하며 와일드카드 * 를 지원합니다|  Dict |
 | ExposeHeader  | 브라우저가 수신할 수 있는 서버의 사용자 지정 헤더 정보 | Dict |

### 버킷의 CORS 구성 삭제

#### 기능 설명
지정 버킷의 CORS 구성을 삭제합니다.

#### 방식 프로토타입

```
delete_bucket_cors(Bucket, **kwargs)
```
#### 요청 예시

```python
response = client.delete_bucket_cors(
    Bucket='test01-123456789',
)
```
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   | 유형 | 필수 입력 |
| -------------- | -------------- |---------- | ----------- |
|Bucket |버킷 이름, bucketname-appid로 구성|String| 예 |

#### 반환 결과 설명

해당 방법의 반환값은 None입니다.

### 버킷 수명 주기 구성 설정

#### 기능 설명
지정 버킷의 수명 주기 구성을 설정합니다.

#### 방식 프로토타입

```
put_bucket_lifecycle(Bucket, LifecycleConfiguration={}, **kwargs)
```
#### 요청 예시

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
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   | 유형 | 필수 입력 |
| -------------- | -------------- |---------- | ----------- |
 |  Bucket  | 버킷 이름, bucketname-appid로 구성 | String |   예 |
 |  Rule  |  해당 규칙을 설정하며 ID, Filter, Status, Expiration, Transition, NoncurrentVersionExpiration, NoncurrentVersionTransition, AbortIncompleteMultipartUpload 등이 포함됩니다 | List |   예 |
 |  ID  |  규칙 ID 설정 | string |  아니요 |
 |  Filter  | 규칙이 영향을 미치는 객체 집합을 설명하는 데 사용되며 버킷의 모든 객체를 설정해야 할 경우 Prefix는 비워두기로 설정하십시오 | Dict |  예 |
 |  Status  | 규칙을 시작할지를 설정하며 선택 가능 값은 Enabled 또는 Disabled입니다 | Dict |  예 |
 |  Expiration  |  객체 만료 규칙을 설정하며 일수 Days 또는 날짜 Date를 지정할 수 있습니다. Date의 형식은 반드시 GMT ISO 8601이어야 합니다. get_date 방법을 사용하여 구체적인 날짜를 지정하는 것이 좋습니다| Dict |  아니요 |
 |  Transition  | 객체 스토리지 클래스 전환 규칙을 설정하며 일수 Days 또는 날짜 Date를 지정할 수 있습니다. Date의 형식은 반드시 GMT ISO 8601이어야 합니다. get_date 방법을 사용하여 구체적인 날짜를 지정하는 것이 좋습니다. StorageClass는 Standard_IA, Archive를 선택할 수 있으며 해당 클래스의 규칙을 동시에 여러개 설정할 수 있습니다| List |  아니요 |
 |  NoncurrentVersionExpiration  | 현재 버전이 아닌 객체 만료 규칙을 설정하며 일수 NoncurrentDays를 지정할 수 있습니다 |  Dict |  아니요 |
 |  NoncurrentVersionTransition  | 현재 버전이 아닌 객체의 스토리지 클래스 전환 규칙을 설정하며 일수 NoncurrentDays를 지정하고 StorageClass는 Standard_IA를 선택할 수 있습니다. 해당 클래스의 규칙을 동시에 여러개 설정할 수 있습니다| List |  아니요 |
 |  AbortIncompleteMultipartUpload  |멀티파트 업로드 시작 후 며칠 내에 업로드가 완료되어야 하는지 표시합니다 |  Dict |  아니요 |


#### 반환 결과 설명

해당 방법의 반환값은 None입니다.

### 버킷 수명 주기 구성 획득

#### 기능 설명
지정 버킷의 수명 주기 구성을 획득합니다.

#### 방식 프로토타입

```
get_bucket_lifecycle(Bucket, **kwargs)
```
#### 요청 예시

```python
response = client.get_bucket_lifecycle(
    Bucket='test01-123456789',
)
```
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   | 유형 | 필수 입력 |
| -------------- | -------------- |---------- | ----------- |
| Bucket |버킷 이름, bucketname-appid로 구성|String|예 |

#### 반환 결과 설명

버킷의 수명 주기 구성이며 유형은 dict입니다.
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

| 매개변수 이름   | 매개변수 설명   | 유형 |
| -------------- | -------------- |---------- |
|  Rule  |  해당 규칙이며, ID, Filter, Status, Expiration, Transition, NoncurrentVersionExpiration, NoncurrentVersionTransition, AbortIncompleteMultipartUpload 등이 포함됩니다 | List |
|  ID  | 규칙의 ID | String |
|  Filter  |  규칙이 영향을 주는 객체 집합을 설명하는 데 사용됩니다 | Dict |
|  Status  |  규칙 사용 여부, 선택 가능 값은 Enabled 또는 Disabled입니다 | Dict |
|  Expiration  | 객체 만료 규칙이며, 일수 Days 또는 날짜 Date를 지정할 수 있습니다 |  Dict |
|  Transition  | 객체 스토리지 클래스 전환 규칙이며, 일수 Days 또는 날짜 Date를 지정할 수 있습니다. StorageClass는 STANDARD_IA, Archive를 선택할 수 있습니다| List |
|  NoncurrentVersionExpiration  | 현재 버전이 아닌 객체 만료 규칙이며, 일수 NoncurrentDays를 지정할 수 있습니다 |  Dict |
|  NoncurrentVersionTransition  | 현재 버전이 아닌 Object의 스토리지 클래스 전환 규칙이며, 일수 NoncurrentDays를 지정할 수 있고 StorageClass는 STANDARD_IA를 선택할 수 있습니다| List |
|  AbortIncompleteMultipartUpload  |  멀티파트 업로드 시작 후 며칠 내에 업로드가 완료되어야 하는지 표시합니다 | Dict |

### 버킷의 수명 주기 구성 삭제

#### 기능 설명

지정 버킷의 수명 주기 구성을 삭제합니다.

#### 방식 프로토타입

```
delete_bucket_lifecycle(Bucket, **kwargs)
```
#### 요청 예시

```python
response = client.delete_bucket_lifecycle(
    Bucket='test01-123456789',
)
```
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   | 유형 | 필수 입력 |
| -------------- | -------------- |---------- | ----------- |
| Bucket |버킷 이름, bucketname-appid로 구성|String|예 |

#### 반환 결과 설명

해당 방법의 반환값은 None입니다.


### 버킷의 버전 관리 구성 설정

#### 기능 설명
지정 버킷의 버전 관리 관련 구성을 설정합니다.

#### 방식 프로토타입

```
put_bucket_versioning(Bucket, Status, **kwargs)
```
#### 요청 예시

```pythone
response = client.put_bucket_versioning(
    Bucket='test01-123456789',
    Status='Enabled'|'Suspended'
)
```
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   | 유형 | 필수 입력 |
| -------------- | -------------- |---------- | ----------- |
|  Bucket  | 버킷 이름, bucketname-appid로 구성 | String |   예 |
|  Status  | 버킷 버전 관리 상태를 설정하며, 선택 가능 값은 'Enabled' 또는 'Suspended'입니다 | String |   예 |

#### 반환 결과 설명

해당 방법의 반환값은 None입니다.

### 버킷의 버전 관리 구성 획득

#### 기능 설명
지정 버킷의 버전 관리 구성을 획득합니다.

#### 방식 프로토타입

```
get_bucket_versioning(Bucket, **kwargs)
```
#### 요청 예시

```python
response = client.get_bucket_versioning(
    Bucket='test01-123456789',
)
```
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   | 유형 | 필수 입력 |
| -------------- | -------------- |---------- | ----------- |
| Bucket |버킷 이름, bucketname-appid로 구성|String|예 |

#### 반환 결과 설명

버킷 버전 관리 구성이며, 유형은 dict입니다.
```python
{
    'Status': 'Enabled'|'Suspended'
}
```

| 매개변수 이름   | 매개변수 설명   | 유형 |
| -------------- | -------------- |---------- |
|  Status  |  버킷 버전 관리 상태이며, 선택 가능 값은 'Enabled' 또는 'Suspended'입니다 | String |


### 버킷 크로스 도메인 복사 구성 설정

#### 기능 설명
지정 버킷의 크로스 도메인 복사 구성을 설정합니다.

#### 방식 프로토타입

```
put_bucket_replication(Bucket, ReplicationConfiguration={}, **kwargs)
```
#### 요청 예시

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
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   | 유형 | 필수 입력 |
| -------------- | -------------- |---------- | ----------- |
|  Bucket  | 소스 버킷 이름, bucketname-appid로 구성 | String |   예 |
|  Role  |  개시자 ID, 형식: qcs::cam::uin/<OwnerUin>:uin/<SubUin> | String |  아니요 |
|  Rule  |  대응하는 규칙을 설정하며, ID, Status, Prefix, Destination이 포함됩니다 | List |   예 |
|  ID  |  규칙 ID 설정 | string |  아니요 |
|  Status  | 규칙 사용 여부를 설정하며, 선택 가능 값은 Enabled 또는 Disabled입니다 | String |  예 |
|  Prefix  | 규칙의 접두사 매칭 규칙을 설정하며, 비어 있으면 해당하는 버킷에 있는 모든 객체를 나타냅니다 | String |  예 |
|  Destination  | 대상 리소스를 설명하며, Bucket 및 StorageClass가 포함됩니다| Dict |  예 |
|  Bucket  | 지역 간 복제의 대상 버킷을 설정하며, 형식은 qcs::cos:[region]::[bucketname-AppId]입니다 | String |  예 |
|  StorageClass  | 대상 파일의 스토리지 클래스를 설정하며, 선택 가능 값은 'STANDARD', 'STANDARD_IA'입니다 | String |  아니요 |

#### 반환 결과 설명

해당 방법의 반환값은 None입니다.

### 버킷의 지역 간 복제 구성 획득

#### 기능 설명
지정 버킷의 지역 간 복제 구성을 획득합니다.

#### 방식 프로토타입

```
get_bucket_replication(Bucket, **kwargs)
```
#### 요청 예시

```python
response = client.get_bucket_replication(
    Bucket='test01-123456789'
)
```
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   | 유형 | 필수 입력 |
| -------------- | -------------- |---------- | ----------- |
|  Bucket  | 버킷 이름, bucketname-appid로 구성 | String |   예 |

#### 반환 결과 설명

버킷의 지역 간 복제 구성이며, 유형은 dict입니다.
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

| 매개변수 이름   | 매개변수 설명   | 유형 |
| -------------- | -------------- |---------- |
|  Role  |  개시자 ID, 형식: qcs::cam::uin/<OwnerUin>:uin/<SubUin> | String |  아니요 |
|  Rule  |  지역 간 복제의 대응 규칙이며, ID, Status, Prefix, Destination이 포함됩니다 | List |   예 |
|  ID  |  지역 간 복제 규칙의 ID | String |  아니요 |
|  Status  | 지역 간 복제 규칙 사용 여부이며, 선택 가능 값은 Enabled 또는 Disabled입니다 | String |  예 |
|  Prefix  | 지역 간 복제 규칙의 접두사 매칭 규칙이며, 비어 있으면 해당하는 버킷에 있는 모든 객체를 나타냅니다 | String |  예 |
|  Destination  | 대상 리소스를 설명하며, Bucket 및 StorageClass가 포함됩니다| Dict |  예 |
|  Bucket  | 지역 간 복제의 대상 버킷이며, 형식은 qcs::cos:[region]::[bucketname-AppId]입니다 | String |  예 |
|  StorageClass  | 대상 파일의 스토리지 클래스이며, 선택 가능 값은 'STANDARD', 'STANDARD_IA'입니다 | String |  아니요 |

### 버킷의 지역 간 복제 구성 삭제

#### 기능 설명

지정 버킷의 지역 간 복제 구성을 삭제합니다.

#### 방식 프로토타입

```
delete_bucket_replication(Bucket, **kwargs)
```
#### 요청 예시

```python
response = client.delete_bucket_replication(
    Bucket='test01-123456789',
)
```
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   | 유형 | 필수 입력 |
| -------------- | -------------- |---------- | ----------- |
| Bucket |버킷 이름, bucketname-appid로 구성|String|예 |

#### 반환 결과 설명

해당 방법의 반환값은 None입니다.

## Object API 설명

### 파일 간편 업로드

#### 기능 설명

지정된 버킷에 로컬 파일 또는 입력 스트림 업로드를 지원합니다. 20MB 미만의 작은 파일을 업로드하는 것이 좋으며, 1회 업로드 크기는 5GB로 제한됩니다. 큰 파일 업로드는 멀티파트 업로드를 사용하십시오.
>!현재 액세스 정책 항목은 1000으로 제한되어 있습니다. 객체에 대해 ACL 제어가 필요하지 않은 경우 업로드 시 설정하지 마십시오. 기본으로 버킷 권한은 계승됩니다.

#### 방식 프로토타입

```
put_object(Bucket, Body, Key, **kwargs)
```
#### 요청 예시

```python
response = client.put_object(
    Bucket='test01-123456789',
    Body=b'abc'|file,
    Key='test.txt',
    EnableMD5=False
)
```
#### 모든 매개변수 요청 예시
```python
response = client.put_object(
    Bucket='test01-123456789',
    Body=b'abc'|file,
    Key='test.txt',
    EnableMD5=False|True,
    ACL='private'|'public-read'|'public-read-write',  # 이 매개변수 사용 시 ACL 상한인 1000개에 도달하지 않도록 주의하십시오
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
#### 매개변수 설명


| 매개변수 이름   | 매개변수 설명   | 유형 | 필수 입력 |
| -------------- | -------------- |---------- | ----------- |
 |  Bucket  |  버킷 이름, bucketname-appid로 구성 | String |   예 |
 |  Body  | 업로드 파일의 내용이며, 파일 스트림 또는 바이트 스트림일 수 있습니다 |  file/bytes |  예 |
 |  Key  | 객체 키(Key)이며, 버킷에서 객체의 유일한 식별자입니다. 예를 들어 객체의 액세스 도메인 이름 ` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg ` 중 객체 키는 doc1/pic1.jpg입니다 | String |  예 |
| EnableMD5 | SDK가 Content-MD5를 계산할 필요 여부이며, 기본적으로 꺼짐이고, 시작되면 업로드 시간이 증가될 수 있습니다| Bool | 아니요 |
| ACL | 파일의 ACL 설정, 예: 'private', 'public-read', 'public-read-write' |String| 아니요 |
| GrantFullControl | 지정 계정에게 파일에 대한 읽기/쓰기 권한을 부여합니다. 형식은 `id=" ",id=" "` 서브 계정에 권한을 부여해야 할 경우 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`루트 계정에 권한을 부여해야 할 경우 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"` 예: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` |String|아니요|
|GrantRead |지정 계정에 파일의 읽기 권한을 부여합니다. 형식은 `id=" ",id=" "`서브 계정에 권한을 부여해야 할 경우 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`루트 계정에 권한을 부여해야 할 경우 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`예: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` |String|아니요|
| GrantWrite|지정 계정에 파일의 쓰기 권한을 부여합니다. 형식은 `id=" ",id=" "`서브 계정에 권한을 부여해야 할 경우 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`루트 계정에 권한을 부여해야 할 경우 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`예: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` |String|아니요|
 | StorageClass  | 파일의 스토리지 클래스, STANDARD, STANDARD_IA를 설정합니다. 기본값: STANDARD | String      | 아니요   |
 |  Expires  | Content-Expires를 설정합니다 | String|  아니요 |
 |  CacheControl  |  캐시 정책, Cache-Control을 설정합니다 | String |   아니요 |
 |  ContentType  | 콘텐츠 유형, Content-Type을 설정합니다 |String |   아니요 |  
 |  ContentDisposition  |  파일 이름, Content-Disposition을 설정합니다 | String |   아니요 |
 |  ContentEncoding  |  인코딩 형식, Content-Encoding을 설정합니다 | String |   아니요 |
 |  ContentLanguage  |  언어 유형이며, Content-Language를 설정합니다 | String |   아니요 |
 |  ContentLength  | 전송 길이 설정 | String |   아니요 |
 |  ContentMD5  | 업로드 파일의 MD5 값을 인증에 사용하도록 설정합니다 | String |   아니요 |
 |  Metadata | 사용자의 사용자 지정 파일 메타 정보, x-cos-meta 접두사로 시작해야 하며 그렇지 않으면 무시됩니다 | Dict |  아니요 |

#### 반환 결과 설명
업로드 파일의 속성이며, 유형은 dict입니다.

```python
{
    'ETag': 'string',
    'x-cos-expiration': 'string'
}
```


| 매개변수 이름   | 매개변수 설명   | 유형 |
| -------------- | -------------- |---------- |
|  ETag   |  업로드 파일의 MD5 값  | String  |
|  x-cos-expiration   | 수명 주기 설정 후, 파일 만료 시간 규칙을 반환합니다  | String  |

### 파일 다운로드

#### 기능 설명
지정 버킷의 파일을 로컬로 다운로드합니다.

#### 방식 프로토타입

```
 get_object(Bucket, Key, **kwargs)
```
#### 요청 예시

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
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   | 유형 | 필수 입력 |
| -------------- | -------------- |---------- | ----------- |
 |  Bucket  |  버킷 이름, bucketname-appid로 구성 | String  |  예 |
 |  Key  | 객체 키(Key)이며, 버킷에서 객체의 유일한 식별자입니다. 예를 들어 객체의 액세스 도메인 이름 ` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg ` 중 객체 키는 doc1/pic1.jpg입니다 | String | 예 |
 |  Range  |  다운로드 파일의 범위를 설정하며, 형식은 bytes=first-last입니다  | String  |  아니요 |
 |  IfMatch  |  ETag와 지정된 내용이 일치할 때에만 반환됩니다 |String  | 아니요 |  
 |  IfModifiedSince  |   지정된 시간 이후에 수정된 경우에만 반환됩니다 | String  | 아니요 |
 |  IfNoneMatch  |  ETag와 지정된 내용이 불일치한 경우에만 반환됩니다 | String  | 아니요 |
 |  IfUnmodifiedSince  |  파일 수정 시간이 지정한 시간보다 빠르거나 같을 경우에만 반환합니다 | String  | 아니요|
 |  ResponseCacheControl  |  응답 헤더 Cache-Control을 설정합니다 | String  | 아니요 |
 |  ResponseContentDisposition  |  응답 헤더 Content-Disposition을 설정합니다 | String  | 아니요 |
 |  ResponseContentEncoding  |   응답 헤더 Content-Encoding을 설정합니다 | String  | 아니요 |
 |  ResponseContentLanguage  |  응답 헤더 Content-Language를 설정합니다 | String  | 아니요 |
 |  ResponseContentType  |   응답 헤더 Content-Type을 설정합니다 | String  | 아니요 |
 |  ResponseExpires  | 응답 헤더 Content-Expires를 설정합니다 |   String  | 아니요 |
 |  VersionId  | 다운로드 파일의 버전을 지정합니다 |  String  | 아니요 |

#### 반환 결과 설명

다운로드 파일의 본문 및 메타 정보이며, 유형은 dict입니다.

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

| 매개변수 이름   | 매개변수 설명   | 유형 |
| -------------- | -------------- |---------- |
 | Body  |  다운로드 파일의 내용이며, get_raw_stream 방법으로 파일 스트림을 얻을 수 있습니다. `get_stream_to_file` 방법은 파일 내용을 지정된 로컬 파일에 다운로드할 수 있습니다 | StreamBody |
 | 파일 메타 정보  |  다운로드 파일의 메타 정보, Etag 및 x-cos-request-id 등의 정보가 포함되며 설정된 파일 메타 정보도 반환할 수 있습니다 | String |


### 사전 서명 다운로드 링크 획득

#### 기능 설명
사전 서명 다운로드 링크를 획득하여 직접 다운로드에 사용합니다.

#### 방식 프로토타입

```
get_presigned_download_url(Bucket, Key, Expired=300, Params={}, Headers={})
```
#### 요청 예시

```python
response = client.get_presigned_download_url(
    Bucket='test01-123456789',
    Key='test.txt'
)
```
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   | 유형 | 필수 입력 |
| -------------- | -------------- |---------- | ----------- |
 | Bucket  |버킷 이름, bucketname-appid로 구성 |  String |  예 |
 |  Key  | 객체 키(Key)이며, 버킷에서 객체의 유일한 식별자입니다. 예를 들어 객체의 액세스 도메인 이름 ` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg ` 중 객체 키는 doc1/pic1.jpg입니다 | String | 예 |
 |Expired| 서명 만료 시간이며, 단위는 초입니다| Int | 아니요|
 |Params| 서명 중에 들어갈 요청 매개변수입니다| Dict | 아니요|
 |Headers| 서명 중에 들어갈 요청의 헤더입니다| Dict | 아니요|

#### 반환 결과 설명
이 방법 반환값은 사전 서명의 다운로드 URL입니다.

### 파일 삭제

#### 기능 설명
지정 Bucket의 대응하는 파일을 삭제합니다.

#### 방식 프로토타입

```
delete_object(Bucket, Key, **kwargs)
```
#### 요청 예시

```python
response = client.delete_object(
    Bucket='test01-123456789',
    Key='test.txt'
)
```
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   | 유형 | 필수 입력 |
| -------------- | -------------- |---------- | ----------- |
 | Bucket  |버킷 이름, bucketname-appid로 구성 |  String |  예 |
 |  Key  | 객체 키(Key)이며, 버킷에서 객체의 유일한 식별자입니다. 예를 들어 객체의 액세스 도메인 이름 ` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg ` 중 객체 키는 doc1/pic1.jpg입니다 | String | 예 |

#### 반환 결과 설명
해당 방법의 반환값은 None입니다.

### 파일 배치 삭제

#### 기능 설명
지정 버킷의 파일을 일괄 삭제합니다.

#### 방식 프로토타입

```
delete_objects(Bucket, Delete={}, **kwargs)
```
#### 요청 예시

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
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   | 유형 | 필수 입력 |
| -------------- | -------------- |---------- | ----------- |
 | Bucket  | 버킷 이름, bucketname-appid로 구성 |  String |  예 |
 | Delete  | 이번에 삭제된 반환 결과 방식 및 대상 객체를 설명합니다 | Dict | 예 |
 | Object  | 삭제할 각 대상 객체 정보를 설명합니다 | List | 예 |
 | Key     | 객체 키(Key)이며, 버킷에서 객체의 유일한 식별자입니다. 예를 들어, 객체의 액세스 도메인 이름 ` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg ` 중, 객체 키는 doc1/pic1.jpg입니다 | string      | 아니요 |
 | Quiet   |삭제의 반환 결과 방식을 표시하며, 선택 가능 값은 'true', 'false'이고 기본값은 'false'입니다. 'true'로 설정하면 실패한 오류 정보만 반환하며 'false'로 설정하면 성공과 실패의 모든 정보를 반환합니다.|String|아니요|

#### 반환 결과 설명
파일 배치 삭제의 결과이며, 유형은 dict입니다.
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

| 매개변수 이름   | 매개변수 설명   | 유형 |
| -------------- | -------------- |---------- |
 | Deleted  |  삭제 성공한 객체 정보|  List |
 | Key     | 삭제 성공한 객체 경로| String|
 | Error  |  삭제 실패한 객체 정보| List |
 | Key     | 삭제 실패한 객체 경로| String|
 | Code     | 삭제 실패한 객체의 해당 오류 코드| String|
 | Message   |삭제 실패한 객체의 해당 오류 정보| String|


### 파일 속성 획득
#### 기능 설명
지정 파일의 메타 정보를 획득합니다.

#### 방식 프로토타입

```
head_object(Bucket, Key, **kwargs)
```
#### 요청 예시

```python
response = client.head_object(
    Bucket='test01-123456789',
    Key='test.txt',
    IfModifiedSince='string'
)
```
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   | 유형 | 필수 입력 |
| -------------- | -------------- |---------- | ----------- |
  | Bucket   | 버킷 이름, bucketname-appid로 구성  | String  |  예 |
  |  Key  | 객체 키(Key)이며, 버킷에서 객체의 유일한 식별자입니다. 예를 들어 객체의 액세스 도메인 이름 ` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg ` 중 객체 키는 doc1/pic1.jpg입니다 | String | 예 |
  | IfModifiedSince   | 지정된 시간 이후에 수정된 경우에만 반환됩니다 | String  | 아니요 |

#### 반환 결과 설명

획득 파일의 메타 정보이며, 유형은 dict입니다.

```python
{
    'Content-Type': 'application/octet-stream',
    'Content-Length': '16807',
    'ETag': '"9a4802d5c99dafe1c04da0a8e7e166bf"',
    'Last-Modified': 'Wed, 28 Oct 2014 20:30:00 GMT',
    'x-cos-request-id': 'NTg3NzQ3ZmVfYmRjMzVfMzE5N182NzczMQ=='
}
```

| 매개변수 이름   | 매개변수 설명   | 유형 |
| -------------- | -------------- |---------- |
| 파일 메타 정보 |파일의 메타 정보 획득, Etag 및 x-cos-request-id 등의 정보가 포함되며 설정된 파일 메타 정보도 포함됩니다| String|

### 멀티파트 업로드 생성

#### 기능 설명

새로운 멀티파트 업로드 태스크를 만들고, UploadId를 반환합니다.

#### 방식 프로토타입

```
create_multipart_upload(Bucket, Key, **kwargs):
```
#### 요청 예시

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
# UploadId 획득하여 후속 API 사용
uploadid = response['UploadId']
```
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   | 유형 | 필수 입력 |
| -------------- | -------------- |---------- | ----------- |
 | Bucket  | 버킷 이름, bucketname-appid로 구성 |  String |  예 |
 | Key   | 객체 키(Key)이며, 버킷에서 객체의 유일한 식별자입니다. 예를 들어 객체의 액세스 도메인 이름 ` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg ` 중 객체 키는 doc1/pic1.jpg입니다 | String | 예 |
 | StorageClass  | 파일의 스토리지 클래스, STANDARD, STANDARD_IA를 설정합니다. 기본값: STANDARD | String |  아니요 |
 | Expires  |  Content-Expires를 설정합니다 | String| 아니요 |
 | CacheControl  | 캐시 정책, Cache-Control을 설정합니다 | String |  아니요 |
 | ContentType  | 콘텐츠 유형, Content-Type을 설정합니다 | String |  아니요 |
 | ContentDisposition  | 파일 이름, Content-Disposition을 설정합니다 | String |  아니요 |
 | ContentEncoding  | 인코딩 형식, Content-Encoding을 설정합니다 | String |  아니요 |
 | ContentLanguage  | 언어 유형이며, Content-Language를 설정합니다 |  String |  아니요 |
 | Metadata |사용자의 사용자 지정 파일 메타 정보 | Dict |  아니요 |
 | ACL |파일의 ACL 설정, 예: 'private', 'public-read', 'public-read-write' |String| 아니요|
| GrantFullControl | 지정 계정에게 파일에 대한 읽기/쓰기 권한을 부여합니다. 형식은 `id=" ",id=" "` 서브 계정에 권한을 부여해야 할 경우 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`루트 계정에 권한을 부여해야 할 경우 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"` 예: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` |String|아니요|
|GrantRead |지정 계정에 파일의 읽기 권한을 부여합니다. 형식은 `id=" ",id=" "`서브 계정에 권한을 부여해야 할 경우 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`루트 계정에 권한을 부여해야 할 경우 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`예: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` |String|아니요|
| GrantWrite|지정 계정에 파일의 쓰기 권한을 부여합니다. 형식은 `id=" ",id=" "`서브 계정에 권한을 부여해야 할 경우 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`루트 계정에 권한을 부여해야 할 경우 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`예: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` |String|아니요|

#### 반환 결과 설명

멀티파트 업로드의 초기화 정보를 획득하며, 유형은 dict입니다:

```python
{
    'UploadId': '150219101333cecfd6718d0caea1e2738401f93aa531a4be7a2afee0f8828416f3278e5570',
    'Bucket': 'test01-123456789',
    'Key': 'multipartfile.txt'
}

```

| 매개변수 이름   | 매개변수 설명   | 유형 |
| -------------- | -------------- |---------- |
|UploadId | 멀티파트 업로드의 ID|String|
|Bucket |버킷 이름, bucket-appid로 구성|String|
|Key | 객체 키(Key)이며, 버킷에서 개체의 유일한 식별자입니다. 예를 들어 객체의 액세스 도메인 이름 ` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg ` 중 객체 키는 doc1/pic1.jpg입니다|String|

### 멀티파트 업로드 포기

#### 기능 설명
멀티파트 업로드 태스크를 취소하고, 이미 업로드된 파트를 삭제합니다.

#### 방식 프로토타입

```
abort_multipart_upload(Bucket, Key, UploadId, **kwargs)
```
#### 요청 예시

```python
response = client.abort_multipart_upload(
    Bucket='test01-123456789',
    Key='multipart.txt',
    UploadId=uploadid
)
```
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   | 유형 | 필수 입력 |
| -------------- | -------------- |---------- | ----------- |
|Bucket |버킷 이름, bucketname-appid로 구성|String| 예|
|Key | 객체 키(Key)이며, 버킷에서 객체의 유일한 식별자입니다. 예를 들어 객체의 액세스 도메인 이름 ` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg ` 중 객체 키는 doc1/pic1.jpg입니다 |String| 예 |
|UploadId |멀티파트 업로드의 ID|String| 예|

#### 반환 결과 설명
해당 방법의 반환값은 None입니다.

### 파트 업로드
#### 기능 설명
하나의 파트를 지정된 UploadId에 업로드하며, 단일 파트 크기는 5GB를 초과할 수 없습니다.

#### 방식 프로토타입

```
upload_part(Bucket, Key, Body, PartNumber, UploadId, **kwargs)
```
#### 요청 예시

```python
# 주의: 멀티파트 업로드의 최대 파트 수량은 10000입니다
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
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   | 유형 | 필수 입력 |
| -------------- | -------------- |---------- | ----------- |
 | Bucket  | 버킷 이름, bucketname-appid로 구성 | String |  예|
 | Key  | 객체 키(Key)이며, 버킷에서 객체의 유일한 식별자입니다. 예를 들어 객체의 액세스 도메인 이름 ` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg ` 중 객체 키는 doc1/pic1.jpg입니다 | String | 예 |
 | Body  | 멀티파트 업로드의 내용이며, 로컬 파일 스트림 또는 입력 스트림일 수 있습니다 | file/bytes |  예|
 | PartNumber  |멀티파트 업로드의 번호를 식별합니다 |  Int |  예|
 | UploadId  | 멀티파트 업로드의 ID 표시 | String |  예|
 | EnableMD5 | SDK가 Content-MD5를 계산할 필요 여부이며, 기본 설정은 꺼짐이고 시작되면 다음에는 업로드 시간이 증가될 수 있습니다|Bool | 아니요|
 | ContentLength  |전송 길이 설정 |  Int |  아니요|
 | ContentMD5  | 업로드 파일의 MD5 값을 검증에 사용하도록 설정합니다 | String |  아니요|

#### 반환 결과 설명

멀티파트 업로드의 속성이며, 유형은 dict입니다:

```python
{
    'ETag': 'string'
}
```

| 매개변수 이름   | 매개변수 설명   | 유형 |
| -------------- | -------------- |---------- |
| ETag |멀티파트　업로드의 MD5 값.|String|

### 멀티파트 업로드 나열
#### 기능 설명
지정 UploadId에 이미 업로드된 파트의 정보를 나열합니다.

#### 방식 프로토타입

```
list_parts(Bucket, Key, UploadId, MaxParts=1000, PartNumberMarker=0, EncodingType='', **kwargs)
```
#### 요청 예시

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
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   | 유형 | 필수 입력 |
| -------------- | -------------- |---------- | ----------- |
|Bucket |버킷 이름, bucketname-appid로 구성|String| 예|
|Key | 객체 키(Key)이며, 버킷에서 객체의 유일한 식별자입니다. 예를 들어 객체의 액세스 도메인 이름 ` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg ` 중 객체 키는 doc1/pic1.jpg입니다 |String| 예 |
|UploadId |멀티파트 업로드의 ID|String| 예|
|MaxParts |멀티파트의 최대 반환 수량, 기본값은 1000|Int| 아니요|
|PartNumberMarker |기본값은 0이고 첫번째 파트부터 나열하고 PartNumberMarker의 다음 파트부터 나열하기 시작합니다|Int| 아니요|
|EncodingType |기본으로 인코딩하지 않음, 반환값의 인코딩 방식을 규정합니다. 선택 가능 값: url |String|아니요|

#### 반환 결과 설명

모든 멀티파트 업로드의 정보이며, 유형은 dict입니다.

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

| 매개변수 이름   | 매개변수 설명   | 유형 |
| -------------- | -------------- |---------- |
| Bucket   |  버킷 이름, bucketname-appid로 구성  | String  |
|  Key  | 객체 키(Key)이며, 버킷에서 개체의 유일한 식별자입니다. 예를 들어 객체의 액세스 도메인 이름 ` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg ` 중 객체 키는 doc1/pic1.jpg입니다|String|
|  UploadId  |  멀티파트 업로드의 ID | String |
| EncodingType   | 기본으로 인코딩하지 않음, 반환값의 인코딩 방식을 지정합니다. 선택 가능값: url  | String |
| MaxParts   | 파트의 최대 반환 수량, 기본값은 1000  | String  |
| IsTruncated   |  반환된 멀티파트가 잘렸는지 표시합니다  | String|
| PartNumberMarker   | 기본값은 0이고 첫번째 파트부터 나열하고 PartNumberMarker의 다음 파트부터 나열하기 시작합니다  | String  |
| NextPartNumberMarker   |  다음 나열될 파트의 시작 위치를 표시합니다  | String  |
 |  StorageClass  |  파일의 스토리지 클래스, STANDARD, STANDARD_IA. 기본값: STANDARD | String |
|  Part |멀티파트 업로드 관련 정보, ETag, PartNumber, Size, LastModified 등이 포함됩니다 | String |
 |  Initiator  | 멀티파트 업로드의 생성자, DisplayName 및 ID가 포함됩니다 | Dict |
 |  Owner  | 파일 소유자의 정보, DisplayName 및 ID가 포함됩니다 | Dict |


### 멀티파트 업로드 완료

#### 기능 설명

지정된 UploadId의 모든 파트를 한 개의 파일로 모읍니다. 파일의 최종 크기는 1MB보다 커야 하며 그렇지 않으면 오류가 반환됩니다.

#### 방식 프로토타입

```
complete_multipart_upload(Bucket, Key, UploadId, MultipartUpload={}, **kwargs)
```
#### 요청 예시

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
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   | 유형 | 필수 입력 |
| -------------- | -------------- |---------- | ----------- |
|  Bucket  | 버킷 이름, bucketname-appid로 구성 | String |   예|
|  Key  | 객체 키(Key)이며, 버킷에서 객체의 유일한 식별자입니다. 예를 들어 객체의 액세스 도메인 이름 ` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg ` 중 객체 키는 doc1/pic1.jpg입니다 | String  |   예|
|  UploadId  | 멀티파트 업로드의 ID | String  |   예|
|  MultipartUpload  |모든 파트의 ETag 및 PartNumber 정보 |  Dict |   예|

#### 반환 결과 설명

피키징 후의 파일 관련 정보이며, 유형은 dict입니다.

```python
{
    'ETag': '"3f866d0050f044750423e0a4104fa8cf-2"',
    'Bucket': 'test01-123456789',
    'Location': 'test01-123456789.cn-north.myqcloud.com/multipartfile.txt',
    'Key': 'multipartfile.txt'
}
```

| 매개변수 이름   | 매개변수 설명   | 유형 |
| -------------- | -------------- |---------- |
 |  ETag | 병합 후 객체의 고유한 태그 값입니다. 해당 값은 객체 콘텐츠의 MD5 검증값이 아니며, 대상의 고유성을 검사하는 데만 사용할 수 있습니다. 파일 내용을 검사해야 할 경우, 업로드 과정에 단일 파트의 ETag 값을 검증할 수 있습니다. | String |
 |  Bucket  |버킷 이름, bucketname-appid로 구성 |  String |
 |  Location  | URL 주소 |  String |
 |  Key  | 객체 키(Key)이며, 버킷에서 개체의 유일한 식별자입니다. 예를 들어 객체의 액세스 도메인 이름 ` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg ` 중 객체 키는 doc1/pic1.jpg입니다 | String |

### Object ACL 정보 설정

#### 기능 설명

파일의 ACL 정보를 설정하고 ACL, GrantFullControl, GrantRead, GrantWrite를 통해 헤더를 가져오는 방식으로 ACL을 설정하거나 AccessControlPolicy를 통해 본문을 가져오며 ACL을 설정할 수 있습니다. 두 방식 중 하나만 선택해야 하며 그렇지 않으면 충돌이 반환됩니다.
>!현재 접근 정책 항목은 1000으로 제한되어 있습니다. 객체에 대해 ACL 제어가 필요하지 않은 경우 설정하지 마십시오. 기본으로 버킷 권한은 승계됩니다.

#### 방식 프로토타입

```
put_object_acl(Bucket, Key, AccessControlPolicy={}, **kwargs)
```
#### 요청 예시

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
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   | 유형 | 필수 입력 |
| -------------- | -------------- |---------- | ----------- |
| Bucket   |  버킷 이름, bucketname-appid로 구성 | String  |  예  |
| Key   | 객체 키(Key)이며, 버킷에서 객체의 유일한 식별자입니다. 예를 들어 객체의 액세스 도메인 이름 ` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg ` 중 객체 키는 doc1/pic1.jpg입니다 | String  |   예|
| ACL |파일의 ACL 설정, 예: 'private', 'public-read', 'public-read-write' |String| 아니요|
| GrantFullControl | 지정 계정에게 파일에 대한 읽기/쓰기 권한을 부여합니다. 형식은 `id=" ",id=" "` 서브 계정에 권한을 부여해야 할 경우 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`루트 계정에 권한을 부여해야 할 경우 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"` 예: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` |String|아니요|
|GrantRead |지정 계정에 파일의 읽기 권한을 부여합니다. 형식은 `id=" ",id=" "`서브 계정에 권한을 부여해야 할 경우 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`루트 계정에 권한을 부여해야 할 경우 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`예: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` |String|아니요|
| GrantWrite|지정 계정에 파일의 쓰기 권한을 부여합니다. 형식은 `id=" ",id=" "`서브 계정에 권한을 부여해야 할 경우 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`루트 계정에 권한을 부여해야 할 경우 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`예: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` |String|아니요|
| AccessControlPolicy   | 지정 계정에 파일 액세스 권한을 부여하며 구체적인 형식은 get object acl 반환 결과 설명을 참조하십시오| Dict  | 아니요  |


#### 반환 결과 설명

해당 방법의 반환값은 None입니다.

### Object ACL 정보 획득

#### 기능 설명
지정 파일의 ACL 정보를 획득합니다.

#### 방식 프로토타입

```
get_object_acl(Bucket, Key, **kwargs)
```
#### 요청 예시

```python
response = client.get_object_acl(
    Bucket='test01-123456789',
    Key='test.txt'
)
```
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   | 유형 | 필수 입력 |
| -------------- | -------------- |---------- | ----------- |
|Bucket|버킷 이름, bucketname-appid로 구성|String| 예|
|Key | 객체 키(Key)이며, 버킷에서 객체의 유일한 식별자입니다. 예를 들어 객체의 액세스 도메인 이름 ` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg ` 중 객체 키는 doc1/pic1.jpg입니다 | String  |   예|


#### 반환 결과 설명

Bucket ACL 정보이며, 유형은 Dict입니다.
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

| 매개변수 이름   | 매개변수 설명   | 유형 |
| -------------- | -------------- |---------- |
 |  Owner  | 파일 소유자의 정보, DisplayName 및 ID가 포함됩니다 | Dict |
 |  Grant  | 파일 권한 부여자의 정보, Grantee 및 Permission이 포함됩니다 | List |
 |  Grantee  |파일 권한 부여자의 정보, DisplayName, Type, ID 및 URI가 포함됩니다 |  Dict |
 |  DisplayName  |  권한 부여자의 이름 | String |
 |  Type  |  권한 부여자의 유형, 유형은 CanonicalUser 또는 Group입니다 | String |
 |  ID  | Type이 CanonicalUser일 경우 해당 권한 부여자의 ID | String |
 |  URI  |Type이 Group일 때 해당 권한 부여자의 URI |  String |
 |  Permission  |  부여자가 소유한 파일의 권한, 선택 가능 값은 FULL_CONTROL, WRITE, READ이며 각각 읽기/쓰기 권한, 쓰기 권한, 읽기 권한에 대응합니다 | String |

### 파일 복사

#### 기능 설명
파일이 소스 경로에서 대상 경로로 복사될 때 복사 과정 중에서 파일 메타 속성 및 ACL은 수정될 수 있습니다. 복사 조작을 실행해야 할 때 객체가 5GB보다 크고 소스 및 대상 객체가 같은 지역에 있지 않으면 create_multipart_upload() API를 사용하여 멀티파트 업로드를 생성하고 upload_part_copy() API를 사용하여 멀티파트 복사를 진행하고 complete_multipart_upload()를 사용하여 멀티파트 업로드를 완료해야 합니다. 복사할 객체가 5GB보다 작거나 같거나 같은 지역 내에서 복사될 경우 직접 copy_object()를 호출하면 됩니다.

#### 방식 프로토타입

```
copy_object(Bucket, Key, CopySource, CopyStatus='Copy', **kwargs)
```
#### 요청 예시

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
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   | 유형 | 필수 입력 |
| -------------- | -------------- |---------- | ----------- |
 |  Bucket  |  버킷 이름, bucketname-appid로 구성 | String|  예 |
 |  Key  | 객체 키(Key)이며, 버킷에서 객체의 유일한 식별자입니다. 예를 들어 객체의 액세스 도메인 이름 ` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg ` 중 객체 키는 doc1/pic1.jpg입니다 | String | 예 |
 |  CopySource  | 소스 파일을 복사할 경로를 설명하며 Appid, Bucket, Key, Region을 포함합니다 |  Dict | 예 |
 |  CopyStatus  |  선택 가능 값은 'Copy', 'Replaced'이며 'Copy'로 설정 시 설정한 사용자의 메타데이터 정보를 무시하고 직접 복사하며 'Replaced'로 설정하면 설정한 메타 정보에 따라 메타데이터를 수정합니다. 대상 경로와 소스 경로가 같을 경우 반드시 'Replaced'로 설정해야 합니다 | String| 예 |
| ACL | 파일의 ACL 설정, 예: 'private', 'public-read', 'public-read-write' |String| 아니요 |
| GrantFullControl | 지정 계정에게 파일에 대한 읽기/쓰기 권한을 부여합니다. 형식은 `id=" ",id=" "` 서브 계정에 권한을 부여해야 할 경우 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`루트 계정에 권한을 부여해야 할 경우 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"` 예: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` |String|아니요|
|GrantRead |지정 계정에 파일의 읽기 권한을 부여합니다. 형식은 `id=" ",id=" "`서브 계정에 권한을 부여해야 할 경우 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`루트 계정에 권한을 부여해야 할 경우 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`예: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` |String|아니요|
| GrantWrite|지정 계정에 파일의 쓰기 권한을 부여합니다. 형식은 `id=" ",id=" "`서브 계정에 권한을 부여해야 할 경우 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`루트 계정에 권한을 부여해야 할 경우 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`예: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` |String|아니요|
 |  StorageClass  |  파일의 스토리지 클래스, STANDARD, STANDARD_IA를 설정합니다. 기본값: STANDARD | String|  아니요 |
 |  Expires  | Content-Expires를 설정합니다 | String| 아니요 |
 |  CacheControl  | 캐시 정책, Cache-Control을 설정합니다 | String|  아니요 |
 |  ContentType  | 콘텐츠 유형, Content-Type을 설정합니다 | String|  아니요 |
 |  ContentDisposition  |  파일 이름, Content-Disposition을 설정합니다 | String|  아니요 |
 |  ContentEncoding  | 인코딩 형식, Content-Encoding을 설정합니다 | String|  아니요 |
 |  ContentLanguage  |  언어 유형이며, Content-Language를 설정합니다 | String|  아니요 |
 |  Metadata |사용자의 사용자 지정 파일 메타 정보 | Dict |  아니요 |


#### 반환 결과 설명
업로드 파일의 속성이며, 유형은 dict입니다.

```python
{
    'ETag': 'string',
    'LastModified': 'string',
}
```

| 매개변수 이름   | 매개변수 설명   | 유형 |
| -------------- | -------------- |---------- |
| ETag |복사 파일의 MD5 값|String|
| LastModified |복사 파일의 마지막 수정 시간|String|

### 멀티파트 복사

#### 기능 설명
파일의 멀파트 콘텐츠를 소스 경로에서 대상 경로로 복사합니다.

#### 방식 프로토타입

```
upload_part_copy(Bucket, Key, PartNumber, UploadId, CopySource, CopySourceRange='', **kwargs)
```
#### 요청 예시

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
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   | 유형 | 필수 입력 |
| -------------- | -------------- |---------- | ----------- |
|  Bucket  |  버킷 이름, bucketname-appid로 구성 | String|  예 |
|  Key  | 객체 키(Key)이며, 버킷에서 객체의 유일한 식별자입니다. 예를 들어 객체의 액세스 도메인 이름 ` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg ` 중 객체 키는 doc1/pic1.jpg입니다 | String | 예 |
| PartNumber  |멀티파트 업로드의 번호를 식별합니다 |  Int |  예|
| UploadId  | 멀티파트 업로드의 ID 표시 | String |  예|
|  CopySource  | 소스 파일을 복사할 경로를 설명하며 Appid, Bucket, Key, Region을 포함합니다 |  Dict | 예 |
|CopySourceRange| 소스 파일 복사의 범위를 설명하며 형식은 bytes=first-last입니다. 지정하지 않으면 기본으로 전체 소스 파일을 복사합니다|String|아니요|
|CopySourceIfMatch| 소스 파일의 Etag와 주어진 값이 같을 경우에만 복사합니다|String|아니요|
|CopySourceIfModifiedSince| 소스 파일이 주어진 시간 이후에 수정되면 복사합니다|String|아니요|
|CopySourceIfNoneMatch| 소스 파일의 Etag가 주어진 값과 같지 않을 경우에만 복사합니다|String|아니요|
|CopySourceIfUnmodifiedSince| 소스 파일이 주어진 시간 에 수정되지 않은 경우에만 복사합니다|String|아니요|

#### 반환 결과 설명

멀티파트 복사의 속성이며, 유형은 dict입니다.

```python
{
    'ETag': 'string',
    'LastModified': 'string',
}
```

| 매개변수 이름   | 매개변수 설명   | 유형 |
| -------------- | -------------- |---------- |
| ETag |멀티파트 복사의 MD5 값|String|
| LastModified |멀티파트 복사의 마지막 수정 시간|String|

### 보관 파일 복원

#### 기능 설명
COS를 통해 archive 유형으로 보관될 수 있는 객체를 복구하는 데 사용됩니다.

#### 방식 프로토타입

```
restore_object(Bucket, Key, RestoreRequest={}, **kwargs)
```
#### 요청 예시

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
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   | 유형 | 필수 입력 |
| -------------- | -------------- |---------- | ----------- |
|Bucket|버킷 이름, bucketname-appid로 구성|String| 예|
|Key | 객체 키(Key)이며, 버킷에서 객체의 유일한 식별자입니다. 예를 들어 객체의 액세스 도메인 이름 ` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg ` 중 객체 키는 doc1/pic1.jpg입니다 | String  |   예|
|RestoreRequest| 가져온 임시 파일의 규칙을 설명합니다| Dict|예|
|Days| 임시 파일의 만료 시간을 설명합니다| Int|예|
|CASJobParameters| 복구 유형의 구성 정보를 설명합니다| Dict|아니요|
|Tier| 임시 파일을 가져오는 모드를 설명합니다. 선택 가능 값은 'Expedited', Standard', 'Bulk'이며 각각 빠름, 표준 및 느림의 세 가지 모드에 해당합니다| String|아니요|

#### 반환 결과 설명
해당 방법의 반환값은 None입니다.

## High-level API 설명(추천)

### 파일 업로드(중단점 재개)

#### 기능 설명
파일 업로드 API는 사용자 파일의 길이에 따라 자동으로 간편 업로드와 멀티파트 업로드를 선택합니다. 20MB 이하의 파일은 간편 업로드를 호출하고 20MB를 초과하는 파일은 멀티파트 업로드를 호출합니다. 멀티파트 업로드가 완성되지 않은 파일은 자동으로 중단점 재개를 진행할 수 있습니다.

#### 방식 프로토타입

```
upload_file(Bucket, Key, LocalFilePath, PartSize=1, MAXThread=5, **kwargs)
```
#### 요청 예시

```python
response = client.upload_file(
    Bucket='test01-123456789',
    Key='test.txt',
    LocalFilePath='local.txt',
    EnableMD5=False
)
```

#### 모든 매개변수 요청 예시
```python
response = client.upload_file(
    Bucket='test01-123456789',
    Key='test.txt',
    LocalFilePath='local.txt',
    PartSize=1,
    MAXThread=5,
    EnableMD5=False|True,
    ACL='private'|'public-read'|'public-read-write', # 이 매개변수 사용 시 ACL 상한인 1000개에 도달하지 않도록 주의하십시오
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
#### 매개변수 설명


| 매개변수 이름   | 매개변수 설명   | 유형 | 필수 입력 |
| -------------- | -------------- |---------- | ----------- |
 |  Bucket  |  버킷 이름, bucketname-appid로 구성 | String |   예 |
 |  Key  | 객체 키(Key)이며, 버킷에서 객체의 유일한 식별자입니다. 예를 들어 객체의 액세스 도메인 이름 ` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg ` 중 객체 키는 doc1/pic1.jpg입니다 | String |  예 |
|  LocalFilePath  | 로컬 파일의 경로 이름 |  String |  예 |
|  PartSize  | 멀티파트 업로드의 파트 크기이며, 기본값은 1MB |  Int |  아니요 |
|  MAXThread  | 멀티파트 업로드의 동시 업로드 수량이며, 기본으로 5개 스레드로 파트를 업로드합니다 |  Int |  아니요 |
| EnableMD5 | SDK가 Content-MD5를 계산할 필요 여부이며, 기본 설정은 꺼짐이고 시작되면 다음에는 업로드 시간이 증가될 수 있습니다|Bool | 아니요|
| ACL |파일의 ACL 설정, 예: 'private', 'public-read', 'public-read-write' |String| 아니요|
| GrantFullControl | 지정 계정에게 파일에 대한 읽기/쓰기 권한을 부여합니다. 형식은 `id=" ",id=" "` 서브 계정에 권한을 부여해야 할 경우 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`루트 계정에 권한을 부여해야 할 경우 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"` 예: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` |String|아니요|
|GrantRead |지정 계정에 파일의 읽기 권한을 부여합니다. 형식은 `id=" ",id=" "`서브 계정에 권한을 부여해야 할 경우 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`루트 계정에 권한을 부여해야 할 경우 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`예: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` |String|아니요|
| GrantWrite|지정 계정에 파일의 쓰기 권한을 부여합니다. 형식은 `id=" ",id=" "`서브 계정에 권한을 부여해야 할 경우 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`루트 계정에 권한을 부여해야 할 경우 형식은 `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`예: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` |String|아니요|
 | StorageClass  | 파일의 스토리지 클래스, STANDARD, STANDARD_IA를 설정합니다. 기본값: STANDARD | String      | 아니요   |
 |  Expires  | Content-Expires를 설정합니다 | String|  아니요 |
 |  CacheControl  |  캐시 정책, Cache-Control을 설정합니다 | String |   아니요 |
 |  ContentType  | 콘텐츠 유형, Content-Type을 설정합니다 |String |   아니요 |  
 |  ContentDisposition  |  파일 이름, Content-Disposition을 설정합니다 | String |   아니요 |
 |  ContentEncoding  |  인코딩 형식, Content-Encoding을 설정합니다 | String |   아니요 |
 |  ContentLanguage  |  언어 유형이며, Content-Language를 설정합니다 | String |   아니요 |
 |  ContentLength  | 전송 길이 설정 | String |   아니요 |
 |  ContentMD5  | 업로드 파일의 MD5 값을 인증에 사용하도록 설정합니다 | String |   아니요 |
 |  Metadata | 사용자의 사용자 지정 파일 메타 정보 | Dict |   아니요 |

#### 반환 결과 설명
업로드 파일의 속성이며, 유형은 dict입니다.

```python
{
    'ETag': 'string',
    'x-cos-expiration': 'string'
}
```

| 매개변수 이름   | 매개변수 설명   | 유형 |
| -------------- | -------------- |---------- |
|  ETag   |  업로드 파일의 MD5 값  | String  |
|  x-cos-expiration   | 수명 주기 설정 후, 파일 만료 시간 규칙을 반환합니다  | String  |

## 서명 획득 API 설명

### 서명 획득

#### 기능 설명
지정된 조작의 서명을 획득하며 모바일 서명 배포에 자주 사용됩니다.

#### 방식 프로토타입

```
get_auth(Method, Bucket, Key, Expired=300, Headers={}, Params={})
```
#### 요청 예시

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
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   | 유형 | 필수 입력 |
| -------------- | -------------- |---------- | ----------- |
 | Method  |해당 조작의 방법이며, 선택 가능 값은 'PUT', 'POST', 'GET', 'DELETE', 'HEAD'입니다|  String |  예 |
 | Bucket  |버킷 이름, bucketname-appid로 구성 |  String |  예 |
 | Key  | 버킷 조작은 루트 경로 /를 입력하고 객체 조작은 파일의 경로를 입력합니다| String | 예|
 |Expired| 서명 만료 시간이며, 단위는 초입니다| Int | 아니요|
 |Headers| 서명이 들어가야 할 요청 헤더| Dict| 아니요|
 |Params | 서명이 들어가야 할 요청 매개변수| Dict| 아니요|

#### 반환 결과 설명
해당 방법의 반환값은 대응하는 조작의 서명값입니다.

### 사전 서명 링크 획득

#### 기능 설명
사전 서명 링크를 획득하여 배포에 사용합니다.

#### 방식 프로토타입

```
get_presigned_url(Bucket, Key, Method, Expired=300, Params={}, Headers={})
```
#### 요청 예시

```python
response = client.get_presigned_url(
    Bucket='test01-123456789',
    Key='test.txt',
    Method='PUT'|'POST'|'GET'|'DELETE'|'HEAD'
)
```
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   | 유형 | 필수 입력 |
| -------------- | -------------- |---------- | ----------- |
 | Bucket  |버킷 이름, bucketname-appid로 구성 |  String |  예 |
 |  Key  | 객체 키(Key)이며, 버킷에서 객체의 유일한 식별자입니다. 예를 들어 객체의 액세스 도메인 이름 ` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg ` 중 객체 키는 doc1/pic1.jpg입니다 | String | 예 |
 | Method  |해당 조작의 방법이며, 선택 가능 값은 'PUT', 'POST', 'GET', 'DELETE', 'HEAD'입니다|  String |  예 |
 |Expired| 서명 만료 시간이며, 단위는 초입니다| Int | 아니요|
 |Params| 서명 중에 들어갈 요청 매개변수입니다| Dict | 아니요|
 |Headers| 서명 중에 들어갈 요청의 헤더입니다| Dict | 아니요|


#### 반환 결과 설명
이 방법의 반환값은 사전 서명의 URL입니다.

## 이상 유형 설명
CosClientError 및 CosServiceError를 포함하며 각각 SDK 클라이언트 오류 및 COS 서버 오류에 해당합니다.

### CosClientError
CosClientError는 일반적으로 timeout으로 인한 클라이언트 오류를 가리키며 사용자가 캡처 후에 다시 시도나 다른 조작을 선택할 수 있습니다.

### CosServiceError
CosServiceError는 서버가 반환한 구체 정보를 제공합니다. 오류 코드에 대한 더 자세한 정보는 [COS 오류 코드](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오.

```python
#except CosServiceError as e
e.get_origin_msg()  # 기존의 오류 정보 획득, 형식: XML
e.get_digest_msg()  # 처리된 오류 정보를 획득하며 형식은 dict
e.get_status_code() # http 오류 코드 획득(예: 4XX, 5XX)
e.get_error_code()  # Cos 정의 오류 코드 획득
e.get_error_msg()   # COS 오류 코드의 구체 설명 획득
e.get_trace_id()    # 요청의 trace_id 획득
e.get_request_id()  # 요청의 request_id 획득
e.get_resource_location() # URL 주소 획득
```
