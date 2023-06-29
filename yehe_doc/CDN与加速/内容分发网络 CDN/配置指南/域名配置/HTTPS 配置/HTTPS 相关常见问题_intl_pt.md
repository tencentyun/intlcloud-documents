[](id:q1)
### O que é o HTTPS?
O HTTPS significa Hypertext Transfer Protocol Secure, um protocolo de segurança que criptografa e transfere dados com base no protocolo HTTP para garantir a segurança da transferência dos dados. Ao configurar o HTTPS, é necessário fornecer um certificado para o nome de domínio e implantá-lo em todos os nós do CDN, com o intuito de implementar a transferência de dados criptografados em toda a rede.

[](id:q2)
### O CDN é compatível com a configuração do HTTPS?
Sim. O CDN do Tencent Cloud é totalmente compatível com a configuração do HTTPS. É possível carregar seu próprio certificado para implantação, ou acessar o [console do SSL Certificate Service](https://console.cloud.tencent.com/ssl) para solicitar um certificado gratuito de terceiros, fornecido pela TrustAsia.

[](id:q3)
### Como eu configuro um certificado HTTPS?
É possível configurar um certificado HTTPS no [console do CDN](https://console.cloud.tencent.com/cdn). Para ter acesso a instruções detalhadas, consulte [Guia de configuração do HTTPS](https://intl.cloud.tencent.com/document/product/228/35213).

[](id:q4)
### Os certificados HTTPS nos nós do CDN precisam ser sincronizados com as atualizações do certificado HTTPS no servidor de origem?
Não. Atualizar o certificado HTTPS do seu servidor de origem não afeta o certificado configurado no CDN. Basta atualizar o certificado HTTPS no CDN quando ele estiver expirado ou prestes a expirar.


[](id:q5)
### Posso negar o acesso HTTP e permitir apenas o acesso HTTPS?
Sim. Depois de configurar um certificado HTTPS, é possível usar a funcionalidade [Redirecionamento forçado](https://intl.cloud.tencent.com/document/product/228/35214). As solicitações HTTP de usuários serão redirecionadas à força para solicitações HTTPS.
![](https://main.qcloudimg.com/raw/c562127135d558445481ab97973b1ebe.png)


[](id:q6)
### Por que o acesso HTTPS não funciona depois que o CDN é configurado?

Para acesso HTTPS, configure-o conforme as instruções:
1. Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda e clique em **Manage (Gerenciar)** à direita de um nome de domínio para acessar sua página de gerenciamento.
![](https://main.qcloudimg.com/raw/33ea31c11bfac2022ea5753b6d849042.png)
2. Abra a guia **Advanced Configuration (Configuração avançada)** para localizar a seção **HTTPS Configuration (Configuração do HTTPS)**. Clique em **Configure Now (Configurar agora)** para acessar a página **Certificate Management (Gerenciamento de certificado)**. Para ter acesso às instruções sobre a configuração, consulte [Guia de configuração do HTTPS](https://intl.cloud.tencent.com/document/product/228/35213#.E8.AF.81.E4.B9.A6.E9.85.8D.E7.BD.AE).
![](https://main.qcloudimg.com/raw/67be1f3b42a411613c0500afa97e06b5.png)
O acesso HTTPS pode ser ativado após o certificado ser configurado.



