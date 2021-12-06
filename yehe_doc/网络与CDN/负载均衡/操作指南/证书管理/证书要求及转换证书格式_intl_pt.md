Este documento apresenta os requisitos dos certificados SSL e descreve como converter formatos de certificado.

## Processo de solicitação de certificado
1. Use o OpenSSL para gerar um arquivo de chave privada localmente, ou seja, `privateKey.pem`. Mantenha-o privado.
```
openssl genrsa -out privateKey.pem 2048
```
2. Use o OpenSSL para gerar um arquivo de solicitação de certificado, ou seja, `server.csr`. Ele pode ser usado para a solicitação de certificado.
```
openssl req -new -key privateKey.pem -out server.csr
```
3. Obtenha o conteúdo do arquivo de solicitação de certificado e visite os sites da AC para solicitar um certificado.

## Requisitos de formato de certificado
- O certificado a ser solicitado deve estar no formato PEM no Linux. O CLB não é compatível com certificados em outros formatos. Para obter mais informações, consulte [Converter certificados para o formato PEM](#PEM).
- Se o seu certificado for emitido por uma AC raiz, o certificado é exclusivo e o site configurado será considerado confiável pelos navegadores e outros dispositivos de acesso sem a necessidade de certificados adicionais.
- Se o seu certificado for emitido por uma AC intermediária, o arquivo de certificado consistirá em vários certificados. Nesse caso, você precisa combinar manualmente o certificado do servidor e o certificado intermediário para upload.
- Se o seu certificado tiver uma cadeia de certificados, converta-o para o formato PEM e mescle com o conteúdo do certificado para upload.
- A regra de concatenação é a seguinte: coloque o certificado do servidor antes do certificado intermediário, sem linhas em branco entre eles.
>?Você pode verificar as regras de solicitação ou instruções fornecidas pela AC ao emitir o certificado.

**Formato do certificado e formato da cadeia de certificados**
Seguem abaixo exemplos de certificados e formatos de cadeia de certificados. Confirme o formato antes de fazer o upload:
1. Certificado emitido por uma AC raiz: Formato PEM no Linux, conforme mostrado abaixo:
![](https://main.qcloudimg.com/raw/cdea186a04d6f84e08fb38b19540189c.jpg)
As regras de certificado são:
 - Seu certificado deve começar com "——- BEGIN CERTIFICATE ——-" e terminar com "——- END CERTIFICATE ——-", estes devem ser carregados juntos.
 - Cada linha deve conter 64 caracteres, enquanto a última linha pode conter menos de 64 caracteres.
2. Cadeia de certificados de uma AC intermediária:
——-BEGIN CERTIFICATE——-
——-END CERTIFICATE——-
——-BEGIN CERTIFICATE——-
——-END CERTIFICATE——-
——-BEGIN CERTIFICATE——-
——-END CERTIFICATE——-

 Regras da cadeia de certificados:
 - Sem linhas em branco entre os certificados.
 - Todos os certificados devem atender aos requisitos acima.

## Requisitos de formato de chave privada RSA
Segue abaixo um exemplo:
![](https://main.qcloudimg.com/raw/bb9f866becc38dd28b8e62c53c1e551a.jpg)
A chave privada RSA pode incluir todas as chaves privadas (RSA e DSA), chaves públicas (RSA e DSA) e certificados (X.509). Ela armazena dados no formato DER codificado em Base64 e é agrupada por cabeçalhos ASCII, tornando-a adequada para transmissão em modo de texto entre sistemas.

Regras de chave privada RSA:
- Seu certificado deve começar com "——-BEGIN RSA PRIVATE KEY——-" e terminar com "——-END RSA PRIVATE KEY——-", estes devem ser carregados juntos.
- Cada linha deve conter 64 caracteres, enquanto a última linha pode conter menos de 64 caracteres.

Se sua chave privada não começar com "——-BEGIN PRIVATE KEY——-" e terminar com"——-END PRIVATE KEY——-", você pode convertê-la da seguinte maneira:
```
openssl rsa -in old_server_key.pem -out new_server_key.pem
```
Em seguida, será possível fazer o upload do conteúdo `new_server_key.pem` junto com o certificado.

## [](id:PEM)Conversão de certificados para o formato PEM
Atualmente, o CLB aceita apenas certificados no formato PEM. Os certificados em outros formatos precisam ser convertidos para o formato PEM antes de serem carregados por upload no CLB. Recomendamos que você use o OpenSSL. Veja a seguir como converter vários formatos comuns em PEM.
<dx-tabs>
::: DER\sto\sPEM\s
O formato DER costuma ser usado em plataformas Java.
Conversão do certificado:
```
openssl x509 -inform der -in certificate.cer -out certificate.pem
```
Conversão da chave privada:
```
openssl rsa -inform DER -outform PEM -in privatekey.der -out privatekey.pem
```
:::
::: P7B\sto\sPEM\s
O formato P7B costuma ser usado no Windows Server e no Tomcat.
Conversão do certificado:
```
openssl pkcs7 -print_certs -in incertificat.p7b -out outcertificate.cer
```
Você precisa inserir o conteúdo entre "——-BEGIN CERTIFICATE——-" e "——-END CERTIFICATE——-" em `outcertificat.cer` para fazer o upload como certificado.
Conversão de chave privada: em geral, as chaves privadas podem ser exportadas em servidores IIS.
:::
::: PFX\sto\sPEM\s
O formato PFX costuma ser usado no Windows Server.
Conversão do certificado:
```
openssl pkcs12 -in certname.pfx -nokeys -out cert.pem
```
Conversão da chave privada:
```
openssl pkcs12 -in certname.pfx -nocerts -out key.pem -nodes
```	
:::
::: CER/ CRT\sto\sPEM\s
É possível converter certificados em formatos CER/CRT para PEM, modificando diretamente seus nomes de extensão de arquivo. Por exemplo, é possível renomear diretamente o arquivo de certificado `servertest.crt` como `servertest.pem`.
:::
</dx-tabs>








