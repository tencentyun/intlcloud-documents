## Análise comparativa de algoritmos do CLB

### Programação do round-robin ponderado
- **Como funciona**
A programação do round-robin destina-se a programar solicitações para servidores diferentes com base em polling, ou seja, o sistema executa `i = (i + 1) mod n` para selecionar o servidor i em cada programação. A programação do round-robin ponderado pode resolver o desequilíbrio de desempenho de diferentes servidores. Ele usa o peso para representar o desempenho de processamento de um servidor e programa solicitações para diferentes servidores, por peso, através de sondagem. Servidores com maior peso recebem conexões mais rapidamente, contudo precisam processar um número maior de conexões do que aqueles com peso inferior. Servidores com o mesmo peso processam o mesmo número de conexões.
- **Vantagens**
Algoritmo simples e muito prático. É um algoritmo de programação sem estado que não registra o status de todas as conexões.
- **Desvantagens**
A programação do round-robin ponderado é relativamente simples, mas não é adequada para cenários em que o tempo de serviço de uma solicitação muda significativamente ou quando cada solicitação consome diferentes quantidades de tempo. Nesses cenários, a programação do round-robin pode causar desequilíbrio na distribuição de carga entre os servidores.
- **Casos de uso**
Esse algoritmo é adequado para cenários em que cada solicitação consome basicamente a mesma quantidade de tempo no back-end com o melhor desempenho de carregamento. Ele costuma ser usado em serviços de conexão não persistentes, como serviço HTTP.
- **Recomendações**
Se você sabe que cada solicitação consome basicamente a mesma quantidade de tempo no back-end (por exemplo, solicitações processadas por um servidor de back-end são do mesmo tipo ou de tipos semelhantes), é recomendável usar a programação do round-robin ponderado. Se a diferença de tempo entre cada solicitação for pequena, recomendamos que você use este algoritmo porque tem baixo consumo, alta eficiência e não há necessidade de travessia.

### Programação de conexão mínima ponderada
- **Como funciona**
Em situações reais, o tempo que cada solicitação do cliente passa no servidor pode variar muito. Se um algoritmo round-robin simples ou de balanceamento de carga aleatório for usado conforme o tempo de trabalho aumenta, o número de processos de conexão em cada servidor pode variar muito e o balanceamento de carga pode não ser alcançado. Ao contrário da programação do round-robin, a programação de conexão mínima é um algoritmo de programação dinâmico que estima a carga em um servidor com base no respectivo número de conexões ativas. O programador registra o número de conexões estabelecidas atualmente em cada servidor. Se uma solicitação for programada para um servidor, sua quantidade de conexões aumentará em 1. Se uma conexão for interrompida ou expirar, sua quantidade de conexões diminuirá em 1. O algoritmo de programação de conexão mínima ponderada é baseado na programação de conexão mínima e é responsável por aprimorá-la. Pesos diferentes são alocados aos servidores de acordo com o respectivo desempenho de processamento. Dessa forma, o servidor recebe um número de solicitações com base em seu peso.
 1. Suponha que o peso de um servidor de back-end seja wi (i = 1...n) e sua quantidade de conexões seja ci (i = 1...n). O servidor de back-end com o menor valor de ci/wi será o próximo servidor a receber uma nova solicitação.
 2. Para servidores de back-end com o mesmo valor de ci/wi, eles serão programados com base no round-robin ponderado.
- **Vantagens**
Este algoritmo é adequado para solicitações que requerem processamento de longo prazo, como FTP.
- **Desvantagens**
Devido às restrições da API, a conexão mínima e a persistência da sessão não podem ser ativadas ao mesmo tempo.
- **Casos de uso**
Este algoritmo é adequado para cenários em que o tempo usado por cada solicitação no back-end varia muito. Ele costuma ser usado em serviços de conexão de persistência.
- **Recomendações**
Se você precisar processar solicitações diferentes e o tempo de serviço no back-end variar muito (como 3 milissegundos e 3 segundos), recomendamos que você use a programação de conexão mínima ponderada para obter balanceamento de carga.

