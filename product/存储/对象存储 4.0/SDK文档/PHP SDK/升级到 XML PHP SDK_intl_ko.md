JSON PHP SDK와 XML PHP SDK의 문서를 세심하게 비교해 보았다면, 간단한 증분적인 업데이트 아님을 알게 될 겁니다. XML PHP SDK는 아키텍처, 가용성 및 보안성이 크게 향상되었을 뿐만 아니라 사용 편의성, 견고성 그리고 전송 성능에서도 많은 개선이 이루어졌습니다. PHP SDK를 XML PHP SDK로 업그레이드하려면 다음 가이드를 참조하십시오.

## 기능 비교

다음 표는 JSON PHP SDK 및 XML PHP SDK의 주요 기능 비교입니다.

| 기능           | XML PHP SDK             |  JSON PHP SDK                              |
| -------- | :------------: | :------------------:    |
| 파일 업로드 | 로컬 파일, 바이트 스트림, 입력 스트림 업로드 지원<br>기본으로 업로드 덮어쓰기함<br>업로드 모드 스마트 지정<br>간편 업로드 최대 5G 지원<br>멀티파트 업로드 최대 48.82TB(50,000GB) 지원 | 로컬 파일 업로드만 지원<br>덮어쓰기 여부 선택 가능<br>간편 업로드 또는 멀티파트 업로드의 선택 수동 구성 필요<br>간편 업로드 최대 20MB 지원<br>멀티파트 업로드 최대 64GB 지원|
| 파일 삭제 | 배치 삭제 지원 | 단일 파일 삭제만 지원 |
| 버킷 기본 조작 | 버킷 생성<br>버킷 획득<br>버킷 삭제   | 지원하지 않음 |
| 버킷 ACL 조작 | 버킷 ACL 설정<br>버킷 ACL 획득<br>버킷 ACL 삭제   | 지원하지 않음 |
| 버킷 수명 주기 | 버킷 수명 주기 생성<br>버킷 수명 주기 획득<br>버킷 수명 주기 삭제 | 지원하지 않음 |
| 디렉터리 조작 | API가 별도로 제공되지 않음   | 디렉터리 생성<br>디렉터리 조회<br>디렉터리 삭제 |


## 업그레이드 절차
아래 4단계를 수행하여 PHP SDK를 업그레이드하십시오.

**1. PHP SDK 업데이트**

COS XML PHP SDK를 설치하는 데 세 가지 방법이 있습니다.
* Composer 방식.
* Phar 방식.
* 소스 코드 방식

**Composer 방식**
사용자가 Composer를 사용하여 COS XML PHP SDK를 설치할 것을 권장합니다. Composer는 PHP의 중속성 관리 도구로서, 프로젝트가 필요로 하는 중속성을 선언하고, 자동으로 프로젝트에 설치할 수 있습니다.

>?[Composer 공식 웹사이트](https://getcomposer.org/)에서 Composer 설치 방법, 자동 로드 구성 및 의존 항목을 정의하는 데 사용하는 기타 모범 사례 등에 관한 더 많은 내용을 찾을 수 있습니다.

Composer를 사용하여 XML PHP SDK를 설치하는 절차는 다음과 같습니다.
1)터미널을 엽니다.
2)Composer를 다운로드합니다. 다음 명령을 실행합니다.
```
curl -sS https://getcomposer.org/installer | php
```
3)이름이 `composer.json`인 파일을 생성합니다. 내용은 다음과 같습니다.
```
{
    "require": {
        "qcloud/cos-sdk-v5": "1.*"
    }
}
```
4)Composer 사용하여 설치합니다. 다음 명령을 실행합니다.
```
php composer.phar install
```
해당 명령을 사용한 후 현재 디렉터리에서 vendor 폴더를 생성하여, 그 안에 SDK의 의존 라이브러리 및 autoload.php 스크립트를 포함하며, 사용자가 자신의 프로젝트에서 편리하게 호출할 수 있습니다.

5)autoloader 스크립트를 통해 XML PHP SDK를 호출합니다.
```
require '/path/to/sdk/vendor/autoload.php';
```

이로써 프로젝트는 COS XML PHP SDK를 사용할 준비가 되었습니다.


**Phar 방식**
Phar 방식으로 XML PHP SDK를 설치하는 절차는 다음과 같습니다.

1)[Github 릴리스 페이지](https://github.com/tencentyun/cos-php-sdk-v5/releases)에서 해당하는 phar 파일을 다운로드합니다.

2)코드에 Phar 파일 가져옵니다.
```
require  '/path/to/cos-sdk-v5.phar';
```

**소스 코드 방식**
소스 코드 방식으로 SDK를 설치하는 절차는 다음과 같습니다.

1)[Github 릴리스 페이지](https://github.com/tencentyun/cos-php-sdk-v5/releases)에서 해당하는 cos-sdk-v5.tar.gz 압축 파일을 다운로드합니다.

2)압축을 풀고 autoload.php 스크립트를 통해 SDK를 로드합니다.
```
require '/path/to/sdk/vendor/autoload.php';
```

**2. SDK 초기화 방식 변경**

XML PHP SDK에서 초기화 API에서 몇 가지 변경 사항이 발생했습니다. 그에 따라 수정을 진행하십시오.

JSON PHP SDK의 초기화 방식은 다음과 같습니다:

