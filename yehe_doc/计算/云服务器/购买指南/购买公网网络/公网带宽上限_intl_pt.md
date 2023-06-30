Este documento descreve o limite da largura de banda de entrada e saída das instâncias do CVM e compara a largura de banda de pico em diferentes modos de faturamento.

## Limite da largura de banda de saída (largura de banda downstream)

O limite da largura de banda da rede pública se refere ao limite superior da largura de banda de saída, ou seja, a largura de banda que sai das instâncias do CVM. O limite da largura de banda da rede pública varia de acordo com o modo de faturamento da rede. Consulte os detalhes abaixo:
- As seguintes regras se aplicam a instâncias criadas após as 00:00 de 24 de fevereiro de 2020:
<table>
<tbody><tr><th rowspan="2" style="
    width: 20%;
">Método de faturamento da rede</th><th colspan="2">Instância</th><th rowspan="2" style="width:35%">Intervalo do limite da largura de banda (Mbps)</th></tr>
<tr><th style="
    width: 20%;
">Modo de faturamento da instância</th><th style="
    width: 25%;
">Configuração da instância</th></tr>
<tr><td>Faturamento por tráfego</td><td>Instâncias com pagamento conforme o uso</td><td>Todas</td><td>0-100</td></tr>
<tr><td>Faturamento por largura de banda</td><td>Instâncias com pagamento conforme o uso</td><td>Todas</td><td>0-100</td></tr>
<tr><td>Pacote de largura de banda</td><td colspan="2">Todas</td><td>0-2000</td></tr>
</tbody></table>

- As seguintes regras se aplicam a instâncias criadas antes das 00:00 de 24 de fevereiro de 2020:
<table>
<tbody><tr><th rowspan="2" style="
    width: 20%;
">Método de faturamento da rede</th><th colspan="2">Instância</th><th rowspan="2" style="width:35%">Intervalo do limite da largura de banda (Mbps)</th></tr>
<tr><th style="
    width: 20;
">Modo de faturamento da instância</th><th style="
    width: 25%;
">Configuração da instância</th></tr>
<tr><td rowspan="1">Faturamento por tráfego</td><td>Instâncias com pagamento conforme o uso</td><td>Todas</td><td>0-100</td></tr>
<tr><td rowspan="3">Faturamento por largura de banda</td><td>Instâncias com pagamento conforme o uso</td><td>Todas</td><td>0-100</td></tr>
<tr><td>Pacote de largura de banda</td><td>Todas</td><td>0-1000</td></tr>
</tbody></table>



## Limite da largura de banda de entrada (largura de banda upstream)

A largura de banda de entrada da rede pública se refere à largura de banda que flui para as instâncias do CVM.
- Se a largura de banda que você adquiriu for superior a 10 Mbps, o Tencent Cloud atribuirá uma largura de banda de entrada da rede pública igual à largura de banda adquirida.
- Se a largura de banda que você adquiriu for inferior a 10 Mbps, o Tencent Cloud atribuirá uma largura de banda de entrada da rede pública de 10 Mbps.

## Largura de banda de pico
A largura de banda de pico é aplicável para o faturamento por tráfego e para o faturamento por largura de banda, mas tem um significado diferente nesses dois casos, da seguinte forma:

<table>
       <tbody><tr>
			 <th width="17%">Modo de faturamento</th>
			 <th>Diferença</th>
			 <th>Observações</th>
       </tr>
			 <tr>
			 <td>Faturamento por tráfego</td>
			 <td>A largura de banda de pico é considerada apenas como a <strong>largura de banda de pico máxima</strong>, e não como a largura de banda comprometida. Quando os recursos de largura de banda são contestados, a largura de banda de pico pode ser limitada.</td> 
			 <td>A soma da largura de banda de pico de todas as instâncias com faturamento por tráfego em execução (como CVMs, EIPs, endereços IPv6 elásticos) não pode exceder 5 Gbps em uma região. Se o seu aplicativo requer uma largura de banda garantida ou superior, escolha o faturamento por largura de banda.</td> 
			 </tr>
       <tr>          
            <td>Faturamento por largura de banda<br/>(incluindo a assinatura mensal da largura de banda e a largura de banda por hora)</td>
            <td>Essa largura de banda de pico é a largura de banda comprometida, e é garantida em caso de competição de largura de banda.</td>
						<td>A soma da largura de banda de pico de todas as instâncias em execução, como CVMs e EIPs, que são faturadas em uma largura de banda fixa (incluindo largura de banda com assinatura mensal e largura de banda por hora) não pode exceder 50 Gbps em uma região. Se você precisar de uma largura de banda maior, entre em contato com seu representante de vendas.

</td> 
            </tr> 
</tbody></table>


## Documentação
- [Ajuste da configuração da rede](https://intl.cloud.tencent.com/document/product/213/15517)
