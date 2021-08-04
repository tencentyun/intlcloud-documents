본 튜토리얼은 CSS 서비스의 빠른 이해를 돕기 위해 제공됩니다. **유료 항목**과 **가격**의 혼동을 피하기 위해, CSS 서비스를 테스트하기 전에 먼저 CSS [가격 리스트](https://intl.cloud.tencent.com/document/product/267/2819)를 확인해 보실 것을 권장합니다.

<span id="step0"></span>
## 준비 과정

1. [Tencent Cloud 계정](https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2Fproduct%2Flvb)을 생성하고 [실명 인증](https://intl.cloud.tencent.com/document/product/378/3629)을 완료하십시오.실명인증을 하지 않은 사용자는 중국에서 클라우드 라이브 인스턴스를 구매할 수 없습니다.
2. [Tencent Cloud CSS 라이브 방송 서비스 활성화 페이지](https://console.cloud.tencent.com/live?from=product-banner-use-lvb)에서 <Tencent Cloud 서비스 약관>에 체크하여 동의하고 [활성화 신청]을 클릭하면 CSS 서비스가 활성화됩니다.

<span id="step1"></span>
## 1단계: 도메인 추가
CSS 서비스 이용 시 **푸시 스트리밍 도메인**과 **재생 도메인**을 포함하는 최소 **2**개의 도메인이 필요하며, 푸시 스트리밍과 재생은 동일한 도메인을 사용할 수 없습니다.

<span id="step1_1"></span>
1. 자체 도메인을 준비하고, 만일 중국에서 사용할 경우 도메인 ICP비안을 발급 받아야 합니다.
2. CSS 콘솔에 로그인하여 [[도메인 관리]](https://console.cloud.tencent.com/live/domainmanage) 페이지에서 [Create a Distribution]을 클릭하십시오.
3. 자체 도메인 추가 페이지에서 등록한 도메인을 작성하고 도메인 유형을 선택한 뒤 [OK]를 누르십시오.
![](https://main.qcloudimg.com/raw/bee8085a9d29641ddab913fdcd9c75ab.png)
>?
>- CSS에서 기본값으로 테스트 도메인 `xxxx.livepush.myqcloud.com`을 제공하며, 이 도메인을 통해 푸시 스트리밍을 테스트할 수 있습니다. 단, 공식 업무에 이 도메인을 푸시 스트리밍 도메인으로 사용하는 것은 권장하지 않습니다.
>- 도메인 추가가 완료되면 [Domain Management]의 도메인 목록에서 도메인 정보를 조회할 수 있습니다. 이미 추가된 도메인 관리가 필요한 경우, [도메인 관리](https://intl.cloud.tencent.com/document/product/267/31056)를 참조하십시오.
>- 라이브 방송 도메인에 관한 자세한 내용은 [라이브 방송 기초 관련 문제](https://intl.cloud.tencent.com/document/product/267/7968)를 참조하십시오.
<span id="step1_1_1"></span>
4. 도메인 추가가 완료되면 시스템에서 자동으로 CNAME 도메인(`.liveplay.myqcloud.com`을 접미사로 함)을 할당합니다. CNAME 도메인은 직접 액세스할 수 없으며, 도메인 서비스 제공 업체에서 CNAME 설정을 완료하고, 설정이 적용되면 CSS 서비스를 이용할 수 있습니다. DNS 서비스 제공 업체가 Tencent Cloud인 경우의 CNAME 기록 추가 작업 단계는 다음과 같습니다.
	1. [도메인 서비스 콘솔](https://console.cloud.tencent.com/domain)에 로그인합니다.
	2. CNAME을 추가할 도메인을 선택하고 [리졸브]를 클릭합니다.
	3. 도메인 리졸브 페이지에서 [기록 추가]를 클릭합니다.
	4. 신규 열에 도메인 접두사를 호스트 기록으로 작성, 기록 유형을 CNAME으로 선택하고 CNAME 도메인을 기록값으로 작성합니다.
	5. [Save]를 클릭하면 CNAME 기록이 추가됩니다.
>!
>- CNAME 성공 후 적용되기까지 일정 시간이 소요되며, CNAME 실패 시 CSS를 이용할 수 없습니다.
>- 도메인 CNAME 성공 시 CSS 콘솔의 [[도메인 관리]](https://console.cloud.tencent.com/live/domainmanage) 목록의 도메인 CNAME 주소 상태 표시가 ![](https://main.qcloudimg.com/raw/0fc346399ae095d69113d4944e511a20.png)로 변경됩니다.
>- CNAME 조작 후 검사에서 계속 실패하는 경우, 도메인 등록 서비스 제공 업체에 문의하시기 바랍니다.
>- 다른 DNS 서비스 제공 업체를 이용하는 경우 자세한 내용은 [CNAME 설정](https://intl.cloud.tencent.com/document/product/267/31057)을 참조하십시오.


<span id="step2"></span>
## 2단계: 푸시 스트리밍 주소 가져오기

1. 콘솔에서 [CSS Toolkit]>[[Address Generator]](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)를 선택.
2. 주소 생성기 페이지에서 다음과 같이 설정하십시오.
   1. 생성 유형: **푸시 스트리밍 도메인**을 선택합니다.
   2. 도메인 관리에 추가된 푸시 스트리밍 도메인을 선택합니다.
   3. 사용자 정의 스트림 이름 StreamName을 작성합니다. (예시: liveteststream)
   4. 주소 만료 시간을 선택합니다. (예시: 2019-10-18  23:59:59)
   5. [Generator Address]을 클릭하면 푸시 스트리밍 주소가 생성됩니다.
![](https://main.qcloudimg.com/raw/1d9741fe544d1c850ab89b22134f6dc8.png)

> ?
>- 푸시 스트리밍 주소 구조는 다음과 같습니다. `live`는 기본값 AppName, `txSecret`은 푸시 스트리밍 재생을 위한 서명, `txTime`은 푸시 스트리밍 주소의 유효 시간
>- 상기 방법 이외에도 CSS 콘솔의 [[도메인 관리]](https://console.cloud.tencent.com/live/domainmanage)에서 푸시 스트리밍 도메인 선택 후 [Manage]를 클릭하고, [푸시 스트리밍 설정]을 선택하여 푸시 스트리밍 주소의 만료 시간과 사용자 정의 스트림 이름 StreamName 입력 후 [푸시 스트리밍 주소 생성]을 클릭하면 푸시 스트리밍 주소가 생성됩니다.
>- 실제 작업 수요에 따라 푸시 스트리밍 주소를 생성하기 전에 대응하는 [기능 템플릿](https://intl.cloud.tencent.com/document/product/267/34223) 생성을 설정하여 푸시 스트리밍 도메인에 연동할 수 있습니다. 부가 기능 가격은 [가격 리스트](https://intl.cloud.tencent.com/document/product/267/2819)를 참조하십시오.

<span id="step3"></span>
## 3단계: 라이브 방송 푸시 스트리밍

비즈니스 시나리오에 따라 생성한 푸시 스트리밍 주소를 해당 푸시 스트리밍 소프트웨어에 입력하세요.
- PC 단의 푸시 스트리밍은 OBS 푸시 스트리밍 사용을 권장합니다. 자세한 조작 내용은 [OBS 푸시 스트리밍](https://intl.cloud.tencent.com/document/product/267/31569)를 참조하십시오.
- Web 단의 푸시 스트리밍은 [CSS Toolkit]>[[Web Push](https://console.cloud.tencent.com/live/tools/webpush) 사용을 권장합니다. 푸시 스트리밍할 도메인 선택, 사용자 정의 스트림 이름 StreamName 작성, 주소 만료 시간 선택, 카메라 켜기, [Start Push] 클릭순으로 진행합니다.
- 모바일 단의 푸시 스트리밍은 Tencent 비디오 클라우드 Demo를 다운로드 및 설치해 [MLVB]>[카메라 푸시 스트리밍]을 선택하고, 푸시 스트리밍 주소를 주소 편집창에 수동 입력하거나 QR코드를 스캔하여 입력한 뒤, 왼쪽 하단의 시작 버튼을 눌러 푸시 스트리밍을 시작합니다.

<span id="step4"></span>

## 4단계: 재생 주소 가져오기

1. 푸시 스트리밍에 성공하면 [[Streaming Management]](https://console.cloud.tencent.com/live/streammanage)>[Live Streams]을 선택하여 푸시 스트리밍 주소 상태를 조회하고, [테스트]를 클릭해 온라인으로 재생합니다.
2. [CSS Toolkit]>[[Address Generator]](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)를 선택해 재생 주소를 가져오고, 해당 페이지에서 다음과 같이 설정합니다.
   1. 생성 유형: **재생 도메인**을 선택합니다.
   2. 도메인 관리에 추가된 재생 도메인을 선택합니다.
   3. 푸시 스트리밍 주소와 동일한 StreamName을 작성합니다. 재생 주소 StreamName은 푸시 스트리밍 주소 StreamName과 반드시 일치해야 해당 스트림을 재생할 수 있습니다.
   4. 주소 만료 시간을 선택합니다. (예시: 2019-10-13  23:59:59)
   5. [Generator Address]을 클릭하면 재생 주소가 생성됩니다.
![](https://main.qcloudimg.com/raw/d91fe5d373cfc03df2c87562f3984858.png)
<span id="step4_1"></span>
3. 업무 시나리오에 따라 다음의 방식으로 라이브 방송 스트림이 정상적으로 재생되는지 테스트할 수 있습니다.
   1. PC 단의 라이브 방송 스트림 테스트는 [VLC](https://intl.cloud.tencent.com/document/product/267/32483) 등의 툴을 사용한 재생 테스트를 권장합니다. 자세한 내용은 [재생 테스트](https://intl.cloud.tencent.com/document/product/267/31559)를 참조하십시오.
   2. Web 단의 재생 테스트는 플레이어 SDK의 TCPlayerLite 플레이어를 사용해 재생하는 것을 권장합니다. 자세한 내용은 [라이브 방송 재생](https://intl.cloud.tencent.com/document/product/267/31559)을 참조하십시오.
   4. 모바일 단의 스트림 테스트는 Tencent 비디오 클라우드 Demo를 다운로드 및 설치해 [MLVB]>[라이브 방송 풀 스트리밍]을 선택하고, 재생 주소를 주소 편집창에 수동으로 입력하거나 QR코드를 스캔하여 입력한 뒤, 왼쪽 하단의 재생 버튼을 눌러 재생합니다.

## 관련 작업
- **라이브 방송 녹화**를 사용하려면 녹화 템플릿을 생성하고 도메인과 연결 설정을 진행하십시오. 자세한 내용은 [녹화 템플릿 생성](https://intl.cloud.tencent.com/document/product/267/34223)을 참조하십시오.
- **라이브 방송 트랜스 코딩**을 사용하려면 트랜스 코딩 템플릿을 생성하고 도메인과 연동 설정을 진행하십시오. 자세한 내용은 [트랜스 코딩 템플릿 생성](https://intl.cloud.tencent.com/document/product/267/31071)을 참조하십시오.
- **라이브 방송 워터마크**를 사용하려면 워터마크 템플릿을 생성하고 도메인과 연동 설정을 진행하십시오. 자세한 내용은 [워터마크 템플릿 생성](https://intl.cloud.tencent.com/document/product/267/31073)을 참조하십시오.
- **라이브 방송화면 캡처/음란물 감지**를 사용하려면 화면 캡처/음란물 감지 템플릿을 생성하고 도메인과 연동 설정을 진행하십시오. 자세한 내용은 [화면 캡처/음란물 감지 템플릿 생성](https://intl.cloud.tencent.com/document/product/267/31072)을 참조하십시오.
- **라이브 방송 혼합 스트림 기능**을 사용하려면 혼합 스트림 API를 호출해야 합니다. 자세한 내용은 [라이브 방송 혼합 스트림](https://intl.cloud.tencent.com/document/product/267/35997)을 참조하십시오.




## FAQ
- [푸시 스트리밍, 라이브 방송, VOD는 각각 무엇인가요?](https://intl.cloud.tencent.com/document/product/267/7968#.E6.8E.A8.E6.B5.81.E3.80.81.E7.9B.B4.E6.92.AD.E5.92.8C.E7.82.B9.E6.92.AD.E5.88.86.E5.88.AB.E6.98.AF.E4.BB.80.E4.B9.88.EF.BC.9F)
- [지원하는 푸시 스트리밍 프로토콜은 무엇인가요?](https://intl.cloud.tencent.com/document/product/267/7968#.E6.94.AF.E6.8C.81.E5.93.AA.E4.BA.9B.E6.8E.A8.E6.B5.81.E5.8D.8F.E8.AE.AE.EF.BC.9F)
- [지원하는 재생 프로토콜은 무엇인가요?](https://intl.cloud.tencent.com/document/product/267/7968#.E6.94.AF.E6.8C.81.E5.93.AA.E4.BA.9B.E6.92.AD.E6.94.BE.E5.8D.8F.E8.AE.AE.EF.BC.9F)
- [재생 주소는 어떻게 구성되나요?](https://intl.cloud.tencent.com/document/product/267/7968#.E6.92.AD.E6.94.BE.E5.9C.B0.E5.9D.80.E7.94.B1.E4.BB.80.E4.B9.88.E7.BB.84.E6.88.90.EF.BC.9F)
