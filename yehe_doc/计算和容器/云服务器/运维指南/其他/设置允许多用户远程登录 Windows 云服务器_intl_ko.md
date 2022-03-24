## 작업 시나리오
본문은 Windows Server 2016 R2 운영 체제 CVM을 예로 들어 여러 사용자가 Windows CVM에 원격 로그인하도록 설정하는 방법을 안내합니다.

<dx-alert infotype="notice" title="">
Microsoft에서 제공하는 여러 사용자 원격 로그인 기능은 120일의 베타 기간이 있으며, 여러 사용자 로그인 라이선스(RDS CAL)를 구매하지 않으면 베타 기간이 만료된 후 원격 데스크톱을 통해 CVM에 로그인할 수 없으며 mstsc /admin 명령어를 통해서만 로그인이 가능합니다. Windows Server에서는 기본적으로 2명의 사용자가 동시에 로그인할 수 있으므로 대부분의 요구 사항을 충족할 수 있습니다. 실제 비즈니스 시나리오를 기준으로 평가해 주시고, 여러 사용자의 원격 로그인 설정에 대한 수요가 높을 경우 이 글을 참고하여 운영하시기 바랍니다.
</dx-alert>


## 작업 단계

### 원격 데스크톱 서비스 추가
1. Windows CVM에 로그인합니다.
2. 아래 이미지와 같이 운영 체제 인터페이스에서 <img src="https://qcloudimg.tencent-cloud.cn/raw/10c0728e4d194732be4eb6c1a95e0a8c.png" style="margin: -5px 0px;"/>을(를) 클릭하고 팝업된 인터페이스에서 <img src="https://qcloudimg.tencent-cloud.cn/raw/8a27d0993c99b2564c33df6bbabec4f7.png" style="margin: -5px 0px;"/>을(를) 선택한 후 ‘서버 관리자’를 엽니다.
    ![](https://main.qcloudimg.com/raw/66bb5237846f1dd79e3145bfd82d9257.png)
3. **역할 및 기능 추가**를 클릭하면 ‘역할 및 기능 추가 마법사’ 창이 팝업됩니다.
4. 역할 및 기능 추가 마법사’ 창에서 기본 매개변수를 유지하고 세 번 연속 **다음**을 클릭합니다.
5. 아래 이미지와 같이 ‘서버 역할’ 인터페이스에서 ‘원격 데스크톱 서비스’를 선택하고 **다음**을 클릭합니다.
    ![](https://main.qcloudimg.com/raw/54d329c2667ac5c60ffdc2b74f1fc555.png)
6. 기본 매개변수를 유지하고 **다음**을 더블 클릭합니다.
7. 아래 이미지와 같이 ‘역할 서비스 선택’ 인터페이스에서 **원격 데스크톱 세션 호스트**를 선택합니다.
    ![](https://main.qcloudimg.com/raw/8d24fd515bd363dc020257c2843c5562.png)
8. 아래 이미지와 같이 ‘원격 데스크톱 세션 호스트에 필요한 기능 추가’ 창에서 **기능 추가**를 클릭합니다.
    ![](https://main.qcloudimg.com/raw/2a33d896c16b1d98012536cdc3776248.png)
9. 아래 이미지와 같이 ‘역할 서비스 선택’ 인터페이스에서 ‘원격 데스크톱 라이선싱’을 선택합니다.
    ![](https://main.qcloudimg.com/raw/1c908dc77f50488387a2fdbfda08ba35.png)
10. 아래 이미지와 같이 ‘원격 데스크톱 라이선싱에 필요한 기능 추가’ 창에서 **기능 추가**를 클릭합니다.
    ![](https://main.qcloudimg.com/raw/d7aa066366b168ac8a7475155d34ea19.png)
11. **다음**을 클릭합니다.
12. 아래 이미지와 같이 ‘필요한 경우 자동으로 타깃 서버 자동 다시 시작’을 선택하고 팝업된 창에서 **예**를 클릭합니다.
    ![](https://main.qcloudimg.com/raw/df280b0a66470be404f114bd17c47d21.png)
13. **설치**를 클릭하고 원격 데스크톱 서비스 설치가 완료될 때까지 기다립니다.


### 여러 사용자 로그인 라이선스 신청
1. 운영 체제 인터페이스에서 <img src="https://qcloudimg.tencent-cloud.cn/raw/10c0728e4d194732be4eb6c1a95e0a8c.png" style="margin: -5px 0px;"/>을(를) 클릭하고 팝업된 인터페이스에서<img src="https://qcloudimg.tencent-cloud.cn/raw/8a27d0993c99b2564c33df6bbabec4f7.png" style="margin: -5px 0px;"/>을(를) 선택하여, ‘서버 관리자’를 엽니다.
2. ‘서버 관리자’ 창에서 오른쪽 상단의 **툴** > **Remote Desktop Services** > **원격 데스크톱 라이선스 관리자**를 선택합니다.
3.  ‘RD 라이선스 관리자’ 팝업 창에서 서버 행을 우클릭하고 **서버 활성화**를 선택합니다.
4. ‘서버 활성화 마법사’ 팝업 창에서 **다음**을 클릭합니다.
5.  ‘연결 방법’ 설정에서 이 문서의 ‘Web 브라우저’를 선택하고 **다음**을 클릭합니다.
실제 상황에 따라 다른 연결 방법을 선택할 수도 있습니다.
6. [](id:Step6)‘라이선스 서버 활성화’에서 제품 ID를 기록하고 [원격 데스크톱 라이선싱 웹 사이트](https://activate.microsoft.com/)를 방문합니다.
7.  원격 데스크톱 라이선스 웹 사이트에서 ‘라이선스 서버 활성화’를 선택하고 **다음**을 클릭합니다.
8.  [6 단계](#Step6)에서 획득한 제품 ID를 입력하고, 실제 상황에 맞게 회사 정보를 입력한 후 **다음 단계**를 클릭합니다.
9. 입력한 정보가 맞는지 확인한 후 **다음 단계**를 클릭합니다.
10.  [](id:Step10)라이선스 서버 ID를 기록하고 **예**를 클릭합니다.
11.  이전 단계에서 얻은 라이선스 서버 ID를 입력하고 필요한 라이선스 정보를 선택하고 회사 정보를 입력하고 **다음**을 클릭합니다.
본문의 인증 정보는 ‘기업 계약’을 예로 들어 설명합니다.
12.  제품 유형을 선택하고 수량 및 라이선스 자격 정보를 입력합니다.
<dx-alert infotype="explain" title="">
[Microsoft 공식 웹사이트](https://www.microsoftstore.com.cn/software/software)로 이동하여 고객서비스에 문의하여 RDS CALs 라이선스를 구매할 수 있습니다.
</dx-alert>
13. 정보가 맞는지 확인한 후 **다음 단계**를 클릭합니다.
14.  [](id:Step14)키 백 ID를 획득하여 기록합니다.
15. **종료**를 클릭합니다.


### 원격 데스크톱 서비스 라이선스 서버 활성화
1. 운영 체제 인터페이스에서 <img src="https://qcloudimg.tencent-cloud.cn/raw/10c0728e4d194732be4eb6c1a95e0a8c.png" style="margin: -5px 0px;"/>을(를) 클릭하고 팝업된 인터페이스에서<img src="https://qcloudimg.tencent-cloud.cn/raw/8a27d0993c99b2564c33df6bbabec4f7.png" style="margin: -5px 0px;"/>을(를) 선택하여, ‘서버 관리자’를 엽니다.
2. ‘서버 관리자’ 창에서 오른쪽 상단의 **툴** > **Remote Desktop Services** > **원격 데스크톱 라이선스 관리자**를 선택합니다.
3.  ‘RD 라이선스 관리자’ 팝업 창에서 서버 행을 마우스 오른쪽 버튼으로 클릭하고 **서버 활성화**를 선택합니다.
4. ‘서버 활성화 마법사’ 팝업 창에서 **다음**을 클릭합니다.
5.  ‘연결 방법’ 설정에서 이 문서의 ‘Web 브라우저’를 선택하고 **다음**을 클릭합니다.
실제 상황에 따라 다른 연결 방법을 선택할 수도 있습니다.
6.  ‘라이선스 서버 활성화’에서 [10 단계](#Step10)에서 얻은 라이선스 서버 ID를 입력하고 **다음 단계**를 클릭합니다.
12.  ‘서버 활성화 마법사’ 창에 “서버 활성화 마법사를 완료했습니다"라는 메시지가 표시되면 **다음 단계**를 클릭하여 라이선스 설치 단계를 진행합니다.



### RDS 클라이언트 액세스 라이선스 설치
1. ‘라이선스 설치 마법사’ 페이지에서 라이선스 서버 정보를 확인하고 **다음 단계**를 클릭합니다.
2.  ‘클라이언트 라이선스 키 팩 획득하기’에서 [14 단계](#Step14)에서 얻은 라이선스 서버 ID를 입력하고 **다음 단계**를 클릭합니다.
3.  ‘라이선스 설치 마법사’ 창에서 "라이선스 설치 마법사를 완료했습니다."라는 안내는 라이선스가 성공적으로 설치되었음을 나타냅니다.



### 원격 데스크톱 세션 호스트 라이선스 서버 설정
1. 운영 체제 인터페이스에서 <img src="https://qcloudimg.tencent-cloud.cn/raw/10c0728e4d194732be4eb6c1a95e0a8c.png" style="margin: -5px 0px;"/>을(를) 클릭하고 팝업된 인터페이스에서<img src="https://qcloudimg.tencent-cloud.cn/raw/8a27d0993c99b2564c33df6bbabec4f7.png" style="margin: -5px 0px;"/>을(를) 선택하여, ‘서버 관리자’를 엽니다.
2. ‘서버 관리자’ 창에서 오른쪽 상단의 **툴** > **Remote Desktop Services** > **원격 데스크톱 라이선싱 진단**을 선택합니다. 다음 이미지와 같이 현재 서버 상태를 확인합니다.
3. 운영 체제 인터페이스에서 <img src="https://qcloudimg.tencent-cloud.cn/raw/10c0728e4d194732be4eb6c1a95e0a8c.png" style="margin: -5px 0px;"/>을(를) 우클릭하고 팝업 메뉴에서 **실행**을 선택합니다.
4. ‘실행’ 창에 **gpedit.msc**를 입력하고 **Enter**를 눌러 컴퓨터 로컬 그룹 정책을 엽니다.
5.  왼쪽 사이드바에서 **컴퓨터 구성** > **관리 템플릿** > **Windows 구성 요소** > **원격 데스크톱 서비스** > **원격 데스크톱 세션 호스트** > **라이선스**를 선택합니다. ‘지정된 원격 데스크톱 라이선스 서버 사용’을 더블 클릭합니다.
6.  ‘지정된 원격 데스크톱 라이선스 서버 사용’ 팝업창에서 ‘사용함’ 선택 후 옵션에 ‘사용할 라이선스 서버’ 입력 클라우드 서버의 공용 IP 또는 호스트 이름을 입력할 수 있습니다. 설정이 완료되면 **확인**을 클릭합니다.
7.  ‘원격 데스크톱 라이선스 모드 설정’을 더블 클릭하여 엽니다.
8.  팝업된 ‘원격 데스크톱 라이선스 모드 설정’ 창에서 ‘사용’을 선택하고 RD 세션 호스트 서버의 라이선스 모드를 ‘사용자 단위’로 지정합니다. 설정이 완료되면 **확인**을 클릭합니다.
9. CVM을 재시작합니다.

여러 사용자 원격 로그인 설정을 완료했습니다.

## 참고 자료
- [License your RDS deployment with client access licenses (CALs)](https://docs.microsoft.com/en-us/windows-server/remote/remote-desktop-services/rds-client-access-license)
- [Activate the Remote Desktop Services license server](https://docs.microsoft.com/en-us/windows-server/remote/remote-desktop-services/rds-activate-license-server)
- [Install RDS client access licenses on the Remote Desktop license server](https://docs.microsoft.com/en-us/windows-server/remote/remote-desktop-services/rds-install-cals)
