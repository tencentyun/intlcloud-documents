O CLB do Tencent Cloud é disponibilizado com vários protocolos, como TCP, UDP, TCP SSL, HTTP e HTTPS, oferecendo às empresas nomes de domínio e serviços de encaminhamento baseados em URL. Este documento orienta você a criar rapidamente uma instância do CLB e encaminhar solicitações de cliente para duas instâncias do CVM.

## Pré-requisitos
1. Você criou duas instâncias do CVM (este documento considera **rs-1** e **rs-2** como duas instâncias de amostra). Para obter informações sobre como criar instâncias do CVM, consulte [Criação de instâncias pela página de aquisição do CVM](https://intl.cloud.tencent.com/document/product/213/4855).
2. Você implementou serviços de back-end nas duas instâncias do CVM. Este documento usa o encaminhamento de HTTP como exemplo. Os servidores Nginx foram implementados nas instâncias **rs-1** e **rs-2** do CVM e as duas instâncias retornaram duas páginas estáticas HTML dizendo "Hello Nginx! This is rs-1!" e "Hello Nginx! This is rs-2!". Para obter mais informações, consulte [Implementação do Nginx no CentOS](https://intl.cloud.tencent.com/document/product/214/32390).
>!
> - Este documento descreve as etapas para contas de faturamento por IP. Para contas de faturamento por CVM, primeiro adquira largura de banda de rede pública para instâncias de CVM. Se você não tiver certeza do seu tipo de conta, consulte [Verificação do tipo de conta](https://intl.cloud.tencent.com/document/product/684/15246).
> - Neste exemplo, diferentes serviços implementados em servidores de back-end retornarão valores diferentes. Na prática, os serviços implementados em servidores de back-end são idênticos para fornecer uma experiência consistente para todos os usuários.

## Etapa 1: Aquisição de uma instância do CLB
Após uma aquisição bem-sucedida, o sistema atribuirá automaticamente um VIP à instância do CLB. O VIP será usado como o endereço IP para fornecer serviços aos clientes.
1. Faça login no console do Tencent Cloud e vá para a [página de aquisição do CLB](https://buy.cloud.tencent.com/lb).
2. Primeiro, selecione a mesma região da sua instância do CVM. Em seguida, selecione **Cloud Load Balancer** como o tipo de instância, **Public Network (Rede pública)** como o tipo de rede. Para obter mais detalhes, consulte [Seleção de atributos do produto](https://intl.cloud.tencent.com/document/product/214/13629).
>?O teste beta de IP estático de linha única está disponível apenas em Jinan, Hangzhou, Fuzhou, Shijiazhuang, Wuhan e Changsha. É possível enviar uma solicitação para usá-lo. Uma vez permitido, você pode selecionar um ISP (China Mobile, China Unicom ou China Telecom) na página de aquisição. Se quiser experimentar em Guangzhou, Xangai, Nanjing, Pequim, Chengdu e Chongqing, entre em contato com seu representante de vendas.
>
3. Clique em **Buy Now (Comprar agora)** e efetue um pagamento.
4. Volte para a página **Instance Management (Gerenciamento de instâncias)**, selecione a região para ver a nova instância.
![](https://main.qcloudimg.com/raw/2c2afd943a9f6a6d03f55c00e62da8b5.png)

## Etapa 2: Configuração de um listener do CLB
O listener do CLB é usado para encaminhar por meio de um protocolo e porta especificados. Este documento demonstra como configurar uma instância do CLB para encaminhar solicitações HTTP do cliente.
### Configurar o protocolo e porta de escuta HTTP
Quando um cliente inicia uma solicitação, a instância CLB receberá a solicitação de acordo com o protocolo e a porta do front-end de escuta e encaminhará a solicitação para o servidor de back-end.
1. Faça login no [Console do CLB](https://console.cloud.tencent.com/clb/index?rid=1&type=2%2C3).
2. Na página **Instance Management (Gerenciamento de instâncias)**, clique em **Configure Listener (Configurar listener)** na coluna **Operation (Operação)** da instância do CLB de destino.
3. Na guia **Listener Management (Gerenciamento de listener)**, clique em **Create (Criar)** em **HTTP/HTTPS Listener (Listener HTTP/HTTPS)**.
![](https://main.qcloudimg.com/raw/782c60eeb4bf9aa334e4243cf4e068d5.png)
4. Na janela **Create Listener (Criar listener)**, configure os seguintes itens e clique em **Submit (Enviar)**.
  - Nome do listener.
  - Porta de protocolo de escuta (por exemplo, **HTTP:80**).

### Configurar a regra de encaminhamento do listener
Se um cliente iniciar uma solicitação, a instância do CLB irá encaminhá-la de acordo com a configuração da regra de encaminhamento do listener.
1. Na guia **Listener Management (Gerenciamento de listener)**, clique em **+** à direita do novo listener.
![](https://main.qcloudimg.com/raw/f8ab76b69f8a0cfdd5b4332c8b80b1f2.png)
2. Na janela **Create Forwarding Rules (Criar regras de encaminhamento)**, configure nome do domínio, URL, método de balanceamento e clique em **Next (Avançar)**.
  - Nome de domínio: o nome de domínio de seu servidor de back-end (por exemplo, **www.example.com**).
  - Nome de domínio padrão: se uma solicitação do cliente não corresponder a nenhum nome de domínio do listener, a instância do CLB encaminhará a solicitação para o nome de domínio padrão (servidor padrão). Cada listener pode ser configurado com apenas um nome de domínio padrão. Se um listener não tiver um nome de domínio padrão, a instância do CLB encaminhará a solicitação para o primeiro nome de domínio. Este exemplo irá pular a etapa de configuração.
  - URL: o caminho de acesso ao seu servidor de back-end (por exemplo, `/image/`).
  - Selecione **Weighted Round Robin** (Round robin ponderado) como método de balanceamento e clique em **Next (Avançar)**. Para obter mais informações, consulte [Métodos de balanceamento de carga](https://intl.cloud.tencent.com/document/product/214/6153).
![](https://main.qcloudimg.com/raw/263b2486f8a5734ea8aa643ea3b34387.png)
3. Ative a verificação de integridade. Use os valores padrão para os campos de verificação de domínio e caminho e clique em **Next (Avançar)**.
![](https://main.qcloudimg.com/raw/9d8c9bbe1191340e452e9feeafb20e73.png)
4. Desative a persistência da sessão e clique em **Submit (Enviar)**.

Para obter mais informações sobre listeners do CLB, consulte [Visão geral do listener do CLB](https://intl.cloud.tencent.com/document/product/214/6151).
>?
>- Regras de encaminhamento: cada listener pode ser configurado com vários nomes de domínio e cada nome de domínio pode ser configurado com vários URLs. Você pode selecionar um listener ou nome de domínio e clicar no ícone **+** para criar novas regras.
>- Persistência da sessão: se a persistência da sessão estiver desativada e um método round-robin for selecionado, as solicitações do mesmo cliente serão atribuídas a diferentes servidores de back-end em sequência; se a persistência da sessão estiver ativada, ou desativada, mas o método de balanceamento `ip_hash` for usado, as solicitações do mesmo cliente sempre serão atribuídas ao mesmo servidor de back-end.

### Vincular servidores de back-end ao listener
Se um cliente iniciar uma solicitação, a instância do CLB encaminhará a solicitação à instância do CVM que está vinculada ao seu listener para processamento.
1. Na guia **Listener Management (Gerenciamento de listener)**, clique em **+** para expandir o novo listener. Clique no URL e em **Bind (Vincular)** na seção **Forwarding Rules (Regras de encaminhamento)** à direita.
![](https://main.qcloudimg.com/raw/ad3bab63556a4340792b1d5dadcc1b19.png)
2. Na janela pop-up, selecione **CVM** como o tipo de instância, selecione as duas instâncias do CVM **rs-1** e **rs-2** (que estão na mesma região que a instância do CLB) , defina suas portas como **80** e pesos como **10** (o valor padrão) e clique em **Confirm (Confirmar)**.
![](https://main.qcloudimg.com/raw/02a6cf1b63726a7133f97f5f56c10d74.png)
3. [](id: qrjkjc)Agora você pode visualizar as instâncias vinculadas do CVM e seu status de verificação de integridade na seção **Forwarding Rules (Regras de encaminhamento)**. Se o status de saúde da porta for **Healthy (Íntegro)**, a instância do CVM pode normalmente processar solicitações encaminhadas por instâncias do CLB.
![](https://main.qcloudimg.com/raw/8ef5732d0748b73dd1d71b3ab0aed1d4.png)
>!Uma regra de encaminhamento (protocolo de escuta, porta, nome de domínio e URL) pode ser vinculada a várias portas da mesma instância do CVM. Se um usuário implantar o mesmo serviço na porta **80** e **81** da **rs-1**, ambas as portas podem ser vinculadas à regra de encaminhamento de amostra e ambas receberão solicitações encaminhadas pela instância do CLB.

## Etapa 3: Configuração de um grupo de segurança
Depois de criar uma instância do CLB, você pode configurar um grupo de segurança do CLB para isolar o tráfego da rede pública. Para obter mais informações, consulte [Configuração de grupos de segurança do CLB](https://intl.cloud.tencent.com/document/product/214/14733).

Depois de configurar um grupo de segurança, você pode ativar ou desativar o recurso **Allow Traffic by Default (Permitir tráfego por padrão)**:
### Método 1: Habilite "Permitir tráfego por padrão em grupos de segurança"
Para obter mais informações, consulte [Configuração de grupos de segurança do CLB](https://intl.cloud.tencent.com/document/product/214/14733).

### Método 2: Permitir IPs de cliente específicos no grupo de segurança do CVM
Para obter mais informações, consulte [Configuração de grupos de segurança do CLB](https://intl.cloud.tencent.com/document/product/214/14733).

## Etapa 4: Verificação do serviço do CLB
Depois de configurar uma instância do CLB, é possível verificar se ela é eficaz acessando diferentes servidores de back-end por meio de diferentes **nomes de domínio e URLs** na mesma instância do CLB ou verificando o recurso **Roteamento baseado em conteúdo**.
### Método 1: Configurar `hosts` e mapear o nome de domínio para a instância do CLB
1. Em um dispositivo Windows, modifique o arquivo **hosts** no diretório `C:\Windows\System32\drivers\etc`, e mapeie o nome de domínio para o VIP da instância do CLB.
![](https://main.qcloudimg.com/raw/b12ee22250cb7c24d5e12ecb803e6355.png)
2. Para verificar se os **hosts** foram configurados com êxito, você pode executar um comando **ping** no **cmd.exe** para testar se o nome de domínio foi vinculado com êxito ao VIP. Se houver pacotes de dados retornados, eles foram vinculados com êxito.
![](https://main.qcloudimg.com/raw/b11b20840cba86bedbaffaa424b4e021.png)
3. Teste o serviço do CLB acessando http://www.example.com/image/ por meio de um navegador. Se sua página retornar a imagem abaixo, então a solicitação foi encaminhada ao CVM rs-1 pela instância do CLB e o CVM processou, normalmente, a solicitação e retornou a página do serviço.
![](https://main.qcloudimg.com/raw/cf61264a9406d141650ed79da21c6859.png)
4. Como o método de balanceamento do listener é ponderado round robin e os pesos das duas instâncias do CVM são 10, é possível atualizar o navegador para iniciar a solicitação novamente. Caso sua página retorne a imagem abaixo, a solicitação foi encaminhada ao CVM rs-2 pela instância do CLB.
![](https://main.qcloudimg.com/raw/ab7db7b5c3952739919ae6e271bb1348.png)
>! O **/** em ***image/** não pode ser omitido. **/** indica que **image** é um diretório padrão em vez de um nome de arquivo.

## Configuração do redirecionamento (opcional)
O CLB oferece suporte a redirecionamento automático e redirecionamento manual. Para obter mais informações, consulte [Configuração do redirecionamento na camada 7](https://intl.cloud.tencent.com/document/product/214/8839).
- Redirecionamento automático (HTTPS forçado): quando um PC ou navegador móvel acessa um serviço web com uma solicitação HTTP, uma resposta HTTPS é retornada ao navegador após a solicitação passar pelo proxy do CLB, forçando o navegador a acessar a página da web usando HTTPS.
- Redirecionamento manual: se você deseja desativar temporariamente seu negócio na web em casos de produtos esgotados, manutenção de página ou atualização e upgrade, é necessário redirecionar a página original para uma nova página. Caso contrário, o endereço antigo nos favoritos do visitante e no banco de dados do mecanismo de pesquisa retornará uma página de mensagem de erro 404 ou 503, degradando a experiência do usuário, resultando em desperdício de tráfego e até mesmo invalidando as pontuações acumuladas nos mecanismos de pesquisa.


## Operações relevantes
- [Implementação Java Web no CentOS](https://intl.cloud.tencent.com/document/product/214/32391) 
- [Instalação e configuração do PHP](https://intl.cloud.tencent.com/document/product/213/10182)
