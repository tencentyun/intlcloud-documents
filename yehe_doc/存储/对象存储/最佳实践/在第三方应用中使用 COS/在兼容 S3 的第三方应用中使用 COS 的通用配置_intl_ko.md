Amazon Simple Storage Service(Amazon S3, 이하 S3)는 AWS가 최초로 출시한 클라우드 서비스 중 하나입니다. 오랜 발전을 거치면서 S3 프로토콜은 객체 스토리지 업계에서 사실상 표준이 되었습니다. Tencent Cloud COS(이하 COS)는 S3 호환 솔루션을 제공하여 대부분의 S3 호환 애플리케이션에서 직접 COS 서비스를 이용할 수 있습니다. 본 문서는 이러한 애플리케이션에서 COS 서비스 사용을 위한 설정 방법을 중점적으로 소개합니다.

## 준비 작업

### 애플리케이션의 COS 서비스 사용 가능 여부 확인

- 애플리케이션의 설명에서 `S3 Compatible`과 같은 문구가 나오면 대부분의 경우 COS 서비스를 사용할 수 있습니다. 실제 사용 과정에서 애플리케이션의 일부 기능을 정상적으로 사용할 수 없는 경우 Tencent Cloud의 [Submit Ticket](https://console.cloud.tencent.com/workorder/category)으로 문의 바랍니다. 티켓 제출 시 해당 문서에서 가이드를 보고 문의한다는 내용과 함께 관련된 애플리케이션 이름, 화면 캡처 등의 정보를 알려 주시면 더 빨리 문제 해결을 도와드릴 수 있습니다.
- 애플리케이션이 `Amazon S3`만 지원하는 경우 해당 애플리케이션에서 S3 서비스를 사용할 수 있음을 의미하지만, COS 서비스의 사용 가능 여부는 관련 설정에서 추가 확인이 필요합니다. 본 문서에서도 뒷부분의 설정 내용에서 자세히 설명하고 있습니다.

### COS 서비스 준비

#### 1단계: Tencent Cloud 계정 생성

(이미 Tencent Cloud 계정이 있는 경우 이 단계를 생략할 수 있습니다.)

<div style="background-color:#00A4FF; width: 190px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F" target="_blank"  style="color: white; font-size:16px;">Tencent Cloud 계정 생성</a></div>

#### 2단계: 실명 인증

(이미 완료한 경우 이 단계를 생략할 수 있습니다.)

<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/developer" target="_blank"  style="color: white; font-size:16px;"  hotrep="document.guide.3128.btn2">실명 인증</a></div>

자세한 인증 과정은 <a href="https://intl.cloud.tencent.com/document/product/378/3629">실명 인증 소개</a>를 참조하십시오. 실명 인증을 하지 않은 사용자는 중국 내 COS 서비스를 구매할 수 없습니다.

#### 3단계: COS 서비스 활성화

<div style="background-color:#00A4FF; width: 190px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/cos5" target="_blank"  style="color: white; font-size:16px;">COS 서비스 활성화</a></div>

<span id="step4"></span>
#### 4단계: APPID 및 액세스 키 준비

CAM 콘솔의 [API Keys](https://console.cloud.tencent.com/cam/capi) 페이지에서 **APPID**, **SecretId**, **SecretKey**를 획득 및 기록합니다.

![](https://main.qcloudimg.com/raw/9a328839005ea842f917fcd04acdd118.png)

<span id="step5"></span>
#### 5단계: 버킷 생성

일부 애플리케이션에는 버킷 생성 과정이 내장되어 있습니다. 애플리케이션에서 버킷을 생성하도록 하려면 이 단계를 생략할 수 있습니다.

1. [COS 콘솔](https://console.cloud.tencent.com/cos5) 왼쪽 메뉴에서 [버킷 리스트]를 클릭하여 버킷 관리 페이지로 이동합니다.
2. [버킷 생성]을 클릭하여 버킷 정보를 입력합니다.
	- 이름: 버킷 이름입니다(예: examplebucket).
	- 소속 리전: 버킷이 저장된 리전입니다. 본인과 가장 가까운 지역을 선택합니다(예: ‘선전’에 있는 경우 리전을 ‘광저우’로 선택).
	- 액세스 권한: 버킷 액세스 권한입니다. ‘개인 읽기/쓰기’를 선택합니다.
		![](https://main.qcloudimg.com/raw/f8582be0ef7e9cc7bcd52b607e619d4c.png)
3. [확인]을 클릭하면 버킷이 생성됩니다.


## 애플리케이션에서 COS 서비스 설정

### 기본 설정

대부분의 애플리케이션은 사용할 스토리지 서비스를 설정할 때 비슷한 설정 항목이 있습니다. 다음은 이러한 설정 항목에서 흔히 볼 수 있는 이름과 관련 설명입니다.

> 설정 과정에서 궁금한 점이 있으면 [Submit Ticket](https://console.cloud.tencent.com/workorder/category)으로 문의 바랍니다. 티켓 제출 시 해당 문서에서 가이드를 보고 문의한다는 내용과 함께 관련된 애플리케이션 이름, 화면 캡처 등의 정보를 알려 주시면 더 빨리 문제 해결을 도와드릴 수 있습니다.


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
<td>애플리케이션이 사용해야 할 스토리지를 선택할 때 다음과 같은 상황이 있을 수 있습니다.<br><li>해당 선택 항목에 S3 호환 스토리지/S3 Compatible과 같은 문구의 선택 항목이 있는 경우 이 항목을 우선 사용합니다.<br></li><li>amazon web services/AWS/Amazon S3과 같은 문구만 있는 경우 이 항목을 우선 사용합니다. 단, 뒷부분의 설정에서 추가 설명에 주의를 기울여야 합니다.<br></li><li>비슷한 선택 항목은 없지만 애플리케이션의 설명에서 S3 서비스 또는 S3 호환 서비스를 지원한다는 내용이 있는 경우 다음 설정으로 넘어가도 됩니다. 단, 여전히 추가 설명에 주의를 기울여야 합니다.<br></li><li>기타 상황의 경우 해당 애플리케이션은 COS 서비스를 사용할 수 없습니다.</li></td>
</tr>
<tr>
<td>서버/서버 주소/서비스&nbsp;URL/Endpoint/Custom Endpoint/Server URL 등</td>
<td>S3 호환 서비스의 서비스 주소 입력란입니다. COS 서비스 사용 시 여기에 COS 서비스 주소를 입력합니다(포맷: <code>cos.&lt;Region&gt;.myqcloud.com</code> 또는<br><code>https://cos.&lt;Region&gt;.myqcloud.com</code>).<br><code>https://</code> 입력 여부는 애플리케이션마다 조금씩 다르므로 직접 시도해 보시기 바랍니다. 이중 <code>&lt;Region&gt;</code>는 COS의 사용 가능 리전을 의미합니다.<br>귀하는 애플리케이션에서 서비스 주소가 지정한 리전에서만 버킷을 생성 또는 선택할 수 있습니다.<br><li>귀하의 버킷이 광저우 리전에 있는 경우 서비스 주소는 <code>cos.ap-guangzhou.myqcloud.com</code>으로 설정되어 있어야 합니다. 기타 리전으로 설정한 경우 애플리케이션에서 광저우 리전의 버킷을 찾을 수 없습니다.<br><li>애플리케이션의 서비스 공급자 중 <code>Amazon S3</code>만 선택할 수 있고 서버 포트 설정이 가능한 경우 서버 포트를 위의 <code>cos.&lt;Region>.myqcloud.com</code> 또는 <code>https://cos.&lt;Region>.myqcloud.com</code>으로 수정합니다.<br><li>서버 포트 설정이 불가능하거나 서버 포트 설정 항목이 없는 경우 귀하의 애플리케이션은 COS 서비스를 사용할 수 없습니다.</td>
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
<td>기존의 버킷 이름을 선택 또는 입력합니다. 포맷은 <code>&lt;BucketName-APPID&gt;</code>입니다(예: <code>examplebucket-1250000000</code>). 이중 <code>BucketName</code>은 <a href="#step5">5단계</a>에서 버킷 생성 시 입력한 버킷 이름이며, <code>APPID</code>는 <a href="#step4">4단계</a>에서 기록한 <strong>APPID</strong>입니다.<br>위의 설명과 마찬가지로 이곳의 버킷은 서버 주소가 지정한 리전에 한정되어 있으며, 기타 리전의 버킷은 나열되지 않거나 정상적인 사용이 불가능합니다. 새로운 버킷을 생성해야 하는 경우 새로 생성된 버킷 이름도 위의 <code>&lt;BucketName-APPID&gt;</code> 포맷에 부합해야 합니다. 그렇지 않으면 정상적으로 버킷을 생성할 수 없습니다.</td>
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

COS는 S3과 완전히 호환되지는 않습니다. COS 서비스 사용에 문제가 있는 경우 언제든 [Submit Ticket](https://console.cloud.tencent.com/workorder/category)으로 문의 바랍니다. 티켓 제출 시 해당 문서에서 가이드를 보고 문의한다는 내용과 함께 관련된 애플리케이션 이름, 화면 캡처 등의 정보를 알려 주시면 더 빨리 문제 해결을 도와드릴 수 있습니다.
