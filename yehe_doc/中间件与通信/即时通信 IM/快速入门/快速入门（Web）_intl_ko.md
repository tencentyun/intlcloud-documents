Web Demo는 IM TUIKit을 기반으로 구현됩니다. TUIKit은 대화, 채팅, 그룹 및 프로필 관리와 같은 기능을 제공합니다. TUIkit을 사용하면 자신만의 비즈니스 로직을 빠르게 구축할 수 있습니다.

## Demo UI

### 대화 관리

| 대화 시작 | 대화 목록 | 대화 목록 관리 |
| --- | --- | --- |
| ![](https://qcloudimg.tencent-cloud.cn/raw/562deec9715ae2c50f65e8d40c4d7cac.png) | ![](https://qcloudimg.tencent-cloud.cn/raw/990204616a1c551c36ff5bdc57caa66c.png) | ![](https://qcloudimg.tencent-cloud.cn/raw/695589f54d4ac0b9bb9bc24eb97c7e6d.png) |

### 채팅 관리

| 메시지 목록 | 메시지 보내기 | 그룹 채팅 관리 |
| --- | --- | --- |
| ![](https://qcloudimg.tencent-cloud.cn/raw/8cb4fd0813a7ce0f3cab8468098dd896.png) |![](https://qcloudimg.tencent-cloud.cn/raw/f931993108c14ba3b2e628e4ed50a316.png) | ![](https://qcloudimg.tencent-cloud.cn/raw/bb9b0449eb712f9e6fececfdb199418a.png) |



| 기능  | 설명  |
| --- | --- |
| 대화 관리 | 1. 일대일/그룹 채팅 시작 <br/>2. 대화 목록 표시 <br/>3. 대화 목록 관리 |
| 채팅 관리 | 1. 메시지 목록 표시 <br/>2. 메시지 보내기 <br/>3. 그룹 채팅 관리 |


## 데모 실행

### 1단계: 소스 코드 다운로드

필요에 맞는 SDK와 [Demo 소스 코드](https://github.com/TencentCloud/TIMSDK)를 다운로드합니다.

```shell
# 명령 라인 실행
git clone https://github.com/TencentCloud/TIMSDK.git

# Web 프로젝트로 이동

cd TIMSDK/Web/Demo

# demo의 종속성 설치
npm install

cd TIMSDK/Web/Demo/src/TUIKit

# TUIKit의 종속성 설치
npm install
```

### 2단계: 데모 초기화
1. 웹 디렉터리에서 프로젝트를 열고 /debug/GenerateTestUserSig.js 경로를 통해 GenerateTestUserSig 파일을 찾습니다.
2. GenerateTestUserSig 파일에서 필수 매개변수를 설정합니다. 여기서 SDKAppID 및 키는 [IM 콘솔](https://console.cloud.tencent.com/im)에서 얻을 수 있습니다. 대상 앱 카드를 클릭하여 기본 구성 페이지로 이동합니다. 
3. **기본 정보** 영역에서 **키 표시**를 클릭하고 키 정보를 복사하여 GenerateTestUserSig 파일에 저장합니다. 
 ![](https://qcloudimg.tencent-cloud.cn/raw/8d469e975f1ca5a2f3dbc9c6fe8774f5.png)


> !본문에서 UserSig를 얻는 방법은 클라이언트 코드에서 SECRETKEY를 구성하는 것입니다. 이는 SECRETKEY를 디컴파일 및 크래킹에 취약하게 만듭니다. 키가 유출되면 공격자가 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **이 방법은 로컬에서 Demo 프로젝트를 실행하고 디버깅하는 데에만 적합합니다**. 올바른 UserSig 배포 방법은 UserSig의 계산 코드를 서버에 통합하고 App 지향 API를 제공하는 것입니다. UserSig가 필요할 때 App은 동적 UserSig에 대한 요청을 비즈니스 서버에 보낼 수 있습니다. 자세한 내용은 [Calculating UserSig on the Server](https://intl.cloud.tencent.com/document/product/1047/34385)를 참고하십시오.

### 3단계: 프로젝트 실행

```shell
# 프로젝트 실행
npm run serve
```

- [SDK API 매뉴얼](https://web.sdk.qcloud.com/im/doc/en/SDK.html)
- [SDK 업데이트 로그](https://intl.cloud.tencent.com/document/product/1047/34281)
- [Demo 소스 코드](https://github.com/TencentCloud/TIMSDK/tree/master/Web/Demo)
