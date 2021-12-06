>?
>- Atualmente, o CLB IPv6 está em teste beta. Se quiser usá-lo, [envie um tíquete](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=163&source=0&data_title=%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%20LB&step=1) para solicitar.
>- Atualmente, as instâncias do CLB IPv6 podem ser criadas nas regiões de Guangzhou, Xangai, Nanjing, Pequim, Chengdu, Hong Kong (China), Cingapura e Virgínia.
>- O CLB IPv6 não é compatível com o CLB da rede clássica.
>- O CLB IPv6 permite a obtenção do endereço de origem IPv6 do cliente, que pode ser obtido diretamente pelo CLB IPv6 da camada 4 ou por meio do cabeçalho `X-Forwarded-For` do CLB IPv6 do HTTP da camada 7.
>- Atualmente, o CLB IPv6 é totalmente implementado na rede pública; portanto, os clientes no mesmo VPC não podem acessá-lo na rede privada.
>- As implementações do IPv6 ainda estão em seu estágio inicial na Internet. Em caso de falha de acesso, [envie um tíquete](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=163&source=0&data_title=%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%20LB&step=1). O SLA não é garantido durante o período de teste beta.

## Visão geral
O CLB IPv6 é o balanceamento de carga implementado com base na tecnologia de pilha única IPv6. Ele pode colaborar com o CLB IPv4 para implementar a comunicação de pilha dupla IPv6/IPv4. Uma instância do CLB IPv6 é vinculada a um endereço IPv6 de uma instância do CVM e fornece um endereço VIP IPv6.
### Vantagens do CLB IPv6
O CLB IPv6 tem as seguintes vantagens ao ajudar sua empresa a se conectar rapidamente ao IPv6:
- Conexão rápida: o CLB permite a conexão ao IPv6 em questão de segundos e fica disponível no momento da aquisição.
- Fácil de usar: o CLB IPv6 é compatível com o processo de operação do CLB IPv4 e é fácil de usar, sem custos adicionais de aprendizagem.
- Comunicação IPv6 de ponta a ponta: o CLB IPv6 se comunica com instâncias do CVM pelo IPv6, o que ajuda os aplicativos implantados nessas instâncias a atualizar rapidamente para o IPv6 e implementar comunicação IPv6 de ponta a ponta.

### Arquitetura do CLB IPv6
O CLB permite a criação de instâncias do CLB IPv6. O Tencent Cloud atribuirá um endereço IP público IPv6, ou seja, VIP da edição IPv6, a uma instância do CLB IPv6, e o VIP encaminhará solicitações de clientes IPv6 para a instância do CVM IPv6 real.

Uma instância do CLB IPv6 possibilita o acesso rápido do usuário da rede pública IPv6 e se comunica com servidores de back-end pelo IPv6, o que ajuda os aplicativos em nuvem a se atualizarem rapidamente para o IPv6 e implementar comunicação IPv6 de ponta a ponta.

A arquitetura do CLB IPv6 é conforme mostrado abaixo.
![](https://main.qcloudimg.com/raw/d86205a385506928dc13ef9646a91243.png)

## Guia de operação
### Etapa 1. Crie uma instância do CLB IPv6
1. Faça login no site oficial do Tencent Cloud e acesse a [página de aquisição do CLB](https://buy.cloud.tencent.com/lb).
2. Selecione as opções para os seguintes parâmetros corretamente:
 - Billing Mode (Modo de faturamento): apenas o faturamento pay-as-you-go (com pagamento conforme o uso) é aceito.
 - Region (Região): selecione uma região.
 - IP Version (Versão do IP): IPv6.
 - ISP Type (Tipo de ISP): BGP.
 - Network (Rede): selecione um VPC e uma sub-rede que já tenham obtido o CIDR IPv6.
3. Depois de definir os itens de configuração na página de aquisição, clique em **Buy Now (Comprar agora)** para retornar à [página da lista de instâncias do CLB](https://console.cloud.tencent.com/loadbalance/index?rid=1&forward=1), na qual você pode exibir a instância do CLB IPv6 recém-adquirida.

### Etapa 2. Crie um listener do CLB IPv6
1. Faça login no [Console do CLB](https://console.cloud.tencent.com/clb/index?rid=1&type=2%2C3) e clique no ID da instância do CLB IPv6 para acessar a página de detalhes.
2. Selecione a guia **Listener Management (Gerenciamento de listener)** e clique em **Create (Criar)** para criar um listener, por exemplo, um servidor TCP.
>? O CLB permite a criação de listeners do CLB IPv6 da camada 4 (TCP/UDP/TCP SSL) e da camada 7 (HTTP/HTTPS). Para obter mais informações, consulte a [Visão geral de listener do CLB](https://intl.cloud.tencent.com/document/product/214/6151).
>
3. Em "Basic Configurations (Configurações básicas)", configure o nome, as portas de protocolo de escuta e o método de balanceamento e clique em **Next (Avançar)**.
![](https://main.qcloudimg.com/raw/dce7a8870add7556a229c10990444e78.png)
4. Configure a verificação de integridade e clique em **Next (Avançar)**.
![](https://main.qcloudimg.com/raw/7e425de32751160382b602752c302f19.png)
5. Configure a persistência de sessão e clique em **Submit (Enviar)**.
![](https://main.qcloudimg.com/raw/e4d910a5904e1c8fb890d594bb64ba72.png)
6. Após a criação do listener, selecione-o e clique em **Bind (Vincular)** à direita.
>?Antes de vincular o listener a uma instância do CVM, verifique se ela obteve um endereço IPv6.
>
![](https://main.qcloudimg.com/raw/6c1a45bed978f944fcb34984849d5287.png)
7. Na caixa pop-up, selecione a instância do CVM IPv6 real com a qual precisa ser comunicada, configure a porta de serviço e o peso e clique em **OK**.
![](https://main.qcloudimg.com/raw/6c1a45bed978f944fcb34984849d5287.png)
