Python SDK V4와 XML Python SDK의 문서를 세심하게 비교해 보았다면 간단한 증분적 업데이트가 아님을 아셨을 것입니다. XML Python SDK는 아키텍처, 가용성 및 안전성 면에서 상당한 업그레이드가 이루어졌으며 사용성, 견고성 그리고 전송 성능에서도 많은 개선을 이루었습니다. XML Python SDK로 업그레이드하려면 아래 지침을 참조하여 Python SDK의 업그레이드 작업을 완료하십시오.

## 기능 비교

다음 표는 JSON Python SDK 및 XML Python SDK의 주요 기능 비교입니다.

| 기능       | XML Python SDK         | JSON Python SDK                         |
| -------- | :------------: | :------------------:    |
| 파일 업로드 | 로컬 파일, 바이트 스트림, 입력 스트림 업로드 지원<br>기본으로 업로드 덮어쓰기함<br>업로드 모드 스마트 지정, 중단점 재개 지원<br>간편 업로드 최대 5GB 지원<br>멀티파트 업로드 최대 48.82TB(50,000GB) 지원| 로컬 파일 업로드만 지원<br>덮어쓰기 여부 선택 가능<br>간편 업로드 또는 멀티파트 업로드를 수동으로 선택 필요<br>간편 업로드 최대 20MB 지원<br>멀티파트 업로드 최대 64GB 지원|
| 버킷 기본 조작 | 버킷 생성<br>버킷 획득<br>버킷 삭제   | 지원하지 않음 |
| 버킷 ACL 조작 | 버킷 ACL 설정<br>버킷 ACL 획득<br>버킷 ACL 삭제   | 지원하지 않음 |
| 버킷 수명 주기 | 버킷 수명 주기 생성<br>버킷 수명 주기 획득<br>버킷 수명 주기 삭제 | 지원하지 않음 |
| 디렉터리 조작 | API가 별도로 제공되지 않음   | 디렉터리 생성<br>디렉터리 조회<br>디렉터리 삭제 |


## 업그레이드 절차
아래 4단계를 수행하여 Python SDK를 업그레이드하십시오.
**1. Python SDK 업데이트**

pip 명령을 통해 편리하게 최신 XML Python SDK를 획득할 수 있습니다.
```
 pip uninstall qcloud_cos_v4

 pip install -U cos-python-sdk-v5
```

