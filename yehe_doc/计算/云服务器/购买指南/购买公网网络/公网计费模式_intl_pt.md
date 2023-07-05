
## Visão geral do faturamento

O Tencent Cloud fornece redes BGP multilinhas de alta qualidade para garantir uma experiência de rede ideal.
Atualmente, o Tencent Cloud oferece dois planos de faturamento: por tráfego e por largura de banda.
>! 
> - A taxa de rede pública é cobrada com base na largura de banda de saída/no tráfego. A largura de banda de saída refere-se à largura de banda do CVM para a rede pública. Por exemplo, o usuário usa o cliente para baixar recursos da instância do CVM.
> - Para evitar custos inesperados devido a picos de tráfego, você pode definir um limite de largura de banda. O tráfego acima do limite será descartado e não incorrerá em nenhum custo.
> 


## Planos de faturamento


As tabelas a seguir comparam os métodos de pagamento, os ciclos de faturamento e os casos de uso dos dois planos de faturamento diferentes:

- Cálculo do uso com base no tráfego (GB):

 <table class="comparison-table">
                     <tbody><tr>
                        <th>Plano de faturamento</th>
                        <th>Método de pagamento</th>
                                    <th>Ciclo de faturamento</th>
<th>Casos de uso</th>
                     </tr>
                     <tr>
                        <td>Por tráfego</td>
                        <td>Pós-pago</td> 
                                    <td>Por hora</td>
                                    <td>Adequado para cenários em que o pico de tráfego da empresa flutua muito em momentos variados.</td></tr></tbody></table>

- Cálculo do uso com base na largura de banda (Mbps):


 <table class="comparison-table">
                     <tbody><tr>
                        <th>Plano de faturamento</th>
                        <th>Método de pagamento</th>
                                    <th>Ciclo de faturamento</th>
<th>Casos de uso</th>
                     </tr>
                        <td>Pacotes de largura de banda</td>
                        <td>Pós-pago</td> 
                                    <td>Mensal</td>
                                    <td>Adequado para empresas de grande escala, onde o tráfego pode ser escalonado entre instâncias diferentes usando a rede pública.</td>
</tr></tbody></table>


- As larguras de banda de pico do plano de faturamento por tráfego e do plano de faturamento por largura de banda são diferentes. Consulte a tabela abaixo para obter mais detalhes.
<table>
       <tbody><tr>
            <th>Faturamento por tráfego</th>
            <th>Faturamento por largura de banda</th>
       </tr>
       <tr>          
            <td>A largura de banda de pico é considerada apenas como a <strong>largura de banda de pico máxima</strong>, e não como a largura de banda fixa. Em caso de contenção de recursos, a largura de banda de pico pode ser limitada.</td> 
            <td>A largura de banda de pico é considerada como a largura de banda fixa. Em caso de contenção de recursos, a largura de banda de pico será garantida e não será limitada.</td>
            </tr> 
</tbody></table>

## Documentação
[Taxa de rede pública](https://intl.cloud.tencent.com/zh/document/product/213/39743)



