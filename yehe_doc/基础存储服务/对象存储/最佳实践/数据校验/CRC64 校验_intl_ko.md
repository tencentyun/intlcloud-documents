## 소개

클라이언트와 서버 간에 데이터가 전송되면서 데이터에 오류가 발생하기도 합니다. COS는 [MD5 검증](https://intl.cloud.tencent.com/document/product/436/32467)으로 데이터 무결성을 검증하며, CRC64 검사 코드를 이용해 데이터 검사를 합니다.

COS는 새로 업로드되는 객체에 CRC64 계산을 실시하고, 그 결과를 객체의 속성으로 보관합니다. 이후 반환되는 응답 헤더에 x-cos-hash-crc64ecma가 포함되는데, 이 헤더는 업로드한 객체의 CRC64 값을 나타내며 [ECMA-182 표준](https://www.ecma-international.org/publications/standards/Ecma-182.htm)에 따라 계산하여 값을 얻습니다. CRC64의 특성상 런칭 이전 시점부터 COS의 객체에 존재하기 때문에 COS에서 객체의 CRC64 값을 계산하지 않습니다. 따라서 해당 유형의 객체를 획득할 때 CRC64 값이 반환되지 않습니다.

## 작업 설명

현재 CRC64를 지원하는 API는 다음과 같습니다.

- 간편 업로드 인터페이스
	- [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749)와 [POST Object](https://intl.cloud.tencent.com/document/product/436/14690): 반환된 응답 헤더에서 파일의 CRC64 검사 값을 획득할 수 있습니다.
- 멀티파트 업로드 인터페이스
	- [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750): COS에서 반환된 CRC64 값과 로컬에서 계산된 값을 비교 검증합니다.
	- [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742): 멀티파트 각각에 CRC64 속성이 있으면 객체의 CRC64 값이 반환됩니다. 하지만 일부 멀티파트에 CRC64 값이 없는 경우, 반환되지 않습니다.
- [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287)를 실행하면 이와 대응하는 CRC64 값이 반환됩니다.
- [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881)를 실행할 때 원본 객체에 CRC64 값이 있으면 CRC64가 반환되고, 그렇지 않으면 반환되지 않습니다.
- [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745)와 [GET Object](https://intl.cloud.tencent.com/document/product/436/7753)를 실행할 때 객체에 CRC64가 있으면 반환됩니다. 사용자는 COS에서 반환된 CRC64 값과 로컬에서 계산된 CRC64 값을 비교 검증할 수 있습니다.

## API 예시

#### 멀티파트 업로드 응답

다음은 사용자가 Upload Part 요청을 한 뒤 얻은 응답 예시입니다. x-cos-hash-crc64ecma 헤더는 멀티파트의 CRC64 값을 나타냅니다. 해당 값과 로컬에서 계산한 CRC64 값을 비교하여 멀티파트의 무결성을 검사할 수 있습니다.

```shell
HTTP/1.1 200 OK
content-length: 0
connection: close
date: Thu, 05 Dec 2019 01:58:03 GMT
etag: "358e8c8b1bfa35ee3bd44cb3d2cc416b"
server: tencent-cos
x-cos-hash-crc64ecma: 15060521397700495958
x-cos-request-id: NWRlODY0MmJfMjBiNDU4NjRfNjkyZl80ZjZi****
```

#### 멀티파트 업로드 완료 응답

다음은 사용자가 Complete Multipart Upload 요청을 한 뒤 얻은 응답 예시입니다. x-cos-hash-crc64ecma 헤더는 전체 객체의 CRC64 값을 나타냅니다. 해당 값과 로컬에서 계산한 CRC64 값을 비교하여 객체 무결성 검사를 할 수 있습니다.

```shell
HTTP/1.1 200 OK
content-type: application/xml
transfer-encoding: chunked
connection: close
date: Thu, 05 Dec 2019 02:01:17 GMT
server: tencent-cos
x-cos-hash-crc64ecma: 15060521397700495958
x-cos-request-id: NWRlODY0ZWRfMjNiMjU4NjRfOGQ4Ml81MDEw****

[Object Content]
```

## SDK 예시

### Python SDK

다음은 Python SDK를 사례로 한 객체 검사법으로, 전체 코드에 대한 예시는 다음과 같습니다.

> ?코드는 Python 2.7을 기반으로 하였으며, Python SDK의 자세한 사용 방법은 Python SDK의 [객체 작업](https://intl.cloud.tencent.com/document/product/436/31546) 문서를 참고하십시오.

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
import crcmod

logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# SecretId, SecretKey, Region을 포함한 사용자 속성을 설정합니다.
# APPID는 설정에서 삭제되었으니 매개변수 Bucket에 APPID를 입력하십시오. Bucket은 BucketName-APPID로 구성됩니다.
secret_id = COS_SECRETID           # 사용자 SecretId 정보로 대체
secret_key = COS_SECRETKEY         # 사용자 SecretKey 정보로 대체
region = 'ap-beijing'      # 사용자 Region으로 대체, 예시는 베이징 리전
token = None               # 임시 키를 사용할 경우 Token 입력, 기본값이 null이면 입력하지 않음
config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token)  # 설정 객체 획득
client = CosS3Client(config)
```

#### 2. 객체의 검사 값 계산

객체의 멀티파트를 시뮬레이션하고, 전체 객체의 CRC64 검사 값을 계산합니다.

```python
OBJECT_PART_SIZE = 1024 * 1024      #각 멀티파트 크기 시뮬레이션
OBJECT_TOTAL_SIZE = OBJECT_PART_SIZE * 1 + 123      #총 객체 크기
object_body = '1' * OBJECT_TOTAL_SIZE       #객체 콘텐츠

#전체 객체의 crc64 검사 값 계산
c64 = crcmod.mkCrcFun(0x142F0E1EBA9EA3693L, initCrc=0L, xorOut=0xffffffffffffffffL, rev=True)
local_crc64 =str(c64(object_body))
```

#### 3. 멀티파트 업로드 초기화

```python
#멀티파트 업로드 초기화
response = client.create_multipart_upload(
    Bucket='examplebucket-1250000000',  #사용자 Bucket 이름으로 대체. examplebucket은 예시 버킷이며, 1250000000은 예시 APPID임.
    Key='exampleobject',                #업로드한 객체의 Key 값으로 대체
    StorageClass='STANDARD',            #객체의 스토리지 유형
)
#멀티파트 업로드한 UploadId 획득
upload_id = response['UploadId']
```

#### 4. 객체 멀티파트 업로드

객체 멀티파트 업로드는 객체를 여러 파트로 분할하여 업로드하는 것을 뜻합니다. 최대 10000개 파트까지 분할할 수 있습니다. 각 파트의 크기는 1MB-5GB이며, 마지막 파트의 크기는 1MB 미만일 수 있습니다. 멀티파트를 업로드할 때 각 파트의 PartNumber(번호)를 설정하고, 각 파트의 CRC64 값을 계산해야 합니다. 멀티파트 업로드를 성공한 후 반환되는 CRC64 값과 로컬에서 계산한 값을 검사할 수 있습니다.

```python
#객체를 멀티파트 업로드할 때, 각 파트의 크기는 OBJECT_PART_SIZE이며, 마지막 파트의 크기는 OBJECT_PART_SIZE보다 작을 수 있습니다.
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
    local_part_crc64 = str(c64(body))	#로컬에서 CRC64 계산

    response = client.upload_part(
        Bucket='examplebucket-1250000000',
        Key='exampleobject',
        Body=body,
        PartNumber=part_number,
        UploadId=upload_id,
    )   
    part_crc_64 = response['x-cos-hash-crc64ecma']# 서버에서 반환된 CRC64
    if local_part_crc64 != part_crc_64:		# 데이터 검사
    	print 'crc64 check FAIL'
    	exit(-1)
    etag = response['ETag']
    part_list.append({'ETag' : etag, 'PartNumber' : part_number})
```

#### 5. 멀티파트 업로드 완료

모든 멀티파트를 업로드한 뒤 멀티파트 업로드 작업을 완료해야 합니다. COS에서 반환된 CRC64와 로컬 객체의 CRC64를 비교 검증할 수 있습니다.

```python
#멀티파트 업로드 완료
response = client.complete_multipart_upload(
    Bucket='examplebucket-1250000000',  #사용자 Bucket 이름으로 대체. examplebucket은 예시 버킷이며, 1250000000은 예시 APPID임.
    Key='exampleobject',             #객체의 Key 값
    UploadId=upload_id,
    MultipartUpload={       #모든 파트의 ETag와 PartNumber가 모두 대응되어야 함
        'Part' : part_list    
    },
)
crc64ecma = response['x-cos-hash-crc64ecma']
if crc64ecma != local_crc64:			# 데이터 검사
    print 'check crc64 Failed'
    exit(-1)
```

### Java SDK

객체 업로드는 Java SDK의 고급 인터페이스 사용을 권장합니다. Java SDK [객체 작업](https://intl.cloud.tencent.com/document/product/436/31534)을 참고하십시오.

#### 로컬에서 파일의 crc64를 계산하는 방법

```java
String calculateCrc64(File localFile) throws IOException {
    CRC64 crc64 = new CRC64();

    try (FileInputStream stream = new FileInputStream(localFile)) {
        byte[] b = new byte[1024 * 1024];
        while (true) {
            final int read = stream.read(b);
            if (read <= 0) {
                break;
            }
            crc64.update(b, read);
        }
    }

    return Long.toUnsignedString(crc64.getValue());
}
```

#### COS에서 파일의 crc64 값을 가져와서 로컬 파일과 검사하는 방법

```java
// COSClient 생성 참고: [시작하기](https://intl.cloud.tencent.com/document/product/436/10199);
ObjectMetadata cosMeta = COSClient().getObjectMetadata(bucketName, cosFilePath); 
String cosCrc64 = cosMeta.getCrc64Ecma();
String localCrc64 = calculateCrc64(localFile);

if (cosCrc64.equals(localCrc64)) {
    System.out.println("ok");
} else {
    System.out.println("fail");
}
```