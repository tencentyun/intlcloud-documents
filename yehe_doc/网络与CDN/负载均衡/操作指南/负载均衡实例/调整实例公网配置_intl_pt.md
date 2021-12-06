É possível ajustar a largura de banda ou o modo de faturamento das instâncias do CLB da rede pública em tempo real, conforme necessário.

## Restrições
- Instâncias do CLB IPv4: o ajuste da configuração de rede só é permitido para contas de faturamento por IP, mas não para contas de faturamento por CVM.
- Instâncias do CLB IPv6: o ajuste da configuração de rede é permitido para contas de faturamento por IP e por CVM.
- Para obter mais informações sobre como verificar seu tipo de conta, consulte [Verificação do tipo de conta](https://intl.cloud.tencent.com/zh/document/product/684/15246).

## Limite de largura de banda
<table>
<tbody><tr><th>Modo de faturamento da instância</th><th>Modo de faturamento da rede</th><th >Intervalo do limite de largura de banda (em Mbps)</th></tr>
<tr><td rowspan="3">Pagamento conforme o uso</td><td>Faturamento por largura de banda (por hora)</td><td  rowspan="3">0 a 2048 (incluso)</td></tr>
<tr><td>Faturamento por tráfego</td></tr>
<tr><td>Pacote de largura de banda</td></tr>
</tbody></table>

>? Caso precise definir um limite de largura de banda maior, [envie um tíquete](https://console.cloud.tencent.com/workorder/category) ou entre em contato com seu representante de vendas do Tencent Cloud.
>

## Ajuste da largura de banda
1. Faça login no [Console do CLB](https://console.cloud.tencent.com/clb/index?rid=1&type=2%2C3).
2. Na página **Instance Management (Gerenciamento de instâncias)**, selecione uma região e clique em **More (Mais)** -> **Adjust Bandwidth (Ajustar largura de banda)**, à direita de uma instância do CLB de rede pública.
3. Na caixa de diálogo, defina o limite de largura de banda e clique em **Submit (Enviar)**.

## Alteração do modo de faturamento
1. Faça login no [Console do CLB](https://console.cloud.tencent.com/clb/index?rid=1&type=2%2C3).
2. Na página **Instance Management (Gerenciamento de instâncias)**, selecione uma região, clique em **More (Mais)** à direita de uma instância do CLB de rede pública e continue a ajustar o modo de faturamento da rede.
<table>
<tbody><tr><th>Modo de faturamento da instância</th><th>Modo de faturamento da rede</th><th >Ajuste</th></tr>
<tr><td rowspan="3">Pagamento conforme o uso</td><td>Faturamento por largura de banda (por hora)</td><td>Adicionar IP a um pacote de largura de banda: o modo de faturamento da instância permanece o mesmo; o modo de faturamento da rede passa a usar um pacote de largura de banda; cada instância pode ter seu modo de faturamento alterado apenas uma vez.</td></tr>
<tr><td>Faturamento por tráfego</td><td><ul><li>Mudar para assinatura mensal: o modo de faturamento da instância é alterado para assinatura mensal; o modo de faturamento da rede é alterado para faturamento por largura de banda (mensal); cada instância pode ter seu modo de faturamento alterado apenas uma vez.</li><li>Adicionar IP a um pacote de largura de banda: o modo de faturamento da instância permanece o mesmo; o modo de faturamento da rede passa a usar um pacote de largura de banda; cada instância tem uma quantidade limitada de vezes que pode ter seu modo de faturamento alterado.</li></ul></td></tr>
<tr><td>Pacote de largura de banda</td><td>Remover o IP do pacote de largura de banda: o modo de faturamento da instância permanece o mesmo; o modo de faturamento da rede é alterado para faturamento por tráfego; cada instância tem uma quantidade limitada de vezes que pode ter seu modo de faturamento alterado.</td></tr>
</tbody></table>
3. Clique em **Submit (Enviar)** na caixa de diálogo pop-up.

