## Visão geral das configurações

O CDN do Tencent Cloud aceita o redirecionamento forçado de HTTPS/HTTP.

- Se um nome de domínio for configurado com um certificado para a aceleração HTTPS, é possível especificar o método de redirecionamento 301/302 para forçar todas as solicitações HTTP no nó do CDN a serem solicitações HTTPS.
- Também é possível especificar o método de redirecionamento 301/302 para forçar todas as solicitações HTTPS no nó do CDN a serem solicitações HTTP.

## Guia de configuração

### Limitações de configuração

A aceleração HTTPS deve ser ativada para configurar o redirecionamento forçado de HTTPS.

### Instruções de configuração

Faça login no [console do CDN](https://console.cloud.tencent.com/cdn), selecione **Domain Management (Gerenciamento de domínio)** na barra lateral esquerda, clique em **Manage (Gerenciar)** à direita de um nome de domínio para acessar sua página de configuração. Abra a guia ***HTTPS Configuration (Configuração do HTTPS)** para localizar a seção **Forced Redirection (Redirecionamento forçado)**. A funcionalidade fica desativada por padrão.
<img src="https://main.qcloudimg.com/raw/b11157d848d39d4e4bba540598f35eba.png" style="width:700px"/>
Ative o botão e configure o tipo e o método de redirecionamento:
<img src="https://main.qcloudimg.com/raw/731d7bcb51286683d259691178bf2b39.png" style="width:450px"/>
Por fim, clique em **Confirm (Confirmar)** para implantar a configuração:
<img src="https://main.qcloudimg.com/raw/2dcfbacf16b47fe600935f57aadd2e77.png" style="width:700px"/>

