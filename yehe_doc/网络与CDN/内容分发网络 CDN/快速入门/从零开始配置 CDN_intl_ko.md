Tencent Cloud CDN에 액세스하여 원본 서버 콘텐츠를 가장 가까운 사용자 노드에 배포하고, 서비스 노드에서 직접 빠르게 응답하여 사용자 액세스 딜레이를 효과적으로 낮추고 가용성을 높입니다. 
CDN 설정 시 Tencent Cloud 계정 생성, CDN 활성화, 도메인 연결 및 CNAME 구성이 필요하며, 본문에서 차례대로 소개합니다.

## 1단계: Tencent Cloud 계정 생성
이미 Tencent Cloud 계정이 있는 경우는 이 단계를 생략할 수 있습니다.
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.3149.btn1">Tencent Cloud 회원가입하기</a></div>

## 2단계: CDN 활성화
#### 1. 실명 인증 완료
실명 인증을 진행하지 않은 사용자는 먼저 실명 인증을 진행해야 하며, 실명 인증은 CDN 콘솔 또는 고객센터를 통해 진행할 수 있습니다. 자세한 인증 프로세스는 [실명 인증 가이드](https://intl.cloud.tencent.com/document/product/378/3629)를 참조하십시오.
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;;"><a href="https://console.cloud.tencent.com/cdn" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.3149.btn2">CDN 콘솔로 이동</a></div><br>

![](https://main.qcloudimg.com/raw/e593cf6199d64fbcc5c6f50089778cf9.png)
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;;"><a href="https://console.cloud.tencent.com/developer" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.3149.btn2">계정 센터로 이동</a></div><br>

![](https://main.qcloudimg.com/raw/e71557f3118bf3579d551bb2ae2e2e9e.png)
#### 2. CDN 서비스 활성화
실명 인증 완료 후, CDN 서비스를 활성화할 수 있습니다.
(1) 과금 방식 선택
Tencent Cloud CDN은 **중국 내**와 **중국 외** 두 가지 서비스 지역으로 나뉘어 있습니다. 2020년 12월 7일 21:30부터는 CDN 활성화 시 [트래픽 시간에 따른 과금] 방식만 지원하며, 자세한 내용은 [과금 설명](https://intl.cloud.tencent.com/document/product/228/2949)을 참조하십시오.
![](https://main.qcloudimg.com/raw/5f75a3047566df1413233c2c0ac2736f.png)
(2) CDN 활성화
서비스 약관 동의를 선택한 후 [Open CDN]을 클릭하면 활성화되며 CDN 서비스를 사용할 수 있습니다.
![](https://main.qcloudimg.com/raw/4b1997247ae88641d1c2af0289b7ad2a.png)

## 3단계: 도메인 연결
가속 작업을 위해서는 가속 도메인에 연결해야 합니다. CDN이 가속 도메인을 통해 원본 서버 리소스를 CDN 가속 노드에 캐싱하면 사용자가 가까운 곳에서 필요한 리소스를 가져와 리소스 액세스 가속을 실현할 수 있습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/228/5734" hotrep="document.guide.3149.linkdomain">도메인 연결</a>을 참조하십시오.

## 4단계: CNAME 구성
도메인이 CDN에 액세스한 다음 도메인 서비스 공급자가 CNAME 구성을 완료해야 하며, 구성 완료 즉시 CDN 가속 서비스를 이용할 수 있습니다. 자세한 내용은 <a href="https://intl.cloud.tencent.com/document/product/228/3121" hotrep="document.guide.3149.linkcname">CNAME 구성</a>을 참조하십시오.
