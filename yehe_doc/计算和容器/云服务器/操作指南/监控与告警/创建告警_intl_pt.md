## Visão geral
Você pode definir alarmes de limite para monitorar o desempenho do CVM, além de alarmes de eventos para observar o status das instâncias do CVM e a infraestrutura da plataforma subjacente. Quando ocorrer uma exceção, você receberá imediatamente notificações por WeChat, e-mail, SMS, telefone, etc. Uma política de alarmes adequada ajudará a melhorar a robustez e a confiabilidade dos seus aplicativos. Este documento descreve como criar uma política de alarmes. Para obter mais informações, consulte [Criação da política de alarmes](https://intl.cloud.tencent.com/document/product/248/38916).

## Direções
1. Faça login no [console do Cloud Monitor] e selecione **Alarm Configuration (Configuração de alarmes)** > [**Alarm Policy (Política de alarmes)**](https://console.cloud.tencent.com/monitor/alarm2/policy) na barra lateral esquerda.
2. Na página **Alarm Policy (Política de alarmes)**, clique em **Create (Criar)**.
3. Na janela pop-up, configure as informações básicas, a política de alarmes e o modelo de notificações conforme as instruções abaixo.
<table>
  <tr>
    <th>Tipo de configuração</th>
    <th width="19%" colspan=2>Item de configuração</th>
    <th>Descrição</th>
  </tr>
  <tr>
    <td  rowspan="5"> Informações básicas</td>
    <td colspan=2>Nome da política</td>
    <td>Um nome de política personalizado</td>
  </tr>
  <tr>
    <td colspan=2>Observações</td>
    <td>Observações para a política</td>
  </tr>
  <tr>
    <td colspan=2>Tipo do Monitor</td>
    <td>Escolha <b>Cloud Product Monitoring (Monitoramento de produto em nuvem)</b></td>
  </tr>
  <tr>
    <td colspan=2>Tipo da política</td>
    <td>Selecione o tipo de política desejada para monitorar os serviços do Tencent Cloud.</td>
  </tr>
  <tr>
    <td colspan=2>Projeto</td>
    <td>Escolha um projeto conforme necessário. Posteriormente, você poderá encontrar essa política rapidamente, filtrando por projeto.
  </tr>
  <tr>
    <td rowspan="4">Configure políticas de alarmes</td>
    <td colspan=2>Objeto de alarme</td>
    <td>
      <ul>
			         <li><b>Instance ID (ID da instância)</b>: associe a política com a instância do CVM especificada</li>
           <li><b>Tag</b>: associe a política a instâncias do CVM com a tag especificada</li>
               <li><b>Instance Group (Grupo de instâncias)</b>: associe a política ao grupo de instâncias selecionado</li>
		            <li><b>All Objects (Todos os objetos)</b>:  associe a política a todas as instâncias da conta atual (é necessária permissão)</li>
           </ul>
        </td>
		<tr>
		<td rowspan=3>Condição de disparo</td>
    <td><b>Manual Configuration (Configuração manual)</b>(Alarme de métricas)</td>
    <td>
Condição de disparo: especifique a métrica, a comparação, o limite, o período estatístico e a quantidade de períodos consecutivos. Você pode expandir a condição de disparo para visualizar a tendência da métrica e, com base nela, definir um limite adequado.
  <tr>
    <td><b>Manual Configuration (Configuração manual)</b>(Alarme de eventos)</td>
    <td>Crie uma política de alarmes de eventos para receber notificações em caso de exceções de recursos de serviço ou da infraestrutura subjacente</td>
  </tr>
  <tr>
    <td>Selecione o modelo</td>
    <td>Escolha um modelo de configuração conforme necessário. Para obter mais informações sobre as configurações, consulte <a href="https://intl.cloud.tencent.com/document/product/248/38911">Configuração do modelo de condição de disparo</a>.</td>
  </tr>
        <tr>
        <td>Configure a notificação de alarmes (opcional)</td>
        <td colspan=2>Modelo de notificações</td>
        <td>O padrão é o modelo de notificações predefinido (enviar a notificação para o administrador da conta raiz por SMS e e-mail). Até três modelos de notificações podem ser associados a cada política de alarmes. Para obter mais informações sobre as configurações de modelos de notificações, consulte <a href="https://intl.cloud.tencent.com/document/product/248/38922">Criação de modelo de notificações</a>.</li></td>
    </tr>
		</table>
4. Clique em **Complete (Concluir)**.





