
서버 이름 표시(Server Name Indication, SNI)는 서버와 클라이언트의 SSL/TLS 확장을 개선하기 위해 하나의 서버가 하나의 인증서만 사용할 수 있는 문제를 해결하기 위해 설계되었습니다. 서버가 SNI를 지원하는 경우 서버가 여러 인증서에 바인딩될 수 있음을 의미합니다. 클라이언트에 SNI를 사용하려면 서버에 대한 SSL/TLS 연결이 설정되기 전에 연결할 도메인 이름을 지정해야 합니다. 그러면 서버는 도메인 이름을 기반으로 적절한 인증서를 반환합니다.

## 시나리오
레이어 7 HTTPS CLB 리스너는 수신 규칙에서 서로 다른 도메인 이름에서 사용할 수 있는 여러 인증서 바인딩과 같은 SNI를 지원합니다. 예를 들어, CLB 인스턴스의 동일한 `HTTPS:443` 리스너에서 `*.test.com` 및 `*.example.com`에 대해 각각 인증서 1 및 인증서 2를 사용하여 이러한 도메인 이름의 요청을 두 개의 다른 서버 세트로 전달할 수 있습니다.

## 전제 조건
[CLB 인스턴스 구매](https://buy.cloud.tencent.com/lb)를 완료해야 합니다.


## 작업 단계
1. [CLB 콘솔](https://console.cloud.tencent.com/clb)에 로그인합니다.
2. [Configuring HTTPS Listener](https://intl.cloud.tencent.com/document/product/214/32516#.E6.AD.A5.E9.AA.A42.EF.BC.9A.E9.85.8D.E7.BD.AE.E7.9B.91.E5.90.AC.E5.99.A8)를 참고하여 리스너를 구성하고 SNI를 활성화합니다.
![](https://main.qcloudimg.com/raw/a70af5870cf3c02a97368f9bbb46f74f.png)
3. 리스너에 포워딩 규칙을 추가할 때 서로 다른 도메인 이름에 대해 서로 다른 서버 인증서를 구성합니다. 그런 다음 [다음]을 클릭하고 상태 확인 및 세션 지속성을 구성합니다.
![](https://main.qcloudimg.com/raw/e35b92e86b8bade2a0a77a64461a418d.png)
