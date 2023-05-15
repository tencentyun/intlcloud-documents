As taxas de EIP são cobradas de forma diferenciada de acordo com dois tipos de contas, faturamento por IP e faturamento por CVM. Este documento apresenta como as taxas de EIP são cobradas para os dois tipos de contas. 

## Informações gerais

Atualmente, existem dois tipos de contas do Tencent Cloud: faturamento por IP e faturamento por CVM. Todas as contas do Tencent Cloud registradas após 17 de junho de 2020 são contas com faturamento por IP. As diferenças entre os dois tipos de contas são as seguintes:
 - Faturamento por CVM: gerencia a largura de banda/o tráfego em CVMs. Os IPs e os CLBs de contas com faturamento por CVM não têm atributos de largura de banda ou de tráfego de rede, portanto, precisam ser adquiridos e gerenciados em CVMs.
 - Faturamento por IP: gerencia a largura de banda/o tráfego em IPs e CLBs. Os CVMs adquiridos por essas contas não mantêm mais recursos externos de largura de banda ou de tráfego de rede, os CLBs/IPs públicos gerenciam os recursos externos de largura de banda ou de tráfego de rede.

>? Para obter mais informações sobre como verificar seu tipo de conta, consulte [Verificação do seu tipo de conta](https://intl.cloud.tencent.com/document/product/684/15246).

## Itens faturáveis

As taxas de EIP consistem em **taxas de recursos de IP** e **taxas de rede pública**. As contas com faturamento por CVM e faturamento por IP são faturadas da seguinte forma:

### Contas com faturamento por CVM

As contas com faturamento por CVM incorrem apenas em taxas de recursos de IP. As taxas da rede pública são faturadas nas instâncias do CVM.

- Quando o EIP não está vinculado a recursos de nuvem: o EIP cobra apenas <a href="#ip">taxas de recursos de IP</a> por hora.
- Quando o EIP estiver vinculado aos recursos de nuvem: o EIP em si não cobra nenhuma taxa. <a href="https://intl.cloud.tencent.com/document/product/213/10578">As taxas da rede pública</a> são cobradas nas instâncias do CVM.


### Contas com faturamento por IP

Existem três planos de faturamento para contas com faturamento por IP:

<ul>
<li>Faturamento por tráfego: cobra taxas de rede pública e taxas de recursos de IP.</li>
<ul>
<li>Quando o EIP não está vinculado a recursos de nuvem: o EIP cobra apenas <a href="#ip">taxas de recursos de IP</a> por hora, e não cobra taxas de rede pública.</li>
<li>Quando o EIP está vinculado aos recursos de nuvem: o EIP cobra apenas <a href="#net">taxas de rede pública</a>.</li>
</ul>
<li>Assinatura mensal de largura de banda: cobra apenas <a href="#net">taxas de rede pública</a>, independentemente de o EIP ter sido vinculado a recursos de nuvem ou não.</li>
<li>Pacote de largura de banda: cobra taxas de rede pública e taxas de recursos de IP.
<ul>
<li>Quando o EIP não está vinculado a recursos de nuvem: o EIP cobra apenas <a href="#ip">taxas de recursos de IP</a> por hora, e não cobra taxas de rede pública.</li>
<li>Quando o EIP está vinculado aos recursos de nuvem: o EIP cobra apenas <a href="#net">taxas de rede pública</a>.</li>
</ul></li>
</ul>

<span id ="ip"></span>
## Taxa de recursos de IP

### Período de faturamento

A taxa de recursos de IP é paga conforme o uso em um ciclo de faturamento por hora.
As taxas de recursos de IP são faturadas a partir de quando você solicita o EIP. O faturamento é suspenso quando o recurso de nuvem é vinculado, retomado quando o recurso de nuvem é desvinculado e interrompido quando o EIP é liberado. O faturamento tem uma precisão de segundos e as taxas geradas para a hora são liquidadas e deduzidas na hora seguinte. Se o recurso de nuvem for desvinculado e vinculado várias vezes no mesmo ciclo de faturamento, o período de faturamento será o tempo cumulativo que os recursos de nuvem gastam desvinculados.


### Fórmula de faturamento

Taxa de recursos de IP = o preço de inatividade da região onde o EIP está localizado × período de faturamento

#### Preços

<table>
   <tr><th>Região</th><th>Preço (USD/Hora)</th></tr>
   <tr><td>China Continental</td><td>0,031</td></tr>
   <tr><td>Hong Kong, China</br>Singapura</br>Frankfurt</br>Seul</br>Toronto</br>Virgínia</br>Vale do Silício</br>Bangkok</br>Tóquio</br>Mumbai</td><td>0,04</td></tr>
</table>


#### Amostra de faturamento

Suponha que um usuário que tem uma conta com faturamento por CVM solicitou um EIP na região de Guangzhou entre 09:00:00 e 09:59:59 e foi vinculado ao CVM depois de ficar inativo por 15 minutos (900 segundos), então a taxa de recursos de IP gerada é: 0,031 USD/hora \* (900/3.600) hora = 0,00775 USD. 

> ! Para evitar a geração de taxas desnecessárias de recursos de IP, vincule o EIP aos recursos de nuvem imediatamente depois de solicitar o EIP e libere o EIP imediatamente depois de desvinculá-lo dos recursos de nuvem.

<sapn id="net"></span>

## Taxa de rede pública

O tráfego da rede pública gerado pelo EIP será cobrado com taxas de rede pública. Existem dois planos de faturamento diferentes: o faturamento por tráfego e o faturamento por largura de banda. Para obter mais detalhes, consulte o [Faturamento da rede pública](https://intl.cloud.tencent.com/document/product/213/39743). 

## Em atraso
### Conta em atraso
<table>
    <tr><th>Período de atraso</th><th>Descrição</th></tr>
    <tr><td>Menos de 2 horas</td><td>Você pode continuar a usar seus recursos e sua conta continuará a ser cobrada.</td></tr>
    <tr><td>≥ 2 horas ou ＜ 2 horas + 24 horas</td><td>O EIP será mantido, mas o serviço será suspenso. As taxas não serão mais cobradas e o EIP não poderá ser usado.</td></tr>
    <tr><td>≥ 2 horas + 24 horas</td><td><li>O EIP que não foi vinculado aos recursos de nuvem será liberado.</li><li>O EIP que já foi vinculado aos recursos de nuvem será mantido, mas o serviço será suspenso. As taxas não serão mais cobradas e o EIP não poderá ser usado.</li></td></tr>
</table>

### Recursos vinculados em atraso 
Se o recurso vinculado ao seu EIP estiver em atraso, o EIP será desvinculado do recurso, ficará inativo e incorrerá em uma taxa de inatividade. Se você não precisar mais usar o EIP, libere-o no console.



