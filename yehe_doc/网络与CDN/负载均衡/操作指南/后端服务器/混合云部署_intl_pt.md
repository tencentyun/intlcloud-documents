Em cenários de implantação de nuvem híbrida, é possível vincular diretamente as instâncias do CLB aos IPs no IDC local fora da nuvem para vinculá-los a servidores de back-end em VPCs e IDCs.
Atualmente, essa funcionalidade está em beta. Se você quiser usá-la para vinculação entre regiões fora da China Continental, [entre em contato com seu representante do Tencent Cloud](https://intl.cloud.tencent.com/contact-sales).

## Vantagens da solução
- Uma nuvem híbrida pode ser criada rapidamente para conectar os ambientes dentro e fora da nuvem. O CLB pode encaminhar solicitações para instâncias do CVM no VPC na nuvem e no IDC fora da nuvem ao mesmo tempo.
- Os recursos de acesso à rede pública de alta qualidade do Tencent Cloud podem ser reutilizados.
- As funcionalidades avançadas do CLB, como acesso à camada 4/7, verificação de integridade e persistência de sessão, podem ser reutilizadas.
- As redes privadas podem ser interconectadas entre si por meio do [CCN](https://intl.cloud.tencent.com/document/product/1003/30049), o roteamento de baixa granularidade é aceito para garantir a qualidade, e os preços diversificados em camadas são aceitos para reduzir os custos.
![](https://main.qcloudimg.com/raw/e09b0e4b6fcaedf44267f6ca1950ee54.png)	

## Limites
- Atualmente, a vinculação de instâncias do CVM entre redes não é aceita para instâncias do CLB clássico.
- Essa funcionalidade está disponível apenas para contas de faturamento por IP. Para verificar o seu tipo de conta, consulte [Verificação do tipo de conta](https://intl.cloud.tencent.com/document/product/684/15246).
- A vinculação entre regiões 2.0 e a implantação de nuvem híbrida não aceitam [Permitir tráfego por padrão em grupos de segurança](https://intl.cloud.tencent.com/document/product/214/14733), para o qual você precisa permitir o IP do cliente e a porta de serviço no servidor de back-end.
- No momento, essa funcionalidade é aceita apenas em Guangzhou, Shenzhen, Xangai, Jinan, Hangzhou, Pequim, Tianjin, Chengdu, Chongqing, Hong Kong (China), Singapura e Vale do Silício.
- Os listeners TCP e TCP SSL precisam usar TOA no servidor de back-end para obter o IP de origem. Para obter mais informações, consulte [Método de carregamento do módulo TOA](https://intl.cloud.tencent.com/document/product/608/18945).
- Os listeners HTTP e HTTPS precisam usar `X-Forwarded-For` (XFF) para obter o IP de origem.
- Os listeners UDP não podem obter o IP de origem.

## Pré-requisitos
1. Envie uma solicitação de qualificação para o teste beta. Para vinculação entre regiões na China Continental, envie um tíquete para solicitar. Para vinculação entre regiões fora da China Continental, [entre em contato com seu representante do Tencent Cloud](https://intl.cloud.tencent.com/contact-sales).
2. Crie uma instância do CLB. Para obter mais informações, consulte [Criação de instâncias do CLB](https://intl.cloud.tencent.com/document/product/214/6149).
3. Crie uma instância do CCN. Para obter mais informações, consulte [Criação de instâncias do CCN](https://intl.cloud.tencent.com/document/product/1003/30062).
4. Associe o gateway do Direct Connect associado ao IDC e o VPC em questão à instância do CCN criada. Para obter mais informações, consulte [Associação de instâncias de rede](https://intl.cloud.tencent.com/document/product/1003/30064).

## Instruções de procedimento
1. Faça login no [Console do CLB](https://console.cloud.tencent.com/loadbalance).
2. Na página **Instance Management (Gerenciamento de instâncias)**, clique no ID da instância do CLB em questão.
3. Na seção **Real Server (Servidor de back-end)** na guia **Basic Info (Informações básicas)**, clique em **Configure (Configurar)** para vincular um IP privado de outro VPC.
![](https://main.qcloudimg.com/raw/1214576094baa072eb1d3577a5f5781a.png)
4. Clique em **Submit (Enviar)** na caixa pop-up.
![](https://main.qcloudimg.com/raw/4f7b99a8532afabe54440ca7819dcd72.png)
5. Na seção **Real Server (Servidor de back-end)** na guia **Basic Info (Informações básicas)**, clique em **Add SNAT IP (Adicionar IP SNAT)**.
![](https://main.qcloudimg.com/raw/fc41b320241fa4de1d961e1a9c8d428f.png)
6. Na caixa pop-up, selecione **Subnet (Sub-rede)**, clique em **Add (Adicionar)** para atribuir um IP e clique em **Save (Salvar)**.
<img src="https://main.qcloudimg.com/raw/6aad8ac7d4a38a8e74ea7b3b59e36cbb.png" width="50%"/>
7. Na página de detalhes da instância, abra a guia **Listener Management (Gerenciamento de listener)** e vincule um servidor de back-end à instância do CLB na seção de configuração do listener. Para obter mais informações, consulte [Gerenciamento de servidores de back-end](https://intl.cloud.tencent.com/document/product/214/6156).
8. Na caixa pop-up, selecione **Other Private IP (Outro IP privado)**, clique em **Add a private IP (Adicionar um IP privado)**, insira o IP privado do IDC em questão, a porta e o peso e clique em **Confirm (Confirmar)**. Para obter mais informações sobre portas, consulte [Portas comuns do servidor](https://intl.cloud.tencent.com/document/product/213/12451).

9. Agora você pode exibir o IP privado do IDC vinculado na seção **Bound Real Servers (Vincular servidores de back-end)**.<br/>



