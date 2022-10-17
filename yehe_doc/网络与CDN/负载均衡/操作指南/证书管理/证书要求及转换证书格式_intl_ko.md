본문은 SSL 인증서 요구 사항과 인증서 형식 변환 방법을 설명합니다.

## 인증서 신청 절차
1. OpenSSL을 사용하여 개인 키 파일(예: `privateKey.pem`)을 로컬로 생성합니다. 비공개로 유지하십시오.
```
openssl genrsa -out privateKey.pem 2048
```
2. OpenSSL을 사용하여 인증서 요청 파일(예: `server.csr`)을 생성합니다. 인증서 신청에 사용할 수 있습니다.
```
openssl req -new -key privateKey.pem -out server.csr
```
3. 인증서 요청 파일의 내용을 얻고 CA 사이트를 방문하여 인증서를 신청합니다.

## 인증서 형식 요구 사항
- 사용자가 신청해야 하는 인증서는 Linux에서 PEM 형식이어야 합니다. CLB는 다른 형식의 인증서를 지원하지 않습니다. 자세한 내용은 [인증서를 PEM 형식으로 변환](#PEM)을 참고하십시오.
- 인증서가 root 인증 기관(CA)에서 발급된 경우 인증서는 고유하며 구성된 웹 사이트는 추가 인증서가 필요하지 않은 브라우저 및 기타 액세스 장치에서 신뢰할 수 있는 것으로 간주됩니다.
- 인증서가 중급 인증 기관(CA)에서 발급된 경우 인증서 파일은 여러 인증서로 구성됩니다. 이 경우 업로드를 위해 서버 인증서와 중간 인증서를 수동으로 결합해야 합니다.
- 인증서에 인증서 체인이 있는 경우 이를 PEM 형식으로 변환하고 인증서 콘텐츠와 병합하여 업로드하십시오.
- 연결 규칙은 다음과 같습니다. 서버 인증서를 중간 인증서 앞에 빈 줄 없이 배치합니다.
>?인증서 발급 시 CA에서 제공하는 해당 규칙이나 지침을 확인할 수 있습니다.

**인증서 형식 및 인증서 체인 형식**
다음은 인증서 및 인증서 체인 형식의 예입니다. 업로드하기 전에 형식을 확인하십시오.
1. root CA에서 발급한 인증서: Linux의 PEM 형식은 아래와 같습니다.
![](https://main.qcloudimg.com/raw/cdea186a04d6f84e08fb38b19540189c.jpg)
인증서 규칙은 다음과 같습니다.
 - 인증서는 [——-BEGIN CERTIFICATE——-, ——-END CERTIFICATE——-] 시작과 끝을 함께 업로드해야 합니다.
 - 각 줄은 64자를 포함해야 하며 마지막 줄은 64자 미만이어야 합니다.
2. 중급 CA의 인증서 체인:
——-BEGIN CERTIFICATE——-
——-END CERTIFICATE——-
——-BEGIN CERTIFICATE——-
——-END CERTIFICATE——-
——-BEGIN CERTIFICATE——-
——-END CERTIFICATE——-

 인증서 체인 규칙:
 - 인증서 사이에 빈 줄이 없어야 합니다.
 - 모든 인증서는 위와 같은 요구 사항을 충족해야 합니다.

## RSA 개인 키 형식 요구 사항
다음은 예시입니다.
![](https://main.qcloudimg.com/raw/bb9f866becc38dd28b8e62c53c1e551a.jpg)
RSA 개인 키는 모든 개인 키(RSA 및 DSA), 공개 키(RSA 및 DSA) 및 (x509) 인증서를 포함할 수 있습니다. Base64로 인코딩된 DER 형식으로 데이터를 저장하고 ASCII 헤더로 래핑하여 시스템 간의 텍스트 모드 전송에 적합합니다.

RSA 개인 키 규칙:
- 인증서는 [——-BEGIN RSA PRIVATE KEY——-, ——-END RSA PRIVATE KEY——-] 시작과 끝을 함께 업로드해야 합니다.
- 각 줄은 64자를 포함해야 하며 마지막 줄은 64자 미만이어야 합니다.

위의 방식에 따라 [——-BEGIN PRIVATE KEY——-, ——-END PRIVATE KEY——-] 형식으로 사용 가능한 개인 키를 생성하지 않으면 다음과 같이 사용 가능한 개인 키로 변환할 수 있습니다.
```
openssl rsa -in old_server_key.pem -out new_server_key.pem
```
그런 다음 인증서와 함께 new_server_key.pem 콘텐츠를 업로드할 수 있습니다.

## [](id:PEM)인증서를 PEM 형식으로 변환
현재 CLB는 PEM 형식의 인증서만 지원합니다. 다른 형식의 인증서는 CLB에 업로드하기 전에 먼저 openssl을 사용하여 PEM 형식으로 변환해야 합니다. 다음은 몇 가지 일반적인 형식을 PEM 형식으로 변환하는 방법을 보여줍니다.
<dx-tabs>
::: DER\s에서 \sPEM\s으로 변환
DER 형식은 일반적으로 Java 플랫폼에서 사용됩니다.
인증서 변환:
```
openssl x509 -inform der -in certificate.cer -out certificate.pem
```
개인키 변환:
```
openssl rsa -inform DER -outform PEM -in privatekey.der -out privatekey.pem
```
:::
::: P7B\s에서 \sPEM\s으로 변환
P7B 형식은 일반적으로 Windows Server와 tomcat에서 사용됩니다.
인증서 변환:
```
openssl pkcs7 -print_certs -in incertificat.p7b -out outcertificate.cer
```
인증서로 업로드하려면 outcertificat.cer에서 [——-BEGIN CERTIFICATE——-, ——-END CERTIFICATE——-] 의 콘텐츠를 가져와야 합니다.
개인키 변환: 개인키는 일반적으로 IIS 서버에서 내보낼 수 있습니다.
:::
::: PFX\s에서 \sPEM\s으로 변환
PFX 형식은 일반적으로 Windows Server에서 사용됩니다.
인증서 변환:
```
openssl pkcs12 -in certname.pfx -nokeys -out cert.pem
```
개인키 변환:
```
openssl pkcs12 -in certname.pfx -nocerts -out key.pem -nodes
```	
:::
::: CER/CRT\s에서 \sPEM\s으로 변환
파일 확장자 이름을 직접 수정하여 CER/CRT 형식의 인증서를 PEM으로 변환할 수 있습니다. 예를 들어 ‘servertest.crt’ 인증서 파일의 이름을 ‘servertest.pem’으로 직접 바꿀 수 있습니다.
:::
</dx-tabs>








