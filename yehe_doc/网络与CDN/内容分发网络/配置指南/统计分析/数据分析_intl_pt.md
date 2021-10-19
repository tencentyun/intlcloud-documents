A página **Data Analysis (Análise de dados)** exibe vários tipos de gráficos, analisando as fontes do usuário com base nos registros de acesso para ajudá-lo a entender a distribuição dos usuários e o uso empresarial.

Faça login no [console do CDN](https://console.cloud.tencent.com/cdn) e selecione **Statistics (Estatísticas)** > **Data Analysis (Análise de dados)** na barra lateral esquerda para acessar a página **Data Analysis (Análise de dados)**.

- É possível consultar os dados gerados em um período máximo de 31 dias. Os dados históricos são retidos por 90 dias.
- É possível consultar os dados históricos gerados nos últimos três meses.


## Solicitações de acesso de IP exclusivo
A quantidade de solicitações de acesso de IP exclusivo no período especificado é calculada eliminando cópias duplicadas dos IPs do cliente de acesso no log:
<li>Se o intervalo de tempo for menor ou igual a um dia, será fornecida uma curva de IPs desduplicados com uma granularidade de 5 minutos.</li>
<li> As estatísticas de nomes de domínio são contabilizadas desduplicando a quantidade ativa em um dia inteiro. Se houver vários nomes de domínio, projetos ou contas, as estatísticas são contabilizadas acumulando a quantidade ativa diária de cada um com uma granularidade de 5 minutos.</li>
<img src="https://main.qcloudimg.com/raw/bed86e21420fe337d6b0587090fe4b64.png" alt>


## Distribuição dos distritos de acesso dos usuários
O distrito do solicitante de acesso pode ser identificado por meio do IP do cliente de origem, que pode ser exibido em um mapa ou em uma lista, permitindo que você visualize a distribuição distrital de seus usuários.
![](https://main.qcloudimg.com/raw/d89e4321c94499833d04841c7e5e3597.png)

## Distribuição de ISPs dos usuários
O ISP do solicitante de acesso pode ser identificado por meio do IP do cliente de origem, que pode ser exibido em um gráfico circular ou em uma lista, permitindo que você visualize a distribuição de ISPs de seus usuários.
![](https://main.qcloudimg.com/raw/b6fa25e2fb72dbcd02e11fae43e888ed.png)
