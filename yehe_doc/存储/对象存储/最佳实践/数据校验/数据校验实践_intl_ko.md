## 소개

COS는 클라이언트와 서버 간 데이터를 전송할 때 발생할 수 있는 오류에 대해 MD5 검증법을 적용하여 업로드하는 데이터의 무결성을 보장합니다. COS 서버가 수락한 데이터의 MD5 검사 값이 사용자가 설정한 MD5 검사 값과 일치해야만 데이터를 성공적으로 업로드할 수 있습니다.

COS의 모든 객체는 대응하는 ETag가 하나씩 있습니다. ETag는 객체 생성 시 부여되는 객체 콘텐츠의 정보를 표시합니다. 하지만 ETag가 객체 콘텐츠의 MD5 검사 값과 반드시 동일하지는 않습니다. 따라서 ETag로 다운로드한 객체와 원본 객체의 일치성 여부를 검사할 수 없습니다. 사용자는 사용자 정의한 객체 메타데이터(x-cos-meta-\*)로 다운로드한 객체와 원본 객체의 일치성 검사를 실행할 수 있습니다.

## 데이터 검증 방법

- 업로드된 객체 검사
COS에 업로드된 객체와 로컬 객체의 일치성 여부를 검사하려면, 업로드 시 HTTP로 요청한 [Content-MD5](https://intl.cloud.tencent.com/document/product/436/7728) 필드를 Base64를 경유해 코딩한 객체 콘텐츠의 MD5 검사 값으로 설정합니다. 이때 COS 서버에서 사용자가 업로드한 객체를 검사하고, COS 서버가 수락한 객체의 MD5 검사 값이 사용자가 설정한 Content-MD5와 일치해야만 객체를 성공적으로 업로드할 수 있습니다.
- 다운로드한 객체 검사
객체 업로드 시 검사 알고리즘으로 객체의 검사 값을 계산하여 다운로드한 객체와 원본 객체의 일치 여부를 검사할 수 있습니다. 사용자 정의한 메타데이터로 객체 검사 값을 설정한 뒤, 다운로드한 객체의 검사 값을 다시 계산하여 사용자 정의한 메타데이터와 비교 검증합니다. 이 경우, 사용자는 검사 알고리즘을 직접 선택할 수 있으며, 같은 객체를 업로드 및 다운로드할 때 사용하는 검사 알고리즘은 동일해야 합니다.   



## API 인터페이스 예시

#### 간편 업로드 요청

다음은 사용자의 객체 업로드 요청 예시입니다. 객체를 업로드할 때 Content-MD5를 Base64를 경유해 코딩하는 객체 콘텐츠의 MD5 검사 값으로 설정합니다. 이때 COS 서버에서 수락한 객체의 MD5 검사 값과 사용자가 설정한 Content-MD5가 동일해야 객체를 성공적으로 업로드할 수 있으며, 사용자 정의한 메타데이터 x-cos-meta-md5를 객체의 검사 값으로 설정합니다.
>다음 예시는 MD5 검사 알고리즘으로 얻은 객체 검사 값이며, 다른 검사 알고리즘을 적용해도 됩니다.  

```url
PUT /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 21 Jun 2019 09:24:28 GMT
Content-Type: image/jpeg
Content-Length: 13
Content-MD5: ti4QvKtVqIJAvZxDbP/c+Q==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1561109068;1561116268&q-key-time=1561109068;1561116268&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=&q-signature=998bfc8836fc205d09e455c14e3d7e623bd2****
x-cos-meta-md5: b62e10bcab55a88240bd9c436cffdcf9
Connection: close

[Object Content]
```

#### 멀티파트 업로드 요청

다음은 멀티파트 업로드 요청 초기화에 관한 예시입니다. 객체를 멀티파트 업로드할 때 멀티파트 업로드 초기화를 통해 객체의 사용자 정의 메타데이터를 설정할 수 있습니다. 다음 예시에서는 사용자 정의한 메타데이터 x-cos-meta-md5를 객체 검사 값으로 설정합니다.   

```url
POST /exampleobject?uploads HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 21 Jun 2019 09:45:12 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1561109068;1561116268&q-key-time=1561109068;1561116268&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=&q-signature=998bfc8836fc205d09e455c14e3d7e623bd2****
x-cos-meta-md5: b62e10bcab55a88240bd9c436cffdcf9
```

#### 객체 다운로드 응답

다음은 사용자가 객체 다운로드 요청을 하여 얻은 응답 예시입니다. 사용자는 객체 검사 값을 재차 계산한 뒤 응답에 포함된 객체의 사용자 정의 메타데이터 x-cos-meta-md5와 사용자 정의한 메타데이터를 비교하고, 이를 통해 다운로드한 객체와 원본 객체의 일치성 여부를 검증합니다.   

```url
HTTP/1.1 200 OK
Content-Type: application/octet-stream
Content-Length: 13
Connection: close
Accept-Ranges: bytes
Cache-Control: max-age=86400
Content-Disposition: attachment; filename=example.jpg
Date: Thu, 04 Jul 2019 11:33:00 GMT
ETag: "b62e10bcab55a88240bd9c436cffdcf9"
Last-Modified: Thu, 04 Jul 2019 11:32:55 GMT
Server: tencent-cos
x-cos-request-id: NWQxZGUzZWNfNjI4NWQ2NF9lMWYyXzk1NjFj****
x-cos-meta-md5: b62e10bcab55a88240bd9c436cffdcf9

[Object Content]
```

## SDK 예시

다음은 Python SDK를 사례로 한 객체 검사법으로, 전체 코드에 대한 예시는 다음과 같습니다.

>코드는 Python 2.7을 기반으로 하였으며, Python SDK의 자세한 사용 방법은 Python SDK의 [객체 작업](https://intl.cloud.tencent.com/document/product/436/31546) 문서를 참조하십시오.

#### 1. 초기화 설정

SecretId, SecretKey, Region을 포함한 사용자 속성을 설정하고, 클라이언트 객체를 생성합니다.

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
from qcloud_cos import CosServiceError
from qcloud_cos import CosClientError
import sys
import logging
import hashlib

logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# SecretId, SecretKey, Region을 포함한 사용자 속성을 설정합니다.
# APPID는 설정에서 삭제되었으니 매개변수 Bucket에 APPID를 입력하십시오. Bucket은 BucketName-APPID로 구성됩니다.
secret_id = COS_SECRETID           # 본인의 SecretId 정보로 대체
secret_key = COS_SECRETKEY         # 본인의 SecretKey 정보로 대체
region = 'ap-beijing'      # 본인의 Region으로 대체, 예시는 베이징 리전임
token = None               # 임시 키를 사용할 경우, Token 입력, 기본값이 null이면 입력하지 않음
config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token)  # 설정 객체 획득
client = CosS3Client(config)
```

#### 2. 간편한 객체 업로드 검사

#### (1) 객체의 검사 값 계산

MD5 검사 알고리즘으로 객체 검사 값을 얻으며, 다른 검사 알고리즘을 적용할 수도 있습니다.

```python
object_body = 'hello cos'
#객체의 md5 검사 값 획득
md5 = hashlib.md5()
md5.update(object_body)
md5_str = md5.hexdigest()
```

#### (2) 간편한 객체 업로드

코드 중 EnableMD5=True는 객체 업로드 시 MD5 검사 활성화를 뜻합니다. Python SDK에서 Content-MD5를 계산하면 업로드 시간이 다소 지연됩니다. COS 서버가 수락한 객체의 MD5 검사 값과 Content-MD5가 일치해야 객체가 성공적으로 업로드됩니다.
x-cos-meta-md5는 사용자 정의한 매개변수(사용자 정의 매개변수의 이름 형식은 x-cos-meta-\*)이며, 본 예시에서는 객체의 MD5 검사 값을 나타냅니다.

```python
#간편 객체 업로드 및 MD5 검사 활성화
response = client.put_object(
    Bucket='examplebucket-1250000000',      #본인의 Bucket 이름으로 대체, examplebucket은 예시로 든 버킷이며, 1250000000은 예시 APPID임.
    Body='hello cos',                 #업로드한 객체 콘텐츠
    Key='example-object-1',           #업로드한 객체의 Key 값으로 대체 
    EnableMD5=True,                   #업로드한 MD5 검사 활성화
    Metadata={                        #사용자 정의 매개변수 설정, 객체의 MD5 검사 값을 매개변수로 하여 COS 서버에 입력
        'x-cos-meta-md5' : md5_str
    }
)
print 'ETag: ' + response['ETag']     # Object의 Etag값
```

#### (3) 객체 다운로드

객체를 다운로드하고, 사용자 정의 매개변수를 획득합니다.

```python
#객체 다운로드
response = client.get_object(
    Bucket='examplebucket-1250000000',      #본인의 Bucket 이름으로 대체, examplebucket은 예시로 든 버킷이며, 1250000000은 예시 APPID임.
    Key='example-object-1'                  #다운로드한 객체의 Key 값
)
fp = response['Body'].get_raw_stream()
download_object = fp.read()                 #객체 콘텐츠 획득
print "get object body: " + download_object
print 'ETag: ' + response['ETag']               
print 'x-cos-meta-md5: ' + response['x-cos-meta-md5']   #사용자 정의 매개변수 x-cos-meta-md5 획득
```

#### (4) 객체 검사

객체를 성공적으로 다운로드한 뒤, 객체 검사 값을 재차 계산하여(검사 알고리즘은 객체 업로드 때와 동일해야 함) 사용자 정의 매개변수 x-cos-meta-md5와 비교함으로써 다운로드한 객체와 업로드된 객체의 콘텐츠가 일치하는지 검증합니다.

```python
#다운로드한 객체의 MD5 검사 값 계산
md5 = hashlib.md5()                 
md5.update(download_object)
md5_str = md5.hexdigest()
print 'download object md5: ' + md5_str

#다운로드한 객체와 업로드된 객체의 MD5 검사 값 비교하여 객체 일치 여부 검증
if md5_str == response['x-cos-meta-md5']:
    print 'MD5 check OK'
else:
    print 'MD5 check FAIL'
```

#### 3. 객체 멀티파트 업로드 검사

#### (1) 객체의 검사 값 계산

객체의 멀티파트를 시뮬레이션하고, 전체 객체의 검사 값을 계산합니다. 다음은 MD5 검사 알고리즘으로 얻은 객체의 검사 값이며, 다른 검사 알고리즘을 적용할 수도 있습니다.

```python
OBJECT_PART_SIZE = 1024 * 1024      #각 멀티파트 크기 시뮬레이션
OBJECT_TOTAL_SIZE = OBJECT_PART_SIZE * 1 + 123      #총 객체 크기
object_body = '1' * OBJECT_TOTAL_SIZE       #객체 콘텐츠

#전체 객체 콘텐츠의 MD5 검사 값 계산
md5 = hashlib.md5()
md5.update(object_body)
md5_str = md5.hexdigest()
```

#### (2) 멀티파트 업로드 초기화

멀티파트 업로드 초기화 시 사용자 정의 매개변수 x-cos-meta-md5를 설정하고, 전체 객체의 MD5 검사 값을 매개변수 콘텐츠로 정합니다.

```python
#멀티파트 업로드 초기화
response = client.create_multipart_upload(
    Bucket='examplebucket-1250000000',  #본인의 Bucket 이름으로 대체, examplebucket은 예시로 든 버킷이며, 1250000000은 예시 APPID임.
    Key='exampleobject-2',              #업로드한 객체의 Key 값으로 대체 
    StorageClass='STANDARD',            #객체의 스토리지 레벨
    Metadata={
        'x-cos-meta-md5' : md5_str      #사용자 정의 매개변수를 MD5 검사 값으로 설정
    }
)
#멀티파트 업로드한 UploadId 획득
upload_id = response['UploadId']
```

#### (3) 객체 멀티파트 업로드

객체 멀티파트 업로드는 객체를 여러 파트로 분할하여 업로드하는 것을 뜻합니다. 최대 10000개 파트까지 분할할 수 있습니다. 각 파트의 크기는 1MB~5GB이며, 마지막 파트의 크기는 1MB 미만일 수 있습니다. 멀티파트를 업로드할 때 각 파트의 PartNumber(번호)를 설정해야 합니다. EnableMD5=True는 멀티파트 검사 활성화를 뜻하며, 이 검사를 활성화하면 업로드 시간이 다소 지연됩니다. 이때 Python SDK에서 각 파트의 Content-MD5를 계산하며, COS 서버가 수락한 객체의 MD5 검사 값이 Content-MD5와 일치해야 멀티파트를 성공적으로 업로드할 수 있습니다. 업로드가 성공하면 각 파트의 ETag가 반환됩니다.     

```python
#객체를 멀티파트 업로드할 때, 각 파트의 크기는 OBJECT_PART_SIZE이며, 마지막 파트의 크기는 OBJECT_PART_SIZE보다 작을 수 있음
part_list = list()
position = 0
left_size = OBJECT_TOTAL_SIZE
part_number = 0
while left_size > 0:
    part_number += 1
    if left_size >= OBJECT_PART_SIZE:
        body = object_body[position:position+OBJECT_PART_SIZE]
    else:
        body = object_body[position:]
    position += OBJECT_PART_SIZE
    left_size -= OBJECT_PART_SIZE

    #멀티파트 업로드
    response = client.upload_part(
        Bucket='examplebucket-1250000000',  #본인의 Bucket 이름으로 대체, examplebucket은 예시로 든 버킷이며, 1250000000은 예시 APPID임.
        Key='exampleobject-2',              #객체의 Key 값 
        Body=body,
        PartNumber=part_number,
        UploadId=upload_id,
        EnableMD5=True       #멀티파트 검사 활성화, COS 서버가 각 파트에 MD5 검사 실시.
    )
    etag = response['ETag']     #ETag는 각 파트의 MD5 값 표시
    part_list.append({'ETag' : etag, 'PartNumber' : part_number})
    print etag + ', ' + str(part_number)
```

#### (4) 멀티파트 업로드 완료

멀티파트 업로드를 모두 마치면 이를 완료하는 작업을 수행해야 합니다. 각 파트의 ETag와 PartNumber가 모두 대응되어야 합니다. COS 서버는 이를 각 파트의 정확성 여부를 검증하는 용도로 활용합니다. 멀티파트 업로드가 완료된 뒤 반환되는 ETag는 전체 객체 콘텐츠의 MD5 검사 값이 아닌 병합 이후 객체의 고유 태그값입니다. 객체를 다운로드할 때는 사용자 정의 매개변수를 통해 검사하십시오.

```python
#멀티파트 업로드 완료
response = client.complete_multipart_upload(
    Bucket='examplebucket-1250000000',  #본인의 Bucket 이름으로 대체, examplebucket은 예시로 든 버킷이며, 1250000000은 예시 APPID임.
    Key='exampleobject-2',              #객체의 Key 값 
    UploadId=upload_id,
    MultipartUpload={       #모든 파트의 ETag와 PartNumber가 모두 대응해야 함
        'Part' : part_list    
    },
)

#ETag는 병합한 객체의 고유성을 검사하기 위한 고유 태그값으로, 객체 콘텐츠의 MD5 검사 값이 아님.
print "ETag: " + response['ETag']   
print "Location: " + response['Location']   #URL 주소
print "Key: " + response['Key'] 
```

#### (5) 객체 다운로드

객체를 다운로드하고, 사용자 정의 매개변수를 획득합니다.

```python
# 객체 다운로드
response = client.get_object(
    Bucket='examplebucket-1250000000',  #본인의 Bucket 이름으로 대체, examplebucket은 예시로 든 버킷이며, 1250000000은 예시 APPID임.
    Key='exampleobject-2'               #객체의 Key 값 
)
print 'ETag: ' + response['ETag']                        #객체의 ETag는 객체 콘텐츠의 MD5 검사 값 아님 
print 'x-cos-meta-md5: ' + response['x-cos-meta-md5']    #사용자 정의 매개변수 x-cos-meta-md5 획득
```

#### (6) 객체 검사

객체를 성공적으로 다운로드한 뒤, 객체의 MD5 검사 값을 재차 계산하여 사용자 정의 매개변수 x-cos-meta-md5와 비교함으로써 다운로드한 객체와 업로드된 객체의 콘텐츠가 일치하는지 검증합니다.

```python
#다운로드한 객체의 MD5 검사 값 계산
fp = response['Body'].get_raw_stream()
DEFAULT_CHUNK_SIZE = 1024*1024
md5 = hashlib.md5()
chunk = fp.read(DEFAULT_CHUNK_SIZE)     
while chunk:
    md5.update(chunk)
    chunk = fp.read(DEFAULT_CHUNK_SIZE)
md5_str = md5.hexdigest()
print 'download object md5: ' + md5_str

#다운로드한 객체와 업로드된 객체의 MD5 검사 값 비교하여 객체 일치 여부 검증
if md5_str == response['x-cos-meta-md5']:
    print 'MD5 check OK'
else:
    print 'MD5 check FAIL'
```
