## SNI가 무엇인가요?
서버 이름 지시(SNI)는 서버와 클라이언트 SSL/TLS의 확장을 개선하는 데 사용되며 주로 1대의 서버가 1개의 인증서만 사용할 수 있는 단점을 해결하며, SNI 지원은 서버가 여러 개의 인증서를 바인딩할 수 있음을 의미합니다. 클라이언트가 SNI를 사용하려면 서버와 SSL/TLS 연결을 생성하기 전에 연결할 도메인 이름을 지정해야 하며, 서버는 이 도메인 이름에 따라 적합한 인증서를 반환하게 됩니다. CLB의 SNI 지원 기능이 내부 테스트 중이고 사용하려면 [티켓 신청](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=163&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%20LB)을 진행하십시오.

Tencent Cloud 응용형 CLB의 7계층 HTTPS 수신기는 SNI를 지원합니다. 즉, 여러 개의 인증서 바인딩을 지원하므로 수신 규칙 중 다른 도메인 이름은 다른 인증서를 사용할 수 있습니다.
## 사용 전제
SNI를 사용하여 여러 개의 인증서를 바인딩하려면 다음 전제 조건을 만족시켜야 합니다.
- **응용형** CLB 인스턴스를 구매했어야 합니다.
- 인증서를 보유하고 있어야 합니다.

## 작업 절차
### 응용형 CLB 구매
1. [CLB 콘솔](https://console.cloud.tencent.com/loadbalance)에 로그인합니다.
2. 응용형 CLB를 [구매](https://buy.cloud.tencent.com/lb)합니다.

### HTTPS 수신기 생성 및 SNI 구성
1. HTTPS 수신기 생성 시, 여러 도메인 이름이 공용하는 인증서를 종료합니다.
여러 도메인 이름이 공용하는 인증서란 서버의 여러 개의 도메인 이름이 1개의 인증서를 공용하고, 즉 SNI 종료를 의미합니다. 여러 도메인 이름이 공용하는 인증서를 종료하면 SNI 시작을 의미하며, 서버는 도메인 이름별 다른 인증서 사용을 지원합니다.
 ![](https://main.qcloudimg.com/raw/6e8495b977902008382d6bb622116556.png)
2. 해당 수신기에 포워딩 규칙을 추가할 경우, 도메인 이름별로 다른 서버 인증서를 선택할 수 있습니다.
 ![](https://main.qcloudimg.com/raw/94089a2f01a2539df72787ae11804974.png)

