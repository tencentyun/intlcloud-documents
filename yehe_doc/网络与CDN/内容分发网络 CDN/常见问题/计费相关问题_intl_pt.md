### O CDN pode ser faturado pela quantidade de solicitações?
Não. Atualmente, o CDN não aceita o faturamento pela quantidade de solicitações.

### O que acontecerá se o saldo da minha conta ficar negativo?
Para obter mais informações, consulte [Pagamento em atraso](https://intl.cloud.tencent.com/document/product/228/2949#.E6.AC.A0.E8.B4.B9.E8.AF.B4.E6.98.8E) no documento de descrição do faturamento.

### Se o servidor de origem usar o COS, serei cobrado pelo tráfego gerado pelo pull de origem do CDN para o COS?
Não. O tráfego gerado pelo pull de origem do CDN para o COS é faturado pelo COS em vez do CDN. Para obter mais informações, consulte [COS como um servidor de origem](https://intl.cloud.tencent.com/document/product/228/32977).

### Quando o CDN for desabilitado (ou desativado), ele vai gerar tráfego e incorrer em taxas?
Depois que o serviço de aceleração de nome de domínio do CDN for desabilitado, se o nome de domínio ainda estiver configurado com o CNAME, um código de status 404 será retornado para solicitações resolvidas para o nó e uma pequena quantidade de tráfego será consumida. O console registrará esses dados de tráfego para sua referência. Os logs correspondentes também serão gerados. No entanto, como seu nome de domínio foi desabilitado, você não será faturado por esse consumo de tráfego e pacotes de log. Recomendamos que você modifique a resolução de pull de origem primeiro, antes de desabilitar o serviço de aceleração.

### Como eu altero o modo de faturamento do CDN?

Se você achar que o modo de faturamento escolhido não é adequado para suas condições empresariais reais (para obter mais informações sobre como escolher o modo de faturamento adequado para você, consulte [Escolha de um plano de faturamento](https://intl.cloud.tencent.com/document/product/228/2949#.E8.AE.A1.E8.B4.B9.E6.96.B9.E5.BC.8F.E9.80.89.E6.8B.A9)), você pode alterá-lo seguindo as etapas abaixo:
1. Faça login no [Console do CDN](https://console.cloud.tencent.com/cdn), acesse a página de visão geral do serviço e clique em **Change (Alterar)** na seção de modo de faturamento à direita.
![](https://main.qcloudimg.com/raw/38b82d3d166970552437b5525b74c44f.png)
2. Altere o modo de faturamento original **Bill by Traffic (Faturamento por tráfego)** para **Bill by Bandwidth (Faturamento por largura de banda)**.
![](https://main.qcloudimg.com/raw/6fd1575557d0c4b7b06be9f1fc30e1da.png)
3. Depois de alterar o modo de faturamento para **Bill by Bandwidth (Faturamento por largura de banda)**, a cobrança pelo consumo total gerado na data atual será faturada e deduzida no dia seguinte:

### Se o servidor de origem usar o CVM, serei cobrado pelo tráfego gerado pelo pull de origem do CDN para o CVM?

Não. O CDN não cobra por esse tipo de tráfego.

### Qual é a taxa de conversão de Gbps para Mbps no faturamento do CDN?

No faturamento do CDN, 1 Gbps = 1.000 Mbps, 1 Mbps = 1.000 Kbps e 1 Kbps = 1.000 bps.

### Somente o tráfego downstream é faturado no CDN?

Sim. O CDN cobra apenas pelo tráfego downstream, não o upstream.


### Há um atraso no uso de APIs para consultar dados? De quanto tempo?
Há um certo atraso no uso de APIs para consultar dados. As consultas de dados em tempo real, como dados de acesso e dados de faturamento, têm um atraso de cerca de 5 a 10 minutos, já as consultas de dados analíticos, como classificações, têm atrasos de aproximadamente meia hora. Os dados são calibrados no back-end por volta das 3 da manhã, horário de Pequim.
