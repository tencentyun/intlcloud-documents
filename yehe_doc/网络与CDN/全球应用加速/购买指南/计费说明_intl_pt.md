A taxa de serviço do GAAP consiste em itens básicos e itens de valor agregado. (Para mais informações sobre o faturamento de outros serviços da Tencent Cloud, consulte a documentação relacionada ou [entre em contato conosco](https://intl.cloud.tencent.com/document/product/608/42346).

>? As taxas do serviço GAAP em todas as regiões da China Continental são faturadas coletivamente em Guangzhou. Para as regiões fora da China Continental, as taxas são faturadas coletivamente em Singapura.

## Itens faturáveis básicos
A tabela a seguir lista os itens faturáveis básicos e os modos de pagamento:

|Item | Modo de pagamento |
|--|--|
|Taxa de conexão| Pagamento conforme o uso diário |
|Taxa de largura de banda| Pagamento conforme o uso diário|

### Taxa de conexão

A taxa de conexão se refere ao custo dos recursos (servidor, IP etc.) usados para criar uma conexão de aceleração. A taxa está relacionada à especificação da conexão (quantidade de conexões simultâneas/largura de banda). Cada conexão de aceleração é faturada de forma separada e diariamente. Consulte os detalhes abaixo:

<table>
<thead>
<tr>
<th colspan="12"  style="text-align: center">Preços de conexão de aceleração<strong> (Unidade: USD/dia)</strong></th>
</tr>
</thead>
<tbody><tr>
<th>Quantidade de conexões simultâneas/largura de banda</th>
<th>10 Mbps</th>
<th>20 Mbps</th>
<th>50 Mbps</th>
<th>100 Mbps</th>
<th>200 Mbps</th>
<th>500 Mbps</th>
<th>1.000 Mbps</th>
<th>2.000 Mbps</th>
<th>5.000 Mbps</th>
<th>8.000 Mbps</th>
<th>10.000 Mbps</th>
</tr>
<tr>
<td >20K</td>
<td>12,8</td>
<td>12,8</td>
<td>12,8</td>
<td>12,8</td>
<td>12,8</td>
<td>12,8</td>
<td>12,8</td>
<td>25,6</td>
<td>64</td>
<td>102,4</td>
<td>128</td>
</tr>
<tr>
<td>50K</td>
<td>19,2</td>
<td>19,2</td>
<td>19,2</td>
<td>19,2</td>
<td>19,2</td>
<td>19,2</td>
<td>19,2</td>
<td>25,6</td>
<td>64</td>
<td>64.512</td>
<td>128</td>
</tr>
<tr>
<td>100K</td>
<td>32</td>
<td>32</td>
<td>32</td>
<td>32</td>
<td>32</td>
<td>32</td>
<td>32</td>
<td>32</td>
<td>64</td>
<td>102,4</td>
<td>128</td>
</tr>
<tr>
<td>200K</td>
<td>64</td>
<td>64</td>
<td>64</td>
<td>64</td>
<td>64</td>
<td>64</td>
<td>64</td>
<td>64</td>
<td>64</td>
<td>102,4</td>
<td>128</td>
</tr>
<tr>
<td>300K</td>
<td>96</td>
<td>96</td>
<td>96</td>
<td>96</td>
<td>96</td>
<td>96</td>
<td>96</td>
<td>96</td>
<td>96</td>
<td>102,4</td>
<td>128</td>
</tr>
<tr>
<td>400K</td>
<td>128</td>
<td>128</td>
<td>128</td>
<td>128</td>
<td>128</td>
<td>128</td>
<td>128</td>
<td>128</td>
<td>128</td>
<td>128</td>
<td>128</td>
</tr>
<tr>
<td>500K</td>
<td>160</td>
<td>160</td>
<td>160</td>
<td>160</td>
<td>160</td>
<td>160</td>
<td>160</td>
<td>160</td>
<td>160</td>
<td>160</td>
<td>160</td>
</tr>
<tr>
<td>600K</td>
<td>192</td>
<td>192</td>
<td>192</td>
<td>192</td>
<td>192</td>
<td>192</td>
<td>192</td>
<td>192</td>
<td>192</td>
<td>192</td>
<td>192</td>
</tr>
<tr>
<td>700K</td>
<td>224</td>
<td>224</td>
<td>224</td>
<td>224</td>
<td>224</td>
<td>224</td>
<td>224</td>
<td>224</td>
<td>224</td>
<td>224</td>
<td>224</td>
</tr>
<tr>
<td>800K</td>
<td>256</td>
<td>256</td>
<td>256</td>
<td>256</td>
<td>256</td>
<td>256</td>
<td>256</td>
<td>256</td>
<td>256</td>
<td>256</td>
<td>256</td>
</tr>
<tr>
<td>900K</td>
<td>288</td>
<td>288</td>
<td>288</td>
<td>288</td>
<td>288</td>
<td>288</td>
<td>288</td>
<td>288</td>
<td>288</td>
<td>288</td>
<td>288</td>
</tr>
<tr>
<td>1000K</td>
<td>320</td>
<td>320</td>
<td>320</td>
<td>320</td>
<td>320</td>
<td>320</td>
<td>320</td>
<td>320</td>
<td>320</td>
<td>320</td>
<td>320</td>
</tr>
</tbody></table>


#### Cálculo e dedução
- A taxa de conexão gerada entre 00:00:00 e 23:59:59 (UTC+8) de um dia é faturada antes das 18:00 do dia seguinte (UTC+8).
- A taxa de conexão é faturada sempre que você cria uma conexão, incluindo a criação de novas e a recriação de antigas. 
- A especificação de conexão pode ser alterada uma vez por dia. A taxa de conexão do dia é calculada de acordo com a última especificação modificada.
>? Quando uma conexão é desativada, a taxa de largura de banda é interrompida. Mas a taxa de conexão continua. Você precisa excluir a conexão para interromper a cobrança da taxa de conexão.
#### Exemplo de faturamento

Suponha que um usuário crie uma conexão de aceleração Pequim-Singapura em 1º de janeiro, ajuste a especificação da conexão e a exclua às 18:00 de 4 de janeiro. A taxa de conexão é calculada da seguinte forma:

| **Data** | **ID do recurso**    | **Conexões máximas (10K)** | **Largura de banda máxima (Mbps)** | **Taxa de conexão (USD)** |
|-|-|-|-|-|
| 1º de janeiro de 2021 | link-0tisfsxz | 2                 | 10                   | 12,8              |
| 2 de janeiro de 2021 | link-0tisfsxz | 30                | 50                   | 96                |
| 3 de janeiro de 2021 | link-0tisfsxz | 10                | 20                   | 32                |
| 4 de janeiro de 2021 | link-0tisfsxz | 40                | 20                   | 128               |

## Taxa de largura de banda
A taxa de largura de banda se refere ao custo da largura de banda consumida por conexões de aceleração e grupos de conexões de aceleração. Cada conexão de aceleração é faturada de forma separada e diariamente, de acordo com o intervalo de níveis correspondente à largura de banda de pico real usando os seguintes preços em níveis.

| **Nível da largura de banda**                 | **USD/Mbps/dia** |
|--|--|
| < 20 Mbps                     | 20,63            |
| 20 a 100 Mbps (excluindo 100 Mbps)    | 14,29            |
| 100 a 500 Mbps (excluindo 500 Mbps)   | 11,11            |
| 500 a 2.000 Mbps (excluindo 2.000) | 9,52             |
| ≥ 2.000 Mbps                   | 7,94             |

#### Cálculo e dedução

- A taxa de largura de banda gerada entre 00:00:00 e 23:59:59 (UTC+8) de um dia é faturada antes das 18:00 do dia seguinte (UTC+8).
- A largura de banda de entrada e saída da conexão é coletada a cada minuto. O valor mais alto entre todas as amostras coletadas é a largura de banda faturável.

#### Exemplo de faturamento
Suponha que um usuário crie uma conexão de aceleração Pequim-Singapura em 1º de janeiro, ajuste a especificação da conexão e a exclua às 18:00 de 4 de janeiro. A taxa de largura de banda é calculada da seguinte forma:

| **Data** | **ID do recurso**    | **Largura de banda de pico (Mbps)** | **Fórmula** | **Taxa de largura de banda (USD)** |
|--|--|--|--|--|
| 1º de janeiro de 2021 | link-0tisfskk | 7                    | =7×20,63     | 144,41            |
| 2 de janeiro de 2021 | link-0tisfskk | 28                   | =28×14,29    | 400,12            |
| 3 de janeiro de 2021 | link-0tisfskk | 158                  | =158×11,11   | 1.755,38           |
| 4 de janeiro de 2021 | link-0tisfskk | 150                  | =500×9,52    | 4.760              |

###  


## Item faturável de valor agregado

A taxa de rede BGP dedicada é cobrada se você tiver usado uma rede BGP dedicada (Hong Kong) para aceleração do GAAP.

Taxa de rede BGP dedicada = Largura de banda de pico diária × Preço de tabela (3 USD/Mbps/dia)

#### Exemplo de faturamento
Suponha que um usuário crie uma conexão Hong Kong-Singapura pela rede BGP dedicada em 1º de janeiro e a exclua em 4 de janeiro. A taxa é calculada da seguinte forma:

| **Data** | **ID do recurso**   | **Largura de banda de pico (Mbps)** | **Fórmula** | **Taxa da rede BGP dedicada (USD)** |
|-|-|-|-|-|
| 1º de janeiro de 2021 | link-1tifgbp | 7                    | =7×3         | 21                   |
| 2 de janeiro de 2021 | link-1tifgbp | 28                   | =28×3        | 84                   |
| 3 de janeiro de 2021 | link-1tifgbp | 25                   | =25×3        | 75                   |
| 4 de janeiro de 2021 | link-1tifgbp | 50                   | =50×3        | 150                  |