아니면 Python SDK [시작 가이드](https://cloud.tencent.com/document/product/436/12269) 문서를 참고하여 적절한 설치 방식을 선택하십시오.


**2. SDK 초기화 방식 변경**

XML Python SDK는 CosConfig 객체를 추가하여 COS에 액세스하는 구성을 관리합니다. 편리하게 액세스 프로토콜 HTTP/HTTPS, 임시 키 등의 정보를 설정할 수 있습니다. 다음 예제에 따라 SDK 초기화를 진행하십시오.

JSON Python SDK의 초기화 방식은 다음과 같습니다.

```
secret_id = u'COS_SECRETID'      # 사용자의 secretKey로 대체합니다.
secret_key = u'COS_SECRETKEY'      # 사용자의 secretKey로 대체합니다.
region = 'sh'                # 사용자의 지역으로 대체합니다.
appid = 100000               # 사용자의 appid로 대체합니다
cos_client = CosClient(appid, secret_id, secret_key, region=region)
```

XML Python SDK의 초기화 방식은 다음과 같습니다.

```
# appid는 구성 중에서 제거되었으므로 매개변수 버킷에 appid를 넣으십시오. Bucket은 bucketname-appid로 구성됩니다.
# 1. 사용자 구성을 설정하며 secretId, secretKey 및 Region을 포함합니다.
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import logging

logging.basicConfig(level=logging.INFO, stream=sys.stdout)

secret_id = 'COS_SECRETID'      # 사용자의 secretKey로 대체합니다.
secret_key = 'COS_SECRETKEY'      # 사용자의 secretKey로 대체합니다.
region = 'ap-shanghai'      # 사용자의 지역으로 대체합니다.
token = None                # 임시 키를 사용하려면 Token이 전송되어야 합니다. 기본적으로 비어 있으며 입력하지 않아도 됩니다.
scheme = 'https'            # http/https 프로토콜을 사용하여 COS에 액세스하도록 지정하며 기본으로 https이고 입력하지 않아도 됩니다.
config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
# 2. 클라이언트 객체 가져오기
client = CosS3Client(config)
```


**3. 버킷 이름 및 가용 영역 약칭 변경**

XML Python SDK의 버킷 이름과 가용 영역의 약칭은 JSON Python SDK와 다르므로 상응하는 변경을 진행해야 합니다.

**버킷 Bucket**
XML Python SDK 버킷 이름은 사용자 지정 문자열과 APPID의 두 부분으로 구성되며 둘은 대시 "-"로 연결됩니다.
예를 들어 `mybucket1-1250000000`이라면 그 중 `mybucket1`은 사용자 지정 문자열이고 `1250000000`은 APPID입니다.
>?APPID는 Tencent Cloud 계정의 계정 식별자 중 하나이며 클라우드 리소스를 연결하는 데 사용됩니다. 사용자가 Tencent Cloud 계정을 성공적으로 신청한 후 시스템은 자동으로 APPID를 사용자에게 할당합니다. [Tencent Cloud 콘솔](https://console.cloud.tencent.com/)의 [계정 정보]에서 APPID를 볼 수 있습니다.

버킷 설정은 다음의 예제 코드를 참조하십시오.
```
bucket = "examplebucket-1250000000"
file_name = "test.txt"
local_path = 'local.txt'
response = client.upload_file(
    Bucket=bucket,
    LocalFilePath=local_path,
    Key=file_name
)
```


**버킷 가용 영역 약칭 Region**

XML Python SDK의 버킷 가용 영역 약칭에 변경 사항이 있으며, 초기화 시 버킷이 있는 영역의 약칭을 CosConfig로 설정하십시오. 서로 다른 지역의 JSON Python SDK 및 XML Python SDK의 대응 관계는 다음 표를 참조하십시오.

| 지역       | XML Python SDK 지역 약칭         | JSON Python SDK 지역 약칭                         |
| -------- | ------------ | ---------------------------------------- |
| 베이징 1지역(화북) | ap-beijing-1 | tj |
| 베이징       | ap-beijing   | bj |
| 상하이(화동)   | ap-shanghai  | sh |
| 광저우(화남)   | ap-guangzhou | gz |
| 청두(서남)   | ap-chengdu   | cd |
| 충칭       | ap-chongqing | 없음 |
| 싱가포르      | ap-singapore | sgp |
| 홍콩       | ap-hongkong  | hk |
| 토론토      | na-toronto   | ca |
| 프랑크푸르트     | eu-frankfurt | ger |
| 뭄바이       | ap-mumbai    | 없음 |
| 서울       | ap-seoul     | 없음 |
| 실리콘 밸리       | na-siliconvalley     | 없음 |
| 버지니아       | na-ashburn     | 없음 |
| 방콕       | ap-bangkok     | 없음 |
| 모스크바       | eu-moscow     | 없음 |


**4. API 변경**
XML Python SDK로 업그레이드한 후 일부 조작의 API가 변경되므로 실제 필요에 따라 변경하십시오. 동시에 SDK를 보다 편하게 이용할 수 있도록 캡슐화했으므로 자세한 내용은 예제와 [API 문서](https://cloud.tencent.com/document/product/436/12270)를 참조하십시오.
API 변경 내용은 다음의 네 가지입니다.

**1)독립적인 디렉터리 API 없음**

XML SDK에서는 별도의 디렉토리 API를 더 이상 제공하지 않습니다. COS에 폴더와 디렉터리라는 게 없으며 COS는 객체 `project/a.txt`가 업로드되기 때문에 project 폴더를 생성하지 않습니다. 사용자의 사용 습관을 충족시키기 위해 COS는 콘솔이나 COS browser와 같은 그래픽 도구에 [폴더] 또는 [디렉터리] 표시 방식을 시뮬레이션합니다. 이는 키 값이 `project/`이고 내용이 비어 있는 객체를 생성하여 구현하며, 표시 방식은 기존 폴더와 유사합니다.

예: 객체 `project/doc/a.txt`를 업로드하면 구분 기호 `/`는 [폴더]의 표시 방식을 시뮬레이션하여 [폴더] project와 doc를 콘솔에서 볼 수 있습니다. 그 중 doc는 project 하위 [폴더]이며 a.txt 파일을 포함합니다.

따라서 사용 시나리오가 단지 파일 업로드인 경우, 먼저 폴더를 생성하지 않고 파일을 직접 업로드하면 됩니다. 만일 사용 시나리오에 폴더가 필요해 폴더를 생성해야 할 경우, 경로가 ` / `로 끝나는 0KB의 파일을 업로드하면 됩니다. 이렇게 하면 GetBucket API를 호출할 때 해당 파일을 폴더로 사용할 수 있습니다.



**2)고급 업로드 API**

XML SDK에서 고급 업로드 API를 캡슐화하여 해당 API가 파일 크기에 따라 지능형으로 간편 업로드와 멀티파트 업로드 중에서 선택할 수 있습니다. 멀티파트 업로드는 중단점 재개 기능을 갖추고 있으며 스레드 수량을 설정하여 업로드 속도를 제어할 수 있습니다.

고급 업로드 API 사용 시 중단점 재개의 예제 코드는 다음과 같습니다.

```
response = client.upload_file(
    Bucket='examplebucket-1250000000',
    LocalFilePath='local.txt',
    Key=file_name,
    PartSize=10,
    MAXThread=10
)
```

**3)서명 알고리즘이 다름**

일반적으로 수동으로 서명을 계산할 필요가 없지만, SDK의 서명을 프런트 엔드에 반환하는 경우 서명 알고리즘에 변화가 생겼다는 점에 유의하십시오. 서명은 더 이상 단일 서명과 다중 서명을 구분하지 않으며 서명의 유효 기간을 설정하여 보안성을 보장합니다. 구체적인 알고리즘은 [XML 서명 요청](https://intl.cloud.tencent.com/document/product/436/7778) 문서를 참조하십시오.

**4) API 새로 추가**

XML Python SDK는 API를 새로 추가하여 필요에 따라 호출할 수 있습니다. 다음을 포함합니다.

* 버킷의 조작, 즉 create_bucket, delete_bucket, list_objects 등입니다.
* 버킷 ACL의 조작, 즉 put_bucket_acl, get_bucket_acl 등입니다.
* 버킷의 수명 주기 조작, 즉 put_bucket_lifecycle, get_bucket_lifecycle 등입니다.

자세한 내용은 Python SDK [API 문서](https://cloud.tencent.com/document/product/436/12270)를 참조하십시오.
