## 현상 설명

- **현상 1**: <span id="FaultPhenomenon1"></span>
 - 회사 네트워크로 업로드 시 전송 속도가 정상이지만 가정 네트워크로 업로드 시 전송이 느립니다(8Mbps 이하).
 - 모바일 4G 네트워크로 업로드 시 전송 속도가 정상이지만 회사 네트워크로 업로드 시 전송이 느립니다(8Mbps 이하).
- **현상 2**: <span id="FaultPhenomenon2"></span>사용자 정의 도메인으로 업로드 시 전송이 느립니다.

## 예상 원인

- 현상 1 관련:
 1. 다른 네트워크 환경에서 COS 액세스 속도가 다른 경우, 해당 네트워크 ISP 및 네트워크 환경과 관련이 있을 수 있습니다.
 2. 다른 네트워크 환경에서 COS 액세스 속도가 다른 경우, 리전 간 액세스로 인한 문제일 수 있습니다.
- 현상 2 관련: 사용자 정의 도메인 CNAME은 CDN(Content Delivery Network), CVM(Cloud Virtual Machine), 보안 방어 제품과 같은 다른 제품으로 전송된 다음 COS로 전송됩니다.

## 해결 방안

- [현상 1](#FaultPhenomenon1) 상황이 발생한 경우 클라이언트 네트워크 환경을 진단하여 자체적으로 처리할 수 있습니다. 작업 방법에 대한 자세한 내용은 [클라이언트 네트워크 진단](#SearchTheClientNetwork)을 참조하십시오.
- [현상 2](#FaultPhenomenon2) 상황이 발생한 경우 사용자 정의 도메인 리졸브를 수정하면 전송 과정에서 거쳐가는 링크를 줄여 전송 효율을 높일 수 있습니다. 작업 방법에 대한 자세한 내용은 [사용자 정의 도메인 리졸브 수정](#ModifyCustomDomainNameResolution)을 참조하십시오.

## 처리 순서

<span id="SearchTheClientNetwork"></span>
### 클라이언트 네트워크 진단

1. 다음 명령어를 실행하여 IP 주소의 ISP와 클라이언트 네트워크 ISP가 동일한지 확인합니다.
```
ping COS의 액세스 도메인
```
예시:
```
ping examplebucket-1250000000.cos.ap-beijing.mqcloud.com
```
 - 예, [3단계](#step03)를 실행합니다.
 - 아니요, [2단계](#step02)를 실행합니다.
2. <span id="step02"></span>Chrome 브라우저 예시이며, 브라우저에 프록시가 설정되어 있는지 확인합니다.
    1. Chrome 브라우저를 열어 오른쪽 상단의 <img src="https://main.qcloudimg.com/raw/41a048f92c3d6160faff7e211bacce76.png"/> > [설정]을 클릭해 설정 페이지로 이동합니다.
    2. [고급]을 클릭하고 '시스템'에서 [컴퓨터 프록시 설정]을 클릭해 운영 체제의 설정 창을 엽니다.
    프록시가 설정되어 있는지 확인합니다.
     - 예, 프록시를 끕니다.
     - 아니요, [3단계](#step03)를 실행합니다.
3. <span id="step03"></span>모든 Wi-Fi 라우터에 속도 제한이 있는지 확인합니다.
 - 예, 실제 필요에 따라 적절히 허용합니다.
 - 아니요, [4단계](#step04)를 실행합니다.
4. <span id="step04"></span>현재 네트워크의 COS 업로드 전송 성능을 확인합니다.
COS의 COSCMD 툴 예시이며, 20MB 객체의 업로드 및 다운로드 성능을 테스트합니다.
```
coscmd probe -n 1 -s 20
```
다음과 유사한 결과가 반환되며 평균 속도(Average), 최저 속도(Min), 최고 속도(Max) 결과를 얻을 수 있습니다.
![](https://main.qcloudimg.com/raw/2fcecb96df04acc6b0c32c120ccb3c39.png)
5. 브라우저에서 [속도 테스트 사이트](https://www.speedtest.cn/)에 액세스하여 [4단계](#step04)와 함께 클라이언트의 네트워크 대역폭 점유율이 한계값에 달하는지 확인합니다.
 - 4단계 속도가 클라이언트 대역폭 속도보다 느린 경우 [온라인 고객센터](https://cloud.tencent.com/act/event/Online_service)로 문의하시기 바랍니다.
 - 4단계 속도가 클라이언트 대역폭 속도와 동일하고 ISP가 약정한 대역폭보다 낮은 경우 ISP 고객센터로 문의하시기 바랍니다.
 - 4단계 속도가 클라이언트 대역폭 속도와 동일하고 ISP가 약정한 대역폭에 일치하는 경우 [6단계](#step06)를 실행합니다.
6. <span id="step06"></span>중국 내 클라이언트에서 해외 노드 bucket으로 액세스하는지 또는 해외 클라이언트에서 중국 내 노드 bucket으로 액세스하는지 확인합니다.
 - 예, COS의 글로벌 가속 기능 사용을 권장합니다. 자세한 내용은 [글로벌 가속 개요](https://intl.cloud.tencent.com/zh/document/product/436/33409)를 참조하십시오.
 - 아니요. [온라인 고객센터](https://cloud.tencent.com/act/event/Online_service)로 문의하시기 바랍니다.

<span id="ModifyCustomDomainNameResolution"></span>
### 사용자 정의 도메인 리졸브 수정

1. 사용자 정의 도메인 리졸브가 COS 도메인인지 확인합니다.
 - 예. [온라인 고객센터](https://cloud.tencent.com/act/event/Online_service)로 문의하시기 바랍니다.
 COS 주요 도메인은 다음과 같습니다.
```
XXX.cos.ap-beijing.myqcloud.com(COS 기본 도메인)
XXX.cos.accelerate.myqcloud.com(COS 글로벌 가속 도메인)
XXX.cos-website.ap-beijing.myqcloud.com(COS 정적 페이지 도메인)
XXX.picbj.myqcloud.com(COS CI 기본 도메인)
```
 - 아니요, [2단계](#2_step02)를 실행합니다.
COS가 아닌 주요 도메인은 다음과 같습니다. 
```
XXX.file.myqcloud.com 또는 XXX.cdn.dnsv1.com(Tencent Cloud CDN 기본 도메인)
XXX.w.kunlungr.com(aliyunCDN 기본 도메인)
```
2. <span id="2_step02"></span>사용자 정의 도메인의 CNAME을 필요한 COS 도메인으로 리졸브하여 데이터를 업로드합니다.
예를 들어 `upload.mydomain.com  cname XXX.cos.ap-beijing.myqcloud.com`인 경우, 자세한 작업 방법은 [사용자 정의 원본 서버 도메인 활성화](https://cloud.tencent.com/document/product/436/36638)를 참조하십시오.
3. 클라이언트의 기본 COS 도메인을 수정합니다.
C# 코드 예시는 다음과 같습니다.
```
CosXmlConfig config = new CosXmlConfig.Builder()
.SetConnectionTimeoutMs(60000) //연결 타임아웃 시간 설정. 단위: 밀리초, 기본값: 45000ms
.SetReadWriteTimeoutMs(40000) //읽기 및 쓰기 타임아웃 시간 설정. 단위: 밀리초, 기본값: 45000ms
.IsHttps(true) //기본 https 요청 설정 .SetAppid(appid) //Tencent Cloud 계정의 계정 식별 APPID 설정
.SetRegion(region) //기본 버킷 리전 설정
.SetHost("XXXXXX.com") //사용자 정의 도메인 입력
.SetDebugLog(true) .Build(); //CosXmlConfig 객체 생성
```
기타 SDK 호출은 [SDK 개요](https://cloud.tencent.com/document/product/436/6474)를 참조하십시오.