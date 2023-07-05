## 작업 시나리오
일부 보안 그룹 규칙이 더는 필요하지 않으면 보안 그룹 규칙을 삭제할 수 있습니다.

## 전제 조건
- 보안 그룹을 생성하고 해당 보안 그룹에 보안 그룹 규칙을 추가.
<!--보안 그룹 생성 및 규칙 추가 방법은 [보안 그룹 생성](https://intl.cloud.tencent.com/document/product/213/34271)과 [보안 그룹 규칙 추가](https://intl.cloud.tencent.com/document/product/213/34272)를 참조 바랍니다.-->
- Cloud Virtual Machine(CVM) 인스턴스에 허용/차단할 필요가 없는 공용 네트워크 액세스 또는 내부 네트워크 액세스가 있는지 확인.

## 작업 순서
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/index)에 로그인합니다.
2. 왼쪽 메뉴에서 [[보안 그룹](https://console.cloud.tencent.com/cvm/securitygroup)]을 클릭하여 보안 그룹 관리 페이지에 접속합니다.
3. 보안 그룹 관리 페이지에서 [리전]을 선택하여 규칙 삭제가 필요한 보안 그룹을 찾습니다.
4. 규칙 삭제가 필요한 보안 그룹 행에서 작업 표시줄의 [Modify Rules]을 클릭하여 보안 그룹 규칙 페이지에 접속합니다.
5. 보안 그룹 규칙 페이지에서 삭제할 보안 그룹 규칙이 속한 바운드(인바운드/아웃바운드)에 따라 [Inbound/Outbound ] 탭을 클릭합니다.
6. 삭제할 보안 그룹 규칙을 찾으면, 작업 표시줄의 [Delete]를 클릭합니다.
7. 팝업 창이 나타나면 [OK]을 클릭합니다.



