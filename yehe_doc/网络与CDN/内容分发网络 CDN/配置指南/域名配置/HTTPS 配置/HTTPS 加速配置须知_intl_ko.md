사용자의 도메인에 기존 인증서를 설정하려면 먼저 아래 내용을 알아 두어야 합니다. 사용자가 Tencent Cloud SSL 인증서 관리에 있는 인증서대로 설정하였다면 이 단계를 건너뛸 수 있습니다.
## 인증서 업로드
인증 기관(CA)에서 제공한 인증서는 일반적으로 다음과 같은 몇 가지 종류가 있습니다. 그중 CDN이 사용하는 것은 **Nginx** 입니다:
![](https://main.qcloudimg.com/raw/249538db51d90314f84b2c75a6bccc05.png)
Nginx 폴더로 이동하여 텍스트 편집기에서 ".crt"(인증서) 파일과 ".key"(프라이빗 키) 파일을 열면 PEM 형식으로 된 인증서 내용과 프라이빗 키 내용을 확인할 수 있습니다
![](https://main.qcloudimg.com/raw/2a1b11ff93a7cb475d68e38c7701434f/Nginx_certificate.png)

### 인증서
인증서 확장명은 일반적으로 ".pem", ".crt" 또는 ".cer"입니다. 텍스트 편집기에서 인증서 파일을 열면 아래 형식과 비슷한 인증서의 내용을 확인할 수 있습니다.
인증서 PEM 형식: "-----BEGIN CERTIFICATE-----"으로 시작하고, "-----END CERTIFICATE-----"로 끝납니다. 중간은 한 줄에 64자여야 하고 마지막 줄은 64글자 미만이여도 괜찮습니다.
![img](https://main.qcloudimg.com/raw/60ea02d1a2c9623526d7fa79403e658a.jpg)
만약 중급 인증 기관(CA)에서 인증서를 발급 받은 경우 인증서 파일에 여러 개의 인증서가 포함되어 있으므로 서버 인증서와 중간 인증서를 스티칭하여 업로드해야 합니다. 스티칭 규칙은 서버 인증서를 첫 번째에, 중간 인증서를 두 번째에 두고 중간 인증서에는 중간에 빈 줄이 없어야 합니다. 일반적인 상황에서는 기관에서 인증서를 발급할 때 해당 설명이 표시되므로 규칙 설명에 유의하시기 바랍니다.

>
> + 인증서 사이에 빈 줄이 없어야 합니다
> + 각 인증서는 PEM 형식이어야 합니다.

중급 기관에서 발급한 인증서 체인 형식은 다음과 같습니다.
```
-----BEGIN CERTIFICATE-----
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
-----END CERTIFICATE-----
```

### 프라이빗 키
프라이빗 키 확장명은 일반적으로 ".pem" 또는 ".key"입니다. 텍스트 편집기에서 프라이빗 키 파일을 열면 아래 이미지 형식과 유사한 프라이빗 키 내용을 확인할 수 있습니다.
프라이빗 키 PEM 형식: "-----BEGIN RSA PRIVATE KEY-----"로 시작하고 "-----END RSA PRIVATE KEY-----"로 끝납니다. 중간은 한 줄에 64자여야 하고 마지막 줄은 64글자 미만이여도 괜찮습니다.
![img](https://main.qcloudimg.com/raw/e10009916aeb00d5158a3703115d0354.jpg)
“-----BEGIN PRIVATE KEY-----”로 시작하고, “-----END PRIVATE KEY-----”로 끝나는 프라이빗 키를 획득한 경우 openssl 툴을 통해 다음과 같은 명령어로 형식을 변환해주시기 바랍니다.
```
openssl rsa -in old_server_key.pem -out new_server_key.pem
```

### 형식 변환
현재 CDN은 PEM 형식의 인증서만 지원하기 때문에 기타 형식의 인증서는 openssl 툴을 통해 PEM 형식으로 변환할 것을 권장합니다. 다음은 인증서 형식을 PEM 형식으로 변환 시 흔히 사용하는 방법들입니다.
#### DER 형식을 PEM 형식으로 변환
DER 형식은 일반적으로 Java 플랫폼에서 사용됩니다.
인증서 변환:
```
openssl x509 -inform der -in certificate.cer -out certificate.pem
```
프라이빗 키 변환:
```
openssl rsa -inform DER -outform PEM -in privatekey.der -out privatekey.pem
```
#### P7B 형식을 PEM 형식으로 변환
P7B 형식은 일반적으로 Windows Server와 tomcat에서 사용됩니다.
인증서 변환:
```
openssl pkcs7 -print_certs -in incertificat.p7b -out outcertificate.cer
```
텍스트 편집기로 outcertificat.cer을 열면 PEM 형식으로 된 인증서를 조회할 수 있습니다.
프라이빗 키 변환: 프라이빗 키는 일반적으로 IIS 서버에서 내보낼 수 있습니다.
#### PFX 형식을 PEM 형식으로 변환
PFX 형식은 일반적으로 Windows Server에서 사용됩니다.
인증서 변환:
```
openssl pkcs12 -in certname.pfx -nokeys -out cert.pem
```
프라이빗 키 변환:
```
openssl pkcs12 -in certname.pfx -nocerts -out key.pem -nodes
```
### 인증서 체인 완성
자체 인증서 설정을 사용하는 과정에서 아래 이미지와 같이 **인증서 체인을 완성할 수 없음**의 상황이 발생할 수 있습니다.
![img](https://main.qcloudimg.com/raw/ed45f581114cc456a710b7d4997076a2.png)
CA 인증서(PEM 형식)를 도메인 이름 인증서(PEM 형식)의 끝부분에 붙여넣어 인증서 체인을 완성할 수 있습니다. 혹은 티켓 제출을 통해 문의하세요.
![img](https://main.qcloudimg.com/raw/c5adc7371454ec06a7f2f8150ec48ed8/cer11.png)

## 호스팅 인증서

Tencent Cloud는 인증서 호스팅 제품인 [SSL 인증서](http://console.cloud.tencent.com/ssl)를 제공합니다. 기존 인증서를 SSL 인증서 관리 플랫폼에 업로드하여 통합 호스팅하고, 기타 클라우드 서비스에 배포할 수 있으며 인증서 구매 및 신청도 가능합니다.

Tencent Cloud SSL 인증서는 각 사용자에게 TrustaAsia에서 발급한 DV SSL 인증서 20부를 무료로 제공해 드립니다.
