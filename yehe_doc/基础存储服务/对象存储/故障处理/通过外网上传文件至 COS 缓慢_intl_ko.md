## 현상 설명

- **현상1**: <span id="FaultPhenomenon1"></span>
 - 회사 네트워크를 사용해 업로드 시 정상적으로 전송되나, 홈 네트워크를 사용해 업로드 시 전송이 느림(8Mbps 이하)
 - 4G 네트워크를 사용해 업로드 시 정상적으로 전송되나, 회사 네트워크를 사용해 업로드 시 전송이 느림(8Mbps 이하)
- **현상2**: <span id="FaultPhenomenon2"></span>사용자 정의 도메인을 사용해 업로드 시 전송이 느림

## 가능한 원인

- 현상1:
 1. 서로 다른 네트워크 환경에서 COS 액세스 속도가 다른 경우, 해당 네트워크 ISP 및 네트워크 환경과 관련된 문제일 수 있습니다.
 2. 서로 다른 네트워크 환경에서 COS 액세스 속도가 다른 경우, 지역 간 액세스로 인한 문제일 수 있습니다.
- 현상2: Content Delivery Network(CDN), Cloud Virtual Machine(CVM), 높은 보안 제품과 같이 사용자 정의 도메인 CNAME에서 다른 제품을 거쳐 COS로 전송되는 경우일 수 있습니다.

## 해결 방법

