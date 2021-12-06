## Descrição de alarmes
Você pode criar alarmes para métricas de instância especificadas, a fim de que sua instância do CLB envie informações de alarme para grupos de usuários de destino quando seu status de execução atender a uma determinada condição. Fazendo isso, você pode detectar exceções em tempo hábil e tomar as ações apropriadas para garantir a estabilidade e confiabilidade do sistema. Para obter mais informações, consulte a [Visão geral de alarmes](https://intl.cloud.tencent.com/document/product/248/6126).
As políticas de alarmes do CLB abrangem o seguinte:
- Listener da rede pública
- Listener da rede privada
- Porta do servidor (outra)
  - Nível do listener
  - Nível da porta do servidor
- Porta do servidor (tipo clássico da rede privada)
- Monitoramento de protocolo da camada 7

## Listeners da rede pública/privada
Atualmente, tanto o CLB da rede pública quanto o da rede privada aceitam alarmes no nível do listener com as seguintes métricas:

| Métrica | Unidade | Descrição |
|----|------|----|
| Largura de banda de entrada | Mbps | A largura de banda usada pelo cliente para acessar o CLB na rede pública dentro de um período de referência. |
| Largura de banda de saída | Mbps | A largura de banda usada pelo CLB para acessar a rede pública dentro de um período de referência. |
| Quantidade de pacotes de entrada | Pacotes/s | A quantidade de pacotes de dados de solicitações recebidos pelo CLB por segundo dentro de um período de referência. |
| Quantidade de pacotes de saída | Pacotes/s | A quantidade de pacotes de dados enviados pelo CLB por segundo dentro de um período de referência. |

## Porta do servidor (outra)
Todas as instâncias do CLB, exceto as do clássico da rede privada, aceitam alarmes nos dois níveis abaixo:
1. Nível do listener
Você pode configurar a quantidade de portas excepcionais do servidor de back-end de um listener para estatísticas de exceções de todas as portas do servidor vinculadas ao listener, que dispararão alarmes com base no limite configurado. Conforme mostrado abaixo, a quantidade de portas excepcionais de todos os servidores de back-end no listener selecionado é coletada uma vez a cada minuto; se a quantidade for maior que 10 por segundo por dois períodos de referência consecutivos, vai disparar um alarme uma vez por dia.
>?Para ativar o alarme no nível do listener, [envie um tíquete](https://console.cloud.tencent.com/workorder/category) para solicitar.

 - Configure objetos de alarmes:
![](https://main.qcloudimg.com/raw/bf26227edb359e6f7acd01febbbc38c9.png)
 - Configure condições de disparo:
![](https://main.qcloudimg.com/raw/7cb8c5db9a1fb616f478e2e109d31097.png)
2. Nível da porta do servidor
Você pode configurar alarmes de exceções para uma porta especificada de um servidor de back-end vinculado a um listener, de modo que os alarmes sejam enviados sempre que a porta for excepcional.
 - Configure objetos de alarmes:
![](https://main.qcloudimg.com/raw/e1d947188535eac4189254ba0e8a26cb.png)
 - Configure condições de disparo:
![](https://main.qcloudimg.com/raw/80e4072ba35d426e4503a7b64ea63865.png)
>!
>- Exceção da porta do servidor de back-end: significa que o CLB localiza a porta do servidor de back-end indisponível; em alguns casos, a tremulação da rede também pode acionar exceções de porta.
>- As estatísticas no nível do listener incluem o status da porta de todos os servidores de back-end sob o listener, desde a convergência de alarme único até o alarme de limite. Para evitar o impacto da tremulação da rede, recomendamos o uso de alarmes no nível do listener.

## Porta do servidor (tipo clássico da rede privada)
Você pode configurar os alarmes de exceções da porta do servidor para o CLB clássico da rede privada conforme as instruções em "Server Port (Other) > Server port level (Porta do servidor (outra) > Nível da porta do servidor)".
Você pode configurar alarmes de exceções para uma porta especificada de um servidor de back-end vinculado a um listener, de modo que os alarmes sejam enviados sempre que a porta for excepcional.

## Monitoramento de protocolo da camada 7
Você pode configurar políticas de alarme de métrica de monitoramento exclusivas para todos os listeners (HTTP/HTTPS) da camada 7. As métricas específicas são conforme abaixo:

| Métrica | Unidade | Descrição |
|----|------|----|
| Largura de banda de entrada | Mbps | A largura de banda usada pelo cliente para acessar o CLB na rede pública dentro de um período de referência. |
| Largura de banda de saída | Mbps | A largura de banda usada pelo CLB para acessar a rede pública dentro de um período de referência. |
| Quantidade de pacotes de entrada | Pacotes/s | A quantidade de pacotes de dados de solicitações recebidos pelo CLB por segundo dentro de um período de referência. |
| Quantidade de pacotes de saída | Pacotes/s | A quantidade de pacotes de dados enviados pelo CLB por segundo dentro de um período de referência. |
| Quantidade de conexões novas | - | A quantidade de conexões novas estabelecidas por minuto em um período de referência. |
| Quantidade de conexões ativas | - | A quantidade de conexões ativas por minuto em um período de referência. |
| Tempo médio de resposta | ms | O tempo médio de resposta do CLB dentro de um período de referência. |
| Tempo máximo de resposta | ms | O tempo máximo de resposta do CLB dentro de um período de referência. |
| Código de status 2xx | - | A quantidade de códigos de status 2xx retornados pelo servidor de back-end dentro de um período de referência. |
| Código de status 3xx | - | A quantidade de códigos de status 3xx retornados pelo servidor de back-end dentro de um período de referência. |
| Código de status 4xx | - | A quantidade de códigos de status 4xx retornados pelo servidor de back-end dentro de um período de referência. |
| Código de status 5xx | - | A quantidade de códigos de status 5xx retornados pelo servidor de back-end dentro de um período de referência. |
| Código de status 404 | - | A quantidade de códigos de status 404 retornados pelo servidor de back-end dentro de um período de referência. |
| Código de status 502 | - | A quantidade de códigos de status 502 retornados pelo servidor de back-end dentro de um período de referência. |
| Código de status 3xx retornado pelo CLB | - | A quantidade de códigos de status 3xx retornados pelo CLB dentro de um período de referência. |
| Código de status 4xx retornado pelo CLB | - | A quantidade de códigos de status 4xx retornados pelo CLB dentro de um período de referência. |
| Código de status 5xx retornado pelo CLB | - | A quantidade de códigos de status 5xx retornados pelo CLB dentro de um período de referência. |
| Código de status 404 retornado pelo CLB | - | A quantidade de códigos de status 404 retornados pelo CLB dentro de um período de referência. |
| Código de status 502 retornado pelo CLB | - | A quantidade de códigos de status 502 retornados pelo CLB dentro de um período de referência. |

