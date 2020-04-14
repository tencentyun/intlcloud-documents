## 작업 시나리오
CVM의 계정과 비밀번호는 CVM에 로그인하기 위한 자격 증명입니다. 본 문서는 CVM 로그인 비밀번호의 사용 및 관리 방법에 대해 소개합니다.

## 제한 조건

비밀번호를 설정할 때 반드시 다음과 같은 제한 조건을 충족해야 합니다.
- Linux 인스턴스: 비밀번호 길이는 8-30자리로 제한하고, 그 중에서도 12자리 이상의 비밀번호를 사용할 것을 권장합니다. “/”로 시작할 수 없으며 최소 세 항목(`a-z`, `A-Z`, `0-9`와 ```()`~!@#$%^&*-+=_|{}[]:;'<>,.?/```의 특수 부호)을 포함해야 합니다.
- Windows 인스턴스: 비밀번호 길이는 12-30자리로 제한하고, “/”로 시작할 수 없으며 최소 세 항목(`a-z`, `A-Z`, `0-9`와 ```()`~!@#$%^&*-+=_|{}[]:;'<>,.?/```)을 포함해야 하는 동시에, 사용자 이름을 포함하지 않아야 합니다.

## 작업 순서

### 초기 비밀번호 설정
CVM 구매 시 선택한 구성 방식에 따라 초기 비밀번호 설정이 달라집니다.
 - [**빠른 구성**](https://buy.cloud.tencent.com/cvm?tab=lite) 방식을 통해 인스턴스 생성: 초기 비밀번호는 이메일 및 콘솔 [내부 메시지](https://console.cloud.tencent.com/message)를 통해 전송됩니다.
 - [**사용자 정의 구성**](https://buy.cloud.tencent.com/cvm?tab=custom)] 방식을 통해 인스턴스 생성: 생성 과정에서 로그인 방식에 따라 초기 비밀번호 설정 방식이 달라집니다.
<table>
	<tr><th>로그인 방식</th><th>설명</th></tr>
	<tr><td>비밀번호 자동 생성</td><td>초기 비밀번호는 이메일과 콘솔<a href="https://console.cloud.tencent.com/message">내부 메시지</a>를 통해 전송됩니다.</td></tr>
	<tr><td>즉시 키 연결</td><td><b>기본 종료</b>사용자 이름 비밀번호로 로그인, 단, 초기 비밀번호는 여전히 이메일 및 콘솔<a href="https://console.cloud.tencent.com/message">내부 메시지</a>를 통해 전송됩니다.</td></tr>
	<tr><td>비밀번호 설정</td><td>사용자 정의 비밀번호가 곧 초기 비밀번호입니다.</td></tr>
</table>


### 비밀번호 조회

CVM 로그인 비밀번호는 이메일 및 콘솔 [내부 메시지](https://console.cloud.tencent.com/message)를 통해 전송됩니다. 아래의 작업 콘텐츠는 내부 메시지를 예로 듭니다.
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/)에 로그인합니다.
2. 우측 상단의 <img src="https://main.qcloudimg.com/raw/f5d915ab4297418f3eae30fd28f41122.png" style="margin: 0;"></img> 클릭하여 대응하는 제품 정보를 선택합니다.
해당 제품의 정보 페이지에 들어가면 바로 비밀번호를 조회할 수 있습니다.
![](https://main.qcloudimg.com/raw/648d5ea37b192bc1eb384878a79c2453.png)

### 비밀번호 재설정

자세한 내용은 [인스턴스 비밀번호 재설정](https://cloud.tencent.com/document/product/213/16566)을 참조 바랍니다.
