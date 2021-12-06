
## Visão geral
O CLB clássico é fácil de configurar e provê suporte a cenários simples de balanceamento de carga:
- CLB clássico da **rede pública**: aceita protocolos TCP/UDP/HTTP/HTTPS.
- CLB clássico da **rede privada**: aceita protocolos TCP/UDP.

As instâncias do CLB podem ser classificadas em dois tipos: CLB (anteriormente conhecido como "CLB do aplicativo") e CLB clássico.

O CLB inclui todas as funcionalidades do CLB clássico. Com base em suas funcionalidades e desempenho, recomendamos o uso do CLB. Para obter uma comparação detalhada, consulte [Tipos de instâncias](https://intl.cloud.tencent.com/document/product/214/8847).
>!Atualmente, existem dois tipos de contas do Tencent Cloud: faturamento por EIP/CLB e faturamento por CVM. Todas as contas do Tencent Cloud registradas após 17 de junho de 2020, às 00:00:00, são contas com faturamento por EIP/CLB. Para contas do Tencent Cloud registradas antes de 17 de junho de 2020, [verifique os tipos de conta](https://intl.cloud.tencent.com/document/product/684/15246) no console. As contas de faturamento por EIP/CLB não aceitam mais o CLB clássico. Agora você só pode adquirir uma instância do CLB.
>
Este documento apresenta as instâncias do CLB clássico. Após a criação de uma instância, é necessário configurar um listener para ela. O listener capta as solicitações na instância do CLB e distribui o tráfego para o servidor de back-end, com base na política de balanceamento de carga.

## Configurações de listeners
É necessário configurar um listener do CLB da seguinte maneira:
1. Protocolo do listener e porta de escuta. A porta de escuta, ou porta de front-end, é usada para receber e encaminhar solicitações para os servidores de back-end.
2. Porta de back-end. É a porta por meio da qual a instância do CVM fornece serviços, recebe e processa o tráfego da instância do CLB.
3. Política de escuta, como política de balanceamento de carga e persistência de sessão.
4. Política de verificação de integridade.
5. O servidor de back-end pode ser vinculado selecionando seu IP.

> ?Se você configurar vários listeners para uma instância do CLB clássico e vincular vários servidores de back-end, cada listener encaminhará solicitações para todos os servidores de back-end com base em sua configuração.

### Tipos de protocolo aceitos
Um listener do CLB pode ouvir as solicitações da camada 4 e 7 em uma instância do CLB e distribuí-las para servidores de back-end para processamento. A principal diferença entre o CLB da camada 4 e o da camada 7 é qual protocolo será usado para encaminhar o tráfego ao balancear a carga das solicitações do usuário.
- Protocolos da camada 4: protocolos da camada de transporte, incluindo TCP e UDP.
- Protocolos da camada 7: protocolos da camada de aplicativos, incluindo HTTP e HTTPS.

>? 
>1. Uma instância do CLB clássico recebe solicitações e encaminha o tráfego para o servidor de back-end via VIP e porta. Os protocolos da camada 7 não permitem encaminhamento com base no nome de domínio e URL.
>2. Uma instância do CLB clássico da rede privada aceita apenas protocolos da camada 4, não os da camada 7.
>3. Se você precisar das funcionalidades avançadas mencionadas acima, recomendamos escolher o CLB em vez do CLB clássico. Para obter mais informações, consulte os [Tipos de instâncias](https://intl.cloud.tencent.com/document/product/214/8847).

### Configuração de portas
<table>
<thead>
<tr>
<th width="30%">Porta de escuta (porta de front-end)</th>
<th width="30%">Porta de serviço (porta de back-end)</th>
<th width="40%">Descrição</th>
</tr>
</thead>
<tbody><tr>
<td>A porta de escuta é usada por uma instância do CLB para receber e encaminhar solicitações a servidores de back-end para balanceamento de carga.<br><br>Você pode configurar o CLB para o intervalo de portas 1 a 65535, como 21 (FTP), 25 (SMTP), 80 (HTTP) e 443 (HTTPS).</td>
<td>Uma porta de serviço é usada pelo CVM para fornecer serviços, receber e processar o tráfego da instância do CLB.<br><br>Em uma instância do CLB, uma porta de escuta pode encaminhar o tráfego para portas de várias instâncias do CVM.</td>
<td>Em uma instância do CLB,<li>uma porta de escuta deve ser exclusiva.<br>Por exemplo, os listeners TCP:80 e HTTP:80 não podem ser criados ao mesmo tempo.</li><li>Apenas as portas TCP e UDP podem ser iguais.<br>Por exemplo, você pode criar listeners TCP:80 e UDP:80.</li><br>As mesmas portas de serviço podem ser usadas em uma instância do CLB.<br>Por exemplo, os listeners HTTP:80 e HTTPS:443 podem ser vinculados à mesma porta de uma instância do CVM.</td>
</tr>
</tbody></table>

