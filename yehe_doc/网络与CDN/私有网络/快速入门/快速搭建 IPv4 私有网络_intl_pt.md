## Cenários de operação
Considerando as redes necessárias na implantação de um CVM com acesso à internet como exemplo, este documento explica cada etapa em detalhes, desde a criação de um VPC e uma sub-rede, até a aquisição de um CVM, a atribuição de um endereço IP público e, por último, o uso de um grupo de segurança para controlar o tráfego de entrada e saída do CVM.
![](https://main.qcloudimg.com/raw/82eefc24e8eeded09773ef7a5b6ab077.png)

## Pré-requisitos
1. Antes de usar os produtos do Tencent Cloud, é necessário [criar uma conta do Tencent Cloud](https://intl.cloud.tencent.com/register).
2. Confirme a [região e zona de disponibilidade](https://intl.cloud.tencent.com/document/product/215/31786) em que o VPC deve ser implantado com base em seus requisitos de negócios.
3. Compreenda as configurações básicas dos dois tipos de CVMs do Tencent Cloud: [Introdução aos CVMs do Linux](https://intl.cloud.tencent.com/document/product/213/2936) e [Introdução aos CVMs do Windows](https://intl.cloud.tencent.com/document/product/213/2764).

## Etapas
### Etapa 1: (Opcional) Crie um VPC e uma sub-rede.
Você pode criar um VPC e uma sub-rede personalizados ou pode pular esta etapa, optando por fazer com que o sistema crie automaticamente um VPC e uma sub-rede padrão ao adquirir o CVM.
Um VPC inclui pelo menos uma sub-rede. Quando um VPC for criado, o sistema criará uma sub-rede inicial e os recursos do serviço de nuvem só poderão ser adicionados à sub-rede.
As funcionalidades do VPC padrão são iguais às do VPC personalizado que você cria.

1. Faça login no [console do VPC](https://console.cloud.tencent.com/vpc).
2. Depois de selecionar a região do VPC na barra superior, clique em **+New (+Novo)**.
3. Insira as informações do VPC e da sub-rede inicial e clique em **OK**. Se você precisar de várias sub-redes, consulte [Criação de uma sub-rede](https://intl.cloud.tencent.com/document/product/215/31806#.E5.88.9B.E5.BB.BA.E5.AD.90.E7.BD.91).

>Os blocos CIDR (intervalos de IP) de instâncias e sub-redes do VPC não podem ser modificados depois de criados. Portanto, conclua o [planejamento da rede](https://intl.cloud.tencent.com/document/product/215/31795) com antecedência.

### Etapa 2: adquira um CVM.
1. Faça login no [console do CVM](https://console.cloud.tencent.com/cvm).
2. Clique em **Create (Criar)** no canto superior esquerdo da página da lista para acessar a página de aquisição do CVM.
3. Para obter informações sobre as configurações dos CVMs, consulte [Configuração personalizada do CVM no Linux](https://intl.cloud.tencent.com/document/product/213/10517) e [Configuração personalizada do CVM no Windows](https://intl.cloud.tencent.com/document/product/213/10516).
4. Selecione um VPC e uma sub-rede. Existem dois métodos de seleção:
- **Uso de VPC e sub-rede personalizados**
Em **1. Select the region and model (1. Selecione a região e o modelo)** em **Custom Configuration (Configuração personalizada)**, você pode selecionar o VPC e a sub-rede criados na Etapa 1 na opção **Network (Rede)**, e o CVM será criado no VPC e na sub-rede personalizados.

- **Uso de VPC e sub-rede padrão**
Em **1. Select the region and model (1. Selecione a região e o modelo)** em **Custom Configuration (Configuração personalizada)**, você pode selecionar o VPC padrão (Default-VPC) e a sub-rede (Default-subnet) na opção ***Network (Rede)**, e o CVM será criado no VPC e sub-rede padrão.


>Recomendamos que você atribua um endereço IP público gratuito ao adquirir um CVM. Se nenhum endereço IP público tiver sido atribuído durante a aquisição, é possível vincular o CVM a um endereço IP público elástico no console do CVM.

### Etapa 3: configure um grupo de segurança.
Ao adquirir um CVM, é possível selecionar o grupo de segurança padrão (Default) do sistema. Esse grupo de segurança permite todo o tráfego por padrão. É possível definir regras de grupo de segurança com base em suas necessidades.
1. Faça login no [console do CVM](https://console.cloud.tencent.com/cvm).
2. Clique em **Security Group (Grupo de segurança)** na barra lateral esquerda para acessar a página de gerenciamento.
3. Localize o grupo de segurança padrão na lista e clique em **Modify Rules (Modificar regras)**.
4. Modifique as regras de entrada e saída do grupo de segurança nesta página.

Para obter mais informações sobre como configurar regras de grupo de segurança, consulte [Criação de um grupo de segurança](https://intl.cloud.tencent.com/document/product/215/35506) e [Casos de uso de grupos de segurança](https://intl.cloud.tencent.com/document/product/215/35519).

### Etapa 4: configure uma tabela de rotas.
Quando terminar de configurar o CVM e o grupo de segurança, é necessário configurar a tabela de rotas associada à sub-rede.
1. Faça login no [console do VPC](https://console.cloud.tencent.com/vpc).
2. Clique em **Route Tables (Tabelas de rotas)** na barra lateral esquerda para acessar a página de gerenciamento.
3. Localize a tabela de rotas padrão do VPC padrão na lista e clique em seu ID para acessar a página de detalhes.
4. Clique em **+Add Routing Policy (+Adicionar política de roteamento)** em **Routing Policy (Política de roteamento)**.
5. Insira o intervalo de endereços IP de destino para acessar a internet e selecione **CVM's Public IP (IP público do CVM)** para o tipo de próximo salto. Isso indica que quando os CVMs na sub-rede vinculada a essa tabela de rotas acessarem esse intervalo de endereços IP, eles sempre usarão o endereço IP público do CVM.

>Você pode adquirir um NAT Gateway para fornecer acesso à internet aos CVMs sem endereços IP públicos. Para obter mais informações, consulte [NAT Gateways](https://intl.cloud.tencent.com/document/product/1015).
