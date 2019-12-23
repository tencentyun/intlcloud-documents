JSON JavaScript SDK와 비교하면 XML JavaScript SDK는 간단히 점진적 업데이트된 것이 아니라 구조, 가용성과 보안성이 크게 높아졌으며 사용 간편성과 성능 면에서도 엄청나게 큰 개선을 했습니다. XML JavaScript SDK로 업그레이드하려면 다음 안내에 따라 JavaScript SDK 업그레이드 작업을 완료하시기 바랍니다.

## 기능 비교

| 기능           |                     XML JavaScript SDK                      |                     JSON JavaScript SDK                     |
| -------------- | :----------------------------------------------------------: | :----------------------------------------------------------: |
| 파일 업로드       | 로컬 파일, 문자열 내용 지원<br>기본으로 업로드 시 덮어쓰기<br/>멀티파트 업로드는 배치 업로드 지원<br>업로드 모드 스마트 선택: 간편 업로드는 최대 5GB 지원<br>멀티파트 업로드는 최대 48.82TB(50,000GB) 지원 | 로컬 파일 업로드만 지원<br>덮어쓰기 여부 선택가능<br/>20MB보다 작거나 같으면 간편 업로드 사용. 20MB보다 크면 자동 멀티파트 업로드<br>간편 업로드는 최대 20MB 지원<br>멀티파트 업로드는 최대 64GB 지원 |
| 파일 삭제       |                         배치 삭제 지원                         |                       다일 파일 삭제만 지원                       |
| 버킷 기본 작업 |            버킷 생성<br>버킷 획득<br>버킷 삭제            |                            지원되지 않음                            |
| 버킷 ACL 작업  |   버킷 ACL 설정<br>버킷 ACL 획득<br>버킷 ACL 삭제    |                            지원하지 않음                            |
| 버킷 수명 주기 | 버킷 수명 주기 생성<br>버킷 수명 주기 획득<br>버킷 수명 주기 삭제 |                            지원되지 않음                            |
| 디렉토리 조작       |                        API 별도로 제공하지 않음                        |               디렉토리 생성<br>디렉토리 조회<br>디렉토리 삭제               |
| 임시 키 사용   |                     임시 키 지원과 추천                     |                        임시 키 지원되지 않음                        |

## 업그레이드 절차

#### 1. JavaScript SDK 업데이트

