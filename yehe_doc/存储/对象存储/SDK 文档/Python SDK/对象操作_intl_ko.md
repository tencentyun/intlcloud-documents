## 소개

본 문서는 객체에 대한 간단한 작업, 멀티파트 작업 등과 관련한 API 개요 및 SDK 예시 코드에 대해 설명합니다.

**간단한 작업**

| API                                                          | 작업명         | 작업 설명                                  |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Bucket(List Object)](https://intl.cloud.tencent.com/document/product/436/30614) | 객체 쿼리| 버킷의 일부 또는 모든 객체를 쿼리|
| [GET Bucket Object Versions](https://intl.cloud.tencent.com/document/product/436/31551) |객체 및 해당 버전 기록 쿼리 |   버킷의 일부 또는 모든 객체와 해당 버전 기록 쿼리|
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | 객체 업로드       | 버킷에 객체를 업로드    |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | 객체 메타데이터 쿼리  | 객체의 메타데이터 쿼리                |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | 객체 다운로드       | 로컬 파일 시스템에 객체 다운로드        |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | 객체 복사   | 대상 경로에 객체 복사                        |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) |  객체 삭제   | 버킷에서 객체 삭제 |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | 여러 객체 삭제   | 버킷에서 여러 객체 삭제 |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | 아카이브된 객체 복구 | 아카이브 유형의 객체 검색 및 액세스                      |
| [SELECT Object content](https://intl.cloud.tencent.com/document/product/436/32360) | 객체 콘텐츠 인덱스 | 지정 객체에서 콘텐츠 인덱스                      |
| [APPEND Object](https://intl.cloud.tencent.com/document/product/436/7741) | 객체 추가 업로드 | 객체를 멀티파트 추가 방식으로 버킷에 업로드                      |


**멀티파트 작업**

| API                                                          | 작업명         | 작업 설명                             |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | 멀티파트 업로드 조회   | 현재 진행 중인 멀티파트 업로드 정보 조회         |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | 멀티파트 업로드 초기화 | 	멀티파트 업로드 작업 초기화     |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | 파트 업로드       | 파일 멀티파트 업로드                         |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | 멀티파트 복사       | 다른 객체를 한 파트로 복사             |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | 업로드된 파트 조회   | 특정 멀티파트 업로드 작업에서 업로드된 파트 조회   |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | 멀티파트 업로드 완료   | 전체 파일의 멀티파트 업로드 완료               |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | 멀티파트 업로드 중지 | 하나의 멀티파트 업로드 작업 중지 및 이미 업로드한 파트 삭제 |




## 간단한 작업

### 객체 리스트 조회

#### 기능 설명

버킷의 일부 또는 모든 객체를 조회합니다.

#### 메소드 프로토타입

```
list_objects(Bucket, Delimiter="", Marker="", MaxKeys=1000, Prefix="", EncodingType="", **kwargs)
```
#### 요청 예시1: 지정된 버킷의 모든 객체 나열

[//]: # ".cssg-snippet-get-all-objects"
```python
response = client.list_objects(Bucket='examplebucket-1250000000')
if 'Contents' in response:
    for content in response['Contents']:
        print(content['Key'])
# 참고: 버킷에 객체가 너무 많으면 한 번에 1000개의 객체만 반환되며, 여러 페이지로 나열됩니다(예시3 참고).
```

#### 요청 예시2: 특정 접두사 객체 나열

[//]: # ".cssg-snippet-get-prefix-objects"
```python
# 접두사가 folder인 객체 나열
response = client.list_objects(
    Bucket='examplebucket-1250000000',
    Prefix='folder' 
)

# folder1 디렉터리의 파일을 나열합니다. COS의 디렉터리는 ‘/’ 끝의 접두사 이름입니다.
response = client.list_objects(
    Bucket='examplebucket-1250000000',
    Prefix='folder1/' 
)
```

#### 요청 예시3: 페이지별 객체 나열

[//]: # ".cssg-snippet-get-objects-by-page"
```python
# 버킷의 객체를 페이지당 10개로 나눠 나열
marker = ""
while True:
    response = client.list_objects(
        Bucket='examplebucket-1250000000', Prefix='folder1/', Marker=marker, MaxKeys=10)
    if 'Contents' in response:
        for content in response['Contents']:
            print(content['Key'])

    if response['IsTruncated'] == 'false':
        break

    marker = response["NextMarker"]
```

#### 요청 예시4: 지정된 디렉터리의 객체 및 하위 디렉터리 나열

[//]: # ".cssg-snippet-get-files-and-subfolder"
```python
# folder1 디렉터리의 파일과 하위 디렉터리 나열
response = client.list_objects(
    Bucket='examplebucket-1250000000', Prefix='folder1/', Delimiter='/')
# 파일 목록 출력
if 'Contents' in response:
    for content in response['Contents']:
        print(content['Key'])
# 하위 디렉터리 출력
if 'CommonPrefixes' in response:
    for folder in response['CommonPrefixes']:
        print(folder['Prefix'])
```

#### 모든 매개변수 요청 예시

[//]: # ".cssg-snippet-get-bucket-with-delimiter"
```python
response = client.list_objects(
    Bucket='examplebucket-1250000000',
    Prefix='string',
    Delimiter='/',
    Marker='string',
    MaxKeys=100,
    EncodingType='url'
)
```
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   |유형 | 필수 입력 여부 |
| -------------- | -------------- |---------- | ----------- |
| Bucket   | 버킷 이름. BucketName-APPID로 구성  | String  | Yes|
| Prefix   |  기본값 null. 객체 키를 필터링해 prefix로 시작하는 객체와 매칭  | String  |  No|
| Delimiter   |   기본값 null. 세퍼레이터 설정(예: `/`을 설정해 가상 폴더화)  | String|  No|
| Marker   |  기본적으로 UTF-8 이진법 순서로 나열. 반환된 객체 리스트의 시작 위치 표시  | String  |  No|
| MaxKeys   | 반환되는 최대 객체 수. 기본값은 최대 1000개  | Int  |  No|
| EncodingType   |   기본적으로 인코딩하지 않으며, 반환값의 인코딩 방식을 규정. 옵션값: url  | String  | No|

#### 반환 결과 설명

가져온 객체의 메타 정보(dict 형식):

```python
{
    'MaxKeys': '1000', 
    'Prefix': 'string',
    'Delimiter': 'string',
    'Marker': 'string',
    'NextMarker': 'string',
    'Name': 'examplebucket-1250000000',  
    'IsTruncated': 'false'|'true',
    'EncodingType': 'url',
    'Contents':[
        {
            'ETag': '"a5b2e1cfb08d10f6523f7e6fbf3643d5"', 
            'StorageClass': 'STANDARD', 
            'Key': 'exampleobject',
            'Owner': {
                'DisplayName': '1250000000',
                'ID': '1250000000'
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

| 매개변수 이름   | 매개변수 설명   |유형 |
| -------------- | -------------- |---------- |
| MaxKeys   | 반환되는 최대 객체 수. 기본값은 최대 1000개  | String |
| Prefix   |  기본값 null. prefix로 시작하는 객체와 매칭 | String|
| Delimiter   |   기본값 null. 세퍼레이터 설정(예: `/`를 설정해 가상 폴더화)  | String|
| Marker   |  기본적으로 UTF-8 이진법 순서로 나열. 반환된 객체 리스트의 시작 위치 표시  | String  |
| NextMarker| IsTruncated가 true면 다음에 반환된 객체 리스트의 시작 위치 표시  | String  |
| Name   | 버킷 이름은 BucketName-APPID로 구성  | String  |
| IsTruncated   |  반환된 객체의 잘림 여부 표시  | String|
| EncodingType   |   기본적으로 인코딩하지 않으며, 반환값의 인코딩 방식을 규정. 옵션값: url  | String  | No|
|Contents | 'ETag', 'StorageClass', 'Key', 'Owner', 'LastModified', 'Size' 등의 정보를 포함한 모든 객체 메타데이터가 담긴 리스트|List|
|CommonPrefixes |Prefix로 시작하고 Delimiter로 끝나는 모든 객체를 동일한 클래스로 분류|List|

### 객체 및 이전 버전 리스트 조회 

#### 기능 설명

버킷의 일부 또는 모든 객체 및 이전 버전 정보를 조회합니다.

#### 메소드 프로토타입

```
list_objects_versions(Bucket, Prefix="", Delimiter="", KeyMarker="", VersionIdMarker="", MaxKeys=1000, EncodingType="", **kwargs)
```
#### 요청 예시

[//]: # ".cssg-snippet-list-objects-versioning"
```python
response = client.list_objects_versions(
    Bucket='examplebucket-1250000000',
    Prefix='string'
)
```

#### 모든 매개변수 요청 예시

[//]: # ".cssg-snippet-list-objects-versioning-next-page"
```python
response = client.list_objects_versions(
    Bucket='examplebucket-1250000000',
    Prefix='string',
    Delimiter='/',
    KeyMarker='string',
    VersionIdMarker='string',
    MaxKeys=100,
    EncodingType='url'
)
```
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   |유형 | 필수 입력 여부 |
| -------------- | -------------- |---------- | ----------- |
| Bucket   | 버킷 이름. BucketName-APPID로 구성  | String  | Yes|
| Prefix   |  기본값 null. 객체 키를 필터링해 prefix로 시작하는 객체와 매칭  | String  |  No|
| Delimiter   |   기본값 null. 세퍼레이터 설정(예: `/`을 설정해 가상 폴더화)  | String|  No|
| KeyMarker   |  기본적으로 UTF-8 이진법 순서로 나열. 반환된 객체 리스트의 key 시작 위치 표시  | String  |  No|
| VersionIdMarker|  기본적으로 UTF-8 이진법 순서로 나열. 반환된 객체 리스트의 VersionId 시작 위치 표시  | String  |  No|
| MaxKeys   | 반환되는 최대 객체 수. 기본값은 최대 1000개  | Int  |  No|
| EncodingType   |   기본적으로 인코딩하지 않으며, 반환값의 인코딩 방식을 규정. 옵션값: url  | String  | No|

#### 반환 결과 설명

가져온 객체의 메타 정보(dict 형식):

```python
{
    'MaxKeys': '1000', 
    'Prefix': 'string',
    'Delimiter': 'string',
    'KeyMarker': 'string',
    'VersionIdMarker': 'string',
    'NextKeyMarker': 'string',
    'NextVersionIdMarker': 'string',
    'Name': 'examplebucket-1250000000',  
    'IsTruncated': 'false'|'true',
    'EncodingType': 'url',
    'Version':[
        {
            'ETag': '"a5b2e1cfb08d10f6523f7e6fbf3643d5"', 
            'StorageClass': 'STANDARD', 
            'Key': 'exampleobject',
            'VersionId': 'string',
            'IsLatest': 'true'|'false',
            'Owner': {
                'DisplayName': '1250000000',
                'ID': '1250000000'
            }, 
            'LastModified': '2017-08-08T09:43:35.000Z', 
            'Size': '23'
        },
    ],
    'DeleteMarker': [
        {
            'Key': 'exampleobject',
            'VersionId': 'string',
            'IsLatest': 'true'|'false',
            'Owner': {
                'DisplayName': '1250000000',
                'ID': '1250000000'
            },
            'LastModified': '2017-08-08T09:43:35.000Z'
        },
    ],
    'CommonPrefixes':[
        {
            'Prefix': 'string'
        },
    ],
}
```

| 매개변수 이름   | 매개변수 설명   |유형 |
| -------------- | -------------- |---------- |
| MaxKeys   | 반환되는 최대 객체 수. 기본값은 최대 1000개  | String |
| Prefix   |  기본값 null. prefix로 시작하는 객체와 매칭 | String|
| Delimiter   |   기본값 null. 세퍼레이터 설정(예: `/`를 설정해 가상 폴더화)  | String|
| KeyMarker   |  기본적으로 UTF-8 이진법 순서로 나열. 반환된 객체 리스트 키의 시작 위치 표시  | String  |
| VersionIdMarker|  기본적으로 UTF-8 이진법 순서로 나열. 반환된 객체 리스트의 VersionId 시작 위치 표시  | String  |
| NextKeyMarker| IsTruncated가 true면 다음에 반환된 객체 리스트 키의 시작 위치 표시  | String  |
| NextVersionIdMarker| IsTruncated가 true면 다음에 반환된 객체 리스트의 VersionId 시작 위치 표시  | String  |
| Name   | 버킷 이름은 BucketName-APPID로 구성  | String  |
| IsTruncated   |  반환된 객체의 잘림 여부 표시  | String|
| EncodingType   |   기본적으로 인코딩하지 않으며, 반환값의 인코딩 방식을 규정. 옵션값: url  | String  | No|
|Version | 'ETag', 'StorageClass', 'Key', 'VersionId', 'IsLatest', 'Owner', 'LastModified', 'Size' 등의 정보를 포함한 여러 버전의 객체 메타데이터가 담긴 리스트|List|
|DeleteMarker| 'Key', 'VersionId', 'IsLatest', 'Owner', 'LastModified' 등의 정보를 포함한 모든 delete marker 객체 메타데이터가 담긴 리스트|List|
|CommonPrefixes |Prefix로 시작하고 Delimiter로 끝나는 모든 객체를 동일한 클래스로 분류|List|

### 객체 간편 업로드

#### 기능 설명

객체를 버킷에 업로드합니다(PUT Object).

#### 메소드 프로토타입

```
put_object(Bucket, Body, Key, **kwargs)
```
#### 요청 예시1: 파일 간편 업로드

[//]: # ".cssg-snippet-put-object"
```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
from qcloud_cos import CosServiceError
from qcloud_cos import CosClientError

import sys
import logging

logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# secret_id, secret_key, region 등을 포함한 사용자 속성을 설정합니다. Appid는 CosConfig에서 제거되었습니다. 매개변수 Bucket에 Appid를 포함시키십시오. Bucket은 BucketName-Appid로 구성됩니다.
secret_id = 'SecretId'     # 사용자의 SecretId로 대체합니다. CAM 콘솔에 로그인하여 확인 및 관리하십시오. https://console.cloud.tencent.com/cam/capi
secret_key ='SecretKey'   # 사용자의 SecretKey로 대체합니다. CAM 콘솔에 로그인하여 확인 및 관리하십시오. https://console.cloud.tencent.com/cam/capi
region = 'ap-beijing'      # 사용자의 region으로 대체합니다. 생성된 버킷이 속한 region은 콘솔에서 확인 가능합니다. https://console.cloud.tencent.com/cos5/bucket
                           # COS에서 지원되는 모든 region 목록은 다음을 참고하십시오. https://www.qcloud.com/document/product/436/6224
token = None                 # 영구 키를 사용하는 경우 token을 입력할 필요가 없으나, 임시 키를 사용하는 경우 입력해야 합니다. 임시 키 생성 및 사용 가이드는 다음을 참고하십시오. https://cloud.tencent.com/document/product/436/14048

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token)  # 설정 객체 획득
client = CosS3Client(config)

# 파일 스트림 간편 업로드
file_name = 'test.txt'
with open('test.txt', 'rb') as fp:
    response = client.put_object(
        Bucket='examplebucket-1250000000',  # Bucket은 BucketName-APPID로 구성
        Body=fp,
        Key=file_name,
        StorageClass='STANDARD',
        ContentType='text/html; charset=utf-8'
    )
    print(response['ETag'])

# 바이트 스트림 간편 업로드
response = client.put_object(
    Bucket='examplebucket-1250000000',
    Body=b'abcdefg',
    Key=file_name
)
print(response['ETag'])

# 로컬 경로 간편 업로드
response = client.put_object_from_local_file(
    Bucket='examplebucket-1250000000',
    LocalFilePath='local.txt',
    Key=file_name,
)
print(response['ETag'])

# HTTP 헤더 설정 간편 업로드
response = client.put_object(
    Bucket='examplebucket-1250000000',
    Body=b'test',
    Key=file_name,
    ContentType='text/html; charset=utf-8'
)
print(response['ETag'])

# 사용자 정의 헤더 설정 간편 업로드
response = client.put_object(
    Bucket='examplebucket-1250000000',
    Body=b'test',
    Key=file_name,
    Metadata={
        'x-cos-meta-key1': 'value1',
        'x-cos-meta-key2': 'value2'
    }
)
print(response['ETag'])
```
#### 요청 예시2: 디렉터리 생성
COS의 디렉터리는 '/'로 끝나는 특수 객체 이름입니다. Put Object 인터페이스를 호출하면 됩니다.

[//]: # ".cssg-snippet-put-object-diretory"
```python
# 디렉터리 생성
dir_to_create='path/to/create/dir/'
response = client.put_object(
    Bucket='examplebucket-1250000000',  # Bucket은 BucketName-APPID로 구성
    Key=dir_to_create,
    Body=b'',
)
print(response)
```
#### 요청 예시3: 지정 디렉터리에 객체 업로드

[//]: # ".cssg-snippet-put-object-comp"
```python
#'/'로 구분되는 객체 이름을 업로드하면 파일이 포함된 폴더를 자동으로 생성합니다. 해당 폴더에 새로운 파일을 추가할 경우 COS에 파일 업로드 시 Key를 해당 디렉터리 접두사로 입력하기만 하면 됩니다.
dir_name = 'path/to/dir/'
file_name = 'test.txt'
object_key = dir_name + file_name
with open('test.txt', 'rb') as fp:
    response = client.put_object(
        Bucket='examplebucket-1250000000',  # Bucket은 BucketName-APPID로 구성
        Body=fp,
        Key=object_key,
        StorageClass='STANDARD',
        ContentType='text/html; charset=utf-8'
    )
    print(response['ETag'])
```
#### 요청 예시4: 업로드 속도 제한
TrafficLimit 매개변수 설정을 사용하여 업로드 속도를 제한합니다. 단위: bit/s, 속도 제한 설정 범위: 819200 - 838860800, 즉 100KB/s - 100MB/s.

[//]: # ".cssg-snippet-put-object-by-limit"
```python
with open('test.bin', 'rb') as fp:
    response = client.put_object(
        Bucket='examplebucket-1250000000',  # Bucket은 BucketName-APPID로 구성
        Key='exampleobject',
        Body=fp,
        TrafficLimit='819200'
    )
    print(response['ETag'])
```

#### 모든 매개변수 요청 예시
[//]: # ".cssg-snippet-put-object-comp"
```python
response = client.put_object(
    Bucket='examplebucket-1250000000',
    Body=b'bytes'|file,
    Key='exampleobject',
    EnableMD5=False|True,
    ACL='private'|'public-read',  # 이 매개변수는 ACL이 1000개로 제한되어 있으니 신중히 사용하십시오.
    GrantFullControl='string',
    GrantRead='string',
    StorageClass='STANDARD'|'STANDARD_IA'|'ARCHIVE',
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
    },
    TrafficLimit='1048576'
)
```
#### 매개변수 설명


| 매개변수 이름   | 매개변수 설명   |유형 | 필수 입력 여부 |
| -------------- | -------------- |---------- | ----------- |
|  Bucket  | 버킷 이름. BucketName-APPID로 구성 | String |  Yes |
|  Body  | 업로드하는 객체의 콘텐츠. 파일 스트림 또는 바이트 스트림이 될 수 있음 |  file/bytes |  Yes |
|  Key  | 객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg임 | String |  Yes |
| EnableMD5 | SDK의 Content-MD5 계산 여부. 기본적으로 비활성화 상태이며, 활성화 시 업로드 시간 증가|Bool | No|
| ACL |객체 ACL 설정. 예: 'private', 'public-read' |String| No|
| GrantFullControl |권한을 부여받은 계정에 모든 권한 부여. 형식: `id="OwnerUin"`|String|No|
|GrantRead |권한을 부여받은 계정에 읽기 권한 부여. 형식: `id="OwnerUin"`  |String|No|
|  StorageClass  |  객체의 스토리지 유형 설정. STANDARD, STANDARD_IA, ARCHIVE가 있으며, 기본값은 STANDARD. 스토리지 유형에 대한 자세한 내용은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925) 참고 | String |   No |
|  Expires  | Expires 설정 | String|  No |
|  CacheControl  |  캐시 정책. Cache-Control 설정 | String |   No |
|  ContentType  | 콘텐츠 유형. Content-Type 설정 |String |   No |
|  ContentDisposition  |  객체 이름. Content-Disposition 설정 | String |   No |
|  ContentEncoding  |  인코딩 형식. Content-Encoding 설정 | String |   No |
|  ContentLanguage  |  언어 유형. Content-Language 설정 | String |   No |
|  ContentLength  | 전송 길이 설정 | String |   No |
|  ContentMD5  | 검사에 사용할 업로드 객체의 MD5 값 설정 | String |   No |
|  Metadata | 사용자 정의 객체 메타데이터. 반드시 x-cos-meta로 시작해야 하며, 그렇지 않을 경우 무시됨 | Dict |  No |
|  TrafficLimit | 단일 링크의 제한 속도. 단위는 bit/s이며 설정 범위는 819200-838860800, 즉 100KB/s-100MB/s로 설정| String |  No |

#### 반환 결과 설명
업로드한 객체의 속성(dict 유형):

```python
{
    'ETag': 'string',
    'x-cos-version-id': 'string'
}
```


| 매개변수 이름   | 매개변수 설명   |유형 |
| -------------- | -------------- |---------- |
|  ETag   |  업로드한 객체의 MD5 값  | String  |
|  x-cos-version-id   |  버전 제어 활성화 후 객체의 버전 넘버 | String  |



### 객체 메타데이터 조회

#### 기능 설명

객체의 메타데이터 정보를 조회합니다(HEAD Object).

#### 메소드 프로토타입

```
head_object(Bucket, Key, **kwargs)
```
#### 요청 예시

[//]: # ".cssg-snippet-head-object"
```python
response = client.head_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject'
)
```
#### 모든 매개변수 요청 예시

```python
response = client.head_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    VersionId='string',
    IfModifiedSince='Wed, 28 Oct 2020 20:30:00 GMT',
)
```
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   |유형 | 필수 입력 여부 |
| -------------- | -------------- |---------- | ----------- |
| Bucket   | 버킷 이름은 BucketName-APPID로 구성  | String  |  Yes |
| Key   |  객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg임  |String  | Yes |
| VersionId   | 버전 제어 활성화 후 지정 객체의 버전  | String  | No |
| IfModifiedSince   | 지정 시간 이후 수정될 경우에만 반환. 시간 형식: GMT | String  | No |

#### 반환 결과 설명

가져온 객체의 메타 정보(dict 형식):

```python
{
    'ETag': '"9a4802d5c99dafe1c04da0a8e7e166bf"',
    'Last-Modified': 'Wed, 28 Oct 2014 20:30:00 GMT',
    'Cache-Control': 'max-age=1000000',
    'Content-Type': 'application/octet-stream',
    'Content-Disposition': 'attachment; filename="filename.jpg"',
    'Content-Encoding': 'gzip',
    'Content-Language': 'zh-cn',
    'Content-Length': '16807',
    'Expires': 'Wed, 28 Oct 2019 20:30:00 GMT',
    'x-cos-meta-test': 'test',
    'x-cos-version-id': 'MTg0NDUxODMzMTMwMDM2Njc1ODA',
    'x-cos-request-id': 'NTg3NzQ3ZmVfYmRjMzVfMzE5N182NzczMQ=='
}
```


| 매개변수 이름   | 매개변수 설명   |유형 |
| -------------- | -------------- |---------- |
| ETag  |  멀티파트 업로드 시 해당 값은 객체 콘텐츠의 MD5 검사값이 아니므로, 객체 고유성 검사에만 사용 가능 |String|
| Last-Modified | 객체 최종 수정 시간| String|
|  Cache-Control  |  캐시 정책. 표준 HTTP 헤더| String |
|  Content-Type  | 콘텐츠 유형. 표준 HTTP 헤더| String |
|  Content-Disposition  |  파일 이름. 표준 HTTP 헤더| String |
|  Content-Encoding  |  인코딩 포맷. 표준 HTTP 헤더| String |
|  Content-Language  |  언어 유형. 표준 HTTP 헤더| String |
|  Content-Length  | 객체의 크기 | String |
|  Expires | 캐시 만료 시간. 표준 HTTP 헤더| String |
|  x-cos-meta-* | 사용자 정의 객체 메타데이터. 반드시 x-cos-meta로 시작해야 하며, 그렇지 않을 경우 무시됨 | String |
|  x-cos-version-id   |  버전 제어 활성화 후 객체의 버전 넘버 | String  |


### 객체 다운로드

#### 기능 설명

하나의 객체를 로컬에 다운로드합니다(GET Object).

#### 메소드 프로토타입

```
 get_object(Bucket, Key, **kwargs)
```
#### 요청 예시1: 객체 다운로드

[//]: #	".cssg-snippet-get-object"
```python
response = client.get_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject'
)
response['Body'].get_stream_to_file('exampleobject')
```
#### 요청 예시2: 다운로드 속도 제한

[//]: # ".cssg-snippet-get-object-by-limit"
```python
response = client.get_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    TrafficLimit='819200'
)
response['Body'].get_stream_to_file('exampleobject')
```
#### 요청 예시3: 객체 일부 내용 다운로드

[//]: # ".cssg-snippet-get-object-by-range"
```python
response = client.get_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Range='bytes=0-100'
)
response['Body'].get_stream_to_file('exampleobject')
```
#### 모든 매개변수 요청 예시

[//]: #	".cssg-snippet-get-object"
```python
response = client.get_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Range='string',
    IfMatch='"9a4802d5c99dafe1c04da0a8e7e166bf"',
    IfModifiedSince='Wed, 28 Oct 2014 20:30:00 GMT',
    IfNoneMatch='"9a4802d5c99dafe1c04da0a8e7e166bf"',
    IfUnmodifiedSince='Wed, 28 Oct 2014 20:30:00 GMT',
    ResponseCacheControl='string',
    ResponseContentDisposition='string',
    ResponseContentEncoding='string',
    ResponseContentLanguage='string',
    ResponseContentType='string',
    ResponseExpires='string',
    VersionId='string',
    TrafficLimit='819200'
)
```
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   |유형 | 필수 입력 여부 |
| -------------- | -------------- |---------- | ----------- |
|  Bucket  | 버킷 이름. BucketName-APPID로 구성 | String  |  Yes |
|  Key  |  객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg임 | String  | Yes |
|  Range  |  다운로드할 객체의 범위 설정. 형식: bytes=first-last  | String  |  No |
|  IfMatch  |  ETag가 지정된 콘텐츠와 일치해야 반환 |String  | No |
|  IfModifiedSince  |   지정 시간 이후 수정될 경우에만 반환. 시간 형식: GMT | String  | No |
|  IfNoneMatch  |  ETag가 지정 콘텐츠와 불일치 시 반환 | String  | No |
|  IfUnmodifiedSince  |  객체 수정 시간이 지정 시간보다 이르거나 같을 경우에만 반환. 시간 형식: GMT| String  | No|
|  ResponseCacheControl  |  응답 헤더의 Cache-Control 설정 | String  | No |
|  ResponseContentDisposition  |  응답 헤더의 Content-Disposition 설정 | String  | No |
|  ResponseContentEncoding  |   응답 헤더의 Content-Encoding 설정 | String  | No |
|  ResponseContentLanguage  |  응답 헤더의 Content-Language 설정 | String  | No |
|  ResponseContentType  |   응답 헤더의 Content-Type 설정 | String  | No |
|  ResponseExpires  |응답 헤더의 Expires 설정 |   String  | No |
|  VersionId  | 다운로드할 객체 버전 지정 |  String  | No |
|  TrafficLimit | 단일 링크 제한 속도. 단위는 bit/s이며 설정 범위는 819200-838860800, 즉 100KB/s-100MB/s. 고급 인터페이스는 단일 스레드의 속도를 제한| String |  No |

#### 반환 결과 설명

다운로드한 객체의 Body 및 메타 정보(dict 유형):

```python
{
    'Body': StreamBody(),
    'ETag': '"9a4802d5c99dafe1c04da0a8e7e166bf"',
    'Last-Modified': 'Wed, 28 Oct 2014 20:30:00 GMT',
    'Accept-Ranges': 'bytes',
    'Content-Range': 'bytes 0-16086/16087',
    'Cache-Control': 'max-age=1000000',
    'Content-Type': 'application/octet-stream',
    'Content-Disposition': 'attachment; filename="filename.jpg"',
    'Content-Encoding': 'gzip',
    'Content-Language': 'zh-cn',
    'Content-Length': '16807',
    'Expires': 'Wed, 28 Oct 2019 20:30:00 GMT',
    'x-cos-meta-test': 'test',
    'x-cos-version-id': 'MTg0NDUxODMzMTMwMDM2Njc1ODA',
    'x-cos-request-id': 'NTg3NzQ3ZmVfYmRjMzVfMzE5N182NzczMQ=='
}
```

<table>
   <tr>
      <th>매개변수 이름</th>
      <th>매개변수 설명</th>
      <th>유형</th>
   </tr>
   <tr>
      <td>Body</td>
      <td>객체 콘텐츠 다운로드. get_raw_stream() 메소드로 파일 스트림을 얻고, get_stream_to_file(local_file_path) 메소드로 객체 콘텐츠를 지정 로컬 파일에 다운로드</td>
      <td>StreamBody</td>
   </tr>
   <tr>
      <td>ETag</td>
      <td>객체의 MD5 값</td>
      <td>String</td>
   </tr>
   <tr>
      <td>Last-Modified</td>
      <td>객체 최종 수정 시간</td>
      <td>String</td>
   </tr>
   <tr>
      <td nowrap="nowrap">Accept-Ranges</td>
      <td>범위 단위. 표준 HTTP 헤더</td>
      <td>String</td>
   </tr>
   <tr>
      <td>Content-Range</td>
      <td>콘텐츠 범위. 표준 HTTP 헤더</td>
      <td>String</td>
   </tr>
   <tr>
      <td>Cache-Control</td>
      <td>캐시 정책. 표준 HTTP 헤더</td>
      <td>String</td>
   </tr>
   <tr>
      <td>Content-Type</td>
      <td>콘텐츠 유형. 표준 HTTP 헤더</td>
      <td>String</td>
   </tr>
   <tr>
      <td nowrap="nowrap">Content-Disposition</td>
      <td>파일 이름. 표준 HTTP 헤더</td>
      <td>String</td>
   </tr>
   <tr>
      <td>Content-Encoding</td>
      <td>인코딩 포맷. 표준 HTTP 헤더</td>
      <td>String</td>
   </tr>
   <tr>
      <td>Content-Language</td>
      <td>언어 유형. 표준 HTTP 헤더</td>
      <td>String</td>
   </tr>
   <tr>
      <td>Content-Length</td>
      <td>객체 크기</td>
      <td>String</td>
   </tr>
   <tr>
      <td>Expires</td>
      <td>캐시 만료 시간. 표준 HTTP 헤더</td>
      <td>String</td>
   </tr>
   <tr>
      <td>x-cos-meta-*</td>
      <td>사용자 정의 객체 메타데이터. 반드시 x-cos-meta로 시작해야 하며, 그렇지 않을 경우 무시됨</td>
      <td>String</td>
   </tr>
   <tr>
      <td>x-cos-version-id</td>
      <td>버전 제어 활성화 후 객체의 버전 넘버</td>
      <td>String</td>
   </tr>
</table>



### 객체 복사 설정

#### 기능 설명

타깃 경로에 파일을 복사합니다(PUT Object - Copy).

#### 메소드 프로토타입

```
copy_object(Bucket, Key, CopySource, CopyStatus='Copy', **kwargs)
```
#### 요청 예시1: 객체 복사
소스와 타깃은 서로 다른 객체이며, 새로운 타깃 객체가 생성되면, 타깃 객체는 소스 객체의 메타데이터 정보를 복사할 수 있습니다.

[//]: # ".cssg-snippet-copy-object"
```python
response = client.copy_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    CopySource={
        'Bucket': 'sourcebucket-1250000000', 
        'Key': 'exampleobject', 
        'Region': 'ap-guangzhou'
    }
)
```
#### 요청 예시2: 객체 메타데이터 수정
소스와 타깃은 동일한 객체이며 CopyStatus는 Replaced로 설정합니다. 헤더 필드를 통해 객체의 메타데이터를 수정할 수 있습니다.

[//]: # ".cssg-snippet-copy-object-metadata"
```python
response = client.copy_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    CopySource={
        'Bucket': 'sourcebucket-1250000000', 
        'Key': 'exampleobject', 
        'Region': 'ap-guangzhou'
    },
    CopyStatus='Replaced', 
    ContentType='text/plain', # 객체 ContentType 수정
    Metadata={'x-cos-meta-key1': 'value1', 'x-cos-meta-key2': 'value2'} # 사용자 정의 메타데이터 수정
)
```
#### 요청 예시3: 객체 스토리지 유형 수정
소스와 타깃은 동일한 객체이며 CopyStatus는 Replaced로 설정합니다. StorageClass 매개변수를 통해 객체의 스토리지 유형을 수정할 수 있습니다.

[//]: # ".cssg-snippet-copy-object-storage-class"
```python
response = client.copy_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    CopySource={
        'Bucket': 'examplebucket-1250000000', 
        'Key': 'exampleobject', 
        'Region': 'ap-guangzhou'
    },
    CopyStatus='Replaced', 
    StorageClass='STANDARD_IA' # 표준IA 스토리지로 수정
)
```
#### 모든 매개변수 요청 예시

```python
response = client.copy_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    CopySource={
        'Bucket': 'sourcebucket-1250000000', 
        'Key': 'exampleobject', 
        'Region': 'ap-guangzhou',
        'VersionId': 'string'
    },
    CopyStatus='Copy'|'Replaced',
    ACL='private'|'public-read',
    GrantFullControl='string',
    GrantRead='string',
    StorageClass='STANDARD'|'STANDARD_IA',
    Expires='string',
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

