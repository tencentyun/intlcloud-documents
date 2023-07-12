

## 소개


COS(Cloud Object Storage) 콘솔은 코드나 프로그램을 작성하지 않고 COS로 작업하는 가장 쉬운 방법입니다. COS 콘솔에서 직접 COS 서비스를 사용할 수 있습니다.

## 준비 작업

COS를 처음 사용하는 경우 다음의 기본 개념을 먼저 숙지하시기 바랍니다.

- [버킷(Bucket)](https://intl.cloud.tencent.com/document/product/436/13312): 객체 저장 수단으로 객체를 저장하는 '컨테이너'의 기능을 하며, 하나의 버킷에는 무수한 객체를 저장할 수 있습니다.
- [객체(Object)](https://intl.cloud.tencent.com/document/product/436/13324): COS의 기본 단위로 이미지, 문서, 멀티미디어 파일 등 다양한 포맷의 데이터를 의미합니다.
- [리전(Region)](https://intl.cloud.tencent.com/document/product/436/6224): Tencent Cloud의 호스팅 데이터 센터가 분포된 지역으로 COS 데이터를 리전의 버킷에 저장합니다.

COS 콘솔에서 COS 서비스를 이용해 데이터를 클라우드에 빠르게 저장하는 방법은 다음과 같습니다.

## 1단계: Tencent Cloud 계정 생성
Tencent Cloud의 COS 서비스를 사용하려면 먼저 Tencent Cloud 계정을 생성해야 합니다. 하단 버튼을 클릭하면 가입할 수 있습니다. 이미 가입한 경우에는 이 단계를 생략합니다.

<div style="background-color:#00A4FF; width: 125px; height: 35px; line-height:35px; text-align:center;"><a href="https://www.tencentcloud.com/en/account/register" target="_blank"  style="color: white; font-size:13px;">가입하기</a></div>

## 2단계: 실명 인증
가입 완료 후, 가입한 계정으로 [Tencent Cloud 콘솔](https://console.cloud.tencent.com/)에 로그인하여 실명 인증을 합니다. 자세한 작업 가이드는 [Identity Verification Guide](https://intl.cloud.tencent.com/document/product/378/3629)를 참고하십시오(이미 완료한 경우, 이 단계 생략).

<div style="background-color:#00A4FF; width: 125px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/developer" target="_blank"  style="color: white; font-size:13px;"  hotrep="document.guide.3128.btn2">실명 인증하기</a></div>


## 3단계: COS 서비스 활성화
[Tencent Cloud 콘솔](https://console.cloud.tencent.com/)에서 **클라우드 서비스 > COS**를 선택하여 COS 콘솔로 이동한 뒤 인터페이스 안내에 따라 COS 서비스를 활성화합니다. 이미 활성화한 경우에는 이 단계를 생략합니다.

<div style="background-color:#00A4FF; width: 225px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/cos5" target="_blank"  style="color: white; font-size:13px;">COS 서비스 활성화하기</a></div>


## 4단계: 버킷 생성
객체를 저장할 버킷을 생성해야 합니다.

1. [COS 콘솔](https://console.cloud.tencent.com/cos5) 왼쪽 사이드바에서 **버킷 리스트**를 클릭하여 버킷 관리 페이지로 이동합니다.
2. **버킷 생성**을 클릭하여 다음의 설정 정보를 입력합니다. 기타 항목은 기본값을 적용합니다.
 - 이름: 버킷 이름을 입력합니다. 이름은 설정 후 수정이 불가합니다. 본 예시에서는 examplebucket으로 입력합니다.
 - 소속 리전: 버킷이 소속된 리전으로, 사용자의 비즈니스와 가장 근접한 지역을 선택합니다(예: 광저우 리전).
 - 액세스 권한: 버킷에 액세스하는 권한으로, 본 예시에서는 기본값인 '개인 읽기 및 쓰기'를 유지합니다.
3. **확인**을 클릭하여 생성을 완료합니다.


## 5단계: 객체 업로드
로컬에서 파일을 선택해 버킷에 업로드합니다.

1. 버킷 이름을 클릭하여 버킷 리스트 페이지로 이동합니다.
2. **파일 업로드 > 파일 선택**에서 버킷에 업로드할 파일을 선택합니다(예시: exampleobjext.zip 파일).
3. **업로드**를 클릭하면 exampleobjext.zip 파일이 버킷에 업로드됩니다.


## 6단계: 객체 다운로드
클라우드 데이터를 로컬에 다운로드합니다.
1. exampleobjext.zip 파일 오른쪽의 **상세 내용**을 클릭하여 객체 속성 페이지로 이동합니다.
2. 기본 정보 설정 페이지에서 **객체 다운로드**를 클릭하여 다운로드하거나 **임시 링크 복사**를 클릭하여 링크를 브라우저 주소창에 붙여 넣은 뒤 엔터 키를 눌러 객체를 다운로드합니다.
>?기본적으로 다운로드한 객체를 브라우저에서 직접 열 수 있는 경우 객체를 직접 미리 볼 수 있지만 임시 링크에 액세스하여 객체를 다운로드할 수는 없습니다.

## 추가 기능
객체 액세스 권한 설정, 링크 도용 방지 설정, 정적 웹 사이트 설정 등 콘솔의 다양한 기능은 [콘솔 개요](https://intl.cloud.tencent.com/document/product/436/11365)를 참조하십시오.


## 기타 사용 방법
COS 콘솔 외에도 다음과 같은 방법으로 COS 서비스를 관리 및 사용할 수 있습니다.

<table>
<thead>
<tr>
<th align="left" width="30%">기타 사용 방법</th>
<th align="left" width="70%">기능 설명</th>
</tr>
</thead>
<tbody><tr>
<td align="left" width="30%"><a href="https://intl.cloud.tencent.com/document/product/436/11366">COSBrowser 툴</a></td>
<td align="left" width="70%">해당 툴은 데이터 업로드, 다운로드, 액세스 링크 생성 등의 작업을 보다 쉽게 하기 위한 시각화 인터페이스를 지원합니다.</td>
</tr>
<tr>
<td align="left" width="30%"><a href="https://cloud.tencent.com/doc/product/436/10976">COSCMD 툴</a></td>
<td align="left" width="70%">해당 툴은 객체 대량 업로드, 다운로드, 삭제 등의 작업을 위해 간단한 명령 라인을 사용한 명령을 지원합니다.</td>
</tr>
<tr>
<td align="left" width="30%"><a href="https://intl.cloud.tencent.com/document/product/436/7751">API 방식</a></td>
<td align="left" width="70%">COS는 미연결 상태의 경량급 인터페이스인 XML API를 사용합니다. 이 인터페이스를 호출하면 HTTP/HTTPS를 통한 요청 발송 및 응답 수신으로 Tencent Cloud COS 백그라운드와의 인터랙티브 작업이 가능합니다.</td>
</tr>
<tr>
<td align="left" width="30%"><a href="https://intl.cloud.tencent.com/document/product/436/6474">SDK 방식</a></td>
<td align="left" width="70%">Android, C, C++, .NET, Go, iOS, Java, JavaScript, Node.js, PHP, Python, 미니프로그램 SDK 등 다양한 주요 개발 언어를 지원합니다.</td>
</tr>
</tbody></table>



## 질문이 있으십니까?

이용에 불편을 드려 대단히 죄송합니다. [고객센터](https://intl.cloud.tencent.com/contact-sales)를 통해 문의하시기 바랍니다.



