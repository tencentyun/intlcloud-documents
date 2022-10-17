CLB는 레이어 7 리디렉션을 지원하므로 레이어 7 HTTP/HTTPS 리스너에서 리디렉션을 구성할 수 있습니다.
>?
>- 세션 지속성: 클라이언트가 `example.com/bbs/test/123.html`에 액세스하고 백엔드 CVM에서 세션 지속성이 활성화된 경우 `example.com/bbs/test/456.html`로 트래픽을 포워딩하기 위해 리디렉션이 활성화된 후 원래 세션 지속성 메커니즘이 적용되지 않습니다.
>- TCP / UDP 리디렉션: IP + Port 수준의 리디렉션은 현재 지원되지 않지만 이후 버전에서 사용할 수 있습니다.
## 리디렉션 개요
- 자동 리디렉션
  - 개요
  기존 `HTTPS:443` 리스너의 경우 포워딩을 위해 시스템에서 HTTP 리스너(포트 80)를 자동으로 생성합니다. `HTTP:80`으로 전송된 요청은 자동으로 `HTTPS:443`으로 리디렉션됩니다.
  - 사용 사례
 강제 HTTPS 리디렉션, 즉 HTTP 요청을 HTTPS로 리디렉션합니다. 사용자가 HTTP를 통해 PC 또는 모바일 브라우저에서 Web 서비스에 액세스하면 CLB는 포워딩을 위해 `HTTP:80`으로 전송된 모든 요청을 `HTTPS:443`으로 리디렉션합니다.
  - 강점
	 - Set-and-Forget 구성: 하나의 구성 작업만 필요하면 도메인 이름에 대해 강제 HTTPS 리디렉션을 구현할 수 있습니다.
	 - 편리한 업데이트: HTTPS 서비스의 URL 수가 변경되면 이 기능을 콘솔에서 다시 사용하여 새로고침하기만 하면 됩니다.
- 수동 리디렉션
 - 개요
일대일 리디렉션을 구성할 수 있습니다. 예를 들어 CLB 인스턴스에서 `리스너1 / 도메인 이름1 / URL1`을 `리스너2 / 도메인 이름2 / URL2`로 리디렉션을 구성할 수 있습니다.
>?도메인 이름이 자동 리디렉션으로 구성된 경우 수동 리디렉션을 구성할 수 없습니다.
>
 - 사용 사례
단일 경로 리디렉션. 예를 들어, 제품 품절, 페이지 유지보수, 업데이트 및 업그레이드 등의 경우 Web 비즈니스를 일시적으로 비활성화하려면 원래 페이지를 새 페이지로 리디렉션해야 합니다. 리디렉션이 수행되지 않으면 방문자의 즐겨찾기 및 검색 엔진 데이터베이스의 이전 주소가 `404/503` 오류 메시지 페이지를 반환하여 사용자 경험을 저하시키고 트래픽 낭비를 초래합니다.

## 자동 리디렉션
CLB는 HTTP에서 HTTPS로의 원클릭 강제 리디렉션을 지원합니다.
웹 사이트 `https://www.example.com`을 구성해야 한다고 가정합니다. 최종 사용자가 브라우저에서 HTTP 요청(`http://www.example.com`)을 보내든 HTTPS 요청(`https://www.example.com`)을 보내든 상관없이 HTTPS를 통해 안전하게 방문할 수 있습니다.

### 전제 조건
`HTTPS:443` 리스너가 구성되었습니다.

### 작업 단계
1. [CLB 콘솔](https://console.cloud.tencent.com/clb)에서 CLB HTTPS 리스너를 구성하고 `https://example.com`의 Web 환경을 설정합니다. 자세한 내용은 [Configuring HTTPS Listener](https://intl.cloud.tencent.com/document/product/214/32516)를 참고하십시오.
2. HTTPS 리스너 구성 결과는 아래와 같습니다.
![](https://main.qcloudimg.com/raw/6eaf2d1220d140bc37537f3388d78509.png)
3. CLB 인스턴스 세부 정보의 ‘리디렉션 구성’ 탭에서 **리디렉션 정책 생성**을 클릭합니다.
![](https://main.qcloudimg.com/raw/47fa6c0bd8b6f060332333b2685f8efe.png)
4. **자동 리디렉션 구성**을 선택하고 구성된 HTTPS 리스너 및 도메인 이름을 선택한 후 **다음: 경로 구성**을 클릭합니다.
![](https://main.qcloudimg.com/raw/4481d9beac8fa51ee7f6c252c3714a41.png)
5. **제출**을 클릭합니다.
![](https://main.qcloudimg.com/raw/435e1389eadacc7bc90966480a29a131.png)
6. 리디렉션을 구성한 후의 결과는 다음과 같습니다. `HTTP:80` 리스너는 `HTTPS:443` 수신기에 대해 자동으로 구성되었으며 모든 HTTP 트래픽은 자동으로 HTTPS로 리디렉션됩니다.
![](https://main.qcloudimg.com/raw/c3249968deb68888fb591e59289194d9.png)

## 수동 리디렉션
CLB는 일대일 리디렉션 구성을 지원합니다.
예를 들어, 귀하의 비즈니스는 프로모션 캠페인에 forsale 페이지를 사용하고 캠페인 종료 후 캠페인 페이지 `https://www.example.com/forsale`을 새 홈페이지 `https://www.new.com/index`로 리디렉션해야 합니다.

### 전제 조건
- HTTPS 리스너가 구성되어 있어야 합니다.
- 포워딩 도메인 이름 `https://www.example.com/forsale`이 구성되어 있어야 합니다.
- 포워딩 도메인 이름 및 경로 `https://www.new.com/index`가 구성되어 있어야 합니다.


### 작업 단계
1. [CLB 콘솔](https://console.cloud.tencent.com/clb)에서 CLB HTTPS 리스너를 구성하고 `https://example.com`의 Web 환경을 설정합니다. 자세한 내용은 [Configuring HTTPS Listener](https://intl.cloud.tencent.com/document/product/214/32516)를 참고하십시오.
2. HTTPS 구성의 결과는 다음과 같습니다.
![](https://main.qcloudimg.com/raw/5c1fc217e1795a2f6a7b31c2a7ba3bfc.png)
3. CLB 인스턴스 세부 정보의 ‘리디렉션 구성’ 탭에서 **리디렉션 정책 생성**을 클릭합니다.
![](https://main.qcloudimg.com/raw/47fa6c0bd8b6f060332333b2685f8efe.png)
4. **수동 리디렉션 구성**을 선택하고, 원래 액세스한 프론트엔드 프로토콜 포트 `HTTPS:443` 및 도메인 이름 `https://www.example.com/forsale`을 선택하고, 리디렉션 후 프런트엔드 프로토콜 포트 `HTTPS:443` 및 도메인 이름 `https://www.new.com/index`를 선택하고, **다음: 경로 구성**을 클릭합니다.
![](https://main.qcloudimg.com/raw/51106736b5ee61d6e87767652185d57a.png)
5. 원래 액세스 경로로 `/forsale`을 선택하고 리디렉션 후 액세스 경로로 `/index`를 선택하고 **제출**을 클릭하여 구성을 완료합니다.
![](https://main.qcloudimg.com/raw/5f59b88ecc291d912b7faf2cf1d3770e.png)
6. 리디렉션 구성의 결과는 다음과 같습니다. `HTTP:443` 리스너에서 `https://www.example.com/forsale`이 `https://www.new.com/index`로 리디렉션되었습니다.
![](https://main.qcloudimg.com/raw/34364863bd44202df54e89ec3cb923f9.png)


