Este documento descreve como visualizar mensagens de alarme de exceção do DBbrain no console do TencentDB for MySQL.

O serviço de notificação [alarme de exceção] do DBbrain(https://intl.cloud.tencent.com/document/product/1035/37177) envia mensagens de alarme de exceção de instância MySQL em tempo real, permitindo que você descubra problemas de diagnóstico de exceção de banco de dados de forma conveniente e rápida.
Todas as mensagens de alarme de exceção enviadas são exibidas na lista de mensagens do histórico para que você possa visualizar e localizar rapidamente problemas de diagnóstico de exceção enviados anteriormente.

## Visualização de um alarme
### Opção 1
Faça login no [console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Se ocorrer um problema de diagnóstico de exceção em uma instância quando você estiver no console, uma janela aparecerá no canto superior direito do console em tempo real para enviar a notificação de mensagem de alarme de exceção, que contém as informações da instância do banco de dados, como ID e nome de instância, item de diagnóstico e hora de início, para que você possa acompanhar de maneira rápida e conveniente o status de execução da instância do banco de dados.
- Você pode clicar em **View Exception Diagnosis Details (Exibir detalhes do diagnóstico de exceção)** na notificação de mensagem para visualizar os detalhes específicos do diagnóstico e as recomendações de otimização para a instância.
- Se você marcar **No alarm again today (Sem alarme hoje outra vez)** na notificação de mensagem, quando ocorrer um problema de diagnóstico de exceção em uma instância de banco de dados em sua conta, nenhuma mensagem de alarme de exceção será enviada a você através de janela pop-up.

![](https://main.qcloudimg.com/raw/22f1e14880499e6d18ff38f019b74d2d.png)

### Opção 2
 Faça login no [console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb), selecione **Instance List (Lista de instância)**, **Task List (Lista de tarefa)**, **Parameter Template (Modelo de parâmetros)**, **Recycle Bin (Lixeira)** ou **Placement Group (Grupo de inserção)** na barra lateral esquerda e clique em **Exception Alarm (Alarme de exceção)** no canto superior direito para expandir a lista com o histórico de mensagens de alarme de exceção. O número de alarmes gerados nas instâncias em sua conta é exibido ao lado do botão.
![](https://main.qcloudimg.com/raw/18bda2b422ce5c221001f885bd8279a4.png)

Na lista expandida contendo o histórico de mensagens de alarme de exceção, você pode visualizar todas as mensagens de alarme de exceção enviadas. É possível visualizá-las por região e clicar em uma mensagem para exibir os detalhes do diagnóstico do evento de alarme de exceção.
![](https://main.qcloudimg.com/raw/b2fcff416f3db287aa8b44b536bd33bd.png)
