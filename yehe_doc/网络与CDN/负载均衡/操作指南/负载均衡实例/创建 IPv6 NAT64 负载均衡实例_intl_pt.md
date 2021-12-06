>
>- O CLB IPv6 NAT64 só pode ser criado em três regiões: Pequim, Xangai e Guangzhou.
>- O CLB IPv6 NAT64 não é compatível com o CLB da rede clássica.
>- O CLB IPv6 NAT64 não permite a obtenção de IPs do cliente.
>- As implementações do IPv6 ainda estão em estágio preliminar na Internet e o SLA não é garantido. Em caso de falha de acesso, [envie um tíquete](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=163&source=0&data_title=%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%20LB&step=1) para obter ajuda.

O CLB permite a criação de instâncias do CLB IPv6 NAT64. O Tencent Cloud atribuirá um endereço IP público IPv6, ou seja, VIP da edição IPv6, a uma instância, e o VIP encaminhará solicitações de clientes IPv6 para a instância do CVM IPv4 real.

## Visão geral da instância do CLB IPv6 NAT64
Uma instância do CLB IPv6 NAT64 é um balanceador de carga implementado com base na tecnologia de ponte IPv6 NAT64. Por meio de uma instância do CLB IPv6 NAT64, os servidores de back-end podem ser acessados rapidamente por usuários IPv6 sem a necessidade de nenhuma modificação do IPv6.

### Arquitetura do CLB IPv6 NAT64
A arquitetura do CLB IPv6 NAT64 é conforme mostrado abaixo.
![](https://main.qcloudimg.com/raw/e86896cc8286b53e8198facc8d28076f.png)
Quando o CLB IPv6 NAT64 é acessado de uma rede IPv6, o CLB pode converter com facilidade os endereços IPv6 em endereços IPv4 para se adaptar aos serviços existentes e implementar rapidamente a transformação IPv6.

### Vantagens do CLB IPv6 NAT64
O CLB IPv6 NAT64 do Tencent Cloud tem as seguintes vantagens ao ajudar sua empresa a se conectar rapidamente ao IPv6:
- **Conexão rápida:** o CLB permite a conexão ao IPv6 em questão de segundos e fica disponível no momento da aquisição.
- **Transição de negócios descomplicada:** para fazer o trânsito de seus negócios para IPv6 sem complicações, basta transformar o cliente, sem a necessidade de modificações para servidores de back-end. O CLB IPv6 NAT64 aceita o acesso de clientes IPv6 e converte mensagens IPv6 em IPv4. A transição para IPv6 é imperceptível a aplicativos em servidores de back-end, que ainda funcionam em sua forma original.
- **Fácil de usar:** o CLB IPv6 NAT64 é compatível com o processo de operação do CLB IPv4 e é fácil de usar, sem custos adicionais de aprendizagem.

## Guia de operação
### Criação de uma instância do CLB IPv6 NAT64
1. Faça login no site oficial do Tencent Cloud e acesse a [página de aquisição do CLB](https://buy.cloud.tencent.com/lb?rid=1&type=2&vpcId=vpc-k9gii1kb).
2. Selecione as opções para os seguintes parâmetros corretamente:
 - Region (Região): apenas Pequim, Xangai e Guangzhou são aceitas.
 - Instance Type (Tipo de instância): CLB.
 - Network Type (Tipo de rede): rede pública.
 - IP Version (Versão do IP): IPv6 NAT64.
 - Network (Rede): VPC.
 - As demais configurações são iguais às configurações gerais da instância.
3. Depois de definir os itens de configuração na página de aquisição, clique em **Buy Now (Comprar agora)** para retornar à [página da lista de instâncias do CLB](https://console.cloud.tencent.com/loadbalance/index?rid=1&forward=1), na qual você pode exibir a instância do CLB IPv6 NAT64 recém-adquirida.

### Uso do CLB IPv6 NAT64
Faça login no [Console do CLB](https://console.cloud.tencent.com/loadbalance/index?rid=1&forward=1) e clique no ID de uma instância para acessar a página de detalhes. Na guia "Listener Management (Gerenciamento de listener)", é possível configurar listeners e regras de encaminhamento, além de vincular instâncias do CVM. Para obter mais informações, consulte [Introdução ao CLB](https://intl.cloud.tencent.com/document/product/214/8975).
![](https://main.qcloudimg.com/raw/2cacac7c34a7fa241dbd6f9127570391.png)