| 매개변수 이름   | 매개변수 설명   |유형 | 필수 입력 여부 |
| -------------- | -------------- |---------- | ----------- |
|  Bucket  | 버킷 이름은 BucketName-APPID로 구성 | String|  Yes |
|  Key  |  객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg임 | String  | Yes |
|  CopySource  | Bucket, Key, Region, VersionId를 포함한 원본 객체의 경로 복사 |  Dict | Yes |
|  CopyStatus  |  선택값은 Copy와 Replaced. Copy로 설정하는 경우 설정된 사용자 메타데이터 정보를 무시하고 바로 복사. Replaced로 설정하는 경우 설정된 메타정보에 따라 메타데이터 수정. 타깃 경로와 소스 경로가 같은 경우 반드시 Replaced로 설정 필요 | String| Yes |
| ACL |객체 ACL 설정. 예: private, public-read |String| No|
| GrantFullControl |지정 계정에 객체에 대한 모든 권한 부여. 형식: `id="OwnerUin"` |String|No|
|GrantRead |지정 계정에 객체의 읽기 권한 부여. 형식: `id="OwnerUin"`|String|No|
|  StorageClass  |  객체의 스토리지 유형 설정. STANDARD, STANDARD_IA가 있으며, 기본값은 STANDARD. | String|  No |
|  Expires  | Expires 설정 | String| No |
|  CacheControl  | 캐시 정책. Cache-Control 설정 | String|  No |
|  ContentType  | 콘텐츠 유형. Content-Type 설정 | String |  No |
|  ContentDisposition  |  파일 이름. Content-Disposition 설정 | String|  No |
|  ContentEncoding  | 인코딩 포맷. Content-Encoding 설정 | String|  No |
|  ContentLanguage  |  언어 유형. Content-Language 설정 | String|  No |
|  Metadata |사용자 정의 객체 메타데이터 | Dict |  No |


