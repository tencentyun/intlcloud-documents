## 기능 개요

COS 서명 도구는 COS에서 제공된 요청 서명을 생성하는데 사용되는 Web 도구입니다. COS 서명 도구 페이지에서 지정된 매개변수를 입력하여 요청 서명을 생성하고 요청 서명의 정확성을 검증할 수 있습니다.
- 현재 COS에는 XML 및 JSON, 두 가지 버전의 API가 제공됩니다. 두 가지 유형의 API 서명은 입력 매개변수가 다르며 COS에서 XML API를 사용하는 것을 권장합니다. JSON API는 사용자가 XML API를 시작하기 전에 COS에 접근할 수 있도록 제공하는 API입니다. JSON API는 표준 XML API와 기본 아키텍처가 동일하며 데이터는 상호 운용이 가능하며 교차 사용도 가능하지만 두 API는 호환될 수 없습니다.
- XML 버전의 서명에 대한 자세한 내용은 XML 버전의 [요청 서명](https://intl.cloud.tencent.com/document/product/436/7778)을 참조하십시오.
- JSON 버전의 서명에 대한 자세한 내용은 JSON 버전의 [요청 서명](https://cloud.tencent.com/document/product/436/6054)을 참조하십시오.

## 사용 방법

### XML 버전 서명 도구

#### COS 서명 도구 열기

[COS 서명 도구](https://cos5.cloud.tencent.com/static/cos-sign/)를 클릭하여 "COS 서명 도구" 페이지로 이동하십시오.

#### 기본 구성 정보 입력

"기본 정보" 란에 API 버전 및 서명 유효 기간을 기입하십시오.
![avatar](https://main.qcloudimg.com/raw/6855a2f6b18779037090e0769303bbc7.png)
기본 정보의 매개변수가 필수 항목입니다.
- API 버전: XML 버전 API를 선택하십시오.
- 서명 유효 기간: 서명의 유효한 기간입니다. [받기]를 클릭하면 유효 기간이 60분인 서명을 받을 수 있습니다. 유효한 시종 시간을 입력하여 현재 시종 시간 아래의 서명 결과를 복원하는 데 사용할 수도 있습니다. 서명 유효 기간에 대한 자세한 내용은 [요청 서명](https://intl.cloud.tencent.com/document/product/436/7778#.E7.AD.BE.E5.90.8D.E5.86.85.E5.AE.B9)을 참조하십시오.

#### API 키 정보 입력

다음과 같이 "API 키" 란에 API 키 정보를 입력하십시오.
![avatar](https://main.qcloudimg.com/raw/c28b93819a8fdd9e121e6b0702d098d4.png)
API 키의 정보가 필수 항목입니다.
- API 키 매개변수 정보는 콘솔의 [API 키 관리](https://console.cloud.tencent.com/cam/capi) 페이지에서 획득할 수 있습니다.
- 입력 시 해당 정보의 정확성을 확보하십시오. 잘 못 입력하면 무효 서명으로 간주될 수 있습니다.

#### HTTP 매개변수 정보 입력

“HTTP 매개변수” 란에 다음과 같이 관련 매개변수를 입력하십시오.
![avatar](https://main.qcloudimg.com/raw/8fbc5566b31777e646aa457239468cda.png)
주요 매개변수는 다음과 같습니다.
- **HttpMethod: **필수 항목입니다. HTTP 요청 방법에 GET, POST, PUT, DELETE 네 가지를 포함합니다.
- **HttpURI: **필수 항목입니다. HTTP 요청 URI 부분, 즉, 요청을 할 객체 이름입니다.
- **HttpParameters:**선택 항목입니다. HTTP 요청 매개변수입니다. url 매개변수를 검증할 경우 이 매개변수를 입력할 수 있습니다. 그중에 key는 소문자로 되어야 하며 value는 URLEncode를 필요로 하여 여러 개 key를 사전순으로 정렬합니다.
 예를 들어 "prefix=abc"는 지정된 접근 객체 접두사가 abc인 객체를 나타냅니다.
- **HttpHeaders:**선택 항목입니다. HTTP 요청 헤더입니다. url 매개변수를 검증할 경우 이 매개변수를 입력할 수 있습니다. 그중에 key는 소문자로 되어야 하며 value는 URLEncode를 필요로 하여 여러 개 key를 사전순으로 정렬합니다.
 예를 들어 "Host: bucket1-1254000000.cos.ap-beijing.myqcloud.com "은 해당 서명이 계정 1254000000의 버킷 bucket1 아래의 지정한 파일을 접근할 수 있음을 의미합니다.

관련 HTTP 요청 매개변수에 대한 자세한 내용은 [요청 서명](https://intl.cloud.tencent.com/document/product/436/7778#signature-.E8.AE.A1.E7.AE.97)을 참조하십시오.

#### 서명 생성 및 과정 매개변수 확인

[서명 생성]을 클릭하면 오른쪽에 있는 "결과 피드백"에서 다음과 같이 요청 서명 결과를 확인할 수 있습니다.
COS 서명 도구는 생성된 최종 서명 및 서명 계산 과정에서의 과정 매개변수를 각각 보여 줍니다. 관련 과정 매개변수에 대한 자세한 내용은 [요청 서명](https://intl.cloud.tencent.com/document/product/436/7778#signature-.E8.AE.A1.E7.AE.97)을 참조하십시오.

![avatar](https://main.qcloudimg.com/raw/4e5d3164848078e4ac2dc0b9b767ca00.png)

### JSON 버전 서명 도구

#### 기본 구성 정보 입력

1. [COS 서명 도구](https://cos5.cloud.tencent.com/static/cos-sign/)를 클릭하여 "COS 서명 도구" 페이지로 들어갑니다.
2. "기본 정보" 란에 다음과 같이 API 버전, 버킷 이름, 그리고 현재 시간을 기입합니다.
![avatar](https://main.qcloudimg.com/raw/8b764cd2bef9d2d64a3b8faeb26afff1.png)
API 키의 정보가 필수 항목입니다.
- API 버전: JSON 버전 API를 선택하십시오.
- 버킷 이름: 접근할 버킷의 이름을 입력하십시오. 예: bucketname-appid
- 현재 시간: 현재 시스템의 시간입니다. Unix Epoch 타임스탬프 규범에 맞는 수치이며 단위는 초입니다; 지정된 시간을 입력하여 지정된 타임스탬프 아래의 서명 결과를 복원하는 데 사용할 수도 있습니다.

#### API 키 정보 입력

"API 키" 란에 API 키 정보를 입력하십시오.
이 정보는 필수 옵션이며 콘솔의 [API 키 관리](https://console.cloud.tencent.com/cam/capi) 페이지에서 획득할 수 있습니다.
입력 시 해당 정보의 정확성을 확보하십시오. 잘 못 입력하면 무효 서명으로 간주될 수 있습니다.

#### HTTP 매개변수 정보 입력

“HTTP 매개변수” 란에 다음과 같이 관련 매개변수를 입력하십시오.
![avatar](https://main.qcloudimg.com/raw/621bd5458b8da2dcfc6eea7d707fecbb.png)
주요 매개변수는 다음과 같습니다.
- **ExpiredTime: **필수 항목입니다. 서명의 실효 시간이며 단위는 초입니다. [현재 시간] 매개변수에 유효 기간을 추가하여 서명의 실효 시간을 받을 수 있습니다. **단수 서명의 경우 실효 시간을 0으로 설정해야 합니다**.
- **RandomId: **필수 항목입니다. 무부호 10 진수 정수의 랜덤 직렬이 없습니다.
- ** FilePath: **선택 항목입니다. 스토리지 리소스의 상대 경로를 표시합니다. 형식은 /[dirname]/[filename]과 같습니다.
   -  조작 객체가 폴더일 경우 filename이 기본값입니다. filename에 파일 접미사를 포함해야 합니다.
   -  FilePath가 비어 있을 때 생성된 요청 서명은 버킷 내의 모든 대상의 접근에 적용됩니다.

해당 HTTP 요청 매개변수에 대한 자세한 내용은 [요청 서명](https://cloud.tencent.com/document/product/436/6054#.E8.8E.B7.E5.8F.96.E7.AD.BE.E5.90.8D.E6.89.80.E9.9C.80.E4.BF.A1.E6.81.AF)을 참조하십시오.

#### 서명 생성 및 과정 매개변수 확인

[서명 생성]을 클릭하면 오른쪽에 있는 "결과 피드백"에서 요청 서명 결과를 확인할 수 있습니다.
COS 서명 도구는 생성된 최종 서명 및 서명 계산 과정의 과정 매개변수를 각각 보여 줍니다. 관련 과정 매개변수에 대한 자세한 내용은 [서명 요청](https://cloud.tencent.com/document/product/436/6054#.E8.8E.B7.E5.8F.96.E7.AD.BE.E5.90.8D.E6.89.80.E9.9C.80.E4.BF.A1.E6.81.AF2)을 참조하십시오.

## 주의 사항
- 본 서명 도구는 사용자가 잘 못 입력한 매개변수를 식별하고 제시하지 않습니다. 본 도구를 사용하여 요청 서명을 계산하고 SDK 또는 다른 도구의 계산 결과와 비교한다면 본 도구는 사용자가 잘 못 입력한 매개변수를 능동적으로 교정하지 않습니다.
- 본 서명 도구는 사용자가 입력한 무효 매개변수를 식별하고 제시하지만 서명 검증을 통과하지 못하는 요청 서명이 생성될 수 있습니다.
- 본 서명 도구는 사용자가 아직 입력하지 않은 필수 매개변수 항목을 식별 및 제시하며, 필수 매개변수 항목을 완성하지 못할 경우 요청 서명을 생성할 수 없습니다.
