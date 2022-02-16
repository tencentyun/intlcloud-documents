## Visão geral do modo de capacidade de leitura/gravação
O TcaplusDB usa o modo de capacidade de leitura/gravação para calcular o volume de solicitações de leitura/gravação da tabela.

### Unidade de capacidade (CU)
É a unidade mínima de solicitações de acesso a recursos e a unidade estatística mínima de leituras/gravações de dados solicitadas.

### Unidade de capacidade de leitura (RCU)
É a unidade mínima de solicitações de leitura. Os dados de resposta gerados para uma solicitação podem conter várias RCUs. O valor máximo de uma RCU é 4 KB, ou seja, uma RCU indica que uma solicitação de leitura pode ser realizada em um registro que tem até 4 KB de tamanho. Caso necessite ler dados com mais de 4 KB, precisará de mais RCUs.

A quantidade base de uma RCU é 4 KB. O tamanho de uma solicitação abaixo de 4 KB é calculado como 4 KB e o tamanho de uma solicitação acima de 4 KB é calculado como um múltiplo de 4 KB (a parte restante abaixo de 4 KB é calculada como 4 KB).
Segue abaixo um exemplo:
**Capacidade de solicitações de leitura**
  Você envia uma solicitação para consultar um campo em um registro que tem 10 KB de tamanho e o banco de dados retorna o valor do campo especificado do registro. Nesse caso, os dados de resposta são 10 KB, o que é 3 RCUs.

### Unidade de capacidade de gravação (WCU)
É a unidade mínima de solicitações de gravação. Os dados gravados gerados para uma solicitação de gravação podem conter várias WCUs. O valor máximo de uma WCU é 4 KB, ou seja, cada 4 KB de dados gravados será contado como uma WCU.
A quantidade base de uma WCU é 4 KB. O tamanho de uma solicitação abaixo de 4 KB é calculado como 4 KB e o tamanho de uma solicitação acima de 4 KB é calculado como um múltiplo de 4 KB (a parte restante abaixo de 4 KB é calculada como 4 KB).
Você pode selecionar se deseja ativar a funcionalidade de sinalizador de resultado ao executar uma operação de gravação. Se estiver ativada, o sistema calculará automaticamente as CUs retornadas como WCUs.
Quantidade consumida de WCUs = CUs geradas por gravação de dados + CUs retornadas

Segue abaixo um exemplo:
- **Solicitação de gravação**
  Você envia uma solicitação para atualizar o conteúdo de 5 KB e o back-end lê o registro (50 KB no total) contendo os dados de destino do disco para a memória.
  Em seguida, o back-end atualiza o registro e libera o conteúdo de 50 KB no disco após a atualização.
  Se você ativou o sinalizador de resultado, o conteúdo de 5 KB será retornado.
- **Sinalizador de resultado ativado**
  13 CUs (dados de 50 KB gravados no disco) + 2 CUs (dados retornados de 5 KB) = 15 WCUs geradas
- **Sinalizador de resultado não ativado**
  13 CUs (dados de 50 KB gravados no disco) = 13 WCUs geradas

### Modo predefinido
Se você selecionar o modo predefinido, será necessário ajustar a capacidade predefinida de leitura/gravação da tabela com base na alteração de acesso. Esta operação pode ajudar você a controlar a utilização do TcaplusDB para mantê-lo igual ou abaixo da taxa de solicitações definida, para que você possa prever os custos.
Para configurar a capacidade predefinida de maneira perfeita, você precisa estimar o tráfego de aplicativos antecipadamente.

#### Leitura reservada
Refere-se à pré-configuração de RCU de uma tabela. Você precisa estimar o maior consumo de RCU por segundo da tabela no dia e definir o valor como as RCUs reservadas.

#### Gravação reservada
Refere-se à pré-configuração de WCU de uma tabela. Você precisa estimar o maior consumo de WCU por segundo da tabela no dia e definir o valor como as WCUs reservadas.

#### Capacidade reservada
Refere-se à pré-configuração do uso da capacidade do disco de uma tabela. Você precisa estimar a capacidade utilizada pela tabela no dia.

#### Limite e cota de solicitações
Como o valor de RCU ou WCU configurado pode ser muito baixo ou a quantidade de solicitações de acesso pode aumentar, por padrão, o TcaplusDB limita as solicitações que excedem 40% das RCUs ou WCUs reservadas. Esse limite não bloqueia as solicitações; do contrário, faz com que as solicitações sejam enfileiradas para reduzir a frequência de acesso, o que pode atingir o tempo limite do programa. Você pode usar a funcionalidade de monitoramento e alarme para saber se a quantidade atual de solicitações excede a capacidade pré-configurada.

Esse limite pode evitar que seu aplicativo consuma muitas CUs. No entanto, se as solicitações forem limitadas, elas falharão e muitos erros de sistema ocorrerão.

Você pode usar o monitoramento de tabelas do TcaplusDB para monitorar as RCUs/WCUs reais e modificar a cota de tabelas, se necessário.
