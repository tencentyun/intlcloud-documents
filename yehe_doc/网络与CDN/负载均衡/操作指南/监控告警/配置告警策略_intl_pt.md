É possível criar um alarme para disparar alarmes e enviar mensagens de alarme para um determinado grupo de usuários quando um produto do Tencent Cloud atender à condição configurada. O alarme criado pode determinar periodicamente se uma notificação de alarme deve ser enviada com base na diferença entre a métrica monitorada e o limite fornecido.

Os usuários especificados podem tomar medidas preventivas ou corretivas apropriadas em tempo hábil quando o alarme for disparado. Portanto, alarmes criados corretamente podem ajudar você a melhorar a robustez e a confiabilidade de suas aplicações. Para obter mais informações sobre alarmes, consulte [Criação de políticas de alarme](https://intl.cloud.tencent.com/document/product/248/38908).

Você pode criar uma política de alarmes com as seguintes etapas:
1. Faça login no [Console do Cloud Monitor](https://console.cloud.tencent.com/monitor/overview).
2. Clique em **Alarm Configuration (Configuração de alarmes)** > **Alarm Policy (Política de alarmes)** na barra lateral esquerda para acessar a [página de configuração da política de alarmes](https://console.cloud.tencent.com/monitor/policylist).
3. Clique em **Add (Adicionar)** para configurar uma política de alarmes.
4. Configure os itens básicos conforme mostrado abaixo:
 - Policy Name (Nome da política): insira um nome para a política.
 - Remarks (Observações): adicione observações à política.
 - Policy Type (Tipo de política): selecione a métrica de monitoramento.
 - Project (Projeto): selecione um projeto conforme necessário.

5. Configure objetos de alarmes.
 - Se você selecionar "all objects (todos os objetos)", a política de alarmes será associada a todas as instâncias na conta atual.
 - Se você selecionar "some objects (alguns objetos)", a política de alarmes será associada às instâncias selecionadas.
 - Se você selecionar "Instance group (Grupo de instâncias)", a política de alarmes será associada ao grupo de instâncias selecionado.

6. Defina o gatilho do alarme. Você pode escolher um modelo de condição de disparo ou configurar as condições de disparo.
 - Modelo de condição de disparo
  Ative "Trigger Condition Template (Modelo de condição de disparo)" e selecione um modelo configurado na lista suspensa. Para obter as configurações detalhadas, consulte [Configuração de modelos de condição de disparo](https://intl.cloud.tencent.com/document/product/248/38911). Se um modelo recém-criado não for exibido, clique em **Refresh (Atualizar)** à direita.
 - Configure a condição de disparo
Um gatilho de alarme é uma condição semântica que consiste em métrica, período estatístico, relação de comparação, limite, duração e frequência de notificações.
Por exemplo, se a métrica especificada for `pacotes de entrada`, o período estatístico for `1 minuto`, a relação de comparação for `>`, o limite for `100 pacotes/s`, a duração for `2 períodos` e a frequência de notificação for `uma vez por dia`, a quantidade de pacotes de entrada será coletada uma vez a cada minuto, e um alarme será acionado uma vez por dia se a quantidade de pacotes de entrada de um listener do CLB for superior a 100 pacotes/s por duas vezes consecutivas.

7. Configure o canal de alarme. Configure o grupo de destinatários, o período de validade e o canal de recebimento (e-mail e objeto) conforme necessário.

8. Configure o retorno de chamada da API opcional conforme necessário. Insira um URL acessível pela rede pública como o endereço da API de retorno de chamada (nome de domínio ou IP[:port][/path]) e o Cloud Monitor enviará mensagens de alarme para este endereço imediatamente.

9. Quando concluir a configuração, clique em **Complete (Concluir)**.

