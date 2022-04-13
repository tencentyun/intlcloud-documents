

### Servidor de origem
Refere-se ao seu servidor de negócios em execução estável. No console do CDN, é possível selecionar um servidor externo ou COS como o servidor de origem.

### Origem externa
Refere-se a um servidor em que seu próprio serviço da web é implantado. Ao conectar-se a um nome de domínio de aceleração, é possível inserir o endereço IP público do servidor como o servidor de origem.

### Origem do COS
Se os recursos já foram armazenados no COS, um bucket pode ser selecionado como o servidor de origem.

### Servidor de borda
Refere-se a um nó de rede que o CDN usa para armazenar em cache o conteúdo do seu servidor de origem a fim de responder rapidamente às solicitações de usuários de regiões diferentes.

### Registro CNAME
Um registro CNAME (nome canônico) refere-se ao registro de alias em uma resolução de nomes de domínio.
Por exemplo, um servidor chamado `host.example.com` fornece serviços WWW e MAIL. Para facilitar o acesso dos usuários a esses serviços, dois registros CNAME (`www.example.com` e `mail.example.com`) podem ser adicionados para este servidor em seu provedor de serviços de DNS, e todas as solicitações de acesso a esses dois registros CNAME serão encaminhadas para `host.example.com`.

### Nome de domínio do CNAME
Refere-se a um nome de domínio com o sufixo `.cdn.dnsv1.com` que é atribuído pelo sistema ao nome de domínio de aceleração conectado configurado no console do CDN. É necessário configurar um registro CNAME em seu provedor de serviços de nomes de domínio. Após o registro entrar em vigor, o CDN cuidará da resolução de nomes de domínio e todas as solicitações feitas a esse nome de domínio serão encaminhadas aos servidores de borda do CDN.

### Conteúdo estático
Refere-se ao conteúdo que permanece o mesmo nas respostas a várias solicitações do mesmo recurso.
Exemplos incluem arquivos html, css e js, imagens, vídeos, pacotes de instalação de software, arquivos APK e arquivos compactados.

### Conteúdo dinâmico
Refere-se ao conteúdo que varia nas respostas a várias solicitações para o mesmo recurso.
Exemplos incluem: APIs e arquivos .jsp, .asp, .php, .perl e .cgi.

### Pull de origem
No CDN, um pull de origem significa que, quando um usuário envia uma solicitação de um navegador, o servidor que responde à solicitação é o servidor do site de origem, em vez de um servidor de cache em um nó do CDN. Geralmente, se o conteúdo não for armazenado em cache no servidor de cache ou for modificado no servidor de origem, será efetuado o pull do servidor de origem.

### Domínio de origem
Refere-se ao nome de domínio do site acessado no servidor de origem por um nó do CDN durante o pull de origem. Para obter mais informações, consulte [configuração do servidor de origem](https://intl.cloud.tencent.com/document/product/228/6289).

### Nome de domínio
Refere-se a um conjunto de endereços de servidor dos quais os usuários podem lembrar e usar facilmente, e pode ser um site, e-mail, FTP, etc. É usado para identificar a localização eletrônica de um computador (às vezes chamada de localização geográfica) durante a transferência de dados.


### Bucket
No COS, um bucket serve para armazenar um objeto ou vários objetos. Um nome de bucket é uma string definida pelo usuário que conecta uma string numérica gerada pelo sistema com um traço, garantindo assim que esse nome de bucket seja exclusivo. Para obter mais informações, consulte a [Visão geral sobre bucket](https://intl.cloud.tencent.com/document/product/436/13312).
