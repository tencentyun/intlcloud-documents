Este documento descreve como criar, em rede pública, uma instância clássica do CLB chamada `clb-test` e encaminhar solicitações de clientes para dois servidores de back-end.

## Pré-requisitos
1. O CLB apenas encaminha o tráfego e não pode processar solicitações; portanto, você precisa ter uma instância do CVM que processa as solicitações do usuário.
Neste exemplo, duas instâncias do CVM são suficientes, mas você também pode configurar mais instâncias. Neste exemplo, as instâncias do CVM `rs-1` e `rs-2` foram criadas na região de Guangzhou. Para obter mais informações sobre como criar uma instância do CVM, consulte [Aquisição e iniciação das instâncias do CVM](https://intl.cloud.tencent.com/document/product/213/4855).
2. Este documento usa o encaminhamento de HTTP como exemplo. O servidor da web correspondente (como Apache, Nginx ou IIS) deve ser implementado na instância do CVM.
Para verificar o resultado, neste exemplo, o Apache é implementado em `rs-1` e `rs-2`. O Apache retorna "Hello Tomcat! This is rs-1!" em `rs-1` e "Hello Tomcat! This is rs-2!" em `rs-2`. Para obter mais informações sobre como implementar componentes em uma instância do CVM, consulte [Implementação Java Web no Linux (CentOS)](https://intl.cloud.tencent.com/document/product/214/32391) e [Instalação e configuração PHP no Windows](https://intl.cloud.tencent.com/document/product/213/10182).
3. Acesse o IP público e o caminho de suas instâncias do CVM. Se a página implementada for exibida, a implementação do serviço foi bem-sucedida.
>!
> - Para contas tradicionais, a largura de banda da rede pública deve ser adquirida para as instâncias do CVM, pois a largura de banda é cobrada pelo CVM, não pelo CLB. Você pode determinar o tipo de conta conforme as instruções em [Visão geral do faturamento](https://intl.cloud.tencent.com/document/product/214/36999).
> - Neste exemplo, os valores retornados pelo serviço implementado em dois servidores de back-end são diferentes. Em cenários reais, para garantir que todos os usuários tenham uma experiência uniforme, geralmente o mesmo serviço deve ser implementado em todos os servidores de back-end.

## Aquisição de instância clássica do CLB
1. Faça login no site oficial do Tencent Cloud e acesse a [página de aquisição do CLB](https://buy.cloud.tencent.com/lb).
2. Neste exemplo, selecione **Guangzhou** como a região, que é a mesma das instâncias do CVM. Selecione **Classic (Clássico)** como o tipo de instância, **Public Network (Rede pública)** como o atributo de rede e **Default-VPC (Default) (VPC padrão (padrão))** como a rede e insira "clb-test" como o nome da instância.
3. Clique em **Buy Now (Comprar agora)** e efetue o pagamento. Para obter mais informações sobre as instâncias do CLB, consulte [Seleção de atributos do produto](https://intl.cloud.tencent.com/document/product/214/13629).
4. Na página "CLB Instance List (Lista de instâncias do CLB)", selecione a região correspondente para visualizar a instância recém-criada.
![](https://main.qcloudimg.com/raw/183ac407a68c4aafe440aa2c111a154e.png)

## Criação do listener CLB
Um listener CLB encaminha solicitações especificando protocolos e portas. Este documento usa a configuração de encaminhamento de solicitações de cliente HTTP por CLB como um exemplo.
1. Faça login no [Console do CLB](https://console.cloud.tencent.com/clb/index?rid=1&type=2%2C3).
2. Na "CLB Instance List (Lista de instâncias do CLB)", encontre a instância clássica do CLB criada `clb-test` e clique na respectiva ID para entrar em sua página de detalhes.
3. Na seção "Basic Info (Informações básicas)", você pode clicar em "Edit (Editar)" ao lado do nome da instância para renomeá-la.
4. Em **Listeners** em "Listener Management (Gerenciamento de listener)", clique em **Create (Criar)** para criar um listener do CLB.
![](https://main.qcloudimg.com/raw/df7de6ac8996718bc5176b14f25cd3cb.png)
5. Na caixa pop-up, configure o seguinte:
  - Defina o nome como "Listener1".
  - Defina o protocolo do listener e a porta como `HTTP:80`.
  - Defina a porta de back-end para `80`.
  - Selecione "WRR" como o modo de balanceamento de carga.
  - Não verifique a persistência da sessão.
  - Ative a verificação de integridade.
  ![](https://main.qcloudimg.com/raw/41cbc18c096ed2f6c01a238dc426963e.png)
6. Clique em **Complete (Concluir)** para criar o listener do CLB.

Para obter mais informações sobre listeners do CLB, consulte [Visão geral do listener do CLB](https://intl.cloud.tencent.com/document/product/214/6151).

## Vinculação do servidor de back-end
1. Na "CLB Instance List (Lista de instâncias do CLB)", encontre o `clb-test` criado e clique na respectiva ID para entrar em sua página de detalhes.
2. No módulo "Bind Real Server (Vincular servidor de back-end)" em "Listener Management (Gerenciamento de listener)", clique em **Bind (Vincular)**.
![](https://main.qcloudimg.com/raw/a1c1ba2fa1b95a27a534a2446c381fc3.png)
3. Na caixa pop-up, selecione as instâncias CVM `rs-1` e` rs-2` na mesma região da instância do CLB e mantenha o peso padrão delas em "10".
4. Clique em **OK** para concluir a vinculação.
![](https://main.qcloudimg.com/raw/0c9f911e40621ff3615ac47d94651329.png)
5. Expanda o listener **Listener1**. Você pode visualizar o status de verificação de integridade da instância do CVM de back-end. O status "Healthy" (Íntegro) indica que a instância do CVM pode processar adequadamente as solicitações encaminhadas pelo CLB.


## Configuração de grupo de segurança
Depois de criar uma instância do CLB, você pode configurar um grupo de segurança do CLB para isolar o tráfego da rede pública. Para obter mais informações, consulte [Configuração de grupos de segurança do CLB](https://intl.cloud.tencent.com/document/product/214/14733).
Após configurar um grupo de segurança, você pode escolher ativar ou desativar "Permitir tráfego por padrão em grupos de segurança" com diferentes configurações, como segue:

### Método 1. Habilite "Permitir tráfego por padrão em grupos de segurança"
>?Atualmente, essa funcionalidade está em teste beta. Para testá-la, envie um tíquete para solicitação. Esse recurso não é compatível com o CLB clássico em rede privada.
>
Para obter instruções detalhadas, consulte [Configuração de grupos de segurança do CLB](https://intl.cloud.tencent.com/document/product/214/14733).


### Método 2. Permitir IP de cliente no grupo de segurança do CVM
Para obter instruções detalhadas, consulte [Configuração de grupos de segurança do CLB](https://intl.cloud.tencent.com/document/product/214/14733).

## Verificação do serviço CLB
1. Insira o endereço do serviço CLB e a porta `http://vip:80` em um navegador para testar o serviço CLB. Se uma mensagem for exibida conforme mostrado abaixo, a solicitação foi encaminhada para a instância do CVM `rs-1` pelo CLB e a instância do CVM processou corretamente a solicitação e retornou o resultado.
![](https://main.qcloudimg.com/raw/5a7cb3e86d04149978b90050546a2983.png)
2. O algoritmo round robin do listener é "round robin ponderado" e os pesos das duas instâncias do CVM são ambos "10". Se você atualizar a página da web no navegador para enviar uma nova solicitação, você verá que a solicitação é encaminhada para a instância `rs-2` do CVM pelo CLB.
![](https://main.qcloudimg.com/raw/8f9f5f667461a5d0efd3e6b2bbe859f3.png)
>!
> - Se a persistência da sessão for desativada e um método round-robin for usado para a programação, as solicitações serão atribuídas a diferentes servidores de back-end em sequência.
> - Se a persistência da sessão estiver habilitada, ou se estiver desativada, mas a programação ip_hash for usada, as solicitações sempre serão atribuídas ao mesmo servidor de back-end.