XML JavaScript SDK는 [npm](https://www.npmjs.com/package/cos-js-sdk-v5) 레지스트리에 배포되며, npm으로 필요한 의존 패키지 설치를 추천합니다.

```js
npm install cos-js-sdk-v5
```

github 소스 코드에서 js 파일 [dist/cos-js-sdk-v5.min.js](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/dist)을 다운로드하고 script 태그를 통해 페이지 html에 추가해도 됩니다.

```html
<script src="./cos-js-sdk-v5.min.js"></script>
```

#### 2. 버킷 이름과 가용 영역 약칭 변경

XML JavaScript SDK의 버킷 이름과 가용 영역 약칭은 JSON JavaScript SDK와 다르며 그에 맞게 변경해야 합니다.

#### 버킷 Bucket

XML JavaScript SDK 버킷 이름은 사용자 지정 문자열과 APPID의 두 부분으로 구성되며 양자 사이에 대시 “-”로 연결됩니다.
예를 들어 `examplebucket-1250000000`, 여기서 `examplebucket`은 사용자 지정 문자열이고, `1250000000`은 APPID입니다.

> ?APPID는 Tencent Cloud 계정의 ID 중 하나이며, 클라우드 리소스 연결에 사용됩니다. 사용자가 Tencent Cloud 계정을 신청하면 시스템은 자동으로 사용자에게 하나의 APPID를 할당합니다. [Tencent Cloud 콘솔](https://console.cloud.tencent.com/)의 [계정 정보]를 통해 APPID를 조회할 수 있습니다.

버킷 설정은 다음 업로드 예제 코드를 참조하십시오.

```js
cos.getBucket({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
}, function (err, data) {
    console.log(err || data);
});
```

#### 버킷 가용 영역 약칭 Region

XML JavaScript SDK의 버킷 가용 영역 약칭에 변화 사항이 있으며, 각 지역의 JSON JavaScript SDK와 XML JavaScript SDK에서의 대응 관계는 다음 표를 참조하시기 바랍니다.

| 지역             | XML SDK 지역 약칭      | JSON SDK 지역 약칭 |
| ---------------- | ---------------- | ----------- |
| 베이징 1지역(화북) | ap-beijing-1     | tj          |
| 베이징             | ap-beijing       | bj          |
| 상하이(화동)     | ap-shanghai      | sh          |
| 광저우(화남)     | ap-guangzhou     | gz          |
| 청두(서남)     | ap-chengdu       | cd          |
| 충칭             | ap-chongqing     | 없음          |
| 싱가포르           | ap-singapore     | sgp         |
| 홍콩             | ap-hongkong      | hk          |
| 토론토           | na-toronto       | ca          |
| 프랑크푸르트         | eu-frankfurt     | ger         |
| 뭄바이             | ap-mumbai        | 없음          |
| 서울             | ap-seoul         | 없음          |
| 실리콘 밸리             | na-siliconvalley | 없음          |
| 버지니아         | na-ashburn       | 없음          |
| 방콕             | ap-bangkok       | 없음          |
| 모스크바           | eu-moscow        | 없음          |

[지역과 접근 도메인 이름](https://cloud.tencent.com/document/product/436/6224) 문서를 참고해도 됩니다.

각 방식을 호출할 때 버킷 소재 영역의 약칭을 매개변수 `Region`에 설정하십시오.

```java
cos.headBucket({
    Bucket: 'examplebucket-1250000000,
    Region: 'ap-beijing',
}, function (err, data) {
    console.log(err || data);
});
```

#### 3. API 변경

XML JavaScript SDK로 업그레이드한 후에 일부 작업의 API가 변경되었으니 실제 필요에 따라 그에 맞게 변경하십시오.

동시에 SDK를 더욱 쉽게 사용하도록 캡슐화했으며, 구체적인 사항은 [예제 코드](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/demo)와 [API 문서](https://cloud.tencent.com/document/product/436/12260)를 참조하십시오.

API의 주요 변화는 다음과 같습니다.

**1)독립적인 디렉터리 API 없음**

XML SDK에서는 개별적인 디렉토리 API를 더 이상 제공하지 않습니다. COS 자체는 폴더와 디렉토리라는 개념이 없으며, 업로드 객체 `project/a.txt`를 위해 하나의 project 폴더를 생성하지 않습니다. 사용자 사용습관을 충족시키기 위해 COS는 콘솔, COSBrowser 등 그래픽 도구에서 「폴더」 또는 「디렉토리」의 표시방식을 시뮬레이션합니다. 이는 구체적으로 하나의 키값이 `project/`이고 내용이 비어 있는 객체를 생성하여 구현하며, 표시 방식에서 전통적인 폴더를 시뮬레이션했습니다.

예를 들어 업로드 객체 `project/doc/a.txt`의 구분자 `/`는 「폴더」의 표시 방식을 시뮬레이션하기 때문에 콘솔에 「폴더」 project와 doc가 나타나고, 여기서 doc는 project 하위 「폴더」이고 a.txt 파일을 포함합니다.

따라서 단지 파일 업로드 시나리오의 경우, 바로 업로드하면 되며, 먼저 폴더를 생성할 필요가 없습니다. 적용 시나리오에 폴더의 개념이 있으면 폴더를 생성하는 기능을 제공해야 합니다. 경로가 `/`로 끝나는 0KB 파일 하나를 업로드하면 됩니다. 그러면 GetBucket API를 사용했을 때 해당 파일을 폴더로 할 수 있습니다.

**2)임시 키 사용하여 인증**

키를 프론트 엔드 코드에 놓으면 보안 리스크가 있고 백 엔드 계산 서명이 프론트 엔드에 주는 권한을 제어하기 쉽지 않기 때문에 XML  JavaScript SDK는 임시 키를 사용하도록 권장합니다. 구체적인 코드는 다음의 완전한 업로드 예시를 참고합니다.

```js
var Bucket = 'examplebucket-1250000000';
var Region = 'ap-beijing';
var cos = new COS({
    getAuthorization: function (options, callback) {
        var url = 'http://example.com/sts.php';
        var xhr = new XMLHttpRequest();
        xhr.open('GET', url, true);
        xhr.onload = function (e) {
            try {
                var data = JSON.parse(e.target.responseText);
                var credentials = date.credentials;
            } catch (e) {
            }
            callback({
                TmpSecretId: credentials.tmpSecretId,
                TmpSecretKey: credentials.tmpSecretKey,
                XCosSecurityToken: credentials.sessionToken,
                ExpiredTime: data.expiredTime,
            });
        };
        xhr.send();
    }
});
cos.putObject({
    Bucket: Bucket,
    Region: Region,
    Key: file.name,
    Body: file,
    onProgress: function (progressData) {
        console.log('업로드 중', JSON.stringify(progressData));
    },
}, function (err, data) {
    console.log(err, data);
});
```

여전히 백그라운드에서 수동으로 서명을 계산하고 다시 프론트 엔드에 반환하는 방식을 사용하는 경우, 서명 알고리즘에 변화가 생겼다는 점에 유의하십시오. 서명은 더 이상 1회 및 여러 차례 서명을 구분하지 않고 서명의 유효기간 설정을 통해 보안성을 보장합니다. [XML 서명 요청](https://intl.cloud.tencent.com/document/product/436/7778) 파일을 참고하여 서명을 업데이트하십시오.

**3)매개변수와 반환값 동일 형식**

매개변수는 하나의 객체이며 일부 도구 법을 제외하고 API는 모두 하나의 콜백을 통해 오류 정보 또는 성공 결과를 반환합니다. 다음 예시와 같습니다.

```js
cos.putObject({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing-1',
    Key: '1.txt',
}, function (err, data) {
    console.log(err || data);
});
```

**4) API 새로 추가**

XML JavaScript SDK에 API가 추가되었으며 필요에 따라 이를 호출할 수 있습니다. 다음을 포함합니다.

- getService, putBucket, getBucket 등과 같은 버킷의 작업.
- getBucketAcl, putBucketAcl 등과 같은 버킷 ACL의 작업.
- putBucketPolicy, getBucketPolicy, deleteBucketPolicy와 같은 버킷 정책의 작업.
- putBucketLifecycle, getBucketLifecycle, deleteBucketLifecycle과 같은 버킷 수명 주기의 작업.
- 객체 ACL 작업: getObjectAcl, putObjectAcl.
- 객체 복사 조작: putObjectCopy, sliceCopyFile
- 도구 방법: getObjectUrl
- 객체 업로드 대기열: pauseTask, restartTask, cancelTask, getTaskList 방법 및 list-update 이벤트.

더 자세한 사항은 [JavaScript SDK API 문서](https://cloud.tencent.com/document/product/436/12260)를 참조하십시오.
