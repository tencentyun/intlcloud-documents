[](id:senderConfig)
## Opções de configuração do remetente
O Simple Email Service (SES) oferece três maneiras de enviar e-mails: console do SES, API do SES e SMTP do SES. Você pode usar a interface de linha de comando do SES (CLI do SES) ou o [SDK do SES para chamar APIs](https://intl.cloud.tencent.com/document/product/1084/39387) ou chamar APIs do SMTP para enviar e-mails.

Para enviar um e-mail, consulte o [**Guia do console** > **Envio de e-mail**](https://intl.cloud.tencent.com/document/product/1084/40178).
## Opções de implantação flexíveis
### Endereços IP compartilhados
No geral, o SES envia e-mails de endereços IP compartilhados no pool de IPs compartilhados, por padrão. Os endereços compartilhados são uma opção rápida e fácil de usar para os usuários que desejam começar a enviar, usando IPs estabelecidos, imediatamente. A Tencent Cloud ajuda a garantir a qualidade dos IPs compartilhados e uma alta taxa de entrega.
### Endereços IP dedicados
Um IP dedicado é um IP atribuído especialmente a você pela Tencent Cloud para enviar e-mails. No geral, ele nunca foi usado para envio de e-mail ou sempre teve uma boa reputação, o que garante que não será marcado como um IP de spam por organizações anti-spam. A depender do seu volume de envio, você pode solicitar um IP dedicado. Se você precisar enviar uma grande quantidade de e-mails, entre em contato com seu representante de vendas para solicitar um IP dedicado.


## Gerenciamento e segurança da identidade do remetente
Ao receber um e-mail, um provedor de serviços de internet (ISP) verificará se ele está autenticado antes de entregá-lo ao destinatário. A autenticação prova ao ISP que você é o proprietário do endereço de e-mail do qual está enviando. O SES aceita todos os mecanismos de autenticação padrão do setor, incluindo a Sender Policy Framework (SPF), o Domain Keys Identified Mail (DKIM) e a Domain-based Message Authentication. Ocorre, assim, a garantia de que seus e-mails passem pelas verificações do ISP e sejam entregues ao destinatário.
## Estatísticas de envio
O SES disponibiliza vários métodos para monitorar as atividades de envio de e-mail. Por exemplo, ele pode capturar as informações sobre todo o funil de resposta de e-mail (incluindo as quantidades de entregas, de aberturas, de cliques, de devoluções etc.) e fornecer uma análise de dados precisa. Além disso, você pode verificar o status de envio de um e-mail específico chamando [GetSendEmailStatus](https://intl.cloud.tencent.com/document/product/1084/39502) para ajudar a ajustar sua política de envio de e-mail.

[](id:warmUp)
## Warm-up automático 
### Funcionalidades
O processo de entrega de e-mail pode ser extremamente complicado. A reputação de um IP/domínio é vital para melhorar a capacidade de entrega. O warm-up é um processo de criação da sua reputação de envio. O volume de envio deve ser aumentado gradualmente dia após dia e não pode ser elevado ao nível desejado de uma só vez. Um bom warm-up ajuda a estabelecer uma boa reputação com seu ISP.
>? O warm-up automático significa efetuar, automaticamente, o warm-up de seus endereços IP ou domínios de remetente, sem intervenção manual durante todo o processo.
### Descrição
O warm-up automático é dividido em duas categorias: [Regras padrão (padrão)](#default) e [Regras atualizadas](#customize).

#### Regras padrão:
As regras de warm-up padrão se aplicam, por padrão, ao modo de envio em lote. O back-end determinará o progresso do warm-up com base em uma série de políticas e atribuirá automaticamente a cota diária de envio. Todo o processo é automático. Quando a quantidade máxima permitida de e-mails enviados por dia for atingida, o envio de e-mails será interrompido e os demais e-mails entrarão na fila de cache e serão enviados 24 horas depois. O plano de warm-up padrão é o seguinte: [](id:default)

<table style="width: 200px;">
   <tr>
      <th width="0px" style="text-align:center">Dia</td>
      <th width="0px" style="text-align:center">Volume de envio/dia</td>
   </tr>
	<tr>
		<td style="text-align:center"style="text-align:center">1</td>
		<td style="text-align:center">500</td>
	</tr>
	<tr>
		<td style="text-align:center">2</td>
		<td style="text-align:center"sdval="200" >1.000</td>
	</tr>
	<tr>
		<td style="text-align:center">3</td>
		<td style="text-align:center"sdval="500" >2.000</td>
	</tr>
	<tr>
		<td style="text-align:center">4</td>
		<td style="text-align:center"sdval="1000" >5.000</td>
	</tr>
	<tr>
		<td style="text-align:center">5</td>
		<td style="text-align:center"sdval="2000" >10.000</td>
	</tr>
	<tr>
		<td style="text-align:center">6</td>
		<td style="text-align:center"sdval="5000" >20.000</td>
	</tr>
	<tr>
		<td style="text-align:center">7</td>
		<td style="text-align:center"sdval="10000" >40.000</td>
	</tr>
	<tr>
		<td style="text-align:center">8</td>
		<td style="text-align:center"sdval="20000" >60.000</td>
	</tr>
	<tr>
		<td style="text-align:center">9</td>
		<td style="text-align:center"sdval="30000" >80.000</td>
	</tr>
	<tr>
		<td style="text-align:center">10</td>
		<td style="text-align:center"sdval="40000" >100.000</td>
	</tr>
	<tr>
		<td style="text-align:center">11</td>
		<td style="text-align:center"sdval="60000" >150.000</td>
	</tr>
	<tr>
		<td style="text-align:center">12</td>
		<td style="text-align:center"sdval="80000" >200.000</td>
	</tr>
	<tr>
		<td style="text-align:center">13</td>
		<td style="text-align:center"sdval="100000" >300.000</td>
	</tr>
	<tr>
		<td style="text-align:center">14</td>
		<td style="text-align:center"sdval="120000" >400.000</td>
	</tr>
	<tr>
		<td style="text-align:center">15</td>
		<td style="text-align:center"sdval="150000" >500.000</td>
	</tr>
	<tr>
		<td style="text-align:center">16</td>
		<td style="text-align:center"sdval="200000" >600.000</td>
	</tr>
	<tr>
		<td style="text-align:center">17</td>
		<td style="text-align:center"sdval="400000" >700.000</td>
	</tr>
	<tr>
		<td style="text-align:center">18</td>
		<td style="text-align:center"sdval="600000" >800.000</td>
	</tr>
	<tr>
		<td style="text-align:center">19</td>
		<td style="text-align:center"sdval="800000" >900.000</td>
	</tr>
		<tr>
		<td style="text-align:center">20</td>
		<td style="text-align:center"sdval="800000" >1.000.000</td>
	</tr>
</table>

[](id:customize)
#### Regras personalizadas:
Para e-mails de alta qualidade, se o plano de warm-up padrão não atender às suas necessidades, você poderá solicitar um plano de warm-up atualizado. Para obter detalhes e fazer sua solicitação, entre em contato com seu representante de vendas.
[](id:batch)
## Conjunto de funcionalidades de envio em lote
Essas funcionalidades são adequadas para envio em lote de e-mails de marketing ou de notificação. Para enviar e-mails baseados em acionamento (como e-mails transacionais e de autenticação), é recomendável chamar a API `SendEmail`.
### Funcionalidades
Você pode usar a funcionalidade de envio em lote do SES de uma das seguintes maneiras:
•	Console: É necessário um modelo, o tamanho de um e-mail não deve exceder 10 MB e não são permitidos anexos.
•	API: É necessário um modelo, o tamanho de um e-mail não deve exceder 10 MB e são permitidos anexos.

### Descrição
No console, você pode gerenciar endereços de remetentes na página **Email Sending (Envio de e-mail)** > **Recipient Groups (Grupos de destinatários)**.

A funcionalidade de envio em lote está configurada para usar o plano de warm-up padrão. O plano identificará automaticamente a reputação do IP/domínio, atribuirá a cota diária de envio e determinará se o volume total de envio excede a quantidade máxima permitida por dia. Se exceder, o envio de e-mails será interrompido e os demais e-mails entrarão na fila de cache e serão enviados 24 horas depois.

## Envio em lote
Para enviar e-mails em lotes, crie uma tarefa de envio no console, selecione **Batch (Lote)** em **Task Type (Tipo de tarefa)** e defina todos os campos obrigatórios para a tarefa.
## Envio agendado
Os e-mails podem ser enviados em um horário agendado. Selecione **Start Time (Hora de início)** para a tarefa e os e-mails serão enviados automaticamente no horário especificado.
## Envio recorrente
Você pode definir e-mails recorrentes no console especificando os campos da tarefa, incluindo **Start Time (Hora de início)** e **Recurrence (Recorrência)**. O console enviará e-mails de forma automática com base na recorrência especificada.
