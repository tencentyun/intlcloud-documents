### CVM으로 소규모 웹 사이트를 호스팅할 경우, 평상시의 유지보수는 어떻게 해야 하나요?
웹 사이트 애플리케이션 점검 시, 다음의 유지보수 작업을 권장합니다.
- CBS 데이터를 자주 백업합니다. 자세한 내용은 [스냅샷 생성](https://intl.cloud.tencent.com/document/product/362/5755)을 참조 바랍니다.
- SSL 인증서 서비스 사용을 권장합니다. SSL 인증서 서비스를 사용하면 웹 사이트의 인증 및 데이터 암호화 전송이 가능합니다. 자세한 내용은 [SSL 인증서](https://intl.cloud.tencent.com/document/product/1007/30152)를 참조 바랍니다.
- 악성 소프트웨어 검출 플러그 인, DDoS 공격 방어 서비스를 설치하거나 HS 서비스를 구매합니다.
- 웹 사이트 인바운드/아웃바운드 트래픽 현황을 모니터링하여 비정상적인 트래픽을 식별합니다. 액세스를 차단하는 보안 그룹 규칙을 추가하여 비정상적인 요청에 대해 제어할 수 있습니다. 자세한 내용은 [인스턴스 모니터링 데이터 획득](https://intl.cloud.tencent.com/document/product/213/5178) 및 [보안 그룹 규칙 추가](https://intl.cloud.tencent.com/document/product/213/34272)를 참조 바랍니다.
- CVM 인스턴스 및 클라우드의 성능을 모니터링하여 트래픽 액세스 피크 기간을 확인합니다. 업/다운그레이드, Auto Scaling, CBS  확장 등의 작업을 사전에 숙지하여 갑작스러운 피크 시의 요청에 대비합니다. 자세한 내용은 [인스턴스 설정 변경](https://intl.cloud.tencent.com/document/product/213/2178), [Auto Scaling은?](https://intl.cloud.tencent.com/document/product/377/3154), [확장 시나리오 소개](https://intl.cloud.tencent.com/document/product/362/31600)를 참조 바랍니다.
- root/Administrator 사용자 이름 및 비밀번호 자격 증명 방식으로 CVM 인스턴스에 로그인하는 시나리오의 경우, 관리자 비밀번호를 정기적으로 업데이트해야 합니다. 자세한 내용은 [인스턴스 비밀번호 재설정](https://intl.cloud.tencent.com/document/product/213/16566)을 참조 바랍니다.
- 소프트웨어 패치를 정기적으로 업데이트합니다.