```
require('cos-php-sdk-v4/include.php');
use Qcloud\Cos\Api;
//COSClientConfig 객체를 생성하고, 필요에 따라 기본 설정의 구성 매개변수를 수정합니다.
$config = array(
    'app_id' => '',
    'secret_id' => '',
    'secret_key' => '',
    'region' => 'gz',
    'timeout' => 60
);
//cosApi 객체를 생성하고, COS 작업을 구현합니다.
$cosApi = new Api($config);
```

XML PHP SDK의 초기화 방식은 다음과 같습니다.

```
require '/path/to/sdk/vendor/autoload.php';
$cosClient = new Qcloud\Cos\Client(array('region' => getenv('COS_REGION'),
    'credentials'=> array(
        'secretId'    => getenv(' COS_SECRETID'),
        'secretKey' => getenv(' COS_SECRETKEY'))));
```


**3. 버킷 이름 및 가용 영역 약칭 변경**

XML PHP SDK의 버킷 이름과 가용 영역의 짧은 이름은 JSON PHP SDK와 다르므로 상응하는 변경을 진행해야 합니다.

**버킷 Bucket**
XML PHP SDK 버킷 이름은 사용자 지정 문자열과 APPID의 두 부분으로 구성되며 둘은 대시 "-"로 연결됩니다.
예를 들어 `examplebucket-1250000000`, 그 중 `examplebucket`은 사용자 지정 문자열이고 `1250000000`은 APPID입니다.

>?APPID는 Tencent Cloud 계정의 계정 ID이며, 클라우드 리소스를 연결하는 데 사용됩니다. 사용자가 Tencent Cloud 계정을 성공적으로 신청한 후, 시스템은 자동으로 APPID를 사용자에게 할당합니다. [Tencent Cloud 콘솔](https://console.cloud.tencent.com/)에 로그인하고, [계정 정보]에서 APPID를 볼 수 있습니다.

**버킷 가용 영역 약칭 Region**
XML PHP SDK의 버킷 가용 영역 짧은 이름이 변경됩니다. 초기화 시에 다음 표에 따라 region 필드를 입력하십시오.

| 지역             | XML PHP SDK 지역 짧은 이름      | JSON PHP SDK 지역 짧은 이름 |
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
XML PHP SDK로 업그레이드한 후 일부 조작의 API가 변경되므로 실제 필요에 따라 변경하십시오. 동시에 SDK를 보다 편하게 이용할 수 있도록 캐슐화하였습니다. 자세한 내용은 예시와 [API 문서](https://cloud.tencent.com/document/product/436/12267)를 참조하십시오.

API 변경 내용은 다음의 세 가지입니다.

**1)독립적인 디렉터리 API 없음**

XML SDK에서는 개별적인 디렉토리 API를 더 이상 제공하지 않습니다. COS 자체는 폴더와 디렉토리라는 개념이 없으며, 업로드 객체 `project/a.txt`를 위해 하나의 project 폴더를 생성하지 않습니다. 사용자 사용습관을 충족시키기 위해 COS는 콘솔, COS browser 등 그래픽 도구에서 [폴더] 또는 [디렉토리]의 표시방식을 시뮬레이션합니다. 이는 구체적으로 하나의 키값이 `project/`이고 내용이 비어 있는 객체를 생성하여 구현하며, 표시 방식에서 전통적인 폴더를 시뮬레이션했습니다.

예를 들어 업로드 객체 `project/doc/a.txt`의 구분자 `/`는 「폴더」의 표시 방식을 시뮬레이션하기 때문에 콘솔에 「폴더」 project와 doc가 나타나고, 여기서 doc는 project 하위 「폴더」이고 a.txt 파일을 포함합니다.

따라서 단지 파일 업로드 시나리오의 경우, 바로 업로드하면 되며, 먼저 폴더를 생성할 필요가 없습니다. 적용 시나리오에 폴더의 개념이 있으면 폴더를 생성하는 기능을 제공해야 합니다. 경로가 `/ `로 끝나는 0KB 파일 하나를 업로드하면 됩니다. 그러면 `GetBucket` API를 사용했을 때 해당 파일을 폴더로 할 수 있습니다.

**2)서명 알고리즘이 다름**

일반적으로 수동으로 서명을 계산할 필요가 없지만, SDK의 서명을 프런트 엔드에 반환하는 경우 서명 알고리즘에 변화가 생겼다는 점에 유의하십시오. 서명은 더 이상 단일 서명과 다중 서명을 구분하지 않으며 서명의 유효 기간을 설정하여 보안성을 보장합니다. 구체적인 알고리즘은 [XML 서명 요청](https://intl.cloud.tencent.com/document/product/436/7778) 문서를 참조하십시오.


**3) API 새로 추가**

XML PHP SDK가 많은 API를 새로 추가할 수 있으며, 다음을 포함합니다.
* 버킷 작업, 예 PutBucketRequest, GetBucketRequest, ListBucketRequest 등.
* 버킷 ACL의 작업, PutBucketACLRequest, GetBucketACLRequest 등.
* 버킷의 수명 주기 작업, PutBucketLifecycleRequest, GetBucketLifecycleRequest 등.

자세한 내용은 PHP SDK [API 문서](https://cloud.tencent.com/document/product/436/12267)를 참조하십시오.
