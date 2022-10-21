## 작업 시나리오
2020년 3월 23일부터 CLB의 모든 인증서 작업은 인증을 위해 CAM(Cloud Access Management)에 연결되었습니다. 따라서 서브 사용자 계정이 CLB 인증서 작업을 수행할 때 ‘이 작업에 대한 권한이 없습니다. 개발자에게 문의하세요.’ 가 표시되면 아래 지침에 따라 서브 사용자 계정에 인증서 권한을 부여할 수 있습니다.

## 전제 조건
로그인한 계정은 루트 계정이거나 CAM 권한이 있는 서브 사용자 계정이어야 합니다(즉, QcloudCamFullAccess 정책과 연결됨).
>
>- 서브 사용자 계정에 CAM 권한이 있는지 확인하려면 CAM 콘솔의 [사용자 목록](https://console.cloud.tencent.com/cam)으로 이동하여 서브 사용자의 세부 정보 페이지로 이동하여 QcloudCamFullAccess 정책이 연결되었는지 확인합니다.
>- QcloudCamFullAccess 정책이 연결되어 있지만 서브 사용자가 인증서 작업을 수행할 때 ‘API 권한(message:GetReceiversOnAllType)이 없습니다. 개발자에게 문의하세요.’가 표시되면 무시하고 계속 진행할 수 있습니다. 

## 작업 단계
다음 방법으로 인증서 권한을 부여하십시오.

### 방법1: 사용자 지정 정책 연결
1. [CAM 콘솔](https://console.cloud.tencent.com/cam/overview)에 로그인합니다.
2. 왼쪽 사이드바에서 [정책]을 클릭합니다.
3. [사용자 지정 정책 생성]을 클릭하고 팝업 창에서 [정책 구문으로 생성]을 선택합니다.
4. ‘템플릿 정책 선택’ 페이지에서 [빈 템플릿]을 선택하고 [다음]을 클릭합니다.
5. ‘정책 편집’ 페이지에서 정책 이름을 입력하고 ‘정책 내용 편집’ 입력 상자에 다음 정책 내용을 입력합니다.
```
   {
    "version": "2.0",
    "statement": [
        {
            "action": "name/ssl:*",
            "resource": "qcs::ssl:::*",
            "effect": "allow"
        }
    ]
}  
```
6. 그런 다음 [정책 생성]을 클릭하여 ‘정책’ 목록 페이지로 돌아갑니다.
7. ‘정책’ 목록 페이지 상단에서 [사용자 지정 정책]을 선택하고 목록에서 방금 생성한 정책 행을 찾은 다음 작업 열에서 [사용자/그룹 연결]을 클릭합니다.
![](https://main.qcloudimg.com/raw/2a0cf97e6de81cbbc3fcc6af9164bb5a.png)
8. 팝업 창에서 권한을 부여할 사용자를 선택하고 [확인]을 클릭합니다.
![](https://main.qcloudimg.com/raw/2105e8b1ebf79f0d6b1d063aa0bcd158.png)

### 방법2: 사전 설정 정책 연결
1. [CAM 콘솔](https://console.cloud.tencent.com/cam/overview)에 로그인합니다.
2. 왼쪽 사이드바에서 [사용자]>[사용자 목록]을 선택하여 ‘사용자 목록’ 페이지로 이동합니다.
3. 권한을 부여할 서브 사용자 행의 작업 표시줄에서 [권한 부여]를 클릭합니다.
4. 팝업 창에서 QcloudSSLFullAccess(SSL 인증서(SSL) 전체 읽기/쓰기 액세스 권한) 또는 QcloudSSLReadOnlyAccess(SSL 인증서(SSL) 읽기 전용 액세스 권한)를 선택하고 [확인]을 클릭합니다.
![](https://main.qcloudimg.com/raw/a18245f729467395f801002f6defcb8d.png)
