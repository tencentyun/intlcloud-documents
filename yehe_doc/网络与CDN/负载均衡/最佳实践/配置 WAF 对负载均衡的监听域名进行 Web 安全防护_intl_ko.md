[CLB WAF](https://intl.cloud.tencent.com/document/product/627/17470)는 도메인 이름을 CLB 리스너와 바인딩하여 CLB 리스너를 통과하는 HTTP 또는 HTTPS 트래픽을 감지하고 차단할 수 있습니다. 본문은 CLB WAF를 사용하여 CLB에 추가된 도메인 이름에 Web 보안 보호를 적용하는 방법을 소개합니다.

## 전제 조건
- CLB WAF는 현재 베타 버전입니다. 사용하려면 신청서를 제출해야 합니다.
- HTTP 또는 HTTPS 리스너를 생성 완료하여 도메인 이름에 액세스할 수 있어야 합니다. 자세한 내용은 [Getting Started with CLB](https://intl.cloud.tencent.com/document/product/214/8975)를 참고하십시오.
- CLB WAF 서비스를 구입 완료해야 합니다. 자세한 내용은 [Purchase Guide](https://intl.cloud.tencent.com/document/product/627/11730)를 참고하십시오.

## 제한 조건
현재 IPv4 CLB 인스턴스만 CLB WAF 보호를 지원하며 이 기능은 IPv6 및 IPv6 NAT64에 사용할 수 없습니다.

## 작업 단계
<span id ="step1"></span>
### 1단계: CLB 도메인 이름 구성 확인
본문은 `www.example.com`이라는 도메인 이름을 예로 들어 설명합니다.
1. [CLB 콘솔](https://console.cloud.tencent.com/clb)에 로그인하고 왼쪽 사이드바에서 CLB 인스턴스 목록을 클릭하여 [인스턴스 관리] 페이지로 이동합니다.
2. ‘인스턴스 관리’ 페이지에서 인스턴스 영역을 선택한 다음 대상 인스턴스의 오른쪽에 있는 ‘작업’ 열에서 [리스너 구성]을 클릭합니다.
3. ‘리스너 관리’ 탭을 선택하고 ‘HTTP/HTTPS 리스너’ 섹션에서 대상 리스너 왼쪽의 [+] 아이콘을 클릭하여 도메인 이름 세부 정보를 확인합니다.
![](https://main.qcloudimg.com/raw/1d546d69bc1d88faf15ef7acc9270468.png)
4. 다음과 일치하도록 CLB 도메인 이름 구성을 확인하십시오. CLB 인스턴스 ID: ‘lb-f8lm****’,  리스너 이름: ‘http-test’, 도메인 이름: `www.example.com`, 도메인 이름 보호 상태: ‘비활성화됨’(ID, 이름 및 도메인 이름은 실제 경우에 따라 다름).

### 2단계: WAF 콘솔에서 도메인 이름 추가 및 CLB 인스턴스에 바인딩
CLB WAF 서비스로 도메인 이름에 보호를 적용하려면 WAF에 CLB 수신 도메인 이름을 추가하고 CLB 리스너와 바인딩해야 합니다.
1. [WAF 콘솔](https://console.cloud.tencent.com/guanjia/waf/config)에 로그인하고 왼쪽 사이드바에서 [Web Application Firewall]>[보호 설정]을 선택합니다.
2. [CLB] 탭을 선택합니다.
3. [도메인 추가]를 클릭합니다.
![](https://main.qcloudimg.com/raw/5dc4d9c0363a2fe2713f157606efce19.png)
4. ‘도메인 이름을 입력’하고 [다음]을 클릭합니다.
![](https://main.qcloudimg.com/raw/fadb7336503e5ee808fe8a02d9b12005.png)
5. CLB 리전을 선택한 다음 <a href="#step1">1단계: CLB 도메인 이름 구성 확인</a>에서 도메인 이름을 선택하고 [리스너 선택]을 클릭합니다.
![](https://main.qcloudimg.com/raw/4b632c6769bbbe105027e8bdf0b3ba1a.png)
6. 팝업 창의 <a href="#step1">1단계: CLB 도메인 이름 구성 확인</a>에서 CLB 리스너를 선택한 후 [확인]을 클릭합니다.
![](https://main.qcloudimg.com/raw/2793320edb9a79b0c46e4ea4e92e38f6.png)
7. ‘리스너 선택’ 단계에서 [완료]를 클릭하여 WAF에서 CLB 리스너와 도메인 이름 바인딩을 완료합니다.
8. ‘도메인 목록’ 페이지로 돌아가서 도메인 이름, 리전, 바인딩된 CLB 인스턴스 ID, 리스너 및 기타 정보를 확인합니다.

### 3단계: 결과 확인
1. <a href="#step1">1단계: CLB 도메인 이름 구성 확인</a>의 지침에 따라 도메인 이름을 확인합니다. 도메인 이름 보호가 ‘활성화’되고 트래픽 모드가 ‘미러’인 경우 도메인 이름 보호가 활성화됩니다.
 -  도메인 이름에 대한 DNS 리졸브를 구성하지 않은 경우 [Step 2. Perform Local Testing](https://intl.cloud.tencent.com/document/product/627/35652)을 참고하여 WAF 보호가 활성화되었는지 확인하십시오.
 -  도메인 이름에 대해 DNS 리졸브를 구성한 경우 아래 지침에 따라 WAF 보호가 활성화되어 있는지 확인하십시오.
2. 브라우저를 통해 `http://www.example.com/?test=alert(123)`를 방문하십시오.
3. [WAF 콘솔](https://console.cloud.tencent.com/guanjia/waf/config)에 로그인한 다음 왼쪽 사이드바에서 [로그 서비스]>[공격 로그]를 선택합니다.
4. ‘로그 검색’ 탭을 선택하고 추가된 보호 도메인 이름 `www.example.com`을 선택한 후 [검색]을 클릭합니다. CLB에 구성된 도메인 이름에 대한 WAF 보호는 로그 목록에 ‘XSS 공격’ 로그가 있는 경우에 유효합니다.

