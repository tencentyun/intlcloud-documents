## 다운로드 및 설치

#### 관련 리소스
- COS의 XML Python SDK 소스 코드 다운로드 주소: [XML Python SDK](https://github.com/tencentyun/cos-python-sdk-v5)
- SDK 고속 다운로드 주소: [XML Python SDK](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-python-sdk-v5/latest/cos-python-sdk-v5.zip)
- 예시 Demo 다운로드 주소: [XML Python Demo](https://github.com/tencentyun/cos-python-sdk-v5/blob/master/qcloud_cos/demo.py)
- SDK 문서의 모든 예시 코드는 [SDK 코드 예시](https://github.com/tencentyun/cos-snippets/tree/master/Python)를 참조하십시오.
- SDK 로그 업데이트는 [ChangeLog](https://github.com/tencentyun/cos-python-sdk-v5/blob/master/CHANGELOG.md)를 참조하십시오.

#### 환경 종속

COS의 XML Python SDK는 현재 Python 2.7 및 Python 3.4 이상을 지원합니다.
>?본 문서에 나오는 SecretId, SecretKey, Bucket, Region 등의 명칭에 대한 의미 및 획득 방법은 [COS 용어 정보](https://intl.cloud.tencent.com/document/product/436/7751)를 참조하십시오.

#### SDK 설치

SDK 설치 방법에는 pip 설치, 수동 설치, 오프라인 설치의 세 가지 방법이 있습니다.

- pip로 설치(권장)
```sh
 pip install -U cos-python-sdk-v5
```

- 수동 설치
[XML Python SDK](https://github.com/tencentyun/cos-python-sdk-v5)에서 소스 코드를 다운로드합니다. setup으로 수동 설치하고 다음 명령어를 실행합니다.
```python
 python setup.py install
```

- 오프라인 설치
```python
# 외부 네트워크가 연결된 기기에서 다음 명령어를 실행합니다.
mkdir cos-python-sdk-packages
pip download cos-python-sdk-v5 -d cos-python-sdk-packages
tar -czvf cos-python-sdk-packages.tar.gz cos-python-sdk-packages
# 설치 패키지를 외부 네트워크가 연결되지 않은 기기에 복사한 후 다음 명령어를 실행합니다.
# 두 기기의 python 버전은 동일해야 하며, 동일하지 않을 경우 설치에 실패합니다.
tar -xzvf cos-python-sdk-packages.tar.gz
pip install cos-python-sdk-v5 --no-index -f cos-python-sdk-packages
```



## 사용하기
COS Python SDK를 사용한 클라이언트 초기화, 버킷 생성, 버킷 리스트 조회, 객체 업로드, 객체 리스트 조회, 객체 다운로드, 객체 삭제 등의 기본 작업 방법은 아래와 같습니다.

### 초기화
다음 예시 코드를 참조하십시오.

[//]: # (.cssg-snippet-global-init)
```python
# -*- coding=utf-8
# appid는 설정에서 삭제되었습니다. 매개변수 Bucket에 appid를 입력하십시오. Bucket은 BucketName-APPID로 구성됩니다.
# 1. secretId, secretKey, Region을 포함한 사용자 설정
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import logging

logging.basicConfig(level=logging.INFO, stream=sys.stdout)

secret_id = 'SECRETID'      # 사용자 secretId로 변경(CAM 콘솔에 로그인하여 획득)
secret_key = 'SECRETKEY'      # 사용자 secretKey로 변경(CAM 콘솔에 로그인하여 획득)
region = 'COS_REGION'     # 사용자 Region으로 변경
token = None                # 임시 키를 사용할 경우 Token 입력, 기본값이 null이면 입력하지 않음
scheme = 'https'            # http/https 프로토콜을 사용한 COS 액세스로 지정, 기본값이 https이면 입력하지 않음
config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
# 2. 클라이언트 객체 획득
client = CosS3Client(config)
# 다음 설명 또는 Demo 프로그램을 참조하십시오. 자세한 내용은 https://github.com/tencentyun/cos-python-sdk-v5/blob/master/qcloud_cos/demo.py를 확인하십시오.
```


>?임시 키 생성 및 사용에 대한 자세한 내용은 [임시 키 생성 및 사용 가이드](https://intl.cloud.tencent.com/document/product/436/14048)를 참조하십시오.

프록시 설정:

[//]: # (.cssg-snippet-global-init-proxy)
```python
# APPID는 설정에서 삭제되었습니다. 매개변수 Bucket에 APPID를 입력하십시오. Bucket은 BucketName-APPID로 구성됩니다.
# 1. secretId, secretKey, Region을 포함한 사용자 설정
secret_id = 'SECRETID'      # 사용자 secretId로 변경(CAM 콘솔에 로그인하여 획득)
secret_key = 'SECRETKEY'      # 사용자 secretKey로 변경(CAM 콘솔에 로그인하여 획득)
region = 'COS_REGION'     # 사용자 Region으로 변경
proxies = {
    'http': '127.0.0.1:80', # 사용자 HTTP 프록시 주소로 변경
    'https': '127.0.0.1:443' # 사용자 HTTPS 프록시 주소로 변경
}
config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Proxies=proxies)
# 2. 클라이언트 객체 획득
client = CosS3Client(config)
# 다음 설명 또는 Demo 프로그램을 참조하십시오. 자세한 내용은 https://github.com/tencentyun/cos-python-sdk-v5/blob/master/qcloud_cos/demo.py를 확인하십시오.
```

Endpoint 설정:

[//]: # (.cssg-snippet-global-init-endpoint)
```python
# APPID는 설정에서 삭제되었습니다. 매개변수 Bucket에 APPID를 입력하십시오. Bucket은 BucketName-APPID로 구성됩니다.
# 1. secretId, secretKey, Region을 포함한 사용자 설정
secret_id = 'SECRETID'      # 사용자 secretId로 변경(CAM 콘솔에 로그인하여 획득)
secret_key = 'SECRETKEY'      # 사용자 secretKey로 변경(CAM 콘솔에 로그인하여 획득)
region = 'COS_REGION'     # 사용자 Region으로 변경
endpoint = 'cos.accelerate.myqcloud.com' # 사용자 endpoint로 변경
config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Endpoint=endpoint)
# 2. 클라이언트 객체 획득
client = CosS3Client(config)
# 다음 설명 또는 Demo 프로그램을 참조하십시오. 자세한 내용은 https://github.com/tencentyun/cos-python-sdk-v5/blob/master/qcloud_cos/demo.py를 확인하십시오.
```

사용자 정의 도메인 설정:
```python
# APPID는 설정에서 삭제되었습니다. 매개변수 Bucket에 APPID를 입력하십시오. Bucket은 BucketName-APPID로 구성됩니다.
# 1. secretId, secretKey, Region을 포함한 사용자 설정
secret_id = 'SECRETID'      # 사용자 secretId로 변경(CAM 콘솔에 로그인하여 획득)
secret_key = 'SECRETKEY'      # 사용자 secretKey로 변경(CAM 콘솔에 로그인하여 획득)
region = 'COS_REGION'     # 사용자 Region으로 변경

# domain 사용자 정의 도메인 설정
domain = 'user-define.example.com'
config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Domain=domain)
# 2. 클라이언트 객체 획득
client = CosS3Client(config)
# 다음 설명 또는 Demo 프로그램을 참조하십시오. 자세한 내용은 https://github.com/tencentyun/cos-python-sdk-v5/blob/master/qcloud_cos/demo.py를 확인하십시오.
```

글로벌 가속 도메인 설정:
```python
# APPID는 설정에서 삭제되었습니다. 매개변수 Bucket에 APPID를 입력하십시오. Bucket은 BucketName-APPID로 구성됩니다.
# 1. secretId, secretKey, Region을 포함한 사용자 설정
secret_id = 'SECRETID'      # 사용자 secretId로 변경(CAM 콘솔에 로그인하여 획득)
secret_key = 'SECRETKEY'      # 사용자 secretKey로 변경(CAM 콘솔에 로그인하여 획득)
region = 'COS_REGION'     # 사용자 Region으로 변경

# domain 사용자 정의 도메인. 일반적으로 설정할 필요 없으며, 글로벌 가속 도메인을 사용하는 경우 해당하는 도메인으로 설정합니다. 예: examplebucket-1250000000.cos.accelerate.myqcloud.com
# 글로벌 가속 활성화는 https://cloud.tencent.com/document/product/436/38864 참조
domain = 'examplebucket-1250000000.cos.accelerate.myqcloud.com'
config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Domain=domain)
# 2. 클라이언트 객체 획득
client = CosS3Client(config)
# 다음 설명 또는 Demo 프로그램을 참조하십시오. 자세한 내용은 https://github.com/tencentyun/cos-python-sdk-v5/blob/master/qcloud_cos/demo.py를 확인하십시오.
```

### 버킷 생성

[//]: # (.cssg-snippet-put-bucket)
```python
response = client.create_bucket(
    Bucket='examplebucket-1250000000'
)
```

### 버킷 리스트 조회

[//]: # (.cssg-snippet-get-service)
```python
response = client.list_buckets(
)
```

### 객체 업로드

>!간편 업로드는 5GB를 초과하는 파일은 지원하지 않으며, 다음과 같은 고급 업로드 인터페이스 사용을 권장합니다. 매개변수 설명은 [객체 작업](https://intl.cloud.tencent.com/document/product/436/31546) 문서를 참조하십시오.

[//]: # (.cssg-snippet-put-object-comp-comp)
```python
#### 파일 스트림 간편 업로드(5GB를 초과하는 파일은 지원하지 않으며, 다음과 같은 고급 업로드 인터페이스 사용 권장)
# 바이너리 모드(binary mode)로 파일을 여십시오(강력 권장). 그렇지 않을 경우 오류가 발생할 수 있습니다.
with open('picture.jpg', 'rb') as fp:
    response = client.put_object(
        Bucket='examplebucket-1250000000',
        Body=fp,
        Key='picture.jpg',
        StorageClass='STANDARD',
        EnableMD5=False
    )
print(response['ETag'])

#### 바이트 스트림 간편 업로드
response = client.put_object(
    Bucket='examplebucket-1250000000',
    Body=b'bytes',
    Key='picture.jpg',
    EnableMD5=False
)
print(response['ETag'])


#### chunk 간편 업로드
import requests
stream = requests.get('https://cloud.tencent.com/document/product/436/7778')

# 네트워크 스트림은 Transfer-Encoding:chunked 방식으로 COS에 전송됩니다.
response = client.put_object(
    Bucket='examplebucket-1250000000',
    Body=stream,
    Key='picture.jpg'
)
print(response['ETag'])

#### 고급 업로드 인터페이스(권장)
# 파일 크기에 따라 자동으로 간편 업로드 또는 멀티파트 업로드를 선택하며, 멀티파트 업로드는 중단된 지점부터 이어 올리기 기능을 지원합니다.
response = client.upload_file(
    Bucket='examplebucket-1250000000',
    LocalFilePath='local.txt',
    Key='picture.jpg',
    PartSize=1,
    MAXThread=10,
    EnableMD5=False
)
print(response['ETag'])
```

### 객체 리스트 조회

[//]: # (.cssg-snippet-get-bucket)
```python
response = client.list_objects(
    Bucket='examplebucket-1250000000',
    Prefix='folder1'
)
```

`list_objects` 인터페이스 호출 1회당 조회 가능한 객체 수는 1000개입니다. 모든 객체를 조회할 경우 순환 호출이 필요합니다.

[//]: # (.cssg-snippet-get-bucket-recursive)
```python
marker = ""
while True:
    response = client.list_objects(
        Bucket='examplebucket-1250000000',
        Prefix='folder1',
        Marker=marker
    )
    print(response['Contents'])
    if response['IsTruncated'] == 'false':
        break 
    marker = response['NextMarker']
```

### 객체 다운로드

[//]: # (.cssg-snippet-get-object-comp)
```python
####  파일을 로컬로 가져오기
response = client.get_object(
    Bucket='examplebucket-1250000000',
    Key='picture.jpg',
)
response['Body'].get_stream_to_file('output.txt')

#### 파일 스트림 가져오기
response = client.get_object(
    Bucket='examplebucket-1250000000',
    Key='picture.jpg',
)
fp = response['Body'].get_raw_stream()
print(fp.read(2))

#### Response HTTP 헤더 설정
response = client.get_object(
    Bucket='examplebucket-1250000000',
    Key='picture.jpg',
    ResponseContentType='text/html; charset=utf-8'
)
print(response['Content-Type'])
fp = response['Body'].get_raw_stream()
print(fp.read(2))

#### 다운로드 범위 지정
response = client.get_object(
    Bucket='examplebucket-1250000000',
    Key='picture.jpg',
    Range='bytes=0-10'
)
fp = response['Body'].get_raw_stream()
print(fp.read())
```

### 객체 삭제

[//]: # (.cssg-snippet-delete-object-comp)
```python
# object 삭제
## deleteObject
response = client.delete_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject'
)

# 여러 object 삭제
## deleteObjects
response = client.delete_objects(
    Bucket='examplebucket-1250000000',
    Delete={
        'Object': [
            {
                'Key': 'exampleobject1',
            },
            {
                'Key': 'exampleobject2',
            },
        ],
        'Quiet': 'true'|'false'
    }
)
```
