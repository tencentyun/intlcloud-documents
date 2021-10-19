Se você precisar configurar um certificado existente para o seu nome de domínio, consulte as opções a seguir. Se o certificado que você configurar for do SSL Certificates Service do Tencent Cloud, pode pular esta etapa.
## Upload de certificado
Em geral, as autoridades certificadoras (AC) fornecem os seguintes tipos de certificados, e o **Nginx** é usado pelo CDN.
Entre na pasta do Nginx, use um editor de texto para abrir os arquivos ".crt" (certificado) e ".key" (chave privada) e visualize o conteúdo do certificado e da chave privada no formato PEM.

### Certificado
As extensões de certificados comuns incluem ".pem", ".crt" e ".cer". Abra o arquivo do certificado em um editor de texto e tenha acesso ao conteúdo conforme mostrado abaixo.
Um certificado ".pem" começa com "-----BEGIN CERTIFICATE-----" e termina com "-----END CERTIFICATE-----". Cada linha intermediária contém 64 caracteres, já a última linha pode ter menos de 64 caracteres:
![img](https://main.qcloudimg.com/raw/60ea02d1a2c9623526d7fa79403e658a.jpg)
Se o seu certificado for emitido por uma AC intermediária, o arquivo de certificado consistirá em vários certificados. Nesse caso, é necessário unir manualmente os certificados do servidor e os certificados intermediários para upload, colocando o conteúdo do certificado do servidor antes do conteúdo do certificado intermediário, sem linhas em branco entre eles. Consulte as regras ou instruções que acompanham o certificado.

>
> + Não deve haver linhas em branco entre os certificados
> + Todos os certificados estão no formato PEM

Uma cadeia de certificados de uma AC intermediária segue esse formato:
```
-----BEGIN CERTIFICATE-----
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
-----END CERTIFICATE-----
```

### Chave privada
As extensões de chave privada comuns incluem ".pem" e ".key". Abra o arquivo de chave privada em um editor de texto e tenha acesso ao conteúdo conforme mostrado abaixo.
Uma chave privada ".pem" começa com "-----BEGIN RSA PRIVATE KEY-----" e termina com "-----END RSA PRIVATE KEY-----". Cada linha intermediária contém 64 caracteres, já a última linha pode ter menos de 64 caracteres.
![img](https://main.qcloudimg.com/raw/e10009916aeb00d5158a3703115d0354.jpg)
Se sua chave privada começa com "-----BEGIN PRIVATE KEY-----" e termina com "-----END PRIVATE KEY-----", recomendamos que você converta o formato usando o OpenSSL com o seguinte comando:
```
openssl rsa -in old_server_key.pem -out new_server_key.pem
```

### Conversão de outros formatos para PEM
Atualmente, o CDN aceita apenas certificados no formato PEM. Os certificados em outros formatos precisam ser convertidos para o formato PEM. Recomendamos que você use o OpenSSL. A seguir, veja como converter alguns formatos comuns em PEM.
#### DER para PEM
O formato DER costuma ser usado em plataformas Java.
Conversão do certificado:
```
openssl x509 -inform der -in certificate.cer -out certificate.pem
```
Conversão da chave privada:
```
openssl rsa -inform DER -outform PEM -in privatekey.der -out privatekey.pem
```
#### P7B para PEM
O formato P7B costuma ser usado no Windows Server e no Tomcat.
Conversão do certificado:
```
openssl pkcs7 -print_certs -in incertificat.p7b -out outcertificate.cer
```
Abra o outcertificat.cer com um editor de texto para visualizar o conteúdo do certificado PEM.
Conversão de chave privada: em geral, as chaves privadas podem ser exportadas em servidores IIS.
#### PFX para PEM
O formato PFX costuma ser usado no Windows Server.
Conversão do certificado:
```
openssl pkcs12 -in certname.pfx -nokeys -out cert.pem
```
Conversão da chave privada:
```
openssl pkcs12 -in certname.pfx -nocerts -out key.pem -nodes
```
### Conclusão da cadeia de certificados
Ao configurar um certificado privado, você pode encontrar um problema de que a **certificate chain cannot be completed (cadeia de certificados não pode ser concluída)**, conforme mostrado abaixo.

Nesse caso, você pode colar o conteúdo do certificado (no formato PEM) emitido pela AC após o certificado do nome de domínio (no formato PEM) para concluir a cadeia de certificados. Você também pode enviar um tíquete para obter assistência.

## Certificado hospedado

O Tencent Cloud oferece um serviço de hospedagem de certificados: [SSL Certificates Service](http://console.cloud.tencent.com/ssl). Você pode fazer upload de certificados existentes para o console do SSL Certificates Service, para hospedagem e implantação unificadas em outros produtos do Tencent Cloud. Ele também permite que você compre e solicite certificados.

O SSL Certificates Service fornece 20 certificados SSL DV emitidos pela TrustAsia gratuitamente.
