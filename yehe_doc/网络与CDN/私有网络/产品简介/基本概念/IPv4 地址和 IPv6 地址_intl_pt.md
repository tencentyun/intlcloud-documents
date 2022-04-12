Os endereços IP aceitam protocolos de endereçamento IPv4 e IPv6. O IPv4 é amplamente utilizado, mas a quantidade de endereços de rede é limitada, tornando o IPv6 um bom complemento.

### Endereços IPv4
A Tencent Cloud fornece endereços IPv4 para acesso à rede pública e privada. Um endereço IPv4 público pode ser comum ou elástico. Conforme mostrado na figura a seguir, **EIP** indica um endereço IPv4 elástico, **Private (Privado)** indica um endereço IPv4 privado e **Public (Público)** indica um endereço IPv4 público. Esses IPs não serão alterados, a menos que você os desvincule ou altere.
>?Salvo especificação em contrário, IP privado, IP público e EIP se referem a endereços IPv4.
>
![](https://main.qcloudimg.com/raw/6bb952befc42a89392b4d2369f04820d.png)

### Endereços IPv4 privados
Um endereço IPv4 privado é usado para acesso à rede privada da Tencent Cloud, que não pode ser usado para acessar a Internet. Depois que uma instância da CVM for criada, ela será atribuída automaticamente a um endereço IPv4 privado. O endereço IPv4 privado também pode ser personalizado em um ambiente do VPC.

#### Atributos
- A rede privada IPv4 é específica do usuário, e usuários diferentes são isolados uns dos outros. Por padrão, os serviços em nuvem de outro usuário não podem ser acessados por meio da rede privada IPv4.
- A rede privada IPv4 é específica da região, e regiões diferentes são isoladas umas das outras. Por padrão, os serviços em nuvem na mesma conta em uma região diferente não podem ser acessados por meio da rede privada IPv4.

#### Casos de uso
O endereço IPv4 privado pode ser usado para:
- Interconexão entre instâncias do CLB e da CVM baseadas no VPC ou baseadas na rede clássica em uma rede privada IPv4.
- Interconexão entre instâncias da CVM baseadas no VPC ou baseadas na rede clássica em uma rede privada IPv4.
- Interconexão entre instâncias da CVM baseadas na rede clássica ou baseadas no VPC e em outros serviços da Tencent Cloud (como o TencentDB) em uma rede privada IPv4.

#### Operações relevantes
- Para mais informações sobre como obter o endereço IPv4 privado da instância e definir o DNS, consulte [Obtenção de endereços IP privados e configuração do DNS](https://intl.cloud.tencent.com/document/product/213/17941).
- Para mais informações sobre como alterar os endereços IPv4 privados de instâncias da CVM em um VPC, consulte [Modificação de endereços IP privados](https://intl.cloud.tencent.com/document/product/213/16561).

### Endereços IPv4 públicos
A Tencent Cloud fornece IPs públicos e EIPs para acesso à rede pública. Uma instância da CVM com um endereço IPv4 público pode acessar e ser acessada por uma rede pública IPv4.

#### Comparação
A tabela a seguir compara os IPs públicos com os EIPs.
<table>
<thead>
<tr>
<th colspan="2" width="16%">Item</th>
<th>IPs públicos</th>
<th>EIPs</th>
</tr>
</thead>
<tbody>
<tr>
<td colspan="2">Casos de uso</td>
<td>Se você deseja criar uma CVM que permita o acesso à rede pública, pode optar por usar um endereço IP público atribuído automaticamente pelo sistema na criação de uma instância da CVM. Esse endereço IP público tem o mesmo ciclo de vida da CVM e será liberado após a liberação da CVM vinculada.</td>
<td>Se você quiser usar um IP público por um longo tempo, poderá escolher um IP elástico (EIP) e vinculá-lo ao CVM especificado conforme necessário. O EIP pode ser vinculado ou desvinculado muitas vezes, e ainda existirá após a liberação da CVM.</td>
</tr>
<tr>
<td colspan="2">Acesso à rede pública</td>
<td colspan="2">Ambos permitem o acesso à rede pública.</td>
</tr>
<tr>
<td colspan="2">Método de aquisição</td>
<td>Ele só pode ser obtido quando você adquire uma CVM.</td>
<td><li>1. Solicite um EIP no console.</li><li>2. Converta um endereço IP público em um EIP.</li></td>
</tr>
<tr>
<td colspan="2">Funcionalidades</td>
<td>Ele tem o mesmo ciclo de vida da CVM e será liberado após a liberação da CVM vinculada.</td>
<td><li>É independente de outros recursos. Você pode vinculá-lo ou desvinculá-lo de CVMs e NAT Gateways a qualquer momento.</li><li>Você pode liberar um EIP quando não precisar mais dele.</li></td>
</tr>
<tr>
<td colspan="2" >Taxas</td>
<td>Apenas a taxa de rede pública será cobrada.</td>
<td>A taxa de recurso de IP faz parte da taxa de EIP, que varia de acordo com o tipo de conta. Para mais informações, consulte <a href="https://intl.cloud.tencent.com/document/product/684/15246">Verificação do tipo de conta</a>.</td>
</tr>
<tr>
<td colspan="2" rowspan="2">Cota</td>
<td>Está sujeita à quantidade de CVMs que você adquiriu.</td>
<td>Cada conta pode solicitar 20 EIPs em cada região.</td>
</tr>
<tr>
<td colspan="2">Para obter a cota de IPs públicos (incluindo EIPs) vinculados a uma CVM, consulte os limites de IPs públicos vinculados a uma CVM.</td>
</tr>
<tr>
<td rowspan="4" >Operações</td>
<td>Conversão de um IP</td>
<td>É possível converter um IP público em um EIP. O endereço IP não será alterado após a conversão.</td>
<td>Não é possível converter um EIP novamente em um IP público.</td>
</tr>
<tr>
<td>Alteração de um IP</td>
<td>É possível alterar um IP público diretamente.
Para mais informações, consulte <a href="https://intl.cloud.tencent.com/document/product/213/16642" target="_blank">Alteração de endereços IP públicos</a></td>
<td>Não é possível alterar os EIPs diretamente. Você precisa desvincular e liberar o EIP, solicitar um novo e vinculá-lo novamente.</td>
</tr>
<tr>
<td>Liberação de um IP</td>
<td>Se você não precisar mais de um IP público, poderá fazer login no <a href="https://console.cloud.tencent.com/cvm" target="_blank">Console da CVM</a>, localizar o IP público, e na coluna <b>Operation (Operação)</b>, selecionar <b>More (Mais) > IP/ENI > Return Public IP (Retornar IP público)</b> para retorná-lo.</td>
<td>É possível liberar um EIP no console de EIPs.</td>
</tr>
<tr>
<td>Recuperação de um IP</td>
<td colspan="2">Você pode recuperar os IPs públicos ou os EIPs que você usou se eles não tiverem sido usados por outros usuários.</td>
</tr>
</tbody></table>

#### Faturamento
O tráfego de rede pública gerado por endereços IPv4 públicos será cobrado com as taxas de rede pública. Para mais informações, consulte [Preços da rede pública](https://buy.cloud.tencent.com/price/idc).


## Informações relevantes
- Para mais informações sobre como criar rapidamente um Virtual Private Cloud (VPC) IPv4, consulte [Criação de um VPC IPv4](https://intl.cloud.tencent.com/document/product/215/31891).
- Para mais informações sobre EIPs, consulte [IP elástico] (https://intl.cloud.tencent.com/document/product/215/34109).

