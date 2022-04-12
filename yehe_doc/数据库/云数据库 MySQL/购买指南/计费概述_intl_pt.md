>?Agora, este produto disponibiliza a consulta dinâmica de preços e a estimativa de custos. Você pode usar a [Calculadora de preços](https://intl.cloud.tencent.com/pricing/cdb) para obter uma estimativa das taxas.

## Modos de faturamento

Agora, o TencentDB for MySQL fornece o modo de faturamento de assinatura mensal. O preço de pagamento conforme o uso permanece inalterado.



O TencentDB for MySQL permite o faturamento separado de memória e discos para fornecer aos usuários opções mais flexíveis.

Fórmula de preço da instância: Preço da instância = taxa de memória + taxa de armazenamento






## Funcionalidades avançadas

### Capacidade de backup

A capacidade de backup não permite a assinatura mensal. Consulte os preços de pagamento conforme o uso.

**Gerenciamento de renovação de instância**

As opções de renovação em lote, renovação automática, data de expiração coletiva, sinalizador de não renovação podem ser encontradas na página **Renewal Management (Gerenciamento de renovação)**.



**Fórmula de custo de upgrade de instância**

Suponha que uma instância expire em T dias, e a diferença de taxa mensal pré-paga entre a configuração de destino e a configuração atual seja C, então o custo total do upgrade será: T/30 x C.

Suponha que você tenha uma instância com 1 núcleo, 1.000 MB de memória e 100 GB de disco (taxa pré-paga: 24,511 USD/mês) e ela expirará em 15 dias. Se você fizer upgrade para 1 núcleo, 1.000 MB de memória e 200 GB de disco (taxa pré-paga: 34,653 USD/mês), então o custo total do upgrade será: 15/30 x (34,653 - 24,511) = 5,071 USD.



**Excedente do limite de capacidade do disco da instância**

Para garantir a continuidade das operações, você precisa fazer upgrade das especificações da instância ou adquirir capacidade de disco adicional antes que a capacidade dele seja totalmente usada.

Quando o tamanho dos dados armazenados em uma instância exceder seu limite de capacidade, a instância será bloqueada e se tornará somente leitura. Você não poderá gravar dados nela. Você precisará expandir sua capacidade ou excluir algumas tabelas de banco de dados no console para desbloqueá-la.

Para evitar que um banco de dados acione o status de bloqueio repetidamente, uma instância bloqueada será desbloqueada e permitida para leituras e gravações somente quando sua capacidade restante disponível for superior a 20% de sua capacidade total ou superior a 50 GB.



**Taxa de sincronização de tráfego para instâncias de recuperação de desastres**

Atualmente, a sincronização de dados das instâncias de recuperação de desastres no TencentDB for MySQL é gratuita.

Notificaremos os usuários quando essa funcionalidade for comercializada.

## Pagamento conforme o uso

O modelo de preços escalonados de pagamento conforme o uso é baseado na duração do uso.

| Duração do uso | Preços escalonados |
|---------|---------|
| 0 horas < duração ≤ 96 horas   | Aplicam-se as taxas de nível 1 |
| 96 horas < duração ≤ 360 horas | Aplicam-se as taxas de nível 2 |
| Duração > 360 horas          | Aplicam-se as taxas de nível 3 |

### Preço da instância

### Fórmula de faturamento
**Taxas totais = taxas de memória + taxas de capacidade de armazenamento + taxas de capacidade de backup + taxas de tráfego (atualmente gratuitas)**

#### Itens faturáveis
<table>
<thead>
<tr>
<th width="15%">Item faturável</th>
<th>Observações</th>
</tr>
</thead>
<tbody><tr>
<td>Taxas de memória<br></td>
<td>A especificação de instância selecionada na página de aquisição é com pagamento conforme o uso e aceita preços escalonados. Para obter os preços detalhados, consulte <a href="https://buy.cloud.tencent.com/price/cdb/overview" target="_blank">Preços dos produtos</a>.</td>
</tr>
<tr>
<td>Taxas de capacidade de armazenamento</td>
<td>A capacidade de disco selecionada na página de aquisição é com pagamento conforme o uso. Para obter os preços detalhados, consulte <a href="https://buy.cloud.tencent.com/price/cdb/overview" target="_blank">Preços dos produtos</a>.<br>A capacidade de armazenamento armazena arquivos de dados, espaços para tabelas compartilhados, logs de erros, logs de refazer, logs de desfazer, dicionários de dados e binlogs necessários para o TencentDB for MySQL.</tr>
<tr>
<td>Taxas de capacidade de backup</td>
<td>O TencentDB for MySQL fornece uma determinada quantidade de capacidade de backup gratuita de acordo com a região, o que equivale à soma da capacidade de armazenamento de todas as instâncias de dois e três nós (incluindo as instâncias de origem) em sua região. <br>Para mais informações sobre as taxas para capacidade excessiva de backup, consulte <a href="https://intl.cloud.tencent.com/document/product/236/32344" target="_blank">Faturamento do espaço de backup</a>.</td>
</tr>
<tr>
<td>Taxas de tráfego</td>
<td>Taxas de tráfego de rede pública (atualmente gratuitas).</td>
</tr>
</tbody></table>


#### Preço com pagamento conforme o uso

##### Edição de alta disponibilidade
<table>
  <td rowspan=2>Região</td>
  <td colspan=3 >Memória (USD/GB/Hora)</td>
  <td rowspan=2 >Disco (USD/GB/Hora)</td>
 </tr>
 <tr  >
  <td >Nível 1</td>
  <td>Nível 2</td>
  <td>Nível 3</td>
 </tr>
 <tr  >
  <td>Guangzhou</td>
  <td class=xl65 align=right>0,0500</td>
  <td class=xl65 align=right>0,0400</td>
  <td class=xl65 align=right>0,0300</td>
  <td class=xl65 align=right>0,0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Qingyuan</td>
  <td class=xl65 align=right>0,0500</td>
  <td class=xl65 align=right>0,0400</td>
  <td class=xl65 align=right>0,0300</td>
  <td class=xl65 align=right>0,0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Xangai</td>
  <td class=xl65 align=right>0,0500</td>
  <td class=xl65 align=right>0,0400</td>
  <td class=xl65 align=right>0,0300</td>
  <td class=xl65 align=right>0,0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Pequim</td>
  <td class=xl65 align=right>0,0500</td>
  <td class=xl65 align=right>0,0400</td>
  <td class=xl65 align=right>0,0300</td>
  <td class=xl65 align=right>0,0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Chengdu</td>
  <td class=xl65 align=right>0,0500</td>
  <td class=xl65 align=right>0,0400</td>
  <td class=xl65 align=right>0,0300</td>
  <td class=xl65 align=right>0,0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Chongqing</td>
  <td class=xl65 align=right>0,0500</td>
  <td class=xl65 align=right>0,0400</td>
  <td class=xl65 align=right>0,0300</td>
  <td class=xl65 align=right>0,0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Hong Kong (China)</td>
  <td class=xl66 align=right>0,0688</td>
  <td class=xl65 align=right>0,0516</td>
  <td class=xl65 align=right>0,0344</td>
  <td class=xl65 align=right>0,0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Taipé (China)</td>
  <td class=xl65 align=right>0,0688</td>
  <td class=xl65 align=right>0,0516</td>
  <td class=xl65 align=right>0,0344</td>
  <td class=xl65 align=right>0,0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Singapura</td>
  <td class=xl65 align=right>0,0705</td>
  <td class=xl65 align=right>0,0528</td>
  <td class=xl65 align=right>0,0352</td>
  <td class=xl65 align=right>0,0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Bangkok</td>
  <td class=xl65 align=right>0,0556</td>
  <td class=xl65 align=right>0,0417</td>
  <td class=xl65 align=right>0,0278</td>
  <td class=xl65 align=right>0,0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Mumbai</td>
  <td class=xl65 align=right>0,0556</td>
  <td class=xl65 align=right>0,0417</td>
  <td class=xl65 align=right>0,0278</td>
  <td class=xl65 align=right>0,0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Seul</td>
  <td class=xl65 align=right>0,0556</td>
  <td class=xl65 align=right>0,0417</td>
  <td class=xl65 align=right>0,0278</td>
  <td class=xl65 align=right>0,0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Tóquio</td>
  <td class=xl65 align=right>0,0556</td>
  <td class=xl65 align=right>0,0417</td>
  <td class=xl65 align=right>0,0278</td>
  <td class=xl65 align=right>0,0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Vale do Silício</td>
  <td class=xl65 align=right>0,0550</td>
  <td class=xl65 align=right>0,0413</td>
  <td class=xl65 align=right>0,0275</td>
  <td class=xl65 align=right>0,0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Virgínia</td>
  <td class=xl65 align=right>0,0444</td>
  <td class=xl65 align=right>0,0333</td>
  <td class=xl65 align=right>0,0222</td>
  <td class=xl65 align=right>0,0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Toronto</td>
  <td class=xl65 align=right>0,0265</td>
  <td class=xl65 align=right>0,0199</td>
  <td class=xl65 align=right>0,0133</td>
  <td class=xl65 align=right>0,0006</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Frankfurt</td>
  <td class=xl65 align=right>0,0550</td>
  <td class=xl65 align=right>0,0413</td>
  <td class=xl65 align=right>0,0275</td>
  <td class=xl65 align=right>0,0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Moscou</td>
  <td class=xl65 align=right>0,0556</td>
  <td class=xl65 align=right>0,0417</td>
  <td class=xl65 align=right>0,0278</td>
  <td class=xl65 align=right>0,0003</td>
 </tr>
 </tr>
</table>

##### Instâncias somente leitura

<table>
  <td rowspan=2>Região</td>
  <td colspan=3 >Memória (USD/GB/Hora)</td>
  <td rowspan=2 >Disco (USD/GB/Hora)</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Nível 1</td>
  <td class=xl1529815>Nível 2</td>
  <td class=xl1529815>Nível 3</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Guangzhou</td>
  <td class=xl6529815 align=right>0,0250</td>
  <td class=xl6529815 align=right>0,0200</td>
  <td class=xl6529815 align=right>0,0150</td>
  <td class=xl6529815 align=right>0,0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Qingyuan</td>
  <td class=xl6529815 align=right>0,0250</td>
  <td class=xl6529815 align=right>0,0200</td>
  <td class=xl6529815 align=right>0,0150</td>
  <td class=xl6529815 align=right>0,0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Xangai</td>
  <td class=xl6529815 align=right>0,0250</td>
  <td class=xl6529815 align=right>0,0200</td>
  <td class=xl6529815 align=right>0,0150</td>
  <td class=xl6529815 align=right>0,0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Pequim</td>
  <td class=xl6529815 align=right>0,0250</td>
  <td class=xl6529815 align=right>0,0200</td>
  <td class=xl6529815 align=right>0,0150</td>
  <td class=xl6529815 align=right>0,0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Chengdu</td>
  <td class=xl6529815 align=right>0,0250</td>
  <td class=xl6529815 align=right>0,0200</td>
  <td class=xl6529815 align=right>0,0150</td>
  <td class=xl6529815 align=right>0,0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Chongqing</td>
  <td class=xl6529815 align=right>0,0250</td>
  <td class=xl6529815 align=right>0,0200</td>
  <td class=xl6529815 align=right>0,0150</td>
  <td class=xl6529815 align=right>0,0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Hong Kong (China)</td>
  <td class=xl6529815 align=right>0,0344</td>
  <td class=xl6529815 align=right>0,0258</td>
  <td class=xl6529815 align=right>0,0172</td>
  <td class=xl6529815 align=right>0,0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Taipé (China)</td>
  <td class=xl6529815 align=right>0,0344</td>
  <td class=xl6529815 align=right>0,0258</td>
  <td class=xl6529815 align=right>0,0172</td>
  <td class=xl6529815 align=right>0,0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Singapura</td>
  <td class=xl6529815 align=right>0,0352</td>
  <td class=xl6529815 align=right>0,0264</td>
  <td class=xl6529815 align=right>0,0176</td>
  <td class=xl6529815 align=right>0,0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Bangkok</td>
  <td class=xl6529815 align=right>0,0278</td>
  <td class=xl6529815 align=right>0,0208</td>
  <td class=xl6529815 align=right>0,0139</td>
  <td class=xl6529815 align=right>0,0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Mumbai</td>
  <td class=xl6529815 align=right>0,0278</td>
  <td class=xl6529815 align=right>0,0208</td>
  <td class=xl6529815 align=right>0,0139</td>
  <td class=xl6529815 align=right>0,0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Seul</td>
  <td class=xl6529815 align=right>0,0278</td>
  <td class=xl6529815 align=right>0,0208</td>
  <td class=xl6529815 align=right>0,0139</td>
  <td class=xl6529815 align=right>0,0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Tóquio</td>
  <td class=xl6529815 align=right>0,0278</td>
  <td class=xl6529815 align=right>0,0208</td>
  <td class=xl6529815 align=right>0,0139</td>
  <td class=xl6529815 align=right>0,0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Vale do Silício</td>
  <td class=xl6529815 align=right>0,0275</td>
  <td class=xl6529815 align=right>0,0206</td>
  <td class=xl6529815 align=right>0,0138</td>
  <td class=xl6529815 align=right>0,0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Virgínia</td>
  <td class=xl6529815 align=right>0,0222</td>
  <td class=xl6529815 align=right>0,0167</td>
  <td class=xl6529815 align=right>0,0111</td>
  <td class=xl6529815 align=right>0,0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Toronto</td>
  <td class=xl6529815 align=right>0,0133</td>
  <td class=xl6529815 align=right>0,0099</td>
  <td class=xl6529815 align=right>0,0066</td>
  <td class=xl6529815 align=right>0,0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Frankfurt</td>
  <td class=xl6529815 align=right>0,0275</td>
  <td class=xl6529815 align=right>0,0206</td>
  <td class=xl6529815 align=right>0,0138</td>
  <td class=xl6529815 align=right>0,0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Moscou</td>
  <td class=xl6529815 align=right>0,0278</td>
  <td class=xl6529815 align=right>0,0208</td>
  <td class=xl6529815 align=right>0,0139</td>
  <td class=xl6529815 align=right>0,0002</td>
 </tr>
</table>


## Exemplos de faturamento
>?Os preços usados nos exemplos a seguir são apenas para fins demonstrativos, e podem variar dependendo das regiões, campanhas ou políticas. Consulte a página de preços para obter os preços reais.
>

### Assinatura mensal
Suponha que:
- Você comprou uma instância do TencentDB for MySQL de alta disponibilidade com assinatura mensal com 4 núcleos, 8.000 MB de memória e 500 GB de espaço em disco na Zona 3 de Guangzhou por 1 mês.
- Você comprou uma instância do TencentDB for MySQL de alta disponibilidade com assinatura mensal com 4 núcleos, 8.000 MB de memória e 200 GB de espaço em disco na Zona 4 de Guangzhou por 1 mês.

Taxas totais = taxas de memória + taxas de capacidade de armazenamento + taxas de capacidade de backup

##### Taxas de memória e taxas de capacidade de armazenamento
Fórmula de cálculo:
Taxas de memória + taxas de capacidade de armazenamento = 2 x 114,93 USD/mês + (500 GB + 200 GB) x 0,1014 USD/GB/mês x 1 mês = 300,84 USD

##### Taxas de capacidade de backup
A instância do TencentDB for MySQL de alta disponibilidade na Zona 3 de Guangzhou tem capacidade de armazenamento de 500 GB por mês, e a da Zona 4 de Guangzhou tem capacidade de armazenamento de 200 GB por mês, então você pode ter capacidade de backup de 700 GB gratuitamente na região de Guangzhou todo mês.

O uso da capacidade de backup que exceder o nível gratuito será calculado por hora de acordo com a regra a seguir. Por exemplo, se os backups de dados atingirem 800 GB e os backups de logs atingirem 100 GB, o uso total da capacidade de backup em Guangzhou excederá 700 GB, e sua capacidade de backup faturável por hora será de 200 GB (800 + 100 - 700 = 200).

Taxas de capacidade de backup (por hora) = 200 GB (o uso da capacidade de backup que excede o nível gratuito pode mudar com o tempo) x 0,000127 USD/GB/hora

### Pagamento conforme o uso
Suponha que você adquiriu uma instância do TencentDB for MySQL com pagamento conforme o uso com 4 núcleos, 8.000 MB de memória e 500 GB de espaço em disco na região de Guangzhou por 400 horas.
Taxas de nível 1: (0,0250 USD/GB/hora * 8 GB + 500 GB * 0,0003) * 96 horas = 33,6 USD
Taxas de nível 2: (0,0200 USD/GB/hora * 8 GB + 500 GB * 0,0003) * 264 horas = 81,84 USD
Taxas de nível 3: (0,0150 USD/GB/hora * 8 GB + 500 GB * 0,0003) * 40 horas = 10,8 USD
Taxas da instância = taxas de nível 1 + taxas de nível 2 + taxas de nível 3 = 126,24 USD

## Perguntas frequentes
#### Por que foram cobradas taxas adicionais para a minha instância de assinatura mensal?
O uso da capacidade de backup que exceder o nível gratuito será cobrado. Verifique se o uso da capacidade de backup excedeu o nível gratuito.
Você pode verificar o uso da capacidade de backup na página **Database Backup (Backup de banco de dados)** no [Console do TencentDB for MySQL](https://console.cloud.tencent.com/cdb/backup). Para mais informações sobre os preços da capacidade de backup, consulte [Faturamento do espaço de backup](https://intl.cloud.tencent.com/document/product/236/32344).

#### A Tencent Cloud cobrará por instâncias com pagamento conforme o uso se estiverem ociosas?
Sim. Se você terminar de usar os recursos com pagamento conforme o uso, encerre-os o mais rápido possível para evitar taxas adicionais.

#### Quais arquivos são armazenados na capacidade de armazenamento?

- Arquivos de dados: o espaço que os seus dados ocupam, incluindo as tabelas e os índices criados
- Arquivos de sistema (necessários para o banco de dados): espaços para tabelas compartilhados, logs de erros, logs de refazer, logs de desfazer e dicionários de dados
- Binlogs: os binlogs registram todas as instruções DDL e DML (exceto as instruções SELECT e SHOW) e são usados para replicar e restaurar os dados do banco de dados. Quanto mais dados forem alterados, mais binlogs. Para reduzir o espaço ocupado pelos binlogs, eles podem ser carregados no COS.

## Documentação
- Você pode adquirir instâncias do TencentDB for MySQL por meio do console ou de API. Para mais informações, consulte [Métodos de aquisição](https://intl.cloud.tencent.com/document/product/236/5160).
- O TencentDB for MySQL enviará mensagens de alerta para você antes que ele expire e seus recursos sejam reavidos. Para mais informações, consulte [Pagamento em atraso](https://intl.cloud.tencent.com/document/product/236/5159).
- Você pode devolver as instâncias do TencentDB for MySQL e solicitar um reembolso. Para mais informações, consulte [Reembolso](https://intl.cloud.tencent.com/document/product/236/14618).
- Você pode ajustar as instâncias do TencentDB for MySQL para uma especificação superior ou inferior. Para mais informações, consulte [Taxa de ajuste de instância](https://intl.cloud.tencent.com/document/product/236/32345).