### Programação de hash de origem (ip_hash)
- **Como funciona**
A programação de hash de origem usa o endereço IP de origem da solicitação como a chave de hash e localiza o servidor correspondente na tabela de hash atribuída estaticamente. A solicitação será enviada a esse servidor se estiver disponível e não sobrecarregado; caso contrário, será retornado um valor nulo.
- **Vantagens**
O ip_hash pode alcançar certa persistência de sessão lembrando o IP de origem e mapeando solicitações de um cliente para o mesmo servidor de back-end por meio da tabela de hash. Em cenários nos quais a persistência de sessão não é suportada, o ip_hash pode ser usado para a programação.
- **Recomendações**
Este algoritmo calcula o valor de hash do endereço de origem de uma solicitação e distribui a solicitação ao servidor de back-end correspondente com base em seu peso. Isso permite que solicitações do mesmo IP de cliente sejam distribuídas para o mesmo servidor. Este algoritmo é adequado para balanceamento de carga sobre protocolo TCP que não oferece suporte a cookies.

## Escolha do algoritmo de balanceamento de carga e configuração do peso
Nos próximos recursos do CLB, **o encaminhamento da camada 7 oferecerá suporte ao método de balanceamento de conexão mínima.** Fornecemos exemplos de referência sobre como escolher o algoritmo de balanceamento de carga e configurar o peso, para que você possa garantir que os clusters de servidores de back-end realizem negócios em diferentes cenários com estabilidade.
- Cenário 1
Suponha que existam 3 servidores de back-end com a mesma configuração (CPU e memória) e você configure seus pesos para 10. Suponha que 100 conexões TCP tenham sido estabelecidas entre cada servidor de back-end e o cliente. Se um novo servidor de back-end for adicionado, recomendamos que você use o algoritmo de programação de conexão mínima, que pode aumentar rapidamente a carga do 4º servidor e reduzir a pressão nos outros 3 servidores.
- Cenário 2
Suponha que você use os serviços Tencent Cloud pela primeira vez. Seu site acaba de ser construído e está com baixo carregamento. Recomendamos que você compre servidores de back-end com a mesma configuração porque são todos servidores de camada de acesso. Neste cenário, você pode configurar os pesos de todos os servidores de back-end para 10 e usar o algoritmo de programação do round-robin ponderado para distribuir o tráfego.
- Cenário 3
Suponha que você tenha 5 servidores de back-end para realizar solicitações de acesso simples a sites estáticos e a proporção da capacidade de computação (calculada pela CPU e memória) deles seja de 9:3:3:3:1. Neste cenário, você pode configurar os pesos dos servidores para 90, 30, 30, 30 e 10, respectivamente. Como as solicitações de acesso a sites estáticos são principalmente do tipo de conexão de não persistência, você pode usar o algoritmo de programação do round-robin ponderado, para que o CLB possa alocar solicitações com base na taxa de desempenho de servidores de back-end.
- Cenário 4
Suponha que você tenha 10 servidores de back-end para realizar grandes quantidades de solicitações de acesso à web e que não deseja comprar mais servidores. Um dos servidores frequentemente reinicia devido à sobrecarga. Neste cenário, recomendamos que você configure os pesos dos servidores existentes com base em seu desempenho. O servidor com maior carga deve ter um peso menor. Além disso, você pode usar o algoritmo de programação de conexão mínima para alocar solicitações a servidores de back-end com menos conexões ativas para evitar a sobrecarga do servidor.
- Cenário 5
Suponha que você tenha 3 servidores de back-end para processar conexões persistentes com proporções de capacidade de computação (calculada pela CPU e memória) de 3:1:1. O servidor com o melhor desempenho processa mais solicitações, mas você não quer que ele fique sobrecarregado. Em vez disso, você deseja alocar novas solicitações para servidores inativos. Neste cenário, você pode usar o algoritmo de programação de conexão mínima e reduzir apropriadamente os pesos dos servidores ocupados para que o CLB possa alocar solicitações para servidores de back-end com menos conexões ativas, conseguindo, assim, o balanceamento de carga.
- Cenário 6
Suponha que você queira que as solicitações subsequentes do cliente sejam alocadas no mesmo servidor. A programação de round-robin ponderado ou de conexão mínima ponderada não pode garantir que as solicitações do mesmo cliente sejam alocadas para o mesmo servidor. Para atender aos requisitos de seu servidor de aplicativos especificado e manter a "aderência" (ou "continuidade") das sessões do cliente, recomendamos o uso de ip_hash para distribuir o tráfego. Este algoritmo garante que todas as solicitações do mesmo cliente serão distribuídas para o mesmo servidor de back-end, a menos que o número de servidores mude ou o servidor fique indisponível.
