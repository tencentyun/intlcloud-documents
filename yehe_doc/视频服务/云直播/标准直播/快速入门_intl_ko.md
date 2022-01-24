본 튜토리얼은 CSS 서비스의 빠른 이해를 돕기 위해 제공됩니다. **유료 항목**과 **가격**의 혼동을 피하기 위해, CSS 서비스를 테스트하기 전에 먼저 CSS [가격 리스트](https://intl.cloud.tencent.com/document/product/267/2819)를 확인해 보실 것을 권장합니다.



[](id:step0)

## 준비 작업

1. [Tencent Cloud 계정](https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2Fproduct%2Flvb)을 생성하고 [실명 인증](https://intl.cloud.tencent.com/document/product/378/3629)을 완료합니다. 실명 인증을 하지 않은 사용자는 중국 내 CSS 인스턴스를 구매할 수 없습니다.
2. [Tencent Cloud CSS 서비스 활성화 페이지](https://console.cloud.tencent.com/live?from=product-banner-use-lvb)에서 <Tencent Cloud 서비스 약관>에 체크하여 동의하고 **활성화 신청**을 클릭하면 CSS 서비스가 활성화됩니다.


[](id:step1)
## 1단계: 도메인 추가
CSS 서비스 이용 시 **푸시 스트림 도메인**과 **재생 도메인**을 포함하는 최소 **2**개의 도메인이 필요하며, 푸시 스트림과 재생은 동일한 도메인을 사용할 수 없습니다.

<span id="step1_1"></span>
1. 도메인을 준비합니다. 만일 중국에서 사용할 경우 도메인 ICP비안을 완료해야 합니다.
2. CSS 콘솔에 로그인하여 [[도메인 관리]](https://console.cloud.tencent.com/live/domainmanage) 페이지에서 [도메인 추가]를 클릭하십시오.
![](https://main.qcloudimg.com/raw/771bbce97962dcd1cffdd94324941280.png)
>?
>- CSS에서 기본값으로 테스트 도메인 `xxxx.livepush.myqcloud.com`을 제공하며, 이 도메인을 통해 푸시 스트림을 테스트할 수 있습니다. 단, 공식 업무에 이 도메인을 푸시 스트림 도메인으로 사용하는 것은 권장하지 않습니다.
>- 도메인 추가가 완료되면 **도메인 관리**의 도메인 목록에서 도메인 정보를 조회할 수 있습니다. 이미 추가된 도메인 관리가 필요한 경우, [도메인 관리](https://intl.cloud.tencent.com/document/product/267/31056)를 참고하십시오.
>- 라이브 방송 도메인에 관한 자세한 내용은 [라이브 방송 기본 관련](https://intl.cloud.tencent.com/document/product/267/7968)을 참고하십시오.

[](id:step1_1_1)
4. 도메인 추가가 완료되면 시스템에서 자동으로 CNAME 도메인(`.tlivecdn.com` 또는 `.tlivepush.com`을 접미사로 함)을 할당합니다. CNAME 도메인은 직접 액세스할 수 없으며, 도메인 서비스 공급자에서 CNAME 설정을 완료한 후 설정이 적용되면 CSS 서비스를 이용할 수 있습니다. DNS 서비스 제공 업체가 Tencent Cloud인 경우의 CNAME 기록 추가 작업 단계는 다음과 같습니다.
  1.  [도메인 서비스 콘솔](https://console.cloud.tencent.com/domain)에 로그인합니다.
  2.  CNAME을 추가할 도메인을 선택하고 **리졸브**를 클릭합니다.
  3.  도메인 리졸브 페이지에서 **레코드 추가**를 클릭합니다.
  4.  신규 열에 도메인 접두사를 호스트 기록으로 입력합니다. 기록 유형을 CNAME으로 선택하고 CNAME 도메인을 기록값으로 입력합니다.
  5.  **저장**을 클릭하면 CNAME 레코드가 추가됩니다.
>!
>- CNAME 성공 후 적용되기까지 일정 시간이 소요되며, CNAME 실패 시 CSS를 이용할 수 없습니다.
>- 도메인 CNAME 성공 시 CSS 콘솔의 [**도메인 관리**](https://console.cloud.tencent.com/live/domainmanage) 목록의 도메인 CNAME 주소 상태 표시가 ![](https://main.qcloudimg.com/raw/0fc346399ae095d69113d4944e511a20.png)로 변경됩니다.
>- CNAME 작업 후 점검에 계속 실패하는 경우, 도메인 등록 서비스 제공 업체에 문의하시기 바랍니다.
>- 다른 DNS 서비스 제공 업체를 이용하는 경우 자세한 내용은 [도메인 CNAME 설정](https://intl.cloud.tencent.com/document/product/267/31057)을 참고하십시오.


[](id:step2)
## 2단계: 푸시 스트림 주소 가져오기
1. **라이브 방송 툴박스** >  [**주소 생성기**](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)를 선택합니다.
2. 주소 생성기 페이지에서 다음과 같이 설정합니다.
   1. 생성 유형 선택: **푸시 스트림 도메인**을 선택합니다.
   2. 도메인 관리에서 이미 추가된 푸시 스트림 도메인을 선택합니다.
   3. AppName을 입력합니다. 기본값은 `live`입니다.
   4. 사용자 정의 스트림 이름 StreamName을 입력합니다. (예시: `liveteststream`)
   5. 주소 만료 시간을 선택합니다. (예시: `2021-05-31 23:59:59`)
   6. **주소 생성**을 클릭하여 푸시 스트림 주소 생성을 완료합니다.
![](https://main.qcloudimg.com/raw/5a377614d5da22c5193bef68f4a3a6e7.png)

>? 
>- 푸시 스트림 주소 구조는 다음과 같습니다. `live`는 기본값 AppName이고, `txSecret`은 푸시 스트림 재생을 위한 서명이며, `txTime`은 푸시 스트림 주소의 유효 시간입니다.
>- 상기 방법 이외에도 CSS 콘솔의 [**도메인 관리**](https://console.cloud.tencent.com/live/domainmanage)에서 푸시 스트림 도메인 선택 후, **관리**를 클릭하고, **푸시 스트림 설정**을 선택합니다. 푸시 스트림 주소의 만료 시간과 사용자 정의 스트림 이름 StreamName 입력 후, **푸시 스트림 주소 생성**을 클릭하면 푸시 스트림 주소가 생성됩니다.
>- 실제 작업 수요에 따라 푸시 스트림 주소를 생성하기 전에 [기능 템플릿](intl.cloud.tencent.com/document/product/267/34223) 생성을 설정하여 푸시 스트림 도메인에 연동할 수 있습니다. 부가 기능 가격은 [가격 리스트](https://intl.cloud.tencent.com/document/product/267/2819)를 참고하십시오.

[](id:step3)
## 3단계: 라이브 방송 푸시 스트림

서비스 시나리오에 따라 생성한 푸시 스트림 주소를 해당 푸시 스트림 소프트웨어에 입력하십시오.
- PC 푸시 스트림은 OBS 푸시 스트림 사용을 권장합니다. 자세한 작업 관련 내용은 [OBS 푸시 스트림](https://intl.cloud.tencent.com/document/product/267/31569)을 참고하십시오.
- Web에서의 푸시 스트림은 [**Web 푸시**](https://console.cloud.tencent.com/live/tools/webpush) 사용을 권장합니다. 푸시 스트림이 필요한 도메인을 선택하고 사용자 정의 스트림 이름 StreamName을 입력합니다. 주소 만료 시간을 선택하고 카메라를 켠 후 **푸시 스트림 시작**을 클릭합니다.

- 모바일 푸시 스트림은 [Tencent Cloud 툴킷 App](https://intl.cloud.tencent.com/document/product/1071/38147)를 다운로드 및 설치하고, **MLVB** > **푸시 스트림 데모(카메라 푸시 스트림)** 열기 및 선택 후, 수동 입력 또는 QR 코드 스캔을 통해 주소 입력란에 푸시 스트림 주소를 입력하고, **푸시 스트림 시작**을 클릭하면 스트리밍할 수 있습니다.

>? 맞춤화된 App에서 Tencent Cloud가 제공하는 [MLVB SDK](https://intl.cloud.tencent.com/document/product/1071)를 통합해 푸시 스트림 기능을 구현할 수 있습니다.

[](id:step4)
## 4단계: 재생 주소 가져오기
1. 푸시 스트림 완료 후, [**스트림 관리**](https://console.cloud.tencent.com/live/streammanage)> **온라인 스트림**을 선택하여 푸시 스트림 주소 상태를 조회하고, **테스트**를 클릭해 온라인에서 재생 및 시청합니다.
2. **라이브 방송 툴박스** > [**주소 생성기**](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)를 선택하여 재생 주소를 가져옵니다. 해당 페이지에서 다음과 같이 설정합니다.
   1. 생성 유형: **재생 도메인**을 선택합니다.
   2. 도메인 관리에 이미 추가한 재생 도메인을 선택합니다.
   3. AppName을 입력합니다. 기본값은 `live`입니다.
   4. 푸시 스트림 주소와 동일한 StreamName을 입력합니다. 재생 주소 StreamName은 반드시 푸시 스트림 주소 StreamName과 일치해야 해당 스트림을 재생할 수 있습니다.
   5. 주소 만료 시간을 선택합니다. (예시: `2021-05-31 23:59:59`)
   6. 트랜스코딩된 라이브 방송 재생 URL을 생성하려면 사전에 재생 URL이 바인딩된 트랜스코딩 템플릿을 선택합니다. 바인딩 방법은 [라이브 방송 트랜스 코딩>도메인 연결](https://intl.cloud.tencent.com/document/product/267/31071)을 참고하십시오.
   7. **URL 생성**을 클릭하여 재생 URL을 생성합니다.
![](https://main.qcloudimg.com/raw/5025e22cd8c4c555d7de3e0360e13d11.png)
[](id:step4_1)
3. 서비스 시나리오에 따라 다음의 방식으로 라이브 방송 스트림이 정상적으로 재생되는지 테스트할 수 있습니다.
   1. PC 라이브 방송 스트림 테스트는 [VLC 푸시 스트림](https://intl.cloud.tencent.com/document/product/267/32483) 등의 툴을 사용한 재생 테스트를 권장합니다. 자세한 내용은 [라이브 방송 재생](https://intl.cloud.tencent.com/document/product/267/31559)을 참고하십시오.

   2. 모바일에서의 라이브 방송 스트림 테스트는 [Tencent Cloud 툴 패키지App](https://intl.cloud.tencent.com/document/product/1071/38147)을 다운로드 및 설치하고 **MLVB** > **LVB 재생**을 선택한 후, 수동 또는 QR코드 스캔을 통해 주소 편집 창에 재생 URL을 입력하고, 왼쪽 하단의 재생 버튼을 클릭하여 재생할 것을 권장합니다.

>? App에서 푸시 스트림/재생하는 경우 [MLVB SDK](https://intl.cloud.tencent.com/product/mlvb)를 통합하여 CSS 서비스와 결합해 사용할 수 있습니다. 체험 과정에서 문제가 발생한 경우 CSS [FAQ](https://intl.cloud.tencent.com/document/product/267/7968)를 참고하십시오.

## 관련 작업
- **라이브 방송 녹화**를 사용하려면 녹화 템플릿을 생성하고 도메인과 연결 설정을 진행하십시오. 자세한 내용은 [녹화 템플릿 생성](https://intl.cloud.tencent.com/document/product/267/34223)을 참고하십시오.
- **라이브 방송 트랜스 코딩**을 사용하려면 트랜스 코딩 템플릿을 생성하고 도메인과 연동 설정을 진행하십시오. 자세한 내용은 [트랜스 코딩 템플릿 생성](https://intl.cloud.tencent.com/document/product/267/31071)을 참고하십시오.
- **라이브 방송 워터마크**를 사용하려면 워터마크 템플릿을 생성하고 도메인과 연동 설정을 진행하십시오. 자세한 내용은 [워터마크 템플릿 생성](https://intl.cloud.tencent.com/document/product/267/31073)을 참고하십시오.
- **라이브 방송화면 캡처/음란물 감지**를 사용하려면 화면 캡처/음란물 감지 템플릿을 생성하고 도메인과 연동 설정을 진행하십시오. 자세한 내용은 [화면 캡처&음란물 감지 템플릿 생성](https://intl.cloud.tencent.com/document/product/267/31072)을 참고하십시오.
- **라이브 방송 혼합 스트림 기능**을 사용하려면 혼합 스트림 API를 호출해야 합니다. 자세한 내용은 [라이브 방송 혼합 스트림](https://intl.cloud.tencent.com/document/product/267/35997)을 참고하십시오.




## FAQ
- [푸시 스트림, 라이브 방송, VOD의 차이는 무엇인가요?](https://intl.cloud.tencent.com/document/product/267/7968#.E6.8E.A8.E6.B5.81.E3.80.81.E7.9B.B4.E6.92.AD.E5.92.8C.E7.82.B9.E6.92.AD.E5.88.86.E5.88.AB.E6.98.AF.E4.BB.80.E4.B9.88.EF.BC.9F)
- [어떤 푸시 스트림 프로토콜을 지원하나요?](https://intl.cloud.tencent.com/document/product/267/7968#.E6.94.AF.E6.8C.81.E5.93.AA.E4.BA.9B.E6.8E.A8.E6.B5.81.E5.8D.8F.E8.AE.AE.EF.BC.9F)
- [어떤 재생 프로토콜을 지원하나요?](https://intl.cloud.tencent.com/document/product/267/7968#.E6.94.AF.E6.8C.81.E5.93.AA.E4.BA.9B.E6.92.AD.E6.94.BE.E5.8D.8F.E8.AE.AE.EF.BC.9F)
- [재생 주소는 어떻게 구성되나요?](https://intl.cloud.tencent.com/document/product/267/7968#.E6.92.AD.E6.94.BE.E5.9C.B0.E5.9D.80.E7.94.B1.E4.BB.80.E4.B9.88.E7.BB.84.E6.88.90.EF.BC.9F)
- [여러 개의 라이브 방송 URL은 어떻게 조합하여 생성하나요?](https://intl.cloud.tencent.com/document/product/267/38393)

