Você pode verificar a distribuição do usuário final e o uso de recursos na página **Data Analysis (Análise de dados)**.

Faça login no [console do CDN](https://console.cloud.tencent.com/cdn) e selecione **Statistics (Estatísticas)** > **Data Analysis (Análise de dados)** na barra lateral esquerda para acessar a página **Data Analysis (Análise de dados)**.

O período máximo de consulta é de 31 dias. Os dados históricos são retidos por 90 dias.
- É possível consultar os dados de histórico gerados nos últimos três meses.

>! No momento, o ECDN não permite a exibição da quantidade de solicitações de acesso de IP exclusivo e da distribuição da região de acesso do usuário.

## Visão geral de dados

Exibição da visão geral dos dados em sua dimensão de relatório especificada. 
A visão geral dos dados varia de acordo com o método de cobrança.
Para faturamento por tráfego, o tráfego total, a taxa média de acertos de tráfego e o total de solicitações são exibidos.
Para faturamento por largura de banda, largura de banda de pico, largura de banda de pull de origem de pico e solicitações totais são exibidas. 


## Distribuição dos distritos de acesso dos usuários

A distribuição do distrito de acesso do usuário é exibida em sua dimensão de relatório especificada. Com base no IP do cliente de origem, o distrito de acesso do usuário pode ser determinado e exibido em um mapa ou lista, permitindo visualizar a distribuição do distrito de seus usuários. Você pode visualizar estatísticas de províncias na China continental e regiões fora da China continental.


## Tráfego

Exibição da curva de tráfego em sua dimensão de relatório especificada. É possível escolher a visualização da curva de tráfego faturado ou de tráfego de pull de origem.


## Largura de banda

Exibição da curva de largura de banda em sua dimensão de relatório especificada. É possível escolher a visualização da curva de largura de banda faturável ou de largura de banda de pull de origem. A curva de largura de banda de pico é permitida.


## Solicitações

Exibição da curva de solicitações totais em sua dimensão de relatório especificada.


## Códigos de erro

Exibição dos números e proporções de códigos de erro em sua dimensão de relatório especificada.


## 10 URLs principais

Exibição dos 10 URLs principais em sua dimensão de relatório especificada. É possível classificá-los por uso ou solicitações totais.


## 10 projetos principais

Exibição dos dez projetos principais em sua dimensão de relatório especificada.

## 10 nomes de domínio principais

Exibição dos 10 principais nomes de domínio em sua dimensão de relatório especificada.

## Solicitações de acesso de IP exclusivo

As solicitações de acesso de IP exclusivo no período especificado são calculadas eliminando cópias duplicadas dos IPs do cliente de acesso no log:
Se o intervalo de tempo for menor ou igual a um dia, será fornecida uma curva de IPs desduplicados com uma granularidade de 5 minutos.
As estatísticas de nomes de domínio são contadas desduplicando a quantidade ativa em um dia inteiro. Se houver vários nomes de domínio, projetos ou contas, as estatísticas são contabilizadas acumulando a quantidade ativa diária de cada um com uma granularidade de 5 minutos.
>! Apenas os dados dos últimos 30 dias podem ser consultados.



## Distribuição de ISPs de usuários

Com base no IP do cliente de origem, o ISP do usuário pode ser determinado e exibido em um gráfico de pizza ou lista, permitindo que você visualize a distribuição de ISPs de seus usuários.

