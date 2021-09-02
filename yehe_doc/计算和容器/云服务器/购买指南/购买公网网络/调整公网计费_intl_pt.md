>? Atualmente, o modo de assinatura mensal está na versão beta. Os preços publicados aqui são apenas para referência. Consulte suas faturas para obter os preços finais. Para usar essa opção de faturamento, [entre em contato com a equipe de vendas](https://intl.cloud.tencent.com/contact-sales).
>

## Ajuste da largura de banda da rede pública

<table>
<tr><th>Modo de faturamento da rede</th><th>Modo de faturamento do CVM</th><th>Ajustar largura de banda</th></tr>
<tr><td>Assinatura mensal da largura de banda</td><td>Assinatura mensal</td><td>Compatível apenas com o upgrade da largura de banda, e você tem a opção de definir as alterações para que entrem em vigor imediatamente ou em um horário especificado.</td></tr>
<tr><td rowspan=2>Faturamento por tráfego</td><td>Assinatura mensal</td><td rowspan=2>Pode ser feito o upgrade e o downgrade da largura de banda, e as alterações entram em vigor imediatamente. A taxa de rede é calculada com base no uso do tráfego. </td></tr>
<tr><td>Pagamento conforme o uso</td></tr>
</table>

## Alteração do modo de faturamento

<table>
<tr><th>Modo de faturamento da rede</th><th>Modo de faturamento do CVM</th><th>Alterar modo de faturamento da rede</th></tr>
<tr><td>Assinatura mensal da largura de banda</td><td>Assinatura mensal</td><td>Não é compatível.</td></tr>
<tr><td rowspan=2>Faturamento por tráfego</td><td>Assinatura mensal</td><td>Compatível com uma alteração irreversível na assinatura mensal da largura de banda para cada CVM.</td></tr>
<tr><td>Pagamento conforme o uso</td><td>Não é compatível.</td></tr>
</table>


## Exemplo de faturamento

O preço unitário da largura de banda está listado em [Faturamento da rede pública](https://intl.cloud.tencent.com/zh/document/product/213/10578).
>? Este exemplo calcula apenas o custo da rede. As taxas do CVM e de outros dispositivos serão liquidadas separadamente.

### Ajuste da largura de banda

#### Upgrade da largura de banda para a **Assinatura mensal da largura de banda**

Suponha que você adquiriu a assinatura mensal da largura de banda de 2 Mbps para uma instância do CVM na região de Pequim em 1º de novembro de 2018. Você fez o upgrade da largura de banda de 2 Mbps para 5 Mbps entre 20 e 29 de novembro de 2018 por um total de 10 dias.![](https://main.qcloudimg.com/raw/a8ea05b86a9c2e5bda630928585acbe5.png)
A taxa de largura de banda a pagar pela assinatura mensal da largura de banda original em novembro será: largura de banda \* preço unitário = 2 Mbps \* 2,86 USD/Mbps = 5,72 USD
As taxas adicionais após o upgrade da largura de banda serão: a diferença de largura de banda antes e depois do upgrade \* quantidade de dias com o upgrade da largura de banda/dias faturáveis no mês (soma de dias em vários meses) = (3,57 USD/Mbps \* 3 Mbps + 2,86 USD/Mbps \* 2 Mbps - 2,86 USD/Mbps \* 2 Mbps) \* 10 dias/30 dias = 3,57 USD

#### Upgrade ou downgrade da largura de banda para o **faturamento por tráfego**

Você pode ajustar o limite da largura de banda para as instâncias do CVM com faturamento por tráfego sem custo adicional, sempre que precisar. A rede pública é faturada pelo tráfego real.

### Alteração do faturamento da rede pública

#### Alteração de **faturamento por tráfego** para **assinatura mensal da largura de banda**

A taxa de tráfego será liquidada por hora no momento da alteração. Para alterar a opção de faturamento, você só precisa pagar as taxas da assinatura mensal da largura de banda.