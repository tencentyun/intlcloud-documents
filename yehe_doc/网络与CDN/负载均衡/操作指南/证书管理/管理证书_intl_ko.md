CLB(Cloud Load Balancer) 인스턴스의 HTTPS 리스너를 구성할 때 SSL 인증서 서비스에서 인증서를 직접 사용하거나 타사 CA에서 발급한 서버 인증서와 [ SSL Certificate ](https://intl.cloud.tencent.com/document/product/1007/30152)를 CLB에 업로드할 수 있습니다.

## 인증서 요구 사항
CLB는 PEM 형식의 인증서만 지원합니다. 인증서를 업로드하기 전에 인증서, 인증서 체인 및 개인 키가 형식 요구 사항을 충족하는지 확인하십시오. 인증서 요구 사항은 [Certificate Requirements and Certificate Format Conversion](https://intl.cloud.tencent.com/document/product/214/5369)을 참고하십시오.

## 인증서 구성
HTTPS 리스너에 대한 인증서 구성은 다음 두 가지 유형으로 나뉩니다.
- SNI가 활성화되지 않은 경우 모든 도메인 이름이 동일한 인증서를 사용하는 리스너 레벨에서 인증서를 구성할 수 있습니다. 자세한 내용은 [Configuring HTTPS Listener](https://intl.cloud.tencent.com/document/product/214/32516)를 참고하십시오.
- SNI가 활성화된 경우 도메인 이름 레벨에서 인증서를 구성할 수 있으며 리스너 아래의 다른 도메인 이름에 대해 다른 인증서를 구성할 수 있습니다. 자세한 내용은 [SNI Support for Binding Multiple Certificates to a CLB Instance](https://intl.cloud.tencent.com/document/product/214/19048)를 참고하십시오.

## 인증서 일괄 업데이트
인증서 만료가 서비스에 영향을 미치지 않도록 하려면 만료되기 전에 인증서를 업데이트하십시오.
>?인증서가 업데이트된 후 시스템은 레거시 인증서를 삭제하지 않습니다. 대신 새 인증서를 생성합니다. 인증서를 사용하는 모든 CLB 인스턴스에 대해 인증서가 자동으로 업데이트됩니다.

1. [CLB 콘솔](https://console.cloud.tencent.com/clb)에 로그인합니다.
2. 왼쪽 사이드바에서 [인증서 관리]를 클릭합니다.
3. ‘인증서 관리’ 페이지의 인증서 목록에서 대상 인증서 오른쪽의 ‘작업’ 열에서 [업데이트]를 클릭합니다.
4. 팝업되는 ‘인증서 생성’ 대화 상자에서 새 인증서의 인증서 내용과 주요 내용을 입력하고 [제출]을 클릭합니다.
![](https://main.qcloudimg.com/raw/d6534b57f4a33fab69b98fca4d1023f3.png)

## 인증서와 연결된 CLB 인스턴스 보기
1. [CLB 콘솔](https://console.cloud.tencent.com/clb)에 로그인합니다.
2. 왼쪽 사이드바에서 [인증서 관리]를 클릭합니다.
3. ‘인증서 관리’ 페이지의 인증서 목록에서 대상 인증서의 ID를 클릭합니다.
4. ‘기본 정보’ 페이지에서 인증서와 연결된 CLB 인스턴스를 확인합니다.
![](https://main.qcloudimg.com/raw/b3670e111ec8b9e1a43b9c7d2e870be3.png)
