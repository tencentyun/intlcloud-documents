Amazon Simple Storage Service(Amazon S3, 이하 S3)는 AWS에서 출시한 최초의 클라우드 서비스 중 하나입니다. 수년간의 개발 끝에 S3 프로토콜은 객체 스토리지 분야에서 사실상의 표준이 되었습니다. Tencent COS(Cloud Object Storage)는 S3 호환 구현 방식을 제공하므로 대부분의 S3 호환 애플리케이션에서 COS 서비스를 직접 사용할 수 있습니다. 본 문서에서는 COS를 사용하도록 이러한 애플리케이션을 구성하는 방법을 설명합니다.

## 준비 작업

### 애플리케이션의 COS 서비스 사용 가능 여부 확인

- 설명에 `S3 Compatible`이 가능한 애플리케이션은 대부분의 경우 COS를 사용할 수 있습니다. 일부 기능이 제대로 작동하지 않는 경우 [고객센터](https://intl.cloud.tencent.com/contact-sales)에 도움을 요청하십시오. 본 문서의 가이드를 따랐음을 표시하고 애플리케이션 이름 및 스크린샷과 같은 정보를 제공하십시오.
- 애플리케이션 설명에 `Amazon S3`가 지원된다는 내용만 있으면 애플리케이션이 S3 서비스를 사용할 수 있지만 COS를 사용할 수 있는지 여부는 아래에 설명된 대로 관련 구성에서 추가로 평가해야 합니다.

### COS 서비스 준비

#### 1단계: Tencent Cloud 계정 가입

(이미 Tencent Cloud 계정이 있는 경우 이 단계를 생략할 수 있습니다.)

<div style="background-color:#00A4FF; width: 190px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/account/register" target="_blank"  style="color: white; font-size:16px;">Tencent Cloud 계정 가입</a></div>

#### 2단계: 실명 인증

(이미 완료한 경우 이 단계를 생략할 수 있습니다.)

<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/developer" target="_blank"  style="color: white; font-size:16px;"  hotrep="document.guide.3128.btn2">실명 인증하기</a></div>

자세한 인증 과정은 <a href="https://intl.cloud.tencent.com/document/product//378/3629">실명 인증 가이드</a>를 참고하십시오.

#### 3단계: COS 서비스 활성화

<div style="background-color:#00A4FF; width: 190px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/cos5" target="_blank"  style="color: white; font-size:16px;">COS 서비스 활성화</a></div>

<span id="step4"></span>
#### 4단계: APPID 및 액세스 키 준비

CAM 콘솔의 [API Keys](https://console.cloud.tencent.com/cam/capi) 페이지에서 **APPID**, **SecretId**, **SecretKey**를 획득 및 기록합니다.

![](https://qcloudimg.tencent-cloud.cn/raw/82216475f85f3bb8c9662e35998cbbc3.png)

<span id="step5"></span>
#### 5단계: 버킷 생성

[버킷 생성](https://intl.cloud.tencent.com/document/product//436/13309)의 지침에 따라 COS 버킷을 생성합니다.

일부 애플리케이션에는 버킷 생성 프로세스가 내장되어 있습니다. 이러한 애플리케이션이 버킷을 생성하도록 하려면 이 단계를 생략할 수 있습니다.


## 애플리케이션에서 COS 서비스 설정

### 기본 설정

대부분의 애플리케이션에는 스토리지 서비스를 사용하기 위한 유사한 구성 항목이 있습니다. 이러한 구성 항목의 일반 이름과 설명은 다음과 같습니다.

>? 설정 과정에서 궁금한 점이 있으시면 [고객센터](https://intl.cloud.tencent.com/contact-sales)로 문의하시기 바랍니다. 본 문서의 가이드를 따랐음을 표시하고 애플리케이션 이름 및 스크린샷과 같은 정보를 제공하십시오.
>


<table>
<thead>
<tr>
<th>설정 항목에서 흔히 볼 수 있는 이름</th>
<th>관련 설명</th>
</tr>
</thead>
<tbody>
<tr>
<td>공급자/서비스 공급자/<br>스토리지 서비스 공급자/<br>Service&nbsp;Provider/<br>Storage&nbsp;Provider/<br>Provider 등</td>
<td>애플리케이션이 사용해야 할 스토리지를 선택할 때 다음과 같은 상황이 있을 수 있습니다.<br><li>선택 항목에 S3 Compatible Storage/S3 Compatible과 같은 텍스트가 있는 경우 해당 옵션이 먼저 사용됩니다.<br></li><li>선택 항목에 amazon web services/AWS/Amazon S3와 같은 텍스트만 있는 경우 이를 사용하되 구성하는 동안 추가 지침에 주의하십시오.<br></li><li>비슷한 선택 항목이 없지만 애플리케이션 설명에 애플리케이션이 S3 서비스 또는 S3 호환 서비스를 지원한다고 언급하는 경우 아래 구성을 계속할 수 있지만 추가 지침에도 주의해야 합니다.<br></li><li>기타 다른 경우에는 애플리케이션이 COS를 사용하지 못할 수 있습니다.</li></td>
</tr>
<tr>
<td>서버/서버 주소/서비스&nbsp;URL/Endpoint/Custom Endpoint/Server URL 등</td>
<td>S3 호환 서비스의 서비스 주소 입력란입니다. COS 서비스 사용 시 여기에 COS 서비스 주소를 입력합니다(포맷: <code>cos.&lt;Region&gt;.myqcloud.com</code> 또는<br><code>https://cos.&lt;Region&gt;.myqcloud.com</code>).<br><code>https://</code> 입력 여부는 애플리케이션마다 조금씩 다르므로 직접 시도해 보시기 바랍니다. 이 중 <code>&lt;Region&gt;</code>는 COS의 사용 가능 리전을 의미합니다.<br>귀하는 애플리케이션에서 서비스 주소가 지정한 리전에서만 버킷을 생성 또는 선택할 수 있습니다.<br><li>귀하의 버킷이 광저우 리전에 있는 경우 서비스 주소는 <code>cos.ap-guangzhou.myqcloud.com</code>으로 설정되어 있어야 합니다. 기타 리전으로 설정한 경우 애플리케이션에서 광저우 리전의 버킷을 찾을 수 없습니다.<br><li>애플리케이션의 서비스 공급자 중 <code>Amazon S3</code>만 선택할 수 있고 서버 포트 설정이 가능한 경우 서버 포트를 위의 <code>cos.&lt;Region>.myqcloud.com</code> 또는 <code>https://cos.&lt;Region>.myqcloud.com</code>으로 수정합니다.<br><li>서버 포트 설정이 불가능하거나 서버 포트 설정 항목이 없는 경우 귀하의 애플리케이션은 COS 서비스를 사용할 수 없습니다.</td>
</tr>
<tr>
<td>Access Key/Access Key ID 등</td>
<td><a href="#step4">4단계</a>에서 기록된 <strong>SecretId</strong>를 입력하십시오.</td>
</tr>
<tr>
<td>Secret Key/Secret/<br>Secret Access Key 등</td>
<td><a href="#step4">4단계</a>에서 기록된 <strong>SecretKey</strong>를 입력하십시오.</td>
</tr>
<tr>
<td>리전/Region 등</td>
<td>기본값, 자동, Auto 또는 Automatic을 선택합니다.</td>
</tr>
<tr>
<td>버킷/Bucket 등</td>
<td>기존의 버킷 이름을 선택 또는 입력합니다. 포맷은 <code>&lt;BucketName-APPID&gt;</code>입니다(예: <code>examplebucket-1250000000</code>). 이 중 <code>BucketName</code>은 <a href="#step5">5단계</a>에서 버킷 생성 시 입력한 버킷 이름이며, <code>APPID</code>는 <a href="#step4">4단계</a>에서 기록한 <strong>APPID</strong>입니다.<br>위의 설명과 마찬가지로 이곳의 버킷은 서버 주소가 지정한 리전에 한정되어 있으며, 기타 리전의 버킷은 나열되지 않거나 정상적인 사용이 불가능합니다. 새로운 버킷을 생성해야 하는 경우 새로 생성된 버킷 이름도 위의 <code>&lt;BucketName-APPID&gt;</code> 포맷에 부합해야 합니다. 그렇지 않으면 정상적으로 버킷을 생성할 수 없습니다.</td>
</tr>
</tbody></table>


### 기타 항목 및 고급 설정 설명

일부 애플리케이션은 위의 기본 설정 외에도 기타 항목 및 고급 설정이 더 있습니다. 애플리케이션에서 COS 서비스를 원활하게 사용할 수 있도록 아래 일부 COS의 기능 설명을 추가합니다.

- 서버 포트와 프로토콜
  COS 서비스가 지원하는 HTTP 프로토콜과 HTTPS 프로토콜은 모두 프로토콜의 기본 포트인 80과 443 포트를 사용합니다. 보안상의 이유로 HTTPS 프로토콜을 통한 COS 서비스 사용을 권장합니다.
- Path-Style과 Virtual Hosted-Style
  COS는 두 종류의 스타일을 모두 지원합니다.
- AWS V2 서명과 AWS V4 서명
  COS는 두 종류의 서명 포맷을 모두 지원합니다.

## 결론

COS는 S3와의 완전한 호환성을 보장하지 않습니다. 애플리케이션에서 COS 사용 시 질문이 있는 경우 [고객센터](https://intl.cloud.tencent.com/contact-sales)에 도움을 요청하십시오. 본 문서의 가이드를 따랐음을 표시하고 애플리케이션 이름 및 스크린샷과 같은 정보를 제공하십시오.
