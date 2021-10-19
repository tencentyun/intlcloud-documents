### O CDN pode ser faturado pela quantidade de solicitações?
Não. Atualmente, o CDN não aceita o faturamento pela quantidade de solicitações.

### O que acontecerá se minha conta estiver com pagamento em atraso?
Para obter mais informações, consulte a seção [Em atraso](https://intl.cloud.tencent.com/document/product/228/2949#.E6.AC.A0.E8.B4.B9.E8.AF.B4.E6.98.8E) no documento de descrição do faturamento.

### Se o servidor de origem usar o COS, serei cobrado pelo tráfego gerado pelo pull de origem do CDN para o COS?
Não. O tráfego gerado pelo pull de origem do CDN para o COS é faturado pelo COS em vez do CDN. Para obter mais informações, consulte [COS como um servidor de origem do CDN](https://intl.cloud.tencent.com/document/product/228/32977).

### Quando o CDN for desabilitado (ou desativado), ele vai gerar tráfego e incorrer em taxas?
Depois que o serviço de aceleração de nome de domínio do CDN for desabilitado, se o nome de domínio ainda estiver configurado com o CNAME, um código de status 404 será retornado para solicitações resolvidas para o nó e uma pequena quantidade de tráfego será consumida. O console registrará esses dados de tráfego para sua referência. Os logs correspondentes também serão gerados. No entanto, como seu serviço de aceleração de nome de domínio foi desabilitado, você não será faturado por esse consumo de tráfego e pacotes de log. Recomendamos que você modifique a resolução de pull de origem primeiro, antes de desabilitar o serviço de aceleração.

### Como eu altero o modo de faturamento do CDN?

Se você achar que o modo de faturamento escolhido não é adequado para suas condições empresariais reais (para obter mais informações sobre como escolher o modo de faturamento adequado para você, consulte [Visão geral do faturamento](https://intl.cloud.tencent.com/document/product/228/2949#.E8.AE.A1.E8.B4.B9.E6.96.B9.E5.BC.8F.E9.80.89.E6.8B.A9)), você pode alterá-lo seguindo as etapas abaixo:
1. Faça login no [Console do CDN](https://console.cloud.tencent.com/cdn), acesse a página de visão geral do serviço e clique em **Change (Alterar)** na seção de modo de faturamento à direita.
![](https://main.qcloudimg.com/raw/38b82d3d166970552437b5525b74c44f.png)
2. Altere o modo de faturamento original de **Bill by Traffic (Faturamento por tráfego)** para **Bill by Bandwidth (Faturamento por largura de banda)**.
![](https://main.qcloudimg.com/raw/6fd1575557d0c4b7b06be9f1fc30e1da.png)
3. Depois de alterar o modo de faturamento para **Bill by Bandwidth (Faturamento por largura de banda)**, a cobrança pelo consumo total gerado na data atual será faturada e deduzida no dia seguinte.

### Se o servidor de origem usar o CVM, serei cobrado pelo tráfego gerado pelo pull de origem do CDN para o CVM?

Não. O CDN não cobra por esse tipo de tráfego.

### Qual é a taxa de conversão de Gbps para Mbps no faturamento do CDN?

No faturamento do CDN, 1 Gbps = 1.000 Mbps, 1 Mbps = 1.000 Kbps e 1 Kbps = 1.000 bps.

### Somente o tráfego downstream é faturado no CDN?

Sim. O CDN cobra apenas pelo tráfego downstream, não o upstream.


### Como o CDN é faturado?

O CDN oferece dois métodos de faturamento: faturamento por largura de banda e faturamento por tráfego (padrão). Ambos os métodos são com pagamento conforme o uso em um ciclo de faturamento diário. O pagamento do consumo total gerado entre 00:00:00 e 23:59:59 da data vigente será deduzido antes das 18:00 do dia seguinte. Para obter mais informações sobre como escolher um método de faturamento adequado, consulte [Visão geral do faturamento](https://intl.cloud.tencent.com/document/product/228/2949).

### Quando as taxas do CDN são deduzidas?

O CDN tem um faturamento pós-pago. A cobrança pelo consumo total gerado no dia atual é faturada e deduzida no dia seguinte.

- Se você mudar de faturamento por largura de banda para faturamento por tráfego e o consumo ainda não tiver ocorrido durante o dia, você será cobrado no modo de faturamento por tráfego no dia seguinte, a menos que mude o modo de faturamento novamente.
- Caso o consumo já tenha ocorrido, será cobrado o valor do faturamento por largura de banda no dia seguinte. Você será cobrado com o faturamento por tráfego no terceiro dia ao calcular o consumo no segundo dia, a menos que você mude o modo de faturamento novamente.

Se suas taxas de serviço do CDN mensais excederem ou espera-se que excedam US$ 20.000, você poderá se qualificar para um plano de faturamento mensal mais flexível e econômico. Para obter mais informações, envie um tíquete para entrar em contato com a equipe de vendas.

### O que é faturamento 95º percentil mensal?

O faturamento por largura de banda é um método de faturamento baseado no uso da largura de banda de pico.
95º percentil mensal: existem 288 pontos estatísticos de largura de banda do CDN por dia. A partir do primeiro dia do mês vigente, todos os pontos estatísticos de dias válidos (quando a largura de banda é realmente consumida) são classificados em ordem. Os 5% dos pontos estatísticos mais altos são removidos e o valor mais alto restante é a largura de banda faturável. A taxa é então calculada com base no preço de tabela e no modo de liquidação.

> Amostra de faturamento:
> Suponha que o faturamento de um cliente tenha iniciado oficialmente em 1º de janeiro e o preço contratado seja P USD/Mbps/mês.
> Suponha que haja 14 dias válidos em janeiro e a largura de banda faturável para todos os 14 dias válidos tenha 14 * 288 pontos estatísticos. 5% dos pontos estatísticos mais altos são descartados, de modo que Max95 é o ponto mais alto nos pontos estatísticos restantes, que é a largura de banda faturável. A taxa para janeiro é: Max95 * P * 14 / 31.

### Como posso verificar minhas faturas do CDN?

Você pode verificar suas faturas no [Centro de faturamento](https://console.cloud.tencent.com/expense/bill/overview) do Tencent Cloud. Para obter mais informações, consulte [Consulta de faturas](https://intl.cloud.tencent.com/document/product/228/6071).

### Há um atraso no uso de APIs para consultar dados? De quanto tempo?
Há um certo atraso no uso de APIs para consultar dados. As consultas de dados em tempo real, como dados de acesso e dados de faturamento, têm um atraso de cerca de 5 a 10 minutos, já as consultas de dados analíticos, como classificações, têm atrasos de aproximadamente meia hora. Os dados são calibrados no back-end por volta das 3 da manhã, horário de Pequim.
