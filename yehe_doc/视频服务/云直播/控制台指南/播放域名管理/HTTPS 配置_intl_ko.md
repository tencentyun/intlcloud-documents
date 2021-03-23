## 개요
HTTPS 프로토콜은 SSL 및 HTTP 프로토콜을 기반으로 구축된 네트워크 프로토콜로 암호화된 전송과 인증에 사용됩니다. HTTPS 프로토콜은 HTTP 프로토콜보다 보안성이 더 뛰어납니다. HTTPS 가속을 활성화하려는 경우 재생 도메인 이름에 대해 HTTPS 기능을 활성화하고 유효한 인증서를 설정하면 됩니다. 인증서는 Tencent Cloud [SSL 인증서 서비스](https://intl.cloud.tencent.com/product/ssl)에서 구입할 수 있습니다. 이미 인증서가 있으면 인증서를 CSS 콘솔에 업로드하여 설정할 수 있습니다. 현재 LVB에서는 PEM 형식만 지원합니다. 인증서가 다른 형식으로 되어 있으면 먼저 PEM 형식으로 변환해야 합니다. 인증서 형식 요구사항과 설정 방법은 다음과 같습니다.

## 전제 조건
- [CSS 콘솔](https://console.cloud.tencent.com/live)에 로그인합니다.
- [재생 도메인 이름을 추가](https://intl.cloud.tencent.com/zh/document/product/267/35970)합니다.

## 작업 순서 
### 1단계. HTTPS 설정 편집
1. <b>[도메인 관리 페이지](https://console.cloud.tencent.com/live/domainmanage)</b>로 이동하여 설정할 **재생 도메인 이름**을 클릭하거나 오른쪽에 있는 **관리**를 클릭하고 도메인 이름 세부 정보 페이지에 해당 정보를 입력합니다.
2. **고급 설정**을 선택하여 **HTTPS 설정** 탭을 표시합니다.
3. **편집**을 클릭하여 HTTPS 설정 페이지로 이동하고 ![](https://main.qcloudimg.com/raw/897761946b06e8f904bfa6301d282817.png)을 클릭하여 HTTPS 서비스를 활성화합니다.
4. 설정할 인증서 원본을 선택하고 관련 정보를 입력한 후 **저장**을 클릭합니다.
<table>
<tr><th>인증서 원본</th><th>필수 설정 항목</th></tr>
<tr>
<td>자체 소유 인증서</td>
<td><ul style="margin:0">
<li>인증서 이름: 인증서 식별하기 위해 사용자 지정된 이름을 입력합니다.</li>
<li>인증서 내용: Nginx용 <code>.crt</code> 파일의 내용을 입력합니다. 자세한 내용은 <a href="#content">인증서 내용</a>을 참조하십시오.</li>
<li>프라이빗 키 내용: Nginx용 <code>.key</code> 파일의 내용을 입력합니다. 자세한 내용은 <a href="#private_key">인증서 키</a>를 참조하십시오.</li><ul></td>
</tr><tr>
<td>Tencent 클라우드로 호스팅되는 인증서</td>
<td>인증서 목록: <a href="https://console.cloud.tencent.com/ssl">SSL 인증서 서비스</a>에서 업로드된 인증서를 선택합니다.</td>
</tr></table>
<img src="https://main.qcloudimg.com/raw/023725d33c3fdc4e06a4a4eb1791a578.png"></img>

#### 인증서 설명
최상위 [CA](https://intl.cloud.tencent.com/zh/document/product/1007/30192#354)에서 Apache, IIS, Nginx 및 Tomcat 웹 서버용 인증서를 발급합니다. **CSS 암호화에는 Nginx를 사용하므로 Nginx 파일을 선택하여 설정해야 합니다.** 
**SSL 인증서 서비스 콘솔** > **[인증서 관리](https://console.cloud.tencent.com/ssl)**로 이동하여 대상 인증서를 선택하고 "작업" 열에서 **다운로드**를 클릭한 후, 다운로드한 패키지의 압축을 풀어 다음 파일을 가져옵니다.
  ![](https://main.qcloudimg.com/raw/f67e31bfa2c233cf8dc0c4a1e58cb6fc.png)
- <b id="content">인증서 내용</b>: Nginx용 `.crt`파일에서 `-----BEGIN CERTIFICATE-----`와 `-----END CERTIFICATE-----` 사이에 있는 전체 내용을 입력합니다.
**예시:**
![](https://main.qcloudimg.com/raw/e6c61fda3637a2f11e56cec30f0f7bd3.png)
>?보유한 인증서를 중간 CA에서 발급했고 이 인증서에 여러 개의 인증서가 포함된 경우 인증서 내용은 다음과 같이 연결되어 있습니다.
-----BEGIN CERTIFICATE-----
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
-----END CERTIFICATE-----
- <b id="private_key">인증서 프라이빗 키</b>: Nginx용 `.key`파일에서 `----BEGIN RSA PRIVATE KEY-----`와 `-----END RSA PRIVATE KEY-----` 사이에 있는 전체 내용을 입력합니다.
**예시:**
![](https://main.qcloudimg.com/raw/1ca20b0021b49ccb407df43675be37ba.png)

### 2단계. 설정 확인
HTTPS 설정은 약 2시간 후에 적용됩니다. 인증서를 제출하고 약 2시간 후에 도메인 이름으로 접속하십시오. 브라우저의 주소 표시줄에 HTTPS가 표시되면 설정된 것입니다.
![](https://main.qcloudimg.com/raw/b1f54ec35855e5d2adbaeae96a04ef13.png)

### 3단계. 설정 수정
HTTPS 기능은 활성화 및 비활성화할 수 있습니다. HTTPS 기능을 비활성화하면 LVB에서 해당 도메인 이름에 더 이상 HTTPS 서비스를 제공하지 않습니다. 인증서가 만료되면 유효한 새 인증서로 교체해야 합니다.


 >? 인증서에 대한 자세한 내용은 [SSL 인증서 서비스](https://intl.cloud.tencent.com/document/product/1007/30168)를 참조하십시오.
