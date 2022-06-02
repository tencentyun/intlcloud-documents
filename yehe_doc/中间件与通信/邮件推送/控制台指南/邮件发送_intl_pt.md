## Visão geral
Você pode configurar o envio de e-mail no console do SES. Este documento descreve como enviar um e-mail.

## Instruções
### Envio de e-mail
1. Faça login no [console do SES](https://console.cloud.tencent.com/ses/send) e clique em **Email Sending (Envio de e-mail)** para acessar a página **Email Sending (Envio de e-mail)**.
![](https://main.qcloudimg.com/raw/3797c2f860e240f4e4864728aa09c80a.png)
2. Selecione um modelo de e-mail, insira um assunto, selecione um endereço de remetente, insira endereços de destinatários e clique em **Send (Enviar)** para enviar o e-mail.
>? Esta página é apenas para testar o envio de e-mail. São permitidos até 20 endereços de destinatários para um único teste.

### Envio em lote
1. No console, a lista de tarefas de envio é exibida na página **Email Sending (Envio de e-mail)** > **Batch (Em lote)**. A lista de tarefas de envio exibe as informações detalhadas de cada tarefa de envio, incluindo **Sending Progress (Progresso de envio)**, **Task Type (Tipo de tarefa)**, **Task Status (Status da tarefa)** e **Requests (Solicitações)**.
![](https://qcloudimg.tencent-cloud.cn/raw/03e8a8f74f5d0ab785bb016427712502.png)
2. Clique em **Create Sending Task (Criar tarefa de envio)**, selecione **Batch (Em lote)** para **Task Type (Tipo de tarefa)** e defina todos os campos obrigatórios para a tarefa enviar e-mails em lotes.
![](https://qcloudimg.tencent-cloud.cn/raw/bd85315b7f512173a687f6c0ea4f706c.png)

### Envio agendado
1. No console, acesse a página **Email Sending (Envio de e-mail)** > **Batch (Em lote)**, clique em **Create Sending Task (Criar tarefa de envio)** e selecione **Scheduled (Agendado)**.
![](https://qcloudimg.tencent-cloud.cn/raw/7e4f2dcdca1e2f11ba55e7d03861489e.png)
2. Selecione **Start Time (Hora de início)** para a tarefa e os e-mails serão enviados automaticamente no horário especificado.
![](https://qcloudimg.tencent-cloud.cn/raw/55482b11771bbe336023ca840d346234.png)


### Envio recorrente
1. No console, acesse a página **Email Sending (Envio de e-mail)** > **Batch (Em lote)**, clique em **Create Sending Task (Criar tarefa de envio)** e selecione **Recurring (Recorrente)**.
![](https://qcloudimg.tencent-cloud.cn/raw/972566ee846e6629d9518f67686cec99.png)
2. Defina os campos da tarefa, incluindo **Start Time (Hora de início)** e **Recurrence (Frequência)**. O console enviará os e-mails automaticamente com base na frequência especificada.
![](https://qcloudimg.tencent-cloud.cn/raw/e5ca62b26bbbfc467855d04d4e9c088e.png)

>?
>
>- A funcionalidade **Batch (Em lote)** no console é adequada para o envio em lote de e-mails de marketing ou de notificação. Para enviar e-mails baseados em gatilho (como e-mails transacionais e de autenticação), é recomendável chamar a API `SendEmail`.
>- O warm-up automático é integrado à funcionalidade de envio em lote para determinar de forma inteligente a reputação do domínio/IP do remetente e a quantidade máxima permitida de e-mails enviados por dia. Quando esse limite diário for atingido, o envio de e-mails será interrompido e os demais e-mails entrarão na fila de cache e serão enviados 24 horas depois. Consulte o limite diário de e-mail de um domínio/IP para o qual não foi realizado o warm-up em [Plano de warm-up padrão](https://intl.cloud.tencent.com/document/product/1084/43285#default).
>- Você pode usar um único domínio para várias tarefas de envio. Quando o volume total de e-mails exceder a quantidade máxima permitida por dia, os demais e-mails entrarão na fila de cache e serão enviados no dia seguinte.
>- Quando uma tarefa entra na fila de cache, seu status é **Paused (Pausado)** e a barra de progresso de envio permanece estática. Depois de reiniciar a tarefa no dia seguinte, o status passa para **Sending (Enviando)** e a barra de progresso aumenta.
