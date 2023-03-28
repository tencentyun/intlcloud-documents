## 오프라인 푸시 자가진단
### 오프라인 푸시 포지셔닝 툴
이 툴을 사용하여 오프라인 메시지를 받지 못하는 문제를 자가진단할 수 있습니다.

1. [IM 콘솔](https://console.cloud.tencent.com/im)에 로그인한 후 대상 IM 애플리케이션 카드를 클릭합니다.
2. 왼쪽 사이드바에서 **보조 툴**>**오프라인 푸시 자가 진단**을 선택합니다.
3. **오프라인 푸시 포지셔닝 툴** 영역에 UserID를 입력합니다.
4. **장치 상태 가져오기**를 클릭하여 인증서 ID 및 장치 Token과 같은 UserID에 대해 업로드된 정보를 봅니다.
>?인증서 ID 및 장치 Token과 같은 UserID 정보가 업로드되지 않은 경우 쿼리가 종료됩니다.
>
5. UserID의 인증서 ID를 선택하고 **확인 시작**을 클릭한 다음 전송 결과를 봅니다.
 - 성공 프롬프트가 표시되면 콘솔에 입력한 인증서 정보가 정확하고 SDK API를 호출하여 Token이 업로드된 것입니다. 추가 문제 해결을 위해 [사용자 클라이언트 상태 확인 툴](#status)을 사용할 수 있습니다. 
 - 실패 프롬프트가 표시되면 실패 원인과 해결 방법을 볼 수 있습니다.

![](https://main.qcloudimg.com/raw/5c1930b3079c03fa730aacd6950cea1e.png)

[](id:status)
### 사용자 상태 확인 툴
이 툴은 사용자의 상태를 자동으로 파악하고 사용자가 오프라인 푸시 메시지를 받을 준비가 되었는지 확인합니다.

1. [IM 콘솔](https://console.cloud.tencent.com/im)에 로그인한 후 대상 IM 애플리케이션 카드를 클릭합니다.
2. 왼쪽 사이드바에서 **보조 툴**>**오프라인 푸시 자가 진단**을 선택합니다.
3. **사용자 상태 확인 툴** 영역에 UserID를 입력합니다.
4. **상태 가져오기**를 클릭하여 UserID의 현재 상태 및 클라이언트 유형과 같은 정보를 봅니다.
 UserID가 오프라인 푸시 메시지를 수신할 준비가 되었다는 메시지가 표시되면 다른 장치에서 다른 UserID로 로그인하여 현재 UserID로 일대일 문자 메시지를 보내 메시지 수신 가능 여부를 확인할 수 있습니다.

![](https://main.qcloudimg.com/raw/5674cd90ac892e48882cfc0f3130eeab.png)

## UserSig 생성 및 검증
### 서명(UserSig) 생성 툴
시스템은 현재 애플리케이션의 키를 자동으로 가져옵니다. UserID를 입력한 후 이 툴을 사용하여 서명(UserSig)을 빠르게 생성하여 로컬에서 Demo 및 디버그 기능을 실행할 수 있습니다. 온라인 서비스용 UserSig를 생성해야 하는 경우 [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385)를 참고하십시오.

1. [IM 콘솔](https://console.cloud.tencent.com/im)에 로그인한 후 대상 IM 애플리케이션 카드를 클릭합니다.
2. 왼쪽 사이드바에서 **보조 툴**>**UserSig 툴**을 선택합니다.
3. UserSig 생성 툴 영역에 UserID를 입력합니다.
4. **UserSig 생성**을 클릭하여 180일 후에 만료되는 UserSig를 생성합니다.
5. **서명(UserSig) 복사**를 클릭하여 서명을 복사한 다음 서명을 붙여넣고 저장합니다.
 ![](https://main.qcloudimg.com/raw/edc9bb594760b1edcf0366d92ce69d07.png)

### 서명(UserSig) 검증 툴
시스템은 현재 애플리케이션의 키를 자동으로 가져오기합니다. UserID 및 UserSig만 입력하면 이 도구를 사용하여 UserSig의 유효성을 빠르게 확인할 수 있습니다.

1. [IM 콘솔](https://console.cloud.tencent.com/im)에 로그인한 후 대상 IM 애플리케이션 카드를 클릭합니다.
2. 왼쪽 사이드바에서 **보조 툴**>**UserSig 툴**을 선택합니다.
3. 서명(UserSig) 검증 툴 영역에서 UserID 및 UserSig를 입력합니다.
   ![](https://main.qcloudimg.com/raw/5fcd54faa763ff3bb46b074945bd02ed.png)
4. **검증 시작**을 클릭하면 검증 결과를 볼 수 있습니다.
 - 검증에 성공하면, 해당 UserSig의 SDKAppID, UserID, 생성 시간, 서비스 시간 및 만료 시간을 확인할 수 있습니다.
    ![](https://main.qcloudimg.com/raw/383c2f0761eec12124c442683f09de07.png)
 - 검증에 실패하면 검증 결과에서 실패 원인과 해결 방법을 확인할 수 있습니다.
    ![](https://main.qcloudimg.com/raw/b320ffc210f5b93ce261d9a3d697aa07.png)

 

 
