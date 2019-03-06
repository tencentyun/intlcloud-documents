이 문서는 새로운 사용자가 Tencent Cloud CLB를 사용하는 방법을 소개합니다. `clb-test`라는 전통형 공중망 CLB 인스턴스 1개를 생성하고 출처가 클라이언트로온 요청을 백 엔드 CVM 두 대에 포워딩합니다.

## 전제 조건
1. CLB는 트래픽을 포워딩만 책임지고 요청을 처리할 능력을 보유하지 않았기 때문에 사용자 요청을 처리할 수 있는 CVM 인스턴스를 보유해야 합니다.
본 예제 중 CVM 인스턴스 두 대를 보유하면 되며, CVM 수량을 스스로 기획할 수도 있습니다. 본 예제에서는 광저우 지역에 이미 CVM 인스턴스 `rs-1`과 `rs-2`를 생성하였습니다. CVM 인스턴스 생성에 관련 내용은 [CVM 인스턴스 구매 및 시작](https://cloud.tencent.com/document/product/213/4855)을 참조하십시오.
2. 본문은 HTTP 포워딩을 예로 하고 있으며, CVM에는 Apache, Nginx, IIS 등과 같은 해당하는 Web 서버를 배포해야 합니다.
결과를 인증하기 위해 예제는 `rs-1`에 Apache를 배포하고 "Hello Tomcat! This is rs-1!"이 첨부된 HTML을 반환하였으며, `rs-2`에는 Apache를 배포하고 "Hello Tomcat! This is rs-2!"가 첨부된 HTML을 반환하였습니다. CVM에 서비스 배포에 관련 더 많은 내용은 [Linux(CentOS)에 Java Web 배포](게시 예정) 및 [Windows에 PHP 설치 및 구성](https://cloud.tencent.com/document/product/213/10182)을 참조하십시오.
3. CVM의 공인 IP + 경로에 접근하십시오. 배포한 페이지가 보인다면 배포에 성공하였음을 증명합니다.

> 주의:
현재 대역폭 속성이 CLB가 아닌 CVM에 있기 때문에 CVM에는 반드시 공중망 대역폭을 구매해야 합니다.
> - 예제 중 RS에 배포한 서비스 반환값이 다르며, 실제 상황에서 모든 사용자가 같은 체험을 유지할 수 있도록 일반적으로 RS에 완전 동일한 서비스를 배포합니다.

## 전통형 CLB 인스턴스 구매
1. Tencent Cloud [CLB 서비스 구매 페이지](https://buy.cloud.tencent.com/lb)에 로그인합니다.
2. 이 예는 CVM과 같은 [광저우] 지역을 선택하고 인스턴스 유형은 [전통형]을 선택하고, 네트워크 속성은 [공중망]을 선택하고, 네트워크는 [Default-VPC(기본)]을 선택하였으며 인스턴스 이름에 [clb-test]를 입력했습니다.
3. [즉시 구매] 버튼을 클릭하여 지불을 완료합니다.
CLB 인스턴스 관련 더 많은 내용은 [구매 속성 가이드](게시 예정)를 참조하십시오.
![](https://main.qcloudimg.com/raw/fbe58e6536dbd0b24d383f892dc6446d.png)
4. [LB 인스턴스 목록] 페이지에서 해당 지역을 선택하면 새로 생성한 인스턴스를 볼 수 있습니다.
![](https://main.qcloudimg.com/raw/181110567fc16a3ad9a3547ef8e53dc1.png)

## CLB 수신기 생성
CLB 수신기는 지정한 프로토콜 및 포트를 통해 실제 포워딩합니다. 이 문서는 CLB가 클라이언트에 포워딩하는 HTTP 요청 구성을 예로 하고 있습니다.
1. [Tencent Cloud 콘솔](https://console.cloud.tencent.com/)에 로그인하여 [클라우드 제품]-[네트워크]-[CLB]를 클릭하여 CLB 콘솔에 진입합니다.
2. [LB 인스턴스 목록]에서 생성한 전통형 CLB 인스턴스 `clb-test`를 찾아내고 인스턴스 ID를 클릭하여 CLB 세부 정보 페이지에 진입합니다.
3. [기본 정보] 부분에서 이름 뒤의 작은 아이콘을 클릭하여 인스턴스 이름을 수정할 수 있습니다.
4. [수신기 관리]의 [수신기]에서 [생성] 버튼을 클릭하여 CLB 수신기를 생성합니다.
![](https://main.qcloudimg.com/raw/f0e2d9431fd7eebfffd96e4392e3a70a.png)
5. 팝업창에서 아래 내용을 구성합니다.
  - 이름을 'Listener1'로 사용자 지정.
  - 수신 프로토콜 포트는 `HTTP: 80`임.
  - 백 엔드 포트는 `80`임.
  - 밸런싱 방식으로 ‘가중치에 따라 라운드 로빈’ 선택
  - 세션 유지를 선택하지 않음
  - 상태 검사 활성화.
  - [완료] 버튼을 클릭하여 CLB 수신기 생성을 완료합니다.
![](https://main.qcloudimg.com/raw/84f8d4b675e1095d3efa193f3ded0281.png)

CLB 수신기 관련 더 많은 내용은 [CLB 수신기 개요](https://cloud.tencent.com/document/product/214/6151)를 참조하십시오.

## 백 엔드 CVM 바인딩
1. [LB 인스턴스 목록]에서 방금 생성한 `clb-test`를 찾아내고 ID를 클릭하여 CLB 세부 정보 페이지에 진입합니다.
2. [수신기 관리]의 [CVM 바인딩] 모듈에서 [CVM 바인딩] 버튼을 클릭합니다.
![](https://main.qcloudimg.com/raw/6fd77c5e62f56f73ada410d8fad8de09.png)
3. 팝업창에서 CLB와 같은 지역의 CVM 인스턴스 `rs-1`과 `rs-2`를 선택하고 가중치를 모두 기본값 `10`으로 설정합니다.
4. [확인] 버튼을 클릭하여 바인딩을 완료합니다.
![](https://main.qcloudimg.com/raw/014e181f64fcc1e22e6bd90f3ebe5bc6.png)
5. 수신기 [Listener1]을 열면 백 엔드 CVM의 상태 검사 상태를 확인할 수 있습니다. 상태가 "정상" 상태일 경우 CVM이 CLB 포워딩 요청을 정상적으로 처리할 수 있습니다.
![](https://main.qcloudimg.com/raw/9f43f89b03bd0845749cb1c90413c97d.png)

## CLB 서비스 인증
웹 브라우저에 CLB의 서비스 주소와 포트 http://vip:80을 입력하고 CLB 서비스를 테스트합니다. 다음과 같이 이번 요청이 CLB에 의해 rs-1 CVM에 포워딩되었음이 표시되며 CVM은 요청을 정상적으로 처리하고 반환합니다.
![](https://main.qcloudimg.com/raw/5df0db4039dfb4864af5db6b9c6cc3c1.png)

이 수신기의 라운드 로빈 알고리즘은 "가중치로 라운드 로빈"이며 CVM 두 대의 가중치는 모두 10입니다. 웹 브라우저를 세로고침하면 요청이 다시 발송되어 이번 요청이 CLB에 의해 rs-2 CVM에 포워딩되었음을 간주합니다.
![](https://main.qcloudimg.com/raw/ac62269e1fa5373f65c76f9134d96589.png)

> 주의:
> - 사용자가 세션 유지 기능을 끄고 라운드 로빈 방식으로 스케줄링하면 요청이 각기 다른 RS에 순서대로 할당됩니다.
> - 사용자가 세션 유지 기능을 켜거나 세션 유지 기능을 껐지만 ip_hash 스케줄링 방식을 선택하였을 경우, 요청은 동일 RS에 할당됩니다.

## 도메인 이름 구매 및 CLB 인스턴스(선택 가능)에 분석
1. [Tencent Cloud 도메인 이름 등록 페이지](https://dnspod.cloud.tencent.com)를 열어 도메인 이름 조회와 등록을 진행합니다. Qcloudtest.com을 예로 하며, 세부 정보는 [도메인 이름 등록](https://cloud.tencent.com/document/product/242/9595)을 참조하십시오.
2. [Tencent Cloud 콘솔](https://console.cloud.tencent.com/)에 로그인하여 [클라우드 제품]-[도메인 이름과 웹 사이트]-[CDNS]를 클릭합니다.
3. 구매하려는 [도메인 이름]을 클릭하고 [도메인 이름 DNS 관리] 페이지에서 [기록 추가] 버튼을 클릭하여 도메인 이름에 A 기록을 추가하고 다음 내용을 입력합니다.
  - 기록 유형: `A 기록`
  - 호스트 기록: 즉, 도메인 이름 접두사. 이 예제는 모든 접두사를 예로 하고 있으며 `*.qcloudtest.com`으로 설정합니다.
  - 회선 유형: 기본값
  - 기록값: [클라우드 리소스 연결]을 클릭하여 팜업창에서 방금 생성한 `clb-test`를 선택합니다.
  - TTL: 기본값 `600s`로 설정.
  - 추가 완료 후 [저장]을 클릭합니다.

CDNS(클라우드 도메인 이름 서비스)가 인터넷을 통해 레코드를 전송하는 데는 어느 정도 시간이 걸립니다. 도메인 이름이 정상적으로 해석하고 있는지를 테스트하려면 해석 레코드가 얼마 동안 추가된 경우 바인딩된 CNAME 도메인 이름(예: www.qcloudtest.com)에 직접 액세스 할 수 있습니다. 이 방법으로 CLB를 검증할 수 있습니다.
