## 작업 시나리오
CVM의 계정과 비밀번호는 CVM에 로그인하기 위한 자격 증명입니다. 본 문서는 CVM 로그인 비밀번호의 사용 및 관리 방법에 대해 소개합니다.

## 제한 조건

비밀번호를 설정할 때 반드시 다음과 같은 제한 조건을 충족해야 합니다.
- **Linux 인스턴스**: 비밀번호는 8 - 30자로 구성되어야 합니다. 최소 12자의 비밀번호를 사용하는 것이 좋습니다. 비밀번호는 ‘/’로 시작할 수 없으며 다음 중 3개 이상을 포함해야 합니다(`a-z`, `A-Z`, `0-9` 및 특수 부호<code>()`~!@#$%^&*-+=_|{}[]:;'<>,.?/</code>).
- **Windows 인스턴스**: 비밀번호는 12 - 30자로 구성되어야 합니다. 비밀번호는 ‘/’로 시작할 수 없고, 다음 중 3개 이상을 포함해야 하며(`a-z`, `A-Z`, `0-9` 및 특수 부호<code>()`~!@#$%^&*-+=_|{}[]:;'<>,.?/</code>), 사용자 ID를 포함할 수 없습니다.

## 작업 단계

### 초기 비밀번호 설정
CVM 구매 시 선택한 구성 방식에 따라 초기 비밀번호 설정이 달라집니다.
 - [**사용자 정의 구성**](https://buy.intl.cloud.tencent.com/cvm?regionId=4&projectId=-1) 옵션을 사용한 경우 초기 암호는 로그인 방법에 따라 다음과 같이 설정됩니다.
<table>
	<tr><th>로그인 방식</th><th>설명</th></tr>
	<tr><td>비밀번호 자동 생성</td><td>초기 비밀번호는 이메일과 콘솔 <a href="https://console.cloud.tencent.com/message">내부 메시지</a>를 통해 전송됩니다.</td></tr>
	<tr><td>즉시 키 연결</td><td><b>기본적으로 비활성화</b>되어 있습니다. 사용자 이름과 암호를 사용하여 로그인합니다. 나중에 비밀번호를 사용해야 하는 경우 클라우드 서버 콘솔에 로그인하여 <a href="https://intl.cloud.tencent.com/document/product/213/16566">비밀번호를 재설정</a>할 수 있습니다.</td></tr>
	<tr><td>비밀번호 설정</td><td>사용자 정의 비밀번호가 곧 초기 비밀번호입니다.</td></tr>
</table>


### 비밀번호 조회

시스템에서 자동 생성된 비밀번호는 이메일 및 콘솔 [내부 메시지](https://console.cloud.tencent.com/message)로 발송됩니다. 아래의 작업 콘텐츠는 내부 메시지를 예로 듭니다.
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/)에 로그인합니다.
2. 다음 이미지와 같이 오른쪽 상단 모서리에 있는 <img src="https://qcloudimg.tencent-cloud.cn/raw/d47b595ce159b2946f5fbbe10509569a.png" style="margin: -3px 0px;"></img>을(를) 클릭하고 해당 제품 메시지를 선택합니다.
![](https://main.qcloudimg.com/raw/e3c624a805d2f5776807df44bd373b59.png)
해당 제품의 정보 페이지에 들어가면 바로 비밀번호를 조회할 수 있습니다.
![](https://main.qcloudimg.com/raw/73bef8b11ded3d0cee5441d3d3218e25.png)

### 비밀번호 재설정

[인스턴스 비밀번호 재설정](https://intl.cloud.tencent.com/document/product/213/16566)을 참고하십시오.
	
	
