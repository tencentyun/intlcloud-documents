Se os seus negócios estiverem implantados em um IDC local e em uma VPC da Tencent Cloud, você poderá conectá-los pela Cloud Connect Network (CCN) ou pela VPN. Para melhorar a disponibilidade dos negócios, configure a CCN e a VPN Connections como a ligação principal e secundária para comunicação redundante. Este documento orienta você sobre como configurar a CCN e a VPN Connection como ligações principal/secundária para conectar seu IDC à nuvem.
>?Atualmente, a funcionalidade de prioridade de rota está em teste beta. Para testá-la, [envie um tíquete](https://console.cloud.tencent.com/workorder/category).


## Cenários
Suponha que você tenha implantado os seus negócios na VPC da Tencent Cloud e em um IDC. Para interconectá-los, você precisa configurar os serviços de conexão de rede para comunicações de alta disponibilidade da seguinte forma:
+ CCN (principal): conecta o IDC local a um gateway do Direct Connect baseado na CCN por meio de uma conexão física, e adiciona o gateway do Direct Connect e a VPC a umaCCN para habilitar a interconexão. Quando a ligação da conexão estiver normal, todo o tráfego de dados entre o IDC e a VPC será encaminhado pela CCN por meio da conexão física.
+ VPN Connection (secundário): estabelece um túnel VPN IPsec para interconectar o IDC local e a VPC da Tencent Cloud. Quando a ligação de conexão falhar, o tráfego será encaminhado usando essa ligação para garantir a disponibilidade dos negócios.

![](https://main.qcloudimg.com/raw/ce97fc610f1119e92094f72027a3aa9b.png)

## Pré-requisitos
+ O seu dispositivo de gateway do IDC local deve permitir a funcionalidade VPN IPsec e pode atuar como um gateway do cliente para criar um túnel VPN com a VPN Gateway.
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
​	

## Etapas
<dx-steps>
- [Configurar uma instância do Direct Connect](#step1)
- [Configurar uma VPN Connection](#step2)
- [Configurar sondas de rede](#step3)
- [Configurar uma política de alarme](#step4)
- [Alternar entre as rotas principal e secundárias](#step5)
</dx-steps>

## Instruções

### [](id:step1)Etapa 1: conectar o IDC à VPC por meio da CCN
1. Faça login no [Console do Direct Connect](https://console.cloud.tencent.com/dc/dc) e clique em **Connections (Conexões)** na barra lateral esquerda para criar uma conexão.
2. Faça login no [Console da VPC](https://console.intl.cloud.tencent.com/vpc/vpc?rid=4) e clique em **Direct Connect Gateway (Gateway do Direct Connect)** na barra lateral esquerda. Clique em **+New (+Novo)** para criar um gateway do Direct Connect para o qual a **Associate Network (Rede associada)** seja a **CCN**.
3. Clique no **ID/Name (ID/Nome)** do gateway do Direct Connect recém-criado para acessar sua página de detalhes. Selecione a guia **IDC IP Range (Intervalo de IP do IDC)** para inserir o intervalo de IP do IDC, como `10.0.1.0/24`.
4. Acesse a página do [CCN](https://console.cloud.tencent.com/vpc/ccn) e clique em **+New (+Novo)** para criar uma instância do CCN.
5. Acesse a página [Dedicated Tunnels (Túneis dedicados)](https://console.cloud.tencent.com/dc/dc) e clique em **+New (+Novo)** para criar um túnel dedicado para conectar o gateway do Direct Connect baseado no CCN. Insira o nome do túnel, selecione **CCN** para **Access Network (Rede de acesso)** e, em seguida, selecione a instância de gateway do Direct Connect baseada no CCN criada anteriormente. Configure os endereços IP na Tencent Cloud e no IDC, e selecione a rota BGP. Após a conclusão da configuração, clique em **Download configuration guide (Baixar o guia de configurações)** e conclua as configurações do dispositivo IDC conforme as instruções do guia.
6. Associe a VPC e o gateway do Direct Connect baseado no CCN à instância da CCN para interconectar a VPC e o IDC.
>? Para obter instruções detalhadas, consulte [Migração do IDC para a nuvem por meio da CCN](https://intl.cloud.tencent.com/document/product/216/41747).

###  [](id:step2)Etapa 2: conectar o IDC à VPC por meio de uma VPN Connection
1. Faça login no [Console da VPN Gateway](https://console.cloud.tencent.com/vpc/vpnGw?rid=1) e clique em **+New (+Novo)** para criar uma VPN Gateway para o qual a **Associate Network (Rede associada)** seja uma **Virtual Private Cloud**.
2. Clique em **Customer Gateway (Gateway do cliente)** na barra lateral esquerda e clique em **+New (+Novo)** para configurar um gateway do cliente (um objeto lógico da VPN Gateway no IDC). Insira o endereço IP público da VPN Gateway no IDC, como `202.xx.xx.5`.
3. Clique em **VPN Tunnel (Túnel VPN)** na barra lateral esquerda e clique em **+New (+Novo)** para concluir as configurações, como política SPD, IKE e IPsec.
4. Configure o mesmo túnel VPN que a [Etapa 3](#step3) no dispositivo de gateway local do IDC para garantir uma conexão normal.
5. Na tabela de rotas associada à sub-rede da VPC para comunicação, configure uma política de roteamento com a VPN Gateway como o próximo salto e o intervalo de IP do IDC como o destino.
>?Para obter as configurações detalhadas de VPN Gateways em diferentes versões,
>+ Para uma VPN Gateway v1.0 e v2.0, consulte [Conexão da VPC ao IDC (Política SPD)](https://intl.cloud.tencent.com/document/product/1037/39683).
>+ Para uma VPN Gateway v3.0, consulte [Conexão da VPC ao IDC (Tabela de rotas)](https://intl.cloud.tencent.com/document/product/1037/39675).

###  [](id:step3)Etapa 3: configurar sondas de rede
>?Após as duas primeiras etapas, há duas rotas da VPC para o IDC. Ou seja, tanto a CCN quanto a VPN Gateway agem como o próximo salto. A rota da CCN tem uma prioridade mais alta, tornando-a o caminho principal e a VPN Gateway, o caminho secundário.
>
Para acompanhar a qualidade da conexão principal/secundária, configure duas sondas de rede separadamente para monitorar as principais métricas, como latência e taxa de perda de pacotes, e verifique a disponibilidade de rotas principal/secundária.
1. Acesse a página [Network Probe (Sonda de rede)](https://console.cloud.tencent.com/vpc/detection?rid=1) no console da VPC.
2. Clique em **+New (+Novo)** para criar uma sonda de rede. Insira um nome e um IP de destino, selecione uma VPC e uma sub-rede, e defina **Source Next Hop (Próximo salto da fonte)** como a CCN.
3. Repita a [Etapa 2](#step2) e defina **Source Next Hop (Próximo salto da fonte)** como a VPN Gateway. Após a conclusão da configuração, você pode verificar a latência da rede sondada e a taxa de perda de pacotes da CCN e da VPN Connection.
>? Para obter as configurações detalhadas, consulte [Sonda de rede](https://intl.cloud.tencent.com/document/product/215/35522).
>

### [](id:step4)Etapa 4: configurar uma política de alarme
Você pode configurar uma política de alarme para ligações. Quando uma ligação tem uma exceção, são enviadas notificações de alarme a você automaticamente por e-mail e mensagem SMS, alertando-o antecipadamente sobre os riscos.
1. Faça login no console da CM e acesse a página [**Alarm Policy (Política de alarme)**](https://console.cloud.tencent.com/monitor/alarm2/policy).
2. Clique em **Create (Criar)**. Insira o nome da política, selecione VPC/Network Probe (VPC/Sonda de rede) para o tipo de política, especifique as instâncias da sonda de rede como o objeto de alarme e configure as condições de disparo, as notificações de alarme e outras informações. Depois, clique em **Complete (Concluir)**.

### [](id:step5)Etapa 5: alternar entre as rotas principal/secundária
Após receber um alarme de exceção de rede da CCN, você precisa desativar manualmente a rota principal e encaminhar o tráfego para a VPN Gateway da rota secundária.
1. Faça login no console da VPC e acesse a página [**Route Tables (Tabelas de rotas)**](https://console.cloud.tencent.com/vpc/route?rid=1).
2. Localize a tabela de rotas associada à sub-rede da VPC para comunicação, clique em **ID/Name (ID/Nome)** para acessar sua página de detalhes. Clique em <img src="https://main.qcloudimg.com/raw/af79ad3ab5488ea94ead43a8fba3486f.png" width="3%" /> para desativar a rota principal com a CCN como o próximo salto. Em seguida, o tráfego da VPC destinado ao IDC será encaminhado para a VPN Gateway, em vez da CCN.
