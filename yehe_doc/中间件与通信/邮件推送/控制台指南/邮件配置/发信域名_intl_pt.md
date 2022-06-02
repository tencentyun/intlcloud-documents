## Visão geral
Você pode configurar domínios de remetente no console do SES. Este documento descreve como criar um domínio de remetente.

## Pré-requisitos
- Você deve ter permissões de administrador para domínio de remetente.
- Se o seu domínio estiver hospedado na Tencent Cloud, faça login no [console do DNSPod](https://console.cloud.tencent.com/cns) para configuração. Se o seu domínio estiver hospedado em outro provedor de serviços de domínio, configure-o de acordo com a lista de verificação.

## Instruções
1. Faça login no [console do SES](https://console.cloud.tencent.com/ses/domain), clique em **Configuration (Configuração)** > **Sender Domain (Domínio de remetente)** para acessar a página **Sender Domain (Domínio de remetente)** e clique em **Create (Criar)**.
![](https://main.qcloudimg.com/raw/7e4ba21b39ef0d2eb1de2e7ad8d8147a.png)

| Campo | Descrição |
|---------|---------|
| Domínio de remetente | Domínio de remetente configurado |
| Status |<li>**Pending verification (Verificação pendente)**: o domínio deve ser aprovado na verificação antes de poder ser usado para enviar e-mails. </li><br><li>**Verified (Verificado)**: o domínio foi verificado e pode ser usado para enviar e-mails.</li> |
| Operação | Se o status for **Pending verification (Verificação pendente)**, clique em **Verify (Verificar)** para verificar o domínio ou clique em **Delete (Excluir)** para excluí-lo. |

2. Na caixa de diálogo **Create Sender Domain (Criar domínio de remetente)**, insira um domínio e clique em **Submit (Enviar)** para concluir a configuração.
![](https://main.qcloudimg.com/raw/c2c75b71aaaf762f545ad530c6554aeb.png)
>? Para evitar conflitos entre registros SPF e MX, não use domínios de e-mail corporativos.
