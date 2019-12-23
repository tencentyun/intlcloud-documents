## 개발 준비

### 관련 리소스
COS의 XML Python SDK 리소스 다운로드 주소: [XML Python SDK](https://github.com/tencentyun/cos-python-sdk-v5).
데모 예제 Demo 다운로드 주소: [XML Python Demo](https://github.com/tencentyun/cos-python-sdk-v5/blob/master/qcloud_cos/demo.py).

### 환경 의존

COS의 XML Python SDK는 현재 Python 2.6, Python 2.7 및 Python 3.x를 지원합니다.
>?문서에서 나오는 SecretId, SecretKey, Bucket 같은 명칭의 함의 및 획득 방법은 [COS 용어집](https://cloud.tencent.com/document/product/436/7751)을 참조하십시오.

### SDK 설치

SDK 설치 방식에는 pip 설치, 수동 설치 및 오프라인 설치의 세 가지 방식이 있습니다.

#### pip를 사용하여 설치(추천)
```sh
 pip install -U cos-python-sdk-v5
```

#### 수동 설치
[XML Python SDK](https://github.com/tencentyun/cos-python-sdk-v5)에서 소스 코드를 다운로드하고 setup을 통해 수동으로 설치한 후 다음 명령을 실행하십시오.
```python
 python setup.py install
```
#### 오프라인 설치
```python
# 공중망이 있는 기기에서 다음 명령을 수행합니다.
mkdir cos-python-sdk-packages
pip download cos-python-sdk-v5 -d cos-python-sdk-packages
tar -czvf cos-python-sdk-packages.tar.gz cos-python-sdk-packages

# 설치 패키지를 공중망이 없는 기기에 복사한 후 다음 명령을 실행합니다.
# 두 대 기기의 python 버전이 동일하도록 해야 합니다. 그렇지 않으면 설치 실패가 발생할 수 있습니다.
tar -xzvf cos-python-sdk-packages.tar.gz
pip install cos-python-sdk-v5 --no-index -f cos-python-sdk-packages
```

## 시작 가이드
다음의 예제 코드를 참조하십시오.
```python
# appid는 구성 중에서 제거되었으므로 매개변수 버킷에 appid를 넣으십시오. Bucket은 bucketname-appid로 구성됩니다.
# 1. 사용자 구성을 설정하며 secretId, secretKey 및 Region을 포함합니다.
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import logging

logging.basicConfig(level=logging.INFO, stream=sys.stdout)

secret_id = 'xxxxxxxx'       # 사용자의 SecretId로 대체합니다.
secret_key = 'xxxxxxx'      # 사용자의 secretKey로 대체합니다.
region = 'ap-beijing-1'     # 사용자의 지역으로 대체합니다.
token = None                # 임시 키를 사용하려면 Token이 전송되어야 합니다. 기본적으로 비어 있으며 입력하지 않아도 됩니다.
scheme = 'https'            # http/https 프로토콜을 사용하여 COS에 액세스하도록 지정하며 기본으로 https이고 입력하지 않아도 됩니다.
config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
# 2. 클라이언트 객체 가져오기
client = CosS3Client(config)
# 아래 설명을 참조하거나 Demo 응용프로그램을 참조하고 자세한 내용은 https://github.com/tencentyun/cos-python-sdk-v5/blob/master/qcloud_cos/demo.py를 참조하십시오.
```

임시 키 생성 및 사용은 [임시 키 생성 및 사용 가이드](https://cloud.tencent.com/document/product/436/14048)를 참조하십시오.

## 파일 업로드
### 파일 스트림 간편 업로드
```python
file_name = 'test.txt'
# 이진 모드(binary mode)로 파일을 열 것을 강력히 권장합니다. 그렇지 않으면 오류가 발생할 수 있습니다.
with open('test.txt', 'rb') as fp:
    response = client.put_object(
        Bucket='test04-123456789',
        Body=fp,
        Key=file_name,
        StorageClass='STANDARD',
        EnableMD5=False
    )
print(response['ETag'])
```
#### 매개변수 설명
| 매개변수 이름   | 매개변수 설명   | 유형 | 필수 입력 |
| -------------- | -------------- |---------- | ----------- |
| Bucket| 버킷 이름, bucketname-appid로 구성 | String | 예 |
| Body | 업로드 파일의 내용이며, 파일 스트림 또는 바이트 스트림일 수 있습니다| file/bytes | 예 |
| key | 객체 키(Key)이며, 버킷에서 객체의 유일한 식별자입니다. 예를 들어, 객체의 액세스 도메인 이름 ` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg ` 중, 객체 키는 doc1/pic1.jpg입니다 | string      | 예   |
| StorageClass | 파일의 스토리지 클래스를 설정합니다. STANDARD, STANDARD_IA. 기본값: STANDARD | String | 아니요 |
| EnableMD5 | SDK가 Content-MD5를 계산할 필요 여부이며, 기본 설정은 꺼짐이고 시작되면 다음에는 업로드 시간이 증가될 수 있습니다|Bool | 아니요|

더 많은 선택 가능한 매개변수는 [Python SDK API 문서](https://cloud.tencent.com/document/product/436/12270)를 참조하십시오.

### 바이트 스트림 간편 업로드
```python
response = client.put_object(
    Bucket='test04-123456789',
    Body=b'abcdefg',
    Key=file_name,
    EnableMD5=False
)
print(response['ETag'])

```
### chunk 간편 업로드
```python
import requests
stream = requests.get('https://intl.cloud.tencent.com/document/product/436/7778')

# 네트워크 스트림이 Transfer-Encoding:chunked 방식으로 COS에 전송
response = client.put_object(
    Bucket='test04-123456789',
    Body=stream,
    Key=file_name
)
print(response['ETag'])
```

### 로컬 경로 간편 업로드
```python
response = client.put_object_from_local_file(
    Bucket='test04-123456789',
    LocalFilePath='local.txt',
    Key=file_name,
    EnableMD5=False
)
print(response['ETag'])
```

### HTTP 헤더 간편 업로드 설정
```python
response = client.put_object(
    Bucket='test04-123456789',
    Body=b'test',
    Key=file_name,
    ContentType='text/html; charset=utf-8',
    EnableMD5=False
)
print(response['ETag'])
```

### 사용자 지정 헤더 간편 업로드 설정
```python
response = client.put_object(
    Bucket='test04-123456789',
    Body=b'test',
    Key=file_name,
    Metadata={
        'x-cos-meta-key1': 'value1',
        'x-cos-meta-key2': 'value2'
    },
    EnableMD5=False
)
print(response['ETag'])
```

### 고급 업로드 API(추천)
파일 크기에 따라 자동으로 간편 업로드 또는 멀티파트 업로드를 선택하며 멀티파트 업로드는 중단점 재개 기능이 있습니다.
```python
response = client.upload_file(
    Bucket='test04-123456789',
    LocalFilePath='local.txt',
    Key=file_name,
    PartSize=10,
    MAXThread=10,
    EnableMD5=False
)
print(response['ETag'])
```

## 파일 다운로드
### 파일을 로컬로 다운로드
```python
response = client.get_object(
    Bucket='test04-123456789',
    Key=file_name,
)
response['Body'].get_stream_to_file('output.txt')
```
#### 매개변수 설명
| 매개변수 이름   | 매개변수 설명   | 유형 | 필수 입력 |
| -------------- | -------------- |---------- | ----------- |
| Bucket | 버킷 이름, bucketname-appid로 구성 | String| 예 |
| Key | 객체 키(Key)이며, 버킷에서 개체의 유일한 ID입니다. 예를 들어, 객체의 액세스 도메인 이름  bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg  중 객체 키는 doc1/pic1.jpg입니다 | string | 예 |

더 많은 선택 가능한 매개변수는 [Python SDK API 문서](https://cloud.tencent.com/document/product/436/12270)를 참조하십시오.

### 파일 스트림 획득
```python
response = client.get_object(
    Bucket='test04-123456789',
    Key=file_name,
)
fp = response['Body'].get_raw_stream()
print(fp.read(2))
```

### Response HTTP 헤더 설정
```python
response = client.get_object(
    Bucket='test04-123456789',
    Key=file_name,
    ResponseContentType='text/html; charset=utf-8'
)
print response['Content-Type']
fp = response['Body'].get_raw_stream()
print(fp.read(2))
```

### 다운로드 범위 지정
```python
response = client.get_object(
    Bucket='test04-123456789',
    Key=file_name,
    Range='bytes=0-10'
)
fp = response['Body'].get_raw_stream()
print(fp.read())
```
## 이상 유형
CosClientError 및 CosServiceError를 포함하며 각각 SDK 클라이언트 오류 및 COS 서버 오류에 해당합니다.

### CosClientError
CosClientError는 일반적으로 timeout으로 인한 클라이언트 오류를 가리키며 사용자가 캡처 후에 다시 시도나 다른 조작을 선택할 수 있습니다.

### CosServiceError
CosServiceError는 서버가 반환한 구체적인 정보를 제공합니다.
```python
#except CosServiceError as e
e.get_origin_msg()  # 기존의 오류 정보를 획득하며 형식은 XML
e.get_digest_msg()  # 처리된 오류 정보를 획득하며 형식은 dict
e.get_status_code() # http 오류 코드 획득(예: 4XX, 5XX)
e.get_error_code()  # COS 정의 오류 코드 획득
e.get_error_msg()   # COS 오류 코드의 구체 설명 획득
e.get_trace_id()    # 요청의 trace_id 획득
e.get_request_id()  # 요청의 request_id 획득
e.get_resource_location() # URL 주소 획득
```
