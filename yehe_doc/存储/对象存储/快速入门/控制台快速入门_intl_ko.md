
## 소개

COS 콘솔은 사용자의 편의를 위해 제공되는 간편하고 손쉬운 COS 사용 수단입니다. 코딩 또는 실행 프로그램이 없이도 COS 콘솔을 통해 COS 서비스를 바로 이용할 수 있습니다.

## 준비 과정

COS를 처음 사용한다면 다음의 기본 개념을 먼저 숙지하시기 바랍니다.

- [버킷(bucket)](https://intl.cloud.tencent.com/document/product/436/13312): 객체 저장 수단으로 객체를 저장하는 ‘컨테이너’의 기능을 합니다.
- [객체(Object)](https://intl.cloud.tencent.com/document/product/436/13324): COS의 기본 단위로 이미지, 문서, 멀티미디어 파일 등 포맷의 데이터를 의미합니다.
- [리전(Region)](https://intl.cloud.tencent.com/document/product/436/6224): Tencent Cloud의 호스팅 데이터 센터가 분포된 지역으로 COS 데이터를 리전의 버킷에 저장합니다.

COS 콘솔에서 COS 서비스를 이용해 데이터를 클라우드에 간편하게 저장하는 방법은 다음과 같습니다.

## 1단계: Tencent Cloud 계정 생성하기
Tencent Cloud의 COS 서비스를 사용하려면 Tencent Cloud 계정을 만드십시오. 하단 버튼을 클릭하면 가입할 수 있습니다. 이미 가입한 경우에는 이 단계를 생략해도 됩니다.

<div style="background-color:#00A4FF; width: 125px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/register" target="_blank"  style="color: white; font-size:13px;">가입하기</a></div>

## 2단계: 실명 인증하기
가입 완료 후, 가입한 계정으로 [Tencent Cloud 콘솔](https://console.cloud.tencent.com/)에 로그인하여 실명 인증을 합니다. 자세한 방법은 [실명 인증 소개](https://intl.cloud.tencent.com/document/product/378/3629)에서 확인하실 수 있습니다. 실명 인증을 했다면 본 단계는 생략 가능하며, 실명 인증을 하지 않은 경우, 중국에서 COS 인스턴스를 구매할 수 없습니다.

<div style="background-color:#00A4FF; width: 125px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/developer" target="_blank"  style="color: white; font-size:13px;"  hotrep="document.guide.3128.btn2">실명 인증하기</a></div>



## 3단계: COS 서비스 활성화하기
[Tencent Cloud 콘솔](https://console.cloud.tencent.com/)에서 [제품]>[COS]를 선택하여 COS 콘솔로 이동한 뒤 인터페이스 안내에 따라 COS 서비스를 활성화합니다. 이미 활성화한 경우에는 이 단계를 생략해도 됩니다.

<div style="background-color:#00A4FF; width: 125px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/cos5" target="_blank"  style="color: white; font-size:13px;">COS 서비스 활성화하기</a></div>


## 4단계: 버킷 생성하기
객체를 저장할 버킷 하나를 생성해야 합니다.

1. [COS 콘솔](https://console.cloud.tencent.com/cos5) 왼쪽 메뉴에서 [버킷 리스트]를 클릭하여 버킷 관리 페이지로 이동합니다.
2. [버킷 생성]을 클릭하여 다음의 설정 정보를 입력합니다. 기타 항목은 디폴트 값을 적용합니다.
 - 이름: 버킷명을 입력합니다. 버킷명은 설정 후 수정이 불가합니다. examplebucket을 예로 입력합니다.
 - 리전: 버킷이 위치한 리전으로 광저우 리전과 같이 본인의 비즈니스와 가장 근접한 지역을 선택합니다.
 - 액세스 권한: 버킷에 액세스하는 권한으로 ‘개인 읽기 및 쓰기’로 디폴트 값을 설정합니다.
3. [확인]을 클릭하면 버킷 생성이 완료됩니다.


## 5단계: 객체 업로드하기
로컬에서 파일 선택해 버킷으로 업로드하기

1. 버킷명을 클릭하여 버킷 목록 페이지로 이동합니다.
2. [파일 업로드]>[파일 선택]을 선택하여 버킷에 업로드할 파일을 선택합니다. 파일명은 예시로 들면 exampleobjext.txt와 같습니다.
3. [업로드]를 클릭하면 exampleobjext.txt 파일이 버킷에 업로드됩니다.


## 6단계: 객체 다운로드하기
클라우드 데이터를 로컬로 다운로드하기
1. exampleobjext.txt 파일 오른쪽의 [상세보기]를 클릭하여 객체 속성 페이지로 이동합니다.
2. [기본 정보] 설정 페이지에서 [객체 다운로드]를 클릭하여 다운로드하거나 [임시 링크 복사]를 클릭하여 링크를 브라우저 주소창에 붙여 넣은 뒤 엔터 버튼을 입력해 객체를 다운로드합니다.

## 추가 기능
객체 액세스 권한 설정, 링크 도용 방지 설정, 정적 웹 사이트 설정 등 보다 다양한 콘솔 기능을 확인하려면 [콘솔 소개](https://intl.cloud.tencent.com/document/product/436/11365)를 참조하십시오.


## 기타 사용 방법
COS는 COS 서비스의 관리와 사용에 필요한 콘솔 뿐 아니라 다음과 같은 이용 방법을 제공합니다.

<table>
<thead>
<tr>
<th align="left" width="30%">기타 사용 방법</th>
<th align="left" width="70%">기능 설명</th>
</tr>
</thead>
<tbody><tr>
<td align="left" width="30%"><a href="https://intl.cloud.tencent.com/document/product/436/11366">COSBrowser 툴</a></td>
<td align="left" width="70%">해당 툴은 데이터의 편리한 업로드, 다운로드, 액세스 링크 생성 등 작업을 위한 시각화 인터페이스를 제공합니다.</td>
</tr>
<tr>
<td align="left" width="30%"><a href="https://intl.cloud.tencent.com/document/product/436/10976">COSCMD 툴</a></td>
<td align="left" width="70%">해당 툴은 객체의 대량 업로드, 다운로드, 삭제 등 작업을 위한 간단한 명령 라인 명령을 제공합니다.</td>
</tr>
<tr>
<td align="left" width="30%"><a href="https://intl.cloud.tencent.com/document/product/436/7751">API 방식</a></td>
<td align="left" width="70%">COS는 단일 요청을 처리하는 경량의 인터페이스 XML API를 채택하고 있습니다. 이 인터페이스를 호출하여 HTTP/HTTPS의 요청 및 응답을 실행하고, Tencent Cloud COS의 백그라운드와 인터랙티브하게 연결할 수 있습니다.</td>
</tr>
<tr>
<td align="left" width="30%"><a href="https://intl.cloud.tencent.com/document/product/436/6474">SDK 방식</a></td>
<td align="left" width="70%">Android, C, C++, .NET, Go, iOS, Java, JavaScript, Node.js, PHP, Python, 미니프로그램 SDK 등 다양한 주요 개발 언어를 지원합니다.</td>
</tr>
</tbody></table>



## 문제 해결

사용 시 문제가 발생할 경우, [Submit Ticket](https://console.cloud.tencent.com/workorder/category)을 통해 문의하시기 바랍니다.
