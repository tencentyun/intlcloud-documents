## B

### Servidor de borda

- No Content Delivery Network (CDN) do Tencent Cloud, um servidor de borda é um nó de rede que o CDN usa para armazenar em cache o conteúdo do seu servidor de origem para responder rapidamente às solicitações de usuários de regiões diferentes.
- No Global Content Delivery (GCD) do Tencent Cloud, um servidor de borda é um nó de rede que o GCD usa para armazenar em cache o conteúdo do seu servidor de origem para responder rapidamente às solicitações de usuários de regiões diferentes.
- No Edge Computing Machine (ECM) do Tencent Cloud, um servidor de borda é um IDC criado próximo à localização física do usuário e fornece recursos físicos básicos para a computação de borda.

## C

### Registro CNAME

Um registro CNAME (nome canônico) refere-se ao registro de alias na resolução de nomes de domínio.
Por exemplo, um servidor chamado `host.example.com` fornece serviços WWW e MAIL. Para facilitar o acesso dos usuários aos serviços, dois registros CNAME podem ser adicionados para este servidor (`www.example.com` e `mail.example.com`) em seu provedor de serviços de DNS, e todas as solicitações de acesso a esses dois CNAMEs serão encaminhadas para `host.example.com`.

### Nome de domínio do CNAME

- No CDN, um nome de domínio do CNAME é um nome de domínio com o sufixo `.cdn.dnsv1.com` que é atribuído pelo sistema ao nome de domínio de aceleração conectado, configurado no console do CDN. É necessário configurar um registro CNAME em seu provedor de serviços de nomes de domínio. Após o registro entrar em vigor, o CDN cuidará da resolução de nomes de domínio e todas as solicitações feitas a esse nome de domínio serão encaminhadas aos servidores de borda do CDN.
- No GCD, um nome de domínio do CNAME é um nome de domínio com o sufixo `.cdn.dnsv1.com` que é atribuído pelo sistema ao nome de domínio de aceleração conectado, configurado no console do GCD. É necessário configurar um registro CNAME em seu provedor de serviços de nomes de domínio. Após o registro entrar em vigor, o GCD cuidará da resolução de nomes de domínio e todas as solicitações feitas a esse nome de domínio serão encaminhadas aos servidores de borda do GCD.
- No Enterprise Content Delivery Network (ECDN) do Tencent Cloud, um nome de domínio do CNAME é um nome de domínio com o sufixo `.ecdn.dnsv1.com` que é atribuído pelo sistema ao nome de domínio de aceleração conectado configurado no console do ECDN. É necessário configurar um registro CNAME em seu provedor de serviços de nomes de domínio. Após o registro entrar em vigor, a resolução de nomes de domínio será tratada pelo ECDN e todas as solicitações feitas a esse nome de domínio serão encaminhadas aos nós do ECDN.

## D

### Conteúdo dinâmico

Isso se refere à quando os usuários fazem várias solicitações para o mesmo recurso, o conteúdo retornado varia, como APIs e arquivos .jsp, .asp, .php, .perl e .cgi.

## F

### Log de acesso

No CDN, um log de acesso se refere ao log detalhado das solicitações de acesso do usuário ao seu nome de domínio, incluindo tempo da solicitação, IP do cliente, nome do domínio de acesso, caminho do arquivo, número de bytes, código do distrito, código do ISP, código de status HTTP, referencial, tempo de solicitação, agente do usuário (UA), intervalo, método HTTP, identificador de protocolo e acertos/erros do cache.

## H

### Pull de origem

No CDN, um pull de origem significa que, quando um usuário envia uma solicitação de um navegador, o servidor que responde à solicitação é o servidor do site de origem, em vez de um servidor de cache em um nó do CDN. Geralmente, se o conteúdo não for armazenado em cache no servidor de cache ou for modificado no servidor de origem, será efetuado o pull do servidor de origem.

### Cabeçalho de host

No CDN, um cabeçalho de host se refere à um nome de domínio de um site acessado em um servidor de origem por um nó do CDN durante o pull de origem. Para obter mais informações, consulte [Configuração do cabeçalho de host](https://intl.cloud.tencent.com/document/product/228/6293).

## J

### Conteúdo estático

Isso se refere à quando os usuários fazem várias solicitações para o mesmo recurso, o conteúdo retornado permanece o mesmo, como arquivos html, css e js, imagens, vídeos, pacotes de instalação de software, arquivos APK e arquivos compactados.

## M

### Taxa de acertos

No CDN, a taxa de acertos é a porcentagem de solicitações de acertos em relação à quantidade total de solicitações. Quando um usuário final usa o serviço do CDN para acessar um recurso, se o recurso acessado já tiver sido armazenado em cache em um nó do CDN, ele pode ser retornado diretamente ao usuário final, o que é chamado de "acerto". Caso contrário, ele precisa ser recuperado do servidor de origem, o que é chamado de "erro".

## S

### Latência

Isso se refere ao tempo que os dados levam para se mover de uma ponta à outra da rede.

## Y

### Nome de domínio

Um nome de domínio é um conjunto de endereços de servidor fáceis de lembrar e usar pelos usuários, que podem ser um site, e-mail, FTP, etc. É usado para identificar a localização eletrônica (às vezes chamada de localização geográfica) de um computador durante a transferência de dados.

## Z

### Servidor intermediário

Este é um servidor de pull de origem na camada intermediária entre um servidor empresarial (servidor de origem) e um servidor de borda. Ele pode armazenar em cache as solicitações de pull de origem de vários servidores de borda. Para solicitações que possuem o mesmo conteúdo, o servidor intermediário só precisa realizar um pull de origem para entregar o conteúdo a cada servidor de borda, reduzindo a pressão de acesso no servidor empresarial (servidor de origem).

### Servidor de origem próprio

Refere-se à um servidor onde seu próprio serviço Web foi implantado. Ao conectar-se a um nome de domínio de aceleração, é possível inserir o endereço IP público do servidor como o servidor de origem.