- [현상1](#FaultPhenomenon1)의 상황이 발생하는 경우 클라이언트 네트워크 환경을 점검하여 자체적으로 처리할 수 있습니다. 자세한 작업 방법은 [클라이언트 네트워크 진단](#SearchTheClientNetwork)을 참고하십시오.
- [현상2](#FaultPhenomenon2)의 상황이 발생하는 경우 사용자 정의 도메인 리졸브 방식을 변경해 중간에 경유하는 링크를 줄임으로써 전송 효율을 향상시킬 수 있습니다. 자세한 작업 방법은 [사용자 정의 도메인 리졸브 변경](#ModifyCustomDomainNameResolution)을 참고하십시오.

## 처리 단계

<span id="SearchTheClientNetwork"></span>
### 클라이언트 네트워크 진단

1. 다음 명령어를 실행하여 IP 주소 ISP와 클라이언트 네트워크 ISP가 동일한지 확인합니다.
```
ping COS의 액세스 도메인
```
예시:
```
ping examplebucket-1250000000.cos.ap-beijing.mqcloud.com
```
 - 예. [3단계](#step03)를 실행합니다.
 - 아니요. [2단계](#step02)를 실행합니다.
2. <span id="step02"></span>브라우저에 프록시를 설정했는지 확인합니다. 다음은 Chrome 브라우저 예시입니다.
    1. Chrome 브라우저를 열고 오른쪽 상단의 <img src="https://main.qcloudimg.com/raw/41a048f92c3d6160faff7e211bacce76.png"/> > **설정**을 클릭해 설정 페이지를 엽니다.
    2. **고급**을 클릭하고 '시스템'에서 **컴퓨터 프록시 설정**을 클릭하면 운영 체제의 설정창이 열립니다.

    프록시를 설정했는지 확인합니다.
     - 예. 프록시를 끕니다.
     - 아니요. [3단계](#step03)를 실행합니다.
3. <span id="step03"></span>사용하는 Wi-Fi 라우터에 속도 제한이 존재하는지 확인합니다.
 - 예. 실제 필요에 따라 개방합니다.
 - 아니요. [4단계](#step04)를 실행합니다.
4. <span id="step04"></span>현재 네트워크의 COS 업로드 전송 성능을 확인합니다.
20MB 객체로 업로드 및 다운로드 성능을 테스트합니다. 다음은 COS의 COSCMD 툴 예시입니다.
```
coscmd probe -n 1 -s 20
```
평균 속도(Average), 최저 속도(Min), 최고 속도(Max)로 나뉘어 다음과 유사한 결과를 반환합니다.
![](https://main.qcloudimg.com/raw/2fcecb96df04acc6b0c32c120ccb3c39.png)
5. 브라우저를 통해 [속도 테스트 웹사이트](https://www.speedtest.cn/)에 액세스하고 [4단계](#step04)와 결합하여 클라이언트의 네트워크 대역폭 점유율이 한계에 도달하는지 확인합니다.
 - 4단계의 속도가 클라이언트 대역폭 속도보다 낮은 경우 [고객센터](https://intl.cloud.tencent.com/contact-sales)로 문의하십시오.
 - 4단계의 속도가 클라이언트 대역폭 속도와 동일하고 ISP가 약정한 대역폭에 도달하지 않는 경우 ISP 고객센터로 문의하십시오.
 - 4단계의 속도가 클라이언트 대역폭 속도와 동일하고 ISP가 약정한 대역폭에 도달하는 경우 [6단계](#step06)를 실행하십시오.
6. <span id="step06"></span>중국 내 클라이언트가 해외 노드 bucket에 액세스했는지, 해외 클라이언트가 중국 내 노드 bucket에 액세스했는지 확인합니다.
 - 예. COS의 글로벌 가속 기능 사용을 권장합니다.
 - 해당 오류가 아닌 경우: [고객센터](https://intl.cloud.tencent.com/contact-sales)에 문의하십시오.

<span id="ModifyCustomDomainNameResolution"></span>
### 사용자 정의 도메인 리졸브 변경

1. 사용자 정의 도메인 리졸브가 COS 도메인인지 확인합니다.
 - 해당 오류일 경우: [고객센터](https://intl.cloud.tencent.com/contact-sales)에 문의하십시오.
 자주 볼 수 있는 COS 도메인으로는 다음이 있습니다.
```
XXX.cos.ap-beijing.myqcloud.com (COS 기본 도메인)
XXX.cos.accelerate.myqcloud.com (COS 글로벌 가속 도메인)
XXX.cos-website.ap-beijing.myqcloud.com (COS 정적 페이지 도메인)
XXX.picbj.myqcloud.com (COS CI 기본 도메인)
```
 - 아니요. [2단계](#2_step02)를 실행합니다.
자주 볼 수 있는 COS가 아닌 도메인으로는 다음이 있습니다. 
```
XXX.file.myqcloud.com 또는 XXX.cdn.dnsv1.com(Tencent Cloud CDN 기본 도메인)
XXX.w.kunlungr.com(aliyunCDN 기본 도메인)
```
2. <span id="2_step02"></span>사용자 정의 도메인의 CNAME을 필요한 COS 도메인으로 리졸브하고 데이터 업로드를 진행합니다.
예: `upload.mydomain.com  cname XXX.cos.ap-beijing.myqcloud.com`. 자세한 작업 방법은 [사용자 정의 원본 서버 도메인 활성화](https://intl.cloud.tencent.com/document/product/436/31507)를 참고하십시오.
3. 클라이언트의 기본 COS 도메인을 변경합니다.
C# 코드 예시:
```
CosXmlConfig config = new CosXmlConfig.Builder()
.SetConnectionTimeoutMs(60000) //연결 타임아웃 시간 설정. 단위: 밀리초, 기본값: 45000ms
.SetReadWriteTimeoutMs(40000) //읽기 및 쓰기 타임아웃 시간 설정. 단위: 밀리초, 기본값: 45000ms
.IsHttps(true) //기본 https 요청 설정 
.SetAppid(appid) //Tencent Cloud 계정의 계정 식별 APPID 설정
.SetRegion(region)  //기본 버킷 리전 설정
.SetHost("XXXXXX.com") //사용자 정의 도메인 입력
.SetDebugLog(true) .Build(); //CosXmlConfig 객체 생성
```
기타 SDK 호출은 [SDK 개요](https://intl.cloud.tencent.com/document/product/436/6474)를 참고하십시오.

