O Secure Sockets Layer (SSL) é um protocolo de segurança projetado para garantir a segurança e a integridade de dados para comunicações via Internet. Este documento apresenta a autenticação SSL unilateral e a autenticação mútua.
>?Ao criar um listener TCP SSL ou um listener HTTPS para uma instância do CLB, é possível selecionar a autenticação unilateral ou a autenticação mútua como o método de análise do SSL. Para obter mais informações, consulte [Configuração do listener TCP SSL](https://intl.cloud.tencent.com/document/product/214/32519) e [Configuração de um listener HTTPS](https://intl.cloud.tencent.com/document/product/214/32516).

## Diferenças entre autenticação SSL unilateral e autenticação mútua
-Para [autenticação SSL unilateral](#dxrz), os certificados são necessários apenas no servidor, mas não no cliente; enquanto para [autenticação mútua SSL](#sxrz), os certificados são necessários no servidor e no cliente.
- Em comparação com a autenticação mútua SSL, a autenticação unilateral não envolve a verificação do certificado do cliente e a negociação do esquema de criptografia no servidor. Embora o esquema de criptografia do servidor enviado ao cliente não seja criptografado, a segurança da autenticação SSL não é comprometida.
- Os aplicativos da web geralmente têm um grande número de usuários e a verificação da identidade do usuário não é necessária na camada de comunicação, caso em que a autenticação SSL unidirecional pode ser usada. No entanto, a verificação de identidade pode ser necessária para clientes que se conectam a aplicativos financeiros e, neste caso, a autenticação mútua SSL deve ser usada.

<span id="dxrz"></span>
## Autenticação SSL unilateral
Na autenticação SSL unilateral, apenas a identidade do servidor precisa ser verificada. Não é necessário verificar a identidade do cliente. O processo de autenticação SSL unilateral é mostrado abaixo:
<img src="https://main.qcloudimg.com/raw/000d0a44b1bad4b015cfc81ad6e17441.png" width="70%">
1. Um cliente inicia uma solicitação de conexão HTTPS para o servidor junto com as versões de protocolo SSL suportadas, algoritmos de criptografia, números aleatórios gerados e outras informações.
2. O servidor retorna uma versão do protocolo SSL, algoritmo de criptografia, número aleatório gerado, certificado do servidor (server.crt) e outras informações para o cliente.
3. O cliente verifica a validade do certificado (server.crt) para os fatores abaixo e obtém, do certificado, a chave pública do servidor.
  - Se o certificado expirou.
  - Se o certificado foi revogado.
  - Se o certificado é confiável.
  - Se o nome de domínio solicitado é igual ao nome de domínio no certificado recebido.
4. Após o certificado ser verificado, o cliente irá gerar um número aleatório (a chave K; que é usada como a chave de criptografia simétrica para a comunicação), criptografá-lo com a chave pública obtida do certificado do servidor e, em seguida, enviá-lo ao servidor .
5. Após receber as informações criptografadas, o servidor usará sua chave privada (server.key) para efetuar a descriptografia e obter a chave de criptografia simétrica (a chave K).
A chave de criptografia simétrica (a chave K) será usada pelo servidor e pelo cliente para comunicação, garantindo a segurança da informação.

<span id="sxrz"></span>
## Autenticação SSL mútua
Na autenticação SSL mútua, a identidade do servidor e a identidade do cliente precisam ser verificadas. O processo de autenticação SSL mútua é mostrado abaixo:
<img src="https://main.qcloudimg.com/raw/93c4567863719926db8737aa345e008c.png" width="70%">
1. Um cliente inicia uma solicitação de conexão HTTPS para o servidor junto com as versões de protocolo SSL suportadas, algoritmos de criptografia, números aleatórios gerados e outras informações.
2. O servidor retorna uma versão do protocolo SSL, algoritmo de criptografia, número aleatório gerado, certificado do servidor (server.crt) e outras informações para o cliente.
3. O cliente verifica a validade do certificado (server.crt) para os fatores abaixo e obtém, do certificado, a chave pública do servidor.
  - Se o certificado expirou.
  - Se o certificado foi revogado.
  - Se o certificado é confiável.
  - Se o nome de domínio solicitado é igual ao nome de domínio no certificado recebido.
4. O servidor solicita que o cliente envie o certificado do cliente (client.crt) e o cliente o faz.
5. O servidor verifica o certificado do cliente (client.crt). Depois de verificado, o servidor usará o certificado raiz para descriptografar o certificado do cliente e obter a chave pública do cliente.
6. O cliente envia os esquemas de criptografia simétrica compatíveis para o servidor.
7. O servidor seleciona o esquema de criptografia com o nível de criptografia mais alto dentre os esquemas enviados do cliente, usa a chave pública do cliente para criptografá-lo e o retorna ao cliente.
8. O cliente usa sua chave privada (client.key) para descriptografar o esquema de criptografia e gerar um número aleatório (a chave K; que é usada como chave de criptografia simétrica para a comunicação), criptografa-o com a chave pública obtida do certificado do servidor e, em seguida, o envia ao servidor.
9. Após receber as informações criptografadas, o servidor usará sua chave privada (server.key) para efetuar a descriptografia e obter a chave de criptografia simétrica (a chave K).
A chave de criptografia simétrica (a chave K) será usada pelo servidor e pelo cliente para comunicação, garantindo a segurança da informação.

## Documento relevante
[Requisitos de certificado e conversão de formato de certificado](https://intl.cloud.tencent.com/document/product/214/6155)
