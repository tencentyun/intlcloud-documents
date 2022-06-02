[](id:que1) 
### Como faço para testar o envio de e-mails de maneira simples?
Você pode usar suas próprias contas para o teste. Atualmente, o SES oferece um nível gratuito de mil e-mails, mas não oferece contas de teste.

[](id:que5) 
### Posso enviar uma grande quantidade de e-mails desde o início?
Não. É necessário aumentar o volume de envio de forma gradual, dia após dia, e não é possível elevá-lo ao nível desejado de uma só vez. Para ganhar uma boa reputação com seu ISP, é necessário um warm-up automático antes do envio de e-mails. A norma é que as regras de warm-up padrão se apliquem ao modo de envio em lote. Consulte [Funcionalidades](https://intl.cloud.tencent.com/document/product/1084/43285).

[](id:que6) 
### O que é o warm-up?
O warm-up é uma maneira de estabelecer uma reputação para um IP novo. Normalmente, todos os provedores de serviços de e-mail têm um limite na quantidade diária de e-mails enviados de um IP. Você precisa começar com uma quantidade menor de e-mails e aumentar a quantidade de forma gradual a cada dia.

[](id:que7) 
A norma é que as regras de warm-up padrão se apliquem ao modo de envio em lote. O back-end determinará o progresso do warm-up com base em várias políticas e atribuirá automaticamente a cota diária de envio. O processo é totalmente automático. Quando a quantidade máxima permitida de e-mails enviados por dia for atingida, o envio de e-mails será interrompido e os demais e-mails entrarão na fila de cache e serão enviados 24 horas depois. O plano de warm-up padrão é o seguinte:
<table style="width: 200px;">
   <tr>
      <th width="0px" style="text-align:center">Dia</td>
      <th width="0px" style="text-align:center">Volume de envio/dia</td>
   </tr>
	<tr>
		<td style="text-align:center"style="text-align:center">1</td>
		<td style="text-align:center">100</td>
	</tr>
	<tr>
		<td style="text-align:center">2</td>
		<td style="text-align:center"sdval="200" >200</td>
	</tr>
	<tr>
		<td style="text-align:center">3</td>
		<td style="text-align:center"sdval="500" >500</td>
	</tr>
	<tr>
		<td style="text-align:center">4</td>
		<td style="text-align:center"sdval="1000" >1.000</td>
	</tr>
	<tr>
		<td style="text-align:center">5</td>
		<td style="text-align:center"sdval="2000" >2.000</td>
	</tr>
	<tr>
		<td style="text-align:center">6</td>
		<td style="text-align:center"sdval="5000" >5.000</td>
	</tr>
	<tr>
		<td style="text-align:center">7</td>
		<td style="text-align:center"sdval="10,000" >10.000</td>
	</tr>
	<tr>
		<td style="text-align:center">8</td>
		<td style="text-align:center"sdval="20,000" >20.000</td>
	</tr>
	<tr>
		<td style="text-align:center">9</td>
		<td style="text-align:center"sdval="30000" >30.000</td>
	</tr>
	<tr>
		<td style="text-align:center">10</td>
		<td style="text-align:center"sdval="40000" >40.000</td>
	</tr>
	<tr>
		<td style="text-align:center">11</td>
		<td style="text-align:center"sdval="60000" >60.000</td>
	</tr>
	<tr>
		<td style="text-align:center">12</td>
		<td style="text-align:center"sdval="80000" >80.000</td>
	</tr>
	<tr>
		<td style="text-align:center">13</td>
		<td style="text-align:center"sdval="100000" >100.000</td>
	</tr>
	<tr>
		<td style="text-align:center">14</td>
		<td style="text-align:center"sdval="120000" >120.000</td>
	</tr>
	<tr>
		<td style="text-align:center">15</td>
		<td style="text-align:center"sdval="150000" >150.000</td>
	</tr>
	<tr>
		<td style="text-align:center">16</td>
		<td style="text-align:center"sdval="200000" >200.000</td>
	</tr>
	<tr>
		<td style="text-align:center">17</td>
		<td style="text-align:center"sdval="400000" >400.000</td>
	</tr>
	<tr>
		<td style="text-align:center">18</td>
		<td style="text-align:center"sdval="600000" >600.000</td>
	</tr>
	<tr>
		<td style="text-align:center">19</td>
		<td style="text-align:center"sdval="800000" >800.000</td>
	</tr>
		<tr>
		<td style="text-align:center">20</td>
		<td style="text-align:center"sdval="800000" >1.000.000</td>
	</tr>
</table>

Regras personalizadas:

Para e-mails de alta qualidade, se o plano de warm-up padrão não puder atender às suas necessidades, você poderá usar um plano de warm-up personalizado. Para obter detalhes e fazer a solicitação, entre em contato com seu representante de vendas.
