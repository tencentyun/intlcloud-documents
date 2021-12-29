

### Quantidade máxima de conexões simultâneas

Refere-se à quantidade máxima de conexões de acesso simultâneas aceitas por uma conexão do GAAP.



### Registro CNAME

Um registro CNAME (nome canônico) refere-se ao registro de alias em uma resolução de nomes de domínio.
Por exemplo, um servidor chamado `host.example.com` fornece serviços WWW e MAIL. Para facilitar o acesso dos usuários a esses serviços, dois registros CNAME (`www.example.com` e `mail.example.com`) podem ser adicionados para este servidor em seu provedor de serviços de DNS, e todas as solicitações de acesso a esses dois registros CNAME serão encaminhadas para `host.example.com`.



### GAAP

Para obter mais informações, consulte [Global Application Acceleration Platform](#GAAP1).



### Listener

Um listener é usado para fornecer funcionalidades de configuração para a política de encaminhamento de solicitações, incluindo a configuração de protocolos, portas, políticas de programação entre vários servidores de origem e verificações de integridade. As solicitações serão encaminhadas ao servidor de origem de back-end de acordo com a política configurada em um listener.

### Região de aceleração

Refere-se à região onde os usuários estão localizados. Os usuários em regiões de aceleração podem acessar os servidores empresariais na região do servidor de origem por meio de conexões de aceleração.


<span ="GAAP1"></span>
### Global Application Acceleration Platform

O Global Application Acceleration Platform (GAAP) do Tencent Cloud é um produto PaaS que atinge a latência de acesso global ideal. Ele usa conexões de alta velocidade, encaminhamento de cluster e roteamento inteligente entre nós globais para permitir que usuários em regiões diferentes acessem os nós mais próximos, para que o tráfego de solicitações possa ser encaminhado para os servidores de origem, reduzindo o atraso no acesso e a latência.



### Servidor de origem

É um servidor empresarial do cliente e pode ser um servidor autocriado ou um bucket do [COS](https://intl.cloud.tencent.com/product/cos) do Tencent Cloud.
