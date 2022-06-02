## Ativação da funcionalidade de envio por SMTP
## Instruções
### Etapa 1. Acessar a página de endereços de remetente
Faça login no [console do SES](https://console.cloud.tencent.com/ses) e clique em **Configuration (Configuração)** > **Sender Address (Endereço de remetente)** na barra lateral esquerda para acessar a página de endereços de remetente.
![](https://qcloudimg.tencent-cloud.cn/raw/fa124df0a9c52d8712e203e25866a389.png)

### Etapa 2. Configurar a senha do SMTP
1. Na lista de endereços de remetente, localize aquele para o qual você deseja habilitar o envio por SMTP e clique em **Set SMTP Password (Definir senha do SMTP)** na coluna **Operation (Operação)**.
2. Digite a senha do SMTP na janela pop-up e clique em **OK**.



## Envio de e-mail pela API do SMTP
Confira o código de exemplo do SMTP e os parâmetros de solicitação específicos, os parâmetros de resposta e os códigos de erro em [Chamada de exemplo do SMTP](https://intl.cloud.tencent.com/document/product/1084/44456).
>?Os e-mails com anexos podem ser enviados conforme as instruções em [Envio de e-mail com anexo por SMTP](https://intl.cloud.tencent.com/document/product/1084/44454).

## Frequência de envio do SMTP
A taxa de chamadas atual da API do SMTP é limitada a 20 vezes por segundo na mesma conta da Tencent Cloud `appId`. Além disso, o mesmo remetente pode enviar até dez e-mails por hora para o mesmo destinatário.

Entregaremos os e-mails o mais rápido possível após o recebimento. No entanto, devido às diferentes políticas de limitação de tráfego e proteção de reputação de diferentes sistemas de e-mail, para melhorar sua taxa de sucesso de entrega de e-mail, recomendamos que você envie e-mails com uma frequência menor.


