Este documento descreve os preços da rede pública em diferentes modos de faturamento e ajuda você a escolher o plano de faturamento que melhor atenda à sua empresa.

## Faturamento por tráfego
>? As taxas são pagas conforme o uso em um ciclo de faturamento por hora com base no tráfego da rede pública usado. O faturamento por tráfego é adequado para cenários em que o pico de tráfego da empresa flutua muito em momentos variados.

**Preços**
<table>
<thead>
<tr>
<th>Região</th>
<th>Preço (unidade: USD/GB)</th>
</tr>
</thead>
<tbody><tr>
<td>China Continental (sem incluir Hong Kong, Macau e Taiwan), Seul, Hong Kong (China), Jacarta</td>
<td>0,12</td>
</tr>
<tr>
<td>Tóquio</td>
<td>0,13</td>
</tr>
<tr>  
<td>Singapura</td>
<td>0,081</td>
</tr>
<tr>
<td>São Paulo</td>
<td>0,15</td>
</tr>
<tr> 
<td>Toronto, Vale do Silício, Frankfurt</td>
<td>0,077</td>
</tr>
<tr>
<td>Bangkok, Mumbai</td>
<td>0,1</td>
</tr>
<tr> 
<td>Virgínia</td>
<td>0,075</td>
</tr>
<tr>  
</tbody></table>


**Exemplo de faturamento**
Suponha que você adquira um EIP na região de Seul com o modo de faturamento por tráfego e use um total de 10 GB de tráfego entre 07:00:00 e 07:59:59, então às 8:00:00, as taxas a pagar serão: 0,12 USD/GB × 10 GB = 1,2 USD.

> ?
> - As unidades de tráfego são baseadas em 1.024. Por exemplo, 1 TB = 1.024 GB e 1 GB = 1.024 MB.
> - O tráfego da rede pública se refere ao tráfego downstream (em bytes), que são os dados da camada de aplicativo. Durante a transferência de dados real, o tráfego gerado na rede é cerca de 5 a 15% maior do que o tráfego da camada de aplicativo, então o tráfego calculado pelo Tencent Cloud pode ser cerca de 10% a mais do que o calculado pelos próprios usuários no servidor.
> - Consumo por cabeçalhos TCP/IP: em solicitações HTTP baseadas em TCP/IP, cada pacote tem um tamanho máximo de 1.500 bytes e inclui cabeçalhos TCP e IP de 40 bytes, que geram tráfego durante a transferência, mas não podem ser contados pela camada de aplicativo. O custo dessa parte é de cerca de 3%.
> - Retransmissão TCP: durante a transferência normal de dados pela rede, cerca de 3 a 10% dos pacotes são perdidos na internet e retransmitidos pelo servidor. Esse tipo de tráfego, que representa de 3 a 7% do tráfego total, não pode ser contado na camada de aplicativo.


## Pacote de largura de banda
O Tencent Cloud Bandwidth Package (BWP) é um método de faturamento agregado de vários IPs. Este modo economiza muito as taxas de rede pública quando suas instâncias de rede pública têm picos de tráfego em momentos diferentes.
Para obter os preços detalhados, consulte os [Modos de faturamento](https://intl.cloud.tencent.com/document/product/684/15255).


## Referência
- [Faturamento da rede pública](https://intl.cloud.tencent.com/document/product/213/10578)
- [Limite de largura de banda da rede pública](https://intl.cloud.tencent.com/document/product/213/12523)
