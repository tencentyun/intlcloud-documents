A persistência de sessão pode encaminhar solicitações do mesmo IP para o mesmo servidor de back-end. Por padrão, uma instância do CLB roteará solicitações para servidores de back-end diferentes para balanceamento de carga. No entanto, você pode usar a persistência de sessão para rotear solicitações de um usuário especificado para o mesmo servidor de back-end, para que alguns aplicativos que precisam manter sua sessão (como carrinho de compras) possam ser executados corretamente.

## Persistência de sessão da camada 4
Os protocolos da camada 4 (TCP/UDP) aceitam a persistência de sessão baseada em IP de origem. A duração da persistência de sessão pode ser definida como qualquer número inteiro entre 30 e 3.600 segundos. Se o limite de tempo for excedido e a sessão não tiver uma nova solicitação, a persistência de sessão será encerrada. A persistência de sessão está sujeita ao modo de balanceamento de carga:
- No modo de "weighted round-robin (round-robin ponderado)", em que as solicitações são distribuídas com base no peso dos servidores de back-end, a persistência de sessão com base no IP de origem é aceita.
- No modo de "weighted least-connection (conexão mínima ponderada)", em que a programação geral depende da carga e do peso do servidor, a persistência de sessão não é aceita.

## Persistência de sessão da camada 7
Os protocolos da camada 7 (HTTP/HTTPS) aceitam a persistência de sessão com base na inserção de cookies (o CLB insere o cookie no cliente). A duração da persistência de sessão pode ser definida como qualquer valor entre 30 e 3.600 segundos. A persistência de sessão está sujeita ao modo de balanceamento de carga:
- No modo de "weighted round-robin (round-robin ponderado)", em que as solicitações são distribuídas com base no peso dos servidores de back-end, a persistência de sessão com base na inserção de cookies é aceita.
- No modo de "weighted least-connection (conexão mínima ponderada)", em que a programação geral depende da carga e do peso do servidor, a persistência de sessão não é aceita.
- O modo de "IP Hash (Hash de IP)" aceita persistência de sessão com base no IP de origem, mas não na inserção de cookies.

## Tempo limite de conexão
Atualmente, o tempo limite da conexão HTTP (`keepalive_timeout`) é 75 segundos por padrão. Se você quiser ajustá-lo, ative a [configuração personalizada](https://intl.cloud.tencent.com/document/product/214/32427). Se o limite for excedido e a sessão não tiver transmissão de dados, a conexão será desconectada.
Atualmente, o tempo limite da conexão TCP é de 900 segundos por padrão e não pode ser personalizado. Se o limite for excedido e a sessão não tiver transmissão de dados, a conexão será desconectada.

## Configuração da persistência de sessão
1. Faça login no [Console do CLB](https://console.cloud.tencent.com/loadbalance) e clique no ID da instância do CLB a ser configurada com persistência de sessão, para acessar a página de detalhes.
2. Selecione a guia **Listener Management (Gerenciamento de listener)**.
3. Clique em **Modify (Modificar)** após o listener do CLB ser configurado com persistência de sessão.
4. Escolha se deseja ativar a funcionalidade de persistência de sessão. Clique no botão para ativá-la, insira a duração da persistência e clique em **OK**.

## Relação entre conexão persistente e persistência de sessão

### Cenário 1. Negócios HTTP da camada 7

**Suponha que um cliente acesse o protocolo HTTP/1.1 e `Connection:keep-alive` esteja configurado nas informações do cabeçalho. O cliente acessa o CVM por meio de uma instância do CLB sem a persistência de sessão ativada. O cliente pode acessar o mesmo CVM na próxima vez?**

**R:** não.

Primeiro, o keep-alive HTTP indica que a conexão TCP permanece conectada após o envio de uma solicitação, para que o navegador possa enviar solicitações por meio da mesma conexão. A conexão persistente reduz o tempo necessário para estabelecer uma nova conexão para cada solicitação e diminui o consumo de largura de banda. O tempo limite padrão de um cluster do CLB é 75 segundos (se não houver nenhuma solicitação nova dentro de 75 segundos, o TCP será desconectado por padrão).

O keep-alive HTTP é estabelecido entre o cliente e uma instância do CLB. Se a persistência de sessão de cookies estiver desativada, a instância do CLB selecionará uma instância do CVM aleatoriamente, de acordo com a política de sondagem. A conexão persistente anterior não é mais válida.

Portanto, recomendamos que você ative a persistência de sessão.

Se o período da persistência de sessão de cookies for configurado como 1.000 segundos, o cliente iniciará uma solicitação novamente. Como o período entre as duas solicitações excede 75 segundos, a conexão TCP precisa ser estabelecida de novo. A camada de aplicativos identifica o cookie e localiza a instância do CVM que o cliente acessou da última vez, para que seja avaliada novamente desta vez.

### Cenário 2. Negócios TCP da camada 4
**Suponha que um cliente inicie o acesso, o TCP é o protocolo da camada de transporte, a conexão persistente está ativada, mas a persistência de sessão com base no IP de origem está desativada. O mesmo cliente pode acessar o mesmo servidor na próxima solicitação de acesso?**

**R:** não necessariamente.

Primeiro, de acordo com o mecanismo de implementação da camada 4, quando a conexão persistente é ativada para o TCP e não fechada, e a mesma conexão é acessada em duas solicitações, o mesmo cliente pode acessar o mesmo servidor. Se a conexão for fechada por alguns motivos (como reinício da rede ou tempo limite de conexão) durante a segunda solicitação de acesso, a solicitação pode ser programada para outro servidor de back-end. O tempo limite global padrão para uma conexão persistente é 900 segundos, ou seja, a conexão persistente será liberada se não houver uma nova solicitação em 900 segundos.
