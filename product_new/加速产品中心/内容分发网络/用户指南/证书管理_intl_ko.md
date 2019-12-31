CDN에 이미 액세스 한 도메인 이름에 대해 HTTPS 인증서를 구성 할 수 있습니다. CDN은 기존 인증서 또는 Tencent Cloud [SSL 인증서 관리](https://console.cloud.tencent.com/ssl) 콘솔에서 호스팅 또는 발급 된 인증서 구성을 지원합니다.
>인증서 만료 30일 전, 15일 전, 7일 전 및 만료 당일에 Tencent Cloud는 SMS, 메일, 내부 메시지 형태로 사용자 계정에 만료 알림을 보냅니다. 현재 이미 SSL 인증서 사용자 정의 수신자 알람이 지원되고 있으며 [메시지 예약 구독](https://console.cloud.tencent.com/message/subscription) 구성으로 이동할 수 있습니다.

## 인증서 및 개인키
사용자의 도메인 이름 구성에 기존 인증서가 있으면 이하 내용을 먼저 알아야 합니다.
>사용자의 구성이 Tencent Cloud [SSL 인증서 관리](https://console.cloud.tencent.com/ssl) 콘솔에서 호스팅하거나 발급한 인증서인 경우, 해당 부분을 건너 뛰고 바로 [인증서 구성](#configuration) 프로세스를 확인 하십시오.

인증 기관(CA)에서 제공한 인증서는 일반적으로 다음과 같이 몇 가지 종류가 있습니다. 그 중 CDN이 사용하는 것은 **Nginx ** 입니다.
![](https://main.qcloudimg.com/raw/a2c1b413f9cf770cf7facdb3e424eac4.png)
Nginx 폴더로 이동하여 텍스트 편집기에서 ".crt"(인증서) 파일과 ".key"(개인키) 파일을 열어 인증서 내용과 개인키 내용을 PEM 형식으로 봅니다.
![](https://main.qcloudimg.com/raw/2a1b11ff93a7cb475d68e38c7701434f/Nginx_certificate.png)

### 인증서
인증서 확장명은 일반적으로 ".pem", ".crt" 또는 ".cer"입니다. 텍스트 편집기에서 인증서 파일을 열면 인증서의 내용이 아래 형식과 비슷합니다.
인증서 PEM 형식: "——- BEGIN CERTIFICATE ——-"으로 시작하고, "——- END CERTIFICATE ——-"로 끝납니다. 중간 내용은 한 줄에 64글자이며 마지막 줄은 64글자 미만일 수 있습니다.
![](https://main.qcloudimg.com/raw/60ea02d1a2c9623526d7fa79403e658a.jpg)
만약 중급 인증 기관(CA)에서 인증서를 발급 받은 경우 인증서 파일에 여러 인증서가 포함되어 있으므로 서버 인증서와 중간 인증서를 함께 수동으로 업로드해야 합니다. 연결 규칙은 서버 인증서를 첫 번째로 두고, 중간 인증서를 두 번째로 두어야 하며 중간 인증서에는 중간에 빈 줄이 없어야 합니다. 일반적인 상황에서는 기관에서 인증서를 발행할 때 해당 설명이 표시되므로 주의해서 확인하십시오.

>- 인증서 사이에 빈 줄이 없어야 합니다.
>- 각 인증서는 PEM 형식이어야 합니다.

중급 기관에서 발행한 인증서 체인 형식은 다음과 같습니다.
```
-----BEGIN CERTIFICATE-----
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
-----END CERTIFICATE-----
```
### 개인키
개인키 확장명은 일반적으로 ".pem" 또는 ".key"입니다. 텍스트 편집기에서 개인키 파일을 열면 아래 형식과 유사한 개인키 내용을 볼 수 있습니다.
개인키 PEM 형식: "——- BEGIN RSA PRIVATE KEY ——-"으로 시작하고 "——- END RSA PRIVATE KEY ——-"로 끝납니다. 중간 내용은 한 줄에 64자이며 마지막 줄은 64자 미만입니다.
![](https://main.qcloudimg.com/raw/e10009916aeb00d5158a3703115d0354.jpg)
“——-BEGIN PRIVATE KEY——-”으로 시작하고, “——-END PRIVATE KEY——-”로 끝나는 개인키의 경우 openssl 도구를 사용하는 것이 좋습니다. 형식 변환 명령은 다음과 같습니다.
```
openssl rsa -in old_server_key.pem -out new_server_key.pem
```

<span ID ="configuration"></span>
## 인증서 구성
1. [CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인하고 왼쪽 메뉴의 [고급 도구]에서 [인증서 관리]를 클릭하여 관리 페이지로 진입합니다.
2. [인증서 구성]을 클릭하여 인증서 구성 페이지로 진입합니다.
![](https://main.qcloudimg.com/raw/e72970f28fc8539eb1317ad24a41bbcb.png)

### 도메인 이름 선택
[도메인 이름] 드롭다운 메뉴에서 인증서를 구성 할 도메인 이름을 선택하십시오.
![인증서 도메인 이름](https://main.qcloudimg.com/raw/4288a4be379e61addc777b3c3d017ebf.png)

>+ 인증서 구성의 도메인 이름이 이미 Tencent Cloud CDN에 연결되어 있어야 하며 도메인 이름 상태는 ** 배포 중 **또는 ** 활성화 중 **이어야 합니다. **비활성화** 된 상태의 도메인 이름은 배포할 수 없습니다.
> + Tencent Cloud ** 오브젝트 스토리지 ** 또는 ** Cloud Infinite ** 서비스를 사용하여 CDN 가속을 활성화한 후의 `.file.myqcloud.com` 또는`.image.myqcloud.com` 도메인 이름은 인증서로 구성할 수 없습니다.

### 인증서 선택
자체 인증서 또는 Tencent Cloud 호스팅 인증서 위임을 사용하도록 선택할 수 있습니다.
#### 자체 인증서
[자체 인증서]를 선택하여 인증서 내용과 개인키 내용을 텍스트 상자에 붙여넣고 인증서에 주석을 추가하여 구별할 수 있습니다.
![인증서 선택](https://main.qcloudimg.com/raw/6ee06763e595b9739407d295194c0b61.png)

>+ 인증서 내용은 PEM 형식이어야 합니다. 기타 형식 인증서의 경우 다음 **PEM 형식 변환**을 참조하십시오.
> + 인증서에 인증서 체인이 있는 경우 인증서 체인의 내용을 PEM 형식으로 변환하고 인증서의 내용과 함께 업로드하십시오. 인증서 체인을 완료하려면 다음 **인증서 체인**을 참조하십시오.

#### Tencent Cloud 호스팅 인증서
[SSL 인증서 관리](https://console.cloud.tencent.com/ssl) 콘솔에 로그인하여 Trust Asia에서 무료로 제공한 타사 인증서를 신청하거나 기존 인증서를 Tencent Cloud에 호스팅 할 수 있습니다.
도메인 이름에 사용 가능한 인증서 목록을 보려면 [Tencent Cloud 호스팅 인증서 위임]을 선택하십시오. 인증서 리스트에서 사용할 인증서를 선택하면 인증서 형식이 "인증서 ID (비고)"로 표시됩니다.

### 원본 가져오기 방식
인증서를 구성한 후 CDN 노드가 원본 서버 리턴을 진행할 때 방법을 선택할 수 있습니다 CDN은 ** HTTP ** 및 ** 프로토콜 원본 가져오기 ** 두가지 방식의 원본 가져오기를 지원합니다.
![](https://main.qcloudimg.com/raw/719036689548a629283069a4a796156a.png)

>+ **HTTP**를 선택하여 원본 가져오기 구성 완료 후 CDN 노드 사용자는 HTTPS/HTTP 지원을 요청하고 CDN 노드 원본 서버 요청은 HTTP로 할 수 있습니다.
> + ** 프로토콜 따르기 ** 를 선택하여 원본 가져오기 구성으로 가면 사용자의 원본 서버는 유효한 인증서를 배포해야 하고 그렇지 않으면 원본 가져오기에 실패하게 됩니다. 구성 성공 후 사용자가 CDN 노드를 HTTP로 요청한 경우 CDN 노드 원본 가져오기 요청도 HTTP로 됩니다. 사용자가 CDN 노드 요청을 HTTPS로 한 경우 CDN 노드 원본 가져오기 요청도 HTTPS로 됩니다.
> + 도메인 이름 원본 서버를 HTTPS 포트를 443이 아닌 포트로 수정하면 구성이 실패합니다.
> + COS 원본 또는 FTP 원본 도메인 이름은 HTTP 원본 가져오기만 지원합니다.

#### 구성 성공
[제출]을 클릭하면 [인증서 관리] 페이지에서 성공적으로 구성된 도메인 이름 및 인증서 정보를 볼 수 있습니다.
![인증서 구성 성공 목록](https://main.qcloudimg.com/raw/1e3b016e129c9d3f5e311fb9440b2b70.png)

## 일괄 인증서 구성
만약 사용자가 여러 도메인 이름 인증서 또는 광범위 도메인 인증서가 있는 경우 여러 CDN 가속 도메인 이름에 적용할 수 있으며 일괄 구성을 통해 여러 도메인 이름 구성을 한 번에 추가할 수 있습니다.
1. [CDN 콘솔](https://console.cloud.tencent.com/cdn)에 로그인하고 왼쪽 메뉴의 [고급 도구]에서 [인증서 관리]를 클릭하여 관리 페이지로 진입합니다.
2. [일괄 구성]을 클릭하여 일괄 관리 페이지로 진입합니다.
![](https://main.qcloudimg.com/raw/03f34e25c7c2a877fc0dfb3d93b80ee2.png)

### 인증서 업로드
PEM으로 인코딩된 인증서 내용과 개인키를 페이지의 해당 텍스트 상자에 붙여 넣습니다. 노트 이름으로 구성된 인증서를 수정하여 구성을 완료하고 [다음]을 클릭할 수 있습니다.
![일괄](https://main.qcloudimg.com/raw/e01b281accc7f413ced65bc3061d23b5.png)

### 관련 도메인 이름과 원본 가져오기 방식 선택
CDN 시스템은 인증서를 업로드하는 데 사용할 수 있는 CDN 가속 도메인 이름(도메인 이름 상태는 **배포 중** 또는 **활성화 중**이어야 함)을 인식합니다. 연결하려는 도메인 이름을 확인하고 반환 방법을 선택할 수 있습니다.
>+ 한 번에 구성할 가속 도메인 이름을 최대 10 개까지 선택할 수 있습니다.
> + **HTTP**를 선택하여 원본 가져오기 구성 완료 후 CDN 노드 사용자는 HTTPS/HTTP 지원을 요청하고 CDN 노드 원본 서버 요청은 HTTP로 할 수 있습니다.
> + **HTTPS**원본 가져오기 구성을 선택합니다. 원본 서버는 유효한 인증서를 배포하지 않으면 원본 가져오기에 실패합니다. 구성 성공 후 사용자가 CDN 노드를 HTTP로 요청한 경우 CDN 노드 원본 가져오기도 HTTP로 됩니다. 사용자가 CDN 노드 요청을 HTTPS로 한 경우 CDN 노드 원본 가져오기 요청도 HTTPS로 됩니다.
> + 일괄 체크 선택의 도메인 이름 중 원본 서버 수정 HTTPS 포트가 443 포트가 아닐 경우 구성에 실패합니다.
> + 일괄 체크 선택의 도메인 이름 중 COS 원본 또는 FTP 원본의 도메인 이름이 있을 경우 HTTP 원본 가져오기만 지원합니다.

### 구성 제출
[제출]을 클릭하면 CDN이 선택한 도메인 이름에 대한 인증서를 구성합니다. 각 도메인 이름 구성에는 약 5분이 소요됩니다. 잠시만 기다려주십시오. [인증서 관리] 페이지에서 인증서 구성 상태를 볼 수 있습니다.

>+ 만약 구성에 실패하면 도메인 이름 오른쪽의 [편집] 버튼을 클릭하여 인증서를 다시 구성할 수 있습니다.
> 만약 대량 구성의 도메인 이름 중 이미 구성한 인증서의 도메인 이름이 존재하면 원래 인증서를 덮어 쓰고 덮어 쓰기에 실패하면 도메인 이름의 인증서 상태가 [업데이트 실패]로 변경됩니다. 이 때 원래 구성된 인증서는 여전히 유효합니다. 도메인 이름의 오른쪽의 [편집] 버튼을 클릭하여 덮어쓰기할 수 있습니다.

## 인증서 편집
성공적으로 구성된 인증서의 경우 도메인 이름 오른쪽의 [편집] 버튼을 클릭하여 인증서를 업데이트 할 수 있습니다.
![인증서 편집](https://main.qcloudimg.com/raw/0c5d408ac629a39135ed784eb6749bbe.png)
자체 인증서와 Tencent Cloud 호스팅 인증서를 전환할 수 있으며 원본 가져오기 방식을 다시 선택할 수 있습니다. [제출]을 클릭하여 배포를 완료하십시오. 배포 프로세스는 덮어쓰기 되지 않으며 비즈니스 사용에 영향을 미치지 않습니다.

## 인증서 삭제
도메인 이름 오른쪽의 [삭제] 버튼을 클릭하여 CDN에서 배포된 인증서를 삭제할 수 있습니다.
![인증서 삭제](https://main.qcloudimg.com/raw/49df665ca44fb4858f312e050d32b6eb.png)

## 인증서 체인 완성
자체 인증서 구성을 사용하는 과정에서 아래 그림과 같이 **인증서 체인을 완성 불가**의 상황이 발생할 수 있습니다.
CA 인증서(PEM 형식) 내용을 도메인 이름 인증서(PEM 형식) 끝에 게시하여 인증서 체인을 완성할 수 있습니다. 티켓을 제출하여 담당자에게 연락할 수도 있습니다.
![](https://main.qcloudimg.com/raw/c5adc7371454ec06a7f2f8150ec48ed8/cer11.png)

## PEM 형식 변환
현재 CDN은 PEM 형식의 인증서만 지원하기 때문에 기타 형식의 인증서는 openssl 도구를 통해 PEM 형식으로 변환하는 것을 권장합니다. 다음은 인증서 형식을 PEM 형식으로 변환하는 일반적인 방법 중 일부입니다.

### DER형식을 PEM 형식으로 변환
DER 형식은 일반적으로 Java 플랫폼에 나타납니다.
인증서 변환:
```
openssl x509 -inform der -in certificate.cer -out certificate.pem
```
개인키 변환:
```
openssl rsa -inform DER -outform PEM -in privatekey.der -out privatekey.pem
```

### P7B 형식을 PEM 형식으로 변환
P7B 형식은 일반적으로 Windows Server와 Tomcat에 나타납니다.
인증서 변환:
```
openssl pkcs7 -print_certs -in incertificat.p7b -out outcertificate.cer
```
텍스트 편집기로 outcertificat.cer을 열어 인증서의 내용을 PEM 형식으로 봅니다.
개인키 변환: 개인키는 일반적으로 IIS 서버에서 내보낼 수 있습니다.

### PFX 형식을 PEM 형식으로 변환
PFX 형식은 일반적으로 Windows Server에 나타납니다.
인증서 변환:
```
openssl pkcs12 -in certname.pfx -nokeys -out cert.pem
```
개인키 변환:
```
openssl pkcs12 -in certname.pfx -nocerts -out key.pem -nodes
```
