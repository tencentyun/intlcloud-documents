Um método de balanceamento de carga é um algoritmo que aloca tráfego para [servidores de back-end](https://intl.cloud.tencent.com/document/product/214/32388). Cada método produz efeitos diferentes de balanceamento de carga.

## Programação do round-robin ponderado
O algoritmo de programação do round-robin ponderado é usado na programação de solicitações para servidores diferentes, com base na sondagem. Ele pode resolver problemas de desempenho desequilibrado de servidores diferentes. Ele usa o peso para representar o desempenho de processamento de um servidor e programa solicitações para servidores diferentes por peso, com base na sondagem. Ele programa servidores com base na quantidade de conexões novas, em que servidores com um peso maior recebem conexões mais cedo e têm uma chance maior de serem sondados. Os servidores com o mesmo peso vão processar a mesma quantidade de conexões.
- **Vantagem**: esse algoritmo é simples e tem alta praticidade. Ele não precisa registrar o status de todas as conexões e, portanto, é um algoritmo de programação sem estado.
- **Desvantagem**: esse algoritmo é relativamente simples, portanto, não é adequado para situações em que o tempo de serviço de uma solicitação muda muito ou em que cada solicitação precisa consumir tempos diferentes. Nesses casos, ele causará uma distribuição de carga desequilibrada entre os servidores.
- **Cenário aplicável**: esse algoritmo é adequado para cenários em que cada solicitação consome basicamente a mesma quantidade de tempo no back-end, com o melhor desempenho de carregamento. Ele costuma ser usado em serviços de conexão não persistentes, como serviço HTTP.
- **Recomendação**: se você sabe que cada solicitação consome basicamente a mesma quantidade de tempo no back-end (por exemplo, solicitações processadas por um servidor de back-end são do mesmo tipo ou de tipos semelhantes), é recomendável usar a programação do round-robin ponderado. Se a diferença de tempo entre cada solicitação for pequena, esse algoritmo também é recomendado, pois tem baixo consumo e alta eficiência, sem necessidade de travessia.

## Programação de conexão mínima ponderada
Em situações reais, o tempo que as solicitações do cliente permanecem no servidor pode variar muito. À medida que o período de trabalho fica mais longo, se um algoritmo de balanceamento de carga aleatório ou round-robin simples for usado, a quantidade de processos de conexão em cada servidor pode variar muito, podendo não atingir o efeito de balanceamento de carga.
Ao contrário da programação de round-robin, a de conexão mínima é um algoritmo de programação dinâmico que estima a carga de um servidor por sua quantidade de conexões ativas. O programador precisa registrar a quantidade de conexões estabelecidas atualmente em cada servidor. Se uma solicitação for programada para um servidor, a quantidade de conexões aumentará em 1. Se uma conexão for interrompida ou expirar, a quantidade de conexões diminuirá em 1.
No algoritmo de programação de conexão mínima ponderada que é baseado na programação de conexão mínima, pesos diferentes são alocados aos servidores de acordo com a capacidade de processamento deles. Dessa forma, um servidor pode receber uma quantidade de solicitações proporcional ao seu peso, o que é uma melhoria na programação de conexão mínima.
> Suponha que o peso de um servidor de back-end seja wi e a quantidade atual de conexões seja ci. Os valores de ci/wi de cada servidor são calculados em sequência. O servidor de back-end com o menor valor de ci/wi será o próximo servidor que receberá uma nova solicitação. Se houver servidores de back-end com o mesmo valor de ci/wi, eles serão programados com base na programação de round-robin ponderado.

- **Vantagem**: esse algoritmo é adequado para solicitações que requerem processamento de longo prazo, como FTP.
- **Desvantagem**: devido às restrições da API, a conexão mínima e a persistência de sessão não podem ser ativadas ao mesmo tempo.
- **Cenário aplicável**: esse algoritmo é adequado para cenários em que o tempo usado por cada solicitação no back-end varia muito. Ele costuma ser usado em serviços de conexão persistente.
- **Recomendação**: caso precise processar solicitações diferentes e o tempo de serviço necessário para elas no back-end variar muito (como 3 milissegundos e 3 segundos), é recomendável usar a programação de conexão mínima ponderada para atingir o balanceamento de carga.

## Programação de hash de origem
O algoritmo de programação de hash de origem (ip_hash) usa o endereço IP de origem da solicitação como a chave de hash e localiza o servidor correspondente na tabela de hash atribuída estaticamente. A solicitação será enviada a esse servidor se estiver disponível e não sobrecarregado; caso contrário, será retornado um valor nulo.
- **Vantagem**: o ip_hash pode mapear solicitações de um cliente para o mesmo servidor de back-end por meio da tabela de hash. Portanto, em cenários em que a persistência de sessão não é aceita, ele pode ser usado para atingir o efeito de persistência de sessão simples.
- **Recomendação**: esse algoritmo calcula o valor de hash do endereço de origem de uma solicitação e distribui a solicitação para o servidor de back-end correspondente, com base em seu peso. Dessa forma, todas as solicitações do mesmo IP do cliente podem ser distribuídas para o mesmo servidor. Esse algoritmo é adequado para os protocolos que não aceitam cookies.

## Escolha do algoritmo de balanceamento de carga e configuração do peso
Para permitir que clusters de servidores de back-end realizem negócios de maneira estável em cenários diferentes, alguns casos sobre como escolher o algoritmo de balanceamento de carga e como configurar o peso são fornecidos abaixo, para sua referência.
- Cenário 1:
 1. Suponha que existam três servidores de back-end com a mesma configuração (CPU e memória) e você defina todos os seus pesos como 10, pois eles têm o mesmo desempenho.
 2. 100 conexões TCP foram estabelecidas entre cada servidor de back-end e o cliente, e um novo servidor de back-end foi adicionado.
 3. Nesse cenário, é recomendável usar o algoritmo de programação de conexão mínima, que pode aumentar rapidamente a carga do 4º servidor de back-end e reduzir a pressão nos outros 3.
- Cenário 2:
 1. Suponha que você esteja usando os serviços do Tencent Cloud pela primeira vez e que seu site tenha sido criado com carga baixa. É recomendável adquirir servidores de back-end com a mesma configuração, pois são todos servidores de camada de acesso equivalentes.
 2. Nesse cenário, você pode definir os pesos de todos os servidores de back-end como o valor padrão de 10 e usar o algoritmo de programação de round-robin ponderado para distribuir o tráfego.
- Cenário 3:
 1. Suponha que você tenha cinco servidores de back-end que realizam solicitações de acesso simples a páginas estáticas, e a proporção da capacidade de computação (calculada pela CPU e memória) desses servidores seja 9:3:3:3:1.
 2. Nesse cenário, você pode definir o peso dos servidores de back-end para 90, 30, 30, 30 e 10, respectivamente. Como a maioria das solicitações de acesso a páginas da web estáticas são do tipo de conexão não persistente, você pode usar o algoritmo de programação de round-robin ponderado, para que a instância do CLB possa alocar solicitações com base na taxa de desempenho dos servidores.
- Cenário 4:
 1. Suponha que você tenha dez servidores de back-end para realizar muitas solicitações de acesso à web e não deseja adquirir mais servidores, pois isso aumentará as despesas, e um dos servidores reinicia com frequência devido à sobrecarga.
 2. Nesse cenário, é recomendável definir os pesos dos servidores existentes com base no desempenho deles e definir um peso relativamente pequeno para servidores com alta carga. Além disso, você pode usar o algoritmo de programação de conexão mínima para alocar solicitações a servidores de back-end com menos conexões ativas, a fim de evitar a sobrecarga do servidor.　
- Cenário 5:
 1. Suponha que você tenha três servidores de back-end para processar algumas conexões persistentes, e que a proporção da capacidade de computação (calculada pela CPU e memória) desses servidores seja 3:1:1.
 2. O servidor com o melhor desempenho processa mais solicitações, mas você não quer que ele fique sobrecarregado e deseja alocar solicitações novas para servidores inativos.
 3. Nesse cenário, você pode usar o algoritmo de programação de conexão mínima e reduzir de forma apropriada o peso do servidor ocupado, de modo que a instância do CLB possa alocar solicitações para servidores de back-end com menos conexões ativas, conseguindo alcançar o balanceamento de carga.
- Cenário 6:
 1. Suponha que você queira que as solicitações posteriores do cliente sejam alocadas ao mesmo servidor. A programação de round-robin ponderado ou de conexão mínima ponderada não pode garantir que as solicitações do mesmo cliente sejam alocadas para o mesmo servidor.
 2. Para satisfazer os requisitos de seu servidor de aplicativos específico e manter a "aderência" (ou "continuidade") das sessões do cliente, você pode usar o ip_hash para distribuir o tráfego. Esse algoritmo pode garantir que todas as solicitações do mesmo cliente sejam distribuídas para o mesmo servidor de back-end, a menos que a quantidade de servidores mude ou que o servidor fique indisponível.
