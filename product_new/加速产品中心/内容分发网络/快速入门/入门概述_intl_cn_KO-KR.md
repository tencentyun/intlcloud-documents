Tencent Cloud CDN에 액세스하여 원본 서버 콘텐츠를 가장 가까운 사용자 노드에 배포하고, 서비스 노드에서 직접 빠르게 응답하여 사용자 액세스 딜레이를 효과적으로 낮추고 가용성을 높입니다. 
CDN 설정 시 Tencent Cloud 계정 생성, CDN 활성화, 도메인 액세스 및 CNAME 구성이 필요하며, 본문에서 차례대로 소개합니다.

## 1단계: Tencent Cloud 계정 생성
이미 Tencent Cloud 계정이 있는 경우는 이 단계를 생략할 수 있습니다.
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F" target="_blank"  style="color: white; font-size:16px;">여기를 눌러 Tencent Cloud 계정 생성</a></div>

## 2단계: CDN 활성화
#### 1. 실명 인증 완료
실명 인증을 진행하지 않은 사용자는 먼저 실명 인증을 진행해야 하며, 실명 인증은 CDN 콘솔 또는 고객센터를 통해 진행할 수 있습니다. 자세한 인증 프로세스는 [실명 인증 가이드](https://intl.cloud.tencent.com/document/product/378/3629)를 참조하십시오.
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;;"><a href="https://console.cloud.tencent.com/developer" target="_blank"  style="color: white; font-size:16px;">여기를 눌러 고객센터로 이동</a></div><br>

![](https://main.qcloudimg.com/raw/e71557f3118bf3579d551bb2ae2e2e9e.png)
#### 2. 부가 서비스 정보
[CDN Console](https://console.cloud.tencent.com/cdn)로 이동하여 실명 인증 정보 및 선택 서비스 내용을 확인한 다음 [다음 단계]를 클릭하세요.
![](https://main.qcloudimg.com/raw/087a21d256d40282127396a63b67c7b4.png)
#### 3. 결제 방식 선택
CDN은 트래픽 요금제와 대역폭 요금제의 두 가지 과금 방식을 제공하며, 비즈니스 모델에 따라 적절한 과금 방식을 선택할 수 있습니다. 자세한 내용은 [과금 설명](https://intl.cloud.tencent.com/document/product/228/2949)을 참조하십시오.
서비스 약관에 체크하여 동의한 다음 [CDN 활성화]를 클릭하면 바로 가속 서비스를 이용할 수 있습니다.
![](https://main.qcloudimg.com/raw/03c8c19ce7c7c73c956c23dc1c36dd3f.png)

## 3단계: 도메인 액세스
가속 작업을 위해서는 가속 도메인에 액세스해야 합니다. CDN이 가속 도메인을 통해 원본 서버 리소스를 CDN 가속 노드에 캐싱하면 사용자가 가까운 곳에서 필요한 리소스를 가져가 리소스 액세스 가속을 실현할 수 있습니다. 자세한 내용은 [도메인 이름 액세스](https://intl.cloud.tencent.com/document/product/228/5734)를 참조하십시오. 

## 4단계: CNAME 설정
도메인이 CDN에 액세스한 다음 도메인 서비스 공급자가 CNAME 구성을 완료해야 하며, 구성 완료 즉시 CDN 가속 서비스를 이용할 수 있습니다. 자세한 내용은 [CNAME 구성](https://intl.cloud.tencent.com/document/product/228/3121)을 참조하십시오.