#### 반환 결과 설명
업로드한 객체의 속성(dict 유형):

```python
{
    'ETag': 'string',
    'LastModified': 'string',
    'VersionId': 'string',
    'x-cos-copy-source-version-id': 'string'
}
```

| 매개변수 이름   | 매개변수 설명   |유형 |
| -------------- | -------------- |---------- |
| ETag |객체의 MD5 값 복사|String|
| LastModified | 객체의 마지막 수정 시간 복사|String|
| VersionId | 버전 제어 활성화 후 타깃 객체의 버전 넘버 | String |
| x-cos-copy-source-version-id | 원본 객체의 버전 넘버 | String |


### 단일 객체 삭제

#### 기능 설명

지정 객체를 삭제합니다(DELETE Object).

#### 메소드 프로토타입

```
delete_object(Bucket, Key, **kwargs)
```
#### 요청 예시1: 단일 객체 삭제

[//]: # ".cssg-snippet-delete-object"
```python
response = client.delete_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject'
)
```

#### 요청 예시2: 디렉터리 삭제

COS에서 디렉터리는 경로가 ‘/’로 끝나는 특수 object입니다. 직접 Delete Object 인터페이스를 호출하여 디렉터리를 삭제할 수 있습니다.

[//]: # ".cssg-snippet-delete-object"
```python
try:
    to_delete_dir='path/to/delete/dir/'
    response = client.delete_object(
        Bucket='examplebucket-1250000000',
        Key=to_delete_dir,
    )
    print(response)
except CosServiceError as e:
    print(e.get_status_code())
```

#### 요청 예시3: 접두사 일괄 삭제

[//]: # ".cssg-snippet-delete-multi-object"
```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
from qcloud_cos import CosServiceError
from qcloud_cos import CosClientError

import sys
import os
import logging

# secret_id, secret_key, region 등을 포함한 사용자 속성을 설정합니다. Appid는 CosConfig에서 제거되었습니다. 매개변수 Bucket에 Appid를 포함시키십시오. Bucket은 BucketName-Appid로 구성됩니다.
secret_id = 'SecretId'     # 사용자의 SecretId로 대체합니다. CAM 콘솔에 로그인하여 확인 및 관리하십시오. https://console.cloud.tencent.com/cam/capi
secret_key ='SecretKey'   # 사용자의 SecretKey로 대체합니다. CAM 콘솔에 로그인하여 확인 및 관리하십시오. https://console.cloud.tencent.com/cam/capi
region = 'ap-beijing'      # 사용자의 region으로 대체합니다. 생성된 버킷이 속한 region은 콘솔에서 확인 가능합니다. https://console.cloud.tencent.com/cos5/bucket
                           # COS에서 지원되는 모든 region 목록은 다음을 참고하십시오. https://www.qcloud.com/document/product/436/6224
token = None                 # 영구 키를 사용하는 경우 token을 입력할 필요가 없으나, 임시 키를 사용하는 경우 입력해야 합니다. 임시 키 생성 및 사용 가이드는 다음을 참고하십시오. https://cloud.tencent.com/document/product/436/14048

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token)  # 설정 객체 획득
client = CosS3Client(config)

# 지정 접두사(prefix)가 있는 파일 삭제
bucket = 'examplebucket-1250000000'
is_over = False
marker = ''
prefix = 'root/logs'
while not is_over:
    try:
        response = client.list_objects(Bucket=bucket, Prefix=prefix, Marker=marker)
        if response['Contents']:
            for content in response['Contents']:
                print("delete object: ", content['Key'])
                client.delete_object(Bucket=bucket, Key=content['Key'])

            if response['IsTruncated'] == 'false':
                is_over = True
                marker = response['Marker']
    except CosServiceError as e:
        print(e.get_origin_msg())
        print(e.get_digest_msg())
        print(e.get_status_code())
        print(e.get_error_code())
        print(e.get_error_msg())
        print(e.get_resource_location())
        print(e.get_trace_id())
        print(e.get_request_id())
        break
```

#### 모든 매개변수 요청 예시

```python
response = client.delete_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    VersionId='string',
)
```
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   |유형 | 필수 입력 여부 |
| -------------- | -------------- |---------- | ----------- |
| Bucket  |버킷 이름은 BucketName-APPID로 구성 |  String |  Yes |
|  Key  |  객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg임 | String  | Yes |
| VersionId   | 버전 제어 활성화 후 지정 객체의 버전  | String  | No |

#### 반환 결과 설명

삭제한 객체의 정보(dict 유형):

```python
{
    'x-cos-version-id': 'string',
    'x-cos-delete-marker': 'true'|'false',
}
```

| 매개변수 이름   | 매개변수 설명   |유형 |
| -------------- | -------------- |---------- |
| x-cos-version-id | 삭제한 객체의 버전 넘버 | String |
| x-cos-delete-marker | 삭제한 객체가 delete marker인지 표시| String |



### 다수의 객체 삭제

#### 기능 설명

다수의 지정 객체를 삭제합니다(DELETE Multiple Objects).

#### 메소드 프로토타입

```
delete_objects(Bucket, Delete={}, **kwargs)
```
#### 요청 예시

[//]: # ".cssg-snippet-delete-multi-object"
```python
response = client.delete_objects(
    Bucket='examplebucket-1250000000',
    Delete={
        'Object': [
            {
                'Key': 'exampleobject1'
            },
            {
                'Key': 'exampleobject2'
            }
        ]
    }
)
```
#### 모든 매개변수 요청 예시

```python
response = client.delete_objects(
    Bucket='examplebucket-1250000000',
    Delete={
        'Object': [
            {
                'Key': 'exampleobject1',
                'VersionId': 'string'
            },
            {
                'Key': 'exampleobject2',
                'VersionId': 'string'
            },
        ],
        'Quiet': 'true'|'false'
    }
)
```

#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   |유형 | 필수 입력 여부 |
| -------------- | -------------- |---------- | ----------- |
| Bucket  | 버킷 이름. BucketName-APPID로 구성 | String |  Yes |
| Delete  | 이번에 삭제된 반환 결과 방식과 타깃 Object 설명 | Dict | Yes |
| Object  | 삭제 예정인 타깃 Object 정보 설명 | List | Yes |
| Key     | 객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg임| String|No|
| VersionId | 버전 제어 활성화 후 타깃 객체의 버전 넘버 | String |No|
| Quiet   |삭제 반환 결과 방식 지정. true, false 중 선택 가능. 기본값은 false. true로 설정할 경우 실패 오류 정보만 반환. false로 설정할 경우 성공과 실패 정보를 모두 반환|String|No|

#### 반환 결과 설명
객체 일괄 삭제 결과(dict 유형):
```python
{
    'Deleted': [
        {
            'Key': 'string',
            'VersionId': 'string',
            'DeleteMarker': 'true'|'false',
            'DeleteMarkerVersionId': 'string'
        },
        {
            'Key': 'string',
        },
    ],
    'Error': [
        {
            'Key': 'string',
            'VersionId': 'string',
            'Code': 'string',
            'Message': 'string'
        },
    ]
}
```

| 매개변수 이름   | 매개변수 설명   |유형 |
| -------------- | -------------- |---------- |
| Deleted  |  삭제 성공한 Object 정보|  List |
| Key     | 삭제 성공한 Object 경로| String|
| VersionId     | 삭제 성공한 Object 버전 넘버| String|
| DeleteMarker     | 삭제 성공한 Object의 delete marker 여부| String|
| DeleteMarkerVersionId | 삭제 성공한 Object의 delete marker 버전 넘버| String|
| Error  |  삭제 실패한 Object 정보| List |
| Key     | 삭제 실패한 Object 경로| String|
| VersionId     | 삭제 실패한 Object 버전 넘버| String|
| Code     | 삭제 실패한 Object의 해당 에러 코드| String|
| Message   |삭제 실패한 Object의 해당 오류 정보| String|



### 보관된 객체 복구 

#### 기능 설명

아카이브 유형의 객체를 검색하여 액세스합니다(POST Object restore).

#### 메소드 프로토타입

```
restore_object(Bucket, Key, RestoreRequest={}, **kwargs)
```
#### 요청 예시

[//]: # ".cssg-snippet-restore-object"
```python
response = client.restore_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    RestoreRequest={
        'Days': 100,
        'CASJobParameters': {
            'Tier': 'Standard'
        }
    }
)
```
#### 모든 매개변수 요청 예시

```python
response = client.restore_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    RestoreRequest={
        'Days': 100,
        'CASJobParameters': {
            'Tier': 'Expedited'|'Standard'|'Bulk'
        }
    }
)
```
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   |유형 | 필수 입력 여부 |
| -------------- | -------------- |---------- | ----------- |
|Bucket|버킷 이름. BucketName-APPID로 구성|String| Yes|
|key |객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg임|String|Yes|
|RestoreRequest| 검색한 임시 객체의 규칙| Dict|Yes|
|Days| 임시 객체의 만료 시간| Int|Yes|
|CASJobParameters| 복구 유형의 설정 정보| Dict|No|
|Tier| 복구 객체의 모드. CAS 유형의 데이터를 복구할 경우 Expedited, Standard, Bulk 세 가지 모드 선택 가능. DEEP ARCHIVE 유형의 데이터를 복구할 경우 Standard, Bulk 중 선택 가능| String|No|

#### 반환 결과 설명
해당 메소드의 반환값은 None입니다.


### 객체 콘텐츠 인덱스 

#### 기능 설명

지정 객체에서 콘텐츠를 인덱스합니다(SELECT Object content).

#### 메소드 프로토타입

```
select_object_content(Bucket, Key, Expression, ExpressionType, InputSerialization, OutputSerialization, RequestProgress=None, **kwargs)
```
#### 요청 예시

[//]: # ".cssg-snippet-select-object-content"
```python
response = client.select_object_content(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Expression='Select * from COSObject',
    ExpressionType='SQL',
    InputSerialization={
        'CompressionType': 'NONE',
        'JSON': {
            'Type': 'LINES'
        }
    },
    OutputSerialization={
        'CSV': {
            'RecordDelimiter': '\n'
        }
    }
)
```
#### 모든 매개변수 요청 예시

```python
response = client.select_object_content(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Expression='Select * from COSObject',
    ExpressionType='SQL',
    InputSerialization={
        'CompressionType': 'GZIP',
        'JSON': {
            'Type': 'LINES'
        }
    },
    OutputSerialization={
        'CSV': {
            'RecordDelimiter': '\n'
        }
    },
    RequestProgress={
        'Enabled': 'FALSE'
    }
)
```
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   |유형 | 필수 입력 여부 |
| -------------- | -------------- |---------- | ----------- |
|Bucket|버킷 이름. BucketName-APPID로 구성|String| Yes|
|key |객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg|String|Yes|
|Expression|SQL 표현식. 요청할 인덱스 작업을 나타냄| String|Yes|
|ExpressionType| 표현식 유형. 본 항목은 확장 항목으로 현재 SQL 표현식과 SQL 매개변수만 지원| String|Yes|
|InputSerialization| 인덱스 할 객체의 형식. 자세한 내용은 [요청 예시](https://intl.cloud.tencent.com/document/product/436/32360#.E8.AF.B7.E6.B1.82) 참고| Dict|Yes|
|OutputSerialization| 인덱스 결과의 출력 형식. 자세한 내용은 [요청 예시](https://intl.cloud.tencent.com/document/product/436/32360#.E8.AF.B7.E6.B1.82) 참고| Dict|Yes|
|RequestProgress| QueryProgress 쿼리 진행률 정보 반환 여부. COS Select를 선택할 경우 주기적으로 쿼리 진행률 반환| Dict|No|

#### 반환 결과 설명
객체의 Body 및 메타 정보(dict 유형):
```python
{
    'Body': EventStream(),
    'ETag': '"9a4802d5c99dafe1c04da0a8e7e166bf"',
    'Last-Modified': 'Wed, 28 Oct 2014 20:30:00 GMT',
    'Accept-Ranges': 'bytes',
    'Content-Range': 'bytes 0-16086/16087',
    'Cache-Control': 'max-age=1000000',
    'Content-Type': 'application/octet-stream',
    'Content-Disposition': 'attachment; filename="filename.jpg"',
    'Content-Encoding': 'gzip',
    'Content-Language': 'zh-cn',
    'Content-Length': '16807',
    'Expires': 'Wed, 28 Oct 2019 20:30:00 GMT',
    'x-cos-meta-test': 'test',
    'x-cos-version-id': 'MTg0NDUxODMzMTMwMDM2Njc1ODA',
    'x-cos-request-id': 'NTg3NzQ3ZmVfYmRjMzVfMzE5N182NzczMQ=='
}
```

### 객체 추가 업로드 

#### 기능 설명

객체를 멀티파트에 추가하는 방식으로 버킷(APPEND object)에 업로드합니다.

#### 메소드 프로토타입

```
append_object(Bucket, Key, Position, Data, **kwargs)
```
#### 요청 예시

[//]: # ".cssg-snippet-append-object"
```python
response = client.append_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Position=0,
    Data=b'b'*1024*1024
)
```
#### 모든 매개변수 요청 예시

```python
response = client.append_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Position=0,
    Data=b'bytes'|file
)
```
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   |유형 | 필수 입력 여부 |
| -------------- | -------------- |---------- | ----------- |
|Bucket|버킷 이름. BucketName-APPID로 구성|String| Yes|
|key |객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg|String|Yes|
|Position|추가 작업의 시작점으로 단위는 바이트입니다. 첫 번째 추가의 경우 Position=0을 설정하고 후속 추가의 경우 Position을 현재 Object의 content-length로 설정합니다| Int|Yes|
|data|파트의 컨텐츠 업로드. 로컬 파일 스트림 또는 입력 스트림| file/bytes|Yes|

#### 반환 결과 설명
다음에 추가될 위치를 포함한 추가 업로드 후의 객체 속성, dict 유형.
```python
{
    'ETag': '"9a4802d5c99dafe1c04da0a8e7e166bf"',
    'x-cos-next-append-position': '12',
    'x-cos-request-id': 'NjEwN2Q0ZGZfMWNhZjU4NjRfMzM1M19hNzQzYjc2'
}
```

## 멀티파트 작업
다음은 객체의 멀티파트 업로드 작업 내용입니다.

- 객체 멀티파트 업로드: 멀티파트 업로드를 초기화하고 멀티파트를 업로드하면 완료됩니다.
- 멀티파트 이어 보내기: 업로드된 멀티파트를 조회하고 멀티파트를 업로드하면 완료됩니다.
- 업로드된 파트를 삭제합니다.

### 멀티파트 업로드 조회

#### 기능 설명

지정 버킷에서 진행 중인 멀티파트 업로드 정보를 조회합니다(List Multipart Uploads).

#### 메소드 프로토타입

```
list_multipart_uploads(Bucket, Prefix="", Delimiter="", KeyMarker="", UploadIdMarker="", MaxUploads=1000, EncodingType="", **kwargs)
```
#### 요청 예시

[//]: # ".cssg-snippet-list-multi-upload"
```python
response = client.list_multipart_uploads(
    Bucket='examplebucket-1250000000',
    Prefix='dir'
)
```
#### 모든 매개변수 요청 예시

```python
response = client.list_multipart_uploads(
    Bucket='examplebucket-1250000000',
    Prefix='string',
    Delimiter='string',
    KeyMarker='string',
    UploadIdMarker='string',
    MaxUploads=100,
    EncodingType='url'
)
```
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   |유형 | 필수 입력 여부 |
| -------------- | -------------- |---------- | ----------- |
| Bucket   | 버킷 이름. BucketName-APPID로 구성  | String  | Yes|
| Prefix   |  기본값 null. 멀티파트 업로드 키를 필터링해 prefix로 시작하는 멀티파트 업로드와 매칭  | String  |  No|
| Delimiter   |   기본값 null. 세퍼레이터 설정| String|  No|
| KeyMarker   |  UploadIdMarker와 함께 사용하며, 멀티파트 업로드 시작 위치 표시  | String  |  No|
| UploadIdMarker   |  KeyMarker와 함께 사용하며, 멀티파트 업로드 시작 위치 표시. KeyMarker를 지정하지 않으면 UploadIdMarker가 무시됨| String  |  No|
| MaxUploads   |반환되는 멀티파트 업로드 최대 수. 기본값은 최대 1000개  | Int  |  No|
| EncodingType   |   기본적으로 인코딩하지 않으며, 반환값의 인코딩 방식을 규정. 옵션값: url  | String  | No|

#### 반환 결과 설명

멀티파트 업로드 정보 가져오기(dict 유형):

```python
{
    'Bucket': 'examplebucket-1250000000',
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

| 매개변수 이름   | 매개변수 설명   |유형 |
| -------------- | -------------- |---------- |
| Bucket   | 버킷 이름. BucketName-APPID로 구성  | String  |
| Prefix   |  기본값 null. 멀티파트 업로드 키를 필터링해 prefix로 시작하는 멀티파트 업로드와 매칭  | String  |
| Delimiter   |  기본값 null. 세퍼레이터 설정| String|
| KeyMarker   |  UploadIdMarker와 함께 사용하며, 멀티파트 업로드의 key 시작 위치 표시   | String  |
| UploadIdMarker   |  KeyMarker와 함께 사용하며, 멀티파트 업로드의 uploadId 시작 위치 표시. KeyMarker를 지정하지 않으면 UploadIdMarker가 무시됨| String  |
| NextKeyMarker   |  IsTruncated가 true면 다음 멀티파트 업로드의 key 시작 위치 표시  | String  |
| NextUploadIdMarker   |  IsTruncated가 true면 다음 멀티파트 업로드의 uploadId 시작 위치 표시| String  |
| MaxUploads   | 반환되는 멀티파트 업로드 최대 수. 기본값은 최대 1000개  | Int  |
| IsTruncated   |  반환된 멀티파트 업로드의 잘림 여부 표시  | String|
| EncodingType   |   기본적으로 인코딩하지 않으며, 반환값의 인코딩 방식을 규정. 옵션값: url  | String  |
|Upload |'UploadId', 'StorageClass', 'Key', 'Owner', 'Initiator', 'Initiated' 등의 정보를 포함한 모든 멀티파트 업로드가 담긴 리스트|List|
|CommonPrefixes |Prefix로 시작하고 Delimiter로 끝나는 key를 동일한 클래스에 분류|List|


### 멀티파트 업로드 초기화

#### 기능 설명

멀티파트 업로드를 초기화하고 해당하는 uploadId를 가져옵니다(Initiate Multipart Upload).

#### 메소드 프로토타입

```
create_multipart_upload(Bucket, Key, **kwargs):
```
#### 요청 예시

[//]: # ".cssg-snippet-init-multi-upload"
```python
response = client.create_multipart_upload(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    StorageClass='STANDARD'
)
```
#### 모든 매개변수 요청 예시

```python
response = client.create_multipart_upload(
    Bucket='examplebucket-1250000000',
    Key='multipart.txt',
    StorageClass='STANDARD'|'STANDARD_IA'|'ARCHIVE',
    Expires='string',
    CacheControl='string',
    ContentType='string',
    ContentDisposition='string',
    ContentEncoding='string',
    ContentLanguage='string',
    Metadata={
        'x-cos-meta-key1': 'value1',
        'x-cos-meta-key2': 'value2'
    },
    ACL='private'|'public-read',
    GrantFullControl='string',
    GrantRead='string'
)
# 가져온 UploadId를 앞으로의 인터페이스에 사용합니다.
uploadid = response['UploadId']
```
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   |유형 | 필수 입력 여부 |
| -------------- | -------------- |---------- | ----------- |
| Bucket  | 버킷 이름. BucketName-APPID로 구성 | String |  Yes |
| Key  |  객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg임 | String | Yes |
|  StorageClass  | 객체의 스토리지 유형 설정. STANDARD, STANDARD_IA, ARCHIVE가 있으며, 기본값은 STANDARD. 스토리지 유형에 대한 자세한 내용은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925) 참고 | String |  No |
| Expires  |  Expires 설정 | String| No |
| CacheControl  | 캐시 정책. Cache-Control 설정 | String |  No |
| ContentType  | 콘텐츠 유형. Content-Type 설정 | String |  No |
| ContentDisposition  | 파일 이름. Content-Disposition 설정 | String |  No |
| ContentEncoding  | 인코딩 형식. Content-Encoding 설정 | String |  No |
| ContentLanguage  | 언어 유형. Content-Language 설정 |  String |  No |
| Metadata |사용자 정의 객체 메타데이터 | Dict |  No |
| ACL |객체 ACL 설정. 예: 'private', 'public-read' |String| No|
| GrantFullControl |권한을 부여받은 계정에 모든 권한 부여. 형식: `id="OwnerUin"`|String|No|
|GrantRead |권한을 부여받은 계정에 읽기 권한 부여. 형식: `id="OwnerUin"` |String|No|

#### 반환 결과 설명

멀티파트 업로드한 초기화 정보 가져오기(dict 유형):

```python
{
    'UploadId': '150219101333cecfd6718d0caea1e2738401f93aa531a4be7a2afee0f8828416f3278e5570',
    'Bucket': 'examplebucket-1250000000', 
    'Key': 'exampleobject' 
}

```

| 매개변수 이름   | 매개변수 설명   |유형 |
| -------------- | -------------- |---------- |
|UploadId | 멀티파트 업로드의 식별 ID|String|
|Bucket|버킷 이름은 BucketName-APPID로 구성|String|
|key |객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg임|String|

### 멀티파트 업로드

객체를 멀티파트 업로드합니다(Upload Part).

#### 메소드 프로토타입

```
upload_part(Bucket, Key, Body, PartNumber, UploadId, **kwargs)
```
#### 요청 예시

[//]: # ".cssg-snippet-upload-part"
```python
# 참고: 멀티파트 업로드 최대 수는 10000개
response = client.upload_part(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Body=b'b'*1024*1024,
    PartNumber=1,
    UploadId='exampleUploadId'
)
```
#### 모든 매개변수 요청 예시

```python
# 참고: 멀티파트 업로드 최대 수는 10000개
response = client.upload_part(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Body=b'bytes'|file,
    PartNumber=1,
    UploadId='string',
    EnableMD5=False|True,
    ContentLength='123',
    ContentMD5='string',
    TrafficLimit='1048576'
)
```
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   |유형 | 필수 입력 여부 |
| -------------- | -------------- |---------- | ----------- |
| Bucket  | 버킷 이름. BucketName-APPID로 구성 | String |  Yes |
| Key  | 객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg임 | String |  Yes|
| Body  | 멀티파트 업로드의 콘텐츠. 로컬 파일 스트림 또는 입력 스트림 | file/bytes |  Yes|
| PartNumber  |업로드하는 파트의 식별 시리얼 넘버 |  Int |  Yes|
| UploadId  | 멀티파트 업로드의 식별 ID | String |  Yes|
| EnableMD5 | SDK의 Content-MD5 계산 여부. 기본적으로 비활성화 상태이며, 활성화 시 업로드 시간 증가|Bool | No|
| ContentLength  |전송 길이 설정 |  String |  No|
| ContentMD5  | 검사에 사용할 업로드 객체의 MD5 값 설정 | String |  No|
|  TrafficLimit | 단일 링크의 제한 속도. 단위는 bit/s이며 설정 범위는 819200-838860800, 즉 100KB/s-100MB/s로 설정| String |  No |

#### 반환 결과 설명

멀티파트 업로드의 속성(dict 유형):

```python
{
    'ETag': 'string'
}
```

| 매개변수 이름   | 매개변수 설명   |유형 |
| -------------- | -------------- |---------- |
| ETag |업로드된 멀티파트의 MD5 값. |String|

### 멀티파트 복사

다른 객체를 한 파트로 복사합니다(Upload Part - Copy).

#### 메소드 프로토타입

```
upload_part_copy(Bucket, Key, PartNumber, UploadId, CopySource, CopySourceRange='', **kwargs)
```
#### 요청 예시

[//]: # ".cssg-snippet-upload-part-copy"
```python
response = client.upload_part_copy(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    PartNumber=1,
    UploadId='exampleUploadId',
    CopySource={
        'Bucket': 'sourcebucket-1250000000', 
        'Key': 'exampleobject', 
        'Region': 'ap-guangzhou'
    }
)
```
#### 모든 매개변수 요청 예시

```python
response = client.upload_part_copy(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    PartNumber=100,
    UploadId='string',
    CopySource={
        'Bucket': 'sourcebucket-1250000000', 
        'Key': 'sourceObject', 
        'Region': 'COS_REGION', #원본 버킷 Region으로 변경
        'VersionId': 'string'
    },
    CopySourceRange='string',
    CopySourceIfMatch='string',
    CopySourceIfModifiedSince='string',
    CopySourceIfNoneMatch='string',
    CopySourceIfUnmodifiedSince='string'
)
```

#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   |유형 | 필수 입력 여부 |
| -------------- | -------------- |---------- | ----------- |
|  Bucket  | 버킷 이름은 BucketName-APPID로 구성 | String|  Yes |
|  Key  |  객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg임 | String  | Yes |
| PartNumber  |업로드하는 파트의 식별 시리얼 넘버 |  Int |  Yes|
| UploadId  | 멀티파트 업로드의 식별 ID | String |  Yes|
|  CopySource  | Bucket, Key, Region, VersionId를 포함한 원본 객체의 경로 복사 |  Dict | Yes |
|CopySourceRange| 복사할 원본 객체의 범위(형식: bytes=first-last). 지정하지 않으면 원본 객체 전체 복사|String|No|
|CopySourceIfMatch| 원본 객체의 Etag와 주어진 값이 동일한 경우에만 복사|String|No|
|CopySourceIfModifiedSince| 지정된 시간 이후 원본 객체가 수정되면 복사|String|No|
|CopySourceIfNoneMatch| 원본 객체의 Etag와 주어진 값이 동일하지 않은 경우에만 복사|String|No|
|CopySourceIfUnmodifiedSince| 지정된 시간 이후 원본 객체가 수정되지 않으면 복사|String|No|

#### 반환 결과 설명

파트의 속성 복사(dict 유형):
```python
{
    'ETag': 'string',
    'LastModified': 'string',
    'x-cos-copy-source-version-id': 'string',
}
```

| 매개변수 이름   | 매개변수 설명   |유형 |
| -------------- | -------------- |---------- |
| ETag |파트의 MD5 값 복사|String|
| LastModified |파트의 마지막 수정 시간 복사|String|
| x-cos-copy-source-version-id | 원본 객체의 버전 넘버 | String |

### 업로드된 파트 조회

#### 기능 설명

특정 멀티파트 업로드 작업에서 업로드된 파트를 조회합니다(List Parts).

#### 메소드 프로토타입

```
list_parts(Bucket, Key, UploadId, MaxParts=1000, PartNumberMarker=0, EncodingType='', **kwargs)
```
#### 요청 예시

[//]: # ".cssg-snippet-list-parts"
```python
response = client.list_parts(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    UploadId='exampleUploadId'
)
```
#### 모든 매개변수 요청 예시

```python
response = client.list_parts(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    UploadId=uploadid,
    MaxParts=1000,
    PartNumberMarker=100,
    EncodingType='url'
)
```
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   |유형 | 필수 입력 여부 |
| -------------- | -------------- |---------- | ----------- |
|Bucket|버킷 이름. BucketName-APPID로 구성|String| Yes|
|key |객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg임 |String| Yes|
|UploadId |멀티파트 업로드의 식별 ID|String| Yes|
|MaxParts |반환되는 멀티파트의 최대 수. 기본값은 최대 1000개|Int| No|
|PartNumberMarker |기본값: 0. 첫 파트부터 나열하며, PartNumberMarker의 다음 파트부터 나열|Int| No|
|EncodingType |기본적으로 인코딩하지 않으며, 반환값의 인코딩 방식을 규정. 옵션값: url|String|No|

#### 반환 결과 설명

업로드한 모든 파트의 정보(dict 유형):

```python
{
    'Bucket': 'examplebucket-1250000000', 
    'Key': 'exampleobject', 
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

| 매개변수 이름   | 매개변수 설명   |유형 |
| -------------- | -------------- |---------- |
| Bucket   | 버킷 이름. BucketName-APPID로 구성  | String  |
|  Key  |  객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg임 | String |
|  UploadId  |  멀티파트 업로드의 식별 ID | String |
| EncodingType   |   기본적으로 인코딩하지 않으며, 반환값의 인코딩 방식을 규정. 옵션값: url  | String  |
| MaxParts   | 반환하는 멀티파트의 최대 수. 기본값: 최대 1000  | String  |
| IsTruncated   |  반환된 파트의 잘림 여부 표시  | String|
| PartNumberMarker   | 기본값: 0. 첫 파트부터 나열하며, PartNumberMarker의 다음 파트부터 나열  | String  |
| NextPartNumberMarker   |  다음에 나열하는 멀티파트의 시작 위치 표시  | String  |
|  StorageClass  |  객체의 스토리지 유형 설정. STANDARD, STANDARD_IA, ARCHIVE가 있으며, 기본값은 STANDARD. 스토리지 유형에 대한 자세한 내용은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925) 참고 | String |
|  Part |ETag, PartNumber, Size, LastModified 등 업로드된 파트 관련 정보 | String |
|  Initiator  | DisplayName과 ID 등 멀티파트 업로드 생성자 | Dict |
|  Owner  | DisplayName과 ID 등 객체 소유자 정보 | Dict |



### 멀티파트 업로드 완료

#### 기능 설명

전체 객체의 멀티파트 업로드를 완료합니다(Complete Multipart Upload).

#### 메소드 프로토타입

```
complete_multipart_upload(Bucket, Key, UploadId, MultipartUpload={}, **kwargs)
```
#### 요청 예시

[//]: # ".cssg-snippet-complete-multi-upload"
```python
response = client.complete_multipart_upload(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    UploadId='exampleUploadId',
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

| 매개변수 이름   | 매개변수 설명   |유형 | 필수 입력 여부 |
| -------------- | -------------- |---------- | ----------- |
|  Bucket  | 버킷 이름. BucketName-APPID로 구성 | String |   Yes |
|  Key  | 객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg임 | String  |   Yes|
|  UploadId  | 멀티파트 업로드의 식별 ID | String  |   Yes|
|  MultipartUpload  |모든 파트의 ETag와 PartNumber 정보 |  Dict |   Yes|

#### 반환 결과 설명

어셈블된 객체의 관련 정보(dict 유형):

```python
{
    'ETag': '"3f866d0050f044750423e0a4104fa8cf-2"', 
    'Bucket': 'examplebucket-1250000000', 
    'Location': 'examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/exampleobject', 
    'Key': 'exampleobject'
}
```

| 매개변수 이름   | 매개변수 설명   |유형 |
| -------------- | -------------- |---------- |
|  ETag  |병합된 객체의 고유 태그값. 객체 콘텐츠의 MD5 검사값이 아니므로, 객체 고유성 검사에만 사용할 수 있으며 객체 콘텐츠 검사가 필요한 경우 업로드 과정에서 단일 파트의 ETag 값 검사 가능. |  String |
|  Bucket  |버킷 이름. BucketName-APPID로 구성 |  String |
|  Location  | URL 주소 |  String |
|  Key  |  객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg임 | String |


### 멀티파트 업로드 중지

#### 기능 설명

멀티파트 업로드 작업을 중지하고 업로드된 파트를 삭제합니다(Abort Multipart Upload).

#### 메소드 프로토타입

```
abort_multipart_upload(Bucket, Key, UploadId, **kwargs)
```
#### 요청 예시

[//]: # ".cssg-snippet-abort-multi-upload"
```python
response = client.abort_multipart_upload(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    UploadId='exampleUploadId'
)
```
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   |유형 | 필수 입력 여부 |
| -------------- | -------------- |---------- | ----------- |
|Bucket|버킷 이름. BucketName-APPID로 구성|String| Yes|
|key |객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg임|String| Yes|
|UploadId |멀티파트 업로드의 식별 ID|String| Yes|

#### 반환 결과 설명
해당 메소드의 반환값은 None입니다.





 ## 고급 인터페이스(권장)

### 객체 업로드(중단된 지점부터 이어서 전송)

#### 기능 설명
이 고급 인터페이스는 파일 길이에 따라 간편 업로드와 멀티파트 업로드를 자동으로 선택합니다. 20MB 이하 파일은 간편 업로드를 호출하고, 20MB 초과 파일은 멀티파트 업로드를 호출합니다. 멀티파트 업로드가 미완료된 파일은 자동으로 중단된 지점부터 이어서 전송합니다.
멀티파트 업로드하는 파일은 progress_callback 콜백 함수를 통해 업로드 진행률을 확인할 수 있습니다.

#### 메소드 프로토타입

```
upload_file(Bucket, Key, LocalFilePath, PartSize=1, MAXThread=5, EnableMD5=False, progress_callback=None, **kwargs)
```
#### 요청 예시

[//]: # ".cssg-snippet-transfer-upload-file"
```python


response = client.upload_file(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    LocalFilePath='local.txt',
    EnableMD5=False,
    progress_callback=None
)
```

#### 모든 매개변수 요청 예시
```python

def upload_percentage(consumed_bytes, total_bytes):
    """진행 바 콜백 함수. 현재 업로드의 백분율 계산

    :param consumed_bytes: 업로드된 데이터 양
    :param total_bytes: 총 데이터 양
    """
    if total_bytes:
        rate = int(100 * (float(consumed_bytes) / float(total_bytes)))
        print('\r{0}% '.format(rate))
        sys.stdout.flush()
        

response = client.upload_file(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    LocalFilePath='local.txt',
    PartSize=1,
    MAXThread=5,
    progress_callback=upload_percentage,
    EnableMD5=False|True,
    ACL='private'|'public-read', # 이 매개변수는 ACL이 1000개로 제한되어 있으니 신중히 사용하십시오.
    GrantFullControl='string',
    GrantRead='string',
    StorageClass='STANDARD'|'STANDARD_IA'|'ARCHIVE',
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
    },
    TrafficLimit='1048576'
)
```
#### 매개변수 설명


| 매개변수 이름   | 매개변수 설명   |유형 | 필수 입력 여부 |
| -------------- | -------------- |---------- | ----------- |
|  Bucket  | 버킷 이름. BucketName-APPID로 구성 | String |  Yes |
|  Key  | 객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`에서 객체 키는 doc/pic.jpg임 | String |  Yes |
|  LocalFilePath  | 로컬 파일의 경로명 |  String |  Yes |
|  PartSize  | 멀티파트 업로드의 파트 크기. 기본값: 1MB |  Int |  No |
|  MAXThread  | 멀티파트 업로드의 동시 업로드 수량. 기본적으로 5개 스레드로 멀티파트 업로드 |  Int |  No |
|progress_callback |  업로드 진행률 콜백 함수. 이 함수를 사용자 정의하여 업로드 진행률 확인 가능| Func| No |
| EnableMD5 | SDK의 Content-MD5 계산 여부. 기본적으로 비활성화 상태이며, 활성화 시 업로드 시간 증가|Bool | No|
| ACL |객체 ACL 설정. 예: private, public-read  |String| No|
| GrantFullControl |권한을 부여받은 계정에 모든 권한 부여. 형식: `id="OwnerUin"`|String|No|
|GrantRead |권한을 부여받은 계정에 읽기 권한 부여. 형식: `id="OwnerUin"`  |String|No|
|  StorageClass  |  객체의 스토리지 유형 설정. STANDARD, STANDARD_IA, ARCHIVE가 있으며, 기본값은 STANDARD. 스토리지 유형에 대한 자세한 내용은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925) 참고 | String |   No |
|  Expires  | Expires 설정 | String|  No |
|  CacheControl  |  캐시 정책. Cache-Control 설정 | String |   No |
|  ContentType  | 콘텐츠 유형. Content-Type 설정 |String |   No |
|  ContentDisposition  |  파일 이름. Content-Disposition 설정 | String |   No |
|  ContentEncoding  |  인코딩 형식. Content-Encoding 설정 | String |   No |
|  ContentLanguage  |  언어 유형. Content-Language 설정 | String |   No |
|  ContentLength  | 전송 길이 설정 | String |   No |
|  ContentMD5  | 검사에 사용할 업로드 객체의 MD5 값 설정 | String |   No |
|  Metadata | 사용자 정의 객체 메타데이터 | Dict |   No |
|  TrafficLimit | 단일 링크 제한 속도. 단위는 bit/s이며 설정 범위는 819200-838860800, 즉 100KB/s-100MB/s. 고급 인터페이스는 단일 스레드의 속도를 제한| String |  No |

#### 반환 결과 설명
업로드한 객체의 속성(dict 유형):

```python
{
    'ETag': 'string'
}
```

| 매개변수 이름   | 매개변수 설명   |유형 |
| -------------- | -------------- |---------- |
| ETag   |  멀티파트 업로드된 객체. 해당 값은 객체 콘텐츠의 MD5 검사값이 아니므로, 객체 고유성 검사에만 쓰일 수 있음  | String  |


### 객체 다운로드(중단된 지점부터 이어서 전송)

#### 기능 설명
이 고급 인터페이스는 전체 파일 다운로드만 지원합니다. 파일 길이에 따라 간편 다운로드와 멀티파트 다운로드를 자동으로 선택합니다. 20MB 이하 파일은 간편 다운로드를 사용하고, 20MB 초과 파일은 계속 다운로드를 사용합니다. 멀티파트 다운로드가 미완료된 파일은 자동으로 중단된 지점부터 이어서 전송합니다.

#### 메소드 프로토타입

```
download_file(Bucket, Key, DestFilePath, PartSize=20, MAXThread=5, EnableCRC=False, **Kwargs)
```
#### 요청 예시

[//]: # ".cssg-snippet-transfer-upload-file"
```python
response = client.download_file(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    DestFilePath='local.txt'
)
```

#### 모든 매개변수 요청 예시
```python
response = client.download_file(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    DestFilePath='local.txt',
    PartSize=1,
    MAXThread=5,
    EnableCRC=True,
    TrafficLimit='1048576'
    IfMatch='"9a4802d5c99dafe1c04da0a8e7e166bf"',
    IfModifiedSince='Wed, 28 Oct 2014 20:30:00 GMT',
    IfNoneMatch='"9a4802d5c99dafe1c04da0a8e7e166bf"',
    IfUnmodifiedSince='Wed, 28 Oct 2014 20:30:00 GMT',
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


| 매개변수 이름   | 매개변수 설명   |유형 | 필수 입력 여부 |
| -------------- | -------------- |---------- | ----------- |
|  Bucket  | 버킷 이름. BucketName-APPID로 구성 | String  |  Yes |
|  Key  |  객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg` 에서 객체 키는 doc/pic.jpg | String  | Yes |
|  DestFilePath  | 파일을 다운로드하는 로컬 타깃 경로명 |  String |  Yes |
|  PartSize  | 멀티파트 다운로드의 파트 크기. 기본값: 20MB |  Int |  No |
|  MAXThread  | 멀티파트 다운로드의 동시 다운로드 수량. 기본적으로 5개 스레드로 파트 다운로드 |  Int |  No |
|  EnableCRC  | 로컬 파일과 원격 파일의 crc 검사 활성화 여부. 기본값: False |  Bool |  No |
|  TrafficLimit | 단일 링크 제한 속도. 단위는 bit/s이며 설정 범위는 819200-838860800, 즉 100KB/s-100MB/s. 고급 인터페이스는 단일 스레드의 속도를 제한| String |  No |
|  IfMatch  |  ETag가 지정된 콘텐츠와 일치해야 반환 |String  | No |
|  IfModifiedSince  |   지정 시간 이후 수정될 경우에만 반환. 시간 형식: GMT | String  | No |
|  IfNoneMatch  |  ETag가 지정 콘텐츠와 불일치 시 반환 | String  | No |
|  IfUnmodifiedSince  |  객체 수정 시간이 지정 시간보다 이르거나 같을 경우에만 반환. 시간 형식: GMT| String  | No|
|  ResponseCacheControl  |  응답 헤더의 Cache-Control 설정 | String  | No |
|  ResponseContentDisposition  |  응답 헤더의 Content-Disposition 설정 | String  | No |
|  ResponseContentEncoding  |   응답 헤더의 Content-Encoding 설정 | String  | No |
|  ResponseContentLanguage  |  응답 헤더의 Content-Language 설정 | String  | No |
|  ResponseContentType  |   응답 헤더의 Content-Type 설정 | String  | No |
|  ResponseExpires  |응답 헤더의 Expires 설정 |   String  | No |
|  VersionId  | 다운로드할 객체 버전 지정 |  String  | No |

#### 반환 결과 설명
None



### 객체 복사

#### 기능 설명
이 고급 인터페이스는 5GB 미만 파일은 copy_object를 호출하고, 5GB 이상 파일은 멀티파트 업로드의 upload_part_copy를 호출합니다.

#### 메소드 프로토타입

```
copy(Bucket, Key, CopySource, CopyStatus='Copy', PartSize=10, MAXThread=5, **kwargs)
```

#### 요청 예시1: 객체 복사

[//]: # ".cssg-snippet-transfer-copy"
```python
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
from qcloud_cos import CosServiceError
from qcloud_cos import CosClientError

import sys
import os
import logging

# secret_id, secret_key, region 등을 포함한 사용자 속성을 설정합니다. Appid는 CosConfig에서 제거되었습니다. 매개변수 Bucket에 Appid를 포함시키십시오. Bucket은 BucketName-Appid로 구성됩니다.
secret_id = 'SecretId'     # 사용자의 SecretId로 대체합니다. CAM 콘솔에 로그인하여 확인 및 관리하십시오. https://console.cloud.tencent.com/cam/capi
secret_key ='SecretKey'   # 사용자의 SecretKey로 대체합니다. CAM 콘솔에 로그인하여 확인 및 관리하십시오. https://console.cloud.tencent.com/cam/capi
region = 'ap-beijing'      # 사용자의 region으로 대체합니다. 생성된 버킷이 속한 region은 콘솔에서 확인 가능합니다. https://console.cloud.tencent.com/cos5/bucket
                           # COS에서 지원되는 모든 region 목록은 다음을 참고하십시오. https://cloud.tencent.com/document/product/436/6224
token = None                 # 영구 키를 사용하는 경우 token을 입력할 필요가 없으나, 임시 키를 사용하는 경우 입력해야 합니다. 임시 키 생성 및 사용 가이드는 다음을 참고하십시오. https://cloud.tencent.com/document/product/436/14048

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token)  # 설정 객체 획득
client = CosS3Client(config)

response = client.copy(
    Bucket='test',
    Key='copy_10G.txt',
    CopySource={
        'Bucket': 'sourcebucket-1250000000', 
        'Key': 'exampleobject', 
        'Region': 'ap-guangzhou'
    }
)
```

#### 요청 예시2: 객체 이동

[//]: # ".cssg-snippet-transfer-copy-move"
```python
bucket = 'examplebucket-1250000000'
srcKey = 'src_object_key'  # 원본 객체 경로
destKey = 'dest_object_key'   # 타깃 객체 경로

# COS 자체에는 객체 이동 API가 없습니다. 이동이란 이전 객체를 새 객체에 먼저 복사한 다음 이전 객체를 삭제하는 것입니다.
try:
    response = client.copy(
        Bucket=bucket,
        Key=destKey,
        CopySource={
            'Bucket':bucket,
            'Key':srcKey,
            'Region':'ap-guangzhou',
        })
    client.delete_object(Bucket=bucket, Key=srcKey)
except CosException as e:
    print(e.get_error_msg())
```

#### 모든 매개변수 요청 예시

```python
response = client.copy(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    CopySource={
        'Bucket': 'sourcebucket-1250000000', 
        'Key': 'exampleobject', 
        'Region': 'ap-guangzhou'
    }
    CopyStatus='Copy'|'Replaced',
    PartSize=20,
    MAXThread=10
)
```
#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명   |유형 | 필수 입력 여부 |
| -------------- | -------------- |---------- | ----------- |
|  Bucket  | 버킷 이름. BucketName-APPID로 구성 | String  |  Yes |
|  Key  |  객체 키(Key)는 객체의 버킷 내 고유 식별자. 예: 객체의 액세스 도메인`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg` 에서 객체 키는 doc/pic.jpg | String  | Yes |
|  CopySource  | Bucket, Key, Region, VersionId를 포함한 원본 객체의 경로 복사 |  Dict | Yes |
 |  CopyStatus  |복사 상태. 선택값: Copy, Replaced | String | No |
 |  PartSize  |멀티파트 다운로드의 멀티파트 크기. 기본값: 10MB |  Int |  No |
 |  MAXThread  | 멀티파트 다운로드의 동시 다운로드 수량. 기본적으로 5개 스레드로 파트 다운로드 |  Int |  No |

#### 반환 결과 설명
5GB 미만 파일은 copy_object의 반환 결과이고, 5GB 이상 파일은 complete_multipart_upload의 반환 결과입니다(dict 유형).


### 일괄 업로드(로컬 폴더 업로드)

#### 기능 설명
이 예시는 SDK의 기본 인터페이스를 조합하여 로컬 폴더를 COS로 일괄 업로드합니다.

#### 요청 예시

[//]: # ".cssg-snippet-transfer-upload-file"
```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
from qcloud_cos import CosServiceError
from qcloud_cos import CosClientError
from qcloud_cos.cos_threadpool import SimpleThreadPool

import sys
import os
import logging

# secret_id, secret_key, region 등을 포함한 사용자 속성을 설정합니다. Appid는 CosConfig에서 제거되었습니다. 매개변수 Bucket에 Appid를 포함시키십시오. Bucket은 BucketName-Appid로 구성됩니다.
secret_id = 'SecretId'     # 사용자의 SecretId로 대체합니다. CAM 콘솔에 로그인하여 확인 및 관리하십시오. https://console.cloud.tencent.com/cam/capi
secret_key ='SecretKey'   # 사용자의 SecretKey로 대체합니다. CAM 콘솔에 로그인하여 확인 및 관리하십시오. https://console.cloud.tencent.com/cam/capi
region = 'ap-beijing'      # 사용자의 region으로 대체합니다. 생성된 버킷이 속한 region은 콘솔에서 확인 가능합니다. https://console.cloud.tencent.com/cos5/bucket
                           # COS에서 지원되는 모든 region 목록은 다음을 참고하십시오. https://www.qcloud.com/document/product/436/6224
token = None                 # 영구 키를 사용하는 경우 token을 입력할 필요가 없으나, 임시 키를 사용하는 경우 입력해야 합니다. 임시 키 생성 및 사용 가이드는 다음을 참고하십시오. https://cloud.tencent.com/document/product/436/14048

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token)  # 설정 객체 획득
client = CosS3Client(config)

uploadDir = '/root/logs'
bucket = 'examplebucket-125000000'
g = os.walk(uploadDir)
# 업로드의 스레드 풀 생성
pool = SimpleThreadPool()
for path, dir_list, file_list in g:
    for file_name in file_list:
        srcKey = os.path.join(path, file_name)
        cosObjectKey = srcKey.strip('/')
        # COS에 파일 존재 여부 판단
        exists = False
        try:
            response = client.head_object(Bucket=bucket, Key=cosObjectKey)
            exists = True
        except CosServiceError as e:
            if e.get_status_code() == 404:
                exists = False
            else:
                print("Error happened, reupload it.")
        if not exists:
            rint("File %s not exists in cos, upload it", srcKey)
            pool.add_task(client.upload_file, bucket, cosObjectKey, srcKey)


pool.wait_completion()
result = pool.get_result()
if not result['success_all']:
    print("Not all files upload sucessed. you should retry")
```

### 일괄 다운로드(COS에서 디렉터리 다운로드)

#### 기능 설명
이 예시는 SDK의 기본 인터페이스를 조합하여 COS 디렉터리에 있는 파일을 로컬 디스크로 일괄 다운로드합니다.

#### 요청 예시

[//]: # ".cssg-snippet-transfer-upload-file"
```python
# -*- coding=utf-8
import logging
import sys
import json
import os

from qcloud_cos import CosConfig, CosServiceError
from qcloud_cos import CosS3Client
from qcloud_cos.cos_threadpool import SimpleThreadPool

logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# secret_id, secret_key, region 등을 포함한 사용자 속성을 설정합니다. Appid는 CosConfig에서 제거되었습니다. 매개변수 Bucket에 Appid를 포함시키십시오. Bucket은 BucketName-Appid로 구성됩니다.
secret_id = 'SecretId'     # 사용자의 SecretId로 대체합니다. CAM 콘솔에 로그인하여 확인 및 관리하십시오. https://console.cloud.tencent.com/cam/capi
secret_key ='SecretKey'   # 사용자의 SecretKey로 대체합니다. CAM 콘솔에 로그인하여 확인 및 관리하십시오. https://console.cloud.tencent.com/cam/capi
region = 'ap-beijing'      # 사용자의 region으로 대체합니다. 생성된 버킷이 속한 region은 콘솔에서 확인 가능합니다. https://console.cloud.tencent.com/cos5/bucket
                           # COS에서 지원되는 모든 region 목록은 다음을 참고하십시오. https://www.qcloud.com/document/product/436/6224
token = None                 # 영구 키를 사용하는 경우 token을 입력할 필요가 없으나, 임시 키를 사용하는 경우 입력해야 합니다. 임시 키 생성 및 사용 가이드는 다음을 참고하십시오. https://cloud.tencent.com/document/product/436/14048
scheme = 'http'            # http/https 프로토콜 사용하여 COS 액세스. 기본값: https. 입력하지 않아도 됨

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)  # 설정 객체 획득
client = CosS3Client(config)

# 사용자의 bucket 정보
test_bucket = 'examplebucket-1250000000'
start_prefix = 'data/'
# COS는 세퍼레이터 '/'로 가상 디렉터리 시맨틱 구현,
# 기본 null 세퍼레이터를 사용해 디렉터리에 있는 모든 하위 노드를 나열할 수 있으며, 로컬 디렉터리 재귀와 유사한 효과 구현,
# delimiter를 "/"로 설정하면 프로그램에서 서브 디렉터리 재귀 처리 필요
delimiter = ''


# 현재 디렉터리의 하위 노드 나열. 모든 하위 노드 정보 반환
def listCurrentDir(prefix):
    file_infos = []
    sub_dirs = []
    marker = ""
    count = 1
    while True:
        response = client.list_objects(test_bucket, prefix, delimiter, marker)
        # 디버깅 출력
        # json_object = json.dumps(response, indent=4)
        # print(count, " =======================================")
        # print(json_object)
        count += 1

        if "CommonPrefixes" in response:
            common_prefixes = response.get("CommonPrefixes")
            sub_dirs.extend(common_prefixes)

        if "Contents" in response:
            contents = response.get("Contents")
            file_infos.extend(contents)

        if "NextMarker" in response.keys():
            marker = response["NextMarker"]
        else:
            break

    print("=======================================================")

    # delimiter를 "/"로 설정하면 서브 디렉터리 재귀 처리 필요,
    # sorted(sub_dirs, key=lambda sub_dir: sub_dir["Prefix"])
    # for sub_dir in sub_dirs:
    #     print(sub_dir)
    #     sub_dir_files = listCurrentDir(sub_dir["Prefix"])
    #     file_infos.extend(sub_dir_files)

    print("=======================================================")

    sorted(file_infos, key=lambda file_info: file_info["Key"])
    for file in file_infos:
        print(file)
    return file_infos


# 로컬 디렉터리에 파일 다운로드. 로컬 디렉터리에 동일한 이름의 파일이 있는 경우 덮어쓰기
#디렉터리 구조가 존재하지 않는 경우 COS와 동일한 디렉터리 구조 생성
def downLoadFiles(file_infos):
    localDir = "./download/"

    pool = SimpleThreadPool()
    for file in file_infos:
        # 파일을 다운로드하여 로컬로 가져오기
        file_cos_key = file["Key"]
        localName = localDir + file_cos_key

        # 로컬 디렉터리 구조가 존재하지 않는 경우 재귀 생성
        if not os.path.exists(os.path.dirname(localName)):
            os.makedirs(os.path.dirname(localName))

        # skip dir, no need to download it
        if str(localName).endswith("/"):
            continue

        # 실제 다운로드 파일
        # 스레드 풀 방식 사용
        pool.add_task(client.download_file, test_bucket, file_cos_key, localName)

        # 간편 다운로드 방식
        # response = client.get_object(
        #     Bucket=test_bucket,
        #     Key=file_cos_key,
        # )
        # response['Body'].get_stream_to_file(localName)

    pool.wait_completion()
    return None


# 기능을 캡슐화해 COS 상의 디렉터리를 로컬 디스크에 다운로드
def downLoadDirFromCos(prefix):
    global file_infos

    try:
        file_infos = listCurrentDir(prefix)

    except CosServiceError as e:
        print(e.get_origin_msg())
        print(e.get_digest_msg())
        print(e.get_status_code())
        print(e.get_error_code())
        print(e.get_error_msg())
        print(e.get_resource_location())
        print(e.get_trace_id())
        print(e.get_request_id())

    downLoadFiles(file_infos)
    return None


if __name__ == "__main__":
    downLoadDirFromCos(start_prefix)
```


### 객체 일괄 삭제(디렉터리 삭제)

#### 기능 설명
COS 자체에는 디렉터리 개념이 없습니다. 사용자의 사용 습관에 따라 세퍼레이터 /로 ‘디렉터리’를 구현할 수 있습니다.

디렉터리와 그 파일을 삭제하는 작업은 사실상 COS에서 동일한 접두사를 가진 객체를 일괄 삭제하는 것과 같습니다. 현재 COS Python SDK는 이러한 작업을 위한 인터페이스를 제공하지 않지만, 객체 목록 쿼리와 객체 일괄 삭제 작업을 결합하여 디렉터리 및 파일 삭제 효과를 얻을 수 있습니다.

#### 요청 예시
```python
import logging
import sys
import os

from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
from qcloud_cos.cos_threadpool import SimpleThreadPool

logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# secret_id, secret_key, region 등을 포함한 사용자 속성을 설정합니다. Appid는 CosConfig에서 제거되었습니다. 매개변수 Bucket에 Appid를 포함시키십시오. Bucket은 BucketName-Appid로 구성됩니다.
secret_id = 'SecretId'     # 사용자의 SecretId로 대체합니다. CAM 콘솔에 로그인하여 확인 및 관리하십시오. https://console.cloud.tencent.com/cam/capi
secret_key ='SecretKey'   # 사용자의 SecretKey로 대체합니다. CAM 콘솔에 로그인하여 확인 및 관리하십시오. https://console.cloud.tencent.com/cam/capi
region = 'ap-beijing'      # 사용자의 region으로 대체합니다. 생성된 버킷이 속한 region은 콘솔에서 확인 가능합니다. https://console.cloud.tencent.com/cos5/bucket
                           # COS에서 지원되는 모든 region 목록은 다음을 참고하십시오. https://cloud.tencent.com/document/product/436/6224
token = None                 # 영구 키를 사용하는 경우 token을 입력할 필요가 없으나, 임시 키를 사용하는 경우 입력해야 합니다. 임시 키 생성 및 사용 가이드는 다음을 참고하십시오. https://cloud.tencent.com/document/product/436/14048
scheme = 'http'            # http/https 프로토콜 사용하여 COS 액세스. 기본값: https. 입력하지 않아도 됨

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)  # 설정 객체 획득
client = CosS3Client(config)

bucket = 'examplebucket-1250000000'
folder = 'folder/' # 삭제할 디렉터리. '/'끝은 디렉터리를 나타냅니다.

def delete_cos_dir():
    pool = SimpleThreadPool()
    marker = ""
    while True:
        file_infos = []

        # 페이지당 100개의 객체 나열
        response = client.list_objects(Bucket=bucket, Prefix=folder, Marker=marker, MaxKeys=100)

        if "Contents" in response:
            contents = response.get("Contents")
            file_infos.extend(contents)
            pool.add_task(delete_files, file_infos)

        # 나열 완료, 종료
        if response['IsTruncated'] == 'false':
            break
        
        # 다음 페이지 나열
        marker = response["NextMarker"]

    pool.wait_completion()
    return None   

def delete_files(file_infos):

    # 일괄 삭제 요청 구성
    delete_list = []
    for file in file_infos:
        delete_list.append({"Key": file['Key']})

    response = client.delete_objects(Bucket=bucket, Delete={"Object": delete_list})
    print(response)

if __name__ == "__main__":
    delete_cos_dir()
```


## 클라이언트 암호화

#### 기능 설명

Python은 클라이언트 암호화를 지원해 파일을 암호화하여 업로드하고, 다운로드 시 복호화합니다. 클라이언트 암호화는 대칭 AES와 비대칭 RSA 암호화를 지원합니다.
여기서의 대칭과 비대칭은 매번 생성되는 임의 키를 암호화할 때만 사용하며, 파일 데이터 암호화에는 항상 AES256 대칭 암호화를 사용합니다.
클라이언트 암호화는 중요 데이터를 보관하는 고객에게 적합합니다. 클라이언트 암호화는 업로드 속도를 일부 희생하고 SDK 내부에서 직렬 방식을 사용해 업로드를 진행합니다.

### 업로드 암호화 프로세스

1. 파일 객체를 업로드하기 전에 무작위로 대칭 암호화 키를 생성합니다. 무작위로 생성한 키는 사용자의 대칭 또는 비대칭 키를 통해 암호화되며, 암호화된 결과는 객체의 메타데이터에 base64로 인코딩됩니다.
2. 파일 객체를 업로드합니다. 업로드 시 메모리에서 AES256 알고리즘을 사용해 암호화합니다.

### 다운로드 복호화 프로세스

1. 파일 메타데이터에서 암호화에 필요한 정보를 가져와 Base64로 디코딩 후 사용자 보안키로 복호화하여 암호화된 데이터의 키를 얻습니다.
2. 키 쌍을 사용해 입력 스트림을 다운로드하고 AES256을 사용해 복호화하여 복호화된 파일 입력 스트림을 얻습니다.

#### 요청 예시

예시1: 대칭 AES256을 사용해 생성되는 임의 키를 모두 암호화합니다.

[//]: # ".cssg-snippet-put-object-cse-c-aes"
```python
# secret_id, secret_key, region 등을 포함한 사용자 속성을 설정합니다. Appid는 CosConfig에서 제거되었습니다. 매개변수 Bucket에 Appid를 포함시키십시오. Bucket은 BucketName-Appid로 구성됩니다.
secret_id = 'SecretId'     # 사용자의 SecretId로 대체합니다. CAM 콘솔에 로그인하여 확인 및 관리하십시오. https://console.cloud.tencent.com/cam/capi
secret_key ='SecretKey'   # 사용자의 SecretKey로 대체합니다. CAM 콘솔에 로그인하여 확인 및 관리하십시오. https://console.cloud.tencent.com/cam/capi
region = 'ap-beijing'      # 사용자의 region으로 대체합니다. 생성된 버킷이 속한 region은 콘솔에서 확인 가능합니다. https://console.cloud.tencent.com/cos5/bucket
                           # COS에서 지원되는 모든 region 목록은 다음을 참고하십시오. https://www.qcloud.com/document/product/436/6224
token = None                 # 영구 키를 사용하는 경우 token을 입력할 필요가 없으나, 임시 키를 사용하는 경우 입력해야 합니다. 임시 키 생성 및 사용 가이드는 다음을 참고하십시오. https://cloud.tencent.com/document/product/436/14048

conf = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token)

# 방법1: 키 값으로 암호화된 클라이언트 초기화
aes_provider = AESProvider(aes_key='aes_key_value')

# 방법2: 키 경로로 암호화된 클라이언트 초기화
aes_key_pair = AESProvider(aes_key_path='aes_key_path')

client_for_aes = CosEncryptionClient(conf, aes_provider)

# 객체 업로드. 암호화되지 않은 클라이언트의 put_object 기능은 모두 호환됩니다. 자세한 내용은 put_object를 참고하십시오.
response = client_for_aes.put_object(
                        Bucket='examplebucket-1250000000',
                        Body=b'bytes'|file,
                        Key='exampleobject',
                        EnableMD5=False)

# 객체 다운로드. 암호화되지 않은 클라이언트의 get_object 기능은 모두 호환됩니다. 자세한 내용은 get_object를 참고하십시오.
response = client_for_aes.get_object(
                        Bucket='examplebucket-1250000000',
                        Key='exampleobject')

# 멀티파트 업로드. 암호화되지 않은 클라이언트의 멀티파트 업로드와 호환됩니다. 마지막 part를 제외한 각 part의 크기는 16바이트의 배수여야 합니다.
response = client_for_aes.create_multipart_upload(
                        Bucket='examplebucket-1250000000',
                        Key='exampleobject_upload')
uploadid = response['UploadId']
client_for_aes.upload_part(
                Bucket='examplebucket-1250000000',
                Key='exampleobject_upload',
                Body=b'bytes'|file,
                PartNumber=1,
                UploadId=uploadid)
response = client_for_aes.list_parts(
                Bucket='examplebucket-1250000000',
                Key='exampleobject_upload',
                UploadId=uploadid)
client_for_aes.complete_multipart_upload(
                Bucket='examplebucket-1250000000',
                Key='exampleobject_upload',
                UploadId=uploadid,
                MultipartUpload={'Part':response['Part']})

# 중단 지점부터 이어서 전송하는 방식으로 객체를 업로드합니다. `partsize` 크기는 반드시 16바이트의 배수여야 합니다.
response = client_for_aes.upload_file(
    Bucket='test04-123456789',
    LocalFilePath='local.txt',
    Key=file_name,
    PartSize=10,
    MAXThread=10
)

```

예시2: 비대칭 RSA 암호화를 사용해 생성되는 임의 키를 모두 암호화합니다.

[//]: # ".cssg-snippet-put-object-cse-c-rsa"
```python
# secret_id, secret_key, region 등을 포함한 사용자 속성을 설정합니다. Appid는 CosConfig에서 제거되었습니다. 매개변수 Bucket에 Appid를 포함시키십시오. Bucket은 BucketName-Appid로 구성됩니다.
secret_id = 'SecretId'     # 사용자의 SecretId로 대체합니다. CAM 콘솔에 로그인하여 확인 및 관리하십시오. https://console.cloud.tencent.com/cam/capi
secret_key ='SecretKey'   # 사용자의 SecretKey로 대체합니다. CAM 콘솔에 로그인하여 확인 및 관리하십시오. https://console.cloud.tencent.com/cam/capi
region = 'ap-beijing'      # 사용자의 region으로 대체합니다. 생성된 버킷이 속한 region은 콘솔에서 확인 가능합니다. https://console.cloud.tencent.com/cos5/bucket
                           # COS에서 지원되는 모든 region 목록은 다음을 참고하십시오. https://www.qcloud.com/document/product/436/6224
token = None                 # 영구 키를 사용하는 경우 token을 입력할 필요가 없으나, 임시 키를 사용하는 경우 입력해야 합니다. 임시 키 생성 및 사용 가이드는 다음을 참고하십시오. https://cloud.tencent.com/document/product/436/14048

conf = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token)

# 방법1: 키 값으로 암호화된 클라이언트 초기화
rsa_key_pair = RSAProvider.get_rsa_key_pair('public_key_value', 'private_key_value')

# 방법2: 키 경로로 암호화된 클라이언트 초기화
rsa_key_pair = RSAProvider.get_rsa_key_pair('public_key_path', 'private_key_path')

rsa_provider = RSAProvider(key_pair_info=rsa_key_pair)
client_for_rsa = CosEncryptionClient(conf, rsa_provider)

# 객체 업로드. 암호화되지 않은 클라이언트의 put_object 기능은 모두 호환됩니다. 자세한 내용은 put_object를 참고하십시오.
response = client_for_rsa.put_object(
                        Bucket='examplebucket-1250000000',
                        Body=b'bytes'|file,
                        Key='exampleobject',
                        EnableMD5=False)

# 객체 다운로드. 암호화되지 않은 클라이언트의 get_object 기능은 모두 호환됩니다. 자세한 내용은 get_object를 참고하십시오.
response = client_for_rsa.get_object(
                        Bucket='examplebucket-1250000000',
                        Key='exampleobject')

# 멀티파트 업로드. 암호화되지 않은 클라이언트의 멀티파트 업로드와 호환됩니다. 마지막 part를 제외한 각 part의 크기는 16바이트의 배수여야 합니다.
response = client_for_rsa.create_multipart_upload(
                        Bucket='examplebucket-1250000000',
                        Key='exampleobject_upload')
uploadid = response['UploadId']
client_for_rsa.upload_part(
                Bucket='examplebucket-1250000000',
                Key='exampleobject_upload',
                Body=b'bytes'|file,
                PartNumber=1,
                UploadId=uploadid)
response = client_for_rsa.list_parts(
                Bucket='examplebucket-1250000000',
                Key='exampleobject_upload',
                UploadId=uploadid)
client_for_rsa.complete_multipart_upload(
                Bucket='examplebucket-1250000000',
                Key='exampleobject_upload',
                UploadId=uploadid,
                MultipartUpload={'Part':response['Part']})

# 중단 지점부터 이어서 전송하는 방식으로 객체를 업로드합니다. `partsize` 크기는 반드시 16바이트의 배수여야 합니다.
response = client_for_rsa.upload_file(
    Bucket='test04-123456789',
    LocalFilePath='local.txt',
    Key=file_name,
    PartSize=10,
    MAXThread=10
)
```
