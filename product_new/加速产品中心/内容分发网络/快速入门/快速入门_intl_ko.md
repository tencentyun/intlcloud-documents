## **순서 미리보기**
CDN을 사용하는 과정은 아래 그림과 같습니다.
![순서도](https://mc.qcloudimg.com/static/img/f226c2d0655ce65f25bca945082f7760/quick-start-9.png)
## CDN 서비스 이용 안내
CDN 서비스를 사용하기 전에 본인 인증 및 CDN 서비스를 활성화해야 합니다. Tencent Cloud 계정이 이미 CDN을 이용하고 있는 경우 [액세스 도메인 이름](#yuming)부터 진행합니다.
### 실명 인증 완료
1. 새로운 사용자 로그인 [CDN 콘솔](https://console.cloud.tencent.com/cdn)에서 본인 인증을 참조하시기 바랍니다. [인증으로 이동]을 클릭하여 본인 인증을 수행하십시오.
 ![](https://main.qcloudimg.com/raw/b5aa156bf7e0b124808e56640af1da86.png)
2. [계정 센터](https://console.cloud.tencent.com/developer)로 이동하여 [인증 제출]을 클릭하여 인증할 수도 있습니다.
3. 자세한 인증 절차는 [본인 인증 안내서](https://cloud.tencent.com/doc/product/378/3629)를 참조하십시오. 제출되는 즉시 본인 인증이 완료됩니다. 기업 인증은 1 영업일 이내에 완료되며 인증이 완료되면 SMS 가 발송됩니다. [티켓 제출](https://console.cloud.tencent.com/workorder/category/create?level1_id=1andlevel2_id=41andlevel1_name=%E5%85%AC%E5%85%B1%E5%9F%BA % E7 % A1 % 80 % E7 % B1 % BB % E9 % 97 % AE % E9 % A2 % 98andlevel2_name = % E8 % B4 % A6 % E5 % 8F % B7 % E7 % B1 % BB)에서 인증 진행 상황을 참조하십시오.

### 부가 서비스 정보
본인 인증을 완료 한 후 [CDN 콘솔](https://console.cloud.tencent.com/cdn)로 이동하여 본인 인증 정보를 확인하고 서비스 내용을 선택한 후 완료되면 [다음]을 클릭하십시오.

### 결제 수단 선택
CDN은 종량제과 대역폭 요금제의 두 가지 청구 방식을 제공합니다. 비즈니스 모델에 따라 적절한 요금제를 선택할 수 있습니다. 자세한 내용은 [요금제 설명](https://cloud.tencent.com/doc/product/228/2949)을 참조하십시오.
서비스 약관에 동의한 후 [CDN 열기]를 클릭하여 서비스를 시작하십시오.
![](https://main.qcloudimg.com/raw/7d9c4709d99cef3b0789e94688b03591.jpg)
서비스 시작 후 개요 페이지에서 선택한 청구 모드를 확인하실 수 있습니다.
![](https://main.qcloudimg.com/raw/0fd255d1cfdd32956af140be373be7c4.png)

<span id="yuming"></span>
## 액세스 도메인 이름
### 도메인 이름 구성 입력
1. [CDN 콘솔](https://console.cloud.tencent.com/cdn)로 이동하여 왼쪽 메뉴에서 [도메인 관리]를 클릭하여 해당 페이지를 입력한 다음 [도메인 이름 추가]를 클릭하십시오.
 ![](https://main.qcloudimg.com/raw/0f21ace69d94ce51fc1d857948510b4a.jpg)
2. ** 도메인 이름 ** 위치에서 가속이 필요한 도메인 이름을 입력합니다. 도메인 이름은 다음 조건을 충족해야 합니다.
 - 공업정보화부 ICP비안에 등록된 도메인
 - Tencent Cloud CDN에 연결되지 않은 도메인
![](https://main.qcloudimg.com/raw/e0dbd38a9395439f37efeec4a4c10b3e.png)

### 서비스 구성 입력
 **서비스 유형**선택에 따라 도메인 이름 예약을 위한 플랫폼이 결정됩니다. 플랫폼의 가속 구성에는 다음과 같은 차이점이 있습니다. 서비스와 일치하는 유형을 선택하십시오.
 - 정적 가속: 전자 상거래, 웹 사이트 및 게임 이미지 정적 리소스의 가속화 환경
 - 다운로드 가속: 게임 설치 패키지, 오디오 및 비디오 원본 파일 다운로드, 모바일 펌웨어 배포 및 기타 환경
 - 주문형 스트리밍 가속: 주문형 오디오 및 비디오 스트리밍 환경 
 ![](https://main.qcloudimg.com/raw/5af0cdca96bb92488a05d0e8474a7dad.png)

### 추가 완료
도메인 이름을 제출하면 완료됩니다. 도메인 이름 구성이 전체 네트워크 노드에 전달 될 때까지 약 5~10분 소요됩니다．
![](https://main.qcloudimg.com/raw/396d4e1e706558f0fcf9291e8e763d83.jpg)

## CNAME 구성
### CNAME 조회
도메인 이름이 구성되면 시스템은 접미사를 `**. cdn.dnsv1.com` 를 사용하여 해당 **CNAME **을 지정합니다. 콘솔에 표시된 CNAME에 따라 구성합니다．
![](https://main.qcloudimg.com/raw/0f21ace69d94ce51fc1d857948510b4a.jpg)

### CNAME 수정
도메인 이름에 액세스하는 DNS 서비스 제공 업체에서 CNAME을 구성해야 합니다. 구성 방법은 [CNAME 구성](https://cloud.tencent.com/doc/product/228/3121)을 참조하십시오.
### CNAME 유효성 확인
CNAME은 DNS제공업체마다 상이하며 일반적으로 30분내에 적용됩니다. dig를 사용하여 CNAME 유효성 여부를 확인할 수 있으며, ```.cdn.dnsv1.com```도메인 이름이 붙으면 CNAME이 유효한 것입니다.
![](https://main.qcloudimg.com/raw/4c611fda0209a45d9441a2f0336bbf84.png)

