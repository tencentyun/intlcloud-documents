
## Visão geral do faturamento do CBS[](id:CBS)
### Modos de faturamento
O Cloud Block Storage é um serviço de armazenamento em nuvem com pagamento conforme o uso que é fornecido pelo Tencent Cloud.
Consulte a tabela abaixo para obter mais detalhes.

| Plano de faturamento | Pagamento conforme o uso |
|---------|---------|
| Método de pagamento | Um depósito equivalente à taxa de uma hora é solicitado no momento da compra. Esse serviço é faturado por hora. |
| Preços | USD/GB\*hora |
| Duração mínima de uso | Cobrada por segundo e faturada por hora. Você pode adquirir ou cancelar o serviço a qualquer momento. |
| Casos de uso | Este serviço se aplica aos cenários em que a demanda da empresa varia muito, como ofertas relâmpago de comércio eletrônico. |

### Preço
O preço varia por região e por tipo de disco. Para obter mais informações, consulte [Visão geral dos preços](https://intl.cloud.tencent.com/document/product/362/2413).


## Visão geral do faturamento de snapshots[](id:Snapshot)
O serviço de snapshot foi **comercializado** em 22 de janeiro de 2019 às 00:00:00. Todos os snapshots foram faturados com base no uso do armazenamento.
>! [Imagens](https://intl.cloud.tencent.com/document/product/213/4940) usam o serviço de snapshot do CBS para armazenamento de dados. Por isso, manter imagens personalizadas ocupa uma determinada parcela da capacidade do seu snapshot e gera custos.

### Modos de faturamento
Você será cobrado de acordo com o tamanho do armazenamento total dos seus snapshots. Cada região será cobrada separadamente. A taxa do CBS é **paga conforme o uso** em um ciclo de faturamento por hora.
>?Para ver o tamanho dos seus snapshots em cada região, acesse o [Console de snapshots](https://console.cloud.tencent.com/cvm/snapshot/overview).
>





### Preço
O preço dos snapshots varia conforme a região. Para obter mais informações, consulte [Visão geral dos preços](https://intl.cloud.tencent.com/document/product/362/2413).

### Nível gratuito
O Tencent Cloud disponibiliza 50 GB de espaço de armazenamento gratuitamente para usuários da China continental. A política detalhada está descrita abaixo:
- O nível gratuito está disponível para usuários das regiões indicadas no [Console de snapshots](https://console.cloud.tencent.com/cvm/snapshot/overview).
- Esse nível gratuito será encerrado em outubro de 2021.

A tabela a seguir descreve como o armazenamento de snapshots é faturado conforme diferentes circunstâncias:

<table>
     <tr>
         <th>Região</th>  
         <th nowrap="nowrap">Tamanho total do snapshot</th>  
				 <th nowrap="nowrap">Número de discos em nuvem</th>
				 <th>Detalhes</th>
     </tr>
	 <tr>
         <td nowrap="nowrap">Norte da China (Pequim)</td>
         <td>100 GB</td>
				 <td nowrap="nowrap">1 disco em nuvem</td>
				 <td>Elegível para o nível gratuito de 50 GB. O tamanho de armazenamento total faturável do snapshot é de 100 GB - 50 GB = 50 GB.</td>
     </tr> 
	 <tr>
         <td nowrap="nowrap">Hong Kong, Macau e Taiwan, China (Hong Kong)</td>
         <td>60 GB</td>
				 <td>2 discos em nuvem</td>
				 <td>Elegível para o nível gratuito de 50 GB. O tamanho de armazenamento total faturável do snapshot é de 60 GB - 50 GB = 10 GB.</td>
     </tr>
	 <tr>
         <td nowrap="nowrap">Sudeste da Ásia (Singapura)</td>
         <td>40 GB</td>
				 <td>1 disco em nuvem</td>
				 <td>Não é elegível para o nível gratuito. O tamanho de armazenamento total faturável do snapshot é de 40 GB.</td>
     </tr>
</table>

### Pagamento em atraso
Após sua conta entrar em débito, os snapshots apresentarão o status **Isolated (Isolado)**, e o serviço será suspenso. Para obter mais informações, consulte [Política de atraso](https://intl.cloud.tencent.com/document/product/362/31625).

