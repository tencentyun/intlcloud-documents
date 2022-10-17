SCF 함수를 작성하여 백엔드 Web 서비스를 구현하고 CLB 인스턴스와 바인딩하여 서비스를 제공할 수 있습니다.

## 배경 정보
Tencent Cloud [Serverless Cloud Function(SCF)](https://intl.cloud.tencent.com/document/product/583)은 서버를 구매하고 관리할 필요 없이 애플리케이션을 구축하고 실행할 수 있는 서버리스 실행 환경입니다. 함수를 생성한 후 CLB 트리거를 생성하여 함수와 이벤트를 바인딩할 수 있습니다. CLB 트리거는 요청 내용을 매개변수로 함수에 전달하고 함수의 결과를 요청자에게 응답으로 다시 반환합니다.

## 시나리오
<dx-accordion>
::: 일반 \sHTTP/HTTPS\s 액세스
전자상거래, 소셜 미디어 및 툴 등 기타 서비스용 App과 개인 블로그, 이벤트 페이지 등을 위한 Web 응용 프로그램에 적용할 수 있습니다. 워크플로는 다음과 같습니다.
1. App, 브라우저, H5 페이지 또는 미니 프로그램에서 시작된 HTTP/HTTPS 요청은 CLB 인스턴스를 통해 SCF 기능에 액세스합니다.
2. CLB 인스턴스가 인증서 제거를 완료한 후 SCF는 HTTP 서비스만 제공하면 됩니다.
3. 그런 다음 요청은 클라우드 데이터베이스에 쓰기 및 다른 API 호출과 같은 후속 처리를 위해 SCF 함수로 전송됩니다.
![](https://main.qcloudimg.com/raw/534ca758662eaffdd40d243bd8384739.svg)
:::
::: CVM/SCF\s 간 전환
특히 장애 조치 시 HTTP/HTTPS 서비스를 CVM에서 SCF로 마이그레이션하는 데 적용할 수 있습니다. 워크플로는 다음과 같습니다.
1. App, 브라우저, H5 또는 미니프로그램 등이 HTTP/HTTPS 요청을 시작합니다.
2. 그런 다음 요청은 DNS에 의해 두 CLB 인스턴스의 VIP로 레졸루션됩니다.
3. 하나의 CLB 인스턴스는 요청을 CVM으로 포워딩하고 다른 인스턴스는 이를 SCF로 포워딩합니다.
4. 백엔드에서 CVM에서 SCF로의 전환은 클라이언트측에 영향을 주지 않습니다.
![](https://main.qcloudimg.com/raw/d285c006b5945486a725936385d9dcb2.svg)
:::
::: CVM/SCF\s 비즈니스 전환
SCF를 사용하여 고탄력 서비스를 처리하고 CVM을 사용하여 타임 세일 및 스냅업 구매와 같은 시나리오에서 일상적인 비즈니스를 처리하는 데 적용할 수 있습니다.
1. DNS 확인을 통해 도메인 이름 A는 한 CLB 인스턴스의 VIP로 확인되고 도메인 이름 B는 다른 CLB 인스턴스의 VIP로 확인됩니다.
2. 하나의 CLB 인스턴스는 요청을 CVM으로 포워딩하고 다른 인스턴스는 이를 SCF로 포워딩합니다.
![](https://main.qcloudimg.com/raw/96a77f06ecad23ddf13282aa2e6a496b.svg)
:::

</dx-accordion>



## 제한 설명
- SCF와의 바인딩은 광저우, 상하이, 베이징, 청두, 중국홍콩, 싱가포르, 뭄바이, 도쿄 및 실리콘밸리에서만 사용할 수 있습니다.
- SCF 기능은 IP별 청구 계정의 CLB 인스턴스에만 바인딩할 수 있지만 CVM별 청구 계정에는 바인딩할 수 없습니다. CVM별 청구 계정을 사용하는 경우 IP별 청구 계정으로 업그레이드하는 것이 좋습니다. 자세한 내용은 [Checking Account Type](https://intl.cloud.tencent.com/document/product/684/15246)을 참고하십시오. 
- SCF 기능은 기본 네트워크 기반 CLB 인스턴스와 바인딩할 수 없습니다.
- 동일한 리전의 SCF 기능은 CLB 인스턴스와 바인딩될 수 있습니다. SCF 기능은 VPC에서만 바인딩할 수 있지만 리전에서는 바인딩할 수 없습니다.
- SCF 기능은 IPv4 및 IPv6 NAT64 CLB 인스턴스에만 바인딩할 수 있지만 현재 IPv6 CLB 인스턴스에는 바인딩할 수 없습니다.
- SCF 기능은 레이어 7 HTTP 및 HTTPS 리스너에만 바인딩할 수 있지만 레이어 7 QUIC 리스너 또는 레이어 4(TCP, UDP 및 TCP SSL) 리스너에는 바인딩할 수 없습니다.
- SCF ‘Event 함수’만 CLB 인스턴스와 바인딩할 수 있습니다.


## 전제 조건
1. [Creating CLB Instances](https://intl.cloud.tencent.com/document/product/214/6149)를 완료합니다.
2. [Configuring HTTP Listener](https://intl.cloud.tencent.com/document/product/214/32515) 또는 [Configuring HTTPS Listener](https://intl.cloud.tencent.com/document/product/214/32516)를 완료합니다.

## 작업 단계
![](https://main.qcloudimg.com/raw/eca21ba71ea22a6c240d3b4a05dfdce0.svg)

### 1단계: 함수 생성
1. [SCF 콘솔](https://console.cloud.tencent.com/scf)에 로그인하고 왼쪽 사이드바에서 [함수 서비스]를 클릭합니다.
2. ‘함수 서비스’ 페이지에서 [생성]을 클릭합니다.
3. ‘생성’ 페이지에서 생성 모드에 대해 ‘사용자 지정 생성’을 선택하고 함수 이름을 입력합니다. 그런 다음 CLB 인스턴스에 대해 선택한 동일한 리전을 선택하고 런타임 환경에 대해 ‘Python3.6’을 선택하고 입력 상자에 다음 코드를 입력하고(본문에서는 Hello CLB가 사용됨) [완료]를 클릭합니다.
>!CLB 인스턴스를 SCF 함수에 바인딩할 때 콘텐츠는 특정 응답 통합 형식으로 반환되어야 합니다. 자세한 내용은 [Integration response](https://intl.cloud.tencent.com/document/product/583/39849)를 참고하십시오.
```plaintext
# -*- coding: utf8 -*-
import json
def main_handler(event, context):

    return {
        "isBase64Encoded": False,
        "statusCode": 200,
        "headers": {"Content-Type":"text/html"},
        "body": "<html><body><h1>Hello CLB</h1></body></html>"
   }
```

### 2단계: 함수 배포
1. ‘함수 서비스’ 목록 페이지에서 생성한 함수의 이름을 클릭합니다.
2. ‘함수 관리’ 페이지에서 [함수 코드] 탭을 선택하고 하단의 [배포]를 클릭합니다.
![]()

### 3단계: 함수 바인딩
1. [CLB 콘솔](https://console.cloud.tencent.com/clb)에 로그인하고 왼쪽 사이드바에서 [인스턴스 관리]를 클릭합니다.
2. ‘인스턴스 관리’ 페이지 ‘CLB’ 탭에서 대상 인스턴스 오른쪽의 ‘작업’ 열에서 [리스너 구성]을 클릭합니다.
3. HTTP/HTTPS 리스너 섹션에서 SCF 함수와 바인딩할 리스너를 선택합니다. 리스너 왼쪽에 있는 [+] 아이콘과 펼쳐진 도메인 이름 왼쪽에 있는 [+]를 클릭하고 펼쳐진 URL 경로를 선택한 다음 [바인딩]을 클릭합니다.
![]()
4. 팝업 창에서 대상 유형으로 ‘SCF’를 선택하고, 네임 스페이스, 함수 명칭 버전/별칭을 선택하고, 가중치를 설정한 후, [확인]을 클릭합니다.
![]()
5. ‘리스너 관리’ 탭의 ‘포워딩 규칙’ 섹션에 CLB 인스턴스에 바인딩된 함수가 표시되어야 하며, 이는 CLB 트리거가 생성되었음을 나타냅니다.
![]()
>? SCF 콘솔에서 CLB 트리거를 생성하여 CLB 인스턴스를 SCF 기능과 바인딩할 수도 있습니다. 자세한 내용은 [Creating Triggers](https://intl.cloud.tencent.com/document/product/583/31441)를 참고하십시오.

## 결과 검증
1. [SCF 콘솔](https://console.cloud.tencent.com/scf)에 로그인하고 왼쪽 사이드바에서 [함수 서비스]를 클릭합니다.
2. ‘함수 서비스’ 페이지에서 방금 생성한 함수를 클릭합니다.
3. 왼쪽에서 [트리거 관리]를 클릭합니다.
4. ‘트리거 관리’ 페이지에서 액세스 경로를 클릭합니다.
![]()
5. 브라우저에서 액세스 경로를 엽니다. ‘Hello CLB’가 표시되면 함수가 성공적으로 배포된 것입니다.
![]()


## 관련 문서
[Creating Event Function in Console](https://intl.cloud.tencent.com/document/product/583/32742)
