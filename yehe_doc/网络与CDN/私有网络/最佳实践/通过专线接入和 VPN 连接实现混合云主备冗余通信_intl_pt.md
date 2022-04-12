Se os seus negócios estiverem implantados em um IDC local e em uma VPC da Tencent Cloud, você poderá conectá-los pelo Direct Connect ou pela VPN. Para melhorar a disponibilidade dos negócios, configure o DC e a VPN Connections como a ligação principal e secundária para comunicação redundante. Este documento orienta você sobre como configurar o DC e a VPN Connection como ligações principal/secundária para conectar seu IDC à nuvem.
>?
>+ Atualmente, a funcionalidade de prioridade de rota está em teste beta. Para testá-la, [envie um tíquete](https://console.cloud.tencent.com/workorder/category).
>+ O próximo tipo de salto determina a prioridade da rota na tabela de rotas da VPC. Por padrão, a prioridade de rota de alta para baixa é: CCN, gateway do Direct Connect, VPN Gateway e outros.
>+ Atualmente, não é possível ajustar a prioridade da rota no console. Se precisar alterá-la, [envie um tíquete](https://console.cloud.tencent.com/workorder/category).



## Cenários
Você implantou negócios em uma VPC da Tencent Cloud e em um IDC. Para interconectá-los, você precisa configurar os serviços de conexão de rede para comunicações de alta disponibilidade da seguinte forma:
+ Direct Connect (principal): conecta o IDC local a um gateway do Direct Connect baseado na VPC por meio de uma conexão. Quando a ligação da conexão estiver normal, todo o tráfego de dados entre o IDC e a VPC será encaminhado por meio da conexão.
+ VPN Connection (secundário): estabelece um túnel VPN IPsec para interconectar o IDC local e a VPC da Tencent Cloud. Quando a ligação de conexão falhar, o tráfego será encaminhado usando essa ligação para garantir a disponibilidade dos negócios.
![](https://main.qcloudimg.com/raw/c50965f32412860aec344f2cd0dabd6d.png)

## Pré-requisitos
+ O seu dispositivo de gateway do IDC local deve permitir a funcionalidade VPN IPsec, e pode atuar como um gateway do cliente para criar um túnel VPN com a VPN Gateway.
+ O dispositivo de gateway do IDC foi configurado com um endereço IP estático.
+ Dados de exemplo e configuração:
  <table>
  <th colspan="3">Item de configuração</th>
   <th>Valor de exemplo</th>
  <tr>
  <td rowspan="4">Rede</td>
  <td rowspan="2">Informações da VPC</td>
  <td>Bloco CIDR da sub-rede</td>
  <td>192.168.1.0/24 </td>
  </tr>
  <tr>
  <td>IP público da VPN Gateway</td>
  <td>203.xx.xx.82</td>
  </tr>
  <tr>
  <td rowspan="2">Informações do IDC</td>
  <td>Bloco CIDR da sub-rede</td>
  <td>10.0.1.0/24</td>
  </tr>
	<tr>
	<td>IP público do gateway</td>
	<td>202.xx.xx.5</td>
	</tr>
	</table>
	

## Etapas
<dx-steps>
- [Conectar o IDC à VPC pelo Direct Connect](#step1)
- [Conectar o IDC à VPC pela VPN Connection](#step2)
- [Configurar sondas de rede](#step3)
- [Configurar uma política de alarme](#step4)
- [Alternar entre as rotas principal e secundárias](#step5)
  </dx-steps>

## Instruções

### [](id:step1)Etapa 1: conectar o IDC à VPC pelo Direct Connect
1. Faça login no console do Direct Connect, abra os [Dedicated Tunnels (Túneis dedicados)](https://console.cloud.tencent.com/dc/dc) e clique em **Connections (Conexões)** na barra lateral esquerda para criar uma conexão.
2. Faça login no [Console da VPC](https://console.intl.cloud.tencent.com/vpc/vpc?rid=4) e clique em **Direct Connect Gateway (Gateway do Direct Connect)** na barra lateral esquerda. Clique em **+New (+Novo)** para criar um gateway padrão do Direct Connect para o qual a **Associate Network (Rede associada)** seja o **VPC**. Se o intervalo de IP do IDC entrar em conflito com o intervalo de IP da VPC, selecione o **NAT Type (Tipo de NAT)**.
3. Acesse a página **Dedicated Tunnels (Túneis dedicados)** e clique em **+New (+Novo)** para criar um túnel dedicado. Insira o nome do túnel, selecione o tipo de conexão e a instância de gateway do Direct Connect recém-criada. Configure os endereços IP na Tencent Cloud e no IDC, selecione a rota estática e insira o intervalo IP do CPE. Após a conclusão da configuração, clique em **Download configuration guide (Baixar o guia de configurações)** e conclua as configurações do dispositivo IDC conforme as instruções do guia.
4. Na tabela de rotas associada à sub-rede da VPC para a comunicação, configure uma política de roteamento com o gateway do Direct Connect como o próximo salto e o intervalo de IP do IDC como o destino.
>? Para obter as configurações detalhadas, consulte [Introdução](https://intl.cloud.tencent.com/document/product/216/7557).


###  [](id:step2)Etapa 2: conectar o IDC à VPC por meio de uma VPN Connection
1. Faça login no [Console da VPN Gateway](https://console.cloud.tencent.com/vpc/vpnGw?rid=1) e clique em **+New (+Novo)** para criar uma VPN Gateway para o qual a **Associate Network (Rede associada)** seja uma **Virtual Private Cloud**.
2. Clique em **Customer Gateway (Gateway do cliente)** na barra lateral esquerda, e clique em **+New (+Novo)** para configurar um gateway do cliente (um objeto lógico da VPN Gateway no IDC). Insira o endereço IP público da VPN Gateway no IDC, como `202.xx.xx.5`.
3. Clique em **VPN Tunnel (Túnel VPN)** na barra lateral esquerda, e clique em **+New (+Novo)** para concluir as configurações, como política SPD, IKE e IPsec.
4. Configure o mesmo túnel VPN que a Etapa 3 no dispositivo de gateway local do IDC, para garantir uma conexão normal.
5. Na tabela de rotas associada à sub-rede da VPC para a comunicação, configure uma política de roteamento com a VPN Gateway como o próximo salto e o intervalo de IP do IDC como o destino.
>?Para obter instruções detalhadas, consulte [Conexão da VPC ao IDC (Tabela de rotas)](https://intl.cloud.tencent.com/document/product/1037/39675).
>

###  [](id:step3)Etapa 3: configurar sondas de rede
>?Após as duas primeiras etapas, há duas rotas da VPC para o IDC. Ou seja, tanto o gateway do Direct Connect quanto a VPN Gateway agem como o próximo salto. Por padrão, a rota do gateway do Direct Connect tem uma prioridade mais alta, tornando-a o caminho principal, e a VPN Gateway, o caminho secundário.

Para acompanhar a qualidade da conexão principal/secundária, configure duas sondas de rede separadamente, a fim de monitorar as principais métricas, como latência e taxa de perda de pacotes, e verifique a disponibilidade das rotas principal/secundária.
1. Faça login no [Console da VPC](https://console.cloud.tencent.com/vpc/detection?rid=1).
2. Clique em **+New (+Novo)** para criar uma sonda de rede. Insira um nome e um IP de destino, selecione uma VPC e uma sub-rede, e defina **Source Next Hop (Próximo salto da fonte)** como o gateway do Direct Connect.
3. Repita a [Etapa 2](#step2) e defina **Source Next Hop (Próximo salto da fonte)** como a VPN Gateway. Após a conclusão da configuração, você pode verificar a latência e a taxa de perda de pacotes da rede sondada do gateway do Direct Connect e do VPN Connection.
>? Para obter as configurações detalhadas, consulte [Sonda de rede](https://intl.cloud.tencent.com/document/product/215/35522).
>

### [](id:step4)Etapa 4: configurar uma política de alarme
Você pode configurar uma política de alarme para ligações. Quando uma ligação tem uma exceção, são enviadas notificações de alarme a você automaticamente por e-mail e mensagem SMS, alertando-o antecipadamente sobre os riscos.
1. Faça login no console do CM e acesse a página [**Alarm Policy (Política de alarme)**](https://console.cloud.tencent.com/monitor/alarm2/policy).
2. Clique em **Create (Criar)**. Insira o nome da política, selecione VPC/Network Probe (VPC/Sonda de rede) para o tipo de política, especifique as instâncias da sonda de rede como o objeto de alarme, e configure as condições de disparo, as notificações de alarme e outras informações. Depois, clique em **Complete (Concluir)**.

### [](id:step5)Etapa 5: alternar entre as rotas principal/secundária
Após receber os alarmes de exceção sobre o gateway do Direct Connect, você precisa desativar manualmente a rota principal e encaminhar o tráfego para a VPN Gateway da rota secundária.
1. Faça login no console da VPC e acesse a página [**Route Tables (Tabelas de rotas)**](https://console.cloud.tencent.com/vpc/route?rid=1).
2. Localize a tabela de rotas associada à sub-rede da VPC para a comunicação, clique em **ID/Name (ID/Nome)** para acessar sua página de detalhes. Clique em <img src="https://main.qcloudimg.com/raw/af79ad3ab5488ea94ead43a8fba3486f.png" width="3%" /> para desativar a rota principal com a CCN como o próximo salto. Em seguida, o tráfego da VPC destinado ao IDC será encaminhado para a VPN Gateway, em vez do gateway do Direct Connect.